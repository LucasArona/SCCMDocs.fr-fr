---
title: Chemins vers la cogestion
titleSuffix: Configuration Manager
description: Comprenez les prérequis des deux méthodes principales dont vous disposez pour configurer la cogestion.
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754844"
---
# <a name="paths-to-co-management"></a>Chemins vers la cogestion

Vous disposez de deux méthodes principales pour configurer la cogestion. Il est important de comprendre les prérequis pour chaque chemin. Ils nécessitent chacun une combinaison d’Azure Active Directory (Azure AD), de Configuration Manager, de Microsoft Intune et de Windows 10. 

1. [Inscrire automatiquement les appareils gérés par Configuration Manager existants dans Intune](#bkmk_path1)  
2. [Démarrer le client Configuration Manager avec un provisionnement récent](#bkmk_path2)  

![Diagramme des chemins de cogestion](media/co-management-paths.png)



## <a name="bkmk_path1"></a> Chemin 1 : Inscrire automatiquement les clients existants

Le choix de ce chemin peut vous permettre d’inscrire rapidement vos appareils gérés par Configuration Manager existants dans Intune. La gestion de ces appareils depuis Configuration Manager ne diffère pas de celle que vous aviez avant d’activer la cogestion. C’est juste que maintenant vous avez tous les avantages cloud. Ce chemin est transparent pour vos utilisateurs.

Voici ce que vous devez faire pour le configurer :
- Azure AD hybride
    - Active Directory Federation Services (ADFS) avec authentification pass-through (PTA)
    - Azure AD Connect
    - Licence Azure AD Premium
    - Configurer la jonction Azure AD hybride (choisissez une option) :
        - Pour les domaines gérés
        - Pour les domaines fédérés
- Paramètre d’agent du client pour la jonction Azure AD hybride
- Configurer l’inscription automatique des appareils à Intune
- Attribuer des licences utilisateur Intune
- Activer la cogestion dans Configuration Manager

Pour un tutoriel sur ce chemin, consultez [Tutoriel : Activer la cogestion pour les clients Configuration Manager existants](/sccm/comanage/tutorial-co-manage-clients).



## <a name="bkmk_path2"></a> Chemin 2 : Démarrer avec un provisionnement récent

Voici ce que vous devez faire pour le configurer :

1. [Configurer HTTP avancé](/sccm/core/plan-design/hierarchy/enhanced-http)  
2. [Créer les services cloud dans Azure](/sccm/core/servers/deploy/configure/azure-services-wizard)  
3. [Configurer le point de gestion et les clients pour utiliser la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  
4. [Utiliser Intune pour déployer le client Configuration Manager](/sccm/comanage/how-to-prepare-win10)  

> [!Note]  
> Un tutoriel pour ce chemin sera disponible prochainement.

