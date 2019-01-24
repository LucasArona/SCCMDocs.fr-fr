---
title: Éléments dépréciés pour les serveurs de site
titleSuffix: Configuration Manager
description: Découvrez les produits et systèmes d’exploitation que Configuration Manager ne prend plus en charge pour les serveurs de site.
ms.date: 01/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d53ac075-438b-41da-ab85-42f33982da0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8ea24e141d0e01512ed81ca96e88f2f0f2d07bc
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342718"
---
# <a name="removed-and-deprecated-for-configuration-manager-site-servers"></a>Éléments supprimés et dépréciés pour les serveurs de site Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit les produits et systèmes d’exploitation supprimés de la prise en charge dans les serveurs de site Configuration Manager ou qui seront supprimés dans une prochaine mise à jour (dépréciés). Il annonce les changements à venir qui pourraient affecter votre utilisation de Configuration Manager.  

Ces informations sont susceptibles de changer à l’avenir. Elles peuvent ne pas inclure chaque fonctionnalité, produit ou système d’exploitation déprécié.  



## <a name="server-os"></a>Système d’exploitation serveur  

|**Systèmes d’exploitation**|**Première annonce de dépréciation**|**Support supprimé** |  
|-|-|-| 
|Windows Server 2008 R2 avec SP1|10 juillet 2015| Version 1702 <sup>[Remarque 1](#bkmk_note1)</sup>| 
|Windows Server 2008 avec SP2|10 juillet 2015|Version 1511 <sup>[Remarque 2](#bkmk_note2)</sup>|  

#### <a name="bkmk_note1"></a>Remarque 1 : Windows Server 2008 R2 avec SP1
Windows Server 2008 R2 avec Service Pack 1 n’est pas pris en charge pour les serveurs de site ou la plupart des rôles de système de site. Ce système d’exploitation est toujours pris en charge pour le rôle de point de distribution. Cette prise en charge inclut les points de distribution d’extraction, PXE et la multidiffusion. 

> [!Important]  
> La date de fin du support étendu pour Windows Server 2008 R2 avec SP1 est le 14 janvier 2020. Après cette date, Configuration Manager ne prendra plus en charge ce système d’exploitation comme rôle de système de site. 

Vous pouvez mettre à niveau le système d’exploitation du serveur de site de Windows Server 2008 R2 à Windows Server 2012 R2. Pour plus d’informations, consultez [Mettre à niveau sur place le système d’exploitation de serveurs de site exécutant Windows Server 2008 R2](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#bkmk_from2008r2).  


#### <a name="bkmk_note2"></a> Remarque 2 : Windows Server 2008 avec SP2
Windows Server 2008 avec Service Pack 2 n’est pas pris en charge pour les serveurs de site ou la plupart des rôles de système de site. Ce système d’exploitation est toujours pris en charge pour le rôle de point de distribution. Cette prise en charge inclut les points de distribution d’extraction, PXE et la multidiffusion. 

> [!Important]  
> La date de fin du support étendu pour Windows Server 2008 avec SP2 est le 14 janvier 2020. Après cette date, Configuration Manager ne prendra plus en charge ce système d’exploitation comme rôle de système de site.  



## <a name="sql-server"></a>SQL Server   

|**Versions de SQL Server**|**Première annonce de dépréciation**|**Support supprimé**|   
|-|-|-| 
|SQL Server 2008 R2|10 juillet 2015|Version 1702| 
|SQL Server 2008|10 juillet 2015|Version 1511|  


Si vous devez mettre à niveau votre version de SQL Server, nous vous recommandons les méthodes suivantes, de la plus simple à la plus complexe :

1. [Mise à niveau de SQL Server sur place](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (recommandé).  

2. Installez une nouvelle version de SQL Server sur un nouvel ordinateur. Ensuite, pour pointer votre serveur de site vers la nouvelle version de SQL Server, [utilisez l’option de déplacement de la base de données](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) du programme d’installation de Configuration Manager.  

3. Utilisez la [sauvegarde et la récupération](/sccm/protect/understand/backup-and-recovery).  



## <a name="more-information"></a>Informations complémentaires

Pour plus d’informations, consultez les articles suivants : 

- [Supprimé et déprécié](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)  

- [Politique de support Microsoft](https://support.microsoft.com/lifecycle)  

- [Prise en charge des versions Current Branch de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported)  

