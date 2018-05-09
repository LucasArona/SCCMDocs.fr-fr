---
title: Fenêtres de maintenance
titleSuffix: Configuration Manager
description: Utilisez les fenêtres de maintenance pour contrôler l’installation des mises à jour par les sites System Center Configuration Manager.
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ca4886d4-7173-46be-8dcd-1657d5b0deb9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 8b81efc7f31339bd7b19530ef603855f0ee8fad6
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
#  <a name="service-windows-for-site-servers"></a>Fenêtres de maintenance pour les serveurs de site

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez configurer les fenêtres de maintenance sur les sites d’administration centrale et les sites principaux pour contrôler l’installation des mises à jour dans la console.  Vous pouvez configurer plusieurs fenêtres, avec la fenêtre autorisée pour l’installation des mises à jour déterminée par une combinaison de toutes les fenêtres de maintenance pour ce serveur de site.

Quand aucune fenêtre de maintenance n’est configurée :
- **Sur votre site de niveau supérieur** (site d’administration centrale ou site principal autonome) vous choisissez quand démarrer l’installation de la mise à jour.
- **Sur un site principal enfant**, la mise à jour s’installe automatiquement après que le site d’administration centrale a installé la mise à jour.
- **Sur un site secondaire**, les mises à jour ne démarrent jamais automatiquement. Vous devez démarrer manuellement l’installation de la mise à jour à partir de la console, après que le site principal parent a installé la mise à jour.

Quand une fenêtre de maintenance est configurée :
- **Sur votre site de niveau supérieur**, vous ne serez pas en mesure de démarrer l’installation d’une nouvelle mise à jour dans la console Configuration Manager. Même avec une fenêtre de maintenance configurée, le site télécharge automatiquement les mises à jour afin qu’elles soient prêtes à être installées.  
- **Sur un site principal enfant**, les mises à jour installées sur un site d’administration centrale sont téléchargées sur le site principal, mais ne démarrent pas automatiquement. Vous ne pouvez pas démarrer manuellement l’installation d’une mise à jour pendant une période bloquée par l’utilisation d’une fenêtre de maintenance. Lorsque les fenêtres de maintenance ne bloquent plus l’installation de la mise à jour, celle-ci démarre automatiquement.
- Les **sites secondaires** ne prennent pas en charge les fenêtres de maintenance et n’installent pas automatiquement les mises à jour. Une fois que le site parent principal d’un site secondaire installe une mise à jour, vous pouvez démarrer la mise à jour du site secondaire à partir de la console.

## <a name="to-configure-a-service-window"></a>Pour configurer une fenêtre de maintenance

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Configuration du site** > **Sites**, puis sélectionnez le serveur de site sur lequel vous voulez configurer une fenêtre de maintenance.  

2.  Ensuite, modifiez les **Propriétés** des serveurs de site et sélectionnez l’onglet **Fenêtre de service** , où vous pouvez ensuite définir une ou plusieurs fenêtres de service pour ce serveur de site.  
