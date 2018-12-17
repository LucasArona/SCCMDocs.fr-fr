---
title: Entrepôt de données
titleSuffix: Configuration Manager
description: Base de données et point de service de l’entrepôt de données pour Configuration Manager
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7671025b0a643063f30c98922f7da0659e2e1ab9
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456904"
---
#  <a name="the-data-warehouse-service-point-for-configuration-manager"></a>Point de service de l’entrepôt de données pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1277922--> Utilisez le point de service de l’entrepôt de données pour stocker des données d’historique à long terme et créer des rapports sur celles-ci pour votre déploiement de Configuration Manager.

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


L’entrepôt de données prend en charge jusqu’à 2 To de données, avec des horodatages pour le suivi des modifications. L’entrepôt de données stocke des données en synchronisant automatiquement les données de la base de données du site Configuration Manager avec celles de la base de données de l’entrepôt de données. Ces informations seront ensuite accessibles à partir de votre point de rapport. Les données qui sont synchronisées avec la base de données de l’entrepôt de données sont conservées pendant trois ans. Régulièrement, une tâche intégrée supprime les données datant de plus de trois ans.

Les données synchronisées incluent les éléments suivants, qui proviennent des groupes des données de site et des données globales :
- Intégrité de l’infrastructure
- Sécurité
- Compatibilité
- Programme malveillant   
- Déploiements de logiciels
- Détails d’inventaire (toutefois, l’historique d’inventaire n’est pas synchronisé)

Une fois installé, le rôle de système de site installe et configure la base de données de l’entrepôt de données. Il installe également plusieurs rapports, afin que vous puissiez facilement rechercher ces données et créer des rapports les concernant.

Avec la version 1810, vous pouvez synchroniser davantage de tables entre la base de données de site et l’entrepôt de données. Ce changement vous permet de créer davantage de rapports pour répondre aux besoins de votre entreprise.<!--1358870--> 



## <a name="prerequisites"></a>Prérequis

- Le rôle de système de site d’entrepôt de données est pris en charge uniquement sur le site de niveau supérieur de la hiérarchie. Par exemple, un site d’administration centrale ou un site principal autonome.  

- L’ordinateur sur lequel vous installez le rôle de système de site nécessite .NET Framework 4.5.2 ou version ultérieure.  

- Accordez au **compte du point de Reporting Services** l’autorisation d’accès **db_datareader** à la base de données de l’entrepôt de données.  

- Pour synchroniser des données avec la base de données de l’entrepôt de données, Configuration Manager utilise le compte d’ordinateur du rôle de système de site. Ce compte nécessite les autorisations suivantes :  

    - des autorisations de niveau **Administrateur** sur l’ordinateur qui héberge la base de données de l’entrepôt de données ;  

    - une autorisation **DB_Creator** sur la base de données de l’entrepôt de données ;  

    - **DB_owner** ou **DB_reader** avec une autorisation **execute** sur la base de données du site de niveau supérieur.  

- La base de données de l’entrepôt de données nécessite l’utilisation de SQL Server 2012 ou version ultérieure. L’édition peut être Standard, Entreprise ou Datacenter. Il n’est pas nécessaire que la version SQL Server de l’entrepôt de données soit la même que celle du serveur de base de données du site.<!--SCCMDocs issue 662-->  

- La base de données de l’entrepôt prend en charge les configurations SQL Server suivantes :  

    - Instance par défaut ou nommée  

    - Groupe de disponibilité SQL Server AlwaysOn  

    - Cluster de basculement SQL Server  

- Si vous utilisez des [vues distribuées](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), le point de service de l’entrepôt de données doit être installé sur le serveur qui héberge la base de données du site d’administration centrale.  

Pour plus d’informations sur la gestion des licences SQL Server, consultez les [Questions fréquentes (FAQ) sur les produits et la gestion des licences](/sccm/core/understand/product-and-licensing-faq). <!-- sms500967 -->

Attribuez la même taille à la base de données de l’entrepôt de données qu’à votre base de données de site. Même si dans un premier temps la taille de l’entrepôt de données est petite, celle-ci augmentera au fil du temps. <!--SCCMDocs issue 756-->



## <a name="install"></a>Installez

Chaque hiérarchie prend en charge une seule instance de ce rôle, sur n’importe quel système de site du site de niveau supérieur. L’instance SQL Server qui héberge la base de données de l’entrepôt peut être locale ou distante par rapport au rôle de système de site. L’entrepôt de données fonctionne avec le point de Reporting Services installé sur le même site. Il n’est pas obligatoire d’installer les deux rôles de système de site sur le même serveur.   

