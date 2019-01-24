---
title: Référence sur la variable de séquence de tâches
titleSuffix: Configuration Manager
description: En savoir plus sur les variables pour contrôler et personnaliser une séquence de tâches Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 62f15230-d3a6-4afc-abd4-1e07e7ba6c97
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7a2801b7efa513b2b15a58a7a89eee5d4727a21
ms.sourcegitcommit: d5c013a29f53b975fe3a6cb0a41f1e817bd7b235
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54342895"
---
# <a name="task-sequence-variables-in-configuration-manager"></a>Variables de séquence de tâches dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article constitue une référence pour toutes les variables disponibles dans l’ordre alphabétique. Utilisez la fonction **Rechercher** du navigateur (en général **CTRL** + **F**) pour rechercher une variable spécifique. La variable indique si elle est spécifique à une étape particulière. L’article sur les [étapes de séquence de tâches](/sccm/osd/understand/task-sequence-steps) inclut la liste des variables spécifiques à chaque étape. 

Pour plus d'informations, consultez [Utilisation des variables de séquence de tâches](/sccm/osd/understand/using-task-sequence-variables).



## <a name="bkmk_tsvar"></a> Référence sur la variable de séquence de tâches


### <a name="OSDDetectedWinDir"></a> _OSDDetectedWinDir

 Au démarrage de Windows PE, la séquence de tâches analyse les disques durs de l’ordinateur à la recherche d’une installation antérieure du système d’exploitation. L’emplacement du dossier Windows est stocké dans cette variable. Vous pouvez configurer votre séquence de tâches pour récupérer cette valeur à partir de l’environnement, et l’utiliser pour spécifier le même emplacement du dossier Windows à utiliser pour la nouvelle installation du système d’exploitation.


### <a name="OSDDetectedWinDrive"></a> _OSDDetectedWinDrive

 Au démarrage de Windows PE, la séquence de tâches analyse les disques durs de l’ordinateur à la recherche d’une installation antérieure du système d’exploitation. L’emplacement d’installation du système d’exploitation sur le disque dur est stocké dans cette variable. Vous pouvez configurer votre séquence de tâches pour récupérer cette valeur à partir de l’environnement, et l’utiliser pour spécifier le même emplacement de disque dur à utiliser pour le nouveau système d’exploitation.


### <a name="OSDMigrateUsmtPackageID"></a> _OSDMigrateUsmtPackageID

 *S’applique à l’étape [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).*

 (entrée)

 Spécifie l’ID du package Configuration Manager qui contient les fichiers USMT. Cette variable est requise.


### <a name="OSDMigrateUsmtRestorePackageID"></a> _OSDMigrateUsmtRestorePackageID

 *S’applique à l’étape [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).*

 (entrée)

 Spécifie l’ID du package Configuration Manager qui contient les fichiers USMT. Cette variable est requise.


### <a name="SMSTSAdvertID"></a> _SMSTSAdvertID

 Stocke l'ID unique de déploiement de la séquence de tâches en cours d'exécution. Elle utilise le même format qu’un ID de déploiement de distribution logicielle Configuration Manager. Si la séquence de tâches s'exécute à partir d'un média autonome, cette variable n'est pas définie.

 #### <a name="example"></a>Exemple
 `ABC20001`


### <a name="SMSTSAssetTag"></a> _SMSTSAssetTag

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie la balise de ressource de l’ordinateur.


### <a name="SMSTSBootImageID"></a> _SMSTSBootImageID

 Si la séquence de tâches en cours d’exécution référence un package d’images de démarrage, cette variable stocke l’ID de package d’images de démarrage. Si la séquence de tâches ne référence pas un package d’images de démarrage, cette variable n’est pas définie.

 #### <a name="example"></a>Exemple
 `ABC00001`  


### <a name="SMSTSBootUEFI"></a> _SMSTSBootUEFI

 La séquence de tâches définit cette variable lorsqu’elle détecte un ordinateur en mode UEFI.


### <a name="SMSTSClientGUID"></a> _SMSTSClientGUID

 Stocke la valeur du GUID du client Configuration Manager. Si la séquence de tâches s’exécute à partir d’un média autonome, cette variable n’est pas définie.

 #### <a name="example"></a>Exemple
 `0a1a9a4b-fc56-44f6-b7cd-c3f8ee37c04c`


### <a name="SMSTSCurrentActionName"></a> _SMSTSCurrentActionName

 Spécifie le nom de l'étape de séquence de tâches en cours d'exécution. Cette variable est définie avant que le gestionnaire des séquences de tâches exécute chaque étape individuelle.

 #### <a name="example"></a>Exemple
 `run command line`


### <a name="SMSTSDefaultGateways"></a> _SMSTSDefaultGateways

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie les passerelles par défaut utilisées par l’ordinateur.


### <a name="SMSTSDownloadOnDemand"></a> _SMSTSDownloadOnDemand

 Si la séquence de tâches active s’exécute en mode de téléchargement sur demande, cette variable est `true`. Le mode de téléchargement sur demande signifie que le gestionnaire des séquences de tâches télécharge le contenu localement uniquement quand il doit y accéder.


### <a name="SMSTSInWinPE"></a> _SMSTSInWinPE

 Quand l’étape de séquence de tâches active s’exécute dans Windows PE, cette variable est `true`. Testez cette variable de séquence de tâches pour déterminer l’environnement de système d’exploitation actuel.


### <a name="SMSTSIPAddresses"></a> _SMSTSIPAddresses

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie les adresses IP utilisées par l’ordinateur.


### <a name="SMSTSLastActionName"></a> _SMSTSLastActionName
 *À compter de la version 1810*  

 Stocke le nom de la dernière action exécutée. Cette variable se rapporte à **_SMSTSLastActionRetCode**. La séquence de tâches consigne ces valeurs dans le fichier smsts.log. Cette variable est utile lors du dépannage d’une séquence de tâches. Lorsqu’une étape échoue, un script personnalisé peut inclure le nom de l’étape avec le code de retour.


### <a name="SMSTSLastActionRetCode"></a> _SMSTSLastActionRetCode

 Stocke le code de retour à partir de la dernière action exécutée. Cette variable peut être utilisée comme une condition pour déterminer si l'étape suivante est exécutée.

 #### <a name="example"></a>Exemple
 `0`


### <a name="SMSTSLastActionSucceeded"></a> _SMSTSLastActionSucceeded

 - Si la dernière étape a réussi, cette variable est `true`.  

 - Si la dernière étape a échoué, elle est `false`.  

 - Si la séquence de tâches a ignoré la dernière action, car l’étape est désactivée ou la condition associée a été évaluée comme **false**, cette variable n’est pas réinitialisée. Elle contient toujours la valeur de l’action précédente.  

 
### <a name="SMSTSLaunchMode"></a> _SMSTSLaunchMode

 Spécifie que la séquence de tâches a démarré via l’une des méthodes suivantes :  

 - **SMS** : le client Configuration Manager, comme quand un utilisateur le démarre à partir du Centre logiciel
 - **UFD** : média USB hérité
 - **UFD+FORMAT** : média USB plus récent
 - **CD** : CD démarrable
 - **DVD** : DVD démarrable
 - **PXE** : démarrage réseau avec PXE
 - **HD** : média préparé sur un disque dur


### <a name="SMSTSLogPath"></a> _SMSTSLogPath

 Stocke le chemin d'accès complet du répertoire des journaux. Utilisez cette valeur pour déterminer où les étapes de séquence de tâches journalisent leurs actions. Cette valeur n’est pas définie si un disque dur n’est pas disponible.


### <a name="SMSTSMacAddresses"></a> _SMSTSMacAddresses

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie les adresses MAC utilisées par l’ordinateur.


### <a name="SMSTSMachineName"></a> _SMSTSMachineName

 Stocke et spécifie le nom de l'ordinateur. Stocke le nom de l’ordinateur utilisé par la séquence de tâches pour consigner tous les messages d’état. Pour modifier le nom d’ordinateur dans le nouveau système d’exploitation, utilisez la variable [OSDComputerName](#OSDComputerName).


### <a name="SMSTSMake"></a> _SMSTSMake

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie la marque de l’ordinateur.


