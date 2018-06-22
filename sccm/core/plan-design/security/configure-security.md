---
title: Configurer la sécurité
titleSuffix: Configuration Manager
description: Configurez les options de sécurité pour System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 165f7fc0b73e288ac1718def96a50bc91a181cc2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339075"
---
# <a name="configure-security-in-system-center-configuration-manager"></a>Configurer la sécurité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cet article pour configurer les options de sécurité pour System Center Configuration Manager.  

##  <a name="BKMK_ConfigureClientPKI"></a> Configurer les paramètres de certificat client PKI  
Si vous souhaitez utiliser des certificats PKI (infrastructure à clés publiques) pour les connexions client aux systèmes de site utilisant les services IIS (Internet Information Services), la procédure suivante vous permet de configurer les paramètres pour ces certificats.  

#### <a name="to-configure-client-pki-certificate-settings"></a>Pour configurer des paramètres de certificat client PKI  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Configuration du site**, choisissez **Sites**, puis le site principal à configurer.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**, puis l’onglet **Communication de l’ordinateur client**.  

    Cet onglet est disponible uniquement sur un site principal. Si vous ne voyez pas l'onglet **Communication de l'ordinateur client** , vérifiez que vous n'êtes pas connecté à un site d'administration centrale ni à un site secondaire.  

4.  Choisissez **HTTPS uniquement** quand vous voulez que les clients attribués au site utilisent toujours un certificat client PKI pour se connecter aux systèmes de site qui utilisent IIS. Sinon, choisissez **HTTPS ou HTTP** quand vous n’avez pas besoin que les clients utilisent des certificats PKI.  

5.  Si vous avez choisi **HTTPS ou HTTP**, choisissez **Utiliser le certificat client PKI (fonctionnalité d’authentification client) si possible** quand vous voulez utiliser un certificat client PKI pour des connexions HTTP. Le client utilise ce certificat au lieu d'un certificat auto-signé pour s'authentifier auprès des systèmes de site. Cette option est automatiquement sélectionnée si vous choisissez **HTTPS uniquement**.  

    Lorsque des clients sont détectés sur Internet ou qu'ils sont configurés pour la gestion des clients Internet uniquement, ils utilisent toujours un certificat client PKI.  

