---
title: Surveiller la réplication
titleSuffix: Configuration Manager
description: Apprenez à surveiller l’infrastructure et les opérations dans Configuration Manager à l’aide de l’espace de travail Surveillance dans la console.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7a9fcf06630c76fc3e1123fa56861c4de224521
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129372"
---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour surveiller l’infrastructure et les opérations dans System Center Configuration Manager, utilisez l’espace de travail **Surveillance** dans la console Configuration Manager.  

> [!NOTE]  
>  À noter l'exception Migration de cet emplacement, qui est contrôlée directement dans le nœud **Migration** de l'espace de travail **Administration** . Pour plus d'informations, voir [Opérations de migration vers System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 En plus d’utiliser la console Configuration Manager pour la surveillance, vous pouvez utiliser les rapports Configuration Manager ou consulter les fichiers journaux Configuration Manager des composants Configuration Manager. Pour plus d’informations sur les rapports, consultez [Génération de rapports dans System Center Configuration Manager](../../../core/servers/manage/reporting.md). Pour plus d’informations sur les fichiers journaux, consultez [Fichiers journaux dans System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 Lorsque vous surveillez des sites, recherchez des signes indiquant des problèmes qui vous obligent à prendre des mesures. Par exemple :  

-   File d'attente de fichiers sur les serveurs de site et les systèmes de site.  

-   Messages d'état indiquant une erreur ou un problème.  

-   Échec de communication intrasite.  

-   Messages d'erreur et d'avertissement dans le journal d'événements système sur les serveurs.  

-   Messages d'erreur et d'avertissement dans le journal des erreurs Microsoft SQL Server.  

-   Sites ou clients n'ayant rien rapporté depuis longtemps.  

-   Réponse lente depuis la base de données SQL Server.  

-   Signe de défaillance matérielle.  

