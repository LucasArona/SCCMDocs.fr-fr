---
title: Gestion des clients basés sur Internet
titleSuffix: Configuration Manager
description: Créez un plan de gestion des clients basés sur Internet dans System Center Configuration Manager.
ms.date: 05/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 83a7c934-3b11-435d-ba22-cbc274951e83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: afcc3c2d70e1f6d94e7239a0be78c00294108c76
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176704"
---
# <a name="plan-for-internet-based-client-management-in-system-center-configuration-manager"></a>Planifier la gestion des clients basée sur Internet dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion des clients basée sur Internet (ou IBCM, Internet-Based Client Management) vous permet de gérer les clients System Center Configuration Manager quand ils ne sont pas connectés à votre réseau d’entreprise, mais qu’ils disposent d’une connexion Internet standard. Cette configuration offre plusieurs avantages, notamment la réduction des coûts, car il n'est plus nécessaire d'utiliser des réseaux privés virtuels (VPN) et la possibilité de déployer les mises à jour logicielles au moment opportun.  

 En raison des exigences de sécurité plus élevées liées à la gestion des ordinateurs clients sur un réseau public, la gestion des clients basée sur Internet nécessite que les clients et les serveurs de système de site auxquels les clients se connectent utilisent des certificats PKI. Cela garantit l'authentification des connexions par une autorité indépendante et le chiffrement des données vers et depuis ces systèmes de site à l'aide du protocole SSL (Secure Sockets Layer).  

 Utilisez les sections suivantes pour vous aider à planifier la gestion des clients basée sur Internet.  

##  <a name="features-that-are-not-supported-on-the-internet"></a>Fonctionnalités non prises en charge sur Internet  
 Toutes les fonctionnalités de gestion des clients ne sont pas conformes à une utilisation sur Internet. Par conséquent, elles ne sont pas prises en charge quand les clients sont gérés sur Internet. Les fonctionnalités qui ne sont pas prises en charge pour la gestion via Internet reposent généralement sur Active Directory Domain Services ou ne conviennent pas à un réseau public, par exemple la découverte du réseau et Wake-on-LAN (WOL).  

 Les fonctions ci-dessous ne sont pas prises en charge quand les clients sont gérés sur Internet :  

- Le déploiement de client sur Internet, comme l’installation push du client et le déploiement du client basé sur une mise à jour logicielle. Utilisez plutôt l'installation manuelle du client.  

- Attribution automatique du site.  

- Wake-on-LAN.  

- Le déploiement de système d'exploitation. Toutefois, vous pouvez déployer des séquences de tâches qui ne déploient pas un système d'exploitation. Par exemple, des séquences de tâches qui exécutent des scripts et des tâches de maintenance sur les clients.  

- Le contrôle à distance.  

- Le déploiement de logiciels sur des utilisateurs, sauf si le point de gestion Internet peut authentifier l’utilisateur dans Active Directory Domain Services à l’aide de l’authentification Windows (Kerberos ou NTLM). Cela est possible quand le point de gestion Internet approuve la forêt dans laquelle réside le compte d’utilisateur.  

  En outre, la gestion des clients basée sur Internet ne prend pas en charge l’itinérance. L'itinérance permet aux clients de toujours trouver les points de distribution les plus proches pour télécharger du contenu. Les clients qui ne sont pas gérés sur Internet communiquent avec des systèmes de site à partir du site qui leur est attribué quand ces systèmes de site sont configurés pour utiliser un nom de domaine complet (FQDN) Internet et les rôles de système de site autorisent les connexions client à partir d’Internet. Les clients sélectionnent de manière non déterministe l’un des systèmes de site basés sur Internet, indépendamment de la bande passante ou de l’emplacement physique.  

  Quand vous disposez d’un point de mise à jour logicielle qui est configuré pour accepter les connexions à partir d’Internet, les clients Configuration Manager basés sur Internet qui se trouvent sur Internet effectuent toujours une analyse par rapport à ce point de mise à jour logicielle afin de déterminer quelles mises à jour logicielles sont nécessaires. Toutefois, quand ces clients se trouvent sur Internet, ils commencent par essayer de télécharger les mises à jour logicielles à partir de Microsoft Update, plutôt qu’à partir d’un point de distribution basé sur Internet. Ce n’est qu’en cas d’échec qu’ils tenteront de télécharger les mises à jour logicielles exigées à partir d’un point de distribution basé sur Internet. Les clients qui ne sont pas configurés pour la gestion des clients basée sur Internet n’essaient jamais de télécharger les mises à jour logicielles à partir de Microsoft Update, mais utilisent toujours des points de distribution Configuration Manager.  
 
