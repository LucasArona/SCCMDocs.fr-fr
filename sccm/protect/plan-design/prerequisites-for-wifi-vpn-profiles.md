---
title: Prérequis des profils Wi-Fi et VPN
titleSuffix: Configuration Manager
description: Découvrez les autorisations de sécurité nécessaires pour gérer des profils de certificat, des profils Wi-Fi et des profils VPN dans System Center Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9cf922f99ade06459a785e54775a9aedfd8e7a23
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414546"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Prérequis des profils Wi-Fi et VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils Wi-Fi et VPN dans System Center Configuration Manager ont uniquement des dépendances au sein du produit.  

 Vous devez disposer des autorisations de sécurité suivantes pour gérer les paramètres d'accès aux ressources de l'entreprise, par exemple, les profils de certificat, les profils Wi-Fi et les profils VPN :  

- Pour voir et gérer les alertes et rapports pour le Wi-Fi et les profils : **Créer**, **Supprimer**, **Modifier**, **Modifier le rapport**, **Lecture**et **Exécuter le rapport** pour l’objet **Alertes**.  

- Pour créer et gérer des profils de certificat : **Créer une stratégie**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Profil de certificat**.  

- Pour gérer les déploiements de profil Wi-Fi, VPN et de certificat : **Déployer des stratégies de configuration**, **Modifier l’alerte relative à l’état du client**, **Lecture** et **Lire la ressource** pour l’objet **Collection**.  

- Pour gérer toutes les stratégies de configuration : **Créer**, **Supprimer**, **Modifier**, **Lecture** et **Définir l’étendue de sécurité** pour l’objet **Stratégie de configuration**.  

- Pour exécuter des requêtes liées aux profils Wi-Fi et VPN : Autorisation **Lecture** pour l’objet **Requête**.  

- Pour afficher des informations sur les profils Wi-Fi et VPN dans la console System Center Configuration Manager : Autorisation de Lecture **pour l'objet Site**.  

- Pour voir les messages d’état pour les profils Wi-Fi et VPN : Autorisation **Lecture** pour l’objet **Messages d’état**.  

- Pour créer et modifier le profil de certificat d'Autorité de certification approuvé : **Créer une stratégie**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Profil de certificat d’Autorité de certification approuvé**.  

- Pour créer et gérer les profils VPN : **Créer une stratégie**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Profil VPN**.  

- Pour créer et gérer les profils Wi-Fi : **Créer une stratégie**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Profil Wi-Fi**.  

  Le rôle de sécurité **Gestionnaire d’accès aux ressources de l’entreprise** intègre les autorisations permettant de gérer les profils Wi-Fi dans System Center Configuration Manager. Pour plus d’informations, consultez [Configurer la sécurité dans System Center Configuration Manager](../../core/plan-design/security/configure-security.md).
