---
title: Installer le client avec Azure AD
titleSuffix: Configuration Manager
description: Installer et affecter le client Configuration Manager sur les appareils Windows 10 en utilisant Azure Active Directory pour l’authentification
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b722187a895a71b4195200354180cdbc8b2813e6
ms.sourcegitcommit: 12b71da551350c99c5916df3629e33e31040db15
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/17/2018
ms.locfileid: "53530912"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installer et affecter des clients Windows 10 Configuration Manager à l’aide d’Azure AD à des fins d’authentification

Pour installer le client Configuration Manager sur des appareils Windows 10 en utilisant l’authentification Azure AD, intégrez Configuration Manager à Azure Active Directory (Azure AD). Les clients peuvent communiquer sur l’intranet, directement avec un point de gestion HTTPS ou un point de gestion dans un site activé pour HTTP amélioré. Ils peuvent aussi communiquer sur Internet via la passerelle de gestion cloud ou avec un point de gestion Internet. Ce processus utilise Azure AD pour authentifier les clients auprès du site Configuration Manager. Azure AD élimine le besoin de configurer et d’utiliser des certificats d’authentification client.



## <a name="before-you-begin"></a>Avant de commencer

- Un locataire Azure AD est un prérequis.  

- Conditions requises pour les appareils :  

    - Windows 10  

    - Joint à Azure AD, joint à un domaine pur cloud ou joint à Azure AD hybride  

- Conditions requises pour les utilisateurs :  

    - L’utilisateur connecté doit être une identité Azure AD.   

    - Si l’utilisateur est une identité fédérée ou synchronisée, vous devez utiliser la [découverte d’utilisateurs Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) de Configuration Manager ainsi que la [découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc). Pour plus d’informations sur les identités hybrides, consultez [Définir une stratégie d’adoption des identités hybrides](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- En plus des [prérequis](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) pour le rôle de système de site du point de gestion, activez aussi **ASP.NET 4.5** sur ce serveur. Incluez toutes les autres options qui sont sélectionnées automatiquement quand vous activez ASP.NET 4.5.  

- Déterminez si votre point de gestion a besoin du protocole HTTPS. Pour plus d’informations, consultez [Activer le point de gestion pour HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

- Vous pouvez aussi configurez une [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) pour déployer des clients Internet. Pour les clients locaux qui s’authentifient avec Azure AD, vous n’avez pas besoin d’une passerelle de gestion cloud.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurer des services Azure pour la gestion cloud

La première étape consiste à connecter votre site Configuration Manager à Azure AD. Pour plus d’informations sur ce processus, consultez [Configurer des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Créez une connexion au service de **gestion cloud**.

Activez [Découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) dans le cadre de l’intégration à la **gestion cloud**. 

Une fois ces actions effectuées, votre site Configuration Manager est connecté à Azure AD. 



## <a name="configure-client-settings"></a>Configurer les paramètres client

Ces paramètres client permettent de joindre des appareils Windows 10 à Azure AD. Ils permettent également aux clients Internet d’utiliser la passerelle de gestion cloud et le point de distribution cloud.

1.  Configurez les paramètres client suivants dans la section **Services cloud** en utilisant les informations du [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).  

    - **Autoriser l’accès au point de distribution cloud** : activez ce paramètre afin que les appareils Internet puissent obtenir le contenu nécessaire pour installer le client Gestionnaire de configuration. Si le contenu n’est pas disponible sur le point de distribution cloud, les appareils peuvent récupérer le contenu auprès de la passerelle de gestion cloud. Le programme d’amorçage de l’installation du client réessaye le point de distribution cloud pendant 4 heures avant de passer à la passerelle de gestion cloud.<!--495533-->  

    - **Inscrire automatiquement les nouveaux appareils joints au domaine Windows 10 auprès d’Azure Active Directory** : définissez la valeur sur **Oui** ou **Non**. La valeur par défaut est **Oui**. Ce comportement est également celui par défaut dans Windows 10, version 1709.

    - **Permettre aux clients d’utiliser une passerelle de gestion cloud** : réglez sur **Oui** (valeur par défaut) ou **Non**.  

2.  Déployez les paramètres client sur la collection requise d’appareils. Ne déployez pas ces paramètres sur des regroupements d’utilisateurs.

Pour vérifier que l’appareil est joint à Azure AD, exécutez `dsregcmd.exe /status` dans une invite de commandes. Le champ **AzureAdjoined** dans les résultats indique **OUI** si l’appareil est joint à Azure AD.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Installer et inscrire le client avec l’identité Azure AD

Pour installer manuellement le client avec l’identité Azure AD, passez d’abord en revue le processus général dans [Comment installer des clients manuellement](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > L’appareil a besoin d’accéder à Internet pour contacter Azure AD, mais n’a pas besoin d’être basé sur Internet. 

L’exemple suivant montre la structure générale de la ligne de commande : `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Pour plus d’informations, consultez [Propriétés de l’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).

Les propriétés /mp et CCMHOSTNAME spécifient l’un des éléments suivants, en fonction du scénario :
- Point de gestion local. Spécifiez seulement la propriété /mp. CCMHOSTNAME n’est pas obligatoire.
- Passerelle de gestion cloud
- Point de gestion Internet. La propriété SMSMP spécifie le point de gestion Internet ou local.

Cet exemple utilise une passerelle de gestion cloud. Il remplace les exemples de valeurs pour chaque propriété : `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Pour automatiser l’installation en utilisant l’identité Azure AD via Microsoft Intune, consultez le processus pour [Préparer les appareils Windows 10 pour la cogestion](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).



## <a name="next-steps"></a>Étapes suivantes

Une fois terminé, vous pouvez continuer à [surveiller et gérer les clients](/sccm/core/clients/manage/monitor-clients).