Pour réduire les risques de défaillance d'un site, si les tâches de contrôle révèlent des signes de problèmes, recherchez la source du problème et réparez-le dès que possible.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Surveiller les tâches de gestion courantes pour Configuration Manager  
 Configuration Manager assure une surveillance intégrée à partir de la console Configuration Manager. Vous pouvez surveiller de nombreuses tâches, dont celles liées aux mises à jour logicielles, à la gestion de l'alimentation et au déploiement de contenu au sein de votre hiérarchie.  

 Utilisez les informations suivantes pour vous aider à surveiller les tâches Configuration Manager courantes :  

 **Alertes**  
   Consultez [Surveiller les alertes](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) dans [Utiliser des alertes et le système d’état pour System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Paramètres de conformité**  
   Consultez [Comment surveiller les paramètres de compatibilité dans System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md).  

 **Déploiement de contenu**  
   Pour obtenir des informations générales sur la surveillance du contenu, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

Pour plus d'informations sur la surveillance de types spécifiques de déploiement de contenu :
-   Pour surveiller les applications, consultez [Surveiller des applications avec System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   Pour surveiller les packages et programmes, consultez Comment gérer des packages et des programmes dans [Packages et programmes dans System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   Consultez [Comment surveiller Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Surveiller la gestion de l'alimentation**  
 Consultez [Comment surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Surveiller le contrôle de logiciels**  
Consultez [Surveiller l’utilisation des applications avec le contrôle de logiciel dans System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Surveiller les mises à jour logicielles**  
 Consultez [Surveiller les mises à jour logicielles dans System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md).  


##  <a name="BKMK_MonitorInfrastructure"></a> Surveiller l’infrastructure de la hiérarchie pour Configuration Manager  
Configuration Manager fournit plusieurs méthodes pour surveiller l’état et les opérations de votre hiérarchie. Vous pouvez vérifier l'état du système des sites de la hiérarchie, surveiller la réplication intersite à partir d'une hiérarchie de site ou une vue géographique, surveiller les liens de réplication entre sites pour la réplication de base de données et utiliser l'outil Analyseur de lien de réplication pour corriger les problèmes de réplication.  

###  <a name="BKMK_SH_Node"></a> À propos du nœud Hiérarchie de site  
Le nœud **Hiérarchie de site** de l’espace de travail **Surveillance** fournit une vue d’ensemble de votre hiérarchie Configuration Manager et des liens intersites. Vous pouvez utiliser deux vues :  

-   **Diagramme hiérarchique** : Cette vue affiche votre hiérarchie comme une carte topologique qui a été simplifiée pour afficher uniquement les informations vitales.  

-   **Vue géographique** : Cette vue affiche vos sites sur une carte géographique présentant les emplacements des sites que vous configurez.  

Utilisez le nœud **Hiérarchie de site** pour surveiller l'intégrité de chaque site ainsi que les liens de réplication intersites et leur relation à des facteurs externes, comme un emplacement géographique.  

Étant donné que l’état d’un site et l’état des liens intersites sont répliqués en tant que données de site et non en tant que données globales, lorsque vous connectez votre console Configuration Manager à un site principal enfant, vous ne pouvez pas afficher l’état du site ou du lien d’autres sites principaux ou de leurs sites secondaires enfants. Par exemple, dans une hiérarchie comportant plusieurs sites principaux, lorsque votre console Configuration Manager se connecte à un site principal, vous pouvez afficher l’état des sites secondaires enfants, du site principal et du site d’administration centrale, mais vous ne pouvez pas voir l’état d’autres nœuds de la hiérarchie sous le site d’administration centrale.  

 Utilisez la commande **Configurer les paramètres** pour contrôler la manière dont est rendu l'affichage de la hiérarchie du site. Lorsque votre console Configuration Manager est connectée à un seul site, les configurations que vous effectuez au niveau du nœud **Hiérarchie de site** sont répliquées sur tous les autres sites.  

#### <a name="hierarchy-diagram"></a>Diagramme hiérarchique  
 Le diagramme hiérarchique affiche vos sites dans une carte topologique. Dans cette vue, vous pouvez sélectionner un site et afficher un résumé des messages d'état à partir de ce site, effectuer une exploration pour afficher des messages d'état, et accéder à la boîte de dialogue **Propriétés** des sites.  

 En outre, vous pouvez suspendre le pointeur de souris sur un site ou un lien de réplication entre sites pour afficher l'état de niveau élevé pour cet objet. Étant donné que l’état des liens de réplication n’est pas répliqué globalement, dans une hiérarchie comportant plusieurs sites principaux, vous devez connecter votre console Configuration Manager au site d’administration centrale pour afficher les détails du lien de réplication entre tous les sites.  

 Les options suivantes modifient le diagramme hiérarchique :  

-   **Groupes** : vous pouvez configurer le nombre de sites principaux et de sites secondaires qui déclenchent un changement de l'affichage du diagramme hiérarchique, celui-ci combinant les sites dans un seul objet. Lorsque des sites sont combinés dans un seul objet, vous voyez le nombre total de sites et un cumul de niveau élevé des messages d'état et de l'état du site. Les configurations de groupe n'affectent pas la vue géographique.  

-   **Sites favoris** : Vous pouvez spécifier des sites individuels comme sites favoris. Une icône en forme d'étoile identifie un site favori dans le diagramme hiérarchique. Les sites favoris ne sont pas combinés à d'autres sites lorsque vous avez utilisé des groupes et ils sont toujours affichés individuellement.  

#### <a name="geographical-view"></a>Vue géographique  
 La vue géographique affiche l'emplacement de chaque site sur une carte géographique. Seuls les sites que vous configurez avec un emplacement sont affichés. Lorsque vous sélectionnez un site dans cette vue, les liens de réplication vers des sites parents ou enfants sont affichés. Contrairement à l'affichage du diagramme hiérarchique, vous ne pouvez pas afficher les détails du lien de réplication ou du message d'état de site dans cette vue.  

> [!NOTE]  
>  Pour utiliser la vue géographique, Internet Explorer doit être installé sur l’ordinateur auquel se connecte votre console Configuration Manager et cet ordinateur doit pouvoir accéder à Bing Maps à l’aide du protocole HTTP.  

L'option suivante modifie la vue géographique.  

-   **Emplacement de site** : vous pouvez spécifier un emplacement géographique pour chaque site. L'emplacement peut être spécifié sous forme de nom de rue, de lieu, par exemple un nom de ville, ou par des coordonnées de latitude et de longitude. Par exemple, pour indiquer la latitude et la longitude de Redmond Washington, vous devez spécifier **47 40 26.3572 Nord 122 7 17.4432 Ouest** pour l'emplacement du site. Il n'est pas nécessaire de spécifier le symbole des degrés, minutes ou secondes de longitude ou de latitude. Configuration Manager utilise Bing Maps pour afficher l’emplacement de la vue géographique. Cela vous permet d'afficher votre hiérarchie par rapport à un emplacement géographique, ce qui peut fournir des informations sur des problèmes régionaux susceptibles d'affecter des sites spécifiques ou la réplication intersite.  

     Lorsque vous spécifiez un emplacement, vous pouvez utiliser la zone **Emplacement** pour rechercher un site spécifique dans votre hiérarchie. Après avoir sélectionné le site, entrez l'emplacement sous forme de nom de ville ou d'adresse postale dans la colonne **Emplacement** . Configuration Manager utilise Bing Maps pour résoudre l’emplacement.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> Comment surveiller des liens de réplication de la base de données et l’état de la réplication  
 En plus des détails approfondis accessibles à partir du nœud **Hiérarchie de site** de l’espace de travail **Surveillance** , vous pouvez également surveiller les détails de la réplication de la base de données quand vous utilisez le nœud **Réplication de la base de données** de l’espace de travail **Surveillance** . À partir de **Réplication de la base de données**, vous pouvez surveiller l’état des liens de réplication entre les sites, ainsi que les détails de l’initialisation et de la réplication des groupes de réplication sur le site auquel votre console Configuration Manager est connectée.  

> [!TIP]  
>  Un nœud **Réplication de la base de données** apparaît également sous le nœud **Configuration de la hiérarchie** dans l'espace de travail **Administration** , mais vous ne pouvez pas afficher l'état de réplication des liens de réplication de la base de données à partir de cet emplacement.  

####  <a name="BKMK_MonitorReplicationLinks"></a> État des liens de réplication  
La réplication de base de données entre sites implique la réplication de plusieurs ensembles d'informations, appelés groupes de réplication. Chaque groupe de réplication est répliqué avec différentes priorités de réplication. Par défaut, les données contenues dans un groupe de réplication et la fréquence de réplication ne peuvent pas être modifiées.  

 Lorsqu'un lien de réplication est actif et ne présente pas un état en échec ou détérioré, tous les groupes de réplication répliquent dans un délai raisonnable. Si un ou plusieurs groupes de réplication ne parviennent pas à répliquer dans le délai prévu, le lien s'affiche comme détérioré. Les liens détériorés continuent de fonctionner, mais envisagez de les surveiller pour vous assurer qu'ils repassent à l'état actif ou vérifiez-les pour vous assurer qu'ils ne se détériorent pas davantage et que la réplication n'échoue pas.  

 Pour chaque lien de réplication, vous pouvez spécifier le nombre de tentatives de réplication d’un groupe de réplication qui ne parvient pas à terminer la réplication avant que l’état du lien ne soit défini comme détérioré ou en échec. Même si un seul groupe de réplication ne parvient pas à se répliquer alors que les autres le font correctement, l'état du lien est défini comme détérioré ou en échec car un groupe de réplication ne parvient pas à se répliquer à l'issue du nombre de tentatives spécifié. Pour plus d’informations sur les seuils de réplication, consultez la section [Seuils de réplication de la base de données](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) dans [Transfert de données entre sites dans System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

 Utilisez les informations dans le tableau suivant pour comprendre l'état des liens de réplication susceptibles de nécessiter davantage de recherches.  

|Description du lien|Informations complémentaires|  
|----------------------|----------------------|  
|**Le lien est actif**|Aucun problème n'a été détecté et la communication dans le lien est en cours.|  
|**Le lien est dégradé**|La réplication est fonctionnelle, mais au moins un objet ou groupe de réplication a été retardé. Surveillez les liens dans cet état et consultez les informations depuis les deux sites sur le lien pour obtenir des indications sur l'éventualité d'un échec du lien.<br /><br /> Un lien peut également afficher un état dégradé lorsque le site qui reçoit les données répliquées ne peut pas valider rapidement les données dans la base de données. Cela peut se produire lors de la réplication de volumes importants de données. Par exemple, si vous déployez une mise à jour logicielle sur un grand nombre d'ordinateurs, le site parent sur le lien peut prendre un certain temps pour traiter le volume de données répliquées. Un délai de traitement sur le site parent peut entraîner la dégradation de l'état du lien jusqu'à ce que le site parent puisse traiter correctement les données en attente.|  
|**Le lien a échoué**|La réplication ne fonctionne pas. Il est possible qu'un lien de réplication puisse être rétabli sans action supplémentaire. Vous pouvez utiliser l'Analyseur de lien de réplication pour examiner et corriger la réplication sur ce lien.<br /><br /> Cet état peut également indiquer un problème du réseau physique entre le site parent et enfant sur le lien de réplication.|  

 Pendant le processus de mise à niveau d'un site parent vers un nouveau Service Pack, l'état du lien s'affiche comme étant actif si vous l'affichez à partir du site enfant. Après la mise à niveau et jusqu'à la mise à niveau du site enfant vers le même Service Pack que le site parent, l'état du lien s'affiche comme étant actif depuis le site parent et comme étant en cours de configuration depuis le site enfant.  

####  <a name="BKMK_MonitorReplicationStatus"></a> État de la réplication  
 Vous pouvez utiliser le nœud **Réplication de la base de données** dans l'espace de travail **Surveillance** pour afficher l'état de réplication d'un lien de réplication et afficher des détails sur la base de données de site sur chaque site se trouvant sur le lien de réplication. Vous pouvez également afficher des détails sur les groupes de réplication. Pour afficher les détails, sélectionnez un lien de réplication, puis sélectionnez l'onglet correspondant à l'état de réplication à afficher. Le tableau suivant fournit des détails sur les différents onglets relatifs à l’état de la réplication.  

 **Résumé**  
 Permet d'afficher des informations de haut niveau sur la réplication des données de site et des données globales entre les deux sites sur un lien.  

 Vous pouvez également cliquer sur **Afficher les rapports des données de l'historique du trafic** pour afficher un rapport avec les détails sur la bande passante de réseau utilisée par la réplication sur l'intégralité du lien de réplication.  

 **Site parent**  
 Pour le site parent sur un lien de réplication, affichez les détails sur la base de données, notamment :  

-   Ports de pare-feu pour SQL Server  

-   Espace disque disponible  

-   Emplacements de fichiers de base de données  

-   Certificats  

**Site enfant**  
 Pour le site enfant sur un lien de réplication, affichez les détails sur la base de données, notamment :  

-   Ports de pare-feu pour SQL Server  

-   Espace disque disponible  

-   Emplacements de fichiers de base de données  

-   Certificats  

**Détail de l’initialisation**    
 Permet d'afficher l'état d'initialisation des groupes de réplication qui répliquent sur l'intégralité du lien de réplication. Ces informations peuvent vous aider à identifier quand l'initialisation des données de réplication est en cours ou en échec.  

 De plus, vous pouvez utiliser ces informations pour identifier quand un site peut se trouver en mode d'interopérabilité. Le mode d’interopérabilité se produit lorsque le site enfant n’exécute pas la même version de Configuration Manager que le site parent.  

**Détail de la réplication**    
 Permet d'afficher l'état de réplication de chaque groupe de réplication qui réplique sur l'intégralité du lien. Utilisez ces informations pour aider à identifier des problèmes ou des retards pour la réplication de données spécifiques et pour aider à déterminer les seuils de réplication de la base de données appropriés pour ce lien. Pour plus d’informations sur les seuils de réplication de la base de données, consultez la section [Seuils de réplication de la base de données](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) dans [Transfert de données entre sites dans System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

> [!TIP]  
>  Les groupes de réplication de données de site sont envoyés uniquement à partir du site enfant vers le site parent. Les groupes de réplication pour les données globales sont répliqués dans les deux directions.  

###  <a name="BKMK_RLA"></a> À propos de l'analyseur de lien de réplication  
 Configuration Manager inclut l’**analyseur de lien de réplication** que vous utilisez pour analyser et réparer les problèmes de réplication. Vous pouvez utiliser l'analyseur de lien de réplication pour corriger les échecs de lien de réplication en cas d'échec de la réplication et lorsque la réplication cesse de fonctionner mais n'a pas encore été signalée comme ayant échoué. L’analyseur de lien de réplication peut être utilisé pour corriger les problèmes de réplication entre les ordinateurs suivants dans la hiérarchie Configuration Manager (la direction de l’échec de réplication n’a aucune importance) :  

-   Entre un serveur de site et le serveur de base de données de site.  

-   Entre un serveur de base de données de site des sites et un autre ordinateur de base de données de site des sites (réplication intersite).  

Vous pouvez exécuter l’analyseur de lien de réplication dans la console Configuration Manager ou à partir d’une invite de commandes :  

-   Pour exécuter la console Configuration Manager : dans l’espace de travail **Surveillance**, cliquez sur le nœud **Réplication de la base de données**, sélectionnez le lien de réplication que vous souhaitez analyser, puis, dans le groupe **Réplication de la base de données**, dans l’onglet **Accueil**, sélectionnez **Analyseur de lien de réplication**.  

-   Pour l’exécuter à l’invite de commandes, entrez la commande suivante : **%chemin%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;nom de domaine complet du serveur de site source\> &lt;nom de domaine complet du serveur de site de destination\>**  

Lorsque vous exécutez l'analyseur de lien de réplication, celui-ci détecte les problèmes à l'aide d'une série de règles et contrôles de diagnostic. Lorsque l'outil est exécuté, vous voyez les problèmes identifiés par celui-ci. Des instructions pour résoudre un problème, lorsqu'elles sont connues, sont affichées. Si l'analyseur de lien de réplication peut corriger automatiquement un problème, cette option vous est présentée. Une fois l'analyseur de lien de réplication terminé, celui-ci enregistre les résultats dans le rapport suivant basé sur XML et un fichier journal sur le bureau de l'utilisateur qui exécute l'outil :  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

Lorsque l'analyseur de lien de réplication s'exécute, il arrête les services suivants pendant la correction des problèmes, puis il redémarre ces services une fois la correction terminée :  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

Si l'analyseur de lien de réplication ne parvient pas à terminer la correction, vérifiez le serveur de site et redémarrez ces services s'ils sont arrêtés.  

Les actions de recherche et de correction ayant réussi et celles ayant échoué sont consignées pour fournir des détails supplémentaires qui ne sont pas présentés dans l'interface de l'outil.  

**Conditions requises pour utiliser l'analyseur de lien de réplication :**  

-   Le compte que vous utilisez pour exécuter l'analyseur de lien de réplication doit disposer de droits d'administrateur local sur chaque ordinateur qui est impliqué dans le lien de réplication. Le compte ne nécessite pas de rôle de sécurité d'administration basé sur des rôles spécifiques. Par conséquent, un utilisateur administratif disposant d’un accès au nœud **Réplication de la base de données** peut exécuter l’outil dans la console Configuration Manager, ou un administrateur système possédant des droits suffisants vers chaque ordinateur peut exécuter l’outil à une invite de commandes.  

-   Le compte que vous utilisez pour exécuter l'analyseur de lien de réplication doit disposer de droits d'administrateur système sur chaque base de données SQL Server qui est impliquée dans le lien de réplication.  

**Problèmes connus de l’analyseur de lien de réplication :**  

-   Avec la version 1511 de System Center Configuration Manager, l’analyseur de lien de réplication génère des erreurs de certificat SQL Server Service Broker pour les sites principaux mis à niveau à partir de System Center 2012 Configuration Manager. Ces erreurs sont dues à des modifications des noms des certificats introduits dans la version 1511 pour lesquels l’analyseur de lien de réplication n’a pas encore été mis à jour. Vous pouvez ignorer ces erreurs sans risque.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Procédures de surveillance de la réplication de la base de données  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>Pour surveiller l'état de réplication de base de données entre sites de niveau élevé    
1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , cliquez sur **Hiérarchie de site** pour ouvrir la vue **Diagramme hiérarchique** .  

3.  Suspendre brièvement le pointeur de souris sur la ligne entre les deux sites pour afficher l'état de réplication globale et des données de site pour ces sites.  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>Pour surveiller l'état de réplication d'un lien de réplication    
1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , cliquez sur **Réplication de la base de données**, puis sélectionnez le lien de réplication pour le lien que vous souhaitez surveiller. Ensuite, dans l'espace de travail, sélectionnez l'onglet approprié pour afficher différents détails sur l'état de la réplication de ce lien.  
