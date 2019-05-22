---
title: Planifier pour le centre logiciel
titleSuffix: Configuration Manager
description: Choisissez comment vous souhaitez configurer et personnaliser le Centre logiciel pour permettre aux utilisateurs d’interagir avec Configuration Manager.
ms.date: 05/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c6826794-aa19-469d-ae47-1a0db68a1ff1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 50683b43cff113f7cd77efb5d8798fd24b53f90a
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106518"
---
# <a name="plan-for-software-center"></a>Planifier pour le centre logiciel

*S’applique à : System Center Configuration Manager (Current Branch)*

Les utilisateurs modifient les paramètres, recherchent et installent des applications à partir du Centre logiciel. Lorsque vous installez le client Configuration Manager sur un appareil Windows, il installe automatiquement le Centre logiciel également. Le nouveau Centre logiciel a été modernisé. Les applications qui seraient apparues uniquement dans le catalogue des applications dépendant de Silverlight (applications accessibles à l’utilisateur) apparaissent maintenant dans le Centre logiciel sous l’onglet **Applications**.

Pour plus d’informations sur les autres fonctionnalités du Centre logiciel, consultez [Guide de l’utilisateur du Centre logiciel](/sccm/core/understand/software-center).  


## <a name="bkmk_userex"></a> Configurer le Centre logiciel  

Passez en revue les améliorations suivantes apportées au Centre logiciel :

### <a name="starting-in-version-1802"></a>À compter de la version 1802

- Le paramètre client **Utiliser le nouveau Centre logiciel** dans le groupe **Agent ordinateur** est activé par défaut. L’ancienne version du Centre logiciel n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

