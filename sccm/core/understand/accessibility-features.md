---
title: Accessibilité
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités qui rendent System Center Configuration Manager accessible aux personnes en situation de handicap.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fc0e7b81b4b46502e4477f098bdc129b0491be69
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340605"
---
# <a name="accessibility-features-in-system-center-configuration-manager"></a>Fonctionnalités d’accessibilité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


System Center Configuration Manager inclut des fonctionnalités d’accessibilité pour les personnes en situation de handicap.


## <a name="bkmk_aconsole"></a> Fonctionnalités d’accessibilité pour la console Configuration Manager  

**Raccourcis et améliorations apportées avec la version 1706**

|Raccourci clavier|  Fonction|
|--------|--------|  
|Ctrl + M|Définit le focus sur le volet principal (central).|
|Ctrl + T|Définit le focus sur le nœud supérieur dans le volet de navigation. Si le focus était déjà dans ce volet, le focus est défini sur le dernier nœud que vous avez visité.|
|Ctrl + I|Définit le focus sur la barre de navigation, sous le ruban.|
|Ctrl + L|Définit le focus sur le champ **Recherche**, quand il est disponible.|
|Ctrl + D|Définit le focus sur le volet de détails, quand il est disponible.|
|Alt     |Fait basculer le focus vers et hors du ruban.|


- Amélioration de la navigation dans le volet de navigation lorsque vous saisissez les lettres d’un nom de nœud.
- La navigation au clavier via la vue principale et le ruban est désormais circulaire.
- La navigation au clavier dans le volet d’informations est désormais circulaire. Pour revenir à l’objet ou au volet précédent, utilisez Ctrl + D, puis MAJ + TAB.
- Après l’actualisation d’une vue de l’espace de travail, le focus est défini sur le volet principal de cet espace de travail.
- Correction d’un problème pour activer les lecteurs d’écran pour annoncer les noms des éléments de liste.
- Ajout des noms accessibles de plusieurs contrôles sur la page qui active les lecteurs d’écran pour annoncer des informations importantes.


**Les raccourcis suivants sont disponibles pour toutes les versions**

- Pour accéder à un espace de travail, utilisez les raccourcis clavier suivants :  

|Raccourci clavier| Espace de travail|
|--------|--------|  
|Ctrl + 1| Biens et conformité|
|Ctrl + 2|  Bibliothèque de logiciels|
|Ctrl + 3|  Analyse|
|Ctrl + 4|  Administration|


-   Pour accéder au menu d’un espace de travail, sélectionnez la touche Tab jusqu’à ce que l’icône de réduction/développement soit active. Sélectionnez ensuite la flèche Bas pour accéder au menu de l’espace de travail.  

-   Pour naviguer dans le menu d'un espace de travail, utilisez les touches de direction.  

-   Pour accéder aux différentes zones de l'espace de travail, utilisez la touche Tab et les touches Maj+Tab. Pour naviguer dans une zone de l'espace de travail telle que le ruban, utilisez les touches de direction.  

-   Pour accéder à la barre d’adresses quand le focus se trouve dans le nœud de l’arborescence, utilisez Maj+Tab à trois reprises.  

-   Sur une page d'Assistant ou une page de propriétés, vous pouvez vous déplacer entre les zones à l'aide de raccourcis clavier. Sélectionnez la touche Alt et le caractère souligné (Alt+_) pour sélectionner une zone spécifique.     

-  Pour parcourir les différents nœuds d’un espace de travail, entrez la première lettre du nom d’un nœud. Chaque appui sur une touche déplace le curseur au nœud suivant qui commence par cette lettre. Si vous utilisez un lecteur d’écran, le lecteur lit le nom de ce nœud.

