---
title: Configuration Manager dans Azure
description: Informations sur l’utilisation de Configuration Manager dans un environnement Azure.
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d24257d8-8136-47f4-8e0d-34021356dc37
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4efea7baf7820c4edfb61882b14812336c85518
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67516174"
---
# <a name="configuration-manager-on-azure---frequently-asked-questions"></a>Configuration Manager dans Azure – Forum Aux Questions
*S’applique à : System Center Configuration Manager (Current Branch)*

Les questions et réponses suivantes peuvent vous aider à comprendre quand utiliser et comment configurer Configuration Manager dans Microsoft Azure.

## <a name="general-questions"></a>Questions générales
### <a name="my-company-is-trying-to-move-as-many-physical-servers-as-possible-to-microsoft-azure-can-i-move-configuration-manager-servers-to-azure"></a>Mon entreprise tente de déplacer autant de serveurs physiques que possible vers Microsoft Azure. Puis-je déplacer les serveurs Configuration Manager vers Azure ?
Absolument, ce scénario est pris en charge.  Consultez [Prise en charge des environnements de virtualisation pour System Center Configuration Manager](/sccm/core/plan-design/configs/support-for-virtualization-environments).

### <a name="great-my-environment-requires-multiple-sites-should-all-child-primary-sites-be-in-azure-with-the-central-administration-site-or-on-premises-what-about-secondary-sites"></a>Très bien ! Mon environnement requiert plusieurs sites. Tous les sites principaux enfants doivent-ils être dans Azure avec le site d’administration centrale ou locale ? Qu’en est-il des sites secondaires ?
Les communications de site à site (réplication de base de données et basée sur les fichiers) tirent parti de la proximité de l’hébergement dans Azure. Toutefois, tout le trafic associé aux clients serait distant des serveurs de site et des systèmes de site. Si vous utilisez une connexion réseau rapide et fiable entre Azure et votre intranet avec un plan de données illimité, l’hébergement de toute votre infrastructure dans Azure est une option.

Toutefois, si vous utilisez un plan de données contrôlé et la bande passante disponible ou si le coût est un problème, ou si la connexion réseau entre Azure et votre intranet n’est pas rapide ou peut ne pas être fiable, envisagez de placer des sites spécifiques (et les systèmes de site) localement, puis d’utiliser les contrôles de bande passante intégrés dans Configuration Manager.

### <a name="is-having-configuration-manager-in-azure-a-saas-scenario-software-as-a-service"></a>Le fait d’avoir Configuration Manager dans Azure est-il un scénario SaaS (logiciel en tant que service) ?
Non, il s’agit d’un IaaS (infrastructure en tant que service), car vous hébergez vos serveurs d’infrastructure Configuration Manager sur des machines virtuelles Azure.

### <a name="what-areas-should-i-pay-attention-to-when-considering-a-move-of-my-configuration-manager-infrastructure-to-azure"></a>À quelles zones dois-je faire attention lorsque j’envisage un déplacement de mon infrastructure Configuration Manager vers Azure ?
Excellente question. Voici les zones les plus importantes quand vous prenez cette décision. Chacune est explorée dans une section distincte de cette rubrique :
1.  Mise en réseau
2.  Disponibilité
3.  Performances
4.  Coût
5.  Expérience utilisateur

## <a name="networking"></a>Mise en réseau
### <a name="what-about-networking-requirements-should-i-use-expressroute-or-an-azure-vpn-gateway"></a>Qu’en est-il de la configuration réseau requise ? Dois-je utiliser ExpressRoute ou une passerelle VPN Azure ?
La mise en réseau est une décision très importante. Les vitesses et la latence des réseaux peuvent affecter les fonctionnalités entre le serveur de site et les systèmes de site distants, ainsi que les communications des clients vers les systèmes de site. Nous vous recommandons d’utiliser ExpressRoute. Toutefois, Configuration Manager ne présente aucune limitation pour vous empêcher d’utiliser la passerelle VPN Azure. Vous devez examiner attentivement vos besoins (performances, correctifs, distribution de logiciels, déploiement de système d’exploitation) à partir de cette infrastructure, puis prendre votre décision. Voici quelques points à prendre en compte pour chaque solution :

- **ExpressRoute** (recommandé)
  - Extension naturelle de votre centre de données (peut relier plusieurs centres de données)
  - Connexions privées entre des centres de données Azure et votre infrastructure
  - Ne parvient pas jusqu’à l’Internet public
  - Offre une fiabilité, des vitesses élevées, une latence plus faible, une haute sécurité
  - Offre des vitesses pouvant atteindre 10 Gbits/s et des options de plan de données illimitées
