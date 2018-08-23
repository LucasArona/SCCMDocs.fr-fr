---
title: Sauvegarder des sites
titleSuffix: Configuration Manager
description: Apprenez à sauvegarder vos sites avant toute défaillance ou perte de données dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 39af53c6ddfdb58f340432aa3392a046cdeef428
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386210"
---
# <a name="back-up-a-configuration-manager-site"></a>Sauvegarde d'un site Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Préparez les approches de sauvegarde et de récupération pour éviter la perte de données. Pour les sites Configuration Manager, une approche de sauvegarde et de récupération peut vous permettre de récupérer des sites et des hiérarchies plus rapidement avec une moindre perte de données.  

Les sections de cet article peuvent vous aider à sauvegarder vos sites. Pour récupérer un site, consultez [Récupération pour Configuration Manager](/sccm/core/servers/manage/recover-sites).  



## <a name="considerations-before-creating-a-backup"></a>Éléments à prendre en considération avant de créer une sauvegarde  

-   Si vous utilisez un groupe de disponibilité SQL Server Always On pour héberger la base de données du site : modifiez vos plans de sauvegarde et de récupération comme indiqué dans [Se préparer à utiliser SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-backup).  

-   Configuration Manager peut récupérer la base de données du site à partir de la tâche de sauvegarde de Configuration Manager. Il peut également utiliser une sauvegarde de la base de données du site que vous créez avec un autre processus.   

     Par exemple, vous pouvez restaurer la base de données du site à partir d’une sauvegarde créée dans le cadre d’un plan de maintenance Microsoft SQL Server. Vous pouvez également utiliser une sauvegarde créée à l’aide de Data Protection Manager pour sauvegarder la base de données du site.  

-   À partir de la version 1806, installez un serveur de site supplémentaire en mode *passif*. Le serveur de site en mode passif s’ajoute à votre serveur de site existant, qui est en mode *actif*. Un serveur de site en mode passif est disponible pour une utilisation immédiate, en cas de besoin. Pour plus d’informations, consultez [Haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability). Bien que ce rôle ne supprime pas la nécessité de planifier et de mettre en œuvre des opérations de sauvegarde et de récupération, il permet de réduire considérablement les efforts liés à la récupération d’un site en cas de besoin.  
  

####  <a name="using-data-protection-manager-to-back-up-your-site-database"></a>Utilisation de Data Protection Manager pour sauvegarder votre base de données de site
Vous pouvez utiliser System Center DPM (Data Protection Manager) pour sauvegarder la base de données du site Configuration Manager.

Créez un groupe de protection dans DPM pour l’ordinateur de la base de données du site. Dans la page **Sélectionner les membres du groupe** de l’Assistant Nouveau groupe de protection, sélectionnez le service Enregistreur SMS dans la liste des sources de données. Sélectionnez ensuite la base de données du site en tant que membre approprié. Pour plus d’informations sur l’utilisation de DPM, consultez la bibliothèque de documentation de [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).  

> [!IMPORTANT]  
>  Configuration Manager ne prend pas en charge la sauvegarde DPM d’un cluster SQL Server qui utilise une instance nommée. En revanche, il prend en charge la sauvegarde DPM sur un cluster SQL Server qui utilise l’instance par défaut de SQL Server.  

Après avoir restauré la base de données du site, suivez les étapes du processus d’installation pour récupérer le site. Pour utiliser la base de données du site que vous avez sauvegardée avec Data Protection Manager, sélectionnez l’option de récupération **Utiliser une base de données de site récupérée manuellement**.  



## <a name="backup-maintenance-task"></a>Tâche de maintenance de sauvegarde
Il est possible d'automatiser la sauvegarde des sites Configuration Manager en planifiant une tâche de maintenance de sauvegarde du serveur de site prédéfinie. Cette tâche a les fonctionnalités suivantes :

-   s’exécute selon un calendrier ;
-   sauvegarde la base de données du site ;
-   sauvegarde des clés de Registre spécifiques ;
-   sauvegarde des dossiers et fichiers spécifiques ;
-   sauvegarde le [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)   

