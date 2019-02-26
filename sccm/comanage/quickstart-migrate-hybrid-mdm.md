---
title: Migrer à partir de MDM hybride
titleSuffix: Configuration Manager
description: MDM hybride est déconseillée, Intune autonome est requis pour la cogestion.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84625c12c9cac643fe5a895c066632f44ffeacdc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754912"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migration de MDM hybride pour la cogestion

Gestion des appareils mobiles (MDM) hybride est une fonctionnalité déconseillée. Prend en charge des appareils mobiles hybride se termine sur le 1 septembre 2019. Pour plus d’informations, consultez [MDM hybride avec Configuration Manager et Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Version autonome d’Intune est la topologie de déploiement recommandée et est requis pour la cogestion. Si vous souhaitez activer la cogestion, migrer à partir d’une configuration hybride d’Intune vers Intune autonome. 

Dans la vidéo suivante, responsable de programme principal Andrew McMurray responsable marketing produit senior Mayunk Jain discuter et migration de MDM hybride de démonstration :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Marche à suivre

Votre migration vers Intune autonome sera optimale lorsque vous utilisez une approche progressive. Avec une migration en plusieurs phases, vous déplacez un petit sous-ensemble d’utilisateurs et appareils pendant que la plupart de vos utilisateurs et les appareils est toujours gérée avec des appareils mobiles hybride Une fois que vous vérifiez que la migration a réussi, vous pouvez commencer à davantage de ressources une migration vers Intune.

Pour commencer la migration, utilisez le [outil d’importation de données de Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data) pour collecter et d’automatiser le processus d’avoir à recréer les objets de Configuration Manager dans votre client d’autonome d’Intune. Ensuite, changer votre autorité MDM pour un ensemble spécifique d’utilisateurs et tester la fonctionnalité dans la version autonome d’Intune. Lorsque cette vérification est effectuée, modifier votre autorité de gestion des appareils mobiles vers Intune autonome pour tous les utilisateurs.

> [!Important]  
> Si vous utilisez l’accès conditionnel en local dans Configuration Manager, cette fonctionnalité nécessite actuellement Intune hybride.  

Pour plus d’informations sur ce processus de migration, consultez [migrer des appareils et utilisateurs MDM hybrides vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Études de cas

Microsoft IT récemment déplacé des 130 000 utilisateurs de Intune hybride vers Intune autonome des trois derniers mois. Pour plus d’informations, consultez [comment Microsoft utilise l’accès conditionnel - point de terminaison de Zone 1812](https://youtu.be/offk-KH7eIA?t=651). Cette vidéo est une conversation entre Microsoft vice-président Brad Anderson et de Microsoft directeur informatique sécurité Bret Arsenault qui dirigeait personnellement la migration. 

Une grande entreprise pharmaceutique déplacé 10 000 utilisateurs à partir d’Intune hybride vers Intune autonome dans quelques semaines.

Une grande société de conseil informatique en Inde migrés 40 000 utilisateurs Intune hybride vers Intune autonome dans moins d’un mois.



## <a name="contact-fasttrack"></a>Contactez FastTrack

Si vous avez besoin d’assistance de migration de MDM hybride à tout moment dans le processus, accédez à [Microsoft FastTrack](https://Microsoft.com/FastTrack/), connectez-vous, puis demander une assistance. 

Pour plus d’informations, consultez [obtenir de l’aide de FastTrack](/sccm/comanage/quickstart-fasttrack). 

