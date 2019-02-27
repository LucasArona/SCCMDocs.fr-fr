---
title: Préparer des rôles de système de site pour OSD
titleSuffix: Configuration Manager
description: Configurer les rôles de système de site avant de déployer des systèmes d’exploitation dans Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c7f54ccda217ebbae543b70aeead37f6c55cf0f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125684"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Préparer des rôles de système de site pour les déploiements de système d’exploitation avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour déployer des systèmes d’exploitation dans Configuration Manager, commencez par préparer les rôles de système de site suivants qui nécessitent des configurations et des considérations spécifiques.



##  <a name="BKMK_DistributionPoints"></a> Points de distribution  

Le rôle de système de site du point de distribution héberge les fichiers sources que les clients doivent télécharger. Ce contenu est destiné aux applications, mises à jour logicielles, images de système d’exploitation, images de démarrage et packages de pilotes. Contrôlez la distribution du contenu à l’aide de la bande passante, de la limitation et des options de planification.  

Vérifiez que vous avez suffisamment de points de distribution pour prendre en charge le déploiement de systèmes d’exploitation sur les ordinateurs. Planifiez également le placement de ces points de distribution dans votre hiérarchie. Pour plus d’informations, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure). Cet article comprend d’autres considérations de planification pour les points de distribution spécifiques du déploiement de systèmes d’exploitation.  


###  <a name="BKMK_AdditionalPlanning"></a> Considérations de planification supplémentaires concernant les points de distribution  

Tenez compte des éléments de planification supplémentaires suivants pour les points de distribution :  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Comment empêcher les déploiements de système d’exploitation indésirables ?  
Configuration Manager ne fait pas la distinction entre les serveurs de site et les autres ordinateurs de destination d’un regroupement. Si vous déployez une séquence de tâches obligatoire sur un regroupement qui contient un serveur de site, ce dernier exécute la séquence de tâches de la même manière que les autres ordinateurs du regroupement. Vérifiez que votre déploiement de système d’exploitation utilise un regroupement qui comprend les clients prévus.  

Gérez le comportement des déploiements de séquences de tâches à haut risque. Un déploiement à haut risque, qui est installé automatiquement sur un client, est susceptible d’entraîner des résultats indésirables. Il s’agit, par exemple, d’une séquence de tâches avec l’objectif Obligatoire qui déploie un système d’exploitation. Pour réduire la possibilité d’un déploiement à haut risque indésirable, configurez des paramètres de vérification de déploiement. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Combien d’ordinateurs peuvent recevoir simultanément une image de système d’exploitation à partir d’un point de distribution unique ?  
Pour estimer le nombre de points de distribution dont vous avez besoin, examinez les variables suivantes :  
- La vitesse de traitement du point de distribution
- La vitesse de disque du point de distribution
- La bande passante disponible sur le réseau
- La taille du package d’images   
  
Par exemple, si l’on fait abstraction des autres facteurs de ressource de serveur, le nombre maximal d’ordinateurs capables de traiter un package d’images de 4 Go en une heure sur un réseau Ethernet de 100 mégaoctets/s est de 11.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Si vous devez déployer un système d’exploitation sur un nombre spécifique d’ordinateurs dans un délai spécifique, distribuez l’image sur un nombre approprié de points de distribution.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Puis-je déployer un système d’exploitation sur un point de distribution ?  
Vous pouvez déployer un système d’exploitation sur un point de distribution, mais l’image de système d’exploitation doit être reçue d’un autre point de distribution.  


###  <a name="BKMK_PXEDistributionPoint"></a> Configuration de points de distribution pour accepter des requêtes PXE  

Pour déployer des systèmes d’exploitation sur des clients Configuration Manager qui effectuent des demandes de démarrage PXE, configurez un ou plusieurs points de distribution pour accepter les demandes PXE. Une fois le point de distribution configuré, il répond aux demandes de démarrage PXE et détermine l’action de déploiement appropriée. Pour plus d’informations, consultez [Installer ou modifier un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).  


###  <a name="BKMK_RamDiskTFTP"></a> Personnaliser les tailles de bloc et de fenêtre TFTP RamDisk sur des points de distribution compatibles PXE  

Vous pouvez personnaliser les tailles de bloc et de fenêtre TFTP RamDisk pour des points de distribution compatibles PXE. Si vous avez personnalisé votre réseau, une taille importante de bloc ou de fenêtre peut entraîner l’échec du téléchargement de l’image de démarrage avec une erreur d’expiration de délai. La personnalisation des tailles de bloc et de fenêtre TFTP RamDisk permet d’optimiser le trafic TFTP quand vous utilisez PXE pour répondre aux besoins spécifiques de votre réseau. Pour déterminer la configuration la plus efficace, testez les paramètres personnalisés dans votre environnement.  

