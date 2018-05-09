---
title: Préparer le déploiement du logiciel client pour ordinateurs Mac
titleSuffix: Configuration Manager
description: Tâches de configuration avant le déploiement du client Configuration Manager sur des ordinateurs Mac.
ms.date: 11/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 748a56155ca7dbbcf6764c72cf5fdf37d24a277b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Préparer le déploiement du logiciel client pour ordinateurs Mac

*S’applique à : System Center Configuration Manager (Current Branch)*

Procédez comme suit pour vérifier que vous êtes prêt à [déployer le client Configuration Manager sur les ordinateurs Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).

## <a name="mac-prerequisites"></a>Prérequis des ordinateurs Mac

Le package d’installation de client Mac n’est pas fourni avec le support d’installation de Configuration Manager. Téléchargez les **clients pour d’autres systèmes d’exploitation** à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

**Versions prises en charge :**  

-   **Mac OS X 10.6** (Snow Leopard)

-   **Mac OS X 10.7** (Lion)

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

-   **Mac OS X 10.13** (macOS High Sierra)  

## <a name="certificate-requirements"></a>Conditions de certificat
L’installation et la gestion de clients pour les ordinateurs Mac nécessitent des certificats d’infrastructure à clé publique (PKI). Les certificats PKI permettent de sécuriser les communications entre les ordinateurs Mac et le site Configuration Manager grâce à une authentification mutuelle et des transferts de données chiffrés. Configuration Manager peut demander et installer un certificat client utilisateur à l’aide des services de certificat Microsoft avec une autorité de certification d’entreprise (CA) et les rôles de système de site du point d’inscription et du point proxy d’inscription de Configuration Manager. Vous pouvez également demander et installer un certificat d’ordinateur indépendamment de Configuration Manager si le certificat répond aux critères de Configuration Manager.   

Les clients Mac Configuration Manager procèdent toujours à une vérification de la révocation des certificats. Vous ne pouvez pas désactiver cette fonction.  

