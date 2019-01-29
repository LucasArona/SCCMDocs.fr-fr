---
title: Gérer des publications
titleSuffix: Configuration Manager
description: Gérer des groupes de mises à jour logicielles comme une publication avec l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f626d07d1fe25d8277ab2189f136862079dc503c
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896622"
---
# <a name="manage-publications-in-updates-publisher"></a>Gérer des publications dans l’éditeur de mises à jour

*S’applique à : System Center Updates Publisher*

Vous pouvez utiliser des publications pour gérer des offres groupées de mises à jour comme un seul objet. Cela inclut la publication des mises à jour sur un serveur d’administration et l’exportation de la publication en tant que groupe pour une utilisation avec une autre installation de l’éditeur de mise à jour.

## <a name="create-publications"></a>Créer des publications
Les publications sont créées de deux façons :

-   Lorsque vous gérez des mises à jour et des offres groupées dans l **’espace de travail Mises à jour**, vous pouvez leur [affecter](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) une nouvelle publication créée à ce moment-là.

-   Dans l **’espace de travail Publications,** vous pouvez utiliser le bouton **créer** de l’onglet **Publication** du ruban. Cette méthode vous permet de créer une publication pour une utilisation ultérieure. Plus tard, lorsque vous affectez des mises à jour, vous pouvez alors utiliser cette publication.

## <a name="rename-a-publication"></a>Renommer une publication
Pour renommer une publication, sélectionnez la publication dans l **’espace de travail Publications**, puis, dans l’onglet **Publication** du ruban, choisissez **Modifier**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Modifier le type de publication de mises à jour dans une publication
Dans l **’espace de travail Publications**, vous pouvez modifier le **type de publication** de mises à jour et d’offres groupées affectées à une publication.

1. Sélectionnez la publication contenant les mises à jour que vous souhaitez modifier, puis sélectionnez une ou plusieurs mises à jour ou offres groupées dans la liste **Tous &lt;nom de la publication > mises à jour de membre**.

2. Puis, dans l'onglet **Accueil**, choisissez l’une des options suivantes. Les options disponibles dépendent du type de publication des mises à jour que vous avez sélectionné.

   -   **Automatique**
   -   **Tout le contenu**
   -   **Métadonnées uniquement**

Après avoir apporté une modification, vous devrez peut-être actualiser l’affichage de la publication pour voir les nouvelles valeurs.

Pour plus d’informations sur les différents types de publication, consultez [Affecter des mises à jour et des offres groupées à une publication](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication).

> [!TIP]    
> Lorsque vous définissez le type de publication d’une offre groupée, toutes les mises à jour logicielles de cette offre groupée sont publiées avec son type de publication.

## <a name="remove-updates-from-a-publication"></a>Supprimer des mises à jour d’une publication
Pour supprimer des mises à jour ou des offres groupées d’une publication, dans l **’espace de travail Publications** sélectionnez la publication à modifier, puis choisissez les mises à jour et les offres groupées à supprimer. Ensuite, dans l’onglet **Accueil** du ruban, choisissez **Supprimer**.

Lorsque des mises à jour sont supprimées d’une publication, elles restent disponibles dans le référentiel de l’éditeur de mise à jour.

## <a name="publish-publications"></a>Publier des publications
Lorsque vous publiez des mises à jour et des offres groupées, l’éditeur de mise à jour ajoute des informations sur ces mises à jour et offres (métadonnées) et éventuellement les fichiers binaires des mises à jour (tout le contenu) à un serveur de mise à jour pour le déploiement sur des appareils.

