---
title: Planifier la migration
titleSuffix: Configuration Manager
description: Informez-vous sur les sites et les hiérarchies avant de migrer des données vers une hiérarchie de destination System Center Configuration Manager.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2091f3f41336413a49446a14b1190cce426c8277
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333159"
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>Planifier la migration vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de migrer des données vers une hiérarchie de destination System Center Configuration Manager, familiarisez-vous avec les sites et les hiérarchies dans Configuration Manager. Pour plus d’informations sur les sites et les hiérarchies, consultez [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md).  

 Avant de migrer des données à partir d’une hiérarchie source prise en charge, vous devez installer une hiérarchie System Center Configuration Manager comme hiérarchie de destination.  

 Une fois la hiérarchie de destination installée, avant de commencer à migrer les données, configurez les fonctionnalités de gestion et les fonctions que vous voulez utiliser dans votre hiérarchie de destination.  

 En outre, vous devrez peut-être anticiper un éventuel chevauchement entre la hiérarchie source et votre hiérarchie de destination. Supposons par exemple que vous configurez une hiérarchie source pour utiliser les mêmes emplacements réseau ou les mêmes limites que votre hiérarchie de destination, que vous installez ensuite de nouveaux clients sur votre hiérarchie de destination et que vous utilisez l’affectation de site automatique. Dans ce scénario, comme un client Configuration Manager nouvellement installé peut sélectionner un site à rejoindre dans l’une ou l’autre des hiérarchies, le client risque d’être incorrectement affecté à votre hiérarchie source. Par conséquent, au lieu d’utiliser la fonctionnalité d’affectation de site automatique, prévoyez plutôt d’affecter chaque nouveau client de la hiérarchie de destination à un site spécifique de cette hiérarchie.  

 Pour plus d’informations sur les affectations de site, consultez [Considérations sur l’affectation de sites aux clients](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) dans [Interopérabilité entre les différentes versions de System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="plan-topics"></a>Rubriques liées à la planification  
 Utilisez les rubriques suivantes pour planifier la migration d’une hiérarchie source prise en charge vers une hiérarchie de destination System Center Configuration Manager :

-   [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Listes de vérification de l’administrateur pour la planification de la migration dans System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Déterminer s’il faut migrer des données vers System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Planifier une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Listes de vérification de l’administrateur pour la planification de la migration dans System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Planifier une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Planifier une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Planifier la migration d’objets Configuration Manager vers System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Planifier la surveillance de la migration dans System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Planifier la fin de la migration dans System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  
