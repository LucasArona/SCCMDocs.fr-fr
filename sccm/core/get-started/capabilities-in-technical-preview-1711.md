---
title: Technical Preview 1711 | Microsoft Docs
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1711 de System Center Configuration Manager.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 645f41a7bad4bd9365c9ec9d51e2567ae270385a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123295"
---
# <a name="capabilities-in-technical-preview-1711-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1711 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version 1711 de Technical Preview pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problèmes connus dans cette version d’évaluation technique :**
- **Prise en charge de Windows 10, version 1709 (également appelée Fall Creators Update)**.  À partir de cette version de Windows, Windows Media inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour utiliser un package de mise à niveau de système d’exploitation ou une image de système d’exploitation, veillez à sélectionner une [édition prise en charge par Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
- **La mise à jour vers une nouvelle préversion échoue s’il existe un serveur de site en mode passif**. Si vous exécutez une préversion qui a un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez désinstaller ce dernier pour pouvoir correctement mettre à jour votre site de préversion vers cette nouvelle préversion. Vous pouvez réinstaller le serveur de site en mode passif une fois votre site mis à jour.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Améliorations apportées à l’exécution de la séquence de tâches
<!-- 1261338 -->

Cette préversion technique améliore l’étape d’exécution de la séquence de tâches. Les améliorations sont notamment les suivantes :

 - Prise en charge de tous les scénarios de déploiement de système d’exploitation à partir du Centre logiciel, de l’environnement PXE (Preboot Execution Environment) et de médias.
 - Améliorations apportées à des actions de console comme la copie, l’importation, l’exportation et l’avertissement lors de la suppression d’objets.
 - Prise en charge de l’**Assistant Création de contenu préparé**.
 - Intégration à la vérification du déploiement.
 - Vous pouvez désormais utiliser l’étape d’exécution de la séquence de tâches sur plusieurs niveaux de séquences de tâches, et non uniquement sur une relation parent-enfant unique. Les relations multiniveaux ajoutent de la complexité, alors utilisez-les avec précaution. Les références circulaires sont toujours vérifiées dans ces relations.

### <a name="try-it-out"></a>Essayez !  

Essayez d’effectuer les tâches suivantes, puis envoyez-nous vos **Commentaires** à partir de l’onglet **Accueil** du ruban pour nous dire comment cela a fonctionné pour vous :

1. Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis cliquez sur **Exécuter la séquence de tâches**.
2. Cliquez sur **Parcourir** pour sélectionner la séquence de tâches enfant.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Autoriser l’interaction utilisateur durant l’installation d’une application <!-- 1356976 -->

Avec cette préversion, vous pouvez autoriser un utilisateur final à interagir avec l’installation d’une application pendant l’exécution de la séquence de tâches. Par exemple, exécutez un processus d’installation qui invite l’utilisateur final à choisir diverses options. Certains programmes d’installation d’application ne peuvent pas se passer d’invites utilisateur ou le processus d’installation exige des valeurs de configuration spécifiques que seul l’utilisateur connaît. Cette fonctionnalité vous permet de gérer ces scénarios d’installation.

### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches suivantes, puis envoyez vos **Commentaires** à partir de l’onglet **Accueil** du ruban pour nous dire comment cela a fonctionné pour vous :

1.  Créez ou modifiez une application. Pour plus d’informations, consultez [Créer des applications avec System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

    a. Choisissez l’onglet **Expérience utilisateur** dans les **propriétés Windows Installer (\*fichier msi)**.

    b. Sélectionnez **Installer pour le système** pour **Comportement à l’installation**.

    c. Sélectionnez **Qu’un utilisateur ait ouvert une session ou non** pour **Condition d’ouverture de session**.

    d. Sélectionnez **Normale** pour **Visibilité du programme d’installation**. Vous pouvez choisir parmi les trois options suivantes : **Réduite**, **Normale** ou **Agrandie**.

    e. Cochez la case **Autoriser les utilisateurs à interagir avec l’installation du programme**.

2.  Créez ou modifiez une séquence de tâches pour installer l’application à l’aide de l’étape **Installer l’application**. Pour plus d’informations, consultez [Installer l’application](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) dans les [étapes de séquence de tâches dans System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Séquence de tâches d’acquisition des images après l’étape d’installation de Windows et Configuration Manager.

    b. Séquence de tâches de mise à niveau en place dans le groupe post-traitement.

3.  Déployez la séquence de tâches sur un client.
4.  Installez la séquence de tâches depuis le Centre logiciel.

Pendant le déroulement de la séquence de tâches, l’interface de l’installation de l’application s’affiche sur l’appareil de l’utilisateur final cible. La séquence de tâches s’interrompt jusqu’à ce que l’utilisateur final termine le flux de travail de l’installation de l’application.

### <a name="install-using-the-wizard"></a>Installer à l’aide de l’Assistant

Vous pouvez également utiliser cette fonctionnalité lors du déploiement d’une application à l’aide de l’Assistant.

1. Créez ou modifiez une application.
2. Déployez l’application sur un client.
3. Installez l’application à partir du Centre logiciel. L’interface d’installation de l’application doit apparaître. L’utilisateur final doit suivre l’Assistant Installation de l’application pour installer correctement l’application.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
