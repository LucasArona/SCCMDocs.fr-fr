---
title: Gérer des catalogues de mises à jour
titleSuffix: Configuration Manager
description: Gérer des catalogues de mises à jour logicielles pour l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 887f8029-1a3a-423c-a9c1-31dc0d693386
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 03c325f2bd6aa6ea6c39d7994a78b900653e62a1
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415434"
---
# <a name="manage-software-update-catalogs-in-updates-publisher"></a>Gérer des catalogues de mises à jour logicielles dans l’éditeur de mise à jour

*S’applique à : System Center Updates Publisher*

Utilisez l’**espace de travail** **Catalogues** pour gérer les catalogues de mises à jour logicielles. Cela inclut l’ajout de nouveaux catalogues, la gestion d’abonnements à des catalogues existants et l’importation d’informations sur les mises à jour d’un catalogue vers le référentiel de l’éditeur de mise à jour.

Les catalogues de mises à jour logicielles contiennent des informations sur les mises à jour créées par des organisations autres que Microsoft. Ces autres organisations incluent votre propre organisation et les fournisseurs de logiciels tiers qui ont inscrit leurs catalogues auprès de Microsoft. Les catalogues inscrits par des fournisseurs de logiciels sont appelés *catalogues partenaires*. Les catalogues que vous créez et qui ne sont pas inscrits auprès de Microsoft sont appelés catalogues *utilisateur*.

## <a name="add-software-update-catalogs"></a>Ajouter des catalogues de mises à jour logicielles
Vous devez ajouter un catalogue de mises à jour à l’éditeur de mise à jour avant de pouvoir gérer les mises à jour qu’il contient. Lorsque vous ajoutez un catalogue, l’éditeur de mise à jour :
-   Crée un abonnement à ce catalogue afin de pouvoir vérifier les mises à jour de ce catalogue.
-   Ajoute le catalogue à une liste dans la fenêtre **Mes catalogues de mises à jour logiciels** de l **’espace de travail Catalogues**.  

Vous trouverez dans la console des informations sur chaque catalogue auquel vous êtes abonné. Ces Informations incluent l’URL ou l’emplacement de téléchargement, le nom de la société ou de l’organisation qui a créé le catalogue, et la date de la dernière importation ou modification.

