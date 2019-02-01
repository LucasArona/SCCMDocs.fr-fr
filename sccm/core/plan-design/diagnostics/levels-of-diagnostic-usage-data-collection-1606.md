---
title: Données de diagnostic pour 1606
titleSuffix: Configuration Manager
description: En savoir plus sur les niveaux de données de diagnostic et d’utilisation collectés par System Center Configuration Manager version 1606.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7350d03-f440-4744-82d4-75f8c6c25028
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: af82e3b5d0f555494705a28fba291253c83b00ea
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898016"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1606-of-system-center-configuration-manager"></a>Niveaux de collecte des données de diagnostic et d’utilisation pour la version 1606 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager version 1606 collecte trois niveaux de données d’utilisation et de diagnostic : **De base**, **Étendu** et **Complet**. Par défaut, cette fonctionnalité est définie sur le niveau Étendu. Les sections suivantes fournissent des détails supplémentaires sur les données collectées par chaque niveau.

Les modifications par rapport aux versions précédentes sont indiquées par ***[Nouveau]***, ***[Mis à jour]***, ***[Supprimé]*** ou ***[Déplacé]***.


> [!IMPORTANT]
>  Configuration Manager ne collecte pas les codes des sites, les noms des sites, les adresses IP, les noms d’utilisateur ou d’ordinateur, les adresses physiques ni les adresses e-mail aux niveaux De base et Étendu. Toute collecte de ces informations au niveau Complet n’est pas intentionnelle : elles peuvent être incluses dans des informations de diagnostic avancées comme des fichiers journaux ou des instantanés de la mémoire. Microsoft n’utilisera pas ces informations pour vous identifier ou vous contacter, ni à des fins publicitaires.

##  <a name="bkmk_change"></a> Modification du niveau
 Les administrateurs qui disposent d’une étendue administrative basée sur des rôles incluant les autorisations **Modification** sur la classe d’objets **Site** peuvent modifier le niveau des données collectées dans les paramètres des données de diagnostic et d’utilisation de la console Configuration Manager.

   Pour cela, dans la console, accédez à l’onglet Backstage (onglet supérieur gauche avec flèche déroulante), sélectionnez **Données d’utilisation**, puis le niveau de données à utiliser.  

##  <a name="bkmk_level1"></a> Niveau 1 - De base
 Le niveau De base comprend les données relatives à votre hiérarchie, qui sont nécessaires pour aider à améliorer votre expérience d’installation ou de mise à niveau, ainsi que des données pour aider à identifier les mises à jour Configuration Manager qui s’appliquent à votre hiérarchie.

 À compter de System Center Configuration Manager version 1606, ce niveau inclut les éléments suivants :


 -   Informations d’installation :
      - Build, type d’installation, modules linguistiques, fonctionnalités que vous avez activées  

      -   État et erreurs du déploiement du package de mise à jour, progression du téléchargement, et erreurs liées aux prérequis  

      -  Version du script après mise à niveau

      -  Utilisation de l’anneau rapide de mise à jour

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

-  Niveau de télémétrie configuré, mode (en ligne ou hors connexion) et configuration de la mise à jour rapide

-  Utilisation de la découverte du réseau (activée ou désactivée)
-  Console d'administration :

     -  Statistiques sur les connexions de la console (version, langue, SKU et architecture du système d’exploitation, mémoire système, nombre de processeurs logiques, ID du site de connexion, versions .NET installées et modules linguistiques de la console)    


- ***[Nouveau]*** Version SQL, niveau de Service Pack, édition, ID de classement, jeu de caractères


##  <a name="bkmk_level2"></a> Niveau 2 – Étendu
Le niveau Étendu est configuré par défaut après l’installation. Ce niveau comprend les données collectées au niveau De base, ainsi que les données propres aux fonctionnalités (fréquence et durée d’utilisation), les paramètres du client Configuration Manager (nom du composant, état et paramètres tels que les intervalles d’interrogation) et les informations de base sur les mises à jour logicielles.

Ce niveau est recommandé, car il fournit à Microsoft les données minimales nécessaires pour apporter des améliorations utiles dans les futures versions des produits et services. Ce niveau ne collecte pas les noms des objets (sites, utilisateurs, ordinateur ou objets), les informations sur les objets relatifs à la sécurité ni les vulnérabilités telles que le nombre de systèmes qui nécessitent des mises à jour logicielles.

À compter de System Center Configuration Manager version 1606, ce niveau inclut les éléments suivants :

