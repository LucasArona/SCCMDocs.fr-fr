---
title: Matériel recommandé
titleSuffix: Configuration Manager
description: Consultez les recommandations de matériel pour mieux assurer la scalabilité de votre environnement System Center Configuration Manager après son déploiement de base.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5267f0af-34d3-47a0-9ab8-986c41276e6c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ed8d93f65526c8bfa9cf4acabf0db09056563e7
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499509"
---
# <a name="recommended-hardware-for-system-center-configuration-manager"></a>Matériel recommandé pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les recommandations suivantes sont des indications destinées à vous aider à adapter votre environnement System Center Configuration Manager pour qu’il prenne en charge un déploiement plus complexe de sites, de systèmes de site et de clients. Elles ne sont pas prévues pour couvrir toutes les configurations possibles de site et de hiérarchie.  

 Aidez-vous des informations des sections suivantes pour prévoir le matériel capable de répondre aux charges de traitement des clients et des sites qui utilisent les fonctionnalités de Configuration Manager disponibles avec les configurations par défaut.  



##  <a name="bkmk_ScaleSieSystems"></a> Systèmes de site  
 Cette section présente les configurations matérielles recommandées pour les systèmes de site Configuration Manager pour les déploiements prenant en charge le nombre maximal de clients et utilisant la plupart ou l’ensemble des fonctionnalités de Configuration Manager. Les déploiements qui ne prennent pas en charge le nombre maximal de clients et qui n’utilisent pas toutes les fonctionnalités disponibles nécessitent généralement moins de ressources informatiques. En règle générale, les facteurs clés qui limitent les performances de l'ensemble du système sont les suivants, par ordre d'importance :  

1.  Performances d'E/S du disque  

2.  Mémoire disponible  

3.  Processeur  

Pour des performances optimales, utilisez des configurations RAID 10 pour tous les lecteurs de données et une connectivité réseau Ethernet 1 Gbit/s.  

###  <a name="bkmk_ScaleSiteServer"></a> Serveurs de site  

|Configuration de site|Cœurs de processeur|Mémoire (Go)|% d’allocation de mémoire pour SQL Server|  
|-------------------------------|---------------|---------------|----------------------------------------|  
|Serveur de site principal autonome avec un rôle site de base de données sur le même serveur<sup>1</sup>|16|96|80|  
|Serveur de site principal autonome avec une base de données de site distante|8|16|-|  
|Serveur de bases de données distant pour un site principal autonome|16|72|90|  
|Serveur de site d’administration centrale avec un rôle site de base de données sur le même serveur<sup>1</sup>|20|128|80|  
|Serveur de site d’administration centrale avec une base de données de site distante|8|16|-|  
|Serveur de bases de données distant pour un site d’administration centrale|16|96|90|  
|Site principal enfant avec un rôle site de base de données sur le même serveur|16|96|80|  
|Serveur de site principal enfant avec une base de données de site distante|8|16|-|  
|Serveur de bases de données distant pour un site principal enfant|16|72|90|  
|Serveur de site secondaire|8|16|-|  

 <sup>1</sup> Quand le serveur de site et SQL Server sont installés sur le même ordinateur, le déploiement prend en charge les [tailles et échelles](/sccm/core/plan-design/configs/size-and-scale-numbers) maximales pour les sites et les clients. Toutefois, cette configuration peut limiter les [options de haute disponibilité pour System Center Configuration Manager](/sccm/protect/understand/high-availability-options), comme l’utilisation d’un cluster SQL Server. De plus, en raison d’un plus grand nombre d’E/S nécessaire pour prendre en charge l’exécution de SQL Server et du serveur de site Configuration Manager sur le même ordinateur, nous vous conseillons d’utiliser une configuration avec une machine SQL Server distante dans les déploiements de plus grande taille.  

###  <a name="bkmk_RemoteSiteSystem"></a> Serveurs de système de site distants  
 Les indications ci-dessous concernent les ordinateurs qui ont un seul rôle de système de site. Ajustez les valeurs indiquées si vous installez plusieurs rôles de système de site sur le même ordinateur.  

