---
title: Liste de contrôle pour la version 1902
titleSuffix: Configuration Manager
description: Découvrez les actions à entreprendre avant d’effectuer la mise à jour vers Configuration Manager version 1902.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b87ac054-9b37-4725-a3f3-2340cfb10bff
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 801a4819e4bfc9c0f18b87915ea0969b0aa60dc3
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497872"
---
# <a name="checklist-for-installing-update-1902-for-configuration-manager"></a>Liste de contrôle pour l’installation de la mise à jour 1902 de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous utilisez l’édition Current Branch de Configuration Manager, vous pouvez installer la mise à jour dans la console de la version 1902 pour mettre à jour votre hiérarchie à partir d’une version antérieure. <!-- baseline only statement:-->(Comme la version 1902 est également disponible en tant que [support de base de référence](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), vous pouvez utiliser le support d’installation pour installer le premier site d’une nouvelle hiérarchie.)

Pour obtenir la mise à jour de la version 1902, vous devez utiliser un point de connexion de service sur le site de niveau supérieur de votre hiérarchie. Ce rôle de système de site peut être en mode en ligne ou hors connexion. Une fois que votre hiérarchie a téléchargé la mise à jour auprès de Microsoft, recherchez-la dans la console. Dans l’espace de travail **Administration**, sélectionnez le nœud **Mises à jour et maintenance**.

