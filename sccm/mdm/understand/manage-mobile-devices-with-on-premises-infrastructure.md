---
title: Gestion des appareils mobiles locale
titleSuffix: Configuration Manager
description: En savoir plus sur la gestion des appareils mobiles locale, une solution de gestion de périphérique dans Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49e07a7ebe6ec53d61ea9e2ee3bc941dd8561094
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558216"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>On-premises MDM dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager local gestion des appareils mobiles (MDM) est une solution de gestion de périphérique qui s’appuie sur les capacités intégrées de gestion de périphérique du système d’exploitation. Cette fonctionnalité est basée sur la norme Open Mobile Alliance (OMA) Device Management (DM). Il utilise l’infrastructure de gestionnaire de Configuration de votre organisation pour gérer et maintenir les appareils. En local MDM nécessite Microsoft Intune pour configurer la fonctionnalité de gestion, mais il est uniquement nécessaire pour l’abonnement. Intune est parfois utilisé pour aider à informer les appareils pour archiver les modifications de stratégie, mais il n’est pas utilisé pour gérer les appareils ou stocker des données à leur sujet.  

![Concept de la gestion locale](media/On-premises-conceptual.png)  

Gestion des appareils mobiles locale différent de Microsoft Intune, ce qui s’appuie également sur les fonctionnalités OMA DM intégrées. Toutes les fonctions de gestion dans Intune sont fournis par les services cloud. Gestion des appareils mobiles locale différent également de la solution de gestion basée sur le client habituellement offerte par Configuration Manager. Il s’appuie sur une infrastructure similaire, mais n’utilise pas le logiciel client installé séparément sur les appareils qu’il gère.  

> [!Note]  
> Depuis la version 1810, une connexion Intune n’est plus nécessaire pour les nouveaux déploiements de gestion des appareils mobiles en local.<!--3607730, fka 1359124--> Votre organisation exige toujours des licences Intune pour utiliser cette fonctionnalité. Actuellement impossible de supprimer la connexion Intune à partir des déploiements de gestion des appareils mobiles locaux existants. Pour plus d’informations, consultez le [billet de blog du support Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Le tableau suivant répertorie les avantages et inconvénients de la gestion MDM locale par rapport à la gestion basée sur le client classique :  

|Avantages|Inconvénients|  
|----------------|-------------------|  
|**Une infrastructure simplifiée** : nécessite moins de rôles système de site.<br /><br /> **Plus facile à maintenir** - parce que les fonctionnalités de gestion sont intégrée dans le système d’exploitation du périphérique, nouvelles versions du logiciel client n’est pas obligatoire lorsque nouvelles fonctionnalités de gestion sont introduites dans le système de Configuration Manager.<br /><br /> **Local** : la gestion et les données sont conservées en local.|**Moins de fonctionnalités de gestion de clients** : absence d’orchestration, de contrôle de logiciel, d’intégration tierce, de séquencement de tâches ou de prise en charge du Centre logiciel.<br /><br /> **Prise en charge de l’appareil limitée** - actuellement sur site MDM seulement prend en charge les appareils exécutant Windows 10 et Windows 10 Mobile.|  

Les articles suivants fournissent des informations que vous pouvez utiliser pour planifier, préparer et inscrire des appareils pour la gestion MDM locale :  

- [Planifier la gestion MDM locale](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    En savoir plus sur les éléments à prendre en compte lorsque configuration de l’infrastructure Configuration Manager et la planification de l’inscription d’appareils dans locale des appareils mobiles.  

- [Étapes de préparation pour la gestion MDM locale](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Préparer la Configuration Manager pour la gestion MDM locale. Configuration de l’abonnement Microsoft Intune, configurer des certificats, installer des rôles de système de site et configurer l’inscription d’appareil.  

- [Inscrire des appareils pour la gestion MDM locale](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Découvrez comment se produit l’inscription, comment les utilisateurs peuvent inscrire leurs propres appareils et comment inscrire des appareils en bloc avec un package d’inscription.  

