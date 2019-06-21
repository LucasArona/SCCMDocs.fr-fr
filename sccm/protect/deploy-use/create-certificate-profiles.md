---
title: Créer des profils de certificat SCEP
titleSuffix: Configuration Manager
description: Découvrez comment utiliser des profils de certificat pour configurer les appareils gérés avec les certificats nécessaires dans System Center Configuration Manager.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 726df4e6ddbfc34194fd25951d6dbafd1e9008ad
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159541"
---
# <a name="create-certificate-profiles"></a>Créer des profils de certificat

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez des profils de certificat dans Configuration Manager (SCCM) pour configurer les appareils gérés avec les certificats nécessaires pour accéder aux ressources d’entreprise. Avant de créer des profils de certificat, configurez l’infrastructure de certificats, comme décrit dans [Configurer l’infrastructure de certificats pour System Center Configuration Manager](certificate-infrastructure.md).  

Cette rubrique explique comment créer des profils de certificat racine approuvé et des profils de certificat SCEP. Si vous souhaitez créer des profils de certificat PFX, consultez [Créer des profils de certificat PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles).

Pour créer un profil de certificat :

1.  Démarrez l’Assistant Créer un profil de certificat.
1.  Fournissez les informations générales sur le certificat.
1.  Configurez un certificat d’autorité de certification approuvé.  
1.  Configurez les informations de certificat SCEP (uniquement pour les certificats SCEP).  
1.  Spécifiez les plateformes prises en charge pour le profil de certificat.


## <a name="start-the-create-certificate-profile-wizard"></a>Démarrer l’Assistant Créer un profil de certificat  

1.  Dans la console System Center Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , développez **Paramètres de compatibilité**, puis **Accès aux ressources de l'entreprise**, et cliquez sur **Profils de certificat**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil de certificat**.  

## <a name="provide-general-information-about-the-certificate-profile"></a>Fournir des informations générales sur le profil de certificat  

Sur la page **Général** de l'Assistant Création d'un profil de certificat, spécifiez les informations suivantes :  

-   **Nom**: entrez un nom unique pour le profil de certificat. Vous pouvez utiliser jusqu'à 256 caractères.  

-   **Description** : entrez une description qui donne un aperçu du profil de certificat et d’autres informations utiles pour identifier facilement ce profil dans la console System Center Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.  

-   **Spécifiez le type de profil de certificat que vous voulez créer**: choisissez un des types de profil de certificat suivants :  

-   **Certificat d’Autorité de certification approuvé**: sélectionnez ce type de profil de certificat si vous souhaitez déployer un certificat d’autorité de certification racine ou intermédiaire approuvé pour former une chaîne d’approbation des certificats quand l’utilisateur ou l’appareil doit authentifier un autre appareil. Par exemple, l'appareil peut être un serveur RADIUS (Remote Authentication Dial-In User Service) ou un serveur VPN (réseau privé virtuel). Vous devez également configurer un profil de certificat d'Autorité de certification approuvé pour pouvoir créer un profil de certificat SCEP. Dans ce cas, le certificat d'Autorité de certification approuvé doit être le certificat racine approuvé pour l'Autorité de certification qui émet le certificat à l'utilisateur ou à l'appareil.  

-   **Paramètres du protocole SCEP (Simple Certificate Enrollment Protocol)** : sélectionnez ce type de profil de certificat pour demander un certificat pour un appareil ou un utilisateur à l’aide du protocole SCEP et du service de rôle du service d’inscription d’appareils réseau.

-   **Échange d’informations personnelles - Paramètres PKCS #12 (PFX) - Importation** : sélectionnez cette option pour importer un certificat PFX. Pour en savoir plus sur la création de certificats PFX, consultez [Importer des profils de certificat PFX](/sccm/mdm/deploy-use/import-pfx-certificate-profiles).

