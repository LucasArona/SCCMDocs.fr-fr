---
title: Principes de base de l’administration basée sur des rôles
titleSuffix: Configuration Manager
description: Utilisez l’administration basée sur les rôles pour contrôler l’accès administratif à Configuration Manager et les objets que vous gérez.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3b7916b386cb22f2d1869eface009bd10ff17d18
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862547"
---
# <a name="fundamentals-of-role-based-administration-for-system-center-configuration-manager"></a>Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec System Center Configuration Manager, l’administration basée sur des rôles vous permet de sécuriser l’accès nécessaire à l’administration de Configuration Manager. Vous sécurisez également l’accès aux objets que vous gérez, tels que les regroupements, les déploiements et les sites. À présent que vous comprenez les concepts présentés dans cette rubrique, vous pouvez [configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

 Le modèle d’administration basée sur des rôles définit et gère de façon centralisée les paramètres d’accès de sécurité à l’échelle de la hiérarchie pour tous les sites ainsi que les paramètres de site à l’aide des éléments suivants :  

-   Les *rôles de sécurité* sont attribués aux utilisateurs administratifs pour octroyer à ceux-ci (ou à des groupes d’utilisateurs) des autorisations relatives à différents objets Configuration Manager, par exemple, celles de créer ou modifier des paramètres client.  

-   Les *étendues de sécurité* permettent de regrouper des instances d’objets spécifiques qu’un utilisateur administratif est chargé de gérer, par exemple une application qui installe Microsoft Office 2010.  

-   Les *regroupements* permettent de spécifier des groupes de ressources d’utilisateurs et d’appareils que l’utilisateur administratif peut gérer.  

 L’utilisation combinée de rôles de sécurité, d’étendues de sécurité et de regroupements permet de séparer les attributions administratives répondant aux besoins de votre organisation, ainsi que de définir l’étendue administrative d’un utilisateur, autrement dit ce qu’il peut afficher et gérer dans votre déploiement de Configuration Manager.  

## <a name="benefits-of-role-based-administration"></a>Avantages de l’administration basée sur des rôles  

-   Les sites ne sont pas utilisés comme limites administratives.  

-   Après avoir créé des utilisateurs administratifs pour la hiérarchie, il vous suffit de leur attribuer une étendue de sécurité une seule fois.  

-   Toutes les attributions de sécurité sont répliquées et disponibles dans la hiérarchie.  

-   Il existe des rôles de sécurité intégrés permettent d’attribuer les tâches d’administration classiques, mais vous pouvez aussi créer vos propres rôles de sécurité personnalisés en fonction des besoins propres à votre activité.  

-   Les utilisateurs administratifs voient uniquement les objets qu'ils sont autorisés à gérer.  

-   Vous pouvez auditer des actions administratives de sécurité.  

Quand vous concevez et implémentez la sécurité administrative pour Configuration Manager, créez une *étendue administrative* pour un utilisateur administratif à l’aide des éléments suivants :  

