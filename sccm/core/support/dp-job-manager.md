---
title: DP Job Queue Manager
titleSuffix: Configuration Manager
description: Utilisez DP Job Queue Manager pour dépanner et gérer les travaux de distribution de contenu sur les points de distribution Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4b72922a-d11e-4aef-b309-19f5f0716f32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5218d47ae8699ee0feb0cf59405833ec4cc49569
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385830"
---
# <a name="dp-job-queue-manager"></a>DP Job Queue Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Distribution Point (DP) Job Queue Manager fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez-le pour dépanner et gérer les travaux de distribution de contenu en cours sur les points de distribution Configuration Manager. 

L’outil affiche la liste des travaux que le composant Package Transfer Manager a dans sa file d’attente. Il montre également l’état des travaux : prêt à être exécuté, en cours d’exécution ou nouvelle tentative. Il vous permet de manipuler les travaux dans la file d’attente, de les déplacer plus haut dans la liste, d’annuler un travail ou de démarrer manuellement l’exécution d’un travail.

Il obtient également des informations du serveur de site sur lequel le point de distribution exécute un travail. L’outil se connecte au serveur de site via le fournisseur. Il ne se connecte pas à chaque point de distribution distant pour rassembler ces informations. Parce qu’il déclenche des actions et obtient des informations via le fournisseur, il y a un délai pour refléter les changements apportés à partir des points de distribution distants.



## <a name="usage"></a>Utilisation

Exécutez **DPJobMgr.exe**. Le menu principal de l’outil contient les onglets suivants : 

