---
title: Capacités de la version Technical Preview 1704
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1704 de System Center Configuration Manager.
ms.date: 4/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e01270a5666e06f7072c4680398f5c5b590208b3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135134"
---
# <a name="capabilities-in-technical-preview-1704-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1704 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans la version d’évaluation technique 1704 de System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site de version d’évaluation technique Configuration Manager. Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Configurer des applications Android avec des stratégies de configuration des applications
Vous pouvez utiliser des stratégies de configuration des applications disponibles dans System Center Configuration Manager (Configuration Manager) pour distribuer les paramètres pouvant être nécessaires quand un utilisateur exécute une application sur des appareils Android for Work. Les stratégies de configuration des applications Android sont disponibles uniquement sur les appareils Android for Work et s’appliquent aux applications approuvées du magasin Play for Work.

### <a name="try-it-out"></a>Faîtes un essai                 

Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de configuration des applications** puis **Créer une stratégie de configuration d'application**. Sur la page **Général** de l’Assistant, vous pouvez à présent **sélectionner un type de stratégie de configuration**. Spécifiez la plateforme ciblée par la stratégie de configuration d’application : **Stratégie de configuration pour les applications Android for Work**. Vous pouvez ensuite **spécifier des paires nom/valeur** ou **accéder à un fichier JSON de liste de propriétés**. La nouvelle stratégie de configuration des applications s’affiche dans le nœud **Stratégies de configuration des applications** de l’espace de travail **Bibliothèque de logiciels**. Pour associer une stratégie de configuration des applications au déploiement d’une application Android for Work, déployez l’application comme vous le faites habituellement, en suivant la procédure décrite dans la rubrique [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).

## <a name="hardware-inventory-collects-secure-boot-information"></a>L’inventaire matériel collecte des informations sur le démarrage sécurisé
L’inventaire matériel collecte désormais des informations indiquant si le démarrage sécurisé est activé sur les clients. Ces informations sont stockées dans la classe **SMS_Firmware** (introduite dans la version 1702) et activées dans l’inventaire matériel par défaut. Pour plus d’informations sur l’inventaire matériel, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Ajouter des séquences de tâches enfants à une séquence de tâches
Dans cette version, vous pouvez ajouter une nouvelle étape de séquence de tâches qui exécute une autre séquence de tâches, créant ainsi une relation parent/enfant entre les séquences de tâches. Cela vous permet de créer et d’utiliser des séquences de tâches plus modulaires.  

Lorsque vous ajoutez une séquence de tâches enfant à une séquence de tâches, considérez les éléments suivants :

- Les séquences de tâches parent et enfant sont en fait combinées en une stratégie unique exécutée par le client.
- Il n’est pas possible d’ajouter une séquence de tâches enfant qui est un parent d’une autre séquence de tâches.
- L’environnement est global. Par exemple, si une variable est définie par la séquence de tâches parent avant d’être modifiée par la séquence de tâches enfant, la variable restera modifiée. De même, si la séquence de tâches enfant crée une nouvelle variable, la variable est disponible pour les étapes restantes de la séquence de tâches parent.
- Les messages d’état sont envoyés normalement pour une opération de séquence de tâches unique.
- Les séquences de tâches inscrivent des entrées dans le fichier smsts.log et le nouveau journal écritures indique clairement lorsqu’une séquence de tâches enfant démarre.
- Dans la version d’évaluation technique 1704 de Configuration Manager, si les séquences de tâches enfants font référence à un package et que vous exécutez la séquence de tâches parent depuis le Centre logiciel, le client ne trouvera pas le contenu du package lors de l’exécution de la séquence de tâches enfant. Dans ce scénario, vous devez exécuter la séquence de tâches à partir du support (support de démarrage, PXE, etc.).  

    Si la séquence de tâches enfant utilise des étapes comme **Exécuter la ligne de commande** (sans aucune référence de package), **Format**, **BitLocker**, etc., la séquence de tâches est exécutée avec succès depuis le Centre logiciel.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>Pour ajouter une séquence de tâches enfant à une séquence de tâches
1. Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis cliquez sur **Exécuter la séquence de tâches**.
2. Cliquez sur **Parcourir** pour sélectionner la séquence de tâches enfant.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Recharger les images de démarrage avec la version actuelle de Windows PE
Lorsque vous exécutez l’option **Mise à jour des points de distribution** sur une image de démarrage sélectionnée, vous pouvez maintenant choisir de recharger la dernière version de Windows PE (depuis le répertoire d’installation de Windows ADK) dans l’image de démarrage. La page **Général** de l’Assistant fournit des informations sur la version de Windows ADK installée sur le serveur du site, la version de Windows ADK à partir de laquelle Windows PE a été utilisé dans l’image de démarrage, et la version du client Configuration Manager. Vous pouvez utiliser ces informations pour vous aider à décider s’il faut recharger l’image de démarrage. En outre, une nouvelle colonne (**Version du client**) a été ajoutée lorsque vous affichez des images de démarrage dans le nœud **Images de démarrage** et vous indique la version du client Configuration Manager utilisée par chaque image de démarrage.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>Pour recharger une image de démarrage avec la version actuelle de Windows PE

1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Images de démarrage**.
2. Sélectionnez une image de démarrage, puis cliquez sur **Mise à jour des points de distribution**.
3. Sur la page **Général** de l’Assistant, sélectionnez l’option pour **recharger l’image à l’aide de la version actuelle de Windows PE à partir de Windows ADK installé**.

## <a name="improvements-to-operating-system-deployment"></a>Améliorations apportées au déploiement des systèmes d’exploitation
Les améliorations suivantes, inspirées par vos commentaires, ont été apportées au déploiement des systèmes d’exploitation.

- [Nouvelle colonne **Version du système d’exploitation** pour les images de système d’exploitation](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f) : Nous avons ajouté une nouvelle colonne nommée **Version du système d’exploitation** pour montrer la version du système d’exploitation de l’image quand vous affichez des informations dans les nœuds **Images du système d’exploitation** et **Packages de mise à niveau du système d’exploitation**. Seule la version du premier index du fichier .WIM s’affiche. Accédez à l’onglet **Détails** de l’image pour vérifier les versions du système d’exploitation des autres index.

- [Journalisation plus efficace dans Smsts.log](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless) : À compter de cette version, les entrées ne sont plus inscrites dans le fichier smsts.log pour les informations CCM_CIVersionInfo.PolicyID. Avant cette version, un grand nombre d’entrées pouvaient contenir ces informations, ce qui compliquait la recherche d’informations plus pertinentes dans le fichier journal.
