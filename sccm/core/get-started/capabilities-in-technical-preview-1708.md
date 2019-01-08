---
title: Version Technical Preview 1708
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1708 de System Center Configuration Manager.
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3c061ceb-3bdb-4d4f-8c60-344964bd416b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b751dab7ca02112959a9a7d6ed8a51b037f25b0e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422655"
---
# <a name="capabilities-in-technical-preview-1708-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1708 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1708 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problèmes connus dans cette version d’évaluation technique :**
- **La mise à jour vers la préversion 1708 échoue s’il existe un serveur de site en mode passif**. Si vous exécutez la préversion 1706 ou 1707 et que vous avez un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez le désinstaller pour pouvoir mettre à jour votre site de la préversion vers la version 1708. Vous pourrez réinstaller le serveur de site en mode passif lorsque votre site sera passé à la version 1708.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.




**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Améliorations dans la spécification des paramètres du script lorsque vous déployez des scripts PowerShell à partir de Configuration Manager
<!-- 1236459 -->

À compter de Configuration Manager 1706, vous pouvez [créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

Dans la [version d’évaluation technique 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager), nous avons étendu cette fonctionnalité pour permettre à Configuration Manager de lire les paramètres du script.

Dans cette version d’évaluation technique, nous avons étendu la fonctionnalité des paramètres de script pour identifier les paramètres obligatoires, les paramètres facultatifs (vous serez invité à les saisir).

### <a name="try-it-out"></a>Essayez !

1. Suivez les instructions dans [Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).
2. Sur la nouvelle page **Paramètres du script** de l’**Assistant Création d’un script**, choisissez un paramètre puis modifiez ses valeurs.
L’Assistant indique les paramètres obligatoires ainsi que les paramètres facultatifs.
4. Lorsque vous avez terminé la modification des paramètres, effectuez toutes les étapes de l’Assistant.

Lorsque le script s’exécute, il utilise les valeurs de paramètre que vous avez définies. Si vous n’avez pas configuré de paramètre obligatoire, l’utilisateur final sera invité à fournir ce paramètre lors de l’exécution du script.

## <a name="management-insights"></a>Management insights
<!-- 1353967 --> Vous pouvez désormais obtenir des informations sur l’état actuel de votre environnement en fonction de l’analyse des données de la base de données du site. Ces informations vous aident à mieux comprendre votre environnement et à prendre des mesures en fonction de ces renseignements. Passez en revue les informations de gestion dans la console Configuration Manager en sélectionnant **Administration** > **Management Insights** > **All Insights**. Dans cette version, les informations suivantes sont disponibles :

- **Applications sans déploiements** : répertorie les applications de votre environnement qui n’ont pas de déploiements actifs. Cette option facilite la recherche et la suppression des applications inutilisées pour simplifier la liste des applications affichées dans la console.
- **Regroupements vides** : répertorie les regroupements de votre environnement qui n’ont aucun membre. Vous pouvez supprimer ces collections pour simplifier la liste des collections affichées lors du déploiement des objets, par exemple.


## <a name="restart-computers-from-the-configuration-manager-console"></a>Redémarrer les ordinateurs à partir de la console Configuration Manager   
<!-- 1356283 --> À compter de cette version, vous pouvez utiliser la console Configuration Manager pour identifier les appareils clients qui nécessitent un redémarrage, puis utiliser une action de notification de client pour les redémarrer.

Pour identifier les périphériques en attente d’un redémarrage, sélectionnez **Ressources et Conformité** > **Périphériques** puis choisissez une collection de périphériques pouvant nécessiter un redémarrage. Après avoir sélectionné une collection, vous pouvez afficher l’état de chaque périphérique dans le volet des détails d’une nouvelle colonne nommée **Redémarrage en attente**. Chaque périphérique affiche la valeur **Yes** ou **No**.

Pour créer la notification invitant le client à redémarrer un périphérique :
1.  Recherchez le périphérique que vous souhaitez redémarrer dans le nœud Périphériques de la console.
2.  Cliquez avec le bouton droit sur le périphérique, sélectionnez **Notification du client**, puis **Redémarrer**. Une fenêtre s’ouvre et affiche des informations concernant le redémarrage. Cliquez sur **OK** pour confirmer la demande de redémarrage.

Lorsqu’un client reçoit la notification, une fenêtre de notification **Centre logiciel** s’ouvre et pour informer l’utilisateur du redémarrage. Par défaut, le redémarrage se produit après 90 minutes. Vous pouvez modifier le délai de redémarrage en configurant les [paramètres du client](/sccm/core/clients/deploy/configure-client-settings). Les paramètres qui définissent le comportement du redémarrage se trouvent dans l’onglet [Redémarrage de l’ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-restart) des paramètres par défaut.


### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches suivantes, puis envoyez-nous vos **Commentaires** à partir de l’onglet **Accueil** du ruban pour nous dire comment cela a fonctionné pour vous :
1.  Déployez une application ou mettez à jour un périphérique qui obligera ce périphérique à redémarrer pour terminer l’installation.
2.  Recherchez le périphérique dans le nœud **Ressources et Conformité** > **Périphériques** de la console puis vérifiez que ce périphérique affiche **Oui** dans la colonne **Redémarrage en attente**. Un délai de 20 minutes peut s’écouler avant que l’état Redémarrage en attente apparaisse dans la console.
3.  Surveillez le périphérique pour confirmer que la notification du Centre logiciel s’affiche et que le périphérique redémarre correctement.


## <a name="software-center-customization"></a>Personnalisation du Centre logiciel
<!-- 1351224 --> Vous pouvez ajouter des éléments de personnalisation d’entreprise et spécifier la visibilité des onglets du Centre logiciel. Vous pouvez ajouter votre nom de société Centre logiciel spécifique, définir un modèle de couleurs de configuration Centre logiciel, un logo de société et les onglets visibles pour les périphériques clients.

### <a name="customize-software-center"></a>Personnaliser le Centre logiciel

Pour modifier le Centre logiciel :

1. Dans la console **Configuration Manager**, choisissez  **Administration** > **Paramètres client**. Cliquez sur l’instance de paramètre de client souhaitée.
2. Sur l’onglet  **Accueil** , dans le groupe  **Propriétés** , choisissez  **Propriétés**.
3. Dans la boîte de dialogue  **Paramètres par défaut** , choisissez  **Centre logiciel**.
4. Sélectionnez **Oui** pour **sélectionner de nouveaux paramètres afin de spécifier les informations de l’entreprise** et permettre la modification des paramètres de personnalisation du Centre logiciel.
5. Spécifiez le **nom de votre entreprise**.
6. Sélectionnez votre **modèle de couleurs pour le Centre logiciel**.
7. Cliquez sur **Parcourir** pour sélectionner votre logo pour le Centre logiciel. Le logo doit être de type JPEG ou PNG et au format 400 x 100 pixels, avec une taille maximale de 750 Ko.
8. Sélectionnez **OUI** pour afficher les onglets dans le Centre logiciel pour les périphériques clients. Au moins un onglet doit être visible :

    -  Activer l’onglet Applications
    -  Activer l’onglet Mises à jour
    -  Activer l’onglet Systèmes d'exploitation
    -  Activer l’onglet État de l’installation
    -  Activer l’onglet Conformité de l’appareil
    -  Activer l’onglet Options

### <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur la gestion d’applications dans Configuration Manager, consultez [Présentation de la gestion d’applications dans System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management).
