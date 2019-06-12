---
title: Comment créer des plans de déploiement
titleSuffix: Configuration Manager
description: Guide pratique pour créer des plans de déploiement dans l’Analytique de bureau.
ms.date: 06/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b65a700f5c9cdf3225dfb2ecd3c48d76119110f2
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834925"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Comment créer des plans de déploiement dans Desktop Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Cet article fournit les étapes pour la création d’un plan de déploiement dans l’Analytique de bureau. Avant de commencer, tout d’abord [en savoir plus sur les plans de déploiement](/sccm/desktop-analytics/about-deployment-plans).

Suivez les étapes décrites dans cet article pour utiliser l’Analytique de bureau pour créer un plan pour le déploiement de Windows 10.

1. Ouvrez le [portail d’Analytique de bureau](https://aka.ms/m365aprod). Utilisez les informations d’identification qui disposent au moins **contributeurs de l’espace de travail** autorisations.  

2. Sélectionnez **Plans de déploiement** dans le groupe de gestion.  

3. Dans le **Plans de déploiement** volet, sélectionnez **créer**.  

4. Dans le **création du plan de déploiement** volet, configurez les paramètres suivants :  

    - **Nom** : Un nom unique pour le plan de déploiement  

    - **Produits et versions**: Choisir la version Windows 10 à déployer. Microsoft recommande de créer des plans de déploiement qui utilisent la version la plus récente.  

    - **Groupes d’appareils**: Sélectionnez un ou plusieurs groupes, puis **définir en tant que groupes cibles**. Groupes avec **SCCM** comme source sont collections synchronisées à partir du Gestionnaire de Configuration.  

    - **Règles de préparation**: Ces règles vous aide à déterminer quels appareils sont éligibles pour la mise à niveau.  

    - **Date de fin**: Choisissez la date à laquelle Windows doit être entièrement déployé à tous les appareils ciblés.  

5. Sélectionnez **créer**. Le nouveau plan s’affiche dans la liste des plans de déploiement lors de son traitement. Pour accélérer le traitement, demander une actualisation des données de la demande. Pour plus d’informations, consultez [Desktop Analytique FAQ](/sccm/desktop-analytics/faq##can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Ouvrez le plan de déploiement en sélectionnant son nom.  

7. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier l’importance**.  

    1. Sur le **applications** onglet, sélectionnez cette option pour n’afficher que **pas été revues** actifs.  

    2. Sélectionnez chaque application, puis **modifier**. Vous pouvez sélectionner plusieurs applications à modifier en même temps.  

    3. Choisissez un niveau d’importance dans le **Importance** liste. Si vous souhaitez Analytique de bureau pour valider l’application pendant la phase pilote, sélectionnez **critique** ou **Important**. Il ne valide pas les applications marquées en tant que **pas Important**. Prendre en compte la [risque de compatibilité](/sccm/desktop-analytics/compat-risk) et d’autres informations de plan lors de l’affectation de niveaux d’importance.  

        Lorsque vous affectez des niveaux d’importance, vous pouvez également choisir la décision de mise à niveau.  

    4. Sélectionnez **enregistrer** lorsque vous avez terminé.  

8. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier pilote**.  

    1. Passez en revue les appareils recommandées pour le projet pilote.  

    2. Sélectionnez chaque appareil, puis **ajouter pilote**. Si vous êtes en désaccord avec la recommandation, sélectionnez **remplacer**.  

        Pour plus d’informations sur comment Desktop Analytique rend ces recommandations, sélectionnez l’icône d’information dans l’angle supérieur droit de la **identifier pilote** volet.



### <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour déployer sur des appareils de pilotes.
> [!div class="nextstepaction"]  
> [Déploiement pilote](/sccm/desktop-analytics/deploy-pilot)  
