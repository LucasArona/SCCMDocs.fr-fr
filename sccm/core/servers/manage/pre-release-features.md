---
title: Fonctionnalités de préversion
titleSuffix: Configuration Manager
description: Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d892e8d194f61fece977c91ce36ba46cf9dd53d
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250712"
---
# <a name="pre-release-features-in-configuration-manager"></a>Fonctionnalités en préversion dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les fonctionnalités en préversion sont des fonctions incluses dans l’édition Current Branch à des fins de test préalable dans un environnement de production. Ces fonctionnalités sont entièrement prises en charge, mais sont toujours en cours de développement. Elles peuvent donc être modifiées jusqu’à ce qu’elles quittent la préversion.



## <a name="give-consent"></a>Donner votre consentement  

Pour pouvoir utiliser les fonctionnalités en préversion, vous devez d’abord donner votre consentement. Le consentement est une action à effectuer une seule fois par hiérarchie ; elle ne peut pas être annulée. Tant que vous n’avez pas accepté de les utiliser, vous ne pouvez pas activer les nouvelles fonctionnalités en préversion incluses avec les mises à jour. Après avoir activé une fonctionnalité en préversion, vous ne pouvez pas la désactiver.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Cliquez sur **Paramètres de hiérarchie** dans le ruban.  

3. Sous l’onglet **Général** de Propriétés des paramètres de hiérarchie, activez l’option **Accepter d’utiliser les fonctionnalités en préversion**. Cliquez sur **OK**.  



## <a name="enabling-pre-release-features"></a>Activation des fonctionnalités en préversion

Quand vous installez une mise à jour qui comprend des fonctionnalités en préversion, ces dernières sont affichées dans l’Assistant Maintenance et mises à jour, avec les fonctionnalités standard incluses dans la mise à jour.

#### <a name="if-you-have-given-consent"></a>Si vous avez donné votre consentement
Dans l’Assistant Maintenance et mises à jour, activez les fonctionnalités en préversion. Sélectionnez les fonctionnalités en préversion, comme vous le feriez pour toute autre fonctionnalité.     

Si vous le souhaitez, activez les fonctionnalités en préversion plus tard à partir du nœud **Fonctionnalités** sous **Mises à jour et maintenance** dans l’espace de travail **Administration**. Sélectionnez une fonctionnalité, puis cliquez sur **Activer** dans le ruban. Cette option ne peut pas être utilisée tant que vous n’avez pas donné votre consentement.

#### <a name="if-you-havent-given-consent"></a>Si vous n’avez pas donné votre consentement
Dans l’Assistant Maintenance et mises à jour, les fonctionnalités en préversion sont visibles, mais vous ne pouvez pas les activer. Une fois la mise à jour installée, ces fonctionnalités sont visibles dans le nœud **Fonctionnalités**. Toutefois, vous ne pouvez pas les activer tant que vous n’avez pas donné votre consentement.


> [!Important]  
> Dans une hiérarchie multisite, vous pouvez uniquement activer les fonctionnalités facultatives ou en préversion sur le site d’administration centrale. Ceci vise à éviter les conflits au sein de la hiérarchie. <!--507197-->  
> 
> Si vous avez donné votre consentement sur un site principal autonome, et si vous développez ensuite la hiérarchie en installant un nouveau site d’administration centrale, vous devez redonner votre consentement sur ce dernier.  

Quand vous activez une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, redémarrez la console pour pouvoir utiliser la fonctionnalité.



## <a name="pre-release-features"></a>Fonctionnalités de préversion

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| Fonctionnalité          | Ajoutée en préversion | Ajoutée en version complète |  
|------------------|----------------------|-------------------------|
| API Fournisseur SMS <!--1359052--> | Version 1810 | ![Pas encore](media/red_x.png) |
| [Système de site HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Version 1806 | Version 1810 |
| [Applications clientes pour les appareils cogérés](/sccm/comanage/workloads#client-apps) <!--1357892--> | Version 1806 | ![Pas encore](media/red_x.png) |
| [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Version 1806 | Version 1810 |
| [Prise en charge de Cisco AnyConnect 4.0.07x et version supérieure pour iOS](/sccm/mdm/deploy-use/create-vpn-profiles)<!--1357393--> | Version 1802 | Version 1802 <br>avec mise à jour 4163547 |
| [Déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Version 1802 | Version 1806 |
| [Exécuter l’étape de la séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338--> |  Version 1710 | Version 1802 |
| [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Version 1710 | Version 1802 |
| [Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Version 1710 | Version 1802 |
| [Créer et exécuter des scripts PowerShell](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Version 1706 | Version 1802 |
| [Gérer les mises à jour du pilote Microsoft Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490--> | Version 1706 | Version 1710 |
| [Gestion Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--1355092 (1319346)--> | Version 1702 | ![Pas encore](media/red_x.png) |
| [Mise en cache préalable du contenu de la séquence de tâches](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244--> | Version 1702 | Version 1710 |
| [Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) <!--1284624--> | Version 1702 | Version 1706 |
| [Point de service de l’entrepôt de données](/sccm/core/servers/manage/data-warehouse) <!--1277922--> | Version 1702 | Version 1706 |
| [Cache de pair pour la distribution de contenu aux clients](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436--> | Version 1610 | Version 1710 |
| [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Version 1610 | Version 1802 |
| [Connecteur Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Version 1606 | Version 1802 |
| [Maintenance d’un regroupement prenant en charge les clusters (maintenance d’un groupe de serveurs)](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups) <!--1081776--> | Version 1602 | ![Pas encore](media/red_x.png) |
| [Accès conditionnel pour les PC gérés par Configuration Manager](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--  --> | Version 1602 | Version 1702 |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Pour plus d’informations sur les fonctionnalités facultatives qui doivent être activées en premier, consultez [Activation de fonctionnalités facultatives de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Pour plus d’informations sur les fonctionnalités qui sont disponibles uniquement dans la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).  
