---
title: Mettre à niveau vers System Center Configuration Manager
description: Découvrez les étapes d’exécution d’une mise à niveau sur place réussie à partir d’un site et d’une hiérarchie qui exécute System Center 2012 Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1cea0a54bc4c4c2d69f979bb09d83d7f5fac7706
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342713"
---
# <a name="upgrade-to-system-center-configuration-manager"></a>Mettre à niveau vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez exécuter une mise à niveau sur place pour mettre à niveau System Center Configuration Manager à partir d’un site et d’une hiérarchie qui exécute System Center 2012 Configuration Manager.  

 Avant de procéder à la mise à niveau à partir de System Center 2012 Configuration Manager, vous devez préparer les sites en supprimant des configurations spécifiques qui peuvent empêcher la réussite de l’opération et en suivant la séquence de mise à niveau quand plusieurs sites sont concernés.  

 > [!TIP]
 > Lors de la gestion de l’infrastructure de site et de hiérarchie de System Center Configuration Manager, les termes *mise à niveau*, *mise à jour* et *installation* sont utilisés pour décrire trois concepts distincts. Pour connaître la signification et l’usage de chaque terme, consultez [À propos de la mise à niveau, de la mise à jour et de l’installation de l’infrastructure de site et de hiérarchie](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> Chemins de mise à niveau sur place  

**Mise à niveau vers la version 1802**   
Si vous avez un support de base de référence de version 1802, vous pouvez mettre à niveau les produits suivants vers une version sous licence complète de System Center Configuration Manager version 1802 :   
-     Une installation d’évaluation de System Center Configuration Manager version 1802
-     System Center 2012 Configuration Manager avec Service Pack 1
-     System Center 2012 Configuration Manager avec Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager avec Service Pack 1

**Mise à niveau vers la version 1702**   
Si vous avez un support de base de référence 1702, vous pouvez mettre à niveau les produits suivants vers une version sous licence complète de System Center Configuration Manager version 1702 :   
-     Une installation d’évaluation de System Center Configuration Manager version 1702
-     System Center 2012 Configuration Manager avec Service Pack 1
-     System Center 2012 Configuration Manager avec Service Pack 2
-     System Center 2012 R2 Configuration Manager
-     System Center 2012 R2 Configuration Manager avec Service Pack 1

**Mettre à niveau vers la version 1606**  
Le 15 décembre 2016, le média de base de la version 1606 a été republié afin d’ajouter la prise en charge d’autres scénarios de mise à niveau. Cette nouvelle version prend en charge la mise à niveau des produits suivants vers une version sous licence complète de System Center Configuration Manager version 1606 :  
-   Une installation d’évaluation de System Center Configuration Manager version 1606
-   Une installation de version finale (RC) de System Center Configuration Manager  
-   System Center 2012 Configuration Manager avec Service Pack 1  
-   System Center 2012 Configuration Manager avec Service Pack 2  
-   System Center 2012 R2 Configuration Manager sans Service Pack
-   System Center 2012 R2 Configuration Manager avec Service Pack 1  

Si vous utilisez le média de base de la version 1606 téléchargé avant le 15 décembre 2016, vous pouvez mettre à niveau uniquement les produits suivants vers une version sous licence complète de System Center Configuration Manager version 1606 :
-   Une installation d’évaluation de System Center Configuration Manager version 1606
-   System Center 2012 Configuration Manager avec Service Pack 2
-   System Center 2012 R2 Configuration Manager avec Service Pack 1

<!-- Version 1511 has now dropped out of support
**Upgrade to version 1511**  
When you have version 1511 baseline media, you can upgrade the following to a fully licensed  version of System Center Configuration Manager version 1511:  
-   An evaluation install of System Center Configuration Manager version 1511
-   A release candidate install of System Center Configuration Manager  
-   System Center 2012 Configuration Manager with Service Pack 1  
-   System Center 2012 Configuration Manager with Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center 2012 R2 Configuration Manager with Service Pack 1  
-->


> [!TIP]  
>  Une mise à niveau à partir d’une version de System Center 2012 Configuration Manager vers Current Branch peut vous permettre de simplifier votre processus de mise à niveau. Pour plus d'informations, consultez :  
>   
>  -   La section [Versions de base et de mise à jour](../../../../core/servers/manage/updates.md#bkmk_Baselines) dans [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [Dossier CD.Latest pour System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **Les éléments suivants ne sont pas pris en charge :**  
-   La mise à niveau d’une préversion technique de System Center Configuration Manager vers une installation sous licence complète.  Une version d’évaluation technique peut uniquement être mise à niveau vers une version ultérieure de la version d’évaluation technique.  

-   La migration d’une version Technical Preview vers une version sous licence complète n’est pas pris en charge.  

##  <a name="bkmk_checklist"></a> Listes de vérification de mise à niveau  
 Les listes de vérification suivantes peuvent vous aider à planifier une mise à niveau vers System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Avant la mise à niveau :  

**Passez en revue votre environnement System Center 2012 Configuration Manager** et corrigez les problèmes comme détaillé dans l’article KB4018655 : [Les clients Configuration Manager se réinstallent toutes les cinq heures en raison d’une tâche périodique de nouvelle tentative, ce qui peut provoquer une mise à niveau du client par inadvertance](https://support.microsoft.com/help/4018655).

**Vérifiez que votre environnement informatique répond aux configurations prises en charge** nécessaires à la mise à niveau vers System Center Configuration Manager SP1 :  

Passez en revue les systèmes d’exploitation de serveur utilisés pour héberger les rôles de système de site :  

-   Certains anciens systèmes d’exploitation pris en charge par System Center 2012 Configuration Manager ne sont pas pris en charge par System Center Configuration Manager, et les rôles système de site sur ces systèmes d’exploitation doivent être déplacés ou supprimés avant la mise à niveau. Consultez la documentation [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).   
-   L’outil de vérification des conditions préalables pour Configuration Manager ne vérifie pas les prérequis pour les rôles de système de site sur le serveur de site ou sur les systèmes de site distants.  

Passez en revue les conditions préalables requises pour chaque ordinateur qui héberge un rôle de système de site :  

-   Par exemple, pour déployer un système d’exploitation, System Center Configuration Manager utilise le Kit de déploiement et d’évaluation Windows 10 (Windows ADK). Avant d’exécuter le programme d’installation, vous devez télécharger et installer Windows 10 ADK sur le serveur de site et sur chaque ordinateur exécutant une instance du fournisseur SMS.  

Pour obtenir des informations générales sur les plateformes prises en charge et les configurations requises, voir [Configurations prises en charge pour System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Pour plus d’informations sur l’utilisation de Windows ADK avec Configuration Manager, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation dans System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

**Examinez l’état des sites et de la hiérarchie et vérifiez qu’il ne reste aucun problème non résolu :**  
Avant de mettre à niveau un site, veillez à résoudre tous les problèmes fonctionnels touchant le serveur de site, le serveur de base de données de site et les rôles de système de site installés sur les ordinateurs distants. Une mise à niveau de site peut échouer en raison de l'existence de problèmes fonctionnels.  

**Installez toutes les mises à jour critiques applicables aux systèmes d’exploitation des ordinateurs hébergeant le site, le serveur de base de données de site et les rôles de système de site distants :**  
Avant de mettre à niveau un site, installez toutes les mises à jour critiques pour chaque système de site concerné. Si vous installez une mise à jour qui nécessite un redémarrage, redémarrez les ordinateurs concernés avant d'entreprendre la mise à jour du Service Pack.  

Pour plus d'informations, voir [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Désinstallez les rôles de système de site non pris en charge par System Center Configuration Manager :**  
Les rôles système de site suivants ne sont plus utilisés dans System Center Configuration Manager et doivent être désinstallées avant la mise à niveau depuis System Center 2012 Configuration Manager :  

-   Point de gestion hors bande  
-   Point du programme de validation d'intégrité système  

**Désactivez les réplicas de base de données pour les points de gestion au niveau des sites principaux :**  
Configuration Manager ne peut pas réussir la mise à niveau d’un site principal ayant un réplica de base de données activé pour les points de gestion. Désactivez la réplication de base de données avant de :  

-   Créer une sauvegarde de la base de données pour tester la mise à niveau de base de données  
-   Mettre à niveau le site de production vers System Center Configuration Manager  

Pour plus d'informations, consultez :  
-   System Center 2012 Configuration Manager : [Configurer des réplicas de base de données pour les points de gestion](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager : [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)  

**Reconfigurez les points de mise à jour logicielle qui utilisent l’équilibrage de la charge réseau (NLB) :**  
Configuration Manager ne peut pas mettre à niveau un site qui utilise un cluster d’équilibrage de la charge réseau pour héberger des points de mise à jour logicielle.  

Si vous utilisez des clusters NLB pour les points de mise à jour logicielle, utilisez PowerShell pour supprimer le cluster NLB. (À compter de System Center 2012 Configuration Manager SP1, aucune option n’existe dans la console Configuration Manager pour configurer un cluster d’équilibrage de la charge réseau.)  

**Désactivez toutes les tâches de maintenance de site sur chaque site pendant la durée de la mise à niveau de ce site :**  
Avant la mise à niveau vers System Center Configuration Manager, désactivez toutes les tâches de maintenance de site qui peuvent s’exécuter pendant le processus de mise à niveau. Cela inclut, sans toutefois s'y limiter, les tâches suivantes :  

-   Serveur de site de sauvegarde  
-   Supprimer les anciennes opérations du client  
-   Supprimer les données de découverte anciennes  

Lorsqu'une tâche de maintenance de base de données de site s'exécute pendant le processus de mise à niveau, la mise à niveau de site peut échouer.  

Avant de désactiver une tâche, il convient d'enregistrer sa planification pour pouvoir restaurer sa configuration après avoir accompli la mise à niveau du site.  

Pour plus d’informations sur les tâches de maintenance de site, consultez :  

-   System Center 2012 Configuration Manager :  [Planification des tâches de maintenance pour Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center Configuration Manager : [Informations de référence sur les tâches de maintenance pour System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md)  

**Exécutez l’outil de vérification de la configuration requise.**:  
Avant de mettre à niveau un site, vous pouvez exécuter le **vérificateur de la configuration requise** indépendamment du programme d’installation pour vous assurer que votre site est conforme à la configuration requise. Plus tard, quand vous mettez à niveau le site, l’outil de vérification des prérequis s’exécute à nouveau.  

Si vous utilisez le média de base de la version 1606 à partir de la version d’octobre 2016, la vérification indépendante des prérequis évalue le site pour la mise à niveau vers Current Branch et LTSB (Long-Term Servicing Branch) de System Center Configuration Manager. Étant donné que certaines fonctionnalités ne sont pas prises en charge par l’édition LTSB, des entrées du fichier *ConfigMgrPrereq.log* peuvent ressembler à ce qui suit :
 - INFO : Le site est une édition LTSB.
 - Rôle de système de site non pris en charge « Point de synchronisation Asset Intelligence » pour l’édition LTSB ;    Erreur ;    Configuration Manager a détecté que le « Point de synchronisation Asset Intelligence » est installé. Asset Intelligence n’est pas pris en charge dans l’édition LTSB. Vous devez désinstaller le rôle de système de site du point de synchronisation Asset Intelligence pour pouvoir continuer.

Si vous envisagez de mettre à niveau vers l’édition Current Branch, les erreurs concernant l’édition LTSB peuvent être ignorées en toute sécurité. Elles s’appliquent uniquement si vous envisagez de mettre à niveau vers l’édition LTSB.

Plus tard, quand vous exécutez le programme d’installation de Configuration Manager pour effectuer la mise à niveau, la vérification des prérequis s’exécute à nouveau et évalue votre site en fonction de l’édition de System Center Configuration Manager que vous choisissez d’installer (Current Branch ou LTSB). Si vous choisissez de mettre à niveau vers Current Branch, la vérification des fonctionnalités qui ne sont pas prises en charge par LTSB n’est pas exécutée.

Pour plus d’informations, consultez [Outil de vérification des conditions préalables pour System Center Configuration Manager](/sccm/core/servers/deploy/install/prerequisite-checker) et [Liste des vérifications de la configuration requise pour System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Téléchargez les fichiers prérequis et les fichiers redistribuables pour System Center Configuration Manager :**    
Utilisez le **téléchargeur d’installation** pour télécharger les fichiers redistribuables et prérequis, ainsi que les dernières mises à jour de produit pour System Center Configuration Manager.  

Pour plus d’informations, consultez [Téléchargeur d’installation pour System Center Configuration Manager](/sccm/core/servers/deploy/install/setup-downloader).  

**Planifier la gestion des langues client et serveur**:  
Quand vous mettez à niveau un site, la mise à niveau de site installe uniquement les versions des modules linguistiques que vous sélectionnez pendant la mise à niveau.  

-   Le programme d’installation examine la configuration de langue actuelle de votre site et identifie les modules linguistiques disponibles dans le dossier où vous avez stocké les fichiers prérequis téléchargés précédemment.  
-   Vous pouvez alors confirmer la sélection des modules linguistiques serveur et client actifs ou modifier les sélections pour ajouter ou supprimer la prise en charge de langues.  
-   Vous pouvez sélectionner uniquement les modules linguistiques qui sont disponibles quand vous exécutez le programme d’installation (que vous obtenez avec les fichiers prérequis téléchargés).  

> [!NOTE]  
>  Vous ne pouvez pas utiliser les modules linguistiques de System Center 2012 Configuration Manager pour activer des langues pour un site System Center Configuration Manager.  

Pour plus d’informations sur les modules linguistiques, consultez [Modules linguistiques dans System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Passez en revue les considérations relatives aux mises à niveau de site**:  
Lorsque vous mettez à niveau un site, certaines fonctionnalités et configurations retrouvent leur configuration par défaut. Pour vous aider à préparer ces modifications et les modifications associées, passez en revue les informations contenues dans  [Considérations sur la mise à niveau](#bkmk_considerations).  

**Créez une sauvegarde de la base de données du site au niveau du site d’administration centrale et des sites principaux :**  
Avant de mettre à niveau un site, sauvegardez la base de données de site pour être certain de disposer d'une sauvegarde utilisable dans le cadre d'une récupération d'urgence.  

Consultez [Sauvegarde et récupération pour System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Sauvegardez un fichier Configuration.mof personnalisé**:  
Si vous utilisez un fichier Configuration.mof personnalisé pour définir des classes de données que vous utilisez avec un inventaire matériel, créez une sauvegarde de ce fichier avant la mise à niveau du site. Après la mise à niveau, restaurez ce fichier sur votre site. Pour plus d’informations sur l’utilisation de ce fichier, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Testez le processus de mise à niveau de base de données sur une copie de la dernière sauvegarde de la base de données de site :**  
Avant de mettre à niveau un site d’administration centrale ou un site principal Configuration Manager, testez le processus de mise à niveau de base de données de site sur une copie de la base de données de site.  

-   Vous devez tester le processus de mise à niveau de base de données de site, car quand vous mettez à niveau un site, la base de données peut être modifiée.  
-   Bien que le test de mise à niveau ne soit pas obligatoire, il peut identifier des problèmes liés à la mise à niveau avant que votre base de données de production ne soit affectée.  
-   Un échec de mise à niveau de base de données de site peut rendre votre base de données de site inutilisable, et une récupération de site peut s’avérer nécessaire pour rétablir les fonctionnalités.  
-   Bien que la base de données de site soit partagée entre les sites d’une même hiérarchie, prévoyez de tester la base de données sur chacun des sites concernés avant de procéder à leur mise à niveau.  
-   Si vous utilisez des réplicas de base de données pour les points de gestion d’un site principal, désactivez la réplication avant de créer la sauvegarde de la base de données de site.  

Configuration Manager ne prend en charge ni la sauvegarde des sites secondaires, ni le test de mise à niveau d’une base de données de site secondaire.  

L'exécution d'un test de mise à niveau de base de données sur la base de données de site de production n'est pas prise en charge. Cette opération mettrait à niveau la base de données du site et risquerait de rendre votre site inutilisable.  

Pour plus d'informations, voir [Tester la mise à niveau de base de données de site](#bkmk_test).  

**Redémarrez le serveur de site et chaque ordinateur qui héberge un rôle de système de site** :  
Cela permet de vérifier qu’aucune action liée à une installation récente de mises à jour ou aux prérequis n’est en cours. Il s’agit d’un processus interne propre à l’entreprise.  

**Effectuez la mise à niveau des sites.**:  
En commençant par le site de niveau supérieur dans la hiérarchie, exécutez Setup.exe à partir du média source de System Center Configuration Manager.  

Une fois la mise à niveau du site de niveau supérieur effectuée, vous pouvez commencer la mise à niveau de chaque site enfant. Terminez la mise à niveau de chaque site avant de commencer la mise à niveau du site suivant.  

Tant que tous les sites de la hiérarchie n’ont pas été mis à niveau vers System Center Configuration Manager, celle-ci fonctionne en mode de version mixte.  

Pour plus d’informations sur l’exécution d’une mise à niveau, consultez [Mettre à niveau des sites](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Après la mise à niveau :  
**Mettez à niveau les consoles Configuration Manager autonomes** :  
Par défaut, quand vous mettez à niveau un site d’administration centrale ou un site principal, l’installation met également à niveau la console Configuration Manager installée sur le serveur de site. Toutefois, vous devez mettre à niveau manuellement chaque console installée sur un ordinateur autre que le serveur de site.  

> [!TIP]  
>  Fermez chaque console ouverte avant de commencer la mise à niveau.  

Pour plus d’informations, consultez [Installer des consoles System Center Configuration Manager](../../../../core/servers/deploy/install/install-consoles.md).  

**Reconfigurez les réplicas de base de données des points de gestion au niveau des sites principaux :**  
Si vous utilisez des réplicas de base de données pour les points de gestion au niveau des sites principaux, vous devez désinstaller ces réplicas avant la mise à niveau du site. Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données des points de gestion.   
Pour plus d’informations, consultez  [Réplicas de base de données pour les points de gestion de System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigurez les tâches de maintenance de base de données désactivées avant la mise à niveau :**  
Si vous avez désactivé des [tâches de maintenance de base de données pour System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) sur un site avant la mise à niveau, reconfigurez ces tâches sur le site en utilisant les paramètres existants avant la mise à niveau.  

**Mettez à niveau les clients.**:  
Une fois que tous vos sites sont mis à niveau vers System Center Configuration Manager, envisagez de mettre à niveau les clients.  

Lorsque vous migrez un client, le logiciel client existant est désinstallé et la nouvelle version du logiciel client est installée. Pour mettre à niveau des clients, vous pouvez appliquer n’importe quelle méthode prise en charge par Configuration Manager.  

> [!TIP]  
>  Quand vous mettez à niveau le site de niveau supérieur d’une hiérarchie, le package d’installation du client est également mis à jour sur chaque point de distribution de la hiérarchie. Lorsque vous mettez à niveau un site principal, le package de mise à niveau de client disponible auprès de ce site principal est mis à jour.  

Pour plus d’informations sur la mise à niveau de clients existants et sur la façon d’installer de nouveaux clients, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Considérations sur la mise à niveau  
**Actions automatiques** :  
Quand vous effectuez la mise à niveau vers System Center Configuration Manager, les actions suivantes se produisent automatiquement :  

-   Le site opère une réinitialisation de site, qui comprend la réinstallation de tous les rôles de système de site.  
-   Si le site est le site de niveau supérieur d'une hiérarchie, il met à jour le package d'installation de client sur chaque point de distribution de la hiérarchie. Le site met également à jour les images de démarrage par défaut pour utiliser la nouvelle version du système Windows PE fournie avec le Kit de déploiement et d’évaluation Windows 10. Toutefois, la mise à niveau ne met pas niveau les médias existants pour une utilisation avec le déploiement d'image.  
-   Si le site est un site principal, il met à jour le package de mise à niveau de client de ce site.  

**Actions manuelles de l’utilisateur administratif après une mise à niveau**   
Après la mise à niveau d’un site, effectuez les actions suivantes :  

-   Vérifiez que les clients qui sont attribués à chaque site principal sont mis à niveau et installez le logiciel client correspondant à la nouvelle version.  
-   Mettez à niveau chaque console Configuration Manager qui se connecte au site et qui s’exécute sur un ordinateur distant du serveur de site.  
-   Sur les sites principaux où vous utilisez des réplicas de base de données pour les points de gestion, reconfigurez ces réplicas.  
-   Une fois le site mis à niveau, vous devez effectuer une mise à niveau manuelle des médias physiques tels que les fichiers ISO pour les CD et les DVD ou les disques mémoire flash USB, ou les médias préparés utilisés pour les déploiements de Windows To Go ou fournis par des fournisseurs de matériel. Bien que la mise à niveau de site mette à jour les images de démarrage par défaut, elle ne peut pas mettre à niveau ces fichiers multimédias ou les appareils utilisés extérieurs à Configuration Manager.  
-   Effectuez la mise à jour des images de démarrage autres que les images par défaut quand vous n'avez pas besoin de la version d'origine (plus ancienne) de Windows PE.  

**Actions affectant les configurations et les paramètres**   
Quand un site est mis à niveau vers System Center Configuration Manager, certaines configurations et certains paramètres ne sont pas conservés après la mise à niveau ou utilisent une nouvelle configuration par défaut. Le tableau ci-dessous répertorie des paramètres qui ne sont pas conservés ou sont modifiés, et fournit des informations qui vous aideront à anticiper ce problème dans le cadre d’une mise à niveau de site :  

-   **Centre logiciel :**  
    Les valeurs par défaut des éléments suivants du Centre logiciel sont rétablies :  
    -   Les heures d'ouverture indiquées dans**Informations professionnelles** sont réinitialisées sur les valeurs par défaut : de **05:00** à **22:00** Monday à Friday.  
    -   La valeur de **Maintenance de l'ordinateur** est définie sur **Interrompre les activités du Centre logiciel lorsque mon ordinateur est en mode présentation**.  
    -   La valeur de **Contrôle à distance** est définie sur la valeur attribuée à l'ordinateur dans les paramètres du client.  
-   **Calendriers de synthèse des mises à jour logicielles :**  
     Les calendriers de synthèse personnalisés des mises à jour logicielles ou des groupes de mises à jour logicielles sont réinitialisés à la valeur par défaut (1 heure). Au terme de la mise à niveau, réinitialisez les valeurs de synthèse personnalisées sur la fréquence requise.  

##  <a name="bkmk_test"></a> Tester la mise à niveau de base de données de site  
Les informations suivantes s’appliquent uniquement lorsque vous mettez à niveau une version antérieure telle que System Center 2012 Configuration Manager vers System Center Configuration Manager.

Avant de mettre à niveau un site, testez une copie de la base de données de ce site pour la mise à niveau.  

Pour tester la base de données en vue d’une mise à niveau, vous devez dans un premier temps restaurer une copie de la base de données du site sur une instance de SQL Server qui n’héberge pas de site Configuration Manager. La version de SQL Server que vous utilisez pour héberger la copie de la base de données doit être prise en charge par la version de Configuration Manager, qui est la source de la copie de la base de données.  

Ensuite, après avoir restauré la base de données de site, sur l’ordinateur SQL Server, exécutez le programme d’installation de Configuration Manager à partir du dossier du support de source d’installation de System Center Configuration Manager avec l’option de ligne de commande **/TESTDBUPGRADE**.  

-   Pour plus d’informations sur la façon de créer et de restaurer une sauvegarde de base de données de site, consultez [Options de ligne de commande pour le programme d’installation](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Pour plus d’informations sur l’option de ligne de commande **/TESTDBUPGRADE**, consultez le tableau dans [Options de ligne de commande pour le programme d’installation](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  
-   Pour plus d’informations sur les versions de SQL Server prises en charge, consultez la rubrique [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

> [!TIP]  
>  Si vous intégrez Microsoft Intune à Configuration Manager :  
>   
>  quand vous exécutez un test de mise à niveau de base de données sur une copie de la base de données qui a cinq jours ou plus, vous pouvez recevoir l’un des messages suivants :  
>   
>  -   Avertissement : la mise à niveau va forcer la synchronisation complète vers le cloud.  
>  -   Erreur : la mise à niveau de la base de données va forcer la synchronisation complète vers le cloud.  
>   
> Vous pouvez sans risque ignorer ces deux messages pendant un test de mise à niveau de base de données, car ils ne signalent pas de défaillance ou de problème avec le test de mise à niveau. Ils indiquent plutôt que lors de la mise à niveau réelle, les données du groupe de réplication de base de données **Cloud** peuvent être synchronisées avec Microsoft Intune.  

Utilisez la procédure suivante sur chaque site d'administration centrale et site principal que vous envisagez de mettre à niveau.  

#### <a name="to-test-a-site-database-for-upgrade"></a>Pour tester une base de données de site pour la mise à niveau  

1.  Créez une copie de la base de données du site, puis restaurez cette copie sur une instance de SQL Server qui utilise la même édition que la base de données du site et qui n’héberge pas de site Configuration Manager. Par exemple, si la base de données du site s'exécute sur une instance de l'édition Enterprise de SQL Server, veillez à restaurer la base de données sur une instance de SQL Server qui exécute également l'édition Enterprise de SQL Server.  

2.  Après avoir restauré la copie de la base de données, exécutez le programme d’installation à partir du support de source d’installation de System Center Configuration Manager. Quand vous exécutez le programme d’installation, utilisez l’option de ligne de commande **/TESTDBUPGRADE** . Si l'instance SQL Server qui héberge la copie de la base de données n'est pas l'instance par défaut, vous devez également fournir les arguments de ligne de commande pour identifier l'instance qui héberge la copie de la base de données du site.  

     Par exemple, vous prévoyez de mettre à niveau une base de données de site dont le nom de base de données est SMS_ABC. Vous restaurez une copie de cette base de données de site sur une instance prise en charge de SQL Server ayant pour nom d'instance DBTest. Pour tester une mise à niveau de cette copie de la base de données du site, utilisez la ligne de commande suivante : **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     Vous trouverez Setup.exe à l’emplacement suivant sur le média source de System Center Configuration Manager : **SMSSETUP\BIN\X64**.  

3.  Sur l'instance de SQL Server où vous avez exécuté le test de mise à niveau de base de données, examinez ConfigMgrSetup.log à la racine du lecteur système pour connaître la progression et l'issue du test :  

    -   Si le test de mise à niveau de la base de données du site échoue, remédiez aux problèmes liés à cet échec, créez une sauvegarde de la base de données du site, puis testez la mise à niveau de la nouvelle copie de la base de données du site.  
    -   Une fois que le processus a abouti, vous pouvez supprimer la copie de la base de données.  

        > [!NOTE]  
        >  Il n'est pas possible de restaurer la copie de la base de données du site que vous utilisez dans le cadre du test de mise à niveau afin de l'utiliser comme base de données d'un site quelconque.  

Après avoir mis à niveau une copie de la base de données du site, procédez à la mise à niveau du site Configuration Manager et de sa base de données.  

##  <a name="bkmk_upgrade"></a> Effectuez la mise à niveau des sites.  
Dès lors que vous avez mené à bien les tâches de configuration préalables à la mise à niveau de votre site, testé la mise à niveau de la base de données du site sur une copie de la base de données, puis téléchargé les fichiers et les modules linguistiques prérequis pour la version du Service Pack que vous prévoyez d’installer, vous êtes prêt à mettre à niveau votre site Configuration Manager.  

Lorsque vous mettez à niveau un site qui fait partie d'une hiérarchie, vous mettez d'abord à niveau le site situé le plus haut dans la hiérarchie. Ce site de niveau supérieur est soit un site d'administration centrale, soit un site principal autonome. Après avoir effectué la mise à niveau d'un site d'administration centrale, vous pouvez mettre à niveau les sites principaux enfants dans l'ordre que vous voulez. Une fois que vous avez mis à niveau un site principal, vous pouvez mettre à niveau les sites secondaires enfants de ce site ou mettre à niveau d’autres sites principaux avant de mettre à niveau des sites secondaires.  

Pour mettre à niveau un site d’administration centrale ou le site principal, vous exécutez le programme d’installation à partir du support de source d’installation de System Center Configuration Manager. Toutefois, il n'est pas nécessaire d'exécuter le programme d'installation pour mettre à niveau des sites secondaires. Au lieu de cela, il convient d’utiliser la console Configuration Manager pour mettre à niveau un site secondaire après avoir accompli la mise à niveau de son site parent principal.  

Avant de mettre à niveau un site, fermez la console Configuration Manager installée sur le serveur du site en attendant que la mise à niveau du site soit terminée. De même, fermez chacune des consoles Configuration Manager qui s’exécutent sur des ordinateurs autres que le serveur du site. Une fois la mise à niveau du site terminée, vous pouvez reconnecter la console. Toutefois, tant que vous n’avez pas mis à niveau une console Configuration Manager vers la nouvelle version de Configuration Manager, cette console ne peut pas afficher certains objets et certaines informations disponibles dans la nouvelle version de Configuration Manager.  

Utilisez les procédures suivantes pour mettre à niveau des sites Configuration Manager :  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>Pour mettre à niveau un site d'administration centrale ou un site principal  

1.  Vérifiez que l'utilisateur qui exécute le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d'administrateur local sur l'ordinateur serveur du site.  
    -   Droits d'administrateur local sur le serveur de base de données de site distant du site, s'il est distant.    </br></br>

2.  Sur l’ordinateur serveur de site, ouvrez l’Explorateur Windows et accédez à **&lt;SupportSourceInstallationConfigMg\>\SMSSETUP\BIN\X64**.  

3.  Double-cliquez sur **Setup.exe**. L’Assistant Installation de Configuration Manager s’ouvre.  

4.  Dans la page **Avant de commencer** , cliquez sur **Suivant**.  

5.  Sur la page **Mise en route** , sélectionnez **Mettre à niveau ce site Configuration Manager**, puis cliquez sur **Suivant**.  

6.  Sur la page **Clé du produit** , cliquez sur **Suivant**.  

     Si vous avez précédemment installé la version d’évaluation de Configuration Manager, vous pouvez sélectionner **Installer la version illimitée de ce produit avec votre clef de licence**, puis entrer votre clé de produit correspondant à l’installation complète de Configuration Manager pour convertir le site en version complète.  

     À partir de la version d’octobre 2016 du support de la base de référence de la version 1606 de System Center Configuration Manager, vous pouvez spécifier la date d’expiration de votre contrat Software Assurance. Vous avez également la possibilité de spécifier la **date d’expiration Software Assurance** de votre contrat de licence en guise de rappel pratique pour vous. Si vous ne l’entrez pas pendant l’installation, vous pouvez la spécifier ultérieurement depuis la console Configuration Manager.

     >  [!NOTE]   
     >  Microsoft ne valide pas la date d’expiration que vous entrez et ne l’utilise pas pour la validation de la licence.  Vous pouvez ainsi l’utiliser en guise de rappel de votre date d’expiration. Ce rappel s’avère pratique car Configuration Manager vérifie régulièrement les nouvelles mises à jour logicielles proposées en ligne et l’état de votre licence Software Assurance doit être actualisé pour prétendre à l’utilisation de ces mises à jour supplémentaires.    

     Pour plus d’informations, consultez [Licences et branches pour System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

7.  Sur la page **Termes du contrat de licence logiciel Microsoft** , lisez et acceptez les termes du contrat de licence, puis cliquez sur **Suivant**.  

8.  Sur la page **Licences requises** , lisez et acceptez les termes du contrat de licence pour les logiciels requis, puis cliquez sur **Suivant**. Le programme d'installation télécharge et installe automatiquement les logiciels sur les systèmes ou les clients du site, si nécessaire. Vous devez activer toutes les cases à cocher pour passer à la page suivante.  

9. Sur la page **Téléchargements requis** , précisez si le programme d'installation doit télécharger les derniers fichiers redistribuables requis, les modules linguistiques et les dernières mises à jour de produit à partir d'Internet ou utilisez les fichiers téléchargés précédemment, puis cliquez sur **Suivant**. Si vous avez précédemment téléchargé les fichiers à l'aide du téléchargeur d'installation, sélectionnez **Utiliser des fichiers précédemment téléchargés** , puis spécifiez le dossier de téléchargement. Pour plus d’informations, consultez [Téléchargeur d’installation](/sccm/core/servers/deploy/install/setup-downloader).

    > [!NOTE]  
    >  Si vous utilisez des fichiers téléchargés précédemment, vérifiez que le chemin vers le dossier de téléchargement contient la version la plus récente des fichiers.  

10. Sur la page **Sélection de la langue du serveur** , examinez la liste des langues actuellement installées pour le site. Effectuez une sélection parmi les autres langues disponibles sur ce site pour la console Configuration Manager et les rapports, ou effacez les langues que vous ne souhaitez plus prendre en charge sur ce site, puis cliquez sur **Suivant**. L'anglais est sélectionné par défaut et ne peut pas être supprimé.  

    > [!IMPORTANT]  
    >  Chaque version de Configuration Manager ne peut pas utiliser les modules linguistiques d’une version antérieure de Configuration Manager. Pour activer la prise en charge d’une langue sur un site Configuration Manager que vous mettez à niveau, vous devez utiliser la version du module linguistique de cette nouvelle version. Pour exemple, pendant la mise à niveau de System Center 2012 Configuration Manager vers System Center Configuration Manager, si la version System Center Configuration Manager d’un module linguistique n’est pas disponible avec les fichiers prérequis que vous téléchargez, la prise en charge de cette langue ne peut pas être installée.  

11. Sur la page **Sélection de la langue client** , examinez la liste des langues actuellement installées pour le site. Effectuez une sélection parmi les autres langues disponibles sur ce site pour les ordinateurs clients, ou effacez les langues que vous ne voulez plus prendre en charge sur ce site. Précisez si vous souhaitez activer toutes les langues client pour les clients d’appareil mobile, puis cliquez sur **Suivant**. L'anglais est sélectionné par défaut et ne peut pas être supprimé.  

    > [!IMPORTANT]  
    >  Chaque version de Configuration Manager ne peut pas utiliser les modules linguistiques d’une version antérieure de Configuration Manager. Pour activer la prise en charge d’une langue sur un site Configuration Manager que vous mettez à niveau, vous devez utiliser la version du module linguistique de cette nouvelle version. Pour exemple, pendant la mise à niveau de System Center 2012 Configuration Manager vers System Center Configuration Manager, si la version System Center Configuration Manager d’un module linguistique n’est pas disponible avec les fichiers prérequis que vous téléchargez, la prise en charge de cette langue ne peut pas être installée.  

12. Sur la page **Résumé des paramètres** , cliquez sur **Suivant** pour démarrer l'outil de vérification des prérequis et vérifier si le serveur est prêt pour une mise à niveau du site.  

13. Sur la page **Vérification de l'installation préalable** , si aucun problème n'est répertorié, cliquez sur **Suivant** pour mettre à niveau le site et les rôles de système de site. Lorsque l’outil de vérification des prérequis détecte un problème, cliquez sur un élément dans la liste pour plus d'informations sur la résolution du problème. Résolvez tous les éléments de la liste dont l'état est **Erreur** avant de poursuivre l'installation. Après avoir résolu le problème, cliquez sur **Vérifier** pour relancer la vérification des prérequis. Vous pouvez également ouvrir le fichier ConfigMgrPrereq.log à la racine du lecteur système pour passer en revue les résultats de l'outil de vérification des prérequis. Le fichier journal peut contenir des informations supplémentaires qui ne s'affichent pas dans l'interface utilisateur. Pour obtenir la liste des règles et descriptions relatives aux prérequis de l’installation, consultez [Outil de vérification des prérequis](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

Sur la page **Mettre à niveau** , le programme d'installation affiche l'état de la progression globale. Lorsque le programme d'installation a terminé l'installation du serveur de site principal et du système de site, vous pouvez fermer l'Assistant. La configuration du site se poursuit en arrière-plan.  

#### <a name="to-upgrade-a-secondary-site"></a>Pour mettre à niveau un site secondaire  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d'administrateur local sur l'ordinateur du site secondaire.  
    -   Rôle de sécurité d'administrateur d'infrastructure ou d'administrateur complet sur le site principal parent.  
    -   Droits d'administrateur système sur la base de données de site du site secondaire.  
    </br>
2.  Dans la console Configuration Manager, cliquez sur **Administration**.  

3.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

4.  Sélectionnez le site secondaire à mettre à niveau puis, sous l'onglet **Accueil** , dans le groupe **Site** , cliquez sur **Mettre à niveau**.  

5.  Cliquez sur **Oui** pour confirmer la décision et lancer la mise à niveau du site secondaire.  

La mise à niveau du site secondaire progresse en arrière-plan. Une fois la mise à niveau terminée, vous pouvez vérifier l’état de la console Configuration Manager. Pour ce faire, sélectionnez le serveur du site secondaire puis, sous l'onglet **Accueil** , dans le groupe **Site** , cliquez sur **Afficher l'état d'installation**.  

##  <a name="BKMK_PostUpgrade"></a> Exécuter les étapes de post-mise à niveau  
Après avoir mis à niveau un site vers un nouveau Service Pack, vous pouvez être amené à effectuer des tâches supplémentaires pour finaliser la mise à niveau ou reconfigurer le site. Ces tâches peuvent consister notamment à mettre à niveau des clients Configuration Manager ou des consoles Configuration Manager, à réactiver des réplicas de base de données pour des points de gestion ou à restaurer des paramètres pour la fonctionnalité Configuration Manager que vous utilisez et qui ne subsiste pas après la mise à niveau du Service Pack.  

**Problèmes connus pour les sites secondaires :**  
- **Quand vous effectuez la mise à niveau vers la version 1511 :** Pour vérifier que les clients sur les sites secondaires peuvent trouver le point de gestion à partir du site secondaire (point de gestion proxy), ajoutez manuellement le point de gestion aux groupes de limites qui incluent également les points de distribution du site secondaire.  

- **Quand vous effectuez la mise à niveau vers la version 1606 ou ultérieure :** Des points de gestion proxy sont automatiquement ajoutés aux groupes de limites qui incluent les points de distribution du site secondaire.
