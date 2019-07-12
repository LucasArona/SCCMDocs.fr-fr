---
title: Tutoriel&#58; Activer la cogestion pour les nouveaux appareils Windows 10 basés sur Internet
titleSuffix: Configuration Manager
description: Configurez la cogestion pour les appareils Windows 10 pour Configuration Manager et Intune.
keywords: ''
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/08/2019
ms.topic: tutorial
ms.prod: configuration-manager
ms.service: ''
ms.technology: ''
ms.assetid: ''
ms.openlocfilehash: 696c952484b53c186b6f1d4f8e5b711262ded5a8
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678008"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Tutoriel : Activer la cogestion pour les nouveaux appareils basés sur Internet
Avec la cogestion, vous pouvez conserver vos processus établis d’utilisation de Configuration Manager pour gérer des PC dans votre organisation, tout en investissant dans le cloud en recourant à Intune pour la sécurité et l’approvisionnement moderne. 

Dans ce tutoriel, vous configurez la cogestion des appareils Windows 10 dans un environnement où vous utilisez Azure Active Directory (AD) et un AD local, mais où vous n’avez pas un [Azure Active Directory (AD) hybride](/azure/active-directory/devices/concept-azure-ad-join-hybrid). L’environnement Configuration Manager inclut un seul site principal avec tous les rôles de système de site situés sur le même serveur, le serveur de site. Ce tutoriel part du principe que vos appareils Windows 10 sont déjà inscrits auprès d’Intune. 

Si vous avez un Azure AD hybride qui joint votre AD local à Azure AD, nous vous recommandons de suivre notre tutoriel connexe, [Activer la cogestion pour les clients Configuration Manager](/sccm/comanage/tutorial-co-manage-clients). 
 
Suivez ce tutoriel si :  
- Vous avez des appareils Windows 10 sur lesquels vous voulez activer la cogestion. Ces appareils peuvent avoir été provisionnés via Windows Autopilot ou proviennent directement de votre OEM matériel. 
- Vous avez des appareils Windows 10 sur Internet que vous gérez actuellement avec Intune auxquels vous souhaitez ajouter le client Configuration Manager.


**Dans ce tutoriel, vous allez :**  
> [!div class="checklist"]  
> * Passer en revue les prérequis pour Azure et votre environnement local
> * Demander un certificat SSL public pour la passerelle de gestion cloud (CMG)
> * Activer les services Azure dans Configuration Manager
> * Déployer et configurer une passerelle de gestion cloud  
> * Configurer le point de gestion et les clients pour utiliser la CMG
> * Activer la cogestion dans Configuration Manager
> * Configurer Intune pour installer le client Configuration Manager
> * Attribuer une licence pour les services cloud



## <a name="prerequisites"></a>Prérequis  

