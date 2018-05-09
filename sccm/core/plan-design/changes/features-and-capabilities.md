---
title: Fonctions et fonctionnalités
titleSuffix: Configuration Manager
description: Découvrez les principales fonctionnalités de gestion de System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fadc93d1977d5d066a6c4c3884bdbaeefb2a0c90
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Fonctions et fonctionnalités de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les principales fonctionnalités de gestion de System Center Configuration Manager sont exposées ci-après. Chaque fonctionnalité possède ses propres prérequis, et les fonctionnalités que vous souhaitez utiliser peuvent influencer la conception et l’implémentation de votre hiérarchie Configuration Manager. Par exemple, si vous souhaitez déployer des logiciels sur des appareils de votre hiérarchie, vous devez installer le rôle de système de site du point de distribution.  

 Pour plus d’informations sur la planification et l’installation de Configuration Manager pour prendre en charge ces fonctionnalités de gestion dans votre environnement, consultez [Se préparer pour System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Gestion des applications**  

 Fournit un ensemble d’outils et de ressources qui peuvent vous aider à créer, gérer, déployer et surveiller les applications sur les différents types d’appareils que vous gérez. Par ailleurs, Configuration Manager met à votre disposition des outils qui vous aident à protéger les données de votre entreprise contenues dans les applications des utilisateurs. Consultez [Introduction à la gestion des applications](/sccm/apps/understand/introduction-to-application-management).

 **Accès aux ressources d’entreprise**  

 Fournit un ensemble d'outils et de ressources qui permettent aux utilisateurs de votre organisation d'accéder à des données et des applications à partir d'emplacements distants. Ces outils incluent les profils Wi-Fi, les profils VPN, les profils de certificat et l’accès conditionnel à Exchange et SharePoint Online. Consultez [Protéger les données et l’infrastructure des sites avec System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) et [Gérer l’accès aux services dans System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Paramètres de compatibilité**  

 Fournit un ensemble d'outils et de ressources susceptibles de vous aider à évaluer, suivre et corriger la compatibilité de la configuration des appareils clients de l'entreprise. De plus, vous pouvez utiliser les paramètres de compatibilité pour configurer tout un éventail de fonctionnalités et de paramètres de sécurité sur les appareils que vous gérez. Consultez [Garantir la conformité des appareils avec System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Propose une gestion de la sécurité, des logiciels anti-programme malveillant et du Pare-feu Windows pour les ordinateurs de votre entreprise. Consultez [Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventaire**  

 Fournit un ensemble d'outils pour aider à identifier et surveiller les actifs :  

-   **Inventaire matériel**: collecte des informations détaillées sur le matériel des appareils de votre entreprise. Consultez [Présentation de l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Inventaire logiciel**: collecte et rapporte des informations sur les fichiers qui sont stockés sur des ordinateurs clients de votre organisation. Consultez [Présentation de l’inventaire logiciel dans System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Asset Intelligence**: fournit des outils pour collecter les données d'inventaire et surveiller l'utilisation des licences de logiciels dans votre entreprise. Consultez [Présentation d’Asset Intelligence dans System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Gestion des appareils mobiles avec Microsoft Intune**  

 Vous pouvez utiliser Configuration Manager pour gérer des appareils iOS, Android (dont Samsung KNOX Standard), Windows Phone et Windows à l’aide du service Microsoft Intune sur Internet.

 Même si vous utilisez le service Intune, les tâches de gestion s’effectuent à l’aide du rôle de système de site de point de connexion de service, disponible via la console Configuration Manager. Consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **Gestion des appareils mobiles locale**  

 Inscrit et gère les PC et les appareils mobiles en utilisant l’infrastructure Configuration Manager locale et les fonctionnalités de gestion intégrées aux plateformes d’appareils (au lieu d’utiliser un client Configuration Manager installé séparément). Prend actuellement en charge la gestion des appareils Windows 10 Entreprise et Windows 10 Mobile. Consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Déploiement de systèmes d’exploitation**  

 Fournit un outil pour créer des images de système d'exploitation. Vous pouvez ensuite utiliser ces images pour déployer les systèmes d’exploitation sur des ordinateurs, à l’aide du démarrage PXE ou d’un média de démarrage, tel qu’un jeu de CD, un DVD ou des lecteurs flash USB. Notez que cela s’applique aux ordinateurs qui sont gérés par Configuration Manager ainsi qu’aux ordinateurs non gérés. Consultez [Introduction au déploiement de système d’exploitation dans System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Gestion de l’alimentation**  

 Fournit un ensemble d'outils et de ressources que vous pouvez utiliser pour gérer et surveiller la consommation d'énergie des ordinateurs clients dans l'entreprise. Consultez [Présentation de la gestion de l’alimentation dans System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Requêtes**  

 Fournit un outil pour récupérer des informations sur les ressources de votre hiérarchie et des informations sur les données d'inventaire et les messages d'état. Vous pouvez ensuite utiliser ces informations pour établir des rapports ou pour définir des regroupements d’appareils ou d’utilisateurs pour les paramètres de déploiement et de configuration de logiciels. Consultez [Présentation des requêtes dans System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Profils de connexion à distance**  

 Fournit un ensemble d’outils et de ressources pour vous aider à créer, déployer et surveiller les paramètres de connexion à distance vers des appareils de votre organisation. En déployant ces paramètres, vous réduisez l’effort fourni par les utilisateurs pour se connecter à leurs ordinateurs sur le réseau d’entreprise. Consultez [Utilisation de profils de connexion à distance dans System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **Éléments de configuration des données et profils utilisateur**  

 Les éléments de configuration des données et profils utilisateur dans Configuration Manager contiennent des paramètres permettant de gérer la redirection de dossiers, les fichiers hors connexion et les profils itinérants sur des ordinateurs qui exécutent Windows 8 et versions ultérieures pour les utilisateurs de votre hiérarchie. Consultez [Utilisation d’éléments de configuration des données et profils utilisateur dans System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Contrôle à distance**  

 Fournit des outils pour administrer des ordinateurs clients à distance, à partir de la console Configuration Manager. Consultez [Présentation du contrôle à distance dans System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Rapports**  

 Fournissent un ensemble d’outils et de ressources vous permettant d’utiliser les fonctionnalités de création de rapport avancées de SQL Server Reporting Services à partir de la console Configuration Manager. Consultez [Présentation des rapports dans System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Contrôle de logiciel**  

 Fournit des outils pour surveiller et collecter les données d’utilisation des logiciels à partir de clients Configuration Manager. Consultez [Surveiller l’utilisation des applications avec le contrôle de logiciel dans System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Mises à jour logicielles**  

 Fournit un ensemble d'outils et de ressources qui peuvent vous aider à gérer, déployer et surveiller les mises à jour logicielles dans l'entreprise. Consultez [Présentation des mises à jour logicielles dans System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  