-   **Taille de bloc TFTP** : il s’agit de la taille des paquets de données que le serveur envoie au client qui télécharge le fichier. Plus la taille de bloc est importante, moins le serveur envoie de paquets. Il y a donc moins de délais d’aller et retour entre le serveur et le client. Toutefois, une taille de bloc importante entraîne la fragmentation des paquets, ce qui n’est pas pris en charge par la plupart des implémentations du client PXE.  

-   **Taille de fenêtre TFTP** : le protocole TFTP nécessite le renvoi d’un paquet d’accusé de réception (ACK) pour chaque bloc de données envoyé. Le serveur n’envoie pas le bloc suivant dans la séquence tant qu’il n’a pas reçu le paquet ACK pour le bloc précédent. Le fenêtrage TFTP vous permet de définir le nombre de blocs de données nécessaires pour remplir une fenêtre. Le serveur envoie les blocs de données dos à dos jusqu’à ce que la fenêtre soit remplie, et le client renvoie un paquet ACK. Si vous augmentez cette taille de fenêtre, vous réduisez aussi bien le nombre de délais d’aller et retour entre le client et le serveur que le temps global nécessaire au téléchargement d’une image de démarrage.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Modifier la taille de fenêtre TFTP RamDisk  
Pour personnaliser la taille de fenêtre TFTP RamDisk, ajoutez la clé de Registre suivante sur les points de distribution compatibles PXE :  

- **Emplacement** : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nom** : RamDiskTFTPWindowSize  
- **Type** : REG_DWORD  
- **Valeur** : (taille de fenêtre personnalisée)  
    - La valeur par défaut est **1** (un bloc de données remplit la fenêtre).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Modifier la taille de bloc TFTP RamDisk  
Pour personnaliser la taille de fenêtre TFTP RamDisk, ajoutez la clé de Registre suivante sur les points de distribution compatibles PXE :  

- **Emplacement** : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Nom** : RamDiskTFTPBlockSize  
- **Type** : REG_DWORD  
- **Valeur** : (taille de bloc personnalisée)  
    - La valeur par défaut est **4096**.  

> [!Note]  
> Les Services de déploiement Windows et le service de répondeur PXE de Configuration Manager prennent en charge ces configurations TFTP.  


###  <a name="BKMK_DPMulticast"></a> Configurer des points de distribution pour prendre en charge la multidiffusion  

La multidiffusion est une méthode d’optimisation du réseau. Utilisez-la sur les points de distribution quand plusieurs clients sont susceptibles de télécharger la même image de système d’exploitation en même temps. Quand vous utilisez la multidiffusion, plusieurs ordinateurs peuvent télécharger simultanément l’image de système d’exploitation, car celle-ci est multidiffusée par le point de distribution. Sans multidiffusion, le point de distribution envoie une copie des données à chaque client sur une connexion distincte. Pour plus d’informations, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

Avant de déployer le système d’exploitation, configurez un point de distribution pour prendre en charge la multidiffusion. Pour plus d'informations, consultez [Installer et configurer des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-multicast).



##  <a name="BKMK_StateMigrationPoints"></a> Point de migration d'état  

Le point de migration d’état stocke les données d’état utilisateur que USMT capture sur un ordinateur et restaure sur un autre. Toutefois, quand vous capturez des paramètres utilisateur pour un déploiement de système d’exploitation sur le même ordinateur, par exemple, un déploiement où vous actualisez Windows sur l’ordinateur de destination, vous pouvez choisir de stocker les données sur le même ordinateur à l’aide de liens physiques ou d’utiliser un point de migration d’état. Pour certains déploiements d’ordinateur, quand vous créez le magasin d’état, Configuration Manager crée automatiquement une association entre le magasin d’état et l’ordinateur de destination. Au moment de planifier le point de migration d’état, tenez compte des facteurs suivants :    


### <a name="user-state-size"></a>Taille de l’état utilisateur  

La taille de l'état utilisateur affecte directement le stockage sur disque sur le point de migration d'état, ainsi que les performances réseau au cours de la migration. Réfléchissez à la taille de l'état utilisateur et au nombre d'ordinateurs à migrer. Pensez également aux paramètres à migrer à partir de l'ordinateur. Par exemple, si le dossier **Mes documents** est déjà sauvegardé sur un serveur, vous n’avez peut-être pas besoin de le migrer dans le cadre du déploiement d’image. Évitez les migrations inutiles pour ne pas augmenter la taille globale de l’état utilisateur et pour réduire l’incidence sur les performances réseau et le stockage sur disque au niveau du point de migration d’état.  


