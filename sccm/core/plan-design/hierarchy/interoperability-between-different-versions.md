---
title: Interopérabilité entre versions
titleSuffix: Configuration Manager
description: Découvrez comment éviter les conflits entre plusieurs hiérarchies Configuration Manager sur le même réseau.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51243f8df55f2736cfb053f9e38cc7b6716b2158
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66354856"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interopérabilité entre les différentes versions de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez installer et utiliser plusieurs hiérarchies indépendantes de System Center Configuration Manager sur le même réseau. Toutefois, étant donné que des hiérarchies différentes de Configuration Manager n’interagissent pas en dehors du processus de migration, chaque hiérarchie nécessite une configuration pour éviter des conflits. En outre, vous pouvez créer certaines configurations pour faciliter l’interaction des ressources que vous gérez avec les systèmes de site de la hiérarchie correcte.  

Les sections suivantes fournissent des informations sur l'utilisation de différentes versions de Configuration Manager sur le même réseau :  

- [Interopérabilité entre System Center Configuration Manager et les versions antérieures du produit](#BKMK_SupConfigInterop)  

- [Interopérabilité de la console Configuration Manager](#BKMK_ConsoleInterop)  

- [Limitations de Configuration Manager dans une hiérarchie de versions mixtes](#bkmk_mixed)  


## <a name="BKMK_SupConfigInterop"></a> Interopérabilité entre System Center Configuration Manager et les versions antérieures du produit  

Les sites de différentes versions ne peuvent pas coexister dans la même hiérarchie de Configuration Manager. Les seules exceptions sont pendant le processus des scénarios de mise à niveau suivants :

- Depuis System Center 2012 Configuration Manager vers System Center Configuration Manager
- D’une version de System Center Configuration Manager vers une version plus récente à l’aide de mises à jour dans la console

Vous pouvez déployer un site et une hiérarchie System Center Configuration Manager côte à côte avec un site ou une hiérarchie System Center 2012 Configuration Manager qui existe déjà. Envisagez d’empêcher les clients de l’une ou l’autre version d’essayer de joindre un site à partir de l’autre version.

Par exemple, si deux hiérarchies Configuration Manager ou plus ont des [limites qui se chevauchent](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries), comprenant les mêmes emplacements réseau, affectez chaque nouveau client à un site spécifique au lieu d’utiliser l’affectation de site automatique. Pour plus d'informations, consultez la page [Comment attribuer des clients à un site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

En outre, vous ne pouvez pas installer un client depuis System Center 2012 Configuration Manager sur un ordinateur qui héberge un rôle de système de site depuis System Center Configuration Manager. Vous ne pouvez pas non plus installer un client System Center Configuration Manager sur un ordinateur qui héberge un rôle de système de site depuis System 2012 Center Configuration Manager.  

Les connexions et clients suivants ne sont pas pris en charge :  

- Toute version de client System Center 2012 Configuration Manager ou antérieure  

- Tout client de gestion des appareils System Center 2012 Configuration Manager ou antérieur  

- Client de gestion des appareils Windows CE Platform Builder (toute version)  

- Connexion VPN System Center Mobile Device Manager  

### <a name="BKMK_SupConfigSiteAssignment"></a> Considérations sur l’attribution de sites aux clients  

Les clients Configuration Manager peuvent être attribués à un seul site principal. Vous ne pouvez pas prédire l’attribution de site réel d’un client lorsque toutes les conditions suivantes sont remplies :

- Utilisez l’attribution de site automatique pour attribuer des clients à un site pendant l’installation du client
- Plus d’un groupe de limites inclut la même limite
- Les groupes de limites ont différents sites attribués

Si des limites se chevauchent sur plusieurs hiérarchies et sites Configuration Manager, les clients risquent de ne pas être attribués au site que vous escomptez ou de n’être attribués à aucun site.  

Les clients System Center Configuration Manager vérifient la version du site avant de terminer l’attribution complète du site. Si des limites de site se chevauchent, vous ne pouvez pas attribuer des clients à un site avec une version précédente. Toutefois, les clients plus récents de System Center 2012 Configuration Manager peuvent être incorrectement attribués à un site System Center Configuration Manager plus ancien.  

Pour empêcher l’attribution involontaire de clients au mauvais site quand les limites des deux hiérarchies se chevauchent, configurez les paramètres d’installation du client de manière à attribuer les clients à un site spécifique.  

## <a name="bkmk_mixed"></a> Limitations de Configuration Manager dans une hiérarchie de versions mixtes  

Pendant la mise à niveau d’une hiérarchie System Center Configuration Manager, il se peut que la version varie d’un site à l’autre. Par exemple, vous mettez d’abord à niveau le site administration centrale. En raison des fenêtres de maintenance du site, vous ne mettez pas à niveau les sites principaux jusqu'à une date et une heure ultérieures.  

Quand différents sites dans une même hiérarchie exécutent différentes versions, certaines fonctionnalités ne sont pas disponibles. Ce comportement peut affecter la manière dont vous gérez les objets Configuration Manager dans la console Configuration Manager, ainsi que les fonctionnalités accessibles aux clients. Généralement, la fonctionnalité de la version la plus récente de Configuration Manager n’est pas accessible sur des sites ou par des clients qui exécutent une version inférieure de Service Pack.  

### <a name="network-access-account"></a>Compte d'accès réseau

Vous mettez à niveau le site d’administration centrale vers System Center Configuration Manager. Vous affichez les détails du compte d’accès réseau à partir d’une console Configuration Manager connectée à ce site mis à jour. Elle n’affiche pas les détails du compte depuis des sites qui exécutent encore System Center 2012 Configuration Manager.

Une fois le site principal mis à niveau vers la même version que le site d’administration centrale, les détails du compte sont visibles dans la console.

Le même comportement s’applique lorsque vous procédez à une mise à jour entre les versions de System Center Configuration Manager.

### <a name="boot-images-for-os-deployment"></a>Images de démarrage pour le déploiement de systèmes d’exploitation

#### <a name="when-upgrading-from-system-center-2012-configuration-manager-to-system-center-configuration-manager"></a>Lors de la mise à niveau de System Center 2012 Configuration Manager vers System Center Configuration Manager

Quand le site de niveau supérieur d’une hiérarchie est mis à niveau vers System Center Configuration Manager, les images de démarrage par défaut sont automatiquement mises à jour pour utiliser l’évaluation Windows et le kit de déploiement (ADK) version 10. Utilisez ces images de démarrage uniquement pour les déploiements sur des clients de sites System Center Configuration Manager. Pour plus d'informations, consultez la page [Planification de l’interopérabilité pour le déploiement de systèmes d’exploitation](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability).

#### <a name="when-upgrading-between-system-center-configuration-manager-versions"></a>Lors de la mise à niveau entre des versions de System Center Configuration Manager

Tant que les nouvelles versions de Configuration Manager ne mettent pas à jour la version de Windows ADK en cours d’utilisation, il n’y a aucune incidence sur les images de démarrage.

### <a name="new-task-sequence-steps"></a>Nouvelles étapes de séquence de tâche

Lorsque vous créez une séquence de tâches avec une étape introduite dans une version de Configuration Manager non disponible dans une version antérieure, vous pouvez rencontrer les problèmes suivants :

- Une erreur se produit quand vous essayez de modifier la séquence de tâches à partir d’un site exécutant une version précédente de Configuration Manager.

- La séquence de tâches ne s’exécute pas sur un ordinateur exécutant une version antérieure du client Gestionnaire de configuration.

### <a name="client-to-down-level-management-point-communications"></a>Communications entre le client et un point de gestion de niveau inférieur

Un client Configuration Manager qui communique avec un point de gestion d’un site exécutant une version plus ancienne que celle du client ne peut utiliser que les fonctionnalités prises en charge par la version de niveau inférieur de Configuration Manager. Par exemple, si vous déployez du contenu d’un site Configuration Manager récemment mis à niveau vers un client qui communique avec un point de gestion qui n’a pas encore été mis à niveau vers cette version, ce client ne peut pas utiliser les nouvelles fonctionnalités de la version la plus récente.

### <a name="package-and-task-sequence-deployments-to-legacy-clients"></a>Déploiements de séquences de packages et de tâches pour les clients hérités

<!-- SCCMDocs-pr issue #3493 -->

Depuis la version 1902, vous ne pouvez pas déployer une séquence de tâches ou de packages vers une version de client 5.7730 ou version antérieure. Pour contourner cette limitation, mettez à niveau le client vers une version ultérieure.


## <a name="BKMK_ConsoleInterop"></a> Interopérabilité de la console Configuration Manager  

Cette section contient des informations sur l’utilisation de la console Configuration Manager dans un environnement qui possède un mélange de versions de Configuration Manager.  

### <a name="an-environment-with-both-system-center-2012-configuration-manager-and-system-center-configuration-manager"></a>Un environnement avec à la fois System Center 2012 Configuration Manager et System Center Configuration Manager

Pour gérer un site Configuration Manager, la console et le site auquel elle se connecte doivent tous les deux exécuter la même version de Configuration Manager. Par exemple, vous ne pouvez pas utiliser une console System Center 2012 Configuration Manager pour gérer un site System Center Configuration Manager ou vice versa.

L’installation à la fois de la console System Center 2012 Configuration Manager et de la console System Center Configuration Manager sur le même ordinateur n’est pas prise en charge.

### <a name="an-environment-with-multiple-versions-of-system-center-configuration-manager"></a>Environnement avec plusieurs versions de System Center Configuration Manager

System Center Configuration Manager ne prend pas en charge l’installation de plusieurs consoles Configuration Manager sur un ordinateur. Pour utiliser plusieurs consoles propres à différentes versions de System Center Configuration Manager, installez les différentes consoles sur des ordinateurs distincts.

Pendant le processus de mise à jour de sites dans une hiérarchie avec une nouvelle version, vous pouvez connecter une console à un site qui exécute une version plus récente et afficher des informations sur d’autres sites de cette hiérarchie. Toutefois, cette configuration n’est pas recommandée. Il se peut que les différences entre la version de la console et la version du site Configuration Manager entraînent des problèmes sur les données. Certaines des fonctionnalités disponibles dans la dernière version du produit ne seront pas disponibles dans la console.

La gestion d’un site avec une console dont la version ne correspond pas à la version du site n’est pas prise en charge. Elle peut entraîner une perte de données et exposer votre site à des risques. Par exemple, l’utilisation d’une console avec la version 1610 pour gérer un site qui exécute la version 1606 n’est pas prise en charge.