- **Passerelle VPN**
  - Réseaux VPN de site à site/point à site
  - Le trafic parvient jusqu’à l’Internet public
  - Utilise la sécurité du protocole Internet (IPsec) et Internet Key Exchange (IKE)

### <a name="expressroute-has-many-different-options-like-unlimited-vs-metered-different-speed-options-and-premium-add-on-which-should-i-choose"></a>ExpressRoute dispose de nombreuses options différentes telles que différentes options de vitesse, illimitées et contrôlées, ainsi qu’un module complémentaire premium. Laquelle choisir ?
Les options que vous sélectionnez dépendent du scénario que vous mettez en œuvre et du volume de données que vous envisagez de distribuer. Le transfert de données de Configuration Manager peut être contrôlé entre les serveurs de site et les points de distribution, mais la communication de serveur de site à serveur de site ne peut pas être contrôlée.   Lorsque vous utilisez un plan de données contrôlé, le placement de sites spécifiques (et de systèmes de site) localement et l’utilisation de [contrôles de bande passante intégrés à Configuration Manager](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management) permettent de mieux contrôler le coût d’utilisation d’Azure.

### <a name="what-about-installation-requirements-like-active-directory-domains-do-i-still-need-to-join-my-site-servers-to-an-active-directory-domain"></a>Qu’en est-il des exigences d’installation telles que les domaines Active Directory ? Ai-je encore besoin de joindre mes serveurs de site à un domaine Active Directory ?
Oui. Quand vous passez à Azure, les [configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations) restent les mêmes, notamment les exigences d’Active Directory pour l’installation de Configuration Manager.

### <a name="i-understand-the-need-to-join-my-site-servers-to-an-active-directory-domain-but-can-i-use-azure-active-directory"></a>Je comprends le besoin de joindre mes serveurs de site à un domaine Active Directory, mais puis-je utiliser Azure Active Directory ?
Non, Azure Active Directory n’est pas pris en charge à ce stade. Vos serveurs de site doivent cependant être membres d’un [domaine Windows Active Directory](/sccm/core/plan-design/configs/support-for-active-directory-domains).



## <a name="availability"></a>Disponibilité
### <a name="one-of-the-reasons-i-am-moving-infrastructure-to-azure-is-the-promise-of-high-availability-can-i-take-advantage-of-high-availability-options-like-azure-vm-availability-sets-for-vms-that-i-will-use-for-configuration-manager"></a>L’une des raisons pour lesquelles je déplace l’infrastructure vers Azure est la promesse d’une haute disponibilité. Puis-je tirer parti des options de haute disponibilité, telles que les ensembles de disponibilité des machines virtuelles Azure, pour les machines virtuelles que j’utiliserai pour Configuration Manager ?
Oui ! Des ensembles de disponibilité de machines virtuelles Azure peuvent être utilisés pour des rôles de système de site redondants, tels que les points de distribution ou les points de gestion.

Vous pouvez également les utiliser pour les serveurs de site Configuration Manager. Par exemple, les sites d’administration centrale et les sites principaux peuvent tous être dans le même ensemble de disponibilité, ce qui peut vous aider à vous assurer qu’ils ne sont pas redémarrés en même temps.

### <a name="how-can-i-make-my-database-highly-available-can-i-use-azure-sql-database-or-do-i-have-to-use-microsoft-sql-server-in-a-vm"></a>Comment puis-je rendre ma base de données hautement disponible ? Puis-je utiliser Base de données SQL Azure ? Ou dois-je utiliser Microsoft SQL Server sur une machine virtuelle ?
Vous devez utiliser Microsoft SQL Server sur une machine virtuelle. Configuration Manager ne prend pas en charge Azure SQL Server à ce stade. Mais vous pouvez utiliser des fonctionnalités telles que les groupes de disponibilité AlwaysOn pour votre serveur SQL Server. Les [groupes de disponibilité AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) sont recommandés et sont officiellement pris en charge depuis la version 1602 de Configuration Manager.

### <a name="can-i-use-azure-load-balancers-with-site-system-roles-like-management-points--or-software-update-points"></a>Puis-je utiliser des équilibreurs de charge Azure avec des rôles de système de site tels que les points de gestion ou les points de mise à jour logicielle ?
Configuration Manager n’a pas été testé avec les équilibreurs de charge Azure, mais si la fonctionnalité est transparente pour l’application, elle ne doit pas avoir d’effets négatifs sur les opérations normales.


