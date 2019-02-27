---
title: Personnaliser les emplacements de fichiers de base de données
titleSuffix: Configuration Manager
description: Découvrez comment spécifier des emplacements personnalisés pour des fichiers de base de données SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f094e2e6eab0067f51cb7fcd193a4acc914fc5c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134950"
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Emplacements personnalisés pour les fichiers de base de données du site System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager prend en charge les emplacements personnalisés pour les fichiers de base de données SQL Server.  

> [!NOTE]  
>  Cette possibilité de spécifier des emplacements de fichiers autres que les emplacements par défaut n'est pas disponible quand vous utilisez un cluster SQL Server.  

 **Durant l’installation** d’un nouveau site principal ou d’un site d’administration centrale, vous pouvez :  

-   **Spécifier des emplacements de fichier différents de ceux par défaut pour la base de données du site** : Configuration Manager installe puis crée la base de données du site à l’aide de ces emplacements.  

-   **Spécifier l’utilisation d’une base de données SQL Server créée au préalable qui utilise des emplacements de fichiers personnalisés** :  Configuration Manager installe puis utilise cette base de données créée au préalable ainsi que ses emplacements de fichiers préconfigurés.  

**Après l’installation**, vous pouvez modifier l’emplacement des fichiers de base de données du site. Pour ce faire, vous devez arrêter le site et modifier l’emplacement du fichier dans SQL Server :  

-   Sur le serveur de site Configuration Manager, arrêtez le service **SMS_Executive**.  

-   Utilisez la documentation de votre version de SQL Server pour savoir comment déplacer une base de données utilisateur. Par exemple, si vous utilisez SQL Server 2014, consultez [Déplacer des bases de données utilisateur](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) sur TechNet.  

-   Après avoir déplacé le fichier de base de données, redémarrez le service **SMS_Executive** sur le serveur de site Configuration Manager.  
