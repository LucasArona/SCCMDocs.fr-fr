---
title: Comment déployer en production
titleSuffix: Configuration Manager
description: Guide pratique pour le déploiement sur un groupe de production d’Analytique de bureau.
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
ms.openlocfilehash: e93b08766da4abc37ca3663de5fe2919f1953833
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67146060"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Comment déployer en production avec Analytique de bureau

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Une fois que vous avez [déployées au pilote](/sccm/desktop-analytics/deploy-pilot) et examiner l’état de vos ressources, vous êtes prêt à mettre à jour le reste de votre environnement de production.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Il existe trois parties principales pour accomplir le déploiement des mises à jour pour les appareils de production :

1. [Passez en revue les ressources dont ont besoin d’une décision de mise à niveau](#bkmk_review): Pour apporter des appareils prêt pour le déploiement de production, leurs ressources doivent avoir leur décision de mise à niveau la valeur **prêt** ou **prêt, les corrections nécessaires**.  

2. [Déployer sur des appareils qui sont prêts](#bkmk_deploy): Utilisez le Gestionnaire de Configuration pour mettre à jour les appareils qui sont prêts. Postes de travail Analytique fournit la liste des appareils prêts pour le déploiement de production et des rapports pour surveiller la réussite du déploiement.  

3. [Surveiller l’intégrité des appareils mis à jour](#bkmk_monitor): Comme la progresse de déploiement de mise à jour, surveiller l’intégrité des ressources importantes. Si certaines nécessitent une attention, dépanner et résoudre ces problèmes. Si vous décidez que les problèmes ne peuvent pas être résolus, d’arrêter le déploiement sur le dispositif concerné en définissant leur décision de mise à niveau sur **impossible**.  

> [!NOTE]  
> Lorsque vous êtes ainsi certain de la réussite du déploiement pilote, lancez le déploiement de production à tout moment. N’est pas obligatoire que tous les appareils de pilotes atteint tout d’abord l’état « terminé ».  



## <a name="bkmk_review"></a> Passez en revue les ressources dont ont besoin d’une décision de mise à niveau

Analytique bureau vous guide tout au long du processus de révision de vos ressources pour le déploiement de production. Dans le portail Azure, accédez à **plans de déploiement**, sélectionnez un plan de déploiement, puis **préparer production** dans le menu de gauche.

![Vue de capture d’écran de la préparation de Production dans Desktop Analytique](media/prepare-production.png)

Passez en revue l’état de vos applications. Utilisez ces informations pour définir la décision de mise à niveau pour chacune de ces ressources.

Utilisez les onglets pour consulter l’état des applications. Dans chaque vue à onglets, vous pouvez filtrer les résultats pour afficher les périphériques qui sont sur la bonne voie pour la mise à niveau, besoin votre attention, les appareils avec des résultats mixtes et ces appareils dans un état indéterminé.

Sélectionnez **réunion objectifs** pour filtrer la vue à des ressources qui sont probablement prêt pour le déploiement de production en fonction des critères suivants :

- : Une pré-mise à niveau évaluation des risques de risques connus pour la mise à jour des appareils sur lesquels cette ressource installée  

- État d’intégrité : une évaluation après mise à niveau des appareils dans les autres déploiements et si elles ont rencontré des problèmes après la mise à jour a été installé. Pour plus d’informations sur l’intégrité, consultez [surveiller l’intégrité des appareils mis à jour](#bkmk_monitor).  

Pour approuver un élément multimédia pour la mise à niveau, sélectionnez le nom dans la liste, puis sélectionnez une des options suivantes à partir de la **mise à niveau de la décision** liste :

- Passez en revue en cours
- Vous êtes prêt
- Prêt (avec mise à jour)
- Impossible de
- Non révisé

Pour définir cette valeur pour plusieurs applications à la fois, utilisez la première colonne à **Sélectionnez cet élément**, puis choisissez **définir la décision de mettre à niveau**.

![Définir l’option de mise à niveau de la décision sur plusieurs applications](media/prep-prod-set-upgrade-decision.png)

Sélectionnez **aucune donnée** pour afficher les actifs qui n’a pas pu être classifiés. En règle générale, ces ressources sont les ressources qui n’ont pas suffisamment de couverture pour l’Analytique de bureau effectuer une analyse de l’état d’intégrité ou de risque. Pour améliorer la couverture, ajouter d’autres appareils avec ces ressources au pilote, ou demandez à des utilisateurs pilotes pour essayer ces ressources.

Il peut également y avoir des ressources dans le **Attention nécessitée** ou **résultats mixte** état. Ces ressources peuvent nécessiter une vérification supplémentaire avant de vous prendre une décision de mise à niveau pour eux.

Passez en revue toutes les applications. Une fois qu’un appareil donné a une décision de mise à niveau positive pour tous les éléments multimédias, son état passe ensuite à « prêt pour la production. » Afficher le nombre actuel sur la page principale pour le plan de déploiement en sélectionnant la troisième étape de déploiement, **déployer**.


## <a name="bkmk_deploy"></a> Déployer sur des appareils qui sont prêts

Configuration Manager utilise les données d’Analytique de bureau pour créer un regroupement pour le déploiement de production. Ne déployez pas la séquence de tâches à l’aide d’un déploiement classique. Utilisez la procédure suivante pour créer un déploiement intégré de bureau Analytique :

Si vous avez suivi le processus recommandé pour [déployer sur des appareils pilotes](/sccm/desktop-analytics/deploy-pilot#deploy-to-pilot-devices), le déploiement par phases de Configuration Manager est prêt. Lorsque vous marquez des actifs *prêt*, Analytique de bureau synchronise automatiquement ces appareils à Configuration Manager. Ces appareils sont ensuite ajoutés à la collection de production. Lorsque le déploiement par phases se déplace à la deuxième phase, ces appareils de production reçoivent le déploiement de mise à niveau.

Si vous avez configuré le déploiement par phases pour **commencer manuellement le deuxième déploiement phase**, vous devez déplacer manuellement vers la phase suivante. Pour plus d’informations, consultez [Gérer et effectuer le monitoring des déploiements par phases](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).

Si vous avez créé un déploiement unique intégrée au bureau Analytique à la collection pilote, vous devez répéter ce processus à déployer sur le regroupement de production.


### <a name="address-deployment-alerts"></a>Résoudre les alertes de déploiement

Comme avec le déploiement pilote, Analytique de bureau vous conseille de tout problème nécessitant votre attention lors du déploiement de production. Dans l’Analytique de bureau, accédez au plan de déploiement, puis sélectionnez **état du déploiement** dans le menu de gauche. L’affichage d’état de déploiement répertorie les appareils dans les catégories suivantes :  

- Non démarré
- En cours
- Terminé
- A besoin d’attention - appareils (triées par nom de l’appareil)
- Nécessite une attention - problèmes (triés par type de problème)

![Statut de déploiement de production de capture d’écran de bureau Analytique](media/prod-deployment-status.png)


## <a name="bkmk_monitor"></a> Surveiller l’intégrité des appareils mis à jour

Le **préparer production** page se concentre sur les aidant à procéder à des décisions pour vos ressources de mise à niveau. Cette page par défaut montre uniquement les éléments qui ne sont pas encore dans le **prêt** état. Le **surveiller l’intégrité** page affiche les problèmes d’intégrité sur les actifs dignes d’intérêt, même les ressources qui sont marqués **prêt**. Si elle détecte des problèmes, vous pouvez résoudre les problèmes et résoudre le problème ou modifier la décision de mise à niveau **impossible**. Lorsque vous modifiez la décision de mise à niveau, cette action empêche de futures mises à niveau sur les appareils avec cette ressource.

Filtrer cette page par des actifs avec les États d’intégrité suivantes :

| Filtre d’état d’intégrité | Description |
|----------------------|-------------|
| **Faites attention** | (Filtre par défaut) Postes de travail Analytique détecte une régression statistiquement significative pour une mesure d’intégrité pour cette ressource
| **Objectifs de la réunion** | Postes de travail Analytique ne détecte aucune régression de comportement |
| **Données insuffisantes** | Analytique de postes de travail n’a pas suffisamment de données sur cette ressource à faire des recommandations |
| **Aucune donnée** | Aucune donnée d’utilisation encore disponible pour cette ressource |

Pour afficher une vue non filtrée de toutes les ressources, sélectionnez le filtre actif. Cette action supprime ce filtre.

> [!NOTE]  
> Pour réduire le nombre de ressources avec des données insuffisantes, bureau Analytique surveille les ressources sur tous les appareils qui ont mis à niveau vers la version de Windows cible spécifiée dans votre plan de déploiement. Ces périphériques incluent ceux ne pas inclus dans le plan de déploiement spécifique.  

Le critère de tri par défaut est le nombre d’appareils qui ont connu un incident avec cette ressource particulière, afin que vous puissiez voir rapidement celles qui est à l’origine de la plupart des problèmes. Par exemple, lors de l’affichage **applications**, il trie par **périphériques avec application tombe en panne deux dernières semaines**.

Si vous souhaitez examiner l’intégrité pour tous les éléments multimédias, même les ressources avec des données insuffisantes pour l’Analytique de bureau faire des inférences statistiques, procédez comme suit :

1. Sélectionnez la liste déroulante sur le **périphériques des incidents dans les deux dernières semaines** colonne. Ajouter un filtre pour que les composants qui ont connu des incidents sur un certain nombre minimal d’appareils pour être intéressant. Par exemple, afficher les éléments avec des valeurs **supérieur** 100.  

2. Sélectionnez la liste déroulante sur le **% des appareils des incidents dans les deux dernières semaines** colonne et sélectionnez cette option pour trier par **décroissant**.  

    La vue résultante montre les ressources avec le plus élevé d’incident à un nombre minimal d’incidents.  

3. Sélectionnez un élément multimédia pour obtenir plus de détails ou de modifier sa décision de mise à niveau.  

Pour plus d’informations, consultez [surveillance de l’état d’intégrité](/sccm/desktop-analytics/health-status-monitoring).
