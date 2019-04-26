---
title: Gérer l’accès à Dynamics CRM Online
titleSuffix: Configuration Manager
description: Découvrez comment contrôler l’accès à Microsoft Dynamics CRM Online à partir des appareils iOS et Android en utilisant l’accès conditionnel Microsoft Intune.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbd3d765a17d41bfbc2c400a3368cf00784b16c1
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62256094"
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>Gérer l’accès à Dynamics CRM Online dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez contrôler l’accès à Microsoft Dynamics CRM Online à partir des appareils iOS et Android en utilisant l’accès conditionnel Microsoft Intune.  L’accès conditionnel Intune repose sur deux éléments :
* La [stratégie de conformité des appareils](../../protect/deploy-use/device-compliance-policies.md) que l’appareil doit respecter pour être considéré comme conforme.
* La [stratégie d’accès conditionnel](../../protect/deploy-use/manage-access-to-services.md) dans laquelle vous spécifiez les conditions que l’appareil doit remplir pour accéder au service.

Pour en savoir plus sur le fonctionnement de l’accès conditionnel, consultez [Gérer l’accès aux services](../../protect/deploy-use/manage-access-to-services.md).


Quand un utilisateur ciblé tente d’utiliser l’application Dynamics CRM sur son appareil, voici l’évaluation qui se produit :

![Diagramme affichant les points de décision utilisés pour déterminer si l’accès à un service par un appareil est autorisé ou bloqué](media/mdm-ca-dynamics-crm-flow-diagram.png)

L’appareil devant accéder à Dynamics CRM Online doit :
* être un appareil **Android** ou **iOS** ;
* être **inscrit** auprès de Microsoft Intune ;
* être **conforme** à toutes les stratégies de conformité Microsoft Intune déployées.

L’état de l’appareil est stocké dans Azure Active Directory, qui accorde ou bloque l’accès aux fichiers en fonction des conditions que vous spécifiez.

Si une condition n'est pas remplie, l'utilisateur reçoit l'un des messages suivants quand il tente de se connecter :
* Si l’appareil n’est pas inscrit auprès de Microsoft Intune ou dans Azure Active Directory, l’utilisateur reçoit un message contenant des instructions pour installer l’application Portail d’entreprise et inscrire l’appareil.
* Si l’appareil n’est pas conforme, l’utilisateur reçoit un message le redirigeant vers le site web du portail d’entreprise Microsoft Intune ou l’application Portail d’entreprise, où il peut trouver des informations sur le problème et des solutions pour y remédier.

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Configurer l’accès conditionnel pour Dynamics CRM Online  
### <a name="step-1-configure-active-directory-security-groups"></a>Étape 1 : Configurer des groupes de sécurité Active Directory

Avant de commencer, configurez les groupes de sécurité Azure Active Directory pour la stratégie d'accès conditionnel. Vous pouvez configurer ces groupes dans le **centre d’administration Microsoft 365**. Ces groupes serviront à cibler des utilisateurs avec la stratégie ou à les exempter de la stratégie. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu'il utilise doit être conforme à cette stratégie pour qu'il puisse accéder aux ressources.

Vous pouvez spécifier deux types de groupes à utiliser pour la stratégie de Dynamics CRM :
* **Groupes ciblés** : groupes d’utilisateurs auxquels s’applique la stratégie.
* **Groupes exemptés** : groupes d’utilisateurs auxquels la stratégie ne s’applique pas.

Si un utilisateur se trouve dans les deux groupes, il est exempt de la stratégie.

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Étape 2 : Configurer et déployer une stratégie de conformité
[Créez et déployez](../../protect/deploy-use/device-compliance-policies.md) une stratégie de conformité pour tous les appareils auxquels appliquer la stratégie. Il s’agit de tous les appareils qui sont utilisés par les membres des groupes ciblés.

> [!NOTE]
> Les stratégies de conformité sont déployées dans des groupes Microsoft Intune, alors que les stratégies d’accès conditionnel ciblent des groupes de sécurité Azure Active Directory.

> [!IMPORTANT]
> Si vous n’avez pas déployé de stratégie de conformité, les appareils sont considérés comme conformes.

Quand vous êtes prêt, passez à l’Étape 3.
### <a name="step-3-configure-the-dynamics-crm-policy"></a>Étape 3 : Configurer la stratégie Dynamics CRM
Configurez maintenant la stratégie pour restreindre l’accès à Dynamics CRM aux appareils gérés et conformes. Cette stratégie sera stockée dans Azure Active Directory.

1. Dans la console d’administration Microsoft Intune, choisissez **Stratégie > Accès conditionnel > Stratégie Dynamics CRM Online**.

    ![Capture d’écran de la page de la stratégie d’accès conditionnel Dynamics CRM Online](media/mdm-ca-dynamics-crm-policy-configuration.png)

2. Sélectionnez **Activer la stratégie d’accès conditionnel**.
3. Sous **Accès à l’application**, vous pouvez choisir d’appliquer la stratégie d’accès conditionnel à :
   * **iOS**
   * **Android**
4. Sous **Groupes ciblés**, choisissez **Modifier** pour sélectionner les groupes de sécurité Active Directory auxquels la stratégie doit s’appliquer. Vous avez la possibilité de cibler cette stratégie sur tous les utilisateurs ou uniquement sur un groupe sélectionné d’utilisateurs.
5. Sous **Groupes exemptés**, choisissez **Modifier** pour sélectionner les groupes de sécurité Azure Active Directory à exempter de cette stratégie (facultatif).
6. Une fois que vous avez terminé, choisissez **Enregistrer**.

Vous avez configuré l’accès conditionnel pour Dynamics CRM. La stratégie d'accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>analyser la conformité et les stratégies d'accès conditionnel

Dans l’espace de travail **Groupes**, vous pouvez afficher l’état de l’accès conditionnel de vos appareils.

Sélectionnez un groupe d’appareils mobiles quelconque puis, sous l’onglet **Appareils** , sélectionnez l’un des **Filtres**suivants :
* **Appareils non enregistrés avec AAD** : l’accès à Dynamics CRM est bloqué pour ces appareils.
* **Appareils non conformes** : l’accès à Dynamics CRM est bloqué pour ces appareils.
* **Appareils enregistrés avec AAD et conformes** : ces appareils sont autorisés à accéder à Dynamics CRM.

###  <a name="see-also"></a>Voir aussi
[Gérer l’accès à la messagerie](../../protect/deploy-use/manage-email-access.md)

[Gérer l’accès à SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Gérer l’accès à Skype Entreprise Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)
