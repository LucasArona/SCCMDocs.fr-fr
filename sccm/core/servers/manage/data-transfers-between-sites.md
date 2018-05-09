---
title: Transfert de données
titleSuffix: Configuration Manager
description: Découvrez comment Configuration Manager déplace les données entre les sites et comment vous pouvez gérer le transfert des données sur votre réseau.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 45fb1bc31a7e888ca4caa21a710e74ec0fde422c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Transfert de données entre sites dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager utilise la **réplication basée sur les fichiers** et la **réplication de base de données** pour transférer différents types d’informations entre les sites. Découvrez comment Configuration Manager déplace les données entre les sites et comment vous pouvez gérer le transfert des données sur votre réseau.  


## <a name="bkmk_fileroute"></a> File-based replication  
Configuration Manager utilise la réplication basée sur les fichiers pour transférer des données basées sur les fichiers entre les sites dans votre hiérarchie. Ces données incluent les applications et les packages que vous voulez déployer sur des points de distribution dans des sites enfants, ainsi que les enregistrements de données de découverte non traités qui sont transférés vers les sites parents puis traités.  

La communication basée sur les fichiers entre les sites utilise le protocole SMB (**Server Message Block**) sur le port TCP/IP 445. Vous pouvez spécifier la limitation de bande passante et le mode impulsion pour contrôler la quantité de données transférées sur le réseau, et vous pouvez utiliser des planifications pour contrôler à quel moment les données sont envoyées sur le réseau.  

### <a name="bkmk_routes"></a> Itinéraires de réplication de fichiers  
Les informations suivantes peuvent vous aider à configurer et à utiliser les itinéraires de réplication de fichiers.  

#### <a name="file-replication-route"></a>Itinéraire de réplication de fichiers

Chaque itinéraire de réplication de fichiers identifie un site de destination vers lequel les données basées sur des fichiers peuvent être transférées. Chaque site prend en charge un seul itinéraire de réplication de fichiers vers un site de destination spécifique.  

Vous pouvez modifier les paramètres suivants pour les itinéraires de réplication de fichiers :  

-  **Compte de réplication de fichiers**. Ce compte se connecte au site de destination et écrit des données dans le partage **SMS_Site** de ce site. Les données écrites dans ce partage sont traitées par le site de réception. Par défaut, quand un site est ajouté à la hiérarchie, Configuration Manager attribue le compte d’ordinateur du serveur de site du nouveau site comme Compte de réplication de fichiers de ce site. Ce compte est ensuite ajouté au groupe **SMS_SiteToSiteConnection_&lt;code_site\>** du site de destination, un groupe local sur l’ordinateur qui accorde l’accès au partage SMS_Site. Vous pouvez modifier ce compte en un compte d'utilisateur Windows. Si vous changez le compte, veillez à ajouter le nouveau compte au groupe **SMS_SiteToSiteConnection_&lt;code_site\>** du site de destination.  

    > [!NOTE]  
    >  Les sites secondaires utilisent toujours le compte d'ordinateur du serveur de site secondaire en tant que **Compte de réplication de fichiers**.  

