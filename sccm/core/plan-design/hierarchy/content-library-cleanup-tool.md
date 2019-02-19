---
title: Outil de nettoyage de la bibliothèque de contenu
titleSuffix: Configuration Manager
description: Utilisez l’outil de nettoyage de la bibliothèque de contenu pour supprimer le contenu orphelin qui n’est plus associé à un déploiement Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7662ccba7b6f672888ab8d98954fb8cb70631fe4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134620"
---
# <a name="content-library-cleanup-tool"></a>Outil de nettoyage de la bibliothèque de contenu

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’outil en ligne de commande de nettoyage de la bibliothèque de contenu pour supprimer du contenu qui n’est plus associé à aucun package ou application sur un point de distribution. Ce type de contenu est appelé *contenu orphelin*. Cet outil remplace les versions plus anciennes des outils similaires distribuées pour les produits Configuration Manager antérieurs.  

L’outil affecte uniquement le contenu du point de distribution spécifié à l’exécution de l’outil. L’outil ne peut pas supprimer du de la bibliothèque de contenu sur le serveur de site.

Recherchez **ContentLibraryCleanup.exe** dans `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` sur le serveur de site.



## <a name="requirements"></a>spécifications  

- Exécutez l’outil sur un seul point de distribution à la fois.  

- Exécutez-le directement sur l’ordinateur qui héberge le point de distribution à nettoyer ou à distance à partir d’un autre ordinateur.  

- Le compte d’utilisateur qui exécute l’outil doit avoir des autorisations identiques à celles du rôle de sécurité **Administrateur complet** dans Configuration Manager.  



## <a name="modes-of-operation"></a>Modes opératoires

