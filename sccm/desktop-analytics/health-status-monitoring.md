---
title: Analyse du fonctionnement
titleSuffix: Configuration Manager
description: En savoir plus sur le fonctionne de surveillance de l’état d’intégrité dans Analytique de bureau.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 834b7d30aa5331ae73125e1cdfc3c9c7095d58b7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754963"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Analyse dans Analytique de bureau de l’état d’intégrité

Comme vous [déployer une mise à jour en production](/sccm/desktop-analytics/deploy-prod), utilisez Desktop Analytique pour aider à surveiller l’état d’intégrité de vos appareils. Cet article explique en détail comment fonctionne la surveillance de l’intégrité.

Pour plus d’informations sur la façon d’utiliser cette fonctionnalité, consultez [surveiller l’intégrité des appareils mis à jour](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Capture d’écran de la page surveiller l’intégrité de l’Analytique de bureau](media/monitor-health.png)

> [!NOTE]  
> Postes de travail Analytique collecte uniquement les données de contrôle d’intégrité à partir d’appareils qui fournissent des données d’utilisation qu'il peut utiliser comme dénominateur. Cela signifie qu’il n’inclut pas les appareils exécutant Windows 7 et Windows 10 qui ne sont pas définies pour partager des données de diagnostic au niveau avancé (limité). Si plus de 10 % des appareils exécutant Windows 10 sont définies pour partager des données de diagnostic à d’autres niveaux qu’avancé (limité), le **surveiller l’intégrité** page affiche un avertissement dans la bannière.  

Pour afficher plus d’informations sur une application spécifique, le complément ou la macro consultatif, sélectionnez-le dans la liste. 



## <a name="apps-and-office-apps"></a>Applications et les applications Office

![Facteurs d’état d’intégrité pour une application de bureau Analytique](media/monitor-health-status-factors.png)

Analytique de postes de travail analyse des facteurs suivants de l’état d’intégrité pour les applications et les applications Office :

- **Pourcentage d’appareils avec blocages**: Pour les deux dernières semaines, le nombre d’appareils sur lesquels cette application particulière s’est arrêté anormalement divisé par le nombre d’appareils sur lesquels l’application a été utilisée. Cette vue vous permet de voir si la stabilité de l’application a augmenté ou diminué sur la nouvelle version du système d’exploitation. Postes de travail Analytique calcule ce pourcentage pour les ensembles suivants :  

    - **Après mise à jour**: Appareils qui ont mis à jour vers la version de système d’exploitation cible spécifiée dans le plan de déploiement. Pour réduire le nombre de ressources avec des données insuffisantes, bureau Analytique collecte ces données pour tous vos appareils mis à jour. Cet ensemble inclut ces appareils pas dans le plan de déploiement.  

    - **Avant la mise à jour**: Appareils qui se trouvent sur une version du système d’exploitation antérieurs à ce qui est spécifié dans le plan de déploiement. Cette liste n’inclut pas les appareils exécutant Windows 7.   

    - **Moyenne commerciale**: La moyenne (avg) se bloquer taux sur tous les appareils commerciaux. Cette moyenne est calculée sur *tous les* versions de l’application. Si votre version affiche un taux de blocage supérieur à la moyenne commerciale, une version plus stable peuvent être disponibles.  

- **% Sessions avec des blocages**: Similaire au précédent, mais les nombres le pourcentage de sessions avec tombe en panne dans les deux dernières semaines.  

Pour déterminer l’état d’intégrité d’une application, bureau Analytique nécessite des données de moins de 20 périphériques. Sinon, elle indique **pas suffisamment de données** pour l’application. Le service calcule l’état d’intégrité selon les *taux de blocage de session* à partir de ces appareils. Le taux de panne de périphérique est fourni pour information uniquement. Il n’est pas utilisé dans le calcul d’état d’intégrité.

En bas de la page de détails de l’application, les trois onglets suivants peuvent vous aider à résoudre les problèmes :

