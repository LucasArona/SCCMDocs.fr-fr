---
title: Planifier des rôles de système de site
titleSuffix: Configuration Manager"
description: Envisagez l’utilisation de serveurs de système de site et de rôles de système de site quand vous planifiez votre hiérarchie Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6805aed620ea6bd41d1ec3460c1076b44d28f67a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385352"
---
# <a name="plan-for-site-system-servers-and-site-system-roles-in-configuration-manager"></a>Planifier des serveurs de système de site et des rôles de système de site dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque site Configuration Manager que vous installez comprend un serveur de site qui est un **serveur de système de site**. Le site peut également inclure des serveurs de système de site supplémentaires sur des ordinateurs distants par rapport au serveur de site. Les serveurs de système de site (serveur de site ou serveur de système de site distant) prennent en charge les **rôles de système de site**.  


##  <a name="bkmk_siteservers"></a> Serveurs de système de site  

Lorsque vous installez un rôle de système de site sur un ordinateur, celui-ci devient un serveur de système de site. Sur chaque site, vous pouvez installer un ou plusieurs serveurs de système de site supplémentaires. Vous n’avez pas besoin d’installer des serveurs de système de site supplémentaires et vous pouvez choisir d’exécuter tous les rôles de système de site directement sur l’ordinateur serveur de site. Chaque serveur de système de site prend en charge un ou plusieurs rôles de système de site. Les serveurs supplémentaires permettent d’augmenter les fonctionnalités et les capacités d’un site en partageant la charge de traitement que les rôles de système de site font peser sur un serveur.  

Lorsque vous envisagez l’ajout d’un serveur de système de site, assurez-vous que le serveur répond aux conditions requises pour l’utilisation prévue. De même, ajoutez-le à un emplacement réseau qui a une bande passante suffisante pour communiquer avec les points de terminaison attendus. Ces points de terminaison incluent le serveur de site, les ressources du domaine, un emplacement cloud, des serveurs de système de site et des clients.  



##  <a name="bkmk_planroles"></a> Rôles système de site  

Installez les rôles de système de site sur un serveur pour fournir au site des capacités supplémentaires. En voici quelques exemples :  

-   Points de gestion supplémentaires permettant au site de prendre en charge davantage d’appareils, jusqu’à sa capacité maximale.  

-   Points de distribution supplémentaires pour développer votre infrastructure de contenu, ce qui améliore les performances des distributions de contenu aux appareils.  

-   Un ou plusieurs rôles de système de site propres aux fonctions. Par exemple, un point de mise à jour logicielle vous permet de gérer les mises à jour logicielles pour les appareils gérés. Un point de Reporting Services vous permet d’exécuter des rapports pour surveiller, comprendre et partager des informations sur votre environnement.  


Différents sites Configuration Manager peuvent prendre en charge différents ensembles de rôles de système de site. L’ensemble de rôles de système de site pris en charge varie selon le type de site. (Les différents types de sites sont : site d’administration centrale, sites principaux ou sites secondaires.) La topologie de votre hiérarchie peut limiter le placement de certains rôles sur certains types de sites. Par exemple, le point de connexion de service est pris en charge seulement sur le site de plus haut niveau de la hiérarchie. Le site de plus haut niveau peut être un site d’administration centrale ou un site principal autonome. Ce rôle n’est pas pris en charge sur un site principal enfant ou sur des sites secondaires.  

Après l’installation d’un site, vous pouvez déplacer certains rôles de système de site depuis leur emplacement par défaut sur le serveur de site vers un autre serveur. Par exemple, les rôles de point de gestion ou de point de distribution sont installés par défaut sur un serveur de site principal ou secondaire. De même, installez des instances supplémentaires de certains rôles de système de site pour étendre les capacités de votre site et répondre à vos besoins métier. Certains rôles sont obligatoires, tandis que d’autres sont facultatifs.  

