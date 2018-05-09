---
title: Planifier les mises à jour logicielles
titleSuffix: Configuration Manager
description: Il est essentiel de planifier l’infrastructure du point de mise à jour logicielle avant d’utiliser les mises à jour logicielles dans un environnement de production System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 2debedd40fbde8094c14a873235a742ccf15cc95
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>Planifier les mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’utiliser les mises à jour logicielles dans un environnement de production System Center Configuration Manager, vous devez parcourir le processus de planification. Une bonne planification de l’infrastructure du point de mise à jour logicielle est la clé d’une implémentation réussie des mises à jour logicielles.

## <a name="capacity-planning-recommendations-for-software-updates"></a>Recommandations pour la planification de la capacité pour les mises à jour logicielles  
 Vous pouvez utiliser les recommandations suivantes comme ligne de base pour déterminer les informations de planification de capacité des mises à jour logicielles convenant à votre organisation. Les besoins réels en capacités peuvent différer des recommandations indiquées dans cet article selon les critères suivants : votre environnement réseau spécifique, le matériel utilisé pour héberger le système de site du point de mise à jour logicielle, le nombre de clients installés et les rôles de système de site qui sont installés sur le serveur.  

###  <a name="BKMK_SUMCapacity"></a> Planification de la capacité du point de mise à jour logicielle  
 Le nombre de clients pris en charge dépend de la version de Windows Server Update Services (WSUS) exécutée sur le point de mise à jour logicielle et de la coexistence ou non du rôle de système de site du point de mise à jour logicielle avec un autre rôle de système de site.  

-   Le point de mise à jour logicielle peut prendre en charge jusqu’à 25 000 clients quand WSUS s’exécute sur l’ordinateur du point de mise à jour logicielle et quand le point de mise à jour logicielle coexiste avec un autre rôle de système de site.  

-   Le point de mise à jour logicielle peut prendre en charge jusqu’à 150 000 clients quand l’ordinateur distant satisfait à la configuration requise de WSUS pour prendre en charge ce nombre, WSUS est utilisé avec Configuration Manager et vous configurez les éléments suivants :

    Pools d’applications IIS :
    - Augmenter la longueur de file d’attente WsusPool à 2000
    - Multiplier par quatre la limite de mémoire privée WsusPool, ou lui affecter la valeur 0 (illimitée)      

    Pour plus d’informations sur la configuration matérielle requise pour le point de mise à jour logicielle, consultez [Matériel recommandé pour les systèmes de site](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems).

-   Par défaut, Configuration Manager ne prend pas en charge la configuration de points de mise à jour logicielle comme clusters d’équilibrage de la charge réseau (NLB). Avant Configuration Manager version 1702, vous pouviez utiliser le SDK Configuration Manager pour configurer jusqu’à quatre points de mise à jour logicielle sur un cluster d’équilibrage de charge réseau. Cependant, depuis la version 1702, les points de mise à jour logicielle ne sont pas pris en charge en tant que clusters NLB ; les mises à niveau vers cette version sont bloquées si cette configuration est détectée.

### <a name="capacity-planning-for-software-updates-objects"></a>Planification de la capacité pour les objets des mises à jour logicielles  
 Utilisez les informations de capacité suivantes pour planifier les objets des mises à jour logicielles.  

