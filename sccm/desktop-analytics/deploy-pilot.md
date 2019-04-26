---
title: Le déploiement pilote
titleSuffix: Configuration Manager
description: Guide pratique pour le déploiement sur un groupe pilote Analytique de bureau.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4aa078f5a8306cb30ea83d45b93b18971be7764f
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62234282"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Le déploiement pilote avec Analytique de bureau

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Un des avantages du Desktop Analytique est pour aider à identifier le plus petit ensemble d’appareils qui fournissent la plus large couverture de facteurs. Il se concentre sur les facteurs les plus importants pour un pilote de mises à jour et mises à jour Windows et Office. S’assurer que le pilote ne réussit plus vous permet de déplacer plus rapidement et en toute confiance aux grands déploiements en production.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## <a name="address-issues"></a>Résoudre les problèmes

Utilisez le portail d’Analytique de bureau pour passer en revue les problèmes signalés avec les ressources susceptibles de bloquer votre déploiement. Puis l’approuver, rejeter ou modifier la correction suggérée. Tous les éléments doivent être marqués **prêt** ou **prêt (avec mise à jour)** avant le déploiement pilote.

1. Accédez au portail d’Analytique de bureau, puis sélectionnez **plans de déploiement** dans le groupe de gestion.  

2. Ouvrez un plan de déploiement en sélectionnant son nom.  

3. Sélectionnez **préparation pilote** dans le groupe de préparation du menu du plan de déploiement.  

4. Sur le **applications** onglet, passez en revue les applications nécessitant votre entrée.  

5. Pour chaque application, sélectionnez le nom de l’application. Dans le volet d’informations, passez en revue la recommandation, puis sélectionnez la décision de mise à niveau. Si vous choisissez **ne pas été revues** ou **impossible**, puis Bureau Analytique n’inclut pas les appareils avec cette application dans le déploiement pilote. Si vous choisissez **prêt (avec mise à jour)**, utilisez le **notes de mise à jour** pour capturer les actions à suivre pour résoudre un problème, comme *réinstaller* ou *trouver le version recommandée du fabricant*.

6. Répétez cette revue pour d’autres ressources.  



## <a name="create-software"></a>Créer des logiciels

Avant de déployer Windows ou Office, tout d’abord créer les objets de logiciel dans Configuration Manager.

- [Application ProPlus Office 365](https://docs.microsoft.com/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)  

- [Séquence de tâches de mise à niveau sur place de Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)



## <a name="deploy-to-pilot-devices"></a>Déployer sur des appareils de pilotes

Configuration Manager utilise les données d’Analytique de bureau pour créer un regroupement pour le déploiement pilote. Ne déployez pas la séquence de l’application ou une tâche à l’aide d’un déploiement classique. Utilisez la procédure suivante pour créer un déploiement intégré de bureau Analytique :

1. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels**, développez **Desktop Analytique maintenance**, puis sélectionnez le **Plans de déploiement** nœud.  

2. Sélectionnez votre plan de déploiement, puis **détails du Plan de déploiement** dans le ruban.  

3. Dans le **piloter état** vignette, sélectionnez un des types d’objets suivants dans la liste déroulante :  

    - **Application** pour Office 365 ProPlus  

    - **Séquence de tâches** pour Windows 10  
  
   Sélectionnez **déployer**. Cette action lance l’Assistant Déploiement de logiciel pour le type d’objet sélectionné.

    > [!Note]  
    > Avec l’intégration Analytique de bureau, Configuration Manager crée automatiquement une collection pour le plan de déploiement pilote. Il peut prendre jusqu'à 10 minutes pour cette collection à synchroniser que vous puissiez l’utiliser.<!-- 3887891 -->
    >
    > Cette collection est réservée aux appareils de plan de déploiement de bureau Analytique. Les modifications manuelles à cette collection ne sont pas pris en charge.<!-- 3866460, SCCMDocs-pr 3544 -->  

Pour plus d’informations, consultez les articles suivants :  

- [Déployer une application](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy)  

- [Déployer une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)  

Si votre plan de déploiement est pour Windows 10 et Office 365, répétez ce processus pour créer un deuxième déploiement. Par exemple, si le premier déploiement concerne la séquence de tâches, créez un deuxième déploiement pour l’application.



## <a name="monitor"></a>Moniteur

### <a name="configuration-manager-console"></a>Console Configuration Manager

Déploiement d’utiliser le Gestionnaire de Configuration analyse le même déploiement de séquences comme toute autre application et de la tâche. Pour plus d’informations, consultez les articles suivants :  

- [Analyser l’application à partir de la console Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

- [Superviser les déploiements de système d’exploitation](/sccm/osd/deploy-use/monitor-operating-system-deployments)  


### <a name="desktop-analytics-portal"></a>Portail d’Analytique bureau

Utilisez le portail d’Analytique de bureau pour afficher l’état d’un plan de déploiement. Sélectionnez le plan de déploiement, puis **vue d’ensemble du Plan**.

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

Permettent l’exécution du pilote pour une période de temps pour collecter des données opérationnelles. Encouragez les utilisateurs d’appareils de pilotes pour tester des applications, des compléments et macros.

Lorsque votre déploiement pilote répond à vos critères de réussite, accédez à l’article suivant pour déployer en production.
> [!div class="nextstepaction"]  
> [Déployer en production](/sccm/desktop-analytics/deploy-prod)  
