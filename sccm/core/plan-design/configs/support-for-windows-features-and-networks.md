---
title: Prise en charge des fonctionnalités de Windows
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités Windows et réseau prises en charge par Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 915a8ac1d20ca288b2b830791c8a3b79c65ffbce
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383637"
---
# <a name="support-for-windows-features-and-networks-in-configuration-manager"></a>Prise en charge des fonctionnalités Windows et des réseaux dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article identifie la prise en charge par Configuration Manager des fonctionnalités courantes de Windows et des réseaux.  



##  <a name="bkmk_branchcache"></a> BranchCache  

Utilisez Windows BranchCache avec Configuration Manager quand vous l’activez sur des points de distribution, puis configurez les clients pour l’utiliser en mode de cache distribué.

Configurez les paramètres de BranchCache sur un type de déploiement d’applications, sur le déploiement d’un package et pour les séquences de tâches. À partir de la version 1802, BranchCache est activé par défaut. 

Quand les conditions requises de BranchCache sont remplies, cette fonctionnalité permet aux clients situés à des emplacements distants d’obtenir le contenu des clients locaux qui ont un cache actif du contenu.  

Par exemple, quand le premier client BranchCache demande du contenu à un point de distribution configuré en tant que serveur BranchCache, le client télécharge et met en cache ce contenu. Ce contenu est ensuite rendu disponible pour les clients sur le même sous-réseau qui celui qui a demandé ce contenu.

Ces clients mettent également en cache le contenu. Les autres clients du même sous-réseau n’ont pas à télécharger le contenu à partir du point de distribution. Le contenu est distribué sur plusieurs clients, en vue de transferts futurs.  


### <a name="requirements-to-support-branchcache-with-configuration-manager"></a>Exigences pour prendre en charge BranchCache avec Configuration Manager

#### <a name="configure-distribution-points"></a>Configurer les points de distribution
Ajoutez la fonctionnalité **Windows BranchCache** au serveur de système de site configuré en tant que point de distribution.    
- Les points de distribution sur les serveurs configurés pour prendre en charge BranchCache ne nécessitent aucune configuration supplémentaire.   
- Vous ne pouvez pas ajouter Windows BranchCache à un point de distribution cloud. Les points de distribution cloud prennent en charge le téléchargement de contenu par les clients configurés pour Windows BranchCache.  

#### <a name="configure-clients"></a>Configurer des clients    
- Les clients pouvant prendre en charge BranchCache doivent être configurés pour le mode de cache distribué de BranchCache.  
- Le paramètre de système d’exploitation pour les paramètres de client BITS doit être activé afin de permettre la prise en charge de BranchCache.  

