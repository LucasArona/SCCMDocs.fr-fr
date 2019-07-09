---
title: Sécurité et confidentialité pour les requêtes
titleSuffix: Configuration Manager
description: Maîtrisez les bonnes pratiques en matière de sécurité et de confidentialité quand vous recherchez des informations dans la base de données du site.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0315124b44af4359528b590bf0a6b325bfd14eb1
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/04/2019
ms.locfileid: "67561983"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les requêtes vous permettent de récupérer des informations à partir de la base de données du site selon les critères que vous spécifiez. Configuration Manager collecte les informations de base de données du site pendant l’opération standard. Par exemple, en utilisant les informations collectées pendant la détection ou l'inventaire, vous pouvez configurer une requête pour identifier les périphériques qui répondent aux critères spécifiés.  

 Pour plus d’informations sur les requêtes, consultez [Présentation des requêtes dans System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Pour des informations sur les bonnes pratiques en matière de sécurité et de confidentialité en ce qui concerne les opérations de Configuration Manager qui collectent les données que vous pouvez récupérer à l’aide de requêtes, consultez [Sécurité et confidentialité pour System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Bonnes pratiques de sécurité pour les requêtes

 Utilisez les meilleures pratiques en matière de sécurité suivantes pour les requêtes.  

|Bonnes pratiques de sécurité|Informations complémentaires|  
|----------------------------|----------------------|  
|Lorsque vous exportez ou importez une requête enregistrée dans un emplacement réseau, sécurisez l'emplacement et le canal de réseau.|Veillez à restreindre l'accès au dossier réseau.<br /><br /> Utilisez la signature du protocole SMB (Server Message Block) ou la sécurité du protocole Internet (IPsec) entre l’emplacement réseau et le serveur de site pour empêcher un attaquant de falsifier les données de la requête avant leur importation.|  

## <a name="next-steps"></a>Étapes suivantes
  
[Sécurité et confidentialité pour System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