Si les clients Mac ne peuvent pas vérifier l’état de révocation du certificat d’un serveur du fait de leur incapacité à localiser la liste CRL, ils ne peuvent pas se connecter aux systèmes de site Configuration Manager. Vérifiez la conception de votre liste CRL pour être certain que les clients Mac (plus particulièrement ceux appartenant à une forêt différente de celle de l'autorité de certification émettrice) seront en mesure de localiser et de se connecter à un point de distribution de la liste CRL (CDP) pour la connexion des serveurs de système de site.  

Avant d’installer le client Configuration Manager sur un ordinateur Mac, choisissez le mode d’installation du certificat client :  

-   Utilisez l’inscription Configuration Manager à l’aide de l’[outil CMEnroll](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Le processus d'inscription ne prenant pas en charge le renouvellement automatique de certificats, vous devez réinscrire les ordinateurs Mac avant l'expiration du certificat installé.  

-   [Utilisez une demande de certificat et une méthode d’installation indépendantes de Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager).  

Pour plus d’informations sur le certificat client Mac requis et sur les autres certificats PKI nécessaires à la prise en charge des ordinateurs Mac, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

Les clients Mac sont attribués automatiquement au site Configuration Manager qui les gère. Les clients Mac s'installent en tant que clients Internet uniquement, même si la communication est limitée à l'intranet. Cette configuration de client signifie qu'ils communiquent avec les rôles de système de site (points de gestion et points de distribution) sur le site qui leur est attribué si vous configurez ces rôles pour autoriser les connexions client depuis Internet. Les ordinateurs Mac ne communiquent pas avec les rôles de système de site extérieurs au site qui leur est attribué.  

> [!IMPORTANT]  
>  Vous ne pouvez pas utiliser le client Mac Configuration Manager pour vous connecter à un point de gestion configuré pour utiliser un [réplica de base de données](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Déployer un certificat de serveur web sur des serveurs de système de site  
Si ces systèmes de site n’en ont pas, déployez un certificat de serveur web sur les ordinateurs qui ont ces rôles de système de site :  

-   Point de gestion  

-   Point de distribution  

-   Point d'inscription  

-   Point proxy d'inscription  

Le certificat de serveur Web doit contenir le nom de domaine Internet complet qui est spécifié dans les propriétés de système de site. Le serveur ne doit pas nécessairement être accessible sur Internet pour prendre en charge les ordinateurs Mac. Si vous n'exigez pas de gestion des clients basée sur Internet, vous pouvez spécifier la valeur du nom de domaine complet intranet pour le nom de domaine complet Internet.  

Spécifiez la valeur du nom de domaine complet Internet du système de site dans le certificat de serveur web pour le point de gestion, le point de distribution et le point proxy d’inscription.

Pour voir un exemple de déploiement qui crée et installe ce certificat de serveur web, consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Déployer un certificat d’authentification client sur des serveurs de système de site  
 Si ces systèmes de site n’en ont pas, déployez un certificat d’authentification client sur les ordinateurs qui hébergent les rôles de système de site suivants :  

-   Point de gestion  

-   Point de distribution  

 Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de gestion, consultez [Déploiement du certificat client pour les ordinateurs Windows](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

 Pour obtenir un exemple de déploiement qui crée et installe le certificat client pour les points de distribution, consultez [Déploiement du certificat client pour les points de distribution](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

>[!IMPORTANT]
>  Pour déployer le client sur des appareils macOS Sierra, vous devez configurer correctement le nom du sujet du certificat de point de gestion, par exemple en utilisant le nom de domaine complet du serveur de point de gestion.

## <a name="prepare-the-client-certificate-template-for-macs"></a>Préparer le modèle de certificat client pour les ordinateurs Mac  

 Le modèle de certificat doit disposer d'autorisations de **lecture** et d' **inscription** pour le compte d'utilisateur appelé à inscrire le certificat sur l'ordinateur Mac.  

 Consultez [Déploiement du certificat client pour les ordinateurs Mac](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  

## <a name="configure-the-management-point-and-distribution-point"></a>Configurer le point de gestion et le point de distribution  
 Configurez des points de gestion pour les options suivantes :  

-   HTTPS  

-   Autorisez les connexions client à partir d’Internet. Cette valeur de configuration est nécessaire pour gérer les ordinateurs Mac. Toutefois, cela ne signifie pas que les serveurs de système de site doivent être accessibles sur Internet.  

-   Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion  

 Même si les points de distribution ne sont pas indispensables à l’installation du client, vous devez en configurer pour permettre au client de se connecter à partir d’Internet si vous voulez déployer des logiciels sur ces ordinateurs après avoir installé le client.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Pour configurer les points de gestion et les points de distribution pour prendre en charge les ordinateurs Mac  

Avant d'entamer cette procédure, assurez-vous que le serveur de système de site exécutant le point de gestion et le point de distribution est configuré avec un nom de domaine Internet complet. Si ces serveurs de système de site ne prennent pas en charge la gestion des clients sur Internet, vous pouvez spécifier le nom de domaine complet intranet comme valeur du nom de domaine complet Internet.

Les rôles de système de site doivent se trouver dans un site principal.  


1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**, puis choisissez le serveur disposant des rôles de système de site appropriés.  

3.  Dans le volet des détails, cliquez avec le bouton droit sur **Point de gestion**, choisissez **Propriétés du rôle** et, dans la boîte de dialogue **Propriétés du point de gestion**, configurez les options suivantes:  

    1.  Choisissez **HTTPS**.  

    2.  Choisissez **Autoriser les connexions au client Internet uniquement** ou **Autoriser les connexions au client Internet et intranet**. Ces options nécessitent un nom de domaine complet Internet ou intranet.  

    3.  Choisissez **Autoriser les périphériques mobiles et les ordinateurs Mac à utiliser ce point de gestion**.  

4.  Dans le volet des détails, cliquez avec le bouton droit sur **Point de distribution**, choisissez **Propriétés du rôle**, puis dans la boîte de dialogue **Propriétés du point de distribution**, configurez les options suivantes :  

    -   Choisissez **HTTPS**.  

    -   Choisissez **Autoriser les connexions au client Internet uniquement** ou **Autoriser les connexions au client Internet et intranet**. Ces options nécessitent un nom de domaine complet Internet ou intranet.  

    -   Choisissez **Importer un certificat**, accédez au fichier du certificat de point de distribution client exporté, puis spécifiez le mot de passe.  

5.  Répétez les étapes 2 à 4 pour tous les points de gestion et les points de distribution des sites principaux que vous prévoyez d’utiliser avec des ordinateurs Mac.  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurer le point proxy d’inscription et le point d’inscription  
 Vous devez installer ces deux rôles de système de site sur le même site, mais il n'est pas nécessaire de les installer sur le même serveur de système de site ni sur la même forêt Active Directory.  

 Pour plus d’informations sur la sélection élective des rôles de système de site et sur les éléments à prendre en considération, consultez [Rôles de système de site](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) dans [Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Ces procédures permettent de configurer les rôles de système de site pour prendre en charge les ordinateurs Mac.   

-   [Nouveau serveur de système de site](#new-site-system-server)  

-   [Serveur de système de site existant](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>Nouveau serveur de système de site  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Serveurs et rôles de système de site**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un serveur de système de site**.  

4.  Dans la page **Général**, spécifiez les paramètres généraux du système de site.  Vérifiez que vous spécifiez une valeur pour le nom de domaine complet Internet. Si le serveur n’est pas accessible à partir d’Internet, utilisez le nom de domaine complet intranet.  

5.  Dans la page **Sélection du rôle système**, sélectionnez **Point proxy d’inscription** et **Point d’inscription** dans la liste des rôles disponibles.  

6.  Dans la page **Point proxy d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires.  

7.  Dans la page **Paramètres du point d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires. Ensuite, exécutez l’Assistant.  

### <a name="existing-site-system-server"></a>Serveur de système de site existant  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Serveurs et rôles de système de site**, puis choisissez le serveur à utiliser pour prendre en charge les ordinateurs Mac.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Ajouter des rôles de système de site**.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**. Vérifiez que vous spécifiez une valeur pour le nom de domaine complet Internet. Si le serveur n’est pas accessible à partir d’Internet, utilisez le nom de domaine complet intranet.   

5.  Dans la page **Sélection du rôle système**, choisissez **Point proxy d’inscription** et **Point d’inscription** dans la liste des rôles disponibles.  

6.  Dans la page **Point proxy d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires.  

7.  Dans la page **Paramètres du point d’inscription**, vérifiez les paramètres et apportez les modifications nécessaires. Ensuite, exécutez l’Assistant.  

## <a name="install-the-reporting-services-point"></a>Installez le point de Reporting Services.  
 [Installez le point de Reporting Services](../../../core/servers/manage/configuring-reporting.md) si vous voulez exécuter des rapports pour les ordinateurs Mac.  

### <a name="next-steps"></a>Étapes suivantes

[Déployez le client Configuration Manager sur des ordinateurs Mac](/sccm/core/clients/deploy/deploy-clients-to-macs).  
