---
title: Gérer la branche LTSB
titleSuffix: Configuration Manager
description: Différences de gestion de LTSB dans System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3c1b813104f2c43ee4c0d7d519e02bb880433b3b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338820"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gérer Long-Term Servicing Branch dans Configuration Manager

*S’applique à : System Center Configuration Manager (Long-Term Servicing Branch)*

Lorsque vous utilisez Long-Term Servicing Branch (LTSB) dans System Center Configuration Manager, les éléments suivants peuvent vous aider à comprendre les importantes modifications qui affectent la façon dont vous gérez votre infrastructure.

Étant donné que LTSB équivaut à la version 1606 de Current Branch (avec quelques exceptions comme l’intégration d’Intune et certaines fonctionnalités cloud), la plupart des tâches que vous utilisez pour la planification, le déploiement, la configuration et la gestion quotidienne sont identiques.

Par exemple, LTSB prend en charge les mêmes nombre de sites, types de site, clients et infrastructure générale que Current Branch. Ainsi, vous utilisez les instructions figurant dans les rubriques sur la planification et la conception de sites et de hiérarchies pour Current Branch. De même, pour les fonctionnalités LTSB prises en charge par les deux branches, comme les mises à jour logicielles ou le déploiement de système d’exploitation, utilisez les instructions figurant dans les sections de la documentation Current Branch en tenant compte des mises en garde liées au non-accès aux modifications de fonctionnalités introduites après la version 1606 de Current Branch.

Les sections suivantes fournissent des informations sur la gestion de tâches qui ne sont pas similaires.

## <a name="updates-and-servicing"></a>Mises à jour et maintenance
Seules les mises à jour de sécurité critiques sont disponibles en tant que mises à jour dans la console dans LTSB.  

Les informations sur les mises à jour régulières des versions Current Branch ultérieures sont visibles dans la console, mais elles ne sont pas disponibles dans LTSB. Elles ne sont pas téléchargées et ne peuvent pas être installées.

Pour prendre en charge les mises à jour dans la console pour les correctifs de sécurité critiques, un site LTSB a besoin d’utiliser [le point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point). Vous pouvez configurer ce rôle de système de site en mode hors connexion ou en ligne, comme pour Current Branch. LTSB collecte et envoie les mêmes données de télémétrie et d’utilisation que Current Branch.

LTSB prend en charge l’utilisation du programme d’installation de correctif logiciel et de l’outil Inscription de la mise à jour, comme indiqué pour Current Branch.

Pour obtenir des informations générales sur les mises à jour et la maintenance, consultez [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Modifications liées au développement de site et au dossier CD.Latest
Quand vous exécutez LTSB et que vous développez un site principal autonome en installant un nouveau site d’administration centrale, vous devez utiliser le programme d’installation et les fichiers sources du support de la base de référence de la version 1606. Pour Current Branch, vous exécutez le programme d’installation et vous utilisez les fichiers sources du dossier CD.Latest.

Bien que vous n’exécutiez pas le programme d’installation pour le développement de site à partir du dossier CD.Latest, vous continuez d’utiliser ce dossier pour la récupération de site et pour installer un nouveau site principal enfant si votre premier site LTSB était un site d’administration centrale.

Pour plus d’informations sur le développement d’un site, consultez [Développement d'un site principal autonome](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Pour plus d’informations sur le dossier CD.Latest, consultez [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).


## <a name="recovery"></a>Récupération
Lorsque vous récupérez un site, vous devez restaurer le site ou la base de données de site dans sa branche d’origine. Vous ne pouvez pas récupérer une base de données de site Current Branch sur une installation LTSB, et vice versa.
