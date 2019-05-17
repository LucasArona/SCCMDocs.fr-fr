---
title: Créer une séquence de tâches personnalisée
titleSuffix: Configuration Manager
description: Modifiez une séquence de tâches personnalisée dans System Center Configuration Manager pour y ajouter des étapes.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 79ef6832a32f0cb3ea36b8c36423b46ae3216438
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082911"
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Créer une séquence de tâches personnalisée avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous créez une séquence de tâches personnalisée dans System Center Configuration Manager, elle ne contient aucune étape de séquence de tâches. Après avoir créé la séquence de tâches, vous devez la modifier et ajouter les étapes de séquence de tâches dont vous avez besoin.  

##  <a name="BKMK_CustomTS"></a> Créer une séquence de tâches personnalisée  
 Pour créer une séquence de tâches personnalisée, procédez comme suit.  

#### <a name="to-create-a-custom-task-sequence"></a>Pour créer une séquence de tâches personnalisée  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4. Sur la page **Créer une nouvelle séquence de tâches** , sélectionnez **Créez une séquence de tâches personnalisée**.  

5. Sur la page **Informations sur la séquence de tâches** , spécifiez un nom, une description et une image de démarrage facultative pour la séquence de tâches à utiliser, puis fermez l'Assistant.  

   Après avoir fermé l’Assistant Création d’une séquence de tâches, Configuration Manager ajoute la séquence de tâches personnalisée au nœud **Séquences de tâches**. Vous pouvez désormais modifier cette séquence de tâches pour y ajouter des étapes de séquence de tâches.  

   Pour obtenir une liste des étapes de séquence de tâches disponibles, consultez [Étapes de séquence de tâches](../understand/task-sequence-steps.md).  

   Pour plus d’informations sur la modification d’une séquence de tâches, consultez [Modifier une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

   Souvent, vous utiliserez des séquences de tâches pour automatiser des tâches de déploiement de système d’exploitation, mais vous pouvez créer une séquence de tâches personnalisée pour automatiser de nombreuses tâches. Pour plus d’informations, consultez [Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation](create-a-task-sequence-for-non-operating-system-deployments.md).  

   ## <a name="next-steps"></a>Étapes suivantes
   [Déployer la séquence de tâches](/sccm/osd/deploy-use/deploy-a-task-sequence)
