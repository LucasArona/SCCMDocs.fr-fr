---
title: Cogestion pour les appareils Windows 10
titleSuffix: Configuration Manager
description: Découvrez comment gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: d6bbc787-83a5-44b4-ad64-016e5da7413f
ms.openlocfilehash: 9324126014245b586ba8fed87c670ac829f6cb81
ms.sourcegitcommit: 493cc42f05b9388ef872e466e5a75d569642b9fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34703466"
---
# <a name="co-management-for-windows-10-devices"></a>Cogestion pour les appareils Windows 10    
 Dans les mises à jour précédentes de Windows 10, vous pouviez déjà joindre un appareil Windows 10 à Active Directory (AD) en local et à Azure AD sur le cloud (Azure AD hybride). À compter de Configuration Manager version 1710, la cogestion tire parti de cette amélioration et vous permet de gérer simultanément plusieurs appareils Windows 10 version 1709 à l’aide de Configuration Manager et d’Intune. <!-- 1350871 -->
## <a name="why-co-management"></a>Pourquoi la cogestion ?
Nombreux sont les clients qui souhaitent gérer les appareils Windows 10 comme les appareils mobiles, en recourant à une solution cloud plus simple et moins chère. Toutefois, le passage de la gestion classique à la gestion moderne peut s’avérer difficile.  
## <a name="what-is-co-management"></a>Qu’est-ce que la cogestion ?
La cogestion vous permet de gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et d’Intune. C’est une solution qui établit une passerelle entre la gestion classique et la gestion moderne tout en vous donnant la possibilité d’opérer cette transition selon une approche en plusieurs phases.

## <a name="benefits"></a>Avantages 
- Utilisation immédiate des fonctionnalités Intune 
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
        - [Endpoint Protection](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10), à compter de Configuration Manager 1802 <!-- 1357365 -->
    
## <a name="how-to-configure-co-management"></a>Comment configurer la cogestion
Il existe deux principaux parcours pour accéder à la cogestion. Le premier a trait à la cogestion provisionnée par Configuration Manager où les appareils Windows 10 gérés conjointement par Configuration Manager et Azure AD hybride sont inscrits dans Intune. Le second fait intervenir les appareils provisionnés par Intune qui sont inscrits dans Intune, puis installés avec le client Configuration Manager pour atteindre l’état de cogestion.

### <a name="configuration-manager"></a>**Configuration Manager**
 -  Effectuez une mise à niveau vers Configuration Manager version 1710 ou ultérieure.


