---
title: Données de diagnostic et d’utilisation pour la version 1810
titleSuffix: Configuration Manager
description: Découvrez les niveaux de données de diagnostic et d’utilisation collectés dans la version 1810.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bce9e299-7b3a-4f51-8863-a322877daa2c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6dd50d137cdc570b7e37cd96fb310c85ba60840
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458072"
---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1810"></a>Niveaux de collecte des données de diagnostic et d’utilisation pour la version 1810

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager version 1810 collecte trois niveaux de données de diagnostic et d’utilisation : **De base**, **Étendu** et **Complet**. Par défaut, cette fonctionnalité est définie sur le niveau Étendu. Les sections suivantes fournissent des détails supplémentaires sur les données collectées à chaque niveau.

Les modifications par rapport aux versions précédentes sont indiquées par ***[Nouveau]***, ***[Mis à jour]***, ***[Supprimé]*** ou ***[Déplacé]***.


> [!IMPORTANT]
>  Configuration Manager ne collecte pas les codes des sites, les noms des sites, les adresses IP, les noms d’utilisateur ou d’ordinateur, les adresses physiques ou les adresses e-mail aux niveaux De base et Étendu. Toute collecte de ces informations au niveau Complet n’est pas intentionnelle. Elles peuvent être incluses dans des informations de diagnostic avancées comme des fichiers journaux ou des instantanés de mémoire. Microsoft n’utilise pas ces informations pour vous identifier ou vous contacter, ni à des fins publicitaires.



##  <a name="bkmk_change"></a> Modification du niveau

Pour changer le niveau de collecte de données, vous devez **modifier** les autorisations sur la classe d’objets **Site**. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez **Paramètres de hiérarchie** dans le ruban, puis choisissez le niveau de données dans les paramètres Données d’utilisation et de diagnostics.  



##  <a name="bkmk_level1"></a> Niveau 1 - De base
Le niveau De base inclut les données relatives à votre hiérarchie. Il est nécessaire pour améliorer votre expérience quand vous effectuez une installation ou une mise à niveau. Ces données permettent également de déterminer les mises à jour de Configuration Manager qui s’appliquent à votre hiérarchie.

Pour Configuration Manager version 1810, ce niveau comprend les données suivantes :

- Statistiques sur les connexions de la console Configuration Manager : version du système d’exploitation, langue, référence (SKU) et architecture, mémoire système, nombre de processeurs logiques, ID du site de connexion, versions .NET installées et modules linguistiques de la console

- Nombres de types d’application et de déploiement de base : nombre total d’applications, nombre total d’applications avec plusieurs types de déploiement, nombre total d’applications avec des dépendances, nombre total d’applications remplacées, nombre de technologies de déploiement en cours d’utilisation

- Données de la hiérarchie des sites Configuration Manager de base : liste des sites, type, version, état, nombre de clients et fuseau horaire

- ***[Mise à jour]*** Configuration de base de données de base : processeurs, taille de mémoire, paramètres de mémoire, configuration de la base de données Configuration Manager, taille de la base de données Configuration Manager, configuration du cluster et configuration des vues distribuées et version du suivi des modifications  

- Statistiques de découverte de base : nombre de découvertes, tailles de groupe minimale/maximale/moyenne) et moment où le site est entièrement exécuté avec les services Active Directory Azure

- Informations Endpoint Protection de base sur les versions du client de logiciel anti-programme malveillant

- Nombres d’images de déploiements de système d’exploitation de base

- Informations de serveur de système de site de base : rôles de système de site utilisés, état SSL et Internet, système d’exploitation, processeurs, ordinateur physique ou machine virtuelle, et utilisation de la haute disponibilité du serveur de site

- Schéma de base de données Configuration Manager (hachage de toutes les définitions d’objet)

- Niveau configuré pour les données de diagnostic et d’utilisation, mode en ligne ou hors connexion et configuration de mise à jour rapide

- Nombre de paramètres régionaux et de langues du client

- Nombre de versions du client Configuration Manager, de versions du système d’exploitation et de versions d’Office

- Nombre de systèmes d’exploitation des appareils gérés et stratégies définies par le connecteur Exchange

- ***[Mise à jour]*** Nombre d’appareils Windows 10 par branche, build et forêt Active Directory unique  

- Nombre de clients Windows 10 qui utilisent Windows Update for Business  

- Métriques de performances de base de données : informations sur le traitement de la réplication, procédures stockées SQL Server les plus utilisées par processeur et utilisation des disques

