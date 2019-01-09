---
title: Récupération de site
titleSuffix: Configuration Manager
description: Découvrez comment récupérer vos sites dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b56dd830e2550a14d6b1e44d2aa7fdda7c56bc9b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420496"
---
#  <a name="recover-a-configuration-manager-site"></a>Récupération d'un site Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Lancez la récupération d’un site Configuration Manager à chaque défaillance d’un site ou perte de données dans la base de données d’un site. La réparation et la resynchronisation des données constituent les principales tâches de récupération d'un site et elles sont nécessaires pour éviter l'interruption des opérations.

Les sections de cet article peuvent vous aider à récupérer un site Configuration Manager. Pour créer une sauvegarde, consultez [Sauvegarde pour Configuration Manager](/sccm/core/servers/manage/backup-and-recovery).



## <a name="considerations-before-recovering-a-site"></a>Considérations à prendre en compte avant la récupération d’un site

> [!Important]  
> Ces informations s’appliquent uniquement aux scénarios de récupération de site. Quand vous mettez à niveau votre infrastructure locale sans récupérer activement un site défaillant, consultez les informations contenues dans les articles suivants :
> - [Mettre à niveau l’infrastructure locale](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modifier votre infrastructure](/sccm/core/servers/manage/modify-your-infrastructure)


#### <a name="use-the-same-version-and-edition-of-sql-server"></a>Utiliser la même version et la même édition de SQL Server   
Par exemple, la restauration d’une base de données exécutée sur SQL Server 2014 vers SQL Server 2016 n’est pas prise en charge. De même,la restauration d’une base de données de site SQL Server 2016 de l’édition Standard vers l’édition Enterprise n’est pas prise en charge.
- SQL Server ne peut pas être configuré en **mode mono-utilisateur**.
- Vérifiez que les fichiers MDF et LDF sont valides. Quand vous récupérez un site, l’état des fichiers n’est pas vérifié.  

