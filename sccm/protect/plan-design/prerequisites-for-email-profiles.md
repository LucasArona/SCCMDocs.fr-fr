---
title: Conditions préalables pour les profils de messagerie
titleSuffix: Configuration Manager
description: Découvrez les profils de messagerie dans System Center Configuration Manager et leurs dépendances externes et internes au produit.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 58e1f4b56c99cf29c112773b2a82c70695e58744
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="email-profile-prerequisites"></a>Conditions préalables pour les profils de messagerie

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils de messagerie dans System Center Configuration Manager ont des dépendances à la fois externes et internes au produit.  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Des autorisations de sécurité spécifiques doivent avoir été accordées pour gérer les profils de messagerie.|Vous devez disposer des autorisations de sécurité suivantes pour gérer les paramètres d'accès aux ressources entreprise, telles que les profils de messagerie :<br /><br /> - Pour afficher et gérer les alertes et les rapports pour les profils de messagerie : autorisations **Créer**, **Supprimer**, **Modifier**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Alertes**.<br /><br /> - Pour créer et gérer des profils de certificat : autorisations **Créer une stratégie**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Profil de certificat**.<br /><br /> Pour gérer les déploiements de profils de messagerie : autorisations **Déployer des stratégies de configuration**, **Modifier l’alerte relative à l’état du client**, **Lecture** et **Lire la ressource** pour l’objet **Regroupement**.<br /><br /> - Pour gérer toutes les stratégies de configuration : autorisations **Créer**, **Supprimer**, **Modifier**, **Lecture** et **Définir l’étendue de sécurité** pour l’objet **Stratégie de configuration**.<br /><br /> - Pour exécuter des requêtes liées aux profils de messagerie : autorisation **Lecture** pour l’objet **Requête**.<br /><br /> - Pour afficher les informations sur les profils de messagerie dans la console System Center Configuration Manager : autorisation **Lecture** pour l’objet **Site**.<br /><br /> - Pour afficher les messages d’état pour les profils de messagerie : autorisation **Lecture** pour l’objet **Messages d’état**.<br /><br /> - Pour créer et gérer des profils de messagerie : autorisations **Créer une stratégie**, **Modifier le rapport**, **Lecture** et **Exécuter le rapport** pour l’objet **Profil de préparation des communications**.<br /><br /> Le rôle de sécurité **Gestionnaire d’accès aux ressources de l’entreprise** intègre les autorisations permettant de gérer les profils de messagerie dans System Center Configuration Manager. Pour plus d’informations, consultez [Configurer la sécurité dans System Center Configuration Manager](../../core/plan-design/security/configure-security.md).|  
|Attribut de messagerie dans Active Directory|Si vous souhaitez générer l’adresse email des utilisateurs dans un profil de messagerie en utilisant l’adresse SMTP principale de l’utilisateur, la découverte d’utilisateur System Center Configuration Manager doit être configurée pour détecter l’attribut **mail** à partir d’Active Directory (ceci est configuré par défaut).|  

## <a name="external-dependencies"></a>Dépendances externes  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Attribut de messagerie dans Active Directory|Si vous souhaitez générer l’adresse email des utilisateurs dans un profil de messagerie à l’aide de l’adresse SMTP principale de l’utilisateur, cette adresse doit exister dans l’attribut **mail** dans Active Directory.<br /><br /> Pour plus d'informations, consultez la documentation de Windows Server.|
