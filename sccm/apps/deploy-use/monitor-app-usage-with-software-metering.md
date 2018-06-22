---
title: Surveiller l’utilisation des applications avec le contrôle de logiciel
titleSuffix: Configuration Manager
description: Découvrez les opérations qui sont disponibles dans le contrôle de logiciel System Center Configuration Manager.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 66099b45fb04b18c84cd9a3973c1a4d93f0e93a6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335760"
---
# <a name="software-metering-in-system-center-configuration-manager"></a>Contrôle de logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient une référence pour toutes les opérations que vous pouvez effectuer lors de l’utilisation du contrôle de logiciel System Center Configuration Manager.

> [!IMPORTANT]
>  Le contrôle de logiciel est utilisé pour surveiller les applications de bureau des PC Windows avec un nom de fichier se terminant par **.exe**. Le contrôle de logiciel ne surveille pas les applications Windows modernes (telles que celles utilisées par Windows 8).

##  <a name="prerequisites-for-software-metering"></a>Configuration requise pour le contrôle de logiciel
Le contrôle de logiciel ne présente aucune dépendance externe, seulement des dépendances au sein du produit.

|Dépendance|Plus d'informations|
|----------------|----------------------|
|Paramètres client pour le contrôle de logiciel|Pour utiliser le contrôle de logiciel, le paramètre client **Activer le contrôle de logiciel sur les clients** doit être activé et déployé sur les ordinateurs. Vous pouvez déployer les paramètres de contrôle de logiciel sur tous les ordinateurs de la hiérarchie ou déployer les paramètres personnalisés sur des groupes d’ordinateurs. Consultez **Configurer le contrôle de logiciel** dans cette rubrique.|
|Point de Reporting Services|Vous devez configurer un point de Reporting Services pour pouvoir afficher les rapports de contrôle de logiciel. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).|

