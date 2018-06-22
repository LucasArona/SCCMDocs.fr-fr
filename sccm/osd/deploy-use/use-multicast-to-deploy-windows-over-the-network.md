---
title: Utiliser la multidiffusion pour déployer Windows sur le réseau
titleSuffix: Configuration Manager
description: Utilisez la multidiffusion dans votre environnement System Center Configuration Manager afin que plusieurs ordinateurs puissent télécharger simultanément l’image du système d’exploitation.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 648146f11336489f30f03c35cb3d648f161b5e69
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347057"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utiliser la multidiffusion pour déployer Windows sur le réseau avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La multidiffusion est une méthode d'optimisation réseau que vous pouvez utiliser dans votre environnement System Center Configuration Manager où plusieurs clients sont susceptibles de télécharger simultanément la même image du système d'exploitation. En cas d'utilisation de la multidiffusion, plusieurs ordinateurs téléchargent simultanément l'image de système d'exploitation lorsqu'elle est multidiffusée par le point de distribution, plutôt que de faire en sorte que le point de distribution envoie une copie des données à chaque client à l'aide d'une connexion distincte.  

 Vous pouvez déployer des systèmes d’exploitation sur le réseau en utilisant la multidiffusion dans les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

 Effectuez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis consultez les sections suivantes pour savoir comment prendre en charge la multidiffusion.  

##  <a name="BKMK_Configure"></a> Configurer un point de distribution pour prendre en charge la multidiffusion  
 Pour utiliser la multidiffusion pendant le déploiement de systèmes d’exploitation, vous devez configurer un point de distribution pour prendre en charge la multidiffusion. Pour plus d'informations, voir [Configurer des points de distribution pour prendre en charge la multidiffusion](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Préparer une image de système d’exploitation pour les déploiements en multidiffusion  
 Pour configurer le package d’images du système d’exploitation dans l’optique d’une prise en charge de la multidiffusion, voir [Préparer l’image du système d’exploitation pour les déploiements en multidiffusion](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Déployer la séquence de tâches  
 Déployez le système d’exploitation dans un regroupement cible. Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  
