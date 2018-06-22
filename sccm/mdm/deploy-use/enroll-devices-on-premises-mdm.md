---
title: 'Inscrire des appareils '
titleSuffix: Configuration Manager
description: Découvrez les méthodes permettant d’inscrire des appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7e3254fdad766260e3e162378894526e9b4a7249
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353373"
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Inscrire des appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour gérer des ordinateurs et des appareils avec la fonctionnalité de gestion des appareils mobiles locale de System Center Configuration Manager, les appareils doivent être inscrits pour permettre à Configuration Manager de communiquer avec eux pour les tâches de gestion. Configuration Manager propose deux méthodes pour inscrire les appareils :  

-   **Inscription utilisateur** : avec cette méthode, les utilisateurs lancent le processus d’inscription sur leurs appareils. Pour que l’inscription utilisateur aboutisse, un certificat racine approuvé doit être installé sur l’appareil et l’utilisateur doit être configuré pour l’inscription par Configuration Manager.  Pour inscrire un appareil, l’utilisateur fournit simplement des informations d’identification professionnelles et l’appareil est inscrit pour être géré.  

     Pour plus d’informations, consultez [Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

-   **Inscription en bloc** : avec cette méthode, l’utilisateur de l’appareil n’a pas besoin de lancer l’inscription. Au lieu de cela, un package d’inscription en bloc est créé dans Configuration Manager puis placé sur l’appareil et ouvert. Lors de son ouverture, le package fournit les informations nécessaires pour inscrire l’appareil.  

     Pour plus d’informations, consultez [Guide pratique pour inscrire en bloc des appareils avec la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md).  

 > [!NOTE]  
>  Dans la gestion des appareils mobiles locale, la version Current Branch de Configuration Manager prend en charge l’inscription des appareils exécutant les systèmes d’exploitation suivants :  
>   
>  -   Windows 10 Entreprise  
> -   Windows 10 Professionnel  
> -   Windows 10 Collaboration 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Entreprise   
