---
title: Configurer la gestion hybride des appareils Windows avec Microsoft Intune
titleSuffix: Configuration Manager
description: Configurez la gestion des appareils Windows avec System Center Configuration Manager et Microsoft Intune.
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e45cae03754fcfa3a310bf59e8e3280d5088518
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurer la gestion hybride des appareils mobiles Windows avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique explique aux administrateurs informatiques comment utiliser Configuration Manager et Microsoft Intune pour permettre à leurs utilisateurs d’inscrire des appareils mobiles et des PC Windows à la gestion.

## <a name="enable-windows-device-management"></a>Activer la gestion des appareils Windows
Pour activer la gestion des appareils Windows sur des PC ou des appareils mobiles, procédez comme suit :

1.  Avant de configurer l’inscription pour n’importe quelle plateforme, tenez compte des prérequis et des procédures figurant dans [Configurer la gestion hybride des appareils mobiles](setup-hybrid-mdm.md).  
2.  Dans la console Configuration Manager, dans l’espace de travail **Administration**, accédez à **Vue d’ensemble** > **Services Cloud** > **Abonnements Microsoft Intune**.  
3.  Dans le ruban, cliquez sur **Configurer des plateformes**, puis sélectionnez la plateforme Windows :
    - **Windows** pour les PC et ordinateurs portables Windows, puis procédez comme suit :
      1. Sous l’onglet **Général**, cochez la case **Activer l’inscription Windows**.
      2. Si vous utilisez un certificat pour signer le code et déployer l’application Portail d’entreprise, accédez à **Certificat de signature de code**. Les utilisateurs d’appareils peuvent également installer l’application Portail d’entreprise à partir du Microsoft Store, ou vous pouvez déployer l’application à partir du Microsoft Store pour Entreprises sans signature de code.
      3. Vous pouvez aussi configurer [Paramètres Windows Hello Entreprise](windows-hello-for-business-settings.md).
    - **Windows Phone** pour les téléphones et tablettes Windows, puis procédez comme suit :
      1. Sous l’onglet **Général**, cochez la case **Windows Phone 8.1 et Windows 10 Mobile**. Windows Phone 8.0 n’est plus pris en charge.
      2. Si votre organisation a besoin de charger indépendamment des applications d’entreprise, vous pouvez charger le jeton ou le fichier exigé. Pour plus d’informations sur le chargement indépendant d’applications, consultez [Créer des applications Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Jeton d’inscription d’application**
        - **Fichier .pfx**
        - **Aucun** Si vous utilisez un certificat Symantec, vous pouvez spécifier **Afficher une alerte avant l’expiration du certificat Symantec**.
4. Cliquez sur **OK** pour fermer la boîte de dialogue.  Pour simplifier le processus d’inscription à l’aide du portail d’entreprise, créez un alias DNS pour l’inscription des appareils. Ensuite, expliquez aux utilisateurs comment inscrire leurs appareils.

## <a name="choose-how-to-enroll-windows-devices"></a>Choisir comment inscrire les appareils Windows

Une fois que vous avez attribué des licences Intune aux utilisateurs, vous pouvez inscrire les appareils Windows sans étapes supplémentaires et vous pouvez faciliter l’inscription pour les utilisateurs.

Deux facteurs déterminent la façon dont vous pouvez simplifier l’inscription des appareils Windows :
- **Utilisez-vous Azure Active Directory Premium ?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) est inclus avec Enterprise Mobility + Security et d’autres plans de licence.
- **Quelles versions des clients Windows allez-vous inscrire ?** <br>Les appareils Windows 10 peuvent s’inscrire automatiquement quand vous ajoutez un compte professionnel ou scolaire. L’inscription des versions antérieures doit s’effectuer à l’aide de l’application Portail d’entreprise.

