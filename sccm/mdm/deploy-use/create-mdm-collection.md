---
title: Créer un regroupement MDM
titleSuffix: Configuration Manager
description: Créez un regroupement MDM via System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d271499baf48364fe24a8961cae767c46d05a332
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>Créer un regroupement MDM via System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Un regroupement d’utilisateurs Configuration Manager est obligatoire pour spécifier les utilisateurs qui peuvent inscrire des appareils dans la gestion. Vous pouvez utiliser seulement des regroupements d’utilisateurs (au lieu de regroupements d’appareils ) car les licences Intune sont affectées par utilisateur.

> [!NOTE]
> Pour inscrire des appareils avec Intune, vous n’avez pas besoin d’affecter des licences aux utilisateurs dans le portail Office 365 ou dans le portail Azure Active Directory. Vous devez seulement inclure les utilisateurs dans un regroupement qui est associé à l’abonnement Intune (dans une [étape ultérieure](configure-intune-subscription.md)).

À des fins de test, vous pouvez configurer une **règle directe** et ajouter des utilisateurs spécifiques qui peuvent inscrire des appareils. Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Regroupements d’utilisateurs**, cliquez sur l’onglet **Accueil** > **Créer** un groupe, puis cliquez sur **Créer un regroupement d’utilisateurs**. Pour une distribution plus large, utilisez **Règle de requête** et définissez des utilisateurs. Pour plus d’informations sur les regroupements, consultez [Guide pratique pour créer des regroupements](https://technet.microsoft.com/library/mt629371.aspx).

![Créer un regroupement d’utilisateurs pour MDM](../media/mdm-create-user-collection.png)

> [!div class="button"]
[Étape suivante >](confirm-dns.md)
