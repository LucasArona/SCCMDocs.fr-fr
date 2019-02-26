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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754848"
---
# <a name="conditional-access-with-co-management"></a>Accès conditionnel avec la cogestion

Accès conditionnel permet de s’assurer que seuls les utilisateurs approuvés peuvent accéder aux ressources de l’organisation sur les appareils de confiance à l’aide d’applications approuvées. Il est construit à partir de zéro dans le cloud. Si vous gérez des appareils avec Intune ou d’étendre votre déploiement Configuration Manager avec la cogestion, il fonctionne de la même façon.

Dans la vidéo suivante, responsable de programme senior Joey Glocke produit marketing Ainley Locky manager discuter et démonstration de l’accès conditionnel avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Avec la cogestion, Intune évalue chaque appareil dans votre réseau pour déterminer comment la confiance. Il effectue cette version d’évaluation des deux manières suivantes :

1. Intune permet de s’assurer un appareil ou application est gérée et configurée en toute sécurité. Cette vérification dépend de la façon dont vous définissez des stratégies de conformité de votre organisation. Par exemple, assurez-vous que tous les périphériques de chiffrement est activé et ne sont pas jailbreakés.  

    - Cette évaluation revêt une violation de la sécurité préliminaire et basée sur la configuration  

    - Pour les appareils cogérés, Configuration Manager effectue également basée sur la configuration de la version d’évaluation. Par exemple, mises à jour ou applications conformité requise. Intune combine cette version d’évaluation, ainsi que sa propre évaluation.  

2. Intune détecte les incidents de sécurité active sur un appareil. Il utilise la sécurité intelligente de [Windows Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/get-started) et d’autres [fournisseurs de défense contre les menaces mobiles](https://www.lookout.com/about/partners/microsoft). Ces partenaires s’exécutent une analyse comportementale en cours sur les appareils. Cette analyse détecte les incidents actifs, puis transmet ces informations à Intune pour évaluer la conformité en temps réel.  

    - Cette évaluation revêt une violation de la sécurité après et en cas d’incident  

Vice-président Microsoft Brad Anderson explique l’accès conditionnel en profondeur avec des démonstrations en direct pendant le discours Ignite 2018. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Accès conditionnel vous fournit également un emplacement centralisé pour voir l’intégrité de tous les périphériques connectés au réseau. Vous bénéficiez des avantages de l’échelle du cloud, qui est particulièrement utile pour les instances de production test Configuration Manager.


## <a name="benefits"></a>Avantages

Chaque équipe informatique est obsédé avec la sécurité du réseau. Il est obligatoire pour vous assurer que chaque appareil répond à vos besoins de sécurité et d’entreprise avant d’accéder à votre réseau. Avec l’accès conditionnel, vous pouvez déterminer les facteurs suivants : 
- Si chaque appareil est chiffré  
- Si un programme malveillant est installé  
- Si ses paramètres sont mis à jour  
- Si elle est jailbroken ou rooté  

Accès conditionnel combine un contrôle granulaire sur les données de l’organisation avec une expérience utilisateur qui optimise la productivité sur n’importe quel appareil à partir de n’importe quel emplacement.

La vidéo suivante montre comment [Protection avancée de Thread](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) est intégré à des scénarios courants que vous rencontrez régulièrement :

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Cogestion, Intune permet d’intégrer les responsabilités du Gestionnaire de Configuration pour évaluer votre conformité aux normes de sécurité des applications ou des mises à jour requises. Ce comportement est important pour toute organisation informatique qui souhaite continuer à utiliser le Gestionnaire de Configuration pour des applications complexes et de gestion des correctifs.

L’accès conditionnel est également un élément essentiel du développement de votre [réseau de confiance zéro](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/) architecture. Avec l’accès conditionnel, les contrôles d’accès appareil conforme couvrent les couches fondamentales du réseau de confiance de zéro. Cette fonctionnalité est une grande partie de la façon dont vous sécurisez votre organisation à l’avenir.

Pour plus d’informations, consultez le blog sur [amélioration de l’accès conditionnel avec des données de risque de l’ordinateur à partir de Windows Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Études de cas

L’informatique Wipro cabinet de conseil utilise l’accès conditionnel pour protéger et gérer les appareils utilisés par tous les 91,000 employés. Dans une récente étude de cas, le vice-président d’assistance informatique chez Wipro indiqué :

> *Accès conditionnel est un gros avantage pour Wipro. À présent, tous nos employés ont un accès mobile aux informations à la demande. * 
>  *Nous avons amélioré notre productivité employé et les mesures de sécurité. À présent 91,000 employés bénéficient d’un accès hautement sécurisé à plus de 100 applications à partir de n’importe quel appareil, n’importe où.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Autres exemples : 

- Nestle, qui utilise l’accès conditionnel basé sur l’application pour plus de 150 000 employés  

- La société de logiciels d’automatisation, Cadence, ce qui peut maintenant vous assurer que « uniquement les appareils gérés ont accès aux applications Office 365 tels que les équipes et l’intranet de l’entreprise. » Elles offrent aussi leur personnel « accès plus sûr aux autres applications cloud, telles que Workday et Salesforce. » Pour plus d’informations sur l’expérience de Cadence avec Intune, consultez [Cadence augmente le rythme de l’entreprise à l’aide des outils de collaboration mobiles dans Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365).

Intune est également totalement intégrée avec des partenaires comme Cisco ISE, Aruba Clear Pass et Citrix NetScaler. Avec ces partenaires, vous pouvez conserver les contrôles d’accès basés sur l’inscription Intune et l’état de conformité d’appareil pour ces autres plateformes.

Pour plus d’informations, consultez les vidéos suivantes :
- [Brad Anderson démonstrations l’accès conditionnel en détail](https://youtu.be/8321obNofgM?t=547)  
- [Détails supplémentaires à partir du point de terminaison de Zone 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Proposition de valeur

Avec l’accès conditionnel et intégration ATP, vous êtes fortification un composant fondamental de chaque organisation informatique : sécuriser l’accès au cloud.

Dans plus de 63 % de toutes les violations de données, les pirates ont accès au réseau de l’organisation via les informations d’identification utilisateur faibles, par défaut ou volé. Étant donné que l’accès conditionnel met l’accent sur la sécurisation de l’identité de l’utilisateur, elle restreint le vol d’informations d’identification. Accès conditionnel gère et protège vos identités, si privilégié ou non privilégié. Il n’existe aucun meilleur moyen de protéger les appareils et les données sur ces derniers.

Dans la mesure où l’accès conditionnel est un composant principal d’Enterprise Mobility + Security (EMS), aucun programme d’installation local ou n’est architecture requise. Avec Intune et Azure Active Directory (Azure AD), vous pouvez rapidement configurer l’accès conditionnel dans le cloud. Si vous utilisez actuellement Configuration Manager, vous pouvez facilement étendre votre environnement vers le cloud avec la cogestion et l’utiliser dès maintenant.

Pour plus d’informations sur l’intégration d’ATP, consultez ce blog [score de risque d’appareil Windows Defender ATP expose les nouvelles attaques, l’accès conditionnel pour protéger les réseaux des disques](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Il décrit en détail comment un groupe de pirates informatiques avancées utilisé jamais vu outils. Le cloud Microsoft détecté et arrêtés parce que les utilisateurs ciblés avaient accès conditionnel. L’intrusion activé la stratégie d’accès conditionnel en fonction du risque de l’appareil. Bien que l’attaquant a déjà établi une brèche dans le réseau, les machines exploitées sont limitaient automatiquement à partir de l’accès aux services d’organisation et les données gérées par Azure AD.



## <a name="configure"></a>Configurer

Accès conditionnel est facile à utiliser lorsque vous [activer la cogestion](/sccm/comanage/how-to-enable). Il nécessite de déplacer le **des stratégies de conformité** charge de travail à Intune. Pour plus d’informations, consultez [Basculer les charges de travail de Configuration Manager sur Intune](/sccm/comanage/how-to-switch-workloads). 

Pour plus d’informations sur l’utilisation de l’accès conditionnel, consultez les articles suivants : 

- [Accès conditionnel dans Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)  

- [Stratégies de conformité Intune](https://docs.microsoft.com/intune/device-compliance)  

- [En fonction des applications d’accès conditionnel avec Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Fonctionnalités d’accès conditionnel sont disponibles immédiatement pour hybride Azure appareils joints à AD. Ces fonctionnalités incluent l’authentification multifacteur et hybrides de contrôle d’accès Azure AD join. Ce comportement est, car ils sont basés sur les propriétés Azure AD. Pour tirer parti basée sur la configuration de l’évaluation d’Intune et Configuration Manager, activer la cogestion. Cette configuration vous donne accès contrôle directement à partir d’Intune pour les appareils conformes. Il vous donne également fonctionnalité d’évaluation de stratégies de conformité d’Intune.  