||**Azure AD Premium**|**Autre AD** |
|----------|---------------|---------------|  
|**Windows 10**|[Inscription automatique](#enable-windows-10-automatic-enrollment) |[Inscription d’utilisateur](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versions précédentes de Windows**|[Inscription d’utilisateur](#enable-windows-enrollment-without-azure-ad-premium)|[Inscription d’utilisateur](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Activer l’inscription automatique Windows 10

L’inscription automatique permet aux utilisateurs d’inscrire des PC Windows 10 appartenant à l’entreprise ou personnels et des appareils Windows 10 Mobile dans Intune en ajoutant un compte professionnel ou scolaire et en acceptant leur gestion. C’est aussi simple que cela. En arrière-plan, l’appareil de l’utilisateur s’inscrit et rejoint Azure Active Directory. Une fois inscrit, l’appareil est géré avec Intune.

**Conditions préalables**
- Abonnement Premium à Azure Active Directory ([abonnement d’évaluation](http://go.microsoft.com/fwlink/?LinkID=816845))
- Abonnement Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurer l’inscription automatique de la gestion des appareils mobiles

1. Connectez-vous au [portail de gestion Azure](https://portal.azure.com) (https://manage.windowsazure.com) et sélectionnez **Azure Active Directory**.

  ![Capture d’écran montrant le portail Azure](../media/auto-enroll-azure-main.png)

2. Sélectionnez **Mobilité (gestion des données de référence et gestion des applications mobiles)**.

  ![Capture d’écran montrant le portail Azure](../media/auto-enroll-mdm.png)

3. Sélectionnez **Microsoft Intune**.

  ![Capture d’écran montrant le portail Azure](../media/auto-enroll-intune.png)

4. Configurez **Portée de l’utilisateur Gestion des données de référence**. Spécifiez les appareils des utilisateurs qui doivent être gérés par Microsoft Intune. Les appareils Windows 10 de ces utilisateurs sont automatiquement inscrits à la gestion avec Microsoft Intune.

    - **Aucun**
    - **Partiel**
    - **Tous**

   ![Capture d’écran montrant le portail Azure](../media/auto-enroll-scope.png)

5. Utilisez les valeurs par défaut pour les URL suivantes :
    - **URL des conditions d’utilisation de la gestion des données de référence**
    - **URL de détection MDM**
    - **URL de conformité GAM**

6. Sélectionnez **Enregistrer**.


Par défaut, l’authentification à deux facteurs n’est pas activée pour le service. Toutefois, l’authentification à deux facteurs est recommandée au moment de l’inscription d’un appareil. Avant d’exiger l’authentification à deux facteurs pour ce service, vous devez configurer un fournisseur d’authentification à deux facteurs dans Azure Active Directory et configurer vos comptes d’utilisateur pour l’authentification multifacteur. Consultez [Bien démarrer avec le serveur Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Activer l’inscription Windows sans Azure AD Premium
Vous pouvez autoriser les utilisateurs à inscrire leurs appareils sans l’inscription automatique Azure AD Premium. Une fois que vous avez attribué des licences, les utilisateurs peuvent s’inscrire lorsqu’ils ont ajouté leur compte professionnel à leurs appareils personnels ou qu’ils ont joint leurs appareils d’entreprise à Azure AD. La création d’un alias DNS (type d’enregistrement CNAME) permet aux utilisateurs d’inscrire leurs appareils avec plus de facilité. Si vous créez des enregistrements de ressources CNAME DNS, les utilisateurs se connectent et s’inscrivent à Intune sans entrer le nom de serveur Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Créer des enregistrements CNAME pour simplifier l’inscription
Créez des enregistrements de ressources CNAME DNS pour le domaine de votre entreprise. Par exemple, si le site web de votre entreprise est contoso.com, vous devez créer un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com.

La création d’entrées CNAME dans DNS est facultative, mais les enregistrements CNAME facilitent l’inscription pour les utilisateurs. Si aucun enregistrement CNAME d’inscription n’est trouvé, les utilisateurs sont invités à taper le nom du serveur de gestion des appareils mobiles (enrollment.manage.microsoft.com).

|Tapez|Nom de l'hôte|Pointe vers|TTL|  
|----------|---------------|---------------|---|
|CNAME|enterpriseenrollment.domaine_entreprise.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 heure|

Si vous avez plusieurs suffixes UPN, vous devez créer un enregistrement CNAME pour chaque nom de domaine et pointer chacun d’eux vers EnterpriseEnrollment-s.manage.microsoft.com. Par exemple, si les utilisateurs de Contoso utilisent name@contoso.com, mais aussi name@us.contoso.com et name@eu.constoso.com comme e-mail/UPN, l’administrateur DNS de Contoso doit créer les enregistrements CNAME suivants.

|Tapez|Nom de l'hôte|Pointe vers|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 heure|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 heure|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 heure|

`EnterpriseEnrollment-s.manage.microsoft.com` : prend en charge une redirection vers le service Intune avec reconnaissance du domaine à partir du nom de domaine de l’e-mail.

La propagation des modifications DNS peut prendre jusqu’à 72 heures. Vous ne pouvez pas vérifier la modification DNS dans Intune tant que l’enregistrement DNS ne s’est pas propagé.

## <a name="tell-users-how-to-enroll-devices"></a>Expliquer aux utilisateurs comment inscrire des appareils  

 Une fois la configuration effectuée, vous devez faire savoir aux utilisateurs comment inscrire leurs appareils. Pour obtenir de l’aide, consultez [Ce qu’il faut dire aux utilisateurs sur l’inscription de leurs appareils](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Indiquez aux utilisateurs de consulter [Inscrire un appareil Windows dans Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Ces informations s’appliquent aux appareils mobiles gérés par Microsoft Intune et Configuration Manager.

> [!div class="button"]
[< Étape précédente](create-service-connection-point.md) [Étape suivante >](set-up-additional-management.md)
