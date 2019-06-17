---
title: Ressources dans les postes de travail Analytique
titleSuffix: Configuration Manager
description: En savoir plus sur les appareils, des pilotes et des applications dans Desktop Analytique.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 972ccf97590cb7662b5bf0a8e5bd3acb410f5766
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145800"
---
# <a name="assets-in-desktop-analytics"></a>Ressources dans les postes de travail Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Une fois que les appareils signalent des données pour l’Analytique de bureau, il fournit un inventaire des ressources suivantes :

- Appareils  
- Pilotes de matériel  
- Applications installées  

Dans le portail de service, sélectionnez **actifs** dans le menu d’Analytique de bureau.


## <a name="devices"></a>Appareils

Le **appareils** onglet affiche des informations clés sur tous les appareils de votre organisation que vous inscrivez pour l’Analytique de bureau. Vous pouvez trier sur une colonne ou un filtre pour des valeurs particulières.

> [!NOTE]  
> Si le tableau de bord n’est pas signalé le nombre d’appareils voulus pour votre environnement, consultez [la résolution des problèmes de bureau Analytique](/sccm/desktop-analytics/troubleshooting).  

Dans un plan de déploiement, il existe plus de détails sur les appareils. Pour plus d’informations, consultez [planifier les ressources](/sccm/desktop-analytics/about-deployment-plans#plan-assets)

## <a name="apps"></a>Applications

Le **applications** onglet affiche tous les installé les applications qui le service détecte sur vos appareils Windows.

**Dignes d’intérêt** applications sont installées sur plus de 2 % d’appareils inscrits.

Configurer le **Importance** d’applications en définissant l’une des catégories suivantes :

- Critique
- Important
- Ignorer
- Non révisé

Sélectionnez l’application à partir de la liste, puis **modifier**. Cette action affiche les détails de l’application. Sélectionnez le **Importance** menu déroulant et définit une valeur. Vous pouvez également affecter un **propriétaire**. Si vous apportez des modifications, sélectionnez **enregistrer**.

Dans un plan de déploiement, vous pouvez également définir le **mise à niveau de la décision**. Pour plus d’informations, consultez [planifier les ressources](/sccm/desktop-analytics/about-deployment-plans#plan-assets)


## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur les plans de déploiement de bureau Analytique](/sccm/desktop-analytics/about-deployment-plans)  

- [En savoir plus sur les mises à jour de sécurité et de fonctionnalité](/sccm/desktop-analytics/about-updates)  

- [Évaluation de la compatibilité dans Desktop Analytique](/sccm/desktop-analytics/compat-assessment)  