6.  Choisissez **Modifier** pour configurer votre méthode de sélection de client quand plusieurs certificats clients PKI valides sont disponibles sur un client, puis choisissez **OK**.  

    Pour plus d’informations sur la méthode de sélection des certificats clients, consultez [Planification de la sélection des certificats clients PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

7.  Activez ou désactivez la case à cocher pour permettre aux clients de vérifier la liste de révocation de certificats.  

    Pour plus d’informations sur la vérification de la liste de révocation de certificats pour les clients, consultez [Planification de la révocation de certificats PKI](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

8.  Si vous devez spécifier des certificats d’autorité de certification racine approuvés pour les clients, choisissez **Définir**, importez les fichiers de certificat d’autorité de certification racine, puis choisissez **OK**.  

    Pour plus d’informations sur ce paramètre, consultez [Planification des certificats racines approuvés PKI et de la liste des émetteurs de certificats](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRootCAs).  

9. Choisissez **OK** pour fermer la boîte de dialogue des propriétés du site.  

Répétez cette procédure pour tous les sites principaux de la hiérarchie.  

##  <a name="BKMK_ConfigureSigningEncryption"></a> Configurer la signature et le chiffrement  
Configurez les paramètres de signature et de chiffrement les plus sécurisés pour les systèmes de site pris en charge par tous les clients du site. Ces paramètres sont particulièrement importants lorsque vous permettez aux clients de communiquer avec les systèmes de site à l'aide de certificats auto-signés via HTTP.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>Pour configurer la signature et le chiffrement pour un site  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Configuration du site**, choisissez **Sites**, puis le site principal à configurer.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**, puis l’onglet **Signature et chiffrement**.  

    Cet onglet est disponible uniquement sur un site principal. Si vous ne voyez pas l'onglet **Signature et chiffrement** , vérifiez que vous n'êtes pas connecté à un site d'administration centrale ni à un site secondaire.  

4.  Configurez les options de signature et de chiffrement de votre choix, puis choisissez **OK**.  

    > [!WARNING]  
    >  Ne choisissez pas l’option **Demander SHA-256** sans vérifier d’abord que tous les clients susceptibles d’être attribués au site peuvent prendre en charge l’algorithme de hachage ou qu’ils disposent d’un certificat d’authentification client PKI valide. Vous devrez peut-être installer des mises à jour ou des correctifs logiciels sur les clients pour prendre en charge SHA-256. Par exemple, les ordinateurs qui exécutent Windows Server 2003 SP2 doivent installer un correctif qui est référencé dans [l'article 938397 de la Base de connaissances Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226666).  
    >   
    >  Si vous choisissez cette option pour des clients qui ne prennent pas en charge SHA-256 et qui utilisent des certificats auto-signés, Configuration Manager rejette ces clients. Dans ce scénario, le composant SMS_MP_CONTROL_MANAGER enregistre l'ID de message 5443.  

5.  Choisissez **OK** pour fermer la boîte de dialogue **Propriétés** du site.  

Répétez cette procédure pour tous les sites principaux de la hiérarchie.  

##  <a name="BKMK_ConfigureRBA"></a> Configurer l’administration basée sur des rôles  
L'administration basée sur des rôles combine des rôles de sécurité, des étendues de sécurité et des regroupements attribués pour définir l'étendue administrative de chaque utilisateur administratif. L’étendue administrative inclut les objets qu’un utilisateur administratif peut afficher dans la console Configuration Manager et les tâches associées à ces objets que cet utilisateur est autorisé à exécuter. Les configurations d'administration basée sur des rôles s'appliquent à chaque site dans une hiérarchie.  

Les liens suivants renvoient vers les sections correspondantes de l’article [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md) :  

-   [Créer des rôles de sécurité personnalisés](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)  

-   [Configurer des rôles de sécurité](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole)  

-   [Configurer des étendues de sécurité pour un objet](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope)  

-   [Configurer des regroupements pour gérer la sécurité](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl)  

-   [Créer un utilisateur administratif](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_Create_AdminUser)  

-   [Modifier l’étendue administrative d’un utilisateur administratif](../../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)  

> [!IMPORTANT]  
>  Votre propre étendue administrative définit les objets et les paramètres que vous pouvez attribuer lorsque vous configurez une administration basée sur des rôles pour un autre utilisateur administratif. Pour plus d’informations sur la planification de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  

##  <a name="BKMK_ManageAccounts"></a> Gérer les comptes utilisés par Configuration Manager  
Configuration Manager prend en charge les comptes Windows pour de nombreuses tâches et utilisations différentes.  

Utilisez la procédure suivante pour afficher les comptes qui sont configurés pour différentes tâches et pour gérer le mot de passe utilisé par Configuration Manager pour chaque compte.  

#### <a name="to-manage-accounts-that-are-used-by-configuration-manager"></a>Pour gérer les comptes utilisés par Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Comptes** pour afficher les comptes qui sont configurés pour Configuration Manager.  

3.  Pour modifier le mot de passe d’un compte qui est configuré pour Configuration Manager, choisissez le compte.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Choisissez **Définir** pour ouvrir la boîte de dialogue **Compte d’utilisateur Windows**, puis spécifiez le nouveau mot de passe que Configuration Manager doit utiliser pour ce compte.  

    > [!NOTE]  
    >  Le mot de passe que vous spécifiez doit correspondre au mot de passe spécifié pour le compte dans Utilisateurs et ordinateurs Active Directory.  

6.  Choisissez **OK** pour terminer la procédure.  
