---
title: Power Viewer Tool
titleSuffix: Configuration Manager
description: Utilisez Power Viewer Tool pour voir l’état de la fonctionnalité de gestion de l’alimentation sur un client Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8143e3bf-d6bd-4c69-aec1-e6989cf2ecd9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a90982aa38bbe4c171af1246aa1b12bc67b335d
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385950"
---
# <a name="power-viewer-tool"></a>Power Viewer Tool

*S’applique à : System Center Configuration Manager (Current Branch)*

Power Viewer Tool fait partie des [outils de Configuration Manager](/sccm/core/support/tools). Utilisez-le pour voir l’état de la fonctionnalité de gestion de l’alimentation sur un client Configuration Manager.

Exécutez **PowerVwr.exe** en tant qu’administrateur. Quand l’outil démarre, il affiche les fonctionnalités et les paramètres d’alimentation de l’ordinateur local sous l’onglet **Power Config** (Configuration de l’alimentation). 

Pour voir les données de gestion de l’alimentation d’un ordinateur distant :  

1. Accédez au menu **File** (Fichier), puis cliquez sur **Connect** (Se connecter). 

2. Entrez le nom de l’**Ordinateur**, ainsi qu’un **Nom d’utilisateur** et un **Mot de passe**, si nécessaire. 

Il existe trois onglets dans Power Viewer :  

- **Power Config** (Configuration de l’alimentation) : Affichez les fonctionnalités et les paramètres d’alimentation de l’ordinateur ciblé.  

- **Daily Activity** (Activité quotidienne) : Affichez les graphiques des activités quotidiennes du client, notamment les informations suivantes :  

    - **Computer on** (Ordinateur le) : état d’alimentation de l’ordinateur sur une journée. Le mode veille est considéré comme une mise hors tension.  

    - **Monitor on** (Moniteur le) : état activé ou désactivé du moniteur sur une journée.  

    - **User active** (Utilisateur actif) : informations concernant l’activité utilisateur sur une journée.  

- **Power Events** (Événements d’alimentation) : affichage de tous les événements d’alimentation sur une journée. Le client résume ces événements à minuit. Cette synthèse génère les données du graphique des activités quotidiennes.  
