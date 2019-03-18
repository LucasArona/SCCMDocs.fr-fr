---
title: Windows Autopilot pour les appareils existants
titleSuffix: Configuration Manager
description: Utilisez une séquence de tâches Configuration Manager afin de réimager et d’approvisionner un appareil Windows 7 pour Windows Autopilot en mode piloté par l’utilisateur.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 2e96f847-5b5a-4da9-8e8f-6aa488838508
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6878e36e5bf20774f6eef1ee855dda2f95dabfb4
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558000"
---
# <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot pour les appareils existants
<!--3607717, fka 1358333-->

*S’applique à : System Center Configuration Manager (Current Branch)*

[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) offre aux organisations le moyen d’expédier directement de nouveaux appareils Windows 10 intacts à l’utilisateur final et de définir le flux d’approvisionnement que suit l’utilisateur pour obtenir un appareil Windows 10 sécurisé et productif. L’appareil étant inscrit auprès du service Windows Autopilot, vous pouvez lui attribuer le profil Windows Autopilot nécessaire. Ce profil définit l’out-of-box experience (OOBE) de l’appareil. 

[Windows Autopilot pour les appareils existants](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) est disponible avec Windows 10 version 1809 ou ultérieure. Cette fonctionnalité permet de réimager et d’approvisionner un appareil Windows 7 pour [Windows Autopilot en mode piloté par l’utilisateur](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) en une seule séquence de tâches Configuration Manager native. 



## <a name="prerequisites"></a>Prérequis

- Faites l’acquisition du support d’installation de Windows 10 version 1809 ou ultérieure. Puis, créez une image du système d’exploitation Configuration Manager. Pour plus d’informations, consultez [Gérer les images de système d’exploitation](/sccm/osd/get-started/manage-operating-system-images).

