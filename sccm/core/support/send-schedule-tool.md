---
title: Outil Send Schedule
titleSuffix: Configuration Manager
description: Utilisez Send Schedule Tool pour déclencher une planification sur un client Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d5ce547d-3b3b-47d3-bcd7-6ff94692c046
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 97c506c85cbb26dbb68b2e0eb0c223ae2a9d5b7e
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500780"
---
# <a name="send-schedule-tool"></a>Outil Send Schedule

*S’applique à : System Center Configuration Manager (Current Branch)*

Send Schedule Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez-le pour déclencher une planification sur un client ou déclencher l’évaluation d’une base de référence de configuration spécifiée. Il fonctionne aussi bien sur l’ordinateur local que sur un client distant.  

Par exemple, utilisez l’outil pour déclencher un calendrier de l’inventaire ou une évaluation de la conformité. Si un nombre de clients Configuration Manager n’a pas fait récemment état de l’inventaire ou de la conformité, exécutez l’outil pour lancer la planification nécessaire sur chaque client.



## <a name="usage"></a>Utilisation

Exécutez **SendSchedule.exe** en tant qu’administrateur. 

`SendSchedule /L [Computer Name]`
`SendSchedule "<Message GUID | DCM UID>" [Computer Name]` 

Une fois que vous déclenchez un message (GUID), consultez **SMSClientMethodProvider.log**. Pour plus d’informations sur les GUID de message disponibles, consultez [ID de Message](#bkmk_sendschedule-guids).

Une fois que vous déclenchez l’évaluation d’une base de référence de configuration (DCM UID), consultez **DCMAgent.log**.



## <a name="command-line-options"></a>Options de ligne de commande


### <a name="option-l"></a>Option : `/L` 
Listez tous les GUID ou DCM UID de message disponibles pour les envoyer. Affichez le nom explicite des messages de la table de données pour chacun d’eux. Si le nom d’ordinateur est absent, il utilise l’ordinateur local. Si vous spécifiez un message sans nom d’ordinateur, l’outil envoie le message à l’ordinateur local. 



## <a name="examples"></a>Exemples

#### <a name="list-the-available-messages-on-the-local-machine"></a>Lister les messages disponibles sur l’ordinateur local 
`SendSchedule /L` 

#### <a name="list-the-available-messages-on-the-client-mypc"></a>Lister les messages disponibles sur le client MyPC : 
`SendSchedule /L MyPC`

#### <a name="trigger-hardware-inventory-on-the-local-machine"></a>Déclencher l’inventaire matériel sur l’ordinateur local
`SendSchedule {00000000-0000-0000-0000-000000000001}`

#### <a name="trigger-hardware-inventory-on-mypc"></a>Déclencher l’inventaire matériel sur MyPC : 
`SendSchedule {00000000-0000-0000-0000-000000000001} MyPC` 

#### <a name="trigger-the-evaluation-of-a-specific-configuration-baseline-on-mypc"></a>Déclencher l’évaluation d’une base de référence de configuration spécifique sur MyPC : 
`SendSchedule ScopeId_611E8382-C064-4B62-B0DE-EFFB52AE8994/Baseline_36722778-69dd-4423-9632-b61148b2b67e MyPC` 



## <a name="bkmk_sendschedule-guids"></a>ID de message

|ID de message  |Nom d'affichage  |
|---------|---------|
|{00000000-0000-0000-0000-000000000001}|Inventaire matériel|
|{00000000-0000-0000-0000-000000000002}|Inventaire logiciel|
|{00000000-0000-0000-0000-000000000003}|Discovery Inventory|
|{00000000-0000-0000-0000-000000000010}|File Collection|
|{00000000-0000-0000-0000-000000000011}|IDMIF Collection|
|{00000000-0000-0000-0000-000000000021}|Request Machine Assignments|
|{00000000-0000-0000-0000-000000000022}|Evaluate Machine Policies|
|{00000000-0000-0000-0000-000000000023}|Refresh Default MP Task|
|{00000000-0000-0000-0000-000000000024}|LS (Location Service) Refresh Locations Task|
|{00000000-0000-0000-0000-000000000025}|LS Timeout Refresh Task|
|{00000000-0000-0000-0000-000000000026}|Policy Agent Request Assignment (User)|
|{00000000-0000-0000-0000-000000000027}|Policy Agent Evaluate Assignment (User)|
|{00000000-0000-0000-0000-000000000031}|Software Metering Generating Usage Report|
|{00000000-0000-0000-0000-000000000032}|Source Update Message|
|{00000000-0000-0000-0000-000000000037}|Clearing proxy settings cache|
|{00000000-0000-0000-0000-000000000040}|Machine Policy Agent Cleanup|
|{00000000-0000-0000-0000-000000000041}|User Policy Agent Cleanup|
|{00000000-0000-0000-0000-000000000042}|Policy Agent Validate Machine Policy / Assignment|
|{00000000-0000-0000-0000-000000000043}|Policy Agent Validate User Policy / Assignment|
|{00000000-0000-0000-0000-000000000051}|Retrying/Refreshing certificates in AD on MP|
|{00000000-0000-0000-0000-000000000061}|Peer DP Status reporting|
|{00000000-0000-0000-0000-000000000062}|Peer DP Pending package check schedule|
|{00000000-0000-0000-0000-000000000063}|SUM Updates install schedule|
|{00000000-0000-0000-0000-000000000071}|NAP Action|
|{00000000-0000-0000-0000-000000000101}|Hardware Inventory Collection Cycle|
|{00000000-0000-0000-0000-000000000102}|Software Inventory Collection Cycle|
|{00000000-0000-0000-0000-000000000103}|Discovery Data Collection Cycle|
|{00000000-0000-0000-0000-000000000104}|File Collection Cycle|
|{00000000-0000-0000-0000-000000000105}|IDMIF Collection Cycle|
|{00000000-0000-0000-0000-000000000106}|Software Metering Usage Report Cycle|
|{00000000-0000-0000-0000-000000000107}|Windows Installer Source List Update Cycle|
|{00000000-0000-0000-0000-000000000108}|Software Updates Policy Action Software Updates Assignments Evaluation Cycle|
|{00000000-0000-0000-0000-000000000109}|PDP Maintenance Policy Branch Distribution Point Maintenance Task|
|{00000000-0000-0000-0000-000000000110}|DCM policy|
|{00000000-0000-0000-0000-000000000111}|Send Unsent State Message|
|{00000000-0000-0000-0000-000000000112}|State System policy cache cleanout|
|{00000000-0000-0000-0000-000000000113}|Update source policy|
|{00000000-0000-0000-0000-000000000114}|Update Store Policy|
|{00000000-0000-0000-0000-000000000115}|State system policy bulk send high|
|{00000000-0000-0000-0000-000000000116}|State system policy bulk send low|
|{00000000-0000-0000-0000-000000000120}|AMT Status Check Policy|
|{00000000-0000-0000-0000-000000000121}|Application manager policy action|
|{00000000-0000-0000-0000-000000000122}|Application manager user policy action|
|{00000000-0000-0000-0000-000000000123}|Application manager global evaluation action|
|{00000000-0000-0000-0000-000000000131}|Power management start summarizer|
|{00000000-0000-0000-0000-000000000221}|Endpoint deployment reevaluate|
|{00000000-0000-0000-0000-000000000222}|Endpoint AM policy reevaluate|
|{00000000-0000-0000-0000-000000000223}|External event detection|



