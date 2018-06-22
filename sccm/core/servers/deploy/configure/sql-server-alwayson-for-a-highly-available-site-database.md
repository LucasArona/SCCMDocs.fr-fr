---
title: SQL Server AlwaysOn
titleSuffix: Configuration Manager
description: Planifiez l’utilisation d’un groupe de disponibilité SQL Server Always On avec SCCM.
ms.date: 12/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c151ca0199a1623c85f353012e50f13d8f5b6068
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342356"
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Se préparer à l’utilisation de groupes de disponibilité SQL Server Always On avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Préparez System Center Configuration Manager afin d’utiliser des groupes de disponibilité SQL Server Always On comme solution de haute disponibilité et de récupération d’urgence pour la base de données de site.  
Configuration Manager prend en charge des groupes de disponibilité :
-     Sur les sites principaux et sur le site d’administration centrale.
-     Localement ou dans Microsoft Azure.

Quand vous utilisez des groupes de disponibilité dans Microsoft Azure, vous pouvez encore augmenter la disponibilité de la base de données de votre site en utilisant des *groupes de disponibilité Azure*. Pour plus d’informations sur les groupes à haute disponibilité Azure, consultez [Gestion de la disponibilité des machines virtuelles](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Avant de continuer, familiarisez-vous avec la configuration de SQL Server et les groupes de disponibilité SQL Server. Les informations ci-dessous font référence à la bibliothèque de documentation et aux procédures SQL Server.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Voici les scénarios pris en charge pour l’utilisation de groupes de disponibilité avec Configuration Manager. Vous trouverez les détails et les procédures pour chaque scénario à la rubrique [Configurer des groupes de disponibilité pour Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Créez un groupe de disponibilité pour une utilisation avec Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configurez un site pour utiliser un groupe de disponibilité](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Ajouter ou supprimer des membres de réplica synchrone à partir d’un groupe de disponibilité qui héberge une base de données de site](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members).
-     [Configurer des réplicas avec validation asynchrone](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (nécessite Configuration Manager version 1706 ou ultérieure).
-     [Récupérer un site à partir d’un réplica avec validation asynchrone](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (nécessite Configuration Manager version 1706 ou ultérieure).
-     [Déplacez une base de données de site d’un groupe de disponibilité vers une instance par défaut ou nommée d’un serveur SQL Server autonome](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Prérequis
Les conditions préalables suivantes s’appliquent à tous les scénarios. Si d’autres conditions préalables s’appliquent à un scénario spécifique, ces conditions seront détaillées dans ce scénario.   

### <a name="configuration-manager-accounts-and-permissions"></a>Comptes et autorisations de Configuration Manager
**Serveur de site pour l’accès à un membre réplica :**   
Le compte d’ordinateur du serveur de site doit être membre du groupe **Administrateurs locaux** sur chaque ordinateur membre du groupe de disponibilité.

### <a name="sql-server"></a>SQL Server
**Version :**  
Chaque réplica du groupe de disponibilité doit exécuter une version de SQL Server prise en charge par votre version de Configuration Manager. S’ils sont pris en charge par SQL Server, les différents nœuds d’un groupe de disponibilité peuvent exécuter des versions différentes de SQL Server.

**Édition :**  
Vous devez utiliser une édition *Enterprise* de SQL Server.

**Compte :**  
Chaque instance de SQL Server peut s’exécuter sous un compte d’utilisateur de domaine (**compte de service**) ou un compte n’appartenant pas à un domaine. Chaque réplica d’un groupe peut avoir une configuration différente. Les [meilleures pratiques SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd) recommandent d’utiliser un compte avec les autorisations les plus basses possible.

-   Pour configurer les comptes de service et les autorisations pour SQL Server 2016, consultez [Configurer les comptes de service Windows et les autorisations](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) sur MSDN.
-   Pour utiliser un compte n’appartenant pas à un domaine, vous devez utiliser des certificats. Pour plus d’informations, consultez [Utiliser des certificats pour un point de terminaison de mise en miroir de bases de données (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


Pour plus d’informations, consultez [Créer un point de terminaison de mise en miroir de base de données pour les groupes de disponibilité Always On](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Configurations du groupe de disponibilité
**Membres du réplica :**  
-   Le groupe de disponibilité doit avoir un réplica principal.
-   Avant la version 1706, vous pouviez avoir jusqu’à deux réplicas secondaires synchrones.
-   À compter de la version 1706, vous pouvez utiliser les mêmes nombre et type de réplicas dans un groupe de disponibilité pris en charge par la version de SQL Server que vous utilisez.

-   À partir de la version 1706, vous pouvez utiliser un réplica avec validation asynchrone pour récupérer votre réplica synchrone. Consultez les [options de récupération de base de données de site]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) dans la rubrique Sauvegarde et récupération pour plus d’informations sur la façon d’y parvenir.
    > [!CAUTION]  
    > Configuration Manager ne prend pas en charge le [basculement](https://go.microsoft.com/fwlink/?linkid=626885) pour utiliser le réplica avec validation asynchrone comme base de données de votre site.
Étant donné que Configuration Manager ne valide pas l’état du réplica avec validation asynchrone pour vérifier qu’il est à jour, et que, [par définition, un réplica de ce type peut être désynchronisé]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), l’utilisation d’un réplica avec validation asynchrone comme base de données de site risque de compromettre l’intégrité de votre site et de ses données.

Chaque membre du réplica doit :
-   utiliser **l’instance par défaut**;  
    *Depuis la version 1702, vous pouvez utiliser une* ***instance nommée***.

-     définir **Connexions dans le rôle principal** sur **Oui**
-     définir **Secondaire accessible en lecture** sur **Oui**  
-     être configuré pour le **basculement manuel**.      

    >  [!TIP]
    >  Configuration Manager prend en charge l’utilisation de réplicas synchrones de groupe de disponibilité quand il est configuré pour le **Basculement automatique**. Toutefois, **Basculement manuel** doit être défini lorsque :
    >  -  Vous exécutez le programme d’installation pour spécifier l’utilisation de la base de données de site dans le groupe de disponibilité.
    >  -  Lorsque vous installez une mise à jour dans Configuration Manager (pas seulement les mises à jour qui s’appliquent à la base de données de site).  

**Emplacement du membre du réplica :**  
Tous les réplicas d’un groupe de disponibilité doivent être hébergés localement ou sur Microsoft Azure. Un groupe incluant un membre local et un membre dans Azure n’est pas pris en charge.     

Lorsque vous configurez un groupe de disponibilité dans Azure et que le groupe se situe derrière un équilibreur de charge interne ou externe, les éléments suivants constituent les ports par défaut que vous devez ouvrir pour permettre au programme d’installation d’accéder à chaque réplica :   

-     Mappeur de point de terminaison RCP - **TCP 135**   
-     Server Message Block – **TCP 445**  
    *Vous pouvez supprimer ce port après le déplacement de la base de données. Depuis la version 1702, ce port n’est plus nécessaire.*
-     SQL Server Service Broker : **TCP 4022**
-     SQL sur TCP : **TCP 1433**   

Une fois l’installation terminée, les ports suivants doivent rester accessibles :
-     SQL Server Service Broker : **TCP 4022**
-     SQL sur TCP : **TCP 1433**

Depuis la version 1702, vous pouvez utiliser des ports personnalisés pour ces configurations. Les mêmes ports doivent être utilisés par le point de terminaison et sur tous les réplicas du groupe de disponibilité.


**Écouteur :**   
Le groupe de disponibilité doit avoir au moins un **écouteur de groupe de disponibilité**. Le nom virtuel de cet écouteur est utilisé quand vous configurez Configuration Manager pour utiliser la base de données du site dans le groupe de disponibilité. Bien qu’un groupe de disponibilité puisse contenir plusieurs écouteurs, Configuration Manager ne peut en utiliser qu’un seul. Consultez [Créer ou configurer un écouteur de groupe de disponibilité (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server) pour plus d’informations.

**Chemins d’accès au fichier :**   
Quand vous exécutez le programme d’installation de Configuration Manager pour configurer un site afin d’utiliser la base de données dans un groupe de disponibilité, chaque serveur réplica secondaire doit avoir un chemin de fichier SQL Server identique à celui utilisé pour les fichiers de base de données du site figurant sur le réplica principal actuel.
-   À défaut de chemin identique, le programme d’installation ne peut pas ajouter l’instance du groupe de disponibilité comme nouvel emplacement de la base de données du site.
-   En outre, le compte de service SQL Server local doit avoir une autorisation **Contrôle total** sur ce dossier.

Les serveurs de réplication secondaires doivent avoir ce chemin de fichier uniquement pendant que vous utilisez le programme d’installation pour spécifier l’instance de base de données dans le groupe de disponibilité. Une fois que le programme d’installation a configuré la base de données du site dans le groupe de disponibilité, vous pouvez supprimer le chemin inutilisé des serveurs de réplication secondaires.

Par exemple, examinez le scénario suivant :
-   Vous créez un groupe de disponibilité qui utilise trois serveurs SQL Server.

-   Votre serveur de réplication principal est une nouvelle installation de SQL Server 2014. Par défaut, les fichiers .MDF et .LDF de la base de données sont stockés dans C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA.

-   Vos deux serveurs de réplication secondaires ont été mis à niveau vers SQL Server 2014 à partir de versions antérieures et conservent le chemin de fichier d’origine pour stocker les fichiers de base de données, à savoir C:\Program Files\Microsoft SQL Server\MSSQL10.MSSQLSERVER\MSSQL\DATA.

-   Avant de tenter de déplacer la base de données du site vers ce groupe de disponibilité, sur chaque serveur de réplication secondaire, vous devez créer le prochain chemin de fichier, même si les réplicas secondaires n’utilisent pas cet emplacement de fichier, à savoir C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA (il s’agit du même chemin que celui en cours d’utilisation sur le réplica principal).

-   Vous accordez ensuite au compte de service SQL Server sur chaque réplica secondaire un accès en contrôle total à l’emplacement du fichier qui vient d’être créé sur ce serveur.

-   Vous pouvez désormais exécuter correctement le programme d’installation de Configuration Manager pour configurer le site afin qu’il utilise la base de données du site figurant dans le groupe de disponibilité.

**Configurer la base de données sur un nouveau réplica :**   
 La base de données de chaque réplica doit être définie avec les éléments suivants :
-   **Intégration du CLR** doit être *activé*
-     **Max text repl size** doit être *2147483647*
-     Le propriétaire de la base de données doit être le *compte SA*
-     **TRUSTWORTY** doit être **ON**
-     **Service Broker** doit être *activé*

Vous pouvez appliquer ces configurations uniquement à un réplica principal. Pour configurer un réplica secondaire, vous devez d’abord basculer le réplica principal vers le réplica secondaire afin de définir ce dernier comme nouveau réplica principal.   

Utilisez la documentation SQL Server lorsque cela est nécessaire pour vous aider à configurer les paramètres. Par exemple, consultez [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) ou [Intégration du CLR](/sql/relational-databases/clr-integration/clr-integration-enabling) dans la documentation SQL Server.

### <a name="verification-script"></a>Script de vérification
Vous pouvez exécuter le script suivant afin de vérifier les configurations de base de données pour les réplicas principal et secondaire. Avant de pouvoir résoudre un problème sur un réplica secondaire, vous devez le modifier afin de le définir comme réplica principal.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

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

## <a name="limitations-and-known-issues"></a>Limitations et problèmes connus
Les limitations suivantes s’appliquent à tous les scénarios.   

**Configurations et options SQL Server qui ne sont pas prises en charge :**
- **Groupes de disponibilité de base**  
  Depuis l’édition standard de SQL Server 2016, les [groupes de disponibilité de base](https://msdn.microsoft.com/library/mt614935.aspx) ne prennent pas en charge les accès en lecture aux réplicas secondaires, ce qui est obligatoire pour une utilisation avec Configuration Manager.
- **Instance de cluster de basculement**  
  Les [instances de cluster de basculement](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server) ne sont pas prises en charge pour un réplica que vous utilisez avec Configuration Manager.

- **MultiSubnetFailover**    
    L’utilisation d’un groupe de disponibilité dans une configuration à plusieurs sous-réseaux ou avec la chaîne de connexion du mot clé [MutliSubnetFailover](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server#MultiSubnetFailover) n’est pas prise en charge.



**Serveurs SQL qui hébergent des groupes de disponibilité supplémentaires :**   
Avant la version 1610 de Configuration Manager, si un groupe de disponibilité sur un serveur SQL Server héberge un ou plusieurs groupes de disponibilité en plus du groupe que vous utilisez pour Configuration Manager, chaque réplica de chacun des ces groupes de disponibilité supplémentaires doit disposer des configurations suivantes lorsque vous exécutez le programme d’installation de Configuration Manager ou installez une mise à jour pour Configuration Manager :
-   **basculement manuel**
-   **autoriser toute connexion en lecture seule**

**Utilisation d’une base de données non prise en charge :**
-   **Configuration Manager prend uniquement en charge la base de données de site dans un groupe de disponibilité :** Les éléments suivants ne sont pas pris en charge :
    -   Base de données Rapports
    -   Base de données WSUS
-   **Base de données préexistante :** vous ne pouvez pas utiliser la nouvelle base de données créée sur le réplica. Au lieu de cela, vous devez restaurer une copie de base de données Configuration Manager existante vers le réplica principal lors de la configuration d’un groupe de disponibilité.

**Erreurs d’installation dans le fichier ConfigMgrSetup.log :**  
Lorsque vous exécutez le programme d’installation pour déplacer une base de données de site vers un groupe de disponibilité, le programme d’installation tente de traiter les rôles de la base de données sur les réplicas secondaires du groupe de disponibilité et consigne les erreurs comme suit :
-   ERREUR : erreur SQL Server : [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Échec de la mise à jour de la base de données « CM_AAA », car celle-ci est en lecture seule. Installation de Configuration Manager 21/1/2016 16:54:59 7344 (0x1CB0)  

Ces erreurs peuvent être ignorées sans problème.

## <a name="changes-for-site-backup"></a>Modifications pour la sauvegarde de site
**Sauvegarder des fichiers de base de données :**  
Quand une base de données du site s’exécute dans un groupe de disponibilité, vous devez exécuter la tâche intégrée de maintenance de serveur **Sauvegarder le site** pour sauvegarder les paramètres et fichiers Configuration Manager courants. Toutefois, évitez d’utiliser les fichiers .MDF ou .LDF créés par cette sauvegarde. Au lieu de cela, effectuez des sauvegardes directes de ces fichiers de base de données à l’aide de SQL Server.

**Journal de transactions :**  
Le mode de récupération de la base de données de site doit être défini sur **Complète** (condition requise pour une utilisation dans un groupe de disponibilité). Avec cette configuration, planifiez le monitorage et la gestion de la taille du journal de transactions de la base de données de site. Dans le mode de récupération complète, les transactions ne sont pas renforcées tant qu’une sauvegarde complète de la base de données ou du journal des transactions n’a pas été effectuée. Consultez [Sauvegarde et restauration des bases de données SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) pour plus d’informations.

## <a name="changes-for-site-recovery"></a>Modifications pour la récupération de site
Vous pouvez utiliser l’option de récupération de site **Ignorer la récupération de base de données (Utiliser cette option si la base de données de site n’était pas affectée)** si au moins un nœud du groupe de disponibilité reste fonctionnel.

 Avant de pouvoir récupérer le site si tous les nœuds d’un groupe de disponibilité ont été perdus, vous devez recréer le groupe de disponibilité. Configuration Manager ne peut pas reconstruire ni restaurer le nœud de disponibilité. Une fois le groupe recréé et une sauvegarde restaurée et reconfigurée, vous pouvez utiliser l’option de récupération de site  **Ignorer la récupération de base de données (Utiliser cette option si la base de données de site n’était pas affectée)**.

Pour plus d’informations, consultez [Sauvegarde et récupération pour System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Modifications pour la création de rapports
**Installez le point de Reporting Services :**  
Le point de Reporting Services ne prend pas en charge l’utilisation du nom virtuel d’écouteur du groupe de disponibilité ni l’hébergement de la base de données Reporting services dans un groupe de disponibilité SQL Server Always On :
-   Par défaut, l’installation du point de Reporting Services utilise le nom virtuel spécifié en tant qu’écouteur comme **nom du serveur de base de données de site** . Modifiez cette option pour spécifier un nom d’ordinateur et une instance d’un réplica dans le groupe de disponibilité.
-   Pour décharger la création de rapports et augmenter la disponibilité lorsqu’un nœud de réplica est en mode hors ligne, vous pouvez installer d’autres points de Reporting Services sur chaque nœud de réplica et configurer chaque point de Reporting Services afin qu’il pointe vers son propre nom d’ordinateur.

Lorsque vous installez un point de Reporting Services sur chaque réplica du groupe de disponibilité, la création de rapports peut toujours se connecter à un serveur de point de rapport actif.

**Basculer le point de Reporting Services utilisé par la console :**  
Pour exécuter des rapports, dans la console, accédez à **Surveillance** > **Vue d’ensemble** > **reporting** > **Rapports**, puis choisissez **Options de rapport**. Dans la boîte de dialogue Options de rapport, sélectionnez le point de Reporting Services souhaité.

## <a name="next-steps"></a>Étapes suivantes
Après avoir assimilé les conditions préalables, les limitations et les modifications apportées aux tâches requises lorsque vous utilisez des groupes de disponibilité, consultez [Configurer des groupes de disponibilité pour Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag) afin de connaître les procédures d’installation et de configuration de votre site pour utiliser des groupes de disponibilité.
