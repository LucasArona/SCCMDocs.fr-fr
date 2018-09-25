---
title: Planifier la gestion des applications
titleSuffix: Configuration Manager
description: Implémentez et configurez les dépendances nécessaires au déploiement d’applications dans Configuration Manager.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df936f3ab5567840560497edd60a32f3bbb9c74d
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893599"
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

Pour plus d’informations sur cette spécification, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Certificats des applications dont le code est signé pour les appareils mobiles

Quand vous signez le code des applications à déployer sur des appareils mobiles, n’utilisez pas de certificat généré par un modèle Version 3 (**Windows Server 2008, Enterprise Edition**). Ce modèle de certificat crée un certificat qui est compatible avec les applications Configuration Manager pour appareils mobiles.

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

Les clients contactent un point de gestion pour télécharger la stratégie client, localiser du contenu et se connecter au catalogue des applications. Si les clients ne peuvent pas accéder à un point de gestion, ils ne peuvent pas utiliser le catalogue d'applications.

> [!Note]  
> À compter de la version 1806, les rôles du catalogue d’applications ne sont plus nécessaires pour afficher les applications accessibles aux utilisateurs dans le Centre logiciel. Pour plus d'informations, consultez [Configurer le Centre logiciel](#bkmk_userex).<!--1358309-->  
  

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


### <a name="discovered-user-accounts-for-application-catalog"></a>Comptes d’utilisateur découverts pour le catalogue d’applications

Configuration Manager doit d’abord détecter les comptes d’utilisateur avant que les utilisateurs puissent afficher et demander des applications du catalogue des applications. Pour plus d’informations, consultez [Exécuter la découverte](/sccm/core/servers/deploy/configure/run-discovery).  


### <a name="application-catalog-web-service-point"></a>Point de service web du catalogue des applications

Le point de service Web du catalogue des applications est un rôle de système de site qui fournit des informations sur les logiciels disponibles à partir de votre bibliothèque de logiciels au site web du catalogue des applications auquel les utilisateurs accèdent.

