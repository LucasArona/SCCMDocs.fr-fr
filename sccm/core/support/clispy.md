---
title: Client Spy
titleSuffix: Configuration Manager
description: Utilisez Client Spy pour résoudre les problèmes de distribution de logiciels, d’inventaire et de contrôle de logiciel sur les clients Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: adb826a13e96947bba29a3a0928301517d446bc6
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495779"
---
# <a name="client-spy"></a>Client Spy

*S’applique à : System Center Configuration Manager (Current Branch)*

Client Spy fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Il s’agit d’un outil permettant de résoudre les problèmes de distribution de logiciels, d’inventaire et de contrôle de logiciel sur les clients Configuration Manager. 

La plupart des informations récupérées par l’outil se rapportent aux déploiements de logiciels :
- Tous les déploiements de logiciels actuels 
- Historique des distributions de logiciels
- Configuration du cache client
- Éléments mis en cache
- Déploiements obligatoires en attente
- Déploiements disponibles  

Il affiche aussi les informations d’inventaire suivantes
- Date du dernier cycle d’inventaire
- Date du dernier rapport
- Versions majeures et mineures de l’inventaire logiciel
- Regroupement de fichiers
- Inventaire matériel
- Regroupement IDMIF
- Enregistrements de données de découverte (DDR) 

Les règles de contrôle de logiciel sont également affichées. 

> [!Note]   
> Pour améliorer les performances, l’outil collecte uniquement les informations de chaque onglet que vous sélectionnez. De même, lorsque vous cliquez sur **Refresh**, il actualise uniquement les informations de l’onglet affiché.



## <a name="usage"></a>Utilisation


### <a name="tools-menu"></a>Menu Tools

Les actions suivantes sont disponibles dans le menu **Tools** (Outils) :  

#### <a name="connect"></a>Connexion
Récupérez les informations d’un autre ordinateur.  

- Par défaut, l’outil affiche les informations de l’ordinateur actuel. 

- Connectez-vous en utilisant le nom de l’ordinateur distant, le nom d’utilisateur et le mot de passe du compte. L’outil établit une connexion au partage IPC$ sur l’ordinateur distant. Il supprime la connexion quand il se ferme ou quand vous vous connectez à un autre ordinateur.  

- Il nécessite un compte avec des informations d’identification nécessaires pour obtenir les informations.  

- Si vous ne spécifiez pas un nom d’utilisateur et un mot de passe, Client Spy utilise le contexte de sécurité de l’utilisateur actuellement connecté pour tenter d’établir la connexion.  

- Lorsque vous vous connectez à un ordinateur distant, tous les onglets qui sont affichés montrent les informations de l’ordinateur distant.

