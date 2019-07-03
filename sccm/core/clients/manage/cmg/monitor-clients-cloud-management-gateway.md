---
title: Surveiller la passerelle de gestion cloud
titleSuffix: Configuration Manager
description: Surveiller les clients et le trafic réseau via la passerelle de gestion cloud (CMG).
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d184118e0e99231a9160322740ab7690488a28a5
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286762"
---
# <a name="monitor-cloud-management-gateway"></a>Surveiller la passerelle de gestion cloud

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois que la passerelle de gestion cloud est en cours d’exécution et que les clients se connectent par son intermédiaire, vous pouvez surveiller les clients et le trafic réseau pour vérifier que le service fonctionne comme vous le pensez.


## <a name="monitor-clients"></a>Surveiller les clients

Les clients connectés via la passerelle de gestion cloud s’affichent dans la console Configuration Manager de la même façon que les clients locaux. Pour plus d’informations, consultez [Guide pratique pour surveiller des clients](/sccm/core/clients/manage/monitor-clients).


## <a name="monitor-traffic-in-the-console"></a>Surveiller le trafic dans la console

Surveillez le trafic sur la passerelle de gestion cloud avec la console Configuration Manager :

1. Accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Passerelle de gestion cloud**.  

2. Dans le volet Liste, sélectionnez la passerelle de gestion cloud.  

3. Affichez les informations de trafic dans le volet Détails pour le point de connexion de la passerelle de gestion cloud et les rôles de système de site auxquels il se connecte. Ces statistiques indiquent les demandes client entrant dans ces rôles. Les demandes incluent la stratégie, l’emplacement, l’inscription, le contenu, l’inventaire et les notifications des clients.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Configurer des alertes de trafic sortant

Les alertes de trafic sortant vous permettent de savoir quand le trafic réseau est proche d’un niveau de seuil de 14 jours. Quand vous créez la passerelle de gestion cloud, vous pouvez configurer des alertes de trafic. Si vous avez ignoré cette partie, vous pouvez toujours configurer les alertes une fois que le service est en cours d’exécution. Réglez les paramètres d’alerte à tout moment.

1. Accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Passerelle de gestion cloud**.  

2. Sélectionnez la passerelle de gestion cloud dans le volet Liste, puis sélectionnez **Propriétés** dans le ruban.  

3. Accédez à l’onglet **Alertes** pour activer le seuil et les alertes. Spécifiez le seuil de données de 14 jours en gigaoctets (Go). Spécifiez également le seuil en pourcentage auquel déclencher les différents niveaux d’alerte.  

4. Sélectionnez **OK** quand vous avez terminé.  


## <a name="monitor-logs"></a>Surveiller les journaux

La passerelle de gestion cloud génère des entrées dans un certain nombre de fichiers journaux. Pour plus d’informations, consultez [Fichiers journaux dans System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Tableau de bord de gestion cloud

<!--1358461-->
À compter de la version 1806, le tableau de bord de gestion cloud fournit une vue centralisée de l’utilisation de la passerelle de gestion cloud. Quand le site est intégré à des [services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la gestion cloud, il affiche également des données sur les utilisateurs et les appareils cloud.  

La capture d’écran suivante montre une partie du tableau de bord de gestion cloud, comprenant deux des vignettes disponibles :  
![Vignettes du tableau de bord de gestion cloud : Trafic de la passerelle de gestion cloud et Clients actuellement en ligne](media/1358461-cmg-dashboard.png)

Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**. Sélectionnez le nœud **Gestion cloud** et affichez les vignettes du tableau de bord.  


## <a name="connection-analyzer"></a>Analyseur de connexion

À compter de la version 1806, utilisez l’analyseur de connexion de la passerelle de gestion cloud pour une vérification en temps réel dans le cadre de la résolution des problèmes. L’utilitaire de la console vérifie l’état actuel du service, ainsi que le canal de communication qui passe par le point de connexion de la passerelle de gestion cloud vers les points de gestion qui autorisent le trafic de la passerelle.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Services cloud**, puis sélectionnez le nœud **Passerelle de gestion cloud**.  

2. Sélectionnez l’instance cible de la passerelle de gestion cloud, puis sélectionnez **Analyseur de connexion** dans le ruban.  

3. Dans la fenêtre Analyseur de connexion de la passerelle de gestion cloud, sélectionnez l’une des options suivantes pour l’authentification auprès du service :  

     1. **Utilisateur AD Azure** : cette option permet de simuler la communication comme avec une identité d’utilisateur cloud connectée à un appareil Windows 10 joint à Azure AD. Cliquez sur **Connexion** pour entrer les informations d’identification du compte d’utilisateur Azure AD de manière sécurisée.  

     2. **Certificat client** : cette option permet de simuler la communication comme avec un client Configuration Manager disposant d’un [certificat d’authentification client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth).  

4. Sélectionnez **Démarrer** pour démarrer l’analyse. La fenêtre de l’analyseur affiche les résultats. Sélectionnez une entrée pour afficher plus de détails dans le champ Description.  


## <a name="bkmk_stop"></a>Arrêter la passerelle de gestion cloud quand elle dépasse le seuil

<!--3735092-->
À partir de la version 1902, Configuration Manager peut désormais arrêter un service de passerelle de gestion cloud quand le transfert de données total dépasse votre limite. Utilisez des [alertes](#set-up-outbound-traffic-alerts) pour déclencher des notifications quand l’utilisation atteint des niveaux d’avertissement ou critiques. Pour aider à réduire les coûts Azure imprévus en raison d’un pic d’utilisation, cette option désactive le service cloud.

> [!Important]  
> Même si le service n’est pas en cours d’exécution, des coûts sont toujours associés au service cloud. L’arrêt du service n’élimine pas tous les coûts Azure associés. Pour supprimer tous les coûts du service cloud, [supprimez la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).  
>
> Quand le service de passerelle de gestion cloud est arrêté, les clients Internet ne peuvent pas communiquer avec Configuration Manager.  

Le transfert de données total (en sortie) inclut les données provenant du service cloud et du compte de stockage. Ces données proviennent des flux suivants :

- Passerelle de gestion cloud vers le client  
- Passerelle de gestion cloud vers le site, notamment les fichiers journaux de la passerelle de gestion cloud  
- Si vous activez le contenu sur la passerelle de gestion cloud : compte de stockage vers le client  

Pour plus d’informations sur ces flux de données, consultez [Ports et flux de données de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#ports-and-data-flow).

Le seuil d’alerte de stockage est distinct. Cette alerte surveille la capacité de votre instance de stockage Azure.

Quand vous sélectionnez l’instance de la passerelle de gestion cloud dans le nœud **Passerelle de gestion cloud** de la console, vous pouvez voir le transfert de données total dans le volet des détails.

Configuration Manager vérifie la valeur du seuil toutes les six minutes. Si un pic d’utilisation soudain se produit, Configuration Manager peut prendre jusqu’à six minutes pour détecter qu’il a dépassé le seuil, puis arrêter le service.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Arrêter le service cloud quand il dépasse le seuil

1. [Configurer des alertes de trafic sortant](#set-up-outbound-traffic-alerts).  

2. Sur l’onglet **Alertes** de la fenêtre Propriétés de la passerelle de gestion cloud, activez l’option **Arrêter ce service lorsque le seuil critique est dépassé**.  

Pour tester cette fonctionnalité, réduisez provisoirement une des valeurs suivantes :  

- **Seuil du transfert de données sortantes sur 14 jours (Go)** . La valeur par défaut est `10000`.  

- **Pourcentage du seuil déclenchant une alerte critique**. La valeur par défaut est `90`.  
