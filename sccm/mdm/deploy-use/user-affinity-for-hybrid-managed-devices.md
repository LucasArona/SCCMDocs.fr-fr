---
title: Affinité utilisateur pour les appareils gérés hybrides
titleSuffix: Configuration Manager
description: Configurez l’affinité utilisateur pour les appareils gérés dans Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b5d520a7-e9e5-40ee-91f9-f2684214beb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 11b448d27dbf639eaccf0f41ed97b7961a01adb6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="user-affinity-for-hybrid-managed-devices-in-configuration-manager"></a>Affinité utilisateur pour les appareils gérés hybrides dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous configurez des profils pour des appareils d’entreprise, l’administrateur peut spécifier si les appareils gérés peuvent avoir une *affinité utilisateur* qui identifie un utilisateur spécifique avec l’appareil.  

##  <a name="BKMK_iOSCP"></a> Appareils gérés avec une affinité utilisateur  
 Des appareils configurés avec une **affinité utilisateur** peuvent installer et exécuter l’application Portail d’entreprise pour télécharger des applications et gérer des appareils. Lorsque les utilisateurs reçoivent leurs appareils, ils doivent effectuer un certain nombre d’étapes supplémentaires pour achever l’exécution de l’Assistant Installation et installer l’application Portail d’entreprise.  

#### <a name="how-to-enroll-ios-devices-with-user-affinity"></a>Comment inscrire des appareils iOS avec une affinité utilisateur  

1.  Quand les utilisateurs mettent sous tension leurs nouveaux appareils pour la première fois, ils sont invités à exécuter l’Assistant Configuration. Le profil d’inscription peut spécifier de demander des informations d’identification lors de la configuration. Les utilisateurs doivent utiliser les informations d’identification (c’est-à-dire le nom d’utilisateur principal, ou UPN) associées à leur abonnement dans Intune.  

2.  Pendant la configuration, les utilisateurs peuvent également être invités à fournir un ID Apple. Un ID Apple doit être fourni avant que l’appareil puisse installer le portail d’entreprise. Les utilisateurs peuvent fournir un ID Apple une fois la configuration terminée, à partir du menu **Paramètres** d’iOS.  

3.  Une fois la configuration terminée, l’appareil iOS doit installer l’application Portail d’entreprise à partir de l’App Store ; par exemple, [Application Portail d’entreprise](https://itunes.apple.com/us/app/id719171358).  

4.  L’utilisateur peut désormais se connecter au portail d’entreprise avec l’UPN utilisé lors de la configuration de l’appareil.  

5.  Une fois connecté, l’utilisateur est invité à inscrire son appareil. La première étape consiste à **identifier l’appareil**. L’application présente la liste des appareils iOS inscrits par l’entreprise et affectés au compte Intune de l’utilisateur final. Choisissez l’appareil approprié.  

     Si cet appareil n’est pas encore inscrit par l’entreprise, sélectionnez « Nouveau périphérique » pour poursuivre le flux d’inscription standard.  

6.  Sur l’écran suivant, l’utilisateur doit confirmer le numéro de série du nouvel appareil. L’utilisateur peut appuyer sur le lien « Confirmez le numéro de série » pour lancer l’application Paramètres afin de vérifier le numéro de série. L’utilisateur doit ensuite entrer les 4 derniers caractères du numéro de série dans l’application Portail d’entreprise.  

     Cette étape vérifie que l’appareil est l’appareil d’entreprise inscrit dans Intune. Si le numéro de série de l’appareil ne correspond pas, l’appareil sélectionné est incorrect. Revenez à l’écran précédent et sélectionnez un autre appareil.  

7.  Une fois le numéro de série vérifié, l’application Portail d’entreprise redirige l’utilisateur vers le site web Portail d’entreprise pour finaliser l’inscription, puis l’invite à retourner à l’application.  

8.  L’inscription est alors terminée. Vous pouvez désormais utiliser cet appareil avec toutes les fonctionnalités.  

##  <a name="BKMK_noUA"></a> Appareils gérés sans affinité utilisateur  
 Des appareils configurés avec **Pas d’affinité utilisateur** ne prennent pas en charge le Portail d’entreprise et ne doivent pas installer l’application. Le Portail d’entreprise est conçu pour les utilisateurs détenteurs d’informations d’identification d’entreprise, qui ont besoin d’accéder à des ressources d’entreprise personnalisées (par exemple, au courrier électronique). Les appareils inscrits avec **Pas d’affinité utilisateur** ne sont pas destinés à un utilisateur dédié. Une borne, un point de vente (PDV) ou un appareil de démonstration partagé sont des exemples caractéristiques d’utilisation d’appareils inscrits sans aucune affinité utilisateur. Si une affinité utilisateur est requise, vérifiez qu’une **affinité utilisateur** est sélectionnée pour le profil d’inscription de l’appareil avant d’inscrire celui-ci. Pour modifier l’état d’affinité sur un appareil, vous devez le mettre hors service, puis le réinscrire.