#### <a name="software-distribution"></a>Distribution de logiciels
Affiche les onglets [Software Distribution](#software-distribution) (Distribution de logiciels) et masque les autres. Par défaut, Spy Client affiche les onglets de distribution de logiciels.

#### <a name="inventory"></a>Inventaire
Affiche l’onglet Inventory (Inventaire) et masque les autres.

#### <a name="software-metering"></a>Contrôle de logiciel
Affiche l’onglet Software Metering (Contrôle de logiciel) et masque les autres.

#### <a name="save-current-tab-to-file"></a>Save current tab to file
Enregistre les informations de l’onglet actuellement affiché dans un fichier texte que vous spécifiez. 

#### <a name="save-all-tabs-to-file"></a>Save all tabs to file
Enregistre les informations de tous les onglets dans un fichier texte que vous spécifiez. Il enregistre uniquement les informations que votre compte peut voir.



## <a name="software-distribution-tab"></a>Onglet Software Distribution

Configurez les paramètres des quatre onglets suivants :
- [Software Distribution Execution Requests](#bkmk_exec-requests)
- [Software Distribution History](#bkmk_history)
- [Software Distribution Cache Information](#bkmk_cache-info)
- [Software Distribution Pending Executions](#bkmk_pending-exec)


### <a name="bkmk_exec-requests"></a> Software Distribution Execution Requests

Cet onglet affiche tous les déploiements existants, notamment les déploiements ciblés par les appareils et les utilisateurs.

Chaque élément de l’arborescence de l’onglet Software Distribution Execution Requests contient les quatre attributs suivants :
- Advertisement ID. Cette valeur peut être vide dans le cas d’un déploiement disponible. 
- ID du package 
- Nom du programme 
- User. Il peut s’agir du SID de l’utilisateur ciblé ou du SID de l’utilisateur qui a initié la demande. Si les deux sont des demandes système, l’utilisateur affiché est System. 

Pour chaque demande d’exécution, il affiche également les informations suivantes dans une structure de sous-arborescence :
- Nom du programme 
- ID du package 
- Nom du package 
- Request Creation Time 
- État 
- Running State, if State is Running 
- Execution Context (User or Admin) 
- History State (Success, Failure, or NotRun) 
- LastRunTime (Never, if the program hasn't been run before) 
- RetryCount, if State is WaitingRetry 
- ContentAccess (Retry Count, if State is WaitingRetry) 
- FailureCode, if State is WaitingRetry 
- FailureReason, if State is WaitingRetry 

Si la demande nécessite du contenu, l’état est WaitingContent. L’onglet Software Distribution Cache Information affiche les détails de cette demande de téléchargement.

Si la demande d’exécution est une demande de téléchargement, il affiche également le nombre d’octets téléchargés.

> [!Note]   
> Il utilise différentes icônes pour les divers états d’une demande d’exécution.


### <a name="bkmk_history"></a> Software Distribution History

Cet onglet contient des informations sur tous les programmes exécutés précédemment. Ces informations sont stockées dans le Registre.

Les branches principales de cette arborescence représentent les historiques des différents utilisateurs, y compris System. Il affiche une sous-arborescence contenant la liste des packages à partir de laquelle les programmes ont été exécutés pour chaque utilisateur. 

Le nom de package et l’ID de package de chaque sous-arborescence de package affiche une liste des programmes qui ont été exécutés. Il affiche les attributs suivants pour chacun d’eux : 
- Nom du programme
- État d’exécution
- Heure de la dernière exécution
- Code d’échec
- Raison de l’échec  

Le code d’échec et la raison de l’échec sont vides quand un programme a été exécuté avec succès.


### <a name="bkmk_cache-info"></a> Software Distribution Cache Information

#### <a name="cache-config"></a>Cache Config
Contient des informations sur le cache du client Configuration Manager. Ces informations indiquent l’emplacement du cache, la taille du cache et s’il est en cours d’utilisation. 

#### <a name="cached-items"></a>Cached Items
Contient une sous-arborescence de tous les éléments actuellement dans le cache. Chaque élément d’arborescence inclut les informations suivantes sur chaque élément : 
- Emplacement de l’élément (dossier) dans le cache
- État actuel
- ID du package
- Nom du package
- Version du package
- Taille du package
- Nombre de références actuelles
- Heure de la dernière référence (UTC)  

#### <a name="downloading-items"></a>Downloading Items
Ce sont les éléments que le client est en train de télécharger. Chacun d’eux affiche les mêmes informations affichées par les éléments mis en cache et le nombre de kilo-octets téléchargés. 


### <a name="bkmk_pending-exec"></a> Software Distribution Pending Executions

Cet onglet contient des informations qui détaille les déploiements obligatoires faits et à faire et une liste des déploiements disponibles.

Chaque branche de l’arborescence est pour chaque compte d’utilisateur avec les déploiements disponibles, y compris System.

Pour chaque utilisateur, une sous-arborescence contient les trois éléments suivants :  

#### <a name="mandatory-advertisements-with-future-executions"></a>Mandatory Advertisements With Future Executions
Il s’agit des publications obligatoires qui ont toujours des programmes restants à exécuter. Elles peuvent être des publications de calendrier récurrentes, uniques ou multiples. Chacune affiche l’ID de publication, l’heure de la prochaine exécution et le calendrier selon lequel elle est exécutée. 

#### <a name="optional-advertisements"></a>Optional Advertisements
Affiche une liste de toutes les publications qui sont publiées. Il affiche également des détails tels que l’ID de publication, le nom du programme et le nom de package de chacune d’elles. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Past Mandatory Advertisements With No Future Scheduled Executions
Il s’agit d’une liste de publications qui existent sur le client pour lesquelles aucun futur programme n’est prévu de s’exécuter. L’ID de publication, le nom du package et le nom du programme sont affichés. Un élément de la sous-arborescence est affiché pour toutes les publications qui sont facultatives.

> [!Note]  
> Les informations de nom de package sont uniquement disponibles pour les packages qui ont des stratégies publiées qui leur sont associées sur l’ordinateur consulté. Les packages qui n’ont plus de stratégies disponibles associées affichent un message indiquant que le nom du package n’est plus disponible (« Package Name No Longer Available »).  



## <a name="inventory-tab"></a>Onglet Inventaire

Un seul onglet contient les informations d’inventaire. L’arborescence principale présente les cinq éléments suivants :  

- **Inventaire logiciel** : contient la date à laquelle le dernier cycle a commencé, la date du dernier rapport et les versions principale et mineure du dernier rapport.  

- **Regroupement de fichiers** : contient la date à laquelle le dernier cycle a commencé, la date du dernier rapport et les versions principale et mineure du dernier rapport.  

- **Inventaire matériel** : contient la date à laquelle le dernier cycle a commencé, la date du dernier rapport et les versions principale et mineure du dernier rapport.  

- **Regroupement IDMIF** : contient la date à laquelle le dernier cycle a commencé, la date du dernier rapport et les versions principale et mineure du dernier rapport.  

- **DDR** : contient la date à laquelle le dernier cycle a commencé, la date du dernier rapport et les versions principale et mineure du dernier rapport. Les informations DDR apparaissent également dans une sous-arborescence.



## <a name="software-metering-tab"></a>Onglet Software Metering

Cet onglet affiche des informations sous forme d’une sous-arborescence et inclut toutes les règles de contrôle de logiciel. Il affiche chaque règle sous forme de nœud, qu’il identifie par le nom de fichier et l’ID de règle. Développez chaque nœud dans l’arborescence et affichez les informations suivantes :
- Nom du fichier Explorer 
- Nom du fichier d’origine
- ID de la règle
- Version du fichier
- Langage


