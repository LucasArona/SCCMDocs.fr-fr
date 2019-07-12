---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: Projeter d’utiliser un groupe de disponibilité Always On SQL Server avec Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f88334a9c330d3af298ec63b3d7baa56c9714647
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676602"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Se préparer à l’utilisation de groupes de disponibilité SQL Server Always On avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez cet article pour préparer Configuration Manager à utiliser des groupes de disponibilité Always On SQL Server. Cette fonctionnalité constitue une solution de haute disponibilité et récupération d’urgence pour la base de données du site.  

Configuration Manager prend en charge des groupes de disponibilité :
- Sur les sites principaux et sur le site d’administration centrale.
- Localement ou dans Microsoft Azure.

Quand vous utilisez des groupes de disponibilité dans Microsoft Azure, vous pouvez encore augmenter la disponibilité de la base de données de votre site en utilisant des *groupes de disponibilité Azure*. Pour plus d’informations sur les groupes à haute disponibilité Azure, consultez [Gestion de la disponibilité des machines virtuelles](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

> [!Important]
>  Avant de continuer, familiarisez-vous avec la configuration de SQL Server et les groupes de disponibilité SQL Server. Les informations ci-dessous font référence à la bibliothèque de documentation et aux procédures SQL Server.



## <a name="supported-scenarios"></a>Scénarios pris en charge

Les scénarios suivants sont pris en charge pour l’utilisation de groupes de disponibilité avec Configuration Manager. Pour plus d’informations sur chacun et pour connaître les procédures correspondantes, voir [Configurer des groupes de disponibilité pour Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).

- [Créer un groupe de disponibilité pour l’utiliser avec Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group)  
- [Configurer un site pour utiliser un groupe de disponibilité](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group)  
- [Ajouter ou supprimer des membres de réplica synchrone dans un groupe de disponibilité qui héberge une base de données de site](/sccm/core/servers/deploy/configure/configure-aoag#add-or-remove-synchronous-replica-members)  
- [Configurer des réplicas avec validation asynchrone](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-replica)  
- [Récupérer un site à partir d’un réplica avec validation asynchrone](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site)  
- [Déplacer une base de données de site d’un groupe de disponibilité vers une instance par défaut ou nommée d’un serveur SQL Server autonome](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group)  



## <a name="prerequisites"></a>Prérequis

Les conditions préalables suivantes s’appliquent à tous les scénarios. Si d’autres prérequis s’appliquent à un scénario en particulier, ils sont détaillés dans ce scénario.   

### <a name="configuration-manager-accounts-and-permissions"></a>Comptes et autorisations de Configuration Manager

#### <a name="site-server-to-replica-member-access"></a>Serveur de site pour l’accès au membre de réplica   
Le compte d’ordinateur du serveur de site doit faire partie du groupe **Administrateurs local** sur chaque ordinateur membre du groupe de disponibilité.


### <a name="sql-server"></a>SQL Server

#### <a name="version"></a>Version  
Chaque réplica du groupe de disponibilité doit exécuter une version de SQL Server prise en charge par votre version de Configuration Manager. S’ils sont pris en charge par SQL Server, les différents nœuds d’un groupe de disponibilité peuvent exécuter des versions différentes de SQL Server. Pour plus d’informations, consultez [Versions de SQL Server prises en charge pour Configuration Manager](/sccm/core/plan-design/configs/support-for-sql-server-versions).<!--SCCMDocs issue 656-->

#### <a name="edition"></a>Édition  
Utilisez une édition *Entreprise* de SQL Server.

#### <a name="account"></a>Compte  
Chaque instance de SQL Server peut s’exécuter sous un compte d’utilisateur de domaine (**compte de service**) ou un compte n’appartenant pas à un domaine. Chaque réplica d’un groupe peut avoir une configuration différente. 

- Utilisez un compte ayant aussi peu d’autorisations que possible. Pour plus d’informations, voir [Considérations sur la sécurité d’une installation SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation).  

- Pour plus d’informations sur la configuration des comptes de service et des autorisations pour SQL Server, voir [Configurer les comptes de service Windows et les autorisations](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions).  

- Pour utiliser un compte n’appartenant pas à un domaine, vous devez utiliser des certificats. Pour plus d’informations, voir [Utiliser des certificats pour un point de terminaison de mise en miroir de bases de données (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).  

- Pour plus d’informations, voir [Créer un point de terminaison de mise en miroir de bases de données pour les groupes de disponibilité Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).  


### <a name="availability-group-configurations"></a>Configurations du groupe de disponibilité

#### <a name="replica-members"></a>Membres de réplica  
- Le groupe de disponibilité doit avoir un réplica principal.  

- Dans un groupe de disponibilité, utilisez le nombre et le type de réplicas pris en charge par votre version de SQL Server.

- Vous pouvez utiliser un réplica avec validation asynchrone pour récupérer votre réplica synchrone. Pour plus d’informations, voir [Options de récupération d’une base de données de site](/sccm/core/servers/manage/recover-sites#site-database-recovery-options).  

    > [!Warning]  
    > Configuration Manager ne prend pas en charge le *basculement* pour utiliser le réplica avec validation asynchrone comme base de données de site. Pour plus d’informations, voir [Basculement et modes de basculement (groupes de disponibilité Always On)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups?view=sql-server-2014).  

Configuration Manager ne valide pas l’état du réplica avec validation asynchrone pour vérifier qu’il est à jour. Le fait d’utiliser un réplica avec validation asynchrone comme base de données de site risque de compromettre l’intégrité du site et des données. Par conception, un tel réplica est susceptible d’être désynchronisé. Pour plus d’informations, voir [Vue d’ensemble des groupes de disponibilité Always On SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server).

Chaque membre de réplica doit avoir la configuration suivante :

- utiliser *l’instance par défaut* ou une *instance nommée* ;  

- le paramètre **Connexions dans le rôle principal** défini sur **Autoriser toutes les connexions** ;  

- le paramètre **Secondaire accessible en lecture** défini sur **Oui** ;  

- le **basculement manuel** activé.   

  > [!TIP]
  >  Configuration Manager prend en charge l’utilisation de réplicas synchrones de groupe de disponibilité quand il est configuré pour le **Basculement automatique**. Définissez **Basculement manuel** quand :
  >  -  Vous exécutez le programme d’installation de Configuration Manager pour spécifier l’utilisation de la base de données de site dans le groupe de disponibilité.  
  >  -  Vous installez une mise à jour de Configuration Manager (et pas seulement des mises à jour qui s’appliquent à la base de données de site).  

#### <a name="replica-member-location"></a>Emplacement du membre de réplica
Hébergez tous les réplicas d’un groupe de disponibilité sur site ou sur Microsoft Azure. Les groupes incluant un membre local et un membre dans Azure ne sont pas pris en charge.     

Le programme d’installation de Configuration Manager doit se connecter à chaque réplica. Lorsque vous configurez dans Azure un groupe de disponibilité qui se situe derrière un équilibrage de charge interne ou externe, ouvrez les ports par défaut suivant :   

- Mappeur de point de terminaison RPC : **TCP 135**   

- SQL Server Service Broker : **TCP 4022**  

- SQL sur TCP : **TCP 1433**   


Une fois l’installation terminée, les ports suivants doivent rester ouverts pour Configuration Manager :  

- SQL Server Service Broker : **TCP 4022**  

- SQL sur TCP : **TCP 1433**  

Il est possible d’utiliser des ports personnalisés pour ces configurations. Utilisez les mêmes ports personnalisés par le point de terminaison et sur tous les réplicas du groupe de disponibilité.


#### <a name="listener"></a>Écouteur   
Le groupe de disponibilité doit avoir au moins un *écouteur de groupe de disponibilité*. Lorsque Configuration Manager est configuré pour utiliser la base de données de site dans le groupe de disponibilité, il utilise le nom virtuel de cet écouteur. Bien qu’un groupe de disponibilité puisse contenir plusieurs écouteurs, Configuration Manager ne peut en utiliser qu’un seul. Pour plus d’informations, voir [Créer ou configurer un écouteur de groupe de disponibilité SQL Server](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

#### <a name="file-paths"></a>Chemins d’accès des fichiers   
Quand vous exécutez le programme d’installation de Configuration Manager pour configurer un site de manière à ce qu’il utilise la base de données dans un groupe de disponibilité, chaque serveur réplica secondaire doit avoir un chemin d’accès de fichier SQL Server identique à celui des fichiers de base de données du site sur le réplica principal actuel. Sinon, le programme d’installation ne pourra pas ajouter l’instance du groupe de disponibilité comme nouvel emplacement de la base de données du site.  

Le compte de service SQL Server local doit avoir une autorisation **Contrôle total** sur ce dossier.

En ce qui concerne les serveurs réplicas secondaires, ce chemin d’accès de fichier n’est nécessaire qu’au moment où le programme d’installation de Configuration Manager est utilisé pour spécifier l’instance de base de données dans le groupe de disponibilité. Une fois que la configuration de la base de données du site dans le groupe de disponibilité est terminée, vous pouvez supprimer le chemin inutilisé des serveurs réplicas secondaires.

Par exemple, examinez le scénario suivant :

- Vous créez un groupe de disponibilité qui utilise trois serveurs SQL Server.  

- Votre serveur de réplication principal est une nouvelle installation de SQL Server 2014. Par défaut, il stocke les fichiers .MDF et .LDF de la base de données dans `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`.  

- Vous avez mis à niveau vos deux serveurs réplicas secondaires d’une version antérieure vers SQL Server 2014. Avec la mise à niveau, ces serveurs conservent le chemin d’accès de fichier d’origine pour stocker les fichiers de base de données : `C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA`.  

- Avant de déplacer la base de données de site dans ce groupe de disponibilité, créez le chemin d’accès de fichier suivant sur chaque serveur réplica secondaire : `C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA`. Il s’agit d’une copie du chemin d’accès utilisé sur le réplica principal, même si les réplicas secondaires n’utilisent pas cet emplacement de fichier.  

- Vous accordez ensuite au compte de service SQL Server sur chaque réplica secondaire un accès en contrôle total à l’emplacement du fichier qui vient d’être créé sur ce serveur.  

- Vous pouvez désormais exécuter correctement le programme d’installation de Configuration Manager pour configurer le site afin qu’il utilise la base de données du site figurant dans le groupe de disponibilité.  

#### <a name="configure-the-database-on-a-new-replica"></a>Configurer la base de données sur un nouveau réplica   
 Configurez la base de données de chaque réplica avec les paramètres suivants :  

- Activez **l’Intégration du CLR**. Pour plus d’informations, voir [Intégration du CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration/clr-integration-enabling).  

- Définissez **Taille maximale de remplacement du texte** sur `2147483647`.  

- Choisissez le *compte SA* comme propriétaire de base de données.  

- **Activez** le paramètre **TRUSTWORTHY**. Pour plus d’informations, voir [Propriété de base de données TRUSTWORTHY](https://docs.microsoft.com/sql/relational-databases/security/trustworthy-database-property).   

- Activez le **Service Broker**.  

N’appliquez ces configurations qu’à un réplica principal. Pour configurer un réplica secondaire, commencez par basculer le réplica principal sur le secondaire pour faire de ce dernier le nouveau réplica principal.   


### <a name="verification-script"></a>Script de vérification

Exécutez le script SQL suivant afin de vérifier les configurations de base de données des réplicas principal et secondaires. Pour pouvoir résoudre un problème sur un réplica secondaire, modifiez-le en le définissant comme réplica principal.

```SQL
    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targeted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:
```



## <a name="limitations-and-known-issues"></a>Limitations et problèmes connus

Les limitations suivantes s’appliquent à tous les scénarios.   

#### <a name="unsupported-sql-server-options-and-configurations"></a>Configurations et options SQL Server non prises en charge

- **Groupes de disponibilité de base** : Introduits dans l’édition standard de SQL Server 2016, les groupes de disponibilité de base ne prennent pas en charge l’accès en lecture aux réplicas secondaires. La configuration exige cet accès. Pour plus d’informations, voir [Groupes de disponibilité SQL Server de base](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups?view=sql-server-2017).  

- **Instance de cluster de basculement** : Les instances de cluster de basculement ne sont pas prises en charge pour un réplica que vous utilisez avec Configuration Manager. Pour plus d’informations, voir [Instances de clusters de basculement Always On SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server).  

- **MultiSubnetFailover** : L’utilisation d’un groupe de disponibilité avec Configuration Manager n’est pas prise en charge dans une configuration de sous-réseaux multiples. Il n’est pas non plus possible d’utiliser la chaîne de connexion du mot clé [MultiSubnetFailover](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover).  

#### <a name="sql-servers-that-host-additional-availability-groups"></a>Serveurs SQL Server qui hébergent des groupes de disponibilité supplémentaires
<!--SCCMDocs issue 649-->
Si le serveur SQL Server héberge un ou plusieurs groupes de disponibilité en plus du groupe utilisé pour Configuration Manager, il a besoin de paramètres spécifiques lors de l’exécution du programme d’installation de Configuration Manager. Ces paramètres sont également nécessaires pour installer une mise à jour de Configuration Manager. Chacun des réplicas des différents groupes de disponibilité doit disposer des configurations suivantes :

- basculement manuel ;  
- autoriser toutes les connexions en lecture seule.  

#### <a name="unsupported-database-use"></a>Utilisation non prise en charge de la base de données

- **Configuration Manager prend uniquement en charge la base de données de site dans un groupe de disponibilité :** Les bases de données suivantes ne sont pas prises en charge par Configuration Manager dans un groupe de disponibilité SQL Server Always On :  
    - Base de données Rapports  
    - Base de données WSUS  

- **Base de données préexistante :** Il n’est pas possible d’utiliser une nouvelle base de données créée sur le réplica. Lorsque vous configurez un groupe de disponibilité, restaurez une copie d’une base de données Configuration Manager existante vers le réplica principal.  

#### <a name="setup-errors-in-configmgrsetuplog"></a>Erreurs d’installation dans ConfigMgrSetup.log  
Lorsque le programme d’installation de Configuration Manager est exécuté pour déplacer une base de données de site vers un groupe de disponibilité, il tente de traiter les rôles de base de données sur les réplicas secondaires du groupe de disponibilité. Le fichier **ConfigMgrSetup.log** affiche l’erreur suivante :  

`ERROR: SQL Server error: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Failed to update database "CM_AAA" because the database is read-only. Configuration Manager Setup 1/21/2016 4:54:59 PM 7344 (0x1CB0)`  

Ces erreurs peuvent être ignorées sans problème.

#### <a name="site-expansion"></a>Expansion de site
<!--SCCMDocs issue 568-->
Si vous configurez la base de données de site de façon à ce qu’un site principal autonome utilise SQL Always On, vous ne pouvez pas étendre le site afin d’inclure un site d’administration centrale. Ce processus échoue. Pour étendre le site, supprimez temporairement du groupe de disponibilité la base de données du site principal.



## <a name="changes-for-site-backup"></a>Modifications pour la sauvegarde de site

### <a name="backup-database-files"></a>Sauvegarder des fichiers de base de données
  
Quand une base de données de site utilise un groupe de disponibilité, exécutez la tâche de maintenance intégrée **Sauvegarder le serveur de site** pour sauvegarder les paramètres et les fichiers courants de Configuration Manager. N’utilisez pas les fichiers .MDF ou .LDF créés par cette sauvegarde. Au lieu de cela, effectuez des sauvegardes directes de ces fichiers de base de données à l’aide de SQL Server.


### <a name="transaction-log"></a>Journal des transactions  

Définissez le mode de récupération de la base de données de site sur **Complet**. Cette configuration est obligatoire pour utiliser Configuration Manager dans un groupe de disponibilité. Planifiez le monitoring et la gestion de la taille du journal des transactions de la base de données de site. Dans le mode de récupération complète, les transactions ne sont pas renforcées tant qu’une sauvegarde complète de la base de données ou du journal des transactions n’a pas été effectuée. Pour plus d’informations, voir [Sauvegarder et restaurer des bases de données SQL Server](https://docs.microsoft.com/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases).



## <a name="changes-for-site-recovery"></a>Modifications pour la récupération de site

Si au moins un nœud du groupe de disponibilité est encore fonctionnel, utilisez l’option de récupération de site **Ignorer la récupération de base de données (Utilisez cette option si la base de données de site n’a pas été affectée)** .

En cas de perte de tous les nœuds d’un groupe de disponibilité, commencez par recréer le groupe de disponibilité pour pouvoir récupérer le site. Configuration Manager ne peut ni reconstruire ni restaurer le nœud de disponibilité. Recréez le groupe, restaurez la sauvegarde et reconfigurez SQL. Ensuite, utilisez l’option de récupération de site pour **Ignorer la récupération de base de données (Utilisez cette option si la base de données de site n’a pas été affectée)** .

Pour plus d’informations, consultez [Sauvegarde et récupération](/sccm/core/servers/manage/backup-and-recovery).



## <a name="changes-for-reporting"></a>Modifications pour la création de rapports

### <a name="install-the-reporting-service-point"></a>Installer le point de Reporting Services

Le point de Reporting Services ne prend pas en charge l’utilisation du nom virtuel d’écouteur du groupe de disponibilité. Il ne gère pas non plus l’hébergement de sa base de données dans un groupe de disponibilité SQL Server Always On.  

- Par défaut, l’installation du point de Reporting Services utilise le nom virtuel spécifié en tant qu’écouteur comme **Nom du serveur de la base de données de site**. Modifiez ce paramètre pour spécifier un nom d’ordinateur et une instance de réplica dans le groupe de disponibilité.  

- Pour décharger la création de rapports et augmenter la disponibilité lorsqu’un nœud de réplica est hors ligne, vous pouvez installer d’autres points de Reporting Services sur chaque nœud de réplica. Ensuite, configurez chaque point de Reporting Services de façon à ce qu’il utilise son propre nom d’ordinateur. Lorsque vous installez un point de Reporting Services sur chaque réplica du groupe de disponibilité, la création de rapports peut toujours se connecter à un serveur de point de rapport actif.  


### <a name="switch-the-reporting-services-point-used-by-the-console"></a>Basculer le point de Reporting Services utilisé par la console

1. Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**.  

2. Développez **Reporting** et sélectionnez **Rapports**.  

3. Cliquez sur **Options de rapport**.  

4. Dans la boîte de dialogue Options de rapport, sélectionnez le point de Reporting Services à utiliser.  



## <a name="next-steps"></a>Étapes suivantes

Cet article décrit les prérequis, les limitations et les modifications apportées aux tâches courantes qui sont imposés par Configuration Manager lorsque des groupes de disponibilité sont utilisés. Pour connaître les procédures permettant d’installer et de configurer un site de façon à utiliser des groupes de disponibilité, voir [Configurer des groupes de disponibilité](/sccm/core/servers/deploy/configure/configure-aoag).