|Rôle de système de site|Cœurs de processeur|Mémoire (Go)|Espace disque (Go)|  
|----------------------|---------------|---------------|--------------------|  
|Point de gestion|4|8|50|  
|Point de distribution|2|8|Espace disque exigé par le système d’exploitation et pour stocker le contenu que vous déployez|  
|Catalogue d'applications, avec le service Web et le site Web sur l'ordinateur du système de site|4|16|50|  
|Point de mise à jour logicielle<sup>1</sup>|8|16|Espace disque exigé par le système d’exploitation et pour stocker les mises à jour que vous déployez|  
|Tous les autres rôles de système de site|4|8|50|  

 <sup>1</sup> L’ordinateur qui héberge un point de mise à jour logicielle nécessite les configurations suivantes pour les pools d’applications IIS :  

-   Augmenter la **longueur de file d’attente WsusPool** à **2000**.  

-   Multiplier par quatre la **limite de mémoire privée WsusPool**, ou lui affecter la valeur **0** (illimitée).  

###  <a name="bkmk_DiskSpace"></a> Espace disque pour les systèmes de site  
 L’allocation et la configuration de disque contribuent aux performances de Configuration Manager. Comme chaque environnement Configuration Manager est différent, ajustez les valeurs indiquées ci-dessous en fonction de vos besoins.  

 Pour des performances optimales, placez chaque objet sur un volume RAID séparé et dédié. Pour tous les volumes de données (Configuration Manager et ses fichiers de base de données), utilisez RAID 10 pour des performances optimales.  

|Utilisation des données|Espace disque minimum|25 000 clients|50 000 clients|100 000 clients|150 000 clients|700 000 clients (site d’administration centrale)|  
|----------------|------------------------|--------------------|--------------------|---------------------|---------------------|-----------------------------------------------------|  
|Système d'exploitation|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|Consultez les conseils pour le système d'exploitation.|  
|Fichiers journaux et d’application de Configuration Manager|25 Go|50 Go|100 Go|200 Go|300 Go|200 Go|  
|Fichier .mdf de base de données du site|75 Go par tranche de 25 000 clients|75 Go|150 Go|300 Go|500 Go|2 To|  
|Fichier .ldf de base de données du site|25 Go par tranche de 25 000 clients|25 Go|50 Go|100 Go|150 Go|100 Go|  
|Fichiers de base de données temporaires (.mdf et .ldf)|En fonction des besoins|En fonction des besoins|En fonction des besoins|En fonction des besoins|En fonction des besoins|En fonction des besoins|  
|Contenu (partages de point de distribution)|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|En fonction des besoins<sup>1</sup>|  

 <sup>1</sup> Les instructions relatives à l’espace disque n’incluent pas l’espace requis pour le contenu situé dans la bibliothèque de contenu sur le serveur de site ou les points de distribution. Pour plus d’informations sur la planification de la bibliothèque de contenu, consultez [Bibliothèque de contenu](../../../core/plan-design/hierarchy/the-content-library.md).  

 En plus des indications précédentes, prenez en compte les recommandations suivantes pour prévoir l’espace disque nécessaire :  

-   Chaque client nécessite environ 5 Mo d’espace.  

-   Quand vous planifiez la taille de la base de données temporaire pour un site principal, prévoyez une taille combinée de 25 à 30 % du fichier .mdf de la base de données du site. La taille réelle peut être beaucoup plus petite ou plus grande en fonction des performances du serveur de site et du volume de données entrantes sur de courtes et longues périodes.  

    > [!NOTE]  
    >  Quand vous avez 50 000 clients ou plus sur un site, prévoyez d’utiliser au moins quatre fichiers .mdf de base de données temporaire.  

-   La taille de la base de données temporaire pour un site d’administration centrale est généralement beaucoup plus petite que celle d’un site principal.  

-   La base de données d’un site secondaire a les limitations de taille suivantes :  

    -   SQL Server 2012 Express : 10 Go  

    -   SQL Server 2014 Express : 10 Go  

##  <a name="bkmk_ScaleClient"></a> Clients  
 Cette section présente les configurations matérielles recommandées pour les ordinateurs que vous gérez à l’aide du logiciel client Configuration Manager.  

### <a name="client-for-windows-computers"></a>Client pour les ordinateurs Windows  
 Le tableau suivant indique la configuration minimale requise pour les ordinateurs Windows gérés à l’aide de Configuration Manager, y compris les systèmes d’exploitation embarqués :  

