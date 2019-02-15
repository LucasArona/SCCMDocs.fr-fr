---
title: Définitions de programmes malveillants Endpoint Protection à partir d’un partage réseau
titleSuffix: Configuration Manager
description: Découvrez comment télécharger manuellement les dernières mises à jour de définitions de Microsoft et configurer ensuite les clients pour le téléchargement de ces définitions.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ddef4d2a-f481-4020-9ddd-9cca5f9795cb
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2dbe2c5ecfbf58248f1bc391d39d6e0b86b86bc2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140454"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-a-network-share-for-configuration-manager"></a>Activer le téléchargement des définitions de programmes malveillants pour Endpoint Protection à partir d’un partage réseau dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez télécharger manuellement les dernières mises à jour de définition à partir de Microsoft et configurer les clients pour télécharger ces définitions à partir d’un dossier partagé sur le réseau. Les utilisateurs peuvent également lancer des mises à jour de définition quand vous utilisez cette source de mise à jour.

> [!NOTE]
>  Les clients doivent avoir un accès en lecture au dossier partagé pour pouvoir télécharger des mises à jour de définition.

 Pour plus d’informations sur le téléchargement des mises à jour des définitions et des moteurs à stocker sur le partage de fichiers, consultez [Install the latest Microsoft antimalware and antispyware software](https://www.microsoft.com/wdsi/definitions) (Installer les derniers logiciels anti-programme malveillant et anti-espion de Microsoft).

## <a name="to-configure-definition-downloads-from-a-file-share"></a>Pour configurer les téléchargements de définitions à partir d’un partage de fichiers

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.

2.  Dans l’espace de travail **Ressources et Conformité** , développez **Endpoint Protection**, puis cliquez sur **Stratégies anti-programme malveillant**.

3.  Ouvrez la page de propriétés de la **Stratégie de logiciel anti-programme malveillant par défaut** ou créez une stratégie de logiciel anti-programme malveillant. Pour plus d’informations sur la création de stratégies de logiciel anti-programme malveillant, consultez [Guide pratique pour créer et déployer des stratégies de logiciel anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Dans la section **Mises à jour de définitions** de la boîte de dialogue des propriétés du logiciel anti-programme malveillant, cliquez sur **Définir la source**.

5.  Dans la boîte de dialogue **Configurer les sources de mise à jour de définition** , sélectionnez **Mises à jour à partir des partages de fichier UNC**.

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Configurer les sources de mise à jour de définition** .

7.  Cliquez sur **Définir les chemins**. Ensuite, dans la boîte de dialogue **Configurer les chemins d’accès UNC de mise à jour de définition** , ajoutez un ou plusieurs chemins UNC à l’emplacement des fichiers de mise à jour de définition sur un partage réseau.

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Configurer les chemins d’accès UNC de mise à jour de définition** .


> [!div class="button"]
> [Étape suivante >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Retour >](endpoint-configure-alerts.md)
