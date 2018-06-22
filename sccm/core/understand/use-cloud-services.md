---
title: Utiliser des services cloud pour compléter l’infrastructure locale
titleSuffix: Configuration Manager
description: Configurer des ressources cloud pour System Center Configuration Manager afin de compléter votre infrastructure locale.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24fca61e-9cdb-447a-ad7a-f4d2e4fd6704
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 07eb6ec88a5f9b9f7985c317813b2ef7dd5534ff
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344702"
---
# <a name="use-cloud-services-with-system-center-configuration-manager"></a>Utiliser des services cloud avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager prend en charge plusieurs options de cloud. Celles-ci peuvent compléter votre infrastructure locale et vous aider à résoudre certains problèmes d’entreprise comme :  

-   Gérer les appareils BYOD (en utilisant Intune pour gérer les appareils mobiles).  

-   Fournir des ressources de contenu à des clients isolés ou des ressources de l’intranet à l’extérieur de votre pare-feu d’entreprise (en utilisant des points de distribution cloud).  

-   Monter en charge l’infrastructure quand le matériel physique n’est pas disponible ou n’est pas placé de façon logique pour répondre à vos besoins (en utilisant des machines virtuelles Microsoft Azure).  

La configuration de ressources cloud n’est pas indispensable avant de déployer Configuration Manager, mais il peut être utile de comprendre ces options avant d’aller plus en avant dans un plan de conception de hiérarchie. L’utilisation de ressources cloud peut vous faire gagner du temps et économiser de l’argent, mais aussi résoudre des problèmes qu’une infrastructure locale ne peut pas résoudre.  

## <a name="cloud-based-resources-you-can-use-with-configuration-manager"></a>Ressources cloud que vous pouvez utiliser avec Configuration Manager  
 Chaque option présente des conditions d’utilisation différentes. Vous devez donc étudier plus en détail les conditions préalables, les limitations et les coûts supplémentaires possibles selon le niveau d’utilisation pour chacune des options.  

-   Pour plus d'informations sur les points de distribution cloud, voir [Installer des points de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure).

