---
title: "Conditions préalables pour les regroupements | System Center Configuration Manager"
description: "Prenez connaissance des conditions préalables à l’utilisation de regroupements dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
caps.latest.revision: 7
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 99ddc0ba39778db4e8e45d6e954894464c7e047c


---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Conditions préalables pour les regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les regroupements contiennent uniquement des dépendances à l’intérieur du produit.  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Point de Reporting Services|Le rôle de système de site du point de Reporting Services doit être installé pour pouvoir exécuter des rapports pour les regroupements. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Des autorisations de sécurité spécifiques doivent avoir été accordées pour gérer les regroupements|Vous devez disposer des autorisations de sécurité suivantes pour gérer les paramètres de compatibilité :<br /><br /> - Pour créer et gérer des regroupements : **Créer**, **Supprimer**, **Modifier**, **Modifier un dossier**, **Déplacer un objet**, **Lecture** et **Lire la ressource** pour l’objet **Regroupement**.<br /><br /> - Pour gérer les paramètres de regroupement : **Modifier les paramètres de regroupement** pour l’objet **Regroupement**.<br /><br /> L’autorisation **Modifier un dossier** est nécessaire pour tous les dossiers de regroupement, y compris le dossier racine.|  



<!--HONumber=Nov16_HO1-->


