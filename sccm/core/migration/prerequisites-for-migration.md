---
title: Prérequis de la migration
titleSuffix: Configuration Manager
description: Prenez connaissance des versions prises en charge de Configuration Manager, des langues de site source prises en charge et des configurations requises pour la migration.
ms.date: 5/7/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ec976930-7467-4d3c-b33c-991bf408a74a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: da35641b7e00bfdae025d2978beaa541951487da
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2018
ms.locfileid: "33915936"
---
# <a name="prerequisites-for-migration-in-system-center-configuration-manager"></a>Prérequis de la migration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour migrer à partir d’une hiérarchie source prise en charge, vous devez avoir accès à chaque site source Configuration Manager applicable et aux autorisations dans le site de destination System Center Configuration Manager pour configurer et exécuter des opérations de migration.  

 Pour mieux comprendre les versions de Configuration Manager prises en charge pour la migration et les configurations requises, aidez-vous des informations figurant dans les sections suivantes.  

-   [Versions de Configuration Manager prises en charge pour la migration](#BKMK_SupportedMigrationVersions)  

-   [Langues de site source prises en charge pour la migration](#BKMK_SorceSiteLanguage)  

-   [Configurations requises pour la migration](#BKMK_Required_Configurations)  

##  <a name="BKMK_SupportedMigrationVersions"></a> Versions de Configuration Manager prises en charge pour la migration  
 Vous pouvez migrer des données à partir d’une hiérarchie source qui exécute une des versions suivantes de Configuration Manager :  

-   Configuration Manager 2007 SP2 (Pour la migration, il importe peu que le site source dispose de Configuration Manager 2007 R2 ou R3. Tant que le site source exécute SP2, les sites dotés du module complémentaire R2 ou R3 sont pris en charge pour la migration vers System Center Configuration Manager).  

-   System Center 2012 Configuration Manager SP2 ou System Center 2012 R2 Configuration Manager SP1  

    > [!TIP]  
    >  En plus de la migration, vous pouvez utiliser une mise à niveau sur place des sites exécutant System Center 2012 Configuration Manager vers System Center Configuration Manager.  

-   Une hiérarchie System Center Configuration Manager présentant une version identique ou inférieure à celle de System Center Configuration Manager.  

  Par exemple, si vous disposez d’une hiérarchie de destination qui exécute System Center Configuration Manager version 1606, vous pouvez utiliser la migration pour copier des données à partir d’une hiérarchie source qui exécute la version 1606 ou 1602. Toutefois, vous ne pouvez pas migrer des données depuis une hiérarchie source exécutant la version 1610.  


##  <a name="BKMK_SorceSiteLanguage"></a> Langues de site source prises en charge pour la migration  
 Quand vous migrez des données entre hiérarchies Configuration Manager, celles-ci sont stockées dans la hiérarchie de destination dans un format indépendant de la langue pour System Center Configuration Manager. Étant donné que Configuration Manager 2007 ne stocke pas les données dans un format indépendant de la langue, le processus de migration doit convertir les objets dans ce format pendant la migration à partir de Configuration Manager 2007. Par conséquent, seuls les sites sources Configuration Manager 2007 installés avec les langues suivantes sont pris en charge pour la migration :  

-   Anglais  

-   Français  

-   Allemand  

-   Japonais  

-   Coréen  

-   Russe  

-   Chinois simplifié  

-   Chinois traditionnel  

Quand vous migrez des données à partir d’une hiérarchie System Center 2012 Configuration Manager ou System Center Configuration Manager, il n’existe aucune limitation de langue du site source. Les objets dans la base de données du site source sont déjà dans un format indépendant de la langue.  

##  <a name="BKMK_Required_Configurations"></a> Configurations requises pour la migration  
Voici les configurations requises pour la migration :  

-   **Pour configurer, exécuter et surveiller la migration dans la console Configuration Manager :**  

     Dans le site de destination, le rôle de sécurité d'administration **Administrateur d'infrastructure**doit être affecté à votre compte. Ce rôle de sécurité accorde des autorisations pour gérer toutes les opérations de migration, notamment la création de tâches de migration, le nettoyage, la surveillance ainsi que le partage et la mise à niveau de points de distribution.  

-   **Collecte des données :**  

     Pour permettre au site de destination de collecter des données, vous devez configurer les deux comptes d'accès de site source suivants pour l'utilisation avec chaque site source :  

    -   **Compte de site source** : ce compte est utilisé pour accéder au fournisseur SMS du site source.  

        -   Pour un site source Configuration Manager 2007 SP2, ce compte nécessite une autorisation **Lecture** sur tous les objets du site source.  

        -   Pour un site source System Center 2012 Configuration Manager ou System Center Configuration Manager, ce compte requiert une autorisation **Lecture** sur tous les objets du site source. Pour accorder cette autorisation au compte, vous utilisez l’administration basée sur des rôles. Pour plus d’informations sur l’utilisation de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

    -   **Compte de base de données de site source** : ce compte permet d’accéder à la base de données SQL Server du site source, et nécessite des autorisations **Connect**, **Execute**et **Select** sur la base de données du site source.  

    Vous pouvez configurer ces comptes lorsque vous configurez une nouvelle hiérarchie source, la collecte de données d'un site source supplémentaire ou lorsque vous reconfigurez les informations d'identification d'un site source. Ces comptes peuvent utiliser un compte d'utilisateur de domaine, ou vous pouvez définir le compte d'ordinateur du site de niveau supérieur de la hiérarchie de destination.  

    > [!IMPORTANT]  
    >  Si vous utilisez le compte d’ordinateur Configuration Manager pour l’un des comptes d’accès, vérifiez que ce compte est membre du groupe de sécurité **Utilisateurs du modèle COM distribué** dans le domaine du site source.  

    Lorsque vous collectez des données, les protocoles réseau suivants sont utilisés :  

    -   NetBIOS/SMB - 445 (TCP)  

    -   RPC (WMI) - 135 (TCP)  

    -   SQL Server : les ports TCP utilisés par les bases de données de site source et de destination.  

-   **Migrer des mises à jour logicielles :**  

     Avant de migrer des mises à jour logicielles, vous devez configurer votre hiérarchie de destination avec un point de mise à jour logicielle. Pour plus d’informations, consultez [Planification de la migration des mises à jour logicielles](../../core/migration/planning-for-the-migration-of-objects.md#Plan_migrate_Software_updates).  

-   **Partager des points de distribution :**  

     Pour partager des points de distribution depuis un site source, au moins un site principal ou le site d'administration centrale dans la hiérarchie de destination doit utiliser les mêmes numéros de port pour les demandes des clients que le site source. Pour plus d’informations sur les ports pour les demandes des clients, consultez [Comment configurer les ports de communication des clients dans System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md)  

     Pour chaque site source, uniquement les points de distribution installés sur les serveurs système de site qui sont configurés avec un nom de domaine complet sont partagés.  

     En outre, pour partager un point de distribution depuis un site source System Center 2012 Configuration Manager ou System Center Configuration Manager, le **compte de site source** (qui accède au fournisseur SMS du serveur de site source) doit disposer de l’autorisation **Modifier** sur l’objet **Site** sur le site source. Vous accordez cette autorisation au compte à l'aide de l'administration basée sur les rôles. Pour plus d’informations sur l’utilisation de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  


-   **Mettre à niveau ou réaffecter des points de distribution :**  

     Le **compte d'accès de site source** configuré pour collecter des données depuis le fournisseur SMS du site source doit disposer des autorisations suivantes :  

    -   Pour mettre à niveau un point de distribution Configuration Manager 2007, le compte nécessite des autorisations **Lecture**, **Exécuter** et **Supprimer** sur la classe **Site** sur le serveur de site Configuration Manager 2007 afin de pouvoir supprimer correctement le point de distribution du site source Configuration Manager 2007.  

    -   Pour réattribuer un point de distribution System Center 2012 Configuration Manager ou System Center Configuration Manager, le compte doit avoir l’autorisation **Modifier** sur l’objet **Site** sur le site source. Vous accordez cette autorisation au compte à l'aide de l'administration basée sur les rôles. Pour plus d’informations sur l’utilisation de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

     Pour mettre à niveau un point de distribution ou le réaffecter à une nouvelle hiérarchie, les ports qui sont configurés pour les demandes clients sur le site qui gère le point de distribution dans la hiérarchie source doivent correspondre aux ports qui sont configurés pour les demandes client sur le site de destination qui gérera le point de distribution. Pour plus d’informations sur les ports pour les demandes des clients, consultez [Comment configurer les ports de communication des clients dans System Center Configuration Manager](../../core/clients/deploy/configure-client-communication-ports.md).  
