---
title: Cluster SQL Server
titleSuffix: Configuration Manager
description: Utilisez un cluster SQL Server pour héberger la base de données du site System Center Configuration Manager. Inclut des informations sur les options prises en charge.
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f01367c76383454ded14390fc0583c874d32d60e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141736"
---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>Utiliser un cluster SQL Server pour la base de données du site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Vous pouvez utiliser un cluster SQL Server pour héberger la base de données du site System Center Configuration Manager. La base de données du site est le seul rôle de système de site pris en charge sur un cluster de serveurs.  

> [!IMPORTANT]  
>  La configuration réussie des clusters SQL Server s’appuie sur la documentation et les procédures fournies dans la bibliothèque de documentation de SQL Server.  

 Un cluster permet de prendre en charge le basculement et d’améliorer la fiabilité de la base de données de site. Toutefois, il n’offre pas d’autres avantages en matière de traitement ou d’équilibrage de la charge. En fait, une détérioration des performances peut survenir car le serveur de site doit trouver le nœud actif du cluster SQL Server avant de se connecter à la base de données de site.  

 Avant d’installer Configuration Manager, vous devez préparer le cluster SQL Server pour prendre en charge Configuration Manager. (Voir les prérequis plus loin dans cette section.)  

 Au cours de l’installation de Configuration Manager, l’enregistreur du service VSS (service de cliché instantané des volumes) est installé sur chaque nœud d’ordinateur physique du cluster Microsoft Windows Server. Cela permet de prendre en charge la tâche de maintenance **Serveur de site de sauvegarde**.  

 Après l’installation du site, Configuration Manager vérifie toutes les heures la présence de modifications apportées au nœud de cluster. Configuration Manager gère automatiquement toutes les modifications éventuellement détectées qui affectent les installations des composants Configuration Manager (comme un basculement de nœud ou l’ajout d’un nouveau nœud au cluster SQL Server).  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>Options prises en charge pour l’utilisation d’un cluster de basculement SQL Server

Les options suivantes sont prises en charge pour les clusters de basculement SQL Server utilisés comme base de données de site :

-   Cluster d’instance unique  

-   Configuration d’instances multiples  

-   Nœuds actifs multiples  

-   Instance nommée ou par défaut  

Tenez compte des prérequis suivants :  

-   La base de données du site doit être distante du serveur du site. (Le cluster ne peut pas inclure le serveur système du site.)  

-   Vous devez ajouter le compte d’ordinateur du serveur de site au groupe Administrateurs local de chaque serveur dans le cluster.  

-   Pour prendre en charge l’authentification Kerberos, le protocole de communication réseau **TCP/IP** doit être activé pour la connexion réseau de chaque nœud de cluster SQL Server. L’utilisation de**canaux nommés** n’est pas obligatoire, mais peut faciliter la résolution des problèmes d’authentification Kerberos. Les paramètres de protocole réseau sont configurés dans le **Gestionnaire de configuration SQL Server**, sous **Configuration du réseau SQL Server**.  

-   Si vous utilisez une infrastructure PKI, consultez Configuration requise des certificats PKI pour Configuration Manager, afin de connaître les conditions de certificat quand vous utilisez un cluster SQL Server pour la base de données de site.  

Tenez compte des limitations suivantes :  

-   **Installation et configuration :**  

    -   Des sites secondaires ne peuvent pas utiliser un cluster SQL Server.  

    -   Vous n’avez pas la possibilité de spécifier des emplacements de fichier autres que les emplacements par défaut pour la base de données du site quand vous utilisez un cluster SQL Server.  

-   **Fournisseur SMS :**  

    -   L’installation d’une instance du fournisseur SMS n’est pas prise en charge sur un cluster SQL Server ou sur un ordinateur utilisé comme nœud SQL Server en cluster.  

-   **Options de réplication de données :**  

    -   Si vous envisagez d’utiliser des **vues distribuées**, vous ne pouvez pas utiliser un cluster SQL Server pour héberger la base de données de site.  

-   **Sauvegarde et récupération :**  

    -   Configuration Manager ne prend pas en charge la sauvegarde DPM (Data Protection Manager) d’un cluster SQL Server qui utilise une instance nommée. Par contre, il prend en charge la sauvegarde DPM sur un cluster SQL Server qui utilise l’instance par défaut de SQL Server.  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>Préparer une instance SQL Server en cluster pour la base de données de site  

Voici les tâches principales à effectuer afin de préparer votre base de données de site :

-   Créez le cluster virtuel SQL Server pour héberger la base de données du site dans un environnement de cluster Windows Server existant. Pour connaître la procédure d’installation et de configuration d’un cluster SQL Server, consultez la documentation spécifique à votre version de SQL Server. Par exemple, si vous utilisez SQL Server 2008 R2, consultez [Installation d’un cluster de basculement SQL Server 2008 R2](http://go.microsoft.com/fwlink/p/?LinkId=240231).  

-   Sur chaque ordinateur du cluster SQL Server, vous pouvez placer un fichier dans le dossier racine de chaque lecteur sur lequel vous ne voulez pas que Configuration Manager installe les composants du site. Ce fichier doit être nommé **NO_SMS_ON_DRIVE.SMS**. Par défaut, Configuration Manager installe certains composants sur chaque nœud physique pour prendre en charge des opérations telles que la sauvegarde.  

-   Ajoutez le compte ordinateur du serveur de site au groupe **Administrateurs locaux** de chaque ordinateur du nœud de cluster Windows Server.  

-   Dans l’instance SQL Server virtuelle, attribuez le rôle SQL Server **administrateur système** au compte d’utilisateur qui exécutera le programme d’installation de Configuration Manager.  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>Pour installer un nouveau site avec un serveur SQL Server en cluster  
 Pour installer un site qui utilise une base de données de site en cluster, exécutez le programme d’installation de Configuration Manager en suivant votre processus habituel pour installer un site, mais en apportant la modification suivante :  

-   Dans la page **Informations sur la base de données** , spécifiez le nom de l’instance de cluster SQL Server virtuelle qui doit héberger la base de données du site. L’instance virtuelle remplace le nom de l’ordinateur qui exécute SQL Server.  

    > [!IMPORTANT]  
    >  Lorsque vous entrez le nom de l’instance de cluster SQL Server virtuelle, n’entrez pas le nom du serveur Windows Server virtuel créé par le cluster Windows Server. Si vous utilisez le nom du serveur Windows Server virtuel, la base de données de site est installée sur le disque dur local du nœud de cluster Windows Server actif. Cela empêche le basculement en cas d’échec de ce nœud.  
