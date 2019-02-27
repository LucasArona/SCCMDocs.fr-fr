---
title: Surveiller le contenu
titleSuffix: Configuration Manager
description: Apprenez à surveiller le contenu distribué à l’aide de la console Configuration Manager.
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 82e8a693-9adf-4ca3-8484-7e101c34c7c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f6bc81a1aa6d8464094195c33faeecfeaf2d46f0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123928"
---
# <a name="monitor-content-you-have-distributed-with-system-center-configuration-manager"></a>Surveiller le contenu que vous avez distribué avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez la console System Center Configuration Manager pour surveiller le contenu distribué, à savoir :  

-   État de tous les types de package liés aux points de distribution associés.  
-   État de la validation du contenu d’un package.  
-   État du contenu attribué à un groupe de points de distribution spécifique.  
-   État du contenu attribué à un point de distribution.  
-   État des fonctionnalités facultatives pour chaque point de distribution (validation du contenu, PXE et multidiffusion).  

> [!NOTE]  
>  Configuration Manager surveille uniquement le contenu d’un point de distribution situé dans la bibliothèque de contenu. Le contenu stocké sur le point de distribution au sein de packages ou de partages personnalisés n'est pas surveillé.  

##  <a name="BKMK_ContentStatus"></a> Surveillance de l’état du contenu  
 Le nœud **État du contenu** dans l'espace de travail **Surveillance** fournit des informations sur les packages de contenu. Dans la console Configuration Manager, vous pouvez examiner les informations suivantes :  

-   Nom du package.  
-   Type.  
-   Nombre de points de distribution ayant reçu un package.  
-   Niveau de compatibilité.  
-   Date de création du package.  
-   ID du package.  
-   Version source.  

Vous y trouverez également des informations d’état détaillées pour chaque package, ainsi que l’état de distribution du package :  

-   Nombre d’échecs.  
-   Distributions en attente.  
-   Nombre d’installations.

Vous pouvez aussi gérer les distributions qui sont toujours en cours de cheminement vers un point de distribution ou celles qui n’ont pas pu distribuer correctement le contenu à un point de distribution :  

-   L’option pour annuler ou redistribuer du contenu est disponible quand vous affichez le message d’état du déploiement d’une tâche de distribution sur un point de distribution dans le volet **Détails du bien**. Ce volet se trouve sous l’onglet **En cours** ou sous l’onglet **Erreur** du nœud **État du contenu**.  
-   De plus, les détails de la tâche affichent le pourcentage de la tâche qui est terminé quand vous affichez les détails d’une tâche sous l’onglet **En cours**. Les détails du travail affichent également le nombre de nouvelles tentatives restantes pour une tâche, ainsi que la durée restante avant la nouvelle tentative suivante quand vous affichez les détails d’une tâche disponible à partir de l’onglet **Erreur**.  

Quand vous annulez un déploiement qui n’est pas encore terminé, la tâche de distribution pour transférer ce contenu s’arrête :  

-   L’état du déploiement est ensuite mis à jour pour indiquer que la distribution a échoué et a été annulée par une action de l’utilisateur.  
-   Ce nouvel état s'affiche dans l'onglet **Erreur** .  

> [!TIP]  
>  Lorsqu'un déploiement est presque terminé, il est possible que l'action visant à annuler cette distribution ne s'exécute pas avant la fin de la distribution vers le point de distribution. Lorsque cela se produit, l'action visant à annuler le déploiement est ignorée et l'état du déploiement s'affiche comme réussi.  

> [!NOTE]  
>  Bien que vous puissiez sélectionner l'option visant à annuler une distribution vers un point de distribution situé sur un serveur de site, cela n'a aucun effet. Cela est dû au fait que le serveur de site et le point de distribution sur un serveur de site partagent le même magasin de contenu d’instances uniques. Il n’existe aucune tâche réelle de distribution à annuler.  

Quand vous redistribuez du contenu dont le transfert sur un point de distribution a précédemment échoué, Configuration Manager relance immédiatement le redéploiement de ce contenu sur le point de distribution. Configuration Manager met à jour l’état du déploiement pour refléter l’état actuel de ce redéploiement.  

Procédez comme suit pour afficher l’état du contenu et gérer les distributions qui sont toujours en cours ou qui ont échoué.  

### <a name="to-monitor-content-status"></a>Pour surveiller l'état du contenu  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur **État du contenu**. Les packages sont affichés.  

3.  Sélectionnez le package pour lequel vous souhaitez obtenir des informations d'état détaillées.  

4.  Dans l'onglet **Accueil** , cliquez sur **Afficher l'état**. Des informations d'état détaillées pour le package sont affichées.  

### <a name="to-cancel-a-distribution-that-remains-in-progress"></a>Pour annuler une distribution qui est toujours en cours  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur **État du contenu**. Les packages sont affichés.  

3.  Sélectionnez le package que vous souhaitez gérer, puis dans le volet des détails, cliquez sur **Afficher l'état**.  

4.  Dans le volet **Détails du bien** de l’onglet **En cours**, cliquez avec le bouton droit sur l’entrée correspondant à la distribution que vous souhaitez annuler, puis sélectionnez **Annuler**.  

5.  Cliquez sur **Oui** pour confirmer l'action et d'annuler la tâche de distribution pour ce point de distribution.  

