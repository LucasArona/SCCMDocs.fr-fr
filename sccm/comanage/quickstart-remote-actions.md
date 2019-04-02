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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754944"
---
# <a name="remote-actions-with-co-management"></a>Actions à distance avec la cogestion

Vous devez garantir que tous les appareils que vous gérez sont accessibles, quel que soit l’endroit où ils se trouvent, chaque fois qu’ils se connectent. Vous devez également fournir à chaque utilisateur tout ce dont il a besoin pour rester productif, tout en protégeant les applications et les données. Avec les actions d’appareil prises en charge par Intune, vous pouvez résoudre à distance ces opérations critiques.

Dans la vidéo suivante, la program manager principale, Heidi Cheng, et le program manager senior, Danny Guillory, parlent et font la démonstration des actions à distance avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Avantages

Les actions d’appareil à distance vous donnent des contrôles de gestion sur l’appareil sans interférer avec les données personnelles. Ces actions d’appareil à distance vous permettent d’effectuer les opérations suivantes : 
- Supprimer les données d’entreprise sur les appareils perdus ou volés  
- Renommer un appareil  
- Redémarrer un appareil  
- Consulter un inventaire des appareils  
- Contrôler à distance un appareil  
- Effacer les applications OEM préinstallées avec un redémarrage de Nouvelle version  
- Effectuer une réinitialisation aux paramètres d’usine sur n’importe quel appareil Windows 10  

Ces actions sont une façon simple et importante de protéger les données d’entreprise stockées sur ces appareils, que ce soit dans les e-mails ou OneDrive.

