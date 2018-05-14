---
title:
- TITRE DE L’ARTICLE en 35 caractères ou moins
titleSuffix: Configuration Manager
description: ''
ms.date: mm/dd/yyyy
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid:
- GET ONE FROM guidgenerator.com
author:
- GITHUB USERNAME
ms.author:
- ALIAS
manager:
- ALIAS
ms.openlocfilehash: bb0a23b8870d31136967b1bc594580bcc2cd0cd9
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="metadata-and-markdown-template"></a>Métadonnées et modèle Markdown

Ce modèle docs.ms contient des exemples de syntaxe Markdown, ainsi que de l’aide pour définir les métadonnées. Il se trouve dans le répertoire racine de chaque référentiel EM Pilot (par exemple, ~/Azure-RMSDocs-pr/template.md). Il est destiné à être lu comme un fichier Markdown, bien que vous puissiez vous référer à [la version publiée](https://stage.docs.microsoft.com/en-us/rights-management/template) pour voir le rendu des exemples de fichiers Markdown.

Lorsque vous créez un fichier Markdown, il est recommandé de copier le modèle dans un nouveau fichier, de remplir les métadonnées de la manière indiquée ci-dessous, de définir le titre H1 ci-dessus sur le titre de l’article et de supprimer le contenu.


## <a name="metadata"></a>Métadonnées

Le bloc de métadonnées complet, situé au-dessus, est divisé entre les champs obligatoires et les champs facultatifs ; consultez la [Fiche récapitulative des métadonnées OPS](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data) pour plus d’informations. Remarques importantes :

- Vous **devez** mettre un espace entre le signe deux-points (:) et la valeur d’une métadonnée.
- Si une métadonnée facultative n’a pas de valeur, mettez l’élément en commentaire avec le signe # (ne le laissez pas vide et n’utilisez pas « na ») ; si vous ajoutez une valeur à un élément mis en commentaire, veillez à supprimer le signe #.
- Les signes deux-points présents dans une valeur (par exemple, un titre) arrêtent l’analyseur de métadonnées. Utilisez plutôt l’encodage HTML &#58; (par exemple, « title: Azure Rights Management &#58; les principes de base | Azure RMS »).
- **title** : ce titre s’affiche dans les résultats des moteurs de recherche. Il doit se terminer par une barre verticale (|) suivie du nom du service (voir ci-dessus à titre d’exemple). Il n’est pas nécessairement (et n’est généralement pas) identique au titre H1. Il doit comporter environ 65 caractères (y compris | NOM DU SERVICE)
- **author**, **manager**, **reviewer** : le champ author doit contenir le **nom d’utilisateur GitHub** de l’auteur, et non son alias.  En revanche, les champs « manager » et « reviewer » doivent contenir les alias. ms.reviewer spécifie le nom du chef de projet associé à l’article ou au service.
- **ms.assetid** : il s’agit du GUID de l’article en majuscules. Lorsque vous créez un fichier Markdown, récupérez un GUID sur [https://www.guidgenerator.com](https://www.guidgenerator.com).
- **ms.prod**, **ms.service**, **ms.technology**, **ms.devlang**, **ms.topic**, **ms.tgt_pltfrm** : les valeurs possibles de ces éléments se trouvent [ici](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default).

## <a name="basic-markdown-and-gfm"></a>Syntaxe GFM et Markdown de base

Toute la syntaxe Markdown de base et GFM (« GitHub-flavored », de type GitHub) est prise en charge. Pour plus d’informations, consultez les articles :

- [Syntaxe Markdown de référence](https://daringfireball.net/projects/markdown/syntax)
- [Documentation GFM (GitHub-flavored Markdown)](https://guides.github.com/features/mastering-markdown)

## <a name="headings"></a>Titres

Voici quelques exemples de titres de premier et de deuxième niveau.

Il ne **doit** y avoir qu’un seul titre de premier niveau dans une rubrique ; ce sera le titre de la page.  

Les titres de deuxième niveau génèrent la table des matières de la page, qui s’affiche dans la section « Dans cet article » sous le titre de la page.

### <a name="third-level-heading"></a>Titre de troisième niveau
#### <a name="fourth-level-heading"></a>Titre de quatrième niveau
##### <a name="fifth-level-heading"></a>Titre de cinquième niveau
###### <a name="sixth-level-heading"></a>Titre de sixième niveau

## <a name="text-styling"></a>Style du texte

*Italique*

**Gras**

~~Barré~~



## <a name="links"></a>Liens

Pour créer un lien vers un fichier Markdown dans le même référentiel, utilisez les [liens relatifs](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2).

- Exemple : [En quoi consiste Azure Rights Management ?](./understand-explore/what-is-azure-rights-management.md)

Pour créer un lien vers un en-tête dans le même fichier Markdown, affichez la source de l’article publié, recherchez l’ID de l’en-tête (par exemple, `id="blockquote"`) et créez le lien en utilisant # + ID (par exemple, `#blockquote`).

- Exemple : [Citations](#blockquote)

Pour créer un lien vers un en-tête d’un fichier Markdown dans le même référentiel, utilisez les liens relatifs et les liens avec mot-dièse.

- Exemple : [Présentation technique du processus d’inscription](./understand-explore/rms-for-individuals-user-signup.md#technical-overview-of-the-sign-up-process)

Pour créer un lien vers un fichier externe, utilisez l’URL complète comme lien.

- Exemple : [GitHub](http://www.github.com)

Si une URL apparaît dans un fichier Markdown, elle est transformée en lien interactif.

- Exemple : http://www.github.com

## <a name="lists"></a>Listes

### <a name="ordered-lists"></a>Listes triées

1. Ceci
1. est
1. une
1. liste
1. ordonnée  


#### <a name="ordered-list-with-an-embedded-list"></a>Liste triée avec liste intégrée

1. Ceci
1. est
1. une
1. liste
    1. Mademoiselle Rose
    1. Professeur Violet
1. ordonnée
1. intégrée


### <a name="unordered-lists"></a>Listes non triées

- Cette
- est
- une
- liste
- à puces


##### <a name="unordered-list-with-an-embedded-lists"></a>Liste non triée avec listes intégrées

- Cette
- liste
- à puces
    - Madame Pervenche
    - Révérend Olive
- contient  
- d’autres
    1. Colonel Moutarde
    1. Madame Leblanc
- listes


## <a name="horizontal-rule"></a>Règle horizontale

---

## <a name="tables"></a>Tableaux

| Les tableaux        | Sont           | Cool  |
| ------------- |:-------------:| -----:|
| La 3e colonne est      | alignée à droite | 1 600 $ |
| La 2e colonne est      | centrée      |   12 $ |
| La 1re colonne est (par défaut) | alignée à gauche     |    1 $ |


## <a name="code"></a>Code

### <a name="codeblock"></a>Bloc de code

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### <a name="in-line-code"></a>Code en ligne

Voici un exemple de `in-line code`.

## <a name="blockquotes"></a>Citations

> La sécheresse durait maintenant depuis dix millions d’années et le règne des terribles lézards avait depuis longtemps pris fin. Ici, à l’Équateur, sur le continent que l’on appellerait un jour l’Afrique, la lutte pour l’existence avait atteint un nouveau sommet dans la férocité, et le vainqueur n’était pas encore connu. Dans ce territoire aride et désolé, seul le plus petit, le plus rapide ou le plus puissant pouvait croître et espérer survivre.

## <a name="images"></a>Images

### <a name="static-image"></a>Image statique

![voici le texte de remplacement](./media/AzRMS_elements.png)

### <a name="linked-image"></a>Image liée

[![texte de remplacement de l’image liée](./media/AzRMS_elements.png)](https://azure.microsoft.com)

### <a name="animated-gif"></a>Image GIF animée

![image GIF animée](./media/hololens.gif)

## <a name="alerts"></a>Alertes

### <a name="note"></a>Remarque

> [!NOTE]
> Voici une REMARQUE

### <a name="warning"></a>Avertissement

> [!WARNING]
> Voici un AVERTISSEMENT

### <a name="tip"></a>Conseil

> [!TIP]
> Voici un CONSEIL

### <a name="important"></a>Important

> [!IMPORTANT]
> Ceci est IMPORTANT

## <a name="videos"></a>Vidéos

### <a name="channel-9"></a>Channel 9

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### <a name="youtube"></a>YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## <a name="docsms-extentions"></a>Extensions docs.ms

### <a name="button"></a>Bouton

> [!div class="button"]
[liens boutons](/rights-management)

### <a name="selector"></a>Sélectionneur

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [bar](/rights-management/scratch.md)

### <a name="step-by-step"></a>Guide pas à pas

>[!div class="step-by-step"]
[Précédent](https://www.example.com)
[Suivant](https://www.example.com)