-   **Gestion des applications :**  

    -    Informations de base d’utilisation/de ciblage pour les types de déploiement utilisés au sein de l’organisation (ciblé utilisateur ou appareil, nécessaire ou disponible, et applications universelles)  

    -   Informations sur le déploiement d’application (installation/désinstallation, approbation requise, interaction utilisateur activée/désactivée, dépendance et remplacement)  

    -   Statistiques de demande d’application disponibles  

    -   Nombre de packages par type  

    -   Nombre d’applicabilités de l’application par système d’exploitation  

    -   Nombre de déploiements de package/programme  

    -   Nombre d’environnements App-V et propriétés de déploiement  

    -   Nombre de licences d’application Windows 10 concédées  

    -   Nombre minimal/maximal/moyen de déploiements d’applications par utilisateur/appareil par période

    -   Type et durée de fenêtre de maintenance  

    -  Statistiques de taille et de complexité des stratégies d’applications

    - ***[Nouveau]*** Nombre d’applications Windows Store pour Entreprises et statistiques de synchronisation (y compris un résumé des types d’applications)  

    - ***[Nouveau]*** Statistiques des groupes de limites (nombre de rapides, nombre de lents, nombre par groupe)

    - ***[Nouveau]*** Options de configuration MSI et nombres

    - ***[Nouveau]*** Conditions requises pour les applications (nombre de conditions intégrées référencé par la technologie de déploiement)

    - ***[Nouveau]*** Remplacement des applications, profondeur de chaîne maximale

    - ***[Nouveau]*** Utilisation et mode de création d’Universal Data Access (UDA)



-   **Client :**  

    -   Liste/nombre d’agents clients activés  

    -   Nombre d’installations de client à partir de chaque type d’emplacement source  

    -   Nombre d’échecs d’installation de client  

    -  ***[Nouveau]*** Configuration du déploiement de mise à niveau automatique du client, notamment pilotage du client

    -  ***[Nouveau]*** Statistiques d’intégrité du client et récapitulatif des problèmes principaux

    - ***[Nouveau]*** Âge du BIOS en années

    - ***[Nouveau]*** Âge du système d’exploitation en mois

    - ***[Nouveau]*** Nombre d’actions du Centre logiciel

    - ***[Nouveau]*** Version du client AMT (Active Management Technology)

    - ***[Nouveau]*** Erreurs de téléchargement de déploiement client

    - ***[Nouveau]*** État des actions de notification du client (nombre d’exécutions de chaque action, nombre maximal de clients ciblés et taux de réussite moyen)

    - ***[Nouveau]*** Méthodes de déploiement utilisées pour le client et nombre de clients par méthode de déploiement

    - ***[Nouveau]*** Configuration de la taille du cache du client



- ***[Nouveau]*** **Services cloud :**

  - ***[Nouveau]*** Nombre de regroupements qui sont synchronisés avec Operations Management Suite

  - ***[Nouveau]*** Indication de l’activation du connecteur cloud Operations Management Suite



- ***[Nouveau] Regroupements :***

    -  ***[Déplacé]*** Statistiques d’évaluation des regroupements (temps de requête, nombre de regroupements attribués et non attribués, nombres par type, substitution d’ID et utilisation des règles)

    - ***[Nouveau]*** Regroupements sans déploiement

    - ***[Nouveau]*** Utilisation des ID de regroupement (ne pas manquer d’ID)



-   **Paramètres de compatibilité :**  

    -   Nombre d’éléments de configuration par type  

    -   Informations de la ligne de base de configuration de base (nombre, nombre de déploiements et nombre de références)  

    -   ***[Mis à jour]*** Nombre de déploiements faisant référence à des paramètres intégrés (avec capture du paramètre de correction)  

    -   ***[Mis à jour]*** Nombre de règles et de déploiements créés pour les paramètres personnalisés (avec capture du paramètre de correction)  
    -   Nombre de modèles SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, de certificat (.pfx) et de stratégie de conformité déployés

    -  Nombre de déploiements de certificat SCEP, VPN, Wi-Fi, certificat (.pfx) et stratégie de conformité par plateforme

    - ***[Nouveau]*** Stratégie Passport for Work (créée, déployée)



-   **Contenu :**  

    -   Nombre de limites par type  

    -   Informations sur les groupes de limites (nombre de limites et de systèmes de site qui sont attribués à chaque groupe de limites)  

    -   Informations sur les groupes de points de distribution (nombre de packages et de points de distribution qui sont attribués à chaque groupe de points de distribution)  

    -   Informations sur la configuration des points de distribution (utilisation de BranchCache et surveillance des points de distribution)  

    -   Informations sur la configuration du gestionnaire de distribution (threads, délai de nouvelle tentative, nombre de nouvelles tentatives et paramètres de point de distribution d’extraction)  


-   **Endpoint Protection :**  

    -   Utilisation des stratégies du Pare-feu Windows et de logiciel anti-programme malveillant Endpoint Protection (nombre de stratégies uniques attribuées au groupe)<br /><br /> Cela ne comprend pas les informations sur les paramètres inclus dans la stratégie.  

    -   Erreurs de déploiement Endpoint Protection (nombre de codes d’erreur de déploiement de stratégie Endpoint Protection)  

    -   Nombre de regroupements sélectionnés pour être affichés dans le tableau de bord Endpoint Protection  

    -   Nombre d’alertes configurées pour la fonctionnalité Endpoint Protection  

    - ***[Nouveau]*** Nombre de stratégies Advanced Threat Protection (ATP) et indication de déploiement des stratégies


