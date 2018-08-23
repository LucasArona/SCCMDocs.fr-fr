---
title: Conditions requises de l’infrastructure OSD
titleSuffix: Configuration Manager
description: Découvrez les dépendances internes et externes au produit, et la configuration requise, pour un déploiement de système d’exploitation dans Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e54c6c7d8f827a17c69f4e166aeb4dccca4272f
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39382916"
---
# <a name="infrastructure-requirements-for-os-deployment-in-configuration-manager"></a>Configuration de l’infrastructure requise pour un déploiement de système d’exploitation dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements de système d’exploitation dans Configuration Manager présentent des dépendances externes et des dépendances au sein du produit. Utilisez cet article pour vous aider à préparer l’infrastructure d’un déploiement de système d’exploitation.  



##  <a name="BKMK_ExternalDependencies"></a> Dépendances externes à Configuration Manager  

Cette section fournit des informations sur les outils externes, les kits d’installation et les versions de système d’exploitation nécessaires au déploiement des systèmes d’exploitation dans Configuration Manager.  

### <a name="windows-adk-for-windows-10"></a>Windows ADK pour Windows 10  

Windows ADK (Assessment and Deployment Kit) regroupe des outils et de la documentation permettant de configurer et de déployer Windows. Configuration Manager utilise Windows ADK pour automatiser des actions telles que l’installation de Windows, la capture des images et la migration des données et des profils utilisateur.  

Les fonctionnalités suivantes de Windows ADK doivent être installées sur le serveur de site du site de niveau supérieur de la hiérarchie, sur le serveur de site de chaque site principal de la hiérarchie et sur le serveur de système de site du fournisseur SMS :  

-   Outil de migration de l'état utilisateur (USMT) <sup>1</sup>  

-   Outils de déploiement Windows  

-   Environnement de préinstallation Windows (Windows PE)  

