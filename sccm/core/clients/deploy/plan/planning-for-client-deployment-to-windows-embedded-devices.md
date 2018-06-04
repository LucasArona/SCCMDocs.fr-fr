---
title: Planification du déploiement de clients sur des appareils Windows Embedded
titleSuffix: Configuration Manager
description: Planifiez le déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
caps.latest.revision: 7
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: c4f3d8a9b043707340e56d3ae483ad66ca17dc10
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2018
ms.locfileid: "23134495"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-system-center-configuration-manager"></a>Planification du déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a> Si votre appareil Windows Embedded n’inclut pas le client System Center Configuration Manager, vous pouvez utiliser l’une des méthodes d’installation de ce client si l’appareil respecte les dépendances requises. Si l'appareil intégré prend en charge les filtres d'écriture, vous devez désactiver ces filtres avant d'installer le client, puis réactiver les filtres une fois le client installé et attribué à un site.  

 Notez que quand vous désactivez les filtres, vous ne devez pas désactiver les pilotes de filtre. En général, ces pilotes démarrent automatiquement au démarrage de l'ordinateur. La désactivation de ces pilotes empêche l'installation du client ou interfère avec l'orchestration des filtres d'écriture, ce qui entraîne l'échec des opérations du client. Voici les services associés à chaque type de filtre d'écriture devant rester en cours d'exécution :  

|Type de filtre d'écriture|Pilote|Tapez|Description|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Noyau|Met en œuvre la redirection des E/S au niveau du secteur sur les volumes protégés.|  
|FBWF|FBWF|Système de fichiers|Met en œuvre la redirection des E/S au niveau du fichier sur les volumes protégés.|  
|UWF|uwfreg|Noyau|Redirecteur de Registre UWF|  
|UWF|uwfs|Système de fichiers|Redirecteur de fichier UWF|  
|UWF|uwfvol|Noyau|Gestionnaire de volume UWF|  

 Les filtres d'écritures contrôlent la manière dont le système d'exploitation sur l'appareil intégré est mis à jour lorsque vous apportez des modifications, comme lorsque vous installez des logiciels. Lorsque les filtres d'écriture sont activés, au lieu d'apporter les modifications directement dans le système d'exploitation, celles-ci sont redirigées vers un segment de recouvrement temporaire. Si les modifications sont écrites uniquement dans le segment de recouvrement, elles sont perdues lorsque l'appareil intégré s'arrête. Toutefois, si les filtres d'écriture sont temporairement désactivés, les modifications peuvent être rendues définitives afin que vous n'ayez pas à les apporter de nouveau (ou à réinstaller le logiciel) à chaque redémarrage de l'appareil intégré. Cependant, la désactivation temporaire suivie de la réactivation de ces filtres d'écriture requiert un ou plusieurs redémarrages, si bien qu'il est souhaitable de les contrôler en configurant des fenêtres de maintenance permettant aux redémarrages de se produire en dehors des heures de bureau.  

 Vous pouvez configurer des options pour désactiver et réactiver automatiquement les filtres d’écriture quand vous déployez des logiciels tels que des applications, des séquences de tâches, des mises à jour logicielles et le client Endpoint Protection. Il existe une exception pour les lignes de base de configuration comportant des éléments de configuration qui utilisent une correction automatique. Dans ce scénario, la correction se produit toujours dans le segment de recouvrement afin d'être disponible uniquement jusqu'au redémarrage de l'appareil. La correction est appliquée de nouveau lors du prochain cycle d'évaluation, mais uniquement au segment de recouvrement, lequel est effacé au redémarrage. Pour forcer Configuration Manager à valider les modifications de la correction, vous pouvez déployer la ligne de base de configuration, puis un autre déploiement logiciel qui prend en charge la validation de la modification dès que possible.  

 Si les filtres d'écriture sont désactivés, vous pouvez installer des logiciels sur les appareils Windows Embedded à l'aide du Centre logiciel. Toutefois, si les filtres d’écriture sont activés, l’installation échoue et Configuration Manager affiche un message d’erreur indiquant que vos autorisations ne sont pas suffisantes pour installer l’application.  

