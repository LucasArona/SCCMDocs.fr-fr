---
title: Procédures pour les groupes de limites
titleSuffix: Configuration Manager
description: Configurez des groupes de limites pour organiser logiquement les emplacements réseau associés appelés limites.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a7438a2815f615b029888d8fb1ca28f601735d5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140008"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Comment configurer des groupes de limites pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article contient des procédures à suivre pour configurer des groupes de limites. Avant de commencer, assurez-vous de bien comprendre les concepts liés aux groupes de limites. Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).



## <a name="bkmk_create"></a> Créer un groupe de limites  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie**, puis sélectionnez le nœud **Groupes de limites**.  

2.  Dans l'onglet **Accueil**, dans le groupe **Créer**, sélectionnez **Créer un groupe de limites**.  

3.  Dans la boîte de dialogue **Créer un groupe de limites**, dans l’onglet **Général**, spécifiez un **Nom** pour ce groupe de limites. Fournissez éventuellement une **description**.  

4.  Sélectionnez **OK** pour enregistrer le nouveau groupe de limites, ou passez à la section suivante pour configurer le groupe de limites.  


## <a name="bkmk_config"></a> Configurer un groupe de limites  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie**, puis sélectionnez le nœud **Groupes de limites**.  

2.  Sélectionnez le groupe de limites que vous souhaitez modifier, puis sélectionnez **Propriétés** dans le ruban. Cette action ouvre la fenêtre Propriétés du groupe de limites.  

