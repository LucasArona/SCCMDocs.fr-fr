---
title: Icônes utilisées pour les mises à jour logicielles
titleSuffix: Configuration Manager
description: La console Configuration Manager contient des icônes qui indiquent un état pour la mise à jour ou le groupe de mises à jour logicielles synchronisés.
author: aczechowski
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
ms.author: aaroncz
ms.openlocfilehash: 77c6772682c8eb6d1532c0ea38489a45d2466c30
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422859"
---
# <a name="icons-used-for-software-updates-in-system-center-configuration-manager"></a>Icônes utilisées pour les mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les mises à jour logicielles synchronisées sont affichées dans la console Configuration Manager, où la première colonne de chaque mise à jour logicielle contient une icône indiquant un état spécifique. Les groupes de mises à jour logicielles sont également représentés par une icône qui fournit des informations sur l’état des mises à jour logicielles contenues dans chaque groupe. Cette section fournit des informations sur les icônes des mises à jour logicielles et sur la signification de chaque icône.  

## <a name="icons-for-software-updates"></a>Icônes des mises à jour logicielles  
 Les mises à jour logicielles synchronisées sont représentées par une des icônes suivantes.  

### <a name="normal-icon"></a>Icône Normale  
 ![icône](../media/Normal.jpg "Icône Normale") L’icône avec la flèche verte représente une mise à jour logicielle normale.  

 **Description :**  

 Les mises à jour normales ont été synchronisées et sont disponibles pour le déploiement logiciel.  

 **Problèmes liés au fonctionnement :**  

 Il n'existe aucun problème opérationnel.  

### <a name="expired-icon"></a>Icône Expiré  
 ![icône](../media/Expired.jpg "Icône Expiré") L’icône avec un X noir représente une mise à jour logicielle qui a expiré. Vous pouvez également identifier les mises à jour logicielles qui ont expiré en consultant la colonne **Expiré** de la mise à jour logicielle lors de l’affichage de cette dernière dans la console Configuration Manager.  

 **Description :**  

 Les mises à jour logicielles expirées pouvaient auparavant être déployées sur des ordinateurs clients, mais après l’expiration d’une mise à jour logicielle, aucun nouveau déploiement ne peut plus être créé pour les mises à jour logicielles. Les mises à jour logicielles qui ont expiré sont supprimées des déploiements actifs et ne sont plus mises à la disposition des clients.  

 **Problèmes liés au fonctionnement :**  

 Il n'existe aucun problème opérationnel.

### <a name="superseded-icon"></a>Icône Remplacée  
 ![icône](../media/Superseded.jpg "Icône Remplacée") L’icône avec une étoile jaune représente une mise à jour logicielle remplacée. Vous pouvez également identifier les mises à jour logicielles remplacées dans la colonne **Remplacée** de la mise à jour logicielle affichée dans la console Configuration Manager.  

 **Description :**  

 Les mises à jour logicielles remplacées ont été remplacées par des versions plus récentes de la mise à jour logicielle. En règle générale, une mise à jour logicielle qui en remplace une autre effectue une ou plusieurs des opérations suivantes :  

- Elle optimise, améliore ou s’ajoute au correctif fourni par une ou plusieurs mises à jour logicielles précédemment publiées.  

- Elle améliore l’efficacité de son package de fichiers de mise à jour logicielle, que les clients installent si la mise à jour logicielle est approuvée pour l’installation. Par exemple, la mise à jour logicielle remplacée peut contenir des fichiers qui ne sont plus pertinents pour le correctif ou pour les systèmes d’exploitation récemment pris en charge par la nouvelle mise à jour logicielle. Ces fichiers ne sont donc pas inclus dans le package de fichiers de la mise à jour logicielle de remplacement.  

- Met à jour les versions les plus récentes d'un produit, c'est-à-dire, ne s'applique plus aux anciennes versions ou configurations d'un produit. Les mises à jour logicielles peuvent également remplacer d’autres mises à jour logicielles si des modifications ont été apportées pour étendre la prise en charge des langues. Par exemple, une révision récente d’une mise à jour de produit pour Microsoft Office peut supprimer la prise en charge d’un système d’exploitation antérieur, mais ajouter une prise en charge de langues supplémentaires dans la version de mise à jour logicielle initiale.  

  Sous l’onglet Règles de remplacement dans Propriétés du composant du point de mise à jour logicielle, vous pouvez indiquer de quelle façon les mises à jour logicielles remplacées doivent être gérées. Pour plus d'informations, voir [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Problèmes liés au fonctionnement :**  

  Quand cela est possible, déployez la mise à jour logicielle de remplacement sur les ordinateurs clients au lieu de la mise à jour logicielle remplacée. Vous pouvez afficher une liste des mises à jour logicielles qui remplacent la mise à jour logicielle, sous l’onglet **Informations de remplacement** dans les propriétés de mise à jour logicielle.  

