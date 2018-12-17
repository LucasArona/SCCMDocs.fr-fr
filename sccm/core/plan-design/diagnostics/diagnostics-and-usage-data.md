---
title: Données d’utilisation et de diagnostics
titleSuffix: Configuration Manager
description: Découvrez quelles données d’utilisation et de diagnostic System Center Configuration Manager collecte à son sujet.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 132604418ce810fb78b397f3d5f322b10abe6bb3
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820014"
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Données d’utilisation et de diagnostic pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager collecte les données d’utilisation et de diagnostic qui le concernent. Microsoft utilise ensuite ces données pour améliorer le processus d’installation, la qualité et la sécurité des versions ultérieures.  

 Les données d’utilisation et de diagnostic sont collectées pour chaque hiérarchie Configuration Manager. Elle consistent en requêtes SQL Server qui s’exécutent chaque semaine sur chaque site principal et sur le site d’administration centrale. Quand la hiérarchie utilise un site d’administration centrale, les données provenant des sites principaux sont répliquées sur ce site. Sur le site de niveau supérieur de votre hiérarchie, le point de connexion de service soumet ces informations quand il recherche des mises à jour. Si le point de connexion de service est en mode hors connexion, les informations sont transférées à l’aide de l’outil de connexion de service.  

> [!NOTE]  
>  Configuration Manager collecte uniquement les données de la base de données SQL Server du site. Il ne collecte pas de données directement à partir des clients ni des serveurs de site.  

 Pour plus d’informations, consultez la [Déclaration de confidentialité de Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Articles
 Pour en savoir plus sur les données d’utilisation et de diagnostic de Configuration Manager, consultez les articles suivants :  

-   [Utilisation des données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

-   Niveaux de collecte des données d’utilisation et de diagnostic :
    - [Données de diagnostic pour 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Données de diagnostic pour 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

    - [Données de diagnostic pour 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    
    - [Données de diagnostic pour 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  

-   [Mode de collecte des données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

-   [Mode d’affichage des données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

-   [Programme d’amélioration de l’expérience utilisateur (CEIP)](/sccm/core/plan-design/diagnostics/customer-experience-improvement-program-ceip)  

     > [!Note]  
     > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.  


-   [Forum aux questions sur les données de diagnostic et d’utilisation](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  



## <a name="see-also"></a>Voir aussi  
 [À propos du point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point)
