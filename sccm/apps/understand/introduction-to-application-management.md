---
title: Présentation de la gestion d’applications
titleSuffix: Configuration Manager
description: Découvrez les informations de base dont vous aurez besoin pour gérer et déployer des applications Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70ab4136f39b4bf559c3d460ca1528bb4de0f6e1
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384288"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Présentation de la gestion d’applications dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans cet article, vous allez découvrir les principes de base à connaître avant de commencer à utiliser des applications Configuration Manager.  

> [!TIP]  
>  Si vous êtes déjà familiarisé avec la gestion d’applications dans Configuration Manager, ignorez cet article. Passez à la création d’un exemple d’application : [Créer et déployer une application](/sccm/apps/get-started/create-and-deploy-an-application).  



## <a name="what-is-an-application"></a>Qu’est-ce qu’une application ?  

Bien que le terme *application* soit couramment utilisé en informatique, il a une signification spécifique dans Configuration Manager. Comparez plutôt une application à une boîte. Cette boîte contient un ou plusieurs ensembles de fichiers d’installation pour un package logiciel (appelé *type de déploiement*), ainsi que des instructions sur la façon de déployer le logiciel.  

Quand vous déployez l’application sur des appareils, des **spécifications** déterminent le type de déploiement que Configuration Manager installe sur l’appareil.  

Vous pouvez effectuer bien d’autres choses avec une application. Vous en apprendrez plus sur ces choses en parcourant ce guide. Les sections suivantes présentent les concepts que vous devez connaître avant d’aller plus loin :  

#### <a name="deployment-type"></a>Type de déploiement
Si *l’application* est la boîte, le *type de déploiement* est tout ce que contient la boîte. Une application a besoin d’au moins un type de déploiement, car il détermine la façon d’installer l’application. Utilisez plusieurs types de déploiement pour configurer un contenu et un programme d’installation différents pour la même application. 

Par exemple, votre entreprise a une application métier appelée Astoria. Les développeurs de l’application fournissent les moyens suivants pour l’installer :
- Package Windows Installer pour bénéficier de toutes les fonctionnalités sur les appareils Windows 10
- Un package App-V pour une utilisation dans la batterie de serveurs
- Un package d’application Android pour les utilisateurs mobiles  

Vous créez une application unique pour Astoria dans Configuration Manager. L’application définit les métadonnées générales relatives à l’application qui sont communes à toutes les plateformes et méthodes d’installation. Ensuite, vous créez trois types de déploiement pour les méthodes d’installation disponibles et déployez l’application pour tous les utilisateurs. Selon les spécifications et autres configurations liées aux types de déploiement, Configuration Manager détermine la méthode appropriée dans chaque cas d’usage. 

Pour plus d’informations, consultez [Créer des types de déploiement pour l’application](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).

#### <a name="requirements"></a>spécifications
Dans les versions précédentes de Configuration Manager, vous créeriez un regroupement d’appareils sur lesquels déployer une application. Même si vous pouvez toujours créer un regroupement, utilisez des *spécifications* pour définir des critères plus détaillés pour un déploiement d’application.

Par exemple, précisez qu’une application peut uniquement être installée sur des appareils Windows 10. Quand vous déployez l’application sur tous vos appareils, elle n’est installée que sur les appareils Windows 10.

Configuration Manager évalue les spécifications pour déterminer s’il doit installer une application et ses types de déploiement. Ensuite, il détermine le type de déploiement correct selon lequel installer une application. Tous les sept jours par défaut, le client Configuration Manager réévalue les règles de spécification pour déterminer la conformité selon le paramètre client **Planifier la réévaluation des déploiements**.

