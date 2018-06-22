---
title: Fichiers journaux pour la résolution des problèmes
titleSuffix: Configuration Manager
description: Utilisez des fichiers journaux pour résoudre des problèmes liés aux systèmes de site et aux clients Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c068ea5a079d43148191e41dc9a2b4fb7a2e00c7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342662"
---
# <a name="log-files-in-system-center-configuration-manager"></a>Fichiers journaux dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, les composants des clients et des serveurs de site enregistrent les informations sur les processus dans des fichiers journaux individuels. Vous pouvez utiliser les informations contenues dans ces fichiers journaux pour résoudre les problèmes susceptibles de survenir. Par défaut, Configuration Manager active la journalisation pour les composants client et serveur.   

 Les sections suivantes contiennent des détails sur les différents fichiers journaux disponibles. Surveillez les journaux des clients et serveurs Configuration Manager afin de connaître les détails des opérations, ainsi que pour afficher les informations d’erreur pour résoudre les problèmes.  

-   [À propos des fichiers journaux de Configuration Manager](#BKMK_AboutLogs)  

    -   [Configurer des options de journalisation à l’aide du Gestionnaire de service de Configuration Manager](#BKMK_LogOptions)  

    -   [Localisation des fichiers journaux de Configuration Manager](#BKMK_LogLocation)  

-   [Journaux du client Configuration Manager](#BKMK_ClientLogs)  

    -   [Opérations du client](#BKMK_ClientOpLogs)  

    -   [Fichiers journaux de l’installation du client](#BKMK_ClientInstallLog)  

    -   [Client pour Linux et UNIX](#BKMK_LogFilesforLnU)  

    -   [Client pour ordinateurs Mac](#BKMK_LogfilesforMac)  

-   [Fichiers journaux du serveur de site Configuration Manager](#BKMK_ServerLogs)  

    -   [Journaux de serveur de site et de serveur de système de site](#BKMK_SiteSiteServerLog)  

    -   [Fichiers journaux de l’installation du serveur de site](#BKMK_SiteInstallLog) 

    -   [Fichiers journaux du point de service de l’entrepôt de données](#BKMK_DataWarehouse)

    -   [Fichiers journaux du point d’état de secours](#BKMK_FSPLog)  

    -   [Fichiers journaux du point de gestion](#BKMK_MPLog)  

    -   [Fichiers journaux du point de mise à jour logicielle](#BKMK_SUPLog)  

-   [Fichiers journaux pour les fonctionnalités de Configuration Manager](#BKMK_FunctionLogs)  

    -   [Gestion des applications](#BKMK_AppManageLog)  

    -   [Asset intelligence](#BKMK_AILog)  

    -   [Sauvegarde et récupération](#BKMK_BnRLog)  

    -   [Inscription de certificats](#BKMK_CertificateEnrollment)

    -   [Notification du client](#BKMK_BGB)

    -   [Passerelle de gestion cloud](#cloud-management-gateway)

    -   [Paramètres de conformité et accès aux ressources d’entreprise](#BKMK_CompSettingsLog)  

    -   [Accès conditionnel](#BKMK_CA)

    -   [Console Configuration Manager](#BKMK_ConsoleLog)  

    -   [Gestion de contenu](#BKMK_ContentLog)  

    -   [Détection](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Extensions](#BKMK_Extensions)  

    -   [Inventaire](#BKMK_InventoryLog)  

    -   [Contrôle](#BKMK_MeteringLog)  

    -   [Migration](#BKMK_MigrationLog)  

    -   [Appareils mobiles](#BKMK_MDMLog)  

    -   [Déploiement de systèmes d’exploitation](#BKMK_OSDLog)  

    -   [Gestion de l’alimentation](#BKMK_PowerMgmtLog)  

    -   [Contrôle à distance](#BKMK_RCLog)  

    -   [Rapports](#BKMK_ReportLog)  

    -   [Administration basée sur des rôles](#BKMK_RBALog)  

    -   [Point de connexion de service](#BKMK_WITLog)  

    -   [Mises à jour logicielles](#BKMK_SU_NAPLog)  

    -   [Wake On LAN](#BKMK_WOLLog)  

    -   [Maintenance de Windows 10](#BKMK_WindowsServicingLog)

    -   [Agent Windows Update](#BKMK_WULog)  

    -   [Serveur WSUS](#BKMK_WSUSLog)  

##  <a name="BKMK_AboutLogs"></a> À propos des fichiers journaux de Configuration Manager  
 La plupart des processus dans Configuration Manager consignent des informations sur les opérations dans un fichier journal dédié à ce processus. Ces fichiers journaux sont identifiés par des extensions de fichier **.log** ou **.lo_**. Configuration Manager écrit dans un fichier .log jusqu’à ce que ce journal atteigne sa taille maximale. Une fois le journal plein, le fichier .log est copié vers un fichier portant le même nom mais avec l’extension .lo_, et le processus ou le composant continue à écrire dans le fichier .log. Quand le fichier .log atteint à nouveau sa taille maximale, le fichier .lo_ est remplacé et le processus se répète. Certains composants établissent un historique du fichier journal en ajoutant une date et une heure au nom du fichier journal, et en conservant l’extension .log. Le client pour Linux et UNIX constitue une exception à la taille maximale et à l’utilisation du fichier .lo_. Pour plus d’informations sur la façon dont le client pour Linux et UNIX utilise les fichiers journaux, consultez [Gérer des fichiers journaux dans le client pour Linux et UNIX](#BKMK_ManageLinuxLogs) dans cet article.  

 Pour afficher les journaux, utilisez la visionneuse du journal Configuration Manager, CMTrace, qui se trouve dans le dossier \\\SMSSetup\\Tools du média source de Configuration Manager. Il est ajouté à toutes les images de démarrage ajoutées à la Bibliothèque de logiciels.  

###  <a name="BKMK_LogOptions"></a> Configurer des options de journalisation à l’aide du Gestionnaire de service de Configuration Manager  
 Vous pouvez changer l’emplacement où Configuration Manager stocke les fichiers journaux, ainsi que leur taille.  

 Pour modifier la taille des fichiers journaux, changer le nom et l’emplacement du fichier journal, ou forcer plusieurs composants à écrire dans un même fichier journal, procédez comme suit :  

#### <a name="to-modify-logging-for-a-component"></a>Pour modifier la journalisation pour un composant  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**, sélectionnez **État du système**, puis sélectionnez **État du site** ou **État du composant**.  
2.  Sous l’onglet **Accueil**, dans le groupe **Composant**, sélectionnez **Démarrer**, puis sélectionnez **Gestionnaire de service de Configuration Manager**.  
3.  Quand le Gestionnaire de service de Configuration Manager s’ouvre, connectez-vous au site que vous voulez gérer. Si le site que vous voulez gérer n’apparaît pas, sélectionnez **Site**, sélectionnez **Se connecter** et entrez le nom du serveur de site pour le site correct.  
4.  Développez le site et accédez à **Composants** ou à **Serveurs** selon l’emplacement où se trouvent les composants que vous voulez gérer.  
5.  Dans le volet de droite, sélectionnez un ou plusieurs composants.  
6.  Dans le menu **Composant**, sélectionnez **Journalisation**.  
7.  Dans la boîte de dialogue **Enregistrement du composant Configuration Manager** , choisissez les options de configuration disponibles pour votre sélection.  
8.  Cliquez sur **OK** pour enregistrer la configuration.  

###  <a name="BKMK_LogLocation"></a> Localiser les fichiers journaux de Configuration Manager  
Configuration Manager stocke les fichiers journaux dans différents emplacements. Ces emplacements dépendent du processus qui crée le fichier journal et de la configuration de vos systèmes de site. L’emplacement du fichier journal pouvant varier sur un ordinateur, utilisez la fonction de recherche pour localiser les fichiers journaux appropriés sur votre ordinateur Configuration Manager si vous devez résoudre les problèmes pour un scénario spécifique.  

##  <a name="BKMK_ClientLogs"></a> Journaux du client Configuration Manager  
Les sections suivantes répertorient les fichiers journaux liés aux opérations et à l’installation du client.  

###  <a name="BKMK_ClientOpLogs"></a> Opérations du client  
Le tableau suivant répertorie les fichiers journaux qui se trouvent sur le client Configuration Manager.  

|Nom du fichier journal|Description|  
|--------------|-----------------|  
|CAS.log|Service d’accès au contenu. Conserve le cache du package local sur le client.|  
|Ccm32BitLauncher.log|Enregistre les actions liées au démarrage des applications sur le client marqué *run as 32 bit* (exécuter en 32 bits).|  
|CcmEval.log|Enregistre des activités d’évaluation liées à l’état du client Configuration Manager et des détails sur les composants exigés par le client Configuration Manager.|  
|CcmEvalTask.log|Enregistre des activités d’évaluation liées à l’état du client Configuration Manager lancées par la tâche planifiée d’évaluation.|  
|CcmExec.log|Enregistre les activités du client et du service Hôte d'agent SMS. Ce fichier journal inclut également des informations sur l'activation et la désactivation du proxy de mise en éveil.|  
|CcmMessaging.log|Enregistre les activités liées à la communication entre le client et les points de gestion.|  
|CCMNotificationAgent.log|Enregistre les activités liées aux opérations de notification du client.|  
|Ccmperf.log|Enregistre les activités liées à la maintenance et la capture de données relatives aux compteurs de performances du client.|  
|CcmRestart.log|Enregistre les activités de redémarrage du client.|  
|CCMSDKProvider.log|Enregistre les activités pour les interfaces du kit de développement logiciel (SDK) client.|  
|CertificateMaintenance.log|Conserve les certificats pour les points de gestion et le service de domaine Active Directory.|  
|CIDownloader.log|Enregistre des détails sur les téléchargements des définitions des éléments de configuration.|  
|CITaskMgr.log|Enregistre les tâches lancées pour chaque type d’application et de déploiement, comme le téléchargement de contenu, et les actions d’installation ou de désinstallation.|  
|ClientAuth.log|Enregistre l’activité de signature et d’authentification pour le client.|  
|ClientIDManagerStartup.log|Crée et conserve le GUID du client et identifie les tâches effectuées pendant l'inscription et l'attribution des clients.|  
|ClientLocation.log|Enregistre les tâches liées à l'attribution d'un site client.|  
|CMHttpsReadiness.log|Enregistre les résultats de l’exécution de l’outil d’évaluation d’analyse HTTPS de Configuration Manager. Cet outil vérifie si les ordinateurs disposent d’un certificat d’authentification de client PKI qui peut être utilisé avec Configuration Manager.|  
|CmRcService.log|Enregistre des informations pour le service de contrôle à distance.|  
|ContentTransferManager.log|Planifie le service BITS (Background Intelligent Transfer Service) ou SMB (Server Message Block) pour leur permettre de télécharger des packages ou d’y accéder.|  
|DataTransferService.log|Enregistre toutes les communications BITS relatives à l'accès aux stratégies ou aux packages.|  
|EndpointProtectionAgent|Enregistre des informations concernant l’installation du client System Center Endpoint Protection et l’application de la stratégie anti-programme malveillant à ce client.|  
|execmgr.log|Enregistre des détails concernant les packages et les séquences de tâches qui s'exécutent sur le client.|  
|ExpressionSolver.log|Enregistre des informations détaillées concernant les méthodes de détection améliorées utilisées quand la journalisation détaillée ou de débogage est activée.|  
|ExternalEventAgent.log|Enregistre l'historique de la détection des programmes malveillants par Endpoint Protection et des événements liés à l'état du client.|  
|FileBITS.log|Enregistre toutes les tâches d'accès aux packages SMB.|  
|FileSystemFile.log|Enregistre l'activité du fournisseur de l'infrastructure de gestion Windows (WMI) pour l'inventaire logiciel et le regroupement de fichiers.|  
|FSPStateMessage.log|Enregistre l'activité des messages d'état envoyés par le client au point d'état de secours.|  
|InternetProxy.log|Enregistre l’activité de configuration de proxy et d’utilisation réseau pour le client.|  
|InventoryAgent.log|Enregistre les activités de l'inventaire matériel et logiciel et les actions de découverte par pulsations effectuées sur le client.|  
|LocationCache.log|Enregistre l’activité d’utilisation de l’emplacement du cache et de maintenance pour le client.|  
|LocationServices.log|Enregistre l'activité du client pour la localisation des points de gestion, des points de mise à jour logicielle et des points de distribution.|  
|MaintenanceCoordinator.log|Enregistre l’activité des tâches de maintenance générale pour le client.|  
|Mifprovider.log|Enregistre l’activité du fournisseur WMI pour les fichiers .MIF (Management Information Format).|  
|mtrmgr.log|Surveille tous les processus de contrôle des logiciels.|  
|PolicyAgent.log|Enregistre les demandes de stratégie effectuées via le service de transfert de données.|  
|PolicyAgentProvider.log|Enregistre les changements de stratégie.|  
|PolicyEvaluator.log|Enregistre des détails concernant l'évaluation des stratégies sur les ordinateurs clients, dont les stratégies de mises à jour logicielles.|  
|PolicyPlatformClient.log|Enregistre le processus de correction et de conformité pour tous les fournisseurs dans %Program Files%\Microsoft Policy Platform, à l’exception du fournisseur de fichier.|  
|PolicySdk.log|Enregistre les activités pour les interfaces du kit de développement logiciel (SDK) de système de stratégie.|  
|Pwrmgmt.log|Enregistre les informations liées à l'activation ou à la désactivation et à la configuration des paramètres client du proxy de mise en éveil.|  
|PwrProvider.log|Enregistre les activités du fournisseur de la gestion de l’alimentation (PWRInvProvider) hébergé dans le service WMI. Sur toutes les versions prises en charge de Windows, le fournisseur énumère les paramètres actuels sur les ordinateurs pendant l'inventaire matériel et applique des paramètres de mode d'alimentation.|  
|SCClient_&lt;*domaine*\>@&lt;*nom_utilisateur*\>_1.log|Enregistre l'activité dans le centre logiciel pour l'utilisateur spécifié sur l'ordinateur client.|  
|SCClient_&lt;*domaine*\>@&lt;*nom_utilisateur*\>_2.log|Enregistre l'historique des activités dans le centre logiciel pour l'utilisateur spécifié sur l'ordinateur client.|  
|Scheduler.log|Enregistre les activités des tâches planifiées pour toutes les opérations du client.|  
|SCNotify_&lt;*domaine*\>@&lt;*nom_utilisateur*\>_1.log|Enregistre l'activité de notification des utilisateurs sur les logiciels pour l'utilisateur spécifié.|  
|SCNotify_&lt;*domaine*\>@&lt;*nom_utilisateur*\>_1-&lt;*date_heure*>.log|Enregistre l'historique des informations de notification des utilisateurs sur les logiciels pour l'utilisateur spécifié.|  
|setuppolicyevaluator.log|Enregistre la création de stratégies d'inventaire et de configuration dans WMI.|  
|SleepAgent_&lt;*domaine*\>@SYSTEM_0.log|Fichier journal principal pour le proxy de mise en éveil.|  
|smscliui.log|Enregistre l’utilisation du client Configuration Manager dans le Panneau de configuration.|  
|SrcUpdateMgr.log|Enregistre l'activité pour les applications Windows Installer installées, qui sont mises à jour avec les emplacements sources du point de distribution actuel.|  
|StatusAgent.log|Enregistre les messages d'état créés par les composants des clients.|  
|SWMTRReportGen.log|Génère un rapport des données d’utilisation collectées par l’agent de contrôle. Ces données sont enregistrées dans le fichier journal Mtrmgr.log.|  
|UserAffinity.log|Enregistre les détails relatifs à l'affinité entre appareil et utilisateur.|  
|VirtualApp.log|Enregistre des informations spécifiques à l’évaluation des types de déploiement App-V (Application Virtualization).|  
|Wedmtrace.log|Enregistre les opérations liées aux filtres d'écriture sur les clients Windows Embedded.|  
|wakeprxy-install.log|Enregistre les informations liées à l’installation quand les clients reçoivent l’option du paramètre client d’activation du proxy de mise en éveil.|  
|wakeprxy-uninstall.log|Enregistre les informations liées à la désinstallation du proxy de mise en éveil quand les clients reçoivent l’option de désactivation du paramètre client du proxy de mise en éveil, si ce proxy a été précédemment activé.|  

###  <a name="BKMK_ClientInstallLog"></a> Fichiers journaux de l’installation du client  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à l’installation du client Configuration Manager.  

|Nom du fichier journal|Description|  
|--------------|-----------------|  
|ccmsetup.log|Enregistre les tâches de ccmsetup.exe liées au programme d’installation du client, à la mise à niveau du client et à la suppression de client. Permet de dépanner des problèmes d'installation du client.|  
|ccmsetup-ccmeval.log|Enregistre les tâches de ccmsetup.exe liées à l’état et à la correction du client.|  
|CcmRepair.log|Enregistre les activités de réparation de l'agent du client.|  
|client.msi.log|Enregistre les tâches d'installation exécutées par client.msi. Permet de dépanner les problèmes d'installation ou de suppression du client.|  

###  <a name="BKMK_LogFilesforLnU"></a> Client pour Linux et UNIX  
 Le client Configuration Manager pour Linux et UNIX enregistre les informations dans les fichiers journaux suivants :  

> [!TIP]  
>  Utilisez CMTrace pour afficher les fichiers journaux du client pour Linux et UNIX.  

> [!NOTE]  
>  Lorsque vous utilisez la version initiale du client pour Linux et UNIX et faites référence à la documentation de cette section, remplacez les références suivantes pour chaque fichier ou processus :  
>   
>  -   Remplacez **omiserver.bin** par **nwserver.bin**  
> -   Remplacez **omi** par **nanowbem**  

|Nom du fichier journal|Détails|  
|--------------|-------------|  
|Scxcm.log|Fichier journal pour le service principal du client Configuration Manager pour Linux et UNIX (ccmexec.bin). Ce fichier journal contient des informations liées à l'installation et aux opérations en cours de ccmexec.bin.<br /><br /> Par défaut, ce fichier journal se trouve dans **/var/opt/microsoft/scxcm.log**<br /><br /> Pour définir un autre emplacement pour le fichier journal, modifiez **/opt/microsoft/configmgr/etc/scxcm.conf** et changez le champ **PATH** . Il n'est pas nécessaire de redémarrer l'ordinateur ou le service client pour appliquer la modification.<br /><br /> Vous pouvez définir le niveau de journalisation sur quatre valeurs différentes.|  
|Scxcmprovider.log|Fichier journal pour le service CIM du client Configuration Manager pour Linux et UNIX (omiserver.bin). Ce fichier journal contient les informations liées aux opérations en cours de nwserver.bin.<br /><br /> Ce fichier journal se trouve dans **/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Pour définir un autre emplacement pour le fichier journal, modifiez **/opt/microsoft/omi/etc/scxcmprovider.conf** et changez le champ **PATH** . Il n'est pas nécessaire de redémarrer l'ordinateur ou le service client pour appliquer la modification.<br /><br /> Vous pouvez définir le niveau de journalisation sur trois valeurs différentes.|  

 Les deux fichiers journaux prennent en charge plusieurs niveaux de journalisation :  

-   **scxcm.log**. Pour changer le niveau de journalisation, ouvrez **/opt/microsoft/configmgr/etc/scxcm.conf** et changez chaque instance de l’étiquette **MODULE** pour le niveau de journalisation souhaité :  

    -   ERROR : indique des problèmes nécessitant votre attention.  

    -   WARNING : indique des problèmes possibles pour les opérations du client.  

    -   INFO : une journalisation plus détaillée indiquant l’état de différents événements sur le client.  

    -   TRACE : une journalisation détaillée généralement utilisée pour diagnostiquer les problèmes.  

-   **scxcmprovider.log**. Pour définir un autre niveau de journal, modifiez **/opt/microsoft/omi/etc/scxcmprovider.conf** et changez chaque instance de la balise **MODULE** au niveau de journal souhaité :  

    -   ERROR : indique des problèmes nécessitant votre attention.  

    -   WARNING : indique des problèmes possibles pour les opérations du client.

    -   INFO : une journalisation plus détaillée indiquant l’état de différents événements sur le client.  

Dans des conditions de fonctionnement normales, utilisez le niveau de journalisation ERROR. Ce niveau de journalisation crée le fichier journal le plus petit. Au fil de l’augmentation du niveau de journalisation d’ERROR à WARNING, à INFO, puis à TRACE, un fichier journal à chaque fois plus volumineux est créé car plus de données sont écrites dans le fichier journal.  

####  <a name="BKMK_ManageLinuxLogs"></a> Gérer les fichiers journaux du client Linux et UNIX  
Le client pour Linux et UNIX ne limite pas la taille maximale des fichiers journaux du client. Il ne copie pas non plus automatiquement le contenu de ses fichiers .log dans un autre fichier, comme un fichier .lo_. Si vous voulez contrôler la taille maximale des fichiers journaux, implémentez un processus pour gérer les fichiers journaux indépendamment du client Configuration Manager pour Linux et UNIX.  

Par exemple, vous pouvez utiliser la commande Linux et UNIX standard **logrotate** pour gérer la taille et la rotation des fichiers journaux du client. Le client Configuration Manager pour Linux et UNIX a une interface qui permet à **logrotate** de signaler au client le moment où la rotation des journaux est terminée. Le client peut ainsi reprendre la journalisation dans le fichier journal.  

Pour plus d'informations sur **logrotate**, consultez la documentation des distributions Linux et UNIX que vous utilisez.  

###  <a name="BKMK_LogfilesforMac"></a> Client pour ordinateurs Mac  
Le client Configuration Manager pour les ordinateurs Mac enregistre les informations dans les fichiers journaux suivants :  

|Nom du fichier journal|Détails|  
|--------------|-------------|  
|CCMClient-&lt;*date_heure*>.log|Enregistre les activités liées aux opérations du client Mac, notamment la gestion des applications, l’inventaire et la journalisation des erreurs.<br /><br /> Ce fichier journal se trouve dans le dossier /Library/Application Support/Microsoft/CCM/Logs sur l’ordinateur Mac.|  
|CCMAgent-&lt;*date_heure*>.log|Enregistre les informations liées aux opérations du client, notamment les opérations d’ouverture et de fermeture de session utilisateur et l’activité de l’ordinateurs Mac.<br /><br /> Ce fichier journal se trouve dans le dossier ~/Library/Logs sur l’ordinateur Mac.|  
|CCMNotifications-&lt;*date_heure*>.log|Enregistre les activités liées aux notifications Configuration Manage affichées sur l’ordinateur Mac.<br /><br /> Ce fichier journal se trouve dans le dossier ~/Library/Logs sur l’ordinateur Mac.|  
|CCMPrefPane-&lt;*date_heure*>.log|Enregistre les activités liées à la boîte de dialogue Préférences de Configuration Manager sur l’ordinateur Mac, ce qui inclut l’état général et la journalisation des erreurs.<br /><br /> Ce fichier journal se trouve dans le dossier ~/Library/Logs sur l’ordinateur Mac.|  

Le fichier journal SMS_DM.log sur le serveur de système de site enregistre aussi les communications entre les ordinateurs Mac et le point de gestion configuré pour les appareils mobiles et les ordinateurs Mac.  

##  <a name="BKMK_ServerLogs"></a> Fichiers journaux du serveur de site Configuration Manager  
 Les sections suivantes répertorient les fichiers journaux qui se trouvent sur le serveur de site ou qui sont liés à des rôles de système de site spécifiques.  

###  <a name="BKMK_SiteSiteServerLog"></a> Journaux de serveur de site et de serveur de système de site  
 Le tableau suivant répertorie les fichiers journaux qui se trouvent sur le serveur de site et les serveurs de système de site Configuration Manager.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Enregistre les activités de traitement des inscriptions.|Serveur de site|  
|ADForestDisc.log|Enregistre les actions de découverte de forêts Active Directory.|Serveur de site|  
|ADService.log|Enregistre la création de compte et les détails des groupes de sécurité dans Active Directory.|Serveur de site|  
|adsgdis.log|Enregistre les actions de découverte de groupe Active Directory.|Serveur de site|  
|adsysdis.log|Enregistre les actions de découverte du système Active Directory.|Serveur de site|  
|adusrdis.log|Enregistre les actions de découverte d'utilisateurs Active Directory.|Serveur de site|  
|ccm.log|Enregistre les activités de l'installation poussée du client.|Serveur de site|  
|CertMgr.log|Enregistre les activités de certificat pour la communication intra-site.|Serveur de système de site|  
|chmgr.log|Enregistre les activités du gestionnaire d'intégrité du client.|Serveur de site|  
|Cidm.log|Enregistre les modifications apportées aux paramètres du client par le Gestionnaire de données d'installation des clients (CIDM).|Serveur de site|  
|colleval.log|Enregistre des détails concernant la création, la modification et la suppression de regroupements par l'Évaluateur de regroupements.|Serveur de site|  
|compmon.log|Enregistre l'état des threads du composant surveillé pour le serveur de site.|Serveur de système de site|  
|compsumm.log|Enregistre les tâches de l'Outil de synthèse d'état des composants.|Serveur de site|  
|ComRegSetup.log|Enregistre l'installation initiale des résultats d'inscription COM d'un serveur de site.|Serveur de système de site|  
|dataldr.log|Enregistre des informations sur le traitement des fichiers MIF et de l’inventaire matériel dans la base de données Configuration Manager.|Serveur de site|  
|ddm.log|Enregistre les activités du gestionnaire de données de découverte.|Serveur de site|  
|despool.log|Enregistre les transferts de communications entrantes de site à site.|Serveur de site|  
|distmgr.log|Enregistre les détails concernant la création, la compression, la réplication delta et la mise à jour des informations des packages.|Serveur de site|  
|EPCtrlMgr.log|Enregistre des informations concernant la synchronisation des informations sur les menaces de programmes malveillants à partir du serveur de rôle de système de site Endpoint Protection avec la base de données Configuration Manager.|Serveur de site|  
|EPMgr.log|Enregistre l'état du rôle de système de site Endpoint Protection.|Serveur de système de site|  
|EPSetup.log|Fournit des informations sur l'installation du rôle de système de site Endpoint Protection.|Serveur de système de site|  
|EnrollSrv.log|Enregistre les activités du processus du service d'inscription.|Serveur de système de site|  
|EnrollWeb.log|Enregistre les activités du processus du site Web d'inscription.|Serveur de système de site|  
|fspmgr.log|Enregistre les activités du rôle de système de site d'un point d'état de secours.|Serveur de système de site|  
|hman.log|Enregistre des informations sur les modifications de la configuration du site et sur la publication d’informations du site dans les services de domaine Active Directory.|Serveur de site|  
|Inboxast.log|Enregistre les fichiers déplacés du point de gestion vers le dossier Boîtes de réception correspondant sur le serveur de site.|Serveur de site|  
|inboxmgr.log|Enregistre les activités de transfert de fichier entre les dossiers des boîtes de réception.|Serveur de site|  
|inboxmon.log|Enregistre le traitement des fichiers des boîtes de réception et des mises à jour du compteur de performances.|Serveur de site|  
|invproc.log|Enregistre le transfert des fichiers MIF d'un site secondaire vers son site parent.|Serveur de site|  
|migmctrl.log|Enregistre des informations sur les actions de migration qui impliquent des tâches de migration, des points de distribution partagés et des mises à niveau des points de distribution.|Site de plus haut niveau dans la hiérarchie Configuration Manager et chaque site principal enfant.<br /><br /> Dans une hiérarchie comportant plusieurs sites principaux, utilisez le fichier journal créé sur le site d’administration centrale.|  
|mpcontrol.log|Enregistre l’inscription du point de gestion auprès de WINS (Windows Internet Name Service). Enregistre la disponibilité du point de gestion toutes les dix minutes.|Serveur de système de site|  
|mpfdm.log|Enregistre les actions du composant du point de gestion qui déplace les fichiers du client vers le dossier Boîtes de réception correspondant sur le serveur de site.|Serveur de système de site|  
|mpMSI.log|Enregistre des détails sur l’installation du point de gestion.|Serveur de site|  
|MPSetup.log|Enregistre le processus de wrapper d'installation du point de gestion.|Serveur de site|  
|netdisc.log|Enregistre les actions de découverte du réseau.|Serveur de site|  
|ntsvrdis.log|Enregistre l'activité de découverte des serveurs de système de site.|Serveur de site|  
|Objreplmgr|Enregistre le traitement des notifications de modification d'objet pour la réplication.|Serveur de site|  
|offermgr.log|Enregistre les mises à jour des publications.|Serveur de site|  
|offersum.log|Enregistre la synthèse des messages d'état du déploiement.|Serveur de site|  
|OfflineServicingMgr.log|Enregistre les activités de mise à jour des fichiers d'image de systèmes d'exploitation.|Serveur de site|  
|outboxmon.log|Enregistre le traitement des fichiers de la boîte d'envoi et des mises à jour du compteur de performances.|Serveur de site|  
|PerfSetup.log|Enregistre les résultats de l'installation des compteurs de performance.|Serveur de système de site|  
|PkgXferMgr.log|Enregistre les actions du composant SMS_Executive chargé de l’envoi de contenu d’un site principal vers un point de distribution distant.|Serveur de site|  
|policypv.log|Enregistre les mises à jour des stratégies du client pour refléter les modifications apportées aux paramètres du client ou aux déploiements.|Serveur de site principal|  
|rcmctrl.log|Enregistre les activités de réplication de la base de données entre les sites dans la hiérarchie.|Serveur de site|  
|replmgr.log|Enregistre la réplication de fichiers entre les composants du serveur de site et le composant Planificateur.|Serveur de site|  
|ResourceExplorer.log|Enregistre les erreurs, avertissements et informations liés à l’exécution de l’Explorateur de ressources.|Ordinateur qui exécute la console Configuration Manager|  
|ruleengine.log|Enregistre des détails concernant les règles de déploiement automatique pour l'identification, le téléchargement de contenu et la création de groupe et de déploiement de mises à jour logicielles.|Serveur de site|  
|schedule.log|Enregistre des détails concernant la réplication des travaux de site à site et de fichiers.|Serveur de site|  
|Sender.log|Enregistre les fichiers qui sont transférés par réplication basée sur les fichiers entre les sites.|Serveur de site|  
|sinvproc.log|Enregistre des informations sur le traitement des données d'inventaire logiciel vers la base de données de site.|Serveur de site|  
|sitecomp.log|Enregistre des détails concernant la maintenance des composants du site installés sur tous les serveurs de système de site du site.|Serveur de site|  
|sitectrl.log|Enregistre des modifications dans les paramètres du site apportées aux objets de contrôle de site dans la base de données.|Serveur de site|  
|sitestat.log|Enregistre le processus de surveillance de la disponibilité et de l'espace disque de tous les systèmes de site.|Serveur de site|
|SMS_PhasedDeployment.log| Fichier journal pour les déploiements en plusieurs phases, une fonctionnalité en préversion à compter de Configuration Manager version 1802.|Site de niveau supérieur dans la hiérarchie Configuration Manager|   
|SmsAdminUI.log|Enregistre l’activité de la console Configuration Manager.|Ordinateur qui exécute la console Configuration Manager|  
|SMSAWEBSVCSetup.log|Enregistre les activités d'installation du service Web du catalogue des applications.|Serveur de système de site|  
|smsbkup.log|Enregistre les résultats du processus de sauvegarde de site.|Serveur de site|  
|smsdbmon.log|Enregistre les modifications de la base de données.|Serveur de site|  
|SMSENROLLSRVSetup.log|Enregistre les activités d'installation du service Web d'inscription.|Serveur de système de site|  
|SMSENROLLWEBSetup.log|Enregistre les activités d'installation du site Web d'inscription.|Serveur de système de site|  
|smsexec.log|Enregistre le traitement de tous les threads du composant de serveur de site.|Serveur de site ou serveur de système de site|  
|SMSFSPSetup.log|Enregistre les messages générés par l'installation d'un point d'état de secours.|Serveur de système de site|  
|SMSPORTALWEBSetup.log|Enregistre les activités d'installation du site Web du catalogue des applications.|Serveur de système de site|  
|SMSProv.log|Enregistre les accès du fournisseur WMI à la base de données du site.|Ordinateur sur lequel le fournisseur SMS est installé|  
|srsrpMSI.log|Enregistre des résultats détaillés du processus d'installation du point de rapport à partir de la sortie MSI.|Serveur de système de site|  
|srsrpsetup.log|Enregistre les résultats du processus d'installation du point de rapport.|Serveur de système de site|  
|statesys.log|Enregistre le traitement des messages du système d'état.|Serveur de site|  
|statmgr.log|Enregistre l'écriture de tous les messages d'état dans la base de données.|Serveur de site|  
|swmproc.log|Enregistre le traitement des fichiers et des paramètres de contrôle.|Serveur de site|  

###  <a name="BKMK_SiteInstallLog"></a> Fichiers journaux de l’installation du serveur de site  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à l'installation du site.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Enregistre les activités d’évaluation et d’installation des composants prérequis.|Serveur de site|  
|ConfigMgrSetup.log|Enregistre les résultats détaillés de l’installation du serveur de site.|Serveur de site|  
|ConfigMgrSetupWizard.log|Enregistre les informations liées à l’activité dans l’Assistant Installation.|Serveur de site|  
|SMS_BOOTSTRAP.log|Enregistre des informations sur l'avancement du lancement du processus d'installation de site secondaire. Les détails du processus d'installation proprement dit sont donnés dans ConfigMgrSetup.log.|Serveur de site|  
|smstsvc.log|Enregistre des informations sur l’installation, l’utilisation et la suppression d’un service Windows utilisé pour tester la connectivité du réseau et les autorisations entre les serveurs, en utilisant le compte d’ordinateur du serveur à l’origine de la connexion.|Serveur de site et serveur de système de site|  

###  <a name="BKMK_DataWarehouse"></a> Fichiers journaux du point de service de l’entrepôt de données  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au point de service de l’entrepôt de données.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|Enregistre les messages générés par l’installation d’un point de service de l’entrepôt de données.|Serveur de système de site|  
|DWSSSetup.log|Enregistre les messages générés par l’installation d’un point de service de l’entrepôt de données.|Serveur de système de site|  
|Microsoft.ConfigMgrDataWarehouse.log|Enregistre des informations sur la synchronisation des données entre la base de données de site et la base de données de l’entrepôt de données.|Serveur de système de site|  

###  <a name="BKMK_FSPLog"></a> Fichiers journaux du point d’état de secours  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations sur le point d'état de secours.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Enregistre des détails concernant les communications au point d'état de secours à partir de clients hérités d'appareils mobiles et d'ordinateurs clients.|Serveur de système de site|  
|fspMSI.log|Enregistre les messages générés par l'installation d'un point d'état de secours.|Serveur de système de site|  
|fspmgr.log|Enregistre les activités du rôle de système de site d'un point d'état de secours.|Serveur de système de site|  

###  <a name="BKMK_MPLog"></a> Fichiers journaux du point de gestion  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations sur le point de gestion.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Enregistre l'activité de la messagerie du client sur le point de terminaison.|Serveur de système de site|  
|MP_CliReg.log|Enregistre l'activité de l'enregistrement du client traitée par le point de gestion.|Serveur de système de site|  
|MP_Ddr.log|Enregistre la conversion d’enregistrements XML.ddr à partir des clients, puis les copie sur le serveur de site.|Serveur de système de site|  
|MP_Framework.log|Enregistre les activités du point de gestion principal et des composants de l'infrastructure du client.|Serveur de système de site|  
|MP_GetAuth.log|Enregistre les activités d'autorisation du client.|Serveur de système de site|  
|MP_GetPolicy.log|Enregistre l'activité de demandes de stratégie des ordinateurs clients.|Serveur de système de site|  
|MP_Hinv.log|Enregistre des détails concernant la conversion des enregistrements d'inventaire matériel XML à partir de clients ainsi que la copie de ces fichiers sur le serveur de site.|Serveur de système de site|  
|MP_Location.log|Enregistre les demandes d'emplacement et les réponses données par les clients.|Serveur de système de site|  
|MP_OOBMgr.log|Enregistre les activités du point de gestion liées à la réception d’un code secret à usage unique (OTP) de la part d’un client.|Serveur de système de site|  
|MP_Policy.log|Enregistre la communication des stratégies.|Serveur de système de site|  
|MP_Relay.log|Enregistre le transfert de fichiers qui sont collectés auprès du client.|Serveur de système de site|  
|MP_Retry.log|Enregistre les processus des nouvelles tentatives d’inventaire matériel.|Serveur de système de site|  
|MP_Sinv.log|Enregistre des détails concernant la conversion des enregistrements d'inventaire logiciel XML à partir de clients ainsi que la copie de ces fichiers sur le serveur de site.|Serveur de système de site|  
|MP_SinvCollFile.log|Enregistre des détails concernant le regroupement de fichiers.|Serveur de système de site|  
|MP_Status.log|Enregistre des détails concernant la conversion des fichiers de messages d'état XML.svf de clients et la copie de ces fichiers sur le serveur de site.|Serveur de système de site|
|mpcontrol.log|Enregistre l'inscription du point de gestion dans WINS. Enregistre la disponibilité du point de gestion toutes les dix minutes.|Serveur de site|  
|mpfdm.log|Enregistre les actions du composant du point de gestion qui déplace les fichiers du client vers le dossier Boîtes de réception correspondant sur le serveur de site.|Serveur de système de site|  
|mpMSI.log|Enregistre des détails sur l’installation du point de gestion.|Serveur de site|  
|MPSetup.log|Enregistre le processus de wrapper d'installation du point de gestion.|Serveur de site|  

###  <a name="BKMK_SUPLog"></a> Fichiers journaux du point de mise à jour logicielle  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au point de mise à jour logicielle.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Enregistre les détails concernant la réplication des fichiers de notification de mises à jour logicielles, entre un site parent et des sites enfants.|Serveur de site|  
|PatchDownloader.log|Enregistre des détails concernant le processus de téléchargement des mises à jour logicielles vers la destination de téléchargement, sur le serveur de site.|Ordinateur qui héberge la console Configuration Manager à partir de laquelle les téléchargements sont lancés|  
|ruleengine.log|Enregistre des détails concernant les règles de déploiement automatique pour l'identification, le téléchargement de contenu et la création de groupe et de déploiement de mises à jour logicielles.|Serveur de site|  
|SUPSetup.log|Enregistre des détails concernant l'installation du point de mise à jour logicielle. Lorsque l'installation d'un point de mise à jour logicielle se termine, la mention **Installation was successful** est consignée dans ce fichier journal.|Serveur de système de site|  
|WCM.log|Enregistre les détails concernant la configuration du point de mise à jour logicielle et les connexions au serveur WSUS pour les catégories, les classifications et les langues des mises à jour souscrites.|Serveur de site qui se connecte au serveur WSUS|  
|WSUSCtrl.log|Enregistre des détails concernant la configuration, la connectivité de la base de données et l'intégrité du serveur WSUS du site.|Serveur de système de site|  
|wsyncmgr.log|Enregistre les détails concernant le processus de synchronisation des mises à jour logicielles.|Serveur de système de site|  
|WUSSyncXML.log|Enregistre les détails concernant l’outil d’inventaire pour le processus de synchronisation de Microsoft Updates.|Ordinateur client configuré comme hôte de synchronisation pour l’outil d’inventaire de Microsoft Updates|  

##  <a name="BKMK_FunctionLogs"></a> Fichiers journaux pour les fonctionnalités de Configuration Manager  
 Les sections suivantes répertorient les fichiers journaux liés aux fonctions de Configuration Manager.  

###  <a name="BKMK_AppManageLog"></a> Gestion des applications  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la gestion d’applications.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Enregistre des détails concernant l'état actuel et prévu des applications, leur applicabilité, si les exigences ont été respectées, les types de déploiement et les dépendances.|Client|  
|AppDiscovery.log|Enregistre les détails concernant la découverte ou la détection des applications sur les ordinateurs clients.|Client|  
|AppEnforce.log|Enregistre des détails concernant les actions de mise en œuvre (installation et désinstallation) effectuées pour les applications sur le client.|Client|  
|awebsctl.log|Enregistre les activités de surveillance du rôle de système de site du point de service web du catalogue d’applications.|Serveur de système de site|  
|awebsvcMSI.log|Enregistre les informations d'installation détaillées sur le rôle du système de site du point de service Web du catalogue d'applications.|Serveur de système de site|  
|CCMSDKProvider.log|Enregistre les activités de la gestion des applications SDK.|Client|  
|colleval.log|Enregistre des détails concernant la création, la modification et la suppression de regroupements par l'Évaluateur de regroupements.|Serveur de système de site|  
|ConfigMgrSoftwareCatalog.log|Enregistre l'activité du catalogue d'applications, dont l'utilisation de Silverlight.|Client|  
|portlctl.log|Enregistre les activités de surveillance du rôle de système de site du point de site Web du catalogue d'applications.|Serveur de système de site|  
|portlwebMSI.log|Enregistre l'activité d'installation MSI pour le rôle de site Web du catalogue d'applications.|Serveur de système de site|  
|PrestageContent.log|Enregistre les détails concernant l’utilisation de l’outil ExtractContent.exe sur un point de distribution préparé distant. Cet outil extrait le contenu qui a été exporté vers un fichier.|Serveur de système de site|  
|ServicePortalWebService.log|Enregistre l'activité du service Web du catalogue d'applications.|Serveur de système de site|  
|ServicePortalWebSite.log|Enregistre l'activité du site Web du catalogue d'applications.|Serveur de système de site|  
|SMSdpmon.log|Enregistre des détails concernant la tâche planifiée de surveillance de l'intégrité du point de distribution configurée sur un point de distribution.|Serveur de site|  
|SoftwareCatalogUpdateEndpoint.log|Enregistre les activités de gestion de l’URL du catalogue d’applications indiquée dans le Centre logiciel.|Client|  
|SoftwareCenterSystemTasks.log|Enregistre les activités liées à la validation des composants prérequis du Centre logiciel.|Client|  

 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au déploiement des packages et des programmes.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|colleval.log|Enregistre des détails concernant la création, la modification et la suppression de regroupements par l'Évaluateur de regroupements.|Serveur de site|  
|execmgr.log|Enregistre des détails concernant les packages et les séquences de tâches qui s'exécutent.|Client|  

###  <a name="BKMK_AILog"></a> Asset Intelligence  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à Asset Intelligence.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Enregistre les activités des actions d'inventaire d'Asset Intelligence.|Client|  
|aikbmgr.log|Enregistre des détails concernant le traitement des fichiers XML à partir de la boîte de réception, pour la mise à jour du catalogue Asset Intelligence.|Serveur de site|  
|AIUpdateSvc.log|Enregistre l’interaction du point de synchronisation Asset Intelligence avec SCO (System Center Online), le service web en ligne.|Serveur de système de site|  
|AIUSMSI.log|Enregistre les détails concernant l’installation du rôle de système de site du point de synchronisation Asset Intelligence.|Serveur de système de site|  
|AIUSSetup.log|Enregistre les détails concernant l’installation du rôle de système de site du point de synchronisation Asset Intelligence.|Serveur de système de site|  
|ManagedProvider.log|Enregistre des détails concernant la découverte de logiciels avec une balise d'identification logicielle associée. Enregistre également les activités liées à l’inventaire matériel.|Serveur de système de site|  
|MVLSImport.log|Enregistre des détails concernant le traitement de fichiers de licence importés.|Serveur de système de site|  

###  <a name="BKMK_BnRLog"></a> Sauvegarde et récupération  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives aux actions de sauvegarde et de restauration, notamment la réinitialisation de site, et aux modifications apportées au fournisseur SMS.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Enregistre des informations sur les tâches d’installation et de restauration quand Configuration Manager restaure un site à partir d’une sauvegarde.|Serveur de site|  
|smsbkup.log|Enregistre des détails concernant l'activité de sauvegarde du site.|Serveur de site|  
|smssqlbkup.log|Enregistre les résultats du processus de sauvegarde de la base de données de site quand SQL Server est installé sur un serveur qui n’est pas le serveur de site.|Serveur de bases de données du site|  
|Smswriter.log|Enregistre les informations sur l’état de l’enregistreur VSS Configuration Manager utilisé par le processus de sauvegarde.|Serveur de site|  

###  <a name="BKMK_CertificateEnrollment"></a> Inscription de certificats  
 Le tableau suivant répertorie les fichiers journaux de Configuration Manager qui contiennent des informations relatives à l’inscription de certificats. L’inscription de certificats utilise le point d’inscription de certificats et le module de stratégie de Configuration Manager sur le serveur qui exécute le service d’inscription de périphérique réseau.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|Crp.log|Enregistre les activités d’inscription.|Point d'enregistrement de certificat|  
|Crpctrl.log|Enregistre le bon fonctionnement du point d'enregistrement de certificat.|Point d'enregistrement de certificat|  
|Crpsetup.log|Enregistre des détails sur l'installation et la configuration du point d'enregistrement de certificat.|Point d'enregistrement de certificat|  
|Crpmsi.log|Enregistre des détails sur l'installation et la configuration du point d'enregistrement de certificat.|Point d'enregistrement de certificat|  
|NDESPlugin.log|Enregistre les activités de vérification des demandes d’accès et d’inscription des certificats.|Module de stratégie de Configuration Manager et service d’inscription d’appareils réseau|  

 En plus des fichiers journaux de Configuration Manager, consultez les journaux des applications Windows dans l’Observateur d’événements sur le serveur exécutant le service d’inscription d’appareils réseau et sur le serveur hébergeant le point d’enregistrement de certificat. Par exemple, recherchez des messages de la source **NetworkDeviceEnrollmentService** . Vous pouvez également utiliser les fichiers journaux suivants :  

-   Fichiers journaux IIS pour le service d’inscription d’appareils réseau : **&lt;chemin\>\inetpub\logs\LogFiles\W3SVC1**  

-   Fichiers journaux IIS pour le point d’inscription du certificat : **&lt;chemin\>\inetpub\logs\LogFiles\W3SVC1**  

-   Fichier journal de la stratégie d'inscription de périphérique réseau : **mscep.log**  

    > [!NOTE]  
    >  Ce fichier se trouve dans le dossier du profil de compte du service d'inscription de périphériques réseau, par exemple, dans C:\Users\SCEPSvc. Pour plus d'informations sur l'activation de la journalisation pour le service d'inscription de périphériques réseau, consultez la section [Enable Logging (Activer la journalisation)](http://go.microsoft.com/fwlink/?LinkId=320576) dans l'article Network Device Enrollment Service (NDES) in Active Directory Certificate Services (AD CS) (Service d'inscription de périphériques réseau (NDES) dans les services de certificat Active Directory (AD CS)) sur le TechNet Wiki.  

###  <a name="BKMK_BGB"></a> Notification du client  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la notification du client.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Enregistre les détails concernant les activités du serveur de site liées aux tâches de notification du client et au traitement en ligne, ainsi qu’aux fichiers d’état des tâches.|Serveur de site|  
|BGBServer.log|Enregistre les activités du serveur de notification, comme la communication client-serveur et l’envoi de tâches aux clients. Enregistre également les informations sur la génération de fichiers en ligne et de fichiers d’état de tâche à envoyer au serveur de site.|Point de gestion|  
|BgbSetup.log|Enregistre les activités du processus de wrapper d’installation du serveur de notification lors de l’installation et de la désinstallation.|Point de gestion|  
|bgbisapiMSI.log|Enregistre les détails concernant l’installation et la désinstallation du serveur de notification.|Point de gestion|  
|BgbHttpProxy.log|Enregistre les activités du proxy HTTP de notification lors de la transmission des messages des clients via HTTP depuis et vers le serveur de notification.|Client|  
|CCMNotificationAgent.log|Enregistre les activités de l’agent de notification, comme la communication client-serveur, et des informations concernant les tâches reçues et distribuées aux autres agents de client.|Client|  

### <a name="cloud-management-gateway"></a>Passerelle de gestion cloud

Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la passerelle de gestion cloud.

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Enregistre les détails concernant le déploiement du service de passerelle de gestion cloud, l’état du service en cours et les données d’utilisation associées au service.<br>Vous pouvez configurer le niveau de journalisation en modifiant la valeur **Niveau de journalisation** dans la clé de Registre HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER|Le dossier *installdir* sur le serveur de site principal ou les autorités de certification.|
|CMGSetup.log<sup>1</sup>|Enregistre des détails concernant la deuxième phase du déploiement de la passerelle de gestion cloud (déploiement local dans Azure)<br>Vous pouvez configurer le niveau de journalisation à l’aide du paramètre **Niveau de suivi** (**Information** (par défaut), **Verbose**, **Error**) dans l’onglet de **configuration du portail Azure/services cloud**.|Le dossier **%approot%\logs** sur votre serveur Azure, ou le dossier SMS/Logs sur le serveur de système de site|
|CMGHttpHandler.log<sup>1</sup>|Enregistre des détails concernant la liaison du gestionnaire http de la passerelle de gestion cloud avec Internet Information Services dans Azure<br>Vous pouvez configurer le niveau de journalisation à l’aide du paramètre **Niveau de suivi** (**Information** (par défaut), **Verbose**, **Error**) dans l’onglet de **configuration du portail Azure/services cloud**.|Le dossier **%approot%\logs** sur votre serveur Azure, ou le dossier SMS/Logs sur le serveur de système de site|
|CMGService.log<sup>1</sup>|Enregistre des détails concernant le composant principal du service de passerelle de gestion cloud dans Azure<br>Vous pouvez configurer le niveau de journalisation à l’aide du paramètre **Niveau de suivi** (**Information** (par défaut), **Verbose**, **Error**) dans l’onglet de **configuration du portail Azure/services cloud**.|Le dossier **%approot%\logs** sur votre serveur Azure, ou le dossier SMS/Logs sur le serveur de système de site|
|SMS_Cloud_</br>ProxyConnector.log|Enregistre des détails sur la configuration des connexions entre le service de passerelle de gestion cloud et le point de connexion de passerelle de gestion cloud.|Serveur de système de site|

<sup>1</sup> Il s’agit des fichiers journaux Configuration Manager locaux que le gestionnaire de services cloud synchronise toutes les cinq minutes à partir du stockage Azure. La passerelle de gestion cloud transfère (par opération push) les journaux vers le stockage Azure toutes les 5 minutes. Le délai maximal est donc de 10 minutes. Les commutateurs Verbose affectent les journaux locaux et distants. Les noms des fichiers réels incluent le nom du service et l’identificateur de l’instance de rôle. Par exemple, CMG-*NomService*-*IDInstanceRôle*-CMGSetup.log

- Pour résoudre les problèmes de déploiement, utilisez **CloudMgr.log** et **CMGSetup.log**
- Pour la résolution des problèmes d’intégrité du service, utilisez **CMGService.log** et **SMS_Cloud_ProxyConnector.log**.
- Pour résoudre les problèmes de trafic client, utilisez **CMGHttpHandler.log**, **CMGService.log** et **SMS_Cloud_ProxyConnector.log**.

###  <a name="BKMK_CompSettingsLog"></a> Paramètres de conformité et accès aux ressources d’entreprise  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives aux paramètres de compatibilité et à l'accès aux ressources de l'entreprise.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Enregistre des détails concernant le processus de correction et de compatibilité pour les paramètres de compatibilité, les mises à jour logicielles et la gestion d'applications.|Client|  
|CITaskManager.log|Enregistre des informations sur la planification des tâches des éléments de configuration.|Client|  
|DCMAgent.log|Enregistre les informations principales concernant l'évaluation, les rapports de conflit et la correction des éléments de configuration et des applications.|Client|  
|DCMReporting.log|Enregistre des informations sur les rapports des résultats de la plateforme de stratégie sous forme de messages d'état pour les éléments de configuration.|Client|  
|DcmWmiProvider.log|Enregistre des informations sur la lecture des synclets d’élément de configuration provenant de WMI.|Client|  

###  <a name="BKMK_CA"></a> Accès conditionnel
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à l’accès conditionnel.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|ADALOperationProvider.log|Enregistre des détails concernant l’acquisition du jeton AAD.|Client|  
|cloudusersync.log|Enregistre l'activation des licences des utilisateurs.|Ordinateur avec le point de connexion de service|  
|ComplRelayAgent.log|Reçoit l’état de conformité global à partir de DCM, acquiert le jeton MP, acquiert le jeton AAD et transmet la conformité à Intune (le service de relais d’autorité de certification).|Client|  
|DcmWmiProvider.log|Enregistre des informations sur la lecture des synclets d’élément de configuration provenant de WMI.|Client|  
|dmpdownloader.log|Enregistre les détails concernant les téléchargements à partir de Microsoft Intune.|Ordinateur avec le point de connexion de service|
|dmpuploader.log|Enregistre les détails concernant le chargement des modifications de la base de données sur Microsoft Intune.|Ordinateur avec le point de connexion de service|   
|MP_Token.log|Enregistre les demandes de jeton des clients.|Serveur de système de site|  

###  <a name="BKMK_ConsoleLog"></a> Console Configuration Manager  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à la console Configuration Manager.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Enregistre l’installation de la console Configuration Manager.|Ordinateur qui exécute la console Configuration Manager|  
|SmsAdminUI.log|Enregistre des informations relatives au fonctionnement de la console Configuration Manager.|Ordinateur qui exécute la console Configuration Manager|  
|SMSProv.log|Enregistre les activités effectuées par le fournisseur SMS. Les activités de la console Configuration Manager utilisent le fournisseur SMS.|Serveur de site ou serveur de système de site|  

###  <a name="BKMK_ContentLog"></a> Gestion de contenu  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la gestion de contenu.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Enregistre les détails d'un point de distribution cloud spécifique, y compris des informations sur le stockage et l'accès au contenu.|Serveur de système de site|  
|CloudMgr.log|Enregistre les détails concernant l’approvisionnement du contenu, sur la collecte de statistiques de stockage et de bande passante, et sur les actions lancées par l’administrateur pour arrêter ou démarrer le service cloud qui exécute un point de distribution cloud.|Serveur de système de site|  
|DataTransferService.log|Enregistre toutes les communications BITS relatives à l'accès aux stratégies ou aux packages. Ce journal est également utilisé pour la gestion de contenu par les points de distribution d’extraction.|Ordinateur configuré comme point de distribution d’extraction|  
|PullDP.log|Enregistre des détails concernant le contenu que le point de distribution d'extraction transfère à partir de points de distribution source.|Ordinateur configuré comme point de distribution d’extraction|  
|PrestageContent.log|Enregistre les détails concernant l’utilisation de l’outil ExtractContent.exe sur un point de distribution préparé distant. Cet outil extrait le contenu qui a été exporté vers un fichier.|Rôle de système de site|  
|SMSdpmon.log|Enregistre les détails concernant les tâches planifiées de surveillance de l’intégrité du point de distribution configurées sur un point de distribution.|Rôle de système de site|  
|smsdpprov.log|Enregistre des détails concernant l'extraction des fichiers compressés reçus à partir d'un site principal. Ce journal est généré par le fournisseur WMI du point de distribution distant.|Ordinateur de point de distribution n’est pas au même emplacement que le serveur de site|  

###  <a name="BKMK_DiscoveryLog"></a> Découverte  
Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la détection.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Enregistre les actions de la découverte du groupe de sécurité Active Directory.|Serveur de site|  
|adsysdis.log|Enregistre les actions de découverte du système Active Directory.|Serveur de site|  
|adusrdis.log|Enregistre les actions de découverte d'utilisateurs Active Directory.|Serveur de site|  
|ADForestDisc.log|Enregistre les actions de découverte de forêts Active Directory.|Serveur de site|  
|ddm.log|Enregistre les activités du gestionnaire de données de découverte.|Serveur de site|  
|InventoryAgent.log|Enregistre les activités de l'inventaire matériel et logiciel et les actions de découverte par pulsations effectuées sur le client.|Client|  
|netdisc.log|Enregistre les actions de découverte du réseau.|Serveur de site|  

###  <a name="BKMK_EPLog"></a> Endpoint Protection  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à Endpoint Protection.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Enregistre des détails concernant l'installation du client Endpoint Protection et l'application de la stratégie anti-programme malveillant à ce client.|Client|  
|EPCtrlMgr.log|Enregistre les détails concernant la synchronisation des informations sur les menaces de programmes malveillants à partir du serveur de rôle Endpoint Protection avec la base de données Configuration Manager.|Serveur de système de site|  
|EPMgr.log|Surveille l'état du rôle de système de site Endpoint Protection.|Serveur de système de site|  
|EPSetup.log|Fournit des informations sur l'installation du rôle de système de site Endpoint Protection.|Serveur de système de site|  

###  <a name="BKMK_Extensions"></a> Extensions  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées aux extensions.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Enregistre des informations sur le téléchargement des extensions de Microsoft et sur l'installation et la désinstallation de toutes les extensions.|Ordinateur qui exécute la console Configuration Manager|  
|FeatureExtensionInstaller.log|Enregistre des informations sur l’installation et la suppression d’extensions individuelles quand elles sont activées ou désactivées dans la console Configuration Manager.|Ordinateur qui exécute la console Configuration Manager|  
|SmsAdminUI.log|Enregistre l’activité de la console Configuration Manager.|Ordinateur qui exécute la console Configuration Manager|  

###  <a name="BKMK_InventoryLog"></a> Inventaire  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au traitement des données d'inventaire.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Enregistre des informations sur le traitement des fichiers MIF et de l’inventaire matériel dans la base de données Configuration Manager.|Serveur de site|  
|invproc.log|Enregistre le transfert des fichiers MIF d'un site secondaire vers son site parent.|Serveur de site secondaire|  
|sinvproc.log|Enregistre des informations sur le traitement des données d'inventaire logiciel vers la base de données de site.|Serveur de site|  

###  <a name="BKMK_MeteringLog"></a> Contrôle  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées au contrôle.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Surveille tous les processus de contrôle des logiciels.|Serveur de site|  

###  <a name="BKMK_MigrationLog"></a> Migration  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la migration.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Enregistre des informations sur les actions de migration qui impliquent des tâches de migration, des points de distribution partagés et des mises à niveau des points de distribution.|Site de plus haut niveau dans la hiérarchie Configuration Manager et chaque site principal enfant.<br /><br /> Dans une hiérarchie comportant des sites principaux multiples, utilisez le fichier journal créé sur le site d'administration centrale.|  

###  <a name="BKMK_MDMLog"></a> Appareils mobiles  
 Les sections suivantes répertorient les fichiers journaux qui contiennent des informations relatives à la gestion des appareils mobiles.  

####  <a name="BKMK_EnrollmentLog"></a> Inscription  
 Le tableau suivant répertorie les journaux qui contiennent des informations relatives à l'inscription d'appareils mobiles.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Enregistre les communications entre les points de gestion activés pour les appareils mobiles et les points de terminaison du point de gestion.|Serveur de système de site|  
|dmpmsi.log|Enregistre les données Windows Installer pour la configuration d'un point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DMPSetup.log|Enregistre la configuration du point de gestion lorsqu'il est activé pour les appareils mobiles.|Serveur de système de site|  
|enrollsrvMSI.log|Enregistre les données Windows Installer pour la configuration d'un point d'inscription.|Serveur de système de site|  
|enrollmentweb.log|Enregistre la communication entre les appareils mobiles et le point proxy d'inscription.|Serveur de système de site|  
|enrollwebMSI.log|Enregistre les données Windows Installer pour la configuration d'un point proxy d'inscription.|Serveur de système de site|  
|enrollmentservice.log|Enregistre la communication entre un point proxy d'inscription et un point d'inscription.|Serveur de système de site|  
|SMS_DM.log|Enregistre les communications entre les appareils mobiles, les ordinateurs Mac et le point de gestion activé pour les appareils mobiles et les ordinateurs Mac.|Serveur de système de site|  

####  <a name="BKMK_ExchSrvLog"></a> Connecteur Exchange Server  
 Les journaux suivants contiennent des informations relatives au connecteur Exchange Server.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Enregistre les activités et l'état du connecteur Exchange Server.|Serveur de site|  

####  <a name="BKMK_MDLegLog"></a> Client hérité d’appareil mobile  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au client hérité de l'appareil mobile.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Enregistre des détails concernant l'inscription de certificats sur les clients hérités d'appareils mobiles.|Client|  
|DMCertResp.htm|Enregistre la réponse HTML du serveur de certificats lorsque le programme d'inscription de client hérité d'appareil mobile demande un certificat PKI.|Client|  
|DmClientHealth.log|Enregistre les GUID de tous les clients hérités des appareils mobiles qui communiquent avec le point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DmClientRegistration.log|Enregistre les demandes d'inscription et leurs réponses de et vers les clients hérités d'appareils mobiles.|Serveur de système de site|  
|DmClientSetup.log|Enregistre les données d'installation du client pour les clients hérités d'appareils mobiles.|Client|  
|DmClientXfer.log|Enregistre les données de transfert de client pour les clients hérités d'appareils mobiles et les déploiements ActiveSync.|Client|  
|DmCommonInstaller.log|Enregistre l'installation des fichiers de transfert du client pour configurer les fichiers de transfert de clients hérités d'appareils mobiles.|Client|  
|DmInstaller.log|Enregistre si DMInstaller appelle DmClientSetup correctement et si DmClientSetup se termine avec ou sans erreur pour les clients hérités d'appareils mobiles.|Client|  
|DmpDatastore.log|Enregistre toutes les connexions aux bases de données de site et les requêtes effectuées par le point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DmpDiscovery.log|Enregistre toutes les données de découverte provenant des clients hérités d'appareils mobiles sur le point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DmpHardware.log|Enregistre des données d'inventaire matériel provenant de clients hérités d'appareils mobiles sur le point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DmpIsapi.log|Enregistre les communications du client hérité d'appareil mobile avec un point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|dmpmsi.log|Enregistre les données Windows Installer pour la configuration d'un point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DMPSetup.log|Enregistre la configuration du point de gestion lorsqu'il est activé pour les appareils mobiles.|Serveur de système de site|  
|DmpSoftware.log|Enregistre des données de la distribution logicielle provenant de clients hérités d'appareils mobiles sur un point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DmpStatus.log|Enregistre les données de messages d'état à partir de clients d'appareils mobiles sur un point de gestion activé pour les appareils mobiles.|Serveur de système de site|  
|DmSvc.log|Enregistre les communications provenant de clients hérités d'appareils mobiles avec un point de gestion activé pour les appareils mobiles.|Client|  
|FspIsapi.log|Enregistre des détails concernant les communications au point d'état de secours à partir de clients hérités d'appareils mobiles et d'ordinateurs clients.|Serveur de système de site|  

###  <a name="BKMK_OSDLog"></a> Déploiement du système d’exploitation  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au déploiement du système d'exploitation.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|CAS.log|Enregistre des détails lorsque des points de distribution sont trouvés pour le contenu référencé.|Client|  
|ccmsetup.log|Enregistre les tâches ccmsetup liées au programme d’installation client, à la mise à niveau du client et à la suppression de client. Permet de dépanner des problèmes d'installation du client.|Client|  
|CreateTSMedia.log|Enregistre les détails sur la création de médias de séquence de tâches.|Ordinateur qui exécute la console Configuration Manager|  
|DeployToVhd.log|Enregistre les détails concernant le processus de création et de modification de disque dur virtuel.|Ordinateur qui exécute la console Configuration Manager|  
|Dism.log|Enregistre les actions d’installation de pilotes ou les actions d’application de mises à jour pour la maintenance hors connexion.|Serveur de système de site|  
|distmgr.log|Enregistre les détails concernant la configuration de l’activation d’un point de distribution pour PXE (Preboot Execution Environment).|Serveur de système de site|  
|DriverCatalog.log|Enregistre des détails concernant les pilotes de périphérique importés dans le catalogue de pilotes.|Serveur de système de site|  
|mcsisapi.log|Enregistre les informations pour les transferts de packages en multidiffusion et les réponses aux demandes des clients.|Serveur de système de site|  
|mcsexec.log|Enregistre les actions relatives au contrôle de l’intégrité, à l’espace de noms, à la création de sessions et à la vérification des certificats.|Serveur de système de site|  
|mcsmgr.log|Enregistre les modifications apportées à la configuration, au mode de sécurité et à la disponibilité.|Serveur de système de site|  
|mcsprv.log|Enregistre l'interaction du fournisseur de multidiffusion avec les services de déploiement Windows (WDS).|Serveur de système de site|  
|MCSSetup.log|Enregistre des détails concernant l'installation du rôle de serveur de multidiffusion.|Serveur de système de site|  
|MCSMSI.log|Enregistre des détails concernant l'installation du rôle de serveur de multidiffusion.|Serveur de système de site|  
|Mcsperf.log|Enregistre des détails concernant les mises à jour du compteur de performance de multidiffusion.|Serveur de système de site|  
|MP_ClientIDManager.log|Enregistre les réponses du point de gestion aux demandes d’ID client que les séquences de tâches lancent à partir de PXE ou du support de démarrage.|Serveur de système de site|  
|MP_DriverManager.log|Enregistre les réponses du point de gestion aux demandes d'actions de la séquence de tâches Appliquer automatiquement les pilotes.|Serveur de système de site|  
|OfflineServicingMgr.log|Enregistre les détails de la planification de la maintenance hors connexion et des actions d’application de mises à jour sur les fichiers WIM.|Serveur de système de site|  
|Setupact.log|Enregistre des détails sur Windows Sysprep et les journaux d'installation.|Client|  
|Setupapi.log|Enregistre des détails sur Windows Sysprep et les journaux d'installation.|Client|  
|Setuperr.log|Enregistre des détails sur Windows Sysprep et les journaux d'installation.|Client|  
|smpisapi.log|Enregistre des détails concernant les actions de capture de l'état du client et de restauration, et les informations de seuil.|Client|  
|Smpmgr.log|Enregistre des détails concernant les résultats des modifications de configuration et des vérifications de l'intégrité du point de migration de l'état.|Serveur de système de site|  
|smpmsi.log|Enregistre les détails d'installation et de configuration du point de migration d'état.|Serveur de système de site|  
|smpperf.log|Enregistre les mises à jour du compteur de performances du point de migration d'état.|Serveur de système de site|  
|smspxe.log|Enregistre les détails concernant les réponses aux clients qui effectuent un démarrage PXE et les détails concernant l’expansion d’images de démarrage et des fichiers de démarrage.|Serveur de système de site|  
|smssmpsetup.log|Enregistre les détails d'installation et de configuration du point de migration d'état.|Serveur de système de site|
| SMS_PhasedDeployment.log| Fichier journal pour les déploiements en plusieurs phases, une fonctionnalité en préversion à compter de Configuration Manager version 1802.|Site de niveau supérieur dans la hiérarchie Configuration Manager| 
|Smsts.log|Enregistre les activités de séquences de tâches.|Client|  
|TSAgent.log|Enregistre le résultat des dépendances des séquences de tâche avant de démarrer une séquence de tâches.|Client|  
|TaskSequenceProvider.log|Enregistre des détails concernant les séquences de tâches importées, exportées ou modifiées.|Serveur de système de site|  
|loadstate.log|Enregistre des détails concernant l'outil de migration de l'état utilisateur (USMT) et la restauration des données d'état de l'utilisateur.|Client|  
|scanstate.log|Enregistre des détails concernant l'outil de migration de l'état utilisateur (USMT) et la capture des données d'état de l'utilisateur.|Client|  

###  <a name="BKMK_PowerMgmtLog"></a> Gestion de l’alimentation  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations liées à la gestion de l'alimentation.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Enregistre les détails concernant les activités de gestion de l’alimentation sur l’ordinateur client, notamment la surveillance et l’application de paramètres par l’agent du client de gestion de l’alimentation.|Client|  

###  <a name="BKMK_RCLog"></a> Contrôle à distance  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au contrôle à distance.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Enregistre des détails concernant l'activité de l'observateur de contrôle à distance.|Sur l’ordinateur qui exécute l’observateur de contrôle à distance, dans le dossier %temp%.|  

###  <a name="BKMK_ReportLog"></a> Rapports  
 Le tableau suivant répertorie les fichiers journaux de Configuration Manager qui contiennent des informations relatives à la création de rapports.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Enregistre des informations sur l'activité et l'état du point de Reporting Services.|Serveur de système de site|  
|srsrpMSI.log|Enregistre les résultats détaillés du processus d'installation du point de Reporting Services à partir des données fournies par MSI.|Serveur de système de site|  
|srsrpsetup.log|Enregistre les résultats du processus d'installation du point de Reporting Services.|Serveur de système de site|  

###  <a name="BKMK_RBALog"></a> Administration basée sur des rôles  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à la gestion de l'administration basée sur des rôles.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|hman.log|Enregistre les informations concernant les modifications de la configuration du site et la publication d’informations du site sur les services de domaine Active Directory.|Serveur de site|  
|SMSProv.log|Enregistre les accès du fournisseur WMI à la base de données du site.|Ordinateur sur lequel le fournisseur SMS est installé|  

###  <a name="BKMK_WITLog"></a> Point de connexion de service  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au point de connexion de service.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Enregistre des informations concernant les certificats et le compte proxy.|Serveur de site|  
|Colleval.log|Enregistre des détails concernant la création, la modification et la suppression de regroupements par l'Évaluateur de regroupements.|Site principal et site d'administration centrale|  
|Cloudusersync.log|Enregistre l'activation des licences des utilisateurs.|Ordinateur avec le point de connexion de service|  
|dataldr.log|Enregistre des informations sur le traitement des fichiers MIF.|Serveur de site|  
|ddm.log|Enregistre les activités du gestionnaire de données de découverte.|Serveur de site|  
|distmgr.log|Enregistre des détails concernant les requêtes de distribution de contenu.|Serveur de site de niveau supérieur|  
|Dmpdownloader.log|Enregistre les détails concernant les téléchargements à partir de Microsoft Intune.|Ordinateur avec le point de connexion de service|  
|Dmpuploader.log|Enregistre les détails concernant le chargement des modifications de la base de données sur Microsoft Intune.|Ordinateur avec le point de connexion de service|  
|hman.log|Enregistre des informations concernant le transfert des messages.|Serveur de site|  
|objreplmgr.log|Enregistre le traitement des stratégies et des affectations.|Serveur de site principal|  
|Policypv.log|Enregistre la génération de stratégie de toutes les stratégies.|Serveur de site|  
|outgoingcontentmanager.log|Enregistre le contenu chargé vers Microsoft Intune.|Ordinateur avec le point de connexion de service|  
|sitecomp.log|Enregistre les détails de l’installation du point de connexion de service.|Serveur de site|  
|SmsAdminUI.log|Enregistre l’activité de la console Configuration Manager.|Ordinateur qui exécute la console Configuration Manager|  
|SMSProv.log|Enregistre les activités effectuées par le fournisseur SMS. Les activités de la console Configuration Manager utilisent le fournisseur SMS.|Ordinateur sur lequel le fournisseur SMS est installé|  
|SrvBoot.log|Enregistre les détails du service d’installation du point de connexion de service.|Ordinateur avec le point de connexion de service|  
|Statesys.log|Enregistre le traitement des messages de gestion d'appareil mobile.|Site principal et site d'administration centrale|  

###  <a name="BKMK_SU_NAPLog"></a> Mises à jour logicielles  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives aux mises à jour logicielles.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|Ccmperf.log|Enregistre les activités liées à la maintenance et la capture de données relatives aux compteurs de performances du client.|Client|  
|PatchDownloader.log|Enregistre des détails concernant le processus de téléchargement des mises à jour logicielles vers la destination de téléchargement, sur le serveur de site.|Ordinateur qui héberge la console Configuration Manager à partir de laquelle les téléchargements sont lancés|  
|PolicyEvaluator.log|Enregistre des détails concernant l'évaluation des stratégies sur les ordinateurs clients, dont les stratégies de mises à jour logicielles.|Client|  
|RebootCoordinator.log|Enregistre des détails concernant la coordination des redémarrages du système sur des ordinateurs clients après l'installation de mises à jour logicielles.|Client|  
|ScanAgent.log|Enregistre des détails concernant les demandes d'analyse pour les mises à jour logicielles, l'emplacement de WSUS et des actions connexes.|Client|  
|SdmAgent.log|Enregistre les détails concernant le suivi des corrections et de la conformité. Cependant, le fichier journal des mises à jour logicielles, Updateshandler.log, fournit plus d’informations sur l’installation des mises à jour logicielles nécessaires pour la conformité.<br /><br /> Ce fichier journal est partagé avec les paramètres de compatibilité.|Client|  
|ServiceWindowManager.log|Enregistre des détails concernant l'évaluation des fenêtres de maintenance.|Client|  
|SmsWusHandler.log|Enregistre des détails concernant le processus d'analyse pour l'outil d'inventaire de Microsoft Updates.|Client|  
|StateMessage.log|Enregistre les détails concernant les messages d’état des mises à jour logicielles qui sont créés et envoyés au point de gestion.|Client|  
|SUPSetup.log|Enregistre des détails concernant l'installation du point de mise à jour logicielle. Lorsque l'installation d'un point de mise à jour logicielle se termine, la mention **Installation was successful** est consignée dans ce fichier journal.|Serveur de système de site|  
|UpdatesDeployment.log|Enregistre des détails concernant les déploiements sur le client, y compris l'activation, l'évaluation et l'application des mises à jour logicielles. La journalisation documentée contient des informations supplémentaires sur l'interaction avec l'interface utilisateur du client.|Client|  
|UpdatesHandler.log|Enregistre des détails concernant l'analyse de la compatibilité des mises à jour logicielles, ainsi que le téléchargement et l'installation des mises à jour logicielles sur le client.|Client|  
|UpdatesStore.log|Enregistre des détails concernant l'état de compatibilité des mises à jour logicielles qui ont été évaluées au cours du cycle d'analyse de la compatibilité.|Client|  
|WCM.log|Enregistre les détails concernant la configuration du point de mise à jour logicielle et les connexions au serveur WSUS pour les catégories, les classifications et les langues des mises à jour avec abonnement.|Serveur de site|  
|WSUSCtrl.log|Enregistre des détails concernant la configuration, la connectivité de la base de données et l'intégrité du serveur WSUS du site.|Serveur de système de site|  
|wsyncmgr.log|Enregistre les détails concernant le processus de synchronisation des mises à jour logicielles.|Serveur de site|  
|WUAHandler.log|Enregistre des détails concernant l'agent Windows Update sur le client, lors de la recherche des mises à jour logicielles.|Client|  

###  <a name="BKMK_WOLLog"></a> Wake On LAN  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à l’utilisation de Wake On LAN.  

> [!NOTE]  
>  Quand vous complétez l’éveil par appel réseau (Wake On LAN) en utilisant le proxy de mise en éveil, cette activité est journalisée sur le client. Par exemple, consultez CcmExec.log et SleepAgent_<*domaine*\>@SYSTEM_0.log dans la section [Opérations du client](#BKMK_ClientOpLogs) de cet article.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Enregistre des détails concernant les clients auxquels des paquets de mise en éveil doivent être envoyés, le nombre de paquets de mise en éveil envoyés et le nombre de nouvelles tentatives.|Serveur de site|  
|wolmgr.log|Enregistre des détails concernant les procédures de mise en éveil, notamment le moment opportun pour déclencher le réveil des déploiements configurés pour Wake On LAN.|Serveur de site|  

###  <a name="BKMK_WindowsServicingLog"></a>Maintenance de Windows 10  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à la maintenance de Windows 10.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|Ccmperf.log|Enregistre les activités liées à la maintenance et la capture de données relatives aux compteurs de performances du client.|Client|  
|CcmRepair.log|Enregistre les activités de réparation de l'agent du client.|Client|
|PatchDownloader.log|Enregistre des détails concernant le processus de téléchargement des mises à jour logicielles vers la destination de téléchargement, sur le serveur de site.|Ordinateur qui héberge la console Configuration Manager à partir de laquelle les téléchargements sont lancés|  
|PolicyEvaluator.log|Enregistre des détails concernant l'évaluation des stratégies sur les ordinateurs clients, dont les stratégies de mises à jour logicielles.|Client|  
|RebootCoordinator.log|Enregistre des détails concernant la coordination des redémarrages du système sur des ordinateurs clients après l'installation de mises à jour logicielles.|Client|  
|ScanAgent.log|Enregistre des détails concernant les demandes d'analyse pour les mises à jour logicielles, l'emplacement de WSUS et des actions connexes.|Client|  
|SdmAgent.log|Enregistre les détails concernant le suivi des corrections et de la conformité. Cependant, le fichier journal des mises à jour logicielles, Updateshandler.log, fournit plus d’informations sur l’installation des mises à jour logicielles nécessaires pour la conformité.<br /><br /> Ce fichier journal est partagé avec les paramètres de compatibilité.|Client|  
|ServiceWindowManager.log|Enregistre des détails concernant l'évaluation des fenêtres de maintenance.|Client|  
|setupact.log|Fichier journal principal pour la plupart des erreurs qui se produisent pendant le processus d’installation de Windows. Le fichier journal se trouve dans le dossier %windir%\$Windows.~BT\sources\panther.|Client|
|SmsWusHandler.log|Enregistre des détails concernant le processus d'analyse pour l'outil d'inventaire de Microsoft Updates.|Client|  
|StateMessage.log|Enregistre des détails sur les messages d'état des mises à jour logicielles créés et envoyés au point de gestion.|Client|  
|SUPSetup.log|Enregistre des détails concernant l'installation du point de mise à jour logicielle. Lorsque l'installation d'un point de mise à jour logicielle se termine, la mention **Installation was successful** est consignée dans ce fichier journal.|Serveur de système de site|  
|UpdatesDeployment.log|Enregistre des détails concernant les déploiements sur le client, y compris l'activation, l'évaluation et l'application des mises à jour logicielles. La journalisation documentée contient des informations supplémentaires sur l'interaction avec l'interface utilisateur du client.|Client|  
|Updateshandler.log|Enregistre des détails concernant l'analyse de la compatibilité des mises à jour logicielles, ainsi que le téléchargement et l'installation des mises à jour logicielles sur le client.|Client|  
|UpdatesStore.log|Enregistre des détails concernant l'état de compatibilité des mises à jour logicielles qui ont été évaluées au cours du cycle d'analyse de la compatibilité.|Client|  
|WCM.log|Enregistre les détails concernant la configuration du point de mise à jour logicielle et les connexions au serveur WSUS pour les catégories, les classifications et les langues des mises à jour avec abonnement.|Serveur de site|  
|WSUSCtrl.log|Enregistre des détails concernant la configuration, la connectivité de la base de données et l'intégrité du serveur WSUS du site.|Serveur de système de site|  
|wsyncmgr.log|Enregistre les détails concernant le processus de synchronisation des mises à jour logicielles.|Serveur de site|  
|WUAHandler.log|Enregistre des détails concernant l'agent Windows Update sur le client, lors de la recherche des mises à jour logicielles.|Client|  

###  <a name="BKMK_WULog"></a> Agent Windows Update  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives à l'agent Windows Update.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Enregistre les détails concernant les connexions de l’agent Windows Update au serveur WSUS et la récupération des mises à jour logicielles pour l’évaluation de la conformité, et s’il existe des mises à jour pour les composants de l’agent.|Client|  

###  <a name="BKMK_WSUSLog"></a> Serveur WSUS  
 Le tableau suivant répertorie les fichiers journaux qui contiennent des informations relatives au serveur WSUS.  

|Nom du fichier journal|Description|Ordinateur sur lequel se trouve le fichier journal|  
|--------------|-----------------|----------------------------|  
|Change.log|Enregistre les détails concernant les informations de la base de données du serveur WSUS qui ont été modifiées.|Serveur WSUS|  
|SoftwareDistribution.log|Enregistre les détails concernant les mises à jour logicielles qui sont synchronisées depuis la source de mise à jour configurée vers la base de données du serveur WSUS.|Serveur WSUS|  
