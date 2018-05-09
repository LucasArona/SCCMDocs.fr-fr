---
title: Principes de base de la gestion de contenu
titleSuffix: Configuration Manager
description: Utilisez les outils et les options de Configuration Manager pour gérer le contenu que vous déployez.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5dfe33e7182eae158c15afb848d3a9f1702678ba
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Principes de base de la gestion de contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager fournit un puissant système d’outils et d’options pour vous aider à gérer le contenu que vous déployez (applications, packages, mises à jour logicielles et déploiements de système d’exploitation). Configuration Manager stocke le contenu à la fois sur les serveurs de site et sur les points de distribution. Le transfert de ce contenu d’un emplacement à un autre nécessite une large bande passante réseau. Pour planifier et utiliser efficacement l’infrastructure de gestion de contenu, de vous familiariser avec les options et configurations disponibles. Déterminez ensuite comment les utiliser au mieux en fonction de votre environnement réseau et de vos besoins en matière de déploiement de contenu.  

> [!TIP]    
> Pour obtenir plus d’informations sur le processus de distribution de contenu, ainsi que trouver de l’aide sur le diagnostic et la résolution des problèmes généraux relatifs à la distribution de contenu, consultez [Compréhension et résolution des problèmes de distribution de contenu dans Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Les rubriques suivantes exposent des concepts clés de la gestion de contenu. Si un concept doit être complété par des informations supplémentaires ou complexes, les liens d’accès à ces informations sont indiqués.



## <a name="accounts-used-for-content-management"></a>Comptes utilisés pour la gestion de contenu  
 Les comptes suivants peuvent être utilisés pour la gestion de contenu :  

-   **Compte d’accès réseau**: compte utilisé par les clients pour se connecter à un point de distribution et accéder au contenu. Par défaut, le compte d’ordinateur est utilisé en premier.  

     Ce compte est également utilisé par les points de distribution d’extraction pour télécharger du contenu à partir d’un point de distribution source dans une forêt distante.  

-   **Compte d’accès au package** : par défaut, Configuration Manager permet aux utilisateurs et aux administrateurs des comptes d’accès génériques d’accéder au contenu sur un point de distribution. Toutefois, vous pouvez configurer des autorisations supplémentaires pour limiter l’accès.   

-   **Compte de connexion multidiffusion** : utilisé pour les déploiements de système d’exploitation.  

Pour plus d’informations sur ces comptes, consultez [Gérer les comptes pour accéder au contenu](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitation et planification de la bande passante  
 La limitation et la planification sont des options qui vous aident à contrôler la distribution du contenu d’un serveur de site vers des points de distribution. Ces fonctionnalités sont similaires aux contrôles de bande passante pour la réplication de site à site basée sur des fichiers, sans leur être directement liés.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Réplication différentielle binaire  
 La réplication différentielle binaire est un prérequis pour les points de distribution. Elle est parfois simplement appelée « réplication différentielle ». Lors de la distribution de mises à jour à un contenu que vous avez précédemment déployé sur d’autres sites ou sur des points de distribution distants, la réplication différentielle binaire est automatiquement utilisée pour réduire la bande passante utilisée.  

 Cette fonctionnalité réduit la bande passante réseau utilisée lors de l’envoi des mises à jour du contenu distribué. Elle renvoie uniquement le contenu nouveau ou modifié au lieu d’envoyer l’ensemble complet des fichiers sources de contenu chaque fois qu’un changement est apporté à ces fichiers.  

 Quand vous utilisez la réplication différentielle binaire, Configuration Manager identifie les changements apportés aux fichiers sources pour chaque jeu de contenus que vous avez précédemment distribué.  

-   Quand des fichiers du contenu source changent, le site crée une nouvelle version incrémentielle du jeu de contenus. Il ne réplique ensuite que les fichiers modifiés sur les sites de destination et les points de destination. Un fichier est considéré comme modifié si vous l’avez renommé ou déplacé, ou si vous avez modifié son contenu. Par exemple, si vous remplacez un seul fichier de pilote pour un package de pilotes que vous avez précédemment distribué vers plusieurs sites, seul le fichier du pilote modifié est répliqué.  

-   Configuration Manager prend en charge jusqu’à cinq versions incrémentielles d’un jeu de contenus avant de renvoyer le jeu de contenus entier. Après la cinquième mise à jour, la modification suivante du jeu de contenus entraîne la création, par le site, d’une nouvelle version du jeu de contenus. Configuration Manager distribue ensuite la nouvelle version du jeu de contenus pour remplacer le jeu précédent et toutes ses versions incrémentielles. Après la distribution du nouveau jeu de contenus, les modifications incrémentielles ultérieures apportées aux fichiers sources sont de nouveau répliquées en utilisant la réplication différentielle binaire.  

La réplication différentielle binaire est prise en charge entre chaque site parent et enfant dans une hiérarchie. Elle est prise en charge dans un site entre le serveur de site et ses points de distribution normaux. Toutefois, les points de distribution d’extraction et les points de distribution cloud ne prennent pas en charge la réplication différentielle binaire pour le transfert de contenu. Les points de distribution d’extraction prennent en charge les deltas de niveau fichier et le transfert de nouveaux fichiers, mais pas les blocs au sein d’un fichier.

Les applications utilisent toujours la réplication différentielle binaire. La réplication différentielle binaire est facultative pour les packages et n’est pas activée par défaut. Pour utiliser la réplication différentielle binaire pour les packages, activez cette fonctionnalité pour chaque package. Sélectionnez l’option **Activer la réplication différentielle binaire** quand vous créez ou modifiez un package.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](/windows-server/networking/branchcache/branchcache) est une technologie Windows. Les clients prenant en charge BranchCache et ayant téléchargé un déploiement que vous configurez pour BranchCache font alors office de source de contenu pour d’autres clients BranchCache.  

 Par exemple, vous disposez d’un point de distribution qui exécute Windows Server 2012 ou une version ultérieure et qui est configuré comme serveur BranchCache. Quand le premier client prenant en charge BranchCache demande du contenu à partir de ce serveur, le client télécharge ce contenu et le met en cache.  

- Ce client met ensuite le contenu à la disposition d’autres clients BranchCache du même sous-réseau qui mettent également en cache le contenu.  
- Les autres clients du même sous-réseau n’ont pas à télécharger le contenu à partir du point de distribution.  
- Le contenu est distribué sur plusieurs clients, en vue de transferts futurs.  



## <a name="delivery-optimization"></a>Optimisation de la distribution
<!-- 1324696 -->
Les groupes de limites Configuration Manager permettent de définir et de réguler la distribution de contenu sur le réseau de l’entreprise et dans les agences. [L’Optimisation de la distribution de Windows](/windows/deployment/update/waas-delivery-optimization) est une technologie cloud pair à pair de partage de contenu entre appareils Windows 10. À compter de la version 1802, configurez-la de façon à ce qu’elle utilise vos groupes de limites pour partager du contenu entre homologues. Les paramètres client appliquent l’identificateur de groupe de limites comme identificateur du groupe Optimisation de la distribution sur le client. Lorsque le client communique avec le service de cloud d’Optimisation de la distribution, il utilise cet identificateur pour localiser les pairs possédant le contenu souhaité. Pour plus d’informations, consultez les paramètres client de l’[optimisation de la distribution](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).



## <a name="peer-cache"></a>Cache d’homologue
Le cache d’homologue client vous permet de gérer le déploiement de contenu sur les clients distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.

Une fois que vous avez déployé des paramètres client qui activent le cache d’homologue sur un regroupement, les membres de ce regroupement peuvent agir comme source de contenu homologue pour d’autres clients du même groupe de limites.

Pour plus d’informations, voir [Cache d’homologue pour les clients Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Mise en cache d’homologue Windows PE
Quand vous déployez un nouveau système d’exploitation avec Configuration Manager, les ordinateurs qui exécutent la séquence de tâches peuvent utiliser la mise en cache d’homologue Windows PE. Ils téléchargent le contenu à partir d’une source de mise en cache d’homologue au lieu de le télécharger à partir d’un point de distribution. Ce comportement permet de réduire le trafic WAN dans les scénarios de filiale où il n’existe aucun point de distribution local.

Pour plus d’informations, consultez [Mise en cache d’homologue Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).



## <a name="client-locations"></a>Emplacements des clients  
 Les clients accèdent au contenu à partir des emplacements suivants :  

-   **Intranet** (local) :  

    -   Les points de distribution peuvent utiliser HTTP ou HTTPS.  

    -   Utilisez uniquement un point de distribution cloud de secours quand les points de distribution locaux ne sont pas disponibles.  

-   **Internet** :  

    -   Exige des points de distribution qu’ils acceptent le protocole HTTPS.  

    -   Vous pouvez utiliser un point de distribution cloud de secours.  

-   **Groupe de travail**:  

    -   Exige des points de distribution qu’ils acceptent le protocole HTTPS.  

    -   Vous pouvez utiliser un point de distribution cloud de secours.  



## <a name="content-library"></a>Bibliothèque de contenu  
 La bibliothèque de contenu est un stockage SIS (Single-Instance-Store) de contenu dans Configuration Manager. Cette bibliothèque permet de réduire la taille globale du contenu que vous distribuez.  

- En savoir plus sur la [bibliothèque de contenu](../../../core/plan-design/hierarchy/the-content-library.md).
- Utilisez l’[outil de nettoyage de la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) pour supprimer le contenu qui n’est plus associé à une application.  



## <a name="distribution-points"></a>Points de distribution  
 Configuration Manager utilise des points de distribution pour stocker les fichiers nécessaires à l’exécution de logiciels sur les ordinateurs clients. Les clients doivent avoir accès à au moins un point de distribution à partir duquel ils peuvent télécharger les fichiers du contenu que vous déployez.  

 Le point de distribution (non spécifique) de base est communément appelé point de distribution standard. Il existe deux variantes du point de distribution standard qui reçoivent une attention particulière :  

-   **Point de distribution d’extraction** : variation d’un point de distribution où le point de distribution obtient le contenu à partir d’un autre point de distribution (point de distribution source). Ce processus est similaire à la façon dont les clients téléchargent le contenu à partir de points de distribution. Les points de distribution d’extraction peuvent vous permettre d’éviter les goulots d’étranglement de bande passante réseau qui surviennent quand le serveur de site doit distribuer directement le contenu à chaque point de distribution. [Utilisez un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Point de distribution cloud** : variante d’un point de distribution, installée dans Microsoft Azure. [Découvrez comment utiliser un point de distribution cloud](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


Les points de distribution standard prennent en charge diverses configurations et fonctionnalités :  

- Utilisez des contrôles tels que des **planifications** ou une **limitation de bande passante** pour contrôler ce transfert.  
- Utilisez d’autres options, dont le **contenu préparé** et les **points de distribution d’extraction** pour réduire et contrôler la consommation réseau. 
- **BranchCache**, le **cache d’homologue** et l’**optimisation de la distribution** sont des technologies pair à pair permettant de réduire la bande passante réseau utilisée quand vous déployez du contenu.  
- Il existe différentes configurations pour les déploiements de système d’exploitation, comme **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** et la **[multidiffusion](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**.
- Options pour les **appareils mobiles**   
  
  
Les points de distribution d’extraction et cloud prennent en charge un grand nombre de ces configurations, mais présentent des limitations spécifiques à chaque variante de point de distribution.  



## <a name="distribution-point-groups"></a>Groupes de points de distribution  
 Les groupes de points de distribution sont des regroupements logiques de points de distribution qui peuvent simplifier la distribution de contenu.  

 Pour plus d’informations, voir [Gérer les groupes de points de distribution](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).



## <a name="distribution-point-priority"></a>Priorité des points de distribution  
 La valeur de priorité d’un point de distribution est basée sur le temps nécessaire au transfert des déploiements précédents vers ce point de distribution.  

-   Cette valeur s’ajuste automatiquement. Elle est définie sur chaque point de distribution pour aider Configuration Manager à transférer plus rapidement du contenu vers un plus grand nombre de points de distribution.  

-   Quand vous distribuez du contenu simultanément à plusieurs points de distribution, ou à un groupe de points de distribution, le site envoie d’abord le contenu au serveur avec la priorité la plus haute. Il envoie ensuite ce même contenu à un point de distribution avec une priorité plus faible.  

-   La priorité d’un point de distribution ne remplace pas la priorité de distribution pour les packages. La priorité des packages reste le facteur décisif du moment où le site envoie un contenu différent.  

Par exemple, vous disposez d’un package ayant une priorité de package élevée. Vous le distribuez à un serveur ayant une priorité de point de distribution faible. Ce package à priorité élevée est toujours transféré avant un package ayant une priorité plus faible. La priorité des packages s’applique même si le site distribue des packages de priorité plus faible sur des serveurs ayant des priorités de point de distribution plus élevées.

La priorité élevée du package permet à Configuration Manager de distribuer ce contenu à des points de distribution avant d’envoyer les packages ayant une priorité inférieure.  

> [!NOTE]  
>  Les points de distribution d’extraction utilisent également un concept de priorité pour ordonner la séquence de leur points de distribution source.  
>   
>  -   La priorité des points de distribution pour les transferts de contenu vers le serveur est différente de la priorité qu’utilisent les points de distribution d’extraction. Les points de distribution d’extraction utilisent leur priorité quand ils recherchent du contenu à partir d’un point de distribution source.  
>  -   Pour plus d’informations, consultez [Utiliser un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Secours  
 Plusieurs choses ont changé avec Current Branch de Configuration Manager dans la manière dont les clients recherchent un point de distribution qui a du contenu, notamment les scénarios de secours. 

Les clients qui ne trouvent pas de contenu à partir d’un point de distribution associé à leur groupe de limites actuel utilisent des emplacements sources de contenu associés à des groupes de limites voisins. Pour faire office de groupe de secours, un groupe de limites voisin doit avoir une relation définie avec le groupe de limites actuel du client. Cette relation inclut une durée configurée qui doit s’écouler avant qu’un client qui ne trouve pas de contenu localement inclut dans sa recherche des sources de contenu issues du groupe de limites voisin.

Les concepts de points de distribution préférés ne sont plus utilisés, et les paramètres d’**autorisation des emplacements sources de secours pour le contenu** ne sont plus disponibles ou appliqués.

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>Bande passante du réseau  
 Pour mieux gérer la largeur de la bande passante réseau utilisée quand vous distribuez du contenu, vous pouvez utiliser les options suivantes :  

-   **Contenu préparé** : transfert de contenu vers un point de distribution sans distribuer le contenu sur le réseau.  

-   **Planification et limitation** : configurations qui vous aident à contrôler quand et comment le contenu est distribué aux points de distribution.  

Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Vitesse de la connexion réseau vers la source de contenu  
 Plusieurs choses ont changé avec Current Branch de Configuration Manager dans la manière dont les clients recherchent un point de distribution qui a du contenu. Ces changements incluent la vitesse du réseau pour accéder à une source de contenu. 

Les vitesses de connexion réseau qui définissent un point de distribution comme **Rapide** ou **Lent** ne sont plus utilisées. Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon.

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>Distribution de contenu à la demande  
 La distribution de contenu à la demande est une option pour les déploiements d’applications et de packages individuels. Cette option permet la distribution de contenu à la demande vers des serveurs préférés.  

-   Pour activer ce paramètre pour un déploiement, activez **Distribuer le contenu pour ce package vers les points de distribution préférés**.  

-   Quand cette option est activée pour un déploiement, si un client tente de demander du contenu qui n’est disponible sur aucun de ses points de distribution préférés, Configuration Manager distribue automatiquement ce contenu aux points de distribution préférés du client.  

-   Même si cette option force Configuration Manager à distribuer automatiquement le contenu aux points de distribution préférés de ce client, le client peut obtenir ce contenu auprès d’autres points de distribution avant que ses points de distribution préférés reçoivent le déploiement. Quand ce comportement se produit, le contenu est alors disponible sur ce point de distribution pour le prochain client qui cherche ce déploiement.  

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>Package Transfer Manager  
 Package Transfer Manager est le composant de serveur de site qui transfère du contenu vers des points de distribution situés sur d’autres ordinateurs.  

 Pour plus d’informations, reportez-vous à [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>Contenu préparé  
 La préparation du contenu est un processus de transfert de contenu vers un point de distribution sans distribuer le contenu sur le réseau.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
