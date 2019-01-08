---
title: Utiliser des limites et groupes de limites
titleSuffix: Configuration Manager
description: Utilisez les limites et les groupes de limites pour définir les emplacements réseau et les systèmes de site accessibles pour les appareils que vous gérez.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 85d7dbb494f1d6288ad7a45fad98e24a6ad2b393
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421142"
---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Définir des limites de site et les groupes de limites pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les limites pour System Center Configuration Manager définissent les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer. Les groupes de limites sont des groupes logiques de limites que vous configurez.

 Une hiérarchie peut inclure n’importe quel nombre de groupes de limites, et chaque groupe de limites peut contenir n’importe quelle combinaison des types de limites suivants :  

-   Sous-réseau IP  
-   Nom de site Active Directory  
-   Préfixe IPv6  
-   Plage d'adresses IP  

Les clients intranet évaluent leur emplacement réseau actuel, puis utilisent ces informations pour identifier les groupes de limites auxquels ils appartiennent.  

 Les clients utilisent des groupes de limites pour :  
-   **Trouver un site attribué :** Les groupes de limites permettent aux clients de trouver un site principal pour l’attribution du client (attribution automatique de site).  
-   **Trouver des rôles de système de site spécifiques disponibles :** Quand vous associez un groupe de limites à certains rôles de système de site, le groupe de limites fournit aux clients la liste des systèmes de site à utiliser pour l’emplacement du contenu et en tant que points de gestion préférés.  

Les clients Internet ou les clients configurés en tant que clients Internet uniquement n’utilisent pas les informations sur les limites. Ces clients ne peuvent pas utiliser l’attribution automatique de site. Ils peuvent toujours télécharger le contenu de n’importe quel point de distribution sur leur site attribué quand le point de distribution est configuré pour autoriser les connexions clientes depuis Internet.  

**Pour bien démarrer :**
- Tout d’abord, [définissez les emplacements réseau en tant que limites](/sccm/core/servers/deploy/configure/boundaries).
- Puis, poursuivez en [configurant des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups) pour associer les clients dans ces limites aux serveurs de système de site qu’ils peuvent utiliser.



##  <a name="BKMK_BoundaryBestPractices"></a> Meilleures pratiques en matière de limites et de groupes de limites  

- **Utilisez une combinaison du plus petit nombre de limites qui répondent à vos besoins :**  
  Dans le passé, nous vous avons conseillé d’utiliser certains types de limites plus que d’autres. Compte-tenu des modifications apportées pour améliorer les performances, nous vous conseillons dorénavant d’utiliser le ou les types de votre choix qui fonctionnent dans votre environnement et qui vous permettent d’utiliser le plus petit nombre de limites possible pour simplifier vos tâches de gestion.      

- **Éviter le chevauchement des limites pour l’attribution automatique de site :**  
   Chaque groupe de limites prend en charge les configurations d’attribution de site et d’emplacement du contenu, mais il est recommandé de créer un ensemble de groupes de limites à utiliser uniquement pour l’attribution de site. Cela signifie que vous devez vérifier qu’aucune limite d’un groupe de limites n’est membre d’un autre groupe de limites ayant une attribution de site différente. La raison est la suivante :  

  - Une limite peut être incluse dans plusieurs groupes de limites.  

  - Chaque groupe de limites peut être associé à un site principal différent pour l’attribution de site.  

  - Un client sur une limite qui est membre de deux groupes de limites ayant des attributions de site différentes sélectionne au hasard un site auquel se joindre, site qui n’est pas nécessairement le site que vous avez prévu à cet effet.  Cette configuration est appelée chevauchement des limites.  

    Le chevauchement des limites n’est pas un problème pour l’emplacement du contenu. Il s’agit souvent d’une configuration souhaitée qui fournit aux clients des ressources ou emplacements de contenu supplémentaires qu’ils peuvent utiliser.  
