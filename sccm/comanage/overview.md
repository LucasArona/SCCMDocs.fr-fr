---
title: Cogestion pour les appareils Windows 10
titleSuffix: Configuration Manager
description: Découvrez comment gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/26/2019
ms.topic: overview
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e0ae5c392acd03509f70c19f551731065bc4be2
ms.sourcegitcommit: 23852dda81bb8496dd10c0a8ec4f740a8e15efc3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64873275"
---
# <a name="what-is-co-management"></a>Qu’est-ce que la cogestion ?

<!-- 1350871 -->
La cogestion est l’une des principales façons de joindre votre déploiement de Configuration Manager existant au cloud Microsoft 365. Elle vous permet de déverrouiller des fonctionnalités cloud supplémentaires telles que l’accès conditionnel.

La cogestion vous permet de gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune. Elle vous permet d’attacher via le cloud votre investissement existant dans Configuration Manager en ajoutant de nouvelles fonctionnalités. À l’aide de la cogestion, vous avez la possibilité d’utiliser la solution de technologie qui convient le mieux à votre organisation.

Quand un appareil Windows 10 dispose du client Configuration Manager et qu’il est inscrit à Intune, vous bénéficiez des avantages des deux services. Vous contrôlez les charges de travail, le cas échéant, pour lesquelles vous utilisez Intune à la place de Configuration Manager comme autorité. Configuration Manager continue de gérer toutes les autres charges de travail, notamment celles que vous ne basculez pas vers Intune, ainsi que toutes les autres fonctionnalités de Configuration Manager que la cogestion ne prend pas en charge.

Vous êtes également en mesure de piloter une charge de travail avec un ensemble distinct d’appareils. Le pilotage vous permet de tester la fonctionnalité Intune avec un sous-ensemble d’appareils avant de passer à un groupe plus important.

![Diagramme de présentation de la cogestion](media/co-management-overview.png)

