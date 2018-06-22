---
title: Configurer des groupes de limites
titleSuffix: Configuration Manager
description: Aider les clients à trouver des systèmes de site à l’aide de groupes de limites pour organiser de façon logique des emplacements réseau associés appelés limites
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79c6796c116fbe4d182827e24f41ae4d1e5242fe
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342696"
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurer les groupes de limites pour System Center Configuration Manager


*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des groupes de limites dans Configuration Manager afin d’organiser de façon logique des emplacements réseau associés ([limites](/sccm/core/servers/deploy/configure/boundaries)) pour faciliter la gestion de votre infrastructure. Attribuez des limites aux groupes de limites avant d’utiliser le groupe de limites.

Par défaut, Configuration Manager crée un groupe de limites de site par défaut sur chaque site.

Pour configurer des groupes de limites, associez des limites (emplacements réseau) et des rôles de système de site, comme les points de distribution, au groupe de limites. Cette configuration permet d’associer les clients aux serveurs de système de site tels que les points de distribution qui se trouvent près des clients sur le réseau.

Pour augmenter la disponibilité des serveurs de systèmes de site, tels que les points de distribution, sur un plus large éventail d’emplacements réseau, affectez la même limite et le même serveur à plusieurs groupes de limites.

Les clients utilisent un groupe de limites pour les applications suivantes :  

