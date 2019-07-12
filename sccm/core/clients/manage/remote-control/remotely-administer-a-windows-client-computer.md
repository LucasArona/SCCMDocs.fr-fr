---
title: Administrer à distance un ordinateur Windows
titleSuffix: Configuration Manager
description: Administrez un ordinateur client Windows distant à l’aide de System Center Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3c9648c4-645e-4e47-ae10-2da817b8c83b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1a18371a7f75935b3d72262b35385f8f4e81923
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677668"
---
# <a name="how-to-remotely-administer-a-windows-client-computer-by-using-system-center-configuration-manager"></a>Comment administrer à distance un ordinateur client Windows à l’aide de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)* Configuration Manager vous permet de vous connecter aux ordinateurs clients à l’aide du **Contrôle à distance de Configuration Manager**. Avant de commencer à utiliser le contrôle à distance, veillez à consulter les informations des articles suivants :  

-   [Prérequis pour le contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/prerequisites-for-remote-control.md)  

-   [Configuration du contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md)  

Vous pouvez démarrer l’observateur de contrôle à distance de trois manières :  

-   Dans la console Configuration Manager.  

-   À une invite de commandes Windows.  

-   À partir du menu **Démarrer** de Windows sur un ordinateur qui exécute la console Configuration Manager dans le groupe de programmes **Microsoft System Center**.  

## <a name="to-remotely-administer-a-client-computer-from-the-configuration-manager-console"></a>Pour administrer à distance un ordinateur client à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Actifs et Conformité** > **Appareils** ou **Regroupements d’appareils**.  

3.  Sélectionnez l’ordinateur à administrer à distance puis, sous l’onglet **Accueil**, dans le groupe **Appareil**, choisissez **Démarrer** > **Contrôle à distance**.  

    > [!IMPORTANT]  
    >  Si le paramètre client **Inviter l’utilisateur à autoriser le contrôle à distance** a la valeur **True**, la connexion ne démarre pas tant que l’utilisateur de l’ordinateur distant n’accepte pas l’invite de contrôle à distance. Pour plus d’informations, consultez [Configuration du contrôle à distance dans System Center Configuration Manager](../../../../core/clients/manage/remote-control/configuring-remote-control.md).  

4.  Lorsque la fenêtre **Contrôle à distance de Configuration Manager** s'ouvre, vous pouvez administrer à distance l'ordinateur client. Utilisez les options suivantes pour configurer la connexion.  

    > [!NOTE]  
    >  Si l’ordinateur auquel vous vous connectez dispose de plusieurs moniteurs, l’affichage de tous les moniteurs apparaît dans la fenêtre de contrôle à distance.  

    -   **File**
        - **Connecter** : permet de se connecter à un autre ordinateur. Cette option n'est pas disponible lorsqu'une session de contrôle à distance est active.  
        -   **Déconnecter** : permet de déconnecter la session active de contrôle à distance, mais pas de fermer la fenêtre **Contrôle à distance de Configuration Manager**.  
        - **Quitter** : permet de déconnecter la session de contrôle à distance active et de fermer la fenêtre **Contrôle à distance de Configuration Manager**.  

        > [!NOTE]  
        >  Quand vous vous déconnectez d’une session de contrôle à distance, le contenu du Presse-papiers de Windows sur l’ordinateur que vous visualisez est supprimé.


    - **Afficher**
      - **Profondeur de couleur** : choisissez 16 bits ou 32 bits par pixel.
      -  **Plein écran** : permet d’agrandir la fenêtre **Contrôle à distance de Configuration Manager**. Pour quitter le mode plein écran, appuyez sur Ctrl+Alt+Pause.  
      - **Optimiser pour la connexion à faible bande passante** : choisissez cette option si la connexion est à faible bande passante.
      - **Affichage :**
        - **Tous les écrans** : ajouté dans Configuration Manager 1902. Si l’ordinateur auquel vous vous connectez dispose de plusieurs moniteurs, l’affichage de tous les moniteurs apparaît dans la fenêtre de contrôle à distance. **Tous les écrans** est le seul affichage pour les ordinateurs avec plusieurs moniteurs avant 1902.
        -  **Premier écran** : ajouté dans Configuration Manager 1902. Le *premier écran* se trouve en haut à l’extrême gauche, comme illustré dans les paramètres d’affichage Windows. Vous ne pouvez pas sélectionner un écran spécifique. Quand vous faites basculer la configuration de l’observateur, reconnectez la session à distance. L’observateur enregistre votre préférence pour les prochaines connexions.
        -  **Ajuster à la page** : permet de redimensionner l’affichage de l’ordinateur distant pour l’adapter à la taille de la fenêtre **Contrôle à distance de Configuration Manager**.
        - **Barre d’état** : permet d’activer ou de désactiver l’affichage de la barre d’état de la fenêtre **Contrôle à distance de Configuration Manager**.  

       > [!NOTE]  
       >  L’observateur enregistre votre préférence pour les prochaines connexions.

    -   **Action**
        - **Envoyer Ctrl+Alt+Suppr** : permet d’envoyer la séquence de touches Ctrl+Alt+Suppr à l’ordinateur distant. 
        - **Activer le partage du Presse-papiers** : permet de copier et de coller des éléments vers et à partir de l’ordinateur distant. Si vous modifiez cette valeur, vous devez redémarrer la session de contrôle à distance pour appliquer la modification.   
          - Si vous ne voulez pas que le partage du Presse-papiers soit activé dans la console Configuration Manager, sur l’ordinateur exécutant la console, définissez la valeur de la clé de Registre **HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\Remote Control\Clipboard Sharing** sur **0**.
        - **Activer la traduction du clavier** : permet de faire passer la disposition du clavier de l’ordinateur exécutant la console à la disposition de l’appareil connecté.
        - **Verrouiller le clavier distant et la souris** : permet de verrouiller le clavier et la souris distants pour empêcher l’utilisateur d’utiliser l’ordinateur distant.  

    -   **Aide**
        - **À propos du contrôle à distance** : permet d’afficher la version actuelle de la visionneuse.  

5.  Les utilisateurs de l’ordinateur distant peuvent afficher plus d’informations sur la session de contrôle à distance lorsqu’ils cliquent sur l’icône **Contrôle à distance** de Configuration Manager. L’icône est dans la zone de notification de Windows ou dans la barre de session de contrôle à distance.  

## <a name="to-start-the-remote-control-viewer-from-the-windows-command-line"></a>Pour démarrer l'observateur de contrôle à distance à partir de la ligne de commande Windows  

-   À l’invite de commandes Windows, tapez _<Dossier d’installation Configuration Manager>\>_ **\AdminConsole\Bin\x64\CmRcViewer.exe**  

CmRcViewer.exe prend en charge les options de ligne de commande suivantes :  

- *Adresse* : spécifie le nom NetBIOS, le nom de domaine complet (FQDN) ou l’adresse IP de l’ordinateur client auquel vous voulez vous connecter.
- *Nom du serveur de site* : indique le nom du serveur de site System Center Configuration Manager auquel vous voulez envoyer des messages d’état associés à la session de contrôle à distance.
- **/?** : affiche les options de ligne de commande de l’observateur de contrôle à distance.  
     
**Example:CmRcViewer.exe** *<Adresse\>* *<\\\Nom du serveur de site>*  
