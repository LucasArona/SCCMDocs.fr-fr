---
title: Sécurité et confidentialité pour l’administration de site
titleSuffix: Configuration Manager
description: Optimisez la sécurité et la confidentialité pour l’administration de site dans System Center Configuration Manager.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 515385c6c6855e63dc32b522edff9cd2047331bd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour l’administration de site dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations de sécurité et de confidentialité pour les sites System Center Configuration Manager et la hiérarchie.

##  <a name="BKMK_Security_Sites"></a> Bonnes pratiques de sécurité pour l’administration de site  
 Utilisez les bonnes pratiques de sécurité suivantes pour vous aider à sécuriser les sites System Center Configuration Manager et la hiérarchie.  

 **Exécutez le programme d’installation à partir d’une source approuvée et sécurisez le canal de communication entre le support d’installation et le serveur de site.**  

 Pour empêcher la falsification des fichiers sources, exécutez le programme d’installation à partir d’une source approuvée. Si vous stockez les fichiers sur le réseau, sécurisez l'emplacement réseau.  

 Si vous exécutez le programme d’installation à partir d’un emplacement réseau, pour empêcher une éventuelle personne malveillante de falsifier les fichiers lors de leur transmission sur le réseau, utilisez IPsec ou la signature SMB (Server Message Block) entre l’emplacement source des fichiers d’installation et le serveur de site.  

 De plus, si vous utilisez le téléchargeur d’installation pour télécharger les fichiers requis par le programme d’installation, veillez à sécuriser également l’emplacement de stockage de ces fichiers et sécurisez le canal de communication pour cet emplacement lorsque vous exécutez le programme d’installation.  

 **Développez le schéma Active Directory pour System Center Configuration Manager et publiez des sites vers les services de domaine Active Directory.**  

 Les extensions de schéma ne sont pas nécessaires pour exécuter System Center Configuration Manager, mais elles créent un environnement plus sécurisé car les serveurs de site et les clients Configuration Manager peuvent récupérer les informations à partir d’une source approuvée.  

 Si les clients se trouvent dans un domaine non approuvé, déployez les rôles de système de site suivants dans les domaines des clients :  

-   Point de gestion  

-   Point de distribution  

-   Point du site web du catalogue des applications  

> [!NOTE]  
>  Un domaine approuvé pour Configuration Manager requiert l’authentification Kerberos. Cela signifie que si des clients se trouvent dans une autre forêt qui ne dispose pas d’une approbation de forêt bidirectionnelle avec la forêt du serveur de site, ces clients sont considérés comme étant dans un domaine non approuvé. Dans ce cas, une approbation externe n'est pas suffisante.  

 **Utilisez IPsec pour sécuriser les communications entre les sites et serveurs de système de site.**  

 Bien que Configuration Manager sécurise les communications entre le serveur de site et l’ordinateur qui exécute SQL Server, Configuration Manager ne sécurise pas les communications entre les rôles de système de site et SQL Server. Seuls certains systèmes de site (le point d'inscription et le point de service Web du catalogue d'applications) peuvent être configurés pour le protocole HTTPS pour la communication intrasite.  

 Si vous n'utilisez pas de contrôles supplémentaires pour sécuriser ces canaux serveur à serveur, des personnes malveillantes peuvent utiliser différentes attaques d'usurpation ou de l'intercepteur contre les systèmes de site. Utilisez la signature SMB lorsque vous ne pouvez pas utiliser IPsec.  

> [!NOTE]  
>  Il est particulièrement important de sécuriser le canal de communication entre le serveur de site et le serveur de la source du package. Cette communication utilise SMB. Si vous ne pouvez pas utiliser IPsec pour sécuriser cette communication, utilisez la signature SMB afin de vous assurer que les fichiers ne sont pas falsifiés avant que les clients les téléchargent et les exécutent.  

 **Ne modifiez pas les groupes de sécurité créés et gérés par Configuration Manager pour la communication du système de site.**  

 Groupes de sécurité :  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;code_site\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;code_site\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;code_site\>**  

Configuration Manager crée et gère automatiquement ces groupes de sécurité. Cela inclut la suppression de comptes d'ordinateur lorsqu'un rôle de système de site est supprimé.  

Pour garantir la continuité de service et des privilèges minimum, ne modifiez pas ces groupes manuellement.  

**Si les clients ne peuvent pas interroger le serveur du catalogue global pour obtenir des informations Configuration Manager, gérez le processus de mise en service de la clé racine approuvée.**  

