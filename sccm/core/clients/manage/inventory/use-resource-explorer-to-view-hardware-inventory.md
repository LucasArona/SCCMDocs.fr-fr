---
title: Afficher l’inventaire matériel avec l’Explorateur de ressources
titleSuffix: Configuration Manager
description: Utilisez l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager.
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2c8c3dbfef5ea0f35e338b14439c65150310be
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Comment utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’Explorateur de ressources de System Center Configuration Manager pour afficher des informations sur l’inventaire matériel collecté à partir de clients de votre hiérarchie.  

> [!NOTE]  
>  L'Explorateur de ressources n'affichera pas de données d'inventaire avant qu'un cycle d'inventaire matériel ait été exécuté sur le client auquel vous êtes connecté.  

 L’Explorateur de ressources contient les sections suivantes relatives à l’inventaire matériel :  

-   **Matériel** : contient l’inventaire matériel le plus récent collecté à partir de l’appareil client indiqué.  **État de la station de travail** : indique l’heure et la date du dernier inventaire matériel effectué par l’appareil.  

-   **Historique du matériel** : contient un historique des éléments d’inventaire qui ont été modifiés depuis le dernier inventaire matériel. Chaque élément contient un nœud **En cours** et un ou plusieurs nœuds *<date\>*. Vous pouvez comparer les informations du nœud en cours à l’un des nœuds historiques pour découvrir les éléments qui ont été modifiés.  

    > [!NOTE]  
    >  Configuration Manager conserve l'historique de l'inventaire matériel pendant le nombre de jours que vous spécifiez dans la tâche de maintenance du site **Supprimer les historiques d'inventaire anciens**.  

> [!NOTE]  
>  Pour plus d’informations sur la façon d’afficher l’inventaire matériel des clients qui exécutent Linux et UNIX, consultez [Guide pratique pour surveiller les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Comment exécuter l’Explorateur de ressources à partir de la console Configuration Manager  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Appareils**, ou ouvrez un regroupement qui affiche des appareils.  

3.  Choisissez l’ordinateur contenant l’inventaire que vous souhaitez afficher puis, dans l’onglet **Accueil**, dans le groupe **Appareils**, choisissez **Démarrer** >  **Explorateur de ressources**.   

4.  Cliquez avec le bouton droit sur un élément dans le volet droit de la fenêtre **Explorateur de ressources**, puis choisissez **Propriétés** pour ouvrir la boîte de dialogue *Propriétés de <nom_élément\>* et visualiser les informations d’inventaire recueillies sous un format plus lisible.  

