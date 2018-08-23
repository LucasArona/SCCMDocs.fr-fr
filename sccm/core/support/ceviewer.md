---
title: Collection Evaluation Viewer
titleSuffix: Configuration Manager
description: Utilisez Collection Evaluation Viewer pour voir et dépanner le processus d’évaluation des regroupements dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: caad2d93-087c-4dc0-a2a7-6a2fd808b4c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c052979ad310273669d5a7897213bffd9f7e213
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386570"
---
# <a name="collection-evaluation-viewer"></a>Collection Evaluation Viewer

*S’applique à : System Center Configuration Manager (Current Branch)*

Collection Evaluation Viewer fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez-le pour voir et dépanner le processus d’évaluation des regroupements sur le serveur de site principal.

Cet outil montre les informations suivantes :  

- Informations historiques et en direct des évaluations complètes et incrémentielles de regroupements  

- État de la file d’attente des évaluations  

- Durée des évaluations de regroupements  

- Regroupements en cours d’évaluation  

- Estimation de l’heure de début et de fin d’une évaluation de regroupement  



## <a name="about-collection-evaluation"></a>À propos des évaluations de regroupements

Le processus d’évaluation des regroupements s’exécute en évaluant les règles d’appartenance d’un regroupement pour mettre à jour ses membres. Le site place un regroupement qu’il évalue dans l’une des quatre files d’attente suivantes :  

- **Manual Queue** (File d’attente manuelle) : Pour les regroupements qu’un administrateur a sélectionnés manuellement dans la console pour évaluation  

- **New Queue** (Nouvelle file d’attente) : Pour les regroupements qui viennent d’être créés  

- **Full Queue** (File d’attente complète) : Pour les regroupements devant faire l’objet d’une évaluation complète  

- **Incremental Queue** (File d’attente incrémentielle) : Pour les regroupements avec une évaluation incrémentielle  

Quatre threads s’exécutent pour évaluer les regroupements des files d’attente ci-dessus. Chaque file d’attente comprend une série de tableaux, et chaque tableau comprend les regroupements à évaluer. Le thread en cours d’exécution pour la file d’attente sélectionne un regroupement dans le tableau et exécute l’évaluation. La longueur de la file d’attente indique le nombre de tableaux dans la file d’attente.



## <a name="requirements"></a>Configuration requise

- Exécutez l’outil sur le serveur de site  

- Exécutez l’outil via un utilisateur administrateur avec au moins le rôle **Analyste en lecture seule**  

- L’utilisateur doit aussi avoir l’autorisation **Lecture** sur la base de données de site dans SQL



## <a name="usage"></a>Utilisation

Exécutez **CEViewer.exe**. Le menu principal de l’outil contient les onglets suivants : 

