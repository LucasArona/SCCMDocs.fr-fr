---
title: Cogérer des appareils basés sur Internet
titleSuffix: Configuration Manager
description: Découvrez comment préparer vos appareils Windows 10 basés sur Internet pour la cogestion.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31779b3588617816df4309461ed7715b20b0abd4
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "57558029"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Guide pratique pour préparer des appareils basés sur Internet pour la cogestion

Cet article se concentre sur le deuxième chemin de la cogestion, destinée aux nouveaux appareils basés sur Internet. Ce scénario se présente quand vous avez de nouveaux appareils Windows 10 qui rejoignent Azure AD et qui s’inscrivent automatiquement à Intune. Vous installez le client Configuration Manager pour atteindre un état de cogestion.  



## <a name="windows-autopilot"></a>Windows Autopilot

Pour les nouveaux appareils Windows 10, vous pouvez utiliser le service Autopilot pour configurer OOBE (Out-of-Box Experience). Ce processus inclut la jonction de l’appareil à Azure AD et son inscription à Intune.  

Pour plus d’informations, consultez [Vue d’ensemble de Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Pour configurer vos appareils afin qu’ils s’inscrivent automatiquement à Intune quand ils rejoignent Azure AD, consultez  [Inscrire des appareils Windows pour Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Collecter des informations à partir de Configuration Manager

À compter de la version 1802, utilisez Configuration Manager pour collecter et signaler les informations des appareils nécessaires à Microsoft Store pour Entreprises et Éducation. numéro de série, identificateur de produit Windows et identificateur matériel. Ces informations sont utilisées pour inscrire l’appareil dans le Microsoft Store afin de prendre en charge Windows Autopilot. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Supervision**, développez le nœud **Création de rapports**, puis **Rapports**, et sélectionnez le nœud **Matériel - Général**.  

2. Exécutez le rapport **Informations d’appareil Windows AutoPilot**, puis affichez les résultats.  

3. Dans la visionneuse de rapports, sélectionnez l’icône **Exporter**, puis choisissez l’option **CSV (délimité par des virgules)**.  

4. Après avoir enregistré le fichier, chargez les données dans Microsoft Store pour Entreprises et Éducation.  

Pour plus d’informations, consultez [Ajouter des appareils dans le Microsoft Store pour Entreprises et Éducation](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>Autopilot pour les appareils existants
<!--1358333-->

[Windows Autopilot pour les appareils existants](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) est disponible dans Windows 10 version 1809 ou une version ultérieure. Cette fonctionnalité permet de réimager et d’approvisionner un appareil Windows 7 pour [Windows Autopilot en mode piloté par l’utilisateur](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) en une seule séquence de tâches Configuration Manager native. 

Pour plus d’informations, consultez [Séquence de tâches Windows Autopilot pour les appareils existants](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).



## <a name="install-the-configuration-manager-client"></a>Installer le client Configuration Manager

Dans le deuxième chemin, pour les appareils basés sur Internet, vous devez créer une application dans Intune. Déployez cette application pour les appareils Windows 10 qui ne sont pas encore des clients Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Obtenir la ligne de commande de Configuration Manager

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**.  

2. Sélectionnez l’objet de cogestion, puis choisissez **Propriétés** dans le ruban.  

3. Sous l’onglet **Activation**, copiez la ligne de commande. Collez-la dans le Bloc-notes afin de l’enregistrer pour le prochain processus.  

La ligne de commande suivante est un exemple : `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215-->
À compter de la version 1806, moins de propriétés de ligne de commande sont nécessaires.  

- Les propriétés de ligne de commande suivantes sont nécessaires pour tous les scénarios :  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Les propriétés suivantes sont nécessaires lorsque vous utilisez Azure AD pour l’authentification client, au lieu de certificats d’authentification client PKI :  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Si le client revient à l’intranet, la propriété suivante est nécessaire :  
    - SMSMP  

- Si vous utilisez votre propre certificat SSL PKI et que votre liste de révocation de certificats n’est pas publiée sur Internet, le paramètre suivant est nécessaire :  
    - /noCRLCheck  
    
     Pour plus d’informations, consultez [Planification des listes de révocation de certificats](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed).  

À partir de la version 1810, le site publie des informations Azure AD supplémentaires sur la passerelle de gestion cloud (CMG). Un client joint à un Azure AD obtient ces informations à partir de la passerelle CMG pendant le processus ccmsetup, à l’aide du même locataire que celui auquel il est joint. Ce comportement simplifie davantage l’inscription d’appareils à la cogestion dans un environnement avec plusieurs locataires Azure AD. Maintenant les deux seules propriétés ccmsetup requises sont **CCMHOSTNAME** et **SMSSiteCode**.<!--3607731-->

> [!Note]
> Si vous déployez déjà le client Configuration Manager à partir d’Intune, mettez à jour l’application Intune avec une nouvelle ligne de commande et le nouveau MSI. <!-- SCCMDocs-pr issue 3084 -->

L’exemple suivant comprend toutes ces propriétés :   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Pour plus d’informations, consultez [Propriétés de l’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Créer l’application dans Intune

1. Accédez au [portail Azure](https://portal.azure.com), puis ouvrez la page Intune.  

2. Sélectionnez **Applications clientes** > **Applications** > **Ajouter**.  

3. Dans la section **Autre**, sélectionnez **Application métier**.  

4. Chargez le fichier de package d’application **ccmsetup.msi**. Recherchez ce fichier dans le dossier suivant sur le serveur de site Configuration Manager : `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Quand vous mettez à jour le site, vérifiez que vous mettez également à jour cette application dans Intune.  

5. Une fois l’application mise à jour, configurez les informations de l’application avec la ligne de commande que vous avez copiée à partir de Configuration Manager.  

> [!IMPORTANT]    
> Si vous personnalisez cette ligne de commande, vérifiez qu’elle ne contient pas plus de 1 024 caractères. Quand la ligne de commande comprend plus de 1 024 caractères, l’installation du client échoue.


