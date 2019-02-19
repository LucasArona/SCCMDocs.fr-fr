---
title: Configurer des ordinateurs clients pour trouver des points de gestion à l’aide de la publication DNS
titleSuffix: Configuration Manager
description: Définissez des ordinateurs clients pour trouver des points de gestion à l’aide de la publication DNS dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5cebb56324af3993458da5317983697b3304ccf7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128134"
---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>Comment configurer des ordinateurs clients pour trouver des points de gestion à l’aide de la publication DNS dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les clients de System Center Configuration Manager doivent localiser un point de gestion pour terminer l’affectation de site et, dans le cadre d’un processus continu, pour continuer d’être gérés. Les services de domaine Active Directory offrent la méthode la plus sûre pour que les clients sur l'intranet trouvent leurs points de gestion. Toutefois, si les clients ne peuvent pas utiliser cette méthode d'emplacement des services (par exemple, parce que vous n'avez pas étendu le schéma Active Directory ou que les clients font partie d'un groupe de travail), utilisez la publication DNS comme alternative principale à cette méthode.  

> [!NOTE]  
>  Lorsque vous installez le client pour Linux et UNIX, vous devez indiquer le point de gestion à utiliser comme point de contact initial. Pour plus d’informations sur l’installation du client pour Linux et UNIX, consultez [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md).  

 Avant d'utiliser la publication DNS pour les points de gestion, assurez-vous que les serveurs DNS sur l'intranet disposent d'enregistrements de ressource d'emplacement de service (SRV RR) et d'enregistrements de ressource d'hôte correspondant (A ou AAA) pour les points de gestion du site. Les enregistrements de ressource d’emplacement de service peuvent être créés automatiquement par Configuration Manager ou manuellement par l’administrateur DNS qui crée les enregistrements dans DNS.  

 Pour plus d’informations sur la publication DNS comme méthode d’emplacement de service pour les clients Configuration Manager, consultez [Comprendre comment les clients recherchent des services et ressources de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

 Par défaut, les clients recherchent DNS pour les points de gestion dans leur domaine DNS. Toutefois, si aucun point de gestion n’est publié dans le domaine des clients, vous devez configurer manuellement les clients avec un suffixe DNS de point de gestion. Vous pouvez configurer ce suffixe DNS sur les clients, soit pendant l'installation du client, soit après :  

-   Pour configurer les clients pour un suffixe de point de gestion pendant l'installation du client, configurez les propriétés CCMSetup Client.msi.  

-   Pour configurer les clients pour un suffixe de point de gestion après l'installation du client, dans le panneau de configuration, configurez les **Propriétés du Configuration Manager**.  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>Pour configurer les clients pour un suffixe de point de gestion pendant l'installation du client  

- Installez le client avec la propriété CCMSetup Client.msi suivante :  

  - **DNSSUFFIX=** *&lt;domaine du point de gestion\>*  

     Si le site dispose de plusieurs points de gestion et que ceux-ci se trouvent dans plusieurs domaines, ne spécifiez qu'un seul domaine. Lorsque les clients se connectent à un point de gestion dans ce domaine, ils téléchargent une liste de points de gestion disponibles, qui inclura les points de gestion des autres domaines.  

    Pour plus d’informations sur les propriétés de ligne de commande CCMSetup, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>Pour configurer les clients pour un suffixe de point de gestion après l'installation du client  

1.  Dans le Panneau de configuration de l'ordinateur client, accédez à **Configuration Manager**, puis double-cliquez sur **Propriétés**.  

2.  Dans l'onglet **Site** , spécifiez le suffixe DNS d'un point de gestion, puis cliquez sur **OK**.  

     Si le site dispose de plusieurs points de gestion et que ceux-ci se trouvent dans plusieurs domaines, ne spécifiez qu'un seul domaine. Lorsque les clients se connectent à un point de gestion dans ce domaine, ils téléchargent une liste de points de gestion disponibles, qui inclura les points de gestion des autres domaines.