#### <a name="configuration-manager-site-server"></a>Serveur de site Configuration Manager
Ce rôle identifie le serveur sur lequel le programme d’installation de Configuration Manager est exécuté pour installer un site, ou le serveur sur lequel vous installez un site secondaire. Vous ne pouvez pas déplacer ou désinstaller ce rôle tant que le site n’est pas désinstallé.  

#### <a name="configuration-manager-site-system"></a>Système de site Configuration Manager
Ce rôle est attribué à tout ordinateur sur lequel vous installez un site ou un rôle de système de site. Vous ne pouvez pas déplacer ou désinstaller ce rôle tant que vous n’avez pas supprimé le dernier rôle de système de site de l’ordinateur.  

#### <a name="configuration-manager-component-site-system-role"></a>Rôle de système de site de composant Configuration Manager
Ce rôle identifie un système de site qui exécute une instance du service **SMS Executive**. Il est obligatoire de prendre en charge d’autres rôles, comme les points de gestion. Vous ne pouvez pas déplacer ou désinstaller ce rôle tant que vous n’avez pas supprimé le dernier rôle de système de site applicable de l’ordinateur.  

#### <a name="configuration-manager-site-database-server"></a>Serveur de base de données de site Configuration Manager
Le site attribue ce rôle aux serveurs de système de site qui contiennent une instance de la base de données de site. Déplacez ce rôle vers un nouveau serveur seulement en exécutant le programme d’installation pour modifier le site de façon à ce qu’il utilise une autre instance SQL Server pour héberger la base de données de site.  

#### <a name="sms-provider"></a>Fournisseur SMS
Le site attribue ce rôle à chaque ordinateur qui héberge une instance du fournisseur SMS. Le fournisseur SMS est l’interface entre une console Configuration Manager et la base de données de site. Par défaut, ce rôle est installé automatiquement sur le serveur de site d’un site d’administration centrale et sur les sites principaux. Installez des instances supplémentaires sur chaque site pour fournir un accès à d’autres utilisateurs administratifs ou pour la redondance.  

Pour installer des fournisseurs supplémentaires, exécutez le programme d’installation de Configuration Manager afin de [gérer le fournisseur SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider). Ensuite, installez d’autres fournisseurs sur d’autres ordinateurs. Installez une seule instance du fournisseur SMS sur un ordinateur. Cet ordinateur doit se trouver dans le même domaine que le serveur de site.  

#### <a name="application-catalog-web-service-point"></a>Point de service web du catalogue des applications
Un rôle de système de site qui fournit des informations sur les logiciels au site web du catalogue d’applications à partir de la bibliothèque de logiciels. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

#### <a name="application-catalog-website-point"></a>Point du site web du catalogue des applications
Un rôle de système de site qui fournit aux utilisateurs une liste des logiciels disponibles à partir du catalogue d'applications. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

Si le catalogue d’applications prend en charge des ordinateurs clients sur Internet, pour une meilleure sécurité, installez le point de site web du catalogue d’applications dans un réseau de périmètre. Installez ensuite le rôle de service web du catalogue d’applications sur l’intranet.  

#### <a name="asset-intelligence-synchronization-point"></a>Point de synchronisation Asset Intelligence
Ce rôle de système de site se connecte à Microsoft afin de télécharger des informations pour le catalogue Asset Intelligence. Ce rôle charge également les titres sans catégorie, pour que Microsoft puisse les prendre en compte en vue de leur future intégration dans le catalogue. Une hiérarchie prend en charge une seule instance de ce rôle, sur le site de plus haut niveau de votre hiérarchie. Si vous étendez un site principal autonome dans une hiérarchie plus grande, désinstallez ce rôle du site principal. Installez-le ensuite sur le site d’administration centrale. 

Pour plus d’informations, consultez [Asset Intelligence dans Configuration Manager](/sccm/core/clients/manage/asset-intelligence/introduction-to-asset-intelligence).  