-   **Limite de 1 000 mises à jour logicielles dans un déploiement**  

     Vous devez limiter le nombre de mises à jour logicielles à 1 000 pour chaque déploiement de mises à jour logicielles. Lorsque vous créez une règle de déploiement automatique, spécifiez un critère qui limite le nombre de mises à jour logicielles retournées. La règle de déploiement automatique échoue lorsque les critères que vous spécifiez renvoient plus de 1 000 mises à jour logicielles. Vous pouvez vérifier l’état de la règle de déploiement automatique à partir du nœud **Règles de déploiement automatique** dans la console Configuration Manager. Lorsque vous déployez manuellement des mises à jour logicielles, ne sélectionnez pas plus de 1 000 mises à jour à déployer.  

     Vous devez également limiter le nombre de mises à jour logicielles à 1 000 dans une base de référence de configuration. Pour plus d’informations, consultez [Créer des bases de référence de configuration](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="BKMK_SUPInfrastructure"></a> Déterminer l’infrastructure du point de mise à jour logicielle  
 Le site d’administration centrale et tous les sites principaux enfants doivent disposer d’un point de mise à jour logicielle où vous déployez les mises à jour logicielles. Lors de la planification de l'infrastructure du point de mise à jour logicielle, vous devez déterminer les dépendances suivantes :
 - emplacement d’installation du point de sauvegarde logicielle du site ;
 - sites nécessitant un point de mise à jour logicielle qui accepte les communications provenant de clients basés sur Internet ;
 - nécessité ou non d’installer un point de mise à jour logicielle sur un site secondaire.

Utilisez les sections suivantes pour déterminer l'infrastructure du point de mise à jour logicielle.  

> [!IMPORTANT]  
>  Pour plus d’informations sur les dépendances internes et externes nécessaires pour les mises à jour logicielles, consultez [Prérequis pour les mises à jour logicielles](prerequisites-for-software-updates.md).  

 Vous pouvez ajouter plusieurs points de mise à jour logicielle sur un site principal Configuration Manager. La possibilité d'avoir plusieurs points de mise à jour logicielle sur un site offre une tolérance de panne sans impliquer la complexité de l'équilibrage de la charge réseau (NLB). Toutefois, le basculement dont vous bénéficiez avec plusieurs points de mise à jour logicielle n'est pas aussi robuste qu'un équilibrage de la charge pur, mais plutôt conçu pour la tolérance de panne. En outre, la conception du basculement du point de mise à jour logicielle est différente de celle du modèle de randomisation pur utilisé dans la conception des points de gestion. Contrairement à la conception des points de gestion, dans les points de mise à jour logicielle, il existe des coûts en termes de performances du client et du réseau, associés au basculement vers un nouveau point de mise à jour logicielle. Lorsque le client bascule vers un nouveau serveur WSUS pour rechercher des mises à jour logicielles, la taille du catalogue augmente, tout comme les exigences de performance réseau et côté client associées. Par conséquent, le client conserve l'affinité avec le dernier point de mise à jour logicielle qu'il a correctement analysé.  

 Le premier point de mise à jour logicielle que vous installez sur un site principal est la source de synchronisation de tous les points de mise à jour logicielle supplémentaires que vous ajoutez sur le site principal. Une fois que vous avez ajouté vos points de mise à jour logicielle et lancé la synchronisation des mises à jour logicielles, vous pouvez afficher l'état des points de mise à jour logicielle et la source de synchronisation depuis le nœud **État de la synchronisation du point de mise à jour logicielle** dans l'espace de travail **Surveillance** .  

 Quand un point de mise à jour logicielle échoue, et qu'il est configuré en tant que source de synchronisation pour les autres points de mise à jour logicielle sur le site, vous devez supprimer manuellement ce point de mise à jour logicielle en échec et en sélectionner un nouveau à utiliser en tant que source de synchronisation. Pour plus d’informations sur la suppression d’un point de mise à jour logicielle, consultez [Supprimer le rôle de système de site du point de mise à jour logicielle](../get-started/remove-a-software-update-point.md).  

###  <a name="BKMK_SUPList"></a> Liste des points de mise à jour logicielle  
 Configuration Manager fournit au client une liste de points de mise à jour logicielle dans les scénarios suivants : quand un nouveau client reçoit la stratégie d’activation des mises à jour logicielles, ou quand un client ne parvient pas à contacter son point de mise à jour logicielle et qu’il a besoin d’en changer. Le client sélectionne un point de mise à jour logicielle de manière aléatoire dans la liste, puis il hiérarchise les points de mise à jour logicielle qui se trouvent dans la même forêt. Configuration Manager fournit aux clients une liste différente selon le type de client.  

-   **Clients basés sur intranet**: reçoivent la liste des points de mise à jour logicielle que vous pouvez configurer pour autoriser les connexions uniquement depuis l'intranet, ou la liste des points de mise à jour logicielle qui autorisent les connexions client Internet et intranet.  

-   **Clients basés sur Internet**: reçoivent la liste des points de mise à jour logicielle que vous pouvez configurer pour autoriser les connexions uniquement depuis Internet, ou la liste des points de mise à jour logicielle qui autorisent les connexions client Internet et intranet.  

###  <a name="BKMK_SUPSwitching"></a> Basculement de point de mise à jour logicielle  
> [!NOTE]
> Depuis la version 1702, les clients utilisent des groupes de limites pour rechercher un nouveau point de mise à jour logicielle et pour rétablir et trouver un nouveau point de mise à jour logicielle si leur point actuel n’est plus accessible. Vous pouvez ajouter des points de mise à jour logicielle individuels à différents groupes de limites pour contrôler les serveurs qu’un client peut trouver. Pour plus d’informations, consultez la section [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) dans l’article [Configuration des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).

Si vous avez plusieurs points de mise à jour logicielle sur un site, et que l'un d'eux est en échec ou indisponible, les clients se connectent à un point de mise à jour logicielle différent pour continuer de rechercher les dernières mises à jour logicielles. Quand un client est affecté à un point de mise à jour logiciel, il le reste sauf s’il ne parvient pas à rechercher des mises à jour logicielles sur ce point de mise à jour logicielle.  

La recherche des mises à jour logicielles peut échouer avec plusieurs codes de nouvelle tentative et de non-nouvelle tentative différents. Lorsque l'analyse échoue avec un code d'erreur de nouvelle tentative, le client démarre un processus de nouvelle tentative pour rechercher les mises à jour logicielles sur le point de mise à jour logicielle. Les conditions précises qui génèrent un code d'erreur de nouvelle tentative sont généralement dues à l'indisponibilité ou à la surcharge temporaire du serveur WSUS. Le client utilise le processus suivant lorsqu'il ne parvient pas à rechercher les mises à jour logicielles :  

1.  Le client recherche les mises à jour logicielles soit à l'heure planifiée, soit lorsque la recherche est lancée via le Panneau de configuration sur le client, soit en utilisant le Kit de développement logiciel (SDK). Si l'analyse échoue, le client attend 30 minutes avant d'effectuer une nouvelle tentative d'analyse et il utilise le même point de mise à jour logicielle.  

2.  Le client effectue au moins quatre nouvelles tentatives à des intervalles de 30 minutes. Après le quatrième échec, il attend deux minutes supplémentaires, puis il passe au point de mise à jour logicielle suivant dans la liste des points de mise à jour logicielle.  

3.  Le client suit le même processus sur le nouveau point de mise à jour logicielle. Après une analyse réussie, le client continue à se connecter au nouveau point de mise à jour logicielle.

 La liste suivante fournit des informations supplémentaires que vous pouvez consulter en cas de nouvelle tentative et de basculement des points de mise à jour logicielle :  

-   Si un client est déconnecté de l'intranet d'entreprise et qu'il ne parvient pas à rechercher des mises à jour logicielles, il ne bascule pas vers un autre point de mise à jour logicielle. Il s'agit d'un échec attendu, étant donné que le client ne peut pas atteindre le réseau d'entreprise ou le point de mise à jour logicielle qui permet la connexion depuis l'intranet. Le client Configuration Manager détermine la disponibilité du point de mise à jour logicielle intranet.  

-   Si la gestion des clients basés sur Internet est activée et que plusieurs points de mise à jour logicielle sont configurés pour accepter les communications provenant des clients sur Internet, le processus de basculement suit le processus de nouvelle tentative standard décrit dans le scénario précédent.  

-   Si le processus d'analyse a démarré, alors que le client a été mis hors tension avant la fin de l'analyse, cela n'est pas considéré comme un échec d'analyse et cela n'est pas comptabilisé dans les quatre nouvelles tentatives.  

Quand Configuration Manager reçoit un des codes d’erreur suivants de l’Agent Windows Update, le client retente d’établir la connexion :  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Pour rechercher la signification d’un code d’erreur, vous devez convertir le code d’erreur décimal au format hexadécimal, puis rechercher la valeur hexadécimale sur un site tel que le [wiki des codes d’erreur de l’Agent Windows Update](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx).


###  <a name="BKMK_ManuallySwitchSUPs"></a>Basculer manuellement les clients vers un nouveau point de mise à jour logicielle
À compter de Configuration Manager version 1606, vous pouvez activer l’option permettant aux clients Configuration Manager de basculer vers un nouveau point de mise à jour logicielle en cas de problème avec le point de mise à jour logicielle actif. Cette option entraîne des modifications uniquement quand un client reçoit plusieurs points de mise à jour logicielle à partir d’un point de gestion.

> [!IMPORTANT]    
> Quand vous basculez des appareils pour utiliser un nouveau serveur, les appareils utilisent une action de secours pour rechercher ce serveur. C’est pourquoi vous devez passer en revue vos configurations de groupe de limites et vérifiez que vos points de mise à jour logicielle sont dans les groupes de limites appropriés avant de procéder à ce changement. Pour plus d’informations, consultez [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).
>
> Le basculement vers un nouveau point de mise à jour logicielle génère du trafic réseau supplémentaire. Le volume du trafic dépend de vos paramètres de configuration WSUS (classifications des mises à jour, produits, partage d’une base de données WSUS par les points de mise à jour logicielle ou non, etc.). Si vous envisagez de basculer plusieurs appareils, songez à le faire pendant les fenêtres de maintenance pour réduire l’impact sur le réseau durant la synchronisation avec le nouveau serveur de point de mise à jour logicielle.

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Pour activer l’option de basculement vers des points de mise à jour logicielle  
Activez cette option sur un regroupement d’appareils ou sur un ensemble d’appareils sélectionnés. Une fois l’option activée, les clients rechercheront un autre point de mise à jour logicielle lors de la prochaine analyse.

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité > Vue d’ensemble > Regroupements d’appareils**.  

2.  Sous l’onglet **Accueil** , dans le groupe **Regroupement** , cliquez sur **Notification du client**, puis sur **Passer au point de mise à jour logicielle suivant**.  


###  <a name="BKMK_SUP_CrossForest"></a> Points de mise à jour logicielle dans une forêt non approuvée  
 Vous pouvez créer un ou plusieurs points de mise à jour logicielle sur un site pour prendre en charge des clients dans une forêt non approuvée. Pour ajouter un point de mise à jour logicielle dans une autre forêt, vous devez d'abord installer et configurer un serveur WSUS dans la forêt. Démarrez ensuite l’Assistant pour ajouter un serveur de site Configuration Manager doté du rôle de système de site du point de mise à jour logicielle. Dans l'Assistant, configurez les paramètres suivants pour vous connecter correctement au serveur WSUS dans la forêt non approuvée :  

-   Spécifiez un compte d'installation du système de site capable d'accéder au serveur WSUS dans la forêt.  

-   Spécifiez le compte de connexion du serveur WSUS à utiliser pour se connecter au serveur WSUS.  

 Par exemple, vous avez un site principal dans la forêt A doté de deux points de mise à jour logicielle (SUP01 et SUP02). En outre, pour ce même site principal, vous avez deux points de mise à jour logicielle (SUP03 et SUP04) dans la forêt B. Lorsque le basculement se produit dans cet exemple, les points de mise à jour logicielle de la même forêt que le client sont prioritaires.  

###  <a name="BKMK_WSUSSyncSource"></a> Utiliser un serveur WSUS existant comme source de synchronisation sur le site de niveau supérieur  
 En règle générale, le site de niveau supérieur dans votre hiérarchie est configuré pour synchroniser les métadonnées des mises à jour logicielles avec Microsoft Update. Quand votre stratégie de sécurité d’entreprise n’autorise pas l’accès à Internet depuis le site de niveau supérieur, vous pouvez configurer la source de synchronisation pour que le site de niveau supérieur utilise un serveur WSUS existant ne faisant pas partie de votre hiérarchie Configuration Manager. Par exemple, vous pouvez disposer d'un serveur WSUS installé dans votre réseau de périmètre (DMZ) et doté d'un accès Internet, alors que votre site de niveau supérieur en est dépourvu. Vous pouvez configurer le serveur WSUS dans le réseau de périmètre (DMZ) en tant que source de synchronisation pour les métadonnées des mises à jour logicielles. Vous devez veiller à ce que le serveur WSUS situé dans le réseau de périmètre (DMZ) synchronise les mises à jour logicielles répondant aux critères nécessaires dans votre hiérarchie Configuration Manager. Sinon, le site de niveau supérieur risque de ne pas synchroniser les mises à jour logicielles attendues. Lorsque vous installez le point de mise à jour logicielle, configurez un compte de connexion WSUS qui a accès au serveur WSUS dans le réseau de périmètre (DMZ) et vérifiez que le pare-feu autorise le trafic pour les ports appropriés. Pour plus d’informations, consultez les [ports utilisés par le point de mise à jour logicielle vers la source de synchronisation](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="BKMK_NLBSUPSP1"></a> Point de mise à jour logicielle configuré pour utiliser un équilibrage de la charge réseau (NLB)  
 Le basculement de point de mise à jour logicielle répond probablement à vos besoins en matière de tolérance de panne. Par défaut, Configuration Manager ne prend pas en charge la configuration de points de mise à jour logicielle comme clusters d’équilibrage de la charge réseau (NLB). Avant Configuration Manager version 1702, vous pouviez utiliser le SDK Configuration Manager pour configurer jusqu’à quatre points de mise à jour logicielle sur un cluster d’équilibrage de charge réseau. Cependant, depuis la version 1702, les points de mise à jour logicielle ne sont pas pris en charge en tant que clusters NLB ; les mises à niveau vers cette version sont bloquées si cette configuration est détectée. Pour plus d’informations sur l’applet de commande PowerShell Set-CMSoftwareUpdatePoint, consultez [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="BKMK_SUPSecSite"></a> Point de mise à jour logicielle sur un site secondaire  
 Le point de mise à jour logicielle est facultatif sur un site secondaire. Vous pouvez installer un seul point de mise à jour logicielle sur un site secondaire. Les appareils affectés à un site secondaire sont configurés pour utiliser un point de mise à jour logicielle sur le site parent lorsqu'un point de mise à jour logicielle n'est pas installé sur le site secondaire. En général, vous installez un point de mise à jour logicielle sur un site secondaire quand la bande passante réseau est limitée entre les appareils affectés au site secondaire et les points de mise à jour logicielle sur le site principal parent, ou quand le point de mise à jour logicielle est proche de la limite de capacité. Une fois le point de mise à jour logicielle correctement installé et configuré sur le site secondaire, une stratégie à l'échelle du site est mise à jour pour les ordinateurs clients affectés au site et ces derniers commencent à utiliser le nouveau point de mise à jour logicielle.  

##  <a name="BKMK_SUPInstallation"></a> Planifier l’installation du point de mise à jour logicielle  
 Avant de créer un rôle de système de site du point de mise à jour logicielle dans Configuration Manager, vous devez prendre en compte plusieurs exigences, en fonction de votre infrastructure Configuration Manager. Lorsque vous configurez le point de mise à jour logicielle pour communiquer à l'aide du protocole SSL, il est particulièrement important de consulter cette section car vous devez prendre des mesures supplémentaires pour que les points de mise à jour logicielle de votre hiérarchie fonctionnent correctement. Cette section contient des informations sur les actions que vous devez exécuter pour planifier et préparer correctement l'installation du point de mise à jour logicielle.  

###  <a name="BKMK_SUPSystemRequirements"></a> Configuration requise pour le point de mise à jour logicielle  
 Le rôle de système de site du point de mise à jour logicielle doit être installé sur un système de site qui répond aux conditions minimales requises pour WSUS et les configurations prises en charge des systèmes de site Configuration Manager.  

-   Pour plus d’informations sur les conditions minimales requises pour le rôle serveur WSUS dans Windows Server 2012, consultez les détails de la [vérification des considérations et de la configuration requise](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) dans la bibliothèque de documentation Windows Server 2012.  

-   Pour plus d’informations sur les configurations prises en charge pour les systèmes de site Configuration Manager, consultez [Prérequis des sites et systèmes de site](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="BKMK_PlanningForWSUS"></a> Planifier l’installation de WSUS  

Les mises à jour logicielles exigent qu'une version prise en charge de WSUS soit installée sur tous les serveurs de système de site que vous configurez pour le rôle de système de site du point de mise à jour logicielle. De plus, lorsque vous n'installez pas le point de mise à jour logicielle sur le serveur de site, vous devez installer la console d'administration WSUS sur le serveur de site si elle n'est pas encore installée. Cela permet au serveur de site de communiquer avec le serveur WSUS qui est exécuté sur le point de mise à jour logicielle.  

 Quand vous utilisez WSUS sur Windows Server 2012, vous devez configurer des autorisations supplémentaires pour permettre au **Configuration Manager WSUS** dans Configuration Manager de se connecter au serveur WSUS pour effectuer des contrôles d’intégrité réguliers. Choisissez l'une des options suivantes pour configurer ces autorisations :  

-   Ajouter le compte **SYSTEM** au groupe **Administrateurs WSUS**  

-   Ajouter le compte **NT AUTHORITY\SYSTEM** en tant qu'utilisateur de la base de données WSUS (SUSDB) et configurer un minimum de l'appartenance au rôle de base de données webService  

 Pour plus d'informations sur la manière d'installer WSUS sur Windows Server 2012, voir [Installer le rôle serveur WSUS](http://go.microsoft.com/fwlink/p/?LinkId=272355) dans la bibliothèque de documentation de Windows Server 2012.  

 Lorsque vous installez plusieurs points de mise à jour logicielle sur un site principal, utilisez la même base de données WSUS pour chaque point de mise à jour logicielle d'une même forêt Active Directory. Si vous partagez la même base de données, cela permet d'atténuer considérablement, sans l'éliminer entièrement, l'impact sur les performances du client et du réseau, lequel impact peut se produire quand les clients basculent vers un nouveau point de mise à jour logicielle. Une analyse delta se produit quand même lorsqu'un client bascule vers un nouveau point de mise à jour logicielle qui partage une base de données avec l'ancien point de mise à jour logicielle, mais il s'agit d'une analyse beaucoup plus petite que celle qui se produirait si le serveur WSUS possédait sa propre base de données.  

####  <a name="BKMK_CustomWebSite"></a> Configurez WSUS pour utiliser un site Web personnalisé  
 Lorsque vous installez WSUS, vous avez la possibilité d'utiliser le site web par défaut IIS existant ou de créer un site web WSUS personnalisé. Créez un site web personnalisé pour WSUS afin qu’IIS héberge les services WSUS sur un site web virtuel dédié au lieu de partager le site web utilisé par les autres systèmes de site Configuration Manager ou d’autres applications. Ceci est particulièrement vrai lors de l'installation du rôle de système de site du point de mise à jour logicielle sur le serveur de site. Quand vous exécutez WSUS dans Windows Server 2012 ou Windows Server 2016, WSUS est configuré par défaut pour utiliser le port 8530 pour HTTP et le port 8531 pour HTTPS. Vous devez spécifier ces paramètres de port lorsque vous créez le point de mise à jour logicielle sur un site.  

####  <a name="BKMK_WSUSInfrastructure"></a> Utiliser une infrastructure WSUS existante  
 Vous pouvez sélectionner un serveur WSUS qui était actif dans votre environnement avant l’installation de Configuration Manager comme point de mise à jour logicielle. Quand le point de mise à jour logicielle est configuré, vous devez spécifier les paramètres de synchronisation. Configuration Manager se connecte au serveur WSUS qui s’exécute sur le serveur de point de mise à jour logicielle, puis configure WSUS avec les mêmes paramètres. Si vous avez synchronisé WSUS avant qu’il soit configuré comme un point de mise à jour logicielle avec des produits ou classifications que vous n'avez pas configurés dans le cadre des paramètres de synchronisation du point de mise à jour logicielle, les métadonnées des mises à jour logicielles de ces produits et classifications sont synchronisées pour toutes les métadonnées des mises à jour logicielles incluses dans la base de données WSUS, quels que soient les paramètres de synchronisation que vous avez configurés pour le point de mise à jour logicielle. Cela risque d'inclure des métadonnées de mises à jour logicielles inattendues dans la base de données du site. Vous rencontrez le même comportement quand vous ajoutez des produits ou des classifications directement dans la console d’administration WSUS, puis que vous lancez immédiatement une synchronisation. Par défaut, Configuration Manager se connecte toutes les heures à WSUS sur le point de mise à jour logicielle, et réinitialise tous les paramètres modifiés hors de Configuration Manager. Les mises à jour logicielles qui ne respectent pas les produits et classifications que vous spécifiez dans les paramètres de synchronisation expirent, puis elles sont supprimées de la base de données du site.

 Lorsqu’un serveur WSUS est configuré comme point de mise à jour logicielle, vous ne pouvez plus l’utiliser comme un serveur WSUS autonome. Si vous avez besoin d’un serveur WSUS autonome distinct qui n’est pas géré par Configuration Manager, vous devez le configurer sur un serveur différent.

####  <a name="BKMK_WSUSAsReplica"></a> Configurer WSUS comme serveur réplica  
 Quand vous créez un rôle de système de site du point de mise à jour logicielle sur un serveur de site principal, vous ne pouvez pas utiliser un serveur WSUS qui est configuré comme un réplica. Quand le serveur WSUS est configuré en tant que réplica, la configuration du serveur WSUS par Configuration Manager et la synchronisation de WSUS se soldent par un échec. Le premier point de mise à jour logicielle que vous installez sur un site principal est le point de mise à jour logicielle par défaut. Les points de mise à jour logicielle supplémentaires sur le site sont configurés en tant que réplicas du point de mise à jour logicielle par défaut.  

####  <a name="BKMK_WSUSandSSL"></a> Déterminer si WSUS doit être configuré pour utiliser le protocole SSL  
 Vous pouvez utiliser le protocole SSL pour contribuer à sécuriser le service WSUS qui s'exécute sur le point de mise à jour logicielle. WSUS utilise SSL pour authentifier les ordinateurs clients et les serveurs WSUS en aval vers le serveur WSUS. WSUS utilise également SSL pour chiffrer les métadonnées de mise à jour logicielle. Lorsque vous choisissez de sécuriser WSUS avec SSL, vous devez préparer le serveur WSUS avant d'installer le point de mise à jour logicielle.  

 Lorsque vous installez et configurez le point de mise à jour logicielle, vous devez sélectionner le paramètre **Activer les communications SSL pour le serveur WSUS** . Sinon, Configuration Manager configure le serveur WSUS pour qu’il n’utilise pas le protocole SSL. Lorsque vous activez le protocole SSL pour le serveur WSUS qui s'exécute sur un point de mise à jour logicielle, le serveur WSUS qui s'exécute sur le point de mise à jour logicielle sur tous les sites enfants doit également être configuré pour utiliser le protocole SSL.  

###  <a name="BKMK_ConfigureFirewalls"></a> Configurer des pare-feu  
 Les mises à jour logicielles présentes sur un site d’administration centrale Configuration Manager communiquent avec le serveur WSUS qui s’exécute sur le point de mise à jour logicielle qui, à son tour, communique avec la source de synchronisation pour synchroniser les métadonnées des mises à jour logicielles. Les points de mise à jour logicielle sur un site enfant communiquent avec le point de mise à jour logicielle sur le site parent. Quand il existe plusieurs points de mise à jour logicielle sur un site principal, les points supplémentaires doivent communiquer avec le premier point de mise à jour logicielle installé sur le site, qui est le point de mise à jour logicielle par défaut.  

 Il peut être nécessaire de configurer le pare-feu pour qu’il accepte les ports HTTP ou HTTPS utilisés par WSUS dans les scénarios suivants : quand vous avez un pare-feu d’entreprise entre le point de mise à jour logicielle Configuration Manager et Internet, quand vous avez un point de mise à jour logicielle et sa source de synchronisation en amont, ou quand vous avez des points de mise à jour logicielle supplémentaires. La connexion à Microsoft Update est toujours configurée pour utiliser le port 80 pour HTTP et le port 443 pour HTTPS. Vous pouvez utiliser un port personnalisé pour la connexion à partir de WSUS fonctionnant sur le point de mise à jour logicielle sur un site enfant vers WSUS fonctionnant sur le point de mise à jour logicielle sur le site parent. Quand votre stratégie de sécurité n’autorise pas la connexion, vous devez utiliser la méthode de synchronisation d’exportation et d’importation. Pour plus d’informations, consultez la section [Source de synchronisation](#BKMK_SyncSource) de cet article. Pour plus d’informations sur les ports utilisés par WSUS, consultez [Comment déterminer les paramètres de port utilisés par WSUS dans System Center Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  

#### <a name="restrict-access-to-specific-domains"></a>Restreindre l'accès à des domaines spécifiques  
 Si votre organisation n'autorise pas l'ouverture des ports et des protocoles à toutes les adresses sur le pare-feu situé entre le point de mise à jour logicielle actif et Internet, vous pouvez restreindre l'accès aux domaines suivants de sorte que WSUS et les mises à jour automatiques puissent communiquer avec Microsoft Update :  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 Il peut être nécessaire d'ajouter les adresses suivantes au pare-feu qui se trouve entre les deux systèmes de site dans les cas suivants : si les sites enfants ont un point de mise à jour logicielle ou s'il existe un point de mise à jour logicielle actif distant basé sur Internet sur un site :  

 **Point de mise à jour logicielle sur le site enfant**  

-   http://<*Nom de domaine complet du point de mise à jour logicielle sur le site enfant*>  

-   https://<*Nom de domaine complet du point de mise à jour logicielle sur le site enfant*>  

-   http://<*Nom de domaine complet du point de mise à jour logicielle sur le site parent*>  

-   https://<*Nom de domaine complet du point de mise à jour logicielle sur le site parent*>  

##  <a name="BKMK_SyncSettings"></a> Planifier des paramètres de synchronisation  
 La synchronisation des mises à jour logicielles dans Configuration Manager consiste à récupérer les métadonnées des mises à jour logicielles d’après les critères que vous configurez. Le site de plus haut niveau de votre hiérarchie, le site d’administration centrale ou le site principal autonome, synchronisent les mises à jour logicielles à partir de Microsoft Update. Vous pouvez configurer le point de mise à jour logicielle sur le site de niveau supérieur pour qu’il se synchronise avec un serveur WSUS existant qui ne figure pas dans la hiérarchie Configuration Manager. Les sites principaux enfants synchronisent les métadonnées des mises à jour logicielles à partir du point de mise à jour logicielle sur le site d'administration centrale. Avant d'installer et de configurer un point de mise à jour logicielle, utilisez cette section pour planifier les paramètres de synchronisation.  

###  <a name="BKMK_SyncSource"></a> Source de synchronisation  
 Les paramètres de la source de synchronisation du point de mise à jour logicielle spécifient l'emplacement auquel le point de mise à jour logicielle récupère les métadonnées des mises à jour logicielles et indiquent si les événements de rapports WSUS sont créés au cours du processus de synchronisation.  

-   **Source de synchronisation :** le point de mise à jour logicielle sur le site de plus haut niveau configure la source de synchronisation pour Microsoft Update par défaut. Vous pouvez synchroniser le site de niveau supérieur avec un serveur WSUS existant. Le point de mise à jour logicielle sur un site principal enfant configure la source de synchronisation en tant que point de mise à jour logicielle sur le site d'administration centrale par défaut.  

    > [!NOTE]  
    >  Le premier point de mise à jour logicielle que vous installez sur un site principal, qui est le point de mise à jour logicielle par défaut, se synchronise avec le site d’administration centrale. Les points de mise à jour logicielle supplémentaires sur le site principal se synchronisent avec le point de mise à jour logicielle par défaut sur le site principal.  

     Lorsqu'un point de mise à jour logicielle est déconnecté de Microsoft Update ou du serveur de mise à jour en amont, vous pouvez configurer la source de synchronisation pour qu'elle ne soit pas synchronisée avec une source de synchronisation configurée mais qu'elle utilise la fonction d'exportation et d'importation de l'outil WSUSUtil pour synchroniser les mises à jour logicielles. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles à partir d’un point de mise à jour logicielle déconnecté](../get-started/synchronize-software-updates-disconnected.md).  

-   **Événements de rapports WSUS :** L'agent Windows Update sur les ordinateurs clients crée des messages d'événement utilisés pour les rapports WSUS. Ces événements ne sont pas utilisés par la mise à jour logicielle dans Configuration Manager. Ainsi, l’option **Ne pas créer les événements de rapports WSUS** est sélectionnée par défaut. Si ces événements ne sont pas créés, l'ordinateur client peut se connecter au serveur WSUS uniquement lors de l'évaluation des mises à jour logicielles et des analyses de conformité. Si ces événements sont nécessaires à la génération de rapports en dehors des mises à jour logicielles dans Configuration Manager, vous devez modifier ce paramètre pour créer des événements de génération de rapports WSUS.  

###  <a name="BKMK_SyncSchedule"></a> Calendrier de synchronisation  
 Vous pouvez configurer le calendrier de synchronisation uniquement sur le point de mise à jour logicielle du site de niveau supérieur dans la hiérarchie Configuration Manager. Lorsque vous configurez le calendrier de synchronisation, le point de mise à jour logicielle se synchronise avec la source de synchronisation à la date et à l'heure que vous avez spécifiées. Le calendrier personnalisé vous permet de synchroniser les mises à jour logicielles à une date et une heure spécifiques si le nombre de demandes provenant du serveur WSUS, du serveur de site et du réseau est faible (par exemple, à 2 h 00 une fois par semaine). Sinon, vous pouvez démarrer la synchronisation sur le site de niveau supérieur à l’aide de l’action **Mises à jour logicielles de synchronisation** à partir du nœud **Toutes les mises à jour logicielles** ou **Groupes de mises à jour logicielles** dans la console Configuration Manager.  

> [!TIP]  
>  Planifiez la synchronisation des mises à jour logicielles pour qu’elle s’exécute d’après un calendrier adapté à votre environnement. Un scénario courant consiste à définir le calendrier de synchronisation des mises à jour logicielles pour qu'elle soit exécutée peu après la publication d'une mise à jour de sécurité normale de Microsoft le deuxième mardi de chaque mois, généralement appelé Patch Tuesday (Mardi correctif). Un autre scénario courant consiste à définir le calendrier de synchronisation des mises à jour logicielles pour qu'elle soit exécutée tous les jours lorsque vous utilisez des mises à jour logicielles afin de fournir des mises à jour du moteur et des définitions Endpoint Protection.  

 Une fois que le point de mise à jour logicielle a correctement terminé la synchronisation, une demande de synchronisation est envoyée aux sites enfants. Si vous avez des points de mise à jour logicielle supplémentaires sur un site principal, une demande de synchronisation est envoyée à chaque point de mise à jour logicielle. Ce processus se répète sur chaque site de la hiérarchie.  

###  <a name="BKMK_UpdateClassifications"></a> Classifications des mises à jour  
 Chaque mise à jour logicielle fait partie d'une classification particulière qui permet d'organiser les différents types de mises à jour. Pendant le processus de synchronisation, les métadonnées des mises à jour logicielles pour les classifications spécifiées seront synchronisées. Configuration Manager vous permet de synchroniser les mises à jour logicielles avec les classifications de mise à jour suivantes :  

-   **Mises à jour critiques :** spécifie des mises à jour distribuées en grand nombre, répondant à un problème spécifique qui concerne un bogue critique non lié à la sécurité.  

-   **Mises à jour de définitions :** spécifie des mises à jour pour des virus ou d'autres fichiers de définition.  

-   **Packs de fonctionnalités :** spécifie de nouvelles fonctionnalités du produit, distribuées en dehors d'une version et d'une fonctionnalité de produit qui sont généralement incluses dans la version suivante du produit.  

-   **Mises à jour de sécurité :** spécifie des mises à jour distribuées en grand nombre, répondant à un problème de sécurité spécifique à un produit.  

-   **Service Packs :** spécifie des ensembles cumulés de correctifs rattachés à une application. Ces correctifs peuvent comprendre des mises à jour de sécurité, des mises à jour critiques, des mises à jour logicielles, etc.  

-   **Outils :** spécifie des utilitaires ou des fonctionnalités permettant d'effectuer une ou plusieurs tâches.  

-   **Correctifs cumulatifs :** spécifie des ensembles cumulés de correctifs, assemblés pour faciliter leur déploiement. Ces correctifs peuvent comprendre des mises à jour de sécurité, des mises à jour critiques, des mises à jour, etc. Les correctifs cumulatifs concernent généralement un domaine particulier, tel que la sécurité ou un composant de produit.  

-   **Mises à jour :** spécifie une mise à jour d'une application ou d'un fichier déjà installé.  

 Les paramètres de classification des mises à jour sont configurés uniquement sur le site de niveau supérieur. Ils ne sont pas configurés sur le point de mise à jour logicielle des sites enfants, car les métadonnées des mises à jour logicielles du site de niveau supérieur sont répliquées sur les sites principaux enfants. Quand vous sélectionnez des classifications de mises à jour, n’oubliez pas que plus vous en sélectionnez, plus la synchronisation des métadonnées des mises à jour logicielles prend du temps.  

> [!WARNING]  
>  Il est recommandé d'effacer toutes les classifications avant de synchroniser les mises à jour logicielles pour la première fois. Après la synchronisation initiale, sélectionnez les classifications à partir des Propriétés du composant du point de mise à jour logicielle, puis relancez la synchronisation.  

###  <a name="BKMK_UpdateProducts"></a> Produits  
 Les métadonnées de chaque mise à jour logicielle définissent un ou plusieurs produits auxquels elles s'appliquent. Un produit est une édition spécifique d’un système d’exploitation ou d’une application. Un exemple d'un produit est Microsoft Windows Server 2008. Une famille de produits est le système de d'exploitation ou l'application de base d'où sont issus les produits individuels. Par exemple, Microsoft Windows est une famille de produits dont Microsoft Windows Server 2008 fait partie. Vous pouvez spécifier une famille de produits ou des produits distincts au sein d'une famille de produits.  

 Quand des mises à jour logicielles s’appliquent à plusieurs produits et qu’au moins un de ces produits a été sélectionné pour une synchronisation, tous les autres produits apparaissent dans la console Configuration Manager, même s’ils n’ont pas été sélectionnés. Par exemple, si Windows Server 2012 est le seul système d’exploitation auquel vous êtes inscrit et si une mise à jour logicielle s’applique à Windows Server 2012 et Windows Server 2012 Datacenter Edition, ces deux produits apparaîtront dans la base de données du site.  

 Les paramètres de produit sont configurés uniquement sur le site de niveau supérieur. Ils ne sont pas configurés sur le point de mise à jour logicielle des sites enfants, car les métadonnées des mises à jour logicielles du site de niveau supérieur sont répliquées sur les sites principaux enfants. Quand vous sélectionnez des produits, n’oubliez pas que plus vous en sélectionnez, plus la synchronisation des métadonnées des mises à jour logicielles prend du temps.  

> [!IMPORTANT]  
>  Configuration Manager stocke une liste de produits et de familles de produits que vous pouvez choisir quand vous installez le point de mise à jour logicielle pour la première fois. Tant que les mises à jour logicielles ne sont pas effectuées, les produits et familles de produits publiés après la publication de Configuration Manager risquent de ne pas pouvoir être sélectionnés. La synchronisation permet de mettre à jour la liste des produits et des familles de produits pouvant être sélectionnés. Il est recommandé d'effacer tous les produits avant de synchroniser les mises à jour logicielles pour la première fois. Après la synchronisation initiale, sélectionnez les produits dans les propriétés du composant du point de mise à jour logicielle, puis relancez la synchronisation.  

###  <a name="BKMK_SupersedenceRules"></a>Règles de remplacement  
 En règle générale, une mise à jour logicielle qui en remplace une autre effectue une ou plusieurs des opérations suivantes :  

-   Elle optimise, améliore ou met à jour le correctif fourni par une ou plusieurs mises à jour précédemment publiées.  

-   Elle améliore l'efficacité de son package de fichiers de mise à jour, qui est installé sur les ordinateurs clients si la mise à jour est approuvée pour l'installation. Par exemple, la mise à jour remplacée peut contenir des fichiers qui ne sont plus pertinents pour le correctif ou pour les systèmes d'exploitation pris en charge par la nouvelle mise à jour. Ainsi, ces fichiers ne sont pas inclus dans le package de fichiers de la mise à jour de remplacement.  

-   Elle met à jour un produit vers les versions les plus récentes. En d'autres termes, elle met à jour les versions qui ne concernent plus d'anciennes versions ou configurations d'un produit. Les mises à jour peuvent également remplacer d'autres mises à jour si des modifications ont été apportées pour étendre la prise en charge des langues. Par exemple, une révision récente d'une mise à jour de produit pour Microsoft Office peut supprimer la prise en charge d'un ancien système d'exploitation, mais ajouter la prise en charge de langues supplémentaires dans la version de mise à jour initiale.  

 Dans les propriétés du point de mise à jour logicielle, vous pouvez indiquer si vous souhaitez faire expirer immédiatement les mises à jour logicielles remplacées. Dans ce cas, elles ne seront pas incluses dans les nouveaux déploiements et un indicateur sera ajouté aux déploiements existants pour indiquer qu'ils contiennent une ou plusieurs mises à jour logicielles expirées. Ou bien, vous pouvez spécifier une période avant l'expiration des mises à jour logicielles remplacées, ce qui vous permet de continuer à les déployer. Examinez les scénarios suivants, dans lesquels vous devrez peut-être déployer une mise à jour logicielle remplacée :  

-   une mise à jour logicielle de remplacement prend en charge uniquement les versions les plus récentes du système d'exploitation, mais certains de vos ordinateurs clients exécutent des versions antérieures du système d'exploitation ;  

-   une mise à jour logicielle de remplacement présente des conditions d'applications plus restreintes que la mise à jour qu'elle remplace, ce qui peut la rendre inadaptée à certains ordinateurs clients ;  

-   une mise à jour logicielle de remplacement n'a pas été approuvée pour le déploiement dans votre environnement de production.  

    > [!NOTE]  
    > Quand Configuration Manager définit une mise à jour logicielle remplacée avec l’état **Expiré**, celle-ci n’est pas définie avec l’état **Refusé** dans WSUS. Toutefois, quand la tâche de nettoyage WSUS s’exécute, les mises à jour définies avec l’état **Expiré** dans Configuration Manager passent à l’état **Refusé** sur le serveur WSUS, et l’agent Windows Update sur les ordinateurs ne recherche plus ces mises à jour. Cela signifie que les clients continuent à effectuer des recherches pour une mise à jour qui a expiré jusqu’à l’exécution de la tâche de nettoyage. Pour plus d’informations sur la tâche de nettoyage WSUS, consultez [Maintenance des mises à jour logicielles](/sccm/sum/deploy-use/software-updates-maintenance).

###  <a name="BKMK_UpdateLanguages"></a> Langues  
 Les paramètres de langue du point de mise à jour logicielle permettent de configurer les langues pour lesquelles les détails du résumé (les métadonnées des mises à jour logicielles) sont synchronisés pour les mises à jour logicielles, ainsi que les langues des fichiers de mise à jour logicielle qui sont téléchargés pour les mises à jour.  

#### <a name="software-update-file"></a>Fichier de mise à jour logicielle  
 Les langues configurées dans le paramètre **Fichier de mise à jour logicielle** dans les propriétés du point de mise à jour logicielle désignent l'ensemble de langues par défaut qui sera disponible lors du téléchargement des mises à jour logicielles sur un site. Vous pouvez modifier les langues qui sont sélectionnées par défaut à chaque fois que des mises à jour logicielles sont téléchargées ou déployées. Lors du téléchargement, les fichiers de mise à jour logicielle correspondant aux langues configurées sont téléchargés à l'emplacement source du package de déploiement, si les fichiers de mise à jour logicielle sont disponibles dans la langue sélectionnée. Ils sont ensuite copiés dans la bibliothèque de contenu du serveur de site, puis sur les points de distribution configurés pour le package.  

 Les paramètres de langue des fichiers de mise à jour logicielle doivent être configurés avec les langues les plus souvent utilisées dans votre environnement. Par exemple, si des ordinateurs clients attribués au site utilisent surtout l'anglais et le japonais dans le système d'exploitation ou les applications, et si très peu d'autres langues sont utilisées sur ce site, sélectionnez l'anglais et le japonais dans la colonne **Fichier de mise à jour logicielle** lors du téléchargement ou du déploiement de la mise à jour logicielle, et désactivez les cases correspondant aux autres langues. Vous pourrez ainsi utiliser les paramètres par défaut sur la page **Sélection de la langue** des Assistants de déploiement et de téléchargement. En outre, vous empêchez ainsi le téléchargement des fichiers de mise à jour inutiles. Ce paramètre est configuré sur chaque point de mise à jour logicielle de la hiérarchie Configuration Manager.  

#### <a name="summary-details"></a>Détails du résumé  
 Au cours du processus de synchronisation, les informations sur les détails du résumé (métadonnées des mises à jour logicielles) sont mises à jour pour les mises à jour logicielles dans les langues spécifiées. Les métadonnées proposent des informations sur la mise à jour logicielle, telles que le nom, la description, les produits pris en charge par la mise à jour, la classification de la mise à jour, l'ID de l'article, l'URL de téléchargement, les critères d'application, etc.  

 Les paramètres des détails du résumé sont configurés uniquement sur le site de niveau supérieur. Ils ne sont pas configurés sur le point de mise à jour logicielle des sites enfants, car les métadonnées des mises à jour logicielles du site d'administration centrale sont répliquées sur ces sites, via une réplication de fichiers. Lorsque vous sélectionnez les langues des détails du résumé, vous devez choisir uniquement les langues dont votre environnement a besoin. Plus vous choisissez de langues, plus la synchronisation des métadonnées des mises à jour logicielles prendra du temps. Configuration Manager affiche les métadonnées des mises à jour logicielles en fonction des paramètres régionaux du système d’exploitation sur lequel s’exécute la console Configuration Manager. Si les propriétés localisées pour les mises à jour logicielles ne sont pas disponibles dans la langue du système d'exploitation, les informations sur les mises à jour logicielles s'affichent en anglais.  

> [!IMPORTANT]  
>  Veillez à sélectionner toutes les langues des détails du résumé dont vous avez besoin dans la hiérarchie Configuration Manager. Lorsque le point de mise à jour logicielle du site de niveau supérieur se synchronise avec la source de synchronisation, les langues des détails du résumé sélectionnées déterminent les métadonnées de mises à jour logicielles récupérées. Si les langues des détails du résumé sont modifiées après au moins une exécution de la synchronisation, seules les métadonnées de mise à jour logicielle des langues des détails du résumé modifiées se rapportant aux mises à jour logicielles nouvelles ou mises à jour sont récupérées. Les mises à jour logicielles qui ont déjà été synchronisées ne sont pas mises à jour à partir des nouvelles métadonnées des langues modifiées, sauf si une modification est apportée à la mise à jour logicielle au niveau de la source de synchronisation.  

##  <a name="BKMK_MaintenanceWindow"></a> Planification d'une fenêtre de maintenance pour les mises à jour logicielles  
 Vous pouvez ajouter une fenêtre de maintenance dédiée à l’installation de mises à jour logicielles. Vous pouvez configurer une fenêtre de maintenance générale et une fenêtre de maintenance distincte pour les mises à jour logicielles. Lorsque vous disposez d'une fenêtre de maintenance générale et d'une fenêtre de maintenance des mises à jour logicielles, les clients installent des mises à jour logicielles uniquement dans le cadre de la fenêtre de maintenance des mises à jour logicielles. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="BKMK_RestartOptions"></a> Options de redémarrage pour les clients Windows 10 après l’installation de mises à jour logicielles
Quand une mise à jour logicielle nécessitant un redémarrage est déployée à l’aide de Configuration Manager et installée sur un ordinateur, un redémarrage en attente est planifié et une boîte de dialogue de redémarrage s’affiche.

À compter de Configuration Manager version 1606, les options **Mettre à jour et redémarrer**et **Mettre à jour et arrêter** sont disponibles sur les ordinateurs Windows 10 dans les options d’alimentation de Windows chaque fois qu’un redémarrage est en attente pour une mise à jour logicielle Configuration Manager. Après l’utilisation de l’une de ces options, la boîte de dialogue de redémarrage ne s’affiche pas quand l’ordinateur redémarre.

Dans les versions précédentes de Configuration Manager, quand un redémarrage est en attente pour un ordinateur Windows 8 ou version ultérieure, et quand vous arrêtez ou redémarrez l’ordinateur via les options d’alimentation de Windows (au lieu de la boîte de dialogue de redémarrage), la boîte de dialogue de redémarrage reste affichée après le redémarrage de l’ordinateur, et celui-ci doit toujours redémarrer à l’échéance configurée.


## <a name="next-steps"></a>Étapes suivantes
Quand vous planifiez des mises à jour logicielles, consultez [Préparer la gestion des mises à jour logicielles](../get-started/prepare-for-software-updates-management.md).

**Pour plus d’informations :** <br/>
[Notions de base de Configuration Manager as a service et Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service.md)