> [!Tip]  
> Le client Configuration Manager détermine automatiquement s’il est sur l’intranet ou sur Internet. Si le client peut contacter un contrôleur de domaine ou un point de gestion local, il définit son type de connexion sur Intranet actuellement. Sinon, il bascule vers Internet actuellement et le client utilise les points de gestion, les points de mise à jour logicielle et les points de distribution attribués à son site pour la communication.

##  <a name="considerations-for-client-communications-from-the-internet-or-untrusted-forest"></a>Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée  
 Les rôles de système de site suivants installés sur les sites principaux prennent en charge les connexions à partir de clients qui se trouvent dans des emplacements non approuvés, comme Internet ou une forêt non approuvée (les sites secondaires ne prennent pas en charge les connexions client à partir d’emplacements non approuvés) :  

- Point du site web du catalogue des applications  

- Module de stratégie de Configuration Manager  

- Point de distribution (HTTPS est requis par les points de distribution cloud)  

- Point proxy d'inscription  

- Point d’état de secours  

- Point de gestion  

- Point de mise à jour logicielle  

  **À propos des systèmes de site accessibles sur Internet :**    
  Même s’il n’est pas nécessaire de disposer d’une relation de confiance entre la forêt d’un client et celle d’un serveur de système de site, quand la forêt qui contient un système de site accessible sur Internet approuve la forêt qui contient les comptes d’utilisateur, cette configuration prend en charge les stratégies utilisateur pour les appareils sur Internet quand vous activez le paramètre client **Autoriser les demandes de stratégie utilisateur depuis des clients Internet** de la **Stratégie client**.  

  Par exemple, les configurations suivantes illustrent la prise en charge par la gestion des clients basés sur Internet des stratégies utilisateur pour les appareils sur Internet :  

- Le point de gestion Internet est le réseau de périmètre sur lequel réside un contrôleur de domaine en lecture seule pour authentifier l’utilisateur et un pare-feu qui autorise les paquets Active Directory.  

- Le compte d’utilisateur se trouve dans la forêt A (Intranet) et le point de gestion basé sur Internet dans la forêt B (le réseau de périmètre). La forêt B approuve la forêt A et un pare-feu qui intervient autorise les paquets d'authentification.  

- Le compte d’utilisateur et le point de gestion basé sur Internet sont dans la forêt A (Intranet). Le point de gestion est publié sur Internet par le biais d’un serveur proxy web (comme Forefront Threat Management Gateway).  

> [!NOTE]  
>  Si l'authentification Kerberos échoue, l'authentification NTLM est ensuite automatiquement utilisée.  

 Comme l’indique l’exemple précédent, vous pouvez placer des systèmes de site basés sur Internet dans l’intranet quand ils sont publiés sur Internet à l’aide d’un serveur proxy web, comme ISA Server et Forefront Threat Management Gateway. Ces systèmes de site peuvent être configurés pour la connexion client à partir d’Internet uniquement, ou pour les connexions client à partir d’Internet et de l’intranet. Lorsque vous utilisez un serveur proxy Web, vous pouvez le configurer pour le pontage SSL (Secure Sockets Layer) vers SSL (plus sécurisé) ou le tunnel SSL :  

-   **Pontage SSL vers SSL :**    
    La configuration recommandée quand vous utilisez des serveurs web proxy pour la gestion de clients sur Internet est le pontage SSL vers SSL, qui utilise une terminaison SSL avec authentification. Les ordinateurs clients doivent être authentifiés à l'aide de l'authentification de l'ordinateur et les clients hérités de l'appareil mobile sont authentifiés à l'aide de l'authentification utilisateur. Les appareils mobiles inscrits par Configuration Manager ne prennent pas en charge le pontage SSL.  

     La terminaison SSL au niveau du serveur web proxy présente l’avantage que les paquets provenant d’Internet sont inspectés avant d’être transférés au réseau interne. Le serveur web proxy authentifie la connexion cliente, l’arrête, puis ouvre une nouvelle connexion authentifiée vers les systèmes de site basés sur Internet. Quand les clients Configuration Manager utilisent un serveur web proxy, leur identité (GUID client) est contenue en toute sécurité dans la charge utile du paquet pour éviter que le point de gestion prenne le serveur web proxy pour le client. Le pontage n’est pas pris en charge dans Configuration Manager de HTTP vers HTTPS ou de HTTPS vers HTTP.  
     
    > [!Note]  
    > Configuration Manager ne prend pas en charge la définition de configurations de pontage SSL tierces. Par exemple, Citrix Netscaler ou F5 BIG-IP. Contactez le fournisseur de votre appareil afin de configurer le pontage pour une utilisation avec Configuration Manager.  

