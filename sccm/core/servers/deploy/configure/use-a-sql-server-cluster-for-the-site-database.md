---
title: Cluster SQL Server
titleSuffix: Configuration Manager
description: Utiliser un cluster SQL Server pour héberger la base de données du site Configuration Manager
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d07005c63f0d69d57d24eac163b67c34529658cf
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58477549"
---
# <a name="use-a-sql-server-cluster-for-the-site-database"></a>Utiliser un cluster SQL Server pour la base de données du site

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser un cluster de basculement SQL Server pour héberger la base de données du site Configuration Manager. Un cluster permet de prendre en charge le basculement et d’améliorer la fiabilité de la base de données de site. Toutefois, il n’offre pas d’autres avantages en matière de traitement ou d’équilibrage de la charge. En outre, un cluster de basculement SQL Server utilise un stockage partagé et introduit un point de défaillance unique. Une détérioration des performances peut survenir car le serveur de site doit trouver le nœud actif du cluster SQL Server avant de se connecter à la base de données de site.  

> [!IMPORTANT]  
> La configuration réussie des clusters SQL Server s’appuie sur la documentation et les procédures fournies dans la bibliothèque de documentation de SQL Server.  


Avant d’installer Configuration Manager, préparez le cluster SQL Server pour prendre en charge Configuration Manager. Pour plus d’informations, consultez [Préparer une instance SQL Server en cluster](#bkmk_prepare).

Au cours de l’installation de Configuration Manager, l’enregistreur du service VSS (service de cliché instantané des volumes) est installé sur chaque nœud d’ordinateur physique du cluster Microsoft Windows Server. Ce service prend en charge la tâche de maintenance **Serveur de site de sauvegarde**.  

Après l’installation du site, Configuration Manager vérifie toutes les heures la présence de modifications apportées au nœud de cluster. Configuration Manager gère automatiquement toutes les modifications trouvées qui affectent les installations de ses composants. Par exemple, un basculement de nœud ou l’ajout d’un nouveau nœud au cluster SQL Server.  



## <a name="supported-options"></a>Options prises en charge

Les options suivantes sont prises en charge pour les clusters de basculement SQL Server utilisés comme base de données de site :

- Cluster d’instance unique  

- Configuration d’instances multiples  

- Nœuds actifs multiples  

- Instance nommée ou par défaut  



## <a name="prerequisites"></a>Prérequis

Tenez compte des prérequis suivants :  

- La base de données du site doit être distante du serveur du site. Le cluster ne peut pas inclure le serveur système du site.  

    > [!Note]  
    > Depuis la version 1810, le processus d’installation de Configuration Manager ne bloque plus l’installation du rôle de serveur de site sur un ordinateur ayant le rôle Windows pour le clustering de basculement. Auparavant, vous ne pouviez pas colocaliser la base de données de site sur le serveur de site. Avec ce changement, vous pouvez créer un site à haut niveau de disponibilité avec moins de serveurs en utilisant un cluster SQL Server et un serveur de site en mode passif. Pour plus d’informations, consultez [Options de haute disponibilité](/sccm/core/servers/deploy/configure/high-availability-options). <!--3607761, fka 1359132-->  

- Ajoutez le compte d’ordinateur du serveur de site au groupe **Administrateurs** local de chaque serveur dans le cluster.  

- Pour prendre en charge l’authentification Kerberos, activez le protocole de communication réseau **TCP/IP** pour la connexion réseau de chaque nœud de cluster SQL Server. Le protocole **Canaux nommés** n’est pas obligatoire, mais peut faciliter la résolution des problèmes d’authentification Kerberos. Les paramètres de protocole réseau sont configurés dans le **Gestionnaire de configuration SQL Server**, sous **Configuration du réseau SQL Server**.  

- Si vous utilisez une infrastructure à clé publique (PKI), consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements). Il existe une configuration spécifique des certificats lorsque vous utilisez un cluster SQL Server pour la base de données de site.  



## <a name="limitations"></a>Limitations

Tenez compte des limitations suivantes :  


### <a name="installation-and-configuration"></a>Installation et configuration

- Des sites secondaires ne peuvent pas utiliser un cluster SQL Server.  

- Vous n’avez pas la possibilité de spécifier des emplacements de fichier autres que les emplacements par défaut pour la base de données du site quand vous utilisez un cluster SQL Server.  


### <a name="sms-provider"></a>Fournisseur SMS

Vous ne pouvez pas installer une instance du Fournisseur SMS sur un cluster SQL Server. Cela n’est pas non plus pris en charge sur un ordinateur qui s’exécute en tant que nœud SQL Server en cluster.  


### <a name="data-replication-options"></a>Options de réplication de données

Si vous utilisez des **vues distribuées**, vous ne pouvez pas utiliser un cluster SQL Server pour héberger la base de données de site.  


### <a name="backup-and-recovery"></a>Sauvegarde et récupération

Configuration Manager ne prend pas en charge la sauvegarde DPM (Data Protection Manager) d’un cluster SQL Server qui utilise une instance nommée. En revanche, il prend en charge la sauvegarde DPM sur un cluster SQL Server qui utilise l’instance par défaut de SQL Server.  



## <a name="bkmk_prepare"></a> Préparer une instance SQL Server en cluster  

Voici les tâches principales à effectuer afin de préparer votre base de données de site :

- Créez le cluster virtuel SQL Server pour héberger la base de données du site dans un environnement de cluster Windows Server existant. Pour connaître la procédure d’installation et de configuration d’un cluster SQL Server, consultez la documentation spécifique à votre version de SQL Server. Pour plus d’informations, consultez [Créer un cluster de basculement SQL Server](https://docs.microsoft.com/sql/sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup?view=sql-server-2017).  

- Sur chaque ordinateur du cluster SQL Server, placez un fichier dans le dossier racine de chaque lecteur sur lequel vous ne voulez pas que Configuration Manager installe les composants du site. Nommez le fichier `NO_SMS_ON_DRIVE.SMS`. Par défaut, Configuration Manager installe certains composants sur chaque nœud physique pour prendre en charge des opérations telles que la sauvegarde.  

- Ajoutez le compte ordinateur du serveur de site au groupe **Administrateurs locaux** de chaque ordinateur du nœud de cluster Windows Server.  

- Dans l’instance SQL Server virtuelle, attribuez le rôle SQL Server **administrateur système** au compte d’utilisateur qui exécute le programme d’installation de Configuration Manager.  


### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Pour installer un nouveau site avec un serveur SQL Server en cluster  

Pour installer un site qui utilise une base de données de site en cluster, exécutez le programme d’installation de Configuration Manager en suivant votre processus habituel pour installer un site, mais en apportant la modification suivante :  

- Dans la page **Informations sur la base de données** , spécifiez le nom de l’instance de cluster SQL Server virtuelle qui doit héberger la base de données du site. L’instance virtuelle remplace le nom de l’ordinateur qui exécute SQL Server.  

    > [!IMPORTANT]  
    > Lorsque vous entrez le nom de l’instance de cluster SQL Server virtuelle, n’entrez pas le nom du serveur Windows Server virtuel créé par le cluster Windows Server. Si vous utilisez le nom du serveur Windows Server virtuel, la base de données de site est installée sur le disque dur local du nœud de cluster Windows Server actif. Cela empêche le basculement en cas d’échec de ce nœud.  
