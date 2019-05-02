---
title: Accès conditionnel avec la cogestion
titleSuffix: Configuration Manager
description: Contrôler l’accès utilisateur aux ressources de l’organisation en fonction des règles de conformité d’Intune
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2d5e5c7d6075697431f8c537366dc16164fedd1f
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754848"
---
# <a name="conditional-access-with-co-management"></a>Accès conditionnel avec la cogestion

L’accès conditionnel permet de s’assurer que seuls les utilisateurs approuvés peuvent accéder aux ressources de l’organisation sur les appareils approuvés avec les applications approuvées. Il est créé de toutes pièces dans le cloud. Que vous gériez des appareils avec Intune ou étendiez votre déploiement Configuration Manager avec la cogestion, il fonctionne de la même façon.

Dans la vidéo suivante, le program manager senior, Rob York, et le directeur du marketing produit, Locky Ainley, parlent et font la démonstration de l’accès conditionnel avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Avec la cogestion, Intune évalue chaque appareil de votre réseau pour déterminer à quel point il peut être digne de confiance. Il procède à cette évaluation des deux façons suivantes :

1. Intune s’assure qu’un appareil ou une application est géré(e) et configuré(e) de manière sécurisée. Cette vérification dépend de la façon dont vous définissez les stratégies de conformité de votre organisation. Par exemple, assurez-vous que tous les appareils ont le chiffrement activé et ne sont pas jailbreakés.  

    - Cette évaluation est basée sur la configuration et les pré-violations de la sécurité  

    - Pour les appareils cogérés, Configuration Manager procède aussi à une évaluation basée sur la configuration. Par exemple, les mises à jour obligatoires ou la conformité des applications. Intune combine cette évaluation avec sa propre évaluation.  

