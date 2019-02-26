---
title: Cogestion pour les appareils Windows 10
titleSuffix: Configuration Manager
description: Découvrez comment gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: c88bf98e035499c271de8acf9d8fa222e5058447
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754916"
---
# <a name="what-is-co-management"></a>Qu’est-ce que la cogestion ?

<!-- 1350871 --> La cogestion est un des principaux moyens pour attacher votre déploiement de Configuration Manager existant vers le cloud de Microsoft 365. Elle vous permet de déverrouiller des fonctionnalités supplémentaires sur le cloud tels que l’accès conditionnel. 

La cogestion vous permet de gérer simultanément plusieurs appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune. Il vous permet d’attacher votre investissement existant dans Configuration Manager-cloud en ajoutant de nouvelles fonctionnalités. À l’aide de cogestion, vous avez la possibilité d’utiliser la solution de technologie qui convient le mieux à votre organisation. 

Quand un appareil Windows 10 a le client Configuration Manager et est inscrit à Intune, vous bénéficiez des avantages des deux services. Vous contrôlez les charges de travail, le cas échéant, que vous basculez de l’autorité de Configuration Manager à Intune. Configuration Manager continue de gérer toutes les autres charges de travail, y compris les charges de travail que vous ne basculez vers Intune, et toutes les autres fonctionnalités de Configuration Manager que cogestion ne prend pas en charge.

Vous êtes également en mesure de piloter une charge de travail avec un ensemble distinct d’appareils. Pilotage vous permet de tester la fonctionnalité de Intune avec un sous-ensemble d’appareils avant de basculer un groupe plus important. 

![Diagramme de vue d’ensemble de la cogestion](media/co-management-overview.png)



## <a name="paths-to-co-management"></a>Chemins vers la cogestion

Il existe deux principaux parcours pour accéder à la cogestion :  

- **Les clients Configuration Manager existants**: Vous avez des appareils Windows 10 qui sont déjà des clients Configuration Manager. Vous configurez Azure AD hybride et les inscrivez dans Intune.  

- **Nouveaux périphériques basés sur internet**: Vous avez de nouveaux appareils Windows 10 qui rejoindre Azure AD et l’inscrire automatiquement à Intune. Vous installez le client Configuration Manager pour atteindre un état de cogestion.  

