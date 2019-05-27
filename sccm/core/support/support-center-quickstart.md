---
title: Démarrage rapide du Centre d’aide et de support
titleSuffix: Configuration Manager
description: Capturez rapidement l’état d’un client Configuration Manager pour le dépannage.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f63193f9d4c9c754a56186f7a36cb9fabaf95725
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500728"
---
# <a name="support-center-quickstart-guide"></a>Guide de démarrage rapide du Centre d’aide et de support

*S’applique à : System Center Configuration Manager (Current Branch)*

Le Centre d’aide et de support présente des fonctionnalités puissantes, notamment la résolution des problèmes et l’affichage des journaux en temps réel. Il peut aussi être utilisé pour capturer l’état d’un ordinateur client Configuration Manager en quelques minutes seulement. Cette capacité inclut l’accès aux clients distants.

Créez un fichier de *groupe de résolution des problèmes* (.zip) qui capture l’état du client. Ce groupe ne contient pas uniquement les fichiers journaux. Il peut inclure d’autres types de données tels que des paramètres du Registre et des configurations de client. Fournissez ce groupe à un technicien du support qui utilise la visionneuse du Centre d’aide et de support.



## <a name="prerequisites"></a>Prérequis

- Droits administratifs locaux sur un client Configuration Manager  

- Programme d’installation du Centre d’aide et de support. Ce fichier se trouve sur le serveur de site à l’adresse `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Pour plus d’informations, consultez [Centre d’aide et de support - Installer](/sccm/core/support/support-center#install).  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Étape 1 : Créer un bundle de données sur un client local

1.  Installez le Centre d’aide et de support sur le client Configuration Manager.  

2.  Accédez au menu **Démarrer**, dans le groupe **Microsoft System Center**, sélectionnez **Centre d’aide et de support**.  

3.  Sous l’onglet Accueil du ruban, sélectionnez **Collecter les données sélectionnées**. Par défaut, le Centre d’aide et de support collecte uniquement le jeu de données minimal : fichiers journaux, configuration du client et système d’exploitation.  

4.  Enregistrez le fichier du groupe de résolution des problèmes (.zip) dans un dossier sur l’ordinateur. Par défaut, le nom de fichier est semblable à l’exemple suivant : `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Étape 2 : afficher le groupe de données à l’aide de la visionneuse du Centre d’aide et de support

1.  Démarrez la **visionneuse du Centre d'aide et de support**. Cette action peut se produire sur n’importe quel ordinateur où vous installez le Centre d’aide et de support.  

2.  Sélectionnez **Ouvrir le groupe**, accédez au fichier de groupe, puis sélectionnez **Ouvrir**.  

3.  Une fois que la visionneuse du Centre d’aide et de support a traité le fichier, accédez à chaque onglet disponible. Affichez les types de données que le Centre d’aide et de support collecte par défaut :  

    - **Configuration**  

        - Configuration du client Configuration Manager  

        - Système d'exploitation  

        - Ordinateur  

        - Services  

        - Cartes réseau  

    - **Journaux** : choisissez une ou plusieurs entrées dans la liste, puis sélectionnez **Ouvrir**. Cette action ouvre les fichiers journaux sélectionnés dans la visionneuse du journal. Utilisez cette fonctionnalité pour rechercher des codes d’erreur et utilisez des filtres avancés pour analyser plus rapidement les fichiers journaux.  



## <a name="collect-more-data"></a>Collecter des données supplémentaires

Outre ces fonctionnalités de base, le Centre d'aide et de support peut également collecter plusieurs autres informations sur l'état du client. Ouvrez le **Centre d’aide et de support** et sélectionnez **Collecter toutes les données**. Ce processus dure généralement plusieurs minutes, même sur des ordinateurs neufs. Le Centre d’aide et de support collecte les données supplémentaires suivantes :

  - **Stratégie** : collecte les paramètres de stratégie de Configuration Manager, à la fois pour la configuration de la stratégie demandée et la configuration de la stratégie réelle  

  - **Certificats** : informations de clé publique des certificats clients. Le Centre d’aide et de support ne collecte pas les clés privées de certificat.  

  - **Registre de client** : informations de configuration client du Registre. Le Centre d’aide et de support collecte uniquement les informations de Registre de Configuration Manager.  

  - **WMI client** : informations de configuration de client de WMI. Le Centre d’aide et de support ne collecte pas la stratégie client.  

  - **Résolution des problèmes** : données de dépannage en temps réel qui vous permettent de diagnostiquer les problèmes client courants liés à Active Directory, aux points de gestion, au réseau, aux attributions de stratégies et à l’inscription.  

  - **Vidages de débogage** : effectuez le vidage de débogage des processus clients et connexes. Les vidages de débogage peuvent être de grande ampleur. Activez cette option uniquement lors de la résolution de problèmes de performances du client.  

