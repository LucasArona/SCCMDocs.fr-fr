---
title: Configurer l’infrastructure de certificats
titleSuffix: Configuration Manager
description: Découvrez comment configurer l’inscription de certificats dans System Center Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ff32a35ccfe3ca51183497197622408c1a28a99d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416297"
---
# <a name="configure-certificate-infrastructure"></a>Configurer l’infrastructure de certificats

*S’applique à : System Center Configuration Manager (Current Branch)*

Découvrez comment configurer une infrastructure de certificats dans System Center Configuration Manager. Avant de commencer, examinez les conditions requises répertoriées dans [Configuration requise pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Suivez ces étapes pour configurer votre infrastructure pour les certificats SCEP ou PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Étape 1 : Installer et configurer le service d’inscription de périphérique réseau et les dépendances (pour les certificats SCEP uniquement)

 Vous devez installer et configurer le service de rôle du service d'inscription d'appareils réseau pour les services de certificat Active Directory (AD CS), modifier les autorisations de sécurité sur les modèles de certificat, déployer un certificat d'authentification de client PKI et modifier le Registre pour augmenter la taille limite des URL IIS par défaut. Si nécessaire, vous devez aussi configurer l'Autorité de certification (CA) émettrice pour autoriser une période de validité personnalisée.  

> [!IMPORTANT]  
>  Avant de configurer System Center Configuration Manager pour fonctionner avec le service d’inscription d’appareils réseau, vérifiez l’installation et la configuration de ce dernier. Si ces dépendances ne fonctionnent pas correctement, vous aurez des difficultés à résoudre les problèmes d’inscription de certificats à l’aide de System Center Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Pour installer et configurer le service d'inscription d'appareils réseau et les dépendances  

1. Sur un serveur exécutant Windows Server 2012 R2, installez et configurez le service de rôle du service d'inscription d'appareils réseau pour le rôle de serveur des services de certificats Active Directory. Pour plus d'informations, voir [Network Device Enrollment Service Guidance (Guide du service d'inscription d'appareils réseau)](http://go.microsoft.com/fwlink/p/?LinkId=309016) dans la bibliothèque des services de certificats Microsoft Active Directory sur TechNet.  

2. Vérifiez et, si nécessaire, modifiez les autorisations de sécurité des modèles de certificat utilisés par le service d'inscription d'appareils réseau :  

   -   Pour le compte qui exécute la console System Center Configuration Manager : Autorisation **Lecture**.  

        Cette autorisation est requise afin que vous puissiez rechercher et sélectionner le modèle de certificat à utiliser pour créer un profil de paramètres SCEP lorsque vous exécutez l'Assistant de création d'un profil de certificat. La sélection d'un modèle de certificat signifie que certains paramètres dans l'Assistant sont automatiquement renseignés pour vous. Les tâches de configuration sont réduites, ainsi que les risques de sélection de paramètres non compatibles avec les modèles de certificat utilisés par le service d'inscription d'appareils réseau.  

   -   Pour le compte de service SCEP que le pool d'applications du service d'inscription d'appareils réseau utilise : Autorisations **Lecture** et **Inscription**.  

        Cette exigence n’est pas spécifique à System Center Configuration Manager, mais elle fait partie de la configuration du service d’inscription d’appareils réseau. Pour plus d'informations, voir [Network Device Enrollment Service Guidance (Guide du service d'inscription d'appareils réseau)](http://go.microsoft.com/fwlink/p/?LinkId=309016) dans la bibliothèque des services de certificats Microsoft Active Directory sur TechNet.  

   > [!TIP]  
   >  Pour identifier les modèles de certificat utilisés par le service d'inscription d'appareils réseau, affichez la clé de registre suivante sur le serveur exécutant le service d'inscription d'appareils réseau : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Ces autorisations de sécurité sont les valeurs par défaut appropriées pour la plupart des environnements. Toutefois, vous pouvez utiliser une autre configuration de sécurité. Pour plus d’informations, consultez [Planification d’autorisations de modèles de certificat pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Déployez vers ce serveur un certificat PKI prenant en charge l'authentification du client. Vous disposez peut-être déjà d'un certificat adapté installé sur l'ordinateur, que vous pouvez utiliser, ou vous devez (ou préférez) déployer un certificat spécifique. Pour plus d’informations sur la configuration requise de ce certificat, consultez « Serveurs exécutant le module de stratégie de Configuration Manager avec le service de rôle du service d’inscription d’appareils réseau » dans la section **Certificats PKI pour serveurs** de la rubrique [Configuration requise des certificats PKI pour System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

   > [!TIP]
   >  Pour obtenir de l’aide pour le déploiement de ce certificat, suivez les instructions dans la section [Déploiement du certificat client pour les points de distribution](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012), car les exigences relatives au certificat sont identiques, à une exception près :  
   > 
   > - N'activez pas la case à cocher **Autoriser l'exportation de la clé privée** dans l'onglet **Traitement de la demande** des propriétés du modèle de certificat.  
   > 
   >   Vous n’avez pas à exporter ce certificat avec la clé privée, car vous pouvez le rechercher dans le magasin de l’ordinateur local et le sélectionner lors de la configuration du module de stratégie de System Center Configuration Manager.  

4. Localisez le certificat racine auquel est lié le certificat d'authentification. Exportez ensuite ce certificat d'Autorité de certification racine dans un fichier de certificat (.cer). Enregistrez ce fichier dans un emplacement sécurisé auquel vous pouvez accéder en toute sécurité lorsque plus tard vous installez et configurez le serveur de système de site du point d'enregistrement de certificat.  

5. Sur le même serveur, utilisez l’Éditeur du Registre pour augmenter la taille limite des URL IIS par défaut en définissant les valeurs DWORD de clés de Registre suivantes dans HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters :  

   - Définissez la clé **MaxFieldLength** à **65534**.  

   - Définissez la clé **MaxRequestBytes** à **16777216**.  

     Pour plus d’informations, consultez l’article [820129 : Paramètres de Registre Http.sys pour Windows](http://go.microsoft.com/fwlink/?LinkId=309013) dans la Base de connaissances Microsoft.  

6. Sur le même serveur, dans le Gestionnaire des services Internet (IIS), modifiez les paramètres de filtrage des demandes pour l'application /certsrv/mscep, puis redémarrez le serveur. Dans la boîte de dialogue **Modifier les paramètres de filtrage des demandes** , les paramètres **Limites des demandes** doivent se présenter comme suit :  

   - **Longueur maximale autorisée du contenu (octets)**  : **30000000**  

   - **Longueur maximale des URL (octets)**  : **65534**  

   - **Longueur maximale des chaînes de requête (octets)**  : **65534**  

     Pour plus d'informations sur ces paramètres et sur la façon de les configurer, voir [Limites des demandes](http://go.microsoft.com/fwlink/?LinkId=309014) dans la bibliothèque de référence IIS.  

7. Si vous souhaitez pouvoir demander un certificat avec une durée de validité inférieure à celle du modèle de certificat que vous utilisez : Cette configuration est désactivée par défaut pour une Autorité de certification d'entreprise. Pour activer cette option pour une Autorité de certification d'entreprise, utilisez l'outil de ligne de commande Certutil, puis arrêtez et redémarrez le service de certificats à l'aide des commandes suivantes :  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Pour plus d'informations, voir [Outils et paramètres des services de certificat](http://go.microsoft.com/fwlink/p/?LinkId=309015) dans la bibliothèque des technologies PKI sur TechNet.  

8. Vérifiez que le service d’inscription de périphérique réseau fonctionne en utilisant le lien suivant comme exemple : **https://server.contoso.com/certsrv/mscep/mscep.dll**. Vous devriez voir la page Web intégrée Service d'inscription d'appareils réseau. Cette page explique ce qu'est le service et explique que les appareils réseau utilisent l'URL pour soumettre des demandes de certificat.  

   Maintenant que le service d'inscription d'appareils réseau et les dépendances sont configurés, vous êtes prêt à installer et à configurer le point d'enregistrement de certificat.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Étape 2 : Installer et configurer le point d’enregistrement de certificat

Vous devez installer et configurer au moins un point d’enregistrement de certificat dans la hiérarchie System Center Configuration Manager et vous pouvez installer ce rôle de système de site dans le site d’administration centrale ou dans un site principal.  

> [!IMPORTANT]  
>  Avant d'installer le point d'enregistrement de certificat, consultez la section **Configuration requise pour le système de site** de la rubrique [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) pour la configuration de système d'exploitation requise et les dépendances du point d'enregistrement de certificat.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Pour installer et configurer le point d'enregistrement de certificat  

1. Dans la console System Center Configuration Manager, cliquez sur **Administration**.  

2. Dans l'espace de travail **Administration** , développez **Configuration du site**, cliquez sur **Serveurs et rôles de système de site**, puis sélectionnez le serveur à utiliser pour le point d'enregistrement de certificat.  

3. Sous l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**.  

4. Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.  

5. Sur la page **Proxy** , cliquez sur **Suivant**. Le point d'enregistrement de certificat n'utilise pas les paramètres de proxy Internet.  

6. Sur la page **Sélection du rôle système** , sélectionnez **Point d'enregistrement de certificat** dans la liste des rôles disponibles, puis cliquez sur **Suivant**. 

7. Sur la page **Mode d’enregistrement du certificat**, choisissez si vous souhaitez que cet enregistrement de certificat pointe vers **Traiter les demandes de certificat SCEP** ou **Traiter les demandes de certificat PFX**. Un point d’enregistrement de certificat ne peut pas traiter les deux types de requêtes, mais vous pouvez créer plusieurs points d’enregistrement de certificat si vous travaillez avec les deux types de certificats.

   Si vous traitez des certificats PFX, vous devez choisir une autorité de certification Microsoft ou Entrust.

8. La page **Paramètres du point d’enregistrement de certificat** varie selon le type de certificat :
   - Si vous avez sélectionné **Traiter les demandes de certificat SCEP**, configurez les éléments suivants :
     -   **Nom du site web**, **Numéro de port HTTPS** et **Nom de l’application virtuelle** du point d’enregistrement de certificat. Ces champs sont automatiquement renseignés avec les valeurs par défaut. 
     -   **URL du service d’inscription de périphérique réseau et certificat d’autorité de certification racine** : cliquez sur **Ajouter**, puis, dans la boîte de dialogue **Ajouter l’URL et le certificat d’autorité de certification racine**, spécifiez les éléments suivants :
         - URL du service d'inscription d'appareils réseau** : Spécifiez l’URL au format suivant : https://*< FQDN_serveur >*/certsrv/mscep/mscep.dll. Par exemple, si le nom de domaine complet de votre serveur exécutant le service d’inscription de périphérique réseau est server1.contoso.com, tapez **https://server1.contoso.com/certsrv/mscep/mscep.dll**.
         - **Certificat d’autorité de certification racine** : Recherchez et sélectionnez le fichier de certificat (.cer) que vous avez créé et enregistré à l'**étape 1 : Installer et configurer le service d'inscription d'appareils réseau et les dépendances**. Ce certificat d’autorité de certification racine permet au point d’enregistrement de certificat de valider le certificat d’authentification client que le module de stratégie de System Center Configuration Manager va utiliser.  

   - Si vous avez sélectionné **Traiter les demandes de certificats PFX**, vous configurez les détails de la connexion et les informations d’identification pour l’autorité de certification sélectionnée.

     - Pour utiliser Microsoft comme autorité de certification, cliquez sur **Ajouter**, puis, dans la boîte de dialogue **Ajouter une autorité de certification et un compte de certificat**, spécifiez les éléments suivants :
         - **Nom du serveur de l’autorité de certification** : entrez le nom de votre serveur d’autorité de certification.
         - **Compte de l’autorité de certification** : cliquez sur **Définir** pour sélectionner ou créer le compte qui dispose des autorisations d’inscription des modèles sur l’autorité de certification.
         - **Compte de connexion du point d’enregistrement du certificat** : sélectionnez ou créez le compte qui connecte le point d’enregistrement du certificat à la base de données Configuration Manager. Vous pouvez également utiliser le compte de l’ordinateur local qui héberge le point d’enregistrement de certificat.
         - **Compte de publication du certificat Active Directory** : sélectionnez un compte ou créez-en un nouveau qui servira à publier des certificats pour des objets utilisateur dans Active Directory.

         - Dans la boîte de dialogue **URL du service d’inscription des périphériques réseau et du certificat d’Autorité de certification racine**, spécifiez les options suivantes, puis cliquez sur **OK** :  

     - Pour utiliser Entrust comme autorité de certification, spécifiez les éléments suivants :

       - **L’URL du service web MDM**
       - Les informations d’identification (nom d’utilisateur et mot de passe) pour l’URL.

         Quand vous utilisez l’API MDM pour définir l’URL du service web Entrust, veillez à utiliser au moins la version 9 de l’API, comme illustré dans l’exemple suivant :

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Les versions antérieures de l’API ne prennent pas en charge Entrust.

9. Cliquez sur **Suivant** pour terminer l'Assistant.  

10. Attendez quelques minutes pour permettre à l'installation de se terminer, puis vérifiez que le point d'enregistrement de certificat est installé correctement, en utilisant l'une des méthodes suivantes :  

    -   Dans l'espace de travail **Surveillance** , développez **État du système**, cliquez sur **État du composant**, puis recherchez des messages d'état provenant du composant **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   Sur le serveur de système de site, utilisez le fichier *<chemin_installation_ConfigMgr\>* \Logs\crpsetup.log et le fichier *<chemin_installation_ConfigMgr\>* \Logs\crpmsi.log. Une installation réussie renvoie un code de sortie 0.  

    -   Dans un navigateur, vérifiez que vous pouvez vous connecter à l’URL du point d’enregistrement de certificat, par exemple, https://server1.contoso.com/CMCertificateRegistration. Vous devez voir une page **Erreur de serveur** pour le nom de l'application, avec une description HTTP 404.  

11. Recherchez le fichier de certificat exporté pour l’autorité de certification racine, créé automatiquement par le point d’enregistrement de certificat dans le dossier suivant sur l’ordinateur du serveur de site principal : *<chemin_installation_ConfigMgr\>* \inboxes\certmgr.box. Enregistrez ce fichier à un emplacement sécurisé auquel vous pouvez accéder en toute sécurité si vous installez plus tard le module de stratégie de System Center Configuration Manager sur le serveur exécutant le service d’inscription d’appareils réseau.  

    > [!TIP]  
    >  Ce certificat n'est pas immédiatement disponible dans ce dossier. Vous devrez peut-être attendre un certain temps (par exemple, une demi-heure) avant que System Center Configuration Manager ne copie le fichier à cet emplacement.  


## <a name="step-3----install-the-system-center-configuration-manager-policy-module-for-scep-certificates-only"></a>Étape 3 : Installer le module de stratégie de System Center Configuration Manager (pour les certificats SCEP uniquement)

Vous devez installer et configurer le Module de stratégie de System Center Configuration Manager sur chaque serveur que vous avez spécifié dans **étape 2 : Installer et configurer le point d'enregistrement de certificat comme URL pour le service d'inscription d'appareils réseau** dans les propriétés du point d'enregistrement de certificat.  

##### <a name="to-install-the-policy-module"></a>Pour installer le module de stratégie  

1. Sur le serveur qui exécute le service d’inscription d’appareils réseau, connectez-vous en tant qu’administrateur de domaine et copiez les fichiers suivants du dossier <support_installation_ConfigMgr\>\SMSSETUP\POLICYMODULE\X64 sur le support d’installation System Center Configuration Manager vers un dossier temporaire :  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   En outre, si vous avez un dossier LanguagePack sur le support d'installation, copiez ce dossier et son contenu.  

2. À partir du dossier temporaire, exécutez le fichier PolicyModuleSetup.exe pour démarrer l’Assistant Installation du module de stratégie de System Center Configuration Manager.  

3. Sur la page initiale de l'Assistant, cliquez sur **Suivant**, acceptez le termes du contrat de licence, puis cliquez sur **Suivant**.  

4. Sur la page **Dossier d'installation** , acceptez le dossier d'installation par défaut pour le module de stratégie ou spécifiez un autre dossier, puis cliquez sur **Suivant**.  

5. Sur la page **Point d'enregistrement de certificat** , spécifiez l'URL du point d'enregistrement de certificat en utilisant le nom de domaine complet du serveur de système de site et le nom de l'application virtuelle qui est indiqué dans les propriétés du point d'enregistrement de certificat. Le nom de l'application virtuelle par défaut est CMCertificateRegistration. Par exemple, si le nom de domaine complet du serveur de système de site est server1.contoso.com et que vous avez utilisé le nom de l’application virtuelle par défaut, spécifiez **https://server1.contoso.com/CMCertificateRegistration**.  

6. Acceptez le port par défaut **443** ou spécifiez l'autre numéro de port utilisé par le point d'enregistrement de certificat, puis cliquez sur **Suivant**.  

7. Dans la page **Certificat client du module de stratégie**, recherchez et spécifiez le certificat d’authentification client que vous avez déployé à l’**étape 1 : Installer et configurer le service d’inscription d'appareils réseau et les dépendances**, puis cliquez sur **Suivant**.  

8. Dans la page **Certificat du point d’enregistrement de certificat**, cliquez sur **Parcourir** pour sélectionner le fichier de certificat exporté de l’autorité de certification racine que vous avez localisé et enregistré à la fin de l’**étape 2 : Installer et configurer le point d'enregistrement de certificat**.  

   > [!NOTE]  
   >  Si vous n’avez pas enregistré ce fichier de certificat précédemment, il se trouve dans <chemin_installation_ConfigMgr\>\inboxes\certmgr.box sur l’ordinateur du serveur de site.  

9. Cliquez sur **Suivant** pour terminer l'Assistant.  

   Si vous souhaitez désinstaller le module de stratégie de System Center Configuration Manager, utilisez **Programmes et fonctionnalités** dans le Panneau de configuration. 

 
Maintenant que vous avez suivi les étapes de configuration, vous êtes prêt à déployer des certificats aux utilisateurs et aux appareils en créant et en déployant des profils de certificat. Pour plus d’informations sur la création de profils de certificat, consultez [Comment créer des profils de certificat dans System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  
