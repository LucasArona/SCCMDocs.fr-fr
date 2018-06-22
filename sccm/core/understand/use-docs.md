---
title: Guide pratique pour utiliser la documentation
titleSuffix: Configuration Manager
description: Recevez des conseils sur l’utilisation de la bibliothèque de documentation technique de Configuration Manager.
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 46bff7e26a5df326b686b07c37f1d58352755857
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32345089"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Guide pratique pour utiliser la documentation de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit les sections suivantes, ainsi que plusieurs ressources et conseils sur l’utilisation de la bibliothèque de documentation de Configuration Manager :  

- [Comment effectuer une recherche](#bkmk_searchtips)  

- [Soumission de bogues, d’améliorations, de questions et de nouvelles idées concernant la documentation](#bkmk_docfeedback)  

- [Comment être notifié des changements apportés](#bkmk_notifications)  

- [Comment contribuer à la documentation](#bkmk_contribute)  


Pour obtenir une aide générale sur le produit, consultez [Trouver de l’aide](/sccm/core/understand/find-help).


##  <a name="bkmk_searchtips"></a> Rechercher   
 Utilisez les conseils de recherche suivants pour vous aider à trouver les informations dont vous avez besoin :  

-   Quand vous utilisez votre moteur de recherche favori pour rechercher du contenu relatif à Configuration Manager, ajoutez `SCCM` à vos mots clés de recherche.  

    - Recherchez les résultats provenant de docs.microsoft.com pour l’édition Current Branch de Configuration Manager. Les résultats provenant de technet.microsoft.com ou msdn.microsoft.com concernent des versions de produits plus anciennes.  

    - Pour concentrer davantage les résultats de la recherche sur la bibliothèque de contenu actuelle, ajoutez `site:docs.microsoft.com` afin de définir l’étendue à couvrir par le moteur de recherche.  

-   Utilisez des termes de recherche correspondant à la terminologie qui se trouve dans l’interface utilisateur et la documentation en ligne. Évitez les termes ou les abréviations non officiels que vous pouvez voir dans le contenu de la communauté. Par exemple, rechercher « point de gestion » plutôt que « MP », « type de déploiement » plutôt que « DT » et « mises à jour logicielles » plutôt que « SUM ».  

-   Pour effectuer une recherche dans un article que vous consultez, utilisez la fonctionnalité **Rechercher** de votre navigateur. Dans la plupart des navigateurs web actuels, appuyez sur **Ctrl**+**F**, puis entrez vos termes de recherche.  

-   Chaque article sur docs.microsoft.com contient les champs suivants qui vous permettent d’effectuer des recherches dans le contenu :  

    - **Rechercher** en haut à droite. Pour effectuer une recherche dans tous les articles, entrez des termes dans ce champ. Les articles de la bibliothèque de Configuration Manager incluent automatiquement l’étendue « ConfigMgr ».  

    - **Filtrer par titre** au-dessus de la table des matières de gauche. Pour effectuer une recherche dans la table des matières, entrez des termes dans ce champ. Ce champ permet de rechercher uniquement les termes qui apparaissent dans les titres d’articles du nœud actuel. Par exemple, Infrastructure de base ou Gestion des applications.  

- Vous n’arrivez pas à trouver quelque chose ? [Soumettez des commentaires !](#bkmk_docfeedback) Quand vous soumettez un problème, indiquez le moteur de recherche utilisé, les mots clés essayés et l’article cible. Ces commentaires aident Microsoft à optimiser le contenu pour une meilleure recherche.  



## <a name="bkmk_docfeedback"></a> Commentaires

Accédez à la section Commentaires au bas de la page en cliquant sur le lien **Commentaires** en haut à droite d’un article. Cette section est intégrée aux problèmes GitHub. Pour plus d’informations sur l’intégration aux problèmes GitHub, consultez le [billet de blog consacré à la plateforme de documentation](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Pour partager vos commentaires sur le produit Configuration Manager, cliquez sur **Give product feedback** (Fournir des commentaires sur le produit). Pour plus d’informations, consultez [Commentaires produit](/sccm/core/understand/find-help#product-feedback). 

Si vous souhaitez fournir des commentaires sur la documentation, la possession d’un [compte GitHub](https://github.com/join) est un prérequis. Une fois que vous vous êtes connecté, vous disposez d’une autorisation à usage unique pour l’accès à MicrosoftDocs. Cliquez ensuite sur **Give documentation feedback** (Fournir des commentaires sur la documentation), entrez un titre et un commentaire, puis cliquez sur **Submit feedback** (Envoyer des commentaires). Cette action permet de soumettre un nouveau problème relatif à l’article cible dans le [dépôt SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Cette intégration permet également d’afficher tous les problèmes ouverts ou fermés pour l’article cible. S’il en existe, passez-les en revue avant de soumettre un nouveau problème. Si vous trouvez un problème connexe, cliquez sur l’émoticône pour ajouter une réaction, ou développez l’entrée correspondante pour ajouter un commentaire. 

#### <a name="types-of-feedback"></a>Types de commentaire
Utilisez la fonctionnalité Problèmes GitHub pour soumettre les types de commentaire suivants :
- Bogue de la documentation : le contenu est obsolète, vague, confus ou fragmenté.
- Amélioration de la documentation : suggestion d’amélioration de l’article.
- Question sur la documentation : vous avez besoin d’aide pour trouver de la documentation existante.
- Idée de documentation : suggestion d’un nouvel article. Utilisez cette méthode à la place de UserVoice pour les commentaires relatifs à la documentation.
- Félicitations : commentaires positifs sur un article utile ou instructif !
- Localisation : commentaires sur la traduction du contenu.
- SEO (optimisation du référencement d’un site auprès d’un moteur de recherche) : commentaires sur les problèmes de recherche de contenu. Incluez le moteur de recherche, les mots clés et l’article cible dans les commentaires.

Si des problèmes sont soumis pour des rubriques non liées à la documentation, par exemple des [commentaires sur le produit](/sccm/core/understand/find-help#product-feedback), des [questions sur le produit](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB) ou des [demandes de support](https://aka.ms/cmcbsupport), ces problèmes sont fermés et les utilisateurs redirigés vers le canal de commentaires approprié.

Pour partager vos commentaires sur la plateforme docs.microsoft.com, accédez aux [commentaires sur la documentation](https://aka.ms/sitefeedback). La plateforme inclut tous les composants de wrapper tels que l’en-tête, la table des matières et le menu de droite. Elle inclut également le rendu des articles dans le navigateur, par exemple la police, les zones d’alerte et les ancres de page.



## <a name="bkmk_notifications"></a> Notifications

Pour recevoir des notifications en cas de changement du contenu dans la bibliothèque de documentation, suivez les étapes ci-dessous :

1. Utilisez la [recherche de documentation](https://docs.microsoft.com/search/index?scope=ConfigMgr) pour trouver un article ou un ensemble d’articles. Par exemple :
    - Recherchez un article unique par son titre : [« Fichiers journaux pour la résolution des problèmes - Configuration Manager »](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr).
    - Recherchez un article relatif à [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr).
2. Dans le coin supérieur droit, cliquez sur le lien **RSS**. 
3. Utilisez ce flux dans une application RSS pour recevoir des notifications en cas de changement de l’un des résultats de la recherche.


> [!Tip]  
> Vous pouvez également **suivre** le [dépôt SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) sur GitHub. Cette méthode génère un grand nombre de notifications. De plus, elle n’inclut pas les changements apportés à un dépôt privé utilisé par Microsoft.  



## <a name="bkmk_contribute"></a> Contribuer

La bibliothèque de documentation de Configuration Manager, comme la plupart des contenus de docs.microsoft.com, est open source sur GitHub. Cette bibliothèque accepte et encourage les contributions de la communauté. Pour plus d’informations sur la procédure à suivre, consultez le [Guide du contributeur](https://docs.microsoft.com/contribute). La création d’un compte [GitHub](https://github.com/join) est le seul prérequis.

#### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Étapes de base pour contribuer à SCCMdocs
1. Dans l’article cible, cliquez sur **Modifier**. Cette action permet d’ouvrir le fichier source dans GitHub.
2. Pour modifier le fichier source, cliquez sur l’icône de crayon.
3. Apportez vos changements à la source Markdown. Pour plus d’informations, consultez [Guide pratique pour utiliser Markdown et rédiger de la documentation](https://docs.microsoft.com/contribute/how-to-write-use-markdown). 
4. Dans la section Propose file change (Proposer le changement d’un fichier), entrez un commentaire de validation publique décrivant *ce que* vous avez changé. Cliquez ensuite sur **Propose file change** (Proposer le changement d’un fichier).
5. Faites défiler vers le bas et vérifiez les changements apportés. Cliquez sur **Create pull request** (Créer une demande de tirage (pull request)) pour ouvrir le formulaire. Indiquez *pourquoi* vous avez effectué ce changement. Identifiez l’auteur de l’article, et demandez-lui de le réviser. Cliquez sur **Create pull request** (Créer une demande de tirage).

### <a name="what-to-contribute"></a>Type de contribution
Si vous souhaitez apporter votre contribution mais que vous ne savez pas par où commencer, consultez les suggestions suivantes :
- Vérifiez l’exactitude d’un article. Mettez ensuite à jour les métadonnées **ms.date** au format `mm/dd/yyyy`. Ce type de contribution permet d’actualiser le contenu.
- Ajoutez des éclaircissements, des exemples ou des conseils d’aide en fonction de votre expérience utilisateur. Ce type de contribution tire parti de la puissance de la communauté pour permettre le partage des connaissances.  
- Corrigez les traductions effectuées à partir de l’anglais. Ce type de contribution améliore la facilité d’utilisation du contenu localisé.
- Recherchez dans la liste des problèmes les étiquettes destinées à la communauté, par exemple [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue) (problème prioritaire) et [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted) (aide souhaitée). Les auteurs Microsoft affectent ces étiquettes aux problèmes qui sont de bons candidats pour une contribution à la communauté.