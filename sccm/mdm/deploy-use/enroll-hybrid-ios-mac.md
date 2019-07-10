---
title: Configurer la gestion hybride des appareils iOS et Mac avec Microsoft Intune
titleSuffix: Configuration Manager
description: Configurez la gestion des appareils iOS avec System Center Configuration Manager et Microsoft Intune.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c6573ce4faf893e30eac070efd963dc7465e20e
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678847"
---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion des appareils iOS hybride avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec Configuration Manager et Intune, vous activez l’inscription d’appareils iOS et Mac OS X pour octroyer l’accès à la messagerie et aux ressources de l’entreprise aux utilisateurs iPhone, iPad et Mac. Une fois que les utilisateurs installent l’application portail d’entreprise Intune, leurs appareils peuvent être ciblés avec la stratégie. Pour pouvoir gérer des appareils iOS et Mac, vous devez importer un certificat des services de notifications Push Apple (APN) provenant d’Apple. Ce certificat permet à Intune de gérer des appareils iOS et Mac en établissant une connexion avec le service de gestion d’appareils Apple.  

 Vous pouvez aussi inscrire des appareils iOS d’entreprise.  Consultez [Inscrire des appareils d’entreprise](enroll-company-owned-devices.md).  

**Conditions préalables**<br>
Avant de pouvoir configurer l’inscription pour une plateforme, tenez compte des prérequis et des procédures figurant dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).

Pour prendre en charge l’inscription d’appareils iOS, procédez comme suit :  

## <a name="download-a-certificate-signing-request"></a>Télécharger une demande de signature de certificat
Un fichier de demande de signature de certificat est nécessaire pour demander un certificat APNs auprès d’Apple.  

1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud**> **Abonnements Microsoft Intune**.  

2.  Sous l’onglet **Accueil** , cliquez sur **Créer une demande de certificat APNs**. La boîte de dialogue **Effectuer une demande de signature de certificat APNs** s'ouvre.  

3.  Cliquez sur**Parcourir** pour accéder à l'emplacement auquel vous souhaitez enregistrer le fichier du nouveau certificat de demande de certificat. Enregistrez localement le fichier de demande de signature de certificat.  

4.  Cliquez sur **Télécharger**. Le nouveau fichier de demander de signature de certificat Microsoft Intune se télécharge et il est enregistré par Configuration Manager. Le fichier de demande de signature de certificat est utilisé pour demander un certificat de relation d'approbation à partir du portail Apple Push Certificates.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Demander un certificat Push MDM Apple
Le certificat MDM Push est utilisé pour établir une relation d’approbation entre le service de gestion, Intune et les appareils mobiles iOS inscrits.  

1.  Dans un navigateur, accédez au [portail Apple Push Certificates](https://identity.apple.com/pushcert) et connectez-vous avec votre ID Apple d’entreprise. Cet ID Apple doit être utilisé ultérieurement pour renouveler votre certificat APNs.  

2.  Terminez l’Assistant en utilisant le fichier (.csr) de demande de signature de certificat. Téléchargez le certificat MDM Push et enregistrez le fichier .pem localement. Ce fichier de certificat (.pem) est utilisé pour établir une relation d’approbation entre le serveur Apple Push Notification et l’autorité de gestion des appareils mobiles Intune.  

> [!NOTE]  
>  Ne chargez pas le certificat APNs sur Intune tant que vous n’avez pas activé l’inscription iOS dans la console Configuration Manager.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Activer l’inscription et charger le certificat MDM Push
Pour activer l’inscription iOS, chargez le certificat APNs.  

1.  Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.  

2.  Sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **iOS**.  

3.  Dans la boîte de dialogue **Propriétés des abonnements Microsoft Intune** , sélectionnez l’onglet **iOS** et cochez la case **Activer l’inscription iOS** .  
4.  Cliquez sur **Parcourir**et accédez au fichier (.cer) du certificat APNs téléchargé à partir d’Apple. Configuration Manager affiche les informations du certificat APNs. Cliquez sur **OK** pour enregistrer le certificat APNs sur Intune.  

Une fois la configuration terminée, vous devez indiquer aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/end-user-educate). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

## <a name="configure-enrollment-restrictions"></a>Configurer les restrictions d’inscription

Vous pouvez limiter les appareils qui peuvent être inscrits en bloquant les appareils personnels. Cela empêche les utilisateurs d’inscrire leur appareil à l’aide du Portail d’entreprise. Si vous bloquez les appareils personnels, seuls les appareils suivants peuvent être inscrits :
- [Appareils prédéclarés](predeclare-devices-with-hardware-id.md)
- [Appareils gérés par Apple Configurator](ios-hybrid-enrollment-using-apple-configurator.md)
- [Appareils gérés par le Programme d’inscription des appareils (DEP)](ios-device-enrollment-program-for-hybrid.md)
- Appareils inscrits avec un [compte de gestionnaire d’inscription des appareils](enroll-devices-with-device-enrollment-manager.md)

### <a name="to-enable-enrollment-restrictions"></a>Activer les restrictions d’inscription
1. Dans la console Configuration Manager, dans l’espace de travail **Administration** , accédez à **Services cloud** > **Abonnement Microsoft Intune**.
2. Sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **iOS**.
3. Choisissez **Bloquer les appareils personnels** pour limiter l’inscription aux appareils d’entreprise.

> [!div class="button"]
> [< Étape précédente](create-service-connection-point.md) [Étape suivante >](set-up-additional-management.md)
