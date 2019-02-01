---
title: Données de diagnostic pour 1511
titleSuffix: Configuration Manager
description: En savoir plus sur les niveaux de données de diagnostic et d’utilisation collectés par System Center Configuration Manager version 1511.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 128ba61e75bfdbbaf6a3051317b9554253b96e87
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898237"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-system-center-configuration-manager"></a>Niveaux de collecte des données de diagnostic et d’utilisation pour la version 1511 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager version 1511 collecte trois niveaux de données d’utilisation et de diagnostic : **De base**, **Étendu** et **Complet**. Par défaut, cette fonctionnalité est définie sur le niveau Étendu. Les sections suivantes fournissent des détails supplémentaires sur les données collectées par chaque niveau.  

> [!IMPORTANT]  
>  Configuration Manager ne collecte pas les codes des sites, les noms des sites, les adresses IP, les noms d’utilisateur ou d’ordinateur, les adresses physiques ni les adresses e-mail aux niveaux De base et Étendu. Toute collecte de ces informations au niveau Complet n’est pas intentionnelle : elles peuvent être incluses dans des informations de diagnostic avancées comme des fichiers journaux ou des instantanés de la mémoire. Microsoft n’utilisera pas ces informations pour vous identifier ou vous contacter, ni à des fins publicitaires.  

##  <a name="bkmk_change"></a> Modification du niveau  
 Les administrateurs qui disposent d’une étendue administrative basée sur des rôles incluant les autorisations **Modification** sur la classe d’objets **Site** peuvent modifier le niveau des données collectées dans les paramètres des données de diagnostic et d’utilisation de la console Configuration Manager.

 Pour cela, dans la console, accédez à l’onglet Backstage (onglet supérieur gauche avec flèche déroulante), sélectionnez **Données d’utilisation**, puis le niveau de données à utiliser.  


##  <a name="bkmk_level1"></a> Niveau 1 - De base  
 Le niveau De base comprend les données relatives à votre hiérarchie, qui sont nécessaires pour aider à améliorer votre expérience d’installation ou de mise à niveau, ainsi que des données pour aider à identifier les mises à jour Configuration Manager qui s’appliquent à votre hiérarchie.  

 À compter de System Center Configuration Manager version 1511, ce niveau inclut les éléments suivants :  


-   Informations d’installation
    - Build, type d’installation, modules linguistiques et fonctionnalités que vous avez activées

    - État et erreurs du déploiement du package de mise à jour  

-   Métriques de performances de base de données (informations sur le traitement de la réplication, procédures stockées SQL Server les plus utilisées par processeur et utilisation des disques)  

-   Configuration de base de données simple (processeurs, configuration du cluster et configuration des vues distribuées)  

-   Schéma de base de données Configuration Manager (hachage de toutes les définitions d’objet)  

-   Nombre de versions du client Configuration Manager et de versions du système d’exploitation  

-   Nombre de systèmes d’exploitation des appareils gérés et stratégies définies par le connecteur Exchange  

-   Nombre de paramètres régionaux et de langues du client

-   Nombre d’appareils Windows 10 par branche et build  

-   Données de la hiérarchie des sites Configuration Manager de base (liste des sites, type, version, état, nombre de clients et fuseau horaire)  

-   Informations de serveur de système de site de base (rôles de système de site utilisés, état SSL et Internet, système d’exploitation, processeurs, ordinateur physique ou machine virtuelle)  

-   Statistiques de découverte d’utilisateurs de base (nombre de découvertes d’utilisateurs et tailles minimale/maximale/moyenne des groupes)  

-   Informations Endpoint Protection de base (versions du client de logiciel anti-programme malveillant)  

-   Nombres de types d’application et de déploiement de base (nombre total d’applications, nombre total d’applications avec plusieurs types de déploiement, nombre total d’applications avec des dépendances, nombre total d’applications remplacées, nombre de technologies de déploiement utilisées)  

-   Nombre de déploiements de systèmes d’exploitation de base (images)  

-   Types de point de distribution et de point de gestion, et informations de configuration de base (protégés, préparés, PXE, de multidiffusion, d’état SSL, points de distribution pairs/d’extraction, compatibles MDM, compatibles SSL, etc.)  

-   Statistiques de télémétrie (à l’exécution, runtime et erreurs)  

##  <a name="bkmk_level2"></a> Niveau 2 – Étendu  
Le niveau Étendu est configuré par défaut après l’installation. Ce niveau comprend les données collectées au niveau De base, ainsi que les données propres aux fonctionnalités (fréquence et durée d’utilisation), les paramètres du client Configuration Manager (nom du composant, état et paramètres tels que les intervalles d’interrogation) et les informations de base sur les mises à jour logicielles.  

