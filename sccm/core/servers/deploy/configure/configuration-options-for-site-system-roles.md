---
title: Options de rôle de système de site
titleSuffix: Configuration Manager
description: Pour plus d’informations sur les rôles de système de site Configuration Manager qui ne sont pas nécessairement explicites, consultez cet article.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5651eaa7a69c6b75c37cb368973d1d3947e3a498
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341744"
---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Options de configuration pour les rôles de système de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La plupart des options de configuration pour les rôles de système de site System Center Configuration Manager sont explicites ou décrites dans l’Assistant ou des boîtes de dialogue lors de la configuration. Les sections suivantes expliquent les rôles de système de site dont les paramètres peuvent nécessiter des informations supplémentaires.  

##  <a name="BKMK_ApplicationCatalog_Website"></a> Point du site web du catalogue des applications  
 Pour plus d’informations sur la procédure de configuration du point du site web du catalogue des applications, consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Connexions client**  

 Sélectionnez **HTTPS** pour utiliser le paramètre de connexion le plus sécurisé et pour vérifier si les clients se connectent à partir d’Internet. Cette option nécessite un certificat PKI sur le serveur pour l'authentification du serveur sur les clients et pour le chiffrement des données sur le protocole SSL (Secure Socket Layer). Pour en savoir plus sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans Internet Information Services (IIS), consultez la section *Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS* dans la rubrique [Exemple détaillé de déploiement des certificats PKI pour Configuration Manager : Autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Ajouter le site web du catalogue des applications à la zone de sites de confiance**  

 Ce message affiche la valeur dans les paramètres du client par défaut, que le paramètre client **Ajouter le site Web du catalogue des applications dans la zone Sites approuvés d’Internet Explorer** ait la valeur **True** ou **False**. Si vous avez utilisé des paramètres client personnalisés pour configurer ce paramètre, vous devez vérifier cette valeur vous-même.  

 Si ce système de site est configuré pour un nom de domaine complet et si le site web ne se trouve pas dans la zone de sites approuvés dans Internet Explorer, les utilisateurs sont invités à entrer leurs informations d’identification quand ils se connectent au catalogue d’applications.  

 **Nom de l’organisation**  

 Entrez le nom que voient les utilisateurs dans le catalogue d’applications. Ces informations personnalisées aident les utilisateurs à identifier ce site web comme une source approuvée.  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> Point de service web du catalogue des applications  
 Pour plus d’informations sur la procédure de configuration du point de service web du catalogue des applications, consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Sélectionnez **HTTPS** pour authentifier les points de site Web du catalogue d'applications vers ce point de service Web du catalogue des applications.  Cette option nécessite un certificat PKI sur les serveurs qui exécutent le point de site web du catalogue d’applications pour l’authentification du serveur et le chiffrement des données sur le protocole SSL. Pour en savoir plus sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS, consultez la section *Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS* dans la rubrique [Exemple détaillé de déploiement des certificats PKI pour Configuration Manager : Autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_CertificateRegistrationPoint"></a> Point d’enregistrement de certificat  
 Pour en savoir plus sur la configuration du point d’enregistrement de certificat, consultez [Présentation des profils de certificat](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="BKMK_Distribution_Point"></a> Point de distribution  
 Pour en savoir plus sur la configuration du point de distribution pour le déploiement de contenu, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Pour en savoir plus sur la configuration du point de distribution pour les déploiements PXE, consultez [Utiliser PXE pour déployer Windows sur le réseau avec System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Pour en savoir plus sur la configuration du point de distribution pour les déploiements de multidiffusion, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau avec System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Installer et configurer IIS si requis par Configuration Manager**  
 Sélectionnez cette option pour permettre à Configuration Manager d’installer et de configurer IIS sur le système de site s’il n’est pas déjà installé. IIS doit être installé sur tous les points de distribution, et vous devez sélectionner ce paramètre pour continuer dans l'Assistant.  

 **Compte d’installation du système de site**  
 Pour les points de distribution qui sont installés sur un serveur de site, seul le compte d'ordinateur du serveur du site est pris en charge pour être utilisé comme compte d'installation de système de site.  

 **Créer un certificat auto-signé ou importer un certificat client PKI**  
 Ce certificat a deux objectifs :  

1.  Il authentifie le point de distribution à un point de gestion avant que le point de distribution n'envoie des messages d'état.  

2.  Quand l’option **Activer la prise en charge PXE pour les clients** est sélectionnée, le certificat est envoyé aux ordinateurs qui effectuent un démarrage PXE pour qu’ils puissent se connecter à un point de gestion pendant le déploiement du système d’exploitation.  

Quand tous vos points de gestion du site sont configurés pour le protocole HTTP, créez un certificat auto-signé. Quand vos points de gestion sont configurés pour le protocole HTTPS, importez un certificat client PKI.  

Pour importer le certificat, accédez à un fichier PKCS #12 (Public Key Cryptography Standard #12) qui contient un certificat PKI avec les spécifications suivantes pour Configuration Manager :  

-   L'utilisation prévue doit inclure l'authentification du client.  

-   La clé privée doit être configurée pour l’exportation.  

Il n'existe aucune exigence particulière pour le Nom d'objet ou l'Autre nom de l'objet du certificat, et vous pouvez utiliser le même certificat pour plusieurs points de distribution.  

Pour en savoir plus sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Pour obtenir un exemple de déploiement de ce certificat, consultez la section *Déploiement du certificat client pour les points de distribution* de la rubrique [Exemple détaillé de déploiement des certificats PKI pour Configuration Manager : Autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Activer ce point de distribution pour le contenu préparé**  
Cochez cette case pour activer le point de distribution pour le contenu préparé. Quand cette case est cochée, vous pouvez configurer le comportement de distribution durant la distribution du contenu. Vous pouvez choisir de toujours préparer le contenu sur le point de distribution, de préparer le contenu initial pour le package mais d’utiliser le processus de distribution de contenu normal pour les mises à jour du contenu, ou de toujours utiliser le processus de distribution de contenu normal pour le contenu du package.  

**Groupes de limites**  
 Vous pouvez associer des groupes de limites à un point de distribution. Lors d'un déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé au point de distribution pour l'utiliser comme emplacement source pour le contenu.
 - **Avant la version 1610**, vous pouviez cocher la case **Autoriser un emplacement source de secours pour le contenu** pour permettre aux clients situés en dehors de ces groupes de limites de revenir et d’utiliser le point de distribution comme emplacement source pour le contenu quand aucun autre point de distribution n’est disponible.
 - **À partir de la version 1610**, vous ne pouvez plus configurer l’option **Autoriser un emplacement source de secours pour le contenu**.  Au lieu de cela, vous configurez des relations entre les groupes de limites qui vérifient quand un client peut commencer à rechercher des emplacements sources pour le contenu valides dans d’autres groupes de limites.

##  <a name="BKMK_Enrollment_Point"></a> Point d’inscription  
Les points d’inscription sont utilisés pour installer les ordinateurs Mac et inscrire les appareils que vous gérez avec la gestion des appareils mobiles locale. Pour plus d'informations, consultez :  

-   [Guide pratique pour déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale dans System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Connexions autorisées**  
 Ce paramètre HTTPS est sélectionné automatiquement et nécessite un certificat PKI sur le serveur pour l’authentification du serveur sur le point proxy d’inscription, l’authentification du serveur sur le point de service hors bande, ainsi que le chiffrement des données sur SSL. Pour en savoir plus sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS, consultez la section *Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS* dans la rubrique [Exemple détaillé de déploiement des certificats PKI pour Configuration Manager : Autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> Point proxy d’inscription  
Pour en savoir plus sur la configuration d’un point proxy d’inscription pour les appareils mobiles, consultez [Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale dans System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Connexions client**  
 Le paramètre HTTPS est sélectionné automatiquement. Il nécessite un certificat PKI sur le serveur pour l’authentification du serveur sur les appareils mobiles et les ordinateurs Mac inscrits par Configuration Manager, ainsi que pour le chiffrement des données avec SSL (Secure Sockets Layer). Pour en savoir plus sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Pour obtenir un exemple de déploiement du certificat de serveur et des informations sur la manière de le configurer dans IIS, consultez la section *Déploiement du certificat de serveur Web pour les systèmes de site qui exécutent IIS* dans la rubrique [Exemple détaillé de déploiement des certificats PKI pour Configuration Manager : Autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Fallback_Status_Point"></a> Point d’état de secours  
**Nombre de messages d'état** et **Intervalle d'accélération (en secondes)**  
Bien que les paramètres par défaut pour ces options (10 000 messages d'état et 3 600 secondes pour l'intervalle d'accélération) suffisent dans la plupart des cas, vous pouvez être amené à les modifier lorsque les deux conditions suivantes sont vraies :  

-   Le point d'état de secours accepte les connexions uniquement à partir de l'intranet.  

-   Vous utilisez le point d'état de secours pendant un déploiement du client pour de nombreux ordinateurs.  

Dans ce scénario, un flux continu de messages d’état peut créer un retard des messages d’état susceptible d’entraîner une utilisation élevée du processeur sur le serveur de site pendant une période prolongée. En outre, vous risquez de ne pas voir les informations récentes sur le déploiement du client dans la console Configuration Manager et dans les rapports de déploiement du client.  

Ces paramètres de point d’état de secours visent à être configurés pour les messages d’état générés durant le déploiement du client. Ils ne sont pas destinés à être configurés pour les problèmes de communication que peuvent rencontrer les clients, notamment lorsque ceux-ci se trouvent sur Internet et qu’ils ne parviennent pas à se connecter à leur point de gestion Internet. Comme le point d'état de secours ne peut pas appliquer ces paramètres aux seuls messages d'état générés lors du déploiement du client, ne configurez pas ces paramètres lorsque le point d'état de secours accepte les connexions en provenance d'Internet.  

Chaque ordinateur qui installe correctement le client System Center 2012 Configuration Manager envoie les quatre messages d’état ci-dessous au point d’état de secours :  

-   Démarrage du déploiement du client  

-   Déploiement du client réussi  

-   Démarrage de l'attribution du client  

-   Attribution du client réussie  

Les ordinateurs qui ne peuvent pas être installés ou qui affectent le client Configuration Manager envoient des messages d’état supplémentaires.  

Par exemple, si vous déployez le client Configuration Manager sur 20 000 ordinateurs, le déploiement peut envoyer 80 000 messages d’état au point d’état de secours. La configuration d’accélération par défaut permet l’envoi d’un maximum de 10 000 messages d’état au point d’état de secours toutes les 3,600 secondes (1 heure), c’est pourquoi les messages d’état peuvent être retardés sur le point d’état de secours. Vous devez également prendre en compte la largeur de bande réseau disponible entre le point d’état de secours et le serveur de site, ainsi que la capacité du serveur de site à traiter de nombreux messages d’état.  

Pour éviter ces problèmes, envisagez d’augmenter le nombre de messages d’état et de diminuer l’intervalle d’accélération.  

Réinitialisez les valeurs d'accélération pour le point d'état de secours si l'une des conditions suivantes est vraie :  

-   Les valeurs d'accélération actuelles sont supérieures aux valeurs requises pour traiter les messages d'état à partir du point d'état de secours.  

-   Vous trouvez que les paramètres d'accélération actuels entraînent une utilisation élevée du processeur sur le serveur de site.  

Ne modifiez pas les paramètres d'accélération du point d'état de secours avant d'en avoir mesuré les conséquences. Par exemple, lorsque vous augmentez les paramètres d'accélération jusqu'à ce qu'ils atteignent un niveau élevé, l'utilisation du processeur sur le serveur de site peut devenir élevée, ce qui ralentit tout le fonctionnement du site.  
