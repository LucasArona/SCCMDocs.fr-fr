---
title: Inventaire matériel pour Linux et UNIX
titleSuffix: Configuration Manager
description: Découvrez comment utiliser l’inventaire matériel pour Linux et UNIX dans Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b69e6039d7e3626b2e2f7d321bc9150e05ceee3
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748282"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Inventaire matériel pour Linux et UNIX dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Important]  
> Depuis la version 1902, Configuration Manager ne prend en charge les clients Linux ou UNIX. 
> 
> Utilisez plutôt Microsoft Azure Management pour la gestion des serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.

Le client Configuration Manager pour Linux et UNIX prend en charge l’inventaire matériel. Une fois l’inventaire matériel effectué, vous pouvez l’afficher dans l’Explorateur de ressources ou dans les rapports Configuration Manager, et utiliser ces informations pour créer des requêtes et des regroupements qui permettent d’effectuer les opérations suivantes :  

- Déploiement logiciel  

- Application de fenêtres de maintenance  

- Déploiement de paramètres client personnalisés  

L’inventaire matériel pour les serveurs Linux et UNIX utilise un serveur CIM (Common Information Model) basé sur des normes. Le serveur CIM s’exécute en tant que service logiciel (ou démon) et fournit une infrastructure de gestion basée sur des normes DMTF (Distributed Management Task Force). Il fournit des fonctionnalités semblables aux fonctionnalités CIM de l’infrastructure de gestion Windows (WMI, Windows Management Infrastructure) disponibles sur les ordinateurs Windows.  

À partir de la mise à jour cumulative 1, le client pour Linux et UNIX utilise l’**omiserver** version 1.0.6 open source de l’**Open Group**. (Avant la mise à jour cumulative 1, le client utilisait **nanowbem** comme serveur CIM).  

