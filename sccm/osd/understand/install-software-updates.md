---
title: Installer les mises à jour logicielles
titleSuffix: Configuration Manager
description: Recommandations pour l’utilisation de l’étape de séquence de tâches Installer les mises à jour logicielles dans Configuration Manager.
ms.date: 03/01/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 72d1ccd5-3763-4f88-9273-e1a73e8f4286
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 132ef497f25f550eccc068e310c1336050ef3b42
ms.sourcegitcommit: 33a006204f7f5f9b9acd1f3e84c4bc207362d00a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305816"
---
# <a name="install-software-updates"></a>Installer les mises à jour logicielles

*S’applique à : System Center Configuration Manager (Current Branch)*

L’étape **Installer les mises à jour logicielles** est couramment utilisée dans les séquences de tâches de Configuration Manager. Pendant l’installation ou la mise à jour du système d’exploitation, elle déclenche les composants de mises à jour logicielles pour rechercher et déployer des mises à jour. Cette étape peut poser des problèmes à certains clients, par exemple des délais d’expiration longs ou l’échec des mises à jour. Utilisez les informations fournies dans cet article pour atténuer les problèmes courants lors de cette étape et pour mieux les résoudre le cas échéant.

Pour plus d’informations sur cette étape, consultez [Installer les mises à jour logicielles](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)



## <a name="recommendations"></a>Recommandations

