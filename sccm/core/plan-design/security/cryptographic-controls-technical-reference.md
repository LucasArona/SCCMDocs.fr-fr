---
title: Informations techniques de référence sur les contrôles de chiffrement
titleSuffix: Configuration Manager
description: Découvrez de quelle manière la signature et le chiffrement permettent d’empêcher les tentatives malveillantes de lecture des données dans System Center Configuration Manager.
ms.date: 12/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6d25c6a11821b73f34c8a3cd6aa95d4a78c86587
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418393"
---
# <a name="cryptographic-controls-technical-reference"></a>Informations techniques de référence sur les contrôles de chiffrement

*S’applique à : System Center Configuration Manager (Current Branch)*


System Center Configuration Manager utilise la signature et le chiffrement pour sécuriser la gestion des appareils dans la hiérarchie Configuration Manager. La signature permet d’ignorer les données qui ont été modifiées lors du transit. Le chiffrement permet d’empêcher une personne malveillante de lire les données à l’aide d’un analyseur de protocole réseau.  

 L’algorithme de hachage principal utilisé par Configuration Manager pour la signature est SHA-256. Quand deux sites Configuration Manager communiquent entre eux, ils signent leurs communications avec l’algorithme SHA-256. L’algorithme de chiffrement principal implémenté dans Configuration Manager est 3DES. Il est utilisé pour le stockage des données dans la base de données Configuration Manager et pour les communications client HTTP. Lorsque vous utilisez les communications clientes sur HTTPS, vous pouvez configurer votre infrastructure à clé publique (PKI) pour utiliser les certificats RSA avec les longueurs de clé et les algorithmes de hachage maximaux documentées dans [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Pour la plupart des opérations de chiffrement pour les systèmes d’exploitation Windows, Configuration Manager utilise les algorithmes SHA-2, 3DES et AES ainsi que les algorithmes RSA de la bibliothèque CryptoAPI de Windows, rsaenh.dll.  

> [!IMPORTANT]  
>  Pour plus d’informations sur les modifications recommandées en réponse aux vulnérabilités SSL, consultez la rubrique [Vulnérabilités du protocole SSL](#about-ssl-vulnerabilities).  

##  <a name="cryptographic-controls-for-configuration-manager-operations"></a>Contrôles de chiffrement pour les opérations dans Configuration Manager  
 Les informations dans Configuration Manager peuvent être signées et chiffrées, que vous utilisiez ou non des certificats PKI avec Configuration Manager.  

### <a name="policy-signing-and-encryption"></a>Signature et chiffrement de stratégie  
 Les affectations de stratégies client sont signées par le certificat de signature du serveur de site auto-signé afin d'éviter qu'un point de gestion compromis envoie des stratégies qui ont été falsifiées, ce qui présenterait un risque de sécurité. Cela est important si vous utilisez la gestion du client basée sur Internet, car cet environnement nécessite un point de gestion exposé aux communications sur Internet.  

 La stratégie est chiffrée à l’aide de l’algorithme 3DES quand elle contient des données sensibles. Une stratégie qui contient des données sensibles est envoyée aux clients autorisés uniquement. Une stratégie qui ne contient pas de données sensibles n'est pas chiffrée.  

 Quand la stratégie est stockée sur les clients, elle est chiffrée à l’aide d’une interface de programmation d’applications de protection des données (DPAPI).  

### <a name="policy-hashing"></a>Hachage de stratégie  
 Quand les clients Configuration Manager demandent une stratégie, ils obtiennent d’abord une attribution de stratégie pour connaître les stratégies qui leur sont applicables. Par la suite, ils demandent uniquement le corps de ces stratégies. Chaque attribution de stratégie contient le hachage calculé pour le corps de la stratégie correspondante. Le client récupère les corps des stratégies applicables, puis il calcule le hachage de ce corps. Si le hachage du corps de la stratégie téléchargée ne correspond pas à celui de l'attribution de la stratégie, le client annule le corps de la stratégie.  

 L'algorithme de hachage pour la stratégie est SHA-1 et SHA-256.  

### <a name="content-hashing"></a>Hachage du contenu  
 Le service du Gestionnaire de distributions sur le serveur de site hache les fichiers de tous les packages. Le fournisseur de stratégie inclut le hachage dans la stratégie de distribution de logiciels. Quand le client Configuration Manager télécharge le contenu, il régénère le hachage localement et le compare à celui fourni dans la stratégie. Si les hachages correspondent, le contenu n'est pas été altéré et le client installe le logiciel. Si un seul octet du contenu a été altéré, les hachages ne correspondront pas et le logiciel ne sera pas installé. Cette vérification permet de s'assurer que le logiciel correct est installé, car son contenu réel fait l'objet d'une contre-vérification avec la stratégie.  

 L'algorithme de hachage par défaut pour le contenu est SHA-256. Pour modifier ce paramètre par défaut, consultez la documentation du SDK Configuration Manager.  

 Tous les appareils ne prennent pas en charge le hachage du contenu. C’est notamment le cas des appareils suivants :  

-   Clients Windows diffusant du contenu App-V.  

-   Clients Windows Phone. Ces clients vérifient la signature d’une application signée par une source approuvée.  

-   Clients Windows RT. Ces clients vérifient la signature d’une application signée par une source approuvée et utilisent également la validation du nom complet du package.  

-   Appareils iOS. Ces appareils vérifient la signature d’une application signée par un certificat de développeur issu d’une source approuvée.  

-   Clients Nokia. Ces clients vérifient la signature d’une application qui utilise un certificat auto-signé. ou la signature d'un certificat issu d'une source approuvée, pour que le certificat puisse signer les applications Nokia Symbian Installation Source (SIS).  

-   Android. En outre, ces appareils n'utilisent pas la validation de signature pour l'installation des applications.  

-   Clients qui s'exécutent sur des versions de Linux et UNIX qui ne prennent pas en charge SHA-256. Pour plus d’informations, consultez [Planification du déploiement du client sur des ordinateurs Linux et UNIX](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers).  

### <a name="inventory-signing-and-encryption"></a>Signature et chiffrement d’inventaire  
 L'inventaire que les clients envoient aux points de gestion est toujours signé par les appareils, qu'ils communiquent ou non avec les points de gestion via HTTP ou HTTPS. S'ils utilisent le protocole HTTP, vous pouvez choisir de chiffrer ces données, ce qui constitue une meilleure pratique de sécurité.  

### <a name="state-migration-encryption"></a>Chiffrement de la migration d’état  
 Les données stockées sur les points de migration d'état pour le déploiement de système d'exploitation sont toujours chiffrées par l'Outil de migration utilisateur (USMT) en utilisant l'algorithme 3DES.  

### <a name="encryption-for-multicast-packages-to-deploy-operating-systems"></a>Chiffrement des packages de multidiffusion pour déployer des systèmes d’exploitation  
 Pour chaque package de déploiement de système d'exploitation, vous pouvez activer le chiffrement lorsque le package est transféré vers des ordinateurs à l'aide de la multidiffusion. Le chiffrement utilise la norme AES (Advanced Encryption Standard). Si vous activez le chiffrement, aucune configuration de certificat supplémentaire n'est nécessaire. Le point de distribution multidiffusion génère automatiquement des clés symétriques pour le chiffrement du package. Chaque package possède une clé de chiffrement qui lui est propre. La clé est stockée sur le point de distribution multidiffusion à l'aide des API Windows standard. Lorsque le client se connecte à la session de multidiffusion, l'échange de clé se produit sur un canal chiffré, soit avec le certificat d'authentification de client émis par l'infrastructure à clé publique (lorsque le client utilise le protocole HTTPS), soit avec le certificat auto-signé (lorsque le client utilise le protocole HTTP). Le client stocke la clé en mémoire uniquement pendant la durée d'ouverture de la session de multidiffusion.  

### <a name="encryption-for-media-to-deploy-operating-systems"></a>Chiffrement du support pour déployer des systèmes d’exploitation  
 Lorsque vous utilisez un support pour déployer des systèmes d'exploitation et spécifier un mot de passe pour protéger le support, les variables d'environnement sont chiffrées à l'aide de la norme AES (Advanced Encryption Standard). Les autres données sur le support, y compris les packages et le contenu pour les applications, ne sont pas chiffrées.  

### <a name="encryption-for-content-that-is-hosted-on-cloud-based-distribution-points"></a>Chiffrement du contenu hébergé sur des points de distribution cloud  
 Depuis System Center 2012 Configuration Manager SP1, quand vous chargez du contenu vers des points de distribution cloud, le contenu est chiffré à l’aide de l’algorithme AES (Advanced Encryption Standard) avec une clé de 256 bits. Le contenu est de nouveau chiffré à chaque fois que vous le mettez à jour. Lorsque des clients téléchargent le contenu, celui-ci est chiffré et protégé par la connexion HTTPS.  

### <a name="signing-in-software-updates"></a>Signature dans les mises à jour logicielles  
 Toutes les mises à jour logicielles doivent être signées par un éditeur approuvé pour les protéger contre les altérations. Sur les ordinateurs clients, l'Agent Windows Update (WUA) analyse les mises à jour du catalogue, mais n'installe pas la mise à jour s'il ne parvient pas à localiser le certificat numérique dans le magasin des éditeurs approuvés, sur l'ordinateur local. Si un certificat auto-signé a été utilisé pour la publication du catalogue de mises à jour, comme par exemple des éditeurs WSUS auto-signés, le certificat doit également se trouver dans le magasin de certificats des autorités de certification racine approuvées, sur l'ordinateur local, pour vérifier la validité du certificat. WUA vérifie également si le paramètre **Autoriser le contenu signé de la stratégie de groupe d'emplacement des services de mise à jour Microsoft sur l'intranet** est activé sur l'ordinateur local. Ce paramètre de stratégie doit être activé pour que WUA analyse les mises à jour qui ont été créées et publiées à l'aide de l'éditeur de mises à jour.  

 Lorsque les mises à jour logicielles sont publiées dans l'éditeur de mises à jour System Center, un certificat numérique signe les mises à jour logicielles quand elles sont publiées sur un serveur de mise à jour. Vous pouvez soit spécifier un certificat PKI, soit laisser l'éditeur de mises à jour générer un certificat auto-signé pour signer la mise à jour logicielle.  

### <a name="signed-configuration-data-for-compliance-settings"></a>Données de configuration signées pour les paramètres de compatibilité  
 Quand vous importez des données de configuration, Configuration Manager vérifie la signature numérique du fichier. Si les fichiers n'ont pas été signés, ou si la vérification de la signature numérique échoue, vous recevrez un avertissement et serez invité à continuer l'importation. Ne poursuivez l'importation des données de configuration que si vous faites explicitement confiance à l'éditeur et si vous êtes certain de l'intégrité des fichiers.  

### <a name="encryption-and-hashing-for-client-notification"></a>Chiffrement et hachage pour la notification du client  
 Si vous utilisez la notification du client, toutes les communications utilisent le protocole TLS et le niveau de chiffrement le plus élevé que le serveur et les systèmes d'exploitation clients peuvent négocier. Par exemple, un ordinateur client exécutant Windows 7 et un point de gestion exécutant Windows Server 2008 R2 peuvent prendre en charge le chiffrement AES 128 bits, tandis qu’un ordinateur client exécutant Vista et communiquant avec le même point de gestion négociera seulement un chiffrement 3DES. La même négociation se produit lors du hachage des paquets transférés lors de la notification du client, qui utilise l'algorithme SHA-1 ou SHA-2.  

##  <a name="certificates-used-by-configuration-manager"></a>Certificats utilisés par Configuration Manager  
 Pour obtenir la liste des certificats d’infrastructure à clé publique (PKI) pris en charge par Configuration Manager, connaître les exigences ou limitations particulières et savoir comment utiliser les certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Cette liste inclut les longueurs de clé et les algorithmes de hachage pris en charge. La plupart des certificats prennent en charge l'algorithme SHA-256 et la longueur de clé 2 048 bits.  

> [!NOTE]  
>  Le nom d’objet ou l’autre nom d’objet des certificats utilisés par Configuration Manager doit contenir uniquement des caractères codés sur un octet.  

 Les certificats PKI sont requis pour les scénarios suivants :  

- Quand vous gérez des clients Configuration Manager sur Internet.  

- Quand vous gérez des clients Configuration Manager sur des appareils mobiles.  

- Lorsque vous gérez des ordinateurs Mac.  

- Lorsque vous utilisez des points de distribution cloud.  

- Lorsque vous gérez des ordinateurs Intel AMT hors bande.  

  Pour la plupart des autres communications Configuration Manager nécessitant des certificats pour l’authentification, la signature ou le chiffrement, Configuration Manager utilise automatiquement les certificats PKI disponibles. S’il n’y a pas de certificats PKI disponibles, Configuration Manager génère des certificats auto-signés.  

  Configuration Manager n’utilise pas de certificats PKI quand il gère des appareils mobiles à l’aide du connecteur Exchange Server.  

### <a name="mobile-device-management-and-pki-certificates"></a>Gestion d’appareils mobiles et certificats PKI  
 Si l’appareil mobile n’a pas été verrouillé par l’opérateur mobile, vous pouvez utiliser Configuration Manager ou Microsoft Intune pour demander et installer un certificat client. Ce certificat fournit une authentification mutuelle entre le client de l’appareil mobile et les systèmes de site Configuration Manager ou les services Microsoft Intune. Si l’appareil mobile est verrouillé, vous ne pouvez pas utiliser Configuration Manager ou Intune pour déployer des certificats.  

 Si vous activez l’inventaire matériel des appareils mobiles, Configuration Manager ou Intune effectue également l’inventaire des certificats installés sur l’appareil mobile.   

### <a name="operating-system-deployment-and-pki-certificates"></a>Déploiement de systèmes d’exploitation et certificats PKI  
 Quand vous utilisez Configuration Manager pour déployer des systèmes d’exploitation et un point de gestion qui nécessite des connexions client HTTPS, l’ordinateur client a également besoin d’un certificat pour communiquer avec ce point de gestion, même s’il se trouve dans une phase de transition (démarrage depuis le média de séquence de tâches ou un point de distribution PXE, par exemple). Pour la prise en charge de ce scénario, vous devez créer un certificat d’authentification client PKI, l’exporter avec la clé privée, puis l’importer dans les propriétés du serveur de site. Ajoutez également le certificat d’autorité de certification racine approuvée du point de gestion.  

 Si vous créez un média de démarrage, vous importez le certificat d'authentification du client lors de la création du média de démarrage. Configurez un mot de passe sur le support de démarrage pour protéger la clé privée et les autres données sensibles configurées dans la séquence de tâches. Chaque ordinateur qui démarre depuis le support de démarrage présentera le même certificat au point de gestion que celui requis pour les fonctions de clients telles que la demande de stratégies client.  

 Si vous utilisez le démarrage PXE, vous importez le certificat d'authentification du client vers le point de distribution PXE, et il utilise le même certificat pour tous les clients démarrant à partir de ce point de distribution PXE. Une meilleure pratique de sécurité exige que les utilisateurs qui connectent leurs ordinateurs à un service PXE fournissent un mot de passe dans le but de protéger la clé privée et d'autres données sensibles dans les séquences de tâches.  

 Si l'un de ces certificats d'authentification client est compromis, bloquez les certificats dans le nœud **Certificats** de l'espace de travail **Administration** , nœud **Sécurité** . Pour gérer ces certificats, vous devez disposer du droit **Gérer un certificat de déploiement de système d'exploitation** .  

 Une fois le système d’exploitation déployé et Configuration Manager installé, le client a besoin de son propre certificat d’authentification client PKI pour les communications client HTTPS.  

### <a name="isv-proxy-solutions-and-pki-certificates"></a>Solutions proxy ISV et certificats PKI  
 Les éditeurs de logiciels indépendants (ISV) peuvent créer des applications qui étendent les fonctionnalités de Configuration Manager. Par exemple, un éditeur de logiciels indépendant peut créer des extensions pour la prise en charge de plates-formes clientes autres que Windows, comme les ordinateurs Macintosh ou UNIX. Toutefois, si les systèmes de site nécessitent des connexions clientes HTTPS, ces clients doivent également utiliser des certificats PKI pour communiquer avec le site. Dans Configuration Manager, vous pouvez attribuer un certificat au proxy ISV qui autorise les communications entre les clients de proxy ISV et le point de gestion. Si vous utilisez des extensions qui nécessitent des certificats de proxy ISV, consultez la documentation de ce produit. Pour plus d’informations sur la création de certificats proxy ISV, consultez le SDK Configuration Manager.  

 Si le certificat ISV est compromis, bloquez le certificat dans le nœud **Certificats** de l'espace de travail **Administration** , nœud **Sécurité** .  

### <a name="asset-intelligence-and-certificates"></a>Asset Intelligence et certificats  
 Configuration Manager s’installe avec un certificat X.509 que le point de synchronisation Asset Intelligence utilise pour se connecter à Microsoft. Configuration Manager utilise ce certificat pour demander un certificat d’authentification client au service de certificats Microsoft. Le certificat d'authentification du client est installé sur le serveur du système de site du point de synchronisation Asset Intelligence. Il est utilisé pour authentifier le serveur auprès de Microsoft. Configuration Manager utilise le certificat d'authentification client pour télécharger le catalogue Asset Intelligence et télécharger des logiciels.  

 La longueur de clé de ce certificat est de 1024 bits.  

### <a name="cloud-based-distribution-points-and-certificates"></a>Points de distribution cloud et certificats  
 Depuis System Center 2012 Configuration Manager SP1, les points de distribution cloud nécessitent un certificat de gestion (auto-signé ou PKI) que vous chargez vers Microsoft Azure. Ce certificat de gestion nécessite une fonctionnalité d'authentification du serveur et une longueur de clé de certificat de 2 048 bits. En outre, vous devez configurer un certificat de service pour chaque point de distribution cloud. Il ne peut pas être auto-signé, mais il doit également disposer d'une fonctionnalité d'authentification du serveur et d'une clé de certificat de 2 048 bits.  

> [!NOTE]  
>  Le certificat de gestion auto-signé sert uniquement aux tests et n'est pas destiné à être utilisé sur des réseaux de production.  

 Les clients ne nécessitent pas un certificat PKI de client pour utiliser des points de distribution cloud. Ils s'authentifient auprès de l'infrastructure de gestion à l'aide d'un certificat auto-signé ou d'un certificat PKI de client. Le point de gestion envoie ensuite un jeton d’accès Configuration Manager au client et ce dernier le présente au point de distribution cloud. Le jeton reste valide pendant huit heures.  

### <a name="the-microsoft-intune-connector-and-certificates"></a>Connecteur Microsoft Intune et certificats  
 Quand Microsoft Intune inscrit des appareils mobiles, vous pouvez gérer ces appareils dans Configuration Manager en créant un connecteur Microsoft Intune. Le connecteur utilise un certificat PKI ayant une fonctionnalité d’authentification du client pour authentifier Configuration Manager auprès de Microsoft Intune et pour transférer toutes les informations échangées en utilisant le protocole SSL. La taille de la clé de certificat est de 2 048 bits et elle utilise l'algorithme de hachage SHA-1.  

 Lorsque vous installez le connecteur, un certificat de signature est créé et stocké sur le serveur de site pour les clés de chargement de version test et un certificat de chiffrement est créé et stocké sur le point d'enregistrement de certificat pour chiffrer la demande d'accès du protocole d'inscription du certificat simple (SCEP). Ces certificats ont aussi une taille de clé de 2 048 bits et utilisent l'algorithme de hachage SHA-1.  

 Quand Intune inscrit des appareils mobiles, il installe un certificat PKI sur ces appareils. Ce certificat possède une fonctionnalité d'authentification de client et utilise une taille de clé de 2 048 bits ainsi que l'algorithme de hachage SHA-1.  

 Ces certificats PKI sont automatiquement demandés, générés et installés par Microsoft Intune.  

### <a name="crl-checking-for-pki-certificates"></a>Vérification de la liste de révocation de certificats pour les certificats PKI  
 Une liste de révocation de certificats (CRL) PKI augmente la surcharge administrative et de traitement, mais elle est plus sécurisée. Toutefois, si la vérification de la liste de révocation des certificats est activée alors que la liste de révocation des certificats est inaccessible, la connexion PKI échoue. Pour plus d’informations, consultez [Sécurité et confidentialité pour Configuration Manager](/sccm/core/plan-design/security/security-and-privacy).  

 La vérification de la liste de révocation des certificats est activée par défaut dans les services Internet. Par conséquent, si vous utilisez une liste de révocation des certificats avec votre déploiement PKI, aucune configuration supplémentaire n'est requise sur la majorité des systèmes de site Configuration Manager qui exécutent les services Internet. L'exception concerne les mises à jour logicielles, qui nécessitent une étape manuelle pour activer la vérification de la liste de révocation des certificats afin de vérifier les signatures des fichiers de mises à jour logicielles.  

 La vérification de la liste de révocation des certificats est activée par défaut pour les ordinateurs client lorsqu'ils utilisent des connexions client HTTPS. La vérification de la liste de révocation des certificats n'est pas activée par défaut lorsque vous exécutez la console de gestion hors bande pour vous connecter à un ordinateur AMT, et vous pouvez activer cette option. Dans Configuration Manager SP1 ou version ultérieure, vous ne pouvez pas désactiver la vérification de la liste de révocation des certificats pour les clients installés sur des ordinateurs Mac.  

 La vérification de la liste de révocation des certificats n’est pas prise en charge pour les connexions suivantes dans Configuration Manager :  

-   Connexions serveur à serveur.  

-   Appareils mobiles qui sont inscrits par Configuration Manager.  

-   Appareils mobiles qui sont inscrits par Microsoft Intune.  

##  <a name="cryptographic-controls-for-server-communication"></a>Contrôles de chiffrement pour les communications serveur  
 Configuration Manager utilise les contrôles de chiffrement suivants pour les communications serveur.  

### <a name="server-communication-within-a-site"></a>Communications serveur intrasite  
 Chaque serveur de système de site utilise un certificat pour transférer des données vers les autres systèmes de site du même site Configuration Manager. Certains rôles de système de site utilisent également des certificats pour l'authentification. Par exemple, si vous installez le point de proxy d'inscription sur un serveur et le point d'inscription sur un autre serveur, ils peuvent s'authentifier mutuellement à l'aide de ce certificat d'identité. Quand Configuration Manager a besoin d’un certificat pour ce type de communication, il recherche un certificat PKI avec une fonctionnalité d’authentification du serveur parmi les certificats disponibles et l’utilise automatiquement. S’il n’en trouve pas, Configuration Manager génère un certificat auto-signé. Ce certificat auto-signé a une capacité d'authentification serveur, utilise l'algorithme SHA-256 et a une longueur de clé de 2048 bits. Configuration Manager copie le certificat dans le magasin Personnes autorisées sur d’autres serveurs de système de site qui peuvent avoir besoin d’approuver le système de site. Les systèmes de site peuvent ensuite s'approuver mutuellement à l'aide de ces certificats et PeerTrust.  

 En plus de ce certificat pour chaque serveur de système de site, Configuration Manager génère un certificat auto-signé pour la plupart des rôles de système de site. Lorsqu'il existe plusieurs instances de rôle de système de site dans le même site, ils partagent le même certificat. Par exemple, vous pouvez disposer de plusieurs points de gestion ou de plusieurs points d'inscription dans le même site. Ce certificat auto-signé utilise également l'algorithme SHA-256 et sa longueur de clé est de 2 048 bits. Il est également copié dans le magasin Personnes autorisées sur des serveurs de système de site qui pourront avoir besoin de l'approuver. Les rôles de système de site suivants génèrent ce certificat :  

- Point de service web du catalogue des applications  

- Point du site web du catalogue des applications  

- Point de synchronisation Asset Intelligence  

- Point d'enregistrement de certificat  

- Point Endpoint Protection  

- Point d'inscription  

- Point d’état de secours  

- Point de gestion  

- Point de distribution multidiffusion  

- Point de service hors bande  

- Point de Reporting Services  

- Point de mise à jour logicielle  

- Point de migration d’état  

- Point du programme de validation d'intégrité système  

- Connecteur Microsoft Intune  

  Ces certificats sont gérés automatiquement par Configuration Manager et, si nécessaire, générés automatiquement.  

  Configuration Manager utilise également un certificat d’authentification du client pour envoyer des messages d’état du point de distribution vers le point de gestion. Lorsque le point de gestion est configuré pour les connexions client HTTPS uniquement, vous devez utiliser un certificat PKI. Si le point de gestion accepte les connexions HTTP, vous pouvez utiliser un certificat PKI ou choisir d'utiliser un certificat auto-signé qui possède la possibilité d'authentification client, utilise l'algorithme SHA-256 et dont la longueur de clé est de 2 048 bits.  

### <a name="server-communication-between-sites"></a>Communications serveur entre les sites  
 Configuration Manager transfère des données entre les sites en utilisant la réplication de base de données et la réplication basée sur les fichiers. Pour plus d’informations, consultez [Communications entre les points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

 Configuration Manager configure automatiquement la réplication de base de données entre les sites. Il utilise aussi automatiquement des certificats PKI avec une fonctionnalité d’authentification du serveur, s’ils sont disponibles ; sinon, Configuration Manager crée des certificats auto-signés pour l’authentification du serveur. Dans les deux cas, l'authentification entre sites est établie à l'aide de certificats dans le magasin Personnes autorisées qui utilise PeerTrust. L’utilisation de ce magasin de certificats garantit que seuls les ordinateurs SQL Server qui sont utilisés par la hiérarchie Configuration Manager participent à la réplication entre sites. Tandis que les sites principaux et le site d'administration centrale peuvent répliquer des modifications de configuration vers tous les sites de la hiérarchie, les sites secondaires peuvent répliquer les modifications de configuration uniquement vers leur site parent.  

 Les serveurs de site établissent une communication entre sites à l'aide d'un échange de clé sécurisé qui s'effectue automatiquement. Le serveur de site émetteur génère un hachage et le signe avec sa clé privée. Le serveur de site récepteur vérifie la signature en utilisant la clé publique et compare le hachage à la valeur générée localement. Si les valeurs correspondent, le site récepteur accepte les données répliquées. Si les valeurs ne correspondent pas, Configuration Manager rejette les données de réplication.  

 La réplication de base de données dans Configuration Manager utilise Service Broker SQL Server pour transférer des données entre les sites à l’aide des mécanismes suivants :  

- Connexion SQL Server à SQL Server : cette connexion utilise des informations d'identification Windows pour l'authentification serveur et des certificats auto-signés 1 024 bits pour signer et chiffrer les données à l'aide de la norme AES (Advanced Encryption Standard). Si les certificats PKI avec la possibilité d'authentification serveur sont disponibles, ils seront utilisés. Le certificat doit se trouver dans le magasin Personnel pour le magasin de certificats Ordinateur.  

- SQL Service Broker : il utilise des certificats auto-signés avec 2 048 bits pour l'authentification et pour signer et chiffrer les données à l'aide de la norme AES (Advanced Encryption Standard). Le certificat doit se trouver dans la base de données principale SQL Server.  

  La réplication basée sur des fichiers utilise le protocole SMB (Server Message Block) et l'algorithme SHA-256 pour signer les données qui ne sont pas chiffrées mais elle ne contient aucune donnée sensible. Si vous souhaitez chiffrer ces données, vous pouvez utiliser IPsec. Vous devez effectuer ce chiffrement indépendamment de Configuration Manager.  

##  <a name="cryptographic-controls-for-clients-that-use-https-communication-to-site-systems"></a>Contrôles de chiffrement pour les clients qui utilisent la communication HTTPS avec les systèmes de site  
 Lorsque les rôles de système de site acceptent les connexions client, vous pouvez les configurer pour accepter les connexions HTTP et HTTPS, ou uniquement les connexions HTTPS. Les rôles de système de site qui acceptent les connexions à partir d'Internet acceptent uniquement les connexions client via HTTPS.  

 Les connexions client via HTTPS offrent un niveau de sécurité plus élevé grâce à l'intégration avec une infrastructure à clé publique (PKI) pour protéger la communication client-serveur. Cependant, si vous configurez les connexions client HTTPS sans une connaissance approfondie de la planification, du déploiement et des opérations d'une infrastructure à clé publique, un certain risque persiste. Par exemple, si vous ne sécurisez pas votre autorité de certification racine, des personnes malveillantes sont susceptibles de compromettre la fiabilité de l'ensemble de votre infrastructure à clé publique. Le fait de ne pas parvenir à déployer et à gérer les certificats d'infrastructure à clé publique à l'aide de processus contrôlés et sécurisés peut aboutir à des clients non gérés qui ne peuvent pas recevoir de mises à jour logicielles critiques ou de packages.  

> [!IMPORTANT]  
>  Les certificats PKI qui sont utilisés pour la communication client protègent la communication uniquement entre le client et certains systèmes de site. Ils ne protègent pas le canal de communication entre le serveur de site et les systèmes de site ou entre des serveurs de site.  

### <a name="communication-that-is-unencrypted-when-clients-use-https-communication"></a>Communications non chiffrées quand les clients utilisent la communication HTTPS  
 Lorsque les clients communiquent avec des systèmes de site à l'aide du protocole HTTPS, les communications sont généralement chiffrées via le protocole SSL. Cependant, dans les cas suivants, les clients communiquent avec les systèmes de site sans recourir au chiffrement :  

- le client ne parvient pas à effectuer une connexion HTTPS sur l'Intranet et revient à utiliser le protocole HTTP lorsque les systèmes de site autorisent cette configuration  

- Communication vers les rôles de système de site suivants :  

  -   le client envoie des messages d'état au point d'état de secours  

  -   le client envoie des demandes PXE à un point de distribution compatible PXE  

  -   Le client envoie les données de notification à un point de gestion  

  Les points Reporting services sont configurés pour utiliser HTTP ou HTTPS, indépendamment du mode de communication client.  

##  <a name="cryptographic-controls-for-clients-chat-use-http-communication-to-site-systems"></a>Contrôles de chiffrement pour les clients qui utilisent la communication HTTP avec les systèmes de site  
 Quand les clients utilisent la communication HTTP avec des rôles de système de site, ils peuvent utiliser des certificats PKI pour l’authentification du client ou bien les certificats auto-signés que Configuration Manager génère. Les certificats auto-signés qui sont générés par Configuration Manager comportent un identificateur d’objet personnalisé utilisé pour la signature et le chiffrement. Ces certificats permettent d’identifier le client de façon unique. Pour tous les systèmes d'exploitation pris en charge sauf Windows Server 2003, ces certificats auto-signés utilisent SHA-256 et ont une longueur de clé de 2 048 bits. Pour Windows Server 2003, SHA1 est utilisé avec une longueur de clé de 1 024 bits.  

### <a name="operating-system-deployment-and-self-signed-certificates"></a>Déploiement de systèmes d’exploitation et certificats auto-signés  
 Quand vous utilisez Configuration Manager pour déployer des systèmes d’exploitation avec des certificats auto-signés, l’ordinateur client a également besoin d’un certificat pour communiquer avec le point de gestion, même s’il se trouve dans une phase de transition (démarrage depuis le média de séquence de tâches ou un point de distribution PXE, par exemple). Pour prendre en charge ce scénario pour les connexions HTTP, Configuration Manager génère des certificats auto-signés qui comportent un identificateur d’objet personnalisé utilisé pour la signature et le chiffrement. Ces certificats permettent d’identifier le client de façon unique. Pour tous les systèmes d'exploitation pris en charge sauf Windows Server 2003, ces certificats auto-signés utilisent SHA-256 et ont une longueur de clé de 2 048 bits. Pour Windows Server 2003, SHA1 est utilisé avec une longueur de clé de 1 024 bits. Si ces certificats auto-signés sont compromis, afin d'empêcher les intrus de les utiliser pour emprunter l'identité des clients approuvés, bloquez les certificats dans le nœud **Certificats** de l'espace de travail **Administration** , nœud **Sécurité** .  

### <a name="client-and-server-authentication"></a>Authentification client et serveur  
 Quand des clients se connectent via HTTP, ils authentifient les points de gestion à l’aide des services de domaine Active Directory ou de la clé racine approuvée de Configuration Manager. Les clients n'authentifient pas d'autres rôles de système de site, comme les points de migration de l'état ou les points de mise à jour logicielle.  

 Lorsqu'un point de gestion authentifie un client pour la première fois en utilisant le certificat auto-signé du client, ce mécanisme offre une sécurité minimale car n'importe quel ordinateur peut générer un certificat auto-signé. Dans ce scénario, le processus d'identité client doit être complété par une approbation. Seuls les ordinateurs approuvés doivent obtenir cette approbation, soit automatiquement par Configuration Manager, soit manuellement par un administrateur. Pour plus d’informations, consultez la section d’approbation dans [Communications entre les points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints).  

## <a name="about-ssl-vulnerabilities"></a>Vulnérabilités du protocole SSL
Pour améliorer la sécurité de vos clients et serveurs Configuration Manager, effectuez les étapes suivantes :

-   Activer TLS 1.2

    Pour activer TLS 1.2 pour Configuration Manager, consultez l’article de la Base de connaissances suivant : [Guide pratique pour activer TLS 1.2 pour Configuration Manager](https://support.microsoft.com/en-us/help/4040243/how-to-enable-tls-1-2-for-configuration-manager).
-   Désactiver SSL 3.0, TLS 1.0 et TLS 1.1 
-   Réorganiser les suites de chiffrement en rapport avec TLS 

Pour plus d’informations, consultez [Guide pratique pour restreindre l’utilisation de certains algorithmes et protocoles de chiffrement dans Schannel.dll](https://support.microsoft.com/en-us/kb/245030/) et [Hiérarchisation des suites de chiffrement Schannel](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx). Ces procédures n’affectent pas les fonctionnalités de Configuration Manager.

