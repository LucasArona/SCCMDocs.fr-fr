---
title: Synchroniser à distance la stratégie sur des appareils inscrits auprès d’Intune
titleSuffix: Configuration Manager
description: Découvrir comment synchroniser la stratégie sur des appareils inscrits auprès d’Intune à partir de la console Configuration Manager
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3ecd2c480ab67a82539edff6daa18ef0f93628c6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Synchroniser à distance la stratégie sur des appareils inscrits auprès d’Intune à partir de la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous pouvez demander une synchronisation de la stratégie pour un appareil mobile inscrit auprès d’Intune à partir de la console Configuration Manager. Cela vous évite de devoir demander une synchronisation dans l’application Portail d’entreprise sur l’appareil. 

Pour cela :

1.  Sélectionnez un appareil sous **Actifs et Conformité** > **Vue d’ensemble** > **Appareils**.
2.  Cliquez sur **Envoyer une demande de synchronisation** dans le menu **Actions de l’appareil à distance**.


Au bout de cinq à dix minutes, toutes les modifications apportées à la stratégie sont synchronisées avec l’appareil. Vous pouvez afficher des informations sur l’état de la demande de synchronisation dans une nouvelle colonne des affichages d’appareil, appelée **État de la synchronisation à distance**, ainsi que dans la section des données de découverte de la boîte de dialogue **Propriétés** de chaque appareil.
