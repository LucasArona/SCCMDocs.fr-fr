---
title: Capacités de la version Technical Preview 1608
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1608 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 339ad109eae4d54ff5f8e04e18f29c9e47e8930d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121673"
---
# <a name="capabilities-in-technical-preview-1608-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1608 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1608 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  




##  <a name="improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step"></a>Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture  
L’étape de préparation du client ConfigMgr va désormais supprimer complètement le client Configuration Manager, au lieu de supprimer uniquement des informations clés. Lorsque la séquence de tâches déploie l’image capturée du système d’exploitation, elle installe un nouveau client Configuration Manager chaque fois.  


## <a name="improvements-to-software-center"></a>Améliorations apportées au Centre logiciel
* Les onglets **Applications**, **Mises à jour** et **Systèmes d’exploitation** du Centre logiciel affichent désormais les logiciels récemment ajoutés. Les nombres du volet de navigation indiquent combien de nouveaux fragments de logiciels figurent sous chaque onglet.
* Les utilisateurs peuvent désormais demander une approbation pour des applications, puis afficher l’historique des demandes dans la vue **Détails de l’application** du Centre logiciel. Le bouton **Requête** dans **Détails de l’application** ne redirige plus vers le catalogue d’applications web.

## <a name="improvements-to-asset-intelligence"></a>Améliorations apportées à Asset Intelligence
Nous avons ajouté un champ dans les propriétés pour les logiciels inventoriés qui vous permet de définir une relation parent-enfant avec d’autres logiciels. Dans la liste des logiciels inventoriés, vous pouvez alors afficher le parent de tous les logiciels et également masquer tous les logiciels enfants.

### <a name="configure-a-parent-to-child-relationship"></a>Configurer une relation parent-enfant
  1. Pour définir un logiciel parent, dans le nœud Logiciels inventoriés, cliquez avec le bouton droit sur un élément logiciel dans la liste **Logiciels inventoriés**, puis choisissez **propriétés**.
  2. Dans la boîte de dialogue qui s’ouvre, sélectionnez le logiciel que vous souhaitez définir en tant que logiciel parent pour votre sélection initiale.

### <a name="filter-the-software-display"></a>Filtrer l’affichage des logiciels
Après avoir défini des relations parent-enfant, vous pouvez filtrer votre vue pour afficher uniquement les logiciels qui sont parents ou qui n’ont aucune relation définie. Cela masque tout logiciel défini en tant qu’enfant d’un autre logiciel inventorié. Pour cela :
   1.   Pour le volet de recherche, choisissez **Ajouter des critères**.
   2. Sélectionnez **Logiciel parent** et modifiez la valeur du critère en spécifiant **est vide**, puis cliquez sur **Rechercher**.

L’affichage indique à présent uniquement les éléments logiciels parents et les logiciels qui n’ont pas de relations définies. Un logiciel qui n’est qu’un enfant d’un autre titre n’apparaît pas.

## <a name="remote-control-keyboard-translation"></a>Traduction du clavier de contrôle à distance
Dans le passé, Configuration Manager transmettait la position des touches à partir de l’emplacement de l’utilisateur vers l’emplacement de la personne effectuant le partage. Cela posait des problèmes pour les configurations de clavier qui différaient entre l’afficheur et la personne effectuant le partage. Par exemple, un afficheur avec un clavier anglais tapait un « A », mais le clavier français de la personne effectuant le partage fournissait un « Q ». Nous modifions le comportement par défaut afin que le caractère lui-même soit transmis du clavier de l’afficheur vers la personne effectuant le partage, et que ce que l’afficheur souhaite taper parvienne auprès de la personne effectuant le partage.

Ce comportement peut être désactivé par l’afficheur s’il préfère taper en fonction de la disposition du clavier de la personne effectuant le partage. Pour modifier ce comportement, dans **Contrôle à distance de Configuration Manager**, choisissez **Action** et choisissez **Activer la traduction du clavier** pour transmettre la position des touches.

> [!NOTE]
>
> Les touches spéciales, notamment ~!#@$%, ne seront pas traduites correctement.
