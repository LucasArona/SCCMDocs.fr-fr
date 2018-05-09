---
title: Activer Lookout MTP dans Intune
titleSuffix: Configuration Manager
description: Activez Mobile Threat Protection de Lookout dans la console d’administration Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79a583237d882101d70442cbf6b55a5e3c0e9b11
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Activer la connexion Lookout MTP dans la console d’administration Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique montre comment activer la connexion Lookout MTP dans Intune. Vous devez déjà avoir configuré le connecteur Intune dans la console Lookout avant d’effectuer cette étape.  Si vous ne l’avez pas déjà fait, procédez comme décrit dans [Configurer votre abonnement avec Mobile Threat Protection de Lookout](set-up-your-subscription-with-lookout.md).

Pour activer la connexion Lookout MTP dans Intune, dans la page **Administration** de la [console Administrateur Microsoft Intune](https://manage.microsoft.com), choisissez **Intégration de service tiers**. Choisissez **État de Lookout** et activez **Synchronisation avec MTP** à l’aide du bouton bascule.

![capture d’écran de la page de synchronisation Lookout avec le bouton bascule Activer mis en surbrillance](media/lookout-intune-synchronization.png)

Cette étape termine la configuration de l’intégration de Lookout et Intune dans la console Administrateur Intune.  Les étapes suivantes permettant d’implémenter cette solution impliquent le déploiement des [applications Lookout for Work](configure-and-deploy-lookout-for-work-apps.md) et la configuration de la stratégie de [conformité](enable-device-threat-protection-rule-compliance-policy.md).

>[!IMPORTANT]
> Vous **devez** configurer l’application Lookout for Work avant de créer des règles de stratégie de conformité et de configurer l’accès conditionnel. De cette façon, l’application est prête et disponible pour l’installation afin de permettre aux utilisateurs finaux d’accéder à la messagerie et à d’autres ressources de l’entreprise.

## <a name="next-steps"></a>Étapes suivantes
[Configurer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
