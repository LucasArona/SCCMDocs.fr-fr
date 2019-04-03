---
title: Services de composants et leurs commandes sur des clients UNIX/Linux
titleSuffix: Configuration Manager
description: En savoir plus sur les services de composants et leurs commandes sur des clients Linux et UNIX dans Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f3538265bdd7de801acf3d8f04c5561364989cf
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523977"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Services de composants et leurs commandes sur des clients Linux et UNIX pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Important]  
> Depuis la version 1902, Configuration Manager ne prend en charge les clients Linux ou UNIX. 
> 
> Utilisez plutôt Microsoft Azure Management pour la gestion des serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.


 Le tableau ci-dessous identifie les services de composants clients du client Configuration Manager pour Linux et UNIX.  

|Nom de fichier|Informations complémentaires|  
|---------------|----------------------|  
|ccmexec.bin|Ce service équivaut au service ccmexc sur un client Windows. Il est responsable de toutes les communications avec les rôles de système de site Configuration Manager et communique également avec le service omiserver.bin pour procéder à l’inventaire matériel de l’ordinateur local.<br /><br /> Pour obtenir la liste des arguments de ligne de commande pris en charge, exécutez `ccmexec -h`|  
|omiserver.bin|Ce service est le serveur CIM. Le serveur CIM fournit une infrastructure pour des modules logiciels enfichables appelés fournisseurs. Les fournisseurs interagissent avec les ressources informatiques Linux et UNIX, et recueillent les données de l’inventaire matériel. Par exemple, le **fournisseur process** pour une Linux ordinateur collecte les données associées avec les processus du système d'exploitation Linux.|  

 Les commandes de liste de tables suivantes que vous pouvez utiliser pour démarrer, arrêter ou redémarrer les services du client (ccmexec.bin et omiserver.bin) sur chaque version de Linux ou UNIX. Quand vous démarrez ou arrêtez le service ccmexec, le service omiserver démarre ou s’arrête également.  

|Système d'exploitation|Commandes|  
|----------------------|--------------|  
|Agent universel<br /><br /> RHEL 4 et SLES 9|Démarrer : `/etc/init d/ccmexecd start`<br /><br /> Arrêter : `/etc/init d/ccmexecd stop`<br /><br /> Redémarrer : `/etc/init d/ccmexecd restart`|  
|Solaris 9|Démarrer : `/etc/init d/ccmexecd start`<br /><br /> Arrêter : `/etc/init d/ccmexecd stop`<br /><br /> Redémarrer : `/etc/init d/ccmexecd restart`|  
|Solaris 10|Démarrer :<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Arrêter :<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|Démarrer :<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> Arrêter :<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|Démarrer :<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> Arrêter :<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|Démarrer : `/sbin/init.d/ccmexecd start`<br /><br /> Arrêter : `/sbin/init.d/ccmexecd stop`<br /><br /> Redémarrer : `/sbin/init.d/ccmexecd restart`|  
