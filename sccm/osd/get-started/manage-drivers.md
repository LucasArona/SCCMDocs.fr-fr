---
title: 'Gérer les pilotes '
titleSuffix: Configuration Manager
description: Le catalogue de pilotes Configuration Manager permet d’importer des pilotes de périphérique, de les regrouper dans des packages et de distribuer ces packages à des points de distribution.
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4eb97430bd5d7ae5cc50044f8049f41cb9b4cf08
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351528"
---
# <a name="manage-drivers-in-system-center-configuration-manager"></a>Gérer les pilotes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager propose un catalogue de pilotes qui permet de gérer les pilotes de périphérique Windows dans l’environnement Configuration Manager. Vous pouvez utiliser le catalogue de pilotes pour importer des pilotes de périphérique dans Configuration Manager, les regrouper dans des packages et distribuer ces packages à des points de distribution accessibles pendant le déploiement d’un système d’exploitation. Des pilotes de périphérique peuvent être utilisés lorsque vous installez le système d'exploitation complet sur l'ordinateur de destination et lorsque vous installez Windows PE à l'aide d'une image de démarrage. Les pilotes de périphérique Windows sont composés d'un fichier d'informations d'installation (INF) et de tous les autres fichiers nécessaires à la prise en charge du périphérique. À cette occasion, Configuration Manager obtient les informations matérielles et de plateforme du périphérique à partir de son fichier INF. Pour gérer les pilotes dans votre environnement Configuration Manager, aidez-vous des sections suivantes.

##  <a name="BKMK_DriverCategories"></a> Catégories de pilotes de périphériques  
 Lorsque vous importez des pilotes de périphérique, vous pouvez affecter les pilotes de périphérique à une catégorie. Les catégories de pilotes de périphérique permettent de regrouper les pilotes de périphérique utilisés de la même façon dans le catalogue de pilotes. Par exemple, vous pouvez attribuer tous les pilotes de périphériques de carte réseau à une catégorie précise. Ensuite, quand vous créez une séquence de tâches qui comprend l’étape [Appliquer automatiquement les pilotes](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers), vous pouvez spécifier une catégorie spécifique de pilotes de périphérique. Configuration Manager analyse ensuite le matériel et sélectionne les pilotes applicables de cette catégorie pour les activer sur le système et permettre à l’installation de Windows de les utiliser.  

##  <a name="BKMK_ManagingDriverPackages"></a> Packages de pilotes  
 Vous pouvez regrouper des pilotes de périphérique similaires dans des packages pour simplifier les déploiements de systèmes d’exploitation. Par exemple, vous pouvez décider de créer un package de pilotes pour chaque marque d’ordinateur présente sur votre réseau. Vous pouvez créer un package de pilotes pendant que vous importez des pilotes dans le catalogue de pilotes directement dans le nœud **Packages de pilotes** . Une fois le package de pilotes créé, il doit être distribué aux points de distribution à partir desquels les ordinateurs clients Configuration Manager peuvent installer les pilotes, le cas échéant. Considérez les points suivants :  

-   Lorsque vous créez un package de pilotes, l'emplacement source du package doit pointer sur un partage réseau vide qui n'est pas utilisé par un autre package de pilotes et le fournisseur SMS doit disposer d'autorisations en lecture et en écriture sur cet emplacement.  

-   Quand vous ajoutez des pilotes de périphérique à un package de pilotes, Configuration Manager copie le pilote de périphérique à l’emplacement source du package de pilotes. Vous pouvez ajouter uniquement les pilotes de périphérique qui ont été importés et qui sont activés dans le catalogue de pilotes vers un package de pilotes.  

-   Pour copier un sous-ensemble de pilotes de périphérique à partir d'un package de pilotes existant, créez un nouveau package de pilotes, ajoutez-y le sous-ensemble de pilotes de périphérique, puis distribuez le nouveau package à un point de distribution.  

 Pour savoir comment créer et gérer des packages de pilotes, consultez les sections suivantes.  

###  <a name="CreatingDriverPackages"></a> Créer un package de pilotes  
 Utilisez la procédure ci-dessous pour créer un package de pilotes.  

> [!IMPORTANT]  
>  Pour créer un package de pilotes, vous devez disposer d'un dossier réseau vide qui n'est pas utilisé par un autre package de pilotes. Dans la plupart des cas, vous devez créer un nouveau dossier avant de lancer cette procédure.  

