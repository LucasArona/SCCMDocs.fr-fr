---
title: Associer des utilisateurs à un ordinateur
titleSuffix: Configuration Manager
description: Configurer Configuration Manager pour associer des utilisateurs à des ordinateurs de destination lors du déploiement de systèmes d’exploitation.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 325b571adbcb2750eaa0b3a856dda753c43634f0
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755898"
---
# <a name="associate-users-with-a-destination-computer-in-configuration-manager"></a>Associer des utilisateurs à un ordinateur de destination dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Lorsque vous utilisez Configuration Manager pour déployer des systèmes d'exploitation, vous pouvez associer des utilisateurs à l'ordinateur de destination. Cette option fonctionne qu’un seul ou plusieurs utilisateurs soient les principaux utilisateurs de l'ordinateur de destination.  

 L'affinité entre utilisateur et périphérique prend en charge la gestion orientée utilisateur lorsque vous déployez des applications. Quand vous associez un utilisateur à l’ordinateur de destination sur lequel installer un système d’exploitation, vous pouvez déployer ultérieurement des applications pour cet utilisateur, qui seront installées automatiquement sur l’ordinateur de destination. Alors que vous pouvez configurer la prise en charge de l’affinité entre utilisateur et appareil pendant le déploiement de système d’exploitation, vous ne pouvez pas utiliser l’affinité entre utilisateur et appareil pour déployer le système d’exploitation.  

 Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

 Il existe plusieurs méthodes permettant d’intégrer l’affinité entre utilisateur et appareil dans vos déploiements de système d’exploitation. Vous pouvez intégrer l’affinité entre périphérique et utilisateur dans des déploiements PXE, des déploiements de médias de démarrage et des déploiements de médias préparés.  


### <a name="create-a-task-sequence-that-includes-the-smstsassignusersmode-variable"></a>Créer une séquence de tâches qui inclut la variable **SMSTSAssignUsersMode**

 Ajoutez la variable **SMSTSAssignUsersMode** au début de votre séquence de tâches en suivant l’étape [Définir la variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). Cette variable spécifie comment la séquence de tâches gère les informations utilisateur.

 Pour plus d’informations, consultez [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSAssignUsersMode).


### <a name="create-a-prestart-command-that-gathers-the-user-information"></a>Créer une commande de prédémarrage qui collecte les informations utilisateur

 La commande de prédémarrage peut être un VBScript avec une zone d’entrée. Elle peut également être une application HTML (HTA) qui valide les données utilisateur entrées. 

 Cette commande de prédémarrage doit définir la variable **SMSTSUDAUsers** qui est utilisée lors de l'exécution de la séquence de tâches. Cette variable peut être définie sur un ordinateur, un regroupement ou une variable de séquence de tâches.

 Pour plus d’informations, consultez [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSUDAUsers).


### <a name="configure-how-distribution-points-and-media-associate-the-user-with-the-destination-computer"></a>Configurer comment les points de distribution et les médias associent l'utilisateur à l'ordinateur de destination

 Le point de distribution ou le média prend en charge l’association d’utilisateurs à l’ordinateur de destination sur lequel le système d’exploitation est déployé. Utilisez l'une des méthodes suivantes : 

 - [Configurez un point de distribution pour accepter les requêtes de démarrage PXE](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_PXEDistributionPoint)  
 - [Créer un média de démarrage](/sccm/osd/deploy-use/create-bootable-media)  
 - [Créer un média préparé](/sccm/osd/deploy-use/create-prestaged-media)  


 La configuration de la prise en charge de l'affinité entre utilisateur et appareil n'a pas de méthode intégrée permettant de valider l'identité de l'utilisateur. Ce comportement est important quand un technicien approvisionne l’ordinateur et entre les informations pour le compte de l’utilisateur. En plus de définir la façon dont la séquence de tâches traite les informations utilisateur, la configuration de ces options sur le point de distribution et le média permet de limiter les déploiements démarrés à partir d’un démarrage PXE ou à partir d’un type de média spécifique.
