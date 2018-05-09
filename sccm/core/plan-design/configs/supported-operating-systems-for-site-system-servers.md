---
title: Serveurs de système de site pris en charge
titleSuffix: Configuration Manager
description: Déterminez les versions de Windows que vous pouvez utiliser pour héberger un site ou un rôle de système de site System Center Configuration Manager.
ms.date: 04/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de7f340080111daf3f1b19e26aa838dc6db2e263
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="supported-operating-systems-for-system-center-configuration-manager-site-system-servers"></a>Systèmes d’exploitation pris en charge pour les serveurs de système de site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Cet article explique en détail les versions de Windows que vous pouvez utiliser pour héberger un site ou un rôle de système de site Configuration Manager.


Utilisez les informations de cet article ainsi que celles des articles suivants :
-   [Matériel recommandé pour Configuration Manager](../../../core/plan-design/configs/recommended-hardware.md)
-   [Prérequis des sites et systèmes de site pour Configuration Manager](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)
-   [Taille et échelle de Configuration Manager en chiffres](../../../core/plan-design/configs/size-and-scale-numbers.md)



## <a name="windows-server-2016-standard-and-datacenter"></a>Windows Server 2016 : Standard et Datacenter
Avec le correctif cumulatif proposé dans l’article KB3186654, ce système d’exploitation est pris en charge pour les rôles suivants :

**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](https://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d’état



## <a name="windows-storage-server-2016"></a>Windows Storage Server 2016

**Serveur de système de site :**  

-   Point de distribution  



## <a name="windows-server-2012-r2-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64) : Standard et Datacenter  
**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](https://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d’état  

## <a name="windows-server-2012-x64-standard-and-datacenter"></a>Windows Server 2012 R2 (x64) : Standard et Datacenter  
**Serveurs de site :**  

-   Site d'administration centrale  

-   Site principal  

-   Site secondaire  

**Serveurs de système de site :**  

-   Point de service web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de synchronisation Asset Intelligence  

-   Point d'enregistrement de certificat  

-   Point de distribution  

     Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

-   Point Endpoint Protection  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion

-   Point de Reporting Services  

-   point de connexion de service  

-   Serveur de bases de données du site  

     Les serveurs de bases de données du site ne sont pas pris en charge sur un contrôleur de domaine en lecture seule (RODC). Pour plus d'informations, voir [Vous pouvez rencontrer des problèmes lors de l'installation de SQL Server sur un contrôleur de domaine](https://go.microsoft.com/fwlink/p/?LinkId=264856) dans la Base de connaissances Microsoft. En outre, les serveurs de site secondaire ne sont pris en charge sur aucun contrôleur de domaine.  

-   SMS_Provider  

-   Point de mise à jour logicielle  

-   Point de migration d’état  



## <a name="windows-server-2008-r2-with-sp1-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 R2 avec SP1 (x64) : Standard, Enterprise et Datacenter  
 Windows Server 2008 R2 bénéficie désormais du support étendu au lieu du support standard, comme indiqué dans la [Politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur la prise en charge à venir de ces systèmes d’exploitation utilisés comme serveurs de système de site avec Configuration Manager, consultez [Systèmes d’exploitation serveur dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

 Ce système d’exploitation n’est pas pris en charge pour les serveurs de site ou la plupart des rôles de système de site. Il est toujours pris en charge pour le rôle de système de site du point de distribution, dont les points de distribution d’extraction, et pour PXE et la multidiffusion.

**Serveurs de système de site :**  
-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution sur ce système d’exploitation sont pris en charge pour PXE.

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-server-2008-with-sp2-x86-x64-standard-enterprise-and-datacenter"></a>Windows Server 2008 avec SP2 (x86, x64) : Standard, Enterprise et Datacenter  
 Windows Server 2008 bénéficie désormais du support étendu au lieu du support standard, comme indiqué dans la [Politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur la prise en charge à venir de ces systèmes d’exploitation utilisés comme serveurs de système de site avec Configuration Manager, consultez [Systèmes d’exploitation serveur dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems).  

Ce système d’exploitation n’est pas pris en charge pour les serveurs de site ou les rôles de système de site, à l’exception du point de distribution et du point de distribution d’extraction. Vous pouvez continuer à utiliser ce système d’exploitation comme point de distribution jusqu’à l’annonce de la dépréciation de ce support ou jusqu’à l’expiration de la période du support étendu de ce système d’exploitation. Pour plus d’informations, consultez [Échec de l’installation de System Center Configuration Manager CB et LTSB sur Windows Server 2008](https://support.microsoft.com/help/4015095).

**Serveurs de système de site :**  
-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution sur ce système d’exploitation sont pris en charge pour PXE, mais ne prennent pas en charge le démarrage réseau des ordinateurs clients en mode EFI. Les ordinateurs clients avec un démarrage BIOS ou EFI en mode hérité sont pris en charge.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-10-x86-x64-pro-and-enterprise"></a>Windows 10 (x86, x64) : Professionnel et Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE. 

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-81-x86-x64-professional-and-enterprise"></a>Windows 8.1 (x86, x64) : Professionnel et Entreprise  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  



## <a name="windows-7-with-sp1-x86-x64-professional-enterprise-and-ultimate"></a>Windows 7 avec SP1 (x86, x64) : Professionnel, Entreprise et Édition Intégrale  
**Serveurs de système de site :**  

-   Point de distribution  

    -   Les points de distribution sur ce système d’exploitation ne sont pas pris en charge pour PXE.  

    -   Les points de distribution sur cette version du système d’exploitation ne prennent pas en charge la multidiffusion.  

    -   Les points de distribution prennent en charge plusieurs configurations différentes ayant chacune des exigences différentes. Dans certains cas, ces configurations prennent en charge l’installation sur des serveurs, mais aussi sur des systèmes d’exploitation clients. Pour plus d’informations sur les options disponibles pour les points de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

## <a name="the-server-core-installation-of-windows-server-version-1709"></a>Installation minimale de Windows Server, version 1709
À compter de Configuration Manager 1710, [Windows Server, version 1709](https://docs.microsoft.com/windows-server/get-started/get-started-with-1709) est pris en charge pour une utilisation en tant que point de distribution avec les restrictions suivantes :  
  -   Seule la version 64 bits est prise en charge.
  -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  

## <a name="the-server-core-installation-of-windows-server-2016"></a>Installation minimale de Windows Server 2016
Avec le correctif cumulatif proposé dans l’article KB3186654, ce système d’exploitation est pris en charge pour être utilisé comme point de distribution avec les limitations suivantes :  
  -   Seule la version 64 bits est prise en charge.
  -   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  



## <a name="the-server-core-installation-of-windows-server-2012-r2"></a>Installation minimale de Windows Server 2012 R2  
 L’installation minimale de Windows Server 2012 R2 est prise en charge pour une utilisation comme point de distribution avec les limitations suivantes :  

-   Seule la version 64 bits est prise en charge.

-   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.  



## <a name="the-server-core-installation-of-windows-server-2012"></a>Installation minimale de Windows Server 2012  
 L’installation minimale de Windows Server 2012 est prise en charge pour une utilisation comme point de distribution avec les limitations suivantes :  

-   Seule la version 64 bits est prise en charge.  

-   Les points de distribution sur ce système d’exploitation ne prennent pas en charge PXE ou la multidiffusion.
