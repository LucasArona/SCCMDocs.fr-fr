---
title: Préparer Windows 10 pour la cogestion
titleSuffix: Configuration Manager
description: Découvrez comment préparer vos appareils Windows 10 pour la cogestion.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: d15484ef38264a5c954dc664f9885b800a078ca6
ms.sourcegitcommit: 2badee2b63ae63687795250e298f463474063100
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/14/2018
ms.locfileid: "45601005"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Préparer les appareils Windows 10 pour la cogestion
Vous pouvez activer la cogestion sur les appareils Windows 10 qui sont joints à AD et à Azure AD, et inscrits auprès de Microsoft Intune et d’un client dans Configuration Manager. Pour les nouveaux appareils Windows 10 et pour ceux qui sont déjà inscrits à Intune, installez le client Configuration Manager avant de pouvoir les cogérer. Pour les appareils Windows 10 qui sont déjà des clients Configuration Manager, inscrivez-les à Intune et activez la cogestion dans la console Configuration Manager.

> [!IMPORTANT]
> Les appareils mobiles Windows 10 ne prennent pas en charge la cogestion.



## <a name="prerequisites"></a>Prérequis

Les prérequis suivants doivent être mis en place avant de pouvoir activer la cogestion. Il existe des prérequis généraux et des prérequis distincts pour les appareils dotés du client Configuration Manager et les appareils sur lesquels le client n’est pas installé.


### <a name="general-prerequisites"></a>Conditions préalables

Les prérequis généraux pour activer la cogestion sont les suivants :  

- Configuration Manager version 1710 ou ultérieure  

    - À compter de Configuration Manager version 1806, vous pouvez connecter plusieurs instances Configuration Manager à un seul locataire Intune. <!--1357944-->  

