---
title: Surveiller la passerelle de gestion cloud
titleSuffix: Configuration Manager
description: Surveiller les clients et le trafic réseau via la passerelle de gestion cloud (CMG).
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4ecbeb2484297160797b7b5632c86cee4ff1122
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332472"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Surveiller la passerelle de gestion cloud dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois que la passerelle de gestion cloud est en cours d’exécution et que les clients se connectent par son intermédiaire, vous pouvez surveiller les clients et le trafic réseau pour vérifier que le service fonctionne comme vous pensez qu’il fonctionne.



## <a name="monitor-clients"></a>Surveiller les clients

Les clients connectés via la passerelle de gestion cloud s’affichent dans la console Configuration Manager de la même façon que les clients locaux. Pour plus d’informations, consultez [Guide pratique pour surveiller des clients](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Surveiller le trafic dans la console

Surveillez le trafic sur la passerelle de gestion cloud à l’aide de la console Configuration Manager :

1. Accédez à **Administration > Services cloud > Passerelle de gestion cloud**.

2. Sélectionnez la passerelle de gestion cloud dans le volet Liste.

3. Affichez les informations de trafic dans le volet Détails pour le point de connexion de la passerelle de gestion cloud et les rôles de système de site auxquels il se connecte.



## <a name="set-up-outbound-traffic-alerts"></a>Configurer des alertes de trafic sortant

Les alertes de trafic sortant vous permettent de savoir quand le trafic réseau est proche d’un niveau de seuil de 14 jours. Quand vous créez la passerelle de gestion cloud, vous pouvez définir des alertes de trafic. Si vous avez ignoré cette partie, vous pouvez toujours configurer les alertes une fois que le service est en cours d’exécution. Réglez les paramètres d’alerte à tout moment.

1. Accédez à **Administration > Services cloud > Passerelle de gestion cloud**.

2. Cliquez avec le bouton droit sur la passerelle de gestion cloud dans le volet Liste, puis choisissez **Propriétés**.

3. Cliquez sur l’onglet **Alertes**. Activez le seuil et les alertes. Spécifiez le seuil de données de 14 jours en gigaoctets (Go). Spécifiez également le seuil en pourcentage auquel déclencher les différents niveaux d’alerte.

4. Cliquez sur **OK** quand vous avez terminé.



## <a name="monitor-logs"></a>Surveiller les journaux

La passerelle de gestion cloud génère des entrées dans plusieurs fichiers journaux. Pour plus d’informations, consultez [Fichiers journaux dans System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).
