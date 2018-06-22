---
title: Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune
titleSuffix: Configuration Manager
description: Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1aa0bb03b2e27aebbbf1c080b32445bc7c58c47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346676"
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez collecter un inventaire des applications installées sur des appareils mobiles. La liste des applications inventoriées varie selon que l'appareil appartient à l'entreprise ou à l'utilisateur. Pour les appareils personnels, les seules applications inventoriées sont celles qui sont gérées par Microsoft Intune.  

> [!NOTE]  
>  L’inventaire sur les applications installées sur les appareils mobiles est collecté dans le cadre du processus d’[inventaire matériel](mobile-device-hardware-inventory-hybrid.md).  

 Voici les applications inventoriées pour les appareils personnels ou d’entreprise.  

|Plate-forme|Pour les appareils personnels|Pour les appareils d’entreprise|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées|
|Windows 8.1 (sans client Configuration Manager)|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows Phone 8|Uniquement les applications gérées|Uniquement les applications gérées|  
|Windows RT|Uniquement les applications gérées|Uniquement les applications gérées|  
|iOS|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  
|Android|Uniquement les applications gérées|Toutes les applications installées sur l’appareil|  

Pour en savoir plus sur l’utilisation de l’inventaire logiciel pour collecter des informations sur les fichiers se trouvant sur les appareils des clients, voir [Présentation de l’inventaire logiciel](../../core/clients/manage/inventory/introduction-to-software-inventory.md) et [Comment configurer l’inventaire logiciel](../../core/clients/manage/inventory/configure-software-inventory.md).
