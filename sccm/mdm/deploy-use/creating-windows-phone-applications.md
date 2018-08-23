---
title: Créer des applications Windows Phone
titleSuffix: Configuration Manager
description: Commet créer et déployer des applications pour les appareils Windows Phone dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 77eb0b750934641ceb66b2c8aa611544c654f54f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385437"
---
# <a name="create-windows-phone-applications-in-configuration-manager"></a>Créer des applications Windows Phone dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application Configuration Manager propose un ou plusieurs types de déploiement. Le type de déploiement comprend les fichiers d’installation et les informations nécessaires pour déployer des logiciels sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

Pour connaître les étapes permettant de créer des types de déploiement et des applications Configuration Manager, consultez [Créer une application](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Gardez à l’esprit les considérations suivantes lorsque vous créez et déployez des applications pour des appareils Windows Phone :  


Configuration Manager prend en charge le déploiement des types de fichiers d’application suivants :  

|Type d'appareil|Types de fichiers pris en charge|  
|-----------------|---------------------|  
|Windows Phone 8|xap|  
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Déployez des applications Windows Phone comme **Disponible** ou **Obligatoire**. Utilisez aussi les déploiements pour désinstaller les applications.  
