---
title: Listes de contrôle pour la migration
titleSuffix: Configuration Manager
description: Utilisez les listes de contrôle de l’administrateur pour vous aider à planifier une stratégie de migration vers System Center Configuration Manager.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 295fdf07-93cc-490c-acdd-ce3ee88cb36f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3136c8add4256a646409c4a540da783a04a5b71d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128287"
---
# <a name="administrator-checklists-for-migration-planning-in-system-center-configuration-manager"></a>Listes de vérifications de l’administrateur pour la planification de la migration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les listes de contrôle de l’administrateur suivantes pour vous aider à planifier votre stratégie de migration vers System Center Configuration Manager.

##  <a name="Checklist_Migraiton_Planning"></a> Liste de contrôle de l’administrateur pour la planification de la migration  
 Pour les étapes de planification de la prémigration, utilisez la liste de vérification suivante :  

-   **Évaluez l’environnement actuel :**  

     Identifiez quelles sont les spécifications d'entreprise existantes respectées par la hiérarchie source et élaborez des plans visant à respecter ces spécifications dans la hiérarchie de destination.  

-   **Passez en revue les fonctionnalités de la version de Configuration Manager que vous utilisez et les modifications qu’elle apporte, puis utilisez ces informations pour concevoir votre hiérarchie de destination :**  

    Pour plus d'informations, consultez [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md) et [Nouveautés dans System Center Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)  


-   **Déterminez le modèle de sécurité administrative à utiliser dans le cadre de l’administration basée sur des rôles :**  

    Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   **Évaluez votre réseau et la topologie Active Directory :** Examinez votre structure de domaine et la topologie de réseau existantes et réfléchissez à leur influence sur vos tâches de conception et de migration de hiérarchie.  

-   **Finalisez la conception de votre hiérarchie de destination :**  

    Prenez une décision quant au placement d'un site d'administration centrale, de sites principaux, de sites secondaires et d'options de distribution de contenu.  

-   **Mappez votre hiérarchie aux ordinateurs que vous utiliserez pour les sites et les serveurs de site de la hiérarchie de destination :**  

    Identifiez les ordinateurs qui seront utilisés par les sites et les serveurs de système de site de la hiérarchie de destination, puis vérifiez qu’ils disposent d’une capacité suffisante pour respecter les spécifications opérationnelles actuelles et futures.  