- Types de point de distribution et de point de gestion, et informations de configuration de base : protégés, préparés, PXE, multidiffusion, état SSL, points de distribution d’extraction/entre homologues, compatibles avec la gestion locale des appareils mobiles (MDM) et compatibles SSL

- Liste hachée d’extensions des Assistants et pages de propriétés de console Administrateur

- Informations d’installation :  

    - Build, type d’installation, modules linguistiques, fonctionnalités que vous avez activées   

    - Utilisation en préversion, type de support de configuration, type de branche  

    - Date d’expiration de Software Assurance  

    - État et erreurs du déploiement du package de mise à jour, progression du téléchargement, et erreurs liées aux prérequis  

    - Utilisation de l’anneau rapide de mise à jour  

    - Version du script après mise à niveau  

- Version SQL, niveau de Service Pack, édition, ID de classement et jeu de caractères  

- Statistiques des données de diagnostic et d’utilisation : à l’exécution, runtime, erreurs  

- Information indiquant si la découverte du réseau est activée ou désactivée  

- Nombre de clients ayant rejoint Azure Active Directory  

- Nombre de déploiements par phases créés par type  

- Nombre de clients d’interopérabilité étendue  

- Liste à laquelle a été appliqué un code de hachage pour les propriétés d’inventaire matériel dépassant 255 caractères  

- Nombre de clients par méthode d’inscription à la cogestion  

- Statistiques d’erreurs pour l’inscription à la cogestion  

- Nombre de clients par ancienneté du système d’exploitation Windows, à l’intervalle de trois mois le plus proche  

- ***[Mise à jour]*** Top 10 des noms de processeurs utilisés sur les clients et les serveurs  

- Nombre et taux de traitement des objets Configuration Manager clés : DDR (enregistrements de données de découverte), messages d’état, messages de statut, inventaire matériel, inventaire logiciel et nombre total de fichiers dans les boîtes de réception  

- Informations sur les performances des disques et des processeurs du serveur de site  

- Informations sur la durée de fonctionnement et sur l’utilisation de la mémoire pour les processus du serveur de site Configuration Manager  

- Nombre de plantages des processus du serveur de site Configuration Manager, avec l’ID de signature Watson, le cas échéant  

- ***[Nouveauté]*** Liste hachée du top des requêtes SQL par utilisation de la mémoire et nombre de verrous  

- ***[Déplacement, mise à jour]*** Statistiques agrégées d’utilisation de la cogestion : nombre de clients inscrits jusqu’à ce jour, nombre de clients inscrits, nombre de clients dont l’inscription est en attente, clients recevant la stratégie, états de la charge de travail, tailles des regroupements de pilotes/d’exclusions et erreurs d’inscription  



##  <a name="bkmk_level2"></a> Niveau 2 – Étendu

Le niveau Étendu est configuré par défaut après l’installation. Ce niveau comprend les données collectées au niveau De base et les données spécifiques aux fonctionnalités. Il indique la fréquence et durée d’utilisation de différentes fonctionnalités. Il inclut également des données sur les paramètres du client Configuration Manager : nom du composant, état et certains paramètres comme les intervalles d’interrogation. Des informations de base sont fournies sur l’utilisation des mises à jour logicielles, mais aucune donnée n’est fournie concernant leur conformité.

Microsoft recommande ce niveau, car il fournit le minimum de données nécessaires pour améliorer les produits et les services. Ce niveau ne collecte pas les noms d’objets (sites, utilisateurs, ordinateurs ou objets), les détails des objets liés à la sécurité, ni les vulnérabilités telles que le nombre de systèmes qui nécessitent des mises à jour logicielles.

Pour Configuration Manager version 1810, ce niveau comprend les données suivantes :

### <a name="application-management"></a>Gestion des applications  

- Exigences pour les applications : nombre de conditions prédéfinies référencé par la technologie de déploiement  

- Remplacement des applications, profondeur de chaîne maximale  

- Statistiques d’approbation de l’application et fréquence d’utilisation  

- Statistiques sur les tailles de contenu d’application  

- Informations de déploiement d’application : utilisation de l’installation par rapport à la désinstallation, approbation exigée, interaction utilisateur activée/désactivée, dépendance, remplacement et nombre d’utilisations de la fonctionnalité de comportement à l’installation  

- Statistiques de taille et de complexité des stratégies d’applications  

- Statistiques de demande d’application disponibles  

