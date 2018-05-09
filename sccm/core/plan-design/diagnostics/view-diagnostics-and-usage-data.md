---
title: Afficher les données de diagnostic
titleSuffix: Configuration Manager
description: Affichez les données d’utilisation et de diagnostic pour vérifier que votre hiérarchie System Center Configuration Manager ne contient aucune information sensible.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15e6f84be22d90e937c33ebd3a24520e6832a751
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Comment afficher les données d’utilisation et de diagnostic pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez afficher les données d’utilisation et de diagnostic de votre hiérarchie System Center Configuration Manager pour vérifier qu’elle ne contient aucune information sensible ni identifiable. Les données de télémétrie sont résumées et stockées dans la table **TEL_TelemetryResults** de la base de données du site et mises en forme de manière à être utilisables et efficaces en programmation. Bien que les options suivantes vous offrent une vue des données exactes envoyées à Microsoft, celles-ci ne sont pas destinées à être utilisées à d’autres fins, comme l’analyse des données.  

Utilisez la commande SQL suivante pour voir le contenu de cette table et afficher les données exactes qui sont envoyées. (Vous pouvez également exporter ces données dans un fichier texte.) :  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  Avant d’installer la version 1602, la table qui stocke les données de télémétrie est **TelemetryResults**.  

Quand le point de connexion de service est en mode hors connexion, vous pouvez utiliser l’outil de connexion de service pour exporter les données d’utilisation et de diagnostic actives dans un fichier de valeurs séparées par des virgules (CSV). Exécutez l’outil de connexion de service sur le point de connexion de service en utilisant le paramètre **-Export**.  

##  <a name="bkmk_hashes"></a> Hachages unidirectionnels  
Certaines données se composent de chaînes de caractères alphanumériques aléatoires. Configuration Manager utilise l’algorithme SHA-256, qui utilise le hachage à sens unique, pour garantir que nous ne collectons pas de données potentiellement sensibles. L’algorithme laisse les données dans un état où elles peuvent encore être utilisées à des fins de comparaison et de corrélation. Par exemple, au lieu de collecter les noms des tables dans la base de données de site, un hachage unidirectionnel est capturé pour chaque nom de table. Ceci garantit que les noms de tables personnalisés que vous avez créés ou que des modules complémentaires d’un produit ont créés ne sont pas visibles. Nous pouvons ensuite effectuer le même hachage à sens unique des noms des tables SQL fournis par défaut dans le produit et comparer les résultats de deux requêtes pour déterminer l’écart de votre schéma de base de données par rapport aux paramètres par défaut du produit. Cet écart est ensuite utilisé pour améliorer les mises à jour qui nécessitent des modifications du schéma SQL.  

Lorsque vous affichez les données brutes, une valeur hachée apparaît dans chaque ligne de données. Il s’agit de l’ID de hiérarchie. Cette valeur hachée est utilisée pour garantir que les données sont corrélées avec la même hiérarchie, sans identification du client ou de la source.  

#### <a name="to-see-how-the-one-way-hash-works"></a>Pour voir comment fonctionne le hachage unidirectionnel  

1.  Obtenez l’ID de votre hiérarchie en exécutant l’instruction SQL suivante dans SQL Management Studio sur la base de données Configuration Manager : **select [dbo].[fnGetHierarchyID]\(\)**  

2.  Utilisez le script Windows PowerShell suivant pour réaliser le hachage en sens unique du GUID obtenu de la base de données. Vous pouvez alors le comparer à l’ID de hiérarchie dans les données brutes pour voir comment nous masquons ces données.  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  
