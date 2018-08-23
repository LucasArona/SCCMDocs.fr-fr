---
title: Guide pratique pour utiliser l’Explorateur de ressources
titleSuffix: Configuration Manager
description: Utilisez l’Explorateur de ressources pour afficher l’inventaire matériel dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4f39d06072222c14627481f21139f06ee6656c4
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384982"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-configuration-manager"></a>Guide pratique pour utiliser l’Explorateur de ressources pour afficher l’inventaire matériel dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’Explorateur de ressources dans Configuration Manager pour afficher les informations sur l’inventaire matériel. Le site collecte ces informations à partir de clients de votre hiérarchie.  

> [!Tip]  
>  L’Explorateur de ressources n’affiche pas de données tant qu’un cycle d’inventaire matériel n’a pas été exécuté sur le client auquel vous êtes connecté.  



## <a name="overview"></a>Vue d'ensemble

L’Explorateur de ressources contient les sections suivantes relatives à l’inventaire matériel :  

- **Matériel** : affiche l’inventaire matériel le plus récent collecté à partir de l’appareil client spécifié.  

    - Le nœud **État de la station de travail** affiche la date et l’heure du dernier inventaire matériel effectué à partir de l’appareil.  

- **Historique du matériel** : historique des éléments inventoriés qui ont changé depuis le dernier cycle d’inventaire matériel.  

    - Développez un élément pour afficher un nœud **Actuel** et un ou plusieurs nœuds avec la date d’historique. Comparez les informations du nœud actuel avec l’un des nœuds historiques pour voir les éléments qui ont changés.  

> [!NOTE]  
> Par défaut, Configuration Manager supprime les données d’inventaire matériel qui ont été inactives pendant 90 jours. Ajustez ce nombre de jours dans la tâche de maintenance de site **Supprimer les historiques d’inventaire anciens**. Pour plus d’informations, consultez la rubrique [Tâches de maintenance](/sccm/core/servers/manage/maintenance-tasks).  



## <a name="bkmk_open"></a> Comment ouvrir l’Explorateur de ressources   

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, puis sélectionnez le nœud **Appareils**. Vous pouvez également sélectionner n’importe quel regroupement dans le nœud **Regroupements d’appareils**.  

2.  Sélectionnez un appareil. Dans le ruban, sous l’onglet **Accueil** et le groupe **Appareils**, cliquez sur **Démarrer** et sélectionnez **Explorateur de ressources**.   

> [!Tip]  
> Dans l’Explorateur de ressources, cliquez avec le bouton droit sur un élément dans le volet de résultats approprié pour connaître les actions supplémentaires. Cliquez sur **Propriétés** pour voir cet élément dans un autre format.  



## <a name="bkmk_bigint"></a> Utilisation de valeurs entières longues
<!--1357880--> Dans Configuration Manager versions 1802 et antérieures, l’inventaire matériel a une limite pour les entiers supérieurs à 4 294 967 296 (2^32). Cette limite peut être atteinte pour les attributs, tels que les tailles de disque dur en octets. Le point de gestion ne traite pas les valeurs entières supérieures à cette limite. Par conséquent, aucune valeur n’est stockée dans la base de données. 

À compter de la version 1806, la limite est augmentée à 18 446 744 073 709 551 616 (2^64). 

Pour les propriétés dont la valeur ne change pas, comme la taille totale du disque, vous pouvez ne pas voir immédiatement la valeur après la mise à niveau du site. La plupart des inventaires matériels se présentent sous la forme d’un état d’écart. Le client envoie uniquement les valeurs qui changent. Pour contourner ce comportement, ajoutez une autre propriété à la même classe. Avec cette action, le client met à jour toutes les propriétés de la classe qui ont changé. 



## <a name="see-also"></a>Voir aussi

Pour plus d’informations sur la façon d’afficher l’inventaire matériel des clients qui exécutent Linux et UNIX, consultez [Guide pratique pour surveiller les clients pour des serveurs Linux et UNIX](/sccm/core/clients/manage/monitor-clients-for-linux-and-unix-servers).  

L’Explorateur de ressources affiche également l’inventaire logiciel. Pour plus d’informations, consultez [Guide pratique pour utiliser l’Explorateur de ressources pour consulter l’inventaire logiciel](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).
