---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8305102657a5973c19ca161f65204587954b0232
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62231868"
---
Faire la distinction entre le pilote et de production, utilisez les définitions suivantes :  

- **Pilote** : Un sous-ensemble de vos appareils que vous souhaitez valider avant de déployer sur un ensemble plus important. Analytique de Desktop permet de marquer les appareils comme étant unique à l’ensemble de pilote. Appareils dans le pilote sont prêts à mettre à niveau lors du blocage d’aucune ressource. Une ressource de blocage est marquée comme *critique* et *impossible* pour mettre à niveau.  

- **Production** : Tous les autres appareils inscrits pour l’Analytique de bureau qui ne sont pas dans le pilote. Appareils de production sont prêts à mettre à niveau lorsque toutes les ressources sont approuvées. Postes de travail Analytique déconnecte automatiquement les ressources non critiques.  