> [!NOTE]  
>  Si vous prévoyez d’installer des pilotes en utilisant des séquences de tâches, créez des packages de pilotes qui contiennent moins de 500 pilotes de périphérique.  

 Utilisez la procédure suivante pour créer un package de pilotes.  

#### <a name="to-create-a-driver-package"></a>Pour créer un package de pilotes  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Packages de pilotes**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un package de pilotes**.  

4.  Dans la zone **Nom** , spécifiez un nom descriptif pour le package de pilotes.  

5.  Dans la zone **Commentaire** , entrez une description facultative pour le package de pilotes. Vérifiez que la description fournit des informations sur le contenu ou l'objectif du package de pilotes.  

6.  Dans la zone **Chemin d'accès** , spécifiez un dossier source vide pour le package de pilotes. Entrez le chemin d'accès vers le dossier source au format UNC (Universal Naming Convention). Chaque package de pilotes doit utiliser un dossier unique.  

    > [!IMPORTANT]  
    >  Le compte de serveur de site doit disposer des autorisations en **lecture** et en **écriture** dans le dossier source spécifié.  

 Le nouveau package de pilotes ne contient aucun pilote. L'étape suivante consiste à ajouter des pilotes au package.  

 Si le nœud **Packages de pilotes** contient plusieurs packages, vous pouvez ajouter des dossiers au nœud pour séparer les packages en groupes logiques.  

###  <a name="BKMK_PackageActions"></a> Actions supplémentaires concernant les packages de pilotes  
 Vous pouvez effectuer des actions supplémentaires pour gérer les packages de pilotes lorsque vous sélectionnez un ou plusieurs packages de pilotes dans le nœud **Packages de pilotes** . Ces actions incluent :  

