---
title: Prise en charge de Windows 10
titleSuffix: Configuration Manager
description: Découvrir les versions de Windows 10 prises en charge comme clients ou pour OSD avec System Center Configuration Manager
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c20c4219ce9fedda0cf18d1f1fcc0241a9c058ca
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499488"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Prise en charge de Windows 10 dans Configuration Manager  

*S’applique à : System Center Configuration Manager (Current Branch)*

Découvrez les versions de Windows 10 prises en charge par Configuration Manager, notamment :
- [Windows 10 comme client Configuration Manager](#windows-10-as-a-client)
- [Kit de déploiement et d'évaluation Windows (ADK) pour Windows 10](#windows-10-adk)

> [!Tip]
> Les builds client de Windows Server sont prises en charge de la même façon que la version associée de Windows 10. Par exemple, Windows Server 2016 correspond à la même version de build que Windows 10 LTSB 2016, et Windows Server version 1803 correspond à la même version de build que Windows 10 version 1803.
> 
> Pour plus d’informations sur l’utilisation de Windows Server comme un système de site, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#the-server-core-installation-of-windows-server-version-1803).



## <a name="windows-10-as-a-client"></a>Windows 10 comme client

Configuration Manager tente d’assurer une prise en charge comme client pour chaque nouvelle version de Windows 10 dès que possible après sa publication. Étant donné que les produits ont des calendriers de développement et de publication distincts, la prise en charge assurée par Configuration Manager dépend du moment de leur mise en circulation respective.

Une version de Configuration Manager est supprimée de la matrice quand la [prise en charge de cette version](/sccm/core/servers/manage/current-branch-versions-supported) se termine. De même, la prise en charge des versions de Windows 10, comme Enterprise 2015 LTSB ou 1511, sera supprimée de la matrice quand ces versions ne seront plus prises en charge.

- La dernière version Current Branch de Configuration Manager reçoit des mises à jour de sécurité et des mises à jour critiques, qui peuvent inclure des correctifs pour des problèmes liés aux versions de Windows 10. Lorsque Microsoft publie une nouvelle version Current Branch de Configuration Manager, les versions antérieures reçoivent uniquement les mises à jour de sécurité. Pour plus d’informations, consultez [Prise en charge des versions Current Branch de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).  

    > [!Note]  
    > Le meilleur moyen de rester à jour avec Windows 10 est de rester à jour avec Configuration Manager. Pour plus d’informations, consultez [Configuration Manager et Windows as a Service](/sccm/core/understand/configuration-manager-and-windows-as-service).  

- Ces informations viennent s’ajouter à [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

- Si vous utilisez LTSB (Long Term Servicing Branch) de Configuration Manager, consultez [Configurations prises en charge pour Long Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
Le tableau suivant liste les versions de Windows 10 que vous pouvez utiliser comme client avec différentes versions de Configuration Manager.

| Version de Windows 10 | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 | Configuration Manager 1810 | Configuration Manager 1902 |
|---------------------|-----|-----|-----|-----|-----|
| Entreprise 2015 LTSB <!--10/14/2025-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| Entreprise 2016 LTSB <!--10/13/2026-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| Enterprise LTSC 2019 <!--10/10/2028-->   | ![Non pris en charge](media/Red_X.png)   | ![Non pris en charge](media/Red_X.png)   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1607   <!--04/09/2019-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1703   <!--10/08/2019-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1709   <!--04/14/2020-->   | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1803   <!--11/10/2020-->   | ![Non pris en charge](media/Red_X.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |
| 1809   <!--04/12/2021?-->   | ![Non pris en charge](media/Red_X.png) | ![Non pris en charge](media/Red_X.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

> [!Note]  
> La prise en charge des versions de canal semi-annuel de Windows 10 comprend les éditions suivantes : Entreprise, Professionnel, Éducation et Professionnel Éducation.   

| Clé |
|--|
| ![Prise en charge](media/green_check.png) = **Prise en charge**  |
| ![Non pris en charge](media/Red_X.png) = **Non pris en charge** |

 > [!NOTE]  
 > À compter de la version 1802, Configuration Manager prend en charge le client sur les appareils Windows 10 ARM64. Les fonctionnalités de gestion du client existantes devraient fonctionner avec ces nouveaux appareils, par exemple, l’inventaire matériel et logiciel, les mises à jour logicielles et la gestion des applications. Le déploiement de système d’exploitation n’est pas pris en charge pour le moment. <!-- 1353704 --> 

Pour plus d’informations sur le cycle de vie Windows, consultez la [fiche d’information sur le cycle de vie Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)



## <a name="windows-10-adk"></a>Windows 10 ADK

Quand vous déployez des systèmes d’exploitation avec Configuration Manager, Windows ADK est une dépendance externe obligatoire. Pour plus d’informations, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10).

> [!Important]  
> À compter de Windows 10 version 1809, Windows PE est fourni dans un programme d’installation distinct. Il n’existe aucune différence fonctionnelle.

<br/>
Le tableau suivant répertorie les versions du Windows 10 ADK que vous pouvez utiliser avec différentes versions de Configuration Manager.

| Version de Windows 10 ADK  | Configuration Manager 1710 | Configuration Manager 1802 | Configuration Manager 1806 | Configuration Manager 1810 | Configuration Manager 1902 |
|--------------------|-----|-----|-----|-----|-----|
| **1703**<br>(10.1.15063) | ![Compatibilité descendante](media/blue_compat.png) | ![Compatibilité descendante](media/blue_compat.png) | ![Non pris en charge](media/Red_X.png) | ![Non pris en charge](media/Red_X.png) | ![Non pris en charge](media/Red_X.png) |
| **1709**<br>(10.1.16299) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Compatibilité descendante](media/blue_compat.png) | ![Non pris en charge](media/Red_X.png)   | ![Non pris en charge](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Non pris en charge](media/Red_X.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Compatibilité descendante](media/blue_compat.png) | ![Compatibilité descendante](media/blue_compat.png) |
| **1809**<br>(10.1.17763) | ![Non pris en charge](media/Red_X.png) | ![Non pris en charge](media/Red_X.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) | ![Pris en charge](media/green_check.png) |

|Clé|
|--|
| ![Prise en charge](media/green_check.png) = **Prise en charge** <br/> Microsoft recommande d’utiliser le Windows ADK qui correspond à la version de Windows que vous déployez. Utilisez la dernière version du Windows ADK lors du déploiement de la dernière version de Windows 10. La dernière version du Windows ADK peut prendre en charge le déploiement d’anciennes versions du système d’exploitation, par exemple Windows 7.<!-- SCCMDocs issue 1229 --> Pour plus d’informations sur la prise en charge du composant Windows ADK, consultez [Plateformes prises en charge par DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) et [Exigences de l’outil USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Rétrocompatible](media/blue_compat.png)  = **Rétrocompatible** <br/> Cette combinaison n’est pas testée mais devrait fonctionner. Nous documenterons tous les problèmes connus, ainsi que les mises en garde. |
| ![Non pris en charge](media/Red_X.png) = **Non pris en charge** |

> [!Note]  
> Configuration Manager prend uniquement en charge les composants x86 et amd64 de Windows 10 ADK. Il ne prend pas en charge les composants ARM ou ARM64 pour l’instant. 

> [!Tip]
> Les builds de Windows Server ont les mêmes exigences Windows ADK que la version Windows 10 associée. Par exemple, Windows Server 2016 est la même version de build que Windows 10 LTSB 2016.
