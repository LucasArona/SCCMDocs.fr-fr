---
title: Version Technical Preview 1706
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1706 pour System Center Configuration Manager.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11ad5a0bef004b778ba431c9a2da30f51eafc443
ms.sourcegitcommit: f531d0a622f220739710b2fe6644ea58d024064a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65933301"
---
# <a name="capabilities-in-technical-preview-1706-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1706 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1706 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problèmes connus dans cette version d’évaluation technique :**

-   **Déplacer le point de distribution** : les options de la console pour déplacer un point de distribution entre sites ne peuvent pas être utilisées avec cette version en raison de la limite technique de la version préliminaire d’un seul site principal.

-   **Paramètres de conformité d’appareil** : vous pouvez rencontrer le comportement opposé lorsque vous utilisez les deux nouveaux paramètres de conformité d’appareil :
    - **Bloquer le débogage USB sur l’appareil**
    - **Bloquer les applications provenant de sources inconnues**

        Par exemple, si l’administrateur définit **Bloquer le débogage USB sur l’appareil** sur **true**, tous les appareils qui n’ont pas activé le débogage USB sont marqués comme non conformes.

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Améliorations des groupes de limites pour les points de mise à jour logicielle
<!-- 1324591 -->
Cette version inclut des améliorations pour le fonctionnement des points de mise à jour logicielle avec des groupes de limites. Voici qui résume le nouveau comportement de secours :
- L’action de secours pour les points de mise à jour logicielle utilise désormais un temps configurable pour le repli sur les groupes de limites voisins, avec une durée minimale de 120 minutes.

- Indépendamment de la configuration de secours, un client essaie d’atteindre le dernier point de mise à jour logicielle qu'il a utilisé pendant 120 minutes. Après l’échec de communication avec ce serveur pendant 120 minutes, le client vérifie ensuite son pool de points de mise à jour logicielle disponibles, afin d’en trouver un nouveau.

  -   Tous les points de mise à jour logicielle dans le groupe de limites actuel du client sont ajoutés immédiatement au pool du client.

  -   Comme un client tente d’utiliser son serveur d’origine pendant 120 minutes avant d’en rechercher d’un nouveau, aucun des serveurs supplémentaires n’est contacté jusqu'à ce que deux heures s’écoulent.

  -   Si le repli sur un groupe voisin est configuré pour un minimum de 120 minutes, les points de mise à jour logicielle à partir de ce groupe de limites voisin feront partie du pool de serveurs disponibles du client .

- Après avoir échoué pendant deux heures à atteindre le serveur d’origine, le client passe à un cycle plus court pour contacter un nouveau point de mise à jour logicielle.

  Cela signifie que si un client ne parvient pas à se connecter avec un nouveau serveur, il sélectionne rapidement le serveur suivant à partir de son pool de serveurs disponibles et tente de le contacter.

  -   Ce cycle se poursuit jusqu'à ce que le client se connecte à un point de mise à jour logicielle qu’il peut utiliser.
  -   Jusqu'à ce que le client trouve un point de mise à jour logicielle, les serveurs supplémentaires sont ajoutés à un pool de serveurs disponibles lorsque le temps de secours pour chaque groupe de limites voisin est atteint.

Pour plus d’informations, consultez la section [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) dans la rubrique Groupes de limites pour Current Branch.


## <a name="site-server-role-high-availability"></a>Rôle serveur site haute disponibilité
<!-- 1128774 -->
La haute disponibilité pour le rôle de serveur de site est une solution basée sur Configuration Manager pour installer un serveur de site principal supplémentaire en mode *Passif*. Le serveur de site en mode passif vient s’ajouter à votre serveur de site principal existant qui se trouve en mode *Actif*. Un serveur de site en mode passif est disponible pour une utilisation immédiate, si nécessaire.

Un serveur de site principal en mode passif :
-   Utilise la même base de données de site en tant que serveur de site actif.
-   Reçoit une copie de la bibliothèque de contenu des serveurs de site actifs, qui est ensuite synchronisée.
-   N’écrit pas les données dans la base de données du site tant qu’il est en mode passif.
-   Ne prend pas en charge l’installation ou la suppression de rôles de système de site facultatifs tant que le mode passif est activé.

Pour faire du serveur de site en mode passif le serveur de site en mode actif, vous le promouvez manuellement. Le serveur de site actif devient alors le serveur de site passif. Les rôles de système de site disponibles sur le serveur en mode actif d’origine restent disponibles tant l’ordinateur est accessible. Seul le rôle de serveur de site bascule entre mode passif et mode actif.

Pour installer un serveur de site en mode passif, vous utilisez **l’Assistant Création d’un serveur de système de site** pour configurer un nouveau serveur de site avec le type **Serveur de site principal** et le mode **Passif**. L’assistant exécute ensuite le programme d’installation de Configuration Manager sur le serveur spécifié pour installer le nouveau serveur de site en mode passif. Une fois l’installation terminée, le serveur de site en mode actif assure la synchronisation du serveur de site en mode passif et de sa bibliothèque de contenu avec les modifications ou configurations que vous apportez sur le serveur de site actif.

### <a name="prerequisites-and-limitations"></a>Conditions préalables et limitations
-   Un serveur de site unique en mode passif est pris en charge sur chaque site principal.

-   Le serveur de site en mode passif peut être local ou sur le cloud dans Azure.

-   Les serveurs de site en mode actif et ceux en mode passif doivent être dans le même domaine.

-   Les serveurs de site en mode actif et ceux en mode passif doivent utiliser la même base de données, qui doit être distante par rapport aux ordinateurs de chaque serveur de site.

    -   Le serveur SQL qui héberge la base de données peut utiliser une instance par défaut, appelée instance, cluster SQL Server ou groupe de disponibilité AlwaysOn.

    -   Le serveur de site en mode passif est configuré pour utiliser la même base de données de site que le serveur de site en mode actif. Toutefois, le serveur de site en mode passif n’utilise pas cette base de données jusqu'à sa promotion en mode actif.

