---
title: Outil Inscription de la mise à jour
titleSuffix: Configuration Manager
description: Découvrez quand et comment utiliser l’outil Inscription de la mise à jour pour importer manuellement une mise à jour dans la console Configuration Manager.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8cc13635-85d6-4b07-a3ec-c42188bc5c74
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70322e01e33cdf857768db812450f27a0f17939e
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418225"
---
# <a name="use-the-update-registration-tool-to-import-hotfixes-to-system-center-configuration-manager"></a>Importer des correctifs pour System Center Configuration Manager avec l’outil Inscription de la mise à jour

*S’applique à : System Center Configuration Manager (Current Branch)*

Certaines mises à jour de Configuration Manager indisponibles sur le service cloud Microsoft ne peuvent être obtenues que hors-bande. C’est le cas, par exemple, d’un correctif logiciel en édition limitée destiné à résoudre un problème spécifique.   
Quand vous devez installer une version hors-bande et que le nom de fichier du correctif ou de la mise à jour se termine par l’extension **update.exe**, vous pouvez vous servir de l’**outil Inscription de la mise à jour** pour importer manuellement la mise à jour dans la console Configuration Manager. Cet outil vous permet d’extraire et de transférer le package de mise à jour vers le serveur de site, et d’inscrire la mise à jour auprès de la console Configuration Manager.  

 Si le fichier de correctif a l’extension de fichier **.exe** et non **update.exe**, consultez [Utiliser le programme d’installation de correctif logiciel pour installer les mises à jour de System Center Configuration Manager](../../../core/servers/manage/use-the-hotfix-installer-to-install-updates.md)  

> [!NOTE]  
>  Cette rubrique fournit des indications générales sur la façon d’installer les correctifs pour la mise à jour de System Center Configuration Manager. Pour plus d’informations sur un correctif ou une mise à jour spécifiques, voir l’article correspondant dans la Base de connaissances du support Microsoft.  

 **Conditions préalables à l’utilisation de l’outil Inscription de la mise à jour :**  

-   Cet outil permet d’installer uniquement des mises à jour hors-bande dont le nom se termine par l’extension **.update.exe**  

-   L’outil est autonome et comprend les mises à jour individuelles que vous recevez directement de Microsoft.  

-   L’outil n’a aucune dépendance par rapport au mode du point de connexion de service.  

-   L’outil doit être exécuté sur l’ordinateur hébergeant le point de connexion de service.  

-   .NET Framework 4.52 doit être installé sur l’ordinateur sur lequel l’outil s’exécute (ordinateur faisant office de point de connexion de service).  

-   Le compte que vous utilisez pour exécuter l’outil doit disposer d’autorisations d’**administrateur local** sur l’ordinateur hébergeant le point de connexion de service sur lequel l’outil s’exécute  

-   Le compte que vous utilisez pour exécuter l’outil doit disposer d’autorisations en **écriture** sur le dossier suivant de l’ordinateur hébergeant le point de connexion de service :  **&lt;Répertoire d’installation de ConfigMgr\>\EasySetupPayload\offline**  

### <a name="to-use-the-update-registration-tool"></a>Pour utiliser l’outil Inscription de la mise à jour  

1. Sur l’ordinateur qui héberge le point de connexion de service :  

   -   Ouvrez une invite de commandes avec des privilèges d’administration, puis remplacez les répertoires par l’emplacement contenant **&lt;Produit\>-&lt;version du produit\>-&lt;ID d’article de la Base de connaissances\>-ConfigMgr.Update.exe**  

2. Exécutez la commande suivante pour démarrer l’outil Inscription de la mise à jour :  

   -   **&lt;Produit\>-&lt;version du produit\>-&lt;ID d’article de la Base de connaissances\>-ConfigMgr.Update.exe**  

   Une fois inscrit, le correctif logiciel s’affiche en tant que nouvelle mise à jour dans la console dans les 24 heures.  Vous pouvez accélérer le processus :

   - Ouvrez la console Configuration Manager, accédez à **Administration** > **Mises à jour et maintenance** puis cliquez sur **Rechercher les mises à jour**. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.) 

   L’outil Inscription de la mise à jour consigne ses actions dans un fichier .log sur l’ordinateur local. Ce fichier journal porte le même nom que le fichier .exe du correctif, et est stocké dans le dossier **%SystemRoot%/Temp**.  

    Une fois la mise à jour inscrite, vous pouvez fermer l’outil Inscription de la mise à jour.  

3. Ouvrez la console Configuration Manager, puis accédez à **Administration** > **Mises à jour et maintenance**. Les correctifs importés peuvent désormais être installés. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)

   Pour plus d’informations sur l’installation des mises à jour, consultez [Installer des mises à jour dans la console pour System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md)  