-   **Tunneling** :   
    Si votre serveur web proxy ne peut pas prendre en charge la configuration exigée pour le pontage SSL, ou si vous souhaitez configurer la prise en charge Internet pour les appareils mobiles inscrits par Configuration Manager, le tunneling SSL est également pris en charge. Il s’agit d’une option moins sûre car les paquets SSL provenant d’Internet sont transférés aux systèmes de site sans terminaison SSL et ne peuvent donc pas être inspectés à la recherche de contenu malveillant. Lors de l'utilisation du tunnel SSL, aucune configuration n'est requise pour les certificats pour le serveur Web proxy.  

##  <a name="planning-for-internet-based-clients"></a>Planification des clients basés sur Internet  
 Vous devez décider si les ordinateurs clients qui seront gérés sur Internet seront configurés pour la gestion sur l’intranet et sur Internet, ou pour la gestion des clients sur Internet uniquement. Vous pouvez uniquement configurer l'option de gestion du client pendant l'installation d'un ordinateur client. Si vous changez d'avis ultérieurement, vous devez réinstaller le client.  

> [!NOTE]  
>  Si vous configurez un point de gestion compatible Internet, les clients qui s’y connectent deviennent compatibles Internet dès qu’ils actualisent leur liste de points de gestion disponibles.  

> [!TIP]  
>  Vous n’avez pas à limiter la configuration de la gestion des clients sur Internet uniquement à Internet et vous pouvez également l’utiliser sur l’intranet.  

 Les clients qui sont configurés pour la gestion des clients sur Internet uniquement ne communiquent qu’avec les systèmes de site qui sont configurés pour les connexions client à partir d’Internet. Cette configuration serait appropriée pour les ordinateurs qui ne se connectent jamais à l'Intranet de votre société, par exemple, des ordinateurs de point de vente dans des emplacements distants. Elle peut aussi convenir quand vous voulez limiter les communications client au protocole HTTPS uniquement (par exemple, pour prendre en charge un pare-feu et des stratégies de sécurité limitées) et quand vous installez des systèmes de site basés sur Internet dans un réseau de périmètre et que vous voulez gérer ces serveurs à l’aide du client Configuration Manager.  

 Quand vous souhaitez gérer des clients de groupe de travail sur Internet, vous devez les installer en tant qu’Internet uniquement.  

> [!NOTE]  
>  Les clients d’appareil mobile sont automatiquement configurés en tant qu’Internet uniquement quand ils sont configurés pour utiliser un point de gestion basé sur Internet.  

 D’autres ordinateurs clients peuvent être configurés pour une gestion des clients sur Internet et sur l’intranet. Ils peuvent basculer automatiquement entre la gestion des clients basés sur Internet et la gestion des clients intranet quand ils détectent un changement de réseau. Si ces clients peuvent trouver et se connecter à un point de gestion qui est configuré pour les connexions client sur l’intranet, ces clients sont gérés en tant que clients intranet qui possèdent la fonctionnalité de gestion Configuration Manager complète. Si ces clients ne peuvent pas trouver un point de gestion qui est configuré pour les connexions client sur l’intranet ou s’y connecter, ils tentent de se connecter à un point de gestion basé sur Internet, et en cas de succès, ces clients sont ensuite gérés par les systèmes de site basés sur Internet dans le site qui leur est attribué.  

 L’avantage de pouvoir basculer automatiquement entre la gestion des clients basée sur Internet et la gestion des clients intranet est que les ordinateurs clients peuvent utiliser automatiquement toutes les fonctionnalités de Configuration Manager chaque fois qu’ils sont connectés à l’intranet et continuer d’être gérés pour les fonctions de gestion essentielles quand ils sont sur Internet. En outre, un téléchargement commencé sur Internet peut reprendre sans interruption sur le réseau intranet, et inversement.  

