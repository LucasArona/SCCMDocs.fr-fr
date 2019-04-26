---
title: Ressources dans les postes de travail Analytique
titleSuffix: Configuration Manager
description: En savoir plus sur les appareils, applications, les applications Office, des compléments Office et les macros Office dans Analytique de bureau.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 149c5f2a4469a353c6dce6fde86527ca95518484
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62254640"
---
# <a name="assets-in-desktop-analytics"></a>Ressources dans les postes de travail Analytique 

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Une fois que les appareils signalent des données pour l’Analytique de bureau, il fournit un inventaire des ressources suivantes :
- Appareils  
- Pilotes de matériel  
- Applications installées  
- Applications Office  
- Compléments Office  
- Macros Office  

Dans le portail de service, sélectionnez **actifs** dans le menu d’Analytique de bureau.


## <a name="devices"></a>Appareils

Le **appareils** onglet affiche des informations clés sur tous les appareils de votre organisation que vous inscrivez pour l’Analytique de bureau. Vous pouvez trier sur une colonne ou un filtre pour des valeurs particulières.

> [!NOTE]  
> Si le tableau de bord n’est pas signalé le nombre d’appareils voulus pour votre environnement, consultez [la résolution des problèmes de bureau Analytique](/sccm/desktop-analytics/troubleshooting).  



## <a name="apps"></a>Applications

Le **applications** onglet affiche tous les installé les applications qui le service détecte sur vos appareils Windows.

**Dignes d’intérêt** applications sont installées sur plus de 2 % d’appareils inscrits. <!--You can change the threshold of "noteworthy" by {doing something}.--> 

Configurer le **Importance** d’applications en définissant l’une des catégories suivantes :

- Critique
- Important
- Ignorer
- Non révisé

Sélectionnez l’application à partir de la liste, puis **modifier**. Cette action affiche les détails de l’application. Sélectionnez le **Importance** menu déroulant et définit une valeur. Vous pouvez également affecter un **propriétaire**. Si vous apportez des modifications, sélectionnez **enregistrer**. 


## <a name="office-apps"></a>Applications Office

Le **applications Office** onglet est similaire à l’onglet applications. Il affiche uniquement les applications telles que Microsoft Word ou Excel, et aucune catégorisation ou d’un nombre dignes d’intérêt. Définir l’importance et le propriétaire pour les applications Office comme avec d’autres applications.


## <a name="office-add-ins"></a>Compléments Office

Le **des compléments Office** onglet montre prenant en charge des outils, par exemple, Microsoft Azure Information Protection ou l’utilitaire d’analyse. Cet onglet est similaire à l’onglet applications, et il inclut le nombre dignes d’intérêt. Définir l’importance et le propriétaire comme avec les applications. 


## <a name="office-macros"></a>Macros Office

Le **macros Office** onglet indique si tous les périphériques ont accédé récemment tous les fichiers qui peuvent inclure des macros. 

<!-- (For a detailed list of these file types, see [File formats supported in the 2007 Office system (corrected)](https://blogs.technet.microsoft.com/office_resource_kit/2009/04/04/file-formats-supported-in-the-2007-office-system-corrected/) at the Office IT Pro blog.)
 -->

> [!NOTE]  
> Si vous utilisez également le [Readiness Toolkit](https://aka.ms/readinesstoolkit) pour les compléments Office et Visual Basic pour les macros d’Applications (VBA), cet onglet affiche également des données supplémentaires à partir de ces appareils. 
> 
> Vous n’avez pas besoin d’utiliser le Readiness Toolkit à utiliser l’Analytique de bureau.  



## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur les plans de déploiement de bureau Analytique](/sccm/desktop-analytics/about-deployment-plans)  

- [En savoir plus sur les mises à jour de sécurité et de fonctionnalité](/sccm/desktop-analytics/about-updates)  

