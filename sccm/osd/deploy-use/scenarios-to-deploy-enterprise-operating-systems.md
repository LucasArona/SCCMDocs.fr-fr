---
title: Scénarios de déploiement de systèmes d’exploitation d’entreprise
titleSuffix: Configuration Manager
description: Découvrez différents scénarios de déploiement de systèmes d’exploitation d’entreprise avec Configuration Manager.
ms.date: 02/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6d34c3d8dfa753934f03337d68e989a8bf8fcd7
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838699"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-configuration-manager"></a>Scénarios de déploiement de systèmes d’exploitation d’entreprise avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Voici les scénarios de déploiement de systèmes d’exploitation disponibles dans Configuration Manager :  

#### <a name="upgrade-windows-to-the-latest-version"></a>Effectuer une mise à niveau de Windows vers la dernière version
Ce scénario met à niveau le système d’exploitation sur les ordinateurs sous Windows 7, Windows 8.1 ou Windows 10. Ce processus de mise à niveau conserve les applications, les paramètres et les données utilisateur sur l’ordinateur. Il ne présente aucune dépendance externe, comme Windows ADK. Il peut se révéler plus rapide et plus résilient que les déploiements de systèmes d’exploitation traditionnels.  

Pour plus d’informations, consultez [Effectuer une mise à niveau de Windows vers la dernière version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).


#### <a name="windows-autopilot-for-existing-devices"></a>Windows Autopilot pour les appareils existants
<!--3607717, fka 1358333--> Depuis la version 1810, Windows Autopilot pour les appareils existants est disponible avec Windows 10 version 1809 ou ultérieure. Cette fonctionnalité permet de réimager et d’approvisionner un appareil Windows 7 pour Windows Autopilot en mode piloté par l’utilisateur en une seule séquence de tâches Configuration Manager.

Pour plus d’informations, voir [Windows Autopilot pour les appareils existants](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).


#### <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Actualiser un ordinateur existant avec une nouvelle version de Windows
Ce scénario partitionne, formate (efface) un ordinateur existant et y installe un nouveau système d’exploitation. Il est possible de migrer les données et les paramètres utilisateur une fois le système d’exploitation installé.  

Pour plus d’informations, voir [Actualiser un ordinateur existant avec une nouvelle version de Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).


#### <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal"></a>Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)
Ce scénario installe un système d’exploitation sur un nouvel ordinateur. Il s’agit d’une nouvelle installation du système d’exploitation, qui ne comporte pas de migration des paramètres ou des données utilisateur.  

Pour plus d’informations, voir [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal).


#### <a name="replace-an-existing-computer-and-transfer-settings"></a>Remplacer un ordinateur existant et transférer des paramètres
Ce scénario installe un système d’exploitation sur un nouvel ordinateur. Si vous le souhaitez, vous pouvez migrer des données et des paramètres utilisateur de l’ancien ordinateur vers le nouvel ordinateur.  

Pour plus d’informations, consultez [Remplacer un ordinateur existant et transférer des paramètres](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings).


