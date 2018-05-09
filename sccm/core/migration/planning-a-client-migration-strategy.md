---
title: Planifier la migration des clients
titleSuffix: Configuration Manager
description: Découvrez les tâches de migration des clients depuis une hiérarchie source vers une hiérarchie de destination System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e27b0b7-7bd3-45cd-bc99-9c991606c637
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a67fb2d070c971004418ba47c9eb56b6b0de3e5a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-a-client-migration-strategy-in-system-center-configuration-manager"></a>Planifier une stratégie de migration de clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour migrer des clients de la hiérarchie source vers une hiérarchie de destination System Center Configuration Manager, vous devez effectuer deux tâches. Vous devez migrer les objets qui sont associés au client et vous devez réinstaller ou réaffecter les clients depuis la hiérarchie source à la hiérarchie de destination. Vous migrez tout d'abord les objets pour qu'ils soient disponibles lorsque les clients sont migrés. Les objets associés au client sont migrés à l'aide de tâches de migration. Pour plus d’informations sur la migration des objets associés au client, consultez [Planification d’une stratégie pour les tâches de migration dans System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md).  

 Utilisez les sections suivantes pour planifier la migration des clients vers la hiérarchie de destination.  

-   [Planifier la migration des clients vers la hiérarchie de destination](#Planning_for_Client_Agent_Migration)  

-   [Planifier la gestion des données conservées sur les clients pendant la migration](#Planning_for_Client_Data_Migration)  

-   [Planifier les données d’inventaire et de compatibilité pendant la migration](#Planning_for_Inventory_data_migration)  

##  <a name="Planning_for_Client_Agent_Migration"></a> Planifier la migration des clients vers la hiérarchie de destination  
 Quand vous migrez des clients d’une hiérarchie source, le logiciel client sur l’ordinateur client est mis à niveau avec la version du produit de la hiérarchie de destination.  

-   **Hiérarchie source Configuration Manager 2007** : quand vous migrez des clients à partir d’une hiérarchie source qui exécute une version prise en charge de Configuration Manager, le logiciel client est mis à niveau vers la version cliente de la hiérarchie de destination.  

-   **Hiérarchie source System Center 2012 Configuration Manager ou version ultérieure** : quand vous migrez des clients entre des hiérarchies avec la même version de produit, le logiciel client ne change pas ou ne se met pas à niveau. Le client est simplement réaffecté depuis la hiérarchie source vers un site de la hiérarchie de destination.  

    > [!NOTE]  
    >  Lorsque la version de produit d'une hiérarchie n'est pas prise en charge pour migration vers votre hiérarchie de destination, mettez à niveau tous les sites et les clients dans la hiérarchie source vers une version de produit compatible. Une fois la hiérarchie source mise à niveau vers une version de produit prise en charge, vous pouvez effectuer la migration entre hiérarchies. Pour plus d’informations, consultez [Versions de Configuration Manager prises en charge pour la migration](../../core/migration/prerequisites-for-migration.md#BKMK_SupportedMigrationVersions) dans [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

Tenez compte des informations suivantes pour planifier la migration des clients :  

-   Pour mettre à niveau ou réaffecter des clients d'un site source vers un site de destination, vous pouvez utiliser une méthode de déploiement client prise en charge pour le déploiement de clients dans la hiérarchie de destination. Les méthodes de déploiement client classiques comprennent l'installation poussée du client, la distribution de logiciels, la stratégie de groupe et l'installation du logiciel client basé sur la mise à jour. Pour plus d’informations, consultez [Méthodes d’installation du client dans System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

-   Assurez-vous que l’appareil sur lequel s’exécute le logiciel client dans la hiérarchie source présente la configuration matérielle minimale requise et exécute un système d’exploitation pris en charge par la version de Configuration Manager utilisée dans la hiérarchie de destination.  

-   Avant de migrer un client, exécutez une tâche de migration pour migrer les informations que le client va utiliser dans la hiérarchie de destination.  

-   Les clients mis à niveau conservent leur historique d’exécution pour les déploiements. Cela évite d’avoir à réexécuter inutilement des déploiements dans la hiérarchie de destination.  

    -   Pour les clients Configuration Manager 2007, l’historique d’exécution de publication est conservé.  

    -   Pour les clients à partir de System Center 2012 Configuration Manager ou System Center Configuration Manager, l’historique d’exécution des déploiements est conservé.  

-   Vous pouvez migrer les clients à partir de sites de la hiérarchie source dans l'ordre de votre choix. Toutefois, migrez un nombre limité de clients en plusieurs étapes au lieu de migrer un grand nombre de clients simultanément. Une migration progressive réduit les besoins en bande passante et le traitement du serveur lorsque chaque client qui vient d'être mis à niveau envoie son inventaire complet initial et ses données de compatibilité au site qui lui est affecté.  

-   Quand vous migrez des clients Configuration Manager 2007, le logiciel client existant est désinstallé de l’ordinateur client et le nouveau logiciel client y est installé.  

-   Configuration Manager ne peut pas migrer un client Configuration Manager 2007 sur lequel est installé le client App-V, sauf si la version de ce dernier est la version 4.6 SP1 ou une version ultérieure.  

Vous pouvez surveiller le processus de migration du client dans le nœud **Migration** de l’espace de travail **Administration** dans la console Configuration Manager.  

Après la migration du client vers la hiérarchie de destination, vous ne pouvez plus gérer cet appareil dans votre hiérarchie source et vous devez supprimer le client de la hiérarchie source. Bien que cette action ne soit pas obligatoire dans le cadre du processus de migration des hiérarchies, elle peut empêcher l'identification d'un client migré dans un rapport de hiérarchie source ou un nombre incorrect de ressources entre les deux hiérarchies au cours de la migration. Par exemple, lorsqu'un client migré reste dans la base de données du site source, vous pourriez exécuter un rapport de mises à jour logicielles qui identifie incorrectement l'ordinateur comme ressource non gérée alors qu'il est géré par la hiérarchie de destination.  

##  <a name="Planning_for_Client_Data_Migration"></a> Planifier la gestion des données conservées sur les clients pendant la migration  
Lorsque vous migrez un client de sa hiérarchie source vers la hiérarchie de destination, certaines informations sont conservées sur le périphérique, alors que d'autres ne sont pas disponibles sur le périphérique après la migration.  

Les informations suivantes sont conservées sur le périphérique client :  

-   L’identificateur unique (GUID) qui associe un client à ses informations dans la base de données Configuration Manager.  

-   L'historique de publication ou de déploiement qui empêche les clients de ré exécuter inutilement des publications ou des déploiements dans la hiérarchie de destination.  

Les informations suivantes ne sont pas conservées sur le périphérique client :  

-   Fichiers dans le cache du client. Si le client requiert ces fichiers pour installer le logiciel, il les télécharge à nouveau depuis la hiérarchie de destination.  

-   Informations de la hiérarchie source à propos de publications ou déploiements qui n'ont pas encore été exécutés. Si vous souhaitez que le client exécute des publications ou des déploiements après la migration, vous devez les redéployer vers le client dans la hiérarchie de destination.  

-   Informations sur l'inventaire. Le client renvoie ces informations à son site attribué dans la hiérarchie de destination après la migration du client et la génération des nouvelles données du client.  

-   Données de compatibilité. Le client renvoie ces informations à son site attribué dans la hiérarchie de destination après la migration du client et la génération des nouvelles données du client.  

Quand un client migre, les informations stockées dans le chemin du Registre et des fichiers du client Configuration Manager ne sont pas conservées. Après la migration, réappliquez ces paramètres. Les paramètres types sont les suivants :  

-   Modes de gestion de l'alimentation  

-   Paramètres de journalisation  

-   Paramètres de stratégie locale  

En outre, il peut être nécessaire de réinstaller certaines applications.  

##  <a name="Planning_for_Inventory_data_migration"></a> Planifier les données d’inventaire et de compatibilité pendant la migration  
Les données d'inventaire et de compatibilité client ne sont pas enregistrées lorsque vous migrez un client vers la hiérarchie de destination. En revanche, ces informations sont recréées dans la hiérarchie de destination lorsqu'un client envoie pour la première fois les informations à son site affecté. Pour réduire les besoins en bande passante et le traitement du serveur, ne migrez pas tous les clients en même temps, mais en plusieurs étapes.  

 En outre, vous ne pouvez pas migrer des personnalisations d'inventaire matériel à partir d'une hiérarchie source. Vous devez les introduire dans la hiérarchie de destination indépendamment de la migration. Pour plus d’informations sur la manière d’étendre l’inventaire matériel, consultez [Guide pratique pour configurer l’inventaire matériel dans System Center Configuration Manager](../../core/clients/manage/inventory/configure-hardware-inventory.md).  
