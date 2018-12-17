---
title: Tableau de bord de cogestion
titleSuffix: Configuration Manager
description: Utilisez le tableau de bord de cogestion pour consulter les informations sur les appareils cogérés.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad76140285df1c0125fcd2efab0f4794ed4881bf
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455940"
---
# <a name="co-management-dashboard-in-configuration-manager"></a>Tableau de bord de cogestion dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Depuis la version 1802, consultez un tableau de bord comportant des informations sur la cogestion. Le tableau de bord vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphiques peuvent vous aider à identifier les appareils qui demandent une attention particulière.<!--1356648-->

Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **Cogestion**.

Depuis la version 1810, le tableau de bord de cogestion a été amélioré avec des informations plus détaillées. <!--1358980-->



## <a name="dashboard-tiles"></a>Vignettes du tableau de bord 

Le tableau de bord de cogestion présente des vignettes qui varient en fonction de la version du site. 


### <a name="co-managed-devices"></a>Appareils cogérés

*S’applique aux versions 1802 et 1806*

Indique le pourcentage d’appareils cogérés dans tout votre environnement.
 ![Vignette des appareils cogérés](media\co-management-dashboard\Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribution des systèmes d’exploitation clients

*S’applique à toutes les versions* 

Indique le nombre d’appareils clients par système d’exploitation et par version. Elle utilise les regroupements suivants :  
- Windows 7 et 8.x  
- Windows 10 antérieur à 1709  
- Windows 10 1709 et ultérieur  

    > [!Tip]  
    > Windows 10, version 1709 et ultérieures, est un prérequis pour la cogestion.  

Pointez sur une section du graphique pour connaître le pourcentage d’appareils appartenant à ce groupe de système d’exploitation.
 ![Vignette de distribution des systèmes d’exploitation clients](media\co-management-dashboard\Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>État de la cogestion (anneau)

*S’applique aux versions 1802 et 1806*

Indique la répartition des réussites et des échecs des appareils dans les catégories suivantes :
- Réussite, Joint à une version hybride d’Azure AD  
- Réussite, Joint à Azure AD  
- Échec : Échec de l’inscription automatique  

Pointez sur une section du graphe pour connaître le pourcentage d’appareils appartenant à cette catégorie. 
 ![Vignette de l’état de la cogestion (anneau)](media\co-management-dashboard\Co-management-status-graph.PNG)

Sélectionnez une section du graphe pour voir la liste des appareils appartenant à cette catégorie.
 ![Liste des appareils en échec d’inscription](media\co-management-dashboard\Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>État de la cogestion (entonnoir)

*S’applique à la version 1810 et ultérieures*

Graphique en entonnoir qui indique le nombre d’appareils associés aux états suivants du processus d’inscription :  
- Appareils éligibles  
- Planifié  
- Inscription lancée  
- Inscrit  

![Vignette d’état de la cogestion (entonnoir)](media\co-management-dashboard\1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>État d'inscription à la cogestion

*S’applique à la version 1810 et ultérieures*

Montre la répartition de l’état des appareils dans les catégories suivantes :
- Réussite, joint à une version hybride d’Azure AD  
- Réussite, joint à Azure AD  
- Inscription en cours, joint à une version hybride d’Azure AD  
- Échec, joint à une version hybride d’Azure AD  
- Échec, joint à Azure AD  
- En attente de la connexion de l’utilisateur  

Sélectionnez un état dans la vignette pour accéder à la liste des appareils qui se trouvent dans cet état.  

![Vignette d’état d’inscription à la cogestion](media\co-management-dashboard\1358980-enrollment-status.png)


### <a name="enrollment-errors"></a>Erreurs d’inscription

*S’applique à la version 1810 et ultérieures*

Tableau qui indique le nombre d’erreurs d’inscription des appareils.  


### <a name="workload-transition"></a>Transition des charges de travail

*S’applique à toutes les versions*

Affiche un graphique à barres indiquant le nombre d’appareils dont vous avez opéré la transition vers Microsoft Intune pour les charges de travail disponibles. (La liste des charges de travail varie en fonction de la version de Configuration Manager. Pour plus d’informations, consultez [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune).)

Pointez sur une section du graphique pour connaître le nombre d’appareils ayant fait l’objet d’une transition pour la charge de travail. 
 ![Graphique à barres de transition des charges de travail](media\co-management-dashboard\Workload-Transition.PNG)


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la cogestion, consultez :
 - [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview)
 - [Préparer les appareils Windows 10 pour la cogestion](/sccm/core/clients/manage/co-management-prepare)

    
