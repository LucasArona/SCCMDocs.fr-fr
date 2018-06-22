---
title: Configurer une gestion hybride des appareils mobiles
titleSuffix: Configuration Manager
description: Configurez une inscription d’appareils hybride avec Configuration Manager et Intune.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbc5b9abf63d95185795716cfcb9ebfaf3e2ec3d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347074"
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer une gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*


Avant de pouvoir gérer des appareils iOS, Windows et Android avec Configuration Manager, vous devez les inscrire dans Intune. Effectuez les étapes suivantes pour configurer une inscription d’appareils hybride avec Configuration Manager via Intune. En effectuant les étapes suivantes, vous allez activer l’inscription BYOD (« Apportez votre propre appareil ») pour vos utilisateurs. Ces étapes sont également des conditions préalables pour [l’inscription d’appareils BYOD](enroll-hybrid-ios-mac.md) et [l’inscription d’appareils appartenant à l’entreprise](enroll-company-owned-devices.md).

 |Étapes|Détails|  
 |-----------|-------------|  
 |**Étape 1 :** [Créer un regroupement MDM](create-mdm-collection.md)|Créez un regroupement d’utilisateurs Configuration Manager comprenant les utilisateurs dont les appareils peuvent être inscrits|  
 |**Étape 2 :** [Respecter les critères pour les noms de domaine](confirm-dns.md)|Vérifiez que le service de nom de domaine (DNS) de votre organisation et la gestion des utilisateurs Active Directory répondent aux critères MDM|
 |**Étape 3 :** [Configurer l’abonnement Intune](configure-intune-subscription.md)|Le service Intune vous permet de gérer des appareils via Internet.|  
 |**Étape 4 :** [Ajouter les conditions générales](terms-and-conditions.md)| Créez des conditions générales que les utilisateurs doivent accepter pour pouvoir utiliser l’application Portail d’entreprise|
 |**Étape 5 :** [Créer un point de connexion de service](create-service-connection-point.md)|Le point de connexion de service envoie des informations sur les paramètres et le déploiement des logiciels à Configuration Manager. De plus, il récupère les messages d’état et d’inventaire à partir des appareils mobiles. |  
 |**Étape 6 :** [Activer l’inscription de la plateforme](enable-platform-enrollment.md)|L’inscription des appareils iOS et Windows à des fins de gestion des appareils mobiles nécessite des étapes supplémentaires pour l’établissement de la communication entre le service et les appareils. Android ne nécessite aucune configuration supplémentaire.|  
 |**Étape 7 :** [Configurer une gestion supplémentaire](set-up-additional-management.md)|(Facultatif) Configurer les éléments de configuration et l’accès conditionnel des appareils inscrits|
 |**Étape 8 :** [Vérifier la configuration MDM](verify-mdm-configuration.md)|Affichez les fichiers journaux pour vérifier que le point de connexion de service a été créé et que les comptes d’utilisateur se synchronisent.|

Vous recherchez Intune sans Configuration Manager ?
> [!div class="button"]
[Afficher les documents relatifs à Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Inscrire des appareils
Une fois la configuration de la gestion hybride terminée, les appareils peuvent être inscrits dans Configuration Manager de plusieurs manières :
- **Appareils appartenant à l’entreprise :** dans la section décrivant [l’inscription des appareils appartenant à l’entreprise](enroll-company-owned-devices.md), vous trouverez de l’aide sur les différents moyens d’inscrire des appareils appartenant à l’entreprise, en fonction des plateformes.
- **Appareils appartenant aux utilisateurs (BYOD) :** la section relative à [l’inscription des appareils appartenant aux utilisateurs (BYOD)](enroll-hybrid-ios-mac.md) fournit des informations sur les différentes méthodes d’inscription d’appareils appartenant à l’utilisateur.