- Informations de configuration de base pour les packages et les programmes : options de déploiement et indicateurs de programme  

- Informations de base d’utilisation/de ciblage pour les types de déploiement : ciblé utilisateur ou appareil, nécessaire ou disponible, et applications universelles  

- Nombre d’environnements App-V et propriétés de déploiement  

- Nombre d’applicabilités de l’application par système d’exploitation  

- Nombre d’applications référencées dans une séquence de tâches  

- Nombre de personnalisations distinctes pour le catalogue d’applications  

- Nombre d’applications Office 365 créées à l’aide du tableau de bord  

- Nombre de packages par type  

- Nombre de déploiements de package/programme  

- Nombre de licences d’application Windows 10 concédées  

- Nombre de types de déploiement Windows Installer par paramètres du contenu de désinstallation  

- Nombre d’applications de Microsoft Store pour Entreprises et statistiques de synchronisation : résumé des types d’applications, état des applications sous licence et nombre d’applications sous licence en ligne et hors connexion  

- Type et durée de fenêtre de maintenance  

- Nombre minimal/maximal/moyen de déploiements d’applications par utilisateur/appareil par période  

- Codes d’erreur d’installation d’application les plus courants par technologie de déploiement  

- Options de configuration MSI et nombres  

- Statistiques sur l’interaction de l’utilisateur final avec notification des déploiements de logiciels requis  

- Utilisation et mode de création d’Universal Data Access (UDA)  

- Statistiques agrégées d’affinité entre utilisateur et appareil  

- Nombre maximal et nombre moyen d’utilisateurs principaux par appareil  

- Utilisation de condition globale d’application par type  

- Configuration de la personnalisation du Centre logiciel  

- Disponibilité et statistiques de Package Conversion Manager  

- Nombre de méthodes de détection d’application par type  

- Nombre d’erreurs de mise en conformité d’application  

- Propriétés du programme d’installation MSI  

- Statistiques des demandes d’installation utilisateur  

- ***[Nouveauté]*** Statistiques agrégées sur l’utilisation de la fonctionnalité d’approbation par e-mail  

- ***[Nouveauté]*** Nombre de fichiers, taille du contenu, nombre de services et nombre d’actions personnalisées des MSI dans le catalogue d’applications  


### <a name="client"></a>Client  

- Version du client AMT (Active Management Technology)  

- Âge du BIOS en années  

- Nombre d’appareils avec démarrage sécurisé  

- Nombre d’appareils par état TPM  

- Mise à niveau automatique du client : configuration du déploiement, notamment le test du client et l’utilisation de l’exclusion (client d’interopérabilité étendue)  

- Configuration de la taille du cache du client  

- Erreurs de téléchargement de déploiement des clients  

- Statistiques sur l’intégrité des clients et récapitulatif des principaux problèmes en fonction de la version du client  

- État des actions de notification du client : nombre d’exécutions de chaque action, nombre maximal de clients ciblés et taux de réussite moyen  

- Nombre d’installations de client à partir de chaque type d’emplacement source  

- Nombre d’échecs d’installation de client  

- Nombre d’appareils virtualisés par Hyper-V ou Azure  

- Nombre d’actions du Centre logiciel  

- Nombre d’appareils compatibles UEFI  

- Méthodes de déploiement utilisées pour le client et nombre de clients par méthode de déploiement  

- Liste/nombre d’agents clients activés  

- Âge du système d’exploitation en mois  

- Nombre de classes d’inventaire matériel, règles d’inventaire logiciel et règles de regroupement de fichiers  

- Statistiques pour l’attestation d’intégrité des appareils : codes d’erreur les plus courants, nombre de serveurs locaux et nombre d’appareils dans différents états  

- Nombre d’appareils par navigateur par défaut  

- Nombre de certificats d’authentification serveur générés par Configuration Manager  

- Nombre d’appareils Microsoft Surface par modèle  


### <a name="cloud-services"></a>Services cloud  

- Statistiques de découverte Azure Active Directory  

- Statistiques de configuration et d’utilisation de la passerelle de gestion cloud : nombre de régions et d’environnements, et statistiques d’authentification/autorisation  

- Nombre d’applications et services Azure Active Directory connectés à Configuration Manager  

- Nombre de regroupements synchronisés avec Azure Log Analytics  

- Nombre de connecteurs Upgrade Analytics  

- Indique si le connecteur cloud Azure Log Analytics est activé  

- Nombre de points de distribution d’extraction avec un point de distribution cloud comme emplacement source  


