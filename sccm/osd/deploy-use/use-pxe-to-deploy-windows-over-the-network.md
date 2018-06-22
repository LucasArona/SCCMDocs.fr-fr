---
title: Utiliser PXE pour le déploiement de système d’exploitation sur le réseau
titleSuffix: Configuration Manager
description: Utilisez des déploiements de système d’exploitation lancés par PXE pour actualiser le système d’exploitation d’un ordinateur ou installer une nouvelle version de Windows sur un nouvel ordinateur.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: da5f8b61-2386-4530-ad54-1a5c51911f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: deb8321400eac4085cefca8686f2703cea5f659a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351596"
---
# <a name="use-pxe-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Utiliser PXE pour déployer Windows sur le réseau avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements de système d’exploitation lancés par l’environnement PXE (Preboot Execution Environment) dans Configuration Manager permettent aux clients de demander et de déployer des systèmes d’exploitation sur le réseau. Dans ce scénario de déploiement, vous envoyez l’image de système d’exploitation et les images de démarrage à un point de distribution PXE.

> [!NOTE]  
>  Quand vous créez un déploiement de système d’exploitation qui cible seulement des ordinateurs avec un BIOS x64, les deux images de démarrage x64 et x86 doivent être disponibles sur le point de distribution.

Vous pouvez utiliser les déploiements de système d’exploitation lancés par PXE dans les scénarios suivants :

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

Effectuez les étapes de l’un des scénarios de déploiement de système d’exploitation, puis utilisez les sections de cet article pour préparer les déploiements lancés par PXE.



##  <a name="BKMK_Configure"></a> Configurer au moins un point de distribution qui peut répondre aux demandes PXE
Pour déployer des systèmes d’exploitation sur des clients Configuration Manager qui effectuent des demandes de démarrage PXE, vous devez configurer un ou plusieurs points de distribution pour accepter les demandes PXE. Une fois le point de distribution configuré, il répond aux demandes de démarrage PXE et détermine l’action de déploiement appropriée. Pour plus d’informations, consultez [Installer ou modifier un point de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#pxe).  



## <a name="prepare-a-pxe-enabled-boot-image"></a>Préparer une image de démarrage compatible PXE
Pour utiliser PXE afin de déployer un système d’exploitation, vous avez besoin d’images de démarrage PXE x86 et x64 qui sont distribuées à un ou plusieurs points de distribution PXE. Utilisez les informations pour activer PXE sur une image de démarrage et distribuez l’image de démarrage sur des points de distribution :

-   Pour activer PXE sur une image de démarrage, sélectionnez **Déployer cette image de démarrage depuis le point de distribution PXE** sous l’onglet **Source de données** dans les propriétés de l’image de démarrage.

-   Si vous modifiez les propriétés de l’image de démarrage, redistribuez-la sur les points de distribution. Pour plus d’informations, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).



##  <a name="BKMK_PXEExclusionList"></a> Créer une liste d’exclusion pour les déploiements PXE
Si vous utilisez PXE pour déployer des systèmes d’exploitation, vous pouvez créer des listes d’exclusion sur chaque point de distribution. Ajoutez les adresses MAC à la liste d’exclusion des ordinateurs qui doivent être ignorés par le point de distribution. Les ordinateurs répertoriés ne reçoivent pas les séquences de tâches de déploiement que Configuration Manager utilise pour le déploiement PXE.

#### <a name="to-create-the-exclusion-list"></a>Pour créer la liste d'exclusion

1.  Créez un fichier texte sur le point de distribution qui est activé pour PXE. Par exemple, nommez ce fichier texte **pxeExceptions.txt**.

2.  Utilisez un éditeur de texte brut, tel que le bloc-notes, et ajoutez les adresses MAC des ordinateurs qui doivent être ignorés par le point de distribution compatible PXE. Séparez les valeurs des adresses MAC par un signe deux-points et entrez chaque adresse sur une ligne distincte. Exemple : `01:23:45:67:89:ab`.

3.  Enregistrez le fichier texte sur le serveur de système de site du point de distribution compatible PXE. Le fichier texte peut être enregistré dans n'importe quel emplacement sur le serveur.

4.  Modifiez le registre du point de distribution compatible PXE pour créer une clé de registre **MACIgnoreListFile**. Ajoutez la valeur de chaîne du chemin complet pour le fichier texte sur le serveur de système de site du point de distribution compatible PXE. Utilisez les chemins d'accès au Registre suivants :

     **HKLM\Software\Microsoft\SMS\DP**  

    > [!WARNING]  
    >  Une utilisation incorrecte de l'Éditeur du Registre peut éventuellement provoquer de graves problèmes, lesquels nécessitent parfois la réinstallation complète du système d'exploitation. Microsoft ne garantit pas la résolution des erreurs résultant d'une utilisation incorrecte de l'Éditeur du Registre. Les opérations exécutées dans l'Éditeur du Registre le sont à vos propres risques.

     Il est inutile de redémarrer le serveur après avoir effectué cette modification au niveau du Registre.



## <a name="manage-duplicate-hardware-identifiers"></a>Gérer les identificateurs de matériel dupliqués
Configuration Manager peut reconnaître plusieurs ordinateurs comme un même appareil s’ils ont des attributs SMBIOS en double ou si vous utilisez une carte réseau partagée. Vous pouvez éviter ces problèmes en gérant les identificateurs de matériel en double dans les paramètres de hiérarchie. Pour plus d’informations, consultez [Gérer les identificateurs de matériel dupliqués](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).



