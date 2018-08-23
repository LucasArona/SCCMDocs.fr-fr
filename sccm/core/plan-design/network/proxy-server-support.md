---
title: Prise en charge du serveur proxy
titleSuffix: Configuration Manager
description: Découvrez comment les serveurs de système de site Configuration Manager utilisent les serveurs proxy.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78694282dae7408e1f9e01fd75585f87aef41da7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383549"
---
# <a name="proxy-server-support-in-configuration-manager"></a>Prise en charge de serveur proxy dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Certains serveurs de système de site Configuration Manager nécessitent des connexions à Internet. Si votre environnement nécessite l’utilisation d’un serveur proxy pour communiquer avec Internet, configurez ces rôles de système de site pour qu’ils utilisent le proxy.  

-   Un ordinateur qui héberge un serveur de système de site prend en charge une seule configuration de serveur proxy. Tous les rôles de système de site sur cet ordinateur partagent la même configuration de proxy. Si vous devez séparer les serveurs proxy pour différents rôles ou différentes instances d’un rôle, placez ces rôles sur des serveurs de système de site distincts.  

-   Quand vous configurez de nouveaux paramètres de serveur proxy pour un serveur de système de site qui possède déjà une configuration de serveur proxy, la configuration d’origine est remplacée.  

-   Par défaut, les connexions au proxy utilisent le compte **Système** de l’ordinateur qui héberge le rôle de système de site.  

-   Si le compte d’ordinateur ne peut pas s’authentifier, le serveur de système de site peut stocker les informations d’identification de l’utilisateur pour se connecter au serveur proxy. Ces informations d’identification sont celles du **compte de serveur proxy du système de site**.  



## <a name="site-system-roles-that-use-a-proxy"></a>Rôles de système de site qui utilisent un proxy

Les rôles de système de site suivants se connectent à Internet et, si nécessaire, peuvent utiliser un serveur proxy :  


#### <a name="asset-intelligence-synchronization-point"></a>Point de synchronisation Asset Intelligence
Ce rôle de système de site se connecte à Microsoft et utilise une configuration de serveur proxy sur l’ordinateur qui héberge le point de synchronisation Asset Intelligence.  


#### <a name="cloud-distribution-point"></a>Point de distribution cloud
Le rôle de point de distribution cloud s’exécute dans Microsoft Azure. Vous ne configurez pas ce rôle de système de site pour utiliser un proxy. Définissez la configuration du proxy sur le serveur de site principal qui gère le point de distribution cloud.  

Pour cette configuration, le serveur de site principal :  

-   Doit pouvoir se connecter à Microsoft Azure pour configurer, analyser et distribuer du contenu au point de distribution cloud  

-   Utilise par défaut le compte **Système** de l’ordinateur pour établir la connexion. Il peut également utiliser le compte du serveur proxy du système de site, si nécessaire  

-   Utilise les API de navigateur web Windows  


#### <a name="exchange-server-connector"></a>Connecteur Exchange Server
Ce rôle de système de site se connecte à un serveur Exchange. Il utilise une configuration de serveur proxy sur l’ordinateur qui héberge le connecteur du serveur Exchange Server.  


#### <a name="service-connection-point"></a>point de connexion de service
Ce rôle de système de site se connecte au service cloud Configuration Manager afin de télécharger les mises à jour de version pour Configuration Manager, et se connecte à Microsoft Intune dans une configuration hybride. Il utilise un serveur proxy configuré sur l’ordinateur qui héberge le point de connexion de service.  


#### <a name="software-update-point"></a>Point de mise à jour logicielle
Ce rôle de système de site utilise le proxy quand il se connecte à Microsoft Update pour télécharger les correctifs et synchroniser les informations sur les mises à jour. Comme pour tout autre rôle de système de site, configurez d’abord les paramètres de proxy du système de site. Configurez ensuite les options suivantes spécifiques au point de mise à jour logicielle :  

-   **Utiliser un serveur proxy lors de la synchronisation des mises à jour logicielles**  

-   **Utiliser un serveur proxy lors du téléchargement du contenu avec des règles de déploiement automatiques**  

    > [!Note]  
    > Bien que disponible, ce paramètre n’est pas utilisé par les points de mise à jour logicielle sur les sites secondaires.  

Ces paramètres se trouvent sous l’onglet **Paramètres de compte et proxy** des propriétés du point de mise à jour logicielle.  

> [!NOTE]  
>  Par défaut, le compte **Système** du serveur sur lequel une règle de déploiement automatique a été créée est utilisé pour se connecter à Internet et télécharger les mises à jour logicielles durant l’exécution des règles de déploiement automatique. Vous pouvez également configurer et utiliser le compte de serveur proxy du système de site. 
>   
>  Quand ce compte ne peut pas accéder à Internet, les mises à jour logicielles ne peuvent pas être téléchargées. L’entrée suivante est journalisée dans **ruleengine.log** :  
> `Failed to download the update from internet. Error = 12007.`  



## <a name="configure-the-proxy-for-a-site-system-server"></a>Configurer le proxy pour un serveur de système de site  

1.  Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site**, puis sélectionnez le nœud **Serveurs et rôles de système de site**.  

2.  Sélectionnez le serveur de système de site à modifier. Dans le volet d’informations, cliquez avec le bouton droit sur le rôle **Système de site**, puis sélectionnez **Propriétés**.  

3.  Dans Propriétés du système de site, accédez à l’onglet **Proxy**. Configurez les paramètres de proxy suivants :  

    - **Utiliser un serveur proxy lors de la synchronisation d’informations provenant d’Internet** : sélectionnez cette option pour permettre au serveur de système de site d’utiliser un serveur proxy.  

    - **Nom du serveur proxy** : spécifiez le nom d’hôte ou le FQDN (nom de domaine complet) du serveur proxy de votre environnement.  

    - **Port** : spécifiez le port réseau sur lequel communiquer avec le serveur proxy. Par défaut, il utilise le port **80**.  

    - **Utiliser les informations d’identification pour la connexion au serveur proxy** : de nombreux serveurs proxy imposent à l’utilisateur de s’authentifier. Par défaut, le serveur de système de site utilise son compte d’ordinateur pour se connecter au serveur proxy. Si nécessaire, activez cette option, cliquez sur **Définir**, puis choisissez un **Compte existant** ou spécifiez un **Nouveau compte**. Ces informations d’identification sont celles du **compte de serveur proxy du système de site**.  Pour plus d’informations, consultez [Comptes utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  

4.  Cliquez sur **OK** pour enregistrer la nouvelle configuration de serveur proxy.  