Pour obtenir la liste des versions du kit Windows 10 ADK que vous pouvez utiliser avec différentes versions de Configuration Manager, consultez [Prise en charge de Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

 <sup>1</sup> USMT n'est pas obligatoire sur le serveur de système de site du fournisseur SMS.  

> [!NOTE]  
>  Vous devez installer manuellement Windows ADK sur chaque serveur de site avant d’installer le site Configuration Manager.  

Pour plus d’informations, consultez les articles suivants :  

- [Windows ADK pour les scénarios Windows 10 pour les informaticiens](https://docs.microsoft.com/windows/deployment/windows-adk-scenarios-for-it-pros)  

- [Télécharger le kit Windows ADK pour Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install)  

- [Prise en charge pour Windows 10](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>Outil de migration de l'état utilisateur (USMT)  

Configuration Manager utilise un package USMT qui contient les fichiers sources USMT 10 pour capturer et restaurer l’état utilisateur lors du déploiement de votre système d’exploitation. Quand le programme d’installation de Configuration Manager est exécuté sur le site de niveau supérieur, il crée automatiquement le package USMT. USMT 10 capture l’état utilisateur de Windows 7, Windows 8, Windows 8.1 et Windows 10.  

Pour plus d’informations, consultez les articles suivants :  

- [Scénarios de migration courants pour USMT 10](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios)  

- [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state)  


### <a name="windows-pe"></a>Windows PE  

Windows PE est utilisé pour les images de démarrage pour démarrer un ordinateur. C’est une version de Windows avec des services limités, qui est utilisée au cours de la préinstallation et du déploiement de Windows. La liste suivante inclut les versions prises en charge de Windows ADK pour Configuration Manager, Current Branch :  

#### <a name="windows-adk-version"></a>Version de Windows ADK  
Windows ADK pour Windows 10. Pour plus d’informations, consultez [Prise en charge de Windows 10](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).

#### <a name="windows-pe-versions-for-boot-images-customizable-from-the-configuration-manager-console"></a>Versions de Windows PE pour les images de démarrage personnalisables à partir de la console Configuration Manager  
Windows PE 10  

#### <a name="supported-windows-pe-versions-for-boot-images-not-customizable-from-the-configuration-manager-console"></a>Versions de Windows PE prises en charge pour les images de démarrage non personnalisables à partir de la console Configuration Manager  
Windows PE 3.1<sup>1</sup> et Windows PE 5  

<sup>1</sup> Vous pouvez ajouter une image de démarrage à Configuration Manager uniquement si elle est basée sur Windows PE 3.1. Installez le supplément Windows AIK pour Windows 7 SP1 pour mettre à niveau Windows AIK pour Windows 7 (basé sur Windows PE 3) avec le supplément Windows AIK pour Windows 7 SP1 (basé sur Windows PE 3.1). Téléchargez le supplément Windows AIK pour Windows 7 SP1 à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

Par exemple, si vous utilisez Configuration Manager, vous pouvez personnaliser les images de démarrage de Windows ADK pour Windows 10 (basées sur Windows PE 10) depuis la console Configuration Manager. Toutefois, si les images de démarrage basées sur Windows PE 5 sont prises en charge, vous devez les personnaliser depuis un autre ordinateur et utiliser la version de DISM installée avec Windows ADK pour Windows 8. Ensuite, ajoutez l’image de démarrage à la console Configuration Manager. Pour plus d’informations sur la procédure à suivre pour personnaliser une image de démarrage (ajouter des composants et pilotes facultatifs), activer la prise en charge des commandes pour l’image de démarrage, ajouter l’image de démarrage à la console Configuration Manager et mettre à jour les points de distribution avec l’image de démarrage, consultez [Personnaliser les images de démarrage](/sccm/osd/get-started/customize-boot-images). Pour plus d’informations sur les images de démarrage, consultez [Gérer les images de démarrage](/sccm/osd/get-started/manage-boot-images).  


### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  

WSUS est obligatoire pour le point de mise à jour logicielle, lui-même nécessaire à l’installation des mises à jour logicielles lors du déploiement du système d’exploitation. Pour plus d’informations, consultez [Installer et configurer un point de mise à jour logicielle](/sccm/sum/get-started/install-a-software-update-point).


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>Internet Information Services (IIS) sur les serveurs de système de site  

IIS est nécessaire pour le point de distribution, le point de migration d’état et le point de gestion. Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  


### <a name="windows-deployment-services-wds"></a>Services de déploiement Windows (WDS)  

Dans la version 1802 ou antérieure, WDS est nécessaire pour les déploiements PXE. À partir de la version 1806, vous pouvez activer PXE sur un point de distribution sans WDS. Pour plus d’informations, consultez [Services de déploiement Windows](#BKMK_WDS) dans cet article. 


### <a name="dynamic-host-configuration-protocol-dhcp"></a>DHCP (Dynamic Host Configuration Protocol)  

DHCP est obligatoire dans le cadre des déploiements PXE. Pour pouvoir déployer des systèmes d'exploitation à l'aide de PXE, vous devez disposer d'un serveur DHCP fonctionnant correctement et disposant d'un hôte actif. Pour plus d’informations sur les déploiements PXE, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  


### <a name="supported-operating-systems-and-hard-disk-configurations"></a>Systèmes d'exploitation et configurations de disque dur pris en charge  

Pour plus d’informations sur les versions de système d’exploitation et les configurations de disque dur prises en charge par Configuration Manager quand vous déployez des systèmes d’exploitation, consultez [Systèmes d’exploitation pris en charge](#BKMK_SupportedOS) et [Configurations de disque prises en charge](#BKMK_SupportedDiskConfig).  


### <a name="windows-device-drivers"></a>Pilotes de périphérique Windows  

Vous pouvez utiliser les pilotes de périphérique Windows quand vous installez le système d’exploitation sur l’ordinateur de destination. Vous pouvez aussi les utiliser quand vous exécutez Windows PE dans une image de démarrage. Pour plus d’informations, consultez [Gérer les pilotes](/sccm/osd/get-started/manage-drivers).  



##  <a name="BKMK_InternalDependencies"></a> Dépendances internes à Configuration Manager  

Cette section fournit des informations sur les prérequis d’un déploiement de système d’exploitation Configuration Manager.  


### <a name="os-image"></a>image du système d'exploitation  

Les images de système d’exploitation dans Configuration Manager sont stockées dans le format de fichier WIM (Windows Imaging). Elles constituent une collection compressée de fichiers et de dossiers de référence. Ces images sont nécessaires pour installer et configurer un système d’exploitation sur un ordinateur. Pour plus d’informations, consultez [Gérer les images de système d’exploitation](/sccm/osd/get-started/manage-operating-system-images).  


### <a name="driver-catalog"></a>Catalogue de pilotes  

Pour déployer un pilote de périphérique, importez le pilote de périphérique, activez-le et rendez-le disponible sur un point de distribution auquel le client Configuration Manager a accès. Pour plus d’informations sur le catalogue de pilotes, consultez [Gérer les pilotes](/sccm/osd/get-started/manage-drivers).  


### <a name="management-point"></a>Point de gestion  

Les points de gestion transfèrent des informations entre les clients et le site Configuration Manager. Le client utilise un point de gestion pour exécuter la séquence de tâches permettant d’effectuer le déploiement du système d’exploitation. Pour plus d’informations sur les séquences de tâches, consultez [Considérations relatives à la planification de l’automatisation des tâches](/sccm/osd/plan-design/planning-considerations-for-automating-tasks).  


### <a name="distribution-point"></a>Point de distribution  

Des points de distribution sont utilisés dans la plupart des déploiements pour stocker les données qui servent à déployer un système d’exploitation, telles que les packages d’images ou de pilotes de périphérique. En général, les séquences de tâches récupèrent les données à partir d’un point de distribution pour déployer le système d’exploitation. Pour plus d’informations sur l’installation de points de distribution et sur la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


### <a name="pxe-enabled-distribution-point"></a>Point de distribution PXE  

Pour effectuer des déploiements lancés par PXE, configurez un point de distribution qui accepte les demandes PXE des clients. Pour plus d’informations, consultez [Configurer un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


### <a name="multicast-enabled-distribution-point"></a>Point de distribution multidiffusion  

Pour optimiser vos déploiements de système d’exploitation en utilisant la multidiffusion, configurez un point de distribution qui prend en charge la multidiffusion. Pour plus d’informations, consultez [Configurer un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-multicast).   


### <a name="state-migration-point"></a>Point de migration d’état  

Lorsque vous capturez et restaurez des données d’état utilisateur pour les déploiements côte à côte et d’actualisation, configurez un point de migration d’état qui stocke les données d’état utilisateur sur un autre ordinateur.  

Pour plus d’informations sur la configuration du point de migration d’état, consultez [Point de migration d’état](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_StateMigrationPoints).  

Pour plus d’informations sur la capture et la restauration de l’état utilisateur, consultez [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state).  


### <a name="reporting-services-point"></a>Point de Reporting Services  

Si vous voulez utiliser des rapports Configuration Manager pour les déploiements de système d’exploitation, installez et configurez un point de rapport. Pour plus d’informations, consultez [Création de rapports](/sccm/core/servers/manage/reporting).  


### <a name="security-permissions-for-os-deployments"></a>Autorisations de sécurité pour les déploiements de système d’exploitation  

Le rôle de sécurité **Gestionnaire de déploiement de systèmes d’exploitation** est un rôle prédéfini que vous ne pouvez pas changer. Toutefois, vous pouvez copier le rôle, y apporter des modifications et les enregistrer sous un nouveau rôle de sécurité personnalisé. Voici quelques-unes des autorisations qui s’appliquent directement aux déploiements de système d’exploitation :  

- **Package d’images de démarrage**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

- **Pilotes de périphériques**: Créer, Supprimer, Modifier, Modifier un dossier, Modifier le rapport, Déplacer un objet, Lire, Exécuter le rapport  

- **Package de pilotes**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

- **Image de système d’exploitation**: Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

- **Package de mise à niveau de système d’exploitation** : Créer, Supprimer, Modifier, Modifier un dossier, Déplacer un objet, Lire, Définir l’étendue de sécurité  

- **Package de séquences de tâches**: Créer, Créer un média de séquence de tâches, Supprimer, Modifier, Modifier un dossier, Modifier le rapport, Déplacer un objet, Lire, Exécuter le rapport, Définir l’étendue de sécurité  

Pour plus d’informations, consultez [Créer des rôles de sécurité personnalisés](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole).  


### <a name="security-scopes-for-os-deployments"></a>Étendues de sécurité pour les déploiements de système d’exploitation  

Utilisez des étendues de sécurité pour permettre aux utilisateurs administratifs d'accéder aux objets sécurisables utilisés dans les déploiements de système d’exploitation, tels que les images du système d’exploitation et de démarrage, les packages de pilotes et des packages de séquences de tâches. Pour plus d’informations, consultez [Sécurité et audit](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).  



##  <a name="BKMK_WDS"></a> Services de déploiement Windows  

Dans la version 1802 ou antérieure, WDS (Services de déploiement Windows) doit être installé sur le même serveur que les points de distribution que vous configurez pour prendre en charge PXE ou la multidiffusion. WDS est inclus dans le système d’exploitation du serveur. Pour les déploiements PXE, WDS est le service qui effectue le démarrage PXE. Lorsque le point de distribution est installé et activé pour PXE, Configuration Manager installe un fournisseur dans WDS qui utilise les fonctions de démarrage PXE de WDS.  

À partir de la version 1806, vous pouvez activer PXE sur un point de distribution sans WDS. Pour plus d’informations, consultez l’option **Enable a PXE responder without Windows Deployment Service** (Activer un répondeur PXE sans WDS) dans [Installer et configurer des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).


> [!NOTE]  
>  Si le serveur nécessite un redémarrage, l’installation de WDS peut échouer. 


### <a name="wds-requirements"></a>Configuration requise de WDS  

-   Pour installer WDS sur le serveur, l’administrateur doit être membre du groupe Administrateurs local.  

-   Le serveur WDS doit être membre d'un domaine Active Directory ou contrôleur de domaine d'un domaine Active Directory. Toutes les configurations de forêts et de domaines Windows prennent en charge WDS.  

-   Si le fournisseur est installé sur un serveur distant, installez WDS sur le serveur de site et le fournisseur distant.  


###  <a name="BKMK_WDSandDHCP"></a> Considérations quand vous avez WDS et DHCP sur le même serveur  

Si vous envisagez de cohéberger le point de distribution sur un serveur exécutant DHCP, tenez compte des exigences de configuration suivantes :  

-   Vous devez disposer d'un serveur DHCP opérationnel avec une étendue active. WDS utilise PXE qui exige un serveur DHCP.  

-   Un serveur DNS est requis pour exécuter WDS.  

-   Les ports UDP suivants doivent être ouverts sur le serveur WDS :  

    -   Port 67 (DHCP)  

    -   Port 69 (TFTP)  

    -   Port 4011 (PXE)  

    > [!NOTE]  
    >  Si une autorisation DHCP est nécessaire sur le serveur, vous devez ouvrir le port 68 du client DHCP sur le serveur.  

-   DHCP et WDS nécessitent le port numéro 67. Si vous hébergez à la fois WDS et DHCP, vous pouvez déplacer DHCP ou le point de distribution configuré pour PXE sur un autre serveur. Vous pouvez également suivre la procédure ci-dessous pour configurer le serveur WDS en vue d’écouter sur un autre port.  

#### <a name="to-configure-the-wds-server-to-listen-on-a-different-port"></a>Pour configurer le serveur WDS en vue d’écouter sur un autre port  

1.  Modifiez la clé de registre suivante :  

     `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE`  

2.  Définissez la valeur de Registre **UseDHCPPorts** sur **0**.  

3.  Pour que la nouvelle configuration prenne effet, exécutez la commande suivante sur le serveur :  

     `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  



##  <a name="BKMK_SupportedOS"></a> Systèmes d’exploitation pris en charge  

Tous les systèmes d’exploitation Windows répertoriés comme clients pris en charge dans [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sont pris en charge pour le déploiement de système d’exploitation.  



##  <a name="BKMK_SupportedDiskConfig"></a> Configurations de disque prises en charge  

Le tableau suivant présente les combinaisons de configurations de disque dur sur les ordinateurs de référence et de destination qui sont prises en charge pour le déploiement de système d’exploitation dans Configuration Manager :  

|Configuration de disque dur de l'ordinateur de référence|Configuration de disque dur de l'ordinateur de destination|  
|------------------------------------------------|--------------------------------------------------|  
|Disque de base|Disque de base|  
|Volume simple sur un disque dynamique|Volume simple sur un disque dynamique|  

Configuration Manager prend en charge la capture d’une image de système d’exploitation uniquement sur les ordinateurs configurés avec des volumes simples. Il n'existe pas de prise en charge pour les configurations de disque dur suivantes :  

-   Volumes fractionnés  

-   Volumes agrégés par bandes (RAID 0)  

-   Volumes en miroir (RAID 1)  

-   Volumes de parité (RAID 5)  

Le tableau suivant présente une configuration de disque dur supplémentaire sur les ordinateurs de référence et de destination qui n’est pas prise en charge avec le déploiement de système d’exploitation dans Configuration Manager.  

|Configuration de disque dur de l'ordinateur de référence|Configuration de disque dur de l'ordinateur de destination|  
|------------------------------------------------|--------------------------------------------------|  
|Disque de base|Disque dynamique|  



## <a name="next-steps"></a>Étapes suivantes

- [Préparer des rôles de système de site pour les déploiements de système d’exploitation](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments)
- [Préparer le déploiement du système d’exploitation](/sccm/osd/get-started/prepare-for-operating-system-deployment)
