---
title: Ports utilisés pour les connexions
titleSuffix: Configuration Manager
description: Découvrez les ports réseau obligatoires et personnalisables qu’utilise Configuration Manager pour les connexions.
ms.date: 09/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8338e08ffb6d09299123e363f27e586b650452fe
ms.sourcegitcommit: 231111a704777789629911369f4d9593d2053fc0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55065097"
---
# <a name="ports-used-in-configuration-manager"></a>Ports utilisés dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article répertorie les ports réseau utilisés par Configuration Manager. Certaines connexions utilisent des ports qui ne sont pas configurables, et certaines prennent en charge des ports personnalisés que vous spécifiez. Si vous utilisez une technologie de filtrage des ports, vérifiez que les ports obligatoires sont disponibles. Ces technologies de filtrage des ports sont notamment les pare-feux, les routeurs, les serveurs proxy et la sécurité du protocole Internet (IPsec).   

> [!NOTE]  
>  Si vous prenez en charge les clients Internet par pontage SSL, parallèlement aux exigences de port, vous devrez peut-être également autoriser certains verbes et en-têtes HTTP pour traverser le pare-feu.   



##  <a name="BKMK_ConfigurablePorts"></a> Ports configurables  
 Configuration Manager vous permet de configurer les ports pour les types de communication suivants :  

-   Point du site web du catalogue des applications vers point de service web du catalogue des applications  

-   Point proxy d'inscription vers point d'inscription  

-   Client vers systèmes de site exécutant IIS  

-   Client vers Internet (sous forme de paramètres du serveur proxy)  

-   Point de mise à jour logicielle vers Internet (sous forme de paramètres du serveur proxy)  

-   Point de mise à jour logicielle à serveur WSUS  

-   Serveur de site à serveur de base de données de site  

-   Points de Reporting Services  

    > [!NOTE]  
    >  Les ports qui sont utilisés pour le rôle de système de site du point de Reporting Services sont configurés dans SQL Server Reporting Services. Ces ports sont ensuite utilisés par Configuration Manager pendant les communications à destination du point de Reporting Services. Veillez à passer en revue les ports qui définissent les informations de filtre IP pour les stratégies IPsec ou pour la configuration des pare-feu.  

Par défaut, le port HTTP utilisé pour la communication entre le client et le système de site est le port 80, et le port HTTPS par défaut est le port 443. Vous pouvez modifier les ports HTTP ou HTTPS de communication entre le client et le système de site pendant l’installation ou dans les propriétés de votre site Configuration Manager.  

Les ports qui sont utilisés pour le rôle de système de site du point de Reporting Services sont configurés dans SQL Server Reporting Services. Ces ports sont ensuite utilisés par Configuration Manager pendant les communications à destination du point de Reporting Services. Veillez à passer en revue ces ports quand vous définissez les informations de filtre IP pour les stratégies IPsec ou pour la configuration des pare-feu.  



##  <a name="BKMK_NonConfigurablePorts"></a> Ports non configurables  

Configuration Manager ne vous autorise pas à configurer des ports pour les types de communication suivants :  

-   Site à site  

-   Serveur de site à système de site  

-   Console Configuration Manager vers le fournisseur SMS  

-   Console Configuration Manager vers Internet  

-   Connexions aux services cloud tels que Microsoft Intune et les points de distribution cloud  



##  <a name="BKMK_CommunicationPorts"></a> Ports utilisés par les clients Configuration Manager et les systèmes de site  

Les sections suivantes détaillent les ports qui sont utilisés pour la communication dans Configuration Manager. Les flèches figurant dans les titres des sections indiquent le sens de la communication :  

-   -- > indique qu’un ordinateur initie la communication et que l’autre ordinateur répond toujours ;  

-   &lt; -- > indique que les deux ordinateurs peuvent initier la communication.  


###  <a name="BKMK_PortsAI"></a> Point de synchronisation Asset Intelligence -- > Microsoft  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsAI-to-SQL"></a> Point de synchronisation Asset Intelligence -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsAppCatalogService-SQL"></a> Point de service Web du catalogue des applications -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> Point du site Web du catalogue des applications -- > Point de service Web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> Client -- > Point du site Web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsClient-ClientWakeUp"></a> Client -- &gt; Client  

