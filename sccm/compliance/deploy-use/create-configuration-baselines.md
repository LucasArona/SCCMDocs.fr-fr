---
title: Créer des bases de référence de configuration
titleSuffix: Configuration Manager
description: Créez des bases de référence de configuration dans System Center Configuration Manager pour les déployer ensuite dans un regroupement.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1a6d09e4a5552770a71dc44f473cebd13ba0715c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32331945"
---
# <a name="create-configuration-baselines-in-system-center-configuration-manager"></a>Créer des bases de référence de configuration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les bases de référence de configuration System Center Configuration Manager contiennent des éléments de configuration prédéfinis et, éventuellement, d’autres bases de référence de configuration. Après avoir créé une base de référence de configuration, vous pouvez la déployer vers un regroupement afin que les périphériques de ce regroupement puissent la télécharger et évaluer leur compatibilité avec elle.  

 Les bases de référence de configuration dans Configuration Manager peuvent contenir des révisions spécifiques des éléments de configuration, ou être configurées pour toujours utiliser la dernière version d’un élément de configuration. Pour plus d’informations sur les révisions des éléments de configuration, consultez [Tâches de gestion des données de configuration](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Vous pouvez créer des bases de référence de configuration selon deux méthodes différentes :  

-   Importer des données de configuration depuis un fichier. Pour démarrer l’ **Assistant Importer des données de configuration**, dans le nœud **Éléments de configuration** ou **Lignes de base de configuration** de l’espace de travail **Biens et conformité** , cliquez sur **Importer des données de configuration**.  

-   Utilisez la boîte de dialogue **Créer une ligne de base de configuration** pour créer une nouvelle ligne de base de configuration.  

 Procédez comme suit pour créer une ligne de base de configuration à l'aide de la boîte de dialogue **Créer une ligne de base de configuration** .  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Lignes de base de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une ligne de base de configuration**.  

4.  Dans la boîte de dialogue **Créer une ligne de base de configuration** , entrez un nom unique et une description pour la ligne de base de configuration. Vous pouvez utiliser un maximum de 255 caractères pour le nom et de 512 caractères pour la description.  

5.  La liste **Données de configuration** affiche tous les éléments de configuration ou toutes les bases de référence de configuration qui sont inclus dans cette base de référence de configuration. Cliquez sur **Ajouter** pour ajouter à la liste un nouvel élément de configuration ou une nouvelle ligne de base de configuration. Vous pouvez choisir parmi les priorités suivantes :  

    -   **Éléments de configuration**  

    -   **Mises à jour logicielles**  

    -   **Lignes de base de configuration**  
      > [!IMPORTANT]
      > Vous devez limiter chaque base de référence de configuration à 1 000 mises à jour logicielles.
6.  Utilisez la liste **Changer d’objet** pour spécifier le comportement d’un élément de configuration que vous avez sélectionné dans la liste **Données de configuration** . Vous pouvez choisir parmi les options suivantes  

    -   **Obligatoire** La base de référence de configuration est évaluée comme non compatible si l’élément de configuration n’est pas détecté sur un périphérique client. S’il est détecté, sa conformité est évaluée.  

    -   **Facultatif** La conformité de l’élément de configuration n’est évaluée que si l’application à laquelle il fait référence se trouve sur des ordinateurs client. Si l’application est introuvable, la base de référence de configuration n’est pas marquée comme non compatible (applicable uniquement aux éléments de configuration d’application).  

    -   **Interdit** La base de référence de configuration est évaluée comme non compatible si l’élément de configuration est détecté sur des ordinateurs client (applicable uniquement aux éléments de configuration d’application).  

    > [!NOTE]
    >  La liste **Changer d’objet** est disponible uniquement si vous avez cliqué sur l’option **Cet élément de configuration contient des paramètres d’application** dans la page **Général** de l’Assistant **Création d’élément de configuration**.  

7.  Utilisez la liste **Changer de révision** pour sélectionner une révision spécifique ou la dernière révision de l’élément de configuration afin d’évaluer la conformité sur des périphériques client ou sélectionnez **Toujours utiliser le dernier** pour toujours utiliser la dernière révision. Pour plus d’informations sur les révisions des éléments de configuration, consultez [Tâches de gestion des données de configuration](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

8.  Pour supprimer un élément de configuration de la base de référence de configuration, sélectionnez un élément de configuration, puis cliquez sur **Supprimer**.  

9. Cliquez sur **OK** pour fermer la boîte de dialogue **Créer une ligne de base de configuration** et pour créer la ligne de base de configuration.  
