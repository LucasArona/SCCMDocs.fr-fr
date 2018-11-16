---
title: Migrer des données
titleSuffix: Configuration Manager
description: Découvrez comment transférer des données d’une hiérarchie source vers une hiérarchie de destination Configuration Manager.
ms.date: 11/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4c33c0f2c3b4848d67a09b77247fa53284b02882
ms.sourcegitcommit: 1f8731ed8f0308cb2cb576722adb0821a366e9ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223685"
---
# <a name="migrate-data-between-hierarchies-in-configuration-manager"></a>Migrer des données entre hiérarchies dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La migration vous permet de transférer des données d’une hiérarchie source prise en charge vers une hiérarchie de destination Configuration Manager (Current Branch). Quand vous migrez des données d’une hiérarchie source :  

- Vous accédez aux données des bases de données de site dans l’infrastructure source, puis vous transférez ces données vers votre environnement actuel.  

- La migration ne change pas les données dans la hiérarchie source. Au lieu de cela, le processus découvre les données et en stocke une copie dans la base de données de la hiérarchie de destination.  

Tenez compte des points suivants quand vous planifiez votre stratégie de migration :  

- Vous pouvez migrer une infrastructure Configuration Manager 2007 SP2 existante vers Configuration Manager (Current Branch).  

- Vous pouvez migrer certaines données ou toutes les données prises en charge à partir d’un site source.  

- Vous pouvez migrer les données d’un seul site source vers plusieurs sites dans la hiérarchie de destination.  

- Vous pouvez déplacer des données de plusieurs sites sources vers un seul site dans la hiérarchie de destination.  


