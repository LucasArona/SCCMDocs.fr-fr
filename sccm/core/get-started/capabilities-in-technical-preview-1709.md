---
title: Version Technical Preview 1709
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version 1709 de Technical Preview pour System Center Configuration Manager.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6aa1c324a3ff24feb14c6b867728a76252a8c19d
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176023"
---
# <a name="capabilities-in-technical-preview-1709-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1709 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version 1709 de Technical Preview pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problèmes connus dans cette version d’évaluation technique :**
- **La mise à jour vers la version 1709 de la préversion échoue s’il existe un serveur de site en mode passif**. Si vous exécutez la version 1706, 1707 ou 1708 de la préversion, et que vous avez un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez le désinstaller pour pouvoir correctement mettre à jour vers la version 1709 votre site de la préversion. Vous pouvez réinstaller le serveur de site en mode passif une fois votre site passé à la version 1709.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Expérience de profil VPN améliorée dans la console Configuration Manager
<!-- 1313282 -->
Avec cette version, nous avons mis à jour l’Assistant Création d’un profil VPN et les pages de propriétés pour afficher uniquement les paramètres appropriés à la plateforme sélectionnée. Plus précisément :

- Chaque plateforme a son propre flux de travail, ce qui signifie que les nouveaux profils VPN ne contiennent que les paramètres pris en charge par la plateforme.
- Les pages **Plateformes prises en charge** apparaissent désormais après la page **Général**.  Maintenant, vous choisissez la plateforme avant de définir les valeurs de propriété.
- Lorsque la plateforme est définie sur **Android**, **Android for Work** ou **Windows Phone 8.1**, la page **Plateformes prises en charge** est inutile et ne s’affiche pas.
- Le flux de travail du client Configuration Manager a été combiné aux flux de travail Windows 10 du client de l’appareil mobile hybride (MDM) ; ils prennent en charge les mêmes paramètres.
- Chaque flux de travail de plateforme inclut uniquement les paramètres appropriés à ce flux de travail.  Par exemple, le flux de travail Android contient les paramètres propres à Android ; les paramètres appropriés pour iOS ou Windows 10 Mobile n’apparaissent donc plus dans le flux de travail Android.
- Pour les appareils Windows 8.1, les paramètres gérés par Configuration Manager sont clairement marqués.
- La page VPN automatique est obsolète et a été supprimée.

Ces modifications s’appliquent aux nouveaux profils VPN.  

Pour réduire les problèmes de compatibilité, les profils VPN existants restent inchangés.  Lorsque vous modifiez un profil existant, les paramètres s’affichent comme au moment de sa création.  

### <a name="try-it-out"></a>Essayez !

Créez un profil VPN en suivant la procédure habituelle. Remarquez que les options dans la première page de l’Assistant Création d’un profil VPN ont été modifiées.

1.  Accédez à **Ressources et conformité** > **Vue d’ensemble** > **Paramètres de conformité** > **Accès aux ressources de l’entreprise** > **Profils VPN**, puis choisissez **Créer un profil VPN**.
2.  Entrez un nom dans la page **Général** et choisissez une des options suivantes sous **Spécifiez le type de profil VPN à créer** :

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS et macOS X  
    - Android  
    - Android for Work  

3.  Si vous choisissez **Windows 8.1**, vous avez également la possibilité de **Créer un profil** ou d’**Importer à partir d’un fichier**.
4.  Suivez l’Assistant pour terminer la création du profil.

Lorsque vous sélectionnez différentes plateformes, notez que seuls les paramètres correspondant à la plateforme sélectionnée s’affichent.

## <a name="co-management-for-windows-10-devices"></a>Cogestion pour les appareils Windows 10    
<!-- 1350871 -->
Nombreux sont les clients qui souhaitent gérer les appareils Windows 10 comme les appareils mobiles, en recourant à une solution cloud plus simple et moins chère. Toutefois, le passage de la gestion classique à la gestion moderne peut s’avérer difficile. À partir de Windows 10 version 1607 (également appelée Mise à jour anniversaire), vous pouvez joindre à la fois un appareil Windows 10 à Active Directory (AD) localement et à Azure AD basé sur le cloud (Azure AD hybride). La cogestion tire parti de cette amélioration et vous permet de gérer simultanément plusieurs appareils Windows 10 à l’aide de Configuration Manager et d’Intune. C’est une solution qui établit une passerelle entre la gestion classique et la gestion moderne tout en vous donnant la possibilité d’opérer cette transition selon une approche en plusieurs phases. 