### <a name="cmpivot"></a>CMPivot

- Statistiques d’utilisation de CMPivot  

- ***[Nouveauté]*** Nombre de requêtes CMPivot enregistrées  

- ***[Nouveauté]*** Nombre de requêtes par type d’entité  


### <a name="co-management"></a>Cogestion  

- Planification de l’inscription et statistiques d’historique  

- Nombre de clients éligibles à la cogestion  

- Locataire Microsoft Intune associé  


### <a name="collections"></a>Regroupements  

- Utilisation des ID de regroupement (ne pas manquer d’ID)  

- Statistiques d’évaluation des regroupements : durée des requêtes, nombre de regroupements affectés et non affectés, nombres par type, substitution d’ID et utilisation des règles  

- Regroupements sans déploiement  


### <a name="compliance-settings"></a>Paramètres de conformité  

- Informations de la ligne de base de configuration de base : décompte, nombre de déploiements et nombre de références  

- Statistiques d’erreurs de stratégie de conformité  

- Nombre d’éléments de configuration par type  

- Nombre de déploiements qui référencent des paramètres prédéfinis, notamment le paramètre de correction  

- Nombre de règles et de déploiements créés pour des paramètres personnalisés, notamment le paramètre de correction  

- Nombre de modèles SCEP (Simple Certificate Enrollment Protocol), VPN, Wi-Fi, de certificat (.pfx) et de stratégie de conformité déployés  

- Nombre de déploiements de certificats SCEP, VPN, Wi-Fi, certificats (.pfx) et stratégies de conformité par plateforme  

- Stratégie Windows Hello Entreprise (créée, déployée)  

- Nombre de stratégies de navigateur Microsoft Edge déployées  


### <a name="content"></a>Content  

- Statistiques des groupes de limites : nombre de relations rapides, de relations lentes, de relations par groupe et de relations de repli  

- Informations sur les groupes de limites : nombre de limites et de systèmes de site qui sont attribués à chaque groupe de limites  

- Relations de groupes de limites et configuration de repli  

- Statistiques de téléchargement du contenu client  

- Nombre de limites par type  

- Nombre de clients de cache d’homologue, statistiques d’utilisation et statistiques de téléchargements partiels  

- Informations sur la configuration du gestionnaire de distribution : threads, délai de nouvelle tentative, nombre de nouvelles tentatives et paramètres de point de distribution d’extraction  

- Informations sur la configuration des points de distribution : utilisation de BranchCache et surveillance des points de distribution  

- Informations sur les groupes de points de distribution : nombre de packages et de points de distribution qui sont affectés à chaque groupe de points de distribution  

- Type de bibliothèque de contenu, local ou distant  

- ***[Nouveauté]*** Nombre de groupes de limites par configuration  


### <a name="endpoint-protection"></a>Endpoint Protection  

- Stratégies Windows Defender - Protection avancée contre les menaces (ATP) : nombre de stratégies et indication de déploiement des stratégies  

- Nombre d’alertes configurées pour la fonctionnalité Endpoint Protection  

- Nombre de regroupements sélectionnés pour être affichés dans le tableau de bord Endpoint Protection  

- Nombre de stratégies, de déploiements et de clients ciblés Windows Defender Exploit Guard  

- Erreurs de déploiement Endpoint Protection : nombre de codes d’erreur de déploiement de stratégie Endpoint Protection  

- Utilisation des stratégies du Pare-feu Windows et de logiciel anti-programme malveillant Endpoint Protection (nombre de stratégies uniques affectées au groupe). Ces données ne comprennent pas d’informations sur les paramètres inclus dans la stratégie.  


### <a name="migration"></a>Migration  

- Nombre d’objets migrés (utilisation de l’Assistant Migration)  


### <a name="mobile-device-management-mdm"></a>Gestion des appareils mobiles (MDM)  

- Nombre d’actions d’appareil mobile émises : commandes de verrouillage, de réinitialisation, de mise hors service et de synchronisation immédiate  

- Nombre de stratégies d’appareil mobile  

- Nombre d’appareils mobiles gérés par Configuration Manager et Microsoft Intune et méthode d’inscription (en bloc, basée sur l’utilisateur)  

- Nombre d’utilisateurs qui ont plusieurs appareils mobiles inscrits  

- Statistiques et calendrier d’interrogation des appareils mobiles pour la durée d’inscription des appareils mobiles  


### <a name="microsoft-intune-troubleshooting"></a>Dépannage de Microsoft Intune  

