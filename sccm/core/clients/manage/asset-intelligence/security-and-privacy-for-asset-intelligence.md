---
title: Sécurité et confidentialité d’Asset Intelligence
titleSuffix: Configuration Manager
description: Obtenez des informations sur la sécurité et la confidentialité pour Asset Intelligence dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d0c6f7a0-dcae-4e6d-aa28-35d464d97ff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51bfe17980a7660ecdccfd13a11d6c7bcfd93e5f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344372"
---
# <a name="security-and-privacy-for-asset-intelligence-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations sur la sécurité et la confidentialité pour Asset Intelligence dans System Center Configuration Manager.  

##  <a name="BKMK_Security_AI"></a> Meilleures pratiques de sécurité pour Asset Intelligence  
 Utilisez les meilleures pratiques de sécurité suivantes dans l'optique d'utiliser Asset Intelligence.  

|Bonnes pratiques de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Lorsque vous importez un fichier de licence (fichier de licence en volume Microsoft ou fichier de déclaration générale de licence), sécurisez le fichier et le canal de communication.|Utilisez les autorisations du système de fichier pour vous assurer que seuls les utilisateurs autorisés peuvent accéder aux fichiers de licence et utilisez la signature SMB pour garantir l'intégrité des données lors de leur transfert au serveur de site pendant le processus d'importation.|  
|Utilisez le principe des autorisations minimales pour importer les fichiers de licence.|Utilisez l'administration basée sur les rôles pour accorder l'autorisation Gérer Asset Intelligence à l'utilisateur administratif qui importe des fichiers de licence. Le rôle intégré d'Asset Manager inclut cette autorisation.|  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informations confidentielles pour Asset Intelligence  
 Asset Intelligence étend les fonctions d’inventaire de Configuration Manager afin de permettre une meilleure visibilité des ressources au sein de l’entreprise. La collecte d'informations Asset Intelligence n'est pas activée automatiquement. Vous pouvez modifier le type d'informations collectées en activant les classes de rapport d'inventaire matériel. Pour plus d’informations, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Comme les informations d’inventaire, les informations Asset Intelligence sont stockées dans la base de données Configuration Manager. Lorsque les clients se connectent aux points de gestion à l'aide de HTTPS, les données sont toujours chiffrées lors du transfert vers le point de gestion. Lorsque les clients se connectent à l'aide de HTTP, vous pouvez configurer le transfert de données d'inventaire pour qu'il soit signé et chiffré. Les données d'inventaire ne sont pas stockées au format chiffré dans la base de données. Les informations sont conservées dans la base de données jusqu'à ce que la tâche de maintenance de site **Supprimer les historiques d'inventaire anciens** les supprime par intervalle de 90 jours. Vous pouvez configurer l'intervalle de suppression.  

 Asset Intelligence n'envoie pas d'informations sur les utilisateurs, les ordinateurs ou l'utilisation des licences à Microsoft. Vous pouvez choisir d'envoyer des requêtes System Center Online en vue d'une catégorisation. Ainsi, vous pouvez inventorier un ou plusieurs noms de logiciel sans catégorie et les envoyer dans System Center Online afin de les rechercher, puis de les classer. Une fois un nom de logiciel téléchargé, les fonctions de recherche de Microsoft l'identifient, le classent, puis le mettent à la disposition de tous les clients qui utilisent le service en ligne. Vous devez être conscient des conséquences de la soumission d'informations via System Center Online en termes de confidentialité :  

-   Le téléchargement s'applique uniquement aux informations génériques relatives au nom du logiciel (nom, éditeur, etc.) que vous choisissez d'envoyer au System Center Online. Les informations d'inventaire ne peuvent faire l'objet d'un téléchargement.  

-   Le téléchargement ne se produit jamais automatiquement et le système n'est pas conçu pour que cette tâche soit automatisée. Vous devez sélectionner et approuver manuellement le téléchargement de chaque nom de logiciel.  

-   Une boîte de dialogue vous indique exactement quelles données seront téléchargées, avant le démarrage du processus de téléchargement.  

-   Les informations de licence ne sont pas envoyées à Microsoft. Les informations de licence sont stockées dans une zone séparée de la base de données Configuration Manager et elles ne peuvent pas être envoyées à Microsoft.  

-   Tous les noms de logiciel téléchargés deviennent dès lors publiques, car l'application correspondante ainsi que sa classification sont intégrées au catalogue System Center Online Asset Intelligence, puis seront téléchargées par d'autres utilisateurs du catalogue.  

-   La source du nom du logiciel n'est pas enregistrée dans le catalogue Asset Intelligence. Elle n'est donc pas disponible pour les autres utilisateurs. Vous devez toutefois toujours veiller à ne pas charger de noms d'application contenant des informations confidentielles.  

-   Les données téléchargées ne peuvent pas être rappelées.  

 Avant de configurer le regroupement de données Asset Intelligence et de décider de soumettre des informations à System Center Online, pensez aux besoins de votre organisation en matière de confidentialité.  
