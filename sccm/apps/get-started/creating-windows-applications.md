---
title: Créer des applications Windows
titleSuffix: Configuration Manager
description: Découvrez-en plus sur la création et le déploiement d’applications Windows dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 38732081ce27fde764f7d47a565ce1211cef1f54
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383552"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Créer des applications Windows dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Outre les autres exigences et procédures Configuration Manager à observer pour [créer une application](/sccm/apps/deploy-use/create-applications), prenez en compte les éléments suivants au moment de créer et déployer des applications pour des appareils Windows.  



## <a name="bkmk_general"></a> Éléments généraux à prendre en compte  

Configuration Manager prend en charge le déploiement de formats de package d’application (.aspx) et d’ensemble d’applications (.appxbundle) Windows pour les appareils Windows 8.1 et Windows 10.

Depuis la version 1806, Configuration Manager prend également en charge les nouveaux formats de package d’application (.msix) et d’ensemble d’applications (.msixbundle) Windows 10. Les dernières versions de [Windows Insider Preview](https://insider.windows.com/) prennent en charge ces nouveaux formats.<!--1357427-->  

- Pour une vue d’ensemble de MSIX, voir [Examen plus poussé de MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Pour savoir comment créer une application MSIX, voir [Prise en charge de MSIX introduite dans la version 17682 d’Insider](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  

Quand vous créez une application dans la console Configuration Manager, sélectionnez **Package d’application Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** comme **Type** de fichier d’installation d’application. Pour plus d’informations, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications). 

> [!Note]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités s’affichent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version cliente n’est pas également la plus récente.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Provisionner les packages d’application Windows pour tous les utilisateurs sur un appareil
<!--1358310--> Depuis la version 1806, provisionnez une application avec un package d’application Windows pour tous les utilisateurs d’un appareil. Un exemple courant de ce scénario est le provisionnement d’une application telle que « Minecraft : Education Edition » à partir de Microsoft Store pour Entreprises et Éducation, pour tous les appareils utilisés par les élèves d’une école. Auparavant, Configuration Manager ne prenait en charge l’installation de ces applications que pour un seul utilisateur. Quand il se connectait à un nouvel appareil, l’élève devait attendre pour accéder à une application. À présent que l’application est provisionnée pour tous les utilisateurs d’un appareil, ceux-ci peuvent l’utiliser plus rapidement.

> [!Important]  
> Sachez que l’installation, le provisionnement et la mise à jour de plusieurs versions d’un même package d’application Windows sur un appareil peut entraîner des résultats inattendus. De tels résultats peuvent être obtenus lorsque vous utilisez Configuration Manager pour provisionner l’application, et que vous permettez aux utilisateurs de mettre à jour l’application à partir de Microsoft Store. Pour plus d’informations, consultez les instructions de la section Étapes suivantes pour [gérer les applications à partir du Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Lorsque vous provisionnez une application sous licence hors connexion, Configuration Manager ne permet pas à Windows de la mettre automatiquement à jour à partir de Microsoft Store.  

Configuration Manager prend en charge le provisionnement des applications sur les versions suivantes de Windows :<!--SCCMDocs-pr issue 2762-->
- Action d’installation : Windows 10, versions 1607 et ultérieures
- Action de désinstallation : Windows 10, versions 1703 et ultérieures

Pour configurer un type de déploiement d’application Windows pour cette fonctionnalité, activez l’option **Provisionner cette application pour tous les utilisateurs de l’appareil**. Pour plus d’informations, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications).


> [!Note]  
> Si vous devez désinstaller une application provisionnée sur des appareils auxquels les utilisateurs se sont déjà connectés, vous devez créer deux déploiements de désinstallation. Pour le premier déploiement de désinstallation, ciblez le regroupement d’appareils qui contient les appareils en question. Pour le deuxième déploiement, ciblez le regroupement d’utilisateurs qui contient les utilisateurs déjà connectés aux appareils sur lesquels l’application est provisionnée. Lorsque vous désinstallez une application provisionnée d’un appareil, Windows ne la désinstalle pas pour les utilisateurs. 



## <a name="bkmk_uwp"></a> Prise en charge des applications de plateforme Windows universelle (UWP)  

Les appareils Windows 10 n’ont pas besoin d’une clé de chargement indépendant pour installer des applications métier. Toutefois, pour activer le chargement indépendant sur Windows, la clé de Registre `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` doit avoir la valeur **1**.  

Si vous ne configurez pas cette clé de Registre, Configuration Manager lui affecte automatiquement la valeur **1** la première fois que vous déployez une application sur l’appareil. Si vous avez défini cette valeur sur **0**, Configuration Manager ne peut pas changer automatiquement la valeur et le déploiement de vos applications métier échoue.  

Signez numériquement les applications métier UWP. Utilisez un certificat de signature de code qui est approuvé sur chaque appareil sur lequel vous déployez l’application. Utilisez des certificats de l’infrastructure à clé publique de votre organisation ou achetez un certificat auprès d’un fournisseur tiers dont le certificat racine public est déjà approuvé par Windows.  

Pour signer des packages d’application mobile, utilisez le tableau suivant afin de déterminer le type de certificat de signature de code à utiliser :

| Package  | Symantec  | Non-Symantec  |
|---------|---------|---------|
| Packages **.appx** universels sur les appareils Windows 10 Mobile | Oui | Oui |
| Packages **.xap** | Oui | Non | 
| Packages **.appx** générés pour Windows Phone 8.1 à installer sur les appareils Windows 10 Mobile | Oui | Non | 



## <a name="bkmk_mdm-msi"></a> Déployer des applications Windows Installer sur des appareils Windows 10 inscrits à MDM  

Le type de déploiement **Windows Installer via MDM (\*.msi)** vous permet de créer et déployer des applications Windows Installer sur des appareils inscrits à MDM qui exécutent Windows 10.  

Quand vous utilisez ce type de déploiement, considérez les points suivants :    

-   Ne téléchargez qu’un seul fichier avec l’extension MSI.  

-   Configuration Manager utilise le code de produit et la version de produit du fichier pour la détection d’applications.  

-   Windows utilise le comportement de redémarrage par défaut de l’application. Configuration Manager ne contrôle pas le comportement de redémarrage de l’application.  

-   Les packages MSI par utilisateur sont installés pour un seul utilisateur.  

-   Les packages MSI par ordinateur sont installés pour tous les utilisateurs de l’appareil.  

-   Configuration Manager prend en charge les mises à jour d’application. Le code de produit MSI de chaque version doit être le même.  
