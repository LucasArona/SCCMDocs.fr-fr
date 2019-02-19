---
title: Préversion technique 1806.2
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités disponibles dans la version 1806.2 de Configuration Manager Technical Preview.
ms.date: 06/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3af2a69d-30e7-4dce-832d-82b7a1c082f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ef015f755a42ff113b2ca80bcc2a5650fbf30231
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134739"
---
# <a name="capabilities-in-technical-preview-18062-for-system-center-configuration-manager"></a>Fonctionnalités de la préversion technique 1806.2 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans la version 1806.2 de Configuration Manager Technical Preview. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités au site de votre préversion technique. 

Consultez l’article [Technical Preview](/sccm/core/get-started/technical-preview) avant d’installer cette mise à jour. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->

## <a name="known-issues-in-this-technical-preview"></a>Problèmes connus dans cette préversion technique

### <a name="ki_sqlncli"></a> Les clients ne se mettent pas à jour automatiquement
<!--518760--> Lors de la mise à jour vers la version 1806.2, le site met également à jour SQL Native Client, ce qui peut occasionner un redémarrage en attente sur le serveur de site. En raison de ce délai, certains fichiers ne sont pas mis à jour, ce qui se répercute sur la mise à niveau automatique du client.

#### <a name="workarounds"></a>Solutions de contournement
Évitez ce problème en passant manuellement à SQL Native Client *avant de mettre à jour* Configuration Manager vers la version 1806.2. Pour plus d’informations, consultez la [dernière mise à jour de maintenance pour SQL Server 2012 Native Client](https://www.microsoft.com/download/details.aspx?id=50402).

Si vous déjà mis à jour votre site, la mise à niveau automatique du client et l’installation Push du client ne fonctionneront pas. Vous devrez mettre à jour les clients pour pouvoir tester intégralement la plupart des nouvelles fonctionnalités. Mettez à jour manuellement vos clients de la préversion technique en suivant la procédure ci-dessous :  

1. Localisez les fichiers sources du client dans le dossier **CMUClient** du répertoire d’installation de Configuration Manager sur le serveur de site. Par exemple, `C:\Program Files\Configuration Manager\CMUClient`  

2. Copiez la totalité du dossier CMUClient sur l’appareil client. Par exemple, `C:\Temp\CMUClient`  

    Cet emplacement peut être un partage réseau accessible à partir des clients.  

3. Exécutez la ligne de commande suivante dans une invite de commandes avec élévation de privilèges : `C:\Temp\CMUClient\ccmsetup.exe /source:C:\Temp\CMUClient`  

Si vous installez un nouveau client dans votre site version 1806.2 Technical Preview, suivez la même procédure. 

> [!Important]  
> N’utilisez pas le paramètre de ligne de commande `/MP` dans ce scénario. Ce paramètre est prioritaire sur `/source` et conduit ccmsetup à télécharger le contenu du client à partir du point de gestion ou du point de distribution.
> 
> Des propriétés de ligne de commande comme SMSSITECODE ou CCMLOGLEVEL peuvent être utilisées, mais ne devraient pas être nécessaires pour la mise à niveau d’un client existant. 


### <a name="ki_version"></a> La version 1806.2 indique Version 1806 dans À propos de Configuration Manager
<!--518148--> Après la mise à niveau vers la version 1806.2 Technical Preview, lorsque vous ouvrez la fenêtre **À propos de Configuration Manager** dans le coin supérieur gauche de la console, elle affiche toujours **Version 1806**. 

#### <a name="workaround"></a>Solution de contournement
Utilisez la propriété **Version du site** pour déterminer la différence entre les versions 1806 et 1806.2 :

| Version du site  | Version
|---------|---------|
| 5.0.**8672**.1000 | 1806 |
| 5.0.**8685**.1000 | 1806.2 |
 


</br>

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  


## <a name="bkmk_pod"></a> Améliorations apportées aux déploiements par phases

Cette version intègre les améliorations suivantes du [déploiement par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) :
- [État du déploiement par phases](#bkmk_pod-monitor)
- [Déploiement d’applications par phases](#bkmk_pod-app)
- [Lancement graduel lors des déploiements par phases](#bkmk_pod-throttle)


### <a name="bkmk_pod-monitor"></a> État du déploiement par phases
<!--1358577--> Les déploiements par phases ont maintenant une expérience de monitoring native. Dans le nœud **Déploiements** de l’espace de travail **Monitoring**, sélectionnez un déploiement par phases, puis cliquez sur **État du déploiement par phases** dans le ruban.

![Tableau de bord de l’état du déploiement par phases indiquant l’état de deux phases](media/1358577-phased-deployment-status.png)

Ce tableau de bord montre les informations suivantes pour chaque phase du déploiement :  

- **Nombre total d’appareils** : Nombre d’appareils ciblés par cette phase.  

- **État** : État actuel de cette phase. Chaque phase peut se trouver dans l’un des états suivants :  

    - **Déploiement créé** : Le déploiement par phases a créé un déploiement du logiciel sur le regroupement pour cette phase. Les clients sont activement ciblés avec ce logiciel.  

    - **En attente** : La phase précédente n’a pas encore rempli les critères de réussite pour que le déploiement passe à cette phase.  

    - **Suspendu** : Un administrateur a suspendu le déploiement.  

- **Progression** : États de déploiement à partir des clients selon un code de couleurs. Par exemple : Réussite, En cours, Erreur, Exigences non remplies et Inconnu. 


#### <a name="known-issue"></a>Problème connu
Le tableau de bord d’état du déploiement par phases affiche parfois plusieurs lignes pour une même phase.<!--518510-->


### <a name="bkmk_pod-app"></a> Déploiement d’applications par phases
<!--1358147--> Créez des déploiements par phases pour les applications. Ils permettent d’orchestrer un lancement coordonné et séquencé de logiciels en fonction de groupes et de critères personnalisables.

Dans la console de Configuration Manager, accédez à **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez **Applications**. Sélectionnez une application, puis cliquez sur **Créer un déploiement par phases** dans le ruban. 

Le comportement d’un déploiement d’application par phases est la même que celui des séquences de tâches. Pour plus d’informations, voir [Créer des déploiements par phases pour une séquence de tâches](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="prerequisite"></a>Condition préalable
Distribuez le contenu de l’application à un point de distribution avant de créer le déploiement par phases.<!--518293-->

#### <a name="known-issue"></a>Problème connu
Vous ne pouvez pas créer de phases manuellement pour une application. L’Assistant crée automatiquement deux phases pour les déploiements d’applications.


### <a name="bkmk_pod-throttle"></a> Lancement graduel lors des déploiements par phases
<!--1358578--> Lors d’un déploiement par phases, le lancement peut maintenant se produire progressivement dans chaque phase. Ce comportement limite les risques de problèmes de déploiement et diminue la charge sur le réseau causée par la distribution de contenu auprès des clients. Le site peut rendre le logiciel disponible progressivement en fonction de la configuration de chaque phase. Tous les clients d’une phase donnée ont une échéance qui dépend du moment de la mise à disposition du logiciel. La fenêtre entre la mise à disposition et l’échéance est la même pour tous les clients d’une phase. 

Quand vous créez un déploiement par phases et que vous configurez manuellement une phase, dans la page **Paramètres de la phase** de l’Assistant Ajouter une phase ou sur la page **Paramètres** de l’Assistant Créer un déploiement par phases, configurez l’option : **Rendre ce logiciel disponible progressivement pendant cette période de temps (en jours)**. La valeur par défaut de ce paramètre est **0** ; ainsi, par défaut, le déploiement n’est pas limité.

> [!Note]  
> Cette option n’est disponible à l’heure actuelle que pour les déploiements par phases de séquences de tâches.  



## <a name="bkmk_msix"></a> Prise en charge de nouveaux formats de package d’application Windows
<!--1357427--> Configuration Manager prend maintenant en charge le déploiement de nouveaux formats de package d’application Windows 10 (.msix) et d’ensemble d'applications (.msixbundle). Les dernières versions de [Windows Insider Preview](https://insider.windows.com/) prennent actuellement en charge ces nouveaux formats.

Pour une vue d’ensemble de MSIX, voir [Examen plus poussé de MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).

Pour savoir comment créer une application MSIX, voir [Prise en charge de MSIX introduite dans la version 17682 d’Insider](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).

### <a name="prerequisites"></a>Prérequis
- un client Windows 10 ayant au moins la version 17682 de Windows Insider Preview ;
- un package d'application Windows au format MSIX.

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, [créez une application](/sccm/apps/deploy-use/create-applications). 
2. Sélectionnez le fichier d’installation d’application de **type** **Package d’application Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**.
3. [Déployez l’application](/sccm/apps/deploy-use/deploy-applications) sur le client qui a la dernière version de Windows Insider Preview.



## <a name="bkmk_client-push"></a> Amélioration apportée à la sécurité Push du client
<!--1358204--> Avec la méthode [d’installation Push du client](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation) Configuration Manager, le serveur de site crée une connexion à distance au client pour lancer l’installation. À partir de cette version, le site peut exiger l’authentification mutuelle Kerberos en interdisant le recours à NTLM en secours avant d’établir la connexion. Cette amélioration permet de sécuriser la communication entre le serveur et le client. 

En fonction de vos stratégies de sécurité, il est possible que votre environnement préfère ou requière déjà l’authentification Kerberos plutôt qu’une authentification NTLM plus ancienne. Pour plus d’informations sur l’aspect sécurité de ces protocoles d’authentification, voir [Paramètre de stratégie de sécurité Windows pour restreindre l’authentification NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).


### <a name="prerequisite"></a>Condition préalable

Pour pouvoir utiliser cette fonctionnalité, il faut que les clients se trouvent dans une forêt Active Directory approuvée. Kerberos sous Windows s’appuie sur Active Directory pour l’authentification mutuelle. 


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

Lors de la mise à niveau du site, le comportement existant est conservé. Une fois les propriétés d’installation Push du client *ouvertes*, le site active automatiquement la vérification Kerberos. Si nécessaire, vous pouvez autoriser la connexion à utiliser en secours une connexion NTLM moins sécurisée, ce qui n’est pas recommandé. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**. Sélectionnez le site cible. Dans le ruban, cliquez sur **Paramètres d’installation du client** et sélectionnez **Installation Push du client**.  

2. Le site vient d’activer la vérification Kerberos pour l’installation Push du client. Cliquez sur **OK** pour fermer la fenêtre.  

3. Si votre environnement l’impose, examinez l’option **Autoriser le recours à NTLM en secours pour la connexion** sur l’onglet **Général** de la fenêtre Propriétés d’installation Push du client. Cette option est désactivée par défaut. 



## <a name="bkmk_insights"></a> Insights d’administration pour la maintenance proactive
<!--1352184,et al--> Des insights d’administration supplémentaires sont disponibles dans cette version pour mettre en évidence les problèmes de configuration potentiels. Passez en revue les règles suivantes dans le nouveau groupe **Maintenance proactive** :  

- **Éléments de configuration inutilisés** : Éléments de configuration qui ne font pas partie d’une base de référence de configuration et datent de plus de 30 jours.  

- **Images de démarrage inutilisées** : Images de démarrage non référencées pour l’utilisation de séquences de tâches ou le démarrage PXE.  

- **Groupes de limites sans système de site attribué** : Sans systèmes de site attribué, les groupes de limites ne peuvent être utilisés que pour l’attribution de site.  

- **Groupes de limites sans membres** : Les groupes de limites ne sont pas applicables à l’attribution de site ou à la recherche de contenu s’ils n’ont aucun membre.  

- **Points de distribution ne distribuant pas de contenu aux clients** : Points de distribution n’ayant pas distribué de contenu aux clients au cours des 30 derniers jours. Ces données s’appuient sur les rapports d’historique de téléchargement des clients.  

- **Mises à jour expirées trouvées** : Les mises à jour expirées ne sont pas applicables pour le déploiement.   



## <a name="bkmk_comgmt"></a> Transférer la charge de travail des applications mobiles pour les appareils cogérés
<!--1357892--> Gérez des applications mobiles avec Microsoft Intune tout en continuant à utiliser Configuration Manager pour déployer des applications de bureau Windows. Pour transférer la charge de travail des applications modernes, accédez à la page de propriétés de cogestion. Déplacez le curseur de Configuration Manager vers Pilote ou Tout. 

Une fois cette charge de travail transférée, toutes les applications disponibles déployées à partir d’Intune seront accessibles sur le Portail d’entreprise. Les applications déployées à partir de Configuration Manager sont disponibles dans le centre logiciel. 

Pour plus d’informations, consultez les articles suivants :  

- [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview)  

- [Qu’est-ce que la gestion des applications Microsoft Intune ?](https://docs.microsoft.com/intune/app-management)  



## <a name="bkmk_bgoptions"></a> Options de groupe de limites pour les téléchargements à partir de pairs
<!--1356193--> Les groupes de limites intègrent maintenant des paramètres supplémentaires qui offrent davantage de contrôle sur la distribution du contenu dans l’environnement. Cette version ajoute les options suivantes :  

- **Autoriser les téléchargements à partir de pairs dans ce groupe de limites** : Ce paramètre est activé par défaut. Le point de gestion fournit aux clients une liste d’emplacements de contenu qui comprend des sources de pairs. <!--This setting also affects applying Group IDs for Delivery Optimization.518268-->  

    Il existe deux scénarios courants dans lesquels il peut être envisageable de désactiver cette option :  

    - Si votre groupe de limites comporte des limites provenant d’emplacements éloignés sur le plan géographique, comme un VPN. Deux clients peuvent se trouver dans le même groupe de limites, parce qu’ils sont connectés au moyen d’un VPN, alors qu’ils sont situés à des endroits très différents, ce qui ne convient pas pour le partage de contenu entre pairs.  

    - Si vous utilisez un seul grand groupe de limites pour l’attribution de site, qui ne fait référence à aucun point de distribution.  

- **Durant les téléchargements à partir de pairs, utiliser uniquement des pairs situés dans le même sous-réseau** : Ce paramètre dépend de celui illustré ci-dessus. Lorsque cette option est activée, le point de gestion n’inclut dans la liste des emplacements de contenu que les sources de pairs qui se trouvent dans le même sous-réseau que le client.

    Quelques scénarios courants pour l’activation de cette option :

    - Votre conception de groupe de limites pour la distribution de contenu comprend un grand groupe de limites qui coïncide en partie avec d’autres groupes de limites plus petits. Avec ce nouveau paramètre, la liste des sources de contenu que le point de gestion fournit aux clients n’inclut que les sources de pairs provenant du même sous-réseau.

    - Vous avez un seul grand groupe de limites pour tous les emplacements de bureau distant. Lorsque cette option est activée, les clients ne partagent du contenu qu’au sein du sous-réseau qui se trouve à l’emplacement du bureau distant, plutôt que de prendre le risque de partager du contenu entre différents emplacements.


### <a name="known-issue"></a>Problème connu
Si le client de la source de pairs a plusieurs adresses IP (IPv4, IPv6 ou les deux), la mise en cache partagé entre systèmes homologues ne fonctionne pas. La nouvelle option **Lors des téléchargements à partir de pairs, utiliser seulement les pairs qui se trouvent dans le même sous-réseau** n’a aucun effet si la source de pairs comporte plusieurs adresses IP.<!--518661-->   



## <a name="bkmk_3pupdate"></a> Prise en charge de mises à jour de logiciels tiers pour les catalogues personnalisés
<!--1358714--> Pour répondre à la demande que vous avez exprimée par le biais des [commentaires UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), cette nouvelle version comprend une meilleure prise en charge des mises à jour de logiciels tiers. La [version 1806 Technical Preview](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate) prenait en charge les *catalogues de partenaires*, qui sont des catalogues référencés par des éditeurs de logiciels. Les catalogues que vous fournissez et qui ne sont pas inscrits auprès de Microsoft sont appelés catalogues *personnalisés*. Ajoutez des catalogues personnalisés dans la console de Configuration Manager.  


### <a name="prerequisites"></a>Prérequis 

- Configurez les [mises à jour des logiciels tiers](/sccm/core/get-started/capabilities-in-technical-preview-1806#bkmk-3pupdate). Terminer la phase 1 : Activer et configurer la fonctionnalité.   

- Un catalogue personnalisé signé numériquement contenant des mises à jour logicielles signées numériquement.  

- L’administrateur exige les autorisations suivantes :  

    - Site : Créer, modifier  


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles**, puis sélectionnez le nœud **Catalogues de mises à jour de logiciels tiers**. Cliquez sur **Ajouter un catalogue personnalisé** dans le ruban.  

2. Sur la page **Général**, spécifiez les informations suivantes :  

    - **URL de téléchargement** : adresse HTTPS valide du catalogue personnalisé.  

    - **Éditeur** : nom de l’organisation qui publie le catalogue.  

    - **Nom** : Nom du catalogue à afficher dans la console Configuration Manager.  

    - **Description** : description du catalogue.  

    - **URL du support technique** (facultatif) : adresse HTTPS valide d’un site web d’aide sur le catalogue.  

    - **Contact du support technique** (facultatif) : coordonnées de la personne à contacter pour obtenir de l’aide sur le catalogue.  

3. Effectuez toutes les étapes de l'Assistant. L’Assistant ajoute le nouveau catalogue avec un état désabonné.  

4. Abonnez-vous au catalogue personnalisé avec l’action **S’abonner au catalogue** existante. Pour plus d’informations, consultez [Phase 2 : S’abonner à un catalogue tiers et synchroniser les mises à jour](/sccm/core/get-started/capabilities-in-technical-preview-1806#phase-2-subscribe-to-a-third-party-catalog-and-sync-updates).  

> [!Note]  
> Vous ne pouvez pas ajouter de catalogues utilisant la même URL de téléchargement, ni modifier les propriétés des catalogues. Si vous avez spécifié des propriétés incorrectes pour un catalogue personnalisé, supprimez-le avant de l’ajouter à nouveau.  


#### <a name="unsubscribe-from-a-catalog"></a>Se désabonner d’un catalogue
Pour vous désabonner d’un catalogue, sélectionnez-le dans la liste, puis cliquez sur **Se désabonner du catalogue** dans le ruban. Le désabonnement d’un catalogue provoque les actions et les comportements suivants : 
- Le site arrête la synchronisation des nouvelles mises à jour. 
- Le site bloque les certificats associés pour le contenu de mise à jour et de signature du catalogue. 
- Les mises à jour existantes ne sont pas supprimées, mais il n’est pas forcément possible de les publier ou de les déployer.

#### <a name="delete-a-custom-catalog"></a>Supprimer un catalogue personnalisé
Supprimez les catalogues personnalisés à partir du même nœud de la console. Sélectionnez un catalogue personnalisé à l’état *Désabonné*, puis cliquez sur **Supprimer le catalogue personnalisé**. Si vous avez déjà mis en place un abonnement à ce catalogue, désabonnez-vous avant de le supprimer. Vous ne pouvez pas supprimer les catalogues de partenaires. La suppression d’un catalogue personnalisé a pour effet de le retirer de la liste des catalogues. Cette action n’affecte pas les mises à jour logicielles que vous avez publiées sur votre point de mise à jour logicielle.


### <a name="known-issue"></a>Problème connu
L’action de suppression est grisée sur les catalogues personnalisés, ce qui empêche de supprimer des catalogues personnalisés dans la console. Pour contourner ce problème, utilisez l’outil **wbemtest** sur le serveur de site. Effectuez une requête sur l’instance que vous souhaitez supprimer avec le nom ou l’URL de téléchargement, par exemple : `select * from SMS_ISVCatalog where DownloadURL="http://www.contoso.com/catalog.cab"`. Dans la fenêtre de résultat de la requête, sélectionnez l’objet, puis cliquez sur **Supprimer**.<!--518676-->  



## <a name="bkmk_cloud"></a> Améliorations apportées aux fonctionnalités de gestion cloud

Cette version intègre les améliorations suivantes :  

- Les fonctionnalités suivantes prennent maintenant en charge l’utilisation d’Azure U.S. Government Cloud :<!--511980-->  

    - l’intégration du site pour la **Gestion cloud** avec les [Services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) ;  

    - le déploiement d’une [Passerelle de gestion cloud avec Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) ;  

    - le déploiement d’un [point de distribution cloud avec Azure Resource Manager](/sccm/core/get-started/capabilities-in-technical-preview-1805#cloud-distribution-point-support-for-azure-resource-manager).  

- Les clients utilisent Windows AutoPilot pour configurer Windows 10 sur des appareils joints à Azure Active Directory et connectés au réseau local. Pour installer ou mettre à niveau le client Configuration Manager sur ces appareils, il n’est plus nécessaire de configurer un point de distribution cloud ou un point de distribution local sur **Autoriser les clients à se connecter anonymement**. Au lieu de cela, activez l’option de site **Utiliser des certificats générés par Configuration Manager pour les systèmes de site HTTP**, qui permet à un client joint à un domaine cloud de communiquer avec un point de distribution local compatible avec le protocole HTTP. Pour plus d’informations, voir [Amélioration des communications clientes sécurisées](https://docs.microsoft.com/en-us/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).<!--515854-->  



## <a name="bkmk_report"></a> Nouveau rapport sur la conformité des mises à jour logicielles
<!--1357775--> L’affichage des rapports de conformité des mises à jour logicielles comporte généralement des données provenant de clients qui n’ont pas contacté le site récemment. Un nouveau rapport permet de filtrer les résultats de conformité d’un groupe de mises à jour logicielles donné sur les clients « sains ». Ce rapport affiche l’état de conformité plus réaliste des clients actifs de votre environnement. 
 
Pour afficher le rapport, accédez à l’espace de travail **Monitoring**, développez **Reporting**, puis **Rapports** et **Mises à jour logicielles – Conformité A**, puis sélectionnez **Conformité 9 – Conformité et intégrité globales**. Spécifiez **Groupe de mises à jour**, **Nom de la collection** et l’état **d’intégrité du client**.

Le rapport comprend les parties suivantes :
- **Proportion de clients sains par rapport au nombre total de clients** : Ce graphique à barres compare le nombre de clients « sains », qui ont communiqué avec le site au cours de la période indiquée, avec le nombre total de clients dans le regroupement spécifié.
- **Vue d’ensemble de la conformité** : Ce graphique à secteurs indique l’état de conformité global du groupe de mises à jour logicielles concerné sur les clients actifs dans le regroupement spécifié.
- **5 principales mises à jour non conformes par ID d’article** : Ce graphique à barres montre les cinq principales mises à jour logicielles du groupe concerné qui ne sont pas conformes sur les clients actifs dans le regroupement spécifié.
- La partie inférieure du rapport est un tableau plus détaillé, qui liste les mises à jour logicielles du groupe spécifié.



## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
