---
title: Préparer le déploiement de système d’exploitation
titleSuffix: Configuration Manager
description: Découvrez comment préparer un déploiement de système d’exploitation dans Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8d27e5ac-4f19-4b3d-85c7-fa34eb5d5e7e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7e303a7363e0641210cc7c6e436546d864fe0571
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838716"
---
# <a name="prepare-for-os-deployment-in-configuration-manager"></a>Préparer un déploiement de système d’exploitation dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous devez effectuer plusieurs opérations dans Configuration Manager avant de pouvoir déployer des systèmes d’exploitation. Lisez les articles suivants pour préparer un déploiement de système d’exploitation :  

-   [Gérer les images de démarrage](manage-boot-images.md)  

-   [Gérer les images de système d’exploitation](manage-operating-system-images.md)  

-   [Gérer les packages de mise à niveau de système d’exploitation](manage-operating-system-upgrade-packages.md)  

-   [Gérer les pilotes](manage-drivers.md)  

-   [Gérer l’état utilisateur](manage-user-state.md)  

-   [Préparer les déploiements d’ordinateurs inconnus](prepare-for-unknown-computer-deployments.md)  

-   [Associer des utilisateurs à un ordinateur de destination](associate-users-with-a-destination-computer.md)  



### <a name="os-image-size"></a>Taille des images de système d’exploitation  

Les images de système d’exploitation sont de grande taille. Par exemple, celle de Windows 7 fait au moins 3 Go. La taille de l’image et le nombre d’ordinateurs sur lesquels le système d’exploitation est déployé simultanément ont une incidence sur les performances du réseau et sur la bande passante disponible. Veillez à tester les performances du réseau, pour mieux évaluer l’effet potentiel du déploiement de l’image et le temps nécessaire au déploiement. Parmi les activités Configuration Manager qui affectent les performances réseau figurent la distribution de l’image à un point de distribution, sa distribution d’un site vers un autre et son téléchargement sur le client.  

Veillez également à prévoir un espace de stockage sur disque suffisant sur les points de distribution qui hébergent les images de système d’exploitation.  

Pour plus d’informations, voir [Considérations supplémentaires en matière de planification pour les points de distribution](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_AdditionalPlanning).


### <a name="client-cache-size"></a>Taille de cache du client  

Lorsque les clients Configuration Manager téléchargent du contenu, ils utilisent automatiquement le Service de transfert intelligent en arrière-plan (BITS), s’il est disponible. Lors du déploiement d’une séquence de tâches qui installe un système d’exploitation, vous pouvez définir une option de déploiement spécifiant que les clients Configuration Manager téléchargent l’image complète dans un cache local avant l’exécution de la séquence de tâches.  

Un client Configuration Manager qui doit télécharger une image de système d’exploitation sans disposer d’un espace suffisant dans le cache peut en libérer. Il vérifie les autres packages présents dans le cache pour déterminer si le fait de supprimer d’anciens packages permettrait de libérer suffisamment d’espace disque pour l’image. Si la suppression des packages n’est pas suffisante, le client ne télécharge pas l’image et le déploiement échoue. Ce comportement risque de se produire si le cache comporte un package volumineux configuré pour y rester. Si la suppression des packages permet de libérer suffisamment d’espace disque dans le cache, le client les supprime, puis télécharge l’image dans le cache.  

La taille du cache par défaut sur les clients Configuration Manager n’est pas forcément suffisante pour tous les déploiements d’images de système d’exploitation. Si vous prévoyez de télécharger l’image complète dans le cache du client, adaptez la taille de ce dernier sur les ordinateurs de destination à la taille de l’image déployée.  

Pour plus d’informations, voir [Configurer le cache du client](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  