Pour plus d’informations, consultez [Configurer les clients pour BranchCache](https://docs.microsoft.com/windows/deployment/update/waas-branchcache#configure-clients-for-branchcache) dans la documentation Windows.


### <a name="configuration-manager-supported-os-versions-with-windows-branchcache"></a>Versions de système d’exploitation prises en charge par Configuration Manager avec Windows BranchCache

|Système&nbsp;d’exploitation|Détails de la prise en charge|  
|----------------------|---------------------|  
|Windows 7 avec SP1|Pris en charge par défaut|  
|Windows 8|Pris en charge par défaut|  
|Windows 8.1|Pris en charge par défaut|  
|Windows 10|Pris en charge par défaut|  
|Windows Server 2008 avec SP2|**Nécessite BITS 4.0** : installez BITS 4.0 sur les clients Configuration Manager à l’aide des mises à jour logicielles ou de la distribution de logiciels. Pour plus d’informations, consultez [Windows Management Framework](https://support.microsoft.com/help/968929/windows-management-framework-windows-powershell-2-0-winrm-2-0-and-bits).<br /><br /> Sur ce système d’exploitation, la fonctionnalité de client BranchCache n’est pas prise en charge pour la distribution de logiciels exécutée à partir du réseau ou pour les transferts de fichiers SMB. De plus, ce système d’exploitation ne peut pas utiliser la fonctionnalité BranchCache avec des points de distribution cloud.|  
|Windows Server 2008 R2|Pris en charge par défaut|  
|Windows Server 2012|Pris en charge par défaut|  
|Windows Server 2012 R2|Pris en charge par défaut|  
|Windows Server 2016|Pris en charge par défaut|  

Pour plus d’informations, consultez [BranchCache pour Windows](https://docs.microsoft.com/windows-server/networking/branchcache/branchcache) dans la documentation de Windows Server.  



##  <a name="bkmk_Workgroups"></a> Ordinateurs dans des groupes de travail  

Configuration Manager prend en charge les clients dans des groupes de travail.  

- Configuration Manager prend en charge le déplacement d’un client depuis un groupe de travail vers un domaine, et inversement. Pour plus d’informations, consultez [Guide pratique pour installer des clients Configuration Manager sur des ordinateurs de groupe de travail](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientWorkgroup).  

> [!NOTE]  
>  Bien que les clients des groupes de travail soient pris en charge, tous les systèmes de site doivent être membres d’un domaine Active Directory pris en charge.  



##  <a name="bkmmk_datadedup"></a> Déduplication des données  

Configuration Manager prend en charge l’utilisation de la déduplication des données avec des points de distribution sur les systèmes d’exploitation suivants :  

-   Windows Server 2016
-   Windows Server 2012 R2  
-   Windows Server 2012  


> [!IMPORTANT]  
>  Le volume qui héberge les fichiers sources du package ne peut pas être marqué pour la déduplication des données. Cette limitation est due au fait que la déduplication des données utilise des points d’analyse. Configuration Manager ne prend pas en charge l’utilisation d’un emplacement source de contenu avec des fichiers stockés sur des points d’analyse.  

Pour plus d’informations, consultez [Points de distribution Configuration Manager et déduplication des données de Windows Server 2012](https://cloudblogs.microsoft.com/enterprisemobility/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication/) sur le blog de l’équipe Configuration Manager et [Vue d’ensemble de la déduplication des données](https://docs.microsoft.com/windows-server/storage/data-deduplication/overview) dans la documentation de Windows Server.  



##  <a name="bkmk_DA"></a> DirectAccess  

Configuration Manager prend en charge la fonctionnalité DirectAccess pour la communication entre les clients et les systèmes de serveur de site.  

- Quand toutes les exigences pour DirectAccess sont satisfaites, ce dernier permet aux clients Configuration Manager sur Internet de communiquer avec le site qui leur est affecté comme s’ils étaient sur l’intranet.  

- Pour les actions lancées par le serveur, comme le contrôle à distance et l’installation Push du client, l’ordinateur qui initialise l’action doit exécuter IPv6. Ce protocole doit être pris en charge sur tous les périphériques réseau qui interviennent.  

Configuration Manager ne prend pas en charge les fonctionnalités suivantes sur DirectAccess :  

-   Déploiement de système d’exploitation   

-   Communication entre les sites Configuration Manager  

-   Communication entre les serveurs de système de site Configuration Manager au sein d’un site  



##  <a name="bkmk_dualboot"></a> Ordinateurs à double démarrage  

Configuration Manager ne peut pas gérer plusieurs systèmes d’exploitation sur un seul ordinateur. S’il existe plusieurs systèmes d’exploitation sur un ordinateur à gérer, configurez les méthodes de découverte et d’installation du client du site pour garantir que le client Configuration Manager est installé uniquement sur le système d’exploitation à gérer.  



##  <a name="bkmk_IPv6"></a> IPv6  

En plus du protocole IPv4 (Internet Protocol version 4), Configuration Manager prend en charge IPv6 (Internet Protocol version 6) avec les exceptions suivantes :  

|Fonction| Exception à la prise en charge IPv6|  
|--------------|-------------------------------|  
|Points de distribution cloud|IPv4 est requis pour prendre en charge Microsoft Azure et les points de distribution cloud.|  
|Passerelle de gestion cloud|IPv4 est exigé pour prendre en charge Microsoft Azure et la passerelle de gestion cloud.|  
|Appareils mobiles inscrits par Microsoft Intune et le connecteur de service Microsoft|IPv4 est requis pour prendre en charge les appareils mobiles inscrits par Microsoft Intune et le connecteur de service Microsoft.|  
|Découverte du réseau|IPv4 est requis lorsque vous configurez un serveur DHCP pour effectuer une recherche dans la découverte du réseau.|  
|Déploiement de système d’exploitation|Dans la version 1802 et les versions antérieures, IPv4 est nécessaire pour permettre la prise en charge du déploiement du système d’exploitation.  </br> </br> À partir de la version 1806, activez un répondeur PXE sur un point de distribution sans utiliser les Services de déploiement Windows. Ce nouveau service de répondeur PXE prend en charge IPv6. D’autres aspects liés à la fonctionnalité de déploiement du système d’exploitation, par exemple la capture ou la définition d’adresses IP statiques durant la séquence de tâches, nécessitent toujours IPv4. |  
|Communication avec le proxy de mise en éveil à distance|IPv4 est requis pour prendre en charge les paquets de proxy de mise en éveil du client.|  
|Windows CE|IPv4 est requis pour prendre en charge le client Configuration Manager sur les appareils Windows CE.|  



##  <a name="bkmk_NAT"></a> Traduction d’adresses réseau  

La fonctionnalité NAT (traduction d’adresses réseau) n’est pas prise en charge dans Configuration Manager, à moins que le site ne prenne en charge les clients situés sur Internet, et que les clients détectent qu’ils sont connectés à Internet. Pour plus d’informations sur la gestion du client basée sur Internet, consultez [Planifier la gestion des clients Internet](/sccm/core/clients/deploy/plan/plan-for-managing-internet-based-clients).  



##  <a name="bkmk_storage"></a> Technologie de stockage spécialisée  

Configuration Manager fonctionne avec tout matériel certifié dans la liste de compatibilité matérielle Windows pour la version du système d’exploitation sur laquelle le composant Configuration Manager est installé.

Les rôles de serveur de site exigent NTFS afin que Configuration Manager puisse définir des autorisations sur les répertoires et les fichiers. Configuration Manager suppose qu’il a la propriété complète d’un lecteur logique. Les systèmes de site qui s’exécutent sur des ordinateurs distincts ne peuvent pas partager une partition logique sur une technologie de stockage, quelle qu’elle soit. Cependant, chaque ordinateur peut utiliser une partition logique distincte sur la même partition physique d'un dispositif de stockage partagé.  

### <a name="support-considerations"></a>Considérations relatives à la prise en charge

- **Réseau de zone de stockage** : un SAN (réseau de zone de stockage) est pris en charge quand un serveur Windows pris en charge est attaché directement au volume hébergé par le SAN.  

- **SIS (Single-Instance-Store)**  : Configuration Manager ne prend pas en charge la configuration des dossiers de signatures et de packages de points de distribution sur un volume SIS.  

     De plus, le cache d’un client Configuration Manager n’est pas pris en charge sur un volume SIS.  

- **Lecteur de disque amovible** : Configuration Manager ne prend pas en charge l’installation de systèmes de site ou de clients Configuration Manager sur un lecteur de disque amovible.  
