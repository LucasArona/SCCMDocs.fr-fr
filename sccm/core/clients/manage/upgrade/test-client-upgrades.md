---
title: Tester les mises à niveau du client dans un regroupement de préproduction
titleSuffix: Configuration Manager
description: Testez les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 49ef2ed2-2e15-4637-8b63-1d5b7f9c17e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5a8e7cbfefcb97506ac83231bcb7c24fc54f919e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129661"
---
# <a name="how-to-test-client-upgrades-in-a-pre-production-collection-in-system-center-configuration-manager"></a>Comment tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez tester une nouvelle version du client Configuration Manager dans un regroupement de préproduction avant de mettre à niveau le reste du site vers cette version.  Quand vous procédez ainsi, seuls les appareils qui font partie du regroupement de test sont mis à niveau. Une fois que vous avez pu tester le client, vous pouvez le promouvoir, ce qui rend la nouvelle version du logiciel client disponible pour le reste du site.

> [!NOTE]
> Pour promouvoir un client de test en production, vous devez être connecté tant qu’utilisateur avec le rôle de sécurité **Administrateur complet** et une étendue de sécurité de **Tout**. Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration). Vous devez également être connecté à un serveur connecté au site d’administration centrale ou à un site principal autonome du plus haut niveau.

 Il existe 3 étapes de base pour tester des clients en préproduction.  

1.  Configurez les mises à jour automatiques du client pour utiliser un regroupement de préproduction.  

2.  Installez une mise à jour de Configuration Manager qui inclut une nouvelle version du client.  

3.  Promouvez le nouveau client en production.  

##  <a name="to-configure-automatic-client-upgrades-to-use-a-pre-production-collection"></a>Pour configurer les mises à jour automatiques du client pour utiliser un regroupement de préproduction  
> [!IMPORTANT]
> Le déploiement du client de préproduction n’est pas pris en charge pour les ordinateurs de groupe de travail. Ils ne peuvent pas utiliser l’authentification nécessaire pour permettre au point de distribution d’accéder au package du client de préproduction.  Ils recevront la dernière version du client quand il sera promu client de production.

1. [Configurez un regroupement](../collections/create-collections.md) contenant les ordinateurs sur lesquels vous voulez déployer le client de préproduction.   

2. Dans la console Configuration Manager, ouvrez **Administration** > **Configuration du site** > **Sites**, puis choisissez **Paramètres de hiérarchie**.  

    Sous l’onglet **Mise à niveau des clients** des **Propriétés des paramètres de hiérarchie**:  

   -   Sélectionnez **Mettre à niveau automatiquement tous les clients du regroupement de préproduction en utilisant un client de préproduction**.  

   -   Entrez le nom d’un regroupement à utiliser comme regroupement de préproduction.  

![Tester les mises à niveau du client](media/test-client-upgrades.png)

>[!NOTE]
>Pour modifier ces paramètres, votre compte doit être un membre du rôle de sécurité **Administrateur complet** et de l’étendue de sécurité **Tous**.


##  <a name="to-install-a-configuration-manager-update-that-includes-a-new-version-of-the-client"></a>Pour installer une mise à jour de Configuration Manager qui inclut une nouvelle version du client  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Mises à jour et services**, sélectionnez une mise à jour avec l’indication **Disponible**, puis choisissez **Installer le pack de mise à jour**. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)

     Pour plus d’informations sur l’installation des mises à jour, consultez [Mises à jour pour System Center Configuration Manager](../../../../core/servers/manage/updates.md)  

2.  Lors de l’installation de la mise à jour, dans la page **Options du client** de l’Assistant, sélectionnez **Tester dans le regroupement de préproduction**.  

3.  Déroulez le reste de l’Assistant et installez le pack de mise à jour.  

     Une fois l’Assistant terminé, les clients inclus dans le regroupement de préproduction commencent à déployer le client mis à jour. Vous pouvez surveiller le déploiement de clients mis à niveau en accédant à **Surveillance** > **État du client** > **Déploiement des clients en préproduction**. Pour plus d’informations, consultez [Comment surveiller l’état du déploiement des clients dans System Center Configuration Manager](../../../../core/clients/deploy/monitor-client-deployment-status.md).

    > [!NOTE]
    > L’état du déploiement sur les ordinateurs hébergeant des rôles de système de site dans un regroupement de préproduction peut être signalé comme **Non conforme**, même quand le client a été correctement déployé. Lors de la promotion du client en production, l’état du déploiement est correctement signalé.

##  <a name="to-promote-the-new-client-to-production"></a>Pour promouvoir le nouveau client en production  

1.  Dans la console Configuration Manager, ouvrez **Administration** > **Mises à jour et maintenance**, puis choisissez **Promouvoir le client de préproduction**. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)

    > [!TIP]
    > Le bouton **Promouvoir le client de préproduction** est également disponible quand vous surveillez les déploiements de clients dans la console en utilisant **Surveillance** > **État du client** > **Déploiement des clients en préproduction**.

2.  Examinez les versions du client en production et préproduction, vérifiez que le regroupement de préproduction approprié est spécifié, et cliquez sur **Promouvoir**, puis sur **Oui**.  

3.  Une fois la boîte de dialogue fermée, la version du client mise à jour remplace la version du client en cours d’utilisation dans votre hiérarchie. Vous pouvez ensuite mettre à niveau les clients pour l’ensemble du site. Pour plus d’informations, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

>[!NOTE]
>Pour activer le client de pré-production ou promouvoir un client de pré-production en client de production, votre compte doit être membre du rôle de sécurité avec les autorisations de **lecture** et de **modification** pour l’objet **Packages de mise à jour**.
>Les mises à niveau des clients respectent les fenêtres de maintenance Configuration Manager que vous avez configurées.
