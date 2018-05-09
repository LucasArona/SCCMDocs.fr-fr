---
title: 'Inscrire des appareils d’entreprise '
titleSuffix: Configuration Manager
description: Découvrez les différentes méthodes d’inscription des appareils d’entreprise pour les déploiements hybrides avec Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 36b4169f3bed1957f8ea14159902f408ba642944
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Inscrire des appareils d’entreprise pour les déploiements hybrides avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les appareils d’entreprise ou d’organisation peuvent être gérés de différentes façons en fonction du type de l’appareil et de la méthode utilisée pour son achat.  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Inscrire des appareils iOS à l’aide du programme d’inscription d’appareils DEP  
 Un profil d’inscription « à distance » est déployé sur les appareils ayant été achetés par le biais du programme DEP d’Apple. Quand l’utilisateur exécute l’Assistant Configuration sur l’appareil, cet appareil est automatiquement inscrit dans Intune.  Les appareils inscrits via le programme DEP ne peuvent pas être désinscrits par les utilisateurs. Pour plus d’informations, consultez [Inscription d’appareils iOS via le programme DEP pour les déploiements hybrides avec Configuration Manager](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md).  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Inscrire des appareils iOS à l’aide de l’outil Apple Configurator  
 Avec cette méthode, l’administrateur doit préconfigurer l’inscription de l’appareil iOS après avoir établi une connexion USB entre l’appareil et un ordinateur Mac exécutant Apple Configurator. L’appareil est ensuite remis à l’utilisateur, qui doit exécuter l’Assistant Configuration pour configurer l’appareil avec les informations d’identification de son compte professionnel ou scolaire et terminer le processus d’inscription. Pour plus d’informations, consultez [Inscription d’appareils iOS à l’aide d’Apple Configurator pour les déploiements hybrides avec Configuration Manager](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md).  

## <a name="device-enrollment-manager"></a>Gestionnaire d’inscription d’appareil  
 Les organisations peuvent utiliser Intune pour gérer un grand nombre d’appareils mobiles avec un seul compte d’utilisateur, appelé compte de gestionnaire d’inscription d’appareil. Après avoir créé un compte de gestionnaire d’inscription d’appareil, l’administrateur peut utiliser ce compte s’il a besoin d’inscrire plus de cinq appareils, qui est le nombre autorisé par défaut pour les utilisateurs standard. L’inscription d’appareils à l’aide d’un gestionnaire d’inscription d’appareil est possible uniquement pour les appareils qui ne sont pas dédiés à un utilisateur spécifique. Ces appareils sont appropriés pour les applications de point de vente ou les utilitaires, par exemple, mais ils ne le sont pas pour les utilisateurs qui doivent accéder à leurs e-mails ou à des ressources d’entreprise. Consultez [Inscrire des appareils avec un gestionnaire d’inscription d’appareil à l’aide de Configuration Manager](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md).  

## <a name="user-affinity-for-managed-devices"></a>Affinité utilisateur pour les appareils gérés  
 Quand il configure des profils pour des appareils d’entreprise, l’administrateur peut spécifier si les appareils gérés prennent en charge l’*affinité utilisateur* qui associe un utilisateur spécifique avec l’appareil. Des appareils configurés avec une **affinité utilisateur** peuvent installer et exécuter l’application Portail d’entreprise pour télécharger des applications et gérer des appareils. Consultez [Affinité utilisateur pour les appareils gérés hybrides dans Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md).  

## <a name="manage-devices-with-activation-lock"></a>Gérer des appareils à l’aide du verrou d’activation  
 Microsoft Intune peut vous aider à gérer le verrou d’activation iOS, qui est une fonctionnalité de l’application Rechercher mon iPhone disponible sur les appareils iOS 7.1 et versions ultérieures. Le verrou d'activation est activé automatiquement quand l'application Rechercher mon iPhone est utilisée sur un appareil. Consultez [Gérer le verrou d’activation iOS avec System Center Configuration Manager](../../mdm/deploy-use/manage-ios-activation-lock.md).

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS

Vous pouvez identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity) ou leur numéro de série iOS. Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) contenant les numéros IMEI des appareils ou saisir manuellement les informations sur les appareils.  Pour plus d’informations, consultez [Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).
