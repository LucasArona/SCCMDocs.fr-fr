---
title: Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI
titleSuffix: Configuration Manager
description: Découvrez comment personnaliser une séquence de tâches de déploiement de système d’exploitation afin de préparer une partition FAT32 pour la transition vers UEFI.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bd3df04a-902f-4e91-89eb-5584b47d9efa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bd1181bd14779a6ac659927979185aa174203206
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420173"
---
# <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI
Windows 10 fournit de nombreuses nouvelles fonctionnalités de sécurité qui requièrent des appareils compatibles UEFI. Certains PC Windows modernes prennent en charge UEFI tout en utilisant un BIOS hérité. Pour convertir un appareil en UEFI, vous devez repartitionner le disque dur et reconfigurer le microprogramme de chaque PC. À l’aide des séquences de tâches de Configuration Manager, vous pouvez préparer un disque dur en vue de conversion du BIOS en UEFI, convertir du BIOS en UEFI dans le cadre de la mise à niveau sur place et collecter des informations UEFI dans le cadre de l’inventaire matériel.

## <a name="hardware-inventory-collects-uefi-information"></a>L’inventaire matériel collecte des informations UEFI
Depuis la version 1702, une nouvelle classe d’inventaire matériel (**SMS_Firmware**) et une nouvelle propriété (**UEFI**) sont disponibles pour vous aider à déterminer si un ordinateur démarre ou non en mode UEFI. Quand un ordinateur démarre en mode UEFI, la propriété **UEFI** est définie sur **TRUE**. Cette option est activée dans l’inventaire matériel par défaut. Pour plus d’informations sur l’inventaire matériel, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="create-a-custom-task-sequence-to-prepare-the-hard-drive-for-bios-to-uefi-conversion"></a>Créer une séquence de tâches personnalisée pour préparer le disque dur en vue de la conversion du BIOS en UEFI
À partir de Configuration Manager version 1610, vous pouvez maintenant personnaliser une séquence de tâches de déploiement de système d’exploitation avec une nouvelle variable, TSUEFIDrive, afin que l’étape **Redémarrer l’ordinateur** prépare une partition FAT32 sur le disque dur pour la transition vers UEFI. La procédure suivante fournit un exemple de création des étapes de séquence de tâches pour préparer le disque dur pour la conversion du BIOS en UEFI.

### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Pour préparer la partition FAT32 pour la conversion en UEFI :
Dans une séquence de tâches existante pour installer un système d’exploitation, vous allez ajouter un nouveau groupe avec les étapes permettant d’effectuer la conversion du BIOS en UEFI.

1. Créez un groupe de séquences de tâches après les étapes de capture des fichiers et paramètres, et avant les étapes d’installation du système d’exploitation. Par exemple, créez un groupe après le groupe **Capturer les fichiers et les paramètres** nommé **BIOS-en-UEFI**.
2. Sous l’onglet **Options** du nouveau groupe, ajoutez une nouvelle variable de séquence de tâches comme condition où **_SMSTSBootUEFI** est **différent** de **true**. Vous empêchez ainsi l’exécution des étapes dans le groupe quand un ordinateur est déjà en mode UEFI.

   ![Groupe BIOS en UEFI](../../core/get-started/media/BIOS-to-UEFI-group.png)
3. Sous le nouveau groupe, ajoutez l’étape de séquence de tâches **Redémarrer l’ordinateur**. Dans **Spécifiez l’élément à exécuter après le redémarrage**, sélectionnez **L’image de démarrage attribuée à cette séquence de tâches** pour démarrer l’ordinateur dans Windows PE.  
4. Sous l’onglet **Options**, ajoutez une variable de séquence de tâches comme condition où **_SMSTSInWinPE est égal à False**. Vous empêchez ainsi l’exécution de cette étape si l’ordinateur est déjà dans Windows PE.

   ![Étape Redémarrer l’ordinateur](../../core/get-started/media/restart-in-windows-pe.png)