### <a name="SMSTSMDataPath"></a> _SMSTSMDataPath

 Spécifie le chemin d’accès défini par la variable [SMSTSLocalDataDrive](#SMSTSLocalDataDrive). Quand vous définissez SMSTSLocalDataDrive avant le démarrage de la séquence de tâches, notamment en définissant une variable de regroupement, Configuration Manager définit ensuite la variable _SMSTSMDataPath une fois que la séquence de tâches démarre.


### <a name="SMSTSMediaType"></a> _SMSTSMediaType

 Spécifie le type de média qui est utilisé pour démarrer l’installation. Le média de démarrage, le média complet, l'environnement PXE et le média préparé sont des exemples de types de médias.


### <a name="SMSTSModel"></a> _SMSTSModel

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie le modèle de l’ordinateur.


### <a name="SMSTSMP"></a> _SMSTSMP

 Stocke l’URL ou l’adresse IP d’un point de gestion Configuration Manager.


### <a name="SMSTSMPPort"></a> _SMSTSMPPort

 Stocke le numéro de port d’un point d’administration Configuration Manager.


### <a name="SMSTSOrgName"></a> _SMSTSOrgName

 Stocke le nom de personnalisation affiché par la séquence de tâches dans la boîte de dialogue de progression.


### <a name="SMSTSOSUpgradeActionReturnCode"></a> _SMSTSOSUpgradeActionReturnCode

 *S’applique à l’étape [Mise à niveau du système d’exploitation](task-sequence-steps.md#BKMK_UpgradeOS).*

 Stocke la valeur du code de sortie retournée par le programme d’installation de Windows pour indiquer la réussite ou l’échec. Cette variable est utile avec l’option de ligne de commande `/Compat`.

 #### <a name="example"></a>Exemple
 À l’issue de l’exécution d’une analyse compat-only, prenez des mesures dans les étapes ultérieures selon que le code de sortie échoue ou réussit. En cas de réussite, lancez la mise à niveau. Ou définissez un indicateur dans l’environnement à collecter avec l’inventaire matériel. Par exemple, ajoutez un fichier ou définissez une clé de Registre. Utilisez ce marqueur pour créer un regroupement d’ordinateurs prêts pour la mise à niveau ou nécessitant une action avant la mise à niveau.


### <a name="SMSTSPackageID"></a> _SMSTSPackageID

 Stocke l'ID de la séquence de tâches en cours d'exécution. Cet ID utilise le même format qu’un ID de package Configuration Manager. 

 #### <a name="example"></a>Exemple
 `HJT00001`


### <a name="SMSTSPackageName"></a> _SMSTSPackageName

 Stocke le nom de la séquence de tâches en cours d’exécution. Un administrateur Configuration Manager spécifie ce nom lors de la création de la séquence de tâches.

 #### <a name="example"></a>Exemple
 `Deploy Windows 10 task sequence`


### <a name="SMSTSRunFromDP"></a> _SMSTSRunFromDP

 À définir sur `true` si la séquence de tâches active s’exécute en mode run-from-distribution-point. Ce mode signifie que le gestionnaire des séquences de tâches obtient les partages de packages requis à partir du point de distribution.


### <a name="SMSTSSerialNumber"></a> _SMSTSSerialNumber

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie le numéro de série de l’ordinateur.


### <a name="SMSTSSetupRollback"></a> _SMSTSSetupRollback

 Spécifie si le programme d’installation Windows a effectué une opération de restauration pendant une mise à niveau sur place. Les valeurs des variables peuvent être `true` ou `false`.


### <a name="SMSTSSiteCode"></a> _SMSTSSiteCode

 Stocke le code du site Configuration Manager.

 #### <a name="example"></a>Exemple
 `ABC`


### <a name="SMSTSTimezone"></a> _SMSTSTimezone

 Cette variable stocke les informations de fuseau horaire au format suivant : 

 ```
 Bias,StandardBias,DaylightBias,StandardDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,DaylightDate.wYear,wMonth,wDayOfWeek,wDay,wHour,wMinute,wSecond,wMilliseconds,StandardName,DaylightName
 ```

 #### <a name="example"></a>Exemple
 Pour le fuseau horaire **Heure de la côte est (États-Unis et Canada)** : 

 ```
 300,0,-60,0,11,0,1,2,0,0,0,0,3,0,2,2,0,0,0,Eastern Standard Time,Eastern Daylight Time
 ```


### <a name="SMSTSType"></a> _SMSTSType

 Spécifie le type de séquence de tâches en cours d'exécution. Elle peut avoir l’une des valeurs suivantes :  

 - **1** : séquence de tâches générique
 - **2** : séquence de tâches du déploiement de système d’exploitation


### <a name="SMSTSUseCRL"></a> _SMSTSUseCRL

 Quand la séquence de tâches utilise HTTPS pour communiquer avec le point d’administration, cette variable spécifie si elle utilise la liste de révocation de certificats.


### <a name="SMSTSUserStarted"></a> _SMSTSUserStarted

 Spécifie si un utilisateur a démarré la séquence de tâches. Cette variable est définie uniquement si la séquence de tâches est démarrée à partir du Centre logiciel. Par exemple, si [_SMSTSLaunchMode](#SMSTSLaunchMode) est définie sur `SMS`. 

 Cette variable peut avoir les valeurs suivantes :  

 - `true` : spécifie que la séquence de tâches est démarrée manuellement par un utilisateur à partir du Centre logiciel.  

 - `false` : spécifie que la séquence de tâches est lancée automatiquement par le planificateur Configuration Manager.


### <a name="SMSTSUseSSL"></a> _SMSTSUseSSL

 Indique si la séquence de tâches utilise SSL pour communiquer avec le point de gestion Configuration Manager. Si vous configurez les systèmes de votre site pour le protocole HTTPS, la valeur est définie sur `true`.


### <a name="SMSTSUUID"></a> _SMSTSUUID

 *S’applique à l’étape [Définir des variables dynamiques](task-sequence-steps.md#BKMK_SetDynamicVariables).*

 Spécifie l’UUID de l’ordinateur.


### <a name="SMSTSWTG"></a> _SMSTSWTG

 spécifie si l'ordinateur s'exécute comme un appareil Windows Go To.


### <a name="TSAppInstallStatus"></a> _TSAppInstallStatus

 La séquence de tâches définit cette variable avec l’état d’installation de l’application lors de l’étape [Installer l’application](task-sequence-steps.md#BKMK_InstallApplication). Elle définit l’une des valeurs suivantes :  

 - **Non défini** : l’étape Installer l’application n’a pas été exécutée.  

 - **Erreur** : au moins une application a échoué en raison d’une erreur au cours de l’étape Installer l’application.  

 - **Avertissement** : aucune erreur ne s’est produite pendant l’étape Installer l’application. Une ou plusieurs applications, ou une dépendance nécessaire, n’ont pas été installées car une exigence n’était pas satisfaite.  

 - **Opération réussie** : aucune erreur ou avertissement n’a été détecté pendant l’étape Installer l’application.  


### <a name="OSDAdapter"></a> OSDAdapter

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Cette variable de séquence de tâches est une variable de *matrice*. Chaque élément de la matrice représente les paramètres d'une carte réseau de l'ordinateur. Accédez aux paramètres de chaque carte en combinant le nom de la variable de matrice avec l’index de carte réseau de base zéro et le nom de propriété.

 Si l’étape Appliquer les paramètres réseau configure plusieurs cartes réseau, elle définit les propriétés de la *deuxième* carte réseau à l’aide de l’index **1** dans le nom de variable. Par exemple : OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList et OSDAdapter1DNSDomain.

 Utilisez les noms de variables suivants afin de définir les propriétés de la *première* carte réseau pour l’étape afin de configurer :

#### <a name="osdadapter0enabledhcp"></a>OSDAdapter0EnableDHCP
 Ce paramètre est obligatoire. Les valeurs possibles sont `True` ou `False`. Par exemple :

 `true` : activer le protocole DHCP (Dynamic Host Configuration Protocol) de la carte

#### <a name="osdadapter0ipaddresslist"></a>OSDAdapter0IPAddressList
 Liste délimitée par des virgules des adresses IP de la carte. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur `false`. Ce paramètre est obligatoire.

#### <a name="osdadapter0subnetmask"></a>OSDAdapter0SubnetMask
 Liste délimitée par des virgules des masques de sous-réseaux. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur `false`. Ce paramètre est obligatoire.

#### <a name="osdadapter0gateways"></a>OSDAdapter0Gateways
 Liste délimitée par des virgules des adresses IP de passerelle. Cette propriété est ignorée sauf si **EnableDHCP** est réglé sur `false`. Ce paramètre est obligatoire.

#### <a name="osdadapter0dnsdomain"></a>OSDAdapter0DNSDomain
 Domaine DNS (Domain Name System) de la carte.

#### <a name="osdadapter0dnsserverlist"></a>OSDAdapter0DNSServerList
 Liste délimitée par des virgules des serveurs DNS de la carte. Ce paramètre est obligatoire.

#### <a name="osdadapter0enablednsregistration"></a>OSDAdapter0EnableDNSRegistration
 Définir sur `true` pour enregistrer l’adresse IP de la carte dans DNS.

#### <a name="osdadapter0enablefulldnsregistration"></a>OSDAdapter0EnableFullDNSRegistration
 Définir sur `true` pour enregistrer l’adresse IP de la carte dans DNS sous le nom DNS complet de l’ordinateur.

#### <a name="osdadapter0enableipprotocolfiltering"></a>OSDAdapter0EnableIPProtocolFiltering
 Définir sur `true` pour activer le filtrage de protocole IP sur la carte.

#### <a name="osdadapter0ipprotocolfilterlist"></a>OSDAdapter0IPProtocolFilterList
 Liste délimitée par des virgules des protocoles autorisés à s’exécuter sur IP. Cette propriété est ignorée si **EnableIPProtocolFiltering** est réglé sur `false`.

#### <a name="osdadapter0enabletcpfiltering"></a>OSDAdapter0EnableTCPFiltering
 Définir sur `true` pour activer le filtrage de port TCP sur la carte.

#### <a name="osdadapter0tcpfilterportlist"></a>OSDAdapter0TCPFilterPortList
 Liste délimitée par des virgules des ports auxquels les autorisations d’accès à TCP sont à accorder. Cette propriété est ignorée si **EnableTCPFiltering** est réglé sur `false`.

#### <a name="osdadapter0tcpipnetbiosoptions"></a>OSDAdapter0TcpipNetbiosOptions
 Options pour NetBIOS sur TCP/IP. Les valeurs possibles sont les suivantes :  

 - `0` : utiliser des paramètres NetBIOS du serveur DHCP  
 - `1` : Activer NetBIOS avec TCP/IP  
 - `2` : Désactiver NetBIOS avec TCP/IP  

#### <a name="osdadapter0enablewins"></a>OSDAdapter0EnableWINS
 Définir sur `true` afin d’utiliser WINS pour la résolution de noms.

#### <a name="osdadapter0winsserverlist"></a>OSDAdapter0WINSServerList
 Liste délimitée par des virgules des adresses IP du serveur WINS. Cette propriété est ignorée sauf si **EnableWINS** est réglé sur `true`.

#### <a name="osdadapter0macaddress"></a>OSDAdapter0MacAddress
 Adresse MAC (Media Access Controller) utilisée pour faire correspondre les paramètres à la carte réseau physique.

#### <a name="osdadapter0name"></a>OSDAdapter0Name
 Nom de la connexion réseau tel qu’il apparaît dans le programme Connexions réseau du Panneau de configuration. La longueur du nom est comprise entre 0 et 255 caractères.

#### <a name="osdadapter0index"></a>OSDAdapter0Index
 Index des paramètres de carte réseau dans le tableau des paramètres.

#### <a name="example"></a>Exemple
 - **OSDAdapterCount** = `1`  
 - **OSDAdapter0EnableDHCP** = `FALSE`  
 - **OSDAdapter0IPAddressList** = `192.168.0.40`  
 - **OSDAdapter0SubnetMask** = `255.255.255.0`  
 - **OSDAdapter0Gateways** = `192.168.0.1`  
 - **OSDAdapter0DNSSuffix** = `contoso.com`  


### <a name="OSDAdapterCount"></a> OSDAdapterCount

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie le nombre de cartes réseau installées sur l'ordinateur de destination. Quand la valeur **OSDAdapterCount** est définie, toutes les options de configuration de chaque carte doivent être définies. 

 Par exemple, si vous définissez la valeur **OSDAdapter0TCPIPNetbiosOptions** pour la première carte, vous devez configurer toutes les valeurs pour cette carte.

 Si vous ne spécifiez pas cette valeur, la séquence de tâches ignore toutes les valeurs **OSDAdapter**.


### <a name="OSDApplyDriverBootCriticalContentUniqueID"></a> OSDApplyDriverBootCriticalContentUniqueID

 *S’applique à l’étape [Appliquer le package de pilotes](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

 (entrée)

 Spécifie l'ID de contenu du pilote de périphérique de stockage de masse à installer à partir du package de pilotes. Si vous ne spécifiez pas cette variable, aucun pilote de stockage de masse n’est installé.


### <a name="OSDApplyDriverBootCriticalHardwareComponent"></a> OSDApplyDriverBootCriticalHardwareComponent

 *S’applique à l’étape [Appliquer le package de pilotes](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

 (entrée)

 Spécifie si un pilote de dispositif de stockage de masse est installé. Cette variable doit être de type **scsi**.

 Si [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) est défini, cette variable est requise.


### <a name="OSDApplyDriverBootCriticalID"></a> OSDApplyDriverBootCriticalID

 *S’applique à l’étape [Appliquer le package de pilotes](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

 (entrée)

 Spécifie l'ID critique de démarrage du pilote de périphérique de stockage de masse à installer. Cet ID apparaît dans la section **scsi** du fichier txtsetup.oem du pilote de dispositif.

 Si [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) est défini, cette variable est requise.

### <a name="OSDApplyDriverBootCriticalINFFile"></a> OSDApplyDriverBootCriticalINFFile

 *S’applique à l’étape [Appliquer le package de pilotes](task-sequence-steps.md#BKMK_ApplyDriverPackage).*

 (entrée)

 Spécifie le fichier INF du pilote de stockage de masse à installer.

 Si [OSDApplyDriverBootCriticalContentUniqueID](#OSDApplyDriverBootCriticalContentUniqueID) est défini, cette variable est requise.


### <a name="OSDAutoApplyDriverBestMatch"></a> OSDAutoApplyDriverBestMatch

 *S’applique à l’étape [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

 (entrée)

 S’il existe dans le catalogue de pilotes plusieurs pilotes de périphériques compatibles avec un périphérique matériel, cette variable détermine l’action de l’étape. 

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut) : installer uniquement le meilleur pilote de périphérique  

 - `false` : installe tous les pilotes de périphériques compatibles, et Windows choisit le meilleur pilote à utiliser  


### <a name="OSDAutoApplyDriverCategoryList"></a> OSDAutoApplyDriverCategoryList

 *S’applique à l’étape [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

 (entrée)

 Liste délimitée par des virgules des ID de catégorie uniques du catalogue de pilotes. L’étape **Appliquer automatiquement les pilotes** tient uniquement compte des pilotes figurant dans au moins l’une des catégories spécifiées. Cette valeur est facultative et n'est pas définie par défaut. Obtient les ID de catégorie disponibles par énumération de la liste des objets **SMS_CategoryInstance** sur le site.


### <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword

 *S’applique à l’étape [Activer BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

 (entrée)

 Au lieu de créer un mot de passe de récupération aléatoire, l’étape **Activer BitLocker** utilise la valeur spécifiée comme mot de passe de récupération. La valeur doit être un mot de passe de récupération numérique BitLocker valide.


### <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey

 *S’applique à l’étape [Activer BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).*

 (entrée)

 Au lieu de générer une clé de démarrage aléatoire pour l’option de gestion de clé **Clé de démarrage sur USB uniquement**, l’étape **Activer BitLocker** utilise le module de plateforme sécurisée (TPM) comme clé de démarrage. La valeur doit être une clé de démarrage BitLocker valide 256 bits codée en Base64.


### <a name="OSDCaptureAccount"></a> OSDCaptureAccount

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 (entrée)

 Spécifie un nom de compte Windows qui dispose d'autorisations pour stocker l'image capturée sur un partage réseau ([OSDCaptureDestination](#OSDCaptureDestination)). Spécifiez également [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).

 Pour plus d’informations sur le compte de capture de l’image du système d’exploitation, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#capture-operating-system-image-account).


### <a name="OSDCaptureAccountPassword"></a> OSDCaptureAccountPassword

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 (entrée)

 Spécifie le mot de passe du compte Windows ([OSDCaptureAccount](#OSDCaptureAccount)) employé pour le stockage de l'image capturée sur un partage réseau ([OSDCaptureDestination](#OSDCaptureDestination)).


### <a name="OSDCaptureDestination"></a> OSDCaptureDestination

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 (entrée)

 Spécifie l’emplacement où la séquence de tâches enregistre l’image du système d’exploitation capturée. Le nom du répertoire est limité à 255 caractères. Si le partage réseau nécessite une authentification, spécifiez les variables [OSDCaptureAccount](#OSDCaptureAccount) et [OSDCaptureAccountPassword](#OSDCaptureAccountPassword).


### <a name="OSDComputerName-input"></a> OSDComputerName (entrée)

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 Spécifie le nom de l'ordinateur de destination.

 #### <a name="example"></a>Exemple
 `%_SMSTSMachineName%` (valeur par défaut)


### <a name="OSDComputerName-output"></a> OSDComputerName (sortie)

 *S’applique à l’étape [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

 Défini sur le nom NetBIOS de l'ordinateur. La valeur est définie uniquement si la variable [OSDMigrateComputerName](#OSDMigrateComputerName) est définie sur `true`.


### <a name="OSDConfigFileName"></a> OSDConfigFileName

 *S’applique à l’étape [Appliquer l’image du système d’exploitation](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

 (entrée)

 Spécifie le nom du fichier de réponse de déploiement du système d'exploitation associé au package de l’image du déploiement du système d'exploitation.  


### <a name="OSDDataImageIndex"></a> OSDDataImageIndex

 *S’applique à l’étape [Appliquer l’image de données](task-sequence-steps.md#BKMK_ApplyDataImage).*

 (entrée)

 Spécifie la valeur d'index de l'image qui est appliquée à l'ordinateur de destination.


### <a name="OSDDiskIndex"></a> OSDDiskIndex

 *S’applique à l’étape [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

 (entrée)

 Spécifie le nombre de disques physiques à partitionner.


### <a name="OSDDNSDomain"></a> OSDDNSDomain

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie le serveur DNS principal utilisé sur l'ordinateur de destination.


### <a name="OSDDNSSuffixSearchOrder"></a> OSDDNSSuffixSearchOrder

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie l'ordre de recherche DNS de l'ordinateur de destination.


### <a name="OSDDomainName"></a> OSDDomainName

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie le nom du domaine Active Directory auquel l’ordinateur de destination se joint. La valeur spécifiée doit être un nom de domaine de services de domaine Active Directory valide.


### <a name="OSDDomainOUName"></a> OSDDomainOUName

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie le format du nom RFC 1779 de l'unité d'organisation que l'ordinateur de destination joint. S'il est spécifié, la valeur doit contenir le chemin complet.

 #### <a name="example"></a>Exemple
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`


### <a name="OSDDoNotLogCommand"></a> OSDDoNotLogCommand
 <!--1358493--> *À partir de la version 1806*  
 *S’applique à l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine).*

 (entrée)

 Pour empêcher l’affichage ou la journalisation de données potentiellement sensibles, définissez cette variable sur `TRUE`. Cette variable masque le nom du programme dans le fichier **smsts.log** au cours de l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) d’une séquence de tâches.   


### <a name="OSDEnableTCPIPFiltering"></a> OSDEnableTCPIPFiltering

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie si le filtrage TCP/IP est activé.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false` (valeur par défaut)  


### <a name="OSDGPTBootDisk"></a> OSDGPTBootDisk

 *S’applique à l’étape [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

 (entrée)

 Spécifie s’il faut créer une partition EFI sur un disque dur GPT. Les ordinateurs EFI utilisent cette partition en tant que disque de démarrage.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false` (valeur par défaut)


### <a name="OSDImageCreator"></a> OSDImageCreator

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 (entrée)

 Nom facultatif de l'utilisateur qui a créé l'image. Ce nom est stocké dans le fichier WIM. Le nom de l'utilisateur est limité à 255 caractères.


### <a name="OSDImageDescription"></a> OSDImageDescription

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 (entrée)

 Description facultative définie par l'utilisateur de l’image du système d’exploitation capturée. Cette description est stockée dans le fichier WIM. La description est limitée à 255 caractères.


### <a name="OSDImageIndex"></a> OSDImageIndex

 *S’applique à l’étape [Appliquer l’image du système d’exploitation](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

 (entrée)

 Spécifie la valeur d'index de l'image du fichier WIM qui est appliqué à l'ordinateur de destination.


### <a name="OSDImageVersion"></a> OSDImageVersion

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 (entrée)

 Numéro de version facultatif défini par l'utilisateur à attribuer à l'image du système d'exploitation capturée. Ce numéro de version est stocké dans le fichier WIM. Cette valeur peut être n'importe quelle combinaison de caractères alphanumériques avec une longueur maximale de 32 caractères.


### <a name="OSDInstallDriversAdditionalOptions"></a> OSDInstallDriversAdditionalOptions
<!--516679/2840016--> *À partir de la version 1806*  
 *S’applique à l’étape [Appliquer le package de pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage).*

 (entrée)

 Spécifie des options supplémentaires à ajouter à la ligne de commande DISM lors de l’application d’un package de pilotes. La séquence de tâches ne vérifie pas les options de ligne de commande. 

 Pour utiliser cette variable, activez le paramètre, **Installer le package de pilotes en exécutant DISM avec l’option recurse**, de l’étape **Appliquer le package de pilotes**. 

 Pour plus d’informations, consultez [Options de ligne de commande Windows 10 DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/deployment-image-servicing-and-management--dism--command-line-options).


### <a name="OSDJoinAccount"></a> OSDJoinAccount

 *S’applique aux étapes suivantes :*  
 - [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings)   
 - [Joindre un domaine ou un groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (entrée)

 Spécifie le compte utilisateur du domaine utilisé pour ajouter l'ordinateur de destination au domaine. Cette variable est requise lors de la jonction à un domaine.

 Pour plus d'informations sur le compte de jonction de domaine de la séquence de tâches, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-domain-joining-account).


### <a name="OSDJoinDomainName"></a> OSDJoinDomainName

 *S’applique à l’étape [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

 (entrée)

 Spécifie le nom d’un domaine Active Directory auquel l’ordinateur de destination se joint. Le nom de domaine doit comprendre entre 1 et 255 caractères.


### <a name="OSDJoinDomainOUName"></a> OSDJoinDomainOUName

 *S’applique à l’étape [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

 (entrée)

 Spécifie le format du nom RFC 1779 de l'unité d'organisation que l'ordinateur de destination joint. S'il est spécifié, la valeur doit contenir le chemin complet. Le nom de l’unité d’organisation doit comprendre entre 0 et 32 767 caractères. Cette valeur n’est pas définie si la variable [OSDJoinType](#OSDJoinType) est `1` (joindre le groupe de travail).

 #### <a name="example"></a>Exemple
 `LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com`  

  
### <a name="OSDJoinPassword"></a> OSDJoinPassword

 *S’applique aux étapes suivantes :*  
 - [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  
 - [Joindre un domaine ou un groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)  


 (entrée)

 Spécifie le mot de passe pour [OSDJoinAccount](#OSDJoinAccount) utilisé par l’ordinateur de destination pour se joindre au domaine Active Directory. Si l’environnement de séquence de tâches n’inclut pas cette variable, le programme d’installation de Windows essaie d’utiliser un mot de passe vide. Si la variable [OSDJoinType](#OSDJoinType) est définie sur `0` (joindre le domaine), cette valeur est obligatoire.


### <a name="OSDJoinSkipReboot"></a> OSDJoinSkipReboot

 *S’applique à l’étape [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

 (entrée)

 Spécifie s'il faut ignorer le redémarrage après que l'ordinateur de destination joint le domaine ou le groupe de travail.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false`  


### <a name="OSDJoinType"></a> OSDJoinType

 *S’applique à l’étape [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

 (entrée)

 Spécifie si l'ordinateur de destination se joint à un domaine Windows ou un groupe de travail. 

 #### <a name="valid-values"></a>Valeurs valides
 - `0` : joindre l’ordinateur de destination à un domaine Windows  
 - `1` : joindre l’ordinateur de destination à un groupe de travail  


### <a name="OSDJoinWorkgroupName"></a> OSDJoinWorkgroupName

 *S’applique à l’étape [Joindre le domaine ou le groupe de travail](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).*

 (entrée)

 Spécifie le nom d'un groupe de travail auquel l'ordinateur de destination se joint. Le nom de groupe de travail doit comprendre entre 1 et 32 caractères.


### <a name="OSDKeepActivation"></a> OSDKeepActivation

 *S’applique à l’étape [Préparer de Windows pour capture](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

 (entrée)

 Spécifie si sysprep réinitialise l'indicateur d'activation du produit.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`
 - `false` (valeur par défaut)


### <a name="OSDLocalAdminPassword"></a> OSDLocalAdminPassword

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 (entrée)

 Spécifie le mot de passe du compte Administrateur local. Si vous activez l’option **Générer de façon aléatoire le mot de passe de l’administrateur local et désactiver le compte sur toutes les plates-formes prises en charge**, l’étape ignore cette variable. La valeur spécifiée doit comprendre entre 1 et 255 caractères.


### <a name="OSDMigrateAdapterSettings"></a> OSDMigrateAdapterSettings

 *S’applique à l’étape [Capturer les paramètres réseau](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

 (entrée)

 Spécifie si la séquence de tâches capture les informations de la carte réseau. Ces informations incluent les paramètres de configuration pour TCP/IP, DNS et WINS.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut)
 - `false`


### <a name="OSDMigrateAdditionalCaptureOptions"></a> OSDMigrateAdditionalCaptureOptions

 *S’applique à l’étape [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).*

 (entrée)

 Spécifiez des options de ligne de commande supplémentaires pour l’outil de migration de l’état utilisateur (USMT) utilisées par la séquence de tâches pour capturer l’état utilisateur. L’étape n’expose pas ces paramètres dans l’éditeur de séquence de tâches. Spécifiez ces options sous forme de chaîne, que la séquence de tâches ajoute à la ligne de commande USMT générée automatiquement pour ScanState.

 La précision des options USMT spécifiées avec cette variable de séquence de tâches n'est pas validée avant l'exécution de la séquence de tâches.

 Pour plus d’informations sur les options disponibles, consultez [Syntaxe ScanState](https://docs.microsoft.com/windows/deployment/usmt/usmt-scanstate-syntax).


### <a name="OSDMigrateAdditionalRestoreOptions"></a> OSDMigrateAdditionalRestoreOptions

 *S’applique à l’étape [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).*

 (entrée)

 Spécifiez des options de ligne de commande supplémentaires pour l’outil de migration de l’état utilisateur (USMT) utilisées par la séquence de tâches pour restaurer l’état utilisateur. Spécifiez les options supplémentaires sous forme de chaîne, que la séquence de tâches ajoute à la ligne de commande USMT générée automatiquement pour LoadState. 

 La précision des options USMT spécifiées avec cette variable de séquence de tâches n'est pas validée avant l'exécution de la séquence de tâches.

 Pour plus d’informations sur les options disponibles, consultez [Syntaxe LoadState](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).


### <a name="OSDMigrateComputerName"></a> OSDMigrateComputerName

 *S’applique à l’étape [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

 (entrée)

 Spécifie si le nom de l'ordinateur est migré.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut). La variable [OSDComputerName (sortie)](#OSDComputerName-output) est définie sur le nom NetBIOS de l’ordinateur.  
 - `false`   


### <a name="OSDMigrateConfigFiles"></a> OSDMigrateConfigFiles

 *S’applique à l’étape [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).*

 (entrée)

 Spécifie les fichiers de configuration employés pour contrôler la capture des profils utilisateur. Cette variable est utilisée uniquement si [OSDMigrateMode](#OSDMigrateMode) a la valeur `Advanced`. Cette valeur de liste délimitée par des virgules est définie pour effectuer une migration du profil utilisateur personnalisée.

 #### <a name="example"></a>Exemple
 `miguser.xml,migsys.xml,migapps.xml`  


### <a name="OSDMigrateContinueOnLockedFiles"></a> OSDMigrateContinueOnLockedFiles

 *S’applique à l’étape [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).*

 (entrée)

 Si USMT ne peut pas capturer certains fichiers, cette variable permet à la capture de l’état utilisateur de se poursuivre. 

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut)  
 - `false`   


### <a name="OSDMigrateContinueOnRestore"></a> OSDMigrateContinueOnRestore

 *S’applique à l’étape [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).*

 (entrée)

 Poursuivez le processus, même si l’outil USMT ne peut pas restaurer certains fichiers.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut)  
 - `false`  


### <a name="OSDMigrateEnableVerboseLogging"></a> OSDMigrateEnableVerboseLogging

 *S’applique aux étapes suivantes :*  
 - [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState)  


 (entrée)

 Active la journalisation documentée pour USMT. L’étape requiert cette valeur.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false` (valeur par défaut)  


### <a name="OSDMigrateLocalAccounts"></a> OSDMigrateLocalAccounts

 *S’applique à l’étape [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).*

 (entrée)

 Indique si le compte d'ordinateur local est restauré.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false` (valeur par défaut)  


### <a name="OSDMigrateLocalAccountPassword"></a> OSDMigrateLocalAccountPassword

 *S’applique à l’étape [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState).*

 (entrée)

 Si la variable [OSDMigrateLocalAccounts](#OSDMigrateLocalAccounts) a la valeur `true`, cette variable doit contenir le mot de passe affecté à *tous* les comptes locaux migrés. USMT attribue le même mot de passe à tous les comptes locaux migrés. Considérez ce mot de passe comme temporaire et changez-le ultérieurement à l’aide d’une autre méthode.


### <a name="OSDMigrateMode"></a> OSDMigrateMode

 *S’applique à l’étape [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).*

 (entrée)

 Permet de personnaliser les fichiers capturés par USMT. 

 #### <a name="valid-values"></a>Valeurs valides
 - `Simple` : la séquence de tâches utilise seulement les fichiers de configuration USMT standard  

 - `Advanced` : la variable de séquence de tâches [OSDMigrateConfigFiles](#OSDMigrateConfigFiles) spécifie les fichiers de configuration utilisés par USTM  


### <a name="OSDMigrateNetworkMembership"></a> OSDMigrateNetworkMembership

 *S’applique à l’étape [Capturer les paramètres réseau](task-sequence-steps.md#BKMK_CaptureNetworkSettings).*

 (entrée)

 Spécifie si la séquence de tâches migre les informations d’appartenance au groupe de travail ou au domaine.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut)
 - `false`


### <a name="OSDMigrateRegistrationInfo"></a> OSDMigrateRegistrationInfo

 *S’applique à l’étape [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

 (entrée)

 Spécifie si l’étape migre les informations sur l’utilisateur et l’organisation.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut). La variable [OSDRegisteredOrgName (sortie)](#OSDRegisteredOrgName-output) prend le nom d’organisation inscrit de l’ordinateur.  
 - `false`   


### <a name="OSDMigrateSkipEncryptedFiles"></a> OSDMigrateSkipEncryptedFiles

 *S’applique à l’étape [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState).*

 (entrée)

 Spécifie si les fichiers cryptés sont capturés.

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false` (valeur par défaut)  


### <a name="OSDMigrateTimeZone"></a> OSDMigrateTimeZone

 *S’applique à l’étape [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

 (entrée)

 Spécifie si le fuseau horaire de l'ordinateur est migré.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut). La variable [OSDTimeZone (sortie)](#OSDTimeZone-output) est définie sur le fuseau horaire de l’ordinateur.  
 - `false`   


### <a name="OSDNetworkJoinType"></a> OSDNetworkJoinType

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie si l'ordinateur de destination se joint à un domaine Active Directory ou un groupe de travail.

 #### <a name="value-values"></a>Valeurs
 - `0` : rejoindre un domaine Active Directory  
 - `1` : Joindre un groupe de travail


### <a name="OSDPartitions"></a> OSDPartitions

 *S’applique à l’étape [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

 (entrée)

 Cette variable de séquence de tâches est une variable de matrice des paramètres de partition. Chaque élément de la matrice représente les paramètres d'une partition simple sur le disque dur. Accédez aux paramètres définis pour chaque partition en combinant le nom de la variable de matrice avec le numéro de partition de disque de base zéro et le nom de propriété.

Utilisez les noms de variables suivants pour définir les propriétés de la *première* partition créée sur le disque dur par cette étape :

 #### <a name="osdpartitions0type"></a>OSDPartitions0Type
 Indique le type de partition. Cette propriété est obligatoire. Les valeurs valides sont `Primary`, `Extended`, `Logical` et `Hidden`.

 #### <a name="osdpartitions0filesystem"></a>OSDPartitions0FileSystem
 Indique le type de système de fichiers à utiliser lors du formatage de la partition. Cette propriété est facultative. Si vous ne spécifiez pas de système de fichiers, l’étape ne formate pas la partition. Les valeurs valides sont `FAT32` et `NTFS`.

 #### <a name="osdpartitions0bootable"></a>OSDPartitions0Bootable
 Indique si la partition est amorçable. Cette propriété est obligatoire. Si cette valeur est définie sur `TRUE` pour les disques MBR, l’étape marque cette partition comme active.

 #### <a name="osdpartitions0quickformat"></a>OSDPartitions0QuickFormat
 Indique le type de format utilisé. Cette propriété est obligatoire. Si cette valeur est définie sur `TRUE`, l’étape effectue un formatage rapide. Sinon, l’étape effectue un formatage complet.

 #### <a name="osdpartitions0volumename"></a>OSDPartitions0VolumeName
 Indique le nom attribué au volume après formatage. Cette propriété est facultative.

 #### <a name="osdpartitions0size"></a>OSDPartitions0Size
 Indique la taille de la partition. Cette propriété est facultative. Si cette propriété n'est pas spécifiée, la partition est créée en utilisant la totalité de l'espace disque disponible. Les unités sont spécifiées par la variable **OSDPartitions0SizeUnits** .

 #### <a name="osdpartitions0sizeunits"></a>OSDPartitions0SizeUnits
 L’étape utilise ces unités pour interpréter la variable **OSDPartitions0Size**. Cette propriété est facultative. Les valeurs valides sont `MB` (valeur par défaut), `GB` et `Percent`.

 #### <a name="osdpartitions0volumelettervariable"></a>OSDPartitions0VolumeLetterVariable
 Quand cette étape crée des partitions, elle utilise toujours la lettre de lecteur disponible suivante dans Windows PE. Utilisez cette propriété facultative pour spécifier le nom d’une autre variable de séquence de tâches. L’étape utilise cette variable afin d’enregistrer la nouvelle lettre de lecteur pour référence ultérieure.

 Si vous définissez plusieurs partitions avec cette étape de séquence de tâches, les propriétés de la *deuxième* partition sont définies en utilisant l’index **1** dans le nom de variable. Par exemple : **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat** et **OSDPartitions1VolumeName**.


### <a name="OSDPartitionStyle"></a> OSDPartitionStyle

 *S’applique à l’étape [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk).*

 (entrée)

 Spécifie le style de partition à utiliser lors du partitionnement du disque. 

 #### <a name="valid-values"></a>Valeurs valides
 - `GPT` : utiliser le style de la table de partition GUID
 - `MBR` : utiliser le style de partition à enregistrement de démarrage principal


### <a name="OSDProductKey"></a> OSDProductKey

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 (entrée)

 Spécifie la clé de produit Windows. La valeur spécifiée doit comprendre entre 1 et 255 caractères.


### <a name="OSDRandomAdminPassword"></a> OSDRandomAdminPassword

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 (entrée)

 Spécifie un mot de passe généré de manière aléatoire pour le compte de l'administrateur local dans le nouveau système d'exploitation. 

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut) : le programme d’installation de Windows désactive le compte d’administrateur local sur l’ordinateur cible  

 - `false` : le programme d’installation de Windows active le compte d’administrateur local sur l’ordinateur cible et affecte comme mot de passe la valeur de [OSDLocalAdminPassword](#OSDLocalAdminPassword)  


### <a name="OSDRegisteredOrgName-input"></a> OSDRegisteredOrgName (entrée)

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 Spécifie le nom d'organisation inscrit par défaut dans le nouveau système d'exploitation. La valeur spécifiée doit comprendre entre 1 et 255 caractères.


### <a name="OSDRegisteredOrgName-output"></a> OSDRegisteredOrgName (sortie)

 *S’applique à l’étape [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

 Défini sur le nom d'organisation inscrit de l'ordinateur. La valeur est définie uniquement si la variable [OSDMigrateRegistrationInfo](#OSDMigrateRegistrationInfo) est définie sur `true`.


### <a name="OSDRegisteredUserName"></a> OSDRegisteredUserName

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 (entrée)

 Spécifie le nom d'utilisateur inscrit par défaut dans le nouveau système d'exploitation. La valeur spécifiée doit comprendre entre 1 et 255 caractères.


### <a name="OSDServerLicenseConnectionLimit"></a> OSDServerLicenseConnectionLimit

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 (entrée)

 Spécifie le nombre maximal de connexions autorisées. Le nombre spécifié doit comprendre entre 5 et 9 999 connexions.


### <a name="OSDServerLicenseMode"></a> OSDServerLicenseMode

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 (entrée)

 Spécifie le mode de licence Windows Server utilisé.

 #### <a name="valid-values"></a>Valeurs valides
 - `PerSeat`
 - `PerServer`


### <a name="OSDSetupAdditionalUpgradeOptions"></a> OSDSetupAdditionalUpgradeOptions

 *S’applique à l’étape [Mise à niveau du système d’exploitation](task-sequence-steps.md#BKMK_UpgradeOS).*

 (entrée)

 Spécifie les options de ligne de commande supplémentaires qui sont ajoutées au programme d’installation de Windows durant une mise à niveau Windows 10. La séquence de tâches ne vérifie pas les options de ligne de commande. 

 Pour plus d’informations, consultez [Options de ligne de commande du programme d’installation de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options).


### <a name="OSDStateFallbackToNAA"></a> OSDStateFallbackToNAA

 *S’applique à l’étape [Demander le magasin d'état](task-sequence-steps.md#BKMK_RequestStateStore).*

 (entrée)

 Quand le compte d’ordinateur ne parvient pas à se connecter au point de migration de l’état, cette variable spécifie si la séquence de tâches doit utiliser le compte d’accès réseau. 

 Pour plus d'informations sur le compte d'accès réseau, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#network-access-account).

 #### <a name="valid-values"></a>Valeurs valides
 - `true`  
 - `false` (valeur par défaut)  


### <a name="OSDStateSMPRetryCount"></a> OSDStateSMPRetryCount

 *S’applique à l’étape [Demander le magasin d'état](task-sequence-steps.md#BKMK_RequestStateStore).*

 (entrée)

 Spécifie le nombre de tentatives de recherche d'un point de migration d'état par l'étape de la séquence de tâches avant d'abandonner. Le nombre spécifié doit être compris entre 0 et 600.


### <a name="OSDStateSMPRetryTime"></a> OSDStateSMPRetryTime

 *S’applique à l’étape [Demander le magasin d'état](task-sequence-steps.md#BKMK_RequestStateStore).*

 (entrée)

 Indique la durée en secondes pendant laquelle l'étape de la séquence de tâches attend entre chaque tentative. Le nombre de secondes est limité à 30 caractères.


### <a name="OSDStateStorePath"></a> OSDStateStorePath

 *S’applique aux étapes suivantes :*  
 - [Capturer l’état utilisateur](task-sequence-steps.md#BKMK_CaptureUserState)  
 - [Libérer le magasin d’état](task-sequence-steps.md#BKMK_ReleaseStateStore)  
 - [Demander le magasin d’état](task-sequence-steps.md#BKMK_RequestStateStore)  
 - [Restaurer l’état utilisateur](task-sequence-steps.md#BKMK_RestoreUserState)  


 (entrée)

 Le partage réseau ou le nom de chemin d’accès local du dossier où la séquence de tâches enregistre ou restaure l’état utilisateur. Il n’y a pas de valeur par défaut.


### <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive

 *S’applique à l’étape [Appliquer l’image du système d’exploitation](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).*

 (sortie)

 Indique la lettre de lecteur de la partition contenant les fichiers du système d'exploitation une fois l’image appliquée.


### <a name="OSDTargetSystemRoot-input"></a> OSDTargetSystemRoot (entrée)

 *S’applique à l’étape [Capturer l’image du système d’exploitation](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).*

 Spécifie le chemin du répertoire Windows où a été installé le système d'exploitation sur l'ordinateur de référence. La séquence de tâches le vérifie comme un système d’exploitation pris en charge pour la capture par Configuration Manager.


### <a name="OSDTargetSystemRoot-output"></a> OSDTargetSystemRoot (sortie)

 *S’applique à l’étape [Préparer de Windows pour capture](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).*

 Spécifie le chemin du répertoire Windows où a été installé le système d'exploitation sur l'ordinateur de référence. La séquence de tâches le vérifie comme un système d’exploitation pris en charge pour la capture par Configuration Manager.


### <a name="OSDTimeZone-input"></a> OSDTimeZone (input)

 *S’applique à l’étape [Appliquer les paramètres Windows](task-sequence-steps.md#BKMK_ApplyWindowsSettings).*

 Spécifie le paramètre de fuseau horaire par défaut utilisé dans le nouveau système d'exploitation.


### <a name="OSDTimeZone-output"></a> OSDTimeZone (sortie)

 *S’applique à l’étape [Capturer les paramètres Windows](task-sequence-steps.md#BKMK_CaptureWindowsSettings).*

 Défini sur le fuseau horaire de l'ordinateur. La valeur est définie uniquement si la variable [OSDMigrateTimeZone](#OSDMigrateTimeZone) est définie sur `true`.


### <a name="OSDWipeDestinationPartition"></a> OSDWipeDestinationPartition

 *S’applique à l’étape [Appliquer l’image de données](task-sequence-steps.md#BKMK_ApplyDataImage).*

 (entrée)

 Spécifie s'il faut supprimer les fichiers situés sur la partition de destination.

 #### <a name="valid-values"></a>Valeurs valides
 - `true` (valeur par défaut)
 - `false`


### <a name="OSDWorkgroupName"></a> OSDWorkgroupName

 *S’applique à l’étape [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings).*

 (entrée)

 Spécifie le nom du groupe de travail auquel l'ordinateur de destination se joint.

 Spécifiez cette variable ou la variable [OSDDomainName](#OSDDomainName). Le nom du groupe de travail est limité à 32 caractères. 


### <a name="SMSClientInstallProperties"></a> SMSClientInstallProperties

 *S’applique à l’étape [Configurer Windows et ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).*

 (entrée)

 Spécifie les propriétés d’installation de client qui sont utilisées par la séquence de tâches pendant l’installation du client Configuration Manager.

 Pour plus d’informations, consultez [À propos des propriétés et des paramètres d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="SMSConnectNetworkFolderAccount"></a> SMSConnectNetworkFolderAccount

 *S’applique à l’étape [Se connecter à un dossier réseau](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

 (entrée)

 Spécifie le compte utilisateur utilisé pour se connecter au partage réseau dans [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). Spécifiez le mot de passe du compte avec la valeur [SMSConnectNetworkFolderPassword](#SMSConnectNetworkFolderPassword).

 Pour plus d'informations sur le compte de connexion à un dossier réseau de la séquence de tâches, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#task-sequence-editor-network-folder-connection-account).


### <a name="SMSConnectNetworkFolderDriveLetter"></a> SMSConnectNetworkFolderDriveLetter

 *S’applique à l’étape [Se connecter à un dossier réseau](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

 (entrée)

 Spécifie la lettre de lecteur réseau à laquelle se connecter. Cette valeur est facultative. Si vous ne la spécifiez pas, la connexion réseau doit alors être mappée à une lettre de lecteur. Si cette valeur est spécifiée, la valeur doit être comprise dans la plage allant de D à Z. N’utilisez pas X, c’est la lettre de lecteur utilisée par Windows PE pendant la phase Windows PE.

 #### <a name="examples"></a>Exemples
 - `D:`  
 - `E:`  


### <a name="SMSConnectNetworkFolderPassword"></a> SMSConnectNetworkFolderPassword

 *S’applique à l’étape [Se connecter à un dossier réseau](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

 (entrée)

 Spécifie le mot de passe de [SMSConnectNetworkFolderAccount](#SMSConnectNetworkFolderAccount) utilisé pour la connexion au partage réseau dans [SMSConnectNetworkFolderPath](#SMSConnectNetworkFolderPath). 


### <a name="SMSConnectNetworkFolderPath"></a> SMSConnectNetworkFolderPath

 *S’applique à l’étape [Se connecter à un dossier réseau](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).*

 (entrée)

 Spécifie le chemin d'accès réseau pour la connexion. Si vous avez besoin de mapper ce chemin d’accès à une lettre de lecteur, utilisez la valeur [SMSConnectNetworkFolderDriveLetter](#SMSConnectNetworkFolderDriveLetter).

 #### <a name="example"></a>Exemple
 `\\server\share`


### <a name="SMSInstallUpdateTarget"></a> SMSInstallUpdateTarget

 *S’applique à l’étape [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

 (entrée)

 Spécifie s'il faut installer toutes les mises à jour ou uniquement les mises à jour obligatoires.

 #### <a name="valid-values"></a>Valeurs valides
 - `All`  
 - `Mandatory`  


### <a name="SMSRebootMessage"></a> SMSRebootMessage

 *S’applique à l’étape [Redémarrer l’ordinateur](task-sequence-steps.md#BKMK_RestartComputer).*

 (entrée)

 Indique le message à afficher aux utilisateurs avant le redémarrage de l'ordinateur de destination. Si vous ne définissez pas cette variable, le texte par défaut est affiché. Le message spécifié ne doit pas dépasser 512 caractères.

 #### <a name="example"></a>Exemple
 `Save your work before the computer restarts.`  


### <a name="SMSRebootTimeout"></a> SMSRebootTimeout

 *S’applique à l’étape [Redémarrer l’ordinateur](task-sequence-steps.md#BKMK_RestartComputer).*

 (entrée)

 Spécifie le nombre de secondes pendant lesquelles l'avertissement est affiché à l'attention de l'utilisateur avant le redémarrage de l'ordinateur. 

 #### <a name="examples"></a>Exemples
 - `0` (valeur par défaut) : ne pas afficher un message de redémarrage  
 - `60` : afficher l’avertissement pendant une minute  


### <a name="SMSTSAssignmentsDownloadInterval"></a> SMSTSAssignmentsDownloadInterval

 Délai d’attente (exprimé en secondes) du client entre deux tentatives de téléchargement de la stratégie quand la tentative précédente n’a retourné aucune stratégie. Par défaut, le client attend **0** seconde avant une nouvelle tentative. 

 Cette variable peut être définie à l'aide d'une commande de prédémarrage à partir du média ou de l'environnement PXE.


### <a name="SMSTSAssignmentsDownloadRetry"></a> SMSTSAssignmentsDownloadRetry

 Nombre de tentatives de téléchargement de la stratégie par un client quand aucune stratégie n’est trouvée à la première tentative. Par défaut, le client effectue **0** nouvelle tentative.

 Cette variable peut être définie à l'aide d'une commande de prédémarrage à partir du média ou de l'environnement PXE.


### <a name="SMSTSAssignUsersMode"></a> SMSTSAssignUsersMode

 Spécifie la façon dont une séquence de tâches associe des utilisateurs à l'ordinateur de destination. Définissez la variable sur l'une des valeurs suivantes :  

 - **Auto** : quand la séquence de tâches déploie le système d’exploitation sur l’ordinateur de destination, elle crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination.  

 - **En attente** : la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination. Un administrateur doit approuver la relation pour la définir.  

 - **Disabled** : la séquence de tâches n’associe pas d’utilisateurs à l’ordinateur de destination pendant le déploiement du système d’exploitation.


### <a name="SMSTSDisableStatusRetry"></a> SMSTSDisableStatusRetry
 <!--512358--> Dans les scénarios déconnectés, le moteur de séquence de tâches tente à plusieurs reprises d’envoyer des messages d’état au point de gestion. Dans ce scénario, ce comportement entraîne des retards dans le traitement des séquences de tâches. 

 À compter de la version 1802, définissez cette variable sur `true` pour que le moteur de séquence de tâches ne tente pas d’envoyer des messages d’état si l’envoi du premier message a échoué. Cette première tentative inclut plusieurs nouvelles tentatives.

 Lorsque la séquence de tâches redémarre, la valeur de cette variable persiste. Toutefois, la séquence de tâches tente d’envoyer un premier message d’état. Cette première tentative inclut plusieurs nouvelles tentatives. En cas de réussite, la séquence de tâches continue à envoyer l’état indépendamment de la valeur de cette variable. Si l’envoi de l’état échoue, la séquence de tâches utilise la valeur de cette variable.

 > [!NOTE]  
 > Le [rapport d’état de la séquence de tâches](/sccm/core/servers/manage/list-of-reports#task-sequence---deployment-status) se base sur ces messages d’état pour montrer la progression, l’historique et les détails de chaque étape.


### <a name="SMSTSDisableWow64Redirection"></a> SMSTSDisableWow64Redirection

 *S’applique à l’étape [Exécuter la ligne de commande](task-sequence-steps.md#BKMK_RunCommandLine).*

 (entrée)

 Par défaut sur un système d’exploitation 64 bits, la séquence de tâches recherche et exécute le programme sur la ligne de commande à l’aide du redirecteur du système de fichiers WOW64. Ce comportement permet à la commande de trouver les versions 32 bits des DLL et des programmes de système d’exploitation. L’affectation de la valeur `true` à cette variable désactive l’utilisation du redirecteur de système de fichiers WOW64. La commande recherche les versions 64 bits natives des DLL et des programmes de système d’exploitation. Cette variable est sans effet sous un système d'exploitation 32 bits.


### <a name="SMSTSDownloadAbortCode"></a> SMSTSDownloadAbortCode

 Cette variable contient la valeur du code d’abandon pour le téléchargeur du programme externe. Ce programme est spécifié dans la variable [SMSTSDownloadProgram](#SMSTSDownloadProgram). Si le programme retourne un code d’erreur égal à la valeur de la variable SMSTSDownloadAbortCode, le téléchargement du contenu échoue et aucune autre méthode de téléchargement n’est tentée.


### <a name="SMSTSDownloadProgram"></a> SMSTSDownloadProgram

 Utilisez cette variable pour spécifier un autre fournisseur de contenu (ACP). Un ACP est un programme téléchargeur qui est utilisé pour télécharger du contenu. La séquence de tâches utilise ACP au lieu du téléchargeur Configuration Manager par défaut. Dans le cadre du processus de téléchargement de contenu, la séquence de tâches examine cette variable. Si elle est spécifiée, la séquence de tâches exécute le programme pour télécharger le contenu.


### <a name="SMSTSDownloadRetryCount"></a> SMSTSDownloadRetryCount

 Nombre de fois que Configuration Manager tente de télécharger du contenu à partir d’un point de distribution. Par défaut, le client effectue **2** nouvelles tentatives.


### <a name="SMSTSDownloadRetryDelay"></a> SMSTSDownloadRetryDelay

 Délai d’attente de Configuration Manager (en secondes) avant qu’il tente à nouveau de télécharger du contenu à partir d’un point de distribution. Par défaut, le client attend **15** secondes avant une nouvelle tentative.


### <a name="SMSTSDriverRequestConnectTimeOut"></a> SMSTSDriverRequestConnectTimeOut

 *S’applique à l’étape [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

 Lors de la demande du catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend la connexion au serveur HTTP. Si la connexion prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **60** secondes.


### <a name="SMSTSDriverRequestReceiveTimeOut"></a> SMSTSDriverRequestReceiveTimeOut

 *S’applique à l’étape [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

 Lors de la demande du catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend une réponse. Si la connexion prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **480** secondes.


### <a name="SMSTSDriverRequestResolveTimeOut"></a> SMSTSDriverRequestResolveTimeOut

 *S’applique à l’étape [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

 Lors de la demande du catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend la résolution de noms HTTP. Si la connexion prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **60** secondes.


### <a name="SMSTSDriverRequestSendTimeOut"></a> SMSTSDriverRequestSendTimeOut

 *S’applique à l’étape [Appliquer automatiquement les pilotes](task-sequence-steps.md#BKMK_AutoApplyDrivers).*

 Lors de l’envoi d’une demande de catalogue de pilotes, cette variable correspond au nombre de secondes pendant lesquelles la séquence de tâches attend avant d’envoyer la demande. Si la demande prend plus de temps que le paramètre de délai d’attente, la séquence de tâches annule la demande. Par défaut, le délai d’attente est de **60** secondes.


### <a name="SMSTSErrorDialogTimeout"></a> SMSTSErrorDialogTimeout

 Quand une erreur se produit dans une séquence de tâches, elle affiche une boîte de dialogue avec l’erreur. La séquence de tâches la fait disparaître automatiquement après le nombre de secondes spécifié par cette variable. La valeur par défaut est **900** secondes (15 minutes).


### <a name="SMSTSLanguageFolder"></a> SMSTSLanguageFolder

 utilisez cette variable pour modifier la langue d'affichage d'une image de démarrage indépendante de la langue.


### <a name="SMSTSLocalDataDrive"></a> SMSTSLocalDataDrive

 Spécifie l'emplacement où la séquence de tâches stocke les fichiers temporaires sur l'ordinateur de destination en cours d'exécution.

 Cette variable doit être définie avant le démarrage de la séquence de tâches, notamment en définissant une variable de regroupement. Une fois que la séquence de tâches démarre, Configuration Manager définit la variable [_SMSTSMDataPath](#SMSTSMDataPath).


### <a name="SMSTSMP"></a> SMSTSMP

 Utilisez cette variable pour spécifier l’URL ou l’adresse IP du point de gestion Configuration Manager.


### <a name="SMSTSMPListRequestTimeoutEnabled"></a> SMSTSMPListRequestTimeoutEnabled

 *S’applique aux étapes suivantes :*  
 - [Installer l’application](task-sequence-steps.md#BKMK_InstallApplication)  
 - [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (entrée) 

 Cette variable permet d’activer les demandes MPList répétées pour actualiser le client s’il ne se trouve pas sur l’intranet. Par défaut, cette valeur est définie sur `True`. 

 Si des clients se trouvent sur Internet, définissez cette variable sur `False` pour éviter des retards inutiles. 


### <a name="SMSTSMPListRequestTimeout"></a> SMSTSMPListRequestTimeout

 *S’applique aux étapes suivantes :*  
 - [Installer l’application](task-sequence-steps.md#BKMK_InstallApplication)  
 - [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  


 (entrée) 

 Si la séquence de tâches ne parvient pas à récupérer la liste de points de gestion (MPList) depuis les services d'emplacement, cette variable spécifie le délai d’attente en millisecondes avant de retenter l’étape. Par défaut, la séquence de tâches attend `60000` millisecondes (60 secondes) avant de réessayer. Elle réessaie jusqu'à trois fois.


### <a name="SMSTSPeerDownload"></a> SMSTSPeerDownload

 Utilisez cette variable pour permettre au client d’utiliser la mise en cache d’homologue Windows PE. Le fait de définir cette variable sur `true` active cette fonctionnalité.


### <a name="SMSTSPeerRequestPort"></a> SMSTSPeerRequestPort

 Port réseau personnalisé utilisé par le cache d’homologue de Windows PE pour la diffusion initiale. Le port par défaut configuré dans les paramètres client est **8004**.


### <a name="SMSTSPersistContent"></a> SMSTSPersistContent

 utilisez cette variable pour conserver temporairement le contenu du cache de la séquence de tâches. Cette variable est différente de [SMSTSPreserveContent](#SMSTSPreserveContent), qui permet de conserver le contenu dans le cache du client Configuration Manager une fois que la séquence de tâches est terminée. SMSTSPersistContent utilise le cache de séquence de tâches, tandis que SMSTSPreserveContent utilise le cache du client Configuration Manager. 


### <a name="SMSTSPostAction"></a> SMSTSPostAction

 Spécifie une commande exécutée une fois la séquence de tâches terminée. Par exemple, spécifiez un script qui active des filtres d'écriture sur les appareils intégrés après que la séquence de tâches a déployé un système d'exploitation sur l'appareil.


### <a name="SMSTSPreferredAdvertID"></a> SMSTSPreferredAdvertID

 Force la séquence de tâches à exécuter un déploiement ciblé spécifique sur l’ordinateur de destination. Définissez cette variable à l’aide d’une commande de prédémarrage à partir de média ou PXE. Si cette variable est définie, la séquence de tâches se substitue à tous les déploiements requis.


### <a name="SMSTSPreserveContent"></a> SMSTSPreserveContent

 Cette variable marque le contenu dans la séquence de tâches pour qu’il soit conservé dans le cache du client Configuration Manager après le déploiement. Cette variable est différente de [SMSTSPersistContent](#SMSTSPersistContent), qui conserve le contenu uniquement pendant la durée de la séquence de tâches. SMSTSPersistContent utilise le cache de séquence de tâches, tandis que SMSTSPreserveContent utilise le cache du client Configuration Manager. Définissez SMSTSPreserveContent sur `true` pour activer cette fonctionnalité.


### <a name="SMSTSRebootDelay"></a> SMSTSRebootDelay

 Spécifie le nombre de secondes à attendre avant que l'ordinateur redémarre. Si cette variable est zéro (0), le gestionnaire des séquences de tâches n’affiche pas de boîte de dialogue de notification avant le redémarrage.

 #### <a name="example"></a>Exemple
 - `0` : ne pas afficher de notification  

 - `60` : afficher une notification pendant une minute  


### <a name="SMSTSRebootMessage"></a> SMSTSRebootMessage

 Spécifie le message à afficher dans la boîte de dialogue de notification de redémarrage. Si vous ne définissez pas cette variable, un message par défaut apparaît.

 #### <a name="example"></a>Exemple
 `The task sequence is restarting this computer`


### <a name="SMSTSRebootRequested"></a> SMSTSRebootRequested

 Indique qu'un redémarrage est demandé après que l'étape de séquence de tâches en cours est terminée. Si un redémarrage est nécessaire, définissez cette variable sur `true` et le gestionnaire des séquences de tâches redémarre l'ordinateur après cette étape de la séquence de tâches. Si l’étape de séquence de tâches nécessite un redémarrage pour terminer l’action, définissez cette variable. Après le redémarrage de l’ordinateur, la séquence de tâches continue à s’exécuter à partir de l’étape de séquence de tâches suivante.


### <a name="SMSTSRetryRequested"></a> SMSTSRetryRequested

 Demande une nouvelle tentative après la fin de l'étape de séquence de tâches en cours. Si cette variable de séquence de tâches est définie, la variable [SMSTSRebootRequested](#SMSTSRebootRequested) doit également être définie sur `true`. Après le redémarrage de l'ordinateur, le gestionnaire des séquences de tâches exécute à nouveau la même étape de la séquence de tâches.


### <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName

 *S’applique à l’étape [Exécuter la ligne de commande](task-sequence-steps.md#BKMK_RunCommandLine).*

 (entrée)

 Indique le compte par lequel la ligne de commande est exécutée. La valeur est une chaîne au format nomutilisateur ou domaine\nomutilisateur. Spécifiez le mot de passe du compte avec la variable [SMSTSRunCommandLinePassword](#SMSTSRunCommandLinePassword).

 Pour plus d'informations sur le compte Exécuter en tant que de la séquence de tâches, consultez [Comptes](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account).


### <a name="SMSTSRunCommandLinePassword"></a> SMSTSRunCommandLinePassword

 *S’applique à l’étape [Exécuter la ligne de commande](task-sequence-steps.md#BKMK_RunCommandLine).*

 (entrée)

 Indique le mot de passe pour le compte spécifié par la variable [SMSTSRunCommandLineUserName](#SMSTSRunCommandLineUserName).


### <a name="SMSTSSoftwareUpdateScanTimeout"></a> SMSTSSoftwareUpdateScanTimeout

 *S’applique à l’étape [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

 (entrée)

 Contrôlez le délai d’attente pour l’analyse des mises à jour logicielles pendant cette étape. Par exemple, augmentez la valeur si vous vous attendez à de nombreuses mises à jour lors de l’analyse. La valeur par défaut est `1800` secondes (30 minutes). La valeur de la variable est définie en secondes.

> [!NOTE] 
> À compter de la version 1802, la valeur par défaut est `3600` secondes (60 minutes).

### <a name="SMSTSUDAUsers"></a> SMSTSUDAUsers

 Spécifie les utilisateurs principaux de l’ordinateur de destination en utilisant le format suivant : `<DomainName>\<UserName>`. Séparez plusieurs utilisateurs à l'aide d'une virgule (`,`). Pour plus d’informations, consultez [Associer des utilisateurs à un ordinateur de destination](/sccm/osd/get-started/associate-users-with-a-destination-computer).

 #### <a name="example"></a>Exemple
 `contoso\jqpublic, contoso\megb, contoso\janedoh`


### <a name="SMSTSWaitForSecondReboot"></a> SMSTSWaitForSecondReboot

 *S’applique à l’étape [Installer les mises à jour logicielles](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).*

 (entrée)

 Cette variable de séquence de tâches facultative contrôle le comportement du client quand l’installation d’une mise à jour logicielle nécessite deux redémarrages. Définissez cette variable avant cette étape afin d’empêcher qu’une séquence de tâches échoue en raison d’un second redémarrage résultant de l’installation d’une mise à jour logicielle.

 Définissez la valeur de SMSTSWaitForSecondReboot en secondes afin de spécifier la durée pendant laquelle la séquence de tâches s’interrompt sur cette étape pendant le redémarrage de l’ordinateur. Laissez suffisamment de temps au cas où un second redémarrage serait nécessaire. 

Par exemple, si vous définissez SMSTSWaitForSecondReboot sur `600`, la séquence de tâches est suspendue pendant 10 minutes après un redémarrage, avant l’exécution des étapes supplémentaires. Cette variable est utile quand une étape de séquence de tâches d’installation de mises à jour logicielles installe plusieurs centaines de mises à jour logicielles.


### <a name="TSDisableProgressUI"></a> TSDisableProgressUI
 <!-- 1354291 --> Utilisez cette variable pour contrôler quand la séquence de tâches affiche la progression aux utilisateurs finaux. Pour masquer ou afficher la progression à des moments différents, définissez cette variable plusieurs fois dans une séquence de tâches.  

 - `true` : Masquer la progression de la séquence de tâches  

 - `false` : afficher la progression de la séquence de tâches  


### <a name="TSErrorOnWarning"></a> TSErrorOnWarning 

 *S’applique à l’étape [Installer l’application](task-sequence-steps.md#BKMK_InstallApplication).*

 (entrée) 

 Spécifiez si le moteur de séquence de tâches considère un avertissement détecté comme une erreur lors de cette étape. La séquence de tâches définit la variable [_TSAppInstallStatus](#TSAppInstallStatus) sur `Warning` quand une ou plusieurs applications, ou une dépendance nécessaire, n’ont pas été installées car une exigence n’a pas été satisfaite. Quand vous affectez la valeur `True` à cette variable et que la séquence de tâches affecte la valeur `Warning` à **_TSAppInstallStatus**, le résultat est une erreur. La valeur `False` est le comportement par défaut.


### <a name="WorkingDirectory"></a> WorkingDirectory

 *S’applique à l’étape [Exécuter la ligne de commande](task-sequence-steps.md#BKMK_RunCommandLine).*

 (entrée)

 Spécifie un répertoire de démarrage pour une action de ligne de commande. Le répertoire spécifié ne doit pas dépasser 255 caractères.

 #### <a name="examples"></a>Exemples
 - `C:\`  
 - `%SystemRoot%`  



## <a name="deprecated-variables"></a>Variables déconseillées

Les variables suivantes sont déconseillées :

- **OSDAllowUnsignedDriver** : n’est pas utilisée au cours du déploiement de Windows Vista et des systèmes d’exploitation ultérieurs
- **OSDBuildStorageDriverList** : s’applique uniquement à Windows XP et à Windows Server 2003
- **OSDDiskpartBiosCompatibilityMode** : nécessaire uniquement lors du déploiement de Windows XP ou Windows Server 2003
- **OSDInstallEditionIndex** : inutile après Windows Vista
- **OSDPreserveDriveLetter** : pour plus d’informations, consultez [OSDPreserveDriveLetter](#OSDPreserveDriveLetter)

### <a name="osdpreservedriveletter"></a>OSDPreserveDriveLetter

 > [!Important]
 > Cette variable de séquence de tâches est dépréciée. 
 >
 > Pendant le déploiement d’un système d’exploitation, par défaut, le programme d’installation de Windows détermine la meilleure lettre de lecteur à utiliser (généralement, C:). 

 *Comportement précédent* : lors de l’application d’une image, la variable OSDPreverveDriveLetter détermine si la séquence de tâches utilise ou non la lettre de lecteur capturée dans le fichier d’image (WIM). Définissez la valeur de cette variable sur `false` pour utiliser l’emplacement que vous spécifiez pour le paramètre **Destination** à l’étape de séquence de tâches **Appliquer le système d’exploitation**. Pour plus d’informations, consultez [Appliquer l’image de système d’exploitation](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).



## <a name="see-also"></a>Voir aussi

- [Étapes de séquence de tâches](/sccm/osd/understand/task-sequence-steps)
- [Utilisation des variables de séquence de tâches](/sccm/osd/understand/using-task-sequence-variables)
- [Considérations relatives à la planification de l’automatisation des tâches](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
