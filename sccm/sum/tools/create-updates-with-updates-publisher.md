---
title: Créer des mises à jour
titleSuffix: Configuration Manager
description: Créer et regrouper des mises à jour logicielles avec l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 46a1a8ac-126c-4ee6-ae09-32dfbdb83368
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 7d12962e40880ccd5aef0a2f3a78754748228f75
ms.sourcegitcommit: 23e93055c234a01fd1066d0b0a7e35fb22e47f73
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/15/2018
ms.locfileid: "49324826"
---
# <a name="create--software-updates-and-update-bundles-with-updates-publisher"></a>Créer des mises à jour logicielles et des offres groupées de mises à jour avec l’éditeur de mise à jour

*S’applique à : l'éditeur de mise à jour System Center*

L’éditeur de mise à jour vous permet d’utiliser l’Assistant **Création d’une mise à jour** pour créer vos propres mises à jour et l’Assistant **Création d’une offre groupée** pour créer des offres groupées de mises à jour.

Ces deux Assistants ayant un flux de travail similaire, la procédure de création d’une offre groupée de mises à jour fait référence à la procédure de création de mises à jour et seules les différences pertinentes sont détaillées.

## <a name="use-the-create-update-wizard"></a>Utiliser l’Assistant Création d’une mise à jour
1.  Dans la console, accédez à l **’espace de travail Mises à jour** puis, dans le volet **Mise en route**, choisissez **Mise à jour** dans l’onglet **Accueil** du ruban. Cette opération ouvre l’Assistant **Création d’une mise à jour**.

2.  Sur la page **Package**, utilisez les informations suivantes pour vous aider à configurer la mise à jour :

    -   Choisissez **Parcourir** pour rechercher le package de mises à jour logicielles que vous allez utiliser comme source de package. Les sources valides incluent les fichiers .MSI, .MSP ou .EXE. L’éditeur de mise à jour nécessite l’accès au fichier pour créer un hachage de fichier. Le hachage et le nom du fichier sont ensuite utilisés dans les métadonnées de la mise à jour que vous créez.

    -   Spécifiez l’emplacement source du contenu de cette mise à jour. Il s’agit normalement de l’emplacement où le fichier binaire de mise à jour est téléchargé lors de la publication sur un serveur WSUS.  Si l’option permettant d’**utiliser une source locale pour publier le contenu de la mise à jour logicielle** est sélectionnée, le chemin d’accès n’est pas requis.

        Ultérieurement, si la mise à jour est publiée sur un serveur WSUS, l’éditeur de mise à jour télécharge les fichiers binaires de la mise à jour depuis l’emplacement source indiqué.  Si aucun chemin d’accès n’est fourni, l’éditeur de mise à jour recherchera le [chemin de publication de la source locale](/sccm/sum/tools/updates-publisher-options#advanced) pour le fichier binaire de mise à jour.

    -   Spécifiez le **langage binaire** de la mise à jour logicielle.

    -   Spécifiez les **codes de retour de réussite** et les **codes de redémarrage en attente de réussite** de la mise à jour. Séparez plusieurs codes de retour à l’aide d’une virgule. Vous pouvez utiliser les codes de retour pour déterminer si l’installation de la mise à jour a réussi et si des redémarrages ont été requis.

        -   Les fichiers du programme d’installation et correctifs Windows (fichiers .MSI et .MSP) définissent automatiquement ces valeurs, qui ne peuvent pas être modifiées.

        -   Pour les mises à jour .EXE, les codes par défaut définis par le fichier .EXE sont utilisés si aucun code de retour n’est spécifié.

    -   Spécifiez les arguments de ligne de commande nécessaires pour installer la mise à jour.

        -   Les fichiers du programme d’installation et correctifs Windows (fichiers .MSI et .MSP) définissent automatiquement ces valeurs. Pour ces types de fichiers, les arguments doivent être spécifiés en tant que **\[nom\]=\[valeur\]**. En outre, toutes les options qui commencent par **/** (comme **/qn**) ne sont pas prises en charge pour les mises à jour .MSI ou .MSP.

        -   Pour les mises à jour .EXE, tous les arguments sont valides.

