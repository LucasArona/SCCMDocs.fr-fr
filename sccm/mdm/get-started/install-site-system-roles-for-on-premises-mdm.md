---
title: 'Installer des rôles pour la gestion des appareils mobiles locale '
titleSuffix: Configuration Manager
description: Installez des rôles système de site pour la gestion des appareils mobiles locale dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e5d81d385c48d9653e1596e6a5d9d1163e84f314
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62216253"
---
# <a name="install-site-system-roles-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Installer des rôles de système de site pour la gestion des appareils mobiles locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion des appareils mobiles locale de System Center Configuration Manager nécessite les rôles système de site suivants dans votre infrastructure de site Configuration Manager :  

- Point d'inscription  

- Point proxy d'inscription  

- Point de distribution  

- Point de gestion d’appareil  

- point de connexion de service  

  Si vous ajoutez la gestion des appareils mobiles locale à votre organisation et que la plupart des ordinateurs et appareils de celle-ci sont gérés à l’aide du logiciel client Configuration Manager, la plupart des rôles système de site sont peut-être déjà installés dans le cadre de votre infrastructure existante. Dans le cas contraire, consultez [Ajouter des rôles système de site pour System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) pour plus d’informations sur la façon de les ajouter à votre site.  

> [!NOTE]  
>  Si vous utilisez des réplicas de base de données avec votre rôle de système de site de point de gestion de l’appareil, les appareils nouvellement inscrits échouent à se connecter au point de gestion de l’appareil tant que le réplica de base de données ne s’est pas synchronisé avec celui-ci. Cet échec de connexion se produit car le réplica de base de données n’a pas les informations sur l’appareil nouvellement inscrit nécessaires pour que la connexion réussisse. Les réplicas se synchronisent toutes les 5 minutes : les appareils vont échouer à se connecter pendant les 5 premières minutes après l’inscription (généralement 2 tentatives de connexion), après quoi l’appareil va se connecter avec succès.  

 Que vous utilisiez des rôles de système de site existants ou que vous en ajoutiez de nouveaux, vous devez les configurer de manière à pouvoir les utiliser pour gérer les appareils récents. Suivez les étapes ci-dessous pour configurer le point de distribution et le point de gestion d’appareil afin qu’ils fonctionnent correctement pour la gestion des appareils mobiles locale :  

> [!NOTE]  
>  La branche Current Branch de Configuration Manager prend uniquement en charge les connexions intranet depuis les appareils vers les points de distribution et les points de gestion d’appareil dans le cadre de la gestion des appareils mobiles locale. Toutefois, si vous gérez également des ordinateurs Mac OS X, ces clients nécessitent des connexions internet à ces rôles de système de site. Dans ce cas, quand vous configurez les propriétés du point de distribution et du point de gestion d’appareil, vous devez plutôt utiliser le paramètre **Autoriser les connexions intranet et Internet**.  

### <a name="to-configure-site-system-roles-to-manage-modern-devices"></a>Pour configurer les rôles de système de site pour gérer les appareils récents :  

1. Dans la console Configuration Manager, cliquez sur **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**.  

2. Sélectionnez le serveur de système de site possédant le point de distribution ou le point de gestion d’appareil à configurer, ouvrez les propriétés de **Système de site** et vérifiez qu’un nom de domaine complet est spécifié. Cliquez sur **OK**.  

3. Ouvrez les propriétés du rôle de système de site du point de distribution . Sous l’onglet Général, assurez-vous que **HTTPS** est sélectionné, puis sélectionnez **Autoriser les connexions intranet uniquement**.  

    Si vous gérez également des ordinateurs Mac séparément avec le client Configuration Manager, utilisez **Autoriser les connexions intranet et Internet** à la place.  

   > [!NOTE]  
   >  Les points de distribution configurés pour les connexions intranet nécessitent une configuration particulière des limites du site. La branche Current Branch de Configuration Manager prend uniquement en charge les limites de plage IPv4 pour la gestion des appareils mobiles locale. Pour plus d’informations sur la configuration des limites de site, consultez [Définir les limites de site et les groupes de limites pour System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4. Cochez la case **Autoriser les appareils mobiles à se connecter à ce point de distribution**, puis cliquez sur **OK**.  

5. Ouvrez les propriétés du rôle de système de site du point de gestion. Sous l’onglet Général, assurez-vous que **HTTPS** est sélectionné, puis sélectionnez **Autoriser les connexions intranet uniquement**.  

    Si vous gérez également des ordinateurs Mac séparément avec le client Configuration Manager, utilisez **Autoriser les connexions intranet et Internet** à la place.  

6. Cochez la case **Autoriser les appareils mobiles et les ordinateurs Mac à utiliser ce point de gestion**. Cliquez sur **OK**.  

    Le point de gestion est alors converti en point de gestion d’appareil.  

   Une fois que les rôles de système de site ont été ajoutés et configurés pour la gestion des appareils récents, vous devez configurer les serveurs hébergeant les rôles en tant que points de terminaison approuvés pour inscrire les appareils gérés et communiquer avec ces derniers. Pour plus d’informations, consultez [Configurer des certificats pour les communications approuvées pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md).  