En plus des ports qui sont répertoriés dans ce tableau, le proxy de mise en éveil utilise également des messages de demande d’écho ICMP d’un client à l’autre. Les clients utilisent cette communication pour vérifier si l’autre client est en éveil sur le réseau. Le protocole ICMP est ce que l’on appelle parfois des commandes ping. ICMP ne disposant pas d’un numéro de protocole UDP ou TCP, il ne figure pas dans le tableau ci-dessous. Toutefois, les pare-feu d'hôte de ces ordinateurs clients ou les appareils réseau intervenant sur le sous-réseau doivent autoriser le trafic ICMP pour que la communication avec le proxy de mise en éveil aboutisse.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Éveil par appel réseau|9 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|--|  
|Proxy de mise en éveil|25536 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|--|  


###  <a name="BKMK_PortsClient-PolicyModule"></a> Client -- > Module de stratégie SCEP (protocole d’inscription de certificats simple) de Configuration Manager   

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP||80|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsClient-CloudDP"></a> Client -- >Point de distribution cloud  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).


###  <a name="bkmk_client-cmg"></a> Client -- > Passerelle de gestion cloud  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsClient-DP"></a> Client -- > Point de distribution  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsClient-DP2"></a> Client -- > Point de distribution configuré pour la multidiffusion  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Protocole de multidiffusion|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> Client -- > Point de distribution configuré pour PXE  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|DHCP|67 et 68|--|  
|TFTP|69 <sup>[Note 4](#bkmk_note4)</sup> |--|  
|BINL (Boot Information Negotiation Layer)|4011|--|  

> [!Important]  
> Si vous activez un pare-feu basé sur l’hôte, vérifiez que les règles autorisent le serveur à envoyer et à recevoir des données sur ces ports. Lorsque vous activez un point de distribution pour PXE, Configuration Manager peut activer les règles de trafic entrant (réception) du Pare-feu Windows. Il ne configure pas les règles de trafic sortant (envoi).<!--SCCMDocs issue #744-->  


###  <a name="BKMK_PortsClient-FSP"></a> Client -- > Point d’état de secours  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsClient-GCDC"></a> Client -- > Contrôleur de domaine de catalogue global  
 Un client Configuration Manager ne contacte pas de serveur de catalogue global lorsqu’il s’agit d’un ordinateur de groupe de travail ou lorsqu’il est configuré pour les communications Internet uniquement.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP de catalogue global|--|3268|  


###  <a name="BKMK_PortsClient-MP"></a> Client -- > Point de gestion  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Notification du client (communication par défaut avant le basculement en HTTP ou HTTPS)|--|10123 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsClient-SUP"></a> Client -- > Point de mise à jour logicielle  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup>[Note 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup>[Note 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsClient-SMP"></a> Client -- > Point de migration d’état  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|SMB (Server Message Block)|--|445|  


###  <a name="bkmk_cmgcp-cmg"></a> Point de connexion de passerelle de gestion cloud --> Service cloud de passerelle de gestion cloud  

Configuration Manager utilise ces connexions pour créer le canal de la passerelle de gestion cloud. Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|TCP-TLS (recommandé)|--|10140-10155|  
|HTTPS (avec une machine virtuelle de repli)|--|443|  
|HTTPS (avec plusieurs machines virtuelles de repli)|--|10124-10139|  


###  <a name="bkmk_cmgcp-mp"></a> Point de distribution de passerelle de gestion cloud -- > Point de gestion  

#### <a name="version-1706-or-1710"></a>Version 1706 ou 1710
Le port dépend de la configuration du point de gestion. 

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

#### <a name="version-1802"></a>Version 1802

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="bkmk_cmgcp-sup"></a> Point de connexion de passerelle de gestion cloud -- > Point de mise à jour logicielle  

Le port dépend de la configuration du point de mise à jour logicielle. 

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|
|HTTP|--|80|  

Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsConsole-Client"></a> Console Configuration Manager -- > Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Contrôle à distance (contrôle)|--|2701|  
|Assistance à distance (RDP et RTC)|--|3389|  


###  <a name="BKMK_PortsConsole-Internet"></a>Console Configuration Manager -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  
|HTTPS|--|443|

La console Configuration Manager utilise l’accès à Internet pour les actions suivantes : 
- le téléchargement des mises à jour de logiciels à partir de Microsoft Update pour les packages de déploiement ;
- L’élément Commentaires du ruban
- les liens vers la documentation dans la console.
<!--506823-->


###  <a name="BKMK_PortsConsole-RSP"></a> Console Configuration Manager -- > Point de Reporting Services  


|Description|UDP|TCP|
|-----------------|---------|---------|   
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsConsole-Site"></a> Console Configuration Manager -- > Serveur de site  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (connexion initiale à WMI pour localiser le système fournisseur)|--|135|  


###  <a name="BKMK_PortsConsole-Provider"></a> Console Configuration Manager -- > Fournisseur SMS  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Module de stratégie SCEP (service d’inscription de périphérique réseau) de Configuration Manager -- > Point d’inscription de certificat  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsDWSPSQL"></a> Point de service de l’entrepôt de données --> SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsDist_MP"></a> Point de distribution -- > Point de gestion  
 Un point de distribution communique avec le point de gestion dans les scénarios suivants :  

-   Pour signaler l’état du contenu préparé  

-   Pour signaler les données de synthèse d'utilisation  

-   Pour signaler la validation du contenu  

-   Pour signaler l’état des téléchargements de packages (point de distribution d’extraction)

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Point Endpoint Protection -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80|  


###  <a name="BKMK_PortsEP-to-SQL"></a> Point Endpoint Protection -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> Point proxy d’inscription -- > Point d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> Point d’inscription -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Connecteur du serveur Exchange Server -- &gt; Exchange Online  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Gestion à distance de Windows via HTTPS|--|5986|  


###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Connecteur du serveur Exchange Server -- > Serveur Exchange Server local  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Gestion à distance de Windows via HTTP|--|5985|  


###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Ordinateur Mac -- > Point proxy d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsMP-DC"></a> Point de gestion -- > Contrôleur de domaine  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|  
|LDAP de catalogue global|--|3268|  
|Mappeur de point de terminaison RPC|--|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsMP-Site"></a> Point de gestion &lt; -- > Serveur de site  
 <sup>[Note 5](#bkmk_note5)</sup>   

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Mappeur de point de terminaison RPC|--|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  
|SMB (Server Message Block)|--|445|  


###  <a name="BKMK_PortsMP-SQL"></a> Point de gestion -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> Appareil mobile -- > Point proxy d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> Appareil mobile -- > Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  


###  <a name="BKMK_PortsRSP-SQL"></a> Point de Reporting Services -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> Point de connexion de service -- > Microsoft Intune  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|

Pour plus d’informations, consultez la section [Conditions requises pour l’accès à Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls) du point de connexion de service.


###  <a name="bkmk_scp-cmg"></a> Point de connexion de service -- > Azure (passerelle de gestion cloud)  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Protocole HTTPS pour le déploiement d’un service de passerelle de gestion cloud|--|443|

Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).


###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> Serveur de site &lt; -- > Point de service Web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> Serveur de site &lt; -- > Point du site Web du catalogue des applications  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-AISP"></a> Serveur de site &lt; -- > Point de synchronisation Asset Intelligence  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Client"></a> Serveur de site -- > Client  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Éveil par appel réseau|9 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|--|  


###  <a name="BKMK_PortsSiteServer-CloudDP"></a> Serveur de site -- > Point de distribution cloud  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS|--|443|  

Pour plus d’informations, consultez [Ports et flux de données](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_dataflow).


###  <a name="BKMK_PortsSite-DP"></a> Serveur de site -- > Point de distribution  
 <sup>[Note 5](#bkmk_note5)</sup>  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-DC"></a> Serveur de site -- > Contrôleur de domaine  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|LDAP (Lightweight Directory Access Protocol)|389|389|  
|LDAP de catalogue global|--|3268|  
|Mappeur de point de terminaison RPC|--|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> Serveur de site &lt; -- > Point d’enregistrement de certificat  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> Serveur de site &lt; -- > Point Endpoint Protection  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> Serveur de site &lt; -- > Point d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> Serveur de site &lt; -- > Point proxy d’inscription  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-FSP"></a> Serveur de site &lt; -- > Point d’état de secours  
 <sup>[Note 5](#bkmk_note5)</sup>  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortSite-Internet"></a> Serveur de site -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 1](#bkmk_note1)</sup>|  


###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> Serveur de site &lt; -- > Autorité de certification (CA) émettrice  
 Cette communication est utilisée lorsque vous déployez des profils de certificat à l'aide du point d'enregistrement de certificat. La communication n’est pas utilisée pour chaque serveur de site de la hiérarchie. En fait, elle est utilisée uniquement pour le serveur de site situé en haut de la hiérarchie.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC (DCOM)|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-RSP"></a> Serveur de site &lt; -- > Point de Reporting Services  
 <sup>[Note 5](#bkmk_note5)</sup>  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Site"></a> Serveur de site &lt; -- > Serveur de site  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  


###  <a name="BKMK_PortsSite-SQL"></a> Serveur de site -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  

 Lors de l’installation d’un site utilisant une instance SQL Server distante pour héberger la base de données de site, ouvrez les ports suivants entre le serveur de site et l’instance SQL Server :  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-Provider"></a> Serveur de site -- > Fournisseur SMS  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  
|RPC|--|DYNAMIQUE <sup>[Note 6](#bkmk_note6)</sup>|  


###  <a name="BKMK_PortsSite-SUP"></a> Serveur de site &lt; -- > Point de mise à jour logicielle  
 <sup>[Note 5](#bkmk_note5)</sup>  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|HTTP|--|80 ou 8530 <sup>[Note 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup>[Note 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsSite-SMP"></a> Serveur de site &lt; -- > Point de migration d’état  
 <sup>[Note 5](#bkmk_note5)</sup>  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  
|Mappeur de point de terminaison RPC|135|135|  


###  <a name="BKMK_PortsProvider-SQL"></a> Fournisseur SMS -- &gt; SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMK_PortsSUP-Internet"></a> Point de mise à jour logicielle -- > Internet  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 <sup>[Note 1](#bkmk_note1)</sup>|  


###  <a name="BKMK_PortsSUP-WSUS"></a> Point de mise à jour logicielle -- > Serveur WSUS en amont  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP|--|80 ou 8530 <sup>[Note 3](#bkmk_note3)</sup>|  
|HTTPS|--|443 ou 8531 <sup>[Note 3](#bkmk_note3)</sup>|  


###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 La réplication inter-sites de base de données exige que le serveur SQL Server d’un site communique directement avec le serveur SQL Server de son site parent ou enfant.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Service SQL Server|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  
|Service Broker SQL Server|--|4022 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  

> [!TIP]  
>  Configuration Manager ne nécessite pas SQL Server Browser, qui utilise le port UDP 1434.  


###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> Point de migration d’état -- > SQL Server  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SQL sur TCP|--|1433 <sup>[Note 2](#bkmk_note2) Autre port disponible</sup>|  


###  <a name="BKMY_PortNotes"></a> Notes pour les ports utilisés par les clients Configuration Manager et les systèmes de site  

#### <a name="bkmk_note1"></a>Note 1 : Port du serveur proxy
Ce port ne peut pas être configuré, mais il peut être routé vers un serveur proxy configuré.  

#### <a name="bkmk_note2"></a> Note 2 : Port alternatif disponible
Un autre port peut être défini dans Configuration Manager pour cette valeur. Si un port personnalisé a été défini, remplacez-le lorsque vous définissez les informations de filtre IP pour les stratégies IPsec ou pour configurer les pare-feu.  

#### <a name="bkmk_note3"></a> Note 3 : Windows Server Update Services (WSUS)
WSUS peut être installé pour utiliser les ports 80/443 ou 8530/8531 pour la communication client. Quand vous exécutez WSUS dans Windows Server 2012 ou Windows Server 2016, WSUS est configuré par défaut pour utiliser le port 8530 pour HTTP et le port 8531 pour HTTPS.  

Après l'installation, vous pouvez modifier le port. Il n’est pas nécessaire d’utiliser le même numéro de port pour l’ensemble de la hiérarchie du site.  

- Si le numéro de port HTTP est 80, le numéro de port HTTPS doit être 443.  

- Si le port HTTP a un autre numéro, le port HTTPS doit avoir le numéro 1 ou plus (par exemple 8530 et 8531).   

    > [!NOTE]  
    >  Quand vous configurez le point de mise à jour logicielle pour utiliser HTTPS, le port HTTP doit également être ouvert. Les données non chiffrées, telles que le CLUF pour les mises à jour spécifiques, utilisent le port HTTP.  

#### <a name="bkmk_note4"></a> Note 4 : Trivial FTP (TFTP) Daemon
Le service système Trivial FTP (TFTP) Daemon ne nécessite pas de nom d’utilisateur ou de mot de passe, et fait partie intégrante des services de déploiement Windows (WDS). Le service Trivial FTP met en œuvre la prise en charge du protocole TFTP qui est défini par les normes RFC suivantes :  

- RFC 350 : TFTP  

- RFC 2347 : Extension d’option  

- RFC 2348 : Option de taille de bloc  

- RFC 2349 : Options d’intervalle de délai d’attente et de taille de transfert  

Le protocole TFTP est conçu pour prendre en charge les environnements de démarrage sans disque. Les services Trivial FTP écoutent au port UDP 69 mais répondent à partir d'un port à numéro élevé alloué de manière dynamique. Ainsi, l’activation de ce port permet au service TFTP de recevoir les demandes TFTP entrantes mais n’autorise pas le serveur sélectionné à répondre à ces demandes. Vous ne pouvez pas permettre au serveur sélectionné de répondre aux demandes TFTP entrantes, à moins que le serveur TFTP soit configuré de manière à répondre à partir du port 69.  

Le point de distribution compatible PXE et le client présent dans Windows PE sélectionnent des ports à numéro élevé alloués dynamiquement pour les transferts TFTP. Ces ports sont définis par Microsoft entre 49152 et 65535. Pour plus d’informations, consultez [Vue d’ensemble des services et exigences de ports réseau pour le système Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).

Toutefois, lors du démarrage PXE, la carte réseau de l’appareil sélectionne le port à numéro élevé alloué dynamiquement qu’elle utilise durant le transfert TFTP. La carte réseau de l’appareil n’est pas liée aux ports à numéro élevé qui sont alloués dynamiquement et définis par Microsoft. Elle est uniquement liée aux ports définis par la RFC 350. Ce port est compris dans la plage allant de 0 à 65535. Pour plus d’informations sur les ports à numéro élevé et alloués dynamiquement qui sont utilisés par la carte réseau, contactez le fabricant de l’appareil.


#### <a name="bkmk_note5"></a> Note 5 : Communication entre le serveur de site et les systèmes de site
par défaut, la communication entre le serveur de site et les systèmes de site est bidirectionnelle. Le serveur de site initialise la communication pour configurer le système de site, puis la plupart des systèmes de site se connectent à leur tour au serveur de site pour envoyer des informations d'état. Les points de Reporting Services et les points de distribution n’envoient pas d’informations d’état. Si vous sélectionnez **Exiger que le serveur de site démarre les connexions vers ce système de site** dans les propriétés du système de site, après l’installation du système de site, ce dernier n’établit pas la communication vers le système de site. Au lieu de cela, le serveur de site initie la communication et utilise le compte d’installation du système de site pour l’authentification auprès du serveur de système de site.  

#### <a name="bkmk_note6"></a> Note 6 : Ports dynamiques
Les ports dynamiques utilisent une plage de numéros de ports qui est définie par la version du système d’exploitation. Ces ports sont également appelés « ports éphémères ». Pour plus d'informations sur les plages de port par défaut, voir [Vue d'ensemble des services et exigences de ports réseau pour le système Windows Server](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows).  



##  <a name="BKMK_AdditionalPorts"></a> Listes de ports supplémentaires  

 Les sections suivantes fournissent des informations supplémentaires sur les ports utilisés par Configuration Manager.  

###  <a name="BKMK_ClientShares"></a> Client vers partages serveur  

 Les clients utilisent le protocole SMB (Server Message Block) à chaque fois qu'ils se connectent à des partages UNC. Par exemple :  

-   Installation manuelle du client spécifiant la propriété de ligne de commande CCMSetup.exe **/source:**  

-   Clients Endpoint Protection qui téléchargent des fichiers de définition à partir d’un chemin UNC

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block)|--|445|  


###  <a name="BKMK_SQLPorts"></a> Connexions à Microsoft SQL Server  

 Pour la communication vers le moteur de base de données SQL Server et pour la réplication intersite, vous pouvez utiliser le port de SQL Server par défaut ou spécifier des ports personnalisés :  

-   Utilisation des communications intersites :  

    -   SQL Server Service Broker, qui utilise par défaut le port TCP 4022.  

    -   Service SQL Server, qui utilise par défaut le port TCP 1433.  

-   Les communications intrasites entre le moteur de base de données SQL Server et divers rôles de système de site Configuration Manager utilisent par défaut le port TCP 1433.  

- Configuration Manager utilise les mêmes ports et protocoles pour communiquer avec chaque réplica du groupe de disponibilité SQL qui héberge la base de données comme si le réplica était une instance SQL Server autonome.

Si vous utilisez Azure alors que la base de données de site se trouve derrière un équilibreur de charge interne ou externe, configurez les composants suivants :
- Exceptions de pare-feu sur chaque réplica
- Règles d’équilibrage de charge 

Configurez les ports suivants :
 - SQL sur TCP : TCP 1433
 - SQL Server Service Broker : TCP 4022
 - SMB (Server Message Block) : TCP 445
 - Mappeur de point de terminaison RPC : TCP 135

> [!WARNING]  
>  Configuration Manager ne prend pas en charge les ports dynamiques. Par défaut, les instances nommées de SQL Server utilisent des ports dynamiques pour les connexions au moteur de base de données. Lorsque vous utilisez une instance nommée, configurez manuellement le port statique pour la communication intrasite.  

 Les rôles de système de site suivants communiquent directement avec la base de données SQL Server :  

-   Point de service web du catalogue des applications  

-   Rôle de point d'enregistrement de certificat  

-   Rôle de point d'inscription  

-   Point de gestion  

-   Serveur de site  

-   Point de Reporting Services  

-   fournisseur SMS  

-   SQL Server --> SQL Server  

Chaque base de données de site doit être hébergée sur sa propre instance de SQL Server. Configurez chaque instance avec un ensemble unique de ports.  

Si vous activez un pare-feu basé sur l’hôte sur le serveur SQL, configurez-le pour autoriser les ports nécessaires. Configurez également des pare-feux réseau entre les ordinateurs qui communiquent avec le serveur SQL.  

Pour obtenir un exemple de configuration de SQL Server pour l’utilisation d’un port spécifique, consultez [Configurer un serveur pour écouter un port TCP spécifique](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port).  


### <a name="bkmk_discovery"> </a> Découverte et publication

Configuration Manager utilise les ports suivants pour la découverte et la publication d’informations de site :
 - LDAP (Lightweight Directory Access Protocol) : 389
 - LDAP de catalogue global : 3268
 - Mappeur de point de terminaison RPC : 135
 - RPC : Ports TCP à numéro élevé alloués dynamiquement
 - TCP : 1024 : 5000
 - TCP :  49152 : 65535


###  <a name="BKMK_External"></a> Connexions externes effectuées par Configuration Manager  

Les clients ou les systèmes de site Configuration Manager locaux peuvent établir les connexions externes suivantes :  

-   [Point de synchronisation Asset Intelligence -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Point Endpoint Protection -- &gt; Internet](#BKMK_PortsEndpointProtection_Internet)  

-   [Client -- &gt; Contrôleur de domaine de catalogue global](#BKMK_PortsClient-GCDC)  

-   [Console Configuration Manager -- &gt; Internet](#BKMK_PortsConsole-Internet)  

-   [Point de gestion -- &gt; Contrôleur de domaine](#BKMK_PortsMP-DC)  

-   [Serveur de site -- &gt; Contrôleur de domaine](#BKMK_PortsSite-DC)  

-   [Serveur de site &lt; -- &gt; Autorité de certification (CA) émettrice](#BKMK_PortsIssuingCA_SiteServer)  

-   [Point de mise à jour logicielle -- &gt; Internet](#BKMK_PortsSUP-Internet)  

-   [Point de mise à jour logicielle -- &gt; Serveur WSUS en amont](#BKMK_PortsSUP-WSUS)  

-   [Point de connexion de service -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

- [Point de connexion de service -- > Azure](#bkmk_scp-cmg)  

- [Point de connexion de passerelle de gestion cloud --> Service cloud de passerelle de gestion cloud](#bkmk_cmgcp-cmg)  


###  <a name="BKMK_IBCMports"></a> Configuration requise pour l’installation des systèmes de site qui prennent en charge les clients Internet  

 > [!Note]  
 > Cette section s’applique uniquement à la gestion du client basée sur Internet. Elle ne s’applique pas à la passerelle de gestion cloud. Pour plus d’informations, consultez [Gérer les clients sur Internet](/sccm/core/clients/manage/manage-clients-internet).  

 Les points de gestion basée sur Internet, les points de distribution qui prennent en charge les clients Internet, le point de mise à jour logicielle et le point d’état de repli utilisent les ports suivants pour l’installation et la réparation :  

-   Serveur de site --> Système de site : Mappeur de point de terminaison RPC à l'aide du port UDP et du port TCP 135.  

-   Serveur de site --> Système de site : Ports TCP RPC dynamiques  

-   Serveur de site &lt; --> système de site : Protocole SMB (Server Message Blocks) à l'aide du port TCP 445

Les installations d'applications et de packages sur les points de distribution nécessitent les ports RPC suivants :  

-   Serveur de site -- > Point de distribution : Mappeur de point de terminaison RPC à l'aide du port UDP et du port TCP 135

-   Serveur de site -- > Point de distribution : Ports TCP RPC dynamiques  

Utilisez IPsec pour sécuriser le trafic entre le serveur de site et les systèmes de site. Si vous devez restreindre les ports dynamiques utilisés par RPC, vous pouvez employer l'outil de configuration Microsoft RPC (rpccfg.exe) pour configurer une plage de ports limitée à ces paquets RPC. Pour plus d'informations sur l'outil de configuration RPC, voir [Comment configurer RPC pour qu'il utilise certains ports et comment sécuriser ces ports à l'aide d'IPsec](https://support.microsoft.com/help/908472/how-to-configure-rpc-to-use-certain-ports-and-how-to-help-secure-those).  

> [!IMPORTANT]  
>  Avant d'installer ces systèmes de site, vérifiez que le service d'accès à distance au Registre est en cours d'exécution sur le serveur de système de site et que vous avez spécifié un compte d'installation du système de site si le système de site est situé dans une autre forêt Active Directory sans relation d'approbation.  


###  <a name="BKMK_PortsClientInstall"></a> Ports utilisés par l’installation du client Configuration Manager  

Les ports utilisés par Configuration Manager pendant l’installation du client dépendent de la méthode de déploiement. 

- Pour obtenir la liste des ports utilisés pour chaque méthode de déploiement de client, consultez [Ports utilisés lors du déploiement du client de Configuration Manager](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients#ports-used-during-configuration-manager-client-deployment).  

- Pour plus d’informations sur la configuration du Pare-feu Windows sur le client pour l’installation du client et la communication après l’installation, consultez [Paramètres de port et de pare-feu Windows pour les clients](/sccm/core/clients/deploy/windows-firewall-and-port-settings-for-clients).  


###  <a name="BKMK_MigrationPorts"></a> Ports utilisés par la migration  

Le serveur de site qui exécute la migration utilise plusieurs ports pour se connecter aux sites applicables dans la hiérarchie source. Pour plus d’informations, consultez [Configurations requises pour la migration](/sccm/core/migration/prerequisites-for-migration#BKMK_Required_Configurations).  


###  <a name="BKMK_ServerPorts"></a> Ports utilisés par Windows Server  

 Le tableau suivant répertorie certains des principaux ports utilisés par Windows Server. 

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|DNS|53|53|  
|DHCP|67 et 68|--|  
|Résolution de noms Netbios|137|--|  
|Service de datagramme NetBIOS|138|--|  
|Service de session NETBIOS|--|139|  
|Authentification Kerberos|--|88|

Pour plus d’informations, consultez les articles suivants :
- [Vue d’ensemble des services et exigences de ports réseau pour Windows](https://support.microsoft.com/help/832017/service-overview-and-network-port-requirements-for-windows)  

- [Guide pratique pour configurer un pare-feu pour des domaines et des approbations](https://support.microsoft.com/help/179442/how-to-configure-a-firewall-for-domains-and-trusts)
