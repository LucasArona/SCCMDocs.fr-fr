---
title: Changements de Configuration Manager 2012
description: Identifiez les changements et les nouvelles fonctionnalités de System Center Configuration Manager par rapport à System Center 2012 Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 97f19a06e1edd40c9cd791b46f836f54d1cd22ca
ms.sourcegitcommit: 94bf7d5b5beb9628cc1fdfe75451d33b5de26f8a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152483"
---
# <a name="whats-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>Ce qui a changé dans System Center Configuration Manager par rapport à System Center 2012 Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Current Branch de Configuration Manager présente des changements importants par rapport à System Center 2012 Configuration Manager. Cet article identifie les changements importants et les nouvelles fonctionnalités dans la version de base de référence 1511 de System Center Configuration Manager. Pour en savoir plus sur les changements introduits dans les mises à jour suivantes pour System Center Configuration Manager, consultez [Nouveautés dans les versions incrémentielles de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

La version de décembre 2015 de System Center Configuration Manager (version 1511) était la version initiale du produit Configuration Manager actuel de Microsoft. Elle est généralement désignée sous le nom de « Current Branch » de System Center Configuration Manager. La mention *Current Branch* indique une version qui prend en charge les mises à jour incrémentielles du produit. Elle représente également un moyen de faire la distinction entre cette version et les versions précédentes de Configuration Manager.  

System Center Configuration Manager :  

- N’utilise pas d’identificateur d’année ni de produit dans le nom du produit, comme c’était le cas dans les versions précédentes telles que Configuration Manager 2007 ou System Center 2012 Configuration Manager.  

- Prend en charge les mises à jour incrémentielles dans le produit, aussi appelées versions de mise à jour. La version initiale était la version 1511. Les versions suivantes sont publiées plusieurs fois par an sous la forme de mises à jour dans la console, comme la version 1710.  

- Est installé à l’aide d’une version de base. La version 1511 était la version de base initiale, mais de nouvelles versions de base sont également publiées de temps à autre, comme la version 1802. Les versions de base peuvent être utilisées pour installer un nouveau site System Center Configuration Manager et sa hiérarchie ou pour mettre à niveau à partir d’une version prise en charge de Configuration Manager 2012.  



##  <a name="bkmk_updates"></a> Mises à jour dans la console pour Configuration Manager  

System Center Configuration Manager utilise une méthode de service dans la console appelée **Mises à jour et maintenance** qui facilite la localisation et l’installation des mises à jour recommandées.  

Certaines versions disponibles uniquement comme mises à jour pour des sites existants (à partir de la console Configuration Manager) ne peuvent pas être utilisées pour installer de nouveaux sites Configuration Manager. Par exemple, la mise à jour 1710 est disponible uniquement à partir de la console Configuration Manager. Elle est utilisée pour mettre à jour un site qui exécute déjà une version de System Center Configuration Manager.

Une version de mise à jour est également publiée régulièrement sous la forme d’une nouvelle version de base (par exemple, la mise à jour 1802). Ce type de mise à jour peut être utilisée pour installer une nouvelle hiérarchie sans avoir à démarrer avec une ancienne version de base de référence (comme 1511) et à effectuer une mise à niveau vers la version la plus récente.


Pour plus d’informations sur l’utilisation des mises à jour, consultez [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).  
Pour plus d’informations sur les versions de base, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions).



##  <a name="bkmk_servicepoint"></a>Nouveau rôle de système de site : point de connexion de service  

Le **connecteur Microsoft Intune** est remplacé par un nouveau rôle de système de site qui offre des fonctionnalités supplémentaires, à savoir le **point de connexion de service**. Le point de connexion de service :  

- remplace le connecteur Microsoft Intune quand vous intégrez Intune à la gestion des appareils mobiles locale System Center Configuration Manager.  

- est utilisé comme point de contact pour les appareils que vous gérez.  

- charge des données d’utilisation relatives à votre déploiement sur le service cloud Microsoft.  

- met des mises à jour qui s’appliquent à votre déploiement à disposition à partir de la console Configuration Manager.  

