---
title: Cache d’homologue client
titleSuffix: Configuration Manager
description: Utilisez le cache de pair client pour les emplacements sources lors du déploiement de contenu avec Configuration Manager.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90c5c57d1717363d83fa921d68caced8cf9e8da1
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251715"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Cache de pair pour les clients Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1101436-->
Utilisez le cache de pair pour gérer le déploiement de contenu sur les clients à des emplacements distants. Le cache d’homologue est une solution Configuration Manager intégrée qui permet aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.   

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



## <a name="overview"></a>Vue d'ensemble

Définitions :  

- **Client de cache de pair** : Tout client Configuration Manager qui télécharge du contenu à partir d’un pair  

- **Source de cache de pair** : Un client Configuration Manager que vous activez pour le cache de pair et qui a du contenu à partager avec d’autres clients  

Utilisez des paramètres clients pour permettre à des clients d’être des sources de cache de pair. Vous n’avez pas besoin d’activer des clients de cache de pair. Quand vous autorisez des clients à être des sources de cache de pair, le point de gestion les inclut dans la liste des sources d’emplacement de contenu.<!--510397--> Pour plus d’informations sur ce processus, consultez [Opérations](#operations).  

Une source de cache de pair doit être membre du groupe de limites actuel du client de cache de pair. Le point de gestion n’inclut pas les sources de cache de pair d’un groupe de limites voisin dans la liste des sources de contenu qu’il fournit au client. Il inclut seulement les points de distribution d’un groupe de limites voisin. Pour plus d’informations sur les groupes de limites actuels et voisins, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).<!--SCCMDocs issue 685-->  

Le client Configuration Manager utilise le cache de pair pour délivrer aux clients chaque type de contenu du cache. Ce contenu comprend des fichiers Office 365 et des fichiers d’installation de la version Express.<!--SMS.500850-->  

Le cache de pair ne remplace pas l’utilisation d’autres solutions, comme Windows BranchCache ou Optimisation de livraison. Le cache de pair fonctionne avec d’autres solutions. Ces technologies vous offrent plus d’options pour étendre les solutions traditionnelles de déploiement de contenu, comme les points de distribution. Le cache de pair est une solution personnalisée qui ne dépend pas de BranchCache. Il fonctionne même sans activer ou utiliser BranchCache.  

  > [!Note]  
  > À compter de la version 1802, Windows BranchCache est toujours activé sur les déploiements. Le paramètre **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau** est supprimé.<!--SCCMDocs issue 539--> Si c’est pris en charge par le point de distribution et activé dans les paramètres clients, les clients utilisent BranchCache. Pour plus d'informations, consultez [Configurer BranchCache](/sccm/core/clients/deploy/about-client-settings#configure-branchcache).<!--SCCMDocs issue 735-->   



## <a name="operations"></a>Opérations

