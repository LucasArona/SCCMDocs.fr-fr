---
title: Fonctionnalités de préversion
titleSuffix: Configuration Manager
description: Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d4e9664832b37dd05f001404012acab80fd87a43
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Fonctionnalités en préversion dans System Center Configuration Manager
*S’applique à : System Center Configuration Manager (Current Branch)*

Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Ces fonctionnalités sont entièrement prises en charge mais sont toujours en cours de développement. Elles peuvent donc être modifiées jusqu'à ce qu’elles passent en préversion.

 Pour pouvoir sélectionner et utiliser ces fonctions, vous devez d’abord donner votre consentement via la console Configuration Manager.  

Le consentement est une action à effectuer une seule fois par hiérarchie ; elle ne peut pas être annulée. Tant que vous n’avez pas accepté de les utiliser, vous ne pouvez pas activer les fonctions en préversion incluses avec les mises à jour. Après avoir activé une fonctionnalité en préversion, vous ne pouvez pas la désactiver.

Pour donner votre consentement, accédez à la console, sélectionnez **Administration** > **Configuration du site** > **Sites**, puis choisissez **Paramètres de hiérarchie**. Sous l’onglet **Général**, choisissez **Accepter d’utiliser les fonctionnalités en préversion**.

Lorsque vous installez une mise à jour qui comprend des fonctionnalités de préversion, ces dernières sont affichées dans l’Assistant Maintenance et mises à jour, avec les fonctionnalités standard incluses dans la mise à jour :
  - **Si vous avez donné votre consentement :** vous pouvez activer les fonctionnalités à partir de l’Assistant Maintenance et mises à jour quand vous installez la mise à jour. Pour ce faire, sélectionnez les fonctionnalités de préversion, comme vous le feriez pour toute autre fonctionnalité.     

    Si vous le souhaitez, vous pouvez attendre pour activer une fonctionnalité en préversion par la suite à partir du nœud **Administration** > **Mises à jour et maintenance** > **Fonctionnalités** de la console. Dans le nœud **Fonctionnalités**, sélectionnez la fonctionnalité, puis choisissez **Activer**. Cette option est grisée jusqu’à ce que vous donniez votre consentement. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)
  -   **Si vous n’avez pas donné votre consentement :** lorsque vous installez une mise à jour, les fonctionnalités en préversion sont visibles dans l’Assistant Mises à jour et maintenance, mais elles sont grisées et ne peuvent pas être activées. Une fois la mise à jour installée, vous pouvez afficher ces fonctionnalités dans le nœud **Fonctionnalités**. Mais vous ne pouvez pas les activer tant que vous n’avez pas donné votre consentement dans **Paramètres de hiérarchie**.


> [!Important]  
> Dans une hiérarchie multisite, vous pouvez uniquement activer les fonctionnalités facultatives ou en préversion sur le site d’administration centrale. Ceci vise à éviter les conflits au sein de la hiérarchie. <!--507197-->  
> Si vous avez donné votre consentement sur un site principal autonome, et si vous développez ensuite la hiérarchie en installant un nouveau site d’administration centrale, vous devez redonner votre consentement sur ce dernier.  

 Quand vous activez une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, vous devez redémarrer la console pour voir la nouvelle interface utilisateur associée à cette fonctionnalité.

**Les fonctionnalités en préversion disponibles sont les suivantes** :

 |Fonctionnalité          |Ajoutée en préversion | Ajoutée en version complète|  
|------------------|---------------------|---------------------|
|Prise en charge de Cisco AnyConnect 4.0.07x et ultérieur pour iOS<!--1357393-->|[Version 1802](/sccm/mdm/deploy-use/create-vpn-profiles)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Déploiements par phases<!--1356837-->|[Version 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Exécuter l’étape de la séquence de tâches <!-- 1261338 --> |  [Version 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Version 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Version 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel <!-- 1235616 --> |  [Version 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Version 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager <!-- 1236459 --> |  [Version 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Version 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Gérer les mises à jour du pilote Microsoft Surface <!-- 1098490 --> |  [Version 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Version 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Gestion Device Guard avec Configuration Manager <!-- 1319346 --> |  [Version 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Mise en cache préalable du contenu de la séquence de tâches <!-- 1021244 --> |  [Version 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Version 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application <!-- 1284624 --> |   [Version 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Version 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Point de service de l’entrepôt de données <!-- 1277922 --> |  [Version 1702](/sccm/core/servers/manage/data-warehouse) |[Version 1706](/sccm/core/servers/manage/data-warehouse)|
| Cache d’homologue pour la distribution de contenu aux clients <!-- 1101436 --> |  [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Version 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Passerelle de gestion cloud <!-- 1101764 --> |  [Version 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Version 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Connecteur Microsoft Operations Management Suite <!-- 1236739 --> | [Version 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |[Version 1802](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md)|
| Maintenance d’un regroupement prenant en charge les clusters (maintenance d’un groupe de serveurs) <!-- 1081776 --> | [Version 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Pas encore](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Accès conditionnel pour les PC gérés par System Center Configuration Manager <!--  --> | [Version 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Version 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif) -->

> [!Tip]  
> Pour plus d’informations sur les fonctionnalités facultatives qui doivent être activées en premier, consultez [Activation de fonctionnalités facultatives de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> Pour plus d’informations sur les fonctionnalités qui sont disponibles uniquement dans la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).  
