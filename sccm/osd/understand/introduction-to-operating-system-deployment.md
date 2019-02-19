---
title: Introduction au déploiement de systèmes d’exploitation
titleSuffix: Configuration Manager
description: Comprenez les concepts avant de déployer des systèmes d’exploitation dans votre environnement Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d9a1c545-8301-492c-832f-2c108ff93c77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69df6eaa9d7ca164b5d855840eeca2f2c6f72ffc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123118"
---
# <a name="introduction-to-operating-system-deployment-in-system-center-configuration-manager"></a>Introduction au déploiement de système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser Configuration Manager pour déployer des systèmes d’exploitation de différentes façons. Utilisez les informations contenues dans cette section pour comprendre comment déployer des systèmes d’exploitation et automatiser des tâches. 

##  <a name="BKMK_OSDeploymentProcess"></a> Le processus de déploiement de système d’exploitation  
 Configuration Manager propose plusieurs méthodes que vous pouvez utiliser pour déployer un système d’exploitation. Vous devez effectuer plusieurs actions quelle que soit la méthode de déploiement utilisée.  

-   Identifier les pilotes d’appareils Windows qui sont nécessaires pour démarrer l’image de démarrage ou pour installer l’image du système d’exploitation que vous devez déployer.  

-   Identifier l'image de démarrage que vous souhaitez utiliser pour démarrer l'ordinateur de destination.  

-   Utiliser une séquence de tâches pour capturer une image du système d’exploitation que vous souhaitez déployer. Vous pouvez également utiliser une image de système d’exploitation par défaut.  

-   Distribuer l'image de démarrage, l'image du système d'exploitation et tout contenu associé sur un point de distribution.  

-   Créer une séquence de tâches avec les étapes nécessaires pour déployer l’image de démarrage et l’image du système d’exploitation.  

-   Déployer la séquence de tâches dans un regroupement d’ordinateurs.  

-   Surveiller le déploiement.  

##  <a name="BKMK_OSDScenarios"></a> Scénarios de déploiement du système d’exploitation  
 Vous avez le choix entre de nombreux scénarios de déploiement de systèmes d’exploitation dans Configuration Manager en fonction de votre environnement et de l’objectif de l’installation du système d’exploitation.  Par exemple, vous pouvez partitionner et formater un ordinateur existant avec une nouvelle version de Windows ou mettre à niveau Windows vers la version la plus récente. Pour vous aider à déterminer la méthode de déploiement qui répond à vos besoins, consultez [Scénarios de déploiement de systèmes d’exploitation d’entreprise](../deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).  Vous pouvez choisir parmi les scénarios de déploiement de système d’exploitation suivants :  

-   [Effectuer une mise à niveau de Windows vers la dernière version](../deploy-use/upgrade-windows-to-the-latest-version.md)  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](../deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](../deploy-use/install-new-windows-version-new-computer-bare-metal.md)  