|Action|Description|  
|------------|-----------------|  
|**Créer un fichier de contenu préparé**|Crée des fichiers qui peuvent être utilisés pour importer manuellement le contenu et ses métadonnées associées. Utilisez du contenu préparé lorsque vous avez une bande passante réseau faible entre le serveur de site et les points de distribution sur lesquels est stocké le package de pilotes.|  
|**Supprimer**|Supprime le package de pilotes du nœud **Packages de pilotes** .|  
|**Distribuer du contenu**|Distribue le package de pilotes sur des points de distribution, des groupes de points de distribution et des groupes de points de distribution associés à des regroupements.|  
|**Gérer des comptes d'accès**|Ajoute, modifie ou supprime des comptes d'accès pour le package de pilotes.<br /><br /> Pour plus d’informations sur les comptes d’accès au package, consultez [Comptes utilisés dans Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Déplacer**|Déplace le package de pilotes vers un autre dossier dans le nœud **Packages de pilotes** .|  
|**Mise à jour des points de distribution**|Met à jour le package de pilotes de périphérique sur tous les points de distribution sur lesquels le package est stocké. Cette action copie uniquement le contenu qui a été modifié après sa dernière distribution.|  
|**Propriétés**|Ouvre la boîte de dialogue **Propriétés** dans laquelle vous pouvez examiner et modifier le contenu et les propriétés du pilote de périphérique. Par exemple, vous pouvez modifier le nom et la description du pilote de périphérique, activer le pilote de périphérique et spécifier les plates-formes sur lesquelles le pilote de périphérique peut être exécuté.|  

##  <a name="BKMK_DeviceDrivers"></a> Pilotes d'appareils  
 Vous pouvez installer des pilotes de périphérique sur les ordinateurs de destination sans les inclure dans l'image du système d'exploitation déployée. Configuration Manager propose un catalogue de pilotes qui contient les références à tous les pilotes de périphérique que vous importez dans Configuration Manager. Le catalogue de pilotes se trouve dans l’espace de travail **Bibliothèque de logiciels** et est composé de deux nœuds : **Pilotes** et **Packages de pilotes**. Le nœud **Pilotes** répertorie tous les pilotes que vous avez importés dans le catalogue de pilotes. Ce nœud vous permet de découvrir les détails relatifs à chaque pilote importé, de modifier les pilotes contenus dans un package de pilotes ou une image de démarrage, d’activer ou désactiver un pilote, etc.  

###  <a name="BKMK_ImportDrivers"></a> Importer des pilotes de périphérique dans le catalogue de pilotes  
 Vous devez importer les pilotes de périphérique dans le catalogue de pilotes avant de pouvoir les utiliser lorsque vous déployez un système d'exploitation. Pour mieux gérer vos pilotes de périphérique, importez uniquement les pilotes de périphérique que vous prévoyez d'installer dans le cadre du déploiement de votre système d'exploitation. Toutefois, vous pouvez également stocker plusieurs versions de pilotes de périphérique dans le catalogue de périphériques afin de mettre facilement à niveau des pilotes de périphérique existants lorsque la configuration matérielle requise en matière de périphériques évolue sur votre réseau.  

 Pendant le processus d’importation de pilote de périphérique, Configuration Manager lit le fournisseur, la classe, la version, la signature, le matériel pris en charge et les informations de plateforme prises en charge associées au périphérique. Par défaut, le nom du pilote repose sur celui du premier périphérique matériel pris en charge ; toutefois, le pilote de périphérique peut être renommé par la suite. La liste des plates-formes prises en charge est basée sur les informations dans le fichier INF du pilote. Comme l'exactitude de ces informations peut varier, vérifiez manuellement que le pilote de périphérique est pris en charge une fois qu'il est importé dans le catalogue de pilotes.  

 Après avoir importé des pilotes de périphérique dans le catalogue, vous pouvez les ajouter à des packages de pilotes ou à des packages d’images de démarrage.  

> [!IMPORTANT]  
>  Vous ne pouvez pas importer des pilotes de périphérique directement dans un sous-dossier du nœud **Pilotes** . Pour importer un pilote de périphérique dans un sous-dossier, importez-le d'abord dans le nœud **Pilotes** , puis déplacez-le dans le sous-dossier.  

 Utilisez la procédure suivante pour importer des pilotes de périphérique Windows.  

#### <a name="to-import-windows-device-drivers-into-the-driver-catalog"></a>Pour importer des pilotes de périphérique Windows dans le catalogue de pilotes  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Pilotes**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Importer un pilote** pour démarrer l' **Assistant Importation de nouveau pilote**.  

4.  Sur la page **Trouver le pilote** , spécifiez les options suivantes et cliquez sur **Suivant**:  

    -   **Importer tous les pilotes dans le chemin réseau (UNC) suivant**: Pour importer tous les pilotes de périphérique qui sont contenus dans un dossier spécifique, spécifiez le chemin d'accès réseau vers le dossier de pilote de périphérique. Par exemple :  **\\\\nom_serveur\dossier**.  

        > [!NOTE]  
        >  Le processus d’importation de l’ensemble des pilotes peut prendre un certain temps en présence d’un grand nombre de dossiers et de fichiers de pilote (.inf).  

    -   **Importer un pilote spécifique**: pour importer un pilote spécifique à partir d’un dossier, spécifiez le chemin réseau (UNC) vers le fichier .INF du pilote de périphérique Windows ou le fichier Txtsetup.oem de stockage de masse du pilote.  

    -   **Spécifier l’option pour les pilotes dupliqués** : indiquez comment vous voulez que Configuration Manager gère les catégories de pilotes pendant l’importation d’un pilote de périphérique en double.  

    > [!IMPORTANT]  
    >  Lorsque vous importez des pilotes, le serveur de site doit disposer de l'autorisation **Lecture** pour le dossier, sinon l'importation échoue.  

5.  Sur la page **Détails du pilote** , spécifiez les options suivantes et cliquez sur **Suivant**:  

    -   **Masquer les pilotes hors classe de stockage ou réseau (pour les images de démarrage)**: ce paramètre permet d’afficher uniquement les pilotes réseau et de stockage, et de masquer les autres pilotes qui ne sont généralement pas nécessaires pour les images de démarrage, tels que les pilotes vidéo ou les pilotes de modem.  

    -   **Masquer les pilotes qui ne sont pas signés numériquement**: ce paramètre permet de masquer les pilotes qui ne sont pas signés numériquement.  

    -   Dans la liste des pilotes, sélectionnez les pilotes que vous souhaitez importer dans le catalogue de pilotes.  

    -   **Activer ces pilotes et autoriser leur installation sur les ordinateurs**: sélectionnez ce paramètre pour laisser les ordinateurs installer les pilotes de périphérique. Par défaut, cette case à cocher est activée.  

        > [!IMPORTANT]  
        >  Si un pilote de périphérique est à l'origine d'un problème, ou si vous souhaitez suspendre l'installation d'un pilote de périphérique, vous pouvez désactiver le pilote de périphérique en désactivant la case à cocher **Activer ces pilotes et autoriser leur installation sur les ordinateurs** . Vous pouvez également désactiver les pilotes après leur importation.  

    -   Pour attribuer les pilotes de périphérique à une catégorie administrative à des fins de filtrage, telle que « Postes de travail » ou « Ordinateurs portables », cliquez sur **Catégories** et sélectionnez une catégorie existante ou créez-en une nouvelle. Vous pouvez aussi utiliser l’attribution de catégorie pour configurer les pilotes de périphérique qui s’appliquent au déploiement avec l’étape de séquence de tâches [Appliquer automatiquement les pilotes](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers).  

6.  Dans la page **Ajouter un pilote aux packages** , choisissez d’ajouter ou non les pilotes à un package, puis cliquez sur **Suivant**. Tenez compte des points suivants avant d’ajouter les pilotes à un package :  

    -   Sélectionnez les packages de pilotes qui sont utilisés pour distribuer les pilotes de périphérique.  

         Si vous le souhaitez, cliquez sur **Nouveau package** pour créer un nouveau package de pilotes. Lorsque vous créez un nouveau package de pilotes, vous devez fournir un partage réseau qui n'est pas en cours d'utilisation par d'autres packages de pilotes.  

    -   Si le package a déjà été distribué à des points de distribution, cliquez sur **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Vous ne pouvez pas utiliser les pilotes de périphérique tant qu'ils ne sont pas distribués sur des points de distribution. Si vous cliquez sur **Non**, vous devez exécuter l'action **Mettre à jour les points de distribution** pour que l'image de démarrage contienne les pilotes mis à jour. Si le package de pilotes n'a jamais été distribué, vous devez cliquer sur **Distribuer du contenu** à partir du nœud **Packages de pilotes** .  

7.  Dans la page **Ajouter un pilote aux images de démarrage** , choisissez éventuellement d’ajouter les pilotes de périphérique aux images de démarrage existantes, puis cliquez sur **Suivant**. Si vous sélectionnez une image de démarrage, tenez compte des points suivants :  

    > [!NOTE]  
    >  En guise de meilleure pratique, vous devez ajouter uniquement les pilotes de périphérique de stockage de masse et les pilotes de périphérique réseau aux images de démarrage dans les scénarios de déploiement de systèmes d'exploitation.  

    -   Cliquez sur **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Vous ne pouvez pas utiliser les pilotes de périphérique tant qu'ils ne sont pas distribués sur des points de distribution. Si vous cliquez sur **Non**, vous devez exécuter l'action **Mettre à jour les points de distribution** pour que l'image de démarrage contienne les pilotes mis à jour. Si le package de pilotes n'a jamais été distribué, vous devez cliquer sur **Distribuer du contenu** à partir du nœud **Packages de pilotes** .  

    -   Configuration Manager vous avertit si l’architecture d’un ou plusieurs pilotes ne correspond pas à celle des images de démarrage que vous avez sélectionnées. Si elles ne correspondent pas, cliquez sur **OK** et revenez à la page **Détails du pilote** pour effacer les pilotes qui ne correspondent pas à l'architecture de l'image de démarrage sélectionnée. Par exemple, si vous sélectionnez une image de démarrage x64 et x86, tous les pilotes doivent prendre en charge les deux architectures. Si vous sélectionnez une image de démarrage x64, tous les pilotes doivent prendre en charge l'architecture x 64.  

        > [!NOTE]  
        >  -   L'architecture est basée sur l'architecture signalée dans le fichier .INF du fabricant.  
        > -   Si un pilote indique qu'il prend en charge les deux architectures, vous pouvez l'importer dans l'une ou l'autre image de démarrage.  

    -   Configuration Manager vous avertit si les pilotes de périphérique que vous ajoutez à une image de démarrage ne sont ni des pilotes réseau ni des pilotes de stockage, car dans la plupart des cas ils ne sont pas nécessaires pour l’image de démarrage. Cliquez sur **Oui** pour ajouter les pilotes à l'image de démarrage ou sur **Non** pour revenir en arrière et modifier votre sélection de pilote.  

    -   Configuration Manager vous avertit si un ou plusieurs pilotes sélectionnés ne sont pas correctement signés numériquement. Cliquez sur **Oui** pour continuer ou sur **Non** pour revenir en arrière et apporter des modifications à votre sélection de pilote.  

8.  Effectuez toutes les étapes de l'Assistant.  

###  <a name="BKMK_ModifyDriverPackage"></a> Gérer les pilotes de périphérique dans un package de pilotes  
 Utilisez les procédures suivantes pour modifier les packages de pilotes et les images de démarrage. Pour ajouter ou supprimer des pilotes de périphérique, recherchez les pilotes dans le nœud **Pilotes** , puis modifiez les packages ou les images de démarrage auxquels les pilotes sélectionnés sont associés.  

#### <a name="to-modify-the-device-drivers-in-a-driver-package"></a>Pour modifier les pilotes de périphérique dans un package de pilotes  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Pilotes**.  

3.  Dans le nœud **Pilotes** , sélectionnez les pilotes de périphérique que vous souhaitez ajouter au package de pilotes.  

4.  Dans l'onglet **Accueil** , dans le groupe **Pilote** , cliquez sur **Modifier**, puis sur **Packages de pilotes**.  

5.  Pour ajouter un pilote de périphérique, activez la case à cocher des packages de pilotes auxquels vous souhaitez ajouter les pilotes de périphérique. Pour supprimer un pilote de périphérique, désactivez la case à cocher des packages de pilotes desquels vous souhaitez supprimer le pilote de périphérique.  

     Si vous ajoutez des pilotes de périphérique associés à des packages de pilotes, vous pouvez éventuellement créer un nouveau package en cliquant sur **Nouveau package**qui ouvre la boîte de dialogue **Nouveau package de pilotes** .  

6.  Si le package a déjà été distribué à des points de distribution, cliquez sur **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Vous ne pouvez pas utiliser les pilotes de périphérique tant qu'ils ne sont pas distribués sur des points de distribution. Si vous cliquez sur **Non**, vous devez exécuter l'action **Mettre à jour les points de distribution** pour que l'image de démarrage contienne les pilotes mis à jour. Si le package de pilotes n'a jamais été distribué, vous devez cliquer sur **Distribuer du contenu** à partir du nœud **Packages de pilotes** . Pour que les pilotes soient disponibles, vous devez mettre à jour le package de pilotes sur les points de distribution.  

     Cliquez sur **OK**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Gérer les pilotes de périphérique dans une image de démarrage  
 Vous pouvez ajouter des pilotes de périphérique Windows qui ont été importés dans le catalogue de pilotes à des images de démarrage . Lorsque vous ajoutez des pilotes de périphérique à une image de démarrage, procédez comme suit :  

-   Ajoutez uniquement les pilotes de périphérique de stockage de masse et de carte réseau aux images de démarrage, car les autres types de pilotes ne sont généralement pas requis. Les pilotes qui ne sont pas requis augmentent inutilement la taille de l'image de démarrage.  

-   Ajoutez uniquement les pilotes de périphérique pour Windows 10 à une image de démarrage, car la version requise de Windows PE est basée sur Windows 10.  

-   Assurez-vous que vous utilisez le pilote de périphérique correct pour l'architecture de l'image de démarrage.  N'ajoutez pas un pilote de périphérique x86 à une image de démarrage x64.  

 Pour ajouter ou supprimer des pilotes de périphérique dans une image de démarrage, procédez comme suit :  

#### <a name="to-modify-the--device-drivers-associated-with-a-boot-image"></a>Pour modifier les pilotes de périphérique associés à une image de démarrage  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Pilotes**.  

3.  Dans le nœud **Pilotes** , sélectionnez les pilotes de périphérique que vous souhaitez ajouter au package de pilotes.  

4.  Dans l'onglet **Accueil** , dans le groupe **Pilote** , cliquez sur **Modifier**, puis sur **Images de démarrage**.  

5.  Pour ajouter un pilote de périphérique, activez la case à cocher de l'image de démarrage à laquelle vous souhaitez ajouter les pilotes de périphérique. Pour supprimer un pilote de périphérique, désactivez la case à cocher de l'image de démarrage de laquelle vous souhaitez supprimer le pilote de périphérique.  

6.  Si vous ne souhaitez pas mettre à jour les points de distribution dans lesquels l'image de démarrage est stockée, désactivez la case à cocher **Mettre à jour les points de distribution une fois terminé** . Par défaut, les points de distribution sont mis à jour lorsque l'image de démarrage est mise à jour.  

     Cliquez sur **OK** et tenez compte des points suivants :  

    -   Cliquez sur **Oui** dans la boîte de dialogue pour mettre à jour les images de démarrage sur les points de distribution. Vous ne pouvez pas utiliser les pilotes de périphérique tant qu'ils ne sont pas distribués sur des points de distribution. Si vous cliquez sur **Non**, vous devez exécuter l'action **Mettre à jour les points de distribution** pour que l'image de démarrage contienne les pilotes mis à jour. Si le package de pilotes n'a jamais été distribué, vous devez cliquer sur **Distribuer du contenu** à partir du nœud **Packages de pilotes** .  

    -   Configuration Manager vous avertit si l’architecture d’un ou plusieurs pilotes ne correspond pas à celle des images de démarrage que vous avez sélectionnées. Si elles ne correspondent pas, cliquez sur **OK** et revenez à la page **Détails du pilote** pour effacer les pilotes qui ne correspondent pas à l'architecture de l'image de démarrage sélectionnée. Par exemple, si vous sélectionnez une image de démarrage x64 et x86, tous les pilotes doivent prendre en charge les deux architectures. Si vous sélectionnez une image de démarrage x64, tous les pilotes doivent prendre en charge l'architecture x 64.  

        > [!NOTE]  
        >  -   L'architecture est basée sur l'architecture signalée dans le fichier .INF du fabricant.  
        > -   Si un pilote indique qu'il prend en charge les deux architectures, vous pouvez l'importer dans l'une ou l'autre image de démarrage.  

    -   Configuration Manager vous avertit si les pilotes de périphérique que vous ajoutez à une image de démarrage ne sont ni des pilotes réseau ni des pilotes de stockage, car dans la plupart des cas ils ne sont pas nécessaires pour l’image de démarrage. Cliquez sur **Oui** pour ajouter les pilotes à l'image de démarrage ou sur **Non** pour revenir en arrière et modifier votre sélection de pilote.  

    -   Configuration Manager vous avertit si un ou plusieurs pilotes sélectionnés ne sont pas correctement signés numériquement. Cliquez sur **Oui** pour continuer ou sur **Non** pour revenir en arrière et apporter des modifications à votre sélection de pilote.  

7.  Cliquez sur **OK**.  

###  <a name="BKMK_DriverActions"></a> Actions supplémentaires concernant les pilotes de périphérique  
 Vous pouvez effectuer des actions supplémentaires pour gérer les pilotes de périphérique lorsque vous sélectionnez un ou plusieurs pilotes de périphérique dans le nœud **Pilotes** . Ces actions incluent :  

|Action|Description|  
|------------|-----------------|  
|**Catégoriser**|Efface, gère ou définit une catégorie administrative pour les pilotes de périphérique sélectionnés.|  
|**Supprimer**|Supprime le pilote de périphérique du nœud **Pilotes** et supprime également le pilote des points de distribution associés.|  
|**Désactiver**|Empêche l'installation du pilote de périphérique. Vous pouvez désactiver temporairement les pilotes de périphérique pour que les ordinateurs clients et les séquences de tâches Configuration Manager ne puissent pas les installer quand vous déployez des systèmes d’exploitation. **Remarque :**  L’action Désactiver empêche seulement les pilotes de s’installer en utilisant la séquence de tâches Appliquer automatiquement les pilotes.|  
|**Activer**|Permet aux ordinateurs clients et aux séquences de tâches Configuration Manager d’installer le pilote de périphérique pendant le déploiement du système d’exploitation.|  
|**Déplacer**|Déplace le pilote de périphérique vers un autre dossier dans le nœud **Pilotes** .|  
|**Propriétés**|Ouvre la boîte de dialogue **Propriétés** dans laquelle vous pouvez examiner et modifier les propriétés du pilote de périphérique. Par exemple, vous pouvez modifier le nom et la description du pilote de périphérique, activer le pilote de périphérique et spécifier les plates-formes sur lesquelles le pilote de périphérique peut être exécuté.|  

##  <a name="BKMK_TSDrivers"></a> Utiliser des séquences de tâches pour installer des pilotes de périphérique  
 Utilisez des séquences de tâches pour automatiser le déploiement du système d'exploitation. Chaque étape de la séquence de tâches peut exécuter une action spécifique, telle que l'installation d'un pilote de périphérique. Vous pouvez utiliser les étapes de séquence de tâches suivantes pour installer les pilotes de périphériques pendant que vous déployez des systèmes d'exploitation :  

-   [Appliquer automatiquement les pilotes](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) : cette étape permet de faire correspondre et d’installer automatiquement des pilotes de périphérique pendant le déploiement d’un système d’exploitation. Vous pouvez configurer l'étape de la séquence de tâches de sorte que seul le meilleur pilote correspondant pour chaque périphérique matériel détecté soit installé ou bien spécifier que l'étape de la séquence de tâches installe tous les pilotes compatibles pour chaque périphérique matériel détecté et laisser ensuite le programme d'installation Windows choisir le pilote le mieux adapté. En outre, vous pouvez spécifier une catégorie de pilotes de périphérique pour limiter les pilotes qui sont disponibles pour cette étape.  

-   [Appliquer le package de pilotes](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage) : cette étape permet de mettre tous les pilotes de périphérique contenus dans un package de pilotes spécifique à la disposition du programme d’installation de Windows. Dans les packages de pilotes spécifiés, le programme d'installation de Windows recherche les pilotes de périphérique qui sont nécessaires. Quand vous créez un média autonome, vous devez utiliser cette étape pour installer les pilotes de périphérique.  

 Lorsque vous utilisez ces étapes de séquence de tâches, vous pouvez également spécifier la manière dont les pilotes de périphérique sont installés sur l'ordinateur où vous déployez le système d'exploitation. Pour plus d’informations, consultez [Gérer les séquences de tâches pour automatiser des tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Utiliser des séquences de tâches pour installer des pilotes de périphérique sur des ordinateurs  
 Utilisez la procédure suivante pour installer des pilotes de périphérique dans le cadre du déploiement de systèmes d'exploitation.  

#### <a name="use-a-task-sequence-to-install-device-drivers"></a>Utiliser une séquence de tâches pour installer des pilotes de périphérique  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans le nœud **Séquences de tâches** , sélectionnez la séquence de tâches que vous souhaitez modifier pour installer le pilote de périphérique, puis cliquez sur **Modifier**.  

4.  Rendez-vous à l'emplacement où vous souhaitez ajouter les étapes **Pilote** , cliquez sur **Ajouter**, puis sélectionnez **Pilotes**.  

5.  Ajoutez l'étape **Appliquer automatiquement les pilotes** si vous souhaitez que la séquence de tâches installe tous les pilotes de périphérique ou les catégories spécifiques qui sont spécifiées. Spécifiez les options pour l'étape sous l'onglet **Propriétés** et les conditions pour l'étape sous l'onglet **Options** .  

     Ajoutez l'étape **Appliquer le package de pilotes** si vous souhaitez que la séquence de tâches installe uniquement ces pilotes de périphérique à partir du package spécifié. Spécifiez les options pour l'étape sous l'onglet **Propriétés** et les conditions pour l'étape sous l'onglet **Options** .  

    > [!IMPORTANT]  
    >  Vous pouvez sélectionner **Désactiver cette étape** sous l’onglet **Options** pour désactiver l’étape de dépannage de la séquence de tâches.  

6.  Cliquez sur **OK** pour enregistrer la séquence de tâches.  

 Pour plus d’informations sur la création d’une séquence de tâches pour installer un système d’exploitation, consultez [Créer une séquence de tâches pour installer un système d’exploitation](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).  

##  <a name="BKMK_DriverReports"></a> Rapports de gestion de pilotes  
 Vous pouvez utiliser plusieurs rapports dans la catégorie des rapports **Gestion des pilotes** pour déterminer des informations générales sur les pilotes de périphérique dans le catalogue de pilotes. Pour plus d’informations sur les rapports, consultez [Rapports](../../core/servers/manage/reporting.md).
