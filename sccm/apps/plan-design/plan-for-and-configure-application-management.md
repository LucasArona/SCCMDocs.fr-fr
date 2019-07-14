---
title: Planifier la gestion des applications
titleSuffix: Configuration Manager
description: Implémentez et configurez les dépendances nécessaires au déploiement d’applications dans Configuration Manager.
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3ec099d9ffbb5ffaee1c962faf8443a900c1b324
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176863"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Planifier et configurer la gestion des applications dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cet article pour savoir comment implémenter les dépendances nécessaires au déploiement d’applications dans Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  


### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)

IIS est requis sur les serveurs qui exécutent les rôles de système de site suivants :

- Point du site web du catalogue des applications  
- Point de service web du catalogue des applications  
- Point de gestion  
- Point de distribution  

Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificats des applications dont le code est signé pour les appareils mobiles

Quand vous signez le code des applications à déployer sur des appareils mobiles, n’utilisez pas de certificat généré par un modèle Version 3 (**Windows Server 2008, Enterprise Edition**). Ce modèle de certificat crée un certificat qui est incompatible avec les applications Configuration Manager pour appareils mobiles.

Si vous utilisez les services de certificat Active Directory pour signer le code des applications pour les applications d’appareils mobiles, n’utilisez pas de modèle de certificat Version 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Auditer les événements de connexion pour l’affinité entre utilisateur et appareil  

Si vous voulez créer automatiquement des affinités entre les utilisateurs et les appareils, configurez les clients pour qu’ils procèdent à l’audit des événements de connexion.

Le client Configuration Manager lit les événements de connexion de type **Opération réussie** dans le journal des événements de sécurité Windows afin de déterminer les affinités automatiques entre les utilisateurs et les appareils. Activez ces événements avec les deux stratégies d’audit suivantes :

- **Auditer les événements d'ouverture de session de compte**
- **Auditer les événements d'ouverture de session**

Pour créer automatiquement des relations entre utilisateurs et appareils, vérifiez que ces deux paramètres sont activés sur les ordinateurs clients. Vous pouvez utiliser la stratégie de groupe Windows pour configurer ces paramètres.

Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager


### <a name="management-point"></a>Point de gestion

Les clients contactent un point de gestion pour télécharger la stratégie client, localiser du contenu et se connecter au catalogue des applications. Si les clients ne peuvent pas accéder à un point de gestion, ils ne peuvent pas utiliser le catalogue des applications.

> [!Note]  
> À compter de la version 1806, les rôles du catalogue d’applications ne sont plus nécessaires pour afficher les applications accessibles aux utilisateurs dans le Centre logiciel. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).<!--1358309-->  
  

### <a name="distribution-point"></a>Point de distribution

Pour que les applications puissent être déployées sur les clients, la hiérarchie doit contenir au moins un point de distribution. Par défaut, le serveur de site possède un rôle de système de site du point de distribution activé au cours d'une installation standard. Le nombre et l’emplacement des points de distribution dépendent des exigences propres à votre environnement.

Pour plus d’informations sur l’installation de points de distribution et sur la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


### <a name="reporting-services-point"></a>Point de Reporting Services

Pour utiliser les rapports dans Configuration Manager pour la gestion des applications, installez et configurez d’abord un point de Reporting Services.

Pour plus d’informations, consultez [Rapports dans Configuration Manager](/sccm/core/servers/manage/reporting).  


### <a name="client-settings"></a>Paramètres du client

De nombreux paramètres client contrôlent la manière dont le client installe les applications, ainsi que l’expérience utilisateur sur l’appareil. Ces paramètres client incluent les groupes suivants :

- Agent ordinateur  
- Redémarrage de l’ordinateur  
- Centre logiciel  
- Déploiement logiciel  
- Affinité entre utilisateur et appareil  

Pour plus d’informations, consultez les articles suivants :

- [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings)  
- [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings)  


### <a name="security-permissions-for-application-management"></a>Autorisations de sécurité pour la gestion d'applications

- Le rôle de sécurité **Auteur d’application** comprend les autorisations requises pour créer, modifier et retirer des applications.  

- Le rôle de sécurité **Gestionnaire de déploiement d’application** comprend les autorisations requises pour déployer des applications.  

- Le rôle de sécurité **Administrateur d’application** a toutes les autorisations des rôles de sécurité **Auteur d’application** et **Gestionnaire de déploiement d’application**.  

Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>Client App-V 4.6 SP1 ou version supérieure, pour l'exécution des applications virtuelles

Pour créer des applications virtuelles dans Configuration Manager, installez App-V 4.6 SP1 ou ultérieur sur les appareils.