À chaque démarrage, l’éditeur de mise à jour peut vérifier automatiquement les modifications apportées aux abonnements. Ce paramètre est configuré comme une [option avancée](/sccm/sum/tools/updates-publisher-options#advanced). Dans ce cas, l’éditeur de mise à jour référence les informations concernant l’URL ou l’emplacement de téléchargement pour l’abonnement et vous alerte lorsque des modifications ont été apportées au catalogue depuis la dernière fois que vous l’avez importé dans le référentiel.

Pour rechercher manuellement une mise à jour de catalogue, sélectionnez le catalogue dans la liste **Mes catalogues de mises à jour logicielles**, puis choisissez **Actualiser** dans le ruban.

Outre l’ajout de catalogues et l’affichage des informations sur les catalogues auxquels vous êtes abonné, vous pouvez :
-  **Modifier** les informations concernant les catalogues *utilisateur*.
-  **Supprimer** un catalogue de l’éditeur de mise à jour.
-  **Importer** des mises à jour d’un catalogue vers le référentiel de l’éditeur de mise à jour. Lorsque vous importez des mises à jour, vous importez toutes les mises à jour contenues dans ce catalogue. Vous pouvez ensuite afficher les mises à jour dans l’espace de travail Mises à jour, où vous pouvez ensuite sélectionner et publier des mises à jour vers le serveur de mise à jour.

> [!NOTE]   
> La suppression d’un catalogue de l’éditeur de mise en jour entraîne la suppression des mises à jour de ce catalogue de votre référentiel. Cela n’affecte pas les mises à jour que vous avez publiées sur votre serveur de mise à jour. Pour supprimer de votre serveur de mise à jour des mises à jour qui ne figurent plus dans votre référentiel, consultez la rubrique [Faire expirer des mises à jour logicielles non référencées](/sccm/sum/tools/updates-publisher-options#expire-unreferenced-software-updates).

## <a name="manage-update-catalogs"></a>Gérer des catalogues de mises à jour
Vous pouvez afficher la liste des catalogues que vous avez importés dans la fenêtre **Mes catalogues de mises à jour logiciels** de l **’espace de travail Catalogues**. À partir de cet espace de travail, vous pouvez :

-   **Ajouter un catalogue de partenaires :** Utilisez l’une des opérations suivantes pour rechercher des catalogues partenaires :

    -   Dans la console, accédez à l **’espace de travail Mises à jour** > **Vue d’ensemble**. Dans la fenêtre **Prise en main**, choisissez **Ajouter des catalogues de mises à jour logicielles partenaires**.

    -   Dans la console, accédez à l **’espace de travail Catalogues** > **Mes catalogues**. Puis, dans le ruban, choisissez **Ajouter des catalogues**.

-   **Ajouter un catalogue des utilisateurs :** Dans la console, accédez à l **’espace de travail Catalogues** > **Mes catalogues**. Puis, dans le ruban, choisissez **Ajouter des catalogues**. Outre l’emplacement du fichier .cab, vous devez spécifier un éditeur, un nom et une description pour identifier le catalogue.


-   **Rechercher des mises à jour pour les catalogues :** Sélectionnez un ou plusieurs catalogues, puis choisissez **Actualiser** dans le ruban.

-   **Modifier le catalogue des utilisateurs :** Sélectionnez un catalogue des *utilisateurs*, puis choisissez **Modifier** dans le ruban. Vous pouvez ensuite modifier les propriétés définies par l’utilisateur.

-   **Supprimer des catalogues :** Sélectionnez un ou plusieurs catalogues, puis choisissez **Supprimer** dans le ruban. Cette opération supprime le catalogue, votre abonnement et les mises à jour de ces catalogues du référentiel de votre éditeur de mise à jour.

-   **Ajouter des mises à jour d’un catalogue à votre référentiel** : Choisissez **Importer** dans le ruban pour démarrer l’assistant **Importation de catalogue**. Pour plus d’informations, consultez la rubrique [Importer des mises à jour](#import-updates)

## <a name="import-updates"></a>Importer des mises à jour
Lorsque vous importez un catalogue, Updates Manager ajoute les mises à jour de ce catalogue vers le référentiel de l’éditeur de mise à jour. Une fois les mises à jour importées, vous pouvez les publier sur votre serveur de mise à jour pour les mettre à disposition des appareils gérés.

### <a name="to-import-updates"></a>Pour importer des mises à jour
1. Pour démarrer l’Assistant **Importation de catalogue**, choisissez **Importer** dans le ruban des espaces de travail suivants :

   -   Espace de travail Catalogues

   -   Espace de travail Mises à jour

2. Sur la page **Type d’importation**, sélectionnez un ou plusieurs catalogues que vous avez ajoutés à l’éditeur de mise à jour, ou spécifiez un chemin d’accès à un catalogue que vous n’avez pas encore ajouté comme abonnement. Choisissez **Suivant** pour afficher l’écran de résumé puis, lorsque vous êtes prêt, cliquez sur **Suivant** pour démarrer l’importation.

3. Dans la fenêtre **Avertissement de sécurité : validation du catalogue**, examinez le certificat du catalogue puis, lorsque vous êtes prêt, choisissez **Accepter** pour importer les mises à jour.

   > [!CAUTION]
   > Acceptez uniquement les mises à jour d’éditeurs de confiance. Les mises à jour logicielles provenant d’éditeurs qui n’ont pas été approuvés peuvent endommager les ordinateurs clients lors de la recherche de mises à jour.
   > 
   >  Si vous n’approuvez plus un éditeur, supprimez-le de la liste des éditeurs approuvés. Pour plus d’informations sur l’acceptation de catalogues, cliquez sur **En savoir plus** dans la boîte de dialogue **Avertissement de sécurité : validation du catalogue**.

   Si vous souhaitez toujours accepter les catalogues provenant d’un éditeur, cet éditeur est ajouté à la [liste des éditeurs approuvés](/sccm/sum/tools/updates-publisher-options#trusted-publishers). Vous pouvez consulter et modifier cette liste comme une option de l’éditeur de mise à jour.

4. L’importation ignore les mises à jour qui figurent déjà dans le référentiel et si l’une des opérations suivantes est vraie :

   -   La mise à jour n’a pas été modifiée depuis qu’elle a été importée.

   -   La mise à jour a été modifiée et contient un nouveau hachage numérique. La modification d’une mise à jour empêche le remplacement d’une nouvelle mise à jour car cela entraînerait la suppression des modifications que vous auriez déployées.

5. Sur la page **Confirmation**, examinez les résultats de l’importation.

6. Cliquez sur **Fermer** pour terminer l’Assistant. Vous pouvez désormais afficher les mises à jour de ce catalogue dans l’espace de travail Mises à jour.

## <a name="next-steps"></a>Étapes suivantes
Après avoir importé les mises à jour, les actions courantes sont les suivantes :
-   [Gérer les mises à jour](/sccm/sum/tools/manage-updates-with-updates-publisher) pour les regrouper, les affecter et les déployer sur votre serveur de mise à jour.
-   [Créer des règles de mise en application](/sccm/sum/tools/updates-publisher-applicability-rules) pour mieux déterminer le moment où les mises à jour sont déployées sur le serveur de mise à jour.
