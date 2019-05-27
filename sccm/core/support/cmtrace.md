---
title: CMTrace
titleSuffix: Configuration Manager
description: Découvrez comment utiliser l’outil CMTrace pour afficher les fichiers journaux pour Configuration Manager.
ms.date: 05/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a4a3290-5228-4871-918a-554aa1c20834
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 988e834de78bac64be43600ca73d0d51ff29bf4b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496772"
---
# <a name="cmtrace"></a>CMTrace

*S’applique à : System Center Configuration Manager (Current Branch)*

CMTrace fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Il vous permet d’afficher et de surveiller les fichiers journaux, notamment les types suivants :  

- Fichiers journaux au format Configuration Manager ou CCM (Client Component Manager)  

- Fichiers au format texte ASCII ou Unicode, tels que les journaux de Windows Installer  

L’outil aide à analyser les fichiers journaux par la mise en surbrillance, le filtrage et la recherche d’erreurs.

Depuis la version 1806, l’outil d’affichage des journaux CMTrace est automatiquement installé avec le client Configuration Manager. Il est ajouté au répertoire d’installation du client, qui est par défaut `%WinDir%\CCM\CMTrace.exe`.<!--1357971-->

> [!Note]  
> CMTrace n’est pas automatiquement inscrit auprès de Windows pour ouvrir l’extension de fichier .log. Pour plus d’informations, consultez [Associations de fichiers](#file-associations).  



## <a name="usage"></a>Utilisation

Exécutez **CMTrace.exe**. La première fois que vous exécutez l’outil, vous voyez une invite pour une association de fichiers. Pour plus d’informations, consultez [Associations de fichiers](#file-associations).

Vous effectuez la plupart des actions dans CMTrace à partir des menus suivants :
- [File](#file-menu)
- [Tools](#tools-menu)


### <a name="file-menu"></a>Menu Fichier

Les actions suivantes sont disponibles dans le menu **File** :  
- [Open](#open)
- [Open on Server](#open-on-server)
- [Print](#print)
- [Preferences](#preferences)

Le menu File liste également les huit fichiers les plus récents. Rouvrez rapidement l’un de ces journaux en le sélectionnant dans le menu File. 

#### <a name="open"></a>Ouvrir
Affiche la boîte de dialogue Open pour rechercher un fichier journal. 

Filtrez l’affichage pour les fichiers des types suivants : 
- Fichiers journaux (\*.log)  
- Anciens fichiers journaux (\*.lo_) 
- Tous les fichiers (\*.\*)

Les deux options suivantes ne sont pas sélectionnées par défaut :  

- **Ignore existing lines** : lorsque cette option est sélectionnée, CMTrace ignore le contenu existant du fichier journal sélectionné et n’affiche les nouvelles lignes qu’au moment où elles sont ajoutées. Utilisez cette option pour superviser uniquement les nouvelles actions quand vous n’avez pas besoin de l’historique complet du fichier journal.  

- **Merge selected files** : si vous activez cette option et que vous sélectionnez plusieurs fichiers journaux, CMTrace fusionne les journaux sélectionnés dans la vue. Il les affiche comme s’il s’agissait d’un fichier journal unique. Le journal fusionné est mis à jour de la même façon et prend en charge toutes les autres fonctionnalités de CMTrace comme s’il s’agissait d’un fichier journal unique.  


#### <a name="open-on-server"></a>Open on Server
Parcourez le dossier des journaux Configuration Manager sur un ordinateur du système de site avec la boîte de dialogue Parcourir standard. Vous pouvez également parcourir le réseau à la recherche d’un ordinateur distant.   

Quand vous sélectionnez un ordinateur distant à parcourir, CMTrace recherche le partage Configuration Manager. S’il ne trouve pas de partage avec les fichiers journaux Configuration Manager, il affiche un message d’erreur.  

Pour vous connecter directement à un ordinateur connu sans navigation, utilisez l’action [Open](#open). Entrez un nom de serveur et un partage en utilisant le format UNC.

#### <a name="print"></a>Imprimer
Affichez la boîte de dialogue Imprimer Windows standard. Cette action envoie le fichier journal actuel à une imprimante. Elle met en forme la sortie en fonction des paramètres sous l’onglet Printing de Preferences CMTrace.

#### <a name="preferences"></a>Preferences
Configurez les paramètres pour CMTrace. Les options ci-dessous sont disponibles :  

- Onglet**Général**  

     - **Update Interval** : contrôle la fréquence à laquelle CMTrace recherche des modifications apportées aux fichiers journaux et charge de nouvelles lignes. Par défaut, cette valeur est de 500 millisecondes.  

     - **Highlight** : définit la couleur que CMTrace utilise lors de la mise en surbrillance des lignes de journal que vous choisissez. Par défaut, cette couleur est le jaune de base (rouge : 255, vert : 255, bleu : 0).  

     - **Columns** : configure les colonnes qui sont visibles dans la vue du journal et l’ordre dans lequel elles apparaissent. Par défaut, les colonnes Log Text, Component, Date/Time et Thread sont affichées.  

- Onglet **Printing**  

     - **Columns** : configure les colonnes utilisées lors de l’impression de fichiers journaux et l’ordre dans lequel elles apparaissent. Par défaut, les colonnes affichées sont imprimées.  

     - **Orientation** : définit l’orientation d’impression par défaut lors de l’impression de fichiers journaux. Remplacez ce paramètre dans la boîte de dialogue d’impression. Par défaut, l’orientation Portrait est utilisée.  
 
- Onglet **Advanced**  

     - **Refresh Interval** : force CMTrace à mettre à jour la vue du journal selon un intervalle spécifié lors du chargement d’un grand nombre de lignes. Par défaut, cette option est désactivée avec une valeur égale à zéro.  

        > [!Note]  
        > En règle générale, ne modifiez pas la valeur pour **Refresh Interval**. Cela peut augmenter considérablement le délai nécessaire pour ouvrir des fichiers journaux volumineux. 


### <a name="tools-menu"></a>Menu Tools
Les actions suivantes sont disponibles dans le menu **Tools** :  
- [Find](#find)
- [Find Next](#find-next)
- [Copy to Clipboard](#copy-to-clipboard)
- [Highlight](#highlight)
- [Filter](#filter)
- [Error Lookup](#error-lookup)
- [Pause](#pause)
- [Show/Hide Details](#show/hide-details)
- [Show/Hide Info Pane](#show/hide-info-pane)

#### <a name="find"></a>Trouver
Recherchez une chaîne de texte spécifiée dans le fichier journal ouvert.  

#### <a name="find-next"></a>Suivant
Recherche la chaîne correspondante suivante, que vous avez spécifiée précédemment dans la boîte de dialogue Find.  

#### <a name="copy-to-clipboard"></a>Copy to Clipboard
Copie les lignes sélectionnées comme texte brut dans le Presse-papiers Windows. Si vous examinez les fichiers journaux Configuration Manager et CCM, il copie les colonnes dans le même ordre que l’affichage. Chaque colonne est séparée par un caractère de tabulation. Utilisez cette action lors de la copie des journaux dans les e-mails ou d’autres documents.  

#### <a name="highlight"></a>Highlight
Entrez une chaîne que CMTrace recherche dans le texte de chaque entrée de journal. Il met ensuite en surbrillance n’importe quel texte du journal qui correspond à la chaîne que vous entrez.  

- La mise en surbrillance utilise la couleur que vous avez spécifiée dans Preferences.  

- Pour désactiver la mise en surbrillance, effacez la chaîne de ce champ.  

- Si vous entrez un nombre décimal ou hexadécimal, CMTrace essaie d’associer la valeur à la colonne Thread. Ce comportement permet de mettre en surbrillance le traitement d’un thread unique, sans filtrage des autres threads qui peuvent interagir avec lui.  

- Pour comparer des chaînes par la casse, activez l’option **Case sensitive**.  
 
#### <a name="filter"></a>Filtre
Affichez ou masquez des lignes du journal en fonction des critères spécifiés. Appliquez des filtres à l’une des quatre colonnes qu’elles soient visibles ou non. Ces paramètres s’appliquent à chaque fichier journal ouvert. 

Exemples :
<!--SCCMDocs issue #603-->
- Filtrez **smsts.log** sur le texte d’entrée contenant « the action » ou « the group ». 
- Filtrez **InventoryAgent.log** avec le texte d’entrée qui contient « destination ».


#### <a name="error-lookup"></a>Error Lookup
Tapez ou collez un code d’erreur au format décimal ou hexadécimal pour afficher une description. Les sources d’erreur possibles sont les suivantes : Windows, WMI ou Winhttp.

#### <a name="pause"></a>Suspendre
Suspendez ou redémarrez la surveillance du journal. Les cas d’usage suivants représentent certaines des raisons possibles pour utiliser cette action :  

- Quand CMTrace affiche les informations du fichier journal trop rapidement  

- Quand vous suspendez la surveillance du journal, les informations que CMTrace affiche ne sont pas perdues si le fichier actif bascule vers un nouveau journal  

- Quand vous souhaitez empêcher CMTrace d’afficher de nouvelles données pendant que vous examinez le fichier journal  

#### <a name="showhide-details"></a>Show/Hide Details
Affichez ou masquez toutes les colonnes autres que le texte du journal. Cette action adapte également la colonne de texte du journal à la largeur de la fenêtre. Utilisez cette action quand vous consultez des journaux sur un ordinateur avec une résolution d’affichage faible. Elle affiche plus de texte du journal.  

> [!Note]   
> Quand vous affichez des fichiers de texte brut, CMTrace masque automatiquement les détails, car ils sont toujours vides.  
 
#### <a name="showhide-info-pane"></a>Show/Hide Info Pane
Affichez ou masquez le volet d’informations. Utilisez cette action quand vous consultez des journaux sur un ordinateur avec une résolution d’affichage faible. Elle affiche plus de détails de journalisation.  



## <a name="log-pane"></a>Volet de journal

Le volet de journal figure en haut de la fenêtre CMTrace. Il affiche des lignes des fichiers journaux. 

Quand vous sélectionnez une ligne, elle est temporairement mise en surbrillance à l’aide du modèle de couleurs de sélection Windows. 

Les lignes en surbrillance correspondent aux critères que vous définissez avec l’option **Highlight** dans le menu **Tools**. La mise en surbrillance utilise la couleur que vous spécifiez dans **Preferences**.

CMTrace affiche les lignes avec des erreurs à l’aide d’un arrière-plan rouge et de la couleur de texte jaune. Dans les journaux au format CCM, les entrées du journal ont une valeur de type explicite qui indique l’entrée comme une erreur. Pour les autres formats de journaux, CMTrace effectue une recherche non sensible à la casse dans chaque entrée de n’importe quelle chaîne de texte correspondant à « erreur ».

Il affiche les lignes avec des avertissements à l’aide d’un arrière-plan jaune. Dans les journaux au format CCM, les entrées du journal ont une valeur de type explicite qui indique l’entrée comme un avertissement. Pour les autres formats de journaux, CMTrace effectue une recherche non sensible à la casse dans chaque entrée de n’importe quelle chaîne de texte correspondant à « avertissement ».



## <a name="info-pane"></a>Volet d’informations

Le volet d’informations figure au bas de la fenêtre CMTrace. Ce pack offre les fonctionnalités suivantes :   

- Détails sur l’entrée de journal actuellement sélectionnée  

- Zone de texte qui affiche le texte du journal  

- Affichage des retours chariot afin que le texte mis en forme soit plus facile à lire  

- Entrées longues plus faciles à lire et qui ne sont pas complètement visibles dans le volet de journal  

Affichez ou masquez le volet d’informations avec l’option **Show/Hide Info Pane** dans le menu **Tools**. Si le volet d’informations occupe plus de la moitié de la fenêtre du journal, CMTrace le masque automatiquement.


### <a name="progress-bar"></a>Barre de progression

Quand vous ouvrez un fichier journal pour la première fois, CMTrace remplace le volet d’informations par une barre de progression. Cette barre de progression indique la quantité de contenu du fichier existant qui est chargée. Quand la progression atteint 100 pour cent, CMTrace supprime la barre de progression et la remplace par le volet d’informations. Lorsque vous chargez des fichiers volumineux, ce comportement vous fournit une indication de la durée possible du chargement.


### <a name="status-bar"></a>Barre d’état

Pour les fichiers journaux au format Configuration Manager et CCM, la barre d’état affiche le temps écoulé pour les entrées de journal sélectionnées. Si vous sélectionnez une seule entrée, l’outil affiche le temps écoulé entre la première entrée de journal et l’entrée sélectionnée. Si vous sélectionnez plusieurs entrées, il calcule le temps écoulé entre l’entrée sélectionnée la plus haute et l’entrée sélectionnée la plus basse. CMTrace met en forme ces informations comme suit :

`Elapsed time is <hours>h <minutes>m <seconds>s <milliseconds>ms (<seconds+milliseconds> seconds)`



## <a name="windows-shell-integration"></a>Intégration au shell Windows

CMTrace prend en charge les [associations de fichiers](#file-associations) et la fonction [glisser-déplacer](#drag-and-drop).


### <a name="file-associations"></a>Associations de fichiers 

CMTrace peut s’associer aux extensions de nom de fichier .log et .lo_. Quand le programme démarre, il vérifie le Registre pour déterminer s’il est déjà associé à ces extensions de nom de fichier. Si CMTrace n’est pas déjà associé à des extensions de nom de fichier, vous êtes invité à les associer à CMTrace. Si vous sélectionnez **Do not ask me this again**, CMTrace ignore cette vérification chaque fois qu’il est exécuté sur cet ordinateur.


### <a name="drag-and-drop"></a>Glisser-déplacer

CMTrace prend en charge la fonctionnalité glisser-déplacer de base. Faites glisser un fichier journal à partir de l’Explorateur Windows dans CMTrace pour l’ouvrir.



## <a name="other-tips"></a>Autres conseils

### <a name="last-directory-registry-key"></a>Clé de Registre Last Directory
<!--511280-->
Par défaut, CMTrace enregistre le dernier emplacement de journal que vous avez ouvert. Ce comportement est utile sur le serveur de site, car l’emplacement par défaut correspond chaque fois au chemin des journaux. 

La première fois que vous le lancez sur un client, l’emplacement par défaut correspond au répertoire de travail actuel. Cet emplacement peut être le chemin où vous avez enregistré CMTrace ou un chemin comme `%userprofile%\Desktop`. 

La valeur **Last Directory** dans la clé de Registre `HKEY_CURRENT_USER\Software\Microsoft\Trace32` contrôle cet emplacement par défaut. Si vous définissez cette valeur sur `%windir%\CCM\Logs` sur vos clients, CMTrace ouvre les fichiers à l’emplacement des journaux des clients lors de la première exécution.


## <a name="see-also"></a>Voir aussi

[Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files)