-   L’ordinateur qui exécutera le serveur de site en mode passif :

    -   Doit respecter les [conditions requises pour installer un site principal](https://docs.microsoft.com/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).

    -   Installe à l’aide de fichiers sources correspondant à la version du serveur de site en mode actif.

    -   Ne peut pas avoir un rôle de système de site à partir d’un autre site avant d’installer le site en mode passif.

-   Les ordinateurs de serveur de site en mode passif et actif peuvent exécuter différents systèmes d’exploitation ou versions de service pack, tant les deux restent pris en charge par votre version de Configuration Manager.

-   La promotion du serveur de site en mode passif en serveur en mode actif est manuelle. Il n’y a pas de basculement automatique.

-   Les rôles de système de site peuvent être installés uniquement sur le serveur de site qui est en mode actif.

    -   Un serveur de site en mode actif prend en charge tous les rôles de système de site. Vous ne pouvez pas installer des rôles de système de site sur le serveur lorsqu’il est en mode passif.

    -   Les rôles de système de site qui utilisent une base de données (comme le point de rapport) doivent avoir cette base de données sur un serveur distant à la fois le serveur de site en mode actif et celui en mode passif.

    -   SMS_Provider n’installe pas sur le serveur de site en mode passif. Étant donné que vous devez vous connecter à un SMS_Provider pour le site afin de promouvoir manuellement le serveur de site du mode passif au mode actif, nous vous recommandons [l’installation d’au moins une instance supplémentaire du fournisseur](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider) sur un autre ordinateur.

**Problème connu** :   
Avec cette version, **l’état** pour que les conditions suivantes s’affichent dans la console en tant que valeurs numériques au lieu de texte lisible :
-   131071 – L’installation du serveur de site a échoué
-   720895 : Échec de désinstallation du rôle de serveur de site
-   851967 : Échec du basculement

### <a name="add-a-site-server-in-passive-mode"></a>Ajouter un serveur de site en mode passif
1.  Dans la console, accédez à **Administration** > **Configuration du site** > **Sites** et sélectionnez [Assistant d’ajout de rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Vous pouvez également utiliser **l'Assistant Création de serveur de système de site**.

2.  Sur la page **Général**, spécifiez le serveur qui hébergera le serveur de site en mode passif. Le serveur que vous spécifiez ne peut pas héberger les rôles de système de site avant d’installer un serveur de site en mode passif.

3.  Sur la page **Sélection du rôle système**, sélectionnez uniquement **Serveur de site principal en mode passif**.

4.  Pour terminer l’assistant, vous devez fournir les informations suivantes qui sont utilisées pour exécuter le programme d’installation et installer le rôle de serveur de site sur le serveur spécifié :
    -   Choisissez de copier les fichiers d’installation du serveur de site actif vers le nouveau serveur de site en mode passif, ou spécifiez un chemin d’accès à un emplacement qui contient le contenu du dossier **CD.Latest** du serveur de site actif.

    -   Spécifiez le même serveur de base de données de site et le même nom de base de données que ceux utilisés par le serveur de site en mode actif.

5.  Configuration Manager installe ensuite le serveur de site en mode passif sur le serveur spécifié.

Pour l’état d’installation détaillé, accédez à **Administration** > **Configuration du Site** > **Sites**.
-   L’état du serveur de site en mode passif s’affiche sous la forme **Installation**.

-   Sélectionnez le serveur, puis cliquez sur **Afficher l’état** pour ouvrir **État d’installation de serveur de site** pour plus d’informations.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Promouvoir le serveur de site en mode passif au mode actif
Lorsque vous souhaitez promouvoir le serveur de site en mode passif au mode actif, vous pouvez le faire à partir du volet **Nœuds** dans **Administration** > **Configuration du site** > **Sites**. Tant que vous pouvez accéder à une instance de SMS_Provider, vous pouvez accéder au site pour effectuer cette modification.
1.  Dans le volet **nœuds** de la console Configuration Manager, sélectionnez le serveur de site en mode passif, puis choisissez **Promouvoir en actif** dans le ruban.

2.  **L’état** simple pour le serveur que vous promouvez s’affiche dans le volet **Nœuds** sous la forme **Promotion**.

3.  Une fois la promotion terminée, la colonne **État** affiche **OK** à la fois pour le nouveau serveur de site en mode *Actif* et le nouveau serveur de site en mode *Passif*.

4.  Dans **Administration** > **Configuration du site** > **Sites**, le nom du serveur de site principal affiche désormais le nom du nouveau serveur de site en mode *Actif*.
Pour l’état détaillé, accédez à **Surveillance** > **État du serveur de site**.
    -   La colonne **Mode** identifie le serveur *Actif* et le serveur *Passif*.

    -   Lors de la promotion d’un serveur du mode passif au mode actif, sélectionnez le serveur de site que vous promouvez au mode actif, puis choisissez **Afficher l’état** à partir du ruban. Cette opération ouvre la fenêtre **État de promotion du serveur de site** qui affiche des détails supplémentaires sur le processus.

Lorsqu’un serveur de site en mode actif bascule sur le mode passif, seul le rôle de système de site est rendu passif. Tous les autres rôles de système de site installés sur cet ordinateur restent actifs et accessibles aux clients.


### <a name="daily-monitoring"></a>Surveillance quotidienne
Lorsque vous avez un site principal en mode passif, surveillez-le quotidiennement pour vous assurer qu’il reste synchronisé avec le serveur de site en mode actif et est prêt à être utilisé. Pour ce faire, accédez à **Surveillance** > **État du serveur de site**. Ici, vous pouvez afficher les serveurs de site en mode actif et ceux en mode passif.

L’onglet **Résumé** :
-   La colonne **Mode** identifie le serveur Actif et le serveur Passif.
-   La colonne **État** indique **OK** lorsque le serveur en mode passif est synchronisé avec le serveur en mode actif.
-   Pour afficher des détails supplémentaires sur l’état de synchronisation du contenu, cliquez sur **Afficher l’état** à partir de l’état de synchronisation du contenu. Cela ouvre l’onglet Bibliothèque de contenu où vous pouvez essayer de résoudre les problèmes de synchronisation du contenu.

L’onglet **Bibliothèque de contenu** :
-   Affichez **l’état** pour le contenu qui se synchronise du serveur de site actif vers le serveur de site en mode passif.
-   Vous pouvez sélectionner le contenu avec un état **Échec**, puis choisir **Synchroniser les éléments sélectionnés** à partir du ruban. Cette action tente de resynchroniser ce contenu de la source de contenu vers le serveur de site en mode passif. Lors de la récupération, l’état s’affiche sous la forme **En cours**, et si le serveur est synchronisé, l’état est **Succès**.

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches suivantes, puis envoyez-nous vos **Commentaires** à partir de l’onglet **Accueil** du ruban pour nous dire comment cela a fonctionné pour vous :
-   Je peux installer un site principal en mode passif.
-   Je peux utiliser la console pour promouvoir le serveur de site en mode passif pour en faire le serveur de site en mode actif et confirmer le changement d’état pour les deux serveurs de site.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inclure la confiance pour des fichiers et dossiers spécifiques dans une stratégie de protection des appareils
<!-- 1324676 -->
Dans cette version, nous avons ajouté des fonctionnalités supplémentaires à la gestion des stratégies [Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)

Vous pouvez éventuellement ajouter l’approbation pour des fichiers spécifiques pour les dossiers dans une stratégie Device Guard. Cela vous permet de :

1.  Résoudre les problèmes avec les comportements des programmes d’installation gérés
2.  Approuver les applications métier qui ne peuvent pas être déployées avec Configuration Manager
3.  Approuver des applications qui sont incluses dans une image de déploiement de système d’exploitation.

### <a name="try-it-out"></a>Essayez !

1.  Lorsque vous créez une stratégie Device Guard, sous l’onglet Inclusions de l’assistant de création de stratégie Device Guard, cliquez sur **Ajouter**.
2.  Dans la boîte de dialogue **Ajouter fichier ou dossier approuvé**, spécifiez les informations sur le fichier ou dossier que vous souhaitez approuver. Vous pouvez spécifier un chemin d’accès de dossier ou de fichier local, ou vous connecter à un appareil distant auquel vous êtes autorisé à vous connecter et spécifier un chemin d’accès de fichier ou de dossier sur cet appareil.
3.  Effectuez toutes les étapes de l'Assistant.


## <a name="hide-task-sequence-progress"></a>Masquer la progression de la séquence de tâches
<!-- 1354291 -->
Dans cette version, vous pouvez contrôler le moment auquel la progression de la séquence de tâches s’affiche pour les utilisateurs finaux à l’aide d’une nouvelle variable. Dans votre séquence de tâches, suivez l’étape **Définir une variable de séquence de tâches** pour définir la valeur de la variable **TSDisableProgressUI** pour masquer ou afficher la progression de la séquence de tâches. Vous pouvez suivre l’étape Définir une variable de séquence de tâches plusieurs fois dans une séquence de tâches pour modifier la valeur de la variable. Cela vous permet de masquer ou afficher la progression des séquences de tâches dans les différentes sections de la séquence de tâches.

#### <a name="to-hide-task-sequence-progress"></a>Pour afficher la progression de la séquence de tâches
Dans l’éditeur de séquences de tâches, suivez l’étape [Définir une variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) pour définir la valeur de la variable **TSDisableProgressUI** sur **True** pour masquer la progression de la séquence de tâches.

#### <a name="to-display-task-sequence-progress"></a>Pour afficher la progression des séquences de tâches
Dans l’éditeur de séquences de tâches, suivez l’étape [Définir une variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) pour définir la valeur de la variable **TSDisableProgressUI** sur **False** pour afficher la progression de la séquence de tâches.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Spécifier un autre emplacement de contenu pour installer et désinstaller le contenu
<!-- 1097546 -->
Aujourd’hui, dans Configuration Manager, vous spécifiez l’emplacement d’installation qui contient les fichiers d’installation pour une application. Lorsque vous spécifiez un emplacement d’installation, ce dernier est également utilisé comme emplacement de désinstallation pour le contenu de l’application.
Sur la base de vos retours, lorsque vous souhaitez désinstaller une application déployée, et que le contenu de l’application ne se trouve pas sur l’ordinateur client, le client va à nouveau télécharger tous les fichiers de configuration d’application à nouveau avant que l’application soit désinstallée.
Pour résoudre ce problème, vous pouvez maintenant spécifier à la fois un emplacement de contenu d’installation et éventuellement un emplacement de contenu de désinstallation. En outre, vous pouvez choisir ne pas spécifier d’emplacement de contenu de désinstallation.

### <a name="try-it-out"></a>Essayez !

1. Dans les propriétés de type de déploiement d’une application, cliquez sur l’onglet **Contenu**.
2. Configurez **l’emplacement de contenu d’installation** normalement.
3. Pour **Désinstaller les paramètres de contenu**, choisissez une des options suivantes :
    - **Identique au contenu d’installation** : le même emplacement sera utilisé, que vous installiez ou désinstalliez l’application.
    - **Aucun contenu de désinstallation** : choisissez cette option si vous ne souhaitez pas fournir d’emplacement de contenu de désinstallation de l’application.
    - **Différent du contenu d’installation** : choisissez cette option si vous souhaitez spécifier un emplacement de contenu de désinstallation différent de l’emplacement du contenu d’installation.
5. Si vous avez sélectionné **Différent du contenu d’installation**, recherchez ou entrez l’emplacement du contenu de l’application qui sera utilisé pour désinstaller l’application.
6. Cliquez sur **OK** pour fermer la boîte de dialogue des propriétés de type de déploiement.


## <a name="accessibility-improvements"></a>Améliorations d’accessibilité  
<!--1253000 -->
Cette version préliminaire apporte plusieurs améliorations aux [fonctionnalités d’accessibilité](/sccm/core/understand/accessibility-features) dans la console Configuration Manager. À savoir :     

**Nouveaux raccourcis clavier pour vous déplacer dans la console :**
-   CTRL + M - Définit le focus sur le volet principal (central).
-   CTRL + T - Définit le focus sur le nœud supérieur dans le volet de navigation. Si le focus était déjà dans ce volet, le focus est défini sur le dernier nœud que vous avez visité.
-   CTRL + I - Définit le focus sur la barre de navigation, sous le ruban.
-   CTRL + L - Définit le focus sur le champ **Recherche**, lorsqu’il est disponible.
-   CTRL + D - Définit le focus sur le volet de détails, lorsqu’il est disponible.
-   ALT - Fait basculer le focus vers et hors du ruban.

**Améliorations générales :**
-   Amélioration de la navigation dans le volet de navigation lorsque vous saisissez les lettres d’un nom de nœud.
-   La navigation au clavier via la vue principale et le ruban est désormais circulaire.
-   La navigation au clavier dans le volet d’informations est désormais circulaire. Pour revenir à l’objet ou au volet précédent, utilisez Ctrl + D, puis MAJ + TAB.
-   Après l’actualisation d’une vue de l’espace de travail, le focus est défini sur le volet principal de cet espace de travail.
-   Correction d’un problème pour activer les lecteurs d’écran pour annoncer les noms des éléments de liste.
-   Ajout des noms accessibles de plusieurs contrôles sur la page qui active les lecteurs d’écran pour annoncer des informations importantes.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Modifications apportées à l’assistant de services Azure pour prendre en charge Upgrade Readiness
<!-- 1353331 -->
À partir de cette version, utilisez l’assistant de services Azure pour configurer une connexion de Configuration Manager vers [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). L’utilisation de l’assistant simplifie la configuration du connecteur à l’aide d’un assistant commun pour les services Azure associés.   

Bien que la méthode pour configurer la connexion a changé, les conditions préalables requises pour la connexion et l’utilisation d’Upgrade Readiness restent inchangées.   

### <a name="prerequisites-for-upgrade-readiness"></a>Configuration requise pour Upgrade Readiness
La configuration requise pour une [connexion à Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics#create-a-connection-to-upgrade-readiness) est identique à celle détaillée pour la Current Branch de Configuration Manager. Nous la reprenons ici par commodité :  

**Conditions préalables**
-   Pour ajouter la connexion, votre environnement Configuration Manager doit d’abord configurer un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) dans un [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation). Quand vous ajoutez la connexion à votre environnement, Microsoft Monitoring Agent est également installé sur l’ordinateur exécutant ce rôle de système de site.
-   Inscrivez Configuration Manager comme outil de gestion « Application web et/ou API web » et obtenez l’[ID de client résultant de cette inscription](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
-   Créer une clé de client pour l’outil de gestion inscrit dans Azure Active Directory.
-   Dans le portail de gestion Azure, accordez à l’application web inscrite l’autorisation d’accès à OMS, comme décrit dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

> [!IMPORTANT]       
> Quand vous configurez l’autorisation d’accès à OMS, choisissez le rôle **Collaborateur** et accordez-lui les autorisations sur le groupe de ressources de l’application inscrite.

Après avoir établi la configuration requise, vous pouvez utiliser l’assistant pour créer la connexion.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Utilisez l’assistant de services Azure pour configurer Upgrade Readiness
1.  Dans la console, accédez à **Administration** > **Présentation** > **Services cloud** > **Services Azure**, puis choisissez **Configurer les services Azure** à partir de l’onglet **Accueil** du ruban pour démarrer **l’Assistant Services Azure**.

2.  Dans la page **Services Azure**, sélectionnez le **connecteur Upgrade Readiness**, puis cliquez sur **Suivant**.

3.  Sur la page **Application**, spécifiez votre **environnement Azure** (la version Technical Preview prend en charge uniquement le cloud public). Ensuite, cliquez sur **Importer** pour ouvrir la fenêtre **Importer des applications**.

4.  Dans la fenêtre **Importer des applications**, spécifiez les détails pour une application web qui existe déjà dans Azure AD.
    -   Indiquez un nom convivial pour le nom de client Azure AD. Ensuite, spécifiez l’ID de client, le nom de l’application, l’ID du client, la clé secrète pour l’application web Azure et l’URI d’ID d’application.
    -   Cliquez sur **Vérifier** et, en cas de réussite, cliquez sur **OK** pour continuer.

5.   Sur la page **Configuration**, spécifiez l’abonnement, le groupe de ressources et l’espace de travail Windows Analytics à utiliser avec cette connexion pour Upgrade Readiness.  

6.  Cliquez sur **Suivant** pour accéder à la page **Résumé**, puis terminez l’assistant pour créer la connexion.


## <a name="new-client-settings-for-cloud-services"></a>Nouveaux paramètres client pour les services cloud
<!-- 1319883 -->

Dans cette version, nous avons ajouté deux nouveaux paramètres client à Configuration Manager. Vous les trouverez dans la section **Services cloud**.  Ces paramètres vous offrent les fonctionnalités suivantes :

- Contrôlez les clients Configuration Manager qui peuvent accéder à une passerelle de gestion cloud configurée.
- Inscrivez automatiquement des clients Configuration Manager joints à un domaine Windows 10 avec Azure Active Directory.

Ces nouveaux paramètres vous aident à effectuer les fonctions décrites dans [Configuration Manager 1705 Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1705#new-capabilities-for-azure-ad-and-cloud-management).

### <a name="before-you-start"></a>Avant de commencer

Vous devez avoir installé et configuré Azure AD Connect entre votre annuaire Active Directory local et votre client Azure AD.

Si vous supprimez la connexion, les appareils ne sont pas désinscrits, mais aucun nouvel appareil n’est inscrit.

### <a name="try-it-out"></a>Essayez !

1. Configurer la section suivante de paramètres client (figurant dans les services cloud) en utilisant les informations dans [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).
    -   **Inscrire automatiquement les nouveaux appareils joints à un domaine Windows 10 avec Azure Active Directory** : réglez sur**Oui** (valeur par défaut) ou **Non**.
    -   **Permettre aux clients d’utiliser une passerelle de gestion cloud** : réglez sur **Oui** (valeur par défaut) ou **Non**.
2.  Déployez les paramètres client sur la collection requise d’appareils.

Pour confirmer que l’appareil est joint à Azure AD, exécutez la commande **dsregcmd.exe /status** dans une fenêtre d’invite de commandes. Le champ **AzureAdjoined** dans les résultats affiche **OUI** si l’appareil est joint à Azure AD.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager
<!-- 1236459 -->

Dans Configuration Manager, vous pouvez déployer des scripts sur des appareils clients à l’aide de packages et de programmes. Dans la Technical Preview, nous avons ajouté de nouvelles fonctionnalités qui vous permettent d’effectuer les actions suivantes :

- Importer des scripts PowerShell dans Configuration Manager
- Modifier les scripts à partir de la console Configuration Manager (pour les scripts non signés uniquement)
- Marquer les scripts comme Approuvés ou Refusés pour améliorer la sécurité
- Exécuter des scripts sur des collections d’ordinateurs clients Windows, et des ordinateurs Windows gérés localement. Vous ne pouvez pas déployer des scripts : ils sont exécutés en temps quasi réel sur les appareils clients.
- Examinez les résultats retournés par le script dans la console Configuration Manager.


### <a name="prerequisites"></a>Prérequis

Pour utiliser des scripts, vous devez être membre du rôle de sécurité Configuration Manager approprié.

- **Pour importer et créer des scripts**, votre compte doit avoir les autorisations **Créer** pour les **Scripts SMS** dans le rôle de sécurité **Administrateur complet**.
- **Pour approuver ou refuser des scripts**, votre compte doit avoir les autorisations **Approuver** pour les **Scripts SMS** dans le rôle de sécurité **Administrateur complet**.
- **Pour exécuter des scripts**, votre compte doit avoir les autorisations **Exécuter des scripts** pour les **Collections** dans le rôle de sécurité **Gestionnaire de paramètres de conformité**.

Pour plus d'informations sur les rôles de sécurité de Configuration Manager, voir [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).

Par défaut, les utilisateurs ne peuvent pas approuver un script qu'ils ont créé. Étant donné que les scripts sont puissants, flexibles et peuvent être déployés sur de nombreux appareils, nous avons ajouté un nouveau concept avec la possibilité de séparer les rôles entre la personne qui crée le script et celle qui l’approuve. Cela procure un niveau supplémentaire de sécurité par rapport à l’exécution d’un script sans supervision. Vous pouvez désactiver cette approbation secondaire, pour faciliter les tests, particulièrement en version Technical Preview.

Pour autoriser les utilisateurs à approuver leurs propres scripts :

1. Dans la console Configuration Manager, cliquez sur **Administration**.
2. Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.
3. Dans la liste des sites, sélectionnez votre site, puis, dans l’onglet **accueil**, sous le groupe **Sites**, cliquez sur **Paramètres de hiérarchie**.
4. Dans l’onglet **Général** de la boîte de dialogue **Propriétés des paramètres de hiérarchie**, décochez la case **Ne pas autoriser les auteurs à approuver leurs propres scripts**.


### <a name="try-it-out"></a>Essayez !

#### <a name="import-and-edit-a-script"></a>Importer et modifier un script

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un script**.
4. Sur la page **Script** de l’assistant **Créer un script**, configurez les éléments suivants :
    - **Nom de script** : entrez un nom pour le script. Vous pouvez créer plusieurs scripts portant le même nom, mais il sera alors difficile de trouver le script dont vous avez besoin dans la console Configuration Manager.
    - **Langage du script** : actuellement, seuls les scripts **PowerShell** sont pris en charge.
    - **Importer** : importez un script PowerShell dans la console. Le script s’affiche dans le champ **Script**.
    - **Effacer**  : supprime le script en cours du champ **Script**.
    - **Script** : affiche le script actuellement importé. Vous pouvez modifier le script dans ce champ si nécessaire.
5. Effectuez toutes les étapes de l'Assistant. Le nouveau script s’affiche dans la liste **Script** avec l’état **En attente d’approbation**. Avant de pouvoir exécuter ce script sur les appareils clients, vous devez l’approuver.


#### <a name="approve-or-deny-a-script"></a>Approuver ou refuser un script



Avant de pouvoir exécuter un script, il doit être approuvé. Pour approuver un script :

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans la liste **Script**, sélectionnez le script que vous souhaitez approuver ou refuser puis, dans l’onglet **Accueil**, sous le groupe **Script**, cliquez sur **Approuver/Refuser**.
4. Dans la boîte de dialogue **Approuver ou refuser le script**, **Approuvez** ou **Refusez** le script et entrez éventuellement un commentaire sur votre décision. Si vous refusez un script, il ne peut pas être exécuté sur les appareils clients.
5. Effectuez toutes les étapes de l'Assistant. Dans la liste **Script**, vous verrez la colonne **État d’approbation** changer en fonction de votre action.

#### <a name="run-a-script"></a>Exécuter un script

Une fois qu’un script a été approuvé, il peut être exécuté sur une collection que vous choisissez.

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2. Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements de périphériques**.
3. Dans la liste **Collections d’appareils**, cliquez sur la collection d’appareils sur laquelle vous souhaitez exécuter le script.
3. Sous l'onglet **Accueil**, dans le groupe **Tous les systèmes**, cliquez sur **Exécuter le script**.
4. Sur la page **Script** de l’assistant **Exécuter le Script**, choisissez un script dans la liste. Seuls les scripts approuvés sont affichés. Cliquez sur **Suivant**, puis complétez l’Assistant.

#### <a name="monitor-a-script"></a>Surveiller un script

Après avoir exécuté un script sur les appareils clients, utilisez cette procédure pour surveiller la réussite de l’opération.

1. Dans la console Configuration Manager, cliquez sur **Surveillance**.
2. Dans la liste **Surveillance** , cliquez sur **Résultats du script**.
3. Dans la liste **Résultats du script**, vous pouvez voir les résultats pour chaque script que vous avez exécuté sur des appareils clients. Un code de sortie de script de **0** indique généralement que le script a été exécuté avec succès.

## <a name="pxe-network-boot-support-for-ipv6"></a>Prise en charge du démarrage réseau PXE pour IPv6
<!-- 1269793 -->
Vous pouvez maintenant activer la prise en charge du démarrage réseau PXE pour IPv6 afin de démarrer un déploiement de système d’exploitation de séquence de tâches. Lorsque vous utilisez ce paramètre, les points de distribution compatibles PXE prendront en charge à la fois IPv4 et IPv6. Cette option ne nécessite pas de WDS arrête WDS s’il est présent.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>Pour activer la prise en charge du démarrage PXE pour IPv6
Utilisez la procédure suivante pour activer l’option de prise en charge IPv6 pour PXE.

1. Dans la console Configuration Manager, accédez à **Administration** > **vue d’ensemble** > **Points de distribution**, puis cliquez sur **Propriétés** pour les points de distribution compatibles PXE.
2. Dans l’onglet **PXE**, sélectionnez **Prise en charge d’IPv6** pour activer la prise en charge d’IPv6 pour PXE.

## <a name="manage-microsoft-surface-driver-updates"></a>Gérer les mises à jour du pilote Microsoft Surface
<!-- 1098490 -->
Vous pouvez maintenant utiliser Configuration Manager pour gérer les mises à jour du pilote Microsoft Surface.

### <a name="prerequisites"></a>Prérequis
Tous les points de mise à jour logicielle doivent exécuter Windows Server 2016.

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches suivantes, puis envoyez-nous vos **Commentaires** à partir de l’onglet **Accueil** du ruban pour nous dire comment cela a fonctionné pour vous :
1. Activer la synchronisation pour les pilotes Microsoft Surface. Utilisez la procédure décrite dans [Configurer la classification et les produits](/sccm/sum/get-started/configure-classifications-and-products) et sélectionnez **Inclure les pilotes Microsoft Surface et les mises à jour du microprogramme** dans l’onglet **Classifications** pour activer les pilotes Surface.
2. [Synchroniser les pilotes Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates.md).
3. [Déployer des pilotes Microsoft Surface synchronisés](/sccm/sum/deploy-use/deploy-software-updates)

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configuration de Windows Update pour les stratégies d’entreprise de report d’entreprise
<!-- 1290890 -->
Vous pouvez maintenant configurer des stratégies de report pour les appareils Windows 10 avec mises à jour de fonctionnalités ou de qualité gérés directement par Windows Update for Business. Vous pouvez gérer les stratégies de report du nouveau nœud **Stratégies Windows Update for Business** sous **Bibliothèque de logiciels** > **Maintenance de Windows 10**.

### <a name="prerequisites"></a>Prérequis
Les appareils Windows 10 gérés par Windows Update for Business doivent avoir une connectivité Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Pour créer une stratégie de report Windows Update for Business
1. Dans **Bibliothèque de logiciels** > **Maintenance de Windows 10** > **Mises à jour de Windows pour les stratégies d’entreprise**
2. Sous l’onglet **Accueil**, dans le groupe **Créer**, sélectionnez **Créer une stratégie Windows Update for Business** pour ouvrir l’assistant de création de stratégie Windows Update for Business.
3. Dans la page **Général**, indiquez un nom et une description pour la stratégie.
4. Sur la page **Stratégies de report**, choisissez de différer ou suspendre les mises à jour de fonctionnalités.    
    Les mises à jour de fonctionnalités sont généralement de nouvelles fonctionnalités pour Windows. Après avoir configuré le paramètre **Niveau de préparation de la branche**, vous pouvez définir si et pour quelle durée vous souhaitez différer la réception des fonctionnalités mises à jour après leur disponibilité auprès de Microsoft.
    - **Niveau de disponibilité de la branche** : Définissez la branche pour laquelle l’appareil recevra les mises à jour de Windows (Current Branch ou Current Branch for Business).
    - **Période de report (jours)** :  Spécifiez le nombre de jours pendant lesquels les mises à jour de fonctionnalités sont différées. Vous pouvez différer la réception de ces mises à jour de fonctionnalités pendant une période de 180 jours à partir de leur publication.
    - **Suspendre le démarrage des mises à jour de fonctionnalités** : Choisissez de suspendre la réception des mises à jour de fonctionnalités sur vos appareils pendant une période de 60 jours à partir du moment auquel vous suspendez les mises à jour. Une fois que le nombre maximal de jours s’est écoulé, la fonctionnalité de pause expirera automatiquement et l’appareil analysera les mises à jour de Windows pour déterminer celles qui sont applicables. Suite à cette analyse, vous pouvez à nouveau suspendre les mises à jour. Vous pouvez reprendre les mises à jour de fonctionnalités en désactivant la case à cocher.   
5. Choisissez de différer ou suspendre les mises à jour de qualité.     
    Les mises à jour de qualité sont généralement des améliorations et correctifs apportés aux fonctionnalités existantes de Windows, et sont généralement publiées le premier mardi de chaque mois, même si la publication peut être effectuée à tout moment par Microsoft. Vous pouvez définir si et pour combien de temps vous souhaitez différer la réception des mises à jour de qualité après leur disponibilité.
    - **Période de report (jours)** : Spécifiez le nombre de jours pendant lesquels les mises à jour de fonctionnalités sont différées. Vous pouvez différer la réception de ces mises à jour de fonctionnalités pendant une période de 180 jours à partir de leur publication.
    - **Suspendre le démarrage des mises à jour de qualité** : Choisissez de suspendre la réception des mises à jour de qualité sur vos appareils pendant une période de 35 jours à partir du moment auquel vous suspendez les mises à jour. Une fois que le nombre maximal de jours s’est écoulé, la fonctionnalité de pause expirera automatiquement et l’appareil analysera les mises à jour de Windows pour déterminer celles qui sont applicables. Suite à cette analyse, vous pouvez à nouveau suspendre les mises à jour. Vous pouvez reprendre les mises à jour de qualité en désactivant la case à cocher.
6. Sélectionnez **Installer les mises à jour à partir d’autres produits Microsoft** pour activer le paramètre de stratégie de groupe qui rend les paramètres de report applicables à Microsoft Update, ainsi qu’aux mises à jour de Windows.
7. Sélectionnez **Inclure les pilotes avec Windows Update** pour mettre à jour automatiquement les pilotes proposés avec les mises à jour de Windows. Si vous désactivez ce paramètre, les mises à jour de pilotes ne sont pas téléchargées à partir des mises à jour de Windows.
8. Terminez l'Assistant pour créer la stratégie de report.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Pour déployer une stratégie de report Windows Update for Business
1. Dans **Bibliothèque de logiciels** > **Maintenance de Windows 10** > **Mises à jour de Windows pour les stratégies d’entreprise**
2. Sous l’onglet **Accueil** du groupe **Déploiement**, sélectionnez **Déployer la stratégie Windows Update for Business**.
3. Configurez les paramètres suivants :
    - **Stratégie de configuration à déployer** : Sélectionnez la stratégie Windows Update for Business que vous souhaitez déployer.
    - **Regroupement** : Cliquez sur **Parcourir** pour sélectionner le regroupement dans lequel vous souhaitez déployer la stratégie.
    - **Résoudre les règles non conformes lorsqu’elles sont prises en charge** : Sélectionnez cette option pour résoudre automatiquement toutes les règles qui ne sont pas compatibles pour Windows Management Instrumentation (WMI), le registre, les scripts et tous les paramètres des appareils mobiles inscrits par Configuration Manager.
    - **Autoriser les corrections en dehors de la fenêtre de maintenance** : Si une fenêtre de maintenance a été configurée pour le regroupement vers lequel vous déployez la stratégie, activez cette option pour laisser les paramètres de compatibilité résoudre la valeur en dehors de la fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Générer une alerte** : Configure une alerte qui est générée si la compatibilité de la base de référence de configuration est inférieure à un pourcentage spécifié par une date et une heure spécifiques. Vous pouvez également spécifier si vous souhaitez qu'une alerte soit envoyée à System Center Operations Manager.
    - **Délai aléatoire (heures)** : Spécifie un délai pour éviter un traitement excessif sur le service d’inscription d’appareils réseau. La valeur par défaut est 64 heures.
    - **Calendrier** : Spécifier le calendrier d’évaluation de la compatibilité par rapport auquel le profil déployé est évalué sur les ordinateurs clients. Il peut s'agir d'un calendrier simple ou d'un calendrier personnalisé. Lorsque l'utilisateur ouvre une session, le profil est évalué par les ordinateurs clients.
4.  Terminez l’assistant pour déployer le profil.



## <a name="support-for-entrust-certification-authorities"></a>Prise en charge des autorités de certification Entrust
<!-- 1350740 -->
Configuration Manager prend désormais en charge les autorités de certification Entrust ; Cela permet la remise de certificats PFX pour les appareils inscrits dans Microsoft Intune.

Vous pouvez configurer Entrust en tant qu’autorité de certification lors de l’ajout d’un rôle de point d’enregistrement de certificat dans Configuration Manager. Lorsque vous ajoutez un nouveau profil de certificat qui émet des certificats PFX, vous pouvez sélectionner une autorité de certification Microsoft ou Entrust.

**Problème connu** : Sans la préversion technique 1706, les certificats PFX ne sont pas émis pour les autorités de certification Microsoft. Cela n’affecte pas les certificats PFX importés ou les profils SCEP.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Prise en charge de Cisco (IPsec) pour les profils VPN iOS
<!-- 1321367 -->

Vous pouvez créer un profil VPN iOS avec Cisco (IPsec) comme type de connexion. Pour plus d’informations, consultez [Créer des profils VPN](https://docs.microsoft.com/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="new-windows-configuration-item-settings"></a>Nouveaux paramètres d’élément de configuration Windows
<!-- 1354715 -->

Dans cette version, nous avons ajouté les nouveaux paramètres suivants, que vous pouvez utiliser dans les éléments de configuration Windows :

### <a name="password"></a>Mot de passe

- **Chiffrement de l’appareil**

### <a name="device"></a>Appareil

- **Modification des paramètres de région (version de bureau uniquement)**
- **Modification des paramètres d’alimentation et de mise en veille**
- **Modification des paramètres de langue**
- **Modification de l’heure du système**
- **Changement de nom d’appareil**

### <a name="store"></a>Magasin

- **Mettre à jour automatiquement les applications du Store**
- **Utiliser uniquement le magasin privé**
- **Stocker le démarrage de l’application d’origine**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Bloquer l’accès à about:flags**
- **Remplacement de l’invite de commandes SmartScreen**
- **Remplacement de l’invite de commandes SmartScreen pour les fichiers**
- **Adresse IP localhost WebRTC**
- **Moteur de recherche par défaut**
- **URL OpenSearch XML**
- **Pages d’accueil (version de bureau uniquement)**

Pour plus d'informations sur les paramètres de compatibilité, consultez [Garantir la conformité des appareils](/sccm/compliance/understand/ensure-device-compliance).


## <a name="new-device-compliance-policy-rules"></a>Nouvelles règles de stratégie de conformité d’appareil

* **Type de mot de passe requis**. Spécifie si les utilisateurs doivent créer un mot de passe de type alphanumérique ou numérique. Pour les mots de passe alphanumériques, vous spécifiez également le nombre minimal de jeux de caractères que le mot de passe doit avoir. Les quatre jeux de caractères sont : lettres minuscules, lettres majuscules, symboles et chiffres.

    **Pris en charge sur :**
    * Windows Phone 8+
    * Windows 8.1+
    * iOS 6+
<br></br>
* **Bloquer le débogage USB sur l’appareil**. Vous n’avez pas à configurer ce paramètre, car le débogage USB est déjà désactivé pour les appareils Android for Work.

    **Pris en charge sur :**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Bloquer les applications provenant de sources inconnues**. Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues. Vous n’avez pas à configurer ce paramètre, car les appareils Android for Work limitent toujours l’installation à partir de sources inconnues.

    **Pris en charge sur :**
    * Android 4.0+
    * Samsung KNOX Standard 4.0+
<br></br>
* **Exiger l’analyse des menaces sur les applications**. Ce paramètre spécifie que la fonction Vérifier les applications est activée sur l’appareil.

    **Pris en charge sur :**
    * Android 4.2 à 4.4
    * Samsung KNOX Standard 4.0+

Consultez [Créer et déployer une stratégie de conformité d’appareil](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy) pour essayer les nouvelles règles de conformité d’appareil.

## <a name="new-mobile-application-management-policy-settings"></a>Nouveaux paramètres de stratégie de gestion d’application mobile
À partir de cette version, vous pouvez utiliser trois nouveaux paramètres de stratégie de gestion des applications mobiles (MAM) :

- **Bloquer la capture d’écran (appareils Android uniquement) :** Spécifie que les fonctionnalités de capture d'écran de l'appareil sont bloquées lors de l'utilisation de cette application.

- **Désactiver la synchronisation des contacts :** Empêche l’application d’enregistrer des données sur l’application Contacts native de l’appareil.

- **Désactiver l’impression :** Empêche l’application d’imprimer des données scolaires ou de travail.

Consultez [Protéger les applications à l’aide des stratégies de protection des applications de Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) pour essayer de nouveaux paramètres de stratégie de protection d’application.

## <a name="android-and-ios-enrollment-restrictions"></a>Restrictions de l’inscription Android et iOS
<!-- 1290826 -->
À partir de cette version, les administrateurs peuvent spécifier que les utilisateurs ne peuvent pas inscrire des appareils Android ou iOS personnels dans leur environnement hybride. Cela vous permet de limiter les appareils inscrits aux appareils prédéclarés, appareils d’entreprise ou appareils iOS inscrits avec le programme d’inscription des appareils.

### <a name="try-it-out"></a>Faîtes un essai
1. Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.
2. Sous l’onglet **Accueil**, dans le groupe **Abonnement**, choisissez **Configurer des plateformes**, puis **Android** ou **iOS**.
3. Sélectionnez **Bloquer les appareils personnels**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Stratégie de gestion des applications Android for Work pour le copier-coller
Nous avons mis à jour les descriptions de paramètre pour les éléments de configuration Android for Work pour **Autoriser le partage de données entre le profil de travail et le profil personnel**.

|Avant la Technical Preview 1706 | Nouveau nom de l’option | Comportement|
|-|-|-|
|Empêcher le partage au-delà des limites| Restrictions du partage par défaut| Travail vers personnel : Par défaut (doit être bloqué sur toutes les versions) <br>Personnel vers travail : Par défaut (autorisé sur 6.x+, bloqué sur 5.x)|
|Sans restriction|   Les applications dans le profil personnel peuvent traiter les demandes de partage du profil professionnel| Travail vers personnel : Autorisé  <br>Personnel vers travail : Autorisé|
|Les applications dans le profil professionnel peuvent traiter les demandes de partage du profil personnel |Les applications dans le profil professionnel peuvent traiter les demandes de partage du profil personnel |Travail vers personnel : Valeur par défaut<br>Personnel vers travail : Autorisé<br>(Utile uniquement sur 5.x, où personnel vers travail est bloqué)|

Aucune de ces options n’empêche directement le comportement de copier-coller. Nous avons ajouté un paramètre personnalisé au service et à l’application de portail d’entreprise dans la version 1704. Il peut être configuré pour éviter le copier-coller. Vous pouvez le définir via une URI personnalisée.

-   OMA-URI:  ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
-   Type de valeur : Booléen

Le paramètre DisallowCrossProfileCopyPaste réglé sur true empêche le comportement de copier-coller entre le profil personnel et le profil de travail Android for Work.

### <a name="try-it-out"></a>Faîtes un essai
1. Dans la console Configuration Manager, sélectionnez **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de conformité** > **Éléments de configuration**.
2. Choisissez **Créer** pour créer un nouvel élément de configuration, et spécifiez **Nom** et **Android for Work**.
3. Dans les groupes de paramètres d’appareil à configurer, sélectionnez **Profil de travail**, puis **suivant**.
4. Sélectionnez la valeur **Autoriser le partage de données entre les profils personnels et professionnels**, puis terminez l’assistant.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel
<!-- 1097546 -->
Depuis cette version, vous pouvez utiliser l’état d’attestation d’intégrité de l’appareil en tant que règle de stratégie de conformité pour l’accès conditionnel aux ressources d’entreprise.

### <a name="try-it-out"></a>Faîtes un essai
Sélectionnez une règle d’attestation d’intégrité de l’appareil dans le cadre d’une évaluation de stratégie de conformité.
