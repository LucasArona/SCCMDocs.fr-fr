---
title: 'Concevoir une hiérarchie de site '
titleSuffix: Configuration Manager
description: Découvrez les topologies et les options de gestion disponibles pour System Center Configuration Manager afin de pouvoir planifier votre hiérarchie de site.
ms.date: 8/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 602d9455dcdd69209ef8ba157916b35db976b89f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344651"
---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Concevoir une hiérarchie de sites pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’installer le premier site d’une nouvelle hiérarchie System Center Configuration Manager, il est judicieux de comprendre les topologies disponibles pour Configuration Manager, les types de sites disponibles et leurs relations mutuelles, ainsi que l’étendue de gestion fournie par chaque type de site.
Après avoir étudié les options de gestion de contenu qui peuvent réduire le nombre de sites à installer, vous pouvez planifier une topologie qui répond efficacement aux besoins de votre entreprise et peut être étendue par la suite pour gérer la croissance à venir.  

Lors de la planification, gardez à l’esprit les restrictions qui s’appliquent à l’ajout de sites supplémentaires à une hiérarchie ou à un site autonome :
-   Vous pouvez installer un nouveau site principal sous un site d’administration centrale, jusqu'au [nombre de sites principaux pris en charge](/sccm/core/plan-design/configs/size-and-scale-numbers) pour la hiérarchie.
-   Vous pouvez [développer un site principal autonome pour installer un nouveau site d’administration centrale](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), ce qui vous permet d’installer des sites principaux supplémentaires.
-   Vous pouvez installer de nouveaux sites secondaires sous un site principal, jusqu'aux [limites prises en charge pour le site principal](/sccm/core/plan-design/configs/size-and-scale-numbers) et la hiérarchie globale.
-   Vous ne pouvez pas ajouter un site précédemment installé dans une hiérarchie existante en vue de fusionner deux sites autonomes. Seule l’installation de nouveaux sites dans une hiérarchie existante de sites est prise en charge.


> [!NOTE]
> Quand vous planifiez une nouvelle installation de Configuration Manager, tenez compte des [notes de publication]( /sccm/core/servers/deploy/install/release-notes) qui décrivent en détail les problèmes dans les versions actives. Les notes de publication s’appliquent à toutes les branches de Configuration Manager.  Toutefois, quand vous utilisez l’[édition Technical Preview]( /sccm/core/get-started/technical-preview), vous rencontrez des problèmes spécifiques uniquement à cette édition dans la documentation pour chaque version de Technical Preview.  

##  <a name="bkmk_topology"></a> Topologie de la hiérarchie  
 Les topologies de hiérarchie peuvent aller d’un site principal autonome unique à un groupe de sites principaux et secondaires connectés avec un site d’administration centrale dans le site de niveau supérieur de la hiérarchie.   Le principal facteur qui détermine le type et le nombre de sites que vous utilisez dans une hiérarchie est généralement le nombre et le type d’appareils que vous devez prendre en charge, comme illustré ci-dessous :   

 **Site principal autonome :** utilisez un site principal autonome quand un seul site principal peut prendre en charge la gestion de tous vos appareils et utilisateurs (consultez [Le dimensionnement et la mise à l’échelle en nombres](/sccm/core/plan-design/configs/size-and-scale-numbers)). Cette topologie convient également quand les différents emplacements géographiques de votre société peuvent être correctement servis par un seul site principal.  Pour mieux gérer le trafic réseau, vous pouvez utiliser des points de gestion préférés et une infrastructure de contenu soigneusement planifiée (consultez [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)).  

 Les avantages de cette topologie sont notamment les suivants :  

-   Surcharge administrative simplifiée.  

-   Attribution des sites clients simplifiée et découverte des services et des ressources disponibles.  

-   Élimination du retard possible engendré par la réplication de base de données entre sites.

-   Possibilité de développer une hiérarchie principale autonome en une hiérarchie plus grande avec un site d’administration centrale. Cela vous permet d’installer ensuite de nouveaux sites principaux pour étendre l’échelle de votre déploiement.  