### <a name="invalid-icon"></a>Icône Non valide  
 ![icône](../media/Invalid.jpg "Icône Non valide") L’icône avec un X rouge représente une mise à jour logicielle non valide.  

 **Description :**  

 Les mises à jour logicielles non valides font partie d’un déploiement actif, mais, pour une raison quelconque, le contenu (fichiers de mise à jour logicielle) n’est pas disponible. Voici les scénarios susceptibles de générer cet état :  

- Vous avez déployé la mise à jour logicielle, mais le fichier de mise à jour logicielle a été supprimé du package de déploiement et n’est plus disponible.  

- Vous avez créé un déploiement de mise à jour logicielle sur un site, et l’objet de déploiement a été répliqué sur un site enfant, mais le package de déploiement n’a pas été répliqué sur le site enfant.  

  **Problèmes liés au fonctionnement :**  

  Si le contenu d’une mise à jour logicielle est manquant, les clients ne peuvent pas installer la mise à jour logicielle tant que ce contenu n’est pas disponible sur un point de distribution. Vous pouvez redistribuer le contenu aux points de distribution à l’aide de l’action **Redistribuer** . Quand le contenu d’une mise à jour logicielle est manquant dans un déploiement créé sur un site parent, vous devez répliquer ou redistribuer la mise à jour logicielle sur le site enfant. Pour plus d’informations sur la redistribution de contenu, consultez [Gérer le contenu que vous avez distribué](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Icône Métadonnées uniquement
 ![icône](../media/MetadataOnly.png "Icône Métadonnées uniquement") L’icône avec une flèche bleue représente une mise à jour logicielle de métadonnées uniquement.

 **Description :**  

 Les mises à jour logicielles de métadonnées uniquement sont disponibles dans la console Configuration Manager pour la création de rapports. Vous ne pouvez pas déployer ni télécharger des mises à jour logicielles de métadonnées uniquement, car aucun fichier de mise à jour logicielle n’est associé avec les métadonnées des mises à jour logicielles.  

 **Problèmes liés au fonctionnement :**  

 Les mises à jour logicielles de métadonnées uniquement sont disponibles pour la création de rapports, mais ne sont pas destinées au déploiement de mises à jour logicielles.  

## <a name="icons-for-software-update-groups"></a>Icônes des groupes de mises à jour logicielles  
 Les groupes de mises à jour logicielles sont représentés par une des icônes suivantes.  

### <a name="normal-icon"></a>Icône Normale  
 ![icône](../media/Normal.jpg "Icône Normale") L’icône avec une flèche verte représente un groupe de mises à jour logicielles qui contient uniquement des mises à jour logicielles normales.  

 **Problèmes liés au fonctionnement :**  

 Il n'existe aucun problème opérationnel.  

### <a name="expired-icon"></a>Icône Expiré  
 ![icône](../media/Expired.jpg "Icône Expiré")L’icône avec un X noir représente un groupe de mises à jour logicielles qui contient une ou plusieurs mises à jour logicielles qui ont expiré.  

 **Problèmes liés au fonctionnement :**  

 Quand cela est possible, supprimez ou remplacez les mises à jour logicielles expirées dans le groupe de mises à jour logicielles.  

### <a name="superseded-icon"></a>Icône Remplacée  
 ![icône](../media/Superseded.jpg "Icône Remplacée") L’icône avec une étoile jaune représente un groupe de mises à jour logicielles qui contient une ou plusieurs mises à jour logicielles remplacées.  

 **Problèmes liés au fonctionnement :**  

 Quand cela est possible, remplacez la mise à jour logicielle remplacée dans le groupe de mises à jour logicielles par la mise à jour logicielle de remplacement.  

### <a name="invalid-icon"></a>Icône Non valide  
 ![icône](../media/Invalid.jpg "Icône Non valide") L’icône avec un X rouge représente un groupe de mises à jour logicielles qui contient une ou plusieurs mises à jour logicielles non valides.  

 **Problèmes liés au fonctionnement :**  

 Si le contenu d’une mise à jour logicielle est manquant, les clients ne peuvent pas installer la mise à jour logicielle tant que ce contenu n’est pas disponible sur un point de distribution. Vous pouvez redistribuer le contenu aux points de distribution à l’aide de l’action **Redistribuer** . Quand le contenu d’une mise à jour logicielle est manquant dans un déploiement créé sur un site parent, vous devez répliquer ou redistribuer la mise à jour logicielle sur le site enfant. Pour plus d’informations sur la redistribution de contenu, consultez [Gérer le contenu que vous avez distribué](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  
