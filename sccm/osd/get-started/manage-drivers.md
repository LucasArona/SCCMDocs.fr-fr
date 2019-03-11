---
title: Gérer les pilotes
titleSuffix: Configuration Manager
description: Le catalogue de pilotes Configuration Manager permet d’importer des pilotes de périphérique, de les regrouper dans des packages et de distribuer ces packages à des points de distribution.
ms.date: 03/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be3cc24721674e9da276e7a65af03a5b4a266eed
ms.sourcegitcommit: 33a006204f7f5f9b9acd1f3e84c4bc207362d00a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305692"
---
# <a name="manage-drivers-in-configuration-manager"></a>Gérer les pilotes dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager propose un catalogue de pilotes qui permet de gérer les pilotes de périphérique Windows dans un environnement Configuration Manager. Importez des pilotes de périphérique dans Configuration Manager, regroupez-les dans des packages et distribuez-les auprès des points de distribution. Des pilotes de périphérique peuvent être utilisés pour installer le système d’exploitation complet sur l’ordinateur de destination et pour se servir de Windows PE dans une image de démarrage. Les pilotes de périphérique Windows sont composés d’un fichier d’informations d’installation (INF) et de tous les autres fichiers nécessaires à la prise en charge du périphérique. Lors du déploiement d’un système d’exploitation, Configuration Manager récupère les informations sur le matériel et la plateforme du périphérique dans son fichier INF. 



## <a name="BKMK_DriverCategories"></a> Catégories de pilotes

Lorsque vous importez des pilotes de périphérique, vous pouvez affecter les pilotes de périphérique à une catégorie. Les catégories de pilotes de périphérique permettent de regrouper les pilotes de périphérique utilisés de la même façon dans le catalogue de pilotes. Par exemple, attribuez une catégorie précise à tous les pilotes de périphériques de carte réseau. Ensuite, quand vous créez une séquence de tâches qui comprend l’étape [Appliquer automatiquement les pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers), spécifiez une catégorie de pilotes de périphérique. Configuration Manager analyse ensuite le matériel et sélectionne les pilotes applicables de cette catégorie pour les activer sur le système et permettre à l’installation de Windows de les utiliser.  



## <a name="BKMK_ManagingDriverPackages"></a> Packages de pilotes

Regroupez des pilotes de périphérique similaires dans des packages pour simplifier les déploiements de systèmes d’exploitation. Par exemple, créez un package de pilotes pour chaque marque d’ordinateur présente sur votre réseau. Vous pouvez créer un package de pilotes en important directement des pilotes dans le nœud **Packages de pilotes** du catalogue de pilotes. Distribuez-le ensuite auprès des points de distribution. Les ordinateurs clients Configuration Manager pourront alors les installer. 

Considérations importantes :  

- Lors de la création d’un package de pilotes, son emplacement source doit pointer sur un partage réseau vide et non utilisé par un autre package de pilotes. Le fournisseur SMS doit avoir des autorisations de type **Contrôle total** sur cet emplacement.  

- Lorsqu’un pilote de périphérique est ajouté à un package de pilotes, Configuration Manager le copie à l’emplacement source du package. Seuls les pilotes de périphérique qui ont été importés et sont activés dans le catalogue de pilotes peuvent être ajoutés à un package de pilotes.  

- Il est possible de copier un sous-ensemble des pilotes de périphérique d’un package de pilotes existant. Tout d’abord, créez un package de pilotes. Ensuite, ajoutez le sous-ensemble de pilotes de périphérique au nouveau package, puis distribuez le nouveau package auprès d’un point de distribution.  

- Si vous prévoyez d’installer des pilotes en utilisant des séquences de tâches, créez des packages de pilotes qui contiennent moins de 500 pilotes de périphérique.


### <a name="BKMK_CreatingDriverPackages"></a> Créer un package de pilotes  

> [!IMPORTANT]  
> Pour créer un package de pilotes, vous devez disposer d’un dossier réseau vide et non utilisé par un autre package de pilotes. Dans la plupart des cas, créez un nouveau dossier avant de commencer cette procédure.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Packages de pilotes**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Créer un package de pilotes** dans le groupe **Créer**.  

3. Donnez un **Non** descriptif au package de pilotes.  

