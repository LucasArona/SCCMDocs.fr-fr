---
title: Gérer l’accès aux services Office 365
titleSuffix: Configuration Manager
description: Découvrez comment configurer l’accès conditionnel aux services Office 365 pour les PC gérés par System Center Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 434801b170ed5efcbbafa046a3ac1e94a615ed3d
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196770"
---
# <a name="manage-access-to-office-365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gérer l’accès aux services Office 365 pour les PC gérés par System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1191496-->
Configurez l’accès conditionnel aux services Office 365 pour les PC gérés par Configuration Manager.  

> [!Important]  
> Y compris la gestion des appareils mobiles hybride sur site l’accès conditionnel sont [fonctionnalités déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, consultez [Qu’est-ce que la gestion hybride des appareils mobiles ?](/sccm/mdm/understand/hybrid-mobile-device-management)<!--Intune feature 2683117-->  
> 
> Si vous utilisez l’accès conditionnel sur des appareils gérés avec le client Configuration Manager, pour vous assurer qu’ils sont toujours protégées, tout d’abord activer l’accès conditionnel dans Intune pour ces appareils avant de migrer. Activer la cogestion dans Configuration Manager, déplacer la charge de travail de stratégie de conformité dans Intune, puis terminez votre migration à partir d’Intune hybride vers Intune autonome. Pour plus d’informations, consultez [d’accès conditionnel avec la cogestion](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 


Pour plus d’informations sur la configuration de l’accès conditionnel pour les appareils inscrits et gérés par Microsoft Intune, consultez [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md). Cet article aborde également les appareils qui sont joints à un domaine et dont la conformité n’est pas évaluée.

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="supported-services"></a>Services pris en charge  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>PC pris en charge  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Serveurs Windows pris en charge

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > Pour les serveurs Windows auxquels plusieurs utilisateurs peuvent être connectés simultanément, déployez les mêmes stratégies d’accès conditionnel pour tous ces utilisateurs.

## <a name="configure-conditional-access"></a>Configurer un accès conditionnel  
 Pour configurer un accès conditionnel, vous devez d’abord créer une stratégie de conformité, puis configurer une stratégie d’accès conditionnel. Quand vous configurez des stratégies d’accès conditionnel pour des PC, vous pouvez exiger que ceux-ci soient conformes pour pouvoir accéder aux services Exchange Online et SharePoint Online.  

### <a name="prerequisites"></a>Prérequis  

- Synchronisation d’ADFS et un abonnement Office 365. L’abonnement à Office 365 est pour la configuration d’Exchange Online et SharePoint Online.  

- Abonnement Microsoft Intune L’abonnement Microsoft Intune doit être configuré dans la console Configuration Manager. L’abonnement Intune sert à transférer l’état de conformité des appareils à Azure Active Directory et à accorder les licences d’utilisateur.  

  Les PC doivent répondre aux exigences suivantes :  

- [Conditions préalables](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) pour l’inscription automatique auprès d’Azure Active Directory.  

   Vous pouvez inscrire des PC auprès d’Azure AD via la stratégie de conformité.  

  -   Pour des PC Windows 8.1 et Windows 10, vous pouvez utiliser une stratégie de groupe Active Directory pour configurer vos appareils de façon à ce qu’ils s’inscrivent automatiquement auprès d’Azure AD.  

  -   o   Pour des PC Windows 7, vous devez déployer le package logiciel d’inscription de l’appareil sur le PC par le biais de System Center Configuration Manager. Pour plus de détails, consultez l’article [Inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).  

- Les PC doivent utiliser Office 2013 ou Office 2016 avec l’authentification moderne [activée](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

  Les étapes suivantes s’appliquent aussi bien à Exchange Online qu’à SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Étape 1. Configurer une stratégie de conformité  
 Dans la console Configuration Manager, créez une stratégie de conformité avec les règles suivantes :  

-   **Exiger l’inscription dans Azure Active Directory :** Cette règle vérifie si l’appareil de l’utilisateur est l’espace de travail joints à Azure AD et dans le cas contraire, l’appareil est automatiquement inscrit dans Azure AD. L’inscription automatique est prise en charge seulement sur Windows 8.1. Pour les PC Windows 7, déployez un fichier MSI pour effectuer l’inscription automatique. Pour plus d’informations, consultez [Inscription automatique d’appareils auprès d’Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).  

-   **Toutes les mises à jour requises installées avec une échéance supérieure à un certain nombre de jours :** Spécifiez la valeur pour la période de grâce à partir de l’échéance du déploiement des mises à jour requises sur l’appareil de l’utilisateur. L’ajout de cette règle installe aussi automatiquement les mises à jour obligatoires en attente. Spécifiez les mises à jour obligatoires dans la règle **Mises à jour automatiques requises**.   

-   **Exiger le chiffrement de lecteur BitLocker :** Cette règle vérifie si le lecteur principal (par exemple, C:\\) sur l’appareil est chiffré avec BitLocker. Si BitLocker chiffrement n’est pas activé sur le périphérique principal, l’accès aux services de messagerie et SharePoint est bloqué.  

-   **Exiger un logiciel anti-programme malveillant :** Cette règle vérifie si System Center Endpoint Protection ou Windows Defender est activé et en cours d’exécution. S’il n’est pas activé, l’accès aux services de messagerie et SharePoint est bloqué.  

-   **Signalés comme intègres par le Service d’attestation d’intégrité :** Cette condition inclut quatre règles secondaires pour vérifier la conformité des appareils contre le service d’attestation de l’intégrité des appareils. Pour plus d’informations, consultez [Attestation d’intégrité](/sccm/core/servers/manage/health-attestation). 

    - **Exiger l’activation de BitLocker sur l’appareil**
    - **Exiger l’activation du démarrage sécurisé sur l’appareil** 
    - **Exiger l’activation de l’intégrité du code sur l’appareil**
    - **Exiger l’activation du logiciel anti-programme malveillant sur l’appareil**  

    >[!Tip]  
    > Les critères d’accès conditionnel pour l’attestation d’intégrité de l’appareil ont été ajoutés à la version 1710, sous la forme d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1802, cette fonctionnalité n’est plus en préversion.<!--1235616-->  

    > [!Note]  
    > Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Étape 2. Évaluer l’incidence de l’accès conditionnel  
 Exécutez le **rapport de conformité de l’accès conditionnel**. Il se trouve dans l’espace de travail **Analyse**, sous **Rapports** > **Gestion de la conformité et des paramètres**. Ce rapport affiche l’état de conformité de tous les appareils. L’accès à Exchange Online et à SharePoint Online d’appareils signalés non conformes est bloqué.  

 ![Console Configuration Manager, espace de travail analyse, création de rapports, rapports, de conformité et la gestion des paramètres : Rapport de conformité de l’accès conditionnel](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurer les groupes de sécurité Active Directory  
 Les stratégies d’accès conditionnel ciblent des groupes d’utilisateurs en fonction des types de stratégies. Ces groupes contiennent les utilisateurs que la stratégie cible ou qui sont exemptés de celle-ci. Quand une stratégie cible un utilisateur, chaque appareil qu’il utilise doit être conforme à cette stratégie pour pouvoir accéder au service.  

 Groupes d’utilisateurs de sécurité Active Directory. Ces groupes d’utilisateurs doivent être synchronisés sur Azure Active Directory. Vous pouvez également configurer ces groupes dans le centre d’administration Microsoft 365 ou le portail de compte Intune.  

 Vous pouvez spécifier deux types de groupes dans chaque stratégie. :  

-   **Groupes ciblés** : groupes d’utilisateurs auxquels la stratégie est appliquée. Le même groupe doit être utilisé pour satisfaire aux exigences de conformité et à la stratégie d’accès conditionnel.  

-   **Groupes exemptés :** groupes d’utilisateurs exempts de la stratégie (facultatif).  
    Si un utilisateur se trouve dans les deux, il est exempté de la stratégie.  

     Seuls les groupes ciblés par la stratégie d’accès conditionnel sont évalués.  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Étape 3. Créer une stratégie d’accès conditionnel pour Exchange Online et SharePoint Online  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Pour créer une stratégie pour Exchange Online, sélectionnez **Activer la stratégie d’accès conditionnel pour Exchange Online**.  

     Pour créer une stratégie pour SharePoint Online, sélectionnez **Activer la stratégie d’accès conditionnel pour SharePoint Online**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Liens**, cliquez sur **Configurer la stratégie d’accès conditionnel dans la console Intune**. Il se peut que vous deviez fournir le nom d’utilisateur et le mot de passe du compte utilisé pour connecter Configuration Manager à Intune.  

     La console d’administration Intune s’ouvre.  

4.  Pour Exchange Online, dans la console d’administration Microsoft Intune, cliquez sur **Stratégie > Accès conditionnel > Stratégie Exchange Online**.  

     Pour SharePoint Online, dans la console d’administration Microsoft Intune, cliquez sur **Stratégie > Accès conditionnel > Stratégie SharePoint Online**.  

5.  Définissez la configuration requise du PC Windows sur l’option**Les appareils doivent être conformes**.  

6.  Sous **Groupes ciblés**, cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory auxquels la stratégie s’applique.  

    > [!NOTE]  
    >  Le même groupe d’utilisateurs de sécurité doit être utilisé pour déployer la stratégie de conformité et le groupe ciblé pour la stratégie d’accès conditionnel.  

     Sous **Groupes exemptés**, vous pouvez éventuellement cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory exempts de cette stratégie.  

7.  Cliquez sur **Enregistrer** pour créer et enregistrer la stratégie.  

Les utilisateurs voient les informations de compatibilité dans le Centre logiciel. Quand ils sont bloqués en raison d’une non-conformité, lancez une nouvelle évaluation de la stratégie après avoir résolu les problèmes de conformité.  


## <a name="see-also"></a>Voir aussi

- [Protéger les données et l’infrastructure des sites avec System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)
- [Organigramme de résolution des problèmes d’accès conditionnel pour Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)
