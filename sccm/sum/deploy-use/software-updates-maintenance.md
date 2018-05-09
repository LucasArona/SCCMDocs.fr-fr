---
title: Maintenance des mises à jour logicielles
titleSuffix: Configuration Manager
description: Pour assurer la maintenance des mises à jour dans Configuration Manager, vous pouvez planifier la tâche de nettoyage WSUS, ou vous pouvez l’exécuter manuellement.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 03eabbfcd070bb61b2930fac89a551bbeb111eb4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="software-updates-maintenance"></a>Maintenance des mises à jour logicielles

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez planifier et exécuter la tâche de nettoyage WSUS à partir de la console Configuration Manager, ou l’exécuter manuellement à partir des propriétés du composant de point de mise à jour logicielle. Quand vous choisissez d’exécuter la tâche de nettoyage WSUS, elle s’exécute à la prochaine synchronisation des mises à jour logicielles. Les mises à jour logicielles qui ont expiré présentent un état refusé sur le serveur WSUS et l’Agent Windows Update ne les analyse plus. Par défaut, la tâche de nettoyage WSUS s’exécute tous les 30 jours.  

#### <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Pour planifier et exécuter la tâche de nettoyage WSUS  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Sites**.  

2.  Cliquez sur **Configurer les composants de site** dans le groupe **Paramètres** , puis cliquez sur **Point de mise à jour logicielle** pour ouvrir les propriétés du composant du point de mise à jour logicielle.  

3.  Cliquez sur l’onglet **Règles de remplacement** , sélectionnez **Exécuter l’Assistant Nettoyage WSUS**, puis cliquez sur **OK**.