Exécutez l’outil dans les deux modes suivants : [Scénario](#what-if-mode) et [Suppression](#delete-mode).

> [!Tip]  
> Démarrez avec le mode *Scénario*. Quand vous êtes satisfait des résultats, exécutez l’outil en mode *Suppression*.  


### <a name="what-if-mode"></a>Mode Scénario   

Si vous ne spécifiez pas le paramètre `/delete`, l’outil s’exécute en mode Scénario. Ce mode identifie le contenu qui serait supprimé du point de distribution.

- Dans ce mode, l’outil ne supprime aucune donnée.  

- L’outil écrit dans le fichier journal des informations sur le contenu qui serait supprimé. Vous n’êtes pas invité à confirmer chaque suppression potentielle.  


### <a name="delete-mode"></a>Mode Suppression   

Quand vous exécutez l’outil avec le paramètre `/delete`, l’outil s’exécute en mode Suppression.

- Dans ce mode, le contenu orphelin trouvé sur le point de distribution spécifié peut être supprimé de la bibliothèque de contenu du point de distribution.  

- Avant de supprimer chaque fichier, confirmez que l’outil doit le supprimer. Sélectionnez **O** pour Oui, **N** pour Non ou **Oui pour tout** pour ignorer les autres invites et supprimer tout le contenu orphelin.  


### <a name="log-file"></a>Fichier journal

Quand l’outil s’exécute dans l’un ou l’autre mode, il crée automatiquement un journal. Il nomme le fichier journal avec les informations suivantes : 
- Le mode dans lequel l’outil s’exécute  
- Le nom du point de distribution  
- La date et l’heure de l’opération  

Quand l’exécution de l’outil est terminée, celui-ci ouvre automatiquement le fichier journal dans Windows. 

Par défaut, l’outil écrit le fichier journal dans le dossier temporaire du compte d’utilisateur qui exécute l’outil. Cet emplacement se trouve sur l’ordinateur où vous exécutez l’outil, qui n’est pas toujours la cible de l’outil. Utilisez le commutateur `/log` pour rediriger le fichier journal vers un autre emplacement, y compris un partage réseau.



## <a name="run-the-tool"></a>Exécution de l'outil

Pour exécuter l’outil : 

1. Ouvrez une invite de commandes en tant qu’administrateur. Accédez au répertoire du dossier qui contient **ContentLibraryCleanup.exe**.  

2. Entrez une ligne de commande qui inclut les [paramètres de ligne de commande](#bkmk_params) obligatoires, ainsi que les paramètres facultatifs que vous voulez utiliser.



## <a name="bkmk_params"></a> Paramètres de ligne de commande  

Utilisez ces paramètres de ligne de commande dans n’importe quel ordre.   

### <a name="required-parameters"></a>Paramètres obligatoires

|Paramètre|Détails|
|---------|-------|
| `/dp <distribution point FQDN>`  | Spécifiez le nom de domaine complet du point de distribution à nettoyer. |
| `/ps <primary site FQDN>` | *Obligatoire* seulement lors du nettoyage du contenu d’un point de distribution sur un site secondaire. L’outil se connecte au site parent principal pour exécuter des requêtes sur le fournisseur SMS. Ces requêtes permettent à l’outil de déterminer quel contenu doit se trouver sur le point de distribution. Il peut alors identifier le contenu orphelin à supprimer. Cette connexion au site parent principal doit être établie pour les points de distribution sur un site secondaire, car les détails nécessaires ne sont pas accessibles directement à partir du site secondaire.|
| `/sc <primary site code>`  | *Obligatoire* seulement lors du nettoyage du contenu d’un point de distribution sur un site secondaire. Spécifiez le code de site du site principal parent. |

#### <a name="example-scan-and-log-what-content-it-would-delete-what-if"></a>Exemple : Analyse et journalisation du contenu qu’il supprimerait (Scénario)
`ContentLibraryCleanup.exe /dp server1.contoso.com`

#### <a name="example-scan-and-log-content-for-a-dp-at-a-secondary-site"></a>Exemple : Analyse et journalisation du contenu pour un point de distribution sur un site secondaire
`ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com /sc ABC` 


### <a name="optional-parameters"></a>Paramètres facultatifs

|Paramètre|Détails|
|---------|-------|
|`/delete`| Utilisez ce paramètre quand vous êtes prêt à supprimer du contenu du point de distribution. Il vous demande confirmation avant de supprimer du contenu. </br></br> Si vous n’utilisez pas ce paramètre, l’outil consigne les résultats sur le contenu qu’il supprimerait. Sans ce paramètre, il ne supprime aucun contenu du point de distribution. |
| `/q` | Ce paramètre fait que l’outil s’exécute en mode silencieux et supprime toutes les invites. Ces invites portent notamment sur la suppression de contenu. Il n’ouvre pas non plus automatiquement le fichier journal. |
| `/ps <primary site FQDN>` | Facultatif seulement lors du nettoyage du contenu d’un point de distribution sur un site principal. Spécifiez le nom de domaine complet du site principal auquel appartient le point de distribution. |
| `/sc <primary site code>` | Facultatif seulement lors du nettoyage du contenu d’un point de distribution sur un site principal. Spécifiez le code de site du site principal auquel appartient le point de distribution. |
| `/log <log file directory>` | Spécifiez l’emplacement d’écriture du fichier journal par l’outil. Cet emplacement peut être un lecteur local ou un partage réseau.</br></br> Si vous n’utilisez pas ce paramètre, l’outil place le fichier journal dans le répertoire temp de l’utilisateur sur l’ordinateur où l’outil s’exécute.|

#### <a name="example-delete-content"></a>Exemple : Suppression du contenu 
`ContentLibraryCleanup.exe /dp server1.contoso.com /delete`

#### <a name="example-delete-content-without-prompts"></a>Exemple : Suppression de contenu sans invite
`ContentLibraryCleanup.exe /q /dp server1.contoso.com /delete` 

#### <a name="example-log-to-local-drive"></a>Exemple : Journalisation sur le disque local
`ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop` 

#### <a name="example-log-to-network-share"></a>Exemple : Journalisation sur un partage réseau
`ContentLibraryCleanup.exe /dp server1.contoso.com /log \\server\share`


### <a name="known-issue"></a>Problème connu

Quand un package ou un déploiement a échoué, ou s’il est en cours, l’outil peut retourner l’erreur suivante : `System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.`

Aucune solution de contournement n’est disponible pour ce problème. L’outil ne peut pas identifier de façon fiable les fichiers orphelins quand du contenu est en cours de déploiement ou n’a pas pu être déployé. L’outil ne vous permet pas de nettoyer du contenu tant que vous n’avez pas résolu ce problème.
