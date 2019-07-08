---
title: 'Tâches courantes de gestion de la compatibilité pour les appareils gérés par le client '
titleSuffix: Configuration Manager
description: Découvrez les paramètres de compatibilité de System Center Configuration Manager en examinant certains scénarios courants.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67a23fd5c1791253a7789fda74a30a0e71566f92
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67550822"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>Tâches courantes de gestion de la compatibilité des appareils avec le client System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article vous donne une présentation de l’utilisation de paramètres de compatibilité de System Center Configuration Manager en vous guidant dans quelques scénarios courants que vous pouvez rencontrer.  

 Si vous connaissez déjà les paramètres de compatibilité, vous trouverez des informations détaillées sur toutes les fonctionnalités que vous utilisez dans [Éléments de configuration pour les appareils gérés avec le client System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items.md).  

 Avant de commencer, lisez [prise en main des paramètres de conformité](../../compliance/get-started/get-started-with-compliance-settings.md) pour apprendre les notions de base sur les paramètres de conformité. Lecture [planifier et configurer les paramètres de conformité](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) pour plus d’informations sur les conditions préalables requises.  

## <a name="general-information-for-each-scenario"></a>Informations générales pour chaque scénario  
 Dans chaque scénario, vous allez créer un élément de configuration qui effectue une tâche spécifique. Pour ouvrir l’Assistant Création d’un élément de Configuration et de prise en main, procédez comme suit :  

1.  Dans la console Configuration Manager, sélectionnez **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

1.  Dans l'onglet **Accueil** , dans le groupe **Créer** , sélectionnez **Créer un élément de configuration**.  

1.  Sur le **général** page de l’Assistant Création d’élément Configuration, illustré dans la capture d’écran suivante, spécifiez un nom et une description pour l’élément de configuration. Puis choisissez le type d’élément de configuration approprié pour chaque scénario dans cet article.  

     ![Page Général de l’Assistant Création d’élément de configuration](/sccm/mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Scénario : Désactiver Bluetooth sur les appareils Windows 10

 Dans ce scénario, votre service de sécurité a identifié la fonctionnalité Bluetooth des appareils comme un moyen pouvant servir à transmettre des informations sensibles de l’entreprise vers l’extérieur. Vous avez récemment mis à niveau tous vos ordinateurs vers Windows 10. Vous décidez de désactiver Bluetooth sur ces appareils.  

1. Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Windows 10** , puis sélectionnez **Suivant**.  

2. Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez toutes les plateformes Windows 10.  

3. Sur le **paramètres du périphérique** page, sélectionnez **appareil**, puis sélectionnez **suivant**.  

4. Dans la page **Périphérique** , sélectionnez la valeur **Interdit** pour **Bluetooth**.  

5. Sélectionnez **Résoudre les paramètres non compatibles** pour faire en sorte que la modification s’applique à tous les appareils Windows 10.  

6. Terminez l’Assistant pour créer l’élément de configuration.  

 Vous pouvez maintenant utiliser les informations contenues dans l’article [Tâches courantes de création et de déploiement de bases de référence de configuration avec System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Scénario : corriger une valeur de Registre incorrecte sur les ordinateurs de bureau Windows

> [!NOTE] 
> Sur les ordinateurs Mac exécutant le client Configuration Manager, vous avez le choix entre deux options pour évaluer la compatibilité :  
> - Évaluer un fichier de préférences (plist) Mac OS X.
> - Utiliser un script personnalisé et évaluer les résultats retournés par le script.  
>
>Pour plus d’informations, consultez [Guide pratique pour créer des éléments de configuration pour les appareils Mac OS X gérés avec le client System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 Dans ce scénario, vous constatez qu’une application line of business importante ne s’exécute pas correctement sur certains ordinateurs Windows 8.1 que vous gérez. Vous découvrez que le problème est lié à la définition de la clé de Registre **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** , qui a la valeur **0** sur certains ordinateurs. Pour que l’application métier s’exécute correctement, cette valeur doit être égale à **1**.  

 Dans cette procédure, vous allez créer un élément de configuration destiné à rechercher les valeurs de clé de Registre incorrectes et à les corriger automatiquement, le cas échéant.  

1. Dans la page **Général** de l’Assistant Création d’élément de configuration, sélectionnez le type d’élément de configuration **Ordinateurs et serveurs Windows (personnalisés)** , puis sélectionnez **Suivant**.  

2. Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez **Windows 8.1** (pour faire en sorte que l’élément de configuration ne s’applique qu’aux ordinateurs concernés).  

3. Dans la page **Paramètres**, sélectionnez **Nouveau** pour créer un paramètre.  

4. Sous l’onglet **Général** de la boîte de dialogue **Créer un paramètre** , configurez ces paramètres :  

   -   **Nom** > **Paramètre de l’exemple**  

   -   **Type de paramètre** > **Valeur de Registre**  

   -   **Type de données** > **Entier** (sachant que la valeur ne peut être qu’un nombre)  

   -   **Ruche** > **HKEY_LOCAL_MACHINE**  

   -   **Clé** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Valeur** > **1** (valeur requise)  

5. Sur le **règles de conformité** onglet de la **créer un paramètre** boîte de dialogue, sélectionnez **New**. Dans le **Create Rule** boîte de dialogue zone, configurez ces paramètres :  

   -   **Nom** > **Règle de l’exemple**  

   -   **Paramètre sélectionné** > Vérifiez que le paramètre sélectionné est le **paramètre de l’exemple**.

   -   **Type de règle** > **Valeur**  

   -   **Le paramètre doit être conforme à la règle suivante** > Vérifiez que le nom du paramètre est correct et configurez l’option pour spécifier que la valeur du paramètre doit être égale à **1**.  

   -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** > Sélectionnez cette case à cocher pour garantir que Configuration manager rétablira la valeur correcte de la clé de Registre si sa valeur est incorrecte.  

6. Terminez l’Assistant pour créer l’élément de configuration.  

 Vous pouvez maintenant utiliser les informations contenues dans l’article [Tâches courantes de création et de déploiement de bases de référence de configuration](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) pour déployer la configuration que vous avez créée sur les appareils.  

## <a name="next-steps"></a>Étapes suivantes

[Créer et déployer des bases de référence de configuration](/sccm/compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines)
