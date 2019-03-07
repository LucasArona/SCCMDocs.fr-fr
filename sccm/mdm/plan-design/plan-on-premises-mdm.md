---
title: Planifier la gestion MDM locale
titleSuffix: Configuration Manager
description: Planifier la gestion des appareils mobiles locale gérer des appareils mobiles dans Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb9349a8c3f107f2da139148e4476537fe6aa7ed
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558080"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Plan pour on-premises MDM dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Gestion locale des appareils mobiles (MDM) permet de gérer les appareils mobiles à l’aide des fonctions de gestion intégrées dans le système d’exploitation du périphérique. La fonctionnalité de gestion est basée sur la norme Open Mobile Alliance (OMA) Device Management (DM), et de nombreuses plateformes d’appareils utilisent cette norme pour autoriser la gestion des appareils. Ces appareils sont appelés *des appareils récents* dans la documentation et de la console Configuration Manager. Ce terme les distingue des autres périphériques nécessitant le client Configuration Manager pour les gérer.  

Considérons les exigences suivantes avant de préparer l’infrastructure Configuration Manager pour gérer la gestion MDM locale.



## <a name="bkmk_devices"></a> Appareils pris en charge  

Dans la gestion des appareils mobiles locale, la version Current Branch de Configuration Manager prend en charge l’inscription des appareils exécutant les systèmes d’exploitation suivants :  
  
- Windows 10 Entreprise  
- Windows 10 Professionnel  
- Windows 10 Collaboration   
- Windows 10 Mobile  
- Windows 10 Mobile Entreprise
- Windows 10 IoT Entreprise   



##  <a name="bkmk_intune"></a> L’abonnement Microsoft Intune  

Pour démarrer à l’aide de la gestion MDM locale, vous avez besoin d’un abonnement Microsoft Intune. L’abonnement est nécessaire uniquement pour le suivi des licences des appareils et n’est pas utilisé pour gérer ou pour stocker les informations de gestion pour les appareils. Toutes les données de gestion sont stockées dans votre organisation à l’aide de l’infrastructure de Configuration Manager en local.  

