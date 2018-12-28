---
title: 'Inscrire des appareils iOS avec Apple Configurator '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de83706e92150a654967ec5cf38c5b18508d4e2b
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416909"
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Inscription d’appareils iOS à l’aide d’Apple Configurator pour les déploiements hybrides avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les entreprises qui achètent des appareils iOS pour leurs employés peuvent les gérer à l’aide de Microsoft Intune. Pour préparer des appareils iOS d’entreprise pour l’inscription, configurez un profil d’inscription dans la console Configuration Manager, puis exportez l’URL du profil pour qu’elle soit utilisée par Apple Configurator. Préparez ensuite l’appareil iOS pour l’inscription. Pour cela, connectez-le à un ordinateur Mac à l’aide d’un câble USB et utilisez Apple Configurator pour le configurer. Apple Configurator rétablit les paramètres d’usine de l’appareil et ajoute le profil d’inscription. L’utilisateur peut ainsi inscrire l’appareil quand il le met en marche pour la première fois dans le cadre de l’Assistant Configuration.

La procédure qui suit est recommandée pour les appareils iOS dédiés utilisés par un seul utilisateur pour accéder à la messagerie professionnelle et aux ressources de l’entreprise comme les applications.  

## <a name="prerequisites"></a>Prérequis  

-   Accès physique aux appareils iOS  