- Les utilisateurs peuvent rechercher et installer les applications disponibles sur les appareils joints à Azure Active Directory (Azure AD). Pour plus d’informations, consultez [Déployer des applications disponibles pour l’utilisateur sur des appareils joints à Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

### <a name="starting-in-version-1806"></a>À compter de la version 1806

- Indiquez la visibilité du lien du site web du catalogue d’applications dans l’onglet **État de l’installation** du Centre logiciel. Pour plus d’informations, consultez les paramètres clients du [Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center).  

- Les rôles du catalogue d’applications ne sont plus nécessaires pour afficher les applications accessibles aux utilisateurs dans le Centre logiciel. Cette modification permet d’alléger l’infrastructure de serveur nécessaire pour fournir des applications aux utilisateurs. Le Centre logiciel s’appuie désormais sur le point de gestion pour obtenir ces informations, ce qui permet une meilleure mise à l’échelle des grands environnements par l’attribution de [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).<!--1358309-->  

    > [!Note]  
    > Si vous utilisez actuellement le catalogue d’applications et mettez à jour vers Configuration Manager version 1806, le catalogue d’applications continue à fonctionner. Les rôles de point du site Web et de point de service Web du catalogue des applications ne sont plus *requis*, mais ils sont toujours *pris en charge*. **L’expérience utilisateur Silverlight** pour le *point du site Web* du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
    >
    > Commencez à planifier la suppression des rôles du catalogue d’applications dans votre infrastructure. Profitez des améliorations apportées au Centre logiciel pour utiliser le point de gestion et simplifier votre environnement Configuration Manager.  

Utilisez le tableau suivant pour comprendre la configuration requise pour le Centre logiciel en fonction de la version spécifique de Configuration Manager :

| Type d'appareil | Version du site | Infrastructure |
|-----------------|--------------|----------------|
| Appareil joint à Azure AD<br>(ou « joint à un domaine cloud ») | 1802 ou 1806 | Point de gestion pour tous les déploiements d’applications |
| Appareil [joint à une version hybride d'Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) sur Internet | 1802 ou 1806 | Passerelle de gestion cloud et point de gestion pour tous les déploiements d’applications |
| Appareil joint au domaine Active Directory local | 1802 | Catalogue d’applications requis pour les applications accessibles à l’utilisateur via le Centre logiciel |
| Appareil joint au domaine Active Directory local | 1806 | Point de gestion pour tous les déploiements d’applications |

> [!Important]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités apparaissent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version des clients n’est pas également la plus récente.


## <a name="bkmk_impact"></a> Remplacer les notifications toast par une fenêtre de dialogue

<!--3555947-->
Parfois, les utilisateurs ne voient pas la notification toast Windows relative à un redémarrage ou à un déploiement obligatoire. Ils ne voient pas non plus l’expérience qui permet de répéter le rappel. Ce comportement peut entraîner une mauvaise expérience utilisateur quand le client atteint une échéance.

À compter de la version 1902, quand [des changements logiciels sont nécessaires](#software-changes-are-required) ou que des déploiements [exigent un redémarrage](#restart-required), vous pouvez utiliser une fenêtre de dialogue plus intrusive.

### <a name="software-changes-are-required"></a>Des changements logiciels sont nécessaires

Lorsque vous [déployez une application](/sccm/apps/deploy-use/deploy-applications) comme prévu avec une échéance fixe, sélectionnez les options de notification à l’utilisateur suivantes sur la page **Expérience utilisateur** de l’Assistant Déploiement de logiciel :

- **Afficher dans le Centre logiciel et afficher toutes les notifications**
- **Quand des changements logiciels sont nécessaires, présenter une fenêtre de dialogue à l’utilisateur au lieu d’une notification toast**

La configuration de ce paramètre de déploiement change l’expérience utilisateur pour ce scénario.

Remplacement de la notification toast suivante :

![Notification toast indiquant que des changements logiciels sont nécessaires](media/3555947-required-toast.png)  

Par la fenêtre de dialogue suivante :

![Fenêtre de dialogue concernant les changements logiciels nécessaires](media/3555947-required-dialog.png)


### <a name="restart-required"></a>Redémarrage nécessaire

Dans le groupe de paramètres client [Redémarrage de l’ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-restart), activez l’option suivante : **Lorsqu’un déploiement exige un redémarrage, présenter une fenêtre de dialogue à l’utilisateur au lieu d’une notification toast**.  

Ce paramètre client modifie l’expérience utilisateur pour tous les déploiements nécessaires qui exigent un redémarrage des types suivants :

- [Application](/sccm/apps/deploy-use/deploy-applications)
- [Séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS)
- [Mise à jour logicielle](/sccm/sum/deploy-use/deploy-software-updates)

Remplacement de la notification toast suivante :

![Notification toast indiquant qu’un redémarrage est nécessaire](media/3555947-restart-toast.png)  

Par la fenêtre de dialogue suivante :

![Fenêtre de dialogue indiquant de redémarrer votre ordinateur](media/3555947-restart-dialog.png)


## <a name="branding-software-center"></a>Personnalisation du Centre logiciel

Modifiez l’apparence du Centre logiciel pour répondre aux exigences de la marque de votre organisation. Cette configuration permet aux utilisateurs de faire confiance au Centre logiciel.

Configuration Manager applique la personnalisation au Centre logiciel selon les priorités suivantes :  

- Si vous n’avez pas installé le catalogue d’applications (recommandé) :  

    1. Paramètres client du **Centre logiciel**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Paramètre client **Nom de l’organisation** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- Si vous avez installé le catalogue d’applications :  

    1. Paramètres client du **Centre logiciel**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#software-center).  

    2. Si vous connectez un abonnement Microsoft Intune à Configuration Manager, le Centre logiciel affiche le *nom d’organisation*, la *couleur* et le *logo de l’entreprise* spécifiés dans les propriétés de l’abonnement Intune. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

    3. Le *nom d’organisation* et la *couleur* que vous spécifiez dans les propriétés du point du site Web du catalogue des applications. Pour plus d’informations, consultez [Options de configuration pour le point du site web du catalogue des applications](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).  

    4. Paramètre client **Nom de l’organisation** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

### <a name="configure-software-center-branding"></a>Configurer la personnalisation du Centre logiciel

<!-- 1351224 -->
Personnalisez l’apparence du Centre logiciel en ajoutant les éléments de marque de votre entreprise et en spécifiant la visibilité des onglets.

Pour plus d’informations, consultez les articles suivants :

- Groupe de paramètres client du [Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center)  
- [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings)  


## <a name="see-also"></a>Voir aussi

- [Guide de l’utilisateur sur le Centre logiciel](/sccm/core/understand/software-center)
- [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management)
