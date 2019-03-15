---
title: Console Configuration Manager
titleSuffix: Configuration Manager
description: Découvrez comment naviguer dans la console Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f9c06f40af1134055d4038fd23954b3f4c59682
ms.sourcegitcommit: 544f335cfd1bfd0a1d4973439780e9f5e9ee8bed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57562106"
---
# <a name="using-the-configuration-manager-console"></a>Utilisation de la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les administrateurs se servent de la console Configuration Manager pour gérer l’environnement Configuration Manager. Cet article aborde les principes fondamentaux de la navigation dans la console.  



## <a name="connect-to-a-site-server"></a>Se connecter à un serveur de site

La console se connecte à votre serveur de site d’administration centrale ou à vos serveurs de site principal. Vous ne pouvez pas connecter une console Configuration Manager à un site secondaire. Vous pouvez [installer la console Configuration Manager](/sccm/core/servers/deploy/install/install-consoles). Pendant l’installation, vous avez spécifié le nom de domaine complet du serveur de site auquel la console se connecte. 

Pour vous connecter à un autre serveur de site, effectuez les étapes suivantes : 

1. Cliquez sur la flèche en haut du [ruban](#ribbon), puis sélectionnez **Connecter à un nouveau site**.  

    ![Connecter la console à un nouveau site](media/connect-to-a-new-site.png)  

2. Tapez le nom de domaine complet du serveur de site. Si vous vous êtes précédemment connecté au serveur de site, sélectionnez le serveur dans la liste déroulante.  

    ![Dans la fenêtre Connexion au site, entrez le nom de domaine complet du serveur de site](media/site-server-fqdn.png)  

3. Sélectionnez **Connexion**.  


À compter de la version 1810, vous pouvez spécifier le niveau d’authentification minimal pour les administrateurs qui accèdent aux sites Configuration Manager. Cette fonctionnalité force les administrateurs à se connecter à Windows avec le niveau requis. Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth). <!--1357013-->  



## <a name="navigation"></a>Navigation

Selon le rôle de sécurité qui vous est attribué, certaines zones de la console peuvent ne pas être visibles. Pour plus d’informations sur les rôles, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration). 


### <a name="workspaces"></a>Espaces de travail

La console Configuration Manager possède quatre **espaces de travail** :  

- **Ressources et Conformité**  

- **Bibliothèque de logiciels**  

- **Monitoring**  

- **Administration**  

![Espaces de travail Configuration Manager avec menu contextuel](media/configuration-manager-workspaces.png)  

Réorganisez les boutons des espaces de travail en sélectionnant la flèche vers le bas et en sélectionnant **Options du volet de navigation**. Sélectionnez un élément à **déplacer vers le haut** ou **déplacer vers le bas**. Sélectionnez **Réinitialiser** pour restaurer l’ordre des boutons par défaut.  

 ![Fenêtre des options du volet de navigation pour réorganiser les espaces de travail](media/navigation-pane-options.png)  

Pour réduire un bouton d’un espace de travail, sélectionnez **Afficher moins de boutons**. Le dernier espace de travail de la liste est réduit en premier. Sélectionnez un bouton réduit, puis choisissez **Afficher plus de boutons** pour rétablir la taille d’origine du bouton.   

![Espaces de travail réduits dans la console Configuration Manager](media/workspace-buttons.png)  


### <a name="nodes"></a>Nœuds

Les espaces de travail sont un regroupement de **nœuds**. Il peut s’agir, par exemple, du nœud **Groupes de mises à jour logicielles** de l’espace de travail **Bibliothèque de logiciels**. 

Une fois que vous êtes dans le nœud, vous pouvez sélectionner la flèche pour réduire le volet de navigation.  

![Exemple de nœud et mise en surbrillance de la flèche Réduire](media/software-update-groups-node.png)  

Quand vous réduisez votre volet de navigation, utilisez la **barre de navigation** pour vous déplacer dans la console.  

![Volet de navigation réduit de Configuration Manager](media/minimized-navigation-pane.png)  

Dans la console, les nœuds sont parfois organisés en dossiers. Si vous cliquez directement sur le dossier, vous accédez généralement à un **index de navigation** ou un **tableau de bord**.  

![Index de navigation des mises à jour logicielles de Configuration Manager](media/software-updates-navigation-index.png)  


### <a name="ribbon"></a>Ruban 

Le ruban se situe en haut de la console Configuration Manager. Le ruban peut avoir plusieurs onglets et peut être réduit à l’aide de la flèche sur la droite. Les boutons du ruban changent en fonction du nœud. La plupart des boutons du ruban sont également disponibles dans les menus contextuels.  

