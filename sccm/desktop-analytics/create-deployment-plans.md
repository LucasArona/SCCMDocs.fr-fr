---
title: Comment créer des plans de déploiement
titleSuffix: Configuration Manager
description: Guide pratique pour créer des plans de déploiement dans l’Analytique de bureau.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: dc94bf46630e2770385b5efaffb431135e3667c7
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67146040"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Comment créer des plans de déploiement dans Desktop Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Cet article fournit les étapes pour la création d’un plan de déploiement dans l’Analytique de bureau. Avant de commencer, tout d’abord [en savoir plus sur les plans de déploiement](/sccm/desktop-analytics/about-deployment-plans).

## <a name="create-a-plan-for-windows-10"></a>Créer un plan pour Windows 10

Suivez les étapes décrites dans cette section pour utiliser l’Analytique de bureau pour créer un plan pour le déploiement de Windows 10.

1. Ouvrez le [portail d’Analytique de bureau](https://aka.ms/desktopanalytics). Utilisez les informations d’identification qui disposent au moins **contributeurs de l’espace de travail** autorisations.  

2. Sélectionnez **Plans de déploiement** dans le groupe de gestion.  

3. Dans le **Plans de déploiement** volet, sélectionnez **créer**.  

4. Dans le **création du plan de déploiement** volet, configurez les paramètres suivants :  

    - **Nom** : Un nom unique pour le plan de déploiement  

    - **Produits et versions**: Choisir la version Windows 10 à déployer. Microsoft recommande de créer des plans de déploiement qui utilisent la version la plus récente.  

    - **Groupes d’appareils**: Sélectionnez un ou plusieurs groupes, puis **définir en tant que groupes cibles**. Groupes avec **SCCM** comme source sont collections synchronisées à partir du Gestionnaire de Configuration.  

    - **Règles de préparation**: Ces règles vous aide à déterminer quels appareils sont éligibles pour la mise à niveau. Pour plus d’informations, consultez [les règles de préparation](#readiness-rules).  

    - **Date de fin**: Choisissez la date à laquelle Windows doit être entièrement déployé à tous les appareils ciblés.  

5. Sélectionnez **créer**. Le nouveau plan s’affiche dans la liste des plans de déploiement lors de son traitement. Pour accélérer le traitement, demander une actualisation des données de la demande. Pour plus d’informations, consultez [Desktop Analytique FAQ](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Ouvrez le plan de déploiement en sélectionnant son nom.  

7. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier l’importance**.  

    1. Sur le **applications** onglet, sélectionnez cette option pour n’afficher que **pas été revues** actifs.  

    2. Sélectionnez chaque application, puis **modifier**. Vous pouvez sélectionner plusieurs applications à modifier en même temps.  

    3. Choisissez un niveau d’importance dans le **Importance** liste. Si vous souhaitez Analytique de bureau pour valider l’application pendant la phase pilote, sélectionnez **critique** ou **Important**. Il ne valide pas les applications marquées en tant que **pas Important**. Évaluer son [compatibilité](/sccm/desktop-analytics/compat-assessment) et d’autres informations de plan lors de l’affectation de niveaux d’importance.  

        Lorsque vous affectez des niveaux d’importance, vous pouvez également choisir la décision de mise à niveau.  

    4. Sélectionnez **enregistrer** lorsque vous avez terminé.  

8. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier pilote**.  

    1. Passez en revue les appareils recommandées pour le projet pilote.  

    2. Sélectionnez chaque appareil, puis **ajouter pilote**. Si vous êtes en désaccord avec la recommandation, sélectionnez **remplacer**.  

        Pour plus d’informations sur comment Desktop Analytique rend ces recommandations, sélectionnez l’icône d’information dans l’angle supérieur droit de la **identifier pilote** volet.

## <a name="readiness-rules"></a>Règles de préparation

Ces règles vous permettent de déterminer les appareils qui sont éligibles pour la mise à niveau sur place. Vous pouvez définir ces règles lorsque vous créez le plan de déploiement, ou les modifiez ultérieurement.

Pour modifier les règles de préparation :

1. Dans le portail d’Analytique de bureau, sélectionnez le plan de déploiement.
1. En regard du nom, sélectionnez **modifier**.
1. Sélectionnez **les règles de préparation**.
1. Sélectionnez **Windows du système d’exploitation**.
1. Apportez les modifications nécessaires, puis sélectionnez **enregistrer**.

Pour **système d’exploitation Windows** mises à niveau, il existe deux règles disponibles : Pilotes de périphériques et les applications Windows.

### <a name="device-drivers"></a>Pilotes d'appareils

Déterminer si vos appareils obtiennent des pilotes à partir de Windows Update. Cette valeur est **hors** par défaut. Activez cette règle lorsque vous utilisez la mise à jour de Windows pour les entreprises pour gérer les mises à jour, y compris les pilotes. Si vous utilisez Configuration Manager pour gérer les mises à jour logicielles, la valeur est cette règle **hors**.

### <a name="windows-applications"></a>Applications Windows

Les applications de bureau Analytique avec la mention *dignes d’intérêt* sont basées sur le seuil du nombre faible d’installation. Définissez ce seuil dans les règles de préparation pour le plan de déploiement. Par défaut, ce seuil est **2.0 %** . Vous pouvez modifier la valeur de `0.0` à `10.0`.


## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour déployer sur des appareils de pilotes.
> [!div class="nextstepaction"]  
> [Déploiement pilote](/sccm/desktop-analytics/deploy-pilot)  
