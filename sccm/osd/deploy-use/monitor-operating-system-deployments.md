---
title: Surveiller les déploiements de système d’exploitation
titleSuffix: Configuration Manager
description: Pour vous aider à surveiller les objets de déploiement de système d’exploitation, la console Configuration Manager fournit des alertes, des rapports et divers indicateurs d’état.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 08085d94-295c-432f-b5e3-9736bce0193b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6e15f7bea1a600cc2cff2e400b2d793cabf1078
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-operating-system-deployments-in-system-center-configuration-manager"></a>Surveiller les déploiements de système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La console Configuration Manager fournit les méthodes suivantes pour vous aider à surveiller vos objets de déploiement de système d’exploitation.  


##  <a name="BKMK_OSDAlerts"></a> Alertes pour les déploiements de système d’exploitation  
 Vous pouvez configurer une alerte dans les paramètres de déploiement de séquence de tâches pour avertir les utilisateurs administratifs quand les niveaux de conformité du déploiement sont inférieurs au pourcentage configuré.  

 Après avoir configuré les paramètres d’alerte, si les conditions spécifiées sont remplies, Configuration Manager génère une alerte. Vous pouvez consulter les alertes de déploiement de séquence de tâches aux emplacements suivants :  

1.  Consultez les alertes récentes dans le nœud **Systèmes d’exploitation** dans l’espace de travail **Bibliothèque de logiciels** .  

2.  Gérez les alertes configurées dans le nœud **Alertes** dans l'espace de travail **Surveillance** .  

##  <a name="BKMK_TSDeployStatus"></a> État du déploiement de séquence de tâches  
 Après avoir déployé une séquence de tâches, vous pouvez surveiller l’état du déploiement. Pour surveiller l’état de déploiement d’une séquence de tâches, procédez comme suit.  

#### <a name="to-monitor-deployment-status"></a>Pour surveiller l'état d'un déploiement  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail Surveillance, cliquez sur **Déploiements**.  

3.  Cliquez sur la séquence de tâches dont vous souhaitez surveiller l’état du déploiement.  

4.  Dans l'onglet **Accueil** , du groupe **Déploiement** , cliquez sur **Afficher l'état**.  

##  <a name="BKMK_TSReports"></a> Rapports sur le déploiement du système d’exploitation  
 De nombreux rapports de déploiement du système d’exploitation prédéfinis sont disponibles. Ils sont organisés en plusieurs catégories et peuvent être utilisés pour obtenir des informations spécifiques sur les déploiements de séquences de tâches et la migration d’état. En plus d'utiliser les rapports préconfigurés, vous pouvez également créer des rapports de mises à jour logicielles personnalisés selon les besoins de votre entreprise. Pour plus d’informations, consultez [Opérations et maintenance pour les rapports](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_MonitorContent"></a> Surveiller le contenu  
 Vous pouvez surveiller le contenu dans la console Configuration Manager pour déterminer l’état de tous les types de package en rapport avec les points de distribution associés, notamment l'état de validation du contenu du package, l'état du contenu attribué à un groupe de points de distribution spécifique, l'état du contenu attribué à un point de distribution et l'état des fonctions facultatives de chaque point de distribution (validation du contenu, PXE et multidiffusion).  

###  <a name="BKMK_ContentStatus"></a> Surveillance de l’état du contenu  
 Le nœud **État du contenu** dans l'espace de travail **Surveillance** fournit des informations sur les packages de contenu. Vous pouvez consulter les informations générales sur l'emballage, l'état de distribution pour le package et les informations d'état détaillées sur le package. Pour afficher l'état du contenu, procédez comme suit.  

#### <a name="to-monitor-content-status"></a>Pour surveiller l'état du contenu  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail Surveillance, développez **État de distribution**, puis cliquez sur **État du contenu**. Les packages sont affichés.  

3.  Sélectionnez le package pour lequel afficher des informations d'état détaillées.  

4.  Dans l'onglet **Accueil** , cliquez sur **Afficher l'état**. Des informations d'état détaillées pour le package sont affichées.  

###  <a name="BKMK_DPGroupStatus"></a> État du groupe de points de distribution  
 Le nœud **État du groupe de points de distribution** dans l'espace de travail **Surveillance** fournit des informations sur les groupes de points de distribution. Vous pouvez consulter les informations générales sur le groupe de points de distribution, notamment l'état du groupe de points de distribution et le degré de conformité, ainsi que les informations d'état détaillées pour le groupe de points de distribution. Pour afficher l'état du groupe de points de distribution, procédez comme suit.  

#### <a name="to-monitor-distribution-point-group-status"></a>Pour surveiller l'état du groupe de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail Surveillance, développez **État de distribution**, puis cliquez sur **État du groupe de points de distribution**. Les groupes de points de distribution sont affichés.  

3.  Sélectionnez le groupe de points de distribution pour lequel afficher des informations d'état détaillées.  

4.  Dans l'onglet **Accueil** , cliquez sur **Afficher l'état**. Des informations d'état détaillées pour le groupe de points de distribution sont affichées.  

###  <a name="BKMK_DPConfigStatus"></a> État de configuration du point de distribution  
 Le nœud **État de configuration du point de distribution** dans l'espace de travail **Surveillance** fournit des informations sur le point de distribution. Vous pouvez examiner les attributs qui sont activés pour le point de distribution, par exemple, PXE, multidiffusion et validation du contenu. Vous pouvez également afficher des informations d'état détaillées pour le point de distribution. Pour afficher l'état de configuration du point de distribution, procédez comme suit.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Pour surveiller l'état de configuration du point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail Surveillance, développez **État de distribution**, puis cliquez sur **État de configuration du point de distribution**. Les points de distribution sont affichés.  

3.  Sélectionnez le point de distribution pour lequel afficher des informations d'état du point de distribution.  

4.  Dans le volet des résultats, cliquez sur l'onglet **Détails** . Des informations d'état pour le point de distribution sont affichées.  
