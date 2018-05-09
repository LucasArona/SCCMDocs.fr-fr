---
title: Sauvegarder des sites
titleSuffix: Configuration Manager
description: Découvrez comment sauvegarder vos sites en cas défaillance ou de perte de données dans System Center Configuration Manager.
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b69789fe6e685e2fe42c260e50329f85f2eb421e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="back-up-a-configuration-manager-site"></a>Sauvegarde d'un site Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Préparez les approches de sauvegarde et de récupération pour éviter la perte de données. Pour les sites Configuration Manager, une approche de sauvegarde et de récupération peut vous permettre de récupérer des sites et des hiérarchies plus rapidement avec une moindre perte de données.  

Les sections de cette rubrique peuvent vous aider à sauvegarder vos sites. Pour récupérer un site, consultez [Récupération pour Configuration Manager](/sccm/protect/understand/recover-sites).  

## <a name="considerations-before-creating-a-backup"></a>Éléments à prendre en considération avant de créer une sauvegarde  
-   **Si vous utilisez un groupe de disponibilité SQL Server Always On pour héberger la base de données du site :** modifiez vos plans de sauvegarde et de récupération comme décrit dans la rubrique [Se préparer à utiliser SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).

-   Configuration Manager peut récupérer la base de données de site à partir de la tâche de maintenance de sauvegarde Configuration Manager ou à partir d'une sauvegarde de base de données de site que vous avez créée avec un autre processus.   

    Par exemple, vous pouvez restaurer la base de données de site à partir d'une sauvegarde créée dans le cadre du plan de maintenance de Microsoft SQL Server. Vous pouvez également utiliser une sauvegarde créée à l’aide de la rubrique Utilisation de Data Protection Manager pour sauvegarder votre base de données de site (DPM).

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilisation de Data Protection Manager pour sauvegarder votre base de données de site
Vous pouvez utiliser System Center 2012 Data Protection Manager (DPM) pour sauvegarder votre base de données de site.

Vous devez créer un nouveau groupe de protection dans DPM pour l'ordinateur de base de données de site. Sur la page **Sélectionner les membres du groupe** de l'Assistant Création d'un nouveau groupe de protection, sélectionnez le service Enregistreur SMS dans la liste des sources de données, puis sélectionnez la base de données de site comme membre approprié. Pour plus d'informations sur l'utilisation de DPM pour sauvegarder votre base de données de site, voir [Bibliothèque de documentation de Data Protection Manager](http://go.microsoft.com/fwlink/?LinkId=272772) sur TechNet.  

> [!IMPORTANT]  
>  Configuration Manager ne prend pas en charge la sauvegarde DPM pour un cluster SQL Server qui utilise une instance nommée, mais il prend en charge la sauvegarde DPM sur un cluster SQL Server qui utilise l'instance par défaut de SQL Server.  

 Après la restauration de la base de données de site, suivez les étapes décrites dans le processus d'installation pour récupérer le site. Sélectionnez l'option de récupération **Utiliser une base de données de site qui a été récupérée manuellement** pour utiliser la base de données de site que vous avez récupérée avec Data Protection Manager.  

## <a name="backup-maintenance-task"></a>Tâche de maintenance de sauvegarde
Il est possible d'automatiser la sauvegarde des sites Configuration Manager en planifiant une tâche de maintenance de sauvegarde du serveur de site prédéfinie. Cette tâche :

-   s’exécute selon un calendrier ;
-   sauvegarde la base de données du site ;
-   sauvegarde des clés de Registre spécifiques ;
-   sauvegarde des dossiers et fichiers spécifiques ;
-   sauvegarde le [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)   

