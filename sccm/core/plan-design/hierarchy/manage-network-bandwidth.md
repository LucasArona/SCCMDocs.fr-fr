---
title: Gérer la bande passante réseau pour le contenu
titleSuffix: Configuration Manager
description: Configurez la planification, la limitation de bande passante et le contenu préparé pour System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2d8587c0640d831a723b9ff7c3a6402d47ee2405
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-network-bandwidth-for-content"></a>Gérer la bande passante réseau pour le contenu
Pour mieux gérer la bande passante réseau utilisée pour le processus de gestion du contenu de System Center Configuration Manager, vous pouvez utiliser les commandes Configuration Manager intégrées de planification et de limitation de bande passante. Vous pouvez également utiliser le contenu préparé. Les sections suivantes décrivent ces options plus en détail.

##  <a name="BKMK_PlanningForThrottling"></a>Planification et limitation de bande passante  

 Lorsque vous créez un package, modifiez le chemin source du contenu ou mettez à jour le contenu sur le point de distribution, les fichiers sont copiés depuis le chemin source vers la bibliothèque de contenu sur le serveur de site. Ensuite, le contenu est copié depuis la bibliothèque de contenu sur le serveur de site vers la bibliothèque de contenu sur les points de distribution. Si des fichiers sources de contenu sont mis à jour et que ces fichiers ont déjà été distribués, Configuration Manager récupère uniquement les fichiers nouveaux ou mis à jour, puis il les envoie au point de distribution.

 Vous pouvez utiliser les commandes de planification et de limitation de bande passante pour la communication entre sites, ainsi que pour la communication entre un serveur de site et un point de distribution distant. Si vous constatez que la bande passante réseau est limitée même après avoir configuré les commandes de planification et de limitation de bande passante, vous pouvez envisager de préparer le contenu sur le point de distribution.  

 Dans Configuration Manager, vous pouvez configurer un calendrier et spécifier des paramètres de limitation de bande passante sur des points de distribution distants qui déterminent quand et comment s’effectue la distribution du contenu. Chaque point de distribution distant peut avoir différentes configurations qui permettent de répondre aux limitations de la bande passante réseau à partir du serveur de site pour le point de distribution distant. Les commandes de programmation et de limitation de bande passante sur le point de distribution sont similaires aux paramètres d’une adresse d’expéditeur standard. Dans ce cas, les paramètres sont utilisés par un nouveau composant appelé Package Transfer Manager.

 Package Transfer Manager distribue le contenu à partir d'un serveur de site, site principal ou secondaire, vers un point de distribution qui est installé sur un système de site. Les paramètres de limitation de bande passante sont spécifiés sous l’onglet **Limites du taux de transfert**, et les paramètres de planification sont spécifiés sous l’onglet **Calendrier** pour un point de distribution qui ne se trouve pas sur un serveur de site. Les paramètres d'heure sont basés sur le fuseau horaire du site émetteur, et non sur le point de distribution.  

> [!IMPORTANT]  
>  Les onglets **Limites du taux de transfert** et **Calendrier** sont affichés uniquement dans les propriétés des points de distribution qui ne sont pas installés sur un serveur de site.  

