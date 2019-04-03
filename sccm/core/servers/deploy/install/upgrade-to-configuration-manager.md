---
title: Mettre à niveau vers Configuration Manager
description: Découvrez les étapes d’exécution d’une mise à niveau sur place réussie à partir d’un site et d’une hiérarchie qui exécute System Center 2012 Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2b6c7dac285493e4887b254c7d6fe7432840d6bd
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58524130"
---
# <a name="upgrade-to-configuration-manager"></a>Mettre à niveau vers Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Exécutez une mise à niveau sur place de la branche actuelle Configuration Manager à partir d’un site et d’une hiérarchie qui exécute System Center 2012 Configuration Manager. Avant la mise à niveau à partir de System Center 2012 Configuration Manager, vous devez préparer les sites. Cette préparation vous oblige à supprimer des configurations spécifiques qui peuvent empêcher une mise à niveau réussie. Suivez ensuite la séquence de mise à niveau si vous plusieurs sites sont concernés.  

> [!TIP]  
> Lors de la gestion de l’infrastructure de site et de hiérarchie de Configuration Manager, les termes *mise à niveau*, *mise à jour* et *installation* sont utilisés pour décrire trois concepts distincts. Pour connaître la signification et l’usage de chaque terme, consultez [À propos de la mise à niveau, de la mise à jour et de l’installation de l’infrastructure de site et de hiérarchie](/sccm/core/understand/upgrade-update-install).



## <a name="bkmk_path"></a> Chemins de mise à niveau sur place  

Les options suivantes représentent les chemins de mise à niveau sur place actuellement  pris en charge :


### <a name="upgrade-to-version-1902"></a>Mise à niveau vers la version 1902

Si vous avez un support de base de référence de version 1902, vous pouvez mettre à niveau les produits suivants vers une version sous licence complète de System Center Configuration Manager version 1902 :   
- Une installation d’évaluation de System Center Configuration Manager version 1902
- System Center 2012 Configuration Manager avec Service Pack 1
- System Center 2012 Configuration Manager avec Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager avec Service Pack 1

### <a name="upgrade-to-version-1802"></a>Mise à niveau vers la version 1802
Si vous avez un support de base de référence de version 1802, vous pouvez mettre à niveau les produits suivants vers une version sous licence complète de System Center Configuration Manager version 1802 :   
- Une installation d’évaluation de System Center Configuration Manager version 1802
- System Center 2012 Configuration Manager avec Service Pack 1
- System Center 2012 Configuration Manager avec Service Pack 2
- System Center 2012 R2 Configuration Manager
- System Center 2012 R2 Configuration Manager avec Service Pack 1

### <a name="upgrade-to-version-1606"></a>Mettre à niveau vers la version 1606
Le 15 décembre 2016, le média de base de la version 1606 a été republié afin d’ajouter la prise en charge d’autres scénarios de mise à niveau. Cette version prend en charge la mise à niveau des versions suivantes vers une version sous licence complète de System Center Configuration Manager version 1606 :  
- Une installation d’évaluation de System Center Configuration Manager version 1606
- Une installation de version finale (RC) de System Center Configuration Manager  
- System Center 2012 Configuration Manager avec Service Pack 1  
- System Center 2012 Configuration Manager avec Service Pack 2  
- System Center 2012 R2 Configuration Manager sans Service Pack
- System Center 2012 R2 Configuration Manager avec Service Pack 1  

Si vous utilisez le média de base de la version 1606 téléchargé avant le 15 décembre 2016, vous pouvez mettre à niveau uniquement les produits suivants vers une version sous licence complète de System Center Configuration Manager version 1606 :
- Une installation d’évaluation de System Center Configuration Manager version 1606
- System Center 2012 Configuration Manager avec Service Pack 2
- System Center 2012 R2 Configuration Manager avec Service Pack 1

Pour plus d’informations sur utilisation de la version 1606, consultez [Foire aux questions sur les branches et la gestion des licences de Configuration Manager](/sccm/core/understand/product-and-licensing-faq).

> [!TIP]  
>  Une mise à niveau à partir d’une version de System Center 2012 Configuration Manager vers Current Branch peut vous permettre de simplifier votre processus de mise à niveau. Pour plus d'informations, consultez :  
>   
> - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#bkmk_Baselines)  
> - [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder)  


### <a name="unsupported-paths"></a>Chemins non pris en charge

Les chemins suivants ne sont pas pris en charge :

- La mise à niveau d’une branche Technical Preview vers une installation sous licence n’est pas prise en charge. Une version d’évaluation technique peut uniquement être mise à niveau vers une version ultérieure de la version d’évaluation technique.  

- La migration d’une version Technical Preview vers une version sous licence complète n’est pas pris en charge.  



##  <a name="bkmk_checklist"></a> Listes de vérification de mise à niveau  

Les listes de vérification suivantes peuvent vous aider à planifier une mise à niveau vers Configuration Manager.  


