---
title: Configuration requise pour la création de rapports
titleSuffix: Configuration Manager
description: Comprenez les diverses dépendances qui ont un impact sur l’utilisation des rapports dans System Center Configuration Manager.
ms.date: 01/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 612056861b896d8c7c271e60e0bb6b78fcbd106e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123261"
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>Configuration requise pour la création de rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La création de rapports dans System Center Configuration Manager comporte des dépendances externes et des dépendances au sein du produit.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  
 Le tableau suivant répertorie les dépendances externes pour la création de rapports.  

|Condition préalable|Informations complémentaires|  
|------------------|----------------------|  
|SQL Server Reporting Services|Pour pouvoir utiliser des rapports dans Configuration Manager, vous devez installer et configurer SQL Server Reporting Services.<br /><br /> Pour plus d'informations sur la planification et le déploiement de Reporting Services dans votre environnement, reportez-vous à la section [Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) de la documentation en ligne de SQL Server 2008.|  
|Dépendances de rôle de système de site pour les ordinateurs qui exécutent le point de Reporting Services.|[Configurations prises en charge pour System Center Configuration Manager](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Dépendances internes à Configuration Manager  
 Le tableau suivant répertorie les dépendances pour la création de rapports dans Configuration Manager.  

|Condition préalable|Informations complémentaires|  
|------------------|----------------------|  
|Point de Reporting Services|Vous devez configurer le rôle système de site du point de Reporting Services pour pouvoir utiliser la création de rapports dans Configuration Manager. Pour plus d’informations sur l’installation et la configuration d’un point Reporting Services, consultez [Configuration de la création de rapports dans Configuration Manager](../../../core/servers/manage/configuring-reporting.md).|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>Versions de SQL Server prises en charge par le point de Reporting Services  
 La base de données Reporting Services peut être installée sur l'instance par défaut ou sur une instance nommée d'une installation 64 bits de SQL Server. L'instance SQL Server peut se trouver au même emplacement que le serveur du système de site ou sur un ordinateur distant.  

 Le tableau ci-dessous indique quelles versions de SQL Server sont prises en charge par le point de Reporting Services.  

|Version SQL Server|Point de Reporting Services|  
|------------------------|------------------------------|
|SQL Server 2017 avec au minimum la mise à jour cumulative 2<br /><br /> -   Standard<br />-   Enterprise|Oui, à compter de Configuration Manager version 1710|  
|SQL Server 2016 avec SP1<br /><br /> -   Standard<br />-   Enterprise|Oui| 
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|Oui|
|SQL Server 2014 avec SP2<br /><br /> -   Standard<br />-   Enterprise|Oui|
|SQL Server 2014 avec SP1<br /><br /> -   Standard<br />-   Enterprise|Oui|
|SQL Server 2012 avec SP4 <br /><br /> -   Standard<br />-   Enterprise|Oui|  
|SQL Server 2012 avec SP3 <br /><br /> -   Standard<br />-   Enterprise|Oui|  
|SQL Server 2008 R2 avec SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|Oui, pour les versions prises en charge de Configuration Manager antérieures à 1702.|  
|SQL Server Express 2008 R2 with SP3|Non pris en charge| 




## <a name="next-steps"></a>Étapes suivantes
[Opérations et maintenance pour les rapports](operations-and-maintenance-for-reporting.md)
