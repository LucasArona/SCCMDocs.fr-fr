---
title: 'Tâches courantes de gestion de la compatibilité pour les appareils gérés par le client '
titleSuffix: Configuration Manager
description: Découvrez les paramètres de compatibilité de System Center Configuration Manager en examinant certains scénarios courants.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a06c4294e85d3942ea3c795f3621d15ffb0ad32f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120798"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Tâches courantes de gestion de la compatibilité des appareils avec le client System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique vous propose une introduction à l’utilisation des paramètres de compatibilité de System Center Configuration Manager à travers des exemples de scénarios courants que vous êtes susceptible de rencontrer.  

 Si vous connaissez déjà les paramètres de compatibilité, vous trouverez une documentation détaillée sur toutes les fonctionnalités que vous utilisez dans la section [Éléments de configuration pour les appareils gérés avec le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md).  

 Avant de commencer, lisez [Bien démarrer avec les paramètres de compatibilité](../../compliance/get-started/get-started-with-compliance-settings.md) pour apprendre les notions de base sur les paramètres de compatibilité, et lisez également [Planifier et configurer les paramètres de compatibilité](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) pour implémenter tous les prérequis.  

## <a name="general-information-for-each-scenario"></a>Informations générales pour chaque scénario  
 Dans chaque scénario, vous allez créer un élément de configuration qui effectue une tâche spécifique. Pour ouvrir l’Assistant Création d’élément de configuration, procédez comme suit :  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4.  Sous l’onglet **Général** de l’Assistant Création d’élément de configuration illustré ci-dessous, nommez et décrivez l’élément de configuration, puis choisissez le type d’élément de configuration approprié pour chaque scénario de cette rubrique.  

     ![Affiche la page Général de l’Assistant Création d’élément de configuration.](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Scénarios pour appareils Windows 10 gérés avec le client Configuration Manager  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>Scénario : désactiver l’utilisation de la fonction Bluetooth sur les appareils Windows 10  
 Dans ce scénario, votre service de sécurité a identifié la fonctionnalité Bluetooth des appareils comme un moyen pouvant servir à transmettre des informations sensibles de l’entreprise vers l’extérieur. Vous avez dernièrement mis à niveau tous vos PC vers Windows 10 et décidez de désactiver la fonctionnalité Bluetooth sur ces appareils.  

1. Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Windows 10** , puis cliquez sur **Suivant**.  

2. Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez toutes les plateformes Windows 10.  

3. Dans la page **Paramètres du périphérique** , sélectionnez **Périphérique**, puis cliquez sur **Suivant**.  

4. Dans la page **Périphérique** , sélectionnez la valeur **Interdit** pour **Bluetooth**.  

5. Sélectionnez **Résoudre les paramètres non compatibles** pour faire en sorte que la modification s’applique à tous les appareils Windows 10.  

6. Terminez l’Assistant pour créer l’élément de configuration.  

   Vous pouvez maintenant utiliser les informations contenues dans la rubrique [Tâches courantes de création et de déploiement de bases de référence de configuration avec System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Scénarios pour ordinateurs de bureau et serveurs Windows gérés avec le client Configuration Manager  
 Sur les ordinateurs Mac exécutant le client Configuration Manager, vous avez le choix entre deux options pour évaluer la compatibilité :  

- Évaluer un fichier de préférences (plist) Mac OS X.  

- Utiliser un script personnalisé et évaluer les résultats retournés par le script.  

  Pour plus d’informations, consultez [Guide pratique pour créer des éléments de configuration pour les appareils Mac OS X gérés avec le client System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scénario : corriger une valeur de Registre incorrecte sur les ordinateurs de bureau Windows  
 Dans ce scénario, vous constatez qu’une d’applications métier importante ne fonctionne pas correctement sur certains ordinateurs que vous gérez et qui exécutent Windows 8.1. Après enquête, vous découvrez que le problème est lié à la définition de la clé de Registre **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** , qui a la valeur **0** sur certains ordinateurs. Pour que l’application métier s’exécute correctement, cette valeur doit être égale à **1**.  

 Dans cette procédure, vous allez créer un élément de configuration destiné à rechercher les valeurs de clé de Registre incorrectes et à les corriger automatiquement, le cas échéant.  

1. Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Ordinateurs et serveurs Windows (personnalisés)** , puis cliquez sur **Suivant**.  

2. Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez **Windows 8.1** (pour faire en sorte que l’élément de configuration ne s’applique qu’aux ordinateurs concernés).  

3. Dans la page **Paramètres** , cliquez sur **Nouveau** pour créer un paramètre.  

4. Sous l’onglet **Général** de la boîte de dialogue **Créer un paramètre** , configurez les éléments suivants :  

   -   **Nom** > **Paramètre de l’exemple**  

   -   **Type de paramètre** > **Valeur de Registre**  

   -   **Type de données** > **Entier** (sachant que la valeur ne peut être qu’un nombre)  

   -   **Ruche** > **HKEY_LOCAL_MACHINE**  

   -   **Clé** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Valeur** > **1** (valeur requise)  

5. Sous l’onglet **Règles de compatibilité** de la boîte de dialogue **Créer un paramètre** , cliquez sur **Nouveau**puis, dans la boîte de dialogue **Créer une règle** , configurez les éléments suivants :  

   -   **Nom** > **Règle de l’exemple**  

   -   **Paramètre sélectionné** : vérifiez que le paramètre sélectionné est le **paramètre de l’exemple**.  

   -   **Type de règle** > **Valeur**  

   -   **Le paramètre doit être conforme à la règle suivante** : vérifiez que le nom du paramètre est correct et configurez l’option pour spécifier que la valeur du paramètre doit être égale à **1**.  

   -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** – Cochez cette case pour garantir que Configuration manager rétablira la valeur correcte de la clé de Registre si sa valeur est incorrecte.  

6. Terminez l’Assistant pour créer l’élément de configuration.  

   Vous pouvez maintenant utiliser les informations contenues dans la rubrique [Tâches courantes de création et de déploiement de bases de référence de configuration](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  
