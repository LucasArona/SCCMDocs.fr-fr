---
title: Mettez à niveau les clients.
titleSuffix: Configuration Manager
description: Obtenez des informations sur la mise à niveau des clients dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 446c83b5-c292-4e74-ba19-0792ac6b3472
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d63100e5525b24ffd8deba447a10325c8209ea00
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416688"
---
# <a name="upgrade-clients-in-system-center-configuration-manager"></a>Mettre à niveau les clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser différentes méthodes pour mettre à niveau le logiciel client System Center Configuration Manager sur les ordinateurs Windows, les serveurs UNIX et Linux ainsi que les ordinateurs Mac. Les avantages et les inconvénients de chaque méthode sont présentés ci-dessous.  

> [!TIP]  
>  Si vous mettez à niveau votre infrastructure de serveur à partir d’une version précédente de Configuration Manager \(comme Configuration Manager 2007 ou System Center 2012 Configuration Manager\), nous vous recommandons d’effectuer les mises à niveau du serveur, dont l’installation de toutes les mises à jour de Current Branch, avant la mise à niveau des clients. De cette façon, vous disposez également de la version la plus récente du logiciel client.  

## <a name="group-policy-installation"></a>Installation via la stratégie de groupe  
 **Plateforme cliente prise en charge** : Windows  

 **Avantages**  

- N’exige pas la découverte des ordinateurs préalablement à la mise à niveau du client.  

- Peut être utilisée pour l'installation de nouveaux clients ou pour les mises à niveau.  

- Les ordinateurs peuvent lire les propriétés de l'installation du client ayant été publiées dans les services de domaine Active Directory.  

- Ne nécessite pas de configuration ni la présence d'un compte d'installation pour l'ordinateur client choisi.  

  **Inconvénients**  

- Peut occasionner un trafic réseau intense si vous effectuez la mise à niveau d’un grand nombre de clients.  

- Si le schéma Active Directory n’est pas étendu pour Configuration Manager, vous devez utiliser les [paramètres de stratégie de groupe](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientGP) pour ajouter les propriétés d’installation du client aux ordinateurs de votre site.  


## <a name="logon-script-installation"></a>Installation via un script d'ouverture de session  
 **Plateforme cliente prise en charge** : Windows  

 **Avantages**  

- N'exige pas la découverte des ordinateurs avant l'installation du client.  

- Peut être utilisée pour l'installation de nouveaux clients ou pour les mises à niveau.  

- Prend en charge les propriétés de ligne de commande de CCMSetup.  

  **Inconvénients**  

- Peut occasionner un trafic réseau intense si vous effectuez la mise à niveau d’un grand nombre de clients sur une courte période.  

- La mise à niveau de tous les ordinateurs clients peut prendre beaucoup de temps si les utilisateurs ne se connectent pas souvent au réseau.  

  Pour plus d’informations, consultez [Comment installer des clients Configuration Manager à l’aide de scripts de connexion](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientLogonScript).  

## <a name="manual-installation"></a>Installation manuelle  
 **Plateforme cliente prise en charge** : Windows, UNIX/Linux, Mac OS X  

 **Avantages**  

- N’exige pas la découverte des ordinateurs préalablement à la mise à niveau du client.  

- Peut être utile dans le cadre de tests.  

- Prend en charge les propriétés de ligne de commande de CCMSetup.  

  **Inconvénients**  

- Aucune automatisation, peut prendre du temps.  

  Pour plus d'informations, consultez les rubriques suivantes :  

- [Guide pratique pour installer manuellement des clients Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)  

- [Guide pratique pour mettre à niveau les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-linux-and-unix-servers.md)  

- [Guide pratique pour mettre à niveau les clients sur des ordinateurs Mac dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-on-mac-computers.md)  

## <a name="upgrade-installation-application-management"></a>Mettre à niveau l'installation (gestion des applications)  
 **Plateforme cliente prise en charge** : Windows  

> [!NOTE]  
>  Vous ne pouvez pas mettre à niveau des clients Configuration Manager 2007 avec cette méthode. Dans ces circonstances, vous pouvez déployer le client Configuration Manager comme un package à partir du site Configuration Manager 2007 ou vous pouvez utiliser la mise à niveau automatique du client, qui crée et déploie automatiquement un package contenant la dernière version du client.  

 **Avantages**  

- Prend en charge les propriétés de ligne de commande de CCMSetup.  

  **Inconvénients**  

- Peut occasionner un trafic réseau intense si vous distribuez le client vers des regroupements volumineux.  

- Peut être utilisée uniquement pour mettre à niveau le logiciel client sur les ordinateurs ayant été découverts et attribués au site.  

  Pour plus d’informations, consultez [Comment installer les clients Configuration Manager à l’aide d’un package et d’un programme](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientApp).  

## <a name="automatic-client-upgrade"></a>Mise à niveau automatique du client  

> [!NOTE]  
>  Peut être utilisée pour mettre à niveau les clients Configuration Manager 2007 vers des clients System Center Configuration Manager. Un client Configuration Manager 2007 peut être attribué à un site Configuration Manager, mais ne peut effectuer aucune action en dehors de la mise à niveau automatique du client.  

 **Plateforme cliente prise en charge** : Windows  

 **Avantages**  

- Peut être utilisée pour que les clients du site disposent automatiquement de la dernière version.  

- Nécessite une administration minimale.  

  **Inconvénients**  

- Ne peut être utilisée que pour mettre le logiciel client à niveau et ne peut pas être utilisée pour installer un nouveau client.  

- N'est pas compatible avec la mise à niveau simultanée de plusieurs clients.  

- S'applique à tous les clients de la hiérarchie affectés à un site. Ne peut pas être étendue par regroupement.  

- Options de planification limitées.  

  Pour plus d’informations, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

## <a name="client-testing"></a>Test du client  
 **Plateforme cliente prise en charge** : Windows  

 **Avantages**  

- Permet de tester les nouvelles versions du client dans un regroupement de préproduction plus petit.  

- Une fois le test terminé, les clients en préproduction sont promus en production et automatiquement mis à niveau à l’échelle du site Configuration Manager.  

  **Inconvénients**  

- Ne peut être utilisée que pour mettre le logiciel client à niveau et ne peut pas être utilisée pour installer un nouveau client.  

  [Comment tester les mises à niveau du client dans un regroupement de préproduction dans System Center Configuration Manager](../../../../core/clients/manage/upgrade/test-client-upgrades.md)  
