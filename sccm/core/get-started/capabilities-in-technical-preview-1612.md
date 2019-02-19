---
title: Capacités de la version Technical Preview 1612
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1612 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bceab2e8-2f05-4a17-9ac8-a7a558670fb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ffe97408d5de71c9ea67b07649d7b92ad77f0a57
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56143699"
---
# <a name="capabilities-in-technical-preview-1612-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1612 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*



Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1612 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="the-data-warehouse-service-point"></a>Point de service de l’entrepôt de données
À partir de la version d’évaluation technique 1612, le point de service de l’entrepôt de données vous permet de stocker des données d’historique à long terme et de créer des rapports sur celles-ci pour votre déploiement de Configuration Manager. Pour ce faire, vous utilisez des synchronisations automatisées entre la base de données du site Configuration Manager et une base de données de l’entrepôt de données. Ces informations sont ensuite accessibles à partir de votre point de Reporting Services.

Par défaut, quand vous installez le nouveau rôle de système de site, Configuration Manager crée la base de données de l’entrepôt de données pour vous sur une instance SQL Server que vous spécifiez. L’entrepôt de données prend en charge jusqu’à 2 To de données, avec des horodatages pour le suivi des modifications.  Par défaut, les données synchronisées à partir de la base de données de site incluent les groupes de données pour les données globales, les données de site, Global_Proxy, les données cloud et les affichages de base de données. Vous pouvez également modifier les éléments synchronisés pour inclure des tables supplémentaires ou exclure des tables spécifiques dans les ensembles de réplications par défaut.
Les données par défaut qui sont synchronisées incluent des informations sur :
- Intégrité de l’infrastructure
- Sécurité
- Compatibilité
- Programme malveillant   
- Déploiements de logiciels
- Détails d’inventaire (toutefois, l’historique d’inventaire n’est pas synchronisé)

Outre l’installation et la configuration de la base de données de l’entrepôt de données, plusieurs nouveaux rapports sont installés afin de pouvoir facilement rechercher ces données et créer des rapports sur celles-ci.

### <a name="data-warehouse-dataflow"></a>Flux de données de l’entrepôt de données   
![Flux_entrepôtdedonnées](./media/datawarehouse.png)

| Étape         | Détails  |
|:------:|-----------|  
| **1**  |  Le serveur de site transfère et stocke les données dans la base de données de site.  |  
| **2** |   En fonction de sa planification et de sa configuration, le point de service de l’entrepôt de données obtient des données de la base de données de site.  |  
| **3** |  Le point de service de l’entrepôt de données transfère et stocke une copie des données synchronisées dans la base de données de l’entrepôt de données. |  
| **A** |  À l’aide de rapports intégrés, une demande de données est effectuée et transmise au point de Reporting Services à l’aide de SQL Server Reporting Services. |  
| **B** |   La plupart des rapports concernent des informations actuelles et ces demandes sont exécutées sur la base de données de site. |  
| **C** | Quand un rapport demande des données d’historique, à l’aide de l’un des rapports avec la *Catégorie* **Entrepôt de données**, la demande est exécutée sur la base de données de l’entrepôt de données.   |  

### <a name="prerequisites-for-the-data-warehouse-service-point-and-database"></a>Conditions préalables pour le point de service de l’entrepôt de données et la base de données
- Un rôle de système de site de point de Reporting Services doit être installé dans votre hiérarchie.
- L’ordinateur sur lequel vous installez le rôle de système de site nécessite .NET Framework 4.5.2 ou version ultérieure.
- Le compte d’ordinateur de l’ordinateur sur lequel vous installez le rôle de système de site doit avoir des autorisations d’administrateur local sur l’ordinateur qui hébergera la base de données de l’entrepôt de données.
- Le compte administratif que vous utilisez pour installer le rôle de système de site doit être un propriétaire de base de données (DBO) sur l’instance de SQL Server qui hébergera la base de données de l’entrepôt de données.  
- La base de données est prise en charge :
  - Avec SQL Server 2012 ou version ultérieure, Enterprise ou Datacenter Edition.
  - Sur une instance par défaut ou nommée.
  - Sur un *cluster SQL Server*. Même si cette configuration doit fonctionner, elle n’a pas été testée et une assistance est conseillée.
  - Quand elle est colocalisée avec la base de données de site ou du point de Reporting Services. Toutefois, nous recommandons de l’installer sur un serveur distinct.  