Planifiez l’exécution de la tâche de sauvegarde du site par défaut au moins tous les cinq jours. En effet, Configuration Manager utilise une période de cinq jours comme *Période de rétention du suivi des modifications SQL Server*. Pour plus d’informations, consultez [Période de rétention du suivi des modifications SQL Server](/sccm/protect/understand/recover-sites#bkmk_SQLretention).

Pour simplifier le processus de sauvegarde, vous pouvez créer un fichier **AfterBackup.bat**. Ce script exécute automatiquement des actions postérieures à la sauvegarde, une fois la tâche de sauvegarde correctement effectuée. Utilisez le fichier AfterBackup.bat pour archiver l’instantané de sauvegarde dans un emplacement sécurisé. Vous pouvez également utiliser le fichier AfterBackup.bat pour copier des fichiers vers votre dossier de sauvegarde, ou pour démarrer d’autres tâches de sauvegarde.  

Vous pouvez sauvegarder un site d’administration centrale et un site principal. Les sites secondaires ou les serveurs de système de site n’ont pas de tâches de sauvegarde.

Quand le service de sauvegarde de Configuration Manager s’exécute, il suit les instructions définies dans le fichier de contrôle de sauvegarde : `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup.box\Smsbkup.ctl`. Vous pouvez apporter des modifications à ce fichier de contrôle de la sauvegarde afin de changer le comportement du service de sauvegarde.  

Les informations sur l’état de la sauvegarde du site sont enregistrées dans le fichier **Smsbkup.log** . Ce fichier est créé dans le dossier de destination que vous spécifiez dans les propriétés de la tâche de maintenance de sauvegarde du serveur de site.  

#### <a name="to-enable-the-site-backup-maintenance-task"></a>Pour activer la tâche de maintenance de sauvegarde de site  
1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2.  Sélectionnez le site pour lequel vous souhaitez activer la tâche de maintenance de sauvegarde du site.  

3.  Cliquez dans le ruban sur **Tâches de maintenance du site**.  

4.  Sélectionnez la tâche de **sauvegarde du serveur de site**, puis cliquez sur **Modifier**.  

5.  Sélectionnez l’option **Activer cette tâche**. Cliquez sur **Définir les chemins** pour spécifier la destination de la sauvegarde. Les options suivantes sont disponibles :  

    > [!IMPORTANT]  
    >  Pour empêcher la falsification des fichiers de sauvegarde, stockez les fichiers dans un emplacement sécurisé. Le chemin de sauvegarde le plus sûr est un lecteur local, vous pouvez donc définir des autorisations de fichiers NTFS sur le dossier. Configuration Manager ne chiffre pas les données de sauvegarde stockées dans le chemin de sauvegarde.  

    -   **Lecteur local sur le serveur de site pour les données de site et la base de données** : spécifie que la tâche stocke les fichiers de sauvegarde du site et de la base de données du site dans le chemin spécifié sur le lecteur de disque local du serveur de site. Créez le dossier local avant l’exécution de la tâche de sauvegarde. Le compte système local sur le serveur de site doit disposer des autorisations de fichiers NTFS d’accès en **écriture** sur le dossier local pour la sauvegarde du serveur de site. Le compte système local sur l’ordinateur qui exécute SQL Server doit disposer des autorisations NTFS d’accès en **écriture** sur le dossier pour la sauvegarde de la base de données du site.  

    -   **Chemin d’accès réseau (nom UNC) aux données de site et à la base de données** : spécifie que la tâche stocke les fichiers de sauvegarde du site et de la base de données du site dans le chemin réseau spécifié. Créez le partage avant l’exécution de la tâche de sauvegarde. Le compte d’ordinateur du serveur de site doit disposer des autorisations de partage et des autorisations NTFS d’accès en **écriture** pour le dossier réseau partagé. Si SQL Server est installé sur un autre ordinateur, le compte d’ordinateur du serveur SQL Server doit avoir les mêmes autorisations.  

    -   **Lecteurs locaux sur le serveur de site et SQL Server** : spécifie que la tâche stocke les fichiers de sauvegarde du site dans le chemin spécifié sur le lecteur local du serveur de site. La tâche stocke les fichiers de sauvegarde de la base de données du site dans le chemin spécifié sur le lecteur local du serveur de base de données du site. Créez les dossiers locaux avant l’exécution de la tâche de sauvegarde. Le compte d'ordinateur du serveur de site doit disposer des autorisations NTFS en **écriture** sur le dossier créé sur le serveur de site. Le compte d'ordinateur de SQL Server doit disposer des autorisations NTFS en **écriture** sur le dossier créé sur le serveur de base de données de site. Cette option est disponible uniquement quand la base de données du site n’est pas installée sur le serveur de site.  

    > [!NOTE]  
    >   L’option permettant d’accéder à la destination de sauvegarde est uniquement disponible quand vous spécifiez le chemin réseau de la destination de sauvegarde.  
    >  
    > Le nom de dossier ou le nom de partage utilisé pour la destination de sauvegarde ne prend pas en charge l’utilisation des caractères Unicode.  

6.  Configurez une planification pour la tâche de sauvegarde de site. Définissez une planification de sauvegarde située en dehors des heures de travail. Si vous avez une hiérarchie, définissez une planification qui s’exécute au moins deux fois par semaine. En cas de défaillance du site, cette planification garantit une rétention maximale des données.  

    Quand vous exécutez la console Configuration Manager sur le même serveur de site que celui que vous configurez pour la sauvegarde, la tâche de sauvegarde utilise l’heure locale pour la planification. Quand vous exécutez la console Configuration Manager à partir d’un autre ordinateur, la tâche de sauvegarde utilise le temps UTC (temps universel coordonné) pour la planification.  

7.  Indiquez si vous souhaitez créer une alerte en cas d’échec de la tâche de sauvegarde du site. Quand cette option est sélectionnée, Configuration Manager crée une alerte critique en cas d’échec de la sauvegarde. Vous pouvez consulter ces alertes dans le nœud **Alertes** de l’espace de travail **Analyse**.  

#### <a name="verify-that-the-backup-site-server-maintenance-task-is-running"></a>Vérifier que la tâche de maintenance de sauvegarde du serveur de site est en cours d’exécution  

-   Vérifiez l'horodatage sur les fichiers dans le dossier de destination de sauvegarde qui a été créé par la tâche. Vérifiez que l’horodatage est mis à jour en fonction de la dernière exécution planifiée de la tâche.  

-   Accédez au nœud **État du composant** de l’espace de travail **Analyse**. Consultez les messages d’état pour **SMS_SITE_BACKUP**. Une fois la sauvegarde du site correctement effectuée, vous voyez l’ID de message **5035**. Ce message indique que la sauvegarde du site s’est effectuée sans erreurs.  

-   Quand vous configurez la tâche de sauvegarde pour créer une alerte en cas d’échec, recherchez les alertes d’échec de sauvegarde dans le nœud **Alertes** de l’espace de travail **Analyse**.  

-   Ouvrez l’Explorateur Windows sur le serveur de site, puis accédez à `<ConfigMgrInstallationFolder>\Logs`. Recherchez les avertissements et les erreurs dans **Smsbkup.log**. Une fois la sauvegarde du site correctement effectuée, le journal affiche `Backup completed` avec l’ID de message `STATMSG: ID=5035`.  

    > [!TIP]  
    >  En cas d’échec de la tâche de maintenance de sauvegarde, redémarrez la tâche de sauvegarde en arrêtant, puis en redémarrant le service Windows **SMS_SITE_BACKUP**.  



## <a name="archive-the-backup-snapshot"></a>Archiver l'instantané de sauvegarde  
La tâche de sauvegarde crée un instantané de sauvegarde au cours de sa première exécution. Vous pouvez utiliser cet instantané pour récupérer votre serveur de site en cas d’échec. Quand la tâche de sauvegarde se réexécute selon la planification définie, elle crée un instantané de sauvegarde qui remplace l’instantané précédent. Ainsi, le site n’a qu’un seul instantané de sauvegarde. Vous n’avez donc aucun moyen de récupérer un instantané de sauvegarde antérieur.  

Conservez plusieurs archives de l’instantané de sauvegarde pour les raisons suivantes :  

-   Il arrive souvent que les médias de sauvegarde soient défectueux, qu’ils se perdent ou qu’ils contiennent uniquement une sauvegarde partielle. La récupération d'un site principal autonome défaillant à partir d'une sauvegarde ancienne est un moindre mal. Pour un serveur de site situé dans une hiérarchie, la sauvegarde doit se trouver dans la période de rétention du suivi des modifications SQL Server, ou bien la sauvegarde n’est pas obligatoire.  

-   La corruption des données sur un site peut passer inaperçue pendant plusieurs cycles de sauvegarde. Vous devrez peut-être utiliser un instantané de sauvegarde antérieur à la corruption du site. Cela s’applique à un site principal autonome et aux sites d’une hiérarchie où la sauvegarde se trouve dans la période de rétention du suivi des modifications SQL Server.  

-   Il est possible que le site n’ait aucun instantané de sauvegarde. Par exemple, en cas d’échec de la tâche de maintenance de sauvegarde du serveur de site. Dans la mesure où la tâche de sauvegarde supprime l’instantané de sauvegarde précédent avant de commencer à sauvegarder les données actuelles, aucun instantané de sauvegarde valide n’est disponible.  



## <a name="using-the-afterbackupbat-file"></a>Utilisation du fichier AfterBackup.bat  
Après avoir sauvegardé correctement le site, la tâche de sauvegarde tente automatiquement d’exécuter un script nommé **AfterBackup.bat**. Créez manuellement le fichier AfterBackup.bat sur le serveur de site dans `<ConfigMgrInstallationFolder>\Inboxes\Smsbkup`. S’il existe un fichier AfterBackup.bat dans le dossier approprié, il s’exécute automatiquement à la fin de la tâche de sauvegarde.

Le fichier AfterBackup.bat vous permet d’archiver l’instantané de sauvegarde à la fin de chaque opération de sauvegarde. Il peut effectuer automatiquement d’autres tâches postérieures à la sauvegarde, qui ne font pas partie de la tâche de maintenance de sauvegarde du serveur de site. Le fichier AfterBackup.bat intègre les opérations d'archivage et de sauvegarde, permettant ainsi d'archiver chaque nouvel instantané de sauvegarde.

Si le fichier AfterBackup.bat n’est pas présent, la tâche de sauvegarde l’ignore sans que cela impacte l’opération de sauvegarde. Pour vérifier que la tâche de sauvegarde a correctement exécuté ce script, accédez au nœud **État du composant** dans l’espace de travail **Analyse**, puis examinez les messages d’état de **SMS_SITE_BACKUP**. Quand la tâche démarre correctement le fichier de commandes AfterBackup.bat, vous voyez l’ID de message **5040**.  

> [!TIP]  
>  Pour archiver les fichiers de sauvegarde de votre serveur de site avec AfterBackup.bat, vous devez utiliser un outil de commande de copie dans le fichier de commandes. [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) de Windows Server est un exemple de ce genre d’outil. Par exemple, créez le fichier AfterBackup.bat avec la commande suivante : `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`  

Bien que la finalité d’AfterBackup.bat soit d’archiver des instantanés de sauvegarde, vous pouvez créer un fichier AfterBackup.bat pour exécuter des tâches supplémentaires à la fin de chaque opération de sauvegarde.  



##  <a name="supplemental-backup-tasks"></a>Tâches de sauvegarde supplémentaires  
La tâche de maintenance de sauvegarde du serveur de site fournit un instantané de sauvegarde pour les fichiers du serveur de site et la base de données du site. Il existe d’autres éléments non sauvegardés que vous devez prendre en compte quand vous créez votre stratégie de sauvegarde. Aidez-vous des sections suivantes pour effectuer votre stratégie de sauvegarde Configuration Manager.  

### <a name="back-up-custom-reports"></a>Sauvegarder des rapports personnalisés   
Si vous modifiez des rapports personnalisés prédéfinis ou créés dans SQL Server Reporting Services, créez une sauvegarde pour les fichiers de base de données du serveur de rapports. La sauvegarde du serveur de rapports doit inclure les composants suivants :
- Fichiers sources des rapports et des modèles
- Clés de chiffrement
- Assemblys ou extensions personnalisés
- Fichiers de configuration
- Vues SQL Server personnalisées utilisées dans les rapports personnalisés
- Procédures stockées personnalisées  

> [!IMPORTANT]  
>  Quand Configuration Manager est mis à niveau vers une version plus récente, les rapports prédéfinis peuvent être remplacés par de nouveaux rapports. Si vous modifiez un rapport prédéfini, veillez à le sauvegarder pour le restaurer ensuite dans Reporting Services.  

Pour plus d’informations sur la sauvegarde de rapports personnalisés dans Reporting Services, consultez [Opérations de sauvegarde et de restauration pour Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).  

### <a name="back-up-content-files"></a>Sauvegarder des fichiers de contenu  
La bibliothèque de contenu dans Configuration Manager est l’emplacement où sont stockés tous les fichiers de contenu pour tous les déploiements de logiciels. La bibliothèque de contenu se trouve sur le serveur de site et sur chaque point de distribution. La tâche de maintenance de sauvegarde du serveur de site ne sauvegarde pas la bibliothèque de contenu, ni les fichiers sources du package. Quand un serveur de site est défaillant, les informations relatives à la bibliothèque de contenu sont restaurées dans la base de données du site. Toutefois, vous devez restaurer la bibliothèque de contenu et les fichiers sources du package.  

-   La bibliothèque de contenu doit être restaurée avant que vous puissiez redistribuer le contenu vers des points de distribution. Quand vous démarrez la redistribution du contenu, Configuration Manager copie les fichiers de la bibliothèque de contenu du serveur de site vers les points de distribution. Pour plus d’informations, consultez [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library).  

-   Les fichiers source d'un package doivent être restaurés avant que vous puissiez mettre à jour le contenu sur des points de distribution. Quand vous démarrez une mise à jour de contenu, Configuration Manager copie les fichiers nouveaux ou modifiés de la source du package vers la bibliothèque de contenu. Il copie ensuite les fichiers vers les points de distribution associés. Exécutez la requête SQL Server suivante sur la base de données du site afin de rechercher l’emplacement source du package pour l’ensemble des packages et applications : `SELECT * FROM v_Package`. Vous pouvez identifier le site source du package en examinant les trois premiers caractères de l'ID de package. Par exemple, si l'ID de package est CEN00001, le code de site pour le site source est CEN. Lorsque vous restaurez les fichiers sources du package, ceux-ci doivent être restaurés vers le même emplacement que celui dans lequel ils se trouvaient avant la défaillance.  

Vérifiez que vous incluez à la fois la bibliothèque de contenu et les fichiers sources de package dans la sauvegarde du système de fichiers du serveur de site.  

### <a name="back-up-custom-software-updates"></a>Sauvegarder les mises à jour logicielles personnalisées  
SCUP (System Center Updates Publisher) est un outil autonome qui vous permet de gérer les mises à jour logicielles personnalisées. L’éditeur de mise à jour utilise une base de données locale pour son espace de stockage des mises à jour logicielles. Quand vous utilisez l’éditeur de mise à jour pour gérer les mises à jour logicielles personnalisées, déterminez si vous devez inclure la base de données de l’éditeur de mise à jour dans votre plan de sauvegarde. Pour plus d’informations, consultez [SCUP](/sccm/sum/tools/updates-publisher).  

Utilisez la procédure suivante pour sauvegarder la base de données de l'éditeur de mise à jour.  

#### <a name="back-up-the-updates-publisher-database"></a>Sauvegarder la base de données SCUP  

1.  Sur l’ordinateur qui exécute SCUP, accédez au fichier de base de données SCUP **Scupdb.sdf** dans `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\`. Il existe un fichier de base de données distinct pour chaque utilisateur qui exécute SCUP.  

2.  Copiez le fichier de base de données vers votre destination de sauvegarde. Par exemple, si votre destination de sauvegarde est `E:\ConfigMgr_Backup`, vous pouvez copier le fichier de base de données SCUP vers `E:\ConfigMgr_Backup\SCUP`.  

    > [!TIP]  
    >  Quand il existe plusieurs fichiers de base de données sur un ordinateur, stockez le fichier dans un sous-dossier qui indique le profil utilisateur associé au fichier de base de données. Par exemple, vous pouvez avoir un fichier de base de données dans `E:\ConfigMgr_Backup\SCUP\User1` et un autre fichier de base de données dans `E:\ConfigMgr_Backup\SCUP\User2`.  



## <a name="user-state-migration-data"></a>Données de migration de l'état utilisateur  
Vous pouvez utiliser les séquences de tâches de Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation. Les propriétés du point de migration d’état listent les dossiers qui stockent les données d’état utilisateur. Ces données ne sont pas sauvegardées dans le cadre de la tâche de maintenance de sauvegarde du serveur de site. Dans le cadre de votre plan de sauvegarde, vous devez sauvegarder manuellement les dossiers que vous spécifiez pour stocker les données de migration d'état utilisateur.   

### <a name="determine-the-folders-used-to-store-user-state-migration-data"></a>Déterminer les dossiers utilisés pour stocker les données de migration d’état utilisateur  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Serveurs et rôles de système de site**.  

2.  Sélectionnez le système de site qui héberge le rôle de migration d’état. Sélectionnez ensuite **Point de migration d’état** dans le volet **Rôles système de site**.  

3.  Cliquez dans le ruban sur **Propriétés**.  

4.  Les dossiers qui stockent les données de migration d'état utilisateur sont répertoriés dans la section **Détails du dossier** de l'onglet **Général** .  



## <a name="about-the-sms-writer-service"></a>À propos du service Enregistreur SMS  
L’Enregistreur SMS est un service qui interagit avec le service VSS (Volume Shadow Copy Service) de Windows pendant le processus de sauvegarde. Le service Enregistreur SMS doit être en cours d’exécution pour que la sauvegarde du site Configuration Manager puisse s’effectuer correctement.  

### <a name="process"></a>Processus  
1. L'Enregistreur SMS s'enregistre auprès du service VSS et établit une liaison à ses interfaces et événements. 
2. Lorsque le service VSS diffuse des événements, ou s'il envoie une notification spécifique à l'Enregistreur SMS, ce dernier répond à la notification et entreprend les mesures appropriées. 
3. L’Enregistreur SMS lit le fichier de contrôle de sauvegarde **smsbkup.ctl** situé dans `<ConfigMgrInstallationPath>\inboxes\smsbkup.box`, puis détermine les fichiers et données à sauvegarder. 
4. L’Enregistreur SMS génère des métadonnées, constituées de divers composants, notamment des données spécifiques provenant de la clé de Registre SMS et de ses sous-clés. 
    a. Il envoie les métadonnées à VSS quand celles-ci sont demandées. 
    b. VSS envoie ensuite les métadonnées à l’application à l’origine de la demande, c’est-à-dire le Gestionnaire de sauvegarde Configuration Manager. 
5. Le Gestionnaire de sauvegarde sélectionne les données à sauvegarder, puis les envoie à l’Enregistreur SMS via VSS. 
6. L'Enregistreur SMS prend les mesures appropriées pour préparer la sauvegarde. 
7. Plus tard, quand VSS est prêt à prendre l’instantané : a. Il envoie un événement b. L’Enregistreur SMS arrête tous les services de Configuration Manager c. Il vérifie que les activités de Configuration Manager sont gelées durant la création de l’instantané. 
8. Une fois le processus d'instantané terminé, l'Enregistreur SMS redémarre les services et les activités.

Le service Enregistreur SMS est installé automatiquement. Il doit être en cours d'exécution lorsque l'application VSS demande une sauvegarde ou une restauration.  

### <a name="writer-id"></a>ID du rédacteur  
L’ID de l’Enregistreur SMS est le suivant : **03ba67dd-dc6d-4729-a038-251f7018463b**.  

### <a name="permissions"></a>Autorisations  
Le service Enregistreur SMS doit s'exécuter sous le compte système local.  

### <a name="volume-shadow-copy-service"></a>Service de cliché instantané du volume  
Le service de cliché instantané du volume (VSS) est un ensemble d'API COM qui implémente une structure permettant de réaliser des sauvegardes de volumes en même temps que les applications sur un système continuent d'écrire dans les volumes. Le service VSS fournit une interface cohérente pour la coordination entre les applications de l'utilisateur qui mettent à jour des données sur le disque (le service Enregistreur SMS) et celles qui sauvegardent des applications (le service Gestionnaire de sauvegarde). Pour plus d’informations, consultez [Service VSS](https://go.microsoft.com/fwlink/p/?LinkId=241968).  



## <a name="next-steps"></a>Étapes suivantes
Après avoir créé une sauvegarde, exercez-vous à [récupérer un site](/sccm/protect/understand/recover-sites) avec cette sauvegarde. Cette pratique peut vous aider à vous familiariser avec le processus de récupération avant de devoir vous y fier. Elle peut également contribuer à confirmer la réussite de la sauvegarde pour la finalité attendue.  