## <a name="performance"></a>Performances
### <a name="what-factors-affect-performance-in-this-scenario"></a>Quels facteurs affectent les performances dans ce scénario ?
[La taille et le type des machines virtuelles Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs), les disques des machines virtuelles Azure (un stockage premium est recommandé, en particulier pour SQL Server), la latence de mise en réseau et la vitesse sont les domaines les plus importants.

### <a name="so-tell-me-more-about-azure-virtual-machines-what-size-vms-should-i-use"></a>Spécifiez donc plus d’informations sur les machines virtuelles Azure ; quelle taille de machines virtuelles dois-je utiliser ?
En règle générale, votre puissance de calcul (UC et mémoire) doit correspondre au [matériel recommandé pour System Center Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware). Toutefois, il existe certaines différences entre le matériel informatique standard et les machines virtuelles Azure, notamment en ce qui concerne les disques que ces machines virtuelles utilisent.  La taille des machines virtuelles que vous utilisez dépend de la taille de votre environnement. Voici quelques recommandations :
- Pour les déploiements en production d’une taille importante, nous recommandons des machines virtuelles Azure de classe « **S** ». Cela tient au fait qu’elles peuvent tirer parti des disques de stockage Premium.  Les machines virtuelles de classe autre que « S » utilisent le stockage d’objets blob et, en général, ne respectent pas les exigences de performances nécessaires pour un environnement de production acceptable.
- Plusieurs disques de stockage Premium doivent être utilisés pour une échelle supérieure et agrégés par bandes dans la console Windows Disk Management pour un nombre maximal d’E/S par seconde.  
- Nous vous recommandons d’utiliser de meilleurs disques premium ou plusieurs disques premium pendant votre déploiement initial de site (comme P30 à la place de P20, et 2xP30 dans un volume agrégé par bandes à la place de 1xP30). Ensuite, si votre site a besoin d’augmenter ultérieurement la taille des machines virtuelles en raison d’une charge supplémentaire, vous pouvez tirer parti de l’UC et de la mémoire supplémentaires qu’une plus grande taille de machine virtuelle fournit. Vous aurez également des disques déjà en place, susceptibles de tirer parti du débit d’E/S par seconde supplémentaire que permet la plus grande taille de machine virtuelle.



Les tableaux suivants répertorient les nombres de disques suggérés initiaux à utiliser sur les sites principaux et d’administration centrale pour des installations de différentes tailles :

**Base de données de site colocalisé** : site d’administration centrale ou site principal avec la base de données de site sur le serveur de site :

| Clients bureau    |Taille de machine virtuelle recommandée|Disques recommandés|
|--------------------|-------------------|-----------------|
|**Jusqu’à 25 000**       |   DS4_V2          |2xP30 (agrégé par bandes)  |
|**de 25 000 à 50 000**      |   DS13_V2         |2xP30 (agrégé par bandes)  |
|**de 50 000 à 100 000**     |   DS14_V2         |3xP30 (agrégé par bandes)  |


**Base de données de site distant** : site d’administration centrale ou site principal avec la base de données de site sur le serveur de site :

| Clients bureau    |Taille de machine virtuelle recommandée|Disques recommandés |
|--------------------|-------------------|------------------|
|**Jusqu’à 25 000**       | Serveur de site : F4S </br>Serveur de base de données : DS12_V2 | Serveur de site : 1xP30 </br>Serveur de base de données : 2xP30 (agrégé par bandes)  |
|**de 25 000 à 50 000**      | Serveur de site : F4S </br>Serveur de base de données : DS13_V2 | Serveur de site : 1xP30 </br>Serveur de base de données : 2xP30 (agrégé par bandes)   |
|**de 50 000 à 100 000**     | Serveur de site : F8S </br>Serveur de base de données : DS14_V2 | Serveur de site : 2xP30 (agrégé par bandes)   </br>Serveur de base de données : 3xP30 (agrégé par bandes)   |

Voici un exemple de configuration pour 50 000 à 100 000 clients sur DS14_V2 avec 3 disques P30 dans un volume agrégé par bandes avec des volumes logiques distincts pour les fichiers d’installation de Configuration Manager et les fichiers de base de données : ![VM)disks](media/vm_disks.png)  



## <a name="user-experience"></a>Expérience utilisateur
### <a name="you-mention-that-user-experience-is-one-of-the-main-areas-of-importance-why-is-that"></a>Vous indiquez que l’expérience utilisateur est l’un des principaux domaines d’importance, pourquoi ?
Les décisions que vous prenez quant à la mise en réseau, la disponibilité, les performances et l’emplacement où vous placez vos serveurs de site Configuration Manager peuvent directement affecter vos utilisateurs. Nous pensons qu’un déplacement vers Azure doit être transparent pour vos utilisateurs afin qu’ils ne rencontrent aucune modification de leurs interactions quotidiennes avec Configuration Manager.

