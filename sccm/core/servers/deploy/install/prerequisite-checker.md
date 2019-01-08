---
title: Outil de vérification de la configuration requise
titleSuffix: Configuration Manager
description: Découvrez comment utiliser l’Outil de vérification des prérequis pour identifier et résoudre les problèmes susceptibles de bloquer l’installation d’un site ou d’un rôle de système de site.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c28152031a540ea3fd5f2ef7233c24fb86c8b7f7
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422026"
---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Outil de vérification des prérequis pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Avant d’exécuter le programme d’installation pour installer ou mettre à niveau un site System Center Configuration Manager, ou avant d’installer un rôle de système de site sur un nouveau serveur, vous pouvez utiliser cette application autonome (**Prereqchk.exe**) de la version de Configuration Manager que vous voulez utiliser pour vérifier l’état de préparation du serveur. Utilisez l’Outil de vérification des prérequis pour identifier et résoudre les problèmes susceptibles de bloquer l’installation d’un site ou d’un rôle de système de site.  

> [!NOTE]  
>  L’Outil de vérification des prérequis s’exécute toujours pendant l’installation.  

Par défaut, quand l’Outil de vérification des prérequis s’exécute :  

-   Il valide le serveur sur lequel il s’exécute.  
-   Il recherche un serveur de site sur l’ordinateur local et exécute uniquement les vérifications applicables au site.  
-   Si aucun site existant n'est détecté, toutes les règles de vérification des prérequis sont exécutées.  
-   Il vérifie les règles pour s’assurer de la présence des logiciels et des paramètres nécessaires à l’installation. Il est possible qu’un logiciel requis nécessite des configurations ou des mises à jour logicielles supplémentaires qui ne sont pas vérifiées par l’Outil de vérification des prérequis.  
-   Il enregistre ses résultats dans le fichier journal **ConfigMgrPrereq.log** sur le lecteur système de l’ordinateur. Le fichier journal peut contenir des informations supplémentaires qui n’apparaissent pas dans l’interface de l’application.  

Quand vous exécutez l’Outil de vérification des prérequis à l’invite de commandes et spécifiez des options de ligne de commande :  

-   L’Outil de vérification des prérequis effectue uniquement les vérifications associées au serveur de site ou aux systèmes de site que vous spécifiez sur la ligne de commande.  
-   Pour vérifier un ordinateur distant, votre compte d’utilisateur doit disposer des droits d’administrateur sur cet ordinateur.  

