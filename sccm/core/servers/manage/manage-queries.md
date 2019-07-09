---
title: Gérer les requêtes
titleSuffix: Configuration Manager
description: Découvrez comment gérer vos requêtes. Inclut un tableau contenant des informations de référence détaillées.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 456289520e25fe94da7e94f6a795537f68ba069e
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561976"
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>Guide pratique pour gérer les requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article peut vous permettre de gérer les requêtes dans System Center Configuration Manager.  

 Pour plus d’informations sur la création de requêtes, consultez [Guide pratique pour créer des requêtes dans System Center Configuration Manager](../../../core/servers/manage/create-queries.md).  

## <a name="manage-queries"></a>Gérer les requêtes
 Dans l'espace de travail **Surveillance** , sélectionnez successivement **Requêtes**, la requête à gérer et une tâche de gestion.  

 Le tableau suivant fournit des informations sur les tâches de gestion.  

|Tâche de gestion|Détails| 
|---------------------|-------------|
|**Exécuter**|Exécute la requête sélectionnée et affiche les résultats dans la console Configuration Manager.|
|**Installer le client**|Ouvre l’**Assistant Installation du client** qui permet d’installer le client Gestionnaire de configuration sur les ordinateurs retournés par la requête sélectionnée.<br /><br /> Cette option n'est pas disponible pour les requêtes qui retournent des appareils mobiles, des utilisateurs ou des groupes d'utilisateurs. <br /><br /> Pour plus d’informations sur la façon d’installer des clients Configuration Manager à l’aide de l’installation push du client, consultez [Guide pratique pour déployer des clients sur des ordinateurs Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).| 
|**Exporterer**|Ouvre l’**Assistant Exportation d’objets**. Cet Assistant vous permet d’exporter la requête dans un fichier au format MOF que vous pouvez ensuite importer sur un autre site.
|**Déplacer**|Ouvre la boîte de dialogue **Déplacer les éléments sélectionnés**. Cette boîte de dialogue vous permet de déplacer la requête sélectionnée vers un dossier que vous avez créé précédemment sous le nœud **Requêtes**.|

## <a name="next-steps"></a>Étapes suivantes 
 [Créer des requêtes dans System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