-   **Processeur et mémoire :** reportez-vous à la configuration processeur et RAM requise pour le système d'exploitation de l'ordinateur.  

-   **Espace disque :** 500 Mo d’espace disque disponible, avec 5 Go recommandés pour le cache du client Configuration Manager. L’espace disque requis est moindre si vous utilisez des paramètres personnalisés pour installer le client Configuration Manager :  

    -   Utilisez la propriété /skipprereq de la ligne de commande de CCMSetup pour éviter d’installer des fichiers dont le client n’a pas besoin. Par exemple, exécutez `CCMSetup.exe /skipprereq:silverlight.exe` si le client n’utilise pas le catalogue d’applications. À compter de Configuration Manager 1802, Silverlight n’est plus installé automatiquement.  

    -   Utilisez la propriété SMSCACHESIZE de Client.msi pour définir un fichier de cache d'une taille inférieure à la taille par défaut de 5 120 Mo. La taille minimale est de 1 Mo. Par exemple, `CCMSetup.exe SMSCachesize=2` crée un cache d’une taille de 2 Mo.  

    Pour plus d'informations sur ces paramètres d'installation du client, consultez [À propos des propriétés d'installation du client](../../../core/clients/deploy/about-client-installation-properties.md).  

    > [!TIP]  
    >  L'installation du client avec un minimum d'espace disque est utile pour les appareils Windows Embedded qui ont généralement des tailles de disque plus petites que les ordinateurs Windows standard.  



 Voici des configurations matérielles minimales supplémentaires pour les fonctionnalités facultatives dans Configuration Manager.  

-   **Déploiement du système d’exploitation :** 384 Mo de RAM  

-   **Centre logiciel :** Processeur 500 MHz  

-   **Contrôle à distance** : Pentium 4 Hyper-Threaded 3 GHz (simple cœur) ou processeur comparable, avec au moins 1 Go de RAM pour une expérience optimale.  

### <a name="client-for-linux-and-unix"></a>Client pour Linux et UNIX  
 Le tableau suivant indique la configuration minimale requise pour les ordinateurs Linux et UNIX que vous gérez avec Configuration Manager.  

|Exigence|Détails|  
|-----------------|-------------|  
|Processeur et mémoire|Reportez-vous à la configuration de processeur et mémoire RAM requise pour le système d'exploitation de l'ordinateur.|  
|Espace disque|500 Mo d’espace disque disponible, avec 5 Go recommandés pour le cache du client Configuration Manager.|  
|Connectivité réseau|Les ordinateurs clients Configuration Manager doivent disposer d’une connexion réseau aux systèmes de site Configuration Manager pour en permettre la gestion.|  

##  <a name="bkmk_ScaleConsole"></a> Console Configuration Manager  
 La configuration requise indiquée dans le tableau ci-dessous s’applique à chaque ordinateur qui exécute la console Configuration Manager.  

 **Configuration matérielle minimale :**  

-   Intel i3 ou processeur comparable  

-   2 Go de RAM  

-   2 Go d’espace disque  

|Paramètre PPP|Résolution minimale|  
|-----------------|------------------------|  
|96 / 100 %|1024 x 768|  
|120 /125 %|1280 x 960|  
|144 / 150 %|1600 x 1200|  
|196 / 200 %|2500 x 1600|  

 **Prise en charge de PowerShell :**  

 Quand vous installez la prise en charge de PowerShell sur un ordinateur qui exécute la console Configuration Manager, vous pouvez exécuter des applets de commande PowerShell sur cet ordinateur pour gérer Configuration Manager.

 - PowerShell 3.0 ou ultérieur est pris en charge

En plus de PowerShell, WMF (Windows Management Framework) version 3.0 ou ultérieure est pris en charge.   


##  <a name="bkmk_ScaleLab"></a> Déploiements de laboratoire  
 Utilisez les recommandations de configuration matérielle suivantes pour les déploiements de laboratoire et de test de Configuration Manager. Ces recommandations s’appliquent à tous les types de sites, avec un maximum de 100 clients :  

|Rôle|Cœurs de processeur|Mémoire (Go)|Espace disque (Go)|  
|----------|---------------|-------------------|-----------------------|  
|Serveur de site et de bases de données|2 - 4|8 - 12|100|  
|Serveur de système de site|1 - 4|2 - 4|50|  
|Client|1 - 2|1 - 3|30|  
