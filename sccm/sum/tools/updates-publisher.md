---
title: Éditeur de mise à jour
titleSuffix: Configuration Manager
description: Utiliser l’éditeur de mise à jour Center Updates pour gérer les mises à jour personnalisées
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 3a9c7758e394118041700192a393aff98f0d9087
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347329"
---
# <a name="system-center-updates-publisher"></a>Éditeur de mise à jour Systems Center

*S’applique à : l'éditeur de mise à jour System Center*

L’éditeur de mise à jour System Center est un outil autonome qui permet à des éditeurs de logiciels indépendants ou des développeurs d’applications métier de gérer les mises à jour personnalisées. Cela inclut les mises à jour qui comportent des dépendances, comme les pilotes et les offres groupées de mises à jour.

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


**Espace de travail Mises à jour :** utilisez cet espace de travail pour [créer](/sccm/sum/tools/create-updates-with-updates-publisher) et [gérer](/sccm/sum/tools/manage-updates-with-updates-publisher) les mises à jour logicielles et les offres groupées de mises à jour. Cela inclut l’affectation de mises à jour et d’offres groupées à une publication, ainsi que la publication et l’exportation vers le référentiel d’un autre éditeur de mise à jour.

**Espace de travail Publications :** c’est ici que vous [gérez vos publications](/sccm/sum/tools/updates-publisher-publications). Une publication est un groupe de mises à jour que vous créez pour simplifier l’exportation et la publication des mises à jour.

La gestion des publications inclut la publication des mises à jour sur un serveur afin que vos clients puissent les trouver et les installer, l’exportation de mises à jour et d’offres groupées à utiliser par d’autres installations de l’éditeur de mise à jour, ou la modification du contenu ou des détails d’une publication.



**Espace de travail Règles :** c’est ici que vous [gérez les règles de mise en application](/sccm/sum/tools/updates-publisher-applicability-rules) qui peuvent être enregistrées puis utilisées avec les mises à jour que vous déployez. Il existe deux types de règles:

-   Règles installables : ces règles permettent de déterminer si un client doit installer une mise à jour.
-   Règles installées : ces règles vérifient si une mise à jour est déjà installée.

**Espace de travail Catalogues :** utilisez cet espace de travail pour ajouter cet espace de travail et [gérer les catalogues de mises à jour logicielles](/sccm/sum/tools/updates-publisher-catalogs). Cela inclut l’importation des mises à jour logicielles de ces catalogues vers le référentiel de l’éditeur de mise à jour.
## <a name="first-steps"></a>Premières étapes
Pour commencer, [installez](/sccm/sum/tools/install-updates-publisher) puis [configurez les options](/sccm/sum/tools/updates-publisher-options) de l’éditeur de mise à jour.
