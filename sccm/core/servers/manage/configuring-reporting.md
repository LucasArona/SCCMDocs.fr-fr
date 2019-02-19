---
title: Configurer les rapports
titleSuffix: Configuration Manager
description: Découvrez comment configurer la génération de rapports dans votre hiérarchie Configuration Manager, y compris des informations sur SQL Server Reporting Services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c65c85c6ec340fe595efa3bfd403e3c8d1d6a017
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134671"
---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>Configuration des rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de créer, modifier et exécuter des rapports dans la console System Center Configuration Manager, vous devez effectuer certaines tâches de configuration. Aidez-vous des sections de cette rubrique pour configurer la génération de rapports dans votre hiérarchie Configuration Manager :  

 Avant de procéder à l’installation et à la configuration de Reporting Services dans votre hiérarchie, passez en revue les rubriques suivantes sur la génération de rapports Configuration Manager :  

-   [Présentation des rapports dans System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Planification de la création de rapports dans System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services est une plate-forme d'édition de rapport basée sur un serveur qui fournit des fonctionnalités complètes de création de rapports pour une variété de sources de données. Le point de Reporting Services dans Configuration Manager communique avec SQL Server Reporting Services pour copier les rapports Configuration Manager dans un dossier de rapports spécifié, configurer les paramètres de Reporting Services et configurer les paramètres de sécurité de Reporting Services. Reporting Services se connecte à la base de données de site Configuration Manager pour récupérer les données qui sont renvoyées quand vous exécutez des rapports.  

 Avant d’installer le point de Reporting Services dans un site Configuration Manager, vous devez installer et configurer SQL Server Reporting Services sur le système de site qui héberge le rôle de système de site du point de Reporting Services. Pour plus d'informations sur l'installation de Reporting Services, consultez la [bibliothèque TechNet de SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Utilisez la procédure suivante pour vérifier que SQL Server Reporting Services est installé et fonctionne correctement.  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>Pour vérifier que SQL Server Reporting Services est installé et en cours d'exécution  

1.  Sur le Bureau, cliquez sur **Démarrer**, **Tous les programmes**, **Microsoft SQL Server 2008 R2**, **Outils de configuration**, puis sur **Gestionnaire de configuration de Reporting Services**.  

2.  Dans la boîte de dialogue **Connexion relative à la configuration de Reporting Services** , spécifiez le nom du serveur hôte de SQL Server Reporting Services. Dans le menu déroulant, sélectionnez l'instance de SQL Server sur laquelle vous avez installé SQL Reporting Services, puis cliquez sur **Se connecter**. Le Gestionnaire de Configuration de Reporting Services s'ouvre.  

3.  Sur la page **État du service de rapport** , vérifiez que l'option **État de Report Server** est définie sur **Démarré**. Sinon, cliquez sur **Démarrer**.  

4.  Sur la page **URL du service Web** , cliquez sur l'URL dans **URL du service Web de service e rapport** pour tester la connexion au dossier de rapport. La boîte de dialogue **Sécurité de Windows** peut s'ouvrir et vous demander vos informations d'identification de sécurité. Par défaut, votre compte d'utilisateur s'affiche. Entrez votre mot de passe, puis cliquez sur **OK**. Vérifiez que la page Web s'ouvre correctement. Fermez la fenêtre du navigateur.  

5.  Sur la page **Base de données** , vérifiez que le paramètre **Mode du serveur de rapports** est configuré sur **Natif**.  

6.  Sur la page **URL du Gestionnaire de rapports** , cliquez sur l'URL dans **Identification du site du Gestionnaire de rapports** pour tester la connexion au répertoire virtuel du Gestionnaire de rapports. La boîte de dialogue **Sécurité de Windows** peut s'ouvrir et vous demander vos informations d'identification de sécurité. Par défaut, votre compte d'utilisateur s'affiche. Entrez votre mot de passe, puis cliquez sur **OK**. Vérifiez que la page Web s'ouvre correctement. Fermez la fenêtre du navigateur.  

    > [!NOTE]  
    >  Le Gestionnaire de rapports de Reporting Services n’est pas nécessaire à la génération de rapports dans Configuration Manager, mais il l’est si vous voulez exécuter des rapports sur un navigateur Internet ou gérer des rapports à l’aide du Gestionnaire de rapports.  

7.  Cliquez sur **Quitter** pour fermer le Gestionnaire de configuration de Reporting Services.  

##  <a name="BKMK_ReportBuilder3"></a> Configuration de Reporting pour utiliser le Générateur de rapports 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>Pour modifier le nom de manifeste Générateur de rapports en Générateur de rapports 3.0  

1.  Sur l’ordinateur exécutant la console Configuration Manager, ouvrez l’Éditeur de Registre Windows.  

2.  Accédez à **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Cliquez deux fois sur la clé **ReportBuilderApplicationManifestName** pour modifier les données de valeur.  

4.  Modifiez **ReportBuilder_2_0_0_0.application** en **ReportBuilder_3_0_0_0.application**, puis cliquez sur **OK**.  

5.  Fermez l'Éditeur de Registre Windows.  

##  <a name="BKMK_InstallReportingServicesPoint"></a> Installation d’un point de Reporting Services  
 Le point de Reporting Services doit être installé sur un site pour gérer les rapports sur le site. Le point de Reporting Services copie les dossiers de rapports et les rapports vers SQL Server Reporting Services, applique la stratégie de sécurité des rapports et des dossiers, et définit des paramètres de configuration dans Reporting Services. L’affichage des rapports dans la console Configuration Manager et leur gestion dans Configuration Manager passent par la configuration préalable d’un point de Reporting Services. Le point de Reporting Services est un rôle de système de site qui doit être configuré sur un serveur sur lequel Microsoft SQL Server Reporting Services est installé et en cours d'exécution. Pour plus d’informations sur la configuration requise, consultez [Configuration requise pour la création de rapports](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  Lors de la sélection d'un site pour installer le point de Reporting Services, n'oubliez pas que les utilisateurs qui accèderont aux rapports devront se trouver dans la même étendue de sécurité que le site où le point de Reporting Services est installé.  

> [!NOTE]  
>  Après avoir installé un point de Reporting Services sur un système de site, ne modifiez pas l'URL du serveur de rapports. Par exemple, si vous créez le point de Reporting Services, puis que vous modifiez l’URL du serveur de rapports dans le Gestionnaire de configuration de Reporting Services, la console Configuration Manager continuera d’utiliser l’ancienne URL, et vous ne pourrez pas exécuter, modifier ou créer de rapports à partir de la console. Lorsque vous devez modifier une URL du serveur de rapports, supprimez le point de Reporting Services, modifiez l'URL, puis réinstallez le point de Reporting Services.  

> [!IMPORTANT]    
> Lorsque vous installez un point de Reporting Services, vous devez spécifier un compte du point de Reporting Services. Plus tard, lorsque les utilisateurs d’un autre domaine tenteront d’exécuter un rapport, le rapport ne pourra pas s’exécuter, sauf s’il existe une relation d’approbation bidirectionnelle entre les domaines.

 Utilisez la procédure suivante pour installer le point de Reporting Services.  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>Pour installer le point de Reporting Services sur un système de site  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.  

    > [!TIP]  
    >  Pour répertorier uniquement les systèmes de site hébergeant le rôle de site du point de Reporting Services, cliquez avec le bouton droit sur **Serveurs et rôles de système de site** pour sélectionner **Point de Reporting Services**.  

3.  Ajoutez le rôle de système de site du point de Reporting Services à un serveur de système de site nouveau ou existant en utilisant l'étape correspondante :  

    > [!NOTE]  
    >  Pour plus d’informations sur la configuration de systèmes de site, consultez [Ajouter des rôles de système de site pour System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **Nouveau système de site** : Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**. L'Assistant **Création d'un serveur de système de site** s'ouvre.  

    -   **Système de site existant** : Cliquez sur le serveur sur lequel vous souhaitez installer le rôle de système de site du point de Reporting Services. Lorsque vous cliquez sur un serveur, la liste des rôles de système de site déjà installés sur le serveur s'affiche dans le panneau des résultats.  

         Sur l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**. L'Assistant **Ajout des rôles de système de site** s'ouvre.  

4.  Sur la page **Général** , spécifiez les paramètres généraux du serveur de système de site. Lorsque vous ajoutez le point de Reporting Services à un serveur de système de site existant, vérifiez les valeurs qui ont été précédemment configurées.  

5.  Sur la page **Sélection du rôle système** , sélectionnez **Point Reporting Services** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.  

6.  Sur la page **Point de Reporting Services** , configurez les paramètres suivants :  

    -   **Nom du serveur de base de données du site** : Spécifiez le nom du serveur qui héberge la base de données du site Configuration Manager. En règle générale, l'Assistant récupère automatiquement le nom de domaine complet (FQDN) du serveur. Pour spécifier une instance de base de données, utilisez le format &lt;*nom_serveur*>\&lt;*nom_instance*>.  

    -   **Nom de la base de données** : Spécifiez le nom de la base de données du site Configuration Manager, puis cliquez sur **Vérifier** pour confirmer que l’assistant a accès à la base de données du site.  

        > [!IMPORTANT]  
        >  Le compte d'utilisateur qui crée le point de Reporting Services doit avoir accès **en lecture** à la base de données de site. Si le test de connexion échoue, une icône d'avertissement rouge s'affiche. Déplacez le curseur sur cette icône afin de lire les informations relatives à la défaillance. Corrigez la défaillance, puis cliquez à nouveau sur **Tester** .  

    -   **Nom du dossier** : Spécifiez le nom de dossier qui est créé et utilisé pour héberger les rapports Configuration Manager dans Reporting Services.  

    -   **Instance du serveur Reporting Services** : Sélectionnez dans la liste l'instance de SQL Server pour Reporting Services. Lorsqu'une seule instance est trouvée, par défaut, elle est répertoriée et sélectionnée. Lorsqu'aucune instance n'est trouvée, vérifiez que SQL Server Reporting Services est installé et configuré, et que le service SQL Server Reporting Services est démarré sur le système de site.  

        > [!IMPORTANT]  
        >  Configuration Manager établit une connexion dans le contexte de l’utilisateur actif avec Windows Management Instrumentation (WMI) sur le système de site sélectionné pour récupérer l’instance de SQL Server pour Reporting Services. L'utilisateur actuel doit disposer d'un accès **Lecture** à WMI sur le système de site, sans quoi, les instances de Reporting Services ne peuvent pas être récupérées.  

    -   **Compte du point de Reporting Services** : Cliquez sur **Définir**, puis sélectionnez le compte à utiliser quand SQL Server Reporting Services sur le point de Reporting Services se connecte à la base de données du site Configuration Manager pour récupérer les données qui s’affichent dans un rapport. Sélectionnez **Compte existant** pour spécifier un compte d’utilisateur Windows déjà configuré en tant que compte Configuration Manager ou sélectionnez **Nouveau compte** pour spécifier un compte d’utilisateur Windows qui n’est pas actuellement configuré en tant que compte Configuration Manager. Configuration Manager accorde automatiquement l’accès à la base de données du site pour l’utilisateur spécifié. L'utilisateur est affiché dans le sous-dossier **Comptes** du nœud **Sécurité** dans l'espace de travail **Administration** avec le nom de compte **Point Reporting Services ConfigMgr** .  

         Le compte qui exécute Reporting Services doit appartenir au groupe de sécurité de domaine local **Groupe d'accès d'autorisation Windows**et l'autorisation **Read tokenGroupsGlobalAndUniversal** doit être définie sur **Autoriser**. Il doit y avoir une relation d’approbation bidirectionnelle pour les utilisateurs d’un domaine différent de celui du compte du point de Reporting Services pour pouvoir exécuter des rapports.

         Le compte d'utilisateur Windows et le mot de passe spécifiés sont chiffrés et stockés dans la base de données Reporting Services. Reporting Services récupère les données de rapports à partir de la base de données de site à l'aide de ce compte et de ce mot de passe.  

        > [!IMPORTANT]  
        >  Le compte que vous spécifiez doit disposer d'une autorisation **Connexion locale** sur l'ordinateur hébergeant la base de données Reporting Services.  

7.  Sur la page **Point Reporting Services** , cliquez sur **Suivant**.  

8.  Sur la page **Résumé** , vérifiez les paramètres, puis cliquez sur **Suivant** pour installer le point de Reporting Services.  

     Une fois l’Assistant complété, des dossiers de rapports sont créés, et les rapports Configuration Manager sont copiés dans les dossiers de rapports spécifiés.  

    > [!NOTE]  
    >  Quand les dossiers de rapports sont créés et que les rapports sont copiés sur le serveur de rapports, Configuration détermine la langue adéquate pour les objets. Si le module linguistique correspondant est installé sur le site, Configuration Manager crée les objets dans la langue du système d’exploitation s’exécutant sur le serveur de rapports du site. Si la langue n'est pas disponible, les rapports sont créés et affichés en anglais. Lorsque vous installez un point de Reporting Services sur un site sans module linguistique, les rapports sont installés en anglais. Si vous installez un module linguistique après avoir installé le point de Reporting Services, vous devez désinstaller et réinstaller ce dernier pour que les rapports soient disponibles dans la langue du module linguistique adéquat. Pour plus d’informations sur les modules linguistiques, consultez [Modules linguistiques dans System Center Configuration Manager](../deploy/install/language-packs.md).  

###  <a name="BKMK_FileInstallationAndSecurity"></a> Installation de fichier et droits de sécurité du dossier de rapport  
 Configuration Manager effectue les actions suivantes pour installer le point de Reporting Services et configurer Reporting Services :  

> [!IMPORTANT]  
>  Les actions dans la liste suivante sont effectuées en utilisant les informations d'identification du compte configuré pour le service SMS_Executive, qui correspond généralement au compte système local du serveur de site.  

- Installe le rôle de site de point de Reporting Services.  

- Crée la source de données dans Reporting Services avec les informations d'identification stockées que vous avez spécifiées dans l'Assistant. Il s'agit du compte d'utilisateur Windows et du mot de passe que Reporting Services utilise pour se connecter à la base de données de site lorsque vous exécutez des rapports.  

- Crée le dossier racine de Configuration Manager dans Reporting Services.  

- Ajoute les rôles de sécurité **Utilisateurs de rapports ConfigMgr** et **Administrateurs de rapport ConfigMgr** dans Reporting Services.  

- Crée des sous-dossiers et déploie les rapports Configuration Manager de %ProgramFiles%\SMS_SRSRP vers Reporting Services.  

- Ajoute le rôle **Utilisateurs de rapports ConfigMgr** de Reporting Services aux dossiers racine pour tous les comptes d’utilisateurs de Configuration Manager qui disposent de droits de **lecture de site**.  

- Ajoute le rôle **Administrateurs de rapport ConfigMgr** de Reporting Services aux dossiers racine pour tous les comptes d’utilisateurs de Configuration Manager qui disposent de droits de **modification de site**.  

- Récupère le mappage entre les dossiers de rapports et les types d’objets sécurisés Configuration Manager (conservés dans la base de données de site Configuration Manager).  

- Configure les droits suivants pour les utilisateurs administratifs de Configuration Manager sur des dossiers de rapports spécifiques de Reporting Services :  

  - Ajoute les utilisateurs et attribue le rôle **Utilisateurs de rapports ConfigMgr** au dossier de rapports associé pour les utilisateurs administratifs qui disposent d’autorisations **Exécuter le rapport** pour l’objet Configuration Manager.  

  - Ajoute les utilisateurs et attribue le rôle **Administrateurs de rapport ConfigMgr** au dossier de rapports associé pour les utilisateurs administratifs qui disposent d’autorisations **Modifier le rapport** pour l’objet Configuration Manager.  

    Configuration Manager se connecte à Reporting Services et définit les autorisations pour les utilisateurs sur les dossiers racine de Configuration Manager et Reporting Services, et sur des dossiers de rapports spécifiques. Après l’installation initiale du point de Reporting Services, Configuration Manager se connecte à Reporting Services dans un intervalle de 10 minutes pour vérifier que les droits d’utilisateur configurés sur les dossiers de rapports sont les droits associés définis pour les utilisateurs de Configuration Manager. Quand des utilisateurs sont ajoutés ou que des droits d’utilisateur sont modifiés sur le dossier de rapports via le Gestionnaire de rapports de Reporting Services, Configuration Manager remplace ces modifications en utilisant les attributions basées sur les rôles qui sont stockées dans la base de données de site. De même, Configuration Manager supprime les utilisateurs qui n’ont pas de droits de génération de rapports dans Configuration Manager.  

##  <a name="BKMK_SecurityRoles"></a> Rôles de sécurité de Reporting Services pour Configuration Manager  
 Quand Configuration Manager installe le point de Reporting Services, les rôles de sécurité suivants sont ajoutés dans Reporting Services :  

-   **Utilisateurs de rapports ConfigMgr** : Les utilisateurs auxquels ce rôle de sécurité est attribué peuvent seulement exécuter des rapports Configuration Manager.  

-   **Administrateurs de rapport ConfigMgr** : Les utilisateurs auxquels ce rôle de sécurité est attribué peuvent exécuter toutes les tâches relatives aux rapports dans Configuration Manager.  

##  <a name="BKMK_VerifyReportingServicesPointInstallation"></a> Vérifier l’installation du point de Reporting Services  
 Après avoir ajouté le rôle de site de point de Reporting Services, vous pouvez vérifier l'installation en consultant les messages d'état spécifiques et les entrées de fichiers journaux. Utilisez la procédure suivante pour vérifier que l'installation du point de Reporting Services a réussi.  

> [!WARNING]  
>  Vous pouvez ignorer cette procédure si des rapports sont affichés dans le sous-dossier **Rapports** du nœud **Rapport** dans l’espace de travail **Surveillance** de la console Configuration Manager.  

#### <a name="to-verify-the-reporting-services-point-installation"></a>Pour vérifier l'installation du point de Reporting Services  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État du système**, puis cliquez sur **État du composant**.  

3.  Cliquez sur **SMS_SRS_REPORTING_POINT** dans la liste des composants.  

4.  Dans l'onglet **Accueil** , dans le groupe **Composant** , cliquez sur **Afficher les messages**, puis cliquez sur **Tous**.  

5.  Spécifiez une date et une heure pour une période avant d'installer le point de Reporting Services, puis cliquez sur **OK**.  

6.  Vérifiez que le message d'état avec l'ID 1015 est répertorié, ce qui indique que le point de Reporting Services a été installé avec succès. Vous pouvez aussi ouvrir le fichier Srsrp.log situé dans le dossier &lt;*Chemin_Installation_ConfigMgr*>\Logs et attendre le message **L’installation a réussi**.  

     Dans l’Explorateur Windows, accédez à &lt;*Chemin_Installation_ConfigMgr*>\Logs.  

7.  Ouvrez Srsrp.log et parcourez le fichier journal à partir de l'heure à laquelle le point de Reporting Services a été installé avec succès. Vérifiez que les dossiers de rapport ont été créés, que les rapports ont été déployés et que la stratégie de sécurité de chaque dossier a été confirmée. Recherchez la mention **La vérification que le service Web SRS est intègre sur le serveur a réussi** après la dernière ligne des confirmations des stratégies de sécurité.  

##  <a name="BKMK_Certificate"></a> Configurer un certificat auto-signé pour les ordinateurs de la console Configuration Manager  
 Il existe de nombreuses options vous permettant de créer des rapports pour SQL Server Reporting Services. Quand vous créez ou modifiez des rapports dans la console Configuration Manager, Configuration Manager ouvre le générateur de rapports pour l’utiliser comme environnement de création. Quelle que soit la façon dont vous créez vos rapports Configuration Manager, un certificat auto-signé est nécessaire à l’authentification sur le serveur de base de données de site. Configuration Manager installe automatiquement le certificat sur le serveur de site et sur les ordinateurs sur lesquels le fournisseur SMS est installé. Par conséquent, vous pouvez créer ou modifier des rapports à partir de la console Configuration Manager quand elle est exécutée sur l’un de ces ordinateurs. En revanche, quand vous créez ou modifiez des rapports à partir d’une console Configuration Manager qui installée sur un autre ordinateur, vous devez exporter le certificat à partir du serveur de site, puis l’ajouter au magasin de certificats **Personnes autorisées** sur l’ordinateur qui exécute la console Configuration Manager.  

> [!NOTE]  
>  Pour plus d'informations sur les autres environnements de création de rapports pour SQL Server Reporting Services, voir [Comparaison d'environnements de création de rapport](http://go.microsoft.com/fwlink/p/?LinkId=242805) dans la documentation en ligne de SQL Server 2008.  

 Prenez pour exemple les procédures suivantes pour transférer une copie du certificat auto-signé du serveur de site vers un autre ordinateur exécutant la console Configuration Manager quand les deux ordinateurs exécutent Windows Server 2008 R2. Si vous ne pouvez pas suivre cette procédure car vous avez une version différente du système d'exploitation, consultez la documentation de votre système d'exploitation pour voir la procédure équivalente.  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>Pour transférer une copie du certificat auto-signé du serveur de site vers un autre ordinateur  

1.  Effectuez les étapes suivantes sur le serveur de site pour exporter le certificat auto-signé :  

    1.  Cliquez sur **Démarrer**, sur **Exécuter**, puis tapez **mmc.exe**. Dans la console vide, cliquez sur **Fichier**, puis sur **Ajouter/Supprimer un composant logiciel enfichable**.  

    2.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

    3.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

    4.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

    5.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

    6.  Dans la console, développez **Certificats (ordinateur local)**, développez **Personnes autorisées**et sélectionnez **Certificats**.  

    7.  Cliquez avec le bouton droit sur le certificat portant le nom convivial &lt;*nom de domaine complet du serveur de site*>, cliquez sur **Toutes les tâches**, puis sélectionnez **Exporter**.  

    8.  Effectuez toutes les étapes de l' **Assistant Exportation de certificat** à l'aide des options par défaut et enregistrez le certificat avec l'extension de nom de fichier **.cer** .  

2.  Effectuez les étapes suivantes sur l’ordinateur qui exécute la console Configuration Manager pour ajouter le certificat auto-signé au magasin de certificats Personnes autorisées :  

    1.  Répétez les étapes précédentes de 1.a à 1.e pour configurer le composant logiciel enfichable MMC **Certificat** sur l’ordinateur du point de gestion.  

    2.  Dans la console, développez **Certificats (ordinateur local)** et **Personnes autorisées**, cliquez avec le bouton droit sur **Certificats**, sélectionnez **Toutes les tâches**, puis sélectionnez **Importer** pour lancer l' **Assistant Importation de certificat**.  

    3.  Sur la page **Fichier à importer** , cliquez sur le certificat sauvegardé à l'étape 1.h, puis cliquez sur **Suivant**.  

    4.  Sur la page **Magasin de certificats** , sélectionnez **Placer tous les certificats dans le magasin suivant**, lorsque le **Magasin de certificats** est paramétré sur **Personnes autorisées**, puis cliquez sur **Suivant**.  

    5.  Cliquez sur **Terminer** pour fermer l'Assistant et terminer la configuration des certificats sur l'ordinateur.  

##  <a name="BKMK_ModifyReportingServicesPoint"></a> Modifier les paramètres du point de Reporting Services  
 Une fois le point de Reporting Services installé, vous pouvez modifier les paramètres de connexion de base de données de site et d'authentification dans les propriétés du point de Reporting Services. Utilisez la procédure suivante pour modifier les paramètres du point de Reporting Services.  

#### <a name="to-modify-reporting-services-point-settings"></a>Pour modifier les paramètres du point de Reporting Services  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site** pour afficher la liste des systèmes de site.  

    > [!TIP]  
    >  Pour répertorier uniquement les systèmes de site hébergeant le rôle de site du point de Reporting Services, cliquez avec le bouton droit sur **Serveurs et rôles de système de site** pour sélectionner **Point de Reporting Services**.  

3.  Sélectionnez le système de site qui héberge le point de Reporting Services sur lequel vous souhaitez modifier les paramètres et sélectionnez **Point de Reporting Services** dans **Rôles de système de site**.  

4.  Dans l'onglet **Rôle du site** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Propriétés du point de Reporting Services** , vous pouvez modifier les paramètres suivants :  

    -   **Nom du serveur de base de données du site** : Spécifiez le nom du serveur qui héberge la base de données du site Configuration Manager. En règle générale, l'Assistant récupère automatiquement le nom de domaine complet (FQDN) du serveur. Pour spécifier une instance de base de données, utilisez le format &lt;*nom_serveur*>\&lt;*nom_instance*>.  

    -   **Nom de la base de données** : Spécifiez le nom de la base de données du site System Center 2012 Configuration Manager, puis cliquez sur **Vérifier** pour confirmer que l’assistant a accès à la base de données du site.  

        > [!IMPORTANT]  
        >  Le compte d'utilisateur qui crée le point de Reporting Services doit avoir accès en lecture à la base de données de site. Si le test de connexion échoue, une icône d'avertissement rouge s'affiche. Déplacez le curseur sur cette icône afin de lire les informations relatives à la défaillance. Corrigez la défaillance, puis cliquez à nouveau sur **Tester** .  

    -   **Compte d’utilisateur** : Cliquez sur **Définir**, puis sélectionnez le compte à utiliser quand SQL Server Reporting Services sur le point de Reporting Services se connecte à la base de données du site Configuration Manager pour récupérer les données affichées dans un rapport. Sélectionnez **Compte existant** pour spécifier un compte d’utilisateur Windows possédant des droits Configuration Manager existants ou sélectionnez **Nouveau compte** pour spécifier un compte d’utilisateur Windows ne possédant pas de droits dans Configuration Manager. Configuration Manager accorde automatiquement au compte d’utilisateur spécifié l’accès à la base de données du site. Le compte est affiché en tant que compte **Point de rapport SRS ConfigMgr** dans le sous-dossier **Comptes** du nœud **Sécurité** dans l'espace de travail **Administration** .  

         Le compte d'utilisateur Windows et le mot de passe spécifiés sont chiffrés et stockés dans la base de données Reporting Services. Reporting Services récupère les données de rapports à partir de la base de données de site à l'aide de ce compte et de ce mot de passe.  

        > [!IMPORTANT]  
        >  Lorsque la base de données de site se trouve sur un système de site distant, le compte que vous spécifiez doit disposer des autorisations **Ouvrir une session localement** sur l'ordinateur.  

6.  Cliquez sur **OK** pour enregistrer les modifications et quitter la boîte de dialogue.  

## <a name="upgrading-sql-server"></a>Mise à niveau de SQL Server  
 Après la mise à niveau de SQL Server et de l’instance SQL Server Reporting Services utilisée comme source de données pour un point de Reporting Services, des erreurs peuvent se produire au moment où vous exécutez ou modifiez des rapports à partir de la console Configuration Manager. Pour que la génération de rapports fonctionne correctement à partir de la console Configuration Manager, vous devez supprimer le rôle de système de site du point de Reporting Services du site, puis le réinstaller. Toutefois, après la mise à niveau, vous pouvez continuer à exécuter et à modifier des rapports à partir d'un navigateur Internet.  

##  <a name="BKMK_ConfigureReportOptions"></a> Configurer les options de rapport  
 Utilisez les options de rapport d’un site Configuration Manager pour sélectionner le point de Reporting Services par défaut à utiliser pour gérer vos rapports. Même si vous pouvez posséder plusieurs points de Reporting Services sur un site, seul le serveur de rapports par défaut sélectionné dans les options de rapport est utilisé pour gérer les rapports. Pour configurer les options de rapport de votre un site, procédez comme suit.  

#### <a name="to-configure-report-options"></a>Pour configurer des options de rapport  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**, puis cliquez sur **Rapports**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Options du rapport**.  

4.  Sélectionnez le serveur de rapports par défaut dans la liste, puis cliquez sur **OK**. Si aucun point de Reporting Services n'est répertorié dans la liste, vérifiez que vous disposez d'un point de Reporting Services correctement installé et configuré sur le site.  

## <a name="next-steps"></a>Étapes suivantes
[Opérations et maintenance pour les rapports](operations-and-maintenance-for-reporting.md)
