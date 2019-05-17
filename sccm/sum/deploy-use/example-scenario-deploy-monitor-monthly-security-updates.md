---
title: Exemple de scénario pour le déploiement et la surveillance des mises à jour logicielles de sécurité
titleSuffix: Configuration Manager
description: Suivez cet exemple de scénario pour découvrir comment utiliser les mises à jour logicielles dans Configuration Manager pour déployer et surveiller les mises à jour logicielles de sécurité mensuelles publiées par Microsoft.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02c1f1cbc80bacf35306d2e4d5367a41ec5d8c1c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496321"
---
# <a name="example-scenario-for-using-system-center-configuration-manager-to-deploy-and-monitor-the-security-software-updates-released-monthly-by-microsoft"></a>Exemple de scénario d’utilisation de System Center Configuration Manager pour le déploiement et la surveillance des mises à jour logicielles de sécurité publiées chaque mois par Microsoft

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique présente un exemple de scénario qui montre comment utiliser les mises à jour logicielles dans System Center Configuration Manager pour déployer et surveiller les mises à jour logicielles de sécurité publiées chaque mois par Microsoft.  

 Dans ce scénario, John est l’administrateur de Configuration Manager à la Woodgrove Bank. Il doit créer une stratégie de déploiement de mises à jour logicielles respectant les conditions et les spécifications suivantes :  

- Un déploiement actif de mises à jour logicielles doit avoir lieu une semaine après la publication par Microsoft des mises à jour logicielles de sécurité, le deuxième mardi de chaque mois. Cet événement est souvent désigné par l'expression « Patch Tuesday ».  

- Les mises à jour logicielles sont téléchargées et répliquées sur les points de distribution. Un déploiement est ensuite testé sur un sous-ensemble de clients, avant que John ne déploie entièrement les mises à jour logicielles dans son environnement de production.  

- John doit pouvoir surveiller la compatibilité des mises à jour logicielles par mois ou par année.  

  Dans ce scénario, nous supposons que l'infrastructure du point de mise à jour logicielle a déjà été mise en œuvre. Utilisez les informations ci-dessous pour planifier et configurer les mises à jour logicielles dans Configuration Manager.  

|Processus|Référence|  
|-------------|---------------|  
|Passez en revue les concepts clés liés aux mises à jour logicielles.|[Présentation des mises à jour logicielles](../understand/software-updates-introduction.md)|  
|Planifiez les mises à jour logicielles. Ces informations vous aident à déterminer l'infrastructure de point de mise à jour logicielle et à planifier les besoins en capacité, l'installation du point de mise à jour logicielle, les paramètres de synchronisation et les paramètres des clients pour les mises à jour logicielles.|[Planifier les mises à jour logicielles](../plan-design/plan-for-software-updates.md)|  
|Configurez les mises à jour logicielles. Ces informations vous aident à installer et à configurer les points de mise à jour logicielle de votre hiérarchie, et facilitent également la configuration et la synchronisation des mises à jour logicielles.<br /><br /> Dans ce scénario, John planifie les synchronisations des mises à jour logicielles pour qu’elles aient lieu le deuxième mercredi de chaque mois. Il s’assure ainsi de toujours récupérer les dernières mises à jour logicielles de sécurité auprès de Microsoft.|[Synchroniser les mises à jour logicielles](../get-started/synchronize-software-updates.md)|  

 Les sections suivantes de cette rubrique présentent des exemples d’étapes à suivre pour déployer et surveiller les mises à jour logicielles de sécurité dans Configuration Manager au sein de votre organisation.

##  <a name="BKMK_Step1"></a> Étape 1 : Créer un groupe de mises à jour logicielles pour la compatibilité annuelle  
 John crée un groupe de mises à jour logicielles, qu’il va ensuite utiliser pour surveiller la compatibilité de toutes les mises à jour logicielles de sécurité déployées en 2016. Il suit la procédure décrite dans le tableau ci-dessous.  

|Processus|Référence|  
|-------------|---------------|  
|Dans le nœud **Toutes les mises à jour logicielles** de la console Configuration Manager, John ajoute des critères pour afficher uniquement les mises à jour logicielles de sécurité ayant été publiées ou révisées en 2015 et respectant les critères suivants :<br /><br /><ul><li>**Critère**: Date de publication ou de révision</li><li>**Condition**: est supérieure ou égale à une date spécifique<br />**Valeur**: 01/01/2015</li><li>**Critères**: Classification des mises à jour<br />**Valeur**: Mises à jour de sécurité</li><li>**Critère**: Expiré <br />**Valeur**: Non</li></ul>|Aucune information supplémentaire|
|John ajoute toutes les mises à jour logicielles ainsi filtrées à un nouveau groupe de mises à jour logicielles respectant les spécifications suivantes :<br /><br /><ul><li>**Nom**: Groupe de compatibilité - Mises à jour de sécurité Microsoft 2015</li><li>**Description**: Mises à jour logicielles|[Ajouter des mises à jour logicielles à un groupe de mises à jour](add-software-updates-to-an-update-group.md)|  

##  <a name="BKMK_Step2"></a> Étape 2 : Créer une règle de déploiement automatique pour le mois actuel  
 John crée une règle de déploiement automatique pour les mises à jour logicielles de sécurité publiées par Microsoft pour le mois en cours. Il suit la procédure décrite dans le tableau ci-dessous.  

