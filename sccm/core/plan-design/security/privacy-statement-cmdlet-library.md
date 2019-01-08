---
title: Déclaration de confidentialité pour la bibliothèque d’applets de commande de Configuration Manager
description: Découvrez comment Microsoft collecte et utilise les données relatives à la bibliothèque d’applets de commande de System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb48f192146a3c0d4bbbe6f005dda537db871da7
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415481"
---
# <a name="system-center-configuration-manager-privacy-statement---configuration-manager-cmdlet-library"></a>Déclaration de confidentialité de System Center Configuration Manager – Bibliothèque d’applets de commande de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette déclaration de confidentialité couvre les fonctionnalités de la bibliothèque d’applets de commande de System Center Configuration Manager.  

## <a name="usage-data"></a>Données d’utilisation  

#### <a name="what-this-feature-does"></a>Descriptif de cette fonctionnalité   

La bibliothèque d’applets de commande de System Center Configuration Manager vous permet de gérer une hiérarchie Configuration Manager à l’aide d’applets de commande et de scripts Windows PowerShell. La bibliothèque d’applets de commande collecte des informations sur l’utilisation des applets de commande dans la bibliothèque pour identifier des tendances et des modèles d’utilisation. La bibliothèque d’applets de commande collecte également les types et le nombre d’erreurs que vous recevez quand vous utilisez les applets de commande.  

#### <a name="information-collected-processed-or-transmitted"></a>Informations collectées, traitées ou transmises
   
Les données d’utilisation collectées comprennent le démarrage, l’arrêt et l’interruption des applets de commande, l’exécution d’applets de commande dépréciées et des métriques d’activité pour les opérations du fournisseur SMS qui sont liées aux applets de commande. Ces informations ne permettent pas de vous identifier personnellement. Les informations collectées sur les erreurs comprennent les erreurs que les applets de commande renvoient ainsi que les détails des erreurs d’exception. Certains rapports détaillés sur les erreurs peuvent inclure par inadvertance des identificateurs individuels, comme le numéro de série d’un appareil connecté à votre ordinateur. La bibliothèque d’applets de commande filtre et rend anonymes les informations dans les rapports d’erreur pour supprimer les identificateurs individuels avant leur transmission à Microsoft.  

#### <a name="use-of-information"></a>Utilisation des informations
   
Microsoft utilise ces informations pour améliorer la qualité, la sécurité et l’intégrité des produits et services qu’elles propose.  

#### <a name="choicecontrol"></a>Choix/contrôle   

Cette fonctionnalité de données d’utilisation est activée par défaut. La bibliothèque d’applets de commande de System Center Configuration Manager a deux clés de Registre qui contrôlent cette fonctionnalité.  

 Pour la désactiver complètement, définissez la valeur de ces deux clés de Registre. Ils correspondent à chacun des fournisseurs de suivi d’événements pour Windows (ETW) :  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0 (désactive la fonctionnalité Données d’utilisation pour le fournisseur du lecteur)  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0 (désactive la fonctionnalité Données d’utilisation pour les applets de commande)  

  Les changements des paramètres de données d’utilisation sont spécifiques à l’ordinateur sur lequel ils sont apportés.  


## <a name="next-steps"></a>Étapes suivantes

[Documentation de la bibliothèque d’applets de commande de System Center Configuration Manager](https://docs.microsoft.com/powershell/sccm/configurationmanager/).   
