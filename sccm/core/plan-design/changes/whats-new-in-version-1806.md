---
title: Nouveautés de la version 1806
titleSuffix: Configuration Manager
description: Obtenez des informations détaillées sur les changements et les nouvelles fonctionnalités introduits dans la version 1806 de l’édition Current Branch de Configuration Manager.
ms.date: 07/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0249dbd3-1e85-4d05-a9e5-420fbe44d850
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c6ae28a50f3145420895b295ebe730fb7b2a9a7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386060"
---
# <a name="whats-new-in-version-1806-of-configuration-manager-current-branch"></a>Nouveautés de la version 1806 de l’édition Current Branch de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1806 pour l’édition Current Branch de Configuration Manager est disponible sous forme de mise à jour dans la console. Appliquez cette mise à jour sur les sites qui exécutent la version 1706, 1710 ou 1802. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

> [!Important]  
> Cet article liste toutes les fonctionnalités importantes de cette version. Toutefois, toutes les sections ne sont pas encore liées au contenu mis à jour en fonction des informations supplémentaires sur les nouvelles fonctionnalités. Continuez à consulter régulièrement cette page sur les mises à jour. Les changements apportés sont indiqués à l’aide de l’étiquette ***[Mis à jour]***. Cette indication sera supprimée quand le contenu sera finalisé.  

<!--
Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4101375).
-->