-   [Rôles de sécurité](#bkmk_Planroles)  

-   [Regroupements](#bkmk_planCol)  

-   [Étendues de sécurité](#bkmk_PlanScope)  


 L’étendue administrative contrôle les objets qu’un utilisateur administratif peut afficher dans la console Configuration Manager et les autorisations dont dispose cet utilisateur sur ces objets. Les configurations d'administration basées sur des rôles sont répliquées sur chaque site de la hiérarchie en tant que données globales, puis sont appliquées à toutes les connexions administratives.  

> [!IMPORTANT]  
>  Les retards de réplication intersite peuvent empêcher un site de recevoir des modifications pour l'administration basée sur les rôles. Pour plus d’informations sur la manière de surveiller la réplication intersite de base de données, consultez la rubrique [Transfert de données entre sites dans System Center Configuration Manager](../../core/servers/manage/data-transfers-between-sites.md).  

##  <a name="bkmk_Planroles"></a> Rôles de sécurité  
 Utilisez des rôles de sécurité pour accorder des autorisations de sécurité aux utilisateurs administratifs. Les rôles de sécurité sont des groupes d'autorisations de sécurité que vous affectez aux utilisateurs administratifs afin qu'ils puissent effectuer leurs tâches administratives. Ces autorisations de sécurité définissent les actions administratives réalisables par un utilisateur administratif ainsi que les autorisations sont accordées pour des types d'objet particulier. Comme bonne pratique de sécurité, affectez les rôles de sécurité qui fournissent des autorisations minimales.  

 Configuration Manager possède plusieurs rôles de sécurité intégrés pour prendre en charge des regroupements typiques de tâches administratives et vous pouvez créer vos propres rôles de sécurité personnalisés pour prendre en charge vos besoins professionnels spécifiques. Exemples de rôles de sécurité intégrés :  

-   *Administrateur complet* : accorde toutes les autorisations dans Configuration Manager.  

-   *Gestionnaire de biens* : accorde des autorisations permettant de gérer le point de synchronisation Asset Intelligence, les classes de création de rapports Asset Intelligence, l’inventaire logiciel, l’inventaire matériel et les règles de contrôle.  

-   *Gestionnaire des mises à jour logicielles* : accorde les autorisations de définir et déployer des mises à jour logicielles. Les utilisateurs administratifs qui sont associés à ce rôle peuvent créer des regroupements, des groupes de mises à jour logicielles, des déploiements et des modèles.  

> [!TIP]  
>  Vous pouvez afficher la liste des rôles de sécurité intégrés et les rôles de sécurité personnalisés que vous créez, ainsi que leurs descriptions, dans la console Configuration Manager. Pour afficher les rôles, dans l’espace de travail **Administration**, développez **Sécurité**, puis sélectionnez **Rôles de sécurité**.  

 Chaque rôle de sécurité dispose d'autorisations spécifiques à différents types d'objets. Par exemple, le rôle de sécurité *Auteur d’application* a les autorisations suivantes pour les applications : Approuver, Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Exécuter un rapport et Définir l’étendue de sécurité.

 Vous ne pouvez pas modifier les autorisations pour les rôles de sécurité intégrés, mais vous pouvez copier le rôle, y apporter des modifications, puis enregistrer ces modifications sous un nouveau rôle de sécurité personnalisé. Vous pouvez également importer des rôles de sécurité que vous avez exportés depuis une autre hiérarchie, par exemple depuis un réseau de test. Passez en revue les rôles de sécurité et leurs autorisations pour déterminer si vous allez utiliser les rôles de sécurité intégrés ou devoir créer vos propres rôles de sécurité personnalisés.  

 ### <a name="to-help-you-plan-for-security-roles"></a>Pour faciliter la planification des rôles de sécurité  

1.  Identifiez les tâches que les utilisateurs administratifs effectuent dans Configuration Manager. Ces tâches peuvent concerner un ou plusieurs groupes de tâches de gestion, tels que le déploiement d'applications et de packages, le déploiement de systèmes d'exploitation et de paramètres pour la conformité, la configuration de sites et de la sécurité, l'audit, le contrôle d'ordinateurs à distance et le recueil de données d'inventaire.  

2.  Mappez ces tâches administratives vers un ou plusieurs rôles de sécurité intégrés.  

3.  Si certains des utilisateurs administratifs effectuent les tâches de plusieurs rôles de sécurité, attribuez-leur ces rôles de sécurité, au lieu de créer un nouveau rôle de sécurité permettant d’effectuer toutes ces tâches.  

4.  Si les tâches que vous avez identifiées ne correspondent pas aux rôles de sécurité intégrés, créez et testez de nouveaux rôles de sécurité.  

Pour plus d’informations sur la façon de créer et de configurer des rôles de sécurité pour l’administration basée sur des rôles, consultez [Créer des rôles de sécurité personnalisés](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) et [Configurer des rôles de sécurité](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) dans la rubrique [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

##  <a name="bkmk_planCol"></a> Regroupements  
 Les regroupements spécifient les ressources d'utilisateur et d'ordinateur qu'un utilisateur administratif peut consulter ou gérer. Par exemple, pour que les utilisateurs administratifs puissent déployer des applications ou effectuer un contrôle à distance, un rôle de sécurité qui leur permet d'accéder à un regroupement contenant ces ressources doit leur être attribué. Vous pouvez sélectionner des regroupements d'utilisateurs ou d'appareils.  

 Pour plus d’informations sur les regroupements, consultez [Présentation des regroupements dans System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md).  

 Avant de configurer l'administration basée sur les rôles, vérifiez si vous devez créer de nouveaux regroupements pour l'une des raisons suivantes :  

-   Organisation fonctionnelle. Par exemple, des regroupements distincts de serveurs et de stations de travail.  

-   Implantation géographique. Par exemple, des regroupements distincts pour l'Amérique du Nord et l'Europe.  

-   Exigences de sécurité et procédures commerciales. Par exemple, des regroupements distincts pour les ordinateurs de production et de test.  

-   Alignement de l'organisation. Par exemple, des regroupements distincts pour chaque unité d'exploitation.  

Pour plus d’informations sur la façon de configurer des regroupements pour l’administration basée sur des rôles, consultez [Configurer des regroupements pour gérer la sécurité](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) dans la rubrique [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

##  <a name="bkmk_PlanScope"></a> Étendues de sécurité  
 Utilisez les étendues de sécurité pour permettre aux utilisateurs administratifs d'accéder à des objets sécurisables. Une étendue de sécurité est un ensemble nommé d’objets sécurisables attribués aux utilisateurs administratifs en tant que groupe. Tous les objets sécurisables doivent être affectés à une ou plusieurs étendues de sécurité. Configuration Manager possède deux étendues de sécurité intégrées :  

-   L’étendue de sécurité intégrée *Toutes* accorde l’accès à toutes les étendues. Vous ne pouvez pas attribuer d'objets à cette étendue de sécurité.  

-   L’étendue de sécurité intégrée *Par défaut* est utilisée pour tous les objets, par défaut. Lorsque vous installez Configuration Manager pour la première fois, tous les objets sont attribués à cette étendue de sécurité.  

Si vous souhaitez restreindre les objets que les utilisateurs administratifs peuvent voir et gérer, vous devez créer et utiliser vos propres étendues de sécurité personnalisées. Les étendues de sécurité ne prennent pas en charge une structure hiérarchique et ne peuvent pas être imbriquées. Les étendues de sécurité peuvent contenir un ou plusieurs types d'objet, dont les suivants :  

-   Abonnements aux alertes  

-   Applications  

-   Images de démarrage  

-   Groupes de limites  

-   Éléments de configuration  

-   Paramètres client personnalisés  

-   Points de distribution et groupes de points de distribution  

-   Packages de pilotes  

-   Conditions globales  

-   Tâches de migration  

-   Images du système d'exploitation  

-   Packages d'installation du système d'exploitation  

-   Packages  

-   Requêtes  

-   Sites  

-   Règles de contrôle de logiciel  

-   Groupes de mises à jour logicielles  

-   Packages de mises à jour logicielles  

-   Packages de séquence de tâches  

-   Éléments et packages des paramètres de l'appareil Windows CE  

Certains objets ne peuvent pas être ajoutés aux étendues de sécurité, car ils ne sont sécurisés que par les rôles de sécurité. L’accès administratif à ces objets ne peut pas être limité à un sous-ensemble des objets disponibles. Par exemple, vous pouvez être un utilisateur administratif et créer des groupes de limites qui sont utilisés pour un site spécifique. Comme l'objet de la limite ne prend pas en charge les étendues de sécurité, vous ne pouvez pas attribuer à cet utilisateur une étendue de sécurité ne lui accordant que l'accès aux limites qui pourraient être associées à ce site. Comme l'objet de la limite ne peut pas être associé à une étendue de sécurité, lorsque vous attribuez un rôle de sécurité qui comprend l'accès aux objets de la limite à un utilisateur, celui-ci peut accéder à toutes les limites de la hiérarchie.  

Parmi les objets qui ne sont pas limités par des étendues de sécurité, on compte les objets suivants :  

-   Forêts Active Directory  

-   Utilisateurs administratifs  

-   Alertes  

-   Stratégies anti-programme malveillant  

-   Limites  

-   Associations d'ordinateurs  

-   Paramètres client par défaut  

-   Modèles de déploiement  

-   Pilotes d'appareils  

-   Connecteur Exchange Server  

-   Mappages de site à site de migration  

-   Profil d'inscription d'appareil mobile  

-   Rôles de sécurité  

-   Étendues de sécurité  

-   Adresses de site  

-   Rôles système de site  

-   Titres des logiciels  

-   Mises à jour logicielles  

-   Messages d'état  

-   Affinités des appareils d'utilisateur  

Créez des étendues de sécurité lorsque vous devez limiter l'accès à des instances d'objets distinctes. Par exemple :  

-   Vous disposez d'un groupe d'utilisateurs administratifs qui doit être capable de consulter les applications de production, mais pas les applications de test. Créer une étendue de sécurité pour les applications de production et une autre pour les applications de test.  

-   Différents utilisateurs administratifs nécessitent différents accès pour certaines instances d'un type d'objet. Par exemple, un groupe d’utilisateurs administratifs requiert l’autorisation Lire pour des groupes de mises à jour logicielles spécifiques et un autre groupe d’utilisateurs administratifs requiert les autorisations Modifier et Supprimer pour d’autres groupes de mises à jour logicielles. Créez différentes étendues de sécurité pour ces groupes de mises à jour logicielles.  

Pour plus d’informations sur la façon de configurer des étendues de sécurité pour l’administration basée sur des rôles, consultez [Configurer des étendues de sécurité pour un objet](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) dans la rubrique [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  
