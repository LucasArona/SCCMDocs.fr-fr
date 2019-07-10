---
title: Configurer votre abonnement Lookout
titleSuffix: Configuration Manager
description: Découvrez comment configurer Lookout Mobile Threat Defense.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0946c455732bc13520d3363187b22b118d6e403
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678886"
---
# <a name="set-up-your-subscription-for-lookout-mobile-threat-defense"></a>Configurer votre abonnement à Lookout Mobile Threat Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Les étapes suivantes sont nécessaires pour configurer l’abonnement à Lookout Mobile Threat Defense :

| #        |Étape  |
| ------------- |-------------|
| 1 | [Collecter les informations Azure AD](#collect-azure-ad-information) |
| 2 | [Configurer votre abonnement](#configure-your-subscription) |
| 3 | [Configurer les groupes d’inscription](#configure-enrollment-groups) |
| 4 | [Configurer la synchronisation des états](#configure-state-sync) |
| 5 | [Configurer le destinataire des rapports d’erreurs envoyés par e-mail](#configure-error-report-email-recipient-information) |
| 6 | [Configurer les paramètres d’inscription](#configure-enrollment-settings) |
| 7 | [Configurer les notifications par e-mail](#configure-email-notifications) |
| 8 | [Configurer la classification des menaces](#configure-threat-classification) |
| 9 | [Surveillance de l’inscription](#watching-enrollment) |


> [!IMPORTANT]  
> Un locataire Lookout Mobile Endpoint Security existant qui n’est pas déjà associé à votre locataire Azure AD ne peut pas être utilisé pour l’intégration à Azure AD et Intune. Contactez le support technique Lookout pour créer un locataire Lookout Mobile Endpoint Security. Utilisez le nouveau locataire pour intégrer vos utilisateurs Azure AD.




## <a name="collect-azure-ad-information"></a>Collecter les informations Azure AD
Votre locataire Lookout Mobility Endpoint Security sera associé à votre abonnement Azure AD pour intégrer Lookout à Intune. Pour activer votre abonnement au service Lookout Mobile Threat Defense, vous devez fournir les informations suivantes à l’équipe du support Lookout (enterprisesupport@lookout.com) :

- **ID de locataire Azure AD**
- **ID d’objet de groupe Azure AD** pour l’accès *complet* à la console Lookout
- **ID d’objet de groupe Azure AD** pour l’accès *restreint* à la console Lookout (facultatif)

Procédez aux étapes suivantes pour collecter les informations demandées par l’équipe du support Lookout.

1. Connectez-vous au [portail Azure](https://portal.azure.com), puis sélectionnez votre abonnement. 

2. Lorsque vous choisissez le nom de votre abonnement, l’URL obtenue comprend l’ID de l’abonnement. Si vous ne trouvez pas votre ID d’abonnement, consultez cet [article du support technique Microsoft](https://support.office.com/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) qui fournit des conseils à cette fin.

3. Recherchez l’ID du groupe Azure AD.  
     > [!NOTE]   
     > **L’ID d’objet de groupe** est indiqué dans la page **Propriétés** du groupe, situé dans le panneau Azure AD du portail Azure.  

   La console Lookout offre deux niveaux d’accès :  

   - **Accès complet :** L’administrateur Azure AD peut créer un groupe pour les utilisateurs qui ont un accès complet et éventuellement créer un groupe pour les utilisateurs qui ont un accès restreint. Seuls les utilisateurs qui sont membres de ces groupes peuvent se connecter à la **console Lookout**.
   - **Accès limité :** Les utilisateurs de ce groupe n’ont pas accès à plusieurs configuration et les inscriptions de modules de la console Lookout, et ont un accès en lecture seule à la **stratégie de sécurité** module de la console Lookout.  

     > [!TIP]  
     > Pour plus d’informations sur les autorisations, consultez [cet article du support Lookout](https://personal.support.lookout.com/hc/articles/114094105653).


4. Une fois que vous avez collecté ces informations, contactez le support technique Lookout (adresse e-mail : enterprisesupport@lookout.com). Le support technique Lookout travaillera avec votre contact principal pour intégrer votre abonnement et créer votre compte d’entreprise Lookout sur la base des informations que vous avez collectées.



## <a name="configure-your-subscription"></a>Configurer votre abonnement

1. Une fois que l’équipe du support Lookout a créé votre compte d’entreprise Lookout, un e-mail comprenant un lien vers [l’url de connexion](https://aad.lookout.com/les?action=consent) est envoyé par Lookout au contact principal de votre entreprise.

2. La première connexion à la console Lookout doit être effectuée à l’aide d’un compte d’utilisateur disposant du rôle d’administrateur général Azure AD, afin d’inscrire votre locataire Azure AD. Les connexions suivantes ne nécessiteront pas ce niveau de privilège Azure AD. Une page de consentement s’affiche. Choisissez **Accepter** pour terminer l’inscription. Une fois que vous avez donné votre consentement, vous êtes redirigé vers la console Lookout.

   ![Capture d’écran de la page de première connexion de la console Lookout](media/lookout-initial-login.png)

3. Dans la [console Lookout](https://aad.lookout.com), à partir du module **Système**, choisissez l’onglet **Connecteurs**, puis sélectionnez **Intune**.

   ![capture d’écran de la console Lookout avec l’onglet Connecteurs ouvert et l’option Intune mise en surbrillance](media/lookout-setup-intune-connector.png)

4. Accédez à **Connecteurs** > **Paramètres de connexion**, puis spécifiez la **fréquence des pulsations** en minutes.

   ![capture d’écran de l’onglet Paramètres de connexion indiquant la fréquence de pulsations configurée](media/lookout-connection-settings.png)



## <a name="configure-enrollment-groups"></a>Configurer les groupes d’inscription
1. Une bonne pratique consiste à créer un groupe de sécurité Azure AD dans le [portail Azure](https://portal.azure.com) avec un petit nombre d’utilisateurs, afin de tester l’intégration Lookout.

    > [!NOTE]  
    > Tous les appareils pris en charge par Lookout et inscrits auprès d’Intune qui sont associés à des utilisateurs identifiés faisant partie d’un groupe d’inscription dans Azure AD, sont inscrits et peuvent être activés dans la console Lookout MTD.

2. Dans la [console Lookout](https://aad.lookout.com), à partir du module **Système**, choisissez l’onglet **Connecteurs**, puis sélectionnez **Enrollment Management** (Gestion de l’inscription) pour définir un ensemble d’utilisateurs dont les appareils doivent être inscrits auprès de Lookout. Ajoutez le **nom complet** du groupe de sécurité Azure AD pour l’inscription.

    ![capture d’écran de la page d’inscription du connecteur Intune](media/lookout-enrollment.png)

    >[!IMPORTANT]  
    > Le **nom complet** respecte la casse, comme le montre la page **Propriétés** du groupe de sécurité dans le portail Azure. Comme le montre l’image ci-dessous, le **nom complet** du groupe de sécurité a une casse mixte, et le titre est entièrement en minuscules. Dans la console Lookout, respectez la casse du **nom complet** du groupe de sécurité.
    >![capture d’écran du portail Azure, service Azure Active Directory, page Propriétés](media/aad-group-display-name.png)

    >[!NOTE]  
    >Pour la recherche des nouveaux appareils, une bonne pratique consiste à utiliser la valeur par défaut (5 minutes) comme incrément d’intervalle. Limitations actuelles, **Lookout ne peut pas valider les noms d’affichage de groupe :** Vérifiez le **SURNOM** champ dans le portail Azure correspond exactement au groupe de sécurité de Azure AD. **Création de groupes imbriqués n’est pas pris en charge :**  Sécurité Azure AD groupes utilisés dans Lookout doivent contenir uniquement des utilisateurs. Ils ne peuvent pas contenir d’autres groupes.

3.  Une fois le groupe ajouté, la prochaine fois que l’utilisateur ouvrira l’application Lookout for Work sur un appareil pris en charge, ce dernier sera activé dans Lookout.

4.  Quand vous êtes satisfait des résultats, étendez l’inscription aux autres groupes d’utilisateurs.



## <a name="configure-state-sync"></a>Configurer la synchronisation des états
Dans l’option **Synchronisation des états**, spécifiez le type de données à envoyer à Intune. L’état de l’appareil et l’état de la menace sont nécessaires pour que l’intégration Lookout Intune fonctionne correctement. Ces paramètres sont activés par défaut.



## <a name="configure-error-report-email-recipient-information"></a>Configurer le destinataire des rapports d’erreurs envoyés par e-mail
Dans l’option **Gestion des erreurs**, entrez l’adresse e-mail à laquelle doivent être envoyés les rapports d’erreurs.

![capture d’écran de la page Gestion des erreurs du connecteur Intune](media/lookout-connector-error-notifications.png)



## <a name="configure-enrollment-settings"></a>Configurer les paramètres d’inscription
Dans le module **Système**, dans la page **Connecteurs**, spécifiez le nombre de jours au terme desquels un appareil est considéré comme déconnecté. Les appareils déconnectés sont considérés comme non conformes et ne peuvent pas accéder à vos applications d’entreprise, selon les stratégies d’accès conditionnel SCCM. Vous pouvez spécifier des valeurs comprises entre 1 et 90 jours.

![Paramètres d’inscription Lookout](media/lookout-console-enrollment-settings.png)



## <a name="configure-email-notifications"></a>Configurer les notifications par e-mail
Si vous souhaitez recevoir des alertes sur les menaces par e-mail, connectez-vous à la [console Lookout](https://aad.lookout.com) avec le compte d’utilisateur qui doit recevoir les notifications. Sous l’onglet **Préférences** du module **Système**, choisissez les niveaux de menace qui doivent recevoir des notifications, puis définissez-les sur **Activé**. Enregistrez vos modifications.

![Capture d’écran de la page Préférences avec le compte d’utilisateur affiché](media/lookout-email-notifications.png) Si vous ne souhaitez plus recevoir de notifications par e-mail, définissez les notifications sur Désactivé, puis enregistrez vos modifications.



## <a name="configure-threat-classification"></a>Configurer la classification des menaces
Le service Lookout Mobile Threat Defense classe les différents types de menaces mobiles. Les [classifications des menaces dans Lookout](http://personal.support.lookout.com/hc/articles/114094130693) ont des niveaux de risque par défaut qui leur sont associés. Ces paramètres peuvent être modifiés à tout moment en fonction des besoins de votre entreprise.

![capture d’écran de la page de stratégie montrant des menaces et des classifications](media/lookout-threat-classification.png)

>[!IMPORTANT]  
> Les niveaux de risque sont un aspect important de la protection contre les menaces mobiles. L’intégration Intune évalue la conformité des appareils en fonction de ces niveaux de risque au moment de l’exécution. L’administrateur Intune définit une règle de stratégie qui identifie un appareil comme non conforme si celui-ci présente une menace active du niveau minimum configuré (**Haut**, **Moyen** ou **Faible**). La stratégie de classification des menaces dans le service Lookout Mobile Threat Defense a donc un impact direct sur l’évaluation de la conformité des appareils dans Intune.



## <a name="watching-enrollment"></a>Surveillance de l’inscription
Une fois la configuration terminée, le service Lookout Mobile Threat Defense commence à interroger Azure AD pour rechercher les appareils qui correspondent aux groupes d’inscription spécifiés. Les informations sur les appareils inscrits se trouvent dans le module Appareils. Les appareils s’affichent dans l’état initial En attente. L’état de l’appareil change une fois que l’application Lookout for Work est installée, ouverte et activée sur l’appareil. Pour plus d’informations sur l’envoi (push) de l’application Lookout for Work vers l’appareil, consultez [Configurer et déployer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).


## <a name="next-steps"></a>Étapes suivantes
[Activer la connexion à Lookout MTP dans Intune](enable-lookout-connection-in-intune.md)
