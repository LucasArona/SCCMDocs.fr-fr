---
title: Nouveautés de la version 1810
titleSuffix: Configuration Manager
description: Obtenez des informations détaillées sur les changements et les nouvelles fonctionnalités introduits dans la version 1810 de l’édition Current Branch de Configuration Manager.
ms.date: 12/20/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 60d1c93acc2fcc2c04d09cd8f0ec0c083089a8ec
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250593"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Nouveautés de la version 1810 de l’édition Current Branch de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1810 pour l’édition Current Branch de Configuration Manager est disponible sous forme de mise à jour dans la console. Appliquez cette mise à jour sur les sites qui exécutent la version 1710, 1802 ou 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Référez-vous toujours à la dernière liste de contrôle pour installer cette mise à jour. Pour plus d’informations, consultez [Liste de contrôle pour installer la mise à jour 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810). Après avoir mis à jour un site, consultez également la [Liste de contrôle post-mise à jour](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

> [!Note]  
> Cet article liste toutes les fonctionnalités importantes de cette version. Toutefois, toutes les sections ne sont pas encore liées au contenu mis à jour en fonction des informations supplémentaires sur les nouvelles fonctionnalités. Continuez à consulter régulièrement cette page sur les mises à jour. Les changements apportés sont indiqués à l’aide de l’étiquette ***[Mis à jour]***. Cette indication sera supprimée quand le contenu sera finalisé.  

