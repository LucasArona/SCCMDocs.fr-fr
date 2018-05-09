---
title: Évaluer dans un environnement lab
titleSuffix: Configuration Manager
description: Créez un environnement lab pour évaluer System Center Configuration Manager pour une utilisation dans votre organisation.
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e8c5ac335e3baa3797ab81c324ff2282302779d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Évaluer System Center Configuration Manager en créant votre propre environnement lab

*S’applique à : System Center Configuration Manager (Current Branch)*

 Découvrez comment créer un environnement lab pour évaluer System Center Configuration Manager pour une utilisation dans votre organisation.  

 System Center Configuration Manager est un outil complexe et puissant qui permet de gérer vos utilisateurs, logiciels et appareils. Il est judicieux de procéder à une évaluation approfondie de System Center Configuration Manager avant de procéder à un déploiement complet de façon à combiner vos connaissances conceptuelles à des exercices pratiques.  

 Ce guide s’adresse principalement aux administrateurs qui évaluent l’utilisation de Configuration Manager dans des environnements d’entreprise :  

-   Administrateurs à la recherche d’une solution de gestion complète de PC, serveurs et appareils mobiles  

-   Administrateurs dans les secteurs de haute sécurité qui exigent la sécurité liée à la gestion locale des appareils et la souplesse liée à la gestion des appareils dans le cloud  

-   Administrateurs qui souhaitent gérer la montée en puissance de leur architecture de serveurs locale  

## <a name="what-this-lab-does"></a>Ce que fait ce lab  
 L’objectif principal sous-tendant la création de cet environnement lab est de vous fournir les connaissances générales qui vous permettront de commencer à utiliser Configuration Manager et d’améliorer votre connaissance de cet outil. Vous allez examiner pas à pas un assembly expédié de la version actuelle de Configuration Manager en utilisant deux serveurs :  

-   L’un hébergeant Active Directory, le contrôleur de domaine et le serveur DNS  

-   Un autre hébergeant Configuration Manager et tous les composants SQL Server associés  

Les ordinateurs clients sont installés sur Hyper-V. Le lab proprement dit peut aussi être exécuté en tant que système entièrement virtualisé sur un seul serveur.  

## <a name="what-this-lab-does-not-do"></a>Ce que ne fait pas ce lab  
 Ce lab ne vous guidera pas dans tous les scénarios de Configuration Manager possibles. Il n’est pas conçu pour être migré immédiatement dans un environnement actif.  

 Une fois ce lab généré, vous disposerez d’un environnement de travail opérationnel. Toutefois, cet environnement ne sera pas optimisé pour des facteurs tels que les performances du système, la gestion de l’espace sur disque dur et le stockage SQL Server.  

##  <a name="BKMK_EvalRec"></a>Lecture recommandée avant d’élaborer le lab  
 La [documentation de System Center Configuration Manager](http://docs.microsoft.com/sccm/) propose un contenu très riche. Nous vous recommandons de lire les rubriques suivantes de cette bibliothèque avant de commencer le lab :  

-   Découvrez les concepts de base concernant la console Configuration Manager, les portails d’utilisateurs finaux, ainsi que des exemples de scénarios dans [Présentation de System Center Configuration Manager](../../core/understand/introduction.md).  

-   Découvrez les principales fonctionnalités de gestion de Configuration Manager dans [Fonctions et fonctionnalités de System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Approfondissez vos connaissances avec [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Découvrez l’importance des rôles de sécurité dans [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Découvrez la gestion de contenu dans [Concepts de la gestion de contenu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Apprenez à traiter correctement les opérations quotidiennes tout au long de votre déploiement dans [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  
