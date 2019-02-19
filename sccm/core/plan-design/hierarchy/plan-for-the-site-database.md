---
title: Planifier la base de données du site
titleSuffix: Configuration Manager
description: Tenez compte de la base de données du site et son rôle serveur quand vous planifiez votre hiérarchie System Center Configuration Manager.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0c9134fa0bbabf5425ce17d21b143d71437aea36
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136379"
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Planifier la base de données du site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le serveur de base de données de site est un ordinateur qui exécute une version prise en charge de Microsoft SQL Server. SQL Server est utilisé pour stocker des informations pour les sites Configuration Manager. Chaque site d’une hiérarchie Configuration Manager contient une base de données du site et un serveur qui est attribué au rôle serveur de la base de données du site.  

-   Pour les sites d'administration centrale et les sites principaux, vous pouvez installer SQL Server sur le serveur de site, ou vous pouvez installer SQL Server sur un ordinateur autre que le serveur de site.  

-   Pour les sites secondaires, vous pouvez utiliser SQL Server Express au lieu d’une installation complète de SQL Server. Le serveur de base de données doit cependant être exécuté sur le serveur de site secondaire.  

-  Pour l’utilisation du groupe de disponibilité SQL, le modèle de récupération de la base de données doit être défini sur FULL  

-  Pour l’utilisation du groupe de disponibilité non SQL, le modèle de récupération de la base de données doit être défini sur SIMPLE  

Vous trouverez plus d’informations sur les modes de récupération SQL dans [Modèles de récupération (SQL Server)](https://docs.microsoft.com/sql/relational-databases/backup-restore/recovery-models-sql-server).

Les configurations SQL Server suivantes peuvent servir à héberger la base de données du site :  

-   Instance par défaut de SQL Server  

-   Une instance nommée sur un seul ordinateur exécutant SQL Server  

-   Une instance nommée sur une instance en cluster de SQL Server  

-   Un groupe de disponibilité AlwaysOn SQL Server (à compter de la version 1602 de System Center Configuration Manager)


Pour héberger la base de données du site, SQL Server doit remplir les conditions requises décrites dans [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Considérations relatives à l’emplacement du serveur de base de données distant  

Si vous utilisez un ordinateur serveur de base de données distant, vérifiez que la connexion réseau est à large bande passante et haute disponibilité. Le serveur de site et certains rôles de système de site doivent communiquer en permanence avec le serveur distant qui héberge la base de données de site.

-   La quantité de bande passante requise pour les communications avec le serveur de base de données dépend de l’association de nombreuses configurations de site et de client. Par conséquent, la bande passante réelle requise ne peut pas être déterminée correctement.  

-   Chaque ordinateur qui exécute le fournisseur SMS et qui se connecte à la base de données du site augmente les besoins en bande passante réseau.  

-   L’ordinateur qui exécute SQL Server doit se trouver dans un domaine qui entretient une relation d’approbation bidirectionnelle avec le serveur de site et tous les ordinateurs exécutant le fournisseur SMS.  

-   Vous ne pouvez pas utiliser un SQL Server en cluster pour le serveur de base de données de site lorsque la base de données de site se trouve au même emplacement que le serveur de site.  


En règle générale, un serveur de système de site prend en charge les rôles de système de site d’un seul site Configuration Manager. Vous pouvez toutefois utiliser différentes instances de SQL Server, sur des serveurs cluster ou non cluster exécutant SQL Server, pour héberger une base de données de différents sites Configuration Manager. Pour prendre en charge des bases de données à partir de différents sites, vous devez configurer chaque instance de SQL Server afin qu'elle utilise des ports uniques pour la communication.  
