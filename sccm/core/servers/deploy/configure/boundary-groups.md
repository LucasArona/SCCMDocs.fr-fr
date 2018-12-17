---
title: Configurer des groupes de limites
titleSuffix: Configuration Manager
description: Aider les clients à trouver des systèmes de site à l’aide de groupes de limites pour organiser de façon logique des emplacements réseau associés appelés limites
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9b2eaaf3581bdb951b23541c96532c5b049aac1
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456360"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configurer des groupes de limites pour Configuration Manager


*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des groupes de limites dans Configuration Manager afin d’organiser de façon logique des emplacements réseau associés ([limites](/sccm/core/servers/deploy/configure/boundaries)) pour faciliter la gestion de votre infrastructure. Attribuez des limites aux groupes de limites avant d’utiliser le groupe de limites.

Par défaut, Configuration Manager crée un groupe de limites de site par défaut sur chaque site.

Pour configurer des groupes de limites, associez des limites (emplacements réseau) et des rôles de système de site, comme les points de distribution, au groupe de limites. Cette configuration permet d’associer les clients aux serveurs de système de site tels que les points de distribution qui se trouvent près des clients sur le réseau.

Pour augmenter la disponibilité des serveurs sur un plus large éventail d’emplacements réseau, affectez la même limite et le même serveur à plusieurs groupes de limites.

Les clients utilisent un groupe de limites pour les applications suivantes :  

