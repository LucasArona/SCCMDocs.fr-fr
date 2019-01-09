---
title: HTTP amélioré
titleSuffix: Configuration Manager
description: Utilisez une méthode d’authentification moderne pour sécuriser les communications clientes sans avoir besoin de certificats PKI.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f2fab639082e6871e5df8dcebe0d1b3a440624c
ms.sourcegitcommit: 1bf26b83fa7da637d299a21e1d3bc61f2d7d8c10
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/07/2019
ms.locfileid: "54060363"
---
# <a name="enhanced-http"></a>HTTP amélioré

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> Cette fonctionnalité a été introduite dans la version 1806 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1810, cette fonctionnalité n’est plus en préversion.  


Microsoft conseille d’utiliser la communication HTTPS pour tous les chemins de communication Configuration Manager, mais c’est difficile pour certains clients en raison du temps de traitement lié à la gestion des certificats PKI. L’intégration à Azure Active Directory (Azure AD) permet d’éviter une partie de ces exigences de certificat. 

La version 1806 de Configuration Manager contient des améliorations concernant la façon dont les clients communiquent avec les systèmes de site. Ces améliorations avaient deux principaux objectifs :  

- Sécuriser les communications clientes sensibles sans avoir besoin de certificats d’authentification serveur PKI.  

- Permettre aux clients d’accéder de manière sécurisée au contenu des points de distribution sans avoir besoin d’un compte d’accès réseau, d’un certificat PKI client ou d’une authentification Windows.  

> [!Note]  
> L’utilisation de certificats PKI reste possible pour les clients qui ont les exigences suivantes :   
> - Utilisation du protocole HTTPS pour toutes les communications clientes  
> - Contrôle avancé de l’infrastructure de signature  


## <a name="bkmk_scenario"></a> Scénarios

Les scénarios suivants bénéficient de ces améliorations :  


### <a name="bkmk_scenario1"></a> Scénario 1 : Client vers point de gestion
<!--1356889-->

Les [appareils joints à Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) peuvent communiquer avec un point de gestion configuré pour HTTP. Le serveur de site génère un certificat pour le point de gestion afin de lui permettre de communiquer via un canal sécurisé.   

> [!Note]  
> Ce comportement est différent de celui observé dans Configuration Manager Current Branch version 1802, où l’utilisation d’un point de gestion HTTPS est nécessaire pour que les appareils joints à Azure AD puissent communiquer par le biais d’une passerelle de gestion cloud. Pour plus d’informations, consultez [Activer le point de gestion pour HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_scenario2"></a> Scénario 2 : Client vers point de distribution
<!--1358228-->

Un groupe de travail ou un client joint à Azure AD peut s’authentifier et télécharger du contenu via un canal sécurisé à partir d’un point de distribution configuré pour HTTP. Ces types d’appareils peuvent également s’authentifier et télécharger du contenu à partir d’un point de distribution configuré pour HTTPS sans avoir besoin d’un certificat PKI sur le client. L’ajout d’un certificat d’authentification client à un groupe de travail ou à un client joint à Azure AD est un processus compliqué.

Ce comportement inclut des scénarios de déploiement de système d’exploitation avec une séquence de tâches exécutée à partir d’un support de démarrage, d’un environnement PXE (Preboot Execution Environment) ou du Centre logiciel. Pour plus d’informations, consultez [Compte d’accès réseau](/sccm/core/plan-design/hierarchy/accounts#network-access-account).<!--1358278-->


### <a name="bkmk_scenario3"></a> Scénario 3 : Identité d’appareil Azure AD 
<!--1358460-->

Un appareil joint à Azure AD ou un [appareil Azure AD hybride](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) peut communiquer de manière sécurisée avec son site attribué, sans qu’un utilisateur Azure AD soit connecté. L’identité d’appareil cloud est désormais suffisante pour s’authentifier auprès du point de gestion et de la passerelle de gestion cloud dans les scénarios orientés appareil. (Un jeton d’utilisateur est toujours requis dans les scénarios orientés utilisateur.)  


## <a name="prerequisites"></a>Prérequis  

- Un point de gestion configuré pour les connexions clientes HTTP. Définissez cette option sous l’onglet **Général** des propriétés du rôle de système de site.  

- Un point de distribution configuré pour les connexions clientes HTTP. Définissez cette option sous l’onglet **Général** des propriétés du rôle de système de site. N’activez pas l’option **Autoriser les clients à se connecter anonymement**.  

- Intégrer le site à Azure AD pour la gestion cloud  

    - Si vous avez déjà effectué cette intégration pour votre site, mettez à jour l’application Azure AD. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Locataires Azure Active Directory**. Sélectionnez le locataire Azure AD, sélectionnez l’application web dans le volet **Applications**, puis sélectionnez **Mettre à jour les paramètres d’application** dans le ruban.  

- *Pour [Scénario 3](#bkmk_scenario3) uniquement* : Un client exécutant Windows 10 version 1803 ou ultérieure et joint à Azure AD. 



## <a name="configure-the-site"></a>Configurer le site

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site, puis choisissez **Propriétés** dans le ruban.  

2. Passez à l’onglet **Communication de l’ordinateur client**. Sélectionnez l’option **HTTPS ou HTTP**, puis activez l’option **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**.  

> [!Tip]
> Un délai maximal de 30 minutes est nécessaire pour que le point de gestion reçoive puis configure le nouveau certificat du site.

Vous pouvez voir ces certificats dans la console Configuration Manager. Accédez à l’espace de travail **Administration**, développez **Sécurité**, puis sélectionnez le nœud **Certificats**. Recherchez le certificat racine **Émission de SMS**, ainsi que les certificats de rôle serveur de site émis par ce certificat racine.

Pour plus d’informations sur la façon dont le client communique avec le point de gestion et le point de distribution dans cette configuration, consultez [Communications depuis les clients vers les systèmes de site et les services](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System).



## <a name="see-also"></a>Voir aussi
- [Planifier la sécurité](/sccm/core/plan-design/security/plan-for-security)  

- [Sécurité et confidentialité pour les clients Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurer la sécurité](/sccm/core/plan-design/security/configure-security)  

- [Communications entre points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

