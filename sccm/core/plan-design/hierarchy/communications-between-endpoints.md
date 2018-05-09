---
title: Communications entre points de terminaison
titleSuffix: Configuration Manager
description: Découvrez comment les systèmes de site et les composants System Center Configuration Manager communiquent sur un réseau.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 603adb982f704c462e043d8c0974fc85a0748863
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>Communications entre points de terminaison dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


##  <a name="Planning_Intra-site_Com"></a> Communications entre les systèmes d’un site  
 Quand des systèmes de site ou des composants Configuration Manager communiquent sur le réseau avec d’autres systèmes de site ou d’autres composants Configuration Manager du site, ils utilisent l’un des protocoles suivants, selon la configuration du site :  

-   SMB (Server Message Block)  

-   HTTP  

-   HTTPS  

À l’exception de la communication depuis le serveur de site vers un point de distribution, ces communications de serveur à serveur dans un site peuvent avoir lieu à tout moment et n’utilisent aucun mécanisme de contrôle de la bande passante réseau. Comme vous ne pouvez pas contrôler la communication entre systèmes de site, vérifiez que vous installez des serveurs de système de site à des emplacements dotés de réseaux rapides et bien connectés.  

Pour gérer plus facilement le transfert de contenu depuis le serveur de site vers des points de distribution :  

-   Configurez le point de distribution pour la planification et le contrôle de la bande passante réseau. Ces contrôles ressemblent aux configurations utilisées par les adresses intersites et vous pouvez souvent utiliser cette configuration au lieu d’installer un autre site Configuration Manager quand le transfert de contenu vers des emplacements réseau distants est votre préoccupation principale en ce qui concerne la bande passante.  

-   Vous pouvez installer un point de distribution comme un point de distribution préparé. Un point de distribution préparé vous permet d'utiliser du contenu qui est placé manuellement sur le serveur de point de distribution et supprime la nécessité de transférer des fichiers de contenu sur le réseau.  

Pour plus d’informations, consultez [Gérer la bande passante réseau pour la gestion de contenu](manage-network-bandwidth.md).


##  <a name="Planning_Client_to_Site_System"></a> Communications depuis les clients vers les systèmes de site et les services  
Les clients lancent des communications vers les rôles de système de site, les services de domaine Active Directory et les services en ligne. Pour activer ces communications, les pare-feu doivent autoriser le trafic réseau entre les clients et le point de terminaison de leurs communications. Les points de terminaison sont les suivants :  

-   **Point du site web du catalogue des applications** : Prend en charge les communications HTTP et HTTPS

-   **Ressources cloud** : Inclut Microsoft Azure et Microsoft Intune  

-   **Module de stratégie de Configuration Manager (NDES)**  : Prend en charge les communications HTTP et HTTPS

-   **Points de distribution** : Prennent en charge les communications HTTP et HTTPS. HTTPS est obligatoire pour les points de distribution cloud  

-   **Point d’état de secours** : Prend en charge les communications HTTP  

-   **Point de gestion** : Prend en charge les communications HTTP et HTTPS  

-   **Microsoft Update**  

-   **Points de mise à jour logicielle** : Prennent en charge les communications HTTP et HTTPS  

-   **Points de migration d’état** : Prennent en charge les communications HTTP et HTTPS  

-   **Divers services de domaine**  

Avant qu’un client puisse communiquer avec un rôle de système de site, le client utilise l’emplacement du service pour rechercher un rôle de système de site prenant en charge son protocole (HTTP ou HTTPS). Par défaut, les clients utilisent la méthode la plus sûre à leur disposition :  

-   Pour utiliser le protocole HTTPS, vous devez disposer d'une infrastructure à clé publique (PKI) et installer des certificats PKI sur des clients et serveurs. Pour plus d’informations sur la façon d’utiliser des certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

