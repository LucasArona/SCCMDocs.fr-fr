---
title: Configurer des sites et des hiérarchies
titleSuffix: Configuration Manager
description: Consultez cette liste de vérification pour vous assurer que vous prenez en compte les configurations les plus courantes qui affectent les sites et les hiérarchies.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9b56f408dc76b3b9bf48fbdab64a50eed14f0f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133610"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Configurer des sites et des hiérarchies pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé votre premier site Configuration Manager ou ajouté des sites supplémentaires à votre hiérarchie, utilisez la liste de vérification suivante relative aux configurations les plus courantes qui affectent les sites et les hiérarchies.  

Les notes de configuration suivantes s’appliquent à la plupart des déploiements :  

- Certaines options sont liées, telles que les limites, les groupes de limites et la découverte de forêts Active Directory.  

- Plusieurs configurations ont des valeurs par défaut que vous pouvez utiliser sans les modifier, du moins pour commencer.  

- D’autres configurations, telles que celles des groupes de limites et des groupes de points de distribution, doivent être configurées avant de pouvoir être utilisées.  

| Action | Détails |  
|------------|-------------|  
| Configurer l’administration basée sur des rôles | Séparez les attributions d’administration pour contrôler la façon dont les utilisateurs administratifs peuvent afficher et gérer les différents objets et données dans votre environnement Configuration Manager.<br /><br /> Les configurations de l’administration basée sur des rôles sont partagées avec tous les sites dans une hiérarchie.   <br/><br/>Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration). |  
| Publier des données de site dans Active Directory Domain Services | Facilitez la recherche de services et l’utilisation efficace des ressources de site pour les clients.<br /><br /> D’abord, [étendez le schéma Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema). Ensuite, configurez individuellement chaque site sur lequel [publier des données de site](/sccm/core/servers/deploy/configure/publish-site-data). |  
| Configurer un point de connexion de service | Planifiez l’installation et la configuration du point de connexion de service sur le site de niveau supérieur de votre hiérarchie. Pour plus d’informations, consultez [À propos du point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point). |  
| Ajouter des rôles de système de site | Installez un ou plusieurs rôles de système de site supplémentaires pour des sites individuels. Pour plus d’informations, consultez [Ajouter des rôles de système de site](/sccm/core/servers/deploy/configure/add-site-system-roles). |  
| Configurer les limites et groupes de limites de site | Spécifiez les limites qui définissent les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer. Configurez ensuite les groupes de limites pour que les clients à ces emplacements réseau puissent trouver les ressources Configuration Manager. Pour plus d’informations, consultez [Définir les limites de site et les groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups). |  
| Configurer les groupes de points de distribution | Configurez des groupes logiques de points de distribution pour faciliter la gestion des déploiements. Pour plus d’informations, voir [Gérer les groupes de points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage). |  
| Exécuter la découverte | Exécutez la découverte pour trouver des ressources sur votre réseau, notamment l’infrastructure réseau, les appareils et les utilisateurs.<br /><br /> Pour plus d’informations, consultez [Exécuter la découverte](/sccm/core/servers/deploy/configure/run-discovery). |  
| Ajouter la redondance et la capacité pour les administrateurs | Installez des fournisseurs SMS et des consoles Configuration Manager supplémentaires pour étendre la capacité des administrateurs à gérer votre infrastructure :<br /><br /> **Installez des fournisseurs SMS supplémentaires** pour fournir une redondance aux connexions de console et d’API au site. Pour plus d’informations, consultez [Gérer le fournisseur SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).<br /><br /> **Installez des consoles Configuration Manager supplémentaires** pour fournir un accès à d’autres utilisateurs administratifs. Pour plus d’informations, consultez [Installer des consoles Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). |  
| Configurer des composants de site | Configurez des composants de site sur chaque site pour modifier le comportement des rôles de système du site et les rapports d’état du site. Pour plus d’informations, consultez [Composants de site](/sccm/core/servers/deploy/configure/site-components). |  
| Créer des regroupements personnalisés | En utilisant les informations découvertes par le site concernant les appareils et les utilisateurs, créez des regroupements personnalisés d’objets pour simplifier les tâches de gestion à venir. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](/sccm/core/clients/manage/collections/create-collections). |  
| Configurer les paramètres de gestion des déploiements à haut risque | Configurez les paramètres d’un site pour avertir les administrateurs lorsqu’ils créent un déploiement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments). |  
| Configurer des réplicas de base de données pour les points de gestion | Configurez un réplica de base de données pour réduire la charge processeur qui est exercée sur le serveur de base de données de site par les points de gestion qui traitent les demandes des clients. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion](/sccm/core/servers/deploy/configure/database-replicas-for-management-points). |  
| Configurer un groupe de disponibilité SQL Server AlwaysOn | Configurez les groupes de disponibilité comme des solutions de haute disponibilité et récupération d’urgence afin d’héberger la base de données des sites principaux et le site d’administration centrale. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site hautement disponible](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). |  
| Modifier la réplication entre sites | Consultez [Transfert de données entre sites](/sccm/core/servers/manage/data-transfers-between-sites) pour en savoir plus sur les sujets suivants :<br /><br /> Configurer la [réplication basée sur les fichiers](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_fileroute) entre sites secondaires<br /><br /> Configurer les [liens de réplication de base de données](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_Dblinks)<br /><br /> Configurer les [vues distribuées](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews) |  
| Configurer des serveurs de site en mode passif | Depuis la version 1806, il est possible de configurer un serveur de site en mode passif pour chaque site principal et pour le site d’administration centrale. Cette fonctionnalité offre aux serveurs de site un haut niveau de disponibilité. Pour plus d’informations, consultez [Haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability). |  
