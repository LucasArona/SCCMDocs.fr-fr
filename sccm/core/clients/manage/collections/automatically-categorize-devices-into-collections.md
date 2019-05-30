---
title: Classement automatiquement des appareils dans des regroupements
titleSuffix: Configuration Manager
description: Classez automatiquement des appareils dans des regroupements.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: e0a70d55eb63a51ca980db1fb7089a9490a2803c
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176719"
---
# <a name="automatically-categorize-devices-into-collections"></a>Classement automatiquement des appareils dans des regroupements

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer des catégories d’appareils pour classer automatiquement les appareils dans des regroupements d’appareils quand vous utilisez Configuration Manager avec Microsoft Intune. Les utilisateurs doivent ensuite choisir une catégorie d’appareils quand ils inscrivent un appareil dans Intune. Vous pouvez changer une catégorie d’appareils dans la console Configuration Manager.

> [!IMPORTANT]
>  Cette fonctionnalité est opérationnelle avec la version de Microsoft Intune de **juin 2016**  et ultérieure. Vérifiez que vous avez effectué la mise à jour vers cette version avant d’essayer ces procédures.

## <a name="create-device-categories"></a>Créer des catégories d’appareils

1.  Accédez à **Ressources et conformité** > **Vue d’ensemble** > **Regroupements d’appareils**.
2.  Sous l’onglet **Accueil**, dans le groupe **Regroupements d’appareils**, choisissez **Gérer les catégories d’appareils**.
3.  Créer, modifier ou supprimer des catégories.

## <a name="associate-a-collection-with-a-device-category"></a>Associer un regroupement à une catégorie d’appareils

Quand vous associez un regroupement à une catégorie d’appareils, tous les appareils de cette catégorie sont ajoutés à ce regroupement. Vous ne pouvez pas ajouter une règle de catégorie d’appareils à un regroupement intégré comme **Tous les systèmes**.

1.  Sous l’onglet **Règles d’adhésion** de la boîte de dialogue **Propriétés** pour un regroupement d’appareils, choisissez **Ajouter une règle** > **Règle de catégorie d’appareils**.
2.  Dans la boîte de dialogue **Sélectionner des catégories d’appareils**, sélectionnez une ou plusieurs catégories d’appareils à appliquer à tous les appareils du regroupement.

## <a name="change-the-category-of-a-device"></a>Changer la catégorie d’un appareil

1.  Dans **Ressources et Conformité** > **Vue d’ensemble** > **Appareils**, sélectionnez un appareil dans la liste **Appareils**.
2.  Sous l’onglet **Accueil**, dans le groupe **Appareil**, choisissez **Modifier la catégorie**.
3.  Choisissez une catégorie, puis choisissez **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Afficher la catégorie à laquelle appartient un appareil

Dans **Ressources et Conformité** > **Vue d’ensemble** > **Appareils**, dans la liste **Appareils**, la catégorie est affichée dans la colonne **Catégorie d’appareil**.

Si la colonne **Catégorie d’appareil** n’est pas affichée, cliquez avec le bouton droit sur l’en-tête de l’une des colonnes dans la liste **Appareils** (comme **Nom**), puis sélectionnez **Catégorie d’appareil**.

Si vous affectez un appareil à une catégorie, puis supprimez par la suite cette catégorie, le rapport **Liste des appareils inscrits par utilisateur dans Microsoft Intune** affichera un GUID dans la colonne **Catégorie d’appareil** au lieu d’un nom de catégorie.
