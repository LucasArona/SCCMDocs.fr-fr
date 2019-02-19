---
title: Bonnes pratiques pour les regroupements
titleSuffix: Configuration Manager
description: Obtenir les bonnes pratiques pour les regroupements dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c685cf4efd5eca5f93694edd4a01715120df9a8
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140573"
---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Pratiques recommandées pour les regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les bonnes pratiques suivantes pour les regroupements dans System Center Configuration Manager.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>N'utilisez pas de mises à jour incrémentielles pour un grand nombre de regroupements.  
 Lorsque vous activez l'option **Utiliser des mises à jour incrémentielles pour ce regroupement** , cette configuration peut entraîner des retards d'évaluation si vous l'activez pour de nombreux regroupements. Le seuil s’élève à environ 200 regroupements dans votre hiérarchie. Le nombre exact dépend des facteurs suivants :  

-   Nombre total de regroupements  

-   Fréquence d'ajout et de modification de ressources dans la hiérarchie  

-   Nombre de clients dans la hiérarchie  

-   Complexité des règles d'appartenance de regroupement dans la hiérarchie  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Assurez-vous que les fenêtres de maintenance sont assez grandes pour déployer des mises à jour logicielles critiques  
 Vous pouvez configurer des fenêtres de maintenance pour les regroupements d'appareils afin de limiter les périodes où Configuration Manager peut installer des logiciels sur ces appareils. Si vous configurez une fenêtre de maintenance trop petite, le client peut ne pas installer les mises à jour logicielles critiques et se retrouver vulnérable à l'attaque qui aurait été contrée par la mise à jour logicielle.  
