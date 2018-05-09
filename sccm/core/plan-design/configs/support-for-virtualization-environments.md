---
title: Prise en charge de la virtualisation
titleSuffix: Configuration Manager
description: Découvrez la configuration requise pour l’installation des rôles système de site et du client System Center Configuration Manager dans un environnement de virtualisation.
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 374a1643c5ea439a7406bbb1f6b53322caa50871
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-virtualization-environments-for-system-center-configuration-manager"></a>Prise en charge des environnements de virtualisation pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager prend en charge l’installation de rôles de système de site et de client sur les systèmes d’exploitation pris en charge qui s’exécutent comme machines virtuelles dans les environnements de virtualisation décrits dans cet article. Cette prise en charge se fait même quand l'hôte de la machine virtuelle (environnement de virtualisation) n'est pas pris en charge comme client ou comme serveur de site.  

 Par exemple, si vous utilisez Microsoft Hyper-V Server 2012 pour héberger une machine virtuelle qui exécute Windows Server 2012, vous pouvez installer les rôles de système de site ou de client sur la machine virtuelle (Windows Server 2012), mais pas sur l’hôte (Microsoft Hyper-V Server 2012).  

|Environnement de virtualisation|  
|--------------------------------|  
|Windows Server 2008 R2|  
|Microsoft Hyper-V Server 2008 R2|  
|Windows Server 2012|  
|Microsoft Hyper-V Server 2012|  
|Windows Server 2012 R2|
|Windows Server 2016 <sup>(voir la *remarque 1*)</sup>|
|Microsoft Hyper-V Server 2016 <sup>(voir la *remarque 1*)|
-  *Remarque 1* : Configuration Manager ne prend pas en charge la [virtualisation imbriquée](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/what-s-new-in-hyper-v-on-windows#a-namebkmknestedanested-virtualization-new), qui est une nouvelle fonctionnalité de Windows Server 2016.


 Chaque machine virtuelle que vous utilisez doit respecter ou dépasser les mêmes configurations matérielle et logicielle requises que celles que vous utiliseriez pour un ordinateur Configuration Manager physique.  

 Vous pouvez vérifier que votre environnement de virtualisation est bien pris en charge pour Configuration Manager à l’aide du programme SVVP (Server Virtualization Validation Program) et de son Assistant Stratégie de prise en charge du programme de virtualisation en ligne. Pour plus d’informations sur le programme SVVP (Server Virtualization Validation Program), consultez [Programme SVVP (Server Virtualization Validation Program) de Windows Server](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
>  Configuration Manager ne prend pas en charge les systèmes d’exploitation invités Virtual PC ou Virtual Server qui sont exécutés sur des ordinateurs Mac.  

Configuration Manager ne peut pas gérer les machines virtuelles, sauf si elles sont en ligne. Il n’est pas possible de mettre à jour une image de machine virtuelle déconnectée, ni de collecter un inventaire via le client Configuration Manager sur l’ordinateur hôte.  

Aucune attention particulière n'est accordée aux machines virtuelles. Par exemple, si la mise à jour d’une image de machine virtuelle a été arrêtée puis redémarrée sans que l’état de la machine virtuelle à laquelle la mise à jour a été appliquée n’ait été enregistré, il est possible que Configuration Manager ne détermine pas s’il est nécessaire de réappliquer cette mise à jour.  

##  <a name="bkmk_Azure"></a> Machines virtuelles Microsoft Azure  
 Configuration Manager peut s’exécuter sur des machines virtuelles Azure de la même manière qu’il s’exécute localement dans votre réseau physique d’entreprise. Vous pouvez utiliser Configuration Manager sur des machines virtuelles Azure dans les scénarios suivants :  

-   **Scénario 1 :** vous pouvez exécuter Configuration Manager sur une machine virtuelle Azure et l’utiliser pour gérer des clients qui sont installés sur d’autres machines virtuelles Azure.  

-   **Scénario 2** : vous pouvez exécuter Configuration Manager sur une machine virtuelle Azure et l’utiliser pour gérer des clients qui ne s’exécutent pas sur Azure.  

-   **Scénario 3** : vous pouvez exécuter différents rôles de système de site Configuration Manager sur des machines virtuelles Azure tout en exécutant d’autres rôles dans votre réseau physique d’entreprise (avec une connectivité réseau appropriée pour les communications).  

La même configuration requise de System Center Configuration Manager en matière de réseaux, de configurations prises en charge et de matériel, applicable à l’installation locale de Configuration Manager sur votre réseau d’entreprise physique, s’applique également aux installations effectuées sur des machines virtuelles Azure.  

Pour plus d’informations, consultez [Configuration Manager sur Azure : Forum Aux Questions](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
>  Les sites et les clients Configuration Manager qui s’exécutent sur des machines virtuelles Azure sont soumis aux mêmes exigences de licence que les installations locales.  
