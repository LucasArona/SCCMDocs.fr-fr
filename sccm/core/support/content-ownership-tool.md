---
title: Content Ownership Tool
titleSuffix: Configuration Manager
description: Utilisez Content Ownership Tool pour modifier la propriété des packages orphelins dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 753d2681-ea72-4f47-94d1-ac10188d9d5b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 962b19f1849628776eb1b9059089f7ce8e6df3ee
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385980"
---
# <a name="content-ownership-tool"></a>Content Ownership Tool

*S’applique à : System Center Configuration Manager (Current Branch)*

Content Ownership Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Il modifie la propriété des packages orphelins dans Configuration Manager. Les packages orphelins n’ont pas de serveur de site propriétaire. Les packages peuvent devenir orphelins en supprimant le serveur de site pendant qu’ils sont toujours détenus par ce serveur de site.

Exécutez l’outil de propriété du contenu sur n’importe quel serveur de site dans la hiérarchie Configuration Manager. Connectez-vous en tant qu’utilisateur administratif avec des autorisations suffisantes sur le package.  

> [!Tip]  
> Utilisez **ContentLibraryCleanup.exe** dans `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` pour *supprimer* le contenu orphelin d’un point de distribution. Pour plus d’informations, consultez [Content Library Cleanup Tool](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool).  



## <a name="features"></a>Fonctionnalités

- Afficher tous les packages orphelins  

- Afficher tous les packages, même s’ils ne sont pas orphelins  

- Afficher l’état de la connexion à un site  

- Filtrer les packages par nom, code de site ou type de package  

- Trier par toute colonne affichée  

- Modifier l’affectation d’un ou de plusieurs packages en une seule action  

- Afficher la progression de l’activité de transfert de propriété  



## <a name="usage"></a>Utilisation

Exécutez **ContentOwnershipTool.exe** pour démarrer l’outil. Les autorisations d’administrateur local sur l’ordinateur ne sont pas nécessaires pour exécuter l’outil.

Il n’existe aucun paramètre de ligne de commande.

> [!Important]   
> Cet outil change la propriété d’un package orphelin. Le package proprement dit ne sort pas du point de distribution sur lequel il est stocké. Ce changement de propriété n’entraîne pas la mise à jour du package sur les points de distribution. Il n’amène pas non plus les clients à réévaluer la stratégie pour le déploiement du package. Après le changement de propriété, vérifiez que le nouveau serveur de site peut accéder aux fichiers sources. Il doit avoir au moins les autorisations **Lecture** sur les fichiers sources de chaque package. 



## <a name="see-also"></a>Voir aussi

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library)
