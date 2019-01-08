---
title: 'Surveiller les clients Linux/UNIX '
titleSuffix: Configuration Manager
description: Surveillez les clients sur des serveurs Linux et UNIX dans System Center Configuration Manager.
ms.date: 08/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d827cf91-b18f-4ee7-b538-24ba6f003ab9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2fe6f2490b1ec527b7e6e09e9ce476e66342d7c9
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421159"
---
# <a name="how-to-monitor-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Guide pratique pour surveiller les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez afficher des informations sur les serveurs Linux et UNIX dans la console System Center Configuration Manager selon les mêmes méthodes que vous employez pour afficher des informations sur des clients Windows.  

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