### <a name="user-state-migration-tool"></a>Outil de migration de l'état utilisateur  

Pour capturer et restaurer l’état utilisateur pendant le déploiement des systèmes d'exploitation, utilisez un package de l’outil de migration utilisateur (USMT) qui pointe vers les fichiers sources USMT. Configuration Manager crée automatiquement ce package dans la console Configuration Manager dans **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**. Configuration Manager utilise USMT 10 pour capturer l’état utilisateur d’un système d’exploitation et le restaurer sur un autre. Le Kit de déploiement et d’évaluation Windows (Windows ADK) pour Windows 10 inclut USMT 10.

Pour obtenir une description des différents scénarios de migration pour USMT 10, consultez [Scénarios de migration courants](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) dans la documentation Windows.  


### <a name="retention-policy"></a>Stratégie de rétention  

Quand vous configurez le point de migration d’état, spécifiez la durée de conservation des données d’état utilisateur qu’il stocke. La durée de conservation des données sur le point de migration d'état dépend de deux éléments :  

-   L'effet que les données stockées ont sur le stockage sur disque.  

-   La nécessité potentielle de conserver les données pendant un certain temps dans le cas où vous devez migrer à nouveau les données.  
  
  
La migration de l’état se produit en deux phases : la capture des données et la restauration des données. Quand vous capturez des données, les données d’état utilisateur sont collectées et enregistrées sur le point de migration d’état. Lorsque vous restaurez les données, les données d'état utilisateur sont récupérées depuis le point de migration d'état et écrites sur l'ordinateur de destination, puis l'étape de séquence de tâches **Libérer le magasin d'état** libère les données stockées. Lorsque les données sont libérées, le minuteur de rétention démarre. Si vous choisissez de supprimer immédiatement les données migrées, les données d’état utilisateur sont supprimées dès leur publication. Si vous choisissez de conserver les données pendant un certain temps, les données seront supprimées une fois cette période écoulée, après la publication des données d'état. Plus la période de rétention définie est longue, plus l'espace disque dont vous pouvez avoir besoin est grand.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Sélectionner le disque pour stocker les données de migration d’état utilisateur  

Lorsque vous configurez le point de migration d’état, spécifiez le lecteur sur le serveur pour stocker les données de migration utilisateur. Vous sélectionnez un lecteur à partir d'une liste de lecteurs fixe. Toutefois, certains de ces lecteurs peuvent représenter des lecteurs non inscriptibles, tels que le lecteur de CD, ou un lecteur de partage non réseau. Certaines lettres de lecteurs peuvent ne pas être mappées à des lecteurs sur l'ordinateur. Spécifiez un lecteur partagé accessible en écriture quand vous configurez un point de migration d’état.  


### <a name="configure-a-state-migration-point"></a>Configuration d'un point de migration d'état  

Utilisez les méthodes suivantes afin de configurer un point de migration d’état pour stocker les données d’état utilisateur :  

-   Utilisez l' **Assistant Création d'un serveur de système de site** pour créer un nouveau serveur de système de site pour le point de migration d'état.  

-   Utilisez l' **Assistant Ajout des rôles de système de site** pour ajouter un point de migration d'état à un serveur existant.  

Quand vous utilisez ces Assistants, vous êtes invité à fournir les informations suivantes pour le point de migration d’état :  

-   Les dossiers pour stocker les données d'état utilisateur.  

-   Le nombre maximal de clients pouvant stocker des données sur le point de migration d'état.  

-   L'espace libre minimum pour le point de migration d'état pour stocker les données d'état utilisateur.  

-   La stratégie de suppression du rôle. Spécifiez que les données d’état utilisateur doivent être supprimées immédiatement après leur restauration sur un ordinateur, ou au bout d’un nombre de jours spécifique après la restauration des données utilisateur sur un ordinateur.  

-   Si le point de migration d’état répond uniquement aux demandes de restauration des données d’état utilisateur. Lorsque vous activez cette option, vous ne pouvez pas utiliser le point de migration d’état pour stocker les données d’état utilisateur.  

Pour connaître les étapes à suivre pour installer un rôle de système de site, consultez [Ajouter des rôles de système de site](/sccm/core/servers/deploy/configure/add-site-system-roles).  