4. Entrez un **Commentaire** facultatif sur le package de pilotes. Utilisez cette description pour fournir des informations sur son contenu ou son usage.  

5. Dans la zone **Chemin d'accès** , spécifiez un dossier source vide pour le package de pilotes. Chaque package de pilotes doit utiliser un dossier unique. Ce chemin d’accès est requis comme emplacement réseau.  

   > [!IMPORTANT]  
   > Le compte de serveur de site doit disposer d’autorisations de type **Contrôle total** dans le dossier source spécifié.  

Le nouveau package de pilotes ne contient aucun pilote. L’étape suivante consiste à en ajouter.  

Si le nœud **Packages de pilotes** contient plusieurs packages, vous pouvez ajouter des dossiers au nœud pour séparer les packages en groupes logiques.  


### <a name="BKMK_PackageActions"></a> Actions supplémentaires concernant les packages de pilotes  

Vous pouvez effectuer des actions supplémentaires de gestion des packages de pilotes en en sélectionnant un ou plusieurs dans le nœud **Packages de pilotes**. 


#### <a name="create-prestage-content-file"></a>Créer un fichier de contenu préparé
Crée des fichiers permettant d’importer manuellement le contenu et les métadonnées associées. Utilisez du contenu préparé lorsque vous avez une bande passante réseau faible entre le serveur de site et les points de distribution sur lesquels est stocké le package de pilotes.

#### <a name="delete"></a>Supprimer
Supprime le package de pilotes du nœud **Packages de pilotes** .

#### <a name="distribute-content"></a>Distribuer du contenu
Distribue le package de pilotes sur des points de distribution, des groupes de points de distribution et des groupes de points de distribution associés à des regroupements.

#### <a name="manage-access-accounts"></a>Gérer des comptes d'accès
Ajoute, modifie ou supprime des comptes d'accès pour le package de pilotes.

Pour plus d’informations sur les comptes d’accès au package, voir [Comptes utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).

#### <a name="move"></a>Déplacer
Déplace le package de pilotes vers un autre dossier dans le nœud **Packages de pilotes** .

#### <a name="update-distribution-points"></a>Mise à jour des points de distribution
Met à jour le package de pilotes de périphérique sur tous les points de distribution sur lesquels le package est stocké. Cette action copie uniquement le contenu qui a été modifié après sa dernière distribution.

#### <a name="properties"></a>Propriétés
Ouvre la boîte de dialogue **Propriétés**. Passez en revue et modifiez le contenu et les propriétés du pilote. Par exemple, modifiez son nom et sa description, activez ou désactivez-le et spécifiez sur quelles plateformes il peut s’exécuter. 

<!--3607716, fka 1358270--> Depuis la version 1810, les packages de pilotes comptent des champs de métadonnées **Fabricant** et **Modèle**. Servez-vous de ces champs pour étiqueter les packages de pilotes avec des informations dans le but de faciliter les tâches de nettoyage ou d’identifier les pilotes périmés ou en double que vous pouvez supprimer. Sous l’onglet **Général**, sélectionnez une valeur existante dans les listes déroulantes ou entrez une chaîne pour créer une entrée. 

Dans le nœud **Packages de pilotes**, ces champs se présentent dans la liste sous forme de colonnes, **Fabricant du pilote** et **Modèle du pilote**. Ils peuvent aussi être utilisés comme critères de recherche. 



## <a name="BKMK_DeviceDrivers"></a> Pilotes d'appareils

Il est possible d’installer des pilotes de périphérique sur des ordinateurs de destination sans les inclure dans l’image de système d’exploitation déployée. Configuration Manager propose un catalogue de pilotes qui contient des références à tous les pilotes de périphérique importés dans Configuration Manager. Le catalogue de pilotes se trouve dans l’espace de travail **Bibliothèque de logiciels** et est composé de deux nœuds : **pilotes** et **packages de pilotes**. Le nœud **Pilotes** liste tous les pilotes importés dans le catalogue de pilotes.  


### <a name="BKMK_ImportDrivers"></a> Importer des pilotes de périphérique dans le catalogue de pilotes  

Pour pouvoir utiliser un pilote au déploiement d’un système d’exploitation, importez-le dans le catalogue de pilotes. Dans un souci de bonne gestion, importez seulement les pilotes que vous prévoyez d’installer dans le cadre de vos déploiements de systèmes d’exploitation. Stockez plusieurs versions de pilotes dans le catalogue pour pouvoir mettre à niveau des pilotes existants en toute simplicité lorsque la configuration matérielle requise évolue sur votre réseau.  

