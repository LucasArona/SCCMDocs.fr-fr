---
title: Scénarios d’installation
titleSuffix: Configuration Manager
description: Découvrez les techniques d’installation d’une nouvelle hiérarchie Configuration Manager lors de la mise à jour ou de la mise à niveau d’un site.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aab0cfd2eba4e003130ca19147bf4c8fb6b2ea9b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501346"
---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>Scénarios pour simplifier votre installation de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec la publication des versions de mise à jour pour la branche Current Branch de System Center Configuration Manager, de nouveaux scénarios sont apparus pour simplifier l’installation d’une nouvelle hiérarchie sur une version de mise à jour (par exemple, la mise à jour 1610), et pour opérer une mise à niveau à partir de Microsoft System Center 2012 Configuration Manager.

Les scénarios pris en charge sont les suivants :  

**Installer une nouvelle hiérarchie de branche Current Branch System Center Configuration Manager** exécutant une version de mise à jour.  

-   Installez uniquement le site de niveau supérieur puis, immédiatement après, mettez-le à jour avec la version que vous voulez utiliser. Vous pouvez ensuite installer d’autres sites directement sur cette version de mise à jour.  
-   Ce scénario évite de devoir installer d’autres sites à un niveau de référence, puis de les mettre à jour avec la version de mise à jour que vous voulez utiliser.  
-   Il évite également de devoir installer les clients sur une version de référence, puis de les réinstaller lors de la mise à jour vers une version ultérieure.  

**Mettre à niveau une infrastructure System Center 2012 Configuration Manager** vers une version de mise à jour de System Center Configuration Manager.  

-   Mettez à niveau manuellement votre site d’administration centrale et chaque site principal vers une version de référence (par exemple, la version 1606) avant d’installer une version de mise à jour (par exemple, la version 1610).  
-   Ne mettez pas à niveau les sites secondaires à partir de Microsoft System Center 2012 Configuration Manager tant que vos sites principaux n’exécutent pas la version de mise à jour que vous voulez utiliser.  
-   Ne mettez pas à niveau les clients à partir de Microsoft System Center 2012 Configuration Manager tant que vos sites principaux n’exécutent pas la version de mise à jour que vous voulez utiliser.  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>Scénario : Installer une nouvelle hiérarchie sur une version de mise à jour  
Dans cet exemple de scénario, installez le premier site d’une hiérarchie à l’aide d’une version de référence de System Center Configuration Manager, telle que la version 1610. Ensuite, installez la mise à jour 1610 avant de déployer des sites ou des clients supplémentaires.  

-   Comme vous prévoyez d’utiliser une version de mise à jour (telle que la version 1610) et de ne pas en rester à la version de référence (telle que la version 1606), vous n’avez pas besoin d’installer des sites supplémentaires puis de les mettre à niveau. Cela s’applique également aux clients.  
-   N’installez pas les sites secondaires de version 1606 pour les mettre à niveau vers la version 1610. Au lieu de cela, installez les sites secondaires une fois que les sites principaux exécutent la version 1610.  

Suivez l’ordre ci-dessous :  

