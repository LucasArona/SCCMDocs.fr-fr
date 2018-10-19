---
title: Configurer des alertes Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment configurer les alertes Endpoint Protection dans System Center Configuration Manager.
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 78afa39b173abc79c4ed1cadc79f41ab32150ecf
ms.sourcegitcommit: 3dfe3f4401651afa9dc65d14a8944ae4e4198b3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48862360"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configurer des alertes pour Endpoint Protection dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez configurer des alertes Endpoint Protection dans Microsoft System Center Configuration Manager pour avertir les utilisateurs administratifs quand des événements spécifiques, comme une infection par un logiciel malveillant, se produisent dans votre hiérarchie. Les notifications s’affichent dans le tableau de bord Endpoint Protection, dans la console Configuration Manager, dans le nœud **Alertes** de l’espace de travail **Surveillance**. Elles peuvent aussi être envoyées par e-mail à des utilisateurs spécifiés.

 Utilisez les étapes suivantes et les procédures supplémentaires de cette rubrique pour configurer des alertes pour Endpoint Protection dans Configuration Manager.

> [!IMPORTANT]
>  Vous devez disposer de l’autorisation **Appliquer la sécurité** pour les regroupements pour pouvoir configurer des alertes Endpoint Protection.

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Étapes de configuration des alertes pour Endpoint Protection dans Configuration Manager

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements de périphériques**.

3.  Dans la liste **Regroupements d’appareils** , sélectionnez le regroupement pour lequel vous voulez configurer des alertes, puis cliquez sur **Propriétés** dans le groupe **Propriétés** sous l’onglet **Accueil**.

    > [!NOTE]
    >  Vous ne pouvez pas configurer d'alertes pour les regroupements d'utilisateurs.

4.  Sous l’onglet **Alertes** de la boîte de dialogue *Propriétés de <nom_regroupement***\>**, sélectionnez **Afficher ce regroupement dans le tableau de bord Endpoint Protection** si vous voulez voir les détails des opérations anti-programme malveillant de ce regroupement dans l’espace de travail **Surveillance** de la console Configuration Manager.

    > [!NOTE]
    >  Cette option n'est pas disponible pour le regroupement **Tous les systèmes** .

5.  Sous l’onglet **Alertes** de la boîte de dialogue *Propriétés de <nom_regroupement***\>**, cliquez sur **Ajouter**.

6.  Dans la section **Générer une alerte lorsque ces conditions s’appliquent** de la boîte de dialogue **Ajouter de nouvelles alertes de regroupement**, sélectionnez les alertes que doit générer Configuration Manager lorsque les événements Endpoint Protection spécifiés se produisent, puis cliquez sur **OK**.

7.  Dans la liste  **Conditions** de l’onglet **Alertes**, sélectionnez chaque alerte Endpoint Protection, puis spécifiez ce qui suit :

    -   **Nom d’alerte** : acceptez le nom par défaut ou entrez un nouveau nom pour l’alerte.

    -   **Gravité d’alerte** : dans la liste, sélectionnez le niveau d’alerte à afficher dans la console Configuration Manager.

