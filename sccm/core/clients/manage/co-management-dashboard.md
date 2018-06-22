---
title: Tableau de bord de cogestion
titleSuffix: Configuraton Manager
description: Passez en revue les informations relatives à la cogestion à l’aide du tableau de bord.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cdf073aa3e9ca3be6062ea0e5e0528bb97937989
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333400"
---
# <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Tableau de bord de cogestion dans System Center Configuration Manager
*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1802, vous pouvez consulter un tableau de bord contenant des informations sur la cogestion. Le tableau de bord vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphiques peuvent vous aider à identifier les appareils qui demandent une attention particulière.<!--1356648-->

## <a name="open-the-co-management-dashboard"></a>Ouvrir le tableau de bord de cogestion
Pour ouvrir le tableau de bord de cogestion, effectuez les étapes suivantes : 

1. Ouvrez la console Configuration Manager. 
2. Cliquez sur le nœud **Analyse**. 
3. Pour charger le tableau de bord, cliquez sur **Cogestion**.

## <a name="reviewing-information-in-the-co-management-dashboard"></a>Consultation des informations contenues dans le tableau de bord de cogestion

Le tableau de bord de cogestion présente quatre graphiques pour votre environnement. 

- **Appareils cogérés** : indique le pourcentage d’appareils cogérés dans tout votre environnement.

    ![Graphique des appareils cogérés](media\co-management-dashboard\Percent-Co-managed-graph.PNG)

- **Distribution de système d’exploitation client** : affiche le nombre d’appareils clients par système d’exploitation et par version. Les regroupements suivants sont utilisés : </br>
    - Windows 7 et 8.x
    - Windows 10 antérieur à 1709
    - Windows 10 1709 et ultérieur

         > [!NOTE] 
         > Windows 10, version 1709 et ultérieures, est un prérequis pour la cogestion.

     Pointer sur une section du graphique vous donne le pourcentage d’appareils du regroupement de systèmes d’exploitation sélectionné.

     ![Graphique de distribution des systèmes d’exploitation clients](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)

- **État de la cogestion** : répartition des réussites et des échecs des appareils selon les catégories suivantes :
    - Réussite, Joint à une version hybride d’Azure AD
    - Réussite, Joint à Azure AD
    - Échec : Échec de l’inscription automatique
    
     Pointer sur une section du graphique vous donne le pourcentage d’appareils dans la catégorie. 

     ![Graphique d’état pour la cogestion](media\co-management-dashboard\Co-management-status-graph.PNG)

     Cliquer sur une section du graphique vous permet d’accéder à une liste d’appareils pour la catégorie.
 
     ![Liste des appareils en échec d’inscription](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


- **Transition des charges de travail** : affiche un graphique à barres indiquant le nombre d’appareils que vous avez fait passer à Microsoft Intune pour les quatre charges de travail disponibles :
    - Stratégies de conformité
    - Accès aux ressources
    - Windows Update for Business
    - Endpoint Protection

     Pointer sur une section du graphique vous donne le nombre d’appareils transférés pour la charge de travail. 
     ![Graphique à barres de transition des charges de travail](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la cogestion, consultez :
 - [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview.md)
 - [Préparer les appareils Windows 10 pour la cogestion](/sccm/core/clients/manage/co-management-prepare.md)

    