|Processus|Référence|  
|-------------|---------------|  
|John crée une règle de déploiement automatique respectant les spécifications suivantes :<br /><br /><ol><li>Sous l'onglet **Général** , John effectue la configuration suivante :<br /> <ul><li>Spécifie **Mises à jour de sécurité mensuelles** comme nom.</li><li>Sélectionne un regroupement de tests contenant un petit nombre de clients.</li><li>Sélectionne **Créer un groupe de mises à jour logicielles**.</li><li>Vérifie que l’option **Activer le déploiement après l’exécution de cette règle** n’est pas sélectionnée.</li></ul></li><li>Sous l'onglet **Paramètres de déploiement** , John sélectionne les paramètres par défaut.</li><li>Dans la page **Mises à jour logicielles**, John configure les filtres de propriétés et les critères de recherche suivants :<br /><ul><li>Date de publication ou de révision : **Dernier mois**.</li><li>Classification des mises à jour : **Mises à jour de sécurité**.</li></ul></li><li>Dans la page **Évaluation**, John configure la règle pour qu’elle soit exécutée à intervalle régulier, le **deuxième mardi** de **chaque mois**. John vérifie également que les synchronisations sont planifiées pour s’exécuter le **deuxième mercredi** de chaque **mois**.</li><li>John conserve les paramètres par défaut des pages Calendrier de déploiement, Expérience utilisateur, Alertes et Paramètres de téléchargement.</li><li>Dans la page **Package de déploiement**, John spécifie un nouveau package de déploiement.</li><li>Sur les pages Emplacement de téléchargement et Sélection de la langue, John conserve les paramètres par défaut.</li></ol>|[Déployer automatiquement des mises à jour logicielles](automatically-deploy-software-updates.md)|  

##  <a name="BKMK_Step3"></a> Étape 3 : Vérifier que les mises à jour logicielles sont prêtes à être déployées  
 Le deuxième jeudi de chaque mois, John vérifie que les mises à jour logicielles sont prêtes à être déployées. Il effectue l’étape suivante.  

|Processus|Référence|  
|-------------|---------------|  
|John vérifie que la synchronisation des mises à jour logicielles s'est bien déroulée.|[État de synchronisation des mises à jour logicielles](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="BKMK_Step4"></a> Étape 4 : déployer le groupe de mises à jour logicielles  
 Une fois qu'il a vérifié que les mises à jour logicielles sont prêtes à être déployées, John les déploie. Il suit la procédure décrite dans le tableau ci-dessous.  

|Processus|Référence|  
|-------------|---------------|  
|John crée deux déploiements de test pour le nouveau groupe de mises à jour logicielles. Pour chaque déploiement, il envisage les environnements suivants :<br /><br /> **Déploiement de test des stations de travail**: pour le déploiement de test des stations de travail, John effectue les opérations suivantes :<br /><br /><ul><li>Spécifie un regroupement de déploiements qui contient un sous-ensemble de clients de station de travail, en vue de vérifier le déploiement.</li><li>Configure les paramètres de déploiement appropriés pour les clients de station de travail de son environnement.</li></ul><br />**Déploiement de test des serveurs**: pour le déploiement de test des serveurs, John effectue les opérations suivantes :<br /><br /><ul><li>Spécifie un regroupement de déploiements qui contient un sous-ensemble de clients de serveur, en vue de vérifier le déploiement.</li><li>Configure les paramètres de déploiement appropriés pour les clients de serveur de son environnement.</li></ul>|[Déployer des mises à jour logicielles](deploy-software-updates.md)|  
|John vérifie que les déploiements de test ont été correctement déployés.|[État de déploiement des mises à jour logicielles](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|John met à jour les deux déploiements en utilisant les nouveaux regroupements contenant ses stations de travail et ses serveurs de production.|Aucune information supplémentaire|  

##  <a name="BKMK_Step5"></a> Étape 5 : Surveiller la compatibilité des mises à jour logicielles déployées  
 John surveille la compatibilité de ses déploiements de mises à jour logicielles. Il suit la procédure décrite dans le tableau ci-dessous.  

|Processus|Référence|  
|-------------|---------------|  
|John surveille l’état du déploiement des mises à jour logicielles dans la console Configuration Manager et examine les rapports de déploiement de mises à jour logicielles accessibles via la console.|[Surveiller les mises à jour logicielles dans System Center Configuration Manager](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="BKMK_Step6"></a> Étape 6 : Ajouter les mises à jour logicielles mensuelles au groupe de mises à jour annuel  
 John ajoute les mises à jour logicielles du groupe de mises à jour logicielles mensuel au groupe de mises à jour logicielles annuel. Il suit la procédure décrite dans le tableau ci-dessous.  

|Processus|Référence|  
|-------------|---------------|  
|John sélectionne les mises à jour logicielles dans le groupe de mises à jour logicielles mensuel et ajoute les mises à jour logicielles au groupe de mises à jour logicielles qu'il a créé pour la compatibilité annuelle. Il effectue un suivi de la compatibilité des mises à jour logicielles et crée différents rapports à des fins de gestion.|[Ajouter des mises à jour logicielles à un groupe de mises à jour déployé](add-software-updates-to-an-update-group.md)|  

John a procédé correctement au déploiement mensuel des mises à jour logicielles de sécurité. Il continue de surveiller la compatibilité des mises à jour logicielles et de créer les rapports correspondants, pour vérifier que les clients de son environnement respectent les niveaux de compatibilité définis.  

##  <a name="BKMK_MonthlyProcess"></a> Processus périodique mensuel de déploiement des mises à jour logicielles  
 À partir du deuxième mois de déploiement des mises à jour logicielles, John suit les étapes trois à six, afin de déployer les mises à jour logicielles de sécurité publiées chaque mois par Microsoft.  
