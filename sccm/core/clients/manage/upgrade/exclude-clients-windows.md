---
title: Empêcher la mise à niveau de clients Windows
titleSuffix: Configuration Manager
description: Découvrez comment empêcher la mise à niveau de clients Windows dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cd6031f-8844-4d0b-8166-b24d6528a94e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b14ff463d6f39e74ad757d992fda1042f534a2cd
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53414665"
---
# <a name="how-to-exclude-upgrading-clients-for-windows-computers-in-system-center-configuration-manager"></a>Guide pratique pour empêcher la mise à niveau de clients sur des ordinateurs Windows dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À partir de la version 1610, vous pouvez empêcher un regroupement de clients d’installer automatiquement les versions mises à jour du client. Cela s’applique à la mise à niveau automatique ainsi qu’à d’autres méthodes, telles que la mise à niveau de logiciels basée sur la mise à jour, les scripts d’ouverture de session et la stratégie de groupe. Vous pouvez utiliser cette fonctionnalité pour un regroupement d’ordinateurs dont la mise à niveau du client nécessite plus d’attention. Un client qui se trouve dans un regroupement exclu ignore les demandes d’installation du logiciel client mis à jour.

## <a name="configure-exclusion-for-automatic-upgrades"></a>Configurer l’exclusion des mises à niveau automatiques

1. Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**, puis cliquez sur **Paramètres de hiérarchie**.

2. Cliquez sur l’onglet **Mise à niveau des clients**.

3. Cochez la case **Exclure les clients spécifiés de la mise à niveau**, puis pour Regroupement à exclure, sélectionnez le regroupement à exclure. Vous pouvez sélectionner un seul regroupement à exclure.

4.  Cliquez sur **OK** pour fermer et enregistrer la configuration. Ensuite, une fois que les clients ont mis à jour la stratégie, les clients figurant dans le regroupement exclu n’installent plus automatiquement les mises à jour du logiciel client. Pour plus d’informations, consultez [Guide pratique pour mettre à niveau des clients sur les ordinateurs Windows](upgrade-clients-for-windows-computers.md).

![Paramètres d’exclusion de mise à niveau automatique](media/automatic_upgrade_exclusion.png)



>[!NOTE]
>Même si l’interface utilisateur indique que les clients ne seront pas mis à niveau, quelle que soit la méthode, il existe deux méthodes que vous pouvez utiliser pour remplacer ces paramètres. L’installation Push du client et une installation manuelle du client peuvent être utilisées pour remplacer cette configuration. Pour plus d’informations, consultez la section suivante.

## <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Guide pratique pour mettre à niveau un client figurant dans un regroupement exclu

Quand un regroupement est configuré comme exclu, les membres de ce regroupement peuvent mettre à niveau leur logiciel client par seulement deux méthodes, qui ont priorité sur l’exclusion :
- **Installation Push du client** : Vous pouvez utiliser l’installation Push du client pour mettre à niveau un client figurant dans un regroupement exclu. Cela est autorisé, car cela est considéré comme l’intention de l’administrateur et vous permet de mettre à niveau les clients sans retirer le regroupement complet de l’exclusion.       

- **Installation manuelle du client** : Vous pouvez mettre à niveau manuellement les clients qui se trouvent dans un regroupement exclu en utilisant le commutateur de ligne de commande suivant avec ccmsetup :  ***/ignoreskipupgrade***

  Si vous tentez de mettre à niveau manuellement un client qui est membre du regroupement exclu et que vous n’utilisez pas ce commutateur, le client n’installe pas le nouveau logiciel client. Pour plus d’informations, consultez [Comment installer les clients Configuration Manager manuellement](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Pour plus d’informations sur les méthodes d’installation de client, consultez [Comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).
