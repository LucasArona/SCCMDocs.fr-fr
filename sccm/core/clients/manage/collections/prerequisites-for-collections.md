---
title: Prérequis pour les regroupements
titleSuffix: Configuration Manager
description: Prenez connaissance des conditions préalables à l’utilisation de regroupements dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a53e4cf1-518a-4210-9c16-022c4261d2fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c05bbd53880e61687c76c1b8caee9f7c541092c3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130205"
---
# <a name="prerequisites-for-collections-in-system-center-configuration-manager"></a>Conditions préalables pour les regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les regroupements contiennent uniquement des dépendances à l’intérieur du produit.  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

|Dépendance|Informations complémentaires|  
|----------------|----------------------|  
|Point de Reporting Services|Le rôle de système de site du point de Reporting Services doit être installé pour pouvoir exécuter des rapports pour les regroupements. Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).|  
|Des autorisations de sécurité spécifiques doivent avoir été accordées pour gérer les regroupements|Vous devez disposer des autorisations de sécurité suivantes pour gérer les paramètres de compatibilité :<br /><br /> - Pour créer et gérer des regroupements : **Créer**, **Supprimer**, **Modifier**, **Modifier un dossier**, **Déplacer un objet**, **Lecture** et **Lire la ressource** pour l’objet **Regroupement**.<br /><br /> - Pour gérer les paramètres d’un regroupement : **Modifier les paramètres de regroupement** pour l’objet **Regroupement**.<br /><br /> L’autorisation **Modifier un dossier** est nécessaire pour tous les dossiers de regroupement, y compris le dossier racine.|  