Avant de pouvoir publier une mise à jour, vous devez configurer l’option [Serveur de mise à jour](/sccm/sum/tools/updates-publisher-options#update-server) de l’éditeur de mise à jour. Pour ouvrir cette option de configuration, accédez à l **’espace de travail Mises à jour** &gt; **Vue d’ensemble** et sélectionnez **Configurer WSUS et le certificat de signature.** Vous pouvez également accéder à la page Serveur de mise à jour dans les options de l’éditeur de mise à jour.

> [!NOTE]   
> Le serveur de mise à jour peut uniquement publier des mises à jour d’une taille maximale de 375 mégaoctets (Mo).

### <a name="to-publish-a-publication"></a>Pour publier une publication

1. Accédez à l **’espace de travail Publications**, puis sélectionnez une publication contenant le groupe de mises à jour et les offres groupées que vous souhaitez publier ou exporter. Puis choisissez **Publier** dans l’onglet **Accueil** du ruban.

2. Sur la page **Sélectionner** de l’Assistant **Publication**, vous pouvez choisir de signer toutes les mises à jour avec un nouveau certificat de publication, mais vous ne pouvez pas modifier le type de publication.

3. Effectuez toutes les étapes de l'Assistant.

   Si la publication échoue, vous recevez un lien vers le fichier UpdatesPublisher.log apparaît qui peut fournir plus d’informations.

## <a name="export-a-publication"></a>Exporter une publication
Vous pouvez exporter une publication à partir du référentiel de l’éditeur de mise à jour. Cette opération exporte les mises à jour et les offres groupées affectées à cette publication et crée un catalogue de mises à jour. Vous pouvez ensuite [ajouter](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) puis [importer](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) ce catalogue vers une autre instance de l’éditeur de mise à jour. Vous pouvez également [exporter les mises à jour](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) qui ne font pas partie d’une publication.

Pour exporter une publication, accédez à l **’espace de travail Publications** et sélectionnez la publication contenant les mises à jour que vous souhaitez exporter. Vous ne pouvez sélectionner qu’une publication à la fois.

Une fois la publication sélectionnée, choisissez **Exporter** dans l’onglet **Accueil** du ruban, puis indiquez un chemin d’accès et un nom de fichier pour l’exportation du catalogue.

Vous avez également la possibilité d’exporter (inclure) des mises à jour de logiciels dépendantes lors de l’exportation.

## <a name="rename-a-publication"></a>Renommer une publication
Pour renommer une publication, sélectionnez la publication dans l **’espace de travail Publications**, puis choisissez **Modifier** dans l’onglet **Publication** du ruban.

## <a name="delete-a-publication"></a>Supprimer une publication
Pour supprimer une publication, sélectionnez la publication dans l **’espace de travail Publications**, puis choisissez **Supprimer** dans l’onglet **Publication** du ruban.

Une fois la publication supprimée de l’éditeur de mise à jour, les mises à jour de cette publication restent disponibles dans le référentiel de l’éditeur de mise à jour.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Faire expirer ou réactiver des mises à jour et des offres groupées
Vous pouvez utiliser l **’espace de travail Mises à jour** pour sélectionner puis faire expirer ou réactiver des mises à jour et des offres groupées. Vous pouvez faire expirer et réactiver des mises à jour et des offres groupées autant de fois que vous le souhaitez.

-   **Pour faire expirer des mises à jour ou des offres groupées**, dans l’espace de travail Mises à jour, sélectionnez une ou plusieurs mises à jour ou offres groupées qui n’ont pas expiré, puis choisissez **Expirer** dans l’onglet **Accueil**. Tant que vous n’avez pas publié la mise à jour ou l’offre groupée dans l’éditeur de mise à jour pour la faire expirer, vous pouvez les réactiver.

    Avant de pouvoir supprimer une mise à jour ou une offre groupée personnalisée de Configuration Manager, vous devez la faire expirer puis publier ce statut expiré dans Configuration Manager. Une fois les mises à jour ou les offres groupées arrivées à expiration dans Configuration Manager, vous ne pouvez plus déployer ou réactiver la mise à jour ou l’offre groupée.

-   **Pour réactiver des mises à jour ou des offres groupées**, dans l’espace de travail Mises à jour, sélectionnez une ou plusieurs mises à jour qui ont expiré, puis choisissez **Réactiver** dans l’onglet **Accueil** du ruban. Si la mise à jour expirée a été précédemment publiée comme ayant expiré dans Configuration Manager, vous ne pouvez pas la réactiver.