3.  Sur la page **Informations**, spécifiez les informations relatives à la mise à jour, incluses lorsque celle-ci est publiée ou exportée. Les détails incluent les propriétés localisées telles que le nom (titre) et la description des mises à jour. Spécifiez ensuite des informations plus générales comme la classification, le fournisseur, le produit et où obtenir plus de détails sur la mise à jour.

     __Propriétés localisées :__

    -   **Langue** : sélectionnez une langue, puis spécifiez un titre et une description. Vous pouvez ensuite sélectionner d’autres langues, une par une, chaque langue prenant en charge ses propres titre et description.

    -   **Titre** : entrez le nom de la mise à jour. Ce nom s’affiche dans l’espace de travail Mises à jour de la console de l’éditeur de mise à jour.

    -   **Description**: une description claire de la mise à jour. Vous pouvez inclure les éléments installés par la mise à jour et indiquer pourquoi ou quand celle-ci doit être utilisée.

     **Classification :** les éléments suivants sont des descriptions communes des différentes classifications.

    -   **Mise à jour** : mise à jour d'une application ou d'un fichier qui sont déjà installés.

    -   **Critique** : mise à jour distribuée en grand nombre, répondant à un problème spécifique qui concerne un bogue critique non lié à la sécurité.

    -   **Feature Pack** : nouvelles fonctionnalités de produit, distribuées en dehors d'une version de produit et incluses généralement dans la version suivante du produit.

    -   **Sécurité** : mise à jour distribuée en grand nombre, répondant à un problème de sécurité spécifique à un produit.

    -   **Correctif cumulatif**: ensemble cumulé de correctifs assemblés pour faciliter leur déploiement. Ces correctifs peuvent comprendre des mises à jour de sécurité, des mises à jour critiques, des mises à jour, etc. Les correctifs cumulatifs concernent généralement un domaine particulier, par exemple la sécurité ou une fonctionnalité de produit.

    -   **Service Pack** : ensemble cumulé de correctifs rattachés à une application. Ces correctifs peuvent comprendre des mises à jour de sécurité, des mises à jour critiques, des mises à jour logicielles, etc.

    -   **Outil** : outil ou fonctionnalité permettant d'effectuer une ou plusieurs tâches.

     -   **Pilote** : mise à jour du logiciel d’un pilote.

    **Fournisseur :** spécifie un fournisseur pour la mise à jour. Vous pouvez utiliser la liste déroulante pour choisir les valeurs des mises à jour figurant dans le référentiel. Lorsque vous spécifiez un fournisseur, l’Assistant crée un dossier portant le nom de ce fournisseur sous **Toutes les mises à jour logicielles** dans l **’espace de travail Mises à jour** si ce dossier n’existe pas déjà. Voici une liste des noms Windows Server Update Services (WSUS) réservés qui ne peuvent pas être entrés pour les mises à jour que vous créez :
 >*   Microsoft Corporation
 >*   Microsoft
 >*   Mise à jour
 >*   Mise à jour logicielle
 >*   Outils
 >*   Outil
 >*   Critique
 >*   Mises à jour critiques
 >*   Sécurité
 >*   Mises à jour de sécurité
 >*   Feature Pack
 >*   Correctif cumulatif
 >*   Service Pack
 >*   Pilote
 >*   Mise à jour du pilote
 >*   Offre groupée
 >*   Offre groupée de mises à jour

**Produit** : spécifie le type de produit pour lequel la mise à jour est destinée. Vous pouvez utiliser la liste déroulante pour choisir les valeurs des mises à jour figurant dans le référentiel. La même liste de noms WSUS réservés qui ne peuvent pas être utilisés pour **Fournisseur**, ne peut pas être utilisée pour **Produit**.

 **URL Informations** : spécifie l’URL où vous trouverez plus d’informations sur cette mise à jour. Vous devez utiliser des minuscules pour **https** ou **http** lorsque vous entrez cette URL.