Pour plus d’informations sur ces actions, consultez [Actions à distance disponibles](#available-remote-actions). 



## <a name="case-studies"></a>Études de cas

La société de conseil internationale Avanade utilise régulièrement des actions à distance pour gérer les appareils utilisés par ses 30 000 employés. Dans un [billet de blog récent](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/), le directeur des systèmes d’information d’Avanade indiquait :

> *Notre victoire immédiate de bénéficier de la fonctionnalité Intune était la possibilité de réinitialiser Windows à distance sur un ordinateur. Cela est important pour nous en cas d’ordinateurs perdus ou volés, ce qui est plus courant avec nos employés très mobiles.*
> *Il s’agit d’une fonctionnalité que, autrement, nous aurions dû générer et gérer dans un package ConfigMgr personnalisé.*

Pour plus d’informations sur la façon d’utiliser ces actions à distance, consultez [Actions d’appareil disponibles](https://docs.microsoft.com/intune/device-management#available-device-actions).


## <a name="value-proposition"></a>Proposition de valeur

Quand un appareil Configuration Manager est cogéré, il ajoute immédiatement ces fonctions dont Configuration Manager ne dispose pas en mode natif. Vous pouvez désormais effectuer toutes les actions à distance qui sont prises en charge par Intune. 

Avec la cogestion, les appareils Configuration Manager sont désormais exactement comme tout autre appareil géré par Intune. Par exemple, ils sont pleinement présents dans le cloud, et vous pouvez y accéder tant qu’ils ont accès à Internet. Vous pouvez effectuer toutes ces actions sans effectuer d’étapes supplémentaires hormis l’activation de la cogestion.

Étant donné que le processus d’inscription automatique est transparent pour l’utilisateur, la productivité de ce dernier n’est absolument pas affectée. Aucune intervention de la part de l’utilisateur n’est nécessaire.


### <a name="available-remote-actions"></a>Actions à distance disponibles

Utilisez ces actions à distance à partir d’Intune une fois que vous avez [activé la cogestion](/sccm/comanage/how-to-enable) dans Configuration Manager.

#### <a name="remove-devices"></a>Supprimer des appareils
- **Mettre hors service** : Cette action supprime les applications gérées et les données managées (le cas échéant), les paramètres et les profils de messagerie qui ont été attribués à cet appareil. L’appareil est ensuite retiré de la gestion Intune. Ce processus s’effectue la prochaine fois que l’appareil s’enregistre et reçoit l’action de mise hors service à distance. La fonction Mettre hors service conserve les données personnelles de l’utilisateur sur l’appareil.  

- **Réinitialiser** : Cette action restaure les paramètres d’usine de l’appareil. Si vous choisissez l’option permettant de **Conserver le compte d’utilisateur et l’état d’inscription**, les données utilisateur sont conservées. Sinon, le lecteur est effacé de manière sécurisée.  

- **Supprimer** : Si vous voulez supprimer des appareils d’Intune sur le portail Azure, supprimez-les à partir du volet spécifique des appareils. La prochaine fois que l’appareil s’enregistre, il supprime toutes les données organisationnelles qu’il stocke.  

Pour plus d’informations, consultez [Supprimer des appareils à l’aide de la réinitialisation, de la mise hors service ou de la désinscription manuelle de l’appareil](https://docs.microsoft.com/intune/devices-wipe).

#### <a name="selective-wipe"></a>Réinitialisation sélective
<!--SCCMDocs issue 973-->
Quand vous choisissez une action **Réinitialisation sélective des applications**, cela supprime les données d’application de l’entreprise sans supprimer les données personnelles. Utilisez cette action quand un appareil est signalé comme perdu ou volé. 

Pour plus d’informations, consultez le [Guide pratique pour effacer uniquement les données d’entreprise des applications gérées par Intune](https://docs.microsoft.com/intune/apps-selective-wipe).

#### <a name="sync"></a>Sync
L’action d’appareil **Synchroniser** force l’appareil sélectionné à s’enregistrer immédiatement auprès d’Intune. Quand un appareil s’enregistre, il reçoit immédiatement toutes les actions et stratégies en attente que vous avez lui avez affectées.

Cette fonctionnalité peut vous aider à immédiatement valider les stratégies que vous avez affectées et résoudre les problèmes les concernant, sans attendre l’enregistrement planifié.

Pour plus d’informations, consultez [Synchroniser des appareils pour obtenir les stratégies et les actions les plus récentes avec Intune](https://docs.microsoft.com/intune/device-sync).

#### <a name="restart"></a>Redémarrer
L’action d’appareil **Redémarrer** entraîne le redémarrage de l’appareil que vous choisissez. Cette action est utile quand il existe un redémarrage en attente, mais que l’utilisateur n’est pas disponible pour l’effectuer.

Pour plus d’informations, consultez [Redémarrer à distance des appareils avec Intune](https://docs.microsoft.com/intune/device-restart).

#### <a name="fresh-start"></a>Nouvelle version
L’action d’appareil **Nouvelle version** supprime toutes les applications installées sur un appareil exécutant Windows 10, version 1703 ou ultérieure. L’action Nouvelle version permet de supprimer des applications préinstallées (OEM) qui sont généralement installées avec un nouvel appareil.

Si vous choisissez de ne pas conserver les données utilisateur, l’appareil est restauré dans sont état prêt à l’emploi. Il se désinscrit d’Azure AD et de MDM.

Si vous avez des normes prédéterminées concernant les applications qui doivent être sur l’appareil, cette action supprime celles qui ne répondent pas à vos critères.

Pour plus d’informations, consultez [Utiliser l’action Nouvelle version pour réinitialiser des appareils Windows 10 avec Intune](https://docs.microsoft.com/intune/device-fresh-start). 

#### <a name="remote-control"></a>Contrôle à distance
Les appareils gérés par Intune peuvent être administrés à distance à l’aide de [TeamViewer](https://www.teamviewer.com/). TeamViewer est un programme tiers que vous achetez séparément.

Pour plus d’informations, consultez [Utiliser TeamViewer pour administrer à distance des appareils Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 



## <a name="configure"></a>Configurer

En dehors du contrôle à distance par l’intermédiaire de TeamViewer, pour commencer à utiliser ces actions d’appareil à distance dans Intune, aucune configuration supplémentaire n’est nécessaire une fois que vous avez [activé la cogestion](/sccm/comanage/how-to-enable).

Pour plus d’informations sur l’utilisation de TeamViewer pour le contrôle à distance, consultez [Utiliser TeamViewer pour administrer à distance des appareils Intune](https://docs.microsoft.com/intune/device-profile-android-teamviewer). 