**Site d’administration centrale avec un ou plusieurs sites principaux enfants :** Utilisez cette topologie quand vous avez besoin de plusieurs sites principaux pour prendre en charge la gestion de tous les appareils et utilisateurs.  Elle est nécessaire quand vous avez besoin d’utiliser plusieurs sites principaux. Les avantages de cette topologie sont notamment les suivants :  


-   Elle prend en charge jusqu’à 25 sites principaux, ce qui vous permet d’étendre l’échelle de votre hiérarchie.  

-   Vous utiliserez toujours le site d’administration centrale, sauf si vous réinstallez vos sites. Ce choix est définitif. Vous ne pouvez pas détacher un site principal enfant pour en faire un site principal autonome.

 Les sections suivantes peuvent vous aider à déterminer quand utiliser un site ou une option de gestion de contenu spécifique plutôt qu’un site supplémentaire.  

##  <a name="BKMK_ChooseCAS"></a> Déterminer quand utiliser un site d’administration centrale  
 Utilisez un site d'administration centrale pour configurer des paramètres à l'échelle de la hiérarchie et surveiller tous les sites et objets dans la hiérarchie. Ce type de site ne gère pas directement les clients, mais il coordonne la réplication de données inter-site, y compris la configuration de sites et de clients dans toute la hiérarchie.  

**Les informations suivantes peuvent vous aider à déterminer quand installer un site d’administration centrale :**  

-   Le site d'administration centrale est le site de niveau supérieur dans une hiérarchie.  

-   Lorsque vous configurez une hiérarchie comprenant plusieurs sites principaux, vous devez installer un site d'administration centrale. Si vous avez immédiatement besoin de deux ou plusieurs sites principaux, installez tout d’abord le site d’administration centrale. Si vous disposez déjà d’un site principal et que vous souhaitez installer un site d’administration centrale, vous devez [développer le site principal autonome](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) pour installer le site administration centrale.

-   Le site d'administration centrale prend en charge uniquement des sites principaux en tant que sites enfants.  

-   Vous ne pouvez pas attribuer de clients au site d'administration centrale.  

-   Le site d’administration centrale ne prend pas en charge les rôles de système de site qui prennent directement en charge les clients, comme les points de gestion et les points de distribution.  

-   Vous pouvez gérer tous les clients dans la hiérarchie et exécuter des tâches de gestion de site pour tout site enfant quand vous utilisez une console Configuration Manager connectée au site d’administration centrale. Cela peut comprendre l’installation de points de gestion ou d’autres rôles de système de site sur des sites principaux ou secondaires enfants.  

-   Quand vous utilisez un site d’administration centrale, il s’agit du seul emplacement où vous pouvez consulter les données de tous les sites de votre hiérarchie. Ces données incluent des informations telles que des données d'inventaire et des messages d'état.  

-   Vous pouvez configurer des opérations de découverte dans toute la hiérarchie à partir du site d'administration centrale en attribuant l'exécution de méthodes de découverte sur des sites individuels.  

-   Vous pouvez gérer la sécurité dans toute la hiérarchie en attribuant différents rôles de sécurité, étendues de sécurité et regroupements à différents utilisateurs administratifs. Ces configurations s'appliquent à chaque site dans la hiérarchie.  

-   Vous pouvez configurer la réplication de fichiers et la réplication de base de données pour contrôler la communication entre les sites de la hiérarchie. Cela consiste notamment à planifier la réplication de base de données pour les données de site et à gérer la bande passante pour le transfert de données basées sur des fichiers entre les sites.  

##  <a name="BKMK_ChoosePriimary"></a> Déterminer quand utiliser un site principal  
 Utilisez les sites principaux pour gérer les clients. Vous pouvez installer un site principal en tant que site principal enfant sous un site d’administration centrale, ou en tant que premier site d’une nouvelle hiérarchie. Un site principal installé en tant que premier site d’une hiérarchie crée un site principal autonome. Les sites principaux enfants et les sites principaux autonomes prennent en charge les sites secondaires en tant que sites enfants du site principal.  

 Utilisez un site principal pour l’une des raisons suivantes :  

-   Pour gérer des appareils et des utilisateurs.  

-   Pour augmenter le nombre d’appareils que vous pouvez gérer avec une hiérarchie unique.  

-   Pour fournir un point de connectivité supplémentaire pour l’administration de votre déploiement.  

