---
title: Windows Defender - Protection avancée contre les menaces
titleSuffix: Configuration Manager
description: Découvrez comment gérer et surveiller le nouveau service Windows Defender - Protection avancée contre les menaces qui aide les entreprises à contrer les attaques avancées.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10d746f88d0e7b869e2b73d389944f3b382d687d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348383"
---
# <a name="windows-defender-advanced-threat-protection"></a>Windows Defender - Protection avancée contre les menaces

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1606 de Configuration Manager (Current Branch), Endpoint Protection facilite la gestion et le monitoring du service [Windows Defender - Protection avancée contre les menaces (ATP)](http://aka.ms/technet-wdatp). Windows Defender ATP permet aux entreprises de détecter, d’investiguer et de répondre aux attaques avancées sur leur réseau.  Les stratégies Configuration Manager ou Microsoft Intune facilitent l’intégration et le monitoring des appareils gérés qui exécutent Windows 10 version 1607 (build 14328) ou ultérieure.

Windows Defender ATP est un service disponible dans le [Centre de sécurité Windows Defender](https://securitycenter.windows.com). Grâce à l’ajout et au déploiement d’un fichier de configuration de l’intégration du client, Configuration Manager peut surveiller l’état du déploiement ainsi que l’intégrité de l’agent Windows Defender ATP. Windows Defender ATP est pris en charge sur les PC exécutant le client Configuration Manager ou gérés par Microsoft Intune, mais les ordinateurs gérés par la gestion MDM hybride d’Intune ne sont pas pris en charge.

 **Conditions préalables**  

-   Abonnement au service en ligne Windows Defender - Protection avancée contre les menaces  
-   Ordinateurs clients exécutant Windows 10 version 1607 ou ultérieure  
-   Ordinateurs clients exécutant la version 1610 de Configuration Manager, un agent client ultérieur ou qui sont gérés par Microsoft Intune

## <a name="how-to-create-an-onboarding-configuration-file"></a>Guide pratique pour créer un fichier de configuration d’intégration  

 1.  Connectez-vous au [service en ligne Windows Defender ATP](https://securitycenter.windows.com/).   

 2.  Cliquez sur l’élément de menu **Gestion du point de terminaison**.  

 3.  Sélectionnez **System Center Configuration Manager (Current Branch) version 1606**, puis cliquez sur **Télécharger le package**.  

 4.  Téléchargez le fichier d’archive compressé (.zip) et extrayez son contenu.

> [!IMPORTANT]
> Le fichier de configuration de Windows Defender ATP contient des informations sensibles qui doivent être conservées de manière sécurisée.

## <a name="onboard-devices-for-windows-defender-atp"></a>Intégrer des appareils pour Windows Defender ATP  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Endpoint Protection** > **Stratégies Windows Defender ATP**, puis cliquez sur **Créer une stratégie Windows Defender ATP**. L’Assistant Création d’une stratégie Windows Defender ATP s’ouvre.  

2.  Tapez un **nom** et une **description** pour la nouvelle stratégie Windows Defender ATP, puis sélectionnez **Intégration**. Cliquez sur **Suivant**.  

3.  Sélectionnez **Parcourir** pour accéder au fichier de configuration fourni par le locataire du service cloud Windows Defender ATP de votre organisation. Cliquez sur **Suivant**.  

4.  Spécifiez les exemples de fichiers collectés et partagés à partir des appareils gérés pour les besoins d’analyse.  

    -   **Aucun**   

    -   **Tous les types de fichiers**  

     Cliquez sur **Suivant**.  

5.  Passez en revue les informations de résumé et terminez l’Assistant.  

6.  Vous pouvez maintenant déployer la stratégie Windows Defender ATP sur les ordinateurs clients gérés en cliquant sur **Déployer**.  

## <a name="monitor-windows-defender-atp"></a>Surveiller Windows Defender ATP  

1.  Dans la console Configuration Manager, accédez à **Surveillance** > **Vue d’ensemble** > **Sécurité**, puis cliquez sur **Windows Defender ATP**.  

2.  Examinez le tableau de bord Windows Defender - Protection avancée contre les menaces.  

    -   **État du déploiement de l’agent Windows Defender** : nombre et pourcentage d’ordinateurs clients gérés éligibles avec la stratégie Windows Defender ATP intégrée active.  

    -   **Intégrité de l’agent Windows Defender ATP** : pourcentage d’ordinateurs clients qui signalent l’état de l’agent Windows Defender ATP.  

        -   **Sain** : fonctionnement correct.  

        -   **Inactif** : aucune donnée n’a été envoyée au service durant la période.  

        -   **État de l’agent** : le service système de l’agent dans Windows n’est pas en cours d’exécution.  

        -   **Non intégré** : la stratégie a été appliquée, mais l’agent n’a pas signalé de stratégie intégrée.  


## <a name="how-to-create-and-deploy-an-offboarding-configuration-file"></a>Guide pratique pour créer et déployer un fichier de configuration de désintégration  

1.  Connectez-vous au [service en ligne Windows Defender ATP](https://securitycenter.windows.com/).   

2.  Cliquez sur l’élément de menu **Gestion du point de terminaison**.  

3.  Sélectionnez **System Center Configuration Manager (Current Branch) version 1606**, puis cliquez sur **Désintégration de point de terminaison**.  

4.  Téléchargez le fichier d’archive compressé (.zip) et extrayez son contenu. Les fichiers de désintégration sont valides pendant 30 jours.

5.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Endpoint Protection** > **Stratégies Windows Defender ATP**, puis cliquez sur **Créer une stratégie Windows Defender ATP**. L’Assistant Création d’une stratégie Windows Defender ATP s’ouvre.  

6.  Tapez un **Nom** et une **Description** pour la stratégie Windows Defender ATP, puis sélectionnez **Désintégration**. Cliquez sur **Suivant**.  

7.  Sélectionnez **Parcourir** pour accéder au fichier de configuration fourni par le locataire du service cloud Windows Defender ATP de votre organisation. Cliquez sur **Suivant**.  

8.  Passez en revue les informations de résumé et terminez l’Assistant.  

9.  Vous pouvez maintenant déployer la stratégie Windows Defender ATP sur les ordinateurs clients gérés en cliquant sur **Déployer**.  

> [!IMPORTANT]
> Les fichiers de configuration de Windows Defender ATP contiennent des informations sensibles qui doivent être conservées de manière sécurisée.

[Windows Defender - Protection avancée contre les menaces](https://technet.microsoft.com/itpro/windows/keep-secure/windows-defender-advanced-threat-protection)

[Résoudre les problèmes liés à l’intégration de Windows Defender - Protection avancée contre les menaces](https://technet.microsoft.com/itpro/windows/keep-secure/troubleshoot-onboarding-windows-defender-advanced-threat-protection)
