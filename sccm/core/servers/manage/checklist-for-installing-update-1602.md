---
title: Liste de contrôle pour 1602
titleSuffix: Configuration Manager
description: Découvrez les actions à entreprendre avant d’effectuer la mise à jour de System Center Configuration Manager version 1511 vers la version 1602.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b63ef197-01f0-4894-b929-5ef8403c5195
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: ecefbaa7de198992ad68c3942fd25311515e4118
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897747"
---
# <a name="checklist-for-installing-update-1602-for-system-center-configuration-manager"></a>Liste de contrôle pour l’installation de la mise à jour 1602 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de mettre à jour System Center Configuration Manager version 1511 vers la version 1602, passez en revue les informations et la liste de contrôle suivantes pour connaître les mesures à prendre avant de commencer la mise à jour.  

 **À propos de l’installation de la mise à jour 1602 :**  

 Vous ne pouvez installer la mise à jour 1602 que sur le site de niveau supérieur de votre hiérarchie. Cela signifie que vous lancez l’installation à partir de votre site d’administration centrale si en avez un, ou à partir de votre site principal autonome.  

-   Les sites principaux enfants installent automatiquement la mise à jour après que le site d’administration centrale a fini de l’installer. Vous pouvez utiliser des fenêtres de maintenance pour contrôler à quel moment le site installe les mises à jour. Depuis la publication de la mise à jour 1602, les fenêtres de maintenance sont nommées *fenêtres de service*. Pour plus d’informations, consultez [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).  

-   Une fois que le site parent principal a installé la mise à jour, vous devez mettre à jour manuellement les sites secondaires à partir de la console Configuration Manager. Les mise à jour automatiques des serveurs de sites secondaires ne sont pas prises en charge.  

Quand le serveur de site installe la mise à jour, les rôles de système de site installés sur le serveur de site et sur des ordinateurs distants sont automatiquement mis à jour. Par conséquent, avant d’installer la mise à jour, vérifiez que chaque serveur de système de site remplit les nouveaux prérequis pour les opérations avec la nouvelle version de mise à jour.  

La première fois que vous utilisez une console Configuration Manager à l’issue de la mise à jour, vous êtes invité à mettre à jour cette console. Pour cela, vous devez exécuter le programme d’installation de Configuration Manager sur l’ordinateur hébergeant la console, puis choisir l’option de mise à jour de la console. Nous vous recommandons de ne pas retarder l’installation de la mise à jour sur la console.  

 **Liste de contrôle :**  

 **Vérifiez que tous les sites exécutent une version prise en charge de System Center Configuration Manager :**  Pour que vous puissiez lancer l’installation de la mise à jour 1602, tous les serveurs de site de la hiérarchie doivent exécuter System Center Configuration Manager version 1511.  

 **Examinez les versions de Microsoft .NET installées sur les serveurs de système de site :** Lorsqu’un site installe la mise à jour 1602, Configuration Manager installe automatiquement .NET Framework 4.5.2 sur chaque ordinateur hébergeant l’un des rôles de système de site suivants (si .NET Framework 4.5 ou ultérieur n’est pas déjà installé) :  

-   Point proxy d'inscription  

-   Point d'inscription  

-   Point de gestion  

-   point de connexion de service  

Cette installation peut mettre le serveur de système de site en état d’attente de redémarrage, et signaler des erreurs sur l’Afficheur des messages d’état du composant Configuration Manager. En outre, des applications .NET sur le serveur peuvent présenter des défaillances aléatoires jusqu’au redémarrage du serveur.  

 Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

 **Examinez l’état des sites et de la hiérarchie et vérifiez qu’il ne reste aucun problème non résolu :** Avant de mettre à jour un site, résolvez tous les problèmes de fonctionnement du serveur de site, du serveur de base de données du site et des rôles de système de site installés sur les ordinateurs distants. Une mise à niveau de site peut échouer en raison de l’existence de problèmes opérationnels.  