Pour réussir ce processus, suivez les recommandations suivantes :
- [Utiliser l’installation hors connexion](#use-offline-servicing)
- [Index unique](#single-index)
- [Réduire la taille de l’image](#bkmk_resetbase)


### <a name="use-offline-servicing"></a>Utiliser l’installation hors connexion

Utilisez Configuration Manager pour installer régulièrement les mises à jour logicielles applicables à vos fichiers image. Cette pratique réduit le nombre de mises à jour que vous devez installer pendant la séquence de tâches. 

Pour plus d’informations, consultez [Appliquer les mises à jour logicielles à une image du système d’exploitation](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).


### <a name="single-index"></a>Index unique

De nombreux fichiers image incluent plusieurs index, par exemple, pour différentes éditions de Windows. Réduisez le fichier image à un index unique dont vous avez besoin. Cette pratique réduit la quantité le temps nécessaire pour appliquer des mises à jour logicielles à l’image. Elle permet également de suivre la recommandation suivante, à savoir réduire la taille de l’image. 


### <a name="bkmk_resetbase"></a> Réduire la taille de l’image

Quand vous appliquez des mises à jour logicielles à l’image, optimisez la sortie en supprimant les mises à jour remplacées. Utilisez l’outil de ligne de commande DISM, par exemple : 

```
dism /Mount-Image /ImageFile:C:\Data\install.wim /MountDir:C:\Mountdir
dism /Image:C:\Mountdir /Cleanup-Image /StartComponentCleanup /ResetBase 
dism /Unmount-Image /MountDir:C:\Mountdir /Commit  
```



## <a name="image-engineering-decisions"></a>Décisions d’ingénierie d’images

Lorsque vous concevez votre processus de création d’images, plusieurs options peuvent avoir un impact sur l’installation de mises à jour logicielles :

- [Recapturer périodiquement l’image](#bkmk_goldimage)  
- [Utiliser l’installation hors connexion](#bkmk_offline)  
- [Utiliser une image par défaut uniquement](#bkmk_installwim)


### <a name="bkmk_goldimage"></a> Recapturer périodiquement l’image

Vous disposez d’un processus automatisé pour capturer une image de système d’exploitation personnalisée selon un calendrier régulier. Cette séquence de tâches de capture installe les dernières mises à jour logicielles. Ces mises à jour peuvent inclure des mises à jour cumulatives, non cumulatives et autres mises à jour critiques, telles que les mises à jour de la pile de maintenance (SSU). La séquence de tâches de déploiement installe les mises à jour supplémentaires depuis la capture.

Pour plus d’informations sur ce processus, consultez [Créer une séquence de tâches pour capturer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


#### <a name="advantages"></a>Avantages
- Moins de mises à jour moins à appliquer au moment du déploiement par le client, ce qui permet de gagner du temps et de la bande passante pendant le déploiement
- Moins de mises à jour susceptibles d’entraîner des redémarrages
- Image personnalisée pour l’organisation
- Moins de variables au moment du déploiement

#### <a name="disadvantages"></a>Inconvénients 
- Temps nécessaire pour créer et capturer l’image, même si c’est en grande partie automatisé
- Temps de distribution de l’image aux points de distribution plus long, ce qui peut être considéré comme une panne de déploiements actifs
- Le temps de test par le biais d’environnements de préproduction peut dépasser un cycle de correctif du système d’exploitation, ce qui peut rendre l’image mise à jour non pertinente 


### <a name="bkmk_offline"></a> Utiliser l’installation hors connexion

Planifiez Configuration Manager pour appliquer des mises à jour logicielles à vos images. 

Pour plus d’informations, consultez [Appliquer les mises à jour logicielles à une image du système d’exploitation](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).


#### <a name="advantages"></a>Avantages
- Moins de mises à jour moins à appliquer au moment du déploiement par le client, ce qui permet de gagner du temps et de la bande passante pendant le déploiement
- Moins de mises à jour susceptibles d’entraîner des redémarrages
- Vous pouvez planifier le processus de maintenance au niveau du site

#### <a name="disadvantages"></a>Inconvénients 
- Sélection manuelle des mises à jour 
- Temps de distribution de l’image aux points de distribution plus long
- Prend uniquement en charge les mises à jour basées sur CBS. Ne peut pas appliquer les mises à jour d’Office

> [!Tip]  
> Vous pouvez automatiser la sélection des mises à jour logicielles à l’aide de PowerShell. Utilisez l’applet de commande [Get-CMSoftwareUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmsoftwareupdate?view=sccm-ps) pour obtenir une liste des mises à jour. Utilisez ensuite l’applet de commande [New-CMOperatingSystemImageUpdateSchedule](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmoperatingsystemimageupdateschedule?view=sccm-ps) pour créer la planification de maintenance hors connexion. L’exemple suivant montre une méthode permettant d’automatiser cette action :
> 
> ```PowerShell
> # Get the OS image
> $Win10Image = Get-CMOperatingSystemImage -Name "Windows 10 Enterprise"
> 
> # Get the latest cumulative update for Windows 10 1809
> $OSBuild = "1809"
> $LatestUpdate = Get-CMSoftwareUpdate -Fast | Where {$_.LocalizedDisplayName -Like "*Cumulative Update for Windows 10 Version $OSBuild for x64*" -and $_.LocalizedDisplayName -notlike "*Dynamic*"} | Sort-Object ArticleID -Descending | Select -First 1 
> Write-Host "Latest update for Windows 10 build" $OSBuild "is" $LatestUpdate.LocalizedDisplayName
> 
> # Create a new update schedule to apply the latest update
> New-CMOperatingSystemImageUpdateSchedule -Name $Win10Image.Name -SoftwareUpdate $LatestUpdate -RunNow -ContinueOnError $True 
> ```


### <a name="bkmk_installwim"></a> Utiliser une image par défaut uniquement

Utilisez le fichier d’image par défaut Windows install.wim dans vos séquences de tâches de déploiement.

#### <a name="advantages"></a>Avantages
- Une bonne source connue, ce qui réduit le risque de rencontrer un problème de corruption d’image
- Élimine la probabilité de problèmes de modifications d’image

#### <a name="disadvantages"></a>Inconvénients 
- Potentiel de volume élevé de mises à jour pendant le déploiement
- Temps de déploiement plus long pour chaque appareil
- Peut ne pas avoir les personnalisations nécessaires et requérir des étapes de séquence de tâches supplémentaires pour la personnalisation



## <a name="flowchart"></a>Organigramme

Cet organigramme illustre le processus d’inclusion de l’étape Installer les mises à jour logicielles dans une séquence de tâches.

[Afficher le diagramme en taille réelle](media/ts-step-install-software-updates.svg)

![Diagramme de flux pour l’étape de séquence de tâches Installer les mises à jour logicielles](media/ts-step-install-software-updates.svg)  

1. **Le processus démarre sur le client** : une séquence de tâches en cours d’exécution sur un client inclut l’étape de mises à jour Installer les mises à jour logicielles.
2. **Compiler et évaluer la stratégie** : le client a compilé toutes les stratégies de mise à jour logicielles dans l’espace de noms WMI RequestedConfigs. (CIAgent.log)
3. *Cette instance est-elle appelée pour la première fois ?*  
    1. **Oui** : accédez à **Analyse complète**  
    2. **Non** : *l’étape est-elle configurée avec l’option [Évaluer les mises à jour logicielles à partir des résultats d’analyse en mémoire cache](/sccm/osd/understand/task-sequence-steps#evaluate-software-updates-from-cached-scan-results) ?*
        1. **Oui** : accédez à **Scanner à partir des résultats mis en cache**
        2. **Non** : accédez à **Analyse complète**
4. Processus d’analyse : une analyse complète ou une analyse à partir des résultats mis en cache, avec un processus de surveillance en parallèle.
    1. **Analyse complète** : le moteur de séquence de tâches appelle l’agent de mise à jour logicielle par le biais de Mettre à jour des API d’analyse pour effectuer une analyse *complète*. (WUAHandler.log, ScanAgent.log)  
        1. **Analyse (complète) de l’agent SUM** : processus d’analyse normal par le biais de Windows Update Agent (WUA), qui communique avec le point de mise à jour logicielle exécutant WSUS. Il ajoute les mises à jour applicables dans le magasin local de mise à jour. (WindowsUpdate.log, UpdateStore.log)
    2. **Scanner à partir des résultats mis en cache** : le moteur de séquence de tâches appelle l’agent de mise à jour logicielle par le biais de Mettre à jour des API d’analyse pour analyser les métadonnées mises en cache. (WUAHandler.log, ScanAgent.log) 
        1. **Analyse (en cache) de l’agent SUM** : Windows Update Agent (WUA) vérifie les mises à jour déjà mises en cache dans le magasin local de mise à jour. (WindowsUpdate.log, UpdateStore.log)
    3. **Démarrer le minuteur d'analyse** : le moteur de séquence de tâches démarre un minuteur et attend. (Ce processus a lieu en parallèle avec l’analyse complète ou une analyse à partir de processus des résultats mis en cache.)
        1. **Surveillance** : le moteur de séquence de tâches surveille l’état de l’agent SUM.
        2. *Que répond l’agent SUM ?*
            - **En cours** : le minuteur a-t-il atteint la valeur de la variable de séquence de tâches, [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout) ? (Valeur par défaut 1 heure)
                - **Oui** : l'étape échoue.
                - **Non** : accédez à **Surveillance**
            - **Échec** : l'étape échoue.
            - **Terminé** : accédez à **Énumérer la liste de mise à jour**
5. **Énumérer la liste de mise à jour** : L’agent SUM énumère la liste des mises à jour renvoyées par l’analyse et détermine lesquelles sont disponibles ou obligatoires.
6. *Y-a-t-il des mises à jour dans la liste des résultats d’analyse ?*
    - **Oui** : Accédez à **Installer des mises à jour**
    - **Non** : rien à installer, l’étape s’achève avec succès. 
7. Processus de déploiement : Le processus d’installation des mises à jour est parallèle au processus de surveillance du déploiement.
    1. **Installer les mises à jour** : le moteur de séquence de tâches appelle l’agent SUM par le biais de l’API de déploiement de mise à jour pour installer toutes les mises à jour disponibles ou uniquement les mises à jour obligatoires. Ce comportement est basé sur la configuration de l’étape, que vous sélectionniez **Requis pour l’installation – Mises à jour logicielles obligatoires uniquement** ou **Disponible pour l’installation – Toutes les mises à jour logicielles**. Vous pouvez également spécifier ce comportement avec la variable [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget).
        1. **Installation de l'agent SUM** : processus d’installation normal à l’aide de lises de mises à jour en cache, avec téléchargement de contenu standard. Installer la mise à jour via Windows Update Agent (WUA). (UpdatesDeployment.log, UpdatesHandler.log, WuaHandler.log, WindowsUpdate.log)
    2. **Démarrer le minuteur de déploiement et afficher la progression** : Le moteur de séquence de tâches démarre un minuteur d’installation, affiche des sous-progressions à des intervalles de 10 % dans l’interface utilisateur de progression TS et attend.
        1. **Surveillance** : le moteur de séquence de tâches interroge l’état de l’agent SUM.
        2. *Que répond l’agent SUM ?*
            - **En cours** : *le processus d’installation a-t-il été inactif pendant 8 heures ?*
                - **Oui** : l'étape échoue.
                - **Non** : accédez à **Surveillance**
            - **Échec** : l'étape échoue.
            - **Terminé** : accédez à *L’étape est-elle configurée avec l’option **Évaluer les mises à jour logicielles à partir des résultats d’analyse en mémoire cache** ?*


### <a name="timeouts"></a>Délais d'expiration

Le diagramme inclut deux des variables de délai d’expiration qui s’appliquent à cette étape. Il existe d’autres minuteurs standard à partir d’autres composants pouvant avoir un impact sur ce processus. 

- Délai d’analyse de mise à jour : 1 heure (smsts.log)  
- Délai de demande d’emplacement : 1 heure (LocationServices.log, CAS.log)  
- Délai de téléchargement du contenu : 1 heure (DTS.log)  
- Délai d’expiration du point de distribution inactif : 1 heure (LocationServices.log, CAS.log)  
- Délai d’expiration total de l’installation inactive : 8 heures (smsts.log)  



## <a name="troubleshooting"></a>Résolution des problèmes

Utilisez les ressources suivantes et des informations supplémentaires pour vous aider à résoudre les problèmes liés à cette étape :

- Veillez à cibler vos déploiements de mises à jour logicielles sur la même collection que le déploiement de séquence de tâches.  

- Veillez à inclure des points de mises à jour logicielles dans les groupes de limites. Pour plus d’informations, consultez cet [article Support Microsoft](https://support.microsoft.com/help/4041012/1702-clients-do-not-get-software-updates-from-configuration-manager).  

- Pour vous aider à résoudre les problèmes liés au processus de gestion des mises à jour logicielles, consultez [Résolution des problèmes de la gestion des mises à jour logicielles](https://support.microsoft.com/help/10680/software-update-management-troubleshooting-in-configuration-manager).  

- Pour aider à améliorer les performances globales, réduisez la taille du catalogue de mises à jour logicielles. Par exemple :  

    - supprimer les classifications, produits et langues inutiles. Pour plus d’informations, consultez [Configurer les classifications et les produits à synchroniser](/sccm/sum/get-started/configure-classifications-and-products).  

    - Réindexer la base de données de site et recréer des statistiques. Pour plus d’informations, consultez le [Livre blanc des performances et des conseils de mise à l’échelle Configuration Manager](https://gallery.technet.microsoft.com/Configuration-Manager-ba55428e).  

    - Refuser les mises à jour inutiles, par exemple :
        - remplacé (à compter de la version 1810, Configuration Manager s’en charge pour vous. Pour plus d’informations, consultez [Comportement de nettoyage de WSUS à partir de la version 1810](/sccm/sum/deploy-use/software-updates-maintenance#wsus-cleanup-behavior-starting-in-version-1810).)
        - Itanium
        - Bêta
        - Version suivante
        - ARM
        - Versions de Windows que vous ne déployez pas