5. Ajoutez une étape pour démarrer l’outil OEM qui convertira le microprogramme du BIOS en UEFI. Il s’agit en général de l’étape de séquence de tâches **Exécuter la ligne de commande** avec une ligne de commande pour démarrer l’outil OEM.
6. Ajoutez l’étape de séquence de tâches Formater et partitionner le disque pour partitionner et formater le disque dur. Dans l’étape, procédez comme suit :
   1. Créez la partition FAT32 qui va être convertie en UEFI avant l’installation du système d’exploitation. Choisissez **GPT** pour **Type de disque**.
    ![Étape Formater et partitionner le disque](../media/format-and-partition-disk.png)
   2. Accédez aux propriétés de la partition FAT32. Entrez **TSUEFIDrive** dans le champ **Variable**. Quand la séquence de tâches détecte cette variable, elle prépare la transition vers UEFI avant le redémarrage de l’ordinateur.
    ![Propriétés de la partition](../../core/get-started/media/partition-properties.png)
   3. Créez une partition NTFS que le moteur de séquence de tâches utilise pour enregistrer son état et pour stocker les fichiers journaux.
7. Ajoutez l’étape de séquence de tâches **Redémarrer l’ordinateur**. Dans **Spécifiez l’élément à exécuter après le redémarrage**, sélectionnez **L’image de démarrage attribuée à cette séquence de tâches** pour démarrer l’ordinateur dans Windows PE.  

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Convertir du BIOS en UEFI pendant une mise à niveau sur place
Windows 10 Creators Update inclut un outil de conversion simple qui automatise le processus de repartitionnement du disque dur pour le matériel compatible UEFI et intègre l’outil de conversion dans le processus de mise à niveau sur place de Windows 7 vers Windows 10. Lorsque vous combinez cet outil avec la séquence de tâches de mise à niveau du système d’exploitation et l’outil OEM qui convertit le microprogramme du BIOS en UEFI, vous pouvez convertir vos ordinateurs du BIOS en UEFI pendant une mise à niveau sur place vers Windows 10 Creators Update.

**Configuration requise** :
- Windows 10 Creators Update
- Ordinateurs prenant en charge UEFI
- Outil OEM qui convertit le microprogramme de l’ordinateur du BIOS en UEFI

### <a name="to-convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Pour convertir du BIOS en UEFI pendant une mise à niveau sur place
1. Créez une séquence de tâches de mise à niveau du système d’exploitation qui effectue une mise à niveau sur place vers Windows 10 Creators Update.
2. Modifiez la séquence de tâches. Dans le **groupe de post-traitement**, ajoutez les étapes suivantes :
   1. Dans la section Général, ajoutez une étape **Exécuter la ligne de commande**. Vous ajouterez la ligne de commande pour l’outil MBR2GPT qui convertit un disque MBR en GPT sans modifier ni supprimer les données du disque. Saisissez la ligne de commande suivante :  **MBR2GPT /convert /disk:0 /AllowFullOS**. Vous pouvez également choisir d’exécuter l’outil MBR2GPT.EXE dans Windows PE plutôt que dans le système d’exploitation complet. Pour cela, ajoutez une étape afin de redémarrer l’ordinateur dans WinPE avant l’étape d’exécution de l’outil MBR2GPT.EXE puis supprimez l’option /AllowFullOS de la ligne de commande. Pour plus d’informations sur l’outil et les options disponibles, consultez [MBR2GPT.EXE](https://technet.microsoft.com/itpro/windows/deploy/mbr-to-gpt).
   2. Ajoutez une étape pour démarrer l’outil OEM qui convertira le microprogramme du BIOS en UEFI. Il s’agit en général de l’étape de séquence de tâches Exécuter la ligne de commande avec une ligne de commande pour démarrer l’outil OEM.
   3. Dans la section Général, ajoutez l’étape **Redémarrer l’ordinateur**. Pour spécifier les éléments à exécuter après le redémarrage, sélectionnez **Le système d'exploitation par défaut installé actuellement**.
3. déployer la séquence de tâches.
