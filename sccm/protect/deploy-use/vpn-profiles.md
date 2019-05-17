---
title: Profils VPN
titleSuffix: Configuration Manager
description: Découvrez comment utiliser des profils VPN dans System Center Configuration Manager pour déployer des paramètres VPN pour les utilisateurs de votre organisation.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 505a4f3c00bc69e115b4130d422e11d8dec3fe30
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500397"
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Profils VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1283610-->
Si vous souhaitez déployer des paramètres VPN pour les utilisateurs de votre organisation, utilisez des profils VPN dans Configuration Manager. En déployant ces paramètres, vous réduisez l'effort que doit fournir l'utilisateur final pour se connecter aux ressources du réseau d'entreprise.  

 Par exemple, supposons que vous souhaitiez configurer tous les appareils Windows 10 en fonction des paramètres nécessaires pour vous connecter à un partage de fichiers sur le réseau de l’entreprise. Vous pouvez créer un profil VPN avec les paramètres nécessaires pour vous connecter au réseau de l’entreprise. Ensuite, déployez ce profil pour tous les utilisateurs qui disposent d’appareils exécutant Windows 10. Les utilisateurs voient la connexion VPN dans la liste des réseaux disponibles et peuvent se connecter très facilement.  

 Lorsque vous créez un profil VPN, vous pouvez inclure un large éventail de paramètres de sécurité. Ces paramètres incluent des certificats pour l’authentification de client et la validation de serveur que vous provisionnez à l’aide des profils de certificat Configuration Manager. Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


 Consultez la page [Utilisation de profils VPN sur des appareils mobiles dans System Center Configuration Manager](/sccm/mdm/deploy-use/create-vpn-profiles) pour passer en revue les appareils que vous pouvez configurer en utilisant Configuration Manager avec Microsoft Intune.  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Profils VPN si Configuration Manager est utilisé  
 Le tableau suivant décrit les profils VPN que vous pouvez configurer pour diverses plateformes d’appareil.  

|Type de connexion|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|Non|Non|Non|Non|  
|**Pulse Secure**|Oui|Non|Oui|Oui|  
|**Client F5 Edge**|Oui|Non|Oui|Oui|  
|**Dell SonicWALL Mobile Connect**|Oui|Non|Oui|Oui|  
|**Check Point Mobile VPN**|Oui|Non|Oui|Oui|  
|**Microsoft SSL (SSTP)**|Oui|Oui|Oui|Non|  
|**Microsoft Automatic**|Oui|Oui|Oui|Non|  
|**IKEv2**|Oui|Oui|Oui|Non|  
|**PPTP**|Oui|Oui|Oui|Non|  
|**L2TP**|Oui|Oui|Oui|Non|  

### <a name="next-steps"></a>Étapes suivantes  
 Utilisez les rubriques suivantes pour planifier, configurer, utiliser et gérer des profils VPN dans Configuration Manager.  

-   [Configuration requise pour les profils VPN dans System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sécurité et confidentialité pour les profils VPN dans System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