-   ***[Supprimé]*** **Gestion des applications mobiles (MAM) :**  

    -   ***[Supprimé]*** Nombre d’applications métier, d’applications Office compatibles MAM et de stratégies par système d’exploitation  

    -   ***[Supprimé]*** Nombre de déploiements de stratégie/application MAM  

    -   ***[Supprimé]*** Nombre de règles créées par paramètre MAM  


- ***[Nouveau]*** **Migration :**

  -  ***[Nouveau]*** Nombre d’objets migrés (utilisation de l’Assistant migration)



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

    -   ***[Nouveau]*** Nombre d’utilisations des étapes de séquence de tâches



-   **Mises à jour du site :**

    - Versions des correctifs logiciels de Configuration Manager installés




-   **Mises à jour logicielles :**  

    -   Nombre total/moyen de regroupements comportant des déploiements de mises à jour logicielles et nombre maximal/moyen de mises à jour déployées  

    -   Nombre de règles de déploiement automatique qui sont liées à la synchronisation  

    -   Nombre de règles de déploiement automatique qui créent de nouvelles mises à jour ou ajoutent des mises à jour à un groupe existant  

    -   Différentiels de disponibilité et d’échéance qui sont utilisés dans les règles de déploiement automatique  

    -   Nombre moyen et maximal d’attributions par mise à jour  

    -   Nombre de mises à jour créées et déployées avec System Center Update Publisher  

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

    -   Classifications qui sont synchronisées par le point de mise à jour logicielle

    -   ***[Nouveau]*** Statistiques d’équilibrage de charge du point de mise à jour logicielle



-   **Données de performances/SQL :**  

    -   Nombre des plus grandes tables de base de données  

    -   Informations sur les réplicas SQL Always-On  

    -  Période de rétention du suivi des modifications SQL

    - ***[Nouveau]*** Types de découverte, activés et planifiés (complète, incrémentielle)

    - ***[Nouveau]*** Statistiques opérationnelles de découverte (nombre d’objets trouvés)

    - ***[Nouveau]*** Problèmes de performances du suivi des modifications SQL, période de rétention et état de nettoyage automatique



- ***[Nouveau]*** **Divers**

    - ***[Nouveau]*** Nombre de sites avec Wake On Lan (WOL)



##  <a name="bkmk_level3"></a> Niveau 3 – Complet
Le niveau Complet inclut toutes les données des niveaux De base et Étendu. Il inclut également des informations supplémentaires sur Endpoint Protection, les pourcentages de compatibilité des mises à jour et les informations de mise à jour logicielle. Ce niveau peut également inclure des informations de diagnostic avancées telles que des fichiers système et des instantanés de la mémoire, qui peuvent inclure des informations personnelles qui existaient dans la mémoire ou les fichiers journaux au moment de la capture.

À compter de System Center Configuration Manager version 1606, ce niveau inclut les éléments suivants :

-   Statistiques d’évaluation et d’actualisation des regroupements

-   Récapitulatif de l’intégrité Endpoint Protection (y compris le nombre de clients protégés, présentant un risque, inconnus et non pris en charge)

-   Configuration de la stratégie Endpoint Protection

-   Informations de déploiement de mise à jour logicielle (pourcentage de déploiements ciblés avec le client ou l’heure UTC, suppression du démarrage nécessaire, facultative ou en mode silencieux)

-   Compatibilité globale des déploiements de mise à jour logicielle

-   Informations sur le calendrier d’évaluation de règle de déploiement automatique

-   ***[SUPPRIMÉ]*** Nombre de clients avec des stratégies de protection d’accès réseau

-   Nombres et codes d’erreur de déploiement de mise à jour logicielle

-   Nombre minimal/maximal/moyen de clients inactifs dans les regroupements de déploiements de mise à jour logicielle

-   Nombre de groupes avec des mises à jour logicielles expirées

-   Nombre minimal/maximal/moyen de mises à jour logicielles par package

-   Pourcentages de réussite d’analyse des mises à jour logicielles

-   Nombre minimal/maximal/moyen d’heures depuis la dernière analyse des mises à jour logicielles

-    Produits des mises à jour logicielles synchronisés par le point de mise à jour logicielle
-    Paramètres de conformité : détails de configuration des modèles SCEP, VPN, Wi-Fi et de stratégie de conformité

-    Type de stratégies d’accès conditionnel EAS (bloquer ou mettre en quarantaine) pour les appareils gérés par Intune

-   ***[Nouveau]*** 50 premières unités centrales dans l’environnement

-   ***[Nouveau]*** Pack de configuration DCM pour l’utilisation de System Center Configuration Manager

-   ***[Nouveau]*** Code de produit MSI (applications courantes que les clients déploient)

-   ***[Nouveau]*** Récapitulatif d’intégrité ATP

-   ***[Nouveau]*** Détails des erreurs d’installation du déploiement du client