-   Quand vous déployez un rôle de système de site qui utilise Internet Information Services (IIS) et prend en charge les communications des clients, vous devez spécifier si les clients se connectent au système de site à l'aide de HTTP ou HTTPS. Si vous utilisez le protocole HTTP, vous devez également envisager les options de signature et de chiffrement. Pour plus d’informations, consultez [Planification de la signature et du chiffrement](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) dans [Planifier la sécurité dans System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

Pour plus d’informations sur l’emplacement de service par les clients, consultez  [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

Pour plus d’informations sur les ports et protocoles utilisés par les clients pour communiquer avec ces points de terminaison, consultez [Ports utilisés dans System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée  
Les rôles de système de site suivants installés sur les sites principaux prennent en charge les connexions de clients qui se trouvent dans des emplacements non approuvés, comme Internet ou une forêt non approuvée. (Les sites secondaires ne prennent pas en charge les connexions du client à partir d’emplacements non approuvés) :  

-   Point du site web du catalogue des applications  

-   Module de stratégie de Configuration Manager  

-   Point de distribution (HTTPS est requis par les points de distribution cloud)  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion  

-   Point de mise à jour logicielle  

**À propos des systèmes de site accessibles sur Internet :**   
Vous n’avez pas besoin d’une relation d’approbation entre la forêt d’un client et celle du serveur de système de site. Toutefois, quand la forêt qui contient un système de site accessible sur Internet approuve la forêt qui contient les comptes d’utilisateurs, cette configuration prend en charge les stratégies utilisateur pour les appareils sur Internet quand vous activez le paramètre client **Autoriser les demandes de stratégie utilisateur depuis des clients Internet** de la **Stratégie client**.  

Par exemple, les configurations suivantes illustrent la prise en charge par la gestion des clients basés sur Internet des stratégies utilisateur pour les appareils situés sur Internet :  

-   Le point de gestion basé sur Internet est le réseau de périmètre sur lequel réside un contrôleur de domaine en lecture seule pour authentifier l'utilisateur et un pare-feu qui intervient autorise les paquets Active Directory.  

-   Le compte d'utilisateur se trouve dans la forêt A (Intranet) et le point de gestion basé sur Internet dans la forêt B (le réseau de périmètre). La forêt B approuve la forêt A et un pare-feu qui intervient autorise les paquets d'authentification.  

-   Le compte d'utilisateur et le point de gestion basé sur Internet sont dans la forêt A (Intranet). Le point de gestion est publié sur Internet à l'aide d'un serveur proxy web (comme Forefront Threat Management Gateway).  

> [!NOTE]  
>  Si l'authentification Kerberos échoue, l'authentification NTLM est ensuite automatiquement utilisée.  

Comme l'indique l'exemple précédent, vous pouvez placer des systèmes de site basés sur Internet dans l'Intranet lorsqu'ils sont publiés sur Internet à l'aide d'un serveur proxy Web, tel que ISA Server et Forefront Threat Management Gateway. Ces systèmes de site peuvent être configurés pour la connexion du client à partir d’Internet uniquement, ou pour les connexions du client à partir d’Internet et d’un intranet. Quand vous utilisez un serveur proxy web, vous pouvez le configurer pour le pontage SSL (Secure Sockets Layer) vers SSL (plus sécurisé) ou le tunnel SSL, comme suit :  

-   **Pontage SSL vers SSL :**   
    La configuration recommandée quand vous utilisez des serveurs web proxy pour la gestion de clients sur Internet est le pontage SSL vers SSL, qui utilise une terminaison SSL avec authentification. Les ordinateurs clients doivent être authentifiés à l'aide de l'authentification de l'ordinateur et les clients hérités de l'appareil mobile sont authentifiés à l'aide de l'authentification utilisateur. Les appareils mobiles inscrits par Configuration Manager ne prennent pas en charge le pontage SSL.  

     La terminaison SSL au niveau du serveur Web proxy présente l'avantage que les paquets provenant d'Internet sont inspectés avant d'être transférés au réseau interne. Le serveur Web proxy authentifie la connexion du client, l'arrête, puis ouvre une nouvelle connexion authentifiée vers les systèmes de site basés sur Internet. Quand les clients Configuration Manager utilisent un serveur web proxy, leur identité (GUID client) est contenue en toute sécurité dans la charge utile du paquet pour éviter que le point de gestion prenne le serveur web proxy pour le client. Le pontage n’est pas pris en charge dans Configuration Manager de HTTP vers HTTPS ou de HTTPS vers HTTP.  

-   **Tunneling** :   
    Si votre serveur web proxy ne peut pas prendre en charge la configuration requise pour le pontage SSL, ou si vous souhaitez configurer la prise en charge Internet pour les appareils mobiles inscrits par Configuration Manager, le tunneling SSL est aussi pris en charge. Il s'agit d'une option moins sûre car les paquets SSL d'Internet sont transférés aux systèmes de site sans terminaison SSL et ne peuvent donc pas être inspectés à la recherche de contenu malveillant. Lors de l'utilisation du tunnel SSL, aucune configuration n'est requise pour les certificats pour le serveur Web proxy.  

##  <a name="Plan_Com_X-Forest"></a> Communications dans les forêts Active Directory  
System Center Configuration Manager prend en charge des sites et des hiérarchies qui recouvrent des forêts Active Directory.  

Configuration Manager prend également en charge les ordinateurs de domaine qui ne se trouvent pas dans la même forêt Active Directory que le serveur de site, et les ordinateurs qui se trouvent dans des groupes de travail :  

-   **Pour prendre en charge des ordinateurs de domaine situés dans une forêt qui n’est pas approuvée par la forêt de votre serveur de site**, vous pouvez procéder comme suit :  

    -   Installez des rôles de système de site dans cette forêt non approuvée, en activant l’option de publication des informations de site dans cette forêt Active Directory.  

    -   Gérez ces ordinateurs comme des ordinateurs de groupe de travail.  

  Quand vous installez des serveurs de système de site dans une forêt Active Directory non approuvée, les communications des clients de cette forêt vers le serveur restent internes à cette forêt, ce qui permet à Configuration Manager d’authentifier l’ordinateur avec Kerberos. Quand vous publiez des informations de site dans la forêt du client, le client peut récupérer les informations de site, notamment la liste des points de gestion disponibles, à partir de sa forêt Active Directory, au lieu de télécharger ces informations à partir de son point de gestion attribué.  

  > [!NOTE]  
  >  Pour gérer les appareils qui se trouvent sur Internet, vous pouvez installer des rôles système de site de type Internet dans votre réseau de périmètre lorsque des serveurs de système de site se trouvent dans une forêt Active Directory. Ce scénario ne nécessite pas d’approbation bidirectionnelle entre le réseau de périmètre et la forêt du serveur de site.  

-   **Pour prendre en charge des ordinateurs situés dans un groupe de travail**, vous devez effectuer les opérations suivantes :  

    -   Approuvez manuellement les ordinateurs du groupe de travail qui utilisent des connexions client HTTP pour accéder aux rôles de système de site. En effet, Configuration Manager ne peut pas authentifier ces ordinateurs avec Kerberos.  

    -   Configurez les clients du groupe de travail avec le compte d’accès réseau pour permettre à ces ordinateurs de récupérer le contenu à partir des points de distribution.  

    -   Fournir aux clients du groupe de travail une méthode de remplacement pour rechercher les points de gestion. Vous pouvez utiliser la publication DNS, WINS, ou attribuer directement un point de gestion. Cela est dû au fait que ces clients ne peuvent pas récupérer les informations de site à partir des services de domaine Active Directory.  

    Ressources connexes dans cette bibliothèque de contenu :  

    -   [Gérer les conflits d’enregistrement pour les clients Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Compte d’accès au réseau](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [Installer des clients Configuration Manager sur des ordinateurs de groupe de travail](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Scénarios de prise en charge d’un site ou d’une hiérarchie qui s’étend sur plusieurs domaines et forêts  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Communication entre les sites d’une hiérarchie qui s’étend sur des forêts  
Ce scénario nécessite une approbation de forêt bidirectionnelle prenant en charge l’authentification Kerberos.  Si vous n’avez pas d’approbation de forêt bidirectionnelle prenant en charge l’authentification Kerberos, Configuration Manager ne prend pas en charge de site enfant dans la forêt distante.  

 **Configuration Manager prend en charge l’installation d’un site enfant dans une forêt distante qui possède l’approbation bidirectionnelle requise avec la forêt du site parent.**  

-   Par exemple, vous pouvez placer un site secondaire dans une autre forêt de son site parent principal tant que l’approbation nécessaire existe.  

> [!NOTE]  
>  Un site enfant peut être un site principal (où le site d’administration centrale est le site parent) ou un site secondaire.  

Les communications intersite dans Configuration Manager utilisent la réplication de base de données et les transferts basés sur des fichiers. Quand vous installez un site, vous devez spécifier un compte à utiliser pour installer le site sur le serveur indiqué. Ce compte établit et conserve également la communication entre les sites.  

Une fois que le site a installé et lancé avec succès les transferts basés sur des fichiers et la réplication de base de données, il est inutile de configurer autre chose pour la communication vers le site.  

**Lorsqu’une approbation de forêt bidirectionnelle existe, Configuration Manager ne nécessite aucune étape de configuration supplémentaire.**  

Par défaut, lorsque vous installez un nouveau site en tant qu’enfant d’un autre site, Configuration Manager configure les éléments suivants :  

-   Un itinéraire de réplication de fichiers intersite sur chaque site qui utilise le compte d’ordinateur du serveur de site. Configuration Manager ajoute le compte d’ordinateur de chaque ordinateur au groupe **SMS_SiteToSiteConnection_&lt;code_site\>** sur l’ordinateur de destination.  

-   Réplication de base de données entre les serveurs SQL Server sur chaque site.  

Les configurations suivantes doivent également être définies :  

-   Les appareils réseau et les pare-feu qui interviennent doivent autoriser les paquets réseau requis par Configuration Manager.  

-   La résolution de noms doit fonctionner entre les forêts.  

-   Pour installer un site ou un rôle de système de site, vous devez spécifier un compte qui dispose des autorisations d'administrateur local sur l'ordinateur spécifié.  

#### <a name="communication-in-a-site-that-spans-forests"></a>Communication dans un site qui s’étend sur des forêts  
Ce scénario ne nécessite aucune approbation de forêt bidirectionnelle.  

**Les sites principaux prennent en charge l’installation de rôles de système de site sur les ordinateurs des forêts distantes**.  

-   Le point de service web du catalogue des applications est la seule exception.  Il est uniquement pris en charge dans la même forêt que le serveur de site.  

-   Si le rôle de système de site accepte les connexions depuis Internet, comme bonne pratique de sécurité, installez ces rôles de système de site dans un emplacement où la limite de forêt fournit une protection pour le serveur de site (par exemple, dans un réseau de périmètre).  

**Pour installer un rôle de système de site sur un ordinateur situé dans une forêt non approuvée :**  

-   Vous devez spécifier un **Compte d’installation du système de site**, utilisé pour installer le rôle de système de site. (Ce compte doit disposer d’informations d’identification administratives locales pour la connexion.) Ensuite, installez les rôles de système de site sur l’ordinateur spécifié.  

-   Vous devez sélectionner l'option de système de site **Exiger que le serveur de site établisse des connexions vers ce système de site**. Pour cela, le serveur de site doit établir des connexions au serveur de système de site pour transférer des données. De cette manière, l’ordinateur qui se trouve dans l’emplacement non approuvé ne peut pas établir de contact avec le serveur de site au sein de votre réseau approuvé. Ces connexions utilisent le **Compte d'installation du système de site**.  

**Pour utiliser un rôle de système de site installé dans une forêt non approuvée,** les pare-feu doivent autoriser le trafic réseau, même quand le serveur de site lance le transfert de données.  

Par ailleurs, les rôles de système de site suivants requièrent un accès direct à la base de données de site. Par conséquent, les pare-feu doivent autoriser le trafic applicable de la forêt non approuvée vers les sites SQL Server :  

-   Point de synchronisation Asset Intelligence  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point de gestion  

-   Point du service de rapport  

-   Point de migration d’état  

Pour plus d’informations, consultez [Ports utilisés dans System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

**Vous serez peut-être amené à configurer l’accès des rôles système de site à la base de données du site :**  

Les rôles de système de site de point d’inscription et de point de gestion se connectent à la base de données de site.  

-   Par défaut, quand ces rôles de système de site sont installés, Configuration Manager configure le compte d’ordinateur du nouveau serveur de système de site comme compte de connexion pour le rôle de système de site et ajoute le compte au rôle de base de données SQL Server approprié.  

-   Lorsque vous installez ces rôles de système de site dans un domaine non approuvé, vous devez configurer le compte de connexion du rôle de système de site pour autoriser le rôle de système de site à obtenir des informations à partir de la base de données.  

Si vous configurez un compte d’utilisateur de domaine comme compte de connexion pour ces rôles de système de site, assurez-vous que le compte d’utilisateur de domaine dispose des accès appropriés à la base de données SQL Server sur ce site :  

-   Point de gestion : **compte de connexion à la base de données du point de gestion**.  

-   Point d'inscription : **compte de connexion du point d'inscription**.  

Lorsque vous planifiez des rôles de système de site dans d'autres forêts, tenez compte des informations supplémentaires suivantes :  

-   Si vous exécutez un pare-feu Windows, configurez les profils de pare-feu applicables pour transmettre les communications entre le serveur de base de données du site et les ordinateurs qui sont installés avec des rôles de système de site distants. Pour plus d’informations sur les profils de pare-feu, consultez [Présentation des profils de Pare-feu](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   Lorsque le point de gestion basé sur Internet approuve la forêt contenant les comptes d'utilisateur, les stratégies utilisateur sont prises en charge. Lorsqu'il n'existe aucune relation d'approbation, seules les stratégies d'ordinateur sont prises en charge.  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>Communication entre les clients et les rôles de système de site quand les clients ne se trouvent pas dans la même forêt Active Directory que leur serveur de site  
Configuration Manager prend en charge les scénarios suivants pour les clients qui ne se trouvent pas dans la même forêt que le serveur de site de leur site :  

-   Il existe une relation d’approbation de forêt bidirectionnelle entre la forêt du client et celle du serveur du site.  

-   Le serveur de rôle de système de site se trouve dans la même forêt que le client.  

-   Le client se trouve sur un ordinateur de domaine sans approbation de forêt bidirectionnelle avec le serveur de site, et les rôles de système de site ne sont pas installés dans la forêt du client.  

-   Le client se trouve sur un ordinateur de groupe de travail.  

Les clients se trouvant sur un ordinateur joint à un domaine peuvent utiliser les services de domaine Active Directory pour l’emplacement du service si leur site est publié dans leur forêt Active Directory.  

Pour publier des informations de site dans une autre forêt Active Directory, vous devez effectuer les opérations suivantes :  

-   Spécifiez la forêt et activez la publication dans cette forêt dans le nœud **Forêts Active Directory** de l’espace de travail **Administration** .  

-   Configurez chaque site pour publier ses données dans les services de domaine Active Directory. Cette configuration permet aux clients se trouvant dans cette forêt d'extraire des informations de site et de trouver des points de gestion. Pour un client qui ne peut pas utiliser les services de domaine Active Directory pour l’emplacement du service, vous pouvez utiliser DNS, WINS ou le point de gestion attribué du client.  

###  <a name="bkmk_xchange"></a> Placer le connecteur du serveur Exchange Server dans une forêt distante  
Pour prendre en charge ce scénario, assurez-vous que la résolution de noms fonctionne entre les forêts (par exemple, via une configuration DNS supplémentaire) et spécifiez le nom de domaine complet (FQDN) intranet du serveur Exchange Server au moment où vous configurez le connecteur du serveur Exchange Server. Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  
