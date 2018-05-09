---
title: Simuler des déploiements d’applications
titleSuffix: Configuration Manager
description: Évaluez la méthode de détection, les exigences et les dépendances d’un type de déploiement sans installer l’application.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bd2f4f24a9bc22daac5b5c6e785ff2ea5d02f49a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simuler des déploiements d’applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser des déploiements simulés pour tester le déploiement d’une application sans installer ni désinstaller l’application. Un déploiement simulé évalue la méthode de détection, les exigences et les dépendances d’un type de déploiement. Les résultats sont signalés dans le nœud **Déploiements** de l’espace de travail **Analyse**. Utilisez la procédure indiquée dans cette rubrique pour simuler un déploiement d’application dans System Center Configuration Manager (Configuration Manager).  

> [!NOTE]  
> Vous ne pouvez pas utiliser les déploiements simulés pour les regroupements d'appareils mobiles.  
>   
> Vous ne pouvez pas déployer une application dont l'objet de déploiement est **Désinstaller** si un déploiement simulé de la même application est actif.  

## <a name="configure-a-simulated-application-deployment"></a>Configurer un déploiement d’application simulé

1.  Dans la console Configuration Manager, sélectionnez un des éléments suivants :  
    -   Un regroupement d'utilisateurs.  
    -   Un regroupement de périphériques.  
    -   Une application Configuration Manager.  

2.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Simuler un déploiement**.  

3.  Dans l’Assistant Simuler un déploiement d’application, définissez les détails suivants pour votre déploiement simulé :  

    -   **Application**. Choisissez **Parcourir**, puis sélectionnez l’application pour laquelle vous souhaitez créer une simulation de déploiement.  

    -   **Regroupement**. Choisissez **Parcourir**, puis sélectionnez le regroupement à utiliser pour le déploiement simulé.  

    -   **Action**. Dans la liste déroulante, indiquez si vous souhaitez simuler l’installation ou la désinstallation de l’application sélectionnée.  

    -   **Déployer automatiquement avec ou sans connexion de l’utilisateur**. Si cette option est cochée, les clients évaluent le déploiement simulé, qu’ils soient connectés ou non.  

4.  Cliquez sur **Suivant**, consultez les informations indiquées dans la page **Résumé**, puis terminez l’Assistant pour créer le déploiement d’application simulé.  

5.  Les applications simulées apparaissent dans le nœud **Déploiements** de l’espace de travail **Analyse** et leur objet est **Simuler**. Pour plus d’informations sur la surveillance des déploiements d’applications, consultez [Surveiller des applications à partir de la console System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).  
