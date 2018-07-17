---
title: Configurer votre laboratoire
titleSuffix: Configuration Manager
description: Configurez un laboratoire pour évaluer Configuration Manager avec des activités réelles simulées.
ms.date: 09/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b1970688-0cd2-404f-a17f-9e2aa4a78758
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 14251bb062423a31bcf74d2079b2e1b667f61ba9
ms.sourcegitcommit: 06d490d526070e17d77e86bc6c200899ded911cb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38967162"
---
# <a name="set-up-your-system-center-configuration-manager-lab"></a>Configurer votre laboratoire de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En suivant les recommandations de cette rubrique, vous pourrez mettre en place un laboratoire pour évaluer Configuration Manager en simulant des activités réelles.  

##  <a name="BKMK_LabCore"></a> Composants principaux  
 La configuration de votre environnement pour System Center Configuration Manager requiert certains composants principaux pour prendre en charge l’installation de Configuration Manager.    

-   **L’environnement lab utilise Windows Server 2012 R2**, sur lequel nous allons installer System Center Configuration Manager.  

     Vous pouvez télécharger une version d’évaluation de Windows Server 2012 R2 à partir du [Centre d’évaluation TechNet](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012).  

     Envisagez de modifier ou de désactiver la configuration de sécurité renforcée d’Internet Explorer pour accéder plus facilement à certains téléchargements référencés tout au long de ces exercices. Consultez [Internet Explorer : Configuration de sécurité renforcée](https://technet.microsoft.com/library/dd883248\(v=ws.10\).aspx) .  

-   **L’environnement lab utilise SQL Server 2012 SP2** pour la base de données de site.  

     Vous pouvez télécharger une version d’évaluation de SQL Server 2012 à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=29066).  

     SQL Server a des [versions prises en charge de SQL Server](../../core/plan-design/configs/support-for-sql-server-versions.md#bkmk_SQLVersions) qui doivent être satisfaites pour pouvoir être utilisées avec System Center Configuration Manager.  

    -   Configuration Manager requiert une version 64 bits de SQL Server pour héberger la base de données de site.  

    -   **SQL_Latin1_General_CP1_CI_AS** en tant que classe **Classement SQL** .  

    -   **L’authentification Windows**, [au lieu de l’authentification SQL](https://technet.microsoft.com/library/ms144284.aspx), est obligatoire.  

    -   Une **instance SQL Server** dédiée est requise.  

    -   Ne limitez pas la **mémoire adressable système** pour SQL Server.  

    -   Configurez le **compte de service SQL Server** de sorte qu’il s’exécute avec un compte d’utilisateur de domaine doté de droits restreints.  

    -   Vous devez installer **SQL Server Reporting Services**.  

    -   **communications intersites** utilisent SQL Server Service Broker sur le port par défaut TCP 4022.  

    -   Les **communications intrasites** entre le moteur de base de données SQL Server et divers rôles de systèmes de site Configuration Manager utilisent par défaut le port TCP 1433.  

-   **Le contrôleur de domaine utilise Windows Server 2008 R2** avec Active Directory Domain Services. Le contrôleur de domaine fonctionne également en tant qu’hôte pour les serveurs DNS et DHCP à utiliser avec un nom de domaine complet.  

     Pour plus d’informations, consultez cette [vue d’ensemble des services de domaine Active Directory](https://technet.microsoft.com/library/hh831484).  

-   **Hyper-V est utilisé avec quelques machines virtuelles** pour vérifier que les opérations de gestion entreprises dans ces exercices fonctionnent comme prévu. Un minimum de trois machines virtuelles est recommandé quand Windows 7 (ou version ultérieure) est installé.  

     Pour plus d’informations, consultez cette [vue d’ensemble d’Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).  

-   **Les droits d’administrateur** sont obligatoires  pour tous ces composants.  

    -   Configuration Manager nécessite un administrateur avec des autorisations locales dans l’environnement Windows Server  

    -   Active Directory nécessite un administrateur avec des autorisations de modification du schéma  

    -   Les machines virtuelles nécessitent des autorisations locales sur les machines elles-mêmes  

Bien qu’elles ne soient pas requises pour ce laboratoire, vous pouvez consulter les [configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) pour plus d’informations sur la configuration requise pour implémenter System Center Configuration Manager. Reportez-vous à la documentation pour les versions logicielles autres que celles référencées ici.  

Une fois que vous avez installé tous ces composants, des étapes supplémentaires sont à suivre pour configurer votre environnement Windows pour Configuration Manager :  

##  <a name="BKMK_LabADPrep"></a> Préparer le contenu d’Active Directory pour le laboratoire  
 Pour ce laboratoire, vous allez créer un groupe de sécurité, puis lui ajouter un utilisateur de domaine.  

-   Groupe de sécurité : **Evaluation**  

    -   Étendue du groupe : **Universal**  

    -   Type de groupe : **Security**  

-   Utilisateur du domaine : **ConfigUser**  

     Dans des circonstances normales, vous n’accorderiez pas un accès universel à tous les utilisateurs au sein de votre environnement. Vous le faites ici avec cet utilisateur afin de rationaliser la mise en ligne de votre laboratoire.  

Les étapes suivantes requises pour permettre aux clients Configuration Manager d’interroger les services de domaine Active Directory pour localiser les ressources de site sont répertoriées dans les procédures suivantes.  

##  <a name="BKMK_CreateSysMgmtLab"></a> Créer le conteneur System Management  
 Configuration Manager ne crée pas automatiquement le conteneur System Management requis dans les services de domaine Active Directory quand le schéma est étendu. Par conséquent, vous allez le créer pour votre laboratoire. Dans cette étape, vous devez [installer l’Éditeur ADSI.](https://technet.microsoft.com/library/cc773354\(WS.10\).aspx#BKMK_InstallingADSIEdit)  

 Veillez à être connecté sous un compte possédant l’autorisation **Créer tous les objets enfants** sur le conteneur **System** dans les services de domaine Active Directory.  

#### <a name="to-create-the-system-management-container"></a>Pour créer le conteneur System Management :  

1.  Exécutez l' **Éditeur ADSI**et connectez-vous au domaine dans lequel réside le serveur de site.  

2.  Développez **Domaine&lt;nom_domaine_complet_ordinateur\>**, développez **<nom_unique\>**, cliquez avec le bouton droit sur **CN=System**, cliquez sur **Nouveau**, puis cliquez sur **Objet**.  

3.  Dans la boîte de dialogue **Créer un objet** , sélectionnez **Conteneur**et cliquez sur **Suivant**.  

4.  Dans le champ **Valeur** , tapez **System Management**, puis cliquez sur **Suivant**.  

5.  Cliquez sur **Terminer** pour terminer la procédure.  

##  <a name="BKMK_SetSecPermLab"></a> Définir les autorisations de sécurité pour le conteneur System Management  
 Accordez au compte d’ordinateur du serveur de site les autorisations nécessaires à la publication des informations de site sur le conteneur. Vous devez utiliser l’Éditeur ADSI pour cette tâche également.  

> [!IMPORTANT]  
>  Vérifiez que vous êtes connecté au domaine du serveur de site avant de commencer la procédure suivante.  

#### <a name="to-set-security-permissions-for-the-system-management-container"></a>Pour définir les autorisations de sécurité pour le conteneur System Management :  

1.  Dans le volet de la console, développez successivement le **domaine du serveur de site**, **DC=&lt;nom_unique_serveur\>**, puis **CN=System**. Cliquez avec le bouton droit sur **CN=System Management**, puis cliquez sur **Propriétés**.  

2.  Dans boîte de dialogue **CN=Propriétés de System Management** , cliquez sur l’onglet **Sécurité** , puis cliquez sur **Ajouter** pour ajouter le compte d’ordinateur du serveur de site. Accordez au compte les autorisations **Contrôle intégral** .  

3.  Cliquez sur **Avancé**, sélectionnez le compte d’ordinateur du serveur de site, puis cliquez sur **Modifier**.  

4.  Dans la liste **Appliquer à** , sélectionnez **Cet objet et tous ceux descendants**.  

5.  Cliquez sur **OK** pour fermer la console **Éditeur ADSI** et terminer la procédure.  

     Pour obtenir des informations supplémentaires sur cette procédure, consultez [Étendre le schéma Active Directory pour System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md)  

##  <a name="BKMK_ExtADSchLab"></a> Étendre le schéma Active Directory avec extadsch.exe  
 Vous allez étendre le schéma Active Directory pour ce laboratoire, car cela permet d’utiliser toutes les fonctions et fonctionnalités Configuration Manager avec une surcharge administrative minimale. L’extension du schéma Active Directory est une configuration à l’échelle de la forêt, qui ne peut être réalisée qu’une seule fois par forêt. L’extension du schéma modifie définitivement l’ensemble des classes et des attributs dans la configuration Active Directory de base. Cette action est irréversible. L’extension du schéma permet à Configuration Manager d’accéder aux composants qui lui permettront de fonctionner plus efficacement dans votre environnement de laboratoire.  

> [!IMPORTANT]  
>  Vérifiez que vous êtes connecté au contrôleur de domaine principal du schéma via un compte qui appartient au groupe de sécurité **Administrateurs du schéma** . Toute tentative d’utilisation d’autres informations d’identification échouera.  

#### <a name="to-extend-the-active-directory-schema-using-extadschexe"></a>Pour étendre le schéma Active Directory avec extadsch.exe :  

1.  Créez une sauvegarde de l’état système du contrôleur de domaine principal du schéma. Pour plus d’informations sur la sauvegarde d’un contrôleur de domaine principal, consultez [Sauvegarde de Windows Server](https://technet.microsoft.com/library/cc770757.aspx).  

2.  Accédez à **\SMSSETUP\BIN\X64** sur le support d’installation.  

3.  Exécutez **extadsch.exe**.  

4.  Pour vérifier que l’extension du schéma a réussi, passez en revue le fichier **extadsch.log** situé dans le dossier racine du lecteur système.  

     Pour obtenir des informations supplémentaires sur cette procédure, consultez [Étendre le schéma Active Directory pour System Center Configuration Manager](../../core/plan-design/network/extend-the-active-directory-schema.md).  

##  <a name="BKMK_OtherTasksLab"></a> Autres tâches requises  
 Vous devez également effectuer les tâches suivantes avant l’installation.  

 **Créer un dossier pour stocker tous les téléchargements**  

 Plusieurs téléchargements sont nécessaires pour obtenir les composants du support d’installation tout au long de cet exercice. Avant de commencer les procédures d’installation, déterminez un emplacement qui ne nécessite pas le déplacement de ces fichiers tant que vous souhaitez utiliser votre laboratoire. Il est recommandé d’utiliser un dossier unique avec des sous-dossiers distincts pour stocker ces téléchargements.  

 **Installer .NET et activer Windows Communication Foundation**  

 Vous devez installer deux infrastructures .NET : .NET 3.5.1 puis .NET 4.5.2+. Vous devez également activer Windows Communication Foundation (WCF). WCF est conçu pour offrir une approche gérable de l’informatique distribuée, une grande interopérabilité et une prise en charge directe de l’orientation service. Il simplifie le développement d’applications connectées via un modèle de programmation orienté service. Consultez [Qu’est-ce que Windows Communication Foundation ?](https://technet.microsoft.com/subscriptions/ms731082\(v=vs.90\).aspx) pour obtenir des informations supplémentaires sur WCF.  

#### <a name="to-install-net-and-activate-windows-communication-foundation"></a>Pour installer .NET et activer Windows Communication Foundation :  

1.  Ouvrez **Server Manager**, puis accédez à **Gérer**. Cliquez sur **Ajouter des rôles et fonctionnalités** pour ouvrir l’ **Ajouter des rôles et fonctionnalités Wizard**.  

2.  Passez en revue les informations fournies dans le panneau **Avant de commencer** , puis cliquez sur **Suivant**.  

3.  Sélectionnez **Installation basée sur un rôle ou une fonctionnalité**, puis cliquez sur **Suivant**.  

4.  Sélectionnez votre serveur à partir du **Pool de serveurs**, puis cliquez sur **Suivant**.  

5.  Examinez le panneau **Rôles de serveurs** , puis cliquez sur **Suivant**.  

6.  Ajoutez les **Fonctionnalités** suivantes en les sélectionnant dans la liste :  

    -   **Fonctionnalités de .NET Framework 3.5**  

        -   **.NET Framework 3.5 (inclut .NET 2.0 et 3.0)**  

    -   **Fonctionnalités de .NET Framework 4.5**  

        -   **.NET Framework 4.5**  

        -   **ASP.NET 4.5**  

        -   **Services WCF**  

            -   **Activation HTTP**  

            -   **Partage de port TCP**  

7.  Examinez l’écran **Rôle Serveur Web (IIS)** et **Services de rôle** , puis cliquez sur **Suivant**.  

8.  Examinez l’écran **Confirmation** , puis cliquez sur **Suivant**.  

9. Cliquez sur **Installer** et vérifiez que l’installation s’est déroulée correctement dans le volet **Notifications** du **Gestionnaire de serveur**.  

10. Une fois l’installation de base de .NET terminée, accédez au [Centre de téléchargement Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=42643) pour obtenir le programme d’installation web de .NET Framework 4.5.2. Cliquez sur le bouton **Télécharger** , puis sur **Exécuter** pour lancer le programme d’installation. Il détecte et installe automatiquement les composants nécessaires dans la langue sélectionnée.  

Pour plus d’informations, consultez les articles suivants qui expliquent pourquoi ces composants .NET Framework sont nécessaires :  

-   [Versions et dépendances du .NET Framework](https://technet.microsoft.com/library/bb822049.aspx)  

-   [Procédure pas à pas de vérification de la compatibilité des applications avec .NET Framework 4 RTM](https://technet.microsoft.com/library/dd889541.aspx)  

-   [Comment : mettre à niveau une application web ASP.NET vers ASP.NET 4](https://technet.microsoft.com/library/dd483478\(VS.100\).aspx)  

-   [Forum Aux Questions sur la politique de support - Microsoft .NET Framework](https://support.microsoft.com/en-us/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update)  

-   [Les coulisses du CLR – L’approche « In-Process Side-by-Side »](https://msdn.microsoft.com/magazine/ee819091.aspx)  

**Activer BITS, IIS et RDC**  

Le [service de transfert intelligent en arrière-plan (BITS)](https://technet.microsoft.com/library/dn282296.aspx) est utilisé pour les applications qui ont besoin de transférer de façon asynchrone des fichiers entre un client et un serveur. En contrôlant le flux des transferts au premier plan et en arrière-plan, le service BITS préserve la réactivité des autres applications réseau. Il reprend également automatiquement les transferts de fichiers en cas d’interruption d’une session de transfert.  

Vous devez installer le service BITS pour ce laboratoire, car ce serveur de site fera également office de point de gestion.  

Internet Information Services (IIS) est un serveur web flexible et évolutif, qui peut servir à héberger ce que vous voulez sur le web. Il est utilisé par Configuration Manager pour plusieurs rôles de système de site. Pour plus d’informations sur IIS, consultez [Sites web pour les serveurs de système de site dans System Center Configuration Manager](../../core/plan-design/network/websites-for-site-system-servers.md).  

La[compression différentielle à distance (RDC)](https://technet.microsoft.com/library/cc754372.aspx) est un ensemble d’API que les applications peuvent utiliser pour déterminer si des modifications ont été apportées à un ensemble de fichiers. La fonctionnalité RDC permet à l’application de répliquer uniquement les parties modifiées d’un fichier, limitant ainsi au maximum le trafic réseau.  

#### <a name="to-enable-bits-iis-and-rdc-site-server-roles"></a>Pour activer les rôles de serveur de site BITS, IIS et RDC :  

1.  Sur votre serveur de site, ouvrez **Server Manager**. Accédez à **Gérer**. Cliquez sur **Ajouter des rôles et fonctionnalités** pour ouvrir l’ **Assistant Ajout de rôles et de fonctionnalités**.  

2.  Passez en revue les informations fournies dans le panneau **Avant de commencer** , puis cliquez sur **Suivant**.  

3.  Sélectionnez **Installation basée sur un rôle ou une fonctionnalité**, puis cliquez sur **Suivant**.  

4.  Sélectionnez votre serveur à partir du **Pool de serveurs**, puis cliquez sur **Suivant**.  

5.  Ajoutez les **Rôles de serveur** suivants en les sélectionnant dans la liste :  

    -   **Serveur web (IIS)**  

        -   **Fonctionnalités HTTP communes**  

            -   **Document par défaut**  

            -   **Exploration des répertoires**  

            -   **Erreurs HTTP**  

            -   **Contenu statique**  

            -   **Redirection HTTP**  

        -   **Intégrité et diagnostics**  

            -   **Journalisation HTTP**  

            -   **Outils de journalisation**  

            -   **Observateur de demandes**  

            -   **Suivi**  

    -   **Performancess**  

        -   **Compression de contenu statique**  

        -   **Compression de contenu dynamique**  

    -   **Security**  

        -   **Filtrage des demandes**  

        -   **Authentification de base**  

        -   **Authentification par mappage de certificat client**  

        -   **Restrictions IP et de domaine**  

        -   **Autorisation URL**  

        -   **Autorisation Windows**  

    -   **Développement d’applications**  

        -   **Extensibilité .NET 3.5**  

        -   **Extensibilité .NET 4.5**  

        -   **ASP**  

        -   **ASP.NET 3.5**  

        -   **ASP.NET 4.5**  

        -   **Extensions ISAPI**  

        -   **Filtres ISAPI**  

        -   **Fichiers Include côté serveur**  

    -   **Serveur FTP**  

        -   **Service FTP**  

    -   **Outils de gestion**  

        -   **Console de gestion IIS**  

        -   **IIS 6 Management Compatibility**  

            -   **Compatibilité avec la métabase de données IIS 6**  

            -   **Console de gestion IIS 6**  

            -   **Outils de script IIS 6**  

            -   **Compatibilité WMI d'IIS 6**  

        -   **Scripts et outils de gestion d’IIS 6**  

        -   **Service d'administration**  

6.  Ajoutez les **Fonctionnalités** suivantes en les sélectionnant dans la liste :  

    -   **service de transfert intelligent en arrière-plan (BITS)**  

          -   **Extension de serveur IIS**  

    -   **Outils d'administration de serveur distant**  

          -   **Outils d’administration de fonctionnalités**  

          -   **Outils d’extensions du serveur BITS**  

7.  Cliquez sur **Installer** et vérifiez que l’installation s’est déroulée correctement dans le volet **Notifications** du **Gestionnaire de serveur**.  

Par défaut, le service IIS bloque l’accès via la communication HTTP ou HTTPS à plusieurs types d’extensions et d’emplacements de fichier. Pour permettre la distribution de ces fichiers sur les systèmes clients, vous devez configurer le filtrage des demandes pour IIS sur votre point de distribution. Pour plus d’informations, consultez [Filtrage des demandes IIS pour les points de distribution](../../core/plan-design/network/prepare-windows-servers.md#BKMK_IISFiltering).  

#### <a name="to-configure-iis-filtering-on-distribution-points"></a>Pour configurer le filtrage IIS sur les points de distribution :  

1.  Ouvrez **IIS Manager** et sélectionnez le nom de votre serveur dans la barre latérale. Vous accédez à l’écran **Accueil** .  

2.  Vérifiez que l’option **Affichage des fonctionnalités** est sélectionnée au bas de l’écran **Accueil** . Accédez à **IIS** et ouvrez **Filtrage des demandes**.  

3.  Dans le volet **Actions** , cliquez sur **Autoriser une extension de nom de fichier...**  

4.  Tapez **.msi** dans la boîte de dialogue et cliquez sur **OK**.  

##  <a name="BKMK_InstallCMLab"></a> Installation de Configuration Manager  
Vous allez [déterminer quand utiliser un site principal](../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md#BKMK_ChoosePriimary) pour gérer directement les clients. Cela permettra à votre environnement lab de prendre en charge la gestion de la [mise à l’échelle du système de site](/sccm/core/plan-design/configs/size-and-scale-numbers) des appareils potentiels.  
Au cours de ce processus, vous allez également installer la console Configuration Manager qui permettra de gérer vos appareils d’évaluation.  

Avant de commencer l’installation, lancez l’[outil de vérification des prérequis](/sccm/core/servers/deploy/install/prerequisite-checker) sur le serveur utilisant Windows Server 2012 pour confirmer que tous les paramètres ont été correctement activés.  

#### <a name="to-download-and-install-configuration-manager"></a>Pour télécharger et installer Configuration Manager :  

1.  Accédez à la page [System Center Évaluations](https://www.microsoft.com/evalcenter/evaluate-system-center-2012-configuration-manager-and-endpoint-protection) pour télécharger la dernière version d’évaluation de System Center Configuration Manager.  

2.  Décompressez le média de téléchargement dans votre emplacement prédéfini.  

3.  Suivez la procédure d’installation indiquée dans la rubrique [Installer un site à l’aide de l’Assistant Installation de System Center Configuration Manager](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites). Dans cette procédure, vous allez entrer les éléments suivants :  

    |Étape de la procédure d’installation de site|Sélection|  
    |-----------------------------------------|---------------|  
    |Étape 4 : la page **Clé du produit**|Sélectionnez **Évaluation**.|  
    |Étape 7 :  **Téléchargements requis**|Sélectionnez **Télécharger les fichiers requis** et spécifier votre emplacement prédéfini.|  
    |Étape 10 : **Paramètres d’installation et du site**|-   **Code du site :LAB**<br />-   **Nom du site :Evaluation**<br />-   **Dossier d’installation :** spécifiez votre emplacement prédéfini.|  
    |Étape 11 : **Installation du site principal**|Sélectionnez **Installer le site principal en tant que site autonome**, puis cliquez sur **Suivant**.|  
    |Étape 12 : **Installation de la base de données**|-   **Nom du serveur SQL Server (nom de domaine complet) :** entrez ici votre nom de domaine complet.<br />-   **Nom de l’instance :** laissez ce champ vide, car vous utiliserez l’instance par défaut de SQL que vous avez installée précédemment.<br />-   **Port Service Broker :** conservez le port par défaut 4022.|  
    |Étape 13 : **Installation de la base de données**|Conservez ces paramètres par défaut.|  
    |Étape 14 : **Fournisseur SMS**|Conservez ces paramètres par défaut.|  
    |Étape 15 : **Paramètres de communication client**|Assurez-vous que l’option **Tous les rôles de système de site acceptent uniquement les communications HTTPS depuis les clients** n’est pas sélectionnée.|  
    |Étape 16 : **Rôles système de site**|Entrez votre nom de domaine complet et assurez-vous que l’option **Tous les rôles de système de site acceptent uniquement les communications HTTPS depuis les clients** est toujours désactivée.|  

##  <a name="BKMK_EnablePubLab"></a> Activer la publication pour le site Configuration Manager  
Chaque site Configuration Manager publie ses propres informations de site sur le conteneur System Management, au sein de sa partition de domaine dans le schéma Active Directory. Des canaux bidirectionnels pour la communication entre Active Directory et Configuration Manager doivent être ouverts pour gérer ce trafic. Vous devez également activer la fonctionnalité Découverte de forêts pour déterminer certains composants de votre infrastructure réseau et Active Directory.  

#### <a name="to-configure-active-directory-forests-for-publishing"></a>Pour configurer des forêts Active Directory pour la publication :  

1.  Dans le coin inférieur gauche de la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l’espace de travail **Administration** , développez **Configuration de la hiérarchie**, puis cliquez sur **Méthodes de découverte**.  

3.  Sélectionnez **Découverte de forêts Active Directory** et cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** , sélectionnez **Activer la découverte de forêts Active Directory**. Une fois cette option activée, sélectionnez **Créer automatiquement les limites de site Active Directory lorsqu’elles sont découvertes**. Une boîte de dialogue s’affiche indiquant **Voulez-vous exécuter la découverte complète dès que possible ?** Cliquez sur **Oui**.  

5.  Dans le groupe **Méthode de découverte** en haut de l’écran, cliquez sur **Exécuter la découverte de forêt maintenant**, puis accédez à **Forêts Active Directory** dans la barre latérale. Votre forêt Active Directory doit figurer dans la liste des forêts découvertes.  

6.  Accédez à la partie supérieure de l’écran, sous l’onglet **Général** .  

7.  Dans l’espace de travail **Administration** , développez **Configuration de la hiérarchie**, puis cliquez sur **Forêts Active Directory**.  

#### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-your-active-directory-forest"></a>Pour permettre à un site Configuration Manager de publier des informations de site vers votre forêt Active Directory :  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Vous allez configurer une nouvelle forêt qui n’a pas encore été découverte.  

3.  Dans l'espace de travail **Administration** , cliquez sur **Forêts Active Directory**.  

4.  Sous l’onglet **Publication** des propriétés du site, sélectionnez votre forêt connectée, puis cliquez sur **OK** pour enregistrer la configuration.
