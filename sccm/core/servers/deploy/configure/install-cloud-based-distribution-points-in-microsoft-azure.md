---
title: Installer des points de distribution cloud
titleSuffix: Configuration Manager
description: Découvrez ce que vous devez faire pour commencer à utiliser des points de distribution cloud dans Microsoft Azure.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2c9c79c5e635a50fecf02c46e2a134df87c2d784
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Installer des points de distribution cloud dans Microsoft Azure pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez installer des points de distribution cloud System Center Configuration Manager dans Microsoft Azure. Si vous n’êtes pas familiarisé avec les points de distribution cloud, consultez [Utiliser un point de distribution cloud](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) avant de poursuivre.

 Avant de commencer l’installation, vérifiez que vous disposez bien des fichiers de certificat nécessaires :  

-   Un certificat de gestion Microsoft Azure exporté dans un fichier .cer et un fichier .pfx.  

-   Un certificat de service de point de distribution cloud Configuration Manager exporté dans un fichier .pfx.  

    > [!TIP]
    >   Pour plus d’informations sur ces certificats, consultez la section consacrée aux points de distribution cloud dans la rubrique [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Pour obtenir un exemple de déploiement du certificat de service de point de distribution cloud, consultez la section « Déploiement du certificat de service pour les points de distribution cloud » dans la rubrique [Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 Une fois que vous avez installé le point de distribution cloud, Azure génère automatiquement un GUID pour le service et l’ajoute au suffixe DNS de **cloudapp.net**. En utilisant ce GUID, vous devez configurer DNS avec un alias DNS (enregistrement CNAME). Cela vous permet de mapper le nom de service que vous définissez dans le certificat de service de point de distribution cloud Configuration Manager au GUID généré automatiquement.  

 Si vous utilisez un serveur Web proxy, vous serez peut-être amené à configurer les paramètres de proxy pour permettre la communication avec le service cloud hébergeant le point de distribution.  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Configurer Azure et installer des points de distribution cloud  
 Utilisez les procédures suivantes pour configurer la prise en charge par Azure des points de distribution et installer le point de distribution cloud dans Configuration Manager.  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>Pour configurer un service cloud dans Azure pour un point de distribution  

1.  Dans un navigateur web, accédez au portail Azure sur https://manage.windowsazure.com, puis accédez à votre compte.  

2.  Cliquez sur **Services hébergés, Comptes de stockage et CDN**, puis sélectionnez **Certificats de gestion**.  

3.  Cliquez avec le bouton droit sur votre abonnement, puis sélectionnez **Ajouter un certificat**.  

4.  Pour **Fichier de certificat**, spécifiez le fichier .cer contenant le certificat de gestion Azure exporté à utiliser pour ce service cloud, puis cliquez sur **OK**.  

Le certificat de gestion est chargé dans Azure, ce qui vous permet maintenant d’installer un point de distribution cloud.  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Pour installer un point de distribution cloud pour Configuration Manager  

1.  Exécutez les étapes de la procédure précédente pour configurer un service cloud dans Azure avec un certificat de gestion.  

2.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis sélectionnez **Points de distribution cloud**. Sous l’onglet **Accueil**, cliquez sur **Créer un point de distribution cloud**.  

3.  Dans la page **Général** de l’Assistant Création d’un point de distribution cloud, configurez les éléments suivants :  

    -   Spécifiez l’**ID d’abonnement** de votre compte Azure.  

        > [!TIP]  
        >  Vous pouvez trouver votre ID d’abonnement Azure dans le portail Azure.  

    -   Spécifiez le **Certificat de gestion**. Cliquez sur **Parcourir** pour spécifier le fichier .pfx contenant le certificat de gestion Azure exporté, puis entrez le mot de passe du certificat. Vous pouvez également spécifier un fichier .publishsettings version 1 issu du Kit de développement logiciel Azure SDK 1.7.  

4.  Cliquez sur **Suivant**. Configuration Manager se connecte à Azure pour valider le certificat de gestion.  

5.  Dans la page **Paramètres**, effectuez les opérations suivantes et cliquez sur **Suivant** :  

    -   Pour **Région**, sélectionnez la région Azure dans laquelle vous souhaitez créer le service cloud qui héberge ce point de distribution.  

    -   Pour **Fichier de certificat**, spécifiez le fichier .pfx qui contient le certificat exporté pour le service de point de distribution cloud Configuration Manager. Entrez ensuite le mot de passe.  

        > [!NOTE]  
        >  La zone **FQDN du service** est complétée automatiquement avec le nom d’objet du certificat. Dans la plupart des cas, vous n’avez pas à le modifier. Vous le devrez exceptionnellement si vous utilisez un certificat générique dans un environnement de test. Par exemple, dans ce cas, vous pouvez ne pas spécifier le nom d’hôte pour que plusieurs ordinateurs dotés du même suffixe DNS puissent utiliser ce certificat. Dans ce scénario, l’objet du certificat contient une valeur similaire à **CN=\*.contoso.com** et Configuration Manager affiche un message indiquant que vous devez spécifier le nom de domaine complet correct. Cliquez sur **OK** pour fermer le message, puis entrez un nom spécifique avant le suffixe DNS pour fournir un nom de domaine complet. Par exemple, vous pouvez ajouter **clouddp1** pour spécifier le nom de domaine complet du service **clouddp1.contoso.com**. Le nom de domaine complet du service doit être unique dans votre domaine et ne doit correspondre à aucun périphérique joint à un domaine.  
        >   
        >  Les certificats génériques sont pris en charge pour tester les environnements uniquement.  

6.  Dans la page **Alertes**, configurez les quotas de stockage, les quotas de transfert, ainsi que le pourcentage de ces quotas auquel Configuration Manager doit générer des alertes. Cliquez ensuite sur **Suivant**.  

7.  Effectuez toutes les étapes de l'Assistant.  

L'Assistant crée un service hébergé pour le point de distribution cloud. Après avoir fermé l’Assistant, vous pouvez surveiller la progression de l’installation du point de distribution cloud dans la console Configuration Manager. Vous pouvez également surveiller le fichier **CloudMgr.log** sur le serveur de site principal. Vous pouvez surveiller la mise en service du service cloud dans le portail Azure.  

> [!NOTE]  
>  La mise en service d’un nouveau point de distribution dans Azure peut prendre jusqu’à 30 minutes. Le message suivant est répété dans le fichier **CloudMgr.log** tant que le compte de stockage n’est pas approvisionné : **En attente de vérification de l’existence du conteneur. Une nouvelle vérification sera effectuée dans 10 secondes**. Le service est ensuite créé et configuré.  

 Pour savoir si l'installation du point de distribution cloud est terminée, employez les méthodes suivantes :  

-   Dans le portail Azure, le **Déploiement** du point de distribution cloud indique l’état **Prêt**.  

-   Dans la console Configuration Manager, dans l’espace de travail **Administration**, sous le nœud **Configuration de la hiérarchie**, **Cloud**, le point de distribution cloud indique l’état **Prêt**.  

-   Configuration Manager affiche l’ID de message d’état **9409** pour le composant SMS_CLOUD_SERVICES_MANAGER.  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> Configurer la résolution de noms pour les points de distribution cloud  
 Pour pouvoir accéder au point de distribution cloud, les clients doivent être en mesure de résoudre le nom du point de distribution cloud de manière à fournir une adresse IP gérée par Azure. Pour ce faire, les clients procèdent en deux étapes :  

1.  Ils mappent le nom de service que vous avez fourni avec le certificat du service de point de distribution cloud Configuration Manager au nom de domaine complet de votre service Azure. Ce nom de domaine complet contient un GUID et le suffixe DNS de **cloudapp.net**. Le GUID est généré automatiquement après l'installation du point de distribution cloud. Vous pouvez afficher le nom de domaine complet dans le portail Azure, en référençant l’**URL du site** dans le tableau de bord du service cloud. Exemple d’URL de site : **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  Ils résolvent le nom de domaine complet du service Azure pour fournir l’adresse IP allouée par Azure. Cette adresse IP peut également être identifiée dans le tableau de bord pour le service cloud du portail Azure, et elle est nommée **ADRESSE IP VIRTUELLE PUBLIQUE (VIP)**.  

Pour mapper le nom de service que vous avez fourni avec le certificat de service de point de distribution cloud Configuration Manager (par exemple **clouddp1.contoso.com**) au nom de domaine complet de votre service Azure (par exemple **d1594d4527614a09b934d470.cloudapp.net**), les serveurs DNS sur Internet doivent avoir un alias DNS (enregistrement CNAME). Les clients peuvent ensuite résoudre le nom de domaine complet du service Azure pour fournir l’adresse IP en utilisant des serveurs DNS sur Internet.  

##  <a name="BKMK_ConfigProxyforCloud"></a> Configurer les paramètres de proxy pour des sites principaux gérant des services cloud  
 Quand vous utilisez des services cloud avec Configuration Manager, le site principal qui gère le point de distribution cloud doit pouvoir se connecter au portail Azure. Le site se connecte à l’aide du compte **Système** de l’ordinateur de site principal. Cette connexion est établie à l'aide du navigateur Web par défaut sur l'ordinateur serveur de site principal.  

 Sur le serveur de site principal qui gère le point de distribution cloud, vous devrez peut-être configurer les paramètres de proxy pour permettre au site principal d’accéder à Internet et à Azure.  

 Pour configurer les paramètres de proxy du serveur de site principal dans la console Configuration Manager, exécutez la procédure ci-dessous.  

> [!TIP]  
>  Vous pouvez également configurer le serveur proxy lors de l’installation de nouveaux rôles de système de site sur le serveur de site principal à l’aide de l’**Assistant Ajout des rôles de système de site**.  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>Pour configurer les paramètres de proxy pour le serveur de site principal  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**. Ensuite, sélectionnez le serveur de site principal qui gère le point de distribution cloud.  

3.  Dans le volet d'informations, cliquez avec le bouton droit sur **Système de site**, puis cliquez sur **Propriétés**.  

4.  Dans **Propriétés du système de site**, sélectionnez l’onglet **Proxy**, puis configurez les paramètres de proxy de ce serveur de site principal.  

5.  Cliquez sur **OK** pour enregistrer les paramètres.  