Pour plus d’informations, consultez [Créer et déployer une application](/sccm/apps/get-started/create-and-deploy-an-application) et [Spécifications pour le type de déploiement](/sccm/apps/deploy-use/create-applications#bkmk_dt-require).

#### <a name="global-conditions"></a>Conditions globales
Tandis que vous utilisez les spécifications avec un type de déploiement spécifique dans une seule application, vous pouvez également créer des *conditions globales*. Les conditions constituent une bibliothèque de spécifications prédéfinies que vous pouvez utiliser avec n’importe quel type d’application et de déploiement. Configuration Manager inclut un ensemble de conditions globales intégrées, ou vous pouvez créer vos propres conditions globales. 

Pour plus d’informations, consultez [Créer des conditions globales](/sccm/apps/deploy-use/create-global-conditions).

#### <a name="simulated-deployment"></a>Déploiement simulé
Un *déploiement simulé* évalue les spécifications, la méthode de détection et les dépendances d’une application. Un client signale les résultats sans installer l’application. 

Pour plus d’informations, consultez [Simuler des déploiements d’applications](/sccm/apps/deploy-use/simulate-application-deployments).  

#### <a name="deployment-action"></a>Action de déploiement
Une *action de déploiement* spécifie si vous souhaitez installer ou désinstaller l’application que vous déployez. Tous les types de déploiement ne prennent pas en charge l’action de désinstallation. 

Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).  

#### <a name="deployment-purpose"></a>Objet du déploiement
*L’objet du déploiement* spécifie si l’application de déploiement est **Obligatoire** ou **Disponible** :  

- Le client installe automatiquement un déploiement *obligatoire* conformément à la planification que vous définissez. Si l’application n’est pas masquée, un utilisateur peut suivre l’état de son déploiement. Il peut également utiliser le Centre logiciel pour installer l’application avant l’échéance.  

- Si vous déployez l’application pour un utilisateur en tant qu’application *disponible*, il la voit dans le Centre logiciel et peut la demander quand bon lui semble.  

Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).  

#### <a name="revisions"></a>Révisions
Quand vous apportez des *modifications* à une application ou à un type de déploiement, Configuration Manager crée une version de l’application. Dans la console Configuration Manager, effectuez les actions suivantes : 
- Afficher l’historique des révisions de chaque application
- Afficher ses propriétés
- Restaurer une version précédente d’une application
- Supprimer une ancienne version

Pour plus d’informations, consultez [Mettre à jour et mettre hors service des applications](/sccm/apps/deploy-use/update-and-retire-applications).  

#### <a name="detection-method"></a>Méthode de détection
Utilisez les *méthodes de détection* pour déterminer si une application est déjà installée sur un appareil. Si la méthode de détection indique que l’application est installée, Configuration Manager n’essaie pas de la réinstaller.

