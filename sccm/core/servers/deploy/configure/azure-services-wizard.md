---
title: Configurer les services Azure
titleSuffix: Configuration Manager
description: Connectez votre environnement Configuration Manager aux services Azure pour la gestion cloud, Upgrade Readiness, Microsoft Store pour Entreprises et Log Analytics.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1e6ef01d38b9359bbb82449ad045312e58646475
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676696"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurer les services Azure à utiliser avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez **l’Assistant Services Azure** pour simplifier le processus de configuration des services cloud Azure que vous utilisez avec Configuration Manager. Cet Assistant fournit une expérience de configuration commune en utilisant des inscriptions d’applications web Azure AD (Azure Active Directory). Ces applications fournissent des détails d’abonnement et de configuration, et authentifient les communications avec Azure AD. Grâce à cette application, vous n’avez pas besoin d’entrer ces mêmes informations chaque fois que vous configurez un nouveau composant ou service Configuration Manager avec Azure.



## <a name="available-services"></a>Services disponibles

Configurez les services Azure suivants à l’aide de cet Assistant :  

-   **Gestion cloud** : ce service permet aux clients et au site de s’authentifier à l’aide d’Azure AD. Cette authentification permet d’autres scénarios, par exemple :  

    - [Installer et attribuer des clients Configuration Manager exécutant Windows 10 avec Azure AD pour l’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configurer la découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Prendre en charge certains [scénarios de passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **Connecteur Log Analytics** : [connectez-vous à Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics). Synchronisez les données de regroupement avec Log Analytics.  

    > [!Note]  
    > Cet article fait référence au *Connecteur Log Analytics*, précédemment appelé *Connecteur OMS*. Il n’existe aucune différence fonctionnelle. Pour plus d’informations, consultez [Gestion Azure - Surveillance](/azure/azure-monitor/terminology#log-analytics).  

-   **Connecteur Upgrade Readiness** : connectez-vous à [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) dans Windows Analytics. Consultez les données de compatibilité de mise à niveau des clients.  

-   **Microsoft Store pour Entreprises** : connectez-vous au [Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Obtenez des applications du Store pour votre organisation que vous pouvez déployer avec Configuration Manager.  

### <a name="service-details"></a>Détails sur le service

Le tableau suivant répertorie des informations sur chacun des services.  

- **Locataires** : nombre d’instances de service que vous pouvez configurer. Chaque instance doit être un locataire Azure distinct.  

- **Clouds** : tous les services prennent en charge le cloud Azure global, mais les services ne prennent pas tous en charge les clouds privés, tels que le cloud Azure US Government.  

- **Application web** : indique si le service utilise une application Azure AD de type *Application/API web*, également appelée application serveur dans Configuration Manager.  

- **Application native** : indique si le service utilise une application Azure AD de type *Native*, également appelée application cliente dans Configuration Manager.  

- **Actions** : indique si vous pouvez importer ou créer ces applications dans l’Assistant Services Azure Configuration Manager.  


|Service  |Locataires  |Clouds  |Application web  |Application native  |Actions  |
|---------|---------|---------|---------|---------|---------|
|Gestion cloud avec<br>découverte d’utilisateurs Azure AD | Plusieurs | Public, privé | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | Importer, Créer |
|Connecteur Log Analytics | Un | Public, privé | ![Pris en charge](media/green_check.png) | ![Non pris en charge](media/Red_X.png) | Importation |
|Upgrade Readiness | Un | Public | ![Pris en charge](media/green_check.png) | ![Non pris en charge](media/Red_X.png) | Importation |
|Microsoft Store pour<br>Entreprises | Un | Public | ![Pris en charge](media/green_check.png) | ![Non pris en charge](media/Red_X.png) | Importer, Créer |


### <a name="about-azure-ad-apps"></a>À propos des applications Azure AD

Des services Azure différents nécessitent des configurations distinctes, que vous définissez dans le portail Azure. En outre, les applications pour chaque service peuvent nécessiter des autorisations distinctes sur des ressources Azure.  

Vous pouvez utiliser une seule application pour plusieurs services. Il n’existe qu’un seul objet à gérer dans Configuration Manager et Azure AD. Quand la clé de sécurité de l’application expire, il vous suffit d’actualiser une clé.

<!-- The most secure configuration is using separate apps for each service. An app for one service might require additional permissions that another service doesn't require. Using one app for different services can provide the app with more permissions than it otherwise requires. 
 --> 

Quand vous créez des services Azure supplémentaires dans l’Assistant, Configuration Manager est conçu pour réutiliser les informations qui sont communes aux services. Ce comportement vous évite d’avoir à entrer les mêmes informations plusieurs fois. 

Pour plus d’informations sur les autorisations d’application nécessaires et les configurations pour chaque service, consultez l’article Configuration Manager approprié dans [Services disponibles](#available-services). 

Pour plus d’informations sur les applications Azure, commencez par les articles suivants :
- [Authentification et autorisation dans Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Vue d’ensemble des applications web](/azure/app-service-web/app-service-web-overview)
- [Concepts de base de l’inscription d’une application dans Azure AD](/azure/active-directory/develop/authentication-scenarios#authentication-basics-in-microsoft-identity-platform)  
- [Inscrire une application auprès de votre locataire Azure Active Directory](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Avant de commencer

Après avoir choisi le service auquel vous souhaitez vous connecter, reportez-vous au tableau dans [Détails sur le service](#service-details). Ce tableau fournit les informations nécessaires pour terminer l’Assistant Services Azure. Ayez préalablement une discussion avec votre administrateur Azure AD. Déterminez, parmi les actions suivantes, celles à effectuer : 

- Créez manuellement les applications à l’avance dans le portail Microsoft Azure. Importez ensuite les détails d’application dans Configuration Manager.  

- Utilisez Configuration Manager pour créer directement les applications dans Azure AD. Pour collecter les données nécessaires à partir d’Azure AD, passez en revue les informations contenues dans les autres sections de cet article.  

Certains services nécessitent que les applications Azure AD disposent d’autorisations spécifiques. Passez en revue les informations pour chaque service afin de déterminer les autorisations requises. Par exemple, avant de pouvoir importer une application web, un administrateur Azure doit tout d’abord la créer dans le [portail Azure](https://portal.azure.com). 

Lors de la configuration du connecteur Upgrade Readiness ou Log Analytics, donnez à votre application web tout juste inscrite une autorisation de *contributeur* sur le groupe de ressources qui contient l’espace de travail approprié. Cette autorisation permet à Configuration Manager d’accéder à cet espace de travail. Au moment d’attribuer l’autorisation, recherchez le nom de l’inscription d’application dans le panneau **Ajouter des utilisateurs** du portail Azure. Ce processus est le même que lors de la [fourniture à Configuration Manager d’autorisations sur Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Un administrateur Azure doit attribuer ces autorisations avant que vous n’importiez l’application dans Configuration Manager.



## <a name="start-the-azure-services-wizard"></a>Démarrer l’Assistant Services Azure

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**.  

2. Sous l’onglet **Accueil** du ruban, dans le groupe **Services Azure**, sélectionnez **Configurer les services Azure**.  

3. Dans la page **Services Azure** de l’Assistant Services Azure :  

    1. Spécifiez un **Nom** pour l’objet dans Configuration Manager.  

    2. Spécifiez une **Description** facultative pour vous aider à identifier le service.  

    3. Sélectionnez le service Azure que vous souhaitez connecter à Configuration Manager.  

4. Sélectionnez **Suivant** pour passer à la page [Propriétés de l’application Azure](#azure-app-properties) de l’Assistant Services Azure.  



## <a name="azure-app-properties"></a>Propriétés de l’application Azure

Dans la page **Application** de l’Assistant Services Azure, sélectionnez d’abord **l’environnement Azure** dans la liste. Reportez-vous au tableau dans [Détails sur le service](#service-details) pour connaître l’environnement actuellement disponible pour le service.

Le reste de la page Application varie selon le service spécifique. Reportez-vous au tableau dans [Détails sur le service](#service-details) pour connaître le type d’application utilisé par le service et l’action que vous pouvez effectuer. 

- Si l’application prend en charge les deux actions Importer et Créer, sélectionnez **Parcourir**. Cette action ouvre la [boîte de dialogue Application serveur](#server-app-dialog) ou la [boîte de dialogue Application cliente](#client-app-dialog).  

- Si l’application prend uniquement en charge l’action Importer, sélectionnez **Importer**. Cette action ouvre la [boîte de dialogue Importer des applications (serveur)](#import-apps-dialog-server) ou la [boîte de dialogue Importer des applications (client)](#import-apps-dialog-client).

Après avoir spécifié les applications dans cette page, sélectionnez **Suivant** pour passer à la page [Configuration ou Découverte](#configuration-or-discovery) de l’Assistant Services Azure.

### <a name="web-app"></a>Application web

Il s’agit d’une application Azure AD de type *Application/API web*, également appelée application serveur dans Configuration Manager.

#### <a name="server-app-dialog"></a>Boîte de dialogue Application serveur

Quand vous sélectionnez **Parcourir** pour **Application web** dans la page Application de l’Assistant Services Azure, la boîte de dialogue Application serveur s’ouvre. Il affiche une liste qui indique les propriétés suivantes de toutes les applications web existantes :
- Nom convivial du locataire
- Nom convivial de l’application
- Type de service

Il existe trois actions possibles à partir de la boîte de dialogue Application serveur :
- Pour réutiliser une application web existante, sélectionnez-la dans la liste. 
- Sélectionnez **Importer** pour ouvrir la [boîte de dialogue Importer des applications](#import-apps-dialog-server).
- Sélectionnez **Créer** pour ouvrir la [boîte de dialogue Créer une application serveur](#create-server-application-dialog).

Après avoir sélectionné, importé ou créé une application web, sélectionnez **OK** pour fermer la boîte de dialogue Application serveur. Cette action renvoie à la [page Application](#azure-app-properties) de l’Assistant Services Azure.

#### <a name="import-apps-dialog-server"></a>Boîte de dialogue Importer des applications (serveur)

Quand vous sélectionnez **Importer** dans la boîte de dialogue Application serveur ou la page Application de l’Assistant Services Azure, la boîte de dialogue Importer des applications s’ouvre. Cette page vous permet d’entrer des informations sur une application web Azure AD qui est déjà créée dans le portail Azure. Les métadonnées relatives à cette application web sont importées dans Configuration Manager. Spécifiez les informations suivantes :
- **Nom du locataire Azure AD**
- **ID de locataire Azure AD**
- **Nom de l'application** : nom convivial de l’application.
- **ID de client**
- **Clé secrète**
- **Expiration de la clé secrète** : sélectionnez une date ultérieure dans le calendrier. 
- **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Elle se trouve dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est https\://ConfigMgrService.  

Après avoir entré les informations, sélectionnez **Vérifier**. Sélectionnez ensuite **OK** pour fermer la boîte de dialogue Importer des applications. Cette action renvoie à la [page Application](#azure-app-properties) de l’Assistant Services Azure ou à la [boîte de dialogue Application serveur](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Boîte de dialogue Créer une application serveur

Quand vous sélectionnez **Créer** dans la boîte de dialogue Application serveur, la boîte de dialogue Créer une application serveur s’ouvre. Cette page permet d’automatiser la création d’une application web dans Azure AD. Spécifiez les informations suivantes :
- **Nom de l'application** : nom convivial de l’application.
- **URL de la page d'accueil** : cette valeur n’est pas utilisée par Configuration Manager, mais elle est exigée par Azure AD. Par défaut, cette valeur est https\://ConfigMgrService.  
- **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Elle se trouve dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est https\://ConfigMgrService.  
- **Période de validité de la clé secrète** : choisissez **1 an** ou **2 ans** dans la liste déroulante. Un an est la valeur par défaut.

Sélectionnez **Se connecter** pour vous authentifier auprès d’Azure en tant qu’utilisateur administratif. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure. Après vous être authentifié correctement auprès d’Azure, la page affiche le **Nom du locataire Azure AD** pour référence. 

Sélectionnez **OK** pour créer l’application web dans Azure AD et fermer la boîte de dialogue Créer une application serveur. Cette action renvoie à la [boîte de dialogue Application serveur](#server-app-dialog).


### <a name="native-client-app"></a>Application cliente native

Il s’agit d’une application Azure AD de type *Native*, également appelée application cliente dans Configuration Manager.

#### <a name="client-app-dialog"></a>Boîte de dialogue Application cliente

Quand vous sélectionnez **Parcourir** pour **Application cliente native** dans la page Application de l’Assistant Services Azure, la boîte de dialogue Application cliente s’ouvre. Il affiche une liste qui indique les propriétés suivantes de toutes les applications natives existantes :
- Nom convivial du locataire
- Nom convivial de l’application
- Type de service

Il existe trois actions possibles à partir de la boîte de dialogue Application cliente :
- Pour réutiliser une application native existante, sélectionnez-la dans la liste. 
- Sélectionnez **Importer** pour ouvrir la [boîte de dialogue Importer des applications](#import-apps-dialog-client).
- Sélectionnez **Créer** pour ouvrir la [boîte de dialogue Créer une application cliente](#create-client-application-dialog).

Après avoir sélectionné, importé ou créé une application native, choisissez **OK** pour fermer la boîte de dialogue Application cliente. Cette action renvoie à la [page Application](#azure-app-properties) de l’Assistant Services Azure.

#### <a name="import-apps-dialog-client"></a>Boîte de dialogue Importer des applications (client)

Quand vous sélectionnez **Importer** dans la boîte de dialogue Application cliente, la boîte de dialogue Importer des applications s’ouvre. Cette page vous permet d’entrer des informations sur une application native Azure AD qui est déjà créée dans le portail Azure. Les métadonnées relatives à cette application native sont importées dans Configuration Manager. Spécifiez les informations suivantes :
- **Nom de l'application** : nom convivial de l’application.
- **ID de client** 

Après avoir entré les informations, sélectionnez **Vérifier**. Sélectionnez ensuite **OK** pour fermer la boîte de dialogue Importer des applications. Cette action renvoie à la [boîte de dialogue Application cliente](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Boîte de dialogue Créer une application cliente

Quand vous sélectionnez **Créer** dans la boîte de dialogue Application cliente, la boîte de dialogue Créer une application cliente s’ouvre. Cette page permet d’automatiser la création d’une application native dans Azure AD. Spécifiez les informations suivantes :
- **Nom de l'application** : nom convivial de l’application.
- **URL de réponse** : cette valeur n’est pas utilisée par Configuration Manager, mais elle est exigée par Azure AD. Par défaut, cette valeur est https\://ConfigMgrService. 

Sélectionnez **Se connecter** pour vous authentifier auprès d’Azure en tant qu’utilisateur administratif. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure. Après vous être authentifié correctement auprès d’Azure, la page affiche le **Nom du locataire Azure AD** pour référence. 

Sélectionnez **OK** pour créer l’application native dans Azure AD et fermer la boîte de dialogue Créer une application cliente. Cette action renvoie à la [boîte de dialogue Application cliente](#client-app-dialog).


### <a name="renew-secret-key-azure-ad-apps"></a>Renouveler la clé secrète des applications Azure AD
Avant la version 1806, pour renouveler la clé secrète d’une application Azure, vous deviez recréer l’application.

Sur la version 1806 et les versions ultérieures :

- Application créée : Sous **Cloud Services node** (Nœud des services cloud), accédez à **Azure Active Directory Tenants** (Locataires Azure Active Directory). Dans le volet de détails, sélectionnez le locataire sur lequel l’application a été créée, puis choisissez **Renew Secret Key** (Renouveler la clé secrète).  

    - Sélectionnez **Se connecter** pour vous authentifier auprès d’Azure en tant qu’utilisateur administratif.  

    - Sélectionnez **OK** pour créer l’application native dans Azure AD et fermer la boîte de dialogue Créer une application cliente. Cette action renvoie à la [boîte de dialogue Application cliente](#client-app-dialog).  

- Application importée : utilisez le portail Azure pour renouveler la clé secrète, puis notez la nouvelle clé secrète et sa date d’expiration. Ajoutez ces informations dans l’Assistant **Renouveler la clé secrète**.  

> [!Note]  
> Enregistrez la clé secrète avant de fermer la page des propriétés de la **clé** de l’application Azure. Ces informations sont supprimées lorsque vous fermez la page.


## <a name="configuration-or-discovery"></a>Configuration ou Découverte

Après avoir spécifié les applications natives et web dans la page des applications, l’Assistant Services Azure passe à la page **Configuration** ou **Découverte**, selon le service auquel vous vous connectez. Les détails de cette page varient d’un service à l’autre. Pour plus d’informations, consultez l’un des articles suivants :  

-   Service **Gestion du cloud**, page **Découverte** : [Configurer la découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   Service **Connecteur Log Analytics**, page **Configuration** : [Configurer la connexion à Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics#configure-the-connection-to-log-analytics)  

-   Service **Connecteur Upgrade Readiness**, page **Configuration** : [Utiliser l’Assistant Azure pour créer la connexion](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   Service **Microsoft Store pour Entreprises**, page **Configurations** : [Configurer la synchronisation du Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_config)  


Pour finir, terminez l’Assistant Services Azure via les pages de résumé, de progression et de fin. Vous avez terminé la configuration du service Azure dans Configuration Manager. Répétez ce processus pour configurer d’autres services Azure.


## <a name="view-the-configuration-of-an-azure-service"></a>Afficher la configuration d’un service Azure
Affichez les propriétés du service Azure que vous avez configuré en vue de son utilisation. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Services Azure**. Sélectionnez le service que vous souhaitez voir ou modifier, puis sélectionnez **Propriétés**.

Si vous sélectionnez un service, puis choisissez **Supprimer** dans le ruban, cette action supprime la connexion dans Configuration Manager. Elle ne supprime pas l’application dans Azure AD. Demandez à votre administrateur Azure de supprimer l’application quand elle est devenue inutile. Vous pouvez aussi exécuter l’Assistant Services Azure pour importer l’application.<!--483440-->


## <a name="cloud-management-data-flow"></a>Flux de données de gestion cloud

Le diagramme suivant est un flux de données conceptuel pour l’interaction entre Configuration Manager, Azure AD et des services cloud connectés. Cet exemple utilise le service de **gestion cloud**, qui inclut un client Windows 10 ainsi que des applications serveur et clientes. Les flux sont similaires pour d’autres services.

![Diagramme de flux de données pour Configuration Manager avec Azure AD et gestion cloud](media/aad-auth.png)

1. L’administrateur Configuration Manager importe ou crée les applications serveur et clientes dans Azure AD.  

2. La méthode de découverte d’utilisateurs Azure AD de Configuration Manager s’exécute. Le site utilise le jeton d’application serveur Azure AD pour rechercher des objets utilisateur dans Microsoft Graph.  

3. Le site stocke des données sur les objets utilisateur. Pour plus d’informations, consultez [Découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  Le client Configuration Manager demande le jeton d’utilisateur Azure AD. Le client génère la revendication à l’aide de l’ID de l’application cliente Azure AD et de l’application serveur comme audience. Pour plus d’informations, consultez [Revendications des jetons de sécurité Azure AD](/azure/active-directory/develop/authentication-scenarios#claims-in-microsoft-identity-platform-security-tokens).  

5.  Le client s’authentifie auprès du site en présentant le jeton Azure AD à la passerelle de gestion cloud et/ou au point de gestion HTTPS local.  


