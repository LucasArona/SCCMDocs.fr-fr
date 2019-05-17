---
title: Gérer la synchronisation des mises à jour logicielles
titleSuffix: Configuration Manager
description: Exécutez ces étapes pour planifier, démarrer manuellement et surveiller la synchronisation des mises à jour logicielles.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4ef815287321bf6c5554ff424da58276af0cc655
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493932"
---
#  <a name="BKMK_SUMSync"></a> Synchroniser les mises à jour logicielles

*S’applique à : System Center Configuration Manager (Current Branch)*

 La synchronisation des mises à jour logicielles dans Configuration Manager consiste à récupérer les métadonnées des mises à jour logicielles correspondant aux critères que vous configurez, comme les produits, les classifications et les langues. En règle générale, les métadonnées sont récupérées par le point de mise à jour logicielle du site d’administration centrale ou d’un site principal autonome auprès de Microsoft Update. Ensuite, le site de niveau supérieur envoie une demande de synchronisation aux autres sites. Quand un site reçoit la demande de synchronisation du site parent, le point de mise à jour logicielle du site récupère les métadonnées des mises à jour logicielles à partir de sa [source de synchronisation](../plan-design/plan-for-software-updates.md#BKMK_SyncSource) en amont. Pour plus d’informations sur la synchronisation des mises à jour logicielles, consultez [Synchronisation des mises à jour logicielles](../understand/software-updates-introduction.md#BKMK_Synchronization).

Vous configurez la synchronisation des mises à jour logicielles de sorte qu’elle s’exécute selon une planification dans les propriétés du point de mise à jour logicielle sur le site de niveau supérieur. Lorsque vous avez configuré le calendrier de synchronisation, vous ne modifiez généralement pas le calendrier dans le cadre des opérations normales. Toutefois, vous pouvez lancer manuellement la synchronisation des mises à jour logicielles au besoin.

  > [!NOTE]  
  >  Les points de mise à jour logicielle doivent être connectés à leur source de synchronisation en amont pour synchroniser les mises à jour logicielles. Quand un point de mise à jour logicielle est déconnecté de sa source de synchronisation en amont, vous pouvez utiliser la méthode d'exportation et importation pour synchroniser les mises à jour logicielles. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles à partir d’un point de mise à jour logicielle déconnecté](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Planifier la synchronisation des mises à jour logicielles
Quand vous configurez une planification pour la synchronisation des mises à jour logicielles, le point de mise à jour logicielle de niveau supérieur lance la synchronisation auprès de Microsoft Update à la date et à l’heure prévues. La planification personnalisée vous permet de synchroniser les mises à jour logicielles à une date et une heure où les demandes du serveur Windows Server Update Services (WSUS), du serveur de site et du réseau sont faibles. Par exemple, vous pouvez définir une planification qui prévoie une synchronisation des mises à jour logicielles toutes les semaines à 2h00. Pendant la synchronisation planifiée, toutes les modifications apportées aux métadonnées de mise à jour logicielle depuis la dernière synchronisation planifiée sont insérées dans la base de données de site. Cela inclut les nouvelles métadonnées de mise à jour logicielle ou les métadonnées qui ont été modifiées, supprimées ou qui sont désormais expirées.

Utilisez les procédures suivantes sur le site de niveau supérieur pour planifier la synchronisation des mises à jour logicielles.  

#### <a name="to-schedule-software-updates-synchronization"></a>Pour planifier la synchronisation des mises à jour logicielles  

  1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

  2.  Dans l'espace de travail Administration, développez **Configuration du site**, puis cliquez sur **Sites**.  

  3.  Dans le volet des résultats, cliquez sur le site d'administration centrale ou le site principal autonome.  

  4.  Sur l'onglet **Accueil** dans le groupe **Paramètres** , développez **Configurer les composants de site**, puis cliquez sur **Point de mise à jour logicielle**.  

  5.  Dans la boîte de dialogue Propriétés du composant du point de mise à jour logicielle, sélectionnez **Activer la synchronisation dans un calendrier**, puis spécifiez le calendrier de synchronisation.  

## <a name="manually-start-software-updates-synchronization"></a>Démarrer manuellement la synchronisation des mises à jour logicielles
Vous pouvez lancer manuellement la synchronisation des mises à jour logicielles sur le site de niveau supérieur dans la console Configuration Manager à partir du nœud **Toutes les mises à jour logicielles** dans l’espace de travail **Bibliothèque de logiciels**.  

Utilisez les procédures suivantes sur le site de niveau supérieur pour lancer manuellement la synchronisation des mises à jour logicielles.  

#### <a name="to-manually-start-software-updates-synchronization"></a>Pour démarrer manuellement la synchronisation des mises à jour logicielles  

1. Dans la console Configuration Manager, qui est connectée au site d’administration centrale ou au site principal autonome, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail Bibliothèque de logiciels, développez **Mises à jour logicielles** , puis cliquez sur **Toutes les mises à jour logicielles** ou **Groupes de mises à jour logicielles**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Synchroniser les mises à jour logicielles**. Cliquez sur **Oui** dans la boîte de dialogue pour confirmer le lancement du processus de synchronisation.  

   Une fois que vous avez lancé le processus de synchronisation sur le point de mise à jour logicielle, vous pouvez surveiller le processus de synchronisation à partir de la console Configuration Manager pour tous les points de mise à jour logicielle de votre hiérarchie. Pour surveiller le processus de synchronisation des mises à jour logicielles, procédez comme suit.  


## <a name="monitor-software-updates-synchronization"></a>Surveiller la synchronisation des mises à jour logicielles
Après avoir lancé le processus de synchronisation, vous pouvez le surveiller à partir de la console Configuration Manager pour tous les points de mise à jour logicielle de votre hiérarchie. Pour surveiller le processus de synchronisation des mises à jour logicielles, procédez comme suit. Pour plus d’informations sur la surveillance des mises à jour logicielles, notamment du processus de synchronisation, consultez [Surveiller les mises à jour logicielles](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Pour surveiller le processus de synchronisation des mises à jour logicielles  

1. Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2. Dans l'espace de travail **Surveillance** , cliquez sur **État de la synchronisation du point de mise à jour logicielle**.  

   Les points de mise à jour logicielle de votre hiérarchie Configuration Manager sont affichés dans le volet résultats. Dans cette vue, vous pouvez surveiller l'état de synchronisation pour tous les points de mise à jour logicielle. Si vous souhaitez des informations plus détaillées sur le processus de synchronisation, vous pouvez examiner le fichier wsyncmgr.log qui se trouve dans le dossier <*chemin_installation_ConfigMgr*>\Logs sur chaque serveur de site.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importer des mises à jour à partir du catalogue Microsoft Update

Le point de mise à jour logicielle de niveau supérieur utilise WSUS pour obtenir des informations sur les mises à jour logicielles de Microsoft Configuration Manager. Vous aurez peut-être parfois besoin d’une mise à jour qui ne se synchronise pas automatiquement dans WSUS pour vos produits et classifications sélectionnés, mais qui est disponible dans le [catalogue Microsoft Update](https://catalog.update.microsoft.com). Les mises à jour qui ne se synchronisent automatiquement dans WSUS sont généralement destinées à résoudre des problèmes très spécifiques. Généralement, si une mise à jour est disponible dans le catalogue, vous pouvez l’importer dans WSUS. Vous pouvez ensuite la synchroniser dans Configuration Manager et la déployer comme toute autre mise à jour.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>Pour importer une mise à jour à partir du catalogue Microsoft Update

1. Ouvrez la console d’administration WSUS et connectez-la au serveur WSUS de niveau supérieur dans votre hiérarchie SCCM. 
   - Si Internet Explorer n’est pas le navigateur web par défaut de l’ordinateur, définissez-le temporairement comme valeur par défaut.
2. Cliquez sur **Mises à jour** ou cliquez sur le nom de votre serveur WSUS. 
3. Dans le volet **Actions**, sélectionnez **Importer des mises à jour...** . Une fenêtre de navigateur pour le [catalogue Microsoft Update](https://catalog.update.microsoft.com) s’affiche.
   ![Sélectionner Importer des mises à jour dans la console WSUS](media/wsus-console-import-updates.png)
4. Si vous y êtes invité, installez le contrôle ActiveX du catalogue Microsoft Update. Le contrôle doit être installé pour importer des mises à jour dans WSUS. 
5. Dans la fenêtre du navigateur, recherchez la mise à jour souhaitée. Cliquez sur le bouton **Ajouter*** pour l’ajouter au panier.
6. Cliquez sur **Afficher le panier**. Vérifiez que l’option pour **importer directement dans Windows Server Update Services** est sélectionnée. Cliquez ensuite sur **Importer**.
    ![Importer une mise à jour du catalogue dans WSUS](./media/import-catalog-update-into-wsus.png)
7. Une fois l’importation terminée, cliquez sur **Fermer** sur la fenêtre du navigateur.
     - Réinitialisez votre navigateur par défaut si nécessaire.
8. Synchronisez votre point de mise à jour logicielle Configuration Manager.


## <a name="next-steps"></a>Étapes suivantes
À l’issue de la première synchronisation de mises à jour logicielles ou après la mise à disposition de nouvelles classifications ou de nouveaux produits, vous devez [configurer les nouvelles classifications et les nouveaux produits](configure-classifications-and-products.md) pour synchroniser les mises à jour logicielles avec les nouveaux critères.

Après avoir synchronisé les mises à jour logicielles avec les critères dont vous avez besoin, [gérez les paramètres des mises à jour logicielles](manage-settings-for-software-updates.md).  