Pour plus d’informations, consultez [Options de la méthode de détection du type de déploiement](/sccm/apps/deploy-use/create-applications##bkmk_dt-detect).

#### <a name="dependencies"></a>Dépendances
Les *dépendances* définissent un ou plusieurs types de déploiement d’une autre application que le client doit installer avant d’installer ce type de déploiement. 

Pour plus d’informations, consultez [Dépendances pour le type de déploiement](/sccm/apps/deploy-use/create-applications#bkmk_dt-depend).  

#### <a name="supersedence"></a>Remplacement
Configuration Manager vous permet de mettre à niveau ou de remplacer des applications existantes en utilisant une relation de *remplacement*. Quand vous remplacez une application, vous spécifiez un nouveau type de déploiement pour remplacer le type de déploiement de l’application remplacée. Vous pouvez aussi décider s’il faut mettre à niveau ou désinstaller l’application remplacée avant que le client n’installe l’application de remplacement.

Pour plus d’informations, consultez [Remplacement d’applications](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence).  

#### <a name="user-centric-management"></a>Gestion centrée sur l'utilisateur
Les applications Configuration Manager prennent en charge la *gestion centrée sur l’utilisateur*, ce qui vous permet d’associer des utilisateurs spécifiques à des appareils spécifiques. Au lieu de mémoriser le nom de l’appareil d’un utilisateur, vous déployez des applications sur l’utilisateur et l’appareil. Cette fonctionnalité vous permet de veiller à ce que les applications les plus importantes soient toujours disponibles sur chacun des appareils de l’utilisateur. Si un utilisateur acquiert un nouvel ordinateur, Configuration Manager installe automatiquement ses applications sur l’appareil avant qu’il ne se connecte. 

Pour plus d’informations, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## <a name="what-application-types-can-you-deploy"></a>Quels types d’applications pouvez-vous déployer ?  

Configuration Manager vous permet de déployer les types d’application suivants :  

- Windows Installer (msi)  

- Package d’application Windows (appx ou appxbundle)  

    > [!Note]  
    > Depuis la version 1806, ce type inclut les nouveaux formats de package d’application (msix) et d’ensemble d’applications (msixbundle) Windows 10.<!--1357427-->  

- Package d’application Windows dans le Microsoft Store  

- Microsoft App-V v4 et v5  

- macOS  


De plus, quand vous gérez des appareils par le biais de la gestion des appareils locaux Microsoft Intune ou Configuration Manager, gérez ces types d’application supplémentaires :  

- Package d’application Windows Phone (xap)  

- Package d’application Windows Phone dans le Microsoft Store  

- Package d’application pour iOS (ipa)  

- Package d'application pour iOS depuis App Store  

- Package d’application pour Android (apk)  

- Package d'application pour Android sur Google Play  

- Windows Installer via MDM (msi)  

- Application web



## <a name="state-based-applications"></a>Applications basées sur l’état  

Les applications Configuration Manager utilisent la surveillance basée sur l’état. Vous pouvez effectuer le suivi du dernier état du déploiement des applications pour des utilisateurs et des appareils. Les messages d'état affichent des informations concernant des appareils individuels. Par exemple, si vous déployez une application sur un regroupement d’utilisateurs, vous pouvez voir l’état de conformité du déploiement ainsi que son objet dans la console Configuration Manager. Surveillez le déploiement de tous vos logiciels à partir de l’espace de travail **Surveillance** dans la console Configuration Manager. Pour plus d’informations, consultez [Surveiller des applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

Le client Configuration Manager réévalue régulièrement les déploiements d’applications. Par exemple :  

- Un utilisateur désinstalle une application déployée. Au cycle d’évaluation suivant, Configuration Manager détecte que l’application n’est pas présente. Le client réinstalle alors l’application automatiquement.  

- Configuration Manager n’a pas installé une application sur un appareil, car elle n’a pas satisfait aux spécifications. Plus tard, une modification est apportée à l'appareil pour qu'il soit conforme à la configuration requise. Configuration Manager détecte cette modification, puis le client installe l’application.  

Vous pouvez définir l’intervalle de réévaluation pour les déploiements d’applications. Utilisez le paramètre client **Planifier la réévaluation des déploiements** dans le groupe **Déploiement logiciel**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#software-deployment).  



## <a name="get-started-creating-an-application"></a>Prendre en main la création d’une application  

Si vous souhaitez vous lancer et créer une application, consultez la procédure pas à pas de l’article [Créer et déployer une application](/sccm/apps/get-started/create-and-deploy-an-application).  

Si vous connaissez déjà les principes de base et que vous recherchez des informations de référence plus approfondies sur toutes les options disponibles, commencez par la rubrique [Créer des applications](/sccm/apps/deploy-use/create-applications).  



## <a name="software-center"></a>Centre logiciel  

Le Centre logiciel est une application Windows installée avec le client Configuration Manager. Utilisez-le pour effectuer les actions suivantes :  
- Rechercher et demander des applications déployées sur l’appareil ou pour l’utilisateur
- Planifier les installations de logiciels et installer ces derniers
- Afficher l’état de l’installation des applications, des mises à jour logicielles et des systèmes d’exploitation
- Configurer les paramètres du contrôle à distance
- Configurer la gestion de l’alimentation

Pour plus d’informations, consultez les articles suivants :  
- [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Guide de l’utilisateur sur le Centre logiciel](/sccm/core/understand/software-center)

> [!Note]  
> Le rôle de point de service web du catalogue des applications n’est plus nécessaire dans la version 1806, mais demeure pris en charge. 
> 
> Le rôle de site web du catalogue des applications n’est pas pris en charge dans la version 1806. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## <a name="packages-and-programs"></a>Packages et programmes  

Configuration Manager continue de prendre en charge les packages et les programmes utilisés dans les versions précédentes du produit. 

Pour plus d’informations, consultez [Packages et programmes](/sccm/apps/deploy-use/packages-and-programs).  



## <a name="next-steps"></a>Étapes suivantes

Les concepts de base de la gestion des applications dans Configuration Manager n’ayant plus de secret pour vous, consultez les articles suivants :
- [Créer et déployer un exemple d’application](/sccm/apps/get-started/create-and-deploy-an-application)
- [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Créer des applications](/sccm/apps/deploy-use/create-applications)
