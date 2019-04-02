---
title: Connexion au cloud à l’aide de la cogestion
titleSuffix: Configuration Manager
description: La cogestion offre une valeur immédiate lorsque vous l’activez.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8d878443-90e7-46e4-9cd3-99e2a19b2ad0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ed92d6249e4459f1902f639840b142977994df9e
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754908"
---
# <a name="cloud-connecting-with-co-management"></a>Connexion au cloud à l’aide de la cogestion

![Bannière de la série Blastoff](media/blastoff-banner.png)

La cogestion ajoute de nouvelles fonctionnalités à votre déploiement Configuration Manager existant, sans modifier la façon dont vous travaillez déjà. Quand vous activez la cogestion, vous commencez immédiatement à tirer des bénéfices du cloud. Vous pouvez appliquer cette valeur à vos processus et infrastructure de gestion existants.

Dans cette série de démarrages rapides sur la cogestion, découvrez comment vous pouvez rapidement développer une nouvelle valeur de gestion. La cogestion est générée pour créer des fonctionnalités et outils que vous pouvez utiliser dès maintenant.


Dans la vidéo suivante, le Vice-président de Microsoft, Brad Anderson, présente cette série sur la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]


| Valeur immédiate | Prise en main |
|-----------------|-----------------|
| - [Accès conditionnel](#bkmk_ca)<br> - [Actions à distance à partir d’Intune](#bkmk_remote)<br> - [Intégrité du client](#bkmk_client-health)<br> - [Azure AD hybride](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Chemins vers la cogestion](#bkmk_paths)<br> - [Configurer Azure AD hybride](#bkmk_setup-hybrid-aad)<br> - [Mise à niveau vers Windows 10](#bkmk_upgrade-win10)<br> - [Migrer à partir de MDM hybride](#bkmk_migrate-hybrid-mdm)<br> - [Obtenir l’aide de FastTrack](#bkmk_fasttrack) | 



## <a name="immediate-value"></a>Valeur immédiate

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Accès conditionnel avec conformité de l’appareil** | Contrôlez l’accès utilisateur aux ressources d’entreprise en fonction des règles de conformité d’Intune | [![Miniature de la vidéo sur l’accès conditionnel](media/thumbnail-conditional-access.png)](/sccm/comanage/quickstart-conditional-access) |
| <a name="bkmk_remote"></a>**Actions à distance à partir d’Intune** | Exécutez des actions à distance à partir d’Intune pour les appareils cogérés. Par exemple, effacez et réinitialisez un appareil, et tenez à jour l’inscription et le compte | [![Miniature de la vidéo des actions à distance](media/thumbnail-remote-action.png)](/sccm/comanage/quickstart-remote-actions) |
| <a name="bkmk_client-health"></a>**Intégrité du client Configuration Manager** | Gérez la visibilité de l’intégrité du client Configuration Manager à partir d’Intune sur le portail Azure | [![Miniature de la vidéo sur l’intégrité du client](media/thumbnail-client-health.png)](/sccm/comanage/quickstart-client-health) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Avec Azure AD, vous pouvez tirer parti d’une productivité accrue pour vos utilisateurs et de la sécurité pour vos ressources, à la fois dans des environnements cloud et local | [![Miniature de la vidéo d’Azure AD hybride](media/thumbnail-azure-ad.png)](/sccm/comanage/quickstart-hybrid-aad) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Réduisez le temps, les ressources et la complexité associés au déploiement, à la gestion et à la mise hors service ou au recyclage des appareils. AutoPilot crée également une meilleure expérience pour les utilisateurs finaux. | [![Miniature de la vidéo de Windows Autopilot](media/thumbnail-autopilot.png)](/sccm/comanage/quickstart-autopilot) |



## <a name="getting-started"></a>Prise en main

Si vous souhaitez activer la cogestion, commencez ici pour résoudre les problèmes techniques que vous pouvez rencontrer.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Chemins vers la cogestion** | Il existe deux méthodes principales pour configurer la cogestion, et il est important de comprendre les prérequis pour chaque chemin.  Chaque chemin nécessite une combinaison d’Azure AD, de ConfigMgr, d’Intune et du client Windows. | [![Miniature de la diapositive des chemins vers la cogestion](media/thumbnail-paths.png)](/sccm/comanage/quickstart-paths) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configurer Azure AD hybride** | Si votre environnement comporte actuellement des appareils Windows 10 joints au domaine, configurez Azure AD hybride avant d’activer la cogestion | [![Miniature de la vidéo de configuration d’Azure AD hybride](media/thumbnail-setup-azure-ad.png)](/sccm/comanage/quickstart-setup-hybrid-aad) |
| <a name="bkmk_upgrade-win10"></a>**Mise à niveau vers Windows 10** | Windows 10 version 1709 ou ultérieure est nécessaire pour la cogestion | [![Miniature de la vidéo de mise à niveau vers Windows 10](media/thumbnail-upgrade-win10.png)](/sccm/comanage/quickstart-upgrade-win10) |
| <a name="bkmk_migrate-hybrid-mdm"></a>**Migrer à partir de MDM hybride** | MDM hybride (Intune intégré à Configuration Manager) est déprécié. Intune autonome est nécessaire pour la cogestion. | [![Miniature de la vidéo de migration à partir de MDM hybride](media/thumbnail-migrate-hybrid-mdm.png)](/sccm/comanage/quickstart-migrate-hybrid-mdm) |
| <a name="bkmk_fasttrack"></a>**Obtenir l’aide de FastTrack** | L’organisation FastTrack est un grand groupe d’ingénieurs Microsoft dont la spécialité est d’aider tous les types d’organisations à déployer des applications Microsoft 365, notamment la configuration de la cogestion. | [![Miniature de la vidéo FastTrack](media/thumbnail-fasttrack.png)](/sccm/comanage/quickstart-fasttrack) |