### <a name="before-you-upgrade"></a>Avant la mise à niveau :  

Passez en revue ces étapes avant d’effectuer une mise à niveau vers Configuration Manager.


#### <a name="review-your-system-center-2012-configuration-manager-environment"></a>Passez en revue votre environnement System Center 2012 Configuration Manager
Corrigez les problèmes comme détaillé dans l’article du support Microsoft suivant : [Les clients Configuration Manager sont réinstallés toutes les cinq heures en raison d’une nouvelle tentative récurrente qui peut provoquer une mise à niveau du client par inadvertance](https://support.microsoft.com/help/4018655).

#### <a name="make-sure-your-environment-meets-the-supported-configurations"></a>Assurez-vous que votre environnement répond aux configurations prises en charge

- Passez en revue la version du système d’exploitation de serveur utilisée pour héberger les rôles de système de site :  

    - Certains anciens systèmes d’exploitation pris en charge par System Center 2012 Configuration Manager ne sont pas pris en charge par la branche actuelle de Configuration Manager. Avant la mise à niveau, supprimez des rôles système de site sur ces versions de système d’exploitation. Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).   

    - L’outil de vérification des conditions préalables pour Configuration Manager ne vérifie pas les prérequis pour les rôles de système de site sur le serveur de site ou sur les systèmes de site distants.  

- Passez en revue les conditions préalables requises pour chaque ordinateur qui héberge un rôle de système de site. Par exemple, pour déployer un système d’exploitation, Configuration Manager utilise le Kit de déploiement et d’évaluation Windows 10 (Windows ADK). Avant d’exécuter le programme d’installation, vous devez télécharger et installer Windows 10 ADK sur le serveur de site et sur chaque ordinateur exécutant une instance du fournisseur SMS.  

Pour plus d’informations sur les plateformes prises en charge et les configurations requises, consultez [Configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations).  

Pour plus d’informations sur l’utilisation de Windows ADK avec Configuration Manager, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="review-the-site-and-hierarchy-status-and-verify-that-there-are-no-unresolved-issues"></a>Examinez l’état des sites et de la hiérarchie et vérifiez qu’il ne reste aucun problème non résolu
Avant de mettre à niveau un site, veillez à résoudre tous les problèmes fonctionnels touchant le serveur de site, le serveur de base de données de site et les rôles de système de site installés sur les ordinateurs distants. Une mise à niveau de site peut échouer en raison de l'existence de problèmes fonctionnels.  

#### <a name="install-all-applicable-critical-updates-for-operating-systems-on-computers-that-host-the-site-the-site-database-server-and-remote-site-system-roles"></a>Installez toutes les mises à jour critiques applicables aux systèmes d’exploitation des ordinateurs hébergeant le site, le serveur de base de données de site et les rôles de système de site distants
Avant de mettre à niveau un site, installez toutes les mises à jour critiques pour chaque système de site concerné. Si vous installez une mise à jour qui nécessite un redémarrage, redémarrez les ordinateurs concernés avant d'entreprendre la mise à jour du Service Pack.  

#### <a name="uninstall-the-site-system-roles-not-supported-by-configuration-manager"></a>Désinstallez les rôles de système de site non pris en charge par Configuration Manager
Les rôles système de site suivants ne sont plus utilisés dans Configuration Manager. Désinstallez-les avant d’effectuer une mise à niveau à partir de System Center 2012 Configuration Manager :  

- Point de gestion hors bande  

- Point du programme de validation d'intégrité système  

#### <a name="disable-database-replicas-for-management-points-at-primary-sites"></a>Désactiver les réplicas de base de données pour les points de gestion des sites principaux
Configuration Manager ne peut pas mettre à niveau un site principal ayant un réplica de base de données pour les points de gestion. Désactivez la réplication de base de données avant de :  

- Créer une sauvegarde de la base de données pour tester la mise à niveau de base de données  

- Mettre à niveau le site de production vers System Center Configuration Manager  

Pour plus d’informations, consultez les articles suivants :  

