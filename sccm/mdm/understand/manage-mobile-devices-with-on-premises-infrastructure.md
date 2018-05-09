---
title: Gestion locale des appareils mobiles
titleSuffix: Configuration Manager
description: Découvrez comment utiliser la gestion des appareils mobiles locale, une méthode de gestion d’appareils disponible dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ac0e4426b2025a88f126f9cc0b2e57f5a5313740
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Gestion des appareils mobiles (MDM) locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion des appareils mobiles (MDM) locale est une solution de gestion d’appareils disponible dans System Center Configuration Manager. Elle s’appuie sur les fonctionnalités de gestion intégrées aux systèmes d’exploitation des appareils (basées sur la norme de gestion d’appareils mobiles OMA DM) quand la gestion et la maintenance des appareils s’effectue via l’infrastructure Configuration Manager d’une entreprise. La gestion d’appareils mobiles locale a besoin de Microsoft Intune pour configurer les fonctions de gestion, mais uniquement pour les abonnements (et parfois pour envoyer des notifications aux appareils leur demandant de s’enregistrer quand des stratégies sont modifiées). Par contre, elle n’en a pas besoin pour gérer les appareils ni pour stocker les données les concernant.  

 ![Concept de la gestion locale](media/On-premises-conceptual.png)  

 La gestion d’appareils mobiles locale diffère de Microsoft Intune qui, tout en s’appuyant aussi sur les fonctionnalités OMA DM intégrées, fournit toutes les fonctions de gestion via des services cloud.  La gestion d’appareils mobiles locale se distingue aussi de la solution de gestion basée sur le client classique de Configuration Manager, car même si elle s’appuie sur une infrastructure d’entreprise analogue, elle n’utilise pas de logiciels clients installés séparément sur les ordinateurs et appareils qu’elle gère.  

 Le tableau ci-dessous indique les avantages et les inconvénients de la gestion d’appareils mobiles locale par rapport à la gestion classique basée sur le client :  

|Avantages|Inconvénients|  
|----------------|-------------------|  
|**Une infrastructure simplifiée** : nécessite moins de rôles système de site.<br /><br /> **Une maintenance plus facile** : dans la mesure où les fonctionnalités de gestion sont intégrées au système d’exploitation des appareils, le recours aux nouvelles versions du logiciel client n’est pas obligatoire quand de nouvelles fonctionnalités de gestion sont introduites dans le système Configuration Manager.<br /><br /> **Local** : la gestion et les données sont conservées en local.|**Moins de fonctionnalités de gestion de clients** : absence d’orchestration, de contrôle de logiciel, d’intégration tierce, de séquencement de tâches ou de prise en charge du Centre logiciel.<br /><br /> **Prise en charge d’appareils limitée** : actuellement, la gestion d’appareils mobiles locale est disponible uniquement pour les appareils exécutant Windows 10 et Windows 10 Mobile.|  

 Les rubriques suivantes contiennent des informations utiles pour planifier, préparer et inscrire des appareils pour la gestion d’appareils mobiles locale :  

-   [Planifier la gestion des appareils mobiles locale dans System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Découvrez les points à prendre en compte pour configurer l’infrastructure Configuration Manager et planifier l’inscription des appareils pour la gestion d’appareils mobiles locale.  

-   [Étapes de préparation pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Découvrez comment préparer le système Configuration Manager pour la gestion d’appareils mobiles locale, notamment comment configurer l’abonnement à Microsoft Intune, configurer des certificats, installer des rôles de système de site et configurer l’inscription des appareils.  

-   [Inscrire des appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Découvrez comment se produit l’inscription, comment les utilisateurs peuvent inscrire leurs propres appareils et comment inscrire des appareils en bloc avec un package d’inscription.  
