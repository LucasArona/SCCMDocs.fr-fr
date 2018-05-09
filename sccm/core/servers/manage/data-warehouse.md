---
title: Entrepôt de données
titleSuffix: Configuration Manager
description: Base de données et point de service de l’entrepôt de données pour System Center Configuration Manager
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf43e69-68b4-469a-ad58-9b66deb29057
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6d6e1850c07207205cad696918f7cd4eb97d3ec8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
#  <a name="the-data-warehouse-service-point-for-system-center-configuration-manager"></a>Le point de service de l’entrepôt de données pour System Center Configuration Manager
*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1277922-->
Utilisez le point de service de l’entrepôt de données pour stocker des données d’historique à long terme et créer des rapports sur celles-ci pour votre déploiement de Configuration Manager.

> [!TIP]
> Cette fonctionnalité a été introduite dans la version 1702 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1706, cette fonctionnalité n’est plus une fonctionnalité en préversion.  


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


L’entrepôt de données prend en charge jusqu’à 2 To de données, avec des horodatages pour le suivi des modifications. Pour stocker des données, vous utilisez des synchronisations automatisées entre la base de données du site Configuration Manager et la base de données de l’entrepôt de données. Ces informations seront ensuite accessibles à partir de votre point de Reporting Services. Les données qui sont synchronisées avec la base de données de l’entrepôt de données sont conservées pendant trois ans. Périodiquement, une tâche intégrée supprime les données datant de plus de trois ans.

Les données synchronisées incluent les éléments suivants, qui proviennent des groupes des données de site et des données globales :
- Intégrité de l’infrastructure
- Sécurité
- Compatibilité
- Programme malveillant   
- Déploiements de logiciels
- Détails d’inventaire (toutefois, l’historique d’inventaire n’est pas synchronisé)

Une fois installé, le rôle de système de site installe et configure la base de données de l’entrepôt de données. Il installe également plusieurs rapports, afin que vous puissiez facilement rechercher ces données et créer des rapports les concernant.



## <a name="prerequisites-for-the-data-warehouse-service-point"></a>Prérequis du point de service de l’entrepôt de données
- Le rôle de système de site d’entrepôt de données est pris en charge uniquement sur le site de niveau supérieur de la hiérarchie. (Un site d’administration centrale ou site principal autonome.)
- L’ordinateur sur lequel vous installez le rôle de système de site nécessite .NET Framework 4.5.2 ou version ultérieure.
- Accordez au **compte du point de Reporting Services** l’autorisation d’accès **db_datareader** à la base de données de l’entrepôt de données. 
- Le compte de l’ordinateur sur lequel vous installez le rôle de système de site est utilisé pour synchroniser les données avec la base de données de l’entrepôt de données. Ce compte nécessite les autorisations suivantes :  
  - des autorisations de niveau **Administrateur** sur l’ordinateur qui héberge la base de données de l’entrepôt de données ;
  - une autorisation **DB_Creator** sur la base de données de l’entrepôt de données ;
  - **DB_owner** ou **DB_reader** avec une autorisation **execute** sur la base de données du site de niveau supérieur.
- La base de données de l’entrepôt de données nécessite l’utilisation de SQL Server 2012 ou version ultérieure. L’édition peut être Standard, Entreprise ou Datacenter.
- Les configurations de SQL Server suivantes sont prises en charge pour héberger la base de données de l’entrepôt :  
  - Une instance par défaut
  - Instance nommée
  - Groupe de disponibilité SQL Server AlwaysOn
  - Cluster de basculement SQL Server
