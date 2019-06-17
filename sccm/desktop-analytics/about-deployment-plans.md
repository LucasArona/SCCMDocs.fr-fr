---
title: Plans de déploiement dans l’Analytique de bureau
titleSuffix: Configuration Manager
description: En savoir plus sur les plans de déploiement dans l’Analytique de bureau.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8080d89995b6ed10efd996b4ad757151e315c74
ms.sourcegitcommit: af207075c4a8bc59242a41d3192a4057452a0e55
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141032"
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

Par défaut, Analytique de bureau actualise quotidiennement les données de plan de déploiement. Toute modification apportée au sein d’un plan de déploiement, telles que l’affectation d’importance à une application ou en choisissant un appareil à inclure dans un programme pilote, prend jusqu'à 24 heures à traiter. Pour accélérer ce processus, demander une actualisation des données de la demande. Pour plus d’informations, consultez [Desktop Analytique FAQ](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Après avoir connecté le bureau Analytique à Configuration Manager, sélectionnez vos collections dans les plans de déploiement. Puis cette intégration vous permet de déployer Windows sur un regroupement basé sur les données d’Analytique de bureau.



## <a name="readiness-rules"></a>Règles de préparation

Les règles de préparation suivantes sont disponibles dans les plans de déploiement :

- Si vos appareils reçoivent automatiquement les pilotes à partir de Windows Update. Si les appareils reçoivent les mises à jour de pilote à partir de Windows Update, puis tous les problèmes de pilote identifiés dans le cadre de l’évaluation de la disponibilité sont automatiquement marquées comme **prêt**.  

- Faible installer seuil du nombre de vos applications Windows. Si une application est installée sur un pourcentage plus élevé d’ordinateurs à ce seuil, le plan de déploiement marque l’application en tant que **Noteworthy**. Cette balise signifie que vous pouvez décider combien il est important de tester pendant la phase pilote.  


## <a name="plan-assets"></a>Plan de ressources

<!-- 4670224 -->

Alors que le [actifs](/sccm/desktop-analytics/about-assets) zone montre également les appareils et les applications, le **actifs du régime** zone sous un plan de déploiement spécifique inclut des informations supplémentaires.

### <a name="devices"></a>Appareils

Consultez le **Windows mise à niveau de la décision** pour chaque appareil dans le plan de déploiement.

Les Windows mise à niveau la décision de **appareil de remplacement** peut être dû à l’une des raisons suivantes :

- Il a échoué d’une vérification de processeur de Windows 10 est requis. Pour plus d’informations, consultez [la configuration matérielle minimale](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Il a un bloc de BIOS
- Il n’a pas suffisamment de mémoire
- Un composant critique de démarrage sur le système dispose d’un pilote bloqué
- La marque et le modèle ne peut pas mettre à niveau
- Il existe un composant de la classe d’affichage avec un bloc de pilote qui a tous les attributs suivants :
    - Vous ne substituez pas
    - Aucun pilote n’est présent dans la nouvelle version du système d’exploitation
    - Il n’est pas déjà sur la mise à jour de Windows
- Il existe un autre composant plug-and-play sur le système qui bloque la mise à niveau
- Il existe un composant sans fil qui utilise un pilote émulé XP
- Un composant réseau avec une connexion active va perdre son pilote. En d’autres termes, après mise à niveau elle pourrait perdre sa connectivité réseau.

### <a name="apps"></a>Applications

Définir le **mise à niveau de la décision** ainsi que le **Importance** pour cette application dans ce plan de déploiement. Pour plus d’informations, consultez [comment créer des plans de déploiement](/sccm/desktop-analytics/create-deployment-plans).

Dans les détails de l’application, vous pouvez également voir les informations suivantes : Recommandations, les facteurs de risque de compatibilité et problèmes connus de Microsoft. Utilisez ces informations pour aider à ensemble la **mise à niveau de la décision**. Pour plus d’informations, consultez [évaluation de la compatibilité](/sccm/desktop-analytics/compat-assessment).

Les applications de bureau Analytique montre comme *dignes d’intérêt* sont basées sur le seuil du nombre faible d’installation pour les règles de préparation du plan de déploiement. Pour plus d’informations, consultez [les règles de préparation](/sccm/desktop-analytics/create-deployment-plans#readiness-rules).

### <a name="drivers"></a>Pilotes

Afficher la liste des pilotes inclus dans ce plan de déploiement. Définir le **mise à niveau de la décision**, passez en revue la recommandation de Microsoft et découvrez les facteurs de risque de compatibilité.


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
