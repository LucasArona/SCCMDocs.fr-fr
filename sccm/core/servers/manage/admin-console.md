---
title: Console Configuration Manager
titleSuffix: Configuration Manager
description: Découvrez comment naviguer dans la console Configuration Manager.
ms.date: 06/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3fc9e6fad0b7be3762b3d642c94c4cf17266e0b3
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285735"
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


### <a name="details-pane"></a>Volet Détails

Vous pouvez obtenir des informations supplémentaires sur les éléments en examinant le volet de détails. Le volet de détails peut présenter un ou plusieurs onglets. Les onglets varient en fonction du nœud.  

![Exemple de volet de résultats dans Configuration Manager](media/details-pane.png)   


### <a name="columns"></a>Colonnes 

Vous pouvez ajouter, supprimer, réorganiser et redimensionner des colonnes. Ces actions vous permettent d’afficher les données que vous préférez. Les colonnes disponibles varient en fonction du nœud. Pour ajouter ou supprimer une colonne à partir de votre vue, cliquez avec le bouton droit sur un en-tête de colonne existant, puis sélectionnez un élément. Réorganisez les colonnes en faisant glisser l’en-tête de colonne jusqu’à l’emplacement souhaité.  

![Ajouter une colonne dans Configuration Manager](media/add-columns.png)  

Au bas du menu contextuel de la colonne, vous pouvez trier ou regrouper selon une colonne. En outre, vous pouvez trier selon une colonne en cliquant sur son en-tête.  

![Configuration Manager, regrouper selon une colonne](media/column-group-by.png)  

## <a name="bkmk_viewconnected"></a> Afficher les consoles récemment connectées
<!--3699367-->

À compter de la version 1902, vous pouvez voir les connexions les plus récentes pour la console Configuration Manager. La vue comprend les connexions actives et les connexions récentes. Vous voyez toujours votre connexion à la console actuelle dans la liste et vous voyez uniquement les connexions à partir de la console Configuration Manager. Vous ne voyez pas les connexions au fournisseur SMS via PowerShell ou d’autres kits SDK. Le site supprime de la liste les instances qui datent de plus de 30 jours.


### <a name="prerequisites-to-view-connected-consoles"></a>Prérequis pour voir les consoles connectées

- Votre compte nécessite l’autorisation **Lire** sur l’objet **SMS_Site**. 
- IIS doit être installé sur le serveur de fournisseur SMS <!---SCCMDocs-pr issue 1326--> 
- Autorisez le fournisseur SMS à utiliser un certificat.<!--SCCMDocs-pr issue 3135--> Utilisez l’une des options suivantes :  

  - Activer [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http) (recommandé)
  - Liez manuellement un certificat basé sur une infrastructure à clé publique (PKI) dans IIS au port 443 du serveur qui héberge le rôle Fournisseur SMS  

### <a name="view-connected-consoles"></a>Voir les consoles connectées

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**.  

2. Développez **Sécurité** et sélectionnez le nœud **Connexions à la console**.  

3. Affichez les connexions récentes, avec les propriétés suivantes :  

    - Nom d'utilisateur
    - Nom de l’ordinateur
    - Code de site connecté
    - Version de la console
    - Dernière connexion : Quand l’utilisateur a *ouvert* la console pour la dernière fois

![Voir les connexions de la console Configuration Manager](media/console-connections.png) 


## <a name="bkmk_notify"></a> Notifications de la console Configuration Manager
<!--3556016, fka 1318035-->
À compter de Configuration Manager version 1902, la console vous informe des événements suivants :

- Mise à jour disponible pour Configuration Manager
- Événements de cycle de vie et de maintenance dans l’environnement

Cette notification se présente sous la forme d’une barre située dans la partie supérieure de la fenêtre de console, sous le ruban. Elle remplace l’expérience précédente associée à la disponibilité de mises à jour Configuration Manager. Ces notifications dans la console affichent toujours des informations critiques, mais n’interfèrent pas avec votre travail dans la console. Vous ne pouvez pas faire disparaître les notifications critiques. La console affiche toutes les notifications dans une nouvelle zone de notification de la barre de titre.

