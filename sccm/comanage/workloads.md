---
title: Charges de travail de cogestion
titleSuffix: Configuration Manager
description: En savoir plus sur les charges de travail que vous pouvez basculer à partir de Configuration Manager vers Microsoft Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.collection: M365-identity-device-management
ms.openlocfilehash: a3723595091e57a7ad2267a4da325e7c134c7bf1
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754875"
---
# <a name="co-management-workloads"></a>Charges de travail de cogestion

Vous n’êtes pas obligé de basculer les charges de travail, ou vous pouvez les faire individuellement lorsque vous êtes prêt. Configuration Manager continue de gérer toutes les autres charges de travail, y compris les charges de travail que vous ne basculez vers Intune, et toutes les autres fonctionnalités de Configuration Manager que cogestion ne prend pas en charge.

Cogestion prend en charge les charges de travail suivantes :

- [Stratégies de conformité](#compliance-policies)  

- [Stratégies Windows Update](#windows-update-policies)  

- [Stratégies d’accès aux ressources](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Configuration de l’appareil](#device-configuration)  

- [Applications Office Démarrer en un clic](#office-click-to-run-apps)  

- [Applications clientes](#client-apps)  



## <a name="compliance-policies"></a>Stratégies de conformité 

Les stratégies de conformité définissent les règles et les paramètres auxquels doit se conformer un appareil pour être considéré conforme par les stratégies d’accès conditionnel. Utilisez également des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l’accès conditionnel. 

Pour plus d’informations sur la fonctionnalité Intune, consultez [stratégies de conformité](https://docs.microsoft.com/intune/device-compliance-get-started).  



## <a name="windows-update-policies"></a>Stratégies Windows Update

Les stratégies Windows Update pour Entreprise vous permettent de configurer des stratégies de report pour les mises à jour de fonctionnalités Windows 10 ou les mises à jour qualité pour les appareils Windows 10 gérés directement par Windows Update pour Entreprise. 

Pour plus d’informations sur la fonctionnalité Intune, consultez [configurer la mise à jour Windows pour les stratégies de report Business](https://docs.microsoft.com/intune/windows-update-for-business-configure).  



## <a name="resource-access-policies"></a>Stratégies d’accès aux ressources

Les stratégies d’accès aux ressources configurent les paramètres VPN, Wi-Fi, d’e-mail et de certificat sur les appareils. 

Pour plus d’informations sur la fonctionnalité Intune, consultez [déployer des profils d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles).



## <a name="endpoint-protection"></a>Endpoint Protection
<!--1357365-->

À compter de Configuration Manager 1802, la charge de travail Endpoint Protection inclut la suite Windows Defender de fonctionnalités de protection contre les logiciels malveillants : 

- Windows Defender Application Guard  
- Pare-feu Windows Defender  
- Windows Defender SmartScreen  
- Chiffrement Windows  
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Centre de sécurité Windows Defender  
- Windows Defender - Protection avancée contre les menaces  
- Protection des informations Windows  

Pour plus d’informations sur la fonctionnalité Intune, consultez [Endpoint Protection pour Microsoft Intune](https://docs.microsoft.com/intune/endpoint-protection-windows-10).



## <a name="device-configuration"></a>Configuration de l’appareil
<!--1357903-->

À compter de Configuration Manager 1806, la charge de travail de configuration appareil inclut des paramètres que vous gérez des appareils dans votre organisation. Cette charge de travail de commutation déplace également le **accès aux ressources** et **Endpoint Protection** charges de travail.

Vous pouvez toujours déployer des paramètres Configuration Manager sur des appareils cogérés, même si Intune représente l’autorité de configuration des appareils. Cette exception peut être utilisée pour configurer les paramètres que votre organisation requiert mais ne sont pas encore disponible dans Intune. Spécifiez cette exception sur une [base de référence de configuration Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Activez l’option **toujours appliquer cette ligne de base même pour les clients gérés conjointement** lors de la création de la ligne de base. Vous pouvez le modifier par la suite la **général** onglet des propriétés d’une base existante.  

Pour plus d’informations sur la fonctionnalité Intune, consultez [créer un profil d’appareil dans Microsoft Intune](https://docs.microsoft.com/intune/device-profile-create).  



## <a name="office-click-to-run-apps"></a>Applications « Démarrer en un clic » Office
<!--1357841-->

À compter de Configuration Manager 1806, cette charge de travail gère les applications Office 365 sur les appareils gérés conjointement. 

- Après avoir déplacé la charge de travail, l’application s’affiche dans le **Portail d’entreprise** sur l’appareil  

- Les mises à jour Office peuvent mettre environ 24 heures à s’afficher sur le client, sauf si les appareils sont redémarrés  

- Il existe une nouvelle condition globale : **Are Office 365 applications managed by Intune on the device** (Les applications Office 365 sont-elles gérées par Intune sur cet appareil ?). Cette condition est ajoutée par défaut dans le cadre d’une exigence pour les nouvelles applications Office 365. Si vous transférez cette charge de travail, les clients cogérés ne répondront pas à cette exigence de l’application. Ils n’installeront donc pas Office 365 déployé via Configuration Manager.  

Pour plus d’informations sur la fonctionnalité Intune, consultez [applications affecter Office 365 pour les appareils Windows 10 avec Microsoft Intune](https://docs.microsoft.com/intune/apps-add-office365). 



## <a name="client-apps"></a>Applications clientes
<!--1357892-->

À compter de Configuration Manager version 1806, utiliser Intune pour gérer les applications clientes sur les appareils Windows 10 cogérés. Une fois cette charge de travail transférée, toutes les applications disponibles déployées à partir d’Intune seront accessibles sur le Portail d’entreprise. Les applications déployées à partir de Configuration Manager sont disponibles dans le centre logiciel.

Pour plus d’informations sur la fonctionnalité Intune, consultez [What ' s gestion des applications Microsoft Intune ?](https://docs.microsoft.com/intune/app-management). 

> [!Note]  
> La charge de travail des applications client est une fonctionnalité en préversion. Pour l’activer, consultez [Fonctionnalités de préversion](/sccm/core/servers/manage/pre-release-features).  



## <a name="next-steps"></a>Étapes suivantes

[Comment basculer des charges de travail](/sccm/comanage/how-to-switch-workloads)  


