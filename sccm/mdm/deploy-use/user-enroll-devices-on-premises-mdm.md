---
title: 'Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale '
titleSuffix: Configuration Manager
description: Comprendre comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 15774704665b2b52daf1061db221ab0eb158eceb
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347516"
---
# <a name="how-users-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Comment les utilisateurs inscrivent des appareils avec la gestion des appareils mobiles locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion des appareils mobiles locale de System Center Configuration Manager permet aux utilisateurs d’inscrire des appareils si une autorisation d’inscription (par le biais de paramètres client mis à jour) leur a été accordée et que le certificat racine nécessaire a été installé sur leurs appareils pour que leurs communications soient approuvées auprès des serveurs hébergeant les rôles de système de site exigés. Pour plus d’informations sur la configuration de l’inscription, consultez [Configurer l’inscription d’appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md).  

> [!NOTE]  
>  Dans la gestion des appareils mobiles locale, la version Current Branch de Configuration Manager prend en charge l’inscription des appareils exécutant les systèmes d’exploitation suivants :  
>   
> -  Windows 10 Entreprise  
> -   Windows 10 Professionnel  
> -   Windows 10 Collaboration \(à compter de Configuration Manager version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Entreprise
> -   Windows 10 IoT Entreprise   

Les tâches suivantes expliquent comment inscrire des ordinateurs et des appareils pour la gestion des appareils mobiles locale et comment vérifier leur inscription :  

-   [Inscrire un ordinateur Windows 10](#bkmk_enrollDesk)  

-   [Inscrire un appareil Windows 10 Mobile](#bkmk_enrollMob)  

-   [Vérifier l’inscription d’appareil](#bkmk_verify)  

##  <a name="bkmk_enrollDesk"></a> Inscrire un ordinateur Windows 10  

1.  Sur un ordinateur Windows 10, accédez aux **Paramètres**.  

2.  Cliquez sur **Comptes**, puis sur **Accès professionnel**.  

3.  Dans Accès professionnel, sous **Connecter à l’entreprise ou l’école**, cliquez sur **Connexion**, entrez votre adresse de messagerie professionnelle, puis cliquez sur **Continuer**.  

4.  Entrez le nom de domaine complet du serveur hébergeant le rôle de système de site de point proxy d’inscription, puis cliquez sur **Continuer**.  

5.  Dans Connexion à un service, entrez le mot de passe de votre adresse de messagerie professionnelle, puis cliquez sur **Connexion**.  

6.  Cliquez sur **Ignorer** pour mémoriser les informations de connexion. L’appareil est alors connecté au bout d’un bref laps de temps.  

##  <a name="bkmk_enrollMob"></a> Inscrire un appareil Windows 10 Mobile  

1.  Sur un appareil Windows 10 Mobile, accédez à **Paramètres**.  

2.  Cliquez sur **Comptes**, puis sur **Accès professionnel**.  

3.  Cliquez sur **Connexion**.  

4.  Entrez votre adresse de messagerie professionnelle et le nom de domaine complet du serveur hébergeant le rôle de système de site de point proxy d’inscription. Cliquez sur **Connexion**.  

5.  Dans l’écran suivant, entrez votre adresse de messagerie professionnelle et le mot de passe, puis cliquez sur **Connexion**. L’appareil est inscrit après un bref laps de temps. Cliquez sur **Terminé**.  

##  <a name="bkmk_verify"></a> Vérifier l’inscription d’appareil  
 Vous pouvez vérifier que les appareils ont été inscrits correctement dans la console Configuration Manager.  

1.  Démarrez la console Configuration Manager.  

2.  Cliquez sur **Ressources et Conformité** > **Vue d’ensemble** > **Appareils**. L’appareil inscrit apparaît dans la liste.  
