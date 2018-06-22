---
title: Tableau de bord des appareils Surface
titleSuffix: Configuraton Manager
description: Passez en revue les informations relatives aux appareils Surface à l’aide du tableau de bord.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: db5df73db6a973ca689def785ee99a40425303fa
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334553"
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>Tableau de bord des appareils Surface dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1802, le tableau de bord des appareils Surface vous fournit, d’un seul coup d’œil, des informations sur les appareils Surface se trouvant dans votre environnement. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Ouvrir le tableau de bord des appareils Surface

Pour ouvrir le tableau de bord des appareils Surface, effectuez les étapes suivantes : 

1. Ouvrez la console Configuration Manager. 
2. Cliquez sur le nœud **Analyse**. 
3. Pour charger le tableau de bord, cliquez sur **Appareils Surface**.

**Tableau de bord des appareils Surface**
![Tableau de bord des appareils Surface](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Consultation des informations contenues dans le tableau de bord des appareils Surface

Le tableau de bord des appareils Surface présente trois graphiques pour votre environnement. 

- **Pourcentage d’appareils Surface** : indique le pourcentage d’appareils Surface dans tout votre environnement.

    ![Graphique Pourcentage d’appareils Surface](media\Percent-Surface-Devices.PNG)
- **Modèles d’appareil Surface** : affiche le nombre d’appareils par modèle Surface. 
    - Pointer sur une section du graphique vous donne le pourcentage d’appareils Surface qui sont du modèle sélectionné. 

         ![Graphique Modèles d’appareil Surface](media\Surface-Models-Hover.PNG)
    - Cliquer sur une section du graphique vous permet d’accéder à une liste d’appareils pour le modèle. 
        ![Liste d’appareils pour le modèle Surface](media\Surface-Model-Device-List.PNG)

- **Cinq principales versions de microprogramme** : affiche un graphique comprenant les cinq principaux modèles de microprogramme de votre environnement. 
    - Pointer sur une section du graphique vous donne le nombre d’appareils Surface qui sont de la version de microprogramme sélectionnée. 
       ![Liste d’appareils pour le modèle Surface](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Plus d'informations

Pour plus d’informations sur les appareils Surface, consultez les éléments suivants :
 - Le site web [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).
    
Pour plus d’informations sur le déploiement des mises à jour de microprogramme Surface dans Configuration Manager, consultez :
 - [Comment gérer les mises à jour de pilote Surface dans Configuration Manager]( https://support.microsoft.com/help/4098906)