- System Center 2012 Configuration Manager : [Configurer des réplicas de base de données pour les points de gestion](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846234\(v=technet.10)  

- Configuration Manager, branche actuelle : [Réplicas de base de données pour les points de gestion](/sccm/core/servers/deploy/configure/database-replicas-for-management-points)  

#### <a name="reconfigure-software-update-points-that-use-nlb"></a>Reconfigurez les points de mise à jour logicielle qui utilisent l’équilibrage de la charge réseau (NLB)
Configuration Manager ne peut pas mettre à niveau un site qui utilise un cluster d’équilibrage de la charge réseau pour héberger des points de mise à jour logicielle.  

Si vous utilisez des clusters NLB pour les points de mise à jour logicielle, utilisez PowerShell pour supprimer le cluster NLB. (À compter de System Center 2012 Configuration Manager SP1, aucune option n’existe dans la console Configuration Manager pour configurer un cluster d’équilibrage de la charge réseau.)  

#### <a name="disable-all-site-maintenance-tasks-at-each-site-for-the-duration-of-that-sites-upgrade"></a>Désactivez toutes les tâches de maintenance de site sur chaque site pendant la durée de la mise à niveau de ce site
Avant la mise à niveau vers Configuration Manager, désactivez toutes les tâches de maintenance de site qui peuvent s’exécuter pendant le processus de mise à niveau. Cela inclut, sans toutefois s'y limiter, les tâches suivantes :  

- Serveur de site de sauvegarde  
- Supprimer les anciennes opérations du client  
- Supprimer les données de découverte anciennes  

Si une tâche de maintenance de base de données de site s'exécute pendant le processus de mise à niveau, la mise à niveau de site peut échouer.  

Avant de désactiver une tâche, il convient d'enregistrer sa planification pour pouvoir restaurer sa configuration après avoir accompli la mise à niveau du site. 

Pour plus d'informations sur les tâches de maintenance de site, consultez les articles suivants :  

- System Center 2012 Configuration Manager : [Planification des opérations de site](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/gg712686\(v=technet.10))  

- Configuration Manager, branche actuelle : [Référence des tâches de maintenance](/sccm/core/servers/manage/reference-for-maintenance-tasks)  

#### <a name="run-setup-prerequisite-checker"></a>Exécutez l’outil de vérification des prérequis du programme d’installation
Avant de mettre à niveau un site, exécutez le **vérificateur de la configuration requise** indépendamment du programme d’installation pour vous assurer que votre site est conforme à la configuration requise. Plus tard, quand vous mettez à niveau le site, l’outil de vérification des prérequis s’exécute à nouveau.  

Si vous utilisez le média de base de la version 1606 à partir de la version d’octobre 2016, la vérification indépendante des prérequis évalue le site pour la mise à niveau vers la branche actuelle et LTSB (Long-Term Servicing Branch) de Configuration Manager. Étant donné que certaines fonctionnalités ne sont pas prises en charge par l’édition LTSB, des entrées du fichier *ConfigMgrPrereq.log* peuvent ressembler aux exemples suivants :
- `INFO: The site is a LTSB edition.`
- `Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. Asset Intelligence is not supported on the LTSB edition. You must uninstall the Asset Intelligence synchronization point site system role before you can continue.`

Si vous envisagez de mettre à niveau vers l’édition Current Branch, les erreurs concernant l’édition LTSB peuvent être ignorées en toute sécurité. Elles s’appliquent uniquement si vous envisagez de mettre à niveau vers l’édition LTSB.

Plus tard, lorsque vous exécutez le programme d’installation de Configuration Manager pour effectuer la mise à niveau, la vérification des prérequis s’exécute à nouveau. Elle évalue votre site en fonction de la branche de Configuration Manager que vous choisissez d’installer (branche actuelle ou LTSB). Si vous choisissez d’effectuer une mise à niveau vers la branche actuelle, la vérification ne s’applique pas aux fonctionnalités qui ne sont pas prises en charge par LTSB.

Pour plus d’informations, consultez [Outil de vérification des conditions préalables](/sccm/core/servers/deploy/install/prerequisite-checker) et [Liste des vérifications de la configuration requise](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

#### <a name="download-prerequisite-files-and-redistributable-files-for-configuration-manager"></a>Téléchargez les fichiers prérequis et les fichiers redistribuables pour Configuration Manager
Utilisez le **téléchargeur d’installation** pour télécharger les fichiers redistribuables et prérequis, ainsi que les dernières mises à jour de produit pour Configuration Manager.  

Pour plus d’informations, consultez [Téléchargeur d’installation pour System Center Configuration Manager](/sccm/core/servers/deploy/install/setup-downloader).  

#### <a name="plan-to-manage-server-and-client-languages"></a>Planifier la gestion des langues client et serveur
Quand vous mettez à niveau un site, la mise à niveau de site installe uniquement les versions des modules linguistiques que vous sélectionnez pendant la mise à niveau.  

- Le programme d’installation passe en revue la configuration de langue actuelle de votre site. Il identifie ensuite les modules linguistiques disponibles dans le dossier où vous avez stocké les fichiers prérequis téléchargés précédemment.  

- Vous pouvez confirmer la sélection des modules linguistiques serveur et client actifs ou modifier les sélections pour ajouter ou supprimer la prise en charge de langues.  

- Seuls les modules linguistiques disponibles lorsque vous exécutez le programme d’installation peuvent être sélectionnés.  

> [!NOTE]  
> Vous ne pouvez pas utiliser les modules linguistiques de System Center 2012 Configuration Manager pour activer des langues pour un site de branche actuelle Configuration Manager.  

Pour plus d’informations sur les modules linguistiques, consultez [Modules linguistiques](/sccm/core/servers/deploy/install/language-packs).  

#### <a name="review-considerations-for-site-upgrades"></a>Passez en revue les considérations relatives aux mises à niveau de site
Lorsque vous mettez à niveau un site, certaines fonctionnalités et configurations retrouvent leur configuration par défaut. Pour vous aider à préparer ces modifications et les modifications associées, consultez [Considérations sur la mise à niveau](#bkmk_considerations).  

#### <a name="create-a-backup-of-the-site-database-at-the-central-administration-site-and-primary-sites"></a>Créez une sauvegarde de la base de données du site au niveau du site d’administration centrale et des sites principaux
Avant de mettre à niveau un site, sauvegardez la base de données de site pour être certain de disposer d'une sauvegarde utilisable dans le cadre d'une récupération d'urgence.  

Pour plus d’informations, consultez [Sauvegarde et récupération](/sccm/core/servers/manage/backup-and-recovery).  

#### <a name="back-up-a-customized-configurationmof-file"></a>Sauvegardez un fichier Configuration.mof personnalisé
Si vous utilisez un fichier Configuration.mof personnalisé pour définir des classes de données que vous utilisez avec un inventaire matériel, créez une sauvegarde de ce fichier. Après la mise à niveau, restaurez ce fichier sur votre site. Pour plus d’informations, consultez la page [Guide pratique pour étendre l’inventaire matériel](/sccm/core/clients/manage/inventory/extend-hardware-inventory).  

#### <a name="test-the-database-upgrade-process-on-a-copy-of-the-most-recent-site-database-backup"></a>Testez le processus de mise à niveau de base de données sur une copie de la dernière sauvegarde de la base de données de site
Avant de mettre à niveau un site d’administration centrale ou un site principal Configuration Manager, testez le processus de mise à niveau de base de données de site sur une copie de la base de données de site.  

- Testez des processus de mise à niveau de la base de données du site. Le processus de mise à niveau d’un site peut modifier sa base de données.  

- Bien que le test de mise à niveau ne soit pas obligatoire, il peut identifier des problèmes liés à la mise à niveau avant que votre base de données de production ne soit affectée.  

- Un échec de mise à niveau de base de données de site peut rendre votre base de données de site inutilisable, et une récupération de site peut s’avérer nécessaire pour rétablir les fonctionnalités.  

- Bien que la base de données de site soit partagée entre les sites d’une même hiérarchie, prévoyez de tester la base de données sur chacun des sites concernés avant de procéder à leur mise à niveau.  

- Si vous utilisez des réplicas de base de données pour les points de gestion d’un site principal, désactivez la réplication avant de créer la sauvegarde de la base de données de site.  

Configuration Manager ne prend en charge ni la sauvegarde des sites secondaires, ni le test de mise à niveau d’une base de données de site secondaire.  

L'exécution d'un test de mise à niveau de base de données sur la base de données de site de production n'est pas prise en charge. Cette opération mettrait à niveau la base de données du site et risquerait de rendre votre site inutilisable.  

Pour plus d'informations, voir [Tester la mise à niveau de base de données de site](#bkmk_test).  

#### <a name="restart-the-site-server-and-each-computer-that-hosts-a-site-system-role"></a>Redémarrez le serveur de site et chaque ordinateur qui héberge un rôle de système de site
Effectuez cette action pour vous assurer qu’il n’existe aucune action en attente suite à l’installation récente de mises à jour ou à la configuration requise.  

#### <a name="upgrade-sites"></a>Effectuez la mise à niveau des sites.
En commençant par le site de niveau supérieur dans la hiérarchie, exécutez Setup.exe à partir du média source de Configuration Manager.  

Une fois la mise à niveau du site de niveau supérieur effectuée, vous pouvez commencer la mise à niveau de chaque site enfant. Terminez la mise à niveau de chaque site avant d'entreprendre la mise à niveau du site suivant.  

Tant que tous les sites de la hiérarchie n’ont pas été mis à niveau vers Configuration Manager, celle-ci fonctionne en mode de version mixte.  

Pour plus d’informations sur l’exécution d’une mise à niveau, consultez [Mettre à niveau des sites](#bkmk_upgrade).  


### <a name="after-you-upgrade"></a>Après la mise à niveau :  

Passez en revue ces étapes après avoir effectuer une mise à niveau vers Configuration Manager.

#### <a name="upgrade-stand-alone-configuration-manager-consoles"></a>Mettez à niveau les consoles Configuration Manager autonomes
Par défaut, quand vous mettez à niveau un site d’administration centrale ou un site principal, l’installation met également à niveau la console Configuration Manager installée sur le serveur de site. Mettez à niveau manuellement chaque console installée sur un ordinateur autre que le serveur de site.  

> [!TIP]  
> Fermez chaque console ouverte avant de commencer la mise à niveau.  

Pour plus d’informations, consultez [Installer des consoles Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).  

#### <a name="reconfigure-database-replicas-for-management-points-at-primary-sites"></a>Reconfigurez les réplicas de base de données des points de gestion au niveau des sites principaux
Si vous utilisez des réplicas de base de données pour les points de gestion au niveau des sites principaux, désinstallez ces réplicas avant la mise à niveau du site. Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données des points de gestion.   

Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).  

#### <a name="reconfigure-any-database-maintenance-tasks-you-disabled-before-the-upgrade"></a>Reconfigurez les tâches de maintenance de base de données désactivées avant la mise à niveau
Si vous avez désactivé des [tâches de maintenance de base de données](/sccm/core/servers/manage/reference-for-maintenance-tasks) sur un site avant la mise à niveau, il convient de reconfigurer ces tâches sur le site en utilisant les paramètres existants avant la mise à niveau.  

#### <a name="upgrade-clients"></a>Mettez à niveau les clients.
Une fois que tous vos sites sont mis à niveau vers Configuration Manager, envisagez de mettre à niveau les clients.  

Lorsque vous migrez un client, le logiciel client existant est désinstallé et la nouvelle version du logiciel client est installée. Pour mettre à niveau des clients, vous pouvez appliquer n’importe quelle méthode prise en charge par Configuration Manager.  

> [!TIP]  
> Quand vous mettez à niveau le site de niveau supérieur d’une hiérarchie, le package d’installation du client est également mis à jour sur chaque point de distribution de la hiérarchie. Lorsque vous mettez à niveau un site principal, le package de mise à niveau de client disponible auprès de ce site principal est mis à jour.  

Pour plus d’informations, consultez [Guide pratique pour mettre à niveau des clients sur les ordinateurs Windows](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers).  



## <a name="bkmk_considerations"></a> Considérations sur la mise à niveau  


### <a name="automatic-actions"></a>Actions automatiques

Quand vous effectuez la mise à niveau vers Configuration Manager, les actions suivantes se produisent automatiquement :  

- Une réinitialisation du site. Cette action inclut la réinstallation de tous les rôles système de site.  

- Si le site est le site de niveau supérieur d'une hiérarchie, il met à jour le package d'installation de client sur chaque point de distribution de la hiérarchie. Le site met également à jour les images de démarrage par défaut pour utiliser la nouvelle version du système Windows PE fournie avec le Kit de déploiement et d’évaluation Windows 10. Toutefois, la mise à niveau ne met pas niveau les médias existants pour une utilisation avec le déploiement d'image.  

- Si le site est un site principal, il met à jour le package de mise à niveau de client de ce site.  


### <a name="manual-actions-after-an-upgrade"></a>Actions manuelles après une mise à niveau

Après la mise à niveau d’un site, veillez à effectuer les actions suivantes :  

- Vérifiez que les clients attribués à chaque site principal sont mis à niveau et installez la nouvelle version du client.  

- Mettez à niveau chaque console Configuration Manager qui se connecte au site et qui s’exécute sur un ordinateur distant du serveur de site.  

- Sur les sites principaux où vous utilisez des réplicas de base de données pour les points de gestion, reconfigurez ces réplicas.  

- Une fois le site mis à niveau, mettez à niveau manuellement les médias physiques comme les fichiers ISO pour CD, DVD ou lecteur flash USB. Cela inclut également le média préparé fourni aux fabricants de matériel. Bien que la mise à niveau de site mette à jour les images de démarrage par défaut, elle ne peut pas mettre à niveau ces fichiers multimédias ou les appareils utilisés extérieurs à Configuration Manager.  

- Effectuez la mise à jour des images de démarrage personnalisées quand vous n'avez pas besoin de la version plus ancienne de Windows PE.  


### <a name="actions-that-affect-configurations-and-settings"></a>Actions affectant les configurations et les paramètres**   

Lorsqu'un site est mis à niveau vers Configuration Manager, certaines configurations et certains paramètres ne sont pas conservés après la mise à niveau. Certaines configurations utilisent une nouvelle valeur par défaut. La liste suivante inclut certains paramètres qui ne sont pas conservés ou qui changent :  

- **Centre logiciel**  
    Les valeurs par défaut des éléments suivants du Centre logiciel sont rétablies :  

    - Les heures d'ouverture indiquées dans**Informations professionnelles** sont réinitialisées sur les valeurs par défaut : de **05:00** à **22:00** Monday à Friday.  

    - La valeur de **Maintenance de l'ordinateur** est définie sur **Interrompre les activités du Centre logiciel lorsque mon ordinateur est en mode présentation**.  
    
    - La valeur de **Contrôle à distance** est définie sur la valeur attribuée à l'ordinateur dans les paramètres du client.  

- **Calendriers de synthèse des mises à jour logicielles** : Les calendriers de synthèse personnalisés des mises à jour logicielles ou des groupes de mises à jour logicielles sont réinitialisés à la valeur par défaut (1 heure). Au terme de la mise à niveau, réinitialisez les valeurs de synthèse personnalisées sur la fréquence requise.  



## <a name="bkmk_test"></a> Tester la mise à niveau de base de données de site  

Les informations suivantes s’appliquent uniquement lorsque vous mettez à niveau une version antérieure telle que System Center 2012 Configuration Manager vers la branche actuelle de Configuration Manager.

Avant de mettre à niveau un site, testez une copie de la base de données de ce site pour la mise à niveau.  

Pour tester la base de données en vue d’une mise à niveau, vous devez dans un premier temps restaurer une copie de la base de données du site sur une instance de SQL Server qui n’héberge pas de site Configuration Manager. La version de SQL Server que vous utilisez pour héberger la copie de la base de données doit être prise en charge par Configuration Manager.  

Après avoir restauré la base de données de site, sur l’ordinateur SQL Server, exécutez le programme d’installation de Configuration Manager à partir du dossier du média source pour Configuration Manager. Utilisez l’option de ligne de commande `/TESTDBUPGRADE`.  

Pour plus d’informations, consultez les articles suivants :

- [Sauvegarde d'un site Configuration Manager](/sccm/core/servers/manage/backup-and-recovery)  

- [Options de ligne de commande pour le programme d’installation](/sccm/core/servers/deploy/install/command-line-options-for-setup#bkmk_setup)  

- [Prise en charge des versions de SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions)  

> [!TIP]  
> Si vous intégrez Microsoft Intune à Configuration Manager :  
>   
>  quand vous exécutez un test de mise à niveau de base de données sur une copie de la base de données qui a cinq jours ou plus, vous pouvez recevoir l’un des messages suivants :  
>   
> - WARN : La mise à niveau va forcer la synchronisation complète vers le cloud.  
> - ERROR : La mise à niveau de la base de données va forcer la synchronisation complète vers le cloud.  
>   
> Vous pouvez sans risque ignorer ces deux messages pendant un test de mise à niveau de base de données, car ils ne signalent pas de défaillance ou de problème avec le test de mise à niveau. Ils indiquent plutôt que lors de la mise à niveau réelle, les données du groupe de réplication de base de données **Cloud** peuvent être synchronisées avec Microsoft Intune.  


### <a name="test-a-site-database-for-upgrade"></a>Testez une base de données de site pour la mise à niveau  

Utilisez la procédure suivante sur chaque site d'administration centrale et site principal que vous envisagez de mettre à niveau :  

1. Effectuez une copie de la base de données de site. Restaurez ensuite cette copie sur une instance de SQL Server qui utilise la même édition que la base de données du site et qui n’héberge pas de site Configuration Manager. Par exemple, si la base de données du site s'exécute sur une instance de l'édition Enterprise de SQL Server, veillez à restaurer la base de données sur une instance de SQL Server qui exécute également l'édition Enterprise de SQL Server.  

2. Après avoir restauré la copie de la base de données, exécutez le programme d’installation à partir du média source de la branche actuelle Configuration Manager. Quand vous exécutez le programme d’installation, utilisez l’option de ligne de commande `/TESTDBUPGRADE`. Si l'instance SQL Server qui héberge la copie de la base de données n'est pas l'instance par défaut, fournissez également les arguments de ligne de commande pour identifier l'instance qui héberge la copie de la base de données du site.  

    Par exemple, vous prévoyez de mettre à niveau une base de données de site dont le nom de base de données est SMS_ABC. Vous restaurez une copie de cette base de données de site sur une instance prise en charge de SQL Server ayant pour nom d'instance DBTest. Pour tester une mise à niveau de cette copie de la base de données du site, utilisez la ligne de commande suivante : `Setup.exe /TESTDBUPGRADE DBtest\CM_ABC`  

    Le fichier Setup.exe se trouve à l’emplacement suivant sur le média source Configuration Manager : `SMSSETUP\BIN\X64`  

3. Sur l'instance de SQL Server où vous avez exécuté le test de mise à niveau de base de données, examinez ConfigMgrSetup.log à la racine du lecteur système pour connaître la progression et l'issue du test :  

    - Si le test de la mise à niveau échoue, corrigez les problèmes ayant entraîné l’échec de la mise à niveau de la base de données du site. Puis créez une nouvelle sauvegarde de la base de données du site et testez la mise à niveau de la nouvelle copie de la base de données du site.  

    - Une fois que le processus a abouti, vous pouvez supprimer la copie de la base de données.  

        > [!NOTE]  
        > Il n'est pas possible de restaurer la copie de la base de données du site que vous utilisez dans le cadre du test de mise à niveau afin de l'utiliser comme base de données d'un site quelconque.  

Après avoir mis à niveau une copie de la base de données du site, procédez à la mise à niveau du site Configuration Manager et de sa base de données.  



## <a name="bkmk_upgrade"></a> Effectuez la mise à niveau des sites.  

Vous êtes prêt à mettre à niveau votre site Configuration Manager après avoir terminé les tâches suivantes :
- Effectuer une mise à niveau préalable des configurations pour votre site
- Tester la mise à niveau de la base de données de site sur une copie de base de données
- Télécharger les fichiers requis et les modules linguistiques pour la version que vous prévoyez d’installer

Lorsque vous mettez à niveau un site qui fait partie d'une hiérarchie, vous mettez d'abord à niveau le site situé le plus haut dans la hiérarchie. Ce site de niveau supérieur est soit un site d'administration centrale, soit un site principal autonome. Après avoir effectué la mise à niveau d'un site d'administration centrale, vous pouvez mettre à niveau les sites principaux enfants dans l'ordre que vous voulez. Une fois que vous avez mis à niveau un site principal, vous pouvez mettre à niveau les sites secondaires enfants de ce site ou mettre à niveau d’autres sites principaux avant de mettre à niveau des sites secondaires.  

Pour mettre à niveau un site d’administration centrale ou le site principal, exécutez le programme d’installation à partir du support de source d’installation de Configuration Manager. N'exécutez pas le programme d'installation pour mettre à niveau des sites secondaires. Au lieu de cela, il convient d’utiliser la console Configuration Manager pour mettre à niveau un site secondaire après avoir accompli la mise à niveau de son site parent principal.  

Avant de mettre à niveau un site, fermez la console Configuration Manager sur le serveur du site en attendant que la mise à niveau du site soit terminée. De même, fermez chacune des consoles Configuration Manager qui s’exécutent sur des ordinateurs autres que le serveur du site. Une fois la mise à niveau du site terminée, vous pouvez reconnecter la console. Toutefois, tant que vous n’avez pas mis à niveau une console Configuration Manager vers la nouvelle version de Configuration Manager, cette console ne peut pas afficher certains objets et certaines informations disponibles dans la nouvelle version de Configuration Manager.  


### <a name="upgrade-a-central-administration-site-or-primary-site"></a>Mettre à niveau un site d'administration centrale ou un site principal  

1. Vérifiez que l'utilisateur qui exécute le programme d'installation possède les droits de sécurité suivants :  

    - Droits **Administrateur** locaux sur le serveur du site  

    - Si le serveur de bases de données du site est distant du serveur de site, les droits **Administrateur** locaux sur ce serveur.  

2. Sur le serveur de site, ouvrez le programme suivant : `<ConfigMgSourceMedia>\SMSSETUP\BIN\X64\Setup.exe`. Cette action ouvre l’Assistant Installation de Configuration Manager.  

3. Lisez les informations sur la page **Avant de commencer**, puis sélectionnez **Suivant**.  

4. Sur la page **Mise en route** , sélectionnez **Mettre à niveau ce site Configuration Manager**, puis choisissez **Suivant**.  

5. Sur la page **Clé du produit** :  

    Si vous avez installé précédemment la version d’évaluation de Configuration Manager, vous pouvez sélectionner **Installer l’édition d’évaluation de ce produit**. Entrez votre clé de produit correspondant à l'installation complète de Configuration Manager. Cette action convertit le site en version complète.  

    Vous pouvez également spécifier la **date d’expiration Software Assurance** de votre contrat de licence en guise de rappel pratique pour vous. Si vous n’entrez pas cette valeur pendant l’installation, vous pourrez la spécifier plus tard dans la console Configuration Manager.  

    > [!NOTE]  
    > Microsoft ne valide pas la date d’expiration que vous entrez et ne l’utilise pas pour la validation de la licence. Elle peut vous servir de rappel. Configuration Manager vérifie régulièrement les nouvelles mises à jour logicielles proposées en ligne, et l’état de votre licence Software Assurance doit être actualisé pour être éligible à ces mises à jour supplémentaires.    

    Pour plus d’informations, consultez [Licences et branches](/sccm/core/understand/learn-more-editions).

6. Dans la page **Termes du contrat de licence logiciel Microsoft**, lisez et acceptez les termes du contrat de licence, puis sélectionnez **Suivant**.  

7. Sur la page **Licences requises** , lisez et acceptez les termes du contrat de licence pour les logiciels requis, puis sélectionnez **Suivant**. Le programme d’installation télécharge et installe automatiquement les logiciels sur les systèmes ou les clients du site, si nécessaire. Avant de passer à la page suivante, acceptez tous les termes du contrat.  

8. Sur la page **Téléchargements requis**, spécifiez si le programme d’installation télécharge le dernier contenu sur Internet ou utilise d’anciens fichiers téléchargés. Ce contenu inclut les fichiers redistribuables requis, les modules linguistiques, ainsi que les dernières mises à jour de produit. Si vous avez précédemment téléchargé les fichiers à l'aide du téléchargeur d'installation, sélectionnez **Utiliser des fichiers précédemment téléchargés** , puis spécifiez le dossier de téléchargement. Pour plus d’informations, consultez [Téléchargeur d’installation](/sccm/core/servers/deploy/install/setup-downloader).  

    > [!NOTE]  
    > Si vous utilisez des fichiers téléchargés précédemment, vérifiez que le chemin vers le dossier de téléchargement contient la version la plus récente des fichiers.  

9. Sur la page **Sélection de la langue du serveur** , examinez la liste des langues actuellement installées pour le site. Sélectionnez les langues supplémentaires disponibles sur ce site pour la console Configuration Manager et les rapports. Vous pouvez également effacer les langues que vous ne voulez plus prendre en charge sur ce site. L'anglais est sélectionné par défaut et ne peut pas être supprimé.  

    > [!IMPORTANT]  
    > Chaque version de Configuration Manager ne peut pas utiliser les modules linguistiques d’une version antérieure de Configuration Manager. Pour activer la prise en charge d’une langue sur un site Configuration Manager que vous mettez à niveau, vous devez utiliser la version du module linguistique de cette nouvelle version. Pour exemple, pendant la mise à niveau de System Center 2012 Configuration Manager vers la branche actuelle de Configuration Manager, si la version de la branche actuelle d’un module linguistique n’est pas disponible avec les fichiers prérequis que vous téléchargez, vous ne pouvez pas installer la prise en charge de cette langue.  

10. Sur la page **Sélection de la langue client** , examinez la liste des langues actuellement installées pour le site. Effectuez une sélection parmi les autres langues disponibles sur ce site pour les ordinateurs clients, ou effacez les langues que vous ne voulez plus prendre en charge sur ce site. Précisez si vous souhaitez activer toutes les langues client pour les clients d’appareil mobile, puis cliquez sur **Suivant**. L'anglais est sélectionné par défaut et ne peut pas être supprimé.  

11. Sur la page **Résumé des paramètres**, passez en revue la configuration. Lorsque vous êtes prêt, sélectionnez **Suivant** pour démarrer l'outil de vérification des prérequis et vérifier si le serveur est prêt pour une mise à niveau du site.  

12. Sur la page **Vérification de l'installation préalable** , si aucun problème n'est répertorié, sélectionnez **Suivant** pour mettre à niveau le site et les rôles de système de site. 

    Si l’outil de vérification des prérequis détecte un problème, sélectionnez un élément dans la liste pour plus d'informations sur la résolution du problème. Résolvez tous les éléments de la liste dont l'état est **Erreur** avant de poursuivre l'installation. Après avoir résolu le problème, cliquez sur **Vérifier** pour relancer la vérification des prérequis. Vous pouvez également ouvrir le fichier ConfigMgrPrereq.log à la racine du lecteur système pour passer en revue les résultats de l'outil de vérification des prérequis. Le fichier journal peut contenir des informations supplémentaires qui ne s'affichent pas dans l'interface utilisateur. Pour obtenir la liste des règles et descriptions relatives aux prérequis de l’installation, consultez [Outil de vérification des prérequis](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).

Sur la page **Mettre à niveau** , le programme d'installation affiche l'état de la progression globale. Lorsque le programme d'installation a terminé l'installation du serveur de site principal et du système de site, vous pouvez fermer l'Assistant. La configuration du site se poursuit en arrière-plan.  


### <a name="upgrade-a-secondary-site"></a>Mettre à niveau un site secondaire  

1. Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    - Droits d’**administrateur** local sur le serveur de site secondaire  

    - Rôle de sécurité d’**administrateur d’infrastructure** ou d’**administrateur complet** sur le site principal parent  

    - Droits d'administrateur système (**AS**) sur la base de données de site du site secondaire  

2. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

3. Sélectionnez le site secondaire à mettre à niveau. Sous l’onglet **Accueil** du ruban, dans le groupe **Site**, sélectionnez **Mettre à niveau**.  

4. Sélectionnez **Oui** pour confirmer la décision et lancer la mise à niveau du site secondaire.  

La mise à niveau du site secondaire s’exécute en arrière-plan. Une fois la mise à niveau terminée, vérifiez l’état de la console Configuration Manager. Sélectionnez le serveur du site secondaire puis, sous l'onglet **Accueil** du ruban, dans le groupe **Site**, sélectionnez **Afficher l'état d'installation**.  



## <a name="BKMK_PostUpgrade"></a> Tâches postérieures à la mise à niveau  

Après avoir mis à niveau un site, vous pouvez être amené à effectuer des tâches supplémentaires pour finaliser la mise à niveau ou reconfigurer le site. Ces tâches peuvent inclure les éléments suivants : 
- Mettre à niveau des clients Configuration Manager
- Mettre à jour des consoles Configuration Manager
- Réactiver des réplicas de base de données pour les points de gestion
- Restaurer les paramètres pour les fonctionnalités de Configuration Manager que vous utilisez et qui ne sont pas conservés après la mise à niveau  

