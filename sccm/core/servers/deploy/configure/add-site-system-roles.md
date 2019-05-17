---
title: Ajouter des rôles de système de site
titleSuffix: Configuration Manager
description: Découvrez les rôles de système de site Configuration Manager et apprenez à les ajouter pour étendre les fonctionnalités de votre site.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96710897dd518832a221717b7fdbec0a73eed01e
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499101"
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>Ajouter des rôles de système de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque site System Center Configuration Manager prend en charge plusieurs rôles de système de site. Chaque rôle étend les fonctionnalités de votre site, ainsi que sa capacité à fournir des services au site et à gérer des appareils et des utilisateurs. Tous les rôles de système de site sur un serveur de système de site doivent être membres du même site.   

Configuration Manager ne prend pas en charge les rôles système de site pour plusieurs sites sur un serveur de système de site unique.  

> [!TIP]  
>  Si vous n’êtes pas familiarisé avec les concepts de base des rôles de système de site ou avec les différences entre le serveur de site, les serveurs de système de site et les rôles de système de site, consultez [Principes de base de System Center Configuration Manager](../../../../core/understand/fundamentals.md).  

 Les rubriques suivantes décrivent des procédures et détails connexes pour l’installation de rôles système de site :  

-   [Installer des rôles système de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     Cette rubrique fournit des conseils de base sur l’utilisation des deux Assistants dans la console, qui permettent d’installer de nouveaux rôles de système de site.  

-   [Installer des points de distribution cloud dans Microsoft Azure pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    Si vous souhaitez utiliser Microsoft Azure pour héberger le contenu que vous déployez sur des clients, les informations contenues dans cette rubrique vous aideront à configurer les fichiers de certificats nécessaires pour permettre à Configuration Manager de communiquer avec votre abonnement Microsoft Azure et de l’utiliser. En outre, vous devrez configurer la résolution de nom pour permettre à vos clients de rechercher vos points de distribution cloud.  

-   [Installer des rôles système de site pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Cette rubrique va vous aider à configurer correctement vos rôles de système de site pour prendre en charge la gestion d’appareils modernes à l’aide de la gestion des appareils mobiles locale de Configuration Manager.  

-   [Options de configuration pour les rôles système de site pour System Center Configuration Manager](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     Certains rôles de système de site prennent en charge des configurations qui nécessitent plus de détails que ce qui peut être expliqué dans l’interface utilisateur. Cette rubrique fournit ces détails.  