Dans le cadre du processus d’importation du pilote de périphérique, Configuration Manager lit les propriétés suivantes sur le pilote :
- Fournisseur
- Class
- Version
- Signature
- Matériel pris en charge
- Informations sur les plateformes prises en charge

Par défaut, le nom du pilote repose sur celui du premier périphérique matériel pris en charge. Il est possible de renommer le pilote de périphérique par la suite. La liste des plates-formes prises en charge est basée sur les informations dans le fichier INF du pilote. Comme l’exactitude de ces informations peut varier, vérifiez manuellement que le pilote est pris en charge après l’avoir importé dans le catalogue.  

Après avoir importé des pilotes de périphérique dans le catalogue, ajoutez-les à des packages de pilotes ou à des packages d’images de démarrage.  

> [!IMPORTANT]  
> Il n’est pas possible d’importer directement des pilotes de périphérique dans un sous-dossier du nœud **Pilotes**. Pour importer un pilote de périphérique dans un sous-dossier, importez-le d'abord dans le nœud **Pilotes** , puis déplacez-le dans le sous-dossier.  


#### <a name="process-to-import-windows-device-drivers-into-the-driver-catalog"></a>Processus d’importation de pilotes de périphériques Windows dans le catalogue de pilotes  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Pilotes**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Importer un pilote** dans le groupe **Créer** pour lancer **l’Assistant Importation de nouveau pilote**.  

3. Sur la page **Trouver le pilote**, spécifiez les options suivantes :  

    - **Importer tous les pilotes dans le chemin réseau (UNC) suivant** : pour importer tous les pilotes de périphérique dans un dossier spécifique, spécifiez son chemin d’accès réseau. Par exemple : `\\servername\share\folder`.  

        > [!NOTE]  
        > En présence de nombreux sous-dossiers et fichiers INF de pilotes, ce processus est susceptible de prendre le temps.  

    - **Importer un pilote spécifique** : pour importer un certain pilote à partir d’un dossier, spécifiez le chemin d’accès réseau vers le fichier .INF du pilote de périphérique Windows.  

    - **Spécifier l’option pour les pilotes dupliqués** : choisissez comment vous voulez que Configuration Manager gère les catégories de pilote en cas d’importation d’un pilote de périphérique en double :  
        - **Importer le pilote et ajouter une catégorie aux catégories existantes**  
        - **Importer le pilote et conserver les catégories existantes**  
        - **Importer le pilote et remplacer les catégories existantes**  
        - **Ne pas importer le pilote**  

    > [!IMPORTANT]  
    > Lorsque vous importez des pilotes, le serveur de site doit disposer de l'autorisation **Lecture** pour le dossier, sinon l'importation échoue.  

4. Sur la page **Détails du pilote**, spécifiez les options suivantes :  

    - **Masquer les pilotes hors classe de stockage ou réseau (pour les images de démarrage)** : utilisez ce paramètre pour afficher seulement les pilotes réseau et les pilotes de stockage. Cette option masque les autres pilotes qui ne sont généralement pas nécessaires pour les images de démarrage, comme les pilotes vidéo et les pilotes de modem.  

    - **Masquer les pilotes qui ne sont pas signés numériquement** : Microsoft recommande de n’utiliser que des pilotes signés numériquement.  

    - Dans la liste des pilotes, sélectionnez les pilotes que vous souhaitez importer dans le catalogue de pilotes.  

    - **Activer ces pilotes et autoriser leur installation sur les ordinateurs** : sélectionnez ce paramètre pour laisser les ordinateurs installer les pilotes de périphérique. Cette option est activée par défaut.  

        > [!IMPORTANT]  
        > Si un pilote de périphérique pose problème ou que vous souhaitez suspendre l’installation d’un pilote de périphérique, désactivez-le lors de l’importation. Vous pouvez également le désactiver après importation.  

    - Pour attribuer aux pilotes de périphérique une catégorie administrative à des fins de filtrage, par exemple « Ordinateurs de bureau » ou « Ordinateurs portables », sélectionnez **Catégories**. Ensuite, choisissez une catégorie ou en créez-en une nouvelle. Utilisez des catégories pour contrôler quels pilotes de périphérique sont concernés par l’étape de séquence de tâches [Appliquer automatiquement les pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers).  