-  **Planification**. Vous pouvez établir le calendrier de chaque itinéraire de réplication de fichiers pour restreindre le type de données et la période de transfert des données vers le site de destination.  
-  **Limites du taux de transfert**. Vous pouvez spécifier des limites de taux de transfert pour chaque itinéraire de réplication de fichiers, afin de contrôler la bande passante réseau utilisée lorsque le site transfère les données vers le site de destination :  

    -  Utilisez l'option **Mode impulsion** pour spécifier la taille des blocs de données envoyés vers le site de destination. Vous pouvez également spécifier un délai entre l’envoi de chaque bloc de données. Utilisez cette option lorsque vous devez envoyer des données via une connexion réseau à très faible bande passante vers le site de destination. Par exemple, vous pouvez forcer l'envoi de 1 Ko de données toutes les cinq secondes, mais empêcher l'envoi de 1 Ko toutes les trois secondes, quelle que soit la vitesse de la liaison ou son utilisation.
    -  Utilisez l'option **Limité aux taux de transfert maximaux indiqués par heure** pour permettre à un site d'envoyer des données vers un site de destination en utilisant uniquement le pourcentage de temps spécifié. Quand vous utilisez cette option, Configuration Manager n’identifie pas la bande passante disponible du réseau, mais divise plutôt le temps pendant lequel il peut envoyer des données en périodes plus petites. Ensuite, les données sont envoyées pendant une courte plage horaire, suivie de plages horaires pendant lesquelles aucune donnée n’est envoyée. Par exemple, si le taux maximal est fixé à **50 %**, Configuration Manager transmet les données pendant une durée, suivie d’une période d’une durée égale pendant laquelle aucune donnée n’est envoyée. La taille effective des donnés (taille des blocs de données) n’est pas gérée. En revanche, seule la durée pendant laquelle des données sont envoyées est gérée.  

        > [!CAUTION]  
        > Par défaut, un site peut utiliser jusqu'à trois **envois simultanés** pour transférer des données vers un site de destination. Lorsque vous définissez des limites de taux pour un itinéraire de réplication de fichiers, les **envois simultanés** dans le cadre de l'envoi de données vers ce site sont limités à un. Cela s'applique même lorsque l'option **Limiter la bande passante disponible (%)** est définie sur **100 %**. Par exemple, si vous utilisez les paramètres par défaut pour l’expéditeur, le taux de transfert vers le site de destination est réduit à un tiers de la capacité par défaut.  

-  Vous pouvez configurer un itinéraire de réplication de fichiers entre deux sites secondaires pour acheminer du contenu basé sur des fichiers entre ces sites.  

Pour gérer un itinéraire de réplication de fichiers, dans l’espace de travail **Administration**, développez le nœud **Configuration de la hiérarchie**, puis sélectionnez **Réplication de fichiers**.  

#### <a name="sender"></a>Expéditeur

Chaque site a un expéditeur. L'expéditeur gère la connexion réseau entre un site et un site de destination et peut établir des connexions vers plusieurs sites à la fois. Pour se connecter à un site, l'expéditeur utilise l'itinéraire de réplication de fichiers vers le site pour identifier le compte à utiliser pour établir la connexion réseau. L’expéditeur utilise également ce compte pour écrire des données dans le partage SMS_Site du site de destination.  

Par défaut, l'expéditeur écrit des données sur un site de destination en utilisant plusieurs **envois simultanés**, généralement appelés « thread ». Chaque envoi simultané (ou « thread ») peut transférer un objet basé sur un fichier différent vers le site de destination. Par défaut, lorsque l'expéditeur commence à envoyer un objet, il continue d'écrire des blocs de données pour cet objet jusqu'à la fin de l'envoi de l'objet complet. Une fois que toutes les données de l'objet ont été envoyées, l'envoi d'un nouvel objet peut commencer sur ce thread.  

Vous pouvez modifier les paramètres suivants pour un expéditeur :  

-  **Nombre maximal d’envois simultanés**. Par défaut, chaque site utilise cinq envois simultanés, dont trois peuvent être utilisés dans le cadre de l’envoi de données vers un site de destination quelconque. En augmentant ce nombre, vous pouvez augmenter le débit des données échangées entre les sites, car Configuration Manager peut transférer davantage de fichiers à la fois. Cela a également pour effet d'augmenter la demande en bande passante entre les sites.  

-  **Paramètres de nouvelle tentative**. Par défaut, chaque site effectue deux nouvelles tentatives de connexion en cas de problème, avec un délai d’une minute entre deux essais. Vous pouvez modifier le nombre de tentatives de connexion du site, ainsi que le délai d’attente entre les tentatives.  

Pour gérer l’expéditeur pour un site, dans l’espace de travail **Administration**, développez le nœud **Configuration du site**, sélectionnez le nœud **Sites**, puis cliquez sur **Propriétés** pour le site à gérer. Sélectionnez l’onglet **Expéditeur** pour modifier les paramètres de l’expéditeur.  