### <a name="to-redistribute-content-that-failed-to-distribute"></a>Pour redistribuer le contenu qui n'a pas pu être distribué  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur **État du contenu**. Les packages sont affichés.  

3.  Sélectionnez le package que vous souhaitez gérer, puis dans le volet des détails, cliquez sur **Afficher l'état**.  

4.  Dans le volet **Détails du bien** sous l’onglet **Erreur**, cliquez avec le bouton droit sur l’entrée correspondant à la distribution que vous souhaitez redistribuer, puis sélectionnez **Redistribuer**.  

5.  Cliquez sur **Oui** pour confirmer l’action et démarrer le processus de redistribution sur ce point de distribution.  

## <a name="distribution-point-group-status"></a>État du groupe de points de distribution  
Le nœud **État du groupe de points de distribution** dans l'espace de travail **Surveillance** fournit des informations sur les groupes de points de distribution. Vous pouvez notamment consulter les informations suivantes :  

-   Nom du groupe de points de distribution.  
-   Description.  
-   Nombre de points de distribution appartenant au groupe de points de distribution.  
-   Nombre de packages attribués au groupe.  
-   État du groupe de points de distribution.  
-   Niveau de compatibilité.  

Vous pouvez également consulter les informations d’état détaillées suivantes :  

-   Erreurs liées au groupe de points de distribution.  
-   Nombre de distributions en cours.
-   Nombre de distributions correctement effectuées.  

### <a name="to-monitor-distribution-point-group-status"></a>Pour surveiller l'état du groupe de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur **État du groupe de points de distribution**. Les groupes de points de distribution sont affichés.  

3.  Sélectionnez le groupe de points de distribution pour lequel vous souhaitez obtenir des informations d'état détaillées.  

4.  Dans l'onglet **Accueil** , cliquez sur **Afficher l'état**. Des informations d'état détaillées pour le groupe de points de distribution sont affichées.  

## <a name="distribution-point-configuration-status"></a>État de configuration du point de distribution  
 Le nœud **État de configuration du point de distribution** dans l'espace de travail **Surveillance** fournit des informations sur le point de distribution. Vous pouvez vérifier quels attributs sont activés pour le point de distribution, notamment le PXE, la multidiffusion, la validation du contenu et l’état de distribution pour le point de distribution. Vous pouvez également afficher des informations d'état détaillées pour le point de distribution.  

> [!WARNING]  
>  L'état de la configuration du point de distribution concerne les dernières 24 heures. Si le point de distribution présente une erreur et que celle-ci est résolue, l'état d'erreur peut s'afficher jusqu'à 24 heures après la restauration du point de distribution.  

Pour afficher l'état de configuration du point de distribution, procédez comme suit.  

### <a name="to-monitor-distribution-point-configuration-status"></a>Pour surveiller l'état de configuration du point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur **État de la configuration du point de distribution**. Les points de distribution sont affichés.  

3.  Sélectionnez le point de distribution pour lequel vous souhaitez obtenir des informations d'état du point de distribution.  

4.  Dans le volet des résultats, cliquez sur l'onglet **Détails** . Des informations d'état pour le point de distribution sont affichées.  

## <a name="client-data-sources-dashboard"></a>Tableau de bord Sources de données du client
À compter de la version 1610, vous pouvez utiliser le tableau de bord **Sources de données du client** pour comprendre l’utilisation du [Cache d’homologue](/sccm/core/plan-design/hierarchy/client-peer-cache) dans votre environnement. Le tableau de bord commencera à afficher des données une fois que les clients auront téléchargé du contenu, et signalera ces informations au site. Cette opération peut prendre jusqu’à 24 heures.

> [!TIP]  
> Le **Cache d’homologue client** et le tableau de bord **Sources de données de clients** sont des [fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features) présentées dans la version 1610. À compter de la version 1710, ces fonctionnalités ne sont plus des fonctionnalités en préversion. Vous devez activer le cache d’homologue client pour que le tableau de bord Sources de données de clients devienne visible dans la console.


Dans la console, accédez à **Surveillance** > **État de distribution** > **Sources de données du client**. Vous pouvez sélectionner ici une période à appliquer au tableau de bord. Ensuite, dans l’affichage, vous pouvez sélectionner le groupe de limites ou le package sur lesquels vous souhaitez afficher des informations. Lors de la consultation de celles-ci, vous pouvez pointer le curseur de la souris sur la surface pour afficher plus de détails sur les différentes sources de contenu ou de stratégie.

Ces détails incluent :  
- **Sources de contenu client** : Affiche la source à partir de laquelle les clients ont obtenu du contenu.
- **Points de distribution** : Affiche le nombre de points de distribution qui font partie du groupe de limites sélectionné.
- **Clients ayant utilisé un point de distribution** : Affiche le nombre de clients membres du groupe de limites sélectionné qui ont utilisé un point de distribution pour obtenir du contenu.
- **Sources de cache de pair** : Affiche, pour le groupe de limites sélectionné, le nombre de sources de cache de pair ayant fourni un historique de téléchargement.
- **Clients ayant utilisé un pair** : Affiche le nombre de clients membres du groupe de limites sélectionné qui ont utilisé une source de cache de pair pour obtenir du contenu.



Vous pouvez également utiliser un nouveau rapport, **Sources de données du client - Résumé**, pour afficher une synthèse des sources de données du client pour chaque groupe de limites.
