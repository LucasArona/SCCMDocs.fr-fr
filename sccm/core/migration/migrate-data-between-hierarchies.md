---
title: Migrer des données
titleSuffix: Configuration Manager
description: Découvrez comment transférer des données d’une hiérarchie source vers une hiérarchie de destination System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 17b0a13040ec589ee8987685d30d9a3d232afde8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336797"
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>Migrer des données entre hiérarchies dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Transférez des données d’une hiérarchie source prise en charge vers une hiérarchie de destination System Center Configuration Manager en procédant à une migration.  Quand vous migrez des données d’une hiérarchie source :  

-   Vous accédez aux données des bases de données de site que vous identifiez dans l’infrastructure source, puis vous transférez ces données vers votre environnement actuel.  

-   La migration ne modifie pas les données de la hiérarchie source, mais découvre les données et en enregistre une copie dans la base de données de la hiérarchie de destination.  

Tenez compte des points suivants quand vous planifiez votre stratégie de migration :  

-   Vous pouvez migrer une infrastructure Configuration Manager 2007 SP2 existante vers System Center Configuration Manager.  

-   Vous pouvez migrer certaines données ou toutes les données prises en charge à partir d’un site source.  

-   Vous pouvez migrer les données d’un seul site source vers plusieurs sites dans la hiérarchie de destination.  

-   Vous pouvez déplacer des données de plusieurs sites sources vers un seul site dans la hiérarchie de destination.  

##  <a name="BKMK_MigrationConcepts"></a> Concepts de migration  
 Vous pouvez rencontrer les concepts et les termes suivants quand vous utilisez la migration.  