- Si vous utilisez des [vues distribuées](/sccm/core/servers/manage/data-transfers-between-sites#bkmk_distviews), le rôle de système de site de point de service de l’entrepôt de données doit être installé sur le serveur qui héberge la base de données du site d’administration centrale.

Pour plus d’informations sur la gestion des licences SQL Server pour la base de données de l’entrepôt de données, consultez la [FAQ sur les produits et la gestion des licences](/sccm/core/understand/product-and-licensing-faq). <!-- sms500967 -->


> [!IMPORTANT]  
> L’entrepôt de données n’est pas pris en charge lorsque l’ordinateur qui exécute le point de service de l’entrepôt de données ou qui héberge la base de données de l’entrepôt de données fonctionne avec l’une des langues suivantes :
> - JPN – Japonais
> - KOR – Coréen
> - CHS – Chinois simplifié
> - CHT – Chinois traditionnel Ce problème sera résolu dans une version à venir.


## <a name="install-the-data-warehouse"></a>Installer l’entrepôt de données
Chaque hiérarchie prend en charge une seule instance de ce rôle, sur n’importe quel système de site du site de niveau supérieur. L’instance SQL Server qui héberge la base de données de l’entrepôt peut être locale ou distante par rapport au rôle de système de site. L’entrepôt de données fonctionne avec le point de Reporting Services installé sur le même site. Il n’est pas obligatoire d’installer les deux rôles de système de site sur le même serveur.   

Pour installer le rôle, vous pouvez utiliser deux assistants : **l’Assistant Ajout des rôles de système de site** ou **l’Assistant Création d’un serveur de système de site**. Pour plus d’informations, consultez la section [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles).  

Quand vous installez le rôle, Configuration Manager crée la base de données de l’entrepôt de données pour vous sur l’instance de SQL Server que vous spécifiez. Si vous spécifiez le nom d’une base de données existante (comme vous le feriez si vous [déplaciez la base de données de l’entrepôt de données vers un nouveau serveur SQL Server](#move-the-data-warehouse-database)), Configuration Manager ne crée pas une base de données, mais utilise à la place celle que vous spécifiez.

### <a name="configurations-used-during-installation"></a>Configurations utilisées lors de l’installation
Page **Sélection du rôle système** :  

Page **Général** :
-   **Paramètres de connexion de la base de données de l’entrepôt de données Configuration Manager** :
     - **Nom de domaine complet SQL Server** : spécifiez le nom de domaine complet (FQDN) du serveur qui héberge la base de données du point de service de l’entrepôt de données.
     - **Nom de l’instance de SQL Server, le cas échéant** : si vous n’utilisez pas l’instance par défaut de SQL Server, vous devez spécifier l’instance utilisée.
     - **Nom de la base de données** : spécifiez le nom de la base de données de l’entrepôt de données. Le nom de la base de données ne doit pas dépasser 10 caractères. (La longueur du nom prise en charge sera augmentée dans une version ultérieure.)
     Configuration Manager crée la base de données de l’entrepôt de données en lui donnant ce nom. Si vous spécifiez un nom de base de données qui existe déjà sur l’instance de SQL Server, Configuration Manager utilise cette base de données.
     - **Port SQL Server utilisé pour la connexion** : spécifiez le numéro de port TCP/IP utilisé par l’instance de SQL Server qui héberge la base de données de l’entrepôt de données. Ce port est utilisé par le service de synchronisation de l’entrepôt de données pour se connecter à la base de données de ce dernier.  
     - **Compte de point de service de l’entrepôt de données** : Depuis la version 1802, indiquez le compte que SQL Server Reporting Services utilise lors de la connexion à la base de données de l’entrepôt de données. 

Page **Calendrier des synchronisations** :   
- **Calendrier des synchronisations** :
    - **Heure de début** : indiquez l’heure de début de la synchronisation de l’entrepôt de données.
    - **Périodicité** :
         - **Tous les jours** : permet d’indiquer que la synchronisation doit s’exécuter chaque jour.
         - **Hebdomadaire** : permet de spécifier une seule journée chaque semaine ainsi qu’une périodicité hebdomadaire pour la synchronisation.


## <a name="reporting"></a>Rapports
Une fois que vous aurez installé un point de service de l’entrepôt de données, plusieurs rapports seront accessibles sur le point de Reporting Services installé sur le même site. Si vous installez le point de service de l’entrepôt de données avant d’installer un point de Reporting Services, les rapports seront automatiquement ajoutés lors de l’installation du point de Reporting Services.

>[!WARNING]
>Dans Configuration Manager version 1802, une prise en charge d’autres informations d’identification a été ajoutée pour le point de l’entrepôt de données. <!--507334-->Si vous avez effectué une mise à niveau à partir d’une version précédente de Configuration Manager, vous devez spécifier les informations d’identification que SQL Server Reporting Services utilise pour se connecter à la base de données de l’entrepôt de données. Les rapports des entrepôts de données ne s’ouvrent pas tant que les informations d’identification ne sont pas spécifiées. Pour indiquer un compte, accédez à **Administration** >**Configuration du site** >**Serveurs et rôles de système de site**. Cliquez sur le serveur avec le point de service de l’entrepôt de données, puis avec le bouton droit sur le rôle de point de service de l’entrepôt de données. Sélectionnez les **propriétés** puis spécifiez le **compte de point de service de l’entrepôt de données**.

Le rôle de système de site de l’entrepôt de données comprend les rapports suivants, qui appartiennent à la catégorie **Entrepôt de données** :
 - **Déploiement de l’application – Historique** : détails du déploiement d’une application donnée pour une machine en particulier.
 - **Endpoint Protection et Compatibilité des mises à jour logicielles - Historique** : affiche les ordinateurs sur lesquels des mises à jour logicielles n’ont pas été effectuées.  
 - **Inventaire matériel général – Historique** : tout l’inventaire matériel d’une machine en particulier.
 - **Inventaire logiciel général – Historique** : tout l’inventaire logiciel d’une machine en particulier.
 - **Vue d’ensemble de l’intégrité de l’infrastructure – Historique** : vue d’ensemble de l’intégrité de l’infrastructure Configuration Manager.
 - **Liste des programmes malveillants détectés – Historique** : programmes malveillants détectés dans l’organisation.
 - **Synthèse de la distribution de logiciels – Historique** : synthèse de la distribution de logiciels pour une publication et une machine en particulier.


## <a name="expand-an-existing-stand-alone-primary-into-a-hierarchy"></a>Étendre un site principal autonome existant vers une hiérarchie
Avant d’installer un site d’administration centrale pour étendre un site principal autonome existant, vous devez désinstaller le rôle de point de service de l’entrepôt de données. Après avoir installé le site d’administration centrale, vous pouvez installer le rôle de système de site sur ce site.  

Contrairement au déplacement de la base de données de l’entrepôt de données, cette modification entraîne une perte des données historiques que vous avez synchronisées sur le site principal. La sauvegarde de la base de données à partir du site principal et sa restauration sur le site d’administration centrale ne sont pas prises en charge.




## <a name="move-the-data-warehouse-database"></a>Déplacer la base de données de l’entrepôt de données
Procédez comme suit pour déplacer la base de données de l’entrepôt de données vers un nouveau serveur SQL Server :

1.  Utilisez SQL Server Management Studio pour sauvegarder la base de données de l’entrepôt de données. Ensuite, restaurez cette base de données sur un serveur SQL Server sur le nouvel ordinateur qui héberge l’entrepôt de données.   
> [!NOTE]     
> Après avoir restauré la base de données sur le nouveau serveur, vérifiez que les autorisations d’accès à la base de données sont les mêmes sur la nouvelle base de données de l’entrepôt de données que sur la base de données de l’entrepôt de données d’origine.  

2.  Utilisez la console de Configuration Manager pour supprimer du serveur actuel le rôle de système de site du point de service de l’entrepôt de données.
3.  Réinstallez le point de service de l’entrepôt de données. Spécifiez le nom du nouveau serveur SQL Server et de l’instance qui hébergera la base de données de l’entrepôt de données que vous avez restaurée.
4.  Une fois le rôle de système de site installé, le déplacement est terminé.

## <a name="troubleshooting-data-warehouse-issues"></a>Résolution des problèmes relatifs à l’entrepôt de données
**Fichiers journaux**  
Utilisez les journaux suivants pour examiner les problèmes d’installation du point de service de l’entrepôt de données ou de synchronisation des données :
 - *DWSSMSI.log* et *DWSSSetup.log* : utilisez ces journaux pour examiner les erreurs survenues lors de l’installation du point de service de l’entrepôt de données.
 - *Microsoft.ConfigMgrDataWarehouse.log* : utilisez ce journal pour examiner la synchronisation des données entre la base de données de site et la base de données de l’entrepôt de données.

**Échec d’installation**  
 L’installation du point de service de l’entrepôt de données échoue sur un serveur de système de site distant quand le premier rôle de système de site installé sur cet ordinateur est celui de l’entrepôt de données.  
  - **Solution** : assurez-vous que l’ordinateur sur lequel vous installez le point de service de l’entrepôt de données héberge déjà au moins un autre rôle de système de site.  


**Problèmes de synchronisation connus**   
La synchronisation échoue et génère le message suivant dans le fichier *Microsoft.ConfigMgrDataWarehouse.log* : **« Impossible de remplir des objets de schéma ».**  
 - **Solution** : assurez-vous que le compte de l’ordinateur qui héberge le rôle de système de site est bien **db_owner** sur la base de données de l’entrepôt de données.

Les rapports de l’entrepôt de données ne s’ouvrent pas lorsque la base de données de l’entrepôt de données et le point de Reporting Services se trouvent sur des systèmes de site différents.  

 - **Solution** : accordez au **compte du point de Reporting Services** l’autorisation d’accès **db_datareader** à la base de données de l’entrepôt de données.

Lorsque vous ouvrez un rapport de l’entrepôt de données, l’erreur suivante est renvoyée :

*Une erreur s’est produite lors du traitement du rapport. (rsProcessingAborted) Impossible de créer une connexion à la source de données 'AutoGen__39B693BB_524B_47DF_9FDB_9000C3118E82_'. (rsErrorOpeningConnection) Une connexion a été établie avec le serveur, mais une erreur s’est ensuite produite pendant la négociation préalable à l’ouverture de session. (Fournisseur : fournisseur SSL, erreur : 0 - La chaîne de certificats a été fournie par une autorité qui n’est pas approuvée.)*

- **Solution** : procédez comme suit pour configurer les certificats.

  1. Sur l’ordinateur qui héberge la base de données de l’entrepôt de données :

    1. Ouvrez IIS, cliquez sur **Certificats de serveur**, puis cliquez avec le bouton droit sur **Créer un certificat auto-signé** et spécifiez le « nom convivial » du nom du certificat en tant que **certificat d’identification SQL Server de l’entrepôt de données**. Sélectionnez le magasin de certificats en tant que **Applications personnelles**.
    2. Ouvrez le **Gestionnaire de configuration SQL Server**. Sous **Configuration du réseau SQL Server**, cliquez avec le bouton droit pour sélectionner **Propriétés** sous **Protocoles pour MSSQLSERVER**. Ensuite, sur l’onglet **Certificat**, sélectionnez le **certificat d’identification SQL Server de l’entrepôt de données** et enregistrez les modifications.  
    3. Ouvrez le **Gestionnaire de configuration SQL Server**. Sous **Services SQL Server**, redémarrez le **service SQL Server** et le service **Reporting Service**.
    4.  Ouvrez la console MMC (Microsoft Management Console) et ajoutez le composant logiciel enfichable relatif aux **certificats**, puis sélectionnez la gestion du certificat pour le **compte d’ordinateur** de la machine locale. Ensuite, dans la console MMC, développez le dossier **Applications personnelles** > **Certificats** et exportez le **certificat d’identification SQL Server de l’entrepôt de données** en tant que fichier **Binaire codé DER X.509 (.cer)**.    
  2.    Sur l’ordinateur qui héberge SQL Server Reporting Services, ouvrez la console MMC et ajoutez le composant logiciel enfichable **Certificats**. Ensuite, sélectionnez la gestion du certificat pour le **Compte d’ordinateur**. Sous le dossier **Autorités de certification racine reconnues**, importez le **certificat d’identification SQL Server de l’entrepôt de données**.


## <a name="data-warehouse-dataflow"></a>Flux de données de l’entrepôt de données   
![Diagramme montrant le flux de données logique entre les composants de site de l’entrepôt de données](./media/datawarehouse.png)

**Synchronisation et stockage des données**

| Étape   | Détails  |
|:------:|-----------|  
| **1**  |  Le serveur de site transfère et stocke les données dans la base de données de site.  |  
| **2**  |      Selon sa planification et sa configuration, le point de service de l’entrepôt de données récupère des données auprès de la base de données de site.  |  
| **3**  |  Le point de service de l’entrepôt de données transfère et stocke une copie des données synchronisées dans la base de données de l’entrepôt de données. |  
**Rapports**

| Étape   | Détails  |
|:------:|-----------|  
| **A**  |  Via des rapports intégrés, un utilisateur demande des données. La demande est transmise au point de Reporting Services à l’aide de SQL Server Reporting Services. |  
| **B**  |      La plupart des rapports concernent des informations actuelles et ces demandes sont exécutées sur la base de données de site. |  
| **C**  | Quand un rapport demande des données d’historique, à l’aide de l’un des rapports de la *Catégorie* **Entrepôt de données**, la demande s’exécute sur la base de données de l’entrepôt de données.   |  
