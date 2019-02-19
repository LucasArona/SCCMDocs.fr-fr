---
title: Mettre à niveau vers Windows 10
titleSuffix: Configuration Manager
description: Découvrez comment utiliser Configuration Manager pour mettre à niveau un système d’exploitation Windows 7 ou ultérieur vers Windows 10.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c118c50eccf7fdb443a54f630d2d5698836d44f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135498"
---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Mettre à niveau Windows vers la dernière version avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit les étapes dans Configuration Manager pour mettre à niveau le système d’exploitation sur un ordinateur. Vous pouvez choisir parmi différentes méthodes de déploiement, telles qu’un média autonome ou le Centre logiciel. Le scénario de mise à niveau sur place présente les caractéristiques suivantes :  

-   Met à niveau le système d’exploitation sur les ordinateurs qui exécutent actuellement :
    - Windows 7, Windows 8 ou Windows 8.1. Vous pouvez également effectuer des mises à niveau de build à build de Windows 10. Par exemple, vous pouvez mettre à niveau Windows 10 version 1607 vers Windows 10 version 1709.  
    
    - Windows Server 2012. Vous pouvez également effectuer des mises à niveau de build à build de Windows Server 2016. Pour plus d’informations sur les chemins de mise à niveau pris en charge, consultez [Chemins de mise à niveau pris en charge](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016).    

-   Conserve les applications, les paramètres et les données utilisateur sur l’ordinateur.  

-   N’a aucune dépendance externe, telles que Windows ADK.  

-   Est plus rapide et plus fiable que les déploiements de système d’exploitation traditionnels.  


> [!Note]  
> À partir de la version 1802, la séquence de tâches de mise à niveau sur place de Windows 10 prend en charge le déploiement sur des clients avec accès Internet par le biais de la [passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Cette capacité permet aux utilisateurs distants de passer plus facilement à Windows 10, sans avoir à se connecter à l’intranet. Pour plus d’informations, consultez [Déployer la mise à niveau sur place de Windows 10 à l’aide de la passerelle de gestion cloud](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->



##  <a name="BKMK_Plan"></a> Plan  

### <a name="task-sequence-requirements-and-limitations"></a>Exigences et limitations de la séquence de tâches

Passez en revue les exigences et limitations suivantes de la séquence de tâches de mise à niveau d’un système d’exploitation pour vérifier qu’elle répond à vos besoins :  

- Ajoutez uniquement les étapes de séquence de tâches qui sont liées à la tâche principale de mise à niveau de système d’exploitation. Ces étapes sont principalement l’installation des packages, des applications ou des mises à jour. Utilisez également les étapes qui exécutent des lignes de commande, PowerShell, ou définissent des variables dynamiques.  

- Passez en revue les pilotes et les applications installés sur les ordinateurs pour vérifier qu’ils sont compatibles avec Windows 10 avant de déployer la séquence de tâches de mise à niveau.  

- Les tâches suivantes ne sont pas compatibles avec la mise à niveau sur place. Elles vous obligent à utiliser des déploiements de système d’exploitation classiques :  

  - Changement de l’appartenance de domaine de l’ordinateur ou mise à jour du groupe Administrateurs locaux.  

  - Implémentation d’un changement fondamental sur l’ordinateur, par exemple : 
    - Changement des partitions de disque
    - Changement de l’architecture système x86 en x64
    - Implémentation d’UEFI. (Pour plus d’informations sur une option possible, consultez [Passer de BIOS à UEFI pendant une mise à niveau sur place](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).)
    - Modification de la langue de système d’exploitation de base  

  - Vous avez des besoins personnalisés, notamment l’utilisation d’une image personnalisée de base ou du chiffrement de disque tiers, ou vous avez besoin d’exécuter des opérations hors connexion WinPE.  

### <a name="infrastructure-requirements"></a>Exigences de l'infrastructure  

Le seul prérequis du scénario de mise à niveau est d’avoir un point de distribution disponible. Distribuez le package de mise à niveau de système d’exploitation et les autres packages que vous ajoutez dans la séquence de tâches. Pour plus d’informations, consultez [Installer ou modifier un point de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).



##  <a name="BKMK_Configure"></a> Configurerr  

### <a name="prepare-the-os-upgrade-package"></a>Préparer le package de mise à niveau de système d’exploitation  

  Le package de mise à niveau de Windows 10 contient les fichiers sources nécessaires pour mettre à niveau le système d’exploitation sur l’ordinateur de destination. Le package de mise à niveau doit être de la même édition, architecture et langue que les clients que vous mettez à niveau. Pour plus d’informations, consultez [Gérer les packages de mise à niveau de système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md).  


### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Créer une séquence de tâches pour mettre à niveau le système d’exploitation  

  Utilisez les étapes indiquées dans [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](create-a-task-sequence-to-upgrade-an-operating-system.md) afin d’automatiser la mise à niveau du système d’exploitation.  

   > [!NOTE]  
   > En général, vous utilisez les étapes indiquées dans [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](create-a-task-sequence-to-upgrade-an-operating-system.md) afin de créer une séquence de tâches pour mettre à niveau un système d’exploitation vers Windows 10. La séquence de tâches comprend l’étape Mettre à niveau le système d’exploitation, ainsi que d’autres groupes et étapes recommandés pour gérer le processus de mise à niveau de bout en bout. Toutefois, vous pouvez créer une séquence de tâches personnalisée et ajouter l’étape de séquence de tâches [Mettre à niveau le système d’exploitation](../understand/task-sequence-steps.md#BKMK_UpgradeOS) pour mettre à niveau le système d’exploitation. Cette étape est la seule obligatoire pour mettre à niveau le système d’exploitation vers Windows 10. Si vous choisissez cette méthode, ajoutez également l’étape [Redémarrer l’ordinateur](../understand/task-sequence-steps.md#BKMK_RestartComputer) après l’étape Mettre à niveau le système d’exploitation pour terminer la mise à niveau. Utilisez le paramètre **Le système d’exploitation par défaut installé actuellement** pour redémarrer l’ordinateur dans le système d’exploitation installé, et non dans Windows PE.  



##  <a name="BKMK_Deploy"></a> Déployer  

Pour déployer le système d’exploitation, appliquez l’une des méthodes de déploiement suivantes :  

  -   [Utiliser le Centre logiciel pour déployer Windows sur le réseau](use-software-center-to-deploy-windows-over-the-network.md)  

  -   [Utiliser un média autonome pour déployer Windows sans utiliser le réseau](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

      > [!IMPORTANT]  
      > Quand vous utilisez un support autonome, vous devez inclure une image de démarrage dans la séquence de tâches pour qu’elle soit disponible dans l’Assistant Support de séquence de tâches.




## <a name="monitor"></a>Moniteur  

Pour surveiller le déploiement de la séquence de tâches permettant de mettre à niveau le système d’exploitation, consultez [Surveiller les déploiements de système d’exploitation](monitor-operating-system-deployments.md).  
