---
title: Upgrade Readiness
titleSuffix: Configuraton Manager
description: Intégrez Upgrade Readiness à Configuration Manager. Accédez aux données de compatibilité de mise à niveau dans votre console d’administration. Ciblez des appareils pour la mise à niveau ou la mise à jour.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 4360fc34e06d4c62c137f8c956274104112d54a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="integrate-upgrade-readiness-with-system-center-configuration-manager"></a>Intégrer Upgrade Readiness à System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Upgrade Readiness (anciennement Upgrade Analytics) fait partie de [Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) qui vous permet d’évaluer et d’analyser l’état de préparation des appareils de votre environnement pour une mise à niveau vers Windows 10. Vous pouvez configurer la version spécifique. Vous pouvez intégrer Upgrade Readiness à Configuration Manager pour accéder aux données de compatibilité de mise à niveau du client dans la console d’administration de Configuration Manager. Vous êtes en mesure de cibler des appareils pour des mises à niveau ou mises à jour à l’aide de regroupements dynamiques créés en fonction de ces données.

Upgrade Readiness est une solution qui s’exécute sur [Operations Management Suite (OMS)](/azure/operations-management-suite/operations-management-suite-overview). Pour en savoir plus sur Upgrade Readiness, consultez [Gérer les mises à niveau de Windows avec Upgrade Readiness](/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness).

<!--
>[!WARNING]
>For Upgrade Readiness to function within Configuration Manager, you must upgrade to Configuration Manager version 1802. The Upgrade Readiness Connector will no longer function in Configuration Manager versions earlier than 1802. 
SMS.507205 Pulled 4/5/18 -->


## <a name="configure-clients"></a>Configurer des clients

Upgrade Readiness, comme toutes les solutions Windows Analytics, s’appuie sur les données de télémétrie Windows. Pour qu’Upgrade Readiness reçoive suffisamment de données de télémétrie, les prérequis suivants doivent être satisfaits :

- Tous les clients doivent être configurés avec une **clé d’ID commercial**. 
- Le niveau de base de la télémétrie doit au minimum être configuré pour les clients Windows 10.
-  Les clients exécutant des versions antérieures sur Windows doivent installer des bases de connaissances spécifiques comme décrit dans [Prise en main d’Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs). Ils doivent également avoir activer la télémétrie dans les **paramètres client**.

La clé d’ID commercial et la télémétrie Windows peuvent être configurées dans les **paramètres client**. Pour en savoir plus, consultez [Utiliser Windows Analytics avec Configuration Manager](../monitor-windows-analytics.md).

>[!NOTE]
>Si Upgrade Readiness ne reçoit pas comme prévu les données de télémétrie envoyées par les appareils de votre environnement, vous pouvez traiter certains de ces problèmes à l’aide du [script de déploiement Upgrade Readiness](/windows/deployment/upgrade/upgrade-readiness-deployment-script). Toutefois, dans la plupart des environnements, le déploiement des bases de connaissances appropriées, ainsi que la configuration de la clé d’ID commercial et de la télémétrie dans les **Paramètres client** devraient suffire.

## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Connecter Configuration Manager à Upgrade Readiness