### <a name="azure-services-and-environment"></a>Services et environnement Azure
- Abonnement Azure ([essai gratuit](https://azure.microsoft.com/free)) 
- Azure Active Directory Premium 
- Abonnement Microsoft Intune 
  > [!TIP]  
  > Un abonnement Mobilité et sécurité d’entreprise (EMS) inclut Azure Active Directory Premium et Microsoft Intune. Abonnement EMS ([essai gratuit](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Les utilisateurs doivent se voir [attribuer des licences](tutorial-co-manage-clients.md#assign-intune-licenses-to-users) pour *Intune* et *Azure Active Directory Premium*
- Intune est configuré pour [l’inscription automatique des appareils](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune)  


### <a name="on-premises-infrastructure"></a>Infrastructure locale
- System Center Configuration Manager Current Branch, version 1810 ou version ultérieure.  
  
  La version 1810 inclut le [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http), qui est utilisé dans ce tutoriel afin d’éviter les exigences PKI complexes. Avec l’utilisation du protocole HTTP amélioré, le site principal que vous utilisez pour gérer les clients doit être configuré pour utiliser des certificats générés par Configuration Manager pour les systèmes de site HTTP.  
   
  La version 1810 introduit également une ligne de commande plus simple une installation basée sur Internet du client Configuration Manager.

- [L’autorité MDM](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) doit être définie sur Intune  

### <a name="external-certificates"></a>Certificats externes :
- Certificat d’authentification serveur de passerelle de gestion cloud. Il s’agit d’un certificat SSL provenant d’un fournisseur de certificats public et approuvé globalement. Par exemple, DigiCert, Thawte ou VeriSign (liste non limitative). Vous allez exporter ce certificat en tant que fichier .PFX avec clé privée.  

- Plus loin dans ce tutoriel, nous fournissons des conseils sur la configuration de la demande pour ce certificat.

### <a name="permissions"></a>Autorisations
Tout au long de ce tutoriel, utilisez les autorisations suivantes pour effectuer les tâches :
- Un compte *administrateur général* dans Azure  
- Un compte *administrateur de domaine* dans l’infrastructure locale  
- Un compte qui est un *administrateur complet* pour *toutes* les étendues dans Configuration Manager   


## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Demander un certificat public pour la passerelle de gestion cloud
Lorsque vos appareils se trouvent sur Internet, la cogestion nécessite la passerelle de gestion de cloud (CMG) Configuration Manager. La passerelle CMG permet à vos appareils Windows 10 basés sur Internet de communiquer avec votre déploiement Configuration Manager local. Pour établir une relation d’approbation entre les appareils et votre environnement Configuration Manager, la passerelle CMG requiert un certificat SSL.

Ce tutoriel utilise un certificat public appelé **Certificat d’authentification serveur de passerelle de gestion cloud** qui est dont l’autorité provient d’un fournisseur de certificats approuvé globalement. Bien qu’il soit possible de configurer la cogestion à l’aide de certificats dont l’autorité provient de votre autorité de certification Microsoft locale, l’utilisation de certificats auto-signés dépasse le cadre de ce tutoriel.

Le **certificat d’authentification serveur de passerelle de gestion cloud** est utilisé pour chiffrer le trafic des communications entre le client Configuration Manager et la passerelle CMG. Le certificat remonte à une racine de confiance pour vérifier l’identité du serveur auprès du client. Le certificat public inclut une racine de confiance à laquelle les clients Windows font déjà confiance.

À propos de ce certificat : 

- Vous identifiez un nom unique pour votre service CMG dans Azure, puis spécifiez ce nom dans votre demande de certificat.  
- Vous générez votre demande de certificat sur un serveur spécifique, puis envoyez la demande à un fournisseur de certificats public pour obtenir le certificat SSL nécessaire.  
- Vous importez le certificat que vous recevez du fournisseur dans le système qui a généré la demande. Vous utilisez le même ordinateur pour exporter le certificat à utiliser lors du déploiement ultérieur de la passerelle CMG sur Azure.  
- Lors de l’installation de la passerelle CMG, un service CMG est créé dans Azure à l’aide du nom que vous avez spécifié dans le certificat.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identifier un nom unique pour votre passerelle de gestion cloud dans Azure
Lorsque vous demandez le certificat d’authentification serveur de passerelle de gestion cloud, vous spécifiez ce qui doit être un nom unique pour identifier votre *service cloud (classique)* dans Azure. Par défaut, le cloud public Azure utilise *cloudapp.net*, et la passerelle CMG est hébergée dans le domaine cloudapp.net en tant que *\<YourUniqueDnsName>.cloudapp.net*.  

> [!TIP]  
> Dans ce tutoriel, le **certificat d’authentification serveur de passerelle de gestion cloud** utilise un nom de domaine complet qui se termine par *contoso.com*.  Une fois que nous avons créé la passerelle CMG, nous allons configurer un enregistrement de nom canonique (CNAME) dans le DNS public de notre organisation. Cet enregistrement crée un alias pour la passerelle CMG qui correspond au nom que nous utilisons dans le certificat public.  

Avant de demander votre certificat public, vérifiez que le nom que vous souhaitez utiliser est disponible dans Azure. Vous ne créez pas directement le service dans Azure. Au lieu de cela, le nom spécifié dans le certificat public que vous demandez est utilisé par Configuration Manager pour créer le service cloud lorsque vous installez la passerelle CMG.  

1. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com/).  

2. Sélectionnez **Créer une ressource**, choisissez la catégorie **Calcul**, puis sélectionnez **Service cloud**. Le panneau du service cloud (classique) s’ouvre.

3. Pour **Nom DNS**, spécifiez le nom de préfixe pour le service cloud que vous allez utiliser. Ce préfixe doit être identique à ce que vous utiliserez ultérieurement lorsque vous demanderez un certificat de publication pour le certificat d’authentification serveur de passerelle de gestion cloud. Nous utilisons *MyCSG*, ce qui crée l’espace de noms *MyCSG.cloudapp.net*. L’interface indique si le nom est disponible ou déjà utilisé par un autre service.  
 Après avoir confirmé que le nom que vous souhaitez utiliser est disponible, vous êtes prêt à soumettre la demande de signature de certificat (CSR).

### <a name="request-the-certificate"></a>Demander le certificat
Utilisez les informations suivantes pour envoyer une demande de signature de certificat pour votre passerelle de gestion cloud à un fournisseur de certificats public. Modifiez les valeurs suivantes afin qu’elles soient pertinentes pour votre environnement.  

- *MyCMG* pour identifier le nom du service de la passerelle de gestion cloud
- *Contoso* en tant que nom de l’entreprise
- *Contoso.com* en tant que domaine public

Nous vous recommandons d’utiliser votre serveur de site principal pour générer les demandes de signature de certificat (CSR). Lorsque vous obtenez le certificat, vous devez l’inscrire sur le même serveur que celui qui a généré la demande CSR ou vous ne pourrez pas exporter la clé privée des certificats, ce qui est nécessaire.  

Demandez un type de fournisseur de clés version 2 lorsque vous générez une demande CSR. Seuls les certificats version 2 sont pris en charge.  

> [!TIP]  
> Lors du déploiement de la passerelle CMG, nous installerons également un point de distribution cloud (CDP) en même temps. Par défaut, lorsque vous déployez une passerelle CMG, l’option **Autoriser la passerelle de gestion cloud à fonctionner comme point de distribution cloud et à servir du contenu à partir du stockage Azure** est sélectionnée. La colocalisation du point CDP sur le serveur avec la passerelle CMG supprime le besoin d’avoir des configurations et des certificats distincts pour prendre en charge le CDP. Bien que le CDP n’est pas nécessaire pour utiliser la cogestion, il est utile dans la plupart des environnements.  
>
> Si vous allez utiliser des points de distribution cloud supplémentaires pour la cogestion, vous devrez demander des certificats distincts pour chaque serveur supplémentaire. Pour demander un certificat public pour le CDP, utilisez les détails de la demande CSR pour la passerelle de gestion cloud. Il suffit de modifier le nom commun afin qu’il soit unique pour chaque CDP.  

**Détails de la demande CSR pour la passerelle de gestion cloud**
- **Nom commun** : ClousServiceNameCMG.YourCompanyPubilcDomainName.com  
Exemple : MyCSG.contoso.com  
- **Autre nom de l’objet** : Identique au nom commun (CN)  
- **Organisation** :  Nom de votre organisation  
- **Service** : Selon votre organisation  
- **Ville** : Selon votre organisation  
- **État** : Selon votre organisation  
- **Pays** : Selon votre organisation  
- **Taille de la clé : 2048**  
- **Fournisseur : Microsoft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>Importer le certificat
Après avoir reçu le certificat public, importez-le dans le magasin de certificats local de l’ordinateur qui a créé la demande CSR. Exportez ensuite le certificat en tant que fichier .PFX afin de pouvoir l’utiliser pour votre passerelle CMG dans Azure.  

En général, les fournisseurs de certificats publics fournissent des instructions pour l’importation du certificat. Le processus d’importation du certificat doit ressembler à ce qui suit :  

1. Sur l’ordinateur où le certificat doit être importé, recherchez le fichier .pfx du certificat.  

2. Cliquez avec le bouton droit sur le fichier, puis sélectionnez **Installer PFX**  

3. Au démarrage de l’Assistant Importation de certificat, sélectionnez **Suivant**.  

4. Sur la page **Fichier à importer**, sélectionnez **Suivant**. 

5. Sur la page **Mot de passe**, entrez le mot de passe pour la clé privée dans la zone Mot de passe, puis sélectionnez **Suivant**.  
  
   Sélectionnez l’option permettant de rendre la clé exportable.

6. Sur la **page Magasin de certificats**, choisissez **Sélectionner automatiquement le magasin de certificats selon le type de certificat**, puis sélectionnez **Suivant**.  

7. Sélectionnez **Terminer**.

### <a name="export-the-certificate"></a>Exporter le certificat
Exportez le *certificat d’authentification serveur de la passerelle de gestion cloud* depuis votre serveur. La ré-exportation du certificat rend celui-ci utilisable pour votre passerelle de gestion cloud dans Azure.  

1. Sur le serveur où vous avez importé le certificat SSL public, exécutez **certlm.msc** pour ouvrir la console Gestionnaire de certificats.  

2. Dans la console Gestionnaire de certificats, sélectionnez **Personnel > Certificats**. Ensuite, cliquez avec le bouton droit sur le *certificat d’authentification serveur de passerelle de gestion cloud* que vous avez inscrit dans la procédure précédente, puis sélectionnez **Toutes les tâches > Exporter**.  

3. Dans l’Assistant Exportation de certificat, sélectionnez **Suivant**, **Oui, exporter la clé privée**, puis **Suivant**.  

4. Dans la page Format de fichier d'exportation, sélectionnez **Échange d'informations personnelles - PKCS #12 (.PFX)** , sélectionnez **Suivant** et fournissez un mot de passe. Pour le nom de fichier, spécifiez un nom tel que **C:\ConfigMgrCloudMGServer**. Vous devrez référencer ce fichier lors de la création de la passerelle CMG dans Azure.  

5. Sélectionnez **Suivant**, puis confirmez les paramètres suivants avant de sélectionner **Terminer** pour terminer l’exportation :  

   - Exporter les clés = Oui  
   - Inclure tous les certificats dans le chemin d’accès de certification = Oui  
   - Format de fichier = Personal Information Exchange (*.pfx)  

6. Une fois l’exportation terminée, recherchez le fichier .pfx et placez-en une copie dans **C:\Certs** sur le serveur de site principal Configuration Manager qui va gérer les clients basés sur Internet. Ce dossier Certs est un dossier temporaire à utiliser lors du déplacement de certificats entre les serveurs. Vous accédez au fichier de certificat à partir du serveur de site principal lorsque vous déployez la passerelle de gestion cloud sur Azure.  

Après avoir copié le certificat sur le serveur de site principal, vous pouvez supprimer le certificat du magasin de certificats personnel sur le serveur membre. 


## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Activer les services cloud Azure dans Configuration Manager
Pour configurer les services Azure à partir de la console Configuration Manager, vous utilisez l’Assistant Configurer les services Azure et créez deux applications Azure Active Directory (Azure AD).  

- **Application serveur** : une *application web* dans Azure AD  
- **Application cliente** : une application *cliente native* dans Azure AD  

Exécutez la procédure suivante sur le serveur de site principal.  

1. À partir du serveur de site principal, ouvrez la console Configuration Manager et accédez à **Administration > Services cloud > Services Azure**, puis sélectionnez **Configurer les services Azure**.  

   Sur la page Configurer les services Azure, spécifiez un nom convivial pour le service de gestion cloud que vous configurez. Par exemple : *Mon service de gestion cloud*   

   Sélectionnez **Gestion cloud**, puis **Suivant**.  
   
   > [!TIP]  
   > Pour plus d’informations sur les configurations que vous effectuez dans l’Assistant, consultez [Démarrer l’Assistant Services Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard)


2. Sur la page **Propriétés de l’application**, pour **Application web**, sélectionnez **Parcourir** pour ouvrir la boîte de dialogue **Application serveur**, puis sélectionnez **Créer**. Configurez les champs suivants :

   - **Nom de l'application** : Spécifiez un nom convivial pour l’application, comme *Application web de gestion cloud*.  

   - **URL de la page d'accueil** : Cette valeur n’est pas utilisée par Configuration Manager, mais elle est exigée par Azure AD. Par défaut, cette valeur est https://ConfigMgrService.  
   
   - **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Elle se trouve dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est https://ConfigMgrService.  

   Ensuite, sélectionnez **Se connecter** et spécifiez un compte d’administrateur général Azure. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure. 

   Une fois que vous êtes connecté, les résultats s’affichent. Sélectionnez **OK** pour fermer la boîte de dialogue Créer une application serveur et revenir à la page Propriétés de l’application. 

3. Pour **Application cliente native**, sélectionnez **Parcourir** pour ouvrir la boîte de dialogue **Application cliente**. 

4. Sélectionnez **Créer** pour ouvrir la boîte de dialogue **Créer une application cliente**, puis configurez les champs suivants :  

   - **Nom de l'application** : Spécifiez un nom convivial pour l’application, comme *Application cliente native de gestion cloud*.
   
   - **URL de réponse** : cette valeur n’est pas utilisée par Configuration Manager, mais elle est exigée par Azure AD. Par défaut, cette valeur est https://ConfigMgrClient.
   Ensuite, sélectionnez **Se connecter** et spécifiez un compte d’administrateur général Azure. Comme pour l’application web, ces informations d’identification ne sont pas enregistrées et ne nécessitent pas d’autorisations dans Configuration Manager.
   
   Une fois que vous êtes connecté, les résultats s’affichent. Sélectionnez **OK** pour fermer la boîte de dialogue Créer une application cliente et revenir à la page Propriétés de l’application. Sélectionnez **Suivant** pour continuer.

5. Sur la page **Configurer les paramètres de découverte**, cochez la case **Activer la découverte des utilisateurs Azure Active Directory**, sélectionnez **Suivant**, puis terminez la configuration des boîtes de dialogue de découverte pour votre environnement.  

6. Continuez sur les pages Résumé, Progression et Fin, puis fermez l’Assistant.  

   Les services Azure pour la découverte des utilisateurs Azure AD est maintenant activée dans Configuration Manager.  Laissez la console ouverte pour l’instant.  

7. Ouvrez un navigateur et connectez-vous au [portail Azure](https://portal.azure.com/).  

8. Sélectionnez **Tous les services > Azure Active Directory > Inscriptions d’applications**, puis :

   1. Sélectionnez l’application web que vous avez créée. 

   2. Accédez à **Paramètres > Autorisations nécessaires**, sélectionnez **Accorder des autorisations**, puis sélectionnez **Oui**.  

   3. Sélectionnez l’application cliente native que vous avez créée. 

   4. Accédez à **Paramètres > Autorisations nécessaires**, sélectionnez **Accorder des autorisations**, puis sélectionnez **Oui**.  

9. Dans la console Configuration Manager, accédez à **Administration > Vue d’ensemble > Services cloud > Services Azure**, puis sélectionnez votre service Azure. Ensuite, cliquez avec le bouton droit sur **Découverte des utilisateurs Azure Active Directory** et sélectionnez **Exécuter la découverte complète maintenant**. Sélectionnez **Oui** pour confirmer l’action.  

10. Sur le serveur de site principal, ouvrez le fichier **SMS_AZUREAD_DISCOVERY_AGENT.log** Configuration Manager et recherchez l’entrée suivante pour confirmer que la détection fonctionne :  *UDX publiée avec succès pour les utilisateurs Azure Active Directory*  

    Par défaut, le chemin du fichier journal est *%Program_Files%\Microsoft Configuration Manager\Logs*.  


## <a name="create-the-cloud-services-in-azure"></a>Créer les services cloud dans Azure
**Dans cette section du tutoriel, vous allez** :
- Créer le service cloud de passerelle de gestion cloud  
- Créer des enregistrements DNS CNAME pour les deux services  

### <a name="create-the-cmg"></a>Créer la passerelle CMG
Utilisez cette procédure pour installer une passerelle de gestion cloud en tant que service dans Azure. La passerelle CMG s’installe sur le site de niveau supérieur de la hiérarchie. Dans ce tutoriel, nous continuons d’utiliser le site principal où les certificats ont été inscrits et exportés.

1. Sur le serveur de site principal, ouvrez la console Configuration Manager et puis accédez **Administration > Vue d’ensemble > Services cloud > Passerelle de gestion cloud**, puis sélectionnez **Créer une passerelle de gestion cloud**.  

2. Sur la page **Général** :  

   1. Sélectionnez votre environnement cloud pour **l’environnement Azure**. Ce tutoriel utilise **AzurePublicCloud**.  
   
   2. Sélectionnez **Déploiement d’Azure Resource Manager**.  
  
   3. **Connectez-vous** à votre abonnement Azure. Configuration Manager fournit des informations supplémentaires en fonction des informations vous avez configurées lorsque vous avez activé les services cloud Azure pour Configuration Manager.  

   Sélectionnez **Suivant** pour continuer.  

3. Sur la page **Paramètres**, recherchez et sélectionnez le fichier nommé **ConfigMgrCloudMGServer.pfx**, c’est-à-dire le fichier que vous avez exporté après avoir importé le certificat de d’authentification serveur de passerelle de gestion cloud. Après avoir spécifié le mot de passe, le **nom du service** et le **nom du déploiement** se renseignent automatiquement, selon les détails du fichier de certificat .pfx. 

4. Choisissez votre **Région**.

5. Pour **Groupe de ressources**, utilisez un groupe de ressources existant ou créez un groupe avec un nom convivial sans espaces, comme **CofigMgrCloudServices**. Si vous choisissez de créer un groupe, il est ajouté en tant que groupe de ressources dans Azure.  

6. Sauf si vous êtes prêt à configurer à l’échelle, utilisez un (1) pour le nombre **d’instances de machine virtuelle**. Le nombre d’instances de machine virtuelle permet à un service cloud de passerelle de gestion cloud (CMG) unique de monter en charge (scale out) pour prendre en charge davantage de connexions client. Plus tard, vous pourrez utiliser la console Configuration Manager pour retourner et modifier le nombre d’instances de machine virtuelle que vous utilisez.  

7. Cochez la case **Vérifier la révocation de certificat client**. 

8. Cochez la case **Autoriser la passerelle de gestion cloud à fonctionner comme un point de distribution cloud et à présenter du contenu à partir du Stockage Azure** si vous souhaitez déployer un point de distribution cloud avec la passerelle CMG.

9. Sélectionnez **Suivant** pour continuer.

10. Passez en revue les valeurs de la page **Alerte**, puis sélectionnez **Suivant**.

11. Examinez la page **Résumé** et cliquez sur **Suivant** pour créer le service cloud de passerelle de gestion cloud. Sélectionnez **Fermer** pour terminer l’Assistant.  

12. Dans le nœud Passerelle de gestion cloud de la console Configuration Manager, vous pouvez désormais voir le nouveau service.  

### <a name="create-dns-cname-records"></a>Créer des enregistrements DNS CNAME

Lorsque vous créez une entrée DNS pour la passerelle CMG, vous activez vos appareils Windows 10 à l’intérieur et à l’extérieur de votre réseau d’entreprise à utiliser la résolution de nom pour rechercher le service cloud de passerelle de gestion cloud dans Azure.

Notre exemple d’enregistrement CNAME utilise les informations suivantes :  

- Le nom de l’entreprise est **Contoso** avec un espace de noms DNS public ***Contoso.com***.  

- Le nom du service de passerelle de gestion cloud est **MyCMG**, qui devient ***MyCMG.CloudApp.Net*** dans Azure.  

Exemple d’enregistrement CNAME : *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Configurer le point de gestion et les clients pour utiliser la CMG
Configurez les paramètres qui permettent aux points de gestion locaux et aux clients d’utiliser la passerelle de gestion cloud. 

Étant donné que nous utilisons le protocole HTTP amélioré pour les communications clientes, il est inutile d’utiliser un point de gestion HTTPS.  

### <a name="create-the-cmg-connection-point"></a>Créer le point de connexion CMG
Configurez le site pour prendre en charge le protocole HTTP amélioré.  

1. Dans la console Configuration Manager, accédez à **Administration > Vue d’ensemble > Configuration du site > Sites**, ouvrez les propriétés du site principal.  

2. Dans l’onglet **Communication de l’ordinateur client**, sélectionnez l’option *HTTPS ou HTTP* pour **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**, puis sélectionnez **OK** pour enregistrer la configuration. 

3. Accédez maintenant à **Administration > Vue d’ensemble > Configuration du site > Serveurs et rôles de système de site** et sélectionnez le serveur avec un point de gestion où vous souhaitez installer le point de connexion de la passerelle de gestion cloud.  

4. Sélectionnez **Ajouter des rôles de système de site**, puis **Suivant**> **Suivant**.  

5. Sélectionnez le **point de connexion de la passerelle de gestion Cloud**, puis sélectionnez **Suivant** pour continuer.  

6. Passez en revue les sélections par défaut de la page **Point de connexion de la passerelle de gestion cloud** et vérifiez que la passerelle CMG correcte est sélectionnée. Si vous avez plusieurs passerelles de gestion cloud, vous pouvez utiliser la liste déroulante pour spécifier une autre passerelle de gestion cloud. Vous pouvez également modifier la passerelle CMG en cours d’utilisation, après l’installation. Sélectionnez **Suivant** pour continuer.

7. Sélectionnez **Suivant** pour démarrer l’installation, puis consultez les résultats sur la page Fin.  Sélectionnez **Fermer** pour terminer l’installation du point de connexion. 

8. Accédez maintenant à **Administration > Vue d’ensemble > Configuration du site > Serveurs et rôles de système de site** et ouvrez les **Propriétés** pour le point de gestion où vous avez installé le point de connexion. Sur l’ongle **Général**, cochez la case **Autoriser le trafic de la passerelle de gestion de cloud Configuration Manager**, puis sélectionnez **OK** pour enregistrer la configuration. 
   > [!TIP]  
   > Bien que cela ne soit pas nécessaire pour activer la cogestion, nous vous recommandons d’apporter cette même modification pour tous les points de mise à jour logicielle. 

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Configurer les paramètres client de façon à conduire les clients à utiliser la passerelle CMG
Utilisez les paramètres client pour configurer les clients Configuration Manager de sorte qu’ils communiquent avec la passerelle CMG.  

1. Ouvrez la **Console Configuration Manager > Administration > Vue d’ensemble > Paramètres client**, puis modifiez les **Paramètres client par défaut**.  

2. Sélectionnez **Services cloud**.

3. Sur la page **Paramètres par défaut**, définissez les paramètres suivants sur = **Oui**  

   - **Inscrire automatiquement les nouveaux appareils joints au domaine Windows 10 auprès d’Azure Active Directory**  

   - **Autoriser les clients à utiliser une passerelle de gestion cloud** 

   - **Autoriser l’accès au point de distribution cloud** 

4. Sur la page **Stratégie client**, définissez **Autoriser les demandes de stratégies utilisateurs provenant de clients Internet** = **Oui** 

1. Sélectionnez **OK** pour enregistrer cette configuration. 



## <a name="enable-co-management-in-configuration-manager"></a>Activer la cogestion dans Configuration Manager
Une fois les configurations, les rôles de système de site et les paramètres Azure en place, vous pouvez configurer Configuration Manager pour activer la cogestion. Toutefois, vous devrez effectuer quelques configurations dans Intune après avoir activé la cogestion avant la fin de ce tutoriel. L’une de ces tâches consiste à configurer Intune pour déployer le client Configuration Manager. Cette tâche est facilitée par l’enregistrement de la ligne de commande pour le déploiement client qui est disponible dans l’Assistant Configuration de la cogestion. C’est pourquoi nous activons la cogestion maintenant, avant de finaliser les configurations pour Intune. 

> [!TIP]  
>  À l’étape six de la procédure suivante, vous allez désigner un regroupement comme *Groupe pilote* pour la cogestion. Il s’agit d’un groupe qui contient un petit nombre de clients permettant de tester les configurations de cogestion. Nous recommandons de créer un regroupement adapté avant de commencer la procédure. Vous pourrez alors le sélectionner sans avoir à quitter la procédure.  
 
1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Cogestion**.

2. Dans le groupe Gérer sous l’onglet Accueil, sélectionnez **Configurer la cogestion** pour ouvrir l’Assistant Configuration de la cogestion.

3. Sur la page *Abonnement*, sélectionnez **Se connecter** et connectez-vous à votre locataire Intune, puis sélectionnez **Suivant**.

4. Sur la page *Activation*, sélectionnez l’une des options suivantes dans la liste déroulante *Inscription automatique dans Intune* :  

   - **Pilote**  -  *(recommandé)* Membres du regroupement qui seront automatiquement inscrits dans Intune et pourront alors être cogérés. Spécifiez le regroupement pilote sur la page *Gestion intermédiaire* de cet Assistant. Cette option permet de tester la cogestion sur un sous-ensemble de clients. Vous pourrez ensuite déployer la cogestion auprès de clients supplémentaires suivant une approche progressive.  

   - **Tous** – Cogestion activée pour tous les clients.  

   Avant de passer à la page suivante de l’Assistant, sélectionnez **Copier** et enregistrez la ligne de commande CCMSetup fournie. Vous utiliserez la ligne de commande ultérieurement lors de la configuration d’Intune pour déployer le client Configuration Manager. Si vous n’enregistrez pas maintenant cette ligne de commande, vous pouvez examiner la configuration de la cogestion à tout moment pour obtenir cette ligne de commande. 

5. Sur la page *Charges de travail*, vous pouvez basculer les charges de travail de **Configuration Manager** à l’une des options suivantes ; ensuite, sélectionnez **Suivant** pour continuer.  
   
   - **Pilote Intune** – Bascule la charge de travail uniquement pour les appareils du groupe pilote. Un regroupement sera désigné comme groupe pilote sur la page suivante de l’Assistant.  
   
   - **Intune** – Bascule la charge de travail associée pour tous les appareils Windows 10 cogérés.  

   Il n’est pas nécessaire de basculer des charges de travail dès l’activation de la cogestion. Vous pourrez revenir consulter cette configuration plus tard à partir de la console Configuration Manager, après avoir configuré la cogestion.  

   Avant de basculer une charge de travail, vérifiez que la charge de travail correspondante dans Intune est correctement configurée et déployée. Ainsi, les charges de travail resteront gérées.  

6. Sur la page *Gestion intermédiaire*, spécifiez le regroupement à utiliser comme **Regroupement pilote**, puis cliquez sur **Suivant**. Il sera utilisé dans le cadre du déploiement progressif de la cogestion. À tout moment, vous pouvez modifier les regroupements dans le groupe pilote à partir des propriétés de cogestion.  

7. Sur la page *Résumé*, sélectionnez **Suivant**, puis **Fermer** pour terminer l’Assistant.  

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Utiliser Intune pour déployer le client Configuration Manager
Vous pouvez utiliser Intune pour installer le client Configuration Manager sur les appareils Windows 10 qui sont actuellement gérés uniquement via Intune.  

Ensuite, quand un appareil Windows 10 précédemment non géré s’inscrit auprès d’Intune, il installe automatiquement le client Configuration Manager.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Créer une application Intune pour installer le client Configuration Manager

1. À partir du serveur de site principal, connectez-vous au [portail Azure](https://portal.azure.com/) et accédez à **Intune > Applications clientes > Applications > Ajouter**.

2. Pour **Type d'application** : Sélectionnez **Application métier**.

3. Sélectionnez **Fichier package d’application**, puis accédez à l’emplacement du fichier Configuration Manager **ccmsetup.msi**, puis sélectionnez **Ouvrir > OK**.
Par exemple, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*   

4. Sélectionnez **Informations sur l’application**, puis spécifiez les détails suivants :
   - **Description** : Client Configuration Manager  

   - **Éditeur** : Microsoft  

   - **Arguments de ligne de commande** :  *\<Spécifiez la ligne de commande **CCMSETUPCMD**. Vous pouvez utiliser la ligne de commande que vous avez enregistrée à partir de la page* Activation *de l’Assistant Configuration de la cogestion. Cette ligne de commande inclut le nom de votre service cloud et des valeurs supplémentaires qui permettent à des appareils d’installer le logiciel client Configuration Manager.>*  

     La structure de ligne de commande doit ressembler à cet exemple utilisant uniquement les paramètres CCMSETUPCMD et SMSSiteCode :  

     ```
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Si la ligne de commande n’est pas disponible, vous pouvez afficher les propriétés de *CoMgmtSettingsProd* dans la console Configuration Manager pour obtenir une copie de la ligne de commande.    

5. Sélectionnez **OK > Ajouter**.  L’application est créée et devient disponible dans la console Intune. Une fois que l’application est disponible, vous pouvez utiliser la section suivante pour configurer Intune qui l’attribuera aux appareils Windows 10.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Attribuer l’application Intune pour installer le client Configuration Manager
La procédure suivante déploie l’application pour l’installation du client Configuration Manager que vous avez créé dans la procédure précédente. 

1. Connectez-vous au [portail Azure](https://portal.azure.com/).  Sélectionnez **Tous les services > Intune > Applications clientes > Applications**, puis sélectionnez **ConfigMgr Client Setup Bootstrap**, l’application que vous avez créée pour déployer le client Configuration Manager.  

2. Sélectionnez **Attributions > Ajouter un groupe**.  Définissez le **Type d’attribution** sur **Requis**, puis utilisez **Groupes inclus** et **Groupes exclus** pour définir les groupes Azure Active Directory (AD) qui ont des utilisateurs et des appareils qui doivent participer à la cogestion.  

3. Sélectionnez **OK** et **enregistrez** la configuration.
L’application est désormais requise par les utilisateurs et appareils auxquels vous l’avez attribuée. Une fois que l’application installe le client Configuration Manager sur un appareil, il est géré par la cogestion.

## <a name="assign-intune-licenses-to-users"></a>Attribuer des licences Intune aux utilisateurs   
Il est essentiel, quoique souvent négligé, d’attribuer une licence Intune à chacun des utilisateurs qui utilisent un appareil cogéré.  

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

8. En haut à droite, une notification présente l’état et le résultat du processus. Si l’attribution au groupe n’a pas abouti (par exemple, en raison de licences préexistantes dans le groupe), cliquez sur la notification pour afficher les détails de l’échec. 


## <a name="summary"></a>Résumé 
Après avoir terminé les étapes de configuration de ce tutoriel, notamment la dernière action pour vous assurer que les licences sont attribuées, vos appareils peuvent être cogérés. 

## <a name="next-steps"></a>Étapes suivantes
- Passer en revue l’état des appareils cogérés avec le [Tableau de bord de cogestion](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard)
- Utiliser [Windows Autopilot](/sccm/comanage/quickstart-autopilot) pour configurer de nouveaux appareils
- Utiliser [l’accès conditionnel](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access) et les règles de conformité Intune pour gérer l’accès utilisateur aux ressources de l’entreprise
