---
title: Sécurité et confidentialité pour les profils Wi-Fi et VPN
titleSuffix: Configuration Manager
description: Découvrez les bonnes pratiques en matière de sécurité pour la gestion des profils Wi-Fi et VPN des appareils dans System Center Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ae2b5825948b8f25491a111e62de9fd6e3534062
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496315"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les profils Wi-Fi et VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Bonnes pratiques de sécurité pour les profils Wi-Fi et VPN  
 Utilisez les bonnes pratiques de sécurité suivantes quand vous gérez des profils Wi-Fi et VPN pour des appareils.  

|Bonnes pratiques de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Dans la mesure du possible, choisissez les options les plus sécurisées prises en charge par votre système d’exploitation client et votre infrastructure Wi-Fi et VPN.|Les profils Wi-Fi et VPN fournissent une méthode pratique pour distribuer et gérer de manière centralisée des paramètres Wi-Fi et VPN que vos appareils prennent déjà en charge. Configuration Manager n’ajoute pas de fonctionnalité Wi-Fi ou VPN.<br /><br /> Identifiez, implémentez et suivez les bonnes pratiques de sécurité recommandées pour vos appareils et votre infrastructure.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informations de confidentialité pour les profils Wi-Fi  
 Vous pouvez utiliser des profils Wi-Fi et VPN pour configurer des appareils clients afin qu’ils se connectent à des serveurs Wi-Fi et VPN, puis pour évaluer si ces appareils deviennent compatibles après l’application des profils. Le point de gestion transmet les informations de compatibilité au serveur de site et les informations sont stockées dans la base de données de site. Les informations sont chiffrées lorsque les appareils les envoient au point de gestion mais ne sont pas stockées au format chiffré dans la base de données de site. La base de données conserve les informations jusqu'à ce que la tâche de maintenance de site **Supprimer les données de gestion de configuration anciennes** les supprime. L'intervalle de suppression par défaut est de 90 jours, mais vous pouvez la modifier. Les informations de compatibilité ne sont pas transmises à Microsoft.  

 Par défaut, les appareils n’évaluent pas les profils Wi-Fi et VPN. En outre, vous devez configurer les profils, puis les déployer auprès des utilisateurs.  

 Avant de configurer les profils Wi-Fi ou VPN, pensez à vos besoins en matière de confidentialité.  
