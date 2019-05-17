---
title: Présentation des regroupements
titleSuffix: Configuration Manager
description: Obtenez une présentation de l’utilisation des regroupements dans System Center Configuration Manager.
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 15359aa414554d0bef9e29c011966caec1c1e6d6
ms.sourcegitcommit: 417e3834a42b415a8e129327dd3c15cc0c7ec5a2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2019
ms.locfileid: "65443148"
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Présentation des regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les regroupements vous permettent d’organiser les ressources en unités gérables. Vous pouvez créer des regroupements pour répondre à vos besoins de gestion des clients et pour effectuer des opérations sur plusieurs ressources à la fois. 

La plupart des tâches de gestion reposent sur ou nécessitent l’utilisation d’un ou plusieurs regroupements. Même si vous pouvez utiliser le regroupement prédéfini Tous les systèmes, son utilisation pour des tâches de gestion n’est pas une bonne pratique. Créez des regroupements personnalisés pour identifier de façon plus spécifique les appareils ou les utilisateurs pour une tâche.  

 Les regroupements intégrés et personnalisés figurent dans les nœuds **Regroupements d’utilisateurs** et **Regroupements de périphériques** dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager.  

 Les derniers regroupements visualisés apparaissent dans le nœud **Utilisateurs** et dans le nœud **Appareils** de l’espace de travail **Biens et conformité**.  

Voici quelques exemples d’utilisation de regroupements :  

|Opération|Exemple|  
|---------|-------|  
|Regroupement des ressources|Vous pouvez créer des regroupements qui rassemblent des ressources en fonction de la hiérarchie de votre organisation.<br /><br /> Par exemple, vous pouvez créer un regroupement de tous les ordinateurs de l’unité d’organisation Active Directory « Siège social de Londres ». Pour plus d’informations sur la création de ce type de regroupement, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Vous pouvez utiliser ce regroupement pour des opérations comme la configuration des paramètres Endpoint Protection, la configuration des paramètres de gestion de l’alimentation des appareils ou l’installation du client Configuration Manager.|  
|Déploiement d’applications|Vous pouvez créer un regroupement de tous les ordinateurs où Microsoft Office 2013 n’est pas installé, puis le déployer sur tous les ordinateurs de ce regroupement.<br /><br /> Vous pouvez également utiliser des données de configuration requise pour l’application pour effectuer cette tâche. Pour plus d’informations, consultez [Comment créer des applications avec System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gestion des paramètres client](../../../../core/clients/deploy/about-client-settings.md)|Bien que les paramètres client par défaut dans Configuration Manager s’appliquent à tous les appareils et à tous les utilisateurs, vous pouvez créer des paramètres client personnalisés qui s’appliquent à un regroupement d’appareils ou d’utilisateurs.<br /><br /> Par exemple, si vous voulez que le contrôle à distance soit disponible sur tous les appareils excepté quelques-uns, configurez les paramètres client par défaut pour autoriser le contrôle à distance, puis configurez les paramètres client personnalisés qui interdisent le contrôle à distance et déployez-les sur le regroupement des clients qui font l’objet de cette exception. |  
|[Gestion de l’alimentation](../power/introduction-to-power-management.md)|Vous pouvez configurer des paramètres d’alimentation spécifiques par regroupement.|  
|[Administration basée sur des rôles](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Utiliser des regroupements pour contrôler quels groupes d’utilisateurs ont accès à différentes fonctionnalités dans la console Configuration Manager.|  
|[Fenêtres de maintenance](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Avec des fenêtres de maintenance, vous pouvez définir une période de temps pendant laquelle différentes opérations Configuration Manager peuvent être effectuées sur les membres d’un regroupement d’appareils. |  


## <a name="collection-types-in-configuration-manager"></a>Types de regroupements dans Configuration Manager  
 Configuration Manager a des regroupements prédéfinis pour les opérations courantes, et vous pouvez aussi créer des regroupements personnalisés.   

### <a name="built-in-collections"></a>Regroupements intégrés  
 Par défaut, Configuration Manager contient les regroupements suivants qui ne peuvent pas être modifiés.  

|**Nom du regroupement**|Description|  
|-------------------------|-----------------|  
|**Tous les groupes d'utilisateurs**|Contient les groupes d'utilisateurs qui sont découverts à l'aide de la découverte de groupes de sécurité Active Directory.|  
|**Tous les utilisateurs**|Contient les utilisateurs qui sont découverts à l'aide de la découverte d'utilisateurs Active Directory.|  
|**Tous les utilisateurs et groupes d'utilisateurs**|Contient tous les utilisateurs et tous les regroupements de groupes d'utilisateurs. Ce regroupement contient la plus grande étendue de ressources utilisateur et groupe d’utilisateurs.|  
|**Tous les clients bureau et serveur**|Contient les appareils serveurs et de bureau qui disposent du client Configuration Manager. L'appartenance est maintenue par découverte par pulsations d'inventaire.|  
|**Tous les appareils mobiles**|Contient les appareils mobiles qui sont gérés par Configuration Manager. L'appartenance est limitée à ces appareils mobiles qui sont affectés à un site avec succès ou découverts par le connecteur Exchange Server.|  
|**Tous les systèmes**|Contient les regroupements Tous les clients poste de travail et serveur, Tous les appareils mobiles et Tous les ordinateurs inconnus, ainsi que tous les appareils mobiles qui sont inscrits par Microsoft Intune. Ce regroupement contient la plus grande étendue de ressources d’appareil.|  
|**Tous les ordinateurs inconnus**|Contient des enregistrements d'ordinateur générique pour plusieurs plates-formes informatiques. Vous pouvez utiliser ce regroupement pour déployer un système d'exploitation à l'aide d'une séquence de tâches et d'un démarrage PXE, d'un média de démarrage ou d'un média préparé.|  

### <a name="custom-collections"></a>Regroupements personnalisés  
 Quand vous créez un regroupement personnalisé dans Configuration Manager, l’appartenance de ce regroupement est déterminée par une ou plusieurs règles de regroupement, comme décrit dans [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). 

