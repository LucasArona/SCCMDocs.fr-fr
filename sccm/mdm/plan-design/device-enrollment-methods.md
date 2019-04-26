---
title: Méthodes d’inscription des appareils à des fins de gestion des appareils mobiles hybride
titleSuffix: Configuration Manager
description: Méthodes d’inscription des appareils à des fins de gestion des appareils mobiles hybride.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be1221b3448c8a2818f7fd02b5ff2d14218bbeed
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62286784"
---
# <a name="overview-of-device-enrollment-methods"></a>Présentation des méthodes d’inscription des appareils

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir étendu Configuration Manager avec Intune, vous pouvez inscrire et gérer des appareils appartenant à l’entreprise ou autoriser les utilisateurs à inscrire leurs appareils personnels. Vous pouvez également gérer des appareils d’entreprise avec Intune à partir de Configuration Manager.

Le tableau suivant présente les différentes méthodes d’inscription et les fonctionnalités qu’elles prennent en charge. Ces fonctionnalités sont les suivantes :
- **Réinitialisation** : réinitialise l’appareil aux paramètres d’usine, en supprimant toutes les données. [Mettre des appareils hors service](../deploy-use/wipe-lock-reset-devices.md)
- **Affinité** : associe les appareils à des utilisateurs. Fonctionnalité nécessaire pour la gestion des applications mobiles (MAM) et l’accès conditionnel aux données d’entreprise. [Affinité utilisateur](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Verrouillage** : empêche les utilisateurs de retirer leur appareil de la gestion. Les appareils iOS nécessitent le mode de verrouillage Supervisé. [Verrouillage à distance](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**Méthodes d’inscription des appareils iOS**

| **Méthode** |  **Réinitialisation** |  **Affinité**    |   **Verrouillage** | **Détails** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Non|    Oui |   Non | [Plus d’informations](../deploy-use/enable-platform-enrollment.md)|
|**[Gestionnaire d’inscription d’appareil](#dem)**|   Non |Non |Non  | [Plus d’informations](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Oui |   Facultatif |  Facultatif|[Plus d’informations](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Oui |   Facultatif |  Non| [Plus d’informations](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Méthodes d’inscription des appareils Windows et Android**

| **Méthode** |  **Réinitialisation** |  **Affinité**    |   **Verrouillage** | **Détails**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | Non|    Oui |   Non | [Plus d’informations](../deploy-use/enroll-hybrid-windows.md)|
|**[Gestionnaire d’inscription d’appareil](#dem)**|   Non |Non |Non  |[Plus d’informations](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Pour répondre à une série de questions qui vous aideront à déterminer la méthode appropriée, consultez [Choisir comment inscrire des appareils](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Avec la méthode d’inscription BYOD (« Apportez votre propre appareil »), les utilisateurs d’appareils personnels installent l’application Portail d’entreprise et inscrivent leurs propres appareils. Ils peuvent ensuite se connecter au réseau d’entreprise et rejoindre le domaine ou Azure Active Directory. Dans beaucoup de scénarios de gestion d’appareils d’entreprise (COD), l’inscription BYOD est nécessaire pour la plupart des plateformes d’appareils. Consultez [Configurer la gestion des appareils mobiles (MDM) hybride](../deploy-use/setup-hybrid-mdm.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Appareils d’entreprise
Les appareils d’entreprise (COD) peuvent être gérés à l’aide de la console Configuration Manager. Il est possible d’inscrire des appareils iOS directement par le biais des outils fournis par Apple. Tous les types d’appareils peuvent être inscrits par un administrateur ou un responsable à l’aide du gestionnaire d’inscription d’appareil. Les appareils dotés d’un numéro IMEI peuvent également être identifiés et référencés comme appartenant à l’entreprise pour mettre en œuvre des scénarios COD.

[Inscrire des appareils d’entreprise](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>Gestionnaire d’inscription d’appareil
Le gestionnaire d’inscription d’appareil est un compte d’utilisateur spécial qui permet d’inscrire et de gérer plusieurs appareils d’entreprise. Les responsables peuvent installer l’application Portail d’entreprise et inscrire de nombreux appareils sans utilisateur. En savoir plus sur le [gestionnaire d’inscription d’appareil](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Le programme d’inscription d’appareil (ou DEP) d’Apple vous permet de créer et déployer une stratégie « à distance » sur des appareils iOS achetés et gérés avec DEP. L’appareil est inscrit quand l’utilisateur le démarre pour la première fois et exécute l’Assistant d’installation iOS. Cette méthode prend en charge le mode **iOS supervisé**, qui fournit les fonctionnalités suivantes :
  - Inscription verrouillée
  - Accès conditionnel
  - Détection de jailbreak
  - Gestion des applications mobiles

En savoir plus sur la méthode [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Cette méthode permet d’inscrire des appareils connectés par USB en utilisant l’Assistant Configuration. L’administrateur crée une stratégie et l’exporte vers Apple Configurator. Les appareils d’entreprise connectés par USB sont préparés à l’aide d’une stratégie. L’administrateur doit inscrire manuellement chaque appareil. Après avoir reçu leur appareil, les utilisateurs exécutent l’Assistant Configuration pour inscrire l’appareil. Cette méthode prend en charge le mode **iOS supervisé**, qui fournit les fonctionnalités suivantes :
  - Accès conditionnel
  - Détection de jailbreak
  - Gestion des applications mobiles

En savoir plus sur l’[inscription via l’Assistant Configuration avec Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Retour au tableau](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gestion des appareils mobiles avec Exchange ActiveSync et Configuration Manager
Les appareils mobiles qui ne sont pas inscrits mais qui se connectent à Exchange ActiveSync (EAS) peuvent être gérés par Intune à l’aide de la stratégie de gestion des appareils mobiles EAS. Intune utilise un connecteur Exchange pour communiquer avec EAS, localement ou hébergé dans le cloud.

[Gestion des appareils mobiles à l’aide d’Exchange ActiveSync et d’Intune](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)
