---
title: Créer des profils de certificat PFX à l’aide d’une autorité de certification
titleSuffix: Configuration Manager
description: Découvrez comment utiliser des fichiers PFX dans System Center Configuration Manager pour générer des certificats spécifiques à l’utilisateur qui prennent en charge l’échange de données chiffrées.
ms.date: 11/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a186e0b2c4b355cabcaaeb3b3124b65d3588fbc8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-pfx-certificate-profiles-using-a-certificate-authority"></a>Guide pratique pour créer des profils de certificat PFX à l’aide d’une autorité de certification

*S’applique à : System Center Configuration Manager (Current Branch)*

Ce document vous explique comment créer un profil de certificat qui utilise une autorité de certification pour les informations d’identification.

La section sur les [profils de certificat](../../protect/deploy-use/introduction-to-certificate-profiles.md) fournit des informations générales sur la création et la configuration des profils de certificat. Elle met en évidence des informations spécifiques sur les profils de certificat associés aux certificats PFX.

## <a name="pfx-certificate-profiles"></a>Profils de certificat PFX
System Center Configuration Manager vous permet de créer un profil de certificat PFX à l’aide des informations d’identification émises par une autorité de certification.  À partir de la version 1706, vous pouvez choisir Microsoft ou Entrust comme autorité de certification.  Quand ils sont déployés sur les appareils des utilisateurs, les fichiers d’échange d’informations personnelles (.pfx) génèrent des certificats spécifiques à l’utilisateur pour prendre en charge l’échange de données chiffrées.

