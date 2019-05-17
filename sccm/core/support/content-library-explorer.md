---
title: Content Library Explorer
titleSuffix: Configuration Manager
description: Utilisez Content Library Explorer pour voir et dépanner la bibliothèque de contenu sur un point de distribution Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1fbd046115dcd4d13cec7a2bf880740a9dd616cc
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495761"
---
# <a name="content-library-explorer"></a>Content Library Explorer

*S’applique à : System Center Configuration Manager (Current Branch)*

Content Library Explorer fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez l’outil pour les activités suivantes :  

- Explorer la bibliothèque de contenu sur un point de distribution spécifique  

- Résoudre les problèmes avec la bibliothèque de contenu  

- Copier les packages, les contenus, les dossiers et les fichiers hors de la bibliothèque de contenu  

- Redistribuer les packages sur le point de distribution  

- Valider les packages sur des points de distribution distants  



## <a name="requirements"></a>spécifications

- Exécutez l’outil en utilisant un compte qui dispose d’un accès administrateur au :  

    - Point de distribution cible  

    - Fournisseur WMI sur le serveur de site  

    - Fournisseur Configuration Manager  

- Seuls les rôles **Administrateur complet** et **Analyste en lecture seule** ont les droits nécessaires pour voir toutes les informations de cet outil.  

    - D’autres rôles, comme **Administrateur d’application**, permettent de voir des informations partielles. Pour plus d’informations, consultez [Packages désactivés](#bkmk_disabled-packages).  

    - L’**Analyste en lecture seule** ne peut pas redistribuer les packages de cet outil.  

- Exécutez l’outil sur n’importe quel ordinateur tant que celui-ci peut se connecter au :  

    - Point de distribution cible  

    - Serveur de site principal  

    - Fournisseur Configuration Manager  

- Si le point de distribution est colocalisé avec le serveur de site, il est quand même nécessaire d’avoir un accès administrateur au serveur de site.  



## <a name="usage"></a>Utilisation 

Lorsque vous démarrez **ContentLibraryExplorer.exe**, entrez le nom de domaine complet (FQDN) du point de distribution cible. L’outil se connecte ensuite au point de distribution. Si le point de distribution fait partie d’un site secondaire, il vous demande le nom de domaine complet du serveur de site principal et le code du site principal.

Dans le volet gauche, affichez les packages qui sont distribués sur ce point de distribution. Développez les packages et explorez leur structure de dossiers. Cette structure correspond à la structure de dossiers à partir de laquelle vous avez créé le package.

Lorsque vous sélectionnez un dossier, l’outil affiche tous les fichiers du dossier dans le volet droit. Cette vue comprend les informations suivantes : 
- Nom de fichier
- Taille du fichier
- Lecteur sur lequel il se trouve
- Autres packages qui utilisent le même fichier sur le lecteur
- La dernière fois que le fichier a été modifié sur le point de distribution

L’outil se connecte également au fournisseur Configuration Manager. Cette connexion sert à déterminer quels packages sont distribués sur le point de distribution et s’ils se trouvent dans la bibliothèque de contenu du point de distribution. Par exemple, un package qui est en attente de distribution risque de ne pas être encore dans la bibliothèque de contenu. Ce package apparaît comme « PENDING » dans l’outil et ne peut faire l’objet d’aucune action.


### <a name="bkmk_disabled-packages"></a> Packages désactivés

Certains packages sont présents sur le point de distribution mais ne sont pas visibles dans la console Configuration Manager. Ces packages sont marqués d’un astérisque (\*). Aucune action ne peut être effectuée sur ces packages. D’autres packages peuvent aussi être marqués d’un astérisque sans aucune action possible. 

Les packages peuvent être désactivés pour trois raisons principales :  

- Le package est la mise à niveau du client Configuration Manager. Ce package contient « ccmsetup.exe ».  

- Votre compte d’utilisateur ne peut pas accéder au package, probablement en raison de l’administration basée sur les rôles. Par exemple, le rôle **Auteur d’application** ne permet pas de voir les packages de pilote dans la console, donc les packages de pilote sur le point de distribution sont marqués comme désactivés.  

- Le package est orphelin sur le point de distribution.  


### <a name="validate-packages"></a>Valider les packages

Validez les packages à l’aide de **Package** > **Validate** dans la barre d’outils. Commencez par sélectionner un nœud de package dans le volet gauche, et non pas un contenu ou un dossier. Pour cette action, l’outil se connecte au fournisseur WMI sur le point de distribution. Lorsque l’outil démarre, les packages auxquels il manque un ou plusieurs contenus sont marqués comme non valides. La validation du package révèle le contenu manquant. Si tout le contenu est présent mais que les données sont altérées, la validation détecte l’altération.


### <a name="redistribute-packages"></a>Redistribuer les packages

Redistribuez les packages à l’aide de **Package** > **Redistribute** dans la barre d’outils. Tout d’abord, sélectionnez un nœud de package dans le volet gauche. Cette action nécessite des autorisations pour redistribuer les packages.


### <a name="other-actions"></a>Autres actions

Utilisez **Edit** > **Copy** pour copier les packages, les contenus, les dossiers et les fichiers hors de la bibliothèque de contenu vers un dossier spécifié. Vous ne pouvez pas copier la bibliothèque de contenu elle-même. Sélectionnez plusieurs fichiers, par contre vous ne pouvez pas sélectionner plusieurs dossiers.

Recherchez des packages à l’aide de **Edit** > **Find Package**. Cette action répond à votre demande en recherchant dans le nom du package et l’ID du package.



## <a name="limitations"></a>Limitations

- L’outil ne peut pas manipuler la bibliothèque de contenu directement en aucune façon. Les changements apportés à la bibliothèque de contenu peuvent entraîner des dysfonctionnements.  

- L’outil peut redistribuer les packages, mais seulement sur le point de distribution cible.  

- Lorsque vous colocalisez le point de distribution avec le serveur de site, vous ne pouvez pas valider les données des packages. Utilisez plutôt la console Configuration Manager. L’outil inspecte quand même le package pour s’assurer que tout le contenu est présent, mais pas nécessairement intact.  

- Vous ne pouvez pas supprimer le contenu avec cet outil.



## <a name="see-also"></a>Voir aussi

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library)
