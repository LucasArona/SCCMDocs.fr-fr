---
title: Technical Preview 1804
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités disponibles dans Configuration Manager Technical Preview version 1804.
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8af43618-ec60-4c3e-a007-12399d1335b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0fcdcc984e267e6c54ad7c6194e8494854f0a1ee
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1804-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1804 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans Technical Preview version 1804 pour Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités au site de votre préversion technique. 

Consultez l’article [Technical Preview](/sccm/core/get-started/technical-preview) avant d’installer cette mise à jour. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template   -->
## <a name="known-issues-in-this-technical-preview"></a>Problèmes connus dans cette préversion technique

### <a name="bkmk_appcathttps"></a> HTTPS ne peut pas être activé sur le point de service web du catalogue des applications
<!--512637-->
Si HTTPS est activé sur le point de service web du catalogue des applications :

- Les applications déployées comme étant disponibles pour les utilisateurs ne s’affichent pas dans le Centre logiciel  

- L’erreur suivante s’affiche dans awebsctl.log :  

     `Call to HttpSendRequestSync failed for port 443 with status code 500, text: Internal Server Error`

#### <a name="workaround"></a>Solution de contournement
Reconfigurez le point de service web du catalogue des applications pour qu’il communique à l’aide de connexions HTTP.  




</br>

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  


## <a name="configure-a-remote-content-library-for-the-site-server"></a>Configurer une bibliothèque de contenu à distance pour le serveur de site  
<!--1357525-->
Pour libérer de l’espace disque sur votre serveur de site principal, vous devez déplacer sa [bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library) vers un autre emplacement de stockage. Vous pouvez déplacer la bibliothèque de contenu sur un autre disque du serveur de site, sur un serveur distinct ou sur des disques à tolérance de panne dans un réseau de zone de stockage (SAN). Nous recommandons l’utilisation d’un réseau SAN qui fournit un stockage élastique capable de croître ou de se réduire au fil du temps pour répondre à vos besoins en termes de contenu. 

Cette bibliothèque de contenu à distance est un nouveau prérequis pour la [haute disponibilité au niveau du rôle serveur de site](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability). 

> [!Note]  
> Cette action déplace uniquement la bibliothèque de contenu sur le serveur de site. Elle n’affecte pas l’emplacement de la bibliothèque de contenu sur les points de distribution. 

### <a name="prerequisites"></a>Prérequis  
- Le compte de l’ordinateur du serveur de site doit disposer d’autorisations en **lecture** et en **écriture** pour le chemin d’accès réseau vers lequel vous déplacez la bibliothèque de contenu. Aucun composant n’est installé sur le système à distance. 

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site** et sélectionnez **Sites**. Dans l’onglet **Résumé** en bas du volet d’informations, vous noterez l’apparition d’une nouvelle colonne pour la **Bibliothèque de contenu**.  

2. Sur le ruban, cliquez sur **Gérer la bibliothèque de contenu**.  

3. Sélectionnez **Sur un partage réseau** et entrez un chemin d’accès réseau valide. Ce chemin d’accès est l’emplacement vers lequel le site déplace la bibliothèque de contenu. Cliquez sur **OK**.  