#### <a name="certificate-registration-point"></a>Point d'enregistrement de certificat
Un rôle de système de site communique avec un serveur qui exécute le service d’inscription de périphériques réseau (NDES, Network Device Enrollment Service). Il gère les demandes de certificat de périphérique qui utilisent le protocole SCEP (Simple Certificate Enrollment Protocol). Ce rôle est pris en charge uniquement sur des sites principaux et le site d’administration centrale.

Bien qu’un point d’enregistrement de certificat puisse fournir une fonctionnalité à une hiérarchie entière, vous pouvez installer plusieurs instances de ce rôle sur un site et sur plusieurs sites dans la même hiérarchie. Cette conception permet l’équilibrage de la charge. Quand plusieurs instances existent dans une hiérarchie, des clients sont affectés de façon aléatoire à l’un des points d’enregistrement de certificat.  

Chaque point d’enregistrement de certificat nécessite un accès à une instance distincte du service NDES. Vous ne pouvez pas configurer plusieurs points d’enregistrement de certificat pour qu’ils utilisent la même instance du service NDES. En outre, n’installez pas le point d’enregistrement de certificat sur le même serveur que celui qui exécute le service NDES.  

#### <a name="cloud-management-gateway-connection-point"></a>Point de connexion de la passerelle de gestion cloud
Ce rôle de système de site communique avec la [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

#### <a name="data-warehouse-service-point"></a>Point de service de l’entrepôt de données
Utilisez le point de service de l’entrepôt de données pour stocker des données d’historique à long terme et créer des rapports sur celles-ci dans votre environnement Configuration Manager. Pour plus d’informations, consultez [Entrepôt de données](/sccm/core/servers/manage/data-warehouse).  

#### <a name="distribution-point"></a>Point de distribution
Un rôle de système de site qui contient des fichiers sources que les clients doivent télécharger, par exemple : 
- Contenu d’application
- Packages logiciels
- Mises à jour logicielles
- Images de système d’exploitation
- Images de démarrage  

Par défaut, ce rôle est installé sur le serveur de site quand vous installez un nouveau site principal ou secondaire. Ce rôle n’est pas pris en charge sur un site d’administration centrale. Installez plusieurs instances de ce rôle sur un site pris en charge et sur plusieurs sites de la même hiérarchie. Pour plus d’informations, consultez [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management) et [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

#### <a name="endpoint-protection-point"></a>Point Endpoint Protection
Configuration Manager utilise ce rôle de système de site pour accepter le contrat de licence Endpoint Protection et configurer l’appartenance par défaut à Microsoft Active Protection Service. Une hiérarchie prend en charge une seule instance de ce rôle et seulement sur le site de plus haut niveau. Si vous étendez un site principal autonome à une hiérarchie plus grande, désinstallez ce rôle du site principal, puis installez-le sur le site d’administration centrale. Pour plus d’informations, consultez [Endpoint Protection dans Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).  

#### <a name="enrollment-point"></a>Point d'inscription
Un rôle de système de site qui utilise des certificats PKI pour permettre à Configuration Manager d’inscrire des appareils mobiles et des ordinateurs macOS. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

Si un utilisateur inscrit des appareils mobiles avec Configuration Manager et que son compte Active Directory se trouve dans une forêt non approuvée par la forêt du serveur de site, installez un point d’inscription dans la forêt de l’utilisateur. Configuration Manager peut alors authentifier l’utilisateur.  

#### <a name="enrollment-proxy-point"></a>Point proxy d'inscription
Un rôle de système de site qui gère les demandes d’inscription Configuration Manager provenant d’appareils mobiles et d’ordinateurs macOS. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

Quand vous prenez en charge des appareils mobiles sur Internet, installez un point proxy d’inscription dans un réseau de périmètre, et installez-en un sur l’intranet.   

#### <a name="exchange-server-connector"></a>Connecteur Exchange Server
Pour plus d’informations sur ce rôle, consultez [Gérer des appareils mobiles à l’aide de Configuration Manager et d’Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

#### <a name="fallback-status-point"></a>Point d’état de secours
Un rôle de système de site qui vous permet de surveiller l’installation des clients. Il identifie les clients qui ne sont pas gérés, car ils ne peuvent pas communiquer avec leur point de gestion. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site et sur plusieurs sites dans la même hiérarchie.     

#### <a name="management-point"></a>Point de gestion
Un rôle de système de site qui fournit aux clients des informations sur l’emplacement des services et des stratégies. Il reçoit également des données de configuration des clients.  

Par défaut, ce rôle est installé sur le serveur de site quand vous installez un nouveau site principal ou secondaire. Les sites principaux prennent en charge plusieurs instances de ce rôle. Les sites secondaires prennent en charge un seul point de gestion. Également appelé point de gestion proxy, ce rôle sur un site secondaire fournit un point de contact local permettant aux clients d’obtenir des stratégies d’ordinateur et d’utilisateur.  

Configurez des points de gestion pour prendre en charge HTTP ou HTTPS. Ils peuvent également en charge les appareils mobiles que vous gérez avec la gestion des appareils mobiles (MDM) locale de Configuration Manager. Pour réduire la charge de traitement placée sur le serveur de base de données du site par les points de gestion à mesure qu’ils répondent aux demandes des clients, utilisez des [réplicas de base de données pour les points de gestion](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reporting-services-point"></a>Point de Reporting Services
Rôle de système de site qui est intégré à SQL Server Reporting Services pour créer et gérer des rapports pour Configuration Manager. Ce rôle est pris en charge sur les sites principaux et le site d’administration centrale, et vous pouvez en installer plusieurs instances sur un site pris en charge. Pour plus d’informations, consultez [Planification de la génération de rapports](/sccm/core/servers/manage/planning-for-reporting).  

#### <a name="service-connection-point"></a>point de connexion de service
Un rôle de système de site qui charge les données d’utilisation à partir de votre site et qui est nécessaire pour mettre les mises à jour de Configuration Manager disponibles dans la console. Ce rôle permet également de gérer les appareils mobiles avec Microsoft Intune et avec la gestion MDM locale. Une hiérarchie prend en charge une seule instance de ce rôle et seulement sur le site de plus haut niveau de votre hiérarchie. Si vous étendez un site principal autonome à une hiérarchie plus grande, désinstallez ce rôle du site principal, puis installez-le sur le site d’administration centrale. Pour plus d’informations, consultez [À propos du point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

#### <a name="software-update-point"></a>Point de mise à jour logicielle
Un rôle de système de site qui est intégré à Windows Server Update Services (WSUS) pour fournir des mises à jour logicielles aux clients Configuration Manager. Ce rôle est pris en charge sur tous les sites :  

-   Installez ce système de site sur le site d’administration centrale pour une synchronisation avec WSUS.  

-   Configurez chaque instance de ce rôle sur les sites principaux enfants à synchroniser avec le site d’administration centrale.  

-   Quand le transfert de données sur le réseau est lent, vous pouvez envisager d’installer un point de mise à jour logicielle sur des sites secondaires.  

Pour plus d’informations, consultez [Planifier les mises à jour logicielles](/sccm/sum/plan-design/plan-for-software-updates).  

#### <a name="state-migration-point"></a>Point de migration d’état
Quand vous migrez un ordinateur vers un nouveau système d’exploitation, ce rôle de système de site stocke les données d’état utilisateur. Ce rôle est pris en charge sur les sites principaux et les sites secondaires. Installez plusieurs instances de ce rôle sur un site et sur plusieurs sites de la même hiérarchie. Pour plus d’informations sur le stockage de l’état utilisateur quand vous déployez un système d’exploitation, consultez [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state).  



## <a name="next-steps"></a>Étapes suivantes

Certains rôles de système de site Configuration Manager nécessitent des connexions à Internet. Si votre environnement nécessite l’utilisation d’un serveur proxy pour le trafic Internet, configurez ces rôles de système de site pour qu’ils utilisent le proxy. Pour plus d’informations, consultez [Prise en charge des serveurs proxy](/sccm/core/plan-design/network/proxy-server-support).  