---
title: Gérer les images de système d’exploitation
titleSuffix: Configuration Manager
description: Découvrez les méthodes permettant de gérer les images de système d’exploitation stockées dans les fichiers image Windows (WIM).
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40bfd1c8a541fbb1f108741ef2d4fa00b11088d7
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176114"
---
# <a name="manage-os-images-with-configuration-manager"></a>Gérer les images de système d’exploitation avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, les images de système d’exploitation sont stockées dans des fichiers image Windows (WIM). Ces images sont une collection compressée de fichiers de référence et de dossiers, qui est utilisée pour installer et configurer un nouveau système d’exploitation sur un ordinateur. De nombreux scénarios de déploiement de système d’exploitation nécessitent une image de système d’exploitation. 

Vous pouvez utiliser une [image de système d’exploitation par défaut](#default-image) ou créer une image de système d’exploitation à partir d’un [ordinateur de référence](#bkmk_capture) que vous configurez. Lorsque vous créez l’ordinateur de référence, vous ajoutez des fichiers de système d’exploitation, des pilotes, des fichiers de prise en charge, des mises à jour logicielles, des outils et des applications au système d’exploitation. Ensuite, vous le capturez pour créer le fichier image. 

### <a name="default-image"></a>Image par défaut

Les fichiers d’installation Windows incluent l’image du système d’exploitation par défaut. Cette image est une image de système d’exploitation de base qui contient un ensemble standard de pilotes. Si vous utilisez l’image de système d’exploitation par défaut, utilisez les étapes de séquence de tâches pour installer des applications et effectuer d’autres configurations une fois que le système d’exploitation est installé sur l’appareil. Recherchez l’image de système d’exploitation par défaut dans les fichiers de source Windows : `\Sources\install.wim`.  

#### <a name="default-image-advantages"></a>Avantages de l’image par défaut

- La taille de l’image est inférieure à celle d’une image capturée.  

- L’installation d’applications et de configurations avec des étapes de séquence de tâches est plus dynamique. Par exemple, vous pouvez changer les configurations et les applications qui sont installées avec la séquence de tâches, sans avoir à réinitialiser l’appareil.  

#### <a name="default-image-disadvantages"></a>Inconvénients de l’image par défaut

- L’installation du système d’exploitation peut prendre plus de temps. L’installation de l’application et des autres configurations est effectuée après l’installation du système d’exploitation.  


### <a name="bkmk_capture"></a> Image capturée à partir d’un ordinateur de référence

Pour créer une image de système d’exploitation personnalisée, créez un ordinateur de référence avec le système d’exploitation souhaité. Ensuite, installez des applications et configurez les paramètres. Capturez l’image du système d’exploitation à partir de l’ordinateur de référence pour créer le fichier WIM. Créez manuellement l’ordinateur de référence ou utilisez une séquence de tâches pour automatiser certaines étapes de création ou l’ensemble du processus. Pour plus d’informations, consultez [Personnaliser les images de système d’exploitation](/sccm/osd/get-started/customize-operating-system-images).  

#### <a name="captured-image-advantages"></a>Avantages de l’image capturée

- L’installation peut être plus rapide que l’utilisation de l’image par défaut. Par exemple, l’image de système d’exploitation capturée vous permet de préinstaller des applications. Dans ce cas, vous n’aurez pas besoin d’installer de nouveau ces mêmes applications à l’aide des étapes de séquence de tâches.  

#### <a name="captured-image-disadvantages"></a>Inconvénients de l’image capturée

- La taille de l’image est potentiellement supérieure à celle de l’image par défaut.  

- Vous devez créer une nouvelle image quand des mises à jour d’applications et d’outils sont nécessaires.  



##  <a name="BKMK_AddOSImages"></a> Ajouter une image de système d’exploitation  

Avant de pouvoir utiliser une image de système d’exploitation, vous devez l’ajouter à votre site Configuration Manager. 

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Images du système d’exploitation**.  

2.  Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, sélectionnez **Ajouter une image du système d’exploitation**. Cette action démarre l’Assistant Ajout d’une image de système d’exploitation.  

3.  Dans la page **Source de données**, spécifiez le **chemin** réseau du fichier image du système d’exploitation. Par exemple, `\\server\share\path\image.wim`.  

4.  Dans la page **Général**, spécifiez les informations suivantes. Ces informations sont utiles à des fins d’identification lorsque vous avez plusieurs images de système d’exploitation.  

    -   **Nom** : nom unique de l’image. Par défaut, le nom est tiré de celui du fichier WIM.  

    -   **Version** : identificateur de version facultatif. Il n’est pas nécessaire que cette propriété corresponde à la version du système d’exploitation de l’image. Il s’agit souvent de la version du package de votre organisation.   

    -   **Commentaire** : brève description facultative.  

5.  Effectuez toutes les étapes de l'Assistant.  

Pour connaître l’applet de commande PowerShell équivalente à cet Assistant de console, consultez [New-CMOperatingSystemImage](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimage?view=sccm-ps).


Ensuite, distribuez l’image de système d’exploitation sur les points de distribution.  



##  <a name="BKMK_DistributeBootImages"></a> Distribuer du contenu vers les points de distribution  

Distribuez les images de système d’exploitation vers les points de distribution comme vous le feriez pour tout autre contenu. Avant de déployer la séquence de tâches, distribuez l’image de système d’exploitation vers au moins un point de distribution. Pour plus d’informations, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



##  <a name="BKMK_OSImageMulticast"></a> Préparer l’image de système d’exploitation pour les déploiements en multidiffusion  

Utilisez des déploiements en multidiffusion pour permettre à plusieurs ordinateurs de télécharger simultanément une image de système d’exploitation. L’image est multidiffusée aux clients par le point de distribution. De cette façon, vous évitez la situation dans laquelle chaque client télécharge une copie de l’image à partir du point de distribution via sa propre connexion. Si vous choisissez la méthode de déploiement de système d’exploitation [Utiliser la multidiffusion pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network), configurez l’image du système d’exploitation de manière à prendre en charge la multidiffusion. Ensuite, distribuez l’image vers un point de distribution configuré pour la multidiffusion. 

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Images du système d’exploitation**.  

2.  Sélectionnez l’image du système d’exploitation que vous souhaitez distribuer vers le point de distribution configuré pour la multidiffusion.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4.  Passez à l’onglet **Paramètres de distribution**, puis configurez les options suivantes :  

    -   **Autoriser ce package à être transféré par multidiffusion (WinPE uniquement)**  : sélectionnez cette option pour permettre à Configuration Manager de déployer simultanément plusieurs images de système d’exploitation à l’aide de la multidiffusion.  

    -   **Chiffrer les packages de multidiffusion** : spécifiez si le site doit chiffrer l’image avant de l’envoyer au point de distribution. Si l’image contient des informations sensibles, utilisez cette option. Si l’image n’est pas chiffrée, son contenu s’affiche sous forme de texte en clair sur le réseau. Dans ce cas, un utilisateur non autorisé peut intercepter et voir le contenu de l’image.  

    -   **Transférer ce package uniquement par multidiffusion** : spécifiez si vous souhaitez que le point de distribution déploie l’image uniquement pendant une session de multidiffusion.  

         Si vous sélectionnez **Transférer ce package uniquement par multidiffusion**, vous devez également spécifier **Télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches** comme option de déploiement pour l’image du système d’exploitation. Pour plus d'informations, voir [Déployer une séquence de tâches](/sccm/osd/deploy-use/deploy-a-task-sequence).   

5.  Sélectionnez **OK** pour enregistrer les paramètres et fermer les propriétés de l’image.  