### <a name="ok-i-get-it-i-plan-to-install-a-single-stand-alone-primary-site-on-an-azure-virtual-machine-and-i-want-to-make-sure-my-costs-are-low-should-i-place-remote-site-systems-like-management-points-distribution-points-and-software-update-points-on-azure-virtual-machines-as-well-or-on-premises"></a>Je comprends. J’envisage d’installer un site principal autonome unique sur une machine virtuelle Azure et je veux m’assurer que les coûts seront faibles. Dois-je placer les systèmes de site (distants) (tels que des points de gestion, des points de distribution et des points de mise à jour logicielle) sur des machines virtuelles Azure aussi ou localement ?
À l’exception des communications depuis le serveur de site vers un point de distribution, des communications de serveur à serveur dans un site peuvent avoir lieu à tout moment et n’utilisent aucun mécanisme pour contrôler l’utilisation de la bande passante réseau. Étant donné que vous ne pouvez pas contrôler les communications entre les systèmes de site, tous les coûts associés à ces communications doivent être pris en compte.

Les vitesses et la latence des réseaux sont d’autres facteurs à prendre en compte également. Des réseaux lents et non fiables peuvent affecter les fonctionnalités entre le serveur de site et les systèmes de site distants, ainsi que les communications des clients vers les systèmes de site. Le nombre de clients managés qui utilisent un système de site donné, ainsi que les fonctionnalités que vous utilisez activement doivent également être pris en compte.
En général, vous pouvez exploiter les conseils normaux en ce qui concerne les liaisons WAN et les systèmes de site, comme point de départ. Dans l’idéal, le débit réseau que vous sélectionnez et recevez entre Azure et votre intranet est cohérent avec un réseau WAN correctement connecté à un réseau rapide.

### <a name="what-about-content-distribution-and-content-management-should-standard-distribution-points-be-in-azure-or-on-premises-and-should-i-use-branchcache-or-pull-distribution-points-on-premises-or-should-i-make-exclusive-use-of-cloud-distribution-points"></a>Qu’en est-il de la distribution de contenu et de la gestion de contenu ? Les points de distribution standard doivent-ils être dans Azure ou localement, et dois-je utiliser BranchCache ou des points de distribution d’extraction localement ? Ou faut-il que j’effectue un usage exclusif des points de distribution cloud ?
L’approche de la gestion de contenu est très similaire à celui pour les serveurs de site et les systèmes de site.
- Si vous utilisez une connexion réseau rapide et fiable entre Azure et votre intranet avec un plan de données illimité, l’hébergement de points de distribution standard dans Azure pourrait être une option.
-  Si vous utilisez un plan de données contrôlé et que le coût de la bande passante est un problème ou que la connexion réseau entre Azure et votre intranet n’est pas rapide ou peut ne pas être fiable, vous pouvez envisager d’autres approches. Elles incluent le positionnement des points de distribution d’extraction ou standard localement, ainsi que l’utilisation de BranchCache. L’utilisation des points de distribution cloud est également une option, mais il existe certaines limites sur les types de contenu pris en charge (par exemple, aucune prise en charge pour les packages de mises à jour logicielles).

