---
title: Créer des éléments de configuration enfants
titleSuffix: Configuration Manager
description: Créez des éléments de configuration enfants dans System Center Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b88ee7eaac8df8ffce93937f3a3f2616b9e085b
ms.sourcegitcommit: 417e3834a42b415a8e129327dd3c15cc0c7ec5a2
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65443162"
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>Guide pratique pour créer des éléments de configuration enfants dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les éléments de configuration enfants sont des copies d’éléments de configuration qui maintiennent une relation avec l’élément de configuration d’origine dans le sens où ils héritent de la configuration d’origine de l’élément de configuration parent.  

Quand vous examinez les propriétés d’un élément de configuration enfant dans la console Configuration Manager, vous ne pouvez pas modifier les objets et les paramètres hérités avec leurs critères de validation. En revanche, il vous est possible d'ajouter, puis de modifier, d'autres critères de validation pour l'élément de configuration enfant. Vous pouvez aussi ajouter de nouveaux objets et paramètres à ce dernier.
On peut par exemple créer et modifier un élément de configuration enfant pour adapter l’élément de configuration d’origine aux besoins de l’entreprise.  

> [!NOTE]  
>  Vous pouvez uniquement créer des éléments de configuration enfants à partir d’éléments de configuration du type **Ordinateurs et serveurs Windows (personnalisés)**.  

## <a name="to-create-a-child-configuration-item"></a>Pour créer un élément de configuration enfant  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

3.  Dans la liste **Éléments de configuration** , sélectionnez l’élément de configuration pour lequel vous souhaitez créer un élément de configuration enfant, puis sous l’onglet **Accueil** , dans le groupe **Élément de configuration** , cliquez sur **Créer un élément de configuration enfant**.  

4.  Sur la page **Général** de l' **Assistant Création d'élément de configuration enfant**, vous pouvez choisir une révision spécifique de l'élément de configuration parent à utiliser pour créer l'enfant. Les autres étapes de cet Assistant sont identiques à celles que vous utiliseriez pour créer un élément de configuration standard. Pour plus d’informations, consultez [Guide pratique pour créer des éléments de configuration personnalisés pour les ordinateurs et serveurs Windows](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Effectuez toutes les étapes de l'Assistant. Le nouvel élément de configuration enfant figure dans la liste **Éléments de configuration** .  
