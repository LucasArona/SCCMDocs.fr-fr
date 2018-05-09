---
title: Méthodes d'installation du client
titleSuffix: Configuration Manager
description: Découvrez les méthodes d’installation du client Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e437709ec1b721cf9ca597bdc944bcce6da9b0f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>Méthodes d’installation du client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser différentes méthodes pour installer le logiciel client Configuration Manager. Utilisez une ou plusieurs méthodes combinées. Cet article décrit chaque méthode de sorte que vous puissiez vous approprier celle qui convient le mieux à votre organisation.  

## <a name="client-push-installation"></a>Installation poussée du client  

**Plateforme cliente prise en charge :** Windows  

#### <a name="advantages"></a>Avantages  

-   Peut être utilisée pour installer le client sur un seul ordinateur, un regroupement d'ordinateurs ou pour les résultats d'une requête.  

-   Peut être utilisée pour installer automatiquement le client sur tous les ordinateurs découverts.  

-   Utilise automatiquement les propriétés d'installation du client définies sous l'onglet **Client** de la boîte de dialogue **Propriétés de l'installation poussée du client** .  

#### <a name="disadvantages"></a>Inconvénients  

-   Une installation poussée vers des regroupements volumineux peut entraîner un trafic réseau excessif.  

-   Peut être utilisée uniquement sur les ordinateurs ayant été découverts par Configuration Manager.  

-   Ne peut pas être utilisée pour installer des clients dans un groupe de travail.  

-   Vous devez spécifier un compte d'installation poussée du client disposant des droits d'administration sur l'ordinateur client souhaité.  

-   Le pare-feu Windows doit être configuré avec des exceptions sur les ordinateurs clients.   

-   Vous ne pouvez pas annuler une installation Push du client. Configuration Manager tente d’installer le client sur toutes les ressources découvertes. En cas d’échec, il renouvelle les tentatives pendant sept jours, au maximum.  

Pour plus d’informations, consultez [Comment installer des clients selon la méthode d’installation Push du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).  



## <a name="software-update-point-based-installation"></a>Installation basée sur un point de mise à jour logicielle  

**Plateforme cliente prise en charge :** Windows  

#### <a name="advantages"></a>Avantages  

-   Peut utiliser votre infrastructure de mises à jour logicielles existante pour gérer le logiciel client.  

-   Si Windows Server Update Services (WSUS) et les paramètres de stratégie de groupe d’Active Directory Domaine Services sont correctement configurés, il peut installer automatiquement le logiciel client sur de nouveaux ordinateurs.  

-   N’exige pas la découverte des ordinateurs avant l’installation du client.  

-   Les ordinateurs peuvent lire les propriétés de l'installation du client ayant été publiées dans les services de domaine Active Directory.  

-   Si le client est supprimé, cette méthode le réinstalle.  

-   Ne nécessite pas de configuration ni la présence d’un compte d'installation pour l’ordinateur client choisi.  

#### <a name="disadvantages"></a>Inconvénients  

-   Nécessite une infrastructure de mises à jour logicielles opérationnelle.  

-   Doit utiliser le même serveur pour l’installation du client et les mises à jour logicielles. Ce serveur doit résider sur un site principal.  

-   Pour installer de nouveaux clients, vous devez configurer un objet de stratégie de groupe dans Active Directory Domain Services avec le port et le point de mise à jour logicielle actifs du client.  

-   Si le schéma Active Directory n’est pas étendu pour Configuration Manager, vous devez utiliser les paramètres de stratégie de groupe pour fournir les propriétés d’installation du client aux ordinateurs.  

Pour plus d’informations, consultez [Comment installer des clients via une installation basée sur des mises à jour logicielles](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  



## <a name="group-policy-installation"></a>Installation via la stratégie de groupe  

**Plateforme cliente prise en charge :** Windows  

#### <a name="advantages"></a>Avantages  

-   N’exige pas la découverte des ordinateurs avant l’installation du client.  

-   Peut être utilisée pour l'installation de nouveaux clients ou pour les mises à niveau.  

-   Les ordinateurs peuvent lire les propriétés de l'installation du client ayant été publiées dans les services de domaine Active Directory.  

-   Ne nécessite pas de configuration ni la présence d’un compte d'installation pour l’ordinateur client choisi.  

#### <a name="disadvantages"></a>Inconvénients  

-   L’installation simultanée d’un grand nombre de clients peut en engendrer un trafic réseau important.  

-   Si le schéma Active Directory n’est pas étendu pour Configuration Manager, vous devez utiliser les paramètres de stratégie de groupe pour ajouter les propriétés d’installation du client aux ordinateurs de votre site.  

Pour plus d’informations, consultez [Comment installer des clients à l’aide d’une stratégie de groupe](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientGP).  



## <a name="logon-script-installation"></a>Installation via un script d'ouverture de session  

**Plateforme cliente prise en charge :** Windows  

#### <a name="advantages"></a>Avantages  

-   N’exige pas la découverte des ordinateurs avant l’installation du client.  

-   Prend en charge les propriétés de ligne de commande de CCMSetup.  

#### <a name="disadvantages"></a>Inconvénients  

-   L’installation simultanée d’un grand nombre de clients sur une courte période peut engendrer un trafic réseau important.  

-   Si certains utilisateurs ne se connectent pas fréquemment au réseau, l’installation sur tous les ordinateurs clients peut prendre beaucoup de temps.  

Pour plus d’informations, consultez [Comment installer des clients à l’aide de scripts d’ouverture de session](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientLogonScript).  



## <a name="manual-installation"></a>Installation manuelle  

**Plateformes clientes prises en charge :** Windows, UNIX/Linux, Mac OS X  

#### <a name="advantages"></a>Avantages  

-   N’exige pas la découverte des ordinateurs avant l’installation du client.  

-   Peut être utile dans le cadre de tests.  

-   Prend en charge les propriétés de ligne de commande de CCMSetup.  

#### <a name="disadvantages"></a>Inconvénients  

-   Aucune automatisation, peut prendre du temps.  

Pour plus d’informations sur la façon d’installer manuellement le client sur chaque plateforme, consultez les articles suivants :  

-   [Guide pratique pour déployer des clients sur des ordinateurs Windows](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)  

-   [Guide pratique pour déployer des clients sur des serveurs UNIX et Linux](/sccm/core/clients/deploy/deploy-clients-to-unix-and-linux-servers)  

-   [Guide pratique pour déployer des clients sur des ordinateurs Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  



## <a name="microsoft-intune-mdm-installation"></a>Installation de Microsoft Intune MDM

**Plateformes clientes prises en charge :** Windows 10

#### <a name="advantages"></a>Avantages  

-   N’exige pas la découverte des ordinateurs avant l’installation du client.  

-   Ne nécessite pas de configuration ni la présence d’un compte d'installation pour l’ordinateur client choisi.  

-   Peut utiliser l’authentification moderne avec Azure Active Directory.  

-   Peut installer et attribuer des ordinateurs sur Internet.  

-   Peut être automatisée avec Windows AutoPilot et Microsoft Intune pour la cogestion.  

#### <a name="disadvantages"></a>Inconvénients  

-   Nécessite des technologies supplémentaires en dehors de Configuration Manager.  

-   Exige que l’appareil ait accès à Internet, même s’il n’est pas basé sur Internet.  

Pour plus d’informations, consultez les articles suivants :  

-   [Guide pratique pour installer des clients sur des appareils Windows gérés par Intune MDM](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm)  

-   [Installer et affecter des clients Windows 10 Configuration Manager à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

