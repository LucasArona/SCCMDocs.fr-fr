---
title: Attestation d’intégrité
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités d’attestation d’intégrité de l’appareil disponibles dans la console Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 116c12d86c097222844e76dde877b674ca7498b9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127114"
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>Attestation d’intégrité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les administrateurs peuvent consulter l’état de l’[attestation d’intégrité des appareils Windows 10](https://technet.microsoft.com/library/mt592023.aspx) dans la console Configuration Manager.  L’attestation de l’intégrité des appareils permet à l’administrateur de s’assurer que les configurations dignes de confiance suivantes de BIOS, de module de plateforme sécurisée (TPM) et de logiciel de démarrage sont activées sur les ordinateurs clients :  

-   Logiciel anti-programme malveillant à lancement anticipé - Un logiciel anti-programme malveillant à lancement anticipé (ELAM) protège votre ordinateur au démarrage et avant l’initialisation de pilotes tiers. [Comment activer le logiciel anti-programme malveillant à lancement anticipé (ELAM)](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Le chiffrement de lecteur BitLocker Windows est un logiciel qui vous permet de chiffrer toutes les données stockées sur le volume hébergeant le système d’exploitation Windows.  [Comment activer BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Démarrage sécurisé - Le démarrage sécurisé est une norme de sécurité développée par des membres du secteur de la fabrication de PC pour s’assurer que votre ordinateur démarre en utilisant uniquement des logiciels approuvés par le fabricant de l’ordinateur. [En savoir plus sur le démarrage sécurisé](https://technet.microsoft.com/library/hh824987.aspx)  
-   Intégrité du code - L’intégrité du code est une fonctionnalité qui améliore la sécurité du système d’exploitation en validant l’intégrité d’un fichier de pilote ou système chaque fois qu’il est chargé en mémoire. [En savoir plus sur l’intégrité du code](https://technet.microsoft.com/library/dd348642.aspx)  

Cette fonctionnalité est disponible pour les PC et les ressources locales gérés par Configuration Manager et les appareils mobiles gérés avec Microsoft Intune. Les administrateurs peuvent spécifier si le signalement s’effectue par le biais du cloud ou de l’infrastructure locale. La surveillance locale de l’attestation d’intégrité des appareils permet à l’administrateur de surveiller les ordinateurs clients sans accès Internet.

## <a name="enable-health-attestation"></a>Activer l’attestation d’intégrité

 **Configuration requise :**  

-   Appareils clients exécutant Windows 10 version 1607 ou Windows Server 2016 version 1607 avec l’option [Attestation d’intégrité de l’appareil](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation) activée.
-   Appareils TPM 1.2 ou TPM 2 compatibles.
-   Lors de l’utilisation de la gestion cloud, communication entre l’agent du client Configuration Manager et le point de gestion avec le service d’attestation d’intégrité (gestion du cloud) via *has.spserv.microsoft.com* (port 443). Localement, le client doit être en mesure de communiquer avec le point de gestion dont l’attestation d’intégrité de l’appareil est activée.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Comment activer la communication avec le service d’attestation d’intégrité sur des ordinateurs clients Configuration Manager

Utilisez cette procédure pour activer la surveillance de l’attestation d’intégrité des appareils qui se connectent à internet.

1.  Dans la console Configuration Manager, choisissez **Administration** > **Vue d’ensemble** > **Paramètres client**.  Sélectionnez l’onglet des paramètres de l’ **Agent ordinateur** .  
2.  Dans la boîte de dialogue **Paramètres par défaut** , sélectionnez **Agent ordinateur** , puis accédez à **Activer la communication avec le service d’attestation d’intégrité**.  
3.  Affectez la valeur **Oui** à **Activer la communication avec le service d’attestation d’intégrité**, puis cliquez sur **OK**.  
4. Ciblez les regroupements d’appareils qui doivent signaler l’intégrité des appareils.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Comment activer la communication avec le service d’attestation d’intégrité local sur des ordinateurs clients Configuration Manager
Utilisez cette procédure pour activer la surveillance de l’attestation d’intégrité des appareils en local qui ne se connectent pas à internet.

À partir de Configuration Manager 1702, l’URL du service d’attestation d’intégrité des appareils en local peut être configurée sur le point de gestion pour prendre en charge les appareils clients sans accès à Internet.

1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Sites**.
2. Cliquez avec le bouton droit sur le site principal ou secondaire avec le point de gestion qui prend en charge des clients d’attestation d’intégrité d’appareils en local, puis sélectionnez **Configurer des composants de site** > **Point de gestion**. La page **Propriétés du composant du point de gestion** s’ouvre.
3. Dans l’onglet **Options avancées**, sélectionnez **Ajouter** et spécifiez une URL de service d’attestation d’intégrité des appareils en local. Vous pouvez ajouter plusieurs URL. Si plusieurs URL locales sont spécifiées, les clients reçoivent le jeu complet et choisissent de façon aléatoire celle à utiliser.
4.  Dans la console Configuration Manager, choisissez **Administration** > **Vue d’ensemble** > **Paramètres client**.  Sélectionnez l’onglet des paramètres de l’ **Agent ordinateur** .  
5.  Faites défiler jusqu’à **Activer la communication avec le service d’attestation d’intégrité**, puis sélectionnez la valeur **Oui**.
7.  Cliquez sur l’option **Utiliser le service d’attestation d’intégrité local**, puis sélectionnez la valeur **Oui**.
8. Ciblez les regroupements d’appareils qui doivent signaler l’intégrité d’appareil avec les paramètres de l’agent client pour activer les rapports d’attestation d’intégrité des appareils.

Vous pouvez également **modifier** ou **supprimer** les URL du service d’attestation d’intégrité des appareils.

> [!NOTE]
> Si vous avez utilisé l’attestation d’intégrité des appareils avant la mise à niveau vers Configuration Manager 1702, les URL locales spécifiées dans les paramètres de l’agent du client sont prérempliées dans les propriétés du point de gestion au cours de la mise à niveau. Les clients locaux continueront d’utiliser l’URL spécifiée dans les paramètres de l’agent client jusqu'à ce qu’ils soient mis à niveau. Ils basculeront ensuite vers une URL spécifiée sur le point de gestion.

## <a name="monitor-device-health-attestation"></a>Surveiller l’attestation d’intégrité de l’appareil Windows

1.  Pour afficher l’attestation d’intégrité de l’appareil, dans la console Configuration Manager, accédez à l’espace de travail **Surveillance** , cliquez sur le nœud **Sécurité** , puis sur **Attestation d’intégrité**.  
2.  L’attestation d’intégrité de l’appareil s’affiche.  

L’attestation d’intégrité des appareils Configuration Manager affiche les informations suivantes :  

-   **État d’attestation d’intégrité** : indique la répartition des appareils en état conforme, non conforme, d’erreur ou inconnu.  
-   **Appareils signalant une attestation d’intégrité** : indique le pourcentage d’appareils signalant l’état d’attestation d’intégrité.  
-   **Appareils non conformes par type de client** : indique la répartition des appareils mobiles et ordinateurs non conformes.  
-   **Principaux paramètres manquants de l’attestation d’intégrité** : indique le nombre d’appareils auxquels un paramètre d’attestation d’intégrité manque, répertoriés par paramètre manquant.

L’état de l’attestation d’intégrité de l’appareil client permet de définir des règles d’accès conditionnel dans des stratégies de conformité pour les appareils gérés par Configuration Manager avec Microsoft Intune. Pour plus d’informations, consultez [Gérer les stratégies de conformité d’appareils dans System Center Configuration Manager](/sccm/protect/deploy-use/device-compliance-policies).  
