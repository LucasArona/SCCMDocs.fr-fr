---
title: Gérer les mises à jour
titleSuffix: Configuration Manager
description: Gérer les mises à jour que vous déployez et créez avec l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: cd64994c-b426-4465-96cd-54b0edc2778d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88cc03de66847143336425dbc4b730703d15378c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493786"
---
# <a name="manage-software-updates-in-updates-publisher"></a>Gérer les mises à jour logicielles dans l’éditeur de mise à jour

*S’applique à : l'éditeur de mise à jour System Center*     

Dans l’éditeur de mise à jour System Center, vous utilisez l **’espace de travail Mises à jour** pour gérer les mises à jour logicielles et offres groupées que vous avez importées dans le référentiel.  

Les tâches de gestion incluent la duplication, la modification et l’expiration ou la réactivation des mises à jour et offres groupées, ainsi que l’affectation de mises à jour et d’offres groupées à des publications. Vous pouvez également exporter des catalogues personnalisés pour une utilisation avec d’autres installations de l’éditeur de mise à jour.

Pour obtenir des mises à jour que vous pouvez gérer :
-  [Ajoutez un catalogue de mises à jour](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) à votre installation de l’éditeur de mise à jour
-  [Importez](/sccm/sum/tools/updates-publisher-catalogs#import-updates) dans votre référentiel les mises à jour à partir de ce catalogue.

Vous pouvez également [créer vos propres mises à jour](/sccm/sum/tools/create-updates-with-updates-publisher).



## <a name="create-a-duplicate-of-an-update"></a>Créer un doublon d’une mise à jour
Vous pouvez créer des doublons, ou copies, des mises à jour dans votre référentiel. Vous pouvez ensuite modifier la copie au lieu de modifier la mise à jour originale. Vous ne pouvez pas créer de copies d’offres groupées de mises à jour.

Pour créer une copie, sélectionnez une mise à jour dans l **’espace de travail Mises à jour**, puis choisissez **Dupliquer**. La copie de la mise à jour s’affiche au même emplacement dans l’espace de travail Mises à jour avec la mention *Copie de* ajoutée à son nom.

La nouvelle copie que vous créez affiche l’état **Non expirée** mais conserve les paramètres de la version originale.

## <a name="edit-updates-and-bundles"></a>Modifier des mises à jour et des offres groupées
Vous pouvez sélectionner et modifier des mises à jour et des offres groupées figurant dans votre référentiel.

Dans l **’espace de travail Mises à jour**, sélectionnez une mise à jour ou une offre groupée, puis choisissez **Modifier** dans l’onglet **Accueil** pour ouvrir l’Assistant de modification. Les mises à jour et les offres groupées disposent d’assistants étroitement liés mais distincts qui présentent les mêmes options que les Assistants [Création d’une mise à jour](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-update-wizard) ou [Création d’une offre groupée](/sccm/sum/tools/create-updates-with-updates-publisher#the-create-bundle-wizard).

Lors de la modification, vous pouvez modifier les détails disponibles concernant la mise à jour ou l’offre groupée afin de l’utiliser dans votre environnement. Par exemple, vous pouvez modifier les règles de mise en application, de priorité ou la langue. Vous pouvez également modifier le produit et le fournisseur pour déplacer la mise à jour ou l’offre groupée vers un dossier personnalisé et regrouper les mises à jour pour votre usage personnel.

## <a name="assign-updates-and-bundles-to-a-publication"></a>Affecter des mises à jour et des offres groupées à une publication
Vous pouvez sélectionner des mises à jour et des offres groupées dans l **’espace de travail Mises à jour**, puis les **affecter** à partir de l’onglet **Accueil** du ruban afin de les ajouter à une publication. Cette opération lance l’Assistant **Affectation de mises à jour logicielles**.
-  Consultez la rubrique [Publier des mises à jour et des offres groupées](#publish-updates-and-bundles-from-the-updates-workspace) pour plus d’informations sur la sélection et la publication de mises à jour et d’offres groupées en une seule tâche.
-  Consultez la rubrique [Gérer les publications](/sccm/sum/tools/updates-publisher-publications) pour plus d’informations sur la gestion de groupes de mises à jour et d’offres groupées comme un seul objet. Après avoir affecté des mises à jour à une publication, vous pouvez gérer cette publication, qui à son tour inclut toutes ses mises à jour affectées.

Lorsque vous affectez des mises à jour à une publication :

-   Vous pouvez inclure des mises à jour expirées et non expirées ainsi que des offres groupées dans la même publication.

-   Spécifiez le type de publication :

    -   **Tout le contenu** : cette option publie tout le contenu de la mise à jour sur votre serveur WSUS. Cela inclut les métadonnées et les fichiers binaires des mises à jour.

    -   **Métadonnées uniquement** : cette option publie uniquement les métadonnées ; les fichiers binaires des mises à jour ne sont pas publiés. Vous pouvez choisir cette option si vous souhaitez regrouper les données de conformité.

    -   **Automatique** : ce mode est uniquement disponible si l’éditeur de mise à jour est connecté à Configuration Manager (voir l’option [Serveur ConfigMgr](/sccm/sum/tools/updates-publisher-options#configmgr-server).)

    Avec ce type, l’éditeur de mise à jour interroge Configuration Manager pour déterminer si les mises à jour ou les offres groupées doivent être publiées avec tout le contenu ou uniquement les métadonnées. Tout le contenu d’une mise à jour est publié uniquement si cette mise à jour respecte le **seuil du nombre de clients demandé** et le **seuil de taille source du package,** qui sont spécifiés dans la page **Serveur ConfigMgr** des options de l’éditeur de mise à jour.

-   Sélectionnez une publication :

    -   Utilisez l’option **Affecter une mise à jour logicielle aux publications existantes** si vous avez déjà créé une publication que vous souhaitez utiliser. Cette option n’est disponible que si au moins une publication existe.

    -   Utilisez l’option **Affecter une mise à jour logicielle à une nouvelle publication** si vous ne disposez d’aucune publication appropriée. Elle créera une nouvelle publication portant le nom que vous spécifiez.

Après avoir affecté des mises à jour à une publication, vous pouvez utiliser l **’espace de travail Publications** pour [publier](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) ou [exporter](/sccm/sum/tools/updates-publisher-publications#export-a-pubilcation) la publication en tant que groupe.

## <a name="publish-updates-and-bundles-from-the-updates-workspace"></a>Publier des mises à jour et des offres groupées à partir de l’espace de travail Mises à jour
Lorsque vous publiez des mises à jour et des offres groupées, l’éditeur de mise à jour ajoute des informations sur ces mises à jour et offres (métadonnées) et éventuellement les fichiers binaires des mises à jour (tout le contenu) à un serveur de mise à jour pour le déploiement sur des appareils.

Avant de pouvoir publier une mise à jour, vous devez configurer l’option [Serveur de mise à jour](/sccm/sum/tools/updates-publisher-options#update-server) de l’éditeur de mise à jour. Pour ouvrir cette option de configuration, accédez à l **’espace de travail Mises à jour** &gt; **Vue d’ensemble** et sélectionnez **Configurer WSUS et le certificat de signature.** Vous pouvez également accéder à la page Serveur de mise à jour dans les options de l’éditeur de mise à jour.

Il existe deux façons de publier des mises à jour et des offres groupées :
-   Directement depuis l'espace de travail Mises à jour. (Consultez la procédure suivante *pour publier des mises à jour et des offres groupées*.)
-   En tant que [publication](/sccm/sum/tools/updates-publisher-publications#publish-pubilcations) depuis l’espace de travail Publications.  

> [!NOTE]   
> Le serveur de mise à jour peut uniquement publier des mises à jour d’une taille maximale de 375 mégaoctets (Mo).

### <a name="to-publish-updates-and-bundles"></a>Pour publier des mises à jour et des offres groupées
1.  Accédez à l **’espace de travail Mises à jour**, puis sélectionnez une ou plusieurs mises à jour et offres groupées que vous souhaitez publier. Puis choisissez **Publier** dans l’onglet **Accueil** du ruban.

2.  Sur la page **Sélectionner** de l’Assistant **Publication**, indiquez comment vous voulez publier les mises à jour. Les options sont les mêmes que pour l[’attribution des mises à jour](#assign-updates-and-bundles-to-a-publication) : **Tout le contenu**, **Uniquement les métadonnées** ou **Automatique**.

    Vous pouvez également choisir de signer toutes les mises à jour avec un nouveau certificat de publication.

3.  Effectuez toutes les étapes de l'Assistant.

Si la publication échoue, vous recevez un lien vers le fichier UpdatesPublisher.log apparaît qui peut fournir plus d’informations.

## <a name="export-updates"></a>Exporter des mises à jour
Vous pouvez exporter des mises à jour et des offres groupées depuis le référentiel de l’éditeur de mise à jour afin de créer un catalogue personnalisé de mises à jour. Vous pouvez ensuite [ajouter](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) puis [importer](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) ce catalogue vers une autre instance de l’éditeur de mise à jour. (Vous pouvez également [exporter des mises à jour sous la forme d’une publication](/sccm/sum/tools/updates-publisher-publications##export-a-publication).)

Pour exporter directement des mises à jour, accédez à l **’espace de travail Mises à jour** > **Toutes les mises à jour logicielles** et sélectionnez une ou plusieurs mises à jour et offres groupées. Vous ne pouvez pas exporter un fournisseur ou un dossier de produit, mais vous pouvez sélectionner un dossier puis les mises à jour de ce dossier pour l’exportation.

Après avoir sélectionné une ou plusieurs mises à jour, choisissez **Exporter** dans l’onglet **Accueil** du ruban, puis indiquez un chemin d’accès et un nom de fichier pour l’exportation du catalogue.

Vous pourrez également exporter (inclure) des mises à jour de logiciels dépendantes.

## <a name="delete-updates-and-bundles"></a>Supprimer des mises à jour et des offres groupées
Vous pouvez supprimer des mises à jour et des offres groupées de mises à jour afin de les supprimer du référentiel de l’éditeur de mise à jour.

Accédez à l **’espace de travail Mises à jour** > **Toutes les mises à jour logicielles** et sélectionnez une ou plusieurs mises à jour individuelles. Puis choisissez **Supprimer** dans l’onglet **Accueil** du ruban.

-   Si votre sélection contient uniquement des mises à jour ou des offres groupées qui n’ont pas été publiées ou qui ont expiré, vous êtes invité à confirmer la suppression.

-   Si votre sélection contient une mise à jour ou une offre groupée qui a été publiée mais n’a pas encore expiré, vous recevez un avertissement. Vous devez [faire expirer](/sccm/sum/tools/updates-publisher-pubilcations#expire-or-reactivate-updates-and-bundles) ces mises à jour puis publier cette modification avant de supprimer les mises à jour du référentiel.  

Si vous supprimez une mise à jour ou une offre groupée d’un fournisseur puis importez de nouveau ce catalogue, cette mise à jour est restaurée dans votre référentiel.

## <a name="manage-vendor-and-product-folders"></a>Gérer des dossiers de produit et de fournisseur
Pour afficher une liste des fournisseurs et des produits de chaque fournisseur pour lequel vous avez importé ou créé des mises à jour, accédez à l **’espace de travail Mises à jour** > **Vue d’ensemble** > **Toutes les mises à jour logicielles**.

Les dossiers des fournisseurs et des produits sont automatiquement créés par l’éditeur de mise à jour lorsque vous utilisez un Assistant pour importer ou créer une mise à jour logicielle ou une offre groupée. Vous pouvez également créer manuellement ces dossiers.

-   Pour créer un dossier de fournisseur, dans le volet de navigation de l **’espace de travail Mises à jour**, cliquez avec le bouton droit sur **Toutes les mises à jour logicielles**, puis choisissez **Créer un fournisseur**.

-   Pour créer un dossier de produit dans un dossier de fournisseur, cliquez avec le bouton droit sur le dossier de fournisseur et choisissez **Créer un produit**.

Outre la création de dossiers, vous pouvez renommer ou supprimer n’importe quel dossier de fournisseur ou de produit de votre référentiel. Pour cela, cliquez avec le bouton droit sur le dossier puis choisissez l’option souhaitée, **Renommer** ou **Supprimer**. La suppression d’un dossier supprime toutes les mises à jour et offres groupées de ce dossier ainsi que ses dossiers de produit du référentiel de l’éditeur de mise à jour.

Vous pouvez déplacer des mises à jour entre des dossiers de fournisseurs et de produits, y compris les dossiers que vous créez. Pour déplacer une mise à jour ou une offre groupée vers un nouveau dossier, vous devez sélectionner puis **modifier** la mise à jour ou l’offre groupée. Puis, dans la page **Informations** de l’Assistant Modification d’une mise à jour, vous pouvez réaffecter le produit et le fournisseur. À la fin de l’Assistant **Modification d’une mise à jour**, la modification est appliquée et la mise à jour est déplacée vers le nouveau dossier.

## <a name="view-the-xml-of-an-update-or-bundle"></a>Afficher la structure XML d’une mise à jour ou d’une offre groupée
Pour sélectionner une mise à jour ou une offre groupée unique, dans l **’espace de travail Mises à jour**, choisissez **Affichage** XML pour afficher la structure XML de cette mise à jour. Il n’existe aucune option permettant de modifier directement la structure XML.
