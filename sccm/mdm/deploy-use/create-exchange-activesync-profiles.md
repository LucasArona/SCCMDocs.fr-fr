---
title: Créer des profils de messagerie Exchange ActiveSync
titleSuffix: Configuration Manager
description: Découvrez comment créer et configurer des profils de messagerie dans System Center Configuration Manager qui fonctionnent avec Microsoft Intune.
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: decd16a03a0381718ada3e4c977d10c159c6be25
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417062"
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Profils de messagerie Exchange ActiveSync dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec Microsoft Intune et Exchange ActiveSync, vous pouvez configurer des appareils avec des profils de messagerie et des restrictions. Cela permet à vos utilisateurs d’accéder à la messagerie d’entreprise sur leurs appareils avec une installation minimale requise de leur part.  

 Vous pouvez configurer les types d'appareils suivants avec des profils de messagerie :  

- Windows 10
- Windows Phone 8.1
- iPhone exécutant iOS 9 et ultérieur 
- iPad exécutant iOS 9 et ultérieur 
- Samsung KNOX Standard 4 et versions ultérieures
- Android for Work

Pour déployer des profils de messagerie sur des appareils, vous devez inscrire ces derniers dans Intune. Pour plus d'informations sur la façon d'inscrire vos appareils, consultez [Gérer les appareils mobiles avec Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).

> [!NOTE]
> Intune propose deux profils de messagerie Android for Work, un pour chacune des applications de messagerie Gmail et Nine Work. Ces applications sont disponibles dans Google Play Store et prennent en charge les connexions à Exchange. Pour activer la connectivité de la messagerie, déployez l’une de ces applications de messagerie sur les appareils de vos utilisateurs, puis créez et déployez le profil approprié. Les applications de messagerie telles que Nine Work peuvent être payantes. Si vous avez des questions, consultez les détails de la licence de l’application ou contactez le fabricant de l’application.

 En plus de configurer un compte de messagerie sur l’appareil, vous pouvez configurer des paramètres de synchronisation pour les contacts, les calendriers et les tâches.  

 Lorsque vous créez un profil de messagerie, vous pouvez inclure un large éventail de paramètres de sécurité. Ces paramètres incluent des certificats pour l’identité, le chiffrement et la signature configurés à l’aide de profils de certificat System Center Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md).    

## <a name="create-an-exchange-activesync-email-profile"></a>Créer un profil de messagerie Exchange ActiveSync  

Pour créer un profil, vous pouvez utiliser l’Assistant Création d’un profil de messagerie Exchange ActiveSync. 

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

2. Dans l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis **Accès aux ressources de l’entreprise** et choisissez **Profils de messagerie**.  

3. Sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer un profil d’e-mail Exchange ActiveSync** pour lancer l’Assistant.

4. Sur la page **Général** de l’Assistant, configurez les éléments suivants :

   - **Nom**. Fournissez un nom descriptif pour le profil de messagerie.

   - **Description**. Si vous le souhaitez, entrez une description du profil de messagerie pour en faciliter l’identification dans la console Configuration Manager.

   - **Ce profil de messagerie est pour Android for Work**. Choisissez cette option si vous déployez ce profil de messagerie uniquement sur des appareils Android for Work. Si vous cochez cette case, la page **Plateformes prises en charge** de l’Assistant ne s’affiche pas. Seuls les profils de messagerie Android for Work sont configurés.

