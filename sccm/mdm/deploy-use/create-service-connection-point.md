---
title: Créer un point de connexion de service
titleSuffix: Configuration Manager
description: Créez un point de connexion de service via System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12626a734138094e7558617b714b2b5acdac6450
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424313"
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>Créer un point de connexion de service via System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir créé votre abonnement, vous pouvez installer le rôle de système de site de point de connexion de service, qui vous permet de vous connecter au service Intune. Ce rôle de système de site envoie les paramètres et les applications au service Intune.

 Le point de connexion de service envoie des informations sur les paramètres et le déploiement des logiciels à Configuration Manager. De plus, il récupère les messages d’état et d’inventaire à partir des appareils mobiles. Le service Configuration Manager joue le rôle d’une passerelle qui communique avec les appareils mobiles et stocke les paramètres.

> [!NOTE]
>  Le rôle de système de site de point de connexion de service ne peut être installé que sur le site d’administration centrale ou un site principal autonome. Le point de connexion de service doit avoir accès à Internet.


## <a name="configure-the-service-connection-point-role"></a>Configurer le rôle de point de connexion de service

1.  Dans la console Configuration Manager, cliquez sur **Administration**.

2.  Dans l’espace de travail **Administration**, développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.

3.  Ajoutez le rôle **Point de connexion de service** à un serveur de système de site nouveau ou existant en suivant l’étape correspondante :

    -   Nouveau serveur de système de site : Sur le **accueil** sous l’onglet le **créer** de groupe, cliquez sur **créer un serveur de système de Site** pour démarrer l’Assistant Création d’une serveur de système de Site.

    -   Serveur de système de site existant : Cliquez sur le serveur sur lequel vous souhaitez installer le rôle de point de connexion de service. Ensuite, sous l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site** pour démarrer l'Assistant Ajout des rôles de système de site.

4.  Dans la page **Sélection du rôle système** , sélectionnez **Point de connexion de service**, puis cliquez sur **Suivant**.
![Créer un point de connexion de service](../media/mdm-service-connection-point.png)

* Effectuez toutes les étapes de l'Assistant.

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Comment le point de connexion de service s’authentifie-t-il auprès du service Microsoft Intune ?
 Le point de connexion de service étend les fonctionnalités de Configuration Manager en se connectant au service cloud Intune qui gère les appareils mobiles via Internet. Le point de connexion de service s’authentifie auprès du service Intune comme suit :

1.  Quand vous créez un abonnement Intune dans la console Configuration Manager, l’administrateur Configuration Manager est authentifié en se connectant à Azure Active Directory, qui effectue une redirection vers le serveur ADFS approprié pour demander le nom d’utilisateur et le mot de passe. Intune délivre ensuite un certificat au locataire.

2.  Le certificat de l’étape 1 est installé sur le rôle de site de point de connexion de service et il est utilisé pour authentifier et autoriser toutes les communications ultérieures avec le service Microsoft Intune.

> [!div class="button"]
> [< Étape précédente](terms-and-conditions.md) [Étape suivante >](enable-platform-enrollment.md)
