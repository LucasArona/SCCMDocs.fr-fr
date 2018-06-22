---
title: Accès conditionnel
titleSuffix: Configuration Manager
description: Découvrez comment utiliser l’accès conditionnel dans System Center Configuration Manager pour sécuriser la messagerie et d’autres services.
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f354647ba9376ff18db1a4b63944ef31272308e1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350576"
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gérer l’accès aux services dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Accès conditionnel dans System Center Configuration Manager
Utilisez l’accès conditionnel pour spécifier des conditions permettant de sécuriser l’e-mail et d’autres services sur les appareils inscrits auprès de Microsoft Intune.  

 Pour plus d’informations sur l’accès conditionnel sur des appareils gérés avec le client Configuration Manager, consultez [Gérer l’accès aux services O365 pour les PC gérés par System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 La procédure classique pour configurer l'accès conditionnel est la suivante :  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Utilisez l'accès conditionnel pour gérer l'accès aux services suivants :  

-   Microsoft Exchange sur site  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype Entreprise Online

-   Dynamics CRM Online

 Pour implémenter un accès conditionnel, vous configurez deux types de stratégies dans Configuration Manager :  

-   Les **stratégies de conformité** sont des stratégies facultatives que vous pouvez déployer dans des regroupements d’utilisateurs et qui évaluent des paramètres comme :  

    -   Code secret  

    -   Chiffrement  

    -   Si l'appareil est jailbreaké ou rooté  

    -   Indique si les e-mails sur l’appareil sont gérés par une stratégie Configuration Manager ou Microsoft Intune  

     Un appareil est signalé conforme pour toutes les stratégies d’accès conditionnel applicables si vous ne déployez pas de stratégie de conformité sur celui-ci.

-   Les **stratégies d’accès conditionnel** sont destinées à un service particulier. Ces stratégies définissent des règles comme les groupes de sécurité Azure Active Directory ou les regroupements d’utilisateurs Configuration Manager à cibler ou à exclure.  

     Vous configurez la stratégie d’accès conditionnel Exchange local à partir de la console Configuration Manager. Cependant, quand vous configurez une stratégie Exchange Online ou SharePoint Online, la console Microsoft Intune s’ouvre pour configurer la stratégie.  

     Contrairement aux autres stratégies Microsoft Intune ou Configuration Manager, vous ne déployez pas les stratégies d’accès conditionnel. Au lieu de cela, vous configurez ces stratégies une seule fois et celles-ci s’appliquent à tous les utilisateurs ciblés.  

 Quand un appareil ne remplit pas les conditions configurées, l’utilisateur est guidé tout au long de l’inscription de l’appareil et de la résolution du problème de conformité de l’appareil.  

Avant de commencer à utiliser l'accès conditionnel, vérifiez que les spécifications requises correctes sont satisfaites :  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Configuration requise pour Exchange Online (en utilisant l’environnement mutualisé partagé)
L'accès conditionnel à Exchange Online prend en charge les appareils qui exécutent :
-   Windows 8.1 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
-   Windows 7.0 ou Windows 8.1 (quand ils sont joints au domaine)
-   Windows Phone 8.1 et versions ultérieures
-   iOS 7.1 et versions ultérieures
-   Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur

 **De plus** :
-   Les appareils doivent être joints à un espace de travail, qui inscrit l'appareil auprès du service Azure Active Directory Device Registration Service (AAD DRS).<br />     
- Les PC joints au domaine doivent être inscrits automatiquement auprès d'Azure Active Directory via la stratégie de groupe ou MSI.

  La section **Accès conditionnel pour les PC** de cet article décrit toute la configuration requise pour l’activation de l’accès conditionnel pour un PC.<br />     
  Le service AAD DRS s’active automatiquement pour les clients Microsoft Intune et Office 365. Les clients qui ont déjà déployé le service ADFS Device Registration Service ne voient pas les appareils inscrits dans leur annuaire Active Directory local.
-   Utilisez un abonnement Office 365 qui comprend Exchange Online (comme E3). Les utilisateurs doivent avoir une licence pour Exchange Online.
-   Le connecteur Exchange Server est facultatif et connecte Configuration Manager à Microsoft Exchange Online. Ce connecteur vous permet de surveiller les informations sur l’appareil par le biais de la console Configuration Manager. Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
Vous n’avez pas besoin du connecteur pour utiliser des stratégies de conformité ou des stratégies d’accès conditionnel. L’exécution de rapports sur l’impact de l’accès conditionnel nécessite le connecteur.

## <a name="requirements-for-exchange-online-dedicated"></a>Configuration requise pour Exchange Online Dedicated
L'accès conditionnel à Exchange Online Dedicated prend en charge les appareils qui exécutent :
-   Windows 8 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
-   Windows 7.0 ou Windows 8.1 (quand ils sont joints au domaine)

  Accès conditionnel aux PC joints au domaine uniquement pour les locataires dans le nouvel environnement dédié Exchange Online.
-   Windows Phone 8 et versions ultérieures
-   Tout appareil iOS utilisant un client de messagerie Exchange ActiveSync (EAS)
-   Android 4 et ultérieur.
-   Pour les clients dans l'environnement Exchange Online Dedicated hérité :    

  Utilisez le connecteur Exchange Server, qui connecte Configuration Manager à Microsoft Exchange sur site. Le connecteur vous permet de gérer les appareils mobiles et active l’accès conditionnel. Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
-   Pour les clients dans le nouvel environnement Exchange Online Dedicated :     
  Le connecteur Exchange Server, qui est facultatif, connecte Configuration Manager à Microsoft Exchange Online et vous permet de gérer les informations sur les appareils. Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md). Vous n’avez pas besoin du connecteur pour utiliser des stratégies de conformité ou des stratégies d’accès conditionnel. L’exécution de rapports sur l’impact de l’accès conditionnel nécessite le connecteur.  