5. Sur la page **Exchange ActiveSync** de l’Assistant, spécifiez les informations suivantes :  

   - **Hôte Exchange ActiveSync**. Spécifiez le nom d’hôte de l’instance Exchange Server d’entreprise qui héberge les services Exchange ActiveSync.  

   - **Nom du compte**. Spécifiez le nom complet du compte de messagerie, tel qu’il apparaît aux utilisateurs sur leurs appareils.  

   - **Nom d’utilisateur du compte**. Sélectionnez le mode de configuration du nom d’utilisateur du compte de messagerie sur les appareils clients. Vous pouvez sélectionner l’une des options suivantes dans la liste déroulante :  

     -   **Nom principal de l’utilisateur**. Utilisez le nom principal complet de l’utilisateur pour la connexion à Exchange.  

     -   **Nom du compte**. Utilisez le nom complet du compte utilisateur à partir d’Active Directory.

     -   **Adresse SMTP principale**. Utilisez l’adresse SMTP principale de l’utilisateur pour la connexion à Exchange.  

   - **Adresse de messagerie**. Sélectionnez la façon dont l’adresse de messagerie de l’utilisateur est générée sur chaque appareil client. Vous pouvez sélectionner l’une des options suivantes dans la liste déroulante :  

     -   **Adresse SMTP principale**. Utilisez l’adresse SMTP principale de l’utilisateur pour la connexion à Exchange.  

     -   **Nom principal de l’utilisateur**. Utilisez le nom principal complet de l'utilisateur comme adresse de messagerie.  

   - **Domaine du compte**. Choisissez l'une des options suivantes :  

     - **Obtenir à partir d'Active Directory**  

     - **Personnalisé**  

       Ce champ s’applique uniquement si **sAMAccountName** est sélectionné dans la liste déroulante **Nom d’utilisateur du compte** .  

   - **Méthode d’authentification**. choisissez l'une des méthodes d'authentification suivantes à utiliser pour authentifier la connexion à Exchange ActiveSync :  

     -   **Certificats**. Un certificat d’identité est utilisé pour authentifier la connexion Exchange ActiveSync.  

     -   **Nom d’utilisateur et mot de passe**. L’utilisateur de l’appareil doit fournir un mot de passe pour se connecter à Exchange ActiveSync. (Le nom d’utilisateur est configuré en tant que partie du profil de messagerie).  

   - **Certificat d’identité**. Cliquez sur **Sélectionner**, puis choisissez un certificat à utiliser pour l'identité.  

      Les certificats d’identité doivent être des certificats SCEP ; vous ne pouvez pas utiliser un certificat PFX.  Pour plus d’informations, consultez [Profils de certificat dans System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

      Cette option est disponible uniquement si vous avez sélectionné **Certificats** sous **Méthode d’authentification**.  

   - **Utiliser S/MIME**. Envoyez des messages électroniques en utilisant le chiffrement S/MIME. Cette option s'applique aux appareils iOS uniquement. Choisissez parmi les options suivantes :

     - **Certificats de signature**.  Choisissez **Sélectionner**, puis un profil de certificat à utiliser pour le chiffrement.  

       Le profil peut être un certificat SCEP ou PFX.  Toutefois, si la signature et le chiffrement sont tous deux utilisés, vous devez sélectionner des profils de certificat PFX pour *à la fois* la signature et le chiffrement.

     - **Certificats de chiffrement**. Cliquez sur **Sélectionner**, puis choisissez un certificat à utiliser pour le chiffrement. Vous pouvez uniquement sélectionner un certificat PFX pour l’utiliser en tant que certificat de chiffrement.

     - Pour chiffrer tous les e-mails sur les appareils iOS, cochez la case **Exiger le chiffrement**.    

       Vous ne pouvez choisir des profils de certificat à ce stade que si vous les avez déjà créés.  Pour plus d’informations, consultez [Profils de certificat dans System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Configurer les paramètres de synchronisation du profil de messagerie Exchange ActiveSync  

Dans la page **Configurer les paramètres de synchronisation** de l'Assistant Création d'un profil de messagerie Exchange ActiveSync, indiquez les informations suivantes :  

-   **Planification**. Sélectionnez la planification selon laquelle les appareils vont synchroniser les données à partir d’Exchange Server. Cette option s'applique uniquement aux appareils Windows Phone. Choisissez parmi :  

    -   **Non configuré**. Aucun calendrier de synchronisation n’est appliqué. Cela permet aux utilisateurs de configurer leur propre calendrier de synchronisation.  

    -   **À la réception de messages**. Les données telles que les messages électroniques et les éléments de calendrier sont automatiquement synchronisées à la réception.  

    -   **15 minutes**. Les données telles que les messages électroniques et les éléments de calendrier sont automatiquement synchronisées toutes les 15 minutes.  

    -   **30 minutes**. Les données telles que les messages électroniques et les éléments de calendrier sont automatiquement synchronisées toutes les 30 minutes.  

    -   **60 minutes**. Les données telles que les messages électroniques et les éléments de calendrier sont automatiquement synchronisées toutes les 60 minutes.  

    -   **Manuel**. L’utilisateur de l’appareil doit lancer la synchronisation manuellement.  

-   **Nombre de jours de courrier électronique à synchroniser**. Dans la liste déroulante, sélectionnez le nombre de jours de courrier électronique que vous souhaitez synchroniser. Choisissez l'une des valeurs suivantes :  

    -   **Non configuré**. Le paramètre n’est pas appliqué. Cela permet aux utilisateurs de configurer la quantité de courrier électronique téléchargé sur leur appareil.  

    -   **Illimité**. Synchronisez tous les messages disponibles.  

    -   **1 jour**  

    -   **3 jours**  

    -   **1 semaine**  

    -   **2 semaines**  

    -   **1 mois**  

-   **Autoriser le déplacement des messages vers d’autres comptes de messagerie**. Choisissez cette option pour autoriser les utilisateurs à déplacer des messages électroniques entre différents comptes qu’ils ont configurés sur leur appareil. Cette option s'applique aux appareils iOS uniquement.  

-   **Autoriser l’envoi de courrier depuis des applications tierces**. Sélectionnez cette option pour autoriser les utilisateurs à envoyer du courrier électronique à partir de certaines applications de messagerie tierces non définies par défaut. Cette option s'applique aux appareils iOS uniquement.  

-   **Synchroniser les adresses de messagerie récemment utilisées**. Sélectionnez cette option pour synchroniser la liste des adresses de messagerie récemment utilisées sur l’appareil. Cette option s'applique aux appareils iOS uniquement.  

-   **Utiliser SSL**. Sélectionnez cette option pour utiliser une communication SSL (Secure Sockets Layer) pour l’envoi et la réception des messages électroniques et pour communiquer avec le serveur Exchange.  

-   **Type de contenu à synchroniser**. Sélectionnez les types de contenu à synchroniser avec des appareils. Cette option s'applique uniquement aux appareils Windows Phone. Choisissez parmi :  

    -   **Courrier électronique**  

    -   **Contacts**  

    -   **Calendrier**  

    -   **Tâches**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Spécifiez les plateformes prises en charge pour le profil de messagerie Exchange ActiveSync.  

1.  Dans la page **Plateformes prises en charge** de l’Assistant Création d’un profil de messagerie Exchange ActiveSync, choisissez les systèmes d’exploitation sur lesquels le profil de messagerie Exchange ActiveSync va être installé. Vous pouvez également choisir **Sélectionner tout** pour installer le profil de messagerie sur tous les systèmes d'exploitation disponibles.  

2.  Fermez l'Assistant.

Pour plus d’informations sur le déploiement des profils de messagerie Exchange ActiveSync, consultez [Guide pratique pour déployer des profils dans System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  
