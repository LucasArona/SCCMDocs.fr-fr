---
title: Configuration requise pour la gestion de l’alimentation
titleSuffix: Configuration Manager
description: Prenez connaissance des prérequis pour la gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9c062f13-3c1f-4621-9cae-de0e322aa03f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c6630ef07c0b7947875ea2adac4e6612143aaee8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-power-management-in-system-center-configuration-manager"></a>Configuration requise pour la gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion de l’alimentation dans System Center Configuration Manager comporte des dépendances externes et des dépendances au sein du produit.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  
 Le tableau suivant répertorie les dépendances externes à Configuration Manager pour l’utilisation de la gestion de l’alimentation.  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Les ordinateurs client doivent être en mesure de prendre en charge les états requis de l'alimentation|Pour utiliser toutes les fonctionnalités de la gestion de l'alimentation, les ordinateurs client doivent être en mesure de prendre en charge la mise en veille, la mise en veille prolongée, la sortie du mode veille et la sortie du mode veille prolongée. Vous pouvez utiliser le rapport **Fonctions de gestion de l'alimentation** afin de déterminer si les ordinateurs peuvent prendre en charge ces actions. Pour plus d’informations, consultez le rapport [Fonctions de gestion de l’alimentation](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Capabilites) dans la rubrique [Guide pratique pour surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).|  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  
 Le tableau suivant répertorie les dépendances au sein de Configuration Manager pour l’utilisation de la gestion de l’alimentation.  

|Dépendance|Informations complémentaires|  
|----------------|----------------------|  
|Vous devez activer la gestion de l'alimentation avant de pouvoir créer et surveiller des modes d'alimentation.|Pour plus d’informations sur la façon d’activer et de configurer la gestion de l’alimentation, consultez [Configuration de la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).|  
|Point de Reporting Services|Vous devez configurer un point de Reporting Services avant de pouvoir afficher des rapports de gestion de l'alimentation. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
