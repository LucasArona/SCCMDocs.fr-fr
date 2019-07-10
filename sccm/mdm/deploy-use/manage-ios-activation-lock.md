---
title: Gérer le verrou d’activation iOS
titleSuffix: Configuration Manager
description: Découvrez comment gérer le verrou d’activation iOS avec System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 780abd0702e34dff7a8026fb54e29ccea6f67170
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678756"
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>Gérer le verrou d’activation iOS avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


System Center Configuration Manager peut vous aider à gérer le verrou d’activation iOS, fonctionnalité de l’application Rechercher mon iPhone pour les appareils iOS 7.1 et versions ultérieures. Quand le verrou d’activation est activé, l’ID et le mot de passe Apple de l’utilisateur doivent être entrés pour permettre à quiconque de :

- désactiver Rechercher mon iPhone ;
- Effacer l'appareil
- Réactiver l'appareil

Sur les appareils **non supervisés** , le verrou d’activation est activé automatiquement dès lors que l’application Rechercher mon iPhone est utilisée.

Sur les appareils **supervisés** , vous devez activer le verrou d’activation à l’aide des paramètres de compatibilité de Configuration Manager.

> [!TIP]
> Le mode supervisé pour les appareils iOS vous permet d'utiliser l'outil de configuration Apple pour verrouiller un appareil et limiter ainsi la fonctionnalité à des usages professionnels spécifiques. Le mode surveillé est généralement destiné uniquement aux appareils appartenant à l'entreprise.

Bien que le verrou d’activation permette de sécuriser les appareils iOS et améliore les chances de récupération en cas de perte ou de vol, cette fonctionnalité peut présenter quelques défis pour les administrateurs informatiques. Par exemple :

- L'un de vos utilisateurs configure le verrou d'activation sur un appareil. L'utilisateur quitte ensuite l'entreprise et rend l'appareil. Sans l’ID et le mot de passe Apple de l’utilisateur, il n’existe aucun moyen de réactiver l’appareil, même si vous le réinitialisez.
- Vous avez besoin d’un rapport répertoriant tous les appareils sur lesquels le verrou d’activation est activé.
- Lors d'une actualisation des appareils de votre organisation, vous souhaitez réaffecter certains appareils à un autre service. Vous ne pouvez réaffecter que les appareils sur lesquels le verrou d’activation n’est pas activé.


Pour résoudre ces problèmes, Apple a introduit le contournement du verrou d'activation dans iOS 7.1. Il vous permet de supprimer le verrou d'activation des appareils supervisés sans avoir l'ID Apple et le mot de passe de l'utilisateur. Les appareils supervisés peuvent générer un code de contournement du verrou d'activation spécifique à l'appareil, qui est stocké sur le serveur d'activation d'Apple.

Vous trouverez un complément d’information sur le verrou d’activation [ici](https://support.apple.com/HT201365).

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Comment Configuration Manager aide à gérer le verrou d’activation

Configuration Manager peuvent vous aider à gérer le verrou d’activation de deux façons :

1. en activant le verrou d’activation sur les appareils supervisés ;
2. en contournant le verrou d’activation sur les appareils supervisés.

> [!IMPORTANT]
> Vous ne pouvez pas contourner le verrou d’activation sur les appareils non supervisés.

Les avantages pour les appareils de l’entreprise sont les suivants :



- L'utilisateur bénéficie des avantages de sécurité offerts par l'application Rechercher mon iPhone.
- Vous pouvez laisser l’utilisateur effectuer son travail en sachant que lorsque vous devrez réaffecter l’appareil, vous pourrez le mettre hors service ou le déverrouiller.


## <a name="enable-activation-lock-on-supervised-devices"></a>Activer le verrou d’activation sur les appareils supervisés

Vous pouvez utiliser les paramètres de compatibilité de Configuration Manager pour créer et déployer un élément de configuration de type **iOS et Mac OS X** pour activer le verrou d’activation sur les appareils supervisés :

1. Aidez-vous des informations contenues dans la rubrique [Comment créer des éléments de configuration pour des appareils iOS et Mac OS X gérés sans le client System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client) pour créer un élément de configuration de type **iOS et Mac OS X**.
2. Dans la page **Sécurité système** de l’Assistant Création d’élément de configuration, configurez le paramètre **Autoriser le verrou d’activation (mode supervisé uniquement)** sur **Autorisé**.
3. [Ajoutez l’élément de configuration à une base de référence de configuration](/sccm/compliance/deploy-use/create-configuration-baselines).
4. [Déployez cette base de référence de configuration](/sccm/compliance/deploy-use/deploy-configuration-baselines) sur le regroupement contenant les appareils iOS pour lesquels vous voulez activer le verrou d’activation.

> [!IMPORTANT]
> Assurez-vous d’être en possession de l’appareil avant de suivre cette procédure. Si ce n’est pas le cas, le verrou d’activation sera contourné et toute personne en possession de l’appareil aura un accès total à celui-ci et aura ainsi tout loisir de désactiver l’application Rechercher mon iPhone, d’effacer le contenu du périphérique ou de le réactiver.

Vous ne pouvez contourner le verrou d’activation ou récupérer le code de contournement du verrou d’activation que sur des appareils supervisés ; toute tentative de contournement du verrou d’activation sur un appareil non supervisé ou d’affichage du code de contournement générera une erreur.



## <a name="view-the-activation-lock-bypass-code"></a>Afficher le code de contournement du verrou d’activation

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2. Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Périphériques**.
3. Sélectionnez un appareil inscrit et en mode supervisé pour lequel le verrou d’activation est activé.
4. Sous l’onglet **Accueil** , dans le groupe **Appareil** , cliquez sur **Actions de l’appareil à distance** > **Afficher le code de contournement du verrou d’activation**.
5. La boîte de dialogue **Code de contournement du verrou d’activation** affiche le code de contournement de l’appareil sélectionné.

## <a name="bypass-activation-lock"></a>Contourner le verrou d’activation

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2. Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Périphériques**.
3. Sélectionnez un appareil inscrit et en mode supervisé pour lequel le verrou d’activation est activé.
3. Sous l’onglet **Accueil** , dans le groupe **Appareils** , cliquez sur **Actions de l’appareil à distance** > **Contourner le verrou d’activation**.
5. Lisez les messages d’avertissement s’affichant dans la boîte de dialogue, puis cliquez sur **Oui** dès que vous êtes prêt à continuer.
6. Vous pouvez examiner l’état de la demande de déverrouillage via :

    - les données de découverte de l’appareil dans la boîte de dialogue des propriétés de l’appareil ;
    - la colonne **État de contournement du verrou d’activation** dans la vue **Appareils** (cette colonne est masquée par défaut) ;
    - la section d’ **informations sur les actions de l’appareil à distance** sous l’onglet **Résumé** du volet d’informations (quand un appareil est sélectionné).