-   Numéros de série des appareils : [Localisation du numéro de série de votre produit Apple](https://support.apple.com/en-us/HT204308)  

-   Ordinateur Mac avec [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

-   Câbles USB pour connecter des appareils à votre ordinateur Mac  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>Ajouter un profil d’inscription des appareils d’entreprise

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Tous les appareils d’entreprise** > **iOS** > **Profils d’inscription**. Cliquez sur **Créer un profil** pour ouvrir l’Assistant Création d’un profil. Configurez les paramètres des pages suivantes :  

2.  Sur la page **Général** , spécifiez informations suivantes :  

    -   **Nom** (non visible pour les utilisateurs)  

    -   **Description** (non visible pour les utilisateurs)  

    -   **Affinité utilisateur** : spécifie la façon dont les appareils sont inscrits. Pour la plupart des scénarios de l’Assistant Configuration, utilisez **Demander une affinité utilisateur**.  

        -   **Demander l’affinité utilisateur**: L’appareil doit être affilié à un utilisateur pendant l’installation initiale et peut ensuite être autorisé à accéder aux e-mails tant que cet utilisateur et les données d’entreprise.  

        -   **Aucune affinité utilisateur**: L’appareil n’est pas affilié à un utilisateur. Utilisez cette affiliation pour les appareils qui effectuent des tâches sans accéder aux données de l'utilisateur local. Les applications nécessitant une affiliation de l'utilisateur ne fonctionneront pas.

    Cliquez sur **Suivant** pour continuer.  

3.  Dans la page **Programme d’inscription d’appareils**, laissez la case **Configurer les paramètres DEP pour ce profil** cochée, puis cliquez sur **Suivant**.  

4.  Passez en revue le résumé, puis cliquez sur **Suivant** pour créer le profil d’inscription. Cliquez sur **Fermer** pour terminer l’Assistant. Vous êtes maintenant prêt à ajouter des numéros IMEI ou de série pour les appareils à inscrire.  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>Prédéclarer des appareils à inscrire avec l’Assistant Configuration

Dans cette étape, vous prédéclarez des appareils comme appartenant à l’entreprise. Pour cela, vous fournissez une liste d’identificateurs de matériel (numéros IMEI ou de série).

Pour plus d’informations, consultez [Prédéclarer des appareils avec des numéros IMEI ou des numéros de série iOS](predeclare-devices-with-hardware-id.md). Une fois cette tâche terminée, revenez à cette page pour passer à l’étape suivante.

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>Exporter le profil à déployer sur les appareils iOS

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Tous les appareils d’entreprise** > **iOS** > **Profils d’inscription**.

2.  Sélectionnez le profil d’inscription à déployer sur les appareils mobiles, puis cliquez sur **Exporter**.

3.  Copiez et enregistrez l’**URL du profil** dans un fichier que vous pouvez modifier.   

4.  Pour prendre en charge Apple Configurator 2, l’URL du profil 2.0 doit être modifiée. Remplacez la partie suivante de l’URL :  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     par  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Enregistrez l’URL du profil modifié. Vous allez l’utiliser pour ajouter l’URL du profil d’inscription dans Apple Configurator dans la [section suivante](#step-4-prepare-the-device-with-apple-configurator).  

> [!NOTE]
> L’URL du profil d’inscription est valide pendant deux semaines après son exportation. Après deux semaines, vous devez exporter une nouvelle URL pour inscrire des appareils iOS.

## <a name="prepare-the-device-with-apple-configurator"></a>Préparer l’appareil avec Apple Configurator

Pour préparer des appareils iOS pour l’inscription, connectez chaque appareil à un ordinateur Mac et chargez le profil d’inscription sur cet appareil.  

> [!WARNING]  
>  Apple Configurator réinitialise les appareils et rétablit les configurations d’usine.  

1. Sur un ordinateur Mac, ouvrez **Apple Configurator 2**.  

2. Dans la barre de menus, cliquez sur **Apple Configurator 2** > **Préférences**.  

3. Dans le volet Préférences, sélectionnez **Serveurs**, puis cliquez sur le symbole « + » situé sous le volet gauche pour lancer l’Assistant Serveur MDM. Cliquez sur **Suivant**.  

4. Entrez le **nom** et l’**URL d’inscription** enregistrés [précédemment](#step-3-export-the-profile-to-deploy-to-ios-devices). Cliquez sur **Suivant**.  

   > [!NOTE]
   > Si vous recevez un avertissement à propos des exigences de profil de confiance pour Apple TV, vous pouvez annuler en toute sécurité l’option **Profil de confiance** en cliquant sur le « X » gris. Vous pouvez également ignorer tout avertissement relatif au certificat d’ancrage (ou certificat racine).

   Pour continuer, cliquez sur **Suivant** jusqu’à la fin de l’exécution de l’Assistant.  

5. Dans le volet **Serveurs**, cliquez sur « Modifier » en regard du profil du nouveau serveur. Vérifiez que l’URL d’inscription correspond exactement à l’URL entrée précédemment. Retapez l’URL si elle est différente, puis cliquez sur **Enregistrer**.  

6. Connectez un appareil iOS à l’ordinateur Mac à l’aide d’un câble USB.  

   > [!WARNING]  
   >  Ce processus rétablit les configurations d’usine des appareils. Avant de connecter l’appareil, réinitialisez-le et mettez-le en marche. Nous vous recommandons d’attendre que l’appareil affiche l’écran Hello avant de continuer.  

7. Cliquez sur **Préparer**. Dans le volet **Prepare iOS Device** (Préparer l’appareil iOS), sélectionnez **Manual** (Manuel), puis cliquez sur **Suivant**.  

8. Dans le volet **Enroll in MDM Server** (Inscription dans un serveur MDM), sélectionnez le nom du serveur que vous avez créé, puis cliquez sur **Suivant**.  

9. Dans le volet **Create an Organization** (Créer une organisation), choisissez ou créez une **organisation**, puis cliquez sur **Suivant**.  

10. Dans le volet **Configure iOS Setup Assistant** (Configurer l’Assistant Installation iOS), choisissez les étapes présentées à l’utilisateur, puis cliquez sur **Prepare** (Préparer). Si vous y êtes invité, authentifiez-vous pour mettre à jour les paramètres d’approbation.  

11. Quand vous avez terminé, vous pouvez déconnecter le câble USB.  

Répétez ces étapes pour tous les appareils à préparer pour l’inscription.

## <a name="distribute-devices"></a>Distribuer les appareils

Les appareils sont désormais prêts pour l’inscription d’entreprise. Éteignez les appareils et distribuez-les aux utilisateurs. Quand vous mettez en marche l’appareil, l’Assistant Configuration démarre et invite l’utilisateur à entrer son compte professionnel ou scolaire pour commencer l’inscription.