Pour activer le cache de pair, déployez les [paramètres clients](#bkmk_settings) sur un regroupement. Les membres de ce regroupement se comportent ensuite comme une source de cache de pair pour les autres clients du même groupe de limites.  

 -  Un client qui agit en tant que source de contenu homologue envoie une liste des contenus mis en cache disponibles à son point de gestion.  

 -  Un autre client du même groupe de limites effectue une demande d’emplacement du contenu au point de gestion. Le serveur retourne la liste des sources de contenu potentielles. Cette liste inclut chaque source de cache de pair qui a ce contenu et qui est en ligne. Elle inclut également les points de distribution et d’autres emplacements de source de contenu dans ce groupe de limites. Pour plus d’informations, consultez [Priorités des sources de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).  

 -  Comme à chaque fois, le client qui demande le contenu sélectionne une source dans la liste fournie. Le client essaie ensuite d’obtenir le contenu.  

À compter de la version 1806, les groupes de limites intègrent des paramètres supplémentaires qui offrent davantage de contrôle sur la distribution du contenu dans l’environnement. Pour plus d’informations, voir [Options de groupe de limites pour les téléchargements de pairs](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).<!--1356193-->

> [!NOTE]  
> Si le client a recours à un groupe de limites voisin pour le contenu, le point de gestion n’ajoute pas les emplacements sources de cache de pair du groupe de limites voisin à la liste des emplacements de sources de contenu potentielles.  

Choisissez seulement les clients les plus appropriés comme sources de cache de pair. Évaluez l’adéquation des clients en fonction d’attributs comme le type de châssis, l’espace disque et la connectivité réseau. Pour plus d’informations vous permettant de sélectionner les meilleurs clients à utiliser pour le cache de pair, consultez [ce blog d’un consultant Microsoft](https://blogs.technet.microsoft.com/askpfeplat/2018/11/21/configuration-manager-peer-cache-custom-reporting-examples/).


### <a name="limited-access-to-a-peer-cache-source"></a>Accès limité à une source de cache de pair  

Une source de cache de pair rejette les demandes de contenu quand elle remplit une des conditions suivantes au moment où un pair demande du contenu :  

  -  Mode de batterie faible  

  -  Charge du processeur dépassant 80 %  

  -  E/S disque avec une valeur de *AvgDiskQueueLength* supérieure à 10  

  -  Plus de connexion disponible vers l’ordinateur  

> [!Tip]  
> Configurez ces paramètres à l’aide de la classe WMI du serveur de configuration du client pour la fonctionnalité de source d’homologue (*SMS_WinPEPeerCacheConfig*) dans le SDK System Center.  

Quand la source de cache de pair rejette une demande de contenu, le client du cache de pair continue de rechercher le contenu dans sa liste des emplacements de sources de contenu.   



## <a name="requirements"></a>spécifications

- Le cache de pair prend en charge toutes les versions de Windows listées dans [Systèmes d’exploitation pris en charge pour les clients et les appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Les systèmes d’exploitation non-Windows ne sont pas pris en charge comme sources de cache de pair ou comme clients de cache de pair.  

- Une source de cache de pair doit être un client Configuration Manager joint au domaine. Cependant, un client qui n’est pas joint à un domaine peut obtenir du contenu auprès d’une source de cache de pair jointe à un domaine.  

- Les clients peuvent télécharger du contenu seulement à partir de sources de cache de pair qui se trouvent dans leur groupe de limites actuel.  

- Un [compte d’accès réseau](/sccm/core/plan-design/hierarchy/accounts#network-access-account) n’est pas nécessaire, à cette exception près :  

    - Configurez un compte d’accès réseau dans le site quand un client autorisé à utiliser le cache de pair exécute une séquence de tâches depuis le Centre logiciel, et qu’il redémarre à partir d’une image de démarrage. Quand l’appareil est sur Windows PE, il utilise le compte d’accès réseau pour obtenir du contenu auprès de la source de cache de pair.  

    - Quand c’est nécessaire, la source de cache de pair utilise le compte d’accès réseau pour authentifier les demandes de téléchargement provenant des pairs. Pour cela, ce compte a seulement besoin des autorisations d’utilisateur de domaine.  

- Dans la version 1802 et les versions antérieures, le dernier envoi de la découverte de pulsation du client détermine la limite actuelle d’une source de cache de pair. Un client qui passe à un groupe de limites différent peut toujours être membre de son groupe de limites précédent pour ce qui concerne le cache de pair. Ce comportement fait qu’un client peut se voir proposer une source de cache de pair qui ne se trouve pas à proximité immédiate de son emplacement réseau. N’autorisez pas des clients itinérants à être des sources de cache de pair.<!--SCCMDocs issue 641-->  

    > [!Important]  
    > À compter de la version 1806, Configuration Manager détermine plus efficacement si une source de cache de pair s’est déplacée vers un autre emplacement. Ce comportement garantit que le point de gestion la propose comme source de contenu aux clients dans le nouvel emplacement, et non dans l’ancien. Si vous utilisez la fonctionnalité de cache de pair avec des sources de cache de pair itinérantes, après avoir mis à jour le site vers la version 1806, vous devez également mettre à jour toutes les sources de cache de pair vers la dernière version du client. Le point de gestion n’inclut pas ces sources de cache de pair dans la liste des emplacements de contenu tant qu’elles n’ont pas été mises à jour vers la version 1806 (minimum).<!--SCCMDocs issue 850-->  

- Avant de tenter de télécharger du contenu, le point de gestion vérifie d’abord que la source de cache de pair est en ligne.<!--sms.498675--> Cette vérification est faite via le « canal rapide » pour la notification des clients, qui utilise le port TCP 10123.<!--511673-->  

> [!Note]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités apparaissent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version des clients n’est pas également la plus récente.  



## <a name="bkmk_settings"></a> Paramètres de cache de pair des clients

Pour plus d’informations sur la configuration des paramètres de cache de pair des clients, consultez [Paramètres du cache des clients](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). 

Pour plus d’informations sur la configuration de ces paramètres, consultez [Guide pratique pour configurer les paramètres des clients](/sccm/core/clients/deploy/configure-client-settings).

Sur les clients autorisés à utiliser le cache de pair et qui utilisent le pare-feu Windows, Configuration Manager configure les ports du pare-feu que vous spécifiez dans les paramètres des clients.



## <a name="bkmk_parts"></a> Prise en charge du téléchargement partiel
<!--1357346-->
À compter de la version 1806, les sources de cache de pair des clients peuvent diviser le contenu en plusieurs parties. Ces parties diminuent le transfert de réseau afin de réduire l’utilisation du réseau WAN. Le point de gestion fournit un suivi plus détaillé des parties du contenu. Il essaie de supprimer plusieurs téléchargements du même contenu par groupe de limites. 


### <a name="example-scenario"></a>Exemple de scénario

Contoso a un seul site principal avec deux groupes de limites : Un siège social et une filiale. Il existe une relation de secours de 30 minutes entre les groupes de limites. Le point de gestion et le point de distribution du site se trouvent uniquement dans la limite du siège social. L’emplacement de la filiale n’a aucun point de distribution local. Deux des quatre clients au niveau de la filiale sont configurés comme sources de cache d’homologue. 

![Schéma de la configuration réseau comme décrite pour l’exemple de scénario](media/1357346-peer-cache-source-parts.png)

1. Vous ciblez un déploiement avec du contenu sur les quatre clients de la filiale. Vous avez distribué du contenu uniquement au point de distribution.  

2. Client3 et Client4 n’ont pas de source locale pour le déploiement. Le point de gestion indique aux clients de patienter 30 minutes avant de revenir au groupe de limites distantes.  

3. Client1 (PCS1) est la première source de cache d’homologue pour actualiser la stratégie avec le point de gestion. Étant donné que ce client est activé comme source de cache d’homologue, le point de gestion lui indique de commencer immédiatement le téléchargement de la partie A à partir du point de distribution.  

4. Quand Client2 (PCS2) contacte le point de gestion, comme la partie A est déjà en cours mais pas encore terminée, le point de gestion lui indique de commencer immédiatement le téléchargement de la partie B à partir du point de distribution.  

5. PCS1 termine le téléchargement de la partie A et en avertit immédiatement le point de gestion. Comme la partie B est déjà en cours mais pas encore terminée, le point de gestion lui indique de commencer le téléchargement de la partie C à partir du point de distribution.  

6. PCS2 termine le téléchargement de la partie B et en avertit immédiatement le point de gestion. Le point de gestion lui indique de commencer le téléchargement de la partie D à partir du point de distribution.  

7. PCS1 termine le téléchargement de la partie C et en avertit immédiatement le point de gestion. Le point de gestion l’informe qu’aucune autre partie n’est disponible à partir du point de distribution distant. Le point de gestion lui indique de télécharger la partie B à partir de son homologue local, PCS2.  

8. Ce processus se poursuit jusqu’à ce que les deux sources de cache d’homologue client aient toutes les parties de l’une et de l’autre. Le point de gestion établit la priorité des parties à partir du point de distribution distant avant d’indiquer aux sources de cache d’homologue de télécharger des parties à partir des homologues locaux.  

9. Client3 est le premier à actualiser la stratégie au terme de la période de repli de 30 minutes. Il vérifie de nouveau auprès du point de gestion, qui indique au client des nouvelles sources locales. Au lieu de télécharger le contenu en totalité à partir du point de distribution sur le réseau WAN, il télécharge le contenu en totalité à partir de l’une des sources de cache d’homologue client. Les clients établissent la priorité des sources d’homologue local. 

> [!Note]  
> Si le nombre de sources de cache d’homologue client est supérieur au nombre de parties du contenu, le point de gestion indique aux sources de cache d’homologue supplémentaires d’attendre une action de repli comme un client normal. 


### <a name="configure-partial-download"></a>Configurer le téléchargement partiel

1. Configurez normalement des [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups) et des sources de cache de pair.  

2. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**. Cliquez sur **Paramètres de hiérarchie** dans le ruban.  

3. Sous l’onglet **Général**, activez l’option permettant de **configurer les sources de cache d’homologue client pour diviser du contenu en parties**.  

4. Créez un déploiement obligatoire avec du contenu.  

   > [!Note]  
   > Cette fonctionnalité fonctionne uniquement quand le client télécharge le contenu en arrière-plan, comme avec un déploiement obligatoire. Les téléchargements à la demande, comme quand l’utilisateur installe un déploiement disponible dans le Centre logiciel, se comportent comme d’habitude.  

Pour les voir gérer le téléchargement du contenu en parties, examinez le fichier **ContentTransferManager.log** sur la source de cache d’homologue client et le fichier **MP_Location.log** sur le point de gestion.  



## <a name="guidance-for-cache-management"></a>Conseils pour la gestion du cache
<!--510645-->
Le cache de pair s’appuie sur le cache du client Configuration Manager pour partager du contenu. Considérez les points suivants pour gérer le cache client dans votre environnement :  

- Le cache du client Configuration Manager n’est pas semblable à la bibliothèque de contenu sur un point de distribution. Alors que vous gérez le contenu que vous distribuez à un point de distribution, le client Configuration Manager gère quant à lui automatiquement le contenu dans son cache. Des paramètres et des méthodes existent pour vous permettre de contrôler le contenu qui se trouve dans le cache d’une source de cache de pair. Pour plus d’informations, consultez [Configurer le cache du client pour les clients Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

- Vous pouvez appliquer une taille de cache et une maintenance normales aux sources de cache de pair. Pour plus d’informations, consultez [Configurer la taille du cache des clients](/sccm/core/clients/deploy/about-client-settings#configure-client-cache-size). Prenez en compte la taille des contenus plus grands, comme les packages de mise à niveau des systèmes d’exploitation ou les fichiers de mise à jour rapide de Windows 10. Comparez vos besoins pour ce contenu avec l’espace disque disponible sur les sources de cache de pair.  

- Le client de source de cache de pair met à jour la dernière date/heure référencée du contenu dans le cache quand un pair le télécharge. Le client utilise cet horodatage quand il gère automatiquement son cache, supprimant d’abord le contenu plus ancien. Ainsi, il doit normalement attendre si possible avant de supprimer du contenu que les clients de cache de pair téléchargent plus fréquemment.  

- Si nécessaire, pendant une séquence de tâches de déploiement de système d’exploitation, utilisez la variable **SMSTSPreserveContent** pour conserver du contenu dans le cache du client. Pour plus d’informations, voir [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSPreserveContent).  

- Si nécessaire, lors de la création des types de logiciels suivants, utilisez l’option permettant de **conserver le contenu dans la mémoire cache du client** :  
    - Applications
    - Packages
    - Images de système d’exploitation
    - Packages de mise à niveau de système d’exploitation
    - Images de démarrage



## <a name="monitoring"></a>Analyse   

Pour mieux comprendre l’utilisation du cache de pair, consultez le tableau de bord **Sources de données des clients**. Pour plus d’informations, consultez le [tableau de bord Sources de données des clients](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

Utilisez également les rapports pour voir l’utilisation des caches de pair. Dans la console, accédez à l’espace de travail **Surveillance**, développez **Rapports**, puis sélectionnez **Rapports**. Tous les rapports suivants sont du type **Contenu de distribution de logiciels** :  

1.  **Rejet du contenu de la source de cache d’homologue** : Fréquence à laquelle les sources de cache de pair d’un groupe de limites rejettent une demande de contenu.  

    > [!Note]  
    > **Problème connu**<!--486652-->: Quand vous explorez les détails des résultats comme *MaxCPULoad* ou *MaxDiskIO*, il se peut que vous receviez une erreur qui indique que le rapport ou les détails sont introuvables. Pour contourner ce problème, utilisez les deux autres rapports qui montrent directement les résultats.  

2. **Rejet conditionnel du contenu de la source de cache d’homologue** : Affichage des détails du rejet pour un groupe de limites ou un type de rejet donné. 

    > [!Note]  
    > **Problème connu**<!--486652-->: Vous ne pouvez pas choisir parmi les paramètres disponibles ; à la place, vous devez les entrer manuellement. Entrez les valeurs pour *Nom de groupe de limites* et *Type de rejet* telles qu’elles apparaissent dans le rapport **Rejet du contenu par une source de cache de pair**. Par exemple, pour *Type de rejet*, vous pouvez entrer *MaxCPULoad* ou *MaxDiskIO*.  

3. **Détails du rejet du contenu de la source de cache d’homologue** : Affichage du contenu demandé par le client au moment du rejet.  

    > [!Note]  
    > **Problème connu**<!--486652-->: Vous ne pouvez pas choisir parmi les paramètres disponibles ; à la place, vous devez les entrer manuellement. Entrez la valeur pour *Type de rejet* telle qu’elle apparaît dans le rapport **Rejet du contenu par une source de cache d’homologue**. Entrez ensuite *l’ID de ressource* pour la source de contenu sur laquelle vous voulez plus d’informations. 
    > 
    > Pour trouver l’ID de ressource de la source de contenu :  
    > 
    > 1. Recherchez le nom de l’ordinateur qui s’affiche comme *Source de cache d’homologue* dans les résultats du rapport **Rejet conditionnel du contenu de la source de cache d’homologue**.  
    > 
    > 2. Accédez à l’espace de travail **Ressources et Conformité**, sélectionnez le nœud **Appareils** et recherchez le nom de cet ordinateur. Utilisez la valeur de la colonne ID de ressource.  

