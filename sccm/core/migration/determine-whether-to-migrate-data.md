---
title: Déterminer les données à migrer
titleSuffix: Configuration Manager
description: Découvrez les données que vous pouvez migrer et celles que ne pouvez pas vers System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 99222dc8-0e1e-4513-8302-7a1acf671e9b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b260a9e3deeb8668d736c3ed5ec2c2519e3ed50
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138974"
---
# <a name="determine-whether-to-migrate-data-to-system-center-configuration-manager"></a>Déterminer s’il faut migrer des données vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, la migration offre un moyen de transférer des données et des configurations créées dans des versions de Configuration Manager prises en charge vers votre nouvelle hiérarchie.  La migration vous permet d’effectuer les opérations suivantes :  

-   Combiner plusieurs hiérarchies en une seule.  

-   Déplacer les données et les configurations d’un déploiement de laboratoire vers votre déploiement de production.

-   Déplacer des données et la configuration à partir d’une version antérieure de Configuration Manager, telle que Configuration Manager 2007, qui n’a pas de chemin de mise à niveau vers System Center Configuration Manager, ou à partir de System Center 2012 Configuration Manager (qui prend en charge un chemin de mise à niveau vers System Center Configuration Manager).  

À l'exception du rôle de système de site du point de distribution et des ordinateurs hébergeant les points de distribution, aucune infrastructure (sites, rôles de système de site ou ordinateurs hébergeant un rôle de système de site) ne peut être migrée ou transférée, ni partagée entre des hiérarchies.  

 Il est impossible de migrer l’infrastructure de serveur, mais vous pouvez migrer des clients Configuration Manager entre des hiérarchies. La migration des clients consiste notamment à migrer les données utilisées par les clients à partir de la hiérarchie source vers la hiérarchie de destination, puis à installer ou à réaffecter le logiciel client afin que le client communique ensuite avec la nouvelle hiérarchie.

