---
title: Données de diagnostic pour 1610
titleSuffix: Configuration Manager
description: En savoir plus sur les niveaux des données de diagnostic et d’utilisation collectées par System Center Configuration Manager version 1610.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: eb20eb90-bcc0-41de-bfea-638ea470c0dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b29044858bb9a9d57db1c2229c826630d0905860
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416518"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1610-of-system-center-configuration-manager"></a>Niveaux de collecte des données de diagnostic et d’utilisation pour la version 1610 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager version 1610 collecte trois niveaux de données d’utilisation et de diagnostic : **De base**, **Étendu** et **Complet**. Par défaut, cette fonctionnalité est définie sur le niveau Étendu. Les sections suivantes fournissent des détails supplémentaires sur les données collectées par chaque niveau.

Les modifications par rapport aux versions précédentes sont indiquées par ***[Nouveau]***, ***[Mis à jour]***, ***[Supprimé]*** ou ***[Déplacé]***.


> [!IMPORTANT]
>  Configuration Manager ne collecte pas les codes des sites, les noms des sites, les adresses IP, les noms d’utilisateur ou d’ordinateur, les adresses physiques ni les adresses e-mail aux niveaux De base et Étendu. Toute collecte de ces informations au niveau Complet n’est pas intentionnelle : elles peuvent être incluses dans des informations de diagnostic avancées comme des fichiers journaux ou des instantanés de la mémoire. Microsoft n’utilisera pas ces informations pour vous identifier ou vous contacter, ni à des fins publicitaires.

##  <a name="bkmk_change"></a> Modification du niveau
 Les administrateurs qui ont une étendue d’administration basée sur des rôles incluant les autorisations **Modifier** sur la classe d’objets **Site** peuvent changer le niveau des données collectées dans les paramètres des données de diagnostic et d’utilisation de la console Configuration Manager.

Depuis la version 1610, vous pouvez changer le niveau de collecte des données à partir de la console en accédant à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Sites**. Ouvrez **Paramètres de hiérarchie**, puis sélectionnez le niveau de données que vous voulez utiliser.  

##  <a name="bkmk_level1"></a> Niveau 1 - De base
 Le niveau De base comprend les données relatives à votre hiérarchie, qui sont nécessaires pour améliorer votre expérience d’installation ou de mise à niveau, ainsi que des données pour identifier les mises à jour Configuration Manager qui s’appliquent à votre hiérarchie.

 Pour System Center Configuration Manager version 1610, ce niveau inclut les éléments suivants :


- Informations d’installation :
    - Build, type d’installation, modules linguistiques, fonctionnalités que vous avez activées  

    - État et erreurs du déploiement du package de mise à jour, progression du téléchargement, et erreurs liées aux prérequis    

    - Version du script après mise à niveau

    - Utilisation de l’anneau rapide de mise à jour

  - ***[Nouveau]*** Utilisation en préversion, type de support de configuration, type de branche

  - ***[Nouveau]*** Date d’expiration de Software Assurance

- Métriques de performances de base de données (informations sur le traitement de la réplication, procédures stockées SQL Server les plus utilisées par processeur et utilisation des disques)

- Configuration de base de données simple (processeurs, configuration du cluster et configuration des vues distribuées)

- Schéma de base de données Configuration Manager (hachage de toutes les définitions d’objet)

- Nombre de versions du client Configuration Manager et de versions du système d’exploitation

- Nombre de systèmes d’exploitation des appareils gérés et stratégies définies par le connecteur Exchange

- Nombre de paramètres régionaux et de langues du client

- Nombre d’appareils Windows 10 par branche et build

- Données de la hiérarchie des sites Configuration Manager de base (liste des sites, type, version, état, nombre de clients et fuseau horaire)

- Informations de serveur de système de site de base (rôles de système de site utilisés, état SSL et Internet, système d’exploitation, processeurs, ordinateur physique ou machine virtuelle)

- Statistiques de découverte d’utilisateurs de base (nombre de découvertes d’utilisateurs et tailles minimale/maximale/moyenne des groupes)

- Informations Endpoint Protection de base (versions du client de logiciel anti-programme malveillant)

- Nombres de types d’application et de déploiement de base (nombre total d’applications, nombre total d’applications avec plusieurs types de déploiement, nombre total d’applications avec des dépendances, nombre total d’applications remplacées, nombre de technologies de déploiement utilisées)

- Nombre de déploiements de systèmes d’exploitation de base (images)

- Types de point de distribution et de point de gestion, et informations de configuration de base (protégés, préparés, PXE, de multidiffusion, d’état SSL, points de distribution pairs/d’extraction, compatibles MDM, compatibles SSL, etc.)

- Statistiques de télémétrie (à l’exécution, runtime, erreurs)

- Niveau de télémétrie configuré, mode (en ligne ou hors connexion) et configuration de la mise à jour rapide

- Utilisation de la découverte du réseau (activée ou désactivée)
- Console d'administration :

     - Statistiques sur les connexions de la console (version, langue, référence (SKU) et architecture du système d’exploitation, mémoire système, nombre de processeurs logiques, ID du site de connexion, versions .NET installées et modules linguistiques de la console)    

