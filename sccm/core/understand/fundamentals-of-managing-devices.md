---
title: Notions de base de la gestion des périphériques
titleSuffix: Configuration Manager
description: Découvrez comment gérer des appareils dans System Center Configuration Manager.
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3890b67e88de6483d231f473ef2025c5f71ed93
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119872"
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>Notions de base de la gestion des appareils avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager peut gérer deux grandes catégories d’appareils :

-   Les *clients* sont des appareils comme les stations de travail, les ordinateurs portables, les serveurs et les appareils mobiles sur lesquels vous installez le logiciel client Configuration Manager. Certaines fonctions de gestion, comme l’inventaire matériel, nécessitent ce logiciel client.  

-   Les *appareils gérés* peuvent inclure des *clients*, mais il s’agit généralement d’un appareil mobile sur lequel le logiciel client Configuration Manager n’est pas installé. Sur ce type d’appareil, vous effectuez la gestion en utilisant Intune ou la fonctionnalité de gestion locale des appareils mobiles intégrée de Configuration Manager.

Vous pouvez aussi regrouper et identifier des appareils en fonction de l’utilisateur, et pas seulement du type de client.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Gestion des appareils avec le client Configuration Manager

Il existe deux façons d’utiliser le logiciel client Configuration Manager pour gérer un appareil. La première consiste à détecter l’appareil sur votre réseau, puis à déployer le logiciel client sur cet appareil. L’autre consiste à installer manuellement le logiciel client sur un nouvel ordinateur, puis à faire en sorte que cet ordinateur rejoigne votre site quand il rejoint votre réseau. Pour détecter les appareils sur lesquels le logiciel client n’est pas installé, exécutez une ou plusieurs des méthodes de découverte intégrées. Après la découverte d’un appareil, vous pouvez utiliser une des différentes méthodes disponibles pour installer le logiciel client. Pour plus d’informations sur l’utilisation de la découverte, consultez [Exécuter la découverte pour System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 Après la découverte des appareils pris en charge pour exécuter le logiciel client Configuration Manager, vous pouvez installer le logiciel avec l’une des différentes méthodes disponibles. Une fois le logiciel installé et le client affecté à un site principal, vous pouvez commencer à gérer l’appareil.  Les méthodes d’installation courantes sont les suivantes :

 - Installation Push du client.

 - Installation basée sur une mise à jour logicielle.

 - Stratégie de groupe.

 - Installation manuelle sur un ordinateur.
 - Client inclus comme partie d’une image de système d’exploitation que vous déployez.  


 Une fois le client installé, vous pouvez simplifier les tâches de gestion des appareils en utilisant des regroupements. Les regroupements sont des groupes d’appareils ou d’utilisateurs que vous créez afin de pouvoir les gérer en tant que groupe. Imaginons, par exemple, que vous souhaitez installer une application d’appareil mobile sur tous les appareils mobiles inscrits par Configuration Manager. Dans ce cas, vous pouvez utiliser le regroupement Tous les appareils mobiles.  

 Pour plus d’informations, consultez ces rubriques :  

-   [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Méthodes d’installation du client dans System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Présentation des regroupements dans System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Paramètres du client  
 Quand vous installez Configuration Manager pour la première fois, tous les clients de la hiérarchie sont configurés avec les paramètres client par défaut. Vous pouvez ensuite modifier ces paramètres, si vous le souhaitez. Les paramètres client comprennent des options de configuration suivantes :

 -  Fréquence à laquelle les appareils communiquent avec le site.

 -  Configuration éventuelle du client pour les mises à jour logicielles et autres opérations de gestion.

 -  La possibilité, pour les utilisateurs, d’inscrire leurs appareils mobiles afin qu’ils soient gérés par Configuration Manager.  

Vous pouvez créer des paramètres client personnalisés et les affecter ensuite à des regroupements.  Les membres du regroupement sont configurés pour utiliser les paramètres personnalisés, et vous pouvez créer plusieurs paramètres client personnalisés qui s’appliquent dans l’ordre (numérique) que vous spécifiez.  En cas de conflit entre paramètres, le paramètre dont le numéro d’ordre est le plus petit remplace les autres paramètres.  

Le schéma ci-dessous montre comment créer et appliquer des paramètres client personnalisés.  

 ![Paramètres du client](media/ClientSettings.gif)  

 Pour en savoir plus sur les paramètres client, consultez  
                [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) et [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## <a name="managing-devices-without-the-configuration-manager-client"></a>Gestion des appareils sans client Configuration Manager  
 Configuration Manager prend en charge la gestion de certains appareils sur lesquels le logiciel client n’est pas installé et qui ne sont pas gérés par Intune. Pour plus d’informations, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) et [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Gestion basée sur l’utilisateur  
 Configuration Manager prend en charge les regroupements d’utilisateurs des services de domaine Active Directory. Quand vous utilisez un regroupement d’utilisateurs, vous pouvez installer le logiciel sur tous les ordinateurs utilisés par les membres du regroupement. Pour garantir que les logiciels que vous déployez s’installent uniquement sur les appareils spécifiés en tant qu’appareil principal d’un utilisateur, configurez l’affinité entre appareil et utilisateur. Un utilisateur peut posséder un ou plusieurs appareils principaux.  

 L’une des façons pour les utilisateurs de contrôler leur expérience de déploiement de logiciels consiste à utiliser l’interface client du **Centre logiciel**. Le **Centre logiciel** est automatiquement installé sur les ordinateurs clients, et est exécuté à partir du menu **Démarrer**. Le **Centre logiciel** permet aux utilisateurs de gérer leurs propres logiciels et d’exécuter les tâches suivantes :  

-   Installez le logiciel.  

-   Planifiez l’installation automatique du logiciel en dehors des heures de travail.  

-   Configurez le moment où Configuration Manager peut installer le logiciel sur un appareil.  

-   Configurez les paramètres d’accès pour le contrôle à distance, si ce dernier est configuré dans Configuration Manager.  

-   Configurez les options de gestion de l’alimentation si un administrateur configure cette option.  


 Un lien disponible dans le **Centre logiciel** permet aux utilisateurs de se connecter au **catalogue d’applications**, où ils peuvent parcourir, installer et demander des logiciels. Le **catalogue d’applications** est également utilisé pour configurer les paramètres de préférence, pour réinitialiser des appareils mobiles et, quand il est configuré, pour spécifier un appareil principal pour l’affinité entre appareil et utilisateur.   

 Les utilisateurs peuvent également accéder au **catalogue d’applications** par le biais d’un intranet de navigateur ou une session Internet.  
