---
title: Configurer votre abonnement avec Lookout
titleSuffix: Configuration Manager
description: Cette rubrique fournit des détails sur la configuration du service Lookout de protection des appareils contre les menaces.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08bf88c0f6660c213c47a5ed283b3be0431056a2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Configurer votre abonnement pour le service Lookout de protection des appareils contre les menaces

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour pouvoir préparer votre abonnement au service Lookout de protection des appareils contre les menaces, le support technique Lookout (enterprisesupport@lookout.com) a besoin des informations suivantes sur votre abonnement Azure Active Directory (Azure AD). Votre locataire Lookout Mobility Endpoint Security sera associé à votre abonnement Azure AD pour intégrer Lookout à Intune. 

* **ID de locataire Azure AD**
* **ID d’objet de groupe Azure AD** pour l’accès **complet** à la console Lookout
* **ID d’objet de groupe Azure AD** pour l’accès **restreint** à la console Lookout (facultatif)

> [!IMPORTANT]
> Un locataire Lookout Mobile Endpoint Security existant qui n’est pas déjà associé à votre locataire Azure AD ne peut pas être utilisé pour l’intégration à Azure AD et Intune. Contactez le support technique Lookout pour créer un locataire Lookout Mobile Endpoint Security. Utilisez le nouveau locataire pour intégrer vos utilisateurs Azure AD.

Consultez la section suivante pour collecter les informations demandées par l’équipe du support technique Lookout.  

