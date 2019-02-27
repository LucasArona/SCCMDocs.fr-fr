---
title: Collecte des données de diagnostic
titleSuffix: Configuration Manager
description: Découvrez comment System Center Configuration Manager collecte les données de diagnostic et d’utilisation y afférentes.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 704c64d314f2eaf4fe2678f316ea729584752d2e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125576"
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Comment les données d’utilisation et de diagnostic sont collectées pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour collecter les données de diagnostic et d’utilisation pour System Center Configuration Manager, chaque site principal exécute des requêtes SQL Server à une fréquence hebdomadaire. Dans une hiérarchie multisite, les données sont répliquées vers le site d’administration centrale.  

Sur le site de niveau supérieur d’une hiérarchie, le rôle système de site de point de connexion de service soumet ces informations quand il recherche des mises à jour. Le mode du point de connexion de service détermine comment les données sont transférées :  

-   **En mode en ligne** : les données d’utilisation et de diagnostic sont envoyées automatiquement une fois par semaine du point de connexion de service au service cloud.  

-   **En mode hors connexion** : les données d’utilisation et de diagnostic sont transférées manuellement à l’aide de l’outil de connexion de service. Pour plus d'informations, voir [Utiliser l’outil de connexion de service pour System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Pour plus d’informations, voir [À propos du point de connexion de service dans System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  