Avant de déployer des applications virtuelles, vous devez également mettre à jour le client App-V avec le correctif décrit dans [l’article 2645225 du Support Microsoft](https://support.microsoft.com/help/2645225).  


### <a name="application-catalog"></a>Catalogue d’applications

> [!Important]  
> Le catalogue des applications est déconseillé. Pour plus d’informations, consultez [Supprimer le catalogue des applications](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Point de service web du catalogue des applications

Le point de service Web du catalogue des applications est un rôle de système de site qui fournit des informations sur les logiciels disponibles à partir de votre bibliothèque de logiciels au site Web du catalogue des applications auquel les utilisateurs accèdent.

Pour plus d’informations sur la configuration de ce rôle de système de site, voir [Installer et configurer le catalogue des applications](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Point du site web du catalogue des applications

Le point du site Web du catalogue des applications est un rôle de système de site fournissant aux utilisateurs une liste des logiciels disponibles.

Pour plus d’informations sur la configuration de ce rôle de système de site, voir [Installer et configurer le catalogue des applications](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Comptes d’utilisateur découverts pour le catalogue d’applications

Configuration Manager doit d’abord détecter les comptes d’utilisateur avant que les utilisateurs puissent afficher et demander des applications du catalogue des applications. Pour plus d’informations, consultez [Exécuter la découverte](/sccm/core/servers/deploy/configure/run-discovery).  



## <a name="bkmk_userex"></a> Configurer le Centre logiciel  

Pour plus d’informations sur la configuration et la personnalisation du Centre logiciel, voir [Planifier le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center).


## <a name="bkmk_remove-appcat"></a> Supprimer le catalogue des applications

<!-- SCCMDocs-pr issue 3051 -->

Le catalogue des applications est déconseillé. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). La liste suivante résume les modifications :

- À compter de la version 1806, **l’expérience utilisateur Silverlight** pour le point du site Web du catalogue des applications n’est plus prise en charge.<!--1358309--> Le rôle de point de service Web du catalogue des applications n’est plus *obligatoire*, mais il reste *pris en charge*.

- Dans la première version Current branch publiée après le 30 juin 2019, les clients mis à jour utiliseront automatiquement le point de gestion pour les déploiements des applications accessibles à l’utilisateur. Vous ne pourrez pas installer de nouveaux rôles de catalogue d’applications.

- Dans la première version Current branch publiée après le 31 octobre 2019, les rôles de catalogue d’applications ne seront plus pris en charge.  

Ces améliorations itératives au Centre logiciel et au point de gestion visent à simplifier votre infrastructure et à supprimer la nécessité des déploiements accessibles à l’utilisateur au niveau du catalogue d’applications. Le Centre logiciel peut offrir tous les déploiements d’applications sans le catalogue d’applications. De même, si vous activez TLS 1.2 et utilisez le protocole HTTP avec le catalogue d’applications, les utilisateurs ne peuvent pas voir les déploiements destinés à l’utilisateur disponibles.

1. Mettez à jour tous les clients avec la version 1806 ou ultérieure.  

1. Personnalisez le Centre logiciel au lieu de définir les propriétés du rôle du site Web du catalogue d’applications. Pour plus d’informations, consultez [Paramètres clients du Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center).  

1. Passez en revue les valeurs par défaut et les paramètres clients personnalisés. Dans le groupe **Agent ordinateur**, vérifiez que le **point de site Web du catalogue d’applications par défaut** est `(none)`.  

    Le client bascule uniquement vers le point de gestion lorsqu’il n’y a aucun rôle de catalogue d’applications dans la hiérarchie. Sinon, il continue d’utiliser une des instances de catalogue d’applications dans la hiérarchie. Ce comportement s’applique à des sites principaux distincts.  

1. Supprimez les rôles système du **site Web de catalogue d’applications** et du **service Web de catalogue d’applications** de tous les sites principaux.

Une fois que vous supprimez les rôles du catalogue d’applications, le Centre logiciel démarre à l’aide du point de gestion pour les déploiements destinés à l’utilisateur disponibles. Ce changement peut prendre jusqu'à 65 minutes. Pour vérifier ce comportement sur un client spécifique, passez en revue la section `SCClient_<username>.log`, puis recherchez une entrée similaire à la ligne suivante :

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="bkmk_appcat"></a> Installer et configurer le catalogue des applications  

> [!Important]  
> Le catalogue des applications est déconseillé. Pour plus d’informations, consultez [Supprimer le catalogue des applications](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Étape 1 : Certificat de serveur web pour le protocole HTTPS

Si vous utilisez des connexions HTTPS, déployez un certificat de serveur Web sur les serveurs de système de site pour le point du site Web du catalogue des applications et le point de service Web du catalogue des applications.

Si vous souhaitez que les clients utilisent le catalogue d’applications à partir d’Internet, déployez un certificat de serveur Web vers au moins un point de gestion. Configurez-le pour les connexions client à partir d’Internet.

Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Étape 2 : Certificat d’authentification client pour le protocole HTTPS

Si vous utilisez un certificat client PKI pour les connexions à des points de gestion, déployez un certificat d’authentification client sur les ordinateurs clients. Même si les clients n’utilisent pas un certificat PKI client pour se connecter au catalogue d’applications, ils doivent se connecter à un point de gestion afin de l’utiliser.

Déployez un certificat d’authentification client sur les ordinateurs clients dans les cas suivants :

- Tous les points de gestion sur l'intranet n'acceptent que les connexions client HTTPS.
- Les clients se connecteront au catalogue des applications depuis Internet.

Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Étape 3 : Installer et configurer les rôles du catalogue d’applications

Installez les rôles du point de service Web du catalogue des applications et du site Web du catalogue des applications sur le même site. Vous n’êtes pas obligé de les installer sur le même serveur ni dans la même forêt Active Directory. Cependant, le point de service Web du catalogue des applications doit se trouver dans la même forêt que la base de données du site.

Pour plus d’informations sur le positionnement des serveurs, consultez [Planifier des serveurs de système de site et des rôles de système de site](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).

> [!NOTE]  
> Installez le catalogue des applications sur un site principal. Vous ne pouvez pas l’installer sur un site secondaire ou sur le site d’administration centrale.  

Installez le catalogue d’applications sur un nouveau serveur de système de site ou un serveur existant dans le site. Pour plus d’informations sur le processus général, consultez [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Dans l’Assistant permettant d’ajouter un rôle de système de site ou de créer un serveur de système de site, sélectionnez les rôles suivants dans la liste :  

- **Point de service Web du catalogue des applications**  
- **Point du site Web du catalogue des applications**  

> [!TIP]  
> Si vous voulez que les ordinateurs clients puissent utiliser le catalogue des applications via Internet, spécifiez le nom de domaine complet Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Vérifier l’installation de ces rôles de système de site  

- Messages d'état : Utiliser les composants **SMS_PORTALWEB_CONTROL_MANAGER** et **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Par exemple, l'ID d'état **1015** pour **SMS_PORTALWEB_CONTROL_MANAGER** confirme que le Gestionnaire de composants de site a correctement installé le point de site Web du catalogue des applications.  

- Fichiers journaux : Rechercher **SMSAWEBSVCSetup.log** et **SMSPORTALWEBSetup.log**.  

    Pour plus d’informations, recherchez les fichiers journaux **awebsvcMSI.log** et **portlwebMSI.log**.  


### <a name="step-4-configure-client-settings"></a>Étape 4 : Configurer les paramètres client

Configurez les paramètres client par défaut si vous souhaitez que tous les utilisateurs aient les mêmes paramètres. Vous pouvez aussi configurer des paramètres client personnalisés pour des regroupements spécifiques.

Pour plus d’informations, consultez les articles suivants :

- [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings)  
    - Agent ordinateur  
    - Redémarrage de l’ordinateur  
    - Centre logiciel  
    - Déploiement logiciel  
    - Affinité entre utilisateur et appareil  
- [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings)  

Le client Configuration Manager configure les appareils avec ces paramètres lorsqu'il téléchargera ensuite la stratégie client. Pour lancer la récupération de stratégie pour un seul client, consultez [Guide pratique pour gérer les clients](/sccm/core/clients/manage/manage-clients).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Étape 5 : Vérifier que le catalogue des applications est opérationnel

Utilisez les procédures suivantes pour vérifier que le catalogue des applications est opérationnel.

> [!NOTE]  
> L’expérience utilisateur du catalogue d’applications nécessite Microsoft Silverlight. Si vous utilisez le catalogue d’applications directement depuis un navigateur, commencez par vérifier que Microsoft Silverlight est installé sur l’ordinateur.  

> [!TIP]  
> L’absence des prérequis fait partie des causes les plus fréquentes des dysfonctionnements du catalogue des applications après l’installation. Vérifiez la configuration requise en matière de rôles pour les rôles de système de site du catalogue d’applications. Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

Dans un navigateur, entrez l’adresse du site Web du catalogue d’applications. Vérifiez que la page web affiche les trois onglets : **catalogue d’applications**, **Mes demandes d’application**et **Mes appareils**.  

Utilisez l’adresse appropriée dans la liste suivante pour le catalogue des applications, où `<server>` est le nom de l’ordinateur, le nom de domaine complet de l’intranet ou le nom de domaine complet Internet :  

- Connexions client HTTPS et paramètres de rôle de système de site par défaut : `https://<server>/CMApplicationCatalog`  

- Connexions client HTTP et paramètres de rôle de système de site par défaut : `http://<server>/CMApplicationCatalog`  

- Connexions client HTTPS et paramètres de rôle de système de site personnalisés : `https://<server>:<port>/<web application name>`  

- Connexions client HTTP et paramètres de rôle de système de site personnalisés : `http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Si vous vous êtes connecté à l’appareil avec un compte d’administrateur de domaine, le client Configuration Manager n’affiche pas les messages de notification. Par exemple, les messages indiquant que de nouveaux logiciels sont disponibles.  
