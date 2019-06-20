---
title: Tutoriel &#58; Activer la cogestion pour les clients Configuration Manager existants
titleSuffix: Configuration Manager
description: Configurez la cogestion avec Microsoft Intune si vous gérez déjà des appareils Windows 10 avec Configuration Manager.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b19f54d60ed0594be4a51b5abcef69304a27ece
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834761"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutoriel : Activer la cogestion pour les clients Configuration Manager existants
Avec la cogestion, vous pouvez conserver vos processus établis d’utilisation de Configuration Manager pour gérer des PC dans votre organisation, tout en investissant dans le cloud en recourant à Intune pour la sécurité et l’approvisionnement moderne.  

Ce tutoriel explique comment configurer la cogestion pour des appareils Windows 10 déjà inscrits dans Configuration Manager. Il part du principe que vous utilisez déjà Configuration Manager pour gérer vos appareils Windows 10.

Suivez ce tutoriel si :  

- Vous disposez d’Active Directory en local, que vous pouvez connecter à Azure Active Directory (Azure AD) dans une configuration Azure AD Hybride. 

  Si vous ne pouvez pas déployer de configuration Azure Active Directory (AD) Hybride en joignant AD en local avec Azure AD, nous vous recommandons de suivre notre tutoriel d’accompagnement [Activer la cogestion pour les nouveaux appareils Windows 10 basés sur Internet](/sccm/comanage/tutorial-co-manage-new-devices). 
- Vous disposez de clients Configuration Manager que vous souhaitez relier au cloud.


**Ce tutoriel comporte plusieurs volets :**  
> [!div class="checklist"]  
> * Passer en revue les prérequis de l’environnement Azure et de l’environnement local  
> * Configurer Azure AD hybride  
> * Configurer les agents clients Configuration Manager de sorte qu’ils s’inscrivent auprès d’Azure AD  
> * Configurer l’inscription automatique des appareils dans Intune  
> * Attribuer des licences Intune aux utilisateurs  
> * Activer la cogestion dans Configuration Manager  


## <a name="prerequisites"></a>Prérequis  