-   **Échange d’informations personnelles - Paramètres PKCS #12 (PFX) - Créer** : sélectionnez cette option pour traiter les certificats PFX en utilisant une autorité de certification. Pour en savoir plus sur la création de certificats PFX, consultez [Créer des profils de certificat PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles).


## <a name="configure-a-trusted-ca-certificate"></a>Configurer un certificat d’autorité de certification approuvé  

> [!IMPORTANT]  
>  Vous devez configurer au moins un profil de certificat d'Autorité de certification approuvé pour pouvoir créer un profil de certificat SCEP.    
>  
>  Si vous modifiez l’une des valeurs suivantes après le déploiement du certificat, un nouveau certificat est demandé :
>  -  Fournisseur de stockage de clés
>  -  Nom du modèle de certificat
>  -  Type de certificat
>  -  Format du nom de l'objet
>  -  Autre nom de l'objet
>  -  Période de validité du certificat
>  -  Utilisation de la clé
>  -  Taille de la clé
>  -  Utilisation améliorée de la clé
>  -  Certificat d’autorité de certification racine

1. Sur la page **Certificat d'Autorité de certification approuvé** de l'Assistant Création d'un profil de certificat, spécifiez les informations suivantes :  

   -   **Fichier de certificat**: cliquez sur **Importer** , puis recherchez le fichier de certificat que vous souhaitez utiliser.  

   -   **Banque de destination**: pour les appareils qui ont plus d’un magasin de certificats, sélectionnez l’emplacement où stocker le certificat. Pour les appareils avec un seul magasin, ce paramètre est ignoré.  

2. Utilisez la valeur **Empreinte numérique de certificat** pour vérifier que vous avez importé le certificat correct.  


## <a name="configure-scep-certificate-information-only-for-scep-certificates"></a>Configurer les informations de certificat SCEP (uniquement pour les certificats SCEP)  

1. Dans la page **Serveurs SCEP** de l’Assistant Créer un profil de certificat, spécifiez l’URL des serveurs NDES qui délivreront des certificats par le biais du protocole SCEP. Vous pouvez choisir d’affecter automatiquement une URL NDES en fonction de la configuration du serveur de système de site de point d’inscription de certificat, ou ajouter les URL manuellement.  

