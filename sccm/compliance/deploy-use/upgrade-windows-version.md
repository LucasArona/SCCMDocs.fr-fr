---
title: Mettre à niveau des appareils Windows vers une version différente
titleSuffix: Configuration Manager
description: Mettez automatiquement à niveau les appareils qui exécutent Windows 10 Desktop ou Windows 10 Mobile vers une autre édition avec Configuration Manager.
ms.date: 01/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c15e919978ae8458f426511dd9a0e6d7c311b4b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333274"
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>Mettre à niveau des appareils Windows avec la stratégie de mise à niveau d’édition dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


La **stratégie de mise à niveau d’édition** vous permet de mettre automatiquement à niveau les appareils qui exécutent une des versions suivantes de Windows 10 vers une autre édition :

- Windows 10 Desktop
- Windows 10 Mobile

Les chemins de mise à niveau suivants sont pris en charge :

- De Windows 10 Professionnel vers Windows 10 Entreprise
- De Windows 10 Famille vers Windows 10 Éducation
- De Windows 10 Mobile vers Windows 10 Mobile Entreprise

Les appareils doivent être inscrit dans Microsoft Intune ou exécuter le logiciel client Configuration Manager. Cette stratégie n’est actuellement pas compatible avec les PC gérés par gestion MDM locale.

## <a name="before-you-start"></a>Avant de commencer  
 Avant de commencer à mettre à niveau des appareils vers la dernière version, passez en revue les prérequis suivants :  

-   Pour les éditions Desktop de Windows 10 : une clé de produit valide pour installer la nouvelle version de Windows sur tous les appareils que vous ciblez avec la stratégie. Cette clé de produit peut être une clé d’activation multiple (MAK) ou une clé de licence en volume générique (GVLK). La clé GVLK est aussi connue sous le nom de clé d’installation de client de service de gestion de clés (KMS). Pour plus d’informations, consultez [Planifier l’activation en volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Pour obtenir la liste des clés d’installation de client KMS, consultez [l’Annexe A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) du guide d’activation de Windows Server. <!--496871-->  

-   Pour Windows 10 Mobile : un fichier de licence XML du Centre de gestion des licences en volume (VLSC). Ce fichier contient les informations de licence de la nouvelle version de Windows sur tous les appareils que vous ciblez avec la stratégie.

- Pour gérer ce type de stratégie, vous devez avoir le rôle de sécurité **Administrateur complet** de Configuration Manager.

## <a name="configure-the-edition-upgrade-policy"></a>Configurer la stratégie de mise à niveau d’édition  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Mise à niveau de l'édition Windows 10**.  

3.  Sous l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie de mise à niveau d’édition**.  

4.  Cliquez sur **Créer une stratégie**.  

5.  Dans la page **Général** de l’ **Assistant Création de stratégie de mise à niveau d’édition**, spécifiez les informations suivantes :  

    -   **Nom** : Entrez un nom pour la stratégie de mise à niveau d’édition  

    -   **Description** (facultatif) : Si vous le souhaitez, entrez une description de la stratégie pour l’identifier dans la console Intune  

    -   **Référence pour mettre à niveau l’appareil vers** : Dans la liste déroulante, sélectionnez la version cible de Windows 10 Desktop ou Windows 10 Mobile  

    -   **Informations sur la licence** : sélectionnez une des options suivantes :  

        -   **Clé de produit** : Entrez une clé de produit valide pour l’édition cible de Windows 10 Desktop  

            > [!NOTE]  
            >  Une fois que vous avez créé une stratégie contenant une clé de produit, vous ne pouvez plus modifier la clé de produit. Configuration Manager masque la clé pour des raisons de sécurité. Pour changer la clé de produit, vous devez entrer à nouveau toute la clé.  

        -   **Fichier de licence** : Cliquez sur **Parcourir** pour sélectionner un fichier de licence valide au format XML. Configuration Manager utilise ce fichier de licence pour mettre à niveau les appareils Windows 10 Mobile.  

6.  Effectuez toutes les étapes de l'Assistant.  


## <a name="deploy-the-edition-upgrade-policy"></a>Déployer la stratégie de mise à niveau d’édition  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Mise à niveau de l'édition Windows 10**.  

3.  Sélectionnez la stratégie de mise à niveau d’édition de Windows 10 que vous voulez déployer puis, dans l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

4.  Dans la boîte de dialogue **Déployer la stratégie de mise à niveau d’édition Windows 10**, choisissez d’abord le regroupement sur lequel vous voulez déployer la stratégie. Sélectionnez la planification selon laquelle le client évalue la stratégie, puis cliquez sur **OK**. Pour les PC gérés par le client Configuration Manager, vous devez déployer la stratégie sur un regroupement d’appareils. Pour les PC inscrits dans Intune, vous pouvez déployer la stratégie sur un regroupement d’utilisateurs ou d’appareils. 



## <a name="next-steps"></a>Étapes suivantes

Surveillez ce déploiement à partir du nœud **Déploiements** de l’espace de travail **Monitoring** . Si des erreurs vous indiquent un échec de déploiement, par exemple :
- **Ne s’applique pas à cet appareil**
- **Échec de la conversion du type de données**

Ces erreurs ne signifient pas que le déploiement a échoué. Vérifiez que la mise à niveau a réussi sur le PC ciblé.

Une fois que le client a évalué la stratégie ciblée, il est redémarré dans les deux heures pour appliquer la mise à niveau. Assurez-vous d’informer les utilisateurs sur lesquels vous déployez la stratégie ou planifiez l’exécution de la stratégie en dehors des heures de travail des utilisateurs.

Si l’erreur suivante s’affiche dans **DcmWmiProvider.log** sur le client, vérifiez que vous utilisez la clé appropriée pour votre scénario d’activation. Pour plus d'informations, consultez la section [Avant de commencer](#before-you-start). Si vous utilisez un service de gestion de clés pour l’activation, vérifiez que vous utilisez une [clé d’installation du client KMS](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys).  <!-- 496871 -->   

`Failed to execute CheckApplicabilityMethod with error = 0x80041001 OsEditionUpgradeProvider`