2. Intune détecte les incidents de sécurité actifs sur un appareil. Il utilise la sécurité intelligente de [Windows Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) et d’autres [fournisseurs de défense contre les menaces mobiles](https://www.lookout.com/about/partners/microsoft). Ces partenaires effectuent une analyse comportementale continue sur les appareils. Cette analyse détecte les incidents actifs, puis transmet ces informations à Intune pour une évaluation de la conformité en temps réel.  

    - Cette évaluation est basée sur les incidents et les post-violations de la sécurité  

Le vice-président de Microsoft, Brad Anderson, parle de l’accès conditionnel en profondeur avec des démonstrations en direct lors de la conférence Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

L’accès conditionnel vous fournit aussi un emplacement centralisé pour voir l’intégrité de tous les appareils connectés au réseau. Vous bénéficiez des avantages du cloud, ce qui est particulièrement utile pour tester les instances de production de Configuration Manager.


## <a name="benefits"></a>Avantages

Pour chaque équipe informatique, la sécurité réseau est une obsession. Il est indispensable de s’assurer que chaque appareil répond à vos exigences de sécurité et métier avant d’accéder à votre réseau. Avec l’accès conditionnel, vous pouvez déterminer les facteurs suivants : 
- Si chaque appareil est chiffré  
- Si un programme malveillant est installé  
- Si ses paramètres sont mis à jour  
- S’il est jailbreaké ou rooté  

L’accès conditionnel allie un contrôle précis sur les données de l’organisation à une expérience utilisateur qui optimise la productivité des employés sur tous les appareils où que vous soyez.

La vidéo suivante montre comment [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) est intégré à des scénarios courants que vous rencontrez régulièrement :

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Avec la cogestion, Intune peut endosser les responsabilités de Configuration Manager pour évaluer la conformité des normes de sécurité de vos applications ou mises à jour requises. Ce comportement est important pour toute organisation informatique qui souhaite continuer à utiliser Configuration Manager pour une gestion complexe des applications et des correctifs.

L’accès conditionnel est également un élément essentiel du développement de l’architecture de votre [réseau de confiance zéro](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/). Avec l’accès conditionnel, les contrôles d’accès des appareils conformes couvrent les fondations du réseau de confiance zéro. Cette fonctionnalité joue un grand rôle dans la façon dont vous allez sécuriser votre organisation dans le futur.

Pour plus d’informations, consultez le billet de blog [Enhancing conditional access with machine-risk data from Windows Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Études de cas

La société de services de conseil informatique Wipro utilise l’accès conditionnel pour protéger et gérer les appareils utilisés par ses 91 000 employés. Dans une récente étude de cas, le vice-président du service informatique de Wipro a noté :

> *L’utilisation de l’accès conditionnel est un énorme succès pour Wipro. À présent, tous nos employés ont un accès mobile aux informations à la demande.*
> *Nous avons amélioré notre posture de sécurité et la productivité de nos employés. À présent 91 000 employés bénéficient d’un accès hautement sécurisé à plus de 100 applications sur tous les appareils, où qu’ils soient.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Autres exemples : 

- Nestlé utilise l’accès conditionnel basé sur les applications pour plus de 150 000 employés  

- La société de logiciels d’automatisation Cadence peut maintenant garantir que « seuls les appareils gérés ont accès aux applications Office 365 comme Teams et à l’intranet de l’entreprise. » Elle offre aussi à leur personnel « un accès plus sûr aux autres applications cloud, comme Workday et Salesforce. » Pour plus d’informations sur l’expérience de Cadence avec Intune, consultez [Cadence increases the pace of business with mobile collaboration tools in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune est également totalement intégré avec des partenaires comme Cisco ISE, Aruba Clear Pass et Citrix NetScaler. Avec ces partenaires, vous pouvez conserver les contrôles d’accès basés sur l’inscription Intune et l’état de conformité des appareils sur ces autres plateformes.

Pour plus d’informations, regardez les vidéos suivantes :
- [Brad Anderson demos conditional access in detail](https://youtu.be/8321obNofgM?t=547)  
- [Additional detail from Endpoint Zone 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposition de valeur

Avec l’accès conditionnel et l’intégration d’ATP, vous consolidez un composant fondamental de chaque organisation informatique : la sécurisation de l’accès au cloud.

Dans plus de 63 % des violations de données, les attaquants ont accès au réseau de l’organisation à cause d’informations d’identification utilisateur faibles, par défaut ou volées. Étant donné que l’accès conditionnel est focalisé sur la sécurisation de l’identité utilisateur, il limite le vol d’informations d’identification. L’accès conditionnel gère et protège vos identités, qu’elles soient privilégiées ou non. Il n’existe aucun meilleur moyen de protéger les appareils et leurs données.

Dans la mesure où l’accès conditionnel est un composant phare d’Enterprise Mobility + Security (EMS), aucune installation ou architecture locale n’est requise. Avec Intune et Azure Active Directory (Azure AD), vous pouvez rapidement configurer l’accès conditionnel dans le cloud. Si vous utilisez Configuration Manager, vous pouvez facilement étendre votre environnement au cloud avec la cogestion et commencer à l’utiliser dès maintenant.

Pour plus d’informations sur l’intégration d’ATP, consultez ce billet de blog [Windows Defender ATP device risk score exposes new cyberattack, drives Conditional access to protect networks](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Il décrit en détail comment un groupe de hackers de haut vol utilisait des outils encore jamais vus. Le cloud Microsoft les a détectés et les a arrêtés parce que les utilisateurs ciblés avaient un accès conditionnel. Leur intrusion a activé la stratégie d’accès conditionnel basée sur les risques de l’appareil. Même si l’attaquant avait déjà établi une brèche dans le réseau, les ordinateurs exploités ont été automatiquement coupés des services de l’organisation et des données gérées par Azure AD.



## <a name="configure"></a>Configurer

L’accès conditionnel est facile à utiliser quand vous [activez la cogestion](/sccm/comanage/how-to-enable). Il nécessite de déplacer la charge de travail **Stratégies de conformité** dans Intune. Pour plus d’informations, consultez [Basculer les charges de travail de Configuration Manager sur Intune](/sccm/comanage/how-to-switch-workloads). 

Pour plus d’informations sur l’utilisation de l’accès conditionnel, consultez les articles suivants : 

- [Accès conditionnel dans Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Stratégies de conformité des appareils Intune](https://docs.microsoft.com/intune/device-compliance)  

- [Accès conditionnel basé sur l’application avec Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Les fonctionnalités d’accès conditionnel sont immédiatement disponibles pour les appareils avec jonction Azure AD hybride. Ces fonctionnalités incluent l’authentification multifacteur et le contrôle d’accès avec jonction Azure AD hybride. Ce comportement s’explique par le fait qu’elles sont basées sur les propriétés Azure AD. Pour tirer profit d’une évaluation basée sur la configuration d’Intune et de Configuration Manager, activez la cogestion. Cette configuration vous donne un contrôle d’accès directement depuis Intune pour les appareils conformes. Elle vous offre aussi la fonctionnalité d’évaluation de stratégies de conformité d’Intune.  