Pour plus d’informations sur la configuration de ce rôle de système de site, consultez [Configurer le Centre logiciel](#bkmk_userex).  

> [!Note]  
> À compter de la version 1806, le rôle de point de service Web du catalogue des applications n’est plus *requis*, mais il est toujours *pris en charge*.<!--1358309-->  
> 
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="application-catalog-website-point"></a>Point du site web du catalogue des applications

Le point du site web du catalogue des applications est un rôle de système de site fournissant aux utilisateurs une liste des logiciels disponibles.
` Pour plus d’informations sur la configuration de ce rôle de système de site, consultez [Configurer le Centre logiciel](#bkmk_userex).

> [!Note]  
> À compter de la version 1806, le rôle de point du site Web du catalogue des applications n’est plus *requis*, mais il est toujours *pris en charge*.<!--1358309-->  
> 
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="bkmk_userex"></a> Configurer le Centre logiciel  

Les utilisateurs modifient les paramètres, recherchent et installent des applications à partir du Centre logiciel. Lorsque vous installez le client Configuration Manager sur un appareil Windows, il installe automatiquement le Centre logiciel également. Le nouveau Centre logiciel a été modernisé. Les applications qui seraient apparues uniquement dans le catalogue des applications dépendant de Silverlight (applications accessibles à l’utilisateur) apparaissent maintenant dans le Centre logiciel sous l’onglet **Applications**. Pour plus d’informations sur les autres fonctionnalités du Centre logiciel, consultez [Guide de l’utilisateur du Centre logiciel](/sccm/core/understand/software-center).  

Passez en revue les améliorations suivantes apportées au Centre logiciel : 

#### <a name="starting-in-version-1802"></a>À compter de la version 1802

- Le paramètre client **Utiliser le nouveau Centre logiciel** dans le groupe **Agent ordinateur** est activé par défaut. L’ancienne version du Centre logiciel n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Les utilisateurs peuvent rechercher et installer les applications disponibles sur les appareils joints à Azure Active Directory (Azure AD). Pour plus d’informations, consultez [Déployer des applications disponibles pour l’utilisateur sur des appareils joints à Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

#### <a name="starting-in-version-1806"></a>À compter de la version 1806

- Indiquez la visibilité du lien du site web du catalogue d’applications dans l’onglet **État de l’installation** du Centre logiciel. Pour plus d’informations, consultez les paramètres clients du [Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center).  

- Les rôles du catalogue d’applications ne sont plus nécessaires pour afficher les applications accessibles aux utilisateurs dans le Centre logiciel. Cette modification permet d’alléger l’infrastructure de serveur nécessaire pour fournir des applications aux utilisateurs. Le Centre logiciel s’appuie désormais sur le point de gestion pour obtenir ces informations, ce qui permet une meilleure mise à l’échelle des grands environnements par l’attribution de [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Si vous utilisez actuellement le catalogue d’applications et mettez à jour vers Configuration Manager version 1806, le catalogue d’applications continue à fonctionner. Les rôles de point du site Web et de point de service Web du catalogue des applications ne sont plus *requis*, mais ils sont toujours *pris en charge*. **L’expérience utilisateur Silverlight** pour le *point du site Web* du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). 
    > 
    > Commencez à planifier la suppression des rôles du catalogue d’applications dans votre infrastructure. Profitez des améliorations apportées au Centre logiciel pour utiliser le point de gestion et simplifier votre environnement Configuration Manager.  

Utilisez le tableau suivant pour comprendre la configuration requise pour le Centre logiciel en fonction de la version spécifique de Configuration Manager :

| Type d'appareil | Version du site | Infrastructure | 
|-----------------|--------------|----------------|
| Appareil joint à Azure AD</br>(ou « joint à un domaine cloud ») | 1802 ou 1806 | Point de gestion pour tous les déploiements d’applications | 
| Appareil [joint à une version hybride d'Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) sur Internet | 1802 ou 1806 | Passerelle de gestion cloud et point de gestion pour tous les déploiements d’applications |
| Appareil joint au domaine Active Directory local | 1802 | Catalogue d’applications requis pour les applications accessibles à l’utilisateur via le Centre logiciel |
| Appareil joint au domaine Active Directory local | 1806 | Point de gestion pour tous les déploiements d’applications |


> [!Important]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités apparaissent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version des clients n’est pas également la plus récente.



## <a name="branding-software-center"></a>Personnalisation du Centre logiciel

Modifiez l’apparence du Centre logiciel pour répondre aux exigences de la marque de votre organisation. Cette configuration permet aux utilisateurs de faire confiance au Centre logiciel. 

Configuration Manager applique la personnalisation au Centre logiciel selon les priorités suivantes :  

- Si vous n’avez pas installé le catalogue d’applications (recommandé) :  

    1. Paramètres client du **Centre logiciel**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Paramètre client **Nom de l’organisation** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Si vous avez installé le catalogue d’applications :  

    1. Paramètres client du **Centre logiciel**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Si vous connectez un abonnement Microsoft Intune à Configuration Manager, le Centre logiciel affiche le *nom d’organisation*, la *couleur* et le *logo de l’entreprise* spécifiés dans les propriétés de l’abonnement Intune. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. Le *nom d’organisation* et la *couleur* que vous spécifiez dans les propriétés du point du site Web du catalogue des applications. Pour plus d’informations, consultez [Options de configuration pour le point du site web du catalogue des applications](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. Paramètre client **Nom de l’organisation** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

#### <a name="configure-software-center-branding"></a>Configurer la personnalisation du Centre logiciel
<!-- 1351224 --> Personnalisez l’apparence du Centre logiciel en ajoutant les éléments de marque de votre entreprise et en spécifiant la visibilité des onglets. 

Pour plus d’informations, consultez les articles suivants :
- Groupe de paramètres client du [Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center)  
- [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings)  



## <a name="bkmk_appcat"></a> Installer et configurer le catalogue d’applications  

> [!Note]  
> À compter de la version 1806, les rôles de point du site Web et de point de service Web du catalogue des applications ne sont plus *requis*, mais ils sont toujours *pris en charge*. Pour plus d’informations, consultez [Configurer le Centre logiciel](#bkmk_userex).  
> 
> **L’expérience utilisateur Silverlight** pour le *point du site Web* du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

> [!IMPORTANT]  
>  Avant de suivre ces étapes, vérifiez que toutes les dépendances sont en place. Pour plus d'informations, consultez les sections suivantes de cet article :
> - [Dépendances externes à Configuration Manager](#dependencies-external-to-configuration-manager)  
> - [Dépendances de Configuration Manager](#configuration-manager-dependencies)


### <a name="step-1-web-server-certificate-for-https"></a>Étape 1 : Certificat de serveur web pour le protocole HTTPS

Si vous utilisez des connexions HTTPS, déployez un certificat de serveur web sur les serveurs de système de site pour le point du site Web du catalogue des applications et le point de service Web du catalogue des applications. 

Si vous souhaitez que les clients utilisent le catalogue d’applications à partir d’Internet, déployez un certificat de serveur web vers au moins un point de gestion. Configurez-le pour les connexions client à partir d’Internet.

Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Étape 2 : Certificat d’authentification client pour le protocole HTTPS

Si vous utilisez un certificat client PKI pour les connexions à des points de gestion, déployez un certificat d’authentification client sur les ordinateurs clients. Même si les clients n’utilisent pas un certificat PKI client pour se connecter au catalogue d’applications, ils doivent se connecter à un point de gestion afin de l’utiliser. 

Déployez un certificat d’authentification client sur les ordinateurs clients dans les cas suivants :
- Tous les points de gestion sur l'intranet n'acceptent que les connexions client HTTPS.
- Les clients se connecteront au catalogue d'applications depuis Internet.

Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Étape 3 : Installer et configurer les rôles du catalogue d’applications

Installez les rôles du point de service Web du catalogue des applications et du site Web du catalogue des applications sur le même site. Vous n’êtes pas obligé de les installer sur le même serveur ni dans la même forêt Active Directory. Cependant, le point de service web du catalogue des applications doit se trouver dans la même forêt que la base de données du site.

Pour plus d’informations sur le positionnement des serveurs, consultez [Planifier des serveurs de système de site et des rôles de système de site](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).

> [!NOTE]  
> Installez le catalogue d’applications sur un site principal. Vous ne pouvez pas l’installer sur un site secondaire ou sur le site d’administration centrale.  

Installez le catalogue d’applications sur un nouveau serveur de système de site ou un serveur existant dans le site. Pour plus d’informations sur le processus général, consultez [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Dans l’Assistant permettant d’ajouter un rôle de système de site ou de créer un serveur de système de site, sélectionnez les rôles suivants dans la liste :  
- **Point de service web du catalogue des applications**  
- **Point du site web du catalogue des applications**  

> [!TIP]  
>  Si vous voulez que les ordinateurs clients puissent utiliser le catalogue des applications via Internet, spécifiez le nom de domaine complet Internet.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Vérifier l’installation de ces rôles de système de site  

- Messages d'état : Utiliser les composants **SMS_PORTALWEB_CONTROL_MANAGER** et **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Par exemple, l'ID d'état **1015** pour **SMS_PORTALWEB_CONTROL_MANAGER** confirme que le Gestionnaire de composants de site a correctement installé le point de site web du catalogue d'applications.  

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


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Étape 5 : vérifier que le catalogue des applications est opérationnel

Utilisez les procédures suivantes pour vérifier que le catalogue d'applications est opérationnel. 

> [!NOTE]  
>  L’expérience utilisateur du catalogue d’applications nécessite Microsoft Silverlight. Si vous utilisez le catalogue d’applications directement depuis un navigateur, commencez par vérifier que Microsoft Silverlight est installé sur l’ordinateur.  

> [!TIP]  
>  L’absence des prérequis fait partie des causes les plus fréquentes des dysfonctionnements du catalogue des applications après l’installation. Vérifiez la configuration requise en matière de rôles pour les rôles de système de site du catalogue d’applications. Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

Dans un navigateur, entrez l’adresse du site web du catalogue d’applications. Vérifiez que la page web affiche les trois onglets : **catalogue d’applications**, **Mes demandes d’application**et **Mes appareils**.  

Utilisez l’adresse appropriée dans la liste suivante pour le catalogue d’applications, où &lt;serveur&gt; est le nom de l’ordinateur, le nom de domaine complet de l’intranet ou le nom de domaine complet Internet :  

- Connexions clientes HTTPS et paramètres de rôle de système de site par défaut : **https://&lt;serveur&gt;/CMApplicationCatalog**  

- Connexions clientes HTTP et paramètres de rôle de système de site par défaut : **http://&lt;serveur&gt;/CMApplicationCatalog**  

- Connexions clientes HTTPS et paramètres de rôle de système de site personnalisés : **https://&lt;serveur&gt;:&lt;port&gt;/&lt;nom_application_web&gt;**  

- Connexions clientes HTTP et paramètres de rôle de système de site personnalisés : **http://&lt;serveur&gt;:&lt;port&gt;/&lt;nom_application_web&gt;**  

> [!NOTE]  
>  Si vous vous êtes connecté à l’appareil avec un compte d’administrateur de domaine, le client Configuration Manager n’affiche pas les messages de notification. Par exemple, les messages indiquant que de nouveaux logiciels sont disponibles.  

