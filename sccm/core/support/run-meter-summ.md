---
title: Run Meter Summarization Tool
titleSuffix: Configuration Manager
description: Utilisez Run Meter Summarization Tool pour déclencher les tâches de résumé du contrôle de logiciel dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b044272663ada4b43536f88c293308c57732e9c4
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500812"
---
# <a name="run-meter-summarization-tool"></a>Run Meter Summarization Tool

*S’applique à : System Center Configuration Manager (Current Branch)*

Run Meter Summarization Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez-le pour déclencher immédiatement les tâches de maintenance de résumé du contrôle de logiciel sur les sites principaux. Par défaut, ces tâches sont exécutées comme prévu dans les tâches de **maintenance du site**, qui démarrent chaque jour après 00:00. 

Ces tâches résument les données dans la table SQL **MeterData** et écrivent les résultats du résumé dans les tables **FileUsageSummary** et **MonthlyUsageSummary**. Vous voyez ensuite le résultat résumé dans les rapports de contrôle de logiciel. Tout utilisateur administratif Configuration Manager qui peut se connecter à la base de données du site principal peut utiliser cet outil pour exécuter le résumé. 

Cet outil exécute les tâches de résumé de données du contrôle de logiciel **Résumé de l’utilisation de fichier** et **Résumé de l’utilisation mensuelle**. Il récapitule toutes les données de compteur sans le délai d’attente habituel de 12 heures. Exécutez-le sur le serveur SQL Server qui héberge la base de données du site. Si le résumé est réussi, le code de sortie a la valeur `0`. Si une erreur s’est produite, le code de sortie est `1`.



## <a name="usage"></a>Utilisation

### <a name="command-line"></a>Ligne de commande

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Options

#### <a name="database-name"></a>Nom de la base de données
Nom de la base de données du site sur le serveur SQL Server.

#### <a name="delay-in-hours-for-summarization"></a>Délai en heures pour le résumé
L’outil résume l’utilisation du contrôle de logiciel générée avant le délai. Par défaut, ce délai est égal à zéro.


### <a name="example"></a>Exemple

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Résumer l’utilisation du contrôle de logiciel générée il y a 12 heures

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>Voir aussi

- [Tâches de maintenance](/sccm/core/servers/manage/maintenance-tasks)
- [Surveiller l’utilisation des applications avec le contrôle de logiciel](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering)