|Concept ou terme|Plus d'informations|  
|---------------------|----------------------|  
|Hiérarchie source|Hiérarchie qui exécute une version prise en charge de Configuration Manager et qui contient les données à migrer. Quand vous configurez la migration, vous identifiez la hiérarchie source au moment de spécifier le site de niveau supérieur de cette hiérarchie. Une fois que vous avez spécifié une hiérarchie source, le site de niveau supérieur de la hiérarchie de destination recueille les données de la base de données du site source désigné afin d'identifier les données que vous pouvez migrer.<br /><br /> Pour plus d’informations, consultez [Hiérarchies sources](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) dans [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Sites source|Sites de la hiérarchie source comportant des données vous pouvez migrer vers votre hiérarchie de destination.<br /><br /> Pour plus d’informations, consultez [Sites sources](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) dans [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Hiérarchie de destination|Hiérarchie System Center Configuration Manager dans laquelle une migration est exécutée pour importer les données d’une hiérarchie source.|  
|Collecte des données|Processus continu d'identification des informations d'une hiérarchie source que vous pouvez migrer vers votre hiérarchie de destination. Configuration Manager vérifie la hiérarchie source selon une planification établie pour identifier les modifications apportées aux informations de la hiérarchie source que vous avez déjà migrées et que vous pourriez souhaiter mettre à jour dans la hiérarchie de destination.<br /><br /> Pour plus d’informations, consultez [Collecte de données](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) dans [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Tâches de migration|Processus de configuration des objets spécifiques à migrer et de gestion de la migration de ces objets vers la hiérarchie de destination.<br /><br /> Pour plus d’informations, consultez [Planification d’une stratégie pour les tâches de migration dans System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md).|  
|Migration des clients|Processus de transfert d'informations que les clients utilisent depuis la base de données du site source vers la base de données de la hiérarchie de destination. Cette migration des données est ensuite suivie d'une mise à niveau du logiciel client sur les périphériques à la version du logiciel client à partir de la hiérarchie de destination.<br /><br /> Pour plus d'informations, voir [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Points de distribution partagés|Points de distribution de la hiérarchie source qui sont partagés avec la hiérarchie de destination tout au long de la période de migration.<br /><br /> Pendant la période de migration, les clients attribués aux sites de la hiérarchie de destination peuvent obtenir du contenu auprès des points de distribution partagés.<br /><br /> Pour plus d’informations, consultez [Partager des points de distribution entre une hiérarchie source et une hiérarchie de destination](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) dans [Planification d’une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Surveillance de la migration|Processus de surveillance des activités de migration. Vous surveillez la progression de la migration et son bon déroulement à partir du nœud **Migration** de l’espace de travail **Administration**.<br /><br /> Pour plus d’informations, consultez [Planification de la surveillance de la migration dans System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md).|  
|Arrêter la collecte de données|Processus consistant à arrêter la collecte de données auprès des sites source. Quand vous n’avez plus de données à migrer à partir d’une hiérarchie source, ou si vous voulez suspendre les activités liées à la migration, vous pouvez configurer la hiérarchie de destination pour arrêter la collecte de données à partir de la hiérarchie source.<br /><br /> Pour plus d’informations, consultez [Collecte de données](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) dans [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Nettoyer les données de migration|Processus de finalisation de la migration à partir d'une hiérarchie source en supprimant les informations relatives à la migration à partir de la base de données des hiérarchies de destination.<br /><br /> Pour plus d’informations, voir [Planification d’une migration complète vers System Center 2012 Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## <a name="typical-workflow-for-migration"></a>Flux de travail standard de migration  
Pour configurer un flux de travail standard de migration :

1.  Spécifiez une hiérarchie source prise en charge.  

2.  Configurez la collecte des données. La collecte de données permet à Configuration Manager de récupère des informations sur les données qui peuvent être migrées à partir de la hiérarchie source.  

     Configuration Manager répète automatiquement le processus de collecte de données selon une planification simple, jusqu’à ce que vous arrêtiez ce processus. Par défaut, il se répète toutes les quatre heures, de telle sorte que Configuration Manager peut identifier les modifications apportées aux données de la hiérarchie source que vous pourriez souhaiter migrer. La collecte de données est également nécessaire pour partager des points de distribution entre la hiérarchie source et la hiérarchie de destination.  

3.  Créez des tâches de migration pour migrer des données entre la hiérarchie source et la hiérarchie de destination.  

4.  Vous pouvez arrêter le processus de collecte de données à tout moment, à l'aide de la commande **Arrêter la collecte de données** . Quand vous arrêtez la collecte de données, Configuration Manager n’identifie plus les modifications apportées aux données de la hiérarchie source et ne peut plus partager de points de distribution entre la hiérarchie source et la hiérarchie de destination. En règle générale, cette commande est utilisée lorsque vous n'avez plus l'intention de migrer des données ni de partager des points de distribution à partir de la hiérarchie source.  

5.  Si vous le souhaitez, après avoir arrêté la collecte de données sur tous les sites pour la hiérarchie source, vous pouvez nettoyer les données de migration à l'aide de la commande **Nettoyer les données de migration** . Cette commande supprime de la base de données de la hiérarchie de destination l'ensemble des données historiques relatives à la migration à partir d'une hiérarchie source.  

Après avoir migré les données d’une hiérarchie source Configuration Manager que vous n’utiliserez plus pour gérer votre environnement, vous pouvez désactiver cette hiérarchie source et son infrastructure.  

##  <a name="BKMK_MigrationScenarios"></a> Scénarios de migration  
 Configuration Manager prend en charge les scénarios de migration ci-suivants.  

> [!NOTE]  
>  L’expansion d’une hiérarchie contenant un site autonome en hiérarchie contenant un site d’administration centrale n’est pas considérée comme une migration. Pour plus d’informations sur l’expansion de hiérarchie, consultez [Étendre un site principal autonome](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) dans [Utiliser l’Assistant Installation pour installer des sites](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Migration à partir de hiérarchies Configuration Manager 2007  
 Quand vous migrez des données à partir de Configuration Manager 2007, vous pouvez pérenniser les investissements liés à votre infrastructure de site existante et profiter des avantages suivants :  

|Avantage|Plus d'informations|  
|-------------|----------------------|  
|Améliorations de la base de données du site|La base de données System Center Configuration Manager assure une prise en charge complète d’Unicode.|  
|Réplication de la base de données entre sites|La réplication dans System Center Configuration Manager s’appuie sur Microsoft SQL Server. Les performances des transferts de données de site à site sont ainsi améliorées.|  
|Gestion centrée sur l'utilisateur|Les utilisateurs constituent l’élément central des tâches de gestion dans System Center Configuration Manager. Par exemple, vous pouvez distribuer un logiciel à un utilisateur, même si vous ne connaissez pas le nom du périphérique pour cet utilisateur. En outre, System Center Configuration Manager offre aux utilisateurs beaucoup plus de contrôle sur les logiciels qui sont installés sur leurs appareils et sur le moment où ils le sont.|  
|Simplification de la hiérarchie|Dans System Center Configuration Manager, le type de site d’administration centrale et les modifications apportées au comportement du site principal et des sites secondaires vous permettent de créer une hiérarchie de site plus simple, plus économique en bande passante réseau et nécessitant un nombre de serveurs moins important.|  
|Administration basée sur des rôles|Ce modèle de sécurité central dans System Center Configuration Manager offre une gestion et une sécurité pour toute la hiérarchie, qui correspondent à vos exigences administratives et opérationnelles.|  

> [!NOTE]  
>  Compte tenu de l’évolution de la conception amorcée par System Center 2012 Configuration Manager, vous ne pouvez pas mettre à niveau une infrastructure Configuration Manager 2007 vers System Center Configuration Manager. La mise à niveau sur place de System Center 2012 Configuration Manager vers System Center Configuration Manager est prise en charge.  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Migration à partir d’une hiérarchie Configuration Manager 2012 ou d’une autre hiérarchie System Center Configuration Manager  
 Le processus de migration de données d’une hiérarchie System Center 2012 Configuration Manager ou System Center Configuration Manager est identique. Vous pouvez notamment migrer les données de plusieurs hiérarchies sources vers une seule hiérarchie de destination, par exemple, quand votre société obtient des ressources supplémentaires qui sont déjà gérées par Configuration Manager. Par ailleurs, vous pouvez migrer des données d’un environnement de test vers votre environnement de production Configuration Manager. Vous pérennisez ainsi les investissements liés à l’environnement de test Configuration Manager.  

## <a name="additional-topics-for-migration"></a>Rubriques supplémentaires relatives à la migration :  

-   [Planification de la migration vers System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [Configuration des hiérarchies sources et des sites sources pour la migration vers System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Opérations de migration vers System Center Configuration Manager](../../core/migration/operations-for-migration.md)  

-   [Sécurité et confidentialité pour la migration vers System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>Voir aussi  
 [Commencer à utiliser System Center Configuration Manager](../../core/servers/deploy/start-using.md)
