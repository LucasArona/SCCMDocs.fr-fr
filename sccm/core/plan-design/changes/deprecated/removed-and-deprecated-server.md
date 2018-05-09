---
title: Déprécié pour les serveurs de site Configuration Manager
titleSuffix: Configuration Manager
description: Découvrez les produits et systèmes d’exploitation que System Center Configuration Manager ne prend plus en charge pour les serveurs de site.
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b92eb8083ce886fcab4d9957b2a79999d72a1a5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="removed-and-deprecated-for-system-center-configuration-manager-site-servers"></a>Supprimé et déprécié pour les serveurs de site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit les produits et systèmes d’exploitation supprimés de la prise en charge dans les serveurs de site System Center Configuration Manager ou qui seront supprimés dans une prochaine mise à jour (dépréciés). Il annonce les changements à venir qui pourraient affecter votre utilisation de Configuration Manager.  

Ces informations peuvent faire l’objet de modifications dans les futures versions et ne pas inclure chaque fonctionnalité, produit ou système d’exploitation déprécié.  


## <a name="deprecated-server-operating-systems"></a>Systèmes d’exploitation serveur dépréciés  

|**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé** |  
|-|-|-| 
|Windows Server 2008 R2|10 juillet 2015| Version 1702  (voir la remarque 1)| 
|Windows Server 2008|10 juillet 2015|Version 1511 </br></br>Le support prend fin quand un système de site est supprimé (Voir la remarque 2).|  

>[!NOTE]
>-   À compter de la version 1702, Windows Server 2008 R2 n’est pas pris en charge pour les serveurs de site ou la plupart des rôles de système de site. Toutefois, les versions antérieures à 1702 continuent de prendre en charge son utilisation. Ce système d’exploitation reste pris en charge pour le rôle de système de site de point de distribution (y compris les points de distribution d’extraction, ainsi que pour PXE et la multidiffusion) jusqu’à l’annonce de la dépréciation de cette prise en charge ou jusqu’à l’expiration du support étendu de ce système d’exploitation. À compter de la version 1602, vous pouvez mettre à niveau sur place le système d’exploitation d’un serveur de site de Windows Server 2008 R2 vers Windows Server 2012 R2.  
>- Pour plus d’informations sur la mise à niveau sur place d’un système d’exploitation de serveurs de site, consultez la section [Mise à niveau sur place du système d’exploitation des serveurs de site qui exécutent Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2) dans [Mettre à niveau l’infrastructure locale qui prend en charge System Center Configuration Manager](/sccm/core/servers/manage/upgrade-on-premises-infrastructure).

>[!NOTE]
>-   Windows Server 2008 n’est pas pris en charge pour les serveurs de site ou les rôles de système de site, à l’exception du point de distribution et du point de distribution d’extraction. Vous pouvez continuer à utiliser ce système d’exploitation comme point de distribution jusqu’à l’annonce de la dépréciation de la prise en charge ou jusqu’à l’expiration du support étendu de ce système d’exploitation. Pour plus d’informations, consultez [Échec de l’installation de System Center Configuration Manager CB et LTSB sur Windows Server 2008](https://support.microsoft.com/help/4015095).

## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Support déprécié pour les versions de SQL Server en tant que base de données de site  

|**Versions de SQL Server**|**Première annonce de dépréciation**|**Support supprimé**|   
|-|-|-| 
|SQL Server 2008 R2|10 juillet 2015|Version 1702| 
|SQL Server 2008|10 juillet 2015|Version 1511|  


Si vous devez mettre à niveau votre version de SQL Server, nous vous recommandons les méthodes suivantes, de la plus simple à la plus complexe.
1. [Mise à niveau de SQL Server sur place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommandé).
2. Installez une nouvelle version de SQL Server sur un nouvel ordinateur. Ensuite, [utilisez l’option de déplacement de la base de données](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) du programme d’installation de Configuration Manager pour pointer votre serveur de site vers la nouvelle version de SQL Server.
3. Utilisez la [sauvegarde et la récupération](/sccm/protect/understand/backup-and-recovery).


## <a name="more-information"></a>Plus d'informations
Pour plus d'informations, voir :
 - [Supprimé et déprécié](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Le site web [Politique de support Microsoft](https://support.microsoft.com/lifecycle).
 - [Prise en charge des versions Current Branch de System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).