---
title: 'Opérations et maintenance pour les rapports '
titleSuffix: Configuration Manager
description: Découvrez les détails de la gestion des rapports et des abonnements aux rapports dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: fff4150d6b8b4529a6f63989447ee5acb725c92f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342288"
---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Opérations et maintenance pour les rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois l’infrastructure en place pour la création de rapports dans System Center Configuration Manager, il existe un certain nombre d’opérations que vous pouvez généralement effectuer pour gérer les rapports et les abonnements aux rapports.  

##  <a name="BKMK_ManageReports"></a> Gérer les rapports Configuration Manager  
 Configuration Manager offre plus de 400 rapports prédéfinis qui vous aident à recueillir, organiser et présenter des informations relatives aux utilisateurs, à l’inventaire logiciel et matériel, aux mises à jour logicielles, aux applications, à l’état du site et à d’autres opérations de Configuration Manager dans votre organisation. Vous pouvez utiliser les rapports prédéfinis comme ils sont, ou vous pouvez modifier un rapport pour qu'il réponde à vos besoins. Vous pouvez également créer des rapports personnalisés basés sur des modèles ou sur SQL qui répondent à vos besoins. Utilisez les sections suivantes pour mieux gérer les rapports Configuration Manager.  

###  <a name="BKMK_RunReport"></a> Exécuter un rapport Configuration Manager  
 Rapports dans le Gestionnaire de Configuration sont stockés dans SQL Server Reporting Services et les données affichées dans le rapport sont récupérées à partir de la base de données de site Configuration Manager. Vous pouvez accéder aux rapports dans la console Configuration Manager ou à l'aide du Gestionnaire de rapports dans un navigateur web. Les rapports peuvent être ouverts depuis n'importe quel ordinateur disposant d'un accès à l'ordinateur exécutant SQL Server Reporting Services, si vous possédez les droits vous permettant de consulter les rapports. Lorsque vous exécutez un rapport, le titre du rapport, la description et la catégorie sont affichés dans la langue du système d'exploitation local.  

> [!NOTE]  
>  Dans certaines langues autres que l’anglais, les caractères peuvent ne pas apparaître correctement dans les rapports.  Dans ce cas, les rapports peuvent être affichés à l’aide du Gestionnaire de rapports basé sur le web ou par le biais de la console Administration à distance.  

> [!WARNING]  
>  Pour exécuter des rapports, vous devez disposez des droits de **Lecture** pour l'autorisation **Site** et l'autorisation **Exécuter le rapport** configurée pour des objets spécifiques.  

> [!IMPORTANT]    
> Il doit y avoir une relation d’approbation bidirectionnelle pour les utilisateurs d’un domaine différent de celui du compte du Point de Reporting Servicies pour pouvoir exécuter des rapports.

