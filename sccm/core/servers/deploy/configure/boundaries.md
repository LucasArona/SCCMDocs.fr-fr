---
title: Définir des limites
titleSuffix: Configuration Manager
description: Découvrez comment définir les emplacements réseau sur votre intranet pouvant contenir des appareils que vous souhaitez gérer.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e27bce7576f6d96a8e8af95fa5df69dd39c05cd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344328"
---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>Définir des emplacements réseau comme limites pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les limites de Configuration Manager sont des emplacements sur votre réseau contenant des appareils que vous souhaitez gérer. La limite sur laquelle se trouve un appareil est équivalente au site Active Directory ou à l’adresse IP réseau identifiée par le client Configuration Manager installé sur l’appareil.
 - Vous pouvez créer manuellement des limites individuelles. Cependant, Configuration Manager ne prend pas en charge l’entrée directe d’un sur-réseau en tant que limite. À la place, utilisez le type de limite de la plage d'adresses IP.
 - Vous pouvez configurer la méthode de [découverte de forêts Active Directory](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) afin de détecter automatiquement et de créer des limites pour chaque sous-réseau IP et site Active Directory ainsi découverts. Lorsque la fonctionnalité de découverte de forêts Active Directory identifie un sur-réseau attribué à un site Active Directory, Configuration Manager convertit le sur-réseau en limite de plage d'adresses IP.  

Il n’est pas rare qu’un appareil utilise une adresse IP dont l’administrateur Configuration Manager n’a pas connaissance. En cas de doute sur l’emplacement réseau d’un appareil, confirmez l’emplacement signalé par l’appareil en exécutant la commande **IPCONFIG** sur l’appareil.  

Quand vous créez une limite, elle reçoit automatiquement un nom basé sur son type et son étendue. Ce nom ne peut pas être modifié. Au lieu de cela, vous pouvez spécifier une description permettant de l’identifier dans la console Configuration Manager.  

Chaque limite est utilisable par tous les sites de votre hiérarchie. Après avoir créé une limite, vous pouvez modifier ses propriétés pour effectuer les opérations suivantes :  
-   Ajouter la limite à un ou plusieurs groupes de limites.  
-   Changer le type ou la portée de la limite.  
-   Afficher l’onglet **Systèmes de site** des limites pour savoir quels serveurs de système de site (points de distribution, points de migration d’état et points de gestion) sont associés à la limite.  

## <a name="to-create-a-boundary"></a>Pour créer une limite  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** > **Limites**  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer Boundary.**  

3.  Dans l'onglet **Général** de la boîte de dialogue Créer une limite, vous pouvez spécifier une **Description** pour identifier une limite par un nom convivial ou une référence.  

4.  Sélectionnez un **Type** pour cette limite :  

    -   Si vous sélectionnez **Sous-réseau IP**, vous devez spécifier un **ID de sous-réseau** pour cette limite.  
        > [!TIP]  
        >  Vous pouvez spécifier le **Réseau** et le **Masque de sous-réseau** pour que l' **ID de sous-réseau** soit automatiquement spécifié. Lorsque vous enregistrez la limite, seule la valeur d'ID de sous-réseau est enregistrée.  

    -   Si vous sélectionnez **Site Active Directory**, vous devez spécifier ou **Parcourir** vers un site Active Directory dans la forêt locale du serveur de site.  

        > [!IMPORTANT]  
        >  Lorsque vous spécifiez un site Active Directory pour une limite, la limite inclut chaque sous-réseau IP membre de ce site Active Directory. Si la configuration du site Active Directory est modifiée dans Active Directory, les emplacements réseau inclus dans cette limite sont également modifiés.  

    -   Si vous sélectionnez **Préfixe IPv6**, vous devez spécifier un **Préfixe** au format de préfixe IPv6.  

    -   Si vous sélectionnez **Plage d'adresses IP**, vous devez spécifier une **Adresse IP de début** et une **Adresse IP de fin** qui inclut la partie d'un sous-réseau IP ou inclut plusieurs sous-réseaux IP.    

5.  Cliquez sur **OK** pour enregistrer la nouvelle limite.  

## <a name="to-configure-a-boundary"></a>Pour configurer une limite  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de la hiérarchie** > **Limites**  

2.  Sélectionnez la limite à modifier.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** de la limite, sélectionnez l'onglet **Général** pour modifier la **Description** ou le **Type** de la limite. Vous pouvez également modifier l'étendue d'une limite en modifiant les emplacements réseau pour la limite. Par exemple, pour une limite de site Active Directory, vous pouvez spécifier un nouveau nom de site Active Directory.  

5.  Sélectionnez l'onglet **Systèmes de site** pour afficher les systèmes de site associés à cette limite. Vous ne pouvez pas modifier cette configuration à partir des propriétés d'une limite.  

    > [!TIP]  
    >  Pour qu'un serveur de système de site soit référencé comme système de site pour une limite, il faut que le serveur de système de site soit associé en tant que serveur de système de site pour au moins un groupe de limites comportant cette limite. Vous pouvez configurer cela sous l'onglet **Références** d'un groupe de limites.  

6.  Sélectionnez l'onglet **Groupes de limites** pour modifier l'appartenance au groupe de limites pour cette limite :  

    -   Pour ajouter cette limite à un ou plusieurs groupes de limites, cliquez sur **Ajouter**, cochez la case d'un ou plusieurs groupes de limites, puis cliquez sur **OK**.  

    -   Pour supprimer cette limite d'un groupe de limites, sélectionnez le groupe de limites, puis cliquez sur **Supprimer**.  

7.  Cliquez sur **OK** pour fermer les propriétés de la limite et enregistrer la configuration.  