-   Pour répondre aux exigences de gestion organisationnelles. Par exemple, vous pouvez installer un site principal à un emplacement distant pour gérer le transfert de contenu de déploiement dans un réseau à faible bande passante. Cependant, avec System Center Configuration Manager, vous pouvez utiliser des options pour limiter l’utilisation de la bande passante réseau lors du transfert de données vers un point de distribution. Cette fonctionnalité de gestion du contenu peut remplacer le besoin d’installer des sites supplémentaires.  


**Les informations suivantes peuvent vous aider à déterminer quand installer un site principal :**  

-   Un site principal peut être un site principal autonome ou un site principal enfant dans une hiérarchie plus grande. Lorsqu'un site principal est membre d'une hiérarchie avec un site d'administration centrale, les sites utilisent la réplication de base de données pour répliquer des données entre les sites. Sauf si vous avez besoin de prendre en charge un nombre de clients et de périphériques supérieur à la capacité d'un seul site principal, envisagez l'installation d'un site principal autonome.  Après l’installation d’un site principal autonome, vous pouvez l’étendre pour qu’il rende compte à un nouveau site d’administration centrale, pour faire monter votre déploiement en puissance.  

-   Un site principal prend en charge uniquement un site d'administration centrale en tant que site parent.  

-   Un site principal prend en charge uniquement des sites secondaires en tant que sites enfants, et peut aussi prendre en charge plusieurs sites enfants secondaires.  

-   Les sites principaux sont chargés de traiter toutes les données du client à partir de leurs clients attribués.  

-   Les sites principaux utilisent la réplication de base de données pour communiquer directement avec leur site d’administration centrale (qui est configuré automatiquement lors de l’installation d’un nouveau site).  

##  <a name="BKMK_ChooseSecondary"></a> Déterminer quand utiliser un site secondaire  
 Utilisez des sites secondaires pour gérer le transfert de contenu de déploiement et de données client dans les réseaux à faible bande passante.  

 Vous gérez un site secondaire à partir d’un site d’administration centrale ou du site principal parent direct du site secondaire. Vous devez associer les sites secondaires à un site principal, et vous ne pouvez pas les déplacer vers un autre site parent sans les avoir préalablement désinstallés puis réinstallés en tant que site enfant sous le nouveau site principal.

Toutefois, vous pouvez acheminer du contenu entre deux sites secondaires homologues pour aider à gérer la réplication basée sur les fichiers du contenu de déploiement. Pour transférer des données du client vers un site principal, le site secondaire utilise la réplication basée sur les fichiers. Un site secondaire utilise également la réplication de base de données pour communiquer avec son site principal parent.  

 Envisagez d'installer un site secondaire si l'une des conditions suivantes est remplie :  

-   Vous n’avez pas besoin de point de connectivité local pour un utilisateur administratif.  

-   Vous devez gérer le transfert de contenu de déploiement vers des sites qui se trouvent à un niveau inférieur dans la hiérarchie.  

