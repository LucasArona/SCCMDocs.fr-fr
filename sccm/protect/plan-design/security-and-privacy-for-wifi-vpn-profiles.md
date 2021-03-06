---
title: "Sécurité et confidentialité des profils Wi-Fi et VPN | System Center Configuration Manager"
description: "Découvrez les bonnes pratiques en matière de sécurité pour la gestion des profils Wi-Fi et VPN des appareils dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/19/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: 4
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 32dff36aa8027b0563b999e7fe6ef41d0eb79020
ms.openlocfilehash: b9d70018708ab5932a3032134b03aef236ef9fda


---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les profils Wi-Fi et VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Cette rubrique contient des informations de sécurité et de confidentialité pour les profils Wi-Fi et VPN dans System Center Configuration Manager.  

##  <a name="a-namebkmksecurityremoteconnectionsa-security-best-practices-for-wi-fi-and-vpn-profiles"></a><a name="BKMK_Security_RemoteConnections"></a> Bonnes pratiques de sécurité pour les profils Wi-Fi et VPN  
 Utilisez les bonnes pratiques de sécurité suivantes lorsque vous gérez des profils Wi-Fi et VPN pour des appareils.  

|Meilleure pratique de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Dans la mesure du possible, choisissez les options les plus sécurisées prises en charge par votre système d’exploitation client et votre infrastructure Wi-Fi et VPN.|Les profils Wi-Fi et VPN fournissent une méthode pratique pour distribuer et gérer de manière centralisée des paramètres Wi-Fi et VPN que vos appareils prennent déjà en charge. System Center Configuration Manager n’ajoute pas de fonctionnalités Wi-Fi ni VPN.<br /><br /> Identifiez, implémentez et suivez les meilleures pratiques de sécurité recommandées pour vos périphériques et votre infrastructure.|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Informations de confidentialité pour les profils Wi-Fi  
 Vous pouvez utiliser des profils Wi-Fi et VPN pour configurer des appareils clients afin qu’ils se connectent à des serveurs Wi-Fi et VPN, puis pour évaluer si ces appareils deviennent compatibles après l’application des profils. Le point de gestion transmet les informations de compatibilité au serveur de site et les informations sont stockées dans la base de données de site. Les informations sont chiffrées lorsque les périphériques les envoient au point de gestion mais ne sont pas stockées au format chiffré dans la base de données de site. La base de données conserve les informations jusqu'à ce que la tâche de maintenance de site **Supprimer les données de gestion de configuration anciennes** les supprime. L'intervalle de suppression par défaut est de 90 jours, mais vous pouvez la modifier. Les informations de compatibilité ne sont pas transmises à Microsoft.  

 Par défaut, les appareils n’évaluent pas les profils Wi-Fi et VPN. En outre, vous devez configurer les profils, puis les déployer auprès des utilisateurs.  

 Avant de configurer les profils Wi-Fi ou VPN, pensez à vos besoins en matière de confidentialité.  



<!--HONumber=Nov16_HO1-->