## <a name="bkmk_dbrep"></a> Database replication  
La réplication de base de données Configuration Manager utilise SQL Server pour transférer les données et fusionner les modifications apportées à la base de données d’un site avec les informations stockées dans la base de données sur d’autres sites de la hiérarchie. Notez les éléments suivants sur la réplication de base de données :

-  Tous les sites partagent les mêmes informations.  
-  Quand vous installez un site dans une hiérarchie, la réplication de base de données est établie automatiquement entre le nouveau site et son site parent désigné.  
-  Une fois l'installation du site terminée, la réplication de base de données démarre automatiquement.  

Quand vous ajoutez un nouveau site à une hiérarchie, Configuration Manager crée une base de données générique sur le nouveau site. Ensuite, le site parent crée un instantané des données appropriées dans sa base de données, puis transfère cet instantané vers le nouveau site par réplication basée sur des fichiers. Le nouveau site utilise ensuite le programme de copie en bloc de SQL Server pour charger les informations dans sa copie locale de la base de données Configuration Manager. Une fois l'instantané chargé, chaque site effectue une réplication de base de données avec l'autre site.  

Pour répliquer des données entre les sites, Configuration Manager utilise son propre service de réplication de base de données. Le service de réplication de base de données utilise le suivi des modifications de SQL Server pour surveiller les modifications apportées à la base de données du site local, puis réplique ces modifications sur les autres sites à l’aide de SQL Server Service Broker (SSB). Par défaut, ce processus utilise le port TCP/IP 4022.  

Configuration Manager regroupe les données répliquées par la réplication de base de données dans différents groupes de réplication. Notez les éléments suivants sur les groupes de réplication :

-  À chaque groupe de réplication correspond une planification de réplication fixe et distincte qui détermine la fréquence de réplication vers d'autres sites des modifications apportées aux données.  

     Par exemple, une modification apportée à une configuration d’administration basée sur des rôles est répliquée rapidement sur d’autres sites pour que ces modifications soient appliquées dès que possible. En revanche, une modification de configuration de plus basse priorité, telle qu’une demande d’installation d’un nouveau site secondaire, est répliquée avec moins d’urgence. Une nouvelle demande de site peut mettre plusieurs minutes pour atteindre le site principal de destination.  

-   Vous pouvez modifier les paramètres suivants de réplication de base de données :  

    -  **Liens de réplication de base de données**. Contrôlez quand un trafic spécifique traverse le réseau.  
    -  **Vues distribuées**. Changez les paramètres des liens de réplication qui permettent aux demandes formulées sur un site d’administration centrale relatives à des données de site sélectionnées d’accéder à ces données directement à partir de la base de données d’un site principal enfant.  
    -  **Planifications**. Spécifiez quand un lien de réplication doit être utilisé et quand différents types de données de site sont répliqués.  
    -  **Totalisation**. Changez les paramètres de totalisation des données concernant le trafic réseau qui traverse les liens de réplication. La totalisation a lieu toutes les 15 minutes par défaut et est utilisée pour la réplication de base de données dans les rapports.  
    -  **Seuils de réplication de base de données**. Définissez quand les liens sont signalés comme détériorés ou en échec. Vous pouvez également configurer à quel moment Configuration Manager doit déclencher des alertes au sujet des liens de réplication dont l’état est Détérioré ou Échec.  

Configuration Manager classe les données qu’il réplique via la réplication de base de données comme **données globales** ou **données de site**. Lorsqu'une réplication de base de données se produit, les modifications apportées aux données globales et aux données de site sont transférées via le lien de réplication de base de données. Les données globales peuvent être répliquées vers un site parent ou enfant. Les données de site sont répliquées uniquement vers un site parent. Un troisième type de données, les données locales, n’est pas répliqué vers d’autres sites. Les données locales sont des informations qui ne sont pas requises par les autres sites. Notez les éléments suivants concernant les types de données :  

