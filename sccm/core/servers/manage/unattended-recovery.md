---
title: Récupération sans assistance
titleSuffix: Configuration Manager
description: Utilisez un script pour récupérer vos sites dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 637727356724085f019ac9ab336bc37e3635ea3a
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415141"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Récupération de site sans assistance pour Configuration Manager   

*S’applique à : System Center Configuration Manager (Current Branch)*

 Pour effectuer une [récupération en mode sans assistance](/sccm/protect/understand/recover-sites#site-recovery-procedures) d’un site d’administration centrale Configuration Manager ou d’un site principal, vous pouvez créer un script d’installation sans assistance puis utiliser le programme d’installation avec l’option de commande **/script**. Le script fournit le même type d’informations que les invites de l’Assistant Installation ; la seule différence est qu’il n'existe pas de paramètres par défaut. Toutes les valeurs doivent être indiquées pour les clés d'installation qui s'appliquent au type de récupération choisi.

 Pour utiliser l’option de ligne de commande /script du programme d’installation, vous devez créer un fichier d’initialisation. Puis spécifiez ce nom de fichier après l’option /script. Le nom du fichier n'a pas importance tant qu'il est suivi de l'extension de fichier **.ini**. Lorsque vous référencez le fichier d'initialisation d'installation à partir de la ligne de commande, vous devez fournir le chemin d'accès complet au fichier. Par exemple, si votre fichier d'initialisation d'installation s'appelle *setup.ini* et qu'il est stocké dans le *dossier C:\setup*, votre ligne de commande serait :

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Vous devez disposer de droits d’administrateur pour exécuter le programme d'installation. Lorsque vous exécutez le programme d’installation avec le script sans assistance, démarrez l’invite de commandes dans un contexte d’administrateur en utilisant **Exécuter en tant qu’administrateur**.

 Le script contient les noms de section, les noms de clé et les valeurs. Les noms des clés de section requis varient en fonction du type de récupération faisant l'objet du script. L’ordre des clés dans les sections et l’ordre des sections dans le fichier n’ont pas d’importance. Les clés ne tiennent pas compte de la casse. Lorsque vous attribuez des valeurs aux clés, le nom de la clé doit être suivi du signe égal (=) et de la valeur de la clé.

 Utilisez les sections suivantes pour créer votre script de récupération de site en mode sans assistance. Les tableaux répertorient les clés de script d'installation disponibles ainsi que leurs valeurs correspondantes, indiquent si elles sont obligatoires ou non, le type d'installation pour lequel elles sont utilisées, ainsi qu'une brève description de la clé.

## <a name="recover-a-central-administration-site-unattended"></a>Récupérer un site d’administration centrale sans assistance
 Utilisez les informations suivantes pour configurer un fichier de script d’installation sans assistance afin de récupérer un site d’administration centrale.

 **Identification**

-   **Nom de clé :** Action

    -   **Obligatoire :** Oui
    -   **Valeurs :** RecoverCCAR
    -   **Détails :** Récupère un site d'administration centrale


-   **Nom de clé :** CDLatest

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest folder.
    -   **Valeurs :** 1. Toute autre valeur que 1 est considérée comme signifiant que CD.Latest.
    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**RecoveryOptions**   
-   **Nom de clé :** ServerRecoveryOptions   

    -   **Obligatoire :** Oui
    -   **Valeurs :** 1, 2 ou 4  
         1 = Serveur de site de récupération et SQL Server.   
         2 = Récupérer le serveur de site uniquement.  
         4 = Récupérer SQL Server uniquement.
    -   **Détails :** Spécifie si le programme d’installation récupère le serveur de site, SQL Server, ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :  
        -   **Valeur = 1** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

             la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

        -   **Valeur = 2** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

        -   **Valeur = 4** la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

-   **Nom de clé :** DatabaseRecoveryOptions

    -   **Obligatoire :** Peut-être
    -   **Valeurs :**   
         - **10** = Restaurer la base de données du site à partir d'une sauvegarde.  
         - **20** = Utiliser une base de données de site qui a été récupérée manuellement avec une autre méthode.   
         - **40** = Créer une nouvelle base de données pour le site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  
         - **80** = Ignorer la récupération de base de données.
    -   **Détails :** Spécifie comment le programme d’installation récupère la base de données de site dans SQL Server. Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.


-   **Nom de clé :** ReferenceSite  

    -   **Obligatoire :** Peut-être
    -   **Valeurs :** &lt;ReferenceSiteFQDN\>
    -   **Détails :** Spécifie le site principal de référence. Si la sauvegarde de base de données est antérieure à la période de rétention du suivi des modifications ou si vous récupérez le site sans sauvegarde, le site d’administration centrale utilise le site de référence pour récupérer les données globales.

         Quand vous ne spécifiez pas de site de référence et que la sauvegarde est antérieure à la période de rétention du suivi des modifications, tous les sites principaux sont réinitialisés avec les données restaurées à partir du site d’administration centrale.

         Lorsque vous ne spécifiez pas de site de référence, et que la sauvegarde est comprise dans la période de rétention du suivi des modifications, seules les modifications apportées depuis la dernière sauvegarde sont répliquées à partir des sites principaux. Lorsqu'il existe des conflits entre des modifications issues de différents sites principaux, le site d'administration centrale utilise la première modification reçue.

         Cette clé est requise lorsque le paramètre **DatabaseRecoveryOptions** a la valeur **40**.

-   **Nom de clé :** SiteServerBackupLocation

    -   **Obligatoire :** Non
    -   **Valeurs :** &lt;PathToSiteServerBackupSet\>
    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde du serveur de site. Cette clé est facultative si le paramètre **ServerRecoveryOptions** a la valeur **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.


-   **Nom de clé :** BackupLocation

    -   **Obligatoire :** Peut-être
    -   **Valeurs :** &lt;PathToSiteDatabaseBackupSet\>
    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde de la base de données du site. La clé **BackupLocation** est requise lorsque vous configurez une valeur de **1** ou **4** pour la clé **ServerRecoveryOptions** , et une valeur de **10** pour la clé **DatabaseRecoveryOptions** .


**Options**

- **Nom de clé :** ProductID
  -   **Obligatoire :** Oui
  -   **Valeurs :**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Détails :** Clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  


- **Nom de clé :** SiteCode

  -   **Obligatoire :** Oui
  -   **Valeurs :** &lt;Code de site\>
  -   **Détails :** Trois caractères alphanumériques qui identifient le site de façon univoque dans votre hiérarchie. Spécifiez le code de site utilisé par le site avant la défaillance.


- **Nom de clé :** SiteName

  -   **Obligatoire :** Oui
  -   **Valeurs :** SiteName
  -   **Détails :** Description du site.


- **Nom de clé :** SMSInstallDir

  - **Obligatoire :** Oui
  - **Valeurs :** &lt;*ConfigMgrInstallationPath*>
  - **Détails :** Spécifie le dossier d’installation des fichiers programmes de Configuration Manager.
    > [!NOTE]   
    >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager.

- **Nom de clé :** SDKServer

  -   **Obligatoire :** Oui
  -   **Valeurs :** &lt;*Nom de domaine complet du fournisseur SMS*>
  -   **Détails :** Spécifie le nom de domaine complet du serveur qui héberge le fournisseur SMS. Spécifiez le serveur qui hébergeait le fournisseur SMS avant la défaillance.

       Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.

- **Nom de clé :** PrerequisiteComp

  -   **Obligatoire :** Oui
  -   **Valeurs :** 0 ou 1  
       0 = téléchargement   
       1 = déjà téléchargé
  -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d’installation télécharge les fichiers.  


- **Nom de clé :** PrerequisitePath

  -   **Obligatoire :** Oui
  -   **Valeurs :** &lt;*PathToSetupPrerequisiteFiles*>
  -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.

- **Nom de clé :** AdminConsole

  -   **Obligatoire :** Peut-être
  -   **Valeurs :** 0 ou 1 0 = ne pas installer   
       1 = installer
  -   **Détails :** Spécifie si la console Configuration Manager doit ou non être installée. Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.


- **Nom de clé :** JoinCEIP   
  > [!Note]  
  > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

  -   **Obligatoire :** Oui
  -   **Valeurs :** 0 ou 1  
       0 = ne pas joindre  
       1 = joindre
  -   **Détails :** Spécifie si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur.

**SQLConfigOptions**

-   **Nom de clé :** SQLServerName 

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;SQLServerName\>*
    -   **Détails :** Nom du serveur ou nom de l’instance en cluster exécutant SQL Server qui héberge la base de données de site. Spécifiez le serveur qui a hébergé la base de données de site avant la défaillance.


-   **Nom de clé :** DatabaseName

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Détails :** Nom de la base de données SQL Server à créer ou utiliser pour installer la base de données du site d'administration centrale. Spécifiez le nom de base de données qui était utilisé avant la défaillance.

        > [!IMPORTANT]  
        >  Si vous n’utilisez pas l’instance par défaut, vous devez spécifier le nom d’instance et le nom de base de données de site.

-   **Nom de clé :** SQLSSBPort

    -   **Obligatoire :** Non
    -   **Valeurs :** &lt;*SSBPortNumber*>
    -   **Détails :** Spécifiez le port SQL Server Service Broker (SSB) utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge. Spécifiez le port SSB utilisé avant la défaillance.

## <a name="recover-a-primary-site-unattended"></a>Récupérer un site principal en mode sans assistance
 Utilisez les informations suivantes pour configurer un fichier de script d’installation sans assistance afin de récupérer un site d’administration centrale.

 **Identification**

-   **Nom de clé :** Action

    -   **Obligatoire :** Oui
    -   **Valeurs :** RecoverPrimarySite
    -   **Détails :** Récupère un site principal


-   **Nom de clé :** CDLatest

    -   **Obligatoire :** Oui, uniquement en cas d’utilisation de médias du dossier CD.Latest folder.
    -   **Valeurs :** 1. Toute autre valeur que 1 est considérée comme signifiant que CD.Latest.
    -   **Détails :** Le script doit inclure cette clé et cette valeur en cas d’exécution de l’installation à partir de médias du dossier CD.Latest dans le cadre de l’installation d’un site principal ou d’administration centrale, ou de la récupération d’un site principal ou d’administration centrale. Cette valeur indique au programme d’installation que des médias de CD.Latest sont utilisés.

**RecoveryOptions**

-   **Nom de clé :** ServerRecoveryOptions

    -   **Obligatoire :** Oui
    -   **Valeurs :** 1, 2 ou 4    
         1 = Serveur de site de récupération et SQL Server.   
         2 = Récupérer le serveur de site uniquement.  
         4 = Récupérer SQL Server uniquement.
    -   **Détails :** Spécifie si le programme d’installation récupère le serveur de site, SQL Server, ou les deux. Les clés associées sont requises lorsque vous définissez la valeur suivante pour le paramètre ServerRecoveryOptions :

        -   **Valeur = 1** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

             la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

        -   **Valeur = 2** : vous avez la possibilité de spécifier une valeur pour la clé **SiteServerBackupLocation** afin de récupérer le site en utilisant une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.

        -   **Valeur = 4** la clé **BackupLocation** est requise lorsque vous configurez la valeur **10** pour la clé **DatabaseRecoveryOptions** , qui consiste à restaurer la base de données de site à partir de la sauvegarde.

-   **Nom de clé :** DatabaseRecoveryOptions

    -   **Obligatoire :** Peut-être
    -   **Valeurs :**   
         - **10** = Restaurer la base de données du site à partir d'une sauvegarde.  
         - **20** = Utiliser une base de données de site qui a été récupérée manuellement avec une autre méthode.     
         - **40** = Créer une nouvelle base de données pour le site. Utilisez cette option lorsqu'aucune sauvegarde de base de données de site n'est disponible. Les données globales et de site sont récupérées via la réplication à partir d'autres sites.  
         - **80** = Ignorer la récupération de base de données.
    -   **Détails :** Spécifie comment le programme d’installation récupère la base de données de site dans SQL Server. Cette clé est requise lorsque la valeur du paramètre **ServerRecoveryOptions** est **1** ou **4**.


-   **Nom de clé :** SiteServerBackupLocation

    -   **Obligatoire :** Non
    -   **Valeurs :** &lt;PathToSiteServerBackupSet\>
    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde du serveur de site. Cette clé est facultative si le paramètre **ServerRecoveryOptions** a la valeur **1** ou **2**. Spécifiez une valeur pour la clé **SiteServerBackupLocation** pour récupérer le site à l'aide d'une sauvegarde de site. Si vous ne spécifiez pas de valeur, le site est réinstallé sans être restauré à partir d'un jeu de sauvegarde.     


-   **Nom de clé :** BackupLocation

    -   **Obligatoire :** Peut-être
    -   **Valeurs :** &lt;PathToSiteDatabaseBackupSet\>
    -   **Détails :** Spécifie le chemin d'accès au jeu de sauvegarde de la base de données du site. La clé **BackupLocation** est requise lorsque vous configurez une valeur de **1** ou **4** pour la clé **ServerRecoveryOptions** , et une valeur de **10** pour la clé **DatabaseRecoveryOptions** .

**Options**

-   **Nom de clé :** ProductID

    -   **Obligatoire :** Oui
    -   **Valeurs :**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Détails :** Clé de produit de l’installation de Configuration Manager avec les tirets. Entrez **Eval** pour installer la version d’évaluation de Configuration Manager.  


-   **Nom de clé :** SiteCode

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;Code de site\>
    -   **Détails :** Trois caractères alphanumériques qui identifient le site de façon univoque dans votre hiérarchie. Spécifiez le code de site utilisé par le site avant la défaillance.


-   **Nom de clé :** SiteName

    -   **Obligatoire :** Oui
    -   **Valeurs :** SiteName
    -   **Détails :** Description du site.


-   **Nom de clé :** SMSInstallDir

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*ConfigMgrInstallationPath*>
    -   **Détails :** Spécifie le dossier d’installation des fichiers programmes de Configuration Manager.

        > [!NOTE]   
        >  Vous pouvez spécifier le chemin d’origine ou un nouveau chemin à utiliser pour l’installation de Configuration Manager.

-   **Nom de clé :** SDKServer

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*Nom de domaine complet du fournisseur SMS*>
    -   **Détails :** Spécifie le nom de domaine complet du serveur qui héberge le fournisseur SMS. Spécifiez le serveur qui hébergeait le fournisseur SMS avant la défaillance.

         Vous pouvez configurer d'autres fournisseurs SMS pour le site après l'installation initiale.

-   **Nom de clé :** PrerequisiteComp

    -   **Obligatoire :** Oui
    -   **Valeurs :** 0 ou 1    
         0 = téléchargement   
         1 = déjà téléchargé   
    -   **Détails :** Spécifie si les fichiers d’installation requis ont déjà été téléchargés. Par exemple, si vous utilisez la valeur 0, le programme d’installation télécharge les fichiers.


-   **Nom de clé :** PrerequisitePath

    -   **Obligatoire :** Oui
    -   **Valeurs :** &lt;*PathToSetupPrerequisiteFiles*>
    -   **Détails :** Spécifie le chemin d’accès aux fichiers d’installation requis. Selon la valeur **PrerequisiteComp** , le programme d’installation utilise ce chemin pour stocker les fichiers téléchargés ou localiser des fichiers déjà téléchargés.


-   **Nom de clé :** AdminConsole

    -   **Obligatoire :** Peut-être
    -   **Valeurs :** 0 ou 1  
         0 = ne pas installer   
         1 = installer  
    -   **Détails :** Spécifie si la console Configuration Manager doit ou non être installée. Cette clé est obligatoire sauf quand le paramètre **ServerRecoveryOptions** a la valeur **4**.

-   **Nom de clé :** JoinCEIP  
    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

    -   **Obligatoire :** Oui
    -   **Valeurs :** 0 ou 1    
         0 = ne pas joindre  
         1 = joindre
    -   **Détails :** Spécifie si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur.


**SQLConfigOptions**

-   **Nom de clé :** SQLServerName 

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;SQLServerName\>*
    -   **Détails :** Nom du serveur ou nom de l’instance en cluster exécutant SQL Server qui héberge la base de données de site. Spécifiez le serveur qui a hébergé la base de données de site avant la défaillance.


-   **Nom de clé :** DatabaseName

    -   **Obligatoire :** Oui
    -   **Valeurs :** *&lt;SiteDatabaseName\>* ou *&lt;InstanceName\>*\\*&lt;SiteDatabaseName\>*
    -   **Détails :** Nom de la base de données SQL Server à créer ou utiliser pour installer la base de données du site d'administration centrale. Spécifiez le nom de base de données qui était utilisé avant la défaillance.

        > [!IMPORTANT]    
        >  Si vous n’utilisez pas l’instance par défaut, vous devez spécifier le nom d’instance et le nom de base de données de site.

-   **Nom de clé :** SQLSSBPort

    -   **Obligatoire :** Non
    -   **Valeurs :** &lt;*SSBPortNumber*>
    -   **Détails :** Spécifiez le port SQL Server Service Broker (SSB) utilisé par SQL Server. Généralement, SSB est configuré pour utiliser le port TCP 4022, mais d'autres ports sont pris en charge. Spécifiez le port SSB utilisé avant la défaillance.

**Option d’extension de hiérarchie**

-   **Nom de clé :** CCARSiteServer

    -   **Obligatoire :** Peut-être
    -   **Valeurs :** &lt;*SiteCodeForCentralAdministrationSite*>
    -   **Détails :** Spécifie le site d’administration centrale auquel un site principal s’attache quand il rejoint la hiérarchie Configuration Manager. Ce paramètre est requis si le site principal était attaché à un site d'administration centrale avant la défaillance. Spécifiez le code de site qui était utilisé pour le site d’administration centrale avant la défaillance.

-   **Nom de clé :** CASRetryInterval

    -   **Obligatoire :** Non
    -   **Valeurs :** &lt;*Intervalle*>
    -   **Détails :** Spécifie l'intervalle (en minutes) avant une nouvelle tentative de connexion au site d'administration centrale après un échec de connexion. Par exemple, en cas d’échec de la connexion au site d’administration centrale, le site principal attend le nombre de minutes que vous avez spécifié pour CASRetryInterval et réessaie d’établir une connexion.


-   **Nom de clé :** WaitForCASTimeout

    -   **Obligatoire :** Non
    -   **Valeurs :** &lt;*Délai d’expiration*>
    -   **Détails :** Spécifie la valeur de délai d'attente maximal (en minutes) pour qu'un site principal se connecte au site d'administration centrale. Par exemple, si un site principal ne parvient pas à se connecter à un site d'administration centrale, le site principal essaie de nouveau d'établir une connexion selon la valeur de CASRetryInterval jusqu'à ce que le délai WaitForCASTimeout soit atteint. Vous pouvez spécifier une valeur de 0 à 100.