> [!Note]  
> Depuis la version 1810, une connexion Intune n’est plus nécessaire pour les nouveaux déploiements de gestion des appareils mobiles en local.<!--3607730, fka 1359124--> Votre organisation exige toujours des licences Intune pour utiliser cette fonctionnalité. Actuellement impossible de supprimer la connexion Intune à partir des déploiements de gestion des appareils mobiles locaux existants. Pour plus d’informations, consultez le [billet de blog du support Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Si votre site comporte des appareils avec une connectivité internet, le service Intune peut être utilisé pour informer les appareils pour vérifier le périphérique point de gestion des mises à jour de la stratégie. Ce comportement utilise strictement Intune pour la notification des appareils exposés à internet. Les appareils sans connexions internet et qui ne peut pas être contacté par Intune s’appuient sur l’intervalle d’interrogation pour vérifier auprès des rôles de système de site pour les fonctions de gestion.  

> [!TIP]  
> Avant de configurer les rôles de système de site nécessaires, configurez l’abonnement Intune. Cette action réduit le temps nécessaire pour les rôles devenir fonctionnelle.  

Pour plus d’informations sur la façon de configurer l’abonnement Intune, consultez [configurer un abonnement Microsoft Intune pour la gestion MDM locale](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Rôles système de site  

Local MDM requiert au moins un de chacun des rôles de système de site suivants :  

- **Point proxy d’inscription** pour prendre en charge les demandes d’inscription.  

- **Point d’inscription** pour prendre en charge l’inscription des appareils.  

- **Point de gestion du périphérique** pour la remise de la stratégie. Ce rôle de système de site est une variante du rôle de point de gestion qui a été configuré pour autoriser la gestion des appareils mobiles.  

- **Point de distribution** pour la remise du contenu.  

- **Point de connexion de service** pour la connexion à Intune pour informer les appareils à l’extérieur du pare-feu.  

Ces rôles de système de site peuvent être installés sur le serveur de système de site unique ou peuvent être exécutés séparément sur des serveurs différents en fonction des besoins de votre organisation. Chaque serveur de système de site utilisé pour la gestion MDM locale doit être configuré en tant que point de terminaison HTTPS pour communiquer avec les appareils approuvés. Pour plus d'informations, voir [Communications fiables requises](#bkmk_trustedComs).  

Pour plus d’informations sur la planification pour les rôles de système de site, consultez [planifier les rôles et les serveurs de système de site pour Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

Pour plus d’informations sur la façon d’ajouter les rôles de système de site nécessaires, consultez [installer des rôles de système de site pour la gestion MDM locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a> Communications fiables  

Gestion des appareils mobiles locale nécessite les rôles de système de site doit être activé pour les communications HTTPS. Selon vos besoins, vous pouvez utiliser l’autorité de certification de votre entreprise (CA) pour établir les connexions approuvées entre serveurs et périphériques. Vous pouvez également utiliser une autorité de certification publiquement disponible à l’autorité de confiance. Dans les deux cas, vous devez un certificat de serveur web à configurer dans IIS sur les serveurs de système de site hébergeant les rôles de système de site nécessaires. Vous devez également le certificat racine de cette autorité de certification installé sur les appareils qui doivent se connecter à ces serveurs.  

Si l’autorité de certification de votre entreprise vous permet d’établir des communications approuvées, procédez comme suit :  

- Créer et émettre le modèle de certificat de serveur web sur l’autorité de certification.  

- Demander un certificat de serveur web pour chaque serveur de système de site hébergeant un rôle de système de site nécessaire.  

- Configurer IIS sur le serveur de système de site pour utiliser le certificat de serveur web demandé.  

Pour les appareils joints au domaine Active Directory d’entreprise, le certificat racine de l’autorité de certification d’entreprise est déjà disponible sur l’appareil pour les connexions approuvées. Ce comportement signifie que les appareils joints au domaine sont automatiquement approuvés pour les connexions HTTPS avec les serveurs de système de site. Toutefois, les appareils non joints au domaine n’automatiquement installer le certificat racine requis. Pour communiquer avec les serveurs de système de site prenant en charge la gestion MDM locale, les appareils non joints au domaine tels que les appareils mobiles vous obligent à installer manuellement le certificat racine sur ces derniers.  

Exporter le certificat racine de l’autorité de certification émettrice pour une utilisation par les différents appareils. Pour obtenir le fichier de certificat racine, vous pouvez l’exporter à l’aide de l’autorité de certification. Une autre méthode consiste à utiliser le certificat de serveur web émis par l’autorité de certification pour extraire la racine et créer un fichier de certificat racine. Ensuite, le certificat racine doit être remis à l’appareil. Certains exemples de méthodes de remise sont les suivantes :

- Système de fichiers  

- Pièce jointe  

- Carte mémoire  

- Périphérique attaché  

- Stockage cloud (tel que OneDrive)  

- Connexion NFC (communication en champ proche)  

- Lecteur de code-barres  

- Package d’approvisionnement OOBE (Out of Box Experience)  

Pour plus d’informations, consultez [configurer des certificats pour les communications approuvées dans la gestion MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> Inscription d’appareils

Pour activer l’inscription des appareils mobiles en local,
- Les utilisateurs doivent être autorisés à inscrire 
- Appareils doivent être configurés pour les communications approuvées avec les serveurs de système de site hébergeant les rôles requis  

Autoriser les utilisateurs à inscrire des appareils en configurant un profil d’inscription dans les paramètres du client Configuration Manager. Vous pouvez utiliser les paramètres de client par défaut pour envoyer le profil d’inscription à tous les utilisateurs détectés. Vous pouvez également définir le profil d’inscription dans les paramètres client personnalisés et pousser les paramètres vers un ou plusieurs regroupements d’utilisateurs.  

Une fois que les utilisateurs sont autorisés, ils peuvent inscrire leurs propres appareils. Pour vous inscrire, le périphérique l’utilisateur doit avoir le certificat racine de l’autorité de certification (CA) qui a émis le certificat de serveur web utilisé sur les serveurs de système de site hébergeant les rôles requis.  

Comme alternative à l’inscription initiée par l’utilisateur, vous pouvez configurer un package d’inscription en bloc. Ce package permet à l’appareil d’être inscrits sans intervention de l’utilisateur. Il peut être remis à l’appareil avant qu’il est configuré pour une utilisation ou issue du processus OOBE.  

Pour plus d’informations sur la façon de configurer et inscrire des appareils, consultez les articles suivants : 

- [Configurer l’inscription d’appareil pour la gestion MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Inscrire des appareils pour la gestion MDM locale](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

