---
title: Créer des environnements virtuels App-V
titleSuffix: Configuration Manager
description: Créez des environnements virtuels avec Microsoft Application Virtualization pour permettre aux applications de partager des données entre elles.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2becf31d807f0854bf6ab9d4eb58adf84d8ab7e6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56135760"
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>Créer des environnements virtuels App-V dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans un environnement virtuel Microsoft Application Virtualization (App-V) dans System Center Configuration Manager (Configuration Manager), les applications virtuelles déployées peuvent partager le même système de fichiers et le même Registre sur les PC Windows clients. Contrairement aux applications virtuelles conventionnelles, ces applications peuvent partager des données entre elles. Les environnements virtuels sont créés ou modifiés sur les PC clients pendant l’installation de l’application ou ultérieurement quand les clients évaluent les applications installées. Vous pouvez contrôler ces applications de telle sorte que lorsque plusieurs applications essaient de modifier un système de fichiers ou une valeur de Registre, l'application d'ordre le plus élevé est prioritaire.  

> [!IMPORTANT]  
>  Ne vous appuyez pas sur des environnements virtuels App-V pour assurer une protection, notamment contre les programmes malveillants.  

 Suivez la procédure ci-dessous pour créer un environnement virtuel App-V dans Configuration Manager.  

## <a name="create-an-app-v-virtual-environment"></a>Créer un environnement virtuel App-V  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Environnements virtuels App-V**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un environnement virtuel**.  

4.  Dans la boîte de dialogue **Créer un environnement virtuel**, entrez les informations suivantes :  

    -   **Nom**.  Entrez un nom unique pour l’environnement virtuel (128 caractères maximum).  

    -   **Description**. (Facultatif) Entrez une description de l’environnement virtuel.  

5.  Pour ajouter un nouveau type de déploiement à l’environnement virtuel, choisissez **Ajouter**. Vous devez ajouter au moins un type de déploiement.  

6.  Dans la boîte de dialogue **Ajouter des applications**, spécifiez un **Nom de groupe** (128 caractères maximum). Vous utiliserez ce nom pour faire référence au groupe d’applications que vous ajoutez à l’environnement virtuel.  

7.  Choisissez **Ajouter**, sélectionnez les applications App-V 5 et les types de déploiement à ajouter au groupe, puis choisissez **OK**.  

8.  Dans la boîte de dialogue **Ajouter des applications**, vous pouvez sélectionner **Ordre croissant** ou **Ordre décroissant** pour définir quelle application est prioritaire dans le cas où plusieurs applications essaient de modifier le système de fichiers ou les paramètres de Registre dans le même environnement virtuel.  

9. Pour revenir à la boîte de dialogue **Créer un environnement virtuel**, choisissez **OK**.  

10. Une fois que vous avez terminé d’ajouter des groupes, choisissez **OK** pour créer l’environnement virtuel. Le nouvel environnement virtuel apparaît dans le nœud **Environnements virtuels App-V** de la console Configuration Manager. Vous pouvez surveiller l’état de vos environnements virtuels grâce au rapport État de l’environnement virtuel App-V.  

    > [!NOTE]  
    >  L’environnement virtuel est ajouté ou modifié sur les PC clients pendant l’installation de l’application ou ultérieurement quand le client évalue les applications installées.  