Pour installer le rôle, vous pouvez utiliser deux assistants : **l’Assistant Ajout des rôles de système de site** ou **l’Assistant Création d’un serveur de système de site**. Pour plus d’informations, consultez la section [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Dans la page **Sélection du rôle système** de l’Assistant, sélectionnez **Point de service de l’entrepôt de données**. 

Quand vous installez le rôle, Configuration Manager crée la base de données de l’entrepôt de données pour vous sur l’instance de SQL Server que vous spécifiez. Si vous spécifiez le nom de la base de données existante, Configuration Manager ne crée pas de base de données. Il utilise celle que vous spécifiez. Ce processus est le même que lorsque vous [déplacez la base de données de l’entrepôt de données vers un nouveau serveur SQL](#move-the-data-warehouse-database).


### <a name="configure-properties"></a>Configurer les propriétés

#### <a name="general-page"></a>Page Général

- **Nom de domaine complet SQL Server** : spécifiez le nom de domaine complet (FQDN) du serveur qui héberge la base de données du point de service de l’entrepôt de données.  

- **Nom de l’instance de SQL Server, le cas échéant** : si vous n’utilisez pas l’instance par défaut de SQL Server, spécifiez l’instance nommée.  

- **Nom de la base de données** : spécifiez le nom de la base de données de l’entrepôt de données. Configuration Manager crée la base de données de l’entrepôt de données en lui donnant ce nom. Si vous spécifiez un nom de base de données qui existe déjà sur l’instance de SQL Server, Configuration Manager utilise cette base de données.  

- **Port SQL Server utilisé pour la connexion** : spécifiez le numéro de port TCP/IP utilisé par l’instance de SQL Server qui héberge la base de données de l’entrepôt de données. Le service de synchronisation de l’entrepôt de données utilise ce port pour se connecter à la base de données de l’entrepôt de données. Par défaut, il utilise le port SQL Server **1433** pour la communication.  

- **Compte de point de service de l’entrepôt de données** : à compter de la version 1802, définissez le **nom d’utilisateur** que SQL Server Reporting Services doit utiliser lors de la connexion à la base de données de l’entrepôt de données.  


#### <a name="synchronization-schedule-page"></a>Page Calendrier des synchronisations
*S’applique à la version 1806 et aux versions antérieures*

- **Heure de début** : indiquez l’heure de début de la synchronisation de l’entrepôt de données.  

- **Périodicité**

    - **Tous les jours** : permet d’indiquer que la synchronisation doit s’exécuter chaque jour.  

    - **Hebdomadaire** : permet de spécifier une seule journée chaque semaine ainsi qu’une périodicité hebdomadaire pour la synchronisation.


#### <a name="synchronization-settings-page"></a>Page Paramètres de synchronisation
*S’applique à la version 1810 et aux versions ultérieures*

- **Paramètre personnalisé de synchronisation de données** : choisissez l’option **Sélectionner des tables**. Dans la fenêtre Tables de base de données, sélectionnez les noms des tables à synchroniser avec la base de données de l’entrepôt de données. Utilisez le filtre pour effectuer une recherche par nom ou sélectionnez la liste déroulante pour choisir des groupes spécifiques. Lorsque vous avez terminé, sélectionnez **OK** pour enregistrer.  

    > [!Note]  
    > Vous ne pouvez pas supprimer les tables sélectionnées par défaut par le rôle.  

- **Heure de début** : indiquez l’heure de début de la synchronisation de l’entrepôt de données.  

- **Périodicité**

    - **Tous les jours** : permet d’indiquer que la synchronisation doit s’exécuter chaque jour.  

    - **Hebdomadaire** : permet de spécifier une seule journée chaque semaine ainsi qu’une périodicité hebdomadaire pour la synchronisation.



## <a name="reporting"></a>Rapports

Une fois que vous aurez installé un point de service de l’entrepôt de données, plusieurs rapports seront accessibles sur le point de Reporting Services du site. Si vous installez le point de service de l’entrepôt de données avant d’installer un point de Reporting Services, les rapports seront automatiquement ajoutés lors de l’installation du point de Reporting Services.

> [!WARNING]  
> À compter de la version 1802, le point de l’entrepôt de données prend en charge les informations d’identification alternatives.<!--507334--> Si vous avez effectué une mise à niveau à partir d’une version précédente de Configuration Manager, vous devez spécifier les informations d’identification que SQL Server Reporting Services doit utiliser pour se connecter à la base de données de l’entrepôt de données. Les rapports de l’entrepôt de données ne s’ouvrent pas tant que vous n’avez pas entré les informations d’identification. 
> 
> Pour spécifier un compte, définissez le **nom d’utilisateur** pour le compte du point de service d’entrepôt de données dans les propriétés du rôle. Pour plus d’informations, consultez [Configurer les propriétés](#configure-properties). 

Le rôle de système de site de l’entrepôt de données comprend les rapports suivants, qui appartiennent à la catégorie **Entrepôt de données** :  

- **Déploiement de l’application – Historique** : détails du déploiement d’une application donnée pour une machine en particulier.  

- **Endpoint Protection et Compatibilité des mises à jour logicielles - Historique** : affiche les ordinateurs sur lesquels des mises à jour logicielles n’ont pas été effectuées.  

- **Inventaire matériel général – Historique** : tout l’inventaire matériel d’une machine en particulier.  

- **Inventaire logiciel général – Historique** : tout l’inventaire logiciel d’une machine en particulier.  

- **Vue d’ensemble de l’intégrité de l’infrastructure – Historique** : vue d’ensemble de l’intégrité de l’infrastructure Configuration Manager.  

- **Liste des programmes malveillants détectés – Historique** : programmes malveillants détectés dans l’organisation.  

- **Synthèse de la distribution de logiciels – Historique** : synthèse de la distribution de logiciels pour une publication et une machine en particulier.  



## <a name="site-expansion"></a>Expansion de site

Avant d’installer un site d’administration centrale pour étendre un site principal autonome existant, désinstallez le rôle de point de service de l’entrepôt de données. Après avoir installé le site d’administration centrale, vous pouvez installer le rôle de système de site sur ce site.  

Contrairement au déplacement de la base de données de l’entrepôt de données, cette modification entraîne une perte des données historiques que vous avez synchronisées sur le site principal. La sauvegarde de la base de données à partir du site principal et sa restauration sur le site d’administration centrale ne sont pas prises en charge.



## <a name="move-the-database"></a>Déplacer la base de données

Procédez comme suit pour déplacer la base de données de l’entrepôt de données vers un nouveau serveur SQL Server :  

1. Utilisez SQL Server Management Studio pour sauvegarder la base de données de l’entrepôt de données. Ensuite, restaurez cette base de données sur un serveur SQL Server sur le nouvel ordinateur qui héberge l’entrepôt de données.  

    > [!NOTE]  
    > Après avoir restauré la base de données sur le nouveau serveur, vérifiez que les autorisations d’accès à la base de données sont les mêmes sur la nouvelle base de données de l’entrepôt de données que sur la base de données de l’entrepôt de données d’origine.  

2. Utilisez la console Configuration Manager pour supprimer du serveur actuel le rôle de point de service de l’entrepôt de données.  

3. Réinstallez le point de service de l’entrepôt de données. Spécifiez le nom du nouveau serveur SQL Server et de l’instance qui hébergera la base de données de l’entrepôt de données que vous avez restaurée.  

4. Une fois le rôle de système de site installé, le déplacement est terminé.  



## <a name="troubleshooting"></a>Résolution des problèmes 

### <a name="log-files"></a>Fichiers journaux 

Utilisez les journaux suivants pour examiner les problèmes d’installation du point de service de l’entrepôt de données ou de synchronisation des données :

- **DWSSMSI.log** et **DWSSSetup.log** : utilisez ces journaux pour examiner les erreurs survenues lors de l’installation du point de service de l’entrepôt de données.  

- **Microsoft.ConfigMgrDataWarehouse.log** : utilisez ce journal pour examiner la synchronisation des données entre la base de données de site et la base de données de l’entrepôt de données.  


### <a name="set-up-failure"></a>Échec d’installation 

Lorsque le rôle de point de service d’entrepôt de données est le premier que vous installez sur un serveur distant, l’installation échoue pour l’entrepôt de données.  

#### <a name="workaround"></a>Solution de contournement 
Vérifiez que l’ordinateur sur lequel vous installez le point de service de l’entrepôt de données héberge au moins un autre rôle.  


### <a name="synchronization-failed-to-populate-schema-objects"></a>La synchronisation n’a pas pu ajouter les objets de schéma 

La synchronisation échoue et génère le message suivant dans le fichier **Microsoft.ConfigMgrDataWarehouse.log** : `failed to populate schema objects`

#### <a name="workaround"></a>Solution de contournement 
Vérifiez que le compte d’ordinateur du rôle de système de site est bien **db_owner** dans la base de données de l’entrepôt de données.


### <a name="reports-fail-to-open"></a>Impossible d’ouvrir les rapports

Les rapports de l’entrepôt de données ne s’ouvrent pas lorsque la base de données de l’entrepôt de données et le point de Reporting Services se trouvent sur des systèmes de site différents.  

#### <a name="workaround"></a>Solution de contournement
Accordez au **compte du point de Reporting Services** l’autorisation d’accès **db_datareader** à la base de données de l’entrepôt de données.


### <a name="error-opening-reports"></a>Erreur lors de l’ouverture des rapports

Lorsque vous ouvrez un rapport de l’entrepôt de données, l’erreur suivante est retournée :

```
An error has occurred during report processing. (rsProcessingAborted)
Cannot create a connection to data source 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection)
A connection was successfully established with the server, but then an error occurred during the pre-login handshake. (provider: SSL Provider, error: 0 - The certificate chain was issued by an authority that is not trusted.)
```

#### <a name="workaround"></a>Solution de contournement 
Effectuez les étapes suivantes pour configurer les certificats :

1. Sur l’ordinateur qui héberge la base de données de l’entrepôt de données :  

    1. Ouvrez IIS, sélectionnez **Certificats de serveur** , puis cliquez avec le bouton droit sur **Créer un certificat auto-signé**. Ensuite, spécifiez un nom convivial pour le certificat, par exemple, **Certificat d’identification SQL Server de l’entrepôt de données**. Sélectionnez le magasin de certificats en tant que **Applications personnelles**.  

    2. Ouvrez le **Gestionnaire de configuration SQL Server**. Sous **Configuration du réseau SQL Server**, cliquez avec le bouton droit pour sélectionner **Propriétés** sous **Protocoles pour MSSQLSERVER**. Passez à l’onglet **Certificat**, sélectionnez le certificat intitulé **Certificat d’identification SQL Server de l’entrepôt de données**, puis enregistrez les modifications.  

    3. Dans le **Gestionnaire de configuration SQL Server**, sous **Services SQL Server**, redémarrez les services **Service SQL Server** et **Service de rapports**.  

    4. Ouvrez la console Microsoft Management Console (MMC), puis ajoutez le composant logiciel enfichable **Certificats**. Sélectionnez le **compte d’ordinateur** de l’ordinateur local. Développez le dossier **Personnel**, puis sélectionnez **Certificats**. Exportez **Certificat d’identification SQL Server de l’entrepôt de données** sous forme de fichier **Binaire encodé DER X.509 (.cer)**.  

2. Sur l’ordinateur qui héberge SQL Server Reporting Services, ouvrez la console MMC, puis ajoutez le composant logiciel enfichable **Certificats**. Sélectionnez **Compte de l’ordinateur**. Sous le dossier **Autorités de certification racine reconnues**, importez le **certificat d’identification SQL Server de l’entrepôt de données**.  



## <a name="data-flow"></a>Flux de données   

![Diagramme montrant le flux de données logique entre les composants de site de l’entrepôt de données](./media/datawarehouse.png)

#### <a name="data-storage-and-synchronization"></a>Synchronisation et stockage des données

| Étape   | Détails  |
|--------|----------|  
| **1**  | Le serveur de site transfère et stocke les données dans la base de données de site. |  
| **2**  | Selon sa planification et sa configuration, le point de service de l’entrepôt de données récupère des données auprès de la base de données de site. |  
| **3**  | Le point de service de l’entrepôt de données transfère et stocke une copie des données synchronisées dans la base de données de l’entrepôt de données. |  


#### <a name="reporting"></a>Rapports

| Étape   | Détails  |
|--------|----------|  
| **A**  | Via des rapports intégrés, un utilisateur demande des données. La demande est transmise au point de Reporting Services à l’aide de SQL Server Reporting Services. |  
| **B**  | La plupart des rapports concernent des informations actuelles et ces demandes sont exécutées sur la base de données de site. |  
| **C**  | Quand un rapport demande des données d’historique, à l’aide de l’un des rapports de la *Catégorie* **Entrepôt de données**, la requête s’exécute sur la base de données de l’entrepôt de données. |  
