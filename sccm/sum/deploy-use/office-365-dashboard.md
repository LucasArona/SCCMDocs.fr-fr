---
title: Tableau de bord Gestion des clients Office 365
titleSuffix: Configuration Manager
description: Consulter les informations sur un client Office 365 dans le tableau de bord Gestion des clients Office 365
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/10/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.collection: M365-identity-device-management
ms.openlocfilehash: aff55aee5b2eaa584a6161452b4a232fab07412a
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802170"
---
# <a name="office-365-client-management-dashboard"></a>Tableau de bord Gestion des clients Office 365

À compter de Configuration Manager version 1802, vous pouvez consulter les informations sur le client Office 365 dans le tableau de bord Gestion des clients Office 365. Le tableau de bord Gestion des clients Office 365 affiche une liste des appareils concernés quand des sections de graphe sont sélectionnées. <!--1357281 -->

## <a name="prerequisites"></a>Prérequis

Les données affichées dans le tableau de bord Gestion des clients Office 365 sont issues de l’inventaire matériel. Pour permettre l’affichage des données dans ce tableau de bord, activez l’inventaire matériel et sélectionnez la classe d’inventaire matériel **Configurations Office 365 ProPlus**.
 
1. Activez l’inventaire matériel si vous ne l’avez pas encore fait. Pour plus d’informations, consultez [Configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client** > **Paramètres client par défaut**.  
3. Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  
4. Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  
5. Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  
6. Dans la boîte de dialogue **Classes d’inventaire matériel**, sélectionnez **Configurations Office 365 ProPlus**.  
7. Cliquez sur **OK** pour enregistrer vos modifications et fermer la boîte de dialogue **Classes d'inventaire matériel** . 

Le tableau de bord Gestion des clients Office 365 commence à afficher des données dès qu’un inventaire matériel est signalé.

## <a name="viewing-the-office-365-client-management-dashboard"></a>Affichage du tableau de bord Gestion des clients Office 365

Pour afficher le tableau de bord Gestion des clients Office 365 dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**. En haut du tableau de bord, utilisez le paramètre de liste déroulante **Regroupement** pour filtrer les données de tableau de bord selon les membres d’un regroupement spécifique. À compter de Configuration Manager version 1802, le tableau de bord Gestion des clients Office 365 affiche une liste des appareils concernés quand des sections de graphe sont sélectionnées.

Le tableau de bord Gestion des clients Office 365 fournit des graphiques pour les informations suivantes :

- Nombre de clients Office 365
- Versions du client Office 365
- Langues du client Office 365
- Canaux du client Office 365 Pour plus d’informations, consultez [Présentation des canaux de mise à jour pour Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="bkmk_o365_readiness"></a> Intégration pour Office 365 ProPlus Readiness
<!--3735402-->
À compter de Configuration Manager version 1902, vous pouvez utiliser le tableau de bord pour identifier les appareils avec une confiance élevée qui sont prêts à être mis à niveau vers Office 365 ProPlus. Cette intégration fournit des insights sur les éventuels problèmes de compatibilité avec les compléments et macros Office utilisés dans votre environnement. Ensuite, utilisez Configuration Manager pour déployer Office sur les appareils prêts.

Le tableau de bord de gestion du client Office 365 présente maintenant une nouvelle vignette, **Office 365 ProPlus Upgrade Readiness**. Cette vignette est un graphique à barres des appareils dans les états suivants :
- Non évalué
- Prêt pour la mise à niveau
- Révision nécessaire

Sélectionnez un état pour obtenir une liste d’appareils. Ce rapport de préparation présente plus de détails sur les appareils. Il présente des colonnes pour l’état de compatibilité des compléments et des macros Office.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Conditions préalables à l’intégration Office 365 ProPlus Readiness

- Activez l’inventaire matériel dans les paramètres du client. Pour plus d’informations, consultez la section [Conditions préalables](#prerequisites).  

- L’appareil nécessite une connectivité au réseau de distribution de contenu (CDN) Office pour télécharger un fichier de préparation de complément. Pour plus d’informations, consultez [Réseaux de distribution de contenu](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Si l’appareil ne peut pas télécharger ce fichier, l’état des compléments est *Révision nécessaire*.  

    > [!Note]  
    > Aucune donnée n’est envoyée à Microsoft pour cette fonctionnalité.  

### <a name="bkmk_ort"></a> Préparation détaillée des macros

Par défaut, l’agent d’analyse regarde la liste des fichiers les plus récemment utilisés (MRU) sur chaque appareil. Il compte les fichiers de cette liste qui prennent en charge les macros. Ces fichiers incluent les types suivants :
- Formats de fichier Office prenant en charge les macros, comme les classeurs Excel prenant en charge les macros (.xlsm) ou les documents Word prenant en charge les macros (.docm)  
- Formats Office plus anciens qui n’indiquent pas de contenu de macro. Par exemple, un classeur Excel 97-2003 (.xls).

Si vous avez besoin d’une évaluation plus détaillée, déployez le **Readiness Toolkit Office**. Cet outil analyse le code dans un fichier de macro. Il vérifie s’il existe des problèmes de compatibilité potentiels. Par exemple, le fichier utilise une fonction qui a changé dans une version plus récente d’Office. Après avoir exécuté le Readiness Toolkit Office, Configuration Manager peut utiliser ses résultats. Ces données supplémentaires améliorent le calcul de la préparation des appareils. Pour plus d’informations, consultez [Utiliser le Readiness Toolkit pour évaluer la compatibilité des applications pour Office 365 ProPlus](http://aka.ms/readinesstoolkit).

## <a name="next-steps"></a>Étapes suivantes

[Gérer Office 365 ProPlus avec Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates)