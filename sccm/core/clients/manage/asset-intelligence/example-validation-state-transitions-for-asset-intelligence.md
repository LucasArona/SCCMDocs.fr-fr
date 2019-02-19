---
title: Exemples de transitions d’état de validation pour Asset Intelligence
titleSuffix: Configuration Manager
description: Découvrez des exemples de transition d’état de validation pour Asset Intelligence dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87f247d380d91a43fedbb78a701d3be89c0e6efa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122013"
---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>Exemples de transitions d’état de validation pour Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les états de validation Asset Intelligence dans System Center Configuration Manager ne sont pas statiques et peuvent se distinguer des actions administratives que vous exécutez pour affecter les données stockées dans le catalogue Asset Intelligence. Cette rubrique propose des exemples possibles de transition d’état de validation.

##  <a name="BKMK_UncategorizedIsCategorized"></a> Un élément de catalogue sans catégorie est catégorisé par l’utilisateur administratif  

|**Transition d'état**|**Description de la transition d'état**|  
|--------------------------|--------------------------------------|  
|**Sans catégorie**|Titre de logiciel inventorié qui n'a pas été catégorisé précédemment par System Center Online ou saisi par l'utilisateur administratif dans le catalogue Asset Intelligence.|  
|**Sans catégorie** à **Définipar l’utilisateur**|L'élément sans catégorie est catégorisé par l'utilisateur administratif.|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> Un élément de catalogue catégorisé est de nouveau catégorisé par l’utilisateur administratif  

|**Transition d'état**|**Description de la transition d'état**|  
|--------------------------|--------------------------------------|  
|**Validé**|L'élément du catalogue a été défini par les chercheurs de System Center Online et figure dans le catalogue Asset Intelligence.|  
|**Validé** à **Défini par l'utilisateur**|Un élément de catalogue validé est de nouveau catégorisé par l'utilisateur administratif.|  

> [!NOTE]  
>  Étant donné que les informations de catégorisation obtenues à partir de System Center Online sont stockées dans la base de données et ne peuvent pas être supprimées, l'utilisateur administratif peut restaurer la catégorisation de System Center Online ultérieurement.  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> Un élément du catalogue défini par l’utilisateur est de nouveau catégorisé par System Center Online  

|**Transition d'état**|**Description de la transition d'état**|  
|--------------------------|--------------------------------------|  
|**Sans catégorie**|Un titre logiciel inventorié sans catégorie par System Center Online ou par l'utilisateur administratif est ajouté au catalogue Asset Intelligence.|  
|**Défini par l'utilisateur**|L'élément sans catégorie est catégorisé par l'utilisateur administratif.|  
|**Défini par l'utilisateur** à **Peut être mis à jour**|Un élément de catalogue défini par l'utilisateur a été catégorisé différemment par System Center Online au cours de mises à jour manuelles en bloc ultérieures du catalogue Asset Intelligence.<br /><br /> L'utilisateur administratif peut utiliser la boîte de dialogue **Résolution de conflit de détails de logiciel** pour décider s'il souhaite utiliser les nouvelles informations de catégorisation ou la valeur précédente définie par l'utilisateur.|  
|**Peut être mis à jour** à **Validé**|L'utilisateur administratif utilise la boîte de dialogue **Résolution de conflit de détails de logiciel** pour utiliser les nouvelles informations de catégorisation reçues depuis System Center Online au cours de la mise à jour précédente du catalogue.|  
|ou||  
|**Peut être mis à jour** à **Défini par l'utilisateur**|L'utilisateur administratif utilise la boîte de dialogue **Résolution de conflit de détails de logiciel** pour utiliser la valeur précédente définie par l'utilisateur.|  

> [!NOTE]  
>  Étant donné que les informations de catégorisation obtenues à partir de System Center Online sont stockées dans la base de données et ne peuvent pas être supprimées, l'utilisateur administratif peut restaurer la catégorisation de System Center Online ultérieurement.  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> Un élément de catalogue sans catégorie est soumis à System Center Online à des fins de catégorisation  

|**Transition d'état**|**Description de la transition d'état**|  
|--------------------------|--------------------------------------|  
|**Sans catégorie**|Un titre logiciel inventorié sans catégorie par System Center Online ou par l'utilisateur administratif est ajouté à la base de données Asset Intelligence.|  
|**Sans catégorie** à **En attente**|L'élément sans catégorie est soumis à System Center Online afin que l'utilisateur administratif puisse le classer.|  
|**En attente** à **Validé**|L'élément est catégorisé par System Center Online. L'utilisateur administratif importe l'élément dans le catalogue Asset Intelligence à l'aide d'une mise à jour en bloc du catalogue ou de la synchronisation du catalogue Asset Intelligence. Les deux sont disponibles en utilisant le rôle de système de site du point de synchronisation Asset Intelligence.|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> Un élément de catalogue défini par l’utilisateur est soumis à System Center Online à des fins de catégorisation  

|**Transition d'état**|**Description de la transition d'état**|  
|--------------------------|--------------------------------------|  
|**Sans catégorie**|Un titre logiciel inventorié sans catégorie précédemment par un utilisateur administratif ou par System Center Online est ajouté à la base de données Asset Intelligence.|  
|**Défini par l'utilisateur**|Vous avez catégorisé l'élément sans catégorie.|  
|**Défini par l'utilisateur** à **En attente**|Vous soumettez l'élément défini par l'utilisateur à System Center Online à des fins de catégorisation.|  
|**En attente** à **Peut être mis à jour**|Un élément du catalogue défini par un utilisateur a été catégorisé différemment par System Center Online lors de la synchronisation de catalogue suivante. Vous pouvez exécuter l'action **Résoudre le conflit** pour décider si vous allez utiliser les nouvelles informations de catégorisation ou la précédente valeur définie par l'utilisateur. Pour plus d’informations sur la résolution des conflits, consultez [Résoudre les conflits de détails de logiciel](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Peut être mis à jour** à **Validé**|Vous exécutez l'action **Résoudre le conflit** et sélectionnez les nouvelles informations de catégorisation reçues depuis System Center Online lors de la précédente mise à jour de catalogue. Pour plus d’informations sur la résolution des conflits, consultez [Résoudre les conflits de détails de logiciel](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|ou||  
|**Peut être mis à jour** à **Défini par l'utilisateur**|Vous exécutez l'action **Résoudre le conflit** et choisissez d'utiliser la précédente valeur définie par l'utilisateur. Pour plus d’informations sur la résolution des conflits, consultez [Résoudre les conflits de détails de logiciel](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Étant donné que les informations de catégorisation obtenues à partir de System Center Online sont stockées dans la base de données et ne peuvent pas être supprimées, vous pouvez restaurer la catégorisation de System Center Online ultérieurement.  
