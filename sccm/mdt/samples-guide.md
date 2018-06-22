---
title: Exemples MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Exemples Microsoft Deployment Toolkit (MDT) '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 2ff0100c-b7ef-4e09-8c96-fc1898390b6d
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 6b36da9f98749858829ab591571496532b26f290
ms.sourcegitcommit: 7198ec49d9ce68c6d55bfb9e2d537b5442a132cb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2018
ms.locfileid: "33915970"
---
# <a name="microsoft-deployment-toolkit-samples-guide"></a>Guide d’exemples Microsoft Deployment Toolkit  
 Ce guide fait partie de Microsoft® Deployment Toolkit (MDT) 2013 et aide une équipe de spécialistes à déployer des systèmes d’exploitation Windows et Microsoft Office. Plus précisément, ce guide est conçu pour fournir des exemples de paramètres de configuration pour des scénarios de déploiement spécifiques.  

> [!NOTE]
>  Dans ce document, le terme *Windows* fait référence aux systèmes d’exploitation Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2, sauf indication contraire. MDT ne prend pas en charge les versions de Windows pour les processeurs ARM. Le terme *MDT* fait référence à MDT 2013, sauf indication contraire.  

 **Pour utiliser ce guide**  

 Passez en revue la liste des rubriques relatives aux scénarios dans la table des matières.  

1.  Sélectionnez le scénario qui correspond le mieux aux objectifs de déploiement de votre organisation.  

2.  Consultez les exemples de paramètres de configuration pour le scénario sélectionné.  

3.  Utilisez les exemples de paramètres de configuration comme base pour les paramètres de configuration dans votre environnement.  

4.  Personnalisez les exemples de paramètres de configuration pour votre environnement.  

 Dans de nombreux cas, plusieurs scénarios peuvent être nécessaires pour couvrir tous les paramètres de configuration de l’environnement.  

 Comme ce guide contient seulement des exemples de paramètres de configuration, consultez les guides listés dans le tableau suivant pour vous aider davantage à personnaliser les paramètres de configuration de l’environnement.  

 |Guide|Ce guide est destiné à vous aider|  
 |-|-|  
 |*Guide de démarrage rapide pour Microsoft System Center 2012 R2 Configuration Manager* |Utilisez System Center 2012 R2 Configuration Manager pour installer le système d’exploitation Windows 8.1 dans un scénario de déploiement d’un nouvel ordinateur.|  
 |*Guide de démarrage rapide pour l’installation avec intervention limitée (LTI)* |Installez le système d’exploitation Windows 8.1 via une installation LTI en utilisant un support de démarrage dans un scénario de déploiement de nouvel ordinateur.|  
 |*Guide de démarrage rapide pour l’installation pilotée par l’utilisateur (UDI)* |Installez le système d’exploitation Windows 8.1 avec l’installation UDI et System Center 2012 R2 Configuration Manager dans un scénario de déploiement d’un nouvel ordinateur.|  
 |*Utilisation de Microsoft Deployment Toolkit* |Personnalisez davantage les fichiers de configuration utilisés dans les déploiements avec installation sans intervention (ZTI) et installation LTI. Ce guide fournit également des conseils généraux pour la configuration et des informations techniques de référence pour les paramètres de configuration.|