Ce niveau est recommandé, car il fournit à Microsoft les données minimales requises pour apporter des améliorations utiles dans les futures versions des produits et services. Ce niveau ne collecte pas les noms des objets (sites, utilisateurs, ordinateur ou objets), les informations sur les objets relatifs à la sécurité ni les vulnérabilités telles que le nombre de systèmes qui nécessitent des mises à jour logicielles.  

À compter de System Center Configuration Manager version 1511, ce niveau inclut les éléments suivants :  

-   **Gestion des applications :**  

    -   Informations de base d’utilisation/de ciblage pour les types de déploiement utilisés au sein de l’organisation (ciblé utilisateur ou appareil, nécessaire ou disponible)  

    -   Informations de déploiement d’application (installation/désinstallation, approbation requise, et interaction utilisateur activée/désactivée)  

    -   Statistiques de demande d’application disponibles  

    -   Nombre de packages par type  

    -   Nombre d’applicabilités de l’application par système d’exploitation  

    -   Nombre de déploiements de package/programme  

    -   Nombre d’environnements App-V et propriétés de déploiement  

    -   Nombre de licences d’application Windows 10 concédées  

    -   Nombre minimal/maximal/moyen de déploiements d’application par utilisateur/appareil  

    -   Type et durée de fenêtre de maintenance  

-   **Client :**  

    -   Liste/nombre d’agents clients activés  

    -   Nombre d’installations de client à partir de chaque type d’emplacement source  

    -   Nombre d’échecs d’installation de client  

-   **Paramètres de compatibilité :**  

    -   Nombre d’éléments de configuration par type  

    -   Informations de la ligne de base de configuration de base (nombre, nombre de déploiements et nombre de références)  

    -   Nombre de déploiements qui font référence à des paramètres intégrés (la valeur du paramètre n’est pas capturée)  

    -   Nombre de règles et de déploiements qui sont créés pour les paramètres personnalisés  

    -   Nombre de modèles de protocole SCEP déployés  

-   **Contenu :**  

    -   Nombre de limites par type  

    -   Informations sur les groupes de limites (nombre de limites et de systèmes de site qui sont attribués à chaque groupe de limites)  

    -   Informations sur les groupes de points de distribution (nombre de packages et de points de distribution qui sont attribués à chaque groupe de points de distribution)  

    -   Informations sur la configuration des points de distribution (utilisation de BranchCache et surveillance des points de distribution)  

    -   Informations sur la configuration du gestionnaire de distribution (threads, délai de nouvelle tentative, nombre de nouvelles tentatives et paramètres de point de distribution d’extraction)  

-   **Endpoint Protection :**  

    -   Utilisation des stratégies du Pare-feu Windows et de logiciel anti-programme malveillant Endpoint Protection (nombre de stratégies uniques attribuées au groupe)<br /><br />Cela ne comprend pas les informations sur les paramètres inclus dans la stratégie.  

    -   Erreurs de déploiement Endpoint Protection (nombre de codes d’erreur de déploiement de stratégie Endpoint Protection)  

    -   Nombre de regroupements sélectionnés pour être affichés dans le tableau de bord Endpoint Protection  

    -   Nombre d’alertes configurées pour la fonctionnalité Endpoint Protection  

-   **Gestion des applications mobiles (MAM) :**  

    -   Nombre d’applications métier et d’applications Office compatibles GAM, et stratégies par système d’exploitation  

    -   Nombre de déploiements de stratégie/application MAM  

    -   Nombre de règles créées par paramètre GAM  

-   **Gestion des appareils mobiles (MDM) :**  

    -   Nombre de commandes (verrouiller, réinitialiser, mettre hors service) d’actions d’appareil mobile émises

    -   Nombre d’appareils mobiles gérés par Configuration Manager et Microsoft Intune, et méthode d’inscription (en bloc ou basée sur l’utilisateur)  

    -   Statistiques et calendrier d’interrogation des appareils mobiles pour la vérification dans la durée des appareils mobiles  

    -   Nombre de stratégies d’appareil mobile  

    -   Nombre d’utilisateurs qui ont plusieurs appareils mobiles inscrits  

-   **Dépannage de Microsoft Intune :**  

    -   Nombre et taille des messages d’état, de statut, d’inventaire, RDR, DDR, UDX, d’état de locataire, POL, LOG, de certificat, CRP, de resynchronisation, CFD, RDO, BEX, ISM et de conformité qui sont téléchargés à partir de Microsoft Intune  

    -   Nombre et taille des messages d’actions d’appareil (réinitialiser, mettre hors service, verrouiller), de télémétrie et de données qui sont répliqués vers Microsoft Intune  

    -   Statistiques de synchronisation utilisateur complète et différentielle pour Microsoft Intune  

