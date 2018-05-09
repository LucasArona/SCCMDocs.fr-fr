---
title: Synchroniser des données avec OMS
titleSuffix: Configuration Manager
description: Synchronisez les données de System Center Configuration Manager vers Microsoft Operations Management Suite.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a01c5534367ad66314afc563cff41adeb2b88dc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
#  <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite"></a>Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1258052-->
Vous pouvez utiliser l’**Assistant Services Azure** pour configurer la connexion de Configuration Manager au service cloud Operations Management Suite (OMS). À compter de la version 1706, l’Assistant remplace les flux de travail précédents pour configurer cette connexion. Pour les versions antérieures, consultez [Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite (1702 et antérieur)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

-   L’Assistant est utilisé pour configurer les services cloud pour Configuration Manager, comme OMS, Microsoft Store pour Entreprises et Azure Active Directory (Azure AD).  

-   Configuration Manager se connecte à OMS pour des fonctionnalités comme [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) ou [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



## <a name="prerequisites-for-the-oms-connector"></a>Conditions préalables pour le connecteur OMS
Les prérequis pour configurer une connexion à OMS sont identiques aux prérequis [documentés pour la version de Current Branch 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Ces informations sont répétées ici :  

-   Avant d’installer le connecteur OMS dans Configuration Manager, vous devez accorder à Configuration Manager les autorisations d’accès à OMS. Plus précisément, vous devez accorder un *accès Contributeur* au *groupe de ressources* Azure qui contient l’espace de travail OMS Log Analytics. Les procédures à suivre sont documentées dans le contenu Log Analytics. Consultez la rubrique [Accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) dans la documentation OMS.

-   Le connecteur OMS doit être installé sur l’ordinateur qui héberge un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) se trouvant en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Vous devez installer un Microsoft Monitoring Agent pour OMS sur le point de connexion de service ainsi que le connecteur OMS. L’agent et le connecteur OMS doivent être configurés pour utiliser le même **espace de travail OMS**. Pour installer l’agent, consultez [Télécharger et installer l’agent](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) dans la documentation OMS.
-   Après avoir installé le connecteur et l’agent, vous devez configurer OMS pour utiliser les données Configuration Manager. Pour ce faire, dans le portail OMS, [importez des regroupements Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections).

## <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Utilisez l’assistant de services Azure pour configurer la connexion à OMS

1.  Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Services Azure**. Choisissez **Configurer les services Azure** sous l’onglet **Accueil** du ruban pour démarrer l’**Assistant Services Azure** .

2.  Sur la page **Services Azure**, sélectionnez le service cloud Operation Management Suite. Saisissez un nom convivial comme **Nom du service Azure** ainsi qu’une description facultative, puis cliquez sur **Suivant**.

3.  Sur la page **Application**, spécifiez votre environnement Azure (la version Technical Preview prend en charge uniquement le cloud public). Ensuite, cliquez sur **Parcourir** pour ouvrir la fenêtre de l’application serveur.

4.  Sélectionnez une application web :

    -   **Importer** : pour utiliser une application web qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Fournissez un nom convivial pour l’application et le locataire. Spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir **vérifié** les informations, cliquez sur **OK** pour continuer.   

    > [!NOTE]   
    > Lorsque vous configurez OMS avec cette version préliminaire, OMS ne prend en charge la fonction *Importer* pour une application web. La création d’une application web n’est pas prise en charge. De même, vous ne pouvez pas réutiliser une application existante pour OMS.

5.  Si vous avez suivi toutes les autres procédures avec succès, les informations sur l’écran **Configuration de la connexion OMS** s’affichent automatiquement sur cette page. Les informations pour les paramètres de connexion devraient s’afficher pour votre **Abonnement Azure**, votre **Groupe de ressources Azure** et votre **Espace de travail Operations Management Suite**.

6.  L’Assistant se connecte au service OMS en utilisant les informations que vous avez saisies. Sélectionnez les collections d’appareils que vous souhaitez synchroniser avec OMS, puis cliquez sur **Ajouter**.

7.  Vérifiez vos paramètres de connexion dans l’écran **Résumé**, puis sélectionnez **Suivant**. L’écran **Progression** indique l’état de connexion, puis **Terminé**.

8.  Une fois l’Assistant terminé, la console Configuration Manager indique que vous avez configuré **Operation Management Suite** comme **Type de service cloud**.

## <a name="sync-data-from-configuration-manager-to-the-microsoft-operations-management-suite-1702-and-earlier"></a>Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite (1702 et antérieur)


*S’applique à : System Center Configuration Manager (1702 et versions antérieures)*

Vous pouvez utiliser le connecteur Microsoft Operations Management Suite (OMS) pour synchroniser les données, comme vos regroupements de System Center Configuration Manager avec OMS Log Analytics dans Microsoft Azure. Le connecteur rend les données de votre déploiement Configuration Manager visibles dans OMS.
> [!TIP]
> À compter de Configuration Manager 1802, le connecteur OMS n’est plus une fonctionnalité en préversion. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/pre-release-features).

Depuis la version 1702, vous pouvez utiliser le connecteur OMS pour vous connecter à un espace de travail OMS figurant sur le Microsoft Azure Government Cloud. Pour cela, vous devez modifier un fichier de configuration avant d’installer le connecteur OMS. Consultez la section [Utiliser le connecteur OMS avec Azure Government Cloud](#fairfaxconfig) de cet article.

### <a name="prerequisites"></a>Prérequis
- Avant d’installer le connecteur OMS dans Configuration Manager, vous devez accorder à Configuration Manager les autorisations d’accès à OMS. Plus précisément, vous devez accorder un *accès Contributeur* au *groupe de ressources* Azure qui contient l’espace de travail OMS Log Analytics. Les procédures à suivre sont documentées dans le contenu Log Analytics. Consultez la rubrique [Accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) dans la documentation OMS.

- Le connecteur OMS doit être installé sur l’ordinateur qui héberge un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) se trouvant en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  Si vous avez connecté OMS à un site principal autonome et que vous prévoyez d’ajouter un site d’administration centrale à votre environnement, vous devez supprimer la connexion actuelle puis reconfigurer le connecteur sur le nouveau site d’administration centrale.

- Vous devez installer un Microsoft Monitoring Agent pour OMS sur le point de connexion de service ainsi que le connecteur OMS.  L’agent et le connecteur OMS doivent être configurés pour utiliser le même **espace de travail OMS**. Pour installer l’agent, consultez [Télécharger et installer l’agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) dans la documentation OMS.

- Après avoir installé le connecteur et l’agent, vous devez configurer OMS pour utiliser les données Configuration Manager.  Pour ce faire, dans le portail OMS, [importez des regroupements Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



### <a name="install-the-oms-connector"></a>Installer le connecteur OMS  
1. Dans la console Configuration Manager, configurez votre [hiérarchie pour utiliser les fonctionnalités de la version préliminaire](/sccm/core/servers/manage/pre-release-features), puis activez l’utilisation du connecteur OMS.  
0
2. Ensuite, accédez à **Administration** > **Services de cloud** > **Connecteur OMS**. Dans le ruban, cliquez sur « Créer une connexion à Operations Management Suite ». Cette étape ouvre l’**Assistant Connexion à Operation Management Suite**. Sélectionnez **Suivant**.  


3.  Dans la page **Général**, vérifiez que vous disposez des informations suivantes, puis sélectionnez **Suivant**.  
  - Configuration Manager inscrit en tant qu’outil de gestion « Application web et/ou API web » et présence de l’[ID de client résultant de cette inscription](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Clé de client créée pour l’outil de gestion inscrit dans Azure Active Directory.  

  - Dans le portail Azure, l’application web inscrite autorisée à accéder à OMS, comme indiqué dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.  Dans la page **Azure Active Directory**, configurez vos paramètres de connexion à OMS en renseignant les champs **Locataire**, **ID Client** et **Clé secrète du client**, puis sélectionnez **Suivant**.  

5.  Dans la page **Configuration de la connexion OMS**, définissez vos paramètres de connexion en renseignant les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.  L’espace de travail doit correspondre à l’espace de travail configuré pour Microsoft Management Agent installé sur le point de connexion de service.  

6.  Vérifiez vos paramètres de connexion dans la page **Résumé**, puis sélectionnez **Suivant**. La page **Progression** indique l’état de connexion, puis **Terminé**.

Après avoir lié Configuration Manager à OMS, vous pouvez ajouter ou supprimer des regroupements et afficher les propriétés de la connexion OMS.

### <a name="verify-the-oms-connector-properties"></a>Vérifiez les propriétés du connecteur OMS
1.  Dans la console de Configuration Manager, accédez à **Administration** > **Services cloud**, puis sélectionnez **Connecteur OMS** afin d’ouvrir la page **Connexion OMS**.
2.  Cette page contient deux onglets :
  - **Azure Active Directory :** 
  
     Cet onglet affiche votre **Llcataire**, l’**ID client**, l’**expiration de la clé secrète client** et vous permet de vérifier si votre clé secrète client a expiré.

  - **Propriétés de connexion OMS :**  

     Cet onglet affiche votre **Abonnement Azure**, votre **Groupe de ressources Azure**, l’**Espace de travail Operations Management Suite**, ainsi que la liste des **Regroupements d’appareils pour lesquels Operations Management Suite peut obtenir des données**. Utilisez les boutons **Ajouter** et **Supprimer** pour modifier les collections autorisées.

### <a name="fairfaxconfig"> </a> Utiliser le connecteur OMS avec Azure Government Cloud


1.  Sur les ordinateurs où est installée la console Configuration Manager, modifiez le fichier de configuration suivant pour qu’il pointe vers Azure Government Cloud : ***&lt;Chemin d’installation de Configuration Manager>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Modifications :**

    Changez la valeur du nom de paramètre *FairFaxArmResourceID* pour qu’elle corresponde à « https://management.usgovcloudapi.net/ »

   - **Avant modification :** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Après modification :**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Changez la valeur du nom de paramètre *FairFaxAuthorityResource* pour qu’elle corresponde à « https://login.microsoftonline.us/ »

  - **Avant modification :** &lt;nom de paramètre="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Après modification :** &lt;nom du paramètre="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.us/&lt;/value>

2.  Après avoir apporté ces deux modifications et enregistré le fichier, redémarrez la console Configuration Manager sur le même ordinateur, puis utilisez cette console pour installer le connecteur OMS. Pour installer le connecteur, utilisez les informations situées sous [Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), puis sélectionnez l’**Espace de travail Operations Management Suite** qui se trouve dans Microsoft Azure Government Cloud.

3.  Une fois le connecteur OMS installé, une connexion à Azure Government Cloud est disponible lorsque vous utilisez une console se connectant au site.
