---
title: Content Library Transfer Tool
titleSuffix: Configuration Manager
description: Utilisez Content Library Transfer Tool pour transférer le contenu d’un lecteur de disque vers un autre sur un point de distribution Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d07bd0a-7012-47f7-8bc5-509a402915b7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f7375a62349aba30ee239aa34fa594650f5a844
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121979"
---
# <a name="content-library-transfer-tool"></a>Content Library Transfer Tool

*S’applique à : System Center Configuration Manager (Current Branch)*

Content Library Transfer Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Il transfère le contenu d’un lecteur de disque à un autre. L’outil est conçu pour s’exécuter sur les systèmes de site de points de distribution. Il prend en charge les points de distribution colocalisés avec un site ou des systèmes de site distants.  

L’outil est utile quand le lecteur de disque qui héberge la bibliothèque de contenu est plein. Tout d’abord, ajoutez ou identifiez un autre disque dur avec suffisamment d’espace pour héberger la bibliothèque de contenu. Utilisez ensuite **ContentLibraryTransfer.exe** pour transférer le contenu de l’ancien disque dur rempli vers le nouveau lecteur vide.
 
Une fois le transfert terminé, le contenu est accessible aux ordinateurs clients à partir du nouvel emplacement.



## <a name="usage"></a>Utilisation 

Exécutez **ContentLibraryTransfer.exe** en tant qu’utilisateur disposant d’autorisations administratives sur le point de distribution. 

#### <a name="syntax"></a>Syntaxe 
`ContentLibraryTransfer.exe –SourceDrive <drive letter of source drive> –TargetDrive <drive letter of destination drive>`

#### <a name="example"></a>Exemple
`ContentLibraryTransfer –SourceDrive E –TargetDrive G`



## <a name="limitations"></a>Limitations

- Exécutez l’outil localement sur le point de distribution. Vous ne pouvez pas l’exécuter à partir d’un ordinateur distant.  

- Utilisez-le uniquement quand les clients n’accèdent pas activement au point de distribution. Si vous exécutez l’outil alors que les clients accèdent au contenu, la bibliothèque de contenu sur le lecteur de destination peut présenter des données incomplètes. Le transfert de données peut échouer complètement et rendre la bibliothèque de contenu inutilisable.  

- Ne distribuez pas du contenu au point de distribution quand vous exécutez l’outil. Si vous exécutez l’outil alors que le contenu est en cours d’écriture sur le point de distribution, la bibliothèque de contenu sur le lecteur de destination peut présenter des données incomplètes. Le transfert de données peut échouer complètement et rendre la bibliothèque de contenu inutilisable.



## <a name="see-also"></a>Voir aussi

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)
- [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library)