-  **Données globales**. Les données globales font référence aux objets créés par l'administrateur et qui sont répliquées sur tous les sites dans la hiérarchie, bien que les sites secondaires reçoivent uniquement un sous-ensemble des données globales, en tant que données globales proxy. Les déploiements logiciels, les mises à jour logicielles, les définitions de regroupement et les étendues de la sécurité de l’administration basée sur les rôles sont autant d’exemples de données globales. Les administrateurs peuvent créer des données globales sur des sites d'administration centrale et des sites principaux.  
-  **Données de site**. Les données de site font référence aux informations opérationnelles créées par les sites principaux Configuration Manager et les clients qui sont sous la hiérarchie de sites principaux. Les données de site sont répliquées vers le site d'administration centrale mais pas vers d'autres sites principaux. Les données de site incluent les données d’inventaire matériel, les messages d’état, les alertes et les résultats de regroupements basés sur des requêtes. Les données de site ne peuvent être consultées que sur le site d’administration centrale et sur le site principal d’où proviennent les données. Les données de site ne peuvent être modifiées que sur le site principal sur lequel elles ont été créées.  

     Toutes les données de site sont répliquées vers le site d’administration centrale. Ce site effectue l’administration et la création de rapports pour toute la hiérarchie des sites.  

Les sections suivantes détaillent les paramètres que vous pouvez modifier pour gérer la réplication de base de données.  

### <a name="bkmk_Dblinks"></a> liens de réplication de base de données  
Quand vous installez un nouveau site dans une hiérarchie, Configuration Manager crée automatiquement un lien de réplication de base de données entre le site parent et le nouveau site. Un lien unique est créé pour connecter les deux sites.  

Vous pouvez modifier les paramètres pour chaque lien de réplication de base de données afin de contrôler plus aisément le transfert de données via le lien de réplication. Chaque lien de réplication prend en charge des configurations distinctes. Les contrôles pour les liens de réplication de base de données sont les suivants :  

-  Arrêtez la réplication de données de site sélectionnées à partir d’un site principal vers le site d’administration centrale, afin que le site d’administration centrale puisse accéder directement à ces données à partir de la base de données du site principal.  
-  Planifiez les données de site sélectionnées à transférer d’un site principal enfant vers le site d’administration centrale.
-  Définissez les paramètres qui déterminent quand un lien de réplication de base de données a l’état Détérioré ou Échec.
-  Spécifiez à quel moment déclencher des alertes dans le cas d’un lien de réplication en échec.
-  Spécifiez la fréquence à laquelle Configuration Manager résume les données sur le trafic de réplication qui utilise le lien de réplication. Ces données sont utilisées dans les rapports.

Pour configurer un lien de réplication de base de données, dans la console Configuration Manager, dans le nœud **Réplication de la base de données**, modifiez les propriétés du lien. Ce nœud apparaît dans l’espace de travail **Surveillance** et dans l’espace de travail **Administration**, sous le nœud **Configuration de la hiérarchie**. Vous pouvez modifier un lien de réplication à partir du site parent ou du site enfant du lien de réplication.  

> [!TIP]  
> Vous pouvez modifier les liens de réplication de base de données à partir du nœud **Réplication de la base de données** dans chaque espace de travail. Toutefois, lorsque vous utilisez le nœud **Réplication de la base de données** dans l’espace de travail **Surveillance**, vous pouvez également consulter l’état de la réplication de base de données des liens de réplication et accéder à l’outil Analyseur de lien de réplication pour mieux identifier les problèmes de réplication de base de données.  

Pour plus d'informations sur la configuration des liens de réplication, voir [Contrôles de réplication de la base de données du site](#BKMK_DBRepControls). Pour plus d’informations sur la surveillance de la réplication, consultez [Comment surveiller des liens de réplication de la base de données et l’état de la réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) dans la rubrique [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Pour planifier des liens de réplication de base de données, aidez-vous des informations figurant dans les sections suivantes.  

### <a name="bkmk_distviews"></a> vues distribuées  
Les vues distribuées permettent aux demandes formulées sur un site d’administration centrale relatives à des données de site sélectionnées d’accéder à ces données directement à partir de la base de données d’un site principal enfant. L’accès direct évite d’avoir à répliquer ces données de site du site principal vers le site d’administration centrale. Comme chaque lien de réplication est indépendant des autres liens de réplication, vous pouvez utiliser les vues distribuées uniquement sur les liens de réplication de votre choix. Vous ne pouvez pas utiliser les vues distribuées entre un site principal et un site secondaire.  

