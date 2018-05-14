---
title: Administrer à distance un ordinateur Windows
titleSuffix: Configuration Manager
description: Administrez un ordinateur client Windows distant à l’aide de System Center Configuration Manager.
ms.date: 07/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4437ef8f88b18b7148eadbc3d125d8ac72fb240a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Comment administrer à distance un ordinateur client Windows à l’aide de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de commencer à utiliser le contrôle à distance, veillez à consulter les informations des rubriques suivantes :  

-   [Prérequis pour le contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configuration du contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

Vous pouvez démarrer l’observateur de contrôle à distance de trois manières :  

-   Dans la console Configuration Manager.  

-   À une invite de commandes Windows.  

-   Dans le menu **Démarrer** de Windows sur un ordinateur qui exécute la console Configuration Manager à partir du groupe de programmes **Microsoft System Center**.  

### <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Pour administrer à distance un ordinateur client à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Actifs et Conformité** > **Appareils** ou **Regroupements d’appareils**.  

3.  Sélectionnez l’ordinateur à administrer à distance puis, sous l’onglet **Accueil**, dans le groupe **Appareil**, choisissez **Démarrer** > **Contrôle à distance**.  

    > [!IMPORTANT]  
    >  Si le paramètre client **Inviter l’utilisateur à autoriser le contrôle à distance** a la valeur **True**, la connexion ne démarre pas tant que l’utilisateur de l’ordinateur distant n’accepte pas l’invite de contrôle à distance. Pour plus d’informations, consultez [Configuration du contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Lorsque la fenêtre **Contrôle à distance de Configuration Manager** s'ouvre, vous pouvez administrer à distance l'ordinateur client. Utilisez les options suivantes pour configurer la connexion.  

    > [!NOTE]  
    >  Si l’ordinateur auquel vous vous connectez dispose de plusieurs moniteurs, l’affichage de tous les moniteurs apparaît dans la fenêtre de contrôle à distance.  

    -   **Fichier - Connecter** : se connecte à un autre ordinateur. Cette option n'est pas disponible lorsqu'une session de contrôle à distance est active.  

    -   **Fichier - Déconnecter** : déconnecte la session active de contrôle à distance, mais ne ferme pas la fenêtre **Contrôle à distance de Configuration Manager**.  

    -   **Fichier - Quitter** : déconnecte la session de contrôle à distance active et ferme la fenêtre **Contrôle à distance de Configuration Manager**.  

        > [!NOTE]  
        >  Quand vous vous déconnectez d’une session de contrôle à distance, le contenu du Presse-papiers de Windows sur l’ordinateur que vous visualisez est supprimé.  

    -   **Affichage - Plein écran** : optimise la fenêtre **Contrôle à distance de Configuration Manager**.  

        > [!NOTE]  
        >  Pour quitter le mode plein écran, appuyez sur Ctrl+Alt+Pause.  

    -   **Afficher - Ajuster à la page** : redimensionne l’affichage de l’ordinateur distant pour l’adapter à la taille de la fenêtre **Contrôle à distance de Configuration Manager**.  

    -   **Afficher - Barre d’état** : active ou désactive l’affichage de la barre d’état de la fenêtre **Contrôle à distance de Configuration Manager**.  

    -   **Action - Envoyer Ctrl+Alt+Suppr** : envoie la séquence de touches Ctrl+Alt+Suppr à l’ordinateur distant.  

    -   **Action - Activer le partage du Presse-papiers** : permet de copier et coller des éléments vers et depuis l’ordinateur distant. Si vous modifiez cette valeur, vous devez redémarrer la session de contrôle à distance pour appliquer la modification.  

        > [!NOTE]  
        >  Si vous ne voulez pas que le partage du Presse-papiers soit activé dans la console Configuration Manager, sur l’ordinateur exécutant la console, définissez la valeur de la clé de Registre **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** sur **0**.  

    -   **Action - Verrouiller le clavier distant et la souris** : verrouille le clavier et la souris distants pour empêcher l’utilisateur d’utiliser l’ordinateur distant.  

    -   **Aide - À propos du contrôle à distance** : affiche la version actuelle de l’observateur.  

5.  Les utilisateurs de l’ordinateur distant peuvent afficher plus d’informations sur la session de contrôle à distance lorsqu’ils cliquent sur l’icône **Contrôle à distance** de Configuration Manager dans la zone de notification de Windows ou sur l’icône dans la barre de la session de contrôle à distance.  

### <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Pour démarrer l'observateur de contrôle à distance à partir de la ligne de commande Windows  

-   À l’invite de commandes Windows, tapez *<Dossier d’installation Configuration Manager\>***\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe prend en charge les options de ligne de commande suivantes :  

- *Adresse* : spécifie le nom NetBIOS, le nom de domaine complet (FQDN) ou l’adresse IP de l’ordinateur client auquel vous voulez vous connecter.
- *Nom du serveur de site* : indique le nom du serveur de site System Center Configuration Manager auquel vous voulez envoyer des messages d’état associés à la session de contrôle à distance.
- **/?** : affiche les options de ligne de commande de l’observateur de contrôle à distance.  
     
**Example:CmRcViewer.exe** *<Adresse\>* *<\\\Nom du serveur de site>*  