8.  Selon l’alerte que vous sélectionnez, spécifiez les informations supplémentaires suivantes :

    -   **Détection d’un programme malveillant** : cette alerte est générée si un logiciel malveillant est détecté sur un ordinateur du regroupement que vous surveillez. Le **seuil de détection des programmes malveillants** indique les niveaux de détection auxquels cette alerte est générée :

        -   **Haute - Toutes les détections** : l’alerte est générée quand un programme malveillant est détecté sur un ou plusieurs ordinateurs du regroupement spécifié, quelle que soit l’action qu’exécute le client Endpoint Protection.

        -   **Moyenne - Détectée, action en attente** : l’alerte est générée quand un programme malveillant est détecté sur un ou plusieurs ordinateurs du regroupement spécifié, et que vous devez le supprimer manuellement.

        -   **Faible - Détectée, toujours active** : l’alerte est générée quand un programme malveillant est détecté sur un ou plusieurs ordinateurs du regroupement spécifié, et qu’il est toujours actif.

    -   **Apparition d’un programme malveillant** : cette alerte est générée si un programme malveillant spécifié est détecté sur un pourcentage donné d’ordinateurs du regroupement que vous surveillez.

        -   **Pourcentage d’ordinateurs sur lesquels un programme malveillant a été détecté** : l’alerte est générée quand le pourcentage d’ordinateurs avec un programme malveillant détecté dans le regroupement est supérieur au pourcentage que vous spécifiez. Spécifiez un pourcentage compris entre **1** et **99**.

            > [!NOTE]
            >  La valeur du pourcentage est basée sur le nombre d’ordinateurs du regroupement, mais exclut les ordinateurs sur lesquels aucun client Configuration Manager n’est installé. Il inclut les ordinateurs sur lesquels le client Endpoint Protection n’est pas encore installé.

    -   **Détection de logiciel malveillant répétée** : cette alerte est générée si un logiciel malveillant spécifique est détecté un nombre spécifié de fois sur un nombre spécifié d’heures sur les ordinateurs du regroupement que vous surveillez. Spécifiez les informations suivantes pour configurer cette alerte :

        -   **Nombre de fois où un programme malveillant a été détecté :** l’alerte est générée quand le nombre de détections d’un même programme malveillant sur les ordinateurs du regroupement est supérieur au nombre d’occurrences spécifié. Spécifiez un nombre compris entre **2** et **32**.

        -   **Intervalle de détection (heures) :** spécifiez l’intervalle de détection (en heures) au cours duquel le nombre de détections de programme malveillant doit être exécuté. Spécifiez un nombre compris entre **1** et **168**.

    -   **Détection de plusieurs logiciels malveillants** : cette alerte est générée si le nombre de types de programmes malveillants détectés pendant un nombre d’heures donné sur les ordinateurs du regroupement que vous surveillez est supérieur au nombre défini. Spécifiez les informations suivantes pour configurer cette alerte :

        -   **Nombre de types de programmes malveillants détectés :** l’alerte est générée quand le nombre spécifié de types différents de programmes malveillants sur les ordinateurs du regroupement est détecté. Spécifiez un nombre compris entre **2** et **32**.

        -   **Intervalle de détection (heures) :** spécifiez l’intervalle de détection, en heures, au cours duquel le nombre de détections de programme malveillant doit être exécuté. Spécifiez un nombre compris entre **1** et **168**.

9. Cliquez sur **OK** pour fermer la boîte de dialogue *Propriétés de <nom_regroupement\>**.  

## <a name="alert-for-outdated-malware-client"></a>Alerte pour les clients contre les programmes malveillants obsolètes

Depuis la version 1702 de Configuration Manager, vous pouvez configurer une alerte pour vous assurer que les clients Endpoint Protection ne sont pas obsolètes. À partir de n’importe quel regroupement d’appareils, vous pouvez maintenant ajouter des colonnes à la liste pour les attributs suivants : **Version du client anti-programme malveillant** et **État du déploiement Endpoint Protection**. Par exemple, dans la console, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Regroupements d’appareils** > **Tous les clients bureau et serveur**. Sélectionnez les colonnes à ajouter en cliquant sur leur en-tête. Pour vérifier une alerte, affichez **Alertes** dans l’espace de travail **Surveillance**. Si plus de 20 % des clients gérés exécutent une version de logiciel anti-programme malveillant ayant expiré, l’alerte « La version du client de logiciel anti-programme malveillant est obsolète » s’affiche. Cette alerte n’apparaît pas sous l’onglet **Surveillance** > **Vue d’ensemble**. Pour mettre à jour les clients de logiciel anti-programme malveillant ayant expiré, activez les mises à jour logicielles pour les clients de logiciel anti-programme malveillant.

Pour configurer le pourcentage auquel l’alerte est générée, développez **Surveillance** > **Alertes** > **Toutes les alertes**, double-cliquez sur **Clients de logiciel anti-programme malveillant obsolètes** et modifiez l’option **Générez une alerte si le pourcentage de clients gérés avec une version obsolète du client de logiciel anti-programme malveillant est supérieur à**.

> [!div class="button"]
[Étape suivante >](endpoint-definition-updates.md)

> [!div class="button"]
[Retour >](endpoint-protection-site-role.md)
