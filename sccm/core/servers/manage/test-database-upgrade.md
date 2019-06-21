---
title: Tester la mise à jour d’une base de données
titleSuffix: Configuration Manager
description: Testez la mise à niveau d’une base de données de site lorsque vous installez des mises à jour pour Configuration Manager.
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: abb696f3-a816-4f12-a9f1-0503a81e1976
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c25e2d2aac1c1763df4282e92114257ee34065ac
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194118"
---
# <a name="test-the-database-upgrade-when-installing-an-update"></a>Tester la mise à niveau d’une base de données avant d’installer une mise à jour

*S’applique à : System Center Configuration Manager (Current Branch)*

Les informations de cette rubrique peuvent vous aider à tester la mise à niveau d’une base de données avant d’installer une mise à jour dans la console pour la branche active de Configuration Manager. Toutefois, le test de la mise à niveau ne constitue plus une étape requise ou recommandée si votre base de données est suspecte ou a été modifiée par des personnalisations qui ne sont pas explicitement prises en charge par Configuration Manager.

## <a name="do-i-need-to-run-a-test-upgrade"></a>Ai-je besoin de tester une mise à niveau ?
Le test d’une mise à niveau n’est plus requis depuis les modifications apportées à System Center Configuration Manager. Ces modifications simplifient le processus et la vitesse à laquelle un environnement de production peut être mis à jour avec des versions plus récentes. Cette refonte a été effectuée pour permettre aux clients de rester à jour avec moins de risques et moins de surcharge opérationnelle lors de l’installation de chaque nouvelle mise à jour.

Les modifications concernent la façon dont les mises à jour s’installent, notamment la logique qui annule automatiquement une mise à jour ayant échoué sans avoir à exécuter une récupération de site. Ces modifications permettent d’utiliser la console pour gérer les installations de mises à jour et incluent une option pour [relancer l’installation d’une mise à jour ayant échoué](/sccm/core/servers/manage/install-in-console-updates#bkmk_retry).

> [!TIP]
> Lorsque vous effectuez une mise à niveau avec System Center Configuration Manager à partir d’un produit plus ancien, par exemple System Center 2012 Configuration Manager, [le test des mises à niveau de la base de données reste une étape recommandée](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#bkmk_test).

Si vous souhaitez néanmoins tester la mise à niveau d’une base de données de site lorsque vous installez une mise à jour dans la console, les informations suivantes vous fournissent [des conseils sur l’installation d’une mise à jour dans la console](/sccm/core/servers/manage/install-in-console-updates#bkmk_install).

## <a name="prepare-to-run-a-test-database-upgrade"></a>Préparer le test d’une mise à niveau de base de données  
Avant d’installer une nouvelle mise à jour dans votre hiérarchie, telle que la mise à jour 1702, vous pouvez tester la mise à niveau de votre base de données de site.

Pour test une mise à niveau, utilisez le programme d’installation de Configuration Manager à partir des fichiers source figurant dans le dossier [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) d’un site qui exécute la version de Configuration Manager vers laquelle vous effectuez la mise à jour. Cela signifie que pour tester la mise à jour de la base de données pour une mise à jour vers 1702 :
-   Vous devez disposer d’au moins un site qui exécute la version 1702 à partir duquel vous pouvez accéder à ce dossier CD.Latest.
-   Si vous n’avez pas de site qui exécute la version requise, vous pouvez installer un site dans un environnement de laboratoire, puis mettre à jour ce site avec la nouvelle version. Cette opération crée le dossier CD.Latest avec la version correcte des fichiers sources.

Le test de la mise à niveau est exécuté sur une sauvegarde de votre base de données de site que vous avez restaurée sur une instance distincte de SQL Server.  Vous exécutez le programme d’installation à partir du dossier **CD.Latest** à l’aide du commutateur de ligne de commande **testdbupgrade** pour tester la mise à niveau qui a restauré la copie de la base de données. Une fois le test de la mise à niveau terminé, la base de données mise à niveau est supprimée. Elle ne peut pas être utilisée par un site Configuration Manager.

Si l’installation d’une mise à jour échoue, vous n’avez pas besoin de récupérer le site. Au lieu de cela, vous pouvez essayer de réinstaller de la mise à jour depuis la console.

##  <a name="run-the-test-upgrade"></a>Tester une mise à niveau    
1. Utilisez le programme d’installation de Configuration Manager et les fichiers sources figurant dans le dossier **CD.Latest** d’un site qui exécute la version vers laquelle vous prévoyez d’effectuer la mise à jour.  

2. Copiez le dossier **CD.Latest** vers un emplacement sur l’instance SQL Server que vous utiliserez pour tester la mise à niveau de la base de données.

3. Créez une sauvegarde de la base de données du site pour laquelle vous souhaitez tester une mise à niveau. Restaurez ensuite une copie de cette base de données sur une instance de SQL Server qui n’héberge pas de site Configuration Manager. L’instance SQL Server doit utiliser la même édition de SQL Server que votre base de données de site.  

4. Après avoir restauré la copie de la base de données, exécutez le fichier **Setup** dans le dossier CD.Latest contenant les fichiers sources de la version vers laquelle vous effectuez la mise à jour. Quand vous exécutez le programme d’installation, utilisez l’option de ligne de commande **/TESTDBUPGRADE** . Si l'instance SQL Server qui héberge la copie de la base de données n'est pas l'instance par défaut, fournissez les arguments de ligne de commande pour identifier l'instance qui héberge la copie de la base de données du site.   

   Par exemple, vous utilisez une base de données de site dont le nom de base de données est *SMS_ABC*. Vous restaurez une copie de cette base de données de site sur une instance prise en charge de SQL Server ayant pour nom d'instance *DBTest*. Pour tester une mise à niveau de cette copie de la base de données du site, utilisez la ligne de commande suivante : **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**.  

   Vous trouverez le fichier Setup.exe à l’emplacement suivant sur le média source de System Center Configuration Manager : **SMSSETUP\BIN\X64**.  

5. Sur l'instance de SQL Server où vous avez exécuté le test de mise à niveau, examinez *ConfigMgrSetup.log* à la racine du lecteur système pour connaître la progression et l'issue du test.  

    Si le test de la mise à niveau échoue, corrigez les problèmes ayant entraîné l’échec de la mise à niveau de la base de données du site. Puis créez une nouvelle sauvegarde de la base de données du site et testez la mise à niveau de la nouvelle copie de la base de données.  



## <a name="next-steps"></a>Étapes suivantes
Une fois le test de la mise à jour de la base de données terminé, supprimez la base de données mise à jour. Elle ne peut pas être utilisée par un site Configuration Manager. Vous pouvez ensuite revenir à votre site actif et [commencer l’installation de la mise à jour](/sccm/core/servers/manage/install-in-console-updates).
