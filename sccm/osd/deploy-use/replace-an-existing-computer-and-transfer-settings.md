---
title: Remplacer un ordinateur existant et transférer des paramètres
titleSuffix: Configuration Manager
description: Dans Configuration Manager, choisissez les méthodes de déploiement, telles que le média de démarrage, la multidiffusion ou le Centre logiciel, pour remplacer un ordinateur existant par un nouveau.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d28f4363-9e8a-4c54-9cb7-0594fabfff26
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2693196ab21474877b5eda4ecce4a93737d1ac59
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="replace-an-existing-computer-and-transfer-settings-with-system-center-configuration-manager"></a>Remplacer un ordinateur existant et transférer des paramètres avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique indique les étapes générales à suivre dans System Center Configuration Manager pour remplacer un ordinateur existant par un nouveau. Pour ce scénario, vous pouvez choisir parmi de nombreuses méthodes de déploiement, telles que média de démarrage, multidiffusion ou Centre logiciel. Vous pouvez aussi choisir d’installer un point de migration d’état pour stocker les paramètres, puis les restaurer sur le nouveau système d’exploitation après son installation. Pour vous aider à déterminer si ce scénario de déploiement de système d’exploitation est adapté à votre cas, consultez [Scénarios de déploiement de systèmes d’exploitation d’entreprise](scenarios-to-deploy-enterprise-operating-systems.md).  

 Utilisez les sections suivantes pour actualiser un ordinateur existant avec une nouvelle version de Windows.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Planifier et implémenter la configuration requise pour l’infrastructure**  

     Plusieurs éléments d’infrastructure doivent être installés et configurés avant de déployer des systèmes d’exploitation, tels que Windows ADK, l’outil de migration utilisateur (USMT), les services de déploiement Windows (WDS), la prise en charge des configurations de disque dur, etc. Pour plus d’informations, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Installer un point de migration d’état (obligatoire uniquement si vous transférez des paramètres)**  

     Quand vous allez capturer les paramètres de l’ordinateur existant et restaurer les paramètres sur le nouveau système d’exploitation, vous devez installer un point de migration d’état. Pour plus d’informations, consultez [Point de migration d’état](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Configurerr  

1.  **Préparer une image de démarrage**  

     Les images de démarrage démarrent un ordinateur dans un environnement Windows PE (système d’exploitation minimal doté de composants et services limités), qui peut ensuite installer un système d’exploitation Windows complet sur l’ordinateur. Quand vous déployez des systèmes d’exploitation, vous devez sélectionner une image de démarrage à utiliser et distribuer cette image sur un point de distribution. Pour préparer l’image de démarrage, utilisez les éléments suivants :  

    -   Pour en savoir plus sur les images de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

    -   Pour plus d’informations sur la personnalisation d’une image de démarrage, consultez [Personnaliser des images de démarrage](../get-started/customize-boot-images.md).  

    -   Distribuez l’image de démarrage à des points de distribution. Pour plus d’informations, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Préparer une image de système d’exploitation**  

     L’image de système d’exploitation contient les fichiers nécessaires pour installer le système d’exploitation sur l’ordinateur de destination. Pour préparer l’image du système d’exploitation, utilisez les éléments suivants :  

    -   Pour en savoir plus sur la création d’une image de système d’exploitation, consultez [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

    -   Distribuez l’image du système d’exploitation à des points de distribution. Pour plus d’informations, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Créer une séquence de tâches pour déployer des systèmes d’exploitation sur le réseau**  

     Utilisez une séquence de tâches pour automatiser l’installation du système d’exploitation sur le réseau. Utilisez les étapes indiquées dans [Créer une séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md) pour créer la séquence de tâches permettant de déployer le système d’exploitation. En fonction de la méthode de déploiement choisie, des considérations supplémentaires peuvent s’appliquer à la séquence de tâches.  

    > [!NOTE]  
    >  Dans ce scénario, si vous capturez et restaurez des paramètres utilisateur et des fichiers, vous pouvez choisir d’utiliser un point de migration d’état ou d’enregistrer les fichiers localement. Pour plus d’informations, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Déployer  

-   Pour déployer le système d’exploitation, appliquez l’une des méthodes de déploiement suivantes :  

    -   [Utiliser le Centre logiciel pour déployer Windows sur le réseau](use-software-center-to-deploy-windows-over-the-network.md)  

    -   [Utiliser un média de démarrage pour déployer Windows sur le réseau](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Utiliser la multidiffusion pour déployer Windows sur le réseau](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Créer une image pour un fabricant OEM en usine ou dépôt local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

## <a name="monitor"></a>Moniteur  

-   **Surveiller le déploiement de la séquence de tâches**  

     Pour surveiller le déploiement de la séquence de tâches permettant d’installer le système d’exploitation, consultez [Surveiller les déploiements de système d’exploitation](monitor-operating-system-deployments.md).  
