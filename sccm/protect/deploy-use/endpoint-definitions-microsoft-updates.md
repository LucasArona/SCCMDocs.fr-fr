---
title: Définitions de programmes malveillants Endpoint Protection à partir d’un partage réseau
titleSuffix: Configuration Manager
description: Apprenez à activer le téléchargement des définitions de programmes malveillants Endpoint Protection à partir de Microsoft Updates pour Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee1734178e3225aaf25a8105d83d9c0315866283
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122183"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Activer le téléchargement des définitions de programmes malveillants Endpoint Protection à partir de Microsoft Updates pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Quand vous choisissez de télécharger des mises à jour de définition à partir de Microsoft Update, les clients vérifient le site Microsoft Update à l’intervalle défini dans la section **Mises à jour de définitions** de la boîte de dialogue Stratégie de logiciel anti-programme malveillant.

 Cette méthode peut être utile quand le client ne dispose pas de connectivité au site Configuration Manager ou que vous voulez permettre aux utilisateurs de lancer des mises à jour de définitions.

> [!IMPORTANT]
>  Les clients doivent avoir accès à Microsoft Update sur Internet pour pouvoir utiliser cette méthode de téléchargement des mises à jour de définitions.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Utilisation du Centre de protection Microsoft contre les programmes malveillants pour télécharger des définitions
 Vous pouvez configurer les clients pour télécharger les mises à jour de définitions à partir du Centre de protection Microsoft contre les programmes malveillants. Cette option est utilisée par les clients Endpoint Protection pour télécharger les mises à jour de définitions s’ils n’ont pas pu les télécharger à partir d’une autre source. Cette méthode de mise à jour peut être utile si un problème détecté au niveau de votre infrastructure Configuration Manager empêche la remise des mises à jour.

> [!IMPORTANT]
>  Les clients doivent avoir accès à Microsoft Update sur Internet pour pouvoir utiliser cette méthode de téléchargement des mises à jour de définition.
> 
> 
> [!div class="button"]
> [Étape suivante >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Retour >](endpoint-configure-alerts.md)
