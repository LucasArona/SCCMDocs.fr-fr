---
title: Role-based Administration Tool
titleSuffix: Configuration Manager
description: Utilisez Role-based Administration and Auditing Tool pour modéliser et auditer des étendues et des rôles de sécurité dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 533d055db3a68360c3c18d0e30e0718bf42c2a7c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500798"
---
# <a name="role-based-administration-and-auditing-tool"></a>Role-based Administration and Auditing Tool

*S’applique à : System Center Configuration Manager (Current Branch)*

Role-based Administration and Auditing Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez cet outil pour les tâches suivantes :

- Modéliser les rôles de sécurité avec des autorisations spécifiques  

- Auditer les étendues de sécurité et les rôles de sécurité qu’ont les autres utilisateurs



## <a name="requirements"></a>spécifications

- Exécutez-le sur le même ordinateur que la console Configuration Manager  

- Vous avez le rôle **Administrateur complet**, **Analyste en lecture seule** ou **Administrateur de sécurité**  

- Affectez votre compte à l’étendue de sécurité **Toutes** et à toutes les collections  

- (*Facultatif*) Pour analyser la sécurité du dossier de rapport, vous devez avoir accès à SQL  

- (*Facultatif*) Pour analyser les détails du rapport, exécutez cet outil sur le serveur de système de site avec le rôle de point de rapport



## <a name="procedures"></a>Procédures


### <a name="model-permissions-for-a-new-role"></a>Modéliser les autorisations d’un nouveau rôle

Utilisez la procédure suivante pour modéliser les autorisations d’un nouveau rôle que vous souhaitez créer : 

1. Exécutez **RBAViewer.exe**.  

2. Sélectionnez les rôles de sécurité de base qui vous intéressent ou commencez à partir d’un jeu d’autorisations vide. Sélectionnez les autorisations nécessaires.  

3. Cliquez sur **Analyser** pour voir l’interface utilisateur visible avec ce rôle personnalisé.  

    > [!Note]  
    > Pour voir si un rôle de sécurité existant répond à vos besoins, basculez vers l’onglet **Similarity**.  

4. Cliquez sur **Export** pour enregistrer le rôle en tant que fichier XML. Ensuite, importez-le dans la console Configuration Manager. Pour plus d’informations, consultez [Créer des rôles de sécurité personnalisés](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Auditer les étendues de sécurité existantes

Utilisez la procédure suivante pour auditer l’ensemble des utilisateurs d’administration, des regroupements et des étendues de sécurité dans Configuration Manager :

1. Exécutez **RBAViewer.exe**.  

2. Sélectionnez le bouton **Audit RBA** dans la barre d’outils.  

    1. Pour voir les relations limitées au regroupement dans une arborescence, basculez vers l’onglet **Collection Summary** (Résumé du regroupement).  

    2. Pour voir les objets affectés à un rôle de sécurité, basculez vers l’onglet **Scope Summary** (Résumé de l’étendue).  


### <a name="audit-a-specific-user"></a>Auditer un utilisateur spécifique

Pour auditer la configuration de l’administration basée sur des rôles d’un utilisateur spécifique, utilisez la procédure suivante :

1. Exécutez **RBAViewer.exe**.  

2. Sélectionnez le bouton **Run as** (Exécuter en tant que) dans la barre d’outils.  

3. Entrez le nom d’utilisateur spécifique pour vérifier les autorisations de ce compte.  

4. L’outil affiche les rôles de sécurité attribués à l’utilisateur ou au groupe de sécurité auquel l’utilisateur appartient. Il affiche aussi les objets que cet utilisateur peut voir et les actions qu’il peut effectuer dans la console.  



## <a name="see-also"></a>Voir aussi

- [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration)
- [Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration)
