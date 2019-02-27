---
title: Communications entre points de terminaison
titleSuffix: Configuration Manager
description: Découvrez comment les systèmes de site et les composants Configuration Manager communiquent sur un réseau.
ms.date: 10/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ebe37bb97c4a1e231bfaf94f420f7f0471f30f6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141957"
---
# <a name="communications-between-endpoints-in-configuration-manager"></a>Communications entre points de terminaison dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article explique la façon dont les clients et les systèmes de site Configuration Manager communiquent sur votre réseau. Il comprend les sections suivantes :  

- [Communications entre les systèmes d’un site](#Planning_Intra-site_Com)  
    - [Serveur de site vers un point de distribution](#bkmk_site2dp)  

- [Communications depuis les clients vers les systèmes de site et les services](#Planning_Client_to_Site_System)  
    - [Communication du client vers un point de gestion](#bkmk_client2mp)  
    - [Communication du client vers un point de distribution](#bkmk_client2dp)  
    - [Éléments à prendre en considération pour les communications clientes à partir d’Internet ou d’une forêt non approuvée](#BKMK_clientspan)  
    - [Informations sur les systèmes de site accessibles sur Internet](#bkmk_internetfacing)  

- [Communications dans les forêts Active Directory](#Plan_Com_X-Forest)  
    - [Prendre en charge des ordinateurs de domaine situés dans une forêt qui n’est pas approuvée par la forêt de votre serveur de site](#bkmk_noforesttrust)  
    - [Prendre en charge des ordinateurs situés dans un groupe de travail](#bkmk_workgroup)  
    - [Scénarios de prise en charge d’un site ou d’une hiérarchie qui s’étend sur plusieurs domaines et forêts](#bkmk_span)  



##  <a name="Planning_Intra-site_Com"></a> Communications entre les systèmes d’un site  

 Quand des systèmes de site ou des composants Configuration Manager communiquent sur le réseau avec d’autres systèmes de site ou d’autres composants du site, ils utilisent l’un des protocoles suivants, selon la configuration du site :  

-   SMB (Server Message Block)  

-   HTTP  

-   HTTPS  

À l’exception de la communication depuis le serveur de site vers un point de distribution, les communications de serveur à serveur dans un site peuvent avoir lieu à tout moment. Ces communications n’utilisent aucun mécanisme de contrôle de la bande passante réseau. Comme vous ne pouvez pas contrôler la communication entre les systèmes de site, assurez-vous d’installer les serveurs de système de site à des emplacements connectés à des réseaux rapides et fiables.  


### <a name="bkmk_site2dp"></a> Serveur de site vers un point de distribution 

Pour gérer plus facilement le transfert de contenu depuis le serveur de site vers des points de distribution, utilisez les stratégies suivantes :  

-   Configurez le point de distribution pour la planification et le contrôle de la bande passante réseau. Ces contrôles ressemblent aux configurations utilisées par des adresses intersites. Utilisez cette configuration au lieu d’installer un autre site Configuration Manager si le transfert de contenu vers des emplacements réseau distincts est votre principale considération en matière de bande passante.  

-   Vous pouvez installer un point de distribution comme un point de distribution préparé. Un point de distribution préparé vous permet d'utiliser du contenu qui est placé manuellement sur le serveur de point de distribution et supprime la nécessité de transférer des fichiers de contenu sur le réseau.  

Pour plus d’informations, consultez [Gérer la bande passante réseau pour la gestion de contenu](manage-network-bandwidth.md).



##  <a name="Planning_Client_to_Site_System"></a> Communications depuis les clients vers les systèmes de site et les services  

Les clients lancent des communications vers les rôles de système de site, les services de domaine Active Directory et les services en ligne. Pour activer ces communications, les pare-feu doivent autoriser le trafic réseau entre les clients et le point de terminaison de leurs communications. Pour plus d’informations sur les ports et protocoles utilisés par les clients pour communiquer avec ces points de terminaison, consultez [Ports utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/ports).  

Avant qu’un client puisse communiquer avec un rôle de système de site, le client utilise l’emplacement du service pour rechercher un rôle prenant en charge son protocole (HTTP ou HTTPS). Par défaut, les clients utilisent la méthode la plus sûre à leur disposition. Pour plus d’informations, consultez [Comprendre comment les clients recherchent des services et des ressources de site](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  

Pour utiliser le protocole HTTPS, configurez une des options suivantes :  

- Utilisez une infrastructure à clé publique (PKI) et installez des certificats PKI sur les clients et serveurs. Pour plus d’informations sur l’utilisation des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

- À compter de la version 1806, configurez le site avec l’option **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**. Pour plus d’informations, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).  

Quand vous déployez un rôle de système de site qui utilise Internet Information Services (IIS) et prend en charge les communications des clients, vous devez spécifier si les clients se connectent au système de site à l'aide de HTTP ou HTTPS. Si vous utilisez le protocole HTTP, vous devez également envisager les options de signature et de chiffrement. Pour plus d’informations, consultez [Planifier la signature et le chiffrement](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForSigningEncryption).  


### <a name="bkmk_client2mp"></a> Communication du client vers un point de gestion

Quand un client communique avec un point de gestion, il y a deux étapes : l’authentification (transport) et l’autorisation (message). Ce processus varie en fonction des facteurs suivants : 
- Configuration de site : HTTP, HTTPS ou HTTP amélioré
- Configuration des points de gestion : HTTPS uniquement, ou HTTP ou HTTPS autorisé
- L’identité de l’appareil dans les scénarios orientés appareil
- L’identité de l’utilisateur dans les scénarios orientés utilisateur

Le tableau suivant permet de mieux comprendre le déroulement de ce processus :  

| Type du point de gestion  | Authentification du client  | Autorisation du client<br>Identité de l’appareil  | Autorisation du client<br>Identité de l’utilisateur  |
|----------|---------|---------|---------|
| HTTP     | Authentification anonyme<br>Avec l’HTTP amélioré, le site vérifie le jeton *d’utilisateur* ou *d’appareil* Azure AD. | Demande de l’emplacement : Authentification anonyme<br>Package client : Authentification anonyme<br>anonyme, avec une des méthodes suivantes pour prouver l’identité de l’appareil :<br> - Anonyme (approbation manuelle)<br> - Authentification intégrée de Windows<br> - Jeton *d’appareil* Azure AD (HTTP amélioré)<br>Après l’inscription, le client utilise la signature des messages pour prouver l’identité de l’appareil | Dans les scénarios orientés utilisateur, utilisez une des méthodes suivantes pour prouver l’identité de l’utilisateur :<br> - Authentification intégrée de Windows<br> - Jeton *d’utilisateur* Azure AD (HTTP amélioré) |
| HTTPS    | Utilisation d’une des méthodes suivantes :<br> - Certificat PKI<br> - Authentification intégrée de Windows<br> - Jeton *d’utilisateur* ou *d’appareil* Azure AD | Demande d’emplacement : Authentification anonyme<br>Package client : Authentification anonyme<br>anonyme, avec une des méthodes suivantes pour prouver l’identité de l’appareil :<br> - Anonyme (approbation manuelle)<br> - Authentification intégrée de Windows<br> - Certificat PKI<br> - Jeton *d’utilisateur* ou *d’appareil* Azure AD<br>Après l’inscription, le client utilise la signature des messages pour prouver l’identité de l’appareil | Dans les scénarios orientés utilisateur, utilisez une des méthodes suivantes pour prouver l’identité de l’utilisateur :<br> - Authentification intégrée de Windows<br> - Jeton *d’utilisateur* Azure AD |

> [!Tip]  
> Pour plus d’informations sur la configuration du point de gestion selon le type d’identité d’appareil et avec la passerelle de gestion cloud, consultez [Activer le point de gestion pour HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_client2dp"></a> Communication du client vers un point de distribution

Quand un client communique avec un point de distribution, il a seulement besoin de s’authentifier avant de télécharger le contenu. Le tableau suivant permet de mieux comprendre le déroulement de ce processus :


| Type du point de distribution  | Authentification du client  |
|----------|---------|
| HTTP     | - Anonyme (si autorisée)<br>- Authentification intégrée de Windows avec un compte d’ordinateur ou un compte d’accès réseau<br> - Jeton d’accès au contenu (HTTP amélioré) |
| HTTPS    | - Certificat PKI<br> - Authentification intégrée de Windows avec un compte d’ordinateur ou un compte d’accès réseau<br> - Jeton d’accès au contenu |


###  <a name="BKMK_clientspan"></a> Éléments à prendre en considération pour les communications clientes à partir d’Internet ou d’une forêt non approuvée  

Les rôles de système de site suivants installés sur les sites principaux prennent en charge les connexions de clients qui se trouvent dans des emplacements non approuvés, comme Internet ou une forêt non approuvée. (Les sites secondaires ne prennent pas en charge les connexions de clients à partir d’emplacements non approuvés.) 

-   Point du site web du catalogue des applications  

-   Module de stratégie de Configuration Manager (NDES) 

-   Point de distribution   

-   Point de distribution cloud (nécessite HTTPS)

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion  

-   Point de mise à jour logicielle  

-   Passerelle de gestion cloud (nécessite HTTPS)


### <a name="bkmk_internetfacing"></a> Informations sur les systèmes de site accessibles sur Internet

> [!Note]  
> La section suivante concerne les scénarios de gestion de clients sur Internet. Elle ne s’applique pas aux scénarios utilisant une passerelle de gestion cloud. Pour plus d’informations, consultez [Gérer les clients sur Internet](/sccm/core/clients/manage/manage-clients-internet).  

Vous n’avez pas besoin d’une relation d’approbation entre la forêt d’un client et celle du serveur de système de site. Toutefois, quand la forêt qui contient un système de site accessible sur Internet approuve la forêt qui contient les comptes d’utilisateurs, cette configuration prend en charge les stratégies utilisateur pour les appareils sur Internet quand vous activez le paramètre client **Autoriser les demandes de stratégie utilisateur depuis des clients Internet** de la **Stratégie client**.  

Par exemple, les configurations suivantes illustrent la prise en charge par la gestion des clients basés sur Internet des stratégies utilisateur pour les appareils sur Internet :  

-   Le point de gestion Internet est le réseau de périmètre sur lequel réside un contrôleur de domaine en lecture seule pour authentifier l’utilisateur et un pare-feu qui autorise les paquets Active Directory.  

-   Le compte d’utilisateur se trouve dans la forêt A (Intranet) et le point de gestion basé sur Internet dans la forêt B (le réseau de périmètre). La forêt B approuve la forêt A et un pare-feu qui intervient autorise les paquets d'authentification.  

-   Le compte d’utilisateur et le point de gestion basé sur Internet sont dans la forêt A (Intranet). Le point de gestion est publié sur Internet par le biais d’un serveur proxy web (comme Forefront Threat Management Gateway).  

> [!NOTE]  
>  Si l'authentification Kerberos échoue, l'authentification NTLM est ensuite automatiquement utilisée.  

Comme dans l’exemple précédent, vous pouvez placer des systèmes de site basés sur Internet dans l’intranet quand ils sont publiés sur Internet via un serveur proxy web. Ces systèmes de site peuvent être configurés pour la connexion cliente à partir d’Internet uniquement, ou pour les connexions clientes à partir d’Internet et de l’intranet. Quand vous utilisez un serveur proxy web, vous pouvez le configurer pour le pontage SSL (Secure Sockets Layer) vers SSL (plus sécurisé) ou le tunnel SSL, comme suit :  

-   **Pontage SSL vers SSL :**   
    La configuration recommandée quand vous utilisez des serveurs web proxy pour la gestion de clients sur Internet est le pontage SSL vers SSL, qui utilise une terminaison SSL avec authentification. Les ordinateurs clients doivent être authentifiés à l'aide de l'authentification de l'ordinateur et les clients hérités de l'appareil mobile sont authentifiés à l'aide de l'authentification utilisateur. Les appareils mobiles inscrits par Configuration Manager ne prennent pas en charge le pontage SSL.  

     La terminaison SSL au niveau du serveur web proxy présente l’avantage que les paquets provenant d’Internet sont inspectés avant d’être transférés au réseau interne. Le serveur web proxy authentifie la connexion cliente, l’arrête, puis ouvre une nouvelle connexion authentifiée vers les systèmes de site basés sur Internet. Quand les clients Configuration Manager utilisent un serveur web proxy, leur identité (GUID client) est stockée de manière sécurisée dans la charge utile du paquet pour éviter que le point de gestion identifie le serveur web proxy comme le client. Le pontage n’est pas pris en charge dans Configuration Manager avec HTTP vers HTTPS ou avec HTTPS vers HTTP.  

-   **Tunneling** :   
    Si votre serveur web proxy ne peut pas prendre en charge la configuration requise pour le pontage SSL, ou si vous souhaitez configurer la prise en charge Internet pour les appareils mobiles inscrits par Configuration Manager, le tunneling SSL est aussi pris en charge. Il s’agit d’une option moins sûre, car les paquets SSL provenant d’Internet sont transférés aux systèmes de site sans terminaison SSL, ce qui empêche leur inspection à la recherche de contenu malveillant. Lors de l'utilisation du tunnel SSL, aucune configuration n'est requise pour les certificats pour le serveur Web proxy.  



##  <a name="Plan_Com_X-Forest"></a> Communications dans les forêts Active Directory  

Configuration Manager prend en charge les sites et hiérarchies qui s’étendent sur plusieurs forêts Active Directory. Il prend également en charge les ordinateurs de domaine qui ne se trouvent pas dans la même forêt Active Directory que le serveur de site, ainsi que les ordinateurs situés dans des groupes de travail.  


### <a name="bkmk_noforesttrust"></a> Prendre en charge des ordinateurs de domaine situés dans une forêt qui n’est pas approuvée par la forêt de votre serveur de site 

-   Installez des rôles de système de site dans cette forêt non approuvée, en activant l’option de publication des informations de site dans cette forêt Active Directory.  

-   Gérez ces ordinateurs comme s’il s’agissait d’ordinateurs de groupe de travail.  

Quand vous installez des serveurs de système de site dans une forêt Active Directory non approuvée, les communications des clients de cette forêt vers le serveur restent internes à cette forêt, ce qui permet à Configuration Manager d’authentifier l’ordinateur avec Kerberos. Quand vous publiez des informations de site dans la forêt du client, le client peut récupérer les informations de site, notamment la liste des points de gestion disponibles, à partir de sa forêt Active Directory, au lieu de télécharger ces informations à partir de son point de gestion attribué.  

> [!NOTE]  
>  Pour gérer des appareils sur Internet, vous pouvez installer des rôles de système de site Internet dans votre réseau de périmètre quand les serveurs de système de site se trouvent dans une forêt Active Directory. Ce scénario ne nécessite pas d’approbation bidirectionnelle entre le réseau de périmètre et la forêt du serveur de site.  


### <a name="bkmk_workgroup"></a> Prendre en charge des ordinateurs situés dans un groupe de travail  

-   Approuvez manuellement les ordinateurs du groupe de travail qui utilisent des connexions client HTTP pour accéder aux rôles de système de site. Configuration Manager ne peut pas authentifier ces ordinateurs avec Kerberos.  

-   Configurez les clients du groupe de travail avec le compte d’accès réseau pour permettre à ces ordinateurs de récupérer le contenu à partir des points de distribution.  

-   Fournir aux clients du groupe de travail une méthode de remplacement pour rechercher les points de gestion. Utilisez la publication DNS, WINS, ou attribuez directement un point de gestion. Ces clients ne peuvent pas récupérer les informations de site à partir d’Active Directory Domain Services.  

Pour plus d’informations, consultez les articles suivants :  

-   [Gérer les enregistrements en conflit](/sccm/core/clients/manage/manage-clients#BKMK_ConflictingRecords)  

-   [Compte d’accès au réseau](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#accounts-used-for-content-management)  

-   [Installer des clients Configuration Manager sur des ordinateurs de groupe de travail](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup)  


###  <a name="bkmk_span"></a> Scénarios de prise en charge d’un site ou d’une hiérarchie qui s’étend sur plusieurs domaines et forêts  

#### <a name="scenario-1-communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Scénario 1 : Communication entre les sites d’une hiérarchie qui s’étend sur des forêts  
Ce scénario nécessite une approbation de forêt bidirectionnelle prenant en charge l’authentification Kerberos.  Si vous n’avez pas d’approbation de forêt bidirectionnelle prenant en charge l’authentification Kerberos, Configuration Manager ne prend pas en charge de site enfant dans la forêt distante.  

Configuration Manager prend en charge l’installation d’un site enfant dans une forêt distante qui possède l’approbation bidirectionnelle requise avec la forêt du site parent. Par exemple, vous pouvez placer un site secondaire dans une autre forêt de son site parent principal tant que l’approbation nécessaire existe.  

> [!NOTE]  
>  Un site enfant peut être un site principal (où le site d’administration centrale est le site parent) ou un site secondaire.  

Les communications intersite dans Configuration Manager utilisent la réplication de base de données et les transferts basés sur des fichiers. Quand vous installez un site, vous devez spécifier un compte à utiliser pour installer le site sur le serveur indiqué. Ce compte établit et conserve également la communication entre les sites. Une fois que le site a été installé et a lancé les transferts basés sur des fichiers et la réplication de base de données, vous n’avez pas d’autres éléments à configurer pour la communication vers ce site.  

S’il y a une approbation de forêt bidirectionnelle, Configuration Manager ne nécessite aucune étape de configuration supplémentaire.  

Par défaut, quand vous installez un nouveau site enfant, Configuration Manager configure les éléments suivants :  

-   Un itinéraire de réplication de fichiers intersite sur chaque site qui utilise le compte d’ordinateur du serveur de site. Configuration Manager ajoute le compte d’ordinateur de chaque ordinateur au groupe **SMS_SiteToSiteConnection_&lt;code_site\>** sur l’ordinateur de destination.  

-   Réplication de base de données entre les serveurs SQL Server sur chaque site.  

Définissez également les configurations suivantes :  

-   Les appareils réseau et les pare-feu qui interviennent doivent autoriser les paquets réseau requis par Configuration Manager.  

-   La résolution de noms doit fonctionner entre les forêts.  

-   Pour installer un site ou un rôle de système de site, vous devez spécifier un compte qui dispose des autorisations d'administrateur local sur l'ordinateur spécifié.  

#### <a name="scenario-2-communication-in-a-site-that-spans-forests"></a>Scénario 2 : Communication dans un site qui s’étend sur des forêts  
Ce scénario ne nécessite pas d’approbation de forêt bidirectionnelle.  

Les sites principaux prennent en charge l’installation de rôles de système de site sur des ordinateurs situés dans des forêts distantes.  

-   Le point de service web du catalogue des applications est la seule exception.  Il est uniquement pris en charge dans la même forêt que le serveur de site.  

-   Quand un rôle de système de site accepte les connexions depuis Internet, la bonne pratique de sécurité est d’installer ce rôle dans un emplacement où la limite de forêt assure une protection pour le serveur de site (par exemple, dans un réseau de périmètre).  

Pour installer un rôle de système de site sur un ordinateur situé dans une forêt non approuvée :  

- Spécifiez un **Compte d’installation du système de site**, que le site utilise pour installer le rôle de système de site. (Ce compte doit disposer d’informations d’identification administratives locales pour la connexion.) Ensuite, installez les rôles de système de site sur l’ordinateur spécifié.  

- Sélectionnez l’option de système de site **Exiger que le serveur de site établisse des connexions vers ce système de site**. Avec ce paramètre, le serveur de site doit établir des connexions au serveur de système de site pour transférer des données. Cette configuration empêche l’ordinateur qui se trouve dans l’emplacement non approuvé d’établir une communication avec le serveur de site au sein de votre réseau approuvé. Ces connexions utilisent le **Compte d'installation du système de site**.  

Pour utiliser un rôle de système de site installé dans une forêt non approuvée, les pare-feu doivent autoriser le trafic réseau, même quand le serveur de site lance le transfert de données.  

Par ailleurs, les rôles de système de site suivants requièrent un accès direct à la base de données de site. Par conséquent, les pare-feu doivent autoriser le trafic applicable de la forêt non approuvée vers les sites SQL Server :  

-   Point de synchronisation Asset Intelligence  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point de gestion  

-   Point du service de rapport  

-   Point de migration d’état  

Pour plus d’informations, consultez [Ports utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/ports).  

Vous pouvez avoir besoin de configurer l’accès du point de gestion et du point d’inscription à la base de données de site.

-   Par défaut, quand vous installez ces rôles, Configuration Manager configure le compte d’ordinateur du nouveau serveur de système de site comme compte de connexion pour le rôle de système de site. Il ajoute ensuite le compte au rôle de base de données SQL Server approprié.  

-   Quand vous installez ces rôles de système de site dans un domaine non approuvé, configurez le compte de connexion du rôle de système de site pour autoriser le rôle de système de site à récupérer des informations de la base de données.  

Si vous configurez un compte d’utilisateur de domaine comme compte de connexion pour ces rôles de système de site, assurez-vous que le compte d’utilisateur de domaine dispose de l’accès approprié à la base de données SQL Server sur ce site :  

-   Point de gestion : **Compte de connexion à la base de données du point de gestion**  

-   Point d'inscription : **Compte de connexion du point d’inscription**  

Lorsque vous planifiez des rôles de système de site dans d'autres forêts, tenez compte des informations supplémentaires suivantes :  

-   Si vous exécutez un pare-feu Windows, configurez les profils de pare-feu applicables pour transmettre les communications entre le serveur de base de données du site et les ordinateurs qui sont installés avec des rôles de système de site distants.   

-   Quand le point de gestion Internet approuve la forêt contenant les comptes d’utilisateur, les stratégies utilisateur sont prises en charge. Lorsqu'il n'existe aucune relation d'approbation, seules les stratégies d'ordinateur sont prises en charge.  

#### <a name="scenario-3-communication-between-clients-and-site-system-roles-when-the-clients-arent-in-the-same-active-directory-forest-as-their-site-server"></a>Scénario 3 : Communication entre les clients et les rôles de système de site quand les clients ne se trouvent pas dans la même forêt Active Directory que leur serveur de site  
Configuration Manager prend en charge les scénarios suivants pour les clients qui ne se trouvent pas dans la même forêt que le serveur de leur site :  

-   Il y a une relation d’approbation de forêt bidirectionnelle entre la forêt du client et celle du serveur du site.  

-   Le serveur de rôle de système de site se trouve dans la même forêt que le client.  

-   Le client se trouve sur un ordinateur de domaine sans approbation de forêt bidirectionnelle avec le serveur de site, et les rôles de système de site ne sont pas installés dans la forêt du client.  

-   Le client se trouve sur un ordinateur de groupe de travail.  

Les clients se trouvant sur un ordinateur joint à un domaine peuvent utiliser les services de domaine Active Directory pour l’emplacement du service si leur site est publié dans leur forêt Active Directory.  

Pour publier des informations de site dans une autre forêt Active Directory :  

-   Spécifiez la forêt et activez la publication dans cette forêt dans le nœud **Forêts Active Directory** de l’espace de travail **Administration** .  

-   Configurez chaque site pour publier ses données dans les services de domaine Active Directory. Cette configuration permet aux clients se trouvant dans cette forêt d'extraire des informations de site et de trouver des points de gestion. Si le client ne peut pas utiliser Active Directory Domain Services pour l’emplacement du service, utilisez DNS, WINS ou le point de gestion attribué du client.  


####  <a name="bkmk_xchange"></a> Scénario 4 : Placer le connecteur du serveur Exchange Server dans une forêt distante  

Pour ce scénario, assurez-vous que la résolution de noms fonctionne entre les forêts. Par exemple, configurez des transferts DNS. Quand vous configurez le connecteur du serveur Exchange Server, spécifiez le nom de domaine intranet complet du serveur Exchange Server. Pour plus d’informations, consultez [Gérer des appareils mobiles à l’aide de Configuration Manager et d’Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="see-also"></a>Voir aussi

- [Planifier la sécurité](/sccm/core/plan-design/security/plan-for-security)  

- [Sécurité et confidentialité pour les clients Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

