---
title: Installer des points de distribution cloud
titleSuffix: Configuration Manager
description: Utilisez ces étapes pour configurer un point de distribution cloud dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef6ace569a73700c2250cd5a45301df387e54c33
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127165"
---
# <a name="install-a-cloud-distribution-point-for-configuration-manager"></a>Installer un point de distribution cloud pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit les étapes pour installer un point de distribution cloud Configuration Manager dans Microsoft Azure. Il comprend les sections suivantes :
- [Avant de commencer](#bkmk_before) 
- [Configurer](#bkmk_setup)
- [Configurer le DNS](#bkmk_dns)
- [Configurer le proxy du serveur de site](#bkmk_proxy)
- [Distribuer du contenu et configurer les clients](#bkmk_client)
- [Gérer et surveiller](#bkmk_monitor)
- [Modification](#bkmk_modify)
- [Dépannage avancé](#bkmk_tshoot) 



## <a name="bkmk_before"></a> Avant de commencer

Commencez par lire l’article [Utiliser un point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Cet article vous aide à planifier et à concevoir vos points de distribution cloud. 

Utilisez la liste de vérification suivante pour vérifier que vous disposez des informations nécessaires et des prérequis pour créer un point de distribution cloud :  

- Le serveur de site peut se connecter à Azure. Si votre réseau utilise un proxy, [configurez le rôle de système de site](#bkmk_proxy).  

- **L’environnement Azure** à utiliser. Par exemple, le cloud public Azure ou le cloud Azure US Government.  

- Depuis la version 1806 et *recommandée*, utilisez le **déploiement Azure Resource Manager**. Les conditions requises sont les suivantes :<!--1322209-->  

    - L’intégration à [Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**. La découverte des utilisateurs Azure AD n’est pas nécessaire.  

    - **L’ID d’abonnement** Azure  

    - Le **groupe de ressources Azure**  

    - Un **compte d’administrateur des abonnements** qui doit se connecter au cours de l’Assistant  

- Si vous prévoyez d’utiliser le **déploiement de service classique** Azure, vous aurez besoin des éléments suivants :  
    > [!Important]  
    > Depuis la version 1810, les déploiements de services Classic dans Azure sont dépréciés dans Configuration Manager. Commencez par utiliser des déploiements Azure Resource Manager pour la passerelle de gestion cloud. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).  

    - **L’ID d’abonnement** Azure  

    - Un **certificat de gestion** Azure, exporté aux formats .CER et .PFX. Un administrateur d’abonnements Azure doit ajouter le. certificat de gestion .CER à l’abonnement qui se trouve dans le [portail Azure](https://portal.azure.com).  

- Un **certificat d’authentification serveur**, exporté au format .PFX  

- Un **nom de service** global unique pour le point de distribution cloud  

    > [!TIP]  
    > Avant de demander le certificat d’authentification serveur qui utilise ce nom de service, vérifiez que le nom de domaine Azure souhaité est unique. Par exemple, *WallaceFalls.CloudApp.Net*. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com). Sélectionnez **Créer une ressource**, choisissez la catégorie **Calcul**, puis sélectionnez **Service cloud**. Dans le champ **Nom DNS**, tapez le préfixe souhaité, par exemple *WallaceFalls*. L’interface indique si le nom de domaine est disponible ou déjà utilisé par un autre service. Ne créez pas le service dans le portail. Utilisez ce processus seulement pour vérifier la disponibilité du nom.  
 
- La **région** Azure pour ce déploiement  



##  <a name="bkmk_setup"></a> Configurer   

Suivez cette procédure sur le site qui doit héberger ce point de distribution cloud, comme déterminé par votre [conception](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_topology).  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Points de distribution cloud**. Dans le ruban, sélectionnez **Créer un point de distribution cloud**.  

2.  Dans la page **Général** de l’Assistant Création d’un point de distribution cloud, configurez les paramètres suivants :  

    1. Spécifiez **l’environnement Azure**.  

    2. Depuis la version 1806 et *recommandée*, sélectionnez **Déploiement Azure Resource Manager** comme méthode de déploiement. Sélectionnez **Se connecter** pour vous authentifier avec un compte Administrateur d’abonnement Azure. L’Assistant remplit automatiquement les champs restants à partir des informations stockées dans les prérequis de l’intégration d’Azure AD. Si vous possédez plusieurs abonnements, sélectionnez l’**ID de l’abonnement** que vous voulez utiliser.  

    > [!Note]  
    > Depuis la version 1810, les déploiements de services Classic dans Azure sont dépréciés dans Configuration Manager. 
    > 
    > Si vous devez utiliser un déploiement de service Classic, sélectionnez cette option dans cette page. Entrez d’abord votre **ID d’abonnement** Azure. Sélectionnez ensuite **Parcourir**, puis le fichier .PFX du certificat de gestion Azure.  

3.  Sélectionnez **Suivant**. Attendez que le site teste la connexion à Azure.  

4.  Dans la page **Paramètres**, spécifiez les paramètres suivants, puis sélectionnez **Suivant** :  

    - **Région** : sélectionnez la région Azure dans laquelle vous souhaitez créer le point de distribution cloud.  

    - **Groupe de ressources** (méthode de déploiement Azure Resource Manager uniquement)  

        - **Utiliser l’existant** : sélectionnez un groupe de ressources existant dans la liste déroulante.  

        - **Créer nouveau** : entrez le nom du nouveau groupe de ressources à créer dans votre abonnement Azure.  

    - **Site principal** : sélectionnez le site principal qui doit distribuer du contenu à ce point de distribution.

    - **Fichier de certificat** : sélectionnez **Parcourir**, puis le fichier .PFX du certificat d’authentification serveur de ce point de distribution cloud. Le nom commun de ce certificat remplit les champs obligatoires **FQDN du service** et **Nom du service**.  

        > [!NOTE]  
        > Le certificat d’authentification serveur du point de distribution cloud prend en charge les caractères génériques. Si vous utilisez un certificat avec caractères génériques, remplacez l’astérisque (\*) dans le champ **FQDN du service** par le nom d’hôte souhaité pour le service.  

5. Dans la page **Alertes**, configurez les quotas de stockage, les quotas de transfert, ainsi que le pourcentage de ces quotas auquel Configuration Manager doit générer des alertes. Puis sélectionnez **Suivant**.  

6. Effectuez toutes les étapes de l'Assistant.  


### <a name="monitor-installation"></a>Surveiller l’installation  

Le site commence par créer un service hébergé pour le point de distribution cloud. Après avoir fermé l’Assistant, surveillez la progression de l’installation du point de distribution cloud dans la console Configuration Manager. Surveillez également le fichier **CloudMgr.log** sur le serveur de site principal. Si nécessaire, surveillez le provisionnement du service cloud dans le portail Azure.  

> [!NOTE]  
>  La mise en service d’un nouveau point de distribution dans Azure peut prendre jusqu’à 30 minutes. Le fichier **CloudMgr.log** répète le message suivant jusqu’à ce que le compte de stockage soit provisionné :  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Une fois le compte de stockage provisionné, le service est créé et configuré.  


### <a name="verify-installation"></a>Vérifier l’installation

Pour vérifier si l’installation du point de distribution cloud est terminée, employez les méthodes suivantes :  

- Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Services cloud**, puis sélectionnez le nœud **Points de distribution cloud**. Localisez le nouveau point de distribution cloud dans la liste. Dans la colonne État, l’état doit être **Prêt**.  

- Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**. Développez **État du système**, puis sélectionnez le nœud **État du composant**. Affichez tous les messages à partir du composant **SMS_CLOUD_SERVICES_MANAGER**, puis recherchez l’ID d’état de message **9409**.  

- Si nécessaire, accédez au portail Azure. Le **Déploiement** du point de distribution cloud indique l’état **Prêt**.  



##  <a name="bkmk_dns"></a> Configurer le DNS  

Pour pouvoir utiliser le point de distribution cloud, les clients doivent être en mesure de résoudre le nom du point de distribution cloud en une adresse IP gérée par Azure. Le point de gestion leur donne le **FQDN du service** du point de distribution cloud. Le point de distribution cloud existe dans Azure et correspond au **Nom du service**. Ces valeurs se trouvent sous l’onglet **Paramètres** des propriétés du point de distribution cloud. 

> [!Note]  
> Dans la console, le nœud **Points de distribution cloud** inclut une colonne nommée **Nom du service**, mais affiche en réalité la valeur **FQDN du service**. Pour voir les deux valeurs, ouvrez les **Propriétés** du point de distribution cloud, puis basculez vers l’onglet **Paramètres**.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

Le nom commun du certificat d’authentification serveur doit inclure le nom de votre domaine. Ce nom est obligatoire lorsque vous achetez un certificat à un fournisseur public. Il est recommandé lors de l’émission de ce certificat à partir de votre infrastructure à clé publique (PKI). Par exemple, `WallaceFalls.contoso.com`. Lorsque vous spécifiez ce certificat dans l’Assistant Création d’un point de distribution cloud, le nom commun remplit la propriété **FQDN du service** (`WallaceFalls.contoso.com`). Le **Nom du service** prend le même nom d’hôte (`WallaceFalls`) et l’ajoute au nom du domaine Azure (`cloudapp.net`). Dans ce scénario, les clients doivent résoudre le **FQDN de service** de votre domaine (`WallaceFalls.contoso.com`) en **Nom du service** Azure (`WallaceFalls.cloudapp.net`). Créez un alias CNAME pour mapper ces noms.


### <a name="create-cname-alias"></a>Créer un alias CNAME

Créez un enregistrement de nom canonique (CNAME) dans le DNS Internet public de votre organisation. Cet enregistrement crée un alias pour la propriété **FQDN du service** du point de distribution cloud que les clients reçoivent, qui correspond au **Nom du service** Azure. Par exemple, créez un enregistrement CNAME pour `WallaceFalls.contoso.com` et son alias `WallaceFalls.cloudapp.net`.  


### <a name="client-name-resolution-process"></a>Processus de résolution des noms de clients

Le processus suivant montre comment un client résout le nom du point de distribution cloud :  

1. Le client obtient le **FQDN du service** du point de distribution cloud dans la liste des sources de contenu. Par exemple, `WallaceFalls.contoso.com`.  

2. Il interroge le DNS qui résout le FQDN du service en **Nom du service** Azure, à l’aide de l’alias CNAME. Par exemple, `WallaceFalls.cloudapp.net`.  

3. Il interroge à nouveau le DNS qui résout le nom du service Azure en adresse IP publique Azure.   

4. Le client utilise cette adresse IP pour démarrer une communication avec le point de distribution cloud.   

5. Le point de distribution cloud présente le certificat d’authentification serveur au client. Le client utilise la chaîne d’approbation du certificat pour le valider.  



## <a name="bkmk_proxy"></a> Configurer le proxy du serveur de site  

Le serveur de site principal qui gère le point de distribution cloud doit pouvoir communiquer avec Azure. Si votre organisation utilise un serveur proxy pour contrôler l’accès à Internet, configurez le serveur de site principal pour utiliser ce proxy.   

Pour plus d’informations, consultez [Prise en charge des serveurs proxy](/sccm/core/plan-design/network/proxy-server-support).  



## <a name="bkmk_client"></a> Distribuer du contenu et configurer les clients

Distribuez du contenu au point de distribution cloud, comme vous le feriez pour un point de distribution local. Le point de gestion n’inclut pas le point de distribution cloud dans la liste des emplacements de contenu, sauf s’il détient le contenu demandé par les clients. Pour plus d’informations, consultez [Distribuer et gérer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content). 

Gérez le point de distribution cloud, comme vous le feriez pour un point de distribution local. Il s’agit notamment de l’attribuer à un groupe de points de distribution et de gérer les packages de contenu. Pour plus d'informations, consultez [Installer et configurer des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).

Les paramètres clients par défaut permettent automatiquement aux clients d’utiliser des points de distribution cloud. Contrôlez l’accès à tous les points de distribution cloud de votre hiérarchie à l’aide des paramètres clients suivants :  

   - Dans le groupe **Paramètres cloud**, modifiez le paramètre **Autoriser l’accès au point de distribution cloud**.  

       - Par défaut, ce paramètre est défini sur **Oui**.  

       - Modifiez et déployez ce paramètre pour les utilisateurs et les appareils.  



## <a name="bkmk_monitor"></a> Gérer et surveiller  

Surveillez le contenu que vous distribuez au point de distribution cloud, comme vous le feriez pour un point de distribution local. Pour plus d’informations, consultez [Surveiller le contenu](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed). 

### <a name="bkmk_alerts"></a> Alertes  

Configuration Manager vérifie régulièrement le service Azure. Si le service n’est pas actif, ou en cas de problèmes liés aux abonnements ou aux certificats, Configuration Manager déclenche une alerte. 

Configurez des seuils pour la quantité de données que vous souhaitez stocker sur le point de distribution cloud et la quantité de données que vous souhaitez que les clients téléchargent à partir du point de distribution. Utilisez des alertes pour ces seuils, afin de savoir quand arrêter ou supprimer un service cloud, quand ajuster le contenu que vous stockez sur le point de distribution et quand modifier les clients qui peuvent utiliser le service. 

- **Seuil d’alerte de stockage** : un seuil d’alerte de stockage définit la limite supérieure de la quantité de données ou de contenu que vous souhaitez stocker sur le point de distribution cloud. Par défaut, ce seuil est défini sur 2 000 Go. Configuration Manager génère des avertissements et des alertes critiques lorsque l’espace disponible atteint les seuils définis. Par défaut, ces alertes sont déclenchées lorsque le niveau atteint 50 % et 90 % du seuil.  

- **Seuil d’alerte de transfert mensuel** : un seuil d’alerte de transfert permet de surveiller la quantité de contenu transféré à partir du point de distribution vers les clients pendant une période de 30 jours. Par défaut, ce seuil est défini sur 10 000 Go. Le site déclenche des avertissements et des alertes critiques lorsque les transferts atteignent les valeurs que vous avez définies. Par défaut, ces alertes sont déclenchées lorsque le niveau atteint 50 % et 90 % du seuil.  

    > [!IMPORTANT]  
    >  Configuration Manager surveille le transfert de données, mais n'interrompt pas ce transfert au-delà du seuil d'alerte de transfert défini.  

Spécifiez des seuils pour chaque point de distribution cloud pendant l’installation, ou utilisez l’onglet **Alertes** des propriétés du point de distribution cloud.  

> [!NOTE]  
>  Les alertes pour un point de distribution cloud dépendent des statistiques d’utilisation fournies par Azure, dont la mise à disposition peut prendre jusqu’à 24 heures. Pour plus d’informations sur Storage Analytics pour Azure, consultez [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

Dans un cycle horaire, le site principal qui surveille le point de distribution cloud télécharge des données transactionnelles à partir d’Azure. Il stocke ces données de transaction dans le fichier `CloudDP-<ServiceName>.log` sur le serveur de site. Configuration Manager évalue ensuite ces informations par rapport aux quotas de stockage et de transfert pour chaque point de distribution cloud. Lorsque le transfert de données atteint ou dépasse le volume défini pour les avertissements ou alertes critiques, Configuration Manager génère l’alerte appropriée.  

> [!WARNING]  
>  Étant donné que le site télécharge des informations sur les transferts de données toutes les heures à partir d’Azure, l’utilisation des données peut dépasser un seuil d’avertissement ou un seuil critique, avant même que Configuration Manager n’accède aux données et n’émette une alerte.  



## <a name="bkmk_modify"></a> Modifier

Affichez des informations générales sur le point de distribution dans le nœud **Points de distribution cloud**, situé sous **Services cloud** dans l’espace de travail **Administration** de la console Configuration Manager. Sélectionnez un point de distribution, puis **Propriétés** pour afficher plus de détails.  

Lorsque vous modifiez les propriétés d’un point de distribution cloud, les paramètres des onglets suivants peuvent être modifiés :  

#### <a name="settings"></a>Paramètres  

- **Description**  

- **Fichier de certificat** : avant l’expiration du certificat d’authentification serveur, émettez un nouveau certificat portant le même nom. Ensuite, ajoutez-y le nouveau certificat pour que le service l’utilise. Si le certificat expire, les clients ne feront pas confiance au service et ne l’utiliseront pas.  

#### <a name="alerts"></a>Alertes
Ajustez les seuils de données pour le stockage et les alertes de transfert mensuel.  

#### <a name="content"></a>Content
Gérez le contenu comme pour un point de distribution local.  


### <a name="redeploy-the-service"></a>Redéployer le service

Les changements plus importants, tels que les configurations suivantes, exigent de redéployer le service :
- Méthode de déploiement classique sur Azure Resource Manager
- Abonnement
- Nom du service
- De PKI privée à PKI publique
- Région Azure

À compter de la version 1806, si vous disposez d’un point de distribution cloud existant dans un déploiement classique et souhaitez utiliser la méthode de déploiement Azure Resource Manager, vous devez déployer un nouveau point de distribution cloud. Il existe deux options :

- Si vous voulez réutiliser le même nom de service :  

    1. Tout d’abord, supprimez le point de distribution cloud classique. En l’absence d’un autre point de distribution cloud, les clients ne peuvent pas obtenir de contenu.  

    2. Créez un point de distribution cloud à l’aide d’un déploiement Resource Manager. Réutilisez le même certificat d’authentification serveur.  

    3. Distribuez le contenu du package de logiciels nécessaire vers le nouveau point de distribution cloud.  

- Si vous voulez utiliser un nouveau nom de service :  

    1. Créez un point de distribution cloud à l’aide d’un déploiement Resource Manager. Utilisez un nouveau certificat d’authentification serveur.  

    2. Distribuez le contenu du package de logiciels nécessaire vers le nouveau point de distribution cloud.  

    3. Supprimez le point de distribution cloud classique.

> [!Tip]  
> Pour déterminer le modèle de déploiement actuel d’un point de distribution cloud :<!--SCCMDocs issue #611-->  
> 1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Points de distribution cloud**.  
> 2. Ajoutez l’attribut **Modèle de déploiement** comme colonne de la vue de liste. Pour un déploiement Resource Manager, cet attribut est **Azure Resource Manager**.  


### <a name="stop-or-start-the-cloud-service-on-demand"></a>Arrêter ou démarrer le service cloud à la demande

Vous pouvez arrêter un point de distribution cloud à tout moment dans la console Configuration Manager. Cette opération empêche immédiatement les clients de télécharger tout autre contenu à partir du service. Redémarrez le service cloud à partir de la console Configuration Manager pour restaurer l’accès des clients. Par exemple, vous pouvez arrêter un service cloud lorsqu’il atteint un seuil de données.  

Lorsque vous arrêtez un point de distribution cloud, le service cloud ne supprime pas le contenu du compte de stockage. Il n’empêche pas non plus le serveur de site de transférer du contenu vers le point de distribution cloud. Le point de gestion retourne toujours le point de distribution cloud aux clients, comme une source de contenu valide. 

Utilisez la procédure suivante pour arrêter un point de distribution cloud :  

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Services cloud**, puis sélectionnez le nœud **Points de distribution cloud**.  

2. Sélectionnez le point de distribution cloud. Pour arrêter le service cloud qui s’exécute dans Azure, sélectionnez **Arrêter le service** dans le ruban.  

3. Sélectionnez **Démarrer le service** pour redémarrer le point de distribution cloud.  


### <a name="delete-a-cloud-distribution-point"></a>Supprimer un point de distribution cloud

Pour désinstaller un point de distribution cloud, sélectionnez-le à partir de la console Configuration Manager, puis sélectionnez **Supprimer**.  

Lorsque vous supprimez un point de distribution cloud d’une hiérarchie, Configuration Manager supprime le contenu du service cloud dans Azure. 

La suppression manuelle de tout composant dans Azure entraîne l’incohérence du système. Cet état conserve des informations orphelines, et des comportements inattendus peuvent se produire.



## <a name="bkmk_tshoot"></a> Dépannage avancé

Si vous avez besoin de collecter les données du journal de diagnostic à partir des machines virtuelles Azure afin de résoudre les problèmes liés à votre point de distribution cloud, utilisez l’exemple PowerShell suivant pour activer l’extension de diagnostic de service pour l’abonnement : <!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using 
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using 

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script. 
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate 
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```


L’exemple suivant est un exemple de fichier **diagnostics.wadcfgx**, comme celui qui est référencé dans la variable **public_config** du script PowerShell ci-dessus. Pour plus d’informations, consultez [Schéma de configuration de l’extension Azure Diagnostics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

