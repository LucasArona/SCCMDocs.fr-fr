---
title: Variables d’action de séquence de tâches
titleSuffix: Configuration Manager
description: Les variables d’action de séquence, telles que les variables de paramètres réseau, permettent de spécifier les paramètres de configuration d’une seule étape de séquence de tâches Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e2269031-0977-4f01-a274-420e00630575
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f66203e335524fa922ec1b6ab3dd4dc5fb917b0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352581"
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>Variables d’action de séquence de tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les variables d’action de séquence de tâches spécifient les paramètres de configuration utilisés par une seule étape de séquence de tâches Configuration Manager. Par défaut, l’étape de séquence de tâches initialise ses paramètres avant son exécution. Ces paramètres sont disponibles uniquement pendant l’exécution de l’étape de séquence de tâches associée. En d’autres termes, la séquence de tâches ajoute la valeur de variable d’action à l’environnement de séquence de tâches avant l’exécution de l’étape de séquence de tâches. La séquence de tâches supprime la valeur de l’environnement une fois l’étape exécutée.  

## <a name="action-variable-example"></a>Exemple de variable d'action  
 Par exemple, vous pouvez spécifier un répertoire de départ pour une action de ligne de commande à l'aide de l'étape de séquence de tâches **Exécuter la ligne de commande** . Cette étape comprend une propriété **Démarrer dans** dont la valeur par défaut est stockée dans le même environnement de la séquence de tâches que la variable **WorkingDirectory** . La variable d'environnement **WorkingDirectory** est initialisée avant l'exécution de l'action de séquence de tâches **Exécuter la ligne de commande** . Lors de l'étape **Exécuter la ligne de commande** , la valeur **WorkingDirectory** est accessible via la propriété **Démarrer dans** . Une fois l’étape terminée, la séquence de tâches supprime la valeur de la variable **WorkingDirectory** de l’environnement. Si la séquence contient une autre étape **Exécuter la ligne de commande**, elle initialise une nouvelle variable **WorkingDirectory** et lui affecte la valeur de départ de l’étape actuelle.  

 La valeur *par défaut* d’une variable d’action de séquence de tâches est présente quand l’étape de séquence de tâches s’exécute. Si vous définissez une *nouvelle* valeur, elle est accessible à plusieurs étapes dans la séquence de tâches. Si vous faites appel à des méthodes de création de variables de séquence de tâches pour remplacer une valeur de variable intégrée, la nouvelle valeur demeure dans l'environnement et remplace la valeur par défaut des autres étapes de la séquence de tâches. Par exemple, si vous ajoutez une étape **Définir la variable de séquence de tâches** comme première étape de la séquence de tâches, qui affecte la valeur **C:\\** à la variable **WorkingDirectory**, toute étape **Exécuter la ligne de commande** dans la séquence de tâches utilise la nouvelle valeur de répertoire de départ.  

## <a name="action-variables-for-task-sequence-actions"></a>Variables d'action pour des actions de séquence de tâches  
 Les variables de séquence de tâches Configuration Manager sont regroupées en fonction de l’action de séquence de tâches à laquelle est elles sont associées. Utilisez les liens suivants pour collecter des informations sur les variables d'action associées à une action spécifique. Les variables de séquence de tâches régissent le fonctionnement de l’action de séquence de tâches. L’action de séquence de tâches lit et utilise les variables que vous marquez en tant que variables d’entrée. Vous pouvez également utiliser l’étape [Définir la variable de séquence de tâches](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) ou l’objet COM TSEnvironment pour définir les variables au moment de l’exécution. Seule l’action de séquence de tâches marque des variables en tant que variables de sortie. Les actions qui se produisent ultérieurement dans la séquence de tâches lisent ces variables de sortie.  

> [!NOTE]  
>  Toutes les actions de séquence de tâches ne sont pas associées à un ensemble de variables de séquence de tâches. Par exemple, bien qu'il existe des variables associées à l'action Activer BitLocker, il n'existe aucune variable associée à l'action Désactiver BitLocker.  



