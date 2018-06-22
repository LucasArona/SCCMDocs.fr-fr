---
title: Planification de la création de rapports
titleSuffix: Configuration Manager
description: Qu’il s’agisse des détails de l’installation, de la sécurité ou de la bande passante réseau, il est important de planifier la création de rapports dans Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 21b9e2b685890cde4c9cc2a0fa57bc9118dcc665
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339255"
---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>Planification de la création de rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La création de rapports dans System Center Configuration Manager propose un ensemble d’outils et de ressources vous permettant d’utiliser les fonctionnalités de création de rapports avancées de SQL Server Reporting Services. Utilisez les sections suivantes pour vous aider à planifier la création de rapports dans Configuration Manager.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Déterminer où installer le point de Reporting Services  
 Lorsque vous exécutez des rapports Configuration Manager sur un site, les rapports ont accès aux informations de la base de données de site à laquelle ils se connectent. Utilisez les sections suivantes pour vous aider à déterminer où installer le point de Reporting Services et quelle source de données utiliser.  

> [!NOTE]  
>  Pour plus d’informations sur la planification de systèmes de site dans Configuration Manager, consultez [Ajouter des rôles système de site](../deploy/configure/add-site-system-roles.md).  

###  <a name="BKMK_SupportedSiteServers"></a> Serveurs de système de site pris en charge  
 Vous pouvez installer le point de Reporting Services sur un site d'administration centrale et sur des sites principaux, ainsi que sur plusieurs systèmes de site d'un ou plusieurs sites de la hiérarchie. Le point de Reporting Services n'est pas pris en charge sur les sites secondaires. Le premier point de Reporting Services sur un site est configuré comme le serveur de rapports par défaut. Vous pouvez ajouter plus de points de Reporting Services sur un site, mais le serveur de rapports par défaut sur chaque site est activement utilisé pour les rapports Configuration Manager. Vous pouvez installer le point de Reporting Services sur le serveur de site ou sur un système de site distant. Il est toutefois plus judicieux d'utiliser Reporting Services sur un serveur de système de site distant pour des raisons d'efficacité.  

###  <a name="BKMK_DataReplication"></a> Considérations relatives à la réplication des données  
 Configuration Manager classe les données qu’il réplique en tant que données globales ou données de site. Les données globales font référence à des objets ayant été créés par des utilisateurs administratifs et qui sont répliquées sur tous les sites de la hiérarchie, alors que les sites secondaires ne reçoivent qu'un sous-ensemble de données globales. Les déploiements de logiciels, les mises à jour logicielles, les regroupements et les étendues de sécurité de l'administration basée sur des rôles sont des exemples de données globales. Les données de site font référence aux informations opérationnelles créées par les sites principaux Configuration Manager et les clients qui sont sous la hiérarchie de sites principaux. Les données de site sont répliquées vers le site d'administration centrale mais pas vers d'autres sites principaux. Les données d'inventaire matériel, les messages d'états, les alertes et les résultats de regroupements basés sur des requêtes sont des exemples de données de site. Les données de site ne sont visibles que sur le site d'administration centrale et sur le site principal dont les données sont originaires.  

 Prenez les facteurs suivants en compte pour vous aider à déterminer où installer vos points de Reporting Services :  

-   Un point de Reporting Services dont la base de données du site d’administration centrale est la source des données des rapports doit avoir accès à toutes les données globales et les données de site de la hiérarchie Configuration Manager. Si vous avez besoin de rapports qui contiennent les données de site de plusieurs sites d’une hiérarchie, il peut être intéressant d’installer le point de Reporting Services sur un système de site, du site d’administration centrale et d’utiliser la base de donnée de ce site comme la source des données des rapports.  

