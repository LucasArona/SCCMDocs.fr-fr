---
title: Liste de contrôle de l’administrateur de gestion de l’alimentation
titleSuffix: Configuration Manager
description: Utilisez la liste de contrôle de l’administrateur pour planifier et implémenter la gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8198669fdf7d0acf3273af2d8a2e83f5b89f520c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156989"
---
# <a name="administrator-checklist-for-power-management-in-system-center-configuration-manager"></a>Liste de contrôle de l’administrateur de gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette liste de vérification de l'administrateur fournit les étapes recommandées pour l'utilisation de la gestion de l'alimentation System Center Configuration Manager au sein de votre organisation.  

## <a name="configuring-power-management"></a>Configuration de la gestion de l’alimentation  
 Suivez ces étapes pour vous aider à configurer votre hiérarchie afin de recueillir des informations sur la gestion de l'alimentation à partir d'ordinateurs client.  

> [!IMPORTANT]  
>  N'appliquez pas de modes d'alimentation pour les ordinateurs de votre hiérarchie avant d'avoir recueilli et analysé les données d'alimentation à partir d'ordinateurs client. Si vous appliquez les nouveaux paramètres de gestion de l'alimentation aux ordinateurs sans examiner préalablement les paramètres existants, cela peut entraîner une augmentation de la consommation d'énergie.  

|Tâche|Détails|  
|----------|-------------|  
|Passez en revue les concepts de gestion de l'alimentation dans la bibliothèque de documentation Configuration Manager.|Voir [Présentation de la gestion de l’alimentation](introduction-to-power-management.md).|  
|Passez en revue les prérequis de la gestion de l'alimentation dans la bibliothèque de documentation Configuration Manager.|Voir [Configuration requise pour la gestion de l’alimentation](prerequisites-for-power-management.md).|  
|Passez en revue les meilleures pratiques pour la gestion de l'alimentation.|Voir [Bonnes pratiques de gestion de l’alimentation](best-practices-for-power-management.md).|  
|Configurez vos regroupements pour gérer la consommation électrique des ordinateurs au sein de votre environnement.|Utilisez **Regroupement pour les rapports sur les données de base**, **Regroupement d’ordinateurs ne prenant pas en charge la gestion l’alimentation**, **Regroupements d’ordinateurs auxquels seront appliqués des modes de gestion de l’alimentation** et **Regroupements d’ordinateurs qui exécutent Windows Server** pour gérer les paramètres d’alimentation des ordinateurs dans votre hiérarchie. Vous pouvez créer plusieurs regroupements et appliquer différents modes d'alimentation à chaque regroupement.|  
|Activez la gestion de l'alimentation.|Avant de pouvoir commencer à utiliser la gestion de l'alimentation, vous devez l'activer et configurer les paramètres client requis. Pour plus d’informations, voir [Configuration de la gestion de l’alimentation](configuring-power-management.md).|  
|Recueillez des informations de gestion de l'alimentation à partir d'ordinateurs client.|Les données de gestion de l'alimentation sont communiquées par les clients via l'inventaire matériel Configuration Manager. Selon le calendrier d'inventaire matériel que vous avez configuré, la récupération de l'inventaire depuis tous les ordinateurs client peut prendre un certain temps.|  

## <a name="monitoring-and-planning-phase"></a>Phase de surveillance et de planification  

