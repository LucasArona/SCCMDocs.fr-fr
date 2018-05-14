---
title: Prise en charge de Windows 10
titleSuffix: Configuration Manager
description: Découvrir les versions de Windows 10 prises en charge comme clients ou pour OSD avec System Center Configuration Manager
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 947392d4c11b419e0e373fbe83db42522d3c5f25
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Prise en charge de Windows 10 dans System Center Configuration Manager  

*S’applique à : System Center Configuration Manager (Current Branch)*


Découvrez les versions de Windows 10 prises en charge par Configuration Manager, notamment :
 -  [Windows 10 comme client Configuration Manager](#windows-10-as-a-client)
 -  [Kit de déploiement et d'évaluation Windows (ADK) pour Windows 10](#windows-10-adk)



## <a name="windows-10-as-a-client"></a>Windows 10 comme client
Configuration Manager tente d’assurer une prise en charge comme client pour chaque nouvelle version de Windows 10 dès que possible après sa publication. Étant donné que les produits ont des calendriers de développement et de publication distincts, la prise en charge assurée par Configuration Manager dépend du moment de leur mise en circulation respective.

Par exemple, une version de Configuration Manager est supprimée de la matrice quand la [prise en charge de cette version](/sccm/core/servers/manage/current-branch-versions-supported) se termine. De même, la prise en charge de versions de Windows 10 comme Enterprise 2015 LTSB or 1511 est supprimée de la matrice quand elles seront retirées de la prise en charge. Pour plus d’informations, consultez [Systèmes d’exploitation dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).

-   Ces informations viennent s’ajouter à [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

-   Si vous utilisez LTSB (Long Term Servicing Branch) de Configuration Manager, consultez [Configurations prises en charge pour Long Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
Le tableau suivant liste les versions de Windows 10 que vous pouvez utiliser comme client avec différentes versions de Configuration Manager.

| Version de Windows 10 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| Entreprise 2016 LTSB            <!--10/13/2026-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1607   <br />(*voir éditions*)   <!--04+6/10/2018-->   | ![Pris en charge](media/green_check.png) <sup>1</sup> | ![Pris en charge](media/green_check.png) <sup>1</sup> | ![Pris en charge](media/green_check.png) <sup>1</sup> |
| 1703   <br />(*voir éditions*)   <!--10+6/09/2018-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1709   <br />(*voir éditions*)   <!--04+6/09/2019-->   | ![Compatibilité descendante](media/blue_compat.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1803   <br />(*voir éditions*)   <!--11/12/2019-->   | ![Non pris en charge](media/Red_X.png) | ![Non pris en charge](media/Red_X.png) | ![Pris en charge](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Éditions :** Entreprise, Professionnel, Éducation, Professionnel Éducation   

<sup>1</sup> Pour plus d’informations, consultez [Infos-clés sur le cycle de vie Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) et la section « Extension de maintenance pour les éditions Entreprise et Éducation ».

| Clé |
|--|
| ![Prise en charge](media/green_check.png) = **Prise en charge**  |
| ![Rétrocompatible](media/blue_compat.png)  = **Rétrocompatible** <br/> Les fonctionnalités de gestion du client existantes devraient fonctionner avec cette nouvelle version Windows 10. Par exemple, l’inventaire matériel, l’inventaire logiciel et les mises à jour logicielles. Nous documentons tous problèmes connus ou mises en garde. <br><br>Cette approche vous offre la possibilité de déployer et de gérer de nouvelles versions de Windows immédiatement avec prise en charge de la compatibilité des applications et sans nécessiter de nouvelle version de mise à jour de Configuration Manager. |
| ![Non pris en charge](media/Red_X.png) = **Non pris en charge** |

 > [!NOTE]  
 > À compter de la version 1802, Configuration Manager prend en charge le client sur les appareils Windows 10 ARM64. Les fonctionnalités de gestion du client existantes devraient fonctionner avec ces nouveaux appareils, par exemple, l’inventaire matériel et logiciel, les mises à jour logicielles et la gestion des applications. Le déploiement de système d’exploitation n’est pas pris en charge pour le moment. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Quand vous déployez des systèmes d’exploitation avec Configuration Manager, le [Windows ADK est une dépendance externe](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) obligatoire.

Le tableau suivant répertorie les versions du Windows 10 ADK que vous pouvez utiliser avec différentes versions de Configuration Manager.

| Version de Windows 10 ADK  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1703  | ![Pris en charge](media/green_check.png) | ![Compatibilité descendante](media/blue_compat.png) | ![Compatibilité descendante](media/blue_compat.png) |
| 1709  | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1803  | ![Non pris en charge](media/Red_X.png)   | ![Non pris en charge](media/Red_X.png) | ![Pris en charge](media/green_check.png) |

|Clé|
|--|
| ![Prise en charge](media/green_check.png) = **Prise en charge** <br/> Windows recommande d’utiliser le Windows ADK qui correspond à la version de Windows que vous déployez. Par exemple, utilisez le Windows ADK pour Windows 10 version 1703 quand vous déployez Windows 10 version 1703. Pour plus d’informations sur la prise en charge du composant Windows ADK, consultez [Plateformes prises en charge par DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) et [Exigences de l’outil USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Rétrocompatible](media/blue_compat.png)  = **Rétrocompatible** <br/> Cette combinaison n’est pas testée mais devrait fonctionner. Nous documentons tous problèmes connus ou mises en garde. |
| ![Non pris en charge](media/Red_X.png) = **Non pris en charge** |

 > [!Note]  
 > Configuration Manager prend uniquement en charge les composants x86 et amd64 de Windows 10 ADK. Il ne prend pas en charge les composants ARM ou ARM64 pour l’instant. 