## <a name="get-your-azure-ad-information"></a>Obtenir vos informations Azure AD
### <a name="azure-ad-tenant-id"></a>ID de locataire Azure AD
Connectez-vous au [portail de gestion Azure AD](https://manage.windowsazure.com) et sélectionnez votre abonnement. 

![capture d’écran de la page Azure AD indiquant le nom du locataire](media/aad_tenant_name.png) Quand vous choisissez le nom de votre abonnement, l’URL résultante inclut l’ID de l’abonnement.  Si vous ne trouvez pas votre ID d’abonnement, consultez cet [article du support technique Microsoft](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US) qui fournit des conseils à cette fin.   
### <a name="azure-ad-group-id"></a>ID de groupe Azure AD
La console Lookout offre deux niveaux d’accès :  
* **Accès complet :** l’administrateur Azure AD peut créer un groupe rassemblant les utilisateurs qui bénéficieront d’un accès complet et, éventuellement, créer un autre groupe pour les utilisateurs qui auront un accès restreint.  Seuls les utilisateurs qui sont membres de ces groupes seront autorisés à se connecter à la **console Lookout**.
* **Accès restreint :** les utilisateurs de ce groupe n’auront pas accès à plusieurs modules d’inscription et de configuration dans la console Lookout, et pourront accéder en lecture seule au module **Stratégie de sécurité** dans la console Lookout.  

Pour plus d’informations sur les autorisations, consultez [cet article](https://personal.support.lookout.com/hc/en-us/articles/114094105653) sur le site web de Lookout.

L’**ID d’objet de groupe** est indiqué dans la page **Propriétés** du groupe dans la **console de gestion Azure AD**.

![capture d’écran de la page Propriétés avec le champ GroupID mis en surbrillance](media/aad_group_object_id.png)

Une fois que vous avez collecté ces informations, contactez le support technique Lookout (adresse e-mail : enterprisesupport@lookout.com).

Le support technique Lookout travaillera avec votre contact principal pour intégrer votre abonnement et créer votre compte d’entreprise Lookout sur la base des informations que vous avez collectées.


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Configurer votre abonnement avec le service Lookout de protection des appareils contre les menaces
### <a name="step-1-set-up-your-device-threat-protection"></a>Étape 1 : Configurer la protection des appareils contre les menaces
Une fois que le support technique Lookout a créé votre compte d’entreprise Lookout, vous pouvez vous connecter à la console Lookout.   Lookout envoie un e-mail au contact principal de votre entreprise, avec un lien vers l’URL de connexion https://aad.lookout.com/les?action=consent

Quand vous vous connectez à la console Lookout pour la première fois, vous devez utiliser un compte d’utilisateur ayant le rôle Azure AD Administrateur général, car Lookout a besoin de ces informations pour inscrire votre locataire Azure AD.   Pour les connexions suivantes, il n’est pas nécessaire d’avoir ce niveau de privilège Azure AD.  À la première connexion, une page de consentement s’affiche. Choisissez **Accepter** pour terminer l’inscription.

![capture d’écran de la page de première connexion de la console Lookout](media/lookout-initial-login.png)

Une fois que vous avez donné votre consentement, vous êtes redirigé vers la console Lookout. Après l’inscription initiale, vous pouvez vous connecter directement en utilisant l’URL https://aad.lookout.com

Consultez l’[article sur le dépannage]() si vous rencontrez des problèmes de connexion.

Les étapes suivantes décrivent les tâches que vous devez effectuer pour terminer la configuration de Lookout dans la [console Lookout](https://aad.lookout.com).

### <a name="step-2-configure-the-intune-connector"></a>Étape 2 : Configurer le connecteur Intune

1.  Dans la console Lookout, à partir du module **Système**, choisissez l’onglet **Connecteurs**, puis sélectionnez **Intune**.

  ![capture d’écran de la console Lookout avec l’onglet Connecteurs ouvert et l’option Intune mise en surbrillance](media/lookout-setup-intune-connector.png)

2.  Dans l’option Paramètres de connexion, définissez la fréquence de pulsations (en minutes).  Votre connecteur Intune est maintenant prêt.  

  ![capture d’écran de l’onglet Paramètres de connexion indiquant la fréquence de pulsations configurée](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>Étape 3 : Configurer les groupes d’inscription
Dans l’option **Gestion des inscriptions**, définissez un ensemble d’utilisateurs dont les appareils doivent être inscrits dans Lookout. La bonne pratique consiste à commencer avec un petit groupe d’utilisateurs pour faire des tests et vous familiariser avec le fonctionnement de l’intégration.  Quand vous êtes satisfait de vos résultats de test, vous pouvez étendre l’inscription à d’autres groupes d’utilisateurs.

Pour commencer à utiliser les groupes d’inscription, définissez d’abord un groupe de sécurité Azure AD pour un ensemble initial d’utilisateurs que vous souhaitez inscrire dans le service Lookout de protection des appareils contre les menaces. Après avoir créé le groupe dans Azure AD, dans la console Lookout, accédez à l’option **Gestion des inscriptions** et ajoutez le **nom complet** du groupe de sécurité Azure AD à inscrire.

Quand un utilisateur est membre d’un groupe d’inscription, tous ses appareils qui sont identifiés et pris en charge dans Azure AD sont inscrits et activables dans le service Lookout de protection des appareils contre les menaces.  La première fois que l’utilisateur ouvre l’application Lookout for Work sur un appareil pris en charge, ce dernier est activé dans Lookout.

![capture d’écran de la page d’inscription du connecteur Intune](media/lookout-enrollment.png)

La bonne pratique consiste à utiliser la valeur par défaut (5 minutes) pour l’incrément de durée de recherche de nouveaux appareils.

>[!IMPORTANT]
> Le nom complet respecte la casse.  Utilisez le **nom complet** indiqué dans la page **Propriétés** du groupe de sécurité dans le portail Azure. Notez que le nom complet utilise une casse mixte dans la page **Propriétés** du groupe de sécurité illustrée ci-dessous.  Le titre, qui est entièrement en minuscules, ne doit pas être utilisé pour accéder à la console Lookout.
>![capture d’écran du portail Azure, service Azure Active Directory, page Propriétés](media/aad-group-display-name.png)

La version actuelle présente les limitations suivantes :  
* Les noms complets des groupes ne sont pas validés.  Veillez à utiliser la valeur du champ **NOM COMPLET** affiché dans le portail Azure pour le groupe de sécurité Azure AD.
* La création de groupes à l’intérieur d’autres groupes n’est pas prise en charge.  Les groupes de sécurité Azure AD spécifiés ne peuvent contenir que des utilisateurs (les groupes imbriqués ne sont pas autorisés).


### <a name="step-4-configure-state-sync"></a>Étape 4 : Configurer la synchronisation des états
Dans l’option **Synchronisation des états**, spécifiez le type de données à envoyer à Intune.  Actuellement, vous devez activer l’état de l’appareil et l’état de la menace pour que l’intégration Lookout Intune fonctionne correctement.  Ces deux états sont activés par défaut.
### <a name="step-5-configure-error-report-email-recipient-information"></a>Étape 5 : Configurer le destinataire des rapports d’erreurs envoyés par e-mail
Dans l’option **Gestion des erreurs**, entrez l’adresse e-mail à laquelle doivent être envoyés les rapports d’erreurs.

![capture d’écran de la page Gestion des erreurs du connecteur Intune](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>Étape 6 : Configurer les paramètres d’inscription
Dans le module **Système**, dans la page **Connecteurs**, spécifiez le nombre de jours au terme desquels un appareil est considéré comme déconnecté.  Les appareils déconnectés sont considérés comme non conformes et ne peuvent pas accéder à vos applications d’entreprise en fonction des stratégies d’accès conditionnel SCCM. Vous pouvez spécifier des valeurs comprises entre 1 et 90 jours.

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>Étape 7 : Configurer les notifications par e-mail
Si vous souhaitez recevoir des alertes sur les menaces par e-mail, connectez-vous à la [console Lookout](https://aad.lookout.com) avec le compte d’utilisateur qui doit recevoir les notifications. Sous l’onglet **Préférences** du module **Système**, définissez les notifications souhaitées sur **ACTIVÉ**. Enregistrez vos modifications.

![capture d’écran de la page Préférences avec le compte d’utilisateur affiché](media/lookout-email-notifications.png) Si vous ne souhaitez plus recevoir de notifications par e-mail, définissez les notifications avec la valeur **DÉSACTIVÉ**, puis enregistrez vos modifications.
### <a name="step-8-configure-threat-classification"></a>Étape 8 : Configurer la classification des menaces
Le service Lookout de protection des appareils contre les menaces classe les différents types de menaces mobiles. Les [classifications des menaces dans Lookout](http://personal.support.lookout.com/hc/en-us/articles/114094130693) ont des niveaux de risque par défaut qui leur sont associés. Ces niveaux peuvent être modifiés à tout moment en fonction des besoins de votre entreprise.

![capture d’écran de la page de stratégie montrant des menaces et des classifications](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Les niveaux de risque spécifiés ici sont un aspect important du service Lookout de protection des appareils contre les menaces, car le processus d’intégration Intune s’en sert pour évaluer la conformité des appareils au moment de l’exécution. En d’autres termes, l’administrateur Intune définit une règle de stratégie qui identifie un appareil comme non conforme si celui-ci présente une menace active du niveau minimum configuré (haut, moyen ou faible). La stratégie de classification des menaces dans le service Lookout de protection des appareils contre les menaces a donc un impact direct sur l’évaluation de la conformité des appareils dans Intune.

## <a name="watching-enrollment"></a>Surveillance de l’inscription
Une fois la configuration terminée, le service Lookout de protection des appareils contre les menaces commence à interroger Azure AD pour rechercher les appareils qui correspondent aux groupes d’inscription spécifiés.  Les informations sur les appareils inscrits se trouvent dans le module Appareils.  Les appareils s’affichent dans l’état initial En attente.  L’état de l’appareil change une fois que l’application Lookout for Work est installée, ouverte et activée sur l’appareil.  Pour plus d’informations sur le transfert (pushing) de l’application Lookout for Work sur l’appareil, consultez la rubrique [Configurer et déployer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md).
## <a name="next-steps"></a>Étapes suivantes
[Activer la connexion à Lookout MTP dans Intune](enable-lookout-connection-in-intune.md)
