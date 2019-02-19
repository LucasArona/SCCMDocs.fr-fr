---
title: Scénarios de déploiement de systèmes d’exploitation d’entreprise
titleSuffix: Configuration Manager
description: En savoir plus sur différents scénarios de déploiement de systèmes d’exploitation d’entreprise avec System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92b968a8dae63d15e087e098452b56b0397c7b78
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137573"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>Scénarios pour déployer des systèmes d’exploitation d’entreprise avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les scénarios de déploiement de système d’exploitation suivants sont disponibles dans System Center Configuration Manager :  

-   [Mettre à niveau Windows vers la dernière version](upgrade-windows-to-the-latest-version.md) : ce scénario met à niveau le système d’exploitation sur les ordinateurs qui exécutent actuellement Windows 7, Windows 8, Windows 8.1 ou Windows 10. Le processus de mise à niveau conserve les applications, les paramètres et les données utilisateur sur l’ordinateur. Il n’existe aucune dépendance externe, telle que Windows ADK, et ce processus est plus rapide et plus fiable que les déploiements de système d’exploitation traditionnels.  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md) : ce scénario partitionne et formate (efface) un ordinateur existant, et installe un nouveau système d’exploitation sur l’ordinateur. Vous pouvez migrer les données et paramètres utilisateur une fois le système d’exploitation installé.  

-   [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md) : ce scénario installe un système d’exploitation sur un nouvel ordinateur. Il s’agit d’une nouvelle installation du système d’exploitation. Elle n’inclut pas de paramètres ou de migration des données utilisateur.  

-   [Remplacer un ordinateur existant et transférer des paramètres](replace-an-existing-computer-and-transfer-settings.md) : ce scénario installe un système d’exploitation sur un nouvel ordinateur. Si vous le souhaitez, vous pouvez migrer des données et des paramètres utilisateur de l’ancien ordinateur vers le nouvel ordinateur.  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>Éléments à prendre en compte avant de déployer des images de système d’exploitation  
 Vous devez prendre en compte certains éléments avant de déployer un système d’exploitation.  

### <a name="operating-system-image-size"></a>Taille de l'image du système d'exploitation  
 La taille de l'image d'un système d'exploitation peut être très grande. Par exemple, la taille de l'image de Windows 7 est de 3 gigaoctets (Go) au minimum. La taille de l'image et le nombre d'ordinateurs sur lesquels vous déployez simultanément le système d'exploitation affecte les performances du réseau et la bande passante disponible. Veillez à tester les performances du réseau pour mieux mesurer les effets du déploiement de l'image et le temps nécessaire pour terminer le déploiement. Les activités Configuration Manager qui affectent les performances du réseau incluent la distribution de l'image à un point de distribution, la distribution de l'image d'un site vers un autre et le téléchargement de l'image sur le client Configuration Manager.  

 Veillez également à prévoir un espace disque suffisant sur les points de distribution qui hébergent les images du système d'exploitation.  

### <a name="client-cache-size"></a>Taille de cache du client  
 Lorsque les clients Configuration Manager téléchargent du contenu, ils utilisent automatiquement le protocole BITS (Background Intelligent Transfer Service), s'il est disponible. Lorsque vous déployez une séquence de tâches qui installe un système d'exploitation, vous pouvez définir une option sur le déploiement pour que les clients Configuration Manager téléchargent l'image complète dans un cache local avant d'exécuter la séquence de tâches.  

 En général, quand un client Configuration Manager doit télécharger une image de système d’exploitation (ou tout autre package), mais que l’espace est insuffisant dans le cache, le client vérifie les autres packages du cache pour déterminer si la suppression de tout ou partie des anciens packages permettra de libérer un espace disque suffisant pour placer l’image. Si la suppression des packages ne permet pas de libérer suffisamment d’espace disque, le client ne télécharge pas l’image et le déploiement échoue. Cela peut se produire si le cache comporte un package important configuré pour rester dans le cache. Si la suppression des packages permet de libérer suffisamment d’espace disque dans le cache, le client les supprime, puis télécharge l’image dans le cache.  

 La taille du cache par défaut sur les clients Configuration Manager n'est peut-être pas suffisante pour la plupart des déploiements d'image de système d'exploitation. Si vous planifiez de télécharger l'image complète dans le cache du client, vous devez régler la taille du cache du client Configuration Manager sur les ordinateurs de destination pour qu'il puisse héberger la taille de l'image déployée.  

 Pour plus d'informations, voir [Configurer le cache du client pour les clients Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## <a name="task-sequence-deployments"></a>Déploiements de séquences de tâches  
 La séquence de tâches que vous créez peut déployer l'image du système d'exploitation sur un ordinateur client Configuration Manager selon l'une des manières suivantes :  

- Téléchargez d'abord l'image et son contenu dans le cache du client Configuration Manager à partir d'un point de distribution, puis installez-le.  

- Installez immédiatement l'image et son contenu à partir du point de distribution.  

- Installer l'image et son contenu comme requis à partir du point de distribution  

  Par défaut, lorsque vous créez le déploiement pour la séquence de tâches, l'image est d'abord téléchargée dans le cache du client Configuration Manager, puis installée. Si vous choisissez de télécharger l’image dans le cache du client Configuration Manager avant de l’exécuter, et si la séquence de tâches contient une étape de repartitionnement du disque dur, cette étape de repartitionnement échoue car le partitionnement du disque dur efface le contenu du cache du client Configuration Manager. Si la séquence de tâches doit repartitionner le disque dur, vous devez exécuter l'installation de l'image depuis le point de distribution à l'aide de l'option **Exécuter le programme à partir du point de distribution**  quand vous déployez la séquence de tâches.  

  Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
