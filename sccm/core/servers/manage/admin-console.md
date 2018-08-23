---
title: Console Configuration Manager
titleSuffix: Configuration Manager
description: Découvrez comment naviguer dans la console Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d783211396f3cdc9f14798ed7dc97e921e45554
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385910"
---
# <a name="using-the-system-center-configuration-manager-console"></a>Utilisation de la console System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les utilisateurs administratifs se servent de la console System Center Configuration Manager pour gérer l’environnement Configuration Manager. Cet article aborde les principes fondamentaux de la navigation dans la console. Les améliorations apportées à la console sont répertoriées par version au bas de cet article. 

## <a name="connect-the-console-to-a-site-server"></a>Connecter la console à un serveur de site
La console se connecte à votre serveur de site d’administration centrale ou à vos serveurs de site principal. Toutefois, vous ne pouvez pas connecter une console Configuration Manager à un site secondaire. Si nécessaire, [installez la console Configuration Manager](../deploy/install/install-consoles.md). Pendant l’installation, vous avez spécifié le nom de domaine complet du serveur de site auquel la console Configuration Manager se connecte. Pour vous connecter à un serveur de site différent, utilisez les instructions suivantes : 

1. Cliquez sur la flèche en haut du ruban, puis sélectionnez **Connecter à un nouveau site**.
    ![Connecter la console à un nouveau site](media/connect-to-a-new-site.png)
2. Tapez le nom de domaine complet du serveur de site. Si vous vous êtes précédemment connecté au serveur de site, sélectionnez le serveur dans la liste déroulante.  
    ![Taper le nom de domaine complet du serveur de site](media/site-server-fqdn.png)
3. Cliquez sur **Connexion**. 

## <a name="navigate-the-console"></a>Naviguer dans la console
Certaines options sous la console peuvent ne pas être visibles en fonction du rôle de sécurité qui vous est attribué. Pour plus d’informations sur les rôles, consultez [Principes de base de l’administration basée sur des rôles](../../understand/fundamentals-of-role-based-administration.md). 

### <a name="workspaces"></a>Espaces de travail
La console Configuration Manager possède quatre **espaces de travail** : 
   - **Ressources et Conformité**
   - **Bibliothèque de logiciels**
   - **Monitoring**
   - **Administration**

 ![Espaces de travail de Configuration Manager](media/configuration-manager-workspaces.png)

Réorganisez les boutons des espaces de travail en cliquant sur la flèche vers le bas et en sélectionnant **Options du volet de navigation**. Sélectionnez un élément à **déplacer vers le haut** ou **déplacer vers le bas**. Cliquez sur **Réinitialiser** pour restaurer l’ordre des boutons par défaut. 

 ![Réorganiser les espaces de travail de Configuration Manager](media/navigation-pane-options.png)

Vous pouvez réduire le bouton d’un espace de travail en sélectionnant **Afficher moins de boutons**. Le dernier espace de travail de la liste est réduit en premier. Si vous cliquez sur un bouton réduit et sélectionnez **Afficher plus de boutons**, la taille d’origine du bouton est rétablie.  

![Espaces de travail de Configuration Manager](media/workspace-buttons.png)


### <a name="nodes"></a>Nœuds
Les espaces de travail sont un regroupement de **nœuds**. Un exemple de nœud est le nœud **Groupes de mises à jour logicielles**. Une fois que vous êtes dans le nœud, vous pouvez cliquer sur la flèche pour réduire le volet de navigation. 

![Espaces de travail de Configuration Manager](media/software-update-groups-node.png)

Vous pouvez utiliser la **barre de navigation** pour vous déplacer dans la console quand votre volet de navigation est réduit. 

![Volet de navigation réduit de Configuration Manager](media/minimized-navigation-pane.png)

Dans la console, les nœuds sont parfois organisés en dossiers. Si vous cliquez directement sur le dossier, vous accédez généralement à un **index de navigation** ou un **tableau de bord**.

![Index de navigation des mises à jour logicielles de Configuration Manager](media/software-updates-navigation-index.png)

### <a name="ribbon"></a>Ruban 
Le ruban se situe en haut de la console Configuration Manager. Le ruban peut avoir plusieurs onglets et peut être réduit à l’aide de la flèche sur la droite. Les boutons du ruban changent en fonction du nœud. La plupart des boutons du ruban sont également disponibles dans les menus contextuels. 
 
![Index de navigation des mises à jour logicielles de Configuration Manager](media/ribbon.png)

### <a name="details-pane"></a>Volet de détails
Vous pouvez obtenir des informations supplémentaires sur les éléments en examinant le volet de détails. Le volet de détails peut présenter un ou plusieurs onglets. Les onglets varient en fonction du nœud. 
![Volet de détails de Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Colonnes 
Vous pouvez ajouter, supprimer, réorganiser et redimensionner des colonnes. Ces actions vous permettent d’afficher les données que vous préférez. Les colonnes disponibles varient en fonction du nœud. Cliquez avec le bouton droit sur un en-tête de colonne, puis cliquez sur un élément à ajouter ou supprimer dans votre affichage. Réorganisez les colonnes en faisant glisser l’en-tête de colonne jusqu’à l’emplacement souhaité. 
![Configuration Manager, ajouter une colonne](media/add-columns.png)

Au bas du menu contextuel de la colonne, vous pouvez trier ou regrouper selon une colonne. En outre, vous pouvez trier selon une colonne en cliquant sur son en-tête. 

![Configuration Manager, regrouper selon une colonne](media/column-group-by.png)

## <a name="console-improvements-in-version-1806"></a>Améliorations apportées à la console dans la version 1806
Dans Configuration Manager version 1806, les améliorations suivantes ont été apportées à la console :

- **Utilisateurs principaux** est disponible comme colonne dans le nœud Appareils. <!--1357280-->
- **Utilisateur actuellement connecté** est disponible comme colonne dans le nœud Appareils.<!--1358202-->
- Copiez les informations à partir du volet **Détails du bien** pour les affichages de surveillance suivants : <!--1357856-->
    - État de distribution du contenu
    - État du déploiement 

    ![Configuration Manager, copier les détails du bien](media/1810-deployment-status.PNG)

 - Envoyez des commentaires à partir de la console. Vous pouvez enregistrer une copie à envoyer ultérieurement si vous n’avez pas accès à Internet. <!--1357542-->
   
    - **Envoyer un sourire** : envoyez des commentaires sur ce qui vous plaît.
    - **Envoyer un smiley mécontent** : envoyez des commentaires sur ce qui ne vous plaît pas. 
    - **Envoyer une suggestion** : vous amène sur UserVoice pour partager vos idées. 
 
       ![Envoyer des commentaires pour Configuration Manager](media/1810-send-a-smile.PNG)
![Formulaire de commentaires Configuration Manager](media/1810-feedback-form.PNG)

## <a name="next-steps"></a>Étapes suivantes
> [!div class="nextstepaction"]
> [Fonctionnalités d’accessibilité](/sccm/core/understand/accessibility-features.md)

