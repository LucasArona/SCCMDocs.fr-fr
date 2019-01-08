---
title: Outil de réinitialisation des mises à jour
titleSuffix: Configuration Manager
description: Utilisez l’outil de réinitialisation des mises à jour pour effectuer des mises à jour dans la console pour System Center Configuration Manager.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 25fa89d6-7e47-45a6-8f4e-70b77560fba6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de5c98e45c6f5d6dca1569de812825cce80d6f70
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417334"
---
# <a name="update-reset-tool"></a>Outil de réinitialisation des mises à jour

*S’applique à : System Center Configuration Manager (Current Branch)*  


À compter de la version 1706, les sites d’administration centrale et les sites principaux Configuration Manager incluent l’outil de réinitialisation des mises à jour Configuration Manager (**CMUpdateReset.exe**). Utilisez l’outil pour résoudre les problèmes de téléchargement ou de réplication des mises à jour dans la console. L’outil se trouve dans le dossier ***\cd.latest\SMSSETUP\TOOLS*** du serveur de site.

Vous pouvez utiliser cet outil avec n’importe quelle version de Current Branch prise en charge.

Utilisez cet outil quand une [mise à jour dans la console](/sccm/core/servers/manage/install-in-console-updates) n’a pas encore été installée et qu’elle se trouve dans un état d’échec. Un état d’échec signifie que le téléchargement de la mise à jour est en cours, mais qu’il est bloqué ou qu’il prend beaucoup trop de temps. Un téléchargement est considéré comme trop long s’il dépasse de plusieurs heures le téléchargement de packages de mise à jour de taille similaire. Il peut également s’agir d’un échec de réplication de la mise à jour sur les sites principaux enfants.  

Lorsque vous exécutez l’outil, il s’exécute sur la mise à jour que vous spécifiez. Par défaut, l’outil ne supprime pas les mises à jour installées ou téléchargées avec succès.  

### <a name="prerequisites"></a>Prérequis
Le compte que vous utilisez pour exécuter l’outil nécessite les autorisations suivantes :
-   Autorisations en **Lecture** et **Écriture** pour la base de données de site du site d’administration centrale et pour chaque site principal de votre hiérarchie. Pour définir ces autorisations, vous pouvez ajouter le compte d’utilisateur en tant que membre des [rôles de base de données fixes](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** et **db_datareader** sur la base de données Configuration Manager de chaque site. L’outil n’interagit pas avec les sites secondaires.
-   **Administrateur local** sur le site de niveau supérieur de votre hiérarchie.
-   **L’administrateur local** sur l’ordinateur hébergeant le point de connexion de service.

Vous devez disposer du GUID du package de mise à jour à réinitialiser. Pour obtenir le GUID :
  1.   Dans la console, accédez à **Administration** > **Mises à jour et maintenance**.
  2.   Dans le volet qui s’affiche, cliquez avec le bouton droit sur l’en-tête d’une des colonnes (comme **État**), puis sélectionnez **GUID du package** pour ajouter cette colonne à l’affichage.
  3.   La colonne affiche maintenant le GUID du package de mise à jour.

> [!TIP]  
> Pour copier le GUID, sélectionnez la ligne pour le package de mise à jour que vous souhaitez réinitialiser, puis utilisez CTRL + C pour copier cette ligne. Si vous collez votre sélection copiée dans un éditeur de texte, vous pouvez ensuite copier uniquement le GUID pour une utilisation en tant que paramètre de ligne de commande quand vous exécutez l’outil.

### <a name="run-the-tool"></a>Exécution de l'outil    
L’outil doit être exécuté sur le site de niveau supérieur de la hiérarchie.

Quand vous exécutez l’outil, utilisez les paramètres de ligne de commande pour spécifier les éléments suivants :
  -   Serveur SQL Server sur le site de niveau supérieur de la hiérarchie.
  -   Nom de la base de données de site sur le site de niveau supérieur.
  -   GUID du package de mise à jour à réinitialiser.

En fonction de l’état de la mise à jour, l’outil identifie les serveurs supplémentaires auxquels il doit accéder.   

Si le package de mise à jour est dans un état *post-téléchargement*, l’outil ne nettoie pas le package. Vous pouvez éventuellement forcer la suppression d’une mise à jour téléchargée avec succès à l’aide du paramètre de suppression de force (consultez les paramètres de ligne de commande plus loin dans cette rubrique).

Une fois que l’outil s’exécute :
-   Si un package a été supprimé, redémarrez le service SMS_Executive sur le site de niveau supérieur. Ensuite, recherchez les mises à jour pour pouvoir retélécharger le package.
-   Si un package n’a pas été supprimé, aucune action n’est nécessaire. La mise à jour se réinitialise, puis redémarre la réplication ou l’installation.

**Paramètres de ligne de commande :**  


|                        Paramètre                         |                                                       Description                                                        |
|----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;Nom de domaine complet de l’instance SQL Server de votre site de niveau supérieur >** | *Obligatoire* <br> Permet de spécifier le nom de domaine complet de l’instance SQL Server qui héberge la base de données de site pour le site de niveau supérieur de votre hiérarchie. |
|                **D - &lt;Nom de la base de données>**                 |                          *Obligatoire* <br> Permet de spécifier le nom de la base de données pour le site de niveau supérieur.                          |
|                 **-P &lt;GUID du package>**                 |                        *Obligatoire* <br> Permet de spécifier le GUID du package de mise à jour à réinitialiser.                        |
|           **-I &lt;Nom de l'instance SQL Server>**           |                    *Facultatif* <br> Permet d’identifier l’instance de SQL Server qui héberge la base de données du site.                     |
|                       **-FDELETE**                       |                       *Facultatif* <br> Permet de forcer la suppression d’un package de mise à jour téléchargé avec succès.                        |

 **Exemples :**  
 Dans un scénario classique, vous souhaitez réinitialiser une mise à jour qui présente des problèmes de téléchargement. Votre nom de domaine complet SQL Server est *server1.fabrikam.com*, la base de données du site est *CM_XYZ* et le GUID du package est *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Vous exécutez : ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 Dans un scénario plus extrême, vous souhaitez forcer la suppression du package de mise à jour problématique. Votre nom de domaine complet SQL Server est *server1.fabrikam.com*, la base de données du site est *CM_XYZ* et le GUID du package est *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Vous exécutez : ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***