Une fois qu’un client a été installé dans la nouvelle hiérarchie et qu’il a envoyé ses données, son identifiant Configuration Manager unique permet à Configuration Manager d’associer plus facilement les données que vous avez migrées précédemment avec chaque ordinateur client.  

 La fonctionnalité fournie par la migration permet de pérenniser les investissements effectués en matière de configurations et de déploiements tout en vous permettant de tirer pleinement parti des principales modifications du produit introduites dans System Center 2012 Configuration Manager et poursuivies dans System Center Configuration Manager. Ces modifications comprennent une hiérarchie Configuration Manager simplifiée qui utilise moins de sites et de ressources ainsi que l’amélioration du traitement avec l’utilisation du code 64 bits natif qui s’exécute sur du matériel 64 bits.  

 Pour plus d’informations sur les versions de Configuration Manager prises en charge par la migration, consultez [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 Les sections suivantes expliquent comment planifier les données que vous pouvez migrer et celles qui ne peuvent pas l’être :  

-   [Données que vous pouvez migrer vers System Center Configuration Manager](#Can_Migrate)  

-   [Données que vous ne pouvez pas migrer vers System Center Configuration Manager](#Cannot_migrate)  

##  <a name="Can_Migrate"></a> Données que vous pouvez migrer vers System Center Configuration Manager  
 Le processus de migration peut migrer la plupart des objets entre des hiérarchies Configuration Manager prises en charge. Les instances migrées de certains objets à partir d’une version prise en charge de Configuration Manager 2007 doivent être modifiées, de façon à ce qu’elles respectent le schéma et le format d’objet de System Center 2012 Configuration Manager.

Ces modifications n’affectent pas les données contenues dans la base de données du site source. Les objets migrés à partir d’une version prise en charge de System Center 2012 Configuration Manager ou de System Center Configuration Manager ne nécessitent aucune modification.  

 Voici des objets qui peuvent migrer en fonction de la version de Configuration Manager utilisée dans la hiérarchie source. Certains objets, telles les requêtes, ne migrent pas. Si vous souhaitez continuer à utiliser ces objets qui ne migrent pas, vous devez les recréer dans la nouvelle hiérarchie. D’autres objets, notamment certaines données des clients, sont recréés automatiquement dans la nouvelle hiérarchie quand vous gérez les clients de cette hiérarchie.  

### <a name="objects-that-you-can-migrate-from-system-center-2012-configuration-manager-or-system-center-configuration-manager-current-branch"></a>Objets que vous pouvez migrer à partir de la version Current Branch de System Center Configuration Manager ou de System Center 2012 Configuration Manager

-   Applications pour System Center 2012 Configuration Manager et versions ultérieures  

-   Environnement virtuel App-V de System Center 2012 Configuration Manager et versions ultérieures  

-   Personnalisations Asset Intelligence  

-   Limites  

-   Regroupements : Pour migrer des regroupements à partir d’une version prise en charge de System Center 2012 Configuration Manager ou de System Center Configuration Manager, vous utilisez une tâche de migration d’objets.  

-   Paramètres de compatibilité :  

    -   Lignes de base de configuration  

    -   Éléments de configuration  

-   Déploiements  

-   Déploiement de système d'exploitation :  

    -   Images de démarrage  

    -   Packages de pilotes  

    -   Pilotes  

    -   Images  

    -   Packages  

    -   Séquences de tâches  

-   Résultats de la recherche : Critères de recherche enregistrés  

-   Mises à jour logicielles :  

    -   Déploiements  

    -   Packages de déploiement  

    -   Modèles  

    -   Listes des mises à jour logicielles  

-   Packages de distribution de logiciels  

-   Règles de contrôle de logiciel  

-   Packages d'application virtuelle  

### <a name="objects-that-you-can-migrate-from-configuration-manager-2007-sp2"></a>Objets que vous pouvez migrer à partir de Configuration Manager 2007 SP2

-   Publications  

-   Applications pour System Center 2012 Configuration Manager et versions ultérieures  

-   Environnement virtuel App-V de System Center 2012 Configuration Manager et versions ultérieures  

-   Personnalisations Asset Intelligence  

-   Limites  

-   Regroupements : Vous migrez des regroupements à partir d’une version prise en charge de Configuration Manager 2007 en utilisant une tâche de migration de regroupements.  

-   Paramètres de compatibilité (désignés par l’expression « gestion de la configuration souhaitée » dans Configuration Manager 2007) :  

    -   Lignes de base de configuration  

    -   Éléments de configuration  

-   Déploiement de système d'exploitation :  

    -   Images de démarrage  

    -   Packages de pilotes  

    -   Pilotes  

    -   Images  

    -   Packages  

    -   Séquences de tâches  

-   Résultats de la recherche : Dossiers de recherche  

-   Mises à jour logicielles :  

    -   Déploiements  

    -   Packages de déploiement  

    -   Modèles  

    -   Listes des mises à jour logicielles  

-   Packages de distribution de logiciels  

-   Règles de contrôle de logiciel  

-   Packages d'application virtuelle  

##  <a name="Cannot_migrate"></a> Données que vous ne pouvez pas migrer vers System Center Configuration Manager  
 Vous ne pouvez pas migrer les types d'objets suivants :  

-   Informations de préparation de client AMT  

-   Fichiers stockés sur les clients, notamment :  

    -   Données d'inventaire et historique client  

    -   Fichiers dans le cache du client  

-   Requêtes  

-   Droits de sécurité Configuration Manager 2007 et instances pour le site et les objets  

-   Rapports Configuration Manager 2007 de SQL Server Reporting Services  

-   Rapports web de Configuration Manager 2007  

-   Rapports System Center 2012 Configuration Manager et System Center Configuration Manager  

-   Administration basée sur des rôles System Center 2012 Configuration Manager et System Center Configuration Manager :  

    -   Rôles de sécurité  

    -   Étendues de sécurité  