### <a name="azure-active-directory"></a>**Azure Active Directory**
  - [Jonction à Azure AD hybride](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (jonction à AD et à Azure AD).
  - [Activez l’inscription automatique Windows 10.](https://docs.microsoft.com/intune/windows-enroll)


### <a name="intune"></a>**Intune**
 - [Comment configurer un abonnement Intune](/sccm/mdm/deploy-use/configure-intune-subscription) ou [Configurer Intune](/intune/setup-steps)  
 - [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  

> [!Note]  
> Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Toutefois, vous pouvez commencer la migration d’utilisateurs vers Intune autonome, puis activer leurs appareils Windows 10 associés pour la cogestion. Pour plus d’informations sur la migration vers Intune autonome, consultez [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).  


### <a name="enable-co-management"></a>Activer la cogestion 
 Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**. Choisissez  **Configurer la cogestion** à partir du ruban pour ouvrir l’**Assistant Intégration de la cogestion** 
   
1. Dans la page **Abonnement**, cliquez sur **Se connecter** et connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**. Vérifiez que le compte utilisé pour se connecter à votre locataire dispose d’une licence Intune. Si ce n’est pas le cas, la connexion échoue avec le message d’erreur suivant : « Utilisateur non reconnu ».   
2. Dans la page **Activation**, choisissez votre paramètre **Inscription automatique dans Intune**. Copiez la ligne de commande pour les appareils déjà inscrits dans Intune, si nécessaire. 
3. Dans la page **Charges de travail**, de chaque charge de travail, choisissez le groupe d’appareils concerné par la gestion avec Intune.
4. Dans la page **Mise en lots**, sélectionnez un regroupement d’appareils en tant que **regroupement pilote**. Vérifiez les informations de **résumé** et terminez l’Assistant. 

### <a name="upgrade-windows-10-client"></a>Mettre à niveau le client Windows 10
- Effectuez une mise à niveau vers [Windows 10, version 1709 (également appelée Fall Creators Update) et ultérieure](/sccm/osd/deploy-use/manage-windows-as-a-service).

### <a name="configure-workloads-to-switch-to-intune"></a>Configurer les charges de travail pour basculer vers Intune 
L’article intitulé [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune) vous explique comment basculer des charges de travail Configuration Manager spécifiques vers Intune. Cet article comprend également des instructions sur la modification des groupes d’appareils pour lesquels des charges de travail sont transférées.

- **Stratégies de conformité :** Les stratégies de conformité définissent les règles et les paramètres auxquels doit se conformer un appareil pour être considéré conforme par les stratégies d’accès conditionnel. Vous pouvez également utiliser des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l'accès conditionnel. Pour plus d’informations, consultez [Stratégies de conformité des appareils](https://docs.microsoft.com/intune/device-compliance-get-started).  

- **Stratégies Windows Update :** Les stratégies Windows Update pour Entreprise vous permettent de configurer des stratégies de report pour les mises à jour de fonctionnalités Windows 10 ou les mises à jour qualité pour les appareils Windows 10 gérés directement par Windows Update pour Entreprise. Pour plus d’informations, consultez [Configurer les stratégies de report Windows Update pour Entreprise](https://docs.microsoft.com/intune/windows-update-for-business-configure).  

- **Stratégies d’accès aux ressources :** Les stratégies d’accès aux ressources configurent les paramètres VPN, Wi-Fi, d’e-mail et de certificat sur les appareils. Pour plus d’informations, consultez [Déployer des profils d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles).

- **Endpoint Protection:** À compter de Configuration Manager 1802, la charge de travail Endpoint Protection peut être transférée à Intune. Pour plus d’informations, consultez [Endpoint Protection pour Microsoft Intune](https://docs.microsoft.com/en-us/intune/endpoint-protection-windows-10)<!-- 1357365 --> et [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune).


### <a name="install-configuration-manager-client-to-the-devices-enrolled-in-intune"></a>Installer le client Configuration Manager sur les appareils inscrits à Intune
Lorsque des appareils Windows 10 sont inscrits à Intune, vous pouvez y installer le client Configuration Manager ([à l’aide d’un argument de ligne de commande spécifique](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client)) pour préparer les clients à la cogestion. Ensuite, activez la cogestion à partir de la console Configuration Manager et commencez le déplacement de charges de travail spécifiques vers Intune pour des appareils Windows 10 spécifiques.
Quant aux appareils Windows 10 qui ne sont pas encore inscrits à Intune, vous pouvez utiliser l’inscription automatique dans Azure pour les inscrire. Pour ce qui est des nouveaux appareils Windows 10, vous pouvez utiliser [Windows AutoPilot](https://docs.microsoft.com/intune/enrollment-autopilot) et configurer l’expérience OOBE (Out of Box Experience) qui inclut l’inscription automatique permettant d’inscrire les appareils à Intune.
 - Activez [Passerelle de gestion cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) dans Configuration Manager (uniquement lorsque vous utilisez Intune pour installer le client Configuration Manager).

## <a name="monitor-co-management"></a>Surveiller la cogestion
[Le tableau de bord de cogestion](/sccm/core/clients/manage/co-management-dashboard) vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphes peuvent vous aider à identifier les appareils qui demandent une attention particulière.


## <a name="next-steps"></a>Étapes suivantes
[Préparer les appareils Windows 10 pour la cogestion](co-management-prepare.md)
