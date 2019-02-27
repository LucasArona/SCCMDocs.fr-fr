---
title: Concevoir une hiérarchie de site
titleSuffix: Configuration Manager
description: Découvrez les topologies et les options de gestion disponibles pour Configuration Manager afin de planifier votre hiérarchie de sites.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74b8f7b099e906856300f5cc76b807daf894e060
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120076"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Concevoir une hiérarchie de sites pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’installer le premier site d’une nouvelle hiérarchie Configuration Manager, il est judicieux de bien comprendre :  

- Les topologies disponibles pour Configuration Manager  

- Les types de sites disponibles et leurs relations entre eux  

- L’étendue de la gestion fournie par chaque type de site  

- Les options de gestion de contenu qui peuvent réduire le nombre de sites que vous devez installer  

Ensuite, planifiez une topologie qui répond efficacement à vos besoins métier actuels et qui peut s’étendre plus tard pour gérer leur croissance future.  

Lors de la planification, gardez à l’esprit les limitations qui s’appliquent à l’ajout de sites supplémentaires à une hiérarchie ou à un site autonome :  

- Installez un nouveau site principal sous un site d’administration centrale, jusqu’au [nombre de sites principaux pris en charge](/sccm/core/plan-design/configs/size-and-scale-numbers) pour la hiérarchie.  

- [Développez un site principal autonome pour installer un nouveau site d’administration centrale](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), pour ensuite installer des sites principaux supplémentaires.  

- Installez de nouveaux sites secondaires sous un site principal, jusqu’à la [limite prise en charge pour le site principal](/sccm/core/plan-design/configs/size-and-scale-numbers) et la hiérarchie globale.  

- Vous ne pouvez pas ajouter un site précédemment installé dans une hiérarchie existante pour fusionner deux sites autonomes. Configuration Manager prend en charge l’installation de nouveaux sites seulement dans une hiérarchie de sites existante.  


> [!NOTE]  
> Quand vous planifiez une nouvelle installation de Configuration Manager, tenez compte des [notes de publication](/sccm/core/servers/deploy/install/release-notes) qui décrivent en détail les problèmes dans les versions actives. Les notes de publication s’appliquent à toutes les branches de Configuration Manager. Quand vous utilisez la [branche de la version Technical Preview](/sccm/core/get-started/technical-preview), vous rencontrez des problèmes spécifiques à cette branche dans la documentation pour chaque version Technical Preview.  



##  <a name="bkmk_topology"></a> Topologie de la hiérarchie  

Les topologies de hiérarchie vont :  

- Du plus simple : Un seul site principal autonome  

- Au plus complexe : Un groupe des sites principaux et secondaires connectés avec un site d’administration centrale sur le site de niveau supérieur de la hiérarchie  

Le principal facteur qui détermine le type et le nombre de sites que vous utilisez dans une hiérarchie est généralement le nombre et le type d’appareils que vous devez prendre en charge.   

### <a name="standalone-primary-site"></a>Site principal autonome

