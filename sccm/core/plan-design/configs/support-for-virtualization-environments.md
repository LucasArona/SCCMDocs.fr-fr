---
title: Prise en charge de la virtualisation
titleSuffix: Configuration Manager
description: Configuration requise pour l’installation des rôles système de site et du client Configuration Manager dans un environnement de virtualisation.
ms.date: 01/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1098e8c5-9676-4c2b-841b-ec88bd04e495
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a2200a72330fab2f0584c419e6b66b2fc25c44b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135600"
---
# <a name="support-for-virtualization-environments-with-configuration-manager"></a>Prise en charge des environnements de virtualisation pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager prend en charge l’installation de rôles système de site ou de clients sur les systèmes d’exploitation pris en charge qui s’exécutent comme machine virtuelle dans les environnements de virtualisation dans cet article. Cette prise en charge se fait même quand l'hôte de la machine virtuelle (environnement de virtualisation) n'est pas pris en charge comme client ou comme serveur de site.  

Par exemple, vous utilisez Microsoft Hyper-V Server 2012 pour héberger une machine virtuelle qui exécute Windows Server 2012. Vous pouvez installer les rôles système de site ou client sur la machine virtuelle exécutant Windows Server 2012. Vous ne pouvez pas installer le client sur l’hôte exécutant Microsoft Hyper-V Server 2012.  


## <a name="virtualization-environments"></a>Environnements de virtualisation

- Windows Server 2019  
- Windows Server 2016 <sup>[Remarque 1](#bkmk_note1)</sup>  
- Microsoft Hyper-V Server 2016 <sup>[Remarque 1](#bkmk_note1)</sup>  
- Windows Server 2012 R2  
- Microsoft Hyper-V Server 2012  
- Windows Server 2012  
- Microsoft Hyper-V Server 2008 R2  
- Windows Server 2008 R2  

#### <a name="bkmk_note1"></a>Remarque 1 : Virtualisation imbriquée
Configuration Manager ne prend pas en charge la [virtualisation imbriquée](https://docs.microsoft.com/windows-server/virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows#BKMK_nested), qui est une nouvelle fonctionnalité de Windows Server 2016.


### <a name="virtualization-environment-support"></a>Prise en charge de l’environnement de virtualisation

Chaque machine virtuelle doit respecter ou dépasser les mêmes configurations matérielle et logicielle requises que celles que vous utiliseriez pour un ordinateur Configuration Manager physique.  

Pour vérifier que votre environnement de virtualisation est bien pris en charge pour Configuration Manager, utilisez le programme SVVP (Server Virtualization Validation Program). Il inclut un assistant Stratégie de prise en charge du programme de virtualisation en ligne. Pour plus d’informations, consultez [Programme SVVP (Server Virtualization Validation Program)](https://www.windowsservercatalog.com/svvp.aspx).  

> [!NOTE]  
> Configuration Manager ne prend pas en charge les systèmes d’exploitation invités Virtual PC ou Virtual Server qui sont exécutés sur des ordinateurs Mac.  

Configuration Manager ne peut pas gérer les machines virtuelles si elles sont hors connexion. Il n’est pas possible de mettre à jour une image de machine virtuelle déconnectée, ni de collecter un inventaire via le client Configuration Manager sur l’ordinateur hôte.  

Aucune attention particulière n'est accordée aux machines virtuelles. Par exemple, si la mise à jour d’une image de machine virtuelle a été arrêtée puis redémarrée sans que l’état de la machine virtuelle à laquelle la mise à jour a été appliquée n’ait été enregistré, il est possible que Configuration Manager ne détermine pas s’il est nécessaire de réappliquer cette mise à jour.  



##  <a name="bkmk_Azure"></a> Machines virtuelles Microsoft Azure  

Configuration Manager peut s’exécuter sur des machines virtuelles Azure de la même manière qu’il s’exécute localement dans votre centre de données. Utilisez Configuration Manager sur des machines virtuelles Azure dans les scénarios suivants :  

- **Scénario 1** : Exécutez Configuration Manager sur une machine virtuelle Azure. Il permet de gérer les clients sur les autres machines virtuelles Azure.  

- **Scénario 2** : Exécutez Configuration Manager sur une machine virtuelle Azure. Il permet de gérer les clients qui ne sont pas en cours d’exécution sur Azure.  

- **Scénario 3** : Exécutez différents rôles de système de site Configuration Manager sur des machines virtuelles Azure. Exécutez d’autres rôles dans votre centre de données local, correctement connecté à Azure.  

La même configuration requise de Configuration Manager en matière de réseaux, de configurations prises en charge et de matériel, applicable à l’installation locale de Configuration Manager, s’applique également aux installations effectuées sur des machines virtuelles Azure.  

Pour plus d’informations, consultez [Configuration Manager sur Azure](/sccm/core/understand/configuration-manager-on-azure).

> [!IMPORTANT]  
> Les sites et les clients Configuration Manager qui s’exécutent sur des machines virtuelles Azure sont soumis aux mêmes exigences de licence que les installations locales.  
