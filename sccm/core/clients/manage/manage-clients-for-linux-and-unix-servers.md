---
title: Gérer les clients Linux et UNIX
titleSuffix: Configuration Manager
description: Découvrez comment gérer les clients sur des serveurs Linux et UNIX dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1bafded91dcdcddacd45134ce6b52f4da9d916ac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334196"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>Guide pratique pour gérer les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous gérez des serveurs Linux et UNIX avec System Center Configuration Manager, vous pouvez configurer des regroupements, des fenêtres de maintenance et des paramètres client pour mieux gérer les serveurs. Par ailleurs, le client Configuration Manager pour Linux et UNIX n’a pas d’interface utilisateur, mais vous pouvez forcer le client à interroger manuellement la stratégie du client.

##  <a name="BKMK_CollectionsforLnU"></a> Regroupements de serveurs Linux et UNIX  
 Utilisez les regroupements pour gérer des groupes de serveurs Linux et UNIX de la même façon que d’autres types de clients. Les regroupements peuvent être des regroupements avec adhésion directe ou des regroupements basés sur une requête. Les regroupements basés sur une requête identifient les systèmes d’exploitation clients, les configurations matérielles ou d’autres détails sur le client qui sont stockés dans la base de données du site. Par exemple, vous pouvez utiliser des regroupements qui incluent des serveurs Linux et UNIX pour gérer les paramètres suivants :  

-   Paramètres du client  

-   Déploiements de logiciels  

-   Application de fenêtres de maintenance  

 Avant de pouvoir identifier un client Linux ou UNIX par son système d’exploitation ou sa distribution, vous devez collecter l’[inventaire matériel](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md) du client.  

 Les paramètres client par défaut pour l’inventaire matériel incluent des informations sur le système d’exploitation de l’ordinateur client. Vous pouvez utiliser la propriété **Légende** de la classe **Système d’exploitation** pour identifier le système d’exploitation d’un serveur Linux ou UNIX.  

 Vous pouvez afficher des informations détaillées sur les ordinateurs qui exécutent le client Configuration Manager pour Linux et UNIX dans le nœud **Appareils** de l’espace de travail **Ressources et Conformité**, dans la console Configuration Manager. Dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager, la colonne **Système d’exploitation** affiche le nom du système d’exploitation de chaque ordinateur.  

 Par défaut, les serveurs Linux et UNIX sont membres du regroupement **Tous les systèmes** . Nous recommandons de créer des regroupements personnalisés qui incluent uniquement les serveurs Linux et UNIX, ou un sous-ensemble de ces serveurs. Les regroupements personnalisés vous permettent de gérer des opérations telles que le déploiement de logiciels ou l’affectation de paramètres client à des groupes d’ordinateurs similaires, et de mesurer ainsi avec précision la réussite d’un déploiement.   

 Quand vous créez un regroupement personnalisé pour des serveurs Linux et UNIX, insérez des requêtes de règle d’appartenance qui incluent l’attribut Légende pour l’attribut Système d’exploitation. Pour plus d’informations sur la création de regroupements, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manage](../../../core/clients/manage/collections/create-collections.md).  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Fenêtres de maintenance pour les serveurs Linux et UNIX  
 Le client Configuration Manager pour les serveurs Linux et UNIX prend en charge l’utilisation des [fenêtres de maintenance](../../../core/clients/manage/collections/use-maintenance-windows.md). Cette prise en charge est inchangée par rapport à celle des clients Windows.  

##  <a name="BKMK_ClientSettingsforLnU"></a> Paramètres client pour les serveurs Linux et UNIX  
 Vous pouvez [configurer les paramètres client](../../../core/clients/deploy/configure-client-settings.md) qui s’appliquent aux serveurs Linux et UNIX de la même façon que vous configurez les paramètres d’autres clients.  

 Par défaut, les **paramètres d’agent client par défaut** s’appliquent aux serveurs Linux et UNIX. Vous pouvez également créer des paramètres client personnalisés et les déployer dans des regroupements de clients spécifiques.  

 Il n’existe pas d’autres paramètres client qui s’appliquent uniquement aux clients Linux et UNIX. Toutefois, il existe des paramètres client par défaut qui ne s’appliquent pas aux clients Linux et UNIX. Le client pour Linux et UNIX applique uniquement les paramètres pour les fonctionnalités qu’il prend en charge.  

 Par exemple, un paramètre d’appareil client personnalisé qui active et configure les paramètres de contrôle à distance est ignoré par les serveurs Linux et UNIX, car le client pour Linux et UNIX ne prend pas en charge le contrôle à distance.  

##  <a name="BKMK_PolicyforLnU"></a> Stratégie d’ordinateur pour les serveurs Linux et UNIX  
 Le client pour les serveurs Linux et UNIX interroge régulièrement la stratégie d’ordinateur de son site pour connaître les configurations demandées et rechercher les déploiements.  

 Vous pouvez également forcer le client sur un serveur Linux ou UNIX à interroger immédiatement la stratégie d’ordinateur. Pour cela, utilisez les informations d’identification **racine** sur le serveur pour exécuter la commande suivante : **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 Des détails sur l’interrogation de la stratégie d’ordinateur sont entrés dans le fichier journal du client partagé **scxcm.log**.  

> [!NOTE]  
>  Le client Configuration Manager pour Linux et UNIX ne demande et ne traite jamais de stratégie utilisateur.  

##  <a name="BKMK_ManageLinuxCerts"></a> Gérer les certificats sur le client pour Linux et UNIX  
 Après avoir installé le client pour Linux et UNIX, vous pouvez utiliser l’outil **certutil** pour mettre à jour le client avec un nouveau certificat PKI et importer une nouvelle liste de révocation de certificats (CRL). Quand vous installez le client pour Linux et UNIX, cet outil est placé dans **/opt/microsoft/configmgr/bin/certutil**. 

 Pour gérer les certificats, sur chaque client, exécutez certutil avec l’une des options suivantes :  

|Option|Plus d'informations|  
|------------|----------------------|  
|importPFX|Utilisez cette option pour spécifier un certificat pour remplacer le certificat actuellement utilisé par un client.<br /><br /> Quand vous utilisez **-importPFX**, vous devez également utiliser le paramètre de ligne de commande **-password** pour fournir le mot de passe associé au fichier PKCS#12.<br /><br /> Utilisez **-rootcerts** pour spécifier des exigences de certificat racine supplémentaires.<br /><br /> Exemple : **certutil -importPFX &lt;chemin du certificat PKCS#12> -mot de passe &lt;mot de passe de certificat\> [-rootcerts &lt;liste de certificats séparés par des virgules>]**|  
|-importsitecert|Utilisez cette option pour mettre à jour le certificat de signature du serveur de site qui se trouve sur le serveur d’administration.<br /><br /> Exemple : **certutil -importsitecert &lt;chemin du certificat DER\>**|  
|-importcrl|Utilisez cette option pour mettre à jour la liste de révocation de certificats sur le client avec un ou plusieurs chemins d’accès de fichiers CRL.<br /><br /> Exemple : **certutil -importcrl &lt;liste de chemins de fichier CRL séparés par des virgules\>**|  
