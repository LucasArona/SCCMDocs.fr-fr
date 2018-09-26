---
title: Actions en cas de non-conformité
titleSuffix: Configuration Manager
description: Découvrir comment configurer des actions en cas de non-conformité avec Configuration Manager
ms.date: 08/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b6a974d1cca4f97cbcf41a0cf644f545cec4b37d
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42589499"
---
# <a name="set-up-actions-for-non-compliance"></a>Configurer des actions en cas de non-conformité

Les **actions en cas de non-conformité** vous permettent de configurer une séquence chronologique d’actions appliquées aux appareils qui ne sont pas conformes. Par exemple, envoyez des e-mails à l’utilisateur final d’appareils non conformes et marquez ces appareils comme non conformes.



## <a name="before-you-begin"></a>Avant de commencer

> [!IMPORTANT]  
> Pour configurer des actions en cas de non-conformité, commencez par créer au moins une stratégie de conformité des appareils.  

Les actions prises en charge en cas de non-conformité sont les suivantes :

- Envoyer un e-mail à l’utilisateur final
- Marquer les appareils comme non conformes

### <a name="send-e-mail-to-end-user"></a>Envoyer un e-mail à l’utilisateur final

Choisir un des modèles d’e-mail par défaut prédéfinis ou créer une notification par e-mail entièrement personnalisée. Configuration Manager permet de personnaliser l’objet et le corps du message, y compris le logo de l’entreprise, les informations de contact et les destinataires supplémentaires.

### <a name="mark-devices-non-compliant"></a>Marquer les appareils comme non conformes

Déterminer une planification en nombre de jours pendant lesquels l’accès aux ressources d’entreprise doit être bloqué pour l’appareil. Cette action peut être immédiate, mais vous pouvez aussi accorder à l’utilisateur une période de grâce pour qu’il se mette en conformité avec les stratégies de conformité des appareils.

### <a name="supported-platforms"></a>Plateformes prises en charge

Prise en charge par [toutes les plateformes gérés par Intune](https://docs.microsoft.com/intune/supported-devices-browsers).



## <a name="to-add-an-email-template"></a>Pour ajouter un modèle d’e-mail

Configuration Manager fournit des modèles d’e-mail, mais vous pouvez également créer vos propres modèles. Le modèle d’e-mail est utilisé plus tard lors du processus de création d’actions en cas de non-conformité pour communiquer avec les utilisateurs.

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

2. Dans l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis choisissez **Modèles de notification de conformité**.  

3. Sous l’onglet **Accueil**, cliquez sur **Créer un modèle de notification de conformité**.  

4. Entrez les informations suivantes :  

    a. **Nom** : nom du modèle d’e-mail  

    > [!Note]  
    > Le champ **De** champ est rempli automatiquement avec une adresse de messagerie no-reply de Microsoft.<!--SCCMDocs issue 652-->  

    c. **Objet** : objet qui explique la notification par e-mail envoyée  

    d. **Corps du message** : autres détails sur la notification par e-mail  

    > [!TIP]  
    > Vous pouvez également inclure un **en-tête d’e-mail** avec le logo de votre entreprise, ainsi qu’un **pied de page d’e-mail** pouvant inclure le nom de votre organisation et ses informations de contact. Modifiez également ces informations dans les propriétés de votre abonnement Intune.  

5. Cliquez sur **OK** pour enregistrer le nouveau modèle d’e-mail.  

6. Dans la page **Ajouter une action**, sélectionnez votre nouveau modèle d’e-mail dans la liste.  

7. Une fois que vous avez sélectionné votre modèle d’e-mail, cliquez sur **OK**.  



## <a name="to-create-actions-for-non-compliance"></a>Pour créer des actions en cas de non-conformité

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

2. Dans l'espace de travail **Ressources et Conformité**, développez **Paramètres de compatibilité**, puis choisissez **Stratégies de conformité**.  

3. Sous l'onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une stratégie de conformité**.  

4. Sélectionnez les **plateformes prises en charge** souhaitées, puis cliquez sur **Suivant** à deux reprises. Vous pouvez ignorer la page **Règles**.  

5. Dans la page **Actions pour la non-conformité**, pour définir ce qui se passe quand un appareil n’est plus conforme, cliquez sur **Nouveau**.  

6. Vous pouvez choisir deux options : **Envoyer un e-mail à l’utilisateur final** ou **Marquer l’appareil comme non conforme**.  

7. Si vous sélectionnez **Envoyer un e-mail à l’utilisateur final**, entrez les informations suivantes :  

    a. **Période de grâce (en jours) :** entrez un nombre de jours de 0 à 365  

    b. **Destinataires supplémentaires (via e-mail)**  

    c. **Sélectionnez le modèle de message :** choisissez un modèle d’e-mail par défaut ou un modèle personnalisé que vous avez créé.  
    
    > [!TIP]   
    > Vous pouvez également ajouter un nouveau modèle d’e-mail quand vous ajoutez l’action **Envoyer un e-mail à l’utilisateur final** en cliquant sur **Nouveau** dans la page **Ajouter une action**.  

8. Si vous sélectionnez **Marquer l’appareil comme non conforme**, vous devez entrer les informations suivantes :  

    a. **Période de grâce (en jours) :** entrez un nombre de jours de 0 à 365  

9. Effectuez toutes les étapes de l'Assistant.  

