---
title: Guide de l’utilisateur du Centre logiciel
titleSuffix: Configuration Manager
description: En savoir plus sur les fonctionnalités du Centre logiciel
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 4c45da7b5a4b7f8945b23d03d0fd551276205ee2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="software-center-user-guide"></a>Guide de l’utilisateur du Centre logiciel

*S’applique à : System Center Configuration Manager (Current Branch)*

L’administrateur informatique de votre organisation utilise le Centre logiciel pour installer des applications, des mises à jour logicielles et mettre à niveau Windows. Ce guide de l’utilisateur décrit les fonctionnalités du Centre logiciel pour les utilisateurs de l’ordinateur.

### <a name="general-notes-about-software-center-functionality"></a>Remarques générales sur les fonctionnalités du Centre logiciel
- Cet article décrit les dernières fonctionnalités du Centre logiciel. Si votre organisation utilise une version antérieure du Centre logiciel, même si elle est prise en charge, les fonctionnalités ne sont pas toutes disponibles. Pour plus d’informations, contactez votre administrateur informatique.
- Votre administrateur informatique peut désactiver certains aspects du Centre logiciel. Votre expérience spécifique peut varier.
<!-- - Your IT admin may change the color of Software Center, and add your organization's logo. The images in this article show the default experience. -->



## <a name="how-to-open-software-center"></a>Comment ouvrir le Centre logiciel

La méthode la plus simple de démarrer le Centre logiciel sur un ordinateur Windows 10 est d’appuyer sur **Démarrer** et taper `Software Center`. 

Si vous naviguez dans le menu Démarrer, recherchez sous le groupe **Microsoft System Center** l’icône **Centre logiciel**.



## <a name="applications"></a>Applications

Cliquez sur l’onglet **Applications** pour rechercher et installer les applications que votre administrateur informatique déploie pour vous ou sur cet ordinateur.
- **Tout** : Affiche toutes les applications que vous pouvez installer
- **Obligatoire** : Votre administrateur informatique impose ces applications. Si vous désinstallez l’une de ces applications, le Centre logiciel la réinstalle.
- **Filtres** : Votre administrateur informatique peut créer des catégories d’applications. Si elle est disponible, cliquez sur la liste déroulante pour filtrer l’affichage sur ces applications uniquement dans une catégorie spécifique. Sélectionnez **Tout** pour afficher toutes les applications.
- **Trier par** : Réorganisez la liste d’applications. Par défaut cette liste est triée selon **Le plus récent**.
- **Rechercher** : Vous ne trouvez toujours pas ce que vous cherchez ? Entrez des mots clés dans la zone de recherche pour le trouver.
-  Basculer la vue :Cliquez sur les icônes pour basculer entre le mode Liste et le mode Mosaïque. Par défaut, la liste d’applications s’affiche sous forme de vignettes de graphique. 
    - Mode Mosaïque : Votre administrateur informatique peut personnaliser les icônes. Sous chaque vignette s’affiche le nom de l’application, l’éditeur et la version. 
    - Mode Liste : Cette vue affiche l’icône, le nom, l’éditeur, la version et l’état de l’application. 


### <a name="install-multiple-applications"></a>Installer plusieurs applications 
<!-- 1357126 -->
Installez plusieurs applications à la fois au lieu d’attendre la fin de l’une pour lancer la suivante. Les applications ne répondent pas toutes aux critères suivants :
- L’application est visible par vous
- L’application n’est pas encore en cours de téléchargement ou installée
- Votre administrateur informatique ne demande pas d’approbation pour installer l’application

Pour installer plusieurs applications à la fois :
 1. Pour activer le mode de multisélection dans le mode Liste, cliquez sur l’icône de multisélection ![Icône de sélection multiple dans le Centre logiciel](media/software-center-multi-select-apps.png) dans le coin supérieur droit.
 2. Sélectionnez plusieurs applications à installer en cochant la case à gauche des applications dans la liste.
 3. Cliquez sur le bouton **Installer les éléments sélectionnés**.

Les applications s’installent normalement, l’une après l’autre.




## <a name="updates"></a>Mises à jour