Utilisez un site principal autonome quand il peut prendre en charge la gestion de tous vos appareils et utilisateurs. Pour plus d’informations, consultez [Le redimensionnement et la mise à l’échelle en nombres](/sccm/core/plan-design/configs/size-and-scale-numbers). Cette topologie convient également quand les emplacements géographiques de votre entreprise peuvent être desservis par un même site principal. Pour faciliter la gestion du trafic réseau, utilisez plusieurs points de gestion dans des groupes de limites et une infrastructure de contenu soigneusement planifiée. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups) et [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

Cette topologie offre les avantages suivants :  

- Surcharge administrative simplifiée  

- Attribution des sites clients simplifiée et découverte des services et des ressources disponibles  

- Élimination des retards possibles engendrés par la réplication de base de données entre sites  

- Possibilité de développer un site principal autonome en une hiérarchie plus grande avec un site d’administration centrale. Ceci vous permet d’installer ensuite de nouveaux sites principaux pour étendre la taille de votre déploiement.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Site d’administration centrale avec un ou plusieurs sites principaux enfants. 

Utilisez cette topologie quand vous avez besoin de plusieurs sites principaux pour prendre en charge la gestion de tous les appareils et utilisateurs. Elle est nécessaire quand vous avez besoin d’utiliser plusieurs sites principaux. 

Cette topologie offre les avantages suivants :  

- Elle prend en charge jusqu’à 25 sites principaux, ce qui vous permet d’étendre l’échelle de votre hiérarchie.    

- Vous utilisez toujours le site d’administration centrale, sauf si vous réinstallez vos sites. Cette option est définitive. Vous ne pouvez pas détacher un site principal enfant pour en faire un site principal autonome.  



##  <a name="BKMK_ChooseCAS"></a> Déterminer quand utiliser un site d’administration centrale  

Utilisez un site d'administration centrale pour configurer des paramètres à l'échelle de la hiérarchie et surveiller tous les sites et objets dans la hiérarchie. Ce type de site ne gère pas directement les clients. Il coordonne la réplication de données de site à site, y compris la configuration de sites et de clients dans toute la hiérarchie.  

Les informations suivantes peuvent vous aider à déterminer quand installer un site d’administration centrale :  

- Le site d'administration centrale est le site de niveau supérieur dans une hiérarchie.  

- Quand vous configurez une hiérarchie comprenant plusieurs sites principaux, installez un site d’administration centrale.  

     - Si vous avez immédiatement besoin de deux sites principaux ou plus, installez d’abord le site d’administration centrale.  

     - Si vous disposez déjà d’un site principal et que vous voulez installer un site d’administration centrale, [étendez le site principal autonome](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand) pour installer le site administration centrale.  

- Le site d'administration centrale prend en charge uniquement des sites principaux en tant que sites enfants.  

- Vous ne pouvez pas affecter de clients au site d’administration centrale.  

- Le site d’administration centrale ne prend pas en charge les rôles de système de site qui prennent directement en charge les clients, comme les points de gestion et les points de distribution.  

- Gérez tous les clients de la hiérarchie et effectuez toutes les tâches de gestion des sites à partir de la console Configuration Manager connectée au site d’administration centrale. Ces tâches peuvent inclure l’installation de points de gestion ou d’autres rôles de système de site sur des sites principaux ou secondaires enfants.  

- Quand vous utilisez un site d’administration centrale, il s’agit du seul emplacement où vous pouvez consulter les données de tous les sites de votre hiérarchie. Ces données incluent des informations telles que des données d'inventaire et des messages d'état.  

- Configurez des opérations de découverte dans toute la hiérarchie à partir du site d’administration centrale. À partir du site d’administration centrale, affectez des méthodes de découverte à exécuter sur des sites principaux spécifiques.  

- Gérez la sécurité dans toute la hiérarchie en attribuant différents rôles de sécurité, étendues de sécurité et regroupements à différents utilisateurs administratifs. Ces configurations s'appliquent à chaque site dans la hiérarchie.  

- Configurez la réplication pour contrôler la communication entre les sites de la hiérarchie. Planifiez la réplication de base de données pour les données de site, et gérez la bande passante pour le transfert de données basées sur des fichiers entre les sites.  



##  <a name="BKMK_ChoosePriimary"></a> Déterminer quand utiliser un site principal  

Utilisez les sites principaux pour gérer les clients. Installez un site principal comme site principal enfant sous un site d’administration centrale, ou comme premier site d’une nouvelle hiérarchie. Un site principal qui est le premier site d’une hiérarchie crée un site principal autonome. Les sites principaux enfants et les sites principaux autonomes prennent en charge les sites secondaires.  

Envisagez d’ajouter des sites principaux supplémentaires pour les raisons suivantes :  

- Pour augmenter le nombre d’appareils gérés avec une même hiérarchie.  

- Pour répondre aux exigences de gestion organisationnelles. Par exemple, vous pouvez installer un site principal à un emplacement distant pour gérer le transfert de contenu de déploiement dans un réseau à faible bande passante.  

     - Envisagez à la place d’utiliser des options pour limiter la bande passante réseau lors du transfert de données vers un point de distribution. Cette fonctionnalité de gestion du contenu peut remplacer le besoin d’installer des sites supplémentaires.  


Les informations suivantes peuvent vous aider à déterminer quand installer un site principal :  

- Un site principal peut être un site principal autonome ou un site principal enfant dans une hiérarchie plus grande. Lorsqu'un site principal est membre d'une hiérarchie avec un site d'administration centrale, les sites utilisent la réplication de base de données pour répliquer des données entre les sites. Sauf si vous avez besoin de prendre en charge un nombre de clients et d’appareils supérieur à la capacité d’un seul site principal, envisagez l’installation d’un site principal autonome. Après avoir installé un site principal autonome, étendez-le si nécessaire ultérieurement pour qu’il rende compte à un nouveau site d’administration centrale et pour faire monter votre déploiement en puissance.  

- Un site principal prend en charge uniquement un site d'administration centrale en tant que site parent.  

- Un site principal prend en charge seulement des sites secondaires comme sites enfants, et il prend en charge plusieurs sites secondaires.  

- Les sites principaux sont chargés de traiter toutes les données du client à partir de leurs clients attribués.  

- Les sites principaux utilisent la réplication de base de données pour communiquer directement avec leur site d'administration centrale. Ce comportement est configuré automatiquement lors de l’installation d’un nouveau site.  



##  <a name="BKMK_ChooseSecondary"></a> Déterminer quand utiliser un site secondaire  

Utilisez des sites secondaires pour gérer le transfert de contenu de déploiement et de données client dans les réseaux à faible bande passante.  

Vous gérez un site secondaire à partir d’un site d’administration centrale ou du site principal parent direct du site secondaire. Les sites secondaires sont attachés à un site principal. Vous ne pouvez pas les déplacer vers un autre site parent sans les avoir préalablement désinstallés, puis réinstallés comme sites enfants sous le nouveau site principal.

Toutefois, vous pouvez acheminer du contenu entre deux sites secondaires homologues pour aider à gérer la réplication basée sur les fichiers du contenu de déploiement. Pour transférer des données du client vers un site principal, le site secondaire utilise la réplication basée sur les fichiers. Un site secondaire utilise également la réplication de base de données pour communiquer avec son site principal parent.  

Envisagez d'installer un site secondaire si l'une des conditions suivantes est remplie :  

- Vous n’avez pas besoin d’un point de connectivité local pour un utilisateur administratif.  

- Vous devez gérer le transfert du contenu de déploiement vers des sites qui se trouvent à un niveau inférieur dans la hiérarchie.  

- Vous devez gérer des informations clientes qui sont envoyées à des sites à un niveau supérieur dans la hiérarchie.  

Si vous ne voulez pas installer un site secondaire et que vous avez des clients dans des emplacements distants, envisagez les options suivantes :  

- Utiliser des technologies de pair à pair, comme Windows BranchCache  

- Activer le contrôle de la bande passante et la planification pour les points de distribution   

Utilisez ces options de gestion de contenu avec ou sans sites secondaires. Elles permettent de réduire la taille de votre infrastructure Configuration Manager. Pour plus d’informations sur les options de gestion de contenu dans Configuration Manager, consultez [Déterminer quand utiliser les options de gestion de contenu](#BKMK_ChooseSecondaryorDP).  


Les informations suivantes peuvent vous aider à déterminer quand installer un site secondaire :  

- Si une instance locale de SQL Server n’est pas disponible, les serveurs de sites secondaires installent automatiquement SQL Server Express lors de l’installation des sites.  

- Une installation de site secondaire est lancée à partir de la console Configuration Manager, au lieu d’exécuter le programme d’installation directement sur un ordinateur.  

- Les sites secondaires utilisent un sous-ensemble des informations de la base de données de site. Ce comportement réduit la quantité de données répliquées par SQL entre le site principal parent et le site secondaire.  

- Les sites secondaires prennent en charge l'acheminement de contenu basé sur des fichiers vers d'autres sites secondaires qui possèdent un site principal parent commun.  

- Les installations de sites secondaires installent automatiquement un point de gestion et des rôles de système de site de point de distribution sur le serveur de site secondaire.  



##  <a name="BKMK_ChooseSecondaryorDP"></a> Déterminer quand utiliser les options de gestion de contenu  

Si vous possédez des clients dans des emplacements réseau distants, envisagez d'utiliser une ou plusieurs options de gestion de contenu plutôt qu'un site principal ou secondaire. Les options suivantes permettent souvent de ne pas devoir installer un site :  

- Optimisation de la distribution pour Windows 10  

- Cache entre pairs Configuration Manager  

- Windows BranchCache  

- Configurer des points de distribution pour le contrôle de la bande passante  

- Copier manuellement du contenu sur les points de distribution (préparation du contenu)  


Si une des conditions suivantes s’applique, envisagez de déployer un point de distribution au lieu d’installer un autre site :  

- Votre bande passante réseau est suffisante pour que les ordinateurs clients à l’emplacement distant puissent communiquer avec un point de gestion sur le site principal. Les clients communiquent avec un point de gestion pour télécharger une stratégie cliente, envoyer l’inventaire, envoyer l’état de la génération de rapports et envoyer des informations de découverte.  

- Le service de transfert intelligent en arrière-plan (BITS, Background Intelligent Transfer Service) ne fournit pas un contrôle suffisant de la bande passante pour les besoins de votre réseau.  

Pour plus d’informations sur les options de gestion de contenu dans Configuration Manager, consultez [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  



##  <a name="bkmk_beyond"></a> Au-delà de la topologie de la hiérarchie  

En même temps que la topologie de votre hiérarchie initiale, prenez également en compte les questions suivantes :  

- Quels rôles de système de site fournissent des services ou des fonctionnalités des différents sites de la hiérarchie ?  

- Comment gérez-vous les configurations et les fonctionnalités à l’échelle de la hiérarchie dans votre infrastructure ?  


Les considérations courantes suivantes sont traitées dans des articles distincts. Ces informations sont importantes, car elles peuvent influencer la conception de votre hiérarchie ou être influencées par celle-ci :  

- Quand vous vous préparez à [gérer des ordinateurs et des appareils](/sccm/core/clients/manage/manage-clients), déterminez si les appareils sont locaux, dans le cloud ou BYOD. Considérez aussi comment vous voulez gérer les appareils qui prennent en charge plusieurs options de gestion. Par exemple, gérer des appareils Windows 10 avec Configuration Manager ou via l’intégration à Microsoft Intune. Pour plus d’informations, consultez [Choisir une solution de gestion d’appareils](/sccm/core/plan-design/choose-a-device-management-solution).  

- Comprenez bien comment votre infrastructure réseau disponible peut avoir une incidence sur le flux des données entre sites distants. Pour plus d’informations, consultez [Préparer votre environnement réseau](/sccm/core/plan-design/network/configure-firewalls-ports-domains). Considérez également l’emplacement géographique de vos utilisateurs et appareils, et déterminez s’ils accèdent à votre infrastructure via votre réseau local ou via Internet.  

- Planifiez une infrastructure de contenu de façon à distribuer efficacement le contenu que vous déployez sur les appareils que vous gérez. Ce contenu peut être des applications, des mises à jour logicielles ou des systèmes d’exploitation. Pour plus d’informations, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

- Déterminer quelles [fonctions et fonctionnalités de Configuration Manager](/sccm/core/plan-design/changes/features-and-capabilities) vous prévoyez d’utiliser. Les différentes fonctionnalités nécessitent des rôles de système de site différents ou une infrastructure Windows différente. Dans une hiérarchie avec plusieurs sites, décidez où vous les déployez pour une utilisation optimale de vos ressources réseau et serveur.  

- Prenez en compte la sécurité des données et des appareils, notamment l’utilisation d’une infrastructure à clé publique (PKI). Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


Passez en revue les articles suivants pour les configurations spécifiques aux sites :  

- [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider)  

- [Planifier la base de données du site](/sccm/core/plan-design/hierarchy/plan-for-the-site-database)  

- [Planifier des serveurs de système de site et des rôles de système de site](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles)  

- [Planifier la sécurité](/sccm/core/plan-design/security/plan-for-security)  

- [Managing network bandwidth](/sccm/core/plan-design/hierarchy/manage-network-bandwidth) lors du déploiement de contenu dans un site  


Prendre en compte les configurations qui couvrent plusieurs sites et hiérarchies  

- [Options de haute disponibilité](/sccm/protect/understand/high-availability-options) pour les sites et les hiérarchies

- [Étendre le schéma Active Directory](/sccm/core/plan-design/network/extend-the-active-directory-schema) et configurer des sites pour [publier des données de site](/sccm/core/servers/deploy/configure/publish-site-data)  

- [Transferts de données entre sites](/sccm/core/servers/manage/data-transfers-between-sites)  

- [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration)  

- [Gérer les clients sur Internet](/sccm/core/clients/manage/manage-clients-internet)  