> [!NOTE]  
>  Les informations présentes dans cette section ne s’appliquent qu’aux utilisateurs détenteurs de licences de produits Microsoft aux États-Unis. Si vous avez obtenu ce produit en dehors des États-Unis, vous pouvez utiliser la carte d’information de filiale fournie avec le package logiciel ou consulter le [site web Accessibilité de Microsoft](http://go.microsoft.com/fwlink/?LinkId=8431) pour obtenir les coordonnées des services de support technique Microsoft. Vous pouvez contacter votre filiale pour savoir si les types de produits ou de services décrits dans cette section sont disponibles dans votre région. Les informations sur l'accessibilité sont disponibles dans d'autres langues, notamment en japonais et en français.  

##  <a name="bkmk_ahelp"></a> Fonctionnalités d’accessibilité dans l’aide de Configuration Manager  
 L’aide de Configuration Manager intègre des fonctionnalités qui la rendent accessible à un plus grand nombre d’utilisateurs, notamment ceux présentant une mobilité réduite, une acuité visuelle réduite ou d’autres handicaps.  

|Tâche|Utiliser ce raccourci clavier|  
|----------------|--------------------------------|  
|Afficher la fenêtre d'aide.|F1|  
|Basculer le curseur entre les volets Rubrique d'aide et Navigation (onglets **Sommaire**, **Rechercher**et **Index** ).|F6|  
|Changer d’onglet (par exemple, **Contenu**, **Rechercher** et **Index**) dans le volet de navigation.|ALT+lettre soulignée de l'onglet|  
|Sélectionner le texte masqué ou le lien hypertexte suivant.|Onglet|  
|Sélectionner le texte masqué ou le lien hypertexte précédent.|Maj+Tabulation|  
|Effectuer l'action pour l'élément sélectionné (option Afficher tout, Masquer tout, texte masqué ou lien hypertexte).|Touche Entrée|  
|Afficher le menu **Options** pour accéder à n'importe quelle commande de la barre d'outils de l'aide.|Alt+O|  
|Masquer ou afficher le volet contenant les onglets **Contenu**, **Rechercher** et **Index**.|Alt+O, puis sélectionner T|  
|Afficher la rubrique précédemment consultée.|Alt+O, puis sélectionner B|  
|Afficher la rubrique suivante dans une séquence de rubriques précédemment affichées.|Alt+O, puis sélectionner F|  
|Revenir à la page d'accueil spécifiée.|Alt+O, puis sélectionner H|  
|Arrêter l’ouverture d’une rubrique dans la fenêtre d’aide, par exemple pour arrêter le téléchargement d’une page web.|Alt+O, puis sélectionner S|  
|Ouvrir la boîte de dialogue **Options Internet** pour Windows Internet Explorer, dans laquelle vous pouvez modifier les paramètres d'accessibilité.|Alt+O, puis sélectionner I|  
|Actualiser la rubrique, par exemple une page Web accessible via un lien.|Alt+O, puis sélectionner R|  
|Imprimer toutes les rubriques d'un livre ou seulement une rubrique sélectionnée.|Alt+O, puis sélectionner P|  
|Fermer la fenêtre d'aide.|Alt+F4|  

#### <a name="to-change-the-appearance-of-a-help-topic"></a>Pour modifier l'apparence d'une rubrique d'aide  

1.  Pour vous préparer à personnaliser les couleurs, les styles et les tailles de police utilisés dans l'Aide, ouvrez la fenêtre de l'Aide.  

2.  Choisissez **Options**, puis **Options Internet**.  

3.  Sous l’onglet **Général**, choisissez **Accessibilité**. Choisissez **Ignorer les couleurs spécifiées sur les pages Web**, **Ignorer les styles de police spécifiés sur les pages Web** et **Ignorer les tailles de police spécifiées sur les pages Web**. Vous pouvez également choisir d'utiliser les paramètres qui sont spécifiés dans votre propre feuille de style.  

#### <a name="to-change-the-color-of-the-background-or-text-in-help"></a>Pour modifier la couleur de l'arrière-plan ou du texte dans l'aide  

1.  Ouvrez la fenêtre d'aide.  

2.  Choisissez **Options**, puis **Options Internet**.  

3.  Sous l’onglet **Général**, choisissez **Accessibilité**. Choisissez ensuite **Ignorer les couleurs spécifiées sur les pages Web**. Vous pouvez également choisir d'utiliser les paramètres qui sont spécifiés dans votre propre feuille de style.  

4.  Pour personnaliser les couleurs utilisées dans l’aide, choisissez **Couleurs** sous l’onglet **Général**. Décochez la case **Utiliser les couleurs Windows**, puis choisissez les couleurs de police et d’arrière-plan que vous souhaitez utiliser.  

    > [!NOTE]  
    >  Si vous modifiez la couleur d'arrière-plan des rubriques d'aide dans la fenêtre de l'Aide, la modification affecte également la couleur d'arrière-plan des pages Web dans Windows Internet Explorer.  

#### <a name="to-change-the-font-in-help"></a>Pour modifier la police dans l'aide  

1.  Ouvrez la fenêtre d'aide.  

2.  Choisissez **Options**, puis **Options Internet**.  

3.  Sous l’onglet **Général**, choisissez **Accessibilité**. Pour utiliser les mêmes paramètres que ceux utilisés dans votre instance d’Internet Explorer, choisissez **Ignorer les styles de police spécifiés sur les pages Web** et **Ignorer les tailles de police spécifiées sur les pages Web**. Vous pouvez également choisir d'utiliser les paramètres qui sont spécifiés dans votre propre feuille de style.  

4.  Pour personnaliser le style de police utilisé dans l’Aide, sous l’onglet **Général**, choisissez **Polices**, puis sur le style de police souhaité.  

    > [!NOTE]  
    >  Si vous modifiez la police des rubriques d'aide dans la fenêtre de l'Aide, la modification affecte également la police des pages Web dans Windows Internet Explorer.  
