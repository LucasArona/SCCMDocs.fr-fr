---
title: Configurer l'éveil par appel réseau
titleSuffix: Configuration Manager
description: Sélectionnez les paramètres Wake On LAN dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32753e44d188aed8d47c22030fba82f86e605efc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332448"
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Guide pratique pour configurer Wake on LAN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Spécifiez les paramètres d’éveil par appel réseau (« Wake On LAN ») pour System Center Configuration Manager quand vous voulez sortir des ordinateurs d’un état de veille pour installer les logiciels requis, notamment des mises à jour logicielles, des applications, des séquences de tâches ou des programmes.

Vous pouvez compléter Wake On LAN en utilisant les paramètres client du proxy de mise en éveil. Cependant, pour pouvoir utiliser le proxy de mise en éveil, vous devez au préalable activer l'éveil par appel réseau sur le site et activer les options **Utiliser uniquement les paquets de mise en éveil** et **Monodiffusion** pour la méthode de transmission de l'éveil par appel réseau. Cette solution de mise en éveil prend également en charge les connexions ad hoc, notamment les connexions Bureau à distance.

Utilisez la première procédure pour configurer l'éveil par appel réseau sur un site principal. Ensuite, utilisez la deuxième procédure pour configurer les paramètres client du proxy de mise en éveil. Cette deuxième procédure configure les paramètres client par défaut, de façon à ce que les paramètres du proxy de mise en éveil soient appliqués à tous les ordinateurs de la hiérarchie. Si vous souhaitez appliquer ces paramètres à certains ordinateurs seulement, créez un paramètre d’appareil personnalisé et attribuez-le à un regroupement contenant les ordinateurs que vous souhaitez configurer pour le proxy de mise en éveil. Pour plus d'informations sur la création de paramètres client personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Un ordinateur qui reçoit les paramètres client du proxy de mise en éveil risque d’interrompre sa connexion réseau pendant 1 à 3 secondes. Cela est dû au fait que le client doit réinitialiser la carte d’interface réseau pour activer le pilote de proxy de mise en éveil.

> [!WARNING]
> Pour éviter une interruption inattendue de vos services réseau, commencez par évaluer le proxy de mise en éveil sur une infrastructure réseau isolée et représentative. Utilisez ensuite les paramètres client personnalisés pour étendre votre test à une sélection d'ordinateurs situés sur plusieurs sous-réseaux. Pour plus d’informations sur le fonctionnement du proxy de mise en éveil, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>Pour configurer l'éveil par appel réseau pour un site

1. Dans la console Configuration Manager, accédez à **Administration > Configuration du site > Sites**.
2. Cliquez sur le site principal à configurer, puis sur **Propriétés**.
3. Cliquez sur l’onglet **Wake On LAN** et configurez les options dont vous avez besoin pour ce site. Pour activer la prise en charge du proxy de mise en éveil, veillez à sélectionner **Utiliser uniquement les paquets de mise en éveil** et **Monodiffusion**. Pour plus d’informations, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Cliquez sur **OK** et répétez cette procédure pour tous les sites principaux de la hiérarchie.

## <a name="to-configure-wake-up-proxy-client-settings"></a>Pour configurer les paramètres client du proxy de mise en éveil

1. Dans la console Configuration Manager, accédez à **Administration > Paramètres client**.
2. Cliquez sur **Paramètres client par défaut**, puis sur **Propriétés**.
3. Sélectionnez **Gestion de l’alimentation**, puis choisissez **Oui** pour **Autoriser le proxy de mise en éveil**.
4. Passez en revue les autres paramètres du proxy de mise en éveil et configurez-les si nécessaire. Pour plus d’informations sur ces paramètres, consultez [Paramètres de gestion de l’alimentation](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Cliquez sur **OK** pour fermer la boîte de dialogue, puis cliquez de nouveau sur **OK** pour fermer la boîte de dialogue Paramètres client par défaut.

Vous pouvez utiliser les rapports de Wake On LAN suivants pour surveiller l'installation et la configuration du proxy de mise en éveil :

- Résumé de l'état de déploiement du proxy de mise en éveil
- Détails sur l'état du déploiement de proxy de mise en éveil

> [!TIP]
> Pour vérifier le bon fonctionnement du proxy de mise en éveil, essayez de vous connecter à un ordinateur en veille. Essayez par exemple de vous connecter à un dossier partagé sur cet ordinateur ou de vous connecter à ce dernier via une connexion Bureau à distance. Si vous utilisez l’accès direct, vérifiez que les préfixes IPv6 fonctionnent en effectuant les mêmes tests sur un ordinateur en veille actuellement connecté à Internet.
