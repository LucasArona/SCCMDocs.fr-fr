---
title: Didacticiel&#58; chemin d’accès de la cogestion 1
titleSuffix: Configuration Manager
description: Configurer la cogestion avec Microsoft Intune quand vous gérez déjà les appareils Windows 10 avec Configuration Manager.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: brenduns
ms.author: brenduns
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1aecb2c33c874717f1da979f1316d1b46b785071
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754872"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Didacticiel : Activer la cogestion pour les clients Configuration Manager existants
Avec la cogestion, vous pouvez conserver votre processus établis pour l’utilisation de Configuration Manager pour gérer des PC dans votre organisation. En même temps, vous êtes investit dans le cloud à l’aide d’Intune pour la sécurité et l’approvisionnement moderne.  

Dans ce didacticiel, vous avez configurer cogestion de vos appareils Windows 10 qui sont déjà inscrits dans Configuration Manager. Ce didacticiel commence par du principe que vous utilisez déjà Configuration Manager pour gérer vos appareils Windows 10.

Utilisez ce didacticiel lorsque :  

- Vous avez une sur site Active Directory que vous pouvez vous connecter à Azure Active Directory (Azure AD) dans une configuration hybride Azure AD
- Vous avez des clients Configuration Manager existants que vous souhaitez attacher de cloud


**Dans ce didacticiel, vous allez :**  
> [!div class="checklist"]  
> * Passez en revue les conditions préalables pour Azure et votre environnement local  
> * Configurer Azure AD hybride  
> * Configurer les agents du client Configuration Manager auprès d’Azure AD  
> * Configurer Intune pour l’inscription automatique des appareils  
> * Attribuer des licences Intune aux utilisateurs  
> * Activer la cogestion dans Configuration Manager  


## <a name="prerequisites"></a>Prérequis  

