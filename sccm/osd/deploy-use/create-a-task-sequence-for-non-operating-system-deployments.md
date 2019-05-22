---
title: Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation
titleSuffix: Configuration Manager
description: Créez des séquences de tâches qui ne servent pas à déployer un système d’exploitation, par exemple pour distribuer des logiciels ou automatiser des tâches.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17ba0f146a80928b1eaae6334e6418a5e08b1114
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083062"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, les séquences de tâches permettent d’automatiser différents types de tâches dans l’environnement. Ces tâches visent essentiellement à déployer des systèmes d’exploitation et sont testées à cet effet. Configuration Manager possède de nombreuses autres fonctionnalités ; utilisez en priorité ces technologies dans les scénarios suivants :

- [Installation d’application](/sccm/apps/understand/introduction-to-application-management)
- [Installation de mises à jour de logiciels](/sccm/sum/understand/software-updates-introduction)
- [Définition de la configuration](/sccm/compliance/understand/ensure-device-compliance)

Explorez également d’autres technologies d’automatisation Microsoft System Center, notamment [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) et [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

Toute la puissance des séquences de tâches réside dans leur flexibilité et leur application. Elles peuvent configurer des paramètres client, distribuer des logiciels, mettre à jour des pilotes, modifier des états utilisateur et effectuer d’autres tâches indépendantes du déploiement de système d’exploitation. Vous pouvez créer une séquence de tâches personnalisée pour ajouter un nombre quelconque de tâches. Dans le cadre d’un déploiement hors déploiement de système d’exploitation, les séquences de tâches personnalisées sont prises en charge dans Configuration Manager. Toutefois, si une séquence de tâches entraîne des résultats indésirables ou incohérents, essayez de simplifier l’opération :

- Utilisez les étapes plus simples.
- Divisez les actions sur plusieurs séquences de tâches.
- Suivez une approche par phases pour créer et tester la séquence de tâches.

Les étapes suivantes peuvent être utilisées dans une séquence de tâches personnalisée pour un déploiement hors déploiement de système d’exploitation :  

- [Vérifier la préparation](/sccm/osd/understand/task-sequence-steps#BKMK_CheckReadiness)  

- [Se connecter à un dossier réseau](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  

- [Télécharger le contenu du package](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)  

- [Installer l’application](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)  

- [Installer le package](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)  

- [Installer les mises à jour logicielles](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)  

- [Redémarrer l’ordinateur](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)  

- [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- [Exécuter le script PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)  

- [Exécuter une séquence de tâches](/sccm/osd/understand/task-sequence-steps#child-task-sequence)  

- [Définir des variables dynamiques](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)  

- [Définir la variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)  
