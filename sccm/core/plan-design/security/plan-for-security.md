---
title: Planifier la sécurité
titleSuffix: Configuration Manager
description: Découvrez les bonnes pratiques et d’autres informations relatives à la sécurité dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5e6aca35dcadf145c0b93f0c984767099eb8960
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083557"
---
# <a name="plan-for-security-in-configuration-manager"></a>Planifier la sécurité dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit les concepts à prendre en compte lors de la planification de la sécurité avec votre implémentation de Configuration Manager. Il comprend les sections suivantes :  

- [Planifier des certificats (auto-signés et PKI)](#BKMK_PlanningForCertificates)  
    - [Certificats Cryptography: Next Generation (CNG)](#bkmk_plan-cng)  
    - [HTTP amélioré](#bkmk_plan-ehttp)  
    - [Certificats pour la passerelle de gestion cloud (CMG) et pour le point de distribution cloud (CDP)](#bkmk_plan-cmgcdp)  
    - [Certificat de signature du serveur de site (auto-signé)](#bkmk_plansitesign)  
    - [Révocation de certificat PKI](#BKMK_PlanningForCRLs)  
    - [Certificats racine approuvés PKI et émetteurs de certificats](#BKMK_PlanningForRootCAs)  
    - [Sélection du certificat client PKI](#BKMK_PlanningForClientCertificateSelection)  
    - [Une stratégie de transition pour les certificats PKI et la gestion des clients via Internet](#BKMK_PlanningForPKITransition)  

- [Planifier la clé racine approuvée](#BKMK_PlanningForRTK)  

- [Planifier la signature et le chiffrement](#BKMK_PlanningForSigningEncryption)  

- [Planifier l’administration basée sur des rôles](#BKMK_PlanningForRBA)  

- [Planifier Azure Active Directory](#bkmk_planazuread)  

- [Planifier l’authentification du fournisseur SMS](#bkmk_auth)



##  <a name="BKMK_PlanningForCertificates"></a> Planifier des certificats (auto-signés et PKI)  

 Configuration Manager utilise une combinaison de certificats auto-signés et de certificats pour infrastructure à clé publique (PKI).  

 Utilisez des certificats PKI quand c’est possible. Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Quand Configuration Manager demande des certificats PKI, lors de l’inscription d’appareils mobiles, vous devez utiliser les services de domaine Active Directory et une autorité de certification d’entreprise. Déployez et gérez tous les autres certificats PKI indépendamment de Configuration Manager. 

 Des certificats PKI sont nécessaires quand les ordinateurs clients se connectent à des systèmes de site basés sur Internet. Certains scénarios impliquant la passerelle de gestion cloud et le point de distribution cloud nécessitent également des certificats PKI. Pour plus d’informations, consultez [Gérer les clients sur Internet](/sccm/core/clients/manage/manage-clients-internet).

 Quand vous utilisez une infrastructure à clés publiques, vous pouvez également utiliser IPsec pour renforcer la sécurité de la communication serveur à serveur entre les systèmes de site d’un site, entre les sites, et pour tout autre transfert de données entre ordinateurs. L’implémentation d’IPsec est indépendante de Configuration Manager.  

 Quand des certificats PKI ne sont pas disponibles, Configuration Manager génère automatiquement des certificats auto-signés. Certains certificats dans Configuration Manager sont toujours auto-signés. Dans la plupart des cas, Configuration Manager gère automatiquement les certificats auto-signés, et vous n’avez rien à faire de plus. Le certificat de signature du serveur de site en est un exemple. Ce certificat est toujours auto-signé. Il garantit que les stratégies téléchargées par les clients à partir du point de gestion ont été envoyées depuis le serveur de site et qu’elles n’ont pas été falsifiées.  


### <a name="bkmk_plan-cng"></a> Certificats Cryptography: Next Generation (CNG)  

 Configuration Manager prend en charge les certificats Cryptography: Next Generation (CNG). Les clients Configuration Manager peuvent utiliser un certificat d’authentification client PKI avec une clé privée dans le fournisseur de stockage de clés (KSP) CNG. La prise en charge du KSP permet aux clients Configuration Manager de prendre en charge une clé privée matérielle, comme TPM KSP pour les certificats d’authentification client PKI. Pour plus d’informations, consultez [Vue d’ensemble des certificats CNG](/sccm/core/plan-design/network/cng-certificates-overview).


### <a name="bkmk_plan-ehttp"></a> HTTP amélioré  

 L’utilisation de la communication HTTPS est recommandée pour tous les chemins de communication de Configuration Manager, mais peut se révéler difficile pour certains clients en raison de la charge supplémentaire liée à la gestion des certificats PKI. L’intégration à Azure Active Directory (Azure AD) permet d’éviter une partie de ces exigences de certificat. Depuis la version 1806, vous pouvez activer l’utilisation de **HTTP amélioré** pour le site. Cette configuration prend en charge HTTPS sur les systèmes de site en utilisant une combinaison de certificats auto-signés et d’Azure AD. Elle ne nécessite pas d’infrastructure PKI. Pour plus d’informations, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).  


### <a name="bkmk_plan-cmgcdp"></a> Certificats pour la passerelle de gestion cloud (CMG) et pour le point de distribution cloud (CDP)

La gestion des clients sur Internet via la passerelle de gestion cloud (CMG) et le point de distribution cloud (CDP) nécessite l’utilisation de certificats. Le nombre et le type de certificats varie en fonction de vos scénarios spécifiques. Pour plus d’informations, consultez les articles suivants :
- [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)  
- [Certificat pour le point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_certs)  


### <a name="bkmk_plansitesign"></a> Planifier le certificat de signature du serveur de site (auto-signé)  

 Les clients peuvent obtenir en toute sécurité une copie du certificat de signature du serveur de site à partir des services de domaine Active Directory et à partir de l’installation Push du client. Si les clients ne peuvent pas obtenir une copie de ce certificat via un de ces mécanismes, installez-le quand vous installez le client. Ce processus est particulièrement important si la première communication du client avec le site s’effectue avec un point de gestion Internet. Comme ce serveur est connecté à un réseau non approuvé, il est plus vulnérable aux attaques. Si vous ne prenez pas cette mesure supplémentaire, les clients téléchargent automatiquement une copie du certificat de signature du serveur de site à partir du point de gestion.  

 Les clients ne peuvent pas obtenir une copie du certificat du serveur de site de façon sécurisée dans les scénarios suivants :  

 - Vous n’installez pas le client via l’installation Push du client et :  

    - Vous n’avez pas étendu le schéma Active Directory pour Configuration Manager.  

    - Vous n’avez pas publié le site du client sur les services de domaine Active Directory.  

    - Le client est issu d'une forêt non approuvée ou d'un groupe de travail.  

 - Vous utilisez la gestion des clients Internet et vous installez le client quand il est sur Internet.  

#### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Pour installer des clients ainsi qu'une copie du certificat de signature du serveur de site  

1.  Recherchez le certificat de signature du serveur de site sur le serveur de site principal. Le certificat est stocké dans le magasin de certificats Windows **SMS**. Il a le nom de sujet **Serveur de site** et le nom convivial **Certificat de signature de serveur de site**.  

2.  Exportez le certificat sans la clé privée, stockez le fichier à un emplacement sécurisé et accédez-y seulement via un canal sécurisé.  

3.  Installez le client avec la propriété client.msi suivante : `SMSSIGNCERT=<full path and file name>`  


###  <a name="BKMK_PlanningForCRLs"></a> Planifier la révocation de certificats PKI  

Quand vous utilisez des certificats PKI avec Configuration Manager, planifiez l’utilisation d’une liste de révocation des certificats. Les appareils utilisent la liste de révocation des certificats pour vérifier le certificat sur l’ordinateur qui se connecte. La liste de révocation des certificats est un fichier créé et signé par une autorité de certification. Il contient une liste de certificats émis par l’autorité de certification, mais qui ont été révoqués. Quand un administrateur de certificats révoque des certificats, son empreinte numérique est ajoutée à la liste de révocation des certificats. Cela se produit par exemple si un certificat émis est altéré ou suspecté de l’être.

> [!IMPORTANT]  
>  L’emplacement de la liste de révocation des certificats étant ajoutée à un certificat au moment de son émission par une autorité de certification, vous devez planifier la liste de révocation des certificats avant de déployer des certificats PKI utilisés par Configuration Manager.  

IIS vérifie toujours la liste de révocation des certificats pour les certificats clients. Cette configuration n’est pas modifiable dans Configuration Manager. Par défaut, les clients Configuration Manager vérifient toujours la liste de révocation des certificats pour les systèmes de site. Désactivez ce paramètre en spécifiant une propriété de site et une propriété CCMSetup.  

Les ordinateurs qui utilisent la vérification de la révocation des certificats, mais qui ne parviennent pas à localiser la liste de révocation des certificats, se comportent comme si tous les certificats de la chaîne de certification étaient révoqués. Ce comportement est dû au fait qu’ils ne peut pas vérifier si les certificats sont dans la liste de révocation des certificats. Dans ce scénario, toutes les connexions nécessitant des certificats et incluant la vérification de la liste de révocation de certificats échouent. Lorsque vous validez que votre liste de révocation de certificats est accessible via son emplacement http, il est important de noter que le client Configuration Manager s’exécute en tant que SYSTÈME LOCAL. Par conséquent, le test d’accessibilité de la liste de révocation de certificats avec un navigateur web s’exécutant sous le contexte l’utilisateur peut réussir, cependant le compte ordinateur peut être bloqué lorsque vous tentez d’établir une connexion http à la même URL CRL en raison de la solution de filtrage web interne. La mise sur liste verte de l’URL CRL dans les solutions de filtrage web peut être nécessaire dans ce cas.

La vérification de la liste de révocation des certificats chaque fois qu’un certificat est utilisé offre plus de sécurité que l’utilisation d’un certificat qui est révoqué, même si cela introduit un délai de connexion et un traitement supplémentaire sur le client. Votre organisation peut exiger cette vérification de sécurité supplémentaire pour les clients sur Internet ou sur un réseau non approuvé.  

Consultez vos administrateurs PKI avant de décider si les clients Configuration Manager doivent vérifier la liste de révocation des certificats. Vous pouvez alors envisager de laisser cette option activée dans Configuration Manager quand les deux conditions suivantes sont remplies :  

-   Votre infrastructure PKI prend en charge une liste de révocation des certificats, et cette liste est publiée à un emplacement accessible par tous les clients Configuration Manager. Ces clients peuvent inclure des appareils sur Internet et dans des forêts non approuvées.  

-   L’exigence de vérification de la liste de révocation des certificats pour chaque connexion à un système de site qui est configuré pour utiliser un certificat PKI a la priorité sur les spécifications suivantes :  
    - Des connexions plus rapides  
    - Un traitement efficace sur le client  
    - Le risque que des clients ne réussissent pas à se connecter à des serveurs si la CRL ne peut pas être localisée.  


###  <a name="BKMK_PlanningForRootCAs"></a> Planifier les certificats racine approuvés PKI et la liste des émetteurs de certificats  

Si vos systèmes de site IIS utilisent des certificats clients PKI pour l’authentification des clients sur HTTP, ou pour le chiffrement et l’authentification des clients sur HTTPS, il peut être nécessaire d’importer des certificats d’autorités de certification racine comme propriété de site. Voici les deux scénarios :  

-   Vous déployez des systèmes d’exploitation à l’aide de Configuration Manager, et les points de gestion acceptent uniquement les connexions de clients HTTPS.  

-   Vous utilisez des certificats clients PKI qui ne se lient pas à un certificat d’autorité de certification racine approuvé par les points de gestion.  

    > [!NOTE]  
    >  Quand vous émettez des certificats PKI clients à partir de la même hiérarchie d’autorités de certification que celle émettant les certificats de serveur que vous utilisez pour les points de gestion, il n’est pas nécessaire de spécifier ce certificat d’autorité de certification racine. Cependant, si vous utilisez plusieurs hiérarchies d’autorités de certification et que vous n’êtes pas certain qu’elles s’approuvent mutuellement, importez l’autorité de certification racine pour la hiérarchie d’autorités de certification des clients.  

Si vous devez importer des certificats d’autorité de certification racine pour Configuration Manager, exportez-les de l’autorité de certification émettrice ou de l’ordinateur client. Si vous exportez le certificat à partir de l’autorité de certification émettrice qui est également l’autorité de certification racine, veillez à ne pas exporter la clé privée. Stockez le fichier du certificat exporté dans un emplacement sécurisé pour empêcher toute falsification. Vous avez besoin d’un accès au fichier quand vous configurez le site. Si vous accédez au fichier sur le réseau, vérifiez que la communication est protégée contre la falsification en utilisant IPsec.  

Si un certificat d’autorité de certification racine que vous importez est renouvelé, vous devez l’importer.  

Ces certificats d’autorité de certification racine importés et le certificat d’autorité de certification racine de chaque point de gestion créent la liste des émetteurs de certificats que les ordinateurs Configuration Manager utilisent de la manière suivante :  

-   Quand un client se connecte à un point de gestion, le point de gestion vérifie que le certificat client est chaîné à un certificat racine approuvé dans la liste des émetteurs de certificats du site. Dans le cas contraire, le certificat est rejeté et la connexion PKI échoue.  

-   Quand des clients sélectionnent un certificat PKI et ont une liste des émetteurs de certificats, ils sélectionnent un certificat lié à un certificat racine approuvé dans la liste des émetteurs de certificats. En cas d’absence de correspondance, le client ne sélectionne pas de certificat PKI. Pour plus d’informations, consultez [Planifier la sélection des certificats clients PKI](#BKMK_PlanningForClientCertificateSelection).  


###  <a name="BKMK_PlanningForClientCertificateSelection"></a> Planifier la sélection des certificats clients PKI  

 Si vos systèmes de site IIS utilisent des certificats clients PKI pour l’authentification des clients sur HTTP, ou pour le chiffrement et l’authentification des clients sur HTTPS, planifiez la façon dont les clients Windows sélectionnent le certificat à utiliser pour Configuration Manager.  

> [!NOTE]  
>  Certains appareils ne prennent pas en charge une méthode de sélection de certificat. À la place, ils sélectionnent automatiquement le premier certificat qui répond aux exigences de certificat. C’est par exemple le cas des clients sur les ordinateurs et les appareils mobiles Mac.  

Dans de nombreux cas, la configuration et le comportement par défaut sont suffisants. Le client Configuration Manager sur les ordinateurs Windows filtre plusieurs certificats en appliquant les critères suivants, dans cet ordre :  

1.  La liste des émetteurs de certificats : le certificat est lié à une autorité de certification racine qui est approuvée par le point de gestion.  

2.  Le certificat se trouve dans le magasin de certificats par défaut de **Personnel**.  

3.  Le certificat est valide, non révoqué, et n'a pas expiré. Le contrôle de validité vérifie également que la clé privée est accessible.  

4.  Le certificat dispose d’une fonctionnalité d’authentification des clients ou il est émis pour le nom de l’ordinateur.  

5.  Le certificat possède la plus longue période de validité.  

Configurez les clients pour qu’ils utilisent la liste des émetteurs de certificats selon les mécanismes suivants :  

-   Publiez-le avec des informations de site Configuration Manager sur les services de domaine Active Directory.  

-   Installez les clients via l’installation Push du client.  

-   Les clients le téléchargent à partir du point de gestion après qu’ils sont correctement affectés à leur site.  

-   Spécifiez-le lors de l’installation du client comme propriété client.msi CCMSetup de CCMCERTISSUERS.  

Les clients qui n’ont pas la liste des émetteurs de certificats lors de leur installation initiale et qui ne sont pas encore affectés au site ignorent cette vérification. Quand des clients ont une liste d’émetteurs de certificats mais qu’ils n’ont pas de certificat PKI chaîné à un certificat racine approuvé de la liste des émetteurs de certificats, la sélection du certificat échoue. Les clients ne continuent pas avec les autres critères de sélection du certificat.  

Dans la plupart des cas, le client Configuration Manager identifie correctement un certificat PKI unique et approprié. Cependant, quand ce n’est pas le cas, au lieu de sélectionner le certificat avec la fonctionnalité d’authentification du client, vous pouvez configurer deux autres méthodes de sélection :  

- Une correspondance partielle des chaînes pour le nom du sujet du certificat client. Cette méthode utilise une correspondance qui ne respecte pas la casse. Elle est appropriée si vous utilisez le nom de domaine complet (FQDN) d’un ordinateur dans le champ Sujet et que vous voulez que la sélection du certificat soit basée sur le suffixe du domaine, par exemple **contoso.com**. Vous pouvez néanmoins utiliser cette méthode de sélection pour identifier une chaîne de caractères séquentiels dans le Nom du sujet du certificat qui différencie le certificat des autres dans le magasin de certificats du client.  

  > [!NOTE]
  >  Vous ne pouvez pas utiliser la correspondance partielle des chaînes avec l’autre nom du sujet comme paramètre de site. Même si vous pouvez spécifier une correspondance partielle des chaînes pour l’autre nom du sujet avec CCMSetup, il sera remplacé par les propriétés du site dans les scénarios suivants :  
  > 
  > - Les clients récupèrent les informations du site qui sont publiées sur les services de domaine Active Directory.  
  >   -   Les clients sont installés à l'aide de la poussée du client.  
  > 
  >   Utilisez une correspondance partielle des chaînes dans l’autre nom du sujet seulement quand vous installez manuellement les clients et qu’ils ne récupèrent pas les informations du site auprès des services de domaine Active Directory. Par exemple, ces conditions s’appliquent aux clients Internet uniquement.  

- Une correspondance pour les valeurs d’attribut du nom du sujet ou de l’autre nom du sujet du certificat client. Cette méthode utilise une correspondance qui respecte la casse. Elle est appropriée si vous utilisez un nom unique X500 ou des identificateurs d’objets équivalents (OID) conformément à la RFC 3280, et que vous voulez que la sélection du certificat soit basée sur les valeurs d’attribut. Vous pouvez spécifier uniquement les attributs et leurs valeurs s'ils doivent identifier de manière unique ou valider le certificat et le différencier des autres certificats du magasin de certificats.  

Le tableau suivant indique les valeurs d’attribut que Configuration Manager prend en charge pour les critères de sélection de certificat.  

|Attribut d'OID|Attribut de nom unique|Définition de l'attribut|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Composant de domaine|  
|1.2.840.113549.1.9.1|E ou E-mail|Adresse de messagerie|  
|2.5.4.3|CN|Nom commun|  
|2.5.4.4|SN|Nom d'objet|  
|2.5.4.5|SERIALNUMBER|Numéro de série|  
|2.5.4.6|C|Code du pays|  
|2.5.4.7|L|Localité|  
|2.5.4.8|S ou ST|Nom de département/province|  
|2.5.4.9|STREET|Adresse|  
|2.5.4.10|O|Nom de l'organisation|  
|2.5.4.11|OU|Unité d'organisation|  
|2.5.4.12|T ou Title|Titre|  
|2.5.4.42|G ou GN ou GivenName|Prénom|  
|2.5.4.43|I ou Initials|Initiales|  
|2.5.29.17|(aucune valeur)|Autre nom de l'objet|  

Si plusieurs certificats appropriés sont détectés après l’application des critères de sélection, vous pouvez remplacer la configuration par défaut pour sélectionner le certificat ayant la plus longue période de validité et spécifier, au contraire, qu’aucun certificat n’est sélectionné. Dans ce scénario, le client ne peut pas communiquer avec des systèmes de site IIS avec un certificat PKI. Le client transmet un message d’erreur au point d’état de secours qui lui est attribué pour vous prévenir de l’échec de sélection du certificat et vous permettre de modifier ou d’affiner vos critères de sélection de certificat. Le comportement du client dépend ensuite de l'emplacement de la connexion qui a échoué, à savoir sur HTTPS ou HTTP :  

-   Si la connexion qui a échoué était établie via HTTPS : le client tente d’établir une connexion sur HTTP et utilise le certificat de client auto-signé.  

-   Si la connexion qui a échoué était établie via HTTP : le client tente d’établir une autre connexion sur HTTP à l’aide du certificat de client auto-signé.  

Pour identifier facilement un certificat de client unique PKI, vous pouvez également spécifier un magasin personnalisé autre que le magasin par défaut **Personnel** dans **Ordinateur**. Cependant, vous devez créer ce magasin indépendamment de Configuration Manager. Vous devez être en mesure de déployer des certificats sur ce magasin personnalisé et de les renouveler avant l’expiration de la période de validité.  

Pour plus d’informations, consultez [Configurer les paramètres pour les certificats PKI clients](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  


###  <a name="BKMK_PlanningForPKITransition"></a> Planifier une stratégie de transition pour les certificats PKI et la gestion des clients basée sur Internet  

Grâce aux options de configuration flexibles de Configuration Manager, vous pouvez effectuer progressivement la transition des clients et du site pour utiliser des certificats PKI et sécuriser ainsi davantage les points de terminaison des clients. Les certificats PKI offrent une meilleure sécurité et vous permettent de gérer les clients Internet.  

En raison du grand nombre d’options et de choix de configuration dans Configuration Manager, il n’existe pas de méthode unique recommandée pour effectuer la transition d’un site afin que tous les clients utilisent des connexions HTTPS. Toutefois, vous pouvez suivre ces étapes comme guide :  

1. Installez le site Configuration Manager et configurez-le de sorte que les systèmes de site acceptent les connexions client via HTTP et HTTPS.  

2. Dans les propriétés du site, sous l’onglet **Communication de l’ordinateur client**, définissez **Paramètres du système de site** sur **HTTP ou HTTPS** et sélectionnez **Utiliser le certificat client PKI (fonctionnalité d’authentification du client) lorsqu’il est disponible**.  Pour plus d’informations, consultez [Configurer les paramètres pour les certificats PKI clients](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureClientPKI).  

3. Pilotez un déploiement PKI pour les certificats clients. Pour obtenir un exemple de déploiement, consultez [Déployer le certificat client pour les ordinateurs Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).  

4. Installez des clients à l'aide de la méthode d'installation poussée du client. Pour plus d’informations, consultez [Comment installer des clients Configuration Manager avec l’installation Push du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  

5. Surveillez le déploiement et l’état des clients à l’aide des rapports et des informations affichés dans la console Configuration Manager.  

6. Déterminez combien de clients utilisent un certificat client PKI en affichant la colonne **Certificat client** dans l'espace de travail **Ressources et conformité**, nœud **Appareils**.  

    Vous pouvez également déployer l’outil d’évaluation de Configuration Manager pour HTTPS (**cmHttpsReadiness.exe**) sur les ordinateurs. Utilisez ensuite les rapports pour voir combien d’ordinateurs peuvent utiliser un certificat PKI client avec Configuration Manager.  

   > [!NOTE]
   >  Quand vous installez le client Configuration Manager, l’outil **CMHttpsReadiness.exe** est installé dans le dossier `%windir%\CCM`. Les options de ligne de commande suivantes sont disponibles pour l’exécution de cet outil :  
   > 
   > - `/Store:<name>` : cette option est identique à la propriété client.msi **CCMCERTSTORE**  
   > - `/Issuers:<list>` : cette option est identique à la propriété client.msi **CCMCERTISSUERS**    
   > - `/Criteria:<criteria>` : cette option est identique à la propriété client.msi **CCMCERTSEL**    
   > - `/SelectFirstCert` : cette option est identique à la propriété client.msi **CCMFIRSTCERT**    
   > 
   >   Pour plus d’informations, consultez [À propos des propriétés d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).  

7. Quand vous êtes certain que suffisamment de clients utilisent leur certificat client PKI pour l’authentification sur HTTP, effectuez ces étapes :  

   1.  Déployez un certificat de serveur web PKI sur un serveur de membre qui exécute un point de gestion supplémentaire pour le site et configurez ce certificat dans IIS. Pour plus d’informations, consultez [Déployer le certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

   2.  Installez le rôle de point de gestion sur ce serveur et configurez l'option **Connexions clients** dans les propriétés du point de gestion pour **HTTPS**.  

8. Contrôlez et vérifiez que les clients qui possèdent un certificat PKI utilisent le nouveau point de gestion à l'aide du protocole HTTPS. Pour vérifier cela, vous pouvez utiliser la journalisation ou les compteurs de performance d’IIS.  

9. Reconfigurez d'autres rôles de système de site pour utiliser les connexions de clients HTTPS. Si vous voulez gérer les clients sur Internet, vérifiez que les systèmes de site ont un nom de domaine complet Internet. Configurez des points de gestion et des points de distribution individuels pour accepter les connexions clientes depuis Internet.  

    > [!IMPORTANT]  
    >  Avant de définir des rôles de système de site pour accepter les connexions à partir d’Internet, consultez les informations de planification et les prérequis pour la gestion de clients Internet. Pour plus d’informations, consultez [Communications entre les points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

10. Étendez le lancement des certificats PKI pour les clients et pour les systèmes de site qui exécutent IIS. Configurez les rôles de système de site pour les connexions clientes et les connexions Internet HTTPS, selon les besoins.  

11. Pour une sécurité maximale : lorsque vous êtes certain que tous les clients utilisent un certificat client PKI pour l’authentification et le chiffrement, modifiez les propriétés de site pour utiliser HTTPS uniquement.  

    Ce plan introduit d’abord des certificats PKI seulement pour l’authentification sur HTTP, puis pour l’authentification et chiffrement sur HTTPS. Quand vous suivez ce plan pour introduire progressivement ces certificats, vous réduisez le risque que les clients ne soient plus gérés. Vous bénéficiez aussi de la sécurité maximale prise en charge par Configuration Manager.  

##  <a name="BKMK_PlanningForRTK"></a> Planifier la clé racine approuvée  

 La clé racine approuvée de Configuration Manager fournit aux clients Configuration Manager un mécanisme pour vérifier que les systèmes de site appartiennent à leur hiérarchie. Chaque serveur de site génère une clé d'échange de site pour communiquer avec d'autres sites. La clé d'échange du site de niveau supérieur dans la hiérarchie est appelée clé racine approuvée.  

 La fonction de la clé racine approuvée dans Configuration Manager ressemble à un certificat racine dans une infrastructure à clé publique. Tout ce qui est signé par la clé privée de la clé racine approuvée est également approuvé plus bas dans la hiérarchie. Les clients stockent une copie de la clé racine approuvée du site dans l’espace de noms WMI **root\ccm\locationservices**. 

 Par exemple, le site émet un certificat pour le point de gestion, qu’il signe avec la clé privée de la clé racine approuvée. Le site partage avec les clients la clé publique de sa clé racine approuvée. Les clients peuvent alors faire la différence entre les points de gestion qui se trouvent dans leur hiérarchie et ceux qui ne s’y trouvent pas.   

 Les clients récupèrent automatiquement la copie publique de la clé racine approuvée selon deux mécanismes :  

- Étendez le schéma Active Directory pour Configuration Manager et publiez les sites sur les services de domaine Active Directory. Ensuite, les clients récupèrent ces informations de site à partir d’un serveur de catalogue global. Pour plus d’informations, consultez [Préparer Active Directory pour la publication de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

- Quand vous installez des clients avec la méthode d’installation Push du client. Pour plus d’informations, consultez [Installation Push du client](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).  

  Si les clients ne peuvent pas récupérer la clé racine approuvée en utilisant un de ces mécanismes, ils font confiance à la clé racine approuvée qui est fournie par le premier point de gestion avec lequel ils communiquent. Dans ce scénario, un client peut être redirigé vers le point de gestion d’un pirate informatique où il recevrait la stratégie à partir du point de gestion non autorisé. Cette action nécessite que l’attaquant soit chevronné. Cette attaque est limitée au court délai avant que le client récupère la clé racine approuvée auprès d’un point de gestion valide. Pour réduire le risque d’un attaquant redirigeant de façon trompeuse les clients vers un point de gestion factice, préprovisionnez la clé racine approuvée sur les clients.  

  Pour préconfigurer et vérifier la clé racine approuvée pour un client Configuration Manager, procédez comme suit :  

- [Préprovisionner la clé racine approuvée sur un client avec un fichier](#bkmk_trk-provision-file)  

- [Préprovisionner la clé racine approuvée sur un client sans utiliser de fichier](#bkmk_trk-provision-nofile)  

- [Vérifier la clé racine approuvée sur un client](#bkmk_trk-verify)  

- [Supprimer ou remplacer la clé racine approuvée](#bkmk_trk-reset)  

  > [!NOTE]  
  > Si les clients peuvent obtenir la clé racine approuvée auprès des services de domaine Active Directory ou via un envoi (push) client, vous ne devez pas la préprovisionner. 
  > 
  > Quand les clients utilisent une communication HTTPS vers les points de gestion, vous ne devez pas préprovisionner la clé racine approuvée. Ils établissent une relation de confiance via les certificats PKI.  


### <a name="bkmk_trk-provision-file"></a> Préprovisionner la clé racine approuvée sur un client avec un fichier  

1.  Sur le serveur de site, ouvrez le fichier suivant dans un éditeur de texte : `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Recherchez l’entrée **SMSPublicRootKey=**. Copiez la clé depuis cette ligne et fermez le fichier sans effectuer aucune modification.  

3.  Créez un fichier texte, puis collez dans ce nouveau fichier les informations de clé que vous avez copiées à partir du fichier mobileclient.tcf.  

4.  Enregistrez le fichier à un emplacement accessible à tous les ordinateurs, mais où le fichier ne peut pas être falsifié.  

5.  Installez le client avec une méthode d’installation qui accepte les propriétés client.msi. Spécifiez la propriété suivante : `SMSROOTKEYPATH=<full path and file name>`  

    > [!IMPORTANT]  
    >  Quand vous spécifiez la clé racine approuvée lors de l’installation du client, spécifiez également le code de site. Utilisez la propriété client.msi suivante : `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-provision-nofile"></a> Préprovisionner la clé racine approuvée sur un client sans utiliser de fichier  

1.  Sur le serveur de site, ouvrez le fichier suivant dans un éditeur de texte : `<Configuration Manager install directory>\bin\mobileclient.tcf`  

2.  Recherchez l’entrée **SMSPublicRootKey=**. Copiez la clé depuis cette ligne et fermez le fichier sans effectuer aucune modification.  

3.  Installez le client avec une méthode d’installation qui accepte les propriétés client.msi. Spécifiez la propriété client.msi suivante : `SMSPublicRootKey=<key>`, où `<key>` est la chaîne que vous avez copiée depuis mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quand vous spécifiez la clé racine approuvée lors de l’installation du client, spécifiez également le code de site. Utilisez la propriété client.msi suivante : `SMSSITECODE=<site code>`   


### <a name="bkmk_trk-verify"></a> Vérifier la clé racine approuvée sur un client  

1. Ouvrez une console Windows PowerShell en tant qu’administrateur.  

2. Exécutez la commande suivante :  

``` PowerShell
 (Get-WmiObject -Namespace root\ccm\locationservices -Class TrustedRootKey).TrustedRootKey
```

La chaîne retournée est la clé racine approuvée. Vérifiez qu’elle correspond à la valeur de **SMSPublicRootKey** dans le fichier mobileclient.tcf sur le serveur de site.  


### <a name="bkmk_trk-reset"></a> Supprimer ou remplacer la clé racine approuvée  

 Supprimez la clé racine approuvée d’un client en utilisant la propriété client.msi **RESETKEYINFORMATION = TRUE**. 

 Pour remplacer la clé racine approuvée, réinstallez le client avec la nouvelle clé racine approuvée. Par exemple, utilisez l’installation Push du client, ou spécifiez la propriété client.msi **SMSPublicRootKey**.  

 Pour plus d’informations sur ces propriétés d’installation, consultez [À propos des paramètres et des propriétés d’installation des clients](/sccm/core/clients/deploy/about-client-installation-properties).



##  <a name="BKMK_PlanningForSigningEncryption"></a> Planifier la signature et le chiffrement  
 
 Quand vous utilisez des certificats PKI pour toutes les communications clientes, vous n’avez pas à planifier la signature et le chiffrement pour contribuer à sécuriser les communications de données des clients. Si vous installez des systèmes de site qui exécutent IIS pour autoriser les connexions clientes HTTP, décidez comment sécuriser la communication des clients pour le site.  

 Pour protéger les données que les clients envoient aux points de gestion, vous pouvez exiger que les clients signent les données. Vous pouvez également exiger l’algorithme SHA-256 pour la signature. Cette configuration est plus sécurisée, mais elle n’exige pas SHA-256, sauf si tous les clients la prennent en charge. De nombreux systèmes d’exploitation offrent une prise en charge native de cet algorithme , mais les systèmes d’exploitation plus anciens peuvent nécessiter une mise à jour ou un correctif logiciel. 

 Alors que la signature contribue à protéger les données de la falsification, le chiffrement permet de les protéger contre la divulgation d’informations. Vous pouvez activer le chiffrement 3DES pour les données d'inventaire et les messages d'état que les clients envoient aux points de gestion dans le site. Vous n’avez pas à installer des mises à jour sur les clients pour prendre en charge cette option. Les clients et les points de gestion nécessitent une utilisation supplémentaire de l’UC pour le chiffrement et le déchiffrement.  

 Pour plus d’informations sur la configuration des paramètres pour la signature et le chiffrement, consultez [Configurer la signature et le chiffrement](/sccm/core/plan-design/security/configure-security#BKMK_ConfigureSigningEncryption).  



##  <a name="BKMK_PlanningForRBA"></a> Planifier l’administration basée sur des rôles  

 Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).  



## <a name="bkmk_planazuread"></a> Planifier Azure Active Directory

 Configuration Manager s’intègre à Azure Active Directory (Azure AD) pour permettre au site et aux clients d’utiliser l’authentification moderne. L’intégration de votre site à Azure AD prend en charge les scénarios Configuration Manager suivants :

**Client**  

- [Gérer les clients sur Internet via la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

- [Gérer les appareils joints au domaine cloud](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

- [Cogestion](/sccm/comanage/overview)  

- [Déployer des applications disponibles pour les utilisateurs](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)  

- [Applications en ligne Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

- Réduisez les exigences en matière d’infrastructure. Par exemple, le [Centre logiciel utilisant le point de gestion](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex) au lieu du catalogue d’applications  

- [Gérer les applications Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates)  


**Serveur**  

- [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness)  

- [Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics)  

- [Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  

- [Hub Communauté](/sccm/core/get-started/capabilities-in-technical-preview-1807#bkmk_hub)  

- [Point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- [Découverte d’utilisateur](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  


 Pour plus d’informations sur la connexion de votre site à Azure AD, consultez [Configurer les services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).


 Pour plus d’informations sur Azure AD, consultez la [documentation d’Azure Active Directory](https://docs.microsoft.com/azure/active-directory/).



## <a name="bkmk_auth"></a> Planifier l’authentification du fournisseur SMS
<!--1357013--> 

Depuis la version 1810, vous pouvez spécifier le niveau d’authentification minimal pour les administrateurs qui accèdent aux sites Configuration Manager. Cette fonctionnalité force les administrateurs à se connecter à Windows avec le niveau requis. Cela s’applique à tous les composants qui accèdent au fournisseur SMS. Par exemple, la console Configuration Manager, les méthodes SDK et les cmdlets Windows PowerShell. 

Cette configuration est un paramètre à l’échelle de la hiérarchie. Avant de modifier ce paramètre, assurez-vous que tous les administrateurs Configuration Manager peuvent se connecter à Windows avec le niveau d’authentification requis. 

Les niveaux ci-dessous sont disponibles :

- **Authentification Windows** : exige une authentification avec les informations d’identification du domaine Active Directory.   

- **Authentification par certificat** : exige l’authentification avec un certificat valide émis par une autorité de certification PKI approuvée.  

- **Authentification Windows Hello Entreprise** : exige une authentification forte à deux facteurs liée à un appareil et utilisant la biométrie ou un code PIN.  

Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). 



## <a name="see-also"></a>Voir aussi
- [Sécurité et confidentialité pour les clients Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurer la sécurité](/sccm/core/plan-design/security/configure-security)  

- [Communications entre points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Informations techniques de référence sur les contrôles de chiffrement](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  

