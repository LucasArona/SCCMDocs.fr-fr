---
title: Configurer les options
titleSuffix: Configuration Manager
description: Configurer les options afin d’utiliser l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 4e620080-5400-45bb-87c2-fbdbc8aeacac
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 126ac524aaea851f5203888d414f7f9b188649c2
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424474"
---
# <a name="configure-options-for-updates-publisher"></a>Configurer les options pour l’éditeur de mise à jour

*S’applique à : Éditeur de mise à jour System Center*

Vérifiez et configurez les options et les paramètres associés qui affectent le fonctionnement de l’éditeur de mise à jour.

Pour accéder aux options de l’éditeur de mise à jour, dans le coin supérieur gauche de la console, cliquez sur **Éditeur de mise à jour** onglet **Propriétés**, puis choisissez **Options**.

![Options](media/properties1.png)   


Les options sont réparties comme suit :

-   Serveur de mise à jour
-   Serveur ConfigMgr
-   Paramètres proxy
-   Éditeurs approuvés
-   Avancé
-   Mises à jour
-   Journalisation

## <a name="update-server"></a>Serveur de mise à jour
Vous devez configurer l’éditeur de mise à jour pour fonctionner avec un serveur de mise à jour comme Windows Server Update Services (WSUS) avant de pouvoir [publier des mises à jour](/sccm/sum/tools/manage-updates-with-updates-publisher#publish-updates-and-bundles). Cela inclut la spécification du serveur, les méthodes pour se connecter à ce serveur lorsqu’il est distant de la console, et un certificat à utiliser pour signer numériquement les mises à jour que vous publiez.

- **Configurez un serveur de mise à jour**. Lorsque vous configurez un serveur de mise à jour, sélectionnez le serveur WSUS de niveau supérieur (serveur de mise à jour) dans votre hiérarchie Configuration Manager afin que tous les sites enfants aient accès aux mises à jour que vous publiez.

  Si votre serveur de mise à jour est distant du serveur de votre éditeur de mise à jour, spécifiez le nom de domaine complet (FQDN) du serveur, et indiquez si vous vous connectez par SSL. Si vous vous connectez par SSL, le port par défaut passe de 8530 à 8531. Assurez-vous que le port que vous définissez correspond au port en cours d’utilisation par votre serveur de mise à jour.

  > [!TIP]  
  > Si vous ne configurez aucun serveur de mise à jour, vous pouvez quand même utiliser l’éditeur de mise à jour pour créer des mises à jour logicielles.

- **Configurez le certificat de signature**. Vous devez configurer un serveur de mise à jour et vous y connecter avant de pouvoir configurer le certificat de signature.

  L’éditeur de mise à jour utilise le certificat de signature pour signer les mises à jour logicielles publiées sur le serveur de mise à jour. La publication échoue si le certificat numérique n’est pas disponible dans le magasin de certificats du serveur de mise à jour ou sur l’ordinateur qui exécute l’éditeur de mise à jour.

  Pour plus d’informations sur l’ajout du certificat au magasin de certificats, consultez la rubrique [Certificats et sécurité de l’éditeur de mise à jour](/sccm/sum/tools/updates-publisher-security).

  Si un certificat numérique n’est pas automatiquement détecté pour le serveur de mise à jour, choisissez l’une des options suivantes :

  -   **Parcourir** : L’option Parcourir n’est disponible que si le serveur de mise à jour est installé sur le serveur sur lequel vous exécutez la console. Une fois que vous sélectionnez un certificat, vous devez choisir l’option **Créer** pour ajouter un certificat au magasin de certificats WSUS sur le serveur de mise à jour. Vous devez entrer le mot de passe du fichier **.pfx** pour les certificats que vous sélectionnez à l’aide de cette méthode.

  -   **Créer :** Utilisez cette option pour créer un nouveau certificat. Cette option ajoute également le certificat au magasin de certificats WSUS sur le serveur de mise à jour.

  **Si vous créez votre propre certificat de signature**, configurez les éléments suivants :

  -   Activez l’option **Autoriser l’exportation de la clé privée**.

  -   Définissez **Utilisation de la clé** sur Signature numérique.

  -   Définissez **Taille de clé minimale** sur une valeur égale ou supérieure à 2 048 bits.

  Utilisez l’option **Supprimer** pour supprimer un certificat du magasin de certificats WSUS. Cette option est disponible si le serveur de mise à jour est local dans la console de l’éditeur de mise à jour que vous utilisez, ou si vous avez utilisé **SSL** pour vous connecter à un serveur de mise à jour à distance.

## <a name="configmgr-server"></a>Serveur ConfigMgr
Choisissez ces options lorsque vous utilisez Configuration Manager avec l’éditeur de mise à jour.

-   **Spécifier le serveur Configuration Manager :** Après avoir activé la prise en charge pour Configuration Manager, spécifiez l’emplacement du serveur de site de niveau supérieur dans votre hiérarchie Configuration Manager. Si ce serveur est éloigné de l’installation de l’éditeur de mise à jour, spécifiez le nom de domaine complet du serveur de site. Choisissez **Tester la connexion** pour vérifier que vous pouvez vous connecter au serveur de site.

-   **Configurer des seuils :** Les seuils sont utilisés lorsque vous publiez des mises à jour avec un type de publication automatique. Les valeurs de seuil vous aident à déterminer le moment où tout le contenu d’une mise à jour est publié au lieu des métadonnées uniquement. Pour en savoir plus de types de publication, consultez la rubrique [Affecter des mises à jour à une publication](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication)

    Vous pouvez utiliser l’un des seuils suivants ou les deux :

    -   **Seuil du nombre de clients demandé :** Définit le nombre de clients qui doivent demander une mise à jour avant que l’éditeur de mise à jour puisse automatiquement publier tout le contenu de cette mise à jour. Tant que le nombre spécifié de clients n’a pas demandé la mise à jour, seules les métadonnées des mises à jour sont publiées.

    -   **Seuil de taille source du package (Mo) :** Empêche la publication automatique des mises à jour qui dépassent la taille que vous spécifiez. Si la taille des mises à jour dépasse cette valeur, seules les métadonnées sont publiées. Si les mises à jour sont inférieures à la taille spécifiée, tout leur contenu peut être publié.

## <a name="proxy-settings"></a>Paramètres proxy
L’éditeur de mise à jour utilise les paramètres proxy lorsque vous importez des catalogues de logiciels à partir d’Internet ou publiez des mises à jour sur Internet.

-   Spécifiez le nom de domaine complet ou l’adresse IP d’un serveur proxy. IPv4 et IPv6 sont pris en charge.

-   Si le serveur proxy authentifie les utilisateurs pour l’accès à Internet, vous devez spécifier le nom Windows. Le nom principal universel (UPN) n’est pas pris en charge.

## <a name="trusted-publishers"></a>Éditeurs approuvés
Lorsque vous importez un catalogue de mises à jour, la source de ce catalogue (basée sur son certificat) est ajoutée comme éditeur approuvé. De même, lorsque vous publiez une mise à jour, la source du certificat des mises à jour est ajoutée comme éditeur approuvé.

Vous pouvez afficher les détails du certificat pour chaque éditeur et supprimer un éditeur de la liste des éditeurs approuvés.

Le contenu provenant d’éditeurs qui n’ont pas été approuvés peut endommager les ordinateurs clients lorsque le client recherche des mises à jour. Vous devriez uniquement accepter les mises à jour d’éditeurs de confiance.

## <a name="advanced"></a>Avancé
Les options avancées incluent ce qui suit :

-   **Emplacement du référentiel :** Affichez et modifiez l’emplacement du fichier de base de données, **scupdb.sdf**. Ce fichier représente le référentiel de l’éditeur de mise à jour.

-   **Horodateur :** Si cette option est activée, un horodatage est ajouté aux mises à jour que vous signez, indiquant la date de leur signature. Une mise à jour signée alors que le certificat était valide peut être utilisée après expiration de ce certificat de signature. Par défaut, les mises à jour logicielles ne peuvent pas être déployées après expiration de leur certificat de signature.

-   **Rechercher les mises à jour des catalogues auxquels vous êtes abonné :** Chaque fois que l’éditeur de mise à jour démarre, il peut vérifier automatiquement les mises à jour des catalogues auxquels vous êtes abonné. Lorsqu’une mise à jour du catalogue est trouvée, les détails sont fournis en tant qu **’alertes récentes** dans la fenêtre **Vue d’ensemble** de l **’espace de travail Mises à jour**.

-   **Révocation de certificat :** Choisissez cette option pour activer des vérifications de révocation de certificat.

-   **Publication source locale :** L’éditeur de mise à jour peut utiliser une copie locale d’une mise à jour que vous publiez avant de télécharger cette mise à jour à partir d’Internet. L’emplacement doit être un dossier sur l’ordinateur qui exécute l’éditeur de mise à jour. Par défaut, cet emplacement est **Mes documents\LocalSourcePublishing.** Utilisez cet emplacement même si vous avez déjà téléchargé une ou plusieurs mises à jour, ou si vous avez modifié une mise à jour que vous souhaitez déployer.

-   **Assistant Nettoyage des mises à jour logicielles :** Démarre l’Assistant Nettoyage des mises à jour logicielles. L’Assistant fait expirer les mises à jour qui figurent sur le serveur de mise à jour mais pas dans le référentiel de l’éditeur de mise à jour. Consultez la page [Faire expirer les mises à jour non référencées](#expire-unreferenced-software-updates) pour plus de détails.

## <a name="updates"></a>Mises à jour
 L’éditeur de mise à jour peut automatiquement rechercher les nouvelles mises à jour chaque fois qu’il s’ouvre. Vous pouvez aussi choisir de recevoir des builds de version préliminaire de l’éditeur de mise à jour.

Pour rechercher manuellement les mises à jour, dans la console de l’éditeur de mise à jour, cliquez sur ![Propriétés](media/properties2.png)  
pour ouvrir les **propriétés de l’éditeur de mise à jour**, puis choisissez **Rechercher les mises à jour**.

Lorsque l’éditeur de mise à jour détecte une nouvelle mise à jour, il affiche la fenêtre **Mise à jour disponible** et vous pouvez alors choisir d’installer cette mise à jour. Si vous choisissez de ne pas installer la mise à jour, vous serez invité à l’installer la prochaine fois que vous ouvrez la console.

## <a name="logging"></a>Journalisation
L’éditeur de mise à jour enregistre les informations de base sur l’éditeur de mise à jour dans **&lt;*chemin*&gt;\Windows\Temp\UpdatesPublisher.log**.

Utilisez le bloc-notes ou **CMTrace** pour afficher le journal. CMTrace est l’outil de fichier journal de Configuration Manager, qui se trouve dans le dossier **\SMSSetup\Tools** du support source Configuration Manager.

Vous pouvez modifier la taille du journal et son niveau de détail.

Lorsque vous activez la journalisation de la base de données, les informations concernant les requêtes exécutées sur la base de données de l’éditeur de mise à jour sont incluses. La journalisation de la base de données peut entraîner une dégradation des performances de l’ordinateur de l’éditeur de mise à jour.

Pour afficher le fichier journal, cliquez dans la console sur ![Propriétés](media/properties2.png) pour ouvrir les **propriétés de l’éditeur de mise à jour**, puis choisissez **Afficher le fichier journal**.

## <a name="expire-unreferenced-software-updates"></a>Faire expirer les mises à jour logicielles non référencées
Vous pouvez exécuter l **’Assistant Nettoyage des mises à jour logicielles** pour faire expirer les mises à jour situées sur votre serveur de mise à jour mais pas dans le référentiel de l’éditeur de mise à jour. Cette procédure avertit Configuration Manager, qui supprime alors ces mises à jour de tous les futurs déploiements.

L’opération consistant à faire expirer une mise à jour ne peut pas être annulée. Effectuez uniquement cette tâche si vous êtes sûr que les mises à jour logicielles que vous sélectionnez ne sont plus requises par votre organisation.

### <a name="to-remove-expired-software-updates"></a>Pour supprimer des mises à jour logicielles expirées
1.  Dans la console de l’éditeur de mise à jour, cliquez sur ![Propriétés](media/properties2.png) pour ouvrir les **propriétés de l’éditeur de mise à jour**, puis choisissez **Options**.

2.  Choisissez **Avancé**, puis sous **Assistant Nettoyage des mises à jour logicielles,** choisissez **Démarrer**.

3.  Sélectionnez les mises à jour logicielles vous souhaitez faire expirer, puis choisissez **Suivant**.

4.  Après avoir vérifié vos sélections, choisissez **Suivant** pour accepter les sélections et faire expirer les mises à jour.

5.  Une fois l’Assistant terminé, choisissez **Fermer** pour terminer l’Assistant.
