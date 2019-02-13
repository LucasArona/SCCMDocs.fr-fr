---
title: Activer une règle de protection des appareils dans la stratégie de conformité
titleSuffix: Configuration Manager
description: Activez une règle de protection contre les menaces mobiles dans la stratégie de conformité des appareils.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 99a5b715-f172-46e1-ac27-ad55bde66d0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0bae054d3daa5aea8e343fef05aa4578221f17b6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133984"
---
# <a name="enable-device-threat-protection-rule-in-the-compliance-policy"></a>Activer une règle de protection contre les menaces des appareils dans la stratégie de conformité

*S’applique à : System Center Configuration Manager (Current Branch)*

Intune avec Mobile Threat Protection de Lookout vous donne la possibilité de détecter les menaces mobiles et d’évaluer les risques sur l’appareil. Vous pouvez créer une règle de stratégie de conformité dans Configuration Manager pour inclure l’évaluation des risques permettant de déterminer si l’appareil est conforme. Vous pouvez ensuite utiliser la stratégie d’accès conditionnel pour autoriser ou bloquer l’accès à Exchange, SharePoint et d’autres services, en fonction de la compatibilité des appareils.

Pour que Mobile Threat Protection de Lookout influence la stratégie de conformité de l’appareil :

* La règle **Protection contre les menaces sur les appareils** doit être activée sur la stratégie de conformité.

* La page **État de Lookout** dans la **console Administrateur Intune** doit apparaître comme étant **Active**. Pour plus d’informations et des instructions sur la façon d’activer l’intégration de Lookout, consultez la rubrique [Activer la connexion de Lookout dans Intune](enable-lookout-connection-in-intune.md).


Avant de créer la règle de protection contre les menaces sur les appareils dans la stratégie de conformité, nous vous recommandons de [configurer votre abonnement avec Mobile Threat Protection de Lookout](set-up-your-subscription-with-lookout.md), [d’activer la connexion de Lookout dans Intune](enable-lookout-connection-in-intune.md) et de [configurer l’application Lookout for Work](configure-and-deploy-lookout-for-work-apps.md). La règle de compatibilité est appliquée seulement une fois que le programme d’installation est terminé.

Pour activer la règle de protection contre les menaces sur les appareils, vous pouvez utiliser une stratégie de conformité existante ou en créer une.

Dans le cadre de l’installation de Mobile Threat Protection de Lookout, dans la [console Lookout](https://aad.lookout.com), vous avez créé une stratégie qui classifie les différentes menaces selon trois niveaux : Élevé, Moyen et Faible. Dans la stratégie de conformité Intune, vous utilisez le niveau de menace pour définir le niveau de menace maximal autorisé.

Dans la page **Règles** de l’Assistant Stratégie de conformité, définissez une nouvelle règle avec les informations suivantes :
  * Condition : Niveau de risque maximal protection appareil contre les menaces.
  * Valeur : La valeur peut être une des opérations suivantes :
    * **Aucun (sécurisé)**: Il s’agit le plus sécurisé. Cela signifie que l’appareil ne peut avoir aucune menace. Si un quelconque niveau de menace est détecté, l’appareil est évalué comme non conforme.
    * **Faible** : L’appareil est évalué comme conforme uniquement si les menaces de niveau faible sont présentes. Toute menace d’un niveau supérieur place l’appareil dans un état de non-conformité.
    * **Support**: L’appareil est évalué comme conforme si les menaces détectées sur l’appareil sont de niveau faible ou moyen. Si des menaces de niveau Élevé sont détectées, l’appareil est déterminé comme étant non conforme.
    * **Haute**: Cette option est la moins sécurisée. Cette option permet en fait tous les niveaux de menaces. Elle peut être utile si vous utilisez cette solution uniquement pour la génération de rapports.

Si vous créez des stratégies d’accès conditionnel pour Office 365 et d’autres services, l’évaluation de conformité ci-dessus est prise en considération, et l’accès aux ressources d’entreprise par les appareils non conformes est bloqué jusqu’à ce que la menace soit résolue.

L’état de la protection contre les menaces sur les appareils est affiché sur le nœud **Sécurité** dans l’espace de travail **Surveillance**.
Un résumé de l’état avec les différents niveaux de menaces est affiché dans un graphique. Vous pouvez cliquer sur les sections du graphique pour voir plus d’informations, comme le nombre d’appareils signalés comme non conformes par plateforme, et les éventuelles erreurs qui sont signalées.
Vous pouvez également voir l’état des appareils individuels dans l’espace de travail **Ressources et conformité**, sous **Appareils**.  Vous pouvez ajouter les colonnes **État de conformité de l’appareil** et **Niveau de menace pour l’appareil** pour afficher l’état.  Par défaut, ces colonnes ne sont pas affichées.
