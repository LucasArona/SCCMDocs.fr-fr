---
title: "Inscrire des appareils avec le gestionnaire d'inscription d'appareil "
titleSuffix: Configuration Manager
description: Inscrivez les appareils d’entreprise avec le compte du gestionnaire d’inscription d’appareil à l’aide de System Center Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2905f26e-7859-497d-b995-5ff48261efa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a691bc98a26cdf56d22c03840997d9e0a380b7b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="enroll-devices-with-device-enrollment-manager-with-configuration-manager"></a>Inscrire des appareils avec un gestionnaire d’inscription d’appareil à l’aide de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les organisations peuvent utiliser Intune pour gérer un grand nombre d'appareils mobiles avec un seul compte d'utilisateur. Le compte *Gestionnaire d’inscription des appareils* (DEM) est un compte d’utilisateur spécial servant à inscrire des appareils. Vous ajoutez des utilisateurs existants au compte DEM afin de leur accorder des fonctionnalités DEM spéciales. Chaque appareil inscrit utilise une licence unique. Nous vous recommandons d’utiliser les appareils inscrits via ce compte en tant qu’appareils partagés sans affinité utilisateur plutôt qu’en tant qu’appareils personnels et dédiés.  

## <a name="enroll-corporate-owned-devices-with-the-device-enrollment-manager"></a>Inscrire des appareils d’entreprise avec le gestionnaire d’inscription d’appareil  
 Vous pouvez affecter à un directeur ou responsable de magasin, par exemple, un compte de gestionnaire d'inscription d'appareil pour lui permettre d'effectuer les opérations suivantes :  

-   Inscrire jusqu’à 1 000 appareils pour la gestion  
-   Utiliser l’application Portail d’entreprise pour installer des applications d’entreprise  
-   Configurer l'accès aux données de l'entreprise  

Les limitations suivantes s’appliquent aux appareils gérés en utilisant un compte de gestionnaire d’inscription d’appareil :

- Le directeur du magasin ne peut pas réinitialiser l'appareil à partir du portail d'entreprise.  
- Les appareils ne peuvent pas être joints à un espace de travail ou à Azure Active Directory. Cela empêche les appareils d’utiliser l’accès conditionnel.
-  Pour déployer des applications d’entreprise sur des appareils gérés avec le gestionnaire d’inscription d’appareil, déployez l’application Portail d’entreprise en tant qu’**Installation requise** sur le compte d’utilisateur du gestionnaire d’inscription d’appareil. Le gestionnaire d’inscription d’appareil peut alors lancer l’application Portail d’entreprise pour installer des applications supplémentaires.
- Pour améliorer les performances, l’application Portail d’entreprise affiche uniquement l’appareil local. La gestion à distance des autres appareils DEM ne peut être assurée qu’à partir de la console Configuration Manager et par l’administrateur.
- Le site web Portail d’entreprise n’est pas accessible aux comptes de gestionnaire d’inscription d’appareil. Utilisez l’application Portail d’entreprise.
- Si vous utilisez le gestionnaire d’inscription d’appareil pour inscrire des appareils iOS, vous ne pouvez pas utiliser Apple Configurator ou le Programme d’inscription des appareils Apple (DEP) pour inscrire des appareils. (iOS uniquement) 

 **Exemples de scénarios faisant intervenir un gestionnaire d’inscription d’appareil :**   
Un restaurant souhaite que son personnel de service utilise des tablettes et commande des écrans pour le personnel de cuisine. Les employés ne doivent jamais accéder aux données de l’entreprise ni ouvrir de session en tant qu’utilisateur. L'administrateur Intune crée un compte de gestionnaire d'inscription d'appareil et inscrit les appareils d'entreprise à l'aide de ce compte. L'administrateur pourrait également donner les informations d'identification du gestionnaire d'inscription d'appareil au directeur du restaurant, puis lui permettre d'inscrire et de gérer les appareils.  

 L'administrateur ou le directeur peuvent déployer des applications propres aux rôles sur les appareils du restaurant. Un administrateur peut également sélectionner un appareil dans la console et le supprimer de la Gestion des appareils mobiles.  

#### <a name="add-a-device-enrollment-manager"></a>Ajouter un gestionnaire d’inscription d’appareil  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Services cloud**, puis cliquez sur **Abonnements Microsoft Intune**. Sélectionnez l’abonnement Microsoft Intune auquel vous allez ajouter un gestionnaire d’inscription d’appareil, puis cliquez sur **Propriétés**.  

3.  Dans la boîte de dialogue Propriétés de l’abonnement Microsoft Intune, cliquez sur l’onglet **Gestionnaire d’inscription d’appareil**.  

4.  Cliquez sur **Ajouter/Supprimer**.  

5.  Dans la boîte de dialogue **Gestionnaire d’inscription d’appareil**, tapez le nom de l’utilisateur que vous souhaitez ajouter comme gestionnaire d’inscription d’appareil, puis cliquez sur **Rechercher**. Sélectionnez l’utilisateur que vous souhaitez ajouter comme gestionnaire d’inscription d’appareil, puis cliquez sur **Ajouter**.  

6.  Confirmez le compte d’utilisateur appelé à devenir gestionnaire d’inscription d’appareil et cliquez sur **Ajouter/Supprimer**.  Une licence d’abonnement est nécessaire pour chaque utilisateur qui accède au service. De plus, le *gestionnaire d’inscription d’appareil* ne peut pas être administrateur Intune. Déterminez si vous devez ajouter des licences supplémentaires avant d'utiliser cette fonctionnalité.  

7.  Le gestionnaire d’inscription d’appareil peut maintenant inscrire des appareils mobiles en appliquant la même procédure qu’un utilisateur final pour un scénario BYOD dans le portail d’entreprise.  

#### <a name="delete-a-device-enrollment-manager-from-intune"></a>Supprimer un gestionnaire d'inscription d'appareil d'Intune  
La suppression d'un gestionnaire d'inscription d'appareil n'affecte pas les appareils inscrits. Quand un gestionnaire d'inscription d'appareil est supprimé :  
- aucun appareil inscrit n’est désinscrit ;  
- les appareils inscrits continuent à être entièrement gérés ;  
- les informations d’identification de compte du gestionnaire d’inscription d’appareil supprimé restent valides et vous permettent de vous connecter au portail d’entreprise pour accéder aux applications ;  
- la suppression du gestionnaire d'inscription d'appareil n'entraîne pas la réinitialisation ou la mise hors service des appareils ;  
- il existe toujours une relation entre le compte du gestionnaire d'inscription d'appareil supprimé et les appareils inscrits, mais aucun appareil supplémentaire ne peut être inscrit.

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  
2.  Dans l'espace de travail **Administration** , développez **Services cloud**, puis cliquez sur **Abonnements Microsoft Intune**. Sélectionnez l’abonnement Microsoft Intune auquel vous allez ajouter un gestionnaire d’inscription d’appareil, puis cliquez sur **Propriétés**.  
3.  Dans la boîte de dialogue Propriétés de l’abonnement Microsoft Intune, cliquez sur l’onglet **Gestionnaire d’inscription d’appareil**.  
4.  **Recherchez** le gestionnaire d’inscription d’appareil à supprimer et cliquez sur **Supprimer**, puis sur **OK**.  