Pour plus d’informations sur les chemins d’accès, consultez [chemins d’accès à la cogestion](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Avantages 

Quand vous inscrivez les clients Configuration Manager existants dans la cogestion, vous bénéficiez de la valeur immédiate suivante :  

- Accès conditionnel avec la conformité des appareils  

- Actions à distance basée sur Intune, par exemple : redémarrage, contrôle à distance ou les paramètres d’usine

- Visibilité centralisée de l’intégrité de l’appareil  

- Lier des utilisateurs, appareils et applications avec Azure Active Directory (Azure AD)  

- Modernes d’approvisionnement avec Windows Autopilot  

- Actions à distance

Pour plus d’informations sur cette valeur immédiate à partir de la cogestion, consultez la série de guides de démarrage rapide pour [Cloud connect avec la cogestion](/sccm/comanage/quickstarts).

La cogestion vous permet également d’orchestrer avec Intune pour plusieurs charges de travail. Pour plus d’informations, consultez le [charges de travail](#workloads) section. 



## <a name="prerequisites"></a>Prérequis

Cogestion présente ces conditions préalables dans les domaines suivants :

- [Gestion des licences](#licensing)  
- [Configuration Manager](#configuration-manager)  
- [Azure Active Directory](#azure-ad) (Azure AD)  
- [Microsoft Intune](#intune)  
- [Windows 10](#windows-10)  
- [Rôles et autorisations](#permissions-and-roles)  

### <a name="licensing"></a>Licences

- Azure AD Premium 
- Licence EMS ou Intune pour tous les utilisateurs  

    > [!Note]  
    > Une à Enterprise Mobility + Security (EMS) abonnement inclut Azure Active Directory Premium et Microsoft Intune.

> [!Tip]  
> Vérifiez que vous affectez une licence Intune au compte que vous utilisez pour vous connecter à votre client. Sinon, Échec de la connexion avec le message d’erreur « L’utilisateur n’est ne pas reconnu ».  


### <a name="configuration-manager"></a>Configuration Manager

Cogestion nécessite Configuration Manager version 1710 ou ultérieure.

À compter de Configuration Manager version 1806, vous pouvez connecter plusieurs instances du Gestionnaire de Configuration à un seul locataire Intune. <!--1357944-->  

L’activation de cogestion lui-même ne nécessite pas que vous intégrez votre site auprès d’Azure AD. Pour le [deuxième scénario de chemin d’accès](#paths-to-co-management), basés sur internet des clients Configuration Manager requièrent le [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) (CMG). La passerelle CMG nécessite que le site est [intégrée à Azure AD pour la gestion cloud](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Les appareils Windows 10 doivent être joints à Azure AD. Ils peuvent être de l’un des types suivants :  

    - [Joint à Azure AD Hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), où l’appareil est joint à votre annuaire Active Directory local et inscrit dans Azure Active Directory.  

    - [Joint à Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) uniquement. (Ce type est parfois appelé « joint à un domaine cloud »)<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurer Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Activer l’inscription automatique Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Toutefois, vous pouvez commencer la migration d’utilisateurs vers Intune autonome, puis activer leurs appareils Windows 10 associés pour la cogestion. Pour plus d’informations sur la migration vers Intune autonome, consultez [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
> 
> Si vous utilisez une [autorité mixte](/sccm/mdm/deploy-use/migrate-mixed-authority), effectuez d’abord la migration vers Intune autonome. Ensuite, définissez l’autorité MDM sur Intune avant de configurer la cogestion.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Mettre à niveau vos appareils Windows 10, version 1709 ou ultérieure. Pour plus d’informations, consultez [adoption de Windows en tant que service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Les appareils mobiles Windows 10 ne prennent pas en charge la cogestion.


### <a name="permissions-and-roles"></a>Rôles et autorisations
<!--SCCMDocs issue #667-->

| Action | Rôle nécessaire |
|----|----|
| Configurer une passerelle de gestion cloud dans Configuration Manager | Azure **Gestionnaire d’abonnements** |
| Créer des applications Azure AD à partir de Configuration Manager | Azure AD **administrateur général** |
| Importer des applications Azure dans Configuration Manager | Configuration Manager **administrateur complet**<br>Aucun des rôles Azure supplémentaires nécessités |
| Activer la cogestion dans Configuration Manager | Un utilisateur Azure AD<br>Configuration Manager **administrateur complet** avec **tous les** droits d’étendue.<!--SCCMDoc issue 626--> | 

Pour plus d’informations sur les rôles Azure, consultez [Présentation des différents rôles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Pour plus d’informations sur les rôles de Configuration Manager, consultez [principes de base d’administration en fonction du rôle](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Charges de travail 

Vous n’êtes pas obligé de basculer les charges de travail, ou vous pouvez les faire individuellement lorsque vous êtes prêt. Configuration Manager continue de gérer toutes les autres charges de travail, y compris les charges de travail que vous ne basculez vers Intune, et toutes les autres fonctionnalités de Configuration Manager que cogestion ne prend pas en charge.

Cogestion prend en charge les charges de travail suivantes :

- Stratégies de conformité  

- Stratégies Windows Update  

- Stratégies d’accès aux ressources  

- Endpoint Protection  

- Configuration de l’appareil  

- Applications « Démarrer en un clic » Office  

- Applications clientes  

Pour plus d’informations, consultez [charges de travail](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Surveiller la cogestion

Le tableau de bord de cogestion vous permet d’examiner les ordinateurs qui sont cogérées dans votre environnement. Les graphes peuvent vous aider à identifier les appareils qui demandent une attention particulière.

![Capture d’écran du tableau de bord de cogestion](media/co-management-dashboard.png)

Pour plus d’informations, consultez [comment surveiller la cogestion](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur la valeur immédiate et la mise en route avec la cogestion](/sccm/comanage/quickstarts)  

- [Didacticiel : Activer la cogestion pour les clients Configuration Manager existants](/sccm/comanage/tutorial-co-manage-clients)  