5. Sur la page **Ajouter un pilote aux packages**, choisissez si vous souhaitez ajouter les pilotes à un package.  

    - Sélectionnez les packages de pilotes qui sont utilisés pour distribuer les pilotes de périphérique.  

        Si nécessaire, sélectionnez **Nouveau package** pour créer un nouveau package de pilotes. Lorsque vous créez un package de pilotes, indiquez un partage réseau non utilisé par d’autres packages de pilotes.  

    - Si le package a déjà été distribué auprès de points de distribution, sélectionnez **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Les pilotes de périphérique ne sont pas utilisables tant qu’ils ne sont pas distribués sur des points de distribution. Si vous sélectionnez **Non**, exécutez l’action **Mettre à jour le point de distribution** avant d’utiliser l’image de démarrage. Si le package de pilotes n’a jamais été distribué, il faut utiliser l’action **Distribuer du contenu** du nœud **Packages de pilotes**.  

6. Sur la page **Ajouter le pilote aux images de démarrage**, choisissez si vous souhaitez ajouter les pilotes de périphérique à des images de démarrage existantes.  

    > [!NOTE]  
    > N’ajoutez que des pilotes de stockage et des pilotes réseau aux images de démarrage.  

    - Sélectionnez **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Les pilotes de périphérique ne sont pas utilisables tant qu’ils ne sont pas distribués sur des points de distribution. Si vous sélectionnez **Non**, exécutez l’action **Mettre à jour le point de distribution** avant d’utiliser l’image de démarrage. Si le package de pilotes n’a jamais été distribué, il faut utiliser l’action **Distribuer du contenu** du nœud **Packages de pilotes**.  

    - Configuration Manager vous avertit si l’architecture d’un ou plusieurs pilotes ne correspond pas à celle des images de démarrage sélectionnées. Si elles ne correspondent pas, sélectionnez **OK**. Revenez à la page **Détails du pilote** pour effacer les pilotes qui ne correspondent pas à l’architecture de l’image de démarrage sélectionnée. Par exemple, si vous sélectionnez une image de démarrage x64 et x86, tous les pilotes doivent prendre en charge les deux architectures. Si vous sélectionnez une image de démarrage x64, tous les pilotes doivent prendre en charge l'architecture x 64.  

        > [!NOTE]  
        > - L’architecture est basée sur celle indiquée dans le fichier INF du fabricant.  
        > - Si un pilote indique qu’il prend en charge les deux architectures, vous pouvez l’importer dans n’importe quelle image de démarrage.  

    - Configuration Manager vous avertit si vous ajoutez des pilotes de périphérique qui ne sont pas des pilotes réseau ou des pilotes de stockage dans une image de démarrage. Dans la plupart des cas, ils ne sont pas nécessaires à l’image de démarrage. Sélectionnez **Oui** pour ajouter les pilotes à l’image de démarrage ou **Non** pour revenir en arrière et modifier votre sélection de pilotes.  

    - Configuration Manager vous avertit si un ou plusieurs pilotes sélectionnés ne sont pas signés numériquement. Sélectionnez **Oui** pour continuer ou **Non** pour revenir en arrière et apporter des modifications à votre sélection de pilotes.  

7. Effectuez toutes les étapes de l'Assistant.  


### <a name="BKMK_ModifyDriverPackage"></a> Gérer les pilotes de périphérique dans un package de pilotes  

Utilisez les procédures suivantes pour modifier les packages de pilotes et les images de démarrage. Pour ajouter ou supprimer un pilote, commencez par le localiser dans le nœud **Pilotes**. Ensuite, modifiez les packages ou les images de démarrage auxquelles le pilote sélectionné est associé.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Pilotes**.  

2. Sélectionnez les pilotes de périphérique que vous souhaitez ajouter à un package de pilotes.  

3. Sous l’onglet **Accueil** du ruban, sélectionnez **Modifier** dans le groupe **Pilote**, puis choisissez **Packages de pilotes**.  

