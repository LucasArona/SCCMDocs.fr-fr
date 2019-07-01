---
title: Éditeur de mise à jour
titleSuffix: Configuration Manager
description: Utiliser l’éditeur de mise à jour Center Updates pour gérer les mises à jour personnalisées
ms.date: 6/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26ad3be032a3dd8ea21d7eeb6a4755c32d546f38
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158660"
---
# <a name="system-center-updates-publisher"></a>Éditeur de mise à jour Systems Center

*S’applique à : l'éditeur de mise à jour System Center*

L’éditeur de mise à jour System Center (SCUP) est un outil autonome qui permet aux éditeurs de logiciels indépendants ou aux développeurs d’applications métier de gérer les mises à jour personnalisées. Cette gestion des mises à jour personnalisées inclut des mises à jour qui ont des dépendances, comme les pilotes et mises à jour.

À l’aide de l’éditeur de mise à jour, vous pouvez :

-   Importer des mises à jour à partir de catalogues externes (catalogues de mises à jour non-Microsoft).
-   Modifier des définitions de mise à jour, y compris la mise en application, et les métadonnées de déploiement.
-   Exporter les mises à jour vers des catalogues externes.
-   Publier les mises à jour sur un serveur de mise à jour.

Une fois que vous publiez des mises à jour sur un serveur de mise à jour, vous pouvez ensuite utiliser System Center Configuration Manager pour détecter et déployer ces mises à jour sur vos appareils gérés.

> [!TIP]  
> La version précédente, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), reste prise en charge. Cette version mise à jour conserve les mêmes fonctionnalités, mais elle prend en charge d’autres systèmes d’exploitation, de nouvelles fonctionnalités pour simplifier certaines tâches, et propose une nouvelle interface utilisateur.

## <a name="workspaces"></a>Espaces de travail
Lorsque vous ouvrez l’éditeur de mise à jour, il affiche par défaut le nœud Vue d’ensemble de l *’espace de travail Mises à jour.*

![Console de l’éditeur de mise à jour](media/console1.png)   


L’éditeur de mise à jour comporte quatre espaces de travail qui facilitent son utilisation.


**Espace de travail Mises à jour :** utilisez cet espace de travail pour [créer](/sccm/sum/tools/create-updates-with-updates-publisher) et [gérer](/sccm/sum/tools/manage-updates-with-updates-publisher) les mises à jour logicielles et les offres groupées de mises à jour. Cet espace de travail inclut l’affectation de mises à jour et d’offres groupées à une publication, ainsi que la publication et l’exportation vers le référentiel d’un autre éditeur de mise à jour.

**Espace de travail Publications :** c’est dans cet espace de travail que vous [gérez vos publications](/sccm/sum/tools/updates-publisher-publications). Une publication est un groupe de mises à jour que vous créez pour simplifier l’exportation et la publication des mises à jour.

La gestion des publications inclut la publication des mises à jour sur un serveur afin que vos clients puissent les trouver et les installer, l’exportation de mises à jour et d’offres groupées à utiliser par d’autres installations de l’éditeur de mise à jour, ou la modification du contenu ou des détails d’une publication.

**Espace de travail Règles :** c’est ici que vous [gérez les règles de mise en application](/sccm/sum/tools/updates-publisher-applicability-rules) qui peuvent être enregistrées puis utilisées avec les mises à jour que vous déployez. Il existe deux types de règles:

-   Règles installables : ces règles permettent de déterminer si un client doit installer une mise à jour.
-   Règles installées : ces règles vérifient si une mise à jour est déjà installée.

**Espace de travail Catalogues :** utilisez cet espace de travail pour ajouter cet espace de travail et [gérer les catalogues de mises à jour logicielles](/sccm/sum/tools/updates-publisher-catalogs). Cet espace de travail inclut l’importation des mises à jour logicielles de ces catalogues vers le référentiel de l’éditeur de mise à jour.

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>Quelles sont les nouveautés dans la version préliminaire de System Center Updates Publisher

>[!NOTE] 
>Les informations contenues dans cette section s’applique uniquement à la version préliminaire de System Center Updates publisher. Pour installer la version préliminaire, téléchargez-le à partir de la [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=58390).

Il est un nouveau mode de création dans la version préliminaire de System Center Updates Publisher pour vous aider à créer vos mises à jour. Lorsque vous activez le mode Création, un **espace de travail de catégories** est ajouté à l’écran d’accueil. Un nouveau **détection** bouton est également ajouté à la **espace de travail mises à jour** lorsque le mode de création est activé. 

### <a name="to-enable-authoring-mode-in-the-preview"></a>Pour activer le mode Création dans la version préliminaire

1. Dans le coin supérieur gauche de la console, cliquez sur le **Updates Publisher** **propriétés** onglet, puis choisissez **Options**.
1. Accédez à la **Authoring** options.
1. Cochez la case **activer le mode de création**.

![Activer le mode Création pour le serveur de publication de mises à jour](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>À propos de l’espace de travail de catégories

L’espace de travail de catégories permet aux auteurs de mise à jour organiser les mises à jour qui vont ensemble. Par exemple, si vous êtes un fabricant OEM, vous pouvez organiser vos mises à jour en fonction des modèles ou des gammes de produits. Vous pouvez définir plusieurs catégories et catégories enfants mais catégories pas général enfant en tant que vous êtes limités à deux niveaux.

![Capture d’écran de l’espace de travail de catégories](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Affecter une mise à jour à une catégorie

Une fois que vous avez créé votre mise à jour, vous pouvez l’affecter à une catégorie en sélectionnant la mise à jour puis en cliquant sur le **classer** bouton. Vous pouvez également avec le bouton droit de la mise à jour et sélectionnez **classer**.

![Capture d’écran de classement d’une mise à jour](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>À propos des detectoids

Une fois que le mode de création est activé, vous pouvez créer des detectoids des mises à jour. Les Detectoids sont utiles lorsque vous avez plusieurs mises à jour qui utilisent la même règle (ou un ensemble de règles) pour déterminer la mise en application. Dans ce cas, vous créeriez une détection et attribuez-lui comme condition préalable pour une mise à jour. Vous pouvez affecter plusieurs detectoids à une mise à jour créé.


### <a name="create-a-detectoid"></a>Créer une détection

1. Ouvrez l'**espace de travail Mises à jour**.
1. Dans le ruban, cliquez sur le **détection** bouton.
1. Suivez les invites de l’Assistant pour créer votre détection.



![Mettre à jour les conditions préalables à l’aide d’une détection](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>Étapes suivantes
Pour commencer, [installez](/sccm/sum/tools/install-updates-publisher) puis [configurez les options](/sccm/sum/tools/updates-publisher-options) de l’éditeur de mise à jour.
