---
title: Cogestion pour les appareils Windows 10
titleSuffix: Configuration Manager
description: Découvrez comment gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 1791217e22e2bcc6d5fd2603abee3aaced816afe
ms.sourcegitcommit: 1f8731ed8f0308cb2cb576722adb0821a366e9ce
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223736"
---
# <a name="co-management-for-windows-10-devices"></a>Cogestion pour les appareils Windows 10    

Dans les mises à jour précédentes de Windows 10, vous pouviez déjà joindre un appareil Windows 10 à Active Directory (AD) en local et à Azure AD sur le cloud (Azure AD hybride). À compter de Configuration Manager version 1710, la cogestion tire parti de cette amélioration. Elle vous permet de gérer simultanément des appareils Windows 10 version 1709 à l’aide de Configuration Manager et d’Intune. <!-- 1350871 -->


## <a name="why-co-management"></a>Pourquoi la cogestion ?

Nombreux sont les clients qui souhaitent gérer les appareils Windows 10 comme les appareils mobiles, en recourant à une solution cloud plus simple et moins chère. Toutefois, le passage de la gestion classique à la gestion moderne peut s’avérer difficile.  


## <a name="what-is-co-management"></a>Qu’est-ce que la cogestion ?

La cogestion vous permet de gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et d’Intune. C’est une solution qui établit une passerelle entre la gestion classique et la gestion moderne tout en vous donnant la possibilité d’opérer cette transition selon une approche en plusieurs phases.


## <a name="benefits"></a>Avantages 

Utilisation immédiate des fonctionnalités Intune suivantes :  
 
