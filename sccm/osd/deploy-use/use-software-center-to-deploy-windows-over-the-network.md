---
title: Utiliser le Centre logiciel pour déployer Windows sur le réseau
titleSuffix: Configuration Manager
description: Vous pouvez déployer un système d’exploitation dans le Centre logiciel afin d’actualiser un ordinateur existant avec une nouvelle version de Windows ou afin d’effectuer une mise à niveau de Windows vers la version la plus récente.
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99cd37d0034725c85709e454960171714cd3db13
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133814"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utiliser le Centre logiciel pour déployer Windows sur le réseau avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez rendre disponible la séquence de tâches pour installer un système d’exploitation dans System Center Configuration Manager dans le Centre logiciel. Vous pouvez déployer un système d’exploitation dans le Centre logiciel dans les scénarios de déploiement de système d’exploitation suivants :

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md)

Effectuez les étapes dans un des scénarios de déploiement de système d’exploitation. Puis utilisez les sections suivantes pour préparer les déploiements qui sont disponibles dans le centre logiciel.

## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement  
Pour rendre le déploiement de système d’exploitation disponible dans le centre logiciel, configurez le déploiement. Vous pouvez configurer le déploiement dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel ou sous l’onglet **Paramètres de déploiement** dans les propriétés du déploiement. Pour le paramètre **Rendre disponible aux éléments suivants** , sélectionnez **Clients Configuration Manager uniquement** ou **Clients, média et environnement PXE Configuration Manager**. Une fois que le système déploie le système d’exploitation, il est affiché dans le Centre logiciel pour les membres du regroupement cible.

##  <a name="BKMK_Deploy"></a> Déployer la séquence de tâches sur les ordinateurs  
Déployez le système d’exploitation dans un regroupement cible. Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quand vous déployez des systèmes d’exploitation pour le Centre logiciel, vous pouvez configurer si le déploiement est obligatoire ou disponible.

-   **Déploiement obligatoire** : Les déploiements obligatoires rendent le système d’exploitation accessible dans le Centre logiciel, mais il est démarré automatiquement conformément à la planification d’affectation configurée.

-   **Déploiement disponible** : Le système d’exploitation est disponible dans le Centre logiciel et l’utilisateur peut l’installer à la demande.