-   [Remplacement d’un ordinateur existant et transfert des paramètres](../deploy-use/replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_OSDMethods"></a> Méthodes pour déployer des systèmes d’exploitation  
 Il existe plusieurs méthodes que vous pouvez utiliser pour déployer des systèmes d’exploitation sur des ordinateurs clients Configuration Manager.  

- **Déploiements initiés par PXE** : Les déploiements initiés par PXE permettent aux ordinateurs clients de demander un déploiement sur le réseau. Avec cette méthode de déploiement, l'image du système d'exploitation et une image de démarrage Windows PE sont envoyées à un point de distribution qui est configuré pour accepter les requêtes de démarrage PXE. Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau avec System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

- **Rendre les systèmes d’exploitation disponibles dans le centre logiciel** : Vous pouvez déployer un système d’exploitation et le mettre à disposition dans le centre logiciel. Les clients Configuration Manager peuvent lancer l’installation du système d’exploitation à partir du Centre logiciel. Pour plus d’informations, consultez [Remplacer un ordinateur existant et transférer des paramètres](../deploy-use/replace-an-existing-computer-and-transfer-settings.md).  

- **Déploiements multidiffusion** : les déploiements multidiffusion économisent la bande passante réseau en envoyant de manière simultanée des données à plusieurs clients plutôt que d'envoyer une copie des données à chaque client via une connexion distincte. Avec cette méthode de déploiement, l'image du système d'exploitation est envoyée à un point de distribution. Celui-ci déploie à son tour l'image lorsque les ordinateurs clients demandent le déploiement. Pour plus d’informations, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

- **Déploiements de médias de démarrage** : les déploiements de médias de démarrage vous permettent de déployer le système d'exploitation au démarrage de l'ordinateur de destination. Au démarrage de l'ordinateur de destination, il récupère la séquence de tâches, l'image du système d'exploitation et tout autre contenu requis à partir du réseau. Étant donné que le contenu n'est pas inclus sur le média, vous pouvez mettre à jour le contenu sans avoir à recréer le média. Pour plus d’informations, consultez [Créer un média de démarrage](../deploy-use/create-bootable-media.md).  

- **Déploiements de médias autonomes** : Les déploiements de médias autonomes vous permettent de déployer des systèmes d'exploitation dans les conditions suivantes :  

  - dans les environnements où il n'est pas pratique de copier une image du système d'exploitation ou d'autres packages volumineux sur le réseau ;  

  - dans les environnements sans connectivité réseau ou avec une connectivité réseau avec une faible bande passante.  

    Pour plus d’informations, voir [Créer un média autonome](../deploy-use/create-stand-alone-media.md).  

- **Déploiements de médias préparés** : les déploiements de médias préparés vous permettent de déployer un système d'exploitation sur un ordinateur qui n'est pas entièrement préparé. Le média préparé est un fichier WIM (Windows Imaging Format) qui peut être installé sur un système nu par le fabricant ou dans un centre de reclassement d’entreprise qui n’est pas connecté à l’environnement Configuration Manager.  

   Ensuite, dans l’environnement Configuration Manager, l’ordinateur commence par utiliser l’image de démarrage fournie par le média, puis il se connecte au point de gestion de site pour les séquences de tâches disponibles qui terminent le processus de téléchargement. Cette méthode de déploiement peut réduire le trafic réseau car l'image de démarrage et l'image du système d'exploitation sont déjà sur l'ordinateur de destination. Vous pouvez spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. Pour plus d’informations, consultez [Créer un média préparé](../deploy-use/create-prestaged-media.md).  

##  <a name="BKMK_BootImages"></a> Images de démarrage  
 Une image de démarrage dans Configuration Manager est une image Windows PE (WinPE) utilisée pendant un déploiement de système d’exploitation. Les images de démarrage servent à démarrer un ordinateur dans WinPE, qui est un système d’exploitation minimal avec des composants et des services limités qui préparent l’ordinateur de destination pour l’installation de Windows. Configuration Manager propose deux images de démarrage : Une pour prendre en charge les plates-formes x86 et l'autre pour prendre en charge les plates-formes x64. Celles-ci sont considérées comme des images de démarrage par défaut. Les images de démarrage que vous créez et ajoutez à Configuration Manager sont considérées comme des images personnalisées. Les images de démarrage par défaut peuvent être remplacées automatiquement quand vous mettez à jour Configuration Manager. Pour plus d’informations sur les images de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

##  <a name="BKMK_OSImages"></a> Images du système d’exploitation  
 Les images de système d’exploitation dans Configuration Manager sont stockées au format de fichier WIM (Windows Imaging Format) et représentent un regroupement compressé de fichiers et de dossiers de référence nécessaires pour installer et configurer avec succès un système d’exploitation sur un ordinateur. Pour tous les scénarios de déploiement de système d’exploitation, vous devez sélectionner une image de système d’exploitation. Vous pouvez utiliser l’image de système d’exploitation par défaut ou créer l’image de système d’exploitation à partir d’un ordinateur de référence que vous configurez. Pour plus d’informations, voir [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

##  <a name="BKMK_OSUpgradePackages"></a> Packages de mise à niveau du système d’exploitation  
 Les packages de mise à niveau de système d’exploitation servent à mettre à niveau un système d’exploitation. Il s’agit de déploiements de système d’exploitation initiés par le programme d’installation. Vous importez des packages de mise à niveau de système d’exploitation dans Configuration Manager à partir d’un DVD ou d’un fichier ISO monté. Pour plus d’informations, consultez [Gérer les packages de mise à niveau de système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md).  

##  <a name="BKMK_OSDMedia"></a> Médias pour déployer des systèmes d’exploitation  
 Vous pouvez créer plusieurs types de médias qui peuvent être utilisés pour déployer des systèmes d'exploitation. Les différents types de médias incluent le média qui est utilisé pour capturer des images de système d'exploitation et le média de démarrage, préparé et autonome qui est utilisé pour déployer un système d'exploitation. Les médias vous permettent de déployer des systèmes d’exploitation sur des ordinateurs qui ne disposent pas de connexion réseau ou qui possèdent une connexion avec une faible bande passante vers votre site Configuration Manager. Pour plus d’informations sur la façon d’utiliser des médias, consultez [Créer un média de séquence de tâches](../deploy-use/create-task-sequence-media.md).  

##  <a name="BKMK_DeviceDrivers"></a> Pilotes d'appareils  
 Vous pouvez installer des pilotes de périphérique sur les ordinateurs de destination sans les inclure dans l'image du système d'exploitation déployée. Configuration Manager propose un catalogue de pilotes qui contient les références à tous les pilotes de périphérique que vous importez dans Configuration Manager. Le catalogue de pilotes se trouve dans l’espace de travail **Bibliothèque de logiciels** et est composé de deux nœuds : **pilotes** et **packages de pilotes**. Le nœud **Pilotes** répertorie tous les pilotes que vous avez importés dans le catalogue de pilotes. Vous pouvez utiliser ce nœud pour découvrir les détails sur chaque pilote importé, pour modifier le package de pilotes ou l'image de démarrage auquel/à laquelle appartient un pilote, pour activer ou désactiver un pilote, et bien plus encore. Pour plus d’informations, consultez [Gérer les pilotes](../get-started/manage-drivers.md).  

##  <a name="BKMK_OSDUserState"></a> Enregistrer et restaurer l’état utilisateur  
 Lorsque vous déployez des systèmes d'exploitation, vous pouvez enregistrer l'état utilisateur à partir de l'ordinateur de destination, déployer le système d'exploitation, puis restaurer l'état utilisateur une fois que le système d'exploitation est déployé. Ce processus est généralement utilisé quand vous installez le système d’exploitation sur un ordinateur client Configuration Manager.  

 Les informations relatives à l'état utilisateur sont capturées et restaurées à l'aide de séquences de tâches. Lorsque les informations d'état utilisateur sont capturées, elles peuvent être stockées selon l'une des manières suivantes :  

- Vous pouvez stocker les données d'état utilisateur à distance en configurant un point de migration d'état. La séquence de tâches Capturer envoie les données au point de migration d'état. Ensuite, une fois le système d'exploitation déployé, la séquence de tâches Restaurer récupère les données et restaure l'état utilisateur sur l'ordinateur de destination.  

- Vous pouvez stocker les données d'état utilisateur localement à un emplacement spécifique. Dans ce scénario, la séquence de tâches Capturer copie les données utilisateur vers un emplacement spécifique sur l'ordinateur de destination. Puis, une fois le système d'exploitation déployé, la séquence de tâches Restaurer récupère les données utilisateur à partir de cet emplacement.  

- Vous pouvez spécifier les liens physiques qui peuvent être utilisés pour restaurer les données utilisateur vers leur emplacement d'origine. Dans ce scénario, les données d'état utilisateur restent sur le lecteur lorsque l'ancien système d'exploitation est supprimé. Ensuite, une fois le système d'exploitation déployé, la séquence de tâches Restaurer utilise les liens physiques pour restaurer les données d'état utilisateur vers leur emplacement d'origine.  

  Pour plus d’informations, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

##  <a name="BKMK_UnknownComputer"></a> Déployer sur des ordinateurs inconnus  
 Vous pouvez déployer un système d’exploitation sur des ordinateurs qui ne sont pas gérés par Configuration Manager. Il n'existe aucun enregistrement de ces ordinateurs dans la base de données Configuration Manager. Ces ordinateurs sont appelés ordinateurs inconnus. Les ordinateurs inconnus sont les suivants :  

- Un ordinateur sur lequel le client Configuration Manager n’est pas installé  

- Un ordinateur qui n’est pas importé dans Configuration Manager  

- Un ordinateur qui n’est pas détecté par Configuration Manager  

  Pour plus d’informations, voir [Préparer les déploiements d’ordinateurs inconnus](../get-started/prepare-for-unknown-computer-deployments.md).  

##  <a name="BKMK_UDA"></a> Associer des utilisateurs à un ordinateur  
 Lorsque vous déployez un système d'exploitation, vous pouvez associer des utilisateurs à l'ordinateur de destination pour prendre en charge des actions d'affinité entre appareil et utilisateur. Lorsque vous associez un utilisateur à l'ordinateur de destination, l'utilisateur administratif peut effectuer des actions ultérieurement sur l'un des ordinateurs associés à cet utilisateur, notamment déployer une application sur l'ordinateur d'un utilisateur spécifique. Toutefois, lorsque vous déployez un système d'exploitation, vous ne pouvez pas déployer le système d'exploitation sur l'ordinateur d'un utilisateur spécifique. Pour plus d’informations, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).  

##  <a name="BKMK_TaskSequences"></a> Utiliser des séquences de tâches pour automatiser des étapes  
 Vous pouvez créer des séquences de tâches pour effectuer diverses tâches au sein de votre environnement Configuration Manager. Les actions de la séquence de tâches sont définies dans les étapes individuelles de la séquence. Lors de l'exécution de la séquence de tâches, les actions de chaque étape sont effectuées au niveau de la ligne de commande sans intervention de l'utilisateur. Vous pouvez utiliser des séquences de tâches pour les opérations suivantes :  

-   [Créer une séquence de tâches pour installer un système d’exploitation](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)  

-   [Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation](../deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)  

-   [Créer une séquence de tâches pour capturer un système d’exploitation](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)  

-   [Créer une séquence de tâches pour capturer et restaurer l’état utilisateur](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)  

-   [Créer une séquence de tâches personnalisée](../deploy-use/create-a-custom-task-sequence.md)  
