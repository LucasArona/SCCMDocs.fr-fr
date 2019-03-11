---
title: Créer des applications Windows
titleSuffix: Configuration Manager
description: Découvrez-en plus sur la création et le déploiement d’applications Windows dans Configuration Manager.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: c70212962342bd254a5024c17bb292783b760233
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838869"
---
# <a name="create-windows-applications-in-configuration-manager"></a>Créer des applications Windows dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Outre les autres exigences et procédures Configuration Manager à observer pour [créer une application](/sccm/apps/deploy-use/create-applications), prenez en compte les éléments suivants au moment de créer et déployer des applications pour des appareils Windows.  



## <a name="bkmk_general"></a> Éléments généraux à prendre en compte  

Configuration Manager prend en charge le déploiement de formats de package d’application (.aspx) et d’ensemble d’applications (.appxbundle) Windows pour les appareils Windows 8.1 et Windows 10.

Quand vous créez une application dans la console Configuration Manager, sélectionnez **Package d’application Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** comme **Type** de fichier d’installation d’application. Pour plus d’informations sur la création d’applications en général, voir [Créer des applications](/sccm/apps/deploy-use/create-applications). Pour plus d’informations sur le format MSIX, voir [Prise en charge du format MSIX](#bkmk_msix). 

> [!Note]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités s’affichent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version cliente n’est pas également la plus récente.<!--SCCMDocs issue 646-->  



## <a name="bkmk_provision"></a> Provisionner les packages d’application Windows pour tous les utilisateurs sur un appareil
<!--1358310--> Depuis la version 1806, provisionnez une application avec un package d’application Windows pour tous les utilisateurs d’un appareil. Un exemple courant de ce scénario est l’approvisionnement d’une application telle que « Minecraft : Education Edition » à partir de Microsoft Store pour Entreprises et Éducation, pour tous les appareils utilisés par les étudiants d’une école. Auparavant, Configuration Manager ne prenait en charge l’installation de ces applications que pour un seul utilisateur. Quand il se connectait à un nouvel appareil, l’élève devait attendre pour accéder à une application. À présent que l’application est provisionnée pour tous les utilisateurs d’un appareil, ceux-ci peuvent l’utiliser plus rapidement.

> [!Important]  
> Sachez que l’installation, le provisionnement et la mise à jour de plusieurs versions d’un même package d’application Windows sur un appareil peut entraîner des résultats inattendus. De tels résultats peuvent être obtenus lorsque vous utilisez Configuration Manager pour provisionner l’application, et que vous permettez aux utilisateurs de mettre à jour l’application à partir de Microsoft Store. Pour plus d’informations, consultez les instructions de la section Étapes suivantes pour [gérer les applications à partir du Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Lorsque vous provisionnez une application sous licence hors connexion, Configuration Manager ne permet pas à Windows de la mettre automatiquement à jour à partir de Microsoft Store.  

Configuration Manager prend en charge le provisionnement des applications sur les versions suivantes de Windows :<!--SCCMDocs-pr issue 2762-->
- Action d’installation : Windows 10, version 1607 et ultérieure
- Action de désinstallation : Windows 10, version 1703 et ultérieure

Pour configurer un type de déploiement d’application Windows pour cette fonctionnalité, activez l’option **Provisionner cette application pour tous les utilisateurs de l’appareil**. Pour plus d’informations, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications).


> [!Note]  
> Si vous devez désinstaller une application provisionnée sur des appareils auxquels les utilisateurs se sont déjà connectés, vous devez créer deux déploiements de désinstallation. Pour le premier déploiement de désinstallation, ciblez le regroupement d’appareils qui contient les appareils en question. Pour le deuxième déploiement, ciblez le regroupement d’utilisateurs qui contient les utilisateurs déjà connectés aux appareils sur lesquels l’application est provisionnée. Lorsque vous désinstallez une application provisionnée d’un appareil, Windows ne la désinstalle pas pour les utilisateurs. 



## <a name="bkmk_msix"></a> Prise en charge du format MSIX
<!--1357427-->

Depuis la version 1806, Configuration Manager prend en charge les nouveaux formats de package d’application (.msix) et d’ensemble d’applications (.msixbundle) Windows 10. Windows 10 1809 (ou version ultérieure) prend en charge ces nouveaux formats.  

- Pour une vue d’ensemble de MSIX, voir [Examen plus poussé de MSIX](https://blogs.msdn.microsoft.com/sgern/2018/06/18/a-closer-look-at-msix/).  

- Pour savoir comment créer une application MSIX, voir [Prise en charge de MSIX introduite dans la version 17682 d’Insider](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376).  


### <a name="convert-applications-to-msix"></a>Convertir des applications en MSIX
<!--3607729, fka 1359029-->

Depuis la version 1810, vous pouvez convertir vos applications Windows Installer (.msi) existantes au format MSIX. 

#### <a name="prerequisites"></a>Prérequis
- Un appareil de référence sous Windows 10 version 1809 ou ultérieure  

- Connectez-vous à Windows sur cet appareil en tant qu’utilisateur disposant de droits d’administrateur local  

- Installez les applications suivantes sur cet appareil :  

    - Console Configuration Manager  

    - Installez [l’outil d’empaquetage MSIX](https://www.microsoft.com/store/productId/9N5LW3JBCXKF) à partir du Microsoft Store  

    - Installez le [pilote de l’outil d’empaquetage MSIX](https://docs.microsoft.com/windows/msix/packaging-tool/mpt-known-issues#msix-packaging-tool-driver-considerations)<!--SCCMDocs-pr issue #3091-->  

N’installez pas d’autres applications ou services sur cet appareil. Il s’agit de votre système de référence. 

#### <a name="process-to-convert-applications-to-msix-format"></a>Convertir des applications au format MSIX
1. Élevez la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.  

2. Sélectionnez une application qui a un type de déploiement Windows Installer (.msi).  

    > [!Note]  
    > Vous devez être en mesure d’accéder au contenu source de l’application à partir de l’appareil de référence.  
    > 
    > Le nom de l’application ne peut pas contenir de caractères spéciaux. Configuration Manager utilise le nom de l’application en tant que nom du fichier de sortie.  
    > 
    > N’installez pas cette application sur l’appareil de référence à l’avance.  

3. Sélectionnez **Convertir en .MSIX** dans le ruban.

Une fois l’Assistant terminé, l’outil d’empaquetage MSIX crée un fichier MSIX à l’emplacement spécifié dans l’Assistant. Pendant ce processus, Configuration Manager installe en mode silencieux l’application sur l’appareil de référence.

Si le processus échoue, la page de résumé pointe vers le fichier journal avec plus d’informations. S’il existe une erreur sur la capture de l’état utilisateur, déconnectez-vous de Windows. Le fait de vous reconnecter peut résoudre ce problème.

Pour utiliser cette application MSIX, vous devez d’abord la signer numériquement afin que les clients lui fassent confiance. Pour plus d’informations sur ce processus, consultez les articles suivants : 
- [MSIX – Outil d’empaquetage MSIX – signer le package MSIX](https://blogs.msdn.microsoft.com/sgern/2018/09/06/msix-the-msix-packaging-tool-signing-the-msix-package/)
- [Comment signer un package d’application à l’aide de SignTool](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

Après avoir signé l’application, créez un nouveau type de déploiement sur l’application dans Configuration Manager. Pour plus d’informations, consultez [Créer des types de déploiement pour l’application](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).




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
