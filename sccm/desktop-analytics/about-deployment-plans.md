---
title: Plans de déploiement dans l’Analytique de bureau
titleSuffix: Configuration Manager
description: En savoir plus sur les plans de déploiement dans l’Analytique de bureau.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91cd7fc450ee53f900ae890e3a698c26c789ba8c
ms.sourcegitcommit: 4023fb6fb534d8a0d589c8208f021e3311c7167f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64880582"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>À propos des plans de déploiement dans l’Analytique de bureau

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Postes de travail Analytique collecte et analyse des données de périphérique, l’application et pilote dans votre organisation. En fonction de cette analyse et de votre entrée, vous pouvez utiliser le service pour créer des plans de déploiement pour Windows 10. Les plans de déploiement comprennent les fonctionnalités suivantes :  

- Recommandez automatiquement les périphériques à inclure dans les pilotes  

- Identifier les problèmes de compatibilité et suggère des solutions d’atténuation  

- Évaluer l’intégrité du déploiement avant, pendant et après les mises à jour  

- Suivre la progression de votre déploiement  

Dans le cadre de votre plan de déploiement, vous effectuez les actions suivantes :  

- Définir quelles versions de Windows 10 que vous souhaitez déployer  

- Choisissez les groupes de périphériques vers lequel vous souhaitez déployer  

- Créer des règles de préparation pour le déploiement  

- Définir l’importance de vos applications  

- Choisissez pilotes appareils selon les recommandations automatique  

- Décider comment résoudre les problèmes avec les applications basées sur les recommandations d’Analytique de bureau  

Analytique bureau actualise les données de plan de déploiement de tous les jours. Les modifications que vous apportez peuvent ne pas apparaîtront pendant 24 heures. Ces modifications incluent l’affectation d’importance à une application, ou en choisissant un appareil à inclure dans un projet pilote.  

Après avoir connecté le bureau Analytique à Configuration Manager, sélectionnez vos collections dans les plans de déploiement. Puis cette intégration vous permet de déployer Windows sur un regroupement basé sur les données d’Analytique de bureau.

Alors que le bureau Analytique fonctionne mieux avec les collections de Configuration Manager, vous pouvez également créer des groupes d’appareils dans le journal Analytique. Pour plus d’informations, consultez [recherches dans les journaux des groupes d’ordinateurs dans le journal Analytique](https://docs.microsoft.com/azure/log-analytics/log-analytics-computer-groups).



## <a name="readiness-rules"></a>Règles de préparation

Les règles de préparation suivantes sont disponibles dans les plans de déploiement :

- Si vos appareils reçoivent automatiquement les pilotes à partir de Windows Update. Si les appareils reçoivent les mises à jour de pilote à partir de Windows Update, puis tous les problèmes de pilote identifiés dans le cadre de l’évaluation de la disponibilité sont automatiquement marquées comme **prêt**.  

- Faible installer seuil du nombre de vos applications Windows. Si une application est installée sur un pourcentage plus élevé d’ordinateurs à ce seuil, le plan de déploiement marque l’application en tant que **Noteworthy**. Cette balise signifie que vous pouvez décider combien il est important de tester pendant la phase pilote.  



## <a name="importance"></a>importance

Dans le cadre du plan de déploiement, définissez la *importance* des applications. Postes de travail Analytique détecte ces applications comme étant installé sur les appareils cibles. Ce paramètre permet de déterminer quels sont les appareils qu’elle contient dans la phase pilote du déploiement Analytique de bureau.

Si une application est installée sur moins de 2 % des périphériques ciblés, elle est marquée **faible nombre d’installations**. Pourcentage de deux est la valeur par défaut. Vous pouvez ajuster le seuil dans les paramètres de préparation de 0 % à 10 %. Postes de travail Analytique marque automatiquement ces applications en tant que **prêt à mettre à niveau**.  

Pour les applications, choisissez une importance de **critique**, **Important**, ou **pas important**. Si vous marquez un comme critiques ou importantes, Analytique de bureau inclut dans le déploiement pilote certains périphériques avec cette application. Il inclut le service dans le pilote plusieurs instances d’une application critique. Si vous marquez une application n’est pas important, bureau Analytique lui donne automatiquement **prêt à mettre à niveau**.



## <a name="pilot-devices"></a>Appareils de pilote

Postes de travail Analytique combine vos informations d’importance avec les paramètres globaux de pilotes. Il crée ensuite une recommandation pour lequel les appareils doivent faire partie du déploiement pilote. Le déploiement pilote recommandé inclut des appareils avec différentes configurations matérielles et une ou plusieurs instances de toutes les applications critiques et importantes. Si une application est marquée comme critique, le service recommande plus d’appareils avec cette application dans le pilote.



## <a name="deployment-plans-in-configuration-manager"></a>Plans de déploiement dans Configuration Manager

Après avoir créé un plan de déploiement, utilisez Configuration Manager pour déployer les produits. Une fois le démarrage du déploiement, postes de travail Analytique surveille le déploiement en fonction des paramètres dans le plan.


## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur les ressources de bureau Analytique](/sccm/desktop-analytics/about-assets): appareils, des pilotes et des applications  

- [En savoir plus sur les mises à jour de sécurité et de fonctionnalité](/sccm/desktop-analytics/about-updates)  

- [Créer un plan de déploiement](/sccm/desktop-analytics/create-deployment-plans)  
