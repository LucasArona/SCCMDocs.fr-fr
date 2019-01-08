---
title: 'Inventaire matériel '
titleSuffix: Configuration Manager
description: Obtenez une présentation de l’inventaire matériel dans System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3969952e-9d05-49c9-82a2-e7e90ccef511
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 91bb316c59929898ea18bd1e647cff884f106f1c
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424780"
---
# <a name="introduction-to-hardware-inventory-in-system-center-configuration-manager"></a>Présentation de l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’inventaire matériel dans System Center Configuration Manager pour recueillir des informations sur la configuration matérielle des appareils clients de votre organisation. Pour recueillir l'inventaire matériel, le paramètre **Activer l'inventaire matériel sur les clients** doit être activé dans les paramètres client.  

 Une fois l’inventaire matériel activé et un cycle d’inventaire matériel exécuté par le client, ce dernier envoie les informations à un point de gestion sur le site du client. Le point de gestion transfère ensuite les informations d’inventaire au serveur de site Configuration Manager, qui les stocke dans la base de données du site. L'inventaire matériel s'exécute sur les clients en fonction de la planification que vous spécifiez dans les paramètres du client.  

 Vous pouvez utiliser plusieurs méthodes pour afficher les données d’inventaire matériel que Configuration Manager recueille. Ces référentiels sont notamment les suivants :  

- [Créer des requêtes qui retournent des appareils basés sur une configuration matérielle spécifique](../../../../core/servers/manage/queries-technical-reference.md).  

- [Créer des regroupements basés sur des requêtes qui reposent sur une configuration matérielle spécifique](../../../../core/clients/manage/collections/introduction-to-collections.md). Les appartenances à un regroupement basé sur une requête sont mises à jour automatiquement selon un calendrier. Vous pouvez utiliser des regroupements pour plusieurs tâches, notamment le déploiement de logiciel. .  

- [Exécuter des rapports qui affichent des détails spécifiques sur les configurations matérielles de votre organisation](../../../../core/servers/manage/reporting.md).   

- [Utilisez l’Explorateur de ressources](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) pour afficher des informations détaillées sur l’inventaire matériel collecté à partir d’appareils clients.   

  Lorsque l'inventaire matériel s'exécute sur un appareil client, les premières données d'inventaire renvoyées par le client sont toujours un inventaire complet. Les informations d'inventaire suivantes contiennent uniquement des informations d'inventaire différentielles. Le serveur de site traite les informations d'inventaire différentielles selon l'ordre dans lequel il les reçoit. S’il manque des informations différentielles pour un client, le serveur de site rejette les informations différentielles supplémentaires et indique au client d’exécuter un cycle d’inventaire complet.  

  Configuration Manager assure une prise en charge limitée des ordinateurs à double démarrage. Configuration Manager peut détecter les ordinateurs à double démarrage, mais retourne uniquement les informations d’inventaire du système d’exploitation qui était actif au moment de l’inventaire.  

> [!NOTE]  
>  Pour plus d’informations sur l’utilisation de l’inventaire matériel avec des clients qui exécutent Linux et UNIX, consultez [Inventaire matériel pour Linux et UNIX dans System Center Configuration Manager](../../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md).  

## <a name="extending-configuration-manager-hardware-inventory"></a>Extension de l’inventaire matériel Configuration Manager  
 En plus de l’inventaire matériel intégré dans Configuration Manager, vous pouvez également utiliser une des méthodes suivantes pour étendre l’inventaire matériel en vue de collecter des informations supplémentaires :  

- Vous pouvez activer, désactiver, ajouter et supprimer des classes d’inventaire pour l’inventaire matériel à partir de la console Configuration Manager.|  
- Utilisez des fichiers NOIDMIF pour collecter des informations sur les appareils clients qui ne peuvent pas être inventoriés par Configuration Manager. Par exemple, vous pouvez souhaiter recueillir des informations numéros de périphérique actif qui existe uniquement en tant qu'étiquette sur le périphérique. Inventaire NOIDMIF est automatiquement associé à l'appareil client collectées à partir de.  
- Utilisez des fichiers IDMIF pour collecter des informations sur les ressources qui ne sont associées à aucun client Configuration Manager ; par exemple, les projecteurs, les photocopieurs et les imprimantes réseau.  

  Pour plus d’informations sur l’utilisation de ces méthodes pour étendre l’inventaire matériel de Configuration Manager, consultez [Guide pratique pour configurer l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