4. Pour ajouter un pilote de périphérique, activez la case à cocher des packages de pilotes auxquels vous souhaitez ajouter les pilotes de périphérique. Pour supprimer un pilote de périphérique, désactivez la case à cocher des packages de pilotes desquels vous souhaitez supprimer le pilote de périphérique.  

    Si vous ajoutez des pilotes de périphérique associés à des packages de pilotes, vous pouvez si vous le souhaitez créer un package. Sélectionnez **Nouveau Package** pour ouvrir la boîte de dialogue **Nouveau package de pilotes**.  

5. Si le package a déjà été distribué auprès de points de distribution, sélectionnez **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Les pilotes de périphérique ne sont pas utilisables tant qu’ils ne sont pas distribués sur des points de distribution. Si vous sélectionnez **Non**, exécutez l’action **Mettre à jour le point de distribution** avant d’utiliser l’image de démarrage. Si le package de pilotes n’a jamais été distribué, il faut utiliser l’action **Distribuer du contenu** du nœud **Packages de pilotes**. Pour que les pilotes soient disponibles, vous devez mettre à jour le package de pilotes sur les points de distribution.  

    Sélectionnez **OK** lorsque vous avez terminé.  


### <a name="BKMK_ManageDriversBootImage"></a> Gérer les pilotes de périphérique dans une image de démarrage  

Vous pouvez ajouter à des images de démarrage des pilotes de périphérique Windows importés dans le catalogue de pilotes. Lorsque vous ajoutez des pilotes de périphérique à une image de démarrage, procédez comme suit :  

- N’ajoutez que des pilotes de stockage et des pilotes réseau aux images de démarrage. Les autres types de pilotes ne sont généralement pas obligatoires dans Windows PE. Les pilotes non requis augmentent inutilement la taille de l’image de démarrage.  

- N’ajoutez que les pilotes de périphérique de Windows 10 à une image de démarrage. La version requise de Windows PE est basée sur Windows 10.  

- Veillez à utiliser le pilote de périphérique adapté à l’architecture de l’image de démarrage. N’ajoutez pas un pilote de périphérique x86 à une image de démarrage x64.  

#### <a name="process-to-modify-the-device-drivers-associated-with-a-boot-image"></a>Processus de modification des pilotes de périphérique associés à une image de démarrage  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Pilotes**.  

2. Sélectionnez les pilotes de périphérique que vous souhaitez ajouter au package de pilotes.  

3. Sous l’onglet **Accueil** du ruban, sélectionnez **Modifier** dans le groupe **Pilote**, puis choisissez **Images de démarrage**.  

4. Pour ajouter un pilote de périphérique, activez la case à cocher de l'image de démarrage à laquelle vous souhaitez ajouter les pilotes de périphérique. Pour supprimer un pilote de périphérique, désactivez la case à cocher de l'image de démarrage de laquelle vous souhaitez supprimer le pilote de périphérique.  

5. Si vous ne souhaitez pas mettre à jour les points de distribution dans lesquels l’image de démarrage est stockée, décochez la case **Mettre à jour les points de distribution une fois terminé**. Par défaut, les points de distribution sont mis à jour lorsque l'image de démarrage est mise à jour.  

    - Sélectionnez **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Les pilotes de périphérique ne sont pas utilisables tant qu’ils ne sont pas distribués sur des points de distribution. Si vous sélectionnez **Non**, exécutez l’action **Mettre à jour le point de distribution** avant d’utiliser l’image de démarrage. Si le package de pilotes n’a jamais été distribué, il faut utiliser l’action **Distribuer du contenu** du nœud **Packages de pilotes**.  

    - Configuration Manager vous avertit si l’architecture d’un ou plusieurs pilotes ne correspond pas à celle des images de démarrage sélectionnées. Si elles ne correspondent pas, sélectionnez **OK**. Revenez à la page **Détails du pilote** pour effacer les pilotes qui ne correspondent pas à l’architecture de l’image de démarrage sélectionnée. Par exemple, si vous sélectionnez une image de démarrage x64 et x86, tous les pilotes doivent prendre en charge les deux architectures. Si vous sélectionnez une image de démarrage x64, tous les pilotes doivent prendre en charge l'architecture x 64.  

        > [!NOTE]
        > - L’architecture est basée sur celle indiquée dans le fichier INF du fabricant.  
        > - Si un pilote indique qu'il prend en charge les deux architectures, vous pouvez l'importer dans l'une ou l'autre image de démarrage.  

    - Configuration Manager vous avertit si vous ajoutez des pilotes de périphérique qui ne sont pas des pilotes réseau ou des pilotes de stockage dans une image de démarrage. Dans la plupart des cas, ils ne sont pas nécessaires à l’image de démarrage. Sélectionnez **Oui** pour ajouter les pilotes à l’image de démarrage ou **Non** pour revenir en arrière et modifier votre sélection de pilotes.  

    - Configuration Manager vous avertit si un ou plusieurs pilotes sélectionnés ne sont pas signés numériquement. Sélectionnez **Oui** pour continuer ou **Non** pour revenir en arrière et apporter des modifications à votre sélection de pilotes.  


