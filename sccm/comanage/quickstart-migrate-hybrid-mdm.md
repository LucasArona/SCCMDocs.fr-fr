---
title: Migrer à partir de MDM hybride
titleSuffix: Configuration Manager
description: MDM hybride est déprécié. Intune autonome est nécessaire pour la cogestion.
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754912"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Migrer à partir de MDM hybride pour la cogestion

La gestion hybride des appareils mobiles (MDM) est une fonctionnalité dépréciée. La prise en charge de MDM hybride se termine le 1er septembre 2019. Pour plus d’informations, consultez [MDM hybride avec Configuration Manager et Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Intune autonome est la topologie de déploiement recommandée et est nécessaire pour la cogestion. Si vous voulez activer la cogestion, migrez d’une configuration hybride d’Intune vers Intune autonome. 

Dans la vidéo suivante, le program manager principal, Andrew McMurray, et le directeur du marketing produit senior, Mayunk Jain, parlent et font la démonstration de la migration à partir de MDM hybride :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Marche à suivre

Votre migration vers Intune autonome sera optimale si vous utilisez une approche progressive. Avec ce type d’approche, vous déplacez une petite partie d’utilisateurs et d’appareils, tandis que la plupart de vos utilisateurs et appareils restent gérés par MDM hybride. Après avoir vérifié que la migration a réussi, vous pouvez commencer la migration d’autres ressources vers Intune.

Pour commencer la migration, utilisez l’[outil Microsoft Intune Data Importer](/sccm/mdm/deploy-use/migrate-import-data) pour collecter et automatiser le processus de recréation des objets à partir de Configuration Manager dans votre locataire autonome Intune. Ensuite, changez votre autorité MDM pour un ensemble d’utilisateurs spécifique, puis testez la fonctionnalité dans la version autonome d’Intune. Une fois cette vérification effectuée, changez votre autorité MDM pour la définir sur Intune autonome pour tous les utilisateurs.

> [!Important]  
> Si vous utilisez l’accès conditionnel local dans Configuration Manager, cette fonctionnalité nécessite actuellement Intune hybride.  

Pour plus d’informations sur ce processus de migration, consultez [Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Études de cas

L’équipe informatique de Microsoft a récemment déplacé 130 000 utilisateurs d’Intune hybride vers Intune autonome en trois mois. Pour plus d’informations, consultez la vidéo relative à l’[utilisation de l’accès conditionnel par Microsoft - Zone de point de terminaison 1812](https://youtu.be/offk-KH7eIA?t=651). Cette vidéo est une conversation entre le Vice-président de Microsoft, Brad Anderson, et le Directeur de la sécurité des systèmes d’information de Microsoft, Bret Arsenault, qui a personnellement supervisé la migration. 

Une grande entreprise pharmaceutique a déplacé 10 000 utilisateurs d’Intune hybride vers Intune autonome en quelques semaines.

Une grande société de conseil informatique basée en Inde a migré 40 000 utilisateurs d’Intune hybride vers Intune autonome en moins d’un mois.



## <a name="contact-fasttrack"></a>Contacter FastTrack

Si vous avez besoin d’assistance concernant la migration de MDM hybride à n’importe quelle étape du processus, accédez à [Microsoft FastTrack](https://Microsoft.com/FastTrack/), connectez-vous, puis demandez de l’aide. 

Pour plus d’informations, consultez [Obtenir l’aide de FastTrack](/sccm/comanage/quickstart-fasttrack). 

