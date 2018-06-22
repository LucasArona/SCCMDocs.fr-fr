---
title: Créer une image pour un fabricant OEM en usine ou un dépôt local
titleSuffix: Configuration Manager
description: Procédez à des déploiements de médias préparés pour réduire le trafic réseau pendant le déploiement d’un système d’exploitation sur un ordinateur qui n’est pas entièrement approvisionné.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c8cf0af19017f4acfd95bcd01f8226229c05a14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353390"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>Créer une image pour un fabricant OEM en usine ou un dépôt avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements de médias préparés dans System Center Configuration Manager permettent de déployer un système d’exploitation sur un ordinateur qui n’est pas entièrement approvisionné. Un média préparé est un fichier WIM (Windows Imaging Format) qui peut être installé sur un ordinateur nu par le fabricant (OEM) ou dans un centre de reclassement d’entreprise qui n’est pas connecté à l’environnement Configuration Manager. Par la suite, dans l’environnement Configuration Manager, l’ordinateur commence par utiliser l’image de démarrage fournie par le média, un contrôle de hachage est effectué sur le média préparé pour vérifier qu’il est valide, puis l’ordinateur se connecte au point de gestion de site pour les séquences de tâches disponibles qui terminent le processus de téléchargement.


Cette méthode de déploiement peut réduire le trafic réseau car l'image de démarrage et l'image du système d'exploitation sont déjà sur l'ordinateur de destination. Vous pouvez spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. Une fois le système d’exploitation installé sur l’ordinateur, le cache de séquence de tâches local est vérifié en premier à la recherche d’applications, de packages ou de packages de pilotes, et si le contenu est introuvable ou a été modifié, il est téléchargé à partir d’un point de distribution configuré dans le média préparé, puis installé.  

 Vous pouvez utiliser un média préparé dans les scénarios de déploiement de système d’exploitation suivants :  

-   [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Remplacement d’un ordinateur existant et transfert des paramètres](replace-an-existing-computer-and-transfer-settings.md)  

 Effectuez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis utilisez les sections suivantes pour vous préparer et créer le média préparé.  

## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement  
 Quand vous utilisez un média préparé pour démarrer le processus de déploiement de système d’exploitation, vous devez configurer le déploiement pour rendre le système d’exploitation accessible au média. Vous pouvez configurer cela dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel ou sous l’onglet **Paramètres de déploiement** dans les propriétés du déploiement.  Pour le paramètre **Rendre disponible aux éléments suivants** , sélectionnez l’une des options suivantes :  

-   **Clients, média et environnement PXE Configuration Manager**  

-   **Média et environnement PXE uniquement**  

-   **Média et environnement PXE uniquement (masqué)**  

## <a name="create-the-prestaged-media"></a>Créer le média préparé  
 Créez le fichier de média préparé à envoyer à l’OEM ou à votre dépôt local. Pour plus d’informations, consultez [Créer un média préparé avec System Center Configuration Manager](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Envoyer le fichier de média préparé à l’OEM ou au dépôt local  
 Envoyez le média à l’OEM ou à votre dépôt local pour préparer les ordinateurs. Le fichier de média préparé est appliqué à un disque dur formaté sur l’ordinateur.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Démarrer l’ordinateur pour installer le système d’exploitation  
 Le fichier de média préparé est appliqué aux ordinateurs. Quand l’ordinateur est démarré pour la première fois, le processus d’installation de système d’exploitation démarre.  
