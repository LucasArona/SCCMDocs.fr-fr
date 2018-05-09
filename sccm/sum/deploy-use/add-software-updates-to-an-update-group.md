---
title: 'Ajouter des mises à jour à un groupe de mises à jour '
titleSuffix: Configuration Manager
description: Ajoutez manuellement ou automatiquement des mises à jour logicielles à un groupe de mises à jour logicielles dans votre environnement.
author: aczechowski
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: df213206ee673e872852958233973e4f091728b9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="add-software-updates-to-an-update-group"></a>Ajouter des mises à jour logicielles à un groupe de mises à jour  

*S’applique à : System Center Configuration Manager (Current Branch)*

 Les groupes de mises à jour logicielles vous permettent d'organiser efficacement les mises à jour logicielles dans votre environnement. Vous pouvez ajouter des mises à jour logicielles à un groupe de mises à jour logicielles manuellement ou automatiquement à l’aide d’une règle de déploiement automatique (ADR). Une telle règle vous permet aussi de déployer un groupe de mises à jour logicielles manuellement ou automatiquement. Après avoir déployé un groupe de mises à jour logicielles, vous pouvez ajouter de nouvelles mises à jour logicielles au groupe et Configuration Manager les déploiera automatiquement. Pour ajouter des mises à jour logicielles à un groupe nouveau ou existant de mises à jour logicielles, procédez comme suit.  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>Pour ajouter des mises à jour logicielles à un nouveau groupe de mises à jour logicielles  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail Bibliothèque de logiciels, développez **Mises à jour logicielles**, puis cliquez sur **Toutes les mises à jour logicielles**.  

3.  Sélectionnez les mises à jour logicielles à ajouter au nouveau groupe de mises à jour logicielles.  

4.  Dans l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Créer un groupe de mises à jour logicielles**.  

5.  Spécifiez le nom du groupe de mises à jour logicielles et indiquez éventuellement une description. Utilisez un nom et une description suffisamment détaillés pour vous permettre de déterminer quel type de mises à jour logicielles se trouve dans le groupe de mises à jour logicielles. Pour continuer, cliquez sur **Créer**.  

6.  Cliquez sur **Groupes de mises à jour logicielles** pour afficher le nouveau groupe de mises à jour logicielles.  

7.  Sélectionnez le groupe de mises à jour logicielles et, sous l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Afficher les membres** pour afficher la liste des mises à jour logicielles incluses dans le groupe.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Pour ajouter des mises à jour logicielles à un groupe de mises à jour logicielles existant  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail Bibliothèque de logiciels, développez **Mises à jour logicielles**, puis cliquez sur **Toutes les mises à jour logicielles**.  

3.  Sélectionnez les mises à jour logicielles que vous souhaitez ajouter au nouveau groupe de mises à jour logicielles.  

    > [!NOTE]  
    >  Dans le nœud **Toutes les mises à jour logicielles**, par défaut, Configuration Manager affiche uniquement les mises à jour logicielles classées comme **Critique** et **Sécurité** et qui ont été publiées au cours des 30 derniers jours.  

4.  Dans l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Modifier l'adhésion**.  

5.  Sélectionnez le groupe de mises à jour logicielles dans lequel vous souhaitez ajouter les mises à jour logicielles.  

6.  Cliquez sur le nœud **Groupes de mises à jour logicielles** pour afficher le groupe de mises à jour logicielles.  

7.  Sélectionnez le groupe de mises à jour logicielles et, sous l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Afficher les membres** pour afficher la liste des mises à jour logicielles incluses dans le groupe.  