- [Connect](#bkmk_connect) (Se connecter) : Établit la connexion initiale au serveur de site principal et à SQL Server  

- [Full Evaluation](#bkmk_full-eval) (Évaluation complète) : Fournit des informations détaillées sur toutes les évaluations complètes déjà effectuées   

- [Incremental Evaluation](#bkmk_incremental-eval) (Évaluation incrémentielle) : Fournit des informations détaillées sur toutes les évaluations incrémentielles déjà effectuées  

- [All Queues](#bkmk_all-q) (Toutes les files d’attente) : Récapitule les évaluations de regroupements actuelles des quatre files d’attente  

- [Manual Queue](#bkmk_manual-q) (File d’attente manuelle) : Fournit des informations détaillées sur l’évaluation de regroupement actuelle de la file d’attente manuelle  

- [New Queue](#bkmk_new-q) (Nouvelle file d’attente) : Fournit des informations détaillées sur l’évaluation de regroupement actuelle de la nouvelle file d’attente  

- [Full Queue](#bkmk_full-q) (File d’attente complète) : Fournit des informations détaillées sur l’évaluation de regroupement actuelle de la file d’attente complète  

- [Incremental Queue](#bkmk_incremental-q) (File d’attente incrémentielle) : Fournit des informations détaillées sur l’évaluation de regroupement actuelle de la file d’attente incrémentielle  


### <a name="bkmk_connect"></a> Onglet Connect (Se connecter)

Cet onglet vous permet d’établir la connexion initiale au serveur de site principal. L’outil établit également une connexion au serveur SQL qui héberge la base de données de site.

Les connexions au serveur de site principal et aux serveurs SQL utilisent les informations d’identification actuelles de l’utilisateur connecté. Les connexions au site d’administration centrale ou à un site secondaire ne sont pas prises en charge. Aucun processus d’évaluation de regroupement ne s’exécute sur ces sites.

Une fois que l’outil réussit à établir une connexion, une notification apparaît en bas de Collection Evaluation Viewer qui confirme la connexion de l’outil à SQL server. 


### <a name="bkmk_full-eval"></a> Onglet Full Evaluation (Évaluation complète)

Affiche des informations détaillées sur les évaluations de regroupements complètes déjà effectuées. Il existe huit colonnes :  

- **Collection Name** : Nom du regroupement  

- **Site ID** : ID de site du regroupement   

- **Run Time** : Durée d’exécution de la dernière évaluation de regroupement, en secondes  

- **Last Evaluation Completion Time** : Heure de fin de la dernière évaluation de regroupement  

- **Next Evaluation Time** : Heure de début de la prochaine évaluation complète  

- **Member Changes** : Changements de membre dans la dernière évaluation de regroupement Ces changements sont plus (membres ajoutés) ou moins (membres supprimés).  

- **Last Member Change Time** : Heure du dernier changement d’appartenance dans l’évaluation de regroupement  

- **Percent** : Pourcentage de la durée d’évaluation de ce regroupement sur la durée totale de l’évaluation (tous les regroupements)  


### <a name="bkmk_incremental-eval"></a> Onglet Incremental evaluation (Évaluation incrémentielle)

Affiche des informations détaillées sur les évaluations de regroupements incrémentielles déjà effectuées. Il existe sept colonnes :  

- **Collection Name** : Nom du regroupement  

- **Site ID** : ID de site du regroupement   

- **Run Time** : Durée d’exécution de la dernière évaluation de regroupement, en secondes  

- **Last Evaluation Completion Time** : Heure de fin de la dernière évaluation de regroupement  

- **Member Changes** : Changements de membre dans la dernière évaluation de regroupement Ces changements sont plus (membres ajoutés) ou moins (membres supprimés).  

- **Last Member Change Time** : Heure du dernier changement d’appartenance dans l’évaluation de regroupement  

- **Percent** : Pourcentage de la durée d’évaluation de ce regroupement sur la durée totale de l’évaluation (tous les regroupements)  


### <a name="bkmk_all-q"></a>Onglet All Queues (Toutes les files d’attente)

Récapitule les évaluations de regroupements en direct des quatre files d’attente. Il existe six sections :  

- **Summary** : Liste le nombre total de regroupements et la longueur de la file d’attente de tous les regroupements des quatre files d’attente  

- **Running Evaluation** : Liste le regroupement en cours d’évaluation dans chaque file d’attente et la durée de l’exécution  

- **Manual Update** : Affiche un petit récapitulatif des regroupements en cours d’évaluation, une estimation de l’heure de fin et l’ordre de l’évaluation dans la file d’attente manuelle  

- **New collection** : Affiche un petit récapitulatif des regroupements en cours d’évaluation, une estimation de l’heure de fin et l’ordre de l’évaluation dans la nouvelle file d’attente  

- **Full evaluation** : Affiche un petit récapitulatif des regroupements en cours d’évaluation, une estimation de l’heure de fin et l’ordre de l’évaluation dans la file d’attente des évaluations complètes  

- **Incremental evaluation** : Affiche un petit récapitulatif des regroupements en cours d’évaluation, une estimation de l’heure de fin et l’ordre de l’évaluation dans la file d’attente des évaluations incrémentielles  


### <a name="bkmk_manual-q"></a> Onglet Manual Queue (File d’attente manuelle)

Affiche des informations sur l’évaluation de regroupement manuelle en cours. L’ordre dans la liste est l’ordre dans lequel le regroupement est évalué. Il existe quatre colonnes :  

- **Collection Name** : Nom du regroupement  

- **Site ID** : ID de site du regroupement   

- **Estimated Completion Time** : Estimation de l’heure de fin de l’évaluation  

- **Estimated Run Time** : Estimation de la durée d’exécution de l’évaluation au format jour:heure:minute:seconde  


### <a name="bkmk_new-q"></a> Onglet New Queue (Nouvelle file d’attente)

Affiche des informations en direct sur la nouvelle évaluation de regroupement en cours. L’ordre dans la liste est l’ordre dans lequel le regroupement est évalué. Il existe quatre colonnes :  

- **Collection Name** : Nom du regroupement  

- **Site ID** : ID de site du regroupement   

- **Estimated Completion Time** : Estimation de l’heure de fin de l’évaluation  

- **Estimated Run Time** : Estimation de la durée d’exécution de l’évaluation au format jour:heure:minute:seconde  


### <a name="bkmk_full-q"></a> Onglet Full Queue (File d’attente complète)

Affiche des informations sur l’évaluation de regroupement complète en cours. L’ordre dans la liste est l’ordre dans lequel le regroupement est évalué. Il existe quatre colonnes :  

- **Collection Name** : Nom du regroupement  

- **Site ID** : ID de site du regroupement   

- **Estimated Completion Time** : Estimation de l’heure de fin de l’évaluation  

- **Estimated Run Time** : Estimation de la durée d’exécution de l’évaluation au format jour:heure:minute:seconde  


### <a name="bkmk_incremental-q"></a> Onglet Incremental Queue (File d’attente incrémentielle)

Affiche des informations sur l’évaluation de regroupement incrémentielle en cours. L’ordre dans la liste est l’ordre dans lequel le regroupement est évalué. Il existe quatre colonnes :  

- **Collection Name** : Nom du regroupement  

- **Site ID** : ID de site du regroupement   

- **Estimated Completion Time** : Estimation de l’heure de fin de l’évaluation  

- **Estimated Run Time** : Estimation de la durée d’exécution de l’évaluation au format jour:heure:minute:seconde  



