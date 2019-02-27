---
title: Options de ligne de commande du programme d’installation
titleSuffix: Configuration Manager
description: Créez des scripts d’automatisation pour installer System Center Configuration Manager à partir d’une ligne de commande.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f5c85e3058a63868cfee28865c1be222919b29a8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141821"
---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Options de ligne de commande pour le programme d’installation de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Utilisez les informations suivantes pour configurer des scripts ou installer System Center Configuration Manager à partir d’une ligne de commande.  

##  <a name="bkmk_setup"></a> Options de ligne de commande pour le programme d’installation  
 **/DEINSTALL**  
 Désinstalle le site. Exécutez le programme d’installation à partir de l’ordinateur sur lequel est installé le serveur de site.  

 **/DONTSTARTSITECOMP**  
 Installe un site, mais empêche le démarrage du service Gestionnaire de composant de site. Tant que le service Gestionnaire de composant de site n'a pas démarré, le site n'est pas actif. Le Gestionnaire de composant de site est chargé d’installer et de démarrer le service SMS_Executive, ainsi que d’autres processus au niveau du site. Une fois l’installation du site terminée, quand vous démarrez le service Gestionnaire de composant de site, ce dernier installe le service SMS_Executive et d’autres processus nécessaires au fonctionnement du site.  

 **/HIDDEN**  
 Masque l'interface utilisateur pendant l'installation. Utilisez cette option uniquement avec l’option **/SCRIPT**. Le fichier de script sans assistance doit fournir toutes les options nécessaires pour éviter l’échec du programme d’installation.  

 **/NOUSERINPUT**  
 Désactive l’entrée utilisateur pendant l’installation, mais affiche l’Assistant Installation. Utilisez cette option uniquement avec l’option **/SCRIPT**. Le fichier de script sans assistance doit fournir toutes les options nécessaires pour éviter l’échec du programme d’installation.  

 **/RESETSITE**  
 Effectue une réinitialisation du site qui permet de réinitialiser la base de données et les comptes de service du site. Exécutez le programme d’installation à partir de **<*Chemin d’installation de Configuration Manager*>\BIN\X64** sur le serveur de site. Pour plus d’informations sur la réinitialisation du site, consultez la section [Exécuter une réinitialisation de site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) de la rubrique [Modifier votre infrastructure System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*Nom de l’instance*>\\<*Nom de la base de données*>**  
 Effectue un test sur une sauvegarde de la base de données du site pour vérifier qu’elle peut être mise à niveau. Indiquez le nom d’instance et le nom de base de données pour la base de données de site. Si vous spécifiez uniquement le nom de la base de données, le programme d’installation utilise le nom de l’instance par défaut.  

> [!IMPORTANT]  
>  N’exécutez pas cette option de ligne de commande sur la base de données de votre site de production. L’exécution de cette option de ligne de commande sur la base de données de votre site de production met à niveau la base de données du site et risque de rendre votre site inutilisable.  

 **/UPGRADE**  
 Exécute une mise à niveau sans assistance d’un site. Quand vous utilisez **/UPGRADE**, vous devez spécifier la clé du produit, en incluant les tirets (-). Par ailleurs, vous devez spécifier le chemin des fichiers nécessaires au programme d’installation que vous avez téléchargés précédemment.  

 Exemple : `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Pour plus d’informations sur les fichiers nécessaires au programme d’installation, consultez [Téléchargeur d’installation](setup-downloader.md).  

 **/SCRIPT <*Chemin du script d’installation*>**  
 Effectue des installations sans assistance. Un fichier d’initialisation de l’installation est requis quand vous utilisez l’option **/SCRIPT**. Pour plus d’informations sur l’exécution du programme d’installation sans assistance, consultez [Installer des sites à l’aide d’une ligne de commande](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST <*Nom de domaine complet du fournisseur SMS*>**  
 Installe le fournisseur SMS sur l'ordinateur spécifié. Indiquez le nom de domaine complet de l’ordinateur du fournisseur SMS. Pour plus d’informations sur le fournisseur SMS, consultez [Planifier le fournisseur SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST <*Nom de domaine complet du fournisseur SMS*>**  
 Désinstalle le fournisseur SMS sur l'ordinateur spécifié. Indiquez le nom de domaine complet de l’ordinateur du fournisseur SMS.  

 **/MANAGELANGS <*Chemin du script de langue*>**  
 Gère les langues installées sur un site installé précédemment. Pour utiliser cette option, exécutez le programme d’installation à partir de **<*Chemin d’installation de Configuration Manager*>\BIN\X64** sur le serveur de site. Indiquez l’emplacement du fichier de script de langue qui contient les paramètres de langue. Pour plus d’informations sur les options de langue disponibles dans le fichier du script d’installation de langue, consultez la section [Options de ligne de commande pour gérer les langues](#bkmk_Lang).  

##  <a name="bkmk_Lang"></a> Options de ligne de commande pour gérer les langues  
 **Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** ManageLanguages  

    -   **Détails :** Permet de gérer la prise en charge des langues serveur, client et client mobile d'un site.  

**Options**  

-   **Nom de clé :** AddServerLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues de serveur qui seront disponibles pour la console Configuration Manager, ainsi que les rapports et objets Configuration Manager. L'anglais est disponible par défaut.  

-   **Nom de clé :** AddClientLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues qui seront disponibles sur les ordinateurs clients. L'anglais est disponible par défaut.  

-   **Nom de clé :** DeleteServerLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues à supprimer qui ne seront plus disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** DeleteClientLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues à supprimer qui ne seront plus disponibles sur les ordinateurs clients. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** MobileDeviceLanguage  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si les langues du client de l'appareil mobile sont installées.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Télécharger  

         1 = Déjà téléchargé  

    -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin des fichiers nécessaires au programme d’installation*>  

    -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.  

##  <a name="bkmk_Unattended"></a> Clés du fichier de script d’installation sans assistance  
 Utilisez les sections suivantes pour vous aider à créer votre script d’installation sans assistance. Les listes affichent les clés de script d’installation disponibles ainsi que leurs valeurs correspondantes, indiquent si elles sont obligatoires ou non, le type d’installation pour lequel elles sont utilisées, ainsi qu’une brève description de la clé.  

### <a name="unattended-install-for-a-central-administration-site"></a>Installation sans assistance d’un site d’administration centrale  
 Utilisez les détails suivants pour installer un site d’administration centrale à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** InstallCAS  

    -   **Détails :** Installe un site d’administration centrale.  

-   **Nom de clé :** CDLatest  

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest folder.    

    -   **Valeurs :** 1. Toute autre valeur que 1 est considérée comme signifiant que CD.Latest.

    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Code de site*>  

    -   **Détails :** Spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie.  

-   **Nom de clé :** Nom du site  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de site*>  

    -   **Détails :** Spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin d’installation de Configuration Manager*>  

    -   **Détails :** Spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le fournisseur SMS. Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Télécharger  

         1 = Déjà téléchargé  

    -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin des fichiers nécessaires au programme d’installation*>  

    -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  
    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas participer  

         1 = Participer  

    -   **Détails :** Permet de préciser si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur.  

-   **Nom de clé :** AddServerLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues de serveur qui seront disponibles pour la console Configuration Manager, ainsi que les rapports et objets Configuration Manager. L'anglais est disponible par défaut.  

-   **Nom de clé :** AddClientLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues qui seront disponibles sur les ordinateurs clients. L'anglais est disponible par défaut.  

-   **Nom de clé :** DeleteServerLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Permet de modifier un site après son installation. Spécifie les langues à supprimer qui ne seront plus disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** DeleteClientLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Permet de modifier un site après son installation. Spécifie les langues à supprimer qui ne seront plus disponibles sur les ordinateurs clients. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** MobileDeviceLanguage  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si les langues du client de l'appareil mobile sont installées.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName   

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom du serveur SQL*>  

    -   **Détails :** Spécifie le nom du serveur ou de l’instance en cluster exécutant SQL Server qui hébergera la base de données du site.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de la base de données du site*> ou <*Nom de l’instance*>\\<*Nom de la base de données du site*>  

    -   **Détails :** Spécifie le nom de la base de données SQL Server à créer ou à utiliser quand le programme d’installation installe la base de données du site d’administration centrale.  

        > [!IMPORTANT]  
        >  Si vous n’utilisez pas l’instance par défaut, vous devez spécifier le nom d’instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Numéro du port SSB*>  

    -   **Détails :** Spécifie le port SQL Server Service Broker (SSB) utilisé par SQL Server. SSB est généralement configuré pour utiliser le port TCP 4022, mais vous pouvez configurer un autre port.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .mdb de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .mdb de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .ldf de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .ldf de la base de données.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie s’il convient d’installer un point de connexion de service sur ce site. Comme le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être **0** pour un site principal enfant.  

-   **Nom de clé :** CloudConnectorServer  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur de point de connexion de service*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site du point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si le point de connexion de service utilise un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** Obligatoire quand **UseProxy** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur proxy*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur proxy utilisé par le point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** Obligatoire quand **UseProxy** est égal à 1  

    -   **Valeurs :** <*Numéro de port*>  

    -   **Détails :** Spécifie le numéro de port à utiliser pour le port proxy.  

### <a name="unattended-install-for-a-primary-site"></a>Installation sans assistance d’un site principal  
Utilisez les détails suivants pour installer un site principal à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** InstallPrimarySite  

    -   **Détails :** Installe un site principal.  

-   **Nom de clé :** CDLatest  

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest folder.    

    -   **Valeurs :** 1. Toute autre valeur que 1 est considérée comme signifiant que CD.Latest.

    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Code de site*>  

    -   **Détails :** Spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie.  

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de site*>  

    -   **Détails :** Spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin d’installation de Configuration Manager*>

    -   **Détails :** Spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le fournisseur SMS. Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Télécharger  

         1 = Déjà téléchargé  

    -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin des fichiers nécessaires au programme d’installation*>  

    -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  
    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas participer  

         1 = Participer  

    -   **Détails :** Spécifie s’il convient de participer au programme d’amélioration des services.  

-   **Nom de clé :** ManagementPoint  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Nom de domaine complet du serveur de site du point de gestion*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site du point de gestion.  

-   **Nom de clé :** ManagementPointProtocol  

    -   **Obligatoire :** Non  

    -   **Valeurs :** HTTPS *ou* HTTP  

    -   **Détails :** Spécifie le protocole à utiliser pour le point de gestion.  

-   **Nom de clé :** DistributionPoint  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Nom de domaine complet du serveur de site du point de distribution*>  

    -   **Détails :** Spécifie le protocole à utiliser pour le point de distribution.  

-   **Nom de clé :** DistributionPointProtocol  

    -   **Obligatoire :** Non  

    -   **Valeurs :** HTTPS *ou* HTTP  

    -   **Détails :** Spécifie le protocole à utiliser pour le point de distribution.  

-   **Nom de clé :** RoleCommunicationProtocol  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** EnforceHTTPS *ou* HTTPorHTTPS  

    -   **Détails :** Spécifie s’il convient de configurer tous les systèmes de site pour n’accepter que les communications HTTPS à partir de clients ou de configurer la méthode de communication pour chaque rôle de système de site. Quand vous sélectionnez **EnforceHTTPS**, l’ordinateur client doit disposer d’un certificat d’infrastructure à clé publique (PKI) valide pour l’authentification du client.  

-   **Nom de clé :** ClientsUsePKICertificate  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas utiliser  

         1 = Utiliser  

    -   **Détails :** Spécifie si les clients devront utiliser un certificat PKI de client pour communiquer avec les rôles de système de site.  

-   **Nom de clé :** AddServerLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues de serveur qui seront disponibles pour la console Configuration Manager, ainsi que les rapports et objets Configuration Manager. L'anglais est disponible par défaut.  

-   **Nom de clé :** AddClientLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Spécifie les langues qui seront disponibles sur les ordinateurs clients. L'anglais est disponible par défaut.  

-   **Nom de clé :** DeleteServerLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Permet de modifier un site après son installation. Spécifie les langues à supprimer qui ne seront plus disponibles pour la console Configuration Manager, les rapports et les objets Configuration Manager. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** DeleteClientLanguages  

    -   **Obligatoire :** Non  

    -   **Valeurs :** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK ou ZHH  

    -   **Détails :** Permet de modifier un site après son installation. Spécifie les langues à supprimer qui ne seront plus disponibles sur les ordinateurs clients. L'anglais est disponible par défaut et ne peut pas être supprimé.  

-   **Nom de clé :** MobileDeviceLanguage  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si les langues du client de l'appareil mobile sont installées.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName   

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom du serveur SQL*>  

    -   **Détails :** Spécifie le nom du serveur ou de l’instance en cluster exécutant SQL Server qui hébergera la base de données du site.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de la base de données du site*> ou <*Nom de l’instance*>\\<*Nom de la base de données du site*>  

    -   **Détails :** Spécifie le nom de la base de données SQL Server à créer ou à utiliser lorsque vous installez la base de données du site principal.  

        > [!IMPORTANT]  
        >  Si vous n’utilisez pas l’instance par défaut, vous devez spécifier le nom d’instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Numéro du port SSB*>  

    -   **Détails :** Spécifie le port SSB utilisé par SQL Server. SSB est généralement configuré pour utiliser le port TCP 4022, mais vous pouvez configurer un autre port.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .mdb de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .mdb de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .ldf de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .ldf de la base de données.  

**HierarchyExpansionOption**  

-   **Nom de clé :** CCARSiteServer  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Nom de domaine complet du site d’administration centrale*>  

    -   **Détails :** Spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Spécifiez le site d’administration centrale lors de l’installation.  

-   **Nom de clé :** CASRetryInterval  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*intervalle*>  

    -   **Détails :** Spécifie l'intervalle (en minutes) avant une nouvelle tentative de connexion au site d'administration centrale après un échec de connexion. Par exemple, en cas d’échec de la connexion au site d’administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour la valeur **CASRetryInterval** et réessaye d’établir la connexion.  

-   **Nom de clé :** WaitForCASTimeout  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*délai_attente*>  

         Valeur de **0** à **100**  

    -   **Détails :** Spécifie la valeur de délai d'attente maximal (en minutes) pour qu'un site principal se connecte au site d'administration centrale. Par exemple, en cas d’échec de la connexion d’un site principal à un site d’administration centrale, le site principal réessaye d’établir la connexion en fonction de la valeur de **CASRetryInterval** jusqu’à ce que le délai **WaitForCASTimeout** soit atteint. Vous pouvez spécifier une valeur entre **0** et **100**.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie s’il convient d’installer un point de connexion de service sur ce site. Comme le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être **0** pour un site principal enfant.  

-   **Nom de clé :** CloudConnectorServer  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur de point de connexion de service*\>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site du point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si le point de connexion de service utilise un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** Obligatoire quand **UseProxy** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur proxy*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur proxy utilisé par le point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** Obligatoire quand **UseProxy** est égal à 1  

    -   **Valeurs :** <*Numéro de port*>  

    -   **Détails :** Spécifie le numéro de port à utiliser pour le port proxy.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Récupération sans assistance d’un site d’administration centrale  
 Utilisez les détails suivants pour récupérer un site d’administration centrale à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** RecoverCCAR  

    -   **Détails :** Récupère un site d’administration centrale.  

-   **Nom de clé :** CDLatest  

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest folder.    

    -   **Valeurs :** 1. Toute autre valeur que 1 est considérée comme signifiant que CD.Latest.

    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**RecoveryOptions**  

-   **Nom de clé :** ServerRecoveryOptions  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 1, 2 ou 4  

         1 = Récupérer le serveur de site et SQL Server.  

         2 = Récupérer le serveur de site uniquement.  

         4 = Récupérer SQL Server uniquement.  

    -   **Détails :** Spécifie si le programme d’installation récupère le serveur de site, SQL Server, ou les deux. Les clés associées sont nécessaires quand vous définissez la valeur suivante pour le paramètre **ServerRecoveryOptions** :  

        -   Valeur = 1 : Vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 2 : Vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 4 : la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.  

-   **Nom de clé :** DatabaseRecoveryOptions  

    -   **Obligatoire :** Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.  

    -   **Valeurs :** 10, 20, 40 ou 80  

         10 = Restaurer la base de données du site à partir d'une sauvegarde.  

         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.  

         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  

         80 = Ignorer la récupération de base de données.  

    -   **Détails :** Spécifie comment le programme d’installation récupère la base de données de site dans SQL Server.  

-   **Nom de clé :** ReferenceSite  

    -   **Obligatoire :** Cette clé est requise lorsque le paramètre **DatabaseRecoveryOptions** a la valeur **40**.  

    -   **Valeurs :** <*Nom de domaine complet du site de référence*>  

    -   **Détails :** Spécifie le site principal de référence que le site d’administration centrale utilise pour récupérer des données globales si la sauvegarde de base de données est antérieure à la période de rétention du suivi des modifications ou lorsque vous récupérez le site sans sauvegarde.  

         Quand vous ne spécifiez pas de site de référence et que la sauvegarde est antérieure à la période de rétention du suivi des modifications, tous les sites principaux sont réinitialisés avec les données restaurées à partir du site d’administration centrale.  

         Quand vous ne spécifiez pas de site de référence et que la sauvegarde est comprise dans la période de rétention du suivi des modifications, seules les modifications effectuées après la sauvegarde sont répliquées à partir des sites principaux. Lorsqu'il existe des conflits entre des modifications issues de différents sites principaux, le site d'administration centrale utilise la première modification reçue.  

-   **Nom de clé :** SiteServerBackupLocation  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du jeu de sauvegarde du serveur de site*>  

    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde du serveur de site. Cette clé est facultative si le paramètre **ServerRecoveryOptions** a la valeur **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

-   **Nom de clé :** BackupLocation  

    -   **Obligatoire :** Cette clé est obligatoire quand vous configurez la valeur **1** ou **4** pour la clé **ServerRecoveryOptions**, et la valeur **10** pour la clé **DatabaseRecoveryOptions**.  

    -   **Valeurs :** <*Chemin du jeu de sauvegarde de la base de données du site*>  

    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde de la base de données du site.  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *ou* Eval  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Code de site*>  

    -   **Détails :** Spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie. Indiquez le code de site que le site utilisait avant la défaillance.

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Nom de site*>  

    -   **Détails :** Spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin d’installation de Configuration Manager*>  

    -   **Détails :** Spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui héberge le fournisseur SMS. Spécifiez le serveur qui hébergeait le fournisseur SMS avant la défaillance.  

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale. Pour plus d’informations sur le fournisseur SMS, consultez [Planifier le fournisseur SMS pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Télécharger  

         1 = Déjà téléchargé  

    -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin des fichiers nécessaires au programme d’installation*>  

    -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  
    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas participer  

         1 = Participer  

    -   **Détails :** Spécifie s’il convient de participer au programme d’amélioration des services.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName   

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom du serveur SQL*>  

    -   **Détails :** Spécifie le nom du serveur ou de l’instance en cluster exécutant SQL Server et qui héberge la base de données du site. Spécifiez le serveur qui a hébergé la base de données de site avant la défaillance.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de la base de données du site*> ou <*Nom de l’instance*>\\<*Nom de la base de données du site*>  

    -   **Détails :** Spécifie le nom de la base de données SQL Server à créer ou de la base de données SQL Server à utiliser pour installer la base de données du site d’administration centrale. Spécifiez le nom de base de données qui était utilisé avant la défaillance.  

        > [!IMPORTANT]  
        >  Si vous n’utilisez pas l’instance par défaut, vous devez spécifier le nom d’instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Numéro du port SSB*>  

    -   **Détails :** Spécifie le port SSB utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022. Spécifiez le port SSB utilisé avant la défaillance.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .mdb de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .mdb de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .ldf de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .ldf de la base de données.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie s’il convient d’installer un point de connexion de service sur ce site. Comme le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être **0** pour un site principal enfant.  

-   **Nom de clé :** CloudConnectorServer  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur de point de connexion de service*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site du point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si le point de connexion de service utilise un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur proxy*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur proxy utilisé par le point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Numéro de port*>  

    -   **Détails :** Spécifie le numéro de port à utiliser pour le port proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Récupération sans assistance d’un site principal  
 Utilisez les détails suivants pour récupérer un site principal à l’aide d’un fichier de script d’installation sans assistance.  

**Identification**  

-   **Nom de clé :** Action  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*RecoverPrimarySite*>  

    -   **Détails :** Récupère un site principal.  

-   **Nom de clé :** CDLatest  

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest folder.    

    -   **Valeurs :** 1. Toute autre valeur que 1 est considérée comme signifiant que CD.Latest.

    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.    

**RecoveryOptions**  

-   **Nom de clé :** ServerRecoveryOptions  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 1, 2 ou 4  

         1 = Récupérer le serveur de site et SQL Server.  

         2 = Récupérer le serveur de site uniquement.  

         4 = Récupérer SQL Server uniquement.  

    -   **Détails :** Spécifie si le programme d’installation récupère le serveur de site, SQL Server, ou les deux. Les clés associées sont nécessaires quand vous définissez la valeur suivante pour le paramètre **ServerRecoveryOptions** :  

        -   Valeur = 1 : Vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 2 : Vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l’aide d’une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

        -   Valeur = 4 : la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.  

-   **Nom de clé :** DatabaseRecoveryOptions  

    -   **Obligatoire :** Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.  

    -   **Valeurs :** 10, 20, 40 ou 80  

         10 = Restaurer la base de données du site à partir d'une sauvegarde.  

         20 = Utiliser une base de données de site qui a été récupérée manuellement à l'aide d'une autre méthode.  

         40 = Créer une nouvelle base de données de site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  

         80 = Ignorer la récupération de base de données.  

    -   **Détails :** Spécifie comment le programme d’installation récupère la base de données de site dans SQL Server.  

-   **Nom de clé :** SiteServerBackupLocation  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du jeu de sauvegarde du serveur de site*>  

    -   **Détails :**  

         Spécifie le chemin d'accès au jeu de sauvegarde du serveur de site. Cette clé est facultative si le paramètre **ServerRecoveryOptions** a la valeur **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.  

-   **Nom de clé :** BackupLocation  

    -   **Obligatoire :** Cette clé est obligatoire quand vous configurez la valeur **1** ou **4** pour la clé **ServerRecoveryOptions**, et la valeur **10** pour la clé **DatabaseRecoveryOptions**.  

    -   **Valeurs :** <*Chemin du jeu de sauvegarde de la base de données du site*>  

    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde de la base de données du site.  

**Options**  

-   **Nom de clé :** ProductID  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* ou *Eval*  

    -   **Détails :** Spécifie la clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  

-   **Nom de clé :** SiteCode  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Code de site*>  

    -   **Détails :** Spécifie les trois caractères alphanumériques qui identifient le site de manière unique dans votre hiérarchie. Indiquez le code de site que le site utilisait avant la défaillance.

-   **Nom de clé :** SiteName  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Nom de site*>  

    -   **Détails :** Spécifie le nom de ce site.  

-   **Nom de clé :** SMSInstallDir  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin d’installation de Configuration Manager*>  

    -   **Détails :** Spécifie le dossier d’installation des fichiers programmes de Configuration Manager.  

-   **Nom de clé :** SDKServer  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de domaine complet du fournisseur SMS*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui héberge le fournisseur SMS. Spécifiez le serveur qui hébergeait le fournisseur SMS avant la défaillance. Configurez d’autres fournisseurs SMS pour le site après l’installation initiale. Pour plus d’informations sur le fournisseur SMS, consultez [Planifier le fournisseur SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nom de clé :** PrerequisiteComp  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Télécharger  

         1 = Déjà téléchargé  

    -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur **0**, le programme d’installation télécharge les fichiers.  

-   **Nom de clé :** PrerequisitePath  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Chemin des fichiers nécessaires au programme d’installation*>  

    -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.  

-   **Nom de clé :** AdminConsole  

    -   **Obligatoire :** Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si la console Configuration Manager doit ou non être installée.  

-   **Nom de clé :** JoinCEIP  
    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas participer  

         1 = Participer  

    -   **Détails :** Spécifie s’il convient de participer au programme d’amélioration des services.  

**SQLConfigOptions**  

-   **Nom de clé :** SQLServerName   

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom du serveur SQL*>  

    -   **Détails :** Spécifie le nom du serveur ou de l’instance en cluster exécutant SQL Server et qui héberge la base de données du site. Spécifiez le serveur qui a hébergé la base de données de site avant la défaillance.  

-   **Nom de clé :** DatabaseName  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Nom de la base de données du site*> ou <*Nom de l’instance*>\\<*Nom de la base de données du site*>

    -   **Détails :**  

         Spécifie le nom de la base de données SQL Server à créer ou de la base de données SQL Server à utiliser pour installer la base de données du site d’administration centrale. Spécifiez le nom de base de données qui était utilisé avant la défaillance.  

        > [!IMPORTANT]  
        >  Si vous n’utilisez pas l’instance par défaut, vous devez spécifier le nom d’instance et le nom de base de données de site.  

-   **Nom de clé :** SQLSSBPort  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** <*Numéro du port SSB*>  

    -   **Détails :** Spécifie le port SSB utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022. Spécifiez le port SSB utilisé avant la défaillance.  

-   **Nom de clé :** SQLDataFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .mdb de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .mdb de la base de données.  

-   **Nom de clé :** SQLLogFilePath  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*Chemin du fichier .ldf de la base de données*>  

    -   **Détails :** Spécifie un autre emplacement pour créer le fichier .ldf de la base de données.  

**HierarchyExpansionOptions**  

-   **Nom de clé :** CCARSiteServer  

    -   **Obligatoire :** Voir les détails.  

    -   **Valeurs :** <*Code du site d’administration centrale*>  

    -   **Détails :** Spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Ce paramètre est requis si le site principal était attaché à un site d'administration centrale avant la défaillance. Spécifiez le code de site qui était utilisé pour le site d’administration centrale avant la défaillance.  

-   **Nom de clé :** CASRetryInterval  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*intervalle*>  

    -   **Détails :** Spécifie l'intervalle (en minutes) avant une nouvelle tentative de connexion au site d'administration centrale après un échec de connexion. Par exemple, en cas d’échec de la connexion au site d’administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour la valeur **CASRetryInterval** et réessaye d’établir la connexion.  

-   **Nom de clé :** WaitForCASTimeout  

    -   **Obligatoire :** Non  

    -   **Valeurs :** <*délai_attente*>  

    -   **Détails :** Spécifie la valeur de délai d'attente maximal (en minutes) pour qu'un site principal se connecte au site d'administration centrale. Par exemple, en cas d’échec de la connexion d’un site principal à un site d’administration centrale, le site principal réessaye d’établir la connexion en fonction de la valeur de **CASRetryInterval** jusqu’à ce que le délai **WaitForCASTimeout** soit atteint. Vous pouvez spécifier une valeur entre **0** et **100**.  

**CloudConnectorOptions**  

-   **Nom de clé :** CloudConnector  

    -   **Obligatoire :** Oui  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie s’il convient d’installer un point de connexion de service sur ce site. Comme le point de connexion de service peut uniquement être installé sur le site de niveau supérieur d’une hiérarchie, cette valeur doit être **0** pour un site principal enfant.  

-   **Nom de clé :** CloudConnectorServer  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur de point de connexion de service*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur qui hébergera le rôle de système de site du point de connexion de service.  

-   **Nom de clé :** UseProxy  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** 0 ou 1  

         0 = Ne pas installer  

         1 = Installer  

    -   **Détails :** Spécifie si le point de connexion de service utilise un serveur proxy.  

-   **Nom de clé :** ProxyName  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Nom de domaine complet du serveur proxy*>  

    -   **Détails :** Spécifie le nom de domaine complet du serveur proxy utilisé par le point de connexion de service.  

-   **Nom de clé :** ProxyPort  

    -   **Obligatoire :** Obligatoire quand **CloudConnector** est égal à 1  

    -   **Valeurs :** <*Numéro de port*>  

    -   **Détails :** Spécifie le numéro de port à utiliser pour le port proxy.  