-   Un point de Reporting Services dont la base de données du site principal enfant est la source des données des rapport ne doit avoir accès aux données globales et aux données de site que pour le site principal local et les sites secondaires enfants. Les données de site d’autres sites principaux de la hiérarchie Configuration Manager ne sont pas répliquées sur le site principal, et ainsi, Reporting Services n’y a pas accès. Si vous avez besoin de rapports qui contiennent des données de site d’un site principal spécifique ou des données globales, mais que vous ne souhaitez pas que l’utilisateur du rapport ait accès aux données de site d’autres sites principaux, installez un point de Reporting Services sur un système de site du site principal et utilisez la base de données du site principal comme source des données des rapports.  

###  <a name="BKMK_NetworkBandwidth"></a> Considérations relatives à la bande passante réseau  
 Les serveurs de système de site du même site communiquent entre eux à l'aide du protocole SMB, HTTP ou HTTPS, selon la configuration du site. Comme ces communications ne sont pas gérées et qu'elles peuvent se produire à tout moment sans contrôle de la bande passante réseau, vérifiez la bande passante réseau disponible avant d'installer le rôle du point de Reporting Services sur un système de site.  

> [!NOTE]  
>  Pour plus d’informations sur la planification de systèmes de site, consultez [Ajouter des rôles système de site](../deploy/configure/add-site-system-roles.md).  

##  <a name="BKMK_RoleBaseAdministration"></a> Planification de l’administration basée sur des rôles pour les rapports  
 La sécurité des rapports est très similaire à celles d’autres objets de Configuration Manager pour lesquels il est possible d’attribuer des rôles de sécurité et des autorisations à des utilisateurs administratifs. Les utilisateurs administratifs ne peuvent exécuter et modifier que les rapports pour lesquels ils disposent de droits de sécurité appropriés. Pour exécuter des rapports sur la console Configuration Manager, vous devez disposer d’un droit de **Lecture** pour les autorisations du **Site** et les autorisations configurées pour des objets spécifiques.  

 Cependant, contrairement à d’autres objets dans Configuration Manager, les droits de sécurité que vous avez définis pour les utilisateurs administratifs dans la console Configuration Manager doivent également être configurés dans Reporting Services. Quand vous configurez des droits de sécurité dans la console Configuration Manager, le point de Reporting Services se connecte à Reporting Services et définit les autorisations appropriées pour les rapports. Par exemple, le rôle de sécurité **Gestionnaire des mises à jour logicielles** est associé aux autorisations **Exécuter le rapport** et **Modifier le rapport** . Les utilisateurs administratifs qui ne disposent que du rôle **Gestionnaire des mises à jour logicielles** ne peuvent exécuter et modifier des rapports que pour les mises à jour logicielles. Les rapports d’autres objets ne sont pas affichés dans la console Configuration Manager. L’exception à ce principe est que certains rapports ne sont pas associés à des objets sécurisables Configuration Manager spécifiques. Pour ces rapports, l'utilisateur administratif doit disposer du droit **Lecture** pour que le **Site** puisse exécuter les rapports et du droit **Modifier** pour que le **Site** puisse modifier les rapports.  

 Les rapports sont entièrement activés pour l’administration basée sur les rôles. Les données de tous les rapports inclus dans Configuration Manager sont filtrées en fonction des autorisations de l’utilisateur administratif qui exécute le rapport. Les utilisateurs administratifs dotés de rôles spécifiques ne peuvent afficher que les informations définies pour leurs rôles.  

 Pour plus d’informations sur les droits de sécurité pour les rapports, consultez [Configurer la création de rapports](configuring-reporting.md).  

 Pour plus d’informations sur l’administration basée sur des rôles dans Configuration Manager, consultez [Configurer l’administration basée sur des rôles](../deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Étapes suivantes  
 Utilisez les rubriques supplémentaires suivantes pour vous aider à planifier les rapports dans Configuration Manager :  

-   [Prérequis de la création de rapports dans System Center Configuration Manager](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [Bonnes pratiques pour la création de rapports dans System Center Configuration Manager](../../../core/servers/manage/best-practices-for-reporting.md)  
