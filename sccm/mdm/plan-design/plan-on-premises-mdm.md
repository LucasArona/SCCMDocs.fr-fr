---
title: Planifier la gestion des appareils mobiles locale
titleSuffix: Configuration Manager
description: Planifiez la gestion des appareils mobiles (MDM) locale pour gérer des appareils mobiles dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10cddac80b9a7ea4bd912e2f52585cdcef7e70da
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Planifier la gestion des appareils mobiles locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Tenez compte des conditions requises suivantes avant de préparer l’infrastructure Configuration Manager à la gestion des appareils mobiles locale.

##  <a name="bkmk_devices"></a> Appareils pris en charge  
 La gestion des appareils mobiles locale vous permet de gérer des appareils mobiles à l’aide des fonctions de gestion intégrées aux systèmes d’exploitation des appareils.  La fonctionnalité de gestion est basée sur la norme Open Mobile Alliance (OMA) Device Management (DM), et de nombreuses plateformes d’appareils utilisent cette norme pour autoriser la gestion des appareils.  Nous les appelons **appareils modernes** (dans la documentation et l’interface utilisateur de la console Configuration Manager) pour les différencier des autres appareils dont la gestion nécessite le client Configuration Manager.  

 > [!NOTE]  
>  Dans la gestion des appareils mobiles locale, la version Current Branch de Configuration Manager prend en charge l’inscription des appareils exécutant les systèmes d’exploitation suivants :  
>   
> -  Windows 10 Entreprise  
> -   Windows 10 Professionnel  
> -   Windows 10 Collaboration \(à compter de Configuration Manager version 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Entreprise
> -   Windows 10 IoT Entreprise   

##  <a name="bkmk_intune"></a> Utilisation de l’abonnement Microsoft Intune  
 Pour pouvoir utiliser la gestion des appareils mobiles locale, vous avez besoin d’un abonnement Microsoft Intune. L’abonnement est nécessaire uniquement pour effectuer le suivi des licences des appareils. Il ne sert pas à gérer ou à stocker des informations sur la gestion des appareils. Toute la gestion s’effectue dans votre organisation à l’aide de l’infrastructure Configuration Manager locale.  

 > [!NOTE]  
 > À compter de la version 1610, Configuration Manager prend en charge l’utilisation simultanée de Microsoft Intune et de l’infrastructure Configuration Manager locale pour gérer les appareils mobiles.   

 Si votre site comporte des appareils dotés d’une connectivité Internet, vous pouvez utiliser le service Intune pour que les appareils vérifient l’existence de mises à jour de la stratégie par le biais du point de gestion d’appareil. Cette utilisation d’Intune est réservée uniquement à la notification des appareils exposés à Internet. Les appareils sans connexion Internet (ne pouvant pas être contactés par Intune) se fient à l’intervalle d’interrogation configuré pour vérifier les fonctions de gestion auprès des rôles système de site.  

> [!TIP]  
>  Nous vous recommandons de configurer l’abonnement Intune avant de configurer les rôles système de site nécessaires, pour que ces derniers soient opérationnels le plus rapidement possible.  

 Pour plus d’informations sur la façon de configurer l’abonnement Intune, consultez [Configurer un abonnement Microsoft Intune pour la gestion locale des appareils mobiles dans System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="bkmk_roles"></a> Rôles système de site nécessaires  
 La gestion des appareils mobiles locale nécessite au moins un rôle système de site parmi chacun des suivants :  

-   **Point proxy d’inscription** pour prendre en charge les demandes d’inscription.  

-   **Point d’inscription** pour prendre en charge l’inscription des appareils.  

-   **Point de gestion du périphérique** pour la remise de la stratégie. Ce rôle de système de site est une variante du rôle de point de gestion qui a été configuré pour autoriser la gestion des appareils mobiles.  

-   **Point de distribution** pour la remise du contenu.  

-   **Point de connexion de service** pour la connexion à Intune pour informer les appareils à l’extérieur du pare-feu.  

 Vous pouvez installer ces rôles de système de site sur le serveur de système de site unique, ou vous pouvez les exécuter séparément sur des serveurs distincts en fonction des besoins de votre organisation. Chaque serveur de système de site utilisé pour la gestion des appareils mobiles locale doit être configuré comme point de terminaison HTTPS pour communiquer avec les appareils de confiance. Pour plus d'informations, voir [Communications fiables requises](#bkmk_trustedComs).  

 Pour plus d’informations sur la planification des rôles de système de site, consultez [Planifier des serveurs de système de site et des rôles système de site pour System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Pour plus d’informations sur l’ajout des rôles de système de site obligatoires, consultez [Installer des rôles de système de site pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="bkmk_trustedComs"></a> Communications fiables requises  
 La gestion des appareils mobiles locale exige que des rôles système de site soient activés pour les communications HTTPS. En fonction de vos besoins, vous pouvez utiliser l’autorité de certification de votre entreprise pour établir les connexions approuvées entre les serveurs et les appareils, ou vous pouvez utiliser une autorité de certification publique comme autorité de confiance.  Dans les deux cas, vous devez configurer un certificat de serveur web avec IIS sur les serveurs de système de site hébergeant les rôles de système de site nécessaires, et vous devez installer le certificat racine de cette autorité de certification sur les appareils qui doivent se connecter à ces serveurs.  

 Si vous utilisez l’autorité de certification de votre entreprise pour établir des communications approuvées, vous devez effectuer les tâches suivantes :  

-   Créer et émettre le modèle de certificat de serveur web sur l’autorité de certification.  

-   Demander un certificat de serveur web pour chaque serveur de système de site hébergeant un rôle de système de site nécessaire.  

-   Configurer IIS sur le serveur de système de site pour utiliser le certificat de serveur web demandé.  

 Pour les appareils joints au domaine Active Directory d’entreprise, le certificat racine de l’autorité de certification d’entreprise est déjà disponible sur l’appareil pour les connexions approuvées. Cela signifie que les appareils appartenant au domaine (comme les ordinateurs de bureau) sont automatiquement approuvés pour les connexions HTTPS avec les serveurs de système de site. En revanche, les appareils non joints au domaine (généralement les appareils mobiles) ne possèdent pas le certificat racine nécessaire. Vous devez installer manuellement le certificat racine sur ces appareils pour qu’ils puissent communiquer correctement avec les serveurs de système de site prenant en charge la gestion des appareils mobiles locale.  

 Vous devez exporter le certificat racine de l’autorité de certification émettrice pour une utilisation par les différents appareils. Pour obtenir le fichier de certificat racine, vous pouvez l’exporter à l’aide de l’autorité de certification. Une méthode plus simple consiste à utiliser le certificat de serveur web émis par l’autorité de certification pour extraire la racine et créer un fichier de certificat racine.   Ensuite, le certificat racine doit être remis à l’appareil.  Voici quelques exemples de méthodes de remise :  

-   Système de fichiers  

-   Pièce jointe  

-   Carte mémoire  

-   Périphérique attaché  

-   Stockage cloud (tel que OneDrive)  

-   Connexion NFC (communication en champ proche)  

-   Lecteur de code-barres  

-   Package d’approvisionnement OOBE (Out of Box Experience)  

 Pour plus d'informations, consultez [Configurer des certificats pour les communications approuvées pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md).  

##  <a name="bkmk_enrollment"></a> Considérations relatives à l’inscription  
 Pour permettre l’inscription des appareils à la gestion des appareils mobiles locale, vous devez autoriser les utilisateurs à inscrire leurs appareils et ceux-ci doivent pouvoir établir des communications approuvées avec les serveurs de système de site hébergeant les rôles système de site nécessaires.  

 Pour accorder aux utilisateurs l’autorisation d’inscrire des appareils, vous pouvez configurer un profil d’inscription dans les paramètres client de Configuration Manager. Vous pouvez utiliser les paramètres client par défaut pour envoyer le profil d’inscription à tous les utilisateurs découverts, ou vous pouvez configurer le profil d’inscription dans les paramètres client personnalisés et envoyer les paramètres à un ou plusieurs regroupements d’utilisateurs.  

 Une fois l’autorisation d’inscription accordée aux utilisateurs, ils peuvent inscrire leurs appareils. Pour que l’inscription soit possible, il faut que l’appareil possède le certificat racine de l’autorité de certification qui a émis le certificat de serveur web utilisé sur les serveurs de système de site hébergeant les rôles de système de site nécessaires.  

 En guise d’alternative à l’inscription initiée par l’utilisateur, vous pouvez configurer un package d’inscription en bloc qui permet d’inscrire l’appareil sans intervention de l’utilisateur. Vous pouvez remettre ce package à l’appareil avant sa mise en service initiale ou à l’issue du processus OOBE.  

 Pour plus d’informations sur la façon de configurer et d’inscrire des appareils, consultez  

-   [Configurer l’inscription d’appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Inscrire des appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  
