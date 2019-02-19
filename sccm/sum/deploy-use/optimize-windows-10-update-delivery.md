---
title: Optimiser la distribution de Windows Update pour Windows 10
titleSuffix: Configuration Manager
description: Découvrez comment utiliser Configuration Manager pour gérer le contenu des mises à jour de Windows 10.
ms.date: 06/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: b670cfaf-96a4-4fcb-9caa-0f2e8c2c6198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92ac9cbfd8b4c68a818a3988c0ce1f3ec26a2215
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139168"
---
# <a name="optimize-windows-10-update-delivery-with-configuration-manager"></a>Optimiser la distribution de Windows Update pour Windows 10 avec Configuration Manager

*S’applique à : System Center Configuration Manager (current branch)*

Pour la plupart des clients, suivre le rythme des mises à jour mensuelles de Windows 10 implique en premier lieu une bonne stratégie de distribution de contenu avec Configuration Manager. L’ampleur de ces mises à jour qualité peut constituer une source de préoccupation pour les grandes organisations. Il existe des technologies conçues pour réduire la bande passante et la charge réseau afin d’optimiser la distribution des mises à jour. Cet article décrit ces technologies, les compare et donne des recommandations pour vous aider à choisir.  
 
Windows 10 propose plusieurs types de mises à jour. Pour plus d'informations, voir [Types de mises à jour dans Windows Update pour Entreprise](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb#update-types). Cet article se concentre sur les mises à jour *qualité* de Windows 10 avec Configuration Manager. 


## <a name="express-update-delivery"></a>Distribution de mises à jour rapide

Le téléchargement des mises à jour qualité de Windows 10 peut représenter de gros volumes. Dans un souci de cohérence et de simplicité, chaque package contient tous les correctifs précédemment publiés. Microsoft a pu réduire la taille du contenu des mises à jour Windows 10 téléchargé par les clients avec une fonctionnalité d’installation rapide. Cette fonctionnalité est utilisée aujourd'hui par des millions d’appareils qui extraient directement les mises à jour à partir du service Windows Update, ce qui réduit considérablement la taille de téléchargement. Cet avantage est également accessible à tous ceux dont les clients n’effectuent pas directement le téléchargement auprès du service Windows Update. 

Configuration Manager a intégré la prise en charge des [fichiers d’installation rapide](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates) des mises à jour qualité de Windows 10 dans la version 1702. Toutefois, pour une expérience optimale, il est recommandé d’utiliser la version 1802 ou une version ultérieure de Configuration Manager. Pour profiter des meilleures performances possibles en vitesse de téléchargement, il est également conseillé d’utiliser Windows 10 version 1703 (ou ultérieure). 

> [!NOTE]  
> Le contenu de la version rapide est considérablement plus volumineux que la version qui comprend la totalité des fichiers. Un fichier d’installation rapide comporte toutes les variations possibles pour chaque fichier qu'il est destiné à mettre à jour. Par conséquent, la quantité d’espace disque requise augmente pour les mises à jour de la source du package et sur les points de distribution lorsque la prise en charge rapide est activée dans Configuration Manager. Même si l’espace disque requis sur les points de distribution est supérieur, la taille du contenu téléchargé par les clients à partir de ces points de distribution diminue. Les clients téléchargent seulement les bits dont ils ont besoin (deltas), non la totalité de la mise à jour.



## <a name="peer-to-peer-content-distribution"></a>Distribution de contenu pair à pair

Même si les clients téléchargent seulement les portions de contenu dont ils ont besoin, il est possible d’accélérer les mises à jour de Windows dans l’environnement grâce à la distribution de contenu pair à pair. Le fait de tirer parti des pairs comme source de téléchargement des mises à jour qualité peut être utile pour les environnements dans lesquels les points de distribution locaux ne sont pas présents dans des bureaux distants. Ce comportement évite aux clients d’avoir à télécharger du contenu à partir d’un point de distribution distant sur une liaison WAN lente. Les pairs peuvent également être utiles lorsque les clients utilisent le service Windows Update en secours. Un pair suffit pour télécharger le contenu des mises à jour à partir du cloud avant de le mettre à disposition d’autres appareils.

Configuration Manager prend en charge de nombreuses technologies pair à pair, notamment les suivantes :
- Optimisation de la distribution de Windows
- Cache entre pairs Configuration Manager
- Windows BranchCache  

Les sections suivantes apportent des informations complémentaires sur ces technologies.


### <a name="windows-delivery-optimization"></a>Optimisation de la distribution de Windows

