---
title: 'Mettre à niveau les clients macOS '
titleSuffix: Configuration Manager
description: Mettez à niveau les clients sur des ordinateurs Mac dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fb0ef52bc3359e1b31b2e2237a87e58bf671bcb7
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260834"
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>Comment mettre à niveau les clients sur les ordinateurs Mac dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Suivez les étapes générales décrites ci-dessous pour mettre à niveau le client pour des ordinateurs Mac à l’aide d’une application System Center Configuration Manager. Vous pouvez également télécharger le fichier d'installation du client Mac, le copier dans un emplacement réseau partagé ou un dossier local sur l'ordinateur Mac puis demander aux utilisateurs d'exécuter l'installation manuellement.  

> [!NOTE]  
>  Avant d’effectuer ces étapes, assurez-vous que votre ordinateur Mac dispose de la configuration requise. Consultez [Systèmes d’exploitation pris en charge pour les ordinateurs Mac](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>Étape 1 : Télécharger le dernier fichier d’installation du client Mac à partir du Centre de téléchargement Microsoft  
 Le client Mac pour Configuration Manager n’est pas fourni sur le support d’installation de Configuration Manager et doit être téléchargé à partir du Centre de téléchargement Microsoft. Les fichiers d'installation du client Mac sont contenus dans un fichier Windows Installer nommé ConfigmgrMacClient.msi.  

 Vous pouvez télécharger ce fichier à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=525184).  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>Étape 2 : Exécuter le fichier d’installation téléchargé pour créer le fichier d’installation du client Mac  
 Sur un ordinateur exécutant Windows, exécutez **ConfigmgrMacClient.msi** que vous avez téléchargé pour décompresser le fichier d'installation du client Mac, nommé **Macclient.dmg**. Ce fichier est disponible, par défaut, dans le dossier **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** sur l'ordinateur Windows une fois que vous avez décompressé les fichiers.  

## <a name="step-3-extract-the-client-installation-files"></a>Étape 3 : Extraire les fichiers d’installation du client  
 Copiez le fichier Macclient.dmg dans un partage réseau ou dans un dossier local sur un ordinateur Mac. Puis, sur l'ordinateur Mac, montez et ouvrez le fichier Macclient.dmg et copiez les fichiers dans un dossier sur l'ordinateur Mac.  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>Étape 4 : Créer un fichier .cmmac pouvant être utilisé pour créer une application  

1.  Utilisez l'outil **CMAppUtil** (disponible dans le dossier **Outils** des fichiers d'installation du client Mac) pour créer un fichier .cmmac à partir du package d'installation du client. Ce fichier sera utilisé pour créer l’application Configuration Manager.  

2.  Copiez le nouveau fichier **CMClient.pkg.cmmac** dans un emplacement disponible pour l’ordinateur qui exécute la console Configuration Manager.  

 Pour plus d’informations, consultez [Procédures supplémentaires de création et de déploiement d’applications pour ordinateurs Mac](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers).  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**Étape 5 :** Créer et déployer une application contenant les fichiers du client Mac  

1.  Dans la console Configuration Manager, créez une application à partir du fichier **CMClient.pkg.cmmac** qui contient les fichiers d’installation du client.  

2.  Déployez cette application sur les ordinateurs Mac de votre hiérarchie.  

 Pour plus d’informations, consultez [Création d’applications pour ordinateurs Mac avec System Center Configuration Manager](../../../../apps/get-started/creating-mac-computer-applications.md).  

## <a name="step-6-users-install-the-latest-client"></a>Step 6 : Les utilisateurs installent la dernière version du client  
 Les utilisateurs de clients Mac seront informés qu’une mise à jour du client Configuration Manager est disponible et qu’elle doit être installée. Une fois que les utilisateurs installent le client, ils doivent redémarrer leur ordinateur Mac.  

 Après le redémarrage de l'ordinateur, l'Assistant Inscription d'ordinateur s'exécute automatiquement pour demander un nouveau certificat d'utilisateur. L’Assistant Inscription d’ordinateur sera automatiquement exécuté uniquement lors de la première installation du client SCCM. Et il ne sera pas réexécuté si vous essayez de mettre à jour le client avec un nouveau programme d’installation ultérieurement dans la mesure où il a déjà un certificat utilisateur valide. 

 Si vous n’utilisez pas l’inscription Configuration Manager, mais que vous installez le certificat client indépendamment de Configuration Manager, consultez [Configurer le client mis à niveau pour qu’il utilise un certificat existant](#BKMK_UpgradingClient_MachineEnrollment).  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configurer le client mis à niveau pour qu’il utilise un certificat existant  
 Exécutez la procédure suivante pour empêcher l’exécution de l’Assistant Inscription ordinateur et pour configurer le client mis à niveau afin qu’il utilise un certificat client existant.  

-   Dans la console Configuration Manager, créez un élément de configuration du type **Mac OS X**.  

-   Ajoutez un paramètre à cet élément de configuration avec le type de paramètre **Script**.  

-   Ajoutez le script suivant au paramètre :  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   Ajoutez l’élément de configuration à une base de référence de configuration, puis déployez cette dernière sur tous les ordinateurs Mac qui installent un certificat indépendamment de Configuration Manager.  

 Pour plus d’informations sur la création et le déploiement d’éléments de configuration pour des ordinateurs Mac, consultez [Comment créer des éléments de configuration pour des appareils Mac OS X gérés avec le client System Center Configuration Manager](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md) et [Comment déployer des bases de référence de configuration dans System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md).  
