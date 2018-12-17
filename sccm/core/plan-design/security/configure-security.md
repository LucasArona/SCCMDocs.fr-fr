---
title: Configurer la sécurité
titleSuffix: Configuration Manager
description: Configurez les options de sécurité pour Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d1aaf6db583d9749dda3be14cfd06acbff19b093
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456088"
---
# <a name="configure-security-in-configuration-manager"></a>Configurer la sécurité dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cet article pour configurer les options de sécurité pour Configuration Manager. Il décrit les options de sécurité suivantes :
- [Communication de l’ordinateur client](#BKMK_ConfigureClientPKI) pour les certificats clients PKI  
- [Signature et chiffrement](#BKMK_ConfigureSigningEncryption)  
- [Administration basée sur des rôles](#BKMK_ConfigureRBA)  
- [Gérer les comptes](#BKMK_ManageAccounts)  
- [Configurer Azure Active Directory](#bkmk_azuread)  
- [Configurer l’authentification du fournisseur SMS](#bkmk_auth)  



##  <a name="BKMK_ConfigureClientPKI"></a> Configurer les paramètres de certificat client PKI  

Si vous souhaitez utiliser des certificats PKI (infrastructure à clés publiques) pour les connexions client aux systèmes de site utilisant les services IIS (Internet Information Services), la procédure suivante vous permet de configurer les paramètres pour ces certificats.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Pour configurer des paramètres de certificat client PKI  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site principal à configurer.  

2.  Dans le ruban, choisissez **Propriétés**. Passez ensuite à l’onglet **Communication de l’ordinateur client**.  

    Cet onglet est disponible uniquement sur un site principal. Si vous ne voyez pas l’onglet **Communication de l’ordinateur client**, vérifiez que vous n’êtes pas connecté à un site d’administration centrale ni à un site secondaire.  

3.  Sélectionnez les paramètres pour les systèmes de site qui utilisent IIS.  

    - **HTTPS uniquement** : les clients affectés au site utilisent toujours un certificat client PKI quand ils se connectent à des systèmes de site qui utilisent IIS.  

    - **HTTPS ou HTTP** : vous n’exigez pas que les clients utilisent des certificats PKI.  

    - **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP** : pour plus d’informations sur ce paramètre, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).  

4.  Sélectionnez les paramètres pour les ordinateurs clients.  

    - **Utiliser le certificat client PKI (fonctionnalité d’authentification client)** : si vous choisissez le paramètre de serveur de site **HTTPS or HTTP**, choisissez cette option pour utiliser un certificat client PKI pour les connexions HTTP. Le client utilise ce certificat au lieu d'un certificat auto-signé pour s'authentifier auprès des systèmes de site. Si vous choisissez **HTTPS uniquement**, cette option est automatiquement sélectionnée.  

    Quand plusieurs certificats clients PKI valides sont disponibles sur un client, choisissez **Modifier** pour configurer les méthodes de sélection de certificat client.  

    Pour plus d’informations sur la méthode de sélection des certificats clients, consultez [Planification de la sélection des certificats clients PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForClientCertificateSelection).  

    - **Les clients vérifient la liste de révocation des certificats (CRL) pour les systèmes de site** : activez ce paramètre pour que les clients vérifient les certificats révoqués dans la liste de révocation des certificats de votre organisation.  

    Pour plus d’informations sur la vérification de la liste de révocation de certificats pour les clients, consultez [Planification de la révocation de certificats PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).  

5.  Pour importer, afficher et supprimer les certificats des autorités de certification racine approuvées, choisissez **Définir**.  

    Pour plus d’informations, consultez [Planification des certificats racine approuvés PKI et de la liste des émetteurs de certificats](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRootCAs).  


Répétez cette procédure pour tous les sites principaux de la hiérarchie.  



##  <a name="BKMK_ConfigureSigningEncryption"></a> Configurer la signature et le chiffrement  

Configurez les paramètres de signature et de chiffrement les plus sécurisés pour les systèmes de site pris en charge par tous les clients du site. Ces paramètres sont particulièrement importants lorsque vous permettez aux clients de communiquer avec les systèmes de site à l'aide de certificats auto-signés via HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Pour configurer la signature et le chiffrement pour un site  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site principal à configurer.  

2.  Dans le ruban, sélectionnez **Propriétés**, puis passez à l’onglet **Signature et chiffrement**.  

    Cet onglet est disponible uniquement sur un site principal. Si vous ne voyez pas l’onglet **Signature et chiffrement**, vérifiez que vous n’êtes pas connecté à un site d’administration centrale ni à un site secondaire.  

3.  Configurez les options de signature et de chiffrement pour la communication des clients avec le site.  

    - **Exiger la signature** : les clients signent les données avant de les envoyer au point de gestion.  

    - **Exiger SHA-256** : les clients utilisent l’algorithme SHA-256 pour signer les données.  

    > [!WARNING]  
    >  N’activez pas **Exiger SHA-256** sans d’abord vérifier que tous les clients prennent en charge cet algorithme de hachage. Ces clients incluent ceux qui peuvent être affectés au site dans le futur.  
    >   
    >  Si vous choisissez cette option et que des clients avec des certificats auto-signés ne prennent pas en charge SHA-256, Configuration Manager les rejette. Le composant SMS_MP_CONTROL_MANAGER consigne l’ID de message 5443.  

    - **Utiliser le chiffrement** : les clients chiffrent les données d’inventaire et les messages d’état du client avant l’envoi au point de gestion. Ils utilisent l’algorithme 3DES.  

Répétez cette procédure pour tous les sites principaux de la hiérarchie.  



##  <a name="BKMK_ConfigureRBA"></a> Configurer l’administration basée sur des rôles  

L'administration basée sur des rôles combine des rôles de sécurité, des étendues de sécurité et des regroupements attribués pour définir l'étendue administrative de chaque utilisateur administratif. Une étendue inclut les objets qu’un utilisateur peut voir dans la console et les tâches associées à ces objets que cet utilisateur est autorisé à effectuer. Les configurations d'administration basée sur des rôles s'appliquent à chaque site dans une hiérarchie.  

Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration). Cet article détaille les actions suivantes :  

- Créer des rôles de sécurité personnalisés  

- Configurer des rôles de sécurité  

- Configurer des étendues de sécurité pour un objet  

- Configurer des regroupements pour gérer la sécurité  

- Créer un utilisateur administratif  

- Modifier l’étendue administrative d’un utilisateur administratif  

> [!IMPORTANT]  
>  Votre propre étendue administrative définit les objets et les paramètres que vous pouvez attribuer lorsque vous configurez une administration basée sur des rôles pour un autre utilisateur administratif. Pour plus d’informations sur la planification de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).  



##  <a name="BKMK_ManageAccounts"></a> Gérer les comptes utilisés par Configuration Manager  

Configuration Manager prend en charge les comptes Windows pour de nombreuses tâches et utilisations différentes. Pour voir les comptes qui sont configurés pour différentes tâches et pour gérer le mot de passe utilisé par Configuration Manager pour chaque compte, effectuez la procédure suivante :  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>Pour gérer les comptes utilisés par Configuration Manager  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Sécurité**, puis choisissez le nœud **Comptes**.  

2.  Pour changer le mot de passe d’un compte, sélectionnez le compte dans la liste. Ensuite, dans le ruban, choisissez **Propriétés**.  

3.  Choisissez **Définir** pour ouvrir la boîte de dialogue **Compte d’utilisateur Windows**. Spécifiez le nouveau mot de passe de Configuration Manager à utiliser pour ce compte.  

    > [!NOTE]  
    >  Le mot de passe que vous spécifiez doit correspondre au mot de passe de ce compte dans Active Directory.  

Pour plus d’informations, consultez [Comptes utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).



##  <a name="bkmk_azuread"></a> Configurer Azure Active Directory

Intégrez Configuration Manager à Azure Active Directory (Azure AD) pour simplifier et activer votre environnement pour le cloud. Permettez au site et aux clients de s’authentifier avec Azure AD. Pour plus d’informations, reportez-vous au service **Gestion cloud** dans [Configurer les services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).



## <a name="bkmk_auth"></a> Configurer l’authentification du fournisseur SMS

Depuis la version 1810, vous pouvez spécifier le niveau d’authentification minimal pour les administrateurs qui accèdent aux sites Configuration Manager. Cette fonctionnalité force les administrateurs à se connecter à Windows avec le niveau requis. Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Voir aussi

- [Planifier la sécurité](/sccm/core/plan-design/security/plan-for-security)  

- [Sécurité et confidentialité pour les clients Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Communications entre points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Informations techniques de référence sur les contrôles de chiffrement](/sccm/core/plan-design/security/cryptographic-controls-tehnical-reference)  

- [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements)  
