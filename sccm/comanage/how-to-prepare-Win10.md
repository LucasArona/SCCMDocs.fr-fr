---
title: Cogérer les périphériques basés sur internet
titleSuffix: Configuration Manager
description: Découvrez comment préparer vos appareils basés sur internet de Windows 10 pour la cogestion.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbe26eee8b01c581776b1c134e1fe59cf4293e1a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754851"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Comment préparer les appareils basés sur internet pour la cogestion

Cet article se concentre sur le deuxième chemin d’accès à la cogestion, pour les nouveaux appareils basés sur internet. Ce scénario est lorsque vous avez de nouveaux appareils Windows 10 qui rejoindre Azure AD et l’inscrire automatiquement à Intune. Vous installez le client Configuration Manager pour atteindre un état de cogestion.  



## <a name="windows-autopilot"></a>Windows Autopilot

Pour les nouveaux appareils Windows 10, vous pouvez utiliser le service Autopilot pour configurer l’expérience OOBE (box) à l’emploi. Ce processus inclut la jonction de l’appareil à Azure AD et l’inscription de l’appareil dans Intune.  

Pour plus d’informations, consultez [vue d’ensemble de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Pour configurer vos appareils à être automatiquement inscrire dans Intune quand ils rejoignent Azure AD, consultez [les appareils Windows de s’inscrire pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Collecter des informations de Configuration Manager

À compter de la version 1802, utilisez Configuration Manager pour collecter et signaler les informations des appareils nécessaires à Microsoft Store pour Entreprises et Éducation. numéro de série, identificateur de produit Windows et identificateur matériel. Il est utilisé pour inscrire l’appareil dans le Microsoft Store pour prendre en charge de Windows Autopilot. 

1. Dans la console Configuration Manager, accédez à la **surveillance** espace de travail, développez le **Reporting** nœud, développez **rapports**, puis sélectionnez le **matériel - Général** nœud.  

2. Exécutez le rapport, **informations d’appareil Windows Autopilot**et afficher les résultats.  

3. Dans la visionneuse de rapports, sélectionnez le **exporter** icône, puis choisissez le **CSV (délimité par des virgules)** option.  

4. Après avoir enregistré le fichier, chargez les données dans Microsoft Store pour Entreprises et Éducation.  

Pour plus d’informations, consultez [ajouter des appareils dans Microsoft Store pour entreprises et Éducation](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>AutoPilot pour les périphériques existants
<!--1358333-->

[Autopilot Windows pour les périphériques existants](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) est Windows 10 disponibles, 1809 ou version ultérieure. Cette fonctionnalité vous permet de réinitialiser et approvisionner un appareil Windows 7 pour [mode pilotée par l’utilisateur de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) à l’aide d’une séquence de tâches de Configuration Manager unique et natif. 



## <a name="install-the-configuration-manager-client"></a>Installer le client Configuration Manager

Pour les appareils basés sur internet dans le deuxième chemin d’accès, vous devez créer une application dans Intune. Déployez cette application sur les appareils Windows 10 qui ne sont pas déjà, les clients Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Obtenir la ligne de commande de Configuration Manager

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**.  

2. Sélectionnez l’objet de cogestion, puis choisissez **propriétés** dans le ruban.  

3. Sur le **activation** onglet, copiez la ligne de commande. Collez-le dans le bloc-notes à enregistrer pour le processus suivant.  

La ligne de commande suivante est un exemple : `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215--> À compter de la version 1806, moins de propriétés sont maintenant nécessaires pour la ligne de commande.  

- Les propriétés de ligne de commande suivantes sont nécessaires pour tous les scénarios :  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Les propriétés suivantes sont nécessaires lorsque vous utilisez Azure AD pour l’authentification client, au lieu de certificats d’authentification client PKI :  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Si le client se reconnecte à l’intranet, la propriété suivante est requise :  
    - SMSMP  

- Si à l’aide de votre propre certificat SSL de PKI et votre liste de révocation n’est pas publié sur internet, le paramètre suivant est requis :  
    - /noCRLCheck  
    
     Pour plus d’informations, consultez [planification de révocation de certificats](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

L’exemple suivant inclut toutes ces propriétés :   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Pour plus d’informations, consultez [Propriétés de l’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Créer l’application dans Intune

1. Accédez à la [Azure portal](https://portal.azure.com), puis ouvrez la page Intune.  

2. Sélectionnez **les applications clientes** > **applications** > **ajouter**.  

3. Dans la section **Autre**, sélectionnez **Application métier**.  

4. Télécharger le **ccmsetup.msi** fichier package d’application. Ce fichier se trouve dans le dossier suivant sur le Gestionnaire de Configuration de serveur de site : `<ConfigMgr installation directory>\bin\i386`.  

5. Après la mise à jour de l’application, configurez les informations de l’application avec la ligne de commande que vous avez copiée à partir du Gestionnaire de Configuration.  

> [!IMPORTANT]    
> Si vous personnalisez la ligne de commande, assurez-vous qu’il n’est pas supérieure à 1 024 caractères. Lorsque la longueur de ligne de commande est supérieure à 1024 caractères, l’installation du client échoue.