4.  Sur la page **Informations facultatives**, vous pouvez configurer les détails qui fournissent des informations supplémentaires sur la mise à jour.

    -   **ID du bulletin** : les ID de bulletin sont généralement, mais pas toujours, fournis par les fournisseurs de mises à jour.

    -   **ID de l’article** : si l’article d’une mise à jour logicielle est disponible, l’ID de l’article peut être utile pour les personnes qui cherchent plus d’informations sur la mise à jour.

    -   **ID de CVE :** répertorie un ou plusieurs identificateurs CVE (Common Vulnerabilities and Exposures) qui fournissent des informations de sécurité sur la mise à jour ou l’offre groupée de mises à jour. Si la liste contient plusieurs CVE, utilisez un point-virgule pour les séparer, comme dans cet exemple : *CVE1;CVE2.*

    -   **URL de prise en charge :** répertorie les URL qui contiennent des informations de prise en charge pour cette mise à jour, le cas échéant. Vous devez utiliser des minuscules pour **https** ou **http** lorsque vous entrez cette URL.

    -   **Gravité :** définit le niveau de gravité de cette mise à jour.

    -   **Impact :** les options suivantes peuvent être utilisées pour spécifier l’impact :
        -   **Normal** : indique que la mise à jour nécessite les procédures d’installation par défaut.
        -   **Mineur**  : indique que la mise à jour nécessite les procédures d’installation minimale.
        -   **Nécessite une prise en charge exclusive** : indique que la mise à jour doit être installée par elle-même, sans tenir compte d’autres mises à jour.   <br /><br />

    -   **Comportement de redémarrage :** permet de fournir des informations sur le comportement de redémarrage des mises à jour. Ce paramètre n’affecte pas le comportement réel de l’installation de la mise à jour.

        -   **Ne redémarre jamais** : l’ordinateur n’effectue jamais un redémarrage du système après l’installation de la mise à jour logicielle.
        -   **Nécessite toujours un redémarrage** : l’ordinateur effectue toujours un redémarrage du système après l’installation de la mise à jour logicielle.
        -   **Peut nécessiter un redémarrage** : après l’installation de la mise à jour, l’ordinateur demande un redémarrage du système uniquement si un redémarrage est nécessaire. L’utilisateur a la possibilité de reporter le redémarrage. Il s'agit de la valeur par défaut. <br /><br />

5.  Sur la page des **conditions préalables**, spécifiez les conditions préalables qui doivent être réunies sur un ordinateur avant de pouvoir installer cette mise à jour. Les conditions requises peuvent être des **detectoids** ou d’autres mises à jour. Les detectoids sont des règles de haut niveau nécessitant, par exemple, des ordinateurs équipés d’un processeur 64 bits. Les detectoids peuvent également indiquer les mises à jour spécifiques qui doivent être installées avant de pouvoir installer cette mise à jour.

    -   Pour de meilleures performances, utilisez des detectoids au lieu de créer des règles *installables* et des *règles installées* qui effectuent la même vérification ou action.

    Utilisez l’option de recherche des **mises à jour logicielles et detectoids disponibles** pour vous aider à trouver des mises à jour ou des detectoids spécifiques. Par exemple, recherchez **processeur** pour trouver les detectoids vous permettant de limiter l’installation à une architecture de processeur spécifique.

    Vous pouvez sélectionner un ou plusieurs éléments à la fois pour les ajouter comme condition préalable. Lorsque vous ajoutez des conditions préalables, les detectoids sélectionnés sont ajoutés comme un ou plusieurs groupes. Pour pouvoir effectuer l’installation, un ordinateur doit remplir les conditions d’au moins un membre de chaque groupe que vous configurez :

 -   Lorsque vous cliquez sur **Ajouter une condition préalable**, tous les éléments que vous avez sélectionnés sont ajoutés à des groupes individuels distincts. Pour bénéficier de cette mise à jour, un ordinateur doit remplir les conditions de ce groupe et répondre aux exigences de tous les autres groupes configurés.

 -   Lorsque vous cliquez sur **Ajouter un groupe**, tous les éléments que vous avez sélectionnés sont ajoutés à un même groupe. Pour bénéficier de cette mise à jour, un ordinateur doit remplir au moins une des conditions de ce groupe et répondre aux exigences de tous les autres groupes configurés.

6.  Sur la page **Remplacement**, spécifiez les mises à jour remplacées par cette mise à jour. Lorsque cette mise à jour est publiée, Configuration Manager marque chaque mise à jour remplacée comme ayant **expiré**. Les clients installeront ensuite cette mise à jour au lieu des mises à jour remplacées.

