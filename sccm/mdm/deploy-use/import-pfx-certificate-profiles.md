---
title: Créer des profils de certificat PFX en important les détails du certificat
titleSuffix: Configuration Manager
description: Découvrez comment utiliser des fichiers PFX dans System Center Configuration Manager pour générer des certificats spécifiques à l’utilisateur qui prennent en charge l’échange de données chiffrées.
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b999dddc048c1afe0dd4212ed9b99ebc9c991ff0
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678854"
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Guide pratique pour créer des profils de certificat PFX en important les détails du certificat

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous allez découvrir ici comment créer un profil de certificat en important des informations d’identification à partir de certificats externes.  

Les [profils de certificat](../../protect/deploy-use/introduction-to-certificate-profiles.md) fournissent des informations générales sur la création et la configuration des profils de certificat. Cette rubrique met en évidence des informations spécifiques sur les profils de certificat associés aux certificats PFX.

- Configuration Manager donne accès à divers magasins de certificats adaptés à différents appareils et systèmes d’exploitation.  À savoir :

  -   iOS et MacOS/OSX
  -   Android et Android for Work
  -   Windows 10, notamment Windows 10 Mobile.

Pour plus d’informations, consultez [Prérequis des profils de certificat](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Profils de certificat PFX
System Center Configuration Manager vous permet d’importer des informations d’identification de certificats, puis d’approvisionner des fichiers d’échange d’informations personnelles (.pfx) sur les appareils des utilisateurs. Vous pouvez utiliser des fichiers PFX pour générer des certificats spécifiques à l'utilisateur pour prendre en charge l'échange de données chiffrées.

> [!TIP]  
>  Une procédure pas à pas décrivant ce processus est disponible dans [Comment créer et déployer des profils de certificat PFX dans Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Créer, importer et déployer un profil de certificat PFX (Personal Information Exchange)  

### <a name="get-started"></a>Bien démarrer

1.  Dans la console System Center Configuration Manager, cliquez sur **Ressources et Conformité**.  
2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis **Accès aux ressources de l'entreprise**, et cliquez sur **Profils de certificat**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil de certificat**.

4.  Dans la page **Général** de l'Assistant **Créer un profil de certificat** , spécifiez les informations suivantes :  

    -   **Nom** : Entrez un nom unique pour le profil de certificat. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Description** : Entrez une description qui donne un aperçu du profil de certificat et d’autres informations utiles pour identifier facilement ce profil dans la console System Center Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Spécifiez le type de profil de certificat que vous voulez créer** : Pour les certificats PFX, choisissez l’une des options suivantes :  

        -   **Échange d'informations personnelles -- Paramètres PKCS #12 (PFX) -- Importation** : Crée un profil de certificat en important des informations par programme à partir de certificats existants.  

        -   **Échange d’informations personnelles - paramètres PKCS #12 (PFX) - créer**: Crée un profil de certificat PFX à l’aide des informations d’identification fournies par une autorité de certification.  Pour plus d’informations, consultez [Guide pratique pour créer des profils de certificat PFX à l’aide d’une autorité de certification](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Créer un profil de certificat PFX pour les informations d’identification importées

Pour importer un certificat PFX, vous utilisez le SDK de Configuration Manager pour déployer un script de création de fichier PFX. 

Les certificats importés sont plus tard déployés sur les appareils inscrits.

1. Dans la page **Certificat PFX** de l’**Assistant Création d’un profil de certificat**, spécifiez l’emplacement du fournisseur de stockage de clé d’appareil :
    - **Installer dans le module de plateforme sécurisée (TPM) s'il existe**  
    - **Installer dans le module de plateforme sécurisée (TPM) sinon mettre en échec** 
    - **Installer dans Windows Hello Entreprise, sinon mettre en échec** 
    - **Installer dans le fournisseur de stockage de la clé du logiciel** 
2. Cliquez sur **Suivant**. 
3. Dans la page **Plateformes prises en charge** de l’Assistant, choisissez les plateformes d’appareils prises en charge, puis cliquez sur **Suivant**.

### <a name="finish-the-profile"></a>Terminer le profil

1.  Cliquez sur **Suivant**, passez en revue la page **Résumé** , puis fermez l'Assistant.  
2.  Le profil de certificat contenant le fichier PFX est désormais disponible à partir de l'espace de travail **Profils de certificat** . 
3.  Pour déployer le profil, dans l’espace de travail **Ressources et conformité**, accédez à **Paramètres de compatibilité** > **Accès aux ressources de l’entreprise** > **Profils de certificat**, cliquez avec le bouton droit sur le certificat requis, puis cliquez sur **Déployer**. 

### <a name="deploy-a-create-pfx-script"></a>Déployer un script de création de fichier PFX

Utilisez le [SDK Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=613525) pour déployer un script de création de fichier PFX. 

Le script de création de fichier PFX ajouté dans Configuration Manager 2012 SP2 ajoute une classe SMS_ClientPfxCertificate au kit SDK. Cette classe comprend les méthodes suivantes :  

-   `ImportForUser`  

-   `DeleteForUser`  

L’exemple suivant importe des informations d’identification dans un profil de certificat PFX.

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

Pour utiliser cet exemple, mettez à jour les variables de script suivantes :  

   -   **blob**\ : objet blob PFX chiffré en base64  
   -   **$Password** : mot de passe pour le fichier PFX  
   -   **$ProfileName** : nom du profil PFX  
   -   **ComputerName** : nom de l’ordinateur hôte   

## <a name="see-also"></a>Voir aussi
La section [Créer un profil de certificat](../../protect/deploy-use/create-certificate-profiles.md) vous guide tout au long des étapes de l’Assistant Créer un profil de certificat.

[Guide pratique pour créer des profils de certificat PFX en important les détails du certificat](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

[Déployer des profils dans System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) décrit comment déployer des profils de certificat.
