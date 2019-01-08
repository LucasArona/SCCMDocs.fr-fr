---
title: Configurer les ports de communication des clients
titleSuffix: Configuration Manager
description: Configurez les ports de communication des clients dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 84d8be8b8f00edd541425bd0e94f7411c45dab55
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422128"
---
# <a name="how-to-configure-client-communication-ports-in-system-center-configuration-manager"></a>Comment configurer les ports de communication des clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez modifier les numéros des ports de demande utilisés par les clients System Center Configuration Manager pour communiquer avec les systèmes de site qui utilisent des protocoles HTTP et HTTPS pour les communications. Même si les protocoles HTTP ou HTTPS sont sans doute déjà configurés pour les pare-feu, une notification de client utilisant le protocole HTTP ou HTTPS consomme plus de ressources processeur et de mémoire sur l'ordinateur du point de gestion qu'en utilisant un numéro de port personnalisé. Vous pouvez également spécifier le numéro de port de site à utiliser si vous réveillez les clients à l'aide de paquets de réveil traditionnels.  

 Lorsque vous spécifiez les ports de demande HTTP et HTTPS, vous pouvez spécifier un numéro de port par défaut et un autre numéro de port. Les clients essaient automatiquement le port alternatif après un échec de communication avec le port par défaut. Vous pouvez spécifier des paramètres pour la communication de données HTTP et HTTPS.  

 Les valeurs par défaut des ports de demande client sont **80** pour le trafic HTTP et **443** pour le trafic HTTPS. Modifiez-les uniquement si vous ne souhaitez pas utiliser ces valeurs par défaut. Un exemple typique d'utilisation des ports personnalisés est lorsque vous utilisez un site Web personnalisé dans IIS, plutôt que le site Web par défaut. Si vous modifiez les numéros de port par défaut pour le site Web par défaut dans IIS et que d'autres applications utilisent également le site Web par défaut, ils sont susceptibles d'échouer.  

> [!IMPORTANT]
>  Avant de modifier des numéros de port dans Configuration Manager, pensez aux conséquences. Exemples :  
> 
> - Si vous changez les numéros de port des services de demande client en tant que configuration du site et que des clients existants ne sont pas reconfigurés de façon à utiliser les nouveaux numéros de port, ceux-ci ne seront pas gérés.  
>   -   Avant de configurer un numéro de port non défini par défaut, assurez-vous que les pare-feu et tous les périphériques réseau intermédiaires peuvent prendre en charge cette configuration, puis effectuez la reconfiguration en conséquence. Si vous allez gérer des clients sur Internet et modifier le numéro de port HTTPS par défaut 443, les routeurs et les pare-feu d'Internet pourraient bloquer cette communication.  

 Pour vous assurer que les clients ne sont pas non gérés après la modification des numéros de port de demande, les clients doivent être configurés pour utiliser les nouveaux numéros de port de demande. Lorsque vous modifiez les ports de requêtes sur un site principal, tout site secondaire associé héritera automatiquement de la même configuration de port. Utilisez la procédure décrite dans cette rubrique pour configurer les ports de requêtes sur le site principal.  

> [!NOTE]  
>  Pour plus d’informations sur la façon de configurer les ports de demande pour les clients sur les ordinateurs qui exécutent Linux et UNIX, consultez [Configurer des ports de demande pour le client pour Linux et UNIX](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Lorsque le site Configuration Manager est publié dans les services de domaine Active Directory, les nouveaux clients et les clients existants qui peuvent accéder à ces informations seront automatiquement configurés avec leurs paramètres de port du site. Vous ne devez effectuer aucune opération ultérieure. Les clients qui ne peuvent pas accéder à ces informations publiées dans les services de domaine Active Directory incluent les clients des groupes de travail, les clients d'une autre forêt Active Directory, les clients configurés pour la gestion Internet uniquement et les clients qui se trouvent actuellement sur Internet. Si vous modifiez les numéros de ports par défaut après l'installation de ces clients, réinstallez-les et installez tout nouveau client à l'aide de l'une des méthodes suivantes :  

- Réinstallez les clients en utilisant l'Assistant Installation poussée du client. L'Installation poussée du client configure automatiquement les clients avec la configuration de port de site en cours. Pour plus d’informations sur l’utilisation de l’Assistant Installation Push du client, consultez [Guide pratique pour installer des clients Configuration Manager à l’aide d’une installation Push](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

- Réinstallez les clients à l'aide du programme CCMSetup.exe ainsi que les propriétés d'installation du client.msi de CCMHTTPPORT et CCMHTTPSPORT. Pour plus d’informations sur ces propriétés, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

- Réinstallez les clients à l'aide d'une méthode qui permet de rechercher les propriétés d'installation du client Configuration Manager dans les Services de domaine Active Directory. Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  Pour reconfigurer les numéros de port de clients existants, vous pouvez également utiliser le script PORTSWITCH.VBS fourni avec le support d'installation dans le dossier SMSSETUP\Tools\PortConfiguration .  

> [!IMPORTANT]  
>  Pour les clients existants et les nouveaux clients sur Internet, vous devez configurer les numéros de port par défaut en utilisant les propriétés CCMSetup.exe client.msi de CCMHTTPPORT et CCMHTTPSPORT.  

 Après avoir modifié les ports de demande sur le site, les nouveaux clients installés à l'aide de la méthode d'installation poussée du client à l'échelle du site seront automatiquement configurés avec les numéros de port du site en cours.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>Pour configurer les numéros de port de communication client pour un site  

1. Dans la console Configuration Manager, cliquez sur **Administration**.  

2. Dans l'espace de travail **Administration** développez **Configuration du site**, cliquez sur **Sites**et sélectionnez le site principal à configurer.  

3. Dans l'onglet **Accueil** , cliquez sur **Propriétés**, puis sur l'onglet **Ports** .  

4. Sélectionnez l'un des éléments et cliquez sur l'icône Propriétés pour ouvrir la boîte de dialogue **Détails du port** .  

5. Dans la boîte de dialogue **Détails du port** , spécifiez le numéro de port et la description de l'élément et cliquez sur **OK**.  

6. Sélectionnez **Utiliser un site Web personnalisé** si vous souhaitez utiliser le nom du site Web personnalisé de **SMSWeb** pour les systèmes de site qui exécutent IIS.  

7. Cliquez sur **OK** pour fermer la boîte de dialogue des propriétés du site.  

   Répétez cette procédure pour tous les sites principaux de la hiérarchie.
