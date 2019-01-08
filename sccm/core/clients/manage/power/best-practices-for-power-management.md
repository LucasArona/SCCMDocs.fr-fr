---
title: Meilleures pratiques de gestion de l’alimentation
titleSuffix: Configuration Manager
description: Obtenez les bonnes pratiques de gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a08162f36c247136dd346140480e2d29be0c4017
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424797"
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>Meilleures pratiques de gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les bonnes pratiques de gestion de l’alimentation suivantes dans System Center Configuration Manager.  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>Effectuer la phase de surveillance à un moment représentatif  
 La phase de surveillance de la gestion de l'alimentation fournit des informations sur la consommation d'énergie, l'activité, les fonctionnalités de gestion de l'alimentation et l'impact sur l'environnement des ordinateurs de votre organisation. Veillez à choisir une période représentative pour effectuer la phase de surveillance. Par exemple, l'exécution de la phase de surveillance un jour férié ne fournit pas un rapport réaliste sur l'utilisation énergétique des ordinateurs.  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>Créer un regroupement de contrôle d’ordinateurs sans appliquer de modes de gestion de l’alimentation.  
 Créez deux regroupements d’ordinateurs pour vous aider à surveiller les effets de l’application de modes de gestion de l’alimentation aux ordinateurs. Le premier regroupement doit contenir la majorité des ordinateurs auxquels vous souhaitez appliquer les paramètres d’alimentation et l’autre regroupement (le regroupement de contrôle) doit contenir les autres ordinateurs. Appliquez le mode de gestion de l’alimentation requis au regroupement contenant la majorité des ordinateurs. Vous pouvez ensuite exécuter des rapports pour comparer le coût de l’alimentation, la gestion de l’alimentation et l’impact sur l’environnement des ordinateurs auxquels vous avez appliqué des paramètres d’alimentation et le regroupement de contrôle auquel vous n’avez pas appliqué de paramètres d’alimentation.  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>Exécuter le rapport des paramètres d’alimentation avant d’appliquer un mode de gestion de l’alimentation  
 Avant d'appliquer un mode de gestion de l'alimentation à un regroupement d'ordinateurs, exécutez le rapport **Paramètres d'alimentation** pour mieux comprendre les paramètres de gestion de l'alimentation qui sont déjà configurés sur les ordinateurs du regroupement. Si vous appliquez les nouveaux paramètres de gestion de l'alimentation aux ordinateurs sans examiner préalablement les paramètres existants, cela peut entraîner une augmentation de la consommation d'énergie.  

## <a name="exclude-servers-from-power-management"></a>Exclure les serveurs de la gestion de l’alimentation  
 La gestion de l’alimentation n’est pas prise en charge pour les ordinateurs qui exécutent Windows Server (bien que les données de gestion de l’alimentation soient collectées). Veillez à ajouter les serveurs à un regroupement et à exclure ce dernier de la gestion de l’alimentation.  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>Exclure les ordinateurs que vous ne souhaitez pas gérer  
 Si vous disposez d'ordinateurs que vous ne souhaitez pas gérer avec la gestion de l'alimentation, ajoutez-les à un regroupement et assurez-vous que le regroupement est exclu de la gestion de l'alimentation.  

 Voici quelques exemples d'ordinateurs à exclure de la gestion de l'alimentation :  

- Les ordinateurs qui doivent rester allumés.  

- Les ordinateurs auxquels des utilisateurs ont besoin de se connecter à l'aide de la connexion Bureau à distance.  

- Les ordinateurs qui ne peuvent pas utiliser la gestion de l'alimentation.  

- Ordinateurs dotés du rôle de système de site de point de distribution.  

- Ordinateurs publics tels que les bornes d'informations, les écrans d'affichage ou les consoles de surveillance pour lesquels l'ordinateur et le moniteur doivent toujours être allumés.  

  Pour plus d’informations, consultez [Configuration de la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/configuring-power-management.md).  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>Appliquer d’abord les modes de gestion de l’alimentation à un regroupement test d’ordinateurs  
 Testez toujours les conséquences liées à l'application d'un mode de gestion de l'alimentation à un regroupement test d'ordinateurs avant d'appliquer le mode d'alimentation à un plus grand regroupement d'ordinateurs.  

 Les paramètres d'alimentation appliqués aux ordinateurs exécutant Windows XP ou Windows Server 2003 ne sont pas rétablis selon leurs valeurs d'origine, même si vous excluez l'ordinateur de la gestion de l'alimentation. Sur les versions ultérieures de Windows, l'exclusion d'un ordinateur de la gestion de l'alimentation entraîne le rétablissement des valeurs d'origine de tous les paramètres d'alimentation. Il est impossible de rétablir les valeurs d'origine de chaque paramètre d'alimentation.  

## <a name="apply-power-plan-settings-individually"></a>Appliquer individuellement les paramètres de mode de gestion de l’alimentation  
 Surveiller les conséquences liées à l'application de chaque paramètre d'alimentation avant d'appliquer le paramètre suivant pour s'assurer que chaque paramètre a l'effet requis. Pour plus d’informations sur les paramètres du mode de gestion de l’alimentation, consultez [Paramètres de mode de gestion de l’alimentation disponibles](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) dans la rubrique [Guide pratique pour créer et appliquer des modes de gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>Surveiller régulièrement les ordinateurs pour voir si plusieurs modes de gestion de l’alimentation leur sont appliqués  
 La gestion de l'alimentation inclut un rapport qui affiche les ordinateurs auxquels plusieurs modes d'alimentation sont appliqués.  

 Si un ordinateur est membre de plusieurs regroupements, chacun appliquant des modes de gestion de l'alimentation différents, les actions suivantes sont effectuées :  

-   Gestion de l'alimentation : Si plusieurs valeurs sont appliquées à un ordinateur comme paramètres d'alimentation, c'est la valeur la moins restrictive qui est utilisée.  

-   Heure d'éveil : si plusieurs heures d'éveil sont appliquées à un ordinateur de bureau, l'heure la plus proche de minuit sera utilisée.  

     Pour plus d’informations, consultez [Ordinateurs avec plusieurs modes de gestion de l’alimentation](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple) dans la rubrique [Guide pratique pour surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md). Pour plus d’informations sur la manière dont la gestion de l’alimentation résout les conflits, consultez [Guide pratique pour créer et appliquer des modes de gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>Enregistrer ou exporter les informations de gestion de l’alimentation pendant la phase de surveillance et de planification de la gestion de l’alimentation  
 Les informations de gestion de l’alimentation utilisées par les rapports quotidiens sont conservées dans la base de données du site Configuration Manager pendant 31 jours.  

 Les informations de gestion de l’alimentation utilisées par les rapports mensuels sont conservées dans la base de données du site Configuration Manager pendant 13 mois.  

 Quand vous exécutez des rapports pendant les phases de surveillance, de planification et de conformité de la gestion de l’alimentation, enregistrez ou exportez les résultats de tous les rapports pour lesquels vous souhaitez conserver les données afin de les comparer ultérieurement au cas où ils seraient ensuite supprimés par Configuration Manager.  
