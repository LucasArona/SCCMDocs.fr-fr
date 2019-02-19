---
title: Planifier les mises à jour logicielles
titleSuffix: Configuration Manager
description: Il est essentiel de planifier l’infrastructure du point de mise à jour logicielle avant d’utiliser les mises à jour logicielles dans un environnement de production Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.collection: M365-identity-device-management
ms.openlocfilehash: 730d99764f8ae8f8ce1b76bfd13411988c3a2e23
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138538"
---
# <a name="plan-for-software-updates-in-configuration-manager"></a>Planifier les mises à jour logicielles dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’utiliser les mises à jour logicielles dans un environnement de production Configuration Manager, vous devez parcourir le processus de planification. Une bonne planification de l’infrastructure du point de mise à jour logicielle est la clé d’une implémentation réussie des mises à jour logicielles.



## <a name="capacity-planning-recommendations-for-software-updates"></a>Recommandations pour la planification de la capacité pour les mises à jour logicielles  

Cette section inclut les sous-rubriques suivantes :  
- [Planification de la capacité du point de mise à jour logicielle](#BKMK_SUMCapacity)
- [Planification de la capacité pour les objets des mises à jour logicielles](#bkmk_sum-capacity-obj)  


Utilisez les recommandations suivantes comme ligne de base. Celle-ci vous aide à déterminer les informations de planification de capacité des mises à jour logicielles convenant à votre organisation. Les besoins en capacité réels peuvent varier par rapport aux recommandations répertoriées dans cet article en fonction des critères suivants : 
- Votre environnement réseau spécifique
- Le matériel que vous utilisez pour héberger le système de site du point de mise à jour logicielle
- Le nombre de clients gérés
- Les autres rôles de système de site installés sur le serveur  


###  <a name="BKMK_SUMCapacity"></a> Planification de la capacité du point de mise à jour logicielle  

Le nombre de clients pris en charge dépend de la version de Windows Server Update Services (WSUS) qui s’exécute sur le point de mise à jour logicielle. Il varie également selon que le rôle de système de site du point de mise à jour logicielle coexiste ou non avec un autre rôle de système de site :  

-   Le point de mise à jour logicielle peut prendre en charge jusqu’à 25 000 clients quand WSUS s’exécute sur le serveur du point de mise à jour logicielle et que le point de mise à jour logicielle coexiste avec un autre rôle de système de site.  

-   Le point de mise à jour logicielle peut prendre en charge jusqu’à 150 000 clients quand un serveur distant satisfait à la configuration requise de WSUS, que WSUS est utilisé avec Configuration Manager et que vous configurez les paramètres suivants :

    Pools d’applications IIS :
    - Augmenter la longueur de file d’attente WsusPool à 2000
    - Multiplier par quatre la limite de mémoire privée WsusPool, ou lui affecter la valeur 0 (illimitée). Par exemple, si la limite par défaut est 1 843 200 Ko, l’augmenter à 7 372 800. Pour plus d’informations, consultez ce [billet de blog de l’équipe de support Configuration Manager](https://blogs.technet.microsoft.com/configurationmgr/2015/03/23/configmgr-2012-support-tip-wsus-sync-fails-with-http-503-errors/).  

    Pour plus d’informations sur la configuration matérielle requise pour le point de mise à jour logicielle, consultez [Matériel recommandé pour les systèmes de site](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).  


### <a name="bkmk_sum-capacity-obj"></a> Planification de la capacité pour les objets des mises à jour logicielles  

Utilisez les informations de capacité suivantes pour planifier les objets des mises à jour logicielles :  

#### <a name="limit-of-1000-software-updates-in-a-deployment"></a>Limite de 1 000 mises à jour logicielles dans un déploiement  
Limitez le nombre de mises à jour logicielles à 1 000 pour chaque déploiement de mises à jour logicielles. Quand vous créez une règle de déploiement automatique, spécifiez des critères qui limitent le nombre de mises à jour logicielles. La règle de déploiement automatique échoue quand les critères spécifiés retournent plus de 1 000 mises à jour logicielles. Vérifiez l’état de la règle de déploiement automatique à partir du nœud **Règles de déploiement automatique** dans la console Configuration Manager. Quand vous déployez manuellement des mises à jour logicielles, ne sélectionnez pas plus de 1 000 mises à jour à déployer.  

Limitez également le nombre de mises à jour logicielles à 1 000 dans une base de référence de configuration. Pour plus d’informations, consultez [Créer des bases de référence de configuration](/sccm/compliance/deploy-use/create-configuration-baselines).



##  <a name="BKMK_SUPInfrastructure"></a> Déterminer l’infrastructure du point de mise à jour logicielle  

Cette section inclut les sous-rubriques suivantes :    
- [Liste des points de mise à jour logicielle](#BKMK_SUPList)
- [Basculement de point de mise à jour logicielle](#BKMK_SUPSwitching)
- [Basculer manuellement les clients vers un nouveau point de mise à jour logicielle](#BKMK_ManuallySwitchSUPs)
- [Points de mise à jour logicielle dans une forêt non approuvée](#BKMK_SUP_CrossForest)
- [Utiliser un serveur WSUS existant comme source de synchronisation sur le site de niveau supérieur](#BKMK_WSUSSyncSource)
- [Point de mise à jour logicielle sur un site secondaire](#BKMK_SUPSecSite)  
- [Planifier les clients basés sur Internet](#bkmk_internet-clients)  
- [Planifier le contenu de la mise à jour logicielle](#bkmk_content)  
- [Planifier les mises à jour tierces](#bkmk_thirdparty)  


Le site d’administration centrale et tous les sites principaux enfants doivent disposer d’un point de mise à jour logicielle. Pendant la planification de l’infrastructure du point de mise à jour logicielle, déterminez les dépendances suivantes :
 - Emplacement d’installation du point de sauvegarde logicielle du site  
 - Sites nécessitant un point de mise à jour logicielle qui accepte les communications provenant de clients basés sur Internet
 - Nécessité ou non d’installer un point de mise à jour logicielle sur des sites secondaires  

> [!IMPORTANT]  
>  Pour plus d’informations sur les dépendances internes et externes nécessaires pour les mises à jour logicielles, consultez [Prérequis pour les mises à jour logicielles](prerequisites-for-software-updates.md).  

Ajoutez plusieurs points de mise à jour logicielle sur un site principal Configuration Manager pour fournir la tolérance de panne. La conception du basculement du point de mise à jour logicielle est différente de celle du modèle de randomisation pur utilisé dans la conception des points de gestion. Contrairement à la conception des points de gestion, il existe des coûts en termes de performances du client et du réseau liés à la conception des points de mise à jour logicielle quand les clients basculent vers un nouveau point de mise à jour logicielle. Lorsque le client bascule vers un nouveau serveur WSUS pour rechercher des mises à jour logicielles, la taille du catalogue augmente, tout comme les exigences de performance réseau et côté client associées. Ainsi, le client conserve l’affinité avec le dernier point de mise à jour logicielle à partir duquel il a correctement analysé.  

Le premier point de mise à jour logicielle que vous installez sur un site principal est la source de synchronisation de tous les points de mise à jour logicielle supplémentaires que vous ajoutez sur le site principal. Une fois que vous avez ajouté les points de mise à jour logicielle et démarré la synchronisation, affichez l’état des points de mise à jour logicielle et la source de synchronisation depuis le nœud **État de la synchronisation du point de mise à jour logicielle** dans l’espace de travail **Surveillance**.  

En cas de défaillance du point de mise à jour logicielle configuré en tant que source de synchronisation pour le site, supprimez manuellement le rôle défaillant. Ensuite, sélectionnez un nouveau point de mise à jour logicielle à utiliser en guise de source de synchronisation. Pour plus d’informations, consultez [Supprimer le rôle de système de site du point de mise à jour logicielle](../get-started/remove-a-software-update-point.md).  


###  <a name="BKMK_SUPList"></a> Liste des points de mise à jour logicielle  

Configuration Manager fournit au client la liste des points de mise à jour logicielle dans les scénarios suivants :  

- Un nouveau client reçoit la stratégie pour activer les mises à jour logicielles  

- Un client ne peut pas contacter son point de mise à jour logicielle attribué et doit basculer vers un autre  

Le client sélectionne au hasard un point de mise à jour logicielle dans la liste. Il privilégie les points de mise à jour logicielle de la même forêt. Configuration Manager fournit aux clients une liste différente selon le type de client :  

-   **Clients basés sur intranet** : reçoivent la liste des points de mise à jour logicielle que vous pouvez configurer pour autoriser les connexions uniquement depuis l’intranet, ou la liste des points de mise à jour logicielle qui autorisent les connexions client Internet et intranet.  

-   **Clients basés sur Internet** : reçoivent la liste des points de mise à jour logicielle que vous pouvez configurer pour autoriser les connexions uniquement depuis Internet, ou la liste des points de mise à jour logicielle qui autorisent les connexions client Internet et intranet.  


###  <a name="BKMK_SUPSwitching"></a> Basculement de point de mise à jour logicielle  

> [!NOTE]  
> Les clients utilisent des groupes de limites pour rechercher un nouveau point de mise à jour logicielle. Si leur point de mise à jour logicielle actuel n’est plus accessible, ils utilisent également des groupes de limites pour en rechercher un nouveau. Ajoutez des points de mise à jour logicielle individuels à différents groupes de limites pour contrôler les serveurs qu’un client peut trouver. Pour plus d’informations, consultez [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  

Si vous avez plusieurs points de mise à jour logicielle sur un site, et que l’un d’eux est en échec ou indisponible, les clients se connectent à un point de mise à jour logicielle différent. Avec ce nouveau serveur, les clients continuent de rechercher les dernières mises à jour logicielle. Quand un client est affecté à un point de mise à jour logicielle, il le reste sauf s’il ne parvient pas à effectuer l’analyse.  

La recherche des mises à jour logicielles peut échouer avec plusieurs codes de nouvelle tentative et de non-nouvelle tentative différents. Lorsque l'analyse échoue avec un code d'erreur de nouvelle tentative, le client démarre un processus de nouvelle tentative pour rechercher les mises à jour logicielles sur le point de mise à jour logicielle. Les conditions précises qui génèrent un code d'erreur de nouvelle tentative sont généralement dues à l'indisponibilité ou à la surcharge temporaire du serveur WSUS. Quand le client ne parvient pas à rechercher les mises à jour logicielles, il utilise le processus suivant :  

1.  Le client recherche les mises à jour logicielles :  
    - À l’heure planifiée
    - Quand il est exécuté manuellement à partir du Panneau de configuration sur le client
    - Quand il est exécuté manuellement à partir de la console Configuration Manager par le biais d’une action de notification du client
    - Quand il est exécuté à partir d’une méthode SDK Configuration Manager  

2.  Si l’analyse échoue, le client attend 30 minutes avant de la relancer. Il utilise le même point de mise à jour logicielle.  

3.  Le client effectue au moins quatre nouvelles tentatives toutes les 30 minutes. Après le quatrième échec, il attend deux minutes supplémentaires, puis il passe au point de mise à jour logicielle suivant dans sa liste.  

4.  Le client répète ce processus avec le nouveau point de mise à jour logicielle. Après une analyse réussie, le client continue à se connecter au nouveau point de mise à jour logicielle.  

La liste suivante fournit des informations supplémentaires à consulter en cas de nouvelle tentative et de basculement des points de mise à jour logicielle :  

-   Si un client est déconnecté de l’intranet et qu’il ne parvient pas à rechercher des mises à jour logicielles, il ne bascule pas vers un autre point de mise à jour logicielle. Cet échec est attendu, car le client ne peut pas atteindre le réseau interne ou un point de mise à jour logicielle qui permet les connexions depuis l’intranet. Le client Configuration Manager détermine la disponibilité du point de mise à jour logicielle intranet.  

-   Si vous gérez les clients sur Internet et avez configuré plusieurs points de mise à jour logicielle pour accepter les communications provenant des clients sur Internet, le processus de basculement suit le processus de nouvelle tentative standard décrit précédemment.  

-   Si le processus d’analyse démarre, alors que le client est éteint avant la fin de l’analyse, cela n’est pas considéré comme un échec d’analyse et cela n’est pas comptabilisé dans les quatre nouvelles tentatives.  

Quand Configuration Manager reçoit un des codes d’erreur suivants de l’Agent Windows Update, le client retente d’établir la connexion :  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Pour rechercher la signification d’un code d’erreur, convertissez le code d’erreur décimal au format hexadécimal, puis recherchez la valeur hexadécimale sur un site tel que le [wiki des codes d’erreur de l’Agent Windows Update](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx). Par exemple, le code d’erreur décimal 2149842970 est la valeur hexadécimale 8024001A, qui signifie WU_E_POLICY_NOT_SET Une valeur de stratégie n’a pas été définie.  


###  <a name="BKMK_ManuallySwitchSUPs"></a> Basculer manuellement les clients vers un nouveau point de mise à jour logicielle

Basculez les clients Configuration Manager vers un autre point de mise à jour logicielle quand ils rencontrent des problèmes avec le point de mise à jour logicielle actif. Ce changement se produit uniquement quand un client reçoit plusieurs points de mise à jour logicielle à partir d’un point de gestion.

> [!IMPORTANT]    
> Quand vous basculez des appareils pour utiliser un nouveau serveur, les appareils utilisent une action de secours pour rechercher ce serveur. Avant de procéder à ce changement, passez en revue vos configurations de groupe de limites pour vérifier que vos points de mise à jour logicielle sont dans les groupes de limites appropriés. Pour plus d’informations, consultez [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).  
>
> Le basculement vers un nouveau point de mise à jour logicielle génère du trafic réseau supplémentaire. La quantité de trafic varie selon vos paramètres de configuration WSUS, par exemple, les classifications et produits synchronisés ou l’utilisation d’une base de données WSUS partagée. Si vous envisagez de basculer plusieurs appareils, faites-le pendant les fenêtres de maintenance. Vous réduisez ainsi l’impact sur votre réseau quand les clients analysent avec le nouveau point de mise à jour logicielle.  

#### <a name="process-to-switch-software-update-points"></a>Processus de basculement vers des points de mise à jour logicielle  
Procédez à ce changement sur un regroupement d’appareils. Une fois l’action déclenchée, les clients recherchent un autre point de mise à jour logicielle pendant la prochaine analyse.  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, puis sélectionnez le nœud **Regroupements d’appareils**.  

2.  Sélectionnez le regroupement cible. Sous l’onglet **Accueil** du ruban, dans le groupe **Regroupement**, cliquez sur **Notification du client**, puis sur **Passer au point de mise à jour logicielle suivant**.  


###  <a name="BKMK_SUP_CrossForest"></a> Points de mise à jour logicielle dans une forêt non approuvée  

Créez un ou plusieurs points de mise à jour logicielle sur un site pour prendre en charge des clients dans une forêt non approuvée. Pour ajouter un point de mise à jour logicielle dans une autre forêt, installez et configurez d’abord un serveur WSUS dans cette forêt. Démarrez ensuite l’Assistant pour ajouter un serveur de site Configuration Manager doté du rôle de système de site du point de mise à jour logicielle. Dans l'Assistant, configurez les paramètres suivants pour vous connecter correctement au serveur WSUS dans la forêt non approuvée :  

-   Spécifiez un **compte d’installation du système de site** capable d’accéder au serveur WSUS dans la forêt non approuvée.  

-   Spécifiez un **compte de connexion du serveur WSUS** pour vous connecter au serveur WSUS.  

Par exemple, vous avez un site principal dans la forêt A doté de deux points de mise à jour logicielle (SUP01 et SUP02). Pour ce même site principal, vous avez également deux points de mise à jour logicielle (SUP03 et SUP04) dans la forêt B. Au moment du basculement vers le point de mise à jour logicielle suivant, les clients privilégient les serveurs de la même forêt.  


###  <a name="BKMK_WSUSSyncSource"></a> Utiliser un serveur WSUS existant comme source de synchronisation sur le site de niveau supérieur  

En règle générale, le site de niveau supérieur dans votre hiérarchie est configuré pour synchroniser les métadonnées des mises à jour logicielles avec Microsoft Update. Quand votre stratégie de sécurité de l’organisation n’autorise pas le site de niveau supérieur à accéder à Internet, configurez la source de synchronisation pour le site de niveau supérieur de sorte à utiliser un serveur WSUS existant. Ce serveur WSUS ne fait pas partie de votre hiérarchie Configuration Manager. Par exemple, vous disposez d’un serveur WSUS dans un réseau connecté à Internet (réseau de périmètre), mais votre site de niveau supérieur se trouve dans un réseau interne sans accès à Internet. Configurez le serveur WSUS dans le réseau de périmètre en tant que source de synchronisation pour les métadonnées des mises à jour logicielles. Configurez le serveur WSUS dans le réseau de périmètre pour synchroniser les mises à jour logicielles avec les mêmes critères que ceux dont vous avez besoin dans Configuration Manager. Sinon, le site de niveau supérieur risque de ne pas synchroniser les mises à jour logicielles attendues. Quand vous installez le point de mise à jour logicielle, configurez un compte de connexion du serveur WSUS. Ce compte a besoin d’accéder au serveur WSUS dans le réseau de périmètre. Vérifiez également que le pare-feu autorise le trafic pour les ports appropriés. Pour plus d’informations, consultez les [ports utilisés par le point de mise à jour logicielle vers la source de synchronisation](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsSUP-WSUS).  


###  <a name="BKMK_SUPSecSite"></a> Point de mise à jour logicielle sur un site secondaire  

Le point de mise à jour logicielle est facultatif sur un site secondaire. Installez un seul point de mise à jour logicielle sur un site secondaire. Quand un point de mise à jour logicielle n’est pas installé sur le site secondaire, les appareils à l’intérieur des limites de ce site utilisent un point de mise à jour logicielle sur leur site principal attribué. En général, vous installez un point de mise à jour logicielle sur un site secondaire quand la bande passante réseau est limitée entre les appareils sur le site secondaire et les points de mise à jour logicielle sur le site principal parent. Vous pouvez également utiliser cette configuration quand le point de mise à jour logicielle sur le site principal est proche de la limite de capacité. Une fois que vous avez correctement installé et configuré un point de mise à jour logicielle sur le site secondaire, une stratégie à l’échelle du site est mise à jour pour les clients, qui commencent alors à utiliser le nouveau point de mise à jour logicielle.  


### <a name="bkmk_internet-clients"></a> Planifier les clients basés sur Internet

Quand vous avez besoin de gérer des appareils qui gagnent Internet depuis votre réseau, développez un plan pour gérer les mises à jour logicielles sur ces appareils. Configuration Manager prend en charge plusieurs technologies pour ce scénario. Utilisez-en une ou plusieurs, selon les exigences de votre organisation.

#### <a name="cloud-management-gateway"></a>Passerelle de gestion cloud
Créez une passerelle de gestion cloud dans Microsoft Azure et activez au moins un point de mise à jour logicielle local pour autoriser le trafic à partir des clients basés sur Internet. Quand les clients gagnent Internet, ils continuent à analyser par rapport à vos points de mise à jour logicielle. Tous les clients basés sur Internet obtiennent toujours le contenu auprès du service cloud Microsoft Update. 

Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="internet-based-client-management"></a>Gestion des clients basés sur Internet
Placez un point de mise à jour logicielle dans un réseau accessible sur Internet et activez-le pour autoriser le trafic à partir des clients basés sur Internet. Quand les clients gagnent Internet, ils basculent vers ce point de mise à jour logicielle à des fins d’analyse. Tous les clients basés sur Internet obtiennent toujours le contenu auprès du service cloud Microsoft Update.

Pour plus d’informations sur les avantages et inconvénients de la gestion des clients basés sur Internet, consultez [Gérer les clients sur Internet](/sccm/core/clients/manage/manage-clients-internet).

#### <a name="windows-update-for-business"></a>Windows Update for Business
Windows Update pour Entreprise vous permet de maintenir les appareils Windows 10 à jour en permanence avec les dernières mises à jour des fonctionnalités et qualité. Ces appareils se connectent directement au service cloud Windows Update. Configuration Manager peut faire la distinction entre les ordinateurs Windows 10 qui utilisent WUfB et WSUS pour obtenir les mises à jour logicielles.

Pour plus d’informations, consultez [Intégration à Windows Update pour Entreprise](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).


### <a name="bkmk_content"></a> Planifier le contenu de la mise à jour logicielle

Les clients doivent télécharger les fichiers de contenu pour les mises à jour logicielles afin de les installer. Configuration Manager fournit plusieurs technologies pour prendre en charge la gestion et la distribution de ce contenu. Si vous préférez, vous pouvez configurer des déploiements de mises à jour logicielles pour autoriser ou obliger les clients à obtenir du contenu directement auprès du service cloud Microsoft Update.

#### <a name="download-and-distribute-content"></a>Télécharger et distribuer du contenu 
Par défaut, le processus de gestion des mises à jour logicielles dans Configuration Manager utilise les fonctionnalités de gestion de contenu intégrées. Ces fonctionnalités incluent la bibliothèque de contenu de store centralisée à instance unique et la conception distribuée du rôle de système de site du point de distribution. Vous utilisez ces fonctionnalités quand vous téléchargez et distribuez des packages de déploiement de mises à jour logicielles. 

Pour plus d’informations, consultez [Télécharger les mises à jour logicielles](/sccm/sum/deploy-use/download-software-updates).

#### <a name="manage-express-installation-files-for-windows-10"></a>Gérer les fichiers d’installation rapide pour Windows 10
Configuration Manager prend en charge l’utilisation de fichiers d’installation rapide pour les mises à jour de Windows 10. Les fichiers de mise à jour rapide et les technologies de prise en charge telles que l’optimisation de la distribution peuvent aider à réduire l’impact sur le réseau du téléchargement de grands fichiers de contenu sur les clients. 

Pour plus d’informations, consultez [Optimiser la distribution de Windows Update pour Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).

#### <a name="clients-download-content-from-the-internet"></a>Les clients téléchargent le contenu à partir d’Internet
Quand vous déployez des mises à jour logicielles sur les clients, configurez le déploiement de manière à ce que les clients téléchargent le contenu à partir du service cloud Microsoft Update. Quand les clients ne sont pas en mesure de télécharger le contenu à partir d’une autre source de contenu, ils peuvent toujours le télécharger à partir d’Internet. 

Depuis la version 1806, vous n’êtes pas obligé de créer un package de déploiement quand vous déployez des mises à jour logicielles. Quand vous sélectionnez l’option **Aucun package de déploiement**, les clients peuvent toujours télécharger le contenu à partir de sources locales éventuelles, mais ils effectuent généralement le téléchargement à partir du service Microsoft Update.<!--1357933-->

Les clients basés sur Internet téléchargent toujours le contenu à partir du service cloud Microsoft Update. Ne distribuez pas les packages de déploiement de mises à jour logicielles sur un point de distribution cloud. Vous êtes facturé pour le stockage avec le point de distribution cloud, mais les clients ne téléchargent pas ces packages. 


### <a name="bkmk_thirdparty"></a> Planifier les mises à jour tierces
Configuration Manager s’intègre à WSUS, qui prend en charge en mode natif les mises à jour logicielles publiées par Microsoft. La plupart des clients utilisent d’autres applications tierces qui ont également besoin de mises à jour. Il existe plusieurs options à prendre en compte concernant la façon de maintenir les applications tierces à jour.

#### <a name="supersede-applications-to-update"></a>Remplacer les applications à mettre à jour
Utilisez une relation de remplacement avec la fonctionnalité de gestion d’applications dans Configuration Manager pour mettre à niveau ou remplacer des applications existantes. Quand vous remplacez une application, spécifiez un nouveau type de déploiement pour remplacer le type de déploiement de l’application remplacée. En outre, décidez s’il faut mettre à niveau ou désinstaller l’application remplacée avant d’installer l’application de remplacement.

Pour plus d’informations, consultez [Modifier et remplacer des applications](/sccm/apps/deploy-use/revise-and-supersede-applications).

#### <a name="third-party-software-updates"></a>Mises à jour de logiciels tiers
Depuis la version 1806, utilisez le nœud **Catalogues de mises à jour de logiciels tiers** de la console Configuration Manager pour vous abonner à des catalogues tiers, publier leurs mises à jour sur votre point de mise à jour logicielle, puis les déployer sur les clients.<!--1352101-->

Pour plus d’informations, consultez [Mises à jour de logiciels tiers](/sccm/sum/deploy-use/third-party-software-updates).

#### <a name="system-center-updates-publisher"></a>Éditeur de mise à jour Systems Center
L’éditeur de mise à jour System Center (SCUP) est un outil autonome qui permet à des éditeurs de logiciels indépendants ou des développeurs d’applications métier de gérer les mises à jour personnalisées. Ces mises à jour incluent celles qui comportent des dépendances, comme les pilotes et les offres groupées de mises à jour.

Pour plus d’informations, consultez [Éditeur de mise à jour System Center](/sccm/sum/tools/updates-publisher).



##  <a name="BKMK_SUPInstallation"></a> Planifier l’installation du point de mise à jour logicielle  

Cette section inclut les sous-rubriques suivantes :  
- [Configuration requise pour le point de mise à jour logicielle](#BKMK_SUPSystemRequirements)
- [Planifier l’installation de WSUS](#BKMK_PlanningForWSUS)
- [Configurer des pare-feu](#BKMK_ConfigureFirewalls)  


Cette section contient des informations sur les actions à exécuter pour planifier et préparer correctement l’installation du point de mise à jour logicielle. Avant de créer un rôle de système de site pour le point de mise à jour logicielle dans Configuration Manager, vous devez prendre en compte plusieurs exigences. Les exigences spécifiques dépendent de votre infrastructure Configuration Manager. Quand vous configurez le point de mise à jour logicielle pour communiquer à l’aide de HTTPS, il est particulièrement important de passer en revue cette section. Les serveurs prenant en charge HTTPS nécessitent des étapes supplémentaires pour fonctionner correctement.  

###  <a name="BKMK_SUPSystemRequirements"></a> Configuration requise pour le point de mise à jour logicielle  

Installez le rôle de système de site du point de mise à jour logicielle sur un système de site qui répond aux conditions minimales requises pour WSUS et aux configurations prises en charge des systèmes de site Configuration Manager.  

-   Pour plus d’informations sur les conditions minimales requises pour le rôle serveur WSUS dans Windows Server, consultez les détails de la [vérification des considérations et de la configuration requise](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/plan/plan-your-wsus-deployment#BKMK_1.1).  

-   Pour plus d’informations sur les configurations prises en charge pour les systèmes de site Configuration Manager, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


###  <a name="BKMK_PlanningForWSUS"></a> Planifier l’installation de WSUS  

Installez une version prise en charge de WSUS sur tous les serveurs de système de site que vous configurez pour le rôle de point de mise à jour logicielle. Quand vous n’installez pas le point de mise à jour logicielle sur le serveur de site, installez la console d’administration WSUS sur le serveur de site. Ce composant permet au serveur de site de communiquer avec le serveur WSUS qui est exécuté sur le point de mise à jour logicielle.  

Quand vous utilisez WSUS sur Windows Server version 2012 ou ultérieure, configurez des autorisations supplémentaires pour permettre au composant **Configuration Manager WSUS** dans Configuration Manager de se connecter au serveur WSUS. Ce composant effectue des contrôles d’intégrité réguliers. Choisissez l’une des options suivantes pour configurer les autorisations requises :  

-   Ajouter le compte **SYSTEM** au groupe **Administrateurs WSUS**  

-   Ajouter le compte **NT AUTHORITY\SYSTEM** en tant qu’utilisateur pour la base de données WSUS (SUSDB). Configurez un minimum de l’appartenance au rôle de base de données webService.  
  
Pour plus d’informations sur la manière d’installer WSUS sur Windows Server, consultez [Installer le rôle serveur WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/1-install-the-wsus-server-role).  

Lorsque vous installez plusieurs points de mise à jour logicielle sur un site principal, utilisez la même base de données WSUS pour chaque point de mise à jour logicielle d'une même forêt Active Directory. Le partage de la même base de données améliore les performances quand les clients basculent vers un nouveau point de mise à jour logicielle. Pour plus d’informations, consultez [Utiliser une base de données WSUS partagée pour les points de mise à jour logicielle](/sccm/sum/plan-design/software-updates-best-practices#bkmk_shared-susdb).  


####  <a name="BKMK_CustomWebSite"></a> Configurer WSUS pour utiliser un site web personnalisé  
Lorsque vous installez WSUS, vous avez la possibilité d'utiliser le site web par défaut IIS existant ou de créer un site web WSUS personnalisé. Créez un site web personnalisé pour WSUS afin que les services IIS hébergent les services WSUS sur un site web virtuel dédié. Sinon, il partage le même site web que celui utilisé par les autres applications ou systèmes de site Configuration Manager. Cette configuration est particulièrement nécessaire quand vous installez le rôle de point de mise à jour logicielle sur le serveur de site. Quand vous exécutez WSUS dans Windows Server version 2012 ou ultérieure, WSUS est configuré par défaut pour utiliser le port 8530 pour HTTP et le port 8531 pour HTTPS. Spécifiez ces ports quand vous créez le point de mise à jour logicielle sur un site.  


####  <a name="BKMK_WSUSInfrastructure"></a> Utiliser une infrastructure WSUS existante  
Sélectionnez un serveur WSUS qui était actif dans votre environnement avant l’installation de Configuration Manager comme point de mise à jour logicielle. Quand le point de mise à jour logicielle est configuré, spécifiez les paramètres de synchronisation. Configuration Manager se connecte au serveur WSUS qui s’exécute sur le serveur de point de mise à jour logicielle, puis configure WSUS avec les mêmes paramètres. 

Avant de configurer le serveur en tant que point de mise à jour logicielle, comparez sa configuration concernant les produits et classifications avec vos paramètres Configuration Manager. Si vous avez synchronisé le serveur WSUS existant avant de le configurer en tant que point de mise à jour logicielle et que les listes de produits et classifications sont différentes, il synchronise toutes les métadonnées des mises à jour logicielles, quels que soient les paramètres configurés. Ce comportement aboutit à des métadonnées de mises à jour logicielles inattendues dans la base de données du site. 

Vous rencontrez le même comportement quand vous ajoutez des produits ou des classifications directement dans la console d’administration WSUS, puis que vous lancez immédiatement une synchronisation. Par défaut, Configuration Manager se connecte toutes les heures à WSUS et réinitialise tous les paramètres modifiés hors de Configuration Manager. Les mises à jour logicielles qui ne respectent pas les produits et classifications que vous spécifiez dans les paramètres de synchronisation expirent. Ensuite, elles sont supprimées de la base de données du site.  

Quand un serveur WSUS est configuré comme point de mise à jour logicielle, vous ne pouvez plus l’utiliser comme un serveur WSUS autonome. Si vous avez besoin d’un serveur WSUS autonome distinct qui n’est pas géré par Configuration Manager, configurez-le sur un serveur différent.  

####  <a name="BKMK_WSUSAsReplica"></a> Configurer WSUS comme serveur réplica  
Quand vous ajoutez le rôle de point de mise à jour logicielle sur un serveur de site principal, vous ne pouvez pas utiliser un serveur WSUS qui est configuré en tant que réplica. Quand le serveur WSUS est configuré en tant que réplica, la configuration du serveur WSUS par Configuration Manager et la synchronisation de WSUS se soldent par un échec. Le premier point de mise à jour logicielle que vous installez sur un site principal est le point de mise à jour logicielle par défaut. Les points de mise à jour logicielle supplémentaires sur le site sont configurés en tant que réplicas du point de mise à jour logicielle par défaut.  

####  <a name="BKMK_WSUSandSSL"></a> Déterminer si WSUS doit être configuré pour utiliser le protocole SSL  
Utilisez le protocole SSL pour contribuer à sécuriser le point de mise à jour logicielle. WSUS utilise SSL pour authentifier les ordinateurs clients et les serveurs WSUS en aval vers le serveur WSUS. WSUS utilise également SSL pour chiffrer les métadonnées de mise à jour logicielle. Quand vous choisissez de sécuriser WSUS avec SSL, préparez le serveur WSUS avant d’installer le point de mise à jour logicielle. Pour plus d’informations, consultez l’article [Configurer SSL sur le serveur WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) dans la documentation de WSUS. 

Quand vous installez et configurez le point de mise à jour logicielle, sélectionnez l’option **Activer les communications SSL pour le serveur WSUS**. Sinon, Configuration Manager configure le serveur WSUS pour qu’il n’utilise pas le protocole SSL. Quand vous activez SSL sur un point de mise à jour logicielle, vous devez également configurer des points de mise à jour logicielle sur les sites enfants pour utiliser SSL.  


###  <a name="BKMK_ConfigureFirewalls"></a> Configurer des pare-feu  

Le point de mise à jour logicielle sur un site d’administration centrale Configuration Manager communique avec les services WSUS sur le point de mise à jour logicielle. WSUS communique avec la source de synchronisation pour synchroniser les métadonnées des mises à jour logicielles. Les points de mise à jour logicielle sur un site enfant communiquent avec le point de mise à jour logicielle sur le site parent. Quand il existe plusieurs points de mise à jour logicielle sur un site principal, les points supplémentaires communiquent avec le point de mise à jour logicielle par défaut. Le rôle par défaut est le premier point de mise à jour logicielle installé sur le site.  

Vous devrez peut-être configurer le pare-feu pour autoriser le trafic HTTP ou HTTPS que WSUS utilise dans les scénarios suivants : 
- Entre le point de mise à jour logicielle et Internet
- Entre un point de mise à jour logicielle et sa source de synchronisation en amont
- Entre des points de mise à jour logicielle supplémentaires  

La connexion à Microsoft Update est toujours configurée pour utiliser le port 80 pour HTTP et le port 443 pour HTTPS. Utilisez un port personnalisé pour la connexion à partir de WSUS sur le point de mise à jour logicielle sur un site enfant vers WSUS sur le point de mise à jour logicielle sur le site parent. Quand votre stratégie de sécurité n’autorise pas la connexion, utilisez la méthode de synchronisation d’exportation et d’importation. Pour plus d’informations, consultez la section [Source de synchronisation](#BKMK_SyncSource) de cet article. Pour plus d’informations sur les ports qu’utilise WSUS, consultez [Comment déterminer les paramètres de port utilisés par WSUS dans Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  


#### <a name="restrict-access-to-specific-domains"></a>Restreindre l’accès à des domaines spécifiques  
Si votre organisation n’autorise pas l’ouverture des ports et des protocoles à toutes les adresses sur le pare-feu situé entre le point de mise à jour logicielle actif et Internet, restreignez l’accès aux domaines suivants de sorte que WSUS et les mises à jour automatiques puissent communiquer avec Microsoft Update :  

-   `http://windowsupdate.microsoft.com`  

-   `http://*.windowsupdate.microsoft.com`  

-   `https://*.windowsupdate.microsoft.com`  

-   `http://*.update.microsoft.com`  

-   `https://*.update.microsoft.com`  

-   `http://*.windowsupdate.com`  

-   `http://download.windowsupdate.com`  

-   `http://download.microsoft.com`  

-   `http://*.download.windowsupdate.com`  

-   `http://test.stats.update.microsoft.com`  

-   `http://ntservicepack.microsoft.com`  

Vous devrez peut-être ajouter les adresses ci-après au pare-feu qui se trouve entre les deux systèmes de site dans les cas suivants : 
- Si les sites enfants ont un point de mise à jour logicielle 
- S’il existe un point de mise à jour logicielle actif distant basé sur Internet sur un site

  **Point de mise à jour logicielle sur le site enfant**  

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  



##  <a name="BKMK_SyncSettings"></a> Planifier des paramètres de synchronisation  

Cette section inclut les sous-rubriques suivantes :  
- [Source de synchronisation](#BKMK_SyncSource)
- [Calendrier de synchronisation](#BKMK_SyncSchedule)
- [Classifications des mises à jour](#BKMK_UpdateClassifications)
- [Produits](#BKMK_UpdateProducts)
- [Règles de remplacement](#BKMK_SupersedenceRules)
- [Langues](#BKMK_UpdateLanguages)  


La synchronisation des mises à jour logicielles dans Configuration Manager télécharge les métadonnées des mises à jour logicielles d’après les critères que vous configurez. Le site de niveau supérieur dans votre hiérarchie synchronise les mises à jour logicielles à partir de Microsoft Update. Vous pouvez configurer le point de mise à jour logicielle sur le site de niveau supérieur pour qu’il se synchronise avec un serveur WSUS existant qui ne figure pas dans la hiérarchie Configuration Manager. Les sites principaux enfants synchronisent les métadonnées des mises à jour logicielles à partir du point de mise à jour logicielle sur le site d'administration centrale. Avant d'installer et de configurer un point de mise à jour logicielle, utilisez cette section pour planifier les paramètres de synchronisation.  


###  <a name="BKMK_SyncSource"></a> Source de synchronisation  

Les paramètres de la source de synchronisation du point de mise à jour logicielle spécifient l’emplacement auquel le point de mise à jour logicielle récupère les métadonnées des mises à jour logicielles. Ils indiquent également si le processus de synchronisation crée des événements de rapports WSUS.  

-   **Source de synchronisation** : par défaut, le point de mise à jour logicielle sur le site de niveau supérieur configure la source de synchronisation pour Microsoft Update. Vous pouvez synchroniser le site de niveau supérieur avec un serveur WSUS existant. Le point de mise à jour logicielle sur un site principal enfant configure la source de synchronisation en tant que point de mise à jour logicielle sur le site d’administration centrale.  

    -  Le premier point de mise à jour logicielle que vous installez sur un site principal, qui est le point de mise à jour logicielle par défaut, se synchronise avec le site d’administration centrale. Les points de mise à jour logicielle supplémentaires sur le site principal se synchronisent avec le point de mise à jour logicielle par défaut sur le site principal.  

    - Quand un point de mise à jour logicielle est déconnecté de Microsoft Update ou du serveur de mise à jour en amont, configurez la source de synchronisation pour qu’elle ne soit pas synchronisée avec une source de synchronisation configurée. À la place, configurez-la pour qu’elle utilise la fonction d’exportation et d’importation de l’outil **WSUSUtil** pour synchroniser les mises à jour logicielles. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles à partir d’un point de mise à jour logicielle déconnecté](../get-started/synchronize-software-updates-disconnected.md).  

-   **Événements de rapports WSUS :** l’agent Windows Update sur les ordinateurs clients peut créer des messages d’événement utilisés pour les rapports WSUS. Configuration Manager n’utilise pas ces événements. Ainsi, l’option **Ne pas créer les événements de rapports WSUS** est sélectionnée par défaut. Si ces événements ne sont pas créés, le client peut se connecter au serveur WSUS uniquement au moment de l’évaluation des mises à jour logicielles et des analyses de conformité. Si ces événements sont nécessaires à la génération de rapports en dehors de Configuration Manager, modifiez ce paramètre pour créer des événements de génération de rapports WSUS.  


###  <a name="BKMK_SyncSchedule"></a> Calendrier de synchronisation  

Configurez le calendrier de synchronisation uniquement sur le point de mise à jour logicielle du site de niveau supérieur dans la hiérarchie Configuration Manager. Lorsque vous configurez le calendrier de synchronisation, le point de mise à jour logicielle se synchronise avec la source de synchronisation à la date et à l'heure que vous avez spécifiées. Le calendrier personnalisé vous permet de synchroniser les mises à jour logicielles afin d’optimiser votre environnement. Prenez en compte les exigences de performance du serveur WSUS, du serveur de site et du réseau. Par exemple, 2h00 une fois par semaine. Sinon, démarrez manuellement la synchronisation sur le site de niveau supérieur à l’aide de l’action **Mises à jour logicielles de synchronisation** à partir des nœuds **Toutes les mises à jour logicielles** ou **Groupes de mises à jour logicielles** dans la console Configuration Manager.  

> [!TIP]  
>  Planifiez la synchronisation des mises à jour logicielles pour qu’elle s’exécute à une heure adaptée à votre environnement. Un scénario habituel consiste à définir le calendrier de synchronisation pour qu’il soit exécuté peu après la publication d’une mise à jour logicielle normale de Microsoft le deuxième mardi de chaque mois. Ce jour est souvent désigné par l’expression *Patch Tuesday*. Si vous utilisez Configuration Manager pour fournir des mises à jour du moteur et des définitions Windows Defender et Endpoint Protection, envisagez de définir le calendrier de synchronisation pour qu’il s’exécute tous les jours.  

Une fois le point de mise à jour logicielle correctement synchronisé, il envoie une demande de synchronisation aux sites enfants. Si vous avez des points de mise à jour logicielle supplémentaires sur un site principal, il envoie une demande de synchronisation à chaque point de mise à jour logicielle. Ce processus se répète sur chaque site de la hiérarchie.  


###  <a name="BKMK_UpdateClassifications"></a> Classifications des mises à jour  

Chaque mise à jour logicielle fait partie d'une classification particulière qui permet d'organiser les différents types de mises à jour. Pendant le processus de synchronisation, le site synchronise les métadonnées pour les classifications spécifiées. 

Configuration Manager prend en charge la synchronisation des classifications de mise à jour suivantes :  

-   **Mises à jour critiques** : des mises à jour distribuées en grand nombre, répondant à un problème spécifique qui concerne un bogue critique non lié à la sécurité.  

-   **Mises à jour de définitions** : des mises à jour pour des virus ou d’autres fichiers de définition.  

-   **Packs de fonctionnalités** : nouvelles fonctionnalités de produit, distribuées en dehors d’une version de produit et incluses généralement dans la version suivante du produit.  

-   **Mises à jour de sécurité** : des mises à jour distribuées en grand nombre, répondant à un problème de sécurité spécifique à un produit.  

-   **Service Packs** : ensemble cumulé de correctifs logiciels rattachés à une application ou à un système d’exploitation. Ces correctifs comprennent des mises à jour de sécurité, des mises à jour critiques et des mises à jour logicielles.  

-   **Outils** : utilitaires ou fonctionnalités permettant d’effectuer une ou plusieurs tâches.  

-   **Correctifs cumulatifs** : ensemble cumulé de correctifs assemblé pour faciliter leur déploiement. Ces correctifs comprennent des mises à jour de sécurité, des mises à jour critiques et des mises à jour logicielles. Les correctifs cumulatifs concernent généralement un domaine particulier, tel que la sécurité ou un composant de produit.  

-   **Mises à jour** : mises à jour d’une application ou d’un fichier déjà installés.  

-   **Mises à niveau** : mises à jour de fonctionnalité vers une nouvelle version de Windows 10.  

Configurez les paramètres de classification des mises à jour uniquement sur le site de niveau supérieur. Ils ne sont pas configurés sur le point de mise à jour logicielle des sites enfants, car les métadonnées des mises à jour logicielles sont répliquées à partir du site de niveau supérieur. Quand vous sélectionnez des classifications de mises à jour, n’oubliez pas que plus vous en sélectionnez, plus la synchronisation des métadonnées des mises à jour logicielles prend du temps.  

> [!WARNING]  
>  Il est recommandé d’effacer toutes les classifications avant d’effectuer la toute première synchronisation. Après la synchronisation initiale, sélectionnez les classifications de votre choix, puis réexécutez la synchronisation.  


###  <a name="BKMK_UpdateProducts"></a> Produits  

Les métadonnées de chaque mise à jour logicielle définissent un ou plusieurs produits auxquels elles s’appliquent. Un produit est une édition spécifique d’un OS ou d’une application. Un exemple d’un produit est Microsoft Windows 10. Une famille de produits est l’OS ou l’application de base d’où sont issus les produits individuels. Par exemple, Microsoft Windows est une famille de produits dont Windows 10 et Windows Server 2016 font partie. Sélectionnez une famille de produits ou des produits distincts au sein d’une famille de produits.  

Quand des mises à jour logicielles s’appliquent à plusieurs produits et qu’au moins un de ces produits est sélectionné pour une synchronisation, tous les autres produits apparaissent dans la console Configuration Manager, même s’ils n’ont pas été sélectionnés. Par exemple, vous sélectionnez uniquement le produit Windows Server 2012. Si une mise à jour logicielle s’applique à Windows Server 2012 et Windows Server 2012 Datacenter Edition, ces deux produits sont dans la base de données du site.  

Configurez les paramètres de produit uniquement sur le site de niveau supérieur. Ils ne sont pas configurés sur le point de mise à jour logicielle des sites enfants, car les métadonnées des mises à jour logicielles sont répliquées à partir du site de niveau supérieur. Plus vous choisissez de produits, plus la synchronisation des métadonnées des mises à jour logicielles prendra du temps.  

> [!IMPORTANT]  
>  Configuration Manager stocke une liste de produits et de familles de produits que vous choisissez quand vous installez le point de mise à jour logicielle pour la première fois. Il est possible que vous deviez attendre la fin de la synchronisation pour pouvoir sélectionner les produits et familles de produits qui sont publiés après Configuration Manager. Le processus de synchronisation met à jour la liste des produits et familles de produits disponibles à partir de laquelle vous pouvez effectuer votre choix. Effacez tous les produits avant de synchroniser les mises à jour logicielles pour la première fois. Après la synchronisation initiale, sélectionnez les produits de votre choix, puis réexécutez la synchronisation.  


###  <a name="BKMK_SupersedenceRules"></a> Règles de remplacement  

En règle générale, une mise à jour logicielle qui en remplace une autre effectue une ou plusieurs des opérations suivantes :  

-   Elle optimise, améliore ou met à jour le correctif fourni par une ou plusieurs mises à jour précédemment publiées.  

-   Elle améliore l’efficacité de son package de fichiers de mise à jour, qui est installé sur les clients si la mise à jour est approuvée pour l’installation. Par exemple, la mise à jour remplacée pourrait contenir des fichiers qui ne sont plus appropriés pour le correctif ou pour les systèmes d’exploitation pris en charge par la nouvelle mise à jour. Ces fichiers ne sont pas inclus dans le package de fichiers de remplacement de la mise à jour.  

-   Elle met à jour un produit vers les versions les plus récentes. En d'autres termes, elle met à jour les versions qui ne concernent plus d'anciennes versions ou configurations d'un produit. Les mises à jour peuvent également remplacer d'autres mises à jour si des modifications ont été apportées pour étendre la prise en charge des langues. Par exemple, une révision récente d’une mise à jour de produit pour Microsoft Office peut supprimer la prise en charge d’un ancien OS, mais ajouter la prise en charge de langues supplémentaires dans la version de mise à jour initiale.  

Dans les propriétés du point de mise à jour logicielle, spécifiez que les mises à jour logicielles remplacées expirent immédiatement. Ce paramètre les empêche d’être incluses dans les nouveaux déploiements. Il signale également les déploiements existants pour indiquer qu’ils contiennent une ou plusieurs mises à jour logicielles ayant expiré. Ou bien spécifiez une période de temps au terme de laquelle les mises à jour logicielles remplacées arrivent à expiration. Cette action vous permet de continuer à les déployer. 

Examinez les scénarios suivants, dans lesquels vous devrez peut-être déployer une mise à jour logicielle remplacée :  

-   Une mise à jour logicielle de remplacement prend en charge uniquement les versions plus récentes d’un système d’exploitation. Certains de vos ordinateurs clients exécutent des versions antérieures du système d’exploitation.  

-   Une mise à jour logicielle de remplacement présente des conditions d’applications plus restreintes que la mise à jour qu’elle remplace. Ce comportement peut la rendre inadaptée à certains clients.  

-   Une mise à jour logicielle de remplacement n’a pas été approuvée pour le déploiement dans votre environnement de production.  

    > [!NOTE]  
    > Avant la version 1806 de Configuration Manager, quand ce dernier définit une mise à jour logicielle remplacée avec l’état **Expiré**, celle-ci n’est pas définie avec l’état **Refusé** dans WSUS. Les clients continuent de rechercher une mise à jour expirée jusqu’à ce que la mise à jour soit refusée manuellement ou via un script personnalisé.  Après la version 1806 de Configuration Manager, ce dernier refuse également les mises à jour remplacées dans WSUS. Pour plus d’informations sur la tâche de nettoyage WSUS, consultez [Maintenance des mises à jour logicielles](/sccm/sum/deploy-use/software-updates-maintenance).


###  <a name="BKMK_UpdateLanguages"></a> Langues  

Les paramètres de langue pour le point de mise à jour logicielle vous permettent de configurer les éléments suivants : 
- Les langues pour lesquelles les détails du résumé (métadonnées des mises à jour logicielles) sont synchronisés pour les mises à jour logicielles  
- Les langues des fichiers de mise à jour logicielle qui sont téléchargées pour les mises à jour logicielles  

#### <a name="software-update-file"></a>Fichier de mise à jour logicielle  
Configurez les langues pour le paramètre **Fichier de mise à jour logicielle** dans les propriétés du point de mise à jour logicielle. Ce paramètre fournit les langues par défaut qui sont disponibles quand vous téléchargez des mises à jour logicielles sur un site. Modifiez les langues qui sont sélectionnées par défaut à chaque fois que des mises à jour logicielles sont téléchargées ou déployées. Lors du téléchargement, les fichiers de mise à jour logicielle correspondant aux langues configurées sont téléchargés à l'emplacement source du package de déploiement, si les fichiers de mise à jour logicielle sont disponibles dans la langue sélectionnée. Ensuite, ils sont copiés vers la bibliothèque de contenu sur le serveur de site, avant d’être distribués aux points de distribution qui sont configurés pour le package.  

Configurez les paramètres de langue du fichier de mise à jour logicielle avec les langues qui sont utilisées le plus fréquemment dans votre environnement. Par exemple, les clients dans votre site utilisent principalement l’anglais et le japonais pour Windows ou les applications. Quelques autres langues sont utilisées sur le site. Sélectionnez uniquement l’anglais et le japonais dans la colonne **Fichier de mise à jour logicielle** quand vous téléchargez ou déployez la mise à jour logicielle. Vous pourrez ainsi utiliser les paramètres par défaut sur la page **Sélection de la langue** des Assistants de déploiement et de téléchargement. En outre, vous empêchez ainsi le téléchargement des fichiers de mise à jour inutiles. Configurez ce paramètre sur chaque point de mise à jour logicielle de la hiérarchie Configuration Manager.  

#### <a name="summary-details"></a>Détails du résumé  
Au cours du processus de synchronisation, les informations sur les détails du résumé (métadonnées des mises à jour logicielles) sont mises à jour pour les mises à jour logicielles dans les langues spécifiées. Les métadonnées fournissent des informations sur la mise à jour logicielle, par exemple :
- Nom
- Description
- Produits pris en charge par la mise à jour
- Classification des mises à jour
- ID de l'article
- URL de téléchargement
- Règles de mise en application

Configurez les paramètres des détails du résumé uniquement sur le site de niveau supérieur. Ils ne sont pas configurés sur le point de mise à jour logicielle des sites enfants, car les métadonnées des mises à jour logicielles sont répliquées à partir du site d’administration centrale via une réplication de fichiers. Lorsque vous sélectionnez les langues des détails du résumé, vous devez choisir uniquement les langues dont votre environnement a besoin. Plus vous choisissez de langues, plus la synchronisation des métadonnées des mises à jour logicielles prendra du temps. Configuration Manager affiche les métadonnées des mises à jour logicielles en fonction des paramètres régionaux du système d’exploitation sur lequel s’exécute la console Configuration Manager. Si les propriétés localisées pour les mises à jour logicielles ne sont pas disponibles dans la langue du système d’exploitation, les informations sur les mises à jour logicielles s’affichent en anglais.  

> [!IMPORTANT]  
>  Sélectionnez toutes les langues des détails du résumé dont vous avez besoin. Quand le point de mise à jour logicielle sur le site de niveau supérieur se synchronise avec la source de synchronisation, les langues des détails du résumé sélectionnées déterminent les métadonnées de mises à jour logicielles qu’il récupère. Si vous modifiez les langues des détails du résumé après au moins une exécution de la synchronisation, il récupère les métadonnées de mise à jour logicielle des langues des détails du résumé modifiées se rapportant uniquement aux mises à jour logicielles nouvelles ou mises à jour. Les mises à jour logicielles qui ont déjà été synchronisées ne sont pas mises à jour à partir des nouvelles métadonnées des langues modifiées, sauf si une modification est apportée à la mise à jour logicielle au niveau de la source de synchronisation.  



##  <a name="BKMK_MaintenanceWindow"></a> Planifier une fenêtre de maintenance pour les mises à jour logicielles  

Ajoutez une fenêtre de maintenance dédiée à l’installation des mises à jour logicielles. Vous pouvez ainsi configurer une fenêtre de maintenance générale et une fenêtre de maintenance distincte pour les mises à jour logicielles. Quand vous disposez d’une fenêtre de maintenance générale et d’une fenêtre de maintenance des mises à jour logicielles, les clients installent des mises à jour logicielles uniquement dans le cadre de la fenêtre de maintenance des mises à jour logicielles. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  



##  <a name="BKMK_RestartOptions"></a> Options de redémarrage pour les clients Windows 10 après l’installation de mises à jour logicielles

Quand une mise à jour logicielle nécessitant un redémarrage est déployée et installée à l’aide de Configuration Manager, le client planifie un redémarrage en attente et affiche une boîte de dialogue de redémarrage.

Quand un redémarrage est en attente pour une mise à jour logicielle Configuration Manager, les options **Mettre à jour et redémarrer** et **Mettre à jour et arrêter** sont disponibles sur les ordinateurs Windows 10 dans les options d’alimentation de Windows. Après l’utilisation de l’une de ces options, la boîte de dialogue de redémarrage ne s’affiche pas quand l’ordinateur redémarre.



## <a name="next-steps"></a>Étapes suivantes
Quand vous planifiez des mises à jour logicielles, consultez [Préparer la gestion des mises à jour logicielles](../get-started/prepare-for-software-updates-management.md).  

Pour plus d’informations sur la gestion de Windows en tant que service, consultez [Notions de base de Configuration Manager as a service et Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service).
