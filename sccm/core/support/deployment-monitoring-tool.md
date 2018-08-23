---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Utilisez Deployment Monitoring Tool pour résoudre les problèmes de déploiements de logiciels sur un client Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 67a052fffcaf6ad105f417649aa9f3826922ce80
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385890"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*S’applique à : System Center Configuration Manager (Current Branch)*

Deployment Monitoring Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Il s’agit d’une interface graphique utilisateur conçue pour vous aider à dépanner les déploiements d’applications, de mises à jour logicielles et de bases de référence de configuration sur un client Configuration Manager. L’outil est en lecture seule et ne change aucun état sur le client. Vous pouvez l’utiliser en toute confiance pour diagnostiquer les scénarios de déploiement courants.


## <a name="features"></a>Fonctionnalités

- Exécutez-le en tant qu’administrateur pour dépanner les déploiements sur un client local.  

- Dépannez les déploiements sur un client distant. Lancez l’outil et connectez-vous à un ordinateur distant en tant qu’administrateur.  

- Exportez au format XML toutes les données collectées dans l’outil. Partagez le fichier XML avec d’autres personnes et utilisez-le comme plateforme commune pour parler du dépannage des déploiements.  

- Importez les données déjà exportées vers un autre ordinateur et utilisez celui-ci pour exécuter l’outil en mode hors connexion.   


## <a name="usage"></a>Utilisation

Deployment Monitoring Tool prend en charge l’interface graphique utilisateur uniquement. Pour lancer l’outil, exécutez **DeploymentMonitoringTool.exe** en tant qu’administrateur. Il se compose de trois vues :  

- **Client Properties** (Propriétés du client) : liste des attributs utiles sur l’appareil et le client Configuration Manager. Il s’agit de la vue par défaut.   

- **Deployments** (Déploiements) : affichage de tous les déploiements actuellement ciblés. Sélectionnez un déploiement dans le volet de résultats pour voir plus d’informations dans le volet des détails.  

- **All Updates** (Toutes les mises à jour) : affichage de toutes les mises à jour logicielles et leur état.  

Pour copier des données dans une des vues, sélectionnez une cellule et appuyez sur **CTRL** + **C**.


### <a name="actions-menu"></a>Menu Actions

Les actions suivantes sont disponibles dans le menu **Actions** :  

- **Connect to remote machine** (Se connecter à l’ordinateur distant) : sélectionnez un ordinateur auquel se connecter. Si vous ne spécifiez pas un nom d’utilisateur et un mot de passe, l’outil utilise les informations d’identification actuelles. Cliquez sur **Save** (Enregistrer) pour vous connecter à un ordinateur distant.  

- **Exporter des données** : sélectionnez le fichier dans lequel écrire des données et cliquez sur **Save** (Enregistrer). Utilisez le fichier XML exporté pour le dépannage à distance sur un autre ordinateur.  

- **Import Data** (Importer les données) : sélectionnez un fichier à importer dans l’outil.  

- **View Log** (Voir le journal) : ouvre un fichier journal associé, en fonction de la vue :  
    - Client Properties (Propriétés du client) : `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Deployments (Déploiements) : `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - All Updates (Toutes les mises à jour) : `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Voir aussi

- [Déployer des applications](/sccm/apps/deploy-use/deploy-applications)
- [Déployer des mises à jour logicielles](/sccm/sum/deploy-use/deploy-software-updates)
- [Déployer des bases de référence de configuration](/sccm/compliance/deploy-use/deploy-configuration-baselines)
