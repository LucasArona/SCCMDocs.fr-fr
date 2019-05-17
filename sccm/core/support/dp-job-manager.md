---
title: DP Job Queue Manager
titleSuffix: Configuration Manager
description: Utilisez DP Job Queue Manager pour dépanner et gérer les travaux de distribution de contenu sur les points de distribution Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 720311c9bd4a8ecb9420801881d7c6c142457db3
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500871"
---
# <a name="dp-job-queue-manager"></a>DP Job Queue Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Distribution Point (DP) Job Queue Manager fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez-le pour dépanner et gérer les travaux de distribution de contenu en cours sur les points de distribution Configuration Manager. 

L’outil affiche la liste des travaux que le composant Package Transfer Manager a dans sa file d’attente. Il montre également l’état des travaux : prêt à être exécuté, en cours d’exécution ou nouvelle tentative. Il vous permet de manipuler les travaux dans la file d’attente, de les déplacer plus haut dans la liste, d’annuler un travail ou de démarrer manuellement l’exécution d’un travail.

Il obtient également des informations du serveur de site sur lequel le point de distribution exécute un travail. L’outil se connecte au serveur de site via le fournisseur. Il ne se connecte pas à chaque point de distribution distant pour rassembler ces informations. Parce qu’il déclenche des actions et obtient des informations via le fournisseur, il y a un délai pour refléter les changements apportés à partir des points de distribution distants.



## <a name="usage"></a>Utilisation

Exécutez **DPJobMgr.exe**. Le menu principal de l’outil contient les onglets suivants : 