- Actions à distance
    - [Réinitialisation aux paramètres d’usine](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
    - [Réinitialisation sélective](https://docs.microsoft.com/intune/apps-selective-wipe)
    - [Suppression d’appareils](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
    - [Redémarrage d’un appareil](https://docs.microsoft.com/intune/device-restart)
    - [Nouvelle version](https://docs.microsoft.com/intune/device-fresh-start)  

- Orchestration avec Intune pour les charges de travail suivantes :
    - [Stratégies de conformité](https://docs.microsoft.com/intune/device-compliance-get-started)
    - [Stratégies d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles)
    - [Stratégies Windows Update](https://docs.microsoft.com/intune/windows-update-for-business-configure)
    - [Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10), à compter de Configuration Manager 1802 <!-- 1357365 -->
    - [Configuration de l’appareil](https://docs.microsoft.com/intune/device-profile-create), à compter de Configuration Manager version 1806 <!-- 1357903 -->
    - [Applications « Démarrer en un clic » Office](https://docs.microsoft.com/intune/apps-add-office365), à compter de Configuration Manager 1806 <!--1357841-->
    - [Applications mobiles](https://docs.microsoft.com/intune/app-management), à compter de Configuration Manager 1806 comme fonctionnalité en préversion <!--1357892-->



## <a name="how-to-configure-co-management"></a>Comment configurer la cogestion

 Il existe deux principaux parcours pour accéder à la cogestion :  

   - Configuration Manager provisionne la cogestion : vous inscrivez dans Intune vos appareils Windows 10 joints à Azure AD qui sont déjà des clients Configuration Manager.  

   - Provisionnés par Intune : pour les appareils qui sont déjà inscrits dans Intune, vous installez le client Configuration Manager pour atteindre l’état de cogestion. 


### <a name="configuration-manager"></a>Configuration Manager

 -  Effectuez une mise à niveau vers Configuration Manager version 1710 ou ultérieure.


### <a name="azure-active-directory"></a>Azure Active Directory

 - Les appareils Windows 10 doivent être joints à Azure AD. Ils peuvent être de l’un des types suivants :  

     - [Joint à Azure AD Hybride](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup), où l’appareil est joint à votre annuaire Active Directory local et inscrit dans Azure Active Directory.

     - Joint à Azure AD uniquement. (Ce type est parfois appelé « joint à un domaine cloud »)<!--SCCMDocs issue 605-->

 - [Activez l’inscription automatique Windows 10](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="intune"></a>Intune

 - [Comment configurer un abonnement Intune](/sccm/mdm/deploy-use/configure-intune-subscription) ou [Configurer Intune](/intune/setup-steps)  

 - [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

 > [!Note]  
 > Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Toutefois, vous pouvez commencer la migration d’utilisateurs vers Intune autonome, puis activer leurs appareils Windows 10 associés pour la cogestion. Pour plus d’informations sur la migration vers Intune autonome, consultez [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Activer la cogestion 

 > [!Important]  
 > À compter de la version 1802, pour activer la cogestion, votre compte d’utilisateur administratif dans Configuration Manager doit être un **Administrateur complet** avec **Toutes** les étendues de sécurité. Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).<!--SCCMDoc issue 626-->  

 Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**. Cliquez sur **Configurer la cogestion** dans le ruban pour ouvrir l’**Assistant Intégration de la cogestion**. 
   
1. Dans la page **Abonnement**, cliquez sur **Se connecter**. Connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**.  

    > [!Tip]   
    > Vérifiez que le compte utilisé pour vous connecter à votre locataire dispose d’une licence Intune. Si ce n’est pas le cas, la connexion échoue avec le message d’erreur « Utilisateur non reconnu ».  

2. Dans la page **Activation**, choisissez votre paramètre **Inscription automatique dans Intune**. Copiez la ligne de commande pour les appareils déjà inscrits dans Intune, si nécessaire.  

    > [!Note]  
    > À compter de la version 1806, l’inscription automatique n’est pas immédiate pour tous les clients. Ce comportement permet une mise à l’échelle de l’inscription plus adaptée pour les environnements de grande taille. Configuration Manager rend aléatoire l’inscription en fonction du nombre de clients. Par exemple, si votre environnement comporte 100 000 clients, quand vous activez ce paramètre, l’inscription se produit sur plusieurs jours.<!--1358003-->  

3. Dans la page **Charges de travail**, de chaque charge de travail, choisissez le groupe d’appareils concerné par la gestion avec Intune.  

4. Dans la page **Mise en lots**, sélectionnez un regroupement d’appareils comme **Regroupement pilote**. Vérifiez les informations de **résumé** et terminez l’Assistant.  


### <a name="upgrade-windows-10-client"></a>Mettre à niveau le client Windows 10

- Effectuez une mise à niveau vers [Windows 10, version 1709 (également appelée Fall Creators Update) et ultérieure](/sccm/osd/deploy-use/manage-windows-as-a-service).


### <a name="configure-workloads-to-switch-to-intune"></a>Configurer les charges de travail pour basculer vers Intune 

L’article intitulé [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) vous explique comment basculer des charges de travail Configuration Manager spécifiques vers Intune. Cet article comprend également des instructions sur la modification des groupes d’appareils pour lesquels des charges de travail sont transférées.

#### <a name="compliance-policies"></a>Stratégies de conformité 
Les stratégies de conformité définissent les règles et les paramètres auxquels doit se conformer un appareil pour être considéré conforme par les stratégies d’accès conditionnel. Utilisez également des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l’accès conditionnel. Pour plus d’informations, consultez [Stratégies de conformité des appareils](https://docs.microsoft.com/intune/device-compliance-get-started).  

#### <a name="windows-update-policies"></a>Stratégies Windows Update
Les stratégies Windows Update pour Entreprise vous permettent de configurer des stratégies de report pour les mises à jour de fonctionnalités Windows 10 ou les mises à jour qualité pour les appareils Windows 10 gérés directement par Windows Update pour Entreprise. Pour plus d’informations, consultez [Configurer les stratégies de report Windows Update pour Entreprise](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

#### <a name="resource-access-policies"></a>Stratégies d’accès aux ressources
Les stratégies d’accès aux ressources configurent les paramètres VPN, Wi-Fi, d’e-mail et de certificat sur les appareils. Pour plus d’informations, consultez [Déployer des profils d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles).

#### <a name="endpoint-protection"></a>Endpoint Protection
À compter de Configuration Manager 1802, la charge de travail Endpoint Protection peut être transférée à Intune. Pour plus d’informations, consultez [Endpoint Protection pour Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10)<!-- 1357365 --> et [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).

#### <a name="device-configuration"></a>Configuration de l’appareil
À compter de Configuration Manager 1806, la charge de travail de configuration des appareils peut être transférée à Intune. Pour plus d’informations, consultez [Créer un profil d’appareil dans Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create) et [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).  <!--1357903-->

#### <a name="office-click-to-run-apps"></a>Applications « Démarrer en un clic » Office
À compter de Configuration Manager 1806, la charge de travail Office 365 peut être transférée à Intune. Pour plus d’informations, consultez [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). <!--1357841-->

#### <a name="mobile-apps"></a>Applications mobiles
À compter de Configuration Manager version 1806, la charge de travail des applications mobiles peut être transférée à Intune. Cette fonctionnalité est en préversion. Pour l’activer, consultez [Fonctionnalités de préversion](/sccm/core/servers/manage/pre-release-features). Une fois cette charge de travail transférée, toutes les applications disponibles déployées à partir d’Intune seront accessibles sur le Portail d’entreprise. Les applications déployées à partir de Configuration Manager sont disponibles dans le Centre logiciel.<!--1357892-->


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Installer le client Configuration Manager sur les appareils inscrits à Intune

Quand des appareils Windows 10 sont inscrits dans Intune, installez le client Configuration Manager sur les appareils [à l’aide d’une ligne de commande spécifique](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) pour préparer les clients à la cogestion. Ensuite, activez la cogestion à partir de la console Configuration Manager et commencez le déplacement de charges de travail spécifiques vers Intune pour des appareils Windows 10 spécifiques.
Quant aux appareils Windows 10 qui ne sont pas encore inscrits dans Intune, utilisez l’inscription automatique dans Azure pour les inscrire. Pour ce qui est des nouveaux appareils Windows 10, utilisez [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) pour configurer l’expérience OOBE (Out of Box Experience) qui inclut l’inscription automatique permettant d’inscrire des appareils dans Intune.

Quand vous utilisez Intune pour installer le client Configuration Manager, activez [Passerelle de gestion cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) dans Configuration Manager.



## <a name="monitor-co-management"></a>Surveiller la cogestion

[Le tableau de bord de cogestion](/sccm/core/clients/manage/co-management-dashboard) vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphes peuvent vous aider à identifier les appareils qui demandent une attention particulière.



## <a name="next-steps"></a>Étapes suivantes

[Préparer les appareils Windows 10 pour la cogestion](co-management-prepare.md)