- Dans Microsoft Intune, créez des profils pour Windows Autopilot. Pour plus d’informations, voir [Inscrire des appareils Windows dans Intune avec Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

- Un appareil qui n’est pas déjà inscrit auprès du service Windows Autopilot. Si l’appareil est déjà inscrit, le profil attribué est prioritaire. Autopilot pour le profil de périphériques existant s’applique uniquement si que le profil en ligne arrive à expiration.



## <a name="create-the-configuration-file"></a>Créer le fichier de configuration

1. Sur un appareil Windows équipé d’une connectivité à Internet, ouvrez une fenêtre Commande PowerShell d’administration et exécutez les commandes suivantes :  

    1. Installez les modules requis, puis acceptez les invites pour continuer.  
        ``` PowerShell  
        Install-Module AzureAD
        Install-Module WindowsAutopilotIntune 
        Import-Module WindowsAutopilotIntune 
        ```

    2. Connectez-vous à Intune avec des informations d’identification d’administrateur.  
        ``` PowerShell  
        Connect-AutopilotIntune 
        ```

    3. Récupérez tous les profils Windows Autopilot associés à votre client Intune.  
        ``` PowerShell  
        $AutopilotProfile = Get-AutopilotProfile
        ```

    4. Créez un fichier de configuration pour chaque profil. Les fichiers sont nommés en fonction du nom complet du profil et enregistrés sur le bureau de l’utilisateur actuel.<!--PowerShell example courtesy of GitHub user treestryder from SCCMDocs issue #1196-->  
        ``` PowerShell  
        $AutopilotProfile | ForEach-Object { $_ | ConvertTo-AutoPilotConfigurationJSON | Set-Content -Encoding Ascii "~\Desktop\$($_.displayName).json" }
        ```  

        > [!Note]  
        > Le fichier de configuration ne peut contenir qu’un seul profil. Chaque profil doit être entre accolades `{}`.  

2. Enregistrez l’un des profils dans un fichier au format ANSI nommé **AutopilotConfigurationFile.json**. Enregistrez-le dans un emplacement approprié en tant que source du package Configuration Manager.  

    > [!Tip]  
    > La cmdlet PowerShell **Out-File**, qui permet de rediriger la sortie JSON vers un fichier, utilise par défaut l’encodage Unicode. Elle est par ailleurs susceptible de tronquer les longues lignes. Utilisez la cmdlet **Set-Content** avec le paramètre `-Encoding ASCII` pour définir le bon encodage du texte.   
    > 
    > Le bloc-notes Windows utilise le codage ANSI par défaut.  

3. Créez un package Configuration Manager contenant ce fichier. Aucun programme n’est nécessaire. Pour plus d’informations, consultez [Créer un package](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program).  

    > [!NOTE]  
    > Windows impose que ce fichier soit nommé **AutopilotConfigurationFile.json**. Pour utiliser plusieurs profils Autopilot, créez des packages Configuration Manager distincts.  



## <a name="create-the-task-sequence"></a>Créer la séquence de tâches

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**. Sélectionnez **Créer une séquence de tâches** dans le ruban.  

2. Sur la page **Créer une séquence de tâches**, sélectionnez l’option **Déployer Windows Autopilot pour les appareils existants**.  

3. Sur la page **Informations sur la séquence de tâches**, spécifiez un nom, ajoutez éventuellement une description et sélectionnez une image de démarrage. Pour plus d’informations sur les versions d’image de démarrage prises en charge, consultez [Prise en charge de Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

4. Sur la page **Installer Windows**, sélectionnez le **Package d’images** Windows 10. Ensuite, configurez les paramètres suivants :  

    - **Index d’image** : sélectionnez Entreprise, Éducation ou Professionnel suivant les exigences de votre organisation.  

    - Activez l’option **Partitionner et formater l’ordinateur cible avant d’installer le système d’exploitation**.  

    - **Configurer une séquence de tâches pour une utilisation avec Bitlocker**: Si vous activez cette option, la séquence de tâches inclut les étapes nécessaires pour activer Bitlocker  

    - **Clé de produit** : si vous devez spécifier une clé de produit pour l’activation de Windows, entrez-la ici.  

    - Sélectionnez l’une des options suivantes pour configurer le compte administrateur local dans Windows 10 :  
        - **Générer de façon aléatoire le mot de passe d’administrateur local et désactiver le compte sur toutes les plateformes prises en charge (recommandé)**
        - **Activer le compte et spécifier le mot de passe de l’administrateur local**

5. Sur la page **Configurer le réseau**, sélectionnez l’option **Joindre un groupe de travail**. Cette séquence de tâches utilise l’Outil de préparation du système Windows (Sysprep). Si l’appareil est joint à un domaine, Sysprep échoue.  

6. Sur la page **Installer Configuration Manager**, ajoutez les propriétés d’installation nécessaires pour votre environnement.  

    > [!Tip]  
    > La séquence de tâches n’a besoin de ces informations que si les composants du client Configuration Manager sont nécessaires pendant la séquence de tâches avant l’exécution de Sysprep, par exemple pour installer des mises à jour de logiciels ou des applications. Si vous n’effectuez pas ces actions, le client n’est pas nécessaire. Il est désinstallé avant que la séquence de tâches n’exécute Sysprep.  

7. La page **Inclure les mises à jour** sélectionne l’option par défaut **Ne pas installer les mises à jour logicielles**.  

    > [!Tip]  
    > Utilisez la maintenance des images hors connexion pour que l’image reste à jour avec les dernières mises à jour de qualité de Windows 10. Pour plus d’informations, consultez [Appliquer les mises à jour logicielles sur une image du système d’exploitation](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  

8. Sur la page **Installer les applications**, vous pouvez sélectionner les applications à installer pendant la séquence de tâches. Cependant, Microsoft vous recommande de mettre en miroir l’approche d’image de signature avec ce scénario. Une fois l’appareil provisionné avec Autopilot, appliquez toutes les applications et configurations pour la cogestion de Microsoft Intune ou Configuration Manager. Ce processus fournit une expérience cohérente entre les utilisateurs recevant de nouveaux appareils et ceux utilisant Windows Autopilot pour les appareils existants.  

8. Sur la page **Préparation du système**, sélectionnez le package comportant le fichier de configuration Autopilot. Par défaut, la séquence de tâches redémarre l’ordinateur après avoir exécuté Windows Sysprep. Vous pouvez également sélectionner l’option **Arrêter l’ordinateur après cette séquence de tâches**. Cette option vous permet de préparer un appareil, puis de le livrer à un utilisateur pour une expérience Autopilot cohérente.  

9. Effectuez toutes les étapes de l'Assistant.  

Si vous modifiez la séquence de tâches, elle ressemble à la séquence de tâches par défaut pour appliquer une image de système d’exploitation existante. Cette séquence de tâches comprend les étapes supplémentaires suivantes :  

- **Appliquer la configuration Windows Autopilot** : cette étape applique le fichier de configuration Autopilot à partir du package spécifié. Il ne s’agit pas d’un nouveau type d’étape, mais d’une étape **Exécuter la ligne de commande** pour copier le fichier.  

- **Préparer Windows à la capture** : cette étape, qui exécute Windows Sysprep, propose le paramètre **Arrêter l’ordinateur après l’exécution de cette action**. Pour plus d’informations, consultez [Préparer Windows pour capture](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareWindowsforCapture).  

La séquence de tâches Windows Autopilot pour les appareils existants aboutit à un appareil joint à Azure Active Directory (Azure AD). 

Utilisez le [déplacement du dossier connu](https://docs.microsoft.com/onedrive/redirect-known-folders) OneDrive Entreprise pour que les données de l’utilisateur soient bien sauvegardées avant la mise à niveau Windows 10.



## <a name="next-steps"></a>Étapes suivantes

Utilisez la cogestion pour améliorer les fonctionnalités de gestion de vos appareils Windows 10. L’autre chemin vers la cogestion passe par l’approvisionnement moderne avec Windows Autopilot. Pour plus d’informations, consultez les articles suivants :

- [Qu’est-ce que la cogestion ?](/sccm/comanage/overview)
- [Chemins vers la cogestion](/sccm/comanage/quickstart-paths)
- [Windows Autopilot avec la cogestion](/sccm/comanage/quickstart-autopilot)

