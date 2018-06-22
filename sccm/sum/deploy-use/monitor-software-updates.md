---
title: Surveiller les mises à jour logicielles
titleSuffix: Configuration Manager
description: La console System Center Configuration Manager fournit des alertes et des états pour surveiller les mises à jour et la compatibilité.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/20/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: bc594fe6b870e1054033601a67209aa9ad72ccef
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351857"
---
# <a name="monitor-software-updates-in-system-center-configuration-manager"></a>Surveiller les mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager fournit de nombreuses méthodes pour vous aider à surveiller les objets de mises à jour logicielles, les processus et les informations de conformité. Utilisez les sections suivantes pour surveiller les mises à jour logicielles.

## <a name="software-updates-dashboard"></a>Tableau de bord des mises à jour logicielles
À partir de Configuration Manager version 1610, vous pouvez utiliser le tableau de bord des mises à jour logicielles pour afficher l’état de compatibilité actuel des appareils de votre organisation et analyser rapidement les données pour identifier les appareils qui sont exposés. Pour afficher le tableau de bord, accédez à **Surveillance** > **Vue d’ensemble** > **Sécurité** > **Software Updates Dashboard** (Tableau de bord des mises à jour logicielles).   

##  <a name="BKMK_SUAlerts"></a> Alertes pour les mises à jour logicielles  
 Vous pouvez configurer des alertes pour les mises à jour logicielles afin d'avertir les utilisateurs administratifs lorsque les niveaux de conformité pour les déploiements de mises à jour logicielles sont inférieurs au pourcentage configuré. Vous pouvez configurer des alertes pour les déploiements de mises à jour logicielles aux emplacements suivants :  

-   Paramètre ADR : vous pouvez configurer les paramètres des alertes dans l’Assistant Règle de déploiement automatique et dans les propriétés de la règle de déploiement automatique.  

-   Paramètre de déploiement : vous pouvez configurer les paramètres des alertes dans l’Assistant Déploiement des mises à jour logicielles et dans les propriétés de déploiement.  

Après avoir configuré les paramètres d’alerte, si les conditions spécifiées sont remplies, Configuration Manager génère une alerte. Vous pouvez consulter les alertes des mises à jour logicielles aux emplacements suivants :  

1.  Consultez les alertes récentes dans le nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

2.  Gérez les alertes configurées dans le nœud **Alertes** dans l'espace de travail **Surveillance** .  

##  <a name="BKMK_SUSyncStatus"></a> État de synchronisation des mises à jour logicielles  
 Après avoir lancé le processus de synchronisation, vous pouvez le surveiller à partir de la console Configuration Manager pour tous les points de mise à jour logicielle de votre hiérarchie. Pour surveiller le processus de synchronisation des mises à jour logicielles, procédez comme suit.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Pour surveiller le processus de synchronisation des mises à jour logicielles  

- Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **État de la synchronisation du point de mise à jour logicielle**.  

    Les points de mise à jour logicielle de votre hiérarchie Configuration Manager sont affichés dans le volet des résultats. Dans cette vue, vous pouvez surveiller l'état de synchronisation pour tous les points de mise à jour logicielle. Pour plus d’informations sur le processus de synchronisation, vous pouvez consulter le fichier wsyncmgr.log qui se trouve dans <*chemin_installation_Configuration_Manager*>\Logs sur chaque serveur de site.  

##  <a name="BKMK_SUDeployStatus"></a> État de déploiement des mises à jour logicielles  
 Après avoir déployé les mises à jour logicielles dans un groupe de mises à jour logicielles ou déployé une mise à jour logicielle individuelle, vous pouvez surveiller l'état du déploiement. Pour surveiller l'état de déploiement d'un groupe de mises à jour logicielles ou d'une mise à jour logicielle, procédez comme suit.  

#### <a name="to-monitor-deployment-status"></a>Pour surveiller l'état d'un déploiement  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **Déploiements**.  

2.  Cliquez sur le groupe de mises à jour logicielles ou sur la mise à jour logicielle de laquelle vous voulez surveiller l'état de déploiement.  

