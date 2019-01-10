---
title: Mettez à niveau les clients.
titleSuffix: Configuration Manager
description: Mettez à niveau les clients sur des ordinateurs Windows dans System Center Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9274cbe8d4e5e4e233c0abfdc09582a4d7de329
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53817815"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-system-center-configuration-manager"></a>Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour mettre à niveau le client sur des ordinateurs Windows, vous pouvez utiliser les méthodes d’installation de clients ou les fonctionnalités de mise à niveau automatique de clients de Configuration Manager. Les méthodes d’installation de clients présentées ci-dessous sont tout à fait indiquées pour mettre à niveau des logiciels clients sur les ordinateurs Windows :  

- Installation via la stratégie de groupe  

- Installation via un script d'ouverture de session  

- Installation manuelle  

- Installation de type mise à niveau  

  Si vous voulez mettre à niveau le client en employant l’une des méthodes d’installation de clients, vous trouverez plus d’informations sur l’utilisation de ces méthodes dans [Comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md).

  À partir de la version 1610, vous pouvez empêcher la mise à niveau de clients en spécifiant un groupe d’exclusion. Pour plus d’informations, consultez [Guide pratique pour empêcher la mise à niveau de clients sur les ordinateurs Windows](exclude-clients-windows.md).  


> [!TIP]  
>  Si vous mettez à niveau votre infrastructure de serveur à partir d’une version précédente de Configuration Manager \(comme Configuration Manager 2007 ou System Center 2012 Configuration Manager\), nous vous recommandons d’effectuer les mises à niveau du serveur, dont l’installation de toutes les mises à jour de Current Branch, avant la mise à niveau des clients.   La dernière mise à jour de Current Branch contenant la dernière version du client, il est préférable d’effectuer les mises à niveau des clients après avoir installé toutes les mises à jour de Configuration Manager que vous souhaitez utiliser.

> [!NOTE]
> Si vous voulez réattribuer le site pour les clients pendant la mise à niveau, vous pouvez spécifier le nouveau site à l’aide de la propriété SMSSITECODE client.msi. Si vous utilisez AUTO pour SMSSITECODE, vous devez également spécifier SITEREASSIGN=TRUE pour autoriser la réattribution automatique du site pendant la mise à niveau. Pour plus d’informations, consultez [SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode).

## <a name="use-automatic-client-upgrade"></a>Utiliser la mise à niveau automatique du client  
 Vous pouvez également configurer Configuration Manager pour mettre automatiquement à niveau le logiciel client vers la dernière version du client Configuration Manager quand Configuration Manager détecte qu’un client affecté à la hiérarchie Configuration Manager est antérieur à la version utilisée dans la hiérarchie. Ce scénario inclut la mise à niveau du client vers la dernière version quand il essaie de s’affecter à un site Configuration Manager.  

 Un client peut être mis automatiquement à niveau dans les scénarios suivants :  

-   La version du client est inférieure à la version utilisée dans la hiérarchie.  

-   Le client du site d'administration centrale dispose d'un module linguistique, mais pas le client existant.  

-   La hiérarchie impose une version différente de celle installée sur le client.  

-   Un ou plusieurs fichiers d'installation du client sont d'une version différente.  

> [!NOTE]  
>  Vous pouvez exécuter le rapport **Nombre de clients de Configuration Manager par versions de client** dans le dossier du rapport **Site - Informations client** pour identifier les différentes versions du client Configuration Manager dans votre hiérarchie.  

 Configuration Manager crée un package de mise à niveau par défaut qui est automatiquement envoyé à tous les points de distribution de la hiérarchie. Si vous apportez des modifications au package du client sur le site d’administration centrale, par exemple, en ajoutant un module linguistique client, Configuration Manager met automatiquement à jour le package et le distribue à tous les points de distribution de la hiérarchie. Si la mise à niveau automatique des clients est activée, chaque client installe automatiquement le nouveau module linguistique client.  

> [!NOTE]  
>  Configuration Manager n’envoie pas automatiquement le package de mise à niveau du client aux points de distribution cloud Configuration Manager.  

 Nous vous recommandons d’activer les mises à niveau automatiques des clients dans votre hiérarchie. De cette façon, vos clients sont mis à jour avec une surcharge administrative minimale.  

 Utilisez la procédure suivante pour configurer la mise à niveau automatique des clients. La mise à niveau automatique des clients doit être configurée sur un site d'administration centrale. Cette configuration s'applique alors à tous les clients de votre hiérarchie.  

### <a name="to-configure-automatic-client-upgrades"></a>Pour configurer les mises à niveau automatiques du client  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Sites** , cliquez sur **Paramètres de hiérarchie**.  

4.  Sous l’onglet **Mise à niveau des clients** de la boîte de dialogue **Propriétés des paramètres de hiérarchie** , examinez la version et la date du client de production et vérifiez qu’il s’agit bien de la version que vous voulez utiliser pour mettre à niveau les ordinateurs Windows.  Si ce n’est pas la version du client que vous attendiez, vous serez peut-être amené à promouvoir le client de préproduction en production. Pour plus d’informations, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md).  

5.  Cliquez sur **Mettre à niveau tous les clients de la hiérarchie en utilisant un client de production** et sur **OK** dans la boîte de dialogue de confirmation.  

6.  Si vous ne voulez pas que les mises à niveau du client s’appliquent aux serveurs, cliquez sur **Ne pas mettre à niveau les serveurs**.  

7.  Spécifiez le délai (en jours) dont disposent les ordinateurs pour mettre à niveau le client après avoir reçu la stratégie client. Le client sera mis à niveau dans un intervalle aléatoire, compris dans ce délai. Cela évite les scénarios où un grand nombre d'ordinateurs clients est mis à niveau simultanément.

    > [!NOTE]
    > Un ordinateur doit être en cours d’exécution pour mettre à niveau le client. Si un ordinateur n’est pas en cours d’exécution au moment où la réception de la mise à niveau est planifiée, cette dernière n’a pas lieu. En revanche, dès que l’ordinateur est redémarré, une autre mise à niveau est planifiée à un moment aléatoire pendant le nombre de jours autorisé. Si le redémarrage se produit alors que le délai de la mise à niveau a expiré, celle-ci est planifiée pour se produire à une heure aléatoire dans un délai de 24 heures après le redémarrage de l’ordinateur.
    >     
    > En raison de ce comportement, les ordinateurs régulièrement arrêtés en fin de journée de travail risquent d’avoir besoin de plus de temps que prévu pour se mettre à niveau si l’heure de mise à niveau planifiée de façon aléatoire ne tombe pas dans les heures de travail.

7. À compter de la version 1610, si vous ne voulez pas que des clients soient mis à niveau, cliquez sur **Exclure les clients spécifiés de la mise à niveau** et spécifiez le regroupement à exclure.

8.  Si vous souhaitez que le package d’installation du client soit copié sur des points de distribution activés pour le contenu préparé, cliquez sur **Distribuer automatiquement le package d’installation du client aux points de distribution activés pour le contenu préparé**.  

9. Cliquez sur **OK** pour enregistrer les paramètres et fermer la boîte de dialogue **Propriétés des paramètres de hiérarchie** . Les clients recevront ces paramètres lors de leur prochain téléchargement de la stratégie.

>[!NOTE]
>Les mises à niveau des clients respectent les fenêtres de maintenance Configuration Manager configurées.
