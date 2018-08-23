---
title: Vue d’ensemble des certificats CNG
titleSuffix: Configuration Manager
description: Découvrez la prise en charge des certificats Cryptography Next Generation (CNG) pour les clients et serveurs Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dba904ae-7c44-46db-ae63-999b9821cb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b85961c14c3db69c3e02e776798588fadd0fc89
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383151"
---
# <a name="cng-certificates-overview"></a>Vue d’ensemble des certificats CNG
<!-- 1356191 --> 

Configuration Manager prend en charge les certificats Cryptography : Next Generation (CNG) de manière limitée. Les clients Configuration Manager peuvent utiliser un certificat d’authentification client PKI avec une clé privée dans le fournisseur de stockage de clés (KSP) CNG. La prise en charge du KSP permet aux clients Configuration Manager de prendre en charge une clé privée matérielle, comme TPM KSP pour les certificats d’authentification client PKI.

## <a name="supported-scenarios"></a>Scénarios pris en charge
Vous pouvez utiliser les modèles de certificat [Cryptography API : Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) pour les scénarios suivants :

- Inscription du client et communication avec un point de gestion HTTPS   
- Distribution de logiciels et déploiement d’applications avec un point de distribution HTTPS   
- Déploiement du système d'exploitation  
- Kit SDK de messagerie du client (avec la dernière mise à jour) et proxy ISV   
- Configuration de la passerelle de gestion cloud  

À compter de la version 1802, utilisez des certificats CNG pour les rôles serveur HTTPS suivants : <!-- 1357314 -->   
- Point de gestion
- Point de distribution
- Point de mise à jour logicielle
- Point de migration d’état     

À partir de la version 1806, utilisez des certificats CNG pour les rôles serveur HTTPS suivants :

- Point d’enregistrement de certificat, notamment le serveur NDES avec le module de stratégie Configuration Manager <!--1357314-->

> [!NOTE]
> CNG offre une compatibilité descendante avec Crypto API (CAPI). Les certificats CAPI continuent à être pris en charge même lorsque la prise en charge CNG est activée sur le client.

## <a name="unsupported-scenarios"></a>Scénarios non pris en charge

Les scénarios suivants ne sont actuellement pas pris en charge :

- Les rôles serveur suivants ne sont pas opérationnels quand ils sont installés en mode HTTPS avec un certificat CNG lié au site web dans Internet Information Services (IIS) : 
    - Service web du catalogue des applications
    - Site web du catalogue des applications
    - Point d'inscription  
    - Point proxy d'inscription  

- Le Centre logiciel n’affiche pas les applications et packages disponibles qui sont déployés sur des regroupements d’utilisateurs ou de groupes d’utilisateurs.

- Utilisation de certificats CNG pour créer un point de distribution cloud.

- Si le module de stratégie NDES utilise un certificat CNG pour l’authentification du client, la communication avec le point d’enregistrement de certificat échoue. 
    - Ceci est pris en charge à partir de Configuration Manager version 1806.

- Si vous spécifiez un certificat CNG lors de la création d’un média de séquence de tâches, l’Assistant ne parvient pas à créer un média de démarrage.
    - Ceci est pris en charge à partir de Configuration Manager version 1806.

## <a name="to-use-cng-certificates"></a>Pour utiliser des certificats CNG

Pour utiliser des certificats CNG, votre autorité de certification (CA) doit fournir des modèles de certificat CNG pour les machines cibles. Bien que les détails du modèle varient selon le scénario, les propriétés suivantes sont requises :

- Onglet **Compatibilité**

    - L’**autorité de certification** doit être Windows Server 2008 ou version ultérieure. (Windows Server 2012 recommandé)

    - Le **destinataire du certificat** doit être Windows Vista/Server 2008 ou version ultérieure. (Windows 8/Windows Server 2012 recommandé)

- Onglet **Chiffrement**

    - La **catégorie de fournisseur** doit être **Fournisseur de stockage de clés**. (obligatoire)
    - **La requête doit utiliser l’un des fournisseurs suivants** doit avoir la valeur **Fournisseur de stockage de clés des logiciels Microsoft**. 

> [!NOTE]
> La configuration requise pour votre environnement ou votre organisation peut être différente. Contactez votre expert PKI. Le point important à ne pas négliger est qu’un modèle de certificat doit utiliser un fournisseur de stockage de clés pour tirer parti de CNG.

Pour de meilleurs résultats, nous vous recommandons de créer le nom du sujet à partir des informations Active Directory. Utilisez le nom DNS pour le **format du nom du sujet** et incluez le nom DNS dans le nom de substitution du sujet. Dans le cas contraire, vous devez fournir ces informations au moment de l’inscription de l’appareil dans le profil de certificat.