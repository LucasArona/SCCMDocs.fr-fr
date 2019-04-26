---
title: Préparer pour la gestion MDM locale
titleSuffix: Configuration Manager
description: Préparer la gestion des appareils avec gestion locale des appareils mobiles dans Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1ef60106-8f31-46d6-95a6-25a6495f22c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fad5ce96b84b5a6edfafdead64cff0223009ebf8
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62288641"
---
# <a name="preparation-steps-for-on-premises-mdm-in-configuration-manager"></a>Étapes de préparation pour MDM en local dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour gérer les appareils avec gestion des appareils mobiles sur site Configuration Manager (MDM), d’abord configurer l’infrastructure nécessaire. Les rôles de système de site nécessaires doivent communiquer sur un canal fiable avec les appareils mobiles. Ces rôles incluent le point proxy d’inscription, le point d’inscription, le point de gestion de périphérique et le point de distribution.

Les tâches principales suivantes sont requises pour préparer des applications MDM locales Configuration Manager :  

- [Configurer un abonnement Microsoft Intune pour la gestion MDM locale](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm)  

    S’inscrire à Microsoft Intune, puis ajouter l’abonnement à Configuration Manager via la console Configuration Manager. Cette étape est nécessaire uniquement pour la licence. Intune n’est pas utilisé pour gérer les appareils ou stocker des informations de gestion. La coordination et la gestion des appareils est entièrement assurée dans votre entreprise à l’aide de l’infrastructure Configuration Manager locale.  

    > [!Note]  
    > Depuis la version 1810, une connexion Intune n’est plus nécessaire pour les nouveaux déploiements de gestion des appareils mobiles en local.<!--3607730, fka 1359124--> Votre organisation exige toujours des licences Intune pour utiliser cette fonctionnalité. À l’heure actuelle, il n’est pas possible de supprimer la connexion Intune des déploiements MDM locaux existants. Pour plus d’informations, consultez le [billet de blog du support Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

- [Installer des rôles de système de site pour la gestion MDM locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm)  

    Installer et configurer les systèmes de site nécessaires pour gérer les appareils avec une infrastructure de Configuration Manager en local. Au minimum, cette fonctionnalité requiert le point proxy d’inscription, point d’inscription, point de gestion de périphérique et les rôles de point de distribution.  

- [Configurer des certificats pour les communications approuvées pour la gestion MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  

    Configurer l’infrastructure de Configuration Manager en local pour autoriser les communications fiables (HTTPS) entre les appareils gérés et les serveurs hébergeant les rôles de système de site nécessaires.  

- [Configurer l’inscription d’appareil pour la gestion MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

    Autoriser les utilisateurs à inscrire des ordinateurs et périphériques. Installez le certificat racine approuvé sur les appareils pour autoriser des connexions HTTPS pour les serveurs de système de site. Ces appareils ne sont pas joints au domaine.  

