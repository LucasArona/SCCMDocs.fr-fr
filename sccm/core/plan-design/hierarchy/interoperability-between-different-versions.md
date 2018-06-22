---
title: Interopérabilité entre versions
titleSuffix: Configuration Manager
description: Découvrez comment éviter les conflits entre les multiples hiérarchies System Center Configuration Manager sur le même réseau.
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 712007dd8892e28316f277326b2182e5fe945f7b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340265"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interopérabilité entre les différentes versions de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez installer et utiliser plusieurs hiérarchies indépendantes de System Center Configuration Manager sur le même réseau. Toutefois, étant donné que des hiérarchies différentes de Configuration Manager n’interagissent pas en dehors du processus de migration, chaque hiérarchie nécessite une configuration pour éviter des conflits. En outre, vous pouvez créer certaines configurations pour faciliter l’interaction des ressources que vous gérez avec les systèmes de site de la hiérarchie correcte.  

 Les sections suivantes fournissent des informations sur l'utilisation de différentes versions de Configuration Manager sur le même réseau :  

-   [Interopérabilité entre System Center Configuration Manager et les versions antérieures du produit](#BKMK_SupConfigInterop)  

-   [Interopérabilité de la console Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitations de Configuration Manager dans une hiérarchie de versions mixtes](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interopérabilité entre System Center Configuration Manager et les versions antérieures du produit  
 Les sites de différentes versions ne peuvent pas coexister dans la même hiérarchie, sauf pendant le processus de mise à niveau de System Center 2012 Configuration Manager vers System Center Configuration Manager ou d’une version de System Center Configuration Manager vers une version plus récente (à l’aide de mises à jour dans la console).   

 Étant donné que vous pouvez déployer un site et une hiérarchie System Center Configuration Manager côte à côte avec un site ou une hiérarchie System Center 2012 Configuration Manager qui existe déjà, nous vous recommandons d’empêcher les clients de l’une des versions de tenter de joindre un site à partir de l’autre version.

Par exemple, si plusieurs hiérarchies Configuration Manager ont des limites qui se chevauchent (voir [Chevauchement des limites](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)) qui incluent les mêmes emplacements réseau, une bonne pratique consiste à attribuer chaque nouveau client à un site spécifique au lieu d’utiliser l’attribution de site automatique. Pour plus d’informations sur l’attribution de site automatique dans System Center 2012 Configuration Manager, consultez [Guide pratique pour attribuer des clients à un site dans System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

 De plus, vous ne pouvez pas installer un client à partir de System Center 2012 Configuration Manager sur un ordinateur qui héberge un rôle système de site de System Center Configuration Manager, ni installer un client System Center Configuration Manager sur un ordinateur qui héberge un rôle système de site de System Center 2012 Configuration Manager.  

 De même, les clients suivants et la connexion VPN (Virtual Private Network) suivante ne sont pas pris en charge :  

-   Toute version de client System Center 2012 Configuration Manager ou antérieure  

-   Tout client de gestion des appareils System Center 2012 Configuration Manager ou antérieur  

-   Client de gestion des appareils Windows CE Platform Builder (toute version)  

-   Connexion VPN System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considérations sur l’attribution de sites aux clients  
 Les clients System Center Configuration Manager peuvent être attribués à un seul site principal. Si l'attribution automatique de site est utilisée pour attribuer des clients à un site lors de l'installation du client, et qu'une même limite est configurée sur plusieurs groupes et différents sites sont attribués aux groupes de limites, l'attribution de site d'un client n'est pas prévisible.  

 Si des limites se chevauchent sur plusieurs hiérarchies et sites Configuration Manager, les clients risquent de ne pas être attribués au site que vous escomptez ou de n’être attribués à aucun site.  

 Les clients System Center Configuration Manager vérifient la version du site Configuration Manager avant de procéder à l’attribution de site et ne peuvent pas être attribués à une version précédente quand et si des limites se chevauchent. Toutefois, les clients System Center 2012 Configuration Manager peuvent être incorrectement attribués à un site System Center Configuration Manager.  

 Pour empêcher l’attribution involontaire de clients au mauvais site quand les limites des deux hiérarchies se chevauchent, nous vous recommandons de configurer les paramètres d’installation du client Configuration Manager de manière à attribuer des clients à un site spécifique.  

##  <a name="bkmk_mixed"></a> Limitations de Configuration Manager dans une hiérarchie de versions mixtes  
 Pendant la mise à niveau d’un site System Center Configuration Manager, il se peut que la version varie d’un site à l’autre. Par exemple, vous pouvez mettre à niveau un site d’administration centrale vers une nouvelle version, mais en raison des fenêtres de maintenance de site, un ou plusieurs sites principaux ne peuvent pas être mis à niveau avant une date et une heure futures.  

 Quand différents sites dans une même hiérarchie exécutent différentes versions, certaines fonctionnalités ne sont pas disponibles. Cela peut affecter la manière dont vous gérez les objets Configuration Manager dans la console Configuration Manager, ainsi que les fonctionnalités accessibles aux clients. Généralement, la fonctionnalité de la version la plus récente de Configuration Manager n’est pas accessible sur des sites ou par des clients qui exécutent une version de Service Pack antérieure.  

### <a name="limitations-when-upgrading--configuration-manager"></a>Limitations liées à la mise à niveau de Configuration Manager  

|Objet|Détails|  
|------------|-------------|  
|Compte d'accès réseau|**Mise à niveau de System Center 2012 Configuration Manager vers System Center Configuration Manager :** quand vous affichez les détails du compte d’accès réseau à partir d’une console Configuration Manager connectée à un site d’administration centrale mis à jour vers System Center Configuration Manager, la console n’affiche pas les détails des comptes qui sont configurés sur un site principal qui exécute System Center 2012 Configuration Manager. Une fois le site principal mis à niveau vers la même version que le site d’administration centrale, les détails du compte sont visibles dans la console.<br /><br /> **Mise à niveau entre des versions de System Center Configuration Manager :** quand vous affichez les détails du compte d’accès réseau à partir d’une console Configuration Manager connectée à un site d’administration centrale ayant été mis à jour vers une nouvelle version de System Center Configuration Manager, la console n’affiche pas de détails pour les comptes qui sont configurés sur un site principal qui exécute une version antérieure. Une fois le site principal mis à niveau vers la même version que le site d’administration centrale, les détails du compte sont visibles dans la console.|  
|Images de démarrage pour le déploiement de système d'exploitation|**Mise à niveau de System Center 2012 Configuration Manager vers System Center Configuration Manager :** quand le site de niveau supérieur d’une hiérarchie se met à niveau vers System Center Configuration Manager, les images de démarrage par défaut sont automatiquement mises à jour vers des images de démarrage basées sur Windows Assessment and Deployment Kit 10 (Windows ADK). Utilisez ces images de démarrage uniquement pour les déploiements sur des clients de sites System Center Configuration Manager. Pour plus d’informations, consultez [Planification de l’interopérabilité des déploiements de systèmes d’exploitation dans System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Mise à niveau entre des versions de System Center Configuration Manager :** tant que les nouvelles versions de cm6long ne mettent pas à jour la version de Windows ADK en cours d’utilisation, il n’y a aucune incidence sur les images de démarrage.|  
|Nouvelles étapes de séquence de tâche|Quand vous créez une séquence de tâches avec une étape introduite dans une version de Configuration Manager qui n’est pas disponible dans une version antérieure, vous pouvez rencontrer les problèmes suivants :<br /><br /> -- Une erreur se produit quand vous essayez de modifier la séquence de tâches à partir d’un site exécutant une version précédente de Configuration Manager.<br /><br /> -- La séquence de tâches ne s’exécute pas sur un ordinateur exécutant une version antérieure du client Configuration Manager.|  
|Communications entre le client et un point de gestion de niveau inférieur|Un client Configuration Manager qui communique avec un point de gestion d’un site exécutant une version plus ancienne que celle du client ne peut utiliser que les fonctionnalités prises en charge par la version de niveau inférieur de Configuration Manager. Par exemple, si vous déployez du contenu d’un site Configuration Manager récemment mis à niveau vers un client qui communique avec un point de gestion qui n’a pas encore été mis à niveau vers cette version, ce client ne peut pas utiliser les nouvelles fonctionnalités de la version la plus récente.|  

##  <a name="BKMK_ConsoleInterop"></a> Interopérabilité de la console Configuration Manager  
 Le tableau suivant contient des informations sur l’utilisation de la console Configuration Manager dans un environnement qui possède un mélange de versions de Configuration Manager.  

|Environnement d'interopérabilité|Plus d'informations|  
|----------------------------------|----------------------|  
|Un environnement avec à la fois System Center 2012 Configuration Manager et System Center Configuration Manager|Pour gérer un site Configuration Manager, la console et le site auquel elle se connecte doivent tous les deux exécuter la même version de Configuration Manager. Par exemple, vous ne pouvez pas utiliser une console System Center 2012 Configuration Manager pour gérer un site System Center Configuration Manager, ou vice versa.<br /><br /> L’installation à la fois de la console System Center 2012 Configuration Manager et de la console System Center Configuration Manager sur le même ordinateur n’est pas prise en charge.|  
|Environnement avec plusieurs versions de System Center Configuration Manager|System Center Configuration Manager ne prend pas en charge l’installation de plusieurs consoles Configuration Manager sur un ordinateur. Pour utiliser plusieurs consoles propres à différentes versions de System Center Configuration Manager, vous devez installer les différentes consoles sur des ordinateurs distincts.<br /><br /> Pendant le processus de mise à jour de sites dans une hiérarchie avec une nouvelle version, vous pouvez connecter une console à un site qui exécute une version plus récente et afficher des informations sur d’autres sites de cette hiérarchie. Toutefois, cette configuration n’est pas recommandée, car les différences entre la version de la console et la version du site Configuration Manager risquent d’entraîner des problèmes de données, et certaines fonctionnalités qui sont disponibles dans la dernière version du produit ne sont pas disponibles dans la console. <br /><br> La gestion d’un site avec une console dont la version ne correspond pas à la version du site n’est pas prise en charge. Elle peut entraîner une perte de données et exposer votre site à des risques. Par exemple, l’utilisation d’une console avec la version 1610 pour gérer un site qui exécute la version 1606 n’est pas prise en charge. |