- Le compte qui est utilisé comme *compte du point de Reporting Services* doit avoir l’autorisation **db_datareader** sur la base de données de l’entrepôt de données.  
- La base de données n’est pas prise en charge sur un *groupe de disponibilité SQL Server AlwaysOn*.

### <a name="install-the-data-warehouse"></a>Installer l’entrepôt de données
Vous installez le rôle de système de site de l’entrepôt de données sur un site d’administration centrale ou site principal à l’aide de l’**Assistant Ajout des rôles de système de site** ou de l’**Assistant Création d’un serveur de système de site**. Pour plus d’informations, consultez [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Une hiérarchie prend en charge plusieurs instances de ce rôle, mais une seule instance est prise en charge sur chaque site.  

Quand vous installez le rôle, Configuration Manager crée la base de données de l’entrepôt de données pour vous sur l’instance de SQL Server que vous spécifiez. Si vous spécifiez le nom d’une base de données existante (comme vous le feriez si vous [déplaciez la base de données de l’entrepôt de données vers un nouveau serveur SQL Server](#move-the-data-warehouse-database)), Configuration Manager ne crée pas une base de données, mais utilise à la place celle que vous spécifiez.

#### <a name="configurations-used-during-installation"></a>Configurations utilisées lors de l’installation
Utilisez les informations suivantes pour terminer l’installation du rôle de système de site :

Page **Sélection du rôle système** :  
Avant que l’Assistant n’affiche une option permettant de sélectionner et d’installer le point de service de l’entrepôt de données, vous devez avoir installé un point de Reporting Services.

Page **Général** : Les informations générales suivantes sont requises :
- **Paramètres de base de données Configuration Manager :**   
  - **Nom du serveur** : spécifiez le nom de domaine complet du serveur qui héberge la base de données de site. Si vous n’utilisez pas une instance par défaut de SQL Server, vous devez spécifier l’instance après le nom de domaine complet au format suivant : ***&lt;nom-domaine-complet_SQLServer>\&lt;nom_instance>***
  - **Nom de la base de données** : spécifiez le nom de la base de données de site.
  - **Vérifier** : cliquez sur **Vérifier** pour vous assurer que la connexion à la base de données de site est établie.
</br></br>
- **Paramètres de base de données de l’entrepôt de données :**
  - **Nom du serveur** : spécifiez le nom de domaine complet du serveur qui héberge le point de service de l’entrepôt de données et la base de données. Si vous n’utilisez pas une instance par défaut de SQL Server, vous devez spécifier l’instance après le nom de domaine complet au format suivant : ***&lt;nom-domaine-complet_SQLServer>\&lt;nom_instance>***
  - **Nom de la base de données** : spécifiez le nom de domaine complet de la base de données de l’entrepôt de données.  Configuration Manager va créer la base de données avec ce nom. Si vous spécifiez un nom de base de données qui existe déjà sur l’instance de SQL Server, Configuration Manager utilise cette base de données.
  - **Vérifier** : cliquez sur **Vérifier** pour vous assurer que la connexion à la base de données de site est établie.

Page **Paramètres de synchronisation** :   
- **Paramètres des données :**
  - **Replication groups to synchronize** (Groupes de réplication à synchroniser) : sélectionnez les groupes de données que vous souhaitez synchroniser. Pour plus d’informations sur les différents types de groupes de données, consultez [Réplication de la base de données](/sccm/core/servers/manage/data-transfers-between-sites#a-namebkmkdbrepa-database-replication) et **Vues distribuées** dans [Transfert de données entre sites dans System Center Configuration Manager](/sccm/core/servers/manage/data-transfers-between-sites).
  - **Tables included to synchronize** (Tables incluses à synchroniser) : spécifiez le nom de chaque table supplémentaire que vous souhaitez synchroniser. Séparez plusieurs tables à l’aide d’une virgule. Ces tables seront synchronisées à partir de la base de données de site en plus des groupes de réplication que vous sélectionnez.
  - **Tables excluded to synchronize** (Tables exclues à synchroniser) : spécifiez le nom des tables individuelles à partir des groupes de réplication que vous synchronisez. Les tables que vous spécifiez seront exclues. Séparez plusieurs tables à l’aide d’une virgule.
- **Paramètres de synchronisation :**
  - **Intervalle de synchronisation (minutes)**  : spécifiez une valeur en minutes. Une fois que l’intervalle est atteint, une nouvelle synchronisation démarre. La plage prise en charge est comprise entre 60 et 1 440 minutes (24 heures).
  - **Planification** : spécifiez les jours où la synchronisation doit être exécutée.

**Accès au point de rapport** :   
Une fois le rôle d’entrepôt de données installé, vérifiez que le compte qui est utilisé comme *compte du point de Reporting Services* a l’autorisation **db_datareader** sur la base de données de l’entrepôt de données.

#### <a name="troubleshoot-installation-and-data-synchronization"></a>Résoudre les problèmes d’installation et de synchronisation des données
Utilisez les journaux suivants pour examiner les problèmes d’installation du point de service de l’entrepôt de données ou de synchronisation des données :
- **DWSSMSI.log** et **DWSSSetup.log** : utilisez ces journaux pour examiner les erreurs lors de l’installation du point de service de l’entrepôt de données.
-   **Microsoft.ConfigMgrDataWarehouse.log** : utilisez ce journal pour examiner la synchronisation des données entre la base de données de site et la base de données de l’entrepôt de données.

### <a name="reporting"></a>Rapports
Après avoir installé un rôle de système de site de l’entrepôt de données, les rapports suivants sont disponibles sur votre point de Reporting Services avec la *Catégorie* **Entrepôt de données** :

|Rapport                   | Détails                                  |
|-------------------------|------------------------------------------|
| **Rapport sur le déploiement d’application** | Affiche les détails du déploiement d’application pour une application et un ordinateur spécifiques.|
| **Rapport sur la compatibilité des mises à jour logicielles et Endpoint Protection**   | Affiche les ordinateurs auxquels il manque des mises à jour logicielles.|
| **Rapport sur l’inventaire matériel général**  | Affiche tout l’inventaire matériel pour un ordinateur spécifique.|
| **Rapport sur l’inventaire logiciel général**  | Affiche tout l’inventaire logiciel pour un ordinateur spécifique.|
| **Vue d’ensemble de l’intégrité de l’infrastructure**  |Affiche une vue d’ensemble de l’intégrité de votre infrastructure Configuration Manager.|
| **Liste des programmes malveillants détectés**  |Affiche les programmes malveillants qui ont été détectés dans l’organisation.|
| **Rapport de synthèse sur la distribution de logiciels** | Synthèse de la distribution de logiciels pour une publication et un ordinateur spécifiques.|

### <a name="move-the-data-warehouse-database"></a>Déplacer la base de données de l’entrepôt de données
Procédez comme suit pour déplacer la base de données de l’entrepôt de données vers un nouveau serveur SQL Server :

1. Passez en revue la configuration actuelle de la base de données et enregistrez les détails de configuration, notamment :  
   - les groupes de données que vous synchronisez ;
   - les tables que vous incluez ou excluez dans la synchronisation.       

   Après la restauration de la base de données sur un nouveau serveur et la réinstallation du rôle de système de site, vous allez reconfigurer ces groupes de données et tables.  

2. Utilisez SQL Server Management Studio pour sauvegarder la base de données de l’entrepôt de données, puis à nouveau pour restaurer cette base de données sur le nouvel ordinateur SQL Server qui hébergera l’entrepôt de données.

   Après avoir restauré la base de données sur le nouveau serveur, vérifiez que les autorisations d’accès à la base de données sont les mêmes sur la nouvelle base de données de l’entrepôt de données que sur la base de données de l’entrepôt de données d’origine.

3. Utilisez la console Configuration Manager pour supprimer le rôle de système de site de point de service de l’entrepôt de données du serveur actuel.

4. Installez un nouveau point de service de l’entrepôt de données et spécifiez le nom du nouveau serveur SQL Server et de l’instance qui héberge la base de données de l’entrepôt de données que vous avez restaurée.

5. Une fois le rôle de système de site installé, le déplacement est terminé.

Vous pouvez consulter les journaux de Configuration Manager suivants pour vérifier que le rôle de système de site a été correctement réinstallé :  
- **DWSSMSI.log** et **DWSSSetup.log** : utilisez ces journaux pour examiner les erreurs lors de l’installation du point de service de l’entrepôt de données.
-   **Microsoft.ConfigMgrDataWarehouse.log** : utilisez ce journal pour examiner la synchronisation des données entre la base de données de site et la base de données de l’entrepôt de données.


## <a name="content-library-cleanup-tool"></a>Outil de nettoyage de la bibliothèque de contenu
À partir de la version d’évaluation technique 1612, vous pouvez utiliser un nouvel outil en ligne de commande (**ContentLibraryCleanup.exe**) pour supprimer le contenu qui n’est plus associé à un package ni une application à partir d’un point de distribution (contenu orphelin). Cet outil s’appelle l’outil de nettoyage de la bibliothèque de contenu.

Cet outil n’affecte que le contenu sur le point de distribution que vous spécifiez quand vous exécutez l’outil et que vous ne pouvez pas supprimer le contenu de la bibliothèque de contenu sur le serveur de site.

Après avoir installé la version d’évaluation technique 1612, vous pouvez trouver **ContentLibraryCleanup.exe** dans le dossier *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* sur le serveur de site de la version d’évaluation technique.

L’outil fourni avec cette version d’évaluation technique est destiné à remplacer les anciennes versions des outils similaires distribués pour les produits Configuration Manager précédents. Même si cette version de l’outil cessera de fonctionner après le 1er mars 2017, de nouvelles versions accompagneront les futures versions d’évaluation technique jusqu’à ce que cet outil soit publié dans le cadre de Current Branch ou d’une version hors bande prête pour la production.

### <a name="requirements"></a>spécifications  
 - L’outil peut être exécuté directement sur l’ordinateur qui héberge le point de distribution, ou à distance à partir d’un autre serveur. L’outil peut uniquement être exécuté sur un seul point de distribution à la fois.
 - Le compte d’utilisateur qui exécute l’outil doit avoir directement des autorisations d’administration basée sur des rôles qui correspondent à un administrateur complet dans la hiérarchie Configuration Manager.  L’outil ne fonctionne pas quand un compte d’utilisateur reçoit des autorisations comme membre d’un groupe de sécurité Windows qui dispose des autorisations d’administrateur complet.

### <a name="modes-of-operation"></a>Modes opératoires
L’outil peut être exécuté dans deux modes :
1. **Mode de simulation** :   
   Quand vous ne spécifiez pas le commutateur **/delete**, l’outil s’exécute en mode de simulation et identifie le contenu qui serait supprimé à partir du point de distribution, mais ne supprime en réalité aucune donnée.

   - Quand l’outil s’exécute dans ce mode, les informations sur le contenu qui serait supprimé sont automatiquement écrites dans le fichier journal tools. L’utilisateur n’est pas invité à confirmer chaque suppression potentielle.
   - Par défaut, le fichier journal est écrit dans le dossier temporaire users sur l’ordinateur sur lequel vous exécutez l’outil, mais vous pouvez utiliser le commutateur /log pour rediriger le fichier journal vers un autre emplacement.  
   </br>

   Nous vous recommandons d’exécuter l’outil dans ce mode et de consulter le fichier journal obtenu avant d’exécuter l’outil avec le commutateur /delete.  

2. **Mode Suppression** : Quand vous exécutez l’outil avec le commutateur **/delete**, l’outil s’exécute en mode de suppression.

   - Quand l’outil s’exécute dans ce mode, le contenu orphelin qui se trouve sur le point de distribution spécifié peut être supprimé à partir de la bibliothèque de contenu du point de distribution.
   -  Avant de supprimer chaque fichier, l’utilisateur est invité à confirmer que le fichier doit être supprimé.  Vous pouvez sélectionner **Y** pour oui, **N** pour non, ou **Oui pour tout** pour ignorer les autres invites et supprimer tout le contenu orphelin.  
   </br>

   Nous vous recommandons d’exécuter l’outil en mode de simulation et de consulter le fichier journal obtenu avant d’exécuter l’outil avec le commutateur /delete.  

Quand l’outil de nettoyage de la bibliothèque de contenu s’exécute dans l’un de ces modes, il crée automatiquement un journal avec un nom qui inclut le mode d’exécution de l’outil, le nom du point de distribution, la date et l’heure de l’opération. Le fichier journal s’ouvre automatiquement quand l’exécution de l’outil est terminée. Par défaut, ce journal est écrit dans le dossier **temporaire** users sur l’ordinateur sur lequel vous exécutez l’outil, mais vous pouvez utiliser un commutateur de ligne de commande pour rediriger le fichier journal vers un autre emplacement, dont un partage réseau.   


### <a name="run-the-tool"></a>Exécution de l'outil
Pour exécuter l’outil :
1. Ouvrez une invite de commandes d’administration dans un dossier qui contient **ContentLibraryCleanup.exe**.  
2. Entrez ensuite une ligne de commande qui inclut les commutateurs de ligne de commande obligatoires ainsi que les commutateurs facultatifs que vous souhaitez utiliser.

**Problème connu** : lorsque l’outil s’exécute, une erreur de ce type peut être renvoyée si un package ou un déploiement, quel qu’il soit, a échoué ou est en cours :
-  *System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.*

**Solution de contournement :** aucune. L’outil ne peut pas identifier de façon fiable les fichiers orphelins lorsque du contenu est en cours de déploiement ou n’a pas pu être déployé. Par conséquent, l’outil ne vous autorisera pas à nettoyer le contenu tant que ce problème ne sera pas résolu.



### <a name="command-line-switches"></a>Commutateurs de ligne de commande  
Les commutateurs de ligne de commande suivants peuvent être utilisés dans n’importe quel ordre.   

|Commutateur|Détails|
|---------|-------|
|**/delete**  |**Facultatif** </br> Utilisez ce commutateur quand vous souhaitez supprimer le contenu à partir du point de distribution. Vous êtes invité à confirmer que le contenu doit être supprimé. </br></br> Quand ce commutateur n’est pas utilisé, l’outil enregistre les résultats sur le contenu qui serait supprimé, mais ne supprime aucun contenu à partir du point de distribution. </br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Facultatif** </br> Exécutez l’outil en mode silencieux qui supprime toutes les invites (telles que les invites quand vous supprimez le contenu), et n’ouvrez pas automatiquement le fichier journal. </br></br> Exemple : ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;nom de domaine complet du point de distribution>**  | **Obligatoire** </br> Spécifiez le nom de domaine complet du point de distribution que vous souhaitez nettoyer. </br></br> Exemple :  ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;nom de domaine complet du site principal>**       | **Facultatif** lors du nettoyage du contenu à partir d’un point de distribution sur un site principal.</br>**Obligatoire** lors du nettoyage du contenu à partir d’un point de distribution sur un site secondaire. </br></br> Spécifiez le nom de domaine complet du site principal auquel le point de distribution appartient, ou du site principal parent quand le point de distribution est sur un site secondaire. </br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;code du site principal>**  | **Facultatif** lors du nettoyage du contenu à partir d’un point de distribution sur un site principal.</br>**Obligatoire** lors du nettoyage du contenu à partir d’un point de distribution sur un site secondaire. </br></br> Spécifiez le code du site principal auquel le point de distribution appartient, ou du site principal parent quand le point de distribution est sur un site secondaire.</br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Facultatif** </br> Spécifiez un répertoire dans lequel placer les fichiers journaux. Il peut s’agir d’un lecteur local ou d’un emplacement sur un partage réseau.</br></br> Quand ce commutateur n’est pas utilisé, les fichiers journaux sont automatiquement placés dans le dossier temporaire users.</br></br> Exemple de lecteur local : ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemple de partage réseau : ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|


## <a name="improvements-for-in-console-search"></a>Améliorations apportées à la recherche dans la console
En nous basant sur les commentaires du site UserVoice, nous avons ajouté les améliorations suivantes à la recherche dans la console :
 - **Chemin d’accès de l’objet :**  
  De nombreux objets prennent désormais en charge une nouvelle colonne nommée **Chemin d’accès de l’objet**.  Quand vous effectuez des recherches et incluez cette colonne dans les résultats d’affichage, vous pouvez afficher le chemin d’accès à chaque objet. Par exemple, si vous exécutez une recherche d’applications dans le nœud Applications et également dans les sous-nœuds, la colonne *Chemin d’accès de l’objet* dans le volet des résultats affiche le chemin d’accès à chaque objet retourné.   

- **Conservation du texte recherché :**  
  Quand vous entrez du texte dans la zone de recherche, puis que vous changez la zone dans laquelle effectuer la recherche (d’un sous-nœud au nœud actuel), le texte saisi est désormais conservé et vous n’avez pas à le retaper.

- **Maintien de votre décision d’effectuer des recherches dans les sous-nœuds :**  
 L’option sélectionnée pour effectuer des recherches dans le *nœud actuel* ou *tous les sous-nœuds* est désormais conservée quand vous changez le nœud dans lequel vous travaillez.   Ce nouveau comportement signifie que vous n’avez pas besoin de réinitialiser constamment la décision quand vous parcourez la console.  Par défaut, quand vous ouvrez la console, l’option consiste à effectuer des recherches uniquement dans le nœud actuel.

## <a name="prevent-installation-of-an-application-if-a-specified-program-is-running"></a>Empêcher l’installation d’une application si un programme est en cours d’exécution
Vous pouvez maintenant configurer une liste de fichiers exécutables (portant l’extension .exe) dans les propriétés de type de déploiement qui, s’ils sont exécutés, bloquent l’installation d’une application. Une fois que l’installation est tentée, une boîte de dialogue demande aux utilisateurs de fermer les processus qui bloquent l’installation.

### <a name="try-it-out"></a>Faîtes un essai
Pour configurer une liste de fichiers exécutables
1.  Dans la page de propriétés de tout type de déploiement, cliquez sur l’onglet **Installer Handling** (Gestion du programme d’installation).
2.  Cliquez sur **Ajouter** pour ajouter un ou plusieurs fichiers exécutables à la liste (par exemple, **Edge.exe**)
3.  Cliquez sur **OK** pour fermer la boîte de dialogue des propriétés de type de déploiement.

À présent, quand vous déployez cette application sur un utilisateur ou un appareil et que l’un des fichiers exécutables que vous avez ajoutés est en cours d’exécution, une boîte de dialogue Centre logiciel indique à l’utilisateur final que l’installation a échoué, car une application est en cours d’exécution.

## <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nouvelle notification Windows Hello Entreprise pour les utilisateurs finaux

Une nouvelle notification Windows 10 informe les utilisateurs finaux qu’ils doivent prendre des mesures supplémentaires pour terminer l’installation de Windows Hello Entreprise (par exemple, la configuration d’un code confidentiel).

## <a name="windows-store-for-business-support-in-configuration-manager"></a>Prise en charge du Windows Store pour Entreprises dans Configuration Manager

Vous pouvez désormais déployer des applications sous licence en ligne comme étant **disponibles** à partir du Windows Store pour Entreprises vers des PC exécutant le client Configuration Manager.
Pour plus d’informations, consultez [Gérer les applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

La prise en charge de cette fonctionnalité n’est pour l’instant disponible que pour les PC qui exécutent la version d’évaluation de Windows 10 RS2.

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Revenir à la page précédente en cas d’échec d’une séquence de tâches
Vous pouvez désormais revenir à une page précédente quand vous exécutez une séquence de tâches qui échoue. Avant cette version, vous deviez redémarrer la séquence de tâches en cas d’échec. Par exemple, vous pouvez utiliser le bouton **Précédent** dans les scénarios suivants :

- Quand un ordinateur démarre dans Windows PE, la boîte de dialogue d’amorçage de la séquence de tâches peut s’afficher avant que la séquence de tâches ne soit disponible. Quand vous cliquez sur Suivant dans ce scénario, la dernière page de la séquence de tâches s’affiche avec un message indiquant qu’aucune séquence de tâches n’est disponible. À présent, vous pouvez cliquer sur **Précédent** pour relancer la recherche des séquences de tâches disponibles. Vous pouvez répéter ce processus jusqu’à ce que la séquence de tâches soit disponible.
- Quand vous exécutez une séquence de tâches, mais que les packages de contenu dépendants ne sont pas encore disponibles sur les points de distribution, la séquence de tâches échoue. Vous pouvez désormais distribuer le contenu manquant (s’il ne l’a pas encore été) ou attendre qu’il soit disponible sur les points de distribution, puis cliquer sur **Précédent** pour que la séquence de tâches recherche une nouvelle fois le contenu.

## <a name="express-installation-files-support-for-windows-10-updates"></a>Prise en charge des fichiers d’installation rapide pour les mises à jour de Windows 10
Nous avons ajouté la prise en charge des fichiers d’installation rapide dans Configuration Manager pour les mises à jour de Windows 10. Quand vous utilisez une version prise en charge de Windows 10, vous pouvez maintenant utiliser les paramètres Configuration Manager pour télécharger uniquement le delta entre la mise à jour cumulative de Windows 10 du mois en cours et la mise à jour du mois précédent. Actuellement dans Configuration Manager Current Branch, l’intégralité de la mise à jour cumulative de Windows 10 (notamment toutes les mises à jour des mois précédents) est téléchargée chaque mois. L’utilisation de fichiers d’installation rapide permet des téléchargements plus petits et des durées d’installation plus courtes sur les clients.

> [!IMPORTANT]
> Les paramètres pour la prise en charge de l’utilisation de fichiers d’installation rapide sont disponibles dans Configuration Manager, mais cette fonctionnalité est prise en charge uniquement dans Windows 10 version 1607 incluant la mise à jour de l’agent Windows Update qui a été fournie avec les mises à jour publiées le 10 janvier 2017 (Patch Tuesday). Pour plus d’informations sur ces mises à jour, consultez l’[article de support 3213986](https://support.microsoft.com/help/4009938/january-10-2017-kb3213986-os-build-14393-693). Vous pourrez utiliser les fichiers d’installation rapide après la publication du prochain ensemble de mises à jour, le 14 février 2017. Windows 10 version 1607 sans la mise à jour et les versions antérieures ne gèrent pas les fichiers d’installation rapide.


### <a name="to-enable-the-download-of-express-installation-files-for-windows-10-updates-on-the-server"></a>Pour activer le téléchargement des fichiers d’installation rapide pour les mises à jour de Windows 10 sur le serveur
Pour démarrer la synchronisation des métadonnées pour les fichiers d’installation rapide Windows 10, vous devez l’activer dans les propriétés du point de mise à jour logicielle.
1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**.
2.  Sélectionnez le site d’administration centrale ou le site principal autonome.
3.  Sur l'onglet **Accueil** dans le groupe **Paramètres** , cliquez sur **Configurer les composants de site**, puis cliquez sur **Point de mise à jour logicielle**. Sous l’onglet **Fichiers de mise à jour**, sélectionnez **Télécharger les fichiers complets de toutes les mises à jour approuvées et les fichiers d’installation rapide pour Windows 10**.

### <a name="to-enable-support-for-clients-to-download-and-install-express-installation-files"></a>Pour activer la prise en charge des clients pour télécharger et installer les fichiers d’installation rapide
Pour activer la prise en charge des fichiers d’installation rapide sur les clients, vous devez activer les fichiers d’installation rapide sur les clients dans la section Mises à jour logicielles des paramètres du client. Vous créez ainsi un écouteur HTTP qui écoute les demandes de téléchargement des fichiers d’installation rapide sur le port que vous spécifiez. Quand vous déployez les paramètres du client pour activer cette fonctionnalité sur le client, ils tentent de télécharger le delta entre la mise à jour cumulative de Windows 10 du mois en cours et la mise à jour du mois précédent (les clients doivent exécuter une version de Windows 10 qui prend en charge les fichiers d’installation rapide).
1.  Activez la prise en charge des fichiers d’installation rapide dans les propriétés du composant du point de mise à jour logicielle (procédure précédente).
2.  Dans la console Configuration Manager, accédez à **Administration** > **Paramètres du client**.
3.  Sélectionnez les paramètres du client appropriés, puis cliquez sur **Propriétés** sous l’onglet **Accueil**.
4.  Sélectionnez la page **Mises à jour logicielles** , configurez **Oui** pour le paramètre **Enable installation of Express Updates on clients** (Activer l’installation des mises à jour rapides sur les clients) et configurez le port utilisé par l’écouteur HTTP sur le client pour le paramètre **Port used to download content for Express Updates** (Port utilisé pour télécharger le contenu des mises à jour rapides).


## <a name="odata-endpoint-data-access"></a>Accès aux données de point de terminaison OData

 Configuration Manager offre désormais un point de terminaison OData RESTful pour accéder aux données Configuration Manager. Le point de terminaison est compatible avec OData version 4, qui active des outils comme Excel et Power BI pour accéder facilement aux données Configuration Manager via un seul point de terminaison. La version d’évaluation technique 1612 prend uniquement en charge l’accès en lecture aux objets dans Configuration Manager.  

Les données qui sont actuellement disponibles dans le [fournisseur WMI Configuration Manager](/sccm/develop/reference/configuration-manager-reference) sont désormais également accessibles à l’aide du nouveau point de terminaison OData RESTful. Les jeux d’entités exposés par le point de terminaison OData vous permettent d’énumérer les données que vous pouvez interroger avec le fournisseur WMI.

### <a name="try-it-out"></a>Faîtes un essai

Avant de pouvoir utiliser le point de terminaison OData, vous devez l’activer pour le site.

1.  Accédez à **Administration** > **Configuration du site** > **Sites**.
2.  Sélectionnez le site principal, puis cliquez sur **Propriétés**.
3.  Sous l’onglet Général de la feuille de propriétés du site principal, cliquez sur **Enable REST endpoint for all providers on this site** (Activer le point de terminaison REST pour tous les fournisseurs de ce site), puis sur **OK**.

Dans votre affichage de requêtes OData favori, essayez des requêtes semblables aux exemples suivants pour retourner différents objets dans Configuration Manager :

| Fonction | Requête OData |
|---|---|
| Obtenir tous les regroupements | `http://localhost/CMRestProvider/Collection` |
| Obtenir un regroupement | `http://localhost/CMRestProvider/Collection('SMS00001')`
| Obtenir les 100 premiers appareils dans le regroupement | `http://localhost/CMRestProvider/Collection('SMS00001')/Device?$top=100` |
| Obtenir un appareil avec un ID de ressource dans le regroupement | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)` |
| Obtenir le système d’exploitation de l’appareil dans le regroupement | `http://localhost/CMRestProvider/Collection('SMS00001')/Device(16777573)/OPERATING_SYSTEM` |
| Obtenir les utilisateurs dans le regroupement | `http://localhost/CMRestProvider/Collection('SMS00001')/User` |

> [!NOTE]
> Les exemples de requêtes indiqués dans le tableau utilisent *localhost* comme nom d’hôte dans l’URL et peuvent être utilisés sur l’ordinateur exécutant le fournisseur SMS. Si vous exécutez vos requêtes à partir d’un autre ordinateur, remplacez localhost par le nom de domaine complet du serveur sur lequel le fournisseur SMS est installé.

## <a name="azure-active-directory-onboarding"></a>Intégration d’Azure Active Directory

L’intégration d’Azure Active Directory (AD) crée une connexion entre Configuration Manager et Azure Active Directory qui peut être utilisée par d’autres services cloud. Vous pouvez l’utiliser pour créer la connexion nécessaire pour la passerelle de gestion cloud.

Effectuez cette tâche avec un administrateur Azure, car vous aurez besoin des informations d’identification d’administrateur Azure.

#### <a name="to-create-the-connection"></a>Pour créer la connexion :

2. Dans l’espace de travail **Administration**, choisissez **Services cloud** > **Azure Active Directory** > **Add Azure Active Directory** (Ajouter Azure Active Directory).
2. Choisissez **Connexion** pour créer la connexion à Azure AD.

#### <a name="configuration-manager-client-requirements"></a>Conditions requises pour le client Configuration Manager

Il existe plusieurs conditions requises pour activer la création de la stratégie utilisateur dans la passerelle de gestion cloud.

- Le processus d’intégration d’Azure Active Directory doit être terminé et le client doit être initialement connecté au réseau d’entreprise pour obtenir les informations de connexion.
- Les clients doivent être à la fois liés au domaine (inscrits dans Active Directory) et liés au domaine cloud (inscrits dans Azure AD).
- Vous devez exécuter la [découverte d’utilisateurs Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#active-directory-user-discovery#active-directory-user-discovery).
- Vous devez modifier le client Configuration Manager pour autoriser les demandes de stratégie utilisateur sur Internet et déployer la modification sur le client. Étant donné que cette modification sur le client a lieu *sur l’appareil client*, elle peut être déployée via la passerelle de gestion cloud même si vous n’avez pas effectué les modifications de configuration nécessaires pour la stratégie utilisateur.
- Votre point de gestion doit être configuré pour utiliser HTTPS pour sécuriser le jeton sur le réseau et .NET 4.5 doit être installé.

Après avoir apporté ces modifications à la configuration, vous pouvez créer une stratégie utilisateur et déplacer des clients vers Internet pour tester la stratégie. Les demandes de stratégie utilisateur via la passerelle de gestion cloud seront authentifiées avec l’authentification basée sur un jeton Azure AD.

## <a name="change-to-configuring-multi-factor-authentication-for-device-enrollment"></a>Modification de la configuration de l’authentification multifacteur pour l’inscription d’appareils

Maintenant que vous pouvez configurer l’authentification multifacteur pour l’inscription d’appareils dans le portail Azure, cette option a été supprimée de la console Configuration Manager. Vous trouverez d’autres informations sur la configuration de l’authentification multifacteur pour l’inscription [dans cette rubrique Microsoft Intune](https://docs.microsoft.com/en-us/intune/deploy-use/multi-factor-authentication-azure-active-directory).
