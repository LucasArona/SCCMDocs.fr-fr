---
title: Prérequis pour le déploiement de clients Windows
titleSuffix: Configuration Manager
description: Découvrez les prérequis pour le déploiement du client Configuration Manager sur des ordinateurs Windows.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 025edee312e1c67eba9f9e4f812b03806f51dbbb
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384312"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>Prérequis pour le déploiement de clients sur des ordinateurs Windows dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le déploiement de clients Configuration Manager dans votre environnement présente des dépendances externes et internes au produit, comme décrit ci-dessous. En outre, chaque méthode de déploiement client possède ses propres dépendances qui doivent être respectées pour le bon déroulement des installations clients.  

Pour plus d’informations sur la configuration système et matériel minimale requise pour le client Configuration Manager, consultez [Configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations).  

> [!NOTE]  
>  Les numéros de version de logiciel mentionnés dans cet article indiquent uniquement les numéros de version minimale requise.  



##  <a name="BKMK_prereqs_computers"></a> Prérequis pour les clients Windows  

Utilisez les informations suivantes pour déterminer les prérequis pour installer le client Configuration Manager sur des appareils Windows.  

### <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

|Composant|Description|  
|---|---|  
|Windows Installer version 3.1.4000.2435|Obligatoire pour prendre en charge l'utilisation des fichiers de mise à jour (.msp) Windows Installer pour les packages et les mises à jour logicielles.|  
|Service Microsoft BITS (Background Intelligent Transfer Service) version 2.5|Requis pour autoriser le transfert contrôlé des données entre l’ordinateur client et les systèmes de site Configuration Manager. Le service BITS n’est pas automatiquement téléchargé lors de l’installation du client. Quand BITS est installé sur des ordinateurs, un redémarrage est généralement nécessaire pour terminer l’installation.<br /><br /> La plupart des systèmes d’exploitation incluent le service BITS. Si ce n’est pas le cas, installez BITS avant d’installer le client Configuration Manager.|  
|Planificateur de tâches Microsoft|Activez ce service sur le client pour effectuer l’installation du client.|  


### <a name="bkmk_ExternalDependencies"></a> Dépendances extérieures à Configuration Manager et téléchargées automatiquement pendant l’installation  

Le client Configuration Manager présente des dépendances externes. Ces dépendances dépendent de la version du système d’exploitation et des logiciel installés sur l’ordinateur client.  

Si le client nécessite ces dépendances pour terminer l’installation, il les installe automatiquement.  

