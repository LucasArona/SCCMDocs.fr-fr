---
title: Configurer des sites
titleSuffix: Configuration Manager
description: Consultez cette liste de vérification pour vous assurer que vous prenez en compte les configurations les plus courantes qui affectent les sites et les hiérarchies.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a74f998c7bae22d94f2471724c2d51de918dfc4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>Configurer les sites et hiérarchies pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé votre premier site System Center Configuration Manager ou ajouté des sites supplémentaires à votre hiérarchie, utilisez la liste de vérification suivante relative aux configurations les plus courantes qui affectent les sites et les hiérarchies.  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>Liste de vérification des configurations courantes pour les nouveaux sites et les sites supplémentaires  
Prenez en compte les remarques suivantes sur la configuration, qui s’appliquent à la plupart des déploiements :

-   Certaines options sont liées, telles que les limites, les groupes de limites et la découverte de forêts Active Directory.  

-   Plusieurs configurations ont des valeurs par défaut que vous pouvez utiliser sans modification de configuration, au moins temporairement.  

-   D’autres configurations, telles que celles des groupes de limites et des groupes de points de distribution, doivent être configurées avant de pouvoir être utilisées.  

|Action|Détails|  
|------------|-------------|  
|Configurer l’administration basée sur des rôles|Séparez les attributions d’administration pour contrôler la façon dont les utilisateurs administratifs peuvent afficher et gérer les différents objets et données dans votre environnement Configuration Manager.<br /><br /> Les configurations de l’administration basée sur des rôles sont partagées avec tous les sites dans une hiérarchie.   <br/><br/>Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Publier les données de site dans les services de domaine Active Directory (AD DS)|Facilitez la recherche de services et l’utilisation efficace des ressources de site pour les clients.<br /><br /> Vous devez d’abord [étendre le schéma Active Directory pour System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md), puis chaque site doit être configuré individuellement pour [publier des données de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/publish-site-data.md).|  
|Configurer un point de connexion de service|Planifiez l’installation et la configuration du point de connexion de service sur le site de niveau supérieur de votre hiérarchie. Pour plus d’informations, voir [À propos du point de connexion de service dans System Center Configuration Manager](../../../../core/servers/deploy/configure/about-the-service-connection-point.md).|  
|Ajouter des rôles de système de site|Installez un ou plusieurs rôles de système de site supplémentaires pour des sites individuels.  Pour plus d’informations, consultez [Ajouter des rôles de système de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/add-site-system-roles.md).|  
|Configurer les limites et groupes de limites de site|Spécifiez les limites qui définissent les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer. Configurez ensuite les groupes de limites pour que les clients à ces emplacements réseau puissent trouver les ressources Configuration Manager. Pour plus d’informations, consultez [Définir des limites de site et les groupes de limites pour System Center Configuration Manager](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).|  
|Configurer les groupes de points de distribution|Configurez des groupes logiques de points de distribution pour faciliter la gestion des déploiements. Pour plus d’informations, consultez [Gérer les groupes de points de distribution](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) dans [Installer et configurer des points de distribution pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).|  
|Exécuter la découverte|Exécutez la découverte pour trouver les ressources sur votre réseau, notamment l’infrastructure réseau, les appareils et les utilisateurs.<br /><br /> Pour plus d’informations, voir [Exécuter la découverte pour System Center Configuration Manager](../../../../core/servers/deploy/configure/run-discovery.md).|  
|Accroître la redondance et les fonctionnalités pour les administrateurs qui gèrent votre infrastructure|Installez des fournisseurs SMS et des consoles Configuration Manager supplémentaires pour étendre les fonctionnalités à la disposition des administrateurs qui gèrent votre infrastructure :<br /><br /> **Installez des fournisseurs SMS supplémentaires** pour fournir une redondance aux points de contact qui gèrent votre site et votre hiérarchie. Pour plus d’informations, consultez [Gérer le fournisseur SMS](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) dans [Modifier votre infrastructure System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).<br /><br /> **Installez des consoles Configuration Manager supplémentaires** pour fournir un accès à d’autres utilisateurs administratifs. Pour plus d’informations, consultez [Installer des consoles Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).|  
|Configurer des composants de site|Configurez des composants de site sur chaque site pour modifier le comportement des rôles de système du site et les rapports d’état du site. Pour plus d'informations, voir [Site components for System Center Configuration Manager](../../../../core/servers/deploy/configure/site-components.md).|  
|Créer des regroupements personnalisés|En utilisant les informations découvertes sur les appareils et les utilisateurs, créez des regroupements personnalisés d’objets pour simplifier les tâches de gestion à venir. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|Configurer les paramètres de gestion des déploiements à haut risque|Configurez les paramètres d’un site pour avertir les utilisateurs administratifs quand ils créent un déploiement de séquence de tâches à haut risque.  Pour plus d’informations, consultez [Paramètres pour gérer les déploiements à haut risque pour System Center Configuration Manager](../../../../protect/understand/settings-to-manage-high-risk-deployments.md).|  
|Configurer des réplicas de base de données pour les points de gestion|Configurez un réplica de base de données pour réduire la charge processeur placée sur le serveur de base de données de site par les points de gestion qui traitent les demandes des clients. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).|  
|Configurer un groupe de disponibilité SQL Server AlwaysOn pour héberger la base de données du site|À compter de la version 1602, configurez des groupes de disponibilité comme solutions de haute disponibilité et de récupération d’urgence pour héberger la base de données des sites principaux et du site d’administration centrale. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).|  
|Modifier la réplication entre sites|Pour en savoir plus sur les sujets suivants, consultez [Transfert de données entre sites dans System Center Configuration Manager](../../../../core/servers/manage/data-transfers-between-sites.md) :<br /><br /> Configurer la [réplication basée sur les fichiers](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute) entre sites secondaires<br /><br /> Configurer les [liens de réplication de base de données](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)<br /><br /> Configurer les [vues distribuées](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)|  