Le serveur CIM est installé dans le cadre de l’installation du client pour Linux et UNIX. Le client pour Linux et UNIX communique directement avec le serveur CIM. Il n’utilise pas l’interface WS-MAN du serveur CIM. Le port WS-MAN sur le serveur CIM est désactivé lors de l’installation du client. Microsoft a développé le serveur CIM désormais disponible en tant qu’open source par l’intermédiaire du projet OMI (Open Management infrastructure). Pour plus d’informations sur le projet OMI, consultez le site web [The Open Group](https://www.opengroup.org/) .  

L’inventaire matériel sur les serveurs Linux et UNIX fonctionne en mappant les classes et les propriétés WMI Win32 existantes aux classes et propriétés équivalentes des serveurs Linux et UNIX. Ce mappage un-à-un des classes et des propriétés permet d’intégrer l’inventaire matériel Linux et UNIX à Configuration Manager. Les données d’inventaire des serveurs Linux et UNIX sont affichées avec l’inventaire des ordinateurs Windows dans la console et les rapports Configuration Manager. Vous bénéficiez ainsi d’une expérience de gestion cohérente et hétérogène.  

> [!TIP]  
>  Vous pouvez utiliser la valeur **Caption** pour la classe **Operating System** pour identifier différents systèmes d’exploitation Linux et UNIX dans les requêtes et les regroupements.  

##  <a name="BKMK_ConfigHardwareforLnU"></a> Configuration de l’inventaire matériel pour les serveurs Linux et UNIX  
 Vous pouvez utiliser les paramètres client par défaut ou créer des paramètres d’appareil client personnalisés pour configurer l’inventaire matériel. Quand vous utilisez des paramètres d’appareil client personnalisés, vous pouvez configurer les classes et les propriétés que vous souhaitez collecter uniquement à partir de vos serveurs Linux et UNIX. Vous pouvez également spécifier des planifications personnalisées pour la collecte d’inventaires delta et complets à partir de vos serveurs Linux et UNIX.  

 Le client pour Linux et UNIX prend en charge les classes d’inventaire matériel suivantes disponibles sur les serveurs Linux et UNIX :  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

Les propriétés de ces classes d’inventaire ne sont pas toutes activées pour les ordinateurs Linux et UNIX dans Configuration Manager.  

##  <a name="BKMK_OperationsforHardwareforLnU"></a> Opérations d’inventaire matériel  
 Une fois la collecte de l’inventaire matériel sur vos serveurs Linux et UNIX terminée, vous pouvez afficher et utiliser ces informations comme s’il s’agissait d’autres ordinateurs, et effectuer les opérations suivantes :  

- Utiliser l’Explorateur de ressources pour afficher des informations détaillées sur l’inventaire matériel collecté à partir de serveurs Linux et UNIX  

- Créer des requêtes basées sur des configurations matérielles spécifiques  

- Créer des regroupements basés sur des requêtes qui reposent sur des configurations matérielles spécifiques  

- Exécuter des rapports qui affichent des détails spécifiques sur les configurations matérielles  

L’inventaire matériel sur un serveur Linux ou UNIX s’exécute conformément au calendrier que vous configurez dans les paramètres client. Par défaut, ce calendrier est exécuté tous les sept jours. Le client pour Linux et UNIX prend en charge les cycles d’inventaire complet et les cycles d’inventaire delta.  

Vous pouvez également forcer le client sur un serveur Linux ou UNIX à exécuter immédiatement l’inventaire matériel. Pour exécuter l’inventaire matériel sur un client, utilisez des informations d’identification **racines** pour exécuter la commande suivante pour démarrer un cycle d’inventaire matériel : `/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

Les actions d’inventaire matériel sont entrées dans le fichier journal du client, **scxcm.log**.  

##  <a name="BKMK_CustomHINVforLinux"></a> Comment utiliser l’infrastructure OMI pour créer un inventaire matériel personnalisé  
 Le client pour Linux et UNIX prend en charge l’inventaire matériel personnalisé que vous pouvez créer à l’aide de l’infrastructure OMI. Pour ce faire, vous devez procédez comme suit :  

1.  Créer un fournisseur d’inventaire personnalisé à l’aide de la source OMI  

2.  Configurer les ordinateurs pour qu’ils utilisent le nouveau fournisseur pour les rapports d’inventaire  

3.  Activer Configuration Manager pour prendre en charge le nouveau fournisseur  

###  <a name="BKMK_LinuxProvider"></a> Créer un fournisseur d’inventaire matériel personnalisé pour les ordinateurs Linux et UNIX :  
 Pour créer un fournisseur d’inventaire matériel personnalisé pour le client Configuration Manager pour Linux et UNIX, utilisez **OMI Source - v.1.0.6** et suivez les instructions du guide de démarrage OMI. Ce processus comprend la création d’un fichier MOF (Managed Object Format) qui définit le schéma du nouveau fournisseur. Plus tard, vous importez le fichier MOF dans Configuration Manager pour activer la prise en charge de la nouvelle classe d’inventaire personnalisée.  

 Vous pouvez télécharger OMI Source - v.1.0.6 et le Guide de prise en main OMI à partir du site web [The Open Group](https://github.com/microsoft/omi/blob/master/README.md) . Ces téléchargements se trouvent sous l’onglet **Documents** de la page suivante du site web OpenGroup.org : [Open Management Infrastructure (OMI)](http://go.microsoft.com/fwlink/p/?LinkId=286805).  

###  <a name="BKMK_AddProvidertoLinux"></a> Configurer chaque ordinateur qui exécute Linux ou UNIX avec le fournisseur d’inventaire matériel personnalisé :  
 Après avoir créé un fournisseur d’inventaire personnalisé, vous devez copier puis inscrire le fichier de bibliothèque du fournisseur sur chaque ordinateur dont vous souhaitez recueillir l’inventaire.  

1.  Copiez la bibliothèque du fournisseur sur chaque ordinateur Linux et UNIX dont vous souhaitez recueillir l’inventaire. Le nom de la bibliothèque du fournisseur ressemble à ceci : **XYZ_MyProvider.so**  

2.  Ensuite, sur chaque ordinateur Linux et UNIX, inscrivez la bibliothèque du fournisseur auprès du serveur OMI. Le serveur OMI s’installe sur l’ordinateur quand vous installez le client Configuration Manager pour Linux et UNIX, mais vous devez inscrire manuellement les fournisseurs personnalisés. Exécutez la ligne de commande suivante pour inscrire le fournisseur : `/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  Une fois le nouveau fournisseur inscrit, testez-le à l’aide de l’outil **omicli** . L’outil **omicli** s’installe sur chaque ordinateur Linux et UNIX quand vous installez le client Configuration Manager pour Linux et UNIX. Par exemple, **XYZ_MyProvider** étant le nom du fournisseur que vous avez créé, exécutez la commande suivante sur l’ordinateur : **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     Pour plus d’informations sur **omicli** et sur la façon de tester les fournisseurs personnalisés, consultez le Guide de prise en main OMI.  

> [!TIP]  
>  Utilisez la distribution de logiciels pour déployer des fournisseurs personnalisés et pour inscrire des fournisseurs personnalisés sur chaque ordinateur client Linux et UNIX.  

###  <a name="BKMK_AddLinuxProvidertoCM"></a> Activer la nouvelle classe d’inventaire dans Configuration Manager :  
 Pour que Configuration Manager puisse créer un rapport d’inventaire avec les données fournies par le nouveau fournisseur sur les ordinateurs Linux et UNIX, vous devez importer le fichier MOF qui définit le schéma de votre fournisseur personnalisé.  

 Pour importer un fichier MOF personnalisé dans Configuration Manager, consultez [Guide pratique pour configurer l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md).  