![Exemple de ruban, mise en surbrillance de plusieurs onglets et de la flèche Réduire](media/ribbon.png)   


### <a name="details-pane"></a>Volet de détails

Vous pouvez obtenir des informations supplémentaires sur les éléments en examinant le volet de détails. Le volet de détails peut présenter un ou plusieurs onglets. Les onglets varient en fonction du nœud.  

![Exemple de volet de résultats dans Configuration Manager](media/details-pane.png)   


### <a name="columns"></a>Colonnes 

Vous pouvez ajouter, supprimer, réorganiser et redimensionner des colonnes. Ces actions vous permettent d’afficher les données que vous préférez. Les colonnes disponibles varient en fonction du nœud. Pour ajouter ou supprimer une colonne à partir de votre vue, cliquez avec le bouton droit sur un en-tête de colonne existant, puis sélectionnez un élément. Réorganisez les colonnes en faisant glisser l’en-tête de colonne jusqu’à l’emplacement souhaité.  

![Ajouter une colonne dans Configuration Manager](media/add-columns.png)  

Au bas du menu contextuel de la colonne, vous pouvez trier ou regrouper selon une colonne. En outre, vous pouvez trier selon une colonne en cliquant sur son en-tête.  

![Configuration Manager, regrouper selon une colonne](media/column-group-by.png)  



## <a name="command-line-options"></a>Options de ligne de commande

La console Configuration Manager comprend les options de ligne de commande suivantes :

|Option|Description|  
|------------|-----------------|  
|`/sms:debugview=1`|Un DebugView est inclus dans tous les ResultView qui spécifient une vue. DebugView affiche les propriétés brutes (noms et valeurs).|  
|`/sms:NamespaceView=1`|Affiche la vue d’espace de noms dans la console.|  
|`/sms:ResetSettings`|La console ignore la connexion rendue persistante par l’utilisateur et les états de vue. La taille de la fenêtre n’est pas réinitialisée.|  
|`/sms:IgnoreExtensions`|Désactive les extensions Configuration Manager.|  
|`/sms:NoRestore`|La console ignore la navigation précédente au sein des nœuds persistants.|  



## <a name="tips"></a>Conseils

### <a name="send-feedback"></a>Envoyer des commentaires
<!--1357542-->

À compter de la version 1806, vous devez envoyer vos commentaires produit via la console.  

- **Envoyer un sourire** : envoyer des commentaires sur ce qui vous plaît  

- **Envoyer un smiley mécontent** : envoyer des commentaires sur ce qui ne vous plaît pas  

- **Envoyer une suggestion** : vous amène sur UserVoice pour partager vos idées  
 
Pour plus d’informations, consultez [Commentaires produit](/sccm/core/understand/find-help#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Espace de travail Actifs et Conformité

#### <a name="view-users-for-a-device"></a>Afficher les utilisateurs d’un appareil
Dans la version 1806, le nœud **Appareils** comprend les colonnes suivantes :  

- **Utilisateurs principaux** <!--1357280-->  

- **Utilisateur actuellement connecté** <!--1358202-->  
    > [!NOTE]  
    > Pour voir l’utilisateur actuellement connecté, la [découverte des utilisateurs](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) et l’[affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity) sont nécessaires.  

Pour plus d’informations sur l’affichage d’une colonne non définie par défaut, consultez [Colonnes](#columns).

#### <a name="improvement-to-device-search-performance"></a>Amélioration des performances de la recherche d’appareils
<!-- 3614690 --> À compter de la version 1806, la recherche d’un mot clé dans un regroupement d’appareils ne prend pas en compte toutes les propriétés de l’objet. Si les éléments à rechercher ne sont pas précisés, la recherche s’effectue sur les quatre propriétés suivantes :
- Nom
- Utilisateur ou utilisateurs principaux
- Utilisateur actuellement connecté
- Nom d’utilisateur de la dernière ouverture de session

Ce comportement améliore considérablement le temps de recherche par nom, en particulier dans un environnement de grande taille. Les recherches personnalisées sur des critères spécifiques ne sont pas concernées par cette modification. 


### <a name="monitoring-workspace"></a>Espace de travail Analyse

#### <a name="copy-details-in-monitoring-views"></a>Copier les détails des vues d’analyse
<!--1357856--> À compter de la version 1806, vous devez copier les informations du volet **Détails du bien** pour les nœuds d’analyse suivants :  

- **État de distribution du contenu**  

- **État du déploiement**  

![Vue État du déploiement - Copier les détails du bien](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Étapes suivantes

[Fonctionnalités d’accessibilité](/sccm/core/understand/accessibility-features)

