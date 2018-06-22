---
title: Taille et échelle
titleSuffix: Configuration Manager
description: Déterminez le nombre de rôles de système de site et de sites dont vous avez besoin pour prendre en charge les appareils dans votre environnement.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5a42100-2f60-4952-b495-918025ea6559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b995687e330fe4beca26da83ee29ddc504c38e3a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343930"
---
# <a name="size-and-scale-numbers-for-system-center-configuration-manager"></a>Taille et échelle de System Center Configuration Manager en chiffres

*S’applique à : System Center Configuration Manager (Current Branch)*



Chaque déploiement de Configuration Manager comporte un nombre maximal de sites, de rôles de système de site et d’appareils qu’il peut prendre en charge. Ces nombres varient selon votre structure hiérarchique, les types et nombres de sites que vous utilisez et les rôles de système de site que vous déployez. Les informations contenues dans cet article peuvent vous aider à déterminer le nombre de rôles de système de site et de sites dont vous avez besoin pour prendre en charge les appareils que vous envisagez de gérer.

Utilisez les informations de cette rubrique ainsi que celles contenues dans les articles suivants :
-   [Matériel recommandé](../../../core/plan-design/configs/recommended-hardware.md)
-   [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
-   [Systèmes d’exploitation pris en charge pour les clients et appareils](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)
-   [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)


Ces nombres sont basés sur l’utilisation du matériel recommandé pour Configuration Manager. Ils sont également basés sur les paramètres par défaut de toutes les fonctionnalités Configuration Manager disponibles. Quand vous n’utilisez pas le matériel recommandé ou que vous utilisez des paramètres personnalisés plus stricts, les performances des systèmes de site peuvent se dégrader. Les systèmes de site peuvent ne pas atteindre les niveaux de prise en charge indiqués. (Procéder à l’inventaire matériel ou logiciel plus d’une fois tous les 7 jours, ce qui est la valeur par défaut, constitue un exemple de paramètres clients plus stricts.)

##  <a name="bkmk_SiteSystemScale"></a> Types de sites  

### <a name="central-administration-site"></a>Site d'administration centrale  

-   Un site d’administration centrale peut prendre en charge jusqu’à 25 sites principaux enfants.  


### <a name="primary-site"></a>Site principal  

-   Chaque site principal prend en charge jusqu’à 250 sites secondaires.  

-   Le nombre de sites secondaires par site principal est basé sur des connexions réseau WAN continues et fiables. Pour les emplacements de moins de 500 clients, envisagez à un point de distribution au lieu d'un site secondaire.  

 Pour plus d’informations sur le nombre de clients et d’appareils qu’un site principal peut prendre en charge, consultez [Nombres de clients pour les hiérarchies et les sites](#bkmk_clientnumbers).  


### <a name="secondary-site"></a>Site secondaire  

-   Les sites secondaires ne prennent pas en charge les sites enfants.  



## <a name="bkmk_roles"></a> Rôles système de site    


### <a name="application-catalog-web-service-point"></a>Point de service web du catalogue des applications  

-   Vous pouvez installer plusieurs instances du point de service web du catalogue d'applications sur des sites principaux.  

    > [!TIP]  
    >  Comme bonne pratique, installez le point du site web du catalogue d'applications et le point de service web du catalogue d'applications sur le même système de site lorsque ces points fournissent le service aux clients Intranet.  

    -   Pour améliorer les performances, envisagez prendre en charge jusqu'à 50 000 clients par instance.  

    -   Chaque instance de ce rôle de système de site prend en charge le nombre maximal de clients pris en charge par la hiérarchie.  


### <a name="application-catalog-website-point"></a>Point du site web du catalogue des applications  

-   Vous pouvez installer plusieurs instances du point de site Web du catalogue d'applications sur des sites principaux.  

    > [!TIP]  
    >  Comme bonne pratique, installez le point du site web du catalogue d'applications et le point de service web du catalogue d'applications sur le même système de site lorsque ces points fournissent le service aux clients Intranet.  

    -   Pour améliorer les performances, envisagez prendre en charge jusqu'à 50 000 clients par instance.  

    -   Chaque instance de ce rôle de système de site prend en charge le nombre maximal de clients pris en charge par la hiérarchie.  


### <a name="bkmk_cmg"></a> Passerelle de gestion cloud

- Vous pouvez installer plusieurs instances de la passerelle de gestion cloud (CMG) sur des sites principaux ou sur le site d’administration centrale.  

    > [!Tip]  
    > Dans une hiérarchie, créez la passerelle de gestion cloud sur le site d’administration centrale.  

    - Une passerelle de gestion cloud prend en charge de une à 16 instances de machine virtuelle dans le service cloud Azure.  

    - Chaque instance de machine virtuelle de la passerelle de gestion cloud prend en charge 6 000 connexions clientes simultanées. Quand la passerelle de gestion cloud subit une charge élevée en raison d’un dépassement du nombre de clients pris en charge, elle gère néanmoins les requêtes, mais des délais sont possibles.  

Pour plus d’informations, consultez [Performances et échelle](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) de la passerelle de gestion cloud.


### <a name="cloud-management-gateway-connection-point"></a>Point de connexion de la passerelle de gestion cloud

- Vous pouvez installer plusieurs instances du point de connexion CMG sur des sites principaux.  

- Un point de connexion CMG peut prendre en charge une passerelle de gestion cloud avec jusqu’à quatre instances de machine virtuelle. Si la passerelle de gestion cloud compte plus de quatre instances de machine virtuelle, ajoutez un deuxième point de connexion CMG pour l’équilibrage de charge. Une passerelle de gestion cloud disposant de 16 instances de machine virtuelle doit être liée à quatre points de connexion CMG.

Pour plus d’informations, consultez [Performances et échelle](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#performance-and-scale) de la passerelle de gestion cloud.


### <a name="distribution-point"></a>Point de distribution  

-   Points de distribution par site :  

    -   Chaque site principal et chaque site secondaire prend en charge jusqu'à 250 points de distribution.  

    -   Chaque site principal et secondaire prend en charge jusqu’à 2 000 points de distribution supplémentaires configurés comme points de distribution d’extraction. **Par exemple**, un même site principal prend en charge 2 250 points de distribution quand 2 000 d’entre eux sont configurés comme points de distribution d’extraction.  

    -   Chaque point de distribution prend en charge jusqu'à 4 000 connexions de clients.  

    -   Un point de distribution d’extraction agit comme un client quand il accède au contenu d’un point de distribution source.  

-   Chaque site principal prend en charge un total combiné de 5 000 points de distribution maximum. Ce total inclut tous les points de distribution sur le site principal et tous les points de distribution qui appartiennent aux sites secondaires enfants du site principal.  

-   Chaque point de distribution prend en charge un total combiné allant jusqu'à 10 000 packages et applications.  

> [!WARNING]  
>  Le nombre réel de clients qu’un point de distribution peut prendre en charge dépend de la vitesse du réseau et de la configuration matérielle du serveur.  
>   
>  De la même façon, le nombre de points de distribution d’extraction qu’un point de distribution source peut prendre en charge dépend de la vitesse du réseau et de la configuration matérielle du point de distribution source. Mais ce nombre est également affecté par la quantité de contenu que vous avez déployé. En effet, contrairement aux clients qui accèdent généralement au contenu à des moments différents pendant un déploiement, tous les points de distribution d’extraction demandent du contenu en même temps. Ces derniers peuvent demander tout le contenu disponible, et pas seulement le contenu qui leur est applicable. Quand vous placez une charge de traitement élevée sur un point de distribution source, des retards imprévus peuvent se produire dans la distribution du contenu aux points de distribution cibles.  


### <a name="fallback-status-point"></a>Point d’état de secours  

-   Chaque point d'état de secours peut prendre en charge jusqu'à 100 000 clients.  


### <a name="management-point"></a>Point de gestion  

-   Chaque site principal prend en charge jusqu’à 15 points de gestion.  

    > [!TIP]  
    >  N’installez pas de point de gestion sur des serveurs qui se trouvent sur une liaison lente à partir du serveur de site principal ou du serveur de bases de données du site.  

-   Chaque site secondaire prend en charge un seul point de gestion qui doit être installé sur le serveur de site secondaire.  

 Pour plus d’informations sur le nombre de clients et d’appareils qu’un point de gestion peut prendre en charge, consultez la section [Points de gestion](#bkmk_mp).  


### <a name="software-update-point"></a>Point de mise à jour logicielle  

-   Un point de mise à jour logicielle installé sur le serveur de site peut prendre en charge jusqu'à 25 000 clients.   

-   Un point de mise à jour logicielle distant du serveur de site peut prendre en charge jusqu’à 150 000 clients quand l’ordinateur distant répond à la configuration requise de WSUS (Windows Server Update Services) consistant à prendre en charge ce nombre de clients.  

-   Par défaut, Configuration Manager ne prend pas en charge la configuration de points de mise à jour logicielle comme clusters d’équilibrage de la charge réseau (NLB). Toutefois, vous pouvez utiliser le kit SDK Configuration Manager pour configurer jusqu’à quatre points de mise à jour logicielle sur un cluster NLB.  



##  <a name="bkmk_clientnumbers"></a> Nombres de clients pour les hiérarchies et les sites  
 Utilisez les informations suivantes pour déterminer le nombre de clients et leurs types que vous pouvez prendre en charge sur un site ou dans une hiérarchie.  


###  <a name="bkmk_cas"></a> Hiérarchie avec un site d’administration centrale  
Un site d’administration centrale prend en charge un nombre total d’appareils pouvant atteindre le nombre d’appareils répertoriés pour les trois groupes suivants :  

-   700 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX). Consultez également la prise en charge des [appareils embarqués](#embedded).

-   25 000 appareils exécutant Mac et Windows CE 7.0  

-   L’un des nombres suivants, selon la manière dont votre déploiement prend en charge la gestion des appareils mobiles :  

    -   100 000 appareils que vous gérez à l’aide de la gestion MDM locale  

    -   300 000 appareils cloud  

 Par exemple, dans une hiérarchie, vous pouvez prendre en charge 700 000 ordinateurs de bureau, jusqu’à 25 000 appareils Mac et Windows CE 7.0, et jusqu’à 300 000 appareils cloud quand vous intégrez Microsoft Intune. Cette hiérarchie prend en charge un total de 1 025 000 appareils. Si vous prenez en charge des appareils gérés par la gestion MDM locale, cette hiérarchie totalise 825 000 appareils.  

> [!IMPORTANT]  
>  Une hiérarchie où le site d’administration centrale utilise une édition Standard de SQL Server prend en charge un maximum de 50 000 ordinateurs de bureau et appareils. Pour prendre en charge plus de 50 000 postes de travail et appareils, vous devez utiliser une édition Entreprise de SQL Server. Cette exigence s’applique uniquement à un site d’administration centrale. Elle ne s’applique pas à un site principal autonome ou à un site principal enfant. L’édition de SQL Server que vous utilisez pour un site principal ne limite pas sa capacité pour prendre en charge le nombre indiqué de clients.   


 L’édition de SQL Server utilisée sur un site principal autonome ne limite pas la capacité du site consistant à prendre en charge au maximum le nombre indiqué de clients.  


###  <a name="bkmk_chipri"></a> Site principal enfant  
Chaque site principal enfant d’une hiérarchie disposant d’un site d’administration centrale prend en charge le nombre de clients suivant :  

-   Un total de 150 000 clients et appareils, non limités à un groupe ou à un type spécifiques, à condition que la prise en charge ne dépasse pas le nombre pris en charge par la hiérarchie. Consultez également la prise en charge des [appareils embarqués](#embedded).

Par exemple, un site principal prend en charge 25 000 appareils Mac et Windows CE 7.0. Ce nombre est la limite d’une hiérarchie. Ce site principal peut alors prendre en charge 125 000 ordinateurs de bureau supplémentaires. Le nombre total d’appareils pris en charge pour le site principal enfant est la limite maximale de 150 000 prise en charge.


###  <a name="bkmk_pri"></a> Site principal autonome  
Un site principal autonome prend en charge le nombre suivant d’appareils :  

-   Total de 175 000 clients et appareils, sans dépasser :  

    -   150 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX). Consultez également la prise en charge des [appareils embarqués](#embedded).

    -   25 000 appareils exécutant Mac et Windows CE 7.0

    -   L’un des nombres d’éléments suivants, selon la manière dont votre déploiement prend en charge la gestion des appareils mobiles :  

        -   50 000 appareils que vous gérez à l’aide de la gestion MDM locale  

        -   150 000 appareils cloud  


Par exemple, un site principal autonome prenant en charge 150 000 ordinateurs de bureau et 10 000 clients Mac ou Windows CE 7.0 ne peut prendre en charge que 15 000 appareils supplémentaires. Ces appareils peuvent être basés sur le cloud ou gérés à l’aide de la gestion MDM locale.  


### <a name="embedded"></a>Sites principaux et appareils Windows Embedded
Les sites principaux prennent en charge les appareils embarqués Windows Embedded où les filtres d'écriture basés sur des fichiers (FBWF) sont activés. Quand des appareils embarqués ne disposent pas de filtres d’écriture activés, un site principal peut prendre en charge un nombre d’appareils embarqués pouvant atteindre le nombre autorisé d’appareils pour ce site. Du nombre total des appareils qu’un site principal prend en charge, un maximum de 10 000 de ceux-ci peuvent être des appareils Windows Embedded. Ces appareils doivent être configurés pour les exceptions listées dans la Remarque importante se trouvant dans [Planification du déploiement de clients sur des appareils Windows Embedded](/sccm/core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices). Un site principal prend en charge seulement 3 000 appareils Windows Embedded où EWF est activé et qui ne sont pas configurés pour les exceptions.


###  <a name="bkmk_sec"></a> Sites secondaires  
Les sites secondaires prennent en charge le nombre suivant d’appareils :  

-   15 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  


###  <a name="bkmk_mp"></a> Points de gestion  
Chaque point de gestion peut prendre en charge le nombre suivant d’appareils :  

-   Total de 25 000 clients et appareils, sans dépasser :  

    -   25 000 ordinateurs de bureau (exécutant Windows, Linux et UNIX)  

    -   L’un des nombres d’éléments suivants (pas les deux) :  

        -   10 000 appareils que vous gérez à l’aide de la gestion MDM locale  

        -   10 000 appareils exécutant des clients Mac et Windows CE 7.0
