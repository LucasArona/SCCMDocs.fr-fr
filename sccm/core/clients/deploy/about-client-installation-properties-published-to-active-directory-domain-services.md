---
title: Propriétés d’installation du client dans les services de domaine Active Directory
titleSuffix: Configuration Manager
description: Utilisez les propriétés d’installation du client publiées dans les services de domaine Active Directory dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 585aa6ea6874ac6d6a5264b0f75d8dbcf39ddd0a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334281"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous étendez le schéma Active Directory pour System Center Configuration Manager et que le site est publié dans les services de domaine Active Directory, de nombreuses propriétés d’installation du client sont publiées dans les services de domaine Active Directory. Si un ordinateur peut localiser ces propriétés d'installation du client, il peut les utiliser au cours du déploiement du client Configuration Manager.  

 Les avantages de l'utilisation des services de domaine Active Directory pour publier les propriétés d'installation du client sont les suivants :  

-   Les installations du client basées sur des points de mise à jour logicielle et sur une stratégie de groupe ne nécessitent pas la configuration de paramètres d’installation sur chaque ordinateur.  

-   Ces informations étant générées automatiquement, le risque d'erreur humaine propre à la saisie manuelle des propriétés d'installation est éliminé.  

> [!NOTE]  
>  Pour plus d’informations sur la façon d’étendre le schéma Active Directory pour Configuration Manager et de publier un site, consultez [Extensions de schéma pour System Center Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Propriétés d’installation du client publiées dans les services de domaine Active Directory  
Voici une liste de propriétés d’installation du client. Pour plus d’informations sur chaque élément répertorié ci-dessous, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

-   Code de site Configuration Manager.  

-   Certificat de signature du serveur de site.  

-   Clé racine approuvée.  

-   Ports de communication client pour HTTP et HTTPS.  

-   Point d'état de secours. Si le site a plusieurs points d’état de secours, seul le premier qui a été installé est publié dans les services de domaine Active Directory.  

-   Un paramètre pour indiquer que le client doit communiquer à l'aide de HTTPS uniquement.  

-   Paramètres relatifs aux certificats PKI :  

   -   Si vous souhaitez utiliser un certificat PKI du client.  

   -   Critères de sélection des certificats. Ceci peut être nécessaire dans le cas où le client a plusieurs certificats PKI valides qui peuvent être utilisés pour Configuration Manager.  

   -   Un paramètre pour déterminer le certificat à utiliser si le client possède plusieurs certificats valides après le processus de sélection de certificat.  

   -   Liste d'émetteurs de certificats qui contient une liste de certificats d'autorité de certification racine de confiance.  

-   Propriétés d'installation client.msi qui sont définies sous l'onglet **Client** de la boîte de dialogue **Propriétés de l'installation poussée du client** .

L’installation du client (CCMSetup) utilise les propriétés publiées dans les services de domaine Active Directory seulement si aucune autre propriété n’est spécifiée selon une des méthodes suivantes :  

-   La méthode d’installation manuelle (décrite plus loin dans cet article).

-   La méthode d’installation via la stratégie de groupe (décrite plus loin dans cet article).

> [!NOTE]  
>  Les propriétés d’installation du client sont utilisées pour installer le client. Ces propriétés peuvent être remplacées par de nouveaux paramètres provenant du site qui lui a été affecté une fois que le client est installé et qu’il a été affecté à un site Configuration Manager.  

 Utilisez les informations données dans les sections suivantes pour déterminer quelle méthode d’installation du client Configuration Manager utilise les services de domaine Active Directory pour obtenir les propriétés d’installation du client.  

## <a name="client-push-installation"></a>Installation poussée du client  
 L'installation poussée du client n'utilise pas les services de domaine Active Directory pour accéder aux propriétés d'installation.  

 Au lieu de cela, vous pouvez spécifier les propriétés d’installation du client dans l’onglet **Client** de la boîte de dialogue **Propriétés de l’installation push du client**. Ces options et paramètres de site liés aux clients sont stockés dans un fichier que le client lit pendant l'installation du client.  

> [!NOTE]  
>  Vous n'avez pas à spécifier de propriétés CCMSetup pour l'installation poussée du client, ni de point d'état de secours ou la clé racine de confiance dans l'onglet **Client** . Ces paramètres sont automatiquement fournis aux clients, lorsqu'ils sont installés par l'installation poussée du client.  

 Toutes les propriétés que vous spécifiez dans l’onglet **Client** sont publiées dans les services de domaine Active Directory si le site y est publié. Ces paramètres sont lus par les installations du client où CCMSetup est exécuté sans propriété d'installation.  

## <a name="software-update-point-based-installation"></a>Installation basée sur un point de mise à jour logicielle  
 La méthode d'installation basée sur un point de mise à jour logicielle ne prend pas en charge l'ajout de propriétés d'installation supplémentaires sur la ligne de commande CCMSetup.  

 Si aucune propriété de ligne de commande n'a été configurée sur l'ordinateur client utilisant la stratégie de groupe, CCMSetup recherche des propriétés d'installation dans les services de domaine Active Directory.  

## <a name="group-policy-installation"></a>Installation via la stratégie de groupe  
 La méthode d'installation via la stratégie de groupe ne prend pas en charge l'ajout de propriétés d'installation sur la ligne de commande CCMSetup.  

 Si aucune propriété de ligne de commande n'a été configurée sur l'ordinateur client, CCMSetup recherche des propriétés d'installation dans les services de domaine Active Directory.  

## <a name="manual-installation"></a>Installation manuelle  
 CCMSetup recherche des propriétés d'installation dans les services de domaine Active Directory dans les circonstances suivantes :  

-   Lorsqu'aucune propriété de ligne de commande n'est spécifiée à la suite de la commande CCMSetup.exe.  

-   Lorsque l'ordinateur n'a pas été configuré avec des propriétés d'installation à l'aide de la stratégie de groupe.  

## <a name="logon-script-installation"></a>Installation via un script d'ouverture de session  
 CCMSetup recherche des propriétés d'installation dans les services de domaine Active Directory dans les circonstances suivantes :  

-   Lorsqu'aucune propriété de ligne de commande n'est spécifiée à la suite de la commande CCMSetup.exe.  

-   Lorsque l'ordinateur n'a pas été configuré avec des propriétés d'installation à l'aide de la stratégie de groupe.  

## <a name="software-distribution-installation"></a>Installation via la distribution de logiciels  
 CCMSetup recherche des propriétés d'installation dans les services de domaine Active Directory dans les circonstances suivantes :  

-   Lorsqu'aucune propriété de ligne de commande n'est spécifiée à la suite de la commande CCMSetup.exe.  

-   Lorsque l'ordinateur n'a pas été configuré avec des propriétés d'installation à l'aide de la stratégie de groupe.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Installations pour les clients qui ne peuvent pas accéder aux services de domaine Active Directory  
Ces ordinateurs clients ne peuvent pas lire ou accéder aux propriétés d’installation publiées à partir des services de domaine Active Directory.

 Ces clients incluent les suivants :  

-   Ordinateurs d'un groupe de travail.  

-   Clients affectés à un site Configuration Manager qui n’est pas publié dans les services de domaine Active Directory.  

-   Clients installés quand ils sont sur Internet.  
