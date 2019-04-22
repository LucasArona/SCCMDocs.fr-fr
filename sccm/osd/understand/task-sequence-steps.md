---
title: Étapes de séquence de tâches
titleSuffix: Configuration Manager
description: Découvrez les différentes étapes que vous pouvez ajouter à une séquence de tâches Configuration Manager.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a349997150c951d1a4ec9e0b99f9d24c21f37205
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802952"
---
# <a name="task-sequence-steps-in-configuration-manager"></a>Étapes de séquence de tâches dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous trouverez ci-dessous les différentes étapes de séquence de tâches qui peuvent être ajoutées à une séquence de tâches Configuration Manager. Pour plus d’informations sur la modification d’une séquence de tâches, consultez [Modifier une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  

Les paramètres suivants sont communs à toutes les étapes de la séquence de tâches :

#### <a name="properties-tab"></a>Onglet Propriétés
- **Nom** : l’Éditeur de séquence de tâches vous demande de spécifier un nom court pour décrire cette étape. Quand vous ajoutez une nouvelle étape, l’Éditeur de séquence de tâches définit le nom en utilisant le type par défaut. La longueur du **Nom** ne peut pas dépasser 50 caractères.  

- **Description** : si vous le souhaitez, spécifiez des informations plus détaillées sur cette étape. La longueur de la **Description** ne peut pas dépasser 256 caractères.  

Le reste de cet article décrit les autres paramètres présents sous l’onglet **Propriétés** de chaque étape de la séquence de tâches.

#### <a name="options-tab"></a>Onglet Options  

- **Désactiver cette étape** : la séquence de tâches ignore cette étape quand elle s’exécute sur un ordinateur. L’icône de cette étape est grisée dans l’Éditeur de séquence de tâches.  

- **Continuer en cas d’erreur** : la séquence de tâches continue si une erreur se produit lors de l’exécution de l’étape. Pour plus d’informations, consultez [Considérations relatives à la planification de l’automatisation des tâches](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSGroups).   

