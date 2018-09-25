---
title: Installer la console
titleSuffix: Configuration Manager
description: Installez la console Configuration Manager pour vous connecter à un site d’administration centrale ou à un site principal.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a8d1d0a727f0a4ad4a2bfc25141f7e2982494080
ms.sourcegitcommit: b596d944e49f3c4912c6ca91915ed1418c17a1a2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42584941"
---
# <a name="install-the-system-center-configuration-manager-console"></a>Installer la console System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les administrateurs se servent de la console Configuration Manager pour gérer l’environnement Configuration Manager. Chaque console Configuration Manager peut se connecter à un site d’administration centrale ou à un site principal, Vous ne pouvez pas connecter une console Configuration Manager à un site secondaire.

> [!NOTE]  
>  Les objets visibles par l’administrateur dans la console dépendent des autorisations attribuées à son compte d’utilisateur. Pour plus d’informations sur l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles](../../../../core/understand/fundamentals-of-role-based-administration.md).  

 Quand vous installez le serveur de site, vous pouvez installer la console Configuration Manager en même temps. Pour installer la console indépendamment du serveur de site, exécutez le programme d’installation autonome.  

 Utilisez les procédures suivantes pour installer la console Configuration Manager à l’aide du programme d’installation autonome.  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>Pour installer la console Configuration Manager à l’aide de l’Assistant Installation  

1.  Vérifiez que vous disposez des droits suivants :  

    -  Les droits **d’administrateur** local sur l’ordinateur cible pour la console.  

    -   Les droits de **Lecture** sur l’emplacement des fichiers d’installation de la console Configuration Manager.  

2.  Accédez à l’un des emplacements suivants :  

    -   Sur le serveur de site, accédez à : `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   À partir du support source Configuration Manager, accédez à : `<Configuration Manager source files>\Smssetup\Bin\I386`  

    > [!TIP]  
    >  Au titre des bonnes pratiques, démarrez le programme d’installation de la console Configuration Manager à partir d’un serveur de site plutôt que du support d’installation System Center Configuration Manager. Quand vous installez un serveur de site, il copie les fichiers d’installation de la console Configuration Manager et les modules linguistiques pris en charge pour le site dans le sous-dossier **Tools\ConsoleSetup**. Quand vous installez la console Configuration Manager à partir du support d’installation, la version anglaise est toujours installée. Ce comportement se produit même si le serveur de site prend en charge différentes langues ou qu’une autre langue est définie sur le système d’exploitation de l’ordinateur cible. Vous pouvez éventuellement copier le dossier **ConsoleSetup** vers un autre emplacement pour démarrer l’installation.

3.  Pour ouvrir l’Assistant Installation de la console Configuration Manager, double-cliquez sur **consolesetup.exe**.  

    > [!IMPORTANT]  
    >  Installez toujours la console Configuration Manager à l’aide de la commande **consolesetup.exe**. Même si vous pouvez installer la console Configuration Manager en exécutant adminconsole.msi, cette méthode n’effectue pas de vérification des prérequis ni des dépendances. Il se peut que l’installation ne se déroule pas correctement.  

4.  Dans l’Assistant, sélectionnez **Suivant**.  

5.  Dans la page **Serveur de site**, entrez le nom de domaine complet (FQDN) du serveur de site auquel la console Configuration Manager se connecte.  

6.  Dans la page **Dossier d’installation**, entrez le dossier d’installation de la console Configuration Manager. Le chemin du dossier ne doit pas contenir d'espaces de fin ni de caractères Unicode.  

7.  Dans la page **Programme d’amélioration des services**, indiquez si vous voulez participer à ce programme.  
    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

8.  Dans la page **Prêt pour l’installation**, cliquez sur **Installer** pour installer la console Configuration Manager.  



## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>Pour installer la console Configuration Manager à partir d’une invite de commandes  

1.  Sur le serveur à partir duquel vous installez la console Configuration Manager, ouvrez une fenêtre d’invite de commandes et accédez à l’un des emplacements suivants :  

    -   `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    -   `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    > [!TIP]  
    >  Quand vous installez la console Configuration Manager à partir d’une invite de commandes, la version anglaise est toujours installée. Ce comportement se produit même si une autre langue est définie sur le système d’exploitation de l’ordinateur cible. Pour installer la console Configuration Manager dans une langue autre que l’anglais, vous devez [installer la console Configuration Manager à l’aide de l’Assistant Installation](#to-install-the-configuration-manager-console-by-using-the-setup-wizard).  

2.  À partir de l’invite de commandes, tapez **consolesetup.exe**. Choisissez l’une des options de ligne de commande suivantes :  

|  Option de ligne de commande     | Description     |
  |-------------|-------------|
  |/q|Installe la console Configuration Manager sans assistance. Les options **EnableSQM**, **TargetDir**et **DefaultSiteServerName** sont obligatoires avec cette option.|  
  |/uninstall|Désinstalle la console Configuration Manager. Spécifiez cette option en premier quand vous l’utilisez avec l’option **/q**.|  
  |LangPackDir|Spécifie le chemin d'accès au dossier qui contient les fichiers de langue. Vous pouvez utiliser le **téléchargeur d’installation** pour télécharger les fichiers de langue. Si vous n'utilisez pas cette option, le programme d'installation recherche le dossier de langue dans le dossier actuel. Si le dossier de langue n'est pas trouvé, le programme d'installation poursuit l'installation en anglais uniquement. Pour plus d’informations, consultez [Téléchargeur d’installation](setup-downloader.md).|  
  |TargetDir|Spécifie le dossier où installer la console Configuration Manager. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  
  |EnableSQM|Permet de préciser si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur. Utilisez la valeur **1** pour participer au programme d’amélioration des services et la valeur **0** pour ne pas participer au programme. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .</br></br>Remarque : Depuis Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.  L’utilisation du paramètre entraînera l’échec de l’installation.|  
  |DefaultSiteServerName|Spécifie le nom de domaine complet du serveur de site auquel la console se connecte à son ouverture. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .|  


  ### <a name="examples"></a>Exemples
  **La version 1802 et versions ultérieures n’incluent PAS le paramètre EnableSQM**
  -  `ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

  -  `ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com EnableSQM=1  LangPackDir=C:\Downloads\ConfigMgr`  

  -  `ConsoleSetup.exe /uninstall /q`  
