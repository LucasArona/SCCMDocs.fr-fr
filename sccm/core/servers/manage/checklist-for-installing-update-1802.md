---
title: Liste de contrôle pour 1802
titleSuffix: Configuration Manager
description: Découvrez les actions à entreprendre avant d’effectuer la mise à jour vers System Center Configuration Manager version 1802.
ms.date: 06/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6af92de2-b2c7-4d5c-affd-6cce81979fb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 74fa4e9240cf4a3d369d6b20bcb9233fb6319a8d
ms.sourcegitcommit: 690f64bd02139f893bd0b45e2e0f00ed6bb4e1c1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35259296"
---
# <a name="checklist-for-installing-update-1802-for-system-center-configuration-manager"></a>Liste de contrôle pour l’installation de la mise à jour 1802 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous utilisez Current Branch de System Center Configuration Manager, vous pouvez installer la mise à jour dans la console de la version 1802 pour mettre à jour votre hiérarchie à partir d’une version antérieure. <!-- baseline only statement: -->(Comme la version 1802 est également disponible en tant que [support de base de référence](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions), vous pouvez utiliser le support d’installation pour installer le premier site d’une nouvelle hiérarchie.)

Pour obtenir la mise à jour de la version 1802, vous devez utiliser un point de connexion de service sur le site de niveau supérieur de votre hiérarchie. Ce rôle de système de site peut être en mode en ligne ou hors connexion. Une fois que votre hiérarchie a téléchargé la mise à jour Microsoft, celle-ci est accessible dans la console de l’espace de travail **Administration**, sous le nœud **Mises à jour et maintenance**.