Cliquez sur l’onglet **Mises à jour** pour afficher et installer les mises à jour logicielles que votre administrateur informatique déploie sur cet ordinateur.  
- **Tout** : Affiche toutes les mises à jour que vous pouvez installer
- **Obligatoire** : Votre administrateur informatique impose ces mises à jour.
- **Trier par** : Réorganisez la liste de mises à jour. Par défaut cette liste est triée par **Nom d’application : A-Z**.

Pour installer les mises à jour, cliquez sur **Tout installer**.

Pour installer uniquement des mises à jour spécifiques, cliquez sur l’icône pour basculer sur le mode multisélection. Examinez les mises à jour à installer, puis cliquez sur **Installer la sélection**.



## <a name="operating-systems"></a>Systèmes d'exploitation

Cliquez sur l’onglet **Systèmes d’exploitation** pour afficher et installer les versions de Windows que votre administrateur informatique déploie sur cet ordinateur.  
- **Tout** : Affiche toutes les versions de Windows que vous pouvez installer
- **Obligatoire** : Votre administrateur informatique impose ces mises à niveau.
- **Trier par** : Réorganisez la liste de mises à jour. Par défaut cette liste est triée par **Nom d’application : A-Z**.



## <a name="installation-status"></a>État de l’installation

Cliquez sur l’onglet **État d’installation** pour afficher l’état des applications. Vous pouvez voir les états suivants :
- **Installé**: Le Centre logiciel a déjà installé cette application sur cet ordinateur.
- **Téléchargement** : Le Centre logiciel télécharge le logiciel à installer sur cet ordinateur.
- **Échec** : Le Centre logiciel a rencontré une erreur en essayant d’installer le logiciel.



## <a name="device-compliance"></a>Conformité de l’appareil

Cliquez sur l’onglet **Conformité de l’appareil** pour afficher l’état de conformité de cet ordinateur.

Cliquez sur **Vérifier la conformité** pour évaluer les paramètres de l’appareil par rapport aux stratégies de sécurité définies par votre administrateur informatique.



## <a name="options"></a>Options

Cliquez sur l’onglet **Options** pour afficher les paramètres supplémentaires pour cet ordinateur.

### <a name="work-information"></a>Informations d’utilisation

Indiquer vos heures de travail habituelles. Votre administrateur informatique peut planifier des installations de logiciels en dehors des heures de travail. Réservez au moins quatre heures par jour pour les tâches de maintenance système. Votre administrateur informatique peut toujours installer les applications et les mises à jour logicielles critiques pendant les heures de travail.

- Cliquez sur les listes déroulantes pour sélectionner la plage horaire la plus large pendant laquelle vous êtes susceptible d’utiliser l’ordinateur. Par défaut, ces valeurs vont de **5 h 00** à **22 h 00**

- Cochez la case à côté des jours de la semaine pendant lesquels vous utilisez généralement cet ordinateur. Le Centre logiciel sélectionne uniquement les jours de semaine par défaut.  


### <a name="power-management"></a>Gestion de l'alimentation

Votre administrateur informatique peut définir des stratégies de gestion d’alimentation. Ces stratégies permettent à votre organisation d’économiser l’électricité quand l’ordinateur n’est pas utilisé. 

Pour exempter cet ordinateur de ces stratégies, cochez la case **Ne pas appliquer les paramètres d’alimentation de mon service informatique à cet ordinateur**. Ce paramètre est désactivé par défaut, l’ordinateur applique les paramètres d’alimentation. 


### <a name="computer-maintenance"></a>Maintenance de l’ordinateur

Spécifier la façon dont le Centre logiciel applique les modifications de logiciel avant l’échéance
- **Installer ou désinstaller automatiquement les logiciels obligatoires et redémarrer l’ordinateur uniquement en dehors des heures de bureau spécifiées** : Ce paramètre est désactivé par défaut.
- **Suspendre les activités du Centre logiciel quand mon ordinateur est en mode présentation** : Ce paramètre est activé par défaut.
- **Stratégie de synchronisation** : Cliquez sur ce bouton quand votre administrateur informatique vous l’indique. Cet ordinateur recherche sur les serveurs toutes les nouveautés en termes d’applications, de mises à jour logicielles ou de systèmes d’exploitation.