La vidéo suivante explique et illustre deux [scénarios de migration](#BKMK_MigrationScenarios) courants. Elle montre également les possibilités d’intégration de Microsoft Azure dans les plans de migration.
> [!VIDEO https://www.youtube.com/embed/6_0EwW-5b4E]



##  <a name="BKMK_MigrationConcepts"></a> Concepts  

 Configuration Manager utilise les concepts et termes suivants durant la migration.  

#### <a name="source-hierarchy"></a>Hiérarchie source
Hiérarchie qui exécute une version prise en charge de Configuration Manager et qui contient les données à migrer. Quand vous configurez la migration, vous identifiez la hiérarchie source au moment de spécifier le site de niveau supérieur de cette hiérarchie. Une fois que vous avez spécifié une hiérarchie source, le site de niveau supérieur de la hiérarchie de destination recueille les données de la base de données du site source désigné afin d'identifier les données que vous pouvez migrer. 

Pour plus d’informations, consultez [Hiérarchies sources](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Hierarchies).

#### <a name="source-sites"></a>Sites source
Sites de la hiérarchie source comportant des données vous pouvez migrer vers votre hiérarchie de destination. 

Pour plus d’informations, consultez [Sites sources](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Source_Sites).

#### <a name="destination-hierarchy"></a>Hiérarchie de destination
Hiérarchie Configuration Manager (Current Branch) où une migration est effectuée pour importer des données d’une hiérarchie source.

#### <a name="data-gathering"></a>Collecte des données
Processus continu d'identification des informations d'une hiérarchie source que vous pouvez migrer vers votre hiérarchie de destination. Configuration Manager vérifie la hiérarchie source selon la planification établie. Ce processus identifie les modifications apportées aux informations de la hiérarchie source que vous avez déjà migrées et que vous pouvez avoir besoin de mettre à jour dans la hiérarchie de destination.

Pour plus d’informations, consultez [Collecte des données](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering).

#### <a name="migration-jobs"></a>Tâches de migration
Processus de configuration des objets spécifiques à migrer et de gestion de la migration de ces objets vers la hiérarchie de destination.

Pour plus d’informations, consultez [Planifier une stratégie pour les tâches de migration](/sccm/core/migration/planning-a-migration-job-strategy).

#### <a name="client-migration"></a>Migration des clients
Processus de transfert d'informations que les clients utilisent depuis la base de données du site source vers la base de données de la hiérarchie de destination. Cette migration des données est suivie d’une mise à niveau du logiciel client sur les appareils vers la version du logiciel client de la hiérarchie de destination.

Pour plus d’informations, consultez [Planifier une stratégie de migration de clients](/sccm/core/migration/planning-a-client-migration-strategy).

#### <a name="shared-distribution-points"></a>Points de distribution partagés
Points de distribution de la hiérarchie source que Configuration Manager partage avec la hiérarchie de destination tout au long de la période de migration.

Pendant la période de migration, les clients attribués aux sites de la hiérarchie de destination peuvent obtenir du contenu auprès des points de distribution partagés.

Pour plus d’informations, consultez [Partager des points de distribution entre une hiérarchie source et une hiérarchie de destination](/sccm/core/migration/planning-a-content-deployment-migration-strategy#About_Shared_DPs_in_Migration).

#### <a name="monitoring-migration"></a>Surveillance de la migration
Processus de surveillance des activités de migration. Vous surveillez la progression de la migration et son bon déroulement à partir du nœud **Migration** de l’espace de travail **Administration**.

Pour plus d’informations, consultez [Planification de la surveillance de la migration](/sccm/core/migration/planning-to-monitor-migration-activity).

#### <a name="stop-gathering-data"></a>Arrêter la collecte de données
Processus consistant à arrêter la collecte de données auprès des sites source. Quand vous n’avez plus de données à migrer à partir d’une hiérarchie source, ou si vous voulez suspendre les activités liées à la migration, vous pouvez configurer la hiérarchie de destination pour arrêter la collecte de données à partir de la hiérarchie source.

Pour plus d’informations, consultez [Collecte des données](/sccm/core/migration/planning-a-source-hierarchy-strategy#BKMK_Data_Gathering).

#### <a name="clean-up-migration-data"></a>Nettoyer les données de migration
Processus de finalisation de la migration à partir d'une hiérarchie source en supprimant les informations relatives à la migration à partir de la base de données des hiérarchies de destination.

Pour plus d’informations, consultez [Planifier la fin de la migration](/sccm/core/migration/planning-to-complete-migration).



## <a name="typical-workflow"></a>Flux de travail standard  

Pour configurer un flux de travail standard de migration :

1.  Spécifiez une hiérarchie source prise en charge.  

2.  Configurez la collecte des données. La collecte de données permet à Configuration Manager de récupère des informations sur les données qui peuvent être migrées à partir de la hiérarchie source.  

     Configuration Manager répète automatiquement le processus de collecte de données selon une planification simple, jusqu’à ce que vous arrêtiez ce processus. Par défaut, ce processus se répète toutes les quatre heures, pour permettre à Configuration Manager d’identifier les modifications apportées aux données de la hiérarchie source. La collecte de données est également nécessaire pour partager des points de distribution.  

3.  Créez des tâches de migration pour migrer des données entre la hiérarchie source et la hiérarchie de destination.  

4.  Vous pouvez arrêter le processus de collecte de données à tout moment, à l’aide de l’action **Arrêter la collecte de données**. Quand vous arrêtez la collecte de données, Configuration Manager n’identifie plus les modifications apportées aux données de la hiérarchie source et ne peut plus partager de points de distribution. En règle générale, cette commande est utilisée lorsque vous n'avez plus l'intention de migrer des données ni de partager des points de distribution à partir de la hiérarchie source.  

5.  Si vous le souhaitez, après avoir arrêté la collecte de données sur tous les sites pour la hiérarchie source, vous pouvez nettoyer les données de migration à l’aide de l’action **Nettoyer les données de migration**. Cette action supprime de la base de données de la hiérarchie de destination l’ensemble des données historiques utilisées durant la migration à partir d’une hiérarchie source.  

Après avoir migré les données, si vous n’avez plus besoin de la hiérarchie source pour gérer les appareils dans votre environnement, vous pouvez désactiver cette hiérarchie source et son infrastructure.  



##  <a name="BKMK_MigrationScenarios"></a> Scénarios  

 Configuration Manager prend en charge les scénarios de migration suivants :
- [Migration à partir de hiérarchies Configuration Manager 2007](#bkmk_2007)  
- [Migration à partir d’une hiérarchie Configuration Manager 2012 ou d’une autre hiérarchie Configuration Manager](#bkmk_2012)

> [!NOTE]  
>  L’extension d’une hiérarchie contenant un site autonome en hiérarchie contenant un site d’administration centrale n’est pas considérée comme une migration. Pour obtenir des informations sur l’extension d’une hiérarchie, consultez [Étendre un site principal autonome](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand).  


### <a name="bkmk_2007"></a> Migration à partir de hiérarchies Configuration Manager 2007  

 Quand vous migrez des données à partir de Configuration Manager 2007, vous pouvez pérenniser les investissements liés à votre infrastructure de site existante et profiter des avantages suivants :  

#### <a name="site-database-improvements"></a>Améliorations de la base de données du site
La base de données Configuration Manager (Current Branch) assure une prise en charge complète d’Unicode.

#### <a name="database-replication-between-sites"></a>Réplication de la base de données entre sites
La réplication dans Configuration Manager (Current Branch) s’appuie sur Microsoft SQL Server. Ce comportement améliore les performances des transferts de données de site à site.

#### <a name="user-centric-management"></a>Gestion centrée sur l'utilisateur
Les utilisateurs sont au cœur des tâches de gestion dans Configuration Manager (Current Branch). Par exemple, vous pouvez distribuer un logiciel à un utilisateur, même si vous ne connaissez pas le nom de l’appareil de cet utilisateur. De plus, avec Configuration Manager, les utilisateurs peuvent mieux contrôler quels logiciels sont installés sur leurs appareils et à quel moment effectuer les installations.

#### <a name="hierarchy-simplification"></a>Simplification de la hiérarchie
Configuration Manager (Current Branch) vous permet de créer une hiérarchie de site plus simple. Cette amélioration est due à l’introduction du type de site d’administration centrale et aux changements apportés au comportement des sites principaux et secondaires. Configuration Manager (Current Branch) nécessite moins de bande passante réseau et de serveurs que les versions précédentes.

#### <a name="role-based-administration"></a>Administration basée sur des rôles
Ce modèle de sécurité central dans Configuration Manager (Current Branch) permet de gérer et sécuriser l’ensemble d’une hiérarchie, conformément à vos exigences administratives et opérationnelles.

> [!NOTE]  
>  En raison des changements de conception débutés dans System Center 2012 Configuration Manager, il n’est pas possible de mettre à niveau Configuration Manager 2007 vers Configuration Manager (Current Branch). La mise à niveau sur place de System Center 2012 Configuration Manager vers Configuration Manager (Current Branch) est prise en charge.  


### <a name="bkmk_2012"></a> Migration à partir d’une hiérarchie Configuration Manager 2012 ou d’une autre hiérarchie Configuration Manager  
 Le processus de migration de données d’une hiérarchie System Center 2012 Configuration Manager ou d’une hiérarchie Configuration Manager est identique. Ce processus inclut la migration des données de plusieurs hiérarchies sources vers une seule hiérarchie de destination. Vous pouvez utiliser ce processus quand votre entreprise obtient des ressources supplémentaires qui sont déjà gérées par Configuration Manager. Par ailleurs, vous pouvez migrer des données d’un environnement de test vers votre environnement de production Configuration Manager. Avec ce processus, vous pérennisez vos investissements dans l’environnement de test Configuration Manager.  



## <a name="see-also"></a>Voir aussi  

-   [Planifier la migration vers Configuration Manager](/sccm/core/migration/planning-for-migration)  

-   [Configurer des hiérarchies sources et des sites sources pour la migration](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration)  

-   [Opérations de migration](/sccm/core/migration/operations-for-migration)  

-   [Sécurité et confidentialité pour la migration](/sccm/core/migration/security-and-privacy-for-migration)  

-   [Commencer à utiliser Configuration Manager](/sccm/core/servers/deploy/start-using)
