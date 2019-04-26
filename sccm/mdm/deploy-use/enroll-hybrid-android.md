---
title: Configurer la gestion d’appareils hybrides Android avec Microsoft Intune
titleSuffix: Configuration Manager
description: Préparez la gestion des appareils mobiles Android avec Configuration Manager et Intune.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 00907d200bf54a4a1eb13863cf5bb529aa2f9656
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62282424"
---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion hybride des appareils mobiles Android avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article explique comment activer l’inscription hybride des appareils Android et Android for Work. Vous pouvez ensuite utiliser Configuration Manager pour gérer les appareils dans le cadre d’un abonnement Microsoft Intune configuré. À partir de Google Play, les utilisateurs peuvent télécharger l’application de portail d’entreprise Android qui leur permet d’inscrire des appareils Android (notamment Samsung KNOX Standard) et Android for Work.

Avec Configuration Manager, vous pouvez gérer les paramètres de conformité, réinitialiser ou supprimer des appareils Android, déployer des applications et collecter les informations relatives aux inventaires matériels et logiciels. Sans l’application de portail d’entreprise Android installée sur l’appareil, vous ne disposez pas des fonctions de gestion (telles que les paramètres de conformité et d’inventaire), mais vous pouvez quand même déployer des applications sur des appareils Android.  



## <a name="enable-android-enrollment"></a>Activer l’inscription Android  
Les étapes suivantes permettent à Configuration Manager de gérer des appareils Android sans profil professionnel (autrement dit, par une inscription « Android classique »).

1. Avant de pouvoir configurer l’inscription pour une plateforme, tenez compte des prérequis et effectuez les procédures décrites dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  
2. Dans la console Configuration Manager, dans l’espace de travail **Administration**, choisissez **Vue d’ensemble** > **Services cloud** > **Abonnements Microsoft Intune**, puis choisissez votre abonnement Intune.  
3. Sous l’onglet **Accueil**, dans le groupe **Abonnement** , choisissez **Configurer des plateformes** > **Android**.  
4. Dans la boîte de dialogue **Propriétés d’abonnement Microsoft Intune**, choisissez l’onglet **Android** et cochez la case **Activer l’inscription Android** . Vous pouvez choisir de **Bloquer les appareils personnels** pour limiter l’inscription aux [appareils prédéclarés](predeclare-devices-with-hardware-id.md).

   Une fois la configuration terminée, vous devez indiquer aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](/intune/end-user-educate). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.



## <a name="enable-android-for-work-enrollment"></a>Activer l’inscription Android for Work
Les étapes suivantes permettent à Configuration Manager de gérer des appareils Android avec un profil professionnel.

1. [Créez un compte Google](https://accounts.google.com/SignUp) que vous utiliserez comme compte d’administrateur Android for Work. Ou bien connectez-vous avec le compte associé à toutes les tâches de gestion Android for Work pour ce client Intune. Ce compte Google peut être partagé par les administrateurs qui gèrent des appareils Android. Il s’agit du compte Google utilisé par votre entreprise pour gérer et publier des applications dans la console Play for Work. Vous utilisez ce compte pour approuver les applications dans le magasin Play for Work. Veillez donc à prendre note du nom du compte et du mot de passe.
2. Activez l’inscription Android en liant le compte Google au client Intune géré dans Configuration Manager :
   1. Dans la console Configuration Manager, dans l’espace de travail **Administration**, choisissez **Vue d’ensemble** > **Services cloud** > **Abonnements Microsoft Intune**, puis choisissez votre abonnement Intune.
   2. Sous l’onglet **Accueil**, dans le groupe **Abonnement**, choisissez **Configurer des plateformes** > **Android for Work**.
   3. Dans la boîte de dialogue, choisissez **Configurer Android for Work dans la console Intune**. La console Intune s’ouvre dans votre navigateur web.
   4. Utilisez vos informations d’identification d’administrateur Intune pour vous connecter au portail Azure Intune.
   5. Cliquez sur **Google Play géré**. 
       1. Sélectionnez **J’accepte** pour autoriser Microsoft à [envoyer des informations sur l’utilisateur et sur l’appareil à Google](/intune/data-intune-sends-to-google).
       2. Pour ouvrir le site web Android for Work de Google Play, sélectionnez **Lancez Google pour vous connecter maintenant**. Le site web s’ouvre dans un nouvel onglet de votre navigateur.
       3. Dans la page de connexion de Google, entrez le compte Google de l’étape 1.
       4. Dans **Nom de l’organisation**, entrez le nom de votre entreprise. Pour **Enterprise Mobility Management (EMM) provider** (Fournisseur EMM), « Microsoft Intune » doit être affiché. 
       5. Acceptez le contrat Android for Work, puis choisissez **Confirmer**. Votre demande va être traitée.

   6. Dans la page de connexion de Google, entrez les informations d’identification du compte Google de l’étape 1, puis fournissez les informations relatives à votre société.
3. De retour dans Intune sur le portail Azure, accédez au panneau d’inscription **Android for Work**, puis cliquez sur **Profils professionnels**. Android for Work est maintenant activé. Deux options d’inscription sont disponibles pour les appareils Android for Work :
   - **Gérer tous les appareils comme Android** (désactivé). Tous les appareils Android, notamment ceux qui prennent en charge Android for Work, sont inscrits comme appareils Android conventionnels.
   - **Gérer les appareils pris en charge comme Android for Work** (activé). Tous les appareils qui prennent en charge Android for Work sont inscrits comme appareils Android for Work. Les appareils Android qui ne prennent pas en charge Android for Work sont inscrits comme des appareils Android conventionnels.

> [!NOTE]
> Un problème connu empêche le bon fonctionnement de l’option **Gérer les appareils pris en charge pour les utilisateurs uniquement dans ces groupes comme Android for Work**. Les appareils des utilisateurs dans les groupes Azure AD spécifiés sont inscrits en tant qu’appareils Android et non Android for Work. Pour activer Android for Work, vous devez utiliser l’option **Gérer les appareils pris en charge comme Android for Work**.


Une fois la configuration terminée, indiquez aux utilisateurs comment inscrire leurs appareils. Consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](/intune/end-user-educate). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

Lorsque la liaison est établie, vous voyez le nom du compte et le nom de l’organisation dans Intune, sur le portail Azure. À ce stade, vous pouvez fermer les deux navigateurs.

### <a name="enroll-an-android-for-work-device"></a>Inscrire un appareil Android for Work
L’inscription des appareils Android for Work par vos utilisateurs est similaire à celles des appareils Android. Les utilisateurs peuvent télécharger et installer l’application Portail d’entreprise pour Android sur leurs appareils mobiles. L’application les invite à créer un profil professionnel dans le cadre du processus d’inscription. Une fois le profil professionnel créé, les utilisateurs doivent basculer vers la version gérée du portail d’entreprise. Le portail d’entreprise géré est marqué d’un petit porte-documents orange dans le coin inférieur droit.

### <a name="manage-android-for-work-devices"></a>Gérer des appareils Android for Work
Après avoir activé l’inscription Android for Work, vous pouvez effectuer les tâches de gestion suivantes pour les appareils Android for Work :
- [Approuver les applications](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Créer des éléments de configuration](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gérer les paramètres de conformité](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gérer les profils de messagerie](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Réinitialiser de façon sélective le profil professionnel](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
> [< Étape précédente](create-service-connection-point.md) [Étape suivante >](set-up-additional-management.md)
