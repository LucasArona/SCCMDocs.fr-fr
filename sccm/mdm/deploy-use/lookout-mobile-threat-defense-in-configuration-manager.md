---
title: Restreindre l’accès en fonction du risque
titleSuffix: Configuration Manager
description: Restreignez l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50d79da3ab4e7ace9a682baaa5cfd8d2bdbdce10
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678875"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gérer l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application

*S’applique à : System Center Configuration Manager (Current Branch)*

Contrôlez l’accès depuis les appareils mobiles aux ressources d’entreprise en fonction de l’évaluation des risques effectuée par Lookout. Lookout est une solution de protection contre les menaces sur les appareils, intégrée à Microsoft Intune. Le risque est basé sur les données collectées par le service Lookout. A partir des appareils, le service recueille les données relatives aux vulnérabilités du système d’exploitation, aux applications malveillantes installées et aux profils réseau malveillants. 

En fonction de l’évaluation des risques effectuée par Lookout et activée par le biais des stratégies de conformité Configuration Manager, vous configurez les stratégies d’accès conditionnel. Ces stratégies autorisent ou bloquent les appareils que Configuration Manager détermine comme étant non conformes en raison des menaces détectées sur ces appareils.

> [!Important]  
> Depuis le 14 août 2018, la gestion hybride des appareils mobiles est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, consultez [Qu’est-ce que la gestion hybride des appareils mobiles ?](/sccm/mdm/understand/hybrid-mobile-device-management)<!--Intune feature 2683117-->  



## <a name="how-does-it-work"></a>Comment cela fonctionne-t-il ?

Comment le déploiement de la gestion des appareils mobiles hybride et le service Lookout de protection des appareils contre les menaces vous aident-ils à protéger les ressources d’entreprise ?

L'application mobile Lookout (Lookout for Work) est exécutée sur les appareils mobiles. Elle capture le système de fichiers, la pile réseau et les données d’utilisation des appareils et des applications lorsque ces informations sont disponibles. L’application envoie ces données au service cloud Lookout de protection des appareils contre les menaces, qui calcule le risque cumulé des menaces mobiles pour l’appareil. Utilisez la console Lookout pour modifier la classification des niveaux de risque des menaces en fonction de vos besoins.  

La stratégie de conformité dans Configuration Manager inclut maintenant une nouvelle règle pour la protection contre les menaces mobiles de Lookout qui est basée sur l’évaluation du risque de menaces sur les appareils réalisée par Lookout. Lorsque vous activez cette règle, Configuration Manager évalue la conformité de l’appareil.

Si l’appareil est non conforme à la stratégie de conformité, vous pouvez bloquer l’accès aux ressources telles que SharePoint Online et Exchange Online à l’aide de stratégies d’accès conditionnel. Si l’accès est bloqué, l’utilisateur final reçoit une procédure pas à pas pour l’aider à résoudre le problème et à récupérer l’accès aux ressources d’entreprise. L’utilisateur lance cette procédure pas à pas dans l’application Lookout for Work.



## <a name="supported-platforms"></a>Plateformes prises en charge

- **Android 4.1 et versions ultérieures**, et inscription à Microsoft Intune.  

- **iOS 8 et versions ultérieures**, et inscription à Microsoft Intune.  


Pour plus d’informations sur les plateformes et les langues prises en charge par Lookout, consultez cet [article sur la prise en charge Lookout](https://personal.support.lookout.com/hc/articles/114094140253).



## <a name="prerequisites"></a>Prérequis

- [MDM hybride](/sccm/mdm/understand/hybrid-mobile-device-management)  

- Abonnement à Microsoft Intune et Azure Active Directory.  

- Abonnement d’entreprise à Lookout Mobile EndPoint Security. Pour plus d’informations, consultez [Lookout Mobile Endpoint Security](https://www.lookout.com/products/mobile-endpoint-security).  



## <a name="example-scenarios"></a>Exemples de scénarios


### <a name="control-access-based-on-threat-from-malicious-apps"></a>Contrôler l’accès en fonction de la menace émanant des applications malveillantes

Quand des applications ou programmes malveillants sont détectés sur un appareil, vous pouvez empêcher l’appareil d’effectuer les opérations suivantes :

- Se connecter à la messagerie d’entreprise tant que la menace n’est pas résolue  

- Synchroniser les fichiers d’entreprise à l’aide de l’application OneDrive pour le travail  

- Accéder à des applications stratégiques  

#### <a name="access-blocked-when-malicious-apps-are-detected"></a>Accès bloqué après la détection d’applications malveillantes

![Stratégie d’accès conditionnel bloquant l’accès après la détection d’une application malveillante](media/config-mgr-maliciousapps_blocked.png)

#### <a name="device-unblocked-and-is-able-to-access-company-resources-when-the-threat-is-remediated"></a>Appareil débloqué pouvant accéder aux ressources d’entreprise après correction de la menace

![Stratégie d’accès conditionnel accordant l’accès quand l’appareil est conforme](media/config-mgr-maliciousapps-unblocked.png)


### <a name="control-access-based-on-threat-to-network"></a>Contrôler l’accès en fonction de la menace pour le réseau

Détectez les menaces pour votre réseau, telles que les attaques de l’intercepteur (« man-in-the-middle »), et restreignez l’accès aux réseaux Wi-Fi en fonction du risque évalué pour l’appareil.

#### <a name="access-to-network-through-wifi-blocked"></a>Accès au réseau par Wi-Fi bloqué

![Accès conditionnel interdisant l’accès par Wi-Fi en fonction des menaces pour le réseau](media/config-mgr-network-wifi-blocked.png)

#### <a name="access-granted-on-remediation"></a>Accès accordé après correction

![Accès conditionnel autorisant l’accès après correction de la menace](media/config-mgr-network-wifi-unblocked.png)


### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Contrôler l’accès à SharePoint Online en fonction de la menace pour le réseau

Détectez les menaces pour votre réseau, telles que les attaques de l’intercepteur, et empêchez la synchronisation des fichiers d’entreprise en fonction du risque évalué pour l’appareil.

#### <a name="access-blocked-sharepoint-online-based-on-network-threat-detected-on-the-device"></a>Accès à SharePoint Online bloqué en raison de la menace pour le réseau détectée sur l’appareil

![Accès conditionnel bloquant l’accès de l’appareil à SharePoint Online](media/config-mgr-network-spo-blocked.png)


#### <a name="access-granted-on-remediation"></a>Accès accordé après correction

![Accès conditionnel autorisant l’accès après correction de la menace](media/config-mgr-network-spo-unblocked.png)



## <a name="next-steps"></a>Étapes suivantes

Pour implémenter cette solution, procédez comme suit :  

1. [Configurer votre abonnement avec Lookout Mobile Threat Protection](set-up-your-subscription-with-lookout.md)
2. [Activer la connexion à Lookout MTP dans Intune](enable-lookout-connection-in-intune.md)
3.  [Configurer et déployer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md)
4. [Configurer une stratégie de conformité](enable-device-threat-protection-rule-compliance-policy.md)
5. [Résoudre les problèmes liés à l’intégration de Lookout](troubleshoot-lookout-integration.md)