Pour importer les informations d’identification de certificat à partir de fichiers de certificat existants, consultez [Guide pratique pour créer des profils de certificat PFX en important les détails du certificat](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Créer et déployer un profil de certificat PFX (Personal Information Exchange)  

### <a name="get-started"></a>Bien démarrer

1.  Dans la console System Center Configuration Manager, choisissez **Ressources et Conformité**.  
2.  Dans l’espace de travail **Ressources et Conformité**, choisissez **Paramètres de compatibilité** &gt; **Accès aux ressources de l’entreprise** &gt; **Profils de certificat**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un profil de certificat**.

4.  Dans la page **Général** de l'Assistant **Créer un profil de certificat** , spécifiez les informations suivantes :  

    -   **Nom**: entrez un nom unique pour le profil de certificat. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Description** : entrez une description qui donne un aperçu du profil de certificat et d’autres informations utiles pour identifier facilement ce profil dans la console System Center Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   Dans **Spécifiez le type de profil de certificat que vous voulez créer**, choisissez **Échange d’informations personnelles -- Paramètres PKCS #12 (PFX) -- Créer**, puis choisissez votre autorité de certification dans la liste déroulante.  Depuis la version 1706, vous pouvez choisir **Microsoft** ou **Entrust**.

### <a name="select-supported-platforms"></a>Sélectionner les plateformes prises en charge

La page Plateformes prises en charge identifie les systèmes d’exploitation et les appareils pris en charge par le profil de certificat.  

Les profils de certificat peuvent prendre en charge plusieurs systèmes d’exploitation et appareils ; toutefois, certaines combinaisons de systèmes d’exploitation ou d’appareils peuvent nécessiter des paramètres différents.  Dans ces cas, il est préférable de créer des profils distincts pour chaque ensemble unique de paramètres.  

Depuis la version 1710, les options ci-dessous sont disponibles :

- Windows 10
    - Tout Windows 10 (64 bits)
    - Tout Windows 10 (32 bits)
    - Tout Windows 10 (ARM64)
    - Tout Windows 10 Holographique Entreprise et ultérieur
    - Tout Windows 10 Holographique et ultérieur
    - Tout Windows 10 Collaboration et ultérieur
    - Tout Windows 10 Mobile et ultérieur
- iPhone
- iPad
- Android
- Android for Work

> [!Note]  
> Les appareils MacOS/OSX ne sont pas pris en charge.  

Quand aucune autre option n’est sélectionnée, la case à cocher **Sélectionner tout** sélectionne toutes les options disponibles.  Quand une ou plusieurs options sont sélectionnées, **Sélectionner tout** efface les sélections existantes. 

1.  Sélectionnez une ou plusieurs plateformes prises en charge par le profil de certificat.

1.  Choisissez **Suivant** pour continuer.  


### <a name="configure-certification-authorities"></a>Configurer des autorités de certification

Dans cette partie, vous choisissez le point d’enregistrement de certificat (CRP) pour traiter les certificats PFX.  

1.  Dans la liste **Site principal**, sélectionnez le serveur qui contient le rôle CRP pour l’autorité de certification.
1.  Dans la liste **Autorités de certification**, choisissez l’autorité de certification appropriée en plaçant une coche dans la colonne de gauche.
1.  Quand vous êtes prêt à continuer, choisissez **Suivant**.

Pour en savoir plus, consultez [Infrastructure de certificats](../../protect/deploy-use/certificate-infrastructure.md).


### <a name="configure-certificate-settings-for-microsoft-ca"></a>Configurer les paramètres de certificat pour l’autorité de certification Microsoft

Pour configurer les paramètres de certificat si Microsoft est utilisé comme autorité de certification :

1.  Dans la liste déroulante **Nom du modèle de certificat**, choisissez le modèle de certificat.

1.  Cochez la case **Utilisation du certificat** pour utiliser le profil de certificat pour le chiffrement ou la signature S/MIME.

    Quand vous cochez cette option tout en utilisant Microsoft comme autorité de certification, tous les certificats PFX associés à l’utilisateur cible sont remis à tous les appareils inscrits par l’utilisateur.  Quand cette case est décochée, chaque appareil reçoit un certificat unique.  

1.  Définissez **Format du nom du sujet** sur **Nom commun** ou **Nom unique**.  En cas de doute sur l’option à utiliser, contactez votre administrateur d’autorité de certification.

1.  Pour **Autre nom de l’objet**, activez **l’Adresse de messagerie** et le **Nom principal de l’utilisateur (UPN)** en fonction de votre autorité de certification.

1.  **Seuil de renouvellement** détermine quand les certificats sont automatiquement renouvelés, en fonction du pourcentage de temps restant avant leur expiration.

1.  Définissez la **Période de validité du certificat** sur la durée de vie du certificat.  Vous spécifiez la période en définissant un nombre (1 à 100) et une période (jours, mois ou années).

1.  La **Publication Active Directory** est activée quand le point d’enregistrement de certificat spécifie les informations d’identification Active Directory.  Activez l’option pour publier le profil de certificat dans Active Directory.

1.  Si vous avez sélectionné une ou plusieurs plateformes Windows 10 quand vous avez spécifié les plateformes prises en charge :

    1.  Définissez **Magasin de certificats Windows** sur **Utilisateur**.  (L’option **Ordinateur local** ne déploie pas de certificats et ne doit pas être choisie.)
    1.  Sélectionnez le **Fournisseur de stockage de clés** à partir d’une des options suivantes :

        - **Installer dans le module de plateforme sécurisée (TPM) s'il existe**  
        - **Installer dans le module de plateforme sécurisée (TPM) sinon mettre en échec** 
        - **Installer dans Windows Hello Entreprise, sinon mettre en échec** 
        - **Installer dans le fournisseur de stockage de la clé du logiciel** 

1.  Quand vous avez terminé, choisissez **Suivant** ou **Résumé**.

### <a name="configure-certificate-settings-for-entrust-ca"></a>Configurer les paramètres de certificat pour l’autorité de certification Entrust

Pour configurer les paramètres de certificat si Entrust est utilisé comme autorité de certification :

1.  Dans la liste déroulante **Configuration de l’identificateur numérique**, choisissez le profil de configuration.  Les options de configuration de l’identificateur numérique sont créées par l’administrateur Entrust.

1.  Quand la case **Utilisation du certificat** est cochée, le profil de certificat est utilisé pour le chiffrement ou la signature S/MIME.

    Quand vous utilisez Entrust comme autorité de certification, tous les certificats PFX associés à l’utilisateur cible sont remis à tous les appareils inscrits par l’utilisateur.    Quand cette option *n’est pas* cochée, chaque appareil reçoit un certificat unique.  (Le comportement varie d’une autorité de certification à l’autre ; pour plus d’informations, consultez la section correspondante).

1.  Utilisez le bouton **Format** pour mapper les jetons **Format du nom du sujet** Entrust aux champs ConfigMgr.  

    La boîte de dialogue **Mise en forme des noms de certificat** répertorie les variables de configuration de l’identificateur numérique Entrust.  Pour chaque variable Entrust, choisissez la variable LDAP appropriée dans la liste déroulante associée.

1.  Utilisez le bouton **Format** pour mapper les jetons **Autre nom de l’objet** Entrust à des variables LDAP prises en charge.  

    La boîte de dialogue **Mise en forme des noms de certificat** répertorie les variables de configuration de l’identificateur numérique Entrust.  Pour chaque variable Entrust, choisissez la variable LDAP appropriée dans la liste déroulante associée.

1.  **Seuil de renouvellement** détermine quand les certificats sont automatiquement renouvelés, en fonction du pourcentage de temps restant avant leur expiration.

1.  Définissez la **Période de validité du certificat** sur la durée de vie du certificat.  Vous spécifiez la période en définissant un nombre (1 à 100) et une période (jours, mois ou années).

1.  La **Publication Active Directory** est activée quand le point d’enregistrement de certificat spécifie les informations d’identification Active Directory.  Activez l’option pour publier le profil de certificat dans Active Directory.

1.  Si vous avez sélectionné une ou plusieurs plateformes Windows 10 quand vous avez spécifié les plateformes prises en charge :

    1.  Définissez **Magasin de certificats Windows** sur **Utilisateur**.  (L’option **Ordinateur local** ne déploie pas de certificats et ne doit pas être choisie.)
    1.  Sélectionnez le **Fournisseur de stockage de clés** à partir d’une des options suivantes :

        - **Installer dans le module de plateforme sécurisée (TPM) s'il existe**  
        - **Installer dans le module de plateforme sécurisée (TPM) sinon mettre en échec** 
        - **Installer dans Windows Hello Entreprise, sinon mettre en échec** 
        - **Installer dans le fournisseur de stockage de la clé du logiciel** 

1.  Quand vous avez terminé, choisissez **Suivant** ou **Résumé**.


### <a name="finish-up"></a>Terminer

1.  Dans la page Résumé, passez en revue vos sélections et vérifiez vos choix.

1.  Quand vous êtes prêt, choisissez **Suivant** pour créer le profil.  

1.  Le profil de certificat contenant le fichier PFX est désormais disponible à partir de l'espace de travail **Profils de certificat** . 

1.  Pour déployer le profil :

    1. Ouvrez l’espace de travail **Ressources et Conformité**.
    1. Choisissez **Paramètres de compatibilité** > **Accès aux ressources de l’entreprise** > **Profils de certificat**.
    1. Cliquez avec le bouton droit sur le profil de certificat souhaité, puis choisissez **Déployer**. 


## <a name="see-also"></a>Voir aussi
La section [Créer un profil de certificat](../../protect/deploy-use/create-certificate-profiles.md) vous guide tout au long des étapes de l’Assistant Créer un profil de certificat.

[Guide pratique pour créer des profils de certificat PFX en important les détails du certificat](../../mdm/deploy-use/import-pfx-certificate-profiles.md)

[Déployer des profils de certificat, Wi-Fi, VPN et d’e-mail](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) décrit comment déployer des profils de certificat.