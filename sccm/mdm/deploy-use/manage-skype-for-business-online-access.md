---
title: Gérer l’accès à Skype Entreprise Online
titleSuffix: Configuration Manager
description: Apprenez à utiliser la stratégie d’accès conditionnel pour gérer l’accès à Skype Entreprise Online.
ms.date: 12/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4a88706233e85be6960585963c26bd740e9ff6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348264"
---
# <a name="manage-skype-for-business-online-access"></a>Gérer l’accès à Skype Entreprise Online

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez une stratégie d’accès conditionnel pour Skype Entreprise Online pour gérer l’accès à Skype Entreprise Online en fonction des conditions que vous spécifiez.  


 Quand un utilisateur ciblé tente d’utiliser Skype Entreprise Online sur son appareil, voici l’évaluation qui se produit :![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>Prérequis  

-   Activez [l’authentification moderne](https://aka.ms/SkypeModernAuth) pour Skype Entreprise Online.   

-   Tous vos utilisateurs doivent utiliser Skype Entreprise Online. Si vous avez un déploiement avec à la fois Skype Entreprise Online et Skype Entreprise en local, la stratégie d’accès conditionnel ne s’applique pas aux utilisateurs locaux.  

-   L’appareil devant accéder à Skype Entreprise Online doit :  

    -   être un appareil Android ou iOS

    -   être inscrit auprès de Microsoft Intune

    -   être conforme à toutes les stratégies de conformité Microsoft Intune déployées

 Azure Active Directory stocke l’état de l’appareil, qui accorde ou bloque l’accès aux fichiers en fonction des conditions que vous spécifiez.  
Si une condition n’est pas remplie, l’utilisateur voit l’un des messages suivants quand il se connecte :  

-   Si l’appareil n’est pas inscrit auprès de Microsoft Intune ou dans Azure Active Directory, l’utilisateur voit des instructions concernant l’installation de l’application Portail d’entreprise et l’inscription de l’appareil.  

-   Si l’appareil n’est pas conforme, l’utilisateur voit un message le dirigeant vers le site web du portail d’entreprise ou l’application Portail d’entreprise. Le portail d’entreprise fournit des informations relatives à ce problème et des solutions pour y remédier.  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Configurer l’accès conditionnel pour Skype Entreprise Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Étape 1 : configurer les groupes de sécurité Active Directory  
 Avant de commencer, configurez les groupes de sécurité Azure Active Directory pour la stratégie d'accès conditionnel. Configurez ces groupes dans le Centre d’administration Office 365. Ces groupes contiennent les utilisateurs à cibler avec la stratégie ou à exclure de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu'il utilise doit être conforme à cette stratégie pour qu'il puisse accéder aux ressources.  

 Vous pouvez spécifier deux types de groupes à utiliser pour la stratégie de Skype Entreprise :  

-   Les **Groupes ciblés** contiennent les utilisateurs auxquels s’applique la stratégie  

-   Les **Groupes exemptés** contiennent les utilisateurs à exclure de la stratégie  
    Si un utilisateur figure dans les deux groupes, il est exempté.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Étape 2 : configurer et déployer une stratégie de conformité  
 Créez et déployez une stratégie de conformité sur tous les appareils sur lesquels la stratégie Skype Entreprise Online est ciblée.  

 Pour plus d’informations sur la configuration de la stratégie de conformité, consultez [Gérer les stratégies de conformité d’appareils](../../protect/deploy-use/device-compliance-policies.md).  

> [!NOTE]  
>  Si vous n’avez pas déployé de stratégie de conformité, et que vous activez la stratégie Skype Entreprise Online, tous les appareils ciblés sont autorisés à accéder s’ils sont inscrits auprès de Microsoft Intune.  


### <a name="step-3-configure-the-skype-for-business-online-policy"></a>Étape 3 : configurer la stratégie Skype Entreprise Online  
 Configurez la stratégie de manière à restreindre l’accès à Skype Entreprise Online aux seuls appareils gérés et conformes. Cette stratégie est stockée dans Azure Active Directory.  

1.  Dans la [Console d’administration Microsoft Intune](https://manage.microsoft.com), cliquez sur **Stratégie** > **Accès conditionnel** > **Stratégie Skype Entreprise Online**.  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  Sélectionnez **Activer la stratégie d’accès conditionnel**.  

3.  Sous **Accès à l’application**, vous pouvez choisir d’appliquer la stratégie d’accès conditionnel à :  

    -   iOS  

    -   Android  

4.  Sous **Groupes ciblés**, cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory auxquels la stratégie s’applique. Vous avez la possibilité de cibler cette stratégie sur tous les utilisateurs ou uniquement sur un groupe sélectionné d’utilisateurs.  

5.  Sous **Groupes exemptés**, vous pouvez éventuellement cliquez sur **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory exempts de cette stratégie.  

6.  Une fois terminé, cliquez sur **Enregistrer**.  

 Vous avez maintenant configuré l’accès conditionnel pour Skype Entreprise Online. La stratégie d'accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>analyser la conformité et les stratégies d'accès conditionnel  
 Dans l’espace de travail Groupes, vous pouvez afficher l’état de l’accès conditionnel de vos appareils.  

 Sélectionnez un groupe d’appareils mobiles quelconque puis, sous l’onglet **Appareils** , sélectionnez l’un des **Filtres**suivants :  

-   L’accès à Skype Entreprise Online est bloqué pour les **appareils non enregistrés avec AAD**

-   L’accès à Skype Entreprise Online est bloqué pour les **appareils non compatibles**  

-   Les **appareils inscrits auprès d’AAD et conformes** peuvent accéder à Skype Entreprise Online  

### <a name="see-also"></a>Voir aussi  

 [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)