##  <a name="prerequisites-for-internet-based-client-management"></a>Prérequis pour la gestion des clients basée sur Internet  
 Dans Configuration, la gestion du client basée sur Internet Manager présente les dépendances externes suivantes :  

- Les clients qui seront gérés sur Internet doivent être dotés d’une connexion Internet.  

   Configuration Manager utilise des connexions existantes du fournisseur de services Internet (ISP), qu’elles soient permanentes ou temporaires. Les appareils mobiles clients doivent disposer d’une connexion directe à Internet, alors que les ordinateurs clients peuvent se connecter à Internet directement ou par le biais d’un serveur web proxy.  

- Les systèmes de site qui prennent en charge la gestion des clients basée sur Internet doivent être connectés à Internet et se trouver dans un domaine Active Directory.  

   Les systèmes de site basés sur Internet n’exigent aucune relation d’approbation avec la forêt Active Directory du serveur de site. Toutefois, quand le point de gestion basé sur Internet peut authentifier l’utilisateur à l’aide de l’authentification Windows, les stratégies utilisateur sont prises en charge. En cas d'échec de l'authentification Windows, seules les stratégies d'ordinateur sont prises en charge.  

  > [!NOTE]
  >  Pour prendre en charge des stratégies utilisateur, vous devez également définir sur **Vrai** les deux paramètres client **Stratégie client** :  
  > 
  > - **Activer l'interrogation de la stratégie utilisateur sur les clients**  
  >   -   **Autoriser les demandes de stratégie utilisateur depuis des clients Internet**  

   Un point de site web du catalogue d’applications basé sur Internet nécessite également l’authentification Windows pour authentifier les utilisateurs quand leur ordinateur est sur Internet. Cette exigence est indépendante des stratégies utilisateur.  

- Vous devez posséder une infrastructure à clé publique (PKI) de prise en charge capable de déployer et de gérer les certificats exigés par les clients et gérés sur Internet et les serveurs de système de site basés sur Internet.  

   Pour plus d’informations sur les certificats PKI, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

- Le nom de domaine complet (FQDN) Internet des systèmes de site prenant en charge la gestion du client basée sur Internet doit être enregistré sous la forme d’entrées hôtes sur les serveurs DNS publics.  

- Les pare-feu ou serveurs proxy qui interviennent doivent autoriser les communications client associées aux systèmes de site basés sur Internet.  

   Configuration requise des communications client :  

  - Prise en charge du protocole HTTP 1.1  

  - Autorisation du type de contenu HTTP de pièces jointes MIME fractionnées (fractionné/mixte et application/flux d'octets)  

  - Autorisation des verbes suivants pour le point de gestion Internet :  

    -   HEAD  

    -   CCM_POST  

    -   BITS_POST  

    -   GET  

    -   PROPFIND  

  - Autorisation des verbes suivants pour le point de distribution Internet :  

    -   HEAD  

    -   GET  

    -   PROPFIND  

  - Autorisation des verbes suivants pour le point d’état de secours Internet :  

    -   POST  

  - Autorisation des verbes suivants pour le point du site web du catalogue d’applications basé sur Internet :  

    -   POST  

    -   GET  

  - Autorisation des en-têtes HTTP suivants pour le point de gestion Internet :  

    -   Range:  

    -   CCMClientID:  

    -   CCMClientIDSignature:  

    -   CCMClientTimestamp:  

    -   CCMClientTimestampsSignature:  

  - Autorisation de l’en-tête HTTP suivant pour le point de distribution Internet :  

    -   Range:  

    Pour obtenir des informations de configuration afin de prendre en charge cette configuration requise, reportez-vous à la documentation de votre serveur proxy ou de votre pare-feu.  

    Pour obtenir des configurations de communication similaires quand vous utilisez le point de mise à jour logicielle pour les connexions client à partir d’Internet, consultez la documentation de Windows Server Update Services (WSUS). Par exemple, pour WSUS sur Windows Server 2003, consultez [Annexe D : Paramètres de sécurité](http://go.microsoft.com/fwlink/p/?LinkId=143368), l’annexe de déploiement pour les paramètres de sécurité.