- Version SQL, niveau de Service Pack, édition, ID de classement et jeu de caractères


##  <a name="bkmk_level2"></a> Niveau 2 – Étendu
Le niveau Étendu est configuré par défaut après l’installation. Ce niveau comprend les données collectées au niveau De base, ainsi que les données spécifiques aux fonctionnalités (fréquence et durée d’utilisation), les paramètres du client Configuration Manager (nom du composant, état et paramètres, comme les intervalles d’interrogation) et les informations de base sur les mises à jour logicielles.

Ce niveau est recommandé, car il fournit à Microsoft les données minimales nécessaires pour apporter des améliorations utiles dans les futures versions des produits et services. Ce niveau ne collecte pas les noms des objets (sites, utilisateurs, ordinateur ou objets), les informations sur les objets relatifs à la sécurité ni les vulnérabilités, comme le nombre de systèmes qui nécessitent des mises à jour logicielles.

Pour System Center Configuration Manager version 1610, ce niveau inclut les éléments suivants :

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

    - ***[Mis à jour]*** Nombre d’applications Windows Store pour Entreprises et statistiques de synchronisation (notamment un résumé des types d’applications, l’état des applications sous licence ainsi que le nombre d’applications sous licence en ligne et hors connexion)  

    - Statistiques des groupes de limites (nombre de rapides, nombre de lents, nombre par groupe)

    - Options de configuration MSI et nombres

    - Exigences pour les applications (le nombre de conditions prédéfinies est référencé par la technologie de déploiement)

    - Remplacement des applications, profondeur de chaîne maximale

    - Utilisation et mode de création d’Universal Data Access (UDA)

    - ***[Nouveau]*** Statistiques d’approbation de l’application et fréquence d’utilisation



-   **Client :**  

    -   Liste/nombre d’agents clients activés  

    -   Nombre d’installations de client à partir de chaque type d’emplacement source  

    -   Nombre d’échecs d’installation de client  

    -  ***[Mis à jour]*** Mise à niveau automatique du client : configuration du déploiement, notamment le test du client et l’utilisation de l’exclusion (client d’interopérabilité étendue)

    -  Statistiques d’intégrité du client et récapitulatif des problèmes principaux

    - Âge du BIOS en années

    - Ancienneté du système d’exploitation en mois

    - Nombre d’actions du Centre logiciel

    - Version du client AMT (Active Management Technology)

    - Erreurs de téléchargement de déploiement des clients

    - État des actions de notification du client (nombre d’exécutions de chaque action, nombre maximal de clients ciblés et taux de réussite moyen)

    - Méthodes de déploiement utilisées pour le client et nombre de clients par méthode de déploiement

    - Configuration de la taille du cache du client

    - ***[Nouveau]*** Nombre de classes d’inventaire matériel, règles d’inventaire logiciel et règles de regroupement de fichiers




- **Services cloud :**

  - Nombre de regroupements qui sont synchronisés avec Operations Management Suite

  -  Activation ou non du connecteur cloud Operations Management Suite

  - ***[Nouveau]*** Configuration et statistiques d’utilisation de la passerelle de gestion cloud

  - ***[Nouveau]*** Nombre de connecteurs Upgrade Analytics




- **Regroupements :**

    -  Statistiques d’évaluation des regroupements (durée des requêtes, nombre de regroupements affectés et non affectés, nombres par type, substitution d’ID et utilisation des règles)

    - Regroupements sans déploiement

    - Utilisation des ID de regroupement (ne pas manquer d’ID)



-   **Paramètres de compatibilité :**  

    -   Nombre d’éléments de configuration par type  

    -   Informations de la ligne de base de configuration de base (nombre, nombre de déploiements et nombre de références)  

    -   Nombre de déploiements qui référencent des paramètres prédéfinis (avec capture du paramètre de correction)  

    -   Nombre de règles et de déploiements créés pour les paramètres personnalisés (avec capture du paramètre de correction)  
    -   Nombre de modèles SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, de certificat (.pfx) et de stratégie de conformité déployés

    -  Nombre de déploiements de certificat SCEP, VPN, Wi-Fi, certificat (.pfx) et stratégie de conformité par plateforme

    - Stratégie Passport for Work (créée, déployée)



-   **Contenu :**  

    -   Nombre de limites par type  

    -   Informations sur les groupes de limites (nombre de limites et de systèmes de site qui sont affectés à chaque groupe de limites)  

    - ***[Nouveau]*** Relations de groupes de limites et configuration de secours

    -   Informations sur les groupes de points de distribution (nombre de packages et de points de distribution qui sont affectés à chaque groupe de points de distribution)  

    -   Informations sur la configuration des points de distribution (utilisation de BranchCache et surveillance des points de distribution)  

    -   Informations sur la configuration du gestionnaire de distribution (threads, délai de nouvelle tentative, nombre de nouvelles tentatives et paramètres de point de distribution d’extraction)  

    - ***[Nouveau]*** Nombre de clients du cache de pairs et statistiques d’utilisation

    - ***[Nouveau]*** Statistiques de téléchargement du contenu client


