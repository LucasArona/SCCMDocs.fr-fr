---
title: Configurer l’état du client
titleSuffix: Configuration Manager
description: Sélectionnez les paramètres d’état du client dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 960c6c91bfc7d0b8e7db191ac2bb0ee6286884b4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420037"
---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>Comment configurer l’état du client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Afin de surveiller l’état du client System Center Configuration Manager et de corriger les problèmes rencontrés, vous devez configurer votre site pour spécifier les paramètres qui sont utilisés pour marquer des clients comme inactifs et configurer des options pour vous avertir si l’activité du client passe sous un seuil spécifié. Il est également possible de désactiver la résolution automatique par les ordinateurs des problèmes rencontrés par l'état du client.  

##  <a name="BKMK_1"></a> Pour configurer l’état du client  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , cliquez sur **État du client**, puis dans l'onglet **Accueil** , dans le groupe **État du client** , cliquez sur **Paramètres d'état du client**.  

3.  Dans la boîte de dialogue **Propriétés des paramètres d'état des clients** , spécifiez les valeurs suivantes pour déterminer l'activité du client :  

    > [!NOTE]  
    >  Si aucun des paramètres n'est satisfait, le client sera marqué comme inactif.  

    -   **Demandes de stratégie client lors des jours suivants :** Spécifiez le nombre de jours depuis qu'un client a demandé une stratégie. La valeur par défaut est **7** jours.  

    -   **Découverte par pulsations d’inventaire lors des jours suivants :** Spécifiez le nombre de jours depuis que l'ordinateur client a envoyé un enregistrement de découverte par pulsations d'inventaire à la base de données du site. La valeur par défaut est **7** jours.  

    -   **Inventaire matériel lors des jours suivants :** Spécifiez le nombre de jours depuis que l'ordinateur client a envoyé un enregistrement d'inventaire matériel à la base de données du site. La valeur par défaut est **7** jours.  

    -   **Inventaire des logiciels lors des jours suivants :** Spécifiez le nombre de jours depuis que l'ordinateur client a envoyé un enregistrement d'inventaire logiciel à la base de données du site. La valeur par défaut est **7** jours.  

    -   **Messages d’état lors des jours suivants :** Spécifiez le nombre de jours depuis que l'ordinateur client a envoyé des messages d'état à la base de données du site. La valeur par défaut est **7** jours.  

4.  Dans la boîte de dialogue **Propriétés des paramètres d'état des clients** , spécifiez la valeur suivante pour déterminer la durée pendant laquelle les données de l'historique d'état du client sont conservées :  

    -   **Conserver l’historique de l’état du client pendant le nombre de jours suivant :** Spécifiez la durée pendant laquelle vous voulez que l'historique de l'état du client soit conservé dans la base de données du site. La valeur par défaut est **31** jours.  

5.  Cliquez sur **OK** pour enregistrer les propriétés et fermer la boîte de dialogue **Propriétés des paramètres d'état des clients** .  

##  <a name="BKMK_Schedule"></a> Pour configurer le calendrier de l’état du client  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , cliquez sur **État du client**, puis dans l'onglet **Accueil** , dans le groupe **État du client** , cliquez sur **Planifier la mise à jour de l'état des clients**.  

3.  Dans la boîte de dialogue **Planifier la mise à jour de l'état des clients** , configurez la fréquence à laquelle vous souhaitez que l'état des clients soit mis à jour, puis cliquez sur OK.  

    > [!NOTE]  
    >  Lorsque vous modifiez la planification des mises à jour de l'état des clients, la mise à jour ne prend effet que lors de la mise à jour de l'état des clients suivante (selon le calendrier précédemment configuré).  

##  <a name="BKMK_2"></a> Pour configurer des alertes liées à l’état du client  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements de périphériques**.  

3. Dans la liste **Regroupements de périphériques** , sélectionnez le regroupement pour lequel vous souhaitez configurer des alertes, puis cliquez sur **Propriétés** dans l'onglet **Accueil** , du groupe **Propriétés**.  

   > [!NOTE]  
   >  Vous ne pouvez pas configurer d'alertes pour les regroupements d'utilisateurs.  

4. Sous l’onglet **Alertes** de la boîte de dialogue **Propriétés de**<em>&lt;Nom du regroupement\></em>, cliquez sur **Ajouter**.  

   > [!NOTE]  
   >  L'onglet **Alertes** n'est visible que si le rôle de sécurité auquel vous êtes associé dispose d'autorisations pour les alertes.  

5. Dans la boîte de dialogue **Ajouter de nouvelles alertes de regroupement** , choisissez les alertes que vous souhaitez générer lorsque les seuils d'état du client passent sous une valeur spécifique, puis cliquez sur **OK**.  

6. Dans la liste **Conditions** de l'onglet **Alertes** , sélectionnez chaque alerte relative à l'état du client, puis spécifiez les informations suivantes.  

   -   **Nom d’alerte** – Acceptez le nom par défaut ou entrez un nouveau nom pour l’alerte.  

   -   **Gravité d’alerte** – Dans la liste déroulante, choisissez la gravité d’alerte qui sera affichée dans la console Configuration Manager.  

   -   **Déclencher l’alerte** – Spécifiez le pourcentage seuil pour l’alerte.  

7. Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de**<em>&lt;Nom du regroupement\></em>.  

##  <a name="BKMK_3"></a> Pour exclure des ordinateurs de la résolution automatique  

1. Ouvrez l'éditeur du Registre sur l'ordinateur client pour lequel vous souhaitez désactiver la résolution automatique.  

   > [!WARNING]  
   >  Une utilisation incorrecte de l'Éditeur du Registre peut éventuellement provoquer de graves problèmes, lesquels nécessitent parfois la réinstallation complète du système d'exploitation. Microsoft ne garantit pas la résolution des erreurs résultant d'une utilisation incorrecte de l'Éditeur du Registre. Les opérations exécutées dans l'Éditeur du Registre le sont à vos propres risques.  

2. Accédez à **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3. Entrez l'une des valeurs suivantes pour cette clé de Registre :  

   -   **Vrai** – L’ordinateur client ne résoudra pas automatiquement les problèmes détectés. Vous serez toutefois alerté dans l'espace de travail **Surveillance** des problèmes survenus pour ce client.  

   -   **Faux** – L’ordinateur client résoudra automatiquement les problèmes détectés et vous serez alerté dans l’espace de travail **Surveillance**. Il s'agit du paramètre par défaut.  

4. Fermez l'éditeur du Registre.  

   Vous pouvez également installer des clients à l'aide de la propriété d'installation CCMSetup **NotifyOnly** pour les exclure de la résolution automatique. Pour plus d’informations sur cette propriété d’installation du client, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  
