---
title: Outil de nettoyage de la bibliothèque de contenu
titleSuffix: Configuration Manager
description: Utilisez l’outil de nettoyage de la bibliothèque de contenu pour supprimer le contenu orphelin qui n’est plus associé à un déploiement de System Center Configuration Manager.
ms.date: 4/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d83b23673d8eea6e98f21ea30b6b802eb7e5595
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>Outil de nettoyage de la bibliothèque de contenu pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 À partir de la version 1702, vous pouvez utiliser un outil en ligne de commande (**ContentLibraryCleanup.exe**) pour supprimer le contenu qui n’est plus associé à un package ni une application à partir d’un point de distribution (contenu orphelin). Cet outil , nommé outil de nettoyage de la bibliothèque de contenu, remplace les anciennes versions des outils similaires distribuées pour les anciens produits Configuration Manager.  

L’outil affecte uniquement le contenu du point de distribution spécifié à l’exécution de l’outil. L’outil ne peut pas supprimer le contenu de la bibliothèque de contenu sur le serveur de site.

Vous trouverez **ContentLibraryCleanup.exe** dans le dossier *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* sur le serveur du site d’administration centrale ou du site principal.

## <a name="requirements"></a>spécifications  
 L’outil ne peut s’exécuter que sur un seul point de distribution à la fois.  
 - Il peut s’exécuter directement sur l’ordinateur qui héberge le point de distribution à nettoyer, ou à distance à partir d’un autre serveur.
 - Le compte d’utilisateur qui exécute l’outil doit avoir directement des autorisations d’administration basée sur des rôles qui correspondent à un administrateur complet dans la hiérarchie Configuration Manager. L’outil ne fonctionne pas quand le compte reçoit ces autorisations comme membre d’un groupe de sécurité Windows qui dispose des autorisations d’administrateur complet.

## <a name="modes-of-operation"></a>Modes opératoires
Vous pouvez exécuter l’outil dans les deux modes suivants. Nous vous recommandons d’exécuter l’outil en mode *Simulation* afin de pouvoir consulter les résultats avant d’exécuter l’outil en *mode Suppression* :
  1.    **Mode de simulation** :   
      Si vous ne spécifiez pas le commutateur **/delete**, l’outil s’exécute en mode de simulation et identifie le contenu qui serait supprimé à partir du point de distribution.
   - Dans ce mode, l’outil ne supprime aucune donnée.
   - Les informations sur le contenu qui serait supprimé sont écrites dans le fichier journal de l’outil, et vous n’êtes pas invité à confirmer chaque suppression potentielle.  
      </br>   

  2. **Mode Suppression** :   
    Quand vous exécutez l’outil avec le commutateur **/delete**, l’outil s’exécute en mode de suppression.

     - Dans ce mode, le contenu orphelin qui se trouve sur le point de distribution spécifié peut être supprimé de la bibliothèque de contenu du point de distribution.
     -  Avant de supprimer chaque fichier, vous devez confirmer que le fichier doit être supprimé.  Vous pouvez sélectionner **Y** pour oui, **N** pour non, ou **Oui pour tout** pour ignorer les autres invites et supprimer tout le contenu orphelin.  
     </br>

Quand l’outil s’exécute dans l’un de ces modes, il crée automatiquement un journal avec un nom qui inclut le mode d’exécution de l’outil, le nom du point de distribution et la date et l’heure de l’opération. Le fichier journal s’ouvre automatiquement quand l’exécution de l’outil est terminée.

Par défaut, le fichier journal est écrit dans le dossier temporaire du compte d’utilisateur qui exécute l’outil, sur le même ordinateur. Vous pouvez utiliser le commutateur **/log** pour rediriger le fichier journal vers un autre emplacement, y compris un partage réseau.


## <a name="run-the-tool"></a>Exécution de l'outil
Pour exécuter l’outil :
1. Ouvrez une invite de commandes d’administration dans un dossier qui contient **ContentLibraryCleanup.exe**.  
2. Entrez ensuite une ligne de commande qui inclut les commutateurs de ligne de commande obligatoires ainsi que les commutateurs facultatifs que vous souhaitez utiliser.

**Problème connu** : lorsque l’outil s’exécute, une erreur de ce type peut être renvoyée si un package ou un déploiement, quel qu’il soit, a échoué ou est en cours :
-  *System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.*

**Solution de contournement :** aucune. L’outil ne peut pas identifier de façon fiable les fichiers orphelins lorsque du contenu est en cours de déploiement ou n’a pas pu être déployé. Par conséquent, l’outil ne vous autorisera pas à nettoyer le contenu tant que ce problème ne sera pas résolu.

### <a name="command-line-switches"></a>Commutateurs de ligne de commande  
Les commutateurs de ligne de commande suivants peuvent être utilisés dans n’importe quel ordre.   

|Commutateur|Détails|
|---------|-------|
|**/delete**  |**Facultatif** </br> Utilisez ce commutateur quand vous souhaitez supprimer le contenu à partir du point de distribution. Vous êtes invité à confirmer que le contenu doit être supprimé. </br></br> Quand ce commutateur n’est pas utilisé, l’outil enregistre les résultats sur le contenu qui serait supprimé, mais ne supprime pas de contenu du point de distribution. </br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**Facultatif** </br> Ce commutateur exécute l’outil dans un mode silencieux qui supprime toutes les invites (telles que les invites pour supprimer du contenu), et n’ouvre pas automatiquement le fichier journal. </br></br> Exemple : ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;nom de domaine complet du point de distribution>**  | **Obligatoire** </br> Spécifiez le nom de domaine complet du point de distribution que vous souhaitez nettoyer. </br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;nom de domaine complet du site principal>**       | **Facultatif** lors du nettoyage du contenu à partir d’un point de distribution sur un site principal.</br>**Obligatoire** lors du nettoyage du contenu à partir d’un point de distribution sur un site secondaire. </br></br>L’outil se connecte au site parent principal pour exécuter des requêtes sur SMS_Provider. Ces requêtes permettent à l’outil de déterminer le contenu qui doit être sur le point de distribution, afin de pouvoir identifier le contenu qui est orphelin et peut être supprimé. Cette connexion au site parent principal doit être établie pour les points de distribution sur un site secondaire, car les détails nécessaires ne sont pas accessibles directement à partir du site secondaire.</br></br> Spécifiez le nom de domaine complet du site principal auquel le point de distribution appartient, ou du site principal parent quand le point de distribution est sur un site secondaire. </br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;code du site principal>**  | **Facultatif** lors du nettoyage du contenu à partir d’un point de distribution sur un site principal.</br>**Obligatoire** lors du nettoyage du contenu à partir d’un point de distribution sur un site secondaire. </br></br> Spécifiez le code du site principal auquel le point de distribution appartient, ou du site principal parent quand le point de distribution est sur un site secondaire.</br></br> Exemple : ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**Facultatif** </br> Spécifiez l’emplacement d’écriture du fichier journal par l’outil. Il peut s’agir d’un lecteur local ou d’un emplacement sur un partage réseau.</br></br> Lorsque ce commutateur n’est pas utilisé, le fichier journal est placé dans le dossier temporaire de l’utilisateur, sur l’ordinateur où s’exécute l’outil.</br></br> Exemple de lecteur local : ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>Exemple de partage réseau : ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;partage>\&lt;dossier>***|
