---
title: Récupération de site
titleSuffix: Configuration Manager
description: Découvrez comment récupérer vos sites dans System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bcc4181289e327537750d9790497c5451661de2e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351708"
---
#  <a name="recover-a-configuration-manager-site"></a>Récupération d'un site Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Lancez la récupération d'un site Configuration Manager à chaque défaillance d'un site Configuration Manager ou perte de données dans la base de données d'un site. La réparation et la resynchronisation des données constituent les principales tâches de récupération d'un site et elles sont nécessaires pour éviter l'interruption des opérations.

Les sections de cette rubrique peuvent vous aider à récupérer un site Configuration Manager. Pour créer une sauvegarde, consultez [Sauvegarde pour Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="considerations-before-recovering-a-site"></a>Considérations à prendre en compte avant la récupération d’un site
> [!Important]  
> Ces informations s’appliquent uniquement aux scénarios de récupération de site.  Lorsque vous mettez à niveau votre infrastructure locale sans récupérer activement un site défaillant, consultez les informations contenues dans les rubriques suivantes :
> - [Mettre à niveau l’infrastructure locale](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modifier votre infrastructure](/sccm/core/servers/manage/modify-your-infrastructure)


**Vous devez utiliser la même version et la même édition de SQL Server :** par exemple, la restauration sur SQL Server 2016 d’une base de données qui fonctionnait sur SQL Server 2014 n’est pas prise en charge. De la même manière, il n’est pas possible de restaurer une base de données de site qui s’exécutait sur une édition Standard de SQL Server 2016 vers une édition Enterprise de SQL Server 2016.
-   SQL Server ne doit pas être configuré en **mode mono-utilisateur**.
-   Vérifiez que les fichiers .MDF et .LDF sont valides. Quand vous récupérez un site, l’état des fichiers que vous restaurez n’est pas vérifié.

**Si vous utilisez un groupe de disponibilité SQL Server Always On pour héberger la base de données du site :** modifiez vos plans de récupération comme décrit dans la rubrique [Se préparer à utiliser SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**Si vous utilisez des réplicas de base de données :** après avoir restauré une base de données de site configurée pour des réplicas de base de données et avant de pouvoir utiliser les réplicas de base de données, vous devez reconfigurer chaque réplica de base de données en recréant les publications et les abonnements.

## <a name="determine-your-recovery-options"></a>Détermination de vos options de récupération
Il existe deux zones principales à prendre en compte pour la récupération d'un site principal Configuration Manager et d'un site d'administration centrale : le **serveur de site** et la **base de données de site**.
Les sections suivantes peuvent vous aider à sélectionner les meilleures options pour votre scénario de récupération.

> [!NOTE]   
> Lorsque le programme d'installation détecte un site Configuration Manager existant sur le serveur, vous pouvez démarrer une récupération de site, mais les options de récupération pour le serveur de site sont limitées. Par exemple, si vous exécutez le programme d'installation sur un serveur de site existant, lorsque vous choisissez la récupération, vous pouvez récupérer le serveur de base de données de site mais l'option de récupération du serveur de site est désactivée.

### <a name="site-server-recovery-options"></a>Options de récupération de serveur de site
Démarrez le programme d’installation à partir d’une copie du dossier **CD.Latest** que vous avez créée en dehors du dossier d’installation de Configuration Manager.
-   Si vous exécutez le programme d'installation de Configuration Manager à partir du menu **Démarrer** sur le serveur de site, l'option **Récupérer un site** n'est pas disponible.
-   Si vous avez installé des mises à jour à partir de la console Configuration Manager avant d’effectuer votre sauvegarde, vous ne pouvez pas réinstaller correctement le site en utilisant le programme d’installation à partir du support d’installation ou du chemin d’installation de Configuration Manager.

Sélectionnez ensuite l’option **Récupérer un site** . Vous disposez des options de récupération suivantes pour le serveur de site défaillant :

-   **Récupérer le serveur de site à l’aide d’une sauvegarde existante** : utilisez cette option si vous disposez d’une sauvegarde du serveur de site Configuration Manager qui a été créée sur le serveur de site dans le cadre de la tâche de maintenance de **sauvegarde du serveur de site** avant la défaillance du site. Le site est réinstallé et les paramètres du site sont configurés en fonction du site qui a été sauvegardé.
-   **Réinstaller le serveur de site**: utilisez cette option si vous ne possédez pas de sauvegarde du serveur du site. Le serveur de site est réinstallé et vous devez spécifier les paramètres du site, comme vous le feriez lors d'une installation initiale.
  -   Vous devez utiliser les mêmes code de site et nom de base de données de site que ceux que vous avez utilisés lors de l'installation initiale du site défaillant.
  -   Vous pouvez réinstaller le site sur un nouvel ordinateur qui exécute un nouveau système d’exploitation.
  -   L’ordinateur doit utiliser le même nom et le même nom de domaine complet que le serveur de site d’origine.   

### <a name="site-database-recovery-options"></a>Options de récupération de base de données de site
Lorsque vous exécutez le programme d'installation, vous disposez des options de récupération suivantes pour la base de données de site :
-   **Récupérer la base de données de site à l’aide d’un jeu de sauvegarde** : utilisez cette option si vous disposez d’une sauvegarde de la base de données de site Configuration Manager qui a été créée dans le cadre de la tâche de maintenance de **sauvegarde du serveur de site** exécutée sur le site avant la défaillance de la base de données de site. Lorsque vous possédez une hiérarchie, les modifications qui ont été effectuées au niveau de la base de données de site après la dernière sauvegarde de la base de données de site sont récupérées à partir du site d'administration centrale pour un site principal ou à partir d'un site principal de référence pour un site d'administration centrale. Lorsque vous récupérez la base de données de site pour un site principal autonome, vous perdez les modifications effectuées au niveau du site après la dernière sauvegarde.

   Lorsque vous récupérez la base de données de site pour un site d'une hiérarchie, le comportement de récupération est différent pour un site d'administration centrale et un site principal et lorsque la dernière sauvegarde se situe pendant ou en dehors de la période de rétention du suivi des modifications SQL Server. Pour plus d’informations, voir la section [Scénarios de récupération de base de données de site](##site-database-recovery-scenarios) de cette rubrique.
  > [!NOTE]   
  > La récupération échoue si vous choisissez de restaurer la base de données de site à l'aide d'un jeu de sauvegarde, alors que la base de données de site existe déjà.  

-   **Créer une nouvelle base de données pour ce site** : utilisez cette option si vous ne possédez pas de sauvegarde de la base de données de site Configuration Manager. Lorsque vous possédez une hiérarchie, une nouvelle base de données de site est créée et les données sont récupérées à l'aide des données répliquées depuis le site d'administration centrale pour un site principal ou depuis un site principal de référence pour un site d'administration centrale. Cette option n'est pas disponible lorsque vous récupérez un site principal autonome ou un site d'administration centrale qui ne possède pas de sites principaux.

-   **Utiliser une base de données de site qui a été récupérée manuellement** : utilisez cette option quand vous avez déjà récupéré la base de données de site Configuration Manager mais que vous devez effectuer le processus de récupération.
    -   Configuration Manager peut récupérer la base de données de site à partir de la tâche de maintenance de sauvegarde Configuration Manager ou à partir d'une sauvegarde de base de données de site que vous effectuez à l’aide de DPM ou d’autre processus. Après avoir restauré la base de données de site à l'aide d'une méthode en dehors de Configuration Manager, vous devez exécuter le programme d'installation et sélectionner cette option pour effectuer la récupération de la base de données de site.

    > [!NOTE]   
    > Lorsque vous utilisez DPM pour sauvegarder votre base de données de site, appliquez les procédures DPM pour restaurer la base de données de site sur un emplacement défini avant de continuer le processus de restauration dans Configuration Manager. Pour plus d'informations sur DPM, voir [Bibliothèque de documentation de Data Protection Manager]() sur TechNet.    

    -   Lorsque vous possédez une hiérarchie, les modifications qui ont été effectuées au niveau de la base de données de site après la dernière sauvegarde de la base de données de site sont récupérées à partir du site d'administration centrale pour un site principal ou à partir d'un site principal de référence pour un site d'administration centrale. Lorsque vous récupérez la base de données de site pour un site principal autonome, vous perdez les modifications effectuées au niveau du site après la dernière sauvegarde.     


-   **Ignorer la récupération de base de données** : utilisez cette option quand aucune perte de données ne s’est produite sur le serveur de base de données de site Configuration Manager. Cette option est valide uniquement lorsque la base de données de site se trouve sur un ordinateur différent du serveur de site que vous récupérez.

### <a name="sql-server-change-tracking-retention-period"></a>Période de rétention du suivi des modifications SQL Server
Le suivi des modifications est activé pour la base de données de site dans SQL Server. Le suivi des modifications permet à Configuration Manager de demander des informations sur les modifications qui ont été apportées aux tables de base de données après un moment précis. La période de rétention spécifie la durée de conservation des informations de suivi des modifications. Par défaut, la période de rétention de la base de données de site est définie sur 5 jours. Lorsque vous récupérez une base de données de site, le processus de récupération se déroule différemment si votre sauvegarde a lieu pendant ou en dehors de la période de rétention. Par exemple, en cas d'échec de votre serveur de base de données de site, si votre dernière sauvegarde remonte à 7 jours, elle se situe en dehors de la période de rétention.

Pour plus d’informations sur les éléments internes du suivi des modifications SQL Server, consultez les blogs de l’équipe SQL Server suivants : [Nettoyage du suivi des modifications - partie 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) et [Nettoyage du suivi des modifications - partie 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).

### <a name="reinitialization-of-site-or-global-data"></a>Réinitialisation de données d’un site ou de données globales
Le processus de réinitialisation de site ou de données globales remplace les données existantes dans la base de données de site par les données d'une autre base de données de site. Par exemple, lorsque le site ABC réinitialise les données du site XYZ, les étapes suivantes se produisent :
-   Les données sont copiées du site XYZ au site ABC.
-   Les données existantes pour le site XYZ sont supprimées de la base de données de site sur le site ABC.
-   Les données copiées à partir du site XYZ sont insérées dans la base de données de site du site ABC.

#### <a name="example-scenario-1"></a>Exemple de scénario 1
**Le site principal réinitialise les données globales à partir du site d’administration centrale**: le processus de récupération supprime les données globales existantes pour le site principal dans la base de données du site principal et remplace les données par les données globales copiées à partir du site d’administration centrale.

#### <a name="example-scenario-2"></a>Exemple de scénario 2
**Le site d’administration centrale réinitialise les données du site à partir d’un site principal**: le processus de récupération supprime les données de site existantes pour ce site principal dans la base de données du site d’administration centrale et remplace les données par les données de site copiées à partir du site principal. Les données de site d'autres sites principaux ne sont pas affectées.

### <a name="site-database-recovery-scenarios"></a>Scénarios de récupération de base de données de site
Suite à la restauration d'une base de données de site à partir d'une sauvegarde, Configuration Manager tente de restaurer les modifications effectuées au niveau du site et des données globales après la dernière sauvegarde de la base de données. Voici une description des actions que Configuration Manager démarre après la restauration d’une base de données de site à partir d’une sauvegarde.

**Le site récupéré est un site d’administration centrale :**
-   **Sauvegarde de base de données pendant la période de rétention du suivi des modifications**
    -   **Données globales :** les modifications des données globales après la sauvegarde sont répliquées à partir de tous les sites principaux.
    -   **Données de site :** les modifications des données du site après la sauvegarde sont répliquées à partir de tous les sites principaux.


-   **Sauvegarde de base de données antérieure à la période de rétention du suivi des modifications**
    -   **Données globales :** le site d’administration centrale réinitialise les données globales à partir du site principal de référence, si vous le spécifiez. Ensuite, tous les autres sites principaux réinitialisent les données globales à partir du site d'administration centrale. Si aucun site de référence n'est spécifié, tous les sites principaux réinitialisent les données globales à partir du site d'administration centrale (les données qui ont été restaurées à partir de la sauvegarde).
    -   **Données de site :** le site d’administration centrale réinitialise les données de site à partir de chaque site principal.


**Le site récupéré est un site principal :**
-   **Sauvegarde de base de données pendant la période de rétention du suivi des modifications**
    -   **Données globales :** les modifications apportées aux données globales après la sauvegarde sont répliquées à partir du site d’administration centrale.
    -   **Données de site :** le site d’administration centrale réinitialise les données de site à partir du site principal. Les modifications après la sauvegarde sont perdues, mais la plupart des données sont régénérées par les clients qui envoient des informations au site principal.


-   **Sauvegarde de base de données antérieure à la période de rétention du suivi des modifications**
    -   **Données globales :** le site principal réinitialise les données globales à partir du site d’administration centrale.
    -   **Données de site :** le site d’administration centrale réinitialise les données de site à partir du site principal. Les modifications après la sauvegarde sont perdues, mais la plupart des données sont régénérées par les clients qui envoient des informations au site principal.

## <a name="site-recovery-procedures"></a>Procédures de récupération de site
Appliquez l'une des procédures suivantes pour récupérer votre serveur de site ainsi que la base de données du site.

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Pour démarrer une récupération de site avec l'Assistant Installation
1.  Copiez le [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) à un emplacement en dehors du dossier d’installation de Configuration Manager.
À partir de la copie du dossier CD.Latest, exécutez l’Assistant Installation de Configuration Manager.

2.  Sur la page **Mise en route** , sélectionnez **Récupérer un site**, puis cliquez sur **Suivant**.

3.  Terminez l'Assistant en utilisant les options qui conviennent à la récupération de votre site.

  -   Pendant la récupération, le programme d'installation identifie le port de SQL Server Service Broker (SSB) utilisé par SQL Server. Ne modifiez pas ce paramètre de port lors de la récupération, sinon, la réplication de données ne fonctionnera pas correctement une fois la récupération terminée.

  -   Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager dans l’Assistant Installation.

### <a name="to-start-an-unattended-site-recovery"></a>Pour démarrer une récupération de site en mode sans assistance
  1.    Préparez le script d'installation sans assistance pour les options dont vous avez besoin pour la récupération du site.  Consultez [Clés du fichier de script de récupération de site sans assistance](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.    Exécutez le programme d’installation de Configuration Manager en utilisant l’option de commande **/script**. Par exemple, si vous avez nommé le fichier d’initialisation de l’installation ConfigMgrUnattend.ini et que vous l’avez enregistré dans le répertoire C:\Temp de l’ordinateur sur lequel vous exécutez le programme d’installation, la commande est la suivante : **Setup /script C:\temp\ConfigMgrUnattend.ini**

  > [!NOTE]   
  >  Après la récupération d’un site d’administration centrale, l’établissement de la réplication de certaines données de site à partir des sites enfants peut échouer. Cela peut inclure l’inventaire matériel, l’inventaire logiciel et les messages d’état.
  >
  >  Si cela se produit, vous devez réinitialiser **ConfigMgrDRSSiteQueue** pour la réplication de base de données.  Pour ce faire, utilisez **SQL Server Manager** pour exécuter la requête suivante sur la base de données de site Configuration Manager sur le site d’administration centrale :
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = ’ConfigMgrDRSSiteQueue’ AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>Tâches postérieures à la récupération
Après avoir récupéré votre site, il existe plusieurs tâches à effectuer après la récupération, pour que celle-ci soit complète. Utilisez les sections suivantes pour vous aider à terminer le processus de récupération de site.

### <a name="re-enter-user-account-passwords"></a>Entrer de nouveau des mots de passe du compte d'utilisateur
Après une récupération de serveur de site, les mots de passe des comptes d'utilisateur spécifiés pour le site doivent être entrés de nouveau car ils sont réinitialisés par la restauration du site. Les comptes sont répertoriés sur la page **Terminé** de l'Assistant Installation après la récupération du site, et enregistrés dans C:\ConfigMgrPostRecoveryActions.html sur le serveur de site récupéré.

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Pour entrer de nouveau les mots de passe du compte d'utilisateur après la récupération du site

1.  Ouvrez la console Configuration Manager et connectez-vous au site récupéré.

2.  Dans la console Configuration Manager, cliquez sur **Administration**.

3.  Dans l'espace de travail **Administration** , développez **Sécurité**, puis cliquez sur **Comptes**.

4.  Pour chaque compte pour lequel vous entrez de nouveau le mot de passe, effectuez les opérations suivantes :

    1.  Sélectionnez le compte dans la liste des comptes identifiés après la récupération du site. Vous trouverez cette liste dans C:\ConfigMgrPostRecoveryActions.html sur le serveur de site récupéré.

    2.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir les propriétés du compte.

    3.  Dans l'onglet **Général** , cliquez sur **Définir**et entrez de nouveau les mots de passe du compte.

    4.  Cliquez sur **Vérifier**, sélectionnez la source de données appropriée pour le compte d'utilisateur sélectionné, puis cliquez sur **Tester la connexion** pour vérifier que le compte d'utilisateur peut se connecter à la source de données.

    5.  Cliquez sur **OK** pour enregistrer les modifications du mot de passe, puis cliquez sur **OK**.

### <a name="re-enter-sideloading-keys"></a>Entrer de nouveau les clés de chargement de version test
Après une récupération de serveur de site, vous devez saisir à nouveau les clés de chargement de version test Windows spécifiées pour le site, car elles sont réinitialisées lors de la récupération de site. Une fois que vous avez de nouveau entré les clés de chargement de version test, la valeur de la colonne **Activations utilisées** pour les clés de chargement de version test Windows est réinitialisée dans la console Configuration Manager. Par exemple, avant la défaillance du site, la valeur du champ **Total activations** est définie sur **100** et **Activations utilisées** sur **90** pour le nombre de clés qui ont été utilisées par les appareils. Après la récupération du site, la colonne **Total activations** affiche toujours **100**, mais la colonne **Activations utilisées** affiche la valeur erronée de **0**. Cependant, une fois que 10 nouveaux appareils auront utilisé une clé de chargement de version test, il ne restera aucune clé de chargement de version test et l'appareil suivant ne parviendra pas à appliquer une clé de chargement de version test.

### <a name="recreate-the-microsoft-intune-subscription"></a>Recréer l’abonnement Microsoft Intune
 Si vous récupérez un serveur de site Configuration Manager après que l’ordinateur serveur de site a été ré-imagé, l’abonnement Microsoft Intune n’est pas restauré. Vous devez reconnecter l’abonnement après avoir récupéré le site.  Ne créez pas de demande APN. À la place, chargez le fichier .pem valide actuel qui a été chargé la dernière fois que la gestion iOS a été configurée ou renouvelée. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurer SSL pour les rôles de système de site qui utilisent IIS
Lorsque vous récupérez des systèmes de site qui exécutent IIS et qui ont été configurés pour le protocole HTTPS avant la panne, vous devez reconfigurer IIS pour utiliser le certificat de serveur Web.

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Réinstaller les correctifs sur le serveur de site récupéré
Après la récupération d'un site, vous devez réinstaller tous les correctifs qui étaient appliqués au serveur de site. Consultez la liste des correctifs précédemment installés sur la page **Terminé** de l’Assistant Installation après la récupération d’un site. Cette liste est également enregistrée sous **C:\ConfigMgrPostRecoveryActions.html** sur le serveur de site récupéré.

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Récupérer des rapports personnalisés sur l'ordinateur qui exécute Reporting Services
Si vous avez créé des rapports de Reporting Services personnalisés, en cas de défaillance de Reporting Services, vous pouvez récupérer les rapports lorsque le serveur de rapports a été sauvegardé. Pour plus d'informations sur la restauration de vos rapports personnalisés dans Reporting Services, voir [Opérations de sauvegarde et de restauration pour une installation Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) dans la documentation en ligne de SQL Server 2008.

### <a name="recover-content-files"></a>Récupérer des fichiers de contenu
 La base de données du site contient des informations sur l'emplacement des fichiers de contenu sur le serveur de site, mais les fichiers de contenu ne sont pas sauvegardés ou restaurés lors du processus de sauvegarde et de récupération. Pour récupérer complètement les fichiers de contenu, vous devez restaurer la bibliothèque de contenu et les fichiers sources du package vers leur emplacement d'origine. Il existe plusieurs méthodes pour récupérer vos fichiers de contenu, mais la méthode la plus simple consiste à récupérer les fichiers à partir d'une sauvegarde du système de fichiers du serveur de site.

 Si vous ne disposez pas de sauvegarde du système de fichiers pour les fichiers sources du package, vous devez les copier ou les télécharger manuellement, comme vous l'avez fait lors de la création initiale du package. Vous pouvez exécuter la requête suivante dans SQL Server pour trouver l'emplacement source du package pour tous les packages et applications : `SELECT * FROM v_Package`. Vous pouvez identifier le site source du package en examinant les trois premiers caractères de l'ID de package. Par exemple, si l'ID de package est CEN00001, le code de site pour le site source est CEN. Lorsque vous restaurez les fichiers sources du package, ceux-ci doivent être restaurés vers le même emplacement que celui dans lequel ils se trouvaient avant la défaillance.

 Si vous ne disposez pas d'une sauvegarde des systèmes de fichiers qui contient la bibliothèque de contenu, vous pouvez utiliser les options de restauration suivantes :

-   **Importer un fichier de contenu préparé** : quand vous disposez d’une hiérarchie Configuration Manager, vous pouvez créer un fichier de contenu préparé avec tous les packages et applications d’un autre emplacement, puis importer le fichier de contenu préparé pour récupérer la bibliothèque de contenu sur le serveur de site.

-   **Mettre à jour le contenu**: quand vous démarrez l’action de mise à jour de contenu pour un type de déploiement d’application ou de package, le contenu est copié de la source du package vers la bibliothèque de contenu. Les fichiers sources du package doivent être disponibles sur l'emplacement d'origine pour que cette action soit effectuée avec succès. Vous devez effectuer cette action pour chaque package et chaque application.

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Récupérer les mises à jour logicielles personnalisées sur l'ordinateur qui exécute l'éditeur de mise à jour
Lorsque vous avez inclus les fichiers de base de données de l’éditeur de mise à jour dans votre plan de sauvegarde, vous pouvez récupérer les bases de données en cas de panne de l'ordinateur sur lequel l’éditeur de mise à jour s'exécute. Pour plus d'informations sur l'éditeur de mise à jour, voir [Éditeur de mise à jour System Center 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) dans la bibliothèque TechCenter de System Center.

Utilisez la procédure suivante pour restaurer la base de données de l'éditeur de mise à jour.

#### <a name="to-restore-the-updates-publisher-2011-database"></a>Pour restaurer la base de données de l'éditeur de mise à jour 2011
1.  Réinstallez l’éditeur de mise à jour sur l’ordinateur récupéré.

2.  Copiez le fichier de base de données (Scupdb.sdf) depuis la destination de sauvegarde vers %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ sur l'ordinateur qui exécute l’éditeur de mise à jour.

3.  Lorsque plusieurs utilisateurs exécutent l’éditeur de mise à jour sur l'ordinateur, vous devez copier chaque fichier de base de données vers l'emplacement du profil de l'utilisateur approprié.

### <a name="user-state-migration-data"></a>Données de migration de l'état utilisateur
Dans le cadre des propriétés du système de site du point de migration d'état, vous pouvez spécifier les dossiers qui conservent les données de migration de l'état utilisateur. Après avoir récupéré un serveur disposant d'un dossier qui conserve les données de migration d'état utilisateur, vous devez restaurer manuellement les données de migration d'état utilisateur vers les emplacements qu'elles occupaient avant la panne.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Régénérer les certificats pour les points de distribution
Après la restauration d’un site, le fichier journal distmgr.log peut contenir l’entrée suivante pour un ou plusieurs points de distribution : **Échec de déchiffrage des données PFX du certificat**. Cette entrée indique le site ne peut pas déchiffrer les données de certificat du point de distribution. Pour résoudre ce problème, vous devez régénérer ou réimporter le certificat pour les points de distribution concernés. Ceci peut se faire en utilisant l’applet de commande PowerShell [Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx).

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Mettre à jour les certificats utilisés pour les points de distribution cloud
 Configuration Manager requiert un certificat de gestion pour la communication entre le serveur de site et le point de distribution cloud. Suite à la récupération d'un site, vous devez mettre à jour les certificats des points de distribution cloud.

## <a name="recover-a-secondary-site"></a>Récupération d'un site secondaire
 Configuration Manager ne prend pas en charge la sauvegarde de la base de données sur un site secondaire, mais prend en charge la récupération en réinstallant le site secondaire. La récupération de site secondaire est requise dans le cas de défaillance d'un site secondaire Configuration Manager.

### <a name="requirements-for-reinstalling-a-secondary-site"></a>Configuration requise pour réinstaller un site secondaire
-   L'ordinateur doit respecter toutes les conditions préalables de site secondaire et disposer des droits de sécurité appropriés configurés.
-   Vous devez utiliser le même chemin d'installation qui a été utilisé pour le site en échec.
-   Vous devez utiliser un ordinateur avec la même configuration que l'ordinateur en échec, par exemple, son nom de domaine complet, pour récupérer correctement le site secondaire.
-   L’ordinateur doit avoir la même configuration SQL Server que le site défaillant.
  -   Lors d'une restauration de site secondaire, Configuration Manager n'installe pas SQL Server Express s'il n'est pas déjà installé sur l'ordinateur.
  -   Vous devez utiliser la même version de SQL Server et la même instance de SQL Server que vous avez utilisées pour la base de données de site secondaire avant la défaillance.

### <a name="to-recover-a-secondary-site"></a>Pour récupérer un site secondaire :
Pour récupérer un site secondaire, utilisez l'action **Récupérer le site secondaire** à partir du nœud **Site** dans la console Configuration Manager. Contrairement à la récupération d'un site d'administration centrale ou d'un site principal, la récupération d'un site secondaire n'utilise pas de fichier de sauvegarde, mais réinstalle plutôt les fichiers du site secondaire sur l'ordinateur du site secondaire ayant échoué. Une fois le site réinstallé, les données du site secondaire sont réinitialisées avec les données du site principal parent.

Pendant le processus de récupération, Configuration Manager vérifie si la bibliothèque de contenu existe bien sur l'ordinateur du site secondaire et si le contenu approprié est disponible. Le site secondaire utilisera la bibliothèque de contenu existante, si elle contient le contenu approprié. Sinon, pour récupérer la bibliothèque de contenu d'un site secondaire récupéré, vous devez redistribuer ou prédéfinir le contenu sur ce site récupéré.

Lorsque vous disposez d'un point de distribution qui ne se trouve pas sur le site secondaire, vous n'avez pas à réinstaller le point de distribution lors d'une restauration du site secondaire. Après la restauration du site secondaire, le site se synchronise automatiquement avec le point de distribution.

Vous pouvez vérifier l'état de la récupération du site secondaire à l'aide de l'action **Afficher l'état d'installation** dans le nœud **Sites** de la console Configuration Manager.
