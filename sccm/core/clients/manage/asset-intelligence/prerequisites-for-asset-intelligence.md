---
title: Prérequis pour Asset Intelligence
titleSuffix: Configuration Manager
description: Prenez connaissance des conditions préalables pour Asset Intelligence dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 23ab4f94-7bfe-436e-8a6a-029409a2730c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8e7477f8a5b837327640f78656070579fad23a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="prerequisites-for-asset-intelligence-in-system-center-configuration-manager"></a>Conditions préalables pour Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, Asset Intelligence est soumis à des dépendances externes et à des dépendances au sein du produit.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  
 Le tableau suivant présente les dépendances d’Asset Intelligence qui sont externes à Configuration Manager.  

|Dépendance|Informations complémentaires|  
|----------------|----------------------|  
|Audit des conditions requises pour les événements d'ouverture de session réussis|Quatre rapports Asset Intelligence affichent des informations extraites des journaux d'événements de sécurité Windows sur les ordinateurs client. Si les paramètres du journal des événements de sécurité ne sont pas configurés pour consigner tous les événements de connexion réussie, ces rapports ne contiennent aucune donnée, même si la classe de rapport d'inventaire matériel appropriée est activée.<br /><br /> Les rapports Asset Intelligence suivants dépendent des informations du journal des événements de sécurité Windows :<br /><br /> -   Matériel 03A - Utilisateurs d’ordinateurs principaux<br />-   Matériel 03B - Ordinateurs d’un utilisateur de console principal spécifique<br />-   Matériel 04A - Ordinateur partagé (multi-utilisateur)<br />-   Matériel 05A - Utilisateurs de console sur un ordinateur spécifique<br /><br /> Pour activer l'agent du client d'inventaire matériel en vue de répertorier les informations requises par ces rapports, vous devez d'abord modifier les paramètres du journal des événements de sécurité Windows sur les clients afin de consigner tous les événements de connexion réussie et activer la classe de rapport d'inventaire matériel **SMS_SystemConsoleUser** . Pour plus d’informations sur la modification des paramètres du journal des événements de sécurité afin de consigner tous les événements de connexion réussie, consultez [Activer l’audit des événements de connexion réussie](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableSuccessLogonEvents).|  

> [!NOTE]  
>  La classe de rapport d'inventaire matériel **SMS_SystemConsoleUser** conserve uniquement les données d'événement de connexion réussie enregistrées au cours des 90 derniers jours dans le journal des événements de sécurité, sans tenir compte de la longueur du journal. Si les données contenues dans le journal des événements de sécurité datent de moins de 90 jours, le journal est lu en intégralité.  

## <a name="dependencies-internal-to-configuration-manager"></a>Dépendances internes à Configuration Manager  
 Le tableau suivant présente les dépendances d’Asset Intelligence qui sont internes à Configuration Manager.  

|Dépendance|Informations complémentaires|  
|----------------|----------------------|  
|Conditions requises pour l'agent du client|Les rapports Asset Intelligence dépendent des informations du client obtenues par l'intermédiaire des rapports d'inventaires logiciels et matériels. Pour obtenir les informations nécessaires à tous les rapports Asset Intelligence, vous devez activer les agents clients suivants :<br /><br /> -   Agent du client d’inventaire matériel<br />-   Agent du client de contrôle des logiciels|  
|Dépendances de l'agent du client d'inventaire matériel|Pour collecter les données d'inventaire requises par certains rapports Asset Intelligence, vous devez activer l'agent du client d'inventaire matériel. En outre, certaines classes de rapport d'inventaire matériel dont dépendent les rapports Asset Intelligence doivent être activées sur les ordinateurs du serveur de site principal.<br /><br /> Pour plus d’informations sur l’activation de l’agent du client d’inventaire matériel, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).|  
|Dépendances de l'agent du client de contrôle des logiciels|Un grand nombre de rapports Asset Intelligence sur les logiciels dépendent des données de l'agent du client de contrôle des logiciels. Pour plus d’informations sur l’activation de l’agent du client d’inventaire matériel, consultez [Surveiller l’utilisation des applications avec le contrôle de logiciel dans System Center Configuration Manager](../../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).<br /><br /> Les rapports Asset Intelligence suivants dépendent des données de l'agent du client de contrôle des logiciels :<br /><br /> -   Logiciel 07A - Fichiers exécutables récemment utilisés par le nombre d’ordinateurs<br />-   Logiciel 07B - Ordinateurs ayant récemment utilisé un fichier exécutable spécifié<br />-   Logiciel 07C - Fichiers exécutables récemment utilisés sur un ordinateur spécifique<br />-   Logiciel 08A - Fichiers exécutables récemment utilisés par le nombre d’utilisateurs<br />-   Logiciel 08B - Utilisateurs ayant récemment utilisé un fichier exécutable spécifié<br />-   Logiciel 08C - Fichiers exécutables récemment utilisés par un utilisateur spécifié|  
|Conditions requises pour la classe de rapports d'inventaire matériel Asset Intelligence|Dans Configuration Manager, les rapports Asset Intelligence dépendent de classes de rapports d’inventaire matériel spécifiques. Les rapports Asset Intelligence associés ne contiennent aucune donnée tant que les classes de rapport d'inventaire matériel ne sont pas activées et que les clients n'ont pas signalé d'inventaire matériel sur ces classes. Vous pouvez activer les classes de rapport d'inventaire matériel suivantes pour prendre en charge les obligations de rapport Asset Intelligence :<br /><br /> -   SMS_SystemConsoleUsage<sup>1</sup><br />-   SMS_SystemConsoleUser<sup>1</sup><br />-   SMS_InstalledSoftware<br />-   SMS_AutoStartSoftware<br />-   SMS_BrowserHelperObject<br />-   Win32_USBDevice<br />-   SMS_InstalledExecutable<br />-   SMS_SoftwareShortcut<br />-   SoftwareLicensingService<br />-   SoftwareLicensingProduct<br />-   SMS_SoftwareTag<br /><br /> <sup>1</sup> Par défaut, les classes de rapport d'inventaire matériel Asset Intelligence **SMS_SystemConsoleUsage** et **SMS_SystemConsoleUser** sont activées.<br /><br /> Vous pouvez modifier les classes de rapport d’inventaire matériel Asset Intelligence dans la console Configuration Manager, dans l’espace de travail **Ressources et conformité**, quand vous cliquez sur le nœud **Asset Intelligence**. Pour plus d’informations, consultez la section [Activer les classes de création de rapports d’inventaire matériel Asset Intelligence](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence) dans la rubrique [Configuration d’Asset Intelligence dans Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).|  
|Point de Reporting Services|Le rôle de système de site du point de Reporting Services doit être installé avant que vous puissiez afficher les rapports des mises à jour logicielles. Pour plus d'informations sur la création d'un point de Reporting Services, consultez [Configuration des rapports dans Configuration Manager](http://go.microsoft.com/fwlink/p/?LinkId=232661).|  
