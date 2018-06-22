---
title: Notions de base des sites et des hiérarchies
titleSuffix: Configuration Manager
description: Obtenez des informations de base sur les sites et les hiérarchies System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4db1e15f-e832-4cf9-be33-d3971e635a55
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dbd87268c1572f53fcc86d5f2dc93537ad759260
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339279"
---
# <a name="fundamentals-of-sites-and-hierarchies-for-system-center-configuration-manager"></a>Notions de base des sites et des hiérarchies pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un déploiement de System Center Configuration Manager doit être installé dans un domaine Active Directory. La base de ce déploiement inclut un ou plusieurs sites Configuration Manager qui forment une hiérarchie de sites. Qu’il s’agisse d’un site unique ou d’une hiérarchie à plusieurs sites, le type et l’emplacement des sites que vous installez permettent de faire monter en puissance (développer) votre déploiement si nécessaire et d’offrir des services clés aux appareils et utilisateurs gérés.

## <a name="hierarchies-of-sites"></a>Hiérarchies de sites
Quand vous installez System Center Configuration Manager pour la première fois, le premier site Configuration Manager que vous installez détermine l’étendue de votre hiérarchie. Le premier site Configuration Manager constitue la base à partir de laquelle vous allez gérer les appareils et les utilisateurs dans votre entreprise. Ce premier site doit être un site d’administration centrale ou un site principal autonome.  

 Un *site d’administration centrale* convient aux déploiements à grande échelle. Il fournit un point d’administration centrale et offre la flexibilité nécessaire pour prendre en charge les appareils distribués dans une infrastructure réseau globale. Après avoir installé un site d’administration centrale, vous devez installer un ou plusieurs sites principaux comme sites enfants. Cette configuration est requise du fait qu’un site d’administration centrale ne prend pas directement en charge la gestion des appareils, ce qui est la fonction d’un site principal. Un site d’administration centrale peut prendre en charge plusieurs sites principaux enfants. Les sites principaux enfants permettent de gérer directement des appareils, mais aussi de contrôler la bande passante réseau quand vos appareils gérés ne se trouvent pas tous au même emplacement géographique.  

 Un *site principal autonome* convient pour des déploiements plus petits et permet de gérer des appareils sans devoir installer des sites supplémentaires. Un site principal autonome peut limiter la taille de votre déploiement, mais il prend en charge un scénario d’extension ultérieure de votre hiérarchie par l’installation d’un nouveau site d’administration centrale. Dans ce scénario d’extension du site, votre site principal autonome devient un site principal enfant, et vous pouvez installer des sites principaux enfants supplémentaires sous votre nouveau site d’administration centrale. Vous pouvez alors étendre votre déploiement initial dans la perspective d’une croissance future de votre entreprise.  

> [!TIP]  
>  Un site principal autonome et un site principal enfant sont en fait du même type : il s’agit de sites principaux. La différence de nom est basée sur la relation de hiérarchie qui est créée quand vous utilisez également un site d’administration centrale. Cette relation de hiérarchie peut également limiter l’installation de certains rôles système de site qui étendent les fonctionnalités de Configuration Manager. Cette limitation est due au fait que certains rôles de système de site peuvent uniquement être installés sur le site de niveau supérieur de la hiérarchie, un site d’administration centrale ou un site principal autonome.  

 Après avoir installé votre premier site, vous pouvez installer des sites supplémentaires. Si votre premier site est un site d’administration centrale, vous pouvez installer un ou plusieurs sites principaux enfants. Après avoir installé un site principal (autonome ou principal de l’enfant), vous pouvez installer un ou plusieurs sites secondaires.  

 Un *site secondaire* peut uniquement être installé en tant que site enfant sous un site principal. Ce type de site étend la portée d’un site principal à la gestion de périphériques situés dans des emplacements où la connexion réseau au site principal est lente. Même si un site secondaire étend le site principal, le site principal gère l’ensemble des clients. Le site secondaire assure la prise en charge des appareils de l’emplacement distant. Pour cela, il comprime les informations que vous envoyez (déployez) aux clients et celles que ces clients renvoient au site, et gère leur transfert sur votre réseau.  

 Les schémas suivants offrent des exemples d'architecture de site.  

 ![Exemples de hiérarchie](media/Hierarchy_examples.png)  

 Pour plus d'informations, consultez les rubriques suivantes :  

-   [Présentation de System Center Configuration Manager](../../core/understand/introduction.md)  

-   [Concevoir une hiérarchie de sites pour System Center Configuration Manager](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)  

-   [Installer des sites System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites)  

## <a name="site-system-servers-and-site-system-roles"></a>Serveurs de système de site et rôles de système de site  
 Chaque site Configuration Manager installe des *rôles de système de site* qui prennent en charge les opérations de gestion. Les rôles suivants sont installés par défaut quand vous installez un site :

-   Le rôle serveur de site est affecté à l’ordinateur sur lequel vous installez le site.

-   Le rôle serveur de base de données de site est affecté à l’ordinateur SQL Server qui héberge la base de données du site.

Les autres rôles de système de site sont facultatifs. Utilisez-les uniquement si vous souhaitez utiliser des fonctionnalités qui sont actives dans ces rôles de système de site. Tout ordinateur hébergeant un rôle système de site est considéré comme un serveur de système de site.  

 Pour un déploiement plus petit de Configuration Manager, vous pouvez initialement exécuter tous vos rôles de système de site directement sur l’ordinateur du serveur de site. Ensuite, à mesure que votre environnement géré et vos besoins augmentent, vous pouvez installer des serveurs de système de site supplémentaires pour héberger des rôles de système de site supplémentaires. Cela vous permet d’optimiser le site en fournissant des services à davantage d’appareils.  

 Pour plus d’informations sur les différents rôles de système de site, consultez [Rôles de système de site](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) dans [Planifier des serveurs de système de site et des rôles de système de site pour System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="publishing-site-information-to-active-directory-domain-services"></a>Publication d’informations de site vers les services de domaine Active Directory  
 Pour simplifier la gestion de Configuration Manager, vous pouvez étendre le schéma Active Directory pour qu’il prenne en charge les informations utilisées par Configuration Manager, puis faire en sorte que les sites publient leurs informations clés sur les services de domaine Active Directory (AD DS). Les ordinateurs que vous souhaitez gérer peuvent ensuite récupérer en toute sécurité les informations relatives au site à partir de la source approuvée d’AD DS. Les informations que les clients peuvent récupérer identifient les sites disponibles, les serveurs de système de site et les services que ces serveurs fournissent.  

 *L’extension du schéma Active Directory* n’est effectuée qu’une fois pour chaque forêt, au choix avant ou après l’installation de Configuration Manager.   Quand vous étendez le schéma, vous devez créer un conteneur Active Directory nommé System Management dans chaque domaine. Le conteneur fournit un site Configuration Manager qui publie les données dont les clients ont besoin. Pour plus d’informations, consultez [Préparer Active Directory pour la publication de site](../../core/plan-design/network/extend-the-active-directory-schema.md).  

 La *publication des données du site* renforce la sécurité de votre hiérarchie Configuration Manager et réduit la surcharge administrative, mais elle est facultative pour les fonctionnalités de base de Configuration Manager.  