![Barre de notification et indicateur dans la console](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Configurer un site pour qu’il affiche des notifications non critiques

Vous pouvez configurer chaque site pour qu’il affiche des notifications non critiques sous les propriétés du site.

1.  Dans l'espace de travail **Administration**, développez **Configuration du site**, puis cliquez sur le nœud **Sites**.
1. Sélectionnez le site que vous souhaitez configurer pour les notifications non critiques.
1. Dans le ruban, cliquez sur **Propriétés**.
1. Sous l’onglet **Alertes**, sélectionnez l’option **Activer les notifications de console pour les changements d’intégrité de site non critiques**.
   - Si vous activez ce paramètre, les notifications critiques, d’avertissement et d’informations sont affichées à tous les utilisateurs de la console. Ce paramètre est activé par défaut.  
   - Si vous désactivez ce paramètre, les utilisateurs de la console voient uniquement les notifications critiques.  

La plupart des notifications de la console sont propres à la session. Quand un utilisateur lance la console, elle évalue les requêtes. Pour voir les changements dans les notifications, redémarrez la console. Si un utilisateur fait disparaître une notification non critique, celle-ci réapparaît au redémarrage de la console si elle toujours pertinente.

Les notifications suivantes sont réévaluées toutes les cinq minutes :
- Site en mode de maintenance  
- Site en mode de récupération  
- Site en mode de mise à niveau  

Les notifications suivent les autorisations de l’administration basée sur des rôles. Par exemple, si un utilisateur n’est pas autorisé à voir les mises à jour de Configuration Manager, il ne voit pas ces notifications.

Certaines notifications ont une action associée. Par exemple, si la version de la console ne correspond pas à la version du site, sélectionnez **Installer la nouvelle version de la console**. Cette action lance le programme d’installation de la console. 

Les notifications suivantes s’appliquent avant tout à la branche Technical Preview :  

- La version d’évaluation va expirer dans les 30 jours (avertissement) : la date du jour est à moins de 30 jours de la date d’expiration de la version d’évaluation  
- La version d’évaluation a expiré (critique) : la date du jour est postérieure à la date d’expiration de la version d’évaluation  
- Non-concordance des versions de console (critique) : la version de la console ne correspond pas à la version du site  
- Mise à niveau du site disponible (avertissement) : un nouveau package de mise à jour est disponible  

Pour plus d’informations et des conseils de dépannage, consultez le fichier **SmsAdminUI.log** sur l’ordinateur de la console. Par défaut, ce fichier journal se trouve dans le chemin suivant : `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.

## <a name="bkmk_doc-dashboard"></a> Tableau de bord Documentation dans la console
<!--3556019 FKA 1357546-->

À compter de la version 1902 de Configuration Manager, il y a un nœud **Documentation** dans le nouvel espace de travail **Communauté**. Ce nœud contient des informations à jour sur la documentation et les articles de support Configuration Manager. Il comprend les sections suivantes :  

### <a name="product-documentation-library"></a>Bibliothèque de documentation du produit

- **Recommandé** : liste d’articles importants compilée manuellement.
- **Tendances** : articles les plus lus au cours des 30 derniers jours.
- **Mise à jour récente** : articles révisés au cours des 30 derniers jours.

### <a name="support-articles"></a>Articles de support

- **Articles de dépannage** : procédures pas à pas d’aide à la résolution des problèmes liés aux composants et fonctionnalités de Configuration Manager.
- **Articles de support nouveaux et mis à jour** : articles nouveaux ou mis à jour au cours des deux derniers mois.


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

### <a name="search-device-views-using-mac-address"></a>Vues de recherche d’appareils avec une adresse MAC
<!--3600878-->
*(Nouveauté de la version 1902)*

Vous pouvez rechercher une adresse MAC dans une vue des appareils de la console Configuration Manager. Cette propriété est utile pour les administrateurs de déploiement de système d’exploitation lors de la résolution des problèmes de déploiements PXE. Quand vous voyez une liste d’appareils, ajoutez la colonne **Adresse MAC** à la vue. Utilisez le champ de recherche pour ajouter le critère de recherche **Adresse MAC**.

### <a name="maximize-the-browse-registry-window"></a>Agrandir la fenêtre « Parcourir le registre »
<!--3594151 includes all MMS 1902 console changes-->
*(Nouveauté de la version 1902)*
1. Accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion d’applications** et sélectionnez le nœud **Applications**. 
1. Sélectionnez une application dont le type de déploiement contient une méthode de déploiement. Par exemple, une méthode de détection Windows Installer. 
1. Dans le volet d’informations, accédez à l’onglet **Types de déploiement**. 
1. Ouvrez les propriétés d’un type de déploiement, puis accédez à l’onglet **Méthode de détection**. Sélectionnez **Ajouter une clause**. 
1. Définissez le **Type de paramètre** sur **Registre**, puis sélectionnez **Parcourir** pour ouvrir la fenêtre **Parcourir le registre**. Vous pouvez maintenant agrandir cette fenêtre.  

### <a name="go-to-the-collection-from-an-application-deployment"></a>Accéder au regroupement à partir d’un déploiement d’application

*(Nouveauté de la version 1902)*
1. Accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion d’applications** et sélectionnez le nœud **Applications**. 
1. Sélectionnez une application. Dans le volet d’informations, accédez à l’onglet **Déploiements**.
1. Sélectionnez un déploiement, puis choisissez la nouvelle option **Collection** (Regroupement) dans le ruban, sous l’onglet « Déploiement ». Cette action permet d’accéder à la vue du regroupement, qui est la cible du déploiement.
   - Cette action est également disponible lorsque vous cliquez avec le bouton droit de la souris sur le menu contextuel du déploiement dans cette vue.

### <a name="edit-a-task-sequence-by-default"></a>Modifier une séquence de tâches par défaut

*(Nouveauté de la version 1902)*

Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**. L’action **Modifier** est maintenant celle par défaut lors de l’ouverture d’une séquence de tâches. Auparavant, l’action par défaut était **Propriétés**.  

### <a name="remove-content-from-monitoring-status"></a>Supprimer le contenu de la surveillance de l’état
*(Nouveauté de la version 1902)*

1. Dans l’espace de travail **Surveillance**, développez **État de distribution**, puis sélectionnez **État du contenu**.
1. Sélectionnez un élément dans la liste, puis choisissez l’option **Afficher l’état** dans le ruban. 
1. Dans le volet d’informations du composant, cliquez avec le bouton droit sur un point de distribution, puis sélectionnez la nouvelle option **Supprimer**. Cette action supprime le contenu du point de distribution sélectionné.

### <a name="views-sort-by-integer-values"></a>Tri des vues par des valeurs entières
*(Nouveauté de la version 1902)*

Nous avons apporté des améliorations au tri des données par les différentes vues. Par exemple, dans le nœud **Déploiements** de l’espace de travail **Surveillance**, les colonnes suivantes sont désormais triées en tant que nombres et non en tant que chaînes :  

- Nombre d’erreurs
- Nombre en cours
- Nombre autre
- Nombre de réussites
- Nombre inconnu  

### <a name="move-the-warning-for-a-large-number-of-results"></a>Déplacer l’avertissement pour un grand nombre de résultats
*(Nouveauté de la version 1902)*

Lorsque vous sélectionnez un nœud dans la console qui retourne plus de 1 000 résultats, Configuration Manager affiche l’avertissement suivant :

> Configuration Manager a renvoyé un grand nombre de résultats. Vous pouvez réduire le nombre de résultats à l’aide de recherche. Vous pouvez également cliquer ici pour afficher un maximum de 100 000 résultats.
 
Il existe désormais un espace vide supplémentaire entre cet avertissement et le champ de recherche. Ce déplacement évite de sélectionner par inadvertance l’avertissement pour afficher plus de résultats. 



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

- **Utilisateur principaux** <!--1357280-->  

- **Utilisateur actuellement connecté** <!--1358202-->  
    > [!NOTE]  
    > Pour voir l’utilisateur actuellement connecté, la [découverte des utilisateurs](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_config-adud) et l’[affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity) sont nécessaires.  

Pour plus d’informations sur l’affichage d’une colonne non définie par défaut, consultez [Colonnes](#columns).

#### <a name="improvement-to-device-search-performance"></a>Amélioration des performances de la recherche d’appareils
<!-- 3614690 -->
À compter de la version 1806, la recherche d’un mot clé dans un regroupement d’appareils ne prend pas en compte toutes les propriétés de l’objet. Si les éléments à rechercher ne sont pas précisés, la recherche s’effectue sur les quatre propriétés suivantes :
- Nom
- Utilisateur ou utilisateurs principaux
- Utilisateur actuellement connecté
- Nom d’utilisateur de la dernière ouverture de session

Ce comportement améliore considérablement le temps de recherche par nom, en particulier dans un environnement de grande taille. Les recherches personnalisées sur des critères spécifiques ne sont pas concernées par cette modification. 


### <a name="monitoring-workspace"></a>Espace de travail Analyse

#### <a name="copy-details-in-monitoring-views"></a>Copier les détails des vues d’analyse
<!--1357856-->
À compter de la version 1806, vous devez copier les informations du volet **Détails du bien** pour les nœuds de supervision suivants :  

- **État de distribution du contenu**  

- **État du déploiement**  

![Vue État du déploiement - Copier les détails du bien](media/1810-deployment-status.PNG)



## <a name="next-steps"></a>Étapes suivantes

[Fonctionnalités d’accessibilité](/sccm/core/understand/accessibility-features)

