---
title: Gérer l'accès à SharePoint Online
titleSuffix: Configuration Manager
description: Apprenez à utiliser la stratégie d’accès conditionnel System Center Configuration Manager SharePoint Online pour gérer l’accès à OneDrive.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 69a160a3c7833f196d50185e551f619d68dc0925
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881739"
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gérer l’accès à SharePoint Online dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


La stratégie d’accès conditionnel de Configuration Manager pour **SharePoint Online** gère l’accès aux fichiers OneDrive Entreprise, qui sont stockés sur SharePoint Online. L’accès est basé sur les conditions que vous spécifiez.
Vous pouvez contrôler l'accès à SharePoint Online à partir des applications suivantes pour les plateformes répertoriées :  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android et iOS)  

-   Microsoft Word (Android et iOS)  

-   Microsoft Excel (Android et iOS)  

-   Microsoft PowerPoint (Android et iOS)  

-   Microsoft OneNote (Android et iOS)

Les applications de bureau Office peuvent accéder à SharePoint Online sur les PC exécutant :  

-   Office 2013 et ultérieur pour ordinateur avec [l’authentification moderne](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) activée.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Les PC doivent être joints au domaine ou être conformes aux stratégies définies dans Intune.  



 Quand un utilisateur ciblé tente de se connecter à un fichier à l’aide d’une application prise en charge telle que OneDrive sur son appareil, l’évaluation suivante se produit :  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Pour vous connecter aux fichiers requis, l'appareil exécutant OneDrive doit :  

- Être inscrit auprès de Microsoft Intune ou d’un PC joint à un domaine.  

- Inscrire l’appareil dans Azure Active Directory (Azure AD). Cette inscription se produit automatiquement quand l’appareil est inscrit auprès d’Intune.  

   Pour un PC joint à un domaine, vous devez le configurer de manière à ce qu’il [s’inscrive automatiquement](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) auprès d’Azure AD.  

- Être conforme aux stratégies de conformité Configuration Manager éventuellement déployées.  

  Azure AD stocke l’état de l’appareil. Il accorde ou bloque l’accès aux fichiers en fonction des conditions que vous spécifiez.  

  Si une condition n’est pas remplie, l’utilisateur reçoit l’un des messages suivants quand il tente de se connecter :  

- Si l’appareil n’est pas inscrit auprès d’Intune ou dans Azure AD, l’utilisateur reçoit un message contenant des instructions pour installer l’application Portail d’entreprise et inscrire l’appareil.  

- Si l’appareil n’est pas conforme, un message qui dirige l’utilisateur vers le portail web Intune s’affiche. Ils peuvent y trouver des informations sur le problème et la façon d’y remédier.  

- Pour les appareils mobiles :

  Vous pouvez restreindre l’accès à SharePoint Online par le biais d’un navigateur sur des appareils **iOS** et **Android**. L’accès est autorisé uniquement à partir des navigateurs pris en charge sur des appareils compatibles :  
  - Safari (iOS)
  - Chrome (Android)
  - Managed Browser (iOS et Android)  

    Les navigateurs non pris en charge sont bloqués.  

- Sur un PC :  


  -   Si la stratégie est définie de manière à exiger la jonction à un domaine et que le PC n’est pas joint à un domaine, un message invitant l’utilisateur à contacter l’administrateur informatique s’affiche.  

  -   Si la stratégie définie exige la jonction à un domaine ou la conformité, et que le PC ne répond pas l’une des conditions, un message contenant des instructions sur la façon d’installer l’application Portail d’entreprise et d’inscrire l’appareil s’affiche.  

Vous pouvez bloquer l'accès à SharePoint Online dans les applications suivantes :  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android et iOS)  

-   Microsoft Word (Android et iOS)  

-   Microsoft Excel (Android et iOS)  

-   Microsoft PowerPoint (Android et iOS)  

-   Microsoft OneNote (Android et iOS)  



## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurer l’accès conditionnel pour SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Étape 1 : Configurer des groupes de sécurité Active Directory  
 Avant de commencer, configurez les groupes de sécurité Azure AD pour la stratégie d’accès conditionnel. Vous pouvez configurer ces groupes dans le **centre d’administration Microsoft 365**, ou le **portail du compte Intune**. Ces groupes incluent les utilisateurs qui sont ciblés par la stratégie ou exemptés de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu’il utilise doit être conforme à cette stratégie pour accéder aux ressources.  

 Vous pouvez spécifier deux types de groupes dans une stratégie SharePoint Online :  

- **Groupes ciblés**: Contient des groupes d’utilisateurs auxquels s’applique la stratégie  

- **Groupes exemptés**: Contient des groupes d’utilisateurs exempts de la stratégie (facultatif)  

  Si un utilisateur se trouve dans les deux groupes, il est exempt de la stratégie.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Étape 2 : Configurer et déployer une stratégie de conformité  
 Créez et déployez une stratégie de conformité sur tous les appareils sur lesquels vous ciblez la stratégie SharePoint Online.  

