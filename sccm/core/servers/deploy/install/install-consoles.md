---
title: Installer la console
titleSuffix: Configuration Manager
description: Installez la console Configuration Manager pour vous connecter à un site d’administration centrale ou à un site principal.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebbbf62bb3cc1e2b96d83ad109064d643544fdb9
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498248"
---
# <a name="install-the-configuration-manager-console"></a>Installer la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les administrateurs se servent de la console Configuration Manager pour gérer l’environnement Configuration Manager. Chaque console Configuration Manager peut se connecter à un site d’administration centrale (CAS) ou à un site principal. Vous ne pouvez pas connecter une console Configuration Manager à un site secondaire.

La console Configuration Manager est toujours installée sur le serveur de site pour le site d’administration centrale ou un site principal. Pour installer la console indépendamment du serveur de site, exécutez le programme d’installation autonome.  



## <a name="prerequisites"></a>Prérequis

- Les droits **d’administrateur** local sur l’ordinateur cible pour la console.  

- Les droits de **Lecture** sur l’emplacement des fichiers d’installation de la console Configuration Manager.  



## <a name="source-paths"></a>Chemins source

Déterminer le chemin source à utiliser :  

- Dossier ConsoleSetup sur le serveur de site : `<Configuration Manager site server installation path>\Tools\ConsoleSetup`  

    Quand vous installez un serveur de site, il copie les fichiers d’installation de la console et les modules linguistiques pris en charge pour le site dans le sous-dossier **Tools\ConsoleSetup**. Vous pouvez éventuellement copier le dossier **ConsoleSetup** vers un autre emplacement pour démarrer l’installation. Lorsque vous mettez à jour le site, il conserve toujours sa version locale à jour.  

- Support d’installation de Configuration Manager : `<Configuration Manager installation media>\SMSSETUP\BIN\I386`  

    Quand vous installez la console Configuration Manager à partir du support d’installation, la version anglaise est toujours installée. Ce comportement se produit même si le serveur de site prend en charge différentes langues ou qu’une autre langue est définie sur le système d’exploitation de l’ordinateur cible.  

Dans la mesure du possible, démarrez le programme d’installation de la console à partir du dossier **ConsoleSetup** plutôt qu’à partir du support source.

> [!Important]  
> N’installez pas la console en utilisant les fichiers source **CD.Latest**. Il s’agit d’un scénario non pris en charge qui peut entraîner des problèmes lors de l’installation de la console. Pour plus d’informations, consultez [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder#unsupported-scenarios).<!-- SCCMDocs issue 1359 -->  

Si vous créez un package pour configurer la console sur d’autres ordinateurs, assurez-vous que le package inclut les fichiers suivants :<!--3612513-->

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab (démarré dans la version 1902)
- ConfigMgr.AC_Extension.amd64.cab (démarré dans la version 1902)



## <a name="use-the-setup-wizard"></a>Utiliser l’Assistant Installation  

1. Accédez au chemin source, puis ouvrez **ConsoleSetup.exe**.  

    > [!IMPORTANT]  
    > Installez toujours la console à l’aide de la commande **Consolesetup.exe**. Même si vous pouvez installer la console Configuration Manager en exécutant AdminConsole.msi, cette méthode n’effectue pas de vérification des prérequis ni des dépendances. Il se peut que l’installation ne se déroule pas correctement.  

2. Dans l’Assistant, sélectionnez **Suivant**.  

3. Dans la page **Serveur de site**, entrez le nom de domaine complet (FQDN) du serveur de site auquel la console Configuration Manager se connecte.  

4. Dans la page **Dossier d’installation**, entrez le dossier d’installation de la console Configuration Manager. Le chemin du dossier ne peut pas contenir d’espaces de fin ni de caractères Unicode.  

5. Dans la page **Programme d’amélioration des services**, indiquez si vous voulez participer à ce programme.  

    > [!Note]  
    > À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

6. Dans la page **Prêt pour l’installation**, sélectionnez **Installer**.  



## <a name="install-from-a-command-prompt"></a>Installer à partir d’une invite de commandes  

> [!TIP]  
> Quand vous installez la console Configuration Manager à partir d’une invite de commandes, la version anglaise est toujours installée. Ce comportement se produit même si une autre langue est définie sur le système d’exploitation de l’ordinateur cible. Pour installer la console Configuration Manager dans une langue autre que l’anglais, [utilisez l’Assistant d’installation](#use-the-setup-wizard).  


### <a name="consolesetupexe-command-line-options"></a>Options de ligne de commande ConsoleSetup.exe

#### <a name="q"></a>/q

Installe la console Configuration Manager sans assistance. Les options **EnableSQM**, **TargetDir**et **DefaultSiteServerName** sont obligatoires avec cette option.

#### <a name="uninstall"></a>/uninstall

Désinstalle la console Configuration Manager. Spécifiez cette option en premier quand vous l’utilisez avec l’option **/q**.

#### <a name="langpackdir"></a>LangPackDir

Spécifie le chemin d'accès au dossier qui contient les fichiers de langue. Vous pouvez utiliser le **téléchargeur d’installation** pour télécharger les fichiers de langue. Si vous n’utilisez pas cette option, le programme d’installation recherche le dossier de langue dans le dossier actuel. Si le dossier de langue n’est pas trouvé, le programme d’installation poursuit l’installation en anglais uniquement. Pour plus d’informations, consultez [Téléchargeur d’installation](setup-downloader.md).

#### <a name="targetdir"></a>TargetDir

Spécifie le dossier où installer la console Configuration Manager. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .

#### <a name="enablesqm"></a>EnableSQM

Permet de préciser si vous souhaitez vous joindre au programme d'amélioration de l'expérience utilisateur. Utilisez la valeur **1** pour participer au programme d’amélioration des services et la valeur **0** pour ne pas participer au programme. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .

> [!Important]  
> À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit. L’utilisation du paramètre entraînera l’échec de l’installation.

#### <a name="defaultsiteservername"></a>DefaultSiteServerName

Spécifie le nom de domaine complet du serveur de site auquel la console se connecte à son ouverture. Vous devez spécifier cette option lorsque vous utilisez l’option **/q** .


### <a name="examples"></a>Exemples

> [!Important]  
> La version 1802 et les versions ultérieures n’incluent pas le paramètre **EnableSQM**

#### <a name="silent-install"></a>Installation silencieuse

`ConsoleSetup.exe /q TargetDir="%ProgramFiles%\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com`

#### <a name="silent-install-with-language-packs"></a>Installation silencieuse avec des packs linguistiques

`ConsoleSetup.exe /q TargetDir="C:\Program Files\ConfigMgr Console" DefaultSiteServerName=MyServer.Contoso.com LangPackDir=C:\Downloads\ConfigMgr`  

#### <a name="silent-uninstall"></a>Désinstallation silencieuse

`ConsoleSetup.exe /uninstall /q`  



## <a name="see-also"></a>Voir aussi

Les objets visibles par l’administrateur dans la console dépendent des autorisations attribuées à son compte d’utilisateur. Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).

Pour plus d’informations sur les principes fondamentaux de la navigation dans les interfaces utilisateur de la console Configuration Manager, consultez [Utilisation de la console](/sccm/core/servers/manage/admin-console).
