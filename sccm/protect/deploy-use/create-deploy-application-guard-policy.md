---
title: Créer et déployer une stratégie Windows Defender Application Guard
titleSuffix: Configuraton Manager
description: Créez et déployez une stratégie Windows Defender Application Guard.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7f0a1ccb71abb2fec27e0430bd4195dc85aceae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Créer et déployer une stratégie Windows Defender Application Guard 
*S’applique à : System Center Configuration Manager (Current Branch)*
<!-- 1351960 -->
Vous pouvez créer et déployer des stratégies [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) à l’aide de la protection du point de terminaison Configuration Manager. Ces stratégies permettent de protéger vos utilisateurs en ouvrant les sites web non approuvés dans un conteneur isolé et sécurisé qui n’est pas accessible par les autres parties du système d’exploitation.

## <a name="prerequisites"></a>Prérequis

Pour créer et déployer une stratégie Windows Defender Application Guard, vous devez utiliser la mise à jour Windows 10 Fall Creators Update (1709). De plus, les appareils Windows 10 sur lesquels vous déployez la stratégie doivent être configurés avec une stratégie d’isolement réseau. Pour plus d’informations, consultez [Vue d’ensemble de Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Créez une stratégie et parcourez les paramètres disponibles :

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.
2. Dans l’espace de travail **Biens et conformité**, choisissez **Vue d’ensemble** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie Windows Defender Application Guard**.
4. Utilisez l’[article](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) comme référence pour pouvoir parcourir et configurer les paramètres disponibles. Configuration Manager vous permet de définir certains paramètres de stratégie. Consultez [Paramètres d’interaction de l’hôte](#BKMK_HIS) et [Comportement de l’application](#BKMK_AppB).
5. Dans la page **Définition du réseau**, spécifiez l’identité d’entreprise et définissez les limites du réseau de votre entreprise.

    > [!NOTE]
    > Les PC Windows 10 stockent une seule liste d’isolements réseau sur le client. Vous pouvez créer deux types différents de listes d’isolement réseau et les déployer sur le client :
    >
    >  - Un depuis Protection des informations Windows
    >  - Un depuis Windows Defender Application Guard
    >
    > Si vous déployez les deux stratégies, les listes d’isolements réseau doivent correspondre. Si vous déployez des listes qui ne correspondent pas au même client, le déploiement échoue. Pour plus d’informations, consultez la [documentation sur la protection des informations Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Lorsque vous avez terminé, suivez l’Assistant et déployez la stratégie sur un ou plusieurs appareils 1709 Windows 10.

### <a name="bkmk_HIS"></a> Paramètres d’interaction de l’hôte
Configure les interactions entre les appareils hôtes et le conteneur Application Guard. Avant Configuration Manager version 1802, le comportement des applications et l’interaction des hôtes étaient sous le même onglet **Paramètres**.

- **Presse-papiers** - Sous les paramètres avant Configuration Manager 1802
    - Type de contenu autorisé
        - Texte
        - Images
- **Impression :**
    - Activer l’impression au format XPS
    - Activer l’impression au format PDF
    - Activer l’impression sur des imprimantes locales
    - Activer l’impression sur des imprimantes réseau
- **Graphisme :** (à compter de Configuration Manager version 1802)
    - Accès au processeur de graphisme virtuel
- **Fichiers :** (à compter de Configuration Manager version 1802)
    - Enregistrer les fichiers téléchargés à héberger

### <a name="bkmk_ABS"></a> Paramètres du comportement des applications
Configure le comportement des applications au sein de la session Application Guard. Avant Configuration Manager version 1802, le comportement des applications et l’interaction des hôtes étaient sous le même onglet **Paramètres**.

- **Contenu :**
   - Les sites d'entreprise peuvent charger du contenu externe à l’entreprise, comme des plug-ins tiers.
- **Autres :**
    - Conserver les données de navigateur générées par l’utilisateur
    - Auditer les événements de sécurité dans la session Application Guard isolée



## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur Windows Defender Application Guard : [Vue d’ensemble de Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Questions fréquentes (FAQ) sur Windows Defender Application Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
