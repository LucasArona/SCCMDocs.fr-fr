---
title: Configurer l’inventaire matériel
titleSuffix: Configuration Manager
description: Configurez l’inventaire matériel pour l’ensemble des clients ou pour un regroupement dans System Center Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1b632a9b7b7b20bc8d6653d35b267043dde6660d
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50410998"
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>Comment configurer l’inventaire matériel dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette procédure configure les paramètres client par défaut pour l’inventaire matériel et s’applique à tous les clients de votre hiérarchie. Si vous voulez que ces paramètres s’appliquent uniquement à certains clients, créez un paramètre client de périphérique personnalisé et affectez-le à un regroupement contenant les périphériques pour lesquels utiliser l’inventaire matériel. Consultez [Guide pratique pour configurer les paramètres clients dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Si un périphérique client reçoit des paramètres d’inventaire matériel de la part de plusieurs ensembles de paramètres client, les classes d’inventaire matériel de chaque ensemble de paramètres sont alors fusionnées lors de l’inventaire matériel. De plus, si vous ne cochez pas une classe dans un paramètre client personnalisé ayant une priorité plus élevée, l’inventaire de cette classe par le client n’est pas désactivé. 

Pour désactiver une classe d’inventaire matériel spécifique sur la plupart des systèmes, hormis quelques uns, la classe doit être décochée dans les paramètres clients par défaut. Créez ensuite un paramètre client personnalisé pour activer la classe, puis déployez-le sur les systèmes cibles.


### <a name="to-configure-hardware-inventory"></a>Pour configurer l'inventaire matériel  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres par défaut**, choisissez **Inventaire matériel**.  

6.  Dans la liste **Paramètres de périphérique** , configurez les éléments suivants :  

    -   **Activer l’inventaire matériel sur les clients** : sélectionnez **Oui**.  

    -   **Calendrier de l’inventaire matériel** : Cliquez sur **Planifier** pour spécifier l’intervalle auquel les clients collectent l’inventaire matériel.  

7.  Configurez les autres [paramètres clients d’inventaire matériel](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory) dont vous avez besoin.  

Les périphériques client sont configurés en utilisant ces paramètres lors du prochain téléchargement de stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [Comment gérer des clients dans Configuration Manager](../../../../core/clients/manage/manage-clients.md).  
