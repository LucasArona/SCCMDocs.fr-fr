---
title: Connexion avec la cogestion de cloud
titleSuffix: Configuration Manager
description: Cogestion offre une valeur immédiate lorsque vous l’activez.
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754908"
---
# <a name="cloud-connecting-with-co-management"></a>Connexion avec la cogestion de cloud

![Bannière de la série blastoff](media/blastoff-banner.png)

Cogestion ajoute de nouvelles fonctionnalités à votre déploiement de Configuration Manager existant, sans modifier la façon dont vous travaillez déjà. Lorsque vous activez la cogestion, immédiatement commencer bénéficiant à partir du cloud. Vous pouvez appliquer cette valeur à vos processus et l’infrastructure de gestion existante.

Dans cette série de démarrage rapide de cogestion, consultez comment mener rapidement nouvelle valeur de gestion. La cogestion est générée pour créer des fonctionnalités et outils que vous pouvez utiliser dès maintenant.


Dans la vidéo suivante, vice-président Microsoft Brad Anderson introduit cette série de cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Cloud-Connecting-with-Co-Management/player]


| Valeur immédiate | Prise en main |
|-----------------|-----------------|
| - [Accès conditionnel](#bkmk_ca)<br> - [Actions à distance à partir d’Intune](#bkmk_remote)<br> - [Intégrité du client](#bkmk_client-health)<br> - [Azure AD hybride](#bkmk_hybrid-aad)<br> - [Windows Autopilot](#bkmk_autopilot) | - [Chemins d’accès à la cogestion](#bkmk_paths)<br> - [Configurer Azure AD hybride](#bkmk_setup-hybrid-aad)<br> - [Mise à niveau vers Windows 10](#bkmk_upgrade-win10)<br> - [Migration de MDM hybride](#bkmk_migrate-hybrid-mdm)<br> - [Obtenir l’aide de FastTrack](#bkmk_fasttrack) | 



## <a name="immediate-value"></a>Valeur immédiate

| | | |
|-|-|-|
| <a name="bkmk_ca"></a>**Accès conditionnel avec la conformité des appareils** | Contrôler l’accès utilisateur aux ressources d’entreprise en fonction des règles de conformité d’Intune | [![Miniature de vidéo de l’accès conditionnel](media/thumbnail-conditional-access.png)](/sccm/comanage/quickstart-conditional-access) |
| <a name="bkmk_remote"></a>**Actions à distance à partir d’Intune** | Exécuter des actions à distance à partir de Intune des périphériques cogérés. Par exemple, réinitialiser et réinitialiser un appareil et tenir à jour l’inscription et compte | [![Miniature de vidéo d’actions à distance](media/thumbnail-remote-action.png)](/sccm/comanage/quickstart-remote-actions) |
| <a name="bkmk_client-health"></a>**Intégrité du client Configuration Manager** | Maintenir la visibilité du contrôle d’intégrité du client Configuration Manager à partir d’Intune sur le portail Azure | [![Miniature de vidéo d’intégrité de client](media/thumbnail-client-health.png)](/sccm/comanage/quickstart-client-health) |
| <a name="bkmk_hybrid-aad"></a>**Azure Active Directory (Azure AD)** | Avec Azure AD vous pouvez tirer parti d’une productivité accrue pour vos utilisateurs et de la sécurité pour vos ressources, dans des environnements cloud et local | [![Miniature de vidéo d’Azure AD hybride](media/thumbnail-azure-ad.png)](/sccm/comanage/quickstart-hybrid-aad) |
| <a name="bkmk_autopilot"></a>**Windows Autopilot** | Réduire le temps, ressources et la complexité associés à déployer, gérer et mise hors service ou recyclage des appareils. AutoPilot crée également une meilleure expérience pour les utilisateurs finaux. | [![Miniature de vidéo de Windows Autopilot](media/thumbnail-autopilot.png)](/sccm/comanage/quickstart-autopilot) |



## <a name="getting-started"></a>Prise en main

Si vous souhaitez activer la cogestion, commencez ici pour débloquer les vous devrez peut-être des problèmes techniques.

| | | |
|-|-|-|
| <a name="bkmk_paths"></a>**Chemins d’accès à la cogestion** | Il existe deux méthodes principales pour configurer la cogestion, et il est important de comprendre les conditions préalables pour chaque chemin d’accès.  Chaque chemin d’accès nécessite une combinaison d’Azure AD, ConfigMgr, Intune et Windows client. | [![Miniature de la diapositive de chemins d’accès de cogestion](media/thumbnail-paths.png)](/sccm/comanage/quickstart-paths) |
| <a name="bkmk_setup-hybrid-aad"></a>**Configurer Azure AD hybride** | Si votre environnement comporte actuellement des appareils Windows 10 joints au domaine, configurez hybride Azure AD avant d’activer la cogestion | [![Miniature de hybride Azure AD de configurer la vidéo](media/thumbnail-setup-azure-ad.png)](/sccm/comanage/quickstart-setup-hybrid-aad) |
| <a name="bkmk_upgrade-win10"></a>**Mise à niveau vers Windows 10** | Windows 10 version 1709 ou ultérieure est requis pour la cogestion | [![Miniature de la mise à niveau Windows 10 vidéo](media/thumbnail-upgrade-win10.png)](/sccm/comanage/quickstart-upgrade-win10) |
| <a name="bkmk_migrate-hybrid-mdm"></a>**Migration de MDM hybride** | MDM hybride (Intune intégré à Configuration Manager) est déconseillée. Version autonome d’Intune est nécessaire pour la cogestion. | [![Miniature de migrer la vidéo MDM hybride](media/thumbnail-migrate-hybrid-mdm.png)](/sccm/comanage/quickstart-migrate-hybrid-mdm) |
| <a name="bkmk_fasttrack"></a>**Obtenir l’aide de FastTrack** | L’organisation de FastTrack est un grand groupe d’ingénieurs de Microsoft spécialisés pour aider à tous les types d’organisations de déployer des applications de Microsoft 365, y compris la configuration de la cogestion. | [![Miniature de vidéo de FastTrack](media/thumbnail-fasttrack.png)](/sccm/comanage/quickstart-fasttrack) |

