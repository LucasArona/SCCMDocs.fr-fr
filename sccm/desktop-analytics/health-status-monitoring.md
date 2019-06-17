---
title: Analyse du fonctionnement
titleSuffix: Configuration Manager
description: En savoir plus sur le fonctionne de surveillance de l’état d’intégrité dans Analytique de bureau.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a95d1cca34dec9a17487e10d980f7e458186106
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145785"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Analyse dans Analytique de bureau de l’état d’intégrité

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Comme vous [déployer une mise à jour en production](/sccm/desktop-analytics/deploy-prod), utilisez Desktop Analytique pour aider à surveiller l’état d’intégrité de vos appareils. Cet article explique en détail comment fonctionne la surveillance de l’intégrité.

Pour plus d’informations sur la façon d’utiliser cette fonctionnalité, consultez [surveiller l’intégrité des appareils mis à jour](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Capture d’écran de la page surveiller l’intégrité de l’Analytique de bureau](media/monitor-health.png)

> [!NOTE]  
> Postes de travail Analytique collecte uniquement les données de contrôle d’intégrité à partir d’appareils qui fournissent des données d’utilisation qu'il peut utiliser comme dénominateur. Cela signifie qu’il n’inclut pas les appareils exécutant Windows 7 et Windows 10 qui ne sont pas définies pour partager des données de diagnostic au niveau avancé (limité). Si plus de 10 % des appareils exécutant Windows 10 sont définies pour partager des données de diagnostic à d’autres niveaux qu’avancé (limité), le **surveiller l’intégrité** page affiche un avertissement dans la bannière.  

Pour afficher plus d’informations sur une application spécifique, sélectionnez-le dans la liste.



## <a name="apps"></a>Applications

![Facteurs d’état d’intégrité pour une application de bureau Analytique](media/monitor-health-status-factors.png)

Analytique de postes de travail analyse des facteurs suivants de l’état d’intégrité pour les applications :

- **Pourcentage d’appareils avec blocages**: Pour les deux dernières semaines, le nombre d’appareils sur lesquels cette application particulière s’est arrêté anormalement divisé par le nombre d’appareils sur lesquels l’application a été utilisée. Cette vue vous permet de voir si la stabilité de l’application a augmenté ou diminué sur la nouvelle version du système d’exploitation. Postes de travail Analytique calcule ce pourcentage pour les ensembles suivants :  

    - **Après mise à jour**: Appareils qui ont mis à jour vers la version de système d’exploitation cible spécifiée dans le plan de déploiement. Pour réduire le nombre de ressources avec des données insuffisantes, bureau Analytique collecte ces données pour tous vos appareils mis à jour. Cet ensemble inclut ces appareils pas dans le plan de déploiement.  

    - **Avant la mise à jour**: Appareils qui se trouvent sur une version du système d’exploitation antérieurs à ce qui est spécifié dans le plan de déploiement. Cette liste n’inclut pas les appareils exécutant Windows 7.  

    - **Moyenne commerciale**: La moyenne (avg) se bloquer taux sur tous les appareils commerciaux. Cette moyenne est calculée sur *tous les* versions de l’application. Si votre version affiche un taux de blocage supérieur à la moyenne commerciale, une version plus stable peuvent être disponibles.  

- **% Sessions avec des blocages**: Similaire au précédent, mais les nombres le pourcentage de sessions avec tombe en panne dans les deux dernières semaines.  

Pour déterminer l’état d’intégrité d’une application, bureau Analytique nécessite des données de moins de 20 périphériques. Sinon, elle indique **pas suffisamment de données** pour l’application. Le service calcule l’état d’intégrité selon les *taux de blocage de session* à partir de ces appareils. Le taux de panne de périphérique est fourni pour information uniquement. Il n’est pas utilisé dans le calcul d’état d’intégrité.

En bas de la page de détails de l’application, les trois onglets suivants peuvent vous aider à résoudre les problèmes :

- **Autres versions**: Liste des autres versions de cette application. Pour chaque version, il montre les modifications relatives aux taux de blocage au sein de votre organisation et la moyenne commerciale. Si vous trouvez une version ultérieure de l’application ayant une vitesse inférieure de la panne, la mise à jour de l’application peut aider.  

    Il indique également si la version a un **prêt pour Windows** signal. Pour plus d’informations, consultez [évaluation de la compatibilité](/sccm/desktop-analytics/compat-assessment#risk-assessment-engine).  

- **Principaux problèmes**: Une liste de l’ID d’échec plus fréquente par nombre d’instances. Un ID de l’erreur identifie la trace de pile associée à l’incident. Vous pouvez utiliser cet ID lorsque vous appelez l’éditeur de l’application pour la prise en charge.  

- **Les incidents récents**:  Une liste des périphériques sur lesquels l’application récemment est tombé en panne. Vous pouvez filtrer par ID de l’erreur et d’autres critères. Utilisez ces informations pour résoudre le problème par la collecte des journaux ou une tentative de correctifs sur des appareils spécifiques avant d’essayer un déploiement plus large.  

Si vous trouvez une régression de santé sérieux que vous ne parvenez pas à résoudre, modifiez l’application **mise à niveau de la décision** à **impossible**. Cette action empêche le déploiement futur de la mise à jour sur des appareils avec cette ressource.


## <a name="see-also"></a>Voir aussi

- [Évaluation de la compatibilité dans Desktop Analytique](/sccm/desktop-analytics/compat-assessment)  

- [Comment déployer en production avec Analytique de bureau](/sccm/desktop-analytics/deploy-prod)  
