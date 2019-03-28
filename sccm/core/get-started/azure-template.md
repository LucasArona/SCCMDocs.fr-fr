---
title: Créer un laboratoire dans Azure
titleSuffix: Configuration Manager
description: Automatiser la création d’un lab Configuration Manager Technical Preview avec des modèles Azure
ms.date: 03/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9875c443-19bf-43a0-9203-3a741f305096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 25283e513e256e8ce779df7b71ac6f6c17f1e370
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58196821"
---
# <a name="create-a-configuration-manager-technical-preview-lab-in-azure"></a>Créer un lab Configuration Manager Technical Preview dans Azure

*S’applique à : System Center Configuration Manager (Technical Preview)*

<!--3556017-->

Ce guide décrit comment créer un environnement lab Configuration Manager dans Microsoft Azure. Il utilise des modèles Azure pour simplifier et automatiser la création d’un lab avec des ressources Azure. Ce processus installe la dernière version de la branche Technical Preview de Configuration Manager. 

Pour plus d’informations sur la branche actuelle de Configuration Manager, consultez [Configuration Manager sur Azure](/sccm/core/understand/configuration-manager-on-azure).



## <a name="prerequisites"></a>Prérequis

Ce processus nécessite un abonnement Azure où vous pouvez créer les objets suivants : 
- Trois machines virtuelles Standard_D2s_v3
- Compte de stockage Standard_LRS

> [!Tip]  
> Pour vous aider à déterminer les coûts potentiels, consultez la [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/).  



## <a name="process"></a>Processus

1. Accédez au [modèle Configuration Manager](https://azure.microsoft.com/resources/templates/sccm-technicalpreview/).  

2. Sélectionnez **Déployer sur Azure** pour ouvrir le portail Azure.  

3. Complétez le modèle de démarrage rapide Azure avec les informations suivantes :

    - De base  

        - **Abonnement** : Nom de l’abonnement où créer les machines virtuelles  

        - **Groupe de ressources** : Sélectionnez un groupe de ressources à utiliser pour ces machines virtuelles  

        - **Emplacement** : Sélectionnez un centre de données Azure pour héberger cet environnement lab  

    - Paramètres  

        - **Préfixe** : Nom du préfixe des machines. Pour plus d’informations, consultez [Informations sur les machines virtuelles Azure](#azure-vm-info).  

        - **Nom d’utilisateur de l’administrateur** : Nom d’un utilisateur sur les machines virtuelles avec des droits d’administration. Vous utilisez cet utilisateur pour vous connecter aux machines virtuelles.  

        - **Mot de passe de l’administrateur** : Le mot de passe doit être conforme aux exigences de complexité d’Azure. Pour plus d’informations, consultez [adminPassword](https://docs.microsoft.com/rest/api/compute/virtualmachines/createorupdate#osprofile).  

    > [!Important]  
    > Les paramètres suivants sont obligatoires pour Azure. Utilisez les valeurs par défaut. Ne changez pas ces valeurs.  
    > 
    > - **\_Emplacement des artefacts** : Emplacement des scripts pour ce modèle <!-- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/sccm-technicalpreview/ -->  
    >
    > - **\_Jeton SAS d’emplacement des artefacts** : Le jeton SAS est nécessaire pour accéder à l’emplacement des artefacts  
    > 
    > - **Emplacement** : Emplacement pour toutes les ressources

4. Lisez les conditions générales. Si vous êtes d’accord, sélectionnez **J’accepte les termes et conditions mentionnés ci-dessus**. Ensuite, sélectionnez **Acheter** pour continuer. 

Azure valide les paramètres, puis le déploiement commence. Vérifiez l’état du déploiement dans le portail Azure. Le processus peut prendre de 2 à 4 heures. Même quand le portail Azure indique un déploiement réussi, les scripts de configuration de continuent de s’exécuter. Ne redémarrez pas les machines virtuelles au cours du processus.

Pour voir l’état des scripts de configuration, connectez-vous au serveur `<prefix>PS1` et consultez le fichier suivant : `%windir%\TEMP\ProvisionScript\PS1.json`. S’il indique que toutes les étapes sont terminées, c’est que le processus est terminé.

Pour vous connecter aux machines virtuelles, obtenez d’abord les adresses IP publiques de chaque machine virtuelle auprès du portail Azure. Quand vous vous connectez à la machine virtuelle, le nom de domaine est `contoso.com`. Utilisez les informations d’identification que vous avez spécifiées dans le modèle de déploiement. Pour plus d’informations, consultez [Guide pratique pour se connecter à et ouvrir une session sur une machine virtuelle Azure exécutant Windows](https://docs.microsoft.com/azure/virtual-machines/windows/connect-logon).



## <a name="azure-vm-info"></a>Informations sur les machines virtuelles Azure

Les trois machines virtuelles ont les spécifications suivantes :
- Standard_D2s_v3, qui a 2 cœurs d’UC et 8 Go de mémoire  
- Windows Server 2016 Datacenter Edition
- 150 Go d’espace disque
- Une adresse IP publique et une adresse IP privée. Les adresses IP publiques sont dans un groupe de sécurité réseau qui autorise uniquement les connexions Bureau à distance sur le port TCP 3389. 

Le préfixe que vous avez spécifié dans le modèle de déploiement est le préfixe du nom des machines virtuelles. Par exemple, si vous définissez « contoso » comme préfixe, le nom de la machine du contrôleur de domaine est `contosoDC`.


### `<prefix>DC`

Contrôleur de domaine Active Directory

#### <a name="windows-features-and-roles"></a>Rôles et fonctionnalités Windows
- Active Directory Domain Services (ADDS)
- .NET
- Compression différentielle à distance (RDC)


### `<prefix>PS1`

- SQL Server
- Windows 10 ADK avec Windows PE 
- Site principal Configuration Manager

#### <a name="windows-features-and-roles"></a>Rôles et fonctionnalités Windows
- .NET
- Compression différentielle à distance (RDC) 
- IIS (Internet Information Service)


### `<prefix>DPMP`

- Point de distribution
- Point de gestion

#### <a name="windows-features-and-roles"></a>Rôles et fonctionnalités Windows
- .NET
- Compression différentielle à distance (RDC) 
- IIS (Internet Information Service)
- Service de transfert intelligent en arrière-plan (BITS)

