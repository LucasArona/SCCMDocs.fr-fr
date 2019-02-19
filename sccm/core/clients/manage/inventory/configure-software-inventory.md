---
title: Configurer l’inventaire logiciel
titleSuffix: Configuration Manager
description: Configurez l’inventaire logiciel, et excluez des dossiers de l’inventaire logiciel dans Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f6b346b9b3737e29268de67f65bbf1b96a670e5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132521"
---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Guide pratique pour configurer l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette procédure configure les paramètres par défaut du client pour l’inventaire logiciel et s’applique à tous les ordinateurs de votre hiérarchie. Si vous souhaitez appliquer ces paramètres uniquement à certains ordinateurs, créez un paramètre d’appareil client personnalisé et affectez-le à un regroupement. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Pour configurer l'inventaire logiciel  

1. Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client**  **Paramètres client par défaut**.  

2. Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

3. Dans la boîte de dialogue **Paramètres par défaut**, choisissez **Inventaire logiciel**.  

4. Dans la liste **Paramètres de périphérique** , configurez les valeurs suivantes :  

   -   **Activer l’inventaire logiciel sur les clients** : dans la liste déroulante, sélectionnez **Vrai**.  

   -   **Planifier l’inventaire logiciel et le regroupement de fichiers** : définit la fréquence de collecte de l’inventaire logiciel et des fichiers par les clients.   

5. Configurez les paramètres client dont vous avez besoin. La section [Inventaire logiciel](../../../../core/clients/deploy/about-client-settings.md#software-inventory) de l’article [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md) contient une liste des paramètres client.  

   Les ordinateurs clients sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [Comment gérer les clients dans System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Le code d’erreur 80041006 dans inventoryprovider.log signifie que la mémoire du fournisseur WMI est insuffisante. Autrement dit, la limite de quota de mémoire pour un fournisseur a été atteinte et le fournisseur d’inventaire ne peut pas continuer.
   > Dans ce cas, l’agent d’inventaire crée un rapport avec 0 entrée, et aucun élément d’inventaire n’est signalé. <br/>
   > Une solution possible consiste à réduire l’étendue de la collecte d’inventaire logiciel. Dans les cas où l’erreur se produit après la limitation de l’étendue de l’inventaire, l’augmentation de la propriété [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/) définie dans la classe [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671) peut constituer une solution.

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Pour exclure des dossiers d'un inventaire logiciel  

1.  Dans Notepad.exe, créez un fichier vide intitulé **Skpswi.dat**.  

2.  Cliquez avec le bouton droit sur le fichier **Skpswi.dat** et cliquez sur **Propriétés**. Dans les propriétés du fichier Skpswi.dat, sélectionnez l'attribut **Masqué** .  

3.  Placez le fichier **Skpswi.dat** à la racine du disque dur ou de la structure de dossiers de chaque client que vous souhaitez exclure de l'inventaire logiciel.  

> [!NOTE]  
>  L'inventaire logiciel n'effectue pas un nouvel inventaire du lecteur de client à moins que le fichier ne soit supprimé du lecteur sur l'ordinateur client.
