---
title: Présentation des requêtes
titleSuffix: Configuration Manager
description: Créez et exécutez des requêtes pour rechercher les objets dans une hiérarchie System Center Configuration Manager qui correspondent à vos critères de requête.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28fe8d38b03efaa101cfe01d8a8a054f0b26f2ed
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561957"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Présentation des requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer et exécuter des requêtes pour rechercher les objets dans une hiérarchie System Center Configuration Manager qui correspondent à vos critères de requête. Ces objets incluent des éléments tels que des types spécifiques d'ordinateurs ou de groupes d'utilisateurs. Les requêtes peuvent renvoyer la plupart des types d’objets Configuration Manager, à savoir des sites, des regroupements, des applications et des données d’inventaire.  

## <a name="query-creation-overview"></a>Vue d’ensemble de la création de requêtes

 Quand vous créez une requête, vous devez spécifier au moins deux paramètres : où effectuer la recherche et ce que vous souhaitez rechercher. Par exemple, pour rechercher la quantité d’espace disponible sur le disque dur de tous les ordinateurs dans un site Configuration Manager, vous pouvez créer une requête pour rechercher la classe d’attribut **Disque logique** et l’attribut **Espace libre (Mo)** pour déterminer l’espace disque disponible.  

 Après avoir créé une requête initiale, vous pouvez spécifier d'autres critères. Par exemple, vous pouvez spécifier que les résultats de la requête incluent uniquement les ordinateurs affectés à un site spécifié. Vous pouvez aussi modifier l'affichage des résultats pour visualiser les résultats dans un ordre qui est significatif pour vous. Par exemple, vous pouvez spécifier que les résultats sont classés par quantité d'espace disponible sur le disque dur en ordre croissant ou décroissant.  

 Lorsque vous créez une requête, elle est stockée par Configuration Manager et affichée dans le nœud **Requêtes** de l’espace de travail **Surveillance**. À partir de cet emplacement, vous pouvez créer de nouvelles requêtes et exécuter, mettre à jour et gérer les requêtes existantes.  

 Vous pouvez également importer une requête dans une règle de requête dans un regroupement Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Étapes suivantes

 [Guide pratique pour créer des requêtes dans System Center Configuration Manager](../../../core/servers/manage/create-queries.md)
