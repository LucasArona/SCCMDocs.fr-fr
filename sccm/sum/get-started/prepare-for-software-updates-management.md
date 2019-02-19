---
title: Préparation à la gestion des mises à jour logicielles
titleSuffix: Configuration Manager
description: Pour préparer votre environnement à la gestion des mises à jour logicielles, effectuez ces tâches qui permettent d’afficher les données d’évaluation de la conformité dans la console System Center Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 01907900-e28b-4cd7-9479-42906416707b
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 57d83601af5aa41a61b80d539bf87f4e9616792c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138022"
---
# <a name="prepare-for-software-updates-management"></a>Préparation à la gestion des mises à jour logicielles

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de pouvoir afficher les données d’évaluation de la conformité des mises à jour logicielles dans la console System Center Configuration Manager et déployer les mises à jour logicielles sur des ordinateurs clients, vous devez effectuer les étapes décrites dans les sections ci-dessous.

## <a name="step-1-install-a-software-update-point"></a>Étape 1 : Installer un point de mise à jour logicielle  
Il doit y avoir un point de mise à jour logicielle installé sur le site d’administration centrale, ou le site principal autonome, et sur les sites principaux pour permettre l’évaluation de la conformité des mises à jour logicielles et le déploiement des mises à jour logicielles sur les clients. Le point de mise à jour de logicielle est facultatif sur les sites secondaires. Pour plus d’informations, consultez [Installer un point de mise à jour logicielle](install-a-software-update-point.md)  

## <a name="step-2-synchronize-software-updates"></a>Étape 2 : Synchroniser les mises à jour logicielles
La synchronisation des mises à jour logicielles consiste à récupérer les métadonnées des mises à jour logicielles correspondant aux critères que vous configurez. Les mises à jour logicielles ne s’affichent pas dans la console Configuration Manager tant que vous ne les avez pas synchronisées. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles](synchronize-software-updates.md).   

## <a name="step-3-configure-classifications-and-products-to-synchronize"></a>Étape 3 : Configurer les classifications et les produits à synchroniser
Effectuez cette configuration sur le site d'administration centrale ou le site primaire autonome. Après la première synchronisation des mises à jour logicielles, Configuration Manager récupère une liste mise à jour de produits et de classifications. Vous pouvez maintenant sélectionner de nouvelles options disponibles dans les propriétés du composant du point de mise à jour logicielle. Après avoir configuré les nouveaux produits et classifications, répétez l’étape 2 pour démarrer la synchronisation des mises à jour logicielles et récupérer les métadonnées de mises à jour logicielles correspondant aux nouveaux critères. Pour plus d’informations, consultez [Configurer les classifications et les produits à synchroniser](configure-classifications-and-products.md).

## <a name="step-4-manage-settings-for-software-updates"></a>Étape 4 : Gérer les paramètres des mises à jour logicielles
Après avoir synchronisé les mises à jour logicielles, vérifiez les paramètres du client Configuration Manager, les configurations de stratégies de groupe et les paramètres des mises à jour logicielles avant de déployer les mises à jour logicielles. Pour plus d’informations, consultez [Gérer les paramètres des mises à jour logicielles](manage-settings-for-software-updates.md).
