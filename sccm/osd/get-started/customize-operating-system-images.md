---
title: 'Personnaliser les images de système d’exploitation '
titleSuffix: Configuration Manager
description: Pour personnaliser une image de système d’exploitation, utilisez des séquences de tâches de capture et de génération, une configuration manuelle ou une combinaison des deux.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 95033a9b-ff13-4b70-b1de-bcb25bcb6024
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0b218d665d574c74358e3d018f45dd5b173cc21c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424168"
---
# <a name="customize-operating-system-images-with-system-center-configuration-manager"></a>Personnaliser les images de système d’exploitation avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les images de système d’exploitation sont des fichiers WIM qui représentent un regroupement compressé des fichiers et dossiers de référence nécessaires à l’installation et à la configuration d’un système d’exploitation sur un ordinateur. Une image de système d’exploitation personnalisée est créée et capturée à partir d’un ordinateur de référence que vous configurez avec l’ensemble des fichiers de système d’exploitation, fichiers de prise en charge, mises à jour logicielles, outils et autres applications logicielles nécessaires. Il vous revient de décider dans quelle mesure vous voulez configurer manuellement l’ordinateur de référence. Vous pouvez totalement automatiser la configuration de l’ordinateur de référence à l’aide d’une séquence de tâches de création et de capture, vous pouvez configurer manuellement certains aspects de l’ordinateur de référence puis automatiser le reste à l’aide de séquences de tâches ou vous pouvez configurer manuellement l’ordinateur de référence sans utiliser de séquences de tâches. Utilisez les sections suivantes pour personnaliser un système d’exploitation.

##  <a name="BKMK_PrepareReferenceComputer"></a> Préparer l’ordinateur de référence  
 Avant de capturer l’image de système d’exploitation d’un ordinateur de référence, vous devez réfléchir à plusieurs aspects.  

###  <a name="BKMK_RefComputerDecide"></a> Choisir entre une configuration automatisée ou manuelle  
 La section suivante décrit les avantages et inconvénients des configurations manuelle et automatisée de l’ordinateur de référence.  

#### <a name="automated-configuration"></a>Configuration automatisée  
 **Avantages**  

- La configuration peut être complètement autonome et ne pas nécessiter la présence d'un administrateur ou d'un utilisateur.  

- Vous pouvez réutiliser la séquence de tâches pour répéter la configuration d'ordinateurs de référence supplémentaires, en toute confiance.  

- Vous pouvez modifier la séquence de tâches pour appliquer des différences aux ordinateurs de référence sans avoir à recréer toute la séquence de tâches.  

  **Inconvénients**  

- L'action initiale de création et de test d'une séquence de tâches peut prendre du temps.  

- Si la configuration requise de l'ordinateur de référence change de façon significative, les nouvelles étapes de création et de test de la séquence de tâches peuvent prendre du temps.  

#### <a name="manual-configuration"></a>Configuration manuelle  
 **Avantages**  

- Vous n'avez pas besoin de créer une séquence de tâches, ni de perdre du temps à tester et corriger la séquence de tâches.  

- Vous pouvez l’installer directement à partir de CD sans avoir à insérer tous les packages logiciels (y compris Windows lui-même) dans un package Configuration Manager.  

  **Inconvénients**  

- La précision de la configuration de l’ordinateur de référence dépend de l’administrateur ou de l’utilisateur qui configure l’ordinateur.  

- Vous devez toujours vérifier et tester l'ordinateur de référence pour vous assurer qu'il est correctement configuré.  

- Vous ne pouvez pas réutiliser la méthode de configuration.  

- Requiert qu'une personne soit activement impliquée tout au long du processus.  

###  <a name="BKMK_RefComputerConsiderations"></a> Considérations relatives à l’ordinateur de référence  
 La section suivante répertorie les éléments de base à prendre en compte lorsque vous configurez un ordinateur de référence.  

-   **Système d’exploitation à déployer**  

     L'ordinateur de référence doit être installé avec le système d'exploitation que vous avez l'intention de déployer sur vos ordinateurs de destination. Pour plus d’informations sur les systèmes d’exploitation que vous pouvez déployer, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Service Pack approprié**  

     L'ordinateur de référence doit être installé avec le système d'exploitation que vous avez l'intention de déployer sur vos ordinateurs de destination.  

-   **Mises à jour logicielles appropriées**  

     Installez toutes les applications logicielles que vous souhaitez inclure dans l'image du système d'exploitation que vous capturez à partir de l'ordinateur de référence. Vous pouvez également installer des applications logicielles lorsque vous déployez l'image capturée du système d'exploitation sur vos ordinateurs de destination.  

-   **Appartenance au groupe de travail**  

     L'ordinateur de référence doit être configuré en tant que membre d'un groupe de travail.  

