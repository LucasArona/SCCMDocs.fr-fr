---
title: Utiliser un média autonome pour déployer Windows sans utiliser le réseau
titleSuffix: Configuration Manager
description: Utilisez un média autonome dans Configuration Manager pour déployer des systèmes d’exploitation lorsque la bande passante est limitée ou comme option pour actualiser, installer ou mettre à niveau des ordinateurs.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 58a0d2ae-de76-401f-b854-7a5243949033
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e50806868955eac807645a5378aea53acdc899
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="use-stand-alone-media-to-deploy-windows-without-using-the-network-in-system-center-configuration-manager"></a>Utiliser un média autonome pour déployer Windows sans utiliser le réseau dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, un média autonome contient tout ce qui est nécessaire pour permettre le déploiement d’un système d’exploitation sur un ordinateur. Cela comprend l’image de démarrage, l’image du système d’exploitation et la séquence de tâches permettant d’installer le système d’exploitation, c’est-à-dire les applications, les pilotes, etc. Les déploiements de médias autonomes vous permettent de déployer des systèmes d'exploitation dans les conditions suivantes :  

-   dans les environnements où il n'est pas pratique de copier une image du système d'exploitation ou d'autres packages volumineux sur le réseau ;  

-   dans les environnements sans connectivité réseau ou avec une connectivité réseau avec une faible bande passante.  

Vous pouvez utiliser un média autonome dans les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md)  

 Exécutez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis préparez et créez le média autonome en vous aidant des indications fournies dans les sections suivantes.  

## <a name="task-sequence-actions-not-supported-when-using-stand-alone-media"></a>Actions de séquence de tâches non prises en charge lors de l’utilisation d’un média autonome  
 Si vous avez effectué les étapes de l’un des scénarios de déploiement de système d’exploitation pris en charge, la séquence de tâches permettant de déployer ou mettre à niveau le système d’exploitation a été créée et tout le contenu associé a été distribué à un point de distribution. Quand vous utilisez un média autonome, voici les actions qui ne sont pas prises en charge dans la séquence de tâches :  

-   Étape Appliquer automatiquement les pilotes dans la séquence de tâches. L’application automatique des pilotes de périphérique présents dans le catalogue de pilotes n’est pas prise en charge, mais vous pouvez choisir l’étape Appliquer le package de pilotes pour mettre à la disposition du programme d’installation de Windows un ensemble de pilotes spécifique.  

-   Installation de mises à jour logicielles.  

-   Installation du logiciel avant le déploiement du système d’exploitation.  

-   Association d'utilisateurs à l'ordinateur de destination pour prendre en charge l'affinité entre appareil et utilisateur.  

-   Le package dynamique s'installe via la tâche Installer les packages.  

-   L'application dynamique s'installe via la tâche Installer l'application.  

> [!NOTE]  
>  Si votre séquence de tâches servant à déployer un système d’exploitation comprend l’étape [Installer le package](../understand/task-sequence-steps.md#BKMK_InstallPackage) et que vous créez le média autonome sur un site d’administration centrale, une erreur peut se produire. Le site d'administration centrale ne dispose pas des stratégies de configuration de client requises pour activer l'agent de distribution logicielle au cours de l'exécution de la séquence de tâches. L’erreur suivante peut apparaître dans le fichier CreateTsMedia.log :  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`
>   
>  Dans le cas d’un média autonome qui comprend une étape **Installer le package**, vous devez créer le média autonome sur un site principal sur lequel l’agent de distribution logicielle est activé ou ajoutez une étape [Exécuter la ligne de commande](../understand/task-sequence-steps.md#BKMK_RunCommandLine) après l’étape [Configurer Windows et ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) et avant la première étape **Installer le package** de la séquence de tâches. L'étape **Exécuter la ligne de commande** exécute une commande de ligne de commande WMIC pour activer l'agent de distribution logicielle avant l'exécution de la première étape Installer le package. Vous pouvez utiliser la ligne de commande suivante dans l'étape **Exécuter la ligne de commande** de votre séquence de tâches :  
>   
>  **Ligne de commande** : **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  

## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement  
 Quand vous utilisez un média autonome pour lancer le processus de déploiement de système d’exploitation, vous devez configurer le déploiement pour rendre le système d’exploitation accessible au média. Vous pouvez configurer cela dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel ou sous l’onglet **Paramètres de déploiement** dans les propriétés du déploiement.  Pour le paramètre **Rendre disponible aux éléments suivants** , sélectionnez l’une des options suivantes :  

-   **Clients, média et environnement PXE Configuration Manager**  

-   **Média et environnement PXE uniquement**  

-   **Média et environnement PXE uniquement (masqué)**  

## <a name="create-the-stand-alone-media"></a>Créer le média autonome  
 Vous pouvez préciser si le média autonome est un disque mémoire flash USB ou un ensemble de CD/DVD. L’ordinateur qui démarre le média doit prendre en charge l’option que vous choisissez comme lecteur de démarrage. Pour plus d’informations, voir [Créer un média autonome](create-stand-alone-media.md).  

## <a name="install-the-operating-system-from-stand-alone-media"></a>Installer le système d’exploitation à partir d’un média autonome  
 Insérez le média autonome dans un lecteur de démarrage sur l’ordinateur, puis mettez-le sous tension pour installer le système d’exploitation.  