Si les clients ne peuvent pas interroger le catalogue global pour obtenir des informations Configuration Manager, ils doivent s’appuyer sur la clé racine approuvée pour authentifier des points de gestion valides. La clé racine approuvée est stockée dans le Registre du client et peut être configurée à l'aide d'une stratégie de groupe ou d'une configuration manuelle.  

Si le client ne dispose pas d'une copie de la clé racine approuvée avant de contacter un point de gestion pour la première fois, il approuve le premier point de gestion avec lequel il communique. Pour réduire le risque d'un acte de piraterie consistant à réacheminer les clients vers un point de gestion non autorisé, vous pouvez préparer la mise en service des clients avec la clé racine approuvée. Pour plus d’informations, voir [Planification de la clé racine approuvée](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Utilisez des numéros différents des numéros de port par défaut.**  

L’utilisation de numéros de port différents des numéros par défaut peut vous permettre de bénéficier d’une sécurité supplémentaire, car les personnes malveillantes ont plus de difficulté à explorer l’environnement en vue d’une attaque. Si vous décidez d’utiliser des ports autres que les ports par défaut, planifiez-les avant d’installer Configuration Manager et utilisez-les de manière cohérente sur tous les sites de la hiérarchie. Les ports de demande client et l’éveil par appel réseau (Wake On LAN), notamment, permettent d’utiliser des numéros de port autres que les numéros par défaut.  

**Utilisez la séparation des rôles sur les systèmes de site.**  

Bien que vous puissiez installer tous les rôles de système de site sur un seul ordinateur, cette pratique est rarement utilisée sur les réseaux de production, car elle crée un point de défaillance unique.  

**Réduisez le profil d'attaque.**  

L’isolation de chaque rôle de système de site sur un serveur différent réduit le risque qu’une attaque contre les vulnérabilités d’un système de site puisse être utilisée contre un autre système de site. De nombreux rôles de système de site requièrent l’installation d’IIS (Internet Information Services) sur le système de site et cela augmente la surface d’attaque. Si vous devez combiner des rôles de système de site afin de réduire les dépenses en matériel, combinez les rôles de système de site IIS uniquement avec d’autres rôles de système de site nécessitant IIS.  

> [!IMPORTANT]  
>  Le rôle de point d’état de secours est une exception. Comme ce rôle de système de site accepte les données non authentifiées des clients, nous vous recommandons de ne jamais attribuer le rôle de point d’état de secours à un autre système de site Configuration Manager.  


**Suivez les meilleures pratiques de sécurité pour Windows Server et exécutez l'Assistant Configuration de la sécurité sur tous les systèmes de site.**  

L'Assistant Configuration de la sécurité (SCW) vous aide à créer une stratégie de sécurité que vous pouvez appliquer à n'importe quel serveur de votre réseau. Une fois que vous avez installé le modèle System Center Configuration Manager, l’Assistant Configuration de la sécurité reconnaît les applications, les services, les ports et les rôles de système de site Configuration Manager. Il autorise ensuite les communications requises pour Configuration Manager et bloque les communications non requises.  

L’Assistant Configuration de la sécurité est inclus dans le kit de ressources pour System Center 2012 Configuration Manager, que vous pouvez télécharger dans le Centre de téléchargement Microsoft : [System Center 2012 – Composants additionnels et extensions du composant Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=251931).  

**Configurez des adresses IP statiques pour les systèmes de site.**  

Les adresses IP statiques sont plus simples à protéger des attaques de résolution de noms.  

Elles facilitent également la configuration d’IPsec. L’utilisation d’IPsec est une bonne pratique de sécurité pour sécuriser les communications entre des systèmes de site dans Configuration Manager.  

**N'installez pas d'autres applications sur des serveurs de système de site.**  

Lorsque vous installez d’autres applications sur des serveurs de système de site, vous augmentez la surface d’attaque pour Configuration Manager et risquez des problèmes d’incompatibilité.  

**Exigez la signature et autorisez le cryptage comme une option de site.**  

Activez les options de signature et de cryptage pour le site. Assurez-vous que tous les clients peuvent prendre en charge l’algorithme de hachage SHA-256, puis activez l’option **Exiger SHA-256**.  

**Limitez et surveillez les utilisateurs administratifs Configuration Manager et utilisez l’administration basée sur les rôles pour accorder à ces utilisateurs les autorisations minimales dont ils ont besoin.**  

Accordez un accès administratif à Configuration Manager uniquement aux utilisateurs auxquels vous faites confiance, puis accordez-leur les autorisations minimales en utilisant les rôles de sécurité intégrés ou en personnalisant les rôles de sécurité. Les utilisateurs administratifs qui peuvent créer, modifier et déployer des applications, des séquence de tâches, des mises à jour logicielles, des éléments de configuration et des références de configuration, peuvent potentiellement contrôler des appareils dans la hiérarchie Configuration Manager.  

Auditez régulièrement les affectations d'utilisateur administratifs et leur niveau d'autorisation pour vérifier les modifications requises.  

Pour plus d'informations sur la configuration de l'administration basée sur des rôles, voir la section [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

**Sécurisez les sauvegardes Configuration Manager et le canal de communication lors de la sauvegarde et de la restauration.**  

Lorsque vous sauvegardez Configuration Manager, ces informations incluent des certificats et d’autres données sensibles qui pourraient être utilisées par une personne malveillante pour l’emprunt d’identité.  

Utilisez la signature SMB ou IPsec lorsque vous transférez ces données sur le réseau et sécurisez l'emplacement de sauvegarde.  

**Lorsque vous exportez ou importez des objets à partir de la console Configuration Manager vers un emplacement réseau, sécurisez l’emplacement et le canal de réseau.**  

Veillez à restreindre l'accès au dossier réseau.  

Utilisez la signature SMB ou IPsec entre l’emplacement réseau et le serveur de site, et entre l’ordinateur qui exécute la console Configuration Manager et le serveur de site pour empêcher une personne malveillante de falsifier les données exportées. Utilisez IPsec pour chiffrer les données sur le réseau afin d'éviter la divulgation d'informations.  

**Si un système de site n’est pas désinstallé correctement ou cesse de fonctionner et ne peut pas être restauré, supprimez manuellement les certificats Configuration Manager pour ce serveur à partir des autres serveurs Configuration Manager.**  

Pour supprimer la confiance entre homologues initialement établie avec le système de site et les rôles de système de site, supprimez manuellement les certificats Configuration Manager pour le serveur en échec dans le magasin de certificats **Personnes autorisées** sur d’autres serveurs de système de site. Ceci est particulièrement important si vous adaptez le serveur sans le reformater.  

Pour plus d’informations sur ces certificats, consultez la section **Contrôles de chiffrement pour la communication du serveur** dans [Informations techniques de référence sur les contrôles de chiffrement pour System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**Ne configurez pas les systèmes de site basés sur Internet pour relier le réseau de périmètre et l'Intranet.**  

Ne configurez pas les serveurs de système de site comme multi-résidents, afin qu’ils se connectent au réseau de périmètre et à l’intranet. Bien que cette configuration autorise les systèmes de site basés sur Internet à accepter les connexions client à partir d'Internet et de l'Intranet, elle élimine une limite de sécurité entre le réseau de périmètre et l'Intranet.  

**Si le serveur de système de site se trouve sur un réseau non approuvé (tel qu'un réseau de périmètre), configurez le serveur de site pour établir des connexions avec le système de site.**  

Par défaut, les systèmes de site établissent des connexions avec le serveur de site pour transférer des données, ce qui peut constituer un risque pour la sécurité lorsque la connexion est établie depuis un réseau non approuvé vers le réseau approuvé. Lorsque des systèmes de site acceptent des connexions depuis Internet ou résident dans une forêt non approuvée, configurez l'option du système de site **Exiger que le serveur de site établisse des connexions vers ce système de site** afin que toutes les connexions soient établies depuis le réseau approuvé une fois que le système de site et tout rôle de système de site a été installé.  

**Si vous utilisez un serveur proxy Web pour la gestion des clients basés sur Internet, utilisez le pontage SSL vers SSL à l'aide de la terminaison avec authentification.**  

 Lorsque vous configurez la terminaison SSL au niveau du serveur Web proxy, les paquets provenant d'Internet sont inspectés avant d'être transférés au réseau interne. Le serveur Web proxy authentifie la connexion du client, l'arrête, puis ouvre une nouvelle connexion authentifiée vers les systèmes de site basés sur Internet.  

 Lorsque les ordinateurs clients Configuration Manager utilisent un serveur web proxy pour se connecter à des systèmes de site basés sur Internet, l’identité du client (GUID client) est contenue, en toute sécurité, dans la charge utile du paquet pour que le point de gestion ne considère pas le serveur web proxy comme le client. Si votre serveur Web proxy ne peut pas prendre en charge la configuration requise pour le pontage SSL, le tunnel SSL est également pris en charge. Il s'agit d'une option moins sûre car les paquets SSL d'Internet sont transférés aux systèmes de site sans terminaison et ne peuvent donc pas être inspectés à la recherche de contenu malveillant.  

 Si votre serveur Web proxy ne peut pas prendre en charge la configuration requise pour le pontage SSL, vous pouvez utiliser le tunnel SSL. Toutefois, il s'agit d'une option moins sûre car les paquets SSL d'Internet sont transférés aux systèmes de site sans terminaison et ne peuvent donc pas être inspectés à la recherche de contenu malveillant.  

> [!WARNING]  
>  Les appareils mobiles qui sont inscrits par Configuration Manager ne peuvent pas utiliser le pontage SSL et doivent utiliser le tunnel SSL uniquement.  

**Configurations à utiliser si vous configurez le site pour qu’il réveille les ordinateurs afin d’installer le logiciel :**  

-   Si vous utilisez des paquets de mise en éveil traditionnels, utilisez la monodiffusion plutôt que des diffusions dirigées vers le sous-réseau.  

-   Si vous devez utiliser des diffusions dirigées vers le sous-réseau, configurez les routeurs de sorte à autoriser les diffusions vers IP uniquement à partir du serveur de site et uniquement sur un numéro de port autre que le port par défaut.  

Pour plus d’informations sur les différentes technologies Wake On LAN, consultez [Planification de l’éveil des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

**Si vous utilisez la notification par courrier électronique, configurez un accès authentifié au serveur de messagerie SMTP.**  

Dans la mesure du possible, utilisez un serveur de courrier qui prend en charge l’accès authentifié et le compte d’ordinateur du serveur de site pour l’authentification. Si vous devez spécifier un compte d'utilisateur pour l'authentification, utilisez un compte qui dispose des privilèges minimum.  

##  <a name="BKMK_Security_SiteServer"></a> Bonnes pratiques de sécurité pour le serveur de site  
 Utilisez les bonnes pratiques de sécurité suivantes pour mieux sécuriser le serveur de site Configuration Manager.  

 **Installez Configuration Manager sur un serveur membre plutôt que sur un contrôleur de domaine.**  

 Le serveur de site Configuration Manager et les systèmes de site ne nécessitent pas d’installation sur un contrôleur de domaine. Un contrôleur de domaine ne possède pas de base de données SAM (Security Accounts Management) locale autre que la base de données du domaine. Lorsque vous installez Configuration Manager sur un serveur membre, vous pouvez gérer les comptes Configuration Manager dans la base de données SAM locale plutôt que dans la base de données du domaine.  

 Cette pratique réduit également la surface d'attaque sur vos contrôleurs de domaine.  

 **Installez des sites secondaires en évitant de copier les fichiers vers le serveur de site secondaire sur le réseau.**  

 Lorsque vous exécutez le programme d’installation et créez un site secondaire, ne sélectionnez pas l’option de copie des fichiers depuis le site parent vers le site secondaire, et n’utilisez pas un emplacement réseau source. Lorsque vous copiez des fichiers sur le réseau, un attaquant doué pourrait pirater le package d'installation du site secondaire et falsifier les fichiers avant qu'ils soient installés, bien qu'il soit difficile de programmer cette attaque. Cette attaque peut être atténuée à l'aide d'IPsec ou de SMB lorsque vous transférez les fichiers.  

 Au lieu de copier les fichiers sur le réseau, sur le serveur de site secondaire, copiez les fichiers sources du dossier multimédia vers un dossier local. Ensuite, lorsque vous exécutez le programme d’installation pour créer un site secondaire, dans la page **Fichiers sources d’installation**, sélectionnez **Utiliser les fichiers sources dans l’emplacement local suivant sur l’ordinateur de site secondaire (le plus sûr)**, et spécifiez ce dossier.  

 Pour plus d’informations, consultez [Install a secondary site](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) (Installer un site secondaire) dans la rubrique [Use the Setup Wizard to install sites](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) (Utiliser l’Assistant Configuration pour installer des sites).  

##  <a name="BKMK_Security_SQLServer"></a> Bonnes pratiques de sécurité pour SQL Server  
 Configuration Manager utilise SQL Server comme base de données principale. Si la base de données est compromise, des personnes malveillantes pourraient contourner Configuration Manager et accéder directement à SQL Server afin de lancer des attaques via Configuration Manager. Considérez les attaques contre SQL Server comme présentant un risque élevé et traitez-les en conséquence.  

 Utilisez les bonnes pratiques de sécurité suivantes pour mieux sécuriser SQL Server pour Configuration Manager.  

 **N’utilisez pas le serveur de base de données de site Configuration Manager pour exécuter d’autres applications SQL Server.**  

 L’augmentation du nombre d’accès au serveur de base de données de site Configuration Manager augmente le risque auquel sont exposées vos données Configuration Manager. Si la base de données du site Configuration Manager est compromise, les autres applications sur le même ordinateur SQL Server présentent également des risques.  

 **Configurez SQL Server pour utiliser l'authentification Windows.**  

 Configuration Manager accède au site de base de données à l’aide d’un compte Windows et de l’authentification Windows, mais vous pouvez également configurer SQL Server de sorte qu’il utilise le mode mixte SQL Server. Le mode mixte SQL Server vous permet de configurer des connexions SQL supplémentaires afin d’accéder à la base de données, mais cela n’est pas nécessaire et augmente la surface d’attaque.  

 **Prenez des mesures supplémentaires pour assurer que les sites secondaires qui utilisent SQL Server Express disposent des dernières mises à jour logicielles.**  

 Lorsque vous installez un site principal, Configuration Manager télécharge SQL Server Express depuis le Centre de téléchargement Microsoft, puis copie les fichiers sur le serveur de site principal. Lorsque vous installez un site secondaire et sélectionnez l’option d’installation de SQL Server Express, Configuration Manager installe la version téléchargée précédemment et ne vérifie pas si de nouvelles versions sont disponibles. Pour vous assurer que le site secondaire dispose des dernières versions, effectuez l’une des tâches suivantes :  

-   Une fois le site secondaire installé, exécutez Windows Update sur le serveur de site secondaire.  

-   Avant d'installer le site secondaire, installez SQL Server Express manuellement sur l'ordinateur qui va exécuter le serveur de site secondaire et assurez-vous d'installer la version la plus récente, ainsi que toutes les mises à jour logicielles. Installez ensuite le site secondaire et sélectionnez l’option pour utiliser une instance existante de SQL Server.  

Exécutez régulièrement Windows Update sur ces sites et sur toutes les versions installées de SQL Server pour vous assurer qu'ils disposent des dernières mises à jour logicielles.  

**Suivez les meilleures pratiques pour SQL Server.**  

Identifiez et suivez les meilleures pratiques pour votre version de SQL Server. Prenez toutefois en compte les impératifs suivants pour Configuration Manager :  

-   Le compte d'ordinateur du serveur de site doit être membre du groupe Administrateurs sur l'ordinateur exécutant SQL Server. Si vous suivez la recommandation SQL Server « Définir des administrateurs de manière explicite », le compte utilisé pour exécuter l’installation sur le serveur de site doit être membre du groupe Utilisateurs SQL.  

-   Si vous installez SQL Server à l'aide d'un compte utilisateur de domaine, vous devez configurer un nom principal de service (SPN) pour le compte d'ordinateur de domaine dans les services de domaine Active Directory. Sans le nom de principal du service, l’authentification Kerberos échoue, de même que l’installation de Configuration Manager.  

##  <a name="BKMK_Security_IIS"></a> Bonnes pratiques de sécurité pour les systèmes de site exécutant IIS  
Plusieurs rôles de système de site dans Configuration Manager requièrent IIS. Le processus de sécurisation IIS permet à Configuration Manager de fonctionner correctement et réduit les risques d’attaques de sécurité. Dans la mesure du possible, réduisez le nombre de serveurs qui requièrent IIS. Par exemple, exécutez uniquement le nombre de points de gestion dont vous avez besoin pour prendre en charge votre base de clients, en tenant compte de la haute disponibilité et de l'isolation du réseau pour la gestion des clients basée sur Internet.  

 Utilisez les meilleures pratiques de sécurité suivantes pour contribuer à sécuriser les systèmes de site qui exécutent IIS.  

 **Désactivez les fonctions IIS dont vous n’avez pas besoin.**  

 Installez uniquement les fonctionnalités IIS minimales pour le rôle de système de site que vous installez. Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Configurez les rôles de système de site pour exiger HTTPS.**  

 Lorsque les clients se connectent à un système de site à l'aide du protocole HTTP au lieu de HTTPS, ils utilisent l'authentification Windows, qui peut avoir recours à l'authentification NTLM plutôt qu'à l'authentification Kerberos. Avec l'authentification NTLM, les clients risquent de se connecter à un serveur non autorisé.  

 Les points de distribution peuvent présenter l'exception à cette meilleure pratique de sécurité dans la mesure où les comptes d'accès aux packages ne fonctionnent pas lorsque ces points de distribution sont configurés pour le protocole HTTPS. Les comptes d'accès aux packages fournissent des autorisations d'accès au contenu, vous permettant de limiter les utilisateurs disposant des droits d'accès au contenu. Pour plus d’informations, voir [Bonnes pratiques de sécurité pour la gestion de contenu](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Configurez une liste de certificats de confiance dans IIS pour les rôles système de site.**  

Rôles des systèmes de site :  

-   Point de distribution configuré pour le protocole HTTPS  

-   Point de gestion configuré pour le protocole HTTPS et pour la prise en charge des appareils mobiles

Une liste de certificats de confiance est une liste définie d'autorités de certification racine de confiance. Utilisée avec une stratégie de groupe et un déploiement d’infrastructure à clé publique (PKI), une liste de certificats de confiance vous permet de compléter les autorités de certification racine de confiance déjà configurées sur votre réseau, notamment celles installées automatiquement avec Microsoft Windows ou ajoutées par le biais des autorités de certification racine d’entreprise Windows. Toutefois, lorsqu’une liste de certificats de confiance est configurée dans IIS, elle définit un sous-ensemble des autorités de certification racine de confiance.  

Ce dernier vous confère un contrôle accru de la sécurité car la liste de certificats de confiance limite l'acceptation des certificats clients à ceux qui sont publiés à partir de la liste des autorités de certification de la liste de certificats de confiance. Par exemple, Windows est fourni avec différents certificats d’autorités de certification tierces renommées, telles que VeriSign et Thawte.

Par défaut, l'ordinateur qui exécute les services Internet (IIS) approuve les certificats liés à ces autorités de certification connues. Si vous ne configurez pas IIS avec une liste de certificats de confiance pour les rôles de système de site répertoriés, tout appareil doté d’un certificat client publié par ces autorités de certification est accepté comme client Configuration Manager valide. Si vous configurez les services Internet (IIS) avec une liste de certificats de confiance qui ne comprend pas ces autorités de certification, les connexions de clients sont rejetées si le certificat requis était lié à ces autorités de certification. Cependant, pour que les clients Configuration Manager soient acceptés dans les rôles de système de site répertoriés, vous devez configurer IIS avec une liste de certificats de confiance qui spécifie les autorités de certification utilisées par les clients Configuration Manager.  

> [!NOTE]  
>  Seuls les rôles de système de site répertoriés exigent que vous configuriez une liste de certificats de confiance dans IIS. La liste d’émetteurs de certificats utilisée par Configuration Manager pour les points de gestion fournit la même fonctionnalité aux ordinateurs clients lorsqu’ils se connectent aux points de gestion HTTPS.  

Pour plus d'informations sur la façon de configurer une liste d'autorités de certification approuvées dans IIS, consultez la documentation de IIS.  

**N'installez pas le serveur de site sur un ordinateur comportant IIS.**  

La séparation des rôles permet de réduire le profil d'attaque et d'optimiser la récupération. De plus, le compte d’ordinateur du serveur de site dispose généralement des privilèges d’administrateur sur tous les rôles de système de site (et probablement sur les clients Configuration Manager, si vous utilisez l’installation poussée du client).  

**Utilisez des serveurs IIS dédiés pour Configuration Manager.**  

Il est possible d’héberger plusieurs applications basées sur le web sur les serveurs IIS utilisés par Configuration Manager, mais cela peut augmenter considérablement votre surface d’attaque. Une application mal configurée peut permettre à un attaquant d’acquérir le contrôle d’un système de site Configuration Manager, puis d’étendre son contrôle à la hiérarchie.  

Si vous devez exécuter d’autres applications basées sur le web sur des systèmes de site Configuration Manager, créez un site web personnalisé pour les systèmes de site Configuration Manager.  

**Utilisez un site web personnalisé.**  

Pour les systèmes de site exécutant IIS, vous pouvez configurer Configuration Manager pour utiliser un site web personnalisé en lieu et place du site web par défaut pour IIS. Si vous devez exécuter d’autres applications basées sur le Web sur le système de site, vous devez utiliser un site web personnalisé. Ce paramètre s’applique à l’ensemble du site plutôt qu’à un système de site spécifique.  

En plus de fournir une sécurité supplémentaire, vous devez utiliser un site Web personnalisé si vous exécutez d'autres applications Web sur le système de site.  

**Si vous passez du site Web par défaut à un site Web personnalisé après l'installation des rôles de point de distribution, supprimez les répertoires virtuels par défaut.**  

Lorsque vous utilisez un site web personnalisé à la place du site web par défaut, Configuration Manager ne supprime pas les anciens répertoires virtuels. Supprimez les répertoires virtuels que Configuration Manager a créés initialement sous le site web par défaut.  

Par exemple, les répertoires virtuels à supprimer pour un point de distribution sont les suivants :  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Suivez les meilleures pratiques relatives au serveur IIS.**  

Identifiez et suivez les meilleures pratiques relatives à votre version du serveur IIS. Toutefois, prenez en considération les spécifications de Configuration Manager relatives à certains rôles de système de site spécifiques. Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

##  <a name="BKMK_Security_ManagementPoint"></a> Bonnes pratiques de sécurité pour le point de gestion  
 Les points de gestion représentent l’interface principale entre les appareils et Configuration Manager. Toute attaque contre le point de gestion et le serveur sur lequel il s’exécute doit être considérée comme représentant un risque élevé et doit être traitée en conséquence. Appliquez toutes les bonnes pratiques de sécurité et surveillez toute activité inattendue.  

 Utilisez les bonnes pratiques suivantes pour mieux sécuriser un point de gestion dans Configuration Manager.  

**Lorsque vous installez un client Configuration Manager sur le point de gestion, attribuez-le au site de ce point de gestion.**  

 Évitez le scénario où un client Configuration Manager sur un système de site de point de gestion est attribué à un site autre que le site du point de gestion.  

 Si vous migrez vers System Center Configuration Manager à partir d’une version antérieure, migrez dès que possible le logiciel client sur le point de gestion vers System Center Configuration Manager.  

##  <a name="BKMK_Security_FSP"></a> Bonnes pratiques de sécurité pour le point d’état de secours  
 Utilisez les bonnes pratiques de sécurité suivantes si vous installez un point d’état de secours dans Configuration Manager.  

 Pour plus d'informations sur les considérations relatives à la sécurité, voir [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#determine-if-you-need-a-fallback-status-point).  


**N’exécutez pas d’autres rôles de système de site sur le système de site et n’installez pas le point d’état de secours sur un contrôleur de domaine.**  

 Le point d'état de secours est conçu pour accepter les communications non authentifiées provenant de n'importe quel ordinateur. De ce fait, l'exécution de ce rôle de système de site avec d'autres rôles de système de site ou sur un contrôleur de domaine augmente considérablement le risque auquel est exposé le serveur.  

**Lorsque vous utilisez des certificats PKI pour la communication client dans Configuration Manager, installez le point d’état de secours avant d’installer les clients.**  

 Si les systèmes de site Configuration Manager n’acceptent pas la communication client HTTP, vous pouvez ne pas être au courant que des clients ne sont pas gérés en raison de problèmes liés aux certificats PKI. Toutefois, si les clients sont affectés à un point d’état de secours, ces problèmes de certificat sont signalés par le point d’état de secours.  

 Pour des raisons de sécurité, vous ne pouvez pas affecter un point d’état de secours aux clients une fois qu’ils sont installés. Au lieu de cela, vous ne pouvez attribuer ce rôle que pendant l’installation des clients.  

**Évitez d'utiliser le point d'état de secours dans le réseau de périmètre.**  

 Le point d'état de secours est conçu pour accepter les données provenant de n'importe quel client. Un point d'état de secours sur le réseau de périmètre facilite le dépannage des clients basés sur Internet, mais il convient d'évaluer les avantages liés au dépannage par rapport aux risques pouvant être engendrés par un système de site qui accepte les données non authentifiées sur un réseau accessible au public.  

 Si vous installez le point d’état de secours sur le réseau de périmètre ou sur tout réseau non approuvé, configurez le serveur de site de sorte qu’il initialise les transferts de données au lieu du paramètre par défaut qui autorise le point d’état de secours à se connecter au serveur de site.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Problèmes de sécurité pour l’administration de site  
 Passez en revue les problèmes de sécurité suivants pour Configuration Manager :  

-   Configuration Manager ne possède aucune défense contre un utilisateur administratif autorisé qui utilise Configuration Manager pour attaquer le réseau. Les utilisateurs administratifs non autorisés représentent un risque élevé pour la sécurité et peuvent lancer de nombreuses attaques, dont notamment les stratégies suivantes :  

    -   l’utilisation de la fonction de déploiement de logiciels pour installer et exécuter automatiquement un logiciel malveillant sur tous les clients Configuration Manager de l’entreprise ;  

    -   l’utilisation du contrôle distant pour prendre à distance le contrôle d’un client Configuration Manager sans autorisation ;  

    -   la configuration d'intervalles d'interrogation rapides et d'un grand nombre d'inventaires afin de créer des attaques par déni de service contre les clients et les serveurs ;  

    -   l'utilisation d'un site de la hiérarchie pour écrire des données dans un autre site Active Directory.  

    La hiérarchie du site constitue la limite de sécurité. Considérez le sites comme des limites de gestion uniquement.  

    Analysez toutes les opérations de l'utilisateur administratif et consultez régulièrement les journaux d'audit. Il est impératif de vérifier les antécédents professionnels des utilisateurs administratifs Configuration Manager avant de les recruter, puis de les soumettre régulièrement à des vérifications.  

-   Si le point d'inscription est compromis, un attaquant peut obtenir des certificats pour authentification et voler les informations d'identification des utilisateurs qui inscrivent leurs appareils mobiles.  

    Le point d'inscription communique avec une autorité de certification et peut créer, modifier et supprimer des objets Active Directory. N’installez jamais le point d’inscription dans le réseau de périmètre et surveillez toute activité inattendue.  

-   Si vous autorisez des stratégies d'utilisateur pour la gestion des clients basés sur Internet ou configurez le point du site Web du catalogue d'applications pour les utilisateurs lorsqu'ils sont sur Internet, vous augmentez votre profil d'attaque.  

    En plus des certificats PKI pour les connexions client à serveur, ces configurations requièrent l'authentification Windows, qui peut avoir recours à l'authentification NTLM plutôt qu'à l'authentification Kerberos. L'authentification NTLM est vulnérable aux attaques par relecture et emprunt d'identité. Pour authentifier correctement un utilisateur sur Internet, vous devez autoriser une connexion d'un serveur de système de site basé sur Internet à un contrôleur de domaine.  

-   Le partage Admin$ est requis sur les serveurs de système de site.  

    Le serveur de site Configuration Manager utilise le partage Admin$ pour se connecter aux systèmes de site et y effectuer des opérations de service. Ne désactivez pas ou ne supprimez pas le partage Admin$.  

-   Configuration Manager utilise des services de résolution de noms pour se connecter à d’autres ordinateurs. Ces services sont difficiles à sécuriser contre des attaques de sécurité telles que l’usurpation, l’altération, la répudiation, la divulgation d’informations, le déni de service et l’élévation de privilèges.  

    Identifiez et suivez les meilleures pratiques de sécurité pour la version de DNS et WINS que vous utilisez pour la résolution de noms.  

##  <a name="BKMK_Privacy_Cliients"></a> Informations de confidentialité pour la découverte  
 La découverte crée des enregistrements pour les ressources réseau et les stocke dans la base de données System Center Configuration Manager. Les enregistrements de données de découverte contiennent des informations sur les ordinateurs, telles que les adresses IP, les systèmes d’exploitation et les noms des ordinateurs. Les méthodes de découverte Active Directory peuvent également être configurées pour découvrir toute information stockée dans les services de domaine Active Directory.  

 La seule méthode de découverte activée par défaut est la découverte par pulsations d’inventaire, mais cette méthode découvre uniquement les ordinateurs sur lesquels le logiciel client System Center Configuration Manager est installé.  

 Les informations de découverte ne sont pas envoyées à Microsoft. Au lieu de cela, elles sont stockées dans la base de données Configuration Manager. Les informations sont conservées dans la base de données jusqu’à leur suppression, tous les 90 jours, par la tâche de maintenance du site **Supprimer les données de découverte anciennes**.  

 Avant de configurer d'autres méthodes de découverte ou d'étendre la découverte Active Directory, pensez aux conditions requises en termes de confidentialité.  
