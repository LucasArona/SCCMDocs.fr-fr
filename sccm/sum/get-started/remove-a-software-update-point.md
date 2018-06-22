---
title: Supprimer un point de mise à jour logicielle
titleSuffix: Configuration Manager
description: Suivez cette procédure pour supprimer le rôle système de site du point de mise à jour logicielle sur un site à partir de la console Configuration Manager.
author: aczechowski
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 585077c44b13d79da55e8ab140fd93998b8371c1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353567"
---
#  <a name="BKMK_RemoveSUP"></a> Supprimer le rôle de système de site du point de mise à jour logicielle  

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez supprimer le rôle système de site du point de mise à jour logicielle sur un site à partir de la console Configuration Manager. La stratégie du client est mise à jour, de façon à retirer le point de mise à jour logicielle de la liste. Lorsque vous supprimez le dernier point de mise à jour logicielle du site, le point de mise à jour logicielle ne contient plus de points de mise à jour logicielle et les mises à jour logicielles sont purement et simplement désactivées au niveau du site. Quand un site principal contient plusieurs points de mise à jour logicielle et que vous supprimez celui qui est configuré comme source de synchronisation, vous devez en choisir un autre sur le site pour en faire la nouvelle source de synchronisation.  

> [!NOTE]  
>  Lorsque vous supprimez d'un système de site le rôle de site du point de mise à jour logicielle, attendez au moins 15 minutes avant de le réinstaller.  

 Pour supprimer un point de mise à jour logicielle, suivez les instructions ci-dessous.  

#### <a name="to-remove-the-software-update-point"></a>Pour supprimer le point de mise à jour logicielle  

1.  Dans la console **Configuration Manager** , cliquez sur **Administration**.  

2.  Dans l'espace de travail Administration, développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.  

3.  Sélectionnez le serveur de système de site contenant le point de mise à jour logicielle à supprimer, puis dans **Rôles de système de site**, sélectionnez **Point de mise à jour logicielle**.  

4.  Sous l'onglet **Rôle du site** , dans le groupe **Rôle du site** , cliquez sur **Supprimer le rôle**. Confirmez que vous voulez supprimer le point de mise à jour logicielle ou sélectionnez une nouvelle source de synchronisation pour les autres points de mise à jour logicielle du site.  
