---
title: Configurer un abonnement Intune
titleSuffix: Configuration Manager
description: Configurer un abonnement Intune pour le suivi des licences sur site Gestion des appareils mobiles dans Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 1e42b1c1-3d58-481f-8647-5c7ae640c5f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff4fcc67325645387aea1e57354321769a515ca
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62217012"
---
# <a name="set-up-a-microsoft-intune-subscription-for-on-premises-mdm-in-configuration-manager"></a>Configurer un abonnement Microsoft Intune pour des applications MDM locales dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager local gestion des appareils mobiles (MDM) nécessite un abonnement Microsoft Intune pour le suivi des licences. Le service Intune n’est pas utilisé pour gérer les appareils ou pour stocker les informations de gestion. Pour des applications MDM locales, toute la gestion des appareils est gérée par l’infrastructure Configuration Manager.  

Avant d’installer les rôles de système de site nécessaires pour la gestion MDM locale, configurez l’abonnement Intune. Cette action réduit le temps nécessaire pour les rôles de système de site qui vient d’être installé devenir fonctionnelle.  

> [!Note]  
> Depuis la version 1810, une connexion Intune n’est plus nécessaire pour les nouveaux déploiements de gestion des appareils mobiles en local.<!--3607730, fka 1359124--> Votre organisation exige toujours des licences Intune pour utiliser cette fonctionnalité. À l’heure actuelle, il n’est pas possible de supprimer la connexion Intune des déploiements MDM locaux existants. Pour plus d’informations, consultez le [billet de blog du support Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  



##  <a name="sign-up-for-microsoft-intune"></a>S’inscrire à Microsoft Intune  

Intune est nécessaire pour que la gestion MDM locale soit fonctionnel. [Inscrivez-vous](https://docs.microsoft.com/intune/free-trial-sign-up) pour un abonnement d’évaluation ou payant. Accédez ensuite à l’étape suivante pour ajouter l’abonnement à Configuration Manager.  



##  <a name="add-the-intune-subscription-to-configuration-manager"></a>Ajouter l’abonnement Intune à Configuration Manager  

Pour ajouter l’abonnement à Configuration Manager, vous suivez les mêmes étapes de base comme vous le feriez lors de l’ajout de l’abonnement pour la gestion hybride MDM avec Intune. Lisez les remarques ci-dessous qui décrivent les différences spécifiques, puis suivez les instructions fournies dans [Configurer votre abonnement Intune](/sccm/mdm/deploy-use/configure-intune-subscription).  

> [!NOTE]
>  Lorsque vous ajoutez l’abonnement Intune, n’oubliez pas les notes suivantes :  
> 
> - La collection spécifiée dans l’Assistant Ajouter un abonnement Microsoft Intune n’est pas utilisée pour la délégation des droits d’utilisateur local gestion des appareils mobiles. Il est utilisé uniquement pour la gestion des appareils mobiles avec Intune. Toutefois, vous devez spécifier un regroupement de l’Assistant continuer.  
> 
> - Le code de site que vous spécifiez dans l’Assistant est ignoré pour la gestion MDM locale. Il utilise le code de site que vous spécifiez lors de l’inscription profil qui autorise les utilisateurs à inscrire des appareils.  
> 
> - N’activez pas l’authentification multifacteur. Il n’est pas pris en charge dans la gestion MDM locale.  



##  <a name="configure-the-intune-subscription-for-on-premises-mdm"></a>Configurer l’abonnement Intune pour la gestion MDM locale  

1. Dans la console Configuration Manager, accédez à la **Administration** espace de travail, développez **Services Cloud**, puis sélectionnez le **abonnements Microsoft Intune** nœud. Sélectionnez votre abonnement, puis choisissez **propriétés** dans le ruban.   

    1. Dans la section Gestion des appareils mobiles locale en bas de la **général** page, choisissez une des options suivantes :

        - Si vous prévoyez d’avoir uniquement des appareils gérés localement, sélectionnez l’option à **uniquement gérer les appareils en local**.  

            > [!NOTE]  
            > Lorsque vous activez cette option, vous configurez l’abonnement Intune pour conserver tous les gestion stockées en local. Aucune donnée de gestion de périphérique n’est répliquée vers le cloud.  

        - Si vous prévoyez d’avoir des appareils gérés par Intune et Configuration Manager en local, ne configurez pas cette option.  

    Sélectionnez **OK** pour fermer les propriétés d’abonnement.

2. Si vous envisagez de gérer les appareils Windows 10 Mobile, sélectionnez votre abonnement dans la liste, sélectionnez **configurer des plateformes** dans le ruban, puis sélectionnez **Windows Phone**.  

    1. Sélectionnez l’option pour **Windows Phone 8.1 et Windows 10 Mobile**, puis sélectionnez **OK**.  

3. Si vous prévoyez de gérer des ordinateurs de bureau Windows 10, sélectionnez votre abonnement dans la liste, sélectionnez **configurer des plateformes** dans le ruban, puis sélectionnez **Windows**.  

    1. Sélectionnez l’option **l’inscription Windows activer**, puis sélectionnez **OK**.  

