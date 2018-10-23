---
title: Dépannage de MDT
titleSuffix: Microsoft Deployment Toolkit
description: 'Guide de référence pour le dépannage de MDT (Microsoft Deployment Toolkit) '
ms.date: 09/09/2016
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 91a7a69a-deac-4b0f-aac9-b7bd187c53fb
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: efb65086878a46bfb3485fdd8b0be6f613225261
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2018
ms.locfileid: "27821013"
---
# <a name="troubleshooting-reference-for-the-microsoft-deployment-toolkit"></a>Guide de référence pour le dépannage de MDT (Microsoft Deployment Toolkit)
 Le déploiement de systèmes d’exploitation et d’applications ainsi que la migration de l’état utilisateur peuvent être relativement compliqués, même en vous aidant d’outils et de ressources d’assistance appropriés. Ce guide de référence, qui accompagne Microsoft® Deployment Toolkit (MDT) 2013, fournit des informations sur les problèmes connus actuels, des solutions possibles à ces problèmes et divers conseils de dépannage.  

> [!NOTE]
>  Dans ce document, le terme *Windows* fait référence aux systèmes d’exploitation Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012 et Windows Server 2008 R2, sauf indication contraire. MDT ne prend pas en charge les versions de Windows avec processeur ARM. Le terme *MDT* désigne MDT 2013, sauf indication contraire.  