- [Connexion](#bkmk_connect) : Établit la connexion initiale au serveur de site principal  

- [Vue d’ensemble](#bkmk_overview) : résume en un affichage unique tous les travaux qui s’exécutent sur tous les points de distribution  

- [Informations sur les points de distribution](#bkmk_dp-info) : sélection de plusieurs points de distribution pour les suivre et gérer un seul travail d’intérêt  

- [Gérer les travaux](#bkmk_manage-jobs) : Affiche dans une seule vue plate une liste de tous les travaux et de leurs états. Manipulez les travaux, déplacez-les en haut de la liste, annulez-les ou démarrez-les manuellement.  


### <a name="bkmk_connect"></a> Onglet Connect (Se connecter)

Cet onglet vous permet d’établir la connexion initiale au serveur de site principal. Il utilise les informations d’identification actuelles de l’utilisateur connecté. Vous ne pouvez pas vous connecter au site d’administration centrale ni à des sites secondaires. La connexion nécessite le rôle de sécurité **Administrateur complet**.

Une fois que l’outil réussit à établir une connexion, une notification au bas de l’outil confirme qu’il est connecté au serveur de site. 


### <a name="bkmk_overview"></a> Onglet Overview (Vue d’ensemble)

Affiche un récapitulatif de tous les travaux sur tous les points de distribution. Consultez les colonnes suivantes :  

- **Point de distribution** : répertorie les noms des points de distribution  

- **Travaux en cours d’exécution** : affiche le nombre de travaux simultanés qui s’exécutent sur un point de distribution spécifique.  

    > [!Tip]  
    > Le nombre de distributions de logiciels simultanées est un paramètre de site. Modifiez ce paramètre dans les Propriétés du composant de distribution de logiciels.  

- **Nombre total de travaux** : affiche le nombre de tous les travaux ciblés pour un point de distribution spécifique. Ce nombre comprend les travaux qui s’exécutent, qui font l’objet d’une nouvelle tentative ou qui attendent d’être exécutés.  

- **Nombre total de nouvelles tentatives** : affiche le nombre de fois où des travaux ont fait l’objet d’une nouvelle tentative sur un point de distribution spécifique. Un nombre plus élevé peut représenter un problème général avec ce point de distribution spécifique.  


> [!Tip]  
> - Pour trier chaque colonne sous cet onglet, cliquez sur le nom de la colonne.  
> 
> - Actualisez manuellement les informations contenues sous cet onglet en cliquant sur **Refresh** (Actualiser).  
> 
> - Actualisez automatiquement les informations sous cet onglet en cliquant sur **Start Auto Refresh** (Démarrer l’actualisation automatique) et en définissant l’intervalle d’actualisation automatique. L’intervalle d’actualisation par défaut est de deux minutes.  


### <a name="bkmk_dp-info"></a> Onglet Distribution Point Info (Informations sur les points de distribution)

Affiche la liste de tous les points de distribution sous le site connecté. Le volet gauche liste tous les points de distribution. Cliquez sur **Select All** (Tout sélectionner) ou **Unselect All** (Tout désélectionner) au besoin, ou sélectionnez plusieurs points de distribution spécifiques dans cette liste. Le volet de gauche montre les travaux des points de distribution sélectionnés.

Il existe huit colonnes :  

- **Icône d’état** : Il existe trois icônes d’état possibles :  

    - **Prêt** : indique qu’un travail spécifique a terminé toutes les étapes de vérification. Il est prêt à être ajouté aux travaux simultanés en cours d’exécution. Les travaux avec cet état sont généralement dans une phase d’attente. En effet, ils attendent la fin des processus en cours d’exécution pour libérer de l’espace pour eux.  

    - **En cours d’exécution** : indique qu’un travail spécifique est actuellement en cours d’exécution sur un point de distribution. Pour les travaux en cours d’exécution longs (gros paquets), il y a généralement une progression (%) jusqu’à la fin. Il montre ce pourcentage dans la colonne **Progress** de cette vue. Pour les petits paquets, la colonne **Progress** peut rester vide. Le travail peut être déjà fini avant qu’il ne reçoive l’état du point de distribution distant.  

    - **Nouvelle tentative** : indique qu’un travail spécifique a échoué et est désormais dans un état de nouvelle tentative. Ce travail est retenté après l’intervalle de nouvelle tentative. Cet intervalle est configurable et défini sur 30 minutes par défaut.  

- **Logiciels** : nom du package ciblé pour un point de distribution spécifique  

- **ID du package** : ID du package ciblé pour un point de distribution spécifique  

- **Taille** : taille du package mesurée en Ko  

- **Progression** : pourcentage d’achèvement du travail. Pour plus d’informations, consultez la description de l’icône d’état **Running**.  

- **Heure de démarrage/redémarrage** : pour un travail en cours d’exécution, cette valeur est l’heure de démarrage (vert). Pour un travail de nouvelle tentative, cette valeur est l’heure de nouvelle tentative du travail.  

- **Nouvelles tentatives** : nombre de nouvelles tentatives effectuées pour ce package.  

- **Nom du point de distribution** : le nom de domaine complet (FQDN) du point de distribution  

> [!Tip]  
> - Pour trier chaque colonne sous cet onglet, cliquez sur le nom de la colonne.  
> 
> - Actualisez manuellement les informations contenues sous cet onglet en cliquant sur **Refresh** (Actualiser).  
> 
> - Actualisez automatiquement les informations sous cet onglet en cliquant sur **Start Auto Refresh** (Démarrer l’actualisation automatique) et en définissant l’intervalle d’actualisation automatique. L’intervalle d’actualisation par défaut est de deux minutes.  
> 
> - Si vous devez modifier un travail particulier, cliquez avec le bouton droit sur le travail de cette vue et sélectionnez **Manage Job** (Gérer le travail). Cette action ouvre l’[onglet de gestion des travaux](#bkmk_manage-jobs).  


### <a name="bkmk_manage-jobs"></a> Onglet Manage Jobs (Gérer les travaux)

Affiche dans une seule vue plate une liste de tous les travaux et de leurs états. Il contient les mêmes huit colonnes que l’[onglet Distribution Point Info](#bkmk_dp-info). Dans cette vue, cliquez avec le bouton droit sur les travaux pour les actions suivantes :  

- **Exécuter**: démarre un travail dont l’état n’est pas en cours d’exécution  

- **Déplacer en haut** : déplace un ou plusieurs travaux en haut de la file d’attente. Cette action peut entraîner l’exécution immédiate des travaux. Un travail de priorité inférieure peut être interrompu en raison de cette action.  

- **Monter** : déplace un travail spécifique une ligne au-dessus. Un travail de priorité inférieure peut interrompre son exécution en raison de cette action.  

- **Descendre** : déplace un travail spécifique une ligne en dessous.  

- **Déplacer en bas** : déplace un ou plusieurs travaux en bas de la file d’attente.  

    > [!Tip]  
    > Faites glisser les travaux dans la liste pour les déplacer.  

- **Annuler** : essaie d’annuler un ou plusieurs travaux.  

    > [!Note]  
    > Vous ne pouvez pas annuler les travaux quand ils touchent à leur fin. Si le serveur de site est également un point de distribution, vous ne pouvez pas annuler les travaux sur le serveur de site.  



## <a name="see-also"></a>Voir aussi

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Package Transfer Manager](/sccm/core/plan-design/hierarchy/package-transfer-manager)