3.  Dans l'onglet **Accueil** , du groupe **Déploiement** , cliquez sur **Afficher l'état**.  

##  <a name="BKMK_SUReports"></a> Rapports des mises à jour logicielles  
 Les messages d'état des mises à jour logicielles fournissent des informations sur la conformité des mises à jour logicielles et présentent l'état de l'évaluation et de l'application des déploiements des mises à jour logicielles. Vous pouvez exécuter des rapports de mises à jour logicielles pour afficher ces messages d'état. Il existe plus de 30 rapports de mises à jour logicielles prédéfinis disponibles. Ceux-ci sont organisés en plusieurs catégories et peuvent être utilisés pour signaler des informations spécifiques sur les mises à jour logicielles et les déploiements. En plus d'utiliser les rapports préconfigurés, vous pouvez également créer des rapports de mises à jour logicielles personnalisés selon les besoins de votre entreprise. Pour plus d’informations, consultez [Opérations et maintenance pour les rapports](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Surveiller le contenu  
 Vous pouvez surveiller le contenu dans la console Configuration Manager pour déterminer l’état de tous les types de package en rapport avec les points de distribution associés, notamment l'état de validation du contenu du package, l'état du contenu attribué à un groupe de points de distribution spécifique, l'état du contenu attribué à un point de distribution et l'état des fonctions facultatives de chaque point de distribution (validation du contenu, PXE et multidiffusion).  

###  <a name="BKMK_ContentStatus"></a> Surveillance de l’état du contenu  
 Le nœud **État du contenu** dans l'espace de travail **Surveillance** fournit des informations sur les packages de contenu. Vous pouvez consulter les informations générales sur l'emballage, l'état de distribution pour le package et les informations d'état détaillées sur le package. Pour afficher l'état du contenu, procédez comme suit.  

#### <a name="to-monitor-content-status"></a>Pour surveiller l'état du contenu  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **État de distribution** > **État du contenu**. Les packages sont affichés.  

2.  Sélectionnez le package pour lequel afficher des informations d'état détaillées.  

3.  Dans l'onglet **Accueil** , cliquez sur **Afficher l'état**. Des informations d'état détaillées pour le package sont affichées.  

###  <a name="BKMK_DPGroupStatus"></a> État du groupe de points de distribution  
 Le nœud **État du groupe de points de distribution** dans l'espace de travail **Surveillance** fournit des informations sur les groupes de points de distribution. Vous pouvez consulter les informations générales sur le groupe de points de distribution, notamment l'état du groupe de points de distribution et le degré de conformité, ainsi que les informations d'état détaillées pour le groupe de points de distribution. Pour afficher l'état du groupe de points de distribution, procédez comme suit.  

#### <a name="to-monitor-distribution-point-group-status"></a>Pour surveiller l'état du groupe de points de distribution  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **État de distribution** > **État du groupe de points de distribution**. Les groupes de points de distribution sont affichés.  

2.  Sélectionnez le groupe de points de distribution pour lequel afficher des informations d'état détaillées.  

3.  Dans l'onglet **Accueil** , cliquez sur **Afficher l'état**. Des informations d'état détaillées pour le groupe de points de distribution sont affichées.  

###  <a name="BKMK_DPConfigStatus"></a> État de configuration du point de distribution  
 Le nœud **État de configuration du point de distribution** dans l'espace de travail **Surveillance** fournit des informations sur le point de distribution. Vous pouvez examiner les attributs qui sont activés pour le point de distribution, par exemple, PXE, multidiffusion et validation du contenu. Vous pouvez également afficher des informations d'état détaillées pour le point de distribution. Pour afficher l'état de configuration du point de distribution, procédez comme suit.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Pour surveiller l'état de configuration du point de distribution  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **État de distribution** > **État de la configuration du point de distribution**. Les points de distribution sont affichés.  

2.  Sélectionnez le point de distribution pour lequel afficher des informations d'état du point de distribution.  

3.  Dans le volet des résultats, cliquez sur l'onglet **Détails** . Des informations d'état pour le point de distribution sont affichées.  