Ce rôle de système de site prend en charge à la fois un mode en ligne et hors connexion de fonctionnement. Pour plus d’informations, consultez [À propos du point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  



##  <a name="bkmk_usage"></a> Collecte des données d’utilisation  

Configuration Manager collecte des données d’utilisation sur vos sites et votre infrastructure. Ces informations sont compilées et transmises au service cloud Microsoft par le point de connexion de service. Configuration Manager en a besoin pour télécharger les mises à jour applicables à la version de Configuration Manager que vous utilisez pour votre déploiement. Au moment de configurer le point de connexion de service, vous pouvez définir le niveau des données collectées et si celles-ci sont envoyées automatiquement (mode en ligne) ou manuellement (mode hors connexion).  

Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



##  <a name="bkmk_AMT"></a> Prise en charge de la technologie Intel AMT (Active Management Technology)  

Configuration Manager Current Branch supprime la prise en charge native des ordinateurs AMT à partir de la console Configuration Manager. Les ordinateurs AMT restent entièrement gérés quand vous utilisez le [module complémentaire Intel SCS pour Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Ce module complémentaire vous permet d’accéder aux dernières fonctionnalités permettant de gérer AMT tout en supprimant les limitations introduites jusqu’à ce que Configuration Manager puisse intégrer ces changements.  

La suppression de la technologie AMT intégrée pour Configuration Manager inclut la gestion hors bande. Le rôle de système de site de point de gestion hors bande n’est plus disponible.  

> [!Note]   
> La gestion hors bande dans System Center 2012 Configuration Manager n’est pas affectée par cette modification.  



##  <a name="bkmk_out"></a> Fonctionnalités déconseillées  

Certaines fonctionnalités, telles que la [prise en charge de la technologie Intel AMT (Active Management Technology)](#bkmk_AMT), sont retirées de la console Configuration Manager. D’autres comme la protection d’accès réseau sont entièrement retirées. Par ailleurs, certains produits Microsoft plus anciens comme Windows Vista, Windows Server 2008 et SQL Server 2008 ne sont plus pris en charge.  

Pour obtenir la liste des fonctionnalités déconseillées, consultez [Éléments supprimés et dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).  

Pour plus d’informations sur les produits, les systèmes d’exploitation et les configurations pris en charge, consultez [Configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations).  



## <a name="client-deployment"></a>Déploiement des clients  

Configuration Manager inaugure une nouvelle fonctionnalité visant à tester les nouvelles versions du client Configuration Manager avant la mise à niveau du reste du site avec le nouveau logiciel. Vous pouvez configurer un regroupement de préproduction dans lequel piloter un nouveau client. Dès lors que vous êtes satisfait du nouveau logiciel client en préproduction, vous pouvez le promouvoir pour mettre automatiquement à niveau le reste du site avec la nouvelle version.  

Pour plus d’informations sur le test des clients, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction](/sccm/core/clients/manage/upgrade/test-client-upgrades).  



## <a name="os-deployment"></a>Déploiement de système d’exploitation  

Tenez compte des modifications suivantes apportées au déploiement du système d’exploitation :

- Dans l’Assistant Création d’une séquence de tâches, un nouveau type de séquence de tâches est disponible : **Mettre à niveau un système d'exploitation à partir d'un package de mise à niveau**. Cette séquence permet de créer la procédure de mise à niveau des ordinateurs Windows 7, Windows 8 ou Windows 8.1 vers Windows 10. Pour plus d’informations, consultez [Effectuer une mise à niveau de Windows vers la dernière version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Le cache d’homologue Windows PE est désormais disponible pendant le déploiement de systèmes d’exploitation. Les ordinateurs qui exécutent une séquence de tâches pour le déploiement d’un système d’exploitation peuvent utiliser le cache d’homologue Windows PE pour obtenir le contenu d’une source de cache d’homologue au lieu de télécharger du contenu auprès d’un point de distribution. Ce comportement permet de réduire le trafic WAN dans les scénarios pour des filiales où il n’existe pas de point de distribution local. Pour plus d’informations, consultez [Préparer la mise en cache d’homologue Windows PE pour réduire le trafic WAN](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic).  

- Vous pouvez désormais afficher l’état de Windows sous forme de service dans votre environnement. Vous pouvez également créer des plans de maintenance pour former des anneaux de déploiement et vérifier que les ordinateurs Windows 10 Current Branch sont tenus à jour quand de nouvelles versions sont publiées. En outre, vous pouvez voir des alertes pour les clients Windows 10 quand la fin de support de leur build approche. Pour plus d’informations, consultez [Gérer Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service).  



## <a name="application-management"></a>Gestion des applications  

Tenez compte des modifications suivantes apportées à la gestion des applications :

- Configuration Manager vous permet de déployer des applications de la plateforme Windows universelle pour les appareils exécutant Windows 10 et des versions ultérieures. Pour plus d’informations, consultez [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications).  

- Le Centre logiciel a été modernisé. Les applications disponibles pour les utilisateurs qui figuraient uniquement dans le catalogue d’applications apparaissent désormais dans le Centre logiciel sous l’onglet Applications. Ces déploiements sont ainsi plus identifiables pour les utilisateurs qui n’ont plus besoin d’utiliser le catalogue d’applications. De plus, un navigateur Silverlight n’est plus nécessaire. Pour plus d’informations, consultez [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

- Par l’intermédiaire du type d’application MDM, le nouveau Windows Installer vous permet de créer et déployer des applications Windows Installer sur les PC inscrits qui exécutent Windows 10. Pour plus d’informations, consultez [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications).  

- Quand vous créez une application pour une application iOS interne, vous devez seulement spécifier le fichier d’installation (.ipa) de l’application. Vous n’avez plus besoin de spécifier de fichier de liste de propriétés (.plist) correspondant. Consultez [Création d’applications iOS](/sccm/apps/get-started/creating-ios-applications).  

- Dans Configuration Manager 2012, pour spécifier un lien vers une application du Windows Store, vous pouviez soit spécifier directement le lien, soit accéder à un ordinateur distant sur lequel l’application était installée. Dans Configuration Manager Current Branch, vous pouvez toujours entrer directement le lien mais, au lieu d’accéder à un ordinateur de référence, vous pouvez rechercher l’application directement dans le Store à partir de la console Configuration Manager.  



## <a name="software-updates"></a>Mises à jour logicielles  

Tenez compte des modifications suivantes apportées aux mises à jour logicielles :

- Configuration Manager peut désormais faire la distinction entre les différentes méthodes de gestion des mises à jour logicielles pour les ordinateurs. Plus précisément, il peut faire la distinction entre un ordinateur Windows 10 qui se connecte à Windows Update for Business (WUfB) et un ordinateur connecté au serveur WSUS. **UseWUServer** est un nouvel attribut qui indique si l’ordinateur est géré avec WUfB. Vous pouvez utiliser ce paramètre dans un regroupement pour retirer ces ordinateurs de la gestion des mises à jour logicielles. Pour plus d'informations, voir [Intégration avec Windows Update for Business dans Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10).  

- Vous pouvez maintenant planifier et exécuter la tâche de nettoyage WSUS à partir de la console Configuration Manager. Dans les propriétés du **composant du point de mise à jour logicielle**, quand vous choisissez d’exécuter la tâche de nettoyage WSUS, elle s’exécute à la prochaine synchronisation des mises à jour logicielles. Les mises à jour logicielles qui ont expiré présentent un état refusé sur le serveur WSUS et l’Agent Windows Update ne les analyse plus. Pour plus d'informations, voir [Schedule and run the WSUS clean up task](/sccm/sum/deploy-use/software-updates-maintenance).  



## <a name="compliance-settings"></a>Paramètres de conformité  

Tenez compte des modifications suivantes apportées aux paramètres de compatibilité :

- Configuration Manager améliore le flux de travail pour créer les éléments de configuration. Désormais, quand vous créez un élément de configuration et que vous sélectionnez une plateforme prise en charge, seuls les paramètres correspondant à cette plateforme vous sont proposés. Consultez [Bien démarrer avec les paramètres de compatibilité](/sccm/compliance/get-started/get-started-with-compliance-settings).  

- L’Assistant **Création d’élément de configuration** vous permet désormais de choisir plus facilement le type d’élément de configuration à créer. De plus, les éléments de configuration nouveaux et mis à jour sont disponibles pour :  

    - Les appareils Windows 10 gérés avec le client Configuration Manager  

    - Les appareils Mac OS X gérés avec le client Configuration Manager  

    - Les ordinateurs de bureau et serveur Windows gérés avec le client Configuration Manager  

    - Les appareils Windows 8.1 et Windows 10 gérés sans le client Configuration Manager  

    - Les appareils Windows Phone gérés sans le client Configuration Manager  

    - Les appareils iOS et Mac OS X gérés sans le client Configuration Manager  

    - Les appareils Samsung KNOX Standard et Android gérés sans le client Configuration Manager  
  
    Pour plus d’informations, consultez [Créer des éléments de configuration](/sccm/compliance/deploy-use/create-configuration-items).  

- Prise en charge de la gestion des paramètres sur les ordinateurs Mac OS X inscrits avec Microsoft Intune ou gérés avec le client Configuration Manager. Consultez [Comment créer des éléments de configuration pour des appareils iOS et Mac OS X gérés sans le client Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).  



## <a name="on-premises-mobile-device-management"></a>Gestion locale des appareils mobiles  

Vous pouvez désormais gérer les appareils mobiles au moyen d’une infrastructure Configuration Manager locale. Les données de gestion et des appareils sont traitées localement et ne font pas partie de Microsoft Intune ni d’autres services cloud. Ce type de gestion d’appareils ne fait appel à aucun logiciel client. Configuration Manager gère les appareils avec des fonctionnalités qui sont intégrées aux systèmes d’exploitation des appareils.  

Pour plus d'informations, consultez [Gérer des appareils mobiles avec une infrastructure locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).