<!--
The following additional updates to this release are also now available:
- [Update rollup for System Center Configuration Manager current branch, version 1806](https://support.microsoft.com/help/4057517)
-->


Les sections suivantes fournissent des détails sur les changements et les nouvelles fonctionnalités de la version 1806 de l’édition Current Branch de Configuration Manager.  



<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1806 drops support for the following products:
-->



## <a name="site-infrastructure"></a>Infrastructure de site

### <a name="cmpivot"></a>CMPivot
<!--1358456--> Configuration Manager met à disposition un grand magasin de données d’appareils centralisé, que les clients utilisent pour générer des rapports. Le site collecte généralement ces données chaque semaine. CMPivot est un nouvel utilitaire de console, qui permet désormais d’accéder à l’état en temps réel des appareils de votre environnement. Il exécute immédiatement une requête sur tous les appareils actuellement connectés du regroupement cible, et retourne les résultats. Vous pouvez ensuite filtrer et regrouper ces données dans l’outil. En fournissant les données en temps réel des clients en ligne, vous pouvez répondre plus rapidement aux questions métier, résoudre les problèmes et corriger les incidents de sécurité. 

Pour plus d’informations, consultez [CMPivot](/sccm/core/servers/manage/cmpivot).  


### <a name="site-server-high-availability"></a>Haute disponibilité du serveur de site
<!--1128774--> La haute disponibilité pour un rôle serveur de site principal autonome est une solution basée sur Configuration Manager, qui permet d’installer un serveur de site supplémentaire en mode passif. Le serveur de site en mode passif s’ajoute à votre serveur de site existant, qui est en mode actif. Un serveur de site en mode passif est disponible pour une utilisation immédiate, en cas de besoin. 

Pour plus d’informations, consultez les articles suivants : 
- [Haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability) 
- [Organigramme - Configurer un serveur de site en mode passif](/sccm/core/servers/deploy/configure/passive-site-server-flowchart)
- [Organigramme – Promouvoir le serveur de site (planifié)](/sccm/core/servers/deploy/configure/promote-site-server-flowchart)
- [Organigramme – Promouvoir le serveur de site (non planifié)](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart)


### <a name="improvements-to-management-insights"></a>Améliorations des insights de gestion
Cette version intègre les améliorations suivantes des insights de gestion :  

- Certains insights de gestion permettent désormais d’entreprendre une action. Cette action consiste à naviguer vers le nœud associé dans la console, ou à afficher une vue filtrée basée sur une requête.<!--1357930-->  

- Un nouveau groupe pour la maintenance proactive est disponible avec six nouvelles règles, qui permettent de mettre en évidence les problèmes de configuration potentiels à éviter via une maintenance régulière.<!--1352184-->  

Pour plus d’informations, consultez [Insights de gestion](/sccm/core/servers/manage/management-insights).


### <a name="configuration-manager-tools"></a>Outils de Configuration Manager
<!--1357145--> Les outils serveur et clients de Configuration Manager sont désormais inclus sur le serveur. Vous les trouverez dans le dossier `CD.Latest\SMSSETUP\Tools` du serveur de site. Aucune installation supplémentaire n’est requise. 

Pour plus d’informations, consultez [Outils de Configuration Manager](/sccm/core/support/tools).


### <a name="exclude-active-directory-containers-from-discovery"></a>Exclure les conteneurs Active Directory de la détection
<!--1358143--> Pour réduire le nombre d’objets découverts, excluez certains conteneurs spécifiques de la découverte de systèmes Active Directory. 



## <a name="content-management"></a>Gestion de contenu

### <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurer une bibliothèque de contenu à distance pour le serveur de site
<!--1357525--> Pour configurer la haute disponibilité du serveur de site, ou pour libérer de l’espace disque sur les serveurs de site d’administration centrale ou les serveurs de sites principaux, déplacez la bibliothèque de contenu vers un autre emplacement de stockage. Déplacez la bibliothèque de contenu vers un autre disque du serveur de site, vers un serveur distinct ou vers des disques à tolérance de panne d’un réseau SAN (réseau de zone de stockage). 

Pour plus d’informations, consultez les articles suivants : 
- [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library)
- [Organigramme – Gérer la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart)


### <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Prise en charge du point de distribution cloud pour Azure Resource Manager
<!--1322209--> Durant la création d’un point de distribution cloud, l’Assistant permet désormais de créer un déploiement **Azure Resource Manager**. Azure Resource Manager est une plateforme moderne qui permet de gérer toutes les ressources d’une solution en tant qu’entité unique, appelée groupe de ressources. Durant le déploiement d’un point de distribution cloud avec Azure Resource Manager, le site utilise Azure Active Directory pour authentifier et créer les ressources cloud nécessaires. Le certificat de gestion Azure classique n’est pas nécessaire pour ce déploiement modernisé. 

La documentation sur les fonctionnalités du point de distribution cloud a également été révisée et améliorée. Pour plus d’informations, consultez les articles suivants :
- [Utiliser un point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)   
- [Installer un point de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)  


### <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Prise en charge des points de distribution cloud comme source par les points de distribution d’extraction  
<!--1321554--> De nombreux clients utilisent des points de distribution d’extraction dans des bureaux distants ou des filiales pour télécharger du contenu à partir d’un point de distribution source sur le réseau WAN (réseau étendu). Si vos bureaux distants ont une meilleure connexion à Internet, ou si vous souhaitez réduire la charge de vos liaisons WAN, vous pouvez désormais utiliser un point de distribution cloud dans Microsoft Azure en tant que source. Quand vous ajoutez une source sous l’onglet **Point de distribution d’extraction** des propriétés de point de distribution, tout point de distribution cloud du site est maintenant répertorié comme point de distribution disponible. Le comportement des deux rôles système de site reste inchangé par ailleurs. 

Pour plus d’informations, consultez [Utiliser un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).


### <a name="enable-distribution-points-to-use-network-congestion-control"></a>Configurer les points de distribution pour utiliser le contrôle de surcharge du réseau
<!--1358112--> La fonctionnalité LEDBAT (Low Extra Delay Background Transport) de Windows Server permet de gérer les transferts réseau en arrière-plan. Pour les points de distribution qui s’exécutent sur des versions prises en charge de Windows Server, activez une option permettant d’ajuster le trafic réseau. Les clients utilisent uniquement la bande passante réseau lorsqu’elle est disponible. 

Pour plus d’informations, consultez [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat).


### <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Prise en charge du téléchargement partiel dans le cache d’homologue client pour réduire l’utilisation du réseau WAN
<!--1357346--> Les sources de cache d’homologue client peuvent désormais diviser le contenu en plusieurs parties. Ces parties diminuent le transfert de réseau afin de réduire l’utilisation du réseau WAN. Le point de gestion fournit un suivi plus détaillé des parties du contenu. Il essaie de supprimer plusieurs téléchargements du même contenu par groupe de limites. 

Pour plus d’informations, consultez [Prise en charge du téléchargement partiel](/sccm/core/plan-design/hierarchy/client-peer-cache#bkmk_parts). 


### <a name="boundary-group-options-for-peer-downloads"></a>Options de groupe de limites pour les téléchargements à partir de pairs
<!--1356193--> Les groupes de limites intègrent maintenant des paramètres supplémentaires qui offrent davantage de contrôle sur la distribution du contenu dans l’environnement. Cette version ajoute les options suivantes :  

- **Autoriser les téléchargements à partir de pairs dans ce groupe de limites** : ce paramètre est activé par défaut. Le point de gestion fournit aux clients une liste d’emplacements de contenu qui comprend des sources de pairs. Ce paramètre affecte également l’application des ID de groupes pour l’optimisation de la distribution.  

- **Lors des téléchargements à partir de pairs, utiliser seulement les pairs qui se trouvent dans le même sous-réseau** : ce paramètre dépend de celui qui est illustré ci-dessus. Lorsque cette option est activée, le point de gestion n’inclut dans la liste des emplacements de contenu que les sources de pairs qui se trouvent dans le même sous-réseau que le client.  



<!-- ## Migration  -->



## <a name="client-management"></a>Gestion des clients

### <a name="improvement-to-client-push-security"></a>Amélioration apportée à la sécurité d’envoi (push) du client
<!--1358204--> Durant l’utilisation de la méthode d’envoi (push) du client pour l’installation du client Configuration Manager, le site peut désormais imposer une authentification mutuelle Kerberos. Cette amélioration permet de sécuriser la communication entre le serveur et le client. 

Pour plus d’informations, consultez [Comment installer des clients selon la méthode d’installation Push du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


### <a name="bkmk_ehttp"></a> Système de site HTTP amélioré
<!--1356889,1358228--> L’utilisation de la communication HTTPS est recommandée pour tous les chemins de communication Configuration Manager, mais peut se révéler difficile pour certains clients en raison des frais liés à la gestion des certificats PKI. L’intégration à Azure Active Directory (Azure AD) permet d’éviter une partie de ces exigences de certificat. 

Cette version comprend des améliorations concernant la façon dont les clients communiquent avec les systèmes de site. Dans les propriétés du site, sous l’onglet **Communication de l’ordinateur client**, sélectionnez l’option **HTTPS ou HTTP**, puis activez la nouvelle option **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**. Il s’agit d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features).

Cette option prend en charge les scénarios principaux suivants :  

- **Du client au point de gestion HTTP**<!--1356889--> : les [appareils joints à Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) peuvent communiquer via une Passerelle de gestion cloud avec un point de gestion configuré pour le protocole HTTP. Le serveur de site génère un certificat pour le point de gestion afin de lui permettre de communiquer via un canal sécurisé.   

- **Du client au point de distribution HTTP**<!--1358228--> : un groupe de travail ou un client joint à Azure AD peut télécharger du contenu via un canal sécurisé à partir d’un point de distribution configuré pour le protocole HTTP.   


### <a name="azure-ad-device-identity"></a>Identité d’appareil Azure AD 
<!--1358460--> Un appareil [joint à Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) ou un [appareil Azure AD hybride](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) peut communiquer de manière sécurisée avec son site attribué, sans qu’un utilisateur Azure AD soit connecté. L’identité d’appareil cloud est désormais suffisante pour s’authentifier auprès du point de gestion et de la passerelle de gestion cloud.  


### <a name="cmtrace-installed-with-client"></a>CMTrace installé avec le client
<!--1357971--> Désormais, l’outil d’affichage des journaux CMTrace est automatiquement installé avec le client Configuration Manager. Il est ajouté au répertoire d’installation du client, qui est par défaut `%WinDir%\ccm\cmtrace.exe`. 

Pour plus d’informations, consultez [CMTrace](/sccm/core/support/cmtrace).


### <a name="cloud-management-dashboard"></a>Tableau de bord de gestion cloud
<!--1358461--> Le nouveau tableau de bord de gestion cloud fournit un affichage centralisé de l’utilisation de la Passerelle de gestion cloud. Lorsque le site est intégré à Azure AD, il affiche également les données sur les utilisateurs cloud et les appareils. Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**. Sélectionnez le nœud **Gestion cloud** et affichez les vignettes du tableau de bord.  

Cette fonctionnalité inclut également **l’analyseur de connexion de la passerelle de gestion cloud** pour la vérification en temps réel dans le cadre de la résolution des problèmes. L’utilitaire de la console vérifie l’état actuel du service, ainsi que le canal de communication qui passe par le point de connexion de la passerelle de gestion cloud vers les points de gestion qui autorisent le trafic de la passerelle. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Services cloud**, puis sélectionnez **Passerelle de gestion cloud**. Sélectionnez l’instance cible de la passerelle de gestion cloud, puis cliquez dans le ruban sur **Analyseur de connexion**.


### <a name="improvements-to-cloud-management-gateway"></a>Améliorations apportées à la passerelle de gestion cloud

La version 1806 comprend les améliorations suivantes pour la Passerelle de gestion cloud :

#### <a name="simplified-client-bootstrap-command-line"></a>Ligne de commande de démarrage du client simplifiée
<!--1358215--> Durant l’installation du client Configuration Manager sur Internet via une passerelle de gestion cloud, le nombre de propriétés nécessaires sur la ligne de commande est désormais réduit. Cette amélioration réduit la taille de la ligne de commande utilisée dans Microsoft Intune pour la préparation de la cogestion. 

Les propriétés de ligne de commande suivantes sont nécessaires pour tous les scénarios :
  - CCMHOSTNAME  
  - SMSSITECODE  

Les propriétés suivantes sont nécessaires lorsque vous utilisez Azure AD pour l’authentification client, au lieu de certificats d’authentification client PKI :
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

La propriété suivante est nécessaire si le client doit revenir à l’intranet :
  - SMSMP  

L’exemple suivant comprend toutes les propriétés mentionnées ci-dessus :   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

<!--For more information, see [Client installation properties](/sccm/core/clients/deploy/about-client-installation-properties).-->

#### <a name="download-content-from-a-cmg"></a>Télécharger du contenu à partir d’une passerelle de gestion cloud
<!--1358651--> Auparavant, vous deviez déployer un point de distribution cloud et une passerelle de gestion cloud sous forme de rôles distincts. À présent, une passerelle de gestion cloud peut également proposer du contenu aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure. Pour activer cette fonctionnalité, activez la nouvelle option **Allow CMG to function as a cloud distribution point and serve content from Azure storage** (Autoriser la passerelle de gestion cloud à fonctionner comme un point de distribution cloud et à distribuer du contenu à partir du stockage Azure) sous l’onglet **Paramètres** des propriétés de la passerelle de gestion cloud. 

#### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Les certificat racines approuvés ne sont plus nécessaires avec Azure AD
<!--503899-->Quand vous créez une passerelle de gestion cloud, vous n’êtes plus obligé de fournir un [certificat racine approuvé](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-trusted-root-certificate-to-clients) dans la page Paramètres. Ce certificat n’est pas nécessaire lorsque vous utilisez Azure Active Directory (Azure AD) pour l’authentification client, mais il était auparavant nécessaire dans l’Assistant. Si vous utilisez des certificats d’authentification client PKI, vous devez continuer d’ajouter un certificat racine approuvé pour la passerelle de gestion cloud.



## <a name="co-management"></a>Cogestion

### <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synchroniser la stratégie MDM de Microsoft Intune pour un appareil cogéré
<!--1357377--> Quand vous passez à une charge de travail en cogestion, les appareils cogérés se synchronisent automatiquement avec la stratégie MDM de Microsoft Intune. Cette synchronisation est effectuée lorsque vous lancez l’action **Télécharger la stratégie d’ordinateur** à partir de Notification du client, dans la console Configuration Manager. 

Pour plus d’informations, consultez [Basculer les charges de travail de Configuration Manager sur Intune](/sccm/core/clients/manage/co-management-switch-workloads).


### <a name="transition-new-workloads-to-intune-using-co-management"></a>Effectuer la transition de nouvelles charges de travail vers Intune à l’aide de la cogestion
Vous pouvez désormais effectuer la transition des charges de travail suivantes de Configuration Manager à Intune après avoir activé la cogestion :  

- **Configuration de l’appareil**<!--1357903--> : cette charge de travail vous permet d’utiliser Intune pour déployer des stratégies MDM, tout en continuant à utiliser Configuration Manager pour déployer des applications.  

- **Office 365**<!--1357841--> : les appareils n’installent pas les déploiements Office 365 à partir de Configuration Manager.  

- **Applications mobiles**<!--1357892--> : toutes les applications disponibles déployées à partir d’Intune sont disponibles sur le Portail d’entreprise. Les applications déployées à partir de Configuration Manager sont disponibles dans le centre logiciel. Il s’agit d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features).  

Pour effectuer la transition de ces charges de travail, accédez à la page de propriétés de cogestion, puis déplacez le curseur de charge de travail de Configuration Manager vers **Pilote** ou **Tout**. 

Pour plus d’informations, consultez [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview).


### <a name="support-for-multiple-hierarchies-to-one-intune-tenant"></a>Prise en charge de la consolidation de plusieurs hiérarchies en un seul locataire Intune
<!--1357944--> Certains clients ont plusieurs hiérarchies Configuration Manager qu’ils souhaitent consolider plus tard en tant que locataire unique pour Azure Active Directory et Microsoft Intune. La cogestion prend désormais en charge la connexion de plusieurs environnements Configuration Manager au même locataire Intune.

Pour plus d’informations, consultez [Préparer les appareils Windows 10 pour la cogestion](/sccm/core/clients/manage/co-management-prepare).
 


## <a name="compliance-settings"></a>Paramètres de conformité

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurer les paramètres Windows Defender SmartScreen pour Microsoft Edge
<!--1353701--> La stratégie de paramètres de conformité du navigateur Microsoft Edge ajoute les trois paramètres suivants pour Windows Defender SmartScreen : 
- Autoriser SmartScreen
- Les utilisateurs peuvent remplacer l’invite SmartScreen pour les sites
- Les utilisateurs peuvent remplacer l’invite SmartScreen pour les fichiers

Pour plus d’informations, consultez [Configurer les paramètres Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).


### <a name="scap-extensions"></a>Extensions SCAP
<!--1357552--> Convertissez le contenu SCAP (Security Content Automation Protocol) en bases de référence des paramètres de conformité, et générez des rapports SCAP à l’aide d’une extension de console. Cette fonctionnalité inclut également un nouveau tableau de bord pour visualiser la conformité du client, ainsi que la conformité aux règles XCCDF. 

Pour plus d’informations, consultez [À propos des extensions SCAP](/sccm/compliance/plan-design/scap/about-scap).



## <a name="application-management"></a>Gestion des applications

### <a name="phased-deployment-of-applications"></a>Déploiement d’applications par phases
<!--1358147--> Créez un déploiement par phases pour une application. Ils permettent d’orchestrer un lancement coordonné et séquencé de logiciels en fonction de groupes et de critères personnalisables. Par exemple, déployez l’application sur un regroupement pilote, puis poursuivez automatiquement le lancement en fonction des critères de réussite. 

Pour plus d’informations, consultez les articles suivants :  

- [Créer un déploiement par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gérer et effectuer le monitoring des déploiements par phases](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  


### <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Provisionner les packages d’application Windows pour tous les utilisateurs sur un appareil
<!--1358310--> Provisionnez une application avec un package d’application Windows pour tous les utilisateurs de l’appareil. Un exemple courant de ce scénario est le provisionnement d’une application telle que « Minecraft : Education Edition » à partir de Microsoft Store pour Entreprises et Éducation, pour tous les appareils utilisés par les élèves d’une école. Auparavant, Configuration Manager ne prenait en charge l’installation de ces applications que pour un seul utilisateur. Quand il se connectait à un nouvel appareil, l’élève devait attendre pour accéder à une application. À présent que l’application est provisionnée pour tous les utilisateurs d’un appareil, ceux-ci peuvent l’utiliser plus rapidement. 

Pour plus d’informations, consultez [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).


### <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Intégration de l’Outil de personnalisation Office au programme d’installation d’Office 365
<!--1358149--> L’Outil de personnalisation Office est désormais intégré au programme d’installation d’Office 365 dans la console Configuration Manager. Quand vous créez un déploiement pour Office 365, configurez dynamiquement les derniers paramètres de gestion Office. Microsoft met à jour l’Outil de personnalisation Office à chaque sortie de nouvelles builds d’Office 365. Cette intégration vous permet de tirer parti des nouveaux paramètres de gestion d’Office 365 dès qu’ils sont disponibles. 

Pour plus d’informations, consultez [Déployer des applications Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).


### <a name="support-for-new-windows-app-package-formats"></a>Prise en charge de nouveaux formats de package d’application Windows
<!--1357427--> Configuration Manager prend maintenant en charge le déploiement de nouveaux formats de package d’application Windows 10 (.msix) et d’ensemble d'applications (.msixbundle). 

Pour plus d’informations, consultez [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_general).


### <a name="uninstall-application-on-approval-revocation"></a>Désinstaller une application en cas de révocation de l’approbation
<!--1357891--> Le comportement a changé quand vous révoquez l’approbation d’une application. Maintenant, lorsque vous refusez la requête visant l’application, le client désinstalle l’application sur l’appareil de l’utilisateur. Ce comportement nécessite l’activation de la [fonctionnalité facultative](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approuver les demandes d’application pour les utilisateurs appareil par appareil**. 

Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications#bkmk_approval).


### <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861--> Package Conversion Manager est désormais un outil intégré qui vous permet de convertir les packages Configuration Manager 2007 hérités en applications de l’édition Current Branch de Configuration Manager. Ensuite, vous pouvez utiliser les fonctionnalités des applications telles que les dépendances, les règles de spécification et l’affinité entre utilisateur et appareil.

Commencez par les actions suivantes à partir du nœud **Packages** de la console Configuration Manager :  

   - **Analyser le package** : démarre le processus de conversion en analysant le package.  

   - **Convertir le package** : cette action permet de convertir facilement certains packages en applications.  

   - **Corriger et convertir** : certains packages nécessitent que les problèmes soient résolus avant leur conversion en applications.  

Accédez ensuite au tableau de bord **État de la conversion de package** dans l’espace de travail **Analyse**. Ce nouveau tableau de bord montre l’analyse globale, ainsi que l’état de conversion des packages du site. Il s’agit d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features).



## <a name="os-deployment"></a>Déploiement de système d’exploitation

### <a name="improvements-to-phased-deployments"></a>Améliorations apportées aux déploiements par phases

Cette version intègre les améliorations suivantes pour les déploiements par phases :  

#### <a name="create-a-phased-deployment-with-manually-configured-phases"></a>Créer un déploiement par phases avec des phases configurées manuellement
<!--1358148--> Pour une séquence de tâches, configurez manuellement les phases quand vous créez un déploiement par phases. Ajoutez jusqu’à 10 phases supplémentaires sous l’onglet **Phases** de l’Assistant Création d’un déploiement par phases. Vous pouvez toujours créer automatiquement un déploiement à deux phases par défaut. 

Pour plus d’informations, consultez [Créer un déploiement par phases avec des phases configurées manuellement](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_manual).

#### <a name="phased-deployment-status"></a>État du déploiement par phases
<!--1358577--> Les déploiements par phases ont maintenant une expérience de monitoring native. Dans le nœud **Déploiements** de l’espace de travail **Monitoring**, sélectionnez un déploiement par phases, puis cliquez sur **État du déploiement par phases** dans le ruban. 

Pour plus d’informations, consultez [Gérer et effectuer le monitoring des déploiements par phases](/sccm/osd/deploy-use/manage-monitor-phased-deployments).  

#### <a name="gradual-rollout-during-phased-deployments"></a>Lancement graduel durant les déploiements par phases
<!--1358578--> Lors d’un déploiement par phases, le lancement peut maintenant se produire progressivement dans chaque phase. Ce comportement limite les risques de problèmes de déploiement et diminue la charge sur le réseau causée par la distribution de contenu auprès des clients. Le site peut rendre le logiciel disponible progressivement en fonction de la configuration de chaque phase. Tous les clients d’une phase donnée ont une échéance qui dépend du moment de la mise à disposition du logiciel. La fenêtre entre la mise à disposition et l’échéance est la même pour tous les clients d’une phase. 

Pour plus d’informations, consultez [Paramètres de phase](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence#bkmk_settings).  


### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10
<!--1358500--> Le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend désormais un nouveau groupe, ainsi que des actions qu’il est recommandé d’ajouter en cas d’échec du processus de mise à niveau. Ces actions facilitent la résolution des problèmes. Un exemple est l’outil Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Il s’agit d’un outil de diagnostic autonome qui vous permet d’obtenir des informations détaillées sur la raison de l’échec d’une mise à niveau Windows 10. 

Pour plus d’informations, consultez [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-on-failure).


### <a name="improvements-to-pxe-enabled-distribution-points"></a>Améliorations apportées aux points de distribution compatibles PXE
<!--1357580--> Sous l’onglet **PXE** des propriétés des points de distribution, cochez **Activer un répondeur PXE sans les Services de déploiement Windows**. Cette nouvelle option active un répondeur PXE sur le point de distribution, qui n’a pas besoin des services WDS (Services de déploiement Windows). Les services WDS n’étant pas obligatoires, le point de distribution PXE peut être un système d’exploitation client ou serveur, notamment Windows Server Core. Ce nouveau service de répondeur PXE prend en charge le protocole IPv6 et améliore également la flexibilité des points de distribution PXE dans les bureaux distants. 

Pour plus d’informations, consultez les détails relatifs à l’[activation de PXE sur le point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


### <a name="network-access-account-not-required-for-some-scenarios"></a>Compte d’accès réseau non obligatoire pour certains scénarios
<!--1358278,1358279--> La fonctionnalité [Système de site HTTP amélioré](#bkmk_ehttp) supprime également certaines dépendances du compte d’accès réseau. Lorsque vous activez la nouvelle option de site **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**, les scénarios suivants ne nécessitent pas de compte d’accès réseau pour télécharger le contenu à partir d’un point de distribution :  

- Séquences de tâches exécutées à partir d’un support de démarrage ou d’un environnement PXE
- Séquence de tâches exécutées à partir du Centre logiciel  

Ces séquences de tâches conviennent aux déploiements de système d’exploitation et aux déploiements personnalisés. Elles sont également prises en charge par les ordinateurs de groupe de travail.


### <a name="other-improvements-to-os-deployment"></a>Autres améliorations apportées au déploiement du système d’exploitation

#### <a name="mask-sensitive-data-stored-in-task-sequence-variables"></a>Masquer les données sensibles stockées dans les variables de séquence de tâches
<!--1358330--> À l’étape [Définir la variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable), sélectionnez la nouvelle option **Ne pas afficher cette valeur**. Par exemple, quand vous spécifiez un mot de passe. 

#### <a name="mask-program-name-during-run-command-step-of-a-task-sequence"></a>Masquer le nom du programme durant l’étape Exécuter la commande d’une séquence de tâches
<!--1358493--> Pour empêcher l’affichage ou la journalisation de données potentiellement sensibles, affectez à la variable de la séquence de tâches **OSDDoNotLogCommand** la valeur `TRUE`. Cette variable masque le nom du programme dans le fichier smsts.log au cours de l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) d’une séquence de tâches.   

#### <a name="task-sequence-variable-for-dism-parameters-when-installing-drivers"></a>Variable de séquence de tâches pour les paramètres DISM durant l’installation de pilotes
<!--516679--> Pour spécifier des paramètres de ligne de commande supplémentaires pour DISM, utilisez la nouvelle variable de séquence de tâches **OSDInstallDriversAdditionalOptions**. Activez le paramètre d’étape [Appliquer le package de pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) pour **Installer le package de pilotes en exécutant DISM avec l’option recurse**. 

#### <a name="option-to-use-full-disk-encryption"></a>Option d’utilisation du chiffrement de disque complet
<!--SCCMDocs-pr issue 2671--> Les étapes [Activer BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_EnableBitLocker) et [Préconfigurer BitLocker](/sccm/osd/understand/task-sequence-steps#BKMK_PreProvisionBitLocker) incluent désormais une option pour **Utiliser le chiffrement de disque complet**. Par défaut, ces étapes permettent de chiffrer l’espace utilisé sur le lecteur. Ce comportement par défaut est recommandé, car il est plus rapide et plus efficace. Si votre organisation doit chiffrer l’intégralité du lecteur durant l’installation, activez cette option. Le programme d’installation de Windows attend que le lecteur entier soit chiffré, ce qui prend beaucoup de temps, en particulier sur les grands lecteurs. 



## <a name="software-center"></a>Centre logiciel

### <a name="software-center-infrastructure-improvements"></a>Améliorations apportées à l’infrastructure du Centre logiciel
<!--1358309--> Les rôles du catalogue d’applications ne sont plus nécessaires pour afficher les applications accessibles aux utilisateurs dans le Centre logiciel. Cette modification permet d’alléger l’infrastructure de serveur nécessaire pour fournir des applications aux utilisateurs. Le Centre logiciel s’appuie désormais sur le point de gestion pour obtenir ces informations, ce qui permet une meilleure mise à l’échelle des grands environnements par l’attribution de [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

> [!Note]  
> Les rôles de point du site web et de point de service web du catalogue des applications ne sont plus *obligatoires* dans la version 1806. Toutefois, ils sont toujours *pris en charge*. 
> 
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Spécifier la visibilité du lien du site web du catalogue des applications dans le Centre logiciel
<!--1358214--> Utilisez les paramètres du client pour vérifier si le lien permettant d’**Ouvrir le site web du catalogue des applications** apparaît dans le nœud **État d’installation** du Centre logiciel.  

Pour plus d’informations, consultez [Paramètres clients du Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center).

> [!Note]  
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  


### <a name="custom-tab-for-webpage-in-software-center"></a>Onglet personnalisé pour une page web du Centre logiciel
<!--1358132--> Utilisez les paramètres clients pour créer un onglet personnalisé afin d’ouvrir une page web dans le Centre logiciel. Cette fonctionnalité vous permet d’afficher du contenu à vos utilisateurs finaux d’une façon cohérente et fiable. La liste suivante comprend quelques exemples :  

- Contacter le service informatique : informations sur la façon de contacter le service informatique de votre organisation  

- Centre de support informatique : actions informatiques en libre-service telles que la recherche dans une base de connaissances ou l’ouverture d’un ticket de support.  

- Documentation pour les utilisateurs finaux : articles destinés aux utilisateurs de votre organisation sur différents sujets informatiques comme l’utilisation d’applications ou la mise à niveau vers Windows 10.  

Pour plus d’informations, consultez [Paramètres clients du Centre logiciel](/sccm/core/clients/deploy/about-client-settings#software-center) et le [Guide de l’utilisateur du Centre logiciel](/sccm/core/understand/software-center).


### <a name="maintenance-windows-in-software-center"></a>Fenêtres de maintenance dans le Centre logiciel
<!--1358131--> Le Centre logiciel affiche désormais la prochaine fenêtre de maintenance planifiée. Sous l’onglet État de l’installation, passez de la vue Tous à la vue À venir. Elle affiche la période et la liste des déploiements qui sont planifiés. S’il n’existe aucune fenêtre de maintenance future, la liste est vide. 

Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows) et le [Guide de l’utilisateur du Centre logiciel](/sccm/core/understand/software-center).



## <a name="software-updates"></a>Mises à jour logicielles

### <a name="third-party-software-updates"></a>Mises à jour de logiciels tiers
<!--1357605, 1352101, 1358714--> Les mises à jour de logiciels tiers vous permettent de vous abonner aux catalogues partenaires de la console Configuration Manager et de publier les mises à jour vers WSUS. Vous pouvez ensuite déployer ces mises à jour à l’aide du processus de gestion des mises à jour logicielles existant. 

Pour plus d’informations, consultez [Activer les mises à jour tierces](/sccm/sum/deploy-use/third-party-software-updates).


### <a name="deploy-software-updates-without-content"></a>Déployer des mises à jour logicielles sans contenu
<!--1357933--> Déployez les mises à jour logicielles sur les appareils sans télécharger et distribuer au préalable le contenu aux points de distribution. Cette fonctionnalité est utile lorsque le contenu des mises à jour est très volumineux, ou si vous souhaitez que les clients obtiennent toujours le contenu via le service cloud Microsoft Update. Dans ce cas, les clients peuvent également télécharger le contenu auprès d’homologues qui disposent déjà du contenu nécessaire. Le client Configuration Manager continue de gérer le téléchargement de contenu. Vous pouvez donc utiliser la fonctionnalité de cache d’homologue Configuration Manager ou d’autres technologies telles que l’optimisation de la distribution. Cette fonctionnalité prend en charge tous les types de mises à jour pris en charge par la gestion des mises à jour logicielles Configuration Manager, y compris les mises à jour Windows et Office. 

Pour plus d’informations, consultez l’option **Aucun package de déploiement** quand vous [déployez manuellement les mises à jour logicielles](/sccm/sum/deploy-use/manually-deploy-software-updates) ou [déployez automatiquement les mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrer les règles de déploiement automatique par architecture de mise à jour logicielle
 <!--1322266--> Vous pouvez désormais filtrer les règles de déploiement automatique pour exclure les architectures telles qu’Itanium et ARM64. Dans la page **Mises à jour logicielles** de l’Assistant Création d’une règle de déploiement automatique, le filtre de propriétés **Architecture** est désormais disponible. 

Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).


### <a name="improved-wsus-maintenance"></a>Améliorations apportées à la maintenance de WSUS 
<!--1357898--> L’Assistant Nettoyage de WSUS refuse désormais les mises à jour qui sont arrivées à expiration, conformément aux règles de remplacement définies dans les propriétés du composant du point de mise à jour logicielle. 

Pour plus d’informations, consultez [Maintenance des mises à jour logicielles](/sccm/sum/deploy-use/software-updates-maintenance).



## <a name="reporting"></a>Rapports

### <a name="new-software-updates-compliance-report"></a>Nouveau rapport sur la conformité des mises à jour logicielles
<!--1357775--> L’affichage des rapports de conformité des mises à jour logicielles comporte généralement des données provenant de clients qui n’ont pas contacté le site récemment. Un nouveau rapport, **Conformité 9 - Intégrité et conformité d’ensemble**, vous permet de filtrer les résultats de conformité d’un groupe de mises à jour logicielles spécifique en fonction des clients dont l’intégrité est « saine ». Ce rapport affiche l’état de conformité plus réaliste des clients actifs de votre environnement. 

Pour plus d’informations, consultez [Rapports des mises à jour logicielles](/sccm/sum/deploy-use/monitor-software-updates#BKMK_SUReports).



## <a name="inventory"></a>Inventaire

### <a name="bkmk_bigint"></a> Améliorations apportées à l’inventaire matériel pour les valeurs d’entiers longs
<!--1357880--> Auparavant, l’inventaire matériel était limité aux entiers supérieurs à 4 294 967 296 (2^32). Cette limite pouvait être atteinte pour les attributs tels que les tailles de disque dur en octets. Dans la mesure où le point de gestion ne traitait pas les valeurs entières supérieures à cette limite, aucune valeur n’était stockée dans la base de données. La nouvelle version prend désormais en charge les entiers de longueur 18 446 744 073 709 551 616 (2^64). 

Pour plus d’informations, consultez [Utilisation de valeurs entières longues](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory#bkmk_bigint).


### <a name="hardware-inventory-default-unit-revision"></a>Révision de l’unité par défaut pour l’inventaire matériel
<!--514442--> Dans [Configuration Manager version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), l’unité par défaut utilisée dans de nombreuses vues Rapports est passée des mégaoctets (Mo) aux gigaoctets (Go). En raison des [améliorations apportées à l’inventaire matériel au niveau des valeurs d’entiers longs](#bkmk_bigint), et en vue de répondre à la demande des utilisateurs, nous sommes repassé aux mégaoctets pour l’unité par défaut.



<!-- ## Mobile device management -->



<!-- ## Protect devices-->




## <a name="configuration-manager-console"></a>Console Configuration Manager

### <a name="product-lifecycle-dashboard"></a>Tableau de bord Cycle de vie du produit
<!--1319632--> Le tableau de bord de cycle de vie des produits affiche l’état de la stratégie de cycle de vie des produits Microsoft installés sur les appareils gérés avec Configuration Manager. Il vous fournit également des informations sur les produits Microsoft de votre environnement, leur état de prise en charge et leur date de fin de support. Utilisez le tableau de bord pour comprendre la disponibilité du support de chaque produit. Ces informations vous aident à planifier la date de la mise à jour des produits Microsoft utilisés, avant la fin du support.   

Pour plus d’informations, consultez [Tableau de bord Cycle de vie du produit](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="copy-asset-details-from-monitoring-views"></a>Copier les détails du bien à partir des affichages d’analyse
<!--1357856--> Les domaines suivants de l’espace de travail **Analyse** prennent désormais en charge la copie de texte :  

- Dans le nœud **Déploiements**, sélectionnez un déploiement, puis cliquez sur **Afficher l’état**. Dans le volet **Détails du bien** de l’affichage État du déploiement, sélectionnez un ou plusieurs appareils.  

- Développez le nœud **État de distribution**, puis sélectionnez **État du contenu**. Sélectionnez un logiciel, puis cliquez sur **Afficher l’état**. Dans le volet **Détails du bien** de l’affichage État du contenu, sélectionnez un ou plusieurs points de distribution. 

Cliquez avec le bouton droit sur le bien, puis sélectionnez **Copier**. Cette action permet de copier les biens sélectionnés sous forme d’une liste de valeurs délimitées par des virgules, qui inclut tous les détails. Le raccourci clavier **CTRL** + **C** fonctionne également dans ces affichages. 

Pour plus d’informations, consultez [Améliorations apportées à la console dans la version 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806).


### <a name="improvements-to-the-surface-dashboard"></a>Améliorations apportées au tableau de bord Surface
<!--1358654--> Cette version intègre les améliorations suivantes du tableau de bord Surface :  

- Le tableau de bord Surface affiche désormais une liste des appareils appropriés quand vous sélectionnez des sections de graphe spécifiques :  

   - En cliquant sur la vignette **Pourcentage d’appareils Surface**, vous affichez la liste des appareils Surface.  

   - En cliquant sur une barre de la vignette **Top cinq des versions de microprogramme**, vous affichez la liste des appareils Surface avec la version de leur microprogramme.  

- Quand vous affichez ces listes d’appareils dans le tableau de bord Surface, cliquez avec le bouton droit de la souris sur un appareil pour effectuer des actions courantes.  

Pour plus d’informations, consultez [Tableau de bord Surface](/sccm/core/clients/manage/surface-device-dashboard).


### <a name="view-the-currently-signed-on-user-for-a-device"></a>Afficher l’utilisateur connecté à un appareil
<!--1358202--> Désormais, par défaut, le nœud **Appareils** de l’espace de travail **Ressources et Conformité** affiche une colonne indiquant l’**utilisateur connecté**. Elle s’affiche également pour toutes les listes d’appareils spécifiques à un regroupement. Cette valeur est synchronisée avec [l’état du client](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). Quand l’utilisateur se déconnecte, le client efface cette valeur. Si aucun utilisateur n’est connecté, la valeur est vide. 

Pour plus d’informations, consultez [Améliorations apportées à la console dans la version 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806).


### <a name="submit-feedback-from-the-configuration-manager-console"></a>Envoyer des commentaires à partir de la console Configuration Manager  
<!--1357542-->

Envoyer un sourire ! Vous pouvez maintenant communiquer directement avec l’équipe Configuration Manager sur vos expériences. L’envoi de commentaires est facile à partir de la console Configuration Manager. Nous voulons recevoir tous vos commentaires : les éloges, les problèmes et les suggestions. Dans la console Configuration Manager, cliquez sur le bouton en forme de sourire dans l’angle supérieur droit au-dessus du ruban. Ces commentaires sont envoyés directement à l’équipe produit Microsoft pour Configuration Manager. Bien que l’utilisation du concentrateur de commentaires de Windows 10 soit toujours prise en charge, nous vous encourageons à utiliser la fonction de commentaires dans la console.  

Pour plus d’informations, consultez [Améliorations apportées à la console dans la version 1806](/sccm/core/servers/manage/admin-console#console-improvements-in-version-1806) et [Commentaires sur le produit](/sccm/core/understand/find-help#BKMK_1806Feedback).



## <a name="next-steps"></a>Étapes suivantes

Quand vous êtes prêt à installer cette version, consultez [Installation des mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).

> [!TIP]  
> Pour installer un nouveau site, utilisez une version de base de référence de Configuration Manager.  
>
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Pour plus d’informations sur les problèmes importants et connus, consultez les [Notes de publication](/sccm/core/servers/deploy/install/release-notes).
