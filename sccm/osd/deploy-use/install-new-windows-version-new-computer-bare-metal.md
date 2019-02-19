---
title: Installer Windows sur un nouvel ordinateur
titleSuffix: Configuration Manager
description: Utilisez Configuration Manager pour installer un système d’exploitation sur un nouvel ordinateur (système nu) à l’aide d’un média PXE, OEM ou autonome.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2e565363bbee5852338d730e39bdead6aa5d8457
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134263"
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu) avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique indique les étapes générales à suivre dans System Center Configuration Manager pour installer un système d’exploitation sur un nouvel ordinateur. Pour ce scénario, vous pouvez choisir parmi de nombreuses méthodes de déploiement différentes, telles que PXE, OEM ou média autonome. Pour vous aider à déterminer si ce scénario de déploiement de système d’exploitation est adapté à votre cas, consultez [Scénarios de déploiement de systèmes d’exploitation d’entreprise](scenarios-to-deploy-enterprise-operating-systems.md).  

Utilisez les sections suivantes pour actualiser un ordinateur existant avec une nouvelle version de Windows.  

##  <a name="BKMK_Plan"></a> Plan  

-   **Planifier et implémenter la configuration requise pour l’infrastructure**  

     Plusieurs éléments d’infrastructure doivent être installés et configurés avant de déployer des systèmes d’exploitation, tels que Windows ADK, les services de déploiement Windows (WDS, Windows Deployment Services), les configurations de disques durs prises en charge, et ainsi de suite. Pour plus d’informations, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).

##  <a name="BKMK_Configure"></a> Configurer  

1.  **Préparer une image de démarrage**  

     Les images de démarrage démarrent un ordinateur dans un environnement Windows PE (système d’exploitation minimal doté de composants et services limités), qui peut ensuite installer un système d’exploitation Windows complet sur l’ordinateur.   Quand vous déployez des systèmes d’exploitation, vous devez sélectionner une image de démarrage à utiliser et distribuer cette image sur un point de distribution. Pour préparer l’image de démarrage, utilisez les éléments suivants :  

    -   Pour en savoir plus sur les images de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

    -   Pour plus d’informations sur la personnalisation d’une image de démarrage, consultez [Personnaliser des images de démarrage](../get-started/customize-boot-images.md).  

    -   Distribuez l’image de démarrage à des points de distribution. Pour plus d'informations, voir [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Préparer une image de système d’exploitation**  

     L’image de système d’exploitation contient les fichiers nécessaires pour installer le système d’exploitation sur l’ordinateur de destination. Pour préparer l’image du système d’exploitation, utilisez les éléments suivants :  

    -   Pour en savoir plus sur la création d’une image de système d’exploitation, consultez [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).

    -   Distribuez l’image du système d’exploitation à des points de distribution. Pour plus d’informations, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

    > [!NOTE]
    > De nouvelles installations de Windows peuvent également être effectuées à partir des fichiers d’installation sources via des packages de mise à niveau du système d’exploitation, mais utilisez plutôt des images de système d’exploitation comme **install.wim**.
    >
    > Le déploiement de nouvelles installations de Windows via des packages de mise à niveau du système d’exploitation est toujours pris en charge, mais il nécessite des pilotes compatibles avec cette méthode. Lorsque vous installez Windows à partir d’un package de mise à niveau du système d’exploitation, les pilotes sont installés dans Windows PE au lieu d’être simplement injectés dans Windows PE. Certains pilotes ne peuvent pas être installés dans Windows PE. Si des pilotes ne peuvent pas être installés dans Windows PE, utilisez dans ce cas une image de système d’exploitation.  

3.  **Créer une séquence de tâches pour déployer des systèmes d’exploitation sur le réseau**  

     Utilisez une séquence de tâches pour automatiser l’installation du système d’exploitation sur le réseau. Utilisez les étapes indiquées dans [Créer une séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md) pour créer la séquence de tâches permettant de déployer le système d’exploitation. En fonction de la méthode de déploiement choisie, des considérations supplémentaires peuvent s’appliquer à la séquence de tâches.  

##  <a name="BKMK_Deploy"></a> Déployer  

-   Pour déployer le système d’exploitation, appliquez l’une des méthodes de déploiement suivantes :  

    -   [Utiliser PXE pour déployer Windows sur le réseau](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Utiliser la multidiffusion pour déployer Windows sur le réseau](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Créer une image pour un fabricant OEM en usine ou dépôt local](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Utiliser un média autonome pour déployer Windows sans utiliser le réseau](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Utiliser un média de démarrage pour déployer Windows sur le réseau](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Moniteur  

-   **Surveiller le déploiement de la séquence de tâches**  

     Pour surveiller le déploiement de la séquence de tâches permettant d’installer le système d’exploitation, consultez [Surveiller les déploiements de système d’exploitation](monitor-operating-system-deployments.md).  
