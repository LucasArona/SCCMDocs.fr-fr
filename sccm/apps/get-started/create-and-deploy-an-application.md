---
title: Créer et déployer une application
titleSuffix: Configuration Manager
description: Créez et déployez une application contenant une application métier et apprenez à gérer efficacement les applications.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3d34ec4abb712ce6797033a5ff490280611e1b02
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Créer et déployer une application avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique vous montre de façon concrète comment créer une application avec System Center Configuration Manager. Dans cet exemple, vous créez et vous déployez une application qui contient une application métier pour PC Windows appelée **Contoso.msi**. Cette application doit être installée sur tous les PC exécutant Windows 10 dans votre entreprise. Au fil des étapes, vous allez découvrir de nombreuses façons de gérer efficacement les applications.  

 Cette procédure est destinée à vous donner une vue d’ensemble de la manière de créer et déployer des applications Configuration Manager. Elle ne couvre cependant pas toutes les options de configuration, ni la façon de créer et déployer des applications pour d’autres plateformes.  

 Pour obtenir des détails spécifiques adaptés à chaque plateforme, consultez une des rubriques suivantes :  

-   [Créer des applications Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Créer des applications iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Créer des applications Android](../../apps/get-started/creating-android-applications.md)  
-   [Créer des applications Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Créer des applications pour ordinateurs Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Créer des applications serveur Linux et UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [Créer des applications Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md)


Si vous êtes déjà familiarisé avec les applications Configuration Manager, vous pouvez ignorer cette rubrique. Vous pouvez cependant consulter la rubrique [Créer des applications](../../apps/deploy-use/create-applications.md) pour découvrir toutes les options disponibles quand vous créez et déployez des applications.  

## <a name="before-you-start"></a>Avant de commencer  

Veillez à prendre connaissance des informations contenues dans la rubrique de [présentation de la gestion des applications](/sccm/apps/understand/introduction-to-application-management) de façon à préparer votre site à l’installation d’applications, et à comprendre la terminologie utilisée dans cette rubrique.  

 Vérifiez aussi que les fichiers d’installation de l’application **Contoso.msi** se trouvent à un emplacement accessible sur votre réseau.  

## <a name="create-the-configuration-manager-application"></a>Créer l’application Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Pour démarrer l’Assistant Création d’une application et créer l’application  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application**.  

4.  Dans la page **Général** de l’ **Assistant Création d’une application**, choisissez **Détecter automatiquement les informations de cette application à partir des fichiers d’installation**. Ceci permet de préremplir certaines informations dans l’Assistant avec les informations extraites du fichier d’installation .msi. Spécifiez ensuite les informations suivantes :  

    -   **Type** : choisissez **Windows Installer (fichier \*.msi)**.  

    -   **Emplacement** : entrez l’emplacement du fichier d’installation **Contoso.msi** (ou choisissez **Parcourir** pour le sélectionner). Notez que l’emplacement doit être spécifié sous la forme *\\\Serveur\Partage\Fichier* pour permettre à Configuration Manager de trouver les fichiers d’installation.  

    Le résultat doit ressembler à la capture d’écran suivante :  

    ![Page Général de l’Assistant Gestion des applications](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

5.  Choisissez **Suivant**. La page **Importer des informations** affiche des informations sur l’application et tous les fichiers associés qui ont été importés dans Configuration Manager. Quand vous avez terminé, choisissez à nouveau **Suivant**.  

6.  Dans la page **Informations générales**, vous pouvez fournir des informations complémentaires sur l’application pour faciliter le tri et sa localisation dans la console Configuration Manager.  

     De plus, le champ **Programme d’installation** vous permet de spécifier la ligne de commande complète à utiliser pour installer l’application sur les PC. Vous pouvez modifier ce champ pour ajouter vos propres propriétés (par exemple **/q** pour effectuer une installation sans assistance).  

    > [!TIP]  
    >  Certains champs de cette page de l’Assistant peuvent avoir été renseignés automatiquement au moment où vous avez importé les fichiers d’installation de l’application.  

     Le résultat doit ressembler à la capture d’écran suivante :  

     ![Page Informations générales de l’Assistant Gestion des applications](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

7.  Choisissez **Suivant**. Dans la page Résumé, vous pouvez vérifier vos paramètres d’application, puis terminer l’Assistant.  

 Vous avez fini de créer l’application. Pour la trouver, dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion d’applications**, puis choisissez **Applications**. Pour cet exemple, vous verrez ceci :  

 ![Graphique de l’application finale](/sccm/apps/get-started/media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examiner les propriétés de l’application et son type de déploiement  

Maintenant que vous avez créé une application, vous pouvez si nécessaire en ajuster les paramètres. Pour afficher les propriétés de l’application, sélectionnez l’application et, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

 La boîte de dialogue **Propriétés de l’application <Contoso\>** contient beaucoup d’éléments que vous pouvez configurer pour ajuster le comportement de l’application. Pour plus d’informations sur tous les paramètres configurables, consultez [Créer des applications](../../apps/deploy-use/create-applications.md). Pour cet exemple, vous allez seulement modifier quelques propriétés du type de déploiement de l’application.  

 Choisissez l’onglet **Types de déploiement** > Type de déploiement **Application Contoso** > **Modifier**.  

Une boîte de dialogue similaire à celle-ci s’affiche :  

![Page de propriétés de l’application dans la gestion des applications](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Ajouter une spécification pour le type de déploiement  
 Les spécifications indiquent les conditions devant être remplies pour qu’une application soit installée sur un appareil.  Vous pouvez choisir des spécifications prédéfinies ou créer les vôtres. Dans cet exemple, vous ajoutez une spécification pour que l’application soit installée uniquement sur les PC exécutant Windows 10.  

1.  Dans la page de propriétés du type de déploiement que vous venez d’ouvrir, choisissez l’onglet **Spécifications**.  

2.  Choisissez **Ajouter** pour ouvrir la boîte de dialogue **Créer une spécification**.  

3.  Dans la boîte de dialogue **Créer une spécification** , indiquez les informations suivantes :  

    -   **Catégorie** : **Appareil**  

    -   **Condition** : **Système d’exploitation**  

    -   **Type de règle** : **Valeur**  

    -   **Opérateur** : **L’un des**  

    -   Dans la liste des systèmes d’exploitation, sélectionnez **Windows 10**.  

    Vous obtenez une boîte de dialogue similaire à celle-ci :  

    ![Page de spécifications dans la gestion des applications](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  Choisissez **OK** pour fermer chaque page de propriétés que vous avez ouverte. Revenez ensuite à la liste **Applications** dans la console Configuration Manager.  

> [!TIP]  
>  Les spécifications peuvent permettre de réduire le nombre de regroupements Configuration Manager dont vous avez besoin. Comme vous venez de spécifier que l’application peut être installée uniquement sur les PC exécutant Windows 10, vous pouvez la déployer ultérieurement sur un regroupement contenant des ordinateurs qui exécutent de nombreux systèmes d’exploitation différents. L’application ne sera cependant installée que sur les PC Windows 10.  

## <a name="add-the-application-content-to-a-distribution-point"></a>Ajouter le contenu de l’application à un point de distribution  

Ensuite, pour déployer l’application sur des PC, vérifiez que le contenu de l’application est copié sur un point de distribution. Les PC accèdent au point de distribution pour installer l’application.  

> [!TIP]  
>  Pour plus d’informations sur les points de distribution et la gestion de contenu dans Configuration Manager, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels**, développez **Applications**. Ensuite, dans la liste des applications, sélectionnez l’**Application Contoso** que vous avez créée.  

3.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Distribuer du contenu**.  

4.  Dans la page **Général** de l’**Assistant Distribuer du contenu**, vérifiez que le nom de l’application est correct, puis choisissez **Suivant**.  

5.  Dans la page **Contenu**, vérifiez les informations qui seront copiées sur le point de distribution, puis choisissez **Suivant**.  

6.  Dans la page **Destination du contenu**, choisissez **Ajouter** pour sélectionner un ou plusieurs points de distribution ou bien des groupes de points de distribution sur lesquels le contenu de l’application doit être installé.  

7.  Effectuez toutes les étapes de l'Assistant.  

Vous pouvez vérifier que le contenu de l’application a bien été copié sur le point de distribution dans l’espace de travail **Surveillance**, sous **État de distribution** > **État du contenu**.  

## <a name="deploy-the-application"></a>Déployer l'application  

Ensuite, déployez l’application sur un regroupement de périphériques de votre hiérarchie. Dans cet exemple, vous déployez l’application sur le regroupement d’appareils **Tous les systèmes**.  

> [!TIP]  
>  N’oubliez pas que seuls les ordinateurs Windows 10 installeront l’application en raison des spécifications que vous avez sélectionnées précédemment.  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Dans la liste d’applications, sélectionnez l’application que vous avez créée précédemment (**Application Contoso**) puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer**.  

4.  Dans la page **Général** de l’**Assistant Déploiement logiciel**, choisissez **Parcourir** pour sélectionner le regroupement d’appareils **Tous les systèmes**.  

5.  Dans la page **Contenu**, vérifiez que le point de distribution à partir duquel les PC doivent installer l’application est bien sélectionné.  

6.  Dans la page **Paramètres de déploiement**, vérifiez que l’action de déploiement définie est **Installer** et que l’objectif du déploiement est **Obligatoire**.  

    > [!TIP]  
    >  En définissant l’objectif de déploiement sur **Obligatoire**, vous avez l’assurance que l’application est installée sur des PC conformes aux spécifications que vous avez définies. Si vous définissez la valeur **Disponible**, les utilisateurs peuvent installer l’application à la demande à partir du Centre logiciel.  

7.  Dans la page **Planification** , vous pouvez configurer à quel moment l’application sera installée. Pour cet exemple, sélectionnez **Dès que possible après le délai disponible**.  

8.  Dans la page **Expérience utilisateur**, choisissez **Suivant** pour accepter les valeurs par défaut.  

9. Effectuez toutes les étapes de l'Assistant.  

Utilisez les informations de la section **Surveiller l’application** ci-dessous pour voir l’état du déploiement de votre application.  

## <a name="monitor-the-application"></a>Surveiller l’application  
 Cette section vous explique comment examiner en un coup d’œil l’état du déploiement de l’application que vous venez de déployer.  

### <a name="to-review-the-deployment-status"></a>Pour consulter l’état du déploiement  

1.  Dans la console Configuration Manager, choisissez **Surveillance** > **Déploiements**.  

3.  Dans la liste des déploiements, sélectionnez **Application Contoso**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Afficher l’état**.  

5.  Sélectionnez un des onglets suivants pour en voir davantage sur l’état du déploiement de l’application :  

    -   **Opération réussie** : l’application a bien été installée sur les PC indiqués.  

    -   **En cours** : l’installation de l’application n’est pas encore terminée.  

    -   **Erreur** : une erreur s’est produite lors de l’installation de l’application sur les PC indiqués. Des informations complémentaires sur l’erreur sont aussi affichées.  

    -   **Config non satisfaite** : aucune tentative d’installation de l’application sur les appareils indiqués n’a été faite, car ils n’étaient pas conformes aux spécifications que vous avez configurées (en l’occurrence, ils n’exécutaient pas Windows 10).  

    -   **Inconnu** : Configuration Manager n’a pas pu signaler l’état du déploiement. Faites une nouvelle vérification ultérieurement.  

> [!TIP]  
>  Il existe plusieurs façons de surveiller les déploiements d’applications. Pour plus d’informations, consultez [Surveiller les applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

## <a name="end-user-experience"></a>Expérience de l’utilisateur final  

Les utilisateurs ayant des PC gérés par Configuration Manager et exécutant Windows 10 voient un message les invitant à installer l’application Contoso. L’application s’installe dès lors qu’ils acceptent l’installation.  
