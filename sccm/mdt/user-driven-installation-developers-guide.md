---
title: User Driven Installation
titleSuffix: Microsoft Deployment Toolkit
description: 'Guide du développeur pour l’installation UDI de Microsoft Deployment Toolkit 2013. '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: a2b3a3a0-7b81-4191-b1f9-c618e59347c3
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 434178f100c32a4188ecf5283066f9332035f761
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821083"
---
# <a name="user-driven-installation---developers-guide"></a>User Driven Installation - Guide du développeur
User Driven Installation (UDI) aide à simplifier le déploiement des systèmes d’exploitation clients Windows®, tels que Windows 8.1, sur les ordinateurs utilisant la fonctionnalité Déploiement de système d’exploitation (OSD) dans Microsoft® System Center 2012 R2 Configuration Manager. UDI fait partie de Microsoft Deployment Toolkit (MDT).  

## <a name="introduction"></a>Introduction  
 En règle générale, quand vous déployez des systèmes d’exploitation à l’aide de la fonctionnalité OSD, vous devez fournir toutes les informations nécessaires pour déployer le système d’exploitation. Les informations sont configurées dans des fichiers de configuration ou dans des bases de données (par exemple dans le fichier CustomSettings.ini ou la base de données MDT [MDT DB]). Vous devez fournir tous les paramètres de configuration avant de lancer le déploiement.  

 UDI fournit une interface pilotée par un Assistant qui vous permet de fournir des informations de configuration juste avant d’effectuer le déploiement. Ce comportement vous permet de créer des séquences de tâches OSD génériques, puis de fournir des informations propres à l’ordinateur au moment du déploiement, ce qui offre davantage de flexibilité durant le processus de déploiement.  

### <a name="target-audience"></a>Public visé  
 Ce guide est destiné aux développeurs qui créent des pages d’Assistant personnalisées pour UDI Wizard et des éditeurs de pages d’Assistant personnalisées pour UDI Wizard Designer. Ce guide part du principe que vous savez comment développer des applications Windows à l’aide de :  

-   C++, qui sert à créer des pages d’Assistant personnalisées.  

-   Microsoft .NET Framework, qui sert à créer des éditeurs de pages d’Assistant personnalisées.  

-   Windows Presentation Foundation (WPF), qui sert à créer des éditeurs de pages d’Assistant personnalisées.  

-   Langages pris en charge par WPF, tels que C#, C++ ou Microsoft Visual Basic® .NET, qui servent à créer des éditeurs de pages d’Assistant personnalisées.  

### <a name="about-this-guide"></a>À propos de ce guide  
 Ce guide fournit les informations de référence nécessaires pour vous aider à personnaliser UDI pour votre organisation. Ce guide ne traite pas d’opérations administratives ou d’exploitation, telles que l’installation de MDT (qui inclut UDI), la configuration d’UDI pour déployer des systèmes d’exploitation et des applications, ou l’exécution de déploiements à l’aide de UDI Wizard. Pour plus d’informations à ce sujet, consultez les rubriques UDI mentionnées dans le document *Utilisation de Microsoft Deployment Toolkit*, qui est fourni avec MDT.  

## <a name="udi-development-overview"></a>Vue d’ensemble du développement UDI  
 Le développement UDI vous permet d’étendre les fonctionnalités fournies par UDI. En général, le développement UDI est nécessaire quand vous souhaitez recueillir des informations supplémentaires consommées par le processus de déploiement UDI. Ces informations supplémentaires sont généralement enregistrées en tant que variables de séquence de tâches lues par les étapes de séquence de tâches dans une séquence de tâches UDI dans Configuration Manager.  

### <a name="udi-architecture"></a>Architecture UDI  
 L’objectif global du développement UDI consiste à créer des pages d’Assistant personnalisées qui peuvent être affichées dans UDI Wizard. En créant des pages d’Assistant personnalisées, vous pouvez étendre les fonctionnalités existantes d’UDI afin de répondre aux exigences techniques et professionnelles votre organisation. Une page d’Assistant personnalisée recueille des informations en plus de ou à la place des pages d’Assistant fournies par UDI.  

 La figure 1 illustre la relation entre UDI Wizard Designer et UDI Wizard.  

 ![UDIDevelopersGuide1](media/UDIDevelopersGuide1.jpg "UDIDevelopersGuide1")  
Figure 1. Relation entre UDI Wizard et UDI Wizard Designer  

 **Figure 1. Relation entre UDI Wizard et UDI Wizard Designer**  

 À un niveau conceptuel, le développement UDI inclut la création de :  

-   **Pages d’Assistant personnalisées**. Les pages d’Assistant sont affichées dans UDI Wizard et recueillent les informations nécessaires pour terminer le processus de déploiement. Vous créez des pages d’Assistant à l’aide de C++ dans Microsoft Visual Studio®. Les pages d’Assistant personnalisées sont implémentées en tant que DLL lues par UDI Wizard. Le SDK UDI contient un exemple montrant comment créer des pages d’Assistant personnalisées.  

