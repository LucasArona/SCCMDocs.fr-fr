---
title: Planifier et configurer les paramètres de compatibilité
titleSuffix: Configuration Manager
description: Découvrez les prérequis et les tâches de configuration pour l’utilisation des paramètres de compatibilité dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d728dae6dc67a4c66403bdb2299e50dcd6e3557
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677943"
---
# <a name="plan-for-and-configure-compliance-settings-in-system-center-configuration-manager"></a>Planifier et configurer les paramètres de compatibilité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de commencer à utiliser les paramètres de compatibilité System Center Configuration Manager, vous devez prendre connaissance de certains prérequis et de certaines tâches à effectuer.  

## <a name="prerequisites-for-compliance-settings"></a>Conditions préalables pour les paramètres de compatibilité  

|Condition préalable|Informations complémentaires|  
|------------------|----------------------|  
|Les clients Windows Configuration Manager doivent être activés et configurés pour l’évaluation de la compatibilité.|Voir ci-dessous|  
|Si vous souhaitez exécuter des rapports, vous devez configurer la création de rapports pour votre site.|[Rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md)|  
|Autorisations de sécurité requises.|Le rôle de sécurité **Gestionnaire de paramètres de compatibilité** inclut les autorisations nécessaires pour gérer les paramètres de compatibilité, les éléments de configuration des profils et données utilisateur, ainsi que les profils de connexion à distance.<br /><br /> [Configurer l’administration basée sur des rôles](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Activer et configurer les paramètres de compatibilité (pour les PC Windows uniquement)  

Cette procédure définit les paramètres de compatibilité client par défaut et s’applique à tous les ordinateurs de votre hiérarchie. Si vous voulez appliquer ces paramètres à certains ordinateurs seulement, créez un paramètre client d’appareil personnalisé et affectez-le à un regroupement qui contient les ordinateurs pour lesquels vous souhaitez utiliser des paramètres de compatibilité. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Les autres types d’appareils ne nécessitent aucune configuration spécifique pour évaluer les paramètres de compatibilité.  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client** > **Paramètres par défaut**.  
2.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  
3.  Dans la boîte de dialogue **Paramètres par défaut** , cliquez sur **Paramètres de compatibilité**.  
4.  Définissez les paramètres client suivants pour les paramètres de compatibilité :
    - **Activer l’évaluation de compatibilité sur les clients** : Affectez la valeur **Vrai** si vous souhaitez évaluer la compatibilité sur les appareils clients.
    - **Planifier l’évaluation de compatibilité** : Cliquez sur **Calendrier** si vous souhaitez modifier la planification d’évaluation de compatibilité par défaut sur les appareils clients.
    - **Activer les données et profils utilisateurs** : Activez cette option si vous souhaitez créer et déployer des éléments de configuration de profils et données utilisateur sur les ordinateurs Windows. Pour plus d’informations, consultez [Créer des éléments de configuration des données et profils utilisateur](/sccm/compliance/deploy-use/create-remote-connection-profiles).
5. Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres par défaut** .  

Les ordinateurs clients sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie du client.  
