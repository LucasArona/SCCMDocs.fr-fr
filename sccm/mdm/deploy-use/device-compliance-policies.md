---
title: Stratégies de conformité des appareils
titleSuffix: Configuration Manager
description: Découvrez comment gérer les stratégies de conformité dans Configuration Manager pour rendre les appareils compatibles avec les stratégies d’accès conditionnel.
ms.date: 07/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2544d2b61c3d92555d0bc1abc908003f1c982bab
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136515"
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>Stratégies de conformité des appareils dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les stratégies de conformité dans Configuration Manager définissent les règles et les paramètres auxquels un appareil doit se conformer pour être considéré comme conforme au vu des stratégies d’accès conditionnel. Vous pouvez également utiliser des stratégies de conformité pour surveiller et corriger les problèmes de conformité avec les appareils indépendamment de l'accès conditionnel.  


> [!IMPORTANT]  
>  Cet article décrit les stratégies de conformité applicables aux appareils gérés par Microsoft Intune. Les stratégies de conformité applicables aux appareils gérés par le client Configuration Manager sont décrites dans [Gérer l’accès aux services O365 pour les appareils gérés par Configuration Manager](/sccm/protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  

 Ces règles incluent des exigences telles que :  

-   Un code confidentiel et des mots de passe pour accéder à un appareil  

-   Le chiffrement des données stockées sur l’appareil  

-   Si l'appareil est jailbreaké ou rooté  

-   Si la messagerie sur l’appareil est gérée par une stratégie Intune, ou si le service Windows d’attestation d’intégrité de l’appareil signale celui-ci comme étant défectueux.  

-   Les applications qui ne peuvent pas être installées sur l’appareil.  


 Vous déployez des stratégies de conformité sur des regroupements d'utilisateurs. Quand une stratégie de conformité est déployée sur un utilisateur, tous ses appareils dont l'objet d'une vérification de la conformité.  



## <a name="supported-device-types"></a>Types d’appareils pris en charge

 Le tableau suivant répertorie les appareils pris en charge par les stratégies de conformité et la façon dont les paramètres de non-conformité sont gérés quand la stratégie est utilisée avec une stratégie d’accès conditionnel.  

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

 **Corrigé** = La conformité est appliquée par le système d’exploitation de l’appareil. Par exemple, l’utilisateur est obligé de définir un code PIN. En aucun cas le paramètre n’est pas conforme.  

 **Mis en quarantaine** = Le système d’exploitation de l’appareil ne fait pas respecter la conformité. Par exemple, les appareils Android ne forcent pas l’utilisateur à chiffrer l’appareil. Dans ce cas :  

-   Si l’utilisateur est ciblé par une stratégie d’accès conditionnel, l’appareil est bloqué.  

-   Le portail d’entreprise ou portail web informe l’utilisateur d’éventuels problèmes de conformité.  



## <a name="devices-without-any-assigned-compliance-policy"></a>Appareils sans aucune stratégie de conformité affectée
<!--2520152--> À compter de juillet 2018, indiquez si tous les appareils auxquels aucune stratégie de conformité n’est affectée sont considérés comme conformes ou non. Par défaut, les appareils sans aucune stratégie de conformité affectée sont considérés comme conformes. Utilisez les étapes suivantes pour changer ce paramètre dans le portail Azure :

1. Connectez-vous à [Intune sur le portail Azure](https://aka.ms/intuneportal).  

2. Sélectionnez **Conformité de l’appareil**, puis **Paramètres de stratégie de conformité** dans le groupe Installation.  

3. Pour le paramètre **Marquer les appareils sans stratégie de conformité comme étant**, sélectionnez l’une des options suivantes :  

     - **Conforme** (valeur par défaut) : les appareils sans aucune stratégie de conformité affectée sont considérés comme conformes à la stratégie. Si l’accès conditionnel est activé, ces appareils ont accès aux ressources internes.  

     - **Non conforme** : les appareils sans aucune stratégie de conformité affectée sont considérés comme non conformes à la stratégie. Si l’accès conditionnel est activé, ces appareils sont bloqués des ressources internes selon les conditions dans la stratégie d’accès conditionnel.  

4. Cliquez sur Enregistrer.  

Nous vous recommandons de déployer au moins une stratégie de conformité pour chaque plateforme à tous les utilisateurs de votre environnement. Affectez ensuite à ce paramètre la valeur **Non conforme** pour garantir la sécurité de vos ressources internes. Pour plus d’informations, consultez le billet de blog [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies).



## <a name="next-steps"></a>Étapes suivantes  
[Créer et déployer une stratégie de conformité d’appareil](/sccm/mdm/deploy-use/create-compliance-policy)

### <a name="see-also"></a>Voir aussi  
 [Gérer l’accès aux services dans Configuration Manager](/sccm/protect/deploy-use/manage-access-to-services)
