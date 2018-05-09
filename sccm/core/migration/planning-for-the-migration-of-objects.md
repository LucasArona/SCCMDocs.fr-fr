---
title: Migrer des objets
titleSuffix: Configuration Manager
description: Découvrez comment planifier la migration des objets entre des hiérarchies dans un environnement System Center Configuration Manager.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 066caf00-e419-4efb-93d3-ba4ba878297c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e42b7c8db3ef8c6d645d29f371fd6da475159bd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-the-migration-of-configuration-manager-objects-to-system-center-configuration-manager"></a>Planifier la migration d’objets Configuration Manager vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec System Center Configuration Manager, vous pouvez migrer de nombreux objets différents associés à différentes fonctionnalités trouvées sur un site source. Utilisez les sections suivantes pour planifier la migration d'objets entre des hiérarchies.  

-   [Planifier la migration des mises à jour logicielles](#Plan_migrate_Software_updates)  

-   [Planifier la migration du contenu](#Plan_Migrate_content)  

-   [Planifier la migration des regroupements](#BKMK_MigrateCollections)  

-   [Planifier la migration de déploiements de systèmes d’exploitation](#Plan_migrate_OSD)  

-   [Planifier la migration de la gestion de configuration souhaitée](#Plan_Migrate_Compliance_settings)  

-   [Planifier la migration des limites](#Plan_migrate_Boundaries)  

-   [Planifier la migration des rapports](#Plan_Migrate_reports)  

-   [Planifier la migration des dossiers d’organisation et de recherche](#Plan_Migrate_Org_Folders)  

-   [Planifier la migration des personnalisations Asset Intelligence](#Plan_Migrate_AI)  

-   [Planifier la migration des personnalisations des règles de contrôle de logiciel](#Plan_Migrate_SWM_Rules)  

##  <a name="Plan_migrate_Software_updates"></a> Planifier la migration des mises à jour logicielles  
 Vous pouvez migrer des objets de mise à jour logicielle, comme des packages de mise à jour logicielle et les déploiements de mise à jour logicielle.  

 Pour migrer des objets de mise à jour logicielle, vous devez d’abord configurer votre hiérarchie de destination avec des configurations qui correspondent à l’environnement de votre hiérarchie source. Pour cela, vous devez exécuter les actions suivantes :  

-   Déployer un point de mise à jour logicielle actif dans la hiérarchie de destination  

-   Configurer le catalogue de produits et de langues de sorte qu’il corresponde à la configuration de votre hiérarchie source  

-   Synchroniser le point de mise à jour logicielle de la hiérarchie de destination avec WSUS (Windows Server Update Services)  

Lorsque vous migrez des mises à jour logicielles, tenez compte des éléments suivants :  

-   La migration d’objets de mise à jour logicielle peut échouer si vous n’avez pas synchronisé les informations de votre hiérarchie de destination de sorte qu’elles correspondent à la configuration de votre hiérarchie source.  

    > [!WARNING]  
    >  Configuration Manager ne prend pas en charge l’outil WSUSutil pour synchroniser les données entre une hiérarchie source et une hiérarchie de destination.  

-   Vous ne pouvez pas migrer des mises à jour personnalisées publiées à l'aide de l'éditeur de mise à jour System Center. Vous devez republier les mises à jour personnalisées dans la hiérarchie de destination.  

Quand vous migrez depuis une hiérarchie source Configuration Manager 2007, le processus de migration modifie certains objets de mise à jour logicielle en fonction du format utilisé par la hiérarchie de destination. Utilisez le tableau suivant pour planifier la migration des objets de mise à jour logicielle depuis Configuration Manager 2007.  

|Objet Configuration Manager 2007|Nom de l'objet après la migration|  
|-----------------------------------|---------------------------------|  
|Listes des mises à jour logicielles|Les listes de mises à jour logicielles sont converties en groupes de mises à jour.|  
|Déploiements de mises à jour logicielles|Les déploiements de mise à jour logicielle sont convertis en déploiements et groupes de mises à jour.<br /><br /> Une fois que vous avez effectué la migration d’un déploiement de mise à jour logicielle à partir de Configuration Manager 2007, vous devez l’activer dans la hiérarchie de destination avant de pouvoir le déployer.|  
|Packages de mises à jour logicielles|Les packages de mises à jour logicielles restent des packages de mises à jour logicielles.|  
|Modèles de mise à jour logicielle|Les modèles de mise à jour logicielle restent des modèles de mise à jour logicielle.<br /><br /> La valeur **Durée** dans les modèles de déploiement Configuration Manager 2007 n’est pas migrée.|  

Quand vous migrez des objets à partir d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, les objets de mise à jour logicielle ne sont pas modifiés.  

##  <a name="Plan_Migrate_content"></a> Planifier la migration du contenu  
 Vous pouvez migrer du contenu d'une hiérarchie source prise en charge vers votre hiérarchie de destination. Pour une hiérarchie source Configuration Manager 2007, ce contenu comprend des programmes et des packages de distribution de logiciels, ainsi que des applications virtuelles, comme Microsoft Application Virtualization (App-V). Pour les hiérarchies sources System Center 2012 Configuration Manager et System Center Configuration Manager, ce contenu inclut des applications et des applications virtuelles App-V. Quand vous migrez du contenu entre des hiérarchies, les fichiers sources compressés sont migrés vers la hiérarchie de destination.  

### <a name="packages-and-programs"></a>Packages et programmes  
 Lorsque vous migrez des packages et des programmes, ils ne sont pas modifiés par la migration. Cependant, avant de les migrer, vous devez configurer chaque package pour qu’il utilise un chemin d’accès UNC (Universal Naming Convention) pour son emplacement de fichier source. Dans le cadre de la configuration de la migration de packages et de programmes, vous devez affecter à un site de la hiérarchie de destination la gestion de ce contenu. Le contenu n’est pas migré à partir du site affecté, mais après la migration, le site affecté accède à l’emplacement du fichier source d’origine en utilisant le mappage UNC.  

 Après avoir migré un package et un programme vers la hiérarchie de destination et tant que la migration de la hiérarchie source est active, vous pouvez mettre le contenu à la disposition des clients de cette hiérarchie en utilisant un point de distribution partagé. Pour utiliser un point de distribution partagé, le contenu doit rester accessible sur le point de distribution au niveau du site source. Pour plus d’informations sur les points de distribution partagés, consultez [Partager les points de distribution entre les hiérarchies sources et de destination](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) dans [Planifier une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

 Si la version du contenu migré a changé dans la hiérarchie source ou la hiérarchie de destination, les clients ne peuvent plus accéder au contenu à partir du point de distribution partagé dans la hiérarchie de destination. Dans ce cas, vous devez migrer à nouveau le contenu pour restaurer une version cohérente du package entre la hiérarchie source et la hiérarchie de destination. Ces informations sont synchronisées pendant le cycle de collecte des données.  

> [!TIP]  
>  Pour chaque package que vous migrez, mettez-le à jour dans la hiérarchie de destination. Cette action peut éviter les problèmes liés au déploiement du package sur les points de distribution de la hiérarchie de destination. Cependant, quand vous mettez à jour un package sur le point de distribution de la hiérarchie de destination, les clients de cette hiérarchie ne peuvent plus obtenir ce package à partir d’un point de distribution partagé. Pour mettre à jour un package dans la hiérarchie de destination, dans la console Configuration Manager, accédez à la bibliothèque de logiciels, cliquez avec le bouton droit sur le package, puis sélectionnez **Mettre à jour les points de distribution**. Effectuez cette action pour chaque package que vous migrez.  

> [!TIP]  
>  Vous pouvez utiliser Microsoft System Center Configuration Manager Package Conversion Manager pour convertir les packages et les programmes en applications System Center Configuration Manager. Téléchargez le gestionnaire de conversion des packages à partir du site [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=212950) . Pour plus d'informations, consultez [Gestionnaire de conversion des packages Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=247245).  

### <a name="virtual-applications"></a>Applications virtuelles  
Quand vous migrez des packages App-V à partir d’un site Configuration Manager 2007 pris en charge, le processus de migration les convertit en applications dans la hiérarchie de destination. En outre, selon les publications existantes du package App-V, les types de déploiements suivants sont créés dans la hiérarchie de destination :  

-   S'il n'existe pas de publications, un type de déploiement est créé qui utilise les paramètres du type de déploiement par défaut.  

-   S’il existe une publication, un type de déploiement utilisant les mêmes paramètres que la publication Configuration Manager 2007 est créé.  

-   S’il existe plusieurs publications, un type de déploiement est créé pour chaque publication Configuration Manager 2007 en utilisant les paramètres pour cette publication.  

> [!IMPORTANT]  
>  Si vous migrez un package App-V Configuration Manager 2007 précédemment migré, la migration échoue car les packages d’applications virtuelles ne prennent pas en charge le comportement de remplacement d’une migration. Dans ce cas, vous devez supprimer le package d'application virtuelle migré à partir de la hiérarchie de destination, puis créer une tâche de migration pour migrer l'application virtuelle.  

> [!NOTE]  
>  Après avoir migré un package App-V, vous pouvez utiliser l’Assistant Mise à jour du contenu pour changer le chemin d’accès source pour les types de déploiement App-V. Pour plus d’informations sur la mise à jour de contenu pour un type de déploiement, consultez « Comment gérer les types de déploiement » dans [Tâches de gestion pour les applications System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

Quand vous migrez depuis une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, vous pouvez migrer des objets pour l’environnement virtuel App-V, en plus des types de déploiement et des applications App-V. Pour plus d’informations sur les environnements App-V, consultez [Déploiement d’applications virtuelles App-V avec System Center Configuration Manager](../../apps/get-started/deploying-app-v-virtual-applications.md).  

### <a name="advertisements"></a>Publications  
Vous pouvez migrer des publications d’un site source Configuration Manager 2007 pris en charge vers la hiérarchie de destination en utilisant la migration basée sur les regroupements. Si vous mettez à niveau un client, il conserve l'historique des publications déjà exécutées pour empêcher le client de réexécuter les publications migrées.  

> [!NOTE]  
>  Vous ne pouvez pas migrer de publications pour les packages virtuels. Il s'agit d'une exception à la migration des publications.  

### <a name="applications"></a>Applications  
 Vous pouvez migrer des applications depuis une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager prise en charge vers une hiérarchie de destination. Si vous réattribuez un client de la hiérarchie source à la hiérarchie de destination, le client conserve l'historique des applications installée précédemment pour éviter qu'il réexécute une application migrée.  

##  <a name="BKMK_MigrateCollections"></a> Planifier la migration des regroupements  
 Vous pouvez migrer les critères des regroupements d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager prise en charge. Pour ce faire, vous utilisez une tâche de migration basée sur un objet. Lorsque vous migrez un regroupement, vous migrez les règles du regroupement et non les informations sur les membres du regroupement ni les informations ou les objets associés aux membres du regroupement.  

 La migration de l’objet de regroupement n’est pas prise en charge quand vous effectuez une migration à partir d’une hiérarchie source Configuration Manager 2007.  

##  <a name="Plan_migrate_OSD"></a> Planifier la migration de déploiements de systèmes d’exploitation  
Vous pouvez migrer les objets de déploiement de système d'exploitation suivants à partir d'une hiérarchie source pris en charge :  

-   Images et packages de système d'exploitation Le chemin source des images de démarrage est remplacé par l’emplacement de l’image par défaut pour le kit Windows AIK (Windows Administrative Installation Kit) sur le site de destination. Vous trouverez ci-dessous les exigences et les restrictions liées à la migration d'images et de packages de système d'exploitation :  

    -   Pour migrer des fichiers image, le compte d’ordinateur du serveur Fournisseur SMS du site de plus haut niveau de la hiérarchie de destination doit disposer de l’autorisation de **lecture** et d’**écriture** sur les fichiers image sources de l’emplacement Windows AIK du site source.  

    -   Quand vous migrez un package d’installation de système d’exploitation, vérifiez que la configuration du package sur le site source pointe vers le dossier qui contient le fichier WIM et non pas vers le fichier WIM lui-même. Si le package d'installation pointe vers le fichier WIM, la migration du package d'installation échoue.  

    -   Quand vous migrez un package d’images de démarrage à partir d’un site source Configuration Manager 2007, l’ID du package n’est pas conservé dans le site de destination. La conséquence de cela est que les clients de la hiérarchie de destination ne peuvent pas utiliser les packages d'images de démarrage disponibles sur les points de distribution partagés.  

-   Séquences de tâches Quand vous migrez une séquence de tâches qui a une référence à un package d’installation de client, cette référence est remplacée par une référence au package d’installation de client de la hiérarchie de destination.  

    > [!NOTE]  
    >  Quand vous migrez une séquence de tâches, Configuration Manager peut migrer des objets qui ne sont pas nécessaires dans la hiérarchie de destination. Ces objets incluent les images de démarrage et les packages d’installation du client Configuration Manager 2007.  

-   Pilotes et packages de pilotes Lorsque vous migrez des packages de pilotes, le compte d’ordinateur du fournisseur SMS dans la hiérarchie de destination doit avoir un contrôle total sur la source du package.

##  <a name="Plan_Migrate_Compliance_settings"></a> Planifier la migration de la gestion de configuration souhaitée  
Vous pouvez migrer des éléments de configuration et des lignes de base de configuration.  

> [!NOTE]  
>  Les éléments de configuration non interprétés des hiérarchies sources Configuration Manager 2007 ne sont pas pris en charge pour la migration. Vous ne pouvez pas migrer ou importer ces éléments de configuration dans la hiérarchie de destination. Pour plus d’informations sur les éléments de configuration non interprétés, consultez « Éléments de configuration non interprétés » dans la rubrique [À propos des éléments de configuration dans la gestion de la configuration souhaitée](http://go.microsoft.com/fwlink/?LinkId=103846), dans la bibliothèque de documentation Configuration Manager 2007.  

Vous pouvez importer les packs de configuration Configuration Manager 2007. Le processus d’importation convertit automatiquement les packs de configuration pour qu’ils soient compatibles avec System Center Configuration Manager.  

##  <a name="Plan_migrate_Boundaries"></a> Planifier la migration des limites  
 Vous pouvez migrer des limites entre les hiérarchies. Quand vous migrez des limites à partir de Configuration Manager 2007, chaque limite du site source migre simultanément et est ajoutée à un nouveau groupe de limites créé dans la hiérarchie de destination. Quand vous migrez les limites d’une hiérarchie System Center Configuration Manager 2012 ou System Center Configuration Manager, chaque limite sélectionnée est ajoutée à un nouveau groupe de limites dans la hiérarchie de destination.  

 Chaque groupe de limites créé automatiquement est activé pour l'emplacement de contenu, mais pas pour l'attribution de site. Cela empêche les limites de se chevaucher pour l'attribution de site entre les hiérarchies source et de destination. Quand vous migrez depuis un site source Configuration Manager 2007, ceci permet d’empêcher que les nouveaux clients Configuration Manager 2007 installés soient affectés de manière incorrecte à la hiérarchie de destination. Par défaut, les clients System Center Configuration Manager ne sont pas affectés automatiquement aux sites Configuration Manager 2007.  

 Lors de la migration, si vous partagez un point de distribution avec la hiérarchie de destination, les limites associées à cette distribution migrent automatiquement vers la hiérarchie de destination. Dans la hiérarchie de destination, la migration crée un groupe de limites en lecture seule pour chaque point de distribution partagé. Si vous modifiez les limites du point de distribution de la hiérarchie source, le groupe de limites de la hiérarchie de destination est mis à jour par rapport à ces modifications lors du prochain cycle de collecte de données.  

##  <a name="Plan_Migrate_reports"></a> Planifier la migration des rapports  
Configuration Manager ne prend pas en charge la migration des rapports. Utilisez plutôt le Générateur de rapports Microsoft SQL Server Reporting Services pour exporter des rapports à partir de la hiérarchie source, puis importez-les dans la hiérarchie de destination.  

> [!NOTE]  
>  Le schéma des rapports ayant changé entre Configuration Manager 2007 et System Center Configuration Manager, testez chaque rapport importé à partir d’une hiérarchie Configuration Manager 2007 pour vérifier qu’il fonctionne comme prévu.  

Pour plus d’informations sur la création de rapports, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="Plan_Migrate_Org_Folders"></a> Planifier la migration des dossiers d’organisation et de recherche  
 Vous pouvez migrer des dossiers organisationnels et des dossiers de recherche d'une hiérarchie source prise en charge vers une hiérarchie de destination. De plus, à partir d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, vous pouvez migrer les critères d’une recherche enregistrée vers une hiérarchie de destination.  

 Par défaut, le processus de migration conserve les structures de dossiers de recherche et de dossiers d'administration pour les objets et les regroupements. Cependant, dans l’Assistant Création de tâche de migration, sur la page **Paramètres** , vous pouvez configurer une tâche de migration de sorte que la structure organisationnelle des objets ne soit pas migrée en décochant la case correspondant à cette option. Les structures organisationnelles des regroupements sont toujours gérées.  

 Ceci ne s'applique pas à un dossier de recherche qui contient des applications virtuelles. Quand un package App-V est migré, le package est converti en application dans System Center Configuration Manager. Après la migration du dossier de recherche, seuls les packages restants sont trouvés et le dossier de recherche ne peut pas trouver le package App-V du fait de la conversion en application lorsque le package App-V migre.  

 Quand vous migrez une recherche enregistrée à partir d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, vous migrez les critères de la recherche et non les informations relatives aux résultats de la recherche. La migration d’une recherche enregistrée est non applicable à partir d’un site source Configuration Manager 2007.  

##  <a name="Plan_Migrate_AI"></a> Planifier la migration des personnalisations Asset Intelligence  
 Vous pouvez migrer des personnalisations pour Asset Intelligence d'une hiérarchie source prise en charge vers une hiérarchie de destination. La structure des personnalisations Asset Intelligence n’a pas changé de manière significative entre Configuration Manager 2007 et System Center Configuration Manager.  

> [!NOTE]  
>  System Center Configuration Manager ne prend pas en charge la migration d’objets Asset Intelligence depuis un site Configuration Manager 2007 utilisant Asset Intelligence Service 2.0 (AIS 2.0).  

##  <a name="Plan_Migrate_SWM_Rules"></a> Planifier la migration des personnalisations des règles de contrôle de logiciel  
 Le contrôle de logiciel n’a pas changé de manière significative entre Configuration Manager 2007 et System Center Configuration Manager. Vous pouvez migrer vos règles de contrôle de logiciel d'une hiérarchie source prise en charge vers une hiérarchie de destination.  

 Par défaut, les règles de contrôle de logiciel que vous migrez vers une hiérarchie de destination ne sont associées à aucun site spécifique de la hiérarchie de destination et s'appliquent à tous les clients de la hiérarchie. Pour appliquer une règle de contrôle de logiciel aux clients d'un site spécifique, vous devez modifier la règle de mesure après l'avoir migrée.  
