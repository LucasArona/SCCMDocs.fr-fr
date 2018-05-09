---
title: Bibliothèque de contenu
titleSuffix: Configuration Manager
description: Découvrez la bibliothèque de contenu qu’utilise System Center Configuration Manager pour réduire la taille globale du contenu distribué.
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df34c2c8ecb0f906657d1bbc2e49c87a5ff93e15
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="the-content-library-in-system-center-configuration-manager"></a>Bibliothèque de contenu System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La bibliothèque de contenu est l’emplacement de stockage SIS (Single-Instance Store) utilisé par Configuration Manager pour réduire la taille globale de l’ensemble du contenu que vous distribuez. Elle stocke tous les fichiers de contenu des mises à jour logicielles, des applications, des déploiements de système d’exploitation, etc.

 - Une copie de la bibliothèque de contenu est automatiquement créée et gérée sur chaque **serveur de site** et chaque **point de distribution**.

 - Avant de télécharger les fichiers de contenu vers le serveur de site ou de copier les fichiers sur les points de distribution, Configuration Manager vérifie si chaque fichier de contenu se trouve déjà dans la bibliothèque de contenu.
 - Si le fichier de contenu est disponible, Configuration Manager ne le copie pas et associe le fichier de contenu existant à l’application ou au package.

Sur les ordinateurs sur lesquels vous installez un point de distribution, vous pouvez configurer les éléments suivants :

- un ou plusieurs lecteurs de disque sur lesquels vous voulez créer la bibliothèque de contenu ;
- une priorité pour chaque lecteur que vous utilisez.

Lorsque Configuration Manager copie des fichiers de contenu, il les copie sur le lecteur ayant la plus haute priorité, sauf si ce lecteur dispose d’une quantité d’espace libre inférieure à la quantité minimale spécifiée.
- Vous configurez les paramètres de lecteur lors de l'installation du point de distribution.
- Vous ne pouvez pas configurer les paramètres de lecteur dans les propriétés du point de distribution, une fois l’installation terminée.


Pour plus d’informations sur la configuration des paramètres de lecteur pour le point de distribution, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


>  [!IMPORTANT]  
>  Pour déplacer la bibliothèque de contenu vers un autre emplacement sur un point de distribution après l’installation, utilisez l’**outil Content Library Transfer** dans la boîte à outils de System Center 2012 R2 Configuration Manager. Vous pouvez télécharger les outils depuis le [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  

## <a name="about-the-content-library-on-the-central-administration-site"></a>À propos de la bibliothèque de contenu sur le site d’administration centrale  
 Par défaut, Configuration Manager crée une bibliothèque de contenu sur le site d’administration centrale, lors de l’installation du site. La bibliothèque de contenu est placée sur le lecteur du serveur de site possédant l'espace disponible le plus important. Comme vous ne pouvez pas installer un point de distribution sur le site d’administration centrale, vous ne pouvez pas attribuer une priorité aux lecteurs à utiliser pour la bibliothèque de contenu. Comme la bibliothèque de contenu sur d'autres serveurs de site ou sur des points de distribution, lorsque le lecteur contenant la bibliothèque de contenu n'a plus d'espace disponible, la bibliothèque de contenu s'étend sur le lecteur disponible suivant.  

 Configuration Manager utilise la bibliothèque de contenu sur le site d’administration centrale dans les scénarios suivants :  

-   Lorsque vous créez un contenu sur le site d’administration centrale.  

-   Lorsque vous migrez le contenu depuis un autre site Configuration Manager et désignez le site d’administration centrale comme site de gestion du contenu.  

> [!NOTE]  
>  Lorsque vous créez un contenu sur un site principal, puis le distribuez à un autre site principal ou à un site secondaire sous un autre site principal, le site d'administration centrale stocke temporairement ce contenu dans la boîte de réception du planificateur sur le site d'administration centrale, sans toutefois ajouter ce contenu à sa bibliothèque de contenu.  

 Utilisez les options suivantes pour gérer la bibliothèque de contenu sur le site d'administration centrale :  

-   Pour empêcher l’installation de la bibliothèque de contenu sur un lecteur spécifique, créez un fichier vide nommé **no_sms_on_drive.sms** et copiez-le dans le dossier racine du lecteur avant la création de la bibliothèque de contenu.  

-   Une fois la bibliothèque de contenu créée, utilisez l’**outil Content Library Transfer** de la boîte à outils System Center 2012 R2 Configuration Manager pour gérer l’emplacement de la bibliothèque de contenu. Vous pouvez télécharger les outils depuis le [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkId=279566).  