En plus des nouvelles fonctionnalités, cette version inclut également des modifications supplémentaires comme des corrections de bogues. Pour plus d’informations, consultez [Récapitulatif des changements dans Configuration Manager Current Branch, version 1810](https://support.microsoft.com/help/4482169).

<!--
For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell 1810 Release Notes](https://docs.microsoft.com/powershell/sccm/1810_release_notes?view=sccm-ps).

The following additional updates to this release are also now available:
- [Update rollup for Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4462978)
-->

> [!Important]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités apparaissent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version des clients n’est pas également la plus récente.

Cet article récapitule les changements et les nouvelles fonctionnalités de Configuration Manager version 1810.  



## <a name="bkmk_deprecated"></a> Fonctionnalités et systèmes d’exploitation dépréciés

Découvrez-en plus sur les changements de prise en charge avant leur implémentation dans [Éléments supprimés et dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

À compter du 14 août 2018, la fonctionnalité de gestion des appareils mobiles hybrides est dépréciée. Pour plus d’informations, voir [Présentation de la gestion MDM hybride](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

Le support de System Center Endpoint Protection (SCEP) pour Mac et Linux (toutes les versions) prend fin le 31 décembre 2018. La disponibilité de nouvelles définitions de virus pour SCEP pour Mac et SCEP pour Linux sera peut-être supprimée une fois que le support aura pris fin. Pour plus d’informations, consultez le [billet de blog sur la fin du support](https://go.microsoft.com/fwlink/?linkid=870182).

Les déploiements de services classiques dans Azure sont désormais dépréciés dans Configuration Manager. Commencez par utiliser des déploiements Azure Resource Manager pour la passerelle de gestion cloud et le point de distribution cloud. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).
<!--
Version 1810 drops support for the following products:
-->



## Infrastructure de site <a name="bkmk_infra"></a>

### <a name="support-for-windows-server-2019"></a>Prise en charge de Windows Server 2019
<!--1359195--> Configuration Manager prend désormais en charge Windows Server 2019 et Windows Server version 1809 comme systèmes de site. 

Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Prise en charge de la hiérarchie pour la haute disponibilité du serveur de site
<!--1358224--> Les sites d’administration centrale et les sites principaux enfants peuvent désormais avoir un serveur de site supplémentaire en mode passif. 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### <a name="improvements-to-setup-prerequisites"></a>Améliorations apportées aux prérequis de l’installation

Désormais, quand vous installez la version 1810 ou effectuez une mise à jour vers celle-ci, le programme d’installation de Configuration Manager contient ou améliore les vérifications des prérequis suivants :

- **Redémarrage du système en attente** : La vérification de ce prérequis est maintenant plus résiliente. Elle vérifie des clés de Registre supplémentaires pour les fonctionnalités de Windows. Pour plus d’informations, consultez [Redémarrage du système en attente](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Nettoyage du suivi des modifications SQL** : Cette fonctionnalité vérifie si la base de données du site a un backlog des données de suivi des modifications SQL. Pour plus d’informations, notamment une procédure pour vérifier et effacer ce backlog, consultez [Nettoyage du suivi des modifications SQL](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking). <!--SCCMDocs-pr issue 3023-->  

- **Version de SQL Native Client** : La vérification de ce prérequis est mise à jour pour les versions de SQL Native Client qui prennent en charge TLS 1.2. La version minimale est [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Pour plus d’informations, consultez la section [Version de SQL Native Client](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Système de site sur un nœud de cluster Windows** : Le processus d’installation de Configuration Manager ne bloque plus l’installation du rôle serveur de site sur un ordinateur ayant le rôle Windows pour le clustering de basculement. SQL Always On exige ce rôle, ce qui vous empêchait de colocaliser la base de données de site sur le serveur de site. Avec ce changement, vous pouvez créer un site à haut niveau de disponibilité avec moins de serveurs en utilisant SQL Always On et un serveur de site en mode passif. Pour plus d’informations, consultez [Cluster de basculement Windows](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster). <!--1359132-->  




### <a name="new-permission-for-client-notification-actions"></a>Nouvelle autorisation pour les actions de notification du client
<!--SCCMDocs-pr issue #2972--> Les actions de notification du client nécessitent l’autorisation **Notifier la ressource** sur la classe SMS_Collection. Les rôles intégrés suivants disposent de cette autorisation par défaut :
- Administrateur complet  
- Administrateur d'infrastructure  

Ajoutez cette autorisation aux rôles personnalisés qui doivent utiliser des actions de notification du client. 

Pour plus d’informations, consultez [Notifications du client](/sccm/core/clients/manage/client-notification).



## <a name="bkmk_content"></a> Gestion de contenu

### <a name="new-boundary-group-options"></a>Nouvelles options de groupe de limites
<!--1358749--> Les groupes de limites intègrent désormais les paramètres supplémentaires suivants qui offrent davantage de contrôle pour la distribution de contenu dans un environnement :

- **Préférer les points de distribution aux pairs au sein du même sous-réseau** : Par défaut, le point de gestion classe par ordre de priorité les sources de cache d’homologue au début de la liste des emplacements de contenu. Ce paramètre inverse cette priorité pour les clients qui se trouvent dans le même sous-réseau que la source de cache d’homologue.  

- **Préférer les points de distribution cloud aux points de distribution** : Si vous avez une succursale qui utilise un lien Internet plus rapide, vous pouvez désormais classer le contenu cloud par ordre de priorité.  

Pour plus d’informations, voir [Options de groupe de limites pour les téléchargements de pairs](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Règle Insights de gestion pour la version cliente de la source de cache d’homologue
<!-- 1358008 --> Le nœud **Insights de gestion** a une nouvelle règle pour identifier les clients qui servent de source de cache d’homologue mais qui n’ont pas été mis à niveau depuis une version cliente antérieure à 1806. La nouvelle règle est **Mettre à niveau les sources de cache de pair avec la dernière version du client Configuration Manager**, et fait partie du nouveau groupe de règles **Maintenance proactive**. Les clients antérieurs à 1806 ne peuvent pas être utilisés en tant que source de cache d’homologue pour les clients qui exécutent la version 1806 ou une version ultérieure. Sélectionnez **Prendre des mesures** pour ouvrir une vue d’appareil qui affiche la liste des clients. 

Pour plus d’informations, consultez [Insights de gestion](/sccm/core/servers/manage/management-insights).



## <a name="bkmk_client"></a> Gestion des clients

### <a name="new-client-notification-action-to-wake-up-device"></a>Nouvelle action de notification du client pour sortir un appareil du mode veille
<!--1317364--> Vous pouvez désormais sortir un client du mode veille à partir de la console Configuration Manager, même si le client ne se trouve pas sur le même sous-réseau que le serveur de site. Si vous avez besoin de procéder à une maintenance ou d’interroger des appareils, vous n’êtes pas limité par les clients distants qui sont en veille. Le serveur de site emprunte le canal de notification des clients pour identifier un autre client éveillé sur le même sous-réseau distant. Le client éveillé envoie alors une requête Wake On LAN (paquet magique).

### <a name="new-option-to-perform-client-notification-from-devices-node"></a>Nouvelle option pour effectuer la notification du client à partir du nœud Appareils
<!--1317364--> Jusqu’à la version 1810, l’option **Notification du client** était uniquement disponible à partir du nœud Regroupement d’appareils ou lors de l’affichage de l’appartenance à un regroupement d’appareils. Il est désormais possible d’effectuer une **Notification du client** à partir du nœud **Appareils** directement. Il n’est plus nécessaire de se trouver dans une vue de l’appartenance au regroupement. 

Pour plus d’informations, consultez [Notifications du client](/sccm/core/clients/manage/client-notification).


### <a name="improvements-to-collection-evaluation"></a>Améliorations apportées à l’évaluation de regroupement
<!--1358981--> Les changements suivants apportés au comportement d’évaluation de regroupement peuvent améliorer les performances de site :  
 
- Auparavant, lorsque vous configuriez une planification sur un regroupement basé sur une requête, le site continuait à évaluer la requête que le paramètre de regroupement **Planifier une mise à jour complète sur ce regroupement** soit activé ou pas. Pour désactiver entièrement la planification, vous deviez modifier la planification sur **Aucun**. Désormais, le site efface la planification lorsque vous désactivez ce paramètre. Pour spécifier une planification pour l’évaluation du regroupement, activez l’option **Planifier une mise à jour complète sur ce regroupement**.  

- Vous ne pouvez pas désactiver l’évaluation de regroupements intégrés, comme **Tous les systèmes**, mais vous pouvez maintenant configurer la planification. Ce comportement vous permet de personnaliser cette action sur une heure qui répond aux besoins de votre entreprise. 

<!--For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).-->


### <a name="improvement-to-client-installation"></a>Amélioration apportée à l’installation du client
<!--1358840--> Pendant l’installation du client Configuration Manager, le processus ccmsetup contacte le point de gestion pour localiser le contenu nécessaire. Avant, dans ce processus, le point de gestion retournait uniquement les points de distribution du groupe de limites actif du client. Si aucun contenu n’était disponible, le processus d’installation se repliait sur le téléchargement du contenu auprès du point de gestion. Aucune option ne permettait de se replier sur les points de distribution d’autres groupes de limites qui auraient pu disposer du contenu nécessaire. Maintenant, le point de gestion retourne les points de distribution en fonction de la configuration des groupes de limites. 

Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup).


### <a name="improvements-to-internet-based-client-setup"></a>Améliorations apportées à l’installation de clients basés sur Internet
<!--1359181-->
<!--move this under co-management?--> Cette version simplifie davantage le processus d’installation du client Configuration Manager pour les clients sur Internet. Le site publie des informations Azure Active Directory (Azure AD) supplémentaires sur la passerelle de gestion cloud (CMG). Un client joint à un Azure AD obtient ces informations à partir de la passerelle CMG pendant le processus ccmsetup, à l’aide du même locataire que celui auquel il est joint. Ce comportement simplifie davantage l’inscription d’appareils à la cogestion dans un environnement avec plusieurs locataires Azure AD. Maintenant les deux seules propriétés ccmsetup requises sont **CCMHOSTNAME** et **SMSSiteCode**.

<!--For more information, see [Prepare Windows 10 devices for co-management](https://docs.microsoft.com/en-us/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).-->



## <a name="bkmk_comgmt"></a> Cogestion

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Stratégie de conformité des applications obligatoires pour les appareils cogérés
<!--1358196--> Définissez les règles de la stratégie de conformité pour les applications obligatoires dans Configuration Manager. Cette évaluation des applications fait partie de l’état de conformité global envoyé à Microsoft Intune pour les appareils cogérés.

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### <a name="improvement-to-co-management-dashboard"></a>Amélioration apportée au tableau de bord de cogestion
<!--1358980--> Le tableau de bord de cogestion a été amélioré avec des informations plus détaillées, à savoir :  

- Vignette **État d’inscription à la cogestion** comportant des états supplémentaires

- Nouvelle vignette **État de la cogestion** avec un graphique en entonnoir montrant les états du processus d’inscription

- Nouvelle vignette avec le nombre des **erreurs d’inscription**

![Capture d’écran du tableau de bord Cogestion montrant les quatre vignettes principales](media/1358980-comgmt-dashboard.png)

Pour plus d’informations, consultez [Tableau de bord de cogestion](/sccm/comanage/how-to-monitor#co-management-dashboard).



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gestion des applications

### <a name="convert-applications-to-msix"></a>Convertir des applications en MSIX
<!--1359029--> À compter de la version 1806, Configuration Manager prend en charge le déploiement du nouveau format de package d’application (.msix) Windows 10. Vous pouvez désormais convertir vos applications Windows Installer (.msi) existantes au format MSIX.

<!--For more information, see [Create Windows applications](/sccm/apps/get-started/creating-windows-applications#bkmk_general).  this might move to a new section for msix-->


### <a name="repair-applications"></a>Réparer des applications
<!--1357866--> Spécifiez une ligne de commande de réparation pour les types de déploiement basés sur Windows Installer et le Programme d’installation de script. Si vous activez ensuite l’option sur le déploiement, un nouveau bouton est disponible dans le Centre logiciel pour **réparer** l’application. Lorsque vous configurez une application avec un programme de réparation, les utilisateurs peuvent démarrer la commande depuis le centre logiciel. 

Pour plus d’informations, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications#bkmk_dt-content) et [Déployer des applications](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Approuver les demandes d’application par e-mail
<!--1321550--> Configurez des notifications par e-mail pour les demandes d’approbation d’applications. Quand un utilisateur demande une application, vous recevez un e-mail. Cliquez sur les liens de l’e-mail pour approuver ou refuser la demande, sans avoir besoin d’utiliser la console Configuration Manager.

Pour plus d’informations, consultez [Approuver des applications](/sccm/apps/deploy-use/app-approval).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>Les méthodes de détection ne chargent pas les profils Windows PowerShell
<!--1359239--> Vous pouvez utiliser des scripts Windows PowerShell pour les méthodes de détection destinées aux applications et aux paramètres dans les éléments de configuration. Quand ces scripts s’exécutent sur des clients, le client Configuration Manager appelle maintenant PowerShell avec le paramètre `-NoProfile`. Cette option démarre PowerShell sans aucun profil. 

Un profil PowerShell est un script qui s’exécute au démarrage de PowerShell. Vous pouvez créer un profil PowerShell pour personnaliser votre environnement et ajouter des éléments spécifiques à la session à chaque session PowerShell que vous démarrez. 

> [!Note]  
> Ce changement de comportement ne s’applique pas à [Scripts](/sccm/apps/deploy-use/create-deploy-scripts) ni à [CMPivot](/sccm/core/servers/manage/cmpivot). Ces deux fonctionnalités utilisent déjà ce paramètre PowerShell.    

<!--For more information, see []().-->


## <a name="bkmk_osd"></a> Déploiement de système d’exploitation

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Prise en charge de la séquence de tâches de Windows Autopilot pour les appareils existants
<!--1358333-->

[Windows Autopilot pour les appareils existants](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430), est désormais disponible avec Windows 10, version 1809 ou ultérieure. Cette nouvelle fonctionnalité vous permet de réimager et de provisionner un appareil Windows 7 pour [Windows Autopilot en mode piloté par l’utilisateur](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) à l’aide d’une seule séquence de tâches Configuration Manager native. 

<!--For more information, see []().--> 


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Spécifier le lecteur pour la maintenance des images de système d’exploitation hors connexion  
<!--1358924--> Spécifiez à présent le lecteur utilisé par Configuration Manager pour ajouter des mises à jour logicielles à des images de système d’exploitation et à des packages de mise à niveau de système d’exploitation. Ce processus peut consommer une grande quantité d’espace disque en raison des fichiers temporaires. Cette option vous permet donc de sélectionner le lecteur à utiliser. 

Pour plus d’informations, consultez [Gérer les images de système d’exploitation](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) ou [Gérer les packages de mise à niveau de système d’exploitation](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Prise en charge des séquences de tâches pour les groupes de limites
<!--1359025--> Quand un appareil exécute une séquence de tâches et a besoin d’acquérir du contenu, il utilise désormais des comportements de groupe de limites comparables à ceux du client Configuration Manager.   

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Améliorations apportées à la maintenance des pilotes
<!--1358270--> Les packages de pilotes comptent désormais des champs de métadonnées supplémentaires pour **Fabricant** et **Modèle**. Servez-vous de ces champs pour étiqueter les packages de pilotes avec des informations dans le but de faciliter les tâches de nettoyage ou d’identifier les pilotes périmés ou en double que vous pouvez supprimer.


### <a name="new-task-sequence-variable-for-last-action-name"></a>Nouvelle variable de séquence de tâches pour le nom de la dernière action
<!--SCCMDocs-pr issue #2964--> En plus de la variable _SMSTSLastActionRetCode, la séquence de tâches définit la nouvelle variable **_SMSTSLastActionName**. Elle enregistre également cette valeur dans le fichier smsts.log. Cette nouvelle variable est utile dans le cadre du dépannage d’une séquence de tâches. Quand une étape échoue, un script personnalisé peut inclure le nom de l’étape avec le code de retour.

Pour plus d’informations, voir [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName).



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a> Mises à jour logicielles

### <a name="phased-deployment-of-software-updates"></a>Déploiement échelonné des mises à jour logicielles
<!--1358146--> Créer des déploiement par phases pour les mises à jour logicielles. Ils permettent d’orchestrer un lancement coordonné et séquencé de logiciels en fonction de groupes et de critères personnalisables.

Pour plus d’informations, voir [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Amélioration apportée aux fenêtres de maintenance pour les mises à jour logicielles
<!--vso2839307--> Le paramètre client suivant est dans le groupe **Mises à jour logicielles** pour contrôler le comportement d’installation des mises à jour logicielles dans les fenêtres de maintenance : 

**Activer l’installation des mises à jour dans la fenêtre de maintenance « Tous les déploiements » quand la fenêtre de maintenance « Mises à jour logicielles » est disponible**

Par défaut, cette option est définie sur **Non** pour rester dans la lignée du comportement existant. Choisissez **Oui** pour permettre aux clients d’utiliser les autres fenêtres de maintenance disponibles afin d’installer les mises à jour logicielles.

<!--For more information, see []().-->



## <a name="bkmk_report"></a> Rapports

### <a name="improvement-to-lifecycle-dashboard"></a>Amélioration apportée au tableau de bord Cycle de vie
<!--1358702--> Le tableau de bord Cycle de vie du produit comporte désormais des informations pour **System Center 2012 Configuration Manager et versions ultérieures**. 

Il existe également un nouveau rapport, **Cycle de vie 05A - Tableau de bord Cycle de vie du produit**. Celui-ci contient des informations semblables à celles du tableau de bord dans la console.

Pour plus d’informations sur ce tableau de bord, consultez [Utiliser le tableau de bord Cycle de vie du produit](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="improvement-to-data-warehouse"></a>Amélioration apportée à l’entrepôt de données
<!--1358870--> Vous pouvez maintenant synchroniser plus de tables de la base de données de site avec l’entrepôt de données. Ce changement vous permet de créer davantage de rapports pour répondre aux besoins de votre entreprise.

Pour plus d’informations, consultez [Entrepôt de données](/sccm/core/servers/manage/data-warehouse).



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Console Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Authentification administrateur Configuration Manager
<!--1357013--> Vous pouvez maintenant spécifier le niveau d’authentification minimal pour les administrateurs qui accèdent aux sites Configuration Manager. Cette fonctionnalité force les administrateurs à se connecter à Windows avec le niveau requis. Pour configurer ce paramètre, recherchez l’onglet **Authentification** dans **Paramètres de la hiérarchie**. 

Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth).


### <a name="support-center"></a>Centre d’aide et de support
<!--1357489--> Utilisez le Centre d’aide et de support pour la résolution des problèmes clients, l’affichage des journaux en temps réel ou la capture de l’état d’un ordinateur client Configuration Manager pour l’analyser ultérieurement. Le Centre d’aide et de support est un outil unique permettant de combiner de nombreux outils administrateur de résolution des problèmes. Recherchez le programme d’installation du Centre d’aide et de support sur le serveur de site dans le dossier **cd.latest\SMSSETUP\Tools\SupportCenter**.

Pour plus d’informations, consultez [Centre d’aide et de support](/sccm/core/support/support-center).


### <a name="management-insights-dashboard"></a>Tableau de bord Insights de gestion
<!--1357979-->

Le nœud **Insights de gestion** comprend désormais un tableau de bord graphique. Ce tableau de bord présente une vue d’ensemble de l’état des règles, ce qui vous permet de montrer plus facilement votre progression. Le tableau de bord comprend les vignettes suivantes :

- **Index des insights de gestion** : Suit la progression globale des règles d’insights de gestion. L’index est une moyenne pondérée. Les règles critiques sont celles qui comptent le plus. Les règles facultatives sont celles qui ont le moins de poids.  

- **Groupes d’insights de gestion** : Affiche le pourcentage de règles dans chaque groupe.  

- **Priorité des insights de gestion** : Affiche le pourcentage de règles par priorité.  

- **Tous les insights** : Tableau des insights comprenant la priorité et l’état.  

![Capture d’écran du tableau de bord Insights de gestion](media/1357979-management-insights-dashboard.png)

Pour plus d’informations, consultez [Insights de gestion](/sccm/core/servers/manage/management-insights).


### <a name="improvements-to-cmpivot"></a>Améliorations apportées à CMPivot
<!--1359068--> CMPivot intègre les améliorations suivantes :

- Enregistrement des requêtes en **Favori**.  

- Sous l’onglet Résumé de la requête, sélectionnez le nombre d’appareils en Échec ou Hors connexion, puis sélectionnez l’option permettant de **Créer un regroupement**. 

Pour plus d’informations sur les autres améliorations apportées à CMPivot sur le plan des performances et du dépannage, consultez [Améliorations apportées aux scripts](#bkmk_scripts).

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> Améliorations apportées aux scripts
<!--1358239--> Vous pouvez désormais afficher la sortie de script détaillée au format JSON brut ou structuré. Cette mise en forme rend la sortie plus facile à lire et à analyser. 

Les améliorations suivantes en matière de performances et de dépannage s’appliquent à CMPivot et aux scripts :

- Les clients mis à jour retournent une sortie de moins de 80 Ko au site via un canal de communication rapide. Cette modification améliore les performances d’affichage de la sortie de script ou de requête.  

- Journaux supplémentaires pour le dépannage  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### <a name="sms-provider-api"></a>API Fournisseur SMS
<!--1321523--> Le fournisseur SMS fournit désormais des accès d’interopérabilité d’API en lecture seule à WMI sur HTTPS. Le **fournisseur SMS** apparaît sous la forme d’un rôle avec une option permettant d’autoriser la communication sur la passerelle de gestion cloud. Ce paramètre permet actuellement d’activer les approbations d’application par e-mail à partir d’un appareil distant. Pour plus d’informations, consultez [Approuver les requêtes des applications par e-mail](#approve-application-requests-via-email).



## <a name="bkmk_opmdm"></a> MDM au niveau local

### <a name="an-intune-connection-is-no-longer-required-for-on-premises-mdm"></a>Une connexion Intune n’est plus nécessaire pour MDM au niveau local
<!--1359124--> Le prérequis consistant à configurer un abonnement Microsoft Intune n’est plus nécessaire pour MDM au niveau local. Votre organisation exige toujours des licences Intune pour utiliser cette fonctionnalité. 



## <a name="next-steps"></a>Étapes suivantes

Quand vous êtes prêt à installer cette version, consultez [Installer des mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates) et [Liste de contrôle pour installer la mise à jour 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810).

> [!TIP]  
> Pour installer un nouveau site, utilisez une version de base de référence de Configuration Manager.  
>
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Pour plus d’informations sur les problèmes importants et connus, consultez les [Notes de publication](/sccm/core/servers/deploy/install/release-notes).

Après avoir mis à jour un site, consultez également la [Liste de contrôle post-mise à jour](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).