#### <a name="sql-server-always-on-availability-groups"></a>Groupes de disponibilité SQL Server AlwaysOn   
Si vous utilisez des groupes de disponibilité SQL Server AlwaysOn pour héberger la base de données du site, modifiez vos plans de récupération comme décrit dans la rubrique [Se préparer à utiliser SQL Server AlwaysOn](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

#### <a name="database-replicas"></a>Réplicas de base de données  
Après avoir restauré une base de données de site que vous avez configurée pour les réplicas de base de données, reconfigurez chaque réplica. Avant de pouvoir utiliser les réplicas de base de données, recréez les publications et les abonnements.



## <a name="determine-your-recovery-options"></a>Détermination de vos options de récupération

Il existe deux zones principales à prendre en compte pour la récupération d’un serveur de site principal Configuration Manager et d’un site d’administration centrale : le **serveur de site** et la **base de données de site**.
Les sections suivantes peuvent vous aider à sélectionner les meilleures options pour votre scénario de récupération.

> [!NOTE]   
> Quand le programme d’installation de Configuration Manager détecte un site existant sur le serveur, vous pouvez démarrer une récupération de site, mais les options de récupération pour le serveur de site sont limitées. Par exemple, si vous exécutez le programme d'installation sur un serveur de site existant, lorsque vous choisissez la récupération, vous pouvez récupérer le serveur de base de données de site mais l'option de récupération du serveur de site est désactivée.


### <a name="site-server-recovery-options"></a>Options de récupération de serveur de site

Démarrez le programme d’installation de Configuration Manager à partir d’une copie du dossier **CD.Latest** que vous avez créée en dehors du dossier d’installation de Configuration Manager.  

-   Si vous exécutez le programme d’installation à partir du menu **Démarrer** sur le serveur de site, l’option **Récupérer un site** n’est pas disponible.  

-   Si vous avez installé des mises à jour à partir de la console Configuration Manager avant d’effectuer votre sauvegarde, vous ne pouvez pas réinstaller le site en utilisant le programme d’installation à partir des emplacements suivants : 
    - Support d’installation
    - Chemin d’installation de Configuration Manager 

Sélectionnez ensuite l’option **Récupérer un site** . Vous disposez des options de récupération suivantes pour le serveur de site défaillant :  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Récupérer le serveur de site à l’aide d’une sauvegarde existante
Utilisez cette option quand vous disposez d’une sauvegarde de Configuration Manager du serveur de site antérieure à la défaillance du site. Le site crée cette sauvegarde dans le cadre de la tâche de maintenance de **sauvegarde du serveur de site**. Le site est réinstallé et les paramètres du site sont configurés en fonction du site qui a été sauvegardé.  

#### <a name="reinstall-the-site-server"></a>Réinstaller le serveur de site.
Utilisez cette option si vous ne possédez pas de sauvegarde du serveur de site. Le serveur de site est réinstallé et vous devez spécifier les paramètres du site, comme vous le feriez lors d’une installation initiale.  

-   Utilisez les mêmes code de site et nom de base de données de site que ceux que vous avez utilisés lors de l’installation initiale du site défaillant.  

-   Vous pouvez réinstaller le site sur un nouvel ordinateur qui exécute une nouvelle version du système d’exploitation.  

-   Le serveur doit utiliser les mêmes nom d’hôte et nom de domaine complet que ceux du serveur de site d’origine.   


### <a name="site-database-recovery-options"></a>Options de récupération de base de données de site

Quand vous exécutez le programme d’installation de Configuration Manager, vous disposez des options de récupération suivantes pour la base de données de site :  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Récupérer la base de données de site à l’aide d’un jeu de sauvegarde
Utilisez cette option quand vous disposez d’une sauvegarde de Configuration Manager de la base de données de site antérieure à la défaillance de la base de données. Le site crée cette sauvegarde dans le cadre de la tâche de maintenance de **sauvegarde du serveur de site**. Dans une hiérarchie, lors de la restauration d’un site principal, le processus de récupération récupère à partir du site d’administration centrale toute modification apportée à la base de données de site après la dernière sauvegarde. Lors de la restauration du site d’administration centrale, le processus de récupération récupère ces modifications à partir d’un site principal de référence. Quand vous récupérez la base de données de site pour un site principal autonome, vous perdez les modifications effectuées au niveau du site après la dernière sauvegarde.  

Quand vous récupérez la base de données de site pour un site d’une hiérarchie, le comportement de récupération est différent pour un site d’administration centrale et un site principal. Le comportement est également différent lorsque la dernière sauvegarde se situe pendant ou en dehors de la période de rétention du suivi des modifications SQL Server. Pour plus d’informations, consultez la section [Scénarios de récupération de base de données de site](#site-database-recovery-scenarios) de cet article.  

> [!NOTE]   
> La récupération échoue si vous choisissez de restaurer la base de données de site à l’aide d’un jeu de sauvegarde, alors que la base de données de site existe déjà.   

#### <a name="create-a-new-database-for-this-site"></a>Créer une base de données pour ce site
Utilisez cette option si vous ne possédez pas de sauvegarde de la base de données de site. Dans une hiérarchie, le processus de récupération crée une base de données de site. Lors de la restauration d’un site principal enfant, il récupère les données en les répliquant à partir du site d’administration centrale. Lors de la restauration du site d’administration centrale, il réplique les données à partir d’un site principal de référence. Cette option n’est pas disponible quand vous récupérez un site principal autonome ou un site d’administration centrale qui ne possède pas de sites principaux.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Utiliser une base de données de site qui a été récupérée manuellement
Utilisez cette option quand vous avez déjà récupéré la base de données de site Configuration Manager, mais que vous devez effectuer le processus de récupération.  

- Configuration Manager peut récupérer la base de données de site à partir des processus suivants :  

  - Tâche de maintenance de sauvegarde Configuration Manager  
  - Sauvegarde de base de données de site avec DPM (Data Protection Manager)  
  - Autre processus de sauvegarde   

    Après avoir restauré la base de données de site à l’aide d’une méthode en dehors de Configuration Manager, exécutez le programme d’installation et sélectionnez cette option pour effectuer la récupération de la base de données de site.  

    > [!NOTE]   
    > Lorsque vous utilisez DPM pour sauvegarder votre base de données de site, appliquez les procédures DPM pour restaurer la base de données de site sur un emplacement défini avant de continuer le processus de restauration dans Configuration Manager. Pour plus d’informations sur DPM, consultez la bibliothèque de documentation de [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).    

- Dans une hiérarchie, lors de la récupération d’une base de données de site principale, le processus de récupération récupère à partir du site d’administration centrale toute modification apportée à la base de données de site après la dernière sauvegarde. Lors de la restauration du site d’administration centrale, le processus de récupération récupère ces modifications à partir d’un site principal de référence. Quand vous récupérez la base de données de site pour un site principal autonome, vous perdez les modifications effectuées au niveau du site après la dernière sauvegarde.   

#### <a name="skip-database-recovery"></a>Ignorer la récupération de base de données.
Utilisez cette option quand aucune perte de données ne s’est produite sur le serveur de base de données de site Configuration Manager. Cette option est valide uniquement lorsque la base de données de site se trouve sur un ordinateur différent du serveur de site que vous récupérez.  


### <a name="sql-server-change-tracking-retention-period"></a>Période de rétention du suivi des modifications SQL Server

Configuration Manager active le suivi des modifications pour la base de données de site dans SQL Server. Le suivi des modifications permet à Configuration Manager de demander des informations sur les modifications apportées aux tables de base de données après un moment précis. La période de rétention spécifie la durée de conservation des informations de suivi des modifications. Par défaut, la période de rétention de la base de données de site est définie sur cinq jours. Lorsque vous récupérez une base de données de site, le processus de récupération se déroule différemment si votre sauvegarde a lieu pendant ou en dehors de la période de rétention. Par exemple, en cas d’échec de votre serveur SQL Server, si votre dernière sauvegarde remonte à sept jours, elle se situe en dehors de la période de rétention.

Pour plus d’informations sur les éléments internes du suivi des modifications SQL Server, consultez les billets de blog de l’équipe SQL Server suivants : [Nettoyage du suivi des modifications - partie 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) et [Nettoyage du suivi des modifications - partie 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2).


### <a name="reinitialization-of-site-or-global-data"></a>Réinitialisation de données d’un site ou de données globales

Le processus de réinitialisation de site ou de données globales remplace les données existantes dans la base de données de site par les données d'une autre base de données de site. Par exemple, lorsque le site ABC réinitialise les données du site XYZ, les étapes suivantes se produisent :
- Les données sont copiées du site XYZ au site ABC.
- Les données existantes pour le site XYZ sont supprimées de la base de données de site sur le site ABC.
- Les données copiées à partir du site XYZ sont insérées dans la base de données de site du site ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-central-administration-site"></a>Exemple de scénario 1 : Le site principal réinitialise les données globales à partir du site d’administration centrale  
Le processus de récupération supprime les données globales existantes pour le site principal dans la base de données du site principal et remplace les données par les données globales copiées à partir du site d'administration centrale.

#### <a name="example-scenario-2-the-central-administration-site-reinitializes-the-site-data-from-a-primary-site"></a>Exemple de scénario 2 : Le site d’administration centrale réinitialise les données du site à partir d’un site principal 
Le processus de récupération supprime les données de site existantes pour ce site principal dans la base de données du site d’administration centrale. Il remplace les données par les données de site copiées à partir du site principal. Les données de site d’autres sites principaux ne sont pas affectées.


### <a name="site-database-recovery-scenarios"></a>Scénarios de récupération de base de données de site

Suite à la restauration d’une base de données de site à partir d’une sauvegarde, Configuration Manager tente de restaurer les modifications apportées aux données globales et données de site après la dernière sauvegarde de la base de données. Configuration Manager démarre les actions suivantes après la restauration d’une base de données de site à partir d’une sauvegarde :  

#### <a name="recovered-site-is-a-central-administration-site"></a>Le site récupéré est un site d’administration centrale
- Sauvegarde de base de données pendant la période de rétention du suivi des modifications  

     - **Données globales** : Les modifications des données globales après la sauvegarde sont répliquées à partir de tous les sites principaux.  

     - **Données de site** : Les modifications des données du site après la sauvegarde sont répliquées à partir de tous les sites principaux.  

- Sauvegarde de base de données antérieure à la période de rétention du suivi des modifications  

     - **Données globales** : Le site d’administration centrale réinitialise les données globales à partir du site principal de référence, si vous le spécifiez. Ensuite, tous les autres sites principaux réinitialisent les données globales à partir du site d'administration centrale. Si vous ne spécifiez pas de site de référence, tous les sites principaux réinitialisent les données globales à partir du site d’administration centrale. Il s’agit des données qui ont été restaurées à partir de la sauvegarde.  

     - **Données de site** : Le site d'administration centrale réinitialise les données du site à partir de chaque site principal.  

#### <a name="recovered-site-is-a-primary-site"></a>Le site récupéré est un site principal
- Sauvegarde de base de données pendant la période de rétention du suivi des modifications  

     - **Données globales** : Les modifications apportées aux données globales après la sauvegarde sont répliquées à partir du site d'administration centrale.  

     - **Données de site** : Le site d'administration centrale réinitialise les données du site à partir du site principal. Les modifications après la sauvegarde sont perdues. Les clients regénèrent la plupart des données quand ils envoient des informations au site principal.  

- Sauvegarde de base de données antérieure à la période de rétention du suivi des modifications  
     - **Données globales** : Le site principal réinitialise les données globales à partir du site d'administration centrale.  

     - **Données de site** : Le site d'administration centrale réinitialise les données du site à partir du site principal. Les modifications après la sauvegarde sont perdues. Les clients regénèrent la plupart des données quand ils envoient des informations au site principal.  



## <a name="site-recovery-procedures"></a>Procédures de récupération de site

Appliquez l’une des procédures suivantes pour récupérer votre serveur de site ainsi que la base de données de site :


### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Démarrer une récupération de site avec l’Assistant Installation

1.  Copiez le [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) à un emplacement en dehors du dossier d’installation de Configuration Manager. À partir de la copie du dossier CD.Latest, exécutez l’Assistant Installation de Configuration Manager.  

2.  Sur la page **Mise en route** , sélectionnez **Récupérer un site**, puis cliquez sur **Suivant**.  

3.  Terminez l'Assistant en utilisant les options qui conviennent à la récupération de votre site.  

     - Pendant la récupération, le programme d’installation identifie le port SQL Server Service Broker (SSB) utilisé par SQL Server. Ne modifiez pas ce paramètre de port lors de la récupération, sinon la réplication de données ne fonctionnera pas correctement une fois la récupération terminée.  

     - Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager dans l’Assistant Installation.  


### <a name="start-an-unattended-site-recovery"></a>Démarrer une récupération de site en mode sans assistance

1. Préparez le script d'installation sans assistance pour les options dont vous avez besoin pour la récupération du site. Pour plus d’informations, consultez [Récupération de sites en mode sans assistance](/sccm/core/servers/manage/unattended-recovery).  

2. Exécutez le programme d’installation de Configuration Manager en utilisant l’option de ligne de commande `/script`. Par exemple, vous créez un fichier d’initialisation de l’installation nommé **ConfigMgrUnattend.ini**. Vous l’enregistrez dans le répertoire `C:\Temp` de l’ordinateur sur lequel vous exécutez le programme d’installation. Utilisez la commande suivante :  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  


> [!NOTE]   
>  Après la récupération d’un site d’administration centrale, l’établissement de la réplication de certaines données de site à partir des sites enfants peut échouer. Ces données peuvent inclure l’inventaire matériel, l’inventaire logiciel et les messages d’état.
>
>  Si ce problème se produit, réinitialisez **ConfigMgrDRSSiteQueue** pour la réplication de base de données. Utilisez **SQL Server Manager** pour exécuter la requête suivante sur la base de données de site pour le site d’administration centrale :
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## <a name="post-recovery-tasks"></a>Tâches postérieures à la récupération

Après avoir récupéré votre site, il existe plusieurs tâches à effectuer après la récupération, pour que celle-ci soit complète. Utilisez les sections suivantes pour vous aider à terminer le processus de récupération de site.


### <a name="reenter-user-account-passwords"></a>Entrer de nouveau les mots de passe des comptes d’utilisateur

Après une récupération de serveur de site, entrez de nouveau les mots de passe des comptes d’utilisateur du site. Ces mots de passe sont réinitialisés lors de la récupération de site. Les comptes sont répertoriés dans la page **Terminé** de l’Assistant Installation après la récupération du site. La liste est également enregistrée dans `C:\ConfigMgrPostRecoveryActions.html` sur le serveur de site récupéré.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Entrer de nouveau les mots de passe des comptes d’utilisateur après la récupération du site
1. Ouvrez la console Configuration Manager et connectez-vous au site récupéré.  

2. Accédez à l’espace de travail **Administration**, développez **Sécurité**, puis cliquez sur **Comptes**.  

3. Pour chaque compte, effectuez les opérations suivantes pour entrer de nouveau le mot de passe :  

     1. Sélectionnez le compte dans la liste identifiée après la récupération du site.  

     2. Cliquez dans le ruban sur **Propriétés**.  

     3. Sous l’onglet **Général**, cliquez sur **Définir** et entrez de nouveau le mot de passe du compte.  

     4. Cliquez sur **Vérifier**, sélectionnez la source de données appropriée pour le compte d’utilisateur sélectionné, puis cliquez sur **Tester la connexion**. Cette étape permet de tester si le compte d’utilisateur peut se connecter à la source de données et de vérifier les informations d’identification.  

     5. Cliquez sur **OK** pour enregistrer les modifications du mot de passe, puis sur **OK** pour fermer la page de propriétés du compte.  


### <a name="reenter-sideloading-keys"></a>Entrer de nouveau les clés de chargement indépendant

Après une récupération de serveur de site, entrez de nouveau les clés de chargement indépendant Windows spécifiées pour le site. Ces clés sont réinitialisées lors de la récupération de site. Une fois que vous avez entré de nouveau les clés de chargement indépendant, le site réinitialise le nombre dans la colonne **Activations utilisées** pour les clés de chargement indépendant Windows. 

Par exemple, avant la défaillance du site, le nombre de la colonne **Total activations** est **100**. Le nombre de clés qui ont été utilisées par les appareils, ou **Activations utilisées**, est **90**. Après la récupération du site, la colonne **Total activations** affiche toujours **100**, mais la colonne **Activations utilisées** affiche la valeur erronée de **0**. Une fois que 10 nouveaux appareils auront utilisé une clé de chargement indépendant, il ne restera aucune clé de chargement indépendant et le onzième appareil ne parviendra pas à appliquer une clé de chargement indépendant.


### <a name="recreate-the-microsoft-intune-subscription"></a>Recréer l’abonnement Microsoft Intune

Si vous récupérez un serveur de site Configuration Manager une fois qu’il a été réinitialisé, l’abonnement Microsoft Intune n’est pas restauré. Reconnectez l’abonnement après avoir récupéré le site. Ne créez pas de demande APN. Au lieu de cela, chargez le fichier PEM valide en cours. Utilisez le fichier que vous avez chargé la dernière fois que vous avez configuré ou renouvelé la gestion iOS. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).


### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurer SSL pour les rôles de système de site qui utilisent IIS

Quand vous récupérez des systèmes de site qui exécutent IIS et qui ont été configurés pour le protocole HTTPS, reconfigurez IIS pour utiliser le certificat de serveur web.


### <a name="reinstall-hotfixes"></a>Réinstaller les correctifs 

Après la récupération d'un site, vous devez réinstaller tous les correctifs qui étaient appliqués au serveur de site. Après la récupération d’un site, consultez la liste des correctifs précédemment installés dans la page **Terminé** de l’Assistant Installation. Cette liste est également enregistrée dans `C:\ConfigMgrPostRecoveryActions.html` sur le serveur de site récupéré.


### <a name="recover-custom-reports"></a>Récupérer des rapports personnalisés 

Certains clients créent des rapports personnalisés dans SQL Server Reporting Services. En cas d’échec de ce composant, récupérez les rapports à partir d’une sauvegarde du serveur de rapports. Pour plus d’informations sur la restauration de vos rapports personnalisés dans Reporting Services, consultez [Opérations de sauvegarde et de restauration pour une installation Reporting Services ](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).


### <a name="recover-content-files"></a>Récupérer des fichiers de contenu

La base de données de site assure le suivi de l’emplacement où le serveur de site stocke les fichiers de contenu. Les fichiers de contenu ne sont pas sauvegardés ni restaurés lors du processus de sauvegarde et de récupération. Pour récupérer complètement les fichiers de contenu, restaurez la bibliothèque de contenu et les fichiers sources du package à leur emplacement d’origine. Il existe plusieurs méthodes pour récupérer vos fichiers de contenu. La méthode la plus simple consiste à restaurer les fichiers à partir d’une sauvegarde du système de fichiers du serveur de site.

Si vous ne disposez pas d’une sauvegarde du système de fichiers pour les fichiers sources du package, vous devez les copier ou les télécharger manuellement. Ce processus est similaire à la création initiale du package. Exécutez la requête suivante dans SQL Server pour trouver l’emplacement source du package pour tous les packages et applications : `SELECT * FROM v_Package`. Identifiez le site source du package en examinant les trois premiers caractères de l’ID de package. Par exemple, si l'ID de package est CEN00001, le code de site pour le site source est CEN. Lorsque vous restaurez les fichiers sources du package, ceux-ci doivent être restaurés vers le même emplacement que celui dans lequel ils se trouvaient avant la défaillance.

Si vous ne disposez pas d’une sauvegarde du système de fichiers qui inclut la bibliothèque de contenu, vous pouvez utiliser les options de restauration suivantes :  

- **Importer un fichier de contenu préparé** : Dans une hiérarchie Configuration Manager, vous pouvez créer un fichier de contenu préparé avec tous les packages et applications d’un autre emplacement. Importez ensuite le fichier de contenu préparé pour récupérer la bibliothèque de contenu sur le serveur de site.  

- **Mettre à jour le contenu** : Configuration Manager copie le contenu de la source du package vers la bibliothèque de contenu. Pour que cette action soit correctement effectuée, les fichiers sources du package doivent être disponibles à l’emplacement d’origine. Effectuez cette action sur chaque package et chaque application.


### <a name="recover-custom-software-updates"></a>Récupérer les mises à jour logicielles personnalisées

Quand vous avez inclus les fichiers de base de données de l’éditeur de mise à jour System Center dans votre plan de sauvegarde, vous pouvez récupérer les bases de données en cas de panne de l’ordinateur sur lequel l’éditeur de mise à jour s’exécute. Pour plus d’informations sur l’éditeur de mise à jour, consultez [Éditeur de mise à jour System Center](/sccm/sum/tools/updates-publisher).

#### <a name="restore-the-updates-publisher-database"></a>Restaurer la base de données de l’éditeur de mise à jour
1. Réinstallez l’éditeur de mise à jour sur l’ordinateur récupéré.  

2. Copiez le fichier de base de données **Scupdb.sdf** depuis la destination de sauvegarde vers `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` sur l’ordinateur qui exécute l’éditeur de mise à jour.  

3. Quand plusieurs utilisateurs exécutent l’éditeur de mise à jour sur l’ordinateur, copiez chaque fichier de base de données à l’emplacement du profil de l’utilisateur approprié.  


### <a name="user-state-migration-data"></a>Données de migration de l'état utilisateur

Dans le cadre des propriétés du point de migration d’état, vous pouvez spécifier les dossiers qui conservent les données de l’état utilisateur. Après avoir récupéré un point de migration d’état, restaurez manuellement les données de l’état utilisateur sur le serveur. Restaurez les données dans les mêmes dossiers qu’elles occupaient avant la panne.


### <a name="regenerate-the-certificates-for-distribution-points"></a>Régénérer les certificats pour les points de distribution

Après la restauration d’un site, le fichier **distmgr.log** peut contenir l’entrée suivante pour un ou plusieurs points de distribution : `Failed to decrypt cert PFX data`. Cette entrée indique le site ne peut pas déchiffrer les données de certificat du point de distribution. Pour résoudre ce problème, regénérez ou réimportez le certificat pour les points de distribution concernés. Utilisez l’applet de commande PowerShell [Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint).


### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Mettre à jour les certificats utilisés pour les points de distribution cloud

Configuration Manager requiert un certificat de gestion Azure pour la communication entre le serveur de site et les points de distribution cloud. Suite à la récupération d’un site, mettez à jour les certificats des points de distribution cloud.



## <a name="recover-a-secondary-site"></a>Récupération d'un site secondaire

Configuration Manager ne prend pas en charge la sauvegarde de la base de données sur un site secondaire, mais prend en charge la récupération en réinstallant le site secondaire. La récupération de site secondaire est requise dans le cas de défaillance d'un site secondaire Configuration Manager.


### <a name="requirements"></a>spécifications

- Le serveur doit respecter tous les prérequis de site secondaire et disposer des droits de sécurité appropriés configurés.  

- Utilisez le chemin d’installation qui a été utilisé pour le site défaillant.  

- Utilisez un serveur avec la même configuration que le serveur défaillant. Cette configuration inclut son nom de domaine complet.  

- Le serveur doit avoir la même configuration SQL Server que le site défaillant.  

     - Lors de la récupération d’un site secondaire, Configuration Manager n’installe pas SQL Server Express s’il n’est pas déjà installé sur l’ordinateur.  

     - Utilisez la même version de SQL Server et la même instance de SQL Server que vous avez utilisées pour la base de données de site secondaire avant la défaillance.  


### <a name="procedure"></a>Procédure

Utilisez l’action **Récupérer le site secondaire** à partir du nœud **Sites** dans la console Configuration Manager. Contrairement à d’autres types de sites, la récupération d’un site secondaire n’utilise pas un fichier de sauvegarde. Ce processus réinstalle les fichiers du site secondaire sur le serveur défaillant. Une fois le site réinstallé, les données du site secondaire sont réinitialisées à partir du site principal parent.

Pendant le processus de récupération, Configuration Manager vérifie si la bibliothèque de contenu existe bien sur le serveur de site secondaire. Il vérifie également que le contenu approprié est disponible. Le site secondaire utilise la bibliothèque de contenu existante, si elle inclut le contenu approprié. Sinon, pour récupérer la bibliothèque de contenu d’un site secondaire, redistribuez ou préparez le contenu sur le serveur.

Quand vous disposez d’un point de distribution qui ne se trouve pas sur le serveur de site secondaire, vous n’avez pas à réinstaller le point de distribution lors d’une récupération du site secondaire. Après la restauration du site secondaire, le site se synchronise automatiquement avec le point de distribution.

Vous pouvez vérifier l’état de la récupération du site secondaire à l’aide de l’action **Afficher l’état d’installation** à partir du nœud **Sites** dans la console Configuration Manager.
