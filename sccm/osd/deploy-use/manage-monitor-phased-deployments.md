---
title: Gérer et surveiller les déploiements par phases
titleSuffix: Configuration Manager
description: Découvrez comment gérer et surveiller les déploiements par phases de logiciels dans Configuration Manager.
ms.date: 04/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: dc245916-bc11-4983-9c4d-015f655007c1
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f378fd399a874b0db3844bbf02528dfe92981db5
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500662"
---
# <a name="manage-and-monitor-phased-deployments"></a>Gérer et surveiller les déploiements par phases

Cet article décrit comment gérer et surveiller les déploiements par phases. Les tâches de gestion incluent le démarrage manuel de la phase suivante et l’interruption ou la reprise d’une phase. 

Vous devez tout d’abord créer un déploiement par phases : 
- [Application](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Mise à jour logicielle](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Séquence de tâches](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  



## <a name="bkmk_move"></a> Passer à la phase suivante

Lorsque vous sélectionnez le paramètre **Commencer manuellement la deuxième phase de déploiement**, le site ne démarre pas automatiquement la phase suivante en fonction des critères de réussite définis. Vous devez manuellement lancer la phase suivante du déploiement par phases.  

1. La méthode de lancement de cette action varie en fonction du type de logiciel que vous déployez :  

    - **Application** (uniquement dans la version 1806 ou ultérieure) : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez **Applications**.   

    - **Mise à jour logicielle** (uniquement dans la version 1810 ou ultérieure) : accédez à l’espace de travail **Bibliothèque de logiciels**, puis sélectionnez un des nœuds suivants :    
        - mises à jour logicielles  
            - **Toutes les mises à jour logicielles**  
            - **Groupes de mises à jour logicielles**   
        - Maintenance de Windows 10, **toutes les mises à jour Windows 10**  
        - Gestion des clients Office 365, **mises à jour Office 365**  

    - **Séquence de tâches** : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.   

2. Sélectionnez le logiciel pour le déploiement par phases.  

3. Dans le volet d’informations, accédez à l’onglet **Déploiements par phases**.  

4. Sélectionnez le déploiement par phases, puis cliquez sur **Passer à la phase suivante** dans le ruban.  

    ![Menu contextuel des actions disponibles pour un déploiement par phases](media/Suspend-phased-deployment.PNG)



## <a name="bkmk_suspend"></a> Interrompre et reprendre des phases 

Vous pouvez interrompre ou reprendre manuellement un déploiement par phases. Par exemple, vous venez de créer un déploiement par phases pour une séquence de tâches. Pendant la période de surveillance de la phase dans votre groupe pilote, vous remarquez un grand nombre d’échecs. Vous interrompez le déploiement par phases afin d’arrêter l’exécution de la séquence de tâches sur d’autres appareils. Après avoir résolu le problème, vous reprenez le déploiement par phases pour continuer le processus. 

1. La méthode de lancement de cette action varie en fonction du type de logiciel que vous déployez :  

    - **Application** (uniquement dans la version 1806 ou ultérieure) : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez **Applications**.   

    - **Mise à jour logicielle** (uniquement dans la version 1810 ou ultérieure) : accédez à l’espace de travail **Bibliothèque de logiciels**, puis sélectionnez un des nœuds suivants :    
        - mises à jour logicielles  
            - **Toutes les mises à jour logicielles**  
            - **Groupes de mises à jour logicielles**   
        - Maintenance de Windows 10, **toutes les mises à jour Windows 10**  
        - Gestion des clients Office 365, **mises à jour Office 365**  

    - **Séquence de tâches** : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**. Sélectionnez une séquence de tâches existante, puis cliquez sur **Créer un déploiement par phases** dans le ruban.  

2. Sélectionnez le logiciel pour le déploiement par phases.  

3. Dans le volet d’informations, accédez à l’onglet **Déploiements par phases**.  

4. Sélectionnez le déploiement par phases, puis cliquez sur **Interrompre** ou **Reprendre** dans le ruban.  

<!-- Removed for 1806, need to clarify behavior with engineering
When you suspend a phased deployment, it sets the available and deadline times on the active deployments to a future time. When you resume, it generates a new schedule based on when you resume the phased deployment. The new schedule helps to avoid problems if you resume after the original deadline. For example, the initial schedule has the required deadline seven days after the deployment is available. You suspend it on the second day. If you aren't ready to resume it until day eight, you don't want the deployment to be immediately past the deadline. So it generates a new deadline starting from when you resume the phased deployment on day eight. 
-->


## <a name="bkmk_monitor"></a> Surveiller le déploiement
<!--1358577-->
À compter de la version 1902, les déploiements par phases ont leur propre nœud de monitoring dédié, ce qui facilite leur identification et la navigation dans la vue de monitoring des déploiements par phases. Dans l’espace de travail **Monitoring**, sélectionnez **Déploiements par phases**, puis double-cliquez sur l’un des déploiements par phases pour en connaître l’état. <!--3555949-->

Dans Configuration Manager 1806 et 1810, vous pouvez voir l’expérience de monitoring native des déploiements par phases. Dans le nœud **Déploiements** de l’espace de travail **Monitoring**, sélectionnez un déploiement par phases, puis cliquez sur **État du déploiement par phases** dans le ruban.

![Tableau de bord de l’état du déploiement par phases indiquant l’état de deux phases](media/1358577-phased-deployment-status.png)

Ce tableau de bord montre les informations suivantes pour chaque phase du déploiement :  

- **Nombre total d’appareils** ou **Nombre total de ressources** : nombre d’appareils ciblés par cette phase.  

- **État** : état actuel de cette phase. Chaque phase peut se trouver dans l’un des états suivants :  

    - **Déploiement créé** : le déploiement par phases a créé un déploiement du logiciel sur la collection de cette phase. Les clients sont activement ciblés avec ce logiciel.  

    - **En attente** : la phase précédente n’a pas encore rempli les critères de réussite pour que le déploiement passe à cette phase.  

    - **Suspendu** : un administrateur a suspendu le déploiement.  

- **Progression** : états de déploiement à partir des clients selon un code de couleurs. Par exemple : Réussite, En cours, Erreur, Exigences non remplies et Inconnu. 

#### <a name="success-criteria-tile"></a>Vignette Critères de réussite

Utilisez la liste déroulante **Select Phase** (Sélectionnez la phase) pour changer l’affichage de la vignette **Critères de réussite**. Cette vignette compare la valeur **Objectif de la phase** par rapport à la conformité actuelle du déploiement. Avec les paramètres par défaut, l’objectif de la phase est de 95 %. Cette valeur signifie que le déploiement doit présenter une conformité de 95 % pour passer à la phase suivante.

Dans l’exemple, l’objectif de la phase est de 65 % et la conformité actuelle est de 66,7 %. Comme la première phase répondait aux critères de réussite, le déploiement par phases a automatiquement commencé la deuxième phase.  

   ![Exemple de vignette Critères de réussite dans État du déploiement par phases, avec un objectif de 65 %](media/pod-status-success-criteria-tile.png)

L’objectif de la phase est le même que le **pourcentage de réussite du déploiement** dans la page de paramètres de la phase *suivante*. C’est cette deuxième phase qui définit les critères de réussite de la première phase selon lesquels le déploiement par phases peut démarrer la phase suivante. Pour voir ce paramètre : 

1. Accédez au déploiement par phases du logiciel et affichez ses propriétés.  

2. Accédez à l’onglet **Phases**. Sélectionnez **Phase 2** et cliquez sur **Afficher**.  

3. Dans la fenêtre Propriétés de la phase, accédez à l’onglet **Paramètres de la phase**.  

4. Examinez la valeur **Pourcentage de réussite du déploiement** dans le groupe *Critères de réussite de la phase précédente*.  

Par exemple, les propriétés suivantes concernent la même phase que la vignette Critères de réussite ci-dessus qui affichait un objectif de 65 % :  
![Onglet Paramètres de la phase dans les propriétés de la phase](media/phase-properties-phase-settings.png)