-   **Éditeurs de pages d’Assistant personnalisées**. Vous utilisez des éditeurs de pages d’Assistant pour configurer le comportement de votre page d’Assistant personnalisée. Les éditeurs de pages d’Assistant personnalisées sont implémentés en tant que DLL lues par UDI Wizard Designer. Vous créez des éditeurs de pages d’Assistant à l’aide de :  

    -   [WPF](http://msdn.microsoft.com/library/ms754130.aspx) version 4.0  

    -   [Microsoft Prism](http://compositewpf.codeplex.com/) version 4.0  

    -   [Microsoft Unity Application Block](http://unity.codeplex.com/) (Unity) version 2.1  

     MDT inclut tous les assemblys nécessaires pour créer un éditeur de pages d’Assistant personnalisées utilisable dans UDI Wizard Designer. Le SDK UDI contient un exemple montrant comment créer des éditeurs de pages d’Assistant personnalisées.  

 En outre, UDI Wizard Designer consomme des fichiers de prise en charge de configuration d’éditeur de pages d’Assistant. Vous créez des fichiers de configuration d’éditeur de pages d’Assistant dans le cadre du processus de création de vos pages d’Assistant personnalisées et de vos éditeurs de pages d’Assistant personnalisées. UDI Wizard Designer crée les informations XML nécessaires dans le fichier de configuration UDI Wizard et le fichier .app correspondant.  

### <a name="preparing-the-udi-development-environment"></a>Préparation de l’environnement de développement UDI  
 Avant de commencer à créer vos propres pages d’Assistant personnalisées et éditeurs de pages d’Assistant, effectuez les étapes suivantes afin de préparer l’environnement de développement UDI :  

1.  Préparez les prérequis de l’environnement de développement UDI comme décrit dans [Préparer les prérequis de l’environnement de développement UDI](#PrepareUDIDevelopmentEnvironmentPrerequisites).  

2.  Configurez l’environnement de développement UDI comme décrit dans [Configurer l’environnement de développement UDI](#ConfigureUDIDevelopmentEnvironment).  

3.  Vérifiez que l’environnement de développement UDI est configuré correctement, comme décrit dans [Vérifier l’environnement de développement UDI](#VerifyUDIDeploymentEnvironment).  

####  <a name="PrepareUDIDevelopmentEnvironmentPrerequisites"></a> Préparer les prérequis de l’environnement de développement UDI  
 Pour préparer les prérequis de l’environnement de développement UDI, effectuez les étapes suivantes :  

1.  Préparez les prérequis matériels de l’environnement de développement UDI comme décrit dans [Préparer les prérequis matériels de l’environnement de développement UDI](#PrepareUDIDevelopmentEnvironmentHardwarePrerequisites).  

2.  Préparez les prérequis logiciels de l’environnement de développement UDI comme décrit dans [Préparer les prérequis logiciels de l’environnement de développement UDI](#PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites).  

#####  <a name="PrepareUDIDevelopmentEnvironmentHardwarePrerequisites"></a> Préparer les prérequis matériels de l’environnement de développement UDI  
 Les prérequis matériels de l’environnement de développement UDI sont identiques à ceux de l’édition de Microsoft Visual Studio 2010 que vous utilisez. Pour plus d’informations sur ces prérequis, consultez la configuration système requise pour chaque édition à la page [Produits Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

#####  <a name="PrepareUDIDevelopmentEnvironmentSoftwarePrerequisites"></a> Préparer les prérequis logiciels de l’environnement de développement UDI  
 Les prérequis logiciels de l’environnement de développement UDI sont les suivants :  

-   Tout système d’exploitation Windows pris en charge par Visual Studio 2010 (Windows 7 ou Windows Server® 2008 R2 est recommandé.)  

     Vous aurez besoin d’un système d’exploitation Windows qui prend en charge l’architecture de processeur pour laquelle vous souhaitez développer. Vous pouvez effectuer un développement UDI 32 bits et 64 bits à l’aide d’un système d’exploitation 64 bits. Sur un système d’exploitation 32 bits, vous ne pouvez effectuer qu’un développement UDI 32 bits. Pour cette raison, vous devez utiliser un système d’exploitation 64 bits.  

    > [!NOTE]
    >  Les versions IntelItanium (IA-64) du système d’exploitation Windows ne sont pas prises en charge pour les environnements de développement UDI.  

     Pour plus d’informations sur les systèmes d’exploitation pris en charge par Visual Studio 2010, consultez la configuration système requise pour chaque édition à la page [Produits Visual Studio 2010](http://www.microsoft.com/visualstudio/products/2010-editions).  

-   Microsoft .NET Framework version 4.0 (requis par Visual Studio 2010)  

-   Langage C++ (le langage utilisé pour étendre les pages UDI Wizard)  

-   Autres langages pris en charge par WPF, tels que C#, Visual Basic .NET ou C++/Common Language Infrastructure, qui sont utilisés pour étendre des éditeurs de pages d’Assistant d’UDI Wizard Designer  

    > [!NOTE]
    >  L’exemple de code source pour les éditeurs de pages d’Assistant d’UDI Wizard Designer est écrit en C#. Installez le langage C# si vous souhaitez utiliser l’exemple de code source.  

####  <a name="ConfigureUDIDevelopmentEnvironment"></a> Configurer l’environnement de développement UDI  
 Une fois les prérequis de l’environnement de développement UDI satisfaits, effectuez les étapes suivantes pour configurer l’environnement de développement UDI :  

1.  Installez Visual Studio 2010.  

     Veillez à installer C++ et tout autre langage pris en charge par WPF.  

    > [!NOTE]
    >  L’exemple de code source pour les pages d’éditeur d’UDI Wizard Designer est écrit en C#. Installez le langage C# si vous souhaitez utiliser l’exemple de code source.  

     Pour plus d’informations sur l’installation de Visual Studio 2010, consultez [Installation de Visual Studio](http://msdn.microsoft.com/library/e2h7fzkw.aspx).  

2.  Installez MDT.  

     Pour plus d’informations sur la façon d’installer MDT, consultez la section « Installation ou mise à niveau de MDT » dans le document MDT intitulé *Utilisation de Microsoft Deployment Toolkit*.  

3.  Dans l’Explorateur Windows, créez *dossier_local* (où *dossier_local* est un dossier situé sur un lecteur local sur l’ordinateur de développement).  

4.  Copiez le dossier *dossier_installation*\SDK dans *dossier_local* (où *dossier_installation* est le dossier dans lequel vous avez installé MDT et *dossier_local* est un dossier situé sur un lecteur local sur l’ordinateur de développement).  

     Vous copiez le dossier du SDK vers un autre emplacement car MDT est installé dans le dossier Program Files, dans lequel il est impossible d’écrire sans autorisations élevées. La copie du dossier du SDK vers un autre emplacement vous permet de modifier les fichiers dans le dossier SDK sans disposer d’autorisations élevées.  

5.  Copiez le dossier *dossier_installation*\Templates\Distribution\Tools dans *dossier_local* (où *dossier_installation* est le dossier dans lequel vous avez installé MDT et *dossier_local* est le dossier créé plus haut).  

6.  Renommez le dossier *dossier_local*\Tools en *dossier_local*\OSDSetupWizard (où *dossier_local* est le dossier créé plus haut).  

     Une fois terminé, la structure de dossiers sous *dossier_local* doit ressembler à la structure de dossiers illustrée dans la Figure 2 (où *dossier_local* est le dossier créé plus haut, et appelé *UDIDevelopment* dans la figure).  

     ![UDIDevelopersGuide2](media/UDIDevelopersGuide2.jpg "UDIDevelopersGuide2")  
Figure 2. Structure de dossiers pour le développement UDI  

     **Figure 2. Structure de dossiers pour le développement UDI**  

####  <a name="VerifyUDIDeploymentEnvironment"></a> Vérifier l’environnement de développement UDI  
 Une fois l’environnement de développement UDI configuré, vérifiez que la configuration est correcte en vous assurant que les exemples de projets sont générés correctement dans Visual Studio 2010.  

 Vérifiez que l’environnement de développement UDI est configuré correctement en déterminant si :  

-   Le projet SamplePage est généré correctement, comme décrit dans [Vérifier que le projet SamplePage est généré correctement](#VerifySamplePageProjectBuildsCorrectly).  

-   Le projet SampleEditor est généré correctement, comme décrit dans [Vérifier que le projet SampleEditor est généré correctement](#VerifySampleEditorProjectBuildsCorrectly).  

#####  <a name="VerifySamplePageProjectBuildsCorrectly"></a> Vérifier que le projet SamplePage est généré correctement  
 Le projet SamplePage fournit un exemple montrant comment créer une page d’Assistant personnalisée pour UDI Wizard. Pour plus d’informations sur le projet SamplePage, consultez [Examiner la solution Visual Studio SamplePage](#ReviewSamplePageVisualStudioSolution).  

 **Pour vérifier que le projet SamplePage est généré correctement**  

1.  Démarrez Visual Studio 2010.  

2.  Ouvrez le projet SamplePage.  

     Le projet SamplePage réside dans le dossier *dossier_local*\SDK\UDI\SamplePage (où *dossier_local* est le dossier créé plus haut).  

3.  Dans Visual Studio 2010, dans l’Explorateur de solutions, cliquez sur le projet SamplePage, puis sur **Propriétés**.  

     La boîte de dialogue **Pages de propriétés SamplePage** s’affiche.  

4.  Dans la boîte de dialogue **Pages de propriétés SamplePage**, accédez à Propriétés de configuration/Débogage.  

5.  Dans les propriétés de débogage, sous **Configuration**, sélectionnez **Toutes les configurations**.  

6.  Dans les propriétés de débogage, sous **Commande**, tapez **$(TargetDir)\OSDSetupWizard.exe.**  

7.  Dans les propriétés de débogage, sous **Répertoire de travail**, tapez **TARGETDIR**.  

8.  Dans la boîte de dialogue **Pages de propriétés SamplePage**, accédez à Propriétés de configuration/Événements de build/Événement post-build.  

9. Dans les propriétés d’événement post-build, sous **Ligne de commande**, tapez la commande suivante :  

    ```  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\*.*" "$(TargetDir)"  
    xcopy /y /i "$(ProjectDir)..\..\..\..\OSDSetupWizard\x86\en-us" "$(TargetDir)en-us"  
    copy /y "$(ProjectDir)..\..\..\..\OSDSetupWizard\OSDResults\Images\UDI_Wizard_Banner.bmp" "$(ProjectDir)header.bmp"  
    copy /y "$(ProjectDir)Config.xml" "$(TargetDir)”  
    copy /y "$(ProjectDir)header.bmp" "$(TargetDir)header.bmp"  
    ```  

10. Dans la boîte de dialogue **Pages de propriétés SamplePage**, cliquez sur **OK**.  

11. Enregistrez le projet.  

12. Dans le menu **Déboguer**, cliquez sur **Démarrer le débogage**.  

     La boîte de dialogue **Microsoft Visual Studio** signale que la source n’est plus à jour et vous invite à générer le projet.  

13. Dans la boîte de dialogue **Microsoft Visual Studio**, cliquez sur **Oui**.  

     La boîte de dialogue **Aucune information de débogage** s’affiche pour vous signaler qu’aucune information de débogage n’est disponible pour OSDSetupWizard.exe.  

14. Dans la boîte de dialogue **Aucune information de débogage**, cliquez sur **Oui**.  

     UDI Wizard s’ouvre et affiche la page d’Assistant personnalisée.  

15. Vérifiez que vous pouvez sélectionner une valeur dans **Choose your location**.  

16. Dans le formulaire **Wizard with sample page**, cliquez sur **Cancel**.  

     La boîte de dialogue **Cancel Wizard** s’affiche.  

17. Dans la boîte de dialogue **Cancel Wizard**, cliquez sur **Oui**.  

18. Fermez Visual Studio 2010.  

#####  <a name="VerifySampleEditorProjectBuildsCorrectly"></a> Vérifier que le projet SampleEditor est généré correctement  
 Le projet SampleEditor fournit un exemple montrant comment créer un éditeur de pages d’Assistant personnalisées pour UDI Wizard Designer. Pour plus d’informations sur le projet SampleEditor, consultez [Examiner la solution Visual Studio SamplePage](#ReviewSamplePageVisualStudioSolution).  

 **Pour vérifier que le projet SampleEditor est généré correctement**  

1.  Démarrez Visual Studio 2010.  

2.  Ouvrez le projet SampleEditor.  

     Le projet SampleEditor réside dans le dossier *dossier_local*\SDK\UDI\SampleEditor (où *dossier_local* est le dossier créé plus haut).  

3.  Dans Visual Studio 2010, dans l’Explorateur de solutions, sélectionnez le projet SampleEditor.  

4.  Dans le menu **Projet**, cliquez sur **Ajouter une référence**.  

     La boîte de dialogue **Ajouter une référence** s’ouvre.  

5.  Dans la boîte de dialogue **Ajouter une référence**, cliquez sur l’onglet **Parcourir**.  

6.  Sous l’onglet **Parcourir**, accédez à *dossier_installation*\Bin (où *dossier_installation* est le dossier dans lequel vous avez installé MDT). Sélectionnez les fichiers suivants, puis cliquez sur **OK** :  

    -   Microsoft.Enterprise.UDIDesigner.Common.dll  

    -   Microsoft.Enterprise.UDIDesigner.DataService.dll  

    -   Microsoft.Enterprise.UDIDesigner.Infrastructure.dll  

    -   Microsoft.Practices.Prism.dll  

    -   Microsoft.Practices.ServiceLocation.dll  

    -   Microsoft.Practices.Unity.dll  

    -   RibbonControlsLibrary.dll  

    > [!NOTE]
    >  Vous pouvez sélectionner plusieurs fichiers sous l’onglet **Parcourir** en maintenant enfoncée la touche Ctrl pendant que vous cliquez sur les fichiers.  

7.  Dans l’Explorateur de solutions, accédez à SampleEditor/Références.  

8.  Vérifiez qu’aucune référence ne présente un avertissement ou une erreur.  

9. Dans l’Explorateur de solutions, cliquez sur le projet SampleEditor, puis sur **Propriétés**.  

     La boîte de dialogue **Pages de propriétés SampleEditor** s’affiche.  

10. Dans la boîte de dialogue **Pages de propriétés SampleEditor**, cliquez sur l’onglet **Déboguer**.  

11. Sous l’onglet **Déboguer**, cliquez sur **Démarrer le programme externe**.  

12. Dans **Démarrer le programme externe**, tapez ***dossier_installation\Bin\UDIDesigner.exe*** (où *dossier_installation* est le dossier dans lequel vous avez installé MDT), puis cliquez sur **OK**.  

    > [!TIP]
    >  Vous pouvez cliquer sur le bouton de sélection (...) pour rechercher le dossier et sélectionner UDIDesigner.exe.  

13. Dans le menu **Fichier**, cliquez sur **Enregistrer tout**.  

14. Copiez le fichier *dossier_local* \SDK\SamplePage\SamplePage.dll.config dans le dossier *dossier_installation*\Bin\Config (où *dossier_local* est le dossier que vous avez créé sur l’ordinateur de développement plus tôt durant le processus de configuration et *dossier_installation* est le dossier dans lequel vous avez installé MDT).  

15. Dans Visual Studio 2010, dans le menu **Déboguer**, cliquez sur **Démarrer le débogage**.  

     UDI Wizard Designer démarre.  

16. Dans UDI Wizard Designer, sur le ruban, cliquez sur **Ouvrir**.  

     La boîte de dialogue **Ouvrir** s’affiche.  

17. Dans la boîte de dialogue **Ouvrir**, ouvrez le fichier *dossier_local*\SDK\SamplePage\SamplePage\Config.xml (où *dossier_local* est le dossier que vous avez créé sur l’ordinateur de développement plus tôt durant le processus de configuration).  

     Le fichier Config.xml s’ouvre et le [StageGroup](#StageGroup) personnalisé s’affiche dans le volet de détails.  

18. Dans le volet de détails, cliquez sur l’onglet **Configurer**.  

19. Passez en revue les informations de configuration pour la zone **Emplacement**, notamment :  

    -   Le bouton **Unlocked**, avec lequel vous activez ou désactivez la zone **Emplacement**.  

    -   La zone **Default value**, dans laquelle vous entrez une valeur par défaut à afficher dans la zone **Location**.  

    -   **Le nom complet convivial visible dans la page de récapitulatif**, dans laquelle vous entrez la légende pour les informations affichées dans la page **Summary**.  

    -   La zone de liste **Location**, qui comprend une liste d’emplacements possibles.  

20. Fermez UDI Wizard Designer.  

21. Fermez Visual Studio 2010.  

## <a name="reviewing-the-udi-sdk-examples"></a>Examen des exemples du SDK UDI  
 Avant de commencer le développement, passez en revue les exemples fournis dans le SDK UDI. Utilisez les informations contenues dans ce guide et le code source dans les exemples pour vous aider à créer vos propres pages d’Assistant personnalisées UDI et éditeurs de pages d’Assistant.  

 Passez en revue les exemples du SDK UDI en examinant :  

-   Le contenu du dossier du SDK que vous avez copié précédemment lors du processus d’installation, comme décrit dans [Examiner le contenu du dossier de SDK](#ReviewContentsofSDKFolder).  

-   L’exemple de page UDI Wizard personnalisée comme décrit dans [Examiner la solution Visual Studio SamplePage](#ReviewSamplePageVisualStudioSolution).  

-   L’exemple de page UDI Wizard personnalisée comme décrit dans [Examiner la solution Visual Studio SampleEditor](#ReviewSampleEditorVisualStudioSolution).  

###  <a name="ReviewContentsofSDKFolder"></a> Examiner le contenu du dossier de SDK  
 Lors de la configuration de l’environnement de développement UDI, vous avez copié le dossier de SDK à partir du dossier dans lequel vous avez installé MDT vers un autre dossier que vous avez créé. Le Tableau 1 répertorie les dossiers immédiatement sous le dossier du SDK et fournit une brève description de chacun d’eux.  

### <a name="table-1-folders-in-the-udi-sdk"></a>Tableau 1. Dossiers dans le SDK UDI  

|**Dossier**|**Ce dossier contient**|  
|-|-|  
|Includes|Les fichiers d’en-tête C++ nécessaires pour créer des pages d’Assistant personnalisées pour UDI Wizard|  
|Libs|Les fichiers de bibliothèque C++ qui seront liés à votre page personnalisée. Il existe des versions 32 bits et 64 bits des bibliothèques de liens statiques. **Remarque :** les versions Itanium des bibliothèques (IA-64) ne sont pas disponibles.|  
|SampleEditor|Un projet Visual Studio pour la création d’un éditeur personnalisé permettant de modifier la page SamplePage dans UDI Wizard Designer, qui est écrit en C#.|  
|SamplePage|Un projet Visual Studio pour la création d’une page UDI Wizard personnalisée, qui est écrit en Visual C++.|  

###  <a name="ReviewSamplePageVisualStudioSolution"></a> Examiner la solution Visual Studio SamplePage  
 Avant de commencer à créer vos pages d’Assistant personnalisées et éditeurs de pages d’Assistant, effectuez les tâches suivantes afin de préparer l’environnement de développement UDI :  

-   Passez en revue les étapes du cycle de vie d’une page UDI Wizard, comme décrit dans [Examiner le cycle de vie d’une page d’Assistant](#ReviewWizardPageLifeCycle).  

-   Passez en revue la solution Visual Studio pour l’exemple SamplePage dans le SDK UDI comme décrit dans [Examiner l’exemple SamplePage](#ReviewSamplePageExample).  

####  <a name="ReviewWizardPageLifeCycle"></a> Examiner le cycle de vie d’une page d’Assistant  
 Une page UDI Wizard a des méthodes qui correspondent à chaque étape (ou phase) du cycle de vie de la page. Dans le cadre de la création de votre page d’Assistant personnalisée, vous devez substituer ces méthodes dans votre code. Le Tableau 2 répertorie les méthodes que vous devez substituer, et fournit une brève description de chaque méthode, notamment quand utiliser la méthode durant le cycle de vie de la page d’Assistant.  

### <a name="table-2-methods-in-a-wizard-page-life-cycle"></a>Tableau 2. Méthodes dans le cycle de vie d’une page d’Assistant  

|**Méthode**|**Description**|  
|-|-|  
|**OnWindowCreated**|Cette méthode est appelée une seule fois, après la création de la fenêtre de la page.<br /><br /> Pour cette méthode, écrivez du code qui initialise la page pour la première fois et ne doit être exécuté qu’une seule fois. Par exemple, utilisez cette méthode pour initialiser des champs ou pour lire des informations de configuration à partir des éléments **Setter** dans le fichier de configuration UDI Wizard.|  
|**OnWindowShown**|Cette méthode est appelée chaque fois que la page est affichée dans UDI Wizard. Elle est appelée la première fois que la page est affichée et chaque fois que vous y accédez en cliquant sur **Suivant** ou **Précédent** dans l’Assistant.<br /><br /> Pour cette méthode, écrivez du code qui prépare la page à être affichée, par exemple pour la lecture de variables en mémoire, de variables de séquence de tâches ou de variables d’environnement, puis la mise à jour de la page en fonction des modifications apportées à ces variables.|  
|**OnCommonControlEvent**|Cette méthode peut être appelée chaque fois que la page d’Assistant est affichée et reçoit un message WM_NOTIFY à partir d’un enfant (en règle générale des contrôles communs).<br /><br /> Pour cette méthode, écrivez du code qui gère WM_NOTIFY en fonction du message de notification. Par exemple, vous souhaiterez peut-être répondre à des événements à partir d’un contrôle commun, comme des événements de clic ou de double-clic pour un contrôle **TreeView**.|  
|**OnUnhandledEvent**|Cette méthode est appelée chaque fois qu’un message de fenêtre non géré se produit pour votre page d’Assistant. Elle offre la possibilité d’intercepter et de gérer ces messages de fenêtre qui ne seraient normalement pas gérés.<br /><br /> Pour cette méthode, écrivez du code qui gère les messages de fenêtre applicables à votre page d’Assistant. En règle générale, vous n’aurez pas besoin de substituer cette méthode.|  
|**OnNextClicked**|Cette méthode est appelée quand vous cliquez sur **Suivant** dans l’Assistant.<br /><br /> Pour cette méthode, écrivez du code qui effectue les actions nécessaires avant de passer à la page suivante de l’Assistant, par exemple exécuter une validation qui peut prendre un certain temps. Si la validation échoue, vous pouvez annuler la demande **Suivant** et afficher un message.|  
|**OnWindowHidden**|Cette méthode est appelée chaque fois que la page est masquée quand la page précédente ou suivante de l’Assistant est affichée.<br /><br /> Pour cette méthode, écrivez du code qui effectue une action avant que la page soit masquée, avant qu’une autre page soit affichée. En règle générale, vous n’aurez pas besoin de substituer cette méthode.|  

####  <a name="ReviewSamplePageExample"></a> Examiner l’exemple SamplePage  
 Passez en revue l’exemple SamplePage à l’aide de la liste suivante, qui représente la séquence d’événements durant le cycle de vie de page d’Assistant de l’exemple SamplePage :  

1.  UDI Wizard, OSDSetupWizard.exe, lit les informations de configuration à partir du fichier de configuration UDI Wizard dans l’exemple (le fichier Config.xml), comme décrit dans [Étape 1 : UDI Wizard (OSDSetupWizard.exe) lit le fichier Config.xml](#UDIWizardReadstheConfigFile).  

2.  UDI Wizard charge les DLL nécessaires pour chaque page d’Assistant répertoriée dans le fichier de configuration UDI Wizard comme indiqué dans [Étape 2 : UDI Wizard charge la DLL pour la page d’Assistant personnalisée](#UDIWizardLoadstheDLLforCustomWizardPage).  

3.  UDI Wizard affiche la page d’Assistant personnalisée et autorise l’interaction de contrôle souhaitée comme décrit dans [Étape 3 : UDI Wizard affiche la page d’Assistant personnalisée](#UDIWizardDisplaysCustomWizardPage).  

4.  Quand la page d’Assistant personnalisée a recueilli les informations, effectuez toutes les tâches nécessaires avant de cliquer sur **Suivant** afin de passer à l’Assistant suivant comme décrit dans [Étape 4 : L’utilisateur clique sur le bouton Suivant dans la page d’Assistant personnalisée](#TheNextButtonisClickedinCustomWizardPage).  

#####  <a name="UDIWizardReadstheConfigFile"></a> Étape 1 : UDI Wizard (OSDSetupWizard.exe) lit le fichier Config.xml  
 Quand UDI Wizard (OSDSetupWizard.exe) démarre, par défaut il lit le fichier de configuration UDI Wizard, à savoir UDIWizard_Config.xml, le fichier de configuration principal pour UDI Wizard.  

> [!NOTE]
>  L’exemple utilise le fichier Config.xml comme fichier de configuration. Dans MDT, le fichier de configuration par défaut est le fichier UDIWizard_Config.xml, qui réside dans le dossier Scripts dans le package de fichiers MDT pour la configuration.  

 Vous pouvez remplacer le fichier de configuration par défaut utilisé par UDI Wizard en modifiant l’étape de séquence de tâches UDI Wizard de manière à utiliser le paramètre **/definition**. Pour plus d’informations sur le remplacement du fichier de configuration par défaut utilisé par UDI Wizard, consultez « Remplacer le fichier de configuration par défaut utilisé par UDI Wizard ».  

 Les éléments de niveau supérieur dans le fichier Config.xml sont les suivants :  

-   Élément [DLL](#DLLs)  

-   Élément [Style](#Style)  

-   Élément [Pages](#Pages)  

-   Élément [StageGroups](#StageGroups)  

 Pour plus d’informations sur le schéma du fichier de configuration UDI Wizard et sur chacun de ces éléments, consultez [Référence du schéma de fichier de configuration UDI Wizard](#UDIWizardConfigurationFileSchemaReference).  

 UDI Wizard analyse l’élément **DLLs** à la recherche des fichiers .dll à charger. Dans l’exemple, deux fichiers .dll sont répertoriés : SamplePage.dll et SharedPages.dll. Ces fichiers .dll doivent résider dans le même dossier que les outils OSDSetupWizard.exe : le dossier \\*plateforme* (où *plateforme* est x86 pour la version 32 bits ou x64 pour la version 64 bits).  

 UDI Wizard analyse l’élément **Pages** à la recherche des pages qui sont définies. Dans l’exemple, deux pages sont définies : **Custom** et **SummaryPage**. L’attribut **Type** de l’élément **Page** est défini dans le fichier PageClassIDs.h et identifie de façon unique le type de votre page personnalisée.  

 Dans l’exemple, le type défini est **Microsoft.SamplePage.LocationPage**. Pour votre page personnalisée, substituez les éléments suivants afin d’éviter tout conflit avec d’autres pages que vous pourriez créer ultérieurement :  

-   Le nom de votre organisation à la place de **Microsoft**  

-   Le nom de votre projet à la place de **SamplePage**  

-   Le nom de votre page d’Assistant personnalisée à la place de **LocationPage**  

#####  <a name="UDIWizardLoadstheDLLforCustomWizardPage"></a> Étape 2 : UDI Wizard charge la DLL pour la page d’Assistant personnalisée  
 Quand UDI Wizard charge votre DLL, il appelle la fonction **RegisterFactories**, qui doit être implémentée dans votre fichier .dll. Dans l’exemple, cette fonction est implémentée dans le fichier dllmain.ccp. Chaque page d’Assistant que vous créez doit implémenter la fonction **RegisterFactories**.  

 La fonction **RegisterFactories** sert à inscrire la classe de fabrique de votre page d’Assistant dans le registre de fabrique de classe pour UDI Wizard. Les *fabriques de classe* sont des classes qui peuvent créer une instance d’une autre classe. La fonction **RegisterFactories** crée une instance d’une classe de fabrique et passe cette classe au registre de fabrique de classe pour UDI Wizard, ce qui rend cette classe de fabrique accessible à l’Assistant. UDI Wizard recherche une classe de fabrique inscrite avec un ID qui correspond à l’attribut **Type** de l’élément **Page** de la page d’Assistant personnalisée.  

 Dans l’exemple, l’ID est défini en tant que **ID_Location** dans le fichier PageClassIds.h en tant que **Microsoft.SamplePage.LocationPage**, qui correspond à l’attribut **Type** pour l’élément  **Page** dans le fichier Config.xml. **ID_Location** est passé comme paramètre dans la fonction **RegisterFactories** implémentée dans le fichier dllmain.ccp.  

 Vous pouvez créer une fonction à l’aide du modèle de fonction Register_*nom* pour simplifier la création d’une instance de fabrique et inscrire la nouvelle instance. La valeur **nom** fournie à l’aide du modèle de fonction Register doit implémenter l’interface **iClassFactory**. La [classe ClassFactoryImpl](#ClassFactoryImplClass) gère la plupart des détails pour l’implémentation d’une fabrique de classe.  

 Vous pouvez également utiliser la fonction **RegisterFactories** pour inscrire des types de tâches et des types de validateurs. Pour plus d'informations, consultez :  

-   [Création de tâches UDI personnalisées](#CreatingCustomUDITasks)  

-   [Création de validateurs UDI personnalisés](#CreatingCustomUDIValidators)  

> [!NOTE]
>  L’exemple contient et inscrit une seule page d’Assistant personnalisée. Il n’inclut pas de tâches ou de validateurs personnalisés, et n’en inscrit donc pas.  

#####  <a name="UDIWizardDisplaysCustomWizardPage"></a> Étape 3 : UDI Wizard affiche la page d’Assistant personnalisée  
 La page d’Assistant personnalisée dans l’exemple est définie dans le fichier LocationPage.cpp. Les pages d’Assistant sont dérivées de classes de modèle qui fournissent la plupart des fonctionnalités qu’offre une page. Toutes les pages d’Assistant doivent dériver de la [classe de modèle WizardPageImpl](#WizardPageImplTemplateClass), qui implémente l’[interface IWizardPage](#IWizardPageInterface). Chaque page d’Assistant peut implémenter d’autres classes de modèle facultatives et les interfaces correspondantes en fonction des besoins de la page.  

 La [classe de modèle WizardPageImpl](#WizardPageImplTemplateClass) a plusieurs interfaces utiles qui peuvent vous aider à écrire des pages d’Assistant personnalisées. Implémentez la [classe de modèle WizardPageImpl](#WizardPageImplTemplateClass) en tant que classe de base pour votre page d’Assistant personnalisée.  

 Pour obtenir :  

-   La liste des classes de modèle disponibles pour les pages d’Assistant, consultez [Classes d’assistance de page d’Assistant](#WizardPageHelperClasses).  

-   La liste des interfaces disponibles pour les classes de modèle de page d’Assistant, consultez [Interfaces de page d’Assistant](#WizardPageInterfaces).  

 La page d’Assistant personnalisée dans l’exemple est dérivée de la [classe de modèle WizardPageImpl](#WizardPageImplTemplateClass) et implémente l’[interface IWizardPage](#IWizardPageInterface). Elle implémente aussi l’interface **IFieldCallback**. Ces deux interfaces sont implémentées dans le fichier LocationPage.cpp.  

 L’exemple de page d’Assistant personnalisée substitue les méthodes suivantes :  

-   **OnWindowCreated**. La méthode **OnWindowCreated** dans l’exemple de page d’Assistant appelle les méthodes suivantes :  

    -   [AddField](#AddField). Cette méthode associe le contrôle de zone **IDC_COMBO_LOCATION** dans la ressource **IDD_LOCATION_PAGE** à l’élément [Data](#Data) nommé **Location** dans le fichier Config.xml.  

         Outre la méthode **AddField**, vous pouvez utiliser les méthodes [AddRadioGroup](#AddRadioGroup) et [AddToGroup](#AddToGroup) pour prendre en charge d’autres contrôles et comportements.  

        > [!NOTE]
        >  Veillez à appeler la méthode [AddField](#AddField), [AddRadioGroup](#AddRadioGroup) ou [AddToGroup](#AddToGroup) avant d’appeler la méthode [InitFields](#InitFields).  

    -   [InitFields](#InitFields). Utilisez cette méthode pour initialiser les champs (contrôles) que vous avez ajoutés au formulaire. Le pointeur de la page est un paramètre. Dans l’exemple, le pointeur **this**, qui fait référence à la page actuelle, est passé.  

        > [!NOTE]
        >  Pour prendre en charge l’utilisation du pointeur **this**, vous devez implémenter l’interface **IFieldCallback** en plus des interfaces prises en charge par la [classe de modèle WizardPageImpl](#WizardPageImplTemplateClass).  

         L’interface **IFieldCallback** appelle la méthode **SetFieldDefault**, qui sert à définir les valeurs par défaut des contrôles autres que les zones de texte et les cases à cocher. Dans l’exemple, la méthode **SetFieldDefault** définit l’index initial du contrôle de zone de liste déroulante en fonction de la valeur par défaut spécifiée dans l’élément **Default** pour l’élément [Field](#Field) dans le fichier Config.xml.  

     La méthode **OnWindowCreated** configure le contrôleur de formulaire à l’aide de l’[interface IFormController](#IFormController-Interface). Pour plus d’informations sur la configuration du contrôleur de formulaire, consultez [Configuration du formulaire](#SettingUptheForm).  

-   **InitLocations**. Cette méthode remplit la zone de liste déroulante à partir de la liste des emplacements dans le fichier Config.xml. L’élément [Data](#Data) et les éléments enfants [DataItem](#DataItem) dans le fichier Confg.xml fournissent la liste des valeurs possibles.  

-   **OnNextClicked**. Cette méthode effectue les tâches suivantes :  

    -   Elle met à jour la variable de séquence de tâches **TSLocation** avec la valeur sélectionnée dans la zone de liste déroulante à l’aide de la méthode **SaveFields**.  

    -   Elle ajoute des informations qui seront affichées dans la page **Summary** à l’aide de la méthode **SaveFields**.  

#####  <a name="TheNextButtonisClickedinCustomWizardPage"></a> Étape 4 : L’utilisateur clique sur le bouton Suivant dans la page d’Assistant personnalisée  
 Quand l’utilisateur a renseigné les champs dans la page d’Assistant personnalisée, il clique sur **Suivant**, ce qui appelle la méthode **OnNextClicked**. La méthode **OnNextClicked** effectue les tâches nécessaires, telles que l’enregistrement des modifications de configuration apportées à la page d’Assistant personnalisée, avant de passer à la page suivante.  

 Pour l’exemple de page d’Assistant personnalisée, la substitution de la méthode **OnNextClicked** est implémentée dans le fichier LocationPage.ccp. Dans la méthode **OnNextClicked** dans l’exemple de page d’Assistant personnalisée, les méthodes suivantes sont appelées :  

1.  [InitSection](#InitSection). Cette méthode initialise l’en-tête (légende) pour les données de synthèse affichées dans la page **Summary**. En règle générale, vous pouvez définir cette valeur à l’aide de la fonction **DisplayName()**. Les données associées à cette légende sont enregistrées à l’aide de la méthode [SaveFields](#SaveFields).  

2.  [SaveFields](#SaveFields). Cette méthode enregistre les valeurs de champs dans les variables de séquence de tâches et dans les données affichées dans la page **Summary**.  

###  <a name="ReviewSampleEditorVisualStudioSolution"></a> Examiner la solution Visual Studio SampleEditor  
 Avant de commencer à créer vos propres pages d’Assistant personnalisées et éditeurs de pages d’Assistant, effectuez les étapes suivantes afin de préparer l’environnement de développement UDI :  

-   Passez en revue l’architecture d’UDI Wizard Designer comme décrit dans [Examiner l’architecture d’UDI Wizard Designer](#ReviewUDIWizardDesignerArchitecture).  

-   Passez en revue les composants d’une page UDI Wizard qui peut être personnalisée à l’aide du fichier de configuration UDI Wizard comme décrit dans [Examiner les composants configurables d’une page UDI Wizard](#ReviewConfigurableComponentsofUDIWizardPage).  

-   Examinez l’exemple EditorPage fourni dans le SDK UDI comme décrit dans [Examiner l’exemple EditorPage](#ReviewEditorPageExample).  

####  <a name="ReviewUDIWizardDesignerArchitecture"></a> Examiner l’architecture d’UDI Wizard Designer  
 UDI Wizard Designer a été développé à l’aide de WPF, Prism et Unity. UDI Designer sert à modifier le fichier de configuration UDI Wizard (UDIWizard_Config.xml), qui est lu par UDI Wizard (OSDSetupWizard.exe) au moment de l’exécution. L’élément [Pages](#Pages) dans le fichier de configuration UDI Wizard contient une liste de pages qui a un élément [Page](#Page) distinct pour chaque page d’Assistant.  

 Quand vous modifiez les paramètres de configuration d’une page d’Assistant, UDI Wizard Designer charge l’éditeur de page personnalisée qui correspond au type de page d’Assistant. Les éditeurs de pages d’Assistant personnalisées sont développées en tant que contrôles utilisateur WPF. Les pages des éditeurs de pages d’Assistant personnalisées utilisent le modèle de conception MVVM [Model–View–ViewModel](http://msdn.microsoft.com/magazine/dd419663.aspx) pour WPF.  

 Le modèle de conception MVVM permet de séparer l’interface utilisateur (présentation) des données présentées. Les données sont une façade par-dessus l’élément [Page](#Page) dans le fichier de configuration UDI Wizard (le fichier Config.xml dans l’exemple), qui est accessible à l’aide de la propriété [CurrentPage](#CurrentPage) de l’interface [IDataService](#IDataService).  

 UDI Wizard Designer utilise le **DependencyAttribute** pour obtenir l’accès à la classe **DataService** en fonction du framework d’injection de dépendance dans Unity. Pour plus d’informations sur le framework d’injection de dépendance dans Unity, consultez [Inject Some Life into Your Applications—Getting to Know the Unity Application Block (Insufflez de la vie dans vos applications — Introduction à Unity Application Block](http://msdn.microsoft.com/library/ff650806.aspx).  

####  <a name="ReviewConfigurableComponentsofUDIWizardPage"></a> Examiner les composants configurables d’une page UDI Wizard  
 Quand vous créez votre page d’Assistant personnalisée, il est possible que certains paramètres de configuration soient définis dans le code et ne puissent pas être modifiés une fois la page compilée. En revanche, pour d’autres paramètres de configuration vous devrez autoriser la modification de ces paramètres de configuration à l’aide d’UDI Wizard Designer.  

 En règle générale, les paramètres de configuration que vous souhaitez configurer à l’aide d’UDI Wizard Designer sont enregistrés dans le fichier de configuration UDI Wizard (le fichier Config.xml dans l’exemple). Toutefois, vous pouvez également créer votre propre fichier de configuration distinct, si nécessaire. Le fichier UDIWizard_Config.xml.app constitue un exemple d’utilisation d’un fichier de configuration distinct. Il est utilisé par la tâche **Découverte d’application** et par le type de page d’Assistant **ApplicationPage**.  

 Voici une liste des paramètres de configuration courants que vous pouvez gérer à l’aide d’UDI Wizard Designer :  

-   **Field**. Utilisez des champs pour permettre aux utilisateurs de fournir une entrée. Les champs apparaissent en tant qu’éléments [Field](#Field) dans le fichier de configuration UDI Wizard (UDIWizard_Config.xml), qui contient les paramètres de configuration pour chaque champ. L’éditeur de page d’Assistant correspondant doit fournir une méthode pour modifier les paramètres de configuration de champ du champ à l’aide de [FieldElementControl](#FieldElementControl).  

-   **Propriétés**. Les éléments Setter aident à créer des propriétés pour les entités dans la page, telles que des pages dans l’élément [Page](#Page), des champs dans l’élément [Field](#Field) ou des données dans l’élément [Data](#Data) ou [DataItem](#DataItem). Vous configurez les propriétés dans les éléments [Setter](). Ajoutez un élément [Setter]() distinct pour chaque propriété que vous souhaitez définir. Vous modifiez les propriétés à l’aide du [SetterControl](#SetterControl) et vous configurez d’autres éléments [Setter]() à l’aide d’autres contrôles.  

-   **Données**. Les données servent à stocker des informations pour une utilisation par la page d’Assistant et d’autres composants. Vous pouvez définir des données pour des pages ou des champs à l’aide de l’élément [Data](#Data) ou [DataItem](#DataItem). Les données peuvent être définies dans une structure plate ou hiérarchique grâce à l’utilisation appropriée des éléments [Data](#Data) et [DataItem](#DataItem). Le fichier Config.xml de l’exemple dans le SDK montre comment créer des structures de données plates.  

 L’éditeur de page d’Assistant personnalisée que vous créez doit être capable de gérer ces paramètres de configuration.  

####  <a name="ReviewEditorPageExample"></a> Examiner l’exemple EditorPage  
 L’exemple EditorPage est utilisé pour configurer les paramètres de configuration de la page d’Assistant **SamplePage** dans le fichier de configuration UDI Wizard. L’exemple EditorPage comprend les composants principaux suivants :  

-   L’interface utilisateur pour configurer les paramètres de la zone de liste déroulante **Location**  

-   L’interface utilisateur pour ajouter ou modifier un emplacement dans la liste des emplacements possibles, qui sont affichés dans la zone de liste déroulante **Location**  

-   Les paramètres de configuration lus et enregistrés dans le fichier de configuration UDI Wizard  

-   Le code de prise en charge pour les autres composants  

 Passez en revue l’exemple EditorPage dans Visual Studio en effectuant les étapes suivantes :  

1.  Vérifiez comment l’éditeur de page d’Assistant **SampleEditor** est chargé et initialisé dans UDI Wizard Designer comme décrit dans [Examiner le chargement et l’initialisation de l’éditeur de page d’Assistant](#ReviewWizardPageEditorLoadingInitialization).  

2.  Passez en revue l’interface utilisateur permettant de modifier la zone de liste déroulante **Location** dans les fichiers LocationPageEditor.xaml et LocationPageEditor.xaml.cs comme décrit dans [Examiner l’interface utilisateur utilisée pour configurer la zone de liste déroulante Location](#ReviewUserInterfaceUsedtoConfigureLocationComboBox).  

3.  Passez en revue l’interface utilisateur utilisée pour ajouter ou modifier des emplacements dans la liste dans les fichiers AddEditLocationView.xaml et AddEditLocationView.xaml.cs comme décrit dans [Examiner l’interface utilisateur utilisée pour modifier la liste des emplacements possibles](#ReviewUserInterfaceUsedtoModifyListofPossibleLocations).  

4.  Passez en revue le code utilisé pour gérer les informations de configuration enregistrées dans le fichier de configuration UDI Wizard comme décrit dans [Examiner le code utilisé pour gérer les informations de configuration](#ReviewCodeUsedtoManageConfigurationInformation).  

#####  <a name="ReviewWizardPageEditorLoadingInitialization"></a> Examiner le chargement et l’initialisation de l’éditeur de page d’Assistant  
 Les éditeurs de pages d’Assistant personnalisées sont chargés selon les besoins par UDI Wizard Designer. Les fichiers de configuration UDI Wizard Designer sont chargés quand UDI Wizard Designer démarre. UDI Wizard Designer analyse le dossier *dossier_installation*\Bin\Config (où *dossier_installation* est le nom du dossier où MDT est installé) à la recherche de fichiers qui ont une extension de fichier .config.  

 Lors de la configuration de l’environnement de développement UDI, vous avez copié le fichier SamplePage.dll.confg dans le dossier *dossier_installation*\Bin\Config. Quand vous démarrez UDI Wizard Designer, le fichier SamplePage.dll.confg est détecté et chargé.  

 UDI Wizard Designer utilise les attributs suivants de l’élément [Page](#Page) dans le fichier SamplePage.dll.confg pour charger et initialiser l’exemple EditorPage :  

-   **DesignerAssembly**. Cet attribut détermine le nom de la DLL à charger. Cette DLL doit être placée dans le même dossier que le fichier UDIDesigner.exe, à savoir le dossier *dossier_installation* \Bin (où *dossier_installation* est le nom du dossier dans lequel MDT est installé).  

-   **DesignerType**. Cet attribut est le nom de type Microsoft .NET de la classe qui contient le contrôle utilisateur WPF.  

-   **Type**. Utilisez cet attribut pour configurer le type de page de la page d’Assistant personnalisée, qui est chargée par UDI Wizard. UDI Wizard Designer utilise cet attribut pour trouver l’élément [Page](#Page) approprié dans le fichier de configuration UDI Wizard.  

-   **Dll**. Utilisez cet attribut pour configurer l’élément [DLL](#DLL) dans le fichier de configuration UDI Wizard, que UDI Wizard Designer crée.  

-   **Description**. Utilisez cet attribut pour fournir des informations sur l’éditeur de page d’Assistant. La valeur de cet attribut est affichée dans la boîte de dialogue **Ajouter une nouvelle page** dans UDI Wizard Designer, qui permet d’ajouter la page d’Assistant à la bibliothèque de pages.  

-   **DisplayName**. Utilisez cet attribut pour fournir le nom de la page d’Assistant personnalisée affichée dans UDI Wizard Designer. La valeur de cet attribut est affichée dans la boîte de dialogue **Ajouter une nouvelle page** dans UDI Wizard Designer, qui permet d’ajouter la page d’Assistant à la bibliothèque de pages.  

     Dans l’exemple, le type de la page d’Assistant personnalisée **SamplePage** est **Microsoft.SamplePage.LocationPage**, qui est enregistré dans le fichier Config.xml. Le fichier Config.xml réside dans le dossier *dossier_local*\SDK\SamplePage\SamplePage (où *dossier_local* est le dossier que vous avez créé sur l’ordinateur de développement plus tôt durant le processus de configuration).  

#####  <a name="ReviewUserInterfaceUsedtoConfigureLocationComboBox"></a> Examiner l’interface utilisateur utilisée pour configurer la zone de liste déroulante Location  
 Quand l’éditeur de page d’Assistant est chargé et initialisé, l’éditeur de page d’Assistant SampleEditor est chargé lorsqu’une page avec le type **Microsoft.SamplePage.LocationPage** est modifiée. L’interface utilisateur de l’éditeur de page est stockée dans le fichier LocationPageEditor.xaml.  

 Si vous examinez l’interface utilisateur sous l’onglet **Conception** et le code sous l’onglet **XAML**, vous pouvez voir la relation entre l’interface graphique utilisateur et les éléments et attributs dans le code XAML (Extensible Application Markup Language).  

 Par exemple, si vous examinez l’élément **Controls:FieldElementControl** dans le code XAML, vous pouvez observer comment il se rapporte à la disposition de l’interface utilisateur correspondante. Utilisez l’élément **Controls:FieldElementControl** pour définir le contrôle [FieldElementControl](#FieldElementControl).  

 Les paramètres **Binding** dans le fichier XAML lient les champs dans l’exemple d’éditeur de page aux informations contenues dans le fichier de configuration UDI Wizard. Par exemple, le code suivant lie la zone de texte **Default value** à l’élément [Default](#Default) dans le fichier de configuration de UDI Wizard (Config.xml dans l’exemple) :  

```  
<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
```  

 Pour plus d’informations, consultez [How to: Make Data Available for Binding in XAML (Guide pratique pour rendre des données disponibles pour la liaison en XAML)](http://msdn.microsoft.com/library/ms748857.aspx).  

 Utilisez l’élément **Views:CollectionTControl.ColumnCollectionView** dans le code XAML pour modifier la liste des emplacements disponibles dans l’affichage de grille. Vous utilisez le contrôle [CollectionTControl](#CollectionTControl) pour afficher l’affichage de grille et le lier à l’élément [Data](#Data) nommé **Location** dans le fichier de configuration UDI.  

#####  <a name="ReviewUserInterfaceUsedtoModifyListofPossibleLocations"></a> Examiner l’interface utilisateur utilisée pour modifier la liste des emplacements possibles  
 L’interface utilisateur pour la modification de la liste des emplacements possibles est composée des éléments suivants :  

-   Des boutons de ruban et un menu contextuel qui vous permettent d’ajouter, de modifier, de supprimer ou de changer l’ordre des éléments dans la liste des emplacements, comme indiqué dans [Examiner le menu contextuel et les boutons de ruban pour la modification de la liste des emplacements](#ReviewContextSensitiveMenuandRibbonButtons)  

-   Une boîte de dialogue qui s’affiche quand vous choisissez d’ajouter ou de modifier un élément dans la liste des emplacements, comme décrit dans [Examiner la boîte de dialogue pour l’ajout ou la modification des emplacements](#ReviewDialogBoxforAddingEditingLocations)  

######  <a name="ReviewContextSensitiveMenuandRibbonButtons"></a> Examiner le menu contextuel et les boutons de ruban pour la modification de la liste des emplacements  
 Quand vous cliquez avec le bouton droit dans la zone de liste qui contient la liste des emplacements, un menu contextuel s’affiche. Le ruban comporte des boutons correspondants qui vous permettent d’effectuer les mêmes tâches. L’élément de contrôle **Views:CollectionsTControl** dans le fichier LocationPageEditor.xaml définit les méthodes appelées en fonction de l’action effectuée et des propriétés que vous avez définies comme suit :  

-   **SelectedItem**. Cette propriété liée aux données est activée quand l’utilisateur sélectionne un élément dans la liste. Cette propriété est liée à la propriété **CurrentLocation** dans le modèle d’affichage, qui se trouve dans le fichier LocationPageEditorViewModel.cs et est utilisée par le contrôle [CollectionTControl](#CollectionTControl) pour passer l’élément sélectionné quand vous modifiez ou supprimez un élément existant.  

-   **AddItemAction**. Cette action est effectuée quand l’utilisateur clique sur l’option **Add Item** dans le menu contextuel ou les boutons correspondants sur le ruban. Il existe une liaison de données à une propriété dans le modèle d’affichage qui retourne l’objet **AddLocationAction**. Cet objet est la méthode **AddLocationCallback**, située dans le fichier LocationPageEditorViewModel.cs. Il affiche la boîte de dialogue dans le fichier AddEditLocationView.xaml.  

-   **EditItemAction**. Cette action est effectuée quand l’utilisateur clique sur l’option **Edit Item** dans le menu contextuel. Il existe une liaison de données à une propriété dans le modèle d’affichage qui retourne l’objet **EditLocationAction**. Cet objet est la méthode **EditLocationCallback**, située dans le fichier LocationPageEditorViewModel.cs. Il affiche la boîte de dialogue dans le fichier AddEditLocationView.xaml.  

-   **RemoveAction**. Cette action est effectuée quand l’utilisateur clique sur l’option **Remove Item** dans le menu contextuel. Il existe une liaison de données à une propriété dans le modèle d’affichage qui retourne le **RemoveAction** objet. Cet objet est la **EditLocationCallback** (méthode), situé dans le fichier LocationPageEditorViewModel.cs et affiche un message qui confirme la suppression de l’emplacement.  

######  <a name="ReviewDialogBoxforAddingEditingLocations"></a> Examiner la boîte de dialogue pour l’ajout ou la modification des emplacements  
 Si vous ajoutez un nouvel emplacement à la liste des emplacements ou modifiez un emplacement existant, un message s’affiche dans le fichier AddEditLocationView.xaml. Le message s’affiche à l’aide de la méthode de fenêtre [ShowDialogWindow](#ShowDialogWindow) dans le fichier LocationPageEditorViewModel.cs.  

 L’interface utilisateur dans le fichier AddEditLocationView.xaml est composée des éléments suivants :  

-   Un frame de boîte de dialogue nommé **DialogFrame**, qui comprend les éléments suivants :  

    -   Un titre, que vous configurez à l’aide de l’attribut **DialogTitle** du frame de boîte de dialogue  

    -   Un bouton **OK**, qui définit l’état de retour de la propriété **Approved** sur **True** (l’état de retour est vérifié dans la méthode **AddLocationCallback** dans le fichier LocationPageEditorViewModel.cs afin de déterminer si l’utilisateur a cliqué sur **OK**.)  

    -   Un bouton **Cancel**, qui définit l’état de retour de la propriété **Approved** sur **False** (l’état de retour est vérifié dans la méthode **AddLocationCallback** dans le fichier LocationPageEditorViewModel.cs afin de déterminer si l’utilisateur a cliqué sur **Cancel**.)  

-   Un élément WPF qui contient :  

    -   Une étiquette, que vous configurez à l’aide de l’attribut **Content**.  

    -   Une zone de texte, qui est liée à l’élément [Data](#Data) nommé **Location** dans le fichier de configuration UDI (le fichier Config.xml dans l’exemple).  

######  <a name="ReviewCodeUsedtoManageConfigurationInformation"></a> Examiner le code utilisé pour gérer les informations de configuration  
 Les informations de configuration de votre page d’Assistant personnalisée sont stockées dans le fichier de configuration UDI Wizard, à savoir :  

-   Le fichier config.XML dans l’exemple fourni avec le SDK UDI (Ce fichier contient uniquement les paramètres de configuration pour l’exemple.)  

-   Le fichier UDIWizard_Config.xml fourni avec MDT, stocké dans le dossier *dossier_installation*\Templates\Distribution\Scripts (où *dossier_installation* est le dossier dans lequel vous avez installé MDT) ; ce fichier contient les paramètres de configuration pour toutes les phases et pages d’Assistant intégrées  

 Dans l’exemple SampleEditor, la routine **Locations** aide à gérer les informations de configuration. Elle se trouve dans le fichier LocationPageEditorViewModel.cs. La routine **Locations** retourne une liste des emplacements à partir du fichier de configuration UDI Wizard. Plus précisément, la liste retournée contient un élément pour chaque élément [DataItem](#DataItem) figurant dans le fichier de configuration UDI Wizard.  

## <a name="creating-custom-udi-wizard-pages"></a>Création de pages UDI Wizard personnalisées  
 La procédure à suivre pour créer des pages UDI Wizard personnalisées est la suivante :  

1.  Effectuez une copie de la solution SamplePage comme point de départ.  

2.  Placez les contrôles (champs) souhaités sur le formulaire.  

3.  Écrivez du code pour effectuer les tâches appropriées lors du chargement de la page d’Assistant (substitutions pour la méthode **OnWindowCreated**), y compris les étapes suivantes :  

    1.  Initialisation du SDK  

    2.  Lecture des variables en mémoire, des variables de séquence de tâches, des variables d’environnement ou des informations de fichier XML (telles que les propriétés **Setter**)  

4.  Écrivez du code pour effectuer les tâches appropriées lors de l’affichage de la page (substitutions pour la méthode **OnWindowShown**), y compris les étapes suivantes :  

    1.  Activation ou désactivation des contrôles en fonction des informations lues quand la page s’est chargée à l’étape 3  

    2.  Mise à jour des contrôles en fonction des informations lues quand la page s’est chargée à l’étape 3, comme le remplissage des contrôles en fonction des informations lues.  

5.  Écrivez du code pour effectuer les tâches appropriées pendant que l’utilisateur interagit avec la page d’Assistant.  

6.  Écrivez du code pour effectuer les tâches appropriées quand l’utilisateur clique sur **Suivant** dans UDI Wizard (substitutions pour la méthode **OnNextClicked**), y compris les étapes suivantes :  

    1.  Mise à jour des variables en mémoire, des variables de séquence de tâches, des variables d’environnement ou des informations de fichier XML  

    2.  Mise à jour des informations de page de synthèse (si elle n’a pas été effectuée par les champs dans la page)  

7.  Générez la solution.  

     Assurez-vous que la version de la DLL que vous créez est la même plateforme de processeur que l’installation de MDT, plus spécifiquement la plateforme de processeur de l’environnement Windows PE (Windows Preinstallation Environment). UDI Wizard peut s’exécuter sur :  

    -   **Le système d’exploitation existant sur l’ordinateur cible**. Vous pouvez exécuter des versions 32 bits de votre page d’Assistant sur des systèmes d’exploitation Windows 32 bits ou 64 bits. En revanche, vous ne pouvez exécuter des versions 64 bits de votre page d’Assistant que sur des systèmes d’exploitation Windows 64 bits.  

    -   **Windows PE sur l’ordinateur cible**. Windows PE ne prend pas en charge l’exécution d’applications 32 bits sur une version 64 bits de Windows PE. Par conséquent, vous devez avoir créé une version de votre page d’Assistant pour chaque architecture de processeur de Windows PE que vous envisagez d’utiliser.  

8.  Copiez la DLL de votre page d’Assistant personnalisée dans le dossier *dossier_installation*\Templates\Distribution\Tools\plateforme (où *dossier_installation* est le dossier dans lequel vous avez installé MDT et *plateforme* est **x86** pour la version 32 bits ou **x64** pour la version 64 bits).  

9. Effectuez les étapes de création d’éditeur de page personnalisée.  

## <a name="creating-custom-wizard-page-editors"></a>Création d’éditeurs de pages d’Assistant personnalisées  
 La procédure à suivre pour créer des éditeurs de pages UDI Wizard personnalisées est la suivante :  

1.  Effectuez une copie de la solution SampleEditor comme point de départ.  

2.  Créez l’interface utilisateur principale d’éditeur de page dans un fichier .xaml.  

3.  Ajoutez des instances du contrôle [FieldElementControl](#FieldElementControl) en fonction des besoins de la page d’Assistant à configurer (si nécessaire).  

4.  Ajoutez des instances du contrôle [SetterControl](#SetterControl) en fonction des besoins de la page d’Assistant à configurer (si nécessaire).  

5.  Ajoutez des instances du contrôle [CollectionTControl](#CollectionTControl) en fonction des besoins de la page d’Assistant à configurer (si nécessaire).  

6.  Ajoutez l’interface [IDataService](#IDataService).  

7.  Écrivez le code approprié pour mettre à jour le fichier de configuration UDI Wizard en fonction des paramètres de configuration à configurer à l’aide de votre éditeur de page d’Assistant personnalisée.  

8.  Créez des boîtes de dialogue enfants dans un fichier .xaml et appelez-les à partir de l’éditeur de page principale à l’aide de l’interface [IMessageBoxService](#IMessageBoxService) en fonction des besoins de la page d’Assistant à configurer.  

9. Ajoutez les interfaces appropriées au ruban UDI Wizard Designer en fonction des besoins de la page d’Assistant à configurer.  

10. Générez la solution.  

    > [!NOTE]
    >  Vérifiez que la version de la DLL que vous créez est la même plateforme de processeur que l’installation de MDT. Par exemple, si vous installez la version 64 bits de MDT, générez une version 64 bits de votre éditeur de page personnalisée.  

11. Créez un fichier de configuration UDI Wizard Designer pour charger les DLL nécessaires, et mappez l’éditeur de page d’Assistant à la page d’Assistant correspondante (le fichier SamplePage.dll.config dans l’exemple).  

     Pour plus d’informations sur les éléments nécessaires pour effectuer le mappage entre la page d’Assistant et l’éditeur de page d’Assistant, consultez l’élément [DesignerMappings](#DesignerMappings), les éléments enfants et les attributs correspondants.  

12. Copiez le fichier de configuration UDI Wizard Designer que vous avez créé à l’étape précédente dans le dossier *dossier_installation*\Bin\Config (où *dossier_installation* est le dossier dans lequel vous avez installé la version de MDT).  

13. Copiez la DLL de votre éditeur de page d’Assistant personnalisée dans le dossier *dossier_installation*\Bin (où *dossier_installation* est le dossier dans lequel vous avez installé MDT).  

##  <a name="CreatingCustomUDITasks"></a> Création de tâches UDI personnalisées  
 Les *tâches UDI* sont des DLL écrites en C++ qui implémentent l’[interface ITask](#ITaskinterface). Vous inscrivez la DLL auprès de la bibliothèque de tâches UDI Wizard Designer en créant un fichier de configuration UDI Wizard Designer (fichier .config) dans le dossier *dossier_installation*\Bin\Config (où *dossier_installation* est le dossier dans lequel vous avez installé MDT).  

> [!NOTE]
>  Vous pouvez créer une DLL qui contient des pages d’Assistant, des tâches et des validateurs dans le même fichier .dll. Vous pouvez également créer un fichier de configuration UDI Wizard Designer unique (.config) qui contient les paramètres de configuration pour les pages d’Assistant, les tâches et les validateurs figurant dans la DLL.  

 **Pour créer des tâches UDI personnalisées**  

1.  Écrivez du code qui implémente l’[interface ITask](#ITaskinterface) et les méthodes suivantes :  

    -   [Init](#Init). Cette méthode est appelée pour initialiser votre tâche.  

    -   [Execute](#Execute). Cette méthode est appelée pour exécuter votre tâche.  

2.  Écrivez du code qui inscrit la fabrique de classe de tâches personnalisées auprès du registre de fabrique.  

3.  Générez la solution pour votre tâche personnalisée.  

    > [!NOTE]
    >  Vérifiez que la version de la DLL que vous créez est la même plateforme de processeur que l’installation de MDT. Par exemple, si vous installez la version 64 bits de MDT, générez une version 64 bits de votre tâche UDI personnalisée.  

4.  Créez un élément [Task](#Task) sous l’élément [TaskLibrary](#TaskLibrary) dans le fichier de configuration UDI Wizard Designer similaire à l’extrait suivant :  

    ```  
    <Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
       <TaskItem Type="Setter" Name="Status Bitmap">  
          <Param Name="BitmapFilename"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Log File">  
          <Param Name="log"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Write Configuration File">  
          <Param Name="writecfg"/>  
       </TaskItem>  
       <TaskItem Type="Setter" Name="Read Configuration File">  
          <Param Name="readcfg"/>  
       </TaskItem>  
    </Task>  
    ```  

    > [!NOTE]
    >  Tous les éléments [Task](#Task) doivent inclure le paramètre **BitmapFilename**. Spécifiez tous les autres paramètres nécessaires en fonction de la tâche. Par exemple, dans l’extrait précédent, le paramètre **log** sert à spécifier un paramètre pour l’emplacement d’un fichier journal.  

5.  Copiez le fichier de configuration UDI Wizard Designer créé à l’étape précédente dans le dossier *dossier_installation*\Bin\Config (où *dossier_installation* est le dossier dans lequel vous avez installé MDT).  

6.  Copiez la DLL de votre tâche personnalisée dans le dossier *dossier_installation*\Templates\Distribution\Tools\plateforme (où *dossier_installation* est le dossier dans lequel vous avez installé MDT et *plateforme* est **x86** pour la version 32 bits ou **x64** pour la version 64 bits).  

##  <a name="CreatingCustomUDIValidators"></a> Création de validateurs UDI personnalisés  
 Les *validateurs UDI* sont des DLL écrites en C++ qui implémentent l’interface **IValidator**. Vous inscrivez la DLL auprès de la bibliothèque de validateurs UDI Wizard Designer en créant un fichier de configuration UDI Wizard Designer (fichier .config) dans le dossier *dossier_installation*\Bin\Config (où *dossier_installation* est le dossier dans lequel vous avez installé MDT).  

 **Pour créer des validateurs UDI personnalisés**  

1.  Écrivez du code qui crée une sous-classe de la classe **BaseValidator** et implémente les méthodes suivantes :  

    -   **Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)**. Le contrôleur de formulaire appelle le membre **Init** pour initialiser le validateur. Cette méthode doit appeler la méthode **Init** pour la classe **BaseValidator**. En règle générale, elle lit les propriétés définies pour le validateur à partir du fichier de configuration UDI Wizard. Par exemple, le validateur **InvalidCharactersValidator** récupère la valeur de la propriété **InvalidChars** à l’aide de cette méthode.  

    -   **IsValid**. Le contrôleur de formulaire appelle cette méthode pour déterminer si le contrôle contient du texte valide. Voici un exemple de méthode **IsValid** pour un validateur qui valide le fait que le champ n’est pas vide :  

        ```  
        BOOL IsValid(LPBSTR pMessage)  
        {  
            __super::IsValid(pMessage);  

            _bstr_t text;  
            m_pText->GetText(text.GetAddress());  
            return (text.length() > 0);  
        }  
        ```  

    -   **Init(IControl \*pControl, LPCTSTR message)**. Le contrôleur de formulaire appelle ce membre pour chaque frappe de touche et autres événements afin que le validateur puisse valider le contenu du contrôle et mettre à jour (ou effacer) les messages en bas de la page d’Assistant.  

     En général, il s’agit des seules méthodes que vous devez substituer. Toutefois, en fonction du validateur, vous devrez peut-être substituer d’autres méthodes dans la sous-classe de la classe **BaseValidator** que vous créez. Pour plus d’informations sur ces autres méthodes, consultez la classe **BaseValidator**.  

2.  Écrivez du code qui inscrit la classe de tâches personnalisées auprès du registre de fabrique.  

3.  Générez la solution pour votre tâche personnalisée.  

    > [!NOTE]
    >  Vérifiez que la version de la DLL que vous créez est la même plateforme de processeur que l’installation de MDT. Par exemple, si vous installez la version 64 bits de MDT, générez une version 64 bits de votre tâche UDI personnalisée.  

4.  Créez un élément [Validator](#Validator) sous l’élément **ValidatorLibrary** dans le fichier de configuration UDI Wizard Designer similaire à l’extrait suivant :  

    ```  
    <Validator   
    <Validator DLL="" Description="Must follow a pre-defined pattern" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern">  
       <Param Description="Enter the message you want displayed when the text in this field doesn't match the pattern:" Name="Message" DisplayName="Message"/>  
       <Param Description="The name of a pre-defined regular expression pattern. Must be Username, ComputerName, or Workgroup" Name="NamedPattern" DisplayName="Named Pattern"/>  
    </Validator>  
    ```  

    > [!WARNING]
    >  Tous les éléments [Validator](#Validator) doivent inclure le paramètre **Message**. Spécifiez tous les autres paramètres requis par le validateur. Par exemple, dans l’extrait précédent, le paramètre **NamedPattern** sert à spécifier un paramètre pour le nom d’un modèle d’expression régulière prédéfini.  

5.  Copiez le fichier de configuration UDI Wizard Designer créé à l’étape précédente dans le dossier *dossier_installation*\Bin\Config (où *dossier_installation* est le dossier dans lequel vous avez installé MDT).  

6.  Copiez la DLL de votre tâche personnalisée dans le dossier *dossier_installation*\Templates\Distribution\Tools\plateforme (où *dossier_installation* est le dossier dans lequel vous avez installé MDT et *plateforme* est **x86** pour la version 32 bits ou **x64** pour la version 64 bits).  

## <a name="udi-wizard-reference"></a>Référence d’UDI Wizard  

### <a name="wizard-page-components"></a>Composants de page d’Assistant  
 Vous pouvez utiliser les composants intégrés de votre choix pour générer vos pages personnalisées.  

#### <a name="creating-component-instances"></a>Création d’instances de composant  
 UDI Wizard utilise des fabriques de classes afin de créer des instances d’objets pour vous. Ces fabriques sont inscrites auprès d’un registre de fabrique, avec une chaîne comme clé de fabrique. Par exemple, le composant **WmiRepository** est identifié par la chaîne « Microsoft.Wizard.WmiRepository », qui est disponible dans le fichier d’en-tête IWmiRepository en tant que **ID_WmiRepository**.  

 En supposant que vous avez écrit votre page en tant que sous-classe de **WizardPageImpl**, vous pouvez créer une instance d’un **WmiRepoistory** comme suit :  

```  
PWmiRepository pWmi;  
CreateInstance(Container(), ID_WmiRepository, &pWmi);  
```  

 La fonction **CreateInstance** est une fonction de modèle de type sécurisé pour la création de nouvelles instances de composants. **PWmiRepository** étant un pointeur intelligent, il gère le décompte de références pour vous.  

#### <a name="creatable-components"></a>Composants qui peuvent être créés  
 Il existe un ensemble de composants que vous pouvez inscrire auprès du registre. Le premier ensemble de composants est toujours inscrit, car le fichier exécutable UDI Wizard principal le fournit. Les deux autres ensembles de composants sont fournis dans des DLL « facultatives ». Pour que ces composants soient disponibles, la DLL doit être répertoriée dans la section **DLL** du fichier .config XML. Votre code n’a pas besoin de savoir quel fichier exécutable contient un composant spécifique.  

 Le tableau 3 présente les ID des composants enregistrés auprès du registre de fabrique (défini dans OSDSetupWizard) ; le nom d’un composant est l’ID amputé du préfixe *ID_*.  

### <a name="table-3-component-ids"></a>Tableau 3. ID des composants  

|**ID**|**Description**|  
|-|-|  
|ID_ACPowerTask|(ITask IWizardComponent) Tâche de précontrôle qui vérifie que votre ordinateur ne s’exécute pas uniquement sur batterie|  
|ID_AppDiscoveryTask|(ITask IWizardComponent) Tâche spécialisée pour découvrir les éléments logiciels que vous avez installés sur votre ordinateur|  
|**ID_BackgroundTask**|(**IBackgroundTask**, **IWizardComponent**) Peuvent être utilisés pour exécuter une tâche sur un autre thread|  
|**ID_CopyFilesTask**|(**ITask**, **IWizardComponent**) Tâche pour copier un ou plusieurs fichiers|  
|**ID_FormController**|(**IFormController**) Votre page recevant sa propre instance, vous n’avez généralement pas besoin de créer une instance vous-même|  
|**ID_InvalidCharactersValidator**|(**IValidator**) Permet de s’assurer qu’aucun champ de texte ne contient des caractères issus d’une liste fournie au validateur|  
|**ID_Logger**|(**ILogger**) Votre page recevant un pointeur vers une instance partagée, vous n’avez généralement pas besoin de créer une instance vous-même|  
|**ID_NonEmptyValidator**|(**IValidator**) Validateur qui garantit qu’aucun champ n’est vide|  
|**ID_PasswordValidator**|(**IValidator**) Validateur qui garantit que deux champs de texte n’ont pas le même contenu|  
|**ID_Regex**|(**IRegEx**) Évalue les expressions régulières, en recherchant des correspondances|  
|**ID_RegExValidator**|(**IValidator**) Validateur qui effectue une validation par rapport à une expression régulière ou à un modèle connu|  
|**ID_SimpleStringProperties**|(**IStringProperties**, **ISimpleStringProperties**) Fournit un moyen simple pour envoyer des propriétés aux tâches sans utiliser XML|  
|**ID_ShellExecuteTask**|(**ITask**, **IWizardComponent**) Exécuter un programme externe|  
|**ID_SummaryBag**|(**ISummaryBag**) Disponible indirectement à partir de votre page par le biais de la méthode Form|  
|**ID_TaskManager**|(**ITaskManager**, **IBackgroundCallback**, **IWizardComponent**) Gère l’exécution d’un ensemble de tâches et de l’interface utilisateur|  
|**ID_WmiRepository**|(**IWmiRepository**, **IWizardComponent**) Vous permet d’exécuter des requêtes WMI (Windows Management Instrumentation)|  
|**ID_IXmlDocument**|(**Type IXmlDocument**) Fournit une façade pour lire et écrire des documents XML|  

 Les tableaux 4 et 5 présentent la bibliothèque OSDRefreshWizard.dll définie, les pages partagées et les autres composants de contrôle.  

### <a name="table-4-directory-controls"></a>Tableau 4. Contrôles de répertoire  

|**ID**|**Description**|  
|-|-|  
|**ID_Directory**|(**IDirectory**) Façade pour obtenir des informations de répertoire à partir du système de fichiers|  

### <a name="table-5-defined-sharedpagesdll"></a>Tableau 5. Bibliothèque SharedPages.dll définie  

|**ID**|**Description**|  
|-|-|  
|**ID_ADHelper**|(**IADHelper**) Fournit une façade pour un ensemble limité de fonctionnalités dans AD DS (Active Directory Domain Services)|  
|**ID_CpuInfo**|(**ICpuInfo**) Détermine si votre processeur a une architecture 32 ou 64 bits|  
|**ID_DomainJoinValidator**|(**IDomainJoinValidator**) A des méthodes pour vérifier si un ensemble d’informations d’identification est autorisé à joindre un domaine|  
|**ID_DriveList**|(**IDriveList**, **IBindableList**, **IWizardComponent**) Utilise WMI pour obtenir la liste des lecteurs de votre ordinateur|  
|**ID_WiredNetworkTask**|(**ITask**) Tâche qui vérifie si vous êtes connecté au réseau avec une carte réseau câblée (plutôt qu’avec une carte réseau sans fil)|  

#### <a name="control-components"></a>Composants de contrôle  
 Vous interagissez avec les contrôles de votre page par le biais de la fonction de modèle **GetControlWrapper**, qui donne accès à un des types de composants répertoriés dans le tableau 6.  

### <a name="table-6-components"></a>Tableau 6. Composants  

|**Types de contrôles de boîte de dialogue**|**Description**|  
|-|-|  
|**CONTROL_CHECK_BOX**|(**ICheckBox**) Façade pour utiliser des contrôles de case à cocher|  
|**CONTROL_COMBO_BOX**|(**IComboBox**) Façade pour les contrôles de zone de liste déroulante|  
|**CONTROL_GENERIC**|(**IControl**) Permet d’utiliser la plupart des types de contrôles pour contrôler les états d’activation et de visibilité|  
|**CONTROL_LIST_VIEW**|(**IListView**) Façade donnant accès aux fonctionnalités d’un contrôle d’affichage de liste|  
|**CONTROL_PROGRESS_BAR**|(**IProgressBar**) Façade pour utiliser la position d’un contrôle de barre de progression|  
|**CONTROL_RADIO_BUTTON**|(**IRadioButton**) Façade pour utiliser des contrôles de case d’option|  
|**CONTROL_STATIC_TEXT**|(**IStaticText**) Façade qui fournit l’autorisation de lecture/écriture sur le texte d’un contrôle, par exemple une étiquette ou zone de texte|  
|**CONTROL_TREE_VIEW**|(**ItreeView**) Façade pour utiliser un contrôle arborescence|  

#### <a name="image-list-component"></a>Composant ImageList  
 Ce composant est une façade pour un contrôle **ImageList** sur votre page. Vous créez une liste d’images par le biais de l’interface **IListView** ou **ITreeView**.  

#### <a name="formcontroller-component"></a>Composant FormController  
 L’Assistant crée ce composant pour vous et le passe à votre page. Vous y accédez à partir de votre page à l’aide de la méthode **Form**, implémentée par la classe de base **WizardPageImpl**.  

#### <a name="invalidcharactervalidator-component"></a>Composant InvalidCharacterValidator  
 Il s’agit d’un type de validateur que vous pouvez inclure dans une page. L’ID est **ID_InvalidCharactersValidator** (défini dans IValidator.h), qui a la valeur de texte « Microsoft.Wizard.Validation.InvalidChars ».  

 Ce validateur recherche une seule propriété appelée **InvalidChars** (un élément **Setter** dans le fichier .config), qui contient la liste des caractères non autorisés. Il vérifie les caractères d’une zone de texte ; si le texte contient des caractères figurant dans cette liste, le composant signale une erreur.  

#### <a name="nonemptyvalidator-component"></a>Composant NonEmptyValidator  
 Il s’agit d’un type de validateur que vous pouvez inclure dans une page. L’ID est **ID_NonEmptyValidator** (défini dans IValidator.h), qui a la valeur de texte « Microsoft.Wizard.Validation.NonEmpty ».  

 Ce validateur signale une erreur si la zone de texte (ou tout autre contrôle qui prend en charge **IStaticText**) a une valeur de chaîne vide.  

#### <a name="passwordvalidator-component"></a>Composant PasswordValidator  
 Il s’agit d’un type de validateur que vous pouvez inclure dans une page. L’ID est **ID_PasswordValidator** (défini dans IValidator.h), qui a la valeur de texte « Microsoft.Wizard.Validation.Password ».  

 Ce validateur fonctionne avec deux contrôles de texte différents (contrôles qui prennent en charge **IStaticText**) et signale une erreur s’ils ne contiennent pas les mêmes valeurs. En d’autres termes, il échoue si les zones de texte **Password** (Mot de passe) et **Confirm Password** (Confirmer le mot de passe) ne correspondent pas.  

 Étant donné que ce validateur requiert deux contrôles, sa configuration est plus sophistiquée que celle d’autres validateurs. La configuration peut ressembler à ceci :  

```  
Form()->AddToGroup(IDC_EDIT_PASSWORD, IDC_EDIT_PASSWORD2);  
PValidator pValidator;  
Form()->AddValidator(IDC_EDIT_PASSWORD, ID_PasswordValidator, pMessage, &pValidator);  
PStaticText pPassword2;  
GetControlWrapper(View(), IDC_EDIT_PASSWORD2, CONTROL_STATIC_TEXT, &pPassword2);  
pValidator->SetProperty(0, pPassword2);  
```  

 Tout d’abord, vous définissez le contrôle **Confirm Password** (Confirmer le mot de passe) en tant « qu’enfant » du contrôle **Password** (Mot de passe). De cette façon, si le contrôleur de formulaire désactive le contrôle **Password** (Mot de passe), il désactive également le contrôle **Confirm Password** (Confirmer le mot de passe). Ensuite, vous ajoutez un validateur de mot de passe au formulaire. Enfin, vous fournissez au validateur de mot de passe l’interface avec le contrôle **Confirm Password** (Confirmer le mot de passe).  

 Deux contrôles étant nécessaires, vous devez utiliser du code pour configurer ce validateur plutôt que le fichier .config.  

#### <a name="regexvalidator-component"></a>Composant RegExValidator  
 Il s’agit d’un type de validateur que vous pouvez inclure dans une page. L’ID est **ID_RegExValidator** (défini dans IValidator.h), qui a la valeur de texte « Microsoft.Wizard.Validation.RegEx ».  

 Ce validateur compare le contenu d’un contrôle de texte (prenant en charge **IStaticText**) à une expression régulière ; il échoue si le texte ne correspond pas à l’expression régulière.  

 Vous pouvez également utiliser ce validateur avec un modèle nommé prédéfini. Pour utiliser une expression régulière, le code XML doit contenir une propriété setter appelée **Pattern**. Si vous préférez utiliser un modèle nommé, utilisez un setter **NamedPattern** défini sur l’une des valeurs du tableau 7.  

### <a name="table-7-named-pattern-setters"></a>Tableau 7. Setters de modèle nommé  

|**Modèle**|**Description**|  
|-|-|  
|Utilisateur|Vérifie que le texte est de la forme domaine\utilisateur ou user@domain|  
|ComputerName|Le nom doit comprendre entre 1 et 15 caractères, et ne peut pas inclure certains caractères (par exemple : et ?)|  
|Groupe de travail|Le nom doit comprendre entre 1 et 15 caractères, et ne peut pas inclure certains caractères (par exemple =, + et ?)|  

#### <a name="factoryregistry-component"></a>Composant FactoryRegistry  
 Ce composant effectue le suivi de tous les services et fabriques de classes. Il implémente l’interface **IFactoryRegistry** et est disponible indirectement par le biais de la méthode **Container** de votre page. En outre, le registre charge des DLL d’extension. Après avoir chargé une DLL, le registre recherche une fonction exportée appelée **RegisterFactories**. Vous devez implémenter cette fonction et y inscrire les fabriques de classes pour vos pages, tâches et validateurs (et toutes autres fabriques de classes à inscrire). Voici une illustration tirée de l’exemple de projet :  

```  
extern "C" __declspec(dllexport) void RegisterFactories(IFactoryRegistry *factories)  
{  
Register<LocationPageFactory>(ID_LocationPage, factories);  
}  
```  

#### <a name="logger-component"></a>Composant Logger  
 Ce composant est disponible pour votre page par le biais de la méthode **Logger** (implémentée par **WizardPageImpl**). Cette méthode vous permet d’écrire des entrées dans le fichier journal. Le contenu du fichier journal sert à diagnostiquer les problèmes que les utilisateurs peuvent rencontrer en exécutant l’Assistant UDI.  

#### <a name="propertybag-component"></a>Composant PropertyBag  
 Le *jeu de propriétés* est un conteneur pour les variables de mémoire. Vous pouvez y accéder à partir de votre page à l’aide de **Container()->Properties()**. Les variables de mémoire sont utiles pour passer des données temporaires d’une page à une autre.  

#### <a name="tsvariablebag-and-tsrepository-components"></a>Composants TSVariableBag et TSRepository  
 Le composant **TSVariableBag** vous permet de lire et d’écrire les variables de séquence de tâches. Il conserve les valeurs en mémoire jusqu’à ce que l’utilisateur clique sur **Finish** (Terminer) (par défaut). Vous pouvez accéder au jeu **TSVariable** par le biais de la méthode **TSVariables** de la page (implémentée par la classe de base **WizardPageImpl**). Ces composants journalisent toutes les lectures et écritures de variables de séquence de tâches.  

#### <a name="wmirepository-component"></a>Composant WmiRepository  
 Ce composant fournit une façade pour utiliser des requêtes WMI. Vous pouvez appeler la fonction d’assistance **CreateInstance** avec **ID_WmiRepository** pour obtenir une instance de ce composant, qui prend en charge l’interface **IWmiRepository**. Ce composant retourne des enregistrements de résultats par le biais de l’interface **IWmiIterator**.  

###  <a name="WizardPageHelperClasses"></a> Classes d’assistance de page de l’Assistant  
 Vous pouvez créer des pages d’Assistant UDI personnalisées à l’aide des classes d’assistance intégrées fournies avec le SDK UDI. Le tableau 8 répertorie les classes d’assistance que vous pouvez utiliser pour créer des pages d’Assistant personnalisées.  

### <a name="table-8-helper-classes"></a>Tableau 8. Classes d’assistance  

|**Classes d’assistance**|**Description**|  
|-|-|  
|[Classe ClassFactoryImpl](#ClassFactoryImplClass)|Il s’agit d’une classe de base utile pour créer une fabrique de classe en vue de son inscription auprès du registre de fabrique.|  
|[Classe de modèle d’interface](#InterfaceTemplateClass)|Utilisez cette classe de modèle quand vous souhaitez créer un composant qui implémente plusieurs interfaces.|  
|[Classe d’assistance de chemin](#PathHelperClass)|Cette classe fournit les opérations de fichier/répertoire courantes.|  
|[Classe de modèle de pointeur](#PointerTemplateClass)|Cette classe fournit un décompte de références pour la gestion de la durée de vie dans les composants COM. Il est important de libérer les interfaces dont vous ne vous servez plus. Cette classe de modèle gère la durée de vie automatiquement.|  
|[Classe PUnknown](#PUnkownClass)|Cette classe est un pointeur intelligent pour l’interface IUnknown. Pour toutes les autres interfaces, utilisez la classe de modèle Pointer.|  
|[Classe d’assistance StringUtil](#StringUtilHelperClass)|Cette classe fournit des méthodes d’assistance qui facilitent l’utilisation des chaînes.|  
|[Classe de modèle SubInterface](#SubInterfaceTemplateClass)|Cette classe de base facilite l’implémentation d’un composant qui prend en charge une interface héritant elle-même d’une autre interface.|  
|[Classe de modèle UnknownImpl](#UnknownImplTemplateClass)|Cette classe gère la plupart des détails de la création d’un composant COM.|  
|[Classe de modèle WizardComponent](#WizardComponentTemplateClass)|Cette classe de base est utilisée pour créer des composants qui ont besoin d’accéder aux services d’Assistant, tels que la création de composants et la journalisation.|  
|[Classe de modèle WizardPageImpl](#WizardPageImplTemplateClass)|Cette classe de base doit être utilisée comme classe de base pour toutes les pages d’Assistant personnalisées|  

####  <a name="ClassFactoryImplClass"></a> Classe ClassFactoryImpl  
 Il s’agit d’une classe de base utile pour créer une fabrique de classe en vue de son inscription auprès du registre de fabrique.  

 Voici un extrait du fichier LocationPage.h de l’exemple de projet qui illustre la définition de la classe **ClassFactoryImpl**.  

```  
#pragma once  

#include "ClassFactoryImpl.h"  

class LocationPageFactory :public ClassFactoryImpl  
{  
protected:  
    IUnknown *CreateNewInstance();  
};  
```  

 Voici un extrait du fichier LocationPage.cpp de l’exemple de page d’Assistant qui illustre la définition de la fabrique de classe pour la page.  

```  
IUnknown *LocationPageFactory::CreateNewInstance()  
{  
    return static_cast<IWizardPage *>(new LocationPage);  
}  
```  

####  <a name="InterfaceTemplateClass"></a> Classe de modèle d’interface  
 Utilisez cette classe de modèle quand vous souhaitez créer un composant qui implémente plusieurs interfaces, par exemple :  

```  
classLocationPage :public Interface<IFieldCallback, WizardPageImpl<IDD_LOCATION_PAGE>>  
```  

 Ce code crée une chaîne de classe de base qui prend en charge **IFieldCalback** et les interfaces prises en charge par **WizardPageImpl** (en l’occurrence **IWizardPage**).  

####  <a name="PathHelperClass"></a> Classe d’assistance de chemin  
 Cette classe fournit les opérations de fichier/répertoire courantes :  

```  
static inline std::wstring GetModulePath(HINSTANCE hModule)  
```  

 Elle retourne également le chemin complet du fichier .exe ou .dll avec le handle d’instance que vous fournissez à cette méthode :  

```  
static inline std::wstring GetModuleFilename(HINSTANCE hModule)  
```  

 La classe retourne le chemin complet et le nom du fichier .exe et .dll avec le handle d’instance que vous fournissez à cette méthode :  

```  
static inline std::wstring GetDirecotryName(LPCWSTR fullName)  
```  

 . . . ou simplement le chemin sans le nom de fichier :  

```  
static inline std::wstring GetFileName(LPCWSTR fullName)  
```  

 À partir d’un chemin comportant un nom de fichier, la classe d’assistance de chemin retourne uniquement le nom de fichier :  

```  
static inline std::wstring Combine(LPCWSTR path, LPCWSTR name)  
```  

 Enfin, la classe retourne une nouvelle chaîne qui combine le chemin et le nom (ou un autre chemin).  

####  <a name="PointerTemplateClass"></a> Classe de modèle de pointeur  
 Cette classe est définie dans Pointer.h. Étant donné que les composants COM utilisent le décompte de références pour la gestion de la durée de vie, il est important de toujours libérer les interfaces dont vous ne vous servez plus. Microsoft fournit une classe de modèle qui gère la durée de vie automatiquement. Par exemple, si vous souhaitez un pointeur intelligent pour une interface de XML, vous pouvez écrire quelque chose comme ceci :  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 La première ligne définit le pointeur intelligent. La seconde ligne illustre la récupération d’un pointeur intelligent par le biais d’un autre appel. L’opérateur **&** libère toujours une interface existante s’il en contient une et retourne l’adresse du pointeur interne. Une fois que vous avez récupéré un pointeur de cette façon, l’instance **Pointer** appelle automatiquement **Release** quand la variable quitte la portée. Microsoft vous recommande d’utiliser des pointeurs intelligents au lieu d’appeler **AddRef** et **Release** manuellement.  

 En outre, la classe de pointeur intelligent **Pointer** appelle **QueryInterface** pour récupérer d’autres interfaces automatiquement. Par exemple, quand le registre de fabrique crée une instance d’un composant, il a un code similaire à celui-ci :  

```  
PWizardComponent pComp = pUnknown;  
if (pComp != nullptr)  
    pComp->SetContainer(m_pContainer);  
```  

 La première ligne appelle **QueryInterface** en arrière-plan pour demander l’interface **IWizardComponent**. Le pointeur intelligent qui en résulte est égal à **nullptr** si le composant ne prend pas en charge cette interface.  

####  <a name="PUnkownClass"></a> Classe PUnknown  
 Cette classe est un pointeur intelligent pour l’interface **IUnknown**. Pour toutes les autres interfaces, utilisez la classe de modèle **Pointer**.  

####  <a name="StringUtilHelperClass"></a> Classe d’assistance StringUtil  
 Cette classe est définie dans Utilities.h et fournit des méthodes d’assistance qui facilitent l’utilisation des chaînes :  

```  
static inline int CompareIgnore(LPCWSTR first, LPCWSTR second)  
```  

 Cette méthode compare deux chaînes, sans tenir compte de la casse (voir le tableau 9).  

### <a name="table-9-stringutil-helper-class"></a>Tableau 9. Classe d’assistance StringUtil  

|**Retourne**|**Description**|  
|-|-|  
|**0**|Les chaînes correspondent, indépendamment de la casse|  
|**<0**|Première < seconde|  
|**>0**|Première > seconde|  

 Voici un exemple :  

```  
static inline std::wstring Format(LPCWSTR input, int index, LPCWSTR value)  
static inline std::wstring Format(LPCWSTR input, int index, DWORD value)  
```  

 Ces méthodes rappellent un peu les méthodes **Format** Microsoft .NET par la formulation des paramètres en **{0}**. Toutefois, elles n’effectuent pas de mise en forme de l’entrée, uniquement une substitution :  

```  
static inline std::wstring Printf(std::wstring format, I val)  
static inline std::wstring Printf(std::wstring format, I val1, J val2)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3)  
static inline std::wstring Printf(std::wstring format, I val1, J val2, K val3, L val4)  
```  

 Ce sont des wrappers autour de **StringCchPrintf** qui retournent un **wstring** pour que vous n’ayez pas à allouer vous-même de la mémoire pour les chaînes ou mémoires tampons.  

####  <a name="SubInterfaceTemplateClass"></a> Classe de modèle SubInterface  
 Cette classe de base facilite l’implémentation d’un composant qui prend en charge une interface héritant elle-même d’une autre interface. Par exemple, l’interface **ICheckBox** hérite de **IControl**. Voici la façon dont cette classe est utilisée pour définir le **CheckBoxWrapper** :  

```  
classCheckBoxWrapper :public SubInterface<IControl, UnknownImpl<ICheckBox> >  
```  

 L’interface de base est le premier paramètre, tandis que l’interface dérivée est le deuxième paramètre.  

####  <a name="UnknownImplTemplateClass"></a> Classe de modèle UnknownImpl  
 Cette classe est définie dans UnknownImpl.h et gère la plupart des détails de la création d’un composant COM. Voici un exemple d’utilisation de cette classe de base :  

```  
classDirectory :public UnknownImpl<IDirectory>  
```  

 Ce code définit une classe qui prend en charge l’interface **IDirectory**.  

####  <a name="WizardComponentTemplateClass"></a> Classe de modèle WizardComponent  
 Cette classe est définie dans IWizardComponent.h, et est une classe de base utile pour créer des composants qui ont besoin d’accéder aux services d’Assistant, tels que la création de composants et la journalisation.  

 Voici un exemple de définition du composant **CopyFilesTask** :  

```  
classCopyFilesTask :public WizardComponent<ITask>  
{  
    ...  
```  

 Le paramètre de cette classe de modèle est l’interface « principale » que vous souhaitez utiliser pour votre composant, soit **ITask** dans le cas des tâches. Utiliser **WizardComponent** signifie que votre composant prend en charge l’interface que vous fournissez (**ITask** dans cet exemple) et **IWizardComponent**.  

 Chaque fois que vous utilisez le registre de fabrique de classe pour créer un composant, le registre appelle la méthode **IWizardComponent->SetContainer** du composant pour fournir à ce dernier l’accès aux services d’Assistant.  

####  <a name="WizardPageImplTemplateClass"></a> Classe de modèle WizardPageImpl  
 Utilisez cette classe comme classe de base pour vos pages personnalisées, par exemple :  

```  
class LocationPage :public WizardPageImpl<IDD_LOCATION_PAGE>  
```  

 Le paramètre est l’ID de ressource pour votre modèle de boîte de dialogue.  

###  <a name="WizardPageInterfaces"></a> Interfaces de la page de l’Assistant  
 L’Assistant UDI utilise des interfaces pour accéder aux différents contrôles sur votre page. Dans la page, vous utilisez la fonction **GetControlWrapper** pour récupérer un wrapper de contrôle. Voici un exemple :  

```  
PStaticText pFormat;  
GetControlWrapper(View(), IDC_CHECK_PARTITION, CONTROL_STATIC_TEXT, &pFormat);  
```  

 Ici, **PStaticText** est un pointeur intelligent vers l’interface **IStaticText**. Les pointeurs intelligents appellent automatiquement la méthode **Release()** COM quand ils quittent la portée ou que vous passez l’adresse d’une variable (comme **&pFormat**) à une méthode.  

#### <a name="iadhelper-interface"></a>Interface IADHelper  

```  
__interfaceIADHelper : IUnknown  
{  
    HRESULT Init(ILogger *pLogger);  
    HRESULT ValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain);  
    HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain);  
};  

```  

##### <a name="hresult-initilogger-plogger"></a>HRESULT Init(ILogger \*pLogger)  
 Initialisez ce composant, en le passant au journaliseur afin qu’il puisse journaliser les informations.  

##### <a name="hresultvalidlogonlpctstr-username-lpctstr-password-lpctstr-domain"></a>HRESULTValidLogon(LPCTSTR userName, LPCTSTR password, LPCTSTR domain)  
 Cette méthode vérifie si un ensemble d’informations d’identification est valide, comme indiqué dans le tableau 10.  

### <a name="table-10-hresultvalidlogon"></a>Tableau 10. HResultValidLogon  

|**HResult**|**Description**|  
|-|-|  
|S_OK|Les informations d’identification sont valides|  
|S_FALSE|Les informations d’identification ne sont pas valides|  
|E_FAIL|Impossible de trouver le contrôleur de domaine ; consultez les journaux pour plus d’informations|  

##### <a name="hresult-hasaccesslpctstr-username-lpctstr-password-lpctstr-domain-lpctstr-computername-lpctstr-accountdomain"></a>HRESULT HasAccess(LPCTSTR username, LPCTSTR password, LPCTSTR domain, LPCTSTR computerName, LPCTSTR accountDomain)  
 Cette méthode vérifie si un ensemble d’informations d’identification a accès en lecture/écriture à l’objet ordinateur dans AD DS, comme indiqué dans le tableau 11.  

### <a name="table-11-hresult-hasaccess"></a>Tableau 11. HResult HasAccess  

|**HRESULT**|**Description**|  
|-|-|  
|S_OK|L’utilisateur a accès.|  
|E_FAIL|L’utilisateur n’a pas accès. Pour plus d’informations, consultez le fichier journal.|  

#### <a name="ibackgroundtask-interface"></a>Interface IBackgroundTask  

```  
__interface IBackgroundTask : IUnknown  
{  
    HRESULT Init(ITask *pTask, int id, IBackgroundCallback *pCallback);  
    void Start(void);  
    BOOL Running(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    HRESULT Terminate(DWORD exitCode);  
    HRESULT GetExitCode(LPDWORD pCode, HRESULT *pHresult);  
    HRESULT Close(void);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 La page **Progress** (Progression) utilise cette classe pour exécuter des tâches sur un thread distinct. Vous pouvez également utiliser cette classe quand vous souhaitez effectuer des opérations sur un thread distinct. Les *tâches* sont toute classe qui prend en charge l’interface **ITask**.  

 Cette interface est implémentée par le composant **ID_BackgroundTask** (« Microsoft.Wizard.BackgroundTask »), défini dans l’interface IBackgroundTask.h.  

##### <a name="hresult-inititask-ptask-int-id-ibackgroundcallback-pcallback"></a>HRESULT Init(ITask \*pTask, int id, IBackgroundCallback \*pCallback)  
 Cette interface initialise le composant, comme indiqué dans le tableau 12.  

### <a name="table-12-hresult-init"></a>Tableau 12. HRESULT Init  

|**Paramètre**|**Description**|  
|-|-|  
|**pTask**|Pointeur vers la classe qui contient le code que vous souhaitez exécuter sur un autre thread|  
|**Id**|Nombre que vous pouvez utiliser dans la méthode **Finished** du rappel pour indiquer la tâche dont l’exécution est terminée ; utile si vous démarrez plusieurs tâches avec la même méthode de rappel|  
|**pCallback**|Classe qui implémente la méthode **Finished**, qui est appelée chaque fois qu’une tâche se termine ; l’appel à la méthode **Finished** se trouve sur le thread d’arrière-plan, pas sur le thread d’interface utilisateur|  

##### <a name="void-startvoid"></a>void Start(void)  
 Cette méthode démarre la tâche sur un thread d’arrière-plan et retourne les éléments indiqués dans le tableau 13.  

### <a name="table-13-return-background-thread"></a>Tableau 13. Thread d’arrière-plan de retour  

|**Retourne**|**Description**|  
|-|-|  
|**E_INVALIDARG**|La tâche est déjà en cours d’exécution ; vous ne pouvez donc pas la démarrer maintenant.|  
|**E_FAIL**|Impossible de démarrer le thread.|  
|**S_OK**|Le thread a démarré.|  

##### <a name="bool-running"></a>BOOL Running()  
 Cette méthode retourne TRUE si la tâche en arrière-plan est en cours d’exécution, FALSE sinon.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Cette méthode attend que l’exécution du thread prenne fin ou que le nombre de millisecondes se soit écoulé.  

##### <a name="hresult-terminatedword-exitcode"></a>HRESULT Terminate(DWORD exitCode)  
 Cette méthode arrête le thread en cours d’exécution (voir les tableaux 14 et 15). Ce processus peut prendre un peu de temps après le retour de cette méthode.  

### <a name="table-14-hresult-terminate-exit-code"></a>Tableau 14. Code de sortie d’arrêt HRESULT  

|**Paramètre**|**Description**|  
|-|-|  
|**exitCode**|Le code de sortie envoyé à la méthode de rappel Finished, également disponible à partir de la méthode **GetExitCode**.|  

### <a name="table-15-termination-codes"></a>Tableau 15. Codes d’arrêt  

|**Retourne**|**Description**|  
|-|-|  
|**E_FAIL**|Échec de l’appel d’arrêt.|  
|**S_OK**|La demande d’arrêt du thread a réussi.|  

##### <a name="hresult-getexitcodelpdword-pcode-hresult-phresult"></a>HRESULT GetExitCode(LPDWORD pCode, HRESULT \*pHresult)  
 Utilisez cette méthode pour obtenir les résultats de l’exécution de la tâche sur le thread d’arrière-plan (voir le tableau 16).  

### <a name="table-16-result-codes"></a>Tableau 16. Codes de résultat  

|**Paramètre**|**Description**|  
|-|-|  
|**pCode**|Pointeur vers un **DWORD** qui est défini en retour, ou **nullptr** si vous n’avez pas besoin de la valeur de retour. À la sortie, ce paramètre est défini sur **STILL_ACTIVE** si le thread est en cours d’exécution, sur le code retourné par la méthode **Execute** de la tâche ou sur la valeur passée à la méthode **Terminate** si vous avez appelé cette méthode.|  
|**pHresult**|Pointeur vers un **HRESULT** qui est défini en retour, ou **nullptr** si vous n’avez pas besoin de la valeur **HRESULT**.|  

##### <a name="hresult-closevoid"></a>HRESULT Close(void)  
 Cette méthode libère le thread d’arrière-plan. Elle retourne **E_INVALIDARG** si le thread est en cours d’exécution, **S_OK** dans le cas contraire.  

#### <a name="icheckbox-interface"></a>Interface ICheckBox  

```  
__interface ICheckBox : IControl  
{  
    void Check(BOOL check);  
    BOOL IsButtonChecked();  
};  
```  

##### <a name="void-checkbool-check"></a>void Check(BOOL check)  
 Définir l’état d’activation de la case à cocher. Quand la méthode a la valeur TRUE, la case est cochée ; quand la méthode a la valeur FALSE, la case est décochée.  

##### <a name="bool-isbuttonchecked"></a>BOOL IsButtonChecked()  
 Cette méthode signale l’état d’activation actuel d’une case à cocher.  

#### <a name="icombobox-interface"></a>Interface IComboBox  

```  
__interface IComboBox : IControl  
{  
    HRESULT Bind([in] IBindableList *pList);  
    HRESULT Select(int index);  
    int Selected(void);  
    void Add([in] LPCTSTR caption);  
    HRESULT GetText([out, retval] LPBSTR pText);  
    void Clear();  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **CheckBoxWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_COMBO_BOX**.  

##### <a name="hresult-bindin-ibindablelist-plist"></a>HRESULT Bind([in] IBindableList \*pList)  
 Utilisez cette méthode quand vous avez une source de données qui implémente l’interface **IBindableList**. La zone de liste initialise le contenu avec les légendes issues de cette liste.  

##### <a name="hresult-selectint-index"></a>HRESULT Select(int index)  
 Sélectionner dans la zone de liste modifiable l’élément correspondant à l’index.  

##### <a name="int-selectedvoid"></a>int Selected(void)  
 Cette méthode retourne l’index de l’élément sélectionné ou **-1** si rien n’est sélectionné.  

##### <a name="void-addin-lpctstr-caption"></a>void Add([in] LPCTSTR caption)  
 Ajouter manuellement un élément à la zone de liste modifiable.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Récupérer la chaîne de l’élément actuellement sélectionné dans la zone de liste modifiable.  

##### <a name="void-clear"></a>void Clear()  
 Supprimer tous les éléments de la zone de liste modifiable.  

#### <a name="icontrol-interface"></a>Interface IControl  

```  
__interface IControl : IUnknown  
{  
    HRESULT SetEnable(BOOL enable);  
    BOOL IsEnabled(void);  
    HRESULT SetVisible(BOOL visible);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **CheckBoxWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_GENERIC**.  

##### <a name="hresult-setenablebool-enable"></a>HRESULT SetEnable(BOOL enable)  
 Activer ou désactiver le contrôle.  

##### <a name="bool-isenabledvoid"></a>IsEnabled(void)  
 Retourne la valeur TRUE si le contrôle est activé, FALSE sinon.  

##### <a name="hresult-setvisiblebool-visible"></a>HRESULT SetVisible(BOOL visible)  
 Afficher ou masquer le contrôle.  

#### <a name="icpuinfo-interface"></a>Interface ICpuInfo  

```  
__interface ICpuInfo : IUnknown  
{  
    BOOL Is64Bit(void);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Vous obtenez cette interface en créant un composant **ID_CpuInfo**. La méthode unique indique si l’UC a une architecture 32 ou 64 bits. Notez que si vous avez un système d’exploitation 32 bits sur un ordinateur 64 bits, cette méthode retourne la valeur TRUE, car elle signale uniquement la largeur de l’UC (pas celle du système d’exploitation).  

##### <a name="idirectory-interface"></a>Interface IDirectory  

```  
__interface IDirectory : IUnknown  
{  
    BOOL FileExists(LPCWSTR name);  
    BOOL FindFirst([in] LPCWSTR name);  
    HRESULT FoundName([out, retval] LPBSTR name);  
    DWORD FoundAttributes(void);  
    BOOL FindNext(void);  
    void FinishFind(void);  
};  
```  

###### <a name="overview"></a>Vue d'ensemble  
 Le composant **Directory** ,que vous créez à l’aide de **ID_Directory**, fournit une façade pour utiliser les répertoires dans le système de fichiers.  

###### <a name="bool-fileexistslpcwstr-name"></a>BOOL FileExists(LPCWSTR name)  
 Cette méthode retourne la valeur TRUE si un fichier portant le nom spécifié existe.  

###### <a name="bool-findfirstin-lpcwstr-name"></a>BOOL FindFirst([in] LPCWSTR name)  
 Cette méthode recherche une première correspondance pour le nom spécifié. Elle prend en charge les caractères génériques et retourne les noms de fichiers et de répertoires. La méthode retourne la valeur TRUE si une correspondance a été trouvée, FALSE sinon.  

###### <a name="hresult-foundnameout-retval-lpbstr-name"></a>HRESULT FoundName([out, retval] LPBSTR name)  
 Cette méthode récupère le nom du fichier trouvé avec un appel à **FindFirst** ou **FindNext**.  

###### <a name="dword-foundattributesvoid"></a>DWORD FoundAttributes(void)  
 Cette méthode retourne l’attribut du tout dernier fichier ou répertoire trouvé. Vous pouvez utiliser du code tel que le suivant pour déterminer s’il s’agit d’un répertoire :  

```  
pDirectory->FoundAttributes() & FILE_ATTRIBUTE_DIRECTORY  
```  

###### <a name="bool-findnextvoid"></a>BOOL FindNext(void)  
 Rechercher la correspondance suivante. Cette méthode retourne la valeur TRUE si une autre correspondance a été trouvée, FALSE sinon.  

###### <a name="void-finishfindvoid"></a>void FinishFind(void)  
 Cette méthode libère les ressources utilisées pour l’opération de recherche.  

#### <a name="idomainjoinvalidator-interface"></a>Interface IDomainJoinValidator  

```  
__interface IDomainJoinValidator : IUnknown  
{  
    HRESULT Init(ILogger *pLogger, IWizardPageContainer *pContainer, IStaticText *pUsername, IStaticText *pPassword, IStaticText *pComputerName);  
    HRESULT IsUsernameValid(LPCWSTR domainName);  
    BOOL CanModifyComputerAdEntry(LPCWSTR domainName);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Vous obtenez une instance de cette interface à l’aide de la valeur **ID_DomainJoinValidator** dans la fonction de modèle **CreateInstance**.  

##### <a name="hresult-initilogger-plogger-iwizardpagecontainer-pcontainer-istatictext-pusername-istatictext-ppassword-istatictext-pcomputername"></a>HRESULT Init(ILogger \*pLogger, IWizardPageContainer \*pContainer, IStaticText \*pUsername, IStaticText \*pPassword, IStaticText \*pComputerName)  
 Initialiser l’instance, comme illustré dans le tableau 17.  

### <a name="table-17-hresult-init---instance-initialization"></a>Tableau 17. HRESULT Init ; initialisation de l’Instance  

|**Paramètre**|**Description**|  
|-|-|  
|**pLogger**|Instance du journaliseur, qui est disponible pour votre page par le biais de la méthode **Logger** de la page|  
|**pContainer**|Passe les résultats à partir de la méthode **Container** de votre page|  
|**pUsername**|Zone de texte qui contient le nom d’utilisateur à valider|  
|**pPassword**|Zone de texte qui contient le mot de passe à valider|  
|**PComputerName**|Zone de texte qui contient le nom de l’ordinateur qui sera finalement joint au domaine|  

##### <a name="hresult-isusernamevalidlpcwstr-domainname"></a>HRESULT IsUsernameValid(LPCWSTR domainName)  
 Cette méthode utilise la méthode **IADHelper->ValidLogon** pour effectuer le travail. Consultez cette méthode pour plus d’informations.  

##### <a name="bool-canmodifycomputeradentrylpcwstr-domainname"></a>BOOL CanModifyComputerAdEntry(LPCWSTR domainName)  
 Vérifier si l’utilisateur dispose des droits nécessaires pour modifier l’entrée d’ordinateur. La plupart du travail est effectué par **IADHelper->HasAccess**. Si cette méthode retourne la valeur FALSE, vérifiez le fichier journal pour plus d’informations.  

#### <a name="idrivelist-interface"></a>Interface IDriveList  

```  
__interface IDriveList : IUnknown  
{  
    HRESULT Init(IWmiRepository *pWmi);  
    HRESULT SetWhereClause(LPCTSTR whereClause);  
    HRESULT SetMinimumDriveSize(__int64 size);  
    HRESULT Update(void);  
    HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned);  

    size_t Count(void);  
    HRESULT GetProperty(size_t index, LPCTSTR propName,  LPVARIANT value);  
    HRESULT GetCaption(size_t index,  LPBSTR pCaption);  
}  
```  

##### <a name="hresult-initiwmirepository-pwmi"></a>HRESULT Init(IWmiRepository \*pWmi)  
 Appelez cette méthode avant d’appeler d’autres composants. Vous devez créer un **WmiRepository** avant d’appeler cette méthode.  

##### <a name="hresult-setwhereclauselpctstr-whereclause"></a>HRESULT SetWhereClause(LPCTSTR whereClause)  
 Cette méthode vous permet d’ajouter du texte qui apparaît sous la forme d’une clause « where » dans la requête. Par exemple, la ligne suivante retourne uniquement les lecteurs USB :  

```  
pDrives->SetWhereClause(L"WHERE InterfaceType='USB'");  
```  

##### <a name="hresult-setminimumdrivesizeint64-size"></a>HRESULT SetMinimumDriveSize(\__int64 size)  
 Définir la taille de lecteur minimale, en octets, pour les lecteurs retournés par la requête.  

##### <a name="hresult-updatevoid"></a>HRESULT Update(void)  
 Exécuter la requête. La liste de lecteurs disponible après l’appel de cette méthode est triée par lettre de lecteur.  

##### <a name="hresult-addpropertyenumdiskquerysection-section-lpctstr-propname-lpctstr-propnamereturned"></a>HRESULT AddProperty(ENUM_DISK_QUERY_SECTION section, LPCTSTR propName, LPCTSTR propNameReturned)  
 Cette méthode ajoute les noms de propriétés supplémentaires que vous souhaitez faire figurer dans les résultats de la requête. Appelez cette méthode avant d’appeler **Update**. Le tableau 18 illustre trois des propriétés utiles.  

### <a name="table-18-hresult-addproperty-useful-properties"></a>Tableau 18. HRESULT AddProperty : propriétés utiles  

|**Section**|**Propriété**|**Description**|  
|-|-|-|  
|**DISKQUERY_LOGICALDISK**|**Size**|Taille, en octets, représentée sous forme de chaîne|  
|**DISKQUERY_DISKPARTITION**|**DiskIndex**|Numéro de disque sous la forme d’un entier, en commençant par 0|  
|**DISKQUERY_LOGICALDISK**|**VolumeName**|Nom de volume|  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Nombre d’enregistrements retournés par la requête. Appelez **Update** avant d’appeler cette méthode.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propname--lpvariant-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propName, LPVARIANT value)  
 Cette méthode récupère la valeur d’une propriété à partir des résultats de la requête, comme indiqué dans le tableau 19.  

### <a name="table-19-hresult-getproperty"></a>Tableau 19. HRESULT GetProperty  

|**Paramètre**|**Description**|  
|-|-|  
|**Index**|Index de base zéro de l’enregistrement de résultat|  
|**propName**|Nom de la propriété, tel que « Size »|  
|**Valeur**|En retour, ce paramètre contient une valeur de type variant de la propriété|  

##### <a name="hresult-getcaptionsizet-index--lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Cette méthode récupère la légende pour un enregistrement qui est la même que la propriété **Caption**.  

#### <a name="iimagelist-interface"></a>Interface IImageList  

```  
__interface IImageList  
{  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    HImageList GetImageList(void);  
    int AddImage(HInstance hInstance, int resourceId);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **ImageList**. Vous récupérez une instance de ce composant à partir de l’interface **IListView**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Créer une liste d’images, gérée par ce composant. Appelez cette méthode une seule fois.  

##### <a name="himagelist-getimagelistvoid"></a>HImageList GetImageList(void)  
 Cette méthode retourne le handle de la liste d’images si vous devez effectuer d’autres opérations sur la liste d’images.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HInstance hInstance, int resourceId)  
 Ajouter une nouvelle image à la liste d’images à partir d’une ressource, comme indiqué dans le tableau 20.  

### <a name="table-20-hresult-iimagelist-interface"></a>Tableau 20. Interface HRESULT IImageList  

|**Paramètre**|**Description**|  
|-|-|  
|**hInstance**|Handle d’instance du module qui contient la ressource bitmap|  
|**resourceId**|ID de la ressource à charger dans la liste d’images|  

#### <a name="ilistview-interface"></a>Interface IListView  

```  
__interface IListView : IControl  
{  
    int AddItem([in] LPCTSTR text);  
    int AddColumn(int width, [in] LPCTSTR text);  
    HRESULT SetSubItem(int index, int column, [in] LPCTSTR text);  
    int GetWidth(void);  
    void SetExtendedStyle(DWORD style);  
    int GetSelectedItem(void);  
    HRESULT SelectItem(int index);  
    BOOL IsItemChecked(int index);  
    int GetItemCount(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  
    HRESULT SetImage(int index, int imageIndex);  
    HRESULT Clear(void);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **CheckBoxWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_LIST_VIEW**.  

##### <a name="int-additemin-lpctstr-text"></a>int AddItem([in] LPCTSTR text)  
 Ajouter une nouvelle ligne à la zone de liste. La méthode retourne l’index de l’élément qui vient d’être ajouté.  

##### <a name="int-addcolumnint-width-in-lpctstr-text"></a>int AddColumn(int width, [in] LPCTSTR text)  
 Ajouter une nouvelle colonne à l’affichage de liste.  

##### <a name="hresult-setsubitemint-index-int-column-in-lpctstr-text"></a>HRESULT SetSubItem(int index, int column, [in] LPCTSTR text)  
 Définir le texte dans une colonne autre que la première colonne de la zone de liste, comme indiqué dans le tableau 21.  

### <a name="table-21-hresult-setsubitem"></a>Tableau 21. HRESULT SetSubItem  

|**Paramètre**|**Description**|  
|-|-|  
|**index**|Index de l’élément de liste que vous souhaitez modifier|  
|**column**|Index de la colonne que vous souhaitez mettre à jour ; la première colonne est définie avec **AddItem**, tandis que la seconde colonne et les suivantes sont définies avec cette méthode|  
|**text**|Chaîne à afficher dans la colonne|  

##### <a name="int-getwidthvoid"></a>int GetWidth(void)  
 Cette méthode retourne la largeur de la zone de texte entière.  

##### <a name="void-setextendedstyledword-style"></a>void SetExtendedStyle(DWORD style)  
 Cette méthode vous permet de définir des styles étendus sur la zone de liste, par exemple :  

```  
m_pList->SetExtendedStyle(LVS_EX_FULLROWSELECT);  
```  

##### <a name="int-getselecteditemvoid"></a>int GetSelectedItem(void)  
 Cette méthode retourne l’index de l’élément d’affichage de liste actuellement sélectionné.  

##### <a name="hresult-selectitemint-index"></a>HRESULT SelectItem(int index)  
 Définir l’élément sélectionné dans la liste sur cet index.  

##### <a name="bool-isitemcheckedint-index"></a>BOOL IsItemChecked(int index)  
 Cette méthode retourne la valeur TRUE si un élément dans la liste est sélectionné. Cette méthode requiert que vous appeliez **SetExtendedStyle** pour définir le style de la case à cocher.  

##### <a name="int-getitemcountvoid"></a>int GetItemCount(void)  
 Cette méthode retourne le nombre d’éléments dans l’affichage de liste.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Créer une liste d’images et l’attacher à l’affichage de liste.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Ajouter une image à la liste d’images de l’affichage de liste. Vous devez d’abord appeler **CreateImageList**.  

##### <a name="hresult-setimageint-index-int-imageindex"></a>HRESULT SetImage(int index, int imageIndex)  
 Définir l’image à afficher sur le côté gauche d’un élément spécifique de l’affichage de liste.  

##### <a name="hresult-clearvoid"></a>HRESULT Clear(void)  
 Supprimer tous les éléments de l’affichage de liste.  

#### <a name="iprogressbar-interface"></a>Interface IProgressBar  

```  
__interface IProgressBar : IControl  
{  
    HRESULT SetPercentage(int position);  
    int GetPercentage(void);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **ProgressBarWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_PROGRESS_BAR**.  

##### <a name="hresult-setpercentageint-position"></a>HRESULT SetPercentage(int position)  
 Définir la position de la barre de progression à l’aide d’un nombre compris entre 0 et 100. Par défaut, les nouvelles barres de progression Win32® ont une plage maximale de 100.  

##### <a name="int-getpercentagevoid"></a>int GetPercentage(void)  
 Cette méthode retourne la position actuelle de la barre de progression.  

#### <a name="iradiobutton-interface"></a>Interface IRadioButton  

```  
__interface IRadioButton : IControl  
{  
public:  
    void SetGroup(int firstId, int lastId);  
    void CheckRadio(int id);  
    BOOL IsButtonChecked(int id);  
    void EnableRadio(int id, BOOL enable);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **RadioButtonWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_RADIO_BUTTON**.  

##### <a name="void-setgroupint-firstid-int-lastid"></a>void SetGroup(int firstId, int lastId)  
 Fournir le wrapper avec la plage de cases d’option qui doit être traitée en tant que groupe. Appelez cette méthode avant d’appeler **CheckRadio**.  

##### <a name="void-checkradioint-id"></a>void CheckRadio(int id)  
 Définir la case d’option spécifique en tant que bouton unique dans le groupe de cases d’option sélectionnées. Appelez **SetGroup** avant d’appeler cette méthode.  

##### <a name="bool-isbuttoncheckedint-id"></a>BOOL IsButtonChecked(int id)  
 Cette méthode retourne la valeur TRUE si la case d’option est sélectionnée, FALSE dans le cas contraire.  

##### <a name="void-enableradioint-id-bool-enable"></a>void EnableRadio(int id, BOOL enable)  
 Cette méthode active ou désactive une case d’option.  

#### <a name="istatictext-interface"></a>Interface IStaticText  

```  
__interface IStaticText : IControl  
{  
    HRESULT SetText([in] LPCTSTR pText);  
    HRESULT GetText([out, retval] LPBSTR pText);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **StaticTextWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_STATIC_TEXT**.  

##### <a name="hresult-settextin-lpctstr-ptext"></a>HRESULT SetText([in] LPCTSTR pText)  
 Définir le texte du contrôle.  

##### <a name="hresult-gettextout-retval-lpbstr-ptext"></a>HRESULT GetText([out, retval] LPBSTR pText)  
 Cette méthode retourne la valeur actuelle du texte du contrôle.  

####  <a name="ITaskinterface"></a> Interface ITask  

```  
__interface IControl : IUnknown  
{  
    HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings);  
    HRESULT Execute(LPDWORD pReturnCode);  
};  
```  

 Implémentez cette interface si vous souhaitez que votre composant soit disponible en tant que tâche dans la page de précontrôle, ou si vous souhaitez utiliser le composant **BackgroundTask** pour effectuer le travail sur un thread d’arrière-plan.  

 Voici les composants qui implémentent l’interface **ITask** :  

-   ID_ShellExecuteTask, L"Microsoft.Wizard.ShellExecuteTask"  

-   ID_CopyFilesTask, L"Microsoft.Wizard.CopyFilesTask"  

-   ID_ACPowerTask, L"Microsoft.OSDRefresh.ACPowerTask"  

-   ID_WiredNetworkTask, L"Microsoft.SharedPages.WiredNetworkTask"  

##### <a name="init"></a>Initial  

```  
HRESULT Init(IStringProperties *pProperties, ISettingsProperties *pTaskSettings)  
```  

 Si vous écrivez une tâche pour la page de précontrôle, appelez cette méthode pour initialiser votre tâche. Le fichier .config contient du code XML qui peut ressembler à ceci :  

```  
<Task DisplayName="Check Windows Scripting Host" Type="Microsoft.Wizard.ShellExecuteTask">  
  <Setter Property="filename">%windir%\system32\cscript.exe</Setter>  
  <Setter Property="parameters">Preflight\OSDCheckWSH.vbs</Setter>  
  <Setter Property="BitmapFilename">images\WinScriptHost.bmp</Setter>  
  <ExitCodes>  
    <ExitCode State="Success" Type="0" Value="0" Text="" />  
    <ExitCode State="Error" Type="-1" Value="*" Text="Windows Scripting Host not installed." />  
  </ExitCodes>  
</Task>  
```  

 Le paramètre **pProperties** fournit l’accès aux trois valeurs de setter, tandis que le paramètre **pTaskSettings** permet d’accéder à l’élément **Task** et aux enfants. La plupart des tâches ont uniquement besoin de lire des données à partir du paramètre **pProperties**.  

#####  <a name="Execute"></a> Execute  

```  
HRESULT Execute(LPDWORD pReturnCode)  
```  

 Voici où vous écrivez le code qui effectue la tâche. Cette méthode doit retourner **S_OK** en l’absence d’erreur, et elle peut retourner un autre **HRESULT** en cas d’erreur pendant l’exécution de la tâche. Les valeurs autres que **S_OK** retournées par cette méthode sont mises en correspondance avec les éléments <Error\> de la section <ExitCodes\> si vous utilisez la page de précontrôle.  

 Le paramètre **pReturnCode** doit être mis à jour avec un nombre qui indique l’état de la tâche. Ces valeurs sont mises en correspondance par la page de précontrôle avec les éléments <ExitCode\>.  

#### <a name="itreeview-interface"></a>Interface ITreeView  

```  
__interface ITreeView : IControl  
{  
    void EnableCheckboxes(void);  
    HRESULT CreateImageList(int width, int height, UINT flags);  
    int AddImage(HINSTANCE hInstance, int resourceId);  

    HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL);  
    void SetImage(HTREEITEM item, int image, int expandImage);  

    void Clear(void);  
    BOOL SetFirstVisible(HTREEITEM item);  
    BOOL SelectItem(HTREEITEM item);  
    void CheckItem(HTREEITEM item, UINT checkState);  
    HTREEITEM SelectedItem(void);  
    int SetItemHeight(SHORT height);  
    HRESULT EnableItem(HTREEITEM item, BOOL enable);  
    void Expand(HTREEITEM hItem, BOOL expand);  

    HTREEITEM GetChild(HTREEITEM hParent);  
    HTREEITEM GetParent(HTREEITEM hNode);  
    HTREEITEM GetNextItem(HTREEITEM hPrevious);  

    UINT IsChecked(HTREEITEM item);  
    BOOL IsEnabled(HTREEITEM item);  

    INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL *pCancel);  
    HRESULT SetEventHandler(ITreeViewEvent *pEventHandler);  

    void SetSelectedBackColor(COLORREF color);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **TreeViewWrapper**. Vous récupérez une instance de ce composant à l’aide de la fonction d’assistance **GetControlWrapper** avec le type **CONTROL_TREE_VIEW**.  

##### <a name="void-enablecheckboxesvoid"></a>void EnableCheckboxes(void)  
 Cette méthode coche les cases dans le contrôle arborescence en définissant le style **TVS_CHECKBOXES**.  

##### <a name="hresult-createimagelistint-width-int-height-uint-flags"></a>HRESULT CreateImageList(int width, int height, UINT flags)  
 Ajouter une nouvelle liste d’images au contrôle arborescence. Le paramètre **flags** est passé dans l’appel à la fonction Win32 **ImageList_Create**.  

##### <a name="int-addimagehinstance-hinstance-int-resourceid"></a>int AddImage(HINSTANCE hInstance, int resourceId)  
 Ajouter une image à la liste d’images à partir d’une ressource (**resourceId**) dans le module avec le handle d’instance **hInstance**.  

##### <a name="htreeitem-additemlpctstr-text-htreeitem-hparent--null"></a>HTREEITEM AddItem(LPCTSTR text, HTREEITEM hParent = NULL)  
 Ajouter un nœud à l’arborescence. Le nouveau nœud est ajouté au niveau supérieur si **hParent** a la valeur NULL. Dans le cas contraire, fournissez le handle à l’élément parent où vous souhaitez ajouter le nouvel élément. Cette méthode retourne le handle vers le nouvel élément.  

##### <a name="void-setimagehtreeitem-item-int-image-int-expandimage"></a>void SetImage(HTREEITEM item, int image, int expandImage)  
 Définir l’image à utiliser pour un élément d’arborescence. Vous pouvez définir l’image normale et l’image développée.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Supprimer tous les éléments de l’arborescence.  

##### <a name="bool-setfirstvisiblehtreeitem-item"></a>BOOL SetFirstVisible(HTREEITEM item)  
 Vérifier que l’élément d’arborescence est visible. L’arborescence défile si nécessaire pour afficher cet élément.  

##### <a name="bool-selectitemhtreeitem-item"></a>BOOL SelectItem(HTREEITEM item)  
 Définir l’élément actuellement sélectionné sur l’élément que vous fournissez. Vous pouvez ensuite appeler **SetFirstVisible** pour vous assurer que l’élément qui vient d’être sélectionné est visible.  

##### <a name="void-checkitemhtreeitem-item-uint-checkstate"></a>void CheckItem(HTREEITEM item, UINT checkState)  
 Schématiquement, cette méthode définit l’image à afficher pour la case à cocher dans l’arborescence. Ces images sont dans un contrôle **ImageList** distinct que gère l’arborescence. Par défaut, cette liste d’images comporte trois images, comme indiqué dans le tableau 22.  

### <a name="table-22void-checkitem-image-list-default"></a>Tableau 22. void CheckItem : configuration par défaut de la liste d’images  

|**checkState**|**Description**|  
|-|-|  
|**0**|Vide|  
|**1**|Supprimée|  
|**2**|Sélectionnée|  

##### <a name="htreeitem-selecteditemvoid"></a>HTREEITEM SelectedItem(void)  
 Cette méthode retourne le handle de l’élément d’arborescence actuellement sélectionné.  

##### <a name="int-setitemheightshort-height"></a>int SetItemHeight(SHORT height)  
 Cette méthode définit la hauteur de tous les éléments dans le contrôle arborescence en pixels. Elle retourne la hauteur précédente en pixels.  

##### <a name="hresult-enableitemhtreeitem-item-bool-enable"></a>HRESULT EnableItem(HTREEITEM item, BOOL enable)  
 Cette méthode active ou désactive un élément unique dans l’arborescence. Désactiver un élément ayant des enfants n’entraîne pas la désactivation de ces derniers.  

##### <a name="void-expandhtreeitem-hitem-bool-expand"></a>void Expand(HTREEITEM hItem, BOOL expand)  
 Cette méthode développe ou réduit un nœud de l’arborescence.  

##### <a name="htreeitem-getchildhtreeitem-hparent"></a>HTREEITEM GetChild(HTREEITEM hParent)  
 Cette méthode retourne le premier enfant d’un élément d’arborescence ou une valeur NULL s’il n’y a aucun enfant.  

##### <a name="htreeitem-getparenthtreeitem-hnode"></a>HTREEITEM GetParent(HTREEITEM hNode)  
 Cette méthode retourne le handle du parent d’un nœud dans l’arborescence ou la valeur NULL si le nœud est au niveau supérieur.  

##### <a name="htreeitem-getnextitemhtreeitem-hprevious"></a>HTREEITEM GetNextItem(HTREEITEM hPrevious)  
 Vous pouvez appeler cette méthode avec un handle retourné par **GetChild** pour itérer tous les enfants d’un nœud. Cette méthode retourne le frère suivant dans l’arborescence qui partage le même parent.  

##### <a name="uint-ischeckedhtreeitem-item"></a>UINT IsChecked(HTREEITEM item)  
 Cette méthode retourne **0** si le nœud d’arborescence n’est pas sélectionné, **1** sinon.  

##### <a name="bool-isenabledhtreeitem-item"></a>BOOL IsEnabled(HTREEITEM item)  
 Cette méthode retourne la valeur TRUE si le nœud d’arborescence est activé, FALSE sinon.  

##### <a name="intptr-commoncontroleventword-controlid-void-pinfo-bool-pcancel"></a>INT_PTR CommonControlEvent(WORD controlId, void* pInfo, BOOL \*pCancel)  
 Cette méthode est à usage interne uniquement.  

##### <a name="hresult-seteventhandleritreeviewevent-peventhandler"></a>HRESULT SetEventHandler(ITreeViewEvent \*pEventHandler)  
 Appelez cette méthode si vous souhaitez recevoir une notification quand l’élément sélectionné change ou que l’utilisateur change l’état d’activation d’un élément d’arborescence. Vous devez implémenter **ITreeViewEvent** dans votre composant pour recevoir ces rappels.  

##### <a name="void-setselectedbackcolorcolorref-color"></a>void SetSelectedBackColor(COLORREF color)  
 Définir la couleur d’arrière-plan utilisée pour l’élément sélectionné.  

#### <a name="iwmiiteration-interface"></a>Interface IWmiIteration  

```  
__interface IWmiIterator : IUnknown  
{  
    HRESULT Next(void);  
    HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Vous utilisez généralement cette interface, avec **IWmiRepository**, quand vous recourez à des appels WMI. L’interface **IWmiIteration** vous permet d’itérer les valeurs retournées par une requête.  

##### <a name="hresult-nextvoid"></a>HRESULT Next(void)  
 Accéder à l’élément suivant dans les résultats d’une requête, comme indiqué dans le tableau 23.  

### <a name="table-23-hresult-nextvoid-query-returns"></a>Tableau 23. HRESULT Next(void) : valeurs de retour de requête  

|**HRRESULT**|**Description**|  
|-|-|  
|**S_OK**|Accès au résultat suivant ; vous pouvez utiliser **GetProperty** pour récupérer les propriétés de ce résultat.|  
|**S_FALSE**|Il n’y a plus d’élément dans la liste.|  
|**E_NOT_SET**|Il n’y a aucun résultat de requête|  

##### <a name="hresult-getpropertylpctstr-propertyname-out-lpvariant-pvalue"></a>HRESULT GetProperty(LPCTSTR propertyName, [out] LPVARIANT pValue)  
 Cette méthode récupère la valeur d’une propriété à partir de l’enregistrement de résultat actuel, comme indiqué dans les tableaux 24 et 25.  

### <a name="table-24-hresult-getproperty"></a>Tableau 24. HRESULT GetProperty  

|**Paramètre**|**Description**|  
|-|-|  
|**propertyName**|Nom de la propriété à extraire|  
|**pValue**|Pointe vers une structure de type VARIANT qui, en retour, contient la valeur de propriété|  

### <a name="table-25-hresult-getproperty-result"></a>Tableau 25. HRESULT GetProperty : résultat  

|**HRESULT**|**Description**|  
|-|-|  
|**S_OK**|La valeur de propriété a été récupérée.|  
|**WBEM_E_NOT_FOUND**|Aucune propriété ne porte le nom indiqué.|  
|**E_NOT_VALID_STATE**|Aucun enregistrement actif.|  

> [!NOTE]
>  La méthode **GetProperty** peut retourner des codes d’erreur WMI autres que ceux répertoriés dans le tableau 25. Les valeurs répertoriées sont les résultats couramment retournés.  

#### <a name="iwmirepository-interface"></a>Interface IWmiRepository  

```  
__interface IWmiRepository : IUnknown  
{  
    HRESULT SetNamespace(LPCWSTR namespaceName);  
    HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **WmiRepository** (**ID_WmiRepository**).  

##### <a name="hresult-setnamespacelpcwstr-namespacename"></a>HRESULT SetNamespace(LPCWSTR namespaceName)  
 Cette méthode définit l’espace de noms WMI à utiliser pour la requête. Appelez cette méthode avant d’appeler **ExecQuery**. Si vous n’appelez pas cette méthode, l’espace de noms est root\cimv2. Cette méthode retourne toujours **S_OK**.  

##### <a name="hresult-execquerylpcwstr-query-out-iwmiiterator-ppiterator"></a>HRESULT ExecQuery(LPCWSTR query, [out] IWmiIterator **ppIterator)  
 Exécuter une requête sur l’espace de noms WMI défini par un appel à **SetNamespace**, comme indiqué dans les tableaux 26 et 27.  

### <a name="table-26-hresult-execquery"></a>Tableau 26. HRESULT ExecQuery  

|**Paramètre**|**Description**|  
|-|-|  
|**Query**|Chaîne de la requête WMI à exécuter|  
|**ppIterator**|Passez un pointeur vers un pointeur d’interface, qui, en retour, est rempli avec une interface, vous donnant accès aux résultats de la requête|  

### <a name="table-27-hresult-query-result"></a>Tableau 27. Résultat de la requête HRESULT  

|**HRESULT**|**Description**|  
|-|-|  
|**S_OK**|Requête réussie|  
|**Autre**|Si la requête n’a pas réussi, retourne un **HRESULT** WMI.|  

#### <a name="iformcontroller-interface"></a>Interface IFormController  

```  
__interface IFormController : IUnknown  
{  
    Init(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    SetPageInfo(ISettingsProperties *pPageInfo);  

    Validate(void);  

    AddToGroup(int groupControlId, int controlId);  
    UpdateCheckGroup(int groupControlId);  
    AddValidator(int controlId, IValidator *pValidator, IControl *pCOntrol = 0);  

    AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr);  
    DisableValidation(int controlId, BOOL disable);  

    AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type);  
    AddRadioGroup(LPCWSTR groupName, int radioControlId);  
    EnableRadioGroup(LPCWSTR groupName, BOOL enable);  
    InitFields(IFieldCallback *pFieldCallback = nullptr);  
    SaveFields(IFieldCallback *pFieldCallback = nullptr);  
    BOOL IsFieldDisabled(int controlId);  

    InitSection(LPCWSTR key, LPCWSTR sectionCaption);  
    AddSummaryItem(LPCWSTR first, LPCWSTR second);  
    SuppressLogValue(LPCWSTR tsVariableName);  
    SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption);  
    LoadText(int controlId, LPCWSTR tsVariableName);  

    void ControlEvent(WORD eventId, WORD controlId);  
    BOOL IsValid(void);  
 };  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Chaque page de l’Assistant UDI possède son propre contrôleur de formulaire qui implémente cette interface. Ce contrôleur vous permet de connecter les données de champ dans le fichier .config XML aux contrôles de votre page. Ensuite, le contrôleur de formulaire gère de nombreux détails pour vous.  

#####  <a name="SettingUptheForm"></a> Configuration du formulaire  
 En règle générale, configurez le contrôleur de formulaire dans la méthode **OnWindowCreated** de votre page. Cette opération implique généralement l’appel des méthodes indiquées dans le tableau 28.  

### <a name="table-28-onwindowcreated-method"></a>Tableau 28. Méthode OnWindowCreated  

|**Méthode**|**Description**|  
|-|-|  
|**Init**|Initialise le contrôleur de formulaire|  
|**AddField**|Fournit une connexion entre un champ dans le fichier .config XML qui est un nom de chaîne et un contrôle dans la boîte de dialogue de votre page qui est un ID|  
|**AddRadioGroup**|Permet de connecter une case d’option à un groupe et à un contrôle dans votre boîte de dialogue|  
|**AddToGroup**|Vous permet d’ajouter des contrôles « enfants » qui sont activés ou désactivés en compagnie de leur parent ou en fonction de la case d’option sélectionnée|  
|**InitFields**|Appelez cette méthode après avoir appelé toutes les méthodes **Add** pour configurer le formulaire|  
|**Validate**|Effectue la validation initiale|  

##### <a name="processing-form-events"></a>Traitement des événements de formulaire  
 Ajoutez l’appel suivant à votre méthode **OnControlEvent** :  

```  
Form()->ControlEvent(eventId, controlId);  
```  

 Cet appel transmet les événements au contrôleur de formulaire afin qu’il puisse traiter les événements liés au formulaire.  

##### <a name="save-form-data"></a>Enregistrer les données de formulaire  
 Dans la méthode **OnNextClicked**, appelez les méthodes de formulaire indiquées dans le tableau 29.  

### <a name="table-29-onnextclicked-method"></a>Tableau 29. Méthode OnNextClicked  

|**Méthode**|**Description**|  
|-|-|  
|**InitSection**|Fournit le nom de la section qui s’affiche dans la page **Summary** (Résumé) pour cette page|  
|**SaveFields**|Enregistrer les valeurs de champ dans des variables de séquence de tâches et dans la page **Summary** (Résumé)|  

#####  <a name="Init"></a> Init  

```  
HRESULT Init(IWizardPageView *pView, IWizardPageContainer *pContainer)  
```  

 Généralement, vous appelez cette méthode vers le début de la méthode **OnWindowCreated** de votre page. La commande doit ressembler à ceci :  

```  
Form()->Init(View(), Container());  
```  

##### <a name="setpageinfo"></a>SetPageInfo  

```  
HRESULT SetPageInfo(ISettingsProperties *pPageInfo)  
```  

 Cette méthode est appelée en interne, et vous ne devez pas l’appeler vous-même. Elle fournit le XML de la page au contrôleur de formulaire.  

##### <a name="validate"></a>Validate  

```  
HRESULT Validate(void)  
```  

 Cette méthode exécute tous les validateurs attachés aux contrôles. Si un validateur ne réussit pas, le contrôleur de formulaire affiche un message d’avertissement, désactive le bouton **Next** (Suivant), puis arrête le traitement de validation. En règle générale, vous devez uniquement appeler cette méthode à la fin de votre méthode **OnWindowCreated** ; elle retourne toujours **S_OK**.  

##### <a name="addtogroup"></a>AddToGroup  

```  
AddToGroup(int groupControlId, int controlId)  
```  

 Cette méthode ajoute un contrôle en tant « qu’enfant » d’une case à cocher ou d’une case d’option, comme indiqué dans le tableau 30. Tous ces contrôles enfants sont désactivés quand le contrôle parent n’est pas sélectionné. Cette méthode retourne toujours **S_OK**.  

### <a name="table-30-addtogroup"></a>Tableau 30. AddToGroup  

|**Paramètre**|**Description**|  
|-|-|  
|**groupControlId**|ID de la case à cocher ou de la case d’option qui contrôle l’état d’activation du contrôle enfant|  
|**Controlld**|ID du contrôle à ajouter en tant qu’enfant|  

##### <a name="updatecheckgroup"></a>UpdateCheckGroup  

```  
HRESULT UpdateCheckGroup(int groupControlId)  
```  

 Cette méthode met à jour l’état d’activation ou de désactivation des contrôles enfants d’un groupe en fonction de l’état du contrôle parent. En règle générale, il est inutile d’appeler cette méthode vous-même, car le contrôleur de formulaire l’appelle pour vous.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, IValidator *pValidator, IControl *pControl = 0)  
```  

 Appelez cette méthode uniquement si vous avez l’intention de créer un validateur dans du code plutôt qu’avec le XML. Cette méthode retourne toujours **S_OK**.  

##### <a name="addvalidator"></a>AddValidator  

```  
HRESULT AddValidator(int controlId, LPCWSTR validatorId, LPCWSTR message, IValidator **ppValidator = nullptr)  
```  

 Appelez cette méthode uniquement si vous avez l’intention de créer un validateur dans du code plutôt qu’avec le XML.  

##### <a name="disablevalidation"></a>DisableValidation  

```  
HRESULT DisableValidation(int controlId, BOOL disable)  
```  

 Appelez cette méthode pour restaurer une validation standard ou désactiver le validateur d’un contrôle explicitement, comme indiqué dans le tableau 31. Cette méthode est utile, par exemple, quand vous devez activer ou désactiver des règles pour des contrôles qui ne sont pas couverts par la validation de formulaire et que vous devez désactiver la validation d’un contrôle. En d’autres termes, normalement, vous n’appelez pas cette méthode. Cette méthode retourne toujours **S_OK**.  

### <a name="table-31-hresult-disablevalidation"></a>Tableau 31. HRESULT DisableValidation  

|**Paramètre**|**Description**|  
|-|-|  
|**controlId**|Contrôle pour lequel vous souhaitez activer ou désactiver la validation|  
|**Désactiver**|Définissez ce paramètre sur TRUE pour désactiver la validation ou sur FALSE pour restaurer la validation normale|  

#####  <a name="AddField"></a> AddField  

```  
HRESULT AddField(LPCWSTR fieldName, int controlId, BOOL suppressLog, DialogControlTypes type)  
```  

 Ajouter un mappage de contrôle entre le nom dans un élément **Field** du fichier XML .config et l’ID de contrôle dans la boîte de dialogue de votre page, comme indiqué dans le tableau 32. Vous devez appeler cette méthode avant d’appeler **InitFields**, car **InitFields** utilise ces informations. Cette méthode retourne toujours **S_OK**.  

### <a name="table-32-hresult-addfield"></a>Tableau 32. HRESULT AddField  

|**Paramètre**|**Description**|  
|-|-|  
|**Fieldname**|Nom du champ tel qu’il apparaît dans le XML de votre page|  
|**controlId**|ID du contrôle dans le modèle de boîte de dialogue de votre page|  
|**suppressLog**|Définissez ce paramètre sur TRUE si vous ne souhaitez pas que les valeurs de ce champ soient écrites dans le fichier journal ; définissez toujours ce paramètre sur TRUE pour les champs de code confidentiel ou de mot de passe|  
|**Type**|Type de contrôle, parmi les suivants :<br /><br /> -   **CONTROL_STATIC_TEXT**<br />-   **CONTROL_COMBO_BOX**<br />-   **CONTROL_LIST_VIEW**<br />-   **CONTROL_PROGRESS_BAR**<br />-   **CONTROL_GENERIC**<br />-   **CONTROL_RADIO_BUTTON**<br />-   **CONTROL_CHECK_BOX**<br />-   **CONTROL_TREE_VIEW**|  

#####  <a name="AddRadioGroup"></a> AddRadioGroup  

```  
HRESULT AddRadioGroup(LPCWSTR groupName, int radioControlId)  
```  

 Cette méthode ajoute un contrôle à un groupe de cases d’option nommé, comme indiqué dans le tableau 33. Vous devez l’appeler avant la méthode **InitFields**, car cette méthode utilise les attributs de l’élément **RadioGroup** pour contrôler les paramètres de tous les contrôles de case d’option dans le groupe. Les groupes de cases d’option peuvent être verrouillés, par exemple, afin que toutes les cases d’option soient désactivées, mais les contrôles enfants ne sont activés ou désactivés qu’en fonction de la case d’option sélectionnée. Cette méthode retourne toujours **S_OK**.  

### <a name="table-33-hresult-addradiogroup"></a>Tableau 33. HRESULT AddRadioGroup  

|**Paramètre**|**Description**|  
|-|-|  
|**groupName**|Chaîne qui définit un groupe de cases d’option dans cette page|  
|**radioControlId**|ID d’une case d’option unique à ajouter à ce groupe|  

##### <a name="enableradiogroup"></a>EnableRadioGroup  

```  
HRESULT EnableRadioGroup(LPCWSTR groupName, BOOL enable)  
```  

 Cette méthode permet d’activer ou de désactiver un groupe de cases d’option entier. La désactivation d’un groupe de cases d’option désactive tous les contrôles de case d’option dans le groupe, ainsi que les enfants de ces cases d’option qui ont été ajoutés avec **AddToGroup**. Consultez les tableaux 34 et 35.  

### <a name="table-34-enableradiogroup"></a>Tableau 34. EnableRadioGroup  

|**Paramètre**|**Description**|  
|-|-|  
|**groupName**|Nom d’un groupe de cases d’option que vous avez déjà défini par un appel à **AddRadioGroup**|  
|**Activer**|Définissez ce paramètre sur TRUE pour activer le groupe de cases d’option, ou sur FALSE pour désactiver le groupe|  

### <a name="table-35-hresult-enableradiogroup"></a>Tableau 35. HRESULT EnableRadioGroup  

|**HRESULT**|**Description**|  
|-|-|  
|**S_OK**|Groupe activé ou désactivé|  
|**E_INVALIDARG**|Aucun groupe de cases d’option ne porte le nom que vous avez indiqué|  

#####  <a name="InitFields"></a> InitFields  

```  
HRESULT InitFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Avant d’appeler cette méthode, appelez **AddField** pour chaque champ que le XML peut contrôler. Cette méthode retourne toujours **S_OK**.  

 Le paramètre **pFieldCallback** est facultatif. Si vous le fournissez, le contrôleur de formulaire appelle **SetFieldDefault** pour les contrôles qui ne sont ni **CONTROL_STATIC_TEXT**, ni **CONTROL_CHECK_BOX**. Ce comportement vous permet de récupérer une valeur par défaut à partir du XML et de la définir dans le contrôle vous-même.  

#####  <a name="SaveFields"></a> SaveFields  

```  
HRESULT SaveFields(IFieldCallback *pFieldCallback = nullptr)  
```  

 Cette méthode enregistre les valeurs de champs dans les variables de séquence de tâches et dans les données de synthèse qui s’affichent dans la page **Summary** (Résumé). En fournissant un pointeur dans **pFieldCallback**, vous pouvez gérer l’enregistrement des valeurs pour les contrôles ne prenant pas en charge **CONTROL_STATIC_TEXT**.  

##### <a name="isfielddisabled"></a>IsFieldDisabled  

```  
BOOL IsFieldDisabled(int controlId)  
```  

 Cette méthode vous permet de déterminer si un champ a été désactivé dans le XML.  

#####  <a name="InitSection"></a> InitSection  

```  
HRESULT InitSection(LPCWSTR key, LPCWSTR sectionCaption)  
```  

 Cette méthode initialise les données de synthèse qui s’affichent dans la page **Summary** (Résumé), comme indiqué dans le tableau 36. Appelez cette méthode dans votre méthode **OnNextClicked** avant d’appeler **SaveFields**. Cette méthode retourne toujours **S_OK**.  

### <a name="table-36-hresult-initsection"></a>Tableau 36. HRESULT InitSection  

|**Paramètre**|**Description**|  
|-|-|  
|**Key**|Ce paramètre doit être propre à votre page. Il est utilisé pour garantir que chaque page possède ses propres informations de synthèse.|  
|**sectionCaption**|En-tête qui s’affiche dans la page **Summary** (Résumé) pour les informations de synthèse de cette page En général, vous utilisez **DisplayName()** comme valeur pour ce paramètre.|  

##### <a name="addsummaryitem"></a>AddSummaryItem  

```  
HRESULT AddSummaryItem(LPCWSTR first, LPCWSTR second)  
```  

 Cette méthode vous permet d’ajouter des éléments de synthèse à la page **Summary** (Résumé) au-dessus et au-delà des éléments définis avec le XML. Consultez le tableau 37.  

### <a name="table-37-hresult-addsummaryitem"></a>Tableau 37. HRESULT AddSummaryItem  

|**Paramètre**|**Description**|  
|-|-|  
|**First**|Légende de l’élément de synthèse, qui est affichée sur le côté gauche|  
|**Second**|Valeur qui s’affiche sur le côté droit|  

##### <a name="suppresslogvalue"></a>SuppressLogValue  

```  
HRESULT SuppressLogValue(LPCWSTR tsVariableName)  
```  

 Appelez cette méthode pour les variables de séquence de tâches dont vous ne souhaitez pas que les valeurs soient écrites dans le fichier journal. Appelez cette méthode pour les variables de séquence de tâches qui stockent les mots de passe, les codes confidentiels ou d’autres valeurs sensibles qu’un utilisateur est susceptible d’entrer.  

##### <a name="savetext"></a>SaveText  

```  
HRESULT SaveText(int controlId, LPCWSTR tsVariableName, LPCWSTR summaryCaption)  
```  

 Cette méthode enregistre la valeur d’un contrôle de texte dans une variable de séquence de tâches et dans la section de synthèse. En règle générale, il est inutile d’appeler cette méthode vous-même, car le contrôleur de formulaire s’en charge pour tous les champs. Consultez le tableau 38.  

### <a name="table-38-hresult-savetext"></a>Tableau 38. HRESULT SaveText  

|**Paramètre**|**Description**|  
|-|-|  
|**controlId**|ID de la zone de texte qui contient la valeur à enregistrer (ou tout autre contrôle qui retourne du texte)|  
|**tsVariableName**|Nom de la variable de séquence de tâches à modifier|  
|**summaryCaption**|Légende dans la page **Summary** (Résumé) pour cette valeur|  

##### <a name="loadtext"></a>LoadText  

```  
HRESULT LoadText(int controlId, LPCWSTR tsVariableName)  
```  

 Cette méthode lit la valeur d’une variable de séquence de tâches et définit la zone de texte sur cette valeur.  

##### <a name="controlevent"></a>ControlEvent  

```  
void ControlEvent(WORD eventId, WORD controlId)  
```  

 Appelez cette méthode sur votre méthode **OnControlEvent** pour vous assurer que le contrôleur de formulaire peut traiter les événements de contrôle, ce qu’il doit faire pour fonctionner correctement. Les valeurs que vous passez à cette méthode sont les mêmes que celles passées à la méthode **OnControlEvent**.  

##### <a name="isvalid"></a>IsValid  

```  
BOOL IsValid(void)  
```  

 Cette méthode retourne l’état de la validation la plus récente du formulaire. Si un des validateurs de contrôle a signalé une erreur, cette méthode retourne FALSE. En d’autres termes, elle retourne TRUE uniquement si tous les contrôles dans la page sont valides.  

#### <a name="ivalidator-interface"></a>Interface IValidator  

```  
__interface IValidator : IUnknown  
{  
    HRESULT Init(IControl *pControl, LPCTSTR message);  
    HRESULT Init(IControl *pControl, IWizardPageContainer *pContainer, IStringProperties *pProperties);  
    BOOL, IsValid(LPBSTR pMessage);  
    HRESULT SetProperty(int propertyId, LPVARIANT pValue);  
    HRESULT SetProperty(int propertyId, IUnknown *pUnknown);  
    HRESULT SetProperty)(int propertyId, LPCTSTR pValue);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Les *validateurs* sont des composants qui peuvent valider un contrôle spécifique dans votre page. Le moyen le plus simple pour implémenter un validateur consiste à en faire une sous-classe de la classe **BaseValidator**, qui est définie dans le fichier d’en-tête BaseValidator.h.  

##### <a name="hresult-initicontrol-pcontrol-lpctstr-message"></a>HRESULT Init(IControl \*pControl, LPCTSTR message)  
 Si vous créez un validateur dans le code, vous pouvez appeler cette méthode pour initialiser le validateur. Consultez le tableau 39.  

### <a name="table-39-hresult-init"></a>Tableau 39. HRESULT Init  

|**Paramètre**|**Description**|  
|-|-|  
|**pControl**|Contrôle que votre validateur doit valider|  
|**Message**|Message à afficher dans la page si le contrôle n’est pas valide|  

##### <a name="hresult-initicontrol-pcontrol-iwizardpagecontainer-pcontainer-istringproperties-pproperties"></a>HRESULT Init(IControl \*pControl, IWizardPageContainer \*pContainer, IStringProperties \*pProperties)  
 Le contrôleur de formulaire appelle cette méthode pour initialiser les validateurs qu’il crée en fonction du XML de la page. Consultez le tableau 40.  

### <a name="table-40-hresult-init-method"></a>Tableau 40. HRESULT : méthode Init  

|**Paramètre**|**Description**|  
|-|-|  
|**pControl**|Contrôle que votre validateur doit valider|  
|**pContainer**|Si votre validateur a besoin d’accéder au journaliseur ou de créer d’autres composants|  
|**pProperties**|Fournit l’accès aux propriétés (éléments setter) pour votre validateur|  

##### <a name="bool-isvalidlpbstr-pmessage"></a>BOOL, IsValid(LPBSTR pMessage)  
 Cette méthode retourne la valeur TRUE si le contrôle est valide, FALSE sinon. En retour, **pMessage** doit être rempli avec un nouveau **BSTR** qui contient le message à afficher quand le contrôle n’est pas valide.  

##### <a name="hresult-setpropertyint-propertyid-lpvariant-pvalue"></a>HRESULT SetProperty(int propertyId, LPVARIANT pValue)  
 Vous pouvez implémenter cette méthode si vous avez besoin de valeurs supplémentaires qui ne sont pas fournies dans le XML.  

##### <a name="hresult-setpropertyint-propertyid-iunknown-punknown"></a>HRESULT SetProperty(int propertyId, IUnknown \*pUnknown)  
 Vous pouvez implémenter cette méthode si vous avez besoin de valeurs supplémentaires qui ne sont pas fournies dans le XML.  

##### <a name="hresult-setpropertyint-propertyid-lpctstr-pvalue"></a>HRESULT SetProperty)(int propertyId, LPCTSTR pValue)  
 Vous pouvez implémenter cette méthode si vous avez besoin de valeurs supplémentaires qui ne sont pas fournies dans le XML.  

#### <a name="iregex-interface"></a>Interface IRegEx  

```  
__interface IRegEx : IUnknown  
{  
    BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex);  
    HRESULT GetMatch(size_t index, LPBSTR pValue);  
};  
```  

 Cette méthode est implémentée par le composant **ID_Regex** (IRegex.h) et prend en charge le traitement des expressions régulières.  

##### <a name="bool-matchesregexlpctstr-input-lpctstr-regex"></a>BOOL MatchesRegex(LPCTSTR input, LPCTSTR regex)  
 Cette méthode exécute l’expression régulière sur le texte d’entrée. Plus précisément, elle utilise la fonction **regex_match** de la bibliothèque standard C++. La méthode retourne la valeur TRUE si des correspondances ont été trouvées, FALSE sinon.  

##### <a name="hresult-getmatchsizet-index-lpbstr-pvalue"></a>HRESULT GetMatch(size_t index, LPBSTR pValue)  
 Cette méthode vous permet de récupérer les correspondances à partir de l’appel de **MatchesRegex** le plus récent. Notez que cette méthode ne comporte aucun traitement d’erreur ; elle retourne **S_OK** ou lève une exception.  

#### <a name="isummaryinfo-interface"></a>Interface ISummaryInfo  

```  
__interface ISummaryInfo : IUnknown  
{  
    size_t Count(void);  
    HRESULT Clear(void);  
    HRESULT AddInfo(LPCTSTR pFirst, LPCTSTR pSecond);  
    HRESULT GetInfo(size_t index, LPBSTR pFirst, LPBSTR pSecond);  
    HRESULT GetCaption(LPBSTR pCaption);  
    HRESULT SetCaption(LPCTSTR caption);  
};  
```  

 Vous ne devez pas utiliser cette interface directement. À la place, utilisez **IFormController**.  

#### <a name="isummarybag"></a>ISummaryBag  

```  
__interface ISummaryBag : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetInfoByIndex(size_t index, [out] ISummaryInfo **ppSummary);  
    HRESULT GetInfoByKey(LPCTSTR key, [out] ISummaryInfo **ppSummary);  
};  
```  

 Vous ne devez pas utiliser cette interface directement. À la place, utilisez **IFormController**.  

#### <a name="itsvariablebag-interface"></a>Interface ITSVariableBag  

```  
__interface ITSVariableBag : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue);  
    void Clear(void);  
    HRESULT Remove([in] LPCTSTR variableName);  
    HRESULT SuppressLogValue([in] LPCTSTR variableName);  
    void Save(void);  
};  
```  

 Cette interface fournit l’accès aux variables de séquence de tâches. Vous pouvez accéder à cette interface à l’aide de la méthode **TSVariables()** de votre page.  

##### <a name="void-getvaluein-lpctstr-variablename-out-lpbstr-pvalue"></a>void GetValue([in] LPCTSTR variableName, [out] LPBSTR pValue)  
 Cette méthode lit la valeur d’une variable de séquence de tâches.  

> [!NOTE]
>  Les valeurs sont mises en cache après la première lecture.  

##### <a name="void-setvaluein-lpctstr-variablename-in-lpctstr-pvalue"></a>void SetValue([in] LPCTSTR variableName, [in] LPCTSTR pValue)  
 Cette méthode définit la valeur d’une variable de séquence de tâches. Cette valeur est enregistrée en mémoire. Les valeurs de séquence de tâches sont écrites quand vous cliquez sur **Finish** (Terminer) dans l’Assistant UDI.  

##### <a name="void-clearvoid"></a>void Clear(void)  
 Cette méthode supprime toutes les valeurs de séquence de tâches qui ont été enregistrées en mémoire.  

##### <a name="hresult-removein-lpctstr-variablename"></a>HRESULT Remove([in] LPCTSTR variableName)  
 Cette méthode supprime de la mémoire une valeur de séquence de tâches spécifique. La prochaine fois que vous appelez **GetValue** avec le même nom de séquence de tâches, la méthode tente de la récupérer de la séquence de tâches.  

##### <a name="hresult-suppresslogvaluein-lpctstr-variablename"></a>HRESULT SuppressLogValue([in] LPCTSTR variableName)  
 Chaque fois que des variables de séquence de tâches sont écrites, comme quand vous cliquez sur **Finish** (Terminer) dans l’Assistant UDI, les noms et les valeurs sont écrits dans le fichier journal. Appelez cette méthode pour supprimer l’enregistrement des valeurs sensibles, telles que les mots de passe ou les codes confidentiels, pour une variable de séquence de tâches spécifique.  

##### <a name="void-savevoid"></a>void Save(void)  
 Cette méthode enregistre toutes les valeurs de séquence de tâches qui ont été définies avec les appels de **SetValue**.  

#### <a name="itsvariablerepository-interface"></a>ITSVariableRepository Interface  

```  
__interface ITSVariableRepository : IUnknown  
{  
    void GetValue([in] LPCTSTR variableName, BOOL logValue, [out] LPBSTR pValue);  
    void SetValue([in] LPCTSTR variableName, BOOL logValue, [in] LPCTSTR value);  
};  
```  

 Cette interface est destinée à une utilisation interne par **TSVariableBag** pour la lecture et l’écriture de variables de séquence de tâches.  

#### <a name="iwizardfinish-interface"></a>Interface IWizardFinish  

```  
__interface IWizardFinish : IUnknown  
{  
    HRESULT Canceled(void);  
    HRESULT Finished(void);  
};  
```  

 Cette interface est utile dans les scénarios avancés où vous souhaitez effectuer un traitement supplémentaire quand vous cliquez sur **Finish** (Terminer) ou **Cancel** (Annuler) dans l’Assistant UDI. L’Assistant UDI contient une tâche **Finish** (Terminer) qui enregistre les variables de séquence de tâches quand vous cliquez sur **Finish** (Terminer). Si vous annulez l’Assistant, la tâche se contente de définir la variable de séquence de tâches **OSDSetupWizCancelled** sur la valeur TRUE ; elle n’enregistre pas les modifications apportées à d’autres variables de séquence de tâches.  

 Si vous créez votre propre composant de fin, vous devez l’inscrire avec du code similaire à celui-ci :  

```  
Register<MyFinishTaskFactory>(ID_MyFinishTask, pRegistry);  

PWizardFinish pFinish;  
CreateInstance(pRegistry, ID_MyFinishTask, &pFinish);  

PWizardFinishService pService;  
GetService<IWizardFinishService>(pRegistry, &pService);  

pService->Register(pFinish);  
```  

#### <a name="ibindablelist-interface"></a>Interface IBindableList  

```  
__interface IBindableList : IUnknown  
{  
    size_t Count(void);  
    HRESULT GetCaption(size_t index, LPBSTR pCaption);  
};  
```  

 Implémentez cette interface si vous souhaitez lier un composant de source de données à une zone de liste modifiable en appelant sa méthode **Bind**.  

##### <a name="sizet-countvoid"></a>size_t Count(void)  
 Cette méthode retourne le nombre d’éléments dans la liste.  

##### <a name="hresult-getcaptionsizet-index-lpbstr-pcaption"></a>HRESULT GetCaption(size_t index, LPBSTR pCaption)  
 Cette méthode retourne la légende de l’élément à un index spécifique.  

#### <a name="idatanodes-interface"></a>Interface IDataNodes  

```  
__interface IDataNodes : IUnknown  
{  
    size_t Count();  
    HRESULT SetCaptionProperty(LPCTSTR captionProperty);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue);  
    HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode);  
};  
```  

 Cette interface fournit l’accès à des données hiérarchiques qui peuvent être enregistrées dans une page. Vous obtenez cette interface par le biais de méthodes sur l’interface **ISettingsProperties**, qui est disponible pour votre page par l’intermédiaire de la méthode **Settings**.  

 Les données du XML d’une page peuvent ressembler à ceci  

```  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  
```  

 Appeler **Settings()->GetDataNode(L"Network", &pData)** vous procure une instance **IDataNodes** avec deux éléments de données (ayant chacun deux propriétés).  

##### <a name="sizet-count"></a>size_t Count()  
 Cette méthode retourne le nombre d’éléments **DataItem**.  

##### <a name="hresult-setcaptionpropertylpctstr-captionproperty"></a>HRESULT SetCaptionProperty(LPCTSTR captionProperty)  
 Le composant qui prend en charge cette interface prend également en charge **IBindableList**, ce qui facilite le remplissage d’une zone de liste modifiable avec des données à partir du XML de la page. Cette méthode contrôle la propriété (setter) qui, dans chaque élément **DataItem**, doit être utilisée pour cette liaison. Par exemple, si vous appelez cette méthode avec **DisplayName**, elle utilise cette propriété setter pour la liaison de données. La zone de liste modifiable contient alors **Public** et **Dev Team** comme éléments.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-out-lpbstr-propertyvalue"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, [out] LPBSTR propertyValue)  
 Cette méthode obtient une propriété d’un des éléments **DataItem**. Consultez les tableaux 41 et 42.  

### <a name="table-41-dataitem-getproperty"></a>Tableau 41. DataItem GetProperty  

|**Paramètre**|**Description**|  
|-|-|  
|**Index**|Valeur d’index (à partir de 0) du **DataItem** dont vous souhaitez récupérer une valeur de propriété|  
|**propertyName**|Nom de la propriété setter dont vous souhaitez récupérer une valeur|  
|**propertyValue**|En retour, contient la valeur de chaîne d’une propriété|  

### <a name="table-42-hresult-getproperty"></a>Tableau 42. HRESULT GetProperty  

|||  
|-|-|  
|**HRESULT**|**Description**|  
|**S_OK**|La propriété a été récupérée.|  
|**E_INVALIDARG**|L’index se trouve au-delà de la fin du tableau.|  

##### <a name="hresult-getnodesizet-index-out-isettingsproperties-ppnode"></a>HRESULT GetNode(size_t index, [out] ISettingsProperties **ppNode)  
 Cette méthode est similaire à **GetProperty**, mais au lieu de retourner une valeur d’un **DataItem**, elle retourne le **DataItem** entier wrappé dans une interface  **ISettingsProperties**. Consultez les tableaux 43 et 44.  

### <a name="table-43-hresult-getnode"></a>Tableau 43. HRESULT GetNode  

|**Paramètre**|**Description**|  
|-|-|  
|Index|Valeur d’index (à partir de 0) du **DataItem** dont vous souhaitez récupérer une valeur de propriété|  
|**ppNode**|À la sortie, l’interface **ISettingsProperties** qui wrappe le nœud **DataItem**|  

### <a name="table-44-hresult-getnode-results"></a>Tableau 44. HRESULT GetNode : résultats  

|**HRESULT**|**Description**|  
|-|-|  
|**S_OK**|Le nœud a été récupéré.|  
|**E_INVALIDARG**|L’index se trouve au-delà de la fin du tableau.|  

#### <a name="ifactoryregistry-interface"></a>Interface IFactoryRegistry  

```  
__interface IFactoryRegistry : IUnknown  
{  
    void Register(LPCTSTR type,  IClassFactory *pFactory);  
    HRESULT LoadAndRegister(LPCTSTR dllName, ILogger *pLogger);  
    BOOL Contains(LPCTSTR type);  
    HRESULT GetFactory(LPCTSTR type,  IClassFactory **ppFactory);  
    HRESULT CreateInstance(LPCTSTR type,  IUnknown **ppInstance);  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
    HRESULT RegisterService(REFGUID iid, IUnknown *pService);  
    HRESULT GetService(REFGUID iid,  IUnknown **ppService);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Quand vous créez une page personnalisée, au minimum vous devez créer une *fabrique de page* : une classe qui implémente **IClassFactory**. (Vous pouvez utiliser **ClassFactoryImpl** comme classe de base pour votre fabrique.)  

##### <a name="void-registerlpctstr-type--iclassfactory-pfactory"></a>void Register(LPCTSTR type, IClassFactory \*pFactory)  
 Cette méthode inscrit une fabrique de classe auprès du registre. Consultez le tableau 45.  

### <a name="table-45-iclassfactory-void-register"></a>Tableau 45. IClassFactory void Register  

|**Paramètre**|**Description**|  
|-|-|  
|**Type**|Chaîne qui identifie la fabrique que vous inscrivez ; en règle générale, vous pouvez inclure le nom de votre société dans la chaîne de ce paramètre pour en assurer l’unicité|  
|**pFactory**|Pointeur vers une instance de la fabrique de classe|  

##### <a name="hresult-loadandregisterlpctstr-dllname-ilogger-plogger"></a>HRESULT LoadAndRegister(LPCTSTR dllName, ILogger \*pLogger)  
 Cette méthode est à usage interne uniquement.  

##### <a name="bool-containslpctstr-type"></a>BOOL Contains(LPCTSTR type)  
 Cette méthode est généralement à usage interne. Elle vérifie si une fabrique de classe a été inscrite pour un type.  

##### <a name="hresult-getfactorylpctstr-type--iclassfactory-ppfactory"></a>HRESULT GetFactory(LPCTSTR type, IClassFactory **ppFactory)  
 Cette méthode vous permet de récupérer la fabrique de classe. En règle générale, vous appelez **CreateInstance**. Toutefois, si vous vous apprêtez à créer un même composant en quantité élevée, il est plus efficace de récupérer la fabrique, puis de lui demander de créer les instances à votre place.  

##### <a name="hresult-createinstancelpctstr-type--iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, IUnknown **ppInstance)  
 Cette méthode crée une instance d’un composant, à partir de son type. Utilisez la méthode de modèle **CreateInstance** à la place, qui permet la création d’objets de type sécurisé.  

##### <a name="hresult-setcontaineriwizardpagecontainer-pcontainer"></a>HRESULT SetContainer(IWizardPageContainer \*pContainer)  
 Cette méthode est à usage interne uniquement.  

##### <a name="hresult-registerservicerefguid-iid-iunknown-pservice"></a>HRESULT RegisterService(REFGUID iid, IUnknown \*pService)  
 Les *services* sont des instances uniques d’un composant qui peuvent être utilisées à divers endroits. Vous pouvez utiliser cette méthode pour inscrire un service sur une page, puis récupérer la même instance d’une autre page.  

##### <a name="hresult-getservicerefguid-iid--iunknown-ppservice"></a>HRESULT GetService(REFGUID iid, IUnknown **ppService)  
 Cette méthode récupère un service qui a été inscrit par un appel à RegisterService.  

##### <a name="hresult-setlanguagelangid-languageid"></a>HRESULT SetLanguage(LANGID languageId)  
 Cette méthode définit la langue de l’Assistant UDI sur l’identificateur de langue que vous avez fourni dans le paramètre **languageId**.  

##### <a name="langid-getlanguage"></a>LANGID GetLanguage()  
 Cette méthode retourne la valeur de l’identificateur de langue que vous avez fourni avec le paramètre de ligne de commande **/locale** pour l’Assistant UDI. La méthode retourne l’une des valeurs suivantes :  

-   Valeur de l’identificateur de langue fourni avec le paramètre de ligne de commande **/locale**  

-   0, si vous n’avez pas fourni le paramètre de ligne de commande **/locale**  

#### <a name="ilogger-interface"></a>Interface ILogger  

```  
__interface ILogger : IUnknown  
{  
    HRESULT Init(LPCWSTR logFilename);  
    HRESULT MoveLog(LPCWSTR logFilename);  
    HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message);  
    HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message);  
    HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message);  
    HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Normal(LPCTSTR component, LPCTSTR message);      
    HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Verbose(LPCTSTR component, LPCTSTR message);  
    HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2);  
    HRESULT Debug(LPCWSTR component, LPCWSTR message);  
    HRESULT EnableDebug(BOOL debug);  
    HRESULT Close(void);  
    HRESULT GetLogFilename(LPBSTR pFilename);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 L’Assistant UDI journalise les informations dans un fichier journal, qui vous permet de résoudre les problèmes détectés dans le champ. Il est judicieux que vos pages journalisent les informations. Vous pouvez obtenir un pointeur vers cette interface à partir de votre page à l’aide de la méthode **Logger()** de la page. Les lignes dans le fichier journal contiennent un numéro de « niveau » qui représente les messages d’erreur, normaux, détaillés ou de débogage.  

> [!NOTE]
>  Les messages de débogage ne sont pas enregistrés dans le fichier journal, sauf si la prise en charge du débogage est activée. Vous pouvez activer la prise en charge du débogage en ajoutant la ligne suivante à l’élément **Style** dans le fichier .config :  

```  
<Setter Property="debug">true</Setter>  
```  

##### <a name="init"></a>Initial  

```  
HRESULT Init(LPCWSTR logFilename)  
```  

 Cette méthode est à usage interne uniquement.  

##### <a name="movelog"></a>MoveLog  

```  
HRESULT MoveLog(LPCWSTR logFilename)  
```  

 Cette méthode est à usage interne uniquement.  

##### <a name="logbase"></a>LogBase  

```  
HRESULT LogBase(EMessageType messageType, LPCTSTR component, SYSTEMTIME eventTime, LPCTSTR message)  
```  

 Cette méthode est à usage interne uniquement.  

##### <a name="log"></a>Journal  

```  
HRESULT Log(EMessageType messageType, LPCTSTR component, LPCTSTR message)  
```  

 Cette méthode est à usage interne uniquement.  

##### <a name="error"></a>Erreur  

```  
HRESULT Error(HRESULT error, LPCTSTR component, LPCTSTR message)  
```  

 Appelez cette méthode pour journaliser des informations sur une erreur. Consultez le tableau 46.  

### <a name="table-46-hresult-error"></a>Tableau 46. HRESULT Error  

|**Paramètre**|**Description**|  
|-|-|  
|**Erreur**|Code d’erreur retourné par un appel (ce code s’affiche dans l’entrée du journal en tant que numéro.)|  
|**Composant**|Chaîne qui identifie la source de l’erreur, généralement votre page ou le composant que vous avez écrit|  
|**Message**|Message qui explique ce qui a provoqué l’erreur|  

#####  <a name="Error2"></a> Error2  

```  
HRESULT Error2(HRESULT error, LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Cette méthode est comparable à la méthode **Error**, mais vous permet de fournir un message en deux parties. Le message final a « message », puis « message2 » dans le fichier de sortie. Il s’agit simplement d’une méthode pratique.  

##### <a name="normal"></a>Normal  

```  
HRESULT Normal(LPCTSTR component, LPCTSTR message)  
```  

 Cette méthode journalise un message normal. Consultez la description de la méthode [Error](#Error) pour en savoir plus sur les paramètres.  

##### <a name="normal2"></a>Normal2  

```  
HRESULT Normal2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Cette méthode journalise un message normal. Consultez la description de la méthode [Error2](#Error2) pour en savoir plus sur les paramètres.  

##### <a name="verbose"></a>Verbose  

```  
HRESULT Verbose(LPCTSTR component, LPCTSTR message)  
```  

 Cette méthode journalise un message détaillé. Consultez la description de la méthode [Error](#Error) pour en savoir plus sur les paramètres.  

##### <a name="verbose2"></a>Verbose2  

```  
HRESULT Verbose2(LPCTSTR component, LPCTSTR message, LPCTSTR message2)  
```  

 Cette méthode journalise un message détaillé. Consultez la description de la méthode [Error2](#Error2) pour en savoir plus sur les paramètres.  

##### <a name="debug"></a>Débogage  

```  
HRESULT Debug(LPCWSTR component, LPCWSTR message)  
```  

 Cette méthode journalise un message de débogage. Consultez la description de la méthode [Error](#Error) pour en savoir plus sur les paramètres. Les messages de débogage ne sont pas enregistrés dans le fichier sauf si le débogage est activé. Pour plus de détails, consultez la section Vue d’ensemble.  

##### <a name="enabledebug"></a>EnableDebug  

```  
HRESULT EnableDebug(BOOL debug)  
```  

 Cette méthode est à usage interne uniquement.  

##### <a name="close"></a>Fermer  

```  
HRESULT Close(void)  
```  

 Cette méthode est à usage interne uniquement.  

##### <a name="getlogfilename"></a>GetLogFilename  

```  
HRESULT GetLogFilename(LPBSTR pFilename)  
```  

 Cette méthode récupère le nom du fichier journal.  

#### <a name="iorientation-interface"></a>Interface IOrientation  

```  
__interface IOrientation : IUnknown  
{  
    void SetController(IWizardDialogController *pController);  
    int AddPage(LPCTSTR name);  
    void SelectPage(int index);  
};  
```  

 Cette interface est à usage interne uniquement.  

#### <a name="isettings-interface"></a>Interface ISettings  

```  
__interface ISettings : IUnknown  
{  
    int NumDlls();  
    int NumPages();  

    HRESULT SetStage(LPCWSTR stageName);  
    HRESULT GetDllName(long index, __out LPBSTR pDllName);  
    HRESULT GetPageInfo(long index, __out ISettingsProperties **ppPageInfo);  
    HRESULT GetStyle(__out ISettingsProperties **ppStyleInfo);  
};  
```  

 Cette interface est à usage interne uniquement.  

#### <a name="isettingsproperties-interface"></a>Interface ISettingsProperties  

```  
__interface ISettingsProperties : IUnknown  
{  
    HRESULT GetAttribute(LPCTSTR attributeName, __out LPBSTR attributeValue);  
    IStringProperties * Properties();  
   RESULT SelectNodes(LPCTSTR xPath, __out IXMLDOMNodeList **ppList);  
    HRESULT SelectSingleNode(LPCTSTR xPath, __out IXMLDOMNode **ppNode);  
    HRESULT GetDataNode(LPCTSTR name, __out ISettingsProperties **ppNode);  
    HRESULT GetDataNodes(__out IDataNodes **ppNodes);  
    HRESULT GetChildDataNodes(LPCTSTR childeName, __out IDataNodes **ppNodes);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface fournit l’accès aux données de la page. Pour accéder au niveau supérieur des données de la page, utilisez la méthode **Settings()** de celle-ci.  

##### <a name="hresult-getattributelpctstr-attributename--lpbstr-attributevalue"></a>HRESULT GetAttribute(LPCTSTR attributeName, LPBSTR attributeValue)  
 Cette méthode vous permet de récupérer les valeurs des attributs sur le nœud principal, qui est le nœud **Page** quand vous utilisez la méthode **Settings()** de la page.  

##### <a name="istringproperties--properties"></a>IStringProperties * Properties()  
 Cette méthode permet d’accéder aux valeurs de propriété setter sous le nœud principal. Dans le cas d’une page, voici les propriétés de niveau supérieur.  

##### <a name="hresult-selectnodeslpctstr-xpath--ixmldomnodelist-pplist"></a>HRESULT SelectNodes(LPCTSTR xPath, IXMLDOMNodeList **ppList)  
 Appelez cette méthode si vous souhaitez obtenir directement une liste de nœuds XML à l’aide d’une expression XPath. Il est préférable d’utiliser l’une des autres méthodes si vous le pouvez. Utilisez cette méthode uniquement si vous ne pouvez pas accéder aux nœuds d’une autre façon.  

##### <a name="hresult-selectsinglenodelpctstr-xpath--ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xPath, IXMLDOMNode **ppNode)  
 Appelez cette méthode si vous souhaitez obtenir directement un nœud XML unique à l’aide d’une expression XPath. Il est préférable d’utiliser l’une des autres méthodes si vous le pouvez. Utilisez cette méthode uniquement si vous ne pouvez pas accéder à un nœud d’une autre façon.  

##### <a name="hresult-getdatanodelpctstr-name--isettingsproperties-ppnode"></a>HRESULT GetDataNode(LPCTSTR name, ISettingsProperties **ppNode)  
 Récupérer un élément **Data** en fonction de l’attribut **Name** de cet élément.  

##### <a name="hresult-getdatanodesidatanodes-ppnodes"></a>HRESULT GetDataNodes(IDataNodes **ppNodes)  
 Cette méthode récupère une liste d’éléments **DataItem** sous le nœud actuel. À partir du niveau de la page, appelez **GetDataNode** pour récupérer une interface **ISettingsProperty** pour les données. Ensuite, sur cette instance, appelez **GetDataNodes** pour récupérer la liste des enregistrements. Voici un code XML illustrant cette méthode :  

```  
    <Page …>  
      <Data Name="Network">  
        <DataItem>  
          <Setter Property="DisplayName">Public</Setter>  
          <Setter Property="Share">\\servername\Share</Setter>  
        </DataItem>  
        <DataItem>  
          <Setter Property="DisplayName">Dev Team</Setter>  
          <Setter Property="Share">\\servername\DevShare</Setter>  
        </DataItem>  
      </Data>  

PSettingsProperties pData;  
Settings()->GetDataNode(L"Network", &pData);  
PDataNodes pNodes;  
pData->GetDataNodes(&pNodes);  
```  

##### <a name="hresult-getchilddatanodeslpctstr-childename--idatanodes-ppnodes"></a>HRESULT GetChildDataNodes(LPCTSTR childeName, IDataNodes **ppNodes)  
 Cette méthode fournit un moyen rapide d’accéder à l’ensemble des nœuds **DataItem** sous un nœud **Data** spécifique. À partir du code XML de l’exemple **GetDataNodes**, le code suivant effectue la même chose que les quatre lignes de code dans l’exemple sous **GetDataNodes**, mais avec une vérification des erreurs :  

```  
ISimpleStringProperties Interface  
```  

#### <a name="isimplestringproperties-interface"></a>ISimpleStringProperties Interface  

```  
__interface ISimpleStringProperties : IStringProperties  
{  
void Add(LPCTSTR propertyName, LPCTSTR value);  
};  
```  

 En soi, cette interface peut s’avérer superflue. Toutefois, elle est implémentée par le composant **ID_SimpleStringProperties**, qui implémente également l’interface **IStringProperties**. Vous pouvez utiliser ce composant si vous devez passer un jeu de propriétés à un autre composant, tel qu’une tâche, mais que vous souhaitez ajouter des valeurs par programmation au lieu d’utiliser des valeurs issues d’un XML. Voici un exemple d’utilisation de cette interface :  

```  
PSimpleStringProperties *pProperties;  
CreateInstance(Container(), ID_SimpleStringProperties, &pProperties);  
pProperties->Add(L"filename", L"%windir%\\system32\\cscript.exe");  
pTask->Init(pProperties, nullptr);  
IStringProperties  
__interface IStringProperties : IUnknown  
{  
    HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue);  
};  
```  

 Cette interface fournit un accès simple à un ensemble d’éléments setter provenant d’un XML. Cette interface est disponible pour les propriétés d’une page à l’aide de **Settings()->Properties()**.  

##### <a name="hresult-getlpctstr-propertyname-out-lpbstr-ppropvalue"></a>HRESULT Get(LPCTSTR propertyName, [out] LPBSTR pPropValue)  
 Cette méthode récupère une valeur de propriété unique. Consultez les tableaux 47 et 48.  

### <a name="table-47-ihresult-get-property-value"></a>Tableau 47. IHRESULT Get : obtenir la valeur de propriété  

|**Paramètre**|**Description**|  
|-|-|  
|**propertyName**|Nom de la propriété à lire|  
|**pPropValue**|À la sortie, contient la valeur de propriété sous forme de chaîne (Cette valeur est **nullptr** s’il n’existe pas de propriété.)|  

### <a name="table-48-ihresult-get-property-value-results"></a>Tableau 48. IHRESULT Get : résultats de la récupération de la valeur de propriété  

|||  
|-|-|  
|**HRESULT**|**Description**|  
|**S_OK**|La valeur de propriété est récupérée.|  
|**E_INVALIDARG**|Aucune propriété ne porte le nom indiqué.|  

#### <a name="itaskmanager-interface"></a>Interface ITaskManager  

```  
__interface ITaskManager : IUnknown  
{  
    HRESULT Init(IWizardPageView *pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties *pPageInfo, ITaskManagerCallback *pCallback);  
    HRESULT SetFailMessage(LPCWSTR message);  

    HRESULT Start(void);  

    HRESULT GetTaskMessage(size_t index, LPBSTR message);  
    HRESULT GetResultType)(size_t index, LPBSTR type);  
    HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value);  
    int GetSelectedIndex(void);  
    HRESULT Wait(DWORD waitMilliseconds);  
    size_t FailedCount(void);  
    size_t WarningCount(void);  
    size_t SucceedCount(void);  
    size_t RunningCount(void);  

    void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo);  
    void OnControlEvent(WORD eventId, WORD controlId);  
    void EnableButtons(BOOL enable);  
}  
```  

 Cette interface est implémentée par le composant **TaskManager** (**ID_TaskManager** dans ITaskManager.h), composant qui exécute des tâches sur la page de précontrôle. Vous pouvez utiliser la page de précontrôle directement, comme à l’accoutumée, ou créer votre propre page, laissant à ce composant le soin d’effectuer la majeure partie du travail.  

##### <a name="hresult-initiwizardpageview-ppageview-int-idlistview-int-idmessage-int-idretrybutton-isettingsproperties-ppageinfo-itaskmanagercallback-pcallback"></a>HRESULT Init(IWizardPageView \*pPageView, int idListView, int idMessage, int idRetryButton, ISettingsProperties \*pPageInfo, ITaskManagerCallback \*pCallback)  
 Vous devez appeler cette méthode avant d’appeler toute autre méthode. Elle initialise le composant **TaskManager**. Consultez le tableau 49.  

### <a name="table-49-hresult-init"></a>Tableau 49. HRESULT Init  

|**Paramètre**|**Description**|  
|-|-|  
|**pPageView**|Fournit l’accès à la page destinée à exécuter les tâches (Cette page doit avoir un ensemble spécifique de contrôles, décrits dans les paramètres suivants.)|  
|**idListView**|ID de contrôle d’un contrôle **ListView** qui affiche la liste des tâches et leur état|  
|**idMessage**|ID de contrôle d’une zone de texte qui sert à afficher un message pour la tâche que vous sélectionnez.|  
|**idRetryButton**|ID de contrôle d’un bouton sur lequel vous pouvez cliquer pour réexécuter des tâches|  
|**pPageInfo**|Un wrapper autour du XML de la page (**TaskManager** charge l’ensemble des tâches à exécuter à partir de ce XML.)|  
|**pCallback**|Peut être Null (si ce paramètre n’est pas Null, **TaskManager** appelle la méthode **Started** quand il démarre une tâche et la méthode **Finished** pour chaque tâche dont l’exécution prend fin.)|  

##### <a name="hresult-setfailmessagelpcwstr-message"></a>HRESULT SetFailMessage(LPCWSTR message)  
 Cette méthode définit le message qui s’affiche si une ou plusieurs tâches échouent.  

##### <a name="hresult-startvoid"></a>HRESULT Start(void)  
 Cette méthode démarre toutes les tâches. Chaque tâche est démarrée sur un thread distinct.  

##### <a name="hresult-gettaskmessagesizet-index-lpbstr-message"></a>HRESULT GetTaskMessage(size_t index, LPBSTR message)  
 Cette méthode est à usage interne uniquement. Elle récupère le message actuel d’une tâche en fonction de son index dans la liste des tâches.  

##### <a name="hresult-getresulttypesizet-index-lpbstr-type"></a>HRESULT GetResultType)(size_t index, LPBSTR type)  
 Cette méthode récupère le « type » actuel d’une tâche. Le tableau 50 indique les types disponibles.  

### <a name="table-50-hresult-getresulttype"></a>Tableau 50. HRESULT GetResultType  

|**Type**|**Description**|  
|-|-|  
|**0**|Représente une tâche qui a réussi|  
|**1**|Représente une tâche qui a retourné un avertissement|  
|**-1**|Représente une tâche ayant échoué|  

 Le type est récupéré à partir du code de sortie ou d’erreur de la tâche et d’une correspondance avec ce code dans l’élément XML <ExitCodes\> de la tâche.  

##### <a name="hresult-getpropertysizet-index-lpctstr-propertyname-lpbstr-value"></a>HRESULT GetProperty(size_t index, LPCTSTR propertyName, LPBSTR value)  
 Cette méthode est utilisée par les pages de progression et de précontrôle pour récupérer la propriété setter **BitmapFilename** afin d’afficher une image en regard du message de la tâche que vous sélectionnez. En d’autres termes, vous pouvez ajouter une méthode setter personnalisée au XML la tâche, puis le récupérer avec cette méthode.  

##### <a name="int-getselectedindexvoid"></a>int GetSelectedIndex(void)  
 Cette méthode récupère l’index de la tâche actuellement sélectionnée, ce qui est utile si vous souhaitez récupérer des informations supplémentaires sur la tâche (voir la méthode **GetProperty**) en vue de les afficher. Les pages de progression et de précontrôle utilisent cette méthode afin d’afficher une image pour la tâche sélectionnée.  

##### <a name="hresult-waitdword-waitmilliseconds"></a>HRESULT Wait(DWORD waitMilliseconds)  
 Cette méthode, principalement utile dans le cadre d’un test unitaire, permet de s’assurer que les tâches se terminent avant le test. Normalement, vous n’appelez pas cette méthode. Elle prend fin quand toutes les tâches ont terminé de s’exécuter ou que le délai d’attente s’est écoulé.  

##### <a name="sizet-failedcountvoid"></a>size_t FailedCount(void)  
 Cette méthode retourne le nombre de tâches actuellement marquées comme ayant échoué.  

##### <a name="sizet-warningcountvoid"></a>size_t WarningCount(void)  
 Cette méthode retourne le nombre de tâches actuellement marquées en tant qu’avertissement.  

##### <a name="sizet-succeedcountvoid"></a>size_t SucceedCount(void)  
 Cette méthode retourne le nombre de tâches actuellement marquées comme ayant réussi.  

##### <a name="sizet-runningcountvoid"></a>size_t RunningCount(void)  
 Cette méthode retourne le nombre de tâches en cours d’exécution.  

##### <a name="void-oncommoncontroleventword-controlid-lpnmhdr-pinfo"></a>void OnCommonControlEvent(WORD controlId, LPNMHDR pInfo)  
 Appelez cette méthode à partir du **OnCommonControlEvent** de votre page afin que **TaskManager** puisse traiter les événements dont il a besoin.  

##### <a name="void-oncontroleventword-eventid-word-controlid"></a>void OnControlEvent(WORD eventId, WORD controlId)  
 Appelez cette méthode à partir du **OnControlEvent** de votre page afin que **TaskManager** puisse traiter les événements dont il a besoin.  

##### <a name="void-enablebuttonsbool-enable"></a>void EnableButtons(BOOL enable)  
 Cette méthode est à usage interne uniquement.  

#### <a name="iwizardcomponent-interface"></a>Interface IWizardComponent  

```  
__interface IWizardComponent : IUnknown  
{  
    HRESULT SetContainer(IWizardPageContainer *pContainer);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 En règle générale, vous n’implémentez pas cette interface directement, mais plutôt par le biais de la classe de modèle **WizardComponent**. Si votre composant implémente cette interface et que vous avez inscrit une fabrique de classe auprès du registre, votre composant reçoit un pointeur vers l’instance **IWizardPageContainer** au moment de sa création. Cela vous permet, par exemple, d’accéder au journaliseur ou au registre pour créer d’autres composants dont votre composant est susceptible d’avoir besoin.  

#### <a name="iwizarddialogcontroller-interface"></a>Interface IWizardDialogController  

```  
__interface IWizardDialogController : IUnknown  
{  
    void Initialize(ISettings *pSettings);  
    void InitPages(void);  
    void Start();  
    void Next();  
    void Finish();  
    void Previous();  
    int NumPages();  
    void Cancel();  

    HRESULT Focus(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage();  

    void ChangePage(size_t newIndex);  
    IUnknown *CurrentPage(void);  
    HRESULT GetCurrentTitle([out, retval] LPBSTR pDisplayName);  
};  
```  

 Cette interface est à usage interne uniquement.  

#### <a name="iwizarddialogview-interface"></a>Interface IWizardDialogView  

```  
__interface IWizardDialogView : IUnknown  
{  
    HRESULT LoadBannerImage(LPCTSTR bannerFilename);  
    HRESULT LoadPage(LPCTSTR pageType, ISettingsProperties *pPageSettings, IWizardPageView **view);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    HRESULT Focus(WizardButtons button);  
    void EnableFinish(BOOL isFinish);  
    void Exit(int exitCode);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
    void SetTitle(LPCTSTR title);  
    void SetPageTitle(LPCTSTR title);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    HWND GetHwnd(void);  
    void UpdateFocus(void);  
};  
```  

 Cette interface est à usage interne uniquement.  

####  <a name="IWizardPageInterface"></a> Interface IWizardPage  

```  
__interface IWizardPage : IUnknown  
{  
    HRESULT SetPageSettings(ISettingsProperties *pPageSettings);  
    HINSTANCE GetInstanceHandle(void);  
    int GetDialogResourceId(void);  
    void WindowCreated(IWizardPageView *pView, IWizardPageContainer *pContainer);  
    void WindowShown(void);  
    void WindowHidden(void);  

    HRESULT NextClicked(void);  
    void ControlEvent(WORD eventId, WORD controlId);  
    void CommonControlEvent(WORD controlId, LPNMHDR pInfo, LPBOOL pCancel);  
    void UnhandledEvent(HWND hwnd, UINT message, WPARAM wParam, LPARAM lParam);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface étant implémentée par **WizardPageImpl**, vous ne devez généralement pas le faire vous-même. L’Assistant appelle toutes ces méthodes pour vous quand il interagit avec vos pages personnalisées.  

#### <a name="iwizardpagecontainer-interface"></a>Interface IWizardPageContainer  

```  
__interface IWizardPageContainer : IUnknown  
{  
    ILogger * Logger(void);  
    IPropertyBag * Properties(void);  
    HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance);  
    HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance);  
    HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest);  
    HRESULT GotoPage(LPCTSTR pageName);  
    int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType);  
    BOOL InPreview(void);  
    HWND GetHwnd(void);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est disponible pour votre page par le biais de la méthode **Container** (implémentée par **WizardPageImpl**) et vous donne accès à divers services de l’Assistant.  

##### <a name="ilogger--loggervoid"></a>ILogger * Logger(void)  
 Utilisez cette méthode pour écrire des messages dans le fichier journal, par exemple :  

```  
Logger()->Verbose(s_component, L"Message for log file");  
```  

##### <a name="ipropertybag--propertiesvoid"></a>IPropertyBag * Properties(void)  
 Cette méthode permet d’accéder à des variables « mémoire », propriétés qui ne sont stockées en mémoire que pendant l’exécution de l’Assistant UDI. Ces propriétés sont disponibles pour d’autres pages dans le code ou dans le XML à l’aide de la syntaxe **$memoryVarName$**.  

##### <a name="hresult-createinstancelpctstr-type-out-iunknown-ppinstance"></a>HRESULT CreateInstance(LPCTSTR type, [out] IUnknown **ppInstance)  
 Cette méthode vous permet de créer une instance de tout composant qui a été inscrit. Toutefois, il est préférable d’utiliser la fonction de modèle **CreateInstance**, car elle est fortement typée.  

##### <a name="hresult-getservicerefiid-iid-out-iunknown-ppinstance"></a>HRESULT GetService(REFIID iid, [out] IUnknown **ppInstance)  
 Cette méthode permet de récupérer un service qui a été inscrit. Toutefois, il est préférable d’appeler la fonction de modèle **GetService**, qui est fortement typée (au lieu d’utiliser **IUnknown**).  

##### <a name="hresult-replacevariableslpctstr-source-out-lpbstr-pdest"></a>HRESULT ReplaceVariables(LPCTSTR source, [out] LPBSTR pDest)  
 Cette méthode gère l’utilisation des variables à l’intérieur des valeurs de chaîne. Elle prend en charge les formats indiqués dans les tableaux 51 et 52.  

### <a name="table-51-hresult-replacevariables"></a>Tableau 51. HRESULT ReplaceVariables  

|**Format**|**Description**|  
|-|-|  
|**$Name$**|Remplace la valeur d’une variable de mémoire par ce nom (si aucune variable de mémoire ne porte ce nom, le « jeton » est supprimé.)|  
|**%Name%**|Variable de séquence de tâches ou variable d’environnement. L’ordre est le suivant :<br /><br /> 1.  Utiliser la valeur d’une variable de séquence de tâches, si elle existe.<br />2.  Utiliser la valeur d’une variable de séquence d’environnement, si elle existe.<br />3.  Sinon, supprimer ce texte de la chaîne.|  

### <a name="table-52-hresult-parameter"></a>Tableau 52. Paramètre HRESULT  

|**Paramètre**|**Description**|  
|-|-|  
|**Source**|Chaîne d’entrée, qui peut contenir n’importe quelle combinaison de variables **$** et **%** ou aucune|  
|**pDest**|En retour, contient une nouvelle chaîne dont tous les jetons sont remplacés conformément au tableau 51|  

##### <a name="hresult-gotopagelpctstr-pagename"></a>HRESULT GotoPage(LPCTSTR pageName)  
 Cette méthode n’a pas été entièrement testée. L’idée est que vous puissiez passer directement à une page spécifique en fonction du nom de la page tel que défini dans le fichier .config. Appeler cette méthode ignore **OnNextClicked** sur votre page. En outre, le comportement de cette méthode étant susceptible de changer, vous l’utilisez à vos propres risques.  

##### <a name="int-showmessageboxlpctstr-message-lpctstr-lpcaption-uint-utype"></a>int ShowMessageBox(LPCTSTR message, LPCTSTR lpCaption, UINT uType)  
 Cette méthode affiche une boîte de message avec le texte et la légende que vous fournissez. Le paramètre **uType** est toute valeur que vous pouvez fournir à la fonction Win32 **MessageBox**.  

##### <a name="bool-inpreviewvoid"></a>BOOL InPreview(void)  
 Cette méthode retourne la valeur TRUE si vous avez lancé l’Assistant en mode « Aperçu » en fournissant le commutateur **/Preview**. En mode Aperçu, le bouton **Next** (Suivant) n’est jamais désactivé. Cette méthode permet d’ignorer, en mode Aperçu, du code qui, par exemple, pourrait entraîner des problèmes si la page comportait des données non valides.  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Cette méthode retourne le **HWND** pour la boîte de dialogue principale. Utilisez cette méthode avec précaution. En règle générale, l’interface de programmation d’applications de l’Assistant UDI est conçue afin que vous n’utilisiez jamais de handles de fenêtre directement.  

#### <a name="iwizardpageview-interface"></a>Interface IWizardPageView  

```  
__interface IWizardPageView : IUnknown  
{  
    HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown **ppControl);  
    HWND GetHwnd(void);  
    HWND GetControl(int itemId);  
    HRESULT Show (void);  
    HRESULT Hide(void);  
    HRESULT Focus(int itemId);  
    IWizardPage * Page(void);  
    IFormController * Form(void);  

    HRESULT FocusWizardButton(WizardButtons button);  
    HRESULT SetEnable(WizardButtons button, BOOL enable);  
    void ShowWarningMessage(LPCTSTR message);  
    void HideWarningMessage(void);  
};  
```  

 Cette interface est disponible pour le code de votre page par le biais de la méthode **View** (implémentée par **WizardPageImpl**).  

##### <a name="hresult-getcontrolwrapperint-itemid-dialogcontroltypes-controltype-iunknown-ppcontrol"></a>HRESULT GetControlWrapper(int itemId, DialogControlTypes controlType, IUnknown \*ppControl)  
 UDI Wizard (Assistant UDI) utilise des *wrappers*, qui sont en réalité des façades permettant d’interagir avec les contrôles de votre page. L’utilisation de ces façades à la place des contrôles réels facilite grandement l’écriture de tests pour votre page, car vous pouvez fournir des façades fictives à partir de vos tests.  

 Au lieu d’utiliser directement cette méthode, il est préférable d’utiliser la méthode modèle **GetControlWrapper**, qui est fortement typée, par exemple :  

```  
PComboBox m_pLanguagePackCombo;  
GetControlWrapper(View(), IDC_MY_COMBO, CONTROL_COMBO_BOX, &m_pCombo);  
```  

##### <a name="hwnd-gethwndvoid"></a>HWND GetHwnd(void)  
 Cette méthode retourne le handle de fenêtre de votre page. En règle générale, vous n’avez pas besoin d’accéder à ce handle de fenêtre.  

##### <a name="hwnd-getcontrolint-itemid"></a>HWND GetControl(int itemId)  
 Si nécessaire, vous pouvez appeler cette méthode pour obtenir le handle de fenêtre d’un contrôle sur votre page. (Il est préférable d’appeler la fonction de modèle **GetControlWrapper**).  

##### <a name="hresult-show-void"></a>HRESULT Show (void)  
 Cette méthode est à usage interne uniquement.  

##### <a name="hresult-hidevoid"></a>HRESULT Hide(void)  
 Cette méthode est à usage interne uniquement.  

##### <a name="hresult-focusint-itemid"></a>HRESULT Focus(int itemId)  
 Affecte au focus d’entrée un contrôle spécifique.  

##### <a name="iwizardpage--pagevoid"></a>IWizardPage * Page(void)  
 Cette méthode est à usage interne uniquement.  

##### <a name="iformcontroller--formvoid"></a>IFormController * Form(void)  
 Cette méthode est à usage interne uniquement.  

##### <a name="hresult-focuswizardbuttonwizardbuttons-button"></a>HRESULT FocusWizardButton(WizardButtons button)  
 Affecte au focus l’un des boutons de l’Assistant.**WizardButtons** a deux valeurs : **BackButton** et **NextButton**.  

##### <a name="hresult-setenablewizardbuttons-button-bool-enable"></a>HRESULT SetEnable(WizardButtons button, BOOL enable)  
 Demande que l’un des boutons de l’Assistant soit activé ou désactivé. Le bouton ne correspond pas forcément à l’état que vous demandez. Par exemple, si vous exécutez UDI Wizard (Assistant UDI) avec le commutateur **/preview**, les boutons sont toujours activés. **WizardButtons** a deux valeurs : **BackButton** et **NextButton**.  

##### <a name="void-showwarningmessagelpctstr-message"></a>void ShowWarningMessage(LPCTSTR message)  
 Cette méthode affiche un message d’avertissement au bas de la zone de contenu de la page. Ce message peut correspondre au texte de votre choix.  

##### <a name="void-hidewarningmessagevoid"></a>void HideWarningMessage(void)  
 Masque un message d’avertissement que vous avez affiché via un appel à **ShowWarningMessage**.  

#### <a name="ixmldocument-interface"></a>Interface IXmlDocument  

```  
__interface IXmlDocument : IUnknown  
    HRESULT Load(LPCTSTR filename);  
    HRESULT LoadXml(LPCTSTR xml);  
    HRESULT Save(LPCWSTR filename);  
    HRESULT GetParseErrorMessage(LPBSTR pMessage);  
    HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList **ppNodes);  
    HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode **ppNode);  
    HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns);  
    HRESULT AddAttribute(IXMLDOMNode *pNode, LPCWSTR name, LPCWSTR value);  
    HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode **ppNode);  
};  
```  

##### <a name="overview"></a>Vue d'ensemble  
 Cette interface est implémentée par le composant **ID_IXmlDocument**, qui est une façade conçue pour faciliter l’utilisation de documents XML en C++.  

##### <a name="hresult-loadlpctstr-filename"></a>HRESULT Load(LPCTSTR filename)  
 Cette méthode charge un document XML à partir d’un fichier externe. Elle retourne **S_OK** si le fichier a été chargé sans erreurs, ou **S_FALSE** si une erreur s’est produite. Quand une erreur se produit, vous pouvez obtenir le message d’erreur en appelant **GetParseErrorMessage**.  

##### <a name="hresult-loadxmllpctstr-xml"></a>HRESULT LoadXml(LPCTSTR xml)  
 Cette méthode charge un document XML à partir d’une chaîne au lieu d’un fichier externe. À part la source de lecture du contenu XML, le comportement est le même que celui de la méthode **Load**.  

##### <a name="hresult-savelpcwstr-filename"></a>HRESULT Save(LPCWSTR filename)  
 Cette méthode enregistre le document XML en mémoire dans un fichier externe.  

##### <a name="hresult-getparseerrormessagelpbstr-pmessage"></a>HRESULT GetParseErrorMessage(LPBSTR pMessage)  
 Cette méthode retourne une nouvelle chaîne avec le message d’erreur de chargement du document XML, le cas échéant. Elle retourne toujours **S_OK**.  

##### <a name="hresult-selectnodeslpctstr-xpath-ixmldomnodelist-ppnodes"></a>HRESULT SelectNodes(LPCTSTR xpath, IXMLDOMNodeList \**ppNodes)  
 Cette méthode vous permet d’utiliser une expression XPath pour récupérer une collection de nœuds à partir du document. Elle retourne toujours **S_OK**.  

##### <a name="hresult-selectsinglenodelpctstr-xpath-ixmldomnode-ppnode"></a>HRESULT SelectSingleNode(LPCTSTR xpath, IXMLDOMNode \**ppNode)  
 Cette méthode vous permet d’utiliser une expression XPath pour récupérer un nœud à partir du document. Elle retourne toujours **S_OK**.  

##### <a name="hresult-addschemalpctstr-filename-lpctstr-ns"></a>HRESULT AddSchema(LPCTSTR filename, LPCTSTR ns)  
 Cette méthode ajoute le nom d’un fichier de schéma externe qui permet de valider le schéma de votre document XML au moment de son chargement. L’espace de noms que vous indiquez correspond à la chaîne que vous pouvez utiliser dans les requêtes XPath, bien que cela n’ait pas été testé.  

##### <a name="hresult-addattributeixmldomnode-pnode-lpcwstr-name-lpcwstr-value"></a>HRESULT AddAttribute(IXMLDOMNode \*pNode, LPCWSTR name, LPCWSTR value)  
 Cette méthode ajoute un nouvel attribut à un nœud existant dans le document XML. Consultez le tableau 53.  

### <a name="table-53-hresult-addattribute"></a>Tableau 53. HRESULT AddAttribute  

|**Paramètre**|**Description**|  
|-|-|  
|**pNode**|Nœud auquel vous souhaitez ajouter un attribut|  
|**Nom**|Nom du nouvel attribut|  
|**Valeur**|Valeur du nouvel attribut|  

##### <a name="hresult-createnodedomnodetype-type-lpcwstr-name-lpcwstr-ns-ixmldomnode-ppnode"></a>HRESULT CreateNode(DOMNodeType type, LPCWSTR name, LPCWSTR ns, IXMLDOMNode \**ppNode)  
 Appelez cette méthode pour créer un nœud :  

```  
Pointer<IXMLDOMNode> pNewChild  
pXmlDom->CreateNode(NODE_ELEMENT, L"MyElement", L"", &pNewChild);  
```  

 Une fois que vous avez créé un nœud, vous pouvez l’ajouter en tant qu’enfant à un autre nœud en appelant la méthode **appendChild** du parent.  

### <a name="helper-functions"></a>Fonctions d’assistance  

#### <a name="createinstance-template-function"></a>Fonction de modèle CreateInstance  

```  
HRESULT CreateInstance(IWizardPageContainer *pContainer, LPCTSTR type, I **ppObject)  
```  

 Cette fonction est définie dans IWizardPageContainer.h et fournit un wrapper de type sécurisé sur la méthode **IWizardPageContainer->CreateInstance**. Exemple :  

```  
CreateInstance<IDirectory>(Container(), ID_Directory, &pDirectory);  
```  

 Ce code crée un composant **ID_Directory** pour récupérer l’interface **IDirectory** de ce composant.  

#### <a name="getservice-template-function"></a>Fonction de modèle GetService  

```  
void GetService(IWizardPageContainer *pContainer, I **ppService)  
```  

 Cette fonction est définie dans IWizardPageContainer.h et fournit un wrapper de type sécurisé sur la méthode **IWizardPageContainer->GetService**. Exemple :  

```  
GetService<ITSVariableBag>(Container(), &pTsBag);  
```  

 Cette fonction récupère le composant de séquence de tâches, qui prend en charge l’interface **ITSVariableBag**. (Pour **ITSVariableBag**, vous pouvez utiliser la méthode TSVariables de la classe **WizardPageImpl** à la place.)  

### <a name="udi-wizard-designer-configuration-file-schema-reference"></a>Référence du schéma du fichier de configuration d’UDI Wizard Designer (Concepteur de l’Assistant UDI)  
 Ce fichier est consommé par UDI Wizard Designer (Concepteur de l’Assistant UDI). Un fichier distinct est créé pour chaque fichier .dll personnalisé. Il peut contenir des éditeurs de pages d’Assistant personnalisés, des tâches personnalisées ou des validateurs personnalisés. Le fichier doit finir par *.config* et se trouver dans le dossier *dossier_installation*\Bin\Config (où *dossier_installation* correspond au dossier où vous avez installé MDT).  

  Le tableau 54 liste les éléments du fichier de configuration d’UDI Wizard Designer (Concepteur de l’Assistant UDI) et leurs descriptions. L’élément **DesignerConfig** est le nœud racine de cette référence.  

### <a name="table-54-elements-in-the-udi-wizard-designer-configuration-file-and-their-descriptions"></a>Tableau 54. Éléments du fichier de configuration d’UDI Wizard Designer (Concepteur de l’Assistant UDI) et leurs descriptions  

|**Nom de l’élément**|**Description**|  
|-|-|  
|[DesignerConfig](#DesignerConfig)|Spécifie la racine de tous les autres éléments|  
|[DesignerMappings](#DesignerMappings)|Regroupe un ensemble d’éléments [Page](#Page)|  
|[Page](#Page)|Spécifie un éditeur de page d’Assistant à charger dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Il permet de modifier les paramètres de configuration d’une page d’Assistant|  
|[Param](#Param)|Spécifie un paramètre passé à l’élément [Task](#Task) ou [Validator](#Validator) parent, qui correspond à un élément [Setter]() dans le fichier de configuration d’UDI Wizard (Assistant UDI). **Remarque :** Les attributs de cet élément sont différents si le parent correspond à l’élément [Task](#Task) ou [Validator](#Validator).|  
|[Task](#Task)|Spécifie une tâche dans la bibliothèque de tâches|  
|[TaskItem](#TaskItem)|Spécifie un groupe de paramètres passés à la tâche|  
|[TaskLibrary](#TaskLibrary)|Regroupe un ensemble d’éléments [Task](#Task)|  
|[Validator](#Validator)|Spécifie un validateur dans la bibliothèque de validateurs|  
|[ValidatorLibrary](#ValidatorLibrary)|Regroupe un ensemble d’éléments [Validator](#Validator)|  

####  <a name="DesignerConfig"></a> DesignerConfig  
 Cet élément spécifie la racine de tous les autres éléments.  

##### <a name="element-information"></a>Informations sur l'élément  
  Le tableau 55 fournit des informations sur l’élément [DesignerConfig](#DesignerConfig).  

### <a name="table-55-designerconfig-element-information"></a>Tableau 55. Informations sur l’élément DesignerConfig  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une : cet élément est obligatoire.|  
|Éléments parents|Aucun|  
|Contenu|**DesignerMappings**, **TaskLibrary**, **ValidatorLibrary**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="DesignerMappings"></a> DesignerMappings  
 Cet élément regroupe un ensemble d’éléments [Page](#Page).  

##### <a name="element-information"></a>Informations sur l'élément  
  Le tableau 56 fournit des informations sur l’élément [DesignerMappings](#DesignerMappings).  

### <a name="table-56-designermappings-element-information"></a>Tableau 56. Informations sur l’élément DesignerMappings  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou une dans l’élément [DesignerConfig](#DesignerConfig). Cet élément est facultatif, s’il n’existe aucune page d’Assistant personnalisée dans la DLL correspondant à ce fichier de configuration d’UDI Wizard Designer (Concepteur de l’Assistant UDI).|  
|Éléments parents|**DesignerConfig**|  
|Contenu|**Page**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<DesignerConfig>  
   + <TaskLibrary>  
   + <ValidatorLibrary>  
   - <DesignerMappings>  
        <Page DLL="SharedPages.dll"  
           Description="Used to display text that describes the current stagegroup"  
           Type="Microsoft.SharedPages.WelcomePage"  
           DisplayName="Welcome"   
           Image="Welcome_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.WelcomePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Captures or restores user state data"  
           Type="Microsoft.OSDRefresh.UserStatePage"  
           DisplayName="User Data"  
           Image="UserState_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.UserStatePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
        <Page DLL="OSDRefreshWizard.dll"  
           Description="Allows selecting the image to install, target drive, and whether to format"  
           Type="Microsoft.OSDRefresh.VolumePage"  
           DisplayName="Volume"  
           Image="Volume_188.png"  
           DesignerType="Microsoft.Enterprise.UDIDesigner.CoreModules.Views.VolumePageView"  
           DesignerAssembly="Microsoft.Enterprise.UDIDesigner.CoreModules.dll"/>  
     </DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Page"></a> Page  
 Cet élément spécifie un éditeur de page d’Assistant à charger dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Cet éditeur permet en retour de modifier les paramètres de configuration d’une page d’Assistant.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 57 fournit des informations sur l’élément [Page](#Page).  

### <a name="table-57-page-element-information"></a>Tableau 57. Informations sur l’élément Page  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs pour chaque page d’Assistant définie dans l’élément [DesignerMappings](#DesignerMappings)|  
|Éléments parents|**DesignerMappings**|  
|Contenu|Contenu XML bien formé|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 58 liste les attributs de l’élément [Page](#Page) avec une description de chacun d’eux.  

### <a name="table-58-attributes-and-corresponding-values-for-the-page-element"></a>Tableau 58. Attributs et valeurs correspondantes de l’élément Page  

|**Attribut**|**Description**|  
|-|-|  
|**Description**|Spécifie le texte d’informations décrivant le paramètre, qui s’affiche dans UDI Wizard Designer (Concepteur de l’Assistant UDI)|  
|**DesignerAssembly**|Spécifie le nom du fichier .dll associé à l’éditeur de page d’Assistant (le fichier .dll doit exister dans le dossier *dossier_installation*\Bin (où *dossier_installation* correspond au dossier où vous avez installé MDT.)|  
|**DesignerType**|Spécifie le nom de l’éditeur de page d’Assistant dans le fichier .dll indiqué dans l’attribut **DesignerAssembly** (il s’agit du type Microsoft .NET de l’éditeur de page d’Assistant avec l’espace de noms Microsoft .NET complet).|  
|**DisplayName**|Spécifie le nom convivial de l’éditeur de page, qui s’affiche dans UDI Wizard Designer (Concepteur de l’Assistant UDI)|  
|**DLL**|Spécifie le nom du fichier .dll associé à la page de l’Assistant (le fichier .dll doit exister dans le dossier *dossier_installation*\Templates\Distribution\Tools\\*plateforme* (où *dossier_installation* correspond au dossier où vous avez installé MDT et *plateforme* correspond à **x86** pour la version 32 bits ou **x64** pour la version 64 bits.) **Remarque :** Vérifiez que l’architecture du processeur DLL correspond à l’architecture du processeur MDT installée. Par exemple, si vous avez installé une version 32 bits de MDT, veillez à utiliser une DLL 32 bits pour la page de l’Assistant.|  
|**Image**|Spécifie le nom d’une image de la page au format PNG (le fichier .png doit exister dans le dossier *dossier_installation*\Bin\Images (où *dossier_installation* correspond au dossier où vous avez installé MDT.)|  
|**Type**|Spécifie l’éditeur de page d’Assistant et doit correspondre au nom utilisé quand la page personnalisée a été inscrite|  

##### <a name="remarks"></a>Remarques  
 UDI Wizard Designer (Concepteur de l’Assistant UDI) utilise l’élément [Page](#Page) comme modèle pour créer le contenu XML initial d’un nouvel Assistant. UDI Wizard Designer (Concepteur de l’Assistant UDI) effectue une validation de schéma pour vérifier que les éléments [Page](#Page) et les éléments enfants ont un format valide. Cet élément fournit un mappage entre le type de page d’UDI Wizard (Assistant UDI) et les informations dont UDI Wizard Designer (Concepteur de l’Assistant UDI) a besoin pour modifier et créer des pages de ce type à l’aide d’un éditeur de page personnalisé.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Param"></a> Param  
 Cet élément spécifie un paramètre passé à l’élément [Task](#Task) ou [Validator](#Validator) parent, et correspond à un élément [Setter]() dans le fichier de configuration d’UDI Wizard (Assistant UDI).  

> [!NOTE]
>  Les attributs de cet élément sont différents si le parent est l’élément [Task](#Task) ou [Validator](#Validator).  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 59 fournit des informations sur l’élément [Param](#Param).  

### <a name="table-59-param-element-information"></a>Tableau 59. Informations sur l’élément Param  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs pour chaque élément [TaskItem](#TaskItem) ou [Validator](#Validator) parent|  
|Éléments parents|**TaskItem**, **Validator**|  
|Contenu|Contenu XML bien formé|  

##### <a name="element-attributes"></a>Attributs d’élément  
  Le tableau 60 liste les attributs de l’élément [Param](#Param) et fournit une description de chacun d’eux.  

### <a name="table-60-attributes-and-corresponding-values-for-the-param-element"></a>Tableau 60. Attributs et valeurs correspondantes de l’élément Param  

|**Attribut**|**Description**|  
|-|-|  
|**Description**|Spécifie le texte d’informations décrivant le paramètre, qui s’affiche dans UDI Wizard Designer (Concepteur de l’Assistant UDI). **Remarque :** Cet attribut est valide uniquement pour l’élément [Validator](#Validator).|  
|**DisplayName**|Spécifie le nom convivial du paramètre validator, qui s’affiche pour la page d’UDI Wizard (Assistant UDI) appropriée dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce nom est généralement plus descriptif que l’attribut **Name**. **Remarque :** Cet attribut est valide uniquement pour l’élément [Validator](#Validator).|  
|**Nom**|Spécifie le nom du paramètre passé à la tâche ou au validateur, en fonction de l’élément parent (cet attribut devient l’attribut **Property** d’un élément [Setter]() dans le fichier de configuration d’UDI Wizard.) **Remarque :** Ce paramètre est utilisé pour les éléments parents [TaskItem](#TaskItem) et [Validator](#Validator).|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Task"></a> Task  
 Cet élément spécifie une tâche dans la bibliothèque de tâches.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 61 fournit des informations sur l’élément [Task](#Task).  

### <a name="table-61-task-element-information"></a>Tableau 61. Informations sur l’élément Task  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans l’élément [TaskLibrary](#TaskLibrary) (cet élément n’est pas facultatif si l’élément **TaskLibrary** est spécifié).|  
|Éléments parents|**TaskLibrary**|  
|Contenu|**TaskItem**|  

##### <a name="element-attributes"></a>Attributs d’élément  
  Le tableau 62 liste les attributs de l’élément [Task](#Task) et fournit une description de chacun d’eux.  

### <a name="table-62-attributes-and-corresponding-values-for-the-task-element"></a>Tableau 62. Attributs et valeurs correspondantes de l’élément Task  

|**Attribut**|**Description**|  
|-|-|  
|**Description**|Spécifie le texte d’informations décrivant la tâche, qui s’affiche dans UDI Wizard Designer (Concepteur de l’Assistant UDI)|  
|**DLL**|Spécifie le nom du fichier .dll associé à la tâche (le fichier .dll doit exister dans le dossier *dossier_installation*\Templates\Distribution\Tools\\*plateforme* (où *dossier_installation* correspond au dossier où vous avez installé MDT et *plateforme* correspond à **x86** pour la version 32 bits ou **x64** pour la version 64 bits.)|  
|**Nom**|Spécifie le nom de la tâche, qui s’affiche dans la page d’UDI Wizard (Assistant UDI) approprié et dans UDI Wizard Designer (Concepteur de l’Assistant UDI)|  
|**Type**|Spécifie le type de tâche, inscrit auprès du Registre de fabrique et utilisé pour appeler une tâche spécifique dans un fichier .dll|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="TaskItem"></a> TaskItem  
 Cet élément spécifie un groupe de paramètres passés à la tâche.  

##### <a name="element-information"></a>Informations sur l'élément  
  Le tableau 63 fournit des informations sur l’élément [TaskItem](#TaskItem).  

### <a name="table-63-taskitem-element-information"></a>Tableau 63. Informations sur l’élément TaskItem  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs pour chaque élément **Task**|  
|Éléments parents|**Task**|  
|Contenu|**Param**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 64 liste les attributs de l’élément [TaskItem](#TaskItem) et fournit une description de chacun d’eux.  

### <a name="table-64-attribute-and-corresponding-values-for-the-taskitem-element"></a>Tableau 64. Attribut et valeurs correspondantes de l’élément TaskItem  

|**Attribut**|**Description**|  
|-|-|  
|**Type**|Spécifie le type d’élément à créer dans le fichier de configuration d’UDI Wizard (Assistant UDI). Un élément XML correspondant à la valeur de cet attribut est créé. Par exemple, si la valeur de cet attribut est [File](#File), un élément **File** est créé dans le fichier de configuration d’UDI Wizard (Assistant UDI).<br /><br /> Les seules valeurs prises en charge sont :<br /><br /> -   **File**, qui nécessite deux éléments enfants [Param](#Param) (un élément enfant **Param** avec l’attribut **Name** ayant la valeur **Source** et un autre élément enfant **Param** avec l’attribut **Name** ayant la valeur **Dest**)<br />-   [Setter](), qui nécessite un élément enfant **Param**|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="TaskLibrary"></a> TaskLibrary  
 Cet élément regroupe un ensemble d’éléments [Task](#Task).  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 65 fournit des informations sur l’élément [TaskLibrary](#TaskLibrary).  

### <a name="table-65-tasklibrary-element-information"></a>Tableau 65. Informations sur l’élément TaskLibrary  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou une dans l’élément [DesignerConfig](#DesignerConfig). Cet élément est facultatif, s’il n’existe aucune tâche personnalisée dans la DLL correspondant à ce fichier de configuration d’UDI Wizard Designer (Concepteur de l’Assistant UDI).|  
|Éléments parents|**DesignerConfig**|  
|Contenu|**Task**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<DesignerConfig>  
   - <TaskLibrary>  
        +<Task DLL="" Description="Executes a process with the given command line." Type="Microsoft.Wizard.ShellExecuteTask" Name="Shell Execute Task">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Discovers supported applications for install." Type="Microsoft.OSDRefresh.AppDiscoveryTask" Name="Application Discovery">  
        +<Task DLL="SharedPages.dll" Description="Check to ensure a wired network connection is available." Type="Microsoft.SharedPages.WiredNetworkTask" Name="Wired Network Check">  
        +<Task DLL="OSDRefreshWizard.dll" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.OSDRefresh.ACPowerTask" Name="AC Power Check">  
        +<Task DLL="" Description="Check to ensure power source is AC (not battery)." Type="Microsoft.Wizard.CopyFilesTask" Name="Copy Files Task">  
     </TaskLibrary>  
   + <ValidatorLibrary>  
   + <DesignerMappings>  
</DesignerConfig>  
```  

####  <a name="Validator"></a> Validator  
 Cet élément spécifie un validateur dans la bibliothèque de validateurs.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 66 fournit des informations sur l’élément [Validator](#Validator).  

### <a name="table-66-validator-element-information"></a>Tableau 66. Informations sur l’élément Validator  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans l’élément [ValidatorLibrary](#ValidatorLibrary) (cet élément est facultatif.)|  
|Éléments parents|**ValidatorLibrary**|  
|Contenu|**Param**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 67 liste les attributs de l’élément [Validator](#Validator) et fournit une description de chacun d’eux.  

### <a name="table-67-attributes-and-corresponding-values-for-the-validator-element"></a>Tableau 67. Attributs et valeurs correspondantes de l’élément Validator  

|**Attribut**|**Description**|  
|-|-|  
|**Description**|Spécifie le texte d’informations décrivant le validateur, qui s’affiche dans UDI Wizard Designer (Concepteur de l’Assistant UDI)|  
|**DisplayName**|Spécifie le nom convivial du validateur affiché dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce nom est généralement plus descriptif que l’attribut **Name**.|  
|**DLL**|Spécifie le nom du fichier .dll associé au validateur (le fichier .dll doit exister dans le dossier *dossier_installation*\Templates\Distribution\Tools\\*plateforme* (où *dossier_installation* correspond au dossier où vous avez installé MDT et *plateforme* correspond à **x86** pour la version 32 bits ou **x64** pour la version 64 bits.)|  
|**Nom**|Spécifie le nom du validateur, qui s’affiche dans la page d’UDI Wizard (Assistant UDI) approprié et dans UDI Wizard Designer (Concepteur de l’Assistant UDI)|  
|**Type**|Spécifie le type de validateur, inscrit auprès du Registre de fabrique et utilisé pour appeler un validateur spécifique dans un fichier .dll|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="ValidatorLibrary"></a> ValidatorLibrary  
 Cet élément regroupe un ensemble d’éléments [Validator](#Validator).  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 68 fournit des informations sur l’élément [ValidatorLibrary](#ValidatorLibrary).  

### <a name="table-68-validatorlibrary-element-information"></a>Tableau 68. Informations sur l’élément ValidatorLibrary  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou une dans l’élément [DesignerConfig](#DesignerConfig). Cet élément est facultatif, s’il n’existe aucun validateur personnalisé dans la DLL correspondant à ce fichier de configuration d’UDI Wizard Designer (Concepteur de l’Assistant UDI).|  
|Éléments parents|**DesignerConfig**|  
|Contenu|**Validator**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 <DesignerConfig\>   + <TaskLibrary\>   - <ValidatorLibrary\>        +<Validator DLL="" Description="Impose la saisie de texte dans un champ" Type="Microsoft.Wizard.Validation.NonEmpty" Name="NonEmpty"\>        +<Validator DLL="" Description="Interdit certains caractères dans un champ" Type="Microsoft.Wizard.Validation.InvalidChars" Name="InvalidChars"\>        +<Validator DLL="" Description="Impose le respect d’un modèle prédéfini" Type="Microsoft.Wizard.Validation.RegEx" Name="NamedPattern"\>        +<Validator DLL="" Description="Impose une correspondance entre le contenu et une expression régulière" Type="Microsoft.Wizard.Validation.RegEx" Name="RegEx"\>     </ValidatorLibrary\>   + <DesignerMappings\></DesignerConfig\>  

## <a name="udi-wizard-designer-reference"></a>Référence d’UDI Wizard Designer (Concepteur de l’Assistant UDI)  

### <a name="controls"></a>Contrôles  
 Les contrôles qui permettent de créer des éditeurs de pages d’Assistant personnalisés utilisables dans UDI Wizard Designer (Concepteur de l’Assistant UDI) sont des instances WPF de **UserControl**. Le tableau 69 liste les contrôles qui permettent de créer des éditeurs de pages d’Assistant personnalisés.  

### <a name="table-69-controls-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tableau 69. Contrôles qui permettent de créer des éditeurs de pages d’Assistant personnalisés  

|Contrôle|Description|  
|-|-|  
|[CollectionTControl](#CollectionTControl)|Ce contrôle sert à modifier les données stockées dans l’élément [Data](#Data) au sein d’un élément [Page](#Page).|  
|[FieldElementControl](#FieldElementControl)|Ce contrôle sert à modifier un champ généralement lié à un contrôle TextBox dans la page .xaml.|  
|[SetterControl](#SetterControl)|Ce contrôle sert à modifier la valeur d’un élément [setter]() dans le fichier de configuration d’UDI Wizard (Assistant UDI).|  

####  <a name="CollectionTControl"></a> CollectionTControl  
 Ce contrôle fournit de nombreuses fonctionnalités d’édition des données. La meilleure façon d’apprendre à utiliser ce contrôle est de consulter l’exemple qui montre comment modifier des données via l’élément **Data** d’une page. Plus précisément, l’exemple montre comment ajouter, supprimer et modifier des éléments dans ce contrôle.  

####  <a name="FieldElementControl"></a> FieldElementControl  
 Utilisez ce contrôle pour modifier un champ généralement lié à un contrôle **TextBox** dans la page .xaml.  

##### <a name="example"></a>Exemple  
 L’extrait suivant d’un fichier .xaml montre comment utiliser **FieldElementControl** pour configurer la valeur par défaut d’un champ dans une page d’Assistant à l’aide d’un contrôle **TextBox** enfant :  

```  
<Controls:FieldElementControl  
Width="450"  
Margin="0,5"  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
HeaderText="Location Combo Box"  
InstructionText="Here you can configure the behavior of the location combo box."  
HideValidationTab="True">  

<TextBox Text="{Binding FieldData.DefaultValue,  
 UpdateSourceTrigger=PropertyChanged,  
 Mode=TwoWay}"/>  
</Controls:FieldElementControl>  
```  

##### <a name="properties"></a>Propriétés  

###### <a name="fielddata"></a>FieldData  
 Cette propriété de type chaîne contient des informations qui permettent de connecter **FieldElementControl** au contenu XML sous-jacent du champ. La connexion est établie avec une propriété de l’interface de l’éditeur de page. L’extrait suivant d’un fichier .xaml montre comment utiliser la propriété **FieldData** :  

```  
FieldData="{Binding DataContext.Location, ElementName=ControlRoot}"  
```  

 Dans cet extrait, l’interface de l’éditeur de page s’appelle **ControlRoot** et est spécifiée dans le paramètre **ElementName**. La liaison est effectuée à la propriété **DataContext.Location** de l’interface de l’éditeur de page **ControlRoot**. **DataContext** est un modèle de vue qui pointe vers l’élément [Page](#Page) dans le fichier de configuration d’UDI Wizard (Assistant UDI). **Location** est une propriété de la vue qui retourne une liste des emplacements possibles et est définie par un élément [Data](#Data) dans le fichier de configuration d’UDI Wizard (Assistant UDI). Chaque emplacement est défini par un élément [DataItem](#DataItem) dans le fichier de configuration d’UDI Wizard (Assistant UDI).  

###### <a name="headertext"></a>HeaderText  
 Cette propriété de type chaîne vous permet de spécifier un en-tête pour le contrôle [FieldElementControl](#FieldElementControl). L’en-tête sert de titre au contrôle. Son texte, mis en forme en gras et en orange, s’affiche juste au-dessus du contrôle.  

###### <a name="instructiontext"></a>InstructionText  
 Cette propriété de type chaîne vous permet de spécifier un texte à caractère informatif pour le contrôle [FieldElementControl](#FieldElementControl). En règle générale, le texte permet de fournir une brève description du champ et d’expliquer comment la configuration de ce champ affecte la page correspondante de l’Assistant.  

###### <a name="hideenablebutton"></a>HideEnableButton  
 Cette propriété booléenne vous permet de contrôler la visibilité du bouton qui change d’état quand il passe de **Unlocked** à **Locked** (activé ou désactivé). Si sa valeur est :  

-   **True**, le bouton n’est pas visible  

-   **False**, le bouton est visible (valeur par défaut.)  

###### <a name="hidedefaulttab"></a>HideDefaultTab  
 Cette propriété booléenne vous permet de contrôler la visibilité de la section qui contient le contrôle utilisé pour définir la valeur par défaut. Bien que la propriété fasse référence à un onglet, il n’existe aucun onglet dans [FieldElementControl](#FieldElementControl) mais plutôt une section qui peut être masquée. Si sa valeur est :  

-   **True**, la section n’est pas visible  

-   **False**, la section est visible (valeur par défaut.)  

###### <a name="hideborder"></a>HideBorder  
 Cette propriété booléenne vous permet de contrôler la visibilité de la bordure autour du contrôle de champ. Si sa valeur est :  

-   **True**, la bordure n’est pas visible  

-   **False**, la bordure est visible (valeur par défaut.)  

###### <a name="hideimage"></a>HideImage  
 Cette propriété booléenne vous permet de contrôler la visibilité de l’image configurée par la propriété **FieldImageSource**. Si sa valeur est :  

-   **True**, l’image n’est pas visible  

-   **False**, l’image est visible (valeur par défaut.)  

###### <a name="hidevalidationtab"></a>HideValidationTab  
 Cette propriété booléenne vous permet de contrôler la visibilité de la section où est gérée la liste des validateurs. Bien que la propriété fasse référence à un onglet, il n’existe aucun onglet dans [FieldElementControl](#FieldElementControl) mais plutôt une section qui peut être masquée. Si sa valeur est :  

-   **True**, la section n’est pas visible  

-   **False**, la section est visible (valeur par défaut.)  

###### <a name="hidesummarytab"></a>HideSummaryTab  
 Cette propriété booléenne vous permet de contrôler la visibilité de la section dans laquelle vous configurez la légende de résumé du champ. La légende et la valeur correspondante du champ s’affichent dans une page d’Assistant de type **SummaryPage** au sein d’un flux d’étape. Bien que la propriété fasse référence à un onglet, il n’existe aucun onglet dans [FieldElementControl](#FieldElementControl) mais plutôt une section qui peut être masquée. Si sa valeur est :  

-   **True**, la section n’est pas visible  

-   **False**, la section est visible (valeur par défaut.)  

###### <a name="hidetasksequencetab"></a>HideTaskSequenceTab  
 Cette propriété booléenne vous permet de contrôler la visibilité de la section dans laquelle vous configurez la variable de séquence de tâches correspondant au champ. Bien que la propriété fasse référence à un onglet, il n’existe aucun onglet dans [FieldElementControl](#FieldElementControl) mais plutôt une section qui peut être masquée. Si sa valeur est :  

-   **True**, la section n’est pas visible  

-   **False**, la section est visible (valeur par défaut.)  


####  <a name="SetterControl"></a> SetterControl  
 Utilisez ce contrôle pour modifier la valeur d’un élément [Setter]() dans le fichier de configuration d’UDI Wizard (Assistant UDI). Ce contrôle contient un contrôle enfant qui permet de modifier la valeur de l’élément **setter**.  

##### <a name="example"></a>Exemple  
 L’extrait suivant d’un fichier .xaml montre comment utiliser **SetterControl** pour modifier un élément [Setter]() nommé **KeyLocationSetter** à l’aide d’un contrôle **TextBox** enfant.  

```  
<Controls:SetterControl Margin="5"  
        Width="450"  
        HeaderText="Title text"  
        SetterData="{Binding KeyLocationSetter}"   
        InstructionText="What this means…"  
        HorizontalAlignment="Left">  

    <TextBox  
                   Margin="0,3"  
                   Text="{Binding SetterData.SetterValue, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"  
    />  

</Controls:SetterControl>  
```  

##### <a name="properties"></a>Propriétés  

###### <a name="setterdata"></a>SetterData  
 Vous devez lier ceci à une propriété de votre vue ou modèle de vue qui se connecte au setter. Cela ressemble à la façon dont vous liez un champ, comme indiqué pour **FieldElementControl**.  

###### <a name="headertext"></a>HeaderText  
 Cette propriété vous permet de définir le texte qui apparaît dans l’en-tête du contrôle. Considérez cette propriété comme le titre du contrôle. Par défaut, son texte s’affiche en gras et en orange.  

###### <a name="instructiontext"></a>InstructionText  
 Définissez cette propriété en fonction du texte à afficher sous l’en-tête. En règle générale, il s’agit d’un texte d’instruction qui indique à l’utilisateur de votre éditeur personnalisé quand et pourquoi il souhaite modifier le comportement du champ.  

### <a name="interfaces"></a>Interfaces  
Le tableau 70 liste les interfaces qui permettent de créer des éditeurs de pages d’Assistant personnalisés.  

### <a name="table-70-interfaces-that-can-be-used-to-create-custom-wizard-page-editors"></a>Tableau 70. Interfaces qui permettent de créer des éditeurs de pages d’Assistant personnalisés  

|**Interface**|**Description**|  
|-|-|  
|[IDataService](#IDataService)|Utilisez cette interface pour connecter des champs aux éléments **Data** du fichier de configuration d’UDI Wizard (Assistant UDI).|  
|[IMessageBoxService](#IMessageBoxService)|Cette interface donne accès aux méthodes qui vous permettent d’afficher les boîtes de message.|  

####  <a name="IDataService"></a> IDataService  
 Cette interface contient plusieurs propriétés et méthodes, mais vous n’avez besoin que d’une seule propriété. Cette propriété est la seule documentée ici.  

 Vous pouvez utiliser l’injection de dépendances pour obtenir un pointeur vers cette interface en utilisant du code semblable à celui-ci dans votre classe :  

```  
[Dependency]  
public IDataService DataService { get; set; }  
```  

##### <a name="properties"></a>Propriétés  
 Le tableau 71 liste les propriétés de l’interface **IDataService**.  

### <a name="table-71-properties-for-the-idataservice-interface"></a>Tableau 71. Propriétés de l’interface IDataService  

|**Interface**|**Description**|  
|-|-|  
|[CurrentPage](#CurrentPage)|Cette propriété permet d’accéder aux éléments, attributs et valeurs XML situés sous le contexte de la page en cours de modification dans le fichier de configuration d’UDI Wizard (Assistant UDI).|  

######  <a name="CurrentPage"></a> CurrentPage  

```  
XElement CurrentPage { get; set; }  
```  

 Cette propriété donne accès au code XML de la page active. Vous ne devez jamais définir cette propriété. Toutefois, vous êtes libre de modifier le code XML de votre page. L’exemple d’éditeur de page montre des exemples de modification de code XML. Vous devez utiliser cette propriété principalement quand vous avez des données personnalisées. Pour les champs et les propriétés (setters), vous pouvez utiliser des contrôles prédéfinis qui prennent en charge tous les détails.  

####  <a name="IMessageBoxService"></a> IMessageBoxService  
 Cette interface donne accès aux méthodes qui vous permettent d’afficher les boîtes de message. Vous vous demandez peut-être pourquoi vous avez besoin d’une interface pour afficher une boîte de message. En fait, vous n’en avez pas besoin : Microsoft utilise cette interface dans le code, car elle permet d’écrire des tests automatisés pour les pages du concepteur.  

 Toutefois, l’utilisation de ces méthodes offre un avantage intéressant : le « propriétaire » des boîtes de dialogue est toujours UDI Wizard (Assistant UDI), ce qui garantit que la boîte de dialogue est correctement regroupée avec la fenêtre principale.  

 Vous pouvez utiliser l’injection de dépendances pour obtenir un pointeur vers cette interface en utilisant du code semblable à celui-ci dans votre classe :  

```  
[Dependency]  
public IMessageBoxService MessageBoxes { get; set; }  
```  

##### <a name="methods"></a>Méthodes  
 Le tableau 72 liste les méthodes de l’interface **IMessageBoxService**.  

### <a name="table-72-methods-for-the-imessageboxservice-interface"></a>Tableau 72. Méthodes de l’interface IMessageBoxService  

|**Méthode**|**Description**|  
|-|-|  
|[ShowMessageBox](#ShowMessageBox)|Cette méthode surchargée permet d’afficher une boîte de message avec les membres suivants :<br /><br /> -   [ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)<br />-   [ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)<br />-   [ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|  
|[ShowDialogWindow](#ShowDialogWindow)|Utilisez cette méthode pour créer une boîte de dialogue.|  
|[ShowWizardWindow](#ShowWizardWindow)|Utilisez cette méthode pour afficher un éditeur personnalisé dans une boîte de dialogue qui inclut les boutons de navigation **Suivant** et **Précédent**.|  

######  <a name="ShowMessageBox"></a> ShowMessageBox  
 Cette méthode affiche une boîte de message qui représente un enfant de l’éditeur de page d’Assistant personnalisé. Ce membre est surchargé : le tableau 73 contient une liste des membres et une brève description de chacun d’eux. Pour obtenir des informations complètes sur chaque membre (notamment la syntaxe, l’utilisation et les exemples), consultez la section correspondant à chacun d’entre eux.  

### <a name="table-73-overloaded-members-for-the-showmessagbox-method"></a>Tableau 73. Membres surchargés de la méthode ShowMessagBox  

|Membre|Description|  
|-|-|  
|[ShowMessageBox(String message, String caption, MessageBoxImage icon)](#ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon)|Affiche une boîte de message avec une icône et un bouton **OK**|  
|[ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)](#ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon)|Affiche une boîte de message avec une icône et différentes combinaisons possibles de boutons|  
|[ShowMessageBox(Exception exception)](#ShowMessageBox_Exception_exception)|Affiche une boîte de message qui fournit des informations sur une exception et comporte un bouton **OK**|  

######  <a name="ShowMessageBox_Stringmessage_Stringcaption_MessageBoxImage_icon"></a> ShowMessageBox(String message, String caption, MessageBoxImage icon)  

```  
void ShowMessageBox(String message, String caption, MessageBoxImage icon);  
```  

 Cette méthode affiche une boîte de message avec un bouton **OK**. Consultez le tableau 74.  

### <a name="table-74-parameters-for-the-showmessageboxstring-message-string-caption-messageboximage-icon-method"></a>Tableau 74. Paramètres de la méthode ShowMessageBox(String message, String caption, MessageBoxImage icon)  

|**Paramètre**|**Description**|  
|-|-|  
|**message**|Message à afficher dans la zone de contenu de la boîte de message|  
|**caption**|Texte à afficher dans la barre de titre de la boîte de dialogue|  
|**icon**|Type d’icône à afficher dans la boîte de message|  

######  <a name="ShowMessageBox_stringmessage_stringcaption_MessageBoxButtonbutton_MessageBoxImage_icon"></a> ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

```  
MessageBoxResult ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon);  
```  

 Cette méthode affiche une boîte de message avec l’ensemble de boutons à présenter, et signale le bouton sur lequel vous avez cliqué. Consultez le tableau 75.  

### <a name="table-75-parameters-for-the-showmessageboxstring-message-string-caption-messageboxbutton-button-messageboximage-icon-method"></a>Tableau 75. Paramètres de la méthode ShowMessageBox(string message, string caption, MessageBoxButton button, MessageBoxImage icon)  

|**Paramètre**|**Description**|  
|-|-|  
|**message**|Message à afficher dans la zone de contenu de la boîte de message|  
|**caption**|Texte à afficher dans la barre de titre de la boîte de dialogue|  
|**button**|Boutons à afficher|  
|**icon**|Type d’icône à afficher dans la boîte de message|  

######  <a name="ShowMessageBox_Exception_exception"></a> ShowMessageBox(Exception exception)  

```  
void ShowMessageBox(Exception exception);  
```  

 Cette méthode affiche une boîte de message qui signale les informations relatives à une exception. Cette boîte de message a un seul bouton **OK**. Consultez le tableau 76.  

### <a name="table-76-parameters-for-the-showmessageboxexception-exception-method"></a>Tableau 76. Paramètres de la méthode ShowMessageBox(Exception exception)  

|**Paramètre**|**Description**|  
|-|-|  
|**exception**|Exception à signaler (la boîte de dialogue utilise **exception.Message** comme contenu.)|  

######  <a name="ShowDialogWindow"></a> ShowDialogWindow  

```  
void ShowDialogWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Cette méthode crée une boîte de dialogue, dont le contenu correspond au texte spécifié dans le paramètre **viewType**. L’UDI Designer (Concepteur UDI) crée une instance de ce type et l’incorpore dans une boîte de dialogue avec les boutons **OK** et **Annuler**.  

 Vous passez les données à votre contrôle à l’aide du paramètre dialogPayload. La solution **SampleEditor** dans le répertoire du kit SDK contient un exemple d’utilisation de cette fonctionnalité.  

######  <a name="ShowWizardWindow"></a> ShowWizardWindow  

```  
void ShowWizardWindow(Type viewType, DialogInteraction dialogPayload);  
```  

 Cette méthode vous permet d’afficher un éditeur personnalisé dans une boîte de dialogue qui inclut les boutons de navigation **Suivant** et **Précédent**. Microsoft n’a pas fourni d’exemple d’utilisation de cette méthode.  

###  <a name="UDIWizardConfigurationFileSchemaReference"></a> Référence du schéma du fichier de configuration d’UDI Wizard (Assistant UDI)  
 Ce fichier est consommé par UDI Wizard (Assistant UDI) et configuré par UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce fichier permet de configurer les éléments suivants :  

-   Pages d’Assistant affichées dans UDI Wizard (Assistant UDI)  

-   Séquence des pages d’Assistant dans UDI Wizard (Assistant UDI)  

-   Paramètres des champs de chaque page d’Assistant  

-   StageGroups disponibles dans UDI Wizard Designer (Concepteur de l’Assistant UDI)  

-   Étapes disponibles au sein de chaque Assistant Déploiement dans UDI Wizard Designer (Concepteur de l’Assistant UDI)  

  Le tableau 77 liste les éléments du fichier de configuration d’UDI Wizard (Assistant UDI) et leurs descriptions. L’élément **Wizard** est le nœud racine de cette référence.  

### <a name="table-77-elements-in-the-udi-wizard-configuration-file-and-their-descriptions"></a>Tableau 77. Éléments du fichier de configuration d’UDI Wizard (Assistant UDI) et leurs descriptions  

|**Nom de l’élément**|**Description**|  
|-|-|  
|[Data](#Data)|Regroupe les éléments [DataItem](#DataItem) individuels dans un élément [Page](#Page) et est nommé par l’attribut **Name**.|  
|[DataItem](#DataItem)|Regroupe les éléments [Setter]() individuels dans un élément [Page](#Page). Vous pouvez créer des données hiérarchiques en incluant un ou plusieurs éléments [Data](#Data) dans un élément [DataItem](#DataItem). Chaque élément **DataItem** représente un élément individuel. Par exemple, une liste de lecteurs disponibles peut avoir un élément **DataItem** pour le nom d’affichage, et un autre élément **DataItem** pour la lettre de lecteur correspondante.|  
|[Par défaut](#Default)|Spécifie une valeur par défaut pour le champ spécifié dans l’élément [Field](#Field) ou [RadioGroup](#RadioGroup) parent. La valeur par défaut est définie en fonction de la valeur encadrée par cet élément.|  
|[DLL](#DLL)|Spécifie une DLL qui doit être chargée et référencée par UDI Wizard (Assistant UDI) et UDI Wizard Designer (Concepteur de l’Assistant UDI).|  
|[DLLs](#DLLs)|Regroupe les éléments [DLL](#DLL) individuels.|  
|[Erreur](#Error)|Spécifie un code d’erreur qu’une tâche peut retourner. La valeur du code d’erreur est retournée par la valeur **HRESULT** de la tâche, et est interceptée par cet élément pour fournir des informations d’erreur plus spécifiques.|  
|[ExitCode](#ExitCode)|Spécifie un code de sortie possible pour une tâche. Les codes de sortie sont des codes de retour attendus par la tâche. Créez un élément **ExitCode** pour chaque code de sortie possible. Sinon, spécifiez un astérisque (\*) dans l’attribut **Value** pour prendre en charge les codes de retour non listés dans les autres éléments **ExitCode**.|  
|[ExitCodes](#ExitCodes)|Regroupe un ensemble d’éléments [ExitCode](#ExitCode) et [Error](#Error) pour un élément [Task](#Task) ou un élément **Error**.|  
|[Field](#Field)|Spécifie une instance d’un contrôle dans un élément [Page](#Page) utilisé pour fournir une personnalisation en XML. Tous les contrôles n’autorisent pas la personnalisation en XML. Seuls les contrôles qui utilisent l’élément [Field](#Field) le permettent.|  
|[Fields](#Fields)|Regroupe les éléments [Field](#Field) individuels dans un élément [Page](#Page).|  
|[File](#File)|Spécifie la source et la destination d’une opération de copie de fichiers à l’aide du type de tâche **Microsoft.Wizard.CopyFilesTask**. Vous pouvez inclure un élément **File** distinct pour copier plusieurs fichiers dans une même tâche.|  
|[Page](#Page)|Spécifie une instance d’une page et inclut tous les paramètres de configuration de celle-ci.|  
|[PageRef](#PageRef)|Spécifie une référence à l’instance d’une page dans un élément [Stage](#Stage) au sein d’un élément [StageGroup](#StageGroup).|  
|[Pages](#Pages)|Regroupe les éléments [Page](#Page) individuels.|  
|[RadioGroup](#RadioGroup)|Spécifie un groupe de cases d’option dans un élément [Field](#Field).|  
|[StageGroup](#StageGroup)|Spécifie un groupe d’une ou de plusieurs étapes.|  
|[StageGroups](#StageGroups)|Regroupe un ensemble de groupes d’étapes dans un fichier de configuration d’UDI Wizard (Assistant UDI).|  
|[Setter]()|Spécifie le paramètre de propriété d’une valeur pour une propriété nommée dans la propriété **Property**.|  
|[Stage](#Stage)|Spécifie une étape dans un élément [StageGroup](#StageGroup) et contient un ou plusieurs éléments [PageRef](#PageRef).|  
|[Style](#Style)|Regroupe les éléments [setter]() individuels qui configurent l’apparence d’UDI Wizard (Assistant UDI), notamment le titre affiché en haut de l’Assistant et l’image de bannière affichée dans UDI Wizard (Assistant UDI).|  
|[Task](#Task)|Spécifie une tâche à exécuter sur la page spécifiée dans l’élément [Page](#Page) parent.|  
|[Tâches](#Tasks)|Regroupe un ensemble de tâches pour un élément [Page](#Page).|  
|[Validator](#Validator)|Spécifie un validateur pour le contrôle de champ indiqué dans l’élément [Field](#Field) parent.|  
|[Wizard](#Wizard)|Spécifie la racine de tous les autres éléments.|  

####  <a name="Data"></a> Data  
 Cet élément regroupe les éléments [DataItem](#DataItem) individuels dans un élément [Page](#Page) et est nommé par l’attribut **Name**.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 78 fournit des informations sur l’élément [Data](#Data).  

### <a name="table-78-data-element-information"></a>Tableau 78. Informations sur l’élément Data  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément [Page](#Page) (cet élément est facultatif.)|  
|Éléments parents|**Page**, **DataItem**|  
|Contenu|**DataItem**, **Setter**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 79 liste les attributs de l’élément [Data](#Data) et fournit une description de chacun d’eux.  

### <a name="table-79-attributes-and-corresponding-values-for-the-data-element"></a>Tableau 79. Attributs et valeurs correspondantes de l’élément Data  

|**Attribut**|**Description**|  
|-|-|  
|**Nom**|Spécifie le nom de l’élément [Data](#Data)|  

##### <a name="remarks"></a>Remarques  
 L’attribut **Name** permet au code de récupérer un ensemble de données spécifique.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="DataItem"></a> DataItem  
 Cet élément regroupe les éléments [Setter]() individuels dans un élément [Page](#Page). Vous pouvez créer des données hiérarchiques en incluant un ou plusieurs éléments [Data](#Data) dans un élément [DataItem](#DataItem). Chaque élément **DataItem** représente un élément individuel. Par exemple, une liste de lecteurs disponibles peut avoir un élément **DataItem** pour le nom d’affichage, et un autre élément **DataItem** pour la lettre de lecteur correspondante.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 80 fournit des informations sur l’élément [DataItem](#DataItem).  

### <a name="table-80-dataitem-element-information"></a>Tableau 80. Informations sur l’élément DataItem  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément [Data](#Data) (cet élément est facultatif.)|  
|Éléments parents|**Data**|  
|Contenu|**Data**, **Setter**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

#### <a name="default"></a>Valeur par défaut  
 Cet élément spécifie une valeur par défaut pour le champ spécifié dans l’élément [Field](#Field) ou [RadioGroup](#RadioGroup) parent. La valeur par défaut est définie en fonction de la valeur encadrée par cet élément.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 81 fournit des informations sur l’élément [Default](#Default).  

### <a name="table-81-default-element-information"></a>Tableau 81. Informations sur l’élément Default  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences |Zéro ou plus dans un élément [Field](#Field) ou [RadioGroup](#RadioGroup) (cet élément est facultatif.)|  
|Éléments parents|**Field**, **RadioGroup**|  
|Contenu|Il peut s’agir de tout contenu XML bien formé mais en règle générale, il s’agit de texte standard|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 Dans l’exemple suivant, la valeur par défaut du champ **TimeZone** est « Pacific Standard Time » :  

```  
<Field Name="TimeZone" Enabled="true" VarName="OSDTimeZone" Summary="Time Zone:">  
  <Default>Pacific Standard Time</Default>  
```  

####  <a name="DLL"></a> DLL  
 Cet élément spécifie une DLL à charger et référencer pour UDI Wizard (Assistant UDI) et UDI Wizard Designer (Concepteur de l’Assistant UDI).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 82 fournit des informations sur l’élément [DLL](#DLL).  

### <a name="table-82-dll-element-information"></a>Tableau 82. Informations sur l’élément DLL  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans l’élément [DLLs](#DLLs)|  
|Élément parent|**DLLs**|  
|Contenu|Aucun contenu n’est autorisé pour cet élément|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 83 liste les attributs de l’élément [DLL](#DLL) et fournit une description de chacun d’eux.  

### <a name="table-83-attributes-and-corresponding-values-for-the-dll-element"></a>Tableau 83. Attributs et valeurs correspondantes de l’élément DLL  

|**Attribut**|**Description**|  
|-|-|  
|Nom|Spécifie le nom de la DLL à référencer pour UDI Wizard (Assistant UDI) et UDI Wizard Designer (Concepteur de l’Assistant UDI)|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<DLLs>  
  <DLL Name="OSDRefreshWizard.dll" />   
  <DLL Name="SharedPages.dll" />  
</DLLs>  
```  

####  <a name="DLLs"></a> DLLs  
 Cet élément regroupe les éléments [DLL](#DLL) individuels.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 84 fournit des informations sur l’élément [DLLs](#DLLs).  

### <a name="table-84-dlls-element-information"></a>Tableau 84. Informations sur l’élément DLLs  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Un|  
|Éléments parents|**Wizard**|  
|Contenu|**DLL**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<DLLs>  
   <DLL Name="OSDRefreshWizard.dll" />  
   <DLL Name="SharedPages.dll" />   
</DLLs>  
```  

####  <a name="Error"></a> Error  
 Cet élément spécifie un code d’erreur qu’une tâche peut retourner. La valeur du code d’erreur est retournée et interceptée par la valeur **HRESULT** de la tâche pour fournir des informations d’erreur plus spécifiques.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 85 fournit des informations sur l’élément [Error](#Error).  

### <a name="table-85-error-element-information"></a>Tableau 85. Informations sur l’élément Error  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément [ExitCode](#ExitCode) (cet élément est facultatif.)|  
|Éléments parents|**ExitCodes**|  
|Contenu|Contenu XML bien formé|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 86 liste les attributs de l’élément [Error](#Error) et fournit une description de chacun d’eux.  

###  

|**Attribut**|**Description**|  
|-|-|  
|**État**|Spécifie l’état de retour d’une tâche ayant rencontré une erreur. En règle générale, la valeur de cet attribut est Error. Cette valeur est affichée dans la colonne **State** sur la page d’Assistant dans UDI Wizard (Assistant UDI).|  
|**Text**|Spécifie le texte descriptif de la condition d’erreur rencontrée par la tâche.|  
|**Type**|Spécifie si cet élément représente une erreur, un avertissement ou une opération réussie. La valeur spécifiée dans **Type** doit être unique au sein d’un élément [ExitCodes](#ExitCodes). Voici les valeurs valides pour cet élément :<br /><br /> -   **0.** L’élément représente une opération réussie.<br />-   **1.** L’élément représente un avertissement.<br />-   **-1.** L’élément représente une erreur.|  
|**Valeur**|Spécifie la valeur du code retourné par la tâche en tant que valeur numérique. La spécification d’un astérisque (*) indique l’élément par défaut pour les codes de retour qui ne sont pas listés dans les autres éléments [Error](#Error).|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="ExitCode"></a> ExitCode  
 Cet élément spécifie un code de sortie possible pour une tâche. Les codes de sortie sont des codes de retour attendus par la tâche. Créez un élément **ExitCode** pour chaque code de sortie possible. Sinon, spécifiez un astérisque (\*) dans l’attribut **Value** pour prendre en charge les codes de retour non listés dans les autres éléments **ExitCode**.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 87 fournit des informations sur l’élément [ExitCode](#ExitCode).  

### <a name="table-87-exitcode-element-information"></a>Tableau 87. Informations sur l’élément ExitCode  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément [ExitCodes](#ExitCodes) (cet élément est facultatif.)|  
|Éléments parents|**ExitCodes**|  
|Contenu|Au moins un élément [ExitCode](#ExitCode), et zéro élément [Error](#Error) ou plus|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 88 liste les attributs de l’élément [ExitCode](#ExitCode) et fournit une description de chacun d’eux.  

### <a name="table-88-attributes-and-corresponding-values-for-the-exitcode-element"></a>Tableau 88. Attributs et valeurs correspondantes de l’élément ExitCode  

|**Attribut**|Description|  
|-|-|  
|**État**|Spécifie l’état de retour d’une tâche. La valeur de cet attribut est affichée dans la colonne **State** sur la page d’Assistant correspondante dans UDI Wizard (Assistant UDI). Vous pouvez utiliser pour cet attribut des valeurs significatives par rapport à votre tâche. Voici les valeurs classiques utilisées pour cet attribut :<br /><br /> - Réussite<br />- Avertissement<br />-   Error|  
|**Text**|Spécifie le texte descriptif du code de sortie de la tâche.|  
|**Type**|Spécifie si cet élément représente une erreur, un avertissement ou une opération réussie. La valeur spécifiée dans Type doit être unique au sein d’un élément [ExitCodes](#ExitCodes). Voici les valeurs valides pour cet élément :<br /><br /> -   **0.** L’élément représente une opération réussie.<br />-   **1.** L’élément représente un avertissement.<br />-   **-1.** L’élément représente une erreur.|  
|**Valeur**|Spécifie la valeur du code retourné par la tâche en tant que valeur numérique. La spécification d’un astérisque (*) indique l’élément par défaut pour les codes de retour qui ne sont pas listés dans les autres éléments [ExitCode](#ExitCode).|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="ExitCodes"></a> ExitCodes  
 Cet élément regroupe un ensemble d’éléments [ExitCode](#ExitCode) et [Error](#Error) pour un élément [Task](#Task) ou un élément **Error**.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 89 fournit des informations sur l’élément [ExitCodes](#ExitCodes).  

### <a name="table-89-exitcodes-element-information"></a>Tableau 89. Informations sur l’élément ExitCodes  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une dans chaque élément [Task](#Task)|  
|Éléments parents|**Task**|  
|Contenu|**Error**, **ExitCode**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Field"></a> Field  
 Cet élément spécifie une instance d’un contrôle dans un élément [Page](#Page) utilisé pour fournir une personnalisation en XML. Tous les contrôles n’autorisent pas la personnalisation en XML. Seuls les contrôles qui utilisent l’élément [Field](#Field) le permettent.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 90 fournit des informations sur l’élément [Field](#Field).  

### <a name="table-90-field-element-information"></a>Tableau 90. Informations sur l’élément Field  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément [Field](#Field) (cet élément est facultatif.)|  
|Éléments parents|**Fields**|  
|Contenu|**Default**, **Validator**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 91 liste les attributs de l’élément [Field](#Field) et fournit une description de chacun d’eux.  

### <a name="table-91-attributes-and-corresponding-values-for-the-field-element"></a>Tableau 91. Attributs et valeurs correspondantes de l’élément Field  

|**Attribut**|**Description**|  
|-|-|  
|**Enabled**|Spécifie si le champ est activé pour l’entrée utilisateur (l’attribut peut avoir la valeur True ou False.)|  
|**Nom**|Spécifie le nom du champ|  
|**Résumé**|Spécifie le texte descriptif affiché dans la page d’Assistant **Résumé** pour la valeur définie par ce champ|  
|**VarName**|Spécifie le nom de variable de séquence de tâches lu ou configuré à l’aide du champ dans l’élément parent [Field](#Field)|  

##### <a name="remarks"></a>Remarques  
 Cet élément peut contenir zéro élément [Default](#Default) ou plus, ou plusieurs éléments [Validator](#Validator).  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Fields"></a> Fields  
 Cet élément regroupe les éléments [Field](#Field) individuels dans un élément [Page](#Page).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 92 fournit des informations sur l’élément [Fields](#Fields).  

### <a name="table-92-fields-element-information"></a>Tableau 92. Informations sur l’élément Fields  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément [Page](#Page) (cet élément est facultatif.)|  
|Éléments parents|**Page**|  
|Contenu|**Field**, **RadioGroup**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="File"></a> File  
 Cet élément spécifie la source et la destination d’une opération de copie de fichiers à l’aide du type de tâche **Microsoft.Wizard.CopyFilesTask**. Vous pouvez inclure un élément [File](#File) distinct pour copier plusieurs fichiers dans une même tâche.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 93 fournit des informations sur l’élément [File](#File).  

### <a name="table-93-file-element-information"></a>Tableau 93. Informations sur l’élément File  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs pour chaque tâche ayant un type de tâche **Microsoft.Wizard.CopyFilesTask**|  
|Éléments parents|**Task**|  
|Contenu|Aucun|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 94 liste les attributs de l’élément [File](#File) et fournit une description de chacun d’eux.  

### <a name="table-94-attributes-and-corresponding-values-for-the-file-element"></a>Tableau 94. Attributs et valeurs correspondantes de l’élément File  

|**Attribut**|**Description**|  
|-|-|  
|**Dest**|Spécifie le chemin complet ou relatif du dossier de destination pour le fichier spécifié dans l’attribut **Source**. Les variables d’environnement sont autorisées en tant qu’éléments faisant partie du chemin.|  
|**Source**|Spécifie le chemin complet ou relatif du fichier source copié par le type de tâche **Microsoft.Wizard.CopyFilesTask**. Cet attribut prend en charge les caractères génériques, ce qui permet de copier plusieurs fichiers à l’aide d’un seul élément [File](#File). Les variables d’environnement sont autorisées en tant qu’éléments faisant partie du chemin.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="PageElement"></a> Page  
 Cet élément spécifie une instance d’une page et inclut tous les paramètres de configuration de celle-ci.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 95 fournit des informations sur l’élément [Page](#Page).  

### <a name="table-95-page-element-information"></a>Tableau 95. Informations sur l’élément Page  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans chaque élément [Pages](#Pages)|  
|Éléments parents|**Pages**|  
|Contenu|**Data**, **Fields**, **Setter**, **Tasks**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 96 liste les attributs de l’élément [Page](#Page) et fournit une description de chacun d’eux.  

### <a name="table-96-attributes-and-corresponding-values-for-the-page-element"></a>Tableau 96. Attributs et valeurs correspondantes de l’élément Page  

|**Attribut**|**Description**|  
|-|-|  
|**DisplayName**|Spécifie le nom convivial de la page d’Assistant affichée dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce nom est généralement plus descriptif que l’attribut **Name**.|  
|**Nom**|Spécifie le nom de la page d’Assistant affichée dans UDI Wizard Designer (Concepteur de l’Assistant UDI).|  
|**Type**|Spécifie le type de page d’Assistant directement lié à une page d’Assistant particulière dans une DLL.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="PageRef"></a> PageRef  
 Cet élément spécifie une référence à l’instance d’une page dans un élément [Stage](#Stage) au sein d’un élément [StageGroup](#StageGroup).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 97 fournit des informations sur l’élément [PageRef](#PageRef).  

### <a name="table-97-pageref-element-information"></a>Tableau 97. Informations sur l’élément PageRef  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans un élément [Stage](#Stage)|  
|Éléments parents|**Stage**|  
|Contenu|Aucun|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 98 liste l’attribut de l’élément [PageRef](#PageRef), ainsi que sa description.  

### <a name="table-98-attributes-and-corresponding-values-for-the-pageref-element"></a>Tableau 98. Attributs et valeurs correspondantes de l’élément PageRef  

|**Attribut**|**Description**|  
|-|-|  
|**Page**|Spécifie l’instance d’une page dans un élément [Stage](#Stage) au sein d’un élément [StageGroup](#StageGroup). Affectez à cette valeur l’attribut Name d’un élément [Page](#Page).|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Pages"></a> Pages  
 Cet élément regroupe les éléments [Page](#Page) individuels.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 99 fournit des informations sur l’élément [Pages](#Pages).  

### <a name="table-99-pages-element-information"></a>Tableau 99. Informations sur l’élément Pages  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Un|  
|Éléments parents|**Wizard**|  
|Contenu|**Page**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<Pages>  
   + <Page Name="WelcomePage" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="ConfigScanPage" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="ConfigScanBareMetal" DisplayName="Deployment Readiness" Type="Microsoft.OSDRefresh.ConfigScanPage">  
   + <Page Name="RebootPage" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
   + <Page Name="WelcomePageReplace" DisplayName="Welcome" Type="Microsoft.SharedPages.WelcomePage">  
   + <Page Name="VolumePage" DisplayName="Volume" Type="Microsoft.OSDRefresh.VolumePage">  
   + <Page Name="UserRestorePage" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ComputerPage" DisplayName="New Computer Details" Type="Microsoft.OSDRefresh.ComputerPage">  
   + <Page Name="AdminAccounts" DisplayName="Administrator Password" Type="Microsoft.SharedPages.AdminAccountsPage">  
   + <Page Name="UDAPage" DisplayName="User Device Affinity" Type="Microsoft.OSDRefresh.UDAPage">  
   + <Page Name="LanguagePage" DisplayName="Language" Type="Microsoft.OSDRefresh.LanguagePage">  
   + <Page Name="ApplicationPage" DisplayName="Install Programs" Type="Microsoft.OSDRefresh.ApplicationPage">  
     <Page Name="SummaryPage" DisplayName="Summary" Type="Microsoft.Shared.SummaryPage" />   
   + <Page Name="UserCapturePageOldPC" DisplayName="Select Target" Type="Microsoft.OSDRefresh.UserStatePage">  
   + <Page Name="ProgressPage" DisplayName="Capture Data" Type="Microsoft.OSDRefresh.ProgressPage">  
   + <Page Name="RebootAfterCapture" DisplayName="Reboot" Type="Microsoft.OSDRefresh.RebootPage">  
</Pages>  
```  

####  <a name="RadioGroup"></a> RadioGroup  
 Cet élément spécifie un groupe de cases d’option dans un élément [Field](#Field).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 100 fournit des informations sur l’élément [RadioGroup](#RadioGroup).  

### <a name="table-100-radiogroup-element-information"></a>Tableau 100. Informations sur l’élément RadioGroup  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans un élément [Fields](#Fields) (cet élément est facultatif.)|  
|Éléments parents|**Fields**|  
|Contenu|**Par défaut**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 101 liste les attributs de l’élément [RadioGroup](#RadioGroup) et fournit une description de chacun d’eux.  

### <a name="table-101-attributes-and-corresponding-values-for-the-radiogroup-element"></a>Tableau 101. Attributs et valeurs correspondantes de l’élément RadioGroup  

|**Attribut**|**Description**|  
|-|-|  
|**Locked**|Spécifie si le groupe de cases d’option est activé pour l’entrée utilisateur. L’attribut peut avoir la valeur :<br /><br /> -   **True**. Spécifie que les cases d’option sont désactivées et que les utilisateurs ne peuvent pas sélectionner de case d’option dans le groupe.<br />-   **False**. Spécifie que les cases d’option sont activées et que les utilisateurs peuvent sélectionner une case d’option dans le groupe.|  
|**Nom**|Spécifie le nom du groupe de cases d’option.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="StageGroup"></a> StageGroup  
 Cet élément spécifie un groupe d’étapes de déploiement.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 102 fournit des informations sur l’élément [StageGroup](#StageGroup).  

### <a name="table-102-stagegroup-element-information"></a>Tableau 102. Informations sur l’élément StageGroup  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans un élément [StageGroups](#StageGroups)|  
|Éléments parents|**StageGroups**|  
|Contenu|**Stage**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Le tableau 103 liste l’attribut de l’élément [StageGroup](#StageGroup), ainsi que sa description.  

### <a name="table-103-attributes-and-corresponding-values-for-the-stagegroup-element"></a>Tableau 103. Attributs et valeurs correspondantes de l’élément StageGroup  

|**Attribut**|**Description**|  
|-|-|  
|**DisplayName**|Spécifie le nom convivial du groupe d’étapes affiché dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce nom est généralement plus descriptif que l’attribut **Name**.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="StageGroups"></a> StageGroups  
 Cet élément regroupe un ensemble de groupes d’étapes dans un fichier de configuration d’UDI Wizard (Assistant UDI).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 104 fournit des informations sur l’élément [StageGroups](#StageGroups).  

### <a name="table-104-stagegroups-element-information"></a>Tableau 104. Informations sur l’élément StageGroups  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou une dans un élément [Wizard](#Wizard)|  
|Éléments parents|**Wizard**|  
|Contenu|**StageGroup**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Setter"></a> Setter  
 Cet élément spécifie un paramètre de propriété pour la valeur d’une propriété nommée dans la propriété **Property**.  

##### <a name="element-information"></a>Informations sur l'élément  
 Le tableau 105 fournit des informations sur l’élément [Setter]().  

### <a name="table-105-setter-element-information"></a>Tableau 105. Informations sur l’élément Setter  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou plus dans chaque élément parent (cet élément est facultatif.)|  
|Éléments parents|**Data**, **DataItem**, **Page**, **Style**, **Task**, **Validator**|  
|Contenu|Contient une valeur de chaîne dans l’attribut **Property**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 106 liste l’attribut de l’élément [Setter](), ainsi que sa description.  

### <a name="table-106-attributes-and-corresponding-values-for-the-setter-element"></a>Tableau 106. Attributs et valeurs correspondantes de l’élément Setter  

|**Attribut**|**Description**|  
|-|-|  
|**Propriété**|Spécifie le nom de propriété défini. Le nom de propriété est défini en fonction de la valeur encadrée par cet attribut.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

#### <a name="stage"></a>Étape  
 Cet élément spécifie un élément [Stage](#Stage) dans un élément [StageGroup](#StageGroup), et contient un ou plusieurs éléments [PageRef](#PageRef).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 107 fournit des informations sur l’élément [Stage](#Stage).  

### <a name="table-107-stage-element-information"></a>Tableau 107. Informations sur l’élément Stage  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans un élément [StageGroup](#StageGroup)|  
|Éléments parents|**StageGroup**|  
|Contenu|**PageRef**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 108 liste les attributs de l’élément [Stage](#Stage) et fournit une description de chacun d’eux.  

### <a name="table-108-attributes-and-corresponding-values-for-the-stage-element"></a>Tableau 108. Attributs et valeurs correspondantes de l’élément Stage  

|**Attribut**|**Description**|  
|-|-|  
|**DisplayName**|Spécifie le nom convivial de la page d’Assistant affichée dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce nom est généralement plus descriptif que l’attribut **Name**.|  
|**Nom**|Spécifie le nom de l’étape. La valeur de cet élément est utilisée au démarrage d’UDI Wizard (Assistant UDI) avec le paramètre de ligne de commande **/stage: name**.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Style"></a> Style  
 Cet élément regroupe les éléments [Setter]() individuels qui configurent l’apparence d’UDI Wizard (Assistant UDI), notamment le titre affiché en haut de l’Assistant et l’image de bannière affichée dans UDI Wizard (Assistant UDI).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 109 fournit des informations sur l’élément Style.  

### <a name="table-109-style-element-information"></a>Tableau 109. Informations sur l’élément Style  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Un|  
|Éléments parents|**Wizard**|  
|Contenu|**Setter**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<Style>  
  <Setter Property="bannerFilename">UDI_Wizard_Banner.bmp</Setter>   
  <Setter Property="title">Operating System Deployment (OSD) Refresh Wizard</Setter>   
</Style>  
```  

####  <a name="TaskElement"></a> Task  
 Cet élément spécifie une tâche à exécuter sur la page spécifiée dans l’élément [Page](#Page) parent.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 110 fournit des informations sur l’élément [Task](#Task).  

### <a name="table-110-task-element-information"></a>Tableau 110. Informations sur l’élément Task  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Une ou plusieurs dans un élément [Tasks](#Tasks)|  
|Éléments parents|**Tâches**|  
|Contenu|**ExitCodes**, **File**, **Setter**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 111 liste les attributs de l’élément [Task](#Task) et fournit une description de chacun d’eux.  

### <a name="table-111-attributes-and-corresponding-values-for-the-task-element"></a>Tableau 111. Attributs et valeurs correspondantes de l’élément Task  

|**Attribut**|**Description**|  
|-|-|  
|**DependsOn**|Spécifie si la tâche dépend d’une autre tâche. La valeur de cet attribut est définie en fonction de l’attribut **Name** d’un autre élément [Task](#Task). **Remarque :** Vous ne pouvez pas configurer cet attribut à l’aide d’UDI Wizard Designer (Concepteur de l’Assistant UDI). Toutefois, vous pouvez ajouter manuellement cet attribut à un élément [Task](#Task) en modifiant directement le fichier .xml.|  
|**DisplayName**|Spécifie le nom convivial de la tâche affichée dans UDI Wizard Designer (Concepteur de l’Assistant UDI). Ce nom est généralement plus descriptif que l’attribut **Name**.|  
|**Nom**|Spécifie le nom de la tâche. Ce nom doit être unique.|  
|Tapez|Spécifie le type de la tâche à exécuter, lequel est défini dans la DLL qui contient la tâche.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Tasks"></a> Tasks  
 Cet élément regroupe un ensemble de tâches pour un élément [Page](#Page).  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 112 fournit des informations sur l’élément [Tasks](#Tasks).  

### <a name="table-112-tasks-element-information"></a>Tableau 112. Informations sur l’élément Tasks  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou une dans chaque élément [Page](#Page) (cet élément est facultatif.)|  
|Éléments parents|**Page**|  
|Contenu|**Task**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 113 liste les attributs de l’élément [Tasks](#Tasks) et fournit une description de chacun d’eux.  

### <a name="table-113-attributes-and-corresponding-values-for-the-tasks-element"></a>Tableau 113. Attributs et valeurs correspondantes de l’élément Tasks  

|**Attribut**|**Description**|  
|-|-|  
|**NameTitle**|Spécifie la légende qui apparaît en haut de la colonne contenant le nom des tâches dans la page d’Assistant appropriée.|  
|**StatusTitle**|Spécifie la légende qui apparaît en haut de la colonne contenant l’état des tâches dans la page d’Assistant appropriée.|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="ValidatorElement"></a> Validator  
 Cet élément spécifie un validateur pour le contrôle de champ indiqué dans l’élément [Field](#Field) parent.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 114 fournit des informations sur l’élément [Validator](#Validator).  

### <a name="table-114-validator-element-information"></a>Tableau 114. Informations sur l’élément Validator  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Zéro ou une dans un élément [Field](#Field)|  
|Éléments parents|**Field**|  
|Contenu|**Setter**|  

##### <a name="element-attributes"></a>Attributs d’élément  
Le tableau 115 liste l’attribut de l’élément [Validator](#Validator), ainsi que sa description.  

### <a name="table-115-attributes-and-corresponding-values-for-the-validator-element"></a>Tableau 115. Attributs et valeurs correspondantes de l’élément Validator  

|**Attribut**|**Description**|  
|-|-|  
|Tapez|Spécifie le type du validateur, lequel est défini dans la DLL qui contient le validateur|  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  
 aucune.  

####  <a name="Wizard"></a> Wizard  
 Cet élément spécifie la racine de tous les autres éléments.  

##### <a name="element-information"></a>Informations sur l'élément  
Le tableau 116 fournit des informations sur l’élément [Wizard](#Wizard).  

### <a name="table-116-wizard-element-information"></a>Tableau 116. Informations sur l’élément Wizard  

|**Attribut**|**Valeur**|  
|-|-|  
|Nombre d’occurrences|Un|  
|Éléments parents|Aucun|  
|Contenu|**DLLs**, **Pages**, **StageGroups**, **Style**|  

##### <a name="element-attributes"></a>Attributs d’élément  
 Cet élément n’a aucun attribut.  

##### <a name="remarks"></a>Remarques  
 aucune.  

##### <a name="example"></a>Exemple  

```  
<Wizard>  
   + <DLLs>  
   + <Style>  
   + <Pages>  
   + <StageGroups>  
</Wizard>  
```
