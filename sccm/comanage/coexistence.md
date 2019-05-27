---
title: Coexistence de la gestion des données de référence tierce
titleSuffix: Configuration Manager
description: Découvrez des informations sur l’utilisation d’un MDM de tiers avec Configuration Manager
ms.date: 04/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6abf4c81d03d5887294c85337b403a6fb17dca98
ms.sourcegitcommit: 23852dda81bb8496dd10c0a8ec4f740a8e15efc3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873368"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Coexistence d’un service MDM de tiers avec Configuration Manager

Quand vous gérez des appareils Windows 10 en parallèle avec Configuration Manager et Microsoft Intune, cette fonctionnalité est appelée [cogestion](/sccm/comanage/overview). Quand vous gérez des appareils avec Configuration Manager et que vous vous inscrivez auprès d’un service MDM de tiers, cette fonctionnalité est appelée *coexistence*. Le fait d’avoir deux autorités de gestion pour un même appareil peut s’avérer délicat si la gestion n’est pas correctement orchestrée entre les deux. Avec la cogestion, Configuration Manager et Intune équilibrent les [charges de travail](/sccm/comanage/workloads) pour garantir qu’il n’y a pas de conflits. Cette interaction n’existe pas avec les services de tiers : il existe donc des limitations avec les fonctionnalités de gestion dans le cas de la coexistence.

Le client Configuration Manager peut coexister avec un service MDM de tiers sur un appareil qui est joint à Azure Active Directory. L’appareil peut être de l’un des types suivants :

- [Joint à Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) uniquement. (Ce type est parfois désigné comme « joint à un domaine cloud »)  

- [Joint au domaine hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), où l’appareil est joint à votre annuaire Active Directory local et inscrit auprès d’Azure Active Directory.  

> [!Note]  
> Il ne prend pas en charge les [appareils personnels](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device).  

Quand le client Configuration Manager détecte qu’un service MDM tiers gère également l’appareil, il désactive automatiquement certaines charges de travail dans Configuration Manager. Ce comportement permet au service MDM de prendre en charge ces fonctions. Il empêche également les paramètres en conflit sur le client qui pourraient impacter négativement l’appareil et l’expérience utilisateur. Les charges de travail suivantes sont désactivées dans Configuration Manager dans ce cas :

- Stratégies d’accès aux ressources pour les paramètres VPN, Wi-Fi, d’e-mail et de certificat
- Gestion des applications, notamment les packages hérités
- Analyse et installation des mises à jour logicielles
- Endpoint Protection, la suite Windows Defender de fonctionnalités de protection contre les logiciels malveillants
- Stratégie de conformité pour l’accès conditionnel
- Configuration de l’appareil
- Gestion d’Office « Démarrer en un clic »

Le client Configuration Manager évite le conflit avec l’autorité de gestion tiers en continuant les opérations en lecture seule suivantes :

- Inventaire matériel et logiciel
- Asset Intelligence
- Contrôle de logiciel
- Rapports de gestion de l’alimentation

Pour plus d’informations sur les avantages de la cogestion avec Configuration Manager et Intune, consultez [Avantages de la cogestion](/sccm/comanage/overview#benefits).