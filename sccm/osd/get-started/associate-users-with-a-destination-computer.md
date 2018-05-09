---
title: Association d’utilisateurs à un ordinateur de destination
titleSuffix: Configuration Manager
description: Configurez System Center Configuration Manager pour associer des utilisateurs à des ordinateurs de destination lors du déploiement de systèmes d’exploitation.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a4065b0e6774160efb6be22fe2ec8268c60d6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>Associer des utilisateurs à un ordinateur de destination dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous utilisez System Center Configuration Manager pour déployer le système d’exploitation, vous pouvez associer des utilisateurs à l’ordinateur de destination sur lequel le système d’exploitation est déployé. Cette configuration consiste à spécifier ce qui suit :  

-   Qu'un seul utilisateur soit l'utilisateur principal de l'ordinateur de destination.  

-   Que plusieurs utilisateurs soient les utilisateurs principaux de l'ordinateur de destination.  

 L'affinité entre utilisateur et périphérique prend en charge la gestion orientée utilisateur lorsque vous déployez des applications. Quand vous associez un utilisateur à l’ordinateur de destination sur lequel installer un système d’exploitation, vous pouvez déployer ultérieurement des applications pour cet utilisateur, qui seront installées automatiquement sur l’ordinateur de destination. Toutefois, même si vous pouvez configurer la prise en charge de l'affinité entre utilisateur et périphérique lorsque vous déployez des systèmes d'exploitation, vous ne pouvez pas utiliser l'affinité entre utilisateur et périphérique pour déployer des systèmes d'exploitation.  

 Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>Comment spécifier un utilisateur quand vous déployez des systèmes d’exploitation  
 Le tableau suivant répertorie les actions que vous pouvez effectuer pour intégrer l'affinité entre périphérique et utilisateur dans vos déploiements de système d'exploitation. Vous pouvez intégrer l’affinité entre périphérique et utilisateur dans des déploiements PXE, des déploiements de médias de démarrage et des déploiements de médias préparés.  

|Action|Plus d'informations|  
|------------|----------------------|  
|Créer une séquence de tâches qui inclut la variable **SMSTSAssignUsersMode**|Ajoutez la variable **SMSTSAssignUsersMode** au début de votre séquence de tâches en suivant l’étape de la séquence de tâches [Définir la variable de séquence de tâches](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable). Cette variable spécifie comment la séquence de tâches gère les informations utilisateur.<br /><br /> Définissez la variable sur l'une des valeurs suivantes :<br /><br /> <br /><br /> **Auto**: la séquence de tâches crée automatiquement une relation entre l'utilisateur et l'ordinateur de destination et déploie le système d'exploitation.<br /><br /> **En attente**: la séquence de tâches crée une relation entre l'utilisateur et l'ordinateur de destination, mais attend l'approbation de l'utilisateur administratif avant le déploiement du système d'exploitation.<br /><br /> **Désactivé**: la séquence de tâches n'associe pas un utilisateur à l'ordinateur de destination et continue à déployer le système d'exploitation.<br /><br /> <br /><br /> Cette variable peut également être définie sur un ordinateur ou un regroupement. Pour plus d’informations sur les variables intégrées, consultez [Variables intégrées de séquence de tâches](../../osd/understand/task-sequence-built-in-variables.md).|  
|Créer une commande de prédémarrage qui collecte les informations utilisateur|La commande de prédémarrage peut être un script Visual Basic (VB) avec une zone de texte ou bien une application HTML (HTA) qui valide les données utilisateur qui sont saisies.<br /><br /> La commande de prédémarrage doit définir la variable **SMSTSUdaUsers** qui est utilisée lors de l'exécution de la séquence de tâches. Cette variable peut être définie sur un ordinateur, un regroupement ou une variable de séquence de tâches. Utilisez le format suivant pour ajouter plusieurs utilisateurs : *domaine\utilisateur1, domaine\utilisateur2, domaine\utilisateur3*.|  
|Configurer comment les points de distribution et les médias associent l'utilisateur à l'ordinateur de destination|Quand vous [configurez un point de distribution pour des demandes de démarrage PXE](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) et quand vous créez un [média de démarrage](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) ou un [média préparé](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) à l’aide de l’Assistant Création d’un média de séquence de tâches, vous pouvez spécifier comment le point de distribution ou le média prend en charge l’association d’utilisateurs avec l’ordinateur de destination sur lequel le système d’exploitation est déployé.<br /><br /> La configuration de la prise en charge de l'affinité entre périphérique et utilisateur n'a pas de méthode intégrée permettant de valider l'identité de l'utilisateur. Cela peut être important quand un technicien qui approvisionne l’ordinateur entre les informations pour le compte de l’utilisateur. En plus de définir la façon dont les informations utilisateur sont traitées par la séquence de tâches, la configuration de ces options sur le point de distribution et le média permet de limiter les déploiements démarrés à partir d’un démarrage PXE ou à partir d’un type de média spécifique.|  