[L’Optimisation de la distribution](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) est la principale technologie de téléchargement et la principale méthode de distribution pair à pair intégrée à Windows 10. Les clients Windows 10 peuvent récupérer du contenu à partir d’autres appareils qui se trouvent sur leur réseau local et téléchargent les mêmes mises à jour. Avec les [options Windows disponibles pour l’Optimisation de la distribution](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#delivery-optimization-options), vous pouvez configurer les clients dans des groupes. Ce regroupement permet à votre organisation d’identifier les appareils qui sont potentiellement les meilleurs candidats pour répondre aux demandes pair à pair. L’Optimisation de la distribution réduit considérablement la bande passante globale servant à tenir les appareils à jour tout en accélérant le téléchargement.

> [!NOTE]  
> L’Optimisation de la distribution est une solution cloud gérée. L’accès à Internet est requis pour utiliser les fonctionnalités pair à pair de ce service.  

Pour optimiser les résultats, vous devrez peut-être définir le [mode de téléchargement](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#download-mode) de l’Optimisation de la distribution sur **Groupe (2)** et définir des *ID de groupe*. En mode groupé, le peering peut traverser les sous-réseaux internes entre les appareils qui appartiennent au même groupe, y compris dans des bureaux distants. Utilisez [l’option ID de groupe](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#select-the-source-of-group-ids) pour créer votre propre groupe personnalisé, indépendamment des domaines et des sites AD DS. Le mode de téléchargement groupé est l’option recommandée pour la plupart des organisations qui recherchent la meilleure optimisation de la bande passante avec l’Optimisation de la distribution.

Il est difficile de configurer manuellement ces ID de groupe en cas d’itinérance des clients entre différents réseaux. La version 1802 de Configuration Manager a introduit une nouvelle fonctionnalité qui simplifie la gestion de ce processus en [intégrant les groupes de limites avec l’Optimisation de la distribution](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization). Lorsqu’un client est activé, il communique avec son point de gestion pour recevoir des stratégies et fournit des informations sur son groupe de limites et son réseau. Configuration Manager crée un ID unique pour chaque groupe de limites. Le site utilise les informations d’emplacement du client pour configurer automatiquement son ID de groupe d’Optimisation de la distribution avec l’ID de limites de Configuration Manager. En cas d’itinérance du client vers un autre groupe de limites, il communique avec son point de gestion et est automatiquement reconfiguré avec un nouvel ID de groupe de limites. Grâce à cette intégration, l’Optimisation de la distribution peut utiliser les informations sur le groupe de limites de Configuration Manager pour trouver un pair permettant de télécharger les mises à jour.


### <a name="configuration-manager-peer-cache"></a>Cache entre pairs Configuration Manager

Le [cache entre pairs](/sccm/core/plan-design/hierarchy/client-peer-cache) est une fonctionnalité de Configuration Manager qui permet aux clients de partager directement du contenu avec d’autres clients à partir de leur cache Configuration Manager local. Il ne remplace pas l’utilisation d’autres solutions de mise en cache partagé entre systèmes homologues, comme Windows BranchCache. Il fonctionne conjointement avec elles, pour vous offrir plus d’options d’extension des solutions traditionnelles de déploiement de contenu, comme les points de distribution. Le cache entre pairs ne repose pas sur BranchCache. Il fonctionne même sans activer ou utiliser BranchCache.

> [!NOTE]  
> Les clients ne peuvent télécharger du contenu qu’à partir de clients du cache entre systèmes homologues qui se trouvent dans leur groupe de limites actuel.  


### <a name="windows-branchcache"></a>Windows BranchCache
[BranchCache](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) est une technologie d’optimisation de la bande passante dans Windows. Chaque client possède un cache et représente une autre source de contenu. Les appareils qui se trouvent sur le même réseau peuvent demander ce contenu. [Configuration Manager peut utiliser BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache) pour autoriser des homologues à récupérer du contenu les uns auprès des autres sans avoir à contacter systématiquement un point de distribution. Avec BranchCache, les fichiers sont mis en cache sur chacun des clients ; les autres clients peuvent les récupérer si nécessaire. Cette approche distribue le cache, à la différence d’un point de récupération unique. Ce comportement permet d’économiser beaucoup de bande passante, tout en réduisant le délai de réception du contenu demandé pour les clients. 



## <a name="selecting-the-right-peer-caching-technology"></a>Sélectionner la bonne technologie de mise en cache partagé entre systèmes homologues

La technologie de mise en cache partagé entre systèmes homologues à privilégier pour les fichiers d’installation rapide dépend de l’environnement et des exigences. Même si Configuration Manager prend en charge toutes les technologies pair à pair ci-dessus, utilisez les plus pertinentes pour votre environnement. Pour la plupart des clients, la mise en cache partagé entre systèmes homologues intégrée à Windows 10 avec Optimisation de la distribution devrait suffire, à condition de pouvoir répondre aux exigences de l’Optimisation de la distribution en matière d’accès à Internet. Si vos clients ne remplissent pas ces critères, vous pouvez vous tourner vers la fonctionnalité de cache entre pairs de Configuration Manager. Si vous utilisez actuellement BranchCache avec Configuration Manager et que cette solution répond à tous vos besoins, les fichiers rapides avec BranchCache seront peut-être un bon choix pour vous. 

### <a name="peer-cache-comparison-chart"></a>Tableau comparatif des caches entre pairs


| Fonctionnalité  | Optimisation de la distribution  | Cache d’homologue  | BranchCache  |
|---------|---------|---------|---------|
| Pris en charge sur plusieurs sous-réseaux | Oui | Oui | Non |
| Limitation de bande passante | Oui (native) | Oui (avec BITS) | Oui (avec BITS) |
| Prise en charge du contenu partiel | Oui | Seulement pour Office 365 et les mises à jour rapides | Oui |
| Contrôle de la taille du cache sur le disque | Oui | Oui | Oui |
| Détection d’une source de pairs | Automatique | Manuelle (paramètre de l’agent client) | Automatique |
| Découverte de pairs | Par le biais du service cloud d’Optimisation de la distribution (accès à Internet requis) | Par le biais du point de gestion (en fonction des groupes de limites du client) | Multidiffusion |
| Rapports | Oui (avec Windows Analytics) | Tableau de bord des sources de données du client ConfigMgr | Tableau de bord des sources de données du client ConfigMgr |
| Contrôle de l’utilisation du réseau WAN | Oui (natif, contrôlable par le biais de paramètres de stratégie de groupe) | Groupes de limites | Prise en charge des sous-réseaux uniquement |
| Types de contenus pris en charge | - Mises à jour rapides (avec ConfigMgr)</br> - Mises à jour Windows et de sécurité</br> - Pilotes</br> - Applications du Windows Store</br> - Applications du Windows Store pour Entreprises | Tous les types de contenus de ConfigMgr, y compris les images téléchargées dans [Windows PE](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic) | Tous les types de contenus de ConfigMgr, à l’exception des images |
| Gestion avec ConfigMgr | Partielle (paramètre de l’agent client) | Oui (paramètre de l’agent client) | Oui (paramètre de l’agent client) |



## <a name="conclusion"></a>Conclusion

Microsoft recommande d’optimiser la distribution de mises à jour qualité de Windows 10 à l’aide de Configuration Manager avec des fichiers d’installation rapide et une technologie de mise en cache partagé entre systèmes homologues si nécessaire. Cette approche devrait aider à résoudre les difficultés que peut représenter le téléchargement de contenu volumineux pour installer des mises à jour qualité sur des appareils Windows 10. Il est également conseillé de tenir les appareils Windows 10 à jour en déployant des mises à jour qualité tous les mois. Cette pratique réduit le delta de contenu des mises à jour qualité requises par les appareils chaque mois. La taille des téléchargements à partir de points de distribution ou de sources de pairs s’en trouve ainsi diminuée. 

En raison de la nature des fichiers d’installation rapide, leur contenu est considérablement plus volumineux que celui des fichiers complets. Cette taille a pour conséquence un allongement du temps de téléchargement des mises à jour du service de Windows Update vers le serveur de site Configuration Manager. La quantité d’espace disque nécessaire pour le serveur de site et les points de distribution augmente également. La durée totale nécessaire pour télécharger et distribuer les mises à jour qualité peut être plus longue. Toutefois, les avantages du côté de l’appareil devraient être notables pendant le téléchargement et l’installation des mises à jour qualité par les appareils Windows 10.

Si les compromis côté serveur causés par des mises à jour plus volumineuses gênent l’adoption de la prise en charge rapide, mais que les avantages du côté de l’appareil sont critiques pour votre entreprise et votre environnement, Microsoft vous recommande d’utiliser [Windows Update pour Entreprise](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10) avec Configuration Manager. Windows Update pour Entreprise offre tous les avantages de la version rapide sans obliger à télécharger, stocker et distribuer les fichiers d’installation rapide dans l’ensemble de votre environnement. Les clients téléchargent directement le contenu à partir du service Windows Update ; ainsi, ils peuvent toujours utiliser l’Optimisation de la distribution.



## <a name="bkmk_faq"></a> Foire aux questions

#### <a name="how-do-windows-express-downloads-work-with-configuration-manager"></a>Comment les téléchargements rapides Windows fonctionnent-ils avec Configuration Manager ?

Tout d’abord, l’agent de mise à jour de Windows (WUA) demande du contenu rapide. S’il ne parvient pas installer la mise à jour rapide, il peut revenir à la mise à jour avec fichier complet.  

1. Le client Configuration Manager demande à l’agent WUA de télécharger le contenu de la mise à jour. Lorsque l’agent WUA lance un téléchargement rapide, il commence par télécharger un stub (par exemple, `Windows10.0-KB1234567-<platform>-express.cab`), qui fait partie du package rapide.  

2. L’agent WUA transmet ce stub au programme d’installation des mises à jour de Windows, les services à base de composants (CBS). Ces services utilisent le stub pour effectuer un inventaire local, comparant les deltas du fichier sur l’appareil avec les éléments nécessaires pour accéder à la dernière version proposée du fichier.  

3. Les services CBS demandent ensuite à l’agent WUA de télécharger les plages requises à partir d’un ou plusieurs fichiers .psf rapides.  

4. L’Optimisation de la distribution se coordonne avec Configuration Manager et télécharge les plages à partir d’un point de distribution local ou de pairs s’il y en a. Si l’Optimisation de la distribution est désactivée, le Service de transfert intelligent en arrière-plan (BITS) est utilisé de la même manière, avec Configuration Manager qui coordonne les sources du cache entre pairs. L’Optimisation de la distribution ou le service BITS transmet les plages à l’agent WUA, qui les met à la disposition des services CBS, chargés de les appliquer et de les installer.  


#### <a name="why-are-the-express-files-psf-so-large-when-stored-on-configuration-manager-peer-sources-in-the-ccmcache-folder"></a>Pourquoi les fichiers rapides (.psf) sont-ils si volumineux lorsqu’ils sont stockés sur des sources de pairs de Configuration Manager dans le dossier ccmcache ?

Les fichiers rapides (.psf) sont des fichiers partiellement alloués. Pour déterminer l’espace réellement utilisé sur le disque par le fichier, examinez la propriété **Taille sur le disque** du fichier. Cette propriété devrait être considérablement plus petite que la valeur Taille.  


#### <a name="does-configuration-manager-support-express-installation-files-with-windows-10-feature-updates"></a>Configuration Manager prend-il en charge les fichiers d’installation rapide avec les mises à jour des fonctionnalités de Windows 10 ?

Non, Configuration Manager ne prend en charge à l’heure actuelle les fichiers d’installation rapide qu’avec les mises à jour qualité de Windows 10.  


#### <a name="how-much-disk-space-is-needed-per-quality-update-on-the-site-server-and-distribution-points"></a>Quelle est la quantité d’espace disque nécessaire par mise à jour qualité sur le serveur de site et les points de distribution ?

Cela dépend. Pour chaque mise à jour qualité, la version avec fichier complet et la version rapide de la mise à jour sont toutes deux stockées sur les serveurs. Les mises à jour qualité de Windows 10 étant cumulatives, la taille de ces fichiers augmente chaque mois. Prévoyez un minimum de 5 Go par mise à jour et par langue. 


#### <a name="do-configuration-manager-clients-still-benefit-from-express-installation-files-when-falling-back-to-the-windows-update-service"></a>Les clients Configuration Manager bénéficient-ils toujours des fichiers d’installation rapide lorsqu’ils reviennent au service Windows Update ?

Oui. Si vous utilisez l’option de déploiement de mise à jour logicielle suivante, les clients utiliseront toujours les mises à jour rapides et l’Optimisation de la distribution lorsqu’ils reviendront au service cloud :  

**Si les mises à jour logicielles ne sont pas disponibles sur le point de distribution des groupes actifs, voisins ou de site, téléchargez le contenu à partir de Microsoft Update.**


#### <a name="why-is-express-file-content-not-downloaded-for-existing-updates-after-i-enable-express-file-support"></a>Pourquoi le contenu des fichiers rapides n’est-il pas téléchargé pour les mises à jour existantes une fois la prise en charge des fichiers rapides activée ? 

Les modifications ne sont effectives que pour les nouvelles mises à jour synchronisées et déployées une fois la prise en charge activée.


#### <a name="is-there-any-way-to-see-how-much-content-is-downloaded-from-peers-using-delivery-optimization"></a>Existe-t-il un moyen de connaître la quantité de contenu téléchargé auprès de pairs à l’aide de l’Optimisation de la distribution ?
La version 1703 de Windows 10 (et les versions ultérieures) comporte deux nouvelles cmdlets PowerShell, **Get-DeliveryOptimizationPerfSnap** et **Get-DeliveryOptimizationStatus**. Elles donnent plus d’informations sur l’Optimisation de la distribution et l’utilisation du cache. Pour plus d’informations, voir [Cmdlets Windows PowerShell permettant d’analyser l’utilisation](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#windows-powershell-cmdlets-for-analyzing-usage).


#### <a name="how-do-clients-communicate-with-delivery-optimization-over-the-network"></a>Comment les clients communiquent-ils avec l’Optimisation de la distribution sur le réseau ?
Pour plus d’informations sur les ports de réseau, les exigences en matière de proxy et les noms d’hôtes pour les pare-feu, voir [FAQ sur l’Optimisation de la distribution](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions).

