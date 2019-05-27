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
ms.openlocfilehash: 43dcbe3abc200ecf32a83888e7b9712efd21584e
ms.sourcegitcommit: 99dfe4fb9e9cfd20c44380ae442b3a5b895a0d9b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65214757"
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les requêtes vous permettent de récupérer des informations à partir de la base de données du site selon les critères que vous spécifiez. Configuration Manager collecte les informations de base de données de site pendant le fonctionnement standard. Par exemple, en utilisant les informations qui ont été collectées à partir de découverte ou d'inventaire, vous pouvez configurer une requête pour identifier les périphériques qui répondent aux critères spécifiés.  

 Pour plus d’informations sur les requêtes, consultez [Présentation des requêtes dans System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md). Pour plus d’informations sur les bonnes pratiques en matière de sécurité et les informations de confidentialité pour les opérations Configuration Manager qui collectent les informations que vous pouvez récupérer à l’aide de requêtes, consultez [Sécurité et confidentialité pour System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md).  

## <a name="security-best-practices-for-queries"></a>Bonnes pratiques de sécurité pour les requêtes

 Utilisez les meilleures pratiques de sécurité suivantes pour les requêtes.  

|Bonnes pratiques de sécurité|Informations complémentaires|  
|----------------------------|----------------------|  
|Lorsque vous exportez ou importez une requête qui est enregistrée dans un emplacement réseau, sécurisez l'emplacement et le canal de réseau.|Veillez à restreindre l'accès au dossier réseau.<br /><br /> Utilisez la signature SMB ou IPsec entre l’emplacement réseau et le serveur de site pour empêcher un intrus de falsifier les données de la requête avant leur importation.|  

## <a name="next-steps"></a>Étapes suivantes
  
[Sécurité et confidentialité pour System Center Configuration Manager](../../../core/plan-design/security/security-and-privacy.md)
