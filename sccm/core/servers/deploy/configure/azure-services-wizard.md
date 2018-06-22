---
title: Configurer les services Azure
titleSuffix: Configuration Manager
description: Connectez votre environnement Configuration Manager aux services Azure pour la gestion cloud, Upgrade Readiness, Microsoft Store pour Entreprises et Operations Management Suite.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ff953d658c54c2cebbbfd29a6bba83fe65cc08e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342339"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurer les services Azure à utiliser avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez **l’Assistant Services Azure** pour simplifier le processus de configuration des services cloud Azure que vous utilisez avec Configuration Manager. Cet Assistant fournit une expérience de configuration commune en utilisant des inscriptions d’applications web Azure AD (Azure Active Directory). Ces applications fournissent des détails d’abonnement et de configuration, et authentifient les communications avec Azure AD. Grâce à cette application, vous n’avez pas besoin d’entrer ces mêmes informations chaque fois que vous configurez un nouveau composant ou service Configuration Manager avec Azure.



## <a name="available-services"></a>Services disponibles

Configurez les services Azure suivants à l’aide de cet Assistant :  

-   **Gestion cloud** : Ce service permet aux clients et au site de s’authentifier à l’aide d’Azure AD. Cette authentification permet d’autres scénarios, par exemple :  

    - [Installer et attribuer des clients Configuration Manager exécutant Windows 10 avec Azure AD pour l’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configurer la découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Prendre en charge certains [scénarios de passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **Connecteur OMS** : [Connectez-vous à Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS). Synchronisez des données telles que des regroupements avec OMS Log Analytics.  

-   **Connecteur Upgrade Readiness** : Connectez-vous à [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) dans Windows Analytics. Consultez les données de compatibilité de mise à niveau des clients.  

-   **Microsoft Store pour Entreprises** : Connectez-vous au [Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Obtenez des applications du Store pour votre organisation que vous pouvez déployer avec Configuration Manager.  

### <a name="service-details"></a>Détails sur le service

Le tableau suivant répertorie des informations sur chacun des services.  

- **Locataires** : nombre d’instances de service que vous pouvez configurer. Chaque instance doit être un locataire Azure distinct.  

- **Clouds** : tous les services prennent en charge le cloud Azure global, mais les services ne prennent pas tous en charge les clouds privés, tels que le cloud Azure US Government.  

- **Application web** : indique si le service utilise une application Azure AD de type *Application/API web*, également appelée application serveur dans Configuration Manager.  

- **Application native** : indique si le service utilise une application Azure AD de type *Native*, également appelée application cliente dans Configuration Manager.  

- **Actions** : indique si vous pouvez importer ou créer ces applications dans l’Assistant Services Azure Configuration Manager.  


|Service  |Locataires  |Clouds  |Application web  |Application native  |Actions  |
|---------|---------|---------|---------|---------|---------|
|Gestion cloud avec</br>découverte d’utilisateurs Azure AD | Plusieurs | Public | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | Importer, Créer |
|Connecteur OMS | Un | Public, privé | ![Pris en charge](media/green_check.png) | ![Non pris en charge](media/Red_X.png) | Importation |
|Upgrade Readiness | Un | Public | ![Pris en charge](media/green_check.png) | ![Non pris en charge](media/Red_X.png) | Importation |
|Microsoft Store pour</br>Entreprises et Éducation | Un | Public | ![Pris en charge](media/green_check.png) | ![Non pris en charge](media/Red_X.png) | Importer, Créer |


### <a name="about-azure-ad-apps"></a>À propos des applications Azure AD

Des services Azure différents nécessitent des configurations distinctes, que vous définissez dans le portail Azure. En outre, les applications pour chaque service peuvent nécessiter des autorisations distinctes sur des ressources Azure.  

Vous pouvez utiliser une seule application pour plusieurs services. Il n’existe qu’un seul objet à gérer dans Configuration Manager et Azure AD. Quand la clé de sécurité de l’application expire, il vous suffit d’actualiser une clé.

La configuration la plus sécurisée consiste à utiliser des applications distinctes pour chaque service. Une application pour un service peut nécessiter des autorisations supplémentaires qui s’avèrent inutiles pour un autre service. L’utilisation d’une application pour différents services peut fournir à l’application plus d’autorisations que nécessaire. 

Quand vous créez des services Azure supplémentaires dans l’Assistant, Configuration Manager est conçu pour réutiliser les informations qui sont communes aux services. Ce comportement vous évite d’avoir à entrer les mêmes informations plusieurs fois. 

Pour plus d’informations sur les autorisations d’application nécessaires et les configurations pour chaque service, consultez l’article Configuration Manager approprié dans [Services disponibles](#available-services). 

Pour plus d’informations sur les applications Azure, commencez par les articles suivants :
- [Authentification et autorisation dans Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Vue d’ensemble des applications web](/azure/app-service-web/app-service-web-overview)
- [Concepts de base de l’inscription d’une application dans Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad)  
- [Inscrire une application auprès de votre locataire Azure Active Directory](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Avant de commencer

Après avoir choisi le service auquel vous souhaitez vous connecter, reportez-vous au tableau dans [Détails sur le service](#service-details). Ce tableau fournit les informations nécessaires pour terminer l’Assistant Services Azure. Ayez préalablement une discussion avec votre administrateur Azure AD. Décidez si vous créez manuellement les applications à l’avance dans le portail Azure pour en importer ensuite les détails dans Configuration Manager. Vous pouvez aussi utiliser Configuration Manager pour créer directement les applications dans Azure AD. Pour collecter les données nécessaires à partir d’Azure AD, passez en revue les informations contenues dans les autres sections de cet article.

Certains services nécessitent que les applications Azure AD disposent d’autorisations spécifiques. Passez en revue les informations pour chaque service afin de déterminer les autorisations requises. Par exemple, avant de pouvoir importer une application web, un administrateur Azure doit tout d’abord la créer dans le [portail Azure](https://portal.azure.com). Lors de la configuration du connecteur Upgrade Readiness ou OMS, vous devez donner à votre application web tout juste inscrite une autorisation de *contributeur* sur le groupe de ressources qui contient l’espace de travail OMS approprié. Cette autorisation permet à Configuration Manager d’accéder à cet espace de travail. Recherchez le nom de l’inscription d’application dans le panneau **Ajouter des utilisateurs** au moment d’attribuer l’autorisation. Ce processus est le même que lors de la [fourniture à Configuration Manager d’autorisations sur OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms). Un administrateur Azure doit attribuer ces autorisations avant que vous n’importiez l’application dans Configuration Manager.



## <a name="start-the-azure-services-wizard"></a>Démarrer l’Assistant Services Azure

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**.  

2.  Sous l’onglet **Accueil** du ruban, dans le groupe **Services Azure**, cliquez sur **Configurer les services Azure**.  

3.  Dans la page **Services Azure** de l’Assistant Services Azure :  

    1. Spécifiez un **Nom** pour l’objet dans Configuration Manager.  

    2. Spécifiez une **Description** facultative pour vous aider à identifier le service.  

    3. Sélectionnez le service Azure que vous souhaitez connecter à Configuration Manager.  

4. Cliquez sur **Suivant** pour passer à la page [Propriétés de l’application Azure](#azure-app-properties) de l’Assistant Services Azure.  



## <a name="azure-app-properties"></a>Propriétés de l’application Azure

Dans la page **Application** de l’Assistant Services Azure, sélectionnez d’abord **l’environnement Azure** dans la liste. Reportez-vous au tableau dans [Détails sur le service](#service-details) pour connaître l’environnement actuellement disponible pour le service.

Le reste de la page Application varie selon le service spécifique. Reportez-vous au tableau dans [Détails sur le service](#service-details) pour connaître le type d’application utilisé par le service et l’action que vous pouvez effectuer. 
- Si l’application prend en charge les deux actions Importer et Créer, cliquez sur **Parcourir**. Cette action ouvre la [boîte de dialogue Application serveur](#server-app-dialog) ou la [boîte de dialogue Application cliente](#client-app-dialog).
- Si l’application prend uniquement en charge l’action Importer, cliquez sur **Importer**. Cette action ouvre la [boîte de dialogue Importer des applications (serveur)](#import-apps-dialog-server) ou la [boîte de dialogue Importer des applications (client)](#import-apps-dialog-client).

Après avoir spécifié les applications dans cette page, cliquez sur **Suivant** pour passer à la page [Configuration ou Découverte](#configuration-or-discovery) de l’Assistant Services Azure.

### <a name="web-app"></a>Application web

Il s’agit d’une application Azure AD de type *Application/API web*, également appelée application serveur dans Configuration Manager.

#### <a name="server-app-dialog"></a>Boîte de dialogue Application serveur

Quand vous cliquez sur **Parcourir** pour **Application web** dans la page Application de l’Assistant Services Azure, il ouvre la boîte de dialogue Application serveur. Il affiche une liste qui indique les propriétés suivantes de toutes les applications web existantes :
- Nom convivial du locataire
- Nom convivial de l’application
- Type de service

Il existe trois actions possibles à partir de la boîte de dialogue Application serveur :
- Pour réutiliser une application web existante, sélectionnez-la dans la liste. 
- Cliquez sur **Importer** pour ouvrir la [boîte de dialogue Importer des applications](#import-apps-dialog-server).
- Cliquez sur **Créer** pour ouvrir la [boîte de dialogue Créer une application serveur](#create-server-application-dialog).

Après avoir sélectionné, importé ou créé une application web, cliquez sur **OK** pour fermer la boîte de dialogue Application serveur. Cette action renvoie à la [page Application](#azure-app-properties) de l’Assistant Services Azure.

#### <a name="import-apps-dialog-server"></a>Boîte de dialogue Importer des applications (serveur)

Quand vous cliquez sur **Importer** dans la boîte de dialogue Application serveur ou la page Application de l’Assistant Services Azure, il ouvre la boîte de dialogue Importer des applications. Cette page vous permet d’entrer des informations sur une application web Azure AD qui est déjà créée dans le portail Azure. Les métadonnées relatives à cette application web sont importées dans Configuration Manager. Spécifiez les informations suivantes :
- **Nom du locataire Azure AD**
- **ID de locataire Azure AD**
- **Nom de l’application** : nom convivial pour l’application.
- **ID de client**
- **Clé secrète**
- **Expiration de la clé secrète** : sélectionnez une date ultérieure dans le calendrier. 
- **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Elle se trouve dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est https://ConfigMgrService.  

Après avoir entré les informations, cliquez sur **Vérifier**. Cliquez ensuite sur **OK** pour fermer la boîte de dialogue Importer des applications. Cette action renvoie à la [page Application](#azure-app-properties) de l’Assistant Services Azure ou à la [boîte de dialogue Application serveur](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Boîte de dialogue Créer une application serveur

Quand vous cliquez sur **Créer** dans la boîte de dialogue Application serveur, la boîte de dialogue Créer une application serveur s’ouvre. Cette page permet d’automatiser la création d’une application web dans Azure AD. Spécifiez les informations suivantes :
- **Nom de l’application** : nom convivial pour l’application.
- **URL de la page d’accueil** : cette valeur n’est pas utilisée par Configuration Manager, mais est requise par Azure AD. Par défaut, cette valeur est https://ConfigMgrService.  
- **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Elle se trouve dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est https://ConfigMgrService.  
- **Période de validité de la clé secrète** : cliquez sur la liste déroulante et sélectionnez **1 an** ou **2 ans**. Un an est la valeur par défaut.

Cliquez sur **Se connecter** pour vous authentifier auprès d’Azure en tant qu’utilisateur administratif. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure. Après vous être authentifié correctement auprès d’Azure, la page affiche le **Nom du locataire Azure AD** pour référence. 

Cliquez sur **OK** pour créer l’application web dans Azure AD et fermer la boîte de dialogue Créer une application serveur. Cette action renvoie à la [boîte de dialogue Application serveur](#server-app-dialog).


### <a name="native-client-app"></a>Application cliente native
    
Il s’agit d’une application Azure AD de type *Native*, également appelée application cliente dans Configuration Manager.

#### <a name="client-app-dialog"></a>Boîte de dialogue Application cliente

Quand vous cliquez sur **Parcourir** pour **Application cliente native** dans la page Application de l’Assistant Services Azure, il ouvre la boîte de dialogue Application cliente. Il affiche une liste qui indique les propriétés suivantes de toutes les applications natives existantes :
- Nom convivial du locataire
- Nom convivial de l’application
- Type de service

Il existe trois actions possibles à partir de la boîte de dialogue Application cliente :
- Pour réutiliser une application native existante, sélectionnez-la dans la liste. 
- Cliquez sur **Importer** pour ouvrir la [boîte de dialogue Importer des applications](#import-apps-dialog-client).
- Cliquez sur **Créer** pour ouvrir la [boîte de dialogue Créer une application cliente](#create-client-application-dialog).

Après avoir sélectionné, importé ou créé une application native, cliquez sur **OK** pour fermer la boîte de dialogue Application cliente. Cette action renvoie à la [page Application](#azure-app-properties) de l’Assistant Services Azure.

#### <a name="import-apps-dialog-client"></a>Boîte de dialogue Importer des applications (client)

Quand vous cliquez sur **Importer** dans la boîte de dialogue Application cliente, la boîte de dialogue Importer des applications s’ouvre. Cette page vous permet d’entrer des informations sur une application native Azure AD qui est déjà créée dans le portail Azure. Les métadonnées relatives à cette application native sont importées dans Configuration Manager. Spécifiez les informations suivantes :
- **Nom de l’application** : nom convivial pour l’application.
- **ID de client** 

Après avoir entré les informations, cliquez sur **Vérifier**. Cliquez ensuite sur **OK** pour fermer la boîte de dialogue Importer des applications. Cette action renvoie à la [boîte de dialogue Application cliente](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Boîte de dialogue Créer une application cliente

Quand vous cliquez sur **Créer** dans la boîte de dialogue Application cliente, la boîte de dialogue Créer une application cliente s’ouvre. Cette page permet d’automatiser la création d’une application native dans Azure AD. Spécifiez les informations suivantes :
- **Nom de l’application** : nom convivial pour l’application.
- **URL de réponse** : cette valeur n’est pas utilisée par Configuration Manager, mais est requise par Azure AD. Par défaut, cette valeur est https://ConfigMgrService. 

Cliquez sur **Se connecter** pour vous authentifier auprès d’Azure en tant qu’utilisateur administratif. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure. Après vous être authentifié correctement auprès d’Azure, la page affiche le **Nom du locataire Azure AD** pour référence. 

Cliquez sur **OK** pour créer l’application native dans Azure AD et fermer la boîte de dialogue Créer une application cliente. Cette action renvoie à la [boîte de dialogue Application cliente](#client-app-dialog).


## <a name="configuration-or-discovery"></a>Configuration ou Découverte

Après avoir spécifié les applications natives et web dans la page des applications, l’Assistant Services Azure passe à une page **Configuration** ou **Découverte**, selon le service auquel vous vous connectez. Les détails de cette page varient d’un service à l’autre. Pour plus d’informations, consultez l’un des articles suivants :  

-   Service de **gestion cloud**, page **Découverte** : [Configurer la découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   Service du **connecteur OMS**, page **Configuration** : [Configurer la connexion à OMS](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#use-the-azure-services-wizard-to-configure-the-connection-to-oms)  

-   Service du **connecteur Upgrade Readiness**, page **Configuration** : [Utiliser l’Assistant Azure pour créer la connexion](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   Service du **Microsoft Store pour Entreprises**, page **Configuration** : [Configurer la synchronisation du Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#for-configuration-manager-version-1706-and-later)  


Pour finir, terminez l’Assistant Services Azure via les pages de résumé, de progression et de fin. Vous avez terminé la configuration d’un service Azure dans Configuration Manager. Répétez ce processus pour configurer d’autres services Azure.


## <a name="view-the-configuration-of-an-azure-service"></a>Afficher la configuration d’un service Azure
Vous pouvez afficher les propriétés d’un service Azure que vous avez configuré en vue de son utilisation. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Services Azure**. Sélectionnez le service que vous souhaitez afficher ou modifier, puis cliquez sur **Propriétés**.

Si vous sélectionnez un service, puis cliquez sur **Supprimer** dans le ruban, cette action supprime la connexion dans Configuration Manager. Elle ne supprime pas l’application dans Azure AD. Demandez à votre administrateur Azure de supprimer l’application quand elle est devenue inutile. Vous pouvez aussi exécuter l’Assistant Services Azure pour importer l’application.<!--483440-->


## <a name="cloud-management-data-flow"></a>Flux de données de gestion cloud

Le diagramme suivant est un flux de données conceptuel pour l’interaction entre Configuration Manager, Azure AD et des services cloud connectés. Cet exemple utilise le service de **gestion cloud**, qui inclut un client Windows 10 ainsi que des applications serveur et clientes. Les flux sont similaires pour d’autres services.

![Diagramme de flux de données pour Configuration Manager avec Azure AD et gestion cloud](media/aad-auth.png)

1.  L’administrateur Configuration Manager importe ou crée les applications serveur et clientes dans Azure AD.  

2.  La méthode de découverte d’utilisateurs Azure AD de Configuration Manager s’exécute. Le site utilise le jeton d’application serveur Azure AD pour rechercher des objets utilisateur dans Microsoft Graph.  

3.  Le site stocke des données sur les objets utilisateur. Pour plus d’informations, consultez [Découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  Le client Configuration Manager demande le jeton d’utilisateur Azure AD. Le client génère la revendication à l’aide de l’ID de l’application cliente Azure AD et de l’application serveur comme audience. Pour plus d’informations, consultez [Revendications des jetons de sécurité Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens).  

5.  Le client s’authentifie auprès du site en présentant le jeton Azure AD à la passerelle de gestion cloud et/ou au point de gestion HTTPS local.  


