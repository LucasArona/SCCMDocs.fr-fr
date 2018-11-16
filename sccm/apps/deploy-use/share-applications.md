---
title: Partager des applications dans le Centre logiciel
titleSuffix: Configuration Manager
description: Partagez un lien vers une application dans le Centre logiciel de System Center Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 309a369358789e1948ab7b17ddb0e3619ae1b129
ms.sourcegitcommit: 2504617dc4db90e205327d06cab32f050e88dbf2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51505157"
---
# <a name="share-an-application-from-software-center"></a>Partager une application à partir du Centre logiciel

*S’applique à : System Center Configuration Manager (Current Branch)* <!-- 1706 -->

Pour copier un lien hypertexte vers une application dans le Centre logiciel, utilisez le bouton ![Partager](media/share15.png)**Partager** qui se trouve dans la vue Détails de l’application. Vous pouvez uniquement partager des liens hypertexte vers des applications. En cas d’indisponibilité de l’application, le lien hypertexte ouvre une fenêtre contenant un message de type « Application non disponible ».

1. Choisissez **Applications**, puis sélectionnez l’application.
2. Cliquez sur le bouton ![Partager](media/share15.png) **Partager**.
3. Dans la fenêtre, cliquez sur **Copier**.
4. Collez l’URL dans un e-mail pour partager l’application.  

> [!TIP]  
>  Pour créer un lien dans un e-mail Outlook, appuyez sur **CTRL** + **K** et collez l’URL.  
>  
> Par défaut, Outlook affiche une alerte de sécurité pour le protocole du Centre logiciel quand le destinataire clique sur le lien. Vous pouvez empêcher ce comportement dans votre environnement en ajoutant une clé de protocole approuvée au Registre. Par exemple, `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