## <a name="requirements-for-exchange-on-premises"></a>Configuration requise pour Exchange sur site
L’accès conditionnel à Exchange sur site prend en charge les éléments suivants :
-   Windows 8 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
-   Windows Phone 8 et versions ultérieures
-   Application de messagerie native sur iOS
-   Application de messagerie native sur Android 4 ou version ultérieure
-   L’application Microsoft Outlook n’est pas prise en charge (Android et iOS)

**De plus** :

- La version d’Exchange doit être Exchange 2010 ou une version ultérieure
- La baie de serveurs d’accès au client (CAS) du serveur Exchange est prise en charge

> [!TIP]
> Si votre environnement Exchange est dans une configuration de serveur CAS, vous devez configurer le connecteur Exchange sur site pour pointer vers l’un des serveurs CAS.
- Utilisez le connecteur Exchange Server, qui connecte Configuration Manager à Microsoft Exchange sur site. Le connecteur vous permet de gérer les appareils mobiles et active l’accès conditionnel. Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Assurez-vous d’utiliser la dernière version du connecteur Exchange local. Configurez le connecteur Exchange local à l’aide de la console Configuration Manager. Pour obtenir une procédure pas à pas, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Configurer uniquement le connecteur sur le site principal de Configuration Manager

- Exchange ActiveSync peut être configuré avec l’authentification basée sur les certificats ou une entrée d’informations d’identification utilisateur


## <a name="requirements-for-skype-for-business-online"></a>Configuration requise pour Skype Entreprise Online
L'accès conditionnel à SharePoint Online prend en charge les appareils qui exécutent :
 -   iOS 7.1 et versions ultérieures
 -   Android 4.0 et versions ultérieures
 -   Samsung Knox Standard 4.0 ou ultérieur

Activez [l’authentification moderne](https://aka.ms/SkypeModernAuth) pour Skype Entreprise Online. 

Tous vos utilisateurs doivent utiliser Skype Entreprise Online. Si vous avez un déploiement avec à la fois Skype Entreprise Online et Skype Entreprise en local, la stratégie d’accès conditionnel ne s’applique pas aux utilisateurs locaux.

## <a name="requirements-for-sharepoint-online"></a>Configuration requise pour SharePoint Online
L'accès conditionnel à SharePoint Online prend en charge les appareils qui exécutent :
 -   Windows 8.1 et versions ultérieures (quand ils sont inscrits auprès d’Intune)
 -   Windows 7.0 ou Windows 8.1 (quand ils sont joints au domaine)
 -   Windows Phone 8.1 et versions ultérieures
 -   iOS 7.1 et versions ultérieures
 -   Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur

 **De plus** :
 -   Les appareils doivent être joints à un espace de travail, qui inscrit l'appareil auprès du service Azure Active Directory Device Registration Service (AAD DRS).

 Les PC joints au domaine doivent être inscrits automatiquement auprès d'Azure Active Directory via la stratégie de groupe ou MSI. La section **Accès conditionnel pour les PC** de cet article décrit toute la configuration requise pour l’activation de l’accès conditionnel pour un PC.

 Le service AAD DRS s’active automatiquement pour les clients Microsoft Intune et Office 365. Les clients qui ont déjà déployé le service ADFS Device Registration Service ne voient pas les appareils inscrits dans leur annuaire Active Directory local.
 -   Un abonnement SharePoint Online est requis et les utilisateurs doivent disposer d'une licence pour SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Accès conditionnel pour les PC

 Vous pouvez configurer l’accès conditionnel pour les PC qui exécutent des applications de bureau Office, et accéder à Exchange Online ou à SharePoint Online. Les PC doivent répondre aux exigences suivantes :
 -   Le PC doit exécuter Windows 7.0 ou Windows 8.1
 -   Le PC doit être joint à un domaine ou être conforme

 Pour être conforme, le PC doit être inscrit auprès de Microsoft Intune et être conforme aux stratégies.

 Pour les PC joints à un domaine, vous devez le configurer pour qu’il [s’inscrive automatiquement](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) auprès d’Azure Active Directory.
 -   [L'authentification moderne Office 365 doit être activée](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)et toutes les mises à jour Office les plus récentes doivent être installées.<br />     L’authentification moderne permet aux clients Windows Office 2013 d’utiliser la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library) et permet de bénéficier d’une sécurité accrue telle que l’authentification multifacteur et l’authentification basée sur les certificats.
 -   Configurez des règles de revendications AD FS pour bloquer les protocoles autres que l'authentification moderne.  

## <a name="next-steps"></a>Étapes suivantes  
 Lisez les rubriques suivantes pour savoir comment configurer des stratégies de conformité et des stratégies d'accès conditionnel pour votre scénario :  

-   [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Gérer l’accès à la messagerie dans System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Gérer l’accès à SharePoint Online dans System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Gérer l’accès à Skype Entreprise Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Voir aussi  

 [Bien démarrer avec les paramètres de compatibilité dans System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)