- [Site intégré à Azure AD pour la gestion cloud](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- Licence EMS ou Intune pour tous les utilisateurs  

- [Inscription automatique auprès d’Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) activée  

- Abonnement Intune et autorité MDM dans Intune définie sur **Intune**.  

    - Si vous utilisez une [autorité mixte](/sccm/mdm/deploy-use/migrate-mixed-authority), effectuez d’abord la migration vers Intune autonome. Ensuite, définissez l’autorité MDM sur Intune avant de configurer la cogestion.<!--SCCMDocs issue #797-->


> [!Note]  
> Si vous avez un environnement MDM hybride (Intune intégré à Configuration Manager), vous ne pouvez pas activer la cogestion. Toutefois, vous pouvez commencer la migration d’utilisateurs vers Intune autonome, puis activer leurs appareils Windows 10 associés pour la cogestion. Pour plus d’informations sur la migration vers Intune autonome, consultez [Démarrer la migration de MDM hybride vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).


### <a name="prerequisite-azure-resource-manager-roles"></a>Rôles Azure Resource Manager prérequis
<!--SCCMDocs issue #667--> Pour plus d’informations sur les rôles Azure, consultez [Présentation des différents rôles](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).
|Action|Rôle nécessaire|
|----|----|
|Configurer une passerelle de gestion cloud|Gestionnaire d’abonnements Azure|
|Configurer un point de distribution cloud|Gestionnaire d’abonnements Azure|
|Créer des applications Azure Active Directory à partir de la console Configuration Manager|Administrateur général Azure Active Directory|
|Importer des applications clientes et serveur Azure dans la console Configuration Manager| Administrateur Configuration Manager, aucun rôle Azure supplémentaire nécessaire|
|Configurer la cogestion à l’aide de l’Assistant Cogestion| Droits de l’utilisateur Azure Active Directory, et être administrateur Configuration Manager avec des droits sur toutes les étendues 


### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Prérequis supplémentaires pour les appareils dotés du client Configuration Manager

- Windows 10, version 1709 ou ultérieure  

- [Jonction à Azure AD hybride](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) (jonction à AD et à Azure AD)  


### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Prérequis supplémentaires pour les appareils non dotés du client Configuration Manager

- Windows 10, version 1709 ou ultérieure  

- [Passerelle de gestion cloud](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) dans Configuration Manager (quand vous utilisez Intune pour installer le client Configuration Manager)  


> [!IMPORTANT]
> Les appareils mobiles Windows 10 ne prennent pas en charge la cogestion.



## <a name="command-line-to-install-configuration-manager-client"></a>Ligne de commande pour installer un client Configuration Manager

Créez une application dans Intune pour les appareils Windows 10 qui ne sont pas encore des clients Configuration Manager. Lors de la création de l’application dans les sections suivantes, utilisez cette ligne de commande :

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### <a name="example-command-line"></a>Exemple de ligne de commande
Si vous avez les valeurs suivantes :

- **URL du point de terminaison d’authentification mutuelle de la passerelle de gestion cloud** : `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!Note]    
   >Utilisez la valeur **MutualAuthPath** dans la vue SQL **vProxy_Roles** pour la valeur **URL du point de terminaison de l’authentification mutuelle pour la passerelle de gestion cloud**.  

- **FQDN du point de gestion** : `mp1.contoso.com`    
- **Sitecode** : `PS1`    
- **ID de locataire Azure AD** : `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **ID d’application cliente Azure AD** : `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **URI d’ID de ressource AAD** : `ConfigMgrServer`    

  > [!Note]    
  > Utilisez la valeur **IdentifierUri** trouvée dans la vue SQL **vSMS_AAD_Application_Ex** pour la valeur **URI de l’ID de la ressource AAD**.  

Utilisez alors la ligne de commande suivante :

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215--> À compter de la version 1806, moins de propriétés sont maintenant nécessaires pour la ligne de commande.  

- Les propriétés de ligne de commande suivantes sont nécessaires pour tous les scénarios :  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Les propriétés suivantes sont nécessaires lorsque vous utilisez Azure AD pour l’authentification client, au lieu de certificats d’authentification client PKI :  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- La propriété suivante est nécessaire si le client doit revenir à l’intranet :  
    - SMSMP  

L’exemple suivant comprend toutes les propriétés mentionnées ci-dessus :   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Pour plus d’informations, consultez [Propriétés de l’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).


> [!Tip]
> Recherchez les paramètres de ligne de commande pour votre site en effectuez les étapes suivantes :     
> 
> 1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**.  
> 
> 2. Dans le ruban, sélectionnez **Configurer la cogestion** pour ouvrir l’Assistant Intégration de la cogestion. (Si vous avez déjà configuré la cogestion, sélectionnez **Propriétés**. Passez ensuite à l’étape 4.)    
> 
> 3. Dans la page Abonnement, sélectionnez **Se connecter**. Connectez-vous à votre locataire Intune, puis cliquez sur **Suivant**.    
> 
> 4. Dans la page Activation, sélectionnez **Copier** pour copier la ligne de commande dans le Presse-papiers. Enregistrez ensuite la ligne de commande à utiliser dans la procédure pour créer l’application.  
> 
> 5. Cliquez sur **Annuler** pour quitter l’Assistant.  

> [!Important]    
> Si vous personnalisez la ligne de commande pour installer le client Configuration Manager, veillez à ce qu’elle ne dépasse pas 1 024 caractères. Quand la ligne de commande fait plus de 1024 caractères, l’installation du client échoue.



## <a name="new-windows-10-devices"></a>Nouveaux appareils Windows 10

Pour les nouveaux appareils Windows 10, vous pouvez utiliser le service Autopilot pour configurer le mode OOBE (Out Of Box Experience) qui inclut la jonction de l’appareil à AD et à Azure AD, ainsi que son inscription dans Intune. Ensuite, créez une application dans Intune pour déployer le client Configuration Manager.  

1. Activez AutoPilot pour les nouveaux appareils Windows 10. Pour plus d’informations, consultez [Présentation de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > À compter de la version 1802, utilisez Configuration Manager pour collecter et signaler les informations des appareils nécessaires à Microsoft Store pour Entreprises et Éducation. numéro de série, identificateur de produit Windows et identificateur matériel. Dans l’espace de travail **Monitoring** de la console de Configuration Manager, développez le nœud **Création de rapports**, puis **Rapports**, et sélectionnez le nœud **Matériel – Général**. Exécutez le nouveau rapport, **Informations sur les appareils Windows AutoPilot**, et affichez les résultats. Dans la visionneuse de rapports, cliquez sur l’icône **Exporter**, puis sélectionnez l’option **CSV (délimité par des virgules)**. Après avoir enregistré le fichier, chargez les données dans Microsoft Store pour Entreprises et Éducation. Pour plus d’informations, consultez la page [Ajouter des appareils dans Microsoft Store pour Entreprises et Éducation](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).

2. Configurez l’inscription automatique dans Azure AD pour que vos appareils soient inscrits automatiquement à Intune. Pour plus d’informations, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

3. Créez une application dans Intune avec le package du client Configuration Manager et déployez l’application sur les appareils Windows 10 que vous souhaitez gérer conjointement. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   



## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Appareils Windows 10 non inscrits à Intune ou non-clients Configuration Manager

Pour les appareils Windows 10 qui ne sont pas inscrits dans Intune ou qui disposent du client Configuration Manager, vous pouvez utiliser l’inscription automatique pour les inscrire dans Intune. Ensuite, créez une application dans Intune pour déployer le client Configuration Manager.

1. Configurez l’inscription automatique dans Azure AD pour que vos appareils soient inscrits automatiquement à Intune. Pour plus d’informations, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  

2. Créez une application dans Intune avec le package du client Configuration Manager et déployez l’application sur les appareils Windows 10 que vous souhaitez gérer conjointement. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).



## <a name="windows-10-devices-enrolled-in-intune"></a>Appareils Windows 10 inscrits à Intune

Pour les appareils Windows 10 qui sont déjà inscrits à Intune, créez une application dans Intune pour déployer le client Configuration Manager. Utilisez la [ligne de commande pour installer un client Configuration Manager](#command-line-to-install-configuration-manager-client) lorsque vous suivez les étapes permettant d’[installer des clients à partir d’Internet avec Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  



## <a name="next-steps"></a>Étapes suivantes

[Basculer les charges de travail de Configuration Manager sur Intune](co-management-switch-workloads.md)