### <a name="BKMK_DriverActions"></a> Actions supplémentaires concernant les pilotes de périphérique  

Vous pouvez effectuer des actions supplémentaires de gestion des pilotes en les sélectionnant dans le nœud **Pilotes**.  

#### <a name="categorize"></a>Catégoriser
Efface, gère ou définit une catégorie administrative pour les pilotes sélectionnés.

#### <a name="delete"></a>Supprimer
Supprime le pilote du nœud **Pilotes** et des points de distribution associés.

#### <a name="disable"></a>Désactiver
Empêche l’installation du pilote. Cette action le désactive temporairement. La séquence de tâches ne peut pas installer un pilote désactivé lors du déploiement d’un système d’exploitation. 

> [!Note]  
> Cette action n’empêche l’installation des pilotes que pendant l’étape **Appliquer automatiquement les pilotes** de la séquence de tâches.

#### <a name="enable"></a>Activez
Permet aux séquences de tâches et aux ordinateurs clients Configuration Manager d’installer le pilote de périphérique pendant le déploiement du système d’exploitation.

#### <a name="move"></a>Déplacer
Déplace le pilote de périphérique vers un autre dossier dans le nœud **Pilotes** .

#### <a name="properties"></a>Propriétés
Ouvre la boîte de dialogue **Propriétés**. Passez en revue et modifiez les propriétés du pilote. Par exemple, modifiez son nom et sa description, activez ou désactivez-le et spécifiez sur quelles plateformes il peut s’exécuter.



## <a name="BKMK_TSDrivers"></a> Utiliser des séquences de tâches pour installer des pilotes  

Utilisez des séquences de tâches pour automatiser le déploiement du système d’exploitation. Chaque étape de la séquence de tâches peut exécuter une action spécifique, comme installer un pilote. Vous pouvez utiliser les deux étapes de séquence de tâches suivantes pour installer des pilotes de périphériques lors du déploiement d’un système d’exploitation :  

- [Appliquer automatiquement les pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) : Cette étape permet de faire correspondre et d'installer automatiquement des pilotes de périphérique dans le cadre du déploiement d'un système d'exploitation. Vous pouvez configurer l’étape de la séquence de tâches de façon à installer uniquement le pilote le plus adapté à chaque périphérique matériel détecté. Sinon, demandez-lui d’installer tous les pilotes compatibles pour chaque périphérique matériel détecté et de laisser le programme d’installation de Windows choisir le meilleur. Vous pouvez également spécifier une catégorie de pilotes de périphérique afin de limiter les pilotes disponibles à cette étape.  

- [Appliquer le package de pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) : Cette étape permet de mettre tous les pilotes de périphérique d'un package de pilotes spécifique à la disposition du programme d'installation de Windows. Dans les packages de pilotes spécifiés, le programme d'installation de Windows recherche les pilotes de périphérique qui sont nécessaires. Quand vous créez un média autonome, vous devez utiliser cette étape pour installer les pilotes de périphérique.  

Lorsque vous utilisez ces étapes de séquence de tâches, vous pouvez également spécifier la manière dont les pilotes sont installés sur l’ordinateur au moment du déploiement du système d’exploitation. Pour plus d’informations, consultez [Gérer les séquences de tâches pour automatiser des tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="BKMK_DriverReports"></a> Rapports de pilotes  

Vous pouvez utiliser plusieurs rapports dans la catégorie des rapports **Gestion des pilotes** pour déterminer des informations générales sur les pilotes de périphérique dans le catalogue de pilotes. Pour plus d’informations sur les rapports, consultez [Rapports](/sccm/core/servers/manage/reporting).

