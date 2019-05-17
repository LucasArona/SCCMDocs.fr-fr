---
title: Options de rôle de système de site
titleSuffix: Configuration Manager
description: Pour plus d’informations sur les rôles de système de site Configuration Manager qui ne sont pas nécessairement explicites, consultez cet article.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5fb9a553efa634dad314da58298611cdf0bbb58
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498977"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Options de configuration pour les rôles de système de site dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La plupart des options de configuration pour les rôles de système de site Configuration Manager sont explicites ou décrites dans l’Assistant ou des boîtes de dialogue lors de la configuration. Les sections suivantes expliquent les rôles de système de site dont les paramètres peuvent nécessiter des informations supplémentaires.  



##  <a name="BKMK_ApplicationCatalog_Website"></a> Point du site web du catalogue des applications  

> [!Note]  
> À compter de la version 1806, le point du site Web du catalogue des applications n’est plus *requis*, mais il est toujours *pris en charge*. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).  
> 
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

 Pour plus d’informations sur la procédure de configuration du point du site Web du catalogue des applications, consultez [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="client-connections"></a>Connexions client
 Sélectionnez **HTTPS** pour utiliser le paramètre de connexion le plus sécurisé et pour vérifier si les clients se connectent à partir d’Internet. Cette option nécessite un certificat PKI sur le serveur pour l'authentification du serveur sur les clients et pour le chiffrement des données sur le protocole SSL (Secure Socket Layer). Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS (Internet Information Services), consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>Ajouter le site Web du catalogue d'applications à la zone de sites approuvés  
 Ce message affiche la valeur dans les paramètres du client par défaut, que le paramètre client **Ajouter le site Web du catalogue des applications dans la zone Sites approuvés d’Internet Explorer** ait la valeur **True** ou **False**. Si vous avez utilisé des paramètres client personnalisés pour configurer ce paramètre, activez ce dernier.  

 Si ce système de site est configuré pour un nom de domaine complet et si le site web ne se trouve pas dans la zone de sites approuvés dans Internet Explorer, les utilisateurs sont invités à entrer leurs informations d’identification quand ils se connectent au catalogue d’applications.  

 #### <a name="organization-name"></a>Nom de l'organisation  

 Entrez le nom que voient les utilisateurs dans le catalogue d’applications. Ces informations personnalisées aident les utilisateurs à identifier ce site web comme une source approuvée.  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> Point de service web du catalogue des applications  

> [!Note]  
> À compter de la version 1806, le point de service Web du catalogue des applications n’est plus *requis*, mais il est toujours *pris en charge*. Pour plus d'informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).  

 Pour plus d’informations sur la procédure de configuration du point de service Web du catalogue des applications, consultez [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="https"></a>HTTPS

 Sélectionnez **HTTPS** pour authentifier les points de site Web du catalogue d'applications vers ce point de service Web du catalogue des applications. Cette option nécessite un certificat PKI sur les serveurs qui exécutent le point du site Web du catalogue des applications pour l’authentification du serveur et le chiffrement des données sur le protocole SSL. Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS (Internet Information Services), consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_CertificateRegistrationPoint"></a> Point d’enregistrement de certificat  

 Pour plus d’informations sur la configuration du point d’enregistrement de certificat, consultez [Présentation des profils de certificat](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  



##  <a name="BKMK_Distribution_Point"></a> Point de distribution  

 Pour plus d’informations sur la configuration du point de distribution pour le déploiement de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

 Pour plus d’informations sur la configuration du point de distribution pour les déploiements PXE, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

 Pour plus d’informations sur la configuration du point de distribution pour les déploiements de multidiffusion, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Installer et configurer IIS si requis par Configuration Manager
 Sélectionnez cette option pour permettre à Configuration Manager d’installer et de configurer IIS sur le système de site s’il n’est pas déjà installé. IIS doit être installé sur tous les points de distribution, et vous devez sélectionner ce paramètre pour continuer dans l'Assistant.  

 #### <a name="site-system-installation-account"></a>Compte d'installation du système de site
 Pour les points de distribution qui sont installés sur un serveur de site, seul le compte d'ordinateur du serveur du site est pris en charge pour être utilisé comme compte d'installation de système de site. Pour plus d’informations, voir [Comptes](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>Créer un certificat auto-signé ou importer un certificat client PKI
 Ce certificat a deux objectifs :  

1.  Il authentifie le point de distribution à un point de gestion avant que le point de distribution n'envoie des messages d'état.  

2.  Lorsque l’option **Activer la prise en charge PXE pour les clients** est sélectionnée, le certificat est envoyé aux ordinateurs pour le démarrage de PXE. Ils utilisent ce certificat pour se connecter à un point de gestion pendant le déploiement du système d’exploitation.  

Quand tous vos points de gestion du site sont configurés pour le protocole HTTP, créez un certificat auto-signé. Quand vos points de gestion sont configurés pour le protocole HTTPS, importez un certificat client PKI.  

Pour importer le certificat, accédez à un fichier PKCS #12 (Public Key Cryptography Standard #12) qui contient un certificat PKI avec les spécifications suivantes pour Configuration Manager :  

-   L'utilisation prévue doit inclure l'authentification du client.  

-   La clé privée doit être configurée pour l’exportation.  

Il n’existe aucune exigence particulière pour le nom de l’objet du certificat ou l’autre nom de l’objet (SAN). Vous pouvez utiliser le même certificat pour plusieurs points de distribution.  

Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements). 

Pour obtenir un exemple de déploiement de ce certificat, consultez [Déploiement du certificat client pour les points de distribution](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>Activer ce point de distribution pour le contenu préparé
Cochez cette case pour activer le point de distribution pour le contenu préparé. Lorsque vous activez cette option, vous pouvez configurer le comportement de distribution durant la distribution du contenu. Vous pouvez choisir de toujours préparer le contenu sur le point de distribution, de préparer le contenu initial pour le package mais d’utiliser le processus de distribution de contenu normal pour les mises à jour du contenu, ou de toujours utiliser le processus de distribution de contenu normal pour le contenu du package. Pour plus d’informations, consultez [Contenu préparé](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

#### <a name="boundary-groups"></a>Groupes de limites
 Vous pouvez associer des groupes de limites à un point de distribution. Lors d'un déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé au point de distribution pour l'utiliser comme emplacement source pour le contenu. Configurez des relations entre les groupes de limites qui vérifient quand un client peut commencer à rechercher des emplacements sources valides pour le contenu dans d’autres groupes de limites. Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).



##  <a name="BKMK_Enrollment_Point"></a> Point d’inscription  

Les points d’inscription sont utilisés pour installer les ordinateurs macOS et inscrire les appareils que vous gérez avec la gestion des appareils mobiles locale. Pour plus d’informations, consultez les articles suivants :  

-   [Guide pratique pour déployer des clients sur des ordinateurs Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>Connexions autorisées
 Ce paramètre HTTPS est sélectionné automatiquement et nécessite un certificat PKI sur le serveur pour l’authentification du serveur sur le point proxy d’inscription, l’authentification du serveur sur le point de service hors bande, ainsi que le chiffrement des données sur SSL. Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS, consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> Point proxy d’inscription  

Pour plus d’informations sur la configuration d’un point proxy d’inscription pour les appareils mobiles, consultez [Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

#### <a name="client-connections"></a>Connexions client
 Le paramètre HTTPS est sélectionné automatiquement. Il requiert que les certificats PKI suivants soient présents sur le serveur : 
- Pour l’authentification serveur sur les appareils mobiles et les ordinateurs Mac que vous inscrivez avec Configuration Manager 
- Pour le chiffrement des données via SSL (Secure Sockets Layer)

Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS, consultez [Déploiement du certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Fallback_Status_Point"></a> Point d’état de secours  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Nombre de messages d’état et Intervalle d’accélération (en secondes)
Les paramètres par défaut pour ces options sont 10 000 messages d’état et 3 600 secondes pour l’intervalle d’accélération. Bien que ces paramètres soient adaptés à la plupart des cas, vous devrez peut-être les modifier lorsque les deux conditions suivantes sont remplies :  

-   Le point d'état de secours accepte les connexions uniquement à partir de l'intranet.  

-   Vous utilisez le point d'état de secours pendant un déploiement du client pour de nombreux ordinateurs.  

Dans ce scénario, un flux continu de messages d’état peut créer un retard des messages d’état susceptible d’entraîner une utilisation élevée du processeur sur le serveur de site pendant une période prolongée. En outre, vous risquez de ne pas voir les informations récentes sur le déploiement du client dans la console Configuration Manager et dans les rapports de déploiement du client.  

Ces paramètres de point d’état de secours visent à être configurés pour les messages d’état générés durant le déploiement du client. Ils ne sont pas destinés à être configurés pour les problèmes de communication que peuvent rencontrer les clients, notamment lorsque ceux-ci se trouvent sur Internet et qu’ils ne parviennent pas à se connecter à leur point de gestion Internet. Comme le point d’état de secours ne peut pas appliquer ces paramètres aux seuls messages d’état générés lors du déploiement du client, ne configurez pas ces paramètres lorsque le point d’état de secours accepte les connexions en provenance d’Internet.  

Chaque ordinateur qui installe correctement le client Configuration Manager envoie les quatre messages d’état ci-dessous au point d’état de secours :  

-   Démarrage du déploiement du client  

-   Déploiement du client réussi  

-   Démarrage de l'attribution du client  

-   Attribution du client réussie  

Les ordinateurs qui ne peuvent pas être installés ou qui attribuent le client Configuration Manager envoient des messages d’état supplémentaires.  

Par exemple, si vous déployez le client Configuration Manager sur 20 000 ordinateurs, le déploiement peut envoyer 80 000 messages d’état au point d’état de secours. La configuration d’accélération par défaut permet l’envoi d’un maximum de 10 000 messages d’état au point d’état de secours toutes les 3,600 secondes (1 heure), c’est pourquoi les messages d’état peuvent être retardés sur le point d’état de secours. Vous devez également prendre en compte la largeur de bande réseau disponible entre le point d’état de secours et le serveur de site, ainsi que la capacité du serveur de site à traiter de nombreux messages d’état.  

Pour éviter ces problèmes, envisagez d’augmenter le nombre de messages d’état et de diminuer l’intervalle d’accélération.  

Réinitialisez les valeurs d'accélération pour le point d'état de secours si l'une des conditions suivantes est vraie :  

-   Les valeurs d'accélération actuelles sont supérieures aux valeurs requises pour traiter les messages d'état à partir du point d'état de secours.  

-   Vous trouvez que les paramètres d’accélération actuels entraînent une utilisation élevée du processeur sur le serveur de site.  

Ne modifiez pas les paramètres d’accélération du point d’état de secours avant d’en avoir mesuré les conséquences. Par exemple, lorsque vous augmentez les paramètres d’accélération jusqu’à ce qu’ils atteignent un niveau élevé, l’utilisation du processeur sur le serveur de site peut devenir élevée, ce qui ralentit tout le fonctionnement du site.  
