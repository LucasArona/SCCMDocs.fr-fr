---
title: Principes de base de la gestion de contenu
titleSuffix: Configuration Manager
description: Utilisez les outils et les options de Configuration Manager pour gérer le contenu que vous déployez.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e4585d21b06bbfaa659fe09693af8cff109a1b6
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676812"
---
# <a name="fundamental-concepts-for-content-management-in-configuration-manager"></a>Principes de base de la gestion de contenu dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager prend en charge un puissant système d’outils et d’options pour gérer les contenus logiciels. Les déploiements de logiciels, comme les applications, les packages, les mises à jour logicielles et les déploiements de système d’exploitation, nécessitent tous des contenus. Configuration Manager stocke le contenu à la fois sur les serveurs de site et sur les points de distribution. Le transfert de ce contenu d’un emplacement à un autre nécessite une large bande passante réseau. Pour planifier et utiliser efficacement l’infrastructure de gestion de contenu, il est nécessaire de bien comprendre les options et les configurations disponibles. Déterminez ensuite comment les utiliser au mieux en fonction de votre environnement réseau et de vos besoins en matière de déploiement de contenu.  

> [!TIP]    
> Pour obtenir plus d’informations sur le processus de distribution de contenu, ainsi que trouver de l’aide sur le diagnostic et la résolution des problèmes généraux relatifs à la distribution de contenu, consultez [Compréhension et résolution des problèmes de distribution de contenu dans Microsoft Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Les rubriques suivantes exposent des concepts clés de la gestion de contenu. Si un concept doit être complété par des informations supplémentaires ou complexes, les liens d’accès à ces informations sont indiqués.



## <a name="accounts-used-for-content-management"></a>Comptes utilisés pour la gestion de contenu  
 Les comptes suivants peuvent être utilisés pour la gestion de contenu :  

#### <a name="network-access-account"></a>Compte d'accès réseau
Utilisé par les clients pour se connecter à un point de distribution et accéder au contenu. Par défaut, le compte d’ordinateur est utilisé en premier.  

Ce compte est également utilisé par les points de distribution d’extraction pour télécharger du contenu à partir d’un point de distribution source dans une forêt distante.  

Depuis la version 1806, certains scénarios ne nécessitent plus l’utilisation d’un compte d’accès réseau. Vous pouvez autoriser le site à utiliser le protocole HTTP amélioré avec l’authentification Azure Active Directory.<!--1358228--> 

Pour plus d’informations, consultez [Compte d’accès réseau](/sccm/core/plan-design/hierarchy/accounts#network-access-account).

#### <a name="package-access-account"></a>Compte d'accès au package
Par défaut, Configuration Manager permet aux utilisateurs et aux administrateurs des comptes d’accès génériques d’accéder au contenu sur un point de distribution. Toutefois, vous pouvez configurer des autorisations supplémentaires pour limiter l’accès.   

Pour plus d’informations, consultez [Compte d’accès au package](/sccm/core/plan-design/hierarchy/accounts#package-access-account).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitation et planification de la bande passante  
 La limitation et la planification sont des options qui vous aident à contrôler la distribution du contenu d’un serveur de site vers des points de distribution. Ces fonctionnalités sont similaires aux contrôles de bande passante pour la réplication de site à site basée sur des fichiers, sans leur être directement liés.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Réplication différentielle binaire  
 La réplication différentielle binaire est parfois appelée « réplication delta ». Elle est utilisée pour distribuer des mises à jour à un contenu que vous avez précédemment déployé sur d’autres sites ou sur des points de distribution distants. Pour permettre à la réplication différentielle binaire de réduire la bande passante utilisée, installez la fonctionnalité **Compression différentielle à distance** sur les points de distribution. Pour plus d’informations, consultez [Prérequis des points de distribution](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012dppreq).

 Cette fonctionnalité réduit la bande passante réseau utilisée lors de l’envoi des mises à jour du contenu distribué. Elle renvoie uniquement le contenu nouveau ou modifié au lieu d’envoyer l’ensemble complet des fichiers sources de contenu chaque fois qu’un changement est apporté à ces fichiers.  

 Quand vous utilisez la réplication différentielle binaire, Configuration Manager identifie les changements apportés aux fichiers sources pour chaque jeu de contenus que vous avez précédemment distribué.  

-   Quand des fichiers du contenu source changent, le site crée une nouvelle version incrémentielle du contenu. Il ne réplique ensuite que les fichiers modifiés sur les sites de destination et les points de destination. Un fichier est considéré comme modifié si vous l’avez renommé ou déplacé, ou si vous avez modifié son contenu. Par exemple, si vous remplacez un seul fichier de pilote pour un package de pilotes que vous avez précédemment distribué vers plusieurs sites, seul le fichier du pilote modifié est répliqué.  

-   Configuration Manager prend en charge jusqu’à cinq versions incrémentielles d’un jeu de contenus avant de renvoyer le jeu de contenus entier. Après la cinquième mise à jour, la modification suivante du jeu de contenus entraîne la création, par le site, d’une nouvelle version du jeu de contenus. Configuration Manager distribue ensuite la nouvelle version du jeu de contenus pour remplacer le jeu précédent et toutes ses versions incrémentielles. Après la distribution du nouveau jeu de contenus, les modifications incrémentielles ultérieures apportées aux fichiers sources sont de nouveau répliquées en utilisant la réplication différentielle binaire.  

La réplication différentielle binaire est prise en charge entre chaque site parent et enfant dans une hiérarchie. Elle est prise en charge dans un site entre le serveur de site et ses points de distribution normaux. Toutefois, les points de distribution d’extraction et les points de distribution cloud ne prennent pas en charge la réplication différentielle binaire pour le transfert de contenu. Les points de distribution d’extraction prennent en charge les deltas de niveau fichier et le transfert de nouveaux fichiers, mais pas les blocs au sein d’un fichier.

Les applications utilisent toujours la réplication différentielle binaire. La réplication différentielle binaire est facultative pour les packages et n’est pas activée par défaut. Pour utiliser la réplication différentielle binaire pour les packages, activez cette fonctionnalité pour chaque package. Sélectionnez l’option **Activer la réplication différentielle binaire** quand vous créez ou modifiez un package.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) est une technologie Windows. Les clients prenant en charge BranchCache et ayant téléchargé un déploiement que vous configurez pour BranchCache font alors office de source de contenu pour d’autres clients BranchCache.  

 Par exemple, vous disposez d’un point de distribution qui exécute Windows Server 2012 ou une version ultérieure et qui est configuré comme serveur BranchCache. Quand le premier client prenant en charge BranchCache demande du contenu à partir de ce serveur, le client télécharge ce contenu et le met en cache.  

- Ce client met ensuite le contenu à la disposition d’autres clients BranchCache du même sous-réseau qui mettent également en cache le contenu.  
- Les autres clients du même sous-réseau n’ont pas à télécharger le contenu à partir du point de distribution.  
- Le contenu est distribué sur plusieurs clients, en vue de transferts futurs.  

Pour plus d’informations, consultez [Prise en charge de Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache).



## <a name="delivery-optimization"></a>Optimisation de la distribution
<!-- 1324696 -->
Les groupes de limites Configuration Manager permettent de définir et de réguler la distribution de contenu sur le réseau de l’entreprise et dans les agences. [L’Optimisation de la distribution de Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) est une technologie cloud pair à pair de partage de contenu entre appareils Windows 10. À compter de la version 1802, configurez-la de façon à ce qu’elle utilise vos groupes de limites pour partager du contenu entre homologues. Les paramètres client appliquent l’identificateur de groupe de limites comme identificateur du groupe Optimisation de la distribution sur le client. Lorsque le client communique avec le service de cloud d’Optimisation de la distribution, il utilise cet identificateur pour localiser les pairs possédant le contenu souhaité. Pour plus d’informations, consultez les paramètres client de l’[optimisation de la distribution](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).

L’optimisation de la distribution est la technologie recommandée pour [optimiser la distribution de la mise à jour Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery) des fichiers d’installation rapide pour les mises à jour de qualité de Windows 10.



## <a name="windows-ledbat"></a>Windows LEDBAT
<!--1358112-->
La fonctionnalité LEDBAT (Low Extra Delay Background Transport) de Windows est une fonctionnalité de contrôle de la congestion réseau de Windows Server qui permet de gérer les transferts réseau d’arrière-plan. Pour les points de distribution qui s’exécutent sur des versions prises en charge de Windows Server, activez une option permettant d’ajuster le trafic réseau. Les clients utilisent alors la bande passante réseau seulement quand elle est disponible. 

Pour plus d’informations sur la fonctionnalité LEDBAT de Windows, consultez le billet de blog [New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/).

Pour plus d’informations sur l’utilisation de Windows LEDBAT avec des points de distribution Configuration Manager, consultez les informations sur le paramètre **Ajuster la vitesse de téléchargement pour utiliser la bande passante réseau inutilisée (Windows LEDBAT)** quand vous [configurez les paramètres généraux d’un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-general).



## <a name="peer-cache"></a>Cache d’homologue
Le cache d’homologue client vous permet de gérer le déploiement de contenu sur les clients distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.

Déployez d’abord les paramètres clients pour activer le cache de pair sur un regroupement. Les membres de ce regroupement se comportent ensuite comme une source de contenu de pair pour les autres clients du même groupe de limites.

À compter de la version 1806, les sources de cache de pair client peuvent diviser le contenu en plusieurs parties. Ces parties diminuent le transfert de réseau afin de réduire l’utilisation du réseau WAN. Le point de gestion fournit un suivi plus détaillé des parties du contenu. Il essaie de supprimer plusieurs téléchargements du même contenu par groupe de limites.<!--1357346-->

Pour plus d’informations, consultez [Cache d’homologue pour les clients Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Mise en cache d’homologue Windows PE
Quand vous déployez un nouveau système d’exploitation avec Configuration Manager, les ordinateurs qui exécutent la séquence de tâches peuvent utiliser la mise en cache d’homologue Windows PE. Ils téléchargent le contenu à partir d’une source de mise en cache d’homologue au lieu de le télécharger à partir d’un point de distribution. Ce comportement permet de réduire le trafic WAN dans les scénarios pour des filiales où il n’existe pas de point de distribution local.

Pour plus d’informations, consultez [Mise en cache d’homologue Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).



## <a name="client-locations"></a>Emplacements des clients  
 Les clients accèdent au contenu à partir des emplacements suivants :  

-   **Intranet** (local) :  

    -   Les points de distribution peuvent utiliser HTTP ou HTTPS.  

    -   Utilisez un point de distribution cloud de secours seulement quand des points de distribution locaux ne sont pas disponibles.  

-   **Internet** :  

    -   Nécessite des points de distribution accessibles via Internet pour accepter HTTPS.  

    -   Peut utiliser un point de distribution cloud ou une passerelle de gestion cloud.  
    
        *   À compter de la version 1806, une passerelle de gestion cloud peut également distribuer du contenu aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure. Pour plus d’informations, consultez [Modifier une passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway).

-   **Groupe de travail**:  

    -   Exige des points de distribution qu’ils acceptent le protocole HTTPS.  

    -   Peut utiliser un point de distribution cloud ou une passerelle de gestion cloud.  



## <a name="content-source-priority"></a>Priorités des sources de contenu

Quand un client a besoin de contenu, il envoie au point de gestion une demande quant à l’emplacement du contenu. Le point de gestion retourne une liste d’emplacements sources qui sont valides pour le contenu demandé. Cette liste varie en fonction du scénario spécifique, des technologies utilisées, de conception des sites, des groupes de limites et des paramètres de déploiement. La liste suivante contient tous les emplacements sources de contenu possibles qu’un client peut utiliser, dans l’ordre de priorité où il les utilise :  

1. Le point de distribution sur le même ordinateur que le client
2. Une source de pair dans le même sous-réseau du réseau
3. Un point de distribution dans le même sous-réseau du réseau
4. Une source de pair dans le même groupe de limites
5. Un point de distribution dans le groupe de limites actif
6. Un point de distribution dans un groupe de limites voisin configuré pour le secours
9. Un point de distribution dans le groupe de limites du site par défaut 
10. Le service cloud Windows Update
11. Un point de distribution accessible sur Internet
12. Un point de distribution cloud dans Azure



## <a name="content-library"></a>Bibliothèque de contenu  
 La bibliothèque de contenu est un stockage SIS (Single-Instance-Store) de contenu dans Configuration Manager. Cette bibliothèque permet de réduire la taille globale du contenu que vous distribuez.  

- En savoir plus sur la [bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library).
- Utilisez l’[outil de nettoyage de la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) pour supprimer le contenu qui n’est plus associé à une application.  



## <a name="distribution-points"></a>Points de distribution  
 Configuration Manager utilise des points de distribution pour stocker les fichiers nécessaires à l’exécution de logiciels sur les ordinateurs clients. Les clients doivent avoir accès à au moins un point de distribution à partir duquel ils peuvent télécharger les fichiers du contenu que vous déployez.  

 Le point de distribution (non spécifique) de base est communément appelé point de distribution standard. Il existe deux variantes du point de distribution standard qui reçoivent une attention particulière :  

-   **Point de distribution d’extraction** : variation d’un point de distribution où le point de distribution obtient le contenu à partir d’un autre point de distribution (point de distribution source). Ce processus est similaire à la façon dont les clients téléchargent le contenu à partir de points de distribution. Les points de distribution d’extraction peuvent vous permettre d’éviter les goulots d’étranglement de bande passante réseau qui surviennent quand le serveur de site doit distribuer directement le contenu à chaque point de distribution. [Utilisez un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Point de distribution cloud** : variation d’un point de distribution qui est installé sur Microsoft Azure. [Découvrez comment utiliser un point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point).  


Les points de distribution standard prennent en charge diverses configurations et fonctionnalités :  

- Utilisez des contrôles tels que des **planifications** ou une **limitation de bande passante** pour contrôler ce transfert.  

- Utilisez d’autres options, dont le **contenu préparé** et les **points de distribution d’extraction** pour réduire et contrôler la consommation réseau.  

- **BranchCache**, le **cache d’homologue** et l’**optimisation de la distribution** sont des technologies pair à pair permettant de réduire la bande passante réseau utilisée quand vous déployez du contenu.  

- Il existe différentes configurations pour les déploiements de système d’exploitation, comme **[PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)** et la **[multidiffusion](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_DPMulticast)** .  

- Options pour les **appareils mobiles**   
  
Les points de distribution d’extraction et cloud prennent en charge un grand nombre de ces configurations, mais ils présentent des limitations spécifiques à chaque variante de point de distribution.  



## <a name="distribution-point-groups"></a>Groupes de points de distribution  
 Les groupes de points de distribution sont des regroupements logiques de points de distribution qui peuvent simplifier la distribution de contenu.  

 Pour plus d’informations, voir [Gérer les groupes de points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_manage).



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

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="network-bandwidth"></a>Bande passante du réseau  
 Pour mieux gérer la largeur de la bande passante réseau utilisée quand vous distribuez du contenu, vous pouvez utiliser les options suivantes :  

-   **Contenu préparé** : transfert de contenu vers un point de distribution sans distribuer le contenu sur le réseau.  

-   **Planification et limitation** : configurations qui vous aident à contrôler quand et comment le contenu est distribué aux points de distribution.  

Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Vitesse de la connexion réseau vers la source de contenu  
 Plusieurs choses ont changé avec Current Branch de Configuration Manager dans la manière dont les clients recherchent un point de distribution qui a du contenu. Ces changements incluent la vitesse du réseau pour accéder à une source de contenu. 

Les vitesses de connexion réseau qui définissent un point de distribution comme **Rapide** ou **Lent** ne sont plus utilisées. Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon.

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="on-demand-content-distribution"></a>Distribution de contenu à la demande  
 La distribution de contenu à la demande est une option pour les déploiements d’applications et de packages individuels. Cette option permet la distribution de contenu à la demande vers des serveurs préférés.  

-   Pour activer ce paramètre pour un déploiement, activez : **Distribuer le contenu pour ce package vers les points de distribution préférés**.  

-   Quand vous activez cette option pour un déploiement et si un client demande du contenu qui n’est disponible sur aucun de ses points de distribution préférés, Configuration Manager distribue automatiquement ce contenu aux points de distribution préférés du client.  

-   Même si cette option force Configuration Manager à distribuer automatiquement le contenu aux points de distribution préférés de ce client, le client peut obtenir ce contenu auprès d’autres points de distribution avant que ses points de distribution préférés reçoivent le déploiement. Quand ce comportement se produit, le contenu est alors disponible sur ce point de distribution pour le prochain client qui cherche ce déploiement.  

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="package-transfer-manager"></a>Package Transfer Manager  
 Package Transfer Manager est le composant de serveur de site qui transfère du contenu vers des points de distribution situés sur d’autres ordinateurs.  

 Pour plus d’informations, reportez-vous à [Package Transfer Manager](/sccm/core/plan-design/hierarchy/package-transfer-manager).  



## <a name="prestage-content"></a>Contenu préparé  
 La préparation du contenu est un processus de transfert de contenu vers un point de distribution sans distribuer le contenu sur le réseau.  

 Pour plus d’informations, consultez [Gérer la bande passante réseau](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).