###  <a name="BKMK_ApplyDataImage"></a> Appliquer l’image de données   
 Pour plus d’informations, consultez [Appliquer l’image de données](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (entrée)|Spécifie la valeur d'index de l'image qui est appliquée à l'ordinateur de destination.|  
|OSDWipeDestinationPartition<br /><br /> (entrée)|Spécifie s'il faut supprimer les fichiers situés sur la partition de destination.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Appliquer le package de pilotes   
Pour plus d’informations, consultez [Appliquer le package de pilotes](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (entrée)|Spécifie l'ID de contenu du pilote de périphérique de stockage de masse à installer à partir du package de pilotes. Si vous ne spécifiez pas cette variable, aucun pilote de stockage de masse n’est installé.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (entrée)|Spécifie le fichier INF du pilote de stockage de masse à installer.<br /><br /> <br /><br /> Cette variable de séquence de tâches est requise si OSDApplyDriverBootCriticalContentUniqueID est défini.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (entrée)|Spécifie si un pilote de dispositif de stockage de masse est installé. Cette variable doit être de type **scsi**.<br /><br /> Cette variable de séquence de tâches est requise si OSDApplyDriverBootCriticalContentUniqueID est défini.|  
|OSDApplyDriverBootCriticalID<br /><br /> (entrée)|Spécifie l'ID critique de démarrage du pilote de périphérique de stockage de masse à installer. Cet ID apparaît dans la section **scsi** du fichier txtsetup.oem du pilote de dispositif.<br /><br /> Cette variable de séquence de tâches est requise si OSDApplyDriverBootCriticalContentUniqueID est défini.|  
|OSDAllowUnsignedDriver<br /><br /> (entrée)|Spécifie s'il faut configurer Windows pour autoriser l'installation de pilotes de périphérique non signés. Cette variable de séquence de tâches n'est pas utilisée au cours du déploiement du système d'exploitation Windows Vista et version ultérieure.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Appliquer les paramètres réseau   
 Pour plus d’informations, consultez [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (entrée)|Cette variable de séquence de tâches est une variable de matrice. Chaque élément de la matrice représente les paramètres d'une carte réseau de l'ordinateur. Accédez aux paramètres de chaque carte en combinant le nom de la variable de matrice avec l’index de carte réseau de base zéro et le nom de propriété.<br /><br />Si cette étape configure plusieurs cartes réseau, elle définit les propriétés de la deuxième carte réseau à l’aide de l’index dans le nom de variable. Par exemple, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList et OSDAdapter1EnableWINS.<br /><br />Par exemple, utilisez les noms de variables suivants afin de définir les propriétés de la première carte réseau pour cette étape de séquence de tâches :<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** : **true** active le protocole DHCP (Dynamic Host Configuration Protocol) de la carte.<br />    Ce paramètre est obligatoire. Les valeurs possibles sont **True** et **False**.</li><li>**OSDAdapter0IPAddressList** : liste délimitée par des virgules des adresses IP de la carte. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur **false**.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0SubnetMask** : liste délimitée par des virgules des masques de sous-réseaux. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur **false**.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0Gateways** : liste délimitée par des virgules des adresses IP de passerelle. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur **false**.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0DNSDomain** : domaine DNS (Domain Name System) de la carte.</li><li>**OSDAdapter0DNSServerList** : liste délimitée par des virgules des serveurs DNS de la carte.<br />    Ce paramètre est obligatoire.</li><li>**OSDAdapter0EnableDNSRegistration** : **true** pour enregistrer les adresses IP de la carte dans le système DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration** : **true** pour enregistrer les adresses IP de la carte dans le système DNS sous le nom DNS complet de l’ordinateur.</li><li>**OSDAdapter0EnableIPProtocolFiltering** : **true** pour activer le filtrage de protocoles IP sur la carte.</li><li>**OSDAdapter0IPProtocolFilterList** : liste délimitée par des virgules des protocoles autorisés à s’exécuter sur IP. Cette propriété est ignorée sauf si **EnableIPProtocolFiltering** est réglé sur **false**.</li><li>**OSDAdapter0EnableTCPFiltering** : **true** pour activer le filtrage de ports TCP sur la carte.</li><li>**OSDAdapter0TCPFilterPortList** : liste délimitée par des virgules des ports auxquels les autorisations d’accès à TCP sont à accorder. Cette propriété est ignorée sauf si **EnableTCPFiltering** est réglé sur **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions** : options pour NetBIOS sur TCP/IP. Les valeurs possibles sont les suivantes :<br /><br /> <ul><li>**0** : utiliser des paramètres NetBIOS du serveur DHCP.</li><li>**1** : activer NetBIOS avec TCP/IP.</li><li>**2** : désactiver NetBIOS avec TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS** : **true** pour utiliser WINS pour la résolution de noms.</li><li>**OSDAdapter0WINSServerList** : liste délimitée par des virgules des adresses IP du serveur WINS. Cette propriété est ignorée sauf si **EnableWINS** est réglé sur **true**.</li><li>**OSDAdapter0MacAddress** : adresse MAC (Media Access Controller) utilisée pour faire correspondre les paramètres à la carte réseau physique.</li><li>**OSDAdapter0Name** : nom de la connexion réseau tel qu’il apparaît dans le programme Connexions réseau du Panneau de configuration. La longueur du nom est comprise entre 0 et 255 caractères.</li><li>**OSDAdapter0Index** : index des paramètres de carte réseau dans le tableau des paramètres.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (entrée)|Spécifie le nombre de cartes réseau installées sur l'ordinateur de destination. Quand la valeur **OSDAdapterCount** est définie, toutes les options de configuration de chaque carte doivent être définies. Par exemple, si vous définissez la valeur **OSDAdapterTCPIPNetbiosOptions** pour une carte spécifique, toutes les valeurs pour cette carte doivent également être configurées.<br /><br />Si cette valeur n’est pas spécifiée, toutes les valeurs **OSDAdapter** sont ignorées.|  
|OSDDNSDomain<br /><br /> (entrée)|Spécifie le serveur DNS principal utilisé sur l'ordinateur de destination.|  
|OSDDomainName<br /><br /> (entrée)|Spécifie le nom du domaine Windows auquel l'ordinateur de destination se joint. La valeur spécifiée doit être un nom de domaine de services de domaine Active Directory valide.|  
|OSDDomainOUName<br /><br /> (entrée)|Spécifie le format du nom RFC 1779 de l'unité d'organisation que l'ordinateur de destination joint. S'il est spécifié, la valeur doit contenir le chemin complet.<br /><br /> Exemple :<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (entrée)|Spécifie si le filtrage TCP/IP est activé.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDJoinAccount<br /><br /> (entrée)|Spécifie le compte réseau utilisé pour ajouter l'ordinateur de destination à un domaine Windows.|  
|OSDJoinPassword<br /><br /> (entrée)|Spécifie le mot de passe réseau utilisé pour ajouter l'ordinateur de destination à un domaine Windows.|  
|OSDNetworkJoinType<br /><br /> (entrée)|Spécifie si l'ordinateur de destination se joint à un domaine Windows ou un groupe de travail.<br /><br /> **0** indique que l’ordinateur de destination se joint à un domaine Windows. **1** spécifie que l’ordinateur se joint à un groupe de travail.<br /><br /> Valeurs valides :<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (entrée)|Spécifie l'ordre de recherche DNS de l'ordinateur de destination.|  
|OSDWorkgroupName<br /><br /> (entrée)|Spécifie le nom du groupe de travail auquel l'ordinateur de destination se joint.<br /><br /> Spécifiez cette valeur ou la valeur **OSDDomainName**. Le nom du groupe de travail est limité à 32 caractères.<br /><br /> Exemple :<br /><br /> **Comptabilité**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Appliquer l’image du système d’exploitation   
 Pour plus d'informations, voir [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (entrée)|Spécifie le nom du fichier de réponse de déploiement du système d'exploitation associé au package de déploiement du système d'exploitation.|  
|OSDImageIndex<br /><br /> (entrée)|Spécifie la valeur d'index de l'image du fichier WIM qui est appliquée à l'ordinateur de destination.|  
|OSDInstallEditionIndex<br /><br /> (entrée)|Spécifie la version du système d'exploitation Windows Vista ou version ultérieure qui est installée. Si aucune version n’est précisée, le programme d’installation de Windows détermine la version à installer à l’aide de la clé du produit référencé.<br /><br /> Utilisez uniquement une valeur égale à zéro (0) si les conditions suivantes sont vraies :<br /><br /> -   Vous installez un système d’exploitation antérieur à Windows Vista.<br />-   Vous installez une édition de licence en volume de Windows Vista ou version ultérieure, et aucune clé de produit n’est spécifiée.<br /><br /> Valeurs valides :<br /><br /> **0** (par défaut)|  
|OSDTargetSystemDrive (sortie)|Indique la lettre de lecteur de la partition contenant les fichiers du système d'exploitation.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Appliquer les paramètres Windows   
 Pour plus d’informations, consultez [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (entrée)|Spécifie le nom de l'ordinateur de destination.<br /><br /> Exemple :<br /><br /> **%_SMSTSMachineName%** (par défaut)|  
|OSDProductKey<br /><br /> (entrée)|Spécifie la clé de produit Windows. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  
|OSDRegisteredUserName<br /><br /> (entrée)|Spécifie le nom d'utilisateur inscrit par défaut dans le nouveau système d'exploitation. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  
|OSDRegisteredOrgName<br /><br /> (entrée)|Spécifie le nom d'organisation inscrit par défaut dans le nouveau système d'exploitation. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  
|OSDTimeZone<br /><br /> (entrée)|Spécifie le paramètre de fuseau horaire par défaut utilisé dans le nouveau système d'exploitation.|  
|OSDServerLicenseMode<br /><br /> (entrée)|Spécifie le mode de licence Windows Server utilisé.<br /><br /> Valeurs valides :<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (entrée)|Spécifie le nombre maximal de connexions autorisées. Le nombre spécifié doit comprendre entre 5 et 9 999 connexions.|  
|OSDRandomAdminPassword<br /><br /> (entrée)|Spécifie un mot de passe généré de manière aléatoire pour le compte de l'administrateur dans le nouveau système d'exploitation. Si cette variable a la valeur **true**, le programme d’installation de Windows désactive le compte d’administrateur local sur l’ordinateur cible. Si cette variable a la valeur **false**, le programme d’installation de Windows active le compte d’administrateur local sur l’ordinateur cible et affecte comme mot de passe la valeur de **OSDLocalAdminPassword**.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (entrée)|Spécifie le mot de passe de l'administrateur local. Si vous activez **Générer de façon aléatoire le mot de passe de l’administrateur local et désactiver le compte sur toutes les plates-formes prises en charge**, l’étape ignore cette variable. La valeur spécifiée doit comprendre entre 1 et 255 caractères.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Appliquer automatiquement les pilotes   
 Pour plus d’informations, consultez [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (entrée)|Liste délimitée par des virgules des ID de catégorie uniques du catalogue de pilotes. L’étape **Appliquer automatiquement les pilotes** tient uniquement compte des pilotes figurant dans au moins l’une des catégories spécifiées. Cette valeur est facultative et n'est pas définie par défaut. Obtient les ID de catégorie disponibles par énumération de la liste des objets **SMS_CategoryInstance** sur le site.|  
|OSDAllowUnsignedDriver<br /><br /> (entrée)|Spécifie si Windows est configuré pour autoriser l'installation de pilotes de périphérique non signés. Cette variable de séquence de tâches n'est pas utilisée au cours du déploiement de Windows Vista et des systèmes d'exploitation ultérieurs.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (entrée)|S’il existe dans le catalogue de pilotes plusieurs pilotes de périphériques compatibles avec un périphérique matériel, cette variable détermine l’action de l’étape. Si cette variable a la valeur **true**, l’étape installe uniquement le meilleur pilote de périphérique. Si cette variable a la valeur **false**, l’étape installe tous les pilotes de périphériques compatibles, et Windows choisit le meilleur pilote à utiliser.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|Lors de la demande du catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend la connexion au serveur HTTP. Si la connexion prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **60** secondes.|  
|SMSTSDriverRequestReceiveTimeOut|Lors de la demande du catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend une réponse. Si la connexion prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **480** secondes.|
|SMSTSDriverRequestResolveTimeOut|Lors de la demande du catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend la résolution de noms HTTP. Si la connexion prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **60** secondes.|
|SMSTSDriverRequestSendTimeOut|Lors de l’envoi d’une demande de catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend avant d’envoyer la demande. Si la demande prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **60** secondes.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Capturer les paramètres réseau   
 Pour plus d’informations, consultez [Capturer les paramètres réseau](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (entrée)|Spécifie si les informations de configuration des paramètres de carte réseau (TCP/IP, DNS et WINS) sont capturées.<br /><br /> Exemples :<br /><br /> **true** (par défaut)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (entrée)|Spécifie si les informations d'appartenance à un groupe de travail ou un domaine sont migrées dans le cadre du déploiement du système d'exploitation.<br /><br /> Exemples :<br /><br /> **true** (par défaut)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturer l’image du système d’exploitation   
 Pour plus d’informations, consultez [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (entrée)|Spécifie un nom de compte Windows qui dispose d'autorisations pour stocker l'image capturée sur un partage réseau.|  
|OSDCaptureAccountPassword<br /><br /> (entrée)|Spécifie le mot de passe du compte Windows employé pour le stockage de l'image capturée sur un partage réseau.|  
|OSDCaptureDestination<br /><br /> (entrée)|Spécifie l'emplacement où l'image capturée du système d'exploitation est enregistrée. Le nom du répertoire est limité à 255 caractères.|  
|OSDImageCreator<br /><br /> (entrée)|Nom facultatif de l'utilisateur qui a créé l'image. Ce nom est stocké dans le fichier WIM. Le nom de l'utilisateur est limité à 255 caractères.|  
|OSDImageDescription<br /><br /> (entrée)|Description facultative de l'image du système d'exploitation capturée définie par l'utilisateur. Cette description est stockée dans le fichier WIM. La description est limitée à 255 caractères.|  
|OSDImageVersion<br /><br /> (entrée)|Numéro de version facultatif défini par l'utilisateur à attribuer à l'image du système d'exploitation capturée. Ce numéro de version est stocké dans le fichier WIM. Cette valeur peut être n'importe quelle combinaison de lettres avec une longueur maximale de 32 caractères.|  
|OSDTargetSystemRoot<br /><br /> (entrée)|Spécifie le chemin du répertoire Windows où a été installé le système d'exploitation sur l'ordinateur de référence. Configuration Manager vérifie que ce système d’exploitation est pris en charge pour la capture.|  



###  <a name="BKMK_CaptureUserState"></a> Capturer l’état utilisateur   
 Pour plus d’informations, consultez [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrée)|Le chemin d'accès UNC ou local du dossier sur lequel l'état utilisateur est enregistré. Pas de valeur par défaut.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (entrée)|Options de ligne de commande supplémentaires de l’outil de migration de l’état utilisateur (USMT) utilisées par la séquence de tâches pour capturer l’état utilisateur. L’étape n’expose pas ces paramètres dans l’éditeur de séquence de tâches. Spécifiez ces options sous forme de chaîne, que la séquence de tâches ajoute à la ligne de commande USMT générée automatiquement.<br /><br />La précision des options USMT spécifiées avec cette variable de séquence de tâches n'est pas validée avant l'exécution de la séquence de tâches.|  
|OSDMigrateMode<br /><br /> (entrée)|Permet de personnaliser les fichiers capturés par l'outil de migration de l'état utilisateur (USMT). Si cette variable a la valeur **Simple**, la séquence de tâches utilise seulement les fichiers de configuration USMT standard. Si cette variable a la valeur **Avancé**, la variable de séquence de tâches OSDMigrateConfigFiles spécifie les fichiers de configuration utilisés par USTM.<br /><br /> Valeurs valides :<br /><br /> **Simple**<br /><br /> **Avancé**|  
|OSDMigrateConfigFiles<br /><br /> (entrée)|Spécifie les fichiers de configuration employés pour contrôler la capture des profils utilisateur. Cette variable est utilisée uniquement si OSDMigrateMode a la valeur Avancé. Cette valeur de liste délimitée par des virgules est définie pour effectuer une migration du profil utilisateur personnalisée.<br /><br /> Exemple : miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (entrée)|Si USMT ne peut pas capturer certains fichiers, cette variable permet à la capture de l’état utilisateur de se poursuivre.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrée)|Active la journalisation documentée pour USMT.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (entrée)|Spécifie si les fichiers cryptés sont capturés.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|_OSDMigrateUsmtPackageID<br /><br /> (entrée)|Spécifie l’ID du package Configuration Manager qui contient les fichiers USMT. Cette variable est requise.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Capturer les paramètres Windows   
 Pour plus d’informations, consultez [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (entrée)|Spécifie si le nom de l'ordinateur est migré.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**<br /><br /> Si la valeur est **true**, la variable OSDComputerName prend le nom NetBIOS de l’ordinateur.|  
|OSDComputerName<br /><br /> (sortie)|Défini sur le nom NetBIOS de l'ordinateur. La valeur est définie uniquement si la variable OSDMigrateComputerName a la valeur **true**.|  
|OSDMigrateRegistrationInfo<br /><br /> (entrée)|Spécifie si l’étape migre les informations sur l’utilisateur et l’organisation.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**<br /><br /> Si la valeur est **true**, la variable OSDRegisteredOrgName prend le nom d’organisation inscrit de l’ordinateur.|  
|OSDRegisteredOrgName<br /><br /> (sortie)|Défini sur le nom d'organisation inscrit de l'ordinateur. La valeur est définie uniquement si la variable OSDMigrateRegistrationInfo a la valeur **true**.|  
|OSDMigrateTimeZone<br /><br /> (entrée)|Spécifie si le fuseau horaire de l'ordinateur est migré.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**<br /><br /> Si la valeur est **true**, la variable OSDTimeZone est définie sur le fuseau horaire de l’ordinateur.|  
|OSDTimeZone<br /><br /> (sortie)|Défini sur le fuseau horaire de l'ordinateur. La valeur est définie uniquement si la variable OSDMigrateTimeZone a la valeur **true**.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> Se connecter à un dossier réseau   
 Pour plus d’informations, consultez [Se connecter à un dossier réseau](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (entrée)|Spécifie le compte d'administrateur utilisé pour se connecter au partage réseau.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (entrée)|Spécifie la lettre de lecteur réseau à laquelle se connecter. Cette valeur est facultative. Si vous ne la spécifiez pas, la connexion réseau doit alors être mappée à une lettre de lecteur. À l’inverse, si vous la spécifiez, cette valeur doit être comprise entre D: et Z:. En outre, n’utilisez pas X: car il s’agit de la lettre de lecteur utilisée par Windows PE au cours de la phase Windows PE.<br /><br /> Exemples :<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (entrée)|Spécifie le mot de passe réseau utilisé pour se connecter au partage réseau.|  
|SMSConnectNetworkFolderPath<br /><br /> (entrée)|Spécifie le chemin d'accès réseau pour la connexion.<br /><br /> Exemple :<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a> Activer BitLocker   
 Pour plus d’informations, consultez [Activer BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (entrée)|Au lieu de créer un mot de passe de récupération aléatoire, l'action de la séquence de tâches **Activer BitLocker** utilise la valeur spécifiée comme mot de passe de récupération. La valeur doit être un mot de passe de récupération numérique BitLocker valide.|  
|OSDBitLockerStartupKey<br /><br /> (entrée)|Au lieu de générer une clé de démarrage aléatoire pour l’option de gestion de clé **Clé de démarrage sur USB uniquement**, l’étape **Activer BitLocker** utilise le module de plateforme sécurisée (TPM) comme clé de démarrage. La valeur doit être une clé de démarrage BitLocker valide 256 bits codée en Base64.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Formater et partitionner le disque   
 Pour plus d’informations, consultez [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (entrée)|Spécifie le nombre de disques physiques à partitionner.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (entrée)|Lors du partitionnement du disque dur pour des raisons de compatibilité avec certains types de BIOS, cette variable spécifie si les optimisations d’alignement du cache sont désactivées. Ceci est nécessaire lors du déploiement des systèmes d’exploitation Windows XP ou Windows Server 2003. Pour plus d'informations, consultez [l'article 931760](http://go.microsoft.com/fwlink/?LinkId=134081) et [l'article 931761](http://go.microsoft.com/fwlink/?LinkId=134082) de la Base de connaissances Microsoft.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)| 
|OSDGPTBootDisk<br /><br /> (entrée)|Spécifie s’il faut créer une partition EFI sur un disque dur GPT. Les ordinateurs EFI utilisent cette partition en tant que disque de démarrage.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDPartitions<br /><br /> (entrée)|Spécifie un tableau de paramètres de partition. Consultez la rubrique liée au kit de développement logiciel (SDK) pour accéder aux variables de matrice dans l'environnement de la séquence de tâches.<br /><br /> Cette variable de séquence de tâches est une variable de matrice. Chaque élément de la matrice représente les paramètres d'une partition simple sur le disque dur. Accédez aux paramètres définis pour chaque partition en combinant le nom de la variable de matrice avec le numéro de partition de disque de base zéro et le nom de propriété.<br /><br /> Par exemple, utilisez les noms de variables suivants pour définir les propriétés de la première partition créée sur le disque dur par cette étape :<br /><br /> - **OSDPartitions0Type** : spécifie le type de partition. Cette propriété est obligatoire. Les valeurs valides sont : **Principal**, **Étendu**, **Logique** et **Caché**.<br />-   **OSDPartitions0FileSystem** : spécifie le type de système de fichier à utiliser lors du formatage de la partition. Cette propriété est facultative. Si vous ne spécifiez pas de système de fichiers, l’étape ne formate pas la partition. Les valeurs valides sont **FAT32** et **NTFS**.<br />-   **OSDPartitions0Bootable** : indique si la partition est amorçable. Cette propriété est obligatoire. Si cette valeur est **TRUE** pour les disques MBR, l’étape marque cette partition comme active.<br />-   **OSDPartitions0QuickFormat** : spécifie le type de format utilisé. Cette propriété est obligatoire. Si cette valeur est **TRUE**, l’étape effectue un formatage rapide. Sinon, l’étape effectue un formatage complet.<br />-   **OSDPartitions0VolumeName** : spécifie le nom attribué au volume après formatage. Cette propriété est facultative.<br />-   **OSDPartitions0Size** : spécifie la taille de la partition. Les unités sont spécifiées par la variable **OSDPartitions0SizeUnits** . Cette propriété est facultative. Si cette propriété n'est pas spécifiée, la partition est créée en utilisant la totalité de l'espace disque disponible.<br />-   **OSDPartitions0SizeUnits** : l’étape utilise ces unités pour interpréter la variable **OSDPartitions0Size**. Cette propriété est facultative. Les valeurs valides sont **Mo** (par défaut), **Go** et **Pourcent**.<br />-   **OSDPartitions0VolumeLetterVariable** : quand cette étape crée des partitions, elle utilise toujours la lettre de lecteur disponible suivante dans Windows PE. Utilisez cette propriété facultative pour spécifier le nom d’une autre variable de séquence de tâches. L’étape utilise cette variable afin d’enregistrer la nouvelle lettre de lecteur pour référence ultérieure.<br /><br />Si vous définissez plusieurs partitions avec cette action de séquence de tâches, les propriétés de la deuxième partition sont définies en utilisant leur index dans le nom de variable. Par exemple : **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** et **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (entrée)|Spécifie le style de partition à utiliser lors du partitionnement du disque. **MBR** indique le style de partition Enregistrement de démarrage principal, et **GPT** indique le style Table de partition GUID.<br /><br /> Valeurs valides :<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Installer l’application   
 Pour plus d’informations, consultez [Installer l’application](task-sequence-steps.md#BKMK_InstallApplication).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Spécifiez si le moteur de séquence de tâches considère un avertissement détecté comme une erreur lors de cette étape. La séquence de tâches affecte la valeur **Warning** à la variable _TSAppInstallStatus quand une ou plusieurs applications, ou une dépendance nécessaire, n’ont pas été installées car une exigence n’a pas été satisfaite. Quand vous affectez la valeur **True** à cette variable et que la séquence de tâches affecte la valeur Warning à _TSAppInstallStatus, le résultat est une erreur. La valeur **False** est le comportement par défaut.| 
|SMSTSMPListRequestTimeoutEnabled|Cette variable permet d’activer les demandes MPList répétées pour actualiser le client s’il ne se trouve pas sur l’intranet. <br />Par défaut, cette valeur est **True**. Si des clients se trouvent sur Internet, vous pouvez définir cette variable sur **False** pour éviter des retards inutiles. Cette variable s’applique uniquement aux étapes de la séquence de tâches relatives à l’installation de l’application et à l’installation des mises à jour logicielles.|  
|SMSTSMPListRequestTimeout|Spécifiez le délai d’attente (en millisecondes) d’une séquence de tâche avant qu’elle réessaie d’installer une application après un échec de récupération de la liste de points de gestion à partir des services d’emplacement. Par défaut, la séquence de tâches attend **60000** millisecondes (60 secondes) avant de retenter d’exécuter l’étape et elle effectue jusqu’à trois nouvelles tentatives.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Installer les mises à jour logicielles   
Pour plus d’informations, consultez [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (entrée)|Spécifie s'il faut installer toutes les mises à jour ou uniquement les mises à jour obligatoires.<br /><br /> Valeurs valides :<br /><br /> **Tous**<br /><br /> **Obligatoire**|  
|SMSTSSoftwareUpdateScanTimeout| Contrôlez le délai d’attente pour l’analyse des mises à jour logicielles pendant cette étape. Par exemple, augmentez la valeur si vous vous attendez à de nombreuses mises à jour lors de l’analyse. La valeur par défaut est **1800** secondes (30 minutes). La valeur de la variable est définie en secondes. |
|SMSTSWaitForSecondReboot|Cette variable de séquence de tâches facultative contrôle le comportement du client quand l’installation d’une mise à jour logicielle nécessite deux redémarrages. Définissez cette variable avant cette étape afin d’empêcher qu’une séquence de tâches échoue en raison d’un second redémarrage résultant de l’installation d’une mise à jour logicielle.<br /><br /> Définissez la valeur de SMSTSWaitForSecondReboot en secondes afin de spécifier la durée pendant laquelle la séquence de tâches s’interrompt sur cette étape pendant le redémarrage de l’ordinateur. Laissez suffisamment de temps au cas où un second redémarrage serait nécessaire. <br />Par exemple, si vous définissez SMSTSWaitForSecondReboot sur 600, la séquence de tâches est suspendue pendant 10 minutes après un redémarrage, avant l’exécution des étapes supplémentaires. Cette variable est utile quand une étape de séquence de tâches d’installation de mises à jour logicielles installe plusieurs centaines de mises à jour logicielles.| 
|SMSTSMPListRequestTimeoutEnabled|Cette variable permet d’activer les demandes MPList répétées pour actualiser le client s’il ne se trouve pas sur l’intranet. <br />Par défaut, cette valeur est **True**. Si des clients se trouvent sur Internet, vous pouvez définir cette variable sur **False** pour éviter des retards inutiles. Cette variable s’applique uniquement aux étapes de la séquence de tâches relatives à l’installation de l’application et à l’installation des mises à jour logicielles.|  
|SMSTSMPListRequestTimeout|Spécifiez le délai d’attente (en millisecondes) d’une séquence de tâche avant qu’elle réessaie d’installer une mise à jour logicielle après un échec de récupération de la liste de points de gestion à partir des services d’emplacement. Par défaut, la séquence de tâches attend **60000** millisecondes (60 secondes) avant de retenter d’exécuter l’étape et elle effectue jusqu’à trois nouvelles tentatives.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Joindre le domaine ou le groupe de travail   
 Pour plus d’informations, consultez [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (entrée)|Spécifie le compte utilisé par l’ordinateur de destination pour se joindre au domaine Active Directory. Cette variable est requise lors de la jonction à un domaine.|  
|OSDJoinDomainName<br /><br /> (entrée)|Spécifie le nom d’un domaine Active Directory auquel l’ordinateur de destination se joint. Le nom de domaine doit comprendre entre 1 et 255 caractères.|  
|OSDJoinDomainOUName<br /><br /> (entrée)|Spécifie le format du nom RFC 1779 de l'unité d'organisation que l'ordinateur de destination joint. S'il est spécifié, la valeur doit contenir le chemin complet. Le nom de l’unité d’organisation doit comprendre entre 0 et 32 767 caractères. Cette valeur n’est pas définie si la variable **OSDJoinType** est **1** (joindre le groupe de travail).<br /><br /> Exemple :<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (entrée)|Spécifie le mot de passe réseau utilisé par l’ordinateur de destination pour se joindre au domaine Active Directory. Si l’environnement de séquence de tâches n’inclut pas cette variable, le programme d’installation de Windows essaie d’utiliser un mot de passe vide. Si la variable **OSDJoinType** est définie sur **0** (joindre le domaine), cette valeur est obligatoire.|  
|OSDJoinSkipReboot<br /><br /> (entrée)|Spécifie s'il faut ignorer le redémarrage après que l'ordinateur de destination joint le domaine ou le groupe de travail.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (entrée)|Spécifie si l'ordinateur de destination se joint à un domaine Windows ou un groupe de travail. Pour joindre l’ordinateur de destination à un domaine Windows, spécifiez **0**. Pour joindre l’ordinateur de destination à un groupe de travail, spécifiez **1**.<br /><br /> Valeurs valides :<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (entrée)|Spécifie le nom d'un groupe de travail auquel l'ordinateur de destination se joint. Le nom de groupe de travail doit comprendre entre 1 et 32 caractères.<br /><br /> Exemple :<br /><br /> **Comptabilité**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Préparer Windows pour capture   
 Pour plus d’informations, consultez [Préparer Windows pour capture](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (entrée)|Spécifie si Sysprep crée une liste de pilotes de dispositifs de stockage de masse. Ce paramètre s’applique uniquement à Windows XP et à Windows Server 2003. Cette variable remplit la section [SysprepMassStorage] de sysprep.inf avec les informations de tous les pilotes de stockage de masse qui sont pris en charge par l’image à capturer.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDKeepActivation<br /><br /> (entrée)|Spécifie si sysprep réinitialise l'indicateur d'activation du produit.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDTargetSystemRoot<br /><br /> (sortie)|Spécifie le chemin du répertoire Windows où a été installé le système d'exploitation sur l'ordinateur de référence. Configuration Manager vérifie que ce système d’exploitation est pris en charge pour la capture.|  



###  <a name="BKMK_ReleaseStateStore"></a> Libérer le magasin d’état   
 Pour plus d’informations, consultez [Libérer le magasin d’état](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrée)|Le chemin d'accès UNC ou local de l'emplacement à partir duquel l'état utilisateur est restauré. Cette valeur est utilisée par les actions de séquence de tâches **Capturer l'état utilisateur** et **Restaurer l'état utilisateur** .|  



###  <a name="BKMK_RequestState"></a> Demander le magasin d’état   
  Pour plus d’informations, consultez [Libérer le magasin d’état](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (entrée)|Quand le compte d’ordinateur ne parvient pas à se connecter au point de migration de l’état, cette variable spécifie si la séquence de tâches doit utiliser le compte d’accès réseau.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDStateSMPRetryCount<br /><br /> (entrée)|Spécifie le nombre de tentatives de recherche d'un point de migration d'état par l'étape de la séquence de tâches avant d'abandonner. Le nombre spécifié doit être compris entre 0 et 600.|  
|OSDStateSMPRetryTime<br /><br /> (entrée)|Indique la durée en secondes pendant laquelle l'étape de la séquence de tâches attend entre chaque tentative. Le nombre de secondes est limité à 30 caractères.|  
|OSDStateStorePath<br /><br /> (sortie)|Le chemin d'accès UNC au dossier sur le point de migration d'état où est stocké l'état d'utilisateur.|  



###  <a name="BKMK_RestartComputer"></a> Redémarrer l’ordinateur   
 Pour plus d’informations, consultez [Redémarrer l’ordinateur](task-sequence-steps.md#BKMK_RestartComputer).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (entrée)|Indique le message à afficher aux utilisateurs avant le redémarrage de l'ordinateur de destination. Si vous ne définissez pas cette variable, le texte par défaut est affiché. Le message spécifié ne doit pas dépasser 512 caractères.<br /><br /> Exemple :<br /><br /> **Enregistrez votre travail avant le redémarrage de l’ordinateur.**|  
|SMSRebootTimeout<br /><br /> (entrée)|Spécifie le nombre de secondes pendant lesquelles l'avertissement est affiché à l'attention de l'utilisateur avant le redémarrage de l'ordinateur. Précisez zéro seconde pour indiquer qu'aucun message de redémarrage n'apparaît.<br /><br /> Exemples :<br /><br /> **0** (par défaut)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Restaurer l’état utilisateur   
  Pour plus d’informations, consultez [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (entrée)|Le chemin d'accès UNC ou local du dossier à partir duquel l'état utilisateur est restauré.|  
|OSDMigrateContinueOnRestore<br /><br /> (entrée)|Poursuivez le processus, même si l’outil USMT ne peut pas restaurer certains fichiers.<br /><br /> Valeurs valides :<br /><br /> **true** (par défaut)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (entrée)|Active la journalisation documentée pour l'outil USMT. Cette valeur est requise par l’action.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDMigrateLocalAccounts<br /><br /> (entrée)|Indique si le compte d'ordinateur local est restauré.<br /><br /> Valeurs valides :<br /><br /> **true**<br /><br /> **false** (par défaut)|  
|OSDMigrateLocalAccountPassword<br /><br /> (entrée)|Si la variable **OSDMigrateLocalAccounts** a la valeur « true », cette variable doit contenir le mot de passe affecté à tous les comptes locaux migrés. USMT attribue le même mot de passe à tous les comptes locaux migrés. Considérez ce mot de passe comme temporaire et changez-le ultérieurement à l’aide d’une autre méthode.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (entrée)|Indique les options de ligne de commande supplémentaires de l’outil USMT qui sont utilisées lors de la restauration de l’état utilisateur. Ces options supplémentaires sont spécifiées sous forme d'une chaîne ajoutée à la ligne de commande USMT générée de manière automatique. La précision des options USMT spécifiées avec cette variable de séquence de tâches n'est pas validée avant l'exécution de la séquence de tâches.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (entrée)|Spécifie l’ID du package Configuration Manager qui contient les fichiers USMT. Cette variable est requise.|  



###  <a name="BKMK_RunCommand"></a> Exécuter la ligne de commande   
  Pour plus d’informations, consultez [Exécuter la ligne de commande](task-sequence-steps.md#BKMK_RunCommandLine).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action|Description|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (entrée)|Par défaut sur un système d’exploitation 64 bits, la séquence de tâches recherche et exécute le programme sur la ligne de commande à l’aide du redirecteur du système de fichiers WOW64. Ce comportement permet à la commande de trouver les versions 32 bits des DLL et des programmes de système d’exploitation. L’affectation de la valeur **true** à cette variable désactive l’utilisation du redirecteur de système de fichiers WOW64. La commande recherche les versions 64 bits natives des DLL et des programmes de système d’exploitation. Cette variable est sans effet sous un système d'exploitation 32 bits.|  
|WorkingDirectory<br /><br /> (entrée)|Spécifie un répertoire de démarrage pour une action de ligne de commande. Le répertoire spécifié ne doit pas dépasser 255 caractères.<br /><br /> Exemples :<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (entrée)|Indique le compte par lequel la ligne de commande est exécutée. La valeur est une chaîne au format nomutilisateur ou domaine\nomutilisateur.|  
|SMSTSRunCommandLinePassword<br /><br /> (entrée)|Indique le mot de passe pour le compte spécifié par la variable SMSTSRunCommandLineUserName.|  



### <a name="set-dynamic-variables"></a>Définir des variables dynamiques  
Pour plus d’informations, consultez [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Spécifie la marque de l’ordinateur.|  
|_SMSTSModel|Spécifie le modèle de l’ordinateur.|  
|_SMSTSMacAddresses|Spécifie les adresses MAC utilisées par l’ordinateur.|  
|_SMSTSIPAddresses|Spécifie les adresses IP utilisées par l’ordinateur.|  
|_SMSTSSerialNumber|Spécifie le numéro de série de l’ordinateur.|  
|_SMSTSAssetTag|Spécifie la balise de ressource de l’ordinateur.|  
|_SMSTSUUID|Spécifie l’UUID de l’ordinateur.|  
|_SMSTSDefaultGateways|Spécifie les passerelles par défaut utilisées par l’ordinateur.|  



###  <a name="BKMK_SetupWindows"></a> Configurer Windows et ConfigMgr   
  Pour plus d’informations, consultez [Configurer Windows et ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (entrée)|Spécifie les propriétés d’installation de client qui sont utilisées pendant l’installation du client Configuration Manager.|  



### <a name="upgrade-operating-system"></a>Mettre à niveau le système d’exploitation  
 Pour plus d’informations, consultez [Mettre à niveau le système d’exploitation](task-sequence-steps.md#BKMK_UpgradeOS).  

#### <a name="details"></a>Détails  

|Nom de la variable d'action<br /><br /> (entrée)|Description|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (entrée)|Spécifie les options de ligne de commande supplémentaires qui sont ajoutées au programme d’installation de Windows durant une mise à niveau Windows 10. La séquence de tâches ne vérifie pas les options de ligne de commande.<br /><br /> Pour plus d’informations, consultez [Options de ligne de commande du programme d’installation de Windows](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  
