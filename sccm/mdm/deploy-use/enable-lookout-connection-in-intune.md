---
title: Activer Lookout MTD dans Intune
description: Activez Lookout Mobile Threat Defense (MTD) dans le portail Microsoft Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b36e98edfffcc26b7fb2670cbfdc31c165331f0f
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62226881"
---
# <a name="enable-lookout-mtd-connection-in-the-intune-admin-console"></a>Activer la connexion à Lookout MTD dans la console d’administration Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article explique comment activer la connexion à Lookout Mobile Threat Defense (MTD) dans Microsoft Intune. Vous devez déjà avoir configuré le connecteur Intune dans la console Lookout avant d’effectuer cette étape. Si ce n’est déjà fait, procédez aux étapes décrites dans [Configurer votre abonnement avec Mobile Threat Protection de Lookout](set-up-your-subscription-with-lookout.md).



## <a name="enable-the-lookout-mtd-connector"></a>Activer le connecteur Lookout MTD

1. Accédez au [portail Azure](https://portal.azure.com) et connectez-vous avec vos informations d’identification Intune. Une fois connecté, vous voyez le **tableau de bord Azure**.  

2. Dans le **tableau de bord Azure**, dans le menu de gauche, choisissez **Tous les services**, puis tapez **Intune** dans la zone de texte de filtre.  

3. Quand vous choisissez **Intune**, le **tableau de bord Intune** s’ouvre.  

4. Dans le **tableau de bord Intune**, choisissez **Conformité de l’appareil**, puis choisissez **Mobile Threat Defense** sous la section **Configurer**.  

5. Dans le volet **Mobile Threat Defense**, choisissez **Ajouter**.  

6. Dans la liste déroulante, choisissez **Lookout** pour **Mobile Threat Defense connector to setup** (Connecteur Mobile Threat Defense à configurer).  

7. Activez les options nécessaires en fonction des besoins de votre entreprise.  



## <a name="mtd-toggle-options"></a>Options MTD

Vous pouvez décider des options MTD que vous devez activer en fonction des besoins de votre entreprise. Voici des informations détaillées concernant ces options :

- **Se connecter Android 4.1 + appareils Lookout for Work MTD**: Lorsque vous activez cette option, vous pouvez avoir Android 4.1 + sauvegarder de signaler des risques de sécurité des appareils à Intune.  
    - **Marquer comme non conforme si aucune donnée n’est reçue**: Si Intune ne reçoit pas les données sur un appareil sur cette plateforme à partir de Lookout, considère l’appareil non conforme.  

- **Connectez des appareils iOS 8.0 + à Lookout for Work MTD**: Lorsque vous activez cette option, vous pouvez avoir des appareils iOS 8.0 + rapportant risque de sécurité à Intune.
    - **Marquer comme non conforme si aucune donnée n’est reçue**: Si Intune ne reçoit pas les données sur un appareil sur cette plateforme à partir de Lookout, considère l’appareil non conforme.  

> [!TIP]  
> Dans le volet Mobile Threat Defense, vous pouvez voir **l’état de la connexion** et la date de **dernière synchronisation** entre Intune et Lookout.



## <a name="next-steps"></a>Étapes suivantes
Cette étape termine la configuration de l’intégration de Lookout et Intune. Les étapes suivantes permettant d’implémenter cette solution impliquent le déploiement des [applications Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) et la configuration de la stratégie de [conformité](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> Vous *devez* configurer l’application Lookout for Work avant de créer des règles de stratégie de conformité et de configurer l’accès conditionnel. Avec cette action, l’application est prête et disponible pour l’installation afin de permettre aux utilisateurs finaux d’accéder à l’e-mail et à d’autres ressources de l’entreprise.

[Configurer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