1. **Installez un site de niveau supérieur pour votre nouvelle hiérarchie** à l’aide du support de référence.  

   -   Vous pouvez utiliser le support de référence uniquement pour installer le premier site d’une nouvelle hiérarchie.  
   -   Par exemple, installez un site de niveau supérieur à l’aide de la version de référence 1606. Pour plus d’informations, voir [Utiliser l’Assistant Installation pour installer des sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

   Après cette étape, votre site de niveau supérieur exécute la version 1606.  

2. **Utilisez des mises à jour dans la console pour mettre à jour votre site de niveau supérieur vers une version ultérieure.**  

   -   Avant d’installer des clients ou des sites enfants, mettez à jour votre site de niveau supérieur vers la version de mise à jour que vous prévoyez d’utiliser.  
   -   Par exemple, vous pouvez mettre à jour vers la version 1610 votre site de niveau supérieur qui exécute la version 1606. Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

   Après cette étape, votre site de niveau supérieur exécute la version 1610.  

3. **Installez les nouveaux sites principaux enfants sous un site d’administration centrale.**  

   - Utilisez le support d’installation du dossier CD.Latest sur le serveur du site d’administration centrale pour installer les sites principaux enfants. Pour plus d’informations, voir [Dossier CD.Latest pour System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md).  

     Ce support de source d’installation est requis pour s’assurer que la version des nouveaux sites principaux enfants corresponde à celle du site d’administration centrale.  

   Après cette étape, vos nouveaux sites principaux enfants exécutent la version 1610.  

4. **Au niveau de chaque site principal, utilisez l’option d’installation dans la console pour installer de nouveaux sites secondaires.**  

   -   Comme vous n’avez pas installé les sites secondaires quand les sites principaux utilisaient la version 1606, vous n’avez pas besoin de mettre à niveau les sites secondaires.  
   -   Au lieu de cela, installez de nouveaux sites secondaires qui exécutent la version 1610. Pour plus d’informations, consultez [Installer un site secondaire](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary) dans la rubrique [Utiliser l’Assistant Installation pour installer des sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

   Après cette étape, les nouveaux sites secondaires sont installés et exécutent la version 1610.  

5. **Installez les nouveaux clients sur le site principal.**  

   -   Comme vous n’avez pas installé de clients quand les sites principaux utilisaient la version 1606, vous n’avez pas besoin de mettre à niveau de clients de version 1606 vers la version 1610.  
   -   Au lieu de cela, installez de nouveaux clients exécutant la version 1610. Pour plus d’informations, voir [Déployer des clients dans System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md).  

   Après cette étape, de nouveaux clients exécutant la version 1610 sont installés.  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>Scénario : Mettre à niveau System Center 2012 Configuration Manager vers une version de mise à jour de la branche Current Branch de System Center Configuration Manager  
Dans cet exemple de scénario, mettez à niveau votre infrastructure System Center 2012 Configuration Manager vers une version de mise à jour de System Center Configuration Manager, telle que la version 1610.  

-   Le site d’administration centrale et chaque site principal nécessitent une mise à niveau vers la version de référence 1606 avant l’installation de la mise à jour pour la version 1610.  
-   La version 1606 n’est pas installée ni mise à niveau sur les sites secondaires et les clients. Au lieu de cela, ils passent directement de Microsoft System Center 2012 Configuration Manager à System Center Configuration Manager version 1610.  

Suivez l’ordre ci-dessous :  

1. **Mettez à niveau votre site Microsoft System Center 2012 Configuration Manager de niveau supérieur** vers une version de référence de la branche Current Branch (comme la version 1606) à l’aide du support de source d’installation pour System Center Configuration Manager. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

   -   Comme dans les scénarios de mise à niveau classiques, vous mettez toujours à niveau d’abord le site de niveau supérieur d’une hiérarchie, puis les sites enfants.  

   Après cette étape, votre site de niveau supérieur exécute la version 1606.  

2. **Mettez à niveau chaque site principal enfant dans votre hiérarchie** vers cette même version de référence.  

   -   Quand vous effectuez la mise à niveau à partir de Microsoft System Center 2012 Configuration Manager, vous devez mettre à niveau manuellement chaque site principal vers une version de référence de Current Branch.  
   -   Vous ne devez pas mettre à niveau les sites secondaires à ce stade.  

   Après cette étape, chaque site principal exécute la version 1606.  

3. **Définissez des fenêtres de maintenance sur les sites principaux enfants.** Après avoir mis à niveau tous vos sites principaux vers la version de référence, envisagez de configurer des fenêtres de maintenance pour contrôler le moment où ces sites installeront les mises à jour de l’infrastructure. Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).  (Les fenêtres de maintenance sont appelées *fenêtres de service* dans la version 1606.)  

   -   Un site principal enfant installe automatiquement les mises à jour que vous installez sur un site d’administration centrale.  
   -   Les sites secondaires n’installent pas automatiquement les nouvelles versions. Vous devez les mettre à niveau manuellement dans la console.  

   Après cette étape, lorsque vous installez des mises à jour sur le site d’administration centrale, les sites principaux enfants n’installent ces mises à jour que lorsque leur fenêtre de maintenance les y autorise.  

4. **Installez la version de mise à jour sur votre site de niveau supérieur.** Cela a pour effet de mettre à jour votre site de niveau supérieur. Une fois qu’un site d’administration centrale a installé la version de mise à jour, chaque site principal enfant installe automatiquement cette mise à jour, à moins que l’installation soit bloquée par une fenêtre de maintenance.  

   -   Par exemple, vous pouvez mettre à jour votre site de niveau supérieur de la version 1606 vers la version 1610. Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md).  

   Après cette étape, votre site d’administration centrale et chaque site principal exécutent la version 1610.  

5. **Mettez à niveau les sites secondaires.** Une fois qu’un site principal a installé la mise à jour et exécute la version 1610, utilisez l’option dans la console pour mettre à niveau les sites secondaires.  

   -   Cela a pour effet de mettre à niveau les sites secondaires directement à partir de Microsoft System Center 2012 Configuration Manager vers la version de mise à jour que vous avez installée sur le site principal.  
   -   Pour plus d’informations sur la mise à niveau d’un site secondaire, consultez la section sur la [mise à niveau des sites](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade) dans la rubrique [Mettre à niveau vers System Center Configuration Manager](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

6. **Mettez à niveau les clients.** Pour mettre à niveau les clients, utilisez les informations de la rubrique [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

   -   Cela a pour effet de mettre à niveau les clients directement à partir de Microsoft System Center 2012 Configuration Manager vers la version de mise à jour que vous avez installée sur le site principal.  

   Après cette étape, les clients sont mis à niveau vers la version 1610 sans mise à niveau préalable vers la version 1606.