Planifiez l’exécution de la tâche de sauvegarde de site par défaut au minimum tous les cinq jours. La raison en est que Configuration Manager utilise une période de 5 jours comme *Période de rétention du suivi des modifications SQL Server*.  (Consultez la section [Période de rétention du suivi des modifications SQL Server](/sccm/protect/understand/recover-sites#bkmk_SQLretention) dans la rubrique Récupérer des sites.)

Pour simplifier le processus de sauvegarde, vous pouvez créer un fichier **AfterBackup.bat** pour accomplir automatiquement des actions postérieures à la sauvegarde une fois la tâche de maintenance de sauvegarde correctement exécutée. Le fichier AfterBackup.bat est généralement utilisé pour archiver l'instantané de sauvegarde à un emplacement sécurisé. Vous pouvez également utiliser le fichier AfterBackup.bat pour copier des fichiers vers votre dossier de sauvegarde et démarrer d'autres tâches de sauvegarde supplémentaires.  

Vous pouvez sauvegarder un site d'administration centrale et un site principal, mais il n'existe pas de prise en charge de la sauvegarde des sites secondaires ou des serveurs de système de site.

Quand le service de sauvegarde de Configuration Manager est en cours d’exécution, il suit les instructions définies dans le fichier de contrôle de sauvegarde (**&lt;dossier_installation_ConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). Vous pouvez apporter des modifications à ce fichier de contrôle de la sauvegarde afin de changer le comportement du service de sauvegarde.  

Les informations sur l’état de la sauvegarde du site sont enregistrées dans le fichier **Smsbkup.log** . Ce fichier est créé dans le dossier de destination spécifié dans les propriétés de la tâche de maintenance de sauvegarde du serveur de site.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Pour activer la tâche de maintenance de sauvegarde de site  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Configuration de site** > **Sites**.  

2.  Sélectionnez le site dans lequel vous souhaitez activer la tâche de maintenance de sauvegarde de site.  

3.  Dans l'onglet **Accueil**, dans le groupe **Paramètres**, cliquez sur **Tâches de maintenance de site**.  

4.  Choisissez **Serveur de site de sauvegarde**  >  **Modifier**.  

5.  Choisissez **Activer cette tâche** > **Définir les chemins** pour spécifier la destination de la sauvegarde. Les options suivantes sont disponibles :  

    > [!IMPORTANT]  
    >  Pour empêcher la falsification des fichiers de sauvegarde, stockez les fichiers dans un emplacement sécurisé. Le chemin de sauvegarde vers un lecteur local est le plus sûr pour pouvoir définir des autorisations de système de fichiers NTFS sur le dossier. Quelle que soit l'option que vous sélectionnez, Configuration Manager ne chiffre pas les données de sauvegarde stockées dans le chemin de sauvegarde.  

    -   **Lecteur local sur le serveur de site pour les données de site et la base de données**: spécifie que les fichiers de sauvegarde pour le site et la base de données de site sont stockés dans le chemin spécifié sur le disque local du serveur de site. Vous devez créer le dossier local avant d'exécuter la tâche de sauvegarde. Le compte système local sur le serveur de site doit disposer des autorisations de système de fichiers NTFS en **écriture** sur le dossier local pour la sauvegarde de serveur de site. Le compte système local sur l'ordinateur qui exécute SQL Server doit disposer des autorisations NTFS en **écriture** sur le dossier pour la sauvegarde de base de données de site.  

    -   **Chemin d’accès réseau (nom UNC) aux données de site et à la base de données**: spécifie que les fichiers de sauvegarde pour le site et la base de données de site sont stockés dans le chemin UNC spécifié. Vous devez créer le partage avant l'exécuter la tâche de sauvegarde. Le compte d'ordinateur du serveur de site et le compte d'ordinateur de SQL Server, si SQL server est installé sur un autre ordinateur, doivent disposer des autorisations NTFS en **écriture** et de partage sur le dossier réseau partagé.  

    -   **Lecteurs locaux sur le serveur de site et SQL Server**: spécifie que les fichiers de sauvegarde pour le site sont stockés dans le chemin spécifié sur le disque local du serveur de site, et les fichiers de sauvegarde pour la base de données de site sont stockés sur le chemin spécifié sur le disque local du serveur de base de données de site. Vous devez créer les dossiers locaux avant d'exécuter la tâche de sauvegarde. Le compte d'ordinateur du serveur de site doit disposer des autorisations NTFS en **écriture** sur le dossier créé sur le serveur de site. Le compte d'ordinateur de SQL Server doit disposer des autorisations NTFS en **écriture** sur le dossier créé sur le serveur de base de données de site. Cette option est disponible uniquement lorsque la base de données de site n'est pas installée sur le serveur de site.  

    > [!NOTE]  
    >   L'option d'accès à la destination de sauvegarde n'est disponible que lorsque vous spécifiez le chemin UNC de la destination de sauvegarde.

    > Le nom de dossier ou le nom de partage utilisé pour la destination de sauvegarde ne prend pas en charge les caractères Unicode.  

6.  Configurez une planification pour la tâche de sauvegarde de site. Comme bonne pratique, considérez une planification de sauvegarde en dehors des heures de travail. Si vous disposez d'une hiérarchie, pensez à une planification qui s'exécute au moins deux fois par semaine pour assurer une conservation maximale des données en cas de défaillance du site.  

    Lorsque vous exécutez la console Configuration Manager sur le même serveur de site que vous configurez pour la sauvegarde, la tâche de maintenance de sauvegarde du serveur de site utilise l'heure locale pour la planification. Lorsque vous exécutez la console Configuration Manager à partir d'un ordinateur distant du site que vous configurez pour la sauvegarde, la tâche de maintenance de sauvegarde du serveur de site utilise le temps universel coordonné (UTC) pour la planification.  

7.  Indiquez si vous souhaitez créer une alerte en cas d'échec de la tâche de sauvegarde de site, cliquez sur **OK**, puis cliquez de nouveau sur **OK**. Lorsqu'il est sélectionné, Configuration Manager crée une alerte critique pour l'échec de sauvegarde, que vous pouvez consulter dans le nœud **Alertes** de l'espace de travail **Surveillance**.  

 Ensuite, vérifiez que la tâche de maintenance de sauvegarde du serveur de site est en cours d’exécution afin de vous assurer que les sauvegardes sont créées.  

#### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Pour vérifier que la tâche de maintenance de sauvegarde du serveur de site est en cours d’exécution  
Vérifiez que la tâche de maintenance de sauvegarde de site est en cours d’exécution en examinant les éléments suivants :  

-   Vérifiez l'horodatage sur les fichiers dans le dossier de destination de sauvegarde qui a été créé par la tâche. Vérifiez que l'horodatage a été mis à jour avec l'heure de la dernière exécution de la tâche.  

-   Dans le nœud **État du composant** de l'espace de travail **Surveillance** , consultez les messages d'état pour SMS_SITE_BACKUP. Lorsque la sauvegarde de site est terminée, le message ID 5035 s'affiche, indiquant que la sauvegarde de site a été effectuée sans erreurs.  

-   Lorsque la tâche de maintenance de sauvegarde du serveur de site est configurée pour créer une alerte en cas d'échec de la sauvegarde, vous pouvez vérifier les échecs de sauvegarde dans le nœud **Alertes** de l'espace de travail **Surveillance** .  

-   Dans &lt;*dossier_installation_ConfigMgr*>\Logs, recherchez les avertissements et les erreurs dans le fichier smsbkup.log. Une fois la sauvegarde de site terminée, `Backup completed` s'affiche avec un horodateur et un ID de message `STATMSG: ID=5035`.  

    > [!TIP]  
    >  Lorsque la tâche de maintenance de la sauvegarde échoue, vous pouvez redémarrer la tâche de sauvegarde en arrêtant, puis en redémarrant le service SMS_SITE_BACKUP.  

## <a name="archive-the-backup-snapshot"></a>Archiver l'instantané de sauvegarde  
La première fois que la tâche de maintenance de sauvegarde du serveur de site est exécutée, elle génère un instantané de sauvegarde que vous pouvez utiliser pour récupérer votre serveur de site en cas de défaillance. Lorsque la tâche de sauvegarde est réexécutée au cours des cycles suivants, un nouvel instantané de sauvegarde est créé et remplace l'instantané précédent. Ainsi, le site n'a qu'un seul instantané de sauvegarde, et vous n'avez aucun moyen de récupérer un instantané de sauvegarde antérieur.  

Il est également recommandé d'effectuer plusieurs archives d'instantanés de sauvegarde pour les raisons suivantes :  

-   Il arrive souvent que le média de sauvegarde soit défectueux, égaré ou ne contienne qu'une partie de la sauvegarde. La récupération d'un site principal autonome défaillant à partir d'une sauvegarde ancienne est un moindre mal. Pour un serveur de site dans une hiérarchie, la sauvegarde doit être dans la période de rétention des modifications de suivi de SQL Server, ou bien la sauvegarde n'est pas requise.  

-   La corruption des données sur un site peut passer inaperçue pendant plusieurs cycles de sauvegarde. Vous devrez peut-être utiliser un instantané de sauvegarde antérieur à la corruption du site. Cela s'applique à un site primaire autonome et aux sites dans une hiérarchie où la sauvegarde se trouve dans la période de rétention des modifications de suivi de SQL Server.  

-   Le site ne dispose peut-être d'aucun instantané de sauvegarde si, par exemple, la tâche de maintenance de sauvegarde du serveur de site échoue. Comme la tâche de sauvegarde supprime l'instantané de sauvegarde précédent avant de démarrer la sauvegarde des données en cours, aucun instantané de sauvegarde valide ne sera disponible.  

## <a name="using-the-afterbackupbat-file"></a>Utilisation du fichier AfterBackup.bat  
Après avoir sauvegardé le site, la tâche de sauvegarde du serveur de site tente automatiquement d'exécuter un fichier nommé AfterBackup.bat. Vous devez créer manuellement le fichier AfterBackup.bat dans &lt;*dossier_installation_ConfigMgr*>\Inboxes\Smsbkup. Si un fichier AfterBackup.bat existe et est stocké dans le dossier approprié, il est exécuté automatiquement à l'issue de l'exécution de la tâche de sauvegarde.

Le fichier AfterBackup.bat permet d'archiver l'instantané de sauvegarde à la fin de chaque opération de sauvegarde, et d'effectuer automatiquement d'autres tâches postérieures à la sauvegarde, qui ne font pas partie de la tâche de maintenance de sauvegarde du serveur de site. Le fichier AfterBackup.bat intègre les opérations d'archivage et de sauvegarde, permettant ainsi d'archiver chaque nouvel instantané de sauvegarde.

Lorsque le fichier AfterBackup.bat n'est pas présent, la tâche de sauvegarde l'ignore sans effet sur l'opération de sauvegarde. Pour vérifier que la tâche de sauvegarde de site a exécuté avec succès le fichier AfterBackup.bat, consultez le nœud **État du composant** dans l'espace de travail **Surveillance** et vérifiez les messages d'état pour SMS_SITE_BACKUP. Lorsque la tâche démarre avec succès le fichier de commande AfterBackup.bat, le message ID 5040 s'affiche.  

> [!TIP]  
>  Pour créer le fichier AfterBackup.bat afin d'archiver vos fichiers de sauvegarde de serveur de site, vous devez utiliser un outil de commande de copie, tel que [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408), dans le fichier de commandes. Par exemple, vous pouvez créer le fichier AfterBackup.bat et, sur la première ligne, ajouter une instruction similaire à la suivante : `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

 Même si le but premier du fichier AfterBackup.bat est d'archiver des instantanés de sauvegarde, vous pouvez créer un fichier AfterBackup.bat pour exécuter d'autres tâches à la fin de chaque opération de sauvegarde.  

##  <a name="supplemental-backup-tasks"></a>Tâches de sauvegarde supplémentaires  
La tâche de maintenance de sauvegarde du serveur de site fournit un instantané de sauvegarde pour les fichiers de serveur de site et la base de données de site, mais il existe certains autres éléments non sauvegardés que vous devez considérer lorsque vous créez votre stratégie de sauvegarde. Utilisez les sections suivantes pour définir votre stratégie de sauvegarde Configuration Manager.  

### <a name="back-up-custom-reporting-services-reports"></a>Sauvegarde des rapports Reporting Services personnalisés  
Lorsque vous avez modifié des rapports Reporting Services personnalisés prédéfinis ou créés, la création d'une sauvegarde pour les fichiers de base de données de serveur du rapport est une partie importante de votre stratégie de sauvegarde. La sauvegarde du serveur de rapports doit inclure une sauvegarde des fichiers sources pour les rapports et les modèles, des clés de cryptage, des assemblys ou des extensions personnalisés, des fichiers de configuration, des vues SQL Server personnalisées, des procédures stockées personnalisées, etc.  

> [!IMPORTANT]  
>  Quand Configuration Manager est mis à niveau vers une version plus récente, les rapports prédéfinis peuvent être remplacés par de nouveaux rapports. Si vous modifiez un rapport prédéfini, sauvegardez le rapport avant d’effectuer la mise à jour, puis restaurez-le dans Reporting Services.  

 Pour plus d’informations sur la sauvegarde de vos rapports personnalisés dans Reporting Services, consultez [Opérations de sauvegarde et de restauration pour Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) dans la documentation en ligne de SQL Server 2014.  

### <a name="back-up-content-files"></a>Sauvegarder des fichiers de contenu  
La bibliothèque de contenu dans Configuration Manager correspond à l'emplacement dans lequel sont enregistrés tous les fichiers de contenu pour le déploiement des mises à jour logicielles, des applications, du système d'exploitation, etc. La bibliothèque de contenu se trouve sur le serveur de site et sur chaque point de distribution. La tâche de maintenance de sauvegarde du serveur de site n'inclut pas une sauvegarde de la bibliothèque de contenu ou des fichiers sources du package. Lors de la défaillance d'un serveur de site, les informations sur les fichiers de la bibliothèque de contenu sont restaurées vers la base de données de site, mais vous devez restaurer la bibliothèque de contenu et les fichiers sources des packages sur le serveur de site.  

-   **Bibliothèque de contenu**: la bibliothèque de contenu doit être restaurée avant que vous puissiez redistribuer le contenu vers des points de distribution. Lorsque vous démarrez la redistribution du contenu, Configuration Manager copie les fichiers depuis la bibliothèque de contenu sur le serveur de site vers les points de distribution. La bibliothèque de contenu pour le serveur de site se trouve dans le dossier SCCMContentLib, qui est généralement situé sur le lecteur qui dispose de la plus grande quantité d'espace libre au moment de l'installation du site.  

-   **Fichiers sources d’un package**: les fichiers sources d’un package doivent être restaurés avant que vous puissiez mettre à jour le contenu sur des points de distribution. Lorsque vous démarrez la mise à jour d'un contenu, Configuration Manager copie les fichiers nouveaux ou modifiés depuis la source du package vers la bibliothèque de contenu, qui à son tour copie les fichiers vers des points de distribution associés. Vous pouvez exécuter la requête suivante dans SQL Server pour trouver l'emplacement source du package pour tous les packages et applications : `SELECT * FROM v_Package`. Vous pouvez identifier le site source du package en examinant les trois premiers caractères de l'ID de package. Par exemple, si l'ID de package est CEN00001, le code de site pour le site source est CEN. Lorsque vous restaurez les fichiers sources du package, ceux-ci doivent être restaurés vers le même emplacement que celui dans lequel ils se trouvaient avant la défaillance.  

 Vérifiez que vous incluez à la fois la bibliothèque de contenu et les emplacements sources du package dans la sauvegarde de votre système de fichiers pour le serveur de site.  

### <a name="back-up-custom-software-updates"></a>Sauvegarder les mises à jour logicielles personnalisées  
 System Center Updates Publisher 2011 est un outil autonome qui vous permet de publier des mises à jour logicielles personnalisées vers Windows Server Update Services (WSUS), de synchroniser les mises à jour logicielles vers Configuration Manager, d’évaluer la compatibilité des mises à jour logicielles et de déployer des mises à jour logicielles personnalisées sur des clients. L’éditeur de mise à jour utilise une base de données locale pour son espace de stockage des mises à jour logicielles. Quand vous utilisez l’éditeur de mise à jour pour gérer les mises à jour logicielles personnalisées, déterminez si vous devez inclure la base de données de l’éditeur de mise à jour dans votre plan de sauvegarde. Pour plus d'informations sur l'éditeur de mise à jour, voir [Éditeur de mise à jour System Center 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) dans la bibliothèque TechCenter de System Center.  

 Utilisez la procédure suivante pour sauvegarder la base de données de l'éditeur de mise à jour.  

#### <a name="to-back-up-the-updates-publisher-2011-database"></a>Pour sauvegarder la base de données de l'éditeur de mise à jour 2011  

1.  Sur l’ordinateur qui exécute l’éditeur de mise à jour, accédez au fichier de base de données de l’éditeur de mise à jour (Scupdb.sdf) dans %*USERPROFILE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\\. Il existe un fichier de base de données différent pour chaque utilisateur qui exécute l’éditeur de mise à jour.  

2.  Copiez le fichier de base de données vers votre destination de sauvegarde. Par exemple, si votre destination de sauvegarde est E:\ConfigMgr_Backup, vous pouvez copier le fichier de base de données de l’éditeur de mise à jour vers E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  Lorsqu'il existe plusieurs fichiers de base de données sur un ordinateur, envisagez de stocker le fichier dans un sous-dossier qui indique le profil utilisateur associé au fichier de base de données. Par exemple, vous pourriez avoir un seul fichier de base de données dans E:\ConfigMgr_Backup\SCUP2011\User1 et un autre fichier de base de données dans E:\ConfigMgr_Backup\SCUP2011\User2.  

## <a name="user-state-migration-data"></a>Données de migration de l'état utilisateur  
Vous pouvez utiliser des séquences de tâches Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation où vous souhaitez conserver l’état utilisateur du système d’exploitation actuel. Les dossiers qui stockent les données d'état utilisateur sont répertoriés dans les propriétés du point de migration d'état. Ces données de migration d'état utilisateur ne sont pas sauvegardées dans le cadre de la tâche de maintenance de sauvegarde du serveur de site. Dans le cadre de votre plan de sauvegarde, vous devez sauvegarder manuellement les dossiers que vous spécifiez pour stocker les données de migration d'état utilisateur.   

### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Pour déterminer les dossiers utilisés pour stocker les données de migration d'état utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis choisissez **Serveurs et rôles de système de site**.  

3.  Sélectionnez le système de site qui héberge le rôle de migration d'état, puis choisissez **Point de migration de l'état** dans **Rôles de système de site**.  


4.  Dans l'onglet **Rôle du site** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  
5.  Les dossiers qui stockent les données de migration d'état utilisateur sont répertoriés dans la section **Détails du dossier** de l'onglet **Général** .  



## <a name="about-the-sms-writer-service"></a>À propos du service Enregistreur SMS  
L'Enregistreur SMS est un service qui interagit avec le service de cliché instantané du volume (VSS, Volume Shadow copy Service) pendant le processus de sauvegarde. Le service Enregistreur SMS doit être en cours d'exécution pour mener à bien la sauvegarde de site Configuration Manager.  

### <a name="purpose"></a>Fonction  
L'Enregistreur SMS s'enregistre auprès du service VSS et établit une liaison à ses interfaces et événements. Lorsque le service VSS diffuse des événements, ou s'il envoie une notification spécifique à l'Enregistreur SMS, ce dernier répond à la notification et entreprend les mesures appropriées. L’Enregistreur SMS lit le fichier de contrôle de sauvegarde (smsbkup.ctl), situé dans &lt;*chemin_installation_ConfigMgr*>\inboxes\smsbkup.box, puis détermine les fichiers et les données à sauvegarder. L'Enregistreur SMS génère des métadonnées, consistant de différents composants, en se basant sur ces informations ainsi que sur des données spécifiques à partir de la clé de Registre SMS et des sous-clés. Il envoie les métadonnées vers le service VSS lorsqu'elles sont demandées. Le service VSS envoie ensuite les métadonnées à l'application faisant la demande ; le Gestionnaire de sauvegarde Configuration Manager. sélectionne les données à sauvegarder et les envoie à l'Enregistreur SMS via le service VSS. L'Enregistreur SMS prend les mesures appropriées pour préparer la sauvegarde. Plus tard, lorsque le service VSS est prêt à prendre l'instantané, il envoie un événement ; l'Enregistreur SMS arrête tous les services Configuration Manager et s'assure que toutes les activités Configuration Manager sont figées pendant la création de l'instantané. Une fois le processus d'instantané terminé, l'Enregistreur SMS redémarre les services et les activités.  

Le service Enregistreur SMS est installé automatiquement. Il doit être en cours d'exécution lorsque l'application VSS demande une sauvegarde ou une restauration.  

### <a name="writer-id"></a>ID du rédacteur  
L’ID d’enregistreur pour l’Enregistreur SMS est le suivant : 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Autorisations  
Le service Enregistreur SMS doit s'exécuter sous le compte système local.  

### <a name="volume-shadow-copy-service"></a>Service de cliché instantané du volume  
Le service de cliché instantané du volume (VSS) est un ensemble d'API COM qui implémente une structure permettant de réaliser des sauvegardes de volumes en même temps que les applications sur un système continuent d'écrire dans les volumes. Le service VSS fournit une interface cohérente pour la coordination entre les applications de l'utilisateur qui mettent à jour des données sur le disque (le service Enregistreur SMS) et celles qui sauvegardent des applications (le service Gestionnaire de sauvegarde). Pour plus d'informations, consultez la rubrique [Volume Shadow Copy Service (Service de cliché instantané du volume)](http://go.microsoft.com/fwlink/p/?LinkId=241968) dans Windows Server TechCenter.  

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé une sauvegarde, exercez-vous à [récupérer un site](/sccm/protect/understand/recover-sites) avec cette sauvegarde. Cela vous aidera à vous familiariser avec le processus de récupération avant d’y recourir en cas de besoin et à confirmer que la sauvegarde créée correspond à son usage prévu.  