-   **Sysprep**  

     L'outil de préparation du système (Sysprep) est une technologie que vous pouvez utiliser avec d'autres outils de déploiement pour installer des systèmes d'exploitation Windows sur du matériel neuf. Sysprep prépare un ordinateur en vue de la création d'une image disque ou de sa livraison à un client, en configurant l'ordinateur de telle sorte qu'un nouvel identificateur de sécurité (SID) soit créé pour l'ordinateur lors de son redémarrage. Par ailleurs, Sysprep nettoie les paramètres et les données des utilisateurs et de l'ordinateur qui ne doivent pas être copiés sur un ordinateur de destination.  

     Vous pouvez appliquer Sysprep manuellement sur l'ordinateur de référence en exécutant la commande suivante :  

     `Sysprep /quiet /generalize /reboot`  

     L’option /generalize indique à Sysprep de supprimer les données propres au système de l’installation de Windows. Les informations spécifiques du système incluent, entre autres, les journaux des événements et les ID de sécurité uniques (SID). Une fois les informations système uniques supprimées, l’ordinateur redémarre.  

     Vous pouvez automatiser Sysprep à l'aide de l'étape [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) d'une séquence de tâches ou d'un média de capture.  

    > [!IMPORTANT]  
    >  L'étape de séquence de tâches [Prepare Windows for Capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture) tente de réinitialiser le mot de passe de l'administrateur local sur l'ordinateur de référence sur une valeur vide avant l'exécution de Sysprep. Si la stratégie de sécurité locale **Le mot de passe doit respecter certaines exigences de complexité** est activée, cette étape de séquence de tâches ne parvient pas à réinitialiser le mot de passe administrateur. Dans ce cas, désactivez cette stratégie avant d'exécuter la séquence de tâches.  

     Pour plus d’informations sur Sysprep, consultez [Informations techniques de référence de l’outil de préparation du système (Sysprep)](http://go.microsoft.com/fwlink/?LinkId=280286).  

-   **Outils et scripts appropriés nécessaires à l’atténuation des scénarios d’installation**  

     Outils et scripts appropriés nécessaires à l'atténuation des scénarios d'installation  

-   **Personnalisation de bureau appropriée, telle que fond d’écran, logo et profil utilisateur par défaut**  

     Vous pouvez configurer l'ordinateur de référence avec les propriétés de personnalisation du bureau que vous souhaitez inclure lorsque vous capturez l'image du système d'exploitation à partir de l'ordinateur de référence. Les propriétés de bureau incluent un fond d’écran, un logo de l’entreprise et un profil utilisateur par défaut standard.  

##  <a name="BKMK_ManuallyBuildReference"></a> Créer manuellement un ordinateur de référence  
 Utilisez la procédure suivante pour créer manuellement un ordinateur de référence.  

> [!NOTE]  
>  Quand vous créez manuellement l’ordinateur de référence, vous pouvez capturer l’image du système d’exploitation à l’aide d’un média de capture. Pour plus d’informations, consultez [Créer un média de capture](../deploy-use/create-capture-media.md).  

#### <a name="to-manually-build-the-reference-computer"></a>Pour créer manuellement l’ordinateur de référence  

1. Identifiez l'ordinateur à utiliser comme ordinateur de référence.  

2. Configurez l'ordinateur de référence avec le système d'exploitation approprié et tout autre logiciel requis pour créer l'image du système d'exploitation que vous souhaitez déployer.  

   > [!WARNING]  
   >  Installez au minimum le système d’exploitation et le Service Pack appropriés, les pilotes de prise en charge et les mises à jour logicielles requises.  

3. Configurez l'ordinateur de référence en tant que membre d'un groupe de travail.  

4. Réinitialisez le mot de passe de l'administrateur local sur l'ordinateur de référence pour que la valeur du mot de passe soit vide.  

5. Exécutez Sysprep au moyen de la commande :  **sysprep /quiet /generalize /reboot**. L’option /generalize indique à Sysprep de supprimer les données propres au système de l’installation de Windows. Les informations spécifiques du système incluent, entre autres, les journaux des événements et les ID de sécurité uniques (SID). Une fois les informations système uniques supprimées, l’ordinateur redémarre.  

   Une fois que l’ordinateur de référence est prêt, capturez l’image de système d’exploitation de l’ordinateur de référence à l’aide d’une séquence de tâches.  Pour une procédure détaillée, consultez [Capturer une image de système d’exploitation à partir d’un ordinateur de référence existant](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_CaptureExistingRefComputer).  

##  <a name="BKMK_UseTSToBuildReference"></a> Utiliser une séquence de tâches pour créer un ordinateur de référence  
 Vous pouvez automatiser le processus de création d’un ordinateur de référence en déployant le système d’exploitation, les pilotes, les applications et autres éléments à l’aide d’une séquence de tâches.  Pour créer l’ordinateur de référence et capturer l’image de système d’exploitation à partir de ce même ordinateur de référence, procédez comme suit.  

-   Utilisez une séquence de tâches pour créer et capturer l’image de système d’exploitation à partir de l’ordinateur de référence.  Pour une procédure détaillée, voir [Utiliser une séquence de tâches pour créer et capturer un ordinateur de référence](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md#BKMK_BuildCaptureTS).  
