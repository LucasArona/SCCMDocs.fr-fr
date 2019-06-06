---
title: Mode de provisionnement
titleSuffix: Configuration Manager
description: En savoir plus sur le mode de provisionnement pendant la séquence de tâches Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 970b1fea320d8fe039062cf81789d14398930be5
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403433"
---
# <a name="provisioning-mode"></a>Mode de provisionnement

*S’applique à : System Center Configuration Manager (Current Branch)*

Lors d’une séquence de tâches de déploiement de système d’exploitation, Configuration Manager place le client en mode de provisionnement. (Une séquence de tâches de déploiement du système d’exploitation inclut la mise à niveau sur place vers Windows 10.) Dans cet état, le client ne traite pas la stratégie du site. Ce comportement permet à la séquence de tâches de s’exécuter sans le risque que d’autres déploiements soient en cours d’exécution sur le client. Quand la séquence de tâches se termine, avec succès ou avec un échec géré, elle sort le client du mode de provisionnement.

Si la séquence de tâches échoue de façon inattendue, le client peut être laissé en mode de provisionnement. Par exemple, si l’appareil redémarre au milieu du traitement de la séquence de tâches, il ne peut pas récupérer. Un administrateur doit identifier et corriger manuellement les clients qui se trouvent dans cet état.


## <a name="manually-remove-provisioning-mode"></a>Supprimer manuellement le mode de provisionnement

Si un client est laissé en mode de provisionnement, utilisez ce processus manuel pour rétablir le fonctionnement normal du client.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> L’un des changements apportés par cette méthode WMI est la définition d’une valeur de Registre, mais ce n’est pas le seul. Changer simplement la valeur de Registre ne fait pas entièrement sortir le client du mode de provisionnement. Si vous modifiez manuellement le Registre, le client peut faire preuve de comportements inattendus.  


## <a name="client-provisioning-mode-timeout"></a>Délai d’expiration du mode de provisionnement de client

À compter de la version 1902, la séquence de tâches définit un horodatage quand elle place le client en mode de provisionnement. Toutes les 60 minutes, un client en mode de provisionnement vérifie la durée écoulée depuis l’horodatage. S’il a été en mode de provisionnement pendant plus de 48 heures, le client quitte automatiquement le mode de provisionnement et redémarre son processus.

La valeur par défaut du délai d’expiration du mode de provisionnement est de 48 heures. Vous pouvez ajuster ce minuteur sur un appareil en définissant la valeur de **ProvisioningMaxMinutes** dans la clé de Registre suivante : `HKLM\Software\Microsoft\CCM\CcmExec`. Si cette valeur n’existe pas ou est `0`, le client utilise la valeur par défaut de 48 heures.


## <a name="process-flow-diagrams"></a>Diagrammes de flux de processus

Ces diagrammes montrent le flux de processus pour la séquence de tâches et le client.

### <a name="task-sequence"></a>Séquence de tâches

Le diagramme suivant montre comment la séquence de tâches définit le mode de provisionnement :

![Diagramme de flux d’une séquence de tâches définissant le mode de provisionnement](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Correction du client

Le diagramme suivant montre comment le client quitte le mode de provisionnement :

![Diagramme de flux d’un client quittant le mode de provisionnement](media/3197824-client-flow.png)


## <a name="see-also"></a>Voir aussi

[Configurer Windows et ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr)

[Mettre à niveau le système d’exploitation](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS)