- **Autres versions**: Liste des autres versions de cette application. Pour chaque version, il montre les modifications relatives aux taux de blocage au sein de votre organisation et la moyenne commerciale. Si vous trouvez une version ultérieure de l’application ayant une vitesse inférieure de la panne, la mise à jour de l’application peut aider.  

    Il indique également si la version a un **prêt pour Windows** signal. Pour plus d’informations, consultez [risque de compatibilité pour les applications Windows](/sccm/desktop-analytics/compat-risk#risk-assessment-engine).  

- **Principaux problèmes**: Une liste de l’ID d’échec plus fréquente par nombre d’instances. Un ID de l’erreur identifie la trace de pile associée à l’incident. Vous pouvez utiliser cet ID lorsque vous appelez l’éditeur de l’application pour la prise en charge.  

- **Les incidents récents**:  Une liste des périphériques sur lesquels l’application récemment est tombé en panne. Vous pouvez filtrer par ID de l’erreur et d’autres critères. Utilisez ces informations pour résoudre le problème par la collecte des journaux ou une tentative de correctifs sur des appareils spécifiques avant d’essayer un déploiement plus large.  

Si vous trouvez une régression de santé sérieux que vous ne parvenez pas à résoudre, modifiez l’application **mise à niveau de la décision** à **impossible**. Cette action empêche le déploiement futur de la mise à jour sur des appareils avec cette ressource.



## <a name="office-add-ins"></a>Compléments Office

![Capture d’écran de facteurs d’état d’intégrité pour un complément Office](media/office-add-in-health-status-factors.png)

Analytique de postes de travail analyse des facteurs suivants de l’état d’intégrité pour les compléments Office :

- **Pourcentage d’appareils avec les incidents**: Un incident est quelque chose qui empêche un complément de fonctionner correctement. Par exemple, il ne parvient pas à charger ou cesse de répondre. Cette section montre, pour les deux dernières semaines, le nombre d’appareils sur lesquels le complément sélectionné avait un incident divisé par le nombre d’appareils sur lesquels le complément est installé. Postes de travail Analytique calcule ce pourcentage pour les ensembles suivants :  

    - **Après mise à jour**: Appareils qui ont mis à jour vers la version d’Office de cible spécifiée dans le plan de déploiement. Pour réduire le nombre de ressources avec des données insuffisantes, bureau Analytique collecte ces données pour tous vos appareils mis à jour. Cet ensemble inclut ces appareils pas dans le plan de déploiement.  

    - **Avant la mise à jour**: Appareils exécutant n’importe quelle version d’Office antérieure à la version que le déploiement plan cibles. <!-- This does not include {include min version of Office}  --> Pour évaluer l’intégrité de la macro complémentaire, comparez cette métrique pour le **après mise à jour** pourcentage.  

    - **Moyenne commerciale**: Le taux d’incident de type moyenne (avg) sur tous les appareils commerciaux qui utilisent la même version du complément, sur la même version d’Office. Utilisez ce taux pour comparer par rapport à des appareils de votre organisation. Si cette version du complément rencontre une fréquence plus élevée aux incidents à la moyenne commerciale, vous pouvez avoir un facteur de l’environnement contribuant aux incidents.  

- **% Des Sessions avec les incidents**: Similaire au précédent, mais les nombres le pourcentage de sessions avec tombe en panne dans les deux dernières semaines.  

Pour déterminer l’état d’intégrité des compléments, Analytique de bureau nécessite au moins trois appareils pour le taux d’incident de périphérique et au moins 10 sessions pour le taux d’incident de session. Pour les deux taux, il compare les valeurs pour déterminer s’il existe une régression avant et après. Aucune régression n’est considéré comme vers la réalisation des objectifs. 

Postes de travail Analytique calcule l’état d’intégrité global du complément Office basé sur une combinaison de périphérique et session taux incident à l’aide de la matrice suivante :

|  | Données insuffisantes des pannes de l’appareil  | Métriques de blocage de périphériques intègres | Régression dans les mesures de blocage d’appareil |
|----------------|---------------------|-----------------------|------------------------|
| **Données insuffisantes pour les sessions avec les incidents**| Données insuffisantes| Objectifs de la réunion | Données insuffisantes |
| **Métriques sain pour les sessions avec les incidents** | Objectifs de la réunion | Objectifs de la réunion | Objectifs de la réunion |
| **Régression dans les métriques pour les sessions avec les incidents** | Données insuffisantes | Objectifs de la réunion | Faites attention |


La page des détails du complément Office inclut également les détails suivants pour vous aider à résoudre les problèmes : 

- **Les incidents récents**: Une liste des appareils sur lesquels un incident complément récemment s’est produite. Cette liste permet de résoudre le problème par la collecte des journaux ou une tentative de correctifs sur ces appareils spécifiques avant d’essayer un déploiement plus large.  



## <a name="office-macros"></a>Macros Office

![Capture d’écran de facteurs d’état d’intégrité pour un avis de macros Office](media/office-macros-health-status-factors.png)

Postes de travail Analytique signale l’état d’intégrité sur *avis de macro*. Avis de macro sont les éventuels problèmes détectés dans les fichiers Office contenant des macros. Ces problèmes sont spécifiques à une application Office. Par exemple, Word, Excel, PowerPoint ou Visio. 

Analytique de postes de travail analyse des facteurs suivants de l’état d’intégrité pour les macros Office :

- **Pourcentage d’appareils avec erreur de compilation**: Pour les deux dernières semaines, le nombre d’appareils sur les erreurs liées à l’avis de sécurité s’est produite pendant l’activation de la macro divisée par le nombre d’appareils sur lesquels l’avis de sécurité a été détectée. Postes de travail Analytique calcule ce pourcentage pour les ensembles suivants : 

    - **Après mise à jour**: Les appareils sur lesquels la version d’Office est identique cible du plan de déploiement  

    - **Avant la mise à jour**: Les appareils exécutant n’importe quelle version d’Office antérieure à la cible du plan de déploiement  

    - **Moyenne commerciale**: La moyenne (avg) de tous les périphériques commerciales exécuter la même version d’Office en tant que cible du plan de déploiement  

- **Pourcentage d’appareils avec erreur d’exécution** similaire à l’exemple précédent, mais pour les deux dernières semaines, les appareils sur lesquels les erreurs liées à l’avis de sécurité s’est produite pendant l’exécution de macro divisée par le nombre d’appareils sur lesquels l’avis de sécurité a été détectée.  

La page de détails de macros Office inclut également les détails suivants pour vous aider à résoudre les problèmes : 

- **Les incidents récents**: Une liste des périphériques sur quelle macro erreurs runtime et de compilation récemment s’est produite. Cette liste permet de résoudre le problème par la collecte des journaux ou une tentative de correctifs sur ces appareils spécifiques avant d’essayer un déploiement plus large.



## <a name="see-also"></a>Voir aussi

- [Risque de compatibilité pour les applications Windows dans Desktop Analytique](/sccm/desktop-analytics/compat-risk)  

- [Comment déployer en production avec Analytique de bureau](/sccm/desktop-analytics/deploy-prod)  
