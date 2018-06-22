---
title: Mettre à niveau des installations d’évaluation
titleSuffix: Configuration Manager
description: Découvrez comment mettre à niveau une installation d’évaluation vers une installation complète de System Center Configuration Manager.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9a32f5a3-9917-434f-9811-106170f404be
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b1bbce9f3ca7a1a6cf9c199677b33e34d9be109c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335913"
---
# <a name="upgrade-an-evaluation-installation-of-system-center-configuration-manager-to-a-full-installation"></a>Mettre à niveau une installation d’évaluation de System Center Configuration Manager vers une installation complète

*S’applique à : System Center Configuration Manager (Current Branch)*

Si vous avez installé une version d’évaluation de System Center Configuration Manager, après 180 jours, la console Configuration Manager passe en lecture seule jusqu’à ce que vous activiez le produit dans la page **Maintenance de site** du programme d’installation. À tout moment avant ou après la période de 180 jours, vous pouvez mettre à niveau l’installation d’évaluation vers une installation complète.  

> [!NOTE]  
>  Quand vous connectez une console Configuration Manager à une installation d’évaluation de Configuration Manager, la barre de titre de la console indique le nombre de jours restants avant l’expiration de l’installation d’évaluation. Le nombre de jours n’est pas actualisé automatiquement et est mis à jour uniquement quand vous effectuez une nouvelle connexion à un site.  

 Vous pouvez mettre à niveau les sites suivants qui exécutent une installation d’évaluation :  

-   Site d'administration centrale  
-   Site principal  

Dans la mesure où les sites secondaires ne sont pas considérés comme des installations d'évaluation, il est inutile de modifier un site secondaire après la mise à niveau de son site parent principal vers une installation complète.  

Prérequis à la mise à niveau d’une version d’évaluation vers une version sous licence :  

-   Vous devez disposer d’un produit valide à utiliser pendant la mise à niveau.  
-   Votre compte doit avoir des droits **administrateur** sur l’ordinateur sur lequel le site est installé.  

### <a name="to-upgrade-an-evaluation-version-of-configuration-manager-to-a-licensed-version"></a>Pour mettre à niveau une version d’évaluation de Configuration Manager vers une version sous licence  

1.  Sur le serveur de site, exécutez **Setup.exe** (programme d’installation de Configuration Manager) à partir du dossier d’installation de Configuration Manager (**%chemin%\BIN\X64**). Vous devez exécuter la copie du programme d’installation qui se trouve sur le serveur de site dans le dossier Configuration Manager, car les options de maintenance de site ne sont pas disponibles quand vous exécutez le programme d’installation à partir du support d’installation.  
2.  Dans la page **Avant de commencer**, sélectionnez **Suivant**.  
3.  Dans la page **Mise en route**, sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis sélectionnez **Suivant**.  
4.  Dans la page **Maintenance de site**, sélectionnez **Passer d’une version d’évaluation à une version sous licence**, entrez une clé de produit valide, puis sélectionnez **Suivant**.  
5.  Dans la page **Termes du contrat de licence logiciel Microsoft**, lisez et acceptez les termes du contrat de licence, puis sélectionnez **Suivant**.  
6.  Dans la page **Configuration**, sélectionnez **Fermer** pour terminer l’Assistant.  

    > [!NOTE]  
    >  La barre de titre d’une console Configuration Manager qui reste connectée au site mis à niveau peut indiquer que le site est toujours une version d’évaluation jusqu’à ce que vous reconnectiez la console au site.  
