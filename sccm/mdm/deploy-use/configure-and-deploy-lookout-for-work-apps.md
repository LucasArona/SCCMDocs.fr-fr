---
title: Déployer l’application Lookout for Work
titleSuffix: Configuration Manager
description: Configurez et déployez les applications Lookout for Work.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a812ed059bc0d96c23af986c2051416c26f6a15a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
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
    - Nom : Lookout for Work
    - Description : Lookout offre la meilleure protection contre les menaces mobiles pour assurer la sécurité de votre appareil. Quand l’application Lookout est installée, elle protège votre appareil contre les menaces. En cas de détection de menaces, elle vous avertit, ainsi que votre administrateur informatique.
    - Catégorie administrative : gestion de l’ordinateur  

    En cas de réussite de l’opération, l’application Lookout for Work s’affiche alors dans la liste des applications.

3.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer** pour déployer l’application Lookout for Work sur les utilisateurs.   
    >[!IMPORTANT]  
    >Vous devez sélectionner les mêmes utilisateurs que ceux qui ont été ajoutés à l’option Gestion des inscriptions dans la console Lookout MTP.  

    Choisissez l’option **Installation requise**. Cette option exige que l’application Lookout soit installée sur l’appareil de l’utilisateur.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (version Enterprise signée de l’application Lookout)

- **Étape 1 :** Vérifiez que la **gestion iOS** est configurée sur votre appareil. Pour obtenir des instructions sur la configuration de votre appareil pour la gestion iOS, consultez [Configurer la gestion des appareils iOS et Mac](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).

- **Étape 2 :** **Resignez** l’application iOS Lookout for Work. Lookout distribue son application iOS Lookout for Work en dehors de l’App Store iOS. **Avant de distribuer l’application**, vous devez resigner l’application avec votre certificat de développeur d’entreprise iOS. Pour obtenir des instructions détaillées pour resigner des applications iOS Lookout for Work, consultez [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) sur le site Lookout.


- **Étape 3 :** Activez l’authentification Azure Active Directory pour les utilisateurs iOS en effectuant les étapes suivantes :
  1.  Connectez-vous au [portail de gestion Azure Active Directory](https:/portal.azure.com), puis accédez à la page d’application.
  2.  Ajoutez l’**application iOS Lookout for Work** comme **application cliente native**.
  ![capture d’écran de la boîte de dialogue Ajouter des applications présentant l’option d’application cliente native](media/aad-add-app.png)

  3. Remplacez **com.lookout.enterprise.nom_de_votre_entreprise** par l’ID d’ensemble client que vous avez sélectionné quand vous avez signé le package IPA.
  4.  Ajoutez l’URI de redirection supplémentaire **&lt;companyportal://code/>** suivi d’une version codée URL de votre URI de redirection d’origine.
  5.  Ajoutez **Autorisations déléguées** à votre application.

  Pour plus d’informations, consultez [Configurer une application cliente native](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).


- **Étape 4 :** Chargez le fichier .ipa resigné comme décrit dans la rubrique [Créer des applications iOS avec System Center Configuration Manager](/sccm/apps/get-started/creating-ios-applications). Définissez la version de système d’exploitation minimale sur iOS version 8.0 ou ultérieure.


- **Étape 5 :** Créez la stratégie de configuration d’application gérée comme décrit dans la rubrique [Configurer des applications iOS à l’aide de stratégies de configuration des applications dans System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).


- **Étape 6 :** **Pour déployer l’application sur les utilisateurs**, sélectionnez l’application Lookout for Work dans la page **Applications**, sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer**.

  Sélectionnez les mêmes utilisateurs que ceux qui ont été ajoutés à l’option Gestion des inscriptions dans la console Lookout. Choisissez l’option **Installation requise**. Cette option exige que l’application Lookout soit installée sur l’appareil de l’utilisateur.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Que se passe-t-il quand l’application déployée est ouverte sur l’appareil ?

Quand l’utilisateur ouvre Lookout for Work sur l’appareil, ce dernier les invite à activer l’application. Ils doivent choisir de se connecter avec l’option Azure Active Directory. Une procédure pas à pas détaillée pour l’utilisateur final est disponible dans les articles suivants :

- [Vous êtes invité à installer Lookout for Work sur votre appareil Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [Vous devez résoudre une menace détectée par Lookout for Work sur votre appareil Android](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Étapes suivantes
- [Activer une règle de protection des appareils contre les menaces dans la stratégie de conformité](enable-device-threat-protection-rule-compliance-policy.md)
