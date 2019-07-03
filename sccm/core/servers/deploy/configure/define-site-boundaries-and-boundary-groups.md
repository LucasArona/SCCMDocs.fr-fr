---
title: Utiliser des limites et groupes de limites
titleSuffix: Configuration Manager
description: Utilisez les limites et les groupes de limites pour définir les emplacements réseau et les systèmes de site accessibles pour les appareils que vous gérez.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d160c6ab64c5ad097bf5986882b65171b0df4651
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194157"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Définir les limites de site et les groupes de limites

*S’applique à : System Center Configuration Manager (Current Branch)*

Les *Limites* dans Configuration Manager définissent les emplacements réseau sur votre Intranet. Ces emplacements incluent les appareils que vous souhaitez gérer. Les *groupes de limites* sont des groupes logiques de limites que vous configurez.

Une hiérarchie peut inclure n’importe quel nombre de groupes de limites. Chaque groupe de limites peut contenir n’importe quelle combinaison de types de limites suivants :  

- Sous-réseau IP  
- Nom de site Active Directory  
- Préfixe IPv6  
- Plage d'adresses IP  

Les clients intranet évaluent leur emplacement réseau actuel, puis utilisent ces informations pour identifier les groupes de limites auxquels ils appartiennent.  

Les clients utilisent des groupes de limites pour :  

- **Trouver un site attribué :** Les groupes de limites permettent aux clients de trouver un site principal pour l’attribution du client. Ce comportement est également appelé *attribution automatique de site*.  

- **Trouver des rôles de système de site spécifiques disponibles :** Associer un groupe de limites à certains rôles de système de site. Le site fournit ensuite aux clients cette liste de systèmes de site dans le groupe de limites. Les clients utilisent ces systèmes de site pour des actions telles que la recherche de contenu un d’un point de gestion situé à proximité.  

Les clients Internet ou les clients configurés en tant que clients Internet uniquement n’utilisent pas les informations sur les limites. Ces clients ne peuvent pas utiliser une attribution automatique du site. Ils peuvent télécharger le contenu d’un point de distribution basé sur internet à partir de leur site attribué ou d’un point de distribution basé sur le cloud.  

À partir de la version 1902, vous pouvez associer une passerelle de gestion cloud (CMG) avec un groupe de limites. Pour plus d’informations, consultez [Conception de la hiérarchie de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#hierarchy-design).<!--3640932-->


## <a name="BKMK_BoundaryBestPractices"></a> Recommandations

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Utilisez une combinaison du plus petit nombre de limites qui répondent à vos besoins

Utilisez le ou les types de limites choisis qui fonctionnent dans votre environnement. Pour simplifier vos tâches de gestion, utilisez les types de limites qui vous permettent d’utiliser le plus petit nombre de limites possible.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Éviter le chevauchement des limites pour l’attribution automatique de site

Même si chaque groupe de limites prend à la fois en charge la référence d’attribution de site et de système de site, créez un ensemble de groupes de limites à utiliser uniquement pour l’attribution de site. Vérifiez qu’aucune limite d’un groupe de limites n’est membre d’un autre groupe de limites ayant une attribution de site différente.

- Une limite unique peut être incluse dans plusieurs groupes de limites.  

- Chaque groupe de limites peut être associé à un site principal différent pour l’attribution de site.  

- Pour une limite qui est membre de deux groupes de limites différents avec des attributions de site différentes, les clients sélectionnent au hasard un site à joindre. Ce comportement peut ne pas concerner le site dont vous souhaitez que le client le joigne. Cette configuration est appelée *chevauchement des limites*.  

    Le chevauchement de limites n’est pas un problème pour l'emplacement du contenu. Cette configuration peut être utile, car eIle fournit aux clients des ressources supplémentaires ou des emplacements de contenu qu’ils peuvent utiliser.  


## <a name="next-steps"></a>Étapes suivantes

- [Définissez les emplacements réseau en tant que limites](/sccm/core/servers/deploy/configure/boundaries)

- [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups)
