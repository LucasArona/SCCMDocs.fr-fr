---
title: Cache d’homologue client
titleSuffix: Configuration Manager
description: Utilisez le cache d’homologue pour les emplacements sources de contenu du client lors du déploiement de contenu avec System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b705a2cb8eccae3abe63c5de0680c712ab2e181e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337800"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache d’homologue pour les clients Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1101436-->
Utilisez le **cache d’homologue** pour gérer le déploiement de contenu sur les clients distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.   

> [!TIP]  
> Cette fonctionnalité a été introduite dans la version 1610 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1710, cette fonctionnalité n’est plus une fonctionnalité en préversion.  


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="overview"></a>Vue d'ensemble
Un client de cache d’homologue est un client Configuration Manager qui est activé pour utiliser le cache d’homologue. Un client de cache d’homologue qui a du contenu qu’il peut partager avec d’autres clients est une source de cache d’homologue.
 -  Vous utilisez des paramètres du client pour permettre aux clients d’utiliser le cache d’homologue.
 -  Pour partager du contenu en tant que source de cache d’homologue, un client de cache d’homologue :
    -  Les appareils doivent être joints à un domaine. Toutefois, un client qui n’est pas joint à un domaine peut obtenir du contenu à partir d’une source de cache d’homologue jointe à un domaine.
    -  Il doit être un membre du groupe de limites actuel du client qui recherche le contenu. Quand un client utilise une action de secours pour rechercher du contenu dans un groupe de limites voisin, la liste des emplacements sources de contenu n’inclut pas un client de cache d’homologue dans un groupe de limites voisin. Pour plus d’informations sur les groupes de limites actuels et voisins, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Le client Configuration Manager délivre chaque type de contenu dans le cache à d’autres clients en utilisant le cache d’homologue. Ce contenu comprend des fichiers Office 365 et représente des fichiers d’installation.<!--SMS.500850-->
 -  Le cache d’homologue ne remplace pas l’utilisation d’autres solutions, comme BranchCache. Le cache d’homologue fonctionne avec d’autres solutions pour vous donner plus d’options permettant d’étendre les solutions traditionnelles de déploiement de contenu, comme les points de distribution. Le cache d’homologue est une solution personnalisée qui ne dépend pas de BranchCache. Si vous n’activez pas ou n’utilisez pas Windows BranchCache, le cache d’homologue fonctionne quand même.

### <a name="operations"></a>Opérations

Pour activer le cache d’homologue, déployez les paramètres client sur un regroupement. Les membres de ce regroupement se comportent ensuite comme une source de contenu d’homologue pour d’autres clients du même groupe de limites.
 -  Un client qui agit en tant que source de contenu homologue envoie une liste des contenus mis en cache disponibles à son point de gestion.
 -  Quand le client suivant de ce groupe de limites demande ce contenu, chaque source du cache d’homologue qui a ce contenu et qui est en ligne est retournée dans la liste des sources potentielles de contenu. Cette liste inclut également les points de distribution et d’autres emplacements de source de contenu dans ce groupe de limites.
 -  Dans le processus normal, le client qui demande le contenu sélectionne une source dans la liste fournie. Le client essaie ensuite d’obtenir le contenu.

> [!NOTE]
> Si le client a recours à un groupe de limites voisin pour le contenu, il n’ajoute pas les emplacements sources de contenu du cache d’homologue du groupe de limites voisin à la liste des emplacements de sources de contenu potentiels.  


