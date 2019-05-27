---
title: À propos de la mise à niveau, de la mise à jour et de l’installation
titleSuffix: Configuration Manager
description: Découvrez la différence entre les termes Installation, Mise à jour et Mise à niveau, lors de la gestion de l’infrastructure Configuration Manager.
ms.date: 04/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 53803d154a871739c5dd8cf7eaff4eebf92fd651
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083416"
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>À propos de la mise à niveau, de la mise à jour et de l’installation pour l’infrastructure de site et de hiérarchie

*S’applique à : System Center Configuration Manager (Current Branch)*


Lors de la gestion de l’infrastructure de site et de hiérarchie de System Center Configuration Manager, les termes *mise à niveau*, *mise à jour* et *installation* sont utilisés pour décrire trois concepts distincts.

## <a name="upgrade"></a>Mettre à niveau
La *mise à niveau* ou *mise à niveau en place* est utilisée lors de la conversion de votre site ou hiérarchie Configuration Manager 2012 vers un site ou une hiérarchie qui exécute System Center Configuration Manager.
Lorsque vous mettez à niveau System Center 2012 Configuration Manager vers System Center Configuration Manager, vous continuez à utiliser les mêmes serveurs pour héberger vos sites et serveurs de site, et vous conservez vos données et configurations existantes pour Configuration Manager.  Cela est différent de la [migration](/sccm/core/migration/migrate-data-between-hierarchies) qui est une façon de conserver vos configurations et données concernant les périphériques gérés tout en utilisant de nouveaux sites System Center Configuration Manager installés sur du nouveau matériel.

Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).



## <a name="update"></a>Mise à jour
La *mise à jour* est utilisée pour l’installation de mises à jour dans la console pour System Center Configuration Manager et pour les mises à jour hors bande qui sont des mises à jour qui ne peuvent pas être fournies à partir de la console Configuration Manager. Les mises à jour dans la console peuvent modifier la version de votre site Current Branch (ou site Technical Preview) afin qu’il exécute une version ultérieure. Par exemple, si votre site exécute la version 1806, vous pouvez installer une mise à jour pour la version 1810. Les mises à jour peuvent également installer des correctifs pour un problème connu, sans modifier la version des sites.      

En règle générale, les mises à jour ajoutent des correctifs de sécurité, apportent une amélioration de la qualité et de nouvelles fonctionnalités à votre déploiement existant. Si vous utilisez la branche Technical Preview, une mise à jour peut installer une version plus récente de Technical Preview.
-   Vous choisissez quand installer la mise à jour dans la console, en commençant par le site de niveau supérieur dans votre hiérarchie.
- Vous pouvez installer toute mise à jour disponible à partir de la console. Par exemple, si votre site exécute la version 1802, et que les versions 1806 et 1810 sont proposées, envisagez d’installer la version 1810, car chaque version inclut les fonctionnalités qui ont été mises à disposition dans les versions précédentes.
- Une fois l’installation d’une nouvelle mise à jour terminée sur votre site de niveau supérieur, les sites principaux enfants démarrent automatiquement le processus de mise à jour. Toutefois, vous pouvez définir des [fenêtres de maintenance](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers) pour contrôler la planification des mises à jour.
- Les sites secondaires n’installent pas automatiquement les mises à jour. Vous devez démarrer manuellement la mise à jour à partir de la console Configuration Manager.

Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](/sccm/core/servers/manage/updates) et [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).



## <a name="install"></a>Installez
*L’installation* est utilisée lors de la création d’une nouvelle hiérarchie Configuration Manager ou l’ajout de sites supplémentaires à une hiérarchie existante.  

Lorsque vous installez un nouveau site principal ou un site d’administration centrale, l’emplacement de setup.exe et de ses fichiers source associés que vous utilisez dépend de votre scénario d’installation.

Pour plus d’informations, consultez [Préparer l’installation des sites](/sccm/core/servers/deploy/install/prepare-to-install-sites).