-   Attribution automatique du site  
-   Recherche d’un serveur de système de site capable de fournir un service, notamment :  
    - Points de distribution pour l’emplacement du contenu  
    - Points de mise à jour logicielle  
    - Points de migration de l'état  
    - Points de gestion préférés  

        > [!Note]  
        > Si vous utilisez des points de gestion préférés, activez cette option pour la hiérarchie et non pas à partir de la configuration du groupe de limites. Pour plus d’informations, consultez [Activer l’utilisation des points de gestion préférés](#to-enable-use-of-preferred-management-points).  



##  <a name="boundary-groups-and-relationships"></a>Relations et groupes de limites

Pour chaque groupe de limites de votre hiérarchie, vous pouvez affecter :

- Une ou plusieurs limites. Le groupe de limites **actif** d’un client correspond à un emplacement réseau défini comme limite affectée à un groupe de limites donné. Un client peut avoir plusieurs groupes de limites actifs.  

- Un ou plusieurs rôles de système de site. Les clients peuvent toujours utiliser des rôles associés à leur groupe de limites actif. Selon d’autres configurations, ils peuvent utiliser des rôles disponibles dans d’autres groupes de limites.  

Pour chaque groupe de limites créé, vous pouvez configurer un lien à sens unique vers un autre groupe de limites. Ce lien est appelé **relation**. Les groupes de limites vers lequel pointent ces liens sont appelés groupes de limites **voisins**. Un groupe de limites peut avoir plusieurs relations, chacune avec un groupe de limites voisin spécifique.

Quand un client ne parvient pas à trouver un système de site disponible dans son groupe de limites actif, la configuration de chaque relation détermine le moment où il commence à effectuer des recherches dans un groupe de limites voisin. Cette recherche dans des groupes supplémentaires est appelée **repli**.

Pour plus d'informations, consultez les procédures suivantes :  
- [Créer un groupe de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_create)  
- [Configurer un groupe de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config)  



## <a name="fallback"></a>Repli

Pour éviter des problèmes quand les clients ne trouvent pas de système de site disponible dans leur groupe de limites actif, définissez la relation entre les groupes de limites pour le comportement de repli. Le repli permet à un client d’étendre sa recherche à des groupes de limites supplémentaires pour trouver un système de site disponible.

Les relations sont configurées dans l’onglet **Relations** des propriétés du groupe de limites. Lorsque vous configurez une relation, vous définissez un lien vers un groupe de limites voisin. Pour chaque type de rôle de système de site pris en charge, configurez des paramètres indépendants pour le recours au groupe de limites voisin. Pour plus d’informations, consultez [Configurer le comportement de repli](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_bg-fallback).

Par exemple, quand vous configurez une relation vers un groupe de limites donné, définissez le déclenchement du repli après 20 minutes. La valeur par défaut est de 120 minutes Pour obtenir un exemple plus complet, consultez [Exemple d’utilisation des groupes de limites](#example-of-using-boundary-groups).

Si un client ne trouve pas un rôle de système de site disponible dans son groupe de limites actif, il utilise le délai de repli en minutes. Ce délai détermine le moment où le client commence à rechercher un système de site disponible associé au groupe de limites voisin.  

Quand un client ne peut pas trouver de système de site disponible, il commence à effectuer des recherches à des emplacements de groupes de limites voisins. Ce comportement augmente le pool de systèmes de site disponibles. La configuration des groupes de limites et de leurs relations définit l’utilisation de ce pool par le client.

- Un groupe de limites peut avoir plusieurs relations. Avec cette configuration, vous pouvez configurer un repli pour chaque type de système de site sur différents voisins après différents délais.    

- Les clients utilisent uniquement le repli sur un groupe de limites qui est un voisin direct de leur groupe de limites actuel.  

- Quand un client est membre de plusieurs groupes de limites, le groupe de limites actif est défini en tant qu’union de tous les groupes de limites du client. Le client peut ensuite recourir à des voisins de n’importe lequel de ces groupes de limites d’origine.  


### <a name="the-default-site-boundary-group"></a>Le groupe de limites de site par défaut

Vous pouvez créer vos propres groupes de limites, en sachant que chaque site présente un groupe de limites de site par défaut créé par Configuration Manager. Ce groupe est nommé **Default-Site-Boundary-Group&lt;sitecode>**. Par exemple, le groupe du site ABC s’appellerait **Default-Site-Boundary-Group&lt;ABC>**.

Pour chaque groupe de limites que vous créez, Configuration Manager crée automatiquement un lien implicite vers chacun des groupes de limites de site par défaut de la hiérarchie.  

- Le lien implicite est une option de repli par défaut d’un groupe de limites actif sur le groupe de limites de site par défaut. Le délai de repli par défaut est de 120 minutes.  

- Pour les clients qui ne sont pas sur une limite associée à un groupe de limites : pour identifier les rôles de système de site valides, ils doivent utiliser le groupe de limites par défaut du site qui leur a été affecté.  


Pour gérer le recours au groupe de limites de site par défaut :  

- Ouvrez les propriétés du groupe de limites par défaut du site et modifiez les valeurs de l’onglet **Comportement par défaut**. Les modifications apportées ici s’appliquent à *tous* les liens implicites vers ce groupe de limites. Ces paramètres par défaut peuvent être remplacés lorsque vous configurez un lien explicite vers ce groupe de limites de site par défaut à partir d’un autre groupe de limites.  

- Ouvrez les propriétés d’un groupe de limites personnalisé. Modifiez les valeurs du lien explicite vers un groupe de limites de site par défaut. Lorsque vous définissez un nouveau délai de repli ou de repli en bloc en minutes, ce changement affecte uniquement le lien que vous configurez. La configuration du lien explicite remplace les paramètres de l’onglet **Comportement par défaut** d’un groupe de limites de site par défaut.  



## <a name="site-assignment"></a>Attribution de site  

 Vous pouvez configurer chaque groupe de limites avec un site attribué pour les clients.  

-   Quand un client récemment installé utilise l’attribution automatique de site, il rejoint le site attribué d’un groupe de limites qui englobe l’emplacement réseau actuel du client.  

-   Après avoir été attribué à un site, un client ne modifie pas son attribution de site quand il change d’emplacement réseau. Par exemple, un client est en itinérance vers un nouvel emplacement réseau. Cet emplacement est une limite dans un groupe de limites disposant d’une attribution de site différente. Le site attribué au client ne change pas.  

-   Lorsque la découverte de systèmes Active Directory détecte une nouvelle ressource, le site évalue les informations sur le réseau de la ressource en fonction des limites des groupes de limites. Ce processus associe la nouvelle ressource à un site attribué pour une utilisation par la méthode d'installation poussée du client.  

-   Quand une limite est membre de plusieurs groupes de limites auxquels différents sites sont attribués, les clients sélectionnent l’un des sites de manière aléatoire.  

-   Les modifications apportées à un site attribué à des groupes de limites s’appliquent uniquement aux nouvelles actions d’attribution de site. Les clients déjà attribués à un site ne réévaluent pas leur attribution à un site en fonction des changements apportés à la configuration d’un groupe de limites (ou à leur emplacement réseau).  

Pour plus d’informations sur l’attribution d’un site au client, consultez [Utilisation de l'attribution automatique de site pour les ordinateurs](/sccm/core/clients/deploy/assign-clients-to-a-site#BKMK_AutomaticAssignment).  

Pour plus d’informations sur la façon de configurer l’attribution de site, consultez les procédures suivantes :
- [Configurer l’attribution de site et sélectionner des serveurs de système de site](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_references)
- [Configurer un site de repli pour l’attribution de site automatique](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_site-fallback)



## <a name="distribution-points"></a>Points de distribution

Quand un client demande l’emplacement d’un point de distribution, Configuration Manager lui envoie une liste des systèmes de site. Ces systèmes de site sont du type approprié associé à chaque groupe de limites qui inclut l’emplacement réseau actuel du client :

-   **Lors de la distribution de logiciels**, les clients demandent un emplacement pour le contenu de déploiement sur une source de contenu valide. Cet emplacement peut être un point de distribution ou une source de cache d’homologue.  

-   **Durant le déploiement de système d’exploitation**, les clients demandent un emplacement où envoyer ou recevoir des informations sur la migration de leur état.  

    - Depuis la version 1810, les clients acquièrent le contenu en fonction des comportements du groupe de limites. Pour plus d’informations, consultez [Prise en charge des séquences de tâches pour les groupes de limites](#bkmk_bgr-osd).  

Lors du déploiement de contenu, si un client demande du contenu qui n’est pas disponible à partir d’une source de son groupe de limites actif, le client continue de demander ce contenu. Il essaie différentes sources de contenu dans son groupe de limites actif, jusqu’à ce que la période de repli d’un groupe de limites voisin ou du groupe de limites de site par défaut soit atteinte. Si le client n’a pas encore trouvé de contenu, il étend ensuite sa recherche de sources de contenu aux groupes de limites voisins.

Si vous configurez le contenu de sorte à le distribuer à la demande et qu’il n’est pas disponible sur un point de distribution quand un client le demande, le site commence à le transférer vers ce point de distribution. Il est possible que le client trouve ce serveur comme source de contenu avant d’utiliser un groupe de limites voisin en repli.


### <a name="bkmk_ccmsetup"></a> Installation du client
<!--1358840-->

Pendant l’installation du client Configuration Manager, le processus ccmsetup contacte le point de gestion pour localiser le contenu nécessaire. Pendant ce processus dans les versions 1806 et antérieures, le point de gestion retournait uniquement les points de distribution du groupe de limites actif du client. Si aucun contenu n’était disponible, le processus d’installation se repliait sur le téléchargement du contenu auprès du point de gestion. Aucune option ne permettait de se replier sur les points de distribution d’autres groupes de limites qui auraient pu disposer du contenu nécessaire. 

Depuis la version 1810, le point de gestion retourne les points de distribution en fonction de la configuration des groupes de limites. Si vous définissez des relations dans le groupe de limites, le point de gestion retourne les points de distribution dans l’ordre suivant :
1. Groupe de limites actif  
2. Groupes de limites voisins  
3. Groupe de limites par défaut du site  

> [!Note]  
> Le processus d’installation du client n’utilise pas la durée de repli. Pour localiser le contenu le plus rapidement possible, il se replie immédiatement sur le groupe de limites suivant.  


### <a name="bkmk_bgr-osd"></a> Prise en charge des séquences de tâches pour les groupes de limites
<!--1359025-->

Depuis la version 1810, quand un appareil exécute une séquence de tâches et a besoin d’acquérir du contenu, il utilise désormais des comportements de groupe de limites comparables à ceux du client Configuration Manager.   

Configurez ce comportement à l’aide des paramètres suivants dans la page **Points de distribution** du déploiement de la séquence de tâches : 

- **Utiliser un point de distribution distant quand aucun point de distribution local n’est disponible** : pour ce déploiement, la séquence de tâches peut se replier sur les points de distribution d’un groupe de limites voisin.  

- **Autoriser les clients à utiliser les points de distribution du groupe de limites de site par défaut** : pour ce déploiement, la séquence de tâches peut se replier sur les points de distribution du groupe de limites de site par défaut.  

Pour utiliser ce nouveau comportement, veillez à mettre à jour les clients vers la dernière version.

#### <a name="location-priority"></a>Priorité de l’emplacement  

La séquence de tâches tente d’acquérir le contenu dans l’ordre suivant :  

1. Sources de cache d’homologue  

2. Points de distribution du groupe de limites *actif*  

3. Points de distribution d’un groupe de limites *voisin*  

    > [!Important]  
    > Compte tenu de la nature du traitement des séquences de tâches, qui se produit en temps réel, il n’attend pas le temps de basculement d’un groupe de limites voisin. Il utilise les temps de basculement pour classer par ordre de priorité les groupes de limites voisins. Par exemple, si la séquence de tâches ne parvient pas à acquérir du contenu auprès d’un point de distribution de son groupe de limites actif, elle tente immédiatement auprès d’un point de distribution dans un groupe de limites voisin dont le temps de basculement est le plus court. Si ce processus échoue, il bascule alors vers un point de distribution dans un groupe de limites voisin ayant un temps de basculement supérieur.  

4. Points de distribution dans le groupe de limites *par défaut du site*  

Le fichier journal de séquence de tâches **smsts.log** indique la priorité des sources d’emplacement qu’il utilise en fonction des propriétés de déploiement.


### <a name="bkmk_bgoptions"></a> Options de groupe de limites pour les téléchargements à partir de pairs

<!--1356193--> Depuis la version 1806, les groupes de limites intègrent les paramètres supplémentaires suivants qui offrent davantage de contrôle sur la distribution du contenu dans l’environnement :  

- [Autoriser les téléchargements à partir de pairs dans ce groupe de limites](#bkmk_bgoptions1)  

- [Durant les téléchargements à partir de pairs, utiliser uniquement des pairs situés dans le même sous-réseau](#bkmk_bgoptions2)  

<!--1358749--> La version 1810 comporte les options supplémentaires suivantes :  

- [Préférer les points de distribution aux pairs au sein du même sous-réseau](#bkmk_bgoptions3)  

- [Préférer les points de distribution cloud aux points de distribution](#bkmk_bgoptions4)  

Pour plus d’informations sur la façon de configurer ces paramètres, consultez [Configurer un groupe de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_config).


#### <a name="bkmk_bgoptions1"></a> Autoriser les téléchargements à partir de pairs dans ce groupe de limites
Ce paramètre est activé par défaut. Le point de gestion fournit aux clients une liste d’emplacements de contenu qui comprend des sources de pairs. Ce paramètre affecte également l’application des ID de groupes pour [l’optimisation de la distribution](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).  

Il existe deux scénarios courants dans lesquels il peut être envisageable de désactiver cette option :  

- Si votre groupe de limites comporte des limites provenant d’emplacements éloignés sur le plan géographique, comme un VPN. Deux clients peuvent se trouver dans le même groupe de limites, parce qu’ils sont connectés au moyen d’un VPN, alors qu’ils sont situés à des endroits très différents, ce qui ne convient pas pour le partage de contenu entre pairs.  

- Si vous utilisez un seul grand groupe de limites pour l’attribution de site, qui ne fait référence à aucun point de distribution.  

#### <a name="bkmk_bgoptions2"></a> Durant les téléchargements à partir de pairs, utiliser uniquement des pairs situés dans le même sous-réseau
Ce paramètre dépend de l’option précédente. Lorsque cette option est activée, le point de gestion n’inclut dans la liste des emplacements de contenu que les sources de pairs qui se trouvent dans le même sous-réseau que le client.

Quelques scénarios courants pour l’activation de cette option :

- Votre conception de groupe de limites pour la distribution de contenu comprend un grand groupe de limites qui coïncide en partie avec d’autres groupes de limites plus petits. Avec ce nouveau paramètre, la liste des sources de contenu que le point de gestion fournit aux clients n’inclut que les sources de pairs provenant du même sous-réseau.

- Vous avez un seul grand groupe de limites pour tous les emplacements de bureau distant. Lorsque cette option est activée, les clients ne partagent du contenu qu’au sein du sous-réseau qui se trouve à l’emplacement du bureau distant, plutôt que de prendre le risque de partager du contenu entre différents emplacements.

#### <a name="bkmk_bgoptions3"></a> Préférer les points de distribution aux pairs au sein du même sous-réseau
Par défaut, le point de gestion classe par ordre de priorité les sources de cache d’homologue au début de la liste des emplacements de contenu. Ce paramètre inverse cette priorité pour les clients qui se trouvent dans le même sous-réseau que la source de cache d’homologue.  

#### <a name="bkmk_bgoptions4"></a> Préférer les points de distribution cloud aux points de distribution
Si vous avez une succursale qui utilise un lien Internet plus rapide, vous pouvez désormais classer le contenu cloud par ordre de priorité.  



## <a name="software-update-points"></a>Points de mise à jour logicielle

Les clients utilisent des groupes de limites pour rechercher un nouveau point de mise à jour logicielle. Pour contrôler les serveurs qu’un client peut trouver, ajoutez des points de mise à jour logicielle individuels à différents groupes de limites.

Si vous effectuez la mise à jour à partir d’une version antérieure à la version 1702, chaque site ajoute tous les points de mise à jour logicielle existants au groupe de limites de site par défaut. Ce comportement de mise à jour du site garde le comportement du client précédent pour sélectionner un point de mise à jour logicielle dans le pool de serveurs disponibles. Ce comportement est conservé tant que vous ne choisissez pas d’ajouter des points de mise à jour logicielle propres à chaque groupe de limites pour une sélection contrôlée et un comportement de repli.

Si vous installez un nouveau site, des points de mise à jour logicielle ne sont pas ajoutés au groupe de limites de site par défaut. Attribuez des points de mise à jour logicielle à un groupe de limites afin que les clients puissent les trouver et les utiliser.


### <a name="fallback-for-software-update-points"></a>Action de repli pour les points de mise à jour logicielle

Pour les points de mise à jour logicielle, le repli est configuré comme les autres rôles de système de site, mais avec les restrictions suivantes :  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>Les nouveaux clients utilisent des groupes de limites pour sélectionner les points de mise à jour logicielle.
Lorsque vous installez de nouveaux clients, ils sélectionnent un point de mise à jour logicielle parmi les serveurs associés aux groupes de limites que vous configurez. Ce comportement vient remplacer celui qui consistait, pour les clients, à sélectionner un point de mise à jour logicielle de manière aléatoire dans une liste des serveurs partageant la forêt du client.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>Les clients continuent d’utiliser un dernier point de mise à jour logicielle correct connu jusqu’à ce qu’ils en recherchent un nouveau une fois l’action de repli lancée.
Les clients qui disposent déjà d’un point de mise à jour logicielle continuent de l’utiliser jusqu’à ce qu’il ne soit plus accessible. Ce comportement comprend la poursuite de l’utilisation d’un point de mise à jour logicielle non associé au groupe de limites actif du client.

Ce comportement est intentionnel. Le client continue d’utiliser un point de mise à jour logicielle existant, même s’il ne s’agit pas du groupe de limites actif du client. Quand le point de mise à jour logicielle change, le client synchronise ses données avec le nouveau serveur, ce qui peut entraîner une utilisation importante du réseau. Si tous les clients basculent vers un nouveau serveur en même temps, le délai de transition peut permettre d’éviter la saturation du réseau.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Un client tente toujours d’atteindre son dernier point de mise à jour logicielle correct connu pendant 120 minutes avant de démarrer l’action de repli.
Après 120 minutes, si le client n’a pas établi de contact, il enclenche un repli. Quand le repli démarre, le client reçoit la liste de tous les points de mise à jour logicielle dans son groupe de limites actif. Des points de mise à jour logicielle supplémentaires dans des groupes de limites voisins et de site par défaut sont disponibles en fonction des configurations de repli.


### <a name="fallback-configurations-for-software-update-points"></a>Configurations de repli pour les points de mise à jour logicielle

Vous pouvez configurer des **durées avant repli (en minutes)** inférieures à 120 minutes pour les points de mise à jour logicielle. Toutefois, le client tente toujours d’atteindre son point de mise à jour logicielle d’origine pendant 120 minutes. Il étend ensuite sa recherche à des serveurs supplémentaires. Les délais de repli des groupes de limites démarrent dès que le client ne parvient pas à atteindre le serveur d’origine. Quand le client étend sa recherche, le site fournit tous les groupes de limites configurés depuis moins de 120 minutes.

Pour bloquer le repli d’un point de mise à jour logicielle sur un groupe de limites voisin, affectez au paramètre la valeur **Jamais de repli**.

Après avoir échoué pendant deux heures à atteindre le serveur d’origine, le client utilise un cycle plus court pour établir une connexion à un nouveau point de mise à jour logicielle. Ce comportement permet au client d’explorer rapidement la liste croissante des points de mise à jour logicielle potentiels.

#### <a name="example"></a>Exemple
Vous configurez des points de mise à jour logicielle dans le groupe de limites *A* pour qu’ils basculent après **10** minutes. Vous configurez le même paramètre pour le groupe de limites *B* sur **130** minutes. Un client dans le groupe de limites *Z* ne parvient pas à atteindre son dernier point de mise à jour logicielle correct connu.

- Pendant les 120 prochaines minutes, le client essaie d’atteindre uniquement son serveur d’origine dans le groupe de limites Z. Après 10 minutes, Configuration Manager ajoute les points de mise à jour logicielle à partir d’un groupe de limites A au pool de serveurs disponibles. Toutefois, le client ne tente pas de les contacter, ni aucun autre serveur, jusqu’à ce que la période initiale de 120 minutes s’écoule.  

- Après avoir essayé de contacter le point de mise à jour logicielle d’origine pendant 120 minutes, le client étend sa recherche. Il ajoute des serveurs au pool disponible des points de mise à jour logicielle qui se trouvent dans son groupe de limites actif et dans tous les groupes de limites voisins configurés depuis une durée inférieure ou égale à 120 minutes. Ce pool inclut les serveurs du groupe de limites A qui ont été ajoutés au pool de serveurs disponibles.  

- Après 10 minutes supplémentaires, le client étend la recherche pour inclure les points de mise à jour logicielle du groupe de limites B. Ce qui donne un total de 130 minutes après le premier échec du client dans sa tentative d’atteindre son dernier point de mise à jour logicielle correct connu.  


### <a name="manually-switch-to-a-new-software-update-point"></a>Basculer manuellement vers un nouveau point de mise à jour logicielle

En plus du repli, utilisez la notification du client pour forcer manuellement un appareil à basculer vers un nouveau point de mise à jour logicielle.

Quand vous basculez vers un nouveau serveur, les appareils utilisent le repli pour rechercher ce serveur. Passez en revue vos configurations de groupes de limites. Vérifiez que vos points de mise à jour logicielle sont dans les groupes de limites appropriés avant de procéder à ce changement.

Pour plus d’informations, consultez [Basculer manuellement les clients vers un nouveau point de mise à jour logicielle](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Points de gestion
<!-- 1324594 --> Depuis la version 1802, configurez des relations de repli pour les points de gestion entre les groupes de limites. Ce comportement offre un meilleur contrôle des points de gestion que les clients utilisent. L’onglet **Relations** des propriétés du groupe de limites comporte une colonne pour le point de gestion. Lors de l’ajout d’un nouveau groupe de limites de repli, le temps de repli du point de gestion est actuellement toujours égal à zéro (0). Ce comportement est identique pour le **Comportement par défaut** dans le groupe de limites de site par défaut.

Auparavant, un problème se produisait souvent pour les points de gestion protégés présents dans un réseau sécurisé. Les clients du réseau d’entreprise principal recevaient une stratégie comprenant ce point de gestion protégé, même s’ils ne pouvaient pas communiquer avec lui à travers un pare-feu. Pour résoudre ce problème, utilisez l’option **Jamais de repli** pour que les clients ne se replient que sur les points de gestion avec lesquels ils peuvent communiquer.

Lors de la mise à niveau du site vers la version 1802, Configuration Manager ajoute tous les points de gestion intranet au groupe de limites de site par défaut. (Ce groupe de serveurs n’inclut pas les points de gestion qui sont uniquement accessibles sur Internet.) Ce comportement de mise à niveau permet de s’assurer que les versions antérieures des clients continuent de communiquer avec les points de gestion. Pour tirer pleinement parti de cette fonctionnalité, déplacez vos points de gestion vers les groupes de limites de votre choix.

> [!Note]  
> Si vous activez un repli sur les points de distribution dans le groupe de limites par défaut de site, et qu’un point de gestion est colocalisé sur un point de distribution, le site ajoute également le point de gestion au groupe de limites par défaut de site.<!--VSO 2841292-->  

Si un client se trouve dans un groupe de limites sans point de gestion attribué, le site donne au client la liste complète des points de gestion. Ce comportement permet de s’assurer qu’un client reçoit toujours une liste de points de gestion.

Le repli du groupe de limites de point de gestion ne change pas le comportement lors de l’installation du client (ccmsetup.exe). Si la ligne de commande ne spécifie pas le point de gestion initial avec le paramètre/MP, le nouveau client reçoit la liste complète des points de gestion disponibles. Pour son processus d’amorçage initial, le client utilise le premier point de gestion auquel il peut accéder. Une fois inscrit auprès du site, il recevra la liste des points de gestion convenablement triée avec ce nouveau comportement. 

Pour plus d’informations sur le comportement du client pour acquérir du contenu lors de l’installation, consultez [Installation du client](#bkmk_ccmsetup).

Au cours de la mise à niveau du client, si vous ne spécifiez pas le paramètre de ligne de commande /MP, le client interroge les sources comme Active Directory et WMI concernant n’importe quel point de gestion disponible. La mise à niveau du client ne respecte pas la configuration du groupe de limites. <!--VSO 2841292-->  

Pour que les clients utilisent cette fonctionnalité, activez le paramètre suivant : **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites** dans **Paramètres de hiérarchie**. 

> [!Note]  
> Les processus de déploiement de système d’exploitation ne prennent pas en charge les groupes de limites pour les points de gestion.  


### <a name="troubleshooting"></a>Résolution des problèmes

De nouvelles entrées apparaissent dans **LocationServices.log**. L’attribut **Localité** identifie l’un des états suivants :

- **0** : Inconnu  

- **1** : le point de gestion spécifié se trouve uniquement dans le groupe de limites de site par défaut pour le repli  

- **2** : le point de gestion spécifié se trouve dans un groupe de limites voisin ou distant. S’il est à la fois dans le groupe de limites de site par défaut et dans un groupe voisin, la localité est 2.  

- **3** : le point de gestion spécifié se trouve dans le groupe de limites local ou actif. S’il est à la fois dans le groupe de limites actif et dans un groupe voisin ou le groupe de limites de site par défaut, la localité est 3. Si vous n’activez pas le paramètre des points de gestion préférés dans les Paramètres de hiérarchie, la localité est toujours 3, quel que soit le groupe de limites du point de gestion.  

Les clients utilisent en premier les points de gestion locaux (localité 3), puis distants (localité 2) et enfin de repli (localité 1). 

Quand un client reçoit cinq erreurs en 10 minutes et ne parvient pas à communiquer avec l’un des points de gestion de son groupe de limites actif, il tente de contacter un point de gestion d’un groupe de limites voisin ou du groupe de limites de site par défaut. Si le point de gestion du groupe de limites actif revient en ligne par la suite, le client retourne au point de gestion local lors du prochain cycle d’actualisation. Ce cycle a une durée de 24 heures, ou se termine au redémarrage du service de l’agent Configuration Manager.



## <a name="bkmk_preferred"></a> Points de gestion préférés

 > [!Note]
 > Le comportement de ce paramètre de hiérarchie, **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**, change depuis la version 1802. Quand vous activez ce paramètre, Configuration Manager utilise la fonctionnalité de groupe de limites pour le point de gestion attribué. Pour plus d’informations, consultez [Points de gestion](#management-points). 

 Les points de gestion préférés permettent à un client d’identifier un point de gestion associé à son emplacement réseau actuel (limite) avec celui-ci.  

- Un client essaie d’utiliser un point de gestion préféré de son site attribué avant d’en utiliser un qui n’est pas configuré comme préféré.  

- Pour utiliser cette option, activez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites** dans **Paramètres de hiérarchie**. Configurez ensuite des groupes de limites au niveau de chaque site principal. Incluez les points de gestion à associer aux limites de ces groupes de limites. Pour plus d’informations, consultez [Activer l’utilisation des points de gestion préférés](/sccm/core/servers/deploy/configure/boundary-group-procedures#bkmk_proc-prefer).  

- Quand vous configurez les points de gestion préférés et qu’un client organise sa propre liste de points de gestion, il place les points de gestion préférés en haut de sa liste. Cette liste comprend tous les points de gestion du site affecté au client.  

> [!NOTE]  
>  L’itinérance du client signifie qu’il change d’emplacement réseau. Il peut s’agir, par exemple, d’un ordinateur portable déplacé vers un emplacement de bureau distant. Quand un client est en itinérance, il peut utiliser un point de gestion à partir du site local avant d’essayer d’utiliser un serveur de son site attribué. Cette liste de serveurs de son site attribué comprend les points de gestion préférés. Pour plus d’informations, consultez [Comprendre comment les clients recherchent des services et des ressources de site](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  



## <a name="overlapping-boundaries"></a>Chevauchement des limites  

 Configuration Manager prend en charge les configurations de limites se chevauchant pour l’emplacement du contenu. Quand l’emplacement réseau du client appartient à plusieurs groupes de limites :

-   Quand un client demande du contenu, Configuration Manager lui envoie une liste de tous les points de distribution qui disposent du contenu.  

-   Quand un client demande à un serveur d’envoyer ou de recevoir des informations sur la migration de son état, Configuration Manager lui envoie une liste de tous les points de migration d’état associés à un groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche depuis lequel transférer le contenu ou les informations sur la migration de l'état.  



## <a name="example-of-using-boundary-groups"></a>Exemple d’utilisation de groupes de limites

L’exemple suivant utilise un client qui recherche du contenu sur un point de distribution. Cet exemple peut s’appliquer à d’autres rôles de système de site qui utilisent des groupes de limites. 

Créez trois groupes de limites qui ne partagent pas de limites ni de serveurs de système de site :  

- Groupe BG_A avec les points de distribution DP_A1 et DP_A2   

- Groupe BG_B avec les points de distribution DP_B1 et DP_B2  

- Groupe BG_C avec les points de distribution DP_C1 et DP_C2  

Ajoutez les emplacements réseau de vos clients en tant que limites uniquement au groupe de limites BG_A. Configurez ensuite des relations à partir de ce groupe de limites vers les deux autres groupes de limites :  

- Configurez des points de distribution pour le premier groupe *voisin* (BG_B) à utiliser après 10 minutes. Ce groupe contient les points de distribution DP_B1 et DP_B2. Les deux sont correctement connectés aux emplacements des premiers groupes de limites.  

- Configurez le deuxième groupe *voisin* (BG_C) à utiliser après 20 minutes. Ce groupe contient les points de distribution DP_C1 et DP_C2. Les deux se trouvent sur un réseau étendu à distance des deux autres groupes de limites.  

- Ajoutez également un point de distribution supplémentaire qui se trouve sur le serveur de site au groupe de limites de site par défaut. Ce serveur est l’emplacement source de contenu que vous préférez le moins, mais il se trouve au milieu de tous les groupes de limites.

    Exemple de groupes de limites et de durées de repli :

     ![Exemple de groupes de limites et de durées de repli](media/BG_Fallback.png)


Avec cette configuration :  

- Le client commence la recherche de contenu dans les points de distribution de son groupe de limites *actif* (BG_A). Il passe deux minutes dans chaque point avant de passer au suivant dans le groupe. Le pool des emplacements sources de contenu valides du client inclut DP_A1 et DP_A2.  

- Si le client ne parvient pas à trouver le contenu dans son groupe de limites *actuel* après une recherche de 10 minutes, il ajoute alors les points de distribution du groupe de limites BG_B à sa recherche. Il continue ensuite à rechercher le contenu dans un point de distribution de son pool combiné de serveurs. Ce pool inclut maintenant ceux des groupes de limites BG_A et BG_B. Le client continue de contacter chaque point de distribution pendant deux minutes avant de passer au serveur suivant de son pool. Le pool des emplacements sources de contenu valides du client inclut DP_A1, DP_A2, DP_B1 et DP_B2.  

- Après 10 minutes supplémentaires (20 minutes au total), si le client n’a toujours pas trouvé un point de distribution avec du contenu, il étend son pool de serveurs disponibles pour inclure ceux du deuxième groupe *voisin*, le groupe de limites BG_C. Le client dispose désormais de six points de distribution pour sa recherche : DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 et DP_C2. Il continue de changer de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.  

- Si le client n’a pas trouvé le contenu après un total de 120 minutes, il revient en arrière pour inclure le *groupe de limites de site par défaut* dans le cadre de sa recherche continue. Le pool inclut désormais tous les points de distribution des trois groupes de limites configurés et le point de distribution final situé sur le serveur de site. Le client continue alors sa recherche de contenu, en changeant de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.  

En configurant les différents groupes voisins pour être disponibles à différents moments, vous contrôlez quand des points de distribution spécifiques sont ajoutés en tant qu’emplacement source de contenu. Le client utilise le repli sur le groupe de limites de site par défaut comme filet de protection pour le contenu qui n’est pas disponible à partir de tout autre emplacement.



## <a name="changes-from-prior-versions"></a>Modifications par rapport aux versions antérieures

Voici les principales modifications apportées aux groupes de limites et à la façon dont les clients recherchent le contenu dans Configuration Manager Current Branch. La plupart de ces modifications et concepts fonctionnent ensemble.


### <a name="configurations-for-fast-or-slow-are-removed"></a>Les configurations rapides ou lentes sont supprimées

Vous ne configurez plus des points de distribution individuels pour qu’ils soient rapides ou lents. Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon. En raison de cette modification, l’onglet **References** (Références) des propriétés du groupe de limites ne prend plus en charge la configuration rapide ou lente.  


### <a name="new-default-boundary-group-at-each-site"></a>Nouveau groupe de limites par défaut sur chaque site

Chaque site principal possède un nouveau groupe de limites par défaut nommé **Groupe-limites-site-défaut&lt;code_site>**. Quand un client n’est pas à un emplacement réseau affecté à un groupe de limites, il utilise les systèmes de site associés au groupe par défaut à partir de son site affecté. Envisagez d’utiliser ce groupe de limites en remplacement de la notion d’emplacement de repli pour le contenu.     

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>**Autoriser l'emplacement source de secours pour le contenu** est supprimé
Vous ne configurez plus explicitement un point de distribution à utiliser pour le repli. Les options de configuration de ce paramètre sont supprimées de la console.

De plus, le résultat de la définition du paramètre **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** sur un type de déploiement pour les applications a changé. Ce paramètre sur un type de déploiement permet maintenant à un client d’utiliser le groupe de limites de site par défaut comme emplacement source de contenu.

#### <a name="boundary-groups-relationships"></a>Relations des groupes de limites
Vous pouvez lier chaque groupe de limites à un ou plusieurs groupes de limites supplémentaires. Ces liens forment des relations que vous configurez sous le nouvel onglet des propriétés du groupe de limites nommé **Relations** :  

- Chaque groupe de limites auquel un client est directement associé est appelé groupe de limites **actuel**.  

- Tout groupe de limites qu’un client peut utiliser en raison d’une association entre le groupe de limites *actif* de ce client et un autre groupe est appelé groupe de limites **voisin**.  

- Sous l’onglet **Relations**, ajoutez des groupes de limites à utiliser comme groupe de limites *voisin*. Configurez également un délai en minutes de repli. Quand un client ne parvient pas à trouver le contenu à partir d’un point de distribution dans le groupe *actif*, ce délai détermine quand il doit commencer à effectuer des recherches dans les emplacements de contenu de ces groupes de limites *voisins*.  

    Quand vous ajoutez ou modifiez la configuration d’un groupe de limites, vous pouvez bloquer le repli sur ce groupe de limites spécifique à partir du groupe actif que vous configurez.  

Pour utiliser la nouvelle configuration, définissez des associations explicites (liens) entre un groupe de limites et un autre. Configurez tous les points de distribution de ce groupe associé avec le même délai en minutes. Quand un client ne parvient pas à trouver une source de contenu dans son groupe de limites *actif*, la durée que vous configurez détermine quand il doit commencer à rechercher des sources de contenu dans son groupe de limites voisin.

En plus des groupes de limites que vous configurez explicitement, chaque groupe de limites a un lien implicite vers le groupe de limites de site par défaut. Ce lien devient actif après 120 minutes. Ensuite, le groupe de limites de site par défaut devient un groupe de limites voisin. Ce comportement permet aux clients d’utiliser les points de distribution associés à ce groupe de limites comme emplacements sources de contenu.

Ce comportement remplace ce qui était précédemment désigné sous le nom de repli pour le contenu. Remplacez ce comportement par défaut de 120 minutes en associant explicitement le groupe de limites de site par défaut à un groupe *actif*. Définissez une durée spécifique en minutes ou bloquez totalement le repli pour empêcher son utilisation.


### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>Les clients tentent d’obtenir le contenu à partir de chaque point de distribution pendant deux minutes au maximum

Quand un client recherche un emplacement source de contenu, il tente d’accéder à chaque point de distribution pendant deux minutes avant d’essayer ensuite un autre point de distribution. Ce comportement représente un changement par rapport aux versions précédentes où les clients tentaient de se connecter à un point de distribution pendant deux heures au maximum.

- Les clients sélectionnent au hasard le premier point de distribution dans le pool des serveurs disponibles du groupe (ou des groupes) de limites *actif(s)* du client.  

- Après deux minutes, si le client n’a pas trouvé le contenu, il bascule vers un nouveau point de distribution et tente d’obtenir le contenu de ce serveur. Ce processus se répète toutes les deux minutes jusqu’à ce que le client trouve le contenu ou atteigne le dernier serveur dans son pool.  

- Si un client ne peut pas trouver un emplacement source de contenu valide dans son pool *actif* avant la période de repli sur un groupe de limites *voisin*, le client ajoute alors les points de distribution de ce groupe *voisin* à la fin de sa liste actuelle. Il effectue ensuite des recherches dans le groupe étendu d’emplacements sources qui inclut les points de distribution des deux groupes de limites.  

    > [!TIP]  
    > Quand vous créez un lien explicite entre le groupe de limites actif et le groupe de limites de site par défaut, puis définissez une durée de repli inférieure à celle d’un lien vers un groupe de limites voisin, les clients commencent à effectuer des recherches dans les emplacements sources du groupe de limites de site par défaut avant d’inclure le groupe voisin.  

- Quand le client ne parvient pas à obtenir le contenu du dernier serveur dans le pool, il recommence le processus.  



## <a name="see-also"></a>Voir aussi

- [Procédures pour les groupes de limites](/sccm/core/servers/deploy/configure/boundary-group-procedures)  

- [À propos des limites](/sccm/core/servers/deploy/configure/boundaries)  

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  
