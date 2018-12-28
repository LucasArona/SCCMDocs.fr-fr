---
title: Déployer l’application Lookout for Work
titleSuffix: Configuration Manager
description: Configurez et déployez les applications Lookout for Work.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 00fa7e538f6156f0dacee00feeb4b767a3c83a5c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417613"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurer et déployer les applications Lookout for Work

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article explique comment configurer et déployer l’application Lookout for Work pour les appareils Android et iOS.



## <a name="android-google-play-store-app"></a>Android (application Google Play Store)
1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

2.  Dans la page **Général** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :  
    - Type : sélectionnez **Package d’application pour Android sur Google Play**.
    - Emplacement : copiez le lien de l’application Lookout for Work à partir du Google Play Store et collez-le ici
    - Serveur de publication : Lookout Mobile Security
    - Nom : Lookout for Work
    - Description : Lookout offre la meilleure protection contre les menaces mobiles pour sécuriser votre appareil. Quand l’application Lookout est installée, elle protège votre appareil contre les menaces. En cas de détection de menaces, elle vous avertit, ainsi que votre administrateur informatique.
    - Catégorie administrative : Gestion de l’ordinateur  

    En cas de réussite de l’opération, l’application Lookout for Work s’affiche alors dans la liste des applications.  

3.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer** pour déployer l’application Lookout for Work sur les utilisateurs.   
    >[!IMPORTANT]  
    >Vous devez sélectionner les mêmes utilisateurs que ceux qui ont été ajoutés à l’option Gestion des inscriptions dans la console Lookout MTP.  

    Choisissez l’option **Installation requise**. Cette option exige que l’application Lookout soit installée sur l’appareil de l’utilisateur.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (version Enterprise signée de l’application Lookout)

1. Vérifiez que la gestion iOS est configurée sur vos appareils. Pour obtenir des instructions sur la configuration de votre appareil pour la gestion iOS, consultez [Configurer la gestion des appareils iOS et Mac](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).  

2. Resignez l’application iOS Lookout for Work. Lookout distribue son application iOS Lookout for Work en dehors de l’App Store iOS. Avant de distribuer l’application, vous devez la resigner avec votre certificat de développeur d’entreprise iOS. Pour obtenir des instructions détaillées pour resigner des applications iOS Lookout for Work, consultez [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) sur le site Lookout.  

3. Activez l’authentification Azure Active Directory (Azure AD) pour les utilisateurs iOS.
   1.  Connectez-vous au [panneau Azure AD du portail Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview), puis accédez à la page des inscriptions d’applications.  
   2.  Spécifiez le nom **Application iOS Lookout for Work**, puis sélectionnez **Native** comme type d’application.  
   ![capture d’écran de la boîte de dialogue Ajouter des applications présentant l’option d’application cliente native](media/aad-add-app-reg.png)

   3.  Pour cet URI de redirection, utilisez le format `lookoutwork://com.lookout.enterprise.<yourcompanyname>`, en remplaçant `<yourcompanyname>` par le nom de votre entreprise. Exemple : `lookoutwork://com.lookout.enterprise.contoso`
   4. Cliquez sur **Créer** pour créer l’application. 
   5.  Ouvrez la nouvelle application, cliquez sur **Paramètres**, puis ajoutez un URI de redirection supplémentaire. Utilisez le format `companyportal://code/<originalURI>`, où `<originalURI>` est une version encodée URL de votre URI de redirection d’origine. Par exemple, `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`
   6.  Dans les paramètres d’application, accédez à **Autorisations requises**, puis cliquez sur **Ajouter**. Sélectionnez les autorisations déléguées suivantes :  

       | API  | Autorisation  |
       |---------|---------|
       | Lookout MTP     | Accès à Lookout MTP         |
       | Microsoft Graph     | Se connecter et lire le profil utilisateur        |  

   Pour plus d’informations, consultez [Configurer une application cliente native](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).  


4. Dans Configuration Manager, chargez le fichier .ipa resigné. Définissez la version de système d’exploitation minimale sur iOS version 8.0 ou ultérieure. Pour plus d’informations, consultez [Créer des applications iOS](/sccm/apps/get-started/creating-ios-applications).   


5. Créez la stratégie de configuration des applications gérées. Pour plus d’informations, consultez [Configurer des applications iOS avec des stratégies de configuration des applications mobiles](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  


6. Déployez l’application Lookout for Work pour les utilisateurs. Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).  

   Sélectionnez les mêmes utilisateurs que ceux qui ont été ajoutés à l’option Gestion des inscriptions dans la console Lookout. Choisissez l’option **Installation requise**. Cette option exige que l’application Lookout soit installée sur l’appareil de l’utilisateur.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Que se passe-t-il quand l’application déployée est ouverte sur l’appareil ?

Quand l’utilisateur ouvre Lookout for Work sur l’appareil, ce dernier les invite à activer l’application. Il doit choisir de se connecter avec l’option Azure AD. Une procédure pas à pas détaillée pour l’utilisateur final est disponible dans les articles suivants :

- [Vous êtes invité à installer Lookout for Work sur votre appareil Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Vous devez résoudre une menace détectée par Lookout for Work sur votre appareil Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Étapes suivantes
- [Activer une règle de protection des appareils contre les menaces dans la stratégie de conformité](enable-device-threat-protection-rule-compliance-policy.md)
