---
title: Plans de déploiement dans l’Analytique de bureau
titleSuffix: Configuration Manager
description: En savoir plus sur les plans de déploiement dans l’Analytique de bureau.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce726ffa0dfc8a46bd0891e50ff087ad4931d901
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62243356"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>À propos des plans de déploiement dans l’Analytique de bureau 

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Postes de travail Analytique collecte et analyse des données de périphérique, l’application et pilote dans votre organisation. En fonction de cette analyse et de votre entrée, vous pouvez utiliser le service pour créer des plans de déploiement pour Windows 10 et Office 365 ProPlus. Les plans de déploiement comprennent les fonctionnalités suivantes :  

- Recommandez automatiquement les périphériques à inclure dans les pilotes  

- Identifier les problèmes de compatibilité et suggère des solutions d’atténuation  

- Évaluer l’intégrité du déploiement avant, pendant et après les mises à jour  

- Suivre la progression de votre déploiement  


Dans le cadre de votre plan de déploiement, vous effectuez les actions suivantes :  

 - Définissez les produits et les versions que vous souhaitez déployer : Windows 10, Office 365 ProPlus, ou les deux  

 - Choisissez les groupes de périphériques vers lequel vous souhaitez déployer  

 - Créer des règles de préparation pour le déploiement  

 - Définir l’importance de vos applications et les compléments Office  

 - Choisissez pilotes appareils selon les recommandations automatique  

 - Décider comment résoudre les problèmes avec les applications et les compléments Office selon les recommandations à partir de l’Analytique de bureau  


Analytique bureau actualise les données de plan de déploiement de tous les jours. Les modifications que vous apportez peuvent ne pas apparaîtront pendant 24 heures. Ces modifications incluent l’affectation d’importance à une application, ou en choisissant un appareil à inclure dans un projet pilote.  

Si vous vous connectez Desktop Analytique à Configuration Manager, sélectionnez vos collections dans les plans de déploiement. Puis cette intégration vous permet de déployer Windows ou Office à un regroupement basé sur les données d’Analytique de bureau. 

Si vous n’utilisez pas le Gestionnaire de Configuration, vous pouvez créer des groupes dans le journal Analytique. Pour plus d’informations, consultez [recherches dans les journaux des groupes d’ordinateurs dans le journal Analytique](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups). 



## <a name="readiness-rules"></a>Règles de préparation

Les règles de préparation suivantes sont disponibles dans les plans de déploiement :

- Si vos appareils reçoivent automatiquement les pilotes à partir de Windows Update. Si les appareils reçoivent les mises à jour de pilote à partir de Windows Update, puis tous les problèmes de pilote identifiés dans le cadre de l’évaluation de la disponibilité sont automatiquement marquées comme **prêt**.  

- Faible installer seuil du nombre de vos applications Windows. Si une application est installée sur un pourcentage plus élevé d’ordinateurs à ce seuil, le plan de déploiement marque l’application en tant que **Noteworthy**. Cette balise signifie que vous pouvez décider combien il est important de tester pendant la phase pilote.  

- Mettre à jour Office 365 ProPlus à partir de 32 bits à 64 bits sur les appareils qui ont une version 64 bits de Windows. Ce comportement est la valeur par défaut.  

- Lors de la mise à jour à partir d’une version antérieure d’Office, laissez les applications Office plus anciennes, même si ces applications n’existent pas dans la version la plus récente de Microsoft Office. Ce comportement n’est pas sur par défaut.  

- Faible installer seuil du nombre de vos compléments Office. Le seuil par défaut est `2%`. Compléments sous ce seuil sont automatiquement définis pour *faible nombre d’installations*. Analytique de bureau ne valide pas ces compléments pendant la phase pilote. 

    Si un complément est installé sur un pourcentage plus élevé d’ordinateurs à ce seuil, le plan de déploiement marque le complément en tant que *Noteworthy*. Vous pouvez ensuite son importance pour tester pendant la phase pilote.   



## <a name="importance"></a>importance

Dans le cadre du plan de déploiement, définissez la *importance* des applications et des compléments Office. Postes de travail Analytique détecte ces applications comme étant installé sur les appareils cibles. Ce paramètre permet de déterminer quels sont les appareils qu’elle contient dans la phase pilote du déploiement Analytique de bureau. 

Si une application ou un complément est installé sur moins de 2 % des périphériques ciblés, elle est marquée **faible nombre d’installations**. Pourcentage de deux est la valeur par défaut. Vous pouvez ajuster le seuil dans les paramètres de préparation de 0 % à 10 %. Postes de travail Analytique marque automatiquement ces applications et les compléments en tant que **prêt à mettre à niveau**.  

Pour les applications et des compléments, choisissez une importance de **critique**, **Important**, ou **pas important**. Si vous marquez un comme critiques ou importantes, Analytique de bureau inclut dans le déploiement pilote certains périphériques avec l’application ou le complément. Le service inclut dans le pilote des instances d’une application critique ou d’un complément. Si vous marquez une application ou le complément n’est pas important, bureau Analytique lui donne automatiquement **prêt à mettre à niveau**.



## <a name="pilot-devices"></a>Appareils de pilote

Postes de travail Analytique combine vos informations d’importance avec les paramètres globaux de pilotes. Il crée ensuite une recommandation pour lequel les appareils doivent faire partie du déploiement pilote. Le déploiement pilote recommandé inclut des appareils avec différentes configurations matérielles et une ou plusieurs instances de toutes les applications critiques et importantes. Si une application est marquée comme critique, le service recommande plus d’appareils avec cette application dans le pilote.



## <a name="deployment-plans-in-configuration-manager"></a>Plans de déploiement dans Configuration Manager

Après avoir créé un plan de déploiement, utilisez Configuration Manager pour déployer les produits. Une fois le démarrage du déploiement, postes de travail Analytique surveille le déploiement en fonction des paramètres dans le plan.

<!--more on deployment plans in SCCM-->

<!-- test comment-->

## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur les ressources de bureau Analytique](/sccm/desktop-analytics/about-assets): périphériques, applications, les applications Office, des compléments Office et les macros Office  

- [En savoir plus sur les mises à jour de sécurité et de fonctionnalité](/sccm/desktop-analytics/about-updates)  

- [Créer un plan de déploiement](/sccm/desktop-analytics/create-deployment-plans)  

