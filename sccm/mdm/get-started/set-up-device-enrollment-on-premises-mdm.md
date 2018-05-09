---
title: "Configurer l'inscription d'appareils "
titleSuffix: Configuration Manager
description: Accordez aux utilisateurs l’autorisation d’inscrire leurs appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d0424b662df4baba7374685dd7631347501352c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurer l’inscription d’appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour permettre aux utilisateurs d’inscrire leurs appareils pour la gestion des appareils mobiles locale dans System Center Configuration Manager, vous devez leur accorder l’autorisation de le faire. Pour accorder aux utilisateurs l’autorisation d’inscrire des appareils, effectuez les tâches ci-dessous.

-   [Créer un profil d’inscription qui permet aux utilisateurs d’inscrire des appareils récents](#bkmk_createProf)  

-   [Définir des paramètres du client supplémentaires pour des périphériques inscrits](#bkmk_addClient)  

-   [Permettre aux utilisateurs de recevoir le profil d’inscription des appareils récents](#bkmk_enableUsers)  

-   [Stocker le certificat racine sur les appareils à inscrire](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> Créer un profil d’inscription qui permet aux utilisateurs d’inscrire des appareils récents  
 Pour transmettre en mode push les paramètres nécessaires pour permettre aux utilisateurs d’inscrire des appareils récents, vous pouvez ajouter un nouveau profil d’inscription aux paramètres client par défaut, qui est appliqué à tous les utilisateurs détectés dans le site Configuration Manager.  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Vue d’ensemble** > **Paramètres client**, ouvrez **Paramètres client par défaut**, puis sélectionnez **Inscription**.  

2.  Sous Paramètres du périphérique, spécifiez l’intervalle d’interrogation pour les appareils récents.  

3.  Sous Paramètres utilisateur, sélectionnez **Oui** pour **Autoriser les utilisateurs à inscrire des appareils récents**.  

4.  En regard de **Profil d’inscription des appareils récents**, cliquez sur **Définir un profil**, puis sur **Créer**.  

5.  Dans Créer un profil d’inscription, tapez un nom pour le profil d’inscription et choisissez le code de site de gestion que vous souhaitez que les utilisateurs ayant le profil d’inscription utilisent. Cliquez sur **OK** plusieurs fois pour quitter la page Paramètres par défaut.  

> [!NOTE]  
>  Si vous souhaitez déployer le profil d’inscription vers une partie des utilisateurs découverts, vous pouvez utiliser un regroupement d’utilisateurs et créer des paramètres client personnalisés à déployer dans ce regroupement. Pour plus d’informations sur la création de paramètres client personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

##  <a name="bkmk_addClient"></a> Définir des paramètres du client supplémentaires pour des périphériques inscrits  
 En plus de définir le profil d’inscription pour des périphériques modernes, vous pouvez définir des paramètres du client supplémentaires pour la configuration de périphériques quand ils sont inscrits.  Pour plus d’informations sur la configuration des paramètres client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

 Tous les paramètres client ne sont pas disponibles pour la gestion des appareils mobiles locale. La version Current Branch de Configuration Manager prend en charge les paramètres client suivants pour la gestion des appareils mobiles locale :  

-   Inscription - Ces paramètres spécifient le profil d’inscription de périphériques gérés. Pour plus d’informations sur la façon de configurer un profil d’inscription, consultez [Créer un profil d’inscription qui permet aux utilisateurs d’inscrire des appareils récents](#bkmk_createProf).  

-   Stratégie client - Ces paramètres spécifient la fréquence de téléchargement de la stratégie client sur le périphérique. Vous pouvez également activer des paramètres pour cibler des utilisateurs avec une interrogation de stratégie. Pour plus d’informations sur les paramètres de stratégie client, consultez la section Stratégie du client dans [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

-   Déploiement de logiciels - Ce paramètre définit l’intervalle d’évaluation des périphériques clients pour les déploiements de logiciels. Pour plus d’informations sur les paramètres de déploiement de logiciels, consultez la section Déploiement logiciel dans [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

    > [!NOTE]  
    >  Pour la gestion des appareils mobiles locale, les paramètres de déploiement de logiciels peuvent uniquement servir comme paramètres client par défaut. Vous ne pouvez pas utiliser les paramètres de déploiement de logiciels avec des paramètres client personnalisés dans la version Current Branch de Configuration Manager.  

##  <a name="bkmk_enableUsers"></a> Permettre aux utilisateurs de recevoir le profil d’inscription des appareils récents  
 Pour que les utilisateurs reçoivent les paramètres client modifiés avec le profil d’inscription pour la gestion des appareils mobiles locale, ils doivent être découverts par le biais de la méthode de découverte Active Directory. Pour vous assurer que toute personne ayant besoin du profil d’inscription l’obtient, exécutez la découverte des utilisateurs Active Directory. Pour obtenir des instructions sur la façon de découvrir des utilisateurs, consultez [Exécuter la découverte pour System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

##  <a name="bkmk_storeCert"></a> Stocker le certificat racine sur les appareils à inscrire  
 Les utilisateurs d’appareils appartenant à un domaine auront probablement déjà le certificat racine requis pour établir des communications fiables avec les serveurs hébergeant les rôles de système de site, car la racine a été émise dans le cadre du processus de jonction de domaine Active Directory. Vous devez installer manuellement le certificat racine sur les ordinateurs et les appareils mobiles qui ne sont pas joints à un domaine pour que l’inscription ait lieu. Ces appareils n’auront pas automatiquement le certificat racine nécessaire.  

 Vous devez fournir le fichier de certificat exporté à l’appareil pour l’installation manuelle via e-mail, OneDrive, carte SD, clé USB ou toute autre méthode qui répond le mieux à vos besoins.  

 Le certificat racine que vous devez utiliser sur les appareils est celui que vous avez exporté dans [Exporter le certificat ayant la même racine que le certificat de serveur web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

1.  Sur l’appareil à inscrire, recherchez le fichier de certificat racine et double-cliquez dessus.  

2.  Dans la fenêtre Certificat, cliquez sur **Installer un certificat**.  

3.  Dans l’Assistant Importation de certificat, sélectionnez **Ordinateur local**et cliquez sur **Suivant**.  

4.  Dans la fenêtre Contrôle de compte d’utilisateur, cliquez sur **Oui**.  

5.  Sélectionnez **Placer tous les certificats dans le magasin suivant**, puis cliquez sur **Parcourir**.  

6.  Cliquez sur **Autorités de certification racine de confiance**, sur **OK**, puis sur **Suivant**.  

7.  Cliquez sur **Terminer**.  