### <a name="azure-services-and-environment"></a>Environnement et les services azure
- Abonnement Azure ([version d’évaluation gratuite](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Abonnement Microsoft Intune
  > [!TIP]  
  > Une à Enterprise Mobility + Security (EMS) abonnement inclut Azure Active Directory Premium et Microsoft Intune. Abonnement EMS ([version d’évaluation gratuite](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Si elle est déjà présent dans votre environnement, au cours de ce didacticiel, vous allez :
- Affecter une licence pour des utilisateurs *Intune* et pour *Azure Active Directory Premium*
- Configurer [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre votre annuaire local Active Directory et votre Azure Active Directory (AD) du client


### <a name="on-premises-infrastructure"></a>Infrastructure locale
- Un [version prise en charge](https://docs.microsoft.com/sccm/core/servers/manage/updates#supported-versions) de current branch de System Center Configuration Manager
- Le [autorité MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) doit être définie sur Intune  


### <a name="permissions"></a>Autorisations
Tout au long de ce didacticiel, utilisez les autorisations suivantes pour effectuer des tâches :  
- Un compte qui est un *administrateur général* dans Azure  
- Un compte qui est un *administrateur de domaine* sur votre infrastructure locale  
- Un compte qui est un *administrateur complet* pour *tous les* étendues dans le Gestionnaire de Configuration   

## <a name="set-up-hybrid-azure-ad"></a>Configurer Azure AD hybride
Lorsque vous configurez un hybride Azure AD, que vous configurez vraiment à l’intégration d’un site Active Directory avec Azure AD à l’aide d’Azure AD Connect et Active Directory Federated Services (ADFS). Avec une configuration réussie, vos employés peuvent se connecter en toute transparence des systèmes externes à l’aide de leur site informations d’identification AD.

> [!IMPORTANT]  
> Ce didacticiel décrit en détail un processus simple pour configurer hybride Azure AD pour un domaine géré. Nous vous recommandons de vous être familiarisé avec le processus et vous basez pas sur ce didacticiel vous permettront de comprendre et de déploiement hybride d’Azure AD.
>
> Pour plus d’informations sur Azure AD hybride, commencez par les articles suivants dans la documentation Azure Active Directory :
> - [Planifier votre implémentation de la jointure Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)
> -  [Planifier votre implémentation de jointure Azure AD hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)
> -  [Contrôler la jonction hybride Azure AD de vos appareils](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-control)
> -  [Configurer hybride Azure AD join pour les domaines fédérés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  


### <a name="set-up-azure-ad-connect"></a>Configurer Azure AD Connect  
Azure AD hybride nécessite la configuration d’Azure AD Connect pour synchroniser les comptes d’ordinateurs dans votre local Active Directory (AD) et l’objet appareil dans Azure AD.

Depuis la version 1.1.819.0, Azure AD Connect vous offre un Assistant pour configurer une jointure hybrid Azure AD. Utilisation de cet Assistant simplifie le processus de configuration.  

Pour configurer Azure AD Connect, vous avez besoin d’informations d’identification d’un administrateur général pour votre client Azure AD.  

> [!TIP]  
> La procédure suivante ne doit pas être considérée faisant autoritée afin de configurer d’Azure AD Connect, mais est fournie ici pour aider à simplifier la configuration de la cogestion entre Intune et Configuration Manager. Pour le contenu faisant autorité sur ce et les procédures associées afin de configurer Azure AD, consultez [configurer une jointure hybrid Azure AD pour les domaines managés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains) dans la documentation d’Azure AD.  


#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configurer une jonction d’Azure AD hybride à l’aide d’Azure AD Connect

1. Obtenir et installer le [version la plus récente d’Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 ou une version ultérieure).  
2. Lancez Azure AD Connect, puis sélectionnez **configurer**.
3. Sur le **des tâches supplémentaires** page, sélectionnez **configurer les options de l’appareil**, puis sélectionnez **suivant**.
4. Sur le **vue d’ensemble** page, sélectionnez **suivant**.
5. Sur le **se connecter à Azure AD** , entrez les informations d’identification d’un administrateur général pour votre locataire Azure AD.
6. Sur le **options de l’appareil** page, sélectionnez **jonction hybride de configurer Azure AD**, puis sélectionnez **suivant**.
7. Sur le **SCP** page, pour chaque forêt locale souhaité d’Azure AD Connect pour configurer le point de connexion de service (SCP), procédez comme suit, puis sélectionnez **suivant**:  
   1. Sélectionnez la forêt.  
   2. Sélectionnez le service d’authentification.  Si vous avez un domaine fédéré, sélectionnez un serveur AD FS, sauf si votre organisation a exclusivement les clients Windows 10 et vous avez configuré la synchronisation de l’ordinateur/appareil ou à l’aide de votre organisation [SeamlessSSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Cliquez sur **ajouter** à entrer les informations d’identification d’administrateur entreprise.  
8. Sur le **systèmes d’exploitation de périphérique** page, sélectionnez les systèmes d’exploitation utilisés par les appareils dans votre environnement Active Directory, puis **suivant**.  

   Vous pouvez sélectionner l’option permettant de prendre en charge les appareils Windows de bas niveau joints à un domaine, mais n’oubliez pas que cogestion des appareils est uniquement prise en charge pour Windows 10.

9. Si vous avez un domaine géré, ignorez cette étape.  

   Sur le **configuration de fédération** page, entrez les informations d’identification de l’administrateur AD FS, puis sélectionnez **suivant**.
10. Sur le **prêt à configurer** page, sélectionnez **configurer**.
11. Sur le **d’effectuer la Configuration** page, sélectionnez **Exit**.

Si vous rencontrez des problèmes avec Azure AD hybride à la fin jointure de domaine joint les appareils Windows, consultez [jonction hybride Azure AD de résolution des problèmes pour les appareils Windows actuels](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).


## <a name="configure-client-settings-to-direct-clients-register-with-azure-ad"></a>Configurer les paramètres Client pour diriger les clients s’inscrivent auprès d’Azure AD  
Utilisez les paramètres Client pour configurer les clients Configuration Manager pour inscrire automatiquement auprès d’Azure AD.  

1. Ouvrez le **console Configuration Manager** > **Administration** > **vue d’ensemble** > **paramètres Client** , puis modifiez le **paramètres Client par défaut**.  

2. Sélectionnez **Services Cloud**.  

3. Sur le **paramètres par défaut** , définissez **inscrire automatiquement les nouveaux appareils joints à un domaine de Windows 10 avec Azure Active Directory** à = **Oui**.  

4. Sélectionnez **OK** pour enregistrer cette configuration.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configurer l’inscription automatique des appareils à Intune   
Ensuite, nous allons configurer l’inscription automatique des appareils avec Intune. Avec l’inscription automatique, les appareils que vous gérez avec Configuration Manager automatiquement s’inscrire à Intune.

L’inscription automatique permet également aux utilisateurs d’inscrire leurs appareils Windows 10 à Intune. Les appareils inscrits lorsqu’un utilisateur ajoute son compte professionnel à leurs appareils personnels, ou quand un appareil d’entreprise est joint à Azure Active Directory.  

1. Se connecter à la [Azure portal](https://portal.azure.com/) et sélectionnez **Azure Active Directory** > **mobilité (MDM et MAM)** > **Microsoft Intune** .  

2. Configurer **portée d’utilisateur de gestion des appareils mobiles**. Spécifiez les valeurs suivantes pour configurer les appareils des utilisateurs qui sont gérés par Microsoft Intune et accepter les valeurs par défaut pour les valeurs d’URL.  

   - **Certains** : sélectionnez le **groupes** qui peuvent s’inscrire automatiquement leurs appareils Windows 10  

   - **Tous les** -tous les utilisateurs peuvent s’inscrire automatiquement leurs appareils Windows 10 lorsque la valeur **aucun**, l’inscription automatique de gestion des appareils mobiles (MDM) est désactivée.

   > [!IMPORTANT]  
   > Si les deux **étendue des utilisateurs MAM** et l’inscription MDM automatique (**portée d’utilisateur de gestion des appareils mobiles**) sont activés pour un groupe, GAM uniquement est activée. Uniquement Mobile Application Management (MAM) est ajoutée pour les utilisateurs de ce groupe lorsqu’ils workplace joignent leur appareil personnel. Les appareils ne sont pas automatiquement inscrits à MDM.  

3. Sélectionnez **enregistrer** pour terminer la configuration de l’inscription automatique.  

4. Retour à **mobilité (MDM et MAM)** , puis sélectionnez **inscription à Microsoft Intune**.  

5. Pour une étendue d’utilisateur de gestion des appareils mobiles, sélectionnez **tous les**, puis **enregistrer**.  


## <a name="assign-intune-licenses-to-users"></a>Attribuer des licences Intune aux utilisateurs   
Une action souvent négligée mais critique consiste à attribuer une licence Intune à chaque utilisateur qui utilisera un appareil est cogéré.  

Pour attribuer des licences à des groupes d’utilisateurs, utilisez Azure Active Directory.  

1. Se connecter à la [Azure portal](https://portal.azure.com/) avec un compte d’administrateur. Pour gérer les licences, le compte doit être un administrateur de compte d’utilisateur ou un rôle de l’administrateur général.  

2. Sélectionnez **tous les services** dans le volet de navigation gauche, puis sélectionnez **Azure Active Directory**.  

3. Sur le **Azure Active Directory** volet, sélectionnez **licences** pour ouvrir un volet où vous pouvez voir et gérer tous les produits sous licence dans le locataire.  

4. Sous **tous les produits**, sélectionnez votre option de produit qui inclut la licence Intune, puis **affecter** en haut du volet.  

   Par exemple, vous pouvez sélectionner **Enterprise Mobility + Security E5** si c’est le mode d’obtention Intune.  

5. Sur le **affecter une licence** volet, cliquez sur **utilisateurs et groupes** pour ouvrir le **utilisateurs et groupes** volet. Sélectionnez les groupes et utilisateurs individuels auxquels vous souhaitez attribuer une licence.  Ensuite, cliquez sur **sélectionnez** en bas du volet pour confirmer cette sélection.  

6. Sur le **affecter une licence** volet, cliquez sur **options d’affectation** pour afficher tous les plans de service inclus dans le produit que vous avez sélectionnée précédemment. Si vous avez sélectionné un produit unique comme Intune, seulement ce produit est indiqué.  
   - Définissez **Microsoft Intune** à **sur**.  
   - Affecter une licence pour chaque utilisateur **Azure Active Directory Premium**.  

   Lorsque les licenses applicables sont affectés, sélectionnez **OK**.  

7. Pour terminer l’affectation, sur le **affecter une licence** volet, cliquez sur **affecter** en bas du volet.

8. Une notification s’affiche dans le coin supérieur droit qui affiche l’état et le résultat du processus. Si l’affectation au groupe n’a pas pu être effectuée (par exemple, en raison de licences existantes dans le groupe), cliquez sur la notification pour afficher les détails de l’échec.

Pour plus d’informations sur l’attribution de licences pour Intune aux utilisateurs, consultez [attribuer des licences](https://docs.microsoft.com/intune/licenses-assign).


## <a name="enable-co-management-in-configuration-manager"></a>Activer la cogestion dans Configuration Manager
Avec l’ensemble d’Azure AD hybride des configurations du client Configuration Manager en place et les licences de produit attribuées aux utilisateurs, vous êtes prêt à basculer sur l’et activer la cogestion de vos appareils Windows 10.  

> [!TIP]  
>  À l’étape six de la procédure suivante, vous allez affecter une collection comme un *groupe pilote* pour la cogestion. Il s’agit d’un groupe qui contient un petit nombre de clients pour tester vos configurations de cogestion. Nous vous recommandons de que créer une collection appropriée avant de commencer la procédure. Ensuite, vous pouvez sélectionner cette collection sans quitter la procédure pour ce faire.  

1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.

2. Sous l’onglet Accueil, dans le groupe gérer, sélectionnez **configurer la cogestion** pour ouvrir l’Assistant de Configuration de la cogestion.

3. Dans la page d’abonnement, sélectionnez **Sign In** et connectez-vous à votre client Intune, puis sélectionnez **suivant**.

4. Dans la page Activation, à partir de la *l’inscription automatique dans Intune* liste déroulante, sélectionnez une des options suivantes :  

   - **Pilote**  - *(recommandé)* membres du regroupement que vous spécifiez sont automatiquement inscrits dans Intune et peuvent ensuite être gérés conjointement. Vous spécifiez le regroupement pilote sur le *intermédiaire* page de cet Assistant. Cette option vous permet de tester la cogestion sur un sous-ensemble de clients. Vous pouvez ensuite déployer les cogestion à des clients supplémentaires à l’aide d’une approche progressive.  

   - **Tous les** -cogestion est activée pour tous les clients.  

5. Dans la page de charges de travail, vous pouvez basculer les charges de travail à partir de **Configuration Manager** à une des opérations suivantes, puis lorsque vous êtes prêt à continuer, sélectionnez **suivant**.  

   - **Piloter Intune** -bascule d’une charge de travail uniquement pour les appareils dans le groupe pilote. Vous allez affecter une collection en tant que le groupe pilote sur la page suivante de l’Assistant.  

   - **Intune** -bascule la charge de travail associé pour tous les appareils Windows 10 cogérés.  

   Vous n’avez pas besoin de basculer des charges de travail au moment où que vous activez la cogestion. Vous pouvez revenir consulter cette configuration à partir de la console Configuration Manager ultérieurement, après avoir configuré la cogestion.  

   Avant de basculer d’une charge de travail, assurez-vous que la charge de travail correspondant dans Intune est configuré et déployé. Faire c’est le cas conserve les charges de travail gérés.  

6. Dans la page mise en lots, spécifiez un regroupement à utiliser pour le **regroupement pilote**, puis cliquez sur **suivant**. La collection que vous spécifiez est utilisée dans le cadre de votre déploiement progressif de la cogestion. À tout moment, vous pouvez modifier les regroupements dans le groupe pilote à partir des propriétés de cogestion.  

7. Dans la page Résumé, sélectionnez **suivant**, puis **fermer** pour terminer l’Assistant.  


## <a name="next-steps"></a>Étapes suivantes
- Passez en revue l’état des appareils gérés conjointement avec le [tableau de bord de cogestion](/sccm/comanage/how-to-monitor)
- Commencer à obtenir [valeur immédiate](quickstarts.md#immediate-value) à partir de la cogestion
- Utilisez [accès conditionnel](quickstart-conditional-access.md) et règles de conformité Intune pour gérer l’accès utilisateur aux ressources d’entreprise
