---
title: Inventaire logiciel
titleSuffix: Configuration Manager
description: Obtenez une présentation de l’inventaire logiciel dans System Center Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 79eb49da-cd2b-4ffc-b355-b595aeba3aea
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0ca25d64f3dd0e86ddbd89e2d86ae13da170891
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550747"
---
# <a name="introduction-to-software-inventory-in-system-center-configuration-manager"></a>Présentation de l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’inventaire logiciel pour collecter des informations sur les fichiers présents sur les appareils clients. L’inventaire logiciel peut aussi collecter des fichiers auprès des appareils clients et les stocker sur le serveur de site. L'inventaire logiciel est collecté lorsque vous sélectionnez le paramètre **Activer l'inventaire logiciel sur les clients** dans les paramètres du client. Vous pouvez également planifier l’opération dans les paramètres du client.  

Une fois l’inventaire logiciel activé et que les clients exécutent un cycle d’inventaire logiciel, le client envoie les informations à un point de gestion dans le site du client. Le point de gestion transfère ensuite les informations d’inventaire au serveur de site Configuration Manager, qui les stocke dans la base de données du site.

 Voici comment afficher les données de l’inventaire logiciel :  

- [Créez des requêtes](../../../../core/servers/manage/create-queries.md) qui retournent les appareils avec des fichiers spécifiés.   

- Créez des [regroupements basés sur une requête](../../../../core/clients/manage/collections/introduction-to-collections.md) qui incluent les appareils avec des fichiers spécifiés.   

- [Exécutez des rapports](../../../../core/servers/manage/reporting.md) qui fournissent des détails sur les fichiers présents sur les appareils.

- Utiliser l’[Explorateur de ressources](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md) pour examiner les informations détaillées sur les fichiers qui ont été inventoriés et collectés sur les appareils clients.   

 Quand un inventaire logiciel s’exécute sur un appareil client, le premier rapport d’inventaire est un inventaire complet. Les rapports suivants contiennent seulement des informations d’inventaire différentiel. Le serveur de site traite les informations différentielles selon l’ordre dans lequel il les reçoit. S’il manque des informations différentielles pour un client, le serveur de site rejette les informations différentielles suivantes et indique au client d’exécuter un inventaire complet.  

 Configuration Manager peut découvrir les ordinateurs à double démarrage, mais retourne uniquement les informations d’inventaire du système d’exploitation actif au moment de l’inventaire.  

**Appareils mobiles :** Consultez [Inventaire logiciel des appareils mobiles inscrits auprès de Microsoft Intune](../../../../mdm/deploy-use/software-inventory-mobile-devices.md) pour plus d’informations sur la collecte de l’inventaire pour les applications installées sur des appareils mobiles.
