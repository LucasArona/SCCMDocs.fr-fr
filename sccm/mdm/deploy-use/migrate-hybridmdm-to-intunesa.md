---
title: Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune
titleSuffix: Configuration Manager
description: Découvrez comment faire migrer des utilisateurs et appareils MDM hybrides vers Intune sur Azure.
author: aczechowski
manager: dougeby
ms.date: 09/12/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: 4e2471b06c1767bcf914000d626bb22b6ee2bd6b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346319"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune

*S’applique à : System Center Configuration Manager (Current Branch)*    

Lorsque vous êtes prêt à commencer la migration de la gestion hybride des appareils mobiles (MDM) (Intune intégré à Configuration Manager) vers une expérience cloud uniquement à l’aide d’Intune sur Azure, cet article est fait pour vous. Si vous hésitez encore, consultez [Choisir entre la version autonome de Microsoft Intune et la gestion hybride des appareils mobiles avec System Center Configuration Manager](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management). 

Vous pouvez commencer la migration vers la version autonome d’Intune à l’aide d’une approche en plusieurs phases qui vous permet de tester un petit sous-ensemble d’utilisateurs et d’appareils tout en continuant à gérer la plupart de vos utilisateurs et appareils avec la gestion hybride des appareils mobiles. Ensuite, après avoir vérifié la fonctionnalité Intune, vous pouvez commencer la migration des autres utilisateurs vers Intune.    

Les rubriques suivantes indiquent les étapes de la migration des utilisateurs vers la version autonome d’Intune selon une approche progressive.    
  
1.  [Importer les données Configuration Manager dans Microsoft Intune](migrate-import-data.md)   
    L’outil d’importation de données Intune collecte des données sur les objets que vous sélectionnez dans votre hiérarchie Configuration Manager, fournit des détails sur les objets que vous pouvez sélectionner pour l’importation et des informations sur la raison pour laquelle un objet ne peut pas être importé, puis vous permet d’importer les objets sélectionnés dans votre locataire Microsoft Intune. Même si cette étape est facultative, elle peut vous faire gagner du temps en automatisant le processus de recréation des objets entre Configuration Manager et Intune. 
2.  [Préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md)    
    Validez les objets importés à partir de Configuration Manager, créez des objets, créez des groupes AAD et affectez des objets à ces groupes, installez les connecteurs NDES et Exchange, etc. Ces étapes et le démarrage de la migration vers la version autonome d’Intune doivent être transparents pour vos utilisateurs.  
3.  [Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte)](migrate-mixed-authority.md)    
    Configurez une autorité MDM mixte dans le même locataire en choisissant de gérer certains utilisateurs dans Intune et tous les autres appareils avec la gestion hybride des appareils mobiles (MDM) (Intune intégré à Configuration Manager). Vous pouvez tester si la fonctionnalité Intune se comporte comme prévu sur les appareils d’un petit sous-ensemble d’utilisateurs avant de commencer la migration d’autres utilisateurs. 
4.  [Remplacer l’autorité MDM par la version autonome d’Intune](change-mdm-authority.md)     
    Faites passer votre autorité MDM au niveau du locataire de Configuration Manager à Intune. Tous les utilisateurs et appareils restants migrent vers la version autonome d’Intune. Vous allez modifier votre autorité MDM au niveau du locataire après avoir soigneusement testé la fonctionnalité Intune à l’étape précédente et avoir fait migré la majorité ou la totalité de vos utilisateurs.