> [!NOTE]   
>  Tandis que les stratégies de conformité sont déployées sur des groupes Intune ou des regroupements Configuration Manager, les stratégies d’accès conditionnel sont ciblées sur les groupes de sécurité Azure AD.  

 Pour plus d’informations sur la configuration de la stratégie de conformité, consultez [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Si vous n’avez pas déployé de stratégie de conformité et que vous activez la stratégie SharePoint Online, l’accès est accordé à tous les appareils ciblés.  

   

###  <a name="BKMK_OneDrive"></a> Étape 3 : Configurer la stratégie SharePoint Online  

 Ensuite, configurez la stratégie de manière à restreindre l'accès à SharePoint Online aux appareils gérés et conformes. Cette stratégie est stockée dans Azure AD.

 >[!NOTE]
 >Vous pouvez aussi créer une stratégie d’accès conditionnel dans la console de gestion Azure AD. La console de gestion Azure AD vous permet de créer les stratégies d’accès conditionnel aux appareils Intune. Azure AD fait référence à ces stratégies comme la stratégie d’accès conditionnel en fonction de l’appareil. Vous pouvez également créer d’autres stratégies d’accès conditionnel, comme l’authentification multifacteur. Dans le portail, vous pouvez définir des stratégies d’accès conditionnel pour des applications d’entreprise tierces prises en charge par Azure AD, comme Salesforce et Box. Pour plus d’informations, consultez [Guide pratique pour définir la stratégie d’accès conditionnel en fonction de l’appareil Azure AD pour contrôler l’accès aux applications connectées Azure AD](/azure/active-directory/active-directory-conditional-access-policy-connected-applications).  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Sélectionnez **Activer la stratégie d’accès conditionnel pour SharePoint Online**.  

    ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3. Sous **Accès à l’application** pour Outlook et les applications qui utilisent une authentification moderne, vous pouvez choisir de restreindre l’accès aux seuls appareils conformes pour chaque plateforme.  

   > [!TIP]
   >  L’**authentification moderne** permet aux clients Office de bénéficier de la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library).  
   > 
   > - L’authentification ADAL permet aux clients Office de procéder à une authentification basée sur un navigateur (également appelée « authentification passive »). Pour s'authentifier, l'utilisateur est dirigé vers une page web de connexion.  
   >   -   Cette nouvelle méthode de connexion permet de nouveaux scénarios comme l’accès conditionnel basé sur la **compatibilité des appareils** et sur l’exécution préalable de l’**authentification multifacteur**.  
   > 
   >   Pour plus d’informations, consultez [Fonctionnement de l’authentification moderne pour les applications clientes Office 2013 et Office 2016](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517).  

    Pour les PC Windows, ceux-ci doivent être joints à un domaine ou inscrits auprès d’Intune et être conformes. Vous pouvez définir les conditions suivantes :  

   -   **Les appareils doivent être joint au domaine ou conformes**: Le PC doit être joint au domaine ou conformes aux stratégies définies dans Intune. Si le PC ne remplit pas l’une de ces conditions requises, l’utilisateur est invité à inscrire l’appareil auprès d’Intune.  

   -   **Les appareils doivent être joints à un domaine**: Les PC doivent être joints pour accéder à Exchange Online. Si le PC n’est pas joint à un domaine, l’accès à la messagerie électronique est bloqué et l’utilisateur est invité à contacter l’administrateur informatique.  

   -   **Les appareils doivent être conformes**: Les PC doivent être inscrits dans Intune et conformes. Si le PC n’est pas inscrit, un message contenant des instructions sur la procédure d’inscription à suivre s’affiche.  

4. Sous **accès du navigateur** à SharePoint Online et OneDrive entreprise, vous pouvez choisir d’autoriser l’accès à Exchange Online uniquement via les navigateurs pris en charge : Safari (iOS) et Chrome (Android). L’accès à partir d’autres navigateurs est bloqué. Les mêmes restrictions de plateforme que celles que vous avez sélectionnées pour l’accès aux applications pour OneDrive s’appliquent également ici.

   Sur les appareils **Android**, les utilisateurs doivent activer l’option **Activer l’accès au navigateur** sur l’appareil inscrit, en procédant comme suit :
   1.  Lancez **l’application Portail d’entreprise**.
   2.  Accédez à la page **Paramètres** via les trois points (...) ou le bouton de menu matériel.
   3.  Appuyez sur le bouton **Activer l’accès du navigateur** .
   4.  Dans le navigateur Chrome, déconnectez-vous d’Office 365 et redémarrez Chrome.

   Sur les plateformes **iOS et Android**, pour identifier l’appareil utilisé pour accéder au service, Azure AD émet un certificat TLS pour l’appareil. L’appareil affiche le certificat avec une invite demandant à l’utilisateur final pour sélectionner le certificat, comme indiqué dans les captures d’écran suivante : L’utilisateur final doit sélectionner ce certificat avant de pouvoir continuer à utiliser le navigateur.

    **iOS**

    ![capture d’écran de l’invite de certificat sur un iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

     ![capture d’écran de l’invite de certificat sur un appareil Android](media/mdm-browser-ca-android-cert-prompt.png)

5. Sous l'onglet **Accueil** , dans le groupe **Liens** , cliquez sur **Configurer la stratégie d'accès conditionnel dans la console Intune**. Il se peut que vous deviez fournir le nom d’utilisateur et le mot de passe du compte utilisé pour connecter Configuration Manager à Intune.  

    La console d’administration Intune s’ouvre.  

6. Dans la console [console d'administration Microsoft Intune](https://manage.microsoft.com), cliquez sur **Stratégie** > **Accès conditionnel** > **SharePoint Online Stratégie**.  

7. Sélectionnez **Bloquez l'accès des applications à SharePoint Online si l'appareil n'est pas conforme**.  

8. Sous **Groupes ciblés**, cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure AD auxquels la stratégie s’applique.  

9. Sous **Groupes exemptés**, cliquez éventuellement sur **Modifier** pour sélectionner les groupes de sécurité Azure AD exempts de cette stratégie.  

10. Une fois terminé, cliquez sur **Enregistrer**.  

    La stratégie d’accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

    Consultez [Gérer l’accès à SharePoint Online avec Microsoft Intune](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune) pour savoir comment contrôler la stratégie à partir de la console Intune.  

### <a name="see-also"></a>Voir aussi  

 [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