Les vues distribuées peuvent offrir les avantages suivants :  

-  Elles diminuent la charge du processeur lors du traitement des modifications apportées à la base de données sur le site d’administration centrale et les sites principaux.
-  Elles réduisent la quantité de données transférées sur le réseau à destination du site d’administration centrale.
-  Elles améliorent les performances du serveur SQL Server qui héberge la base de données du site d’administration centrale.
-  Elles réduisent l’espace disque utilisé par la base de données sur le site d’administration centrale.

Vous pouvez envisager d’utiliser des vues distribuées lorsqu’un site principal est situé à proximité du site d’administration centrale sur le réseau et que les deux sites sont toujours actifs et connectés. En effet, les vues distribuées remplacent la réplication des données sélectionnées entre les sites par des connexions directes entre les serveurs SQL Server de chaque site. Une connexion directe est établie chaque fois qu’une demande portant sur ces données est formulée sur le site d’administration centrale. En règle générale, les demandes de données que vous pouvez autoriser pour les vues distribuées sont formulées lorsque vous exécutez des rapports ou des requêtes, lorsque vous consultez des informations dans l’Explorateur de ressources et par l’évaluation des regroupements lorsque ceux-ci incluent des règles basées sur les données de site.  

Par défaut, les vues distribuées sont désactivées pour chaque lien de réplication. Lorsque vous activez les vues distribuées pour un lien de réplication, vous sélectionnez les données de site qui ne seront pas répliquées vers le site d’administration centrale via ce lien. Le site d’administration centrale accède à ces données directement à partir de la base de données du site principal enfant qui partage le lien. Pour les vues distribuées, vous pouvez configurer les types de données de site suivants :  

-  Données d'inventaire matériel des clients
-  Données d'inventaire et de contrôle de logiciel des clients
-  Messages d'état en provenance des clients, du site principal et de tous les sites secondaires

Sur le plan opérationnel, les vues distribuées sont invisibles pour un utilisateur administratif qui consulte des données dans la console Configuration Manager ou dans des rapports. Quand une demande est effectuée pour des données activées pour les vues distribuées, le serveur SQL Server qui héberge la base de données du site d’administration centrale accède directement au serveur SQL Server du site principal enfant afin d’extraire les informations. Par exemple, vous utilisez une console Configuration Manager au niveau du site d’administration centrale pour demander des informations sur l’inventaire matériel de deux sites alors qu’un seul des deux possède un inventaire matériel compatible avec une vue distribuée. Les informations d'inventaire pour les clients du site qui n'est pas configuré pour les vues distribuées sont extraites de la base de données au niveau du site d'administration centrale. Les informations d’inventaire des clients du site qui est configuré pour les vues distribuées sont accessibles à partir de la base de données au niveau du site principal enfant. Ces informations apparaissent dans la console Configuration Manager ou dans un rapport sans que la source soit identifiée.  

Tant qu’un lien de réplication comporte un type de données activé pour les vues distribuées, le site principal enfant ne réplique pas ces données sur le site d’administration centrale. Dès que vous désactivez les vues distribuées pour un type de données, le site principal enfant reprend la réplication des données sur le site d’administration centrale dans le cadre d’une réplication normale des données. Toutefois, pour que ces données soient disponibles au niveau du site d’administration centrale, les groupes de réplication qui les contiennent doivent être réinitialisés entre le site principal et le site d’administration centrale. De même, après la désinstallation d’un site principal dont les vues distribuées sont activées, le site d’administration centrale doit effectuer la réinitialisation de ses données pour que vous puissiez accéder aux données activées pour les vues distribuées sur le site d’administration centrale.  