- Nombre et taille des actions d’appareil (réinitialisation, mise hors service, verrouillage), des données d’utilisation et des messages de données répliqués vers Microsoft Intune  

- Nombre et taille des messages d’état, de statut, d’inventaire, RDR, DDR, UDX, d’état de locataire, POL, LOG, de certificat, CRP, de resynchronisation, CFD, RDO, BEX, ISM et de conformité qui sont téléchargés à partir de Microsoft Intune  

- Statistiques de synchronisation utilisateur complète et différentielle pour Microsoft Intune  


### <a name="on-premises-mobile-device-management-mdm"></a>Gestion locale des appareils mobiles  

- Nombre de profils et de packages d’inscription en bloc Windows 10  

- Statistiques de réussite/échec de déploiement pour les déploiements d’applications de gestion MDM locale  


### <a name="os-deployment"></a>Déploiement de système d’exploitation  

- Nombre d’images de démarrage, de pilotes, de packages de pilotes, de points de distribution en multidiffusion, de points de distribution compatibles PXE et de séquences de tâches  

- Nombre d’images de démarrage par version cliente de Configuration Manager  

- Nombre d’images de démarrage par version de Windows PE  

- Nombre de stratégies de mise à niveau d’édition  

- Nombre d’identificateurs de matériel exclus de PXE  

- Nombre de déploiement du système d’exploitation par version de système d’exploitation  

- Nombre de mises à niveau du système d’exploitation au fil du temps  

- Nombre de déploiements de séquences de tâches utilisant l’option de prétéléchargement du contenu  

- Nombre d’utilisations des étapes de séquence de tâches  

- Version de Windows ADK installée  

- Nombre de tâches de maintenance d’images  

- ***[Nouveauté]*** Nombre d’ordinateurs importés  


### <a name="site-updates"></a>Mises à jour du site  

- Versions des correctifs logiciels de Configuration Manager installés  


### <a name="software-updates"></a>mises à jour logicielles  

- Différentiels de disponibilité et d’échéance qui sont utilisés dans les règles de déploiement automatique  

- Nombre moyen et maximal d’attributions par mise à jour  

- Calendriers d’analyse et d’évaluation des mises à jour client  

- Classifications synchronisées par le point de mise à jour logicielle  

- Statistiques d’application de correctifs logiciels au cluster  

- Configuration des mises à jour rapides de Windows 10  

- Configurations qui sont utilisées pour les plans de maintenance actifs de Windows 10  

- Nombre de mises à jour Office 365 déployées  

- Nombre de pilotes Microsoft Surface synchronisés  

- Nombre de groupes et d’attributions de mises à jour  

- Nombre de packages de mises à jour et nombre maximal/minimal/moyen de points de distribution qui sont ciblés par les packages  

- Nombre de mises à jour créées et déployées avec System Center Update Publisher  

- Nombre de stratégies Windows Update for Business créées et déployées  

- Statistiques agrégées des configurations Windows Update pour Entreprise  

- Nombre de règles de déploiement automatique qui sont liées à la synchronisation  

- Nombre de règles de déploiement automatique qui créent de nouvelles mises à jour ou ajoutent des mises à jour à un groupe existant  

- Nombre de règles de déploiement automatique avec plusieurs déploiements  

- Nombre de groupes de mises à jour et nombre minimal/maximal/moyen de mises à jour par groupe  

- Nombre de mises à jour et pourcentage de mises à jour qui sont déployées, expirées, remplacées, téléchargées et qui contiennent des CLUF  

- Statistiques d’équilibrage de charge du point de mise à jour logicielle  

- Planification de la synchronisation du point de mise à jour logicielle  

- Nombre total/moyen de regroupements comportant des déploiements de mises à jour logicielles et nombre maximal/moyen de mises à jour déployées  

- Codes d’erreur d’analyse des mises à jour et nombre d’ordinateurs  

- Versions de contenu du tableau de bord Windows 10  

- Nombre d’abonnements et utilisation des catalogues de mises à jour de logiciels tiers  

- Nombre de mises à jour logicielles déployées avec et sans contenu  

- ***[Nouveauté]*** Statistiques agrégées sur le nombre de mises à jour UUP obligatoires, déployées, arrivées à expiration, remplacées et téléchargées  

- ***[Nouveauté]*** Utilisation des catégories de produit UUP  

- ***[Nouveauté]*** Nombre de clients qui ont déployé au moins une mise à jour qualité UUP ou une mise à jour des fonctionnalités UUP  