La bonne pratique consiste à choisir uniquement les clients les plus appropriés comme sources de cache d’homologue. Évaluez l’adéquation des clients en fonction d’attributs comme le type de châssis, l’espace disque et la connectivité réseau. Pour plus d’informations vous permettant de sélectionner les meilleurs clients à utiliser pour le cache d’homologue, consultez [ce blog rédigé par un consultant Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Accès limité à une source de cache d’homologue**  
À compter de la version 1702, un ordinateur source de cache d’homologue rejette les demandes de contenu quand il remplit une des conditions suivantes :  
  -  Il est en mode de batterie faible.
  -  La charge de l’UC dépasse 80 % au moment où le contenu est demandé.
  -  Les E/S disque ont une valeur *AvgDiskQueueLength* supérieure à 10.
  -  Il n’y a plus de connexion disponible vers l’ordinateur.   

Configurez ces paramètres à l’aide de la classe WMI du serveur de configuration du client pour la fonctionnalité de source d’homologue (*SMS_WinPEPeerCacheConfig*) dans le SDK System Center.

Quand l’ordinateur rejette une demande de contenu, l’ordinateur demandeur continue à rechercher le contenu dans la liste des emplacements de sources de contenu disponibles.   



### <a name="monitoring"></a>Analyse   
Pour vous aider à comprendre l’utilisation du cache d’homologue, vous pouvez afficher le tableau de bord Sources de données du client. Consultez la section relative au [tableau de bord Sources de données du client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

À partir de la version 1702, vous pouvez utiliser trois rapports pour afficher l’utilisation du cache d’homologue. Dans la console, accédez à **Surveillance** > **Comptes rendus** > **Rapports**. Tous les rapports ont le type **Contenu de distribution de logiciels** :
1.  **Rejet du contenu de la source de cache d’homologue** :  
Utilisez ce rapport pour comprendre la fréquence à laquelle les sources de cache d’homologue d’un groupe de limites rejettent une demande de contenu.
 - **Problème connu :** lorsque vous descendez dans la hiérarchie pour accéder à des résultats comme *MaxCPULoad* ou *MaxDiskIO*, il se peut que vous receviez une erreur qui indique que le rapport ou les détails sont introuvables. Pour contourner ce problème, utilisez les deux rapports suivants, qui montrent directement les résultats.

2. **Rejet conditionnel du contenu de la source de cache d’homologue** :  
Utilisez ce rapport pour comprendre les détails du rejet pour un groupe de limites ou un type de rejet donné. Vous pouvez spécifier :

  - **Problème connu :** vous ne pouvez pas choisir parmi une liste de paramètres disponibles ; vous devez les entrer manuellement. Entrez les valeurs *Nom de groupe de limites* et *Type de rejet* comme dans le premier rapport. Par exemple, pour *Type de rejet*, vous pouvez entrer *MaxCPULoad* ou *MaxDiskIO*.

3. **Détails du rejet du contenu de la source de cache d’homologue** :   
  Utilisez ce rapport pour comprendre quel était le contenu demandé par le client au moment du rejet.

 - **Problème connu :** vous ne pouvez pas choisir parmi une liste de paramètres disponibles ; vous devez les entrer manuellement. Entrez la valeur pour *Type de rejet* telle qu’elle apparaît dans le rapport **Rejet du contenu par une source de cache d’homologue**. Entrez ensuite *l’ID de ressource* pour la source de contenu sur laquelle vous voulez plus d’informations. Pour trouver l’ID de ressource de la source de contenu :  

    1. Recherchez le nom de l’ordinateur qui s’affiche comme *Source de cache d’homologue* dans les résultats du rapport **Rejet conditionnel du contenu de la source de cache d’homologue**.  
    2. Ensuite, accédez à **Biens et conformité** > **Appareils**, puis recherchez ce nom d’ordinateur. Utilisez la valeur de la colonne ID de ressource.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Exigences et considérations relatives au cache d’homologue
-   Le cache d’homologue est pris en charge sur tout système d’exploitation Windows pris en charge en tant que client Configuration Manager. Les systèmes d’exploitation autres que Windows ne sont pas pris en charge pour le cache d’homologue.

-   Des clients ne peuvent transférer du contenu qu’à partir de clients de cache d’homologue qui se trouvent dans leur groupe de limites actuel.

-   Avant la version 1706, chaque site où les clients utilisent le cache d’homologue doit être configuré avec un [compte d’accès réseau](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). Depuis la version 1706, ce compte n’est plus nécessaire, sauf dans le cas suivant : un client autorisé à utiliser le cache d’homologue exécute une séquence de tâches depuis le Centre logiciel, et cette séquence de tâches redémarre à partir d’une image de démarrage. Dans ce scénario, le client nécessite toujours le compte d’accès réseau. Quand le client est sur Windows PE, il utilise le compte d’accès réseau pour obtenir du contenu de la source de cache d’homologue.

    Quand c’est nécessaire, le cache d’homologue utilise le compte d’accès réseau pour authentifier les demandes de téléchargement provenant de pairs. Pour cela, ce compte a seulement besoin des autorisations d’utilisateur de domaine.

-   Le dernier envoi de l’inventaire matériel du client détermine la limite d’une source de contenu de cache d’homologue. Un client qui passe à un groupe de limites différent peut toujours être membre de son groupe de limites précédent pour les besoins liés au cache d’homologue. Ce comportement fait qu’un client peut se voir proposer une source de contenu de cache d’homologue qui ne se trouve pas à proximité de son emplacement réseau. Nous vous recommandons d’empêcher les clients qui adoptent souvent cette configuration de participer à une source de cache d’homologue.
-    Depuis la version 1706, le client de cache homologue vérifie d’abord que la source de contenu du cache d’homologue est en ligne avant d’essayer de télécharger le contenu. <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>Pour configurer les paramètres client du cache d’homologue du client
Pour plus d’informations sur la configuration des paramètres client, consultez [Paramètres du cache des clients](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).

Sur les clients autorisés à utiliser le cache d’homologue qui utilisent le pare-feu Windows, Configuration Manager configure les ports du pare-feu que vous spécifiez dans les paramètres des clients.