À compter de Current Branch version 1706, l’[Assistant Services Azure](../../../servers/deploy/configure/azure-services-wizard.md) est utilisé pour simplifier le processus de configuration des services Azure que vous utilisez avec Configuration Manager. Pour connecter Configuration Manager à Upgrade Readiness, une inscription d’application Azure AD de type *application web/API* doit être créée dans le [portail Azure](https://portal.azure.com). Pour en savoir plus sur la création d’une inscription d’application, consultez [Inscrire votre application avec un client Azure Active Directory](/azure/active-directory/active-directory-app-registration). Dans le **portail Azure**, vous devez également donner à votre application web tout juste inscrite des autorisations de *contributeur* sur le groupe de ressources qui contient l’espace de travail OMS qui héberge vos données Upgrade Readiness. L’**Assistant Services Azure** utilise cette inscription d’application pour permettre à Configuration Manager de communiquer en toute sécurité avec Azure AD et de connecter votre infrastructure à vos données Upgrade Readiness.

>[!IMPORTANT]
>Les autorisations de *contributeur* doivent être accordées à l’application elle-même, contrairement à une identité d’utilisateur Azure AD. En effet, c’est l’application inscrite et non un utilisateur Azure AD qui accède aux données pour le compte de votre infrastructure Configuration Manager. Pour accorder les autorisations, vous devez rechercher le nom de l’inscription d’application dans la zone **Ajouter des utilisateurs** au moment d’attribuer l’autorisation. Il s’agit du même processus que celui à suivre pour [accorder à Configuration Manager les autorisations d’accès à OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) pour les connexions à [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Ces étapes doivent être effectuées avant d’importer l’inscription d’application dans Configuration Manager avec l’*Assistant Services Azure*.

### <a name="use-the-azure-wizard-to-create-the-connection"></a>Utiliser l’Assistant Azure pour créer la connexion

Suivez les instructions données dans [Configurer les services Azure à utiliser avec Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md) pour créer une connexion à Upgrade Readiness en important l’inscription d’application web créée ci-dessus. 

Dans la page *Configuration*, les valeurs suivantes sont préremplies si l’importation d’application web a réussi et si les autorisations appropriées sont affectées dans le **portail Azure**. 
-  Abonnements Azure
-  Groupe de ressources Azure
-  Espace de travail Windows Analytics

Plusieurs groupes de ressources ou espaces de travail sont disponibles uniquement si l’application web Azure AD inscrite dispose d’autorisations de *contributeur* sur plusieurs groupes de ressources ou si le groupe de ressources sélectionné comprend plusieurs espaces de travail OMS.
 
## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Afficher et utiliser les informations Upgrade Readiness dans Configuration Manager

Une fois que vous avez intégré Upgrade Readiness à Configuration Manager, vous pouvez afficher l’analyse de la préparation de vos clients pour la mise à niveau.

1. Dans la console Configuration Manager, choisissez **Surveillance** > **Vue d’ensemble** > **Upgrade Readiness**.
2. Passez en revue les données, notamment l’état de préparation à la mise à niveau et le pourcentage d’appareils Windows qui envoient des données de télémétrie.
3. Vous pouvez filtrer le tableau de bord pour afficher les données d’appareils dans des regroupements spécifiques.
4. Vous pouvez afficher les appareils dans un état de préparation particulier et créer un regroupement dynamique pour ces derniers afin de pouvoir les mettre à niveau s’ils sont prêts ou effectuer les actions nécessaires pour corriger les appareils dont la mise à niveau est bloquée.

## <a name="using-the-upgrade-readiness-connector-version-1702-and-earlier"></a>Utilisation du connecteur Upgrade Readiness (versions 1702 et antérieures)

Dans Configuration Manager version 1702 ou antérieure, une autre série d’étapes et d’exigences est nécessaire pour créer une connexion à Upgrade Readiness.

### <a name="prerequisites"></a>Prérequis

- Pour ajouter la connexion, votre environnement Configuration Manager doit d’abord configurer un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) dans un [mode en ligne](https://azure.microsoft.com/documentation/articles/resource-group-create-service-principal-portal/). Quand vous ajoutez la connexion à votre environnement, Microsoft Monitoring Agent est également installé sur l’ordinateur exécutant ce rôle de système de site.
- Inscrivez Configuration Manager comme outil de gestion « Application web et/ou API web » et obtenez l’[ID de client résultant de cette inscription](https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/).
- Créer une clé de client pour l’outil de gestion inscrit dans Azure Active Directory.
- Dans le portail Azure, autorisez l’application web inscrite à accéder à OMS en suivant les étapes décrites dans [Accorder à Configuration Manager les autorisations d’accès à OMS](https://azure.microsoft.com/documentation/articles/log-analytics-sccm/#provide-configuration-manager-with-permissions-to-oms).

    > [!IMPORTANT]
    > Quand vous configurez l’autorisation d’accès à OMS, choisissez le rôle **Collaborateur** et accordez-lui les autorisations sur le groupe de ressources de l’application inscrite.

### <a name="create-the-connection"></a>Créer la connexion

1.  Dans la console Configuration Manager, choisissez **Administration** > **Services cloud** > **Connecteur Upgrade Readiness** > **Créer une connexion à Upgrade Analytics** pour démarrer l’**Assistant Ajout d’une connexion Upgrade Analytics**.
3.  Dans l’écran **Azure Active Directory**, indiquez les valeurs de **Locataire**, **ID de client** et **Clé secrète du client**, puis sélectionnez **Suivant**.
4.  Dans l’écran **Upgrade Readiness**, définissez vos paramètres de connexion en renseignant les champs **Abonnement Azure**, **Groupe de ressources Azure** et **Espace de travail Operations Management Suite**.
5.  Vérifiez vos paramètres de connexion dans l’écran **Résumé**, puis sélectionnez **Suivant**.

    > [!NOTE]
    > Vous devez connecter Upgrade Readiness au site de niveau supérieur de votre hiérarchie. Si vous connectez Upgrade Readiness à un site principal autonome et que vous ajoutez ensuite un site d’administration centrale à votre environnement, vous devez supprimer et recréer la connexion OMS au sein de la nouvelle hiérarchie.