|Tâche|Détails|  
|----------|-------------|  
|Exécutez le rapport **Activité de l'ordinateur**.|Le rapport **Activité de l'ordinateur** affiche un graphique illustrant l'activité du moniteur, de l'ordinateur et de l'utilisateur pour un regroupement spécifique au cours d'une période donnée. Ce rapport est lié au rapport **Détails de l'activité de l'ordinateur** qui affiche les capacités de mise en veille et de mise en éveil des ordinateurs dans le regroupement spécifique. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Consommation énergétique** ou **Consommation énergétique journalière**.|Les rapports **Consommation énergétique** et **Consommation énergétique journalière** affichent la consommation énergétique mensuelle totale en kilowatts par heure (kWh) pour un regroupement spécifique au cours d'une période donnée. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Incidence sur l'environnement** ou  **Incidence journalière sur l'environnement**.|Les rapports **Incidence sur l'environnement** et **Incidence journalière sur l'environnement** affichent un graphique présentant les émissions de dioxyde de carbone (CO2) enregistrées par un regroupement spécifique d'ordinateurs au cours d'une période donnée. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Coût énergétique** ou **Coût énergétique journalier**.|Les rapports **Coût énergétique** et **Coût énergétique journalier** affichent le coût de la consommation énergétique totale au cours d'une période donnée. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Fonctions de gestion de l'alimentation**.|Le rapport **Fonctions de gestion de l'alimentation** affiche les fonctions de gestion de l'alimentation des ordinateurs dans le regroupement spécifique. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Paramètres d'alimentation**.|Le rapport **Paramètres d'alimentation** affiche une liste agrégée des paramètres d'alimentation actuels utilisés par les ordinateurs d'un regroupement spécifique. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Excluez tous les regroupements d'ordinateurs requis de la gestion de l'alimentation.|Voir [Configuration de la gestion de l’alimentation](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Veillez à enregistrer les informations provenant des rapports de gestion de l'alimentation générés pendant la phase de planification et de surveillance. Vous pouvez comparer ces données aux informations de gestion de l'alimentation générées pendant les phases de mise en œuvre et de conformité pour vous aider à évaluer les économies à réaliser en matière de consommation énergétique, de coût de l'alimentation et d'incidence sur l'environnement lors de l'application d'un mode d'alimentation aux ordinateurs de votre hiérarchie.  

## <a name="enforcement-phase"></a>Phase de mise en œuvre  

|Tâche|Détails|  
|----------|-------------|  
|Sélectionnez les modes d'alimentation existants ou créez de nouveaux modes d'alimentation pour les regroupements d'ordinateurs de votre organisation.|Voir [Guide pratique pour créer et appliquer des modes de gestion de l’alimentation](create-and-apply-power-plans.md).|  
|Appliquez ces modes d'alimentation aux ordinateurs.|Voir [Guide pratique pour créer et appliquer des modes de gestion de l’alimentation](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Phase de compatibilité  

|Tâche|Détails|  
|----------|-------------|  
|Exécutez le rapport **Activité de l'ordinateur**.|Le rapport **Activité de l'ordinateur** affiche un graphique illustrant l'activité du moniteur, de l'ordinateur et de l'utilisateur pour un regroupement spécifique au cours d'une période donnée. Ce rapport est lié au rapport **Détails de l'activité par l'ordinateur** qui affiche les capacités de mise en veille et de mise en éveil des ordinateurs dans le regroupement spécifique. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Consommation énergétique** ou **Consommation énergétique journalière**.|Les rapports **Consommation énergétique** et **Consommation énergétique journalière** affichent la consommation énergétique mensuelle totale en kilowatts par heure (kWh) pour un regroupement spécifique au cours d'une période donnée. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Incidence sur l'environnement** ou **Incidence journalière sur l'environnement**.|Les rapports **Incidence sur l'environnement** et **Incidence journalière sur l'environnement** affichent un graphique présentant les émissions de dioxyde de carbone (CO2) enregistrées par un regroupement spécifique d'ordinateurs au cours d'une période donnée. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Exécutez le rapport **Coût énergétique** ou **Coût énergétique journalier**.|Les rapports **Coût énergétique** et **Coût énergétique journalier** affichent le coût de la consommation énergétique totale au cours d'une période donnée. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Résolution des problèmes  

|Tâche|Détails|  
|----------|-------------|  
|Si les ordinateurs de votre hiérarchie ne sont pas entrés en veille ou en veille prolongée, exécutez le rapport **Rapport sur la non mise en veille** pour afficher les causes possibles.|Le **Rapport sur la non mise en veille** affiche une liste des causes courantes qui ont empêché les ordinateurs d'entrer en veille ou en veille prolongée et le nombre d'ordinateurs affectés par chaque cause pendant une période spécifique. Pour plus d’informations, voir [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
|Si plusieurs modes d'alimentation sont appliqués à un seul ordinateur, le mode d'alimentation le moins restrictif est appliqué. Exécutez le rapport **Ordinateurs avec plusieurs modes de gestion de l'alimentation** pour afficher les ordinateurs auxquels sont appliqués plusieurs modes d'alimentation.|Voir **Ordinateurs avec plusieurs modes de gestion de l'alimentation** dans [Guide pratique pour surveiller et planifier la gestion de l’alimentation](monitor-and-plan-for-power-management.md).|  
