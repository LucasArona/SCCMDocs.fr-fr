---
title: Domaines Active Directory pris en charge
titleSuffix: Configuration Manager
description: Prenez connaissance de la configuration requise pour l’appartenance d’un système de site System Center Configuration Manager à un domaine Active Directory.
ms.date: 9/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02353e516e7af45afe273bc0deff5b227a7c7f2c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499436"
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>Domaines Active Directory pris en charge pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Tous les systèmes de site System Center Configuration Manager doivent être membres d’un domaine Windows Server Active Directory pris en charge. Les ordinateurs clients Configuration Manager peuvent être membres du domaine ou membres d’un groupe de travail.  

 **Configuration requise et limitations :**  

-   L’appartenance à un domaine s’applique à des systèmes de site prenant en charge la gestion du client basée sur Internet dans un réseau de périmètre (également appelé DMZ, zone démilitarisée et sous-réseau filtré).  

-   Cela ne permet pas de modifier les paramètres suivants pour un ordinateur qui héberge un rôle de système de site :  

    -   Appartenance au domaine *(y compris suppression d’un système de site du domaine et rattachement au même domaine)*

    -   Nom du domaine  

    -   Nom de l'ordinateur  

Vous devez désinstaller le rôle de système de site (y compris le site s’il s’agit d’un serveur de site) avant d’apporter ces modifications.  

**Les domaines avec les niveaux fonctionnels de domaine suivants sont pris en charge :**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> Espace de noms disjoint  
Configuration Manager prend en charge l’installation de systèmes de site et de clients dans un domaine qui a un espace de noms disjoint.  

Dans un scénario d’espace de noms disjoint, le suffixe du DNS principal d’un ordinateur ne correspond pas au nom de domaine DNS Active Directory où se trouve cet ordinateur. L’ordinateur qui utilise le suffixe DNS principal qui ne correspond pas est dit « disjoint ». Un autre scénario d’espace de noms disjoint se produit si le nom de domaine NetBIOS d’un contrôleur de domaine ne correspond pas au nom de domaine DNS Active Directory.  

Le tableau suivant identifie les scénarios pris en charge pour un espace de noms disjoint.  

|Scénario|Informations complémentaires|  
|--------------|----------------------|  
|**Scénario 1 :**<br /><br /> Le suffixe DNS principal du contrôleur de domaine diffère du nom de domaine DNS d'Active Directory. Les ordinateurs qui sont membres du domaine peuvent être disjoints ou non disjoints.|Dans ce scénario, le suffixe DNS principal du contrôleur de domaine diffère du nom de domaine DNS d'Active Directory. Le contrôleur de domaine est disjoint dans ce scénario. Les ordinateurs qui sont membres du domaine, comme les serveurs et les ordinateurs de site, peuvent avoir un suffixe DNS principal qui correspond soit au suffixe DNS principal du contrôleur de domaine ou au nom de domaine DNS d'Active Directory.|  
|**Scénario 2 :**<br /><br /> Un ordinateur membre d'un domaine Active Directory est disjoint, même si le contrôleur de domaine n'est pas disjoint.|Dans ce scénario, le suffixe DNS principal d'un ordinateur membre sur lequel un système de site est installé diffère du nom de domaine DNS d'Active Directory, même si le suffixe DNS principal du contrôleur de domaine est le même que le nom de domaine DNS d'Active Directory. Dans ce scénario, un contrôleur de domaine n'est pas disjoint et un ordinateur membre est disjoint. Les ordinateurs membres qui exécutent le client Configuration Manager peuvent posséder un suffixe DNS principal qui correspond soit au suffixe DNS principal du serveur du système de site disjoint, soit au nom de domaine DNS d’Active Directory.|  

 Pour permettre à un ordinateur d'accéder à des contrôleurs de domaine disjoints, vous devez changer l'attribut d'Active Directory **msDS-AllowedDNSSuffixes** sur le conteneur d'objets du domaine. Vous devez ajouter les deux suffixes DNS à l'attribut.  

 De plus, pour vérifier que la liste de recherche des suffixes DNS contient tous les espaces de noms DNS déployés au sein de l’organisation, vous devez configurer la liste de recherche pour chaque ordinateur du domaine disjoint. Vérifiez que vous incluez ce qui suit dans la liste d’espaces de noms : le suffixe DNS principal du contrôleur de domaine, le nom de domaine DNS et tous les espaces de noms supplémentaires d’autres serveurs avec lesquels Configuration Manager peut interagir. Vous pouvez utiliser la console de Gestion de stratégie de groupe pour configurer la liste de **Recherche de suffixe de nom de domaine (DNS)** .  

> [!IMPORTANT]  
>  Lorsque vous référencez un ordinateur dans Configuration Manager, entrez-le à l’aide de son suffixe DNS principal. Ce suffixe doit correspondre au nom de domaine complet inscrit comme attribut **dnsHostName** dans le domaine Active Directory et au nom de principal du service associé au système.  

##  <a name="bkmk_SLD"></a> Noms de domaine en une seule partie  
 Configuration Manager prend en charge les systèmes de site et les clients dans un nom domaine en une seule partie quand les critères suivants sont remplis :  

-   Le nom de domaine en une seule partie dans les services de domaine Active Directory doit être configuré avec un espace de noms DNS disjoint associé à un domaine de niveau supérieur valide.  

     **Exemple** : Le nom de domaine en une seule partie Contoso est configuré pour avoir un espace de noms disjoint contoso.com dans DNS. Ainsi, quand vous spécifiez le suffixe DNS dans Configuration Manager pour un ordinateur du domaine Contoso, vous spécifiez « Contoso.com » et non pas « Contoso ».  

-   Les connexions DCOM (Distributed Component Object Model) entre serveurs de site dans le contexte système doivent être établies avec l’authentification Kerberos.  
