---
title: Chemins vers la cogestion
titleSuffix: Configuration Manager
description: Comprendre les conditions préalables pour les deux principales façons pour vous permettent de configurer la cogestion.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5beb5564-2fdf-4f0a-8801-d0cec8214c43
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 803f05dd14da8d280f08f2bcf3608865f384d273
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754844"
---
# <a name="paths-to-co-management"></a>Chemins vers la cogestion

Il existe deux méthodes principales pour configurer la cogestion. Il est important de comprendre les conditions préalables pour chaque chemin d’accès. Ils requièrent chacun une combinaison d’Azure Active Directory (Azure AD), Configuration Manager, Microsoft Intune et Windows 10. 

1. [L’inscription automatique des appareils gérés par Configuration Manager existants dans Intune](#bkmk_path1)  
2. [Démarrer le client Configuration Manager avec l’approvisionnement moderne](#bkmk_path2)  

![Diagramme des chemins d’accès de la cogestion](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Chemin d’accès 1 : L’inscription automatique des clients existants

En prenant ce chemin d’accès peut obtenir vos appareils gérés par Configuration Manager existants rapidement inscrits dans Intune. La gestion de ces appareils à partir du Gestionnaire de Configuration ne diffère pas avant d’activer la cogestion. Vous avez maintenant tous les avantages de cloud. Ce chemin d’accès est transparent pour vos utilisateurs.

Voici ce que vous devez configurer :
- Azure AD hybride
    - Active Directory Federation Services (ADFS) avec l’authentification directe (PTA)
    - Azure AD Connect
    - Licence Azure AD Premium
    - Configurer hybride Azure AD-jointure (choisissez une option) :
        - Pour les domaines managés
        - Pour les domaines fédérés
- Agent du client de configuration pour hybride Azure AD-jointure
- Configurer l’inscription automatique des appareils à Intune
- Attribuer des licences utilisateur Intune
- Activer la cogestion dans Configuration Manager

Pour obtenir un didacticiel sur ce chemin d’accès, consultez [didacticiel : Activer la cogestion pour les clients Configuration Manager existants](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Chemin d’accès 2 : Démarrer avec l’approvisionnement moderne

Voici ce que vous devez configurer :

1. [Le programme d’installation améliorée HTTP](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Créer les services cloud dans Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurer le point de gestion et les clients à utiliser la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Utiliser Intune pour déployer le client Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Un didacticiel pour ce chemin d’accès sera bientôt disponible.