##  <a name="configure-software-metering"></a>Configurer le contrôle de logiciel
 Cette procédure configure les paramètres client par défaut pour le contrôle de logiciel et s’applique à tous les ordinateurs de votre hiérarchie. Si vous souhaitez que ces paramètres s’appliquent uniquement à certains ordinateurs, créez un paramètre client de périphérique personnalisé et déployez-le sur un regroupement contenant les ordinateurs sur lesquels vous souhaitez utiliser le contrôle de logiciel. Pour plus d’informations sur la création de paramètres d’appareil personnalisé, consultez [Configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client** > **Paramètres client par défaut**.

2.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.

3.  Dans la boîte de dialogue **Paramètres par défaut** , cliquez sur **Contrôle de logiciel**.

4.  Dans la liste **Paramètres de périphérique** , configurez les éléments suivants :

    -   **Activer le contrôle de logiciel sur les clients**: sélectionnez **Vrai** pour activer le contrôle de logiciel.

    -   **Planifier le regroupement de données**: configurez la fréquence à laquelle les données de contrôle de logiciel doivent être collectées à partir des ordinateurs clients. Utilisez la valeur par défaut, à savoir tous les **7 jours** ou cliquez sur **Calendrier** pour spécifier une planification personnalisée.

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres par défaut** .

 Les ordinateurs clients sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie du client. Pour lancer la récupération de stratégie pour un seul client, consultez [Gérer les clients](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a>Créer des règles de contrôle de logiciel
 Utilisez l’Assistant Créer une règle de contrôle de logiciel pour créer une règle de contrôle de logiciel pour votre site Configuration Manager.

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Contrôle de logiciel**.

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une règle de contrôle de logiciel**.

4.  Dans la page **Général** de l’Assistant Créer une règle de contrôle de logiciel, spécifiez les informations suivantes :

    -   **Nom** : nom de la règle de contrôle de logiciel. Ce nom doit être unique et descriptif.

        > [!NOTE]
        >  Des règles de contrôle de logiciel peuvent partager le même nom si le nom de fichier contenu dans les règles est différent.

    -   **Nom du fichier** : nom du fichier programme que vous voulez contrôler. Vous pouvez cliquer sur **Parcourir** pour afficher la boîte de dialogue **Ouvrir** , dans laquelle vous pouvez sélectionner le fichier programme à utiliser.

        > [!NOTE]
        >  Si vous tapez le nom du fichier exécutable dans la zone **Nom du fichier** , aucune vérification n’est effectuée pour déterminer si ce fichier existe ou s’il contient les informations d’en-tête nécessaires. Quand cela est possible, cliquez sur **Parcourir** et sélectionnez le fichier exécutable à contrôler.
        >
        >  Le nom du fichier ne doit pas contenir de caractères génériques.
        >
        >  Cette zone est facultative si une valeur est spécifiée pour **Nom du fichier d’origine** .

    -   **Nom du fichier d’origine** : nom du fichier exécutable que vous voulez contrôler. Ce nom correspond aux informations figurant dans l’en-tête du fichier et non pas au nom de fichier proprement dit. Cela peut être utile si le fichier exécutable a été renommé mais que vous voulez le contrôler par son nom d’origine.

        > [!NOTE]
        >  Le nom du fichier d'origine ne doit pas contenir de caractères génériques.
        >
        >  Cette zone est facultative si une valeur est spécifiée pour **Nom du fichier** .

    -   **Version** : version du fichier exécutable que vous voulez contrôler. Vous pouvez utiliser le caractère générique ( &#42; ) pour représenter toute chaîne de caractères, ou le caractère générique ( ? ) pour représenter tout caractère unique. Si vous voulez effectuer l’analyse de toutes les versions d’un fichier exécutable, utilisez la valeur par défaut ( &#42; ).

    -   **Langue** : langue du fichier exécutable à contrôler. La valeur par défaut est le paramètre régional actuel du système d'exploitation que vous utilisez. Si vous sélectionnez un fichier exécutable à contrôler en cliquant sur le bouton **Parcourir** , cette zone est automatiquement remplie si les informations sur la langue sont présentes dans l’en-tête du fichier. Pour contrôler toutes les versions linguistiques d’un fichier, sélectionnez **N’importe laquelle** dans la liste déroulante.

    -   **Description** : description facultative de la règle de contrôle de logiciel.

    -   **Appliquez cette règle de contrôle de logiciel aux clients suivants** : choisissez d’appliquer ou non la règle de contrôle de logiciel à tous les clients de la hiérarchie ou aux clients affectés au site spécifié dans la liste **Site** .

5.  Pour continuer, cliquez sur **Suivant**.

6.  Passez en revue et confirmez ces paramètres, puis terminez l’Assistant pour créer la règle de contrôle de logiciel. La nouvelle règle de contrôle de logiciel s’affiche dans le nœud **Contrôle de logiciel** de l’espace de travail **Ressources et Conformité** .

##  <a name="configure-automatic-software-metering-rules"></a>Configurer les règles de contrôle de logiciel automatiques
 Configuration Manager permet de configurer le contrôle de logiciel pour générer automatiquement des règles désactivées de contrôle de logiciel à partir des données d’inventaire d’utilisation récente dans la base de données de site. Vous pouvez configurer ces données d’inventaire afin de créer des règles de contrôle uniquement pour les applications utilisées sur un pourcentage spécifié d’ordinateurs. Vous pouvez également définir le nombre maximal de règles de contrôle de logiciel automatiquement générées autorisées sur le site.

> [!NOTE]
>  Par défaut, les règles de contrôle de logiciel qui sont créées automatiquement sont désactivées. Pour pouvoir collecter les données d'utilisation à partir de ces règles, vous devez les activer.

1.  Dans la console Configuration Manager, cliquez sur **Actifs et conformité** > **Contrôle de logiciel**, puis, dans l’onglet **Accueil**, dans le groupe **Paramètres**, cliquez sur **Propriétés de contrôle de logiciel**.

3.  Dans la boîte de dialogue **Propriétés de contrôle de logiciel** , définissez les éléments suivants :

    -   **Conservation des données (en jours)** : indique la durée de conservation des données générées par les règles de contrôle de logiciel dans la base de données du site. La valeur par défaut est **90** jours.

    -   Activez l'option **Créer automatiquement des règles de contrôle désactivées à partir des données d'inventaire récemment utilisées**.

    -   **Spécifier le pourcentage d'ordinateurs de la hiérarchie qui doivent utiliser un programme avant qu'une règle de contrôle de logiciel soit créée automatiquement** : la valeur par défaut est **10** pour cent.

    -   **Spécifier le nombre de règles de contrôle de logiciel devant être dépassées dans la hiérarchie avant que la création automatique de règles soit désactivée** : la valeur par défaut est **100** règles.

4.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de contrôle de logiciel** .

##  <a name="manage-software-metering-rules"></a>Gérer les règles de contrôle de logiciel
 Dans l'espace de travail **Biens et conformité** , sélectionnez **Contrôle de logiciel**, puis la règle de contrôle de logiciel à gérer, et enfin sélectionnez une tâche de gestion.

 Utilisez le tableau suivant pour obtenir plus d'informations sur les tâches de gestion qui pourraient nécessiter certaines informations avant de les sélectionner.

|Tâche de gestion|Détails|
|---------------------|-------------|
|**Activer**<br /><br /> **Désactiver**|Active ou désactive une règle de contrôle de logiciel. Ce paramètre est téléchargé vers des ordinateurs client en fonction de l' **Intervalle d'interrogation de la stratégie client** dans la section **Stratégie client** des paramètres client (par défaut, toutes les 60 minutes).<br /><br /> Consultez [Configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).|

##  <a name="monitor-software-metering"></a>Surveiller le contrôle de logiciel
 Le contrôle de logiciel dans Configuration Manager inclut un certain nombre de rapports intégrés qui vous permettent de surveiller les informations concernant les opérations de contrôle de logiciel. Ces rapports affiche la catégorie de rapport de **contrôle des logiciels**.

 Pour plus d’informations sur la configuration de la génération de rapports dans Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).

 En outre, vous pouvez créer des requêtes et des regroupements à partir des données stockées dans la base de données Configuration Manager par le contrôle de logiciel.

 Pour plus d’informations sur les regroupements dans Configuration Manager, consultez [Présentation des regroupements](/sccm/core/clients/manage/collections/introduction-to-collections).

 Pour plus d’informations sur les requêtes dans Configuration Manager, consultez [Présentation des requêtes](/sccm/core/servers/manage/introduction-to-queries).

##  <a name="security-and-privacy-for-software-metering"></a>Sécurité et confidentialité pour le contrôle de logiciel

### <a name="security-issues-for-software-metering"></a>Problèmes de sécurité pour le contrôle de logiciel
 Une personne malveillante pourrait envoyer des informations de contrôle de logiciel non valides à Configuration Manager, qui seraient acceptées par le point de gestion même lorsque le paramètre du client de contrôle de logiciel est désactivé. Ceci peut entraîner la réplication d’un grand nombre de règles de contrôle dans toute la hiérarchie, provoquant ainsi un déni de service sur le réseau et aux serveurs de site Configuration Manager.

 Dans la mesure où une personne malveillante peut créer des données de contrôle de logiciel non valides, ne considérez pas que les informations de contrôle de logiciel font autorité.

 Le contrôle de logiciel est activé par défaut comme un paramètre du client.

###  <a name="privacy-information-for-software-metering"></a>Informations de confidentialité pour le contrôle de logiciel
 Le contrôle de logiciel surveille l'utilisation des applications sur les ordinateurs client. Le contrôle de logiciel est activé par défaut. Vous devez configurer les applications à contrôler. Les informations de contrôle sont stockées dans la base de données Configuration Manager. Ces informations sont chiffrées au cours du transfert vers un point de gestion, mais elles ne sont pas stockées sous forme chiffrée dans la base de données Configuration Manager.

 Ces informations sont conservées dans la base de données jusqu'à leur suppression par les tâches de maintenance de site **Supprimer les données de contrôle de logiciel anciennes** (tous les cinq jours) et **Supprimer les données de résumé de contrôle de logiciel anciennes** (tous les 270 jours). Vous pouvez configurer l'intervalle de suppression. Les informations de contrôle ne sont pas envoyées à Microsoft.

 Avant de configurer le contrôle de logiciel, réfléchissez à vos besoins en matière de confidentialité.

## <a name="example-scenario-for-using-software-metering"></a>Exemple de scénario d’utilisation du contrôle de logiciel
 Dans cette section, vous allez créer un exemple de règle de contrôle de logiciel qui peut vous aider à répondre aux exigences métier suivantes :

-   Déterminer le nombre de copies d’une application particulière dans votre entreprise

-   Découvrir les copies inutilisées d’une application

-   Déterminer les personnes qui utilisent régulièrement une application particulière

 La Woodgrove Bank a déployé Microsoft Office 2010 comme suite de production standard. Toutefois, pour prendre en charge une application héritée, certains ordinateurs doivent continuer à exécuter Microsoft Office Word 2003. Le service informatique souhaite réduire les coûts de support et de licences en supprimant ces copies de Word 2003 si l’application héritée n’est plus utilisée. Le support technique souhaite également identifier les personnes qui utilisent l’application héritée.

 Responsable des systèmes informatiques de la Woodgrove Bank, John utilise le contrôle de logiciel dans Configuration Manager pour atteindre ces objectifs métier. Il effectue les opérations suivantes :

- John vérifie la configuration requise pour le contrôle de logiciel et confirme que le point de Reporting Services est installé et opérationnel.
- John configure les paramètres client par défaut pour le contrôle de logiciel :<br>Il active le contrôle de logiciel et, par défaut, planifie le regroupement de données à raison d’une collecte tous les sept jours.<br>Il configure l’inventaire logiciel pour inventorier les fichiers portant l’extension .exe en paramétrant le paramètre client d’inventaire logiciel **Inventorier ces types de fichiers**.<br>Il ajoute une nouvelle règle de contrôle des logiciels, nommée **woodgrove.exe**, afin de surveiller l’application héritée.
- John attend pendant sept jours, au bout desquels les ordinateurs clients commencent à signaler les données d’utilisation pour le fichier exécutable **woodgrove.exe** .
- John utilise le rapport **Base d’installation pour tous les logiciels contrôlés** de Configuration Manager pour voir les ordinateurs sur lesquels l’application **woodgrove.exe** est chargée.
- Après six mois, John exécute le rapport **Ordinateurs sur lesquels un programme contrôlé est installé, mais n'ayant pas exécuté le programme depuis la date spécifiée**, en spécifiant la règle de contrôle des logiciels et une date de six mois en arrière. Ce rapport identifie 120 ordinateurs qui n’ont pas exécuté le programme au cours des six derniers mois.
- John effectue des vérifications supplémentaires pour s’assurer que l’application héritée n’est pas nécessaire sur les ordinateurs identifiés. Ensuite, il désinstalle l’application héritée et la copie de Word 2003 de ces ordinateurs.<br>John exécute le rapport **Utilisateurs ayant exécuté un programme contrôlé spécifique** pour fournir au support technique la liste des utilisateurs qui continuent d’utiliser l’application héritée.
- John continue de vérifier les rapports de contrôle de logiciel chaque semaine et prend des mesures correctives quand cela est nécessaire.

 À la suite de cette action, les coûts de support et de licences sont réduits en supprimant les applications qui ne sont plus nécessaires. En outre, le support technique possède maintenant la liste souhaitée des utilisateurs qui exécutent l’application héritée.