> [!IMPORTANT]  
> Lorsque vous utilisez les vues distribuées sur un lien de réplication quelconque dans la hiérarchie des sites, vous devez les désactiver pour tous les liens de réplication avant de désinstaller un site principal. Pour plus d’informations, consultez [Désinstaller un site principal configuré avec des vues distribuées](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Prérequis et limitations des vues distribuées  

-  Vous pouvez utiliser les vues distribuées uniquement sur des liens de réplication entre un site d’administration centrale et un site principal.
- Le site d’administration centrale doit utiliser une édition Enterprise de SQL Server. Le site principal n’a pas cette exigence.
-  Le site d'administration centrale peut disposer d'une seule instance du fournisseur SMS installée, et cette instance doit être installée sur le serveur de base de données du site. Cette contrainte sert à prendre en charge l’authentification Kerberos requise pour permettre au serveur SQL Server au niveau du site d’administration centrale d’accéder au serveur SQL Server au niveau du site principal enfant. Il n'existe aucune limitation sur le fournisseur SMS au niveau du site principal enfant.
-  Le site d'administration centrale peut disposer d'un seul point SQL Server Reporting Services installé, et ce dernier doit se trouver sur le serveur de base de données du site. Cette contrainte sert à prendre en charge l’authentification Kerberos requise pour permettre au serveur SQL Server au niveau du site d’administration centrale d’accéder au serveur SQL Server au niveau du site principal enfant.
-  La base de données du site ne peut pas être hébergée sur un cluster SQL Server.
-  La base de données du site ne peut pas être hébergée sur un groupe de disponibilité SQL Server Always On.
-  Le compte d’ordinateur du serveur de base de données du site d’administration centrale requiert des autorisations de lecture pour la base de données du site principal.

> [!IMPORTANT]  
>  Les vues distribuées et les planifications des périodes où les données peuvent être répliquées sont des paramètres qui s’excluent mutuellement pour un lien de réplication de base de données.  

### <a name="BKMK_schedules"></a> Planifier les transferts de données de site sur les liens de réplication de la base de données  
Pour mieux contrôler la bande passante réseau utilisée pour répliquer les données de site depuis un site principal enfant vers son site d'administration centrale, vous pouvez planifier le moment auquel un lien de réplication est utilisé, ainsi que spécifier quand les différents types de données de site se répliquent. Vous pouvez contrôler le moment auquel le site principal réplique les messages d'état, l'inventaire et les données de contrôle. Les liens de réplication de la base de données des sites secondaires ne prennent pas en charge les planifications des données de site. Le transfert de données globales ne peut pas être planifié.  

Quand vous configurez une planification de lien de réplication de la base de données, vous pouvez restreindre le transfert des données de site sélectionnées depuis le site principal vers le site d'administration centrale et vous pouvez configurer différentes heures pour répliquer des types différents de données de site.  

> [!IMPORTANT]  
> Les vues distribuées et les planifications relatives aux dates de réplication des données sont des configurations qui s'excluent mutuellement pour un lien de réplication de la base de données.  

### <a name="BKMK_SummarizeDBReplication"></a> Synthèse du trafic de réplication de la base de données  
Chaque site réalise régulièrement une synthèse des données sur le trafic réseau qui traverse les liens de réplication de la base de données pour ce site. Les données résumées sont utilisées dans les rapports pour la réplication de la base de données. Les deux sites sur un lien de réplication résument le trafic réseau qui traverse le lien de réplication. Le résumé des données est effectué par le serveur SQL Server qui héberge la base de données du site. Une fois les données résumées, les informations sont répliquées vers d’autres sites en tant que données globales.  

Par défaut, le résumé se produit toutes les 15 minutes. Pour modifier la fréquence de synthèse du trafic réseau, dans les propriétés du lien de réplication de la base de données, modifiez la valeur **Intervalle de résumé**. La fréquence de synthèse affecte les informations affichées dans les rapports sur la réplication de la base de données. Vous pouvez choisir un intervalle compris entre 5 et 60 minutes. Lorsque vous augmentez la fréquence de synthèse, vous augmentez la charge de traitement sur le serveur SQL Server au niveau de chaque site sur le lien de réplication.  

### <a name="BKMK_DBRepThresholds"></a> Seuils de réplication de base de données  
Les seuils de réplication de la base de données définissent le moment auquel un lien de réplication de la base de données est signalé comme étant détérioré ou en état d'échec. Par défaut, un lien est défini comme détérioré quand l’un des groupes de réplication ne parvient pas à terminer la réplication à l’issue de 12 tentatives consécutives. Le lien est défini en état d’échec quand l’un des groupes de réplication ne parvient pas à être répliqué à l’issue de 24 tentatives consécutives.  

Vous pouvez spécifier des valeurs personnalisées pour ajuster le moment auquel Configuration Manager signale qu’un lien de réplication est détérioré ou en état d’échec. L’ajustement du moment auquel Configuration Manager signale chaque état de vos liens de réplication de la base de données peut vous aider à surveiller l’intégrité de la réplication de la base de données avec précision.  

Comme il est possible qu’un ou plusieurs groupes de réplication ne parviennent pas à être répliqués alors que les autres groupes de réplication continuent d’être répliqués correctement, prévoyez de vérifier l’état de réplication d’un lien de réplication dès qu’un état détérioré est signalé. S'il existe des délais récurrents pour des groupes de réplication et qu'ils ne présentent pas de problème, où lorsque la liaison réseau entre les sites dispose d'une faible bande passante disponible, envisagez de modifier le nombre de nouvelles tentatives pour l'état détérioré ou en échec du lien. En augmentant le nombre de nouvelles tentatives à effectuer avant de définir le lien comme détérioré ou en état d’échec, vous pouvez éliminer les faux avertissements liés à des problèmes connus et suivre l’état du lien de manière plus précise.  

Prenez en compte également l’intervalle de synchronisation de réplication pour chaque groupe de réplication afin de comprendre la fréquence de réplication de ce groupe. Pour afficher l’**intervalle de synchronisation** des groupes de réplication, dans l’espace de travail **Surveillance**, sous le nœud **Réplication de la base de données**, sélectionnez l’onglet **Détail de la réplication** d’un lien de réplication.  

Pour plus d’informations sur la manière de surveiller la réplication de la base de données, y compris la manière d’afficher l’état de réplication, consultez [Comment surveiller des liens de réplication de la base de données et l’état de la réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) dans la rubrique [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Pour plus d’informations sur la configuration des seuils de réplication de base de données, voir [Contrôles de réplication de la base de données du site](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Contrôles de réplication de la base de données du site  
Vous pouvez modifier les paramètres de chaque base de données de site pour mieux contrôler la bande passante réseau utilisée pour la réplication de base de données. Ces paramètres s’appliquent uniquement à la base de données de site dans laquelle vous configurez les paramètres. Ces paramètres sont toujours utilisés lorsque le site réplique des données via la réplication de base de données vers un autre site.  

Les contrôles de réplication que vous pouvez modifier pour chaque base de données de site sont les suivants :  

-  Modifiez le port SSB.  
-  Configurez le délai d’attente avant que les échecs de réplication déclenchent la réinitialisation de la copie de la base de données du site.  
-  Configurez une base de données de site afin qu'elle compresse les données qu'elle réplique par réplication de base de données. Les données sont compressées uniquement pour le transfert entre les sites et non pour le stockage dans la base de données du site sur l'un des sites.  

Pour modifier les paramètres des contrôles de réplication d’une base de données de site, dans la console Configuration Manager, dans le nœud **Réplication de la base de données**, modifiez les propriétés de la base de données de site. Ce nœud apparaît sous le nœud **Configuration de la hiérarchie** dans l'espace de travail **Administration** et également dans l' **espace de travail Surveillance**. Pour modifier les propriétés de la base de données de site, sélectionnez le lien de réplication entre les sites, puis ouvrez soit **Propriétés de la base de données parent**, soit **Propriétés de la base de données enfant**.  

> [!TIP]  
> Vous pouvez configurer les contrôles de réplication de la base de données à partir du nœud **Réplication de la base de données** dans l'un ou l'autre espace de travail. Toutefois, lorsque vous utilisez le nœud **Réplication de la base de données** dans l’espace de travail **Surveillance**, vous pouvez également afficher l’état de réplication de base de données d’un lien de réplication, puis accéder à l’outil Analyseur de lien de réplication pour mieux identifier les problèmes de réplication.  
