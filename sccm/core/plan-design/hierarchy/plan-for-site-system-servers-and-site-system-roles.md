---
title: Planifier des rôles de système de site
titleSuffix: Configuration Manager
description: Envisagez l’utilisation de serveurs de système de site et de rôles de système de site au moment de planifier votre hiérarchie System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0a7415ba-2c53-4433-983e-780e92aa662f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 252c8544d4d976e210448c7deb285cfbe8b71a0f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-site-system-servers-and-site-system-roles-for-system-center-configuration-manager"></a>Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque site System Center Configuration Manager que vous installez comprend un serveur de site qui est un **serveur de système de site**. Le site peut également inclure des serveurs de système de site supplémentaires sur des ordinateurs distants par rapport au serveur de site. Les serveurs de système de site (serveur de site ou serveur de système de site distant) prennent en charge les **rôles de système de site**.


##  <a name="bkmk_siteservers"></a> Serveurs de système de site  
 Lorsque vous installez un rôle de système de site sur un ordinateur, celui-ci devient un serveur de système de site. Sur chaque site, vous pouvez installer un ou plusieurs serveurs de système de site supplémentaires. Vous pouvez également décider de ne pas installer de serveurs de système de site supplémentaires et exécuter tous les rôles de système de site directement sur l’ordinateur serveur de site. Chaque serveur de système de site prend en charge un ou plusieurs rôles de système de site. Les serveurs supplémentaires permettent d’augmenter les fonctionnalités et capacités d’un site en partageant la charge de traitement du processeur que les rôles de système de site font peser sur un serveur.  

 Lorsque vous envisagez l’ajout d’un serveur de système de site, assurez-vous que le serveur répond aux conditions requises pour l’utilisation prévue. Il est également judicieux de l’ajouter à un emplacement réseau bénéficiant d’une bande passante suffisante pour communiquer avec les points de terminaison attendus, y compris le serveur de site, les ressources de domaine, un emplacement cloud, les serveurs de système de site et les clients).  

 Si vous configurez le serveur de système de site avec un proxy pour une utilisation par des rôles de système de site, consultez [Rôles système de site pouvant utiliser un serveur proxy](#bkmk_proxy).  

##  <a name="bkmk_planroles"></a> Rôles système de site  
 Des rôles système de site sont installés sur un ordinateur pour fournir au site des fonctionnalités supplémentaires. En voici quelques exemples :  

-   Points de gestion supplémentaires permettant au site de prendre en charge davantage d’appareils, jusqu’à sa capacité maximale.  

-   Points de distribution supplémentaires pour développer votre infrastructure de contenu, ce qui améliore les performances des distributions de contenu aux appareils et utilisateurs.  

-   Un ou plusieurs rôles de système de site propres aux fonctions. Par exemple, un point de mise à jour logicielle vous permet de gérer les mises à jour logicielles des appareils pris en charge. Un point de Reporting Services vous permet de générer des rapports pour analyser et comprendre votre déploiement, ou partager des informations sur ce dernier.  


Différents sites Configuration Manager peuvent prendre en charge différents ensembles de rôles de système de site. L’ensemble pris en charge de rôles de système de site dépend du type de site (site d’administration centrale, site principal ou site secondaire). La topologie de votre hiérarchie peut limiter le placement de certains rôles sur certains types de sites. Par exemple, le point de connexion de service est pris en charge uniquement sur le site de niveau supérieur de la hiérarchie, qui peut être un site d’administration centrale ou un site principal autonome. Ce rôle n’est pas pris en charge sur un site principal enfant ou sur des sites secondaires.  

Après l’installation d’un site, vous pouvez déplacer certains rôles de système de site depuis leur emplacement par défaut sur le serveur de site vers un autre serveur. Cela vaut notamment pour le point de gestion ou le point de distribution, qui sont installés par défaut sur un serveur de site principal ou secondaire. Vous pouvez également installer des instances supplémentaires de certains rôles de système de site pour étendre les capacités de votre site (fournir davantage de services aux clients) et répondre aux besoins de votre entreprise. Certains rôles sont obligatoires, tandis que d’autres sont facultatifs.  

-   **Serveur de site Configuration Manager**. Ce rôle identifie le serveur sur lequel le programme d’installation de Configuration Manager est exécuté pour installer un site, ou le serveur sur lequel vous installez un site secondaire. Ce rôle ne peut pas être déplacé ni désinstallé tant que le site n’a pas été désinstallé.  

-   **Système de site Configuration Manager**. Ce rôle est attribué à tout ordinateur sur lequel vous installez un site ou un rôle de système de site. Ce rôle ne peut pas être déplacé ni désinstallé tant que le dernier rôle de système de site n’a pas été supprimé de l’ordinateur.  

-   **Rôle de système de site de composant Configuration Manager**. Ce rôle identifie un système de site exécutant une instance du service SMS Executive. Il est obligatoire pour prendre en charge d’autres rôles, comme des points de gestion. Ce rôle ne peut pas être déplacé ni désinstallé tant que le dernier rôle de système de site applicable n’a pas été supprimé de l’ordinateur.  

-   **Serveur de base de données de site Configuration Manager**. Ce rôle est attribué aux serveurs de système de site qui contiennent une instance de la base de données d’un site. Il ne peut être déplacé vers un nouveau serveur qu’en modifiant le site pour qu’il héberge la base de données du site sur un autre serveur SQL Server.  

-   **Fournisseur SMS**. Ce rôle est attribué à chaque ordinateur qui héberge une instance du fournisseur SMS (l’interface entre une console Configuration Manager et la base de données du site). Par défaut, ce rôle est installé automatiquement sur le serveur d’un site d’administration centrale et les sites principaux. Vous pouvez installer des instances supplémentaires sur chaque site pour fournir un accès à d’autres utilisateurs administratifs.  

     Pour installer des fournisseurs SMS supplémentaires, exécutez le programme d’installation de Configuration Manager afin de [gérer le fournisseur SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider). Ensuite, installez d’autres fournisseurs sur d’autres ordinateurs. Vous ne pouvez installer qu’une seule instance du fournisseur SMS sur un ordinateur, et celui-ci doit être dans le même domaine que le serveur de site.  

-   **Point de service web du catalogue des applications**. Un rôle de système de site qui fournit des informations logicielles au site Web du catalogue d'applications à partir de la bibliothèque de logiciels. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

-   **Point du site web du catalogue des applications**. Un rôle de système de site qui fournit aux utilisateurs une liste des logiciels disponibles à partir du catalogue d'applications. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

     Si le catalogue d’applications prend en charge des ordinateurs clients sur Internet, il est plus sûr d’installer le point de site Web du catalogue des applications dans un réseau de périmètre et le point de service web du catalogue des applications sur l’intranet.  

-   **Point de synchronisation Asset Intelligence**. Ce rôle de système de site se connecte à Microsoft afin de télécharger des informations pour le catalogue Asset Intelligence. Il charge également les titres sans catégorie, en vue de leur éventuelle future intégration dans le catalogue. Une hiérarchie ne prend en charge qu’une seule instance de ce rôle, qui doit se trouver sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome). Si vous étendez un site principal autonome à une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal, puis l’installer sur le site d’administration centrale.   Pour plus d’informations, consultez [Asset Intelligence dans System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Point d’enregistrement de certificat**. Ce rôle de système de site communique avec un serveur qui exécute le Service d’inscription de périphériques réseau. Il gère les demandes de certificat de périphérique qui utilisent le protocole SCEP (Simple Certificate Enrollment Protocol). Ce rôle est pris en charge uniquement sur des sites principaux et le site d’administration centrale.

     Bien qu’un point d’enregistrement de certificat puisse fournir une fonctionnalité à une hiérarchie entière, vous pouvez installer plusieurs instances de ce rôle sur un site et sur plusieurs sites dans la même hiérarchie. Cela facilite l’équilibrage de charge. Quand plusieurs instances existent dans une hiérarchie, des clients sont affectés de façon aléatoire à l’un des points d’enregistrement de certificat.  

     Chaque point d'enregistrement de certificat requiert l'accès à une instance distincte d'un service d'inscription d'appareils réseau. Vous ne pouvez pas configurer plusieurs points d'enregistrement de certificat pour utiliser le même service d'inscription d'appareils réseau. En outre, le point d’enregistrement de certificat ne doit pas être installé sur le serveur exécutant le service d’inscription de périphérique réseau.  

- **Point de connecteur de passerelle de gestion cloud**. Ce rôle de système de site communique avec la [passerelle de gestion cloud](/sccm/core/clients/manage/setup-cloud-management-gateway).

-   **Point de distribution**. Un rôle de système de site qui contient des fichiers sources que les clients peuvent télécharger, notamment le contenu de l'application, les packages logiciels, les mises à jour logicielles, les images du système d'exploitation et les images de démarrage. Par défaut, ce rôle est installé sur l’ordinateur du serveur de site de nouveaux sites principaux et secondaires lors de l’installation du site. Ce rôle n’est pas pris en charge sur un site d’administration centrale. Vous pouvez installer plusieurs instances de ce rôle sur un site pris en charge et sur plusieurs sites dans la même hiérarchie. Pour plus d’informations, consultez [Concepts fondamentaux de la gestion de contenu dans System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) et [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   **Point d’état de secours**. Ce rôle de système de site vous aide à surveiller l’installation des clients et à identifier ceux qui ne sont pas pris en charge, car ils ne peuvent pas communiquer avec leur point de gestion. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site et sur plusieurs sites dans la même hiérarchie.     


-   **Point Endpoint Protection.** Configuration Manager utilise ce rôle de système de site pour accepter le contrat de licence Endpoint Protection et configurer l’appartenance par défaut à Microsoft Active Protection Service. Une hiérarchie ne prend en charge qu’une seule instance de ce rôle, qui doit se trouver sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome). Si vous étendez un site principal autonome à une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal, puis l’installer sur le site d’administration centrale. Pour plus d’informations, consultez [Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md).  

-   **Point d’inscription.** Ce rôle de système de site utilise des certificats PKI pour permettre à Configuration Manager d’inscrire des appareils mobiles et des ordinateurs Mac. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

     Si un utilisateur inscrit des appareils mobiles à l’aide de Configuration Manager et que son compte Active Directory se trouve dans une forêt non approuvée par la forêt du serveur de site, vous devez installer un point d’inscription dans la forêt de l’utilisateur. L’utilisateur peut alors être authentifié.  

-   **Point proxy d’inscription**. Rôle de système de site qui gère les demandes d'inscription Configuration Manager issues des appareils mobiles et des ordinateurs Mac. Bien que ce rôle soit pris en charge uniquement sur des sites principaux, vous pouvez en installer plusieurs instances sur un site ou sur plusieurs sites dans la même hiérarchie.  

     Lors de la prise en charge d’appareils mobiles sur Internet, installez le point proxy d’inscription dans un réseau de périmètre et le point d’inscription sur l’intranet.  

-   **Connecteur Exchange Server**. Pour plus d’informations sur ce rôle, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   **Point de gestion**. Ce rôle de système de site fournit aux clients des informations sur l’emplacement du service et de la stratégie, et reçoit les données de configuration de la part des clients.  

    Par défaut, ce rôle est installé sur l’ordinateur du serveur de site de nouveaux sites principaux et secondaires lors de l’installation du site. Les sites principaux prennent en charge plusieurs instances de ce rôle. Les sites secondaires prennent en charge un seul point de gestion comme point de contact local permettant aux clients d’obtenir des stratégies d’ordinateur et d’utilisateur. (Sur un site secondaire, un point de gestion est appelé point de gestion proxy.)  

     Vous pouvez configurer des points de gestion pour prendre en charge le protocole HTTP ou HTTPS, ainsi que les appareils mobiles que vous gérez via la fonctionnalité de gestion des appareils mobiles locale de System Center Configuration Manager. Vous pouvez utiliser des [réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) pour réduire la charge processeur placée sur le serveur de base de données du site par les points de gestion à mesure qu’ils traitent les demandes des clients.  

-   **Point de Reporting Services**. Rôle de système de site qui est intégré à SQL Server Reporting Services pour créer et gérer des rapports pour Configuration Manager. Ce rôle est pris en charge sur les sites principaux et le site d’administration centrale, et vous pouvez en installer plusieurs instances sur un site pris en charge. Pour plus d’informations, consultez [Planification de la création de rapports dans System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md).  

-   **Point de connexion de service**. Ce rôle de système de site permet de gérer les appareils mobiles avec Microsoft Intune et d’assurer la gestion MDM locale. Il charge aussi les données d’utilisation à partir de votre site et est nécessaire pour mettre les mises à jour de Configuration Manager disponibles dans la console Configuration Manager. Une hiérarchie ne prend en charge qu’une seule instance de ce rôle, qui doit se trouver sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome). Si vous étendez un site principal autonome à une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal, puis l’installer sur le site d’administration centrale. Pour plus d’informations, voir [À propos du point de connexion de service dans System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   **Point de mise à jour logicielle**. Un rôle de système de site qui est intégré à Windows Server Update Services (WSUS) pour fournir des mises à jour logicielles aux clients Configuration Manager. Ce rôle est pris en charge sur tous les sites :  

    -   Installez ce système de site sur le site d’administration centrale pour une synchronisation avec WSUS.  

    -   Configurez chaque instance de ce rôle sur les sites principaux enfants à synchroniser avec le site d’administration centrale.  

    -   Envisagez d’installer un point de mise à jour logicielle sur des sites secondaires quand le transfert de données sur le réseau est lent.  

    Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

-   **Point de migration d’état**. Un rôle de système de site qui stocke les données d'état utilisateur lorsqu'un ordinateur est migré vers un nouveau système d'exploitation. Ce rôle est pris en charge sur les sites principaux et les sites secondaires. Vous pouvez installer plusieurs instances de ce rôle sur un site et sur plusieurs sites dans la même hiérarchie. Pour plus d’informations sur le stockage de l’état utilisateur quand vous déployez un système d’exploitation, consultez [Gérer l’état utilisateur dans System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   **Point du programme de validation d’intégrité système**. Ce rôle de système de site est toujours visible dans la console Configuration Manager, mais il n’est plus utilisé.  

###  <a name="bkmk_proxy"></a> Rôles système de site pouvant utiliser un serveur proxy  
 Certains rôles de système de site Configuration Manager requièrent des connexions à Internet et utilisent un serveur proxy quand le serveur de système de site hébergeant le rôle est configuré pour cela. En règle générale, cette connexion est établie dans le **système** de l’ordinateur sur lequel le rôle de système de site est installé. La connexion ne peut pas utiliser une configuration proxy pour les comptes d’utilisateurs standard. Quand un serveur proxy est requis pour établir une connexion à Internet, vous devez configurer l’ordinateur pour qu’il utilise un serveur proxy :  

-   Vous pouvez configurer un serveur proxy lors de l’installation d’un rôle de système de site.  

-   Vous pouvez ajouter ou modifier une configuration de serveur proxy quand vous utilisez la console Configuration Manager.  

-   Tous les rôles de système de site sur un serveur de système de site qui peuvent utiliser une configuration de serveur proxy adoptent la même configuration. S'il est nécessaire que différents rôles de système de site utilisent différents serveurs proxy, vous devez installer les rôles de système de site sur différents ordinateurs de serveur de système de site.  

-   Si vous modifiez la configuration du serveur proxy, ou installez un nouveau rôle système de site sur un ordinateur ayant déjà une configuration du serveur proxy, la configuration d’origine est remplacée par la nouvelle.  


Pour connaître les procédures de configuration du serveur proxy pour des rôles de système de site, consultez la rubrique [Ajouter des rôles de système de site pour System Center Configuration Manager](../../../core/servers/deploy/configure/add-site-system-roles.md).  

Les rôles système de site pouvant utiliser un serveur proxy sont les suivants :  

-   **Point de synchronisation Asset Intelligence**. Ce rôle de système de site se connecte à Microsoft et utilise une configuration de serveur proxy sur l’ordinateur hébergeant le point de synchronisation Asset Intelligence.  

-   **Point de distribution cloud**. Lorsque vous utilisez un point de distribution cloud, le site principal qui gère ce point doit pouvoir se connecter à Microsoft Azure pour configurer, surveiller et distribuer un contenu au point de distribution. Si un serveur proxy est requis pour cette connexion, vous devez configurer le serveur proxy sur le serveur de site principal. Vous ne pouvez pas configurer un serveur proxy sur le point de distribution cloud dans Azure. Pour plus d’informations, consultez la section [Configurer les paramètres de proxy pour des sites principaux gérant des services cloud](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md#BKMK_ConfigProxyforCloud) dans la rubrique [Installer des points de distribution cloud dans Microsoft Azure pour System Center Configuration Manager](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).  

-   **Connecteur Exchange Server**. Ce rôle de système de site se connecte à un serveur Exchange Server et utilise une configuration de serveur proxy sur l’ordinateur qui héberge le connecteur Exchange Server.  

-   **Point de mise à jour logicielle**. Ce rôle de système de site peut nécessiter des connexions à Microsoft Update pour télécharger des correctifs et synchroniser les informations sur les mises à jour. En règle générale, lorsque vous configurez le serveur proxy, chaque rôle de système de site sur l’ordinateur qui prend en charge l’utilisation du serveur proxy utilise le serveur proxy. Aucune configuration manuelle n'est requise. Le point de mise à jour logicielle est une exception à cette règle. Par défaut, un point de mise à jour logicielle n’utilise pas de serveur proxy disponible, sauf si vous activez également les options suivantes lors de la configuration du point de mise à jour logicielle :  

    -   **Utiliser un serveur proxy lors de la synchronisation des mises à jour logicielles**  

    -   **Utiliser un serveur proxy lors du téléchargement du contenu avec des règles de déploiement automatiques**  

    > [!TIP]  
    >  Pour pouvoir sélectionner l’une ou l’autre option, vous devez configurer un serveur proxy sur le serveur de système de site qui héberge le point de mise à jour logicielle. Le serveur proxy est utilisé uniquement pour les options spécifiques que vous sélectionnez.  

 Pour plus d’informations sur les serveurs proxy associés aux points de mise à jour logicielle, consultez la section Paramètres du serveur proxy dans la rubrique [Installer et configurer un point de mise à jour logicielle](../../../sum/get-started/install-a-software-update-point.md).  

-   **Point de connexion de service**. Lorsque ce rôle de système de site est configuré pour être en ligne (et non hors connexion), il se connecte à Microsoft Intune et au service cloud Microsoft.  
