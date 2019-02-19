---
title: Préparer le déploiement du client sur des ordinateurs Mac
titleSuffix: Configuration Manager
description: Tâches de configuration avant le déploiement du client Configuration Manager sur des ordinateurs Mac.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49edf86f855c934d29ae0ed1101bb319278ccc7c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141049"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Préparer le déploiement du logiciel client pour ordinateurs Mac

*S’applique à : System Center Configuration Manager (Current Branch)*

Effectuez ces étapes pour vous préparer à [déployer le client Configuration Manager sur les ordinateurs Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).



## <a name="mac-prerequisites"></a>Prérequis des ordinateurs Mac

Le package d’installation de client Mac n’est pas fourni avec le support d’installation de Configuration Manager. Téléchargez les **Clients pour systèmes d’exploitation supplémentaires** à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

Pour obtenir la liste des versions prises en charge, consultez [Systèmes d’exploitation pris en charge pour les clients et les appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#mac-computers).



## <a name="certificate-requirements"></a>Conditions de certificat

L’installation et la gestion de clients pour les ordinateurs Mac nécessitent des certificats d’infrastructure à clé publique (PKI). Les certificats PKI permettent de sécuriser les communications entre les ordinateurs Mac et le site Configuration Manager grâce à une authentification mutuelle et des transferts de données chiffrés. Configuration Manager peut demander et installer un certificat client utilisateur. Il utilise les services de certificats avec une autorité de certification d’entreprise ainsi que le point d’inscription et le point proxy d’inscription Configuration Manager. Vous pouvez aussi demander un certificat d’ordinateur et l’installer indépendamment de Configuration Manager. Ce certificat doit respecter les exigences de Configuration Manager en matière de certificats.  

Les clients Mac Configuration Manager vérifient toujours la révocation des certificats. Vous ne pouvez pas désactiver cette fonction.  

Si les clients Mac ne parviennent pas à localiser la liste de révocation de certificats, ils ne peuvent pas se connecter aux systèmes de site Configuration Manager. Vérifiez la conception de votre liste de révocation de certificats, en particulier pour les clients Mac situés dans une forêt différente de celle de l’autorité de certification émettrice. Vérifiez que les clients Mac peuvent localiser et télécharger une liste de révocation de certificats.  

Avant d’installer le client Configuration Manager sur un ordinateur Mac, choisissez le mode d’installation du certificat client :  

-   Utilisez l’inscription Configuration Manager à l’aide de l’[outil CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Le processus d’inscription ne prend pas en charge le renouvellement automatique des certificats. Réinscrivez les ordinateurs Mac avant que le certificat arrive à expiration.  

-   [Utilisez une demande de certificat et une méthode d’installation indépendantes de Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Pour plus d’informations sur la configuration requise des certificats clients Mac, consultez [Configuration requise des certificats PKI pour Configuration Manager](/sccm/core/plan-design/network/pki-certificate-requirements).  

Les clients Mac sont attribués automatiquement au site Configuration Manager qui les gère. Les clients Mac s’installent en tant que clients Internet uniquement, même si la communication est limitée à l’intranet. Cette configuration signifie qu’ils communiquent avec des points de gestion et des points de distribution compatibles Internet du site auquel ils sont affectés. Les ordinateurs Mac ne communiquent pas avec les systèmes de site extérieurs au site auquel ils sont affectés.  

> [!IMPORTANT]  
>  Vous ne pouvez pas utiliser le client Configuration Manager pour macOS pour vous connecter à un point de gestion configuré pour utiliser un [réplica de base de données](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Déployer un certificat de serveur web sur des serveurs de système de site  

Si ces systèmes de site n’en ont pas, déployez un certificat de serveur web sur les ordinateurs qui ont ces rôles de système de site :  

-   Point de gestion  

-   Point de distribution  

-   Point d'inscription  

-   Point proxy d'inscription  

Le certificat de serveur web doit inclure le nom de domaine complet Internet qui est spécifié dans les propriétés de système de site. Le serveur n’a pas besoin d’être accessible depuis Internet pour prendre en charge les ordinateurs Mac. Si vous n’avez pas besoin de la gestion des clients basée sur Internet, vous pouvez spécifier la valeur du nom de domaine complet intranet pour le nom de domaine complet Internet.  

Spécifiez la valeur du nom de domaine complet Internet du système de site dans le certificat de serveur web pour le point de gestion, le point de distribution et le point proxy d’inscription.

Pour obtenir un exemple de déploiement, consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Déployer un certificat d’authentification client sur des serveurs de système de site  

Si ces systèmes de site n’en ont pas, déployez un certificat d’authentification client sur les ordinateurs qui hébergent les rôles de système de site suivants :  

-   Point de gestion  

-   Point de distribution  

Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de gestion, consultez [Déploiement du certificat client pour les ordinateurs Windows](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de distribution, consultez [Déploiement du certificat client pour les points de distribution](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Pour déployer le client sur des appareils exécutant macOS Sierra, vous devez configurer correctement le nom du sujet du certificat de point de gestion. Par exemple utilisez le nom de domaine complet du serveur de point de gestion.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Préparer le modèle de certificat client pour les ordinateurs Mac  

Le modèle de certificat doit disposer d’autorisations **Lecture** et **Inscription** pour le compte d’utilisateur qui inscrit le certificat sur l’ordinateur Mac.  

Pour plus d’informations, consultez [Déploiement du certificat client pour les ordinateurs Mac](/sccm/plan-design/network/example-deployment-of-pki-certificates#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Configurer le point de gestion et le point de distribution  

Configurez des points de gestion pour les options suivantes :  

-   HTTPS  

-   Autorisez les connexions clientes à partir d’Internet. Cette valeur de configuration est nécessaire pour gérer les ordinateurs Mac. Cependant, cela ne signifie pas que les serveurs de système de site doivent être accessibles depuis Internet.  

-   Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion  

Il n’est pas nécessaire de disposer de points de distribution pour installer le client pour Mac. Si vous voulez déployer des logiciels sur ces ordinateurs après avoir installé le client, configurez les points de distribution pour autoriser les connexions clientes depuis Internet.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Pour configurer les points de gestion et les points de distribution pour prendre en charge les ordinateurs Mac  

Avant de démarrer cette procédure, veillez à configurer le point de gestion et le point de distribution avec un nom de domaine complet Internet. Si ces serveurs ne prennent pas en charge la gestion des clients basée sur Internet, spécifiez le nom de domaine complet intranet comme valeur du nom de domaine complet Internet.

Les rôles de système de site doivent se trouver dans un site principal.  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Serveurs et rôles de système de site**. Sélectionnez ensuite le serveur associé aux rôles de système de site appropriés.  

2.  Dans le volet d’informations, sélectionnez le rôle **Point de gestion** et **Propriétés** dans le ruban. Dans la fenêtre **Propriétés de Point de gestion**, configurez ces options :  

    1.  Choisissez **HTTPS**.  

    2.  Choisissez **Autoriser les connexions au client Internet uniquement** ou **Autoriser les connexions au client Internet et intranet**. Ces options nécessitent un nom de domaine complet Internet ou intranet.  

    3.  Choisissez **Autoriser les périphériques mobiles et les ordinateurs Mac à utiliser ce point de gestion**.  

    4. Sélectionnez **OK** pour enregistrer cette configuration.  

3.  Dans le volet d’informations du nœud Serveurs et rôles de système de site, sélectionnez le rôle **Point de distribution**, puis **Propriétés** dans le ruban. Dans la fenêtre **Propriétés de Point de distribution**, configurez ces options :  

    -   Choisissez **HTTPS**.  

    -   Choisissez **Autoriser les connexions au client Internet uniquement** ou **Autoriser les connexions au client Internet et intranet**. Ces options nécessitent un nom de domaine complet Internet ou intranet.  

    -   Choisissez **Importer un certificat**, accédez au fichier du certificat de point de distribution client exporté, puis spécifiez le mot de passe.  

4.  Répétez cette procédure pour tous les points de gestion et les points de distribution des sites principaux qui gèrent des ordinateurs Mac.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurer le point proxy d’inscription et le point d’inscription  

Installez les deux rôles dans le même site. Vous n’êtes pas obligé de les installer sur le même serveur de système de site ni dans la même forêt Active Directory.  

Pour plus d'informations sur la sélection élective des rôles de système de site et sur les éléments à prendre en considération, consultez [Rôle de système de site](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles#bkmk_planroles).  

Ces procédures permettent de configurer les rôles de système de site pour prendre en charge les ordinateurs Mac :   

-   [Nouveau serveur de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles#to-install-site-system-roles-on-a-new-site-system-server)  

-   [Serveur de système de site existant](/sccm/core/servers/deploy/configure/install-site-system-roles#bkmk_Install)    

Dans chaque cas, dans la page **Sélection du rôle système**, sélectionnez **Point proxy d’inscription** et **Point d’inscription** dans la liste des rôles disponibles.  



## <a name="install-the-reporting-services-point"></a>Installez le point de Reporting Services.  

Pour plus d'informations, consultez [Installer le point de Reporting Services](/sccm/core/servers/manage/configuring-reporting).  



## <a name="next-steps"></a>Étapes suivantes

[Déployer le client Configuration Manager sur des ordinateurs Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  