|Composant|Description|  
|---|---|  
|Agent Windows Update version 7.0.6000.363|Requis par Windows pour prendre en charge la détection et le déploiement des mises à jour.|  
|Microsoft Core XML Services (MSXML) version 6.20.5002 ou supérieure|Obligatoire pour prendre en charge le traitement des documents XML dans Windows.|  
|Microsoft Remote Differential Compression (RDC)|Requis pour optimiser la transmission de données sur le réseau.|  
|Microsoft Visual C++ 2013 Redistributable version 12.0.21005.1|Requis pour prendre en charge les opérations de clients. Quand vous installez cette mise à jour sur des ordinateurs clients, il peut être nécessaire d’effectuer un redémarrage pour terminer l’installation.|  
|Microsoft Visual C++ 2005 Redistributable version 8.0.50727.42|Pour la version 1606 et les versions antérieures, exigé pour prendre en charge les opérations de Microsoft SQL Server Compact.|  
|API d'image Windows 6.0.6001.18000|Requis pour permettre à Configuration Manager de gérer les fichiers image Windows (.wim).|  
|Microsoft Policy Platform 1.2.3514.0|Requis pour autoriser les clients à évaluer les paramètres de conformité.|  
|Microsoft Silverlight 5.1.41212.0|Requis pour prendre en charge l'expérience utilisateur du site Web du catalogue d'applications. À compter de Configuration Manager 1802, le client n’installe pas automatiquement Silverlight. La fonctionnalité principale du catalogue des applications est désormais incluse dans le Centre logiciel. Le support du site web du catalogue d’applications se termine avec la version 1806.<!--1356195-->|  
|Microsoft .NET Framework version 4.5.2.|Requis pour prendre en charge les opérations de clients. Installé automatiquement sur l’ordinateur client si Microsoft .NET Framework 4.5 ou une version ultérieure n’est pas installé. Pour plus d’informations, consultez [Détails supplémentaires sur Microsoft .NET Framework version 4.5.2](#dotNet).|  
|Composants Microsoft SQL Server Compact 3.5 SP2|Requis pour conserver les informations liées aux opérations du client.|  


####  <a name="dotNet"></a> Informations supplémentaires sur Microsoft .NET Framework version 4.5.2  

> [!NOTE]  
>  .NET 4.0, 4.5 et 4.5.1 ne sont plus prise en charge. Pour plus d’informations, consultez [Questions fréquentes (FAQ) sur la politique de support - Microsoft .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework).  

Microsoft .NET Framework version 4.5.2 peut nécessiter un redémarrage pour achever l’installation. Une notification **Redémarrage requis** s’affiche dans la barre d’état système. Les scénarios courants suivants nécessitent un redémarrage des ordinateurs clients :  

-   Des services ou des applications .NET sont en cours d’exécution sur l’ordinateur.  

-   Il manque une ou plusieurs mises à jour logicielles nécessaires pour l’installation de .NET.  

-   L’ordinateur doit être redémarré suite à une précédente installation de mises à jour logicielles du .NET Framework.  


Une fois .NET Framework 4.5.2 installé, il peut nécessiter des mises à jour supplémentaires. Ces mises à jour ultérieures peuvent nécessiter des redémarrages supplémentaires de l’ordinateur.  


### <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

Pour plus d’informations, consultez [Déterminer les rôles système de site pour les clients](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

|Composant|Description|  
|---|---|  
|Point de gestion|Pour déployer le client Configuration Manager, vous n’avez pas besoin d’un point de gestion. Les clients nécessitent un point de gestion pour transférer des informations avec le site. Sans point de gestion, vous ne pouvez pas gérer les ordinateurs clients.|  
|Point de distribution|Le point de distribution est un rôle de système de site facultatif, mais recommandé dans le cadre du déploiement et de la gestion de clients. Tous les points de distribution hébergent les fichiers sources des clients. Les clients trouvent le point de distribution le plus proche à partir duquel télécharger les fichiers sources lors de leur déploiement ou de leur mise à jour. Si le site ne possède pas de point de distribution, les ordinateurs téléchargent les fichiers sources des clients à partir de leur point de gestion.|  
|Point d’état de secours|Le point d'état de secours est un rôle de système de site facultatif, mais recommandé dans le cadre du déploiement de clients. Le point d’état de secours effectue le suivi du déploiement des clients et permet aux ordinateurs du site Configuration Manager d’envoyer des messages d’état quand ils ne peuvent pas communiquer avec un point de gestion.|  
|Point de Reporting Services|Le point de Reporting Services est un rôle de système de site facultatif, mais recommandé. Il affiche les rapports liés à la gestion et au déploiement des clients. Pour plus d’informations, consultez [Rapports dans Configuration Manager](/sccm/core/servers/manage/reporting).|  


### <a name="installation-method-dependencies"></a>Dépendances liées aux méthodes d’installation  

Les conditions requises suivantes sont spécifiques aux différentes méthodes d'installation du client.  

#### <a name="client-push-installation"></a>Installation poussée du client  

   -   Le site utilise des comptes d’installation Push du client pour se connecter aux ordinateurs en vue d’installer le client. Spécifiez ces comptes sous l’onglet **Comptes** des Propriétés de l’installation Push du client. Le compte doit être membre du groupe d'administrateurs local sur l'ordinateur de destination.  

         Si vous ne spécifiez pas de compte d’installation Push du client, le serveur de site utilise son compte d’ordinateur.  

   -   Le site doit trouver l’ordinateur sur lequel vous installez le client. Au moins une méthode de découverte de Configuration Manager est nécessaire.  

   -   L'ordinateur dispose d'un partage ADMIN$.  

   -   Pour envoyer (push) automatiquement le client Configuration Manager vers les ressources découvertes, sélectionnez l’option **Activer l’installation Push du client aux ressources attribuées** dans les Propriétés de l’installation Push du client.  

   -   L’ordinateur client doit communiquer avec un point de distribution ou un point de gestion pour télécharger les fichiers sources.  

   -   À compter de la version 1806, quand vous avez besoin de l’authentification mutuelle Kerberos, les clients doivent se trouver dans une forêt Active Directory approuvée. Dans Windows, Kerberos s’appuie sur Active Directory pour l’authentification mutuelle.<!--1358204-->  


Pour utiliser l’installation Push du client, vous devez disposer des autorisations de sécurité suivantes :  

   -   Pour configurer le compte d’installation Push du client : autorisation **Modifier** et **Lire** pour l’objet **Site**.  

   -   Pour utiliser l’installation Push du client pour installer le client dans des regroupements, des appareils et des requêtes : autorisation **Modifier la ressource** et **Lire** pour l’objet **Regroupement**.  


Le rôle de sécurité par défaut **Administrateur d’infrastructure** comprend les autorisations nécessaires pour gérer les installations Push des clients.  


#### <a name="software-update-point-based-installation"></a>Installation basée sur un point de mise à jour logicielle  

   -   Si vous n’avez pas étendu le schéma Active Directory, ou si vous installez des clients à partir d’une autre forêt, utilisez la stratégie de groupe pour provisionner les paramètres d’installation pour CCMSetup.exe. Pour plus d’informations, consultez [Guide pratique pour provisionner les propriétés d’installation du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Publiez le client Configuration Manager sur le point de mise à jour logicielle.  

   -   Pour télécharger les fichiers sources, l’ordinateur client doit communiquer avec un point de distribution ou un point de gestion.  


Pour en savoir plus sur les autorisations de sécurité nécessaires à la gestion des mises à jour logicielles Configuration Manager, consultez [Prérequis pour les mises à jour logicielles](/sccm/sum/plan-design/prerequisites-for-software-updates).  


#### <a name="group-policy-based-installation"></a>Installation basée sur une stratégie de groupe  

   -   Si vous n’avez pas étendu le schéma Active Directory, ou si vous installez des clients à partir d’une autre forêt, utilisez la stratégie de groupe pour provisionner les paramètres d’installation pour CCMSetup.exe. Pour plus d’informations, consultez [Guide pratique pour provisionner les propriétés d’installation du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

   -   Pour télécharger les fichiers sources, l’ordinateur client doit communiquer avec un point de distribution ou un point de gestion.  


#### <a name="logon-script-based-installation"></a>Installation basée sur un script d'ouverture de session  

Pour télécharger les fichiers sources, l’ordinateur client doit communiquer avec un point de distribution ou un point de gestion. Sauf si vous avez spécifié CCMSetup.exe avec le paramètre de ligne de commande suivant : `ccmsetup /source`  


#### <a name="manual-installation"></a>Installation manuelle  

Pour télécharger les fichiers sources, l’ordinateur client doit communiquer avec un point de distribution ou un point de gestion. Sauf si vous avez spécifié CCMSetup.exe avec le paramètre de ligne de commande suivant : `ccmsetup /source`  


#### <a name="microsoft-intune-mdm-installation"></a>Installation de Microsoft Intune MDM

 - Nécessite un abonnement Microsoft Intune et les licences appropriées.  

 - Nécessite que l’appareil dispose d’un accès à Internet, même s’il n’est pas basé sur Internet.  

 - En fonction du cas d’utilisation, vous pouvez aussi avoir besoin de l’une des deux technologies suivantes (ou des deux à la fois) :  

     - Azure Active Directory  

     - Passerelle de gestion cloud  


#### <a name="workgroup-computer-installation"></a>Installation d'ordinateurs d'un groupe de travail  

Pour accéder aux ressources du domaine du serveur de site Configuration Manager, configurez un compte d’accès réseau pour le site.  

Pour plus d’informations sur la configuration du compte d’accès réseau, consultez [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  


#### <a name="software-distribution-based-installation-for-upgrades-only"></a>Installation basée sur la distribution de logiciels (pour les mises à niveau uniquement)  

   -   Si vous n’avez pas étendu le schéma Active Directory, ou si vous installez des clients à partir d’une autre forêt, utilisez la stratégie de groupe pour provisionner les paramètres d’installation pour CCMSetup.exe. Pour plus d’informations, consultez [Guide pratique pour provisionner les propriétés d’installation du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).   

   -   Pour télécharger les fichiers sources, l’ordinateur client doit communiquer avec un point de distribution ou un point de gestion.  


Pour en savoir plus sur les autorisations de sécurité nécessaires à la mise à niveau du client Configuration Manager à l’aide de la gestion d’applications, consultez [Sécurité et confidentialité pour la gestion des applications](/sccm/apps/plan-design/security-and-privacy-for-application-management).  


#### <a name="automatic-client-upgrades"></a>Mises à niveau automatiques des clients  

Vous devez avoir le rôle de sécurité **Administrateur complet** pour pouvoir configurer des mises à niveau automatiques des clients.  


### <a name="firewall-requirements"></a>Configuration requise du pare-feu  

S’il existe un pare-feu entre les serveurs du système de site et les ordinateurs sur lesquels vous souhaitez installer le client Configuration Manager, consultez [Paramètres de port et de pare-feu Windows pour les clients](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients).  



##  <a name="BKMK_prereqs_mobiledevices"></a> Prérequis pour les appareils mobiles clients  

Quand vous installez le client Configuration Manager sur des appareils mobiles et que vous les inscrivez, servez-vous de ces informations pour déterminer les prérequis.  

### <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

-   Autorité de certification d'entreprise Microsoft avec des modèles de certificats pour déployer et gérer les certificats requis pour les appareils mobiles.  

     L'autorité de certification émettrice doit automatiquement approuver les demandes de certificat de la part d'utilisateurs d'appareils mobiles lors du processus d'inscription.  

     Pour plus d’informations sur la configuration requise pour les certificats, consultez [Sécurité et confidentialité pour les profils de certificat](/sccm/protect/plan-design/security-and-privacy-for-certificate-profiles).  

-   Groupe de sécurité qui contient les utilisateurs pouvant inscrire leurs appareils mobiles.  

     Ce groupe de sécurité est utilisé pour configurer le modèle de certificat utilisé lors de l'inscription d'appareils mobiles.  

-   Facultatif mais recommandé : un alias DNS (enregistrement CNAME) nommé **ConfigMgrEnroll**. Configurez cet alias pour le nom de serveur du point proxy d’inscription.  

     Cet alias DNS est nécessaire à la prise en charge de la découverte automatique pour le service d’inscription. Si vous ne configurez pas cet enregistrement DNS, les utilisateurs doivent spécifier manuellement le nom du point proxy d’inscription pendant le processus d’inscription.  

-   Dépendances du rôle système de site pour les ordinateurs qui exécutent les rôles système de site point d’inscription et point proxy d’inscription.  

     Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  


### <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

Pour plus d’informations, consultez [Déterminer les rôles système de site pour les clients](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients).  

-   Point de gestion configuré pour les connexions client HTTPS et activé pour les appareils mobiles  

     Un point de gestion est toujours nécessaire pour installer le client Configuration Manager sur des appareils mobiles. En plus des exigences de configuration et d’activation de HTTPS pour les appareils mobiles, le point de gestion doit être configuré avec un nom de domaine complet Internet et accepter les connexions client en provenance d’Internet.  

-   Point d'inscription et point proxy d'inscription  

     Un point proxy d'inscription gère les demandes d'inscription de la part d'appareils mobiles et le point d'inscription termine le processus d'inscription. Le point d'inscription doit être dans la même forêt Active Directory que le serveur de site, mais le point proxy d'inscription peut être dans une autre forêt.  

-   Paramètres client pour l'inscription d'appareils mobiles  

     Configurez des paramètres client pour permettre aux utilisateurs d'inscrire des appareils mobiles et de configurer au moins un profil d'inscription.  

-   Point de Reporting Services  

     Le point de Reporting Services est un rôle de système de site, facultatif mais recommandé, qui peut afficher des rapports liés à l'inscription d'appareils mobiles et à la gestion de clients.  

     Pour plus d’informations, consultez [Rapports dans Configuration Manager](/sccm/core/servers/manage/reporting).  

-   Pour configurer l'inscription pour les appareils mobiles, vous devez disposer des autorisations de sécurité suivantes :  

    -   Pour ajouter, modifier et supprimer les rôles de système de site d’inscription : autorisation **Modifier** pour l’objet **Site** .  

    -   Pour configurer les paramètres clients de l’inscription : les paramètres clients par défaut nécessitent l’autorisation **Modifier** pour l’objet **Site** et les paramètres clients personnalisés nécessitent des autorisations **Agent client**  .  

     Le rôle de sécurité **Administrateur complet** comprend les autorisations nécessaires pour configurer les rôles de système de site d’inscription.  

     Pour gérer des appareils mobiles inscrits, vous devez disposer des autorisations de sécurité suivantes :  

    -   Pour réinitialiser ou retirer un appareil mobile : **Supprimer la ressource** pour l’objet **Collection** .  

    -   Pour annuler une réinitialisation ou retirer une commande : **Supprimer la ressource** pour l’objet **Collection** .  

    -   Pour autoriser et bloquer des appareils mobiles : **Modifier la ressource** pour l’objet **Collection** .  

    -   Pour verrouiller à distance ou réinitialiser le mot de passe sur un appareil mobile : **Modifier la ressource** pour l’objet **Collection** .  

     Le rôle de sécurité par défaut **Administrateur d’opérations** comprend les autorisations nécessaires pour la gestion des appareils mobiles.  

     Pour plus d’informations sur la configuration des autorisations de sécurité, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration) et [Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration).  


### <a name="firewall-requirements"></a>Configuration requise du pare-feu  

Les appareils réseau intervenants, tels que des routeurs et des pare-feu, ainsi que le Pare-feu Windows, le cas échéant, doivent autoriser le trafic associé à l'inscription d'appareils mobiles :  

-   Entre les appareils mobiles et le point proxy d'inscription : HTTPS (par défaut, TCP 443)  

-   Entre le point proxy d'inscription et le point d'inscription : HTTPS (par défaut, TCP 443)  


Si vous utilisez un serveur web proxy, il doit être configuré pour le tunnel SSL. Le pontage SSL n’est pas pris en charge pour les appareils mobiles.  