## <a name="deploying-windows-8-applications-using-mdt"></a>Déploiement d’applications Windows 8 avec MDT  
 MDT peut déployer des packages d’application Windows 8, qui ont une extension de fichier .aspx. Ces packages d’applications sont nouveaux dans Windows 8. Pour plus d’informations sur ces applications, consultez [Développement d’applications du Windows Store.](http://msdn.microsoft.com/windows/apps)  

 Déployez des applications Windows 8 avec MDT en effectuant les étapes suivantes :  

-   Déployez des applications Windows 8 avec installation LTI comme décrit dans [Déploiement d’applications Windows 8 avec installation LTI](#DeployWin8LTI).  

-   Déployez des applications Windows 8 avec installation UDI comme décrit dans [Déploiement d’applications Windows 8 avec installation UDI](#DeployWin8UDI).  

###  <a name="DeployWin8LTI"></a> Déploiement d’applications Windows 8 avec installation LTI  
 Vous pouvez déployer des applications Windows 8 avec installation LTI comme toute autre application lançant le processus d’installation à partir d’une ligne de commande. Vous pouvez ajouter des applications Windows 8 à des déploiements avec installation LTI dans le nœud Applications de Deployment Workbench.  

 **Pour déployer une application Windows 8 avec une installation LTI**  

1.  Créez un dossier réseau partagé dans lequel stocker l’application.  

2.  Copiez l’application Windows 8 dans le dossier réseau partagé créé à l’étape précédente.  

     Veillez à copier le fichier .aspx de l’application Windows 8 et tous les autres fichiers nécessaires, comme un fichier .cer contenant le certificat de l’application.  

3.  Créez un élément d’application avec installation LTI pour l’application Windows 8 dans le nœud Applications de Deployment Workbench avec l’Assistant New Application (Nouvelle Application).  

     Dans l’Assistant New Application (Nouvelle application), dans la page **Command Details** (Détails de la commande), dans **Command line** (Ligne de commande), tapez **nom_fichier_application** (où *nom_fichier_application* est le nom de l’application Windows 8).  

     Pour plus d’informations sur l’exécution de l’Assistant New Application (Nouvelle application) dans Deployment Workbench, consultez les sections suivantes dans le document MDT, *Utilisation du Microsoft Deployment Toolkit* :  

    -   « Créer une application déployée à partir du partage de déploiement »  

    -   « Créer une application déployée à partir d’un autre dossier réseau partagé »  

4.  Sélectionnez l’élément d’application avec installation LTI créé à l’étape précédente dans une séquence de tâches d’installation LTI.  

###  <a name="DeployWin8UDI"></a> Déploiement d’applications Windows 8 avec une installation UDI  
 Vous pouvez déployer des applications Windows 8 avec une installation UDI comme toute autre application lançant le processus d’installation à partir d’une ligne de commande. Vous pouvez ajouter des applications Windows 8 à des déploiements d’installation UDI dans la page **ApplicationPage** de l’Assistant dans le Concepteur de l’Assistant Installation UDI.  

> [!NOTE]
>  Le déploiement de Windows 8 et d’applications Windows 8 avec une installation UDI nécessite System Center 2012 R2 Configuration Manager.  

 **Pour déployer une application Windows 8 avec une installation UDI**  

1.  Créez un dossier réseau partagé dans lequel stocker l’application.  

     Ce dossier est le dossier source de l’application Configuration Manager que vous créez plus loin dans le processus.  

2.  Copiez l’application Windows 8 dans le dossier réseau partagé créé à l’étape précédente.  

     Veillez à copier le fichier .aspx de l’application Windows 8 et tous les autres fichiers nécessaires, comme un fichier .cer contenant le certificat de l’application.  

3.  Ajouter l’application Windows 8 comme application Configuration Manager  

4.  Créez un élément d’application Configuration Manager pour l’application Windows 8 avec l’Assistant Création d’application dans la console Configuration Manager.  

     Dans l’Assistant Création d’application, créez un type de déploiement pour déployer l’application Windows 8 avec l’Assistant Création d’un type de déploiement. Dans l’Assistant Création d’un type de déploiement, dans la page **Contenu**, dans **Programme d’installation**, tapez **nom_fichier_application** (où *nom_fichier_application*est le nom de l’application Windows 8).  

     Pour plus d’informations sur l’exécution de l’Assistant Création d’application dans la console Configuration Manager, consultez les sections suivantes de la bibliothèque de documentation pour System Center 2012 Configuration Manager, que vous trouverez dans Configuration Manager :  

    -   [Comment créer des applications dans Configuration Manager](http://technet.microsoft.com/library/gg682159.aspx)  

    -   [Comment créer des types de déploiement dans Configuration Manager](http://technet.microsoft.com/library/gg682174.aspx#BKMK_Step3)  

    -   [Comment gérer les applications et les types de déploiement dans Configuration Manager](http://technet.microsoft.com/library/gg682031)  

5.  Vérifiez que la fonctionnalité d’affinité entre utilisateur et appareil de Configuration Manager est correctement configurée pour prendre en charge l’affinité entre utilisateurs et appareils pour le déploiement d’application Configuration Manager.  

     Pour plus d’informations sur la configuration de l’affinité entre utilisateur et appareil permettant de prendre en charge le déploiement d’application Configuration Manager, consultez [Comment gérer l’affinité entre utilisateur et appareil dans Configuration Manager](http://technet.microsoft.com/library/gg699365).  

6.  Déployez l’application créée à l’étape 4 sur les utilisateurs ciblés.  

     Pour plus d’informations sur le déploiement d’une application sur un utilisateur, consultez [Comment déployer des applications dans Configuration Manager](http://technet.microsoft.com/library/gg682082).  

7.  Configurez la page **ApplicationPage** de l’Assistant pour y inclure l’application Configuration Manager créée à l’étape 4 avec le Concepteur de l’Assistant UDI.  

     Pour plus d’informations sur la façon de configurer la page **ApplicationPage** de l’Assistant avec le Concepteur de l’Assistant UDI, consultez la section « Étape 5-11 : personnaliser le fichier de configuration de l’Assistant UDI pour l’ordinateur cible » dans le document MDT *Démarrage rapide pour l’installation UDI*.  

8.  Sélectionnez l’élément d’application avec installation UDI créé à l’étape précédente dans une séquence de tâches d’installation UDI.  

    > [!NOTE]
    >  L’application Windows 8 n’est pas installée par la séquence de tâches : au lieu de cela, elle est installée la première fois que l’utilisateur ouvre une session sur l’ordinateur ciblé (comme défini par le paramètre d’affinité entre utilisateur et appareil configuré à l’étape 5) avec la fonctionnalité de programme d’installation d’application orienté utilisateur (AppInstall.exe) dans l’installation UDI.  

     Pour plus d’informations sur la fonctionnalité de programme d’installation d’application orienté utilisateur dans l’installation UDI, consultez la section « Informations de référence sur le programme d’installation d’application orienté utilisateur », dans le document MDT *Informations de référence sur la boîte à outils*.  

## <a name="managing-mdt-using-windows-powershell"></a>Gestion de MDT avec Windows PowerShell  
 Vous pouvez gérer les partages de déploiement MDT avec Deployment Workbench et Windows PowerShell. MDT contient un composant logiciel enfichable Windows PowerShell™ (Microsoft.BDD.SnapIn), qui doit être chargé avant l’utilisation des fonctionnalités spécifiques à MDT dans Windows PowerShell. Le composant logiciel enfichable Windows PowerShell de MDT inclut :  

-   Un fournisseur Windows PowerShell (MDTProvider), qui fournit l’accès au contenu d’un partage de déploiement  

-   Des applets de commande qui permettent d’administrer les partages de déploiement MDT  

 Gérez les partages de déploiement MDT avec Windows PowerShell en effectuant les étapes suivantes :  

-   Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

-   Créez un partage de déploiement avec Windows PowerShell comme décrit dans [Création d’un partage de déploiement avec Windows PowerShell](#CreateDeployShare).  

-   Affichez les propriétés d’un partage de déploiement avec Windows PowerShell comme décrit dans [Affichage des propriétés d’un partage de déploiement avec Windows PowerShell](#ViewDeployShareProp).  

-   Affichez la liste des partages de déploiement avec Windows PowerShell comme décrit dans [Affichage de la liste des partages de déploiement avec Windows PowerShell](#ViewListDeployShare).  

-   Mettez à jour un partage de déploiement, ce qui génère de nouvelles images de démarrage Windows PE, comme décrit dans [Mise à jour d’un partage de déploiement avec Windows PowerShell](#UpdateDeployShare).  

-   Mettez à jour un partage de déploiement lié, ce qui réplique le contenu d’un partage de déploiement sur le partage de déploiement lié, comme décrit dans [Mise à jour d’un partage de déploiement lié avec Windows PowerShell](#UpdateLinkedDeployShare).  

-   Mettez à jour le support de déploiement, qui réplique le contenu d’un partage de déploiement sur le support de déploiement, puis génère de nouvelles images de démarrage comme décrit dans [Mise à jour du support de déploiement avec Windows PowerShell](#UpdateDeployMedia).  

-   Gérez les éléments d’un partage de déploiement (comme les systèmes d’exploitation, les packages de système d’exploitation, les applications et les pilotes de périphérique) comme décrit dans [Gestion des éléments d’un partage de déploiement avec Windows PowerShell](#ManageItemDeployShare).  

-   Automatisez le remplissage des éléments d’un partage de déploiement (comme les systèmes d’exploitation, les packages de système d’exploitation, les applications et les pilotes de périphérique) comme décrit dans [Automatisation du remplissage d’un partage de déploiement](#AutomatePopulateDeployShare).  

-   Gérez les dossiers d’un partage de déploiement avec Windows PowerShell comme décrit dans [Gestion des dossiers d’un partage de déploiement avec Windows PowerShell](#ManageDeployShareFolder).  

###  <a name="LoadMDTSnapIn"></a> Chargement du composant logiciel enfichable Windows PowerShell de MDT  
 Les applets de commande MDT sont fournies dans un composant logiciel enfichable Windows PowerShell, **Microsoft.BDD.SnapIn**, qui doit être chargé avant l’utilisation des applets de commande MDT. Vous pouvez charger le composant logiciel enfichable Windows PowerShell de MDT selon une des méthodes suivantes :  

-   Chargez le composant logiciel enfichable Windows PowerShell de MDT avec la console Modules Windows PowerShell comme décrit dans [Charger le composant logiciel enfichable Windows PowerShell de MDT avec la tâche Importer les modules système](#LoadMDTSnapInImport).  

-   Chargez le composant logiciel enfichable Windows PowerShell de MDT avec l’applet de commande **Add-PSSnapIn**, comme décrit dans [Charger le composant logiciel enfichable Windows PowerShell de MDT avec l’applet de commande Add-PSSnapIn](#LoadMDTSnapInCmdlet).  

####  <a name="LoadMDTSnapInImport"></a> Charger le composant logiciel enfichable Windows PowerShell de MDT avec la tâche Importer les modules système  
 La tâche Importer les modules système inclut automatiquement tous les modules et les composants logiciels enfichables Windows PowerShell qui se trouvent dans les modules du répertoire %Windir%\System32\WindowsPowerShell\1.0\Modules. MDT installe automatiquement le composant logiciel enfichable Windows PowerShell de MDT **Microsoft.BDD.SnapIn** dans ce dossier lors du processus d’installation de MDT.  

> [!NOTE]
>  La tâche Importer les modules système est disponible seulement dans Windows 7 et Windows Server 2008 R2 quand Windows PowerShell 3.0 n’est pas installé sur l’ordinateur. À compter de Windows PowerShell 3.0, les modules sont importés automatiquement la première fois que vous utilisez une applet de commande dans le module.  

 Vous pouvez démarrer une console Windows PowerShell avec la tâche Import System Modules (Importer les modules système) en effectuant une des procédures suivantes :  

-   Dans la barre des tâches, cliquez avec le bouton droit sur l’icône **Windows PowerShell**, puis cliquez sur **Import System Modules** (Importer les modules système).  

-   Cliquez sur **Démarrer**, pointez sur **Outils d’administration**, puis cliquez sur **Modules Windows PowerShell**.  

 Pour plus d’informations sur le démarrage d’une console Windows PowerShell avec Import System Modules (Importer les modules système), consultez [Starting Windows PowerShell with Import System Modules](http://msdn.microsoft.com/library/windows/desktop/hh847866.aspx).  

####  <a name="LoadMDTSnapInCmdlet"></a> Charger le composant logiciel enfichable Windows PowerShell de MDT avec l’applet de commande Add-PSSnapIn  
 Vous pouvez charger le composant logiciel enfichable Windows PowerShell de MDT, **Microsoft.BDD.PSSnapIn**, à partir de n’importe quel environnement Windows PowerShell avec l’applet de commande [Add-PSSnapIn](http://technet.microsoft.com/library/hh849705.aspx), comme indiqué dans l’exemple suivant :  

```  
Add-PSSnapin -Name Microsoft.BDD.PSSnapIn  
```  

###  <a name="CreateDeployShare"></a> Création d’un partage de déploiement avec Windows PowerShell  
 Vous pouvez créer des partages de déploiement avec les applets de commande Windows PowerShell de MDT. Le dossier racine pour le partage de déploiement est créé et partagé avec des applets de commande Windows PowerShell standard, et des appels à des commandes des classes WMI (Windows Management Instrumentation). Le partage de déploiement est rempli avec le fournisseur Windows PowerShell MDTProvider et l’applet de commande [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx). Le lecteur Windows PowerShell MDTProvider est rendu persistant avec l’applet de commande **Add-MDTPersistentDrive**.  

 **Pour préparer un partage de déploiement avec les applets de commande Windows PowerShell de MDT**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Créez le dossier qui sera la racine du nouveau partage de déploiement avec l’applet de commande **New-Item**, comme indiqué dans l’exemple suivant et décrit dans [Utilisation de l’applet de commande New-Item](http://technet.microsoft.com/library/ee176914.aspx) :  

    ```  
    New-Item "C:\MDTDeploymentShare$" -Type directory  
    ```  

     L’applet de commande indique que la création du dossier a été effectuée.  

3.  Partagez le dossier créé à l’étape précédente en utilisant la classe **WMI win32_share** comme indiqué dans l’exemple suivant :  

    ```  
    ([wmiclass]"win32_share").Create("C:\MDTDeploymentShare$", "MDTDeploymentShare$",0)  
    ```  

     L’appel à la classe **win32_share** retourne les résultats de l’appel. Si la valeur de **ReturnValue** est zéro (0), c’est que l’appel a réussi.  

4.  Spécifiez le nouveau dossier partagé comme partage de déploiement avec l’applet de commande [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx), comme indiqué dans l’exemple suivant :  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose  
    ```  

     L’applet de commande démarre automatiquement la création du partage de déploiement et la copie des informations du modèle dans le nouveau partage de déploiement. À la fin du processus de copie, l’applet de commande affiche les informations du nouveau partage de déploiement.  

    > [!NOTE]
    >  La valeur fournie dans le paramètre *Name* (DS002) doit être unique et ne peut pas être identique à un lecteur Windows PowerShell de partage de déploiement existant.  

5.  Vérifiez que les dossiers appropriés du partage de déploiement ont été créés avec la commande **dir**, comme indiqué dans l’exemple suivant :  

    ```  
    dir ds002:  
    ```  

     La liste des dossiers par défaut à la racine du partage de déploiement s’affiche.  

6.  Ajoutez le nouveau partage de déploiement à la liste des partages de déploiement MDT persistants avec l’applet de commande **Add-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    $NewDS=Get-PSDrive "DS002"  
    Add-MDTPersistentDrive  -Name "DS002" -InputObject $NewDS Verbose  
    ```  

     Dans cet exemple, la variable *$NewDS* est utilisée pour passer l’objet de lecteur Windows PowerShell du nouveau partage de déploiement à l’applet de commande.  

     Vous pouvez aussi combiner les applets de commande [NewPSDrive](http://technet.microsoft.com/library/dd315340.aspx) et **Add-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "C:\MDTDeploymentShare$" -Description "MDT Deployment Share Created with Cmdlets" -NetworkPath "\\WDG-MDT-01\MDTDeploymentShare$" -Verbose | Add-MDTPersistentDrive -Verbose  
    ```  

     Dans l’exemple précédent, le pipeline Windows PowerShell fournit à la fois les paramètres *Name* et *InputObject*.  

###  <a name="ViewDeployShareProp"></a> Affichage des propriétés d’un partage de déploiement avec Windows PowerShell  
 Vous pouvez afficher les propriétés des partages de déploiement MDT avec l’applet de commande [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) et le fournisseur Windows PowerShell MDTProvider. Vous pouvez également voir ces mêmes propriétés dans Deployment Workbench.  

 **Pour voir les propriétés d’un partage de déploiement avec les applets de commande Windows PowerShell de MDT**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les lecteurs Windows PowerShell du partage de déploiement MDT sont restaurés avec l’applet de commande **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Vérifiez que les déploiements MDT qui partagent les lecteurs Windows PowerShell sont restaurés correctement avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell qui sont fournis avec le fournisseur MDTProvider s’affiche.  

4.  Affichez les propriétés du partage de déploiement avec l’applet de commande [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx), comme indiqué dans l’exemple suivant :  

    ```  
    Get-ItemProperty "DS002:"  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3. L’applet de commande retourne les propriétés du partage de déploiement.  

###  <a name="ViewListDeployShare"></a> Affichage de la liste des partages de déploiement avec Windows PowerShell  
 Vous pouvez afficher la liste des partages de déploiement MDT avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796) et le fournisseur Windows PowerShell MDTProvider. Vous pouvez également voir la même liste de partages de déploiement dans Deployment Workbench.  

 **Pour afficher une liste des partages de déploiement avec les applets de commande Windows PowerShell de MDT**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Affichez la liste des déploiements MDT qui partagent les lecteurs Windows PowerShell, une pour chaque partage de déploiement, avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis par le fournisseur MDTProvider s’affiche, une pour chaque partage de déploiement.  

###  <a name="UpdateDeployShare"></a> Mise à jour d’un partage de déploiement avec Windows PowerShell  
 Vous pouvez mettre à jour les partages de déploiement avec l’applet de commande **Update-MDTDeploymentShare** et le fournisseur Windows PowerShell MDTProvider. La mise à jour d’un partage de déploiement crée les images de démarrage Windows PE (fichiers WIM et ISO [International Organization for Standardization]) nécessaires pour démarrer le déploiement avec installation LTI. Vous pouvez effectuer le même processus avec Deployment Workbench, comme décrit dans « Mettre à jour un partage de déploiement dans Deployment Workbench ».  

 **Pour mettre à jour un partage de déploiement avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Vérifiez que les déploiements MDT qui partagent les lecteurs Windows PowerShell sont restaurés correctement avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis avec le fournisseur MDTProvider s’affiche.  

4.  Mettez à jour le partage de déploiement avec l’applet de commande **Update-MDTDeploymentShare**, comme indiqué dans l’exemple suivant :  

    ```  
    Update-MDTDeploymentShare -Path "DS002:" -Force  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

    > [!NOTE]
    >  La mise à jour du partage de déploiement peut prendre un certain temps. La progression de l’applet de commande est indiquée en haut de la console Windows PowerShell.  

     L’applet de commande ne retourne rien si la mise à jour a réussi.  

###  <a name="UpdateLinkedDeployShare"></a> Mise à jour d’un partage de déploiement lié avec Windows PowerShell  
 Vous pouvez mettre à jour (répliquer) des partages de déploiement liés avec l’applet de commande **Update-MDTLinkedDS** et le fournisseur Windows PowerShell MDTProvider. La mise à jour d’un partage de déploiement lié réplique le contenu du partage de déploiement d’origine vers le partage de déploiement lié. Vous pouvez effectuer le même processus avec Deployment Workbench, comme décrit dans « Répliquer des partages de déploiement liés dans Deployment Workbench ».  

 **Pour mettre à jour un partage de déploiement lié avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Vérifiez que les déploiements MDT qui partagent les lecteurs Windows PowerShell sont restaurés correctement avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis avec le fournisseur MDTProvider s’affiche.  

4.  Mettez à jour le partage de déploiement avec l’applet de commande **Update-MDTDeploymentShare**, comme indiqué dans l’exemple suivant :  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

    > [!NOTE]
    >  La mise à jour du partage de déploiement lié peut prendre un certain temps. La progression de l’applet de commande est indiquée en haut de la console Windows PowerShell.  

     L’applet de commande ne retourne rien si la mise à jour a réussi.  

###  <a name="UpdateDeployMedia"></a> Mise à jour d’un support de déploiement avec Windows PowerShell  
 Vous pouvez mettre à jour (générer) des supports de déploiement avec l’applet de commande **Update-MDTMedia** et le fournisseur Windows PowerShell MDTProvider. La mise à jour d’un support de déploiement réplique le contenu du partage de déploiement d’origine vers le partage de déploiement lié, puis génère des fichiers .iso et .wim. Vous pouvez effectuer le même processus avec Deployment Workbench, comme décrit dans « Générer des images de support dans Deployment Workbench ».  

 Quand l’applet de commande **Update-MDTMedia** se termine, les fichiers suivants sont créés :  

-   Un fichier .iso dans le dossier *dossier_support* (où *dossier_support* est le nom du dossier spécifié pour le support)  

     La génération du fichier .iso est une option que vous configurez :  

    -   En cochant la case **Generate a Lite Touch bootable ISO imageGénérer une image ISO Lite Touch démarrable** (Générer une image ISO Lite Touch démarrable) dans l’onglet **General** (Général) de la boîte de dialogue **Properties** (Propriétés) du support (décochez cette case pour réduire le temps nécessaire à la génération du support, sauf si vous devez créer des DVD démarrables ou démarrer des machines virtuelles à partir du fichier .iso.)  

    -   En définissant la même propriété avec l’applet de commande [Set-ItemProperty](http://technet.microsoft.com/library/hh849844)  

-   Des fichiers WIM dans le dossier *dossier_support*\Content\Deploy\Boot (où *dossier_support* est le nom du dossier spécifié pour le support)  

 **Pour mettre à jour un partage de déploiement lié avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Vérifiez que les déploiements MDT qui partagent les lecteurs Windows PowerShell sont restaurés correctement avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis avec le fournisseur MDTProvider s’affiche.  

4.  Mettez à jour le partage de déploiement avec l’applet de commande **Update-MDTDeploymentShare**, comme indiqué dans l’exemple suivant :  

    ```  
    Update-MDTLinkedDS -Path "DS002:\Linked Deployment Shares\LINKED002"  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

    > [!NOTE]
    >  La mise à jour du partage de déploiement lié peut prendre un certain temps. La progression de l’applet de commande est indiquée en haut de la console Windows PowerShell.  

     L’applet de commande ne retourne rien si la mise à jour a réussi.  

###  <a name="ManageItemDeployShare"></a> Gestion des éléments d’un partage de déploiement avec Windows PowerShell  
 Un partage de déploiement contient des éléments qui sont utilisés pour effectuer des déploiements, comme des systèmes d’exploitation, des applications, des pilotes de périphérique, des packages de système d’exploitation et des séquences de tâches. Ces éléments peuvent gérés avec des applets de commande de Windows PowerShell et celles fournies avec MDT.  

 Pour plus d’informations sur la manipulation directe des éléments avec des applets de commande Windows PowerShell, consultez [Manipulation directe des éléments](http://technet.microsoft.com/library/dd315266.aspx). La structure de dossiers pour un partage de déploiement peut également être gérée avec Windows PowerShell. Pour plus d’informations, consultez [Gestion des dossiers des déploiements de partage avec Windows PowerShell](#ManageDeployShareFolder).  

####  <a name="ImportItemDeployShare"></a> Importer un élément dans un partage de déploiement  
 Vous pouvez importer chaque type d’élément, comme des systèmes d’exploitation, des applications ou des pilotes de périphériques, avec des applets de commande MDT. Pour chaque type d’élément, il existe une applet de commande MDT spécifique. Si vous voulez importer plusieurs éléments dans un partage de déploiement avec Windows PowerShell, consultez [Automatisation du remplissage d’un partage de déploiement](#AutomatePopulateDeployShare).  

 Le tableau suivant répertorie les applets de commande Windows PowerShell de MDT utilisées pour importer des éléments dans un partage de déploiement et donne une brève description de chacune d’elles. Des exemples d’utilisation de chaque applet de commande sont fournis dans la section correspondante.  

 |**Applet de commande** | **Description** |  
 |-|-|  
 |**Import-MDTApplication** |Importe une application dans un partage de déploiement|  
 |**Import-MDTDriver** |Importe un ou plusieurs pilotes de périphérique dans un partage de déploiement|  
 |**Import-MDTOperatingSystem** |Importe un ou plusieurs systèmes d’exploitation dans un partage de déploiement|  
 |**Import-MDTPackage** |Importe un ou plusieurs packages de système d’exploitation dans un partage de déploiement|  
 |**Import-MDTTaskSequence** |Importe une séquence de tâches dans un partage de déploiement|  

####  <a name="ViewPropertyDeployShare"></a> Afficher les propriétés d’un élément dans un partage de déploiement  
 Chaque élément d’un partage de déploiement a un ensemble différent de propriétés. Vous pouvez afficher les propriétés d’un élément d’un partage de déploiement avec l’applet de commande [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx). L’applet de commande [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx) utilise le fournisseur MDTProvider pour afficher les propriétés d’un élément spécifique, tout comme vous pouvez voir les propriétés dans Deployment Workbench.  

 Si vous voulez voir les propriétés de plusieurs éléments d’un partage de déploiement avec Windows PowerShell, consultez [Automatisation du remplissage d’un partage de déploiement](#AutomatePopulateDeployShare).  

 **Pour afficher les propriétés d’un élément d’un partage de déploiement avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Vérifiez que les déploiements MDT qui partagent les lecteurs Windows PowerShell sont restaurés correctement avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme indiqué dans l’exemple suivant :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis avec le fournisseur MDTProvider s’affiche.  

4.  Retournez une liste des éléments pour le type d’élément dont vous voulez afficher les propriétés avec l’applet de commande [Get-Item](http://technet.microsoft.com/library/hh849788), comme indiqué dans l’exemple suivant :  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     Dans l’exemple précédent, une liste de tous les systèmes d’exploitation du partage de déploiement est affichée. La sortie est dirigée vers l’applet de commande **Format-List**, ce qui permet d’afficher les noms longs des systèmes d’exploitation. Pour plus d’informations sur l’utilisation de l’applet de commande **Format-List**, consultez [Utilisation de l’applet de commande Format-List](http://technet.microsoft.com/library/ee176830.aspx). Vous pouvez utiliser le même processus pour retourner la liste d’autres types d’éléments, comme les pilotes de périphérique ou les applications.  

    > [!TIP]
    >  Vous pouvez aussi utiliser la commande **dir** pour afficher la liste des systèmes d’exploitation, au lieu de l’applet de commande [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Affichez les propriétés d’un des éléments répertoriés à l’étape précédente avec l’applet de commande [Get-ItemProperty](http://technet.microsoft.com/library/hh849851.aspx), comme indiqué dans l’exemple suivant :  

    ```  
    Get-ItemProperty -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     Dans cet exemple, la valeur du paramètre *Path* est le chemin complet Windows PowerShell vers l’élément, incluant le nom de fichier retourné à l’étape précédente. Vous pouvez utiliser le même processus pour afficher les propriétés d’autres types d’éléments, comme les pilotes de périphérique ou les applications.  

####  <a name="RemoveItemDeployShare"></a> Supprimer un élément d’un partage de déploiement  
 Vous pouvez supprimer un élément d’un partage de déploiement avec l’applet de commande [Remove-Item](http://technet.microsoft.com/library/hh849765). L’applet de commande [Remove-Item](http://technet.microsoft.com/library/hh849765) utilise le fournisseur MDTProvider pour supprimer un élément spécifique, tout comme vous pouvez supprimer un élément dans Deployment Workbench. Si vous voulez supprimer plusieurs éléments d’un partage de déploiement avec Windows PowerShell, consultez [Automatisation du remplissage d’un partage de déploiement](#AutomatePopulateDeployShare).  

> [!NOTE]
>  La suppression d’un élément utilisé par une séquence de tâches provoque l’échec de cette séquence. Vérifiez qu’un élément n’est pas référencé par d’autres éléments du partage de déploiement avant de supprimer cet élément. Une fois qu’un élément est supprimé, il ne peut pas être récupéré.  

 **Pour supprimer un élément d’un partage de déploiement avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec l’applet de commande **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant.  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que l’applet de commande ne peut pas restaurer le lecteur.  

3.  Vérifiez que les déploiements MDT qui partagent les lecteurs Windows PowerShell sont restaurés correctement avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme indiqué dans l’exemple suivant :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis avec le fournisseur MDTProvider s’affiche.  

4.  Retournez une liste des éléments pour le type d’élément dont vous voulez afficher les propriétés avec l’applet de commande [Get-Item](http://technet.microsoft.com/library/hh849788), comme indiqué dans l’exemple suivant :  

    ```  
    Get-Item "DS001:\Operating Systems\*" | Format-List  
    ```  

     Dans l’exemple précédent, une liste de tous les systèmes d’exploitation du partage de déploiement est affichée. La sortie est dirigée vers l’applet de commande **Format-List**, ce qui permet d’afficher les noms longs des systèmes d’exploitation. Pour plus d’informations sur l’utilisation de l’applet de commande **Format-List**, consultez [Utilisation de l’applet de commande Format-List](http://technet.microsoft.com/library/ee176830.aspx). Vous pouvez utiliser le même processus pour retourner la liste d’autres types d’éléments, comme les pilotes de périphérique ou les applications.  

    > [!TIP]
    >  Vous pouvez aussi utiliser la commande **dir** pour afficher la liste des systèmes d’exploitation, au lieu de l’applet de commande [Get-Item](http://technet.microsoft.com/library/hh849788).  

5.  Supprimez un des éléments répertoriés à l’étape précédente avec l’applet de commande [Remove-Item](http://technet.microsoft.com/library/hh849765), comme indiqué dans l’exemple suivant :  

    ```  
    Remove-Item -Path "DS002:\Operating Systems\Windows 8 in Windows 8 x64 install.wim"  
    ```  

     Dans cet exemple, la valeur du paramètre *Path* est le chemin complet Windows PowerShell vers l’élément, incluant le nom de fichier retourné à l’étape précédente.  

     Vous pouvez utiliser le même processus pour supprimer d’autres types d’éléments, comme les pilotes de périphérique ou les applications.  

    > [!NOTE]
    >  La suppression d’un élément utilisé par une séquence de tâches provoque l’échec de cette séquence. Vérifiez qu’un élément n’est pas référencé par d’autres éléments du partage de déploiement avant de supprimer cet élément.  

###  <a name="AutomatePopulateDeployShare"></a> Automatisation du remplissage d’un partage de déploiement  
 Les applets de commande Windows PowerShell de MDT vous permettent de gérer des éléments individuels. Cependant, avec certaines des fonctionnalités de script de Windows PowerShell, les applets de commande peuvent être utilisées pour automatiser le remplissage d’un partage de déploiement.  

 Par exemple, une organisation a besoin de déployer plusieurs partages de déploiement pour les différentes divisions, ou elle peut fournir des services de déploiement de systèmes d’exploitation pour d’autres organisations. Dans ces deux exemples, les organisations doivent avoir la possibilité de créer et de remplir des partages de déploiement configurés de façon cohérente.  

 Une méthode pour gérer plusieurs éléments consisterait à utiliser un fichier de valeurs séparées par des virgules (CSV) contenant une liste de tous les éléments que vous voulez gérer dans un déploiement de partagent avec l’applet de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx).  

 Voici un extrait d’un script Windows PowerShell pour importer une liste d’applications, basé sur les informations contenues dans un fichier .csv, avec les applets de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), [ForEach-Object](http://technet.microsoft.com/library/hh849731) et **Import-MDTApplication** :  

```  
$List=Import-CSV "C:\MDT\Import-MDT-Apps.csv"  
ForEach-Object ($App in $List) {  
Import-MDTApplication –path $App.ApplicationFolder -enable "True" –Name $App.DescriptiveName –ShortName $App.Shortname –Version $App.Version –Publisher $App.Publisher –Language $App.Language –CommandLine $App.CommandLine –WorkingDirectory $App.WorkingDirectory –ApplicationSourcePath $App.SourceFolder –DestinationFolder $App.DestinationFolder –Verbose  
}  
```  

 Dans cet exemple, le fichier C:\MDT\Import-MDT-Apps.csv contient un champ pour chaque variable nécessaire pour importer une application. Pour plus d’informations sur la création d’un fichier .csv à utiliser avec l’applet de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), consultez [Utilisation de l’applet de commande Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

 Vous pouvez utiliser cette même méthode pour importer les systèmes d’exploitation, les pilotes de périphérique et les autres éléments d’un partage de déploiement en effectuant les étapes suivantes :  

1.  Créez un fichier .csv pour chaque type d’élément du partage de déploiement que vous voulez remplir.  

2.  Pour plus d’informations sur la création d’un fichier .csv à utiliser avec l’applet de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), consultez [Utilisation de l’applet de commande Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

3.  Créez un fichier de script Windows PowerShell à utiliser pour automatiser le remplissage du partage de déploiement.  

     Pour plus d’informations sur la création d’un script Windows PowerShell, consultez [Écriture de scripts avec Windows PowerShell](http://technet.microsoft.com/scriptcenter/powershell.aspx).  

4.  Créez les structures de dossiers prérequises nécessaires dans le partage de déploiement avant d’importer les éléments du partage de déploiement.  

     Pour plus d’informations, consultez [Gestion des dossiers des déploiements de partage avec Windows PowerShell](#ManageDeployShareFolder).  

5.  Ajoutez une ligne avec l’applet de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) pour un des fichiers .csv créés à l’étape 1.  

     Pour plus d’informations sur l’applet de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx), consultez [Utilisation de l’applet de commande Import-Csv](http://technet.microsoft.com/library/ee176874.aspx).  

6.  Créez une boucle avec l’applet de commande [ForEach-Object](http://technet.microsoft.com/library/hh849731) qui traite chaque élément du fichier .csv référencé dans l’applet de commande [Import-CSV](http://technet.microsoft.com/library/dd347665.aspx) à l’étape précédente.  

     Pour plus d’informations sur l’applet de commande [ForEach-Object](http://technet.microsoft.com/library/hh849731), consultez [Utilisation de l’applet de commande ForEach-Object](http://technet.microsoft.com/library/ee176828).  

7.  Ajoutez l’applet de commande MDT correspondante pour importer les éléments du partage de déploiement dans la boucle de l’applet de commande [ForEach-Object](http://technet.microsoft.com/library/hh849731) créée à l’étape précédente.  

     Pour plus d’informations sur les applets de commande MDT utilisées pour importer des éléments dans un partage de déploiement, consultez [Importer un élément dans un partage de déploiement](#ImportItemDeployShare).  

###  <a name="ManageDeployShareFolder"></a> Gestion des dossiers des déploiements de partage avec Windows PowerShell  
 Vous pouvez gérer les dossiers d’un partage de déploiement avec des outils en ligne de commande, comme la commande **mkdir**, ou avec des applets de commande Windows PowerShell, comme [New-Item](http://technet.microsoft.com/library/hh849795) et le fournisseur Windows PowerShell MDTProvider. Vous pouvez également voir et gérer la même structure de dossiers de partages de déploiement dans Deployment Workbench. Pour plus d’informations sur la manipulation directe des éléments avec des applets de commande Windows PowerShell, consultez [Manipulation directe des éléments](http://technet.microsoft.com/library/dd315266.aspx).  

#### <a name="create-a-folder-in-a-deployment-share-using-windows-powershell"></a>Créer un dossier dans un partage de déploiement avec Windows PowerShell  
 **Pour créer un dossier dans un partage de déploiement avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que la cmdlet ne peut pas restaurer le lecteur.  

3.  Affichez la liste des déploiements MDT qui partagent des lecteurs Windows PowerShell, une pour chaque partage de déploiement, avec l’applet de commande [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis par le fournisseur MDTProvider s’affiche, une pour chaque partage de déploiement.  

4.  Créez un dossier nommé *Windows_8* dans le dossier Operating Systems (Systèmes d’exploitation) d’un partage de déploiement avec la commande **mkdir**, comme indiqué dans l’exemple suivant :  

    ```  
    mkdir "DS002:\Operating Systems\Windows_8"  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

5.  Tapez la commande suivante pour vérifier que le dossier a été créé correctement :  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Le dossier Windows_8 et tous les autres dossiers existants du dossier Operating Systems (Systèmes d’exploitation) s’affichent.  

6.  Créez un dossier nommé *Windows_7* dans le dossier Operating Systems (Systèmes d’exploitation) d’un partage de déploiement à l’aide de la cmdlet [New-Item](http://technet.microsoft.com/library/hh849795), comme indiqué dans l’exemple suivant et dans la rubrique [Utilisation de l’applet de commande New-Item](http://technet.microsoft.com/library/ee176914.aspx) :  

    ```  
    New-Item "DS002:\Operating Systems\Windows_7" -Type directory  
    ```  

     La cmdlet indique que la création du dossier a été correctement effectuée.  

7.  Tapez la commande suivante pour vérifier que le dossier a été créé correctement :  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Le dossier Windows_7 et tous les autres dossiers existants du dossier Operating Systems (Systèmes d’exploitation) s’affichent.  

#### <a name="delete-a-folder-in-a-deployment-share-using-windows-powershell"></a>Supprimer un dossier dans un partage de déploiement avec Windows PowerShell  
 **Pour supprimer un dossier dans un partage de déploiement avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT, comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que la cmdlet ne peut pas restaurer le lecteur.  

3.  Affichez la liste des déploiements MDT qui partagent des lecteurs Windows PowerShell, un pour chaque partage de déploiement, avec la cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis par MDTProvider s’affiche, un pour chaque partage de déploiement.  

4.  Supprimez (enlevez) un dossier nommé *Windows_8* dans le dossier Operating Systems (Systèmes d’exploitation) d’un partage de déploiement à l’aide de la commande **mkdir**, comme indiqué dans l’exemple suivant :  

    ```  
    rmdir "DS002:\Operating Systems\Windows_8"  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

5.  Tapez la commande suivante pour vérifier que le dossier a été supprimé correctement :  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Le dossier Windows_8 n’est plus affiché dans la liste des dossiers du dossier Operating Systems (Systèmes d’exploitation)  

6.  Supprimez (enlevez) un dossier nommé *Windows_7* dans le dossier Operating Systems (Systèmes d’exploitation) d’un partage de déploiement à l’aide de la cmdlet [Remove-Item](http://technet.microsoft.com/library/hh849765), comme indiqué dans l’exemple suivant :  

    ```  
    Remove-Item "DS002:\Operating Systems\Windows_7"  
    ```  

     La cmdlet indique que la suppression du dossier a été correctement effectuée.  

7.  Tapez la commande suivante pour vérifier que le dossier a été créé correctement :  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Le dossier Windows_7 n’est plus affiché dans la liste des dossiers du dossier Operating Systems (Systèmes d’exploitation).  

#### <a name="rename-a-folder-in-a-deployment-share-using-windows-powershell"></a>Renommer un dossier dans un partage de déploiement avec Windows PowerShell  
 **Pour renommer un dossier dans un partage de déploiement avec Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT, comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que la cmdlet ne peut pas restaurer le lecteur.  

3.  Affichez la liste des déploiements MDT qui partagent des lecteurs Windows PowerShell, un pour chaque partage de déploiement, avec la cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme suit :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis par MDTProvider s’affiche, un pour chaque partage de déploiement.  

4.  Renommez un dossier nommé *Windows_8* en *Win_8* dans le dossier Operating Systems (Systèmes d’exploitation) d’un partage de déploiement à l’aide de la commande **ren**, comme indiqué dans l’exemple suivant :  

    ```  
    ren "DS002:\Operating Systems\Windows_8" "Win_8"  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

5.  Tapez la commande suivante pour vérifier que le dossier a été supprimé correctement :  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Le dossier Windows_8 est renommé en *Win_8*.  

6.  Renommez un dossier nommé *Windows_7* en *Win-7* dans le dossier Operating Systems (Systèmes d’exploitation) d’un partage de déploiement à l’aide de la cmdlet [Rename-Item](http://technet.microsoft.com/library/hh849763), comme indiqué dans l’exemple suivant :  

    ```  
    Rename-Item "DS002:\Operating Systems\Windows_7" "Win_7"  
    ```  

     La cmdlet indique que le renommage du dossier a été correctement effectué.  

7.  Tapez la commande suivante pour vérifier que le dossier a été créé correctement :  

    ```  
    dir "DS002:\Operating Systems"  
    ```  

     Le dossier Windows_7 est renommé en *Win_7*.  

## <a name="automating-the-application-of-operating-system-service-packs-in-deployment-shares"></a>Automatisation de l’application des Service Packs de système d’exploitation dans les partages de déploiement  
 Les Service Packs de système d’exploitation font partie intégrante du cycle de vie des logiciels. Les systèmes d’exploitation existants des partages de déploiement doivent être mis à jour avec ces Service Packs pour garantir que les ordinateurs récemment déployés ou actualisés sont conformes aux dernières recommandations et aux derniers paramètres de configuration relatifs à la sécurité.  

 Quand une organisation a plusieurs partages de déploiement avec plusieurs systèmes d’exploitation dans chacun d’eux, le processus de mise à jour manuelle des systèmes d’exploitation dans chaque partage de déploiement à l’aide des Service Packs appropriés peut prendre du temps. L’automation de l’application des Service Packs de système d’exploitation dans les partages de déploiement incluent les méthodes suivantes :  

-   Copie du contenu source mis à jour contenant déjà le Service Pack (par exemple un support Windows 7 avec SP1) dans le dossier du partage de déploiement où réside le système d’exploitation existant, comme décrit dans [Automatisation de l’application des Service Packs de système d’exploitation à partir de supports sources mis à jour](#AutomateAppFromUSM)  

-   Application du Service Pack à un ordinateur de référence, puis capture d’une image mise à jour à partir d’un ordinateur de référence, comme décrit dans [Automatisation de l’application des Service Packs de système d’exploitation à l’aide d’un ordinateur de référence et de Windows PowerShell](#AutomateAppUsingRef)  

###  <a name="AutomateAppFromUSM"></a> Automatisation de l’application des Service Packs de système d’exploitation à partir de supports sources mis à jour  
 Vous pouvez automatiser le processus de mise à jour des Service Packs de système d’exploitation à l’aide de Windows PowerShell quand vous disposez d’un support source qui inclue le Service Pack, par exemple un DVD auquel Windows 7 SP1 est déjà intégré.  

 Avec cette méthode, les fichiers du support source du système d’exploitation incluant le Service Pack sont copiés à la place des fichiers existants du système d’exploitation sans Service Pack dans le partage de déploiement à l’aide de Windows PowerShell.  

 **Pour automatiser l’application des Service Packs de système d’exploitation à partir de supports sources mis à jour à l’aide de Windows PowerShell**  

1.  Chargez le composant logiciel enfichable Windows PowerShell de MDT, comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

2.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que la cmdlet ne peut pas restaurer le lecteur.  

3.  Affichez la liste des déploiements MDT qui partagent des lecteurs Windows PowerShell, un pour chaque partage de déploiement, à l’aide de la cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme indiqué dans l’exemple suivant :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis par MDTProvider s’affiche, un pour chaque partage de déploiement.  

4.  Supprimez le dossier correspondant au système d’exploitation existant dans le partage de déploiement, à l’aide des cmdlets [Get-ChildItem](http://technet.microsoft.com/library/hh849800) et [Remove-Item](http://technet.microsoft.com/library/hh849765), comme indiqué dans l’exemple suivant :  

    ```  
    Get-ChildItem “DS002:\Operating Systems\Windows 7” –recurse | Remove-Item –recurse –force  
    ```  

     Dans cet exemple, *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

5.  Copiez le contenu des fichiers sources du système d’exploitation intégrant le Service Pack à l’aide de la cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), comme indiqué dans l’exemple suivant :  

    ```  
    Copy-Item "E:\*" -Destination "DS002:\Operating Systems\Windows 7"-Recurse -Force  
    ```  

     Dans cet exemple, les fichiers sources du système d’exploitation sont sur le lecteur E et *DS002:* est le nom d’un lecteur Windows PowerShell retourné à l’étape 3.  

6.  Mettez à jour les supports de déploiement MDT en fonction du partage de déploiement à l’aide de la cmdlet **Update-MDTMedia**.  

 Pour plus d’informations sur la mise à jour du support de déploiement MDT en fonction du partage de déploiement à l’aide de la cmdlet **Update-MDTMedia**, consultez [Mise à jour d’un support de déploiement avec Windows PowerShell](#UpdateDeployMedia).  

###  <a name="AutomateAppUsingRef"></a> Automatisation de l’application des Service Packs de système d’exploitation à l’aide d’un ordinateur de référence et de Windows PowerShell  
 Vous pouvez automatiser le processus de mise à jour des Service Packs de système d’exploitation à l’aide de Windows PowerShell quand seul le Service Pack n’est pas encore intégré au système d’exploitation, par exemple SP1 pour Windows 7 qui n’est pas encore intégré à une image Windows 7.  

 Pour cette méthode, déployez le système d’exploitation sans le Service Pack sur un ordinateur de référence. Appliquez ensuite le Service Pack à l’ordinateur de référence. Capturez ensuite une image du système d’exploitation de l’ordinateur de référence. Pour finir, copiez le fichier .wim capturé sur le fichier Install.wim du système d’exploitation dans le partage de déploiement à l’aide de Windows PowerShell.  

 **Pour automatiser l’application des Service Packs de système d’exploitation à partir de supports sources mis à jour à l’aide de Windows PowerShell**  

1.  Déployez le système d’exploitation cible sur un ordinateur de référence.  

     Pour plus d’informations sur le déploiement d’un ordinateur de référence, consultez les ressources suivantes dans le document MDT, *Utilisation de Microsoft Deployment Toolkit* :  

    -   « Préparation du déploiement LTI sur l’ordinateur de référence »  

    -   "Déploiement et capture d’une image de l’ordinateur de référence dans LTI"  

2.  Installez le Service Pack souhaité sur l’ordinateur de référence.  

     Pour plus d’informations sur l’installation du Service Pack, consultez la documentation qui l’accompagne.  

3.  Capturez une image de l’ordinateur de référence en créant et en déployant une séquence de tâches basée sur le modèle de séquence de tâches **Sysprep and Capture (Sysprep et capture)**.  

     Pour plus d’informations sur la création d’une séquence de tâches basée sur le modèle de séquence de tâches **Sysprep and Capture (Sysprep et capture)**, consultez « Créer une séquence de tâches dans Deployment Workbench ».  

4.  Chargez le composant logiciel enfichable Windows PowerShell de MDT, comme décrit dans [Chargement du composant logiciel enfichable Windows PowerShell de MDT](#LoadMDTSnapIn).  

5.  Vérifiez que les déploiements MDT qui partagent des lecteurs Windows PowerShell sont restaurés avec la cmdlet **Restore-MDTPersistentDrive**, comme indiqué dans l’exemple suivant :  

    ```  
    Restore-MDTPersistentDrive -Verbose  
    ```  

    > [!NOTE]
    >  Si les déploiements MDT qui partagent des lecteurs Windows PowerShell sont déjà restaurés, vous recevez un message d’avertissement indiquant que la cmdlet ne peut pas restaurer le lecteur.  

6.  Affichez la liste des déploiements MDT qui partagent des lecteurs Windows PowerShell, un pour chaque partage de déploiement, à l’aide de la cmdlet [Get-PSDrive](http://technet.microsoft.com/library/hh849796), comme indiqué dans l’exemple suivant :  

    ```  
    Get-PSDrive -PSProvider Microsoft.BDD.PSSnapIn\MDTProvider  
    ```  

     La liste des lecteurs Windows PowerShell fournis par MDTProvider s’affiche, un pour chaque partage de déploiement.  

7.  Copiez le fichier .wim capturé à l’étape 3 sur le fichier Install.wim du système d’exploitation dans le partage de déploiement, à l’aide de la cmdlet [Copy-Item](http://technet.microsoft.com/library/hh849793), comme indiqué dans l’exemple suivant :  

    ```  
    Copy-Item "DS002:\Captures\Win7SP1.wim" -Destination "DS002:\Operating Systems\Windows 7\sources\Install.wim" Force  
    ```  

     Dans cet exemple, le fichier image de système d’exploitation capturé (Win7SP1.wim) présent dans le dossier Captures du partage DS002: correspond au nom d’un lecteur Windows PowerShell retourné à l’étape 6. Le système d’exploitation Windows 7 existant est stocké dans le dossier nommé *Windows 7*.  

8.  Mettez à jour les supports de déploiement MDT en fonction du partage de déploiement à l’aide de la cmdlet **Update-MDTMedia**.  

     Pour plus d’informations sur la mise à jour du support de déploiement MDT en fonction du partage de déploiement à l’aide de la cmdlet **Update-MDTMedia**, consultez [Mise à jour d’un support de déploiement avec Windows PowerShell](#UpdateDeployMedia).  

## <a name="customizing-deployment-based-on-chassis-type"></a>Personnalisation du déploiement en fonction du type de châssis  
 Vous pouvez personnaliser le déploiement en fonction du type de châssis de l’ordinateur. Les scripts créent des variables locales qui peuvent être traitées dans le fichier CustomSettings.ini. Les variables locales `IsLaptop`, `IsDesktop` et `IsServer` indiquent si l’ordinateur est un ordinateur portable, un ordinateur de bureau ou un serveur, respectivement.  

> [!NOTE]
>  Dans les versions antérieures de Deployment Workbench, l’indicateur `IsServer` signifiait que le système d’exploitation existant était un système d’exploitation serveur (par exemple Windows Server 2003 Enterprise Edition). Cet indicateur a été renommé en `IsServerOS`.  

 **Pour implémenter des variables locales dans le fichier CustomSettings.ini**  

1.  Dans la section `[Settings]`, à la ligne`Priority`, ajoutez une section personnalisée pour personnaliser le déploiement en fonction du type de châssis (`ByChassisType` dans l’exemple suivant, où *Chassis* représente le type d’ordinateur).  

2.  Créez la section personnalisée qui correspond à la section personnalisée définie à l’étape 1 (`ByChassisType` dans l’exemple suivant, où *Chassis* représente le type d’ordinateur).  

3.  Définissez une sous-section pour chaque type de châssis à détecter (`Subsection=Laptop-%IsLaptop%, Subsection=Desktop-%IsDesktop%, Subsection=Server-%IsServer%` dans l’exemple suivant).  

4.  Créez une sous-section pour chaque état `True` et `False` de chaque sous-section définie à l’étape 3 (par exemple `[Laptop-True], [Laptop-False], [Desktop-True], [Desktop-False]` dans l’exemple suivant).  

5.  Sous chaque sous-section `True` et `False`, ajoutez les paramètres appropriés en fonction du type de châssis.  

 **Liste 1. Exemple de personnalisation du déploiement en fonction du type de châssis dans le fichier CustomSettings.ini**  

```  
[Settings]  

Priority=...,ByLaptopType,ByDesktopType,ByServerType  

[ByLaptopType]  
Subsection=Laptop-%IsLaptop%  

[ByDesktopType]  
Subsection=Desktop-%IsDesktop%  

[ByServerType]  
Subsection=Server-%IsServer%  
.  
.  
.  

[Laptop-True]  
.  
.  
.  

[Laptop-False]  
.  
.  
.  

[Desktop-True]  
.  
.  
.  

[Desktop-False]  
.  
.  
.  

[Server-True]  
.  
.  
.  

[Server-False]  
.  
.  
.  
```  

## <a name="deploying-applications-based-on-earlier-application-versions"></a>Déploiement d’applications en fonction des versions antérieures des applications  
 Bien souvent, quand vous installez un système d’exploitation sur un ordinateur existant, vous réinstallez les mêmes applications sur cet ordinateur. Pour ce faire, utilisez des scripts MDT (en particulier, ZTIGather.wsf) afin d’interroger deux sources d’informations distinctes :  

-   **Fonctionnalité d’inventaire logiciel Configuration Manager.** Contient un enregistrement pour chaque package d’application (listé dans Programmes et fonctionnalités sur Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2) installé la dernière fois que Configuration Manager a inventorié l’ordinateur.  

-   **Table de mappage.** Décrit le package et le programme à installer pour chaque enregistrement (car les enregistrements listés dans Programmes et fonctionnalités ou Ajout/Suppression de programmes n’identifient pas précisément le package qui a installé l’application, ce qui rend impossible la sélection automatique du package uniquement en fonction de l’inventaire).  

 **Pour effectuer une installation dynamique d’application en fonction de l’ordinateur**  

1.  Utilisez la table de la base de données MDT pour connecter des packages spécifiques aux applications listées dans le système d’exploitation cible.  

2.  Remplissez la table avec des données qui associent le package approprié à l’application listée dans Programmes et fonctionnalités ou Ajout/Suppression de programmes.

     **Requête SQL pour remplir la table**  

    ```  
    use [MDTDB]  
    go  
    INSERT INTO [PackageMapping] (ARPName, Packages) VALUES('Office12.0', 'XXX0000F:Install Office 2010 Professional Plus')  
    go  
    ```  

     La ligne insérée connecte les ordinateurs ayant l’entrée `Office12.0` au package Microsoft Office Professionnel Plus 2010.  

     Cela signifie que Microsoft Office Professionnel Plus 2010 va être installé sur les ordinateurs qui exécutent la version 2007 de Microsoft Office System (Office 12.0). Ajoutez des entrées similaires pour tous les autres packages. Les éléments pour lesquels il n’existe aucune entrée sont ignorés (aucun package n’est installé).  

3.  Créez une procédure stockée pour simplifier la jonction des informations de la nouvelle table avec les données d’inventaire.  

    ```  
    use [MDTDB]  
    go  

    if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[RetrievePackages]') and OBJECTPROPERTY(id, N'IsProcedure') = 1)  
    drop procedure [dbo].[RetrievePackages]  
    go  

    CREATE PROCEDURE [dbo].[RetrievePackages]  
    @MacAddress CHAR(17)  
    AS  

    SET NOCOUNT ON  

    /* Select and return all the appropriate records based on current inventory */  
    SELECT * FROM PackageMapping  
    WHERE ARPName IN  
    (  
      SELECT ProdID0 FROM CM_DB.dbo.v_GS_ADD_REMOVE_PROGRAMS a, CM_DB.dbo.v_GS_NETWORK_ADAPTER n  
      WHERE a.ResourceID = n.ResourceID AND  
      MACAddress0 = @MacAddress  
    )  
    go  
    ```  

     L’utilisation de la procédure stockée de l’exemple précédent suppose que la base de données du site principal/central de Configuration Manager réside sur l’ordinateur où SQL Server s’exécute en tant que base de données MDT. Si la base de données du site principal/central réside sur un autre ordinateur, vous devez apporter les modifications appropriées à la procédure stockée. En outre, vous devez mettre à jour le nom de la base de données (`CM_DB`). Octroyez également à des comptes supplémentaires un accès en lecture à la vue **v_GS_ADD_REMOVE_PROGRAMS** dans la base de données Configuration Manager.  

4.  Configurez le fichier CustomSettings.ini pour interroger cette table de base de données en spécifiant le nom d’une section (`[DynamicPackages]` dans la liste **Priority**) qui pointe vers les informations de base de données.  

    ```  
    [Settings]  
    …  
    Priority=MacAddress, DefaultGateway, DynamicPackages, Default  
    …  
    ```  

5.  Créez une section `[DynamicPackages]` pour spécifier le nom d’une section de base de données.  

    ```  
    [DynamicPackages]  
    SQLDefault=DB_DynamicPackages  
    ```  

6.  Créez une section de base de données pour spécifier les informations de base de données et les détails de la requête.  

    ```  
    [DB_DynamicPackages]  
    SQLServer=SERVER1  
    Database=MDTDB  
    StoredProcedure=RetrievePackages  
    Parameters=MacAddress  
    SQLShare=Logs  
    Instance=SQLEnterprise2005  
    Port=1433  
    Netlib=DBNMPNTW  
    ```  

     Dans l’exemple précédent, la base de données MDT nommée *MDTDB* sur l’ordinateur exécutant l’instance SQL Server nommée *SERVER1* va être interrogée. La base de données contient une procédure stockée nommée `RetrievePackages` (créée à l’étape 3).  

 Quand ZTIGather.wsf s’exécute, l’instruction SQL (Structured Query Language) `SELECT` est générée automatiquement, et la valeur de la clé personnalisée **MakeModelQuery** est passée en tant que paramètre à la requête :  

 ```  
 EXECUTE RetrievePackages ?  
 ```  

 La valeur réelle de la clé personnalisée **MACAddress** est remplacée par le « ? » correspondant.  Cette requête retourne un jeu d’enregistrements avec les lignes entrées à l’étape 2.  

 Il est impossible de passer un nombre variable d’arguments à une procédure stockée. Ainsi, quand un ordinateur a plusieurs adresses MAC, il est impossible de les passer toutes à la procédure stockée. En guide de solution, remplacez la procédure stockée par une vue qui permet d’interroger la vue avec une instruction `SELECT` et une clause `IN` pour passer toutes les valeurs d’adresses MAC.  

 D’après le scénario présenté ici, si la valeur `Office12.0` de l’ordinateur actuel est insérée dans la table (étape 2), une seule ligne est retournée (`XXX0000F:Install Office 2010 Professional Plus`). Cela indique que le package XXX0000F:Install Office 2010 Professional Plus (Installation d’Office Professionnel Plus 2010) est installé par le processus ZTI durant la phase de restauration d’état.  

## <a name="fully-automated-lti-deployment-scenario"></a>Scénario de déploiement LTI entièrement automatisé  
 L’objectif principal de LTI est d’automatiser le processus de déploiement autant que possible. Bien que ZTI assure une automatisation complète du déploiement à l’aide des scripts MDT et des Services de déploiement Windows, LTI est conçu pour fonctionner avec moins d’exigences spécifiques à l’infrastructure.  

 Vous pouvez automatiser l’Assistant Déploiement Windows utilisé dans le processus de déploiement LTI pour réduire (ou éliminer) les pages affichées de l’Assistant. Vous pouvez complètement ignorer l’Assistant Déploiement Windows en spécifiant la propriété **SkipWizard** dans CustomSettings.ini. Pour ignorer certaines pages de l’Assistant, utilisez les propriétés suivantes :  

-   **SkipAdminPassword**  

-   **SkipApplications**  

-   **SkipBDDWelcome**  

-   **SkipBitLocker**  

-   **SkipBitLockerDetails**  

-   **SkipTaskSequence**  

-   **SkipCapture**  

-   **SkipComputerBackup**  

-   **SkipComputerName**  

-   **SkipDomainMembership**  

-   **SkipFinalSummary**  

-   **SkipLocaleSelection**  

-   **SkipPackageDisplay**  

-   **SkipProductKey**  

-   **SkipSummary**  

-   **SkipTimeZone**  

-   **SkipUserData**  

Pour plus d’informations sur chacune de ces propriétés, consultez la propriété correspondante dans le document MDT *Toolkit Reference* (Référence du kit de ressources).  

Pour chaque page ignorée de l’Assistant, indiquez les valeurs des propriétés correspondantes généralement collectées via la page de l’Assistant dans les fichiers CustomSettings.ini et BootStrap.ini. Pour plus d’informations sur les propriétés qui doivent être configurées dans ces fichiers, consultez la section décrivant la spécification de propriétés pour les pages ignorées de l’Assistant Déploiement, dans le document MDT *Toolkit Reference* (Référence du kit de ressources).  

## <a name="fully-automated-lti-deployment-for-a-refresh-computer-scenario"></a>Déploiement LTI entièrement automatisé pour un scénario d’actualisation de l’ordinateur  
 L’exemple suivant montre comment utiliser un fichier CustomSettings.ini dans un scénario d’actualisation d’un ordinateur pour ignorer toutes les pages de l’Assistant Déploiement Windows. Dans cet exemple, les propriétés à indiquer quand vous ignorez la page de l’Assistant se trouvent juste sous la propriété qui permet d’ignorer la page de l’Assistant.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  
SkipCapture=YES  
SkipAdminPassword=YES  
SkipProductKey=YES  

DeploymentType=REFRESH  

SkipDomainMembership=YES  
JoinDomain=DomainName  
DomainAdmin=Administrator  
DomainAdminDomain=DomainName  
DomainAdminPassword=a_secure_password  

SkipUserData=yes  
UserDataLocation=AUTO  
UDShare=\\Servername\Sharename\Directory  
UDDir=%ComputerName%  

SkipComputerBackup=YES  
ComputerBackuplocation=AUTO  
BackupShare=\\Servername\Backupsharename  
BackupDir=%ComputerName%  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%ComputerName%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  
UserID=Administrator  
UserDomain=DomainName  
UserPassword=P@ssw0rd  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=DomainName\Username  
```  

## <a name="fully-automated-lti-deployment-for-a-new-computer-scenario"></a>Déploiement LTI entièrement automatisé pour un scénario d’installation d’un nouvel ordinateur  
 L’exemple suivant montre comment utiliser un fichier CustomSettings.ini dans un scénario d’installation d’un nouvel ordinateur pour ignorer toutes les pages de l’Assistant Déploiement Windows. Dans cet exemple, les propriétés à indiquer quand vous ignorez la page de l’Assistant se trouvent juste sous la propriété qui permet d’ignorer la page de l’Assistant.  

```  
[Settings]  
Priority=Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac /lae  

SkipCapture=YES  
ComputerBackupLocation=\\WDG-MDT-01\Backup$\  
BackupFile=MyCustomImage.wim  

SkipAdminPassword=YES  
SkipProductKey=YES  

SkipDomainMembership=YES  
JoinDomain=WOODGROVEBANK  
DomainAdmin=Administrator  
DomainAdminDomain=WOODGROVEBANK  
DomainAdminPassword=P@ssw0rd  

SkipUserData=Yes  
UserDataLocation=\\WDG-MDT-01\UserData$\Directory\usmtdata  

SkipTaskSequence=YES  
TaskSequenceID=Enterprise  

SkipComputerName=YES  
OSDComputerName=%SerialNumber%  

SkipPackageDisplay=YES  
LanguagePacks001={3af4e3ce-8122-41a2-9cf9-892145521660}  
LanguagePacks002={84fc70d4-db4b-40dc-a660-d546a50bf226}  

SkipLocaleSelection=YES  
UILanguage=en-US  
UserLocale=en-CA  
KeyboardLocale=0409:00000409  

SkipTimeZone=YES  
TimeZoneName=China Standard Time  

SkipApplications=YES  
Applications001={a26c6358-8db9-4615-90ff-d4511dc2feff}  
Applications002={7e9d10a0-42ef-4a0a-9ee2-90eb2f4e4b98}  

SkipBitLocker=YES  
SkipSummary=YES  
Powerusers001=WOODGROVEBANK\PilarA  
CaptureGroups=YES  
SLShare=\\WDG-MDT-01\UserData$\Logs  
Home_page=http://www.microsoft.com/NewComputer  
```  

## <a name="calling-web-services-in-mdt"></a>Appel de services web dans MDT  
 Dans les versions antérieures de MDT, le traitement des règles était pris en charge via CustomSettings.ini et les bases de données. Cela vous permettait de récupérer les valeurs de l’ordinateur local, généralement à l’aide de WMI, pour déterminer les actions à entreprendre sur chaque ordinateur durant le déploiement. De plus, vous pouviez effectuer des requêtes SQL et des appels de procédures stockées pour récupérer des informations supplémentaires de bases de données externes. Toutefois, cette approche présentait certains défis à relever, en particulier pour l’établissement de connexions SQL sécurisées.  

 Pour faciliter la gestion de ce problème, MDT peut effectuer des appels de services web en fonction de règles simples définies dans CustomSettings.ini. Ces requêtes de services web ne nécessitent aucun contexte de sécurité particulier, et peuvent utiliser tous les ports TCP/IP nécessaires pour simplifier les configurations de pare-feu.  

 L’exemple suivant montre comment configurer CustomSettings.ini pour appeler un service web particulier. Dans ce scénario, le service web est choisi au hasard à partir d’une recherche Internet. Il utilise un code postal en entrée et retourne la ville, l’état, l’indicatif régional et le fuseau horaire (sous forme de lettre) correspondants.  

```  
[Settings]  
Priority=Default, USZipService  
Properties=USZip, City, State, Zip, Area_Code, Time_Zones   
[Default]  
USZip=98052   
[USZipService]  
WebService=http://www.webservicex.net/uszip.asmx/GetInfoByZIP  
Parameters=USZip  
```  

 L’exécution de ce code produit une sortie similaire à ce qui suit :
```  
Added new custom property USZIP  
Added new custom property CITY  
Added new custom property STATE  
Added new custom property ZIP  
Added new custom property AREA_CODE  
Added new custom property TIME_ZONES  
Using from [Settings]: Rule Priority = DEFAULT, USZIPSERVICE  
------ Processing the [DEFAULT] section ------  
Property USZIP is now = 98052  
Using from [DEFAULT]: USZIP = 98052  
------ Processing the [USZIPSERVICE] section ------  
Using COMMAND LINE ARG: Ini file = CustomSettings.ini  
CHECKING the [USZIPSERVICE] section  
About to execute web service call to http://www.webservicex.net/uszip.asmx/GetInfoByZIP: USZip=98052  
Response from web service: 200 OK  
Successfully executed the web service.  
Property CITY is now = Redmond  
Obtained CITY value from web service:  CITY = Redmond  
Property STATE is now = WA  
Obtained STATE value from web service:  STATE = WA  
Property ZIP is now = 98052  
Obtained ZIP value from web service:  ZIP = 98052  
Property AREA_CODE is now = 425  
Obtained AREA_CODE value from web service:  AREA_CODE = 425  
------ Done processing CustomSettings.ini ------  
```  

 Il existe quelques complications mineures à surveiller quand vous exécutez un service web :  

-   Ne faites rien de spécial avec les serveurs proxy. Si un proxy anonyme est présent, utilisez-le, mais sachez que les serveurs proxy d’authentification peuvent poser des problèmes. Dans la plupart des cas, aucun service web n’est appelé.  

-   CustomSettings.ini ou ZTIGather.xml recherche les propriétés définies dans les balises XML retournées à la suite de l’appel de service web (comme pour une requête de base de données ou toute autre règle). Toutefois, la recherche XML respecte la casse. Heureusement, le service web décrit ici retourne tous les noms de propriétés en majuscules, ce qui est attendu par ZTIGather.xml. Pour contourner ce problème, il est possible de remapper les entrées qui sont en minuscules, ou qui mélangent majuscules et minuscules.  

-   Il est recommandé d’effectuer une requête `POST` auprès du service web. L’appel de service web doit donc pouvoir prendre en charge `POST`.  

## <a name="connecting-to-network-resources"></a>Connexion aux ressources réseau  
 Durant les processus de déploiement LTI et ZTI, vous pouvez avoir besoin d’accéder à une ressource réseau située sur un autre serveur que celui qui héberge le partage de déploiement. Vous devez être authentifié sur l’autre serveur pour pouvoir accéder aux dossiers ou services partagés sur ce dernier. Par exemple, vous pouvez installer une application à partir d’un dossier partagé situé sur un autre serveur que celui qui héberge le partage de déploiement utilisé par les scripts MDT.  

> [!NOTE]
>  Pour interroger les bases de données SQL Server hébergées sur un autre serveur que celui qui héberge le partage de déploiement, consultez les propriétés **Database**, **DBID**, **DBPwd**, **Instance**, **NetLib**, **Order**, **Parameters**, **ParameterCondition**, **SQLServer**, **SQLShare** et **Table** dans le document MDT *Toolkit Reference* (Référence du kit de ressources).  

 À l’aide du script ZTIConnect.wsf, vous pouvez vous connecter à d’autres serveurs et accéder aux ressources qu’ils hébergent. La syntaxe du script ZTIConnect.wsf est la suivante (où *unc_path* est un chemin UNC [Universal Naming Convention] de connexion au serveur) :  

```  
Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:unc_path  
```  

 Dans la plupart des cas, vous exécutez le script ZTIConnect.wsf en tant que tâche du séquenceur de tâches. Exécutez le script ZTIConnect.wsf avant les tâches qui nécessitent l’accès à un autre serveur que celui qui héberge le partage de déploiement.  

 **Pour ajouter le script ZTIConnect.wsf en tant que tâche à la séquence de tâches d’une build**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement*/Séquences de tâches (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Détails, cliquez sur ***séquence_tâches*** (où *séquence_tâches* correspond à la séquence de tâches à modifier).  

4.  Dans le volet Actions, cliquez sur **Propriétés**.  

5.  Cliquez sur l’onglet Séquence de tâches, accédez à **groupe** (où *groupe* correspond au groupe dans lequel le script ZTIConnect.wsf doit s’exécuter), puis cliquez sur **Ajouter**. Cliquez sur **Général**, puis sur **Exécuter la ligne de commande**.  

    > [!NOTE]
    >  Ajoutez la tâche avant d’ajouter les tâches qui nécessitent l’accès aux ressources situées sur le serveur cible.  

6.  Complétez l’onglet **Propriétés** de la nouvelle tâche à l’aide des informations suivantes :

    |**Dans cette zone** |**Faites cela** |  
    |-|-|  
    |**Nom** |Tapez **Connexion à serveur** (où serveur correspond au nom du serveur auquel se connecter).|  
    |**Description** |Tapez le texte qui explique pourquoi la connexion doit être établie.|  
    |**Command** |Tapez **Cscript.exe “%SCRIPTROOT%\ZTIConnect.wsf” /uncpath:chemin_unc** (où *chemin_unc* correspond au chemin UNC d’un dossier partagé sur le serveur).|  

7.  Complétez l’onglet **Options** de la nouvelle tâche à l’aide des informations suivantes. Sauf indication contraire, acceptez les valeurs par défaut, puis cliquez sur **OK**.  

    |**Dans cette zone** |**Faites cela** |  
    |-|-|  
    |**Codes de réussite** |Tapez **0 3010**. (Le script ZTIConnect.wsf retourne ces codes en cas de réussite.)|  
    |**Zone de liste Conditions** |Ajoutez toutes les conditions nécessaires. (Dans la plupart des cas, cette tâche ne nécessite aucune condition.)|  

 Une fois que vous avez ajouté la tâche qui doit exécuter le script ZTIConnect.wsf, les tâches suivantes peuvent accéder aux ressources réseau du serveur spécifié dans l’option **/uncpath** du script ZTIConnect.wsf.  

## <a name="deploying-the-correct-device-drivers-to-computers-with-the-same-hardware-devices-but-different-make-and-model"></a>Déploiement des pilotes de périphériques appropriés sur des ordinateurs ayant les mêmes périphériques matériels mais avec des marques et des modèles distincts  
 Il existe parfois certaines variantes de noms et de numéros de modèles avec quasiment aucune différence dans le jeu de pilotes. Ces variantes de noms et de numéros de modèles peuvent accroître inutilement le temps nécessaire à la création de plusieurs entrées de base de données pour un modèle donné. La procédure suivante montre comment définir une nouvelle propriété à l’aide d’un appel de fonction de sortie utilisateur qui retourne une sous-chaîne du numéro de modèle.  

 **Pour créer des alias de modèles**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés**, cliquez sur l’onglet **Règles**.  

5.  Créez des alias pour les types de matériel dans les sections Make et Model de la base de données MDT. Tronquez le type du modèle au niveau des parenthèses ouvrantes « ( » dans le nom de modèle. Par exemple, *HP DL360 (G112)* devient *HP DL360*.  

6.  Ajoutez la variable personnalisée **ModelAlias** à chaque section.  

7.  Créez une section `[SetModel]`.  

8.  Ajoutez la section `[SetModel]` aux paramètres **Priority** de la section `[Settings]`.  

9. Ajoutez une ligne à la section `ModelAlias` pour référencer un script de sortie utilisateur qui va tronquer le nom de modèle au niveau de « ( ».  

10. Créez une recherche de base de données **MMApplications**, où **ModelAlias** est égal à **Model**.  

11. Créez un script de sortie utilisateur et placez-le dans le même répertoire que le fichier CustomSettings.ini pour tronquer le nom de modèle.  

    L’exemple suivant montre le contenu d’un fichier CustomSettings.ini et d’un script de sortie utilisateur, respectivement.  

     **CustomSettings.ini** :  

    ```  
    [Settings]   
    Priority=SetModel, MMApplications, Default   
    Properties= ModelAlias   
    [SetModel]   
    ModelAlias=#SetModelAlias()#   
    Userexit=Userexit.vbs   
    [MMApplications]   
    SQLServer=Server1  
    Database=MDTDB   
    Netlib=DBNMPNTW   
    SQLShare=logs   
    Table= MakeModelSettings    
    Parameters=Make, ModelAlias   
    ModelAlias=Model   
    Order=Sequence  
    ```  

     **Script de sortie utilisateur** :  

    ```  
    Function UserExit(sType, sWhen, sDetail, bSkip)   
      UserExit = Success   
    End Function   

    Function SetModelAlias()   
      If Instr(oEnvironment.Item("Model"), "(") <> 0 Then   
        SetModelAlias = Left(oEnvironment.Item("Model"), _  
                          Instr(oEnvironment.Item("Model"), _  
                            "(") - 1)   
        oLogging.CreateEntry "USEREXIT – " & _  
          "ModelAlias has been set to " & SetModelAlias, _  
          LogTypeInfo  
      Else   
        SetModelAlias = oEnvironment.Item("Model")   
        oLogging.CreateEntry " USEREXIT - " & _  
          "ModelAlias has not been changed.", LogTypeInfo   
      End if   
    End Function  
    ```  

## <a name="configuring-conditional-task-sequence-steps"></a>Configuration d’étapes de séquence de tâches conditionnelles  
 Dans certains scénarios, vous pouvez exécuter une étape de séquence de tâches basée de manière conditionnelle sur des critères définis. Vous pouvez ajouter toutes sortes de combinaisons de ces conditions pour déterminer si l’étape de séquence de tâches doit s’exécuter. Par exemple, utilisez la valeur d’une variable de séquence de tâches et la valeur d’un paramètre de Registre pour déterminer si une étape de séquence de tâches doit s’exécuter.  

 À l’aide de MDT, exécutez une séquence de tâches de manière conditionnelle en fonction des points suivants :  

-   Une ou plusieurs instructions **IF**  

-   Variable de séquence de tâches  

-   Version du système d’exploitation cible  

-   Résultats booléens d’une requête WMI  

-   Paramètre de Registre  

-   Logiciel installé sur l’ordinateur cible  

-   Propriétés d’un dossier  

-   Propriétés d’un fichier  

### <a name="configuring-a-conditional-task-sequence-step"></a>Configuration d’une étape de séquence de tâches conditionnelle  
 Vous pouvez configurer les étapes de séquence de tâches conditionnelles dans Deployment Workbench, sous l’onglet **Options** d’une étape de séquence de tâches. Vous pouvez ajouter une ou plusieurs conditions à l’étape de séquence de tâches afin de créer la condition appropriée pour exécuter ou ne pas exécuter l’étape.  

> [!NOTE]
>  Chaque étape de séquence de tâches conditionnelle nécessite au moins une instruction **IF**.  

 **Pour afficher l’onglet Options d’une étape de séquence de tâches**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement*/Séquences de tâches (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Détails, cliquez sur **séquence_tâches** (où *séquence_tâches* correspond au nom de la séquence de tâches à configurer).  

4.  Dans le volet Actions, cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Propriétés** de ***séquence_tâches***, sous l’onglet **Séquence de tâches**, cliquez sur ***étape*** (où *étape* correspond au nom de l’étape de séquence de tâches à configurer), puis cliquez sur l’onglet **Options**.  

 Sous l’onglet **Options** de l’étape de séquence de tâches, effectuez les actions suivantes :  

-   **Ajouter.** Cliquez sur ce bouton pour ajouter une condition à l’étape de séquence de tâches.  

-   **Supprimer.** Cliquez sur ce bouton pour supprimer une condition dans une étape de séquence de tâches.  

-   **Modifier.** Cliquez sur ce bouton pour modifier une condition dans une étape de séquence de tâches.  

### <a name="if-statements-in-conditions"></a>Instructions IF dans les conditions  
 Toutes les conditions de séquence de tâches incluent une ou plusieurs instructions **IF**. Les instructions **IF** sont la base de la création d’étapes de séquence de tâches conditionnelles. Une condition d’étape de séquence de tâches ne peut inclure qu’une seule instruction **IF**. Toutefois, plusieurs instructions **IF** peuvent être imbriquées sous l’instruction **IF** de niveau supérieur pour créer des conditions plus complexes.  

 Une instruction **IF** peut être basée sur les conditions listées dans le tableau ci-après. Vous pouvez les configurer dans la boîte de dialogue **Propriétés de l’instruction IF**.  

 |**Condition** |**Sélectionnez cette option pour exécuter la séquence de tâches si** |  
 |-|-|  
 |**Toutes les conditions** |Toutes les conditions sous cette instruction **IF** doivent être vraies.|  
 |**Une condition** |Une condition sous cette instruction **IF** est vraie.|  
 |**Aucun** |Aucune condition sous cette instruction **IF** n’est vraie.|  

 Complétez la condition d’exécution de l’étape de séquence de tâches en ajoutant d’autres critères aux conditions (par exemple, des variables de séquence de tâches ou des valeurs de paramètre de Registre).  

 **Pour ajouter une condition basée sur une instruction IF à une étape de séquence de tâches**  

1.  Sous l’onglet **Option** de ***étape*** (où *étape* correspond au nom de l’étape de séquence de tâches à configurer), cliquez sur **Ajouter**, puis sur **Instruction If**.  

2.  Dans la boîte de dialogue **Propriétés de l’instruction If**, cliquez sur **condition** (où *condition* correspond à l’une des conditions listées dans le tableau précédent), puis cliquez sur **OK**.  

### <a name="task-sequence-variables-in-conditions"></a>Variables de séquence de tâches dans les conditions  
 Utilisez la condition **Variable de séquence de tâches** pour évaluer les variables de séquence de tâches créées par une tâche **Définir une variable de séquence de tâches** ou par une tâche de la séquence de tâches. Prenons l’exemple d’un réseau qui contient des ordinateurs clients Windows XP. Certains sont membres d’un domaine et d’autres font partie d’un groupe de travail. Sachant que la stratégie de domaine actuelle force tous les paramètres utilisateur à être enregistrés sur le réseau, les paramètres utilisateur doivent être enregistrés uniquement pour les ordinateurs qui ne font pas partie du domaine, c’est-à-dire les ordinateurs du groupe de travail. Dans ce cas, ajoutez une condition à la tâche **Capturer les paramètres et fichiers utilisateur**, qui cible les ordinateurs du groupe de travail.  

 **Pour ajouter une condition basée sur une variable de séquence de tâches**  

1.  Sous l’onglet **Options** de ***étape*** (où *étape* correspond au nom de l’étape de séquence de tâches à configurer), cliquez sur **Ajouter une condition**, puis sur **Variable de séquence de tâches**.  

2.  Dans la boîte de dialogue de condition de la **Variable de séquence de tâches**, dans la zone **Variable**, tapez **OSDJoinType**.  

    > [!NOTE]
    >  Cette variable a la valeur **0** pour les ordinateurs membres d’un domaine, et **1** pour ceux qui sont membres d’un groupe de travail.  

3.  Dans la zone **Condition**, cliquez sur **égal à**.  

4.  Dans la zone **Valeur**, tapez **1**, puis cliquez sur **OK**.  

### <a name="operating-system-version-in-conditions"></a>Version du système d’exploitation dans les conditions  
 Utilisez la condition **Version du système d’exploitation** pour vérifier la version du système d’exploitation d’un ordinateur cible ou du client existant (au moment de la capture d’une image). Prenons l’exemple d’un réseau qui contient plusieurs serveurs qui doivent être mis à niveau de Windows Server 2003 vers Windows Server 2008. Vous devez copier et appliquer uniquement les paramètres réseau aux serveurs qui exécutent Windows Server 2003. Tous les autres serveurs ont les paramètres réseau par défaut utilisés par Windows Server 2008.  

 **Pour ajouter une condition basée sur la version du système d’exploitation**  

1.  Dans l’Éditeur de séquence de tâches, cliquez sur la tâche **Capturer les paramètres réseau**.  

2.  Cliquez sur **Ajouter une condition**, puis sur **Version du système d’exploitation**.  

3.  Dans la zone **Architecture**, cliquez sur le serveur approprié. Pour cet exemple, cliquez sur **x86**.  

4.  Dans la zone **Système d’exploitation**, cliquez sur le système d’exploitation et la version pour lesquels vous souhaitez définir une condition. Pour cet exemple, cliquez sur **x86 Windows 2003**.  

5.  Dans la zone **Condition**, cliquez sur la condition appropriée, puis sur **OK**.  

### <a name="file-properties-in-conditions"></a>Propriétés de fichier dans les conditions  
 Utilisez la condition **Propriétés du fichier** pour vérifier la version et/ou l’horodatage d’un fichier donné afin de déterminer l’exécution ou non d’une tâche ou d’un groupe de tâches. Dans cet exemple, l’environnement de production contient une image Windows Server 2003 constamment mise à jour et utilisée pour chaque nouveau serveur ajouté au réseau. Tous les ordinateurs serveurs de l’environnement exécutent une application personnalisée qui nécessite l’API (interface de programmation d’applications) DAO (Digital Access Object) version 3.60.6815.  

 Tous les serveurs existants fonctionnent correctement. Toutefois, aucun nouveau serveur ajouté au réseau avec l’image ne parvient à exécuter l’application. Dans la mesure où un autre groupe est responsable de la gestion et de la mise à jour des images, vous décidez de changer la séquence de tâches de déploiement pour permettre l’installation de la version appropriée de DAO, si la version existante de DAO déployée avec l’image est incorrecte.  

 **Pour ajouter une condition basée sur des propriétés de fichier à une étape de séquence de tâches dans Configuration Manager 2007 R3**  

1.  Dans Configuration Manager 2007 R3, créez un package pour installer DAO 3.60.6815. Appelez ce package *DAO* avec un programme appelé *InstallDAO*. Pour en savoir plus sur la création de packages, consultez [Guide pratique pour créer un package](http://technet.microsoft.com/library/bb693627.aspx).  

2.  Créez une étape **Installer le logiciel** pour déployer le package DAO.  

3.  Cliquez sur l’étape de séquence de tâches **Installer le logiciel** créée à l’étape 2, puis cliquez sur l’onglet **Options**.  

4.  Cliquez sur **Ajouter une condition**, puis sur **Propriétés du fichier**.  

5.  Dans la zone **Chemin**, tapez **C:\Program Files\Microsoft Shared\DAO\dao360.dll**.  

6.  Cochez la case **Vérifier la version**, puis cliquez sur **différent de** pour la condition.  

7.  Dans la zone **Version**, tapez **3.60.6815**.  

8.  Dans le cas présent, décochez la case **Vérifier l’horodatage**, puis cliquez sur **OK**.  

### <a name="folder-properties-in-conditions"></a>Propriétés de dossier dans les conditions  
 Utilisez la condition **Propriétés du dossier** pour vérifier l’horodatage d’un dossier donné afin de déterminer l’exécution ou non d’une tâche ou d’un groupe de tâches. Prenons l’exemple d’une situation dans laquelle une application développée en interne a été mise à jour pour pouvoir fonctionner avec Windows 8. Tous les ordinateurs du réseau n’ont pas la dernière version de l’application. Vous devez donc effectuer un processus de conversion de données avant de pouvoir mettre à niveau l’application.  

 Si l’horodatage du dossier d’installation de l’application est antérieur ou égal au 31/12/2007, l’ordinateur cible exécute la version incompatible de l’application. Dans ce cas, vous devez exécuter le processus de conversion de données sur l’ordinateur cible. Exécutez une étape de séquence de tâches de manière conditionnelle pour effectuer le processus de conversion de données sur les ordinateurs qui ont une version antérieure de l’application.  

 **Pour ajouter une condition basée sur des propriétés de dossier à une étape de séquence de tâches**  

1.  Dans la console Configuration Manager ou dans Deployment Workbench, dans l’Éditeur de séquence de tâches, modifiez ***séquence_tâches*** (où *séquence_tâches* correspond à la séquence de tâches à modifier).  

2.  Créez une tâche **Ligne de commande** pour effectuer le processus de conversion de données.  

3.  Cliquez sur la tâche créée à l’étape 1.  

4.  Cliquez sur **Ajouter une condition**, puis sur **Propriétés du dossier**.  

5.  Dans la zone **Chemin**, tapez le chemin du dossier qui contient l’application.  

6.  Cochez la case **Vérifier l’horodatage**.  

7.  Cliquez sur **Inférieur ou égal à** pour la condition.  

8.  Dans la zone **Date**, cliquez sur **31/12/2007**.  

9. Dans la zone **Heure**, cliquez sur **00:00:00**, puis sur **OK**.  

### <a name="registry-settings-in-conditions"></a>Paramètres de Registre dans les conditions  
 Utilisez la condition **Paramètre du Registre** pour vérifier l’existence de clés et de valeurs dans le Registre, ainsi que les données correspondantes stockées dans les valeurs de Registre. Prenons l’exemple suivant : une application utilisée sur un ensemble restreint d’ordinateurs ne peut pas s’exécuter sur Windows 8. Un déploiement de Windows 8 est mis en place pour permettre la mise à niveau des ordinateurs qui exécutent Windows XP. Créez une condition sur la toute première tâche d’une séquence pour rechercher dans le Registre une entrée relative à l’application incompatible et, si cette entrée existe, interrompre le processus de déploiement de l’ordinateur concerné.  

 **Pour ajouter une condition basée sur un paramètre de Registre à une étape de séquence de tâches**  

1.  Dans la console Configuration Manager ou dans Deployment Workbench, dans l’Éditeur de séquence de tâches, modifiez ***séquence_tâches*** (où *séquence_tâches* correspond à la séquence de tâches de déploiement de Windows 8).  

2.  Cliquez sur la première tâche de la séquence, puis sur l’onglet **Options**.  

3.  Cliquez sur **Ajouter une condition**, puis sur **Paramètres du Registre**.  

4.  Dans la liste **Clé racine**, cliquez sur **HKEY_LOCAL_MACHINE**.  

5.  Dans la zone **Clé**, tapez **SOFTWARE\WOODGROVE**.  

6.  Cliquez sur **n’existe pas** pour la condition. Dans le cas présent, la tâche s’exécute et la séquence se poursuit uniquement si la clé n’existe pas.  

7.  Éventuellement, la condition peut vérifier la non-existence d’une valeur si vous tapez son nom dans la zone **Nom de la valeur**.  

8.  Si une autre condition que **existe/n’existe pas** est utilisée, spécifiez une valeur et un type de valeur.  

9. Cliquez sur **OK**.  

### <a name="wmi-queries-in-conditions"></a>Requêtes WMI dans les conditions  
 Utilisez la condition **Requête WMI** pour exécuter une requête WMI. La condition a la valeur True si la requête retourne au moins un résultat. Prenons l’exemple d’une équipe de déploiement chargée de mettre à niveau le système d’exploitation de tous les serveurs d’un modèle donné (Dell 1950, par exemple). Vous pouvez utiliser une requête WMI pour vérifier le modèle de chaque ordinateur et procéder au déploiement uniquement si le modèle approprié est trouvé.  

 **Pour ajouter une condition basée sur une requête WMI à une étape de séquence de tâches**  

1.  Dans la console Configuration Manager ou dans Deployment Workbench, dans l’Éditeur de séquence de tâches, modifiez ***séquence_tâches*** (où *séquence_tâches* correspond à la séquence de tâches de mise à niveau des serveurs).  

2.  Cliquez sur la première tâche de la séquence, puis sur l’onglet **Options**.  

3.  Cliquez sur **Ajouter une condition**, puis sur **Interroger WMI**.  

4.  Dans la zone **Espace de noms WMI**, tapez **root\cimv2**.  

5.  Dans la zone **Requête WQL**, tapez **Select \* From Win32_ComputerSystem WHERE Model LIKE "%Dell%%1950%"**. Cliquez sur **OK**.  

### <a name="installed-software-in-conditions"></a>Logiciel installé dans les conditions  
 Utilisez la condition **Logiciel installé** pour vérifier si un logiciel particulier est installé sur un ordinateur cible. Seuls les logiciels installés à l’aide de fichiers MSI (Microsoft Installer) peuvent être évalués à l’aide de cette condition. Imaginons par exemple que vous souhaitiez mettre à niveau le système d’exploitation de tous les serveurs, à l’exception de ceux qui exécutent Microsoft SQL Server 2012.  

 **Pour ajouter une condition basée sur un logiciel installé à une étape de séquence de tâches**  

1.  Dans la console Configuration Manager ou dans Deployment Workbench, dans l’Éditeur de séquence de tâches, modifiez ***séquence_tâches*** (où *séquence_tâches* correspond à la séquence de tâches de mise à niveau des serveurs).  

2.  Cliquez sur la première tâche de la séquence, puis sur l’onglet **Options**.  

3.  Cliquez sur **Ajouter une condition**, puis sur **Logiciel installé**.  

4.  Cliquez sur **Parcourir**, puis sur le fichier MSI pour SQL Server 2012.  

5.  Cochez la case **Faire correspondre à ce produit spécifique** pour indiquer que seuls les ordinateurs ayant SQL Server 2012, et aucune autre version, sont les ordinateurs cibles que cette requête doit détecter.  

6.  Cliquez sur **OK**.  

### <a name="complex-conditions"></a>Conditions complexes  
 Vous pouvez regrouper plusieurs conditions à l’aide d’instructions **IF** pour créer des conditions complexes. Par exemple, une étape particulière doit être exécutée uniquement pour les ordinateurs Contoso 1950 exécutant Windows Server 2003 ou Windows Server 2008. Si vous écrivez la condition sous forme d’instruction **IF** programmatique, elle ressemble à ceci :  

```  
IF ((Computer Model IS “Contoso 1950”) AND (operating system=2003 OR operating system=2008))  
```  

 **Pour ajouter une condition complexe**  

1.  Dans la console Configuration Manager ou dans Deployment Workbench, dans l’Éditeur de séquence de tâches, modifiez ***séquence_tâches*** (où *séquence_tâches* correspond à la séquence de tâches de mise à niveau des serveurs).  

2.  Cliquez sur l’étape de séquence de tâches à laquelle ajouter la condition, puis cliquez sur l’onglet **Options**.  

3.  Cliquez sur **Ajouter une condition**, sur **Instruction If**, puis sur **Toutes les conditions**. Cliquez sur **OK**.  

4.  Cliquez sur l’instruction de condition, sur **Ajouter une condition**, puis sur **Requête WMI**.  

5.  Vérifiez que **root\cimv2** est spécifié en tant qu’espace de noms WMI, puis, dans la zone **Requête WQL**, tapez **SELECT \* FROM Win32_ComputerSystem WHERE ComputerModel LIKE “%Contoso%1950%”**. Cliquez sur **OK**.  

6.  Cliquez sur l’instruction **IF**, puis sur **Ajouter une condition**. Cliquez sur **Instruction If**, puis sur **Une condition**. Cliquez sur **OK**.  

7.  Cliquez sur la seconde instruction **IF**. Cliquez sur **Ajouter une condition**, puis sur **Version du système d’exploitation**.  

8.  Dans la zone **Architecture**, cliquez sur l’architecture des serveurs. Pour cet exemple, cliquez sur **x86**.  

9. Dans la zone **Operating system** (Système d’exploitation), cliquez sur le système d’exploitation et sa version. Pour cet exemple, cliquez sur **x86 Windows 2003 original release** (Clients x86 Windows Server 2003, version d'origine). Cliquez sur **OK**.  

10. Cliquez sur la seconde instruction **IF**. Cliquez sur **Ajouter une condition**, puis sur **Version du système d’exploitation**.  

11. Dans la zone **Architecture**, cliquez sur l’architecture des serveurs. Pour cet exemple, cliquez sur **x86**.  

12. Dans la zone **Operating system** (Système d’exploitation), cliquez sur le système d’exploitation et sa version. Pour cet exemple, cliquez sur **x86 Windows 2008 original release** (Clients x86 Windows Server 2008, version d’origine). Cliquez sur **OK**.  

## <a name="creating-a-highly-scalable-lti-deployment-infrastructure"></a>Création d’une infrastructure de déploiement avec installation LTI hautement évolutive  
 Dans ce scénario, aucune distribution électronique de logiciels n’est disponible pour l’infrastructure de déploiement : vous utilisez donc MDT pour créer une infrastructure de déploiement avec installation LTI entièrement automatisée. L’infrastructure d’installation LTI évolutive utilise les technologies SQL Server, Services de déploiement Windows et Windows Server 2003 DFS-R (Distributed File System Replication).  

 Vous mettez à l’échelle l’infrastructure d’installation LTI comme ceci :  

-   Vérifiez que l’infrastructure appropriée existe, comme décrit dans [Vérification de l’existence de l’infrastructure appropriée](#EnsureInfrastructure)  

-   Ajoutez du contenu à MDT, comme décrit dans [Ajout de contenu à MDT](#AddContent)  

-   Préparez les services de déploiement Windows, comme décrit dans [Préparation des services de déploiement Windows](#PrepareDeployment)  

-   Configurez DFS-R, comme décrit dans [Configuration de la réplication du système de fichiers DFS](#ConfigureFileReplication)  

-   Préparez la réplication SQL Server, comme décrit dans [Préparation de la réplication SQL Server](#PrepareSQLReplication)  

-   Configurez la réplication SQL Server, comme décrit dans [Configuration de la réplication SQL Server](#ConfigureSQLReplication)  

 Ce scénario suppose que MDT est configuré sur un serveur de déploiement principal, et que la configuration de la base de données MDT a déjà été effectuée, comme décrit au début de ce document.  

###  <a name="EnsureInfrastructure"></a> Vérification de l’existence de l’infrastructure appropriée  
 L’infrastructure de déploiement avec installation LTI hautement évolutive utilise une topologie « hub-and-spoke » pour la réplication du contenu : vous devez donc d’abord désigner un serveur de déploiement dans l’environnement de production qui exécutera le rôle du serveur de déploiement principal.  Voici la liste des composants nécessaires pour le serveur de déploiement principal.  

 |**Composant nécessaire** |**Objectif/commentaire** |  
 |-|-|  
 |Windows Server 2003 R2|Nécessaire pour prendre en charge DFS-R|  
 |MDT |Contient la copie principale du partage de déploiement|  
 |SQL Server 2005|Doit être une version complète pour permettre la réplication de la base de données MDT|  
 |DFS-R |Nécessaire pour la réplication du partage de déploiement|  
 |Services de déploiement Windows |Nécessaire pour permettre le lancement des installations réseau PXE|  

 Quand vous avez sélectionné le serveur de déploiement principal, provisionnez d’autres serveurs sur chaque site pour prendre en charge les déploiements d’installation LTI.  Voici la liste des composants nécessaires pour le serveur de déploiement enfant.  

 |**Composant nécessaire** |**Objectif/commentaire** |  
 |-|-|  
 |Windows Server 2003 R2|Nécessaire pour prendre en charge DFS-R|  
 |Microsoft SQL Server 2005 Express Edition |Reçoit des copies répliquées de la base de données MDT|  
 |DFS-R |Nécessaire pour la réplication du partage de déploiement|  
 |Services de déploiement Windows |Nécessaire pour permettre le lancement des installations réseau PXE|  

> [!NOTE]
>  Les services de déploiement Windows doivent être configurés sur chaque serveur enfant, mais il n’est pas nécessaire d’ajouter des images de démarrage ou d’installation.  

###  <a name="AddContent"></a> Ajout de contenu à MDT  
 Remplissez le serveur de déploiement principal avec du contenu en utilisant Deployment Workbench, puis créez et remplissez la base de données MDT, comme décrit dans les sections suivantes. Pour plus d’informations sur le remplissage de la base de données avec :  

-   Des applications : consultez la section « Configuration d’applications dans Deployment Workbench » dans le document MDT *Utilisation de Microsoft Deployment Toolkit*  

-   Des systèmes d’exploitation: consultez la section « Configuration de systèmes d’exploitation dans Deployment Workbench » dans le document MDT *Utilisation de Microsoft Deployment Toolkit*  

-   Des packages de système d’exploitation: consultez la section « Configuration de packages de système d’exploitation dans Deployment Workbench » dans le document MDT *Utilisation de Microsoft Deployment Toolkit*  

-   Des pilotes de périphérique : consultez la section « Configuration de pilotes de périphérique dans Deployment Workbench » dans le document MDT *Utilisation de Microsoft Deployment Toolkit*  

-   Des séquences de tâches : consultez la section « Configuration de séquences de tâches dans Deployment Workbench » dans le document MDT *Utilisation de Microsoft Deployment Toolkit*  

> [!NOTE]
>  Vérifiez que le fichier LiteTouchPE_x86.wim créé lors de la mise à jour du partage de déploiement a été ajouté aux services de déploiement Windows.  

###  <a name="PrepareDeployment"></a> Préparation des services de déploiement Windows  
 Comme le fichier LiteTouchPE_x86.wim sera répliqué périodiquement via le groupe de réplication DFS-R, le magasin de données de configuration de démarrage doit être mis à jour périodiquement de façon à refléter l’environnement Windows PE nouvellement répliqué. Effectuez les étapes suivantes sur chacun des serveurs de déploiement.  

 **Pour préparer les services de déploiement Windows**  

1.  Ouvrez une fenêtre d'invite de commandes.  

2.  Tapez **WDSUtil/set-server/BCDRefreshPolicy/Enabled:yes/RefreshPeriod:60**, puis appuyez sur Entrée.  

> [!NOTE]
>  Dans l’exemple présenté ici, la fréquence d’actualisation est définie sur 60 minutes. Vous pouvez cependant configurer cette valeur de façon à effectuer la réplication à une fréquence identique à celle de la réplication DFS-R.  

###  <a name="ConfigureFileReplication"></a> Configuration de la réplication du système de fichiers distribués (DFS-R)  
 Lors de la mise à l’échelle de l’architecture de déploiement avec installation LTI, vous utilisez DFS-R comme base pour répliquer le contenu du partage de déploiement MDT et de l’environnement de démarrage Windows PE Lite Touch, et du serveur de déploiement principal vers les serveurs de déploiement enfants.  

> [!NOTE]
>  Vérifiez que DFS-R est installé avant d’effectuer les étapes suivantes.  

 **Pour configurer DFS-R pour répliquer le contenu du déploiement**  

1.  Ouvrez la console DFS Management (Gestion DFS).  

2.  Dans la console DFS Management (Gestion DFS), développez DFS Management (Gestion DFS).  

3.  Cliquez avec le bouton droit sur **Replication** (Réplication), puis cliquez sur **New Replication Group** (Nouveau groupe de réplication).  

4.  Dans l’Assistant New Replication Group (Nouveau groupe de réplication), dans la page **Replication Group Type** (Type de groupe de réplication), cliquez sur **New Multipurpose Replication Group** (Nouveau groupe de réplication multi-usage).  

5.  Cliquez sur **Suivant**.  

6.  Dans la page **Name and Domain** (Nom et domaine), entrez les informations suivantes :  

    -   Dans la zone **Name for replication group** (Nom du groupe de réplication), entrez un nom pour le groupe de réplication, par exemple **Groupe de réplication MDT 2010**.  

    -   Dans la zone **Optional description of replication group** (Description facultative du groupe de réplication), entrez une description du groupe de réplication, par exemple **Groupe de réplication des données MDT 2010**.  

    -   Vérifiez que la zone **Domain** (Domaine) contient le nom de domaine correct.  

7.  Cliquez sur **Suivant**.  

8.  Dans la page **Replication Group Members** (Membres du groupe de réplication), effectuez les étapes suivantes :  

    1.  Cliquez sur **Ajouter**.  

    2.  Tapez les noms de tous les serveurs qui sont membres de ce groupe de réplication, par exemple tous les serveurs de déploiement enfants et le serveur de déploiement principal.  

    3.  Cliquez sur **OK**.  

9. Cliquez sur **Suivant**.  

10. Dans la page **Topology Selection** (Sélection de topologie), cliquez sur **Hub and Spoke**, puis cliquez sur **Suivant**.  

11. Dans la page **Hub Members** (Membres concentrateurs), cliquez sur le serveur de déploiement principal, puis cliquez sur **Add** (Ajouter).  

12. Cliquez sur **Suivant**.  

13. Dans la page **Hub and Spoke Connections** (Connexions Hub and Spoke), vérifiez que pour chaque serveur de déploiement enfant, le serveur de déploiement principal indiqué est **Required Hub Member** (Membre concentrateur requis).  

14. Cliquez sur **Suivant**.  

15. Dans la page **Replication Group Schedule and Bandwidth** (Planification et bande passante du groupe de réplication), spécifiez une planification pour répliquer le contenu entre les serveurs.  

16. Cliquez sur **Suivant**.  

17. Dans la page **Primary Member** (Membre principal), dans la zone **Primary Member** (Membre principal), cliquez sur le serveur de déploiement principal.  

18. Cliquez sur **Suivant**.  

19. Dans la page **Folders to Replicate** (Dossiers à répliquer), cliquez sur **Add** (Ajouter), puis effectuez ces étapes :  

    1.  Dans la zone **Local Path of the folder to replicate** (Chemin local du dossier à répliquer), cliquez sur **Browse** (Parcourir) pour accéder au dossier *X:\\*Deployment (où *X* est la lettre de lecteur sur le serveur de déploiement).  

    2.  Cliquez sur **Use name based on path** (Utiliser le nom basé sur le chemin).  

    3.  Cliquez sur **OK**.  

    4.  Cliquez sur **Ajouter**.  

    5.  Dans la boîte de dialogue **Add Folder to Replicate** (Ajouter un dossier à répliquer), cliquez sur **Browse** (Parcourir) pour accéder au dossier *X:* \RemoteInstall\Boot.  

    6.  Cliquez sur **Use name based on path** (Utiliser le nom basé sur le chemin).  

20. Cliquez sur **Suivant**.  

21. Dans la page **Local Path of Distribution on Other Members** (Chemin local de distribution sur les autres membres), effectuez ces étapes :  

    1.  Sélectionnez tous les membres du groupe de distribution, puis cliquez sur **Edit** (Modifier).  

    2.  Dans la boîte de dialogue **Edit Local Path** (Modifier le chemin local), cliquez sur **Enabled** (Activé).  

    3.  Entrez le chemin où le dossier Deployment Share (Partage de déploiement) doit être stocké sur le serveur de déploiement enfant, par exemple ***X:\Deployment*** (où *X* est la lettre de lecteur sur le serveur de déploiement).  

    4.  Cliquez sur **OK**.  

22. Cliquez sur **Suivant**.  

23. Dans la page **Local Path of Boot on Other Members** (Chemin local de démarrage sur les autres membres), effectuez ces étapes :  

    1.  Sélectionnez tous les membres du groupe de distribution, puis cliquez sur **Edit** (Modifier).  

    2.  Dans la boîte de dialogue **Edit Local Path** (Modifier le chemin local), cliquez sur **Enabled** (Activé).  

    3.  Entrez le chemin où le dossier Boot (Démarrage) doit être stocké sur le serveur de déploiement enfant, par exemple ***X:\RemoteInstall\Boot*** (où *X* est la lettre de lecteur sur le serveur de déploiement).  

    4.  Cliquez sur **OK**.  

24. Cliquez sur **Suivant**.  

25. Dans la page **Remote Settings and Create Replication Group** (Paramètres distants - Créer un groupe de réplication), cliquez sur **Create** (Créer) pour terminer l’Assistant New Replication Group (Nouveau groupe de réplication).  

26. Dans la page **Confirmation**, cliquez sur **Close** (Fermer) pour fermer l’Assistant.  

> [!NOTE]
>  Vérifiez que le nouveau groupe de réplication apparaît maintenant sous le nœud Réplication.  

###  <a name="PrepareSQLReplication"></a> Préparation de la réplication SQL Server  
 Avant de pouvoir configurer la réplication SQL Server, vous devez effectuer plusieurs étapes de préconfiguration pour que les serveurs de déploiement soient correctement configurés.  

 **Pour préparer la réplication SQL Server sur le serveur de déploiement principal**  

1.  Créez un dossier pour stocker les instantanés de base de données, puis configurez le dossier en tant que partage.  

    > [!NOTE]
    >  Pour plus d’informations sur la sécurisation du dossier d’instantanés, consultez [Sécurisation du dossier d’instantanés](http://msdn2.microsoft.com/library/ms151151.aspx).  

2.  Vérifiez que le service SQL Server Browser est activé et défini sur Automatique.  

3.  Dans la zone **Configuration de la surface d’exposition de SQL Server**, cliquez sur **Connexions locales et distantes**.  

 **Pour préparer la réplication SQL Server sur le serveur de déploiement enfant**  

1.  Dans la zone **Configuration de la surface d’exposition de SQL Server**, cliquez sur **Connexions locales et distantes**.  

2.  Vous pouvez aussi créer une base de données vide pour héberger la base de données MDT répliquée.  

> [!NOTE]
>  Cette base de données doit avoir le même nom que la base de données MDT sur le serveur de déploiement principal. Par exemple, si la base de données MDT sur le serveur de déploiement principal est nommée *MDTDB*, créez une base de données vide nommée *MDTDB* sur le serveur de déploiement enfant.  

###  <a name="ConfigureSQLReplication"></a> Configuration de la réplication SQL Server  
 Après avoir configuré la réplication des fichiers et des dossiers nécessaires pour créer l’infrastructure de déploiement, configurez SQL Server pour la réplication de la base de données MDT.  

> [!NOTE]
>  Il est également possible de ne gérer qu’une seule base de données MDT centralisée ; cependant, en conservant une version répliquée de la base de données MDT, vous pouvez mieux contrôler les données transférées sur le réseau WAN.  

 SQL Server 2005 utilise un modèle de réplication qui est similaire à un modèle de distribution de magazines :  

1.  Un *magazine* est rendu disponible (publié) par un *éditeur*.  

2.  Des *distributeurs* sont utilisés pour distribuer la publication.  

3.  Les *lecteurs* peuvent s’abonner à une publication : cette publication est alors remise périodiquement à l’abonné (un *abonnement par envoi (push)*).  

 Cette terminologie est utilisée dans les Assistants Installation et Configuration de la réplication SQL Server.  

#### <a name="configure-a-sql-server-publisher"></a>Configurer un serveur de publication SQL Server  
 Pour configurer le serveur de déploiement principal comme serveur de publication SQL Server, effectuez les étapes suivantes :  

1.  Ouvrez SQL Server Management Studio.  

2.  Cliquez avec le bouton droit sur le nœud **Réplication**, puis cliquez sur **Configurer la distribution**.  

3.  Dans l’Assistant Configuration de la distribution, cliquez sur **Suivant**.  

4.  Sur la page **Serveur de distribution**, cliquez sur **agit comme son propre serveur de distribution ; SQL Server crée une base de données de distribution et un journal**, puis cliquez sur **Suivant**.  

5.  Dans la page **Dossier d’instantanés**, dans la section **Préparation de la réplication SQL Server**, entrez le chemin UNC vers le dossier d’instantanés créé.  

6.  Dans la page **Base de données de distribution**, cliquez sur **Suivant**.  

7.  Dans la page **Serveurs de publication**, cliquez sur le serveur de déploiement principal pour le définir comme serveur de distribution, puis cliquez sur **Suivant**.  

8.  Dans la page **Actions de l’Assistant**, cliquez sur **Configurer la distribution**, puis cliquez sur **Suivant**.  

9. Cliquez sur **Terminer**, puis cliquez sur **Fermer** quand l’Assistant est terminé.  

#### <a name="enable-the-mdt-db-for-replication"></a>Activer la base de données MDT pour la réplication  
 Pour activer la base de données MDT pour la réplication sur le serveur de déploiement principal, effectuez les étapes suivantes :  

1.  Dans SQL Server Management Studio, cliquez avec le bouton droit sur le nœud **Réplication**, puis cliquez sur **Propriétés du serveur de publication**.  

2.  Dans la page **Propriétés du serveur de publication**, effectuez ces étapes :  

    1.  Cliquez sur **Bases de données du serveur de publication**.  

    2.  Cliquez sur la base de données MDT, puis cliquez sur **Transactionnel**.  

    3.  Cliquez sur **OK**.  

 La base de données MDT est maintenant configurée pour la réplication transactionnelle et d’instantané.  

#### <a name="create-a-publication-of-the-mdt-db"></a>Créer une publication de la base de données MDT  
 Pour créer une publication de la base de données MDT à laquelle les serveurs de déploiement enfants peuvent s’abonner, effectuez les étapes suivantes :  

1.  Dans SQL Server Management Studio, développez Réplication, cliquez sur **Publications locales**, puis cliquez sur **Nouvelle publication**.  

2.  Dans l’Assistant Nouvelle publication, cliquez sur **Suivant**.  

3.  Dans la page **Base de données de publication**, cliquez sur la base de données MDT, puis cliquez sur **Suivant**.  

4.  Dans la page **Type de publication**, cliquez sur **Publication d’instantané**, puis cliquez sur **Suivant**.  

5.  Dans la page **Articles**, sélectionnez toutes les **Tables, procédures stockées** et **vues**, puis cliquez sur **Suivant**.  

6.  Dans la page **Problèmes d’article**, cliquez sur **Suivant**.  

7.  Dans la page **Filtrer les lignes de la table**, cliquez sur **Suivant**.  

8.  Dans la page **Agent d’instantané**, effectuez ces étapes :  

    1.  Sélectionnez **Créer un instantané immédiatement et garder ce dernier disponible pour l’initialisation des abonnements**.  

    2.  Cliquez sur **Planifier l’exécution de l’Agent d’instantané aux heures suivantes**.  

    3.  Cliquez sur **Modifier**.  

    > [!NOTE]
    >  Spécifiez une planification qui se produit une heure avant la réplication de la base de données.  

9. Cliquez sur **Suivant**.  

10. Dans la page **Sécurité de l’Agent**, cliquez sur le compte sous lequel l’Agent d’instantané doit s’exécuter, puis cliquez sur **Suivant**.  

11. Dans la page **Actions de l’Assistant**, cliquez sur **Créer la publication**, puis cliquez sur **Suivant**.  

12. Dans la page **Terminer l’Assistant**, dans la zone **Nom de la publication**, entrez un nom décrivant la publication.  

13. Cliquez sur **Terminer** pour terminer l’Assistant, puis cliquez sur **Fermer** quand l’Assistant a créé la publication.  

    > [!NOTE]
    >  La publication est désormais visible sous le nœud Publications locales dans SQL Server Management Studio.  

#### <a name="subscribe-child-deployment-servers-to-the-published-mdt-db"></a>Abonner des serveurs de déploiement enfants à la base de données MDT publiée  
 Maintenant que la base de données MDT a été publiée, vous pouvez ajouter les serveurs de déploiement enfants comme abonnés à cette publication. Autrement dit, ils reçoivent une copie de la base de données selon une certaine planification : ainsi, lors d’un déploiement, les ordinateurs clients peuvent interroger une base de données locale au réseau, au lieu d’avoir recours au réseau étendu (WAN).  

 **Pour abonner des serveurs de déploiement enfants à la publication de la base de données MDT**  

1.  Dans SQL Server Management Studio, accédez à Réplication/Publications locales.  

2.  Cliquez avec le bouton droit sur la publication créée à la section précédente, puis cliquez sur **Nouveaux abonnements**.  

3.  Dans l’Assistant Nouveaux abonnements, cliquez sur **Suivant**.  

4.  Dans la page **Publication**, cliquez sur la publication créée à la section précédente.  

5.  Dans la page **Emplacement de l’Agent de distribution**, cliquez sur **Exécuter tous les Agents sur le serveur de distribution NOM_SERVEUR (abonnements par envoi (push))**, puis cliquez sur **Suivant**.  

6.  Dans la page **Abonnés**, ajoutez chacun des serveurs de déploiement enfants en effectuant les étapes suivantes :  

    1.  Cliquez sur **Ajouter un abonné**, puis cliquez sur **Ajouter un abonné SQL Server**.  

    2.  Ajoutez chaque serveur de déploiement enfant.  

    3.  Pour chaque serveur de déploiement enfant ajouté, dans la zone **Base de données d’abonnement**, cliquez sur la base de données MDT vide sur ce serveur de déploiement enfant.  

    > [!NOTE]
    >  Si la base de données MDT vide n’a pas encore été créée, dans la zone **Base de données d’abonnement**, sélectionnez l’option de création d’une base de données.  

    > [!NOTE]
    >  Cette base de données doit avoir le même nom que la base de données MDT sur le serveur de déploiement principal. Par exemple, si la base de données MDT sur le serveur de déploiement principal est nommée *MDTDB*, créez une base de données vide nommée *MDTDB* sur le serveur de déploiement enfant.  

7.  Cliquez sur **Suivant**.  

8.  Dans la page **Sécurité de l’Agent de distribution**, cliquez sur **...** pour ouvrir la boîte de dialogue **Sécurité de l’Agent de distribution**.  

9. Entrez les détails du compte à utiliser pour l’Agent de distribution, puis cliquez sur **Suivant**.  

10. Dans la page **Planification de synchronisation**, effectuez ces étapes :  

    1.  Dans la zone **Planification de l’agent**, cliquez sur **<Définir la planification\>**.  

    2.  Spécifiez la planification qui doit être utilisée pour répliquer la base de données entre les serveurs de déploiement maître et enfants, puis cliquez sur **Suivant**.  

11. Dans la page **Initialiser l’abonnement**, cliquez sur **Suivant**.  

12. Dans la page **Actions de l’Assistant**, cliquez sur **Créer le ou les abonnements**, puis cliquez sur **Suivant**.  

13. Cliquez sur **Terminer**, puis cliquez sur **Fermer** quand l’Assistant se termine avec succès.  

 La réplication SQL Server est maintenant configurée, et la base de données MDT sera répliquée périodiquement du serveur de déploiement principal vers tous les serveurs de déploiement enfants qui y ont été abonnés.  

#### <a name="configure-customsettingsini"></a>Configurer CustomSettings.ini  
 L’infrastructure de déploiement avec installation LTI est maintenant créée, et chaque emplacement contiendra un serveur de déploiement avec installation LTI, avec une copie répliquée des éléments suivants :  

-   Le partage de déploiement  

-   La base de données MDT  

-   L’environnement Windows PE LiteTouchPE_x86 qui a été ajouté aux services de déploiement Windows  

 Vous pouvez maintenant configurer le fichier CustomSettings.ini pour que le partage de déploiement utilise le contenu du déploiement (partage et base de données de déploiement) à partir de son serveur de déploiement local, le serveur qui fournit l’environnement LiteTouchPE_x86.wim via les services de déploiement Windows.  

 Quand le fichier LiteTouchPE_x86.wim est fourni à partir des services de déploiement Windows, une clé de Registre est configurée avec le nom du serveur des services de déploiement Windows que vous utilisez. MDT capture ce nom de serveur dans une variable (%WDSServer%) que vous pouvez utiliser pour configurer CustomSettings.ini.  

 **Pour toujours utiliser le serveur de déploiement avec installation LTI local**  

> [!NOTE]
>  La procédure suivante suppose que le partage de déploiement a été créé et défini en tant que partage Deployment$.  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Cliquez sur l’onglet **Rules** (Règles), puis modifiez le fichier CustomSettings.ini pour y configurer les propriétés suivantes :  

    -   Pour chaque section SQL Server ajoutée, configurez **SQLServer** pour utiliser le nom du serveur **%WDSServer%**, par exemple **SQLServer=%WDSServer%**.  

    -   Si vous configurez **DeployRoot**, configurez-la pour utiliser la variable **%WDSServer%**, par exemple **DeployRoot=\\\\%WDSServer%\Deployment$**.  

5.  Cliquez sur **Edit Bootstrap.ini** (Modifier Bootstrap.ini).  

6.  Configurez BootStrap.ini pour utiliser la propriété **%WDSServer%** en ajoutant ou en modifiant la valeur de **DeployRoot** en **DeployRoot=\\\\%WDSServer%\Deployment$** .  

7.  Cliquez sur **File** (Fichier), puis cliquez sur **Save** (Enregistrer) pour enregistrer les modifications du fichier BootStrap.ini.  

8.  Cliquez sur **OK**.  

     Le partage de déploiement et l’environnement Windows PE LiteTouchPE_x86.wim doivent être mis à jour.  

9. Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

10. Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

11. Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

12. Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

 L’exemple suivant montre CustomSettings.ini après la réalisation des étapes décrites dans cette section.  

 **Exemple de fichier CustomSettings.ini configuré pour une infrastructure de déploiement avec installation LTI évolutive**  

```  
[Settings]  
Priority=CSettings,CPackages, CApps, CAdmins, CRoles, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  
ScanStateArgs=/v:5 /o /c  
LoadStateArgs=/v:5 /c /lac  

[CSettings]  
SQLServer=%WDSServer%  
Instance=  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerSettings  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CPackages]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerPackages  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CApps]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerApplications  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
Order=Sequence  

[CAdmins]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerAdministrators  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  

[CRoles]  
SQLServer=%WDSServer%  
Database=MDTDB  
Netlib=DBNMPNTW  
SQLShare=  
Table=ComputerRoles  
Parameters=UUID, AssetTag, SerialNumber, MacAddress  
ParameterCondition=OR  
```  

## <a name="selecting-a-local-mdt-server-when-multiple-servers-exist"></a>Sélection d’un serveur MDT local quand il existe plusieurs serveurs  
 Dans ce scénario, plusieurs serveurs MDT sont utilisés pour prendre en charge un volume élevé de déploiements simultanés et des déploiements sur plusieurs sites. Quand un déploiement avec installation LTI est initialisé, le comportement par défaut est de demander un chemin vers le serveur MDT auquel se connecter et d’accéder aux fichiers nécessaires pour commencer le processus de déploiement.  

 L’Assistant Windows Deployment (Déploiement Windows) peut utiliser le fichier LocalServer.xml pour présenter un choix de plusieurs serveurs de déploiement connus pour chaque emplacement.  

 Pour utiliser le fichier LocationServer.xml :  

-   Comprenez bien l’objectif et l’utilisation de LocationServer.xml, tels que décrits dans [Présentation de LocationServer.xml](#UnderstandingLocationServer)  

-   Créez le fichier LocationServer.xml comme décrit dans [Création du fichier LocationServer.xml](#CreateLocationServer)  

-   Ajoutez le fichier LocationServer.xml au répertoire Extra Files (Fichiers supplémentaires), comme décrit dans Ajout du fichier LocationServer.xml au répertoire Extra Files (Fichiers supplémentaires)  

-   Mettez à jour le fichier BootStrap.ini comme décrit dans [Mise à jour du fichier BootStrap.ini](#UpdateBootstrap)  

-   Mettez à jour le partage de déploiement comme décrit dans [Mise à jour du partage de déploiement](#UpdateDeploymentShare)  

 Ce scénario suppose que MDT est configuré sur un serveur de déploiement.  

###  <a name="UnderstandingLocationServer"></a> Présentation de LocationServer.xml  
 Vous devez d’abord comprendre comment MDT utilise LocationServer.xml. Lors d’une installation LTI, les scripts MDT lisent et traitent le fichier BootStrap.ini pour collecter des informations initiales sur le déploiement. Ceci se produit avant l’établissement d’une connexion au serveur de déploiement. Pour cela, la propriété **DeployRoot** est généralement utilisée pour spécifier dans le fichier BootStrap.ini à quel serveur de déploiement il doit établir une connexion.  

 Si le fichier BootStrap.ini ne contient pas de propriété **DeployRoot**, les scripts MDT chargent une page d’Assistant pour demander à l’utilisateur un chemin vers le serveur de déploiement. Lors de l’initialisation de la page de l’Assistant **HTML Application (HTA)** (Application HTML), les scripts MDT vérifient l’existence du fichier LocationServer.xml et, s’il existe, l’utilisent pour afficher les serveurs de déploiement disponibles.  

#### <a name="understand-when-to-use-locationserverxml"></a>Comprendre quand utiliser LocationServer.xml  
 MDT offre plusieurs moyens pour déterminer à quel serveur se connecter lors d’un déploiement avec installation LTI. Les différentes méthodes de localisation du serveur de déploiement peuvent être plus adaptées selon les différents scénarios. Il est donc important de comprendre quand utiliser LocationServer.xml.  

 MDT fournit plusieurs méthodes pour découvrir et utiliser automatiquement le serveur de déploiement le plus approprié. Ces méthodes sont répertoriées dans le tableau ci-dessous.

 |**Méthode** |**Détails** |  
 |-|-|  
 |**%WDSServer%** |Cette méthode est utilisée quand le serveur MDT est cohébergé sur le serveur des services de déploiement Windows.<br /><br /> Quand un déploiement avec installation LTI est lancé à partir des services de déploiement Windows, une variable d’environnement, %WDSServer%, est créée et contient le nom du serveur des services de déploiement Windows.<br /><br /> La variable **DeployRoot** peut utiliser cette variable pour se connecter automatiquement à un partage de déploiement sur le serveur des services de déploiement Windows, par exemple :<br /><br /> **DeployRoot=\\\\%WDSServer%\Deployment$** |  
 |**Automatisation basée sur l’emplacement** |MDT peut utiliser l’automatisation basée sur l’emplacement dans le fichier BootStrap.ini pour déterminer le serveur sur lequel il doit déployer.<br /><br /> Utilisez la propriété **Default Gateway** pour faire la distinction entre les différents emplacements : pour chaque propriété **Default Gateway**, un serveur MDT différent est spécifié.<br /><br /> Pour plus d’informations sur l’utilisation de l’automatisation basée sur l’emplacement, consultez « Sélection des méthodes pour l’application des paramètres de configuration ».|  

 Chaque approche répertoriée dans le tableau précédent offre un moyen d’automatiser la sélection du serveur de déploiement à un emplacement donné pour certains scénarios. Ces approches sont destinées à des scénarios spécifiques, par exemple quand le serveur MDT est cohébergé avec les services de déploiement Windows.  

 Il existe d’autres scénarios dans lesquels ces approches ne conviennent pas, par exemple s’il existe plusieurs serveurs de déploiement à un emplacement donné ou si la logique d’automatisation n’est pas possible (par exemple si le réseau n’est pas suffisamment segmenté pour permettre la détermination de l’emplacement ou si le serveur MDT est séparé des services de déploiement Windows).  

 Dans ces scénarios, le fichier LocationServer.xml constitue un moyen souple pour présenter ces informations au moment du déploiement, sans devoir connaître les noms des serveurs et les noms des partages de déploiement.  

###  <a name="CreateLocationServer"></a> Création du fichier LocationServer.xml  
 Pour présenter une liste de serveurs de déploiement disponibles lors d’un déploiement avec installation LTI, créez un fichier LocationServer.xml qui contient des informations sur chaque serveur. Il n’existe pas de fichier LocationServer.xml par défaut dans MDT : vous devez donc le créer en suivant les instructions ci-dessous.  

#### <a name="create-a-locationserverxml-file-to-support-multiple-locations"></a>Créer un fichier LocationServer.xml pour prendre en charge plusieurs emplacements  
 La méthode la plus simple pour créer et utiliser LocationServer.xml consiste à créer ce fichier et à y ajouter des entrées pour chaque serveur de déploiement de l’environnement (au même emplacement ou à des emplacements différents).  

 Construisez le fichier LocationServer.xml en créant une section pour chaque serveur et en ajoutant les informations suivantes :  

-   Un identificateur unique  

-   Un nom d’emplacement, utilisé pour présenter un nom facilement identifiable de cet emplacement  

-   Un chemin UNC du serveur MDT pour cet emplacement  

 Ce qui suit illustre la façon dont le fichier LocationServer.xml est créé en utilisant chacune de ces propriétés avec un exemple de fichier LocationServer.xml configuré pour plusieurs emplacements.  

 **Exemple de fichier LocationServer.xml pour la prise en charge plusieurs emplacements**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 En utilisant ce format, spécifiez différentes entrées de serveur pour chaque emplacement, ou dans les situations où il existe plusieurs serveurs à un même emplacement en spécifiant une entrée de serveur différente pour chaque serveur à cet emplacement, comme indiqué dans l’exemple suivant.   

 **Exemple de fichier LocationServer.xml pour la prise en charge de plusieurs serveurs à plusieurs emplacements**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ DS1, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS01\Deployment$</UNCPath>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso HQ DS2, Seattle, USA  
        </friendlyname>  
        <UNCPath>\\STLDS02\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

#### <a name="create-a-locationserverxml-file-to-load-balance-multiple-servers-at-different-locations"></a>Créer un fichier LocationServer.xml pour équilibrer la charge de plusieurs serveurs situés à des emplacements différents  
 Dans LocationServer.xml, spécifiez plusieurs serveurs par entrée d’emplacement, puis effectuez un équilibrage de charge de base de façon que, quand un emplacement est choisi, MDT sélectionne automatiquement un serveur de déploiement dans la liste des serveurs disponibles. Pour la mise en œuvre de cette fonctionnalité, le fichier LocationServer.xml prend en charge la spécification d’une métrique de pondération.  

 L’exemple suivant montre un exemple de fichier LocationServer.xml configuré pour plusieurs serveurs situés à des emplacements différents.  

 **Exemple de fichier LocationServer.xml pour différents emplacements**  

```  
<?xml version="1.0" encoding="utf-8" ?>  
<servers>  
    <QueryDefault></QueryDefault>  
    <server>  
        <serverid>1</serverid>  
        <friendlyname>  
          Contoso HQ, Seattle, USA  
        </friendlyname>  
        <Server1>\\STLDS01\Deployment$</Server1>  
        <Server2>\\STLDS02\Deployment$</Server2>  
        <Server3>\\STLDS03\Deployment$</Server3>  
        <Server weight=”1”>\\STLDS01\Deployment$</Server>  
        <Server weight=”2”>\\STLDS02\Deployment$</Server>  
        <Server weight=”4”>\\STLDS03\Deployment$</Server>  
    </server>  
    <server>  
        <serverid>2</serverid>  
        <friendlyname>  
          Contoso NYC, New York, USA  
        </friendlyname>  
        <UNCPath>\\NYCDS01\Deployment$</UNCPath>  
    </server>   
</servers>  
```  

 Spécifiez la métrique de pondération avec la balise <server weight\>, qui est utilisée par MDT dans le processus de sélection du serveur. La probabilité qu’un serveur soit sélectionné est calculée comme ceci :  

 **Poids du serveur/somme de tous les poids des serveurs**  

 Dans l’exemple précédent, les trois serveurs du siège social de Contoso apparaissent avec les pondérations 1, 2 et 4. La probabilité qu’un serveur avec un poids de 2 soit sélectionné est de 2 sur 7. Par conséquent, pour utiliser le système de pondération, déterminez la capacité des serveurs disponibles à un emplacement et pondérez chaque serveur avec sa capacité relativement à chacun des autres serveurs.  

### <a name="adding-the-locationserverxml-file-to-the-extra-files-directory"></a>Ajout du fichier LocationServer.xml dans le répertoire Extra Files (Fichiers supplémentaires)  
 Après avoir créé le fichier LocationServer.xml, ajoutez-le aux images de démarrage Windows PE LiteTouch_x86 et LiteTouch_x64 dans le dossier ***X:\\Deploy\Control***. Avec Deployment Workbench, ajoutez d’autres fichiers et dossiers à ces images Windows PE en spécifiant un répertoire supplémentaire pour y ajouter les propriétés du partage de déploiement.  

 **Pour ajouter LocationServer.xml au partage de déploiement**  

1.  Créez un dossier nommé *Extra Files* dans le dossier du partage de déploiement racine (par exemple D:\Production Deployment Share\Extra Files).  

2.  Créez une structure de dossiers dans le dossier Extra Files qui reflète l’emplacement de Windows PE où le fichier supplémentaire doit se trouver.  

     Par exemple, le fichier LocationServer.xml doit se trouver dans le dossier \Deploy\Control dans Windows PE : créez donc la même structure de dossiers sous les Extra Files (par exemple D:\Production Deployment Share\Extra Files\Deploy\Control).  

3.  Copiez LocationServer.xml dans le dossier *partage_déploiement*\Extra Files\Deploy\Control (où *partage_déploiement* est le chemin complet du dossier racine du partage de déploiement).  

4.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

5.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

6.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

7.  Dans la boîte de dialogue ***partage_déploiement Properties*** (Propriétés de partage_déploiement) (où partage_déploiement est le nom du partage de déploiement), effectuez ces étapes :  

    1.  Cliquez sur l’onglet **Windows PE platform Settings** (Paramètres de la plateforme Windows PE) (où *plateforme* est l’architecture de l’image Windows PE à configurer).  

    2.  Dans la section **Windows PE Customizations** (Personnalisations de Windows PE), dans la zone **Extra directory to add** (Répertoire supplémentaire à ajouter), tapez ***chemin*** (où *chemin* est le nom complet du chemin du dossier Extra Files, par exemple D:\Production Deployment Share\Extra Files), puis cliquez sur **OK**.  

###  <a name="UpdateBootstrap"></a> Mise à jour du fichier BootStrap.ini  
 Quand vous créez un partage de déploiement avec Deployment Workbench, une propriété **DeployRoot** est automatiquement créée et remplie dans le fichier BootStrap.ini. Comme le fichier LocationServer.xml est utilisé pour remplir la propriété **DeployRoot**, vous devez supprimer cette valeur du fichier BootStrap.ini.  

 **Pour supprimer la propriété DeployRoot dans BootStrap.ini**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Dans la boîte de dialogue ***partage_déploiement Properties*** (Propriétés de partage_déploiement) (où *partage_déploiement* est le nom du partage de déploiement), cliquez sur l’onglet **Rules** (Règles), puis cliquez sur **Edit BootStrap.ini** (Modifier BootStrap.ini).  

5.  Supprimez la valeur de **DeployRoot** (par exemple **DeployRoot=\\\Server\Deployment$**).  

6.  Cliquez sur **File** (Fichier), puis cliquez sur **Save** (Enregistrer) pour enregistrer les modifications du fichier BootStrap.ini.  

7.  Cliquez sur **OK** pour valider les modifications.  

###  <a name="UpdateDeploymentShare"></a> Mise à jour du partage de déploiement  
 Le partage de déploiement doit ensuite être mis à jour pour générer un nouvel environnement de démarrage LiteTouch_x86 et LiteTouch_x64 qui contient le fichier LocationServer.xml et le fichier BootStrap.ini mise à jour.  

 **Pour mettre à jour le partage de déploiement**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement* (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

4.  Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

5.  Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

6.  Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

> [!NOTE]
>  Une fois le processus de mise à jour terminé, ajoutez les nouveaux environnements Windows PE LiteTouch_x86 et LiteTouch_x64 aux Services de déploiement Windows, ou gravez-les sur un support de démarrage à utiliser pendant le déploiement.  

## <a name="replacing-an-existing-computer-with-a-new-computer-using-lite-touch-installation"></a>Remplacement d’un ordinateur existant par un nouvel ordinateur à l’aide de l’installation LTI  
 Vous pouvez utiliser MDT pour déployer une image sur un nouvel ordinateur destiné à remplacer un ordinateur existant dans l’architecture de l’entreprise. Cette situation peut se produire pendant une mise à niveau depuis un système d’exploitation vers un autre (un nouveau système d’exploitation peut nécessiter un nouveau matériel) ou si l’organisation a besoin d’ordinateurs plus récents et plus rapides pour les applications existantes.  

 Pendant le remplacement d’un ordinateur existant par un nouvel ordinateur, Microsoft vous recommande de prendre en compte tous les paramètres qui sont migrés depuis un ordinateur vers un autre, tels que les comptes d’utilisateur et les données d’état utilisateur. En outre, il est important de créer une solution de récupération en cas d’échec de la migration.  

 Dans cet exemple de déploiement, remplacez l’ordinateur existant (WDG-EXIST-01) par un nouvel ordinateur (WDG-NEW-02) dans le domaine CORP en capturant les données d’état utilisateur à partir de WDG-EXIST-01 et en les enregistrant sur un partage réseau. Ensuite, déployez une image existante sur WDG-NEW-02 et, enfin, restaurez les données d’état utilisateur capturées sur WDG-NEW-02. Le déploiement est effectué à partir d’un serveur de déploiement (WDG-MDT-01).  

 Dans MDT, utilisez le modèle Standard Client Replace Task Sequence (Séquence de tâches Remplacer un client standard) pour créer une séquence de tâches qui effectue toutes les tâches de déploiement nécessaires.  

 Cette démonstration suppose les points suivants :  

-   MDT a été installé sur le serveur de déploiement (WDG MDT 01).  

-   Le partage de déploiement a déjà été créé et rempli, y compris les images de système d’exploitation, les applications et des pilotes de périphérique.  

-   Une image d’un ordinateur de référence a déjà été capturée et sera déployée sur le nouvel ordinateur (WDG NEW 02).  

-   Un dossier de partage réseau (UserStateCapture$) a été créé et partagé sur le serveur de déploiement (WDG MDT 01) avec les autorisations de partage appropriées.  

 Un partage de déploiement doit exister avant que vous ne commenciez cet exemple. Pour plus d’informations sur la création d’un partage de déploiement, consultez la section « Managing Deployment Shares in the Deployment Workbench » (Gestion de partages de déploiement dans Deployment Workbench) du document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

### <a name="step-1-create-a-task-sequence-to-capture-the-user-state"></a>Étape 1 : Créer une séquence de tâches pour capturer l’état utilisateur  
 Créez des séquences de tâches MDT dans le nœud Task Sequences (Séquences de tâches) de Deployment Workbench à l’aide de l’Assistant Nouvelle séquence de tâches. Pour effectuer la première partie du scénario de déploiement de remplacement d’un ordinateur (capture de l’état utilisateur sur l’ordinateur existant), sélectionnez le modèle Standard Client Replace Task Sequence (Séquence de tâches Remplacer un client standard) dans l’Assistant Nouvelle séquence de tâches.  

 **Pour créer une séquence de tâches afin de capturer l’état utilisateur dans le scénario de déploiement de remplacement d’un ordinateur**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **New Task Sequence** (Nouvelle séquence de tâches).  

     L’Assistant Nouvelle séquence de tâches démarre.  

4.  Exécutez l’Assistant Nouvelle séquence de tâches en utilisant les informations suivantes. Acceptez les valeurs par défaut, sauf indication contraire.  

    |**Sur cette page de l’Assistant** |**Faites cela** |  
    |-|-|  
    |**General Settings** (Paramètres généraux) |1.  Dans **Task sequence ID** (ID de séquence de tâches), tapez **VISTA_EXIST**.<br />2.  Dans **Task sequence name** (Nom de séquence de tâches), tapez **Effectuer le scénario de remplacement d’un ordinateur sur un ordinateur existant**.<br />3.  Cliquez sur **Suivant**.|  
    |**Select Template** (Sélectionner un modèle) |Dans **The following task sequence templates are available**. **Select the one you would like to use as a starting point** (Les modèles de séquence de tâches suivants sont disponibles. Sélectionnez celui que vous souhaitez utiliser comme point de départ), sélectionnez **Standard Client Replace Task Sequence** (Séquence de tâches Remplacer un client standard), puis cliquez sur **Next** (Suivant).|  
    |**Résumé** |Vérifiez que les informations sur la configuration sont correctes, puis cliquez sur **Next** (Suivant).|  
    |**Confirmation** |Cliquez sur **Terminer**.|  

 L’Assistant Nouvelle séquence de tâches se termine et la séquence de tâches **VISTA_EXIST** est ajoutée à la liste des séquences de tâches.  

### <a name="step-2-create-a-task-sequence-to-deploy-operating-system-and-restore-the-user-state"></a>Étape 2 : Créer une séquence de tâches pour déployer le système d’exploitation et restaurer l’état utilisateur  
 Créez des séquences de tâches MDT dans le nœud Task Sequences (Séquences de tâches) de Deployment Workbench à l’aide de l’Assistant Nouvelle séquence de tâches. Pour effectuer la seconde partie du scénario de déploiement de remplacement d’un ordinateur (déploiement du système d’exploitation, puis restauration de l’état utilisateur sur l’ordinateur existant), sélectionnez le modèle Standard Client Task Sequence (Séquence de tâches Client standard) dans l’Assistant Nouvelle séquence de tâches.  

 **Pour créer une séquence de tâches afin de déployer l’état utilisateur dans le scénario de déploiement de remplacement d’un ordinateur**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **New Task Sequence** (Nouvelle séquence de tâches).  

     L’Assistant Nouvelle séquence de tâches démarre.  

4.  Exécutez l’Assistant Nouvelle séquence de tâches en utilisant les informations suivantes. Acceptez les valeurs par défaut, sauf indication contraire.  

    |**Sur cette page de l’Assistant**|**Faites cela**|  
    |-|-|  
    |**General Settings** (Paramètres généraux)|1.  Dans **Task sequence ID** (ID de séquence de tâches), tapez **VISTA_NEW**.<br />2.  Dans **Task sequence name** (Nom de séquence de tâches), tapez **Effectuer le scénario de remplacement d’un ordinateur sur un nouvel ordinateur**.<br />3.  Cliquez sur **Suivant**.|  
    |**Select Template** (Sélectionner un modèle)|Dans **The following task sequence templates are available**. **Select the one you would like to use as a starting point** (Les modèles de séquence de tâches suivants sont disponibles. Sélectionnez celui que vous souhaitez utiliser comme point de départ), sélectionnez **Standard Client Task Sequence** (Séquence de tâches Client standard), puis cliquez sur **Next** (Suivant).|  
    |**Select OS** (Sélectionner le système d’exploitation)|Dans **The following operating system images are available to be deployed with this task sequence** (Les images de système d’exploitation suivantes peuvent être déployées avec cette séquence de tâches), sélectionnez celle à utiliser, sélectionnez ***image_vista_capturée*** (où *image_vista_capturée* est l’image capturée que l’ordinateur de référence a ajoutée au nœud Operating Systems (Systèmes d’exploitation) dans Deployment Workbench), puis cliquez sur *Next* (Suivant).|  
    |**Specify Product Key** (Spécifier la clé de produit)|Sélectionnez **Do not specify a product key at this time** (Ne pas spécifier de clé de produit pour l’instant), puis cliquez sur **Next** (Suivant).|  
    |OS Settings (Paramètres du système d’exploitation)|1.  Dans **Full Name** (Nom complet), tapez **Woodgrove Employee**.<br />2.  Dans **Organization** (Organisation), tapez **Woodgrove Bank**.<br />3.  Dans **Internet Explorer Home Page** (Page d’accueil Internet Explorer), tapez **http://www.woodgrovebank.com**.<br />4.  Cliquez sur **Suivant**.|  
    |**Admin Password** (Mot de passe administrateur)|Dans **Administrator Password** (Mot de passe administrateur) et **Please confirm Administrator Password** (Confirmez le mot de passe administrateur), tapez **P@ssw0rd**, puis cliquez sur **Finish** (Terminer).|  
    |**Confirmation**|Cliquez sur **Terminer**.|  

 L’Assistant Nouvelle séquence de tâches se termine et la séquence de tâches **VISTA_NEW** est ajoutée à la liste des séquences de tâches.  

### <a name="step-3-customize-the-mdt-configuration-files"></a>Étape 3 : Personnaliser les fichiers de configuration MDT  
 Une fois la séquence de tâches MDT créée, personnalisez les fichiers de configuration MDT qui contiennent les paramètres de configuration de la capture des informations d’état utilisateur. Plus précisément, personnalisez le fichier CustomSettings.ini au niveau des propriétés du partage de déploiement créé précédemment dans le processus de déploiement. À une étape ultérieure, le partage de déploiement sera mis à jour pour que le fichier de configuration soit mis à jour dans le partage de déploiement.  

 **Pour personnaliser les fichiers de configuration MDT afin de capturer les informations d’état utilisateur**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

     La boîte de dialogue **Properties** (Propriétés) s’affiche.  

4.  Dans la boîte de dialogue **Properties** (Propriétés), cliquez sur l’onglet **Rules** (Règles).  

5.  Sous l’onglet **Rules** (Règles), modifiez le fichier CustomSettings.ini afin qu’il reflète les modifications nécessaires, comme indiqué dans l’exemple suivant. Apportez toute modification supplémentaire que nécessite l’environnement.  

     **Fichier CustomSettings.ini personnalisé**  

    ```  
    [Settings]  
    Priority=Default  
    Properties=MyCustomProperty  

    [Default]  
    OSInstall=Y  

    UDShare=\\WDG-MDT-01\UserStateCapture$  
    UDDir=%OSDCOMPUTERNAME%  
    UserDataLocation=NETWORK  
    SkipCapture=NO  
    SkipAdminPassword=YES  
    SkipProductKey=YES  

    ```  

6.  Dans la boîte de dialogue **Properties** (Propriétés), cliquez sur **OK**.  

7.  Fermez toutes les fenêtres et boîtes de dialogue.  

### <a name="step-4-configure-the-windows-pe-options-for-the-deployment-share"></a>Étape 4 : Configurer les options Windows PE pour le partage de déploiement  
 Configurez les options Windows PE pour le partage de déploiement dans le nœud Deployment Shares (Partages de déploiement) dans Deployment Workbench.  

> [!NOTE]
>  Si les pilotes de périphérique pour l’ordinateur existant (WDG-EXIST-01) et le nouvel ordinateur (WDG-NEW-01) sont inclus dans Windows Vista, ignorez cette étape et passez à l’étape suivante.  

 **Pour configurer les options Windows PE pour le partage de déploiement**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

     La boîte de dialogue **Properties** (Propriétés) s’affiche.  

4.  Dans la boîte de dialogue **Properties** (Propriétés), sous l’onglet **Windows PE *plateforme* Components** (Composants de la plateforme Windows PE) (où *plateforme* est l’architecture de l’image Windows Image PE à configurer), dans **Selection profile** (Profil de sélection), sélectionnez ***pilotes_de_périphérique*** (où *pilotes_de_périphérique* est le nom du profil de sélection des pilotes de périphérique), puis cliquez sur **OK**.  

### <a name="step-5-update-the-deployment-share"></a>Étape 5 : Mettre à jour le partage de déploiement  
 Après avoir configuré les options Windows PE pour le partage de déploiement, mettez à jour ce dernier. La mise à jour du partage de déploiement met à jour tous les fichiers de configuration MDT et génère une version personnalisée de Windows PE. La version personnalisée de Windows PE est utilisée pour démarrer l’ordinateur de référence et lancer le processus de déploiement LTI.  

 **Pour mettre à jour le partage de déploiement dans Deployment Workbench**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement* (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Update DeploymentShare** (Mettre à jour le partage de déploiement).  

     L’Assistant Mise à jour de partage de déploiement démarre.  

4.  Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

5.  Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

6.  Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

 Deployment Workbench démarre la mise à jour du partage de déploiement. Deployment Workbench crée les fichiers LiteTouchPE_x86.iso et LiteTouchPE_x86.wim (pour les ordinateurs cibles 32 bits) ou les fichiers LiteTouchPE_x64.iso et LiteTouchPE_x64.wim (pour les ordinateurs cibles 64 bits) dans le dossier *partage_déploiement*\Boot (où *partage_déploiement* est le dossier partagé utilisé en tant que partage de déploiement).  

### <a name="step-6-create-the-lti-bootable-media"></a>Étape 6 : Créer le support démarrable LTI  
 Indiquez une méthode pour démarrer l’ordinateur avec la version personnalisée de Windows PE créée pendant la mise à jour du partage de déploiement. Deployment Workbench crée les fichiers LiteTouchPE_x86.iso et LiteTouchPE_x86.wim (pour les ordinateurs cibles 32 bits) ou les fichiers LiteTouchPE_x64.iso et LiteTouchPE_x64.wim (pour les ordinateurs cibles 64 bits) dans le dossier *partage_déploiement*\Boot (où *partage_déploiement* est le dossier partagé utilisé en tant que partage de déploiement). Créez le support démarrable LTI approprié à partir d’une de ces images.  

 **Pour créer le support démarrable LTI**  

1.  Dans l’Explorateur Windows, accédez au dossier *partage_déploiement*\Boot (où *partage_déploiement* est le dossier partagé utilisé en tant que partage de déploiement).  

2.  Selon le type d’ordinateur utilisé pour l’ordinateur existant (WDG-EXIST-01) et le nouvel ordinateur (WDG-NEW-02), effectuez l’une des tâches suivantes :  

    -   Si l’ordinateur de référence est un ordinateur physique, créez un CD ou DVD du fichier ISO.  

    -   Si l’ordinateur de référence est une machine virtuelle, démarrez celle-ci directement à partir du fichier ISO ou à partir d’un CD ou DVD du fichier ISO.  

### <a name="step-7-start-the-existing-computer-with-the-lti-bootable-media"></a>Étape 7 : Démarrer l’ordinateur existant avec le support démarrable LTI  
 Démarrez l’ordinateur existant (WDG-EXIST-01) avec le support démarrable LTI créé plus tôt dans le processus. Ce CD démarre Windows PE sur l’ordinateur existant et lance le processus de déploiement MDT. À la fin du processus de déploiement MDT, les informations de la migration de l’état utilisateur sont stockées dans le dossier partagé UserStateCapture$.  

> [!NOTE]
>  Vous pouvez également lancer le processus MDT en démarrant l’ordinateur cible à partir des Services de déploiement Windows. Pour plus d’informations, consultez la section « Preparing Windows Deployment Services » (Préparation des Services de déploiement Windows) dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

 **Pour démarrer l’ordinateur existant avec le support démarrable LTI**  

1.  Démarrez WDG-EXIST-01 avec le support démarrable LTI créé plus tôt dans le processus.  

     Windows PE démarre, puis l’Assistant de déploiement Windows.  

2.  Exécutez l’Assistant de déploiement Windows en utilisant les informations suivantes. Acceptez les valeurs par défaut, sauf indication contraire.  

    |**Sur cette page de l’Assistant**|**Faites cela**|  
    |-|-|  
    |**Welcome to Deployment** (Bienvenue dans l’Assistant de déploiement)|Cliquez sur **Run the Deployment Wizard** (Exécuter l’Assistant de déploiement) pour installer un nouveau système d’exploitation, puis cliquez sur **Next** (Suivant).|  
    |**Specify Credentials for connecting to network shares.** (Spécifiez les informations d’identification pour se connecter aux partages réseau.)|1.  Dans **User Name** (Nom d’utilisateur), tapez **Administrator** (Administrateur).<br />2.  Dans **Password** (Mot de passe), tapez **P@ssw0rd**.<br />3.  Dans **Domain** (Domaine), tapez **CORP**.<br />4.  Cliquez sur **OK**.|  
    |**Select a task sequence to execute on this computer.** (Sélectionnez une séquence de tâches à exécuter sur cet ordinateur.)|Cliquez sur *Effectuer le scénario de remplacement d’un ordinateur sur un ordinateur existant*, puis sur **Next** (Suivant).|  
    |**Specify where to save your data and settings** (Spécifiez l’emplacement auquel enregistrer vos données et paramètres.)|Cliquez sur **Suivant**.|  
    |**Specify where to save a complete computer backup** (Spécifiez l’emplacement auquel enregistrer une sauvegarde d’ordinateur complète.)|Cliquez sur **Do not back up the existing computer** (Ne pas sauvegarder l’ordinateur existant), puis cliquez sur **Next** (Suivant).|  
    |**Ready to begin** (Prêt à démarrer)|Cliquez sur **Begin** (Démarrer).|  

     Si des erreurs ou avertissements se produisent, consultez le document MDT *Troubleshooting Reference* (Guide de dépannage).  

3.  Dans la boîte de dialogue **Deployment Summary** (Résumé du déploiement), cliquez sur **Details** (Détails).  

     Si des erreurs ou avertissements se sont produits, passez-les en revue et enregistrez les informations de diagnostic.  

4.  Dans la boîte de dialogue **Deployment Summary** (Résumé du déploiement), cliquez sur **Finish** (Terminer).  

 Les informations de la migration de l’état utilisateur sont capturées et sont stockées dans le dossier réseau partagé (UserStateCapture$) créé plus tôt dans le processus.  

### <a name="step-8-start-the-new-computer-with-the-lti-bootable-media"></a>Étape 8 : Démarrer le nouvel ordinateur avec le support démarrable LTI  
 Démarrez le nouvel ordinateur (WDG-NEW-02) avec le support démarrable LTI créé plus tôt dans le processus. Ce CD démarre Windows PE sur l’ordinateur de référence et lance le processus de déploiement MDT. À la fin du processus de déploiement MDT, Windows Vista est déployé sur le nouvel ordinateur, et les informations de la migration de l’état utilisateur capturées sont restaurées sur le nouvel ordinateur.  

> [!NOTE]
>  Vous pouvez également lancer le processus MDT en démarrant l’ordinateur cible à partir des Services de déploiement Windows. Pour plus d’informations, consultez la section « Preparing Windows Deployment Services » (Préparation des Services de déploiement Windows) du document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

 **Pour démarrer le nouvel ordinateur avec le support démarrable LTI**  

1.  Démarrez WDG-NEW-02 avec le support démarrable LTI créé plus tôt dans le processus.  

     Windows PE démarre, puis l’Assistant de déploiement Windows.  

2.  Effectuez l’Assistant de déploiement Windows en utilisant les informations suivantes. Acceptez les valeurs par défaut, sauf indication contraire.  

    |**Sur cette page de l’Assistant**|**Faites cela**|  
    |--|--|
    |**Welcome to Deployment** (Bienvenue dans l’Assistant de déploiement)|Cliquez sur **Run the Deployment Wizard** (Exécuter l’Assistant de déploiement) pour installer un nouveau système d’exploitation, puis cliquez sur **Next** (Suivant).|  
    |**Specify Credentials for connecting to network shares.** (Spécifiez les informations d’identification pour se connecter aux partages réseau.)|1.  Dans **User Name** (Nom d’utilisateur), tapez **Administrator** (Administrateur).<br />2.  Dans **Password** (Mot de passe), tapez **P@ssw0rd**.<br />3.  Dans **Domain** (Domaine), tapez **CORP**.<br />4.  Cliquez sur **OK**.|  
    |**Select a task sequence to execute on this computer.** (Sélectionnez une séquence de tâches à exécuter sur cet ordinateur.)|Cliquez sur **Effectuer le scénario de remplacement d’un ordinateur sur un nouvel ordinateur**, puis sur **Next** (Suivant).|  
    |**Configure the computer name** (Configurez le nom d’ordinateur.)|Dans **Computer name** (Nom de l’ordinateur), tapez **WDG-NEW-02**, puis cliquez sur **Next** (Suivant).|  
    |**Join the computer to a domain or workgroup** (Joignez l’ordinateur à un domaine ou à un groupe de travail.)|Cliquez sur **Suivant**.|  
    |**Specify whether to restore user data** (Indiquez si vous souhaitez restaurer les données utilisateur.)|1.  Cliquez sur **Specify a location** (Spécifier un emplacement).<br />2.  Dans **Location** (Emplacement), tapez **\\\WDG-MDT-01\UserStateCapture$\WDG-EXIST-01**.<br />3.  Cliquez sur **Suivant**.|  
    |**Locale Selection** (Sélectionnez les paramètres régionaux.)|Cliquez sur **Suivant**.|  
    |**Set the Time Zone** (Définissez le fuseau horaire.)|Cliquez sur **Suivant**.|  
    |**Specify whether to capture an image** (Spécifiez s’il faut capturer une image.)|Cliquez sur **Do not capture an image of this computer** (Ne pas capturer une image de cet ordinateur), puis cliquez sur **Next** (Suivant).|  
    |**Specify the BitLocker configuration** (Spécifiez la configuration de BitLocker)|Cliquez sur **Do not enable BitLocker for this computer** (Ne pas activer BitLocker pour cet ordinateur), puis cliquez sur **Next** (Suivant).|  
    |**Ready to begin** (Prêt à démarrer)|Cliquez sur **Begin** (Démarrer).|  

     Si des erreurs ou avertissements se produisent, consultez le document MDT *Troubleshooting Reference* (Guide de dépannage).  

3.  Dans la boîte de dialogue **Deployment Summary** (Résumé du déploiement), cliquez sur **Details** (Détails).  

     Si des erreurs ou avertissements se sont produits, passez-les en revue et enregistrez les informations de diagnostic.  

4.  Dans la boîte de dialogue **Deployment Summary** (Résumé du déploiement), cliquez sur **Finish** (Terminer).  

 Windows Vista est maintenant installé sur le nouvel ordinateur et les informations de la migration de l’état utilisateur capturées sont également restaurées.  

## <a name="integrating-custom-deployment-code-into-mdt"></a>Intégration de code de déploiement personnalisé à MDT  
 Il est courant qu’une équipe de déploiement ait des exigences complexes, propres à son environnement cible, qui ne sont pas satisfaites par les actions prédéfinies de la séquence de tâches Deployment Workbench ou par les fichiers de configuration MDT par défaut. Implémenter un code personnalisé est alors nécessaire.  

 Intégrer du code de déploiement personnalisé à MDT implique les étapes suivantes :  

-   Choisir un langage de script, comme décrit dans [Choix du langage de script approprié](#ChooseAppropLanguage)  

-   Tirer parti de ZTIUtility.vbs, comme décrit dans [Comprendre comment tirer parti de ZTIUtility](#UnderstandLeverageZTI)  

-   Intégrer du code de déploiement personnalisé, comme décrit dans [Intégration de code de déploiement personnalisé](#IntegrateCustomDeploy)  

 Les sections suivantes supposent que MDT est configuré sur un serveur de déploiement.  

###  <a name="ChooseAppropLanguage"></a> Choix du langage de script approprié  
 Bien que tout code exécutable sur Windows ou Windows PE puisse être appelé en tant qu’installation d’application ou par le biais d’une étape de séquence de tâches MDT, Microsoft recommande d’utiliser des scripts sous la forme de fichiers .vbs ou .wsf.  

 L’avantage d’utiliser des fichiers .wsf réside dans la journalisation intégrée, en plus de certaines autres fonctions prédéfinies déjà utilisées par les processus ZTI et LTI. Ces fonctions sont disponibles dans le script ZTIUtility distribué avec MDT.  

 Quand il est référencé à partir d’un script personnalisé, le script ZTIUtility initialise les classes d’environnement et de configuration MDT. Les classes disponibles sont les suivantes :  

-   **Logging**. Cette classe fournit les fonctionnalités de journalisation qu’utilisent tous les scripts MDT. En outre, elle crée un fichier journal unique pour chaque script exécuté pendant le déploiement et un fichier journal consolidé de tous les scripts. Ces fichiers journaux sont créés dans un format conçu pour être lu par TRACE32 ; cet outil est disponible dans le [kit de ressources System Center Configuration Manager 2007 V2 Toolkit](https://www.microsoft.com/download/en/details.aspx?id=9257).  

-   **Environment**. Cette classe configure les variables d’environnement collectées par le biais du traitement des règles WMI et MDT et leur permet d’être référencées directement à partir du script. Ainsi, les propriétés de déploiement peuvent être lues, donnant accès à toutes les informations de configuration utilisées par les processus ZTI et LTI.  

-   **Utility**. Cette classe fournit des utilitaires généraux qui sont utilisés dans les scripts ZTI et LTI. Microsoft vous recommande d’examiner cette classe chaque fois que vous développez du code personnalisé, car vous pourriez tout simplement réutiliser du code. Des informations supplémentaires sur certaines des fonctionnalités fournies dans cette classe sont incluses plus loin dans cette section.  

-   **Database**. Cette classe effectue des fonctions telles que la connexion aux bases de données et la lecture des informations dans les bases de données. En règle générale, il est déconseillé d’accéder directement à la classe de base de données ; il est préférable d’utiliser un traitement de règles pour effectuer des recherches dans une base de données.  

-   **Strings**. Cette classe effectue des routines de traitement de chaîne courantes telles que la création d’une liste d’éléments délimitée, l’affichage d’une valeur hexadécimale, la suppression des espaces blancs d’une chaîne, l’alignement à droite ou à gauche d’une chaîne, l’application d’un format de chaîne ou de tableau à une valeur, la génération d’un identificateur global unique (GUID) aléatoire et les conversions en Base64.  

-   **FileHandling**. Cette classe effectue des fonctions telles que la normalisation des chemins, ainsi que la copie, le déplacement et la suppression de fichiers et de dossiers.  

-   **clsRegEx**. Cette classe effectue des fonctions d’expression régulière.  

 Dans MDT, certaines modifications ont été apportées à l’architecture de script pour rendre le client Microsoft Visual Basic® Scripting Edition (VBScript) plus robuste et plus fiable. Ces modifications sont les suivantes :  

-   Modifications importantes apportées à ZTIUtility.vbs (bibliothèque de scripts principale), notamment de nouvelles API et une meilleure gestion des erreurs  

-   Une nouvelle structure globale des scripts ZTI_*xxx*.wsf  

 La structure globale des scripts MDT a également changé. La plupart des scripts MDT sont désormais encapsulés dans des objets VBScript **Class**. La classe est initialisée et appelée avec la fonction **RunNewInstance**.  

> [!NOTE]
>  Malgré les modifications importantes apportées à ZTIUtility.vbs, la plupart des scripts MDT 2008 Update 1 existants fonctionnent tels quels dans MDT, car la majeure partie des scripts MDT incluent ZTIUtility.vbs.  

###  <a name="UnderstandLeverageZTI"></a> Comprendre comment tirer parti de ZTIUtility  
 Le fichier ZTIUtility.vbs contient des classes d’objets que vous pouvez exploiter dans votre code personnalisé. Pour intégrer du code personnalisé à MDT, vous pouvez utiliser :  

-   La classe Logging définie dans ZTIUtility.vbs, comme décrit dans [Utiliser la classe Logging ZTIUtility](#UseZTILogging)  

-   La classe Environment définie dans ZTIUtility.vbs, comme décrit dans [Utiliser la classe Environment ZTIUtility](#UseZTIEnvironment)  

-   La classe Utility définie dans ZTIUtility.vbs, comme décrit dans [Utiliser la classe Utility ZTIUtility](#UseZTIUtility)  

####  <a name="UseZTILogging"></a> Utilisez la classe Logging ZTIUtility  
 La classe Logging dans ZTIUtiliy.vbs fournit un mécanisme simple qui permet à un code personnalisé de journaliser les erreurs, les avertissements et les informations d’état de la même manière que les autres scripts pendant un déploiement ZTI ou LTI. Cette standardisation garantit également que la boîte de dialogue **LTI Deployment Summary** (Résumé du déploiement LTI) indique l’état correct de tout code personnalisé exécuté.  

 Voici un exemple de script de code personnalisé qui utilise les fonctions **oLogging.CreateEntry** et **TestAndFail** pour journaliser différents types de messages, suivant les résultats des diverses actions de script.  

 **Exemple de script utilisant la classe ZTIUtility Logging : ZTI_Example.wsf**  

```  
<job id="ZTI_Example">  
<script language="VBScript" src="ZTIUtility.vbs"/>  
<script language="VBScript">  

' //*******************************************************  
' //  
' // Copyright (c) Microsoft Corporation.  All rights reserved  
' // Microsoft Deployment Toolkit Solution Accelerator  
' // File: ZTI_Example.wsf  
' //  
' // Purpose: Example of scripting with the  
' //          Microsoft Deployment Toolkit.  
' //  
' // Usage: cscript ZTI_Example.wsf [/debug:true]  
' //  
' //*******************************************************  

Option Explicit  
RunNewInstance  

'//--------------------------------------------------------  
'// Main Class  
'//--------------------------------------------------------  
Class ZTI_Example  

'//--------------------------------------------------------  
'// Main routine  
'//--------------------------------------------------------  

Function Main()  

  Dim iRetVal  
  Dim sScriptPath  

  iRetVal = SUCCESS  

  oLogging.CreateEntry "Begin example script…", _  
    LogTypeInfo  

  ' %ServerA% is a generic variable available within  
  ' every CustomSettings.ini file.  

  sScriptPath = "\\" & oEnvironment.Item("ServerA") & _  
    "\public\products\Applications\User\Technet\USEnglish"  

  ' Validate a connection to server, net connect with  
  ' credentials if necessary.  
  iRetVal = oUtility.ValidateConnection( sScriptPath )  
  TestAndFail iRetVal, 9991, "Validate Connection to [" & _  
    sScriptPath & "]"  

  'Run Setup Program  

  iRetVal = oUtility.RunWithHeartbeat( """" & _  
    sScriptPath & "\setup.exe"" /?" )  
  TestAndFail iRetVal, 9991, "RunWithHeartbeat [" & _  
    sScriptPath & "]"  

  'Perform any cleanup from installation process  

  oShell.RegWrite "HKLM\Software\Microsoft\SomeValue", _  
    "Done with Execution of XXX.", "REG_SZ"  

  Main = iRetVal  

End Function  

End Class  

</script>  
</job>  
```  

> [!NOTE]
>  Si vous souhaitez continuer à utiliser des scripts qui appellent **ZTIProcess()** avec **ProcessResults()**, vous pouvez le faire. Toutefois, certaines fonctionnalités de gestion des erreurs améliorées ne seront pas activées.  

####  <a name="UseZTIEnvironment"></a> Utiliser la classe Environment ZTIUtility  
 La classe Environment dans ZTIUtiliy.vbs fournit un accès aux propriétés MDT et permet de les mettre à jour. Dans l’exemple précédent, la portion de code **oEnvironment.Item("Memory")** est utilisée pour récupérer la quantité de mémoire RAM disponible ; elle permet également de récupérer la valeur de toutes les propriétés décrites dans le document MDT *Toolkit Reference* (Référence du Kit de ressources).  

####  <a name="UseZTIUtility"></a> Utiliser la classe Utility ZTIUtility  
 Le script ZTIUtility.vbs contient plusieurs utilitaires couramment utilisés dont peut tirer parti n’importe quel script de déploiement personnalisé. Vous pouvez ajouter ces utilitaires à n’importe quel script, à l’image des classes **oLogging** et **oEnvironment**.  

Le tableau suivant décrit certaines fonctions utiles disponibles et leur sortie. Pour obtenir la liste complète des fonctions disponibles, consultez le fichier ZTIUtility.vbs.  

|**Fonction**|**Sortie**|  
|-|-|
|**oUtility.LocalRootPath**|Retourne le chemin du dossier racine utilisé par le processus de déploiement sur l’ordinateur cible, par exemple, C:\MININT|  
|**oUtility.BootDevice**|Retourne le périphérique de démarrage système, par exemple, MULTI(0)DISK(0)RDISK(0)PARTITION(1)|  
|**oUtility.LogPath**|Retourne le chemin du dossier des journaux utilisé au cours du déploiement, par exemple, C:\MININT\SMSOSD\OSDLOGS|  
|**oUtility.StatePath**|Retourne le chemin du magasin d’état actuellement configuré, par exemple, C:\MININT\StateStore|  
|**oUtility.ScriptName**|Retourne le nom du script appelant la fonction, par exemple, Z-RAMTest|  
|**oUtility.ScriptDir**|Retourne le chemin du script qui appelle la fonction, par exemple, \\\nom_serveur\Deployment$\Scripts|  
|**oUtility.ComputerName**|Détermine le nom d’ordinateur à utiliser pendant le processus de génération, par exemple, nom_ordinateur|  
|**oUtility.ReadIni(file, section, item)**|Permet à l’élément spécifié d’être lu à partir d’un fichier .ini|  
|**oUtility.WriteIni(file, section, item, value)**|Permet à l’élément spécifié d’être écrit dans un fichier .ini|  
|**oUtility.Sections(file)**|Lit les sections d’un fichier .ini et les stocke dans un objet à titre de référence|  
|**oUtility.SectionContents(file, section)**|Lit le contenu du fichier .ini spécifié et le stocke dans un objet|  
|**oUtility.RunWithHeartbeat(sCmd)**|Quand la commande est exécutée, les informations de pulsation sont écrites dans les journaux toutes les 0,5 secondes|  
|**oUtility.FindFile**<br /><br /> **(sFilename,sFoundPath)**|Recherche le fichier spécifié dans le dossier DeployRoot et dans les sous-dossiers standard, notamment Servicing, Tools, USMT, Templates, Scripts et Control|  
|**oUtility.findMappedDrive(sServerUNC)**|Vérifie si un lecteur est mappé sur le chemin d’accès UNC spécifié et retourne la lettre de lecteur|  
|**oUtility.ValidateConnection(sServerUNC)**|Vérifie s’il existe une connexion au serveur spécifié et, si ce n’est pas le cas, tente d’en créer une|  
|**MapNetworkDrive**<br /><br /> **(sShare, SDomID, sDomPwd)**|Mappe une lettre de lecteur sur le chemin d’accès UNC spécifié en tant que partage et retourne la lettre de lecteur utilisée ; retourne une erreur en cas d’échec|  
|**VerifyPathExists(strPath)**|Vérifie que le chemin spécifié existe|  
|**oEnvironment.Substitute(sVal)**|Développe les variables ou fonctions présentes dans une chaîne donnée|  
|**oEnvironment.Item**<br /><br /> **(sName)**|Lit ou écrit une variable dans un magasin persistant|  
|**oEnvironment.Exists**<br /><br /> **(sName)**|Vérifie si la variable existe|  
|**oEnvironment.ListItem**<br /><br /> **(sName)**|Lit ou écrit une variable de type **array** dans un magasin persistant|  
|**oLogging.ReportFailure**<br /><br /> **(sMessage, iError)**|Permet d’effectuer une sortie structurée si une erreur irrécupérable est détectée|  
|**oLogging.CreateEvent**<br /><br /> **(iEventID, iType, sMessage, arrParms)**|Écrit un message dans le fichier journal et publie l’événement sur un serveur défini|  
|**oLogging.CreateEntry**<br /><br /> **(sLogMsg, iType)**|Écrit un message dans le fichier journal|  
|**TestAndFail(iRc, iError, sMessage)**|Quitte le script avec **iError** si **iRc** vaut False ou échoue|  
|**TestAndLog(iRc , sMessage)**|Enregistre un avertissement uniquement si **iRc** vaut False ou échoue|  

###  <a name="IntegrateCustomDeploy"></a> Intégration de code de déploiement personnalisé  
 Le code de déploiement personnalisé peut être intégré au processus MDT de plusieurs manières ; toutefois, quelle que soit la méthode utilisée, les deux règles suivantes doivent être remplies :  

-   Le nom de script du code de déploiement personnalisé doit toujours commencer par la lettre Z.  

-   Le code de déploiement personnalisé doit être placé dans le dossier Scripts sur le partage de déploiement, par exemple, D:\Production Deployment Share\Scripts.  

 Voici les méthodes les plus fréquemment utilisées pour intégrer du code personnalisé qui garantissent également une journalisation cohérente :  

-   Déployer le code en tant qu’application MDT  

-   Lancer le code en tant que commande de séquence de tâches MDT  

-   Lancer le code en tant que script de sortie utilisateur  

#### <a name="deploy-custom-code-as-an-mdt-application"></a>Déployer du code personnalisé en tant qu’application MDT  
 Un code de déploiement personnalisé peut être importé dans Deployment Workbench et géré de la même façon que toute autre application.  

 **Pour créer une application afin d’exécuter du code de déploiement personnalisé**  

1.  Copiez le code de déploiement personnalisée dans le dossier *partage_déploiement*\Scripts (où *partage_déploiement* est le chemin d’accès complet du partage de déploiement).  

2.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

3.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Shares/*partage_déploiement*/Applications (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

4.  Dans le volet Actions, cliquez sur **New Application** (Nouvelle application).  

     L’Assistant Nouvelle application démarre.  

5.  Effectuez l’Assistant Nouvelle application en utilisant les informations suivantes. Acceptez les valeurs par défaut, sauf indication contraire.  

    |**Sur cette page de l’Assistant**|**Faites cela**|  
    |-|-|  
    |**Application Type** (Type d’application)|Cliquez sur **Application without source files or elsewhere on the network** (Application sans fichiers sources ou ailleurs sur le réseau), puis cliquez sur **Next** (Suivant).|  
    |**Détails**|Renseignez cette page en fonction des informations de l’application, puis cliquez sur **Next** (Suivant).|  
    |**Command Details** (Détails de la commande)|1.  Dans la zone **Command line** (Ligne de commande), tapez **cscript.exe %SCRIPTROOT%\code_personnalisé** (où *code_personnalisé* est le nom du code personnalisé qui a été développé).<br />2.  Dans la zone **Working directory** (Répertoire de travail), tapez ***répertoire_de_travail*** (où répertoire_de_travail est le nom du répertoire de travail du code personnalisé ; il s’agit généralement du même dossier que celui spécifié dans la zone **Command line** (Ligne de commande)).<br />3.  Cliquez sur **Suivant**.|  
    |**Résumé**|Vérifiez que les paramètres de configuration sont corrects, puis cliquez sur **Next** (Suivant).|  
    |**Confirmation**|Cliquez sur **Terminer**.|  

 L’application s’affiche dans le nœud Applications, dans Deployment Workbench.  

#### <a name="add-the-custom-code-as-a-task-sequence-step"></a>Ajouter le code personnalisé en tant qu’étape d’une séquence de tâches  
 Le code de déploiement personnalisé peut être appelé directement à partir de n’importe quel point dans une séquence de tâches ; cet appel donne accès aux options et règles de séquence de tâches habituelles.  

 **Pour ajouter le code de déploiement personnalisé à une séquence de tâches**  

1.  Copiez le code de déploiement personnalisée dans le dossier *partage_déploiement*\Scripts (où *partage_déploiement* est le chemin d’accès complet du partage de déploiement).  

2.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

3.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

4.  Dans le volet d’informations, cliquez sur ***séquence_de_tâches*** (où *séquence_de_tâches* est le nom de la séquence de tâches qui exécute le code personnalisé).  

5.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

6.  Dans la boîte de dialogue ***task_sequenceProperties*** (Propriétés de séquence_de_tâches), cliquez sur l’onglet **Task Sequence** (Séquence de tâches).  

7.  Dans l’arborescence de la console, accédez à *groupe* (où *groupe* est le groupe auquel ajouter l’étape de la séquence de tâches).  

8.  Cliquez sur **Add** (Ajouter), sur **General** (Général), puis sur **Run Command Line** (Exécuter la ligne de commande).  

9. Dans l’arborescence de la console, cliquez sur **Run Command Line** (Exécuter la ligne de commande), puis sur l’onglet **Properties** (Propriétés).  

10. Dans la zone **Name** (Nom), tapez ***nom*** (où *nom* est un nom descriptif du code personnalisé).  

11. Sous l’onglet **Properties** (Propriétés) de la zone **Command line** (Ligne de commande), tapez ***ligne_de_commande*** (où *ligne_de_commande* est la commande qui exécute le code personnalisé : par exemple, **cscript.exe %SCRIPTROOT%\CustomCode.vbs**).  

12. Dans la zone **Start in** (Démarrer dans), tapez ***chemin*** (où *chemin* est le chemin d’accès complet du dossier de travail du code personnalisé ; en général, il s’agit du même chemin d’accès que celui spécifié dans la zone **Command Line** (Ligne de commande)), puis cliquez sur **OK**.  

 L’étape de séquence de tâches créée s’affiche dans la liste des étapes de séquence de tâches.  

#### <a name="run-custom-code-as-a-user-exit-script"></a>Exécuter le code personnalisé en tant que script de sortie utilisateur  
 Vous pouvez également exécuter le code personnalisé en tant que script de sortie utilisateur à partir de CustomSettings.ini à l’aide de la directive **UserExit**. Ainsi, les informations sont transmises au processus de validation de règles CustomSettings.ini, et les propriétés MDT sont mises à jour dynamiquement.  

 Pour plus d’informations sur les scripts de sortie utilisateur et la directive **UserExit**, consultez la section « User Exit Scripts in the CustomSettings.ini File » (Scripts de sortie utilisateur dans le fichier CustomSettings.ini) du document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

## <a name="installing-device-drivers-using-various-installation-methods"></a>Installation de pilotes de périphérique à l’aide de diverses méthodes d’installation  
 Dans ce scénario, vous utilisez MDT pour déployer un système d’exploitation sur différents types de matériel. Dans le cadre du processus de déploiement, vous identifiez et installez les pilotes de périphérique afin que chaque type de matériel fonctionne correctement. Il existe deux types principaux de pilotes de périphérique ; chacun d’eux doit être traité différemment pendant le processus de déploiement :  

-   Pilotes de périphérique qui contiennent un fichier .inf pouvant servir à importer les pilotes dans Deployment Workbench  

-   Pilotes de périphérique empaquetés en tant qu’application et devant être installés en tant qu’application  

 À l’aide de MDT, vous pouvez gérer les deux types de pilotes dans le cadre d’un déploiement de système d’exploitation.  

 Installez les pilotes de périphérique en :  

-   Déterminant les méthodes d’installation de chaque pilote de périphérique, comme décrit dans [Déterminer la méthode à utiliser pour installer un pilote de périphérique](#WhichMethodtoInstallDriver)  

-   Utilisant la méthode « pilotes non fournis avec Windows », comme décrit dans [Installation de pilotes de périphérique à l’aide de la méthode « pilotes non fournis avec Windows »](#InstallOutofBoxDrivers)  

-   Les installant en tant qu’applications comme décrit dans [Installation des pilotes de périphérique en tant qu’applications](#InstallDriversasApplications)  

 Ce scénario suppose que MDT s’exécute sur un serveur de déploiement.  

###  <a name="WhichMethodtoInstallDriver"></a> Détermination de la méthode à utiliser pour installer un pilote de périphérique  
 Les fabricants de matériel publient les pilotes de périphérique sous deux formes :  

-   En tant que package que vous pouvez extraire et qui contient les fichiers .inf permettant d’importer le pilote dans Deployment Workbench  

-   En tant qu’application que vous devez installer en suivant les processus d’installation d’application traditionnels  

 Les packages de pilotes de périphérique qui peuvent être extraits pour accéder aux fichiers .inf peuvent utiliser le processus de détection et d’installation de pilote automatique MDT en important d’abord le pilote dans le nœud Out-of-Box Drivers (Pilotes non fournis avec Windows), dans Deployment Workbench.  

 Les packages de pilotes de périphérique qui ne peuvent pas être extraits pour isoler les fichiers .inf ou ceux qui ne fonctionnent pas correctement sans d’abord être installés à l’aide d’un programme d’installation d’application tel qu’un fichier MSI ou Setup.exe peuvent utiliser la fonctionnalité d’installation d’application de MDT et installer le pilote de périphérique pendant le processus de déploiement comme pour toute application normale.  

###  <a name="InstallOutofBoxDrivers"></a> Installation de pilotes de périphérique à l’aide de la méthode « pilotes non fournis avec Windows »  
 Vous pouvez importer des packages de pilotes de périphérique qui incluent un fichier .inf dans Deployment Workbench, puis les installer automatiquement dans le cadre du processus de déploiement. Pour implémenter ce type de déploiement de pilotes de périphérique, ajoutez d’abord le pilote de périphérique à Deployment Workbench.  

 **Pour ajouter le pilote de périphérique à Deployment Workbench**  

1.  Téléchargez les pilotes de périphérique requis pour les types de matériel à déployer et extrayez le package de pilotes de périphérique dans un emplacement temporaire.  

2.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

3.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Out-of-Box Drivers (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

4.  Dans le volet Actions, cliquez sur **Import Drivers** (Importer les pilotes).  

     L’Assistant Importation des pilotes de périphérique démarre.  

5.  Dans la page **Specify Directory** (Spécifier le répertoire), dans la section **Drive source** (Source des pilotes), cliquez sur **Browse** (Parcourir) pour accéder au dossier qui contient les nouveaux pilotes de périphérique, puis cliquez sur **Next** (Suivant).  

    > [!NOTE]
    >  L’Assistant Nouveau pilote de périphérique parcourt tous les sous-répertoires du répertoire source des pilotes ; ainsi, s’il existe plusieurs pilotes à installer, extrayez-les dans des dossiers au sein du même répertoire racine, puis définissez le répertoire source des pilotes en tant que répertoire racine qui contient tous les dossiers source des pilotes.  

6.  Dans la page **Summary** (Résumé), vérifiez que les paramètres sont corrects, puis cliquez sur **Next** (Suivant) pour importer les pilotes dans Deployment Workbench.  

7.  Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

 Si les pilotes de périphérique contiennent des pilotes critiques de démarrage, tels que des pilotes de classes réseau ou de stockage de masse, le partage de déploiement doit ensuite être mis à jour pour générer un nouvel environnement de démarrage LiteTouch_x86 et LiteTouch_x64 qui contient les nouveaux pilotes.  

 **Pour ajouter les pilotes de périphérique aux images Windows PE Lite Touch**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement* (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

4.  Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

5.  Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

6.  Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

###  <a name="InstallDriversasApplications"></a> Installation des pilotes de périphérique en tant qu’applications  
 Les pilotes de périphérique qui sont empaquetés en tant qu’applications et que vous ne pouvez pas extraire dans un dossier contenant un fichier .inf, en plus des fichiers de pilote, doivent être ajoutés à Deployment Workbench en tant qu’application en vue de leur installation pendant le processus de déploiement.  

 Les applications peuvent être spécifiées en tant qu’étape de séquence de tâches ou spécifiées dans CustomSettings.ini ; toutefois, les applications de pilote de périphérique doivent être installées uniquement quand la séquence de tâches est exécutée sur un ordinateur doté des périphériques. Pour ce faire, exécutez l’étape de séquence de tâches pour déployer les applications de pilote de périphérique appropriées en tant qu’étape de séquence de tâches conditionnelle. Les critères conditionnels peuvent être spécifiés pour exécuter l’étape de séquence de tâches à l’aide de requêtes WMI en fonction du périphérique sur l’ordinateur cible.  

#### <a name="add-the-device-driver-application-to-the-deployment-workbench"></a>Ajouter l’application de pilote de périphérique à Deployment Workbench  
 Chaque application de pilote de périphérique doit d’abord être importée dans Deployment Workbench.  

> [!NOTE]
>  Pour indiquer si une application doit être visible pendant le déploiement, dans la boîte de dialogue **Properties** (Propriétés) de l’application concernée, cochez ou décochez la case **Hide this application in the Deployment Wizard** (Masquer cette application dans l’Assistant Déploiement). Répétez ce processus pour chaque application de pilote de périphérique utilisée pendant le déploiement.  

 **Pour ajouter l’application de pilote de périphérique à Deployment Workbench**  

1.  Téléchargez l’application de pilote de périphérique et enregistrez-la dans un emplacement temporaire.  

2.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

3.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Applications (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

4.  Dans le volet Actions, cliquez sur **New Application** (Nouvelle application).  

     L’Assistant Nouvelle application démarre.  

5.  Dans la page **Application Type** (Type d’application), cliquez sur **Application with source files** (Application avec fichiers sources), puis cliquez sur **Next** (Suivant).  

6.  Dans la page **Details** (Détails), tapez les détails pertinents de l’application, puis cliquez sur **Next** (Suivant).  

7.  Dans la page **Source**, dans la section **Source Directory** (Répertoire source), cliquez sur **Browse** (Parcourir) pour y accéder, puis cliquez sur le répertoire qui contient les fichiers sources de l’application de pilote de périphérique. Cliquez sur **OK**.  

8.  Cliquez sur **Suivant**.  

9. Dans la page **Destination**, tapez le nom du répertoire de destination, puis cliquez sur **Next**.  

10. Dans la page **Command Details** (Détails de la commande), dans la section **Command Line** (Ligne de commande), tapez la commande qui autorise l’installation sans assistance de l’application de pilote de périphérique.  

11. Dans la page **Summary** (Récapitulatif), vérifiez que les paramètres sont corrects, puis cliquez sur **Next** pour importer l’application de pilote de périphérique dans Deployment Workbench.  

12. Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

 Une fois que les applications sont importées dans Deployment Workbench, ajoutez-les au processus de déploiement à l’aide de la logique appropriée pour vérifier que l’application s’installe uniquement pendant l’exécution du matériel approprié. Plusieurs méthodes permettent de le faire :  

-   Spécifier l’application de pilote de périphérique dans une séquence de tâches de déploiement.  

-   Spécifier l’application de pilote de périphérique dans CustomSettings.ini.  

-   Spécifier l’application de pilote de périphérique dans la base de données MDT.  

 Chaque approche est décrite plus en détail dans les sections suivantes.  

####  <a name="SpecifyDeviceAppTask"></a> Spécifier l’application de pilote de périphérique dans une séquence de tâches de déploiement  
 La première méthode pour ajouter une application de pilote de périphérique au processus de déploiement est d’utiliser une séquence de tâches afin d’ajouter des étapes pour chaque application de pilote de périphérique.  

 Deux approches principales permettent de gérer les applications de pilote de périphérique dans la séquence de tâches :  

-   Créer un groupe de séquence de tâches pour chaque modèle de matériel, puis ajouter une requête pour exécuter ce groupe d’actions si l’ordinateur correspond à un type de matériel spécifique.  

-   Créer un groupe de séquence de tâches pour des applications propres à un matériel, puis ajouter des requêtes pour chaque action de séquence de tâches de sorte que chaque étape de séquence de tâches est évaluée en fonction du type de matériel et s’exécute uniquement si une correspondance est trouvée.  

 **Pour créer un groupe de séquence de tâches pour chaque type de matériel**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet d’informations, cliquez sur ***séquence_tâches*** (où *séquence_tâches* est la séquence de tâches de déploiement nécessaire pour installer l’application de pilote de périphérique).  

4.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

5.  Dans la boîte de dialogue ***task_sequenceProperties***, sous l’onglet **Task Sequence** (Séquence de tâches), dans le volet d’informations, accédez à State Restore/Windows Update (Pre-Application Installation).  

6.  Sous l’onglet **Task Sequence** (Séquence de tâches), cliquez sur **Add** (Ajouter), puis sur **New Group** (Nouveau groupe).  

     De cette façon vous créez un groupe de séquence de tâches dans la séquence de tâches. Utilisez ce nouveau groupe de séquence de tâches pour créer les étapes d’installation des applications de pilote de périphérique propres à un matériel.  

7.  Dans le volet d’informations, cliquez sur **New Group** (Nouveau groupe).  

8.  Sous l’onglet **Properties** (Propriétés), dans la zone **Name** (Nom), tapez ***nom_groupe*** (où *nom_groupe* est le nom du groupe. Par exemple, *Applications propres à un matériel – Dell Computer Corporation*).  

9. Sous l’onglet **Options**, cliquez sur **Add** (Ajouter), puis sur **Query WMI** (Interroger WMI).  

10. Dans la boîte de dialogue **Task Sequence WMI Condition** (Condition WMI de la séquence de tâches), tapez les informations suivantes :  

    -   Dans la zone **WMI namespace** (Espace de noms WMI), tapez **root\cimv2**.  

    -   Dans la zone **WQL query** (Requête WQL), tapez une requête de langage de requêtes WMI (WQL) à l’aide de la classe **Win32_ComputerSystem** afin de garantir que l’application est installée uniquement pour un type d’application spécifique, par exemple :  

         **Sélectionnez \*FROM Win32_ComputerSystem WHERE Model LIKE *%modèle_matériel%* AND Manufacturer LIKE *%fabricant_matériel%***  

         Dans cet exemple, *modèle_matériel* est le nom du modèle d’ordinateur (par exemple, Latitude D620) et *fabricant_matériel* est le nom du fabricant de l’ordinateur (par exemple, Dell Corporation).  

         Le symbole **%** est un caractère générique inclus dans les noms pour permettre aux administrateurs de retourner tous les modèles ou fabricants d’ordinateur qui contiennent la valeur spécifiée pour ***modèle_matériel*** ou ***fabricant_matériel***.  

     Pour plus d’informations sur les requêtes WMI et WQL, consultez la section « Add WMI Queries to Task Sequence Steps Conditions » (Ajouter des requêtes WMI aux conditions d’étape de séquence de tâches) dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit) et consultez [Querying with WQL](http://msdn.microsoft.com/library/aa392902.aspx) (Interrogation avec WQL).  

11. Cliquez sur **OK** pour envoyer la requête, puis sur **OK** pour envoyer les changements à la séquence de tâches.  

> [!NOTE]
>  Ce processus doit être répété pour chaque type de matériel de chaque application de pilote de périphérique à installer.  

 Une fois que vous avez créé les groupes de séquence de tâches propres à un matériel, les applications de pilote de périphérique peuvent être ajoutées à chaque groupe.  

 **Pour ajouter des applications de pilote de périphérique aux groupes de séquence de tâches propres à un matériel**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet d’informations, cliquez sur ***séquence_tâches*** (où *séquence_tâches* est la séquence de tâches de déploiement nécessaire pour installer l’application de pilote de périphérique).  

4.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

5.  Dans la boîte de dialogue ***task_sequenceProperties***, cliquez sur l’onglet **Task Sequence** (Séquence de tâches).  

6.  Dans le volet d’informations, accédez à State Restore/*groupe_spécifique_matériel* (où *groupe_spécifique_matériel* est le nom du groupe propre à un matériel où est ajoutée l’étape de séquence de tâches pour installer l’application de pilote de périphérique).  

7.  Sous l’onglet **Task Sequence** (Séquence de tâches), cliquez sur **Add** (Ajouter), sur **General** (Général), puis sur **Install Application** (Installer l’application).  

     L’étape de séquence de tâches **Install Application** (Installer l’application) apparaît dans le volet d’informations.  

8.  Dans le volet d’informations, cliquez sur **Install Application.** (Installer l’application)  

9. Sous l’onglet **Properties** (Propriétés), cliquez sur **Install a single application** (Installer une seule application) et dans la liste **Application to install** (Application à installer), sélectionnez ***application_matériel*** (où *application_matériel* est l’application propre à un matériel).  

> [!NOTE]
>  Ce processus doit être répété pour chaque application de pilote de périphérique à utiliser dans le déploiement.  

#### <a name="specify-the-device-driver-application-in-customsettingsini"></a>Spécifier l’application de pilote de périphérique dans CustomSettings.ini  
 Quand un déploiement LTI ou ZTI commence, une des premières actions à effectuer est le traitement des fichiers de contrôle BootStrap.ini et CustomSettings.ini. Ces deux fichiers contiennent des règles qui peuvent être utilisées pour personnaliser le déploiement de manière dynamique.  

 En raison de la façon dont MDT traite le fichier CustomSettings.ini, vous pouvez l’utiliser pour ajouter des applications selon des conditions spécifiques. Cette logique est utilisée pour ajouter des applications propres à un pilote de périphérique pendant le déploiement selon le type de matériel. Les applications sont référencées dans CustomSettings.ini par GUID, situé dans le fichier Applications.xml du partage de déploiement.  

 **Pour rechercher le GUID d’une application importée**  

1.  Dans le partage de déploiement du serveur de déploiement, ouvrez le dossier Control, par exemple, D:\Production Deployment Share\Control.  

2.  Recherchez et ouvrez le fichier Applications.xml.  

3.  Recherchez l’application nécessaire.  

4.  Recherchez le GUID de l’application en identifiant la ligne entre les balises `<guid>` de l’application. Par exemple, `<application guid={c303fa6e-3a4d-425e-8102-77db9310e4d0}>`.  

 Dans le cadre du processus d’initialisation, les processus ZTI et LTI rassemblent des informations sur l’ordinateur sur lequel il s’exécutent. Dans le cadre de ce processus, les requêtes WMI sont exécutées et les valeurs de la classe **Win32_ComputerSystem** pour le modèle et le fabricant sont remplies avec les variables **%Make%** et **%Model%** respectivement.  

 Ces valeurs peuvent être utilisées pendant le traitement du fichier CustomSettings.ini pour lire dynamiquement les sections du fichier en fonction de la marque et du modèle détectés.  L’exemple suivant illustre un fichier CustomSettings.ini.  

 **Exemple CustomSettings.ini configuré pour l’installation d’une application propre à un matériel**  

```  
[Settings]  
Priority=Make, Default  
Properties=MyCustomProperty  

[Default]  
OSInstall=Y  

[Dell Computer Corporation]  
Subsection=Dell-%Model%  

[Dell-Latitude D620]  
MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D}  

[Dell-Latitude D610]  
MandatoryApplications001={c303fa6e-3a4d-425e-8102-77db9310e4d0}  
```  

 Utilisez les propriétés suivantes pour spécifier les applications dans CustomSettings.ini :  

-   **Applications**. Cette propriété peut être utilisée quand les administrateurs de déploiement ne veulent pas présenter un Assistant d’application dans le cadre du processus de déploiement en spécifiant **SkipApplications=YES** dans CustomSettings.ini.  

-   **MandatoryApplications**. Cette propriété peut être utilisée si les administrateurs de déploiement veulent présenter l’Assistant d’application pendant le déploiement pour permettre aux ingénieurs de déploiement de sélectionner des applications supplémentaires à installer pendant le déploiement.  

     Si l’Assistant d’application est utilisé sans la propriété **MandatoryApplications** (par exemple, **SkipApplications=NO**), il remplace les applications spécifiées par la propriété **Applications**.  

     L’exemple précédent montre comment utiliser les valeurs des variables **%Make%** et **%Model%** pour manipuler dynamiquement la façon dont la liste des applications est construite. Les valeurs de la marque et du modèle de chaque type de matériel peuvent être recherchées à l’aide de l’une des méthodes suivantes :  

-   **Outil Informations système**. Utilisez le nœud Résumé système de cet outil pour identifier le **Fabricant du système** (marque) et le **Modèle du système** (modèle).  

-   **Windows PowerShell**. Utilisez l’applet de commande **Get-WMIObject –class Win32_ComputerSystem** pour déterminer la marque et le modèle de l’ordinateur.  

-   **Ligne de commande de Windows Management Instrumentation**. Utilisez **CSProduct Get Name, Vendor** pour retourner le nom (modèle) et le fournisseur (marque) de l’ordinateur.  

 **Pour modifier CustomSettings.ini en ajoutant une logique propre à un matériel**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Cliquez sur l’onglet **Rules** (Règles).  

5.  Les informations entrées sous cet onglet sont stockées dans le fichier CustomSettings.ini. Modifiez les entrées du fichier CustomSettings.ini afin d’ajouter une logique pour chaque modèle de matériel qui a une application propre à un pilote de périphérique, comme décrit dans [Spécifier l’application de pilote de périphérique dans une séquence de tâches](#SpecifyDeviceAppTask).  

6.  Cliquez sur **OK** pour valider les modifications.  

7.  Dans le volet d’informations, cliquez sur *partage_déploiement* (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

8.  Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

9. Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

10. Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

11. Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

 Par défaut, toutes les applications disponibles sont affichées dans l’Assistant de déploiement Windows pendant un déploiement LTI. Comme les applications propres à un pilote de périphérique sont applicables uniquement à des types de matériel spécifiques, vous pouvez ne pas avoir envie de les afficher tout le temps. En spécifiant le package d’application propre à un pilote de périphérique dans CustomSettings.ini, l’application peut être masquée à l’aide de l’option **Hide the application in the Deployment Wizard** (Masquer l’application dans l’Assistant de déploiement) dans la configuration de l’application.  

 **Pour masquer une application dans l’Assistant de déploiement**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Applications (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet d’informations, cliquez sur ***application_pilote_périphérique*** (où *application_pilote_périphérique* est l’application à masquer à partir de l’Assistant de déploiement).  

4.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

5.  Sous l’onglet **General** (Général), cochez la case **Hide the application in the Deployment Wizard** (Masquer l’application dans l’Assistant de déploiement).  

6.  Cliquez sur **Apply** (Appliquer), puis fermez la boîte de dialogue **Properties** (Propriétés).  

#### <a name="specify-the-device-driver-application-in-the-mdt-db"></a>Spécifier l’application de pilote de périphérique dans la base de données MDT  
 La base de données MDT est une version de base de données du fichier CustomSettings.ini et peut être interrogée au moment du déploiement pour obtenir plus d’informations utiles pour le déploiement. Pour plus d’informations sur l’utilisation de la base de données MDT, consultez « Sélection des méthodes pour l’application des paramètres de configuration ».  

 Quand vous interrogez la base de données MDT au moment du déploiement, trois méthodes sont disponibles pour identifier l’ordinateur cible :  

-   Rechercher l’ordinateur individuel (à l’aide de l’adresse MAC, la balise de ressource ou un élément similaire).  

-   Rechercher l’emplacement de l’ordinateur (à l’aide de la passerelle par défaut).  

-   Rechercher la marque et le modèle de l’ordinateur (à l’aide du fabricant WMI ou des requêtes de marque et modèle).  

 Pour chaque entrée de base de données que vous créez, vous pouvez spécifier des propriétés de déploiement, des applications, des administrateurs et s’il faut utiliser des packages Configuration Manager. En créant des entrées de marque et de modèle dans la base de données, vous pouvez ajouter les applications propres à un pilote de périphérique nécessaires.  

 **Pour créer des entrées dans la base de données MDT afin de permettre l’installation d’applications propres à un pilote de périphérique**  

> [!NOTE]
>  Répétez ce processus pour chaque marque et modèle de matériel qui nécessitent une application de pilote de périphérique.  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/**partage_déploiement**/Advanced Configuration/Database/Make and Model (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **New** (Nouveau).  

4.  Dans la boîte de dialogue **Properties** (Propriétés), sous l’onglet **Identity** (Identité), dans la zone **Make** (Marque), tapez ***nom_marque*** (où *nom_marque* est un nom facilement identifié à associer au fabricant de l’ordinateur cible).  

5.  Dans la zone **Model** (Modèle), tapez ***nom_modèle*** (où *nom_modèle* est un nom facilement identifié à associer au modèle de l’ordinateur cible).  

6.  Sous l’onglet **Applications**, ajoutez chaque application de pilote de périphérique nécessaire pour ce modèle de matériel.  

## <a name="initiating-mdt-using-windows-deployment-services"></a>Lancement de MDT à l’aide des services de déploiement Windows  
 Windows Server 2008 utilise les services de déploiement Windows sous forme d’une version mise à jour et repensée des services d’installation à distance, l’outil de déploiement par défaut dans Windows Server 2003 avec SP2. Les services de déploiement Windows vous permettent de déployer des systèmes d’exploitation Windows (notamment Windows 7, Windows Server 2008 ou versions ultérieures) sur un réseau à l’aide d’un support de démarrage ou d’une carte réseau PXE.  

 Avant de déployer les services de déploiement Windows, déterminez les options d’intégration les mieux adaptées à votre environnement parmi les suivantes :  

-   Option 1. Démarrer les ordinateurs dans PXE pour lancer le processus LTI.  

-   Option 2. Déployer une image de système d’exploitation à partir du magasin d’images des services de déploiement Windows.  

-   Option 3. Utiliser la multidiffusion avec MDT et le rôle serveur Services de déploiement Windows de Windows Server 2008.  

### <a name="option-1-boot-computers-in-pxe-to-initiate-the-lti-process"></a>Option 1 : Démarrer les ordinateurs dans PXE pour lancer le processus LTI  
 Réduisez les coûts de gestion des déploiements de système d’exploitation en commençant le processus de déploiement MDT à l’aide des services de déploiement Windows et du protocole DHCP. De cette façon, vous n’avez plus besoin de créer un support de démarrage sur chaque ordinateur cible.  

#### <a name="create-and-import-the-deployment-workbench-windows-pe-image-into-windows-deployment-services"></a>Créer et importer l’image Windows PE de Deployment Workbench dans les services de déploiement Windows  
 Quand vous créez un partage de déploiement MDT ou modifiez un déploiement partage de déploiement MDT existant, vous pouvez créer une image de démarrage Windows PE personnalisée. De cette façon, quand le partage de déploiement est mis à jour, l’image de démarrage Windows PE est automatiquement générée et mise à jour avec les informations du partage de déploiement, et injecte tous les pilotes ou composants supplémentaires spécifiés pendant la configuration du partage de déploiement.  

 L’image de démarrage Windows PE est générée à la fois sous forme d’un fichier image ISO, que vous pouvez écrire sur un CD ou DVD, et d’un fichier WIM de démarrage. Vous pouvez importer le fichier WIM dans les services de déploiement Windows afin que les ordinateurs qui peuvent démarrer dans PXE puissent télécharger et exécuter l’image de démarrage Windows PE LTI sur un réseau utilisé pour initialiser une installation.  

 **Pour créer une image de démarrage Windows PE dans Deployment Workbench**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares (Partages de déploiement)/*partage_déploiement* (où *partage_déploiement* correspond au nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

     Dans la boîte de dialogue ***deployment_shareProperties***, cliquez sur l’onglet **Windows PE*plateforme* Settings** (Paramètres de la *plateforme* Windows PE) (où plateforme est l’architecture de l’image Windows PE à configurer).  

4.  Dans la zone **Lite Touch Boot Image Settings** (Paramètres de l’image de démarrage Lite Touch), cochez la case **Generate a Lite Touch bootable RAM disk ISO image** (Générer une image ISO Lite Touch de disque virtuel démarrable).  

5.  Cliquez sur l’onglet **Windows PE *plateforme* Components** (Composants de la *plateforme* Windows PE) (où *plateforme* est l’architecture de l’image Windows PE à configurer).  

6.  Dans la section **Driver Injection** (Injection de pilotes), cliquez sur les types de pilote appropriés à inclure.  

    > [!NOTE]
    >  Cette étape est inutile si Windows PE inclut déjà les pilotes de périphérique nécessaires.  

7.  Dans la section **Driver Injection** (Injection de pilotes), dans la liste **Selection Profile** (Profil de sélection), sélectionnez le profil de sélection de pilote approprié.  

8.  Dans la boîte de dialogue **Properties** (Propriétés), cliquez sur **OK**.  

    > [!NOTE]
    >  Cette étape est inutile si Windows PE inclut déjà les pilotes de périphérique nécessaires.  

9. Dans le volet d’informations, cliquez sur ***partage_déploiement*** (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

10. Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

11. Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

12. Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

13. Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

     Une fois le processus terminé, le dossier de démarrage (Boot) dans le partage de déploiement contient un certain nombre d’images de démarrage, par exemple :  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x64.wim  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.iso  

     D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim  

 Vous pouvez écrire les fichiers ISO générés directement sur un CD ou DVD, ou les utiliser pour initialiser le processus LTI sur un nouveau matériel. Vous pouvez importer les fichiers WIM de démarrage dans les services de déploiement Windows, pour que les nouveaux ordinateurs puissent initialiser le processus de déploiement LTI sans support physique.  

 **Pour importer l’image Windows PE dans les services de déploiement Windows**  

1.  Démarrez la console des services de déploiement Windows et connectez-vous aux services de déploiement Windows.  

2.  Dans l’arborescence de la console, cliquez sur **Images de démarrage**, puis sur **Ajouter une image de démarrage**.  

3.  Accédez à l’image WIM à importer, par exemple, D:\Production Deployment Share\Boot\LiteTouchPE_x86.wim.  

4.  Le processus d’importation lit automatiquement les métadonnées à partir de l’image de démarrage, mais les valeurs **Nom de l’image** et **Description de l’image** peuvent également être modifiées. **Nom de l’image** affecte les informations d’option de démarrage affichées par le Gestionnaire de démarrage Windows quand le client démarre dans PXE.  

5.  Quand l’image de démarrage a été importée, tout ordinateur qui démarre dans PXE et reçoit une réponse des services de déploiement Windows peut télécharger l’image de démarrage LTI et lancer une installation LTI.  

 L’installation et la configuration des services de déploiement Windows ne sont pas abordées dans ce guide. Pour plus d’informations sur les services de déploiement Windows, consultez le [Guide des services de déploiement Windows](http://technet.microsoft.com/library/cc265612.aspx).  

#### <a name="use-windows-deployment-services-to-automatically-detect-the-deployment-server"></a>Utiliser les services de déploiement Windows pour détecter automatiquement le serveur de déploiement  
 Une autre option est disponible lors de l’utilisation des services de déploiement Windows pour héberger les images de démarrage MDT quand le partage de déploiement MDT est hébergé sur le même serveur que les services de déploiement Windows.  

 Quand un client PXE charge l’image de démarrage MDT, le nom du serveur des services de déploiement Windows qui héberge l’image de démarrage est capturé et placé dans le MDTProperty **WDSServer**. Vous pouvez ensuite référencer cette propriété dans le fichier BootStrap.ini de l’image de démarrage et dans le fichier CustomSettings.ini du partage de déploiement par la propriété **DeployRoot**. De cette façon, le client démarre automatiquement à partir des services de déploiement Windows en utilisant le partage de déploiement hébergé sur le serveur des services de déploiement Windows. Vous n’avez donc pas besoin de spécifier un nom de serveur dans un des fichiers de configuration.  

 **Pour définir le serveur des services de déploiement Windows local comme serveur de déploiement**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Advanced Configuration/Database (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Cliquez sur l’onglet **Rules** (Règles).  

     Les informations entrées sous cet onglet sont stockées dans le fichier CustomSettings.ini.  

5.  Configurez la propriété **DeployRoot** pour utiliser la variable **%WDSServer%**, par exemple, **DeployRoot=\\\\%WDSServer%\Deployment$**.  

6.  Cliquez sur **Edit Bootstrap.ini** (Modifier Bootstrap.ini).  

7.  Configurez BootStrap.ini pour utiliser la propriété **%WDSServer%** en ajoutant ou en changeant la valeur de **DeployRoot** en **DeployRoot=\\\\%WDSServer%\Deployment$** .  

8.  Dans le menu **File**, cliquez sur **Save** pour enregistrer les changements du fichier BootStrap.ini.  

9. Cliquez sur **OK**.  

     Le partage de déploiement doit être mis à jour.  

10. Dans le volet d’informations, cliquez sur **partage_déploiement** (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

11. Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

12. Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

13. Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

14. Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

15. Importez le fichier WIM de démarrage mis à jour dans les services de déploiement Windows.  

### <a name="option-2-deploy-an-operating-system-image-from-the-windows-deployment-services-store"></a>Option 2 : Déployer une image de système d’exploitation à partir du magasin d’images des services de déploiement Windows  
 Si vous utilisez déjà les services de déploiement Windows pour le déploiement de système d’exploitation, étendez la fonctionnalité de MDT en le configurant pour référencer les images de système d’exploitation des services de déploiement Windows déjà en cours d’utilisation au lieu d’utiliser son propre magasin et de compléter les déploiements des services de déploiement Windows avec la gestion de pilote, le déploiement d’application, l’installation de mise à jour, le traitement de règle et d’autres fonctionnalités de MDT. Une fois que MDT référence une image de système d’exploitation des services de déploiement Windows, vous pouvez la traiter comme n’importe quel système d’exploitation transféré vers un partage de déploiement MDT.  

 **Pour référencer une image de système d’exploitation des services de déploiement Windows**  

> [!NOTE]
>  Les étapes suivantes nécessitent qu’au moins une image de système d’exploitation ait été importée précédemment dans le serveur des services de déploiement Windows.  

1.  Mettez à jour MDT pour pouvoir accéder aux images des services de déploiement Windows en copiant les fichiers suivants à partir du dossier Sources du support Windows dans le dossier C:\Program Files\Microsoft Deployment Toolkit\bin sur le serveur des services de déploiement Windows :  

    -   Wdsclientapi.dll  

    -   Wdscsl.dll  

    -   Wdsimage.dll  

    -   Wdstptc.dll (applicable uniquement si vous effectuez la copie à partir des répertoires sources de Windows Server 2008)  

    > [!NOTE]
    >  Le répertoire source Windows utilisé doit correspondre à la plateforme du système d’exploitation en cours d’exécution sur l’ordinateur où est installé MDT.  

2.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

3.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Operating Systems (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

4.  Dans le volet Actions, cliquez sur **Import Operating System** (Importer le système d’exploitation).  

     L’Assistant permettant d’importer un nouveau système d’exploitation démarre.  

5.  Dans la page **OS Type** (Type de système d’exploitation), cliquez sur **Windows Deployment Services images** (Images des services de déploiement Windows), puis sur **Next**.  

6.  Dans la page **WDS Server** (Serveur WDS), tapez le nom du serveur de services de déploiement Windows à référencer (par exemple, **WDSSvr001**), puis cliquez sur **Next**.  

7.  Dans la page **Summary** (Récapitulatif), vérifiez que les informations sont correctes, puis cliquez sur **Next**.  

8.  Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

     Toutes les images disponibles sur le serveur des services de déploiement Windows sont désormais accessibles aux séquences de tâches MDT.  

> [!NOTE]
>  L’importation d’images à partir des services de déploiement Windows ne copie pas les fichiers sources du serveur des services de déploiement Windows dans le partage de déploiement. MDT continue d’utiliser les fichiers sources à partir de leur emplacement d’origine.  

### <a name="option-3-use-multicasting-with-mdt-and-the-windows-server-2008-windows-deployment-services-role"></a>Option 3 : Utiliser la multidiffusion avec MDT et le rôle Services de déploiement Windows de Windows Server 2008  
 Avec la publication de Windows Server 2008, les services de déploiement Windows ont été améliorés pour prendre en charge le déploiement d’images à l’aide de transmissions par multidiffusion. MDT inclut également des mises à jour pour s’intégrer à la multidiffusion des services de déploiement Windows.  

 Par ailleurs, une mise à jour du Kit d’installation automatisée (Windows AIK), version 1.1, inclut Wdsmcast.exe. Cela permet de rejoindre manuellement des sessions de multidiffusion et permet au client de lancer Wdsmcast.exe pour copier des fichiers à partir d’une session de multidiffusion active.  

 Le script LTIApply.wsf utilise Wdsmcast.exe quand il accède aux fichiers sources de système d’exploitation à partir du partage de déploiement. LTIApply.wsf recherche Wdsmcast.exe sur le partage de déploiement dans le dossier *partage_déploiement*\Tools\x86 ou *partage_déploiement*\Tools\x64 (où *partage_déploiement* est le nom du dossier de système de fichiers qui contient le partage de déploiement), selon la version de Windows PE exécutée.  

 Quand LTIApply.wsf est exécuté, il tente toujours de télécharger des images WIM à partir d’un flux de multidiffusion existant, mais il a recourt à une copie de fichier standard si aucun flux de multidiffusion n’existe.  

> [!NOTE]
>  Ce processus s’applique uniquement aux fichiers image WIM.  

 Les prérequis du serveur de déploiement pour préparer la multidiffusion MDT sont les suivants :  

-   Le serveur de déploiement doit exécuter Windows Server 2008 ou version ultérieure  

-   Le rôle Services de déploiement Windows doit être installé à partir de la console de gestion du serveur  

-   Windows AIK 1.1 pour Windows Server 2008 doit être installé  

-   MDT doit être installé  

-   Comme avec n’importe quel déploiement utilisant MDT, au moins une image WIM de système d’exploitation doit avoir été importée, sous la forme d’un ensemble complet de fichiers sources ou d’une image personnalisée avec les fichiers d’installation  

> [!NOTE]
>  Vous devez utiliser la dernière version du Kit d’installation automatisée (Windows AIK) pour la multidiffusion. La copie de Windows PE incluse dans les versions antérieures de Windows AIK, par exemple, Windows AIK 1.0, ne prend pas en charge le téléchargement à partir d’un serveur de multidiffusion.  

 **Pour configurer MDT pour la multidiffusion à partir d’un partage de déploiement existant**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement* (où *partage_déploiement* est le nom du partage de déploiement à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Sous l’onglet **General**, cochez la case **Enable multicast for this deployment share (requires Windows Server 2008 Windows Deployment Services)** (Activer la multidiffusion pour ce partage de déploiement (nécessite les services de déploiement Windows de Windows Server 2008)).  

5.  Cliquez sur **OK**.  

6.  Dans le volet Actions, cliquez sur **Update Deployment Share** (Mettre à jour le partage de déploiement).  

     L’Assistant Update Deployment Share (Mise à jour de partage de déploiement) démarre.  

7.  Dans la page **Options**, sélectionnez les options souhaitées pour la mise à jour du partage de déploiement, puis cliquez sur **Next** (Suivant).  

8.  Dans la page **Summary** (Résumé), vérifiez que les informations sont correctes, puis cliquez sur **Next** (Suivant).  

9. Dans la page **Confirmation**, cliquez sur **Finish** (Terminer).  

 Le partage de déploiement est maintenant configuré pour la transmission par multidiffusion des services de déploiement Windows.  

 Ce processus crée une transmission par multidiffusion des services de déploiement Windows de diffusion automatique qui utilise directement le partage de déploiement MDT existant. MDT ne crée pas de transmissions de diffusion planifiée. Notez également qu’aucune autre image n’est importée dans les services de déploiement Windows et qu’il n’est pas possible d’utiliser la multidiffusion pour les images de démarrage, car le client de multidiffusion ne peut pas être chargé tant que Windows PE est en cours d’exécution.  

 **Pour vérifier que la transmission par multidiffusion a été générée dans les services de déploiement Windows**  

1.  Cliquez sur **Démarrer**, pointez sur **Outils d’administration**, puis cliquez sur **Services de déploiement Windows**.  

2.  Dans l’arborescence de la console des services de déploiement Windows, cliquez sur **Serveurs**, puis sur **Ajouter un serveur**.  

3.  Dans la boîte de dialogue **Ajouter des serveurs**, cliquez sur **Ordinateur local**, puis sur **OK**.  

4.  Dans l’arborescence de la console des services de déploiement Windows, cliquez sur **Serveurs**, puis sur ***nom_serveur*** (où *nom_serveur* est le nom de l’ordinateur exécutant les services de déploiement Windows). Cliquez sur **Transmissions par multidiffusion**.  

5.  Dans le volet d’informations, une nouvelle transmission de diffusion automatique pour le partage de déploiement s’affiche (par ex., **BDD Share Deployment$**.  

6.  Vérifiez que l’état de la transmission de diffusion automatique **BDD Share Deployment$** est définie sur **Actif**.  

 Dès qu’un ordinateur est déployé, vérifiez que le système d’exploitation a été téléchargé à partir d’une transmission par multidiffusion en examinant le fichier BDD.log dans le dossier \Windows\Temp\DeploymentLogs.  

 Le dossier des journaux contient deux entrées, les deux commençant par **Multicast transfer**. Examinez-les pour vérifier que le transfert a réussi. Pour plus d’informations sur les transmissions par multidiffusion avec MDT et les services de déploiement Windows, consultez la section « Enable Windows Deployment Services Multicast Deployment for LTI Deployments » (Activer le déploiement par multidiffusion des services de déploiement Windows pour les déploiements LTI), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

## <a name="performing-staged-deployments-using-mdt-oem-preload"></a>Effectuer des déploiements intermédiaires à l’aide de MDT (préchargement OEM)  
 Dans de nombreuses organisations, les ordinateurs sont chargés avec l’image de système d’exploitation avant le déploiement sur le réseau de production. Dans certains cas, le chargement de l’image de système d’exploitation est effectué par une équipe au sein de l’organisation qui est responsable de la création d’ordinateurs dans un environnement de préproduction. Dans d’autres cas, le chargement de l’image de système d’exploitation est effectué par le fournisseur d’ordinateurs, également appelé *fabricant d’ordinateurs OEM*.  

> [!NOTE]
>  Le processus de préchargement OEM est pris en charge dans MDT uniquement pour les déploiements effectués à l’aide de LTI. Pour Configuration Manager, utilisez la fonctionnalité de support préparé.  

### <a name="overview-of-the-oem-preload-process-in-mdt"></a>Vue d’ensemble du processus de préchargement OEM dans MDT  
 Le processus de préchargement OEM est divisé en trois phases :  

-   **Phase 1**. Créer une image basée sur un support pour l’ordinateur de référence à appliquer dans l’environnement de préproduction.  

-   **Phase 2**. Appliquer l’image d’ordinateur de référence sur l’ordinateur cible dans un environnement de préproduction.  

-   **Phase 3**. Exécuter le déploiement de l’ordinateur cible dans l’environnement de production.  

 La phase 1 et la phase 3 sont généralement effectuées par l’organisation de déploiement. En fonction de l’utilisation du processus de préchargement OEM dans l’organisation, la phase 2 peut être effectuée par l’organisation ou par le fabricant d’ordinateurs qui fournit les ordinateurs. Si l’organisation effectue la phase 2, l’environnement de préproduction se trouve dans l’organisation. Si un fabricant OEM effectue la phase 2, l’environnement de préproduction se trouve dans l’environnement du fabricant OEM.  

#### <a name="overview-of-mdt-configuration-files-in-the-oem-preload-process"></a>Vue d’ensemble des fichiers de configuration MDT dans le processus de préchargement OEM  
 Des fichiers de configuration MDT distincts (CustomSettings.ini et Bootstrap.ini) sont utilisés dans les séquences de tâches exécutées pendant la phase 1 et la phase 3 du processus de préchargement OEM. Toutefois, les deux fichiers de configuration existent simultanément dans différentes structures de dossier.  

 Dans la première phase, les fichiers de configuration sont utilisés pendant la création de l’ordinateur de référence et sont stockés dans le dossier propre à la séquence de tâches utilisée dans cette phase. Les fichiers de configuration utilisés dans la troisième et la dernière phase du processus de préchargement OEM sont stockés dans le dossier propre à la séquence de tâches utilisée dans cette phase.  

 Quand vous modifiez les fichiers de configuration, vérifiez que les changements effectués correspondent à la séquence de tâches appropriée dans chaque phase du processus de préchargement OEM.  

#### <a name="overview-of-mdt-log-files-in-the-oem-preload-process"></a>Vue d’ensemble des fichiers journaux MDT dans le processus de préchargement OEM  
 Des fichiers journaux MDT distincts sont générés pendant la phase 1 et la phase 3 du processus de préchargement OEM :  

-   Les fichiers journaux MDT de la phase 1 sont stockés dans les dossiers C:\MININT et C:\SMSTSLog.  

-   Les fichiers journaux MDT de la phase 3 sont stockés dans le dossier %WINDIR%\System32\CCM\Logs pour les déploiements x86 ou dans le dossier %WINDIR%\SysWow64\CCM\Logs pour les déploiements x64.  

 Utilisez le dossier approprié quand vous diagnostiquez ou résolvez les problèmes de déploiement liés à MDT.  

### <a name="staged-deployments-using-lti"></a>Déploiements intermédiaires à l’aide de LTI  
 Pour les déploiements LTI, effectuez le processus de préchargement OEM à l’aide d’un type de partage de déploiement *Support amovible (support)*. Les autres types de partage de déploiement ne sont pas pris en charge pour le processus de préchargement OEM.  

 Pour exécuter le processus de préchargement OEM, créez une séquence de tâches basée sur le modèle de séquence de tâches LiteTouch OEM Task Sequence, en plus des séquences de tâches utilisées pour déployer le système d’exploitation cible. Ensuite, créez un partage de déploiement *Support amovible (support)* qui crée un fichier ISO du contenu du partage de déploiement, en particulier le fichier LiteTouchPE_x86.iso ou le fichier LiteTouchPE_x64.iso (en fonction de la plateforme du processeur de l’ordinateur cible). Le processus de mise à jour du partage de déploiement crée également une structure de dossiers qui peut être utilisée pour créer un support Universal Disk Format.  

#### <a name="lti-oem-preload-processphase-1-create-a-media-based-image"></a>Processus de préchargement OEM LTI - Phase 1 : Créer une image basée sur un support  
 L’organisation de déploiement exécute la première phase du processus de préchargement OEM. Le livrable final de cette phase est une image de démarrage (par exemple, un fichier ISO) ou un support (par exemple, un DVD) qui est envoyé à l’OEM ou à l’environnement de préproduction dans l’organisation de déploiement. La plupart de ces étapes sont exécutées dans Deployment Workbench.  

 **Pour créer une image basée sur un support à envoyer à l’OEM ou à l’environnement de préproduction dans l’organisation de déploiement**  

1.  Remplissez les nœuds suivants pour le partage de déploiement dans Deployment Workbench :  

    -   Systèmes d'exploitation  

    -   Applications  

    -   Packages  

    -   Pilotes prêts à l’emploi  

     Pour plus d’informations sur l’exécution de cette étape, consultez la section « Managing Deployment Shares in the Deployment Workbench » (Gestion de partages de déploiement dans Deployment Workbench), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

2.  Créez une séquence de tâches basée sur le modèle Litetouch OEM Task Sequence dans Deployment Workbench.  

     Pour plus d’informations sur l’exécution de cette étape, consultez la section « Configuring Task Sequences in the Deployment Workbench » (Configuration des séquences de tâches dans Deployment Workbench), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

3.  Créez une ou plusieurs séquences de tâches utilisées pour déployer le système d’exploitation cible sur l’ordinateur cible après le déploiement dans l’environnement de production.  

     Pour plus d’informations sur l’exécution de cette étape, consultez la section « Configuring Task Sequences in the Deployment Workbench » (Configuration des séquences de tâches dans Deployment Workbench), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

4.  Créez un profil de sélection comprenant les applications, les systèmes d’exploitation, les pilotes, les packages et les séquences de tâches nécessaires pour le déploiement OEM.  

     Pour plus d’informations sur l’exécution de cette étape, consultez la section « Manage Selection Profile » (Gérer les profils de sélection), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

5.  Créez un support de déploiement.  

     Pour plus d’informations sur l’exécution de cette étape, consultez la section « Manage LTI Deployment Media » (Gérer le support de déploiement LTI), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

6.  Mettez à jour le support de déploiement créé dans Deployment Workbench à l’étape précédente.  

     Quand vous mettez à jour le support de déploiement, Deployment Workbench crée le fichier LiteTouchMedia.iso. Pour plus d’informations sur l’exécution de cette étape, consultez la section « Manage LTI Deployment Media » (Gérer le support de déploiement LTI), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

7.  Gravez un DVD du fichier LiteTouchMedia.iso créé à l’étape précédente.  

    > [!NOTE]
    >  Si vous remettez le fichier ISO à l’OEM ou à l’environnement de préproduction de l’organisation, cette étape n’est pas nécessaire.  

8.  Remettez le fichier ISO ou le DVD à l’OEM ou à l’environnement de préproduction de l’organisation.  

#### <a name="lti-oem-preload-processphase-2-apply-the-image-to-the-target-computer"></a>Processus de préchargement OEM LTI - Phase 2 : Appliquer l’image à l’ordinateur cible  
 La deuxième phase du processus de préchargement OEM est exécutée par l’OEM ou par l’équipe de déploiement dans l’environnement de préproduction de l’organisation de déploiement. Pendant cette phase du processus, le fichier .iso ou le DVD créé à la phase 1 est appliqué aux ordinateurs cibles. Le livrable de cette phase est l’image déployée sur les ordinateurs cibles pour qu’ils soient prêts pour le déploiement dans l’environnement de production.  

 **Pour appliquer l’image aux ordinateurs cibles**  

1.  Démarrez un ordinateur cible avec le support créé dans la phase 1.  

     Windows PE démarre, puis l’Assistant de déploiement Windows.  

2.  Dans l’Assistant de déploiement Windows, cliquez sur la séquence de tâches **OEM Preinstallation Task Sequence for Staging Environment** (Séquence de tâches de préinstallation OEM pour l’environnement de préproduction).  

     La séquence de tâches démarre et le contenu du support de démarrage est copié sur le disque dur local de l’ordinateur cible.  

3.  Quand l’Assistant de déploiement Windows est exécuté pour la séquence de tâches **OEM Preinstallation Task Sequence for Staging Environment** (Séquence de tâches de préinstallation OEM pour l’environnement de préproduction), le disque dur est prêt à lancer le reste du processus de déploiement en exécutant l’Assistant de déploiement Windows pour les autres séquences de tâches utilisées dans le déploiement du système d’exploitation.  

     La séquence de tâches **OEM Preinstallation Task Sequence for Staging Environment** (Séquence de tâches de préinstallation OEM pour l’environnement de préproduction) est chargée de déployer l’image sur l’ordinateur cible et de lancer le processus LTI. L’Assistant de déploiement Windows démarre une deuxième fois pour exécuter les séquences de tâches utilisées pour déployer le système d’exploitation sur l’ordinateur cible.  

4.  Clonez le contenu du premier disque dur sur le nombre d’ordinateurs cibles dont vous avez besoin dans l’environnement de préproduction.  

5.  Les ordinateurs cibles sont remis à l’environnement de production pour le déploiement.  

#### <a name="lti-oem-preload-processphase-3-complete-target-computer-deployment"></a>Processus de préchargement OEM LTI - Phase 3 : Exécuter le déploiement des ordinateurs cibles  
 La troisième et dernière phase du processus de préchargement OEM est exécutée dans l’environnement de production de l’organisation de déploiement. Pendant cette phase du processus, l’ordinateur cible est démarré et l’image du support de démarrage, placée sur le disque dur dans l’environnement de préproduction pendant la phase précédente, démarre.  

 **Pour exécuter le déploiement des ordinateurs cibles dans l’environnement de production**  

1.  Démarrez l’ordinateur cible.  

     Windows PE démarre, puis l’Assistant de déploiement Windows.  

2.  Exécutez l’Assistant de déploiement Windows à l’aide des informations de configuration spécifiques de chaque ordinateur cible.  

     Pour plus d’informations sur l’exécution de cette étape, consultez la section « Running the Deployment Wizard » (Exécuter l’Assistant de déploiement), dans le document MDT *Using the Microsoft Deployment Toolkit* (Utilisation de Microsoft Deployment Toolkit).  

 Une fois la phase exécutée, l’ordinateur cible est prêt à être utilisé dans l’environnement de production.  

## <a name="using-windows-powershell-to-perform-common-tasks"></a>Utilisation de Windows PowerShell pour effectuer des tâches courantes  
 Les tâches d’administration MDT dans Deployment Workbench sont effectuées par les applets de commande Windows PowerShell sous-jacentes, que vous pouvez utiliser pour automatiser les tâches administratives comme celles des sections suivantes.  

 Vous pouvez automatiser l’administration de MDT en effectuant les étapes suivantes :  

-   Créer un partage de déploiement comme décrit dans [Création d’un partage de déploiement](#CreateNewDeployShare).  

-   Créer un dossier dans un partage de déploiement comme décrit dans [Création d’un dossier](#CreateFolder).  

-   Supprimer un dossier dans un partage de déploiement comme décrit dans [Suppression d’un dossier](#DeleteFolder).  

-   Importer un pilote de périphérique dans un partage de déploiement comme décrit dans [Importation d’un pilote de périphérique](#ImportDeviceDriver).  

-   Supprimer un pilote de périphérique dans un partage de déploiement comme décrit dans [Suppression d’un pilote de périphérique](#DeleteDeviceDriver).  

-   Importer un package de système d’exploitation dans un partage de déploiement comme décrit dans [Importation d’un package de système d’exploitation](#ImportOpSysPackage).  

-   Supprimer un package de système d’exploitation dans un partage de déploiement comme décrit dans [Suppression d’un package de système d’exploitation](#DeleteOpSysPackage).  

-   Importer un système d’exploitation dans un partage de déploiement comme décrit dans [Importation d’un système d’exploitation](#ImportOpSys).  

-   Supprimer un système d’exploitation dans un partage de déploiement comme décrit dans [Suppression d’un système d’exploitation](#DeleteOpSys).  

-   Créer une application dans un partage de déploiement comme décrit dans [Création d’une application](#CreateApplication).  

-   Supprimer une application dans un partage de déploiement comme décrit dans [Suppression d’une application](#DeleteApplication).  

-   Créer une séquence de tâches dans un partage de déploiement comme décrit dans [Création d’une séquence de tâches](#CreateTaskSequence).  

-   Supprimer une séquence de tâches dans un partage de déploiement comme décrit dans [Suppression d’une séquence de tâches](#DeleteTaskSequence).  

-   Créez une base de données MDT comme décrit dans [Création d’une base de données MDT](#CreateMDTDB).  

-   Créer un profil de sélection comme décrit dans [Création d’un profil de sélection](#CreateSelectProfile).  

-   Mettre à jour un partage de déploiement comme décrit dans [Mise à jour d’un partage de déploiement](#UpdatingDeployShare).  

-   Créer un partage de déploiement lié comme décrit dans [Création d’un partage de déploiement lié](#CreateLinkedDeployShare).  

-   Mettre à jour un partage de déploiement lié comme décrit dans [Mise à jour d’un partage de déploiement lié](#UpdatingLinkedDeployShare).  

-   Supprimer un partage de déploiement lié comme décrit dans [Suppression d’un partage de déploiement lié](#DeleteLinkedDeployShare).  

-   Créer un support de déploiement comme décrit dans [Création d’un support](#CreateMedia).  

-   Générer un support de déploiement comme décrit dans [Génération d’un support](#GenerateMedia).  

-   Supprimer un support de déploiement comme décrit dans [Suppression d’un support](#DeleteMedia).  

###  <a name="CreateNewDeployShare"></a> Création d’un partage de déploiement  
 Les commandes Windows PowerShell suivantes créent un partage de déploiement dans D:\Production Deployment Share nommé *Production$*. Le nouveau partage de déploiement s’affiche dans Deployment Workbench comme Production.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider "MDTProvider" -Root "D:\Production Deployment Share" -Description "Production" -NetworkPath "\\Deployment_Server\Production$" -Verbose | add-MDTPersistentDrive -Verbose  
    ```  

###  <a name="CreateFolder"></a> Création d’un dossier  
 Les commandes Windows PowerShell suivantes créent un dossier Adobe dans l’arborescence de la console Deployment Workbench dans Deployment Workbench\/Deployment Shares\/Production\/Applications.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Applications" -enable "True" -Name "Adobe" -Comments "This folder contains Adobe software" -ItemType "folder" -Verbose remove-psdrive DS001 -Verbose  
    ```  

    > [!NOTE]
    >  Ajoutez « `remove-psdrive` » au script pour garantir que le processus d’arrière-plan se termine avant de continuer.  

###  <a name="DeleteFolder"></a> Suppression d’un dossier  
 Les commandes Windows PowerShell suivantes suppriment le dossier Deployment Workbench\/Deployment Shares\/Production\/Applications\/Adobe.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Remove-item -path "DS002:\Applications\Adobe" -Verbose  
    ```  

> [!NOTE]
>  Le script échoue si le dossier n’est pas vide.  

###  <a name="ImportDeviceDriver"></a> Importation d’un pilote de périphérique  
 Les commandes Windows PowerShell suivantes importent le pilote de périphérique du moniteur Dell 2407 WFP dans le partage de déploiement Production.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtdriver -path "DS002:\Out-of-Box Drivers\Monitor" -SourcePath "D:\Drivers\Dell\2407 WFP" -Verbose  
    ```  

###  <a name="DeleteDeviceDriver"></a> Suppression d’un pilote de périphérique  
 Les commandes Windows PowerShell suivantes suppriment le pilote de périphérique du moniteur Dell 2407 WFP dans le partage de déploiement Production.  

```  
Remove-item -path "DS002:\Out-of-Box Drivers\Dell Inc. Monitor 2407WFP.INF 1.0" -Verbose  
```  

###  <a name="ImportOpSysPackage"></a> Importation d’un package de système d’exploitation  
 Les commandes Windows PowerShell suivantes importent tous les packages de système d’exploitation situés sous D:\\Updates\\Microsoft\\Vista. Ces packages de système d’exploitation sont stockés dans le partage de déploiement Production, qui se trouve dans D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtpackage -path "DS002:\Packages" -SourcePath "D:\Updates\Microsoft\Vista" -Verbose  
    ```  

###  <a name="DeleteOpSysPackage"></a> Suppression d’un package de système d’exploitation  
 Les commandes Windows PowerShell suivantes suppriment le package de système d’exploitation spécifié dans le partage de déploiement Production.  

```  
Remove-item -path "DS002:\Packages\Package_1_for_KB940105 neutral x86 6.0.1.0 KB940105" -Verbose  
```  

###  <a name="ImportOpSys"></a> Importation d’un système d’exploitation  
 Les commandes Windows PowerShell suivantes importent le système d’exploitation Windows Vista situé dans D:\\Operating Systems\\Windows Vista x86. Ce système d’exploitation est stocké dans le partage de déploiement Production, qui se trouve dans D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdtoperatingsystem -path "DS002:\Operating Systems" -SourcePath "D:\Operating Systems\Windows Vista x86" -DestinationFolder "Windows Vista x86" -Verbose  
    ```  

###  <a name="DeleteOpSys"></a> Suppression d’un système d’exploitation  
 Les commandes Windows PowerShell suivantes suppriment le système d’exploitation Windows Vista HOMEBASIC spécifié dans le partage de déploiement Production.  

```  
Remove-item -path "DS002:\Operating Systems\Windows Vista HOMEBASIC in Windows Vista x86 install.wim" -Verbose  
```  

###  <a name="CreateApplication"></a> Création d’une application  
 Les commandes Windows PowerShell suivantes créent l’application Adobe Reader 9 à l’aide des fichiers sources dans D:\\Software\\Adobe\\Reader 9. L’application est stockée dans le partage de déploiement Production, qui se trouve dans D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-MDTApplication -path "DS002:\Applications" -enable "True" -Name "Adobe Reader 9" -ShortName "Reader" -Version "9" -Publisher "Adobe" -Language "" -CommandLine "setup.exe" -WorkingDirectory ".\Applications\Adobe Reader 9" -ApplicationSourcePath "D:\Software\Adobe\Reader 9" -DestinationFolder "Adobe Reader 9" -Source ".\Applications\Adobe Reader 9" -Verbose  
    ```  

###  <a name="DeleteApplication"></a> Suppression d’une application  
 Les commandes Windows PowerShell suivantes suppriment l’application Adobe Reader 9 dans le partage de déploiement Production.  

```  
Remove-item -path "DS002:\Applications\Adobe Reader 9" -Verbose  
```  

###  <a name="CreateTaskSequence"></a> Création d’une séquence de tâches  
 Les commandes Windows PowerShell suivantes créent la séquence de tâches **Windows Vista Production Build** (Build de production Windows Vista) dans le partage de déploiement Production, qui se trouve dans D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Import-mdttasksequence -path "DS002:\Task Sequences" -Name "Windows Vista Business Production Build" -Template "Client.xml" -Comments "Approved for use in the production environment.  This task sequence uses the Standard Client task sequence template" -ID "Vista_Ref" -Version "1.0" -OperatingSystemPath "DS002:\Operating Systems\Windows Vista BUSINESS in Windows Vista x86 install.wim" -FullName "Fabrikam User" -OrgName "Fabrikam" -HomePage "http://www.Fabrikam.com" -AdminPassword "secure_password" -Verbose  
    ```  

###  <a name="DeleteTaskSequence"></a> Suppression d’une séquence de tâches  
 Les commandes Windows PowerShell suivantes suppriment la séquence de tâches **Windows Vista Production Build** dans le partage de déploiement Production.  

```  
Remove-item -path "DS002:\Task Sequences\Windows Vista Business Production Build" -force -Verbose  
```  

###  <a name="CreateMDTDB"></a> Création d’une base de données MDT  
 Les commandes Windows PowerShell suivantes créent une base de données MDT sur le serveur *serveur\_déploiement* pour le partage de déploiement Production. La connexion de base de données se fait par TCP\/IP.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-MDTDatabase -path "DS002:" -SQLServer "DeploymentServer" -Netlib "DBMSSOCN" -Database "MDT2010" -SQLShare "DB_Connect" -Force -Verbose  
    ```  

###  <a name="CreateSelectProfile"></a> Création d’un profil de sélection  
 Les commandes Windows PowerShell suivantes créent un profil de sélection Applications.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Selection Profiles" -enable "True" -Name "Applications" -Comments "" -Definition "<SelectionProfile><Include path="Applications" /></SelectionProfile>" -ReadOnly "False" -Verbose  
    ```  

###  <a name="UpdatingDeployShare"></a> Mise à jour d’un partage de déploiement  
 Les commandes Windows PowerShell suivantes mettent à jour le partage de déploiement Production, qui se trouve dans D:\\Production Deployment Share.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  
    
-   ```
    Update\-MDTDeploymentShare \-path "DS002:" \-Verbose  
    ```
    
###  <a name="CreateLinkedDeployShare"></a> Création d’un partage de déploiement lié  
 Les commandes Windows PowerShell suivantes créent un partage de déploiement qui est lié au partage de déploiement Production et se trouve sous le partage \\\\*nom\_serveur\_distant*\\Deployment$. Le profil de sélection Everything est utilisé pour déterminer le contenu qui est répliqué dans le partage de déploiement lié. Le contenu du partage de déploiement Production est fusionné avec le contenu qui existe déjà dans le partage \\\\*nom\_serveur\_distant*\\Deployment$.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Linked Deployment Shares" -enable "True" -Name "LINKED001" -Comments "" -Root "\\RemoteServerName\Deployment$" -SelectionProfile "Everything" -Replace "False" -Verbose  
    ```  

###  <a name="UpdatingLinkedDeployShare"></a> Mise à jour d’un partage de déploiement lié  
 Les commandes Windows PowerShell suivantes mettent à jour le partage de déploiement LINKED001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Replicate-MDTContent -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="DeleteLinkedDeployShare"></a> Suppression d’un partage de déploiement lié  
 Les commandes Windows PowerShell suivantes suppriment le partage de déploiement LINKED001.  

-   Add\-PSSnapIn Microsoft.BDD.PSSnapIn  

-   ```  
    Remove-item -path "DS002:\Linked Deployment Shares\LINKED001" -Verbose  
    ```  

###  <a name="CreateMedia"></a> Création du support  
 Les commandes Windows PowerShell suivantes créent un dossier source avec le contenu utilisé pour créer un support de démarrage. Le partage de déploiement Production est utilisé comme source. Le profil de sélection Everything détermine le contenu placé dans le dossier de contenu du support. Le fichier LiteTouchMedia.iso est créé quand le support est généré. Le support prend en charge les plateformes x86 et x64.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    New-item -path "DS002:\Media" -enable "True" -Name "MEDIA001" -Comments "some comment here" -Root "D:\Media" -SelectionProfile "Everything" -SupportX86 "True" -SupportX64 "True" -GenerateISO "True" -ISOName "LiteTouchMedia.iso" -Verbose  
    ```  

-   ```  
    New-PSDrive -Name "MEDIA001" -PSProvider "MDTProvider" -Root "D:\Media\Content" -Description "Embedded media deployment share" -Force -Verbose  
    ```  

###  <a name="GenerateMedia"></a> Génération du support  
 Les commandes Windows PowerShell suivantes créent le fichier LiteTouchMedia.iso dans D:\\Media, qui utilise le contenu du dossier source du support MEDIA001.  

-   ```  
    Add-PSSnapIn Microsoft.BDD.PSSnapIn  
    ```  

-   ```  
    New-PSDrive -Name "DS002" -PSProvider MDTProvider -Root "D:\Production Deployment Share"  
    ```  

-   ```  
    Generate-MDTMedia -path "DS002:\Media\MEDIA001" -Verbose  
    ```  

###  <a name="DeleteMedia"></a> Suppression du support  
 Les commandes Windows PowerShell suivantes suppriment le support MEDIA001 dans le partage de déploiement Production.  

```  
Remove-item -path "DS002:\Media\MEDIA001" -Verbos  
```  

## <a name="delaying-domain-join-to-avoid-application-of-group-policy-objects"></a>Retarder la jonction de domaine pour éviter l’application d’objets de stratégie de groupe  
 La stratégie de groupe est une technologie complète et flexible qui permet de gérer efficacement un grand nombre d’objets ordinateur et utilisateur Active Directory Domain Services (AD DS) à travers un modèle centralisé un-à-plusieurs. Les paramètres de stratégie de groupe sont contenus dans un objet de stratégie de groupe (GPO) et liés à un ou plusieurs conteneurs de services AD DS : sites, domaines et unités d’organisation (UO).  

 Certaines organisations ont des paramètres de stratégie de groupe restrictifs qui peuvent entraîner des problèmes pendant les déploiements de système d’exploitation. Par exemple, les paramètres de stratégie de groupe suivants peuvent interrompre un processus d’ouverture de session automatique :  

-   Restrictions d’ouverture de session automatique  

-   Renommage du compte d’administrateur  

-   Légendes et bannières juridiques  

-   Stratégies de sécurité restrictives (par exemple, la stratégie Specialized Security - Limited Functionality [SSFL])  

 Pour résoudre les problèmes qu’un GPO peut entraîner pendant le déploiement, joignez l’ordinateur au domaine le plus tard possible dans le processus de déploiement. Cette jonction peut être effectuée à l’aide d’une étape de séquence de tâches personnalisée qui exécute le script ZTIDomainJoin.wsf.  

 Pour joindre l’ordinateur cible au domaine, le script ZTIDomainJoin.wsf utilise les propriétés **DomainAdmin**, **DomainAdminDomain**, **DomainAdminPassword**, **JoinDomain** et **MachineObjectOU**. Vous pouvez déclarer ces propriétés à l’aide de l’Assistant de déploiement Windows, des règles de partage de déploiement, de la base de données MDT et des règles de regroupement et d’ordinateur Configuration Manager. Le compte utilisé doit disposer les droits nécessaires pour créer et supprimer des objets ordinateur dans le domaine.  

 En règle générale, le script ZTIConfigure.wsf met à jour le fichier Unattend.xml ou Unattend.txt avec les valeurs que ces propriétés spécifient. Ces paramètres sont ensuite analysés par le programme d’installation de Windows, et le système tente d’effectuer la jonction au domaine tôt dans le processus de déploiement. L’ordinateur cible reçoit alors les paramètres spécifiés dans les GPO et peut entraîner l’échec du processus de déploiement.  

 Pour différer intentionnellement la jonction de l’ordinateur cible au domaine pendant le processus de déploiement, vous pouvez supprimer certains éléments du fichier Unattend.xml. Le script ZTIConfigure.wsf ignore l’écriture de propriétés dans le fichier Unattend.xml si l’élément de propriété associé est manquant dans le fichier.  

> [!NOTE]
>  Cet exemple de solution de contournement est valide uniquement quand vous déployez les systèmes d’exploitation Windows 7, Windows Server 2008 ou Windows Server 2008 R2.  

 **Préparer le fichier unattend.xml pour que l’ordinateur cible ne tente pas de joindre le domaine pendant l’installation de Windows**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences/*séquence_tâches* (où *partage_déploiement* est le nom du partage de déploiement et *séquence_tâches* est le nom de la séquence de tâches à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Sous l’onglet **OS Info** (Informations du système d’exploitation), cliquez sur **Edit Unattend.xml** (Modifier Unattend.xml).  

     Windows System Image Manager (Windows SIM) démarre.  

5.  Dans le volet **Answer File** (Fichier de réponses), accédez à **4 specialize/Identification/Credentials**. Cliquez avec le bouton droit sur **Credentials** (Informations d’identification), puis cliquez sur **Delete**.  

6.  Cliquez sur **Oui**.  

7.  Enregistrer le fichier de réponses, puis quittez Windows SIM.  

8.  Cliquez sur **OK** dans la boîte de dialogue **Properties** (Propriétés) de la séquence de tâches.  

 Comme les éléments `Credentials` sont manquants dans le fichier unattend.xml, le script ZTIConfigure.wsf ne peut pas remplir les informations de jonction de domaine dans le fichier Unattend.xml, ce qui empêche le programme d’installation de Windows d’essayer de joindre le domaine.  

 **Pour ajouter une étape de séquence de tâches qui joint l’ordinateur cible au domaine**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft Deployment Toolkit**, puis cliquez sur **Deployment Workbench**.  

2.  Dans l’arborescence de la console Deployment Workbench, accédez à Deployment Workbench/Deployment Shares/*partage_déploiement*/Task Sequences/*séquence_tâches* (où *partage_déploiement* est le nom du partage de déploiement et *séquence_tâches* est le nom de la séquence de tâches à configurer).  

3.  Dans le volet Actions, cliquez sur **Properties** (Propriétés).  

4.  Sous l’onglet **Task Sequence** (Séquence de tâches), développez le nœud de restauration de l’état.  

5.  Vérifiez que l’étape de séquence de tâches **Recover From Domain** (Récupérer à partir du domaine) est présente. Si oui, passez à l’étape 9.  

6.  Dans la boîte de dialogue **Properties** (Propriétés) de la séquence de tâches, cliquez sur **Add** (Ajouter), accédez à **Settings** (Paramètres), puis cliquez sur **Recover From Domain** (Récupérer à partir du domaine).  

7.  Ajoutez l’étape de séquence de tâches **Recover From Domain** (Récupérer à partir du domaine) à l’éditeur de séquence de tâches. Vérifiez que l’étape se trouve dans l’emplacement souhaité dans la séquence de tâches.  

8.  Vérifiez que les paramètres de l’étape de séquence de tâches **Recover From Domain** (Récupérer à partir du domaine) sont configurés selon vos besoins.  

9. Cliquez sur **OK** dans la boîte de dialogue **Properties** (Propriétés) de la séquence de tâches pour enregistrer la séquence de tâches.
