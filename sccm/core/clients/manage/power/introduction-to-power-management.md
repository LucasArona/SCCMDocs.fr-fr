---
title: Présentation de la gestion de l’alimentation
titleSuffix: Configuration Manager
description: Obtenez une présentation de la gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3ddff2a7-99eb-4ef8-b969-f3f7f24053db
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a86b430849945a01093a2eb136afd6d1aa363aaf
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122064"
---
# <a name="introduction-to-power-management-in-system-center-configuration-manager"></a>Présentation de la gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion de l’alimentation dans System Center Configuration Manager répond au besoin de nombreuses organisations de contrôler et réduire la consommation d’énergie de leurs ordinateurs. Cette fonctionnalité tire parti des fonctionnalités de la gestion de l'alimentation intégrée à Windows pour appliquer les paramètres pertinents et cohérents aux ordinateurs de l'organisation. Vous pouvez appliquer différents paramètres d'alimentation aux ordinateurs pendant les heures de bureau et les heures creuses. Par exemple, vous pouvez souhaiter appliquer un mode d'alimentation plus restrictif aux ordinateurs pendant les heures creuses. Dans les cas où les ordinateurs doivent toujours rester allumés, vous pouvez empêcher l'application des paramètres de gestion de l'alimentation.  

 La gestion de l’alimentation dans Configuration Manager comprend plusieurs rapports permettant d’analyser la consommation énergétique et les paramètres d’alimentation des ordinateurs de votre organisation. Vous pouvez également utiliser les rapports pour vous aider à résoudre les problèmes de gestion de l'alimentation.  

 Pour obtenir un flux de travail détaillé sur la configuration et l’utilisation de la gestion de l’alimentation, consultez [Liste de contrôle de l’administrateur pour la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

> [!IMPORTANT]  
>  La gestion de l’alimentation dans Configuration Manager n’est pas prise en charge sur les ordinateurs virtuels. Vous ne pouvez pas appliquer les modes d'alimentation aux ordinateurs virtuels, ni signaler de données d'alimentation à partir de ces ordinateurs.  

## <a name="the-power-management-workflow"></a>Flux de travail de la gestion de l’alimentation  
 Appliquez les trois étapes suivantes pour planifier et mettre en œuvre la gestion de l’alimentation dans Configuration Manager.  

### <a name="monitoring-and-planning-phase"></a>Phase de surveillance et de planification  
 La gestion de l’alimentation utilise l’inventaire matériel de Configuration Manager pour recueillir des données sur les paramètres d’alimentation et d’utilisation des ordinateurs du site. Il existe un certain nombre de rapports que vous pouvez utiliser pour analyser ces données et déterminer les paramètres optimaux de gestion de l'alimentation pour les ordinateurs. Par exemple, pendant la phase de surveillance et de planification du flux de travail de la gestion de l'alimentation, vous pouvez créer des regroupements à partir des données incluses dans le rapport **Fonctions de gestion de l'alimentation** et utiliser ces données pour identifier les ordinateurs qui ne sont pas capables d'effectuer la gestion de l'alimentation. Ensuite, vous pouvez exclure ces ordinateurs de la gestion de l'alimentation.  

> [!IMPORTANT]  
>  N'appliquez pas de modes d'alimentation aux ordinateurs de votre site avant de recueillir et d'analyser les données d'alimentation d'ordinateurs client. Si vous appliquez de nouveaux paramètres de gestion de l'alimentation aux ordinateurs sans examiner préalablement les paramètres existants, vous risquez d'observer une augmentation de la consommation d'énergie.  

### <a name="enforcement-phase"></a>Phase de mise en œuvre  
 La gestion de l'alimentation vous permet de créer des modes d'alimentation que vous pouvez appliquer aux regroupements d'ordinateurs de votre site. Ces modes d'alimentation configurent les paramètres de gestion de l'alimentation Windows sur les ordinateurs. Vous pouvez utiliser les modes de gestion de l’alimentation inclus dans Configuration Manager ou configurer vos propres modes personnalisés. Vous pouvez utiliser les données d'alimentation recueillies pendant la phase de surveillance et de planification comme ligne de base pour vous aider à évaluer les économie d'énergie après avoir appliqué un mode d'alimentation aux ordinateurs. Pour plus d’informations, consultez [Liste de contrôle de l’administrateur pour la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/administrator-checklist-for-power-management.md).  

### <a name="compliance-phase"></a>Phase de compatibilité  
 Dans la phase de compatibilité, vous pouvez exécuter des rapports qui vous aident à évaluer les économies à réaliser en matière de consommation énergétique et de coût de l'alimentation dans votre organisation. Vous pouvez également exécuter des rapports décrivant les améliorations relatives à la quantité de CO2 générée par les ordinateurs. Il existe également des rapports qui vous aident à vérifier que les paramètres d'alimentation ont été correctement appliqués aux ordinateurs, ce qui vous aide à résoudre les problèmes liés à la fonction de gestion de l'alimentation.  
