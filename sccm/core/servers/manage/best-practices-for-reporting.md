---
title: Bonnes pratiques pour les rapports
titleSuffix: Configuration Manager
description: Lire des conseils utiles sur l’utilisation de la fonction de rapport de System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 87ed3a0591107695a1f418b38f2e3f5cb9168c63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337589"
---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Pratiques recommandées pour la création de rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les bonnes pratiques suivantes pour les rapports dans System Center Configuration Manager :  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Pour des performances optimales, installez le point de Reporting Services sur un serveur de système de site distant  
 Même si vous pouvez installer le point de Reporting Services sur le serveur de site ou sur un système de site distant, la performance est meilleure lorsque vous installez le point de Reporting Services sur un serveur de système de site distant.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Optimiser les requêtes de SQL Server Reporting Services  
 En règle générale, les délais de création de rapports sont liés à la durée nécessaire à l'exécution des requêtes et à la récupération des résultats. Si vous utilisez Microsoft SQL Server, les outils tels que l'analyseur de requêtes et le générateur de profils peuvent vous aider à optimiser des requêtes.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Planifier l'exécution du traitement des abonnements aux rapports en dehors des heures de bureau habituelles  
 Dès que possible, planifiez le traitement des abonnements aux rapports en dehors des heures de bureau habituelles pour minimiser le traitement par le processeur sur le serveur de base de données du site Configuration Manager. Cette pratique améliore également la disponibilité pour les demandes de rapport imprévues.  

## <a name="next-steps"></a>Étapes suivantes
[Configurer les rapports](configuring-reporting.md)
