---
title: Préparer la mise en service de BitLocker dans Windows PE
titleSuffix: Configuration Manager
description: La tâche Préconfigurer BitLocker dans Configuration Manager permet d’activer BitLocker à partir de l’environnement de préinstallation Windows (WinPE) avant le déploiement du système d’exploitation.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c7c94ba0-d709-4129-8077-075a8abaea1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad4bfe99e841af5ccc4f6792fda664b8259a5369
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350525"
---
# <a name="preprovision-bitlocker-in-windows-pe-with-system-center-configuration-manager"></a>Préconfigurer BitLocker dans Windows PE avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’étape de séquence de tâches **Préconfigurer BitLocker** dans System Center Configuration Manager vous permet d’activer BitLocker depuis l’environnement de préinstallation Windows (WinPE) préalablement au déploiement du système d’exploitation. Seul l'espace disque utilisé étant chiffré, l'opération de chiffrement est beaucoup plus rapide. Un protecteur clair généré de manière aléatoire est appliqué au volume mis en forme et le volume est chiffré avant l'exécution du processus d'installation de Windows. La possibilité de préconfigurer BitLocker est une nouveauté de Windows 8 et Windows Server 2012. Toutefois, vous pouvez préconfigurer BitLocker sur un disque dur et installer Windows 7, tant que vous suivez les étapes spécifiques. Une fois le programme d'installation de Windows 7 terminé, vous devez définir un protecteur de clé BitLocker car le panneau de configuration BitLocker de Windows 7 ne gère pas BitLocker avec un protecteur clair. Vous devez ajouter un protecteur de clé à l'aide de l'étape **Activer BitLocker** ou en utilisant l'outil de ligne de commande manage-bde.exe.  

 En règle générale, vous devez effectuer les opérations suivantes pour préconfigurer correctement BitLocker sur un ordinateur qui va installer Windows 7 :  

-   Redémarrer l'ordinateur dans Windows PE  

    > [!IMPORTANT]  
    >  Vous devez utiliser une image de démarrage avec Windows PE 4 ou une version ultérieure pour préconfigurer BitLocker. Pour plus d’informations sur les versions de Windows PE prises en charge, consultez [Dépendances externes à Configuration Manager](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_ExternalDependencies).  

-   Partitionner et formater le disque dur  

-   Préconfigurer BitLocker  

-   Installer Windows 7 avec des paramètres de système d'exploitation et de réseau spécifiques  

-   Ajouter un protecteur de clé BitLocker  

 Dans Configuration Manager, la méthode recommandée pour préconfigurer BitLocker sur un disque dur et installer Windows 7 consiste à créer une séquence de tâches et de sélectionner **Installer un package d’images existant** dans la page **Créer une nouvelle séquence de tâches** de l’**Assistant Création d’une séquence de tâches**. L'Assistant crée les étapes de séquence de tâches répertoriées dans le tableau suivant.  

> [!NOTE]  
>  La séquence de tâches peut contenir des étapes supplémentaires en fonction de la façon dont vous avez configuré les paramètres dans l'Assistant. Par exemple, l'étape **Capturer les paramètres Windows** peut être incluse si vous avez sélectionné **Paramètres Microsoft Windows capturés** sur la page **Migration de l'état** de l'Assistant.  

|Étape de séquence de tâches|Détails|  
|------------------------|-------------|  
|Désactiver BitLocker|Cette étape désactive le chiffrement BitLocker, s'il est actuellement activé. Pour plus d’informations, consultez [Désactiver BitLocker](../understand/task-sequence-steps.md#BKMK_DisableBitLocker).|  
|Redémarrer l’ordinateur dans Windows PE|Cette étape redémarre l'ordinateur dans Windows PE en exécutant l'image de démarrage affectée à la séquence de tâches en cours d'exécution. Vous devez utiliser une image de démarrage avec Windows PE 4 ou une version ultérieure pour préconfigurer BitLocker. Pour plus d’informations, consultez [Redémarrer l’ordinateur](../understand/task-sequence-steps.md#BKMK_RestartComputer).|  
|Partitionner le disque 0 - BIOS<br /><br /> Partitionner le disque 0 - UEFI|Ces étapes formatent et partitionnent le disque spécifié sur l'ordinateur de destination à l'aide de BIOS ou UEFI. La séquence de tâches utilise UEFI lorsqu'elle détecte que l'ordinateur de destination est en mode UEFI. Pour plus d’informations, consultez [Formater et partitionner le disque](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk).|  
|Préconfigurer BitLocker|Cette étape permet d'activer BitLocker sur un lecteur avec Windows PE. Seul l'espace disque utilisé est chiffré. Étant donné que vous avez partitionné et formaté le disque dur à l'étape précédente, il n'y a pas de données et le cryptage s'effectue très rapidement. Pour plus d’informations, consultez [Préconfigurer BitLocker](../understand/task-sequence-steps.md#BKMK_PreProvisionBitLocker).|  
|Appliquer le système d'exploitation|Cette étape prépare le fichier de réponses utilisé pour installer le système d'exploitation sur l'ordinateur de destination et règle la variable de séquence de tâches OSDTargetSystemDrive sur la lettre de lecteur de la partition contenant les fichiers de système d'exploitation Le fichier de réponses et la variable sont utilisés par l'étape d'installation de Windows et de ConfigMgr pour installer le système d'exploitation. Pour plus d'informations, voir [Apply Operating System Image](../understand/task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).|  
|Appliquer les paramètres Windows|Cette étape ajoute les paramètres Windows au fichier de réponses. Le fichier de réponses est utilisé par l'étape d'installation de Windows et de ConfigMgr pour installer le système d'exploitation. Pour plus d’informations, consultez [Appliquer les paramètres Windows](../understand/task-sequence-steps.md#BKMK_ApplyWindowsSettings).|  
|Appliquer les paramètres réseau|Cette étape ajoute les paramètres réseau au fichier de réponses. Le fichier de réponses est utilisé par l'étape d'installation de Windows et de ConfigMgr pour installer le système d'exploitation. Pour plus d’informations, consultez [Appliquer l’étape des paramètres réseau](../understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings).|  
|Appliquer les pilotes de périphériques|Cette étape recherche des pilotes et les installe dans le cadre du déploiement du système d'exploitation. Pour plus d’informations, consultez [Appliquer automatiquement les pilotes](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).|  
|Configurer Windows et ConfigMgr|Cette étape effectue la transition de Windows PE vers le nouveau système d'exploitation. Cette étape de séquence de tâches est obligatoire dans tout déploiement de système d'exploitation, elle installe le client Configuration Manager dans le nouveau système d’exploitation et prépare la poursuite de l’exécution de la séquence de tâches dans le nouveau système d’exploitation. Pour plus d’informations, consultez [Configurer Windows et ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).|  
|Activer BitLocker|Cette étape permet le chiffrement BitLocker sur le disque dur et définit des protecteurs de clés. Étant donné que le disque dur a été préconfiguré avec BitLocker, cette étape s'effectue très rapidement. Windows 7 requiert que vous ajoutiez un protecteur de clé. Si vous n'utilisez pas cette étape, vous pouvez exécuter l'outil de ligne de commande manage-bde.exe pour définir un protecteur de clé. Pour plus d’informations, consultez [Activer BitLocker](../understand/task-sequence-steps.md#BKMK_EnableBitLocker).|  
