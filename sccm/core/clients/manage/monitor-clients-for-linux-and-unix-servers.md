---
title: Surveiller les clients Linux/UNIX
titleSuffix: Configuration Manager
description: Surveiller les clients sur des serveurs Linux et UNIX dans Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 47a85ec7dea72f08a0ec48ebb151566b8563ba9a
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523688"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Guide pratique pour surveiller les clients sur des serveurs Linux et UNIX dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Important]  
> Depuis la version 1902, Configuration Manager ne prend en charge les clients Linux ou UNIX. 
> 
> Utilisez plutôt Microsoft Azure Management pour la gestion des serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.

Vous pouvez afficher des informations sur les serveurs Linux et UNIX dans la console Configuration Manager selon les mêmes méthodes que vous employez pour afficher des informations sur des clients Windows.  

 Vous pouvez notamment afficher les informations suivantes :  

- Détails de l’état des clients, dans les tableaux de bord de la console Configuration Manager  

- Détails sur les clients dans les rapports par défaut de Configuration Manager  

- Détails de l’inventaire dans l’Explorateur de ressources  

  Les sections suivantes décrivent comment obtenir ces informations à partir de l’Explorateur de ressources et des rapports.  

##  <a name="BKMK_UseResourceExpforLnU"></a> Utiliser l’Explorateur de ressources pour afficher l’inventaire des serveurs Linux et UNIX  

 Quand un client Configuration Manager envoie un inventaire matériel au site Configuration Manager, vous pouvez par la suite utiliser l’Explorateur de ressources pour consulter ces informations. Le client Configuration Manager pour Linux et UNIX n’ajoute pas de nouvelles classes ou vues d’inventaire dans l’Explorateur de ressources. Les données d’inventaire Linux et UNIX sont mappées aux classes WMI existantes. Vous pouvez afficher les détails d’inventaire de vos serveurs Linux et UNIX dans des classifications Windows à l’aide de l’Explorateur de ressources.  

 Par exemple, vous pouvez collecter la liste de tous les programmes installés en mode natif sur vos serveurs Linux et UNIX, tels que les programmes **.rpms** dans Linux ou **.pkgs** dans Solaris. Une fois que l’inventaire a été envoyé par un client UNIX ou Linux, vous pouvez afficher la liste de tous les programmes UNIX ou Linux installés en mode natif dans l’Explorateur de ressources de la console Configuration Manager.  

 Pour plus d’informations sur l’utilisation de l’Explorateur de ressources, consultez [Guide pratique pour utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md).  

##  <a name="BKMK_UseReportsforLnU"></a> Utiliser des rapports pour afficher des informations sur les serveurs Linux et UNIX  
 Les rapports Configuration Manager contiennent des informations sur les serveurs Linux et UNIX, ainsi que des informations sur les ordinateurs Windows. Aucune configuration supplémentaire n’est nécessaire pour intégrer les données des serveurs Linux et UNIX dans les rapports.  

 Par exemple, si vous générez le rapport Nombre de versions du système d’exploitation, ce rapport affiche la liste des différents systèmes d’exploitation utilisés et le nombre de clients qui exécutent chaque système d’exploitation. Le rapport est créé sur la base des informations d’inventaire matériel envoyées par les différents clients Configuration Manager qui s’exécutent sur les différents systèmes d’exploitation.  

 Vous pouvez aussi créer des rapports personnalisés contenant des données propres aux serveurs Linux et UNIX. Vous pouvez utiliser la propriété **Légende** de la classe d’inventaire matériel **Système d’exploitation** pour identifier les systèmes d’exploitation spécifiques dans la demande de rapport.  

 Pour plus d’informations sur les rapports dans Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../../core/servers/manage/reporting.md).  