-   **Gestion des appareils mobiles (MDM) locale :**  

    -   Statistiques de réussite/échec de déploiement pour les déploiements d’applications de gestion MDM locale  

    -   Nombre de profils et de packages d’inscription en bloc Windows 10  

-   **Déploiement du système d’exploitation :**  

    -   Nombre d’images de démarrage, de pilotes, de packages de pilotes, de points de distribution en multidiffusion, de points de distribution compatibles PXE et de séquences de tâches  

-   **Mises à jour logicielles :**  

    -   Nombre total/moyen de regroupements comportant des déploiements de mises à jour logicielles et nombre maximal/moyen de mises à jour déployées  

    -   Nombre de règles de déploiement automatique qui sont liées à la synchronisation  

    -   Nombre de règles de déploiement automatique qui créent de nouvelles mises à jour ou ajoutent des mises à jour à un groupe existant  

    -   Différentiels de disponibilité et d’échéance qui sont utilisés dans les règles de déploiement automatique  

    -   Nombre moyen et maximal d’attributions par mise à jour  

    -   Nombre de mises à jour créées et déployées à l’aide de System Center Update Publisher  

    -   Nombre de groupes et d’attributions de mises à jour  

    -   Nombre de packages de mises à jour et nombre maximal/minimal/moyen de points de distribution qui sont ciblés par les packages  

    -   Nombre de groupes de mises à jour et nombre minimal/maximal/moyen de mises à jour par groupe  

    -   Nombre de mises à jour et pourcentage de mises à jour qui sont déployées, expirées, remplacées, téléchargées et qui contiennent des CLUF  

    -   Codes d’erreur d’analyse des mises à jour et nombre d’ordinateurs  

    -   Calendriers d’analyse et d’évaluation des mises à jour client  

    -   Planification de la synchronisation du point de mise à jour logicielle  

    -   Nombre de règles de déploiement automatique avec plusieurs déploiements  

    -   Configurations qui sont utilisées pour les plans de maintenance actifs de Windows 10  

    -   Versions de contenu du tableau de bord Windows 10  

    -   Nombre de clients Windows 10 qui utilisent Windows Update for Business  

    -   Statistiques d’application de correctifs logiciels au cluster  

    -   Nombre de mises à jour Office 365 déployées  

-   **Données de performances/SQL :**  

    -   Nombre des plus grandes tables de base de données  

    -   Informations sur les réplicas SQL Always-On  

    -   Nombre de regroupements par type  

##  <a name="bkmk_level3"></a> Niveau 3 – Complet  
Le niveau Complet inclut toutes les données des niveaux De base et Étendu. Il inclut également des informations supplémentaires sur Endpoint Protection, les pourcentages de compatibilité des mises à jour et les informations de mise à jour logicielle. Ce niveau peut également inclure des informations de diagnostic avancées telles que des fichiers système et des instantanés de la mémoire, qui peuvent inclure des informations personnelles qui existaient dans la mémoire ou les fichiers journaux au moment de la capture.  

À compter de System Center Configuration Manager version 1511, ce niveau inclut les éléments suivants :  

-   Statistiques d’évaluation et d’actualisation des regroupements  

-   Récapitulatif de l’intégrité Endpoint Protection (y compris le nombre de clients protégés, présentant un risque, inconnus et non pris en charge)  

-   Configuration de la stratégie Endpoint Protection  

-   Informations de déploiement de mise à jour logicielle (pourcentage de déploiements ciblés avec le client ou l’heure UTC, obligatoire/facultatif/en mode silencieux, et suppression du redémarrage)  

-   Compatibilité globale des déploiements de mise à jour logicielle  

-   Informations sur le calendrier d’évaluation de règle de déploiement automatique  

-   Nombre de clients avec des stratégies de protection d’accès réseau  

-   Nombres et codes d’erreur de déploiement de mise à jour logicielle  

-   Nombre minimal/maximal/moyen de clients inactifs dans les regroupements de déploiements de mise à jour logicielle  

-   Nombre de groupes avec des mises à jour logicielles expirées  

-   Nombre minimal/maximal/moyen de mises à jour logicielles par package  

-   Pourcentages de réussite d’analyse des mises à jour logicielles  

-   Nombre minimal/maximal/moyen d’heures depuis la dernière analyse des mises à jour logicielles  