-   Quand la mise à jour est répertoriée comme **disponible**, elle est prête à être installée. Avant d’installer la version 1902, consultez les informations suivantes sur l’[installation de la mise à jour 1902](#about-installing-update-1902) et la [liste de contrôle](#checklist) pour connaître les configurations à effectuer avant de démarrer la mise à jour.

-   Si la mise à jour s’affiche en indiquant **Téléchargement** et que rien ne change, recherchez les erreurs dans les fichiers **hman.log** et **dmpdownloader.log**.

    -   Le fichier dmpdownloader.log peut indiquer que le processus dmpdownloader attend un intervalle avant de rechercher les mises à jour. Pour redémarrer le téléchargement des fichiers de redistribution de la mise à jour, redémarrez le service **SMS_Executive** sur le serveur de site.

    -   Un autre problème courant de téléchargement se produit lorsque les paramètres du serveur proxy empêchent les téléchargements à partir de http://silverlight.dlservice.microsoft.com, http://download.microsoft.com, et/ou http://go.microsoft.com.

Pour plus d’informations sur l’installation des mises à jour, consultez [Mises à jour et maintenance dans la console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Pour plus d’informations sur les versions actuelles de l’édition Current Branch, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#bkmk_Baselines).



## <a name="about-installing-update-1902"></a>À propos de l’installation de la mise à jour 1902

#### <a name="sites"></a>Sites
Vous devez installer la mise à jour 1902 sur le site de niveau supérieur de votre hiérarchie. Démarrez l’installation à partir de votre site d’administration centrale ou de votre site principal autonome. Une fois la mise à jour installée sur le site de niveau supérieur, les sites enfants ont le comportement de mise à jour suivant :

-   Les sites principaux enfants installent automatiquement la mise à jour quand le site d’administration centrale a fini de l’installer. Vous pouvez utiliser des fenêtres de service pour spécifier à quel moment un site installe la mise à jour. Pour plus d’informations, consultez [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).

-   Mettez à jour manuellement chaque site secondaire à partir de la console Configuration Manager, une fois que le site parent principal a fini d’installer la mise à jour. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.

#### <a name="site-system-roles"></a>Rôles système de site
Quand un serveur de site installe la mise à jour, il met à jour automatiquement l’ensemble des rôles de système de site. Ces rôles se trouvent sur le serveur de site ou sont installés sur des serveurs distants. Avant d’installer la mise à jour, vérifiez que chaque serveur de système de site remplit les prérequis pour la nouvelle version de mise à jour.

#### <a name="configuration-manager-consoles"></a>Consoles Configuration Manager   
La première fois que vous utilisez une console Configuration Manager à l’issue de la mise à jour, vous êtes invité à mettre à jour cette console. Vous pouvez également exécuter le programme d’installation de Configuration Manager sur l’ordinateur qui héberge la console, et choisir l’option de mise à jour de la console. Installez la mise à jour sur la console dès que possible. Pour plus d’informations, consultez [Installer la console Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).

> [!IMPORTANT]  
> Lorsque vous installez une mise à jour sur le site d’administration centrale, tenez compte des limitations suivantes et des retards qui se produisent jusqu’à ce que tous les sites principaux enfants aient également terminé l’installation de la mise à jour :    
> - La **mise à niveau des clients** ne démarre pas. Cela comprend la mise à jour automatique des clients et des clients en préproduction. En outre, il n’est pas possible de mettre en production les clients en préproduction tant que le dernier site n’a pas terminé l’installation de la mise à jour. Après l’installation de la mise à jour sur le dernier site, la mise à niveau des clients commence, en fonction de vos options de configuration.   
> - Les **nouvelles fonctionnalités** que vous activez avec la mise à jour ne sont pas disponibles. L’objectif est d’éviter l’envoi de la réplication de données associées à cette fonctionnalité à un site qui n’a pas encore installé la prise en charge de cette fonctionnalité. Après l’installation de la mise à jour sur tous les sites principaux, la fonctionnalité sera utilisable.   
> - Les **liens de réplication** entre le site d’administration centrale et les sites principaux enfants apparaissent comme non mis à niveau. Cela se présente, dans l’état d’installation du pack de mise à jour, sous la forme d’un état Terminé avec un avertissement pour l’initialisation de la surveillance de la réplication. Dans le nœud Surveillance de la console, cela se présente sous l’état *Lien en cours de configuration*.


## <a name="checklist"></a>Liste de contrôle

#### <a name="all-sites-run-a-supported-version-of-configuration-manager"></a>Tous les sites exécutent une version prise en charge de Configuration Manager  
Chaque serveur de site de la hiérarchie doit exécuter la même version de Configuration Manager pour que vous puissiez démarrer l’installation de la mise à jour 1902. Pour effectuer la mise à jour vers la version 1902, vous devez utiliser les versions 1802, 1806 ou 1810.

#### <a name="review-the-status-of-your-product-licensing"></a>Vérifier l’état de votre licence de produit 
Vous devez avoir un contrat SA (Software Assurance) actif ou des droits d’abonnement équivalents pour installer cette mise à jour. Quand vous mettez à jour le site, la page **Licences** propose une option qui permet de confirmer la **Date d’expiration de la Software Assurance**.

Cette valeur est facultative. Vous pouvez l’utiliser comme rappel de la date d’expiration de votre licence. Cette date est visible lorsque vous installez des mises à jour ultérieures. Vous avez peut-être déjà spécifié cette valeur durant la configuration ou l’installation d’une mise à jour. Vous pouvez également spécifier cette valeur dans la console Configuration Manager. Dans l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**. Sélectionnez **Paramètres de hiérarchie** dans le ruban, puis passez à l’onglet **Licences**.

Pour plus d’informations, consultez [Licences et branches](/sccm/core/understand/learn-more-editions).

#### <a name="review-microsoft-net-versions"></a>Vérifier les versions de Microsoft .NET 
Si, quand un site installe cette mise à jour, la configuration minimale requise de .NET Framework 4.5 n’est pas installée, Configuration Manager installe automatiquement .NET Framework 4.5.2. Quand ce prérequis n’est pas déjà installé, le site l’installe sur chaque serveur qui héberge l’un des rôles de système de site suivants :

-   Point de gestion
-   point de connexion de service
-   Point proxy d'inscription
-   Point d'inscription

Cette installation peut mettre le serveur de système de site en état d’attente de redémarrage, et signaler des erreurs sur l’Afficheur des messages d’état du composant Configuration Manager. En outre, des applications .NET sur le serveur peuvent présenter des défaillances aléatoires jusqu’au redémarrage du serveur.

Pour plus d’informations, consultez  [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

#### <a name="review-the-version-of-the-windows-adk-for-windows-10"></a>Vérifier la version de Windows ADK pour Windows 10
La version de Windows ADK (Kit de déploiement et d’évaluation Windows) pour Windows 10 doit être prise en charge pour Configuration Manager version 1902. Pour plus d’informations sur les versions prises en charge de Windows ADK, consultez [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk). Si vous devez mettre à jour Windows ADK, faites-le avant de commencer la mise à jour de Configuration Manager. En procédant dans cet ordre, vous avez la garantie que les images de démarrage par défaut sont automatiquement mises à jour vers la dernière version de Windows PE. Mettez à jour manuellement les images de démarrage personnalisées après la mise à jour du site.

Si vous mettez à jour le site avant de mettre à jour Windows ADK, consultez [Mettre à jour les points de distribution avec l’image de démarrage](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

#### <a name="review-sql-server-native-client-version"></a>Vérification de la version SQL Server Native Client
Une version minimale de SQL Server 2012 Native Client prenant en charge TLS 1.2 doit être installée. Pour plus d'informations, consultez la [Liste des vérifications de la configuration requise](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client).

#### <a name="review-the-site-and-hierarchy-status-for-unresolved-issues"></a>Examiner l’état du site et de la hiérarchie pour rechercher les problèmes non résolus 
Une mise à niveau de site peut échouer en raison de l’existence de problèmes opérationnels. Avant de mettre un site à jour, résolvez tous les problèmes opérationnels sur les systèmes suivants :  
- Serveur de site  
- Serveur de bases de données du site  
- Rôles de système de site distant sur d’autres serveurs   

Pour plus d’informations, consultez  [Utiliser des alertes et le système d’état](/sccm/core/servers/manage/use-alerts-and-the-status-system).

#### <a name="review-file-and-data-replication-between-sites"></a>Vérifier la réplication des fichiers et des données entre les sites   
Vérifiez que la réplication des fichiers et des bases de données entre les sites est opérationnelle et active. Des retards ou backlogs dans ces domaines peuvent perturber ou empêcher la mise à jour. Pour la réplication de la base de données, vous pouvez utiliser l’Analyseur de lien de réplication pour faciliter la résolution des problèmes avant de commencer la mise à jour.

Pour plus d’informations, consultez [À propos de l’analyseur de lien de réplication](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA).

#### <a name="install-all-applicable-critical-windows-updates"></a>Installer toutes les mises à jour Windows critiques applicables
Avant d’installer une mise à jour pour Configuration Manager, installez les mises à jour critiques du système d’exploitation pour chaque système de site applicable. Ces serveurs incluent le serveur de site, le serveur de base de données du site et les rôles de système de site distants. Si vous installez une mise à jour qui nécessite un redémarrage, redémarrez les serveurs concernés avant de commencer la mise à niveau.

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Désactiver les réplicas de base de données pour les points de gestion des sites principaux   
Configuration Manager ne peut pas mettre à jour correctement un site principal ayant un réplica de base de données activé pour les points de gestion. Avant d’installer une mise à jour pour Configuration Manager, désactivez la réplication de la base de données.

Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

#### <a name="set-sql-server-alwayson-availability-groups-to-manual-failover"></a>Définir un basculement manuel pour les groupes de disponibilité AlwaysOn de SQL Server   
Si vous utilisez un groupe de disponibilité, vérifiez qu’il est défini sur le basculement manuel avant de commencer l’installation de la mise à jour. Une fois le site mis à jour, vous pouvez restaurer le basculement automatique. Pour plus d’informations, consultez  [SQL Server AlwaysOn pour une base de données de site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

#### <a name="disable-site-maintenance-tasks-at-each-site"></a>Désactiver les tâches de maintenance de site sur chaque site
Avant d’installer la mise à jour, désactivez toutes les tâches de maintenance de site qui peuvent s’exécuter pendant le processus de mise à jour. Par exemple, mais sans s’y limiter :

-   Serveur de site de sauvegarde
-   Supprimer les anciennes opérations du client
-   Supprimer les données de découverte anciennes

Si une tâche de maintenance de base de données du site s’exécute pendant l’installation de la mise à jour, celle-ci peut échouer. Avant de désactiver une tâche, enregistrez sa planification pour pouvoir restaurer sa configuration une fois la mise à jour installée.

Pour plus d’informations, consultez  [Tâches de maintenance](/sccm/core/servers/manage/maintenance-tasks)  et [Référence des tâches de maintenance](/sccm/core/servers/manage/reference-for-maintenance-tasks).

#### <a name="temporarily-stop-any-antivirus-software"></a>Arrêter temporairement tout logiciel antivirus 
Avant de mettre à jour un site, arrêtez les logiciels antivirus sur les serveurs Configuration Manager. <!--SMS.503481--> 

#### <a name="create-a-backup-of-the-site-database"></a>Créer une sauvegarde de la base de données du site 
Avant de mettre à jour un site, sauvegardez la base de données du site sur le site d’administration centrale et les sites principaux. Cette opération garantit l’accès à une sauvegarde réussie en cas de reprise d’activité après sinistre.

Pour plus d’informations, consultez  [Sauvegarde et récupération](/sccm/protect/understand/backup-and-recovery).

#### <a name="plan-for-client-piloting"></a>Planifier le pilotage du client   
Quand vous installez une mise à jour qui affecte le client, vous pouvez la tester en mode préproduction avant de procéder au déploiement et à la mise à niveau de votre client actif. Pour tirer parti de cette option, vous devez configurer votre site pour qu’il prenne en charge les mises à niveau automatiques pour la préproduction avant de commencer l’installation de la mise à jour.

Pour plus d’informations, consultez  [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients)  et [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="plan-to-use-service-windows"></a>Planifier l’utilisation des fenêtres de service   
Pour définir une période au cours de laquelle les mises à jour d’un serveur de site peuvent être installées, utilisez les fenêtres de service. Elles vous permettent de contrôler le moment où les sites de votre hiérarchie installent la mise à jour. Pour plus d’informations, consultez  [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).

#### <a name="review-supported-extensions"></a>Vérifier les extensions prises en charge
<!--SCCMdocs#587-->
Si vous étendez Configuration Manager avec d’autres produits provenant de Microsoft ou de partenaires Microsoft, vérifiez que ces produits prennent en charge la version 1902. Demandez cette information au fournisseur du produit. Par exemple, consultez les [notes de publication](/sccm/mdt/release-notes) de Microsoft Deployment Toolkit.

#### <a name="run-the-setup-prerequisite-checker"></a>Exécuter l’outil de vérification des prérequis d’installation   
Quand la mise à jour est répertoriée dans la console comme **Disponible**, vous pouvez exécuter indépendamment l’outil de vérification des prérequis avant d’installer la mise à jour. (Quand vous installez la mise à jour sur le site, l’outil de vérification des prérequis s’exécute à nouveau.)

Pour exécuter une vérification des prérequis à partir de la console, accédez à l’espace de travail **Administration**, puis sélectionnez **Mises à jour et maintenance**. Sélectionnez le package de mise à jour **Configuration Manager 1902**, puis choisissez **Exécuter la vérification des prérequis** dans le ruban.

Pour plus d’informations, consultez la section **Pour exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour** dans [Avant d’installer une mise à jour dans la console](/sccm/core/servers/manage/install-in-console-updates#bkmk_beforeinstall).

> [!IMPORTANT]  
> Quand l’outil de vérification des prérequis s’exécute, le processus met à jour certains fichiers sources de produit utilisés pour les tâches de maintenance du site. Par conséquent, après l’exécution de l’outil de vérification des prérequis, mais avant l’installation de la mise à jour, si vous devez effectuer une tâche de maintenance de site, exécutez  **Setupwfe.exe**  (programme d’installation de Configuration Manager) à partir du dossier CD.Latest sur le serveur de site.

#### <a name="update-sites"></a>Mettre à jour les sites   
Vous êtes désormais prêt à démarrer l’installation de la mise à jour pour votre hiérarchie. Pour plus d’informations sur l’installation de la mise à jour, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Vous pouvez installer la mise à jour en dehors des heures d’ouverture normales. Déterminez à quel moment le processus aura le moins d’impact sur les opérations d’entreprise. L’installation de la mise à jour et ses actions entraînent la réinstallation des composants du site et des rôles de système de site.

Pour plus d’informations, consultez  [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).



## <a name="post-update-checklist"></a>Liste de contrôle postérieure à la mise à jour

Après les mises à jour du site, utilisez la liste de vérification suivante pour effectuer les tâches et les configurations courantes.


#### <a name="confirm-version-and-restart-if-necessary"></a>Confirmer la version et redémarrer (si nécessaire)
Vérifiez que chaque serveur de site et chaque rôle de système de site a été mis à jour vers la version 1902. Dans la console, ajoutez la colonne **Version** aux nœuds **Sites** et **Points de distribution** dans l’espace de travail **Administration**. Quand cela est nécessaire, un rôle de système de site se réinstalle automatiquement pour se mettre à jour vers la nouvelle version. 

Redémarrez les systèmes de site distants qui ne se mettent pas correctement à jour. Examinez l’infrastructure de votre site et vérifiez que les serveurs de site et serveurs de système de site distants appropriés ont redémarré correctement. En règle générale, les serveurs de site redémarrent uniquement quand Configuration Manager installe .NET en tant que prérequis pour un rôle de système de site.


#### <a name="confirm-site-to-site-replication-is-active"></a>Vérifier que la réplication de site à site est active
Dans la console Configuration Manager, accédez aux emplacements suivants pour afficher l’état et vérifier que la réplication est active :  

-   Espace de travail **Surveillance**, nœud **Hiérarchie de site**  

-   Espace de travail **Surveillance**, nœud **Réplication de la base de données**  

Pour plus d’informations, consultez les articles suivants :  
- [Surveiller l’infrastructure de la hiérarchie et de la réplication](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure)
- [À propos de l’analyseur de lien de réplication](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA)  


#### <a name="update-configuration-manager-consoles"></a>Mettre à jour des consoles Configuration Manager
Mettez à jour toutes les consoles Configuration Manager distantes vers la même version. Vous êtes invité à mettre à jour la console dans les cas suivants :  

-   lorsque vous ouvrez la console.  

-   lorsque vous accédez à un nouveau nœud dans la console ;  


#### <a name="reconfigure-database-replicas-for-management-points"></a>Reconfigurer les réplicas de base de données pour les points de gestion
Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données pour les points de gestion que vous avez désinstallés avant la mise à jour du site. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  


#### <a name="reconfigure-any-disabled-maintenance-tasks"></a>Reconfigurer les tâches de maintenance désactivées
Si vous avez désactivé les [tâches de maintenance](/sccm/core/servers/manage/maintenance-tasks) de base de données sur un site avant d’installer la mise à jour, reconfigurez ces tâches. Utilisez les mêmes paramètres qui étaient en vigueur avant la mise à jour.  


#### <a name="update-clients"></a>Mettre à jour des clients
Mettez à jour les clients conformément au plan créé par vos soins, en particulier si vous avez configuré le pilotage des clients avant d’installer la mise à jour. Pour plus d’informations, consultez [Guide pratique pour mettre à niveau des clients sur les ordinateurs Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  


#### <a name="third-party-extensions"></a>Extensions tierces
Si vous utilisez des extensions de Configuration Manager, mettez-les à jour avec la dernière version pour qu’elles prennent en charge Configuration Manager version 1902. 


#### <a name="update-custom-boot-images-and-media"></a>Mettre à jour les images de démarrage personnalisées et les médias
<!--SCCMDocs issue 775-->

Utilisez l’action **Mettre à jour les points de distribution** pour toute image de démarrage que vous utilisez, qu’il s’agisse d’une image de démarrage par défaut ou personnalisée. Cette action garantit que les clients peuvent utiliser la dernière version. Même s’il n’y a pas de nouvelle version de Windows ADK, les composants du client Configuration Manager peuvent changer lors d’une mise à jour. Si vous ne mettez pas à jour les images de démarrage et le média, les déploiements de séquences de tâches peuvent échouer sur les appareils. 

Lorsque vous mettez à jour le site, Configuration Manager. met automatiquement à jour les images de démarrage *par défaut*. Il ne distribue pas automatiquement le contenu mis à jour aux points de distribution. Utilisez l’action **Mettre à jour les points de distribution** sur des images de démarrage spécifiques lorsque vous êtes prêt à distribuer ce contenu sur votre réseau. 

Après la mise à jour du site, mettez à jour manuellement toutes les images de démarrage *personnalisées*. Si nécessaire, cette action met à jour l’image de démarrage avec les derniers composants du client, la recharge éventuellement avec la version actuelle de Windows PE et redistribue le contenu aux points de distribution. 

Pour plus d’informations, consultez [Mettre à jour des points de distribution avec l’image de démarrage](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image). 
