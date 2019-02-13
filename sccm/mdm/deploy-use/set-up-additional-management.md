---
title: Configurer une gestion supplémentaire
titleSuffix: Configuration Manager
description: Configurez des solutions de gestion supplémentaires via System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4877d674-6bbc-4e16-810c-daad70c74daa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d866ce901640b6e7fafb13a6c24318f26c5d5feb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131793"
---
# <a name="set-up-additional-management-with-system-center-configuration-manager"></a>Configurer des solutions de gestion supplémentaires grâce à System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

(Facultatif) Vous pouvez configurer une gestion supplémentaire avant l’inscription des appareils. Ces solutions de gestion peuvent être créées et déployées après l’inscription des appareils, même si de nombreuses organisations préfèrent les déployer au fur et à mesure que les appareils sont intégrés à la gestion.

Les **éléments de configuration** vous permettent de gérer des paramètres tels que l’exigence d’un code confidentiel (PIN) ou d’un chiffrement sur les appareils inscrits, en fonction de leur plateforme :
- [Appareils Windows 10 et Windows 8.1](create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Appareils Windows Phone](create-configuration-items-for-windows-phone-devices-managed-without-the-client.md)
- [Appareils iOS et Mac](create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)
- [Appareils Android et Samsung KNOX Standard](create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)

**Les applications**  peuvent être déployées sur des appareils gérés :
- [Applications iOS](creating-ios-applications.md)
- [Applications Mac](../../apps/get-started/creating-mac-computer-applications.md)
- [Applications Windows (PC)](../../apps/get-started/creating-windows-applications.md)
- [Applications Windows Phone](creating-windows-phone-applications.md)
- [Applications Android](creating-android-applications.md)

L’**accès conditionnel** vous permet de gérer l’accès aux ressources de l’entreprise, notamment :  
- [Accès à l’e-mail](manage-email-access.md)
- [Accès à SharePoint](manage-sharepoint-online-access.md)
- [Accès à Skype Entreprise](manage-skype-for-business-online-access.md)
- [Dynamics CRM Online](manage-dynamics-crm-online-access.md)

**L’authentification multifacteur (MFA)** vous permet de demander l’utilisation de plusieurs méthodes de vérification, ce qui permet d’appliquer une deuxième couche critique de sécurité aux transactions et connexions utilisateur.
Auparavant, vous deviez accéder à la console Intune ou à la console Configuration Manager pour définir l’authentification multifacteur pour les inscriptions Intune. Désormais, vous pouvez vous connecter au [portail Microsoft Azure](https://manage.windowsazure.com) en utilisant vos informations d’identification Intune et configurer les paramètres de l’authentification multifacteur via Azure AD. Pour en savoir plus, voir [Authentification multifacteur pour les inscriptions d’appareils Intune](https://aka.ms/mfa_ad).

> [!div class="button"]
> [< Étape précédente](enable-platform-enrollment.md) [Étape suivante >](verify-mdm-configuration.md)