4. Notez la propriété **État** dans la colonne Bibliothèque de contenu dans le volet d’informations. Elle se met à jour pour afficher la progression du site en termes de déplacement de la bibliothèque de contenu. Lors de l’opération, le pourcentage de progression s’affiche. En cas d’état d’erreur, elle affiche l’erreur. Les erreurs courantes incluent `access denied` ou `disk full`. Lorsque l’opération est terminée, `OK` s’affiche. Consultez **distmgr.log** pour plus d’informations. Pour plus d’informations, consultez [Journaux serveur du serveur de site et du système de site](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Si vous avez besoin redéplacer la bibliothèque de contenu vers le serveur de site, répétez ce processus, mais sélectionnez l’option **Local vers serveur de site**.  

> [!Tip]  
> Pour déplacer le contenu vers un autre disque du serveur de site, utilisez l’outil **Transfert de bibliothèque de contenu**. Pour plus d’informations, consultez [Kit de ressources Configuration Manager](#configuration-manager-toolkit).  



## <a name="bkmk_feedback"></a> Envoyer des commentaires à partir de la console Configuration Manager  
<!--1357542-->

Envoyer un sourire ! Vous pouvez maintenant communiquer directement avec l’équipe Configuration Manager sur vos expériences. L’envoi de commentaires est facile à partir de la console Configuration Manager. Nous voulons recevoir tous vos commentaires : les éloges, les problèmes et les suggestions.  

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des **commentaires** pour nous indiquer comment cela a fonctionné.  

1. Dans la console Configuration Manager, cliquez sur le bouton en forme de sourire dans l’angle supérieur droit au-dessus du ruban.  

2. Sélectionnez l'une des options disponibles  dans la liste déroulante :  

   - **Envoyer un sourire** : vous avez beaucoup apprécié quelque chose ! Pour cette option, entrez des commentaires détaillés. Puis, incluez éventuellement une capture d’écran et votre adresse e-mail.  

   - **Envoyer un smiley mécontent** : vous avez rencontré un problème dans la console ou quelque chose n’a pas fonctionné comme prévu. Pour cette option, entrez des informations détaillées sur le problème produit potentiel. Puis, incluez éventuellement une capture d’écran, votre adresse e-mail et les données de diagnostic.  

   - **Envoyer une suggestion** : vous avez une idée pour modifier et améliorer Configuration Manager. Cette option ouvre notre site [UserVoice](https://configurationmanager.uservoice.com) dans votre navigateur web.  

Ces commentaires sont envoyés directement à l’équipe produit Microsoft pour Configuration Manager. Bien que l’utilisation du concentrateur de commentaires de Windows 10 soit toujours prise en charge, nous vous encourageons à utiliser la fonction de commentaires dans la console.  

Les informations anonymes suivantes sont toujours incluses avec les commentaires à des fins de contexte :  

 - Version et langue de la console Configuration Manager  

 - Version de site Configuration Manager  

 - ID de support, également connu comme ID de hiérarchie  

 - Version et langue du système d’exploitation du système sur lequel la console est en cours d’exécution  

 - L’emplacement exact dans la console où vous avez cliqué sur le sourire  

Ces données sont cohérentes avec la collecte de nos données de diagnostic et d’utilisation. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).

### <a name="known-issues"></a>Problèmes connus

Si vous essayez d’envoyer des commentaires à partir d’un appareil qui n’a pas accès à Internet, l’application risque de se fermer. Pour envoyer un sourire ou un smiley mécontent, assurez-vous que l’appareil est en mesure d’accéder à petrol.office.microsoft.com.



## <a name="support-center"></a>Centre d’aide et de support
<!--1357489-->

Utilisez le Centre d’aide et de support pour la résolution des problèmes client, l’affichage des journaux en temps réel ou la capture de l’état d’un ordinateur client Configuration Manager pour une analyse ultérieure. Le Centre d’aide et de support est un outil unique permettant de consolider de nombreux outils administrateur de résolution des problèmes. Un aperçu de la dernière version du Centre d’aide et de support avec des correctifs de bogues, des améliorations et une préversion de notre nouvelle visionneuse de journal est disponible dans la version Technical Preview. Recherchez le programme d’installation du Centre d’aide et de support sur le serveur de site dans le dossier **cd.latest\SMSSETUP\Tools\SupportCenter**.

 > [!Tip]  
 > La documentation héritée pour les fonctionnalités existantes dans le Centre d’aide et de support est disponible sur [TechNet](https://technet.microsoft.com/library/dn688621.aspx). Les informations pertinentes sont en cours de migration vers la bibliothèque docs.microsoft.com.  

### <a name="new-support-center-features"></a>Nouvelles fonctionnalités du Centre d’aide et de support  

 - Une nouvelle visionneuse du journal, OneTrace. Elle fonctionne de la même que CMTrace et inclut des améliorations, telles qu’une vue à onglets et des fenêtres ancrables.  

 - Une nouvelle fonctionnalité de collecteur de données collecte des journaux de diagnostic à partir de l’ordinateur local ou d’un client Configuration Manager à distance. Elle fournit un diagnostic en temps réel de l’inventaire (en remplacement de Client Spy), de la stratégie (en remplacement de Policy Spy) et du cache client.  



## <a name="configuration-manager-toolkit"></a>Kit de ressources de Configuration Manager
<!--1357145-->

Les outils du serveur et du client Configuration Manager sont désormais inclus avec la version Technical Preview. Vous les trouverez dans le dossier **cd.latest\SMSSETUP\Tools** du serveur de site. Aucune installation supplémentaire n’est requise.

#### <a name="server-tools"></a>Outils de serveur  

 - **Gestionnaire de travaux DP** : permet de résoudre les problèmes relatifs aux travaux de distribution de contenu aux points de distribution  

 - **Visionneuse d’évaluation de collection** : afficher les détails d’évaluation de la collection  

 - **Explorateur de la bibliothèque de contenu** : afficher le contenu du magasin d’instances unique de la bibliothèque de contenu  

 - **Transfert de la bibliothèque de contenu** : transfère la bibliothèque de contenu entre des disques  

 - **Outil de propriété du contenu** : modifie la propriété des packages orphelins. Ces packages existent dans le site sans serveur de site propriétaire.  

 - **Outil d’administration et d’audit en fonction du rôle** : permet aux administrateurs d’auditer la configuration des rôles  

#### <a name="client-tools"></a>Outils clients

 - **CMTrace** : afficher les journaux  

 - **Outil de monitoring de déploiement** : résoudre les problèmes liés aux applications, mises à jour et déploiements de ligne de base  

 - **Policy Spy** : afficher les affectations de stratégies  

 - **Outil Power Viewer** : afficher l’état de la fonctionnalité de gestion de l’alimentation  

 - **Outil Send Schedule** : déclencher des planifications et des évaluations des lignes de base DCM  

> [!Important]  
> Le [Centre d’aide et de support](#support-center) est recommandé dans la plupart des cas d’utilisation, car il inclut des fonctionnalités identiques ou améliorée pour les outils suivants :  
>  - Client Spy
>  - CMTrace<sup>1</sup> 
>  - Outil de monitoring de déploiement
>  - Policy Spy
>  - Outil Send Schedule
> 
> <sup>1</sup> CMTrace ne dépend pas de .NET ou de WPF (Windows Presentation Foundation), donc il est toujours utilisé dans les images de démarrage Windows PE.

### <a name="known-issues"></a>Problèmes connus
Certains outils client et serveur peuvent se fermer de manière inattendue à l’ouverture. Ce problème est dû à un fichier manquant sur le support. Pour contourner le problème, copiez le fichier **Microsoft.Diagnostics.Tracing.EventSource.dll** à partir du répertoire AdminConsole\bin dans les répertoires SMSSETUP\Tools\ClientTools et ServerTools. Ce fichier doit être la même version que celle utilisée par la console Configuration Manager. D’autres versions risquent de ne pas fonctionner. <!--513977-->



## <a name="uninstall-application-on-approval-revocation"></a>Désinstaller une application en cas de révocation de l’approbation
<!--1357891-->

Le comportement a changé lorsque vous révoquez une approbation pour une application. Maintenant, lorsque vous refusez la requête visant l’application, le client désinstalle l’application sur l’appareil de l’utilisateur. 

### <a name="prerequisites"></a>Prérequis
- Activez la fonctionnalité **Approuver les demandes d’application pour les utilisateurs appareil par appareil**.

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console Configuration Manager, déployez pour un utilisateur une application qui nécessite une approbation. Dans l’onglet **Paramètres de déploiement** du déploiement, activez l’option **Un administrateur doit approuver une demande pour cette application sur l’appareil**.  

2. Sur le client Configuration Manager dans le Centre logiciel, l’utilisateur demande l’approbation pour installer l’application.  

3. Dans la console Configuration Manager, approuvez la demande de cet utilisateur pour installer l’application sur l’appareil. Les demandes d’approbation d’application sont affichées dans l’espace de travail **Bibliothèque de logiciels**, sous **Gestion d’applications** dans le nœud **Demandes d’approbation**.  

4. Sur le client dans le Centre logiciel, l’utilisateur installe l’application.  

5. Dans la console Configuration Manager, refusez la demande de l’utilisateur pour installer l’application sur l’appareil.  

### <a name="known-issues"></a>Problèmes connus
- Une fois que l’utilisateur a installé l’application sur le client, mettez à jour la stratégie de l’utilisateur. Dans le Centre logiciel, basculez vers l’onglet **Options**, développez **Maintenance de l’ordinateur** et cliquez sur **Stratégie de synchronisation**.<!--480609-->  

- Le point de service web du catalogue des applications doit être de type HTTP. Pour plus d’informations, consultez [Problèmes connus dans cette préversion technique](#bkmk_appcathttps).<!--512637-->  



## <a name="exclude-active-directory-containers-from-discovery"></a>Exclure les conteneurs Active Directory de la détection
<!--1358143-->
Pour réduire le nombre d’objets détectés, vous pouvez désormais exclure des conteneurs spécifiques de la détection de systèmes Active Directory. Cette fonctionnalité est le résultat de vos [commentaires sur UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8414520-exclude-virtual-cluster-and-ou-from-discovery).

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration de la hiérarchie** et sélectionnez **Méthodes de découverte**. Sélectionnez **Découverte de système Active Directory** et cliquez sur **Propriétés** dans le ruban.  

2. Cliquez sur l’icône Nouveau pour spécifier un nouveau conteneur Active Directory.   

3. Dans la boîte de dialogue Conteneur Active Directory, accédez au **Chemin d’accès** ou entrez-le dans la section Emplacement pour démarrer la détection.  

4. Dans la section Options de recherche, activez l’option **Rechercher de manière récursive les conteneurs enfants Active Directory**. Puis, cliquez sur **Ajouter** pour sélectionner les sous-conteneurs à exclure de cette détection.  

5. Dans la boîte de dialogue Sélectionner un nouveau conteneur, sélectionnez un conteneur enfant à exclure. Cliquez sur **OK** pour fermer la boîte de dialogue Sélectionner un nouveau conteneur.  

6. Cliquez sur **OK** pour fermer la boîte de dialogue Conteneur Active Directory.  

7. Dans la fenêtre Propriétés de découverte de système Active Directory, consultez le chemin d’accès du conteneur Active Directory où démarre la détection. La colonne **Récursive** affiche **Oui** et la nouvelle colonne **A des exclusions** affiche également **Oui**. Cliquez sur **OK** pour fermer la fenêtre Propriétés de découverte de système Active Directory.  



## <a name="specify-the-visibility-of-the-application-catalog-website-link-in-software-center"></a>Spécifier la visibilité du lien du site web Catalogue d’applications dans le Centre logiciel
<!--1358214-->

Vous pouvez désormais contrôler si le lien vers **Ouvrir le site web Catalogue d’applications** s’affiche dans le nœud **État d’installation** du Centre logiciel.  

> [!Note]  
> La prise en charge de l’expérience utilisateur du site web du catalogue d’applications se termine avec la première mise à jour publiée après le 1er juin 2018. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, créez une stratégie personnalisée de paramètres d’appareils clients sur le nœud **Paramètres clients** de l’espace de travail **Administration**.  

2. Sélectionnez le groupe **Centre logiciel**.  

3. Pour **Paramètres du Centre logiciel**, cliquez sur **Personnaliser**.  

4. Activez l’option **Masquer le lien du site web du catalogue d’applications dans le Centre logiciel**.   

Pour plus d’informations sur les paramètres client, consultez [Configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).




## <a name="filter-automatic-deployment-rules-by-software-update-architecture"></a>Filtrer les règles de déploiement automatique par architecture de mise à jour logicielle
 <!--1322266-->
Vous pouvez désormais filtrer les règles de déploiement automatique pour exclure les architectures comme Itanium et ARM64.

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Mises à jour logicielles** et sélectionnez **Règles de déploiement automatique**. Sur le ruban, sélectionnez **Créer une règle de déploiement automatique**.  

2. Renseignez les paramètres appropriés dans l’onglet **Général** et l’onglet **Paramètres de déploiement**.  

3. Dans l’onglet **Mises à jour logicielles**, sélectionnez **Architecture**, puis cliquez sur **Éléments à rechercher** dans les **critères de recherche**.  

4. Sélectionnez les architectures à inclure dans la règle de déploiement automatique.  

5. Cliquez sur **Suivant** et poursuivez la création de la règle de déploiement automatique.  

> [!IMPORTANT]  
> N’oubliez pas qu’il existe des applications 32 bits (x86) et des composants exécutés sur des systèmes 64 bits (x64). Sauf si vous êtes certain de ne pas besoin de x86, activez-le aussi lorsque vous choisissez x64.  

### <a name="known-issues"></a>Problèmes connus
Après avoir ajouté les critères de l’architecture, la page des propriétés de la règle de déploiement automatique affiche **Titre** dans les critères de recherche. La règle de déploiement automatique fonctionne toujours comme prévu et sélectionne les mises à jour logicielles correctes. Toutefois, vous ne pouvez pas inclure à la fois les critères **Architecture** et **Titre** pour l’instant. <!--512634,512632-->



## <a name="improvements-to-os-deployment"></a>Améliorations apportées au déploiement de système d’exploitation
Les améliorations suivantes, inspirées notamment par vos commentaires User Voice, ont été apportées au déploiement des systèmes d’exploitation.  

 - [Masquer les données sensibles stockées dans des variables de séquence de tâches](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed) : dans l’étape [Définir la variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable), sélectionnez la nouvelle option **Ne pas afficher cette valeur**. Par exemple, lorsque vous spécifiez un mot de passe.<!--1358330--> Les comportements suivants s’appliquent lorsque vous activez cette option :
   - La valeur de la variable n’est pas affichée dans le fichier smsts.log.
   - La console Configuration Manager et le fournisseur SMS traitent cette valeur de la même façon que d’autres secrets comme les mots de passe.
   - La valeur n’est pas incluse lorsque vous exportez la séquence de tâches.
   - L’éditeur de la séquence de tâches ne lit pas cette valeur lorsque vous modifiez l’étape. Tapez à nouveau la valeur entière pour apporter des modifications.

   > [!Important]  
   > Les variables et leurs valeurs sont enregistrées avec la séquence de tâches en tant que XML et obscurcies dans la base de données. Lorsque le client demande une stratégie de séquence de tâches à partir du point de gestion, elle est chiffrée en transit et lorsqu’elle est stockée sur le client. Toutefois, toutes les valeurs des variables sont en texte brut dans l’environnement de la séquence de tâches dans la mémoire pendant l’exécution sur le client. Si la séquence de tâches inclut une étape pour extraire la valeur de la variable, cette sortie est au format texte brut. Ce comportement nécessite une action explicite par l’administrateur afin d’inclure une étape de ce type dans la séquence de tâches. 


 - [Masquer le nom du programme pendant l’étape Exécuter la commande d’une séquence de tâches](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15282795-secret-task-sequence-variable-value-exposed) : pour empêcher l’affichage ou la consignation de données potentiellement sensibles, définissez la variable de la séquence de tâches **OSDDoNotLogCommand** sur `TRUE`. Cette variable masque le nom du programme dans le fichier smsts.log au cours de l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) d’une séquence de tâches. <!--1358493-->  



## <a name="improvements-to-the-configuration-manager-console"></a>Améliorations apportées à la console Configuration Manager
- Les informations de l’utilisateur principal sont désormais visibles lorsque vous affichez les membres d’une collection sous **Ressources et conformité**, **Collections d’appareils**.<!--510252-->  



## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
