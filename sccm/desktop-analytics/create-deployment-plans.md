---
title: Comment créer des plans de déploiement
titleSuffix: Configuration Manager
description: Guide pratique pour créer des plans de déploiement dans l’Analytique de bureau.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4b56fac3060acc16fe46221464ddc6535b478399
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754880"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Comment créer des plans de déploiement dans Desktop Analytique 

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Cet article fournit les étapes pour la création d’un plan de déploiement dans l’Analytique de bureau. Avant de commencer, tout d’abord [en savoir plus sur les plans de déploiement](/sccm/desktop-analytics/about-deployment-plans).

Suivez les étapes décrites dans cet article pour utiliser l’Analytique de bureau pour créer un plan pour le déploiement de Windows 10 et Office 365 ProPlus. Créer des plans de déploiement pour Windows 10, Office 365 ProPlus ou les deux.

1. Ouvrez le [portail d’Analytique de bureau](https://aka.ms/m365aprod). Utilisez les informations d’identification qui disposent au moins **contributeurs de l’espace de travail** autorisations.  

2. Sélectionnez **Plans de déploiement** dans le groupe de gestion.  

3. Dans le **Plans de déploiement** volet, sélectionnez **créer**.  

4. Dans le **création du plan de déploiement** volet, configurez les paramètres suivants :  

    - **Nom** : Un nom unique pour le plan de déploiement  

    - **Produits et versions**: Choisissez les produits et les versions à déployer. Microsoft recommande la création de plans de déploiement pour Office et Windows ensemble et à l’aide des versions les plus récentes.  

    - **Groupes d’appareils**: Sélectionnez un ou plusieurs groupes, puis **définir en tant que groupes cibles**. Groupes avec **SCCM** comme source sont collections synchronisées à partir du Gestionnaire de Configuration.  

    - **Règles de préparation**: Ces règles vous aide à déterminer quels appareils sont éligibles pour la mise à niveau. 

    - **Date de fin**: Choisissez la date à laquelle Windows et Office doivent être entièrement déployée sur tous les appareils ciblés.  

5. Sélectionnez **créer**. Le nouveau plan s’affiche dans la liste des plans de déploiement lors de son traitement. Le traitement peut prendre jusqu'à 48 heures avant de procéder à l’étape suivante.   

6. Ouvrez le plan de déploiement en sélectionnant son nom.  

7. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier l’importance**.  

    1. Sur le **applications** onglet, sélectionnez cette option pour n’afficher que **pas été revues** actifs.  

    2. Sélectionnez chaque application, puis **modifier**. Vous pouvez sélectionner plusieurs applications à modifier en même temps.   

    3. Choisissez un niveau d’importance dans le **Importance** liste. Si vous souhaitez Analytique de bureau pour valider le complément pendant la phase pilote, sélectionnez **critique** ou **Important**. Il ne valide pas les compléments marqués comme **pas Important**. Prendre en compte les risques de compatibilité et d’autres informations de plan lors de l’affectation de niveaux d’importance.  

        Lorsque vous affectez des niveaux d’importance, vous pouvez également choisir la décision de mise à niveau.  

    4. Sélectionnez **enregistrer** lorsque vous avez terminé.  

    5. Répétez ces étapes pour le **des compléments Office**.  

8. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier pilote**.  

    1. Passez en revue les appareils recommandées pour le projet pilote.  

    2. Sélectionnez chaque appareil, puis **ajouter pilote**. Si vous êtes en désaccord avec la recommandation, sélectionnez **remplacer**.  

        Pour plus d’informations sur comment Desktop Analytique rend ces recommandations, sélectionnez l’icône d’information dans l’angle supérieur droit de la **identifier pilote** volet.



### <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour déployer sur des appareils de pilotes.
> [!div class="nextstepaction"]  
> [Déploiement pilote](/sccm/desktop-analytics/deploy-pilot)  
