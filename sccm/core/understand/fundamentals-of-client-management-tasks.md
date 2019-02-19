---
title: Principes de base de la gestion des clients
titleSuffix: Configuration Manager
description: Découvrez les tâches que vous exécutez pour gérer les clients System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 468d21123e6a4166957b7dcc8cda614a78d2366e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136396"
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>Principes de base des tâches de gestion des clients pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé les clients System Center Configuration Manager, vous les gérez en exécutant plusieurs tâches.  Certaines tâches sont exécutées à partir de la console Configuration Manager. D’autres sont exécutées à partir de l’application cliente Configuration Manager. L’application cliente Configuration Manager est installée avec le logiciel client Configuration Manager.

## <a name="configuration-manager-console-tasks"></a>Tâches de la console Configuration Manager
 Dans la console Configuration Manager, vous pouvez effectuer diverses tâches de gestion de clients :  

-   Déployer des applications, des mises à jour logicielles, des scripts de maintenance et des systèmes d'exploitation. Configurer l’installation à une date et une heure précises, rendre le logiciel disponible pour que les utilisateurs l’installent sur demande ou configurer la désinstallation des applications.  

-   Protéger les ordinateurs contre les logiciels malveillants et menaces de sécurité, et recevoir un avertissement lorsque des problèmes sont détectés.  

-   Définir les paramètres de configuration client que vous voulez surveiller et corriger s’ils ne sont pas conformes.  

-   Recueillir des informations d'inventaire matériel et logiciel, qui comprennent la surveillance et le rapprochement des informations de licence de Microsoft.  

-   Dépanner des ordinateurs à l’aide d’un contrôle à distance.  

-   Implémenter des paramètres de gestion de l'alimentation pour gérer et surveiller la consommation d'énergie des ordinateurs.  

La console Configuration Manager surveille les tâches précédentes presqu’en temps réel. Les informations sur l’état et les notifications pour chaque tâche sont disponibles dans la console Configuration Manager. Pour capturer des données et des tendances historiques, utilisez les fonctions de rapport intégrées de SQL Server Reporting Services. Les clients envoient des détails au site en tant qu’état du client.  Les informations d’état du client fournissent des indications sur l’intégrité et l’activité du client ; elles sont visibles dans la console ou à l’aide de rapports intégrés pour Configuration Manager. Ces données permettent d’identifier les ordinateurs qui ne répondent pas. Dans certains cas, les problèmes sont résolus automatiquement.  

 Pour plus d’informations sur les tâches de gestion pour les clients, consultez [Comment gérer les clients dans System Center Configuration Manager](../../core/clients/manage/manage-clients.md) et [Comment gérer les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md). Pour en savoir plus sur l’utilisation de rapports, consultez   
            [Présentation des rapports dans System Center Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="configuration-manager-client-application"></a>Application cliente Configuration Manager  
 Quand vous installez le logiciel client Configuration Manager, l’application cliente Configuration Manager est également installée. Contrairement au Centre logiciel, l’application cliente Configuration Manager s’adresse plus au service de support technique qu’aux utilisateurs finaux. Certaines options de configuration nécessitent des autorisations administratives locales et la plupart des options requièrent des connaissances techniques sur le fonctionnement de l’application cliente Configuration Manager. Vous pouvez utiliser cette application pour effectuer les tâches suivantes sur un client :  

-   Consulter les propriétés sur le client : numéro de version, site attribué, point de gestion avec lequel il communique et certificat utilisé, à savoir certificat d’infrastructure à clé publique (PKI) ou certificat auto-signé.  

-   Vérifier que le client a correctement téléchargé une stratégie client après son installation initiale. Vérifier également que les paramètres client sont activés ou désactivés comme prévu, en fonction des paramètres client configurés dans la console Configuration Manager.  

-   Démarrer les actions du client, par exemple télécharger la stratégie client si une modification a été récemment apportée à la configuration dans la console Configuration Manager et que vous ne souhaitez pas attendre la prochaine heure planifiée.  

-   Affecter manuellement un client à un site Configuration Manager ou essayer de trouver un site. Spécifier ensuite le suffixe DNS pour les points de gestion qui publient sur DNS.  

-   Configurer le cache du client qui stocke temporairement les fichiers. Supprimer ensuite les fichiers du cache si vous avez besoin de plus d’espace disque pour installer les logiciels.  

-   Configurer les paramètres de gestion des clients basés sur Internet.  

-   Consulter les lignes de base de configuration qui ont été déployées sur le client, lancer une évaluation de la compatibilité et consulter les rapports de compatibilité.  