- [Connect](#bkmk_connect) (Se connecter) : Établit la connexion initiale au serveur de site principal  

- [Overview](#bkmk_overview) (Vue d’ensemble) : Récapitule dans une vue unique tous les travaux qui s’exécutent sur tous les points de distribution  

- [Distribution Point Info](#bkmk_dp-info) (Infos sur les points de distribution) : Sélection de plusieurs points de distribution pour les suivre et gérer un seul travail d’intérêt  

- [Manage jobs](#bkmk_manage-jobs) (Gérer les travaux) : Affiche dans une seule vue plate une liste de tous les travaux et de leurs états. Manipulez les travaux, déplacez-les en haut de la liste, annulez-les ou démarrez-les manuellement.  


### <a name="bkmk_connect"></a> Onglet Connect (Se connecter)

Cet onglet vous permet d’établir la connexion initiale au serveur de site principal. Il utilise les informations d’identification actuelles de l’utilisateur connecté. Vous ne pouvez pas vous connecter au site d’administration centrale ni à des sites secondaires. La connexion nécessite le rôle de sécurité **Administrateur complet**.

Une fois que l’outil réussit à établir une connexion, une notification au bas de l’outil confirme qu’il est connecté au serveur de site. 


### <a name="bkmk_overview"></a> Onglet Overview (Vue d’ensemble)

Affiche un récapitulatif de tous les travaux sur tous les points de distribution. Consultez les colonnes suivantes :  

- **Distribution Point** (Point de distribution) : Liste les noms des points de distribution  

- **Running Jobs** (Travaux en cours d’exécution) : Affiche le nombre de travaux simultanés qui s’exécutent sur un point de distribution spécifique.  

    > [!Tip]  
    > Le nombre de distributions de logiciels simultanées est un paramètre de site. Modifiez ce paramètre dans les Propriétés du composant de distribution de logiciels.  

- **Total Jobs** (Total des travaux) : Affiche le nombre de tous les travaux destinés à un point de distribution particulier. Ce nombre comprend les travaux qui s’exécutent, qui font l’objet d’une nouvelle tentative ou qui attendent d’être exécutés.  

- **Total Retries** (Total de nouvelles tentatives) : Indique le nombre de nouvelles tentatives sur les travaux d’un point de distribution spécifique. Un nombre plus élevé peut représenter un problème général avec ce point de distribution spécifique.  


> [!Tip]  
> - Pour trier chaque colonne sous cet onglet, cliquez sur le nom de la colonne.  
> 
> - Actualisez manuellement les informations contenues sous cet onglet en cliquant sur **Refresh** (Actualiser).  
> 
> - Actualisez automatiquement les informations sous cet onglet en cliquant sur **Start Auto Refresh** (Démarrer l’actualisation automatique) et en définissant l’intervalle d’actualisation automatique. L’intervalle d’actualisation par défaut est de deux minutes.  


### <a name="bkmk_dp-info"></a> Onglet Distribution Point Info (Informations sur les points de distribution)

Affiche la liste de tous les points de distribution sous le site connecté. Le volet gauche liste tous les points de distribution. Cliquez sur **Select All** (Tout sélectionner) ou **Unselect All** (Tout désélectionner) au besoin, ou sélectionnez plusieurs points de distribution spécifiques dans cette liste. Le volet de gauche montre les travaux des points de distribution sélectionnés.

Il existe huit colonnes :  

- **Status Icon** (Icône d’état) : Il existe trois icônes d’état possibles :  

    - **Ready** (Prêt) : Indique qu’un travail particulier a terminé toutes les étapes de vérification. Il est prêt à être ajouté aux travaux simultanés en cours d’exécution. Les travaux avec cet état sont généralement dans une phase d’attente. En effet, ils attendent la fin des processus en cours d’exécution pour libérer de l’espace pour eux.  

    - **Running** (En cours d’exécution) : Indique qu’un travail particulier est en cours d’exécution sur un point de distribution. Pour les travaux en cours d’exécution longs (gros paquets), il y a généralement une progression (%) jusqu’à la fin. Il montre ce pourcentage dans la colonne **Progress** de cette vue. Pour les petits paquets, la colonne **Progress** peut rester vide. Le travail peut être déjà fini avant qu’il ne reçoive l’état du point de distribution distant.  

    - **Retry** (Nouvelle tentative) : Indique qu’un travail particulier a échoué et est désormais dans un état de nouvelle tentative. Ce travail est retenté après l’intervalle de nouvelle tentative. Cet intervalle est configurable et défini sur 30 minutes par défaut.  

- **Software** (Logiciel) : Nom du paquet qui est destiné à un point de distribution spécifique  

- **Package ID** (ID de paquet) : ID du paquet qui est destiné à un point de distribution spécifique  

- **Size** (Taille) : Taille du paquet en Ko  

- **Progress** (Progression) : Pourcentage d’achèvement du travail. Pour plus d’informations, consultez la description de l’icône d’état **Running**.  

- **Start/Restart Time** (Heure de démarrage/redémarrage) : Pour un travail en cours d’exécution, cette valeur est l’heure de démarrage (vert). Pour un travail de nouvelle tentative, cette valeur est l’heure de nouvelle tentative du travail.  

- **Retries** (Nouvelles tentatives) : Nombre de nouvelles tentatives sur ce paquet.  

- **Distribution Point Name** (Nom du point de distribution) : Nom de domaine complet (FQDN) du point de distribution  

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

- **Run** (Exécuter) : Démarre un travail qui se trouve dans un état autre que l’état Running  

- **Move to Top** (Déplacer en haut) : Déplace un ou plusieurs travaux en haut de la file d’attente. Cette action peut entraîner l’exécution immédiate des travaux. Un travail de priorité inférieure peut être interrompu en raison de cette action.  

- **Move Up** (Monter) : Déplace un travail particulier une ligne au-dessus. Un travail de priorité inférieure peut interrompre son exécution en raison de cette action.  

- **Move Down** (Descendre) : Déplace un travail particulier une ligne en dessous.  

- **Move to Bottom** (Déplacer en bas) : Déplace un ou plusieurs travaux en bas de la file d’attente.  

    > [!Tip]  
    > Faites glisser les travaux dans la liste pour les déplacer.  

- **Cancel** (Annuler) : Tente d’annuler un ou plusieurs travaux.  

    > [!Note]  
    > Vous ne pouvez pas annuler les travaux quand ils touchent à leur fin. Si le serveur de site est également un point de distribution, vous ne pouvez pas annuler les travaux sur le serveur de site.  



## <a name="see-also"></a>Voir aussi

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Package Transfer Manager](/sccm/core/plan-design/hierarchy/package-transfer-manager)
