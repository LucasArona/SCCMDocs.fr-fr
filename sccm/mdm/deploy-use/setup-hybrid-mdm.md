---
title: Configurer la gestion hybride MDM
titleSuffix: Configuration Manager
description: Configurez une inscription d’appareils hybride avec Configuration Manager et Intune.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a69f849d4843ff7a0cf7df4a0b6de044a9506301
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421805"
---
# <a name="set-up-hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Configurer MDM hybride avec Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*


Avant de pouvoir gérer des appareils iOS, Windows et Android avec Configuration Manager, vous devez les inscrire dans Intune. Effectuez les étapes suivantes pour configurer une inscription d’appareils hybride avec Configuration Manager via Intune. En effectuant les étapes suivantes, vous allez activer l’inscription BYOD (« Apportez votre propre appareil ») pour vos utilisateurs. Ces étapes sont également des conditions préalables pour [l’inscription d’appareils BYOD](enroll-hybrid-ios-mac.md) et [l’inscription d’appareils appartenant à l’entreprise](enroll-company-owned-devices.md).

> [!Important]  
> Depuis le 14 août 2018, la gestion hybride des appareils mobiles est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, consultez [Qu’est-ce que la gestion MDM hybride ?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="set-up-steps"></a>Étapes de configuration

 |Étapes|Détails|  
 |-----------|-------------|  
 |**Étape 1 :** [Créer un regroupement MDM](create-mdm-collection.md)|Créez un regroupement d’utilisateurs Configuration Manager comprenant les utilisateurs dont les appareils peuvent être inscrits|  
 |**Étape 2 :** [Exigences relatives aux noms de domaine](confirm-dns.md)|Vérifiez que le service de nom de domaine (DNS) de votre organisation et la gestion des utilisateurs Active Directory répondent aux critères MDM|
 |**Étape 3 :** [Configurer l’abonnement Intune](configure-intune-subscription.md)|Le service Intune vous permet de gérer des appareils via Internet.|  
 |**Étape 4 :** [Ajouter des conditions générales](terms-and-conditions.md)| Créez des conditions générales que les utilisateurs doivent accepter pour pouvoir utiliser l’application Portail d’entreprise|
 |**Étape 5 :** [Créer un point de connexion de service](create-service-connection-point.md)|Le point de connexion de service envoie des informations sur les paramètres et le déploiement des logiciels à Configuration Manager. De plus, il récupère les messages d’état et d’inventaire à partir des appareils mobiles. |  
 |**Étape 6 :** [Activer l’inscription de la plateforme](enable-platform-enrollment.md)|L’inscription des appareils iOS et Windows à des fins de gestion des appareils mobiles nécessite des étapes supplémentaires pour l’établissement de la communication entre le service et les appareils. Android ne nécessite aucune configuration supplémentaire.|  
 |**Étape 7 :** [Configurer une gestion supplémentaire](set-up-additional-management.md)|(Facultatif) Configurer les éléments de configuration et l’accès conditionnel des appareils inscrits|
 |**Étape 8 :** [Vérifier la configuration MDM](verify-mdm-configuration.md)|Affichez les fichiers journaux pour vérifier que le point de connexion de service a été créé et que les comptes d’utilisateur se synchronisent.|



## <a name="enroll-devices"></a>Inscrire des appareils

Une fois la configuration de la gestion hybride terminée, les appareils peuvent être inscrits dans Configuration Manager de plusieurs manières :

- **Entreprise (COD) les appareils :** [Inscrire des appareils d’entreprise](enroll-company-owned-devices.md) fournit des conseils sur les différentes façons de spécifique à la plateforme d’inscrire des appareils d’entreprise  

- **Appareils (BYOD) appartenant à l’utilisateur :** [Inscrire les appareils (BYOD) utilisateur](enroll-hybrid-ios-mac.md) fournit des conseils sur les moyens d’inscrire des appareils appartenant à l’utilisateur  



## <a name="see-also"></a>Voir aussi

Vous recherchez Intune sans Configuration Manager ?
> [!div class="button"]
> [Afficher les documents relatifs à Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