-   **Planifiez votre stratégie de migration d’objets :**  

    Planifiez l’utilisation des tâches de migration disponibles pour migrer différents objets (limites de site, regroupements, publications et déploiements). Pour plus d’informations, consultez [Types de tâches de migration](../../core/migration/planning-a-migration-job-strategy.md#Types_of_Migration) dans [Planification d’une stratégie pour les tâches de migration dans System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)  

    Configuration Manager migre uniquement les objets que vous sélectionnez. Tous les objets qui ne sont pas migrés et qui sont requis dans la hiérarchie de destination doivent être recréés dans cette dernière.  

    Les objets qui peuvent migrer sont affichés lorsque vous configurez des tâches de migration.  

-   **Planifiez votre stratégie de migration de clients :**  

    Lorsque vous migrez des clients vers la hiérarchie de destination, envisagez d'utiliser une approche contrôlée, qui limite la consommation de la bande passante réseau et des ressources de traitement côté serveur. Pour plus d’informations sur la planification d’une stratégie de migration de client, consultez [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Planifiez les données d’inventaire et de conformité :**  

    Configuration Manager ne prend pas en charge la migration des données d’inventaire matériel, d’inventaire logiciel ou de conformité de gestion de la configuration souhaitée pour les mises à jour logicielles ou les clients.  

    En revanche, une fois que le client a été migré vers son nouveau site dans la hiérarchie de destination et qu'il a reçu la stratégie relative à ces configurations, il envoie ces informations à son site attribué. Par le biais de cette opération, les données de compatibilité et d'inventaire actuelles sont ajoutées à base de données du site de destination.  

-   **Planifiez la fin de la migration à partir de la hiérarchie source :**  

    Décidez à quel moment les objets et les clients seront migrés. Au terme de la migration, vous pouvez envisager de retirer les serveurs de site de la hiérarchie source.  

##  <a name="Checklist_Hierarchy_for_migration"></a> Liste de contrôle de l’administrateur pour la migration de la hiérarchie  
Utilisez la liste de vérification suivante pour faciliter la planification d'une hiérarchie de destination avant une migration.  

-   **Identifiez les ordinateurs à utiliser dans la hiérarchie de destination :**  

    Configuration Manager ne prend pas en charge une mise à niveau sur place de l’infrastructure Configuration Manager 2007. Vous utilisez alors la migration pour déplacer les données de Configuration Manager 2007 vers System Center Configuration Manager. Ce déplacement vous oblige à utiliser un déploiement côte à côte et à installer System Center Configuration Manager sur de nouveaux ordinateurs.  

    De même, quand vous procédez à une migration à partir d’une autre hiérarchie System Center Configuration Manager, vous devez installer une nouvelle hiérarchie de destination qui correspond à un déploiement côte à côte vers votre hiérarchie source.  

-   **Créez votre hiérarchie de destination :**  

    Pour préparer la migration, installez et configurez une hiérarchie de destination System Center Configuration Manager comprenant un site principal. Par exemple :  

    -   Installez un site d’administration centrale, puis installez au moins un site principal enfant.  

    -   Si vous ne prévoyez pas d'utiliser un site d'administration centrale, installez un site principal autonome.  

-   **Si vous souhaitez migrer les informations relatives aux mises à jour logicielles, configurez un point de mise à jour logicielle dans la hiérarchie de destination et synchronisez les mises à jour logicielles :**  

    Pour pouvoir migrer les informations relatives aux mises à jour logicielles figurant dans la hiérarchie source, vous devez au préalable configurer et synchroniser les mises à jour logicielles dans la hiérarchie de destination.  


-   **Installez et configurez des rôles système de site supplémentaires dans la hiérarchie de destination :**  

    Configurez les rôles de système de site et les systèmes de site supplémentaires dont vous avez besoin.  

-   **Vérifiez le bon fonctionnement de la hiérarchie de destination :**  

    Vérifiez les points suivants :  

    -   Si la hiérarchie de destination comporte plusieurs sites, vérifiez que la réplication de la base de données entre les sites fonctionne correctement. La réplication de la base de données ne s'applique pas aux sites principaux autonomes.  

    -   Vérifiez que tous les rôles de système de site installés fonctionnent correctement.  

    -   Vérifiez que les clients Configuration Manager que vous installez dans la hiérarchie de destination peuvent communiquer avec le site qui leur a été affecté.  


##  <a name="Checklisit_Migration"></a> Liste de contrôle de l’administrateur pour la migration  
Utilisez la liste de vérification suivante pour migrer les données de la hiérarchie source vers la hiérarchie de destination.  

-   **Activez la migration dans la hiérarchie de destination :**  

    Configurez une hiérarchie source en indiquant le site de niveau supérieur de cette hiérarchie. Pour plus d’informations sur la spécification du site source, consultez [Planification d’une stratégie de hiérarchie source dans System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

-   **Si la hiérarchie source exécute Configuration Manager 2007 SP2, sélectionnez et configurez des sites supplémentaires dans la hiérarchie source :**  

    Pour chacun des sites supplémentaires de la hiérarchie source Configuration Manager 2007 SP2 dont vous souhaitez collecter les données, vous devez configurer des informations d’identification en vue de la collecte de données. Quand vous configurez chaque site source, le processus de collecte de données démarre immédiatement et se poursuit tout au long de la période de migration, jusqu’à ce que vous arrêtiez la collecte de données pour ce site. La collecte de données permet de vérifier que vous pouvez migrer les objets de la hiérarchie source qui ont été ajoutés ou mis à jour depuis la collecte de données précédente.

    > [!NOTE]  
    >  Quand la hiérarchie source exécute System Center 2012 Configuration Manager ou une version ultérieure, il est inutile de configurer des sites sources supplémentaires.  

-   **Configurez le partage du point de distribution :**  

    Vous pouvez partager des points de distribution entre les deux hiérarchies, afin de mettre le contenu des objets que vous migrez à la disposition des clients de la hiérarchie de destination. Ceci garantit que le même contenu reste disponible pour les clients dans les deux hiérarchies et que vous pouvez conserver ce contenu jusqu’à l’arrêt de la collecte de données et la fin de la migration.  

    Pour plus d’informations sur les points de distribution partagés, consultez [Partager les points de distribution entre les hiérarchies sources et de destination](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) dans [Planification d’une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Créez et exécutez des tâches de migration afin de migrer les objets associés aux clients dans la hiérarchie source :**  

    Créez des tâches de migration pour migrer des objets entre des hiérarchies. Les configurations requises pour chaque tâche de migration varient selon les données à migrer.  

    Par exemple, lorsque vous migrez du contenu, quelle que soit la tâche de migration utilisée, vous devez attribuer la propriété de la gestion de ce contenu à un site de la hiérarchie de destination. Le site attribué accédera à l'emplacement du fichier source d'origine relatif au contenu et devra distribuer ce contenu auprès des points de distribution de la hiérarchie de destination.  

    Pour plus d’informations, consultez [Créer et modifier des tâches de migration pour System Center Configuration Manager](../../core/migration/operations-for-migration.md#Create_Edit_migration_Jobs) dans [Opérations de migration vers System Center Configuration Manager](../../core/migration/operations-for-migration.md).  

-   **Migrez les clients vers la hiérarchie de destination :**  

    Le processus de migration des clients dépend de votre scénario de migration :  

    -   Quand vous migrez des clients qui n’utilisent pas la même version du client que la hiérarchie de destination, vous devez mettre à niveau le logiciel client. La mise à niveau consiste à supprimer le client Configuration Manager actuel, puis à installer la nouvelle version du client, qui correspond à celle du site de destination.  

    -   Lorsque vous migrez des clients qui utilisent la même version du client que la hiérarchie de destination, le client n'est pas mis à niveau, ni réinstallé. En revanche, il est réattribué à un site principal dans la hiérarchie de destination.  

    Lorsque vous migrez un client vers la hiérarchie de destination, le client est associé à ses données, que vous avez précédemment migrées vers cette hiérarchie de destination.  

    Pour plus d'informations, voir [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

-   **Mettez à niveau ou réaffectez des points de distribution partagés :**  

    Quand vous n’avez plus à prendre en charge des clients dans votre hiérarchie source, vous pouvez mettre à niveau des points de distribution partagés depuis un site source Configuration Manager 2007 ou réaffecter des points de distribution partagés à partir d’un site source System Center 2012 Configuration Manager ou System Center Configuration Manager. Lorsque vous mettez à niveau ou réaffectez un point de distribution, le rôle de système de site est transféré vers un site principal de la hiérarchie de destination et le point de distribution est supprimé du site source de la hiérarchie source. Quand vous mettez à niveau ou que vous réaffectez un point de distribution partagé, le contenu reste sur l’ordinateur du point de distribution et vous n’avez pas besoin de redéployer le contenu sur de nouveaux points de distribution de la hiérarchie de destination.  

    Vous pouvez également mettre à niveau un point de distribution colocalisé sur un serveur de site secondaire Configuration Manager 2007. Cette opération supprime le site secondaire et conserve un seul point de distribution dans la hiérarchie de destination.  

    Pour plus d’informations sur les points de distribution partagés, consultez [Partager les points de distribution entre les hiérarchies sources et de destination](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) dans [Planification d’une stratégie de migration de déploiement de contenu dans System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

-   **Terminez la migration :**  

    Une fois que vous avez migré les données et les clients de tous les sites de la hiérarchie source et que vous avez mis à niveau les points de distribution concernés, vous pouvez terminer la migration. Pour cela, vous arrêtez la collecte de données pour tous les sites source de la hiérarchie source. Vous pouvez ensuite supprimer toutes les informations de migration dont vous n'avez pas besoin et retirer l'infrastructure de votre hiérarchie source. Pour plus d’informations, voir [Planning to complete migration in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).  
