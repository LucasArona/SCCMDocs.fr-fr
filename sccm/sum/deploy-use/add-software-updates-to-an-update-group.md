---
title: 'Ajouter des mises à jour à un groupe de mises à jour '
titleSuffix: Configuration Manager
description: Ajoutez manuellement ou automatiquement des mises à jour logicielles à un groupe de mises à jour logicielles dans votre environnement.
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: b207d0c210aa25489d67a5a551bf795e86c1582b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500251"
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
    >  Sur le nœud **Toutes les mises à jour de logiciels**, Configuration Manager affiche toutes les mises à jour, à l’exception de celles de la classification **Mises à niveau** et de la classification de produits **Client Office 365**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Modifier l'adhésion**.  

5.  Sélectionnez le groupe de mises à jour logicielles dans lequel vous souhaitez ajouter les mises à jour logicielles.  

6.  Cliquez sur le nœud **Groupes de mises à jour logicielles** pour afficher le groupe de mises à jour logicielles.  

7.  Sélectionnez le groupe de mises à jour logicielles et, sous l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Afficher les membres** pour afficher la liste des mises à jour logicielles incluses dans le groupe.  