-   Quand la mise à jour est répertoriée comme **disponible**, elle est prête à être installée. Avant d’installer la version 1802, passez en revue les informations suivantes [sur l’installation de la mise à jour 1802](#about-installing-update-1802) et la [liste de contrôle](#checklist) pour connaître les configurations à effectuer avant de commencer la mise à jour.

-   Si la mise à jour s’affiche en tant que **Téléchargement en cours** et ne change pas, recherchez les erreurs dans les journaux **hman.log** et **dmpdownloader.log**.

    -   Si dmpdownloader.log indique que le processus dmpdownloader est en veille en attendant la vérification des mises à jour, vous pouvez redémarrer le service **SMS_Executive** sur le serveur de site pour redémarrer le téléchargement des fichiers de redistribution de la mise à jour.

    -   Un autre problème courant de téléchargement se produit quand les paramètres du serveur proxy empêchent les téléchargements à partir de <http://silverlight.dlservice.microsoft.com> et <http://download.microsoft.com>.

Pour plus d’informations sur l’installation des mises à jour, consultez [Mises à jour et maintenance dans la console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Pour plus d’informations sur les versions de Current Branch, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#bkmk_Baselines) dans [Mises à jour pour System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1802"></a>À propos de l’installation de la mise à jour 1802

**Sites :**  
Vous pouvez installer la mise à jour 1802 sur le site de niveau supérieur de votre hiérarchie. Cela signifie que vous lancez l’installation à partir de votre site d’administration centrale si en avez un, ou à partir de votre site principal autonome. Après l’installation de la mise à jour sur le site de niveau supérieur, les sites enfants ont le comportement de mise à jour suivant :

-   Les sites principaux enfants installent automatiquement la mise à jour quand le site d’administration centrale a fini de l’installer. Vous pouvez utiliser des fenêtres de service pour spécifier à quel moment un site installe la mise à jour. Pour plus d’informations, consultez [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).

-   Après que le site parent principal a installé la mise à jour, vous devez mettre à jour manuellement chacun des sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.

**Rôles de système de site :**  
Quand un serveur de site installe la mise à jour, les rôles de système de site installés sur l’ordinateur serveur de site et sur des ordinateurs distants sont automatiquement mis à jour. Avant d’installer la mise à jour, vérifiez que chaque serveur de système de site remplit les prérequis pour les opérations avec la nouvelle version de mise à jour.

**Consoles Configuration Manager :**   
La première fois que vous utilisez une console Configuration Manager à l’issue de la mise à jour, vous êtes invité à mettre à jour cette console. Pour cela, vous devez exécuter le programme d’installation de Configuration Manager sur l’ordinateur hébergeant la console, puis choisir l’option de mise à jour de la console. Nous vous recommandons de ne pas retarder l’installation de la mise à jour sur la console.

> [!IMPORTANT]  
> Lorsque vous installez une mise à jour sur le site d’administration centrale, tenez compte des limitations suivantes et des retards qui se produisent jusqu’à ce que tous les sites principaux enfants aient également terminé l’installation de la mise à jour :    
> - La **mise à niveau des clients** ne démarre pas. Cela comprend la mise à jour automatique des clients et des clients en préproduction. En outre, il n’est pas possible de mettre en production les clients en préproduction tant que le dernier site n’a pas terminé l’installation de la mise à jour. Après l’installation de la mise à jour sur le dernier site, la mise à niveau des clients commence, en fonction de vos options de configuration.   
> - Les **nouvelles fonctionnalités** que vous activez avec la mise à jour ne sont pas disponibles. L’objectif est d’éviter l’envoi de la réplication de données associées à cette fonctionnalité à un site qui n’a pas encore installé la prise en charge de cette fonctionnalité. Après l’installation de la mise à jour sur tous les sites principaux, la fonctionnalité sera utilisable.   
> - Les **liens de réplication** entre le site d’administration centrale et les sites principaux enfants apparaissent comme non mis à niveau. Cela se présente, dans l’état d’installation du pack de mise à jour, sous la forme d’un état Terminé avec un avertissement pour l’initialisation de la surveillance de la réplication. Dans le nœud Surveillance de la console, cela se présente sous l’état *Lien en cours de configuration*.


## <a name="checklist"></a>Liste de contrôle

**Vérifiez que tous les sites exécutent une version de System Center Configuration Manager qui prend en charge la mise à jour vers 1802 :**   
Chaque serveur de site de la hiérarchie doit exécuter la même version de System Center Configuration Manager pour que vous puissiez lancer l’installation de la mise à jour 1802. Pour passer à la version 1802, vous devez utiliser la version 1702, 1706 ou 1710.

**Vérifiez l’état de votre contrat Software Assurance ou des droits d’abonnement équivalents :**   
Vous devez disposer d’un contrat Software Assurance (SA) actif pour installer la mise à jour 1802. Quand vous installez cette mise à jour, l’onglet **Licences** propose l’option vous permettant de confirmer la **date d’expiration de Software Assurance**.

Il s’agit d’une valeur facultative que vous pouvez spécifier pour des raisons pratiques et qui vous servira de rappel concernant la date d’expiration de votre licence. Cette date est visible lorsque vous installez des mises à jour ultérieures. Vous avez peut-être déjà spécifié cette valeur pendant la configuration ou l’installation d’une mise à jour, ou en utilisant l’onglet **Licences** de **Paramètres de hiérarchie**, sur la console de Configuration Manager.

Pour plus d’informations, consultez [Licences et branches pour System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Examinez les versions installées de Microsoft .NET sur les serveurs de système de site** : quand un site installe cette mise à jour, Configuration Manager installe automatiquement le .NET Framework 4.5.2 sur chaque ordinateur hébergeant un des rôles de système de site suivants (si le .NET Framework 4.5 ou ultérieur n’est pas déjà installé) :

-   Point proxy d'inscription
-   Point d'inscription
-   Point de gestion
-   Point de connexion de service

Cette installation peut mettre le serveur de système de site en état d’attente de redémarrage, et signaler des erreurs sur l’Afficheur des messages d’état du composant Configuration Manager. En outre, des applications .NET sur le serveur peuvent présenter des défaillances aléatoires jusqu’au redémarrage du serveur.

Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Vérifiez la version du Kit de déploiement et d’évaluation (ADK) Windows pour Windows 10** : la version de Windows 10 ADK doit être 1703 ou ultérieure. (Pour plus d’informations sur les versions de Windows ADK prises en charge, consultez [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).) Si vous devez mettre à jour Windows ADK, faites-le avant de commencer la mise à jour de Configuration Manager. Les images de démarrage par défaut seront ainsi mises à jour automatiquement vers la dernière version de Windows PE. (Les images de démarrage personnalisé doivent être mises à jour manuellement.)

Si vous mettez à jour le site avant de mettre à jour Windows ADK, consultez [Mettre à jour les points de distribution avec l’image de démarrage](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

**Examinez l’état du site et de la hiérarchie, et vérifiez l’absence de tout problème non résolu :** avant de mettre à jour un site, résolvez tous les problèmes opérationnels pour le serveur de site, le serveur de bases de données du site et les rôles de système de site installés sur des ordinateurs distants. Une mise à niveau de site peut échouer en raison de l’existence de problèmes opérationnels.

Pour plus d'informations, voir [Utiliser des alertes et le système d’état pour System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Examinez la réplication des fichiers et données entre sites :**   
vérifiez que la réplication des fichiers et bases de données entre les sites est opérationnelle et active. Des retards ou backlogs dans ces domaines peuvent perturber ou empêcher la mise à jour.
Pour la réplication de la base de données, vous pouvez utiliser l’Analyseur de lien de réplication pour faciliter la résolution des problèmes avant de commencer la mise à jour.

Pour plus d’informations, consultez [À propos de l’analyseur de lien de réplication](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) dans la rubrique [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Installez toutes les mises à jour critiques applicables pour les systèmes d’exploitation sur les ordinateurs hébergeant le site, le serveur de base de données du site et les rôles de système de site distants :** avant d’installer une mise à jour pour Configuration Manager, installez toutes les mises à jour critiques pour chaque système de site concerné. Si vous installez une mise à jour qui nécessite un redémarrage, redémarrez les ordinateurs concernés avant d'entreprendre la mise à jour.

**Désactivez les réplicas de base de données pour les points de gestion au niveau des sites principaux :**   
Configuration Manager ne peut pas réussir la mise à jour d’un site principal ayant un réplica de base de données activé pour les points de gestion. Désactivez la réplication de base de données avant d’installer une mise à jour pour Configuration Manager.

Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Définissez un basculement manuel pour les groupes de disponibilité SQL Server AlwaysOn :**   
Si vous utilisez un groupe de disponibilité, vérifiez qu’il est défini sur le basculement manuel avant de commencer l’installation de la mise à jour. Une fois le site mis à jour, vous pouvez restaurer le basculement automatique. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

**Reconfigurez les points de mise à jour logicielle qui utilisent l’équilibrage de la charge réseau (NLB) :**   
<!-- Support for NLBs is fully removed with 1702. When 1702 is no longer in support, this statement can drop -->
Configuration Manager ne peut pas mettre à jour un site qui utilise un cluster d’équilibrage de la charge réseau (NLB) pour héberger des points de mise à jour logicielle.

Si vous utilisez des clusters NLB pour les points de mise à jour logicielle, utilisez Windows PowerShell pour supprimer le cluster NLB.
Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Désactivez toutes les tâches de maintenance de site sur chaque site pendant la durée de l’installation de la mise à jour sur ce site :**   
Avant d’installer la mise à jour, désactivez toutes les tâches de maintenance de site qui peuvent s’exécuter pendant le processus de mise à jour. Cela inclut, sans toutefois s'y limiter, les tâches suivantes :

-   Serveur de site de sauvegarde
-   Supprimer les anciennes opérations du client
-   Supprimer les données de découverte anciennes

Si une tâche de maintenance de base de données du site s’exécute pendant l’installation de la mise à jour, celle-ci peut échouer. Avant de désactiver une tâche, enregistrez sa planification pour pouvoir restaurer sa configuration une fois la mise à jour installée.

Pour plus d’informations, consultez [Tâches de maintenance pour System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) et [Référence des tâches de maintenance pour System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Arrêtez temporairement tout logiciel antivirus sur les serveurs System Center Configuration Manager :** avant de mettre à jour un site, vérifiez que vous avez arrêté tout logiciel antivirus sur les serveurs Configuration Manager. <!--SMS.503481--> 

**Créez une sauvegarde de la base de données du site d’administration centrale et des sites principaux :** avant de mettre à jour un site, sauvegardez sa base de données pour être certain de disposer d’une sauvegarde correcte utilisable en cas de récupération d’urgence.

Pour plus d’informations, consultez [Sauvegarde et récupération pour System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Planifiez un test du client :**   
Quand vous installez une mise à jour qui affecte le client, vous pouvez la tester en mode préproduction avant de procéder au déploiement et à la mise à niveau de votre client actif.

Pour tirer parti de cette option, vous devez configurer votre site pour qu’il prenne en charge les mises à niveau automatiques pour la préproduction avant de commencer l’installation de la mise à jour.

Pour plus d’informations, consultez [Mettre à niveau les clients dans System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) et [Comment tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Planifiez l’utilisation des fenêtres de service pour contrôler le moment auquel les serveurs de site installent les mises à jour :**   
Utilisez les fenêtres de service pour définir une période au cours de laquelle les mises à jour à un serveur de site peuvent être installées.

Cela peut vous aider à contrôler le moment où les sites au sein de votre hiérarchie installent la mise à jour. Pour plus d’informations, consultez [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).

**Passez en revue les extensions prises en charge :**   
<!--SCCMdocs#587-->   
Si vous étendez Configuration Manager avec d’autres produits Microsoft ou partenaires, vérifiez que ces produits prennent en charge la version 1802. Demandez cette information au fournisseur du produit. Par exemple, consultez les [notes de publication](/sccm/mdt/release-notes) de Microsoft Deployment Toolkit.

**Exécutez l’outil de vérification des prérequis du programme d’installation :**   
Quand la mise à jour est répertoriée dans la console comme **Disponible**, vous pouvez exécuter indépendamment l’outil de vérification des prérequis avant d’installer la mise à jour. (Quand vous installez la mise à jour sur le site, l’outil de vérification des prérequis s’exécute à nouveau.)

Pour exécuter une vérification des prérequis à partir de la console, accédez à l’espace de travail **Administration**, puis sélectionnez **Mises à jour et maintenance**. Sélectionnez la mise à jour **Configuration Manager 1802**, puis cliquez sur **Exécuter la vérification des prérequis** dans le ruban.

Pour plus d’informations sur le démarrage et la surveillance de la vérification des prérequis, consultez **Étape 3 : exécuter l’outil de vérification des prérequis avant d’installer une mise à jour** dans la rubrique [Installer des mises à jour dans la console pour System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quand l’outil de vérification des prérequis s’exécute indépendamment ou dans le cadre de l’installation d’une mise à jour, le processus met à jour certains fichiers sources du produit qui sont utilisés pour les tâches de maintenance de site. Par conséquent, après l’exécution de l’outil de vérification des prérequis, mais avant l’installation de la mise à jour, si vous devez effectuer une tâche de maintenance de site, exécutez **Setupwfe.exe** (programme d’installation de Configuration Manager) à partir du dossier CD.Latest sur le serveur de site.

**Mettez à jour les sites :**   
Vous êtes maintenant prêt à commencer l’installation de la mise à jour pour votre hiérarchie. Pour plus d’informations sur l’installation de la mise à jour, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).

Nous vous recommandons de planifier l’installation de la mise à jour en dehors des heures de bureau normales pour chaque site, quand le processus d’installation de la mise à jour et ses actions pour réinstaller les composants du site et les rôles de système de site auront le moins d’effet sur les opérations de votre entreprise.

Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="post-update-checklist"></a>Liste de contrôle post-mise à jour
Vérifiez et effectuez les actions suivantes après la fin de l’installation de la mise à jour.
1.  Assurez-vous que la réplication de site à site est active. Dans la console, affichez **Surveillance** > **Hiérarchie de site** et **Surveillance** > **Réplication de la base de données** pour accéder à des indications concernant les problèmes ou à la confirmation que les liens de réplication sont actifs.
2.  Assurez-vous que chaque serveur de site et chaque rôle de système de site est passé à la version 1802. Dans la console, vous pouvez ajouter la colonne facultative **Version** à l’affichage de certains nœuds, y compris **Sites** et **Points de distribution**.

 Lorsque c’est nécessaire, un rôle de système de site se réinstalle automatiquement pour passer à la nouvelle version. Redémarrez les systèmes de site distants qui ne se mettent pas à jour correctement.
3.  Reconfigurez les réplicas de base de données des points de gestion au niveau des sites principaux que vous avez désactivés avant de commencer la mise à jour.
4.  Reconfigurez les tâches de maintenance de la base de données que vous avez désactivées avant de commencer la mise à jour.
5.  Si vous avez configuré le pilotage des clients avant d’installer la mise à jour, mettez à niveau les clients selon le plan que vous avez créé.
6.  Si vous utilisez des extensions Configuration Manager, mettez-les à jour vers la version la plus récente pour qu’elles prennent en charge cette mise à jour Configuration Manager. 
