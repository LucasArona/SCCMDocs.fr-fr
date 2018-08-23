---
title: Maintenance des mises à jour logicielles
titleSuffix: Configuration Manager
description: Pour assurer la maintenance des mises à jour dans Configuration Manager, vous pouvez planifier la tâche de nettoyage WSUS, ou vous pouvez l’exécuter manuellement.
author: aczechowski
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 4b0e2e90-aac7-4d06-a707-512eee6e576c
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3a44643870234a08169db1d55cc834e4ca5fcbb5
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385488"
---
# <a name="software-updates-maintenance"></a>Maintenance des mises à jour logicielles

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez planifier et exécuter des tâches de nettoyage WSUS à partir de la console Configuration Manager, dans les propriétés du composant de point de mise à jour logicielle. Quand vous choisissez pour la première fois d’exécuter la tâche de nettoyage WSUS, elle s’exécute à l’issue de la synchronisation des mises à jour logicielles suivante.  

## <a name="to-schedule-and-run-the-wsus-cleanup-job"></a>Pour planifier et exécuter la tâche de nettoyage WSUS 
Planifiez la tâche de nettoyage WSUS en exécutant les étapes suivantes :   

1.  Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Sites**. 
2. Sélectionnez le site situé au sommet de votre hiérarchie Configuration Manager. 

3.  Cliquez sur **Configurer les composants de site** dans le groupe **Paramètres** , puis cliquez sur **Point de mise à jour logicielle** pour ouvrir les propriétés du composant du point de mise à jour logicielle.  

4. Examinez le **Comportement de remplacement**. Modifiez le comportement, si nécessaire. 
![capture d’écran du comportement de remplacement](media/sccm-supersedence-behavior.PNG)

5.  Cliquez sur l’onglet **Règles de remplacement**, puis sélectionnez **Exécutez l’Assistant de nettoyage WSUS**. Dans la version 1806, l’option est renommée **Exécuter le nettoyage de WSUS après la synchronisation**. 
 
6. Cliquez sur **OK** (cliquez sur **Fermer** si vous utilisez la version 1806).

## <a name="wsus-cleanup-behavior-in-version-1802-and-earlier"></a>Comportement du nettoyage WSUS dans la version 1802 et antérieures
Avant Configuration Manager version 1806, l’option de nettoyage WSUS exécute l’élément suivant : 
- L’option **Mises à jour expirées** de l’Assistant Nettoyage de WSUS sur le serveur WSUS du site de niveau supérieur uniquement. 
![capture d’écran du nettoyage WSUS pour les mises à jour expirées](media/wsus-cleanup-expired.PNG)

-  Le nettoyage des éléments de configuration des mises à jour logicielles se produit dans la base de données Configuration Manager tous les sept jours et supprime les mises à jour superflues de la console. 
   - Cette opération de nettoyage ne supprime pas les mises à jour expirées de la console Configuration Manager si elles sont actuellement déployées. 

Des opérations de maintenance supplémentaire restent nécessaires dans la base de données WSUS de niveau supérieur et dans toutes les autres bases de données WSUS présentes dans l’environnement. Pour obtenir des informations complémentaires et des instructions, consultez le billet de blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/). 


## <a name="wsus-cleanup-behavior-starting-in-version-1806"></a>Comportement de nettoyage WSUS à partir de la version 1806
Depuis la version 1806, l’option de nettoyage WSUS s’actionne après chaque synchronisation et procède aux opérations de nettoyage suivantes : <!--1357898 -->
- L’option **Mises à jour expirées** pour les serveurs WSUS sur le site d’administration centrale et les sites principaux.
    - Les serveurs WSUS des sites secondaires n’exécutent pas les opérations de nettoyage WSUS pour les mises à jour expirées. 
- Configuration Manager génère une liste de mises à jour remplacées à partir de sa base de données. La liste est basée sur le comportement de remplacement dans les propriétés du composant Point de mise à jour logicielle. 
    - Les éléments de configuration de mise à jour répondant aux critères de comportement de remplacement sont expirés dans la console Configuration Manager.
    - Les mises à jour sont refusées dans WSUS pour le site d’administration centrale et les sites principaux, mais pas pour les sites secondaires.
- Le nettoyage des éléments de configuration des mises à jour logicielles se produit dans la base de données Configuration Manager tous les sept jours et supprime les mises à jour superflues de la console. 
    - Cette opération de nettoyage ne supprime pas les mises à jour expirées de la console Configuration Manager si elles sont actuellement déployées. 

> [!NOTE]
> L’option « Mois à attendre avant qu’une mise à jour logicielle remplacée n’expire » est basée sur la date de création de la mise à jour de remplacement. Par exemple, si vous définissez ce paramètre sur 2 mois, les mises à jour qui ont été remplacées sont refusées dans WSUS et expirées dans Configuration Manager dès que la mise à jour de remplacement a 2 mois. 

Toutes les opérations de maintenance WSUS doivent être exécutées manuellement sur les bases de données WSUS d’un site secondaire. Les options de l’**Assistant de nettoyage du serveur WSUS** répertoriées ci-dessous ne s’exécutent pas sur le site d’administration centrale et les sites principaux :

- Mises à jour et révisions de mises à jour inutilisées
- Ordinateurs ne contactant pas le serveur
- Fichiers de mise à jour superflus

 Pour obtenir des informations complémentaires et des instructions, consultez le billet de blog [The complete guide to Microsoft WSUS and Configuration Manager SUP maintenance](https://blogs.technet.microsoft.com/configurationmgr/2016/01/26/the-complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maintenance/). 

## <a name="updates-cleanup-log-entries"></a>Entrées du journal de nettoyage des mises à jour
 
Vous pouvez vérifier cette opération de nettoyage en consultant le fichier wsyncmgr.log pour les entrées suivantes : 
  - Le refus des mises à jour remplacées dans WSUS est effectif dès lors que vous voyez cette entrée du journal : `Cleanup processed <number> total updates and declined <number>`
  - Le nettoyage WSUS démarre dès que vous voyez cette entrée : `Calling WSUS Cleanup.`
  - Le nettoyage WSUS des mises à jour expirées est terminé dès vous voyez cette entrée : `Successfully completed WSUS Cleanup.`
  - Le nettoyage des éléments de configuration des mises à jour expirées Configuration Manager démarre dès que vous voyez cette entrée : `Deleting old expired updates...`
  - Le nettoyage des éléments de configuration des mises à jour expirées Configuration Manager est terminé dès que vous voyez cette entrée : `Deleted <number> expired updates total`