Pour plus d’informations sur les vérifications effectuées par l’Outil de vérification des prérequis, consultez [Liste des vérifications des prérequis pour System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copier les fichiers de l’Outil de vérification des prérequis sur un autre ordinateur  

1.  Dans l’Explorateur Windows, accédez à l’un des emplacements suivants :  

    -   **&lt;*Support d’installation de Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Répertoire d’installation de Configuration Manager*\>\BIN\X64**  

2.  Copiez les fichiers suivants vers le dossier de destination sur l'autre ordinateur :  

    -   Prereqchk.exe  
    -   Prereqcore.dll  
    -   Basesql.dll  
    -   Basesvr.dll  
    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Exécuter l’Outil de vérification des prérequis avec les vérifications par défaut  

1.  Dans l’Explorateur Windows, accédez à l’un des emplacements suivants :  

    -   **&lt;*Support d’installation de Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Répertoire d’installation de Configuration Manager*\>\BIN\X64**  

2.  Exécutez **prereqchk.exe** pour démarrer l’Outil de vérification des prérequis.   
    L’Outil de vérification des prérequis détecte les sites existants et, une fois identifiés, vérifie s'ils sont prêts pour une mise à niveau. Si aucun site n'est trouvé, toutes les vérifications sont effectuées. La colonne **Type de site** fournit des informations sur le serveur de site ou le système de site auquel la règle est associée.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Exécuter l’Outil de vérification des prérequis à partir d’une invite de commandes pour toutes les vérifications par défaut  

1.  Ouvrez une fenêtre d’invite de commandes, puis accédez à l’un des répertoires suivants :  

    -   **&lt;*Support d’installation de Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Répertoire d’installation de Configuration Manager*\>\BIN\X64**  

2.  Entrez  **prereqchk.exe /LOCAL** pour démarrer l’Outil de vérification des prérequis et effectuer toutes les vérifications des prérequis sur le serveur.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Exécuter l’Outil de vérification des prérequis à partir d’une invite de commandes pour utiliser des options  

1. Ouvrez une fenêtre d’invite de commandes, puis accédez à l’un des répertoires suivants :  

   -   **&lt;*Support d’installation de Configuration Manager*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Répertoire d’installation de Configuration Manager*\>\BIN\X64**  

2. Entrez **prereqchk.exe** en ajoutant une ou plusieurs des options de ligne de commande suivantes.  

   Par exemple, pour vérifier un site principal, vous pouvez spécifier ce qui suit :  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;Nom de domaine complet de SQL Server\> /SDK &lt;Nom de domaine complet du fournisseur SMS\> [/JOIN &lt;Nom de domaine complet du site d’administration centrale\>] [/MP &lt;Nom de domaine complet du point de gestion\>] [/DP &lt;Nom de domaine complet du point de distribution\>]**  

   **Serveur de site d’administration centrale** :  

   -   **/NOUI**  

        Non obligatoire. Démarre l’Outil de vérification des prérequis sans afficher l’interface utilisateur. Vous devez spécifier cette option avant toute autre option dans la ligne de commande.  

   -   **/CAS**  

        Obligatoire. Vérifie que l'ordinateur local répond à la configuration requise pour le site d'administration centrale.  

   -   **/SQL &lt;*FQDN de SQL Server*>**  

        Obligatoire. À l’aide du nom de domaine complet, vérifie que l’ordinateur spécifié présente la configuration requise pour que SQL Server puisse héberger la base de données du site Configuration Manager.  

   -   **/SDK &lt;*FQDN du fournisseur SMS*>**  

        Obligatoire. Vérifie que l'ordinateur spécifié répond à la configuration requise pour le fournisseur SMS.  

   -   **/Ssbport**  

        Non obligatoire. Vérifie qu’une exception de pare-feu est en place pour autoriser la communication sur le port SQL Server Service Broker (SSB). Le port SSB par défaut est 4022.  

   -   **InstallDir &lt;*Chemin d’installation de Configuration Manager*>**  

        Non obligatoire. Vérifie l’espace disque minimal nécessaire pour l’installation du site.  

   **Serveur de site principal** :  

   -   **/NOUI**  

       Non obligatoire. Démarre l’Outil de vérification des prérequis sans afficher l’interface utilisateur. Vous devez spécifier cette option avant toute autre option dans la ligne de commande.  

   -   **/PRI**  

        Obligatoire. Vérifie que l'ordinateur local répond à la configuration requise pour le site principal.  

   -   **/SQL &lt;*FQDN de SQL Server*>**  

        Obligatoire. Vérifie que l’ordinateur spécifié présente la configuration requise pour que SQL Server puisse héberger la base de données du site Configuration Manager.  

   -   **/SDK &lt;*FQDN du fournisseur SMS*>**  

        Obligatoire. Vérifie que l'ordinateur spécifié répond à la configuration requise pour le fournisseur SMS.  

   -   **/JOIN &lt;*FQDN du site d’administration centrale*>**  

        Non obligatoire. Vérifie que l'ordinateur local est conforme à la configuration requise pour se connecter au serveur de site d'administration centrale.  

   -   **/MP &lt;*FQDN du point de gestion*>**  

        Non obligatoire. Vérifie que l'ordinateur spécifié répond à la configuration requise pour le rôle de système de site du point de gestion. Cette option est prise en charge uniquement avec l’option **/PRI** .  

   -   **/DP &lt;*FQDN du point de distribution*>**  

        Non obligatoire. Vérifie que l'ordinateur spécifié répond à la configuration requise pour le rôle de système de site du point de distribution. Cette option est prise en charge uniquement avec l’option **/PRI** .  

   -   **/Ssbport**  

        Non obligatoire. Vérifie qu'une exception de pare-feu est en place pour permettre la communication sur le port SSB. Le port SSB par défaut est 4022.  

   -   **InstallDir &lt;*Chemin d’installation de Configuration Manager*>**  

        Non obligatoire. Vérifie l’espace disque minimal nécessaire pour l’installation du site.  

   **Serveur de site secondaire** :  

   -   **/NOUI**  

        Non obligatoire. Démarre l’Outil de vérification des prérequis sans afficher l’interface utilisateur. Vous devez spécifier cette option avant toute autre option dans la ligne de commande.  

   -   **/SEC &lt;*FQDN du serveur de site secondaire*>**  

        Obligatoire. Vérifie que l'ordinateur spécifié répond aux exigences pour le site secondaire.  

   -   **/INSTALLSQLEXPRESS**  

        Non obligatoire. Vérifie que SQL Server Express peut être installé sur l'ordinateur spécifié.  

   -   **/Ssbport**  

        Non obligatoire. Vérifie qu’une exception de pare-feu est en place pour permettre la communication sur le port SSB. Le port SSB par défaut est 4022.  

   -   **/Sqlport**  

        Non obligatoire. Vérifie qu’une exception de pare-feu est en place pour permettre la communication pour le port de service SQL Server, et que le port n’est pas utilisé par une autre instance nommée de SQL Server. Le port par défaut est 1433.  

   -   **InstallDir &lt;*Chemin d’installation de Configuration Manager*>**  

        Non obligatoire. Vérifie l’espace disque minimal nécessaire pour l’installation du site.  

   -   **/SourceDir**  

        Non obligatoire. Vérifie que le compte d'ordinateur du site secondaire peut accéder au dossier qui héberge les fichiers sources d'installation.  

   **Console Configuration Manager** :  

   -   **/Adminui**  

        Obligatoire. Vérifie que l’ordinateur local présente la configuration requise pour l’installation de Configuration Manager.  

3. L’interface utilisateur de l’Outil de vérification des prérequis affiche la liste des problèmes détectés dans la section **Résultat de la vérification de configuration requise** .  

   -   Cliquez sur un élément de la liste pour obtenir plus d'informations sur la façon de résoudre le problème.  
   -   Vous devez résoudre tous les éléments de la liste qui présentent un état **Erreur** avant d’installer le serveur de site, le système de site ou la console Configuration Manager.  
   -   Vous pouvez également ouvrir le fichier **ConfigMgrPrereq.log** à la racine du lecteur système pour examiner les résultats de l’Outil de vérification des prérequis. Le fichier journal peut contenir des informations supplémentaires qui ne sont pas affichées dans l’interface utilisateur de l’Outil de vérification des prérequis.  