-   **Endpoint Protection :**  

    -   Utilisation des stratégies du Pare-feu Windows et de logiciel anti-programme malveillant Endpoint Protection (nombre de stratégies uniques affectées au groupe)<br /><br /> Ceci ne comprend pas d’informations sur les paramètres inclus dans la stratégie.  

    -   Erreurs de déploiement Endpoint protection (nombre de codes d’erreur de déploiement de stratégie Endpoint Protection)  

    -   Nombre de regroupements sélectionnés pour être affichés dans le tableau de bord Endpoint Protection  

    -   Nombre d’alertes configurées pour la fonctionnalité Endpoint Protection  

    -   Nombre de stratégies ATP (Advanced Threat Protection) (nombre de stratégies et si elles sont ou non déployées)


- **Migration :**

  -   Nombre d’objets migrés (utilisation de l’Assistant Migration)



-   **Gestion des appareils mobiles (MDM) :**  

    -   ***[Mis à jour]*** Nombre d’actions d’appareil mobile émises : commandes de verrouillage, de réinitialisation, de mise hors service et Synchroniser maintenant  

    -   Nombre d’appareils mobiles gérés par Configuration Manager et Microsoft Intune, et méthode d’inscription (en bloc ou basée sur l’utilisateur)  

    -   Statistiques et calendrier d’interrogation des appareils mobiles pour la durée d’inscription des appareils mobiles  

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

    -   Nombre d’utilisations des étapes de séquence de tâches

    - ***[Nouveau]*** Nombre de stratégies de mise à niveau d’édition



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

    -   Statistiques d’équilibrage de charge du point de mise à jour logicielle

    -  ***[Nouveau]*** Configuration des mises à jour rapides de Windows 10




-   **Données de performances/SQL :**  

    -   Nombre des plus grandes tables de base de données  

    -   ***[Mis à jour]*** Informations sur les réplicas SQL AlwaysOn, utilisation et état d’intégrité

    -  Période de rétention du suivi des modifications SQL

    - Types de découverte, activés et planifiés (complète, incrémentielle)

    - Statistiques opérationnelles de découverte (nombre d’objets trouvés)

    - Problèmes de performances du suivi des modifications SQL, période de rétention et état de nettoyage automatique



- **Divers**

    - Nombre de sites avec Wake On Lan (WOL)

    - ***[Nouveau]*** Statistiques de performances et d’utilisation des rapports  



##  <a name="bkmk_level3"></a> Niveau 3 – Complet
Le niveau Complet inclut toutes les données des niveaux De base et Étendu. Il inclut également des informations supplémentaires sur Endpoint Protection, les pourcentages de compatibilité des mises à jour et les informations de mise à jour logicielle.  Ce niveau peut également inclure des informations de diagnostic avancées telles que des fichiers système et des instantanés de la mémoire, qui peuvent inclure des informations personnelles qui existaient dans la mémoire ou les fichiers journaux au moment de la capture.

Pour System Center Configuration Manager version 1610, ce niveau inclut les éléments suivants :

-   Statistiques d’évaluation et d’actualisation des regroupements

-   Récapitulatif de l’intégrité Endpoint Protection (y compris le nombre de clients protégés, présentant un risque, inconnus et non pris en charge)

-   Configuration de la stratégie Endpoint Protection

-   Informations de déploiement de mise à jour logicielle (pourcentage de déploiements ciblés avec le client ou l’heure UTC, obligatoire/facultatif/en mode silencieux, et suppression du redémarrage)

-   Compatibilité globale des déploiements de mise à jour logicielle

-   Informations sur le calendrier d’évaluation de règle de déploiement automatique

-   Nombres et codes d’erreur de déploiement de mise à jour logicielle

-   Nombre minimal/maximal/moyen de clients inactifs dans les regroupements de déploiements de mise à jour logicielle

-   Nombre de groupes avec des mises à jour logicielles expirées

-   Nombre minimal/maximal/moyen de mises à jour logicielles par package

-   Pourcentages de réussite d’analyse des mises à jour logicielles

-   Nombre minimal/maximal/moyen d’heures depuis la dernière analyse des mises à jour logicielles

-    Produits des mises à jour logicielles synchronisés par le point de mise à jour logicielle
-    Paramètres de conformité : détails de configuration des modèles SCEP, VPN, Wi-Fi et de stratégie de conformité

-    Type de stratégies d’accès conditionnel EAS (bloquer ou mettre en quarantaine) pour les appareils gérés par Intune

-   50 premières unités centrales dans l’environnement

-   Pack de configuration DCM pour l’utilisation de System Center Configuration Manager

-   Code de produit MSI (applications courantes que les clients déploient)

-   Récapitulatif d’intégrité ATP

-   Détails des erreurs d’installation du déploiement des clients

- ***[Nouveau]*** Détails des applications du Windows Store pour Entreprises (liste de non-agrégation des applications synchronisées, notamment l’ID de l’application, l’état (en ligne ou hors connexion) et le nombre total de licences achetées)
