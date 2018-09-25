---
title: Faire migrer des ressources MDM hybrides vers la version autonome d’Intune
titleSuffix: Configuration Manager
description: Découvrez comment faire migrer des utilisateurs et appareils MDM hybrides vers Intune sur Azure.
author: aczechowski
manager: dougeby
ms.date: 08/14/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 1dd696ce-3e46-4dfa-a76d-592fe0f0320e
ms.openlocfilehash: cff1a695f3f3227f7ec849b34b75762b082c3f31
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584828"
---
# <a name="migrate-hybrid-mdm-users-and-devices-to-intune-standalone"></a>Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune

*S’applique à : System Center Configuration Manager (Current Branch)*    

Cet article explique comment migrer d’une gestion MDM hybride vers une expérience cloud uniquement à l’aide d’Intune sur Azure. 

> [!Important]  
> Depuis le 14 août 2018, la gestion des appareils mobiles hybride est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, consultez [Qu’est-ce que la gestion MDM hybride ?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


Commencez la migration vers Intune autonome à l’aide d’une approche progressive. Avec cette approche, vous testez un petit sous-ensemble d’utilisateurs et d’appareils, mais la plupart de vos utilisateurs et appareils restent gérés par une solution MDM hybride. Après avoir vérifié la fonctionnalité Intune, commencez la migration d’autres ressources vers Intune.    

Pour plus d’informations, consultez les articles suivants :    
  
1.  [Importer les données de Configuration Manager dans Microsoft Intune](migrate-import-data.md)   

    L’outil Intune Data Importer :  

    - Collecte des données sur les objets que vous sélectionnez à partir de votre hiérarchie Configuration Manager  

    - Fournit des détails sur les objets que vous pouvez sélectionner pour l’importation   

    - Fournit des informations sur la raison pour laquelle certains objets ne peuvent pas être importés  

    - Vous permet d’importer les objets sélectionnés dans votre locataire Microsoft Intune  

    Cette étape est facultative. Elle peut vous faire gagner du temps en automatisant le processus de recréation des objets entre Configuration Manager et Intune.  

2.  [Préparer Intune pour la migration des utilisateurs](migrate-prepare-intune.md)    

    - Valider les objets importés à partir de Configuration Manager  

    - Créer des objets  

    - Créer des groupes Azure AD et affecter des objets à ces groupes  

    - Installer des connecteurs NDES et Exchange  

    Ces étapes et le démarrage de la migration vers la version autonome d’Intune doivent être transparents pour vos utilisateurs.   

3.  [Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte)](migrate-mixed-authority.md)    

    Configurer une autorité MDM mixte dans le même locataire. Sélectionnez certains utilisateurs à gérer dans Intune, tout en continuant à gérer tous les autres appareils avec une solution MDM hybride. Testez si la fonctionnalité Intune s’exécute correctement sur les appareils d’un petit sous-ensemble d’utilisateurs avant de commencer la migration d’autres utilisateurs.   

4.  [Remplacer l’autorité MDM par la version autonome d’Intune](change-mdm-authority.md)     

    Faites passer votre autorité MDM au niveau du locataire de Configuration Manager à Intune. Tous les utilisateurs et appareils restants migrent vers la version autonome d’Intune. Après avoir soigneusement testé la fonctionnalité Intune à l’étape précédente et avoir fait migrer la majorité ou la totalité de vos utilisateurs, modifiez votre autorité MDM au niveau du locataire.



## <a name="request-assistance"></a>Demander de l’aide
<!--Intune bug 2339232--> Pour demander de l’aide à partir du programme Microsoft FastTrack, accédez tout d’abord à [FastTrack pour Microsoft 365](https://fasttrack.microsoft.com/microsoft365/capabilities?view=security).

1. Cliquez sur « Connectez-vous » et entrez l’ID de votre organisation.  

2. Accédez au tableau de bord, puis suivez les invites pour accéder au formulaire de **demande d’assistance**.    

3. Microsoft examine votre demande et la transmet à l’équipe la mieux à même de répondre à vos besoins spécifiques et à votre éligibilité.  

Vous trouverez également dans ce tableau de bord les meilleures pratiques ainsi que des outils et des ressources fournis par les experts FastTrack pour vous aider à profiter pleinement de l’expérience Microsoft Cloud.