> [!NOTE]  
>  Le Gestionnaire de rapports est un outil de gestion et d’accès aux rapports basé sur le web que vous utilisez pour administrer une instance de serveur de rapports unique sur un emplacement distant via une connexion HTTP. Vous pouvez utiliser le Gestionnaire de rapports pour les tâches opérationnelles, par exemple, pour afficher des rapports, modifier les propriétés des rapports et gérer les abonnements aux rapports associés. Cette rubrique indique les étapes permettant d'afficher un rapport et de modifier ses propriétés dans le Gestionnaire de rapports. Pour plus d'informations sur les autres options du Gestionnaire de rapports, voir [Gestionnaire de rapports](http://go.microsoft.com/fwlink/p/?LinkId=224916) dans la documentation en ligne de SQL Server 2008.  

 Utilisez les procédures suivantes pour exécuter un rapport de Configuration Manager.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Pour exécuter un rapport dans la console Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**, puis cliquez sur **Rapports** pour consulter la liste des rapports disponibles.  

    > [!IMPORTANT]  
    >  Dans cette version de Configuration Manager, les rapports **Tout le contenu** affichent uniquement les packages, pas les applications.  

    > [!TIP]  
    >  Si aucun rapport n'est répertorié, vérifiez que le point de Reporting Services est installé et configuré. Pour plus d’informations, consultez [Configuration des rapports](configuring-reporting.md).  

3.  Sélectionnez le rapport à exécuter, puis dans l'onglet **Accueil** , dans la section **Groupe de rapports** , cliquez sur **Exécuter** pour ouvrir le rapport.  

4.  Lorsque des paramètres sont requis, spécifiez-les, puis cliquez sur **Afficher le rapport**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>Pour exécuter un rapport depuis un navigateur Web  

1.  Dans votre navigateur web, entrez l’URL du Gestionnaire de rapports, par exemple **http:\/\/Server1\/Reports**. Vous pouvez déterminer l'URL du Gestionnaire de rapports sur le **URL du Gestionnaire de rapports** page dans le Gestionnaire de Configuration de Reporting Services.  

2.  Dans le Gestionnaire de rapports, cliquez sur le dossier de rapports pour Configuration Manager, par exemple, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Si aucun rapport n'est répertorié, vérifiez que le point de Reporting Services est installé et configuré. Pour plus d’informations, consultez [Configuration des rapports](configuring-reporting.md).  

3.  Cliquez sur la catégorie de rapport du rapport que vous souhaitez exécuter, puis cliquez sur le lien du rapport. Le rapport s'ouvre dans le Gestionnaire de rapports.  

4.  Lorsque des paramètres sont requis, spécifiez-les, puis cliquez sur **Afficher le rapport**.  

###  <a name="BKMK_ModifyReportProperties"></a> Modifier les propriétés d’un rapport Configuration Manager  
 Dans la console Configuration Manager, vous pouvez afficher les propriétés d’un rapport, telles que son nom et sa description. Si vous souhaitez modifier ces propriétés, utilisez le Gestionnaire de rapports. Utilisez la procédure suivante pour modifier les propriétés d’un rapport Configuration Manager.  

#### <a name="to-modify-report-properties-in-report-manager"></a>Pour modifier les propriétés de rapports dans le Gestionnaire de rapports  

1.  Dans votre navigateur web, entrez l’URL du Gestionnaire de rapports, par exemple **http:\/\/Server1\/Reports**. Vous pouvez déterminer l'URL du Gestionnaire de rapports sur le **URL du Gestionnaire de rapports** page dans le Gestionnaire de Configuration de Reporting Services.  

2.  Dans le Gestionnaire de rapports, cliquez sur le dossier de rapports pour Configuration Manager, par exemple, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Si aucun rapport n'est répertorié, vérifiez que le point de Reporting Services est installé et configuré. Pour plus d’informations, consultez [Configuration des rapports](configuring-reporting.md).  

3.  Cliquez sur la catégorie du rapport dont vous souhaitez modifier les propriétés, puis cliquez sur son lien. Le rapport s'ouvre dans le Gestionnaire de rapports.  

4.  Cliquez sur l'onglet **Propriétés** . Vous pouvez modifier le nom et la description du rapport.  

5.  Lorsque vous avez terminé, cliquez sur **Appliquer**. Les propriétés du rapport sont enregistrées sur le serveur de rapports et la console Configuration Manager récupère les propriétés de rapport mises à jour pour le rapport.  

###  <a name="BKMK_EditReport"></a> Modifier un rapport Configuration Manager  
 Lorsqu’un rapport Configuration Manager existant ne récupère pas les informations dont vous devez disposer ou qu’il ne donne pas la mise en page ou l’aspect que vous souhaitez, vous pouvez le modifier dans le Générateur de rapports.  

> [!NOTE]  
>  Vous pouvez aussi choisir de cloner un rapport existant en l'ouvrant pour le modifier et en cliquant sur **Enregistrer sous** pour l'enregistrer en tant que nouveau rapport.  

> [!IMPORTANT]  
>  Le compte d'utilisateur doit disposer des autorisations **Site - Modifier** et **Modifier le rapport** sur les objets spécifiques associés au rapport que vous souhaitez modifier.  

> [!IMPORTANT]  
>  Lorsque Configuration Manager est mis à niveau vers une version plus récente, les nouveaux rapports remplacent les rapports prédéfinis. Si vous modifiez un rapport prédéfini, vous devez sauvegarder le rapport avant d'installer la nouvelle version, puis restaurer le rapport dans Reporting Services. Si vous apportez des modifications importantes à un rapport prédéfini, envisagez plutôt de créer un nouveau rapport. Les nouveaux rapports que vous créez avant la mise à niveau d'un site ne sont pas remplacés.  

 Utilisez la procédure suivante pour modifier les propriétés d’un rapport Configuration Manager.  

#### <a name="to-edit-report-properties"></a>Pour modifier les propriétés d'un rapport  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**, puis cliquez sur **Rapports** pour consulter la liste des rapports disponibles.  

3.  Sélectionnez le rapport à modifier, puis dans l'onglet **Accueil** , dans la section **Groupe de rapports** , cliquez sur **Modifier**. Entrez votre compte d'utilisateur et votre mot de passe si vous y êtes invité, puis cliquez sur **OK**. Si le Générateur de rapports n'est pas installé sur l'ordinateur, vous êtes invité à l'installer. Cliquez sur **Exécuter** pour installer le Générateur de rapports, qui est requis pour modifier et créer des rapports.  

4.  Dans le Générateur de rapports, modifiez les paramètres de rapport appropriés, puis cliquez sur **Enregistrer** pour enregistrer le rapport sur le serveur de rapports.  

###  <a name="BKMK_CreateModelBasedReport"></a> Créer un rapport basé sur un modèle  
 Un rapport basé sur un modèle vous permet de sélectionner les éléments que vous souhaitez inclure dans votre rapport de manière interactive. Pour plus d’informations sur la création de modèles de rapport personnalisés, consultez [Création de modèles de rapport personnalisés pour System Center Configuration Manager dans SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  Pour pouvoir créer un rapport, le compte d'utilisateur doit disposer d'une autorisation **Site - Modifier** . L'utilisateur peut créer un rapport uniquement dans les dossiers pour lesquels il dispose d'autorisations **Modifier le rapport** .  

 Pour créer un rapport Configuration Manager basé sur un modèle, procédez comme suit.  

#### <a name="to-create-a-model-based-report"></a>Pour créer un rapport basé sur un modèle  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports** et cliquez sur **Rapports**.  

3.  Dans l'onglet **Accueil** , dans la section **Créer** , cliquez sur **Créer un rapport** pour ouvrir l' **Assistant Création de rapport**.  

4.  Sur la page **Informations** , configurez les paramètres suivants :  

    -   **Type** : Sélectionnez **Rapport basé sur un modèle** pour créer un rapport dans le Générateur de rapports en utilisant un modèle de Reporting Services.  

    -   **Nom**: Spécifiez le nom du rapport.  

    -   **Description**: Spécifiez la description du rapport.  

    -   **Serveur**: Permet d'afficher le nom du serveur sur lequel le rapport est créé.  

    -   **Chemin**: Cliquez sur **Parcourir** pour spécifier un dossier dans lequel vous souhaitez stocker le rapport.  

     Cliquez sur **Suivant**.  

5.  Sur la page **Sélection de modèle** , sélectionnez un modèle disponible dans la liste que vous utilisez pour créer ce rapport. Lorsque vous sélectionnez le modèle de rapport, la section **Aperçu** affiche les vues et les entités de SQL Server qui sont rendues disponibles par le modèle de rapport sélectionné.  

6.  Dans la page **Résumé** , vérifiez les paramètres. Cliquez sur **Précédent** pour modifier les paramètres ou cliquez sur **Suivant** pour créer le rapport dans Configuration Manager.  

7.  Sur la page **Confirmation** , cliquez sur **Fermer** pour quitter l'Assistant, puis ouvrez le Générateur de rapports pour configurer les paramètres du rapport. Entrez votre compte d'utilisateur et votre mot de passe si vous y êtes invité, puis cliquez sur **OK**. Si le Générateur de rapports n'est pas installé sur l'ordinateur, vous êtes invité à l'installer. Cliquez sur **Exécuter** pour installer le Générateur de rapports, qui est requis pour modifier et créer des rapports.  

8.  Dans le Générateur de rapports Microsoft, effectuez la mise en page du rapport, sélectionnez des données dans les vues SQL Server disponibles, ajoutez des paramètres au rapport et ainsi de suite. Pour plus d'informations sur l'utilisation du Générateur de rapports pour créer un nouveau rapport, consultez l'aide du Générateur de rapports.  

9. Cliquez sur **Exécuter** pour exécuter le rapport. Vérifiez que le rapport fournit les informations désirées. Cliquez sur **Création** pour revenir au mode Création pour modifier le rapport, si nécessaire.  

10. Cliquez sur **Enregistrer** pour enregistrer le rapport sur le serveur de rapports. Vous pouvez exécuter et modifier le nouveau rapport dans le nœud **Rapports** de l'espace de travail **Surveillance** .  

###  <a name="BKMK_CreateSQLBasedReport"></a> Créer un rapport basé sur SQL  
 Un rapport basé sur SQL vous permet de récupérer des données basées sur une instruction SQL de rapport.  

> [!IMPORTANT]  
>  Lorsque vous créez une instruction SQL pour un rapport personnalisé, ne faites pas directement référence aux tables SQL Server. Faites plutôt référence aux vues SQL Server de rapports \(noms de vues qui commencent par v\_\) à partir de la base de données de site. Vous pouvez également faire référence aux procédures stockées publiques \(noms de procédures stockées qui commencent par sp\_\) à partir de la base de données de site.  

> [!IMPORTANT]  
>  Pour pouvoir créer un rapport, le compte d'utilisateur doit disposer d'une autorisation **Site - Modifier** . L'utilisateur peut créer un rapport uniquement dans les dossiers pour lesquels il dispose d'autorisations **Modifier le rapport** .  

 Pour créer un rapport Configuration Manager basé sur SQL, procédez comme suit.  

#### <a name="to-create-a-sql-based-report"></a>Pour créer un rapport basé sur SQL  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**, puis cliquez sur **Rapports**.  

3.  Dans l'onglet **Accueil** , dans la section **Créer** , cliquez sur **Créer un rapport** pour ouvrir l' **Assistant Création de rapport**.  

4.  Sur la page **Informations** , configurez les paramètres suivants :  

    -   **Type** : Sélectionnez **Rapport basé sur SQL** pour créer un rapport dans le Générateur de rapports en utilisant une instruction SQL.  

    -   **Nom**: Spécifiez le nom du rapport.  

    -   **Description**: Spécifiez la description du rapport.  

    -   **Serveur**: Permet d'afficher le nom du serveur sur lequel le rapport est créé.  

    -   **Chemin**: Cliquez sur **Parcourir** pour spécifier un dossier dans lequel vous souhaitez stocker le rapport.  

     Cliquez sur **Suivant**.  

5.  Dans la page **Résumé** , vérifiez les paramètres. Cliquez sur **Précédent** pour modifier les paramètres ou cliquez sur **Suivant** pour créer le rapport dans Configuration Manager.  

6.  Sur la page **Confirmation** , cliquez sur **Fermer** pour quitter l'Assistant et ouvrez le Générateur de rapports pour configurer les paramètres du rapport. Entrez votre compte d'utilisateur et votre mot de passe si vous y êtes invité, puis cliquez sur **OK**. Si le Générateur de rapports n'est pas installé sur l'ordinateur, vous êtes invité à l'installer. Cliquez sur **Exécuter** pour installer le Générateur de rapports, qui est requis pour modifier et créer des rapports.  

7.  Dans le Générateur de rapports Microsoft, renseignez l'instruction SQL pour le rapport ou créez une instruction SQL à l'aide des colonnes dans les vues de SQL Server disponibles, puis ajoutez des paramètres au rapport et ainsi de suite.  

8.  Cliquez sur **Exécuter** pour exécuter le rapport. Vérifiez que le rapport fournit les informations désirées. Cliquez sur **Création** pour revenir au mode Création pour modifier le rapport, si nécessaire.  

9. Cliquez sur **Enregistrer** pour enregistrer le rapport sur le serveur de rapports. Vous pouvez exécuter le nouveau rapport dans le nœud **Rapports** de l'espace de travail **Surveillance** .  

##  <a name="BKMK_ManageReportSubscriptions"></a> Gérer les abonnements aux rapports  
 Les abonnements aux rapports dans SQL Server Reporting Services permettent de configurer la remise automatique des rapports spécifiés par courrier électronique ou vers une solution de partage de fichiers, à des intervalles de temps planifiés. Utilisez l’**Assistant Création d’abonnement** dans System Center 2012 Configuration Manager pour configurer les abonnements aux rapports.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a> Créer un abonnement aux rapports pour remettre un rapport à un partage de fichiers  
 Lorsque vous créez un abonnement aux rapports pour remettre un rapport à un partage de fichiers, le rapport est copié au format spécifié pour le partage de fichiers que vous avez indiqué. Vous ne pouvez vous abonner et demander la remise que pour un seul rapport à la fois.  

 À la différence des rapports qui sont hébergés et gérés par un serveur de rapports, les rapports qui sont remis à un dossier partagé sont des fichiers statiques. Les fonctionnalités interactives définies pour le rapport ne fonctionnent pas pour les rapports qui sont stockés sous forme de fichiers sur le système de fichiers. Les fonctionnalités d'interaction sont représentées comme des éléments statiques. Si le rapport comprend des graphiques, la présentation par défaut est utilisée. Si le rapport contient des liens renvoyant à un autre rapport, le lien est restitué sous forme de texte statique. Si vous souhaitez conserver les fonctionnalités interactives dans un rapport remis, utilisez plutôt la remise par courrier électronique. Pour plus d’informations sur la remise de courrier électronique, consultez la section [Créer un abonnement aux rapports pour remettre un rapport par courrier électronique](#BKMK_ReportSubscriptionEmail) plus loin dans cette rubrique.  

 Lorsque vous créez un abonnement qui utilise la remise par partage de fichiers, vous devez spécifier un dossier existant comme dossier de destination. Le serveur de rapports ne crée pas de dossiers sur le système de fichiers. Le dossier que vous spécifiez doit être accessible via une connexion réseau. Lorsque vous spécifiez le dossier de destination dans un abonnement, utilisez un chemin UNC et n'incluez pas de barres obliques inverses à la fin du chemin du dossier. Voici un exemple de chemin UNC valide pour le dossier de destination : \\\\&lt;nom_serveur\>\\reportfiles\\operations\\2011.  

 Les rapports peuvent être rendus dans une variété de formats de fichier, tels que MHTML ou Excel. Pour enregistrer le rapport dans un format de fichier spécifique, sélectionnez ce format de rendu lors de la création de votre abonnement. Par exemple, choisir Excel enregistre le rapport sous forme de fichier Microsoft Excel. Même s'il est possible de sélectionner n'importe quel format de rendu pris en charge, certains formats fonctionnent mieux que d'autres lors du rendu d'un fichier.  

 Utilisez la procédure suivante pour créer un abonnement aux rapports pour remettre un rapport à un partage de fichiers.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Pour créer un abonnement à un rapport en vue de remettre un rapport à un partage de fichiers  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports** , puis cliquez sur **Rapports** pour consulter la liste des rapports disponibles. Vous pouvez sélectionner un dossier de rapports pour répertorier uniquement les rapports associés à ce dossier.  

3.  Sélectionnez le rapport que vous souhaitez ajouter à l'abonnement, puis dans l'onglet **Accueil** , dans la section **Groupe de rapports** , cliquez sur **Créer un abonnement** pour ouvrir l' **Assistant Création d'abonnement**.  

4.  Sur la page **Remise d'abonnement** , configurez les paramètres suivants :  

    -   Rapport remis par : Sélectionnez **Partage de fichiers Windows** pour remettre le rapport à un partage de fichiers.  

    -   **Nom du fichier**: Spécifiez le nom de fichier du rapport. Par défaut, le fichier de rapport n'inclut pas d'extension de nom de fichier. Sélectionnez **Ajouter une extension de fichier à la création** pour ajouter automatiquement une extension de nom de fichier à ce rapport, en fonction du format de rendu.  

    -   **Chemin** : Spécifiez un chemin UNC vers un dossier existant, dans lequel vous souhaitez remettre ce rapport \(par exemple, \\\\&lt;nom_serveur\>\\&lt;partage_serveur\>\\&lt;dossier_rapport\>\).  

        > [!NOTE]  
        >  Le nom d'utilisateur spécifié ultérieurement sur cette page doit avoir accès à ce partage de serveur et disposer des autorisations d'écriture sur le dossier de destination.  

    -   **Format de rendu**: Sélectionnez l'un des formats suivants pour le fichier de rapport :  

        -   **Fichier XML avec données de rapport**: Enregistre le rapport au format Extensible Markup Language.  

        -   **CSV \(délimité par des virgules\)**  : Enregistre le rapport au format de valeurs séparées par des virgules.  

        -   **Fichier TIFF**: Enregistre le rapport au format de fichier TIFF (Tagged Image File Format).  

        -   **Fichier Acrobat \(PDF\)**  : Enregistre le rapport au format Acrobat Portable Document Format.  

        -   **HTML 4.0**: Enregistre le rapport sous la forme d'une page Web affichable uniquement dans les navigateurs qui prennent en charge le langage HTML 4.0. Internet Explorer 5 et versions ultérieures prennent en charge le langage HTML 4.0.  

            > [!NOTE]  
            >  Si votre rapport contient des images, le format HTML 4.0 ne les inclut pas dans le fichier.  

        -   **MHTML \(archive web\)**  : Enregistre le rapport au format MIME HTML \(mhtml\) pouvant être consulté avec de nombreux navigateurs web.  

        -   **Convertisseur RPL** : Enregistre le rapport au format RPL \(Report Page Layout\).  

        -   **Excel**: Enregistre le rapport sous forme de feuille de calcul Microsoft Excel.  

        -   **Word**: Enregistre le rapport sous forme de document Microsoft Word.  

    -   **Nom d'utilisateur**: Spécifiez un compte d'utilisateur Windows disposant des autorisations pour accéder au partage de serveur et au dossier de destination. Le compte d'utilisateur doit avoir accès à ce partage de serveur ainsi que l'autorisation d'écriture sur le dossier de destination.  

    -   **Mot de passe**: Spécifiez le mot de passe du compte d'utilisateur Windows. Dans **Confirmer le mot de passe**, retapez le mot de passe.  

    -   Sélectionnez l'une des options suivantes pour configurer le comportement, lorsqu'un fichier du même nom existe déjà dans le dossier de destination :  

        -   **Remplacer un fichier existant par une version plus récente**: Spécifie que la nouvelle version remplace le fichier de rapport lorsqu'il existe déjà.  

        -   **Ne pas remplacer un fichier existant**: Spécifie qu'aucune action n'est effectuée lorsque le fichier de rapport existe déjà.  

        -   **Incrémenter des noms de fichier dès que des versions plus récentes sont ajoutées**: Spécifie qu'un numéro est ajouté au nom de fichier du nouveau rapport pour le différencier des autres versions lorsque le fichier de rapport existe déjà.  

    -   **Description**: Spécifie la description de cet abonnement au rapport.  

     Cliquez sur **Suivant**.  

5.  Sur la page **Planification d'abonnement** , sélectionnez l'une des options de planification de remise suivantes pour l'abonnement aux rapports :  

    -   **Utiliser une planification partagée**: Une planification partagée est une planification prédéfinie pouvant être utilisée avec d'autres abonnements à des rapports. Activez cette case à cocher, puis sélectionnez une planification partagée dans la liste si un élément a été spécifié.  

    -   **Créer une nouvelle planification**: Configurez la planification selon laquelle ce rapport doit s'exécuter, y compris l'intervalle, l'heure et la date de début et la date de fin de cet abonnement.  

6.  Sur la page **Paramètres d'abonnement** , spécifiez les paramètres pour ce rapport qui seront utilisés lorsqu'il est exécuté en mode sans assistance. Lorsqu'il n'y a aucun paramètre pour le rapport, cette page n'est pas affichée.  

7.  Sur la page **Résumé** , passez en revue les paramètres d'abonnement au rapport. Cliquez sur **Précédent** pour modifier les paramètres ou cliquez sur **Suivant** pour créer un abonnement à un rapport.  

8.  Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant. Vérifiez que l'abonnement au rapport a été créé avec succès. Vous pouvez afficher et modifier des abonnements aux rapports dans le nœud **Abonnements** sous **Rapports** dans l'espace de travail **Surveillance** .  

###  <a name="BKMK_ReportSubscriptionEmail"></a> Créer un abonnement aux rapports pour remettre un rapport par e-mail  
 Lorsque vous créez un abonnement aux rapports afin de remettre un rapport par courrier électronique, un message qui contient le rapport en pièce jointe est envoyé aux destinataires que vous aurez configurés. Le serveur de rapports ne valide pas les adresses de messagerie et n'obtient pas d'adresses à partir d'un serveur de messagerie. Vous devez connaître à l'avance les adresses de messagerie que vous souhaitez utiliser. Par défaut, vous pouvez envoyer des rapports à n'importe quel compte de messagerie électronique valide au sein ou en dehors de votre organisation. Vous pouvez sélectionner une ou les deux options de remise par courrier électronique suivantes :  

-   Envoyer une notification et un lien hypertexte vers le rapport généré.  

-   Envoyer un rapport incorporé ou joint au message. Le format de rendu et le navigateur déterminent si le rapport est incorporé ou joint. Si votre navigateur prend en charge HTML 4.0 et MHTML et que vous sélectionnez le format de rendu MHTML \(archive web\), le rapport est incorporé dans le corps du message. Tous les autres formats de rendu \(CSV, PDF, Word, etc.\) sont ajoutés au message sous forme de pièces jointes. Reporting Services ne vérifie pas la taille de la pièce jointe ni du message avant d'envoyer le rapport. Si le message ou la pièce jointe dépasse la limite maximale autorisée par votre serveur de messagerie, le rapport n'est pas remis.  

> [!IMPORTANT]  
>  Vous devez configurer les paramètres de courrier électronique dans Reporting Services pour que l'option de remise **Courrier électronique** soit disponible. Pour plus d'informations sur la configuration des paramètres de courrier électronique dans Reporting Services, voir [Configuration d'un serveur de rapport pour la remise par courrier électronique](http://go.microsoft.com/fwlink/p/?LinkId=226668) dans la documentation en ligne de SQL Server.  

 Utilisez la procédure suivante pour créer un abonnement aux rapports permettant de remettre un rapport par courrier électronique.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>Pour créer un abonnement aux rapports permettant de remettre un rapport par courrier électronique  

-   Dans la console Configuration Manager, cliquez sur **Surveillance**.  

-   Dans l'espace de travail **Surveillance** , développez **Rapports** , puis cliquez sur **Rapports** pour consulter la liste des rapports disponibles. Vous pouvez sélectionner un dossier de rapports pour répertorier uniquement les rapports associés à ce dossier.  

-   Sélectionnez le rapport que vous souhaitez ajouter à l'abonnement, puis dans l'onglet **Accueil** , dans la section **Groupe de rapports** , cliquez sur **Créer un abonnement** pour ouvrir l' **Assistant Création d'abonnement**.  

-   Sur la page **Remise d'abonnement** , configurez les paramètres suivants :  

    -   **Rapport remis par** : Sélectionnez **E\-mail** pour remettre le rapport en tant que pièce jointe dans un message électronique.  

    -   **À**: Spécifiez une adresse de messagerie valide du destinataire du rapport.  

        > [!NOTE]  
        >  Vous pouvez saisir plusieurs destinataires en séparant chaque adresse de messagerie par un point-virgule.  

    -   **Cc**: Spécifiez l'adresse de messagerie d'un autre destinataire d'une copie du rapport (facultatif).  

    -   **Cci**: Spécifiez l'adresse de messagerie d'un autre destinataire d'une copie confidentielle du rapport (facultatif).  

    -   **Répondre à**: Spécifiez l'adresse de réponse à utiliser au cas où le destinataire déciderait de répondre au message électronique.  

    -   **Objet**: Spécifiez une ligne d'objet pour le message électronique d'abonnement.  

    -   **Priorité**: Sélectionnez l'indicateur de priorité pour ce message électronique. Sélectionnez **Faible**, **Normale**ou **Haute**. Le paramètre de priorité est utilisé par Microsoft Exchange pour définir un indicateur dans le but de spécifier l'importance du message électronique.  

    -   **Commentaire**: Spécifiez un texte à ajouter au corps du message électronique d'abonnement.  

    -   **Description**: Spécifiez la description de l'abonnement à un rapport.  

    -   **Inclure un lien**: Inclut une URL au rapport d'abonnement dans le corps du message électronique.  

    -   **Inclure un rapport** : Spécifiez que le rapport est joint au message électronique. Le format à utiliser pour joindre le rapport est indiqué dans la liste **Format de rendu** .  

    -   **Format de rendu**: Sélectionnez l'un des formats suivants pour le rapport joint :  

        -   **Fichier XML avec données de rapport**: Enregistre le rapport au format Extensible Markup Language.  

        -   **CSV \(délimité par des virgules\)**  : Enregistre le rapport au format de valeurs séparées par des virgules.  

        -   **Fichier TIFF**: Enregistre le rapport au format de fichier TIFF (Tagged Image File Format).  

        -   **Fichier Acrobat \(PDF\)**  : Enregistre le rapport au format Acrobat Portable Document Format.  

        -   **MHTML \(archive web\)**  : Enregistre le rapport au format MIME HTML \(mhtml\) pouvant être consulté avec de nombreux navigateurs web.  

        -   **Excel**: Enregistre le rapport sous forme de feuille de calcul Microsoft Excel.  

        -   **Word**: Enregistre le rapport sous forme de document Microsoft Word.  

-   Sur la page **Planification d'abonnement** , sélectionnez l'une des options de planification de remise suivantes pour l'abonnement aux rapports :  

    -   **Utiliser une planification partagée**: Une planification partagée est une planification prédéfinie pouvant être utilisée avec d'autres abonnements à des rapports. Activez cette case à cocher, puis sélectionnez une planification partagée dans la liste si un élément a été spécifié.  

    -   **Créer une nouvelle planification**: Configurez la planification selon laquelle ce rapport s'exécutera, y compris l'intervalle, l'heure et la date de début et la date de fin de cet abonnement.  

-   Sur la page **Paramètres d'abonnement** , spécifiez les paramètres pour ce rapport qui seront utilisés lorsqu'il est exécuté en mode sans assistance. Lorsqu'il n'y a aucun paramètre pour le rapport, cette page n'est pas affichée.  

-   Sur la page **Résumé** , passez en revue les paramètres d'abonnement au rapport. Cliquez sur **Précédent** pour modifier les paramètres ou cliquez sur **Suivant** pour créer un abonnement à un rapport.  

-   Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant. Vérifiez que l'abonnement au rapport a été créé avec succès. Vous pouvez afficher et modifier des abonnements aux rapports dans le nœud **Abonnements** sous **Rapports** dans l'espace de travail **Surveillance** .  
