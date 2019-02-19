---
title: Créer des rapports personnalisés
titleSuffix: Configuration Manager
description: Définissez des modèles de rapport pour répondre aux besoins de votre activité, puis déployez-les sur Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f2df88b4-c348-4dcf-854a-54fd6eedf485
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: ab6cb2816096697d4ccff6db17f03e4aac1d4f14
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127216"
---
# <a name="creating-custom-report-models-for-system-center-configuration-manager-in-sql-server-reporting-services"></a>Création de modèles de rapport personnalisés pour System Center Configuration Manager dans SQL Server Reporting Services

*S’applique à : System Center Configuration Manager (Current Branch)*

Des exemples de modèles de rapport sont inclus dans System Center Configuration Manager, mais vous pouvez également définir des modèles de rapport qui répondent aux besoins de votre activité, puis déployer le modèle de rapport sur Configuration Manager pour l’utiliser quand vous créez des rapports basés sur des modèles. Le tableau suivant indique les étapes à suivre pour créer et déployer un modèle de rapport basique.  

> [!NOTE]  
>  Pour connaître les étapes à suivre pour créer un modèle de rapport plus avancé, voir la section [Étapes de création d'un modèle de rapport avancé dans SQL Server Reporting Services](#AdvancedReportModel) dans cette rubrique.  

|Étape|Description|Informations complémentaires|  
|----------|-----------------|----------------------|  
|Vérifier que SQL Server Business Intelligence Development Studio est installé|Les modèles de rapport sont conçus et créés à l'aide de SQL Server Business Intelligence Development Studio. Vérifiez que SQL Server Business Intelligence Development Studio est installé sur l'ordinateur sur lequel vous créez le modèle de rapport personnalisé.|Pour plus d'informations sur SQL Server Business Intelligence Development Studio, consultez la documentation de SQL Server 2008.|  
|Création d'un projet de modèle de rapport|Un projet de modèle de rapport comprend un fichier de définition de la source de données (.ds), un fichier de définition d'une vue de source de données (.dsv) et un fichier de modèle de rapport (.smdl).|Pour plus d'informations, voir la section [Pour créer le projet de modèle de rapport](#BKMK_CreateReportModelProject) de cette rubrique.|  
|Définition d'une source de données pour un modèle de rapport|Une fois que vous avez créé un projet de modèle de rapport, vous devez définir une source de données à partir de laquelle extraire les données d'entreprise. Il s’agit en général de la base de données du site Configuration Manager.|Pour plus d'informations, voir la section [Pour définir la source de données du modèle de rapport](#BKMK_DefineReportModelDataSource) de cette rubrique.|  
|Définition d'une vue de source de données pour un modèle de rapport|Après avoir défini les sources de données utilisées dans le projet de modèle de rapport, la prochaine étape consiste à définir une vue de source de données pour le projet. Une vue de source de données est un modèle de données logique basé sur une ou plusieurs sources de données. Les vues de source de données incluent l'accès aux objets physiques (tableaux et vues) contenus dans les sources de données sous-jacentes. SQL Server Reporting Services génère le modèle de rapport à partir de la vue de source de données.<br /><br /> Les vues de la source de données simplifient le processus de conception du modèle en mettant à votre disposition une représentation efficace des données spécifiées. Sans modifier la source de données sous-jacente, vous pouvez renommer les tables et les champs et ajouter l'ensemble des champs et des tables dérivées à une vue de source de données. Pour obtenir un modèle efficace, ajoutez ces tables uniquement à la vue de source de données à utiliser.|Pour plus d'informations, voir la section [Pour définir la vue de la source de données du modèle de rapport](#BKMK_DefineReportModelDataSourceView) de cette rubrique.|  
|Créer un modèle de rapport|Un modèle de rapport correspond à une couche située en haut de la base de données et qui permet d'identifier les entités, les champs, ainsi que les rôles. Une fois publiés à l'aide de ces modèles, les utilisateurs du générateur de rapports peuvent développer des rapports sans avoir à connaître les structures de la base de données et sans devoir comprendre ou composer des requêtes. Les modèles contiennent des ensembles d'éléments de rapport associés et regroupés sous un nom convivial. Ils contiennent également des liens prédéfinis entre les éléments d'entreprise et des calculs prédéfinis. Vous pouvez définir des modèles à l'aide d'un langage XML appelé Semantic Model Definition Language (SMDL). L'extension de fichier du modèle de rapport est .smdl.|Pour plus d'informations, voir la section [Pour créer le modèle de rapport](#BKMK_CreateReportModel) de cette rubrique.|  
|Publication d'un modèle de rapport|Pour générer un rapport via le modèle créé, vous devez publier ce dernier dans un serveur de rapport. La source de données ainsi que la vue de source de données sont incluses dans le modèle lors de sa publication.|Pour plus d'informations, voir la section [Pour publier le modèle de rapport en vue de son utilisation dans SQL Server Reporting Services](#BKMK_PublishReportModel) de cette rubrique.|  
|Déployer le modèle de rapport sur Configuration Manager|Avant de pouvoir utiliser un modèle de rapport personnalisé dans l’**Assistant Création de rapport** pour créer un rapport basé sur un modèle, vous devez déployer le modèle de rapport sur Configuration Manager.|Pour plus d'informations, voir la section [Pour déployer le modèle de rapport personnalisé vers Configuration Manager](#BKMK_DeployReportModel) de cette rubrique.|  

## <a name="steps-for-creating-a-basic-report-model-in-sql-server-reporting-services"></a>Étapes de création d’un modèle de rapport basique dans SQL Server Reporting Services  
 Vous pouvez utiliser les procédures suivantes pour créer un modèle de rapport basique dont les utilisateurs de votre site peuvent se servir pour générer des rapports spécifiques basés sur des modèles et sur des données d’une seule vue de la base de données Configuration Manager. Créez un modèle de rapport destiné à l'auteur du rapport et présentant les informations relatives aux ordinateurs clients de votre site. Ces informations sont extraites de la vue **v_R_System** de la base de données Configuration Manager.  

 Vérifiez que SQL Server Business Intelligence Development Studio est installé sur l'ordinateur où vous effectuez ces procédures et que cet ordinateur dispose d'une connectivité réseau avec le serveur du point de Reporting Services. Pour plus de détails sur SQL Server Business Intelligence Development Studio, consultez la documentation de SQL Server 2008.  

###  <a name="BKMK_CreateReportModelProject"></a> To create the report model project  

1.  Sur le bureau, cliquez sur **Démarrer**, sur **Microsoft SQL Server 2008**, puis sur **SQL Server Business Intelligence Development Studio**.  

2.  Une fois **SQL Server Business Intelligence Development Studio** ouvert dans Microsoft Visual Studio, cliquez sur **Fichier**, **Nouveau**, puis sur **Projet**.  

3.  Dans la boîte de dialogue **Nouveau projet** , sélectionnez **Projet de modèle de rapport** dans la liste **Modèles** .  

4.  Dans la zone **Nom** , spécifiez un nom pour ce modèle de rapport. Dans cet exemple, tapez **Modèle_simple**.  

5.  Pour créer le projet de modèle de rapport, cliquez sur **OK**.  

6.  La solution **Modèle_simple** est créée et s'affiche dans l' **Explorateur de solutions**.  

    > [!NOTE]  
    >  Si le volet **Explorateur de solutions** n'est pas visible, cliquez sur **Afficher**, puis sur **Explorateur de solutions**.  

###  <a name="BKMK_DefineReportModelDataSource"></a> Pour définir la source de données du modèle de rapport  

1.  Dans le volet **Explorateur de solutions** de **SQL Server Business Intelligence Development Studio**, cliquez avec le bouton droit sur **Sources de données** pour sélectionner **Ajouter une nouvelle source de données**.  

2.  Sur la page **Bienvenue dans l'Assistant Sources de données** , cliquez sur **Suivant**.  

3.  Dans la page **Sélectionner la méthode de définition de la connexion** , vérifiez que l'option **Créer une source de données basée sur une connexion existante ou nouvelle** est sélectionnée, puis cliquez sur **Nouveau**.  

4.  Dans la boîte de dialogue **Connection Manager** , spécifiez les propriétés de connexion suivantes pour la source de données :  

    -   **Nom du serveur** : tapez le nom du serveur de base de données du site Configuration Manager ou sélectionnez-le dans la liste. Si vous utilisez une instance nommée au lieu de celle par défaut, tapez &lt;*serveur_base_de_données*>\\&lt;*nom_instance*>.  

    -   Sélectionnez **Utiliser l'authentification Windows**.  

    -   Dans la liste **Sélectionner ou entrer un nom de base de données**, sélectionnez le nom de la base de données du site Configuration Manager.  

5.  Pour vérifier la connexion à la base de données, cliquez sur **Tester la connexion**.  

6.  Si la connexion fonctionne, cliquez sur **OK** pour fermer la boîte de dialogue **Connection Manager** . Si ce n'est pas le cas, vérifiez que les informations entrées sont correctes, puis cliquez à nouveau sur **Tester la connexion** .  

7.  Sur la page **Sélectionner la méthode de définition de la connexion** , vérifiez que l'option **Créer une source de données basée sur une connexion existante ou nouvelle** est sélectionnée. Vérifiez également que la source de données que vous venez de spécifier est sélectionnée dans **Connexions de données**, puis cliquez sur **Suivant**.  

8.  Dans **Nom de la source de données**, spécifiez un nom pour la source de données et cliquez sur **Terminer**. Dans cet exemple, tapez **Modèle_simple**.  

9. La source de données **Modèle_simple.ds** s'affiche désormais dans l' **Explorateur de solutions** sous le nœud **Sources de données** .  

    > [!NOTE]  
    >  Pour modifier les propriétés d'une source de données existante, cliquez deux fois dessus dans le dossier **Sources de données** du panneau **Explorateur de solutions** pour afficher les propriétés de la source de données dans Concepteur de sources de données.  

###  <a name="BKMK_DefineReportModelDataSourceView"></a> Pour définir la vue de la source de données du modèle de rapport  

1.  Dans le volet **Explorateur de solutions**, cliquez avec le bouton droit sur **Vues des sources de données** pour sélectionner **Ajouter une nouvelle vue de source de données**.  

2.  Sur la page **Bienvenue dans l'Assistant Sources de données** , cliquez sur **Suivant**. La page **Sélectionner une source de données** s'affiche.  

3.  Dans la fenêtre **Sources de données relationnelles** , vérifiez que la source de données **Modèle_simple** est sélectionnée, puis cliquez sur **Suivant**.  

4.  Dans la page **Sélectionner des tables et des vues** , dans la liste **Objets disponibles** , sélectionnez la vue suivante à utiliser dans le modèle de rapport : **v_R_System (dbo)**.  

    > [!TIP]  
    >  Pour localiser aisément des vues dans la liste **Objets disponibles** , cliquez sur l'en-tête **Nom** situé en haut de la liste pour trier les objets par ordre alphabétique.  

5.  Après avoir sélectionné la vue, cliquez sur **>** pour transférer l'objet dans la liste **Objets inclus** .  

6.  Si la page **Correspondance de noms** s'affiche, acceptez les sélections par défaut, puis cliquez sur **Suivant**.  

7.  Lorsque vous avez sélectionné les objets dont vous avez besoin, cliquez sur **Suivant**, puis spécifiez un nom pour la vue de la source de données. Dans cet exemple, tapez **Modèle_simple**.  

8.  Cliquez sur **Terminer**. La vue de la source de données **Modèle_simple.dsv** s'affiche dans le dossier **Vues des sources de données** de l' **Explorateur de solutions**.  

###  <a name="BKMK_CreateReportModel"></a> To create the report model  

1.  Dans l' **Explorateur de solutions**, cliquez avec le bouton droit sur **Modèles de rapport** pour sélectionner **Ajouter un nouveau rapport de modèle**.  

2.  Sur la page **Bienvenue dans l'Assistant Modèle de rapport** , cliquez sur **Suivant**.  

3.  Sur la page **Sélectionner des vues de source de données** , sélectionnez la vue de source de données dans la liste **Vues de source de données disponibles** , puis cliquez sur **Suivant**. Dans cet exemple, sélectionnez **Modèle_simple.dsv**.  

4.  Sur la page **Sélectionner règles de génér. du modèle de rapport** , acceptez les valeurs par défaut, puis cliquez sur **Suivant**.  

5.  Sur la page **Collecter les statistiques du modèle** , vérifiez que **Mettre à jour les statistiques du modèle avant la production** est sélectionné, puis cliquez sur **Suivant**.  

6.  Sur la page **Fin de l'Assistant** , spécifiez un nom pour le modèle de rapport. Pour cet exemple, vérifiez que **Modèle_simple** s'affiche.  

7.  Pour terminer l'Assistant et créer le modèle de rapport, cliquez sur **Exécuter**.  

8.  Pour quitter l'assistant, cliquez sur **Terminer**. Le modèle de rapport est affiché dans la fenêtre de conception.  

###  <a name="BKMK_PublishReportModel"></a> Pour publier le modèle de rapport en vue de son utilisation dans SQL Server Reporting Services  

1.  Dans l' **Explorateur de solutions**, cliquez avec le bouton droit sur le modèle de rapport pour sélectionner **Déployer**. Pour cet exemple, le modèle de rapport est **Modèle_simple.smdl**.  

2.  Examinez l'état du déploiement dans l'angle inférieur gauche de la fenêtre **SQL Server Business Intelligence Development Studio** . Lorsque le déploiement est terminé, **Déploiement réussi** s'affiche. En cas d'échec du déploiement, la raison de l'échec s'affiche dans la fenêtre **Sortie** . Le nouveau modèle de rapport est maintenant disponible sur votre site Web SQL Server Reporting Services.  

3.  Cliquez sur **Fichier**, cliquez sur **Enregistrer tout**, puis fermez **SQL Server Business Intelligence Development Studio**.  

###  <a name="BKMK_DeployReportModel"></a> Pour déployer le modèle de rapport personnalisé vers Configuration Manager  

1. Localisez le dossier dans lequel vous avez créé le projet du modèle de rapport. Par exemple, %*PROFIL_UTILISATEUR*%\Documents\Visual Studio 2008\Projects\\*&lt;nom_projet\>.*  

2. Copiez les fichiers suivants du dossier du projet de modèle de rapport dans un dossier temporaire sur votre ordinateur :  

   -   *&lt;nom_modèle\>* **.dsv**  

   -   *&lt;nom_modèle\>* **.smdl**  

3. Ouvrez les fichiers mentionnés précédemment dans un éditeur de texte tel que le Bloc-notes.  

4. Dans le fichier _&lt;nom_modèle\>_**.dsv**, localisez la première ligne, qui est la suivante :  

    **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

    Modifiez cette ligne de la manière suivante :  

    **&lt;DataSourceView xmlns="<http://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView"\>**  

5. Copiez le contenu entier du fichier dans le Presse-papiers Windows.  

6. Fermez le fichier _&lt;nom_modèle\>_**.dsv**.  

7. Dans le fichier _&lt;nom_modèle\>_**.smdl**, localisez les trois dernières lignes, qui sont les suivantes :  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Collez le contenu du fichier _&lt;nom_modèle\>_**.dsv** juste avant la dernière ligne du fichier(**&lt;SemanticModel\>**).  

9. Enregistrez et fermez le fichier _&lt;nom_modèle\>_**.smdl**.  

10. Copiez le fichier _&lt;nom_modèle\>_**.smdl** dans le dossier *%programfiles%* \Microsoft Configuration Manager \AdminConsole\XmlStorage\Other du serveur de site Configuration Manager.  

    > [!IMPORTANT]  
    >  Après avoir copié le fichier du modèle de rapport sur le serveur de site Configuration Manager, vous devez quitter et redémarrer la console Configuration Manager avant de pouvoir utiliser le modèle de rapport à partir de l’**Assistant Création de rapport**.  

##  <a name="AdvancedReportModel"></a> Étapes de création d'un modèle de rapport avancé dans SQL Server Reporting Services  
 Vous pouvez utiliser les procédures suivantes pour créer un modèle de rapport avancé dont les utilisateurs de votre site peuvent se servir pour générer des rapports spécifiques basés sur des modèles et sur des données de plusieurs vues de la base de données Configuration Manager. Vous allez créer un modèle de rapport destiné à l'auteur du rapport et présentant les informations relatives aux ordinateurs clients et au système d'exploitation installé sur ces derniers. Ces informations sont extraites des vues suivantes de la base de données Configuration Manager :  

- **V_R_System** : contient des informations sur les ordinateurs découverts et sur le client Configuration Manager.  

- **V_GS_OPERATING_SYSTEM** : contient des informations sur le système d'exploitation installé sur l'ordinateur client.  

  Les éléments sélectionnés dans les vues précédentes vont être consolidés dans une liste de noms conviviaux, puis présentés à l'auteur du rapport dans le générateur de rapports afin de pouvoir être ajoutés dans des rapports particuliers.  

  Vérifiez que SQL Server Business Intelligence Development Studio est installé sur l'ordinateur où vous effectuez ces procédures et que cet ordinateur dispose d'une connectivité réseau avec le serveur du point de Reporting Services. Pour plus de détails sur SQL Server Business Intelligence Development Studio, consultez la documentation de SQL Server.  

#### <a name="to-create-the-report-model-project"></a>To create the report model project  

1.  Sur le bureau, cliquez sur **Démarrer**, sur **Microsoft SQL Server 2008**, puis sur **SQL Server Business Intelligence Development Studio**.  

2.  Une fois **SQL Server Business Intelligence Development Studio** ouvert dans Microsoft Visual Studio, cliquez sur **Fichier**, **Nouveau**, puis sur **Projet**.  

3.  Dans la boîte de dialogue **Nouveau projet** , sélectionnez **Projet de modèle de rapport** dans la liste **Modèles** .  

4.  Dans la zone **Nom** , spécifiez un nom pour ce modèle de rapport. Dans cet exemple, tapez **Modèle_avancé**.  

5.  Pour créer le projet de modèle de rapport, cliquez sur **OK**.  

6.  La solution **Modèle_avancé** est créée et s'affiche dans l' **Explorateur de solutions**.  

    > [!NOTE]  
    >  Si le volet **Explorateur de solutions** n'est pas visible, cliquez sur **Afficher**, puis sur **Explorateur de solutions**.  

#### <a name="to-define-the-data-source-for-the-report-model"></a>Pour définir la source de données du modèle de rapport  

1.  Dans le volet **Explorateur de solutions** de **SQL Server Business Intelligence Development Studio**, cliquez avec le bouton droit sur **Sources de données** pour sélectionner **Ajouter une nouvelle source de données**.  

2.  Sur la page **Bienvenue dans l'Assistant Sources de données** , cliquez sur **Suivant**.  

3.  Dans la page **Sélectionner la méthode de définition de la connexion** , vérifiez que l'option **Créer une source de données basée sur une connexion existante ou nouvelle** est sélectionnée, puis cliquez sur **Nouveau**.  

4.  Dans la boîte de dialogue **Connection Manager** , spécifiez les propriétés de connexion suivantes pour la source de données :  

    -   **Nom du serveur** : tapez le nom du serveur de base de données du site Configuration Manager ou sélectionnez-le dans la liste. Si vous utilisez une instance nommée au lieu de celle par défaut, tapez &lt;*serveur_base_de_données*>\\&lt;*nom_instance*>.  

    -   Sélectionnez **Utiliser l'authentification Windows**.  

    -   Dans la liste **Sélectionner ou entrer un nom de base de données**, sélectionnez le nom de la base de données du site Configuration Manager.  

5.  Pour vérifier la connexion à la base de données, cliquez sur **Tester la connexion**.  

6.  Si la connexion fonctionne, cliquez sur **OK** pour fermer la boîte de dialogue **Connection Manager** . Si ce n'est pas le cas, vérifiez que les informations entrées sont correctes, puis cliquez à nouveau sur **Tester la connexion** .  

7.  Sur la page **Sélectionner la méthode de définition de la connexion** , vérifiez que l'option **Créer une source de données basée sur une connexion existante ou nouvelle** est sélectionnée. Vérifiez également que la source de données, spécifiée dernièrement, est sélectionnée dans la liste **Connexions de données** , puis cliquez sur **Suivant**.  

8.  Dans **Nom de la source de données**, spécifiez un nom pour la source de données et cliquez sur **Terminer**. Dans cet exemple, tapez **Modèle_avancé**.  

9. La source de données **Modèle_avancé.ds** s'affiche désormais dans l' **Explorateur de solutions** sous le nœud **Sources de données** .  

    > [!NOTE]  
    >  Pour modifier les propriétés d'une source de données existante, cliquez deux fois dessus dans le dossier **Sources de données** du panneau **Explorateur de solutions** pour afficher les propriétés de la source de données dans Concepteur de sources de données.  

#### <a name="to-define-the-data-source-view-for-the-report-model"></a>Pour définir la vue de la source de données du modèle de rapport  

1. Dans le volet **Explorateur de solutions**, cliquez avec le bouton droit sur **Vues des sources de données** pour sélectionner **Ajouter une nouvelle vue de source de données**.  

2. Sur la page **Bienvenue dans l'Assistant Sources de données** , cliquez sur **Suivant**. La page **Sélectionner une source de données** s'affiche.  

3. Dans la fenêtre **Sources de données relationnelles** , vérifiez que la source de données **Modèle_avancé** est sélectionnée, puis cliquez sur **Suivant**.  

4. Sur la page **Sélectionner des tables et des vues** , dans la liste **Objets disponibles** , sélectionnez les vues suivantes à utiliser dans le modèle de rapport :  

   - **v_R_System (dbo)**  

   - **v_GS_OPERATING_SYSTEM (dbo)**  

     Une fois que vous avez sélectionné chaque vue, cliquez sur **>** pour transférer l'objet dans la liste **Objets inclus** .  

   > [!TIP]  
   >  Pour localiser aisément des vues dans la liste **Objets disponibles** , cliquez sur l'en-tête **Nom** situé en haut de la liste pour trier les objets par ordre alphabétique.  

5. Si la boîte de dialogue **Correspondance de noms** s'affiche, acceptez les sélections par défaut, puis cliquez sur **Suivant**.  

6. Lorsque vous avez sélectionné les objets dont vous avez besoin, cliquez sur **Suivant**, puis spécifiez un nom pour la vue de la source de données. Dans cet exemple, tapez **Modèle_avancé**.  

7. Cliquez sur **Terminer**. La vue de la source de données **Modèle_avancé.dsv** s'affiche dans le dossier **Vues des sources de données** de l' **Explorateur de solutions**.  

#### <a name="to-define-relationships-in-the-data-source-view"></a>Pour définir des liens dans la vue de source de données  

1.  Dans l' **Explorateur de solutions**, double-cliquez sur **Modèle_avancé.dsv** pour ouvrir la fenêtre de conception.  

2.  Cliquez avec le bouton droit sur la barre de titre de la fenêtre **v_R_System** pour sélectionner **Remplacer la table**, puis cliquez sur **Par la nouvelle requête nommée**.  

3.  Dans la boîte de dialogue **Créer une requête nommée** , cliquez sur l'icône **Ajouter une table** (généralement la dernière icône sur le ruban).  

4.  Dans la boîte de dialogue **Ajouter une table** , cliquez sur l'onglet **Vues** , sélectionnez **V_GS_OPERATING_SYSTEM** dans la liste, puis cliquez sur **Ajouter**.  

5.  Cliquez sur **Fermer** pour quitter la boîte de dialogue **Ajouter une table** .  

6.  Dans la boîte de dialogue **Créer une requête nommée** , indiquez ce qui suit :  

    -   **Nom :** spécifiez le nom de la requête. Dans cet exemple, tapez **Modèle_avancé**.  

    -   **Description :** spécifiez la description de la requête. Dans cet exemple, tapez **Exemple de modèle de rapport de Reporting Services**.  

7.  Dans la fenêtre **v_R_System** , sélectionnez les éléments suivants dans la liste d'objets à afficher dans le modèle de rapport :  

    -   **ResourceID**  

    -   **ResourceType**  

    -   **Active0**  

    -   **AD_Domain_Name0**  

    -   **AD_SiteName0**  

    -   **Client0**  

    -   **Client_Type0**  

    -   **Client_Version0**  

    -   **CPUType0**  

    -   **Hardware_ID0**  

    -   **User_Domain0**  

    -   **User_Name0**  

    -   **Netbios_Name0**  

    -   **Operating_System_Name_and0**  

8.  Dans la zone **v_GS_OPERATING_SYSTEM** , sélectionnez les éléments suivants dans la liste d'objets à afficher dans le modèle de rapport :  

    -   **ResourceID**  

    -   **Caption0**  

    -   **CountryCode0**  

    -   **CSDVersion0**  

    -   **Description0**  

    -   **InstallDate0**  

    -   **LastBootUpTime0**  

    -   **Locale0**  

    -   **Manufacturer0**  

    -   **Version0**  

    -   **WindowsDirectory0**  

9. Pour que les objets de ces vues s'affichent dans une même liste proposée à l'auteur du rapport, vous devez spécifier une relation entre les deux tables ou vues à l'aide d'une jointure. Pour joindre les deux vues, utilisez l'objet **ResourceID**qui apparaît dans chacune d'elles.  

10. Dans la fenêtre **v_R_System** , cliquez sur l'objet **ResourceID** et, tout en maintenant le bouton de la souris enfoncé, faites-le glisser vers l'objet **ResourceID** de la fenêtre **v_GS_OPERATING_SYSTEM** .  

11. Cliquez sur **OK**.  

12. La fenêtre **Modèle_avancé** , qui remplace la fenêtre **v_R_System** , contient tous les objets nécessaires pour le modèle de rapport des vues **v_R_System** et **v_GS_OPERATING_SYSTEM** . Vous pouvez à présent supprimer la fenêtre **v_GS_OPERATING_SYSTEM** dans le concepteur de vue de source de données. Cliquez avec le bouton droit sur la barre de titre de la fenêtre **v_GS_OPERATING_SYSTEM** pour sélectionner **Supprimer la table de la vue de source de données**. Dans la boîte de dialogue **Supprimer les objets** , cliquez sur **OK** pour confirmer la suppression.  

13. Cliquez sur **Fichier**, puis sur **Enregistrer tout**.  

#### <a name="to-create-the-report-model"></a>To create the report model  

1.  Dans l' **Explorateur de solutions**, cliquez avec le bouton droit sur **Modèles de rapport** pour sélectionner **Ajouter un nouveau rapport de modèle**.  

2.  Sur la page **Bienvenue dans l'Assistant Modèle de rapport** , cliquez sur **Suivant**.  

3.  Sur la page **Sélectionner une vue de source de données** , sélectionnez la vue de source de données dans la liste **Vues de source de données disponibles** , puis cliquez sur **Suivant**. Dans cet exemple, sélectionnez **Modèle_simple.dsv**.  

4.  Sur la page **Sélectionner règles de génér. du modèle de rapport** , ne modifiez pas les valeurs par défaut, puis cliquez sur **Suivant**.  

5.  Sur la page **Collecter les statistiques du modèle** , vérifiez que **Mettre à jour les statistiques du modèle avant la production** est sélectionné, puis cliquez sur **Suivant**.  

6.  Sur la page **Fin de l'Assistant** , spécifiez un nom pour le modèle de rapport. Pour cet exemple, vérifiez que **Modèle_avancé** s'affiche.  

7.  Pour terminer l'Assistant et créer le modèle de rapport, cliquez sur **Exécuter**.  

8.  Pour quitter l'assistant, cliquez sur **Terminer**.  

9. Le modèle de rapport est affiché dans la fenêtre de conception.  

#### <a name="to-modify-object-names-in-the-report-model"></a>Pour modifier des noms d'objet dans le modèle de rapport  

1.  Dans l' **Explorateur de solutions**, cliquez avec le bouton droit sur un modèle de rapport pour sélectionner **Concepteur de vue**. Dans cet exemple, sélectionnez **Modèle_avancé.smdl**.  

2.  Dans la vue de conception de modèle de rapport, cliquez avec le bouton droit sur le nom de n'importe quel objet pour sélectionner **Renommer**.  

3.  Entrez un nouveau nom pour l'objet sélectionné, puis appuyez sur Entrée. Par exemple, vous pouvez renommer l'objet **CSD_Version_0** en **Version du service pack Windows**.  

4.  Après avoir renommé les objets, cliquez sur **Fichier**, puis sur **Enregistrer tout**.  

#### <a name="to-publish-the-report-model-for-use-in-sql-server-reporting-services"></a>Pour publier le modèle de rapport en vue de son utilisation dans SQL Server Reporting Services  

1.  Dans l' **Explorateur de solutions**, cliquez avec le bouton droit sur **Modèle_avancé.smdl** pour sélectionner **Déployer**.  

2.  Examinez l'état du déploiement dans l'angle inférieur gauche de la fenêtre **SQL Server Business Intelligence Development Studio** . Lorsque le déploiement est terminé, **Déploiement réussi** s'affiche. En cas d'échec du déploiement, la raison de l'échec s'affiche dans la fenêtre **Sortie** . Le nouveau modèle de rapport est maintenant disponible sur votre site Web SQL Server Reporting Services.  

3.  Cliquez sur **Fichier**, cliquez sur **Enregistrer tout**, puis fermez **SQL Server Business Intelligence Development Studio**.  

#### <a name="to-deploy-the-custom-report-model-to-configuration-manager"></a>Pour déployer le modèle de rapport personnalisé vers Configuration Manager  

1. Localisez le dossier dans lequel vous avez créé le projet du modèle de rapport. Par exemple, %*PROFIL_UTILISATEUR*%\Documents\Visual Studio 2008\Projects\\*&lt;nom_projet\>.*  

2. Copiez les fichiers suivants du dossier du projet de modèle de rapport dans un dossier temporaire sur votre ordinateur :  

   -   *&lt;nom_modèle\>* **.dsv**  

   -   *&lt;nom_modèle\>* **.smdl**  

3. Ouvrez les fichiers mentionnés précédemment dans un éditeur de texte tel que le Bloc-notes.  

4. Dans le fichier _&lt;nom_modèle\>_**.dsv**, localisez la première ligne, qui est la suivante :  

    **&lt;DataSourceView xmlns="http://schemas.microsoft.com/analysisservices/2003/engine"\>**  

    Modifiez cette ligne de la manière suivante :  

    **&lt;DataSourceView xmlns="<http://schemas.microsoft.com/analysisservices/2003/engine>" xmlns:xsi="RelationalDataSourceView"\>**  

5. Copiez le contenu entier du fichier dans le Presse-papiers Windows.  

6. Fermez le fichier _&lt;nom_modèle\>_**.dsv**.  

7. Dans le fichier _&lt;nom_modèle\>_**.smdl**, localisez les trois dernières lignes, qui sont les suivantes :  

    `</Entity>`  

    `</Entities>`  

    `</SemanticModel>`  

8. Collez le contenu du fichier _&lt;nom_modèle\>_**.dsv** juste avant la dernière ligne du fichier(**&lt;SemanticModel\>**).  

9. Enregistrez et fermez le fichier _&lt;nom_modèle\>_**.smdl**.  

10. Copiez le fichier _&lt;nom_modèle\>_**.smdl** dans le dossier *%programfiles%* \Microsoft Configuration Manager\AdminConsole\XmlStorage\Other du serveur de site Configuration Manager.  

    > [!IMPORTANT]  
    >  Après avoir copié le fichier du modèle de rapport sur le serveur de site Configuration Manager, vous devez quitter et redémarrer la console Configuration Manager avant de pouvoir utiliser le modèle de rapport à partir de l’**Assistant Création de rapport**.  