Pour plus d’informations, consultez [Installer et configurer des points de distribution pour System Center Configuration Manager](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

##  <a name="BKMK_PrestagingContent"></a>Contenu préparé  
 Vous pouvez préparer du contenu pour ajouter les fichiers de contenu à la bibliothèque de contenu sur un serveur de site ou sur un point de distribution avant de distribuer le contenu. Comme les fichiers de contenu figurent déjà dans la bibliothèque de contenu, ils ne sont pas transférés sur le réseau quand vous distribuez le contenu. Vous pouvez préparer des fichiers de contenu pour les applications et les packages.  

Dans la console Configuration Manager, sélectionnez le contenu à préparer, puis utilisez l’**Assistant Création du fichier de contenu préparé**. Cette opération crée un fichier de contenu compressé et préparé qui contient les fichiers et les métadonnées associées pour le contenu. Vous pouvez ensuite importer manuellement le contenu au niveau d'un serveur de site ou d'un point de distribution. Notez les points suivants :  

-   Lorsque vous importez le fichier de contenu préparé sur un serveur de site, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le serveur de site, puis enregistrés dans la base de données du serveur de site.  

-   Quand vous importez le fichier de contenu préparé sur un point de distribution, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le point de distribution. Un message d’état est envoyé au serveur de site pour indiquer au site que le contenu est disponible sur le point de distribution.  

Vous pouvez éventuellement configurer le point de distribution comme **préparé** pour faciliter la gestion de la distribution de contenu. Ensuite, quand vous distribuez le contenu, choisissez l’option souhaitée :  

-   Toujours préparer le contenu sur le point de distribution.  

-   Préparer le contenu initial pour le package, puis utiliser le processus de distribution de contenu standard quand des mises à jour du contenu sont disponibles.  

-   Toujours utiliser le processus de distribution de contenu standard pour le contenu du package.  

###  <a name="BKMK_DetermineToPrestageContent"></a>Déterminer si vous devez préparer du contenu  
 Envisagez de préparer du contenu pour les applications et les packages dans les cas suivants :  

-   **Pour résoudre le problème de bande passante réseau limitée entre le serveur de site et un point de distribution.** Si la planification et la limitation de bande passante ne suffisent pas à répondre à vos besoins en matière de bande passante, songez à préparer le contenu sur le point de distribution. Chaque point de distribution est associé au paramètre **Activer ce point de distribution pour le contenu préparé** que vous pouvez choisir dans les propriétés du point de distribution. Lorsque vous activez cette option, le point de distribution est identifié comme un point de distribution préparé et vous pouvez choisir comment gérer le contenu pour chaque package.  

    Les paramètres suivants sont disponibles dans les propriétés relatives à une application, un package, un package de pilotes, une image de démarrage, un programme d’installation de système d’exploitation et une image. Ils vous permettent de choisir le mode de gestion de la distribution du contenu sur les points de distribution distants qui sont identifiés comme préparés :  

    -   **Télécharger automatiquement le contenu lorsque des packages sont affectés à des points de distribution** : utilisez cette option quand vous disposez de packages plus petits, et que les paramètres de planification et de limitation de bande passante offrent suffisamment de contrôle pour la distribution de contenu.  

    -   **Télécharger uniquement les modifications de contenu vers le point de distribution** : utilisez cette option si vous prévoyez que la taille des futures mises à jour du contenu du package sera normalement inférieure à celle du package initial. Par exemple, vous pouvez préparer une application telle que Microsoft Office, car la taille du package initial est supérieure à 700 Mo et trop volumineuse pour être envoyée sur le réseau. Toutefois, les mises à jour du contenu pour ce package peuvent être inférieures à 10 Mo et distribuables sur le réseau. Citons aussi l’exemple d’un package de pilotes : sa taille initiale peut être importante, mais les ajouts de pilotes incrémentiels au package peuvent être de petite taille.  

    -   **Copier manuellement le contenu de ce package vers le point de distribution** : utilisez cette option quand vous disposez de packages volumineux, avec du contenu tel qu’un système d’exploitation et n’utilisez jamais le réseau pour distribuer le contenu sur le point de distribution. Lorsque vous sélectionnez cette option, vous devez préparer le contenu sur le point de distribution.  

    > [!IMPORTANT]  
    >  Les options précédentes sont applicables pour chaque package et ne sont utilisées que si un point de distribution est identifié comme préparé. Les points de distribution qui n'ont pas été identifiés comme préparés ignorent ces paramètres. Dans ce cas, le contenu est toujours distribué via le réseau à partir du serveur de site vers les points de distribution.  

-   **Pour restaurer la bibliothèque de contenu sur un serveur de site.** lors de la défaillance d'un serveur de site, les informations sur les packages et applications inclus dans la bibliothèque de contenu sont restaurées vers la base de données de site dans le cadre du processus de restauration, mais les fichiers de la bibliothèque de contenu ne sont pas restaurés dans le cadre du processus. Si vous ne disposez pas d’une sauvegarde du système de fichiers pour restaurer la bibliothèque de contenu, vous pouvez créer un fichier de contenu préparé à partir d’un autre site contenant les packages et applications que vous devez avoir. Vous pouvez ensuite extraire le fichier de contenu préparé sur le serveur de site récupéré. Pour plus d’informations sur la sauvegarde et la récupération du serveur de site, consultez [Sauvegarde et récupération pour System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  