-   Vous devez gérer des informations clientes qui sont envoyées à des sites à un niveau supérieur dans la hiérarchie.  

 Si vous ne souhaitez pas installer de site secondaire et que vous avez des clients à des emplacements distants, utilisez Windows BranchCache ou installez des points de distribution qui sont activés pour la planification et le contrôle de la bande passante. Vous pouvez utiliser ces options de gestion de contenu avec ou sans sites secondaires et elles peuvent vous aider à réduire le nombre de sites et de serveurs que vous devez installer. Pour plus d’informations sur les options de gestion de contenu dans Configuration Manager, consultez [Déterminer quand utiliser les options de gestion de contenu](#BKMK_ChooseSecondaryorDP).  


**Les informations suivantes peuvent vous aider à déterminer quand installer un site secondaire :**  

-   Les sites secondaires installent automatiquement SQL Server Express lors de l'installation de site si une instance locale de SQL Server n'est pas disponible.  

-   Une installation de site secondaire est lancée à partir de la console Configuration Manager plutôt qu’en exécutant le programme d’installation directement sur un ordinateur.  

-   Les sites secondaires utilisent un sous-ensemble des informations contenues dans la base de données de site, ce qui réduit la quantité de données répliquées par la réplication de base de données entre le site principal et le site secondaire.  

-   Les sites secondaires prennent en charge l'acheminement de contenu basé sur des fichiers vers d'autres sites secondaires qui possèdent un site principal parent commun.  

-   Les installations de site secondaire déploient automatiquement un point de gestion et un point de distribution situés sur le serveur de site secondaire.  

##  <a name="BKMK_ChooseSecondaryorDP"></a> Déterminer quand utiliser les options de gestion de contenu  
 Si vous possédez des clients dans des emplacements réseau distants, envisagez d'utiliser une ou plusieurs options de gestion de contenu plutôt qu'un site principal ou secondaire. Souvent, vous n’avez pas besoin d’installer un site quand vous utilisez Windows BranchCache, quand vous configurez des points de distribution pour le contrôle de la bande passante, ou quand vous copiez manuellement du contenu vers des points de distribution (préparation du contenu).  


**Envisagez de déployer un point de distribution plutôt que d’installer un autre site si l’une des conditions suivantes s’applique :**  

-   Votre bande passante réseau est suffisante pour que les ordinateurs clients situés à l'emplacement distant communiquent avec un point de gestion afin de télécharger une stratégie client et envoient un inventaire, un état du rapport et des informations de découverte.  

-   Le service de transfert intelligent en arrière-plan (BITS) ne fournit pas de contrôle de bande passante suffisant pour les besoins de votre réseau.  

 Pour plus d’informations sur les options de gestion de contenu dans Configuration Manager, consultez [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

##  <a name="bkmk_beyond"></a> Au-delà de la topologie de la hiérarchie  
 En plus de la topologie de la hiérarchie initiale, réfléchissez aux services ou aux fonctionnalités qui seront disponibles à partir de différents sites dans la hiérarchie (rôles de système de site), et à la façon dont les fonctionnalités et configurations à l’échelle de la hiérarchie seront gérées dans votre infrastructure. Les considérations courantes suivantes sont traitées dans des rubriques distinctes. Ces éléments sont importants, car ils peuvent influencer la conception de votre hiérarchie ou être influencés par celle-ci :  

-   Quand vous vous préparez à [gérer des ordinateurs et des appareils avec System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), déterminez si les appareils que vous gérez sont locaux, situés dans le cloud ou comptent des appareils appartenant à l’utilisateur (BYOD).  Étudiez également la façon dont vous allez gérer les appareils qui sont pris en charge par plusieurs options de gestion, tels que des ordinateurs Windows 10 pouvant être gérés directement par Configuration Manager ou via l’intégration à Microsoft Intune.  

-   Découvrez comment votre infrastructure réseau disponible peut affecter le flux de données entre des sites distants (consultez [Préparer votre environnement réseau pour System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains)). Tenez aussi compte de l’emplacement géographique des utilisateurs et appareils que vous gérez, et déterminez s’ils accèdent à votre infrastructure par l’intermédiaire de votre domaine d’entreprise ou d’Internet.  

-   Planifiez une infrastructure de contenu pour distribuer efficacement les informations que vous déployez (fichiers et applications) sur les appareils que vous gérez (consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)).  

-   Identifiez les [fonctions et fonctionnalités de System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) que vous envisagez d’utiliser, les rôles de système de site ou l’infrastructure Windows nécessaires ainsi que les sites au niveau desquels vous pouvez les déployer dans une hiérarchie comportant plusieurs sites pour une utilisation optimale du réseau et des ressources serveur.  

-   Prenez en compte la sécurité des données et des appareils, notamment l’utilisation d’une infrastructure à clé publique. Consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  


**Passez en revue les ressources suivantes pour les configurations spécifiques aux sites :**  

-   [Planifier le fournisseur SMS pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md)  

-   [Planifier la base de données du site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md)  

-   [Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)  

-   [Planifier la sécurité dans System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/manage-network-bandwidth.md) lors du déploiement de contenu dans un site  


**Tenez compte des configurations qui couvrent plusieurs sites et hiérarchies :**  

-   [Options de haute disponibilité pour System Center Configuration Manager](/sccm/protect/understand/high-availability-options) pour les sites et hiérarchies

-   [Étendre le schéma Active Directory pour System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) et configurer des sites pour la [publication de données de site pour System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)  

-   [Transfert de données entre sites dans System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md)
