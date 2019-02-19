---
title: 'Gestion des clients dans une infrastructure VDI (Virtual Desktop Infrastructure) '
titleSuffix: Configuration Manager
description: Gérez les clients System Center Configuration Manager dans une infrastructure VDI (Virtual Desktop Infrastructure).
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9352d6e5a26afd4cee36f70a19d0566e26643f50
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130569"
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>Considérations sur la gestion des clients System Center Configuration Manager dans une infrastructure VDI

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager prend en charge l’installation du client Configuration Manager dans les scénarios VDI suivants :  

- **Machines virtuelles personnelles** : les machines virtuelles personnelles sont généralement utilisées quand vous voulez vous assurer que les données et les paramètres utilisateur sont conservés sur les machines virtuelles entre les sessions.  

- **Sessions de services Bureau à distance** : les services Bureau à distance permettent à un serveur d’héberger plusieurs sessions clientes simultanées. Les utilisateurs peuvent se connecter à une session, puis exécuter des applications sur ce serveur.  

- **Machines virtuelles regroupées** : les machines virtuelles regroupées ne sont pas conservées entre les sessions. Lorsqu'une session est fermée, toutes les données et tous les paramètres sont supprimés. Les machines virtuelles regroupées sont utiles lorsqu'il est impossible d'utiliser les services Bureau à distance, car une application métier requise ne peut pas s'exécuter sur le serveur Windows hébergeant les sessions clientes.  

  Le tableau suivant recense les éléments à prendre en considération pour la gestion du client Configuration Manager dans une infrastructure VDI.  

|Type de machine virtuelle|Éléments à prendre en considération|  
|--------------------------|--------------------|  
|Machines virtuelles personnelles|Configuration Manager traite les machines virtuelles personnelles comme un ordinateur physique. Le client Configuration Manager peut être préinstallé sur l’image de machine virtuelle ou déployé après avoir approvisionné la machine virtuelle.|  
|Services Bureau à distance|Le client Configuration Manager n’est pas installé pour les sessions Bureau à distance individuelles. Ce client est plutôt installé une seule fois sur le serveur des services Bureau à distance. Toutes les fonctionnalités de Configuration Manager peuvent être utilisées sur le serveur des services Bureau à distance.|  
|Machines virtuelles regroupées|Quand une machine virtuelle regroupée est mise hors service, les modifications que vous apportez à l’aide de Configuration Manager sont perdues.<br /><br /> Les données renvoyées par les fonctionnalités de Configuration Manager, telles que l’inventaire logiciel, l’inventaire matériel et le contrôle de logiciel peuvent ne pas répondre à vos besoins, car la machine virtuelle risque de ne fonctionner que sur une courte période. Envisagez d'exclure les ordinateurs virtuels regroupés des tâches d'inventaire.|  

 Sachant que la virtualisation prend en charge l’exécution de plusieurs clients Configuration Manager sur un même ordinateur physique, de nombreuses opérations du client possèdent un délai randomisé prédéfini pour les actions planifiées telles que l’inventaire matériel et logiciel, les analyses anti-programmes malveillants, les installations logicielles et les analyses de mises à jour logicielles. Ce délai permet de distribuer le traitement processeur et le transfert de données pour un ordinateur doté de plusieurs machines virtuelles qui exécutent le client Configuration Manager.  

> [!NOTE]  
>  À l’exception des clients Windows Embedded en mode maintenance, les clients Configuration Manager qui ne s’exécutent pas dans des environnements virtualisés utilisent aussi ce délai randomisé. Quand le nombre de clients déployés est important, ce comportement permet d’éviter des pics d’utilisation de la bande passante réseau et de réduire les besoins de traitement processeur sur les systèmes de site Configuration Manager, tels que le point de gestion et le serveur de site. L’intervalle du délai varie en fonction de la fonctionnalité de Configuration Manager.  
>   
>  Le délai de randomisation est désactivé par défaut pour les mises à jour logicielles requises à l’aide du paramètre client suivant : **Agent ordinateur** : **Désactiver la randomisation des échéances**.