##  <a name="BKMK_RamDiskTFTP"></a>Taille de bloc et de fenêtre RamDisk TFTP
Vous pouvez personnaliser les tailles de bloc et de fenêtre TFTP RamDisk pour des points de distribution compatibles PXE. Si vous avez personnalisé votre réseau, une taille importante de bloc ou de fenêtre peut entraîner l’échec du téléchargement de l’image de démarrage avec une erreur d’expiration de délai. La personnalisation des tailles de bloc et de fenêtre TFTP RamDisk permet d’optimiser le trafic TFTP quand vous utilisez PXE pour répondre aux besoins spécifiques de votre réseau. Pour déterminer la configuration la plus efficace, testez les paramètres personnalisés dans votre environnement. Pour plus d’informations, voir [Personnalisation des tailles de bloc et de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).



## <a name="configure-deployment-settings"></a>Configurer les paramètres de déploiement
Pour utiliser un déploiement de système de d’exploitation lancé par PXE, configurez le déploiement pour rendre le système d’exploitation accessible aux demandes de démarrage PXE. Configurer les systèmes d’exploitation disponibles sous l’onglet **Paramètres de déploiement** dans les propriétés de déploiement. Pour le paramètre **Rendre disponible aux éléments suivants**, sélectionnez l’une des options suivantes :

-   Clients, média et environnement PXE Configuration Manager

-   Média et environnement PXE uniquement

-   Média et environnement PXE uniquement (masqué)



##  <a name="BKMK_Deploy"></a> Déployer la séquence de tâches
Déployez le système d’exploitation sur un regroupement cible. Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quand vous déployez des systèmes d’exploitation à l’aide de PXE, vous pouvez configurer si le déploiement est obligatoire ou disponible.

-   **Déploiement obligatoire**: les déploiements obligatoires utilisent PXE et ne nécessitent aucune intervention de l’utilisateur. L’utilisateur ne peut pas contourner le démarrage PXE. Toutefois, si l’utilisateur annule le démarrage PXE avant que le point de distribution réponde, le système d’exploitation n’est pas déployé.

-   **Déploiement disponible** : Les déploiements disponibles nécessitent l’intervention de l’utilisateur sur l’ordinateur de destination. L’utilisateur doit appuyer sur la touche F12 pour continuer le processus de démarrage PXE. Sinon, l’ordinateur démarre dans le système d’exploitation actuel ou à partir du périphérique de démarrage suivant disponible.

Vous pouvez redéployer un déploiement PXE requis en désactivant l'état du dernier déploiement PXE affecté à un ordinateur ou à un regroupement Configuration Manager. Pour plus d’informations sur l’action **Effacer les déploiements PXE obligatoires**, consultez [Gérer les clients](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) ou [Gérer les regroupements](/sccm/core/clients/manage/collections/manage-collections#how-to-manage-device-collections). Cette action réinitialise l'état de ce déploiement et installe de nouveau les déploiements requis les plus récents.

> [!IMPORTANT]
> Le protocole PXE n'est pas sécurisé. Assurez-vous que le serveur PXE et le client PXE se trouvent sur un réseau sécurisé physiquement, tel qu'un centre de données, afin d'éviter l'accès non autorisé à votre site.



##  <a name="how-is-the-boot-image-selected-for-clients-booting-with-pxe"></a>Comment l’image de démarrage est-elle sélectionnée pour les clients qui démarrent avec PXE ?
Lorsqu’un client démarre avec PXE, Configuration Manager lui fournit une image de démarrage à utiliser. Configuration Manager utilise une image de démarrage avec une correspondance exacte d’architecture. Si une image de démarrage avec correspondance exacte d’architecture n’est pas disponible, Configuration Manager utilise une image de démarrage avec une architecture compatible. La liste ci-dessous indique de quelle manière une image de démarrage est sélectionnée pour les clients qui démarrent avec PXE.
1. Configuration Manager recherche dans la base de données du site l’enregistrement système qui correspond à l’adresse MAC ou au SMBIOS du client qui essaie de démarrer.  

    > [!NOTE]
    > Si un ordinateur qui est affecté à un site démarre via PXE pour un site différent, les stratégies ne sont pas visibles pour l’ordinateur. Par exemple, si un client est déjà attribué au site A, le point de gestion et le point de distribution sur le site B ne peuvent pas accéder aux stratégies du site A. Le client ne peut pas effectuer de démarrage PXE.

2. Configuration Manager recherche les séquences de tâches qui sont déployées sur l’enregistrement système trouvé à l’étape 1.

3. Dans la liste des séquences de tâches trouvées à l’étape 2, Configuration Manager recherche une image de démarrage qui correspond à l’architecture du client qui tente de démarrer. Si une image de démarrage est trouvée avec la même architecture, celle-ci est utilisée.

4. Si une image de démarrage n’est pas trouvée avec la même architecture, Configuration Manager recherche une image de démarrage qui soit compatible avec l’architecture du client. Il recherche dans la liste des séquences de tâches trouvées à l’étape 2. Par exemple, un client 64 bits est compatible avec des images de démarrage 32 bits et 64 bits. Un client 32 bits est compatible uniquement avec des images de démarrage 32 bits. Un client UEFI est compatible uniquement avec des images de démarrage 64 bits.
