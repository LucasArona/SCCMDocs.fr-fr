---
title: Le déploiement pilote
titleSuffix: Configuration Manager
description: Guide pratique pour le déploiement sur un groupe pilote Analytique de bureau.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e18e2e43e9bb768f81233fb2d2deda0ae05c1961
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145834"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Le déploiement pilote avec Analytique de bureau

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Un des avantages du Desktop Analytique est pour aider à identifier le plus petit ensemble d’appareils qui fournissent la plus large couverture de facteurs. Il se concentre sur les facteurs les plus importants pour un pilote de mises à niveau de Windows et les mises à jour. S’assurer que le pilote ne réussit plus vous permet de déplacer plus rapidement et en toute confiance aux grands déploiements en production.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>Identifier les appareils

La première étape consiste à identifier les périphériques à inclure dans le pilote. Postes de travail Analytique recommande les périphériques basés sur les données transmises et vous pouvez inclure ou remplacez des appareils dans cette liste.

1. Accédez à la [portail d’Analytique de Desktop](https://aka.ms/desktopanalytics)et dans le groupe, sélectionnez gérer **plans de déploiement**.

1. Sélectionnez un plan de déploiement.

1. Dans le groupe préparation du menu du plan de déploiement, sélectionnez **identifier pilote**.

Vous verrez les données d’Analytique de bureau qui affiche le nombre d’appareils qu’il recommande notamment pour la meilleure couverture. Cet algorithme est principalement basé sur l’utilisation des applications importantes et critiques et l’éventail des configurations matérielles.

Prenez les mesures suivantes pour obtenir la liste des appareils supplémentaires recommandée :

- **Ajouter tout au pilote**: Ajoute tous les appareils recommandées dans le groupe pilote
- **Ajouter au projet pilote**: Ajouter uniquement des appareils individuels
- **Remplacez** tous les appareils à partir de l’implémentation pilote spécifiques
- **Recalculer** lorsque vous avez terminé d’apporter des modifications

Vous pouvez également rendre les décisions de l’échelle du système sur les regroupements de Configuration Manager pour inclure ou exclure les pilotes. Dans le menu principal d’Analytique de bureau, dans le groupe de paramètres globaux, sélectionnez **pilote Global**.

### <a name="example"></a>Exemple

- Vous configurez la connexion de bureau Analytique dans Configuration Manager à cibler le **tous les systèmes** collection. Cette action inscrit tous les clients du service.
- Vous configurez également des collections supplémentaires pour la synchronisation avec Bureau Analytique :
    - Tous les clients Windows 10
    - Tous les appareils de l’informatique
    - PDG office
- Dans le **pilote Global** paramètres, vous incluez le **tous les équipements** collections. Vous excluez le **PDG office** collection.
- Vous créez un plan de déploiement, puis sélectionnez le **tout Windows 10 clients** collection.
- Votre **piloter les appareils inclus** liste contient les ensembles d’appareils suivants :
    - Tous les appareils dans votre liste d’inclusion de pilote global : **Tous les appareils de l’informatique**
    - Collections qui font également partie du groupe cible de plan de déploiement : **Tous les clients Windows 10**
- Exclut les postes de travail Analytique à partir de la **supplémentaires recommandés appareils** répertorier tous les périphériques de votre pilote global *exclusion* liste : **PDG office**
- Uniquement les deux premiers regroupements sont considérés comme faisant partie de l’implémentation pilote. Une fois que les mises à niveau réussites à ces groupes et les ressources sont *prêt*, Analytique de bureau synchronise les appareils dans le **PDG office** collection à la collection de production Configuration Manager.


## <a name="address-issues"></a>Résoudre les problèmes

Utilisez le portail d’Analytique de bureau pour passer en revue les problèmes signalés avec les ressources susceptibles de bloquer votre déploiement. Puis l’approuver, rejeter ou modifier la correction suggérée. Tous les éléments doivent être marqués **prêt** ou **prêt (avec mise à jour)** avant le déploiement pilote.

1. Accédez à la [portail d’Analytique de Desktop](https://aka.ms/desktopanalytics)et dans le groupe, sélectionnez gérer **plans de déploiement**.  

2. Sélectionnez un plan de déploiement.  

3. Dans le groupe préparation du menu du plan de déploiement, sélectionnez **préparation pilote**.  

4. Sur le **applications** onglet, passez en revue les applications nécessitant votre entrée.  

5. Pour chaque application, sélectionnez le nom de l’application. Dans le volet d’informations, passez en revue la recommandation, puis sélectionnez la décision de mise à niveau. Si vous choisissez **ne pas été revues** ou **impossible**, puis Bureau Analytique n’inclut pas les appareils avec cette application dans le déploiement pilote. Si vous choisissez **prêt (avec mise à jour)** , utilisez le **notes de mise à jour** pour capturer les actions à suivre pour résoudre un problème, comme *réinstaller* ou *trouver le version recommandée du fabricant*.

6. Répétez cette revue pour d’autres ressources.  


## <a name="create-software"></a>Créer des logiciels

Avant de déployer Windows, tout d’abord créer les objets de logiciel dans Configuration Manager. Pour plus d’informations, consultez [séquence de tâches de mise à niveau sur place de Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).


## <a name="deploy-to-pilot-devices"></a>Déployer sur des appareils de pilotes

Configuration Manager utilise les données d’Analytique de bureau pour créer des regroupements pour les déploiements de pilote et de production. Pour vous assurer que les appareils sont sains après chaque phase de déploiement, procédez comme suit pour créer un déploiement échelonné Analytique de bureau intégré :

1. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels**, développez **Desktop Analytique maintenance**, puis sélectionnez le **Plans de déploiement** nœud.  

2. Sélectionnez votre plan de déploiement, puis **détails du Plan de déploiement** dans le ruban.  

3. Sélectionnez **créer un déploiement par phases** dans le ruban. Cette action lance l’Assistant Création d’un déploiement par phases.

    > [!Tip]  
    > Si vous souhaitez créer un déploiement de séquence de tâches classiques pour simplement la collection pilote, sélectionnez **déployer** dans le **piloter état** vignette. Cette action lance l’Assistant déploiement logiciel. Pour plus d'informations, voir [Déployer une séquence de tâches](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Entrez un nom pour le déploiement, puis sélectionnez la séquence de tâches à utiliser. Utilisez l’option à **créer automatiquement un déploiement en deux phases par défaut**, puis configurez les collections suivantes :  

    - **Première Collection**: Recherchez et sélectionnez le **pilote** collection pour ce plan de déploiement. La convention d’affectation de noms standard pour cette collection est `<deployment plan name> (Pilot)`.

    - **Deuxième Collection**: Recherchez et sélectionnez le **Production** collection pour ce plan de déploiement. La convention d’affectation de noms standard pour cette collection est `<deployment plan name> (Production)`.

    > [!Note]  
    > Avec l’intégration Analytique de bureau, Configuration Manager crée automatiquement des collections de pilote et de production pour le plan de déploiement. Il peut prendre jusqu'à 10 minutes pour ces collections à synchroniser avant de pouvoir les utiliser.<!-- 3887891 -->
    >
    > Ces collections sont réservées pour les appareils de plan de déploiement de bureau Analytique. Les modifications manuelles apportées à ces collections ne sont pas pris en charge.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Terminez l’Assistant pour configurer le déploiement par phases. Pour plus d’informations, voir [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

    > [!Note]  
    > Utilisez le paramètre par défaut à **commencer automatiquement cette phase après une période de report (en jours)** . Les critères suivants doivent être remplies pour la deuxième phase démarrer :
    >
    > 1. Appareils de pilote doivent mettre à niveau et envoyer back révisée des données de diagnostic.
    > 1. La première phase atteint le **pourcentage de réussite du déploiement** critères de réussite. Vous configurez ce paramètre sur le déploiement par phases.
    > 1. Vous devez passer en revue et prendre des décisions de mise à niveau dans Analytique de bureau pour marquer des ressources importantes et critiques comme *prêt*. Pour plus d’informations, consultez [passez en revue les ressources dont ont besoin d’une décision de mise à niveau](/sccm/desktop-analytics/deploy-prod#bkmk_review).
    > 1. Synchronise les postes de travail Analytique aux regroupements Configuration Manager tous les appareils de production qui répondent à la *prêt* critères.
    >
    > Lorsque le Gestionnaire de Configuration par phases déploiement déplace automatiquement à la phase suivante, elle s’applique uniquement aux appareils qui synchronise les Analytique de bureau dans la collection de production.

> [!Important]  
> Ces collections continuent à synchroniser en tant que leurs changements d’appartenance. Par exemple, si vous identifiez un problème avec un élément multimédia et marquez comme **impossible**, les appareils avec cette ressource ne répondent pas à la *prêt* critères. Ces appareils sont supprimés de la collection de déploiement de production.


## <a name="monitor"></a>Moniteur

### <a name="configuration-manager-console"></a>Console Configuration Manager

Ouvrez le plan de déploiement. Le **décisions de mise à niveau de préparation - état global** vignette fournit un résumé de l’état pour le plan de déploiement. Cet état est associé aux collections de votre pilote et de production. Les appareils peuvent être classées dans une des catégories suivantes :

- **Mise à jour**: Les périphériques ont mis à niveau vers la version de Windows cible pour ce plan de déploiement

- **Mise à niveau complète de la décision**: Un des états suivants :
    - Appareils avec des ressources dignes d’intérêt sont **prêt** ou **prêt avec mise à jour**
    - L’état de l’appareil est **bloqué**, **appareil de remplacement** ou **Reinstall appareil**

- **Ne pas été revues**: Appareils avec des ressources dignes d’intérêt **ne pas été revues** ou **révision en cours**

Mises à jour de l’état du périphérique dans le **piloter état** et **état de la Production** vignettes avec les actions suivantes :

- Vous apportez des modifications sur l’évaluation de compatibilité
- Appareils mis à niveau vers la version cible de Windows
- Progression de votre déploiement

Vous pouvez également utiliser le même que d’autres déploiements de séquence de tâches de surveillance de déploiement de Configuration Manager. Pour plus d’informations, consultez [des déploiements de système d’exploitation de l’analyse](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portail d’Analytique bureau

Utilisez le [portail d’Analytique de bureau](https://aka.ms/desktopanalytics) pour afficher l’état d’un plan de déploiement. Sélectionnez le plan de déploiement, puis **vue d’ensemble du Plan**.

![Capture d’écran de vue d’ensemble du plan de déploiement dans l’Analytique de bureau](media/deployment-plan-overview.png)

Sélectionnez le **pilote** vignette. Il récapitule l’état actuel du déploiement pilote. Cette vignette affiche également les données pour le nombre d’appareils n’a ne pas démarrés, en cours, terminé, ou le renvoi des problèmes.

Tous les appareils reporting d’erreurs ou autres problèmes sont également répertoriés dans la zone de détails de pilote à droite. Pour obtenir les détails du problème signalé, sélectionnez **révision**. Cette action modifie la vue pour la **état du déploiement** page

Le **état du déploiement** page répertorie les appareils dans les catégories suivantes :

- Non démarré
- En cours
- Terminé
- Nécessite une attention - appareils
- Nécessite une attention - problèmes

Le **nécessite une attention** catégories affichent les mêmes informations, mais triées différemment.

Sélectionnez une liste spécifique dans une vue pour obtenir plus d’informations sur le problème détecté.

Que vous résolvez ces problèmes de déploiement, le tableau de bord continue à afficher la progression des appareils. Il met à jour comme appareils déplacement à partir de **nécessite une attention** à **terminé**.


## <a name="next-steps"></a>Étapes suivantes

Permettent l’exécution du pilote pendant un certain temps collecter des données opérationnelles. Encouragez les utilisateurs d’appareils de pilotes pour tester vos applications.

Lorsque votre déploiement pilote répond à vos critères de réussite, accédez à l’article suivant pour déployer en production.
> [!div class="nextstepaction"]  
> [Déployer en production](/sccm/desktop-analytics/deploy-prod)  