> [!NOTE]
>  Microsoft DaRT (Diagnostics and Recovery Toolset) contient de puissants outils conçus pour la récupération et le dépannage d’ordinateurs clients qui ne démarrent pas ou qui sont devenus instables. Vous pouvez utiliser DaRT pour déterminer la cause d’un incident, restaurer des fichiers perdus, etc. DaRT est également un outil de dépannage utile pendant les phases de développement et de déploiement d’un système d’exploitation Windows. Par exemple, si une image intégrée ne démarre pas comme elle devrait, vous pouvez démarrer l’ordinateur client qui contient l’image à l’aide de l’environnement de diagnostic ERD Commander. Ensuite, vous pouvez explorer le disque dur de l’ordinateur client, afficher le journal des événements, supprimer des mises à jour, changer des paramètres du système d’exploitation, par exemple. DaRT fait partie de Microsoft Desktop Optimization Pack pour la Software Assurance. Pour en savoir plus sur DaRT, consultez [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## <a name="understanding-logs"></a>Présentation des journaux  
 Pour pouvoir dépanner MDT avec efficacité, il est essentiel d’avoir une bonne connaissance de tous les fichiers journaux (.log) utilisés durant le déploiement d’un système d’exploitation. Savoir quels fichiers journaux examiner en fonction de la condition d’échec rencontrée et de la phase du processus vous permet de clarifier et comprendre des problèmes qui semblent inexplicables et difficilement compréhensibles de prime abord.  

 Le format des fichiers journaux MDT est conçu pour être lu par Trace32, l’un des outils de System Center Configuration Manager 2007 Toolkit V2, que vous pouvez télécharger à partir du [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=9257). Les journaux peuvent également être lus par l’outil CMTrace (Configuration Manager Trace) qui est disponible dans System Center 2012 Configuration Manager et les versions ultérieures. Servez-vous de ces outils le plus souvent possible pour lire les fichiers journaux, car ils facilitent considérablement l’identification des erreurs.  

 Le reste de cette section détaille les fichiers journaux créés durant le déploiement et l’installation de Windows. Cette section donne également des exemples de situations dans lesquelles utiliser les fichiers pour le dépannage.  

### <a name="mdt-logs"></a>Journaux MDT  
 Chaque script MDT crée automatiquement des fichiers journaux lors de son exécution. Les noms de ces fichiers journaux font référence au nom du script exécuté, par exemple, ZTIGather.wsf crée un fichier journal nommé *ZTIGather.log*. Chaque script MDT met également à jour un fichier journal maître commun (BDD.log) qui agrège le contenu de tous les fichiers journaux créés par un script. Les fichiers journaux MDT résident dans le dossier C:\MININT\SMSOSD\OSDLOGS pendant le processus de déploiement. Selon le type de déploiement effectué, les fichiers journaux sont déplacés vers %WINDIR%\SMSOSD ou %WINDIR%\TEMP\SMSOSD à la fin du déploiement. Dans les déploiements LTI (Lite Touch Installation), les journaux sont d’abord placés dans C:\MININT\SMSOSD\OSDLogs. Ils sont ensuite déplacés vers %WINDIR%\TEMP\DeploymentLogs quand le traitement de la séquence de tâches est terminé.  

 MDT crée les fichiers journaux suivants :  

-   **BDD.log**. Il s’agit du fichier journal MDT agrégé qui est copié à un emplacement réseau à la fin du déploiement, si vous spécifiez la propriété **SLShare** dans le fichier Customsettings.ini.  

-   **LiteTouch.log**. Ce fichier est créé durant les déploiements LTI. Il est placé dans %WINDIR%\TEMP\DeploymentLogs, sauf si vous spécifiez l’option **/debug:true**.  

-   **Scriptname*.log**. Ce fichier est créé par chaque script MDT. *Scriptname* représente le nom du script exécuté.  

-   **SMSTS.log**. Ce fichier créé par le séquenceur de tâches décrit toutes les transactions du séquenceur. Selon le scénario de déploiement, il est créé dans %TEMP%, %WINDIR%\System32\ccm\logs, ou C:\\\_SMSTaskSequence, ou C:\SMSTSLog.  

-   **Wizard.log**. Les Assistants de déploiement créent et mettent à jour ce fichier.  

-   **WPEinit.log**. Ce fichier est créé durant le processus d’initialisation de Windows PE. Il facilite la résolution des problèmes rencontrés au démarrage de Windows PE.  

-   **DeploymentWorkbench_*id*.log**. Ce fichier journal est créé dans le dossier %temp% quand vous spécifiez l’option **a /debug** au démarrage de Deployment Workbench.  

### <a name="configuration-manager-operating-system-deployment-logs"></a>Journaux de déploiement de système d’exploitation dans Configuration Manager  
 Pour plus d’informations sur les fichiers journaux de déploiement de système d’exploitation créés par Microsoft System Center 2012 R2 Configuration Manager, consultez [Référence technique pour les fichiers journaux dans Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 Quand vous exécutez USMT, l’outil de migration utilisateur Windows, MDT ajoute automatiquement les options de journalisation pour enregistrer les fichiers journaux USMT aux emplacements des fichiers journaux MDT. Différents fichiers journaux sont créés, selon la phase de déploiement :  

-   **USMTEstimate.log**. Fichier créé lors de l’estimation des exigences par USMT  

-   **USMTCapture.log**. Fichier créé par USMT lors de la capture des données  

-   **USMTRestore.log**. Fichier créé par USMT lors de la restauration des données  

 Le script ZeroTouchInstallation.vbs recherche automatiquement les erreurs et avertissements dans les fichiers journaux de progression USMT. Le script génère l’ID d’événement 41010 dans Microsoft System Center Operations Manager avec le récapitulatif ci-dessous (où *usmt_type* est **ESTIMATE**, **SCANSTATE** ou  **LOADSTATE**, où *error_count* est le nombre total d’erreurs trouvées et où *warning_count* est le nombre total d’avertissements trouvés) :  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 Si le nombre d’erreurs est supérieur à 0, cet événement est classé comme erreur. Si le nombre d’avertissements est supérieur à 0 et qu’il n’y a pas d’erreur, l’événement est classé comme avertissement. Dans les autres cas, l’événement est classé comme information.  

## <a name="identifying-error-codes"></a>Identification des codes d’erreur  
Le tableau 1 répertorie et décrit les codes d’erreur générés par les scripts MDT. Ces codes d’erreur sont enregistrés dans le fichier BDD.log.  

### <a name="table-1-error-codes-and-their-description"></a>Tableau 1. Codes d’erreur accompagnés de leur description  

|**Code d’erreur**|**Description**|  
|-|-|  
|5201|Impossible d’établir une connexion au partage de déploiement. Le déploiement va être interrompu.|  
|5203|Impossible d’établir une connexion au partage de déploiement. Le déploiement va être interrompu.|  
|5205|Impossible d’établir une connexion au partage de déploiement. Le déploiement va être interrompu.|  
|5206|L’Assistant de déploiement a été annulé ou n’a pas été terminé. Le déploiement va être interrompu.|  
|5207|Impossible d’établir une connexion au partage de déploiement. Le déploiement va être interrompu.|  
|5208|**DeploymentType** n’est pas défini. Une valeur doit être définie pour **SkipWizard**.|  
|5208|Le séquenceur de tâches SMS est introuvable. Le déploiement va être interrompu.|  
|5400|Créer un objet : **Set *class_instance* = New *class_name***|  
|5490|Créer MSXML2.DOMDocument.|  
|5495|Create MSXML2.DOMDocument.ParseErr.ErrCode.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Vérifier le GUID OS : %OSGUID% existe.|  
|5602|Ouvrir XML avec OSGUID : %OSGUID%.|  
|5610|Vérifier le fichier.|  
|5630|Vérifier le fichier : *ImagePath*.|  
|5640|Vérifier le fichier : *ImagePath*.|  
|5641|FindFile: ImageX.exe.|  
|5643|Rechercher BootSect.exe.|  
|5650|Vérifier le répertoire : *SourcePath*.|  
|5651|Vérifier le répertoire : *SourcePath*\Platform.|  
|5652|FindFile: bootsect.exe.|  
|6001|Vérifier le lecteur.|  
|6002|Vérifier le lecteur.|  
|6010|Tester TSGUID.|  
|6020|Valeur retournée par Robocopy : *Value*.|  
|6021|Valeur retournée par Robocopy : *Value*.|  
|6101|Rechercher le fichier : *DeployCab*.|  
|6102|Développer les fichiers Sysprep à partir de DEPLOY.CAB.|  
|6111|Exécuter Sysprep.exe.|  
|6121|Exécuter Sysprep.|  
|6191|Tester **CloneTag** dans le Registre pour vérifier la fin de l’exécution de Sysprep.|  
|6192|Tester **SystemSetupInProgress** dans le Registre pour vérifier la fin de l’exécution de Sysprep.|  
|6401|Serveur DHCP autorisé.|  
|6501|Sauvegarde de l’ordinateur impossible, aucun chemin réseau (**BackupShare**, **BackupDir**) spécifié.|  
|6502|ERREUR : IMAGEX introuvable, échec de la sauvegarde.|  
|6601|GetObject(... root/wmi:BCDStore).|  
|6602|BCD.OpenStore (*BCDStore*).|  
|6701|Protecteurs configurés.|  
|6702|Fichiers de démarrage déplacés.|  
|6703|Créer la partition BDE.|  
|6704|Défragmenter le disque.|  
|6705|Réduire le disque.|  
|6706|Tester plusieurs partitions.|  
|6707|Créer les fichiers de démarrage.|  
|6708|Chiffrer le disque.|  
|6709|Établir une connexion au fournisseur WMI MicrosoftVolumeEncryption.|  
|6710|Chiffrement du disque.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Enregistrer la clé externe dans le fichier.|  
|6715|Protéger avec la clé externe.|  
|6716|Enregistrer la clé externe dans le fichier.|  
|6717|Protéger la clé avec un mot de passe numérique.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Enregistrer le mot de passe dans le fichier.|  
|6719|Ouvrir *PasswordFile*.|  
|6720|Chiffrer le lecteur.|  
|6721|Ouvrir *DiskPartFile*.|  
|6722|Créer la partition.|  
|6723|Obtenir le lecteur BDE existant.|  
|6724|Ouvrir *DiskPartFile*.|  
|6727|Essayer d’ouvrir *DiskPartFile*.|  
|6729|Créer le fichier texte *DiskPartFile*.|  
|6730|Exécuter **cmd /c DISKPART.EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2>&1**|  
|6731|Rechercher bcdboot.exe.|  
|6732|Établir une connexion au fournisseur TPM Microsoft.|  
|6733|Obtenir une instance TPM dans la classe du fournisseur.|  
|6734|Obtenir une instance TPM.|  
|6735|Vérifier si TPM est activé.|  
|6736|Vérifier si TPM est activé.|  
|6737|Vérifier si TPM est détenu par un propriétaire.|  
|6738|Vérifier si la propriété de TPM est autorisée.|  
|6739|Vérifier si TPM est activé.|  
|6740|Vérifier si TPM est activé.|  
|6741|Vérifier si TPM est détenu par un propriétaire et si la propriété est autorisée.|  
|6741|Mot de passe défini pour le propriétaire de TPM|  
|6742|Le P@ssword du propriétaire de TPM est défini à la valeur **AdminP@ssword**.|  
|6743|Définir une valeur pour le P@ssword du propriétaire de TPM.|  
|6744|Vérifier si TPM est activé.|  
|6745|Vérifier le propriétaire de TPM.|  
|6746|Vérifier la paire de clés de validité.|  
|6747|Vérifier si TPM est activé.|  
|6748|Vérifier si la propriété de TPM est autorisée.|  
|6749|Convertir un p@ssword de propriétaire en autorisation de propriétaire.|  
|6750|Créer une paire de clés de validité.|  
|6751|Changer l’autorisation du propriétaire.|  
|6752|Exécuter **Cmd**.|  
|6753|Valider TPM.|  
|6754|Obtenir l’instance BDE.|  
|6755|Protéger la clé avec TPM.|  
|6756|Rechercher un média amovible à configurer. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Protéger la clé avec TPM et une clé de démarrage.|  
|6758|Rechercher le code PIN de BDE.|  
|6759|Protéger la clé avec TPM et un code PIN.|  
|6760|Rechercher le média amovible pour **BDEKeyLocation**.|  
|6761|Protéger avec la clé externe.|  
|6762|Enregistrement du P@ssword de récupération dans *PasswordFile*.|  
|6764|Configurer la stratégie BitLocker.|  
|7000|ZTIConfigure.xml introuvable ; abandon.|  
|7001|Rechercher le fichier de réponses unattend.|  
|7100|ERREUR : Ce script doit s’exécuter uniquement dans le système d’exploitation complet.|  
|7101|ERREUR : Le nombre de valeurs fournies est insuffisant pour créer le fichier de réponses DCPromo.|  
|7102|ERREUR : Certaines propriétés obligatoires pour créer un contrôleur de domaine de réplica n’ont pas été spécifiées.|  
|7103|ERREUR : Certaines propriétés obligatoires pour créer un domaine enfant n’ont pas été spécifiées.|  
|7104|ERREUR : Certaines propriétés obligatoires pour créer une forêt n’ont pas été spécifiées.|  
|7105|ERREUR : Certaines propriétés obligatoires pour créer une forêt n’ont pas été spécifiées.|  
|7200|Impossible de configurer le serveur DHCP, car le service n’est pas installé.|  
|7201|Impossible de lire les détails de l’étendue ; échec de `GetScopeDetails()`.|  
|7202|Le nombre de valeurs fournies est insuffisant pour créer l’étendue.|  
|7203|Le nombre de valeurs fournies est insuffisant pour définir la plage d’adresses IP de cette étendue.|  
|7204|Aucune valeur n’est spécifiée dans la plage d’exclusion de l’étendue.|  
|7300|Impossible d’envoyer des commandes DNS.|  
|7700|Ce n’est pas un scénario de déploiement de nouvel ordinateur ; sortie de la partition de disque.|  
|7701|Taille du disque insuffisante pour les partitions système et BDE, taille requise = 1,5 Go.|  
|7702|Taille du disque insuffisante pour les partitions système et WinRE, taille requise = 10 Go.|  
|7703|DeployRoot est sur le disque n° *DiskIndex*. Exécution d’un scénario OEM : Ignorer.|  
|7704|Exécution d’un scénario OEM : Ignorer.|  
|7704|Les partitions étendues et logiques ne sont pas autorisées avec BitLocker.|  
|7712|Vérifier si Drive/*Volume Drive* est présent. Formater.|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|Findfile(PkgMgr.exe).|  
|9601|ERREUR : La tâche de restauration de l’état de ZTITatoo doit être exécutée dans le système d’exploitation complet ; abandon.|  
|9701|Code différent de zéro retourné par l’estimation de l’outil USMT, rc = *Error*.|  
|9702|Capture de l’état utilisateur impossible ; espace local insuffisant et chemin réseau (UDShare, UDDir) non spécifié.|  
|9703|Code différent de zéro retourné par la capture de l’outil USMT, rc = *Error*.|  
|9704|Aucune option de ligne de commande valide n’a été spécifiée.|  
|9801|ERREUR : Tentative de déploiement d’un système d’exploitation client sur une machine exécutant un système d’exploitation serveur.|  
|9802|ERREUR : Tentative de déploiement d’un système d’exploitation serveur sur une machine exécutant un système d’exploitation client.|  
|9803|ERREUR : La mise à niveau de la machine n’est pas autorisée (OSInstall=*OSInstall*) ; abandon.|  
|9804|ERREUR : La quantité de mémoire (*Memory* Mo) est insuffisante. La mémoire minimum nécessaire est de *Memory* Mo.|  
|9805|ERREUR : La vitesse du processeur (*ProcessorSpeed* MHz) est insuffisante.  Elle doit être supérieure ou égale à *ProcessorSpeed* MHz.|  
|9806|ERREUR : Espace libre insuffisant sur *Drive*. Il faut *Size* Mo d’espace supplémentaire.|  
|9807|ERREUR : Espace libre insuffisant sur *Drive*. Il faut *Size* Mo d’espace supplémentaire.|  
|9901|Le script ZTIWindowsUpdate ne doit pas être exécuté dans Windows PE.|  
|9902|ZTIWindowsUpdate a été exécuté et a échoué un trop grand nombre de fois. Nombre = *Count*.|  
|9903|Problème inattendu lors de l’installation des mises à jour de l’Agent Windows Update, rc = *Error*.|  
|9904|Échec de la création de l’objet : **Microsoft.Update.Session**.|  
|9905|Échec de la création de l’objet : **Microsoft.Update.UpdateColl**.|  
|9906|Fichier critique *File* introuvable ; abandon.|  
|10000|Créer un objet : **Set oLTICleanup = New LTICleanup**.|  
|10201|Impossible de joindre le domaine *Domain*. Arrêter l’installation.|  
|10203|FindFile(LTISuspend.wsf).|  
|10204|Exécuter le programme *LTISuspend*.|  
|41024|Exécuter ImageX.|  
|52012|Tous les paramètres de l’Assistant ne sont pas définis.|  

 La liste 1 fournit un extrait de fichier journal qui illustre la recherche d’un code d’erreur. Dans cet extrait, il s’agit du code d’erreur 5001.  

 **Liste 1. Extrait d’un fichier SMSTS.log contenant le code d’erreur 5001**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### <a name="converting-error-codes"></a>Conversion des codes d’erreur  
 Les codes d’erreur signalés dans les fichiers journaux sont très souvent difficiles à comprendre et à corréler à une condition d’erreur réelle. Toutefois, le processus suivant vous explique comment traduire un code d’erreur obscur en informations claires et utiles pour la résolution du problème.  

 **Problème** : une capture d’image échoue avec le code d’erreur 0x80070040.  

 **Première solution possible** : le code d’erreur présenté est au format hexadécimal, et vous devez le convertir au format décimal. Pour effectuer cette conversion, utilisez une calculatrice scientifique, comme la calculatrice fournie avec les systèmes d’exploitation Windows qui est parfaitement adaptée à cette tâche.  

 **Pour convertir un code d’erreur**  

1.  Cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Accessoires**, puis cliquez sur **Calculatrice**.  

2.  Dans le menu **Affichage**, cliquez sur **Scientifique**.  

3.  Sélectionnez **Hex**, puis entrez les quatre derniers chiffres du code, soit **0040**, comme dans l’exemple illustré à la figure 1.  

     ![TroubleshootingReference1](media/TroubleshootingReference1.jpg "TroubleshootingReference1")  
Figure 1. Conversion d’erreur  

     **Figure 1. Conversion d’erreur**  

     Comme vous pouvez le voir, les zéros non significatifs ne sont pas affichés quand la calculatrice est en mode hexadécimal.  

4.  Sélectionnez **Déc**.  

     La valeur hexadécimale *40* est convertie en la valeur décimale *64*.  

5.  Ouvrez une fenêtre d’invite de commandes, tapez **NET HELPMSG 64**, puis appuyez sur Entrée.  

     La commande **NET HELPMSG** traduit le code d’erreur numérique en un texte explicite. Dans cet exemple, le code d’erreur est traduit en « The specified network name is no longer available » (Le nom réseau spécifié n’est plus disponible).  

 Ce message signale un problème réseau potentiel sur l’ordinateur cible ou entre l’ordinateur cible et le serveur où se trouve le partage de déploiement. Le problème peut également être dû à des pilotes réseau qui ne sont pas installés correctement ou à une incompatibilité dans les paramètres de vitesse et duplex.  

 **Deuxième solution possible** : utilisez l’utilitaire de recherche de code d’erreur de Microsoft Exchange Server. Cet utilitaire en ligne de commande facilite la conversion du code d’erreur. Vous pouvez le télécharger à partir du [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=985).  

### <a name="review-of-sample-logs"></a>Revue des exemples de journaux  
 Les différents fichiers journaux créés par MDT sont utiles pour résoudre les problèmes rencontrés durant le processus de déploiement MDT. Les sections suivantes fournissent plusieurs exemples qui montrent comment exploiter les fichiers journaux MDT dans le cadre du dépannage d’un déploiement :  

-   Problèmes liés aux échecs d’accès à la base de données MDT (MDT DB), comme décrit dans [Échec de l’accès à la base de données](#FailuretoAccesstheDatabase)  

####  <a name="FailuretoAccesstheDatabase"></a> Échec de l’accès à la base de données  
 **Problème** : une erreur se produit quand le déploiement effectué utilise un fichier CustomSettings.ini contenant de nombreuses sections et spécifiant, avec la propriété **Priority**, la priorité de chaque section à traiter. Le fichier BDD.log contient les messages d’erreur suivants :  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  Par souci de clarté, les informations du fichier journal ci-dessus ont été représentées telles qu’elles s’affichent dans le programme Trace32.  

 **Solution possible** : comme indiqué à la première ligne de l’exemple de fichier journal, le problème est dû au refus de l’autorisation d’accès à la base de données. Le script ne peut donc pas établir de connexion sécurisée à la base de données, peut-être en raison d’un ID utilisateur et d’un mot de passe manquants. Une tentative d’accès à la base de données a alors été effectuée à l’aide du compte d’ordinateur. Pour contourner ce problème, la solution la plus simple est d’accorder à tout le monde l’accès en lecture à la base de données.  

## <a name="troubleshooting"></a>Résolution des problèmes  
 Avant de vous lancer dans des processus de dépannage complexes, passez en revue les points suivants et assurez-vous que tous les prérequis associés sont remplis :  

-   Des problèmes d’installation peuvent se produire si certains prérequis matériels et logiciels ne sont pas remplis.  

### <a name="application-installation"></a>Installation d’applications  
 Passez en revue les problèmes liés à l’installation d’applications et les solutions possibles :  

-   Fichiers sources d’installation bloqués pour des raisons de sécurité, comme décrit dans [Exécutables bloqués](#BlockedExecutables)  

-   Perte de connectivité réseau, comme décrit dans [Connexions réseau perdues](#LostNetworkConnections)  

-   Erreur 30029 à l’installation de la version 2007 de Microsoft Office System ou des fichiers associés, comme décrit dans [Version 2007 de Microsoft Office System](#MicrosoftOfficeSystem)  

####  <a name="BlockedExecutables"></a> Exécutables bloqués  
 **Problème** : quand les fichiers sources d’installation sont téléchargés à partir d’Internet, ils sont généralement marqués avec un ou plusieurs flux de données du système de fichiers NTFS. Pour plus d’informations sur les flux de données NTFS, consultez [Flux de fichiers](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx). L’existence de flux de données du système de fichiers NTFS peut entraîner l’affichage d’une invite **Open File – Security Warning** (Ouvrir un fichier – Avertissement de sécurité). L’installation s’interrompt jusqu’à ce que vous cliquiez sur **Exécuter** à l’invite.  

 Comme le montre la figure 2, vous pouvez afficher les flux de données du système de fichiers NTFS à l’aide de la commande **More** et de [l’utilitaire Streams](http://technet.microsoft.com/sysinternals/bb897440.aspx).  

 ![TroubleshootingReference2](media/TroubleshootingReference2.jpg "TroubleshootingReference2")  
Figure 2. Flux de données NTFS  

 **Figure 2. Flux de données NTFS**  

 **Première solution possible** : cliquez avec le bouton droit sur le fichier source d’installation, puis cliquez sur **Properties** (Propriétés). Cliquez sur **Unblock** (Débloquer), puis cliquez sur **OK** pour supprimer les flux de données du système de fichiers NTFS dans le fichier. Répétez ce processus pour chaque fichier source d’installation qui est bloqué par l’existence d’un ou de plusieurs flux de données du système de fichiers NTFS.  

 **Deuxième solution possible** : utilisez l’utilitaire Streams, comme dans la figure 2 REF \_Ref308173670 \\h, pour supprimer les flux de données du système de fichiers NTFS dans le fichier source d’installation. L’utilitaire Streams peut supprimer les flux de données du système de fichiers NTFS dans un ou plusieurs fichiers ou dossiers à la fois.  

####  <a name="LostNetworkConnections"></a> Connexions réseau perdues  
 **Problème** : une installation peut échouer quand elle installe des pilotes de périphérique ou qu’elle modifie des configurations de réseau et de périphérique existantes. Ces changements entraînent parfois une dégradation de la connectivité réseau qui provoque l’échec de l’installation.  

 **Solution possible** : implémentez le script ZTICacheUtil.vbs pour permettre le téléchargement et l’exécution de l’installation. Ce script est conçu pour adapter la publication afin de permettre le téléchargement et l’exécution. Le téléchargement utilise le service de transfert intelligent en arrière-plan \(BITS\) si le point de distribution de Configuration Manager prend en charge Web\-based Distributed Authoring et BITS. En parallèle, il modifie Configuration Manager pour exécuter d’abord le script ZTICache.vbs, ce qui empêche le programme de se supprimer pendant le processus de déploiement.  

####  <a name="MicrosoftOfficeSystem"></a> Version 2007 de Microsoft Office System  
 **Problème** : lors du déploiement de la version 2007 d’Office System et l’utilisation d’un fichier correctif \(MSP\) Windows Installer, l’installation peut échouer avec le code d’erreur 30029.  

 Si vous examinez plus en détail le fichier ZTIApplications.log, vous voyez les messages suivants :  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Première solution possible** : déplacez le fichier MSP vers le répertoire des mises à jour, puis exécutez setup.exe sans spécifier l’option **\/adminfile**. Pour plus d’informations sur le déploiement des mises à jour pendant l’installation, consultez [Déploiement d’Office System 2007](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Deuxième solution possible** : vérifiez que la case **Supprimer la boîte de dialogue modale** n’est pas cochée pour le fichier MSP. Pour plus d’informations sur la configuration de ce paramètre, consultez [Aperçu général du Guide de déploiement du système Office 2007](http://technet.microsoft.com/library/bb490141.aspx).  

### <a name="autologon"></a>AutoLogon  
 Passez en revue les problèmes liés à l’ouverture de session automatique et les solutions possibles :  

-   Interruption des processus de déploiement LTI et \(ZTI\) (Zero Touch Installation) à cause des bannières de sécurité d’ouverture de session, comme décrit dans [Bannières de sécurité d’ouverture de session](#LogonSecutiryBanners)  

-   Interruption des processus de déploiement LTI et ZTI à cause de demandes d’informations d’identification utilisateur, comme décrit dans [Demande d’informations d’identification utilisateur](#PromtedforUserCredentials)  

####  <a name="LogonSecutiryBanners"></a> Bannières de sécurité d’ouverture de session  
 **Problème** : les séquences de tâches MDT sont exécutées au cours d’une session d’utilisateur interactif, ce qui nécessite que l’ordinateur cible soit autorisé à se connecter automatiquement à l’aide d’un compte d’administration spécifié. Si un objet de stratégie de groupe \(GPO\) existant implémente une bannière de sécurité d’ouverture de session, l’opération d’ouverture de session automatique n’est pas autorisée à continuer, car la bannière de sécurité interrompt le processus d’ouverture de session jusqu’à ce qu’un utilisateur accepte la stratégie indiquée.  

 **Solution possible** : assurez-vous que l’objet de stratégie de groupe est appliqué à des unités d’organisation \(UO\) spécifiques, et qu’il n’est pas inclus dans l’objet de stratégie de groupe du domaine par défaut. Quand vous ajoutez des ordinateurs au domaine, spécifiez leur ajout à une unité d’organisation à laquelle ne s’applique aucun objet de stratégie de groupe implémentant une bannière de sécurité d’ouverture de session. Dans l’Éditeur de séquence de tâches, ajoutez comme l’une des dernières étapes de la séquence de tâches un script qui déplace le compte d’ordinateur vers l’unité d’organisation souhaitée.  

> [!NOTE]
>  Si vous réutilisez des comptes \(AD DS\) (Active Directory® Domain Services) existants, vérifiez, avant d’effectuer le déploiement sur l’ordinateur cible, que vous avez bien déplacé le compte de l’ordinateur cible vers une unité d’organisation à laquelle ne s’applique pas l’objet de stratégie de groupe implémentant la bannière de sécurité d’ouverture de session.  

####  <a name="PromtedforUserCredentials"></a> Demande d’informations d’identification utilisateur  
 **Problème** : vous avez créé une image d’un ordinateur qui a été joint au domaine. Lors du déploiement de la nouvelle image sur un ordinateur cible, le processus s’interrompt, car l’ouverture de session n’est pas établie automatiquement et l’utilisateur est invité à entrer ses informations d’identification. Le processus de déploiement reprend une fois que l’utilisateur a entré ses informations d’identification et ouvert une session.  

 **Solution possible** : quand vous capturez des images, vous ne devez pas joindre l’ordinateur source à un domaine. Si vous avez déjà joint l’ordinateur à un domaine, joignez-le à un groupe de travail, recapturez l’image, puis réessayez le déploiement sur un ordinateur cible pour déterminer si le problème est résolu.  

### <a name="bios"></a>BIOS  
 **Problème** : lors du déploiement sur un ordinateur cible doté de la technologie Intel vPro, le déploiement peut échouer avec une erreur d’arrêt. Même si tous les pilotes mis à jour ont été ajoutés en tant que pilotes non fournis avec Windows dans Deployment Workbench, l’ordinateur cible ne démarre pas.  

 Solution possible : vérifiez les paramètres du système \(BIOS\) définis sur l’ordinateur cible pour déterminer si le mode Serial Advanced Technology Attachment par défaut est configuré comme AHCI \(Advanced Host Controller Interface\). Malheureusement, certains systèmes d’exploitation Windows ne prennent pas en charge AHCI par défaut.  

### <a name="database-problems"></a>Problèmes liés aux bases de données  
 Passez en revue les problèmes liés aux bases de données et les solutions possibles :  

-   Erreurs générées à cause d’une configuration incorrecte des pare-feu sur le serveur de base de données, comme décrit dans [Demandes SQL Server Browser bloquées](#BlockedSQLServerBrowserRequests)  

-   Erreurs générées à cause de connexions interrompues avec le serveur de base de données, comme décrit dans [Connexions de canaux nommés](#NamedPipeConnections)  

####  <a name="BlockedSQLServerBrowserRequests"></a> Demandes SQL Server Browser bloquées  
 **Problème** : durant le processus de déploiement MDT, certaines informations peuvent être récupérées à partir des bases de données Microsoft SQL Server®. Toutefois, des erreurs sont parfois générées à cause d’une configuration incorrecte d’un pare-feu sur le serveur de base de données.  

 **Solution possible** : le Pare-feu Windows dans Windows Server permet d’empêcher les accès non autorisés aux ressources de l’ordinateur. Cependant, si le pare-feu n’est pas configuré de manière correcte, les tentatives de connexion à une instance de SQL Server peuvent être bloquées. Pour accéder à une instance de SQL Server située derrière le pare-feu, configurez le pare-feu sur l’ordinateur qui exécute SQL Server. Pour plus d’informations sur la configuration des ports de pare-feu pour SQL Server, consultez l’article du Support Microsoft [Comment ouvrir le port du pare-feu pour SQL Server sous Windows Server 2008 ?](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a> Connexions de canaux nommés  
 **Problème** : durant le processus de déploiement MDT, certaines informations peuvent être récupérées à partir des bases de données SQL Server. Toutefois, des erreurs sont parfois générées à cause de connexions SQL Server interrompues. Ces erreurs peuvent se produire quand les connexions de canaux nommés ne sont pas activées dans Microsoft SQL Server.  

 **Solution possible** : activez les canaux nommés dans SQL Server. Vous devez également toujours spécifier la propriété **SQLShare** quand vous établissez une connexion à une base de données externe en utilisant des canaux nommés. Pour établir la connexion à la base de données à l’aide de canaux nommés, utilisez la sécurité intégrée. Dans le cas des déploiements LTI, le compte d’utilisateur que vous spécifiez établit la connexion à la base de données. Pour les déploiements ZTI qui utilisent Configuration Manager, le compte d’accès réseau se connecte à la base de données. Étant donné que Windows PE n’a pas de contexte de sécurité par défaut, vous devez établir une connexion réseau avec le serveur de base de données afin de créer un contexte de sécurité pour l’utilisateur qui se connecte.  

 Le partage réseau spécifié par la propriété **SQLShare** fournit un moyen de se connecter au serveur pour obtenir un contexte de sécurité approprié. Vous devez avoir un accès en lecture au partage. Une fois que la connexion est établie, vous pouvez ensuite établir la connexion de canal nommé à la base de données. La propriété **SQLShare** n’est pas nécessaire et ne doit pas être utilisée pour établir une connexion TCP\/IP à la base de données.  

 Activez les connexions de canaux nommés en effectuant les étapes suivantes, qui diffèrent selon votre version de SQL Server :  

-   Activer les connexions de canaux nommés pour SQL Server 2008 R2, comme décrit dans [Activer les connexions de canaux nommés dans SQL Server 2008 R2](#EnableNamedPipeConnectionsinSQLServer).  

-   Activer les connexions de canaux nommés pour SQL Server 2005, comme décrit dans [Activer les connexions de canaux nommés dans SQL Server 2005](#EnableNamedPipeConnectionsinSQL).  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Activer les connexions de canaux nommés dans SQL Server 2008 R2  
 Pour activer les connexions de canaux nommés dans SQL Server 2008 R2, effectuez les étapes suivantes :  

1.  Sur l’ordinateur SQL Server 2008 R2 qui héberge la base de données à interroger, cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft SQL Server 2008 R2**, puis cliquez sur **SQL Server Management Studio**.  

2.  Dans la console **Microsoft SQL Server Management Studio**, dans **l’Explorateur d’objets**, cliquez avec le bouton droit sur ***nom\_serveur\_sql***, puis cliquez sur **Propriétés** \(où *nom\_serveur\_sql* est le nom de l’ordinateur SQL Server à configurer\).  

3.  La boîte de dialogue Propriétés du serveur \- ***nom\_serveur\_sql*** s’affiche.  

4.  Dans la boîte de dialogue **Propriétés du serveur** \- ***nom\_serveur\_sql***, dans **Sélectionner une page**, cliquez sur  **Connexions**.  

5.  Dans la page **Connexions**, vérifiez que la case **Autoriser les accès distants à ce serveur** est cochée, puis cliquez sur **OK**.  

6.  Fermez la console Microsoft SQL Server Management Studio.  

7.  Sur l’ordinateur SQL Server 2008 R2 qui héberge la base de données à interroger, cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft SQL Server 2008 R2**, pointez sur **Outils de configuration**, puis cliquez sur **Gestionnaire de configuration SQL Server**.  

8.  Dans la console **Gestionnaire de configuration SQL Server**, accédez à Gestionnaire de configuration SQL Server \(Local\) \/ Configuration du réseau SQL Server \/ Protocoles pour *instance\_sql* \(où *instance\_sql* est le nom de l’instance de SQL Server à configurer\).  

9. Dans le volet d’informations, cliquez avec le bouton droit sur **Canaux nommés**, puis cliquez sur **Activer**.  

     La boîte de dialogue d’avertissement s’affiche pour signaler que les modifications qui vont être enregistrées prendront effet uniquement après l’arrêt et le redémarrage du service.  

10. Dans la boîte de dialogue **Avertissement**, cliquez sur **OK**.  

11. Dans la console **Gestionnaire de configuration SQL Server**, accédez à Gestionnaire de configuration SQL Server \(Local\) \/ SQL Server Services.  

12. Dans le volet d’informations, cliquez avec le bouton droit sur **SQL Server*\(instance\_sql\)***, puis cliquez sur **Redémarrer** \(où *instance\_sql* est le nom de l’instance de SQL Server que vous avez configurée à l’étape 2\).  

     La barre de progression du Gestionnaire de configuration SQL Server s’affiche pour indiquer l’état de redémarrage du service. Une fois que le service a redémarré, la barre de progression se ferme.  

13. Fermez la console Gestionnaire de configuration SQL Server.  

 Pour plus d’informations, consultez [How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx) (Comment activer les connexions distantes dans SQL Server 2008).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Activer les connexions de canaux nommés dans SQL Server 2005  
 Pour activer les connexions de canaux nommés dans SQL Server 2005, effectuez les étapes suivantes :  

1.  Sur l’ordinateur SQL Server 2005 qui héberge la base de données à interroger, cliquez sur **Démarrer**, puis pointez sur **Tous les programmes**. Pointez sur **Microsoft SQL Server 2005**, pointez sur **Outils de configuration**, puis cliquez sur **Configuration de la surface d’exposition de SQL Server**.  

2.  Dans la boîte de dialogue **Configuration de la surface d’exposition de SQL Server 2005**, cliquez sur **Configuration de la surface d’exposition pour les services et les connexions**.  

3.  Dans la boîte de dialogue **Configuration de la surface d’exposition pour les services et les connexions – *nom\_serveur*** \(où *nom\_serveur*est le nom de l’ordinateur exécutant SQL Server 2005\), dans **Sélectionnez un composant, puis configurez ses services et connexions**, accédez à MSSQLSERVER\\Database Engine et cliquez sur **Connexions distantes**.  

4.  Cliquez sur **Connexions locales et distantes**, cliquez sur **Utilisation à la fois de TCP\/IP et de canaux nommés**, puis cliquez sur **Appliquer**.  

5.  Dans la boîte de dialogue **Configuration de la surface d’exposition pour les services et les connexions – *nom\_serveur*** \(où *nom\_serveur*est le nom de l’ordinateur exécutant SQL Server 2005\), dans **Sélectionnez un composant, puis configurez ses services et connexions**, accédez à MSSQLSERVER\\Database Engine et cliquez sur **Service**.  

6.  Cliquez sur **Arrêter**.  

     Le service MSSQLSERVER s’arrête.  

7.  Cliquez sur **Démarrer**.  

     Le service MSSQLSERVER démarre.  

8.  Cliquez sur **OK**.  

9. Fermez la boîte de dialogue Configuration de la surface d’exposition de SQL Server 2005.  

 Pour plus d’informations, consultez l’article du Support Microsoft [Comment configurer SQL Server 2005 afin de permettre les connexions à distance](http://support.microsoft.com/kb/914277)  

### <a name="deployment-scripts"></a>Scripts de déploiement  
 Passez en revue les problèmes liés à MDT et les solutions possibles :  

-   Demande d’informations d’identification utilisateur et affichage possible de l’erreur 0x80070035, comme décrit dans [Credentials_script](#Credentials_script)  

-   Affichage du message d’erreur « wuredist.cab not found » (wuredist.cab introuvable), comme décrit dans [ZTIWindowsUpdate](#ZTIWindowsUpdate)  

####  <a name="Credentials_script"></a> Credentials\_script  
 **Problème** : lors du dernier démarrage d’un nouvel ordinateur déployé, l’utilisateur est invité à entrer ses informations d’identification, et un message avec l’erreur 0x80070035 peut s’afficher, indiquant que le chemin réseau est introuvable.  

 **Solution possible** : assurez-vous que le fichier WIM n’inclut pas de dossier MININT ou \_SMSTaskSequence. Pour supprimer ces dossiers, montez d’abord le fichier WIM à l’aide de l’utilitaire ImageX, puis supprimez les dossiers.  

> [!NOTE]
>  Si une erreur d’accès refusé se produit quand vous essayez de supprimer les dossiers dans le fichier WIM, ouvrez une fenêtre d’invite de commandes, accédez à la racine de l’image contenue dans le fichier WIM, puis exécutez **RD MININT** et **RD \_SMSTaskSequence**.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problème** : si vous utilisez le script ZTIWindowsUpdate.wsf pour appliquer des mises à jour logicielles durant le déploiement, sachez que ce script peut communiquer directement avec le site Web Microsoft Update pour télécharger et installer les fichiers binaires nécessaires de l’Agent Windows Update, rechercher les mises à jour logicielles applicables et télécharger les fichiers binaires associés, puis installer les fichiers binaires téléchargés. Ce processus est possible si votre infrastructure réseau est configurée pour autoriser l’ordinateur cible à accéder au site Web Microsoft Update.  

 Si le partage de déploiement ne contient pas les fichiers d’installation de l’Agent Windows Update et que l’ordinateur cible n’a pas les autorisations d’accès à Internet appropriées, l’erreur « wuredist.cab not found » (wuredist.cab introuvable) est signalée dans les fichiers ZTIWindowsUpdate.log et BDD.log.  

 **Solution possible** : suivez les étapes décrites dans la section « ZTIWindowsUpdate.wsf » du *Guide de référence de Microsoft Deployment Toolkit*.  

### <a name="deployment-shares"></a>Partages de déploiement  
 Passez en revue les problèmes liés au partage de déploiement et les solutions possibles :  

-   Échec de la mise à jour des fichiers WIM lors de la mise à jour d’un partage de déploiement, comme décrit dans [Échec de la mise à jour des fichiers WIM](#FailuretoUpdateWIMFiles).  

####  <a name="FailuretoUpdateWIMFiles"></a> Échec de la mise à jour des fichiers WIM  
 Dans un environnement « simple » :  

-   MDT récupère généralement le fichier WIMGAPI.DLL à partir de C:\\Windows\\system32 \(toujours indiqué dans le chemin\). La version de ce fichier WIMGAPI.DLL doit être la même que la version \(build\) du système d’exploitation.  

-   Sur un système d’exploitation 64 bits, MDT utilise toujours le fichier WIMGAPI.DLL x64. Seul ce fichier doit être indiqué dans la variable système PATH. Sur un système d’exploitation 32 bits, MDT utilise toujours le fichier WIMGAPI.DLL x86. Seul ce fichier doit être indiqué dans la variable système PATH. \(D’autres produits, comme Configuration Manager, utilisent la version 32 bits de WIMGAPI.DLL, y compris sur un système d’exploitation 64 bits, mais ils prennent en charge et installent cette version.\)  

 **Problème** : quand vous tentez de mettre à jour un partage de déploiement, l’utilisateur est informé que le montage d’un ou de plusieurs fichiers .wim a échoué.  

 **Solution possible** : ouvrez une fenêtre d’invite de commandes et exécutez **where WIMGAPI.DLL**. Pour la première entrée dans la liste \(le premier emplacement dans les résultats de la recherche du chemin\), vérifiez que la propriété **Version** correspond à la version installée de Windows ADK \(Windows Assessment and Deployment Kit\). Vérifiez également que la propriété correspond au numéro de build du système d’exploitation.  

### <a name="the-windows-deployment-wizard"></a>Assistant de déploiement Windows  
 Passez en revue les problèmes liés à l’Assistant de déploiement Windows et les solutions possibles :  

-   Affichage des pages de l’Assistant de déploiement Windows, même quand LTI est configuré pour ignorer ces pages, comme décrit dans [Les pages de l’Assistant ne sont pas ignorées](#WizardPagesareNotSkipped).  

####  <a name="WizardPagesareNotSkipped"></a> Les pages de l’Assistant ne sont pas ignorées  
 **Problème** : une page de l’Assistant s’affiche même si la base de données MDT (MDT DB) ou le fichier CustomSettings.ini spécifie que les pages de l’Assistant doivent être ignorées.  

 **Solution possible** : pour forcer une page de l’Assistant à être ignorée, incluez toutes les propriétés à définir dans cette page de l’Assistant aux endroits pertinents dans la base de données MDT (MDT DB) ou le fichier CustomSettings.ini, et affectez-leur les valeurs appropriées. Si une propriété n’est pas configurée correctement pour une page de l’Assistant à ignorer, cette page s’affichera. Pour plus d’informations sur les propriétés à définir pour empêcher l’affichage d’une page de l’Assistant à ignorer, consultez la section « Providing Properties for Skipped Deployment Wizard Page » (Définir les propriétés des pages ignorées de l’Assistant de déploiement) dans le *Guide de référence de Microsoft Deployment Toolkit*.  

### <a name="disks-and-partitioning"></a>Disques et partitionnement  
 Passez en revue les problèmes liés au partitionnement de disque et les solutions possibles :  

-   Problèmes de chiffrement de lecteur BitLocker®, comme décrit dans [Chiffrement de lecteur BitLocker](#BitLockerDriveEncryption)  

-   Erreurs de partitionnement de disque, comme décrit dans « Erreurs de partitionnement de disque »  

-   Échec de certains déploiements pour actualiser un ordinateur à cause de l’utilisation de disques logiques ou dynamiques, comme décrit dans [Prise en charge des disques logiques et dynamiques](#SupportforLoogicalandDynamicDisks)  

####  <a name="BitLockerDriveEncryption"></a> Chiffrement de lecteur BitLocker  
 Le bon déroulement du déploiement de BitLocker nécessite une configuration spécifique. Les problèmes potentiels suivants peuvent être liés à la configuration de l’ordinateur cible :  

-   Dans les déploiements ZTI et UDI, le script ZTIBde.wsf échoue avec l’erreur « Impossible d’ouvrir la clé de Registre 'HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName' en lecture », comme décrit dans [Échec du script ZTIBde.wsf avec l’erreur « Impossible d’ouvrir la clé de Registre 'HKEY_CURRENT_USER\Control Panel\International\LocaleName' en lecture »](#ZTIBde.wsf).  

-   Affichage des périphériques USB, lecteurs de CD, lecteurs de DVD ou autres périphériques de médias amovibles sur l’ordinateur cible avec plusieurs lettres de lecteur, comme décrit dans [Affichage des périphériques avec plusieurs lettres de lecteur](#DevicesAppearasMultipleDriveLetters)  

-   Réduction du disque C sur l’ordinateur cible pour fournir suffisamment d’espace disque non alloué, comme décrit dans [Problèmes de réduction des disques](#ProblemswithShrinkingDisks)  

#####  <a name="ZTIBde.wsf"></a> Échec du script ZTIBde.wsf avec l’erreur « Impossible d’ouvrir la clé de Registre 'HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName' en lecture »  
 **Problème** : quand vous tentez de déployer BitLocker sur l’ordinateur cible dans ZTI ou UDI, le script ZTIBde.wsf échoue avec l’erreur « Impossible d’ouvrir la clé de Registre 'HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName' en lecture ».  

 **Solution possible** : spécifiez les paramètres régionaux dans la propriété **UILanguage**. Dans ZTI et UDI, comme le script ZTIBde.wsf s’exécute dans le contrôle système, le profil utilisateur complet n’est pas chargé. Quand le script ZTIBde.wsf tente de lire les paramètres régionaux, il ne les trouve pas dans le Registre, car le \(profil utilisateur\) du Registre n’est pas complètement chargé. Pour contourner ce problème, spécifiez les paramètres régionaux dans la propriété **UILanguage**.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> Affichage des périphériques avec plusieurs lettres de lecteur  
 **Problème** : certains périphériques s’affichent parfois avec plusieurs lettres de lecteur logique, selon la façon dont ils sont partitionnés. Dans certains cas, ils peuvent émuler un lecteur de disquette d’1,44 mégaoctets \(Mo\) et un lecteur de stockage de mémoire. Par conséquent, Windows peut assigner les mêmes lettres de lecteur A et B pour l’émulation de la disquette, et la lettre F pour le lecteur de stockage de mémoire. Par défaut, les scripts MDT utilisent la lettre de lecteur la plus basse \(dans cet exemple, la lettre A\).  

 **Solution possible** : changez le paramètre par défaut dans la page **Specify the BitLocker recovery details** (Spécifier les détails de la récupération BitLocker) de l’Assistant de déploiement Windows. La page de résumé de l’Assistant de déploiement Windows affiche un avertissement qui indique à l’utilisateur quelle lettre de lecteur a été sélectionnée pour le stockage des informations de récupération BitLocker. De plus, les fichiers BDD.log et ZTIBDE.log enregistrent les périphériques de médias amovibles détectés et le périphérique ayant été sélectionné pour stocker les informations de récupération BitLocker.  

#####  <a name="ProblemswithShrinkingDisks"></a> Problèmes de réduction des disques  
 **Problème** : il n’y a pas suffisamment d’espace disque non alloué sur l’ordinateur cible pour activer BitLocker. Le processus de déploiement de BitLocker sur un ordinateur cible a besoin d’au moins 2 gigaoctets \(Go\) d’espace disque non alloué pour la création du volume système. Le *volume système* est le volume qui contient les fichiers spécifiques au matériel nécessaires pour charger Windows après le démarrage de l’ordinateur à partir du BIOS.  

 **Première solution possible** : sur les ordinateurs existants, utilisez l’outil Diskpart pour réduire le disque C afin de permettre la création du volume système. Toutefois, dans certains cas, l’outil Diskpart ne peut pas réduire le disque C suffisamment pour fournir 2 Go d’espace disque non alloué. Cela peut être dû à la fragmentation de l’espace disque sur le disque C.  

 Une solution possible à ce problème consiste à défragmenter le disque C, en effectuant les étapes suivantes :  

1.  Dans l’utilitaire Diskpart, exécutez la commande **shrink querymax** pour déterminer la quantité maximale d’espace disque non alloué.  

2.  Si la valeur retournée à l’étape 1 est inférieure à 2 Go, nettoyez le disque C pour supprimer tous les fichiers inutiles, puis défragmentez-le.  

3.  Réexécutez la a commande **shrink querymax** de l’utilitaire Diskpart pour vérifier qu’il peut y avoir plus de 2 Go d’espace disque non alloué.  

4.  Si la valeur retournée à l’étape 3 est toujours inférieure à 2 Go, effectuez l’une des opérations suivantes :  

    -   Défragmentez le disque C plusieurs fois pour l’optimiser au maximum.  

    -   Sauvegardez les données sur le disque C, supprimez la partition existante, créez une autre partition, puis restaurez les données sur la nouvelle partition.  

 **Deuxième solution possible** : utilisez le script ZTIBDE.wsf, qui exécute l’outil de préparation de disque \(bdehdcfg.exe\) et configure la partition du volume système à une taille de 2 Go par défaut. Vous pouvez personnaliser le script ZTIBDE.wsf pour changer la valeur par défaut, si nécessaire. Toutefois, la modification des scripts MDT n’est pas recommandée.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Prise en charge des disques logiques et dynamiques  
 **Problème** : quand vous effectuez un déploiement pour actualiser un ordinateur, ce processus peut échouer si le déploiement cible un ordinateur qui utilise des lecteurs logiques ou des disques dynamiques.  

 **Solution possible** : MDT ne prend pas en charge le déploiement de systèmes d’exploitation sur des lecteurs logiques ou des disques dynamiques.  

### <a name="domain-join"></a>Jonction de domaine  
 **Problème** : pendant le déploiement, vous utilisez l’Assistant de déploiement Windows pour configurer toutes les informations nécessaires relatives à l’ordinateur cible, y compris les informations d’identification, de jonction de domaine et d’adresse IP statique. À la fin de l’installation, vous vous rendez compte que le système n’a pas été joint au domaine et qu’il se trouve toujours dans un groupe de travail.  

 **Solution possible** : un déploiement LTI de MDT configure les informations d’adresse IP statique après l’installation et le démarrage du système d’exploitation. Si l’ordinateur cible se trouve sur un segment réseau qui n’utilise pas le protocole DHCP \(Dynamic Host Configuration Protocol\), la jointure de domaine automatique spécifiée dans le fichier Unattend.xml échoue, car aucun protocole DHCP n’est disponible.  

 Configurez la jonction à un groupe de travail dans le fichier Unattend.xml. Ensuite, utilisez l’étape de séquence de tâches intégrée **Récupérer à partir du domaine** pour ajouter une étape dans la séquence de tâches qui permet de joindre le domaine après l’application de l’adresse IP statique.  

### <a name="driver-installation"></a>Installation de pilotes  
 Pour garantir une expérience utilisateur optimale, l’installation des périphériques matériels et des pilotes logiciels doit être aussi transparente que possible, avec peu ou pas d’intervention de l’utilisateur. Microsoft fournit des outils et des conseils pour vous aider à créer des packages d’installation qui répondent à cet objectif. Pour obtenir des informations générales sur l’installation des pilotes, consultez [Installation de périphériques et de pilotes](http://www.microsoft.com/whdc/driver/install/default.mspx).  

 Passez en revue les problèmes liés à l’installation de pilotes de périphérique et les solutions possibles :  

-   Problèmes lors de l’utilisation de pilotes de stockage de masse $OEM$ avec MDT, comme décrit dans « Combiner des pilotes de stockage de masse $OEM$ avec la logique de stockage de masse MDT »  

-   Dépannage d’une installation de pilote de périphérique à l’aide du fichier journal SetupAPI.log, comme décrit dans [Dépanner une installation de périphérique avec SetupAPI.log](#TroubleshootDeviceInstallationwithSetupAPI.log)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Dépanner une installation de périphérique avec SetupAPI.log  
 Le livre blanc sur le [dépannage d’une installation de périphérique à l’aide du fichier journal SetupAPI](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) fournit des informations pour déboguer une installation de périphérique Windows. En particulier, ce document explique aux développeurs et testeurs de pilotes comment interpréter les informations contenues dans le fichier journal SetupAPI.  

 Le fichier SetupAPI.log est l’un des fichiers journaux les plus utiles pour le débogage. Ce fichier de texte brut contient les informations que SetupAPI enregistre sur l’installation des périphériques, des Service Pack et des mises à jour. Le fichier contient notamment les enregistrements des modifications apportées aux périphériques et aux pilotes, ainsi que les principaux changements du système depuis la dernière installation de Windows. Ce livre blanc porte essentiellement sur l’utilisation du fichier journal SetupAPI dans le cadre du dépannage des installations de périphériques. Il ne décrit pas les sections du fichier journal qui concernent les installations des Service Pack et des mises à jour.  

### <a name="new-computer-deployments"></a>Déploiements de nouveaux ordinateurs  
 Passez en revue les problèmes liés aux déploiements de nouveaux ordinateurs et les solutions possibles :  

-   Problèmes de démarrage du processus de déploiement avec le démarrage PXE \(Preboot Execution Environment\), comme décrit dans [Démarrage PXE](#PXEBoot)  

####  <a name="PXEBoot"></a> Démarrage PXE  
 En bref, le protocole PXE fonctionne de cette façon : l’ordinateur client active le protocole en diffusant un paquet de détection DHCP. Ce paquet contient une extension qui identifie la requête comme une requête provenant d’un ordinateur client qui implémente le protocole PXE. En supposant qu’un serveur de démarrage implémentant ce protocole étendu est disponible, le serveur de démarrage envoie une offre contenant l’adresse IP du serveur qui doit exécuter le client. Le client utilise ensuite le protocole TFTP pour télécharger le fichier exécutable à partir du serveur de démarrage. Pour finir, l’ordinateur client exécute le programme d’amorçage téléchargé.  

 La phase initiale de ce protocole se superpose à un sous-ensemble de messages DHCP pour permettre au client de détecter un serveur de démarrage \(c’est-à-dire un serveur qui fournit les fichiers exécutables nécessaires pour installer le nouvel ordinateur\). L’ordinateur client peut saisir l’opportunité d’obtenir une adresse IP \(ce qui est le comportement attendu\), mais il n’y est pas obligé.  

 La deuxième phase de ce protocole se passe entre l’ordinateur client et un serveur de démarrage. Elle utilise le format de message DHCP pour faciliter la communication. Par ailleurs, cette phase n’a pas de lien avec les services DHCP standard. Les pages suivantes décrivent toutes les étapes du processus d’initialisation d’un ordinateur client avec PXE.  

 Pour plus d’informations sur la résolution des problèmes liés au démarrage PXE dans les services de déploiement Windows exécutés en mode hérité ou mixte, consultez l’article du Support Microsoft [Description de l’interaction PXE entre le client PXE, DHCP et le serveur RIS](http://support.microsoft.com/kb/244036).  

 Passez en revue les solutions suivantes aux problèmes de démarrage PXE :  

-   Désactivez la journalisation Windows PE dans SetupAPI.log, comme décrit dans [Désactiver la journalisation Windows PE dans les services de déploiement Windows](#DisableWindowsPELogginginWindowsDeploymentServices).  

-   Assurez-vous que DHCP est correctement configuré, comme décrit dans [Vérifier la configuration de DHCP](#EnsuretheProperDHCPConfiguration).  

-   Réduisez les temps de réponse lors de l’assignation d’adresses IP aux ordinateurs clients PXE, comme décrit dans [Réduire le temps de réponse lors de l’assignation d’une adresse IP PXE](#ImprovePXEIPAddressAssignmentResponseTime).  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Désactiver la journalisation Windows PE dans les services de déploiement Windows  
 La première chose à faire est de vérifier que la journalisation dans SetupAPI.log a bien été désactivée.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Vérifier la configuration de DHCP  
 En fonction des modèles de routeur utilisés, la configuration du routeur de transmission des diffusions DHCP peut être prise en charge vers un sous-réseau \(ou une interface de routeur\) ou vers un hôte spécifique. Si les serveurs DHCP et l’ordinateur exécutant les services de déploiement Windows sont des ordinateurs distincts, assurez-vous que les routeurs qui transmettent les diffusions DHCP permettent à la fois aux serveurs DHCP et des services de déploiement Windows de recevoir les diffusions du client. Sinon, l’ordinateur client ne pourra pas recevoir de réponse à sa requête de démarrage à distance.  

 Y a-t-il un routeur entre l’ordinateur client et le serveur d’installation à distance qui n’autorise pas les requêtes ou les réponses via DHCP ? Quand l’ordinateur client des services de déploiement Windows et le serveur des services de déploiement Windows se trouvent dans des sous-réseaux distincts, configurez le routeur entre les deux systèmes pour qu’il transmette les paquets DHCP au serveur des services de déploiement Windows. Cette configuration est nécessaire pour que les ordinateurs clients exécutant les services de déploiement Windows puissent détecter un serveur de services de déploiement Windows à l’aide d’un message de diffusion DHCP. Si la transmission DHCP n’est pas configurée sur un routeur, les diffusions DHCP des ordinateurs clients ne sont pas reçues par le serveur des services de déploiement Windows. Ce processus de transmission DHCP est parfois appelé *Proxy DHCP* ou *Adresse d’assistance IP* dans les manuels de configuration des routeurs. Pour plus d’informations sur la configuration de la transmission DHCP sur un routeur spécifique, reportez-vous aux instructions du routeur utilisé.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Réduire le temps de réponse lors de l’assignation d’une adresse IP PXE  
 Vérifiez les points suivants si la récupération d’une adresse IP par l’ordinateur client PXE prend beaucoup de temps \(de 15 à 20 secondes\) :  

-   La carte réseau sur l’ordinateur cible et le commutateur ou le routeur sont-ils définis sur la même vitesse \(automatique, duplex, maximale, etc.\)  

-   L’adresse IP du serveur des services de déploiement Windows est-elle définie dans le fichier d’assistance IP sur le routeur via lequel la connexion est établie ? Si la liste d’adresses IP dans le fichier d’assistance IP est longue, pouvez-vous déplacer l’adresse du serveur des services de déploiement Windows vers le haut de la liste ?  

### <a name="restarting-the-deployment-process"></a>Redémarrage du processus de déploiement  
 **Problème** : quand vous testez et corrigez une séquence de tâches, nouvelle ou existante, vous devez parfois redémarrer l’ordinateur cible pour permettre au processus de déploiement de recommencer depuis le début. Des résultats inattendus peuvent alors se produire. En effet, comme MDT effectue le suivi de sa progression en écrivant les données sur le disque dur, le redémarrage de l’ordinateur cible force MDT à reprendre là où il s’était arrêté au redémarrage précédent.  

 **Solution possible** : pour permettre le redémarrage du processus de déploiement depuis le début, supprimez les dossiers C:\\MININT et C:\\\_SMSTaskSequence avant de redémarrer l’ordinateur cible.  

### <a name="sysprep"></a>Sysprep  
 Passez en revue les problèmes liés à Sysprep et les solutions possibles :  

-   L’ordinateur cible n’apparaît pas dans l’unité d’organisation AD DS correcte, comme décrit dans [Le compte d’ordinateur ne se trouve pas dans l’unité d’organisation correcte](#ComputerAccountisintheWrongOU).  

####  <a name="ComputerAccountisintheWrongOU"></a> Le compte d’ordinateur ne se trouve pas dans l’unité d’organisation correcte  
 **Problème** : l’ordinateur cible est bien joint au domaine, mais le compte d’ordinateur n’apparaît pas dans l’unité d’organisation correcte.  

 **Première solution possible** : si un compte existe déjà pour l’ordinateur cible, le compte est maintenu dans son unité d’organisation d’origine. Pour déplacer le compte vers l’unité d’organisation spécifiée, ajoutez une étape de séquence de tâches qui utilise un outil d’automatisation, par exemple Microsoft Visual Basic® Scripting Edition, pour déplacer le compte.  

 **Deuxième solution possible** : vérifiez que l’unité d’organisation spécifiée existe et que son format est correct. L’unité d’organisation doit respecter le format suivant : `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### <a name="configuration-manager"></a>Configuration Manager  
 **Problème** : le message d’erreur indiqué à la figure 3 REF \_Ref308174600 \\h s’affiche quand vous essayez de créer un point de service PXE pour Configuration Manager à l’aide de l’option **Créer un certificat PXE auto\-signé**.  

 ![TroubleshootingReference3](media/TroubleshootingReference3.jpg "TroubleshootingReference3")  
Figure  SEQ Figure \\\* ARABIC 3. Erreur liée au point de service PXE  

 **Figure  SEQ Figure \\\* ARABIC 3. Erreur liée au point de service PXE**  

 **Solution possible** : si un point de service PXE existait déjà sur le serveur que vous configurez, ce point de service PXE n’a peut-être pas supprimé les certificats créés automatiquement au moment de sa désinstallation. Supprimez le dossier de certificat PXE dans C:\\Documents and Settings\\*nom\_utilisateur*\\Application Data\\Microsoft\\Crypto\\RSA, où *nom\_utilisateur* est le nom de l’utilisateur qui effectue la configuration actuelle ou qui a effectué la configuration précédente. L’Assistant Nouveau rôle de site doit se terminer correctement dans la console Configuration Manager quand vous avez supprimé le dossier.  

### <a name="task-sequences"></a>Séquences de tâches  
 Passez en revue les problèmes liés aux séquences de tâches et les solutions possibles :  

-   Une séquence de tâches ne se termine pas correctement ou a un comportement imprévisible, comme décrit dans [La séquence de tâches ne se termine pas correctement](#TaskSequenceDoesNotFinishSuccessfully).  

-   Les séquences de tâches OEM \(fabricant d’ordinateurs\) dans LTI s’affichent sur des images de démarrage conçues pour une autre architecture de processeur, comme décrit dans [La séquence de tâches OEM s’affiche sur une image de démarrage créée pour une architecture de processeur différente](#OEMTaskSequenceIncorrectlyAppearsforBootImage).  

-   L’Assistant de déploiement Windows affiche le message d’erreur « Bad Task Sequence Item \(Invalid OS GUID\) » [Séquence de tâches incorrecte (GUID OS non valide)], comme décrit dans [Affichage du message « Bad Task Sequence Item (Invalid OS GUID) » [Séquence de tâches incorrecte (GUID OS non valide)] dans l’Assistant de déploiement Windows](#BadTaskSequenceItem).  

-   Quand vous définissez un nom de connexion réseau, le message « Please enter a valid name for the network adapter » (Entrez un nom valide pour la carte réseau) s’affiche, comme décrit dans [Appliquer les paramètres réseau](#ApplyNetworkSettings).  

-   Des problèmes peuvent se produire à cause d’une configuration incorrecte du paramètre Continuer en cas d’erreur dans les paramètres de configuration pour les étapes de séquence de tâches, comme décrit dans [Utiliser le paramètre Continuer en cas d’erreur](#UseContinueonError).  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> La séquence de tâches ne se termine pas correctement  
 **Problème** : la séquence de tâches ne se termine pas correctement ou a un comportement imprévisible.  

 **Solution possible**: si l’étape de séquence de tâches **Installer le système d’exploitation** \(pour LTI\) ou l’étape de séquence de tâches **Appliquer l’image du système d’exploitation** \(pour UDI et ZTI\) a été modifiée depuis sa création initiale, cela peut produire des résultats imprévisibles. Par exemple, quand une séquence de tâches a initialement été créée pour déployer une image Windows 8.1 32 bits, et que l’étape de séquence de tâches **Installer le système d’exploitation** ou **Appliquer l’image du système d’exploitation** a ensuite été modifiée pour référencer une image Windows 8.1 64 bits, la séquence de tâches risque de ne pas s’exécuter correctement.  

 Il est recommandé de créer une séquence de tâches distincte pour déployer une image d’un système d’exploitation différent.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> La séquence de tâches OEM s’affiche pour une image de démarrage créée pour une architecture de processeur différente  
 **Problème** : une séquence de tâches basée sur un modèle de séquence de tâches OEM dans LTI s’affiche pour une image de démarrage associée à une architecture de processeur différente. Par exemple, une séquence de tâches OEM qui déploie un système d’opération 64 bits s’affiche sur une image de démarrage 32 bits.  

 **Solution possible** : cela correspond au comportement attendu. En effet, les séquences de tâches OEM dans LTI n’étant pas considérées comme dépendantes de la plateforme, elles s’affichent toujours, quelle que soit l’architecture de processeur de l’image de démarrage.  

####  <a name="BadTaskSequenceItem"></a> Affichage du message « Bad Task Sequence Item \(Invalid OS GUID\) » [Séquence de tâches incorrecte (GUID OS non valide)] dans l’Assistant de déploiement Windows  
 **Problème** : quand vous exécutez l’Assistant de déploiement Windows, l’Assistant affiche le message d’erreur « Bad Task Sequence Item \(Invalid OS GUID\) » [Séquence de tâches incorrecte (GUID OS non valide)]. Le système d’exploitation est répertorié dans le fichier OperatingSystem.xml, mais pas dans Deployment Workbench.  

 **Solution possible** : la source du système d’exploitation d’origine a plusieurs fichiers WIM associés. Une référence SKU associée à une séquence de tâches est supprimée, mais il reste d’autres références SKU pour la source du système d’exploitation. Quand vous sélectionnez la séquence de tâches associée à la référence SKU supprimée dans la page **Select a task sequence to execute on this computer** (Sélectionner une séquence de tâches à exécuter sur cet ordinateur) de l’Assistant de déploiement Windows, le message d’erreur « Bad Task Sequence Item \(Invalid OS GUID\) » [Séquence de tâches incorrecte (GUID OS non valide)] s’affiche lorsque vous cliquez sur **Suivant** dans la page de l’Assistant.  

 Pour résoudre ce problème, effectuez l’une des opérations suivantes :  

-   Supprimez toutes les références SKU dans la source du système d’exploitation. L’Assistant de déploiement Windows se comporte alors normalement, et le message d’erreur ne s’affiche plus.  

-   Changez la séquence de tâches pour utiliser une image de système d’exploitation différente.  

####  <a name="ApplyNetworkSettings"></a> Appliquer les paramètres réseau  
 **Problème** : quand vous définissez le nom de la connexion réseau dans Deployment Workbench, une erreur de validation se produit, avec le message « Please enter a valid name for the network adapter » (Entrez un nom valide pour la carte réseau).  

 **Solution possible** : supprimez les espaces et les caractères non valides éventuels dans le nom de connexion spécifié.  

####  <a name="UseContinueonError"></a> Continuer en cas d’erreur  
 Si une séquence de tâches MDT est configurée pour ne pas continuer en cas d’erreur et que cette séquence de tâches retourne une erreur, toutes les séquences de tâches suivantes dans ce groupe de séquences de tâches sont ignorées. Toutefois, les autres groupes de séquences de tâches continuent d’être exécutés. Considérez les points suivants :  

 Deux groupes de séquences de tâches ont été créés, et chaque groupe contient plusieurs étapes de séquence de tâches :  

-   Groupe A  

    -   Étape A  

    -   Étape B  

-   Groupe B  

    -   Étape A  

    -   Étape B  

 Si le groupe A\\l’étape A sont configurés pour ne pas continuer en cas d’erreur, le groupe A\\l’étape B ne seront pas exécutés. Toutefois, toutes les étapes de séquence de tâches dans le groupe B seront exécutées.  

### <a name="the-user-state-migration-tool"></a>Outil de migration utilisateur (USMT)  
 Passez en revue les problèmes liés à USMT et les solutions possibles :  

-   Les raccourcis qui pointent vers des documents stockés dans des dossiers réseau partagés ne sont pas toujours restaurés correctement, comme décrit dans [Raccourcis manquants sur le Bureau](#MissingDesktopShortcuts).  

####  <a name="MissingDesktopShortcuts"></a> Raccourcis manquants sur le Bureau  
 **Problème** : quand vous utilisez l’outil USMT pour migrer des données utilisateur, certains raccourcis qui pointent vers des documents stockés sur le réseau ne sont pas restaurés. Les raccourcis sont capturés durant Scanstate, mais ils ne sont jamais restaurés sur l’ordinateur cible durant Loadstate.  

 **Solution possible** : modifiez le fichier MigUser.xml pour commenter la ligne suivante :  

 Ligne initiale :  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Ligne modifiée :  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### <a name="windows-imaging-format-files"></a>Fichiers au format Windows Imaging (WIM)  
 Passez en revue les problèmes liés aux fichiers WIM et les solutions possibles :  

-   Les déploiements LTI et ZTI échouent avec des erreurs de fichier WIM enregistrées dans le fichier BDD.log, comme décrit dans [Fichier WIM endommagé](#CorruptWIMFile).  

####  <a name="CorruptWIMFile"></a> Fichier WIM endommagé  
 **Problème** : le déploiement d’une image échoue, et les erreurs suivantes sont enregistrées dans le fichier BDD.log :  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Identifiez le problème en montant le fichier WIM à partir des résultats d’ImageX fournis dans l’erreur « The data is invalid » (Données non valides). Une analyse de l’horodatage montre que le fichier .wim est daté de plusieurs années avant la date actuelle. Le fichier .wim a peut-être été maintenu ouvert par un autre processus, comme un antivirus, après avoir été fermé à la fin d’un processus de lecture ou d’écriture.  

 **Solution possible** : restaurez le fichier .wim à partir du support de sauvegarde.  

### <a name="windows-pe"></a>Windows PE  
 Passez en revue les problèmes liés à Windows PE et les solutions possibles :  

-   Le processus de déploiement LTI ou ZTI ne démarre pas en raison d’une mémoire RAM ou d’une carte réseau sans fil limitée, comme décrit dans [Échec du démarrage du processus de déploiement : RAM ou carte réseau sans fil limitée](#LimitedRamorWirelessNetworkAdapter).  

-   Le processus de déploiement LTI ou ZTI ne démarre pas en raison de composants Windows PE manquants, comme décrit dans [Échec du démarrage du processus de déploiement : composants manquants](#MissingComponents).  

-   Le processus de déploiement LTI ou ZTI ne démarre pas en raison de pilotes de périphériques manquants ou incorrects, comme décrit dans [Échec du démarrage du processus de déploiement : pilotes manquants ou incorrects](#MissingorIncorrectDrivers).  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Échec du démarrage du processus de déploiement : RAM ou carte réseau sans fil limitée  
 **Problème** : lors du déploiement d’une image sur certains ordinateurs cibles, Windows PE démarre, exécute **wpeinit** et ouvre une fenêtre d’invite de commandes, mais il ne démarre pas le processus de déploiement. Si, pour résoudre ce problème, vous mappez un lecteur réseau à partir de l’ordinateur cible, un message indique que les pilotes de carte réseau ne sont pas chargés.  

 **Première solution possible** : l’Assistant de déploiement ne démarre pas, car la mémoire RAM est insuffisante. Vérifiez que l’ordinateur cible dispose d’au moins 512 Mo de mémoire RAM et que la mémoire vidéo partagée ne consomme pas plus de 64 Mo sur les 512 Mo disponibles.  

 Les versions de Windows PE prises en charge par MDT ne sont pas exécutables sur un ordinateur cible ayant moins de 512 Mo de RAM.  

 **Deuxième solution possible** : n’incluez pas les pilotes sans fil dans l’image Windows PE.  

####  <a name="MissingComponents"></a> Échec du démarrage du processus de déploiement : composants manquants  
 **Problème** : quand vous examinez le fichier BDD.log suite à l’échec d’un déploiement, vous trouvez l’erreur suivante :  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Solution possible** : cette erreur peut indiquer que l’image Windows PE n’a pas été créée par MDT. Si vous utilisez Configuration Manager, n’utilisez pas les images Windows PE créées par Configuration Manager. À la place, créez une image à l’aide de l’Assistant Microsoft Importation de séquence de tâches.  

> [!NOTE]
>  Les images Windows PE créées par Configuration Manager contiennent des composants qui prennent en charge les scripts, XML et Windows Management Instrumentation (WMI), mais elles n’ont pas de composants prenant en charge Microsoft ActiveX® Data Objects (ADO).  

####  <a name="MissingorIncorrectDrivers"></a> Échec du démarrage du processus de déploiement : pilotes manquants ou incorrects  
 **Problème** : lors du déploiement sur certains ordinateurs cibles, Windows PE démarre, exécute **wpeinit** et ouvre une fenêtre d’invite de commandes, mais il ne démarre pas le processus de déploiement. Si, pour résoudre ce problème, vous mappez un lecteur réseau à partir de l’ordinateur cible, un message indique que les pilotes de carte réseau ne sont pas chargés. L’examen du fichier SetupAPI.log enregistré dans *X*:\Windows\System32\Inf montre que Windows PE génère des erreurs au moment de la configuration de la carte réseau, et notamment l’erreur « This driver is not meant for this platform » (Ce pilote n’est pas conçu pour cette plateforme). Les pilotes répertoriés dans la liste **Out-of-Box Drivers** (Pilotes non fournis avec Windows) ont été injectés dans l’image.  

 **Solution possible** : un pilote Windows PE est peut-être en conflit avec un autre pilote. Quand vous configurez les paramètres de l’image Windows PE dans Deployment Workbench, créez un groupe de pilotes Windows PE qui contient uniquement des pilotes de stockage et de carte réseau, puis configurez le partage de déploiement pour utiliser uniquement ce nouveau groupe de pilotes Windows PE.  

## <a name="deployment-process-flow-charts"></a>Organigrammes des processus de déploiement  
 Cette section présente deux ensembles d’organigrammes MDT : un pour les déploiements LTI et un pour les déploiements ZTI avec Configuration Manager. Chaque organigramme illustre les différentes tâches exécutées durant chaque type de déploiement.  

 Pour vous familiariser avec les processus de déploiement :  

-   Passez en revue les organigrammes des processus de déploiement LTI, présentés dans [Organigrammes des processus de déploiement LTI](#LTIDeploymentProcessFlowcharts)  

-   Passez en revue les organigrammes des processus de déploiement ZTI, présentés dans [Organigrammes des processus de déploiement ZTI](#ZTIDevelopmentProcessFlowcharts)  

###  <a name="LTIDeploymentProcessFlowcharts"></a> Organigrammes des processus de déploiement LTI  
 Les organigrammes décrivent les phases suivantes :  

-   Validation (figure 4)  

-   Capture de l’état (figures 5 et 6)  

-   Préinstallation (figures 7, 8 et 9)  

-   Installation (figure 10)  

-   Postinstallation (figures 11 et 12)  

-   Restauration de l’état (figures 13, 14, 15 et 16)  

 ![TroubleshootingReference4](media/TroubleshootingReference4.jpg "TroubleshootingReference4")  
Figure 4. Organigramme de la phase Validation  

 **Figure 4. Organigramme de la phase Validation**  

 ![TroubleshootingReference5](media/TroubleshootingReference5.jpg "TroubleshootingReference5")  
Figure 5. Organigramme de la phase Capture de l’état (1 sur 2)  

 **Figure 5. Organigramme de la phase Capture de l’état (1 sur 2)**  

 ![TroubleshootingReference6](media/TroubleshootingReference6.jpg "TroubleshootingReference6")  
Figure 6. Organigramme de la phase Capture de l’état (2 sur 2)  

 **Figure 6. Organigramme de la phase Capture de l’état (2 sur 2)**  

 ![TroubleshootingReference7](media/TroubleshootingReference7.jpg "TroubleshootingReference7")  
Figure 7. Organigramme de la phase Préinstallation (1 sur 3)  

 **Figure 7. Organigramme de la phase Préinstallation (1 sur 3)**  

 ![TroubleshootingReference8](media/TroubleshootingReference8.jpg "TroubleshootingReference8")  
Figure 8. Organigramme de la phase Préinstallation (2 sur 3)  

 **Figure 8. Organigramme de la phase Préinstallation (2 sur 3)**  

 ![TroubleshootingReference9](media/TroubleshootingReference9.jpg "TroubleshootingReference9")  
Figure 9. Organigramme de la phase Préinstallation (3 sur 3)  

 **Figure 9. Organigramme de la phase Préinstallation (3 sur 3)**  

 ![TroubleshootingReference10](media/TroubleshootingReference10.jpg "TroubleshootingReference10")  
Figure 10. Organigramme de la phase Installation  

 **Figure 10. Organigramme de la phase Installation**  

 ![TroubleshootingReference11](media/TroubleshootingReference11.jpg "TroubleshootingReference11")  
Figure 11. Organigramme de la phase Postinstallation (1 sur 2)  

 **Figure 11. Organigramme de la phase Postinstallation (1 sur 2)**  

 ![TroubleshootingReference12](media/TroubleshootingReference12.jpg "TroubleshootingReference12")  
Figure 12 Organigramme de la phase Postinstallation (2 sur 2)  

 **Figure 12 Organigramme de la phase Postinstallation (2 sur 2)**  

 ![TroubleshootingReference13](media/TroubleshootingReference13.jpg "TroubleshootingReference13")  
Figure 13. Organigramme de la phase Restauration de l’état (1 sur 4)  

 **Figure 13. Organigramme de la phase Restauration de l’état (1 sur 4)**  

 ![TroubleshootingReference14](media/TroubleshootingReference14.jpg "TroubleshootingReference14")  
Figure 14. Organigramme de la phase Restauration de l’état (2 sur 4)  

 **Figure 14. Organigramme de la phase Restauration de l’état (2 sur 4)**  

 ![TroubleshootingReference15](media/TroubleshootingReference15.jpg "TroubleshootingReference15")  
Figure 15. Organigramme de la phase Restauration de l’état (3 sur 4)  

 **Figure 15. Organigramme de la phase Restauration de l’état (3 sur 4)**  

 ![TroubleshootingReference16](media/TroubleshootingReference16.jpg "TroubleshootingReference16")  
Figure 16. Organigramme de la phase Restauration de l’état (4 sur 4)  

 **Figure 16. Organigramme de la phase Restauration de l’état (4 sur 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> Organigrammes des processus de déploiement ZTI  
 Les organigrammes décrivent les phases suivantes du déploiement ZTI à l’aide de Configuration Manager :  

-   Initialisation (figure 17)  

-   Validation (figure 18)  

-   Capture de l’état (figure 19)  

-   Préinstallation (figure 20)  

-   Installation (figure 21)  

-   Postinstallation (figure 22)  

-   Restauration de l’état (figures 23 et 24)  

-   Capture (figure 25)  

 ![TroubleshootingReference17](media/TroubleshootingReference17.jpg "TroubleshootingReference17")  
Figure 17. Organigramme de la phase Initialisation  

 **Figure 17. Organigramme de la phase Initialisation**  

 ![TroubleshootingReference18](media/TroubleshootingReference18.jpg "TroubleshootingReference18")  
Figure 18. Organigramme de la phase Validation  

 **Figure 18. Organigramme de la phase Validation**  

 ![TroubleshootingReference19](media/TroubleshootingReference19.jpg "TroubleshootingReference19")  
Figure 19. Organigramme de la phase Capture de l’état  

 **Figure 19. Organigramme de la phase Capture de l’état**  

 ![TroubleshootingReference20](media/TroubleshootingReference20.jpg "TroubleshootingReference20")  
Figure 20. Organigramme de la phase Préinstallation  

 **Figure 20. Organigramme de la phase Préinstallation**  

 ![TroubleshootingReference21](media/TroubleshootingReference21.jpg "TroubleshootingReference21")  
Figure 21. Organigramme de la phase Installation  

 **Figure 21. Organigramme de la phase Installation**  

 ![TroubleshootingReference22](media/TroubleshootingReference22.jpg "TroubleshootingReference22")  
Figure 22. Organigramme de la phase Postinstallation  

 **Figure 22. Organigramme de la phase Postinstallation**  

 ![TroubleshootingReference23](media/TroubleshootingReference23.jpg "TroubleshootingReference23")  
Figure 23. Organigramme de la phase Restauration de l’état (1 sur 2)  

 **Figure 23. Organigramme de la phase Restauration de l’état (1 sur 2)**  

 ![TroubleshootingReference24](media/TroubleshootingReference24.jpg "TroubleshootingReference24")  
Figure 24. Organigramme de la phase Restauration de l’état (2 sur 2)  

 **Figure 24. Organigramme de la phase Restauration de l’état (2 sur 2)**  

 ![TroubleshootingReference25](media/TroubleshootingReference25.jpg "TroubleshootingReference25")  
Figure 25. Organigramme de la phase Capture  

 **Figure 25. Organigramme de la phase Capture**  

## <a name="finding-additional-help"></a>Obtenir de l’aide supplémentaire  
 Vous pouvez obtenir de l’aide supplémentaire pour résoudre vos problèmes de déploiement MDT :  

-   En contactant le Support Microsoft, comme décrit dans [Support Microsoft](#MicrosoftSupport)  

-   En recherchant d’autres conseils de dépannage sur les blogs et dans d’autres ressources Internet, comme décrit dans [Support sur Internet](#InternetSupport)  

###  <a name="MicrosoftSupport"></a> Support Microsoft  
 Microsoft fournit les niveaux de Support Premier et Professional pour Microsoft Deployment Toolkit.  

 Support Professional : [http://support.microsoft.com/](http://support.microsoft.com/)  

 Support Premier : [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  Quand vous contactez le Support, précisez que le problème rencontré concerne MDT et une version spécifique.  

###  <a name="InternetSupport"></a> Support sur Internet  
 En plus des informations contenues dans ce guide de référence, vous trouverez de nombreux conseils de dépannage pour MDT dans diverses ressources en ligne. Vous pouvez notamment consulter les ressources en ligne suivantes :  

-   Blogs hébergés par Microsoft  

    -   [Blog de l’équipe MDT](http://blogs.technet.com/b/msdeployment/)  

    -   [Blog de l’équipe Configuration Manager](http://blogs.technet.com/b/configmgrteam/)  

    -   [Blog de Michael Niehaus](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus écrit des articles sur le déploiement de Windows et Microsoft Office.)  

-   Forums et groupes de discussion hébergés par Microsoft :  

     Les forums et groupes de discussion ci-dessous fournissent des informations d’assistance publiées par des employés Microsoft, des professionnels de l’informatique et des experts techniques Microsoft Valued Professional :  

    -   [Configuration Manager - Déploiement de système d’exploitation](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Installation, configuration et déploiement de Windows 8](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Sources d’informations sur le déploiement non fournies par Microsoft :  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