Pour plus d'informations, voir [Utiliser des alertes et le système d’état pour System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Vérifiez la réplication des fichiers et des données entre les sites :**  vérifiez que la réplication des fichiers et bases de données entre les sites est opérationnelle et active. Des retards ou backlogs dans ces domaines peuvent perturber ou empêcher la mise à jour.    

Pour la réplication de la base de données, vous pouvez utiliser l’Analyseur de lien de réplication pour faciliter la résolution des problèmes avant de commencer la mise à jour.    

 Pour plus d’informations, consultez [À propos de l’analyseur de lien de réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) dans la rubrique [Surveiller l’infrastructure de la hiérarchie et de la réplication dans System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Installez toutes les mises à jour critiques applicables aux systèmes d’exploitation des ordinateurs hébergeant le site, le serveur de base de données de site et les rôles de système de site distants :** Avant d’installer une mise à jour pour Configuration Manager, installez les mises à jour critiques pour chaque système de site applicable. Si vous installez une mise à jour qui nécessite un redémarrage, redémarrez les ordinateurs concernés avant d'entreprendre la mise à jour.  

 **Désactivez les réplicas de base de données pour les points de gestion au niveau des sites principaux :** Configuration Manager ne peut pas réussir la mise à jour d’un site principal ayant un réplica de base de données activé pour les points de gestion. Désactivez la réplication de base de données avant de :  

-   Créer une sauvegarde de la base de données pour tester la mise à niveau de base de données.  

-   Installer une mise à jour pour Configuration Manager.  

Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Reconfigurez les points de mise à jour logicielle qui utilisent l’équilibrage de la charge réseau (NLB) :** Configuration Manager ne peut pas mettre à jour un site qui utilise un cluster d’équilibrage de la charge réseau pour héberger des points de mise à jour logicielle.  Si vous utilisez des clusters NLB pour les points de mise à jour logicielle, utilisez Windows PowerShell pour supprimer le cluster NLB.    

 Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md).  

 **Désactivez toutes les tâches de maintenance de site sur chaque site pendant la durée de l’installation de la mise à jour sur ce site :** avant d’installer les mises à jour, désactivez toutes les tâches de maintenance de site qui peuvent s’exécuter pendant le processus de mise à jour. Parmi ces tâches, citons les suivantes :  

-   Serveur de site de sauvegarde  

-   Supprimer les anciennes opérations du client  

-   Supprimer les données de découverte anciennes  

Si une tâche de maintenance de base de données du site s’exécute pendant l’installation de la mise à jour, celle-ci peut échouer. Avant de désactiver une tâche, enregistrez sa planification afin de pouvoir restaurer sa configuration une fois la mise à jour installée.  

 Pour plus d’informations, consultez [Tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) et [Référence des tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md). 

**Arrêtez temporairement tous les logiciels antivirus sur les serveurs System Center Configuration Manager :** Avant de mettre à jour un site, assurez-vous que vous avez arrêté les logiciels antivirus sur les serveurs Configuration Manager. <!--SMS.503481--> 

 **Créez une sauvegarde de la base de données du site au niveau du site d’administration centrale et des sites principaux :** Avant de mettre à jour un site, sauvegardez la base de données de site pour être certain de disposer d’une sauvegarde utilisable dans le cadre d’une reprise d’activité après sinistre.   