### <a name="azure-services-and-environment"></a>Services et environnement Azure
- Abonnement Azure ([essai gratuit](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Abonnement Microsoft Intune
  > [!TIP]  
  > Un abonnement Enterprise Mobility + Security (EMS) comprend à la fois Azure Active Directory Premium et Microsoft Intune. Abonnement EMS ([essai gratuit](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Au cours de ce tutoriel, vous allez effectuer les opérations suivantes si ce n’est pas déjà fait dans votre environnement :
- Attribuer aux utilisateurs une licence *Intune* et *Azure Active Directory Premium*
- Configurer [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre Active Directory en local et le locataire Azure Active Directory (AD)


### <a name="on-premises-infrastructure"></a>Infrastructure locale
- Une [version prise en charge](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) de System Center Configuration Manager Current Branch
- [L’autorité MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) définie sur Intune  


### <a name="permissions"></a>Autorisations
Tout au long de ce tutoriel, utilisez les autorisations suivantes pour effectuer les tâches :  
- Un compte *administrateur général* dans Azure  
- Un compte *administrateur de domaine* dans l’infrastructure locale  
- Un compte *administrateur complet* pour *toutes* les étendues dans Configuration Manager   

## <a name="set-up-hybrid-azure-ad"></a>Configurer Azure AD hybride
Configurer une infrastructure Azure AD Hybride, c’est véritablement configurer l’intégration d’AD en local avec Azure AD à l’aide d’Azure AD Connect et des services de fédération Active Directory (AD FS). Une fois la configuration effectuée, les collaborateurs peuvent se connecter en toute transparence à des systèmes externes avec leurs informations d’identification AD local.

> [!IMPORTANT]  
> Ce tutoriel décrit en détail un processus simple permettant de configurer une infrastructure Azure AD Hybride pour un domaine managé. Nous vous recommandons de vous familiariser avec cette procédure afin de ne pas dépendre de ce tutoriel pour comprendre et déployer l’infrastructure Azure AD Hybride.
>
> Pour plus d’informations sur Azure AD Hybride, commencez par les articles suivants dans la documentation Azure Active Directory :
> - [Planifier une implémentation de jonction Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Planifier une implémentation de jonction Azure AD Hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Contrôler la jonction Azure AD Hybride d’appareils](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurer la jonction Azure AD Hybride pour les domaines fédérés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurer Azure AD Connect  
Azure AD Hybride exige de configurer Azure AD Connect de façon à synchroniser les comptes d’ordinateurs d’Active Directory (AD) en local et l’objet appareil d’Azure AD.

Depuis la version 1.1.819.0, Azure AD Connect propose un Assistant permettant de configurer une jonction Azure AD Hybride en simplifiant le processus.  

Pour configurer Azure AD Connect, vous avez besoin d’informations d’identification d’administrateur général sur votre locataire Azure AD.  

> [!TIP]  
> La procédure suivante ne doit pas être considérée comme faisant autorité pour la configuration d’Azure AD Connect. Sa vocation est de simplifier la configuration de la cogestion entre Intune et Configuration Manager. Pour accéder au contenu de référence à ce sujet et aux procédures de configuration d’Azure AD associées, voir [Configurer une jonction Azure AD Hybride pour les domaines managés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) dans la documentation d’Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurer une jonction Azure AD Hybride avec Azure AD Connect

1. Récupérez et installez la [dernière version d’Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 ou version ultérieure).  
2. Lancez Azure AD Connect, puis sélectionnez **Configurer**.
3. Sur la page **Tâches supplémentaires**, sélectionnez **Configurer les options de l’appareil**, puis **Suivant**.
4. Sur la page **Vue d’ensemble**, sélectionnez **Suivant**.
5. Sur la page **Se connecter à Azure AD**, entrez des informations d’identification d’administrateur général pour votre locataire Azure AD.
6. Sur la page **Options de l’appareil**, sélectionnez **Configurer la jonction Azure AD Hybride**, puis **Suivant**.
7. Sur la page **Systèmes d’exploitation des appareils**, sélectionnez les systèmes d’exploitation utilisés par les appareils de votre environnement Active Directory, puis **Suivant**.  

   Vous pouvez sélectionner l’option permettant de prendre en charge les appareils Windows joints à un domaine de bas niveau. Cependant, n’oubliez pas que la cogestion des appareils n’est prise en charge que pour Windows 10.
8. Sur la page **SCP**, pour chaque forêt locale sur laquelle vous souhaitez qu’Azure AD Connect configure le point de connexion de service (SCP), suivez les étapes ci-dessous, puis sélectionnez **Suivant** :  
   1. Sélectionnez la forêt.  
   2. Sélectionnez le service d’authentification.  Si vous disposez d’un domaine fédéré, sélectionnez le serveur AD FS, sauf si votre organisation comporte exclusivement des clients Windows 10 et que vous avez configuré la synchronisation ordinateur/appareil ou que votre organisation utilise [l’authentification unique transparente](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Cliquez sur **Ajouter** pour entrer les informations d’identification d’administrateur d’entreprise.  
9. Si vous disposez d’un domaine managé, ignorez cette étape.  

   Sur la page **Configuration de la fédération**, entrez les informations d’identification de votre administrateur AD FS, puis sélectionnez **Suivant**.
10. Sur la page **Prêt à configurer**, sélectionnez **Configurer**.
11. Sur la page **Configuration effectuée**, sélectionnez **Quitter**.

En cas de problèmes avec la jonction Azure AD Hybride pour les appareils Windows joints à un domaine, voir [Résolution des problèmes de jonction Azure AD Hybride pour les appareils Windows actuels](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Configurer les paramètres client de façon à conduire les clients à s’inscrire auprès d’Azure AD  
Utilisez les paramètres client pour configurer les clients Configuration Manager de sorte qu’ils s’inscrivent automatiquement auprès d’Azure AD.  

1. Ouvrez la **Console Configuration Manager** > **Administration** > **Vue d’ensemble** > **Paramètres client**, puis modifiez **Paramètres client par défaut**.  

2. Sélectionnez **Services cloud**.  

3. Sur la page **Paramètres par défaut**, définissez **Inscrire automatiquement les nouveaux appareils Windows 10 joints à un domaine auprès d’Azure Active Directory** sur **Oui**.  

4. Sélectionnez **OK** pour enregistrer cette configuration.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurer l’inscription automatique des appareils à Intune   
Configurons maintenant l’inscription automatique des appareils auprès d’Intune. Ainsi, les appareils gérés avec Configuration Manager s’inscriront automatiquement à Intune.

L’inscription automatique permet également aux utilisateurs d’inscrire leurs appareils Windows 10 à Intune. Elle se produit lorsqu’ils ajoutent leur compte professionnel à leurs appareils personnels, ou quand un appareil d’entreprise est joint à Azure Active Directory.  

1. Connectez-vous au [Portail Azure](https://portal.azure.com/) et sélectionnez **Azure Active Directory** > **Mobilité (MDM et MAM)**  > **Microsoft Intune**.  

2. Configurez **Portée des utilisateurs MDM**. Spécifiez l’une des valeurs suivantes pour indiquer quels appareils des utilisateurs sont gérés par Microsoft Intune et accepter les valeurs d’URL par défaut.  

   - **Une partie** : sélectionnez les **Groupes** qui peuvent inscrire automatiquement leurs appareils Windows 10.  

   - **Tous** : tous les utilisateurs peuvent inscrire automatiquement leurs appareils Windows 10. Si la valeur est **Aucun**, l’inscription automatique à la gestion des appareils mobiles (MDM) est désactivée.

   > [!IMPORTANT]  
   > Si la **Portée des utilisateurs MAM** et l’inscription MDM automatique (**Portée des utilisateurs MDM**) sont toutes deux activées pour un groupe, seule la gestion des applications mobiles (MAM) est activée et ajoutée pour les utilisateurs de ce groupe lorsqu’ils joignent leur appareil personnel à leur lieu de travail. Les appareils ne sont pas inscrits automatiquement à la gestion MDM.  

3. Sélectionnez **Enregistrer** pour terminer la configuration de l’inscription automatique.  

4. Revenez à **Mobilité (MDM et MAM)** , puis sélectionnez **Inscription à Microsoft Intune**.  

5. Pour Portée des utilisateurs MDM, sélectionnez **Tous**, puis **Enregistrer**.  


## <a name="assign-intune-licenses-to-users"></a>Attribuer des licences Intune aux utilisateurs   
Il est essentiel, quoique souvent négligé, d’attribuer une licence Intune à chacun des utilisateurs qui utiliseront un appareil cogéré.  

Pour attribuer des licences à des groupes d’utilisateurs, utilisez Azure Active Directory.  

1. Connectez-vous au [portail Azure](https://portal.azure.com/) avec un compte Administrateur. Pour gérer les licences, il doit avoir le rôle Administrateur général ou Administrateur de compte d’utilisateur.  

2. Sélectionnez **Tous les services** dans le volet de navigation gauche, puis **Azure Active Directory**.  

3. Sur le volet **Azure Active Directory**, sélectionnez **Licences** pour ouvrir un volet permettant de voir et de gérer tous les produits sous licence du locataire.  

4. Sous **Tous les produits**, sélectionnez votre option de produit qui comporte la licence Intune, puis **Attribuer** en haut du volet.  

   Par exemple, vous pouvez sélectionner **Enterprise Mobility + Security E5** si c’est ainsi que vous avez obtenu Intune.  

5. Sur le volet **Attribuer une licence**, cliquez sur **Utilisateurs et groupes** pour ouvrir le volet **Utilisateurs et groupes**. Sélectionnez les groupes et les différents utilisateurs auxquels vous souhaitez attribuer une licence.  Ensuite, cliquez sur **Sélectionner** en bas du volet pour confirmer cette sélection.  

6. Sur le volet **Attribuer une licence**, cliquez sur **Options d’attribution** pour afficher tous les plans de services inclus dans le produit sélectionné. Si vous avez choisi un produit unique comme Intune, seul ce produit s’affiche.  
   - Définissez **Microsoft Intune** sur **Actif**.  
   - Attribuez à chaque utilisateur une licence pour **Azure Active Directory Premium**.  

   Une fois les licences applicables attribuées, sélectionnez **OK**.  

7. Pour terminer l’attribution, cliquez sur **Attribuer** en bas du volet **Attribuer une licence**.

8. En haut à droite, une notification présente l’état et le résultat du processus. Si l’attribution au groupe n’a pas abouti (par exemple, en présence de licences préexistantes dans le groupe), cliquez sur la notification pour afficher les détails de l’échec.

Pour plus d’informations sur l’attribution de licences Intune aux utilisateurs, voir [Attribuer des licences](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Activer la cogestion dans Configuration Manager
Maintenant qu’Azure AD Hybride est configuré, que les configurations du client Configuration Manager sont en place et que les licences de produit ont été attribuées aux utilisateurs, activons la cogestion des appareils Windows 10.  

> [!TIP]  
>  À l’étape six de la procédure suivante, nous allons désigner un regroupement comme *Groupe pilote* pour la cogestion. Il s’agit d’un groupe qui contient un petit nombre de clients permettant de tester les configurations de cogestion. Nous recommandons de créer un regroupement adapté avant de commencer la procédure. Vous pourrez alors le sélectionner sans avoir à quitter la procédure.  

1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.

2. Dans le groupe Gérer sous l’onglet Accueil, sélectionnez **Configurer la cogestion** pour ouvrir l’Assistant Configuration de la cogestion.

3. Sur la page Abonnement, sélectionnez **Se connecter** et connectez-vous à votre locataire Intune, puis sélectionnez **Suivant**.

4. Sur la page Activation, sélectionnez l’une des options suivantes dans la liste déroulante *Inscription automatique dans Intune* :  

   - **Pilote**  -  *(recommandé)* Membres du regroupement qui seront automatiquement inscrits dans Intune et pourront alors être cogérés. Spécifiez le regroupement pilote sur la page *Gestion intermédiaire* de cet Assistant. Cette option permet de tester la cogestion sur un sous-ensemble de clients. Vous pourrez ensuite déployer la cogestion auprès de clients supplémentaires suivant une approche progressive.  

   - **Tous** – Cogestion activée pour tous les clients.  

5. Sur la page Charges de travail, vous pouvez basculer les charges de travail de **Configuration Manager** vers l’une des options suivantes ; ensuite, sélectionnez **Suivant** pour continuer.  

   - **Pilote Intune** – Bascule la charge de travail uniquement pour les appareils du groupe pilote. Un regroupement sera désigné comme groupe pilote sur la page suivante de l’Assistant.  

   - **Intune** – Bascule la charge de travail associée pour tous les appareils Windows 10 cogérés.  

   Il n’est pas nécessaire de basculer des charges de travail dès l’activation de la cogestion. Vous pourrez revenir consulter cette configuration plus tard à partir de la console Configuration Manager, après avoir configuré la cogestion.  

   Avant de basculer une charge de travail, vérifiez que la charge de travail correspondante dans Intune est correctement configurée et déployée. Ainsi, les charges de travail resteront gérées.  

6. Sur la page Gestion intermédiaire, spécifiez le regroupement à utiliser comme **Regroupement pilote**, puis cliquez sur **Suivant**. Il sera utilisé dans le cadre du déploiement progressif de la cogestion. À tout moment, vous pouvez modifier les regroupements dans le groupe pilote à partir des propriétés de cogestion.  

7. Sur la page Résumé, sélectionnez **Suivant**, puis **Fermer** pour terminer l’Assistant.  


## <a name="next-steps"></a>Étapes suivantes
- Passez en revue l’état des appareils cogérés avec le [Tableau de bord de cogestion](/sccm/comanage/how-to-monitor)
- Commencez à tirer une [valeur ajoutée immédiate](quickstarts.md#immediate-value) de la cogestion
- Utilisez [l’accès conditionnel](quickstart-conditional-access.md) et les règles de conformité Intune pour gérer l’accès utilisateur aux ressources de l’entreprise