7.  Sur la page **Mise en application**, utilisez l **’éditeur de règles** pour définir un ensemble de règles déterminant si un appareil a besoin de cette mise à jour. (Cette page est similaire à la page **Installé** qui la suit.)

    Pour ajouter une nouvelle règle, cliquez sur ![Nouvelle règle](media/newrule.png). Cette opération ouvre la page Règle de mise en application dans laquelle vous pouvez configurer des règles.

    Les types de règles que vous pouvez créer sont les suivants :

    -   **Fichier** : cette règle oblige un appareil à utiliser un fichier de propriétés correspondant à un ou plusieurs critères que vous spécifiez, avant de pouvoir appliquer cette mise à jour.

    -   **Registre** : ce type permet de spécifier les détails de registre qui doivent être présents avant de pouvoir installer cette mise à jour sur un appareil.

    -   **Système** : cette règle utilise les informations système pour déterminer les conditions de mise en application. Vous pouvez choisir entre la définition d’une version de Windows, une langue de Windows, l’architecture du processeur, ou spécifier une requête WMI qui identifie le système d’exploitation des appareils.

    -   **Windows Installer** : utilisez ce type de règle pour déterminer les conditions de mise en application en fonction d’un correctif .MSI ou Windows Installer (.MSP) installé. Vous pouvez également déterminer si des composants ou des fonctionnalités spécifiques sont installés dans le cadre des exigences.

        > [!IMPORTANT]  
        > Sur les appareils gérés, l’Agent Windows Update ne peut pas détecter les packages Windows Installer installés par l’utilisateur. Lorsque vous utilisez ce type de règle, configurez des règles de mise en application supplémentaires, notamment les versions des fichiers ou les valeurs de clé de registre, de façon à détecter correctement le package Windows Installer, que ce soit par utilisateur ou par système.

    -   **Règle enregistrée** : cette option vous permet de rechercher et d’utiliser les règles que vous avez *créé dans l’espace de travail Règles*.

        Après avoir créé une règle, vous pouvez utiliser les autres icônes pour modifier la règle, et s’il existe plusieurs règles, pour définir des relations entre elles.

    Lorsque vous avez fini de créer et d’ajouter des règles, cliquez sur **OK** dans la boîte de dialogue **Créer un ensemble de règles** pour enregistrer cet ensemble. Vous pouvez ensuite créer une **nouvelle** règle et l’ajouter également à l’ensemble.

    Si vous avez plusieurs règles ou ensembles de règles à ajouter à une mise à jour, vous pouvez utiliser les opérateurs logiques de l **’éditeur de règles** pour déterminer les conditions entre les règles et l’ordre dans lequel elles sont traitées.

8.  Sur la page **Installé**, utilisez l **’éditeur de règles pour** définir un ensemble de règles déterminant si un appareil a déjà installé la mise à jour que vous configurez. (Cette page est similaire à la page **Mise en application** qui la suit.)

    Cette page de l’Assistant permet de configurer des règles avec les mêmes options et critères que la page **Mise en application**.

    À la fin de l’Assistant, la nouvelle mise à jour est ajoutée à un nœud dans l **’espace de travail Mises à jour** qui est identifié par le nom du **fournisseur** et du **produit** de cette mise à jour.

## <a name="use-the-create-bundle-wizard"></a>Utiliser l’Assistant Création d’une offre groupée
Comme cet Assistant utilise le même flux de travail que l’[Assistant Création d’une mise à jour](#use-the-create-update-wizard), utilisez ce flux de travail en tenant compte de la différence suivante concernant les offres groupées :

1.  Pour démarrer l’Assistant, dans la console, accédez à l **’espace de travail Mises à jour** puis choisissez **Offre groupée** dans l’onglet **Accueil** du ruban.

2.  Contrairement à l’Assistant Création d’une mise à jour, il n’existe aucune page Package lors de la création d’une offre groupée.

3.  Sur la page **Informations**, spécifiez les informations relatives à l’offre groupée de mises à jour, incluses lorsque celle-ci est publiée ou exportée.

4.  Sur la page **Informations facultatives**, vous pouvez configurer les détails qui fournissent des informations supplémentaires sur l’offre groupée de mises à jour. Les options disponibles sont les mêmes que pour la création d’une mise à jour. Toutefois, les options liées à l’impact et au comportement du redémarrage ne sont pas disponibles car elles ne s’appliquent pas aux offres groupées.

5.  Sur la page des **conditions préalables**, spécifiez les conditions préalables qui doivent être réunies sur un ordinateur avant de pouvoir installer cette offre groupée. Ces règles sont les mêmes que pour les mises à jour individuelles.

6.  Sur la page **Remplacement**, spécifiez les mises à jour remplacées par cette offre groupée de mises à jour. Ces règles sont les mêmes que pour les mises à jour individuelles.

7.  Sur la page **Membres**, sélectionnez les mises à jour à ajouter à l’offre groupée. Seules les mises à jour que vous avez créées ou importées vers l’éditeur de mise à jour sont disponibles.

À la fin de l’Assistant, la nouvelle offre groupée de mises à jour est ajoutée à un nœud dans l **’espace de travail Mises à jour** qui est identifié par le nom du **fournisseur** de cette offre groupée.
