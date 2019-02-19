---
title: Installer et configurer un point de mise à jour logicielle
titleSuffix: Configuration Manager
description: Il doit y avoir un point de mise à jour logicielle installé sur le site d’administration centrale et sur les sites principaux pour permettre l’évaluation de la conformité des mises à jour logicielles et le déploiement des mises à jour logicielles sur les clients.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b099a645-6434-498f-a408-1d438e394396
ms.collection: M365-identity-device-management
ms.openlocfilehash: b51b8245de3c446657e328456f81bd40ebf71261
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141855"
---
# <a name="install-and-configure-a-software-update-point"></a>Installer et configurer un point de mise à jour logicielle  

*S’applique à : System Center Configuration Manager (Current Branch)*


> [!IMPORTANT]  
>  Avant d’installer le rôle de système de site du point de mise à jour logicielle, vous devez vérifier que le serveur a les dépendances nécessaires et qu’il détermine l’infrastructure du point de mise à jour logicielle sur le site. Pour plus d’informations sur la planification des mises à jour logicielles et pour savoir comment déterminer l’infrastructure de votre point de mise à jour logicielle, consultez [Planifier les mises à jour logicielles](../plan-design/plan-for-software-updates.md).  

 Le point de mise à jour logicielle est nécessaire sur le site d’administration centrale et les sites principaux pour permettre l’évaluation de la conformité des mises à jour logicielles et pour déployer des mises à jour logicielles sur des clients. Le point de mise à jour de logicielle est facultatif sur les sites secondaires. Le rôle de système de site du point de mise à jour logicielle doit être créé sur un serveur sur lequel WSUS est installé. Le point de mise à jour logicielle interagit avec les services WSUS pour configurer les paramètres de mise à jour logicielle et demander la synchronisation des métadonnées de mises à jour logicielles. Dans une hiérarchie Configuration Manager, vous devez installer et configurer le point de mise à jour logicielle d’abord sur le site d’administration centrale, puis sur les sites principaux enfants et, enfin, sur les sites secondaires (le cas échéant). Si vous disposez d'un site principal autonome, et non d'un site d'administration centrale, installez et configurez d'abord le point de mise à jour logicielle sur le site principal, puis éventuellement sur des sites secondaires. Certains paramètres sont uniquement disponibles quand vous configurez le point de mise à jour logicielle sur un site de niveau supérieur. Il existe différentes options à prendre en compte en fonction de l'emplacement auquel vous avez installé le point de mise à jour logicielle.  

> [!IMPORTANT]  
>  Vous pouvez installer plusieurs points de mise à jour logicielle sur un site. Le premier point de mise à jour logicielle que vous installez est configuré en tant que source de synchronisation, laquelle synchronise les mises à jour à partir de Microsoft Update ou à partir de la source de synchronisation en amont. Les autres points de mise à jour logicielle sur le site sont configurés en tant que réplicas du premier point de mise à jour logicielle. Par conséquent, certains paramètres ne sont pas disponibles une fois que vous avez installé et configuré le point de mise à jour logicielle initial.  