- ***[Nouveauté]*** Top des codes d’erreur UUP et nombre d’appareils affectés  


### <a name="sqlperformance-data"></a>Données de performances/SQL  

- Configuration et durée de la synthèse du site  

- Nombre des plus grandes tables de base de données  

- Statistiques opérationnelles de découverte (nombre d’objets trouvés)  

- Types de découverte activés et planifiés (complète, incrémentielle)  

- Informations sur les réplicas SQL AlwaysOn, utilisation et état d’intégrité  

- Problèmes de performances du suivi des modifications SQL, période de rétention et état de nettoyage automatique  

- Période de rétention du suivi des modifications SQL  

- Statistiques de performances des messages d’état et de statut, notamment les types de messages les plus courants et les plus coûteux  

- ***[Nouveauté]*** Statistiques sur le trafic du point de gestion (nombre total d’octets envoyés et reçus par le point de terminaison)  

- ***[Nouveauté]*** Mesures du compteur de performances du point de gestion  


### <a name="miscellaneous"></a>Divers  

- Configuration du point de service de l’entrepôt de données, notamment la planification et la durée moyenne de la synchronisation  

- Nombre de scripts et statistiques d’exécution  

- Nombre de sites avec Wake On LAN (WOL)  

- Statistiques de performances et d’utilisation des rapports  

- Statistiques d’utilisation des déploiements par phases  

- Nombre et progression des insights de gestion  

- Nombre de plantages des processus uniques non liés à Configuration Manager sur le serveur de site, avec l’ID de signature Watson, le cas échéant  



##  <a name="bkmk_level3"></a> Niveau 3 – Complet

Le niveau Complet inclut toutes les données des niveaux De base et Étendu. Il inclut également des informations supplémentaires sur Endpoint Protection, les pourcentages de compatibilité des mises à jour et les informations de mise à jour logicielle. Ce niveau peut également inclure des informations de diagnostics avancées, notamment sur les fichiers système et les instantanés de mémoire. Ces données avancées peuvent inclure des informations personnelles qui existent dans la mémoire ou dans les fichiers journaux au moment de la capture.

Pour Configuration Manager version 1810, ce niveau comprend les données suivantes :

- Informations sur le calendrier d’évaluation de règle de déploiement automatique  

- Récapitulatif d’intégrité ATP  

- Statistiques d’évaluation et d’actualisation des regroupements  

- Statistiques de stratégie de conformité pour les erreurs et la conformité  

- Paramètres de conformité : détails de configuration des modèles SCEP, VPN, Wi-Fi et de stratégie de conformité  

- Pack de configuration DCM pour l’utilisation de Configuration Manager  

- Détails des erreurs d’installation du déploiement des clients  

- Récapitulatif de l’intégrité Endpoint Protection : nombre de clients protégés, présentant un risque, inconnus et non pris en charge  

- Configuration de la stratégie Endpoint Protection  

- Liste des processus configurés avec le comportement à l’installation des applications  

- Nombre minimal/maximal/moyen d’heures depuis la dernière analyse des mises à jour logicielles  

- Nombre minimal/maximal/moyen de clients inactifs dans les regroupements de déploiements de mise à jour logicielle  

- Nombre minimal/maximal/moyen de mises à jour logicielles par package  

- Statistiques de déploiement du code produit MSI  

- Compatibilité globale des déploiements de mise à jour logicielle  

- Nombre de groupes avec des mises à jour logicielles expirées  

- Nombres et codes d’erreur de déploiement de mise à jour logicielle  

- Informations de déploiement de mise à jour logicielle : pourcentage de déploiements ciblés avec le client ou l’heure UTC, obligatoire/facultatif/en mode silencieux, et suppression du redémarrage  

- Produits des mises à jour logicielles synchronisés par point de mise à jour logicielle  

- Pourcentages de réussite d’analyse des mises à jour logicielles  

- 50 premières unités centrales dans l’environnement  

- Type de stratégies d’accès conditionnel EAS (Exchange Active Sync) (bloquer ou mettre en quarantaine) pour les appareils gérés par Microsoft Intune  

- Détails des applications de Microsoft Store pour Entreprises : liste de non-agrégation des applications synchronisées, notamment l’ID de l’application, l’état en ligne ou hors connexion, et le nombre total de licences achetées  

- ***[Nouveauté]*** Nombre de clients envoyés (push) avec l’option de ne pas autoriser le repli sur NTLM  
