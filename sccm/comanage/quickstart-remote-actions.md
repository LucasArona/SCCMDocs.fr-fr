---
title: Actions à distance avec la cogestion
titleSuffix: Configuration Manager
description: Exécuter des actions à distance à partir d’Intune pour les appareils cogérés
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4439aa280edaffbb59f8d49ece58e067a729ec91
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754944"
---
# <a name="remote-actions-with-co-management"></a>Actions à distance avec la cogestion

Vous devez vous assurer que tous les appareils que vous gérez sont accessible, quel que soit l’endroit où il s’agit, chaque fois qu’il se connecte. Vous devez également fournir tout ce dont ils ont besoin pour rester productifs, tout en protégeant les applications et les données à chaque utilisateur. Avec les actions d’appareil pris en charge par Intune, vous pouvez à distance à résoudre ces fonctions critiques.

Dans la vidéo suivante, responsable de programme principal Heidi Cheng et responsable de programme senior Danny Guillory discuteront et de démonstration des actions à distance avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Avantages

Actions de l’appareil à distance vous donnent aux contrôles de gestion sur l’appareil sans interférer avec les données personnelles. Ces actions de l’appareil à distance vous permettent de : 
- Supprimer les données d’entreprise sur les appareils perdus ou volés  
- Renommer un appareil  
- Redémarrer un appareil  
- Inventaire des appareils de révision  
- Contrôler à distance un appareil  
- Effacer les applications OEM préinstallées avec un redémarrage Fresh Start  
- Effectuez une réinitialisation sur n’importe quel appareil Windows 10 des paramètres  

Ces fonctions sont un moyen simple et important pour protéger les données d’entreprise stockées sur ces appareils, que ce soit dans le courrier électronique ou OneDrive.

Pour plus d’informations sur ces actions, consultez [des actions à distance disponibles](#available-remote-actions). 



## <a name="case-studies"></a>Études de cas

Le cabinet de conseil Avanade utilise régulièrement les actions à distance pour gérer les appareils utilisés par leurs employés de 30 000. Dans un [billet de blog récent](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), le directeur informatique d’Avanade indiqué :

> *Notre win immédiate d’avoir les fonctionnalités Intune était la possibilité de réinitialiser à distance Windows sur un ordinateur. Cela est important pour nous pour les ordinateurs perdus ou volés, ce qui est plus courant dans nos employés très mobiles. * 
>  *Il s’agit des fonctionnalités qui nous sinon auraient eu pour créer et gérer dans un package personnalisé de ConfigMgr.*

Pour plus d’informations sur l’utilisation de ces actions à distance, consultez [actions d’appareils disponibles](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Proposition de valeur

Quand un appareil de Configuration Manager est cogéré, il ajoute immédiatement ces fonctions Configuration Manager n’a pas en mode natif. Maintenant vous pouvez désormais réaliser toute action à distance qui est pris en charge par Intune. 

Avec la cogestion, les appareils de Configuration Manager sont désormais comme tout autre appareil géré par Intune. Par exemple, ils ont une présence complète dans le cloud, et y accéder comme à condition qu’ils aient accès à internet. Vous pouvez effectuer toutes ces actions sans procédure supplémentaire au-delà de l’activation de la cogestion.

Étant donné que le processus d’inscription automatique est transparent pour l’utilisateur, il n’existe aucun impact sur leur productivité. L’utilisateur n’a pas besoin de faire quoi que ce soit.


### <a name="available-remote-actions"></a>Actions à distance disponibles

Utilisez ces actions à distance à partir d’Intune une fois que vous [activer la cogestion](/sccm/comanage/how-to-enable) dans Configuration Manager.

#### <a name="remove-devices"></a>Supprimer des appareils
- **Mettre hors service**: Cette action supprime les applications gérées et des données (le cas échéant), paramètres et la messagerie profils qui ont été affectées à cet appareil. L’appareil est ensuite supprimé de la gestion Intune. Ce processus déroule la prochaine heure de l’appareil s’enregistre et reçoit l’instance distante mettre hors service l’action. La fonction de mise hors service conserve les données personnelles de l’utilisateur sur l’appareil.  

- **Réinitialiser**: Cette action restaure un appareil ses paramètres d’usine par défaut. Si vous choisissez l’option à **conserver le compte d’utilisateur et l’état d’inscription**, puis les données utilisateur sont conservées. Sinon, le lecteur est effacé en toute sécurité.  

- **Supprimer**: Si vous souhaitez supprimer des appareils d’Intune sur le portail Azure, les supprimer à partir du volet de périphérique spécifique. La prochaine fois que l’appareil s’enregistre, il supprime toutes les données d’organisation stockées dessus.  

Pour plus d’informations, consultez [supprimer des appareils à l’aide de réinitialisation, de mettre hors service ou de désinscrire manuellement l’appareil](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Réinitialisation sélective
<!--SCCMDocs issue 973--> Lorsque vous choisissez un **réinitialisation sélective des applications**, il supprime les données d’application entreprise sans supprimer les données personnelles. Utilisez cette action quand un appareil est signalé comme perdu ou volé. 

Pour plus d’informations, consultez [Guide pratique pour effacer uniquement les données d’entreprise à partir d’applications gérées par Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>synchronisation
Le **synchronisation** action d’appareil force l’appareil sélectionné à s’enregistrer immédiatement auprès d’Intune. Quand un appareil s’enregistre, il reçoit immédiatement les actions ou les stratégies que vous avez affectés à ce dernier en attente.

Cette fonctionnalité peut vous aider à valider et résoudre les problèmes de stratégies que vous avez affectées, sans attendre la prochaine planifiée archiver immédiatement.

Pour plus d’informations, consultez [synchroniser des appareils pour obtenir les dernières stratégies et actions avec Intune](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Redémarrer
Le **redémarrer** action d’appareil, l’appareil que vous choisissez de redémarrer. Cette action est utile lorsqu’il existe un redémarrage en attente, mais l’utilisateur n’est pas disponible pour ce faire.

Pour plus d’informations, consultez [redémarrer à distance des appareils avec Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Redémarrage à zéro
Le **Fresh Start** action d’appareil supprime toutes les applications installées sur un périphérique exécutant Windows 10, version 1703 ou ultérieure. Redémarrage à zéro permet de supprimer des applications préinstallées (OEM) qui sont généralement installées avec un nouvel appareil.

Si vous choisissez de ne pas conserver les données utilisateur, l’appareil rétablit l’état out-of-box. Il annule l’inscription auprès d’Azure AD et des appareils mobiles.

Si vous avez prédéterminés normes en matière d’applications qui doivent être sur l’appareil, cette action supprime ceux qui ne répondent pas à vos critères.

Pour plus d’informations, consultez [utiliser Fresh Start pour réinitialiser les appareils Windows 10 avec Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Contrôle à distance
Appareils gérés par Intune peuvent être administrés à distance en utilisant [TeamViewer](https://www.teamviewer.com/). TeamViewer est un programme tiers que vous achetez séparément.

Pour plus d’informations, consultez [TeamViewer utilisez pour administrer à distance des appareils Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurer

Autre que de contrôle à distance via TeamViewer, pour commencer à utiliser ces actions à distance d’appareil dans Intune, sans configuration supplémentaire est nécessaire après avoir [activer la cogestion](/sccm/comanage/how-to-enable).

Pour plus d’informations sur l’utilisation de TeamViewer pour le contrôle à distance, consultez [TeamViewer utilisez pour administrer à distance des appareils Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