-   Attribution automatique du site  
-   Recherche d’un serveur de système de site capable de fournir un service, notamment :
    - Points de distribution pour l’emplacement du contenu
    -   Points de mise à jour logicielle
    - Points de migration de l'état
    - Points de gestion préférés (Si vous utilisez des points de gestion préférés, vous devez activer cette option pour la hiérarchie et non pas à partir de la configuration du groupe de limites. Consultez la section [Activer l’utilisation des points de gestion préférés](#to-enable-use-of-preferred-management-points) de cette rubrique.)

##  <a name="boundary-groups-and-relationships"></a>Relations et groupes de limites
Pour chaque groupe de limites de votre hiérarchie, vous pouvez affecter :

-  Une ou plusieurs limites. Le groupe de limites **actif** d’un client correspond à un emplacement réseau défini comme limite affectée à un groupe de limites donné. Un client peut avoir plusieurs groupes de limites actifs.
- Un ou plusieurs rôles de système de site. Les clients peuvent toujours utiliser des rôles de système de site associés à leur groupe de limites actif. En fonction des configurations supplémentaires, ils peuvent dans certains cas utiliser les rôles de système de site dans les groupes de limites supplémentaires.  

Pour chaque groupe de limites créé, vous pouvez configurer un lien à sens unique vers un autre groupe de limites. Ce lien est appelé **relation**. Les groupes de limites vers lequel pointent ces liens sont appelés groupes de limites **voisins**. Un groupe de limites peut avoir plusieurs relations, chacune avec un groupe de limites voisin spécifique.

Quand un client ne parvient pas à trouver un serveur de système de site disponible dans son groupe de limites actif, la configuration de chaque relation détermine le moment où il commence à effectuer des recherches dans un groupe de limites voisin. Cette recherche dans des groupes supplémentaires est appelée **secours**.

## <a name="fallback"></a>Secours
Pour éviter des problèmes quand les clients ne trouvent pas de système de site disponible dans leur groupe de limites actif, définissez la relation entre les groupes de limites pour le comportement de secours. Le secours permet à un client d’étendre sa recherche à des groupes de limites supplémentaires pour trouver un système de site disponible.

Les relations sont configurées dans l’onglet **Relations** des propriétés du groupe de limites. Lorsque vous configurez une relation, vous définissez un lien vers un groupe de limites voisin. Pour chaque type de rôle de système de site pris en charge, configurez des paramètres indépendants pour le recours au groupe de limites voisin. Par exemple, quand vous configurez une relation vers un groupe de limites donné, définissez le déclenchement du secours après 20 minutes au lieu des 120 minutes par défaut pour les points de distribution. Pour obtenir un exemple plus complet, consultez [Exemple d’utilisation des groupes de limites](#example-of-using-boundary-groups).

Si un client ne trouve pas un rôle de système de site disponible dans son groupe de limites actif, il utilise le délai de secours en minutes. Ce délai détermine le moment où le client commence à rechercher un système de site disponible associé au groupe de limites voisin.  

Quand un client ne peut pas trouver de système de site disponible et commence à effectuer des recherches à des emplacements de groupes de limites voisins, il augmente le pool de systèmes de site disponibles. La configuration des groupes de limites et de leurs relations définit l’utilisation de ce pool par le client.

- Un groupe de limites peut avoir plusieurs relations. Avec plusieurs relations, vous pouvez configurer l’intervention de la solution de secours pour chaque type de système de site sur différents voisins après différents délais.    
- Les clients utilisent uniquement en secours un groupe de limites qui est un voisin direct de leur groupe de limites actuel.
- Quand un client est membre de plusieurs groupes de limites, le groupe de limites actif est défini en tant qu’union de tous les groupes de limites du client. Le client peut ensuite recourir à des voisins de n’importe lequel de ces groupes de limites d’origine.

### <a name="the-default-site-boundary-group"></a>Le groupe de limites de site par défaut
Outre les groupes de limites que vous créez, chaque site possède un groupe de limites de site par défaut créé par Configuration Manager. Ce groupe est nommé ***Default-Site-Boundary-Group&lt;sitecode>***. Par exemple, le groupe du site ABC s’appellerait *Default-Site-Boundary-Group&lt;ABC>.*

Pour chaque groupe de limites que vous créez, Configuration Manager crée automatiquement un lien implicite vers chacun des groupes de limites de site par défaut de la hiérarchie.
-   Le lien implicite est une option de secours par défaut d’un groupe de limites actif vers le groupe de limites de site par défaut, qui a un délai de secours par défaut de 120 minutes.
-   Pour les clients qui ne sont pas sur une limite associée à un groupe de limites : pour identifier les rôles de système de site valides, ils doivent utiliser le groupe de limites par défaut du site qui leur a été affecté.

Pour gérer le recours au groupe de limites de site par défaut :
- Ouvrez les propriétés du groupe de limites par défaut du site et modifiez les valeurs de l’onglet **Comportement par défaut**. Les modifications apportées ici s’appliquent à *tous* les liens implicites vers ce groupe de limites. Ces paramètres peuvent être remplacés lorsque vous configurez le lien explicite vers ce groupe de limites de site par défaut à partir d’un autre groupe de limites.
- Ouvrez les propriétés d’un groupe de limites personnalisé. Modifiez les valeurs du lien explicite vers un groupe de limites de site par défaut. Lorsque vous définissez un nouveau délai de secours ou de secours en bloc en minutes, cette modification affecte uniquement le lien que vous configurez. La configuration du lien explicite remplace les paramètres de l’onglet **Comportement par défaut** d’un groupe de limites de site par défaut.


## <a name="site-assignment"></a>Attribution de site  
 Vous pouvez configurer chaque groupe de limites avec un site attribué pour les clients.  

-   Quand un client récemment installé utilise l’attribution automatique de site, il rejoint le site attribué d’un groupe de limites qui englobe l’emplacement réseau actuel du client.  
-   Après avoir été attribué à un site, un client ne modifie pas son attribution de site quand il change d’emplacement réseau. Par exemple, si le client est en itinérance vers un nouvel emplacement réseau représenté par une limite dans un groupe de limites disposant d’une attribution de site différente, le site attribué au client n’est pas modifié.  
-   Lorsque la découverte de systèmes Active Directory détecte une nouvelle ressource, les informations sur le réseau de la ressource découverte sont évaluées en fonction des limites dans les groupes de limites. Ce processus associe la nouvelle ressource à un site attribué pour une utilisation par la méthode d'installation poussée du client.  
-   Quand une limite est membre de plusieurs groupes de limites auxquels différents sites sont attribués, les clients sélectionnent l’un des sites de manière aléatoire.  
-   Les modifications apportées à un site attribué à des groupes de limites s’appliquent uniquement aux nouvelles actions d’attribution de site. Les clients déjà attribués à un site ne réévaluent pas leur attribution à un site en fonction des changements apportés à la configuration d’un groupe de limites (ou à leur emplacement réseau).  

Pour plus d’informations sur l’attribution de site client, consultez [Utilisation de l’attribution automatique de site pour les ordinateurs](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) dans [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Points de distribution

Quand un client demande l’emplacement d’un point de distribution, Configuration Manager lui envoie une liste des systèmes de site. Ces systèmes de site sont du type approprié associé à chaque groupe de limites qui inclut l’emplacement réseau actuel du client :

-   **Lors de la distribution de logiciels**, les clients demandent un emplacement pour le contenu de déploiement disponible à partir d’un point de distribution, ou une autre source de contenu valide (par exemple, un client configuré pour le cache d’homologue).

-   **Durant le déploiement de système d’exploitation**, les clients demandent un emplacement où envoyer ou recevoir des informations sur la migration de leur état.  

Lors du déploiement de contenu, si un client demande du contenu qui n’est pas disponible à partir d’une source de son groupe de limites actif, le client continue de demander ce contenu. Il essaie différentes sources de contenu dans son groupe de limites actif, jusqu’à ce que la période de secours d’un groupe de limites voisin ou du groupe de limites de site par défaut soit atteinte. Si le client n’a pas encore trouvé de contenu, il étend ensuite sa recherche de sources de contenu aux groupes de limites voisins.

Si le contenu est distribué à la demande, mais qu’il n’est pas disponible sur un point de distribution quand il est demandé par un client, le processus de transfert du contenu vers ce point de distribution commence. Il est possible que le client trouve ce serveur comme source de contenu avant d’utiliser un groupe de limites voisin en secours.

## <a name="software-update-points"></a>Points de mise à jour logicielle
Les clients utilisent des groupes de limites pour rechercher un nouveau point de mise à jour logicielle. Pour contrôler les serveurs qu’un client peut trouver, ajoutez des points de mise à jour logicielle individuels à différents groupes de limites.

Si vous effectuez la mise à jour à partir d’une version antérieure à la version 1702, chaque site ajoute tous les points de mise à jour logicielle existants au groupe de limites de site par défaut. Ce comportement de mise à jour du site garde le comportement du client précédent pour sélectionner un point de mise à jour logicielle dans le pool de serveurs disponibles. Ce comportement est conservé tant que vous ne choisissez pas d’ajouter des points de mise à jour logicielle propres à chaque groupe de limites pour une sélection contrôlée et un comportement de secours.

Si vous installez un nouveau site, des points de mise à jour logicielle ne sont pas ajoutés au groupe de limites de site par défaut. Attribuez des points de mise à jour logicielle à un groupe de limites afin que les clients puissent les trouver et les utiliser.

### <a name="fallback-for-software-update-points"></a>Action de secours pour les points de mise à jour logicielle
Pour les points de mise à jour logicielle, le secours est configuré comme les autres rôles de système de site, mais avec les restrictions suivantes :
- **Les nouveaux clients utilisent des groupes de limites pour sélectionner les points de mise à jour logicielle.** Les nouveaux clients installés sélectionnent un point de mise à jour logicielle parmi les serveurs associés aux groupes de limites que vous configurez. Ce comportement vient remplacer celui qui consistait, pour les clients, à sélectionner un point de mise à jour logicielle de manière aléatoire dans une liste des serveurs partageant la forêt du client.

- **Les clients continuent d’utiliser un dernier point de mise à jour logicielle correct connu jusqu’à ce qu’ils en recherchent un nouveau une fois l’action de secours lancée.** Les clients qui disposent déjà d’un point de mise à jour logicielle continuent de l’utiliser jusqu’à ce qu’il ne soit plus accessible. Ce comportement comprend la poursuite de l’utilisation d’un point de mise à jour logicielle non associé au groupe de limites actif du client.

  Le fait qu’un point de mise à jour logicielle existant soit utilisé même si ce serveur ne se trouve pas dans le groupe de limites actif du client est intentionnel. Quand le point de mise à jour logicielle change, le client synchronise ses données avec le nouveau serveur, ce qui peut entraîner une utilisation importante du réseau. Si tous les clients basculent vers un nouveau serveur en même temps, le délai de transition peut permettre d’éviter la saturation du réseau.

- **Un client tente toujours d’atteindre son dernier point de mise à jour logicielle correct connu pendant 120 minutes avant de démarrer l’action de secours.** Après 120 minutes, si le client n’a pas établi de contact, il démarre l’action de secours. Quand l’action de secours démarre, le client reçoit la liste de tous les points de mise à jour logicielle à partir de son groupe de limites actif. Des points de mise à jour logicielle supplémentaires à partir de groupes de limites voisins et de site par défaut sont disponibles en fonction des configurations de secours.

### <a name="fallback-configurations-for-software-update-points"></a>Configurations de l’action de secours pour les points de mise à jour logicielle
#### <a name="beginning-with-version-1706"></a>Depuis la version 1706   
Vous pouvez configurer des **durées avant repli (en minutes)** inférieures à 120 minutes pour les points de mise à jour logicielle. Toutefois, le client tente toujours d’atteindre son point de mise à jour logicielle d’origine pendant 120 minutes. Il étend ensuite sa recherche à des serveurs supplémentaires. Les délais de secours des groupes de limites démarrent dès que le client ne parvient pas à atteindre le serveur d’origine. Quand le client étend sa recherche, le site fournit tous les groupes de limites configurés depuis moins de 120 minutes.

Pour bloquer l’action de secours pour un point de mise à jour logicielle vers un groupe de limites voisin, affectez au paramètre la valeur **Jamais d’action de secours**.

Après avoir échoué pendant deux heures à atteindre le serveur d’origine, le client utilise un cycle plus court pour établir une connexion à un nouveau point de mise à jour logicielle. Ce comportement permet au client d’explorer rapidement la liste croissante des points de mise à jour logicielle potentiels.

 -  **Exemple d’action de secours :**  
    Le groupe de limites actif d’un client a, pour les points de mise à jour logicielle, une action de secours dont la configuration est la suivante : *10* minutes pour le groupe de limites *A* et *130* minutes pour le groupe de limites *B*. Quand le client ne parvient pas à atteindre son dernier point de mise à jour logicielle correct connu :
    -   Le client tente d’atteindre uniquement son serveur d’origine pendant les 120 minutes suivantes. Après 10 minutes, les points de mise à jour logicielle du groupe de limites A sont ajoutés au pool de serveurs disponibles. Toutefois, le client ne peut pas tenter de contacter ces derniers ou tout autre serveur jusqu’à ce que se soit écoulée la période initiale de 120 minutes de reconnexion au serveur d’origine.
    -   Après avoir essayé de localiser ce point de mise à jour logicielle d’origine pendant 120 minutes, le client peut étendre sa recherche. À ce stade, le client ajoute des serveurs au pool disponible des points de mise à jour logicielle qui se trouvent dans son groupe de limites actif et dans tous les groupes de limites voisins configurés depuis une durée inférieure ou égale à 120 minutes. Ce pool inclut les serveurs du groupe de limites A qui ont été ajoutés au pool de serveurs disponibles.
    -       Après 10 minutes supplémentaires (soit un total de 130 minutes après le premier échec du client dans sa tentative d’atteindre son dernier point de mise à jour logicielle correct connu), le client étend la recherche pour inclure les points de mise à jour logicielle du groupe de limites B.  

#### <a name="prior-to-version-1706"></a>Avant la version 1706
Avant la version 1706, les configurations de l’action de secours pour les points de mise à jour logicielle ne gèrent pas une période configurable en minutes. Le comportement de l’action de secours est limité comme suit :

  - **Délai de secours (en minutes) :** cette option est grisée pour les points de mise à jour logicielle et n’est pas configurable. Elle est définie sur 120 minutes.
  -     **Ne jamais activer le secours :** vous pouvez bloquer le secours pour un point de mise à jour logicielle vers un groupe de limites voisin lorsque vous utilisez cette configuration.

Quand un client qui possède déjà un point de mise à jour logicielle ne parvient pas à l’atteindre, il en cherche un autre en secours. En cas d’utilisation du secours, le client reçoit la liste de tous les points de mise à jour logicielle à partir de son groupe de limites actif. S’il ne trouve pas de serveur disponible en 120 minutes, il a ensuite recours à ses groupes de limites voisins et au groupe de limites de site par défaut. Le recours aux deux groupes de limites se produit en même temps. Le délai de secours des points de mise à jour logicielle vers les groupes voisins est défini sur 120 minutes. Vous ne pouvez pas modifier ce délai. 120 minutes correspond également à la durée par défaut utilisée pour le recours au groupe de limites de site par défaut. Lorsque le client a recours à la fois à un groupe de limites voisin et au groupe de limites de site par défaut, il tente de contacter les points de mise à jour logicielle du groupe de limites voisin avant d’essayer d’utiliser ceux du groupe de limites de site par défaut.

### <a name="manually-switch-to-a-new-software-update-point"></a>Basculer manuellement vers un nouveau point de mise à jour logicielle
Outre l’action de secours, vous pouvez utiliser *Notification du client* pour forcer manuellement un appareil à basculer vers un nouveau point de mise à jour logicielle.

Quand vous basculez vers un nouveau serveur, les appareils utilisent l’action de secours pour rechercher ce serveur. Passez en revue vos configurations de groupes de limites. Vérifiez que vos points de mise à jour logicielle sont dans les groupes de limites appropriés avant de procéder à ce changement.

Pour plus d’informations, consultez [Basculer manuellement les clients vers un nouveau point de mise à jour logicielle](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Points de gestion
<!-- 1324594 -->
Depuis la version 1802, configurez des relations de secours pour les points de gestion entre les groupes de limites. Ce comportement offre un meilleur contrôle des points de gestion que les clients utilisent. L’onglet **Relations** des propriétés du groupe de limites comporte une colonne pour le point de gestion. Lors de l’ajout d’un nouveau groupe de limites de secours, le temps de secours du point de gestion est actuellement toujours égal à zéro (0). Ce comportement est identique pour le **Comportement par défaut** dans le groupe de limites de site par défaut.

Auparavant, un problème se produisait souvent pour les points de gestion protégés présents dans un réseau sécurisé. Les clients du réseau d’entreprise principal recevaient une stratégie comprenant ce point de gestion protégé, même s’ils ne pouvaient pas communiquer avec lui à travers un pare-feu. Pour résoudre ce problème, utilisez l’option **Jamais d’action de secours** pour que les clients n’utilisent en secours que les points de gestion avec lesquels ils peuvent communiquer.

Lors de la mise à niveau du site vers la version 1802, Configuration Manager ajoute tous les points de gestion sans accès via Internet au groupe de limites de site par défaut. Ce comportement de mise à niveau permet de s’assurer que les versions antérieures des clients continuent de communiquer avec les points de gestion. Pour tirer pleinement parti de cette fonctionnalité, déplacez vos points de gestion vers les groupes de limites de votre choix.

L’action de secours du groupe de limites de point de gestion ne modifie pas le comportement lors de l’installation du client (ccmsetup.exe). Si la ligne de commande ne spécifie pas le point de gestion initial avec le paramètre/MP, le nouveau client reçoit la liste complète des points de gestion disponibles. Pour son processus d’amorçage initial, le client utilise le premier point de gestion auquel il peut accéder. Une fois inscrit auprès du site, il recevra la liste des points de gestion convenablement triée avec ce nouveau comportement. 

Pour que les clients utilisent cette fonctionnalité, activez le paramètre suivant : **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites** dans **Paramètres de hiérarchie**. 

> [!Note]
> Les processus de déploiement de système d’exploitation ne prennent pas en charge les groupes de limites.

### <a name="troubleshooting"></a>Résolution des problèmes
De nouvelles entrées apparaissent dans **LocationServices.log**. L’attribut **Localité** identifie l’un des états suivants :
- 0 : Inconnu
- 1 : Le point de gestion spécifié se trouve uniquement dans le groupe de limites de site par défaut pour l’action de secours
- 2 : Le point de gestion spécifié se trouve dans un groupe de limites voisin ou distant. S’il est à la fois dans le groupe de limites de site par défaut et dans un groupe voisin, la localité est 2.
- 3 : Le point de gestion spécifié se trouve dans le groupe de limites local ou actif. S’il est à la fois dans le groupe de limites actif et dans un groupe voisin ou le groupe de limites de site par défaut, la localité est 3. Si vous n’activez pas le paramètre des points de gestion préférés dans les Paramètres de hiérarchie, la localité est toujours 3, quel que soit le groupe de limites du point de gestion.

Les clients utilisent en premier les points de gestion locaux (localité 3), puis distants (localité 2) et enfin de secours (localité 1). 

Quand un client reçoit cinq erreurs en 10 minutes et ne parvient pas à communiquer avec l’un des points de gestion de son groupe de limites actif, il tente de contacter un point de gestion d’un groupe de limites voisin ou du groupe de limites de site par défaut. Si le point de gestion du groupe de limites actif revient en ligne par la suite, le client retournera au point de gestion local lors du prochain cycle d’actualisation. Ce cycle a une durée de 24 heures, ou se termine au redémarrage du service de l’agent Configuration Manager.




## <a name="preferred-management-points"></a>Points de gestion préférés

 > [!Note]
 > Le comportement de ce paramètre de hiérarchie, **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**, change depuis la version 1802. Quand vous activez ce paramètre, Configuration Manager utilise la fonctionnalité de groupe de limites pour le point de gestion attribué. Pour plus d’informations, consultez [Points de gestion](#management-points). 

 Les points de gestion préférés permettent à un client d’identifier un point de gestion associé à son emplacement réseau actuel (limite) avec celui-ci.  

-   Un client essaie d’utiliser un point de gestion préféré de son site attribué avant d’en utiliser un qui n’est pas configuré comme préféré.  
-   Pour utiliser cette option, activez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites** dans **Paramètres de hiérarchie**. Configurez ensuite des groupes de limites au niveau de chaque site principal. Incluez les points de gestion à associer aux limites de ces groupes de limites.
-   Quand vous configurez les points de gestion préférés et qu’un client organise sa propre liste de points de gestion, il place les points de gestion préférés en haut de sa liste. Cette liste comprend tous les points de gestion du site affecté au client.  

> [!NOTE]  
>  L’itinérance du client signifie qu’il change d’emplacement réseau. Il peut s’agir, par exemple, d’un ordinateur portable déplacé vers un emplacement de bureau distant. Quand un client est en itinérance, il peut utiliser un point de gestion ou un point de gestion proxy du site local comme nouvel emplacement avant d’essayer d’utiliser un serveur de son site attribué. Cette liste de serveurs de son site attribué comprend les points de gestion préférés. Pour plus d’informations, consultez [Comprendre comment les clients recherchent des services et des ressources de site](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Chevauchement des limites  
 Configuration Manager prend en charge les configurations de limites se chevauchant pour l’emplacement du contenu. Quand l’emplacement réseau du client appartient à plusieurs groupes de limites :

-   Quand un client demande du contenu, Configuration Manager lui envoie une liste de tous les points de distribution qui disposent du contenu.  
-   Quand un client demande à un serveur d’envoyer ou de recevoir des informations sur la migration de son état, Configuration Manager lui envoie une liste de tous les points de migration d’état associés à un groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche depuis lequel transférer le contenu ou les informations sur la migration de l'état.  



## <a name="example-of-using-boundary-groups"></a>Exemple d’utilisation de groupes de limites
L’exemple suivant utilise un client qui recherche du contenu sur un point de distribution. Cet exemple peut s’appliquer à d’autres rôles de système de site qui utilisent des groupes de limites. Gardez à l’esprit que les points de mise à jour logicielle ne prennent pas en charge la configuration du recours à un groupe voisin, et qu’ils utilisent toujours une période de 120 minutes.

Vous créez trois groupes de limites qui ne partagent pas de limites ni de serveurs de système de site :
-   Groupe BG_A avec les points de distribution DP_A1 et DP_A2 associés au groupe
-   Groupe BG_B avec les points de distribution DP_B1 et DP_B2 associés au groupe
-   Groupe BG_C avec les points de distribution DP_C1 et DP_C2 associés au groupe

Ajoutez les emplacements réseau de vos clients en tant que limites uniquement au groupe de limites BG_A. Configurez ensuite des relations à partir de ce groupe de limites vers les deux autres groupes de limites :
-   Configurez des points de distribution pour le premier groupe *voisin* (BG_B) à utiliser après 10 minutes. Ce groupe contient les points de distribution DP_B1 et DP_B2. Les deux sont correctement connectés aux emplacements des premiers groupes de limites.
-   Configurez le deuxième groupe *voisin* (BG_C) à utiliser après 20 minutes. Ce groupe contient les points de distribution DP_C1 et DP_C2. Les deux se trouvent sur un réseau étendu à distance des deux autres groupes de limites.
-   Ajoutez également un point de distribution supplémentaire qui se trouve sur le serveur de site au groupe de limites de site par défaut du site. Ce serveur est l’emplacement source de contenu que vous préférez le moins, mais il se trouve au milieu de tous les groupes de limites.

    Exemple de groupes de limites et de durées de secours :

     ![Exemple de groupes de limites et de durées de secours](media/BG_Fallback.png)


Avec cette configuration :
-   Le client commence la recherche de contenu dans les points de distribution de son groupe de limites *actif* (BG_A). Il passe deux minutes dans chaque point avant de passer au suivant dans le groupe. Le pool des emplacements sources de contenu valides du client inclut DP_A1 et DP_A2.
-   Si le client ne parvient pas à trouver le contenu dans son groupe de limites *actuel* après une recherche de 10 minutes, il ajoute alors les points de distribution du groupe de limites BG_B à sa recherche. Il continue ensuite à rechercher le contenu dans un point de distribution de son pool combiné de serveurs. Ce pool inclut maintenant ceux des groupes de limites BG_A et BG_B. Le client continue de contacter chaque point de distribution pendant deux minutes avant de passer au serveur suivant de son pool. Le pool des emplacements sources de contenu valides du client inclut DP_A1, DP_A2, DP_B1 et DP_B2.
-   Après 10 minutes supplémentaires (20 minutes au total), si le client n’a toujours pas trouvé un point de distribution avec du contenu, il étend son pool de serveurs disponibles pour inclure ceux du deuxième groupe *voisin*, le groupe de limites BG_C. Le client dispose désormais de six points de distribution pour sa recherche (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 et DP_C2). Il continue de changer de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.
-   Si le client n’a pas trouvé le contenu après un total de 120 minutes, il revient en arrière pour inclure le *groupe de limites de site par défaut* dans le cadre de sa recherche continue. Le pool inclut désormais tous les points de distribution des trois groupes de limites configurés et le point de distribution final situé sur le serveur de site. Le client continue alors sa recherche de contenu, en changeant de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.

En configurant les différents groupes voisins pour être disponibles à différents moments, vous contrôlez quand des points de distribution spécifiques sont ajoutés en tant qu’emplacement source de contenu. Le client utilise le secours sur le groupe de limites de site par défaut comme filet de protection pour le contenu qui n’est pas disponible à partir de tout autre emplacement.





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>Modifications par rapport aux versions antérieures
Voici les principales modifications apportées aux groupes de limites et à la façon dont les clients recherchent le contenu dans Configuration Manager Current Branch. La plupart de ces modifications et concepts fonctionnent ensemble.


-   Les configurations rapides ou lentes sont supprimées : vous ne configurez plus des points de distribution individuels pour être rapides ou lents. Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon. En raison de cette modification, l’onglet **References** (Références) des propriétés du groupe de limites ne prend plus en charge la configuration rapide ou lente.
- Nouveau groupe de limites par défaut sur chaque site : chaque site principal possède un nouveau groupe de limites par défaut nommé ***Groupe-limites-site-défaut&lt;code_site>***. Quand un client n’est pas à un emplacement réseau affecté à un groupe de limites, il utilise les systèmes de site associés au groupe par défaut à partir de son site affecté. Envisagez d’utiliser ce groupe de limites en remplacement de la notion d’emplacement de secours pour le contenu.   
 -  **Allow fallback source locations for content** (Autoriser les emplacements sources de secours pour le contenu) est supprimé : vous ne configurez plus explicitement un point de distribution de secours à utiliser. Les options de configuration de ce paramètre sont supprimées de la console.

    En outre, le résultat de la définition du paramètre **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** sur un type de déploiement pour les applications a changé. Ce paramètre sur un type de déploiement permet maintenant à un client d’utiliser le groupe de limites de site par défaut comme emplacement source de contenu.

 -  Relations de groupes de limites : chaque groupe de limites peut être lié à un ou plusieurs groupes de limites supplémentaires. Ces liens forment des relations qui sont configurées sous le nouvel onglet des propriétés du groupe de limites nommé **Relations** :
    -   Chaque groupe de limites auquel un client est directement associé est appelé groupe de limites **actuel**.  
    -   Tout groupe de limites qu’un client peut utiliser en raison d’une association entre le groupe de limites *actif* de ce client et un autre groupe est appelé groupe de limites **voisin**.
    -  Sous l’onglet **Relations**, ajoutez des groupes de limites à utiliser comme groupe de limites *voisin*. Configurez également un délai en minutes de secours. Quand un client ne parvient pas à trouver le contenu à partir d’un point de distribution dans le groupe *actif*, ce délai détermine quand il doit commencer à effectuer des recherches dans les emplacements de contenu de ces groupes de limites *voisins*.

        Quand vous ajoutez ou modifiez la configuration d’un groupe de limites, vous avez la possibilité de bloquer le secours sur ce groupe de limites spécifique à partir du groupe actif que vous configurez.

    Pour utiliser la nouvelle configuration, définissez des associations explicites (liens) entre un groupe de limites et un autre. Configurez tous les points de distribution de ce groupe associé avec le même délai en minutes. Quand un client ne parvient pas à trouver une source de contenu dans son groupe de limites *actif*, la durée que vous configurez détermine quand il doit commencer à rechercher des sources de contenu dans son groupe de limites voisin.

    En plus des groupes de limites que vous configurez explicitement, chaque groupe de limites a un lien implicite vers le groupe de limites de site par défaut. Ce lien devient actif après 120 minutes. Ensuite, le groupe de limites de site par défaut devient un groupe de limites voisin. Ce comportement permet aux clients d’utiliser les points de distribution associés à ce groupe de limites comme emplacements sources de contenu.

    Ce comportement remplace ce qui était précédemment désigné sous le nom de secours pour le contenu. Remplacez ce comportement par défaut de 120 minutes en associant explicitement le groupe de limites de site par défaut à un groupe *actif*. Définissez une durée spécifique en minutes ou bloquez totalement le secours pour empêcher son utilisation.


-   Les clients tentent d’obtenir le contenu à partir de chaque point de distribution pendant deux minutes au maximum : quand un client recherche un emplacement source de contenu, il tente d’accéder à chaque point de distribution pendant deux minutes avant d’essayer ensuite un autre point de distribution. Ce comportement représente un changement par rapport aux versions précédentes où les clients tentaient de se connecter à un point de distribution pendant deux heures au maximum.

    - Les clients sélectionnent au hasard le premier point de distribution dans le pool des serveurs disponibles du groupe (ou des groupes) de limites *actif(s)* du client.

    - Après deux minutes, si le client n’a pas trouvé le contenu, il bascule vers un nouveau point de distribution et tente d’obtenir le contenu de ce serveur. Ce processus se répète toutes les deux minutes jusqu’à ce que le client trouve le contenu ou atteigne le dernier serveur dans son pool.

    - Si un client ne peut pas trouver un emplacement source de contenu valide dans son pool *actif* avant la période de secours sur un groupe de limites *voisin*, le client ajoute alors les points de distribution de ce groupe *voisin* à la fin de sa liste actuelle. Il effectue ensuite des recherches dans le groupe étendu d’emplacements sources qui inclut les points de distribution des deux groupes de limites.

        > [!TIP]  
        > Quand vous créez un lien explicite entre le groupe de limites actif et le groupe de limites de site par défaut, puis définissez une durée de secours inférieure à celle d’un lien vers un groupe de limites voisin, les clients commencent à effectuer des recherches dans les emplacements sources du groupe de limites de site par défaut avant d’inclure le groupe voisin.

    - Quand le client ne parvient pas à obtenir le contenu du dernier serveur dans le pool, il recommence le processus.


## <a name="procedures-for-boundary-groups"></a>Procédures pour les groupes de limites

### <a name="to-create-a-boundary-group"></a>Pour créer un groupe de limites  
1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un groupe limite**.  

3.  Dans la boîte de dialogue **Créer un groupe limite**, sélectionnez l’onglet **Général** et spécifiez un **Nom** pour ce groupe de limites.  

4.  Cliquez sur **OK** pour enregistrer le nouveau groupe de limites.  


### <a name="to-configure-a-boundary-group"></a>Pour configurer un groupe de limites  
 1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

 2.  Sélectionnez le groupe de limites à modifier.  

 3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

 4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, sélectionnez l'onglet **Général** pour modifier les limites membres de ce groupe de limites :  

     -   Pour ajouter des limites, cliquez sur **Ajouter**, cochez la case d'une ou plusieurs limites et cliquez sur **OK**.  

     -   Pour supprimer des limites, sélectionnez la limite à supprimer, puis cliquez sur **Supprimer**.  

 5.  Sélectionnez l'onglet **Références** pour modifier l'attribution de site et la configuration de serveur de système de site associée :  

     -   Pour autoriser l’utilisation de ce groupe de limites par des clients pour l’attribution de site, sélectionnez **Utiliser ce groupe limite pour l’attribution de site**. Sélectionnez ensuite un site dans la liste déroulante **Site attribué**.  

     -   Pour configurer les serveurs de système de site associés à ce groupe de limites  

     1.  Cliquez sur **Ajouter**, puis cochez la case d'un ou plusieurs serveurs. Les serveurs sont ajoutés en tant que serveurs de système de site associés à ce groupe de limites. Seuls les serveurs sur lesquels un rôle de système de site pris en charge est installé sont disponibles.  

         > [!NOTE]  
         >  Vous pouvez sélectionner n'importe quelle combinaison de systèmes de site disponibles à partir de n'importe quel site dans la hiérarchie. Les systèmes de site sélectionnés figurent sous l'onglet **Systèmes de site** des propriétés de chaque limite appartenant à ce groupe de limites.  

     2.  Pour supprimer un serveur de ce groupe de limites, sélectionnez le serveur, puis cliquez sur **Supprimer**.  

         > [!NOTE]  
         >  Pour ne plus utiliser ce groupe de limites pour l’association des systèmes de site, supprimez tous les serveurs répertoriés en tant que serveurs de système de site associés.  

 6.  Pour configurer le comportement de secours, sélectionnez l’onglet **Relations** :  

     - Cliquez sur **Ajouter**, puis sélectionnez le groupe de limites à configurer.

     - Définissez une durée de secours pour les points de distribution. Après cette période de temps, les clients dans le groupe de limites pour lequel vous configurez des relations peuvent commencer à rechercher du contenu à partir des points de distribution du groupe de limites que vous ajoutez.

     - Pour ne pas avoir recours à un groupe de limites spécifique, notamment le *groupe de limites du site par défaut* qui est configuré par défaut, sélectionnez le groupe de limites et cochez la case **Jamais d’action de secours**.   

 7.  Cliquez sur **OK** pour fermer les propriétés du groupe de limites et enregistrer la configuration.  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>Pour associer un serveur de système de site à un groupe de limites  
 1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

 2.  Sélectionnez le groupe de limites à modifier.  

 3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

 4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, sélectionnez l'onglet **Références** .  

 5.  Sous **Sélectionner des serveurs de système de site**, cliquez sur **Ajouter**. Sélectionnez les serveurs de système de site à associer à ce groupe de limites, puis cliquez sur **OK**.  

 6.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration du groupe de limites.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Pour configurer un site de secours pour l'attribution automatique de site  

  1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** >  **Sites**.  

  2.  Dans l'onglet **Accueil** , dans le groupe **Sites** , cliquez sur **Paramètres de hiérarchie**.  

  3.  Dans l'onglet **Général** , cochez la case **Utiliser un site de secours**, puis sélectionnez un site dans la liste déroulante **Site de secours** .  

  4.  Cliquez sur **OK** pour enregistrer la configuration.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Pour activer l’utilisation des points de gestion préférés  

 1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** > **Sites** puis, sous l’onglet **Accueil**, sélectionnez **Paramètres de hiérarchie**.  

 2.  Sous l’onglet **Général** des paramètres de hiérarchie, sélectionnez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**.  

 3.  Cliquez sur **OK** pour fermer la boîte de dialogue et enregistrer la configuration.  