Configurez les paramètres suivants :  
- [Ajouter ou supprimer des limites](#bkmk_add)  
- [Configurer l’attribution de site et sélectionner des serveurs de système de site](#bkmk_references)  
- [Configurer le comportement de secours](#bkmk_bg-fallback)  
- [Configurer les options du groupe de limites](#bkmk_options)  


### <a name="bkmk_add"></a> Ajouter ou supprimer des limites

Dans la fenêtre Propriétés du groupe de limites, utilisez l'onglet **Général** pour modifier les limites membres de ce groupe de limites :  

- Pour ajouter des limites, sélectionnez **Ajouter**. Dans la fenêtre Ajouter des limites, cochez la case pour une ou plusieurs limites et sélectionnez **OK**.  

- Pour supprimer des limites, sélectionnez la limite à supprimer dans la liste, puis cliquez sur **Supprimer**.  


### <a name="bkmk_references"></a> Configurer l’attribution de site et sélectionner des serveurs de système de site

Sélectionnez l'onglet **Références** dans la fenêtre Propriétés du groupe de limites pour modifier l'attribution de site et la configuration de serveur de système de site associée.  

- Pour autoriser l’utilisation de ce groupe de limites par des clients pour l’attribution de site, sélectionnez **Utiliser ce groupe limite pour l’attribution de site**. Sélectionnez ensuite un site dans la liste déroulante **Site attribué**. Pour plus d’informations, consultez [Attribution de site](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).  

- Pour associer les serveurs de système de site disponibles à ce groupe de limites, sélectionnez **Ajouter**. La fenêtre Ajouter des systèmes de site répertorie uniquement les serveurs avec des rôles de système de site pris en charge. Cochez la case d’un ou plusieurs serveurs et sélectionnez **OK**. Les serveurs sont ajoutés en tant que serveurs de système de site associés à ce groupe de limites.  

    > [!NOTE]  
    >  Vous pouvez sélectionner n'importe quelle combinaison de systèmes de site disponibles à partir de n'importe quel site dans la hiérarchie. Les systèmes de site sélectionnés figurent sous l'onglet **Systèmes de site** des propriétés de chaque limite appartenant à ce groupe de limites.  

- Pour supprimer un serveur de ce groupe de limites, sélectionnez le serveur, puis sélectionnez **Supprimer**.  

    > [!NOTE]  
    >  Pour ne plus utiliser ce groupe de limites pour l’association des systèmes de site, supprimez tous les serveurs répertoriés en tant que serveurs de système de site associés.  


### <a name="bkmk_bg-fallback"></a> Configurer le comportement de secours

Pour configurer le comportement de secours, basculez vers l’onglet **Relations** dans la fenêtre Propriétés du groupe de limites.  

- Pour créer une relation avec un autre groupe de limites :  

  - Sélectionnez **Ajouter**. Dans la fenêtre Groupes de limites de secours, sélectionnez le groupe de limites à configurer.  

  - Définissez un délai de secours pour les rôles de système de site suivants :  
    - Point de distribution  
    - Point de mise à jour logicielle  
    - Point de gestion  

      > [!Note]  
      > Par exemple, vous ouvrez la fenêtre Propriétés pour le groupe de limites Branch Office. Dans la fenêtre Groupes de limites de secours, sélectionnez le groupe de limites Main Office. Vous définissez le délai de secours du point de distribution sur `20`. Lorsque vous enregistrez cette configuration, les clients dans le groupe de limites Branch Office démarrent la recherche de contenu sur les points de distribution dans le groupe de limites Main Office après 20 minutes.  

  - Pour empêcher toute action de secours sur un groupe de limites spécifique, sélectionnez le groupe de limites, puis **Jamais d’action de secours** pour le type de rôle de système de site.  Cette action peut inclure le *groupe de limites de site par défaut*.  

- Pour modifier la configuration d’une relation existante, sélectionnez le groupe de limites dans la liste, puis **Modifier**. Cette action ouvre la fenêtre Groupes de limites de secours uniquement pour ce groupe de limites.  
 
- Pour supprimer une relation, sélectionnez le groupe de limites dans la liste, puis cliquez sur **Supprimer**.  

Pour plus d'informations, consultez [Secours](/sccm/core/servers/deploy/configure/boundary-groups#fallback). 


### <a name="bkmk_options"></a> Configurer les options du groupe de limites
<!--1356193--> Depuis la version 1806, pour configurer des options supplémentaires pour les clients dans ce groupe de limites, accédez à l’onglet **Options**. Pour plus d’informations, consultez [Options de groupe de limites pour les téléchargements à partir de pairs](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).

- **Autoriser les téléchargements à partir de pairs dans ce groupe de limites** : Cette option est activée par défaut. Le point de gestion fournit aux clients une liste d’emplacements de contenu qui comprend des sources de pairs.  

    - **Durant les téléchargements à partir de pairs, utiliser uniquement des pairs situés dans le même sous-réseau** : Ce paramètre dépend de celui illustré ci-dessus. Lorsque cette option est activée, le point de gestion n’inclut dans la liste des emplacements de contenu que les sources de pairs qui se trouvent dans le même sous-réseau que le client.  


## <a name="bkmk_site-fallback"></a> Configurer un site de secours pour l’attribution de site automatique  

Si les clients ne sont pas dans un groupe de limites avec un site attribué, affectez-les à ce site lors de leur installation.

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2.  Dans l'onglet **Accueil** du ruban, dans le groupe **Sites**, sélectionnez **Paramètres de hiérarchie**.  

3.  Dans l’onglet **Général**, cochez la case **Utiliser un site de secours**. Sélectionnez ensuite un site dans la liste déroulante **Site de secours**.  

4.  Cliquez sur **OK** pour enregistrer la configuration.  

Pour plus d’informations, consultez [Attribution de site](/sccm/core/servers/deploy/configure/boundary-groups#site-assignment).


## <a name="bkmk_proc-prefer"></a> Activer l’utilisation des points de gestion préférés  

Pour plus d’informations, consultez [Points de gestion préférés](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_preferred).

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Dans l'onglet **Accueil** du ruban, dans le groupe **Sites**, sélectionnez **Paramètres de hiérarchie**.  

3. Dans l’onglet **Général**, sélectionnez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**.  

4. Cliquez sur **OK** pour enregistrer la configuration.  