-   Pour plus d’informations sur Azure, consultez [Azure](http://go.microsoft.com/fwlink/p/?LinkId=262965) dans la bibliothèque MSDN.  

### <a name="azure-virtual-machines-for-cloud-based-infrastructure"></a>Machines virtuelles Azure (pour infrastructure cloud)  
 Configuration Manager prend en charge l’utilisation d’ordinateurs qui s’exécutent en tant que machines virtuelles Azure, de la même manière que les ordinateurs qui s’exécutent localement dans votre réseau physique d’entreprise. Vous pouvez utiliser des machines virtuelles Azure dans les scénarios suivants :  

-   **Scénario 1** : vous pouvez exécuter Configuration Manager sur une machine virtuelle et l’utiliser pour gérer des clients installés sur d’autres machines virtuelles.  

-   **Scénario 2** : vous pouvez exécuter Configuration Manager sur une machine virtuelle et l’utiliser pour gérer des clients qui ne s’exécutent pas dans Azure.  

-   **Scénario 3** : vous pouvez exécuter différents rôles de système de site Configuration Manager sur des machines virtuelles, tout en exécutant d’autres rôles sur votre réseau physique d’entreprise (avec une connectivité réseau appropriée pour les communications).  

Les exigences en matière de réseaux, de systèmes d’exploitation et de matériel qui s’appliquent à l’installation de Configuration Manager sur votre réseau physique d’entreprise s’appliquent également à l’installation de Configuration Manager dans Azure.  

Un abonnement Azure est requis pour utiliser les machines virtuelles Azure. Vous occasionnez des frais en fonction du nombre et de la configuration de vos machines virtuelles, et du niveau d’utilisation des ressources cloud.  

En outre, les sites et les clients Configuration Manager qui s’exécutent sur des machines virtuelles Azure sont soumis aux mêmes exigences de licence que les installations locales.  

### <a name="azure-services-for-cloud-based-distribution-points"></a>Services Azure (pour les points de distribution cloud)  
 Vous pouvez utiliser un service Azure pour héberger un point de distribution Configuration Manager, appelé point de distribution cloud. Vous pouvez [utiliser un point de distribution cloud avec System Center Configuration Manager](../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) en même temps que des points de distribution locaux et des points de distribution déployés sur des machines virtuelles Azure.  

 Cela diffère de l’utilisation d’une machine virtuelle Azure sur laquelle vous déployez un rôle de système de site. Points de distribution cloud :  

-   Ils s’exécutent en tant que service dans Azure, et non sur une machine virtuelle.  

-   Ils sont mis automatiquement à l’échelle pour répondre à l’augmentation des demandes de contenu des clients.  

-   Ils prennent en charge les clients sur Internet et l’intranet.  

Un abonnement Azure est requis pour utiliser Azure afin d’héberger des points de distribution. Les frais dépendent de la quantité de données qui circule vers et depuis le service.  

### <a name="microsoft-intune-for-mobile-device-management"></a>Microsoft Intune (pour gestion des appareils mobiles)  
 Vous pouvez intégrer votre abonnement Microsoft Intune avec Configuration Manager pour permettre la gestion des appareils à l’aide du service Intune. Cette intégration présente les caractéristiques suivantes :  

-   Il s’agit d’une configuration hybride qui étend Configuration Manager (ou Intune selon votre perspective) pour prendre en charge une grande variété d’appareils.  

-   Elle requiert le rôle de système de site Connecteur Microsoft Intune.  

-   Elle nécessite que vous disposiez d’un abonnement Intune distinct avec des licences suffisantes pour les appareils que vous voulez gérer avec Intune.  

Même si Intune utilise Azure, vous n’êtes pas tenu de configurer Azure de façon indépendante, et vous ne vous exposez pas à des coûts en supplément de ceux de l’abonnement Intune.  

### <a name="additional-configuration-manager-capabilities"></a>Fonctionnalités supplémentaires de Configuration Manager  
 Certaines fonctionnalités de Configuration Manager peuvent se connecter à des services cloud, par exemple :  

-   Windows Server Update Services (WSUS).  

-   Le service cloud Configuration Manager, pour télécharger les mises à jour de Configuration Manager.  

Ces fonctions supplémentaires ne nécessitent pas d’avoir un abonnement Azure. Vous n’êtes pas tenu de configurer des connexions, des certificats ou des services spécifiques dans le cloud. En effet, ces fonctionnalités sont automatiquement gérées par Configuration Manager à votre place. Vous devez seulement veiller à ce que les systèmes de site et les appareils puissent accéder aux URL Internet.  

##  <a name="BKMK_CloudSec"></a> Sécurité des services cloud  
 Configuration Manager utilise des certificats pour configurer votre contenu dans Azure et y accéder, et pour gérer les services que vous utilisez. Configuration Manager chiffre les données que vous stockez dans Microsoft Azure, mais n’introduit pas de contrôles de données ou de sécurité en plus de ceux fournis par Microsoft Azure.  

 Pour plus d’informations, consultez les détails des différents scénarios de ressources cloud. Vous pouvez également consulter les rubriques suivantes sur la sécurité dans Azure :  

-   [Azure : Présentation de la gestion des comptes de sécurité dans Azure](http://go.microsoft.com/fwlink/p/?LinkId=262968)  

-   [Azure Security Overview (Présentation des fonctionnalités de sécurité Azure)](http://go.microsoft.com/fwlink/p/?LinkId=262970)  

-   [Get Past the Security Crossroads in Your Cloud Migration (Franchir les barrières de sécurité dans le cadre d'une migration vers le cloud)](http://go.microsoft.com/fwlink/p/?LinkId=262971)  

-   [La sécurité des données avec Azure - partie 1 sur 2](http://go.microsoft.com/fwlink/p/?LinkId=262974)  