> [!NOTE]
>  Si la prise en charge PXE est requise, vous devez utiliser des points de distribution locaux (standard ou d’extraction) pour répondre aux demandes de démarrage. [WDS n’est actuellement pas pris en charge pour s’exécuter sur les machines virtuelles Azure](https://technet.microsoft.com/library/hh831764(v=ws.11).aspx).


### <a name="while-i-am-ok-with-the-limitations-of-cloud-based-distribution-points-i-dont-want-to-put-my-management-point-into-a-dmz-even-though-that-is-needed-to-support-my-internet-based-clients-do-i-have-any-other-options"></a>Les limitations des points de distribution cloud ne me posent pas de problème, mais je ne souhaite pas placer mon point de gestion dans une zone DMZ, même si cela est nécessaire pour prendre en charge mes clients basés sur Internet. Y a-t-il d’autres options à ma disposition ?
Oui ! Dans Configuration Manager version 1610, nous avons introduit la fonctionnalité de préversion [Passerelle de gestion cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway). (Cette fonctionnalité a d’abord été proposée dans la version Technical Preview 1606 sous le nom [Service de proxy cloud](/sccm/core/get-started/capabilities-in-technical-preview-1606#cloud_proxy).)

La fonctionnalité **Passerelle de gestion cloud** fournit un moyen simple de gérer les clients Configuration Manager sur Internet. Ce service, qui est déployé sur Microsoft Azure et nécessite un abonnement Azure, se connecte à votre infrastructure Configuration Manager locale à l’aide d’un nouveau rôle appelé « point de connexion de passerelle de gestion cloud ». Après son déploiement et sa configuration, les clients peuvent accéder aux rôles de système de site Configuration Manager locaux, qu’ils soient connectés au réseau privé interne ou à Internet.

Vous pouvez commencer à utiliser la passerelle de gestion cloud dans votre environnement et nous envoyer vos commentaires pour nous aider à améliorer cette fonctionnalité. Pour plus d’informations sur les fonctionnalités de préversions, consultez [Utiliser des fonctionnalités de préversions de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

### <a name="i-also-heard-that-you-have-another-new-feature-called-peer-cache-introduced-as-a-pre-release-feature-in-version-1610-is-that-different-than-branchcache-which-one-should-i-choose"></a>J’ai également entendu que vous avez introduit une nouvelle fonctionnalité, appelée Cache d’homologue, comme fonctionnalité préliminaire dans la version 1610. Est-elle différente de BranchCache ? Laquelle choisir ?
Oui, totalement différente. La fonctionnalité [Cache d’homologue](/sccm/core/plan-design/hierarchy/client-peer-cache) est une technologie 100 % native de Configuration Manager, alors que BranchCache est une fonctionnalité de Windows. Les deux peuvent vous être utiles. BranchCache utilise une diffusion pour rechercher le contenu requis alors que le cache d’homologue utilise les paramètres de groupe de limites et de flux de travail de distribution standard de Configuration Manager.

Vous pouvez configurer n’importe quel client comme source de mise en cache d’homologue. Ensuite, lorsque les points de gestion fournissent aux clients des informations sur les emplacements sources de contenu, ils fournissent des détails sur les points de distribution et toutes les sources de mise en cache d’homologue qui disposent du contenu que le client requiert.


## <a name="cost"></a>Coût
### <a name="ok-tell-me-a-bit-about-the-cost-will-this-be-a-cost-effective-solution-for-me"></a>Donnez-moi des informations sur le coût. Cette solution sera-t-elle à faible coût ?
Cela est difficile à dire puisque chaque environnement est différent. La meilleure chose à faire est d’estimer le coût de votre environnement à l’aide de la calculatrice de prix de Microsoft Azure : https://azure.microsoft.com/pricing/calculator/

## <a name="additional-resources"></a>Ressources supplémentaires
**Principes de base :**  https://azure.microsoft.com/documentation/articles/fundamentals-introduction-to-azure/

**Types de machines virtuelles Azure :**
 - Tailles de machine virtuelle : https://azure.microsoft.com/documentation/articles/virtual-machines-size-specs/  
 - Prix des machines virtuelles : https://azure.microsoft.com/pricing/details/virtual-machines/  
 - Prix du stockage : https://azure.microsoft.com/pricing/details/storage/

**Considérations sur les performances de disque :**    
 - Introduction aux disques Premium :  https://azure.microsoft.com/blog/2014/12/11/introducing-premium-storage-high-performance-storage-for-azure-virtual-machine-workloads/  
 - Informations approfondies sur les disques Premium : https://azure.microsoft.com/documentation/articles/storage-premium-storage-preview-portal/   
 - Collection pratique de graphiques pour les tailles maximales et les objectifs de performance du stockage : https://azure.microsoft.com/documentation/articles/storage-scalability-targets/  
 - Autre introduction + données utiles pour les passionnés d’informatique sur le fonctionnement du stockage Premium en coulisse :  https://azure.microsoft.com/blog/2015/04/16/azure-premium-storage-now-generally-available-2/

**Disponibilité :**
 - Temps de disponibilité dans les contrats SLA Azure IaaS : https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/  
 - Définition des groupes à haute disponibilité : https://azure.microsoft.com/documentation/articles/virtual-machines-manage-availability/

**Connectivité :**
 - ExpressRoute ou Azure VPN : https://azure.microsoft.com/blog/2014/06/10/expressroute-or-virtual-network-vpn-whats-right-for-me/
 - Prix d’Express Route : https://azure.microsoft.com/pricing/details/expressroute/
 - Plus sur Express Route : https://azure.microsoft.com/documentation/articles/expressroute-introduction/

 
