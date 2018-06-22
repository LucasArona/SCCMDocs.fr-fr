---
title: Stratégies de conformité des appareils
titleSuffix: Configuration Manager
description: Découvrez comment gérer les stratégies de conformité dans System Center Configuration Manager pour rendre les appareils compatibles avec les stratégies d’accès conditionnel.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 776af7499c576f21d47dafec8a668f3c4051ad88
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347261"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Stratégies de conformité des appareils dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les **stratégies de conformité** dans System Center Configuration Manager définissent les règles et les paramètres auxquels un appareil doit se conformer pour être considéré comme conforme au vu des stratégies d’accès conditionnel. Vous pouvez également utiliser des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l'accès conditionnel.  


> [!IMPORTANT]  
>  Cet article décrit les stratégies de conformité applicables aux appareils gérés par Microsoft Intune.    Les stratégies de conformité applicables aux PC gérés par System Center Configuration Manager sont décrites dans [Gérer l’accès aux services O365 pour les PC gérés par System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

 Ces règles incluent des exigences telles que :  

-   Un code confidentiel et des mots de passe pour accéder à un appareil

-   Le chiffrement des données stockées sur l’appareil

-   Si l'appareil est jailbreaké ou rooté  

-   Si la messagerie sur l’appareil est gérée par une stratégie Intune, ou si le service Windows d’attestation d’intégrité de l’appareil signale celui-ci comme étant défectueux.
-   Applications qui ne peuvent pas être installées sur l’appareil.


 Vous déployez des stratégies de conformité sur des regroupements d'utilisateurs. Quand une stratégie de conformité est déployée sur un utilisateur, tous ses appareils dont l'objet d'une vérification de la conformité.  

 Le tableau suivant répertorie les appareils pris en charge par les stratégies de conformité et la façon dont les paramètres de non-conformité sont gérés quand la stratégie est utilisée avec une stratégie d'accès conditionnel.  

|Règle|Windows 8.1 et versions ultérieures|Windows Phone 8.1 et versions ultérieures|iOS 6.0 et versions ultérieures|Android 4.0 et versions ultérieures, Samsung KNOX Standard 4.0 et versions ultérieures, Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**Configuration d’un code confidentiel ou mot de passe**|Corrigé|Corrigé|Corrigé|En quarantaine|  
|**Chiffrement de l’appareil**|N/A|Corrigé|Corrigé (en définissant le code confidentiel)|En quarantaine<br>(Android for Work toujours chiffré)|  
|**Appareil jailbreaké ou rooté**|N/A|N/A|En quarantaine (pas un paramètre)|En quarantaine (pas un paramètre)|  
|**Profil de messagerie**|N/A|N/A|En quarantaine|N/A|  
|**Version minimale du système d’exploitation**|En quarantaine|En quarantaine|En quarantaine|En quarantaine|  
|**Version maximale du système d’exploitation**|En quarantaine|En quarantaine|En quarantaine|En quarantaine|  
|**Attestation d’intégrité de l’appareil (mise à jour 1602)**|Le paramètre n’est pas applicable à Windows 8.1<br /><br /> Windows 10 et Windows 10 Mobile sont mis en quarantaine.|N/A|N/A|N/A|  
|**Applications qui ne peuvent pas être installées**|N/A|N/A|En quarantaine|En quarantaine|

 **Corrigé** = La conformité est appliquée par le système d'exploitation de l'appareil (par exemple, l'utilisateur est obligé de définir un code confidentiel).  Ce n'est jamais la cas quand le paramètre n'est pas conforme.  

 **En quarantaine** = Le système d’exploitation de l’appareil n’applique pas la conformité (par exemple, les appareils Android ne forcent pas l’utilisateur à chiffrer l’appareil).  Dans ce cas :  

-   L'appareil est bloqué si l'utilisateur est ciblé par une stratégie d'accès conditionnel.  

-   Le portail d'entreprise ou portail web informe l'utilisateur des problèmes de conformité.  


### <a name="next-steps"></a>Étapes suivantes  
[Créer et déployer une stratégie de conformité d’appareil](create-compliance-policy.md)
### <a name="see-also"></a>Voir aussi  
 [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