> [!WARNING]  
>  Même si vous ne sélectionnez pas les options Configuration Manager permettant de valider les modifications, celles-ci peuvent l’être si une autre installation logicielle ou modification est effectuée en ce sens. Dans ce scénario, les modifications d'origine sont validées en plus des nouvelles modifications.  

 Quand Configuration Manager désactive les filtres d’écriture pour rendre les modifications définitives, seuls les utilisateurs qui possèdent des droits administratifs locaux peuvent se connecter et utiliser l’appareil intégré. Pendant cette période, les utilisateurs dont les droits sont peu élevés sont verrouillés et ils voient un message indiquant que l'ordinateur n'est pas disponible car il est en cours de maintenance. Cette indisponibilité protège l'appareil pendant que son état permet l'application de modifications définitives et ce comportement de verrouillage du mode de maintenance constitue une autre raison pour configurer une fenêtre de maintenance pendant laquelle les utilisateurs ne se connectent pas à ces appareils.  

 Configuration Manager prend en charge la gestion des types de filtres d’écriture suivants :  

-   Filtre d’écriture basé sur des fichiers (FBWF) : pour plus d’informations, consultez [Filtre d’écriture basé sur des fichiers](http://go.microsoft.com/fwlink/?LinkID=204717).  

-   RAM de filtre d’écriture amélioré (EWF) : pour plus d’informations, consultez [Filtre d’écriture amélioré](http://go.microsoft.com/fwlink/?LinkId=204718).  

-   Filtre d’écriture unifié (UWF) : pour plus d’informations, consultez [Filtre d’écriture unifié](http://go.microsoft.com/fwlink/?LinkId=309236).  

 Configuration Manager ne prend pas en charge les opérations de filtre d’écriture quand l’appareil Windows Embedded est en mode de registre RAM EWF.  

> [!IMPORTANT]  
>  Si vous avez le choix, utilisez des filtres d’écriture basés sur des fichiers avec Configuration Manager pour une efficacité accrue et une meilleure évolutivité.
>
> **Pour les appareils qui utilisent des filtres d’écriture basés sur des fichiers uniquement :** configurez les exceptions suivantes pour rendre permanents l’état du client et les données d’inventaire entre les redémarrages de l’appareil :  
>   
>  -   CCMINSTALLDIR\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  Les appareils qui exécutent Windows Embedded 8.0 et ses versions ultérieures ne prennent pas en charge les exclusions qui contiennent des caractères génériques. Sur ces appareils, vous devez configurer individuellement les exclusions suivantes :  
>   
>  -   Tous les fichiers dans CCMINSTALLDIR portant l'extension .sdf, généralement :  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **Pour les appareils qui utilisent des filtres d’écriture basés sur des fichiers et des filtres d’écriture unifiés :** quand les clients d’un groupe de travail utilisent des certificats à des fins d’authentification auprès de points de gestion, vous devez également exclure la clé privée pour que les clients puissent continuer à communiquer avec les points de gestion. Sur ces appareils, configurez les exceptions suivantes :  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 Pour obtenir un exemple de scénario de déploiement et de gestion d’appareils Windows Embedded avec des filtres d’écriture activés dans Configuration Manager, consultez [Exemple de scénario de déploiement et de gestion de clients System Center Configuration Manager sur des appareils Windows Embedded](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Pour plus d'informations sur la façon de créer des images pour les appareils Windows Embedded et de configurer des filtres d'écriture, reportez-vous à votre documentation Windows Embedded ou contactez votre fabricant d'ordinateurs OEM.  

> [!NOTE]  
>  Lorsque vous sélectionnez les plates-formes applicables aux déploiements logiciels et aux éléments de configuration, celles-ci affichent les familles Windows Embedded, plutôt que des versions spécifiques. Utilisez la liste suivante pour faire correspondre la version spécifique de Windows Embedded aux options figurant dans la zone de liste :  
>   
>  -   L'option**Systèmes d'exploitation intégrés basés sur Windows XP (32 bits)** inclut les éléments suivants :  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   L'option**Systèmes d'exploitation intégrés basés sur Windows 7 (32 bits)** inclut les éléments suivants :  
>   
>      -   Windows Embedded Standard 7 (32 bits)  
>     -   Windows Embedded POSReady 7 (32 bits)  
>     -   Windows ThinPC  
> -   L'option**Systèmes d'exploitation intégrés basés sur Windows 7 (64 bits)** inclut les éléments suivants :  
>   
>      -   Windows Embedded Standard 7 (64 bits)  
>     -   Windows Embedded POSReady 7 (64 bits)