Pour plus d’informations, consultez [Sauvegarde et récupération pour System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Sauvegardez un fichier Configuration.mof personnalisé** : Si vous utilisez un fichier Configuration.mof personnalisé pour définir des classes de données que vous utilisez avec un inventaire matériel, créez une sauvegarde de ce fichier avant la mise à jour du site. Après la mise à jour, restaurez ce fichier sur votre site version 1602. Durant la mise à jour d’un site, le fichier actuel est remplacé par sa version d’origine (par défaut). Pour plus d’informations sur l’utilisation de ce fichier, consultez [Guide pratique pour étendre l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 **Testez la mise à niveau de base de données sur une copie de la dernière sauvegarde de la base de données de site :** avant de mettre à jour un site d’administration centrale ou un site principal System Center Configuration Manager, testez le processus de mise à niveau de base de données de site sur une copie de la base de données de site.  

-   Vous devez tester le processus de mise à niveau de base de données de site, car la base de données peut être modifiée quand vous mettez à niveau un site.  

-   Bien que le test de mise à niveau ne soit pas obligatoire, il peut identifier des problèmes liés à la mise à niveau avant que votre base de données de production ne soit affectée.  

-   Un échec de mise à niveau de base de données de site peut rendre votre base de données de site inutilisable, et une récupération de site peut s'avérer nécessaire pour rétablir les fonctionnalités.  

-   Bien que la base de données de site soit partagée entre sites d'une même hiérarchie, prévoyez de tester la base de données sur chacun des sites concernés avant de procéder à leur mise à niveau.  

-   Si vous utilisez des réplicas de base de données pour les points de gestion d'un site principal, désactivez la réplication avant de créer la sauvegarde de la base de données de site.  

Configuration Manager ne prend en charge ni la sauvegarde des sites secondaires ni la mise à niveau de test d’une base de données de site secondaire.   
N’exécutez pas une mise à niveau de base de données sur la base de données du site de production. Cette opération met à jour la base de données du site et pourrait rendre celui-ci inutilisable. Pour plus d’informations, consultez [Étape 2 : tester la mise à niveau de base de données avant d’installer une mise à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) dans la rubrique **Avant d’installer une mise à jour dans la console**.  

 **Planifiez le pilotage du client :** Quand vous installez une mise à jour qui affecte le client, vous pouvez la tester en mode préproduction avant de procéder au déploiement et à la mise à niveau de votre client actif.   

 Pour tirer parti de cette option, vous devez configurer votre site pour qu’il prenne en charge les mises à niveau automatiques pour la préproduction avant de commencer l’installation de la mise à jour. Pour plus d’informations, consultez [Mettre à niveau les clients dans System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) et   
[Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

 **Planifiez l’utilisation des fenêtres de maintenance pour contrôler le moment auquel les serveurs de site installent les mises à jour :** vous pouvez utiliser les fenêtres de maintenance pour définir une période au cours de laquelle les mises à jour d’un serveur de site peuvent être installées. Cela peut vous aider à contrôler le moment où les sites au sein de votre hiérarchie installent la mise à jour.   

Depuis la publication de la mise à jour 1602, les fenêtres de maintenance sont nommées *fenêtres de service*. Pour plus d’informations, consultez [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).  

 **Exécutez l’outil de vérification des prérequis du programme d’installation :**  avant d’installer la mise à jour 1602, vous pouvez exécuter l’outil de vérification des prérequis, indépendamment de l’installation de la mise à jour. Quand vous installez la mise à jour sur le site, l’outil de vérification des prérequis s’exécute à nouveau.  

Pour plus d'informations, voir **Étape 3 : Exécuter l’outil de vérification des prérequis avant d’installer une mise à jour** dans la rubrique [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md).  

> [!IMPORTANT]  
>  Quand l’outil de vérification des prérequis s’exécute indépendamment ou dans le cadre de l’installation d’une mise à jour, le processus met à jour certains fichiers sources du produit qui sont utilisés pour les tâches de maintenance de site. Par conséquent, après l’exécution de l’outil de vérification des prérequis, mais avant l’installation de la mise à jour 1602, si vous devez effectuer une tâche de maintenance de site, exécutez **Setupwfe.exe** (programme d’installation de Configuration Manager) à partir du dossier CD.Latest sur le serveur du site.  

 **Mettre à jour les sites :** Vous êtes maintenant prêt à commencer l’installation de la mise à jour pour votre hiérarchie. Nous vous recommandons de planifier l’installation de la mise à jour en dehors des heures de bureau normales pour chaque site, quand le processus d’installation de la mise à jour et ses actions pour réinstaller les composants du site et les rôles de système de site auront le moins d’effet sur les opérations de votre entreprise.

Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md).  

## <a name="see-also"></a>Voir aussi  
 [Mises à jour pour System Center Configuration Manager](../../../core/servers/manage/updates.md)
