---
title: Policy Spy
titleSuffix: Configuration Manager
description: Utilisez Policy Spy pour voir et dépanner le système de stratégies sur les clients Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1012ec24-27d9-4193-8236-918d283c7448
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 297aa9f8756b0c7214381e5e688f26cc21645fc4
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500856"
---
# <a name="policy-spy"></a>Policy Spy

*S’applique à : System Center Configuration Manager (Current Branch)*

Policy Spy fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Cet outil sert à voir et à dépanner le système de stratégies sur les clients Configuration Manager. Exécutez **PolicySpy.exe** pour ouvrir l’interface utilisateur. Pour plus d’informations sur l’utilisation de la ligne de commande, consultez [Syntaxe de la ligne de commande](#bkmk_policyspy-syntax).

> [!Important]  
> Exécutez Policy Spy en tant qu’administrateur. Si vous ne l’avez pas **exécuté en tant qu’administrateur**, vous voyez l’erreur suivante dans les informations du client :  
> `There is no client installed on this machine. Connection to client policy failed with error 80041003`


## <a name="bkmk_policyspy-syntax"></a> Syntaxe de la ligne de commande

Policy Spy s’utilise principalement via son interface utilisateur. Il ne fournit pas d’options de ligne de commande limitées pour prendre en charge l’automatisation et le traitement par lots.

`PolicySpy.exe [/export <ExportFilename> [<computername>]]`

### <a name="option-export"></a>Option : `/export`
Cette option exporte en mode silencieux la stratégie de l’ordinateur local ou distant. `<ExportFilename>` est le nom du fichier dans lequel l’outil enregistre la stratégie exporté XML. Si vous spécifiez l’option `<computername>`, Policy Spy exporte la stratégie de cet ordinateur au lieu de celle de l’ordinateur local.

> [!Note]  
> Cette option de ligne de commande n’offre pas le moyen de spécifier des informations d’identification utilisateur. Pour utiliser d’autres informations d’identification permettant d’accéder à un ordinateur distant, utilisez la commande **runas** pour ouvrir une nouvelle invite de commandes avec les informations d’identification de sécurité nécessaires.  


## <a name="usage"></a>Utilisation

### <a name="tools-menu"></a>Menu Tools

Les actions suivantes sont disponibles dans le menu **Tools** (Outils) :  

- **Ouvrir l’ordinateur distant** : Se connecte à la stratégie de configuration du client Gestionnaire de configuration sur un ordinateur distant. Utilisez la boîte de dialogue de connexion pour récupérer le nom de l’ordinateur distant et les informations d’identification utilisateur facultatives. Si la connexion échoue, il affiche des informations sur l’erreur dans le volet des informations du client. Si la connexion échoue encore, essayez de vous connecter en sélectionnant **Refresh** dans le menu **Edit**, ou en appuyant sur F5.  

- **Ouvrir le fichier** : Ouvre un fichier d’exportation de stratégie (XML) créé par l’option **Exporter la stratégie**. L’outil affiche la stratégie exportée exactement comme une stratégie en direct. Il désactive certaines fonctionnalités qui s’appliquent uniquement quand vous vous connectez véritablement à un client.  

- **Demander des affectations de machines** : Déclenche une requête pour des affectations de stratégie machine sur l’ordinateur cible. Cette fonctionnalité est désactivée lors de l’affichage de la stratégie exportée.  

- **Évaluer la stratégie machine** : Déclenche une évaluation de la stratégie machine sur l’ordinateur cible. Cette fonctionnalité est désactivée lors de l’affichage d’une stratégie exportée.  

- **Demander des affectations d’utilisateurs** : Déclenche une requête pour des affectations de stratégie utilisateur pour l’utilisateur actuellement connecté. Cette fonctionnalité est uniquement disponible lors de l’affichage d’une stratégie sur l’ordinateur local.  

- **Évaluer la stratégie utilisateur** : Déclenche une évaluation de la stratégie utilisateur pour l’utilisateur actuellement connecté. Cette fonctionnalité est uniquement disponible lors de l’affichage d’une stratégie sur l’ordinateur local.  

- **Stratégie de réinitialisation** : Supprime toutes les stratégies différentes de celles par défaut et réinitialise les cookies de stratégie pour le site. Il déclenche ensuite une demande pour des affectations de stratégie ordinateur. Cette fonctionnalité est désactivée lors de l’affichage d’une stratégie exportée.  

- **Exporter la stratégie** : Exporte la stratégie de l’ordinateur cible dans un fichier XML. Affichez ce fichier sur n’importe quel ordinateur avec Policy Spy. Pour ouvrir le fichier d’exportation, sélectionnez **Open File** dans le menu **Tools**. Cette fonctionnalité est désactivée lors de l’affichage d’une stratégie exportée.  


### <a name="edit-menu"></a>Menu Edit

Les actions suivantes sont disponibles dans le menu **Edit** (Edition) :  

- **Supprimer** : Supprime l’instance sélectionnée du volet de résultats. Cette action est uniquement prise en charge pour les instances de stratégie. Si vous essayez de supprimer autre chose que des instances de stratégie, l’outil affiche un message d’erreur. Cette fonctionnalité est désactivée lors de l’affichage d’une stratégie exportée.  

- **Actualiser** : Actualise tous les résultats pour afficher les dernières informations. Tous les nœuds de l’arborescence qui sont développés avant l’actualisation sont automatiquement développés par la suite. Si Policy Spy n’arrive pas à se connecter à la stratégie de l’ordinateur cible, il réessaie. Cette fonctionnalité est désactivée lors de l’affichage d’une stratégie exportée.  

- **Effacer les événements** : Efface tous les éléments de l’onglet Événements.  



## <a name="results-pane"></a>Volet Résultats

Le volet des résultats affiche différentes vues du système de stratégies sur l’ordinateur cible. Accédez à ces vues en cliquant sur l’un des quatre onglets suivants : 
- [Actual](#bkmk_policyspy-actual)
- [Requested](#bkmk_policyspy-requested)
- [Par défaut](#bkmk_policyspy-default)
- [Events](#bkmk_policyspy-events)


### <a name="bkmk_policyspy-actual"></a> Actual

Cet onglet affiche la stratégie actuelle du client. La stratégie actuelle détermine le comportement du client et le comportement de ses agents, comme la distribution de logiciels et l’inventaire. L’onglet affiche les résultats sous la forme d’une arborescence avec un nœud racine pour l’espace de noms de l’ordinateur et chaque espace de noms spécifique à l’utilisateur. Développez un nœud d’espace de noms pour afficher une liste de classes. Développez une classe pour afficher une liste de ses instances. La liste de classes inclut uniquement les classes qui ont des instances.


### <a name="bkmk_policyspy-requested"></a> Requested

Cet onglet affiche les affectations de stratégie que le client a récupérées de son site attribué. L’onglet affiche les résultats sous la forme d’une arborescence avec un nœud racine pour l’espace de noms de l’ordinateur et chaque espace de noms spécifique à l’utilisateur. Le développement d’un nœud d’espace de noms affiche les nœuds suivants :  

- **Configuration** : Affiche une liste de classes de configuration dérivées de CCM_Policy_Config, comprenant l’objet de la stratégie, les affectations etc.  

- **Paramètres** : Affiche tous les paramètres actifs générés par les stratégies. Les paramètres sont affichés sous le nœud Configuration. 

> [!Note]   
> Plusieurs instances peuvent exister avec le même nom, car le client n’a pas fusionné ces paramètres dans un jeu résultant final. Policy Spy affiche les instances sous ce nœud en utilisant les propriétés RealKey au lieu de leurs véritables clés de stratégie. Mettez en corrélation ces instances avec le jeu résultant affiché sous l’onglet Actual.  


### <a name="bkmk_policyspy-default"></a> Default

Cet onglet affiche les mêmes informations que l’onglet **Requested**. Il inclut également le contenu des espaces de noms DefaultMachine et DefaultUser.


### <a name="bkmk_policyspy-events"></a> Events

Cet onglet affiche les événements de l’agent de stratégie quand ils se produisent. La vue crée un abonnement aux événements WMI pour tous les événements dérivés de CCM_PolicyAgent_Event. La vue affiche un maximum de 200 événements. Il supprime les événements les plus anciens du haut de la liste, au besoin. Si vous sélectionnez le dernier élément dans la liste, la liste défile automatiquement vers le bas quand elle ajoute de nouveaux événements. Sinon, la vue garde sa position actuelle, et vous devez faire défiler vers le bas ou appuyer sur la touche Fin pour voir les nouveaux événements. Cette vue est toujours vide lors de l’affichage d’une stratégie exportée.



## <a name="client-info-pane"></a>Volet des informations du client
Le volet des informations du client affiche une liste de propriétés de l’ordinateur cible. Il affiche les propriétés suivantes, si elles sont disponibles :  
- Nom
- ID
- Version
- Site
- Point de gestion attribué
- Point de gestion résident
- Point de gestion proxy
- État du proxy



## <a name="details-pane"></a>Volet Détails
Le volet de détails affiche des informations détaillées sur la sélection actuelle. Si aucune sélection n’est active, il affiche des informations sur Policy Spy, notamment la version. Sinon, il affiche une représentation MOF (Manage Object Format) de l’élément sélectionné.

Policy Spy utilise sa propre routine de génération du format MOF pour créer un affichage HTML plus convivial que le format MOF en texte brut généré par WMI. Ce comportement permet à Policy Spy d’ajouter les fonctionnalités suivantes pour rendre le format MOF plus lisible :  

- Mise en surbrillance de la syntaxe  

- Mise en retrait des tableaux et des objets  

- Les propriétés sont organisées en groupes système, hérités et locaux. Par défaut, il réduit le système et les groupes hérités. Vous pouvez voir immédiatement les propriétés que l’instance utilise en réalité.  

- Copiez le format MOF ou MOF en texte brut dans le Presse-papiers. Cette fonctionnalité est utile pour coller le format MOF dans d’autres applications en appelant directement l’outil MofComp.  

Pour les instances d’objets de stratégie dérivées de CCM_Policy_Policy, le volet de détails affiche le corps de la stratégie sous le format MOF qui s’affiche. Si le client n’a pas encore téléchargé le corps de la stratégie, Policy Spy affiche un lien hypertexte. Cliquez sur le lien pour télécharger le corps de la stratégie directement du point de gestion du client. Si l’outil télécharge avec succès le corps de la stratégie, il remplace le lien hypertexte par le contenu de la réponse. Sinon, Policy Spy met à jour l’affichage indiquant que la demande a échoué.

