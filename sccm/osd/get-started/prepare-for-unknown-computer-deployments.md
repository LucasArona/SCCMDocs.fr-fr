---
title: Préparer les déploiements d’ordinateurs inconnus
titleSuffix: Configuration Manager
description: Découvrez comment déployer des systèmes d’exploitation sur des ordinateurs qui ne sont pas gérés par Configuration Manager dans votre environnement System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9e447e34-0943-49ed-b6ba-3efebf3566c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5c64ae61e2ff31a14b6c4b094eafa5feac197e21
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132589"
---
# <a name="prepare-for-unknown-computer-deployments-in-system-center-configuration-manager"></a>Préparer les déploiements sur des ordinateurs inconnus dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Aidez-vous des informations de cette rubrique pour déployer des systèmes d’exploitation sur des ordinateurs inconnus dans votre environnement System Center Configuration Manager. Un ordinateur inconnu est un ordinateur qui n’est pas géré par Configuration Manager. Autrement dit, il n’existe aucun enregistrement pour cet ordinateur dans la base de données Configuration Manager. Les ordinateurs inconnus sont les suivants :  

- Un ordinateur sur lequel le client Configuration Manager n’est pas installé  

- Un ordinateur qui n’est pas importé dans Configuration Manager.  

- Un ordinateur qui n’a pas été découvert par Configuration Manager.  

  Vous pouvez déployer des systèmes d’exploitation sur des ordinateurs inconnus avec les méthodes de déploiement suivantes :  

- [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)  

- [Utiliser un média de démarrage pour déployer un système d’exploitation](../deploy-use/create-bootable-media.md)  

- [Utiliser un média préparé pour déployer un système d’exploitation](../deploy-use/create-prestaged-media.md)  

## <a name="unknown-computer-deployment-workflow"></a>Flux de travail de déploiement d’ordinateur inconnu  
 Voici le flux de travail de base pour déployer un système d’exploitation sur un ordinateur inconnu :  

-   Sélectionnez l'objet d'un ordinateur inconnu à utiliser dans le déploiement. Vous pouvez déployer le système d'exploitation sur l'un des objets des ordinateurs inconnus du regroupement **Tous les ordinateurs inconnus** ou vous pouvez ajouter les objets du regroupement **Tous les ordinateurs inconnus** à un autre regroupement. Configuration Manager fournit deux objets ordinateurs inconnus dans le regroupement **Tous les ordinateurs inconnus**. Un objet est destiné aux ordinateurs x86 et l'autre objet aux ordinateurs x64.  

    > [!NOTE]  
    >  L'objet **Ordinateur x86 inconnu** est destiné aux ordinateurs qui sont uniquement compatibles x86. L’objet **Ordinateur x64 inconnu** est destiné aux ordinateurs qui sont compatibles x86 et x64. En d’autres termes, ces objets décrivent l’architecture de l’ordinateur de destination. Ils ne décrivent pas le système d’exploitation que vous souhaitez déployer sur l’ordinateur de destination.  

-   Créez un média ou configurez un point de distribution PXE pour prendre en charge les déploiements sur des ordinateurs inconnus.  

-   Déployez la séquence de tâches pour installer le système d’exploitation.  

## <a name="unknown-computer-installation-process"></a>Processus d'installation d'un ordinateur inconnu  
 Quand un ordinateur est démarré pour la première fois à partir de PXE ou d’un média, Configuration Manager vérifie s’il existe un enregistrement pour cet ordinateur dans la base de données Configuration Manager. S’il en trouve un, Configuration Manager vérifie ensuite s’il existe des séquences de tâches déployées sur l’enregistrement. S’il ne trouve pas d’enregistrement, Configuration Manager vérifie s’il existe des séquences de tâches déployées sur un objet ordinateur inconnu. Dans les deux cas, Configuration Manager effectue ensuite l’une des actions suivantes :  

- S’il existe une séquence de tâches disponible, Configuration Manager invite l’utilisateur à l’exécuter.  

- S’il existe une séquence de tâches obligatoire, Configuration Manager l’exécute automatiquement.  

- Si aucune séquence de tâches n’est déployée pour l’enregistrement, Configuration Manager génère une erreur indiquant qu’il n’existe pas de séquence de tâches déployée sur l’ordinateur de destination.  

  Quand un ordinateur inconnu est démarré, Configuration Manager le reconnaît comme un ordinateur non préparé plutôt que comme un ordinateur inconnu. Cela signifie que l'ordinateur peut maintenant recevoir les séquences de tâches qui ont été déployées sur l'objet d'ordinateur inconnu. La séquence de tâches déployée installe ensuite une image de système d’exploitation qui doit inclure le client Configuration Manager.  

  Une fois que le client Configuration Manager a été installé, un enregistrement est créé pour l’ordinateur, lequel s’affiche alors dans le regroupement approprié de Configuration Manager. Si l’ordinateur ne parvient pas à installer l’image du système d’exploitation ou le client Configuration Manager, un enregistrement « Inconnu » est créé pour l’ordinateur. Cet ordinateur est affiché dans le regroupement **Tous les systèmes** de Configuration Manager.  

> [!NOTE]  
>  Pendant l'installation de l'image du système d'exploitation, la séquence de tâches peut récupérer les variables de regroupement, mais non les variables d'ordinateur à partir de cet ordinateur.  

##  <a name="BKMK_EnablingUnknown"></a> Activation de la prise en charge d'ordinateur inconnu  
 Utilisez les informations suivantes pour activer la prise en charge des ordinateurs inconnus quand vous déployez un système d’exploitation à l’aide de PXE, d’un média de démarrage et d’un média préparé.  

-   **Environnement Environnement PXE**  

     Cochez la case **Activer la prise en charge d’ordinateur inconnu** sous l’onglet **PXE** pour un point de distribution qui est activé pour PXE. Pour plus d’informations, consultez [Configuration de points de distribution pour accepter des requêtes PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint).  

-   **Média de démarrage**  

     Cochez la case **Activer la prise en charge d'ordinateur inconnu** sur la page **Sécurité** de l'Assistant Création d'un média de séquence de tâches. Pour plus d’informations, consultez [Configuration de points de distribution pour accepter des requêtes PXE](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint) et [Utiliser PXE pour déployer Windows sur le réseau avec System Center Configuration Manager](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

-   **Média préparé**  

     Cochez la case **Activer la prise en charge d'ordinateur inconnu** sur la page **Sécurité** de l'Assistant Création d'un média de séquence de tâches. Pour plus d’informations, consultez [Créer un média préparé avec System Center Configuration Manager](../deploy-use/create-prestaged-media.md).  