> [!IMPORTANT]  
>  Vous ne pouvez pas installer le rôle système de site du point de mise à jour logicielle sur un serveur configuré et utilisé comme serveur WSUS autonome ni utiliser un point de mise à jour logicielle pour gérer directement des clients WSUS. Les serveurs WSUS existants sont uniquement pris en charge en tant que sources de synchronisation en amont pour le point de mise à jour logicielle actif. Consultez [Synchroniser à partir d’un emplacement de source de données en amont](#BKMK_wsussync)

 Vous pouvez ajouter le rôle de système de site de point de mise à jour logicielle à un serveur de système de site existant ou en créer un nouveau. Sur la page **Sélection du rôle système** de l’assistant **Création d’un serveur de système de site** ou <strong>Ajout des rôles de système de site</strong>, selon que vous ajoutez le rôle de système de site à un serveur de site nouveau ou existant, sélectionnez **Point de mise à jour logicielle, puis configurez les paramètres du point de mise à jour logicielle dans l’assistant. Les paramètres varient selon la version de Configuration Manager utilisée. Pour plus d’informations sur l’installation de rôles de système de site, consultez [Installer des rôles de système de site](../../core/servers/deploy/configure/install-site-system-roles.md).  

 Utilisez les sections suivantes pour plus d'informations sur les paramètres du point de mise à jour logicielle sur un site.  

## <a name="proxy-server-settings"></a>Paramètres du serveur proxy  
 Vous pouvez configurer les paramètres du serveur proxy dans différentes pages de l’**Assistant Création d’un serveur de système de site** ou de l’**Assistant Ajout des rôles de système de site** selon votre version de Configuration Manager.  

-   Vous devez configurer le serveur proxy, puis spécifier à quel moment utiliser le serveur proxy pour les mises à jour logicielles. Configurez les paramètres suivants :  

    -   Configurez les paramètres du serveur proxy sur la page **Proxy** de l'Assistant ou sous l'onglet **Proxy** dans Propriétés du système de site. Les paramètres du serveur proxy sont propres au système de site, ce qui signifie que tous les rôles de système de site utilisent les paramètres du serveur proxy que vous spécifiez.  

    -   Spécifiez si le serveur proxy doit être utilisé quand Configuration Manager synchronise les mises à jour logicielles et quand il télécharge du contenu à l’aide d’une règle de déploiement automatique. Configurez les paramètres du serveur proxy du point de mise à jour logicielle sur la page **Paramètres de compte et proxy** de l'Assistant ou sur l'onglet **Paramètres de compte et proxy** des propriétés du point de mise à jour logicielle.  

        > [!NOTE]  
        >  Le paramètre **Utiliser un serveur proxy lors du téléchargement du contenu avec des règles de déploiement automatiques** est disponible mais il n'est pas utilisé pour un point de mise à jour logicielle situé sur un site secondaire. Seul le point de mise à jour logicielle situé sur le site d'administration centrale et le site principal télécharge du contenu depuis la page Microsoft Update.  

> [!IMPORTANT]  
>  Par défaut, le compte **Système local** pour le serveur sur lequel une règle de déploiement automatique a été créée est utilisé pour se connecter à Internet et télécharger les mises à jour logicielles lors de l'exécution des règles de déploiement automatique. Lorsque ce compte n'a pas accès à Internet, les mises à jour logicielles ne peuvent pas être téléchargées et l'entrée suivante est consignée dans le fichier ruleengine.log : **Impossible de télécharger la mise à jour à partir d'Internet. Erreur = 12007**. Configurez les informations d'identification nécessaires pour se connecter au serveur proxy lorsque le compte système local n'a pas accès à Internet.  


## <a name="wsus-settings"></a>Paramètres WSUS  
 Vous devez configurer les paramètres WSUS dans différentes pages de l’**Assistant Création d’un serveur de système de site** ou de l’**Assistant Ajout des rôles de système de site**, selon votre version de Configuration Manager et, dans certains cas, uniquement dans les propriétés du point de mise à jour logicielle (aussi appelées propriétés du composant du point de mise à jour logicielle). Utilisez les informations dans les sections suivantes pour configurer les paramètres WSUS.  

### <a name="BKMK_wsusport"></a>Paramètres de port WSUS  
 Vous devez configurer les paramètres du port WSUS sur la page Point de mise à jour logicielle de l'Assistant ou dans les propriétés du point de mise à jour logicielle. Utilisez la procédure suivante pour déterminer les paramètres de port utilisés par WSUS.  

#### <a name="to-determine-the-port-settings-used-in-iis"></a>Pour déterminer les paramètres de port dans IIS  

 1.  Sur le serveur WSUS, ouvrez le Gestionnaire des services Internet (IIS).  

 2.  Développez le nœud **Sites**, cliquez avec le bouton droit sur le site Web du serveur WSUS, puis cliquez sur **Modifier les liaisons**. Dans la boîte de dialogue Liaisons de site, les valeurs de port HTTP et HTTPS sont affichées dans la colonne **Port** .


### <a name="configure-ssl-communications-to-wsus"></a>Configurer les communications SSL vers WSUS  
 Vous pouvez configurer la communication SSL sur la page **Général** de l'Assistant ou sous l'onglet **Général** des propriétés du point de mise à jour logicielle.  

 Pour plus d’informations sur l’utilisation de SSL, consultez [Decide whether to configure WSUS to use SSL](../plan-design/plan-for-software-updates.md#BKMK_WSUSandSSL).  

### <a name="wsus-server-connection-account"></a>Compte de connexion au serveur SMTP  
 Vous pouvez configurer un compte pour qu'il soit utilisé par le serveur de site lorsqu'il se connecte au service WSUS exécuté sur le point de mise à jour logicielle. Si vous ne configurez pas ce compte, Configuration Manager utilise le compte d’ordinateur du serveur de site pour se connecter à WSUS. Configurez le compte de connexion du serveur WSUS dans la page **Paramètres de compte et proxy** de l’Assistant ou sous l’onglet **Paramètres de compte et proxy** dans les propriétés du point de mise à jour logicielle.  Vous pouvez configurer le compte à différentes étapes de l’Assistant selon la version de Configuration Manager que vous utilisez.  

 Pour plus d’informations sur les comptes Configuration Manager, consultez [Comptes utilisés dans System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="synchronization-source"></a>Source de synchronisation  
 Vous pouvez configurer la source de synchronisation en amont pour la synchronisation des mises à jour logicielles dans la page **Source de synchronisation** de l’Assistant ou sous l’onglet **Paramètres de synchronisation** dans les propriétés du composant de point de mise à jour logicielle. Vos options pour la source de synchronisation varient selon le site.  

 Utilisez le tableau suivant pour les options disponibles lorsque vous configurez le point de mise à jour logicielle au niveau d'un site.  

|Site|Options de source de synchronisation disponibles|  
|----------|----------------------------------------------|  
|-   Site d’administration centrale<br />-   Site principal autonome|-   Synchroniser à partir du site web Microsoft Update<br />-   Synchroniser à partir d’un emplacement de source de données en amont<br />-   Ne pas synchroniser à partir de Microsoft Update ou de la source de données en amont|  
|-   Points de mise à jour logicielle supplémentaires sur un site<br />-   Site principal enfant<br />-   Site secondaire|-   Synchroniser à partir d’un emplacement de source de données en amont|  

 La liste suivante fournit plus d'informations sur chaque option que vous pouvez utiliser comme source de synchronisation :  

-   **Synchroniser à partir de Microsoft Update** : Utilisez ce paramètre pour synchroniser les métadonnées des mises à jour logicielles à partir de Microsoft Update. Le site d'administration centrale doit avoir accès à Internet ; sinon, la synchronisation échoue. Ce paramètre est disponible uniquement lorsque vous configurez le point de mise à jour logicielle sur le site de niveau supérieur.  

    > [!NOTE]  
    >  En présence d’un pare-feu entre le point de mise à jour logicielle et Internet, une configuration du pare-feu peut s’avérer nécessaire pour autoriser l’utilisation des ports HTTP et HTTPS pour le site web WSUS. Vous pouvez également choisir de restreindre l'accès sur le pare-feu à des domaines limités. Pour plus d’informations sur la planification d’un pare-feu prenant en charge les mises à jour logicielles, consultez [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

-   **<a name="BKMK_wsussync"></a>Synchroniser à partir d’un emplacement de source de données en amont** : Utilisez ce paramètre pour synchroniser les métadonnées des mises à jour logicielles à partir de la source de synchronisation en amont. Les sites principaux enfants et les sites secondaires sont automatiquement configurés pour utiliser l'URL du site parent pour ce paramètre. Vous pouvez synchroniser les mises à jour logicielles à partir d’un serveur WSUS existant. Spécifiez une URL, comme https://WSUSServer:8531, où 8531 est le port utilisé pour se connecter au serveur WSUS.  

-   **Ne pas synchroniser à partir de Microsoft Update ou de la source de données en amont** : Utilisez ce paramètre pour synchroniser manuellement les mises à jour logicielles lorsque le point de mise à jour logicielle sur le site de niveau supérieur est déconnecté d'Internet. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles à partir d’un point de mise à jour logicielle déconnecté](synchronize-software-updates-disconnected.md).  

> [!NOTE]  
>  En présence d’un pare-feu entre le point de mise à jour logicielle et Internet, une configuration du pare-feu peut s’avérer nécessaire pour autoriser l’utilisation des ports HTTP et HTTPS pour le site web WSUS. Vous pouvez également choisir de restreindre l'accès sur le pare-feu à des domaines limités. Pour plus d’informations sur la planification d’un pare-feu prenant en charge les mises à jour logicielles, consultez [Configure firewalls](../plan-design/plan-for-software-updates.md#BKMK_ConfigureFirewalls).  

 Vous pouvez également configurer la création d’événements de rapport WSUS dans la page **Source de synchronisation** de l’Assistant ou sous l’onglet **Paramètres de synchronisation** dans les propriétés du composant de point de mise à jour logicielle. Configuration Manager n’utilise pas ces événements. Vous devez donc normalement choisir le paramètre par défaut **Ne pas créer les événements de rapports WSUS**.  

## <a name="synchronization-schedule"></a>Calendrier des synchronisations  
 Configurez le calendrier des synchronisations sur la page **Calendrier des synchronisations** de l'Assistant ou dans les propriétés du composant du point de mise à jour logicielle. Ce paramètre est configuré uniquement sur le point de mise à jour logicielle sur le site de niveau supérieur.  

 Si vous activez le calendrier, vous pouvez configurer un calendrier de synchronisation récurrent simple ou personnalisé. Quand vous configurez un calendrier simple, l’heure de début est établie sur la base de l’heure locale de l’ordinateur qui exécute la console Configuration Manager au moment où vous créez le calendrier. Quand vous configurez l’heure de début d’un calendrier personnalisé, elle est basée sur l’heure locale de l’ordinateur qui exécute la console Configuration Manager.  

> [!TIP]  
>  Planifiez la synchronisation des mises à jour logicielles pour qu’elle s’exécute selon une plage de temps adaptée à votre environnement. Un scénario type consiste à définir le calendrier de synchronisation des mises à jour logicielles pour qu'elle soit exécutée peu après la publication d'une mise à jour de sécurité normale de Microsoft le deuxième mardi de chaque mois, généralement appelé Patch Tuesday (Mardi correctif). Un autre scénario type consiste à définir le calendrier de synchronisation des mises à jour logicielles pour qu'elle soit exécutée tous les jours lorsque vous utilisez des mises à jour logicielles afin de fournir les mises à jour du moteur et de définition Endpoint Protection.  

> [!NOTE]  
>  Si vous choisissez de ne pas activer la synchronisation des mises à jour logicielles selon un calendrier, vous pouvez synchroniser manuellement les mises à jour logicielles à partir du nœud **Toutes les mises à jour logicielles** ou **Groupe de mises à jour logicielles** dans l'espace de travail Bibliothèque de logiciels. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles](synchronize-software-updates.md).  

## <a name="supersedence-rules"></a>Règles de remplacement  
 Configurez les paramètres de remplacement sur la page **Règles de remplacement** de l'Assistant ou sous l'onglet **Règles de remplacement** dans les propriétés du composant du point de mise à jour logicielle. Vous pouvez configurer les règles de remplacement uniquement sur le site de niveau supérieur.  

 Sur cette page, vous pouvez spécifier l'expiration immédiate des mises à jour logicielles remplacées, ce qui permet de les exclure des nouveaux déploiements et de marquer les déploiements existants de manière à indiquer que les mises à jour logicielles remplacées contiennent une ou plusieurs mises à jour logicielles qui ont expiré. Ou bien, vous pouvez spécifier une période avant l'expiration des mises à jour logicielles remplacées, ce qui vous permet de continuer à les déployer. Pour plus d'informations, voir [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

> [!NOTE]  
>  La page **Règles de remplacement** de l’Assistant est uniquement disponible quand vous configurez le premier point de mise à jour logicielle sur le site. Cette page ne s'affiche pas lorsque vous installez des points de mise à jour logicielle supplémentaires.  

## <a name="classifications"></a>Classifications  
 Configurez les paramètres des classifications dans la page **Classifications** de l’Assistant ou sous l’onglet **Classifications** dans les propriétés du composant de point de mise à jour logicielle. Pour plus d’informations sur les classifications de mise à jour logicielle, consultez [Update classifications](../plan-design/plan-for-software-updates.md#BKMK_UpdateClassifications).  

> [!NOTE]  
>  La page **Classifications** de l’Assistant est uniquement disponible quand vous configurez le premier point de mise à jour logicielle sur le site. Cette page ne s'affiche pas lorsque vous installez des points de mise à jour logicielle supplémentaires.  

> [!TIP]  
>  Lorsque vous installez pour la première fois le point de mise à jour logicielle sur le site de niveau supérieur, désactivez toutes les classifications des mises à jour logicielles. Après la synchronisation initiale des mises à jour logicielles, configurez les classifications à partir d'une liste actualisée, puis relancez la synchronisation. Ce paramètre est configuré uniquement sur le point de mise à jour logicielle sur le site de niveau supérieur.  

## <a name="products"></a>Produits  
 Configurez les paramètres des produits dans la page **Produits** de l’Assistant ou sous l’onglet **Produits** dans les propriétés du composant de point de mise à jour logicielle.  

> [!NOTE]  
>  La page **Produits** de l’Assistant est uniquement disponible quand vous configurez le premier point de mise à jour logicielle sur le site. Cette page ne s'affiche pas lorsque vous installez des points de mise à jour logicielle supplémentaires.  

> [!TIP]  
>  Lorsque vous installez pour la première fois le point de mise à jour logicielle sur le site de niveau supérieur, désactivez tous les produits. Après la synchronisation initiale des mises à jour logicielles, configurez les produits à partir d'une liste actualisée, puis relancez la synchronisation. Ce paramètre est configuré uniquement sur le point de mise à jour logicielle sur le site de niveau supérieur.  

## <a name="languages"></a>Langues  
 Configurez les paramètres linguistiques dans la page **Langues** de l’Assistant ou sous l’onglet **Langues** dans les propriétés du composant de point de mise à jour logicielle. Spécifiez les langues pour lesquelles vous souhaitez synchroniser les fichiers de mise à jour logicielle et les détails du résumé. Le paramètre **Fichier de mise à jour logicielle** est configuré au niveau de chaque point de mise à jour logicielle dans la hiérarchie Configuration Manager. Les paramètres **Détails du résumé** sont configurés uniquement sur le point de mise à jour logicielle de niveau supérieur. Pour plus d'informations, voir [Languages](../plan-design/plan-for-software-updates.md#BKMK_UpdateLanguages).  

> [!NOTE]  
>  La page **Langues** de l’Assistant est uniquement disponible quand vous installez le point de mise à jour logicielle sur le site d’administration centrale. Vous pouvez configurer les langues du fichier de mise à jour logicielle sur les sites enfants à partir de l'onglet **Langues** dans les propriétés du composant du point de mise à jour logicielle.  

## <a name="third-party-updates"></a>Mises à jour tierces
À compter de la version 1802 de Configuration Manager, vous pouvez activer les mises à jour tierces pour les clients Configuration Manager. Quand vous activez les mises à jour de logiciels tiers dans les propriétés du composant de point de mise à jour logicielle, le point de mise à jour logicielle télécharge le certificat de signature utilisé par WSUS pour les mises à jour tierces. Cette option n’est pas disponible pendant l’installation du point de mise à jour logicielle et doit être configurée après l’installation. Pour activer les paramètres client des mises à jour tierces, consultez l’article [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#Enable-third-party-software-updates).

## <a name="next-steps"></a>Étapes suivantes
Vous avez installé le point de mise à jour logicielle en commençant par le site de premier niveau dans la hiérarchie Configuration Manager. Répétez les procédures décrites dans cet article pour installer le point de mise à jour logicielle sur chaque site enfant.

Une fois que vous avez installé tous les points de mise à jour logicielle, vous pouvez [synchroniser les mises à jour logicielles](synchronize-software-updates.md).
