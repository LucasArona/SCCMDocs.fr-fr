---
title: Actualiser un ordinateur existant avec une nouvelle version de Windows
titleSuffix: Configuration Manager
description: Vous pouvez utiliser plusieurs méthodes dans Configuration Manager pour partitionner et formater (réinitialiser) un ordinateur existant afin d’y installer un nouveau système d’exploitation.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8481b0934998a44b6142131d2cff3dbbd0821720
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124242"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>Actualiser un ordinateur existant avec une nouvelle version de Windows à l’aide de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique indique les étapes générales à effectuer dans System Center Configuration Manager pour partitionner et formater (réinitialiser) un ordinateur existant afin d’y installer un nouveau système d’exploitation. Pour ce scénario, vous pouvez choisir parmi de nombreuses méthodes de déploiement différentes, telles que PXE, média de démarrage ou Centre logiciel. Vous pouvez aussi choisir d’installer un point de migration d’état pour stocker les paramètres, puis les restaurer sur le nouveau système d’exploitation après son installation. Pour vous aider à déterminer si ce scénario de déploiement de système d’exploitation est adapté à votre cas, consultez [Scénarios de déploiement de systèmes d’exploitation d’entreprise](scenarios-to-deploy-enterprise-operating-systems.md).  

 Utilisez les sections suivantes pour actualiser un ordinateur existant avec une nouvelle version de Windows.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Planifier et implémenter la configuration requise pour l’infrastructure**  

     Plusieurs éléments d’infrastructure doivent être installés et configurés avant de déployer des systèmes d’exploitation, tels que Windows ADK, l’outil de migration utilisateur (USMT), les services de déploiement Windows (WDS), la prise en charge des configurations de disque dur, etc. Pour plus d’informations, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Installer un point de migration d’état (obligatoire uniquement si vous transférez des paramètres)**  

     Quand vous allez capturer les paramètres de l’ordinateur existant et restaurer les paramètres sur le nouveau système d’exploitation, vous devez installer un point de migration d’état. Pour plus d’informations, consultez [Point de migration d’état](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Configurerr  

1.  **Préparer une image de démarrage**  

     Les images de démarrage démarrent un ordinateur dans un environnement Windows PE (système d’exploitation minimal doté de composants et services limités), qui peut ensuite installer un système d’exploitation Windows complet sur l’ordinateur.   Quand vous déployez des systèmes d’exploitation, vous devez sélectionner une image de démarrage à utiliser et distribuer cette image sur un point de distribution. Pour préparer l’image de démarrage, utilisez les éléments suivants :  

    -   Pour en savoir plus sur les images de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

    -   Pour plus d’informations sur la personnalisation d’une image de démarrage, consultez [Personnaliser des images de démarrage](../get-started/customize-boot-images.md).  

    -   Distribuez l’image de démarrage à des points de distribution. Pour plus d'informations, voir [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Préparer une image de système d’exploitation**  

     L’image de système d’exploitation contient les fichiers nécessaires pour installer le système d’exploitation sur l’ordinateur de destination. Pour préparer l’image du système d’exploitation, utilisez les éléments suivants :  

    -   Pour en savoir plus sur la création d’une image de système d’exploitation, consultez [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

    -   Distribuez l’image du système d’exploitation à des points de distribution. Pour plus d’informations, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Créer une séquence de tâches pour déployer des systèmes d’exploitation sur le réseau**  

     Utilisez une séquence de tâches pour automatiser l’installation du système d’exploitation sur le réseau. Utilisez les étapes indiquées dans [Créer une séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md) pour créer la séquence de tâches permettant de déployer le système d’exploitation. En fonction de la méthode de déploiement choisie, des considérations supplémentaires peuvent s’appliquer à la séquence de tâches.  

    > [!NOTE]  
    >  Dans ce scénario, la séquence de tâches formate et partitionne les disques durs sur l’ordinateur. Pour capturer les paramètres utilisateur, vous devez utiliser le point de migration d’état et sélectionner **Enregistrer les paramètres et fichiers utilisateur sur un point de migration d’état** dans la page **Migration de l’état** de l’Assistant Création d’une séquence de tâches. Si vous enregistrez les paramètres et fichiers utilisateur localement, ils seront perdus quand le disque dur sera formaté et Configuration Manager ne pourra pas restaurer les paramètres. Pour plus d’informations, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Déployer  

-   Pour déployer le système d’exploitation, appliquez l’une des méthodes de déploiement suivantes :  

    -   [Utiliser PXE pour déployer Windows sur le réseau](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Utiliser la multidiffusion pour déployer Windows sur le réseau](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Créer une image pour un fabricant OEM en usine ou dépôt local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Utiliser un média autonome pour déployer Windows sans utiliser le réseau](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Utiliser un média de démarrage pour déployer Windows sur le réseau](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Utiliser le Centre logiciel pour déployer Windows sur le réseau](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Moniteur  

-   **Surveiller le déploiement de la séquence de tâches**  

     Pour surveiller le déploiement de la séquence de tâches permettant d’installer le système d’exploitation, consultez [Surveiller les déploiements de système d’exploitation](monitor-operating-system-deployments.md).  
