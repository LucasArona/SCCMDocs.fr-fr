---
title: Gestion hybride des appareils mobiles (MDM) avec Microsoft Intune
titleSuffix: Configuration Manager
description: Découvrez la gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8651b5a82c4e3cb4e39fac53cc5bc3357df6e47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346628"
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous pouvez gérer des appareils iOS, Windows et Android avec Configuration Manager et Microsoft Intune. Toutes les tâches de gestion sont administrées à partir de la console Configuration Manager, où vous effectuez toutes vos autres tâches de gestion de manière intégrée et transparente avec le service en ligne de Microsoft Intune via Internet.  Vous pouvez utiliser Configuration Manager pour permettre aux utilisateurs d’accéder aux ressources d’entreprise sur leurs appareils de manière sécurisée et gérée. Avec la gestion des appareils, vous protégez les données d’entreprise tout en permettant aux utilisateurs d’inscrire leurs appareils personnels ou d’entreprise pour accéder aux données d’entreprise. Fonctionnalités de gestion des appareils :

-   Mise hors service et réinitialisation des appareils
-   Configuration des paramètres de compatibilité tels que les mots de passe, la sécurité, l'itinérance, le chiffrement et la communication sans fil
-   Déploiement d’applications métier sur les appareils
-   Déploiement d'applications sur des appareils qui se connectent au Windows Store, au Windows Phone Store, à l'App Store ou à Google Play
-   Collecte de l'inventaire matériel
-   Collecte de l'inventaire logiciel à l'aide de rapports intégrés

Pour en savoir plus sur les nouvelles fonctionnalités disponibles pour la gestion des appareils mobiles (MDM) hybride, consultez [Nouvelles fonctionnalités pour la gestion des appareils mobiles (MDM) hybride](../understand/whats-new-in-hybrid-mobile-device-management.md).

Ce document part du principe que vous utilisez déjà Configuration Manager pour gérer les ordinateurs et que vous souhaitez étendre la console Configuration Manager avec Intune pour gérer des appareils mobiles. Pour comprendre les différences entre Intune et la gestion des appareils mobiles (MDM) hybride, consultez [Choisir entre la solution autonome Microsoft Intune et la gestion des appareils mobiles hybride avec System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Après avoir étendu Configuration Manager avec Intune, vous pouvez inscrire et gérer des appareils d’entreprise ou autoriser les utilisateurs à inscrire leurs appareils personnels. Vous pouvez également gérer des appareils d’entreprise avec Intune à partir de Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Inscription pour la gestion des appareils mobiles (MDM) hybride
Les appareils peuvent être gérés à l’aide de la gestion hybride s’ils ont été préalablement inscrits auprès du service. Le processus d’inscription des appareils dépend du type et de la propriété de l’appareil, ainsi que du niveau de gestion souhaité.
- L’inscription « Apportez votre propre appareil » (BYOD) permet aux utilisateurs d’inscrire leurs téléphones, tablettes ou PC personnels.
- L’inscription d’appareils d’entreprise (COD) permet de gérer les appareils en utilisant des fonctionnalités comme la réinitialisation à distance, le partage d’appareils ou l’affinité entre utilisateur et appareil.
- Si vous utilisez [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager) (localement ou hébergé dans le cloud), vous pouvez choisir la gestion Intune simple sans inscription. Vous pouvez également gérer des PC Windows à l’aide du [logiciel client Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