> [!Note]  
> Quand vous gérez des appareils Windows 10 en parallèle avec Configuration Manager et Microsoft Intune, cette configuration est appelée *cogestion*. Quand vous gérez des appareils avec Configuration Manager et que vous vous inscrivez auprès d’un service MDM de tiers, cette configuration est appelée *coexistence*. Le fait d’avoir deux autorités de gestion pour un même appareil peut s’avérer délicat si la gestion n’est pas correctement orchestrée entre les deux. Avec la cogestion, Configuration Manager et Intune équilibrent les [charges de travail](#workloads) pour garantir qu’il n’y a pas de conflits. Cette interaction n’existe pas avec les services de tiers : il existe donc des limitations avec les fonctionnalités de gestion dans le cas de la coexistence. Pour plus d’informations, consultez [Coexistence d’un service MDM de tiers avec Configuration Manager](/sccm/comanage/coexistence).


## <a name="paths-to-co-management"></a>Chemins vers la cogestion

Il existe deux principaux parcours pour accéder à la cogestion :  

- **Clients Configuration Manager existants** : Vous avez des appareils Windows 10 qui sont déjà des clients Configuration Manager. Vous configurez Azure AD hybride et les inscrivez à Intune.  

- **Nouveaux appareils basés sur Internet** : Vous avez de nouveaux appareils Windows 10 qui sont joints à Azure AD et qui s’inscrivent automatiquement à Intune. Vous installez le client Configuration Manager pour atteindre un état de cogestion.  

Pour plus d’informations sur les chemins, consultez [Chemins vers la cogestion](/sccm/comanage/quickstart-paths).



## <a name="benefits"></a>Avantages

Quand vous inscrivez les clients Configuration Manager existants dans la cogestion, vous bénéficiez de la valeur immédiate suivante :  

- Accès conditionnel avec conformité de l’appareil  

- Actions à distance basées sur Intune, par exemple redémarrage, contrôle à distance ou réinitialisation aux paramètres d’usine

- Visibilité centralisée de l’intégrité de l’appareil  

- Lien des utilisateurs, appareils et applications avec Azure AD (Azure Active Directory)  

- Provisionnement moderne avec Windows Autopilot  

- Actions à distance

Pour plus d’informations sur cette valeur immédiate de la cogestion, consultez la série de démarrages rapides pour [Connexion au cloud à l’aide de la cogestion](/sccm/comanage/quickstarts).

La cogestion vous permet également d’orchestrer avec Intune pour plusieurs charges de travail. Pour plus d’informations, consultez la section [Charges de travail](#workloads).



## <a name="prerequisites"></a>Prérequis

La cogestion présente les prérequis ci-dessous dans les domaines suivants :

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
    > Un abonnement Enterprise Mobility + Security (EMS) comprend à la fois Azure Active Directory Premium et Microsoft Intune.

> [!Tip]  
> Vérifiez que le compte utilisé pour vous connecter à votre locataire dispose d’une licence Intune. Si ce n’est pas le cas, la connexion échoue avec le message d’erreur « Utilisateur non reconnu ».  


### <a name="configuration-manager"></a>Configuration Manager

La cogestion nécessite Configuration Manager version 1710 ou ultérieure.

À compter de Configuration Manager version 1806, vous pouvez connecter plusieurs instances Configuration Manager à un seul locataire Intune. <!--1357944-->  

L’activation de la cogestion elle-même ne nécessite pas l’intégration de votre site à Azure AD. Pour le [scénario du deuxième chemin](#paths-to-co-management), les clients Configuration Manager basés sur Internet nécessitent la [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). La passerelle de gestion cloud nécessite que le site soit [intégré à Azure AD pour la gestion cloud](/sccm/core/servers/deploy/configure/azure-services-wizard). 


### <a name="azure-ad"></a>Azure AD

- Les appareils Windows 10 doivent être joints à Azure AD. Ils peuvent être de l’un des types suivants :  

    - [Joint à Azure AD Hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), où l’appareil est joint à votre annuaire Active Directory local et inscrit dans Azure Active Directory.  

    - [Joint à Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan) uniquement. (Ce type est parfois désigné comme « joint à un domaine cloud »)<!--SCCMDocs issue 605-->  


### <a name="intune"></a>Intune

- [Configurer Intune](https://docs.microsoft.com/intune/setup-steps)  

- [Activer l’inscription automatique Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment)  

> [!Note]  
> Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Toutefois, vous pouvez commencer la migration d’utilisateurs vers Intune autonome, puis activer leurs appareils Windows 10 associés pour la cogestion. Pour plus d’informations sur la migration vers Intune autonome, consultez [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  
>
> Si vous utilisez une [autorité mixte](/sccm/mdm/deploy-use/migrate-mixed-authority), effectuez d’abord la migration vers Intune autonome. Ensuite, définissez l’autorité MDM sur Intune avant de configurer la cogestion.<!--SCCMDocs issue #797-->


### <a name="windows-10"></a>Windows 10

Mettez à niveau vos appareils vers Windows 10, version 1709 ou ultérieure. Pour plus d’informations, consultez [Adoption de Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).

> [!IMPORTANT]
> Les appareils mobiles Windows 10 ne prennent pas en charge la cogestion.


### <a name="permissions-and-roles"></a>Rôles et autorisations

<!--SCCMDocs issue #667-->
| Action | Rôle nécessaire |
|----|----|
| Configurer une passerelle de gestion cloud dans Configuration Manager | **Gestionnaire d’abonnements** Azure |
| Créer des applications Azure AD à partir de Configuration Manager | **Administrateur général** Azure AD |
| Importer des applications Azure dans Configuration Manager | **Administrateur complet** Configuration Manager<br>Aucun autre rôle Azure n’est nécessaire |
| Activer la cogestion dans Configuration Manager | Utilisateur Azure AD<br>**Administrateur complet** Configuration Manager avec des droits sur **toutes** les étendues.<!--SCCMDoc issue 626--> |

Pour plus d’informations sur les rôles Azure, consultez [Présentation des différents rôles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

Pour plus d’informations sur les rôles Configuration Manager, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).


## <a name="workloads"></a>Charges de travail

Vous n’êtes pas obligé de basculer les charges de travail, ou vous pouvez le faire individuellement quand vous êtes prêt. Configuration Manager continue de gérer toutes les autres charges de travail, notamment celles que vous ne basculez pas vers Intune, ainsi que toutes les autres fonctionnalités de Configuration Manager que la cogestion ne prend pas en charge.

La cogestion prend en charge les charges de travail suivantes :

- Stratégies de conformité  

- Stratégies Windows Update  

- Stratégies d’accès aux ressources  

- Endpoint Protection  

- Configuration de l’appareil  

- Applications « Démarrer en un clic » Office  

- Applications clientes  

Pour plus d’informations, consultez [Charges de travail](/sccm/comanage/workloads).



## <a name="monitor-co-management"></a>Surveiller la cogestion

Le tableau de bord de cogestion vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphes peuvent vous aider à identifier les appareils qui demandent une attention particulière.

![Capture d’écran du tableau de bord de cogestion](media/co-management-dashboard.png)

Pour plus d’informations, consultez [Guide pratique pour superviser la cogestion](/sccm/comanage/how-to-monitor).



## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur la valeur immédiate et la prise en main de la cogestion](/sccm/comanage/quickstarts)  

- [Tutoriel : Activer la cogestion pour les clients Configuration Manager existants](/sccm/comanage/tutorial-co-manage-clients)  