### <a name="prerequisites"></a>Prérequis
Les prérequis suivants doivent être mis en place avant de pouvoir activer la cogestion. Il existe des prérequis généraux et des prérequis distincts pour les clients Configuration Manager existants et les appareils qui ne sont pas clients.

### <a name="known-issues"></a>Problèmes connus
Après avoir créé une stratégie de cogestion, vous ne pouvez plus y apporter de modifications. Il faut la supprimer pour la recréer avec les paramètres dont vous avez besoin. 

#### <a name="general-prerequisites"></a>Conditions préalables
Les prérequis généraux pour activer la cogestion sont les suivants :  

- Technical Preview pour Configuration Manager version 1709
- Azure AD 
- Licence EMS ou Intune pour tous les utilisateurs
- Abonnement Intune &#40;autorité MDM dans Intune définie sur **Intune**&#41;

   > [!Note]  
   > Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Si la migration vers la version autonome d’Intune vous intéresse, consultez [Démarrer la migration de MDM hybride vers la version autonome d’Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Prérequis supplémentaires pour les clients Configuration Manager existants
- Windows 10, version 1709 (Fall Creators Update) et ultérieure
- Jonction à Azure AD hybride (jonction à AD et à Azure AD)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Prérequis supplémentaires pour les nouveaux appareils Windows 10
- Windows 10, version 1709 (Fall Creators Update) et ultérieure
- [Passerelle de gestion cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) dans Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Charges de travail que vous pouvez basculer sur Intune
Après l’activation de la cogestion, Configuration Manager continue de gérer toutes les charges de travail. Lorsque vous pensez être prêt, vous pouvez laisser Intune gérer les charges de travail disponibles. Dans cette version, Intune peut assurer la gestion des charges de travail suivantes.   

#### <a name="compliance-policies"></a>Stratégies de conformité
Les stratégies de conformité définissent les règles et les paramètres auxquels doit se conformer un appareil pour être considéré conforme par les stratégies d’accès conditionnel. Vous pouvez également utiliser des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l'accès conditionnel. Pour plus d’informations, consultez [Stratégies de conformité des appareils](https://docs.microsoft.com/sccm/mdm/deploy-use/device-compliance-policies).  

#### <a name="windows-update-for-business-policies"></a>Stratégies Windows Update pour Entreprise
Les stratégies Windows Update pour Entreprise vous permettent de configurer des stratégies de report pour les mises à jour de fonctionnalités Windows 10 ou les mises à jour qualité pour les appareils Windows 10 gérés directement par Windows Update pour Entreprise. Pour plus d’informations, consultez [Configurer les stratégies de report Windows Update pour Entreprise](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Actions à distance disponibles dans Intune sur Azure pour les appareils gérés conjointement
Quand un appareil Windows 10 est activé pour la cogestion, les actions à distance suivantes sont disponibles sur Azure à partir d’Intune :  
- [Réinitialisation aux paramètres d’usine](https://docs.microsoft.com/intune/devices-wipe#factory-reset)
- [Réinitialisation sélective](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Suppression d’appareils](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Redémarrage d’un appareil](https://docs.microsoft.com/intune/device-restart)
- [Nouvelle version](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Préparer Intune pour la cogestion
Avant de basculer des charges de travail sur Intune à partir de Configuration Manager, créez les profils et les stratégies qui vous sont nécessaires dans Intune pour être sûr que vos appareils continuent d’être protégés.
Dans Intune, vous pouvez créer des objets basés sur les objets que vous utilisez dans Configuration Manager. Par contre, si votre stratégie actuelle est basée sur la gestion héritée ou la gestion classique, vous souhaiterez probablement prendre un moment pour réfléchir aux stratégies et aux profils dont vous avez besoin pour la gestion moderne. Utilisez les ressources suivantes pour créer les stratégies et les profils.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Stratégies Windows Update pour Entreprise](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Profils de configuration d’un appareil](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Présentation de l’architecture de cogestion
Le schéma suivant montre une vue d’ensemble de l’architecture de la cogestion et son intégration aux infrastructures de Configuration Manager et d’Intune existantes.

![Schéma de l’architecture de la cogestion](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Scénarios pour activer la cogestion  
Vous pouvez activer la cogestion pour les appareils Windows 10 inscrits dans Microsoft Intune et pour les clients Configuration Manager Windows 10 existants. Ces deux scénarios mènent à la gestion simultanée des appareils Windows 10 par Configuration Manager et par Intune, ainsi qu’à leur jonction à AD et à Azure AD.  

#### <a name="devices-enrolled-in-intune"></a>Appareils inscrits dans Intune  
Lorsque des appareils Windows 10 sont inscrits à Intune, vous pouvez y installer le client Configuration Manager (à l’aide d’un argument de ligne de commande spécifique) pour préparer les clients à la cogestion. Ensuite, activez la cogestion à partir de la console Configuration Manager et commencez le déplacement de charges de travail spécifiques vers Intune pour des appareils Windows 10 spécifiques.  

Quant aux appareils Windows 10 qui ne sont pas encore inscrits à Intune, vous pouvez utiliser l’inscription automatique dans Azure pour les inscrire. Pour ce qui est des nouveaux appareils Windows 10, vous pouvez utiliser Windows AutoPilot et configurer l’expérience OOBE (Out of Box experience) qui inclut l’inscription automatique permettant d’inscrire les appareils à Intune.  

#### <a name="configuration-manager-clients"></a>Clients Configuration Manager
Lorsque vous avez des appareils Windows 10 qui sont des clients Configuration Manager, vous pouvez les inscrire et activer la cogestion depuis la console Configuration Manager. Configuration Manager déclenche l’inscription automatique dans Intune en fonction des informations de locataire Azure AD.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Préparer les appareils Windows 10 pour la cogestion
Vous pouvez activer la cogestion sur les appareils Windows 10 qui sont joints à AD et à Azure AD, inscrits à Intune et clients dans Configuration Manager. Pour les nouveaux appareils Windows 10 et pour ceux qui sont déjà inscrits à Intune, installez le client Configuration Manager avant de pouvoir les cogérer. Pour les appareils Windows 10 qui sont déjà des clients Configuration Manager, inscrivez-les à Intune et activez la cogestion dans la console Configuration Manager.

#### <a name="command-line-to-install-configuration-manager-client"></a>Ligne de commande pour installer un client Configuration Manager
Créez une application dans Intune pour les appareils Windows 10 qui ne sont pas encore des clients Configuration Manager. Lors de la création de l’application dans les sections suivantes, utilisez cette ligne de commande :

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud*&#62;/ CCMHOSTNAME=&#60;*URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud*&#62; SMSSiteCode=&#60;*Codesite*&#62; SMSMP=https:&#47;/&#60;*Nom de domaine complet du point de gestion*&#62; AADTENANTID=&#60;*ID du locataire AAD*&#62; AADTENANTNAME=&#60;*Nom du locataire*&#62; AADCLIENTAPPID=&#60;*ID de l’application serveur pour l’intégration AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ID de la ressource*&#62;”

Par exemple, si vous aviez les valeurs suivantes :

- **URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud** : https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Utilisez la valeur **MutualAuthPath** dans la vue SQL **vProxy_Roles** pour la valeur **URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud**.

- **Nom de domaine complet du point de gestion** : sccmmp.corp.contoso.com    
- **Sitecode** : PS1    
- **ID du locataire Azure AD** : 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nom du locataire Azure AD** : contoso    
- **ID de l’application cliente Azure AD** : bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI d’ID de ressource AAD** : ConfigMgrServer    

  > [!Note]    
  > Utilisez la valeur **IdentifierUri** trouvée dans la vue SQL **vSMS_AAD_Application_Ex** pour la valeur **URI de l’ID de la ressource AAD**.

Vous utiliseriez la ligne de commande suivante :

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
>Pour trouver les paramètres de ligne de commande pour votre site, effectuez les étapes suivantes :     
> 1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.  
> 2. Sous l’onglet Accueil, dans le groupe Gérer, choisissez **Configurer la cogestion** pour ouvrir l’Assistant Intégration de la cogestion.    
> 3. Dans la page Abonnement, cliquez sur **Se connecter** et connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**.    
> 4. Dans la page Activation, cliquez sur **Copier** dans la section **Appareils inscrits dans Intune** pour copier la ligne de commande dans le Presse-papiers et l’enregistrer ensuite pour vous en servir ultérieurement dans la procédure de création de l’application.  
> 5. Cliquez sur **Annuler** pour quitter l’Assistant.

#### <a name="new-windows-10-devices"></a>Nouveaux appareils Windows 10
Pour les nouveaux appareils Windows 10, vous pouvez utiliser le service Autopilot pour configurer le mode OOBE (Out Of Box Experience) qui inclut la jonction de l’appareil à AD et à Azure AD, ainsi que son inscription dans Intune. Ensuite, créez une application dans Intune pour déployer le client Configuration Manager.  
1. Activez AutoPilot pour les nouveaux appareils Windows 10. Pour plus d’informations, consultez [Présentation de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configurez l’inscription automatique dans Azure AD pour que vos appareils soient inscrits automatiquement dans Intune. Pour plus d’informations, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).
3. Créez une application dans Intune avec le package du client Configuration Manager et déployez l’application sur les appareils Windows 10 que vous souhaitez gérer conjointement. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Appareils Windows 10 non inscrits à Intune ou non-clients Configuration Manager
Pour les appareils Windows 10 qui ne sont pas inscrits à Intune ou qui n’ont pas le client Configuration Manager, vous pouvez utiliser l’inscription automatique pour les inscrire dans Intune. Ensuite, créez une application dans Intune pour déployer le client Configuration Manager.
1. Configurez l’inscription automatique dans Azure AD pour que vos appareils soient inscrits automatiquement à Intune. Pour plus d’informations, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  
2. Créez une application dans Intune avec le package du client Configuration Manager et déployez l’application sur les appareils Windows 10 que vous souhaitez gérer conjointement. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).

#### <a name="windows-10-devices-enrolled-in-intune"></a>Appareils Windows 10 inscrits à Intune
Pour les appareils Windows 10 qui sont déjà inscrits à Intune, créez une application dans Intune pour déployer le client Configuration Manager. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Basculer les charges de travail de Configuration Manager sur Intune
Dans la section précédente, vous avez préparé les appareils Windows 10 pour la cogestion. Ces appareils sont désormais joints à AD et à Azure AD, ils sont inscrits dans Intune et ont le client Configuration Manager. Vous avez probablement encore des appareils Windows 10 joints à AD et qui ont le client Configuration Manager, mais qui ne sont pas joints à Azure AD ni inscrits à Intune. La procédure suivante présente les étapes permettant d’activer la cogestion et de préparer le reste de vos appareils Windows 10 (les clients Configuration Manager sans inscription à Intune) pour la cogestion ; elle vous sert également à lancer le basculement de charges de travail spécifiques de Configuration Manager vers Intune.

1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.    
2. Sous l’onglet Accueil, dans le groupe Gérer, choisissez **Configurer la cogestion** pour ouvrir l’Assistant Intégration de la cogestion.    
3. Dans la page Abonnement, cliquez sur **Se connecter** et connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**.   
4. Dans la page Préparation, configurez les paramètres suivants et cliquez sur **Suivant** :
    - **Groupe pilote** : le groupe pilote contient un ou plusieurs regroupements que vous sélectionnez. Utilisez ce groupe dans le cadre de votre déploiement progressif de la cogestion. Vous pouvez commencer par un regroupement test peu volumineux, puis ajouter d’autres regroupements à ce groupe pilote au fur et à mesure que vous déployez la cogestion pour d’autres utilisateurs et appareils. À tout moment, vous pouvez modifier les regroupements dans le groupe pilote à partir des propriétés de cogestion.
    - **Production** : lorsque vous sélectionnez ce paramètre, tous les appareils Windows 10 pris en charge sont activés pour la cogestion. Configurez le **Groupe d’exclusions** avec un ou plusieurs regroupements. Les appareils membres d’une des collections de ce groupe sont exclus de l’utilisation de la cogestion. 
5. Dans la page Activation, choisissez **Pilote** ou **Tout** (selon les paramètres que vous avez configurés dans la page Préparation) pour activer l’inscription automatique dans Intune, puis cliquez sur **suivant**. Lorsque vous choisissez **Pilote**, seuls les clients Configuration Manager membres du groupe pilote sont automatiquement inscrits à Intune. Cela vous permet d’activer la cogestion sur une partie des clients pour tester initialement la cogestion et la déployer au moyen d’une approche progressive. 
6. Dans la page Charges de travail, choisissez de basculer ou non les charges de travail de Configuration Manager devant être gérées par Intune, puis cliquez sur **suivant**. Utilisez les curseurs pour sélectionner le basculement de la charge de travail vers le groupe pilote, ou pour tous les clients Windows 10 (selon les paramètres que vous avez configurés dans la page Préparation). 
7. Pour activer la cogestion, terminez l’Assistant.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Voir aussi
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview). 
