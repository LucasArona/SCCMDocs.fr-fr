---
title: Gérer des applications
titleSuffix: Configuration Manager
description: Gérez des applications dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a57beb79bf7e4dc51e72d7254ff0f190c6ca32c4
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227997"
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Gérer des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Lorsque vous administrez des appareils par le biais de la gestion des appareils locaux Microsoft Intune ou de Configuration Manager, vous pouvez gérer ces types d’application supplémentaires :
- Package d'application Windows Phone (fichier *.xap)
- Package d'application pour iOS (fichier *.ipa)
- Package d'application pour Android (fichier *.apk)
- Package d'application pour Android sur Google Play
- Package d'application Windows Phone (dans Windows Phone Store)
- Windows Installer par le biais de la gestion des appareils mobiles
- Application Web

Cette section fournit des informations détaillées sur la création et l’administration des applications à l’aide de la fonction de gestion des appareils mobiles locale ou hybride.

La section [Tâches de gestion pour les applications System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md) fournit des informations générales supplémentaires sur la gestion des types de déploiement et applications System Center Configuration Manager.

## <a name="deploying-and-monitoring-apps"></a>Déploiement et surveillance des applications

Dans System Center Configuration Manager, les processus de déploiement et de surveillance sont identiques pour les appareils mobiles et pour les dispositifs locaux (ordinateurs de bureau ou portables). Pour obtenir des informations générales sur le déploiement et la surveillance des applications, vous pouvez lire les rubriques suivantes :

- [Déployer des applications avec System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Surveiller des applications à partir de la console System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Lors du déploiement et de la surveillance des applications, voici quelques considérations à prendre en compte, spécifiques à la gestion des appareils mobiles.

- Les appareils inscrits auprès de la fonction de gestion des appareils mobiles ne prennent pas en charge les déploiements simulés, l’expérience utilisateur ou les paramètres de planification.

- N’ajoutez pas plus de 100 paramètres régionaux à une seule application. Ajout de paramètres régionaux de plus de 100 empêche l’application de se synchroniser avec Intune. Cette action empêche également l’application en cours d’installation ou disponible pour les installer sur l’appareil.

- Vous pouvez associer le déploiement avec une stratégie de configuration d’application iOS, si vous en avez configuré une. Voir [Appliquer des paramètres aux applications iOS à l’aide de stratégies de configuration d’application dans System Center Configuration Manager](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Étapes suivantes

Peut-être voudrez-vous apporter des modifications à une application, en désinstaller une ou remplacer une application déjà déployée par une nouvelle. Pour comprendre le fonctionnement de ces fonctionnalités, voir [Mettre à jour et mettre hors service des applications avec System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md).