2. Renseignez la page **Inscription SCEP** de l’Assistant Créer un profil de certificat.

   -  **Tentatives**: spécifiez le nombre de fois où l’appareil doit renvoyer automatiquement la demande de certificat au serveur exécutant le service d’inscription de périphériques réseau. Ce paramètre prend en charge le scénario où un gestionnaire de l'autorité de certification doit approuver une demande de certificat avant d'être accepté. Ce paramètre est généralement utilisé pour des environnements haute sécurité ou si vous avez une autorité de certification émettrice autonome plutôt qu'une autorité de certification d'entreprise. Vous pouvez également utiliser ce paramètre à des fins de test pour vérifier les options de demande de certificat avant que l'Autorité de certification émettrice traite la demande de certificat. Utilisez ce paramètre conjointement avec le paramètre **Délai de nouvelle tentative (en minutes)** .  

   -   **Délai de nouvelle tentative (en minutes)** : spécifiez l’intervalle, en minutes, entre deux tentatives d’inscription, quand vous utilisez l’approbation du gestionnaire de l’Autorité de certification avant que l’Autorité de certification émettrice traite la demande de certificat. Si vous utilisez l'approbation du gestionnaire à des fins de test, la spécification d'une valeur faible évitera d'attendre trop longtemps une nouvelle tentative de demande de certificat par l'appareil après l'approbation de la demande. Toutefois, si vous utilisez l'approbation du gestionnaire sur un réseau de production, vous voudrez spécifier une valeur élevée pour donner suffisamment de temps à l'administrateur de l'Autorité de certification pour vérifier et approuver ou refuser les approbations en attente.  

   -   **Seuil de renouvellement (%)** : spécifiez le pourcentage de durée de vie restante du certificat avant que l’appareil ne demande le renouvellement du certificat.  

   -   **Fournisseur de stockage de clés**: spécifiez l’emplacement de stockage de la clé du certificat. Choisissez l'une des valeurs suivantes :  

   -   **Installer dans le module de plateforme sécurisée (TPM) s’il existe**: installe la clé dans le module de plateforme sécurisée. Si le module de plateforme sécurisée n'est pas présent, la clé est installée dans le fournisseur de stockage de la clé du logiciel.  

   -   **Installer dans le module de plateforme sécurisée (TPM) sinon mettre en échec**: installe la clé dans le module de plateforme sécurisée. Si le module de plateforme sécurisée n'est pas présent, l'installation échoue.  

   -   **Installer dans Windows Hello Entreprise, sinon mettre en échec** : cette option est disponible pour les appareils Windows 10 Desktop et Mobile. Elle permet d’inscrire la clé dans **Windows Hello Entreprise**, comme cela est décrit dans [Paramètres Windows Hello Entreprise dans System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md). Cette option vous permet également d’ **Exiger une authentification multifacteur** lors de l’inscription des appareils avant de délivrer des certificats à ces appareils. Pour plus d’informations, consultez [Utiliser l’authentification multifacteur dans Microsoft Intune](https://technet.microsoft.com/library/dn889751.aspx) .

   > [!NOTE]  
   > 
   > Quand un utilisateur crée un code confidentiel Windows Hello Entreprise, Windows envoie une notification que Configuration Manager écoute. Configuration Manager peut ainsi déterminer rapidement quels utilisateurs ont créé un code confidentiel Windows Hello. Ensuite, Configuration Manager peut également émettre de nouveaux certificats pour les utilisateurs si Windows Hello est utilisé comme fournisseur de stockage de la clé dans un profil de certificat.  

   -   **Installer dans le fournisseur de stockage de la clé du logiciel**: installe la clé dans le fournisseur de stockage de la clé du logiciel.  

   -   **Appareils pour l’inscription du certificat**: si le profil de certificat est déployé sur un regroupement d’utilisateurs, choisissez d’autoriser l’inscription de certificats uniquement sur l’appareil principal de l’utilisateur ou sur tous les appareils auxquels se connecte l’utilisateur. Si le profil de certificat est déployé sur un regroupement d'appareils, choisissez d'autoriser l'inscription de certificats uniquement pour l'utilisateur principal de l'appareil ou pour tous les utilisateurs qui se connectent à l'appareil.  

3. Sur la page **Propriétés du certificat** de l'Assistant Création d'un profil de certificat, spécifiez les informations suivantes :  

   -   **Nom du modèle de certificat**: cliquez sur **Parcourir** pour sélectionner le nom d’un modèle de certificat que doit utiliser le service d’inscription de périphériques réseau conformément à sa configuration et qui a été ajouté à une Autorité de certification émettrice. Pour avoir accès au modèle de certificat, le compte d’utilisateur utilisé pour exécuter la console System Center Configuration Manager doit avoir l’autorisation de lecture sur ce modèle de certificat. Vous pouvez également, si vous ne pouvez pas utiliser **Parcourir**, taper le nom du modèle de certificat.  

   > [!IMPORTANT]
   >   
   >  Si le nom de modèle de certificat contient des caractères non-ASCII (par exemple, les caractères de l'alphabet chinois), le certificat ne sera pas déployé. Pour vous assurer que le certificat est déployé, vous devez tout d'abord créer une copie du modèle de certificat sur l'autorité de certification et renommez la copie à l'aide de caractères ASCII.  

   Notez les informations suivantes, selon que vous accédez au modèle de certificat ou tapez le nom du certificat :  

   -   Si vous naviguez pour sélectionner le nom du modèle de certificat, certains champs de la page sont automatiquement remplis à partir du modèle de certificat. Dans certains cas, vous ne pouvez pas modifier ces valeurs, sauf si vous choisissez un modèle de certificat différent.  

   -   Si vous tapez le nom du modèle de certificat, assurez-vous que le nom correspond exactement à l'un des modèles de certificat figurant dans le Registre du serveur exécutant le service d'inscription d'appareils réseau. Assurez-vous que vous spécifiez le nom du modèle de certificat et non le nom d'affichage du modèle de certificat.  

   Pour rechercher les noms des modèles de certificats, accédez à la clé suivante : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP. Les modèles de certificat s'affichent sous la forme des valeurs **EncryptionTemplate**, **GeneralPurposeTemplate**et **SignatureTemplate**. Par défaut, la valeur des trois modèles de certificat est **IPSECIntermediateOffline**, laquelle correspond au nom d'affichage du modèle **IPSec (requête hors connexion)** .  

   > [!WARNING]  
   > 
   >  System Center Configuration Manager ne peut pas vérifier le contenu du modèle de certificat quand vous tapez le nom du modèle au lieu de le rechercher. De ce fait, il est possible de sélectionner des options qui ne sont pas prises en charge par le modèle de certificat et qui font échouer la demande de certificat. Dans ce cas, un message d'erreur pour w3wp.exe s'affiche dans le fichier CPR.log, indiquant que le nom du modèle dans la demande de signature de certificat (DSC) et le nom dans la vérification ne correspondent pas.  
   >   
   >  Lorsque vous tapez le nom du modèle de certificat spécifié pour la valeur de **modèle à usage général** , vous devez sélectionner les options **Chiffrement de clé** et **Signature numérique** pour ce profil de certificat. Toutefois, si vous voulez activer l'option **Chiffrement de clé** uniquement dans ce profil de certificat, spécifiez le nom du modèle de certificat pour la clé **Modèle de chiffrement** . De la même manière, si vous voulez activer l'option **Signature numérique** uniquement dans ce profil de certificat, spécifiez le nom du modèle de certificat pour la clé **Modèle de signature** .  

   -   **Type de certificat**: sélectionnez si le certificat est déployé sur un appareil ou un utilisateur.  
   -   **Format du nom de l’objet** : dans la liste, sélectionnez de quelle manière System Center Configuration Manager crée automatiquement le nom de l’objet dans la demande de certificat. Si le certificat est pour un utilisateur, vous pouvez également inclure l'adresse de messagerie de cet utilisateur dans le nom de l'objet. 
    
   > [!NOTE]  
   > 
   > Sélectionnez **Numéro IMEI** ou **Numéro de série** pour faire la distinction entre différents appareils appartenant au même utilisateur. Par exemple, si ces appareils ont un nom commun, leur numéro IMEI ou numéro de série est unique. Si l’appareil ne signale pas de numéro IMEI ou de numéro de série, le certificat est émis avec le nom commun.

   -   **Autre nom de l’objet** : spécifiez de quelle manière System Center Configuration Manager crée automatiquement les valeurs pour l’autre nom de l’objet dans la demande de certificat. Par exemple, si vous avez sélectionné un type de certificat utilisateur, vous pouvez inclure le nom d'utilisateur principal (UPN) dans l'autre nom de l'objet.  Si le certificat client est utilisé pour l'authentification sur un serveur de stratégie réseau, l'autre nom de l'objet doit être défini sur le nom d'utilisateur principal.  

   > [!NOTE]  
   >  - Les appareils iOS ne prennent pas en charge tous les formats pour le nom d'objet et autre nom d'objet dans les certificats SCEP. Si vous spécifiez un format non pris en charge, les certificats ne seront pas inscrits sur les appareils iOS. Lorsque vous configurez un profil de certificat SCEP pour le déploiement sur des appareils iOS, utilisez **Nom commun** pour **Format du nom de l'objet**et **Nom DNS**, **Adresse de messagerie** ou **UPN** pour **Autre nom de l'objet**.  

   -   **Période de validité du certificat** : si vous avez exécuté la commande certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE sur l’autorité de certification émettrice, ce qui autorise une période de validité personnalisée, vous pouvez spécifier le temps restant avant l’expiration du certificat. Pour plus d’informations sur cette commande, consultez la rubrique [Infrastructure de certificats dans System Center Configuration Manager](../../protect/deploy-use/certificate-infrastructure.md).  

   Vous pouvez spécifier une valeur inférieure à la période de validité du modèle de certificat spécifié, mais pas une valeur supérieure. Par exemple, si la période de validité du certificat dans le modèle de certificat est de 2 ans, vous pouvez spécifier une valeur de 1 an mais pas une valeur de 5 ans. La valeur doit également être inférieure à la période de validité restante du certificat de l’autorité de certification émettrice.  

   -   **Utilisation de la clé**: spécifiez les options d’utilisation de la clé pour le certificat. Vous pouvez choisir parmi les options suivantes :  

       -   **Chiffrage de clés**: autorisez l’échange de clés uniquement quand la clé est chiffrée.  

       -   **Signature numérique**: autorisez l’échange de clés uniquement quand une signature numérique contribue à protéger la clé.  

   Si vous avez sélectionné un modèle de certificat à l'aide de l'option **Parcourir**, vous risquez de ne pas pouvoir modifier ces paramètres si vous ne sélectionnez pas un autre modèle de certificat.  

   Le modèle de certificat que vous avez sélectionné doit être configuré avec une ou les deux options d'utilisation de la clé ci-dessus. Sinon, le message **Key usage in CSR and challenge do not match** est présent dans le fichier journal de point d'enregistrement de certificat, **Crp.log**.  


- **Taille de la clé (bits)** : sélectionnez la taille de la clé en bits.  

- **Utilisation de la clé étendue** : cliquez sur **Sélectionner** pour ajouter des valeurs pour le rôle prévu du certificat. Dans la plupart des cas, le certificat demande une **Authentification client** afin que l'utilisateur ou l'appareil puisse être authentifié sur un serveur. Toutefois, vous pouvez ajouter d'autres utilisations de la clé en fonction de vos besoins.  


- **Algorithme de hachage**: sélectionnez l’un des types d’algorithme de hachage disponibles avec ce certificat. Permet de sélectionner le niveau le plus élevé de sécurité pris en charge par les appareils se connectant.  

  > [!NOTE]  
  > 
  >  **SHA-2** prend en charge SHA-256, SHA-384 et SHA-512. **SHA-3** prend uniquement en charge SHA-3.  

- **Certificat d’Autorité de certification racine**: cliquez sur **Sélectionner** pour choisir un profil de certificat d’autorité de certification racine que vous avez précédemment configuré et déployé sur l’utilisateur ou l’appareil. Ce certificat d'autorité de certification doit être le certificat racine de l'autorité de certification qui émet le certificat que vous configurez dans ce profil de certificat.  

  > [!IMPORTANT]  
  >  Si vous spécifiez un certificat d’autorité de certification racine qui n’est pas déployé pour l’utilisateur ou l’appareil, System Center Configuration Manager ne lancera pas la demande de certificat que vous configurez dans ce profil de certificat.  


##  <a name="specify-supported-platforms-for-the-certificate-profile"></a>Spécifier les plateformes prises en charge pour le profil de certificat  

1. Sur la page **Plateformes prises en charge** de l'Assistant Création d'un profil de certificat, sélectionnez les systèmes d'exploitation dans lesquels vous voulez installer le profil de certificat. Vous pouvez également cliquer sur **Sélectionner tout** pour installer le profil de certificat sur tous les systèmes d'exploitation disponibles.
2. Dans la page **Résumé** de l’Assistant, passez en revue les paramètres, puis choisissez **Terminer**. 
 
 
Le nouveau profil de certificat s’affiche dans le nœud **Profils de certificat** de l’espace de travail **Ressources et Conformité**. Il est prêt à être déployé pour les utilisateurs ou les appareils, comme décrit dans la rubrique [Guide pratique pour déployer des profils dans System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