- **Ajouter une condition** : la séquence de tâches évalue ces instructions conditionnelles pour déterminer si elle exécute l’étape. Pour obtenir un exemple d’utilisation d’une variable de séquence de tâches en tant que condition, consultez [Guide pratique pour utiliser les variables de séquence de tâches](/sccm/osd/understand/using-task-sequence-variables#bkmk_access-condition).   

Les sections ci-dessous pour des étapes de séquence de tâches spécifiques décrivent d’autres paramètres possibles sous l’onglet **Options**.



##  <a name="BKMK_ApplyDataImage"></a> Appliquer l’image de données   

Utilisez cette étape pour copier l’image de données sur la partition de destination spécifiée.  

Cette étape est exécutée uniquement sous Windows PE. Elle ne s’exécute dans le système d’exploitation complet. 

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDDataImageIndex](/sccm/osd/understand/task-sequence-variables#OSDDataImageIndex)  
- [OSDWipeDestinationPartition](/sccm/osd/understand/task-sequence-variables#OSDWipeDestinationPartition)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Appliquer l’image de données** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="image-package"></a>Package d'images  
Sélectionnez **Parcourir** pour spécifier le **Package d’images** utilisé par cette séquence de tâches. Sélectionnez le package à installer dans la boîte de dialogue **Sélectionner un package** . Les informations des propriétés associées à chaque package d'images s'affichent en bas de la boîte de dialogue. Utilisez la liste déroulante pour choisir l' **image** que vous souhaitez installer à partir du **package d'images**sélectionné.  

> [!NOTE]  
>  Cette action de séquence de tâches traite l’image comme un fichier de données. Cette action n’effectue aucune configuration pour démarrer l’image en tant que système d’exploitation.  

#### <a name="destination"></a>Destination  
Configurez une des options suivantes :

- **Prochaine partition disponible** : utilisez la partition séquentielle suivante qui n’a pas déjà été ciblée par une étape **Appliquer le système d’exploitation** ou **Appliquer l’image de données** dans cette séquence de tâches.  

- **Disque et partition spécifiques** : sélectionnez le numéro de **disque** (à partir de 0) et le numéro de **partition** (à partir de 1).  

- **Lettre de lecteur logique spécifique** : spécifiez la **lettre de lecteur** affectée à la partition par Windows PE. Cette lettre de lecteur peut être différente de la lettre de lecteur affectée par le système d’exploitation nouvellement déployé.  

- **Lettre de lecteur logique stockée dans une variable** : spécifiez la variable de séquence de tâches contenant la lettre de lecteur affectée à la partition par Windows PE. Cette variable est généralement définie dans la section Avancé de la boîte de dialogue **Propriétés de la partition** pour l’étape de séquence de tâches **Formater et partitionner le disque**.  

#### <a name="delete-all-content-on-the-partition-before-applying-the-image"></a>Supprimer l'intégralité du contenu de la partition avant d'appliquer l'image  
Spécifie que la séquence de tâches supprime tous les fichiers sur la partition cible avant d’installer l’image. Si vous ne supprimez pas le contenu de la partition, cette action peut être utilisée pour appliquer le contenu supplémentaire à une partition précédemment ciblée.  



##  <a name="BKMK_ApplyDriverPackage"></a> Appliquer le package de pilotes  

Utilisez cette étape pour télécharger tous les pilotes du package de pilotes et les installer sur le système d’exploitation Windows.

L'étape de séquence de tâches **Appliquer le package de pilotes** rend disponibles tous les pilotes d'appareils d'un package de pilotes pour l'utilisation avec Windows. Ajoutez cette étape entre les étapes **Appliquer le système d’exploitation** et **Configurer Windows et ConfigMgr** pour que les pilotes du package soient disponibles sous Windows. L'étape de séquence de tâches **Appliquer le package de pilotes** est également utile avec des scénarios de déploiement de médias autonomes.  

Placez les pilotes de périphérique identiques dans un package de pilotes et distribuez-les aux points de distribution appropriés. Par exemple, placez tous les pilotes d’un même fabricant dans un package de pilotes. Distribuez ensuite le package aux points de distribution auquel les ordinateurs associés peuvent accéder.

L’étape **Appliquer le package de pilotes** est pratique pour un média autonome. Cette étape est également utile pour installer un ensemble spécifique de pilotes. Ces types de pilotes incluent les appareils qui ne sont pas détectés par Windows Plug-and-play, comme les imprimantes réseau.  

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet. 

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDApplyDriverBootCriticalContentUniqueID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalContentUniqueID)  
- [OSDApplyDriverBootCriticalHardwareComponent](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalHardwareComponent)  
- [OSDApplyDriverBootCriticalID](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalID)  
- [OSDApplyDriverBootCriticalINFFile](/sccm/osd/understand/task-sequence-variables#OSDApplyDriverBootCriticalINFFile)  
- [OSDInstallDriversAdditionalOptions](/sccm/osd/understand/task-sequence-variables#OSDInstallDriversAdditionalOptions)<!--516679/2840016--> (depuis la version 1806)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Pilotes** et sélectionnez **Appliquer le package de pilotes** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="driver-package"></a>Package de pilotes
Spécifiez le package de pilotes qui contient les pilotes d’appareils nécessaires. Sélectionnez **Parcourir** pour lancer la boîte de dialogue **Sélectionner un package**. Sélectionnez un package de pilotes existant à appliquer. Les propriétés du package associé s'affichent dans la partie inférieure de la boîte de dialogue.  

#### <a name="select-the-mass-storage-driver-within-the-package-that-needs-to-be-installed-before-setup-on-pre-windows-vista-operating-systems"></a>Sélectionnez le pilote de stockage de masse au sein du package à installer avant la configuration sur les systèmes d'exploitation antérieurs à Windows Vista.
Spécifiez les pilotes de stockage de masse nécessaires pour installer un système d’exploitation classique.  

#### <a name="driver"></a>Pilote
Sélectionnez le fichier de pilote de stockage de masse à installer avant l’installation d’un système d’exploitation classique. La liste déroulante est complétée à partir du package spécifié.  

#### <a name="model"></a>Modèle  
Spécifiez l'appareil critique au démarrage nécessaire aux déploiements des systèmes d'exploitation antérieurs à Windows Vista.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-version-of-windows-where-this-is-allowed"></a>Effectuer une installation autonome des pilotes non signés sur les versions de Windows le permettant
Cette option permet à Windows Installer des pilotes sans signature numérique.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Appliquer les paramètres réseau   

Utilisez cette étape pour spécifier les informations de configuration du réseau ou du groupe de travail pour l’ordinateur de destination. La séquence de tâches stocke ces valeurs dans le fichier de réponses approprié. Le programme d’installation de Windows utilise ce fichier de réponses pendant l’action **Configurer Windows et ConfigMgr**.  

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet. 

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDAdapter](/sccm/osd/understand/task-sequence-variables#OSDAdapter)  
- [OSDAdapterCount](/sccm/osd/understand/task-sequence-variables#OSDAdapterCount)  
- [OSDDNSDomain](/sccm/osd/understand/task-sequence-variables#OSDDNSDomain)  
- [OSDDNSSuffixSearchOrder](/sccm/osd/understand/task-sequence-variables#OSDDNSSuffixSearchOrder)  
- [OSDDomainName](/sccm/osd/understand/task-sequence-variables#OSDDomainName)  
- [OSDDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDDomainOUName)  
- [OSDEnableTCPIPFiltering](/sccm/osd/understand/task-sequence-variables#OSDEnableTCPIPFiltering)  
- [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
- [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
- [OSDWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDWorkgroupName)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Paramètres** et **Appliquer les paramètres réseau** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="join-a-workgroup"></a>Joindre un groupe de travail
Sélectionnez cette option pour que l'ordinateur de destination fasse partie du groupe de travail spécifié. Entrez le nom du groupe de travail sur la ligne **Groupe de travail** . Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres réseau**. 

#### <a name="join-a-domain"></a>Joindre un domaine
Sélectionnez cette option pour que l'ordinateur de destination fasse partie du domaine spécifié. Spécifiez ou accédez au domaine, tel que `fabricam.com`. Spécifiez ou accédez à un chemin LDAP (Lightweight Directory Access Protocol) pour une unité d’organisation. Par exemple : `LDAP//OU=computers, DC=Fabricam.com, C=com`.  

#### <a name="account"></a>Compte
Sélectionnez **Définir** afin de spécifier un compte bénéficiant des autorisations nécessaires pour joindre l’ordinateur au domaine. Dans la boîte de dialogue **Compte d'utilisateur Windows**, entrez le nom d'utilisateur au format suivant : `Domain\User`. Pour plus d’informations, consultez [Compte de jonction de domaine](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account). 

#### <a name="adapter-settings"></a>Paramètres de carte réseau  
Spécifiez les configurations réseau pour chaque carte réseau dans l'ordinateur. Sélectionnez **Nouveau** pour ouvrir la boîte de dialogue **Paramètres réseau**, puis spécifiez les paramètres réseau. 
- Si vous utilisez également l’étape **Capturer les paramètres réseau**, la séquence de tâches applique les paramètres précédemment capturés à la carte réseau. 
- Si la séquence de tâches n’a pas déjà capturé de paramètres réseau, elle applique les paramètres spécifiés dans cette étape. 
- La séquence de tâches applique ces paramètres aux cartes réseau dans l’ordre d’énumération des appareils Windows.  
- La séquence de tâches n’applique pas immédiatement à l’ordinateur les paramètres que vous spécifiez dans cette étape. 



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Appliquer l’image du système d’exploitation  

> [!TIP]  
> À compter de Windows 10 version 1709, le média inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour l’utilisation d’un package de mise à niveau du système d’exploitation ou d’une image de système d’exploitation, veillez à sélectionner une [édition prise en charge](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

Utilisez cette étape pour installer un système d’exploitation sur l’ordinateur de destination. 

> [!NOTE]  
>  L’étape **Configurer Windows et ConfigMgr** démarre l’installation de Windows. 

À l’issue de l’exécution de l’action **Appliquer le système d’exploitation**, la variable **OSDTargetSystemDrive** est définie sur la lettre de lecteur de la partition contenant les fichiers du système d’exploitation.  

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet. 

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDConfigFileName](/sccm/osd/understand/task-sequence-variables#OSDConfigFileName)  
- [OSDImageIndex](/sccm/osd/understand/task-sequence-variables#OSDImageIndex)  
- [OSDTargetSystemDrive](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemDrive)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Appliquer l’image de système d’exploitation** pour ajouter cette étape. 

Cette étape effectue des actions selon qu’elle utilise une image de système d’exploitation ou un package de mise à niveau du système d’exploitation.  

#### <a name="os-image-actions"></a>Actions Image du système d’exploitation
L’étape **Appliquer l’image du système d’exploitation** effectue les actions suivantes si une image de système d’exploitation est utilisée :  

1. Supprime tout le contenu sur le volume cible, sauf les fichiers dans le dossier spécifié par la variable **\_SMSTSUserStatePath**.  

2. Extrait le contenu du fichier .wim spécifié sur la partition de destination spécifiée.  

3. Prépare le fichier de réponses :  

    1. Crée un fichier de réponses d’installation de Windows par défaut (sysprep.inf ou unattend.xml) pour le système d’exploitation déployé.  

    2. Fusionne les valeurs du fichier de réponses fourni par l’utilisateur.  

4. Copie les chargeurs de démarrage Windows dans la partition active.  

5. Configure boot.ini ou BCD (Boot Configuration Database) pour qu’ils référencent le système d’exploitation nouvellement installé.  

#### <a name="os-upgrade-package-actions"></a>Actions Package de mise à niveau du système d'exploitation
L’étape **Appliquer l’image du système d’exploitation** effectue les actions suivantes si un package de mise à niveau du système d’exploitation est utilisé :  

1. Supprime tout le contenu sur le volume cible, sauf les fichiers dans le dossier spécifié par la variable **\_SMSTSUserStatePath**.  

2. Prépare le fichier de réponses :  

    1. Crée un fichier de réponses entièrement nouveau, contenant les valeurs standard produites par Configuration Manager.  

    2. Fusionne les valeurs du fichier de réponses fourni par l’utilisateur.  


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="apply-operating-system-from-a-captured-image"></a>Appliquer le système d'exploitation à partir d'une image capturée
Installe une image du système d’exploitation que vous avez capturée. Sélectionnez **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package**. Sélectionnez ensuite le package d’images existant à installer. Si plusieurs images sont associées au **Package d’images** spécifié, utilisez la liste déroulante pour spécifier l’image associée à utiliser pour ce déploiement. Pour afficher des informations de base sur chaque image existante, sélectionnez-la.  

#### <a name="apply-operating-system-image-from-an-original-installation-source"></a>Appliquer le système d'exploitation à partir d'une source d'installation d'origine
Installe un système d’exploitation à l’aide d’un package de mise à niveau du système d’exploitation, qui est également une source d’installation d’origine. Sélectionnez **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package de mise à niveau du système d’exploitation**. Sélectionnez ensuite le package de mise à niveau du système d’exploitation existant à utiliser. Pour afficher des informations de base sur chaque source d’image existante, sélectionnez-la. Les propriétés de la source d'image associée s'affichent dans le volet des résultats dans la partie inférieure de la boîte de dialogue. Si plusieurs éditions sont associées au package spécifié, utilisez la liste déroulante pour sélectionner **l’Édition** à utiliser.  

> [!NOTE]  
> Les **packages de mise à niveau du système d’exploitation** s’adressent principalement à une utilisation avec les mises à niveau sur place et pas pour les nouvelles installations de Windows. Lors du déploiement de nouvelles installations de Windows, utilisez l’option **Appliquer le système d'exploitation à partir d'une image capturée** et **install.wim** à partir des fichiers source d’installation.
> 
> Le déploiement de nouvelles installations de Windows avec des **Packages de mise à niveau du système d’exploitation** est toujours pris en charge, mais il exige des pilotes compatibles avec cette méthode. Lorsque vous installez Windows à partir d’un package de mise à niveau du système d’exploitation, les pilotes sont installés dans Windows PE au lieu d’être simplement injectés dans Windows PE. Tous les pilotes ne sont pas installables dans Windows PE.
> 
> Si les pilotes ne peuvent pas être installés dans Windows PE, créez une **Image de système d’exploitation** avec **install.wim** à partir des fichiers sources d’installation d’origine. Puis, déployez via l’option **Appliquer le système d'exploitation à partir d'une image capturée** à la place.

#### <a name="use-an-unattended-or-sysprep-answer-file-for-a-custom-installation"></a>Utiliser un fichier de réponse Sysprep ou autonome pour une installation personnalisée
Utilisez cette option pour fournir un fichier de réponses d'installation Windows (**unattend.xml**, **unattend.txt**ou **sysprep.inf**) selon la version du système d'exploitation et la méthode d'installation. Le fichier que vous spécifiez peut inclure toutes les options de configuration standard prises en charge par les fichiers de réponse. Par exemple, vous pouvez l'utiliser pour spécifier la page d'accueil par défaut d'Internet Explorer. Spécifiez le package qui contient le fichier de réponses et le chemin associé au fichier dans le package.  

> [!NOTE]  
> Le fichier de réponse d'installation Windows que vous fournissez peut contenir des variables de séquence de tâches incorporées au format `%varname%`, où *varname* correspond au nom de la variable. L’étape **Configurer Windows et ConfigMgr** remplace la chaîne de variable par la valeur réelle de la variable. Vous ne pouvez pas utiliser ces variables de séquence de tâches incorporées dans les champs exclusivement numériques d’un fichier de réponses unattend.xml.  

Si vous ne fournissez pas de fichier de réponses d’installation de Windows, la séquence de tâches génère automatiquement un fichier de réponses.  

#### <a name="destination"></a>Destination  
Configurez une des options suivantes :  

- **Prochaine partition disponible** : utilisez la partition séquentielle suivante qui n’a pas déjà été ciblée par une étape **Appliquer le système d’exploitation** ou **Appliquer l’image de données** dans cette séquence de tâches.  

- **Disque et partition spécifiques** : sélectionnez le numéro de **disque** (à partir de 0) et le numéro de **partition** (à partir de 1).  

- **Lettre de lecteur logique spécifique** : spécifiez la **lettre de lecteur** affectée à la partition par Windows PE. Cette lettre de lecteur peut être différente de la lettre de lecteur affectée par le système d’exploitation nouvellement déployé.  

- **Lettre de lecteur logique stockée dans une variable** : spécifiez la variable de séquence de tâches contenant la lettre de lecteur affectée à la partition par Windows PE. Cette variable est généralement définie dans la section Avancé de la boîte de dialogue **Propriétés de la partition** pour l’étape de séquence de tâches **Formater et partitionner le disque**.  


### <a name="options"></a>Options  

Outre les options par défaut, configurez les paramètres supplémentaires suivants sous l’onglet **Options** de cette étape de séquence de tâches :  

#### <a name="access-content-directly-from-the-distribution-point"></a>Accéder au contenu directement depuis le point de distribution
Configurez la séquence de tâches pour accéder à l’image du système d’exploitation directement depuis le point de distribution. Par exemple, utilisez cette option quand vous déployez des systèmes d’exploitation sur des appareils intégrés ayant une capacité de stockage limitée. Quand cette option est sélectionnée, configurez aussi les paramètres de partage du package sous l’onglet **Accès aux données** des propriétés de l’image du système d’exploitation.  

> [!NOTE]  
> Ce paramètre remplace l’option de déploiement que vous configurez dans la page **Points de distribution** de **l’Assistant Déploiement logiciel**. Ce remplacement est effectué seulement pour l’image du système d’exploitation spécifié par cette étape, et non pas pour le tout contenu de la séquence de tâches.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Appliquer les paramètres Windows  

Utilisez cette étape pour configurer les paramètres Windows de l’ordinateur de destination. La séquence de tâches stocke ces valeurs dans le fichier de réponses approprié. Le programme d’installation de Windows utilise ce fichier de réponses pendant l’étape **Configurer Windows et ConfigMgr**.  

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-input)  
- [OSDLocalAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDLocalAdminPassword)  
- [OSDProductKey](/sccm/osd/understand/task-sequence-variables#OSDProductKey)  
- [OSDRandomAdminPassword](/sccm/osd/understand/task-sequence-variables#OSDRandomAdminPassword)  
- [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-input)  
- [OSDRegisteredUserName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredUserName)  
- [OSDServerLicenseConnectionLimit](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseConnectionLimit)  
- [OSDServerLicenseMode](/sccm/osd/understand/task-sequence-variables#OSDServerLicenseMode)  
- [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-input)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Paramètres** et **Appliquer les paramètres Windows** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="user-name"></a>Nom d'utilisateur
Spécifiez le nom d'utilisateur inscrit à associer à l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres Windows**.  

#### <a name="organization-name"></a>Nom de l'organisation
Spécifiez le nom de l'organisation inscrite à associer à l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres Windows**.  

#### <a name="product-key"></a>Clé du produit  
Spécifiez la clé du produit à utiliser pour l'installation de Windows sur l'ordinateur de destination.  

#### <a name="server-licensing"></a>Licence serveur  
Spécifiez le mode de licence serveur. 
- Sélectionnez le mode de licence **Par serveur** ou **Par utilisateur**.  
- Si vous sélectionnez **Par serveur**, spécifiez également le nombre maximal de connexions autorisées selon les termes de votre contrat de licence.  
- Sélectionnez **Ne pas spécifier** si l'ordinateur de destination n'est pas un serveur ou si vous ne souhaitez pas spécifier le mode de licence.   

#### <a name="maximum-connections"></a>Nombre maximal de connexions
Spécifiez le nombre maximal de connexions disponibles pour cet ordinateur comme spécifié dans votre accord de licence.  

#### <a name="randomly-generate-the-local-administrator-password-and-disable-the-account-on-all-supported-platforms-recommended"></a>Générer de façon aléatoire le mot de passe de l'administrateur local et désactiver le compte sur toutes les plates-formes prises en charge (recommandé)  
Sélectionnez cette option pour que le mot de passe de l’administrateur local soit une chaîne générée de façon aléatoire. Cette option désactive également le compte d’administrateur local sur les plateformes qui prennent en charge cette fonctionnalité.  

#### <a name="enable-the-account-and-specify-the-local-administrator-password"></a>Activer le compte et spécifier le mot de passe de l'administrateur local  
Sélectionnez cette option pour activer le compte d’administrateur local avec le mot de passe spécifié. Entrez le mot de passe dans la ligne **Mot de passe** et confirmez-le dans la ligne **Confirmer le mot de passe** .  

#### <a name="time-zone"></a>Fuseau horaire
Spécifiez le fuseau horaire à configurer sur l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres Windows**.  



##  <a name="BKMK_AutoApplyDrivers"></a> Appliquer automatiquement les pilotes  

Utilisez cette étape pour trouver et installer des pilotes dans le cadre du déploiement du système d’exploitation.  

L'étape de séquence de tâches **Appliquer automatiquement les pilotes** effectue les actions suivantes :  

1. Analyse le matériel et trouve les ID Plug-and-Play de tous les périphériques présents sur le système.  

2. Envoie la liste des périphériques et leurs ID Plug-and-Play au point de gestion. Celui-ci retourne depuis le catalogue de pilotes une liste de pilotes compatibles pour chaque périphérique matériel. La liste inclut tous les pilotes activés quel que soit le package de pilotes où ils se trouvent, les pilotes étiquetés avec la catégorie de pilotes spécifiée.  

3. Pour chaque périphérique matériel, la séquence de tâches choisit le meilleur pilote. Ce pilote est approprié pour le système d’exploitation déployé et se trouve sur un point de distribution accessible.  

4. La séquence de tâches télécharge les pilotes sélectionnés à partir d’un point de distribution et prépare les pilotes sur le système d’exploitation cible.  

    1. Lorsque vous utilisez une image de système d’exploitation, la séquence de tâches place les pilotes dans le magasin de pilotes du système d’exploitation.  

    2. Lorsque vous utilisez un package de mise à niveau du système d’exploitation comme source d’installation d’origine, la séquence de tâches configure l’installation de Windows avec l’emplacement des pilotes.  

5. Lors de l’étape **Configurer Windows et ConfigMgr** de la séquence de tâches, l’installation de Windows recherche les pilotes préparés par cette étape.  

> [!IMPORTANT]  
> Un média autonome ne peut pas utiliser l’étape **Appliquer automatiquement les pilotes**. Dans ce scénario, la séquence de tâches n’a pas de connexion au site Configuration Manager.  

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet.

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDAutoApplyDriverBestMatch](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverBestMatch)  
- [OSDAutoApplyDriverCategoryList](/sccm/osd/understand/task-sequence-variables#OSDAutoApplyDriverCategoryList)  
- [SMSTSDriverRequestConnectTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestConnectTimeOut)  
- [SMSTSDriverRequestReceiveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestReceiveTimeOut)  
- [SMSTSDriverRequestResolveTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestResolveTimeOut)  
- [SMSTSDriverRequestSendTimeOut](/sccm/osd/understand/task-sequence-variables#SMSTSDriverRequestSendTimeOut)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Pilotes** et **Appliquer automatiquement les pilotes** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="install-only-the-best-matched-compatible-drivers"></a>Installer uniquement les pilotes compatibles les plus appropriés
Indique que l'étape de séquence de tâches installe uniquement le pilote le plus approprié pour chaque périphérique matériel détecté.  

#### <a name="install-all-compatible-drivers"></a>Installer tous les pilotes compatibles
La séquence de tâches installe tous les pilotes compatibles pour chaque périphérique matériel détecté. L’installation de Windows choisit ensuite le meilleur pilote. Cette option utilise davantage d’espace disque et de bande passante réseau. La séquence de tâches télécharge plus de pilotes, mais Windows peut sélectionner un meilleur pilote.  

#### <a name="consider-drivers-from-all-categories"></a>Considérer les pilotes de toutes les catégories
La séquence de tâches recherche les pilotes de périphériques appropriés dans toutes les catégories de pilotes disponibles.  

#### <a name="limit-driver-matching-to-only-consider-drivers-in-selected-categories"></a>Limiter la correspondance des pilotes aux pilotes des catégories sélectionnées uniquement
La séquence de tâches recherche les pilotes de périphériques appropriés dans les catégories de pilotes spécifiées.  

#### <a name="do-unattended-installation-of-unsigned-drivers-on-versions-of-windows-where-this-is-allowed"></a>Effectuer une installation autonome des pilotes non signés sur les versions de Windows le permettant
Cette option permet à Windows Installer des pilotes sans signature numérique.   

> [!IMPORTANT]  
> Cette option ne s’applique pas aux systèmes d’exploitation où vous ne pouvez pas configurer la stratégie de signature des pilotes.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capturer les paramètres réseau  

Utilisez cette étape pour capturer les paramètres réseau Microsoft de l’ordinateur exécutant la séquence de tâches. La séquence de tâches enregistre ces paramètres dans des variables de séquence de tâches. Ces paramètres remplacent les paramètres par défaut que vous configurez pour l’étape **Appliquer les paramètres réseau**.  

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDMigrateAdapterSettings](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdapterSettings)  
- [OSDMigrateNetworkMembership](/sccm/osd/understand/task-sequence-variables#OSDMigrateNetworkMembership)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Paramètres** et **Capturer les paramètres réseau** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="migrate-domain-and-workgroup-membership"></a>Migrer l'appartenance au groupe de travail ou au domaine 
Capture les informations d'appartenance du domaine et du groupe de travail de l'ordinateur de destination.  

#### <a name="migrate-network-adapter-configuration"></a>Migrer la configuration de la carte réseau
Capture la configuration de la carte réseau de l'ordinateur de destination. Il capture les informations suivantes : 
- Paramètres de réseau global  
- Nombre de cartes réseau  
- Les paramètres réseau suivants associés à chaque carte réseau : DNS, WINS, IP et filtres de port



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturer l’image du système d’exploitation  

Cette étape capture une ou plusieurs images à partir d’un ordinateur de référence. La séquence de tâches crée un fichier d’image Windows (.wim) sur le partage réseau spécifié. Utilisez ensuite **l’Assistant Ajout d’un package d’image de système d’exploitation** pour importer cette image dans Configuration Manager pour les déploiements de systèmes d’exploitation à base d’image.  

Configuration Manager capture chaque volume (lecteur) sur l’ordinateur de référence dans une image distincte au sein du fichier .wim. Si l’ordinateur de référence a plusieurs volumes, le fichier .wim obtenu contient une image distincte pour chaque volume. Seuls les volumes formatés au format NTFS ou FAT32 sont capturés à cette étape. Les volumes d'un autre format et les volumes USB sont ignorés.  

Le système d’exploitation installé sur l’ordinateur de référence doit être une version de Windows prise en charge par Configuration Manager. Utilisez l’outil SysPrep pour préparer le système d’exploitation de l’ordinateur de référence. Le volume du système d'exploitation installé et le volume de démarrage doivent correspondre.  

Spécifiez un compte disposant d’autorisations d’écriture sur le partage réseau sélectionné. Pour plus d’informations sur le compte de capture de l’image du système d’exploitation, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account).

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet. 

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDCaptureAccount](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccount)  
- [OSDCaptureAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDCaptureAccountPassword)  
- [OSDCaptureDestination](/sccm/osd/understand/task-sequence-variables#OSDCaptureDestination)  
- [OSDImageCreator](/sccm/osd/understand/task-sequence-variables#OSDImageCreator)  
- [OSDImageDescription](/sccm/osd/understand/task-sequence-variables#OSDImageDescription)  
- [OSDImageVersion](/sccm/osd/understand/task-sequence-variables#OSDImageVersion)  
- [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-input)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Capturer l’image de système d’exploitation** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="target"></a>Target  
Chemin d’accès du système de fichiers menant à l’emplacement qu’utilise Configuration Manager pour stocker l’image de système d’exploitation capturée.  

#### <a name="description"></a>Description  
Description facultative définie par l'utilisateur de l'image du système d'exploitation capturée qui est stockée dans le fichier d’image.  

#### <a name="version"></a>Version  
Numéro de version facultatif défini par l'utilisateur à attribuer à l'image du système d'exploitation capturée. Cette valeur peut représenter n'importe quelle combinaison de lettres et de chiffres. Cette valeur est stockée dans le fichier d’image.  

#### <a name="created-by"></a>Créé par  
Nom facultatif de l'utilisateur qui a créé l'image du système d’exploitation. Cette valeur est stockée dans le fichier d’image.  

#### <a name="capture-operating-system-image-account"></a>Compte Capturer l'image du système d'exploitation  
Entrez le compte Windows qui dispose des droits d'accès au partage réseau spécifié. Sélectionnez **Définir** pour spécifier le nom du compte Windows.  



##  <a name="BKMK_CaptureUserState"></a> Capturer l’état utilisateur  

Cette étape utilise l’outil de migration utilisateur (USMT) pour capturer l’état et les paramètres utilisateur de l’ordinateur exécutant la séquence de tâches. Cette étape de séquence de tâches est utilisée avec l'étape de séquence de tâches **Restaurer l'état utilisateur** . Cette étape chiffre toujours le magasin d’état USMT au moyen d’une clé de chiffrement générée et gérée par Configuration Manager.  

Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state).  

Si vous voulez enregistrer et restaurer les paramètres d’état utilisateur à partir d’un point de migration d’état, utilisez cette étape avec les étapes **Demander le magasin d’état** et **Libérer le magasin d’état**.  

Cette étape permet de contrôler un sous-ensemble limité des options USMT les plus couramment utilisées. D'autres options de ligne de commande peuvent être spécifiées au moyen de la variable de séquence de tâches **OSDMigrateAdditionalCaptureOptions**.  

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s’exécute dans le système d’exploitation complet.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [_OSDMigrateUsmtPackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtPackageID)  
- [OSDMigrateAdditionalCaptureOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalCaptureOptions)  
- [OSDMigrateConfigFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateConfigFiles)  
- [OSDMigrateContinueOnLockedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnLockedFiles)  
- [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateMode](/sccm/osd/understand/task-sequence-variables#OSDMigrateMode)  
- [OSDMigrateSkipEncryptedFiles](/sccm/osd/understand/task-sequence-variables#OSDMigrateSkipEncryptedFiles)  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **État utilisateur** et **Capturer l’état utilisateur** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="user-state-migration-tool-package"></a>Package de l'outil de migration de l'état utilisateur
Spécifiez le package qui contient l’outil USMT. La séquence de tâches utilise cette version de l’outil USMT pour capturer l’état et les paramètres utilisateur. Ce package ne requiert pas de programme. Spécifiez un package qui contient la version 32 bits ou 64 bits de l’outil USMT. L’architecture de l’outil USMT varie selon l’architecture du système d’exploitation à partir duquel la séquence de tâches capture l’état.  

#### <a name="capture-all-user-profiles-with-standard-options"></a>Capturer tous les profils utilisateur présentant les options standard
Migrez toutes les informations des profils utilisateur. Il s’agit de l’option par défaut.  

Si vous sélectionnez cette option, mais que vous ne sélectionnez pas **Restaurer les profils utilisateur de l’ordinateur local** dans l’étape **Restaurer l’état utilisateur**, la séquence de tâches échoue. Configuration Manager ne peut pas migrer les nouveaux comptes sans leur attribuer des mots de passe. 

Quand vous utilisez l’option **Installer un package d’image existant** de **l’Assistant Nouvelle séquence de tâches**, la séquence de tâches qui en résulte est par défaut **Capturer tous les profils utilisateur présentant les options standard**. Cette séquence de tâches par défaut ne sélectionne pas l’option permettant de **Restaurer les profils utilisateur de l’ordinateur local**, c’est-à-dire des comptes d’utilisateur n’appartenant pas au domaine.  

Sélectionnez **Restaurer les profils utilisateur de l'ordinateur local** et spécifiez un mot de passe pour le compte à migrer. Dans une séquence de tâches qui a été manuellement créée, ce paramètre est disponible sous l'étape **Restaurer l'état utilisateur**. Dans une séquence de tâches créée à l'aide de l'Assistant **Nouvelle séquence de tâches** , ce paramètre est disponible sur la page de l'assistant d'étape **Restaurer les fichiers et paramètres utilisateur** .  

Si vous ne disposez d’aucun compte d’utilisateur local, ce paramètre ne s’applique pas.  

#### <a name="customize-how-user-profiles-are-captured"></a>Personnaliser la façon dont les profils utilisateur sont capturés
Sélectionnez cette option pour indiquer un fichier de profil personnalisé pour la migration. Sélectionnez **Fichiers** pour choisir les fichiers de configuration qui seront utilisés par l’Outil USMT avec cette étape. Spécifiez un fichier .xml personnalisé contenant les règles qui définissent les fichiers d’état utilisateur à migrer.  

#### <a name="click-here-to-select-configuration-files"></a>Cliquez ici pour sélectionner les fichiers de configuration
Sélectionnez cette option pour sélectionner les fichiers de configuration dans le package USMT que vous souhaitez utiliser pour capturer les profils utilisateur. Sélectionnez le bouton **Fichiers** pour lancer la boîte de dialogue **Fichiers de configuration**. Pour spécifier un fichier de configuration, entrez son nom sur la ligne **Nom de fichier**, puis sélectionnez le bouton **Ajouter**.  

#### <a name="enable-verbose-logging"></a>Activer la journalisation documentée
Activez cette option pour générer des informations de fichiers journaux plus détaillées. Lors de la capture de l’état, la séquence de tâches par défaut génère **Scanstate.log** dans le dossier de journalisation de la séquence de tâches `%WinDir%\ccm\logs`.   

#### <a name="skip-files-using-encrypted-file-system"></a>Ignorer les fichiers utilisant le système de fichiers chiffrés (EFS)
Activez cette option pour ignorer la capture des fichiers chiffrés avec EFS (Encrypted File System). Ces fichiers incluent les fichiers de profil utilisateur. Selon les versions du système d'exploitation et d'USMT, les fichiers chiffrés peuvent ne pas être accessibles après la restauration. Pour plus d'informations, consultez la documentation d'USMT.  

#### <a name="copy-by-using-file-system-access"></a>Copier en utilisant l'accès au système de fichiers
Activez cette option pour spécifier les paramètres suivants :  

- **Continuer si certains fichiers ne peuvent pas être capturés** : activez ce paramètre pour continuer le processus de migration même si certains fichiers ne peuvent pas être capturés. Si vous désactivez cette option et qu’un fichier ne peut pas être capturé, cette étape échoue. Cette option est activée par défaut.  

- **Capturer localement en utilisant les liens au lieu de copier les fichiers**: activez ce paramètre pour utiliser des liens physiques NTFS pour capturer les fichiers.  

    Pour plus d'informations sur la migration de données à l'aide de liens directs, consultez [Magasin de migration de lien direct](https://docs.microsoft.com/windows/deployment/usmt/usmt-hard-link-migration-store).  

- **Capturer en mode hors-ligne (Windows PE uniquement)** : activez ce paramètre pour capturer l’état utilisateur dans Windows PE au lieu du système d’exploitation complet.  

#### <a name="capture-by-using-volume-copy-shadow-services-vss"></a>Capturer en utilisant Volume Copy Shadow Service (VSS)
Cette option vous permet de capturer des fichiers même s’ils sont verrouillés pour modification par une autre application.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capturer les paramètres Windows  

Utilisez cette étape pour capturer les paramètres Windows de l’ordinateur exécutant la séquence de tâches. La séquence de tâches enregistre ces paramètres dans des variables de séquence de tâches. Ces paramètres capturés remplacent les paramètres par défaut que vous configurez pour l’étape **Appliquer les paramètres Windows**.  

Cette étape de séquence de tâches s’exécute dans le système d’exploitation complet ou Windows PE.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDComputerName](/sccm/osd/understand/task-sequence-variables#OSDComputerName-output)  
- [OSDMigrateComputerName](/sccm/osd/understand/task-sequence-variables#OSDMigrateComputerName)  
- [OSDMigrateRegistrationInfo](/sccm/osd/understand/task-sequence-variables#OSDMigrateRegistrationInfo)  
- [OSDMigrateTimeZone](/sccm/osd/understand/task-sequence-variables#OSDMigrateTimeZone)  
- [OSDRegisteredOrgName](/sccm/osd/understand/task-sequence-variables#OSDRegisteredOrgName-output)  
- [OSDTimeZone](/sccm/osd/understand/task-sequence-variables#OSDTimeZone-output)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Paramètres** et **Capturer les paramètres Windows** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="migrate-computer-name"></a>Migrer le nom de l'ordinateur
Capture le nom NetBIOS de l’ordinateur.  

#### <a name="migrate-registered-user-and-organization-names"></a>Migrer les noms d'organisations et d'utilisateurs inscrits
Capture les noms des utilisateurs et des organisations inscrits à partir de l’ordinateur.  

#### <a name="migrate-time-zone"></a>Migrer le fuseau horaire
Capture le paramètre de fuseau horaire sur l’ordinateur.  



##  <a name="BKMK_CheckReadiness"></a> Vérifier la préparation  

Utilisez cette étape pour vérifier que l’ordinateur cible satisfait aux conditions des prérequis du déploiement spécifiées.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Vérifier la préparation** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="ensure-minimum-memory-mb"></a>Garantir une mémoire minimum (Mo)
Vérifiez que la quantité de mémoire (en Mo), atteint ou dépasse la quantité spécifiée. L’étape active ce paramètre par défaut.  

#### <a name="ensure-minimum-processor-speed-mhz"></a>Garantir une vitesse de processeur minimum (MHz)  
Vérifiez que la quantité de mémoire (en Mo) atteint ou dépasse la quantité spécifiée. L’étape active ce paramètre par défaut.  

#### <a name="ensure-minimum-free-disk-space-mb"></a>Garantir un espace disque libre minimum (Mo)
Vérifiez que la quantité d’espace disque libre (en Mo) atteint ou dépasse la quantité spécifiée.  

#### <a name="ensure-current-os-to-be-refreshed-is"></a>S'assurer que le SE à actualiser est
Vérifiez que le système d’exploitation installé sur l’ordinateur cible remplit la condition spécifiée. Par défaut, l’étape définit ce paramètre sur **CLIENT**.  


### <a name="options"></a>Options

> [!NOTE]  
> Si vous activez le paramètre **Continuer en cas d’erreur** sous l’onglet **Options** de cette étape, elle consigne seulement les résultats de la vérification de la préparation. Si une vérification échoue, la séquence de tâches ne s’arrête pas.  



##  <a name="BKMK_ConnectToNetworkFolder"></a> Se connecter à un dossier réseau  

Utilisez cette étape pour créer une connexion avec un dossier réseau partagé.  

Cette étape de séquence de tâches s’exécute dans le système d’exploitation complet ou Windows PE.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [SMSConnectNetworkFolderAccount](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderAccount)  
- [SMSConnectNetworkFolderDriveLetter](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderDriveLetter)  
- [SMSConnectNetworkFolderPassword](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPassword)  
- [SMSConnectNetworkFolderPath](/sccm/osd/understand/task-sequence-variables#SMSConnectNetworkFolderPath)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Se connecter à un dossier réseau** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="path"></a>Chemin d'accès  
Sélectionnez **Parcourir** pour spécifier le chemin du dossier réseau. Utilisez le format `\\server\share`.

#### <a name="drive"></a>Lecteur  
Sélectionnez la lettre de lecteur local à affecter pour cette connexion. 

#### <a name="account"></a>Compte 
Sélectionnez **Définir** afin de spécifier le compte d’utilisateur disposant des autorisations nécessaires pour se connecter à ce dossier réseau. Pour plus d'informations sur le compte de connexion à un dossier réseau de la séquence de tâches, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account).



##  <a name="BKMK_DisableBitLocker"></a> Désactiver BitLocker  

Utilisez cette étape pour désactive le chiffrement BitLocker sur le lecteur du système d’exploitation actuel ou sur un lecteur spécifique. Cette action laisse les protecteurs de clé visibles en texte clair sur le disque dur. Elle ne déchiffre le contenu du lecteur. Cette action se termine presque instantanément.  

> [!NOTE]  
> Le chiffrement de lecteur BitLocker propose un cryptage de bas niveau du contenu d'un volume de disque.  

Si vous avez plusieurs lecteurs chiffrés, désactivez BitLocker sur chaque lecteur de données avant de désactiver BitLocker sur le lecteur du système d'exploitation.  

Cette étape s’exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Disques** et **Désactiver BitLocker** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="current-operating-system-drive"></a>Lecteur du système d'exploitation actuel
Désactive BitLocker sur le lecteur du système d'exploitation actuel.  

#### <a name="specific-drive"></a>Lecteur spécifique  
Désactive BitLocker sur un disque spécifique. Dans la liste déroulante, sélectionnez le disque sur lequel BitLocker est désactivé.  



##  <a name="BKMK_DownloadPackageContent"></a> Télécharger le contenu du package  

Utilisez cette étape pour télécharger un des types de package suivants :  

- Images de système d’exploitation  
- Packages de mise à niveau de système d’exploitation  
- Packages de pilotes  
- Packages  
- Images de démarrage  

Cette étape fonctionne bien dans une séquence de tâches pour mettre à niveau un système d’exploitation dans les scénarios suivants :  

- Pour utiliser une seule séquence de tâches de mise à niveau qui peut fonctionner avec les plateformes x86 et x64. Incluez deux étapes **Télécharger le contenu du package** dans le groupe **Préparer pour la mise à niveau**. Spécifiez des conditions sous l’onglet **Options** pour détecter l’architecture du client et télécharger seulement le package de mise à niveau du système d’exploitation approprié. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable. Utilisez cette variable pour le chemin du média pour l’étape **Mettre à niveau le système d’exploitation**.  

- Pour télécharger dynamiquement un package de pilotes applicable, utilisez deux étapes **Télécharger le contenu du package** avec des conditions pour détecter le type de matériel approprié pour chaque package de pilotes. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable. Utilisez la variable pour la valeur de **Contenu intermédiaire** dans la section Pilotes de l’étape **Mettre à niveau le système d’exploitation**.  

> [!NOTE]  
> Quand vous déployez une séquence de tâches contenant cette étape, ne sélectionnez pas **Télécharger tout le contenu localement avant de démarrer la séquence de tâches** ou **Accéder au contenu directement depuis le point de distribution** pour les **Options de déploiement** dans la page **Points de distribution** de l’Assistant Déploiement logiciel.  

Cette étape s’exécute dans le système d’exploitation complet ou Windows PE. La possibilité d’enregistrer le package dans le cache du client Configuration Manager n’est pas prise en charge dans Windows PE.

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Logiciel** et **Télécharger le contenu du package** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="select-package"></a>Sélection du package  
Sélectionnez l’icône pour choisir le package à télécharger. Ensuite, répétez l’opération pour choisir un autre package.  

#### <a name="place-into-the-following-location"></a>Placez à l’emplacement suivant
Choisissez d’enregistrer le package à l’un des emplacements suivants :  

- **Répertoire de travail de la séquence de tâches** : cet emplacement est également appelé le cache de la séquence de tâches.  

- **Cache du client Configuration Manager** : utilisez cette option pour stocker le contenu dans le cache du client. Par défaut, ce chemin est le suivant : `%WinDir%\ccmcache`.  

- **Chemin personnalisé** : le moteur de séquence de tâches télécharge d’abord le package dans le répertoire de travail de séquence de tâches. Il déplace ensuite le contenu vers ce chemin d’accès que vous spécifiez. Le moteur de séquence de tâches ajoute le chemin avec l’ID de package.  

#### <a name="save-path-as-a-variable"></a>Enregistrez le chemin d’accès en tant que variable
Enregistrez le chemin d’accès du package dans une variable de séquence de tâches personnalisée. Utilisez ensuite cette variable dans une autre étape de la séquence de tâches. 

Configuration Manager ajoute un suffixe numérique au nom de la variable. Par exemple, vous spécifiez une variable `%MyContent%` en tant que variable personnalisée. Il s’agit de la racine de l’emplacement où la séquence de tâches stocke tout le contenu référencé pour cette étape. Ce contenu peut contenir plusieurs packages. Quand vous faites référence à la variable, ajoutez un suffixe numérique. Pour le premier package, consultez `%MyContent01%`. Quand vous faites référence à la variable dans des étapes ultérieures, par exemple **Mettre à niveau le système d’exploitation**, utilisez `%MyContent02%` ou `%MyContent03%`, où le numéro correspond à l’ordre dans lequel l’étape **Télécharger le contenu du package** répertorie les packages.  

#### <a name="if-a-package-download-fails-continue-downloading-other-packages-in-the-list"></a>En cas d’échec de téléchargement d’un package, continuer le téléchargement des autres packages de la liste
Si la séquence de tâches échoue à télécharger un package, elle commence à télécharger le package suivant dans la liste.  



##  <a name="BKMK_EnableBitLocker"></a> Activer BitLocker  

Utilisez cette étape pour activer le chiffrement BitLocker sur au moins deux partitions du disque dur. La première partition active contient le code d'amorçage Windows. Une autre partition contient le système d'exploitation. La partition d'amorçage ne doit pas être chiffrée.  

Utilisez l'étape **Préconfigurer BitLocker** pour activer BitLocker sur un lecteur dans Windows PE. Pour plus d’informations, consultez [Préconfigurer BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
> Le chiffrement de lecteur BitLocker propose un cryptage de bas niveau du contenu d'un volume de disque.  

Cette étape s’exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDBitLockerRecoveryPassword](/sccm/osd/understand/task-sequence-variables#OSDBitLockerRecoveryPassword)  
- [OSDBitLockerStartupKey](/sccm/osd/understand/task-sequence-variables#OSDBitLockerStartupKey)  

Quand vous spécifiez **TPM uniquement**, **TPM et clé de démarrage sur USB** ou **TPM et code confidentiel**, le module de plateforme sécurisée (TPM) doit être dans l’état suivant pour que vous puissiez effectuer l’étape **Activer BitLocker** :  
- Permis  
- Activé  
- Propriété autorisée  

Cette étape effectue l’initialisation des éventuels modules de plateforme sécurisée restants. Les étapes restantes ne nécessitent pas de présence physique ni de redémarrages. Si nécessaire, l’étape **Activer BitLocker** effectue de façon transparente les étapes suivantes d’initialisation des modules de plateforme sécurisée restants :  
- Créer une paire de clés de validité  
- Créer une valeur d'autorisation du propriétaire et la déposer dans Active Directory, qui doit avoir été développé afin de prendre en charge cette valeur.  
- Se définir comme propriétaire  
- Créer la clé racine de stockage ou la réinitialiser si elle existe déjà mais qu'elle est incompatible.  

Si vous voulez que la séquence de tâches attende que l’étape **Activer BitLocker** termine le processus de chiffrement du lecteur, sélectionnez l’option **Attendre**. Si vous ne sélectionnez pas l’option **Attendre**, le processus de chiffrement du lecteur est effectué en arrière-plan. La séquence de tâches passe immédiatement à l’étape suivante.  

BitLocker peut être utilisé pour chiffrer plusieurs lecteurs sur un système d’ordinateur, à la fois le système d’exploitation et les lecteurs de données. Pour chiffrer un lecteur de données, chiffrez d’abord le lecteur du système d’exploitation et terminez le processus de chiffrement. Cette opération est nécessaire, car le lecteur du système d’exploitation stocke les protecteurs de clé des lecteurs de données. Si vous chiffrez le lecteur du système d’exploitation et les lecteurs de données dans la même séquence de tâches, sélectionnez l’option **Attendre** pour l’étape **Activer BitLocker** pour le lecteur du système d’exploitation.  

Si le disque dur est déjà chiffré mais que BitLocker est désactivé, l’étape **Activer BitLocker** réactive les protecteurs de clé et se termine rapidement. Dans ce cas, il n'est pas nécessaire de chiffrer de nouveau le disque dur.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Disques** et **Activer BitLocker** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="choose-the-drive-to-encrypt"></a>Lecteur à chiffrer
Indique le lecteur à chiffrer. Pour chiffrer le lecteur du système d’exploitation actuel, sélectionnez **Lecteur du système d’exploitation actuel**. Ensuite, configurez l’une des options suivantes pour la gestion des clés :  

- **TPM uniquement**: sélectionnez cette option pour utiliser uniquement le module de plateforme sécurisée (TPM).  

- **Clé de démarrage sur USB uniquement**: sélectionnez cette option pour utiliser une clé de démarrage stockée sur une clé USB. Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce qu'un périphérique USB contenant une clé de démarrage BitLocker soit connecté à l'ordinateur.  

- **TPM et clé de démarrage sur USB**: sélectionnez cette option pour utiliser le module TPM et une clé de démarrage stockée sur une clé USB. Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce qu'un périphérique USB contenant une clé de démarrage BitLocker soit connecté à l'ordinateur.  

- **TPM et code confidentiel** : sélectionnez cette option pour utiliser le module TPM et un numéro d’identification personnel (code confidentiel). Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce que l'utilisateur fournisse le code confidentiel.  

Pour chiffrer un lecteur spécifique (un lecteur de données ne comportant pas de système d'exploitation), sélectionnez **Lecteur spécifique**. Puis sélectionnez le lecteur dans la liste.  

#### <a name="use-full-disk-encryption"></a>Utiliser le chiffrement de lecteur complet
<!--SCCMDocs-pr issue 2671-->
Par défaut, cette étape chiffre uniquement l’espace utilisé sur le lecteur. Ce comportement par défaut est recommandé, car il est plus rapide et plus efficace. À compter de la version 1806, si votre organisation doit chiffrer l’intégralité du lecteur durant l’installation, activez cette option. Le programme d’installation de Windows attend que le lecteur entier soit chiffré, ce qui prend beaucoup de temps, en particulier sur les grands lecteurs. 

#### <a name="choose-where-to-create-the-recovery-key"></a>Emplacement de création de la clé de récupération
Pour indiquer à BitLocker de créer le mot de passe de récupération et de déposer la clé dans Active Directory, sélectionnez **Dans Active Directory**. Cette option nécessite que vous étendiez Active Directory pour le dépôt de clé BitLocker. BitLocker peut ensuite enregistrer les informations de récupération associées dans Active Directory. Sélectionnez **Ne pas créer de clé de récupération** pour ne pas créer un mot de passe. La création d’un mot de passe est l’option recommandée.  

#### <a name="wait-for-bitlocker-to-complete-the-drive-encryption-process-on-all-drives-before-continuing-task-sequence-execution"></a>Attendez que BitLocker termine le processus de chiffrement des lecteurs avant de poursuivre l'exécution de la séquence de tâches
Sélectionnez cette option pour autoriser le chiffrement de lecteur BitLocker à se terminer avant l’exécution de la séquence de tâches suivante. Si vous sélectionnez cette option, BitLocker chiffre le volume de disque entier avant que l’utilisateur puisse se connecter à l’ordinateur.  

Le processus de chiffrement peut prendre des heures dans le cas du chiffrement d’un disque dur de grande taille. Si vous ne sélectionnez pas cette option, la séquence de tâches débute immédiatement.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formater et partitionner le disque  

Utilisez cette étape pour formater et partitionner un disque spécifié sur un ordinateur de destination.  

> [!IMPORTANT]  
> Chaque paramètre défini pour cette étape s'applique à un seul disque spécifié. Pour formater et partitionner un autre disque sur l’ordinateur de destination, ajoutez une étape supplémentaire **Formater et partitionner le disque** à la séquence de tâches.  

Cette étape est exécutée uniquement sous Windows PE. Elle ne s’exécute dans le système d’exploitation complet.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDDiskIndex](/sccm/osd/understand/task-sequence-variables#OSDDiskIndex)  
- [OSDGPTBootDisk](/sccm/osd/understand/task-sequence-variables#OSDGPTBootDisk)  
- [OSDPartitions](/sccm/osd/understand/task-sequence-variables#OSDPartitions)  
- [OSDPartitionStyle](/sccm/osd/understand/task-sequence-variables#OSDPartitionStyle)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Disques** et **Formater et partitionner le disque** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="disk-number"></a>Numéro du disque
Numéro de disque physique du disque à formater. Le numéro se base sur le classement d'énumération du disque Windows.  

#### <a name="disk-type"></a>Type du disque
Le type de disque à formater. Deux options sont disponibles dans la liste déroulante : 
- **Standard (MBR)** : secteur de démarrage principal  
- **GPT** : table de partition GUID  

> [!NOTE]  
> Si vous passez le type de disque de **Standard (MBR)** à **GPT** et si la structure des partitions contient une partition étendue, la séquence de tâches supprime toutes les partitions étendues et logiques de la structure. L’Éditeur de séquence de tâches vous invite à confirmer cette action avant de changer le type de disque.  

#### <a name="volume"></a>Volume
Informations spécifiques sur la partition ou le volume créé par la séquence de tâches, incluant les attributs suivants :  
- Nom  
- Espace disque restant  

Pour créer une partition, sélectionnez **Nouveau** afin de lancer la boîte de dialogue **Propriétés de la partition**. Spécifiez le type et la taille de la partition, et s’il s’agit d’une partition de démarrage. Pour modifier une partition existante, choisissez-la, puis sélectionnez le bouton **Propriétés**. Pour plus d’informations sur la façon de configurer des partitions de disque dur, consultez un des articles suivants :  

- [Partitions de disque dur UEFI/GPT](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-uefigpt-based-hard-drive-partitions)  
- [Partitions de disque dur BIOS/MBR](https://docs.microsoft.com/windows-hardware/manufacture/desktop/configure-biosmbr-based-hard-drive-partitions)  

Pour supprimer une partition, choisissez-la, puis sélectionnez **Supprimer**.  



##  <a name="BKMK_InstallApplication"></a> Installer l’application  

Cette étape installe les applications spécifiées, ou un ensemble d’applications défini par une liste dynamique de variables de séquence de tâches. Lorsque la séquence de tâches exécute cette étape, l'installation de l'application commence immédiatement sans attendre un intervalle d'interrogation de stratégie.  

Les applications doivent respecter les critères suivants :  

- L’application doit avoir un type de déploiement **Windows Installer** ou programme d’installation de **script**. Les types de déploiement Package d’application Windows (fichier .appx) ne sont pas pris en charge.  

- Il doit être exécuté sous le compte Système local et non le compte utilisateur.  

- Il ne doit pas interagir avec le Bureau. Le programme doit s'exécuter en mode silencieux ou en mode sans assistance.  

- Il ne doit pas lancer un redémarrage seul. L'application doit demander un redémarrage à l'aide du code de redémarrage standard 3010. Ce comportement permet de s’assurer que cette étape gère correctement le redémarrage. Si l’application retourne un code de sortie 3010, le moteur de séquences de tâches redémarre l’ordinateur. Après le redémarrage, la séquence de tâches se poursuit automatiquement.  

Quand cette étape s’exécute, l’application vérifie l’applicabilité des règles de spécification et la méthode de détection sur ses types de déploiement. Selon les résultats de cette vérification, l'application installe le type de déploiement applicable. Si un type de déploiement contient des dépendances, le type de déploiement dépendant est évalué et installé dans le cadre de cette étape. Les dépendances d'application ne sont pas prises en charge pour les médias autonomes.  

> [!NOTE]  
> Pour installer une application qui en remplace une autre, les fichiers de contenu de l’application remplacée doivent être disponibles. Si ce n’est pas le cas, cette étape de la séquence de tâches échoue. Par exemple, Microsoft Visio 2010 est installé sur un client ou dans une image capturée. Quand l’étape **Installer l’application** installe Microsoft Visio 2013, les fichiers de contenu de Microsoft Visio 2010 (l’application remplacée) doivent être disponibles sur un point de distribution. Si Microsoft Visio n’est pas installé du tout sur un client ou sur l’image capturée, la séquence de tâches installe Microsoft Visio 2013 sans rechercher les fichiers de contenu Microsoft Visio 2010.  

> [!NOTE]  
> Si le client ne parvient pas à extraire la liste des points de gestion à partir des services d’emplacement, utilisez les variables de séquence de tâches **SMSTSMPListRequestTimeoutEnabled** et **SMSTSMPListRequestTimeout**. Ces variables spécifient le délai d’attente en millisecondes d’une séquence de tâches avant de retenter l’installation d’une application. Pour plus d’informations, consultez [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables).

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [_TSAppInstallStatus](/sccm/osd/understand/task-sequence-variables#TSAppInstallStatus)  
- [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
- [TSErrorOnWarning](/sccm/osd/understand/task-sequence-variables#TSErrorOnWarning)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Logiciel** et **Installer une application** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** pour cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="install-the-following-applications"></a>Installer les applications suivantes
La séquence de tâches installe ces applications dans l’ordre spécifié.  

Configuration Manager exclut toutes les applications désactivées ou les applications avec les paramètres suivants :  

- Uniquement quand un utilisateur a ouvert une session  
- Exécuter avec les droits utilisateur  

Ces applications n’apparaissent pas dans la boîte de dialogue **Sélectionner l’application à installer**.

#### <a name="install-applications-according-to-dynamic-variable-list"></a>Installer les applications en fonction de la liste de variables dynamiques
La séquence de tâches installe les applications en utilisant ce nom de variable de base. Le nom de variable de base vaut pour un ensemble de variables de séquence de tâches définies pour un regroupement ou un ordinateur. Ces variables spécifient les applications que la séquence de tâches installe pour ce regroupement ou cet ordinateur. Chaque nom de variable comprend son nom de base courant plus un suffixe numérique commençant par 01. La valeur de chaque variable doit contenir le nom de l'application et rien d'autre.  

Pour que la séquence de tâches installe les applications en utilisant une liste de variables dynamiques, activez le paramètre suivant sous l’onglet **Général** de la boîte de dialogue **Propriétés** de l’application : **Autoriser cette application à être installée à partir de l’action de la séquence de tâches Installer l’application plutôt que de la déployer manuellement**.  

> [!NOTE]  
> Vous ne pouvez pas installer d'applications à l'aide d'une liste de variables dynamiques pour les déploiements de média autonome.  

Par exemple, pour installer une application unique à l'aide d'une variable de séquence de tâches nommée AA01, vous indiquez la variable suivante :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Pour installer deux applications, spécifiez les variables suivantes :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Les conditions suivantes affectent les applications installées par la séquence de tâches :  

- Si la valeur d'une variable contient d'autres informations que le nom de l'application. La séquence de tâches n’installe pas l’application et elle continue.  

- Si la séquence de tâches ne trouve pas une variable portant le nom de base spécifié et le suffixe « 01 », elle n’installe aucune application.  

> [!Important]  
> Ces valeurs de texte respectent la casse. Par exemple, « installer » ne correspond pas à « Installer ». Si vous devez modifier la valeur, l’éditeur de séquence de tâches ne détecte pas un changement de casse. Effectuez une autre modification en même temps, par exemple, modifiez la description de l’étape.<!--509714-->   

#### <a name="if-an-application-fails-continue-installing-other-applications-in-the-list"></a>Si l'installation d'une application échoue, continuer d'installer les autres applications de la liste
Ce paramètre spécifie que l’étape continue quand l’installation d’une application individuelle échoue. Si vous spécifiez ce paramètre, la séquence de tâches continue indépendamment des erreurs d’installation. Si vous ne spécifiez pas ce paramètre et que l’installation échoue, l’étape se termine immédiatement.  


### <a name="options"></a>Options

> [!NOTE]  
> Quand vous sélectionnez **Continuer en cas d’erreur** sous l’onglet **Options** de cette étape, la séquence de tâches continue quand l’installation d’une application échoue. Quand vous n’activez pas cette option, la séquence de tâches échoue et n’installe pas les applications restantes.  

Outre les options par défaut, configurez les paramètres supplémentaires suivants sous l’onglet **Options** de cette étape de séquence de tâches :  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Recommencer cette étape si l’ordinateur redémarre inopinément
Si une des installations d’application redémarre l’ordinateur de façon inattendue, recommence cette étape. L’étape active ce paramètre par défaut avec deux nouvelles tentatives. Vous pouvez spécifier de une à cinq nouvelles tentatives.  



##  <a name="BKMK_InstallPackage"></a> Installer le package

Utilisez cette étape pour installer un package logiciel dans le cadre de la séquence de tâches. Quand cette étape est exécutée, l’installation commence immédiatement sans attendre un intervalle d’interrogation de stratégie.  

Le package doit respecter les critères suivants :  

- Il doit être exécuté sous le compte Système local et non pas sous un compte d’utilisateur.  

- Il ne doit pas interagir avec le Bureau. Le programme doit s'exécuter en mode silencieux ou en mode sans assistance.  

- Il ne doit pas lancer un redémarrage seul. Le logiciel doit demander un redémarrage à l'aide du code de redémarrage standard, 3010. Ce comportement garantit que la séquence de tâches gère correctement le redémarrage. Si le logiciel retourne un code de sortie 3010, le moteur de séquences de tâches redémarre l’ordinateur. Après le redémarrage, la séquence de tâches se poursuit automatiquement.  

Les programmes qui utilisent l'option **Exécuter un autre programme en premier** pour installer un programme dépendant ne sont pas pris en charge lors du déploiement d'un système d'exploitation. Si vous activez l’option **Exécuter un autre programme en premier** et que le programme dépendant a déjà été exécuté sur l’ordinateur de destination, le programme dépendant s’exécute et la séquence de tâches continue. En revanche, si le programme dépendant n’a pas déjà été exécuté sur l’ordinateur de destination, l’étape de la séquence de tâches échoue.  

> [!NOTE]  
> Le site d’administration centrale n’a pas les stratégies de configuration de client nécessaires pour activer l’agent de distribution logicielle lors de l’exécution de la séquence de tâches. Lorsque vous créez un média autonome pour une séquence de tâches sur le site d'administration centrale et que la séquence de tâches contient une étape **Installer le package** , l'erreur suivante peut apparaître dans le fichier CreateTsMedia.log :  
>   
> `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
> 
> Pour un média autonome qui inclut une étape **Installer le package**, créez le média autonome sur un site principal où l’agent de distribution logicielle est activé. Vous pouvez aussi ajouter une étape **Exécuter la ligne de commande** après l’étape **Configurer Windows et ConfigMgr** et avant la première étape **Installer le package**. L’étape **Exécuter la ligne de commande** exécute une commande WMIC pour activer l’agent de distribution logicielle avant la première étape **Installer le package**. Utilisez la commande suivante dans l’étape **Exécuter la ligne de commande** :  
> 
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
> 
> Pour plus d’informations sur la création d’un média autonome, consultez [Créer un média autonome](/sccm/osd/deploy-use/create-stand-alone-media).  

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Logiciel** et **Installer un package** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="install-a-single-software-package"></a>Installer un seul package logiciel
Ce paramètre permet de spécifier un package logiciel Configuration Manager. L’étape attend que l’installation se termine.  

#### <a name="install-software-packages-according-to-dynamic-variable-list"></a>Installer les packages logiciels en fonction de la liste de variables dynamiques
La séquence de tâches installe les packages en utilisant ce nom de variable de base. Le nom de variable de base vaut pour un ensemble de variables de séquence de tâches définies pour un regroupement ou un ordinateur. Ces variables spécifient les packages que la séquence de tâches installe pour ce regroupement ou cet ordinateur. Chaque nom de variable comprend son nom de base courant plus un suffixe numérique commençant par 001. La valeur de chaque variable doit contenir un ID de package et le nom du logiciel séparés par deux-points.  

Pour que la séquence de tâches installe les logiciels en utilisant une liste de variables dynamiques, activez le paramètre suivant sous l’onglet **Avancé** de la boîte de dialogue **Propriétés** du package : **Autoriser l’installation de ce programme depuis la séquence de tâches d’installation du package sans le déployer**.  

> [!NOTE]  
> Vous ne pouvez pas installer de packages logiciels à l'aide d'une liste de variables dynamiques pour les déploiements de média autonome.  

Par exemple, pour installer un package logiciel unique à l'aide d'une variable de séquence de tâches nommée AA001, vous indiquez la variable suivante :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

Pour installer trois packages logiciels, vous indiqueriez les variables suivantes :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

Les conditions suivantes affectent les packages installés par la séquence de tâches :  

- Si vous ne créez pas la valeur d’une variable au format correct, ou si elle ne spécifie pas un ID et un nom de package valides, l’installation du logiciel échoue.  

- Si l’ID de package contient des caractères en minuscules, l’installation du logiciel échoue.  

- Si la séquence de tâches ne trouve pas une variable portant le nom de base spécifié et le suffixe « 001 », elle n’installe aucun package. La séquence de tâches continue.  

> [!Important]  
> Ces valeurs de texte respectent la casse. Par exemple, « installer » ne correspond pas à « Installer ». Si vous devez modifier la valeur, l’éditeur de séquence de tâches ne détecte pas un changement de casse. Effectuez une autre modification en même temps, par exemple, modifiez la description de l’étape.<!--509714-->   

#### <a name="if-installation-of-a-software-package-fails-continue-installing-other-packages-in-the-list"></a>Si l'installation d'un package logiciel échoue, continuer d'installer les autres packages de la liste
Ce paramètre spécifie que l'étape se poursuit si l'installation d'un package logiciel individuel échoue. Si vous spécifiez ce paramètre, la séquence de tâches continue indépendamment des erreurs d’installation. Si vous ne spécifiez pas ce paramètre et que l’installation échoue, l’étape se termine immédiatement.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Installer les mises à jour logicielles  

Utilisez cette étape pour installer des mises à jour logicielles sur l’ordinateur de destination. L'ordinateur de destination n'est pas évalué pour déterminer les mises à jour logicielles applicables avant l'exécution de cette séquence de tâches. À ce moment, l’ordinateur de destination est évalué pour déterminer les mises à jour logicielles comme n’importe quel autre client Configuration Manager. Pour que cette étape installe des mises à jour logicielles, déployez d’abord les mises à jour sur un regroupement dont l’ordinateur cible est membre.  

> [!IMPORTANT]  
> Pour des performances optimales, installez la dernière version de l’Agent Windows Update.  

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE. 

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [SMSInstallUpdateTarget](/sccm/osd/understand/task-sequence-variables#SMSInstallUpdateTarget)  
- [SMSTSMPListRequestTimeoutEnabled](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeoutEnabled)  
- [SMSTSMPListRequestTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSMPListRequestTimeout)  
- [SMSTSSoftwareUpdateScanTimeout](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout)  
- [SMSTSWaitForSecondReboot](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot)  

> [!NOTE]  
> Si le client ne parvient pas à extraire la liste des points de gestion à partir des services d’emplacement, utilisez les variables **SMSTSMPListRequestTimeoutEnabled** et **SMSTSMPListRequestTimeout**. Ces variables spécifient le délai d’attente en millisecondes d’une séquence de tâches avant de retenter l’installation d’une application ou la mise à jour logicielle. Pour plus d’informations, voir [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables).  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Logiciel** et **Installer des mises à jour de logiciels** pour ajouter cette étape. 

Pour obtenir des recommandations et l’organigramme technique de cette étape, voir [Installer des mises à jour de logiciels](/sccm/osd/understand/install-software-updates).


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="required-for-installation---mandatory-software-updates-only"></a>Nécessaires pour l’installation – Mises à jour logicielles obligatoires seulement
Sélectionnez cette option pour installer toutes les mises à jour logicielles obligatoires avec des dates d’échéance d’installation définies par l’administrateur.  

#### <a name="available-for-installation---all-software-updates"></a>Disponibles pour l’installation – Toutes les mises à jour logicielles
Sélectionnez cette option pour installer toutes les mises à jour logicielles disponibles. Déployez d’abord ces mises à jour sur un regroupement dont l’ordinateur est membre. La séquence de tâches installe toutes les mises à jour logicielles disponibles sur les ordinateurs de destination.  

#### <a name="evaluate-software-updates-from-cached-scan-results"></a>Évaluer les mises à jour logicielles à partir des résultats d’analyse en mémoire cache
Par défaut, cette étape utilise les résultats de l’analyse en mémoire cache provenant de l’Agent Windows Update. Désactivez cette option pour indiquer à l’Agent Windows Update de télécharger le dernier catalogue à partir du point de mise à jour logicielle. Activez cette option lors de l’utilisation d’une séquence de tâches pour [capturer et créer une image de système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system). Dans ce scénario, le nombre de mises à jour logicielles est probablement élevé. 

La plupart de ces mises à jour ont des dépendances. Par exemple, installez la mise à jour ABC avant que la mise à jour XYZ n’apparaisse comme étant applicable. Quand vous désactivez ce paramètre et que vous déployez la séquence de tâches sur un grand nombre de clients, ils se connectent tous en même temps au point de mise à jour logicielle. Ce comportement peut entraîner des problèmes de performances pendant le traitement et le téléchargement du catalogue de mise à jour. 

Dans la plupart des cas, utilisez le paramètre par défaut pour utiliser les résultats de l’analyse en cache. 

La variable **SMSTSSoftwareUpdateScanTimeout** contrôle le délai d’expiration de l’analyse des mises à jour logicielles pendant cette étape. La valeur par défaut est de 30 minutes. Pour plus d’informations, voir [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSSoftwareUpdateScanTimeout).


### <a name="options"></a>Options   

Outre les options par défaut, configurez les paramètres supplémentaires suivants sous l’onglet **Options** de cette étape de séquence de tâches :  

#### <a name="retry-this-step-if-computer-unexpectedly-restarts"></a>Recommencer cette étape si l’ordinateur redémarre inopinément
Si une des mises à jour redémarre l’ordinateur de façon inattendue, recommence cette étape. L’étape active ce paramètre par défaut avec deux nouvelles tentatives. Vous pouvez spécifier de une à cinq nouvelles tentatives.  

> [!NOTE]  
> Configurez la variable **SMSTSWaitForSecondReboot** pour spécifier le nombre de secondes de mise en suspens de la séquence de tâches après le redémarrage de l’ordinateur dans ce scénario. Pour plus d’informations, voir [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSWaitForSecondReboot).  



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Joindre le domaine ou le groupe de travail  

Utilisez cette étape pour ajouter l’ordinateur de destination à un domaine ou un groupe de travail.  

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDJoinAccount](/sccm/osd/understand/task-sequence-variables#OSDJoinAccount)  
- [OSDJoinDomainName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainName)  
- [OSDJoinDomainOUName](/sccm/osd/understand/task-sequence-variables#OSDJoinDomainOUName)  
- [OSDJoinPassword](/sccm/osd/understand/task-sequence-variables#OSDJoinPassword)  
- [OSDJoinSkipReboot](/sccm/osd/understand/task-sequence-variables#OSDJoinSkipReboot)  
- [OSDJoinType](/sccm/osd/understand/task-sequence-variables#OSDJoinType)  
- [OSDJoinWorkgroupName](/sccm/osd/understand/task-sequence-variables#OSDJoinWorkgroupName)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Joindre un domaine ou un groupe de travail** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="join-a-workgroup"></a>Joindre un groupe de travail
Sélectionnez cette option pour que l'ordinateur de destination fasse partie du groupe de travail spécifié. Si l’ordinateur est actuellement membre d’un domaine, la sélection de cette option provoque son redémarrage.  

#### <a name="join-a-domain"></a>Joindre un domaine
Sélectionnez cette option pour que l'ordinateur de destination fasse partie du domaine spécifié.  

Facultatif : entrez ou accédez à une unité d'organisation du domaine spécifié pour que l'ordinateur s'y joigne. Si l’ordinateur est actuellement membre d’un autre domaine ou groupe de travail, cette option provoque son redémarrage. Si l’ordinateur est déjà membre d’une autre unité d’organisation, dans la mesure où Active Directory Domain Services n’autorise pas le changement de l’unité d’organisation via cette méthode, l’installation de Windows ignore ce paramètre.  

#### <a name="enter-the-account-which-has-permission-to-join-the-domain"></a>Entrez le compte autorisé à joindre le domaine
Sélectionnez **Définir** afin d’entrer le nom d’utilisateur et le mot de passe d’un compte disposant des autorisations nécessaires pour joindre le domaine. Entrez le compte au format : `Domain\account`. Pour plus d'informations sur le compte de jonction de domaine de la séquence de tâches, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account).  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Préparer le client ConfigMgr pour capture  

Utilisez cette étape pour supprimer ou configurer le client Configuration Manager sur l’ordinateur de référence. Cette action prépare l’ordinateur pour la capture dans le cadre du processus de création d’image.

Cette étape supprime complètement le client Configuration Manager, au lieu de supprimer uniquement des informations clés. Quand la séquence de tâches déploie l’image capturée du système d’exploitation, elle installe chaque fois un nouveau client Configuration Manager.  

> [!Note]  
> Le moteur de séquence de tâches supprime seulement le client pendant la séquence de tâches **Créer et capturer une image de système d’exploitation de référence**. Le moteur de séquence de tâches ne supprime pas le client lors de l’application des autres méthodes de capture, comme un média de capture ou une séquence de tâches personnalisée.  

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Préparer le client ConfigMgr à la capture** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Cette étape ne nécessite aucun paramètre sous l’onglet **Propriétés**.



## <a name="BKMK_PrepareWindowsforCapture"></a> Préparer Windows pour capture  

Utilisez cette étape pour spécifier les options Sysprep à utiliser lors de la capture d’une image de système d’exploitation sur l’ordinateur de référence. Cette étape exécute Sysprep puis redémarre l'ordinateur dans l'image de démarrage Windows PE spécifiée pour la séquence de tâches. Cette action échoue si l’ordinateur de référence est joint à un domaine.  

Cette étape s’exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDKeepActivation](/sccm/osd/understand/task-sequence-variables#OSDKeepActivation)  
- [OSDTargetSystemRoot](/sccm/osd/understand/task-sequence-variables#OSDTargetSystemRoot-output)  


Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Préparer Windows à la capture** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="automatically-build-mass-storage-driver-list"></a>Créer automatiquement la liste des pilotes de stockage de masse
Sélectionnez cette option pour demander à Sysprep de générer automatiquement une liste de pilotes de stockage de masse à partir de l'ordinateur de référence. Cette option active l'option des pilotes de stockage de masse dans le fichier sysprep.inf sur l'ordinateur de référence. Pour plus d’informations sur ce paramètre, consultez la documentation de Sysprep.  

#### <a name="do-not-reset-activation-flag"></a>Ne pas réinitialiser l'indicateur d'activation
Choisissez cette option pour empêcher Sysprep de réinitialiser l'indicateur d'activation du produit.  

#### <a name="shutdown-the-computer-after-running-this-action"></a>Arrêter l’ordinateur après l’exécution de cette action
<!--SCCMDocs-pr issue 2695-->
À compter de la version 1806, cette option indique à Sysprep d’arrêter l’ordinateur au lieu d’appliquer son comportement de redémarrage par défaut. 

Depuis la version 1810, cette étape est utilisée dans la séquence de tâches [Windows Autopilot pour les appareils existants](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).

- Si vous souhaitez que la séquence de tâches actualise l’appareil, puis lance immédiatement OOBE pour Autopilot, laissez cette option désactivée.  

- Activez cette option pour arrêter l’appareil après la création d’images. Vous pouvez ensuite remettre l’appareil à un utilisateur, qui lance OOBE avec Autopilot à la première mise sous tension.  



## <a name="BKMK_PreProvisionBitLocker"></a> Préconfigurer BitLocker  

Utilisez cette étape pour activer BitLocker sur un lecteur dans Windows PE. Par défaut, seul l'espace disque utilisé est chiffré, donc l'opération de chiffrement est beaucoup plus rapide. Vous appliquez les options de gestion de clés à l'aide de l'étape [Activer BitLocker](#BKMK_EnableBitLocker) une fois le système d'exploitation installé. 

Cette étape est exécutée uniquement sous Windows PE. Elle ne s’exécute dans le système d’exploitation complet.  

> [!IMPORTANT]  
> Le préapprovisionnement de BitLocker nécessite au moins Windows 7. L’ordinateur doit également contenir un module de plateforme sécurisée (TPM) pris en charge et activé.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Disques** et **Préapprovisionner BitLocker** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="apply-bitlocker-to-the-specified-drive"></a>Appliquer BitLocker au lecteur spécifié
Spécifiez le lecteur pour lequel vous souhaitez activer BitLocker. BitLocker chiffre seulement l'espace utilisé sur le lecteur.  

#### <a name="use-full-disk-encryption"></a>Utiliser le chiffrement de lecteur complet
<!--SCCMDocs-pr issue 2671-->
Par défaut, cette étape chiffre uniquement l’espace utilisé sur le lecteur. Ce comportement par défaut est recommandé, car il est plus rapide et plus efficace. À compter de la version 1806, si votre organisation doit chiffrer l’intégralité du lecteur durant l’installation, activez cette option. Le programme d’installation de Windows attend que le lecteur entier soit chiffré, ce qui prend beaucoup de temps, en particulier sur les grands lecteurs. 

#### <a name="skip-this-step-for-computers-that-do-not-have-a-tpm-or-when-tpm-is-not-enabled"></a>Ignorer cette étape pour les ordinateurs n'ayant pas un module de plateforme sécurisée ou lorsque celui-ci n'est pas activé
Sélectionnez cette option pour ignorer le chiffrement de lecteur sur un ordinateur qui ne contient pas un module de plateforme sécurisée pris en charge ou activé. Par exemple, utilisez cette option quand vous déployez un système d’exploitation sur une machine virtuelle.  



##  <a name="BKMK_ReleaseStateStore"></a> Libérer le magasin d’état  

Utilisez cette étape pour notifier au point de migration d’état que l’action de capture ou de restauration est terminée. Utilisez cette étape en combinaison avec les étapes **Demander le magasin d’état**, **Capturer l’état utilisateur** et **Restaurer l’état utilisateur**. Vous utilisez ces étapes pour migrer des données d’état utilisateur en utilisant un point de migration d’état et l’outil USMT.  

Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state).  

Si vous utilisez l’étape **Demander le magasin d’état** pour demander l’accès à un point de migration de l’état pour *capturer* l’état utilisateur, cette étape informe le point de migration d’état que le processus de capture est terminé. Le point de migration d’état marque ensuite les données d’état utilisateur comme étant disponibles pour la restauration. Le point de migration d’état définit les autorisations de contrôle d’accès pour les données d’état utilisateur de façon que seul l’ordinateur de restauration y ait accès en lecture seule.  

Si vous utilisez l’étape **Demander le magasin d’état** pour demander l’accès à un point de migration d’état pour *restaurer* l’état utilisateur, cette étape informe le point de migration d’état que le processus de restauration est terminé. Le point de migration d’état active ensuite ses paramètres de rétention des données tels qu’ils ont été configurés.  
> [!IMPORTANT]  
> Définissez l’option **Continuer en cas d’erreur** pour toutes les étapes entre les étapes **Demander le magasin d’état** et **Libérer le magasin d’état**. Chaque étape **Demander le magasin d’état** doit avoir une étape **Libérer le magasin d’état** correspondante.  

Cette étape s’exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **État utilisateur** et **Libérer le magasin d’état** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Cette étape ne nécessite aucun paramètre sous l’onglet **Propriétés**.



## <a name="BKMK_RequestStateStore"></a> Demander le magasin d’état  

Utilisez cette étape pour demander l’accès à un point de migration d’état pendant la capture ou la restauration de l’état.  

Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state).  

Utilisez cette étape en combinaison avec les étapes **Libérer le magasin d’état**, **Capturer l’état utilisateur** et **Restaurer l’état utilisateur**. Vous utilisez ces étapes pour migrer l’état de l’ordinateur en utilisant un point de migration d’état et l’outil USMT.  

> [!NOTE]  
> Lors de la création d’un point de migration d’état, le stockage de l’état de l’utilisateur n’est pas disponible pendant jusqu’à une heure. Pour accélérer ce processus, ajustez les paramètres de propriété sur le point de migration d’état afin de déclencher une mise à jour du fichier de contrôle du site.  

Cette étape s’exécute dans le système d’exploitation complet et dans Windows PE pour l’outil de migration utilisateur hors connexion.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDStateFallbackToNAA](/sccm/osd/understand/task-sequence-variables#OSDStateFallbackToNAA)  
- [OSDStateSMPRetryCount](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryCount)  
- [OSDStateSMPRetryTime](/sccm/osd/understand/task-sequence-variables#OSDStateSMPRetryTime)  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **État utilisateur** et **Demander le magasin d’état** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="capture-state-from-the-computer"></a>Capturer l'état à partir de l'ordinateur
Recherche un point de migration d’état qui répond à la configuration minimale requise, telle qu’elle est configurée dans les paramètres du point de migration état. Par exemple, **Nombre maximum de clients** et **Quantité minimale d’espace disque libre**. Cette option ne garantit pas qu’un espace suffisant est disponible au moment de la migration d’état. Cette option demande l’accès à un point de migration d’état afin de capturer l’état et les paramètres utilisateur sur un ordinateur.  

Si le site Configuration Manager a plusieurs points de migration d’état actifs, cette étape recherche un point de migration d’état avec l’espace disque disponible. La séquence de tâches interroge le point de gestion pour obtenir une liste de points de migration d’état, puis elle évalue chacun d’eux jusqu’à en trouver un qui répond aux exigences minimales.  

#### <a name="restore-state-from-another-computer"></a>Restaurer l'état à partir d'un autre ordinateur
Demande l’accès à un point de migration d’état pour restaurer un état et des paramètres utilisateur précédemment capturés sur un ordinateur de destination.  

S’il existe plusieurs points de migration d’état, cette étape recherche le point de migration d’état qui a l’état pour l’ordinateur de destination.  

#### <a name="number-of-retries"></a>Nombre de tentatives
Nombre de fois que cette étape tente de trouver un point de migration d’état approprié avant d’échouer.  

#### <a name="retry-delay-in-seconds"></a>Délai de nouvelle tentative (en secondes)
Durée en secondes pendant laquelle l'étape de séquence de tâches attend entre chaque tentative.  

#### <a name="if-computer-account-fails-to-connect-to-a-state-store-use-the-network-access-account"></a>Si le compte d’ordinateur ne parvient pas à se connecter au magasin d’état, utiliser le compte d’accès réseau
Si la séquence de tâches ne peut pas accéder au point de migration d’état en utilisant le compte d’ordinateur, elle utilise les informations d’identification du compte d’accès réseau pour se connecter. Cette option est moins sécurisée, car d’autres ordinateurs peuvent utiliser le compte d’accès réseau pour accéder à l’état stocké. Cette option peut être nécessaire si l’ordinateur de destination n’est pas joint à un domaine.  



##  <a name="BKMK_RestartComputer"></a> Redémarrer l’ordinateur  

Utilisez cette étape pour redémarrer l’ordinateur qui exécute la séquence de tâches. Après avoir redémarré, l’ordinateur passe automatiquement à l’étape suivante de la séquence de tâches.  

Cette étape peut s’exécuter dans le système d’exploitation complet ou Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [SMSRebootMessage](/sccm/osd/understand/task-sequence-variables#SMSRebootMessage)  
- [SMSRebootTimeout](/sccm/osd/understand/task-sequence-variables#SMSRebootTimeout)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Redémarrer l’ordinateur** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="the-boot-image-assigned-to-this-task-sequence"></a>L'image de démarrage attribuée à cette séquence de tâches
Sélectionnez cette option pour que l’ordinateur de destination utilise l’image de démarrage qui est affectée à la séquence de tâches. La séquence de tâches utilise l’image de démarrage pour exécuter les étapes suivantes dans Windows PE.  

#### <a name="the-currently-installed-default-operating-system"></a>Le système d'exploitation par défaut installé actuellement
Sélectionnez cette option pour que l'ordinateur de destination redémarre sous le système d'exploitation installé.  

#### <a name="notify-the-user-before-restarting"></a>Notifier l'utilisateur avant de redémarrer
Sélectionnez cette option pour afficher une notification à l’utilisateur avant que l’ordinateur de destination redémarre. L’étape sélectionne cette option par défaut.  

#### <a name="notification-message"></a>Message de notification
Entrez un message de notification à afficher à l’utilisateur avant le redémarrage de l’ordinateur de destination.  

#### <a name="message-display-time-out"></a>Délai d'affichage du message
Spécifiez le délai en secondes avant que l’ordinateur de destination redémarre. La valeur par défaut est de 60 secondes.  



##  <a name="BKMK_RestoreUserState"></a> Restaurer l’état utilisateur  

Utilisez cette étape pour lancer l’outil USMT pour restaurer l’état et les paramètres utilisateur sur l’ordinateur de destination. Vous utilisez cette étape en combinaison avec l’étape **Capturer l’état utilisateur**.  

Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](/sccm/osd/get-started/manage-user-state).  

Utilisez cette étape avec les étapes **Demander le magasin d’état** et **Libérer le magasin d’état** pour enregistrer ou restaurer les paramètres d’état avec un point de migration d’état. Cette option déchiffre toujours le magasin d’état USMT au moyen d’une clé de chiffrement générée et gérée par Configuration Manager.  

L’étape **Restaurer l’état utilisateur** permet de contrôler un sous-ensemble limité des options USMT les plus couramment utilisées. Spécifiez d’autres options de ligne de commande avec la variable **OSDMigrateAdditionalRestoreOptions**.  

> [!IMPORTANT]  
> Si vous utilisez cette étape dans un but non lié à un scénario de déploiement de système d’exploitation, ajoutez l’étape [Restaurer l’état utilisateur](#BKMK_RestartComputer) immédiatement après l’étape **Restaurer l’état utilisateur**.  

Cette étape s’exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [_OSDMigrateUsmtRestorePackageID](/sccm/osd/understand/task-sequence-variables#OSDMigrateUsmtRestorePackageID)  
- [OSDMigrateAdditionalRestoreOptions](/sccm/osd/understand/task-sequence-variables#OSDMigrateAdditionalRestoreOptions)  
- [OSDMigrateContinueOnRestore](/sccm/osd/understand/task-sequence-variables#OSDMigrateContinueOnRestore)  
- [OSDMigrateEnableVerboseLogging](/sccm/osd/understand/task-sequence-variables#OSDMigrateEnableVerboseLogging)  
- [OSDMigrateLocalAccounts](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccounts)  
- [OSDMigrateLocalAccountPassword](/sccm/osd/understand/task-sequence-variables#OSDMigrateLocalAccountPassword)  
- [OSDStateStorePath](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **État utilisateur** et **Restaurer l’état utilisateur** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="user-state-migration-tool-package"></a>Package de l'outil de migration de l'état utilisateur
Spécifiez le package qui contient la version de l’outil USMT que cette étape doit utiliser. Ce package ne requiert pas de programme. Quand l’étape s’exécute, la séquence de tâches utilise la version de l’outil USMT présente dans le package spécifié. Spécifiez un package qui contient la version 32 bits ou 64 bits de l’outil USMT. L’architecture de l’outil USMT varie selon l’architecture du système d’exploitation dont la séquence de tâches restaure l’état. 

#### <a name="restore-all-captured-user-profiles-with-standard-options"></a>Restaurer tous les profils utilisateur capturés présentant des options standard
Restaure les profils utilisateur capturés qui présentent des options standard. Pour personnaliser les options restaurées par l’outil USMT, sélectionnez **Personnaliser la façon dont les profils utilisateur sont capturés**.  

#### <a name="customize-how-user-profiles-are-restored"></a>Personnaliser la restauration des profils utilisateur
Permet de personnaliser les fichiers à restaurer sur l'ordinateur de destination. Sélectionnez **Fichiers** afin de spécifier les fichiers de configuration du package USMT à utiliser pour restaurer les profils utilisateur. Pour ajouter un fichier de configuration, entrez son nom dans la zone **Nom de fichier**, puis sélectionnez **Ajouter**. Le volet Fichiers répertorie les fichiers de configuration utilisés par l’outil USMT. Le fichier .xml que vous spécifiez définit le fichier utilisateur restauré par l’outil USMT.  

#### <a name="restore-local-computer-user-profiles"></a>Restaurer les profils utilisateur de l'ordinateur local
Restaure les profils utilisateur de l'ordinateur local. Ces profils ne sont pas pour les utilisateurs de domaine. Attribuez de nouveaux mots de passe aux comptes d’utilisateur locaux. L’outil USMT ne peut pas migrer les mots de passe d’origine. Entrez le nouveau mot de passe dans le champ **Mot de passe** , puis confirmez le mot de passe dans le champ **Confirmer le mot de passe** .  

#### <a name="continue-if-some-files-cannot-be-restored"></a>Continuer si certains fichiers ne peuvent pas être restaurés
Continue la restauration de l’état et des paramètres utilisateur même si l’outil USMT ne peut pas restaurer certains fichiers. L’étape active cette option par défaut. Si vous désactivez cette option et que l’outil USMT rencontre des erreurs lors de la restauration de fichiers, cette étape échoue immédiatement. L’outil USMT ne restaure pas tous les fichiers.   

#### <a name="enable-verbose-logging"></a>Activer la journalisation documentée
Activez cette option pour générer des informations de fichiers journaux plus détaillées. Lors de la restauration de l’état, la séquence de tâches génère par défaut **Loadstate.log** dans le dossier de journalisation de la séquence de tâches, `%WinDir%\ccm\logs`.  



## <a name="BKMK_RunCommandLine"></a> Exécuter la ligne de commande  

Utilisez cette étape pour exécuter la ligne de commande spécifiée.  

Cette étape peut s’exécuter dans le système d’exploitation complet ou Windows PE.   

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [OSDDoNotLogCommand](/sccm/osd/understand/task-sequence-variables#OSDDoNotLogCommand) (à partir de la version 1806)<!--1358493-->  
- [SMSTSDisableWow64Redirection](/sccm/osd/understand/task-sequence-variables#SMSTSDisableWow64Redirection)  
- [SMSTSRunCommandLineUserName](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLineUserName)  
- [SMSTSRunCommandLinePassword](/sccm/osd/understand/task-sequence-variables#SMSTSRunCommandLinePassword)  
- [WorkingDirectory](/sccm/osd/understand/task-sequence-variables#WorkingDirectory)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Exécuter la ligne de commande** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="command-line"></a>Ligne de commande
Spécifie la ligne de commande que la séquence de tâches exécute. Ce champ doit obligatoirement être renseigné. Intégrez les extensions de nom de fichier, par exemple, .vbs et .exe. Intégrez tous les fichiers de paramètres et les options de ligne de commande requis.  

Si vous ne spécifiez pas l’extension de nom de fichier, Configuration Manager essaie les extensions .com, .exe et .bat. Si le nom de fichier a une extension, mais qu’il ne s’agit pas d’un type exécutable, Configuration Manager essaie d’appliquer une association locale. Par exemple, si la ligne de commande est readme.gif, Configuration Manager démarre l’application spécifiée sur l’ordinateur de destination pour ouvrir les fichiers .gif.  

Exemples :  

`setup.exe /a`  

`cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
> Pour que l’exécution se fasse correctement, faites précéder les actions de la ligne de commande de la commande **cmd.exe /c**. Des commandes de redirection de sortie, d’utilisation de canaux et de copie sont des exemples de ces actions.  

#### <a name="disable-64-bit-file-system-redirection"></a>Désactiver la redirection du système de fichiers 64 bits
Par défaut, les systèmes d’exploitation 64 bits utilisent le redirecteur du système de fichiers WOW64 pour exécuter des lignes de commande. Ce comportement est destiné à trouver les versions 32 bits appropriées des exécutables et des bibliothèques du système d’exploitation. Sélectionnez cette option pour désactiver l’utilisation du redirecteur du système de fichiers WOW64. Windows exécute la commande en utilisant les versions 64 bits natives des exécutables et des bibliothèques du système d’exploitation. Cette option est sans effet lors de l’exécution sur un système d’exploitation 32 bits.  

#### <a name="start-in"></a>Démarrer dans
Spécifie le dossier exécutable pour le programme, comprenant jusqu'à 127 caractères. Ce dossier peut être un chemin d'accès absolu sur l'ordinateur de destination ou un chemin d'accès relatif au dossier du point de distribution qui contient le package. Ce champ est facultatif.  

Exemples :  

`c:\officexp`  

`i386`  

> [!NOTE]  
> Le bouton **Parcourir** permet de parcourir les fichiers et les dossiers de l’ordinateur local. Tout ce que vous sélectionnez doit également exister sur l’ordinateur de destination. Le contenu de la sélection doit exister dans le même emplacement et avec les mêmes noms de fichier et de dossier.  

#### <a name="package"></a>Package
Quand, sur la ligne de commande, vous spécifiez des fichiers ou des programmes qui ne sont pas déjà présents sur l’ordinateur de destination, sélectionnez cette option pour spécifier le package Configuration Manager qui contient les fichiers nécessaires. Le package ne requiert pas de programme. Cette option n'est pas nécessaire si le fichier spécifié existe sur l'ordinateur de destination.  

#### <a name="time-out"></a>Délai
Spécifie une valeur qui représente la durée pendant laquelle Configuration Manager autorise la ligne de commande à s’exécuter. Cette valeur est comprise entre une minute et 999 minutes. La valeur par défaut est 15 minutes. Cette option est désactivée par défaut.  

> [!IMPORTANT]  
> Si vous entrez une valeur qui ne donne pas suffisamment de temps à la commande spécifiée pour se terminer correctement, cette étape échoue. La séquence de tâches toute entière peut échouer en fonction des conditions d’étape ou de groupe. Si le délai d’expiration est atteint, Configuration Manager met fin au processus de la ligne de commande.  

#### <a name="run-this-step-as-the-following-account"></a>Exécuter cette étape en tant que compte suivant
Spécifie que la ligne de commande est exécutée en tant que compte d'utilisateur Windows et non en tant que compte Système local.  

> [!NOTE]  
> Pour exécuter des scripts simples ou des commandes avec un autre compte après avoir installé le système d’exploitation, vous devez d’abord ajouter le compte à l’ordinateur. En outre, vous devrez peut-être restaurer les profils utilisateur Windows pour exécuter des programmes plus complexes, comme un programme d’installation de Windows.  

#### <a name="account"></a>Compte
Spécifie le compte d’utilisateur Windows que cette étape utilise pour exécuter la ligne de commande. La ligne de commande s’exécute avec les autorisations du compte spécifié. Sélectionnez **Définir** pour spécifier le compte de domaine ou d’utilisateur local. Pour plus d'informations sur le compte Exécuter en tant que de la séquence de tâches, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).

> [!IMPORTANT]  
> Si cette étape spécifie un compte d’utilisateur et s’exécute dans Windows PE, l’action échoue. Vous ne pouvez pas joindre Windows PE à un domaine. Le fichier **smsts.log** enregistre cet échec.  



##  <a name="BKMK_RunPowerShellScript"></a> Exécuter le script PowerShell  

Utilisez cette étape pour exécuter le script Windows PowerShell spécifié.  

Cette étape peut s’exécuter dans le système d’exploitation complet ou Windows PE. Pour exécuter cette étape dans Windows PE, activez PowerShell dans l'image de démarrage. Activez le composant WinPE-PowerShell à partir de l'onglet **Composants facultatifs** dans les propriétés de l'image de démarrage. Pour plus d’informations sur la modification d’une image de démarrage, consultez [Gérer les images de démarrage](/sccm/osd/get-started/manage-boot-images).  

> [!NOTE]  
> PowerShell n'est pas activé par défaut sur les systèmes d'exploitation Windows Embedded.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Exécuter le script PowerShell** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="package"></a>Package
Indique le package Configuration Manager qui contient le script PowerShell. Un package peut contenir plusieurs scripts PowerShell.  

#### <a name="script-name"></a>Nom du script
Spécifie le nom du script PowerShell à exécuter. Ce champ doit obligatoirement être renseigné.  

#### <a name="parameters"></a>Paramètres
Spécifie les paramètres passés au script PowerShell. Ces paramètres sont les mêmes que les paramètres du script PowerShell sur la ligne de commande.  

> [!IMPORTANT]  
> Spécifiez les paramètres consommés par le script, et non pour la ligne de commande Windows PowerShell.  
> 
> L'exemple suivant contient des paramètres valides :  
> 
> `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
> 
> L'exemple suivant contient des paramètres non valides. Les deux premiers éléments sont des paramètres de ligne de commande Windows PowerShell (**-NoLogo** et **-ExecutionPolicy Unrestricted**). Le script n’utilise pas ces paramètres.  
> 
> `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

#### <a name="powershell-execution-policy"></a>Stratégie d'exécution de PowerShell
Détermine les scripts PowerShell (le cas échéant) que vous autorisez à s’exécuter sur l’ordinateur. Choisissez l'une des stratégies d'exécution suivantes :  

- **AllSigned** : exécuter seulement les scripts signés par un éditeur approuvé  

- **Non défini** : ne pas définir de stratégie d’exécution  

- **Bypass** : charger tous les fichiers de configuration et exécuter tous les scripts Si vous téléchargez un script non signé à partir d’Internet, Windows PowerShell ne demande pas d’autorisation avant d’exécuter le script.  


> [!IMPORTANT]  
> PowerShell 1.0 ne prend pas en charge les stratégies d'exécution Non défini et Ignorer.  



## <a name="child-task-sequence"></a> Exécuter une séquence de tâches

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Activez cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

À compter de Configuration Manager version 1710, vous pouvez ajouter une nouvelle étape qui exécute une autre séquence de tâches. Cette étape crée une relation parent-enfant entre les séquences de tâches. Avec les séquences de tâches enfants, vous pouvez créer des séquences de tâches plus modulaires et réutilisables.

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Exécuter une séquence de tâches** pour ajouter cette étape. 


### <a name="specifications-and-limitations"></a>Spécifications et limitations

Lorsque vous ajoutez une séquence de tâches enfant à une séquence de tâches, considérez les points suivants :  

- Les séquences de tâches parent et enfant sont en fait combinées en une stratégie unique exécutée par le client.  

- L’environnement est global. Si la séquence de tâches parent définit une variable et que la séquence de tâches enfant change cette variable, elle conserve la dernière valeur. Si la séquence de tâches enfant crée une variable, celle-ci est disponible pour le reste de la séquence de tâches parent.  

- Les messages d’état sont envoyés normalement pour une opération de séquence de tâches unique.  

- La séquence de tâches inscrit des entrées dans le fichier **smsts.log** et le nouveau journal écritures indique clairement lorsqu’une séquence de tâches enfant démarre.  

<!--the following points are from SCCMdocs issue #1079--> 
- Il n’est pas possible de sélectionner une séquence de tâches avec une référence d’image de démarrage. Si le déploiement exige une image de démarrage, spécifiez-le sur la séquence de tâches parente.  

- Si une séquence de tâches enfant est désactivée, le déploiement échoue. Il n’est pas possible d’utiliser l’option **Continuer en cas d’erreur** pour contourner cette limitation.  

- Si une séquence de tâches enfant contient des étapes considérés comme *à fort impact*, le Centre logiciel ne le détecte pas et affiche la notification à fort impact. Modifiez les propriétés de la séquence de tâches parente, sous l’onglet Notification à l’utilisateur, pour spécifier **Il s’agit d’une séquence de tâches à fort impact**.  

- Si une référence de package est manquante dans une séquence de tâches enfant, l’affichage de la séquence de tâches parente ne détecte pas cet état. Si vous modifiez la séquence de tâches parente, elle détecte toutes les références manquantes dans les séquences de tâches enfant.  


### <a name="properties"></a>Propriétés

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="select-task-sequence-to-run"></a>Sélectionner la séquence de tâches à exécuter
Sélectionnez **Parcourir** pour choisir la séquence de tâches enfant. La boîte de dialogue **Sélectionner une séquence de tâches** n’affiche pas la séquence de tâches parent.



## <a name="BKMK_SetDynamicVariables"></a> Définir des variables dynamiques  

Utilisez cette étape pour effectuer les actions suivantes :  

1. Collectez des informations à partir de l’ordinateur et son environnement. Puis, définissez les variables de séquence de tâches spécifiées à l’aide des informations.  

2. Évaluez les règles définies. Définissez les variables de séquence de tâches selon les règles qui ont la valeur true.  


La séquence de tâches définit automatiquement les variables de séquence de tâches en lecture seule suivantes :  
- [\_SMSTSMake](/sccm/osd/understand/task-sequence-variables#SMSTSMake)  
- [\_SMSTSModel](/sccm/osd/understand/task-sequence-variables#SMSTSModel)  
- [\_SMSTSMacAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSMacAddresses)  
- [\_SMSTSIPAddresses](/sccm/osd/understand/task-sequence-variables#SMSTSIPAddresses)  
- [\_SMSTSSerialNumber](/sccm/osd/understand/task-sequence-variables#SMSTSSerialNumber)  
- [\_SMSTSAssetTag](/sccm/osd/understand/task-sequence-variables#SMSTSAssetTag)  
- [\_SMSTSUUID](/sccm/osd/understand/task-sequence-variables#SMSTSUUID)  

Cette étape peut s’exécuter dans le système d’exploitation complet ou Windows PE.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Définir des variables dynamiques** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="dynamic-rules-and-variables"></a>Règles dynamiques et variables
Pour définir une variable dynamique à utiliser dans la séquence de tâches, ajoutez une règle. Ensuite, définissez une valeur pour chaque variable spécifiée dans la règle. Ajoutez aussi une ou plusieurs variables sans ajouter une règle. Quand vous ajoutez une règle, choisissez parmi les catégories suivantes :  

- **Ordinateur** : évalue des valeurs d’étiquette d’inventaire matériel, d’UUID, de numéro de série ou d’adresse MAC. Définissez plusieurs valeurs selon vos besoins. Si une des valeurs est true, la règle est évaluée comme étant vraie. Par exemple, la règle suivante est évaluée comme étant vraie si le numéro de série du périphérique est 5892087 et si l’adresse MAC est 22-A4-5A-13-78-26 :  

    `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

- **Emplacement** : évalue les valeurs de la passerelle réseau par défaut  

- **Marque et modèle** : évalue les valeurs de la marque et du modèle d’un ordinateur La marque et le modèle doivent tous deux être évalués comme vrais pour que la règle soit évaluée comme vraie.   

    Spécifiez l’astérisque (`*`) et le point d’interrogation (`?`) en tant que caractères génériques. L’astérisque correspond à plusieurs caractères et le point d’interrogation correspond à un seul caractère. Par exemple, la chaîne `DELL*900?` correspond à `DELL-ABC-9001` et à `DELL9009`.  

- **Variable de séquence de tâches** : ajoute une variable de séquence de tâches, une condition et une valeur à évaluer. La règle est évaluée comme vraie quand la valeur définie pour la variable remplit la condition spécifiée.  

    Spécifiez une ou plusieurs variables à définir pour une règle évaluée comme étant vraie, ou définissez des variables sans utiliser de règle. Sélectionnez une variable existante ou créez une variable personnalisée.  

    - **Variables de séquence de tâches existantes** : sélectionnez une ou plusieurs variables dans une liste des variables de séquence de tâches existantes. Les variables tableau ne peuvent pas être sélectionnées.  

    - **Variables de séquence de tâches personnalisées** : définissez une variable de séquence de tâches personnalisée. Vous pouvez également spécifier une variable de séquence de tâches existante. Ce paramètre utile pour spécifier un tableau de variables existantes, comme **OSDAdapter**, car les tableaux de variables ne figurent pas dans la liste des variables de séquence de tâches existantes.  


Après avoir sélectionné les variables pour une règle, fournissez une valeur pour chaque variable. Lorsque la règle est évaluée comme vraie, la variable est définie à la valeur spécifiée. Pour chaque variable, vous pouvez sélectionner **Valeur secrète** pour masquer la valeur de la variable. Par défaut, certaines variables existantes (telles que la variable **OSDCaptureAccountPassword**) masquent les valeurs.  

> [!IMPORTANT]  
> Configuration Manager supprime les valeurs des variables marquées comme **Valeur secrète** quand vous importez une séquence de tâches avec l’étape **Définir des variables dynamiques**. Entrez à nouveau la valeur de la variable dynamique après avoir importé la séquence de tâches.  



## <a name="BKMK_SetTaskSequenceVariable"></a> Définir la variable de séquence de tâches  

Utilisez cette étape pour définir la valeur d’une variable qui est utilisée avec la séquence de tâches.  

Cette étape peut s’exécuter dans le système d’exploitation complet ou Windows PE. 

Les variables de séquence de tâches sont lues par les actions et en déterminent le comportement. Pour plus d’informations sur les variables de séquence de tâches spécifiques et leur utilisation, consultez les articles suivants :  
- [Comment utiliser les variables de séquence de tâches](/sccm/osd/understand/using-task-sequence-variables)  
- [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Général** et **Définir la variable de séquence de tâches** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="task-sequence-variable"></a>Variable de séquence de tâches
Spécifiez le nom d’une variable intégrée ou d’action de séquence de tâches, ou spécifiez le nom de votre propre variable définie par l’utilisateur.  

#### <a name="do-not-display-this-value"></a>Ne pas afficher cette valeur
<!--1358330-->
À compter de la version 1806, activez cette option pour masquer les données sensibles stockées dans des variables de séquence de tâches. Par exemple, quand vous spécifiez un mot de passe. 

> [!Note]  
> Activez cette option, puis définissez la valeur de la variable de séquence de tâches. Sinon, elle ne sera pas définie comme vous le souhaitez, ce qui peut provoquer des comportements inattendus à l’exécution de la séquence de tâches.<!--SCCMdocs issue #800--> 

#### <a name="value"></a>Valeur  
La séquence de tâches définit la variable sur cette valeur. Définissez cette variable de séquence de tâches sur la valeur d’une autre variable de séquence de tâches avec la syntaxe `%varname%`.  



## <a name="BKMK_SetupWindowsandConfigMgr"></a> Configurer Windows et ConfigMgr  

Utilisez cette étape pour effectuer la transition de Windows PE vers le nouveau système d’exploitation. Cette étape de séquence de tâches est obligatoire dans tout déploiement de système d'exploitation, elle installe le client Configuration Manager dans le nouveau système d’exploitation et prépare la poursuite de l’exécution de la séquence de tâches dans le nouveau système d’exploitation.  

Cette étape est exécutée uniquement sous Windows PE. Elle ne s’exécute dans le système d’exploitation complet.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [SMSClientInstallProperties](/sccm/osd/understand/task-sequence-variables#SMSClientInstallProperties)  

Cette étape remplace les variables de répertoire de sysprep.inf ou unattend.xml, comme `%WINDIR%` et `%ProgramFiles%`, par le répertoire d’installation de Windows PE, `X:\Windows`. La séquence de tâches ignore les variables spécifiées avec ces variables d’environnement.  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Configurer Windows et ConfigMgr** pour ajouter cette étape. 


### <a name="step-actions"></a>Actions d’étape

Cette étape effectue les actions suivantes :  

#### <a name="preliminaries-windows-pe"></a>Préliminaires : Windows PE  

1. Remplacez les variables de séquence de tâches dans le fichier unattend.xml.  

2. Téléchargez le package qui contient le client Configuration Manager. Ajoutez le package à l’image déployée.  

#### <a name="set-up-windows"></a>Configuration de Windows  

- Installation à base d’image  

    1. Désactivez le client Configuration Manager dans l’image, s’il existe. En d’autres termes, désactivez le démarrage automatique pour le service client Configuration Manager.  

    2. Mettez à jour le Registre dans l’image déployée pour démarrer le système d’exploitation déployé avec la même lettre de lecteur que celle de l’ordinateur de référence.  

    3. Redémarrez sur le système d’exploitation déployé.  

    4. La mini-installation de Windows s’exécute en utilisant le fichier de réponses sysprep.inf ou unattend.xml spécifié précédemment et dont toutes les interactions avec l’utilisateur final sont supprimées. Si vous utilisez l’étape **Appliquer les paramètres réseau** pour la jonction à un domaine, ces informations se trouvent dans le fichier de réponses. La mini-installation de Windows joint l’ordinateur au domaine.  

- Installation avec Setup.exe. Exécute le fichier Setup.exe qui suit le processus d’installation de Windows classique :  

    1. Copiez le package de mise à niveau du système d’exploitation spécifié dans l’étape **Appliquer le système d’exploitation** sur le disque dur.  

    2. Redémarrez sur le système d’exploitation nouvellement déployé.  

    3. La mini-installation de Windows s’exécute en utilisant le fichier de réponses sysprep.inf ou unattend.xml spécifié précédemment et dont tous les paramètres d’interface utilisateur sont supprimés. Si vous utilisez l’étape **Appliquer les paramètres réseau** pour la jonction à un domaine, ces informations se trouvent dans le fichier de réponses. La mini-installation de Windows joint l’ordinateur au domaine.  

#### <a name="set-up-the-configuration-manager-client"></a>Configurer le client Configuration Manager  

1. Une fois la mini-installation de Windows terminée, la séquence de tâches reprend à l’aide de setupcomplete.cmd.  

2. Activez ou désactivez le compte d’administrateur local en fonction de l’option sélectionnée dans l’étape **Appliquer les paramètres Windows**.  

3. Installez le client Configuration Manager en utilisant le package précédemment téléchargé et les propriétés d’installation spécifiées dans cette étape. Le client est installé en « mode de provisionnement ». Ce mode empêche le client de traiter les demandes de nouvelles stratégies avant la fin de la séquence de tâches.  

4. Attendez que le client soit entièrement opérationnel.  

#### <a name="the-step-completes"></a>L’étape est terminée
La séquence de tâches continue en exécutant l’étape suivante.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="client-package"></a>Package client
Sélectionnez **Parcourir**, puis choisissez le package d’installation du client Configuration Manager à utiliser avec cette étape.  

#### <a name="use-pre-production-client-package-when-available"></a>Utiliser le package client de préproduction quand il est disponible
Si un package client de préproduction est disponible et que l’ordinateur est membre du regroupement pilote, la séquence de tâches utilise ce package à la place du package client de production. Le client de préproduction est une version plus récente à tester dans l’environnement de production. Sélectionnez **Parcourir**, puis choisissez le package d’installation du client de préproduction à utiliser avec cette étape.  

#### <a name="installation-properties"></a>Propriétés d'installation
L'attribution de site et la configuration par défaut sont automatiquement spécifiées par l'étape de la séquence de tâches. Ce champ permet de spécifier les propriétés d'installation supplémentaires à utiliser lorsque vous installez le client. Pour entrer plusieurs propriétés d'installation, séparez-les par un espace.  

Spécifiez des options de ligne de commande à utiliser lors de l'installation du client. Par exemple, entrez `/skipprereq: silverlight.exe` pour informer CCMSetup.exe de ne pas installer le composant requis Microsoft Silverlight. Pour plus d’informations sur les options de ligne de commande disponibles pour CCMSetup.exe, consultez [À propos des propriétés d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).  


### <a name="options"></a>Options

> [!NOTE]  
> N’activez pas **Continuer en cas d’erreur** sous l’onglet **Options**. Si une erreur se produit au cours de cette étape, la séquence de tâches échoue selon que vous activez ou non ce paramètre.  



## <a name="BKMK_UpgradeOS"></a> Mettre à niveau le système d’exploitation  

> [!TIP]  
> À compter de Windows 10 version 1709, le média inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour l’utilisation d’un package de mise à niveau du système d’exploitation ou d’une image de système d’exploitation, veillez à sélectionner une [édition prise en charge](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).  

Utilisez cette étape pour mettre à niveau une version antérieure de Windows vers une version plus récente de Windows 10.  

Cette étape de séquence de tâches s'exécute uniquement dans le système d’exploitation complet. Elle ne s'exécute pas dans Windows PE.  

Utilisez les variables de séquence de tâches suivantes avec cette étape :  
- [_SMSTSOSUpgradeActionReturnCode](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode)  
- [OSDSetupAdditionalUpgradeOptions](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions)  

Dans l’Éditeur de séquence de tâches, sélectionnez successivement **Ajouter**, **Images** et **Mettre à niveau le système d’exploitation** pour ajouter cette étape. 


### <a name="properties"></a>Propriétés  

Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

#### <a name="upgrade-package"></a>Package de mise à niveau
Sélectionnez cette option pour spécifier le package de mise à niveau de système d’exploitation Windows 10 à utiliser pour la mise à niveau.  

#### <a name="source-path"></a>Chemin source
Spécifie un chemin local ou réseau au média de Windows 10 utilisé par l’installation de Windows. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows `/InstallFrom`. 

Vous pouvez également spécifier une variable, comme `%MyContentPath%` ou `%DPC01%`. Quand vous utilisez une variable pour le chemin source, sa valeur doit être spécifiée plus tôt dans la séquence de tâches. Par exemple, utilisez l’étape [Télécharger le contenu du package](#BKMK_DownloadPackageContent) afin de spécifier une variable pour l’emplacement du package de mise à niveau du système d’exploitation. Ensuite, utilisez cette variable pour le chemin source de cette étape.  

#### <a name="edition"></a>Édition
Spécifiez l’édition au sein du support du système d’exploitation à utiliser pour la mise à niveau.  

#### <a name="product-key"></a>Clé du produit
Spécifiez la clé de produit à appliquer au processus de mise à niveau.  

#### <a name="provide-the-following-driver-content-to-windows-setup-during-upgrade"></a>Fournir le contenu du pilote suivant à l’installation de Windows pendant la mise à niveau
Ajouter des pilotes à l’ordinateur de destination lors du processus de mise à niveau. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows `/InstallDriver`. Les pilotes doivent être compatibles avec Windows 10. Spécifiez l’une des options suivantes :  

- **Package de pilotes** : sélectionnez **Parcourir** et choisissez un package de pilotes existant dans la liste.  

- **Contenu intermédiaire** : sélectionnez cette option pour spécifier l’emplacement du package de pilotes. Vous pouvez spécifier un dossier local, un chemin réseau ou une variable de séquence de tâches. Quand vous utilisez une variable pour le chemin source, sa valeur doit être spécifiée plus tôt dans la séquence de tâches. Par exemple, en utilisant l’étape [Télécharger le contenu du package](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent).  

#### <a name="time-out-minutes"></a>Délai d’expiration (minutes)
Spécifiez le nombre de minutes avant que Configuration Manager considère que cette étape a échoué. Cette option est utile si l’installation de Windows arrête le traitement mais ne se termine pas.  

#### <a name="perform-windows-setup-compatibility-scan-without-starting-upgrade"></a>Effectuer une analyse de compatibilité d’installation de Windows sans démarrer la mise à niveau
Effectuer l’analyse de compatibilité de l’installation de Windows sans démarrer le processus de mise à niveau. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows `/Compat ScanOnly`. Déployez le package de mise à niveau du système d’exploitation entier avec cette option. 

<!--SCCMDocs-pr issue 2812-->
À compter de la version 1806, lorsque vous activez cette option, cette étape ne place pas le client Configuration Manager en mode de provisionnement. L’installation de Windows s’exécute en mode silencieux en arrière-plan, et le client continue à fonctionner normalement. 

Le programme d’installation renvoie un code de sortie suite à l’analyse. Le tableau suivant indique certains des codes de sortie les plus courants :  

|Code de sortie|Détails|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Aucun problème de compatibilité (« réussite »).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Problèmes de compatibilité pouvant donner lieu à une action.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Le choix de migration sélectionné n’est pas disponible. Par exemple, une mise à niveau depuis Entreprise vers Professionnel.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Non éligible pour Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Espace disque disponible insuffisant.|  

Pour plus d’informations sur ce paramètre, consultez [Options de ligne de commande du programme d’installation de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#6).  

#### <a name="ignore-any-dismissible-compatibility-messages"></a>Ignorer les messages de compatibilité révocables
Spécifie que le programme d’installation a terminé l’installation, en ignorant tous les messages de compatibilité révocables. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows `/Compat IgnoreWarning`.  

#### <a name="dynamically-update-windows-setup-with-windows-update"></a>Mettre à jour dynamiquement l’installation de Windows avec Windows Update
Permet au programme d’installation d’effectuer des opérations de mise à jour dynamiques, comme rechercher, télécharger et installer des mises à jour. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows `/DynamicUpdate`. Ce paramètre n’est pas compatible avec les mises à jour logicielles de Configuration Manager. Activez cette option quand vous gérez des mises à jour avec WSUS (Windows Server Update Services) autonome ou avec Windows Update pour Entreprise.  

#### <a name="override-policy-and-use-default-microsoft-update"></a>Remplacer la stratégie et utiliser Microsoft Update par défaut
Remplacez temporairement la stratégie locale en temps réel pour exécuter des opérations de mise à jour dynamique. L’ordinateur obtient les mises à jour à partir de Windows Update.
