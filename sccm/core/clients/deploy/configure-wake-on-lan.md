---
title: Configurer l'éveil par appel réseau
titleSuffix: Configuration Manager
description: Sélectionnez les paramètres Wake On LAN dans System Center Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59d99a3e3626be111e927dae8651d2e01364ccf5
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083157"
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Guide pratique pour configurer Wake on LAN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Spécifiez les paramètres de Wake on LAN pour System Center Configuration Manager quand vous voulez sortir des ordinateurs de l’état de veille.

## <a name="bkmk_wol-1810"></a> Wake on LAN à compter de la version 1810
<!--3607710-->
À compter de Configuration Manager 1810, il existe une nouvelle façon de sortir des machines de l’état de veille. Vous pouvez sortir un client de l’état de veille depuis la console Configuration Manager, même si le client ne se trouve pas sur le même sous-réseau que le serveur de site. Si vous avez besoin de procéder à une maintenance ou d’interroger des appareils, vous n’êtes pas limité par les clients distants qui sont en veille. Le serveur de site emprunte le canal de notification des clients pour identifier d’autres clients en éveil sur le même sous-réseau distant, puis utilise ces clients pour envoyer une demande Wake On LAN (paquet magique). L’utilisation du canal de notification des clients permet d’éviter les bagotements MAC, ce qui peut entraîner la fermeture du port par le routeur. La nouvelle version de Wake on LAN peut être activée en même temps que l’[ancienne version](#bkmk_wol-previous).

### <a name="limitations"></a>Limitations

- Au moins un client du sous-réseau cible doit être en éveil.
- Cette fonctionnalité ne prend pas en charge les technologies réseau suivantes :
   - IPv6
   - Authentification réseau 802.1x
    >[!NOTE]
    > L’authentification réseau 802.1x peut fonctionner avec une configuration supplémentaire en fonction du matériel et de sa configuration.
- Les machines sortent de veille seulement quand vous les avertissez via la notification du client **Sortir de veille**.
    - Pour la sortie de veille quand une date limite est atteinte, l’ancienne version de Wake on LAN est utilisée.
    -  Si l’ancienne version n’est pas activée, la sortie de veille du client n’a pas lieu pour les déploiements créés avec les paramètres **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis** ou **Envoyer des paquets de mise en éveil**.  


### <a name="security-role-permissions"></a>Autorisations du rôle de sécurité

- **Notifier la ressource** sous la catégorie Regroupement

### <a name="configure-the-clients-to-use-wake-on-lan-starting-in-version-1810"></a>Configurer les clients pour utiliser Wake on LAN à compter de la version 1810

Auparavant, vous deviez activer manuellement le client pour Wake On LAN dans les propriétés de la carte réseau. Configuration Manager 1810 inclut un nouveau paramètre client appelé **Autoriser la sortie de veille du réseau**. Configurez et déployez ce paramètre au lieu de modifier les propriétés de la carte réseau.

1. Sous **Administration**, accédez à **Paramètres client**.
1. Sélectionnez les paramètres client que vous voulez modifier ou créez des paramètres client personnalisés à déployer. Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).
1. Sous les paramètres client **Gestion de l’alimentation**, sélectionnez **Activer** pour le paramètre **Autoriser la sortie de veille du réseau**. Pour plus d’informations sur ce paramètre, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#power-management).

4. À compter de Configuration Manager 1902, la nouvelle version de Wake on LAN prend en compte le port UDP personnalisé que vous spécifiez pour le [paramètre client](/sccm/core/clients/deploy/about-client-settings#power-management) **Numéro de port Wake On LAN (UDP)** . Ce paramètre est partagé par la nouvelle version et l’ancienne version de Wake on LAN.
 
<!--3605925-->

### <a name="wake-up-a-client-using-client-notification-starting-in-1810"></a>Sortir de veille un client en utilisant une notification du client à compter de 1810
 
Vous pouvez sortir de veille un seul client ou plusieurs clients en veille dans un regroupement. Pour les appareils qui sont déjà actifs dans le regroupement, aucune action n’est effectuée. Seuls les clients qui sont en veille reçoivent une demande Wake On LAN. Pour plus d’informations sur la façon de demander à un client de sortir de veille, consultez [Notification des clients](/sccm/core/clients/manage/client-notification).

- **Pour sortir de veille un seul client :** Cliquez avec le bouton droit sur le client, accédez à **Notification du client**, puis sélectionnez **Sortir de veille**.

   ![Notification du client Sortir de veille dans la console](media/wol-wake-up-client-notification.png)

- **Pour sortir de veille tous les clients en veille dans un regroupement :** Cliquez avec le bouton droit sur le regroupement d’appareils, accédez à **Notification du client**, puis sélectionnez **Sortir de veille**.
   - Cette action ne peut pas être effectuée sur les regroupements prédéfinis.
   - Quand vous avez à la fois des clients en veille et des clients actifs dans un regroupement, seuls les clients qui sont en veille reçoivent une demande Wake on LAN.  

### <a name="what-to-expect-when-only-the-new-version-of-wake-on-lan-is-enabled"></a>Que se passe-t-il quand seule la nouvelle version de Wake on LAN est activée ?

Quand seule la nouvelle version de Wake On LAN est activée, seule la notification du client **Sortir de veille** est activée. Les clients ne reçoivent pas de notification quand une date limite est reçue sur des déploiements comme les séquences de tâches, la distribution de logiciels ou les mises à jour logicielles. Une fois qu’une machine est à nouveau en ligne, la console indique quand elle se connecte au point de gestion.

À compter de Configuration Manager version 1902, vous pouvez spécifier le port de Wake on LAN. Ce paramètre est partagé par la nouvelle version et l’ancienne version de Wake on LAN.

### <a name="what-to-expect-when-both-versions-of-wake-on-lan-are-enabled"></a>Que se passe-t-il quand les deux versions de Wake on LAN sont activées ?

Quand les deux versions de Wake on LAN sont activées, vous pouvez utiliser la notification du client **Sortir de veille** et la sortie de veille à une date limite. La notification du client fonctionne un peu différemment du traditionnel Wake on LAN. Pour obtenir une brève explication du fonctionnement de la notification du client, consultez [Wake on LAN à compter de la version 1810](#bkmk_wol-1810) section. Le nouveau paramètre client **Autoriser la sortie de veille du réseau** va changer les propriétés de la carte réseau pour autoriser Wake on LAN. Vous n’avez plus besoin de le changer manuellement pour les nouvelles machines qui sont ajoutées à votre environnement. Toutes les autres fonctionnalités de Wake on LAN n’ont pas été modifiées.

À compter de la version 1902, la notification du client **Sortir de veille** prend en compte votre paramètre **Numéro de port Wake On LAN (UDP)** existant.


## <a name="bkmk_wol-previous"></a> Wake On LAN pour la version 1806 et antérieure

Spécifiez les paramètres d’éveil par appel réseau (« Wake On LAN ») pour System Center Configuration Manager quand vous voulez sortir des ordinateurs d’un état de veille pour installer les logiciels requis, notamment des mises à jour logicielles, des applications, des séquences de tâches ou des programmes.

Vous pouvez compléter Wake On LAN en utilisant les paramètres client du proxy de mise en éveil. Cependant, pour pouvoir utiliser le proxy de mise en éveil, vous devez au préalable activer l'éveil par appel réseau sur le site et activer les options **Utiliser uniquement les paquets de mise en éveil** et **Monodiffusion** pour la méthode de transmission de l'éveil par appel réseau. Cette solution de mise en éveil prend également en charge les connexions ad hoc, notamment les connexions Bureau à distance.

Utilisez la première procédure pour configurer l'éveil par appel réseau sur un site principal. Ensuite, utilisez la deuxième procédure pour configurer les paramètres client du proxy de mise en éveil. Cette deuxième procédure configure les paramètres client par défaut, de façon à ce que les paramètres du proxy de mise en éveil soient appliqués à tous les ordinateurs de la hiérarchie. Si vous souhaitez appliquer ces paramètres à certains ordinateurs seulement, créez un paramètre d’appareil personnalisé et attribuez-le à un regroupement contenant les ordinateurs que vous souhaitez configurer pour le proxy de mise en éveil. Pour plus d'informations sur la création de paramètres client personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Un ordinateur qui reçoit les paramètres client du proxy de mise en éveil risque d’interrompre sa connexion réseau pendant 1 à 3 secondes. Cela est dû au fait que le client doit réinitialiser la carte d’interface réseau pour activer le pilote de proxy de mise en éveil.

> [!WARNING]
> Pour éviter une interruption inattendue de vos services réseau, commencez par évaluer le proxy de mise en éveil sur une infrastructure réseau isolée et représentative. Utilisez ensuite les paramètres client personnalisés pour étendre votre test à une sélection d'ordinateurs situés sur plusieurs sous-réseaux. Pour plus d’informations sur le fonctionnement du proxy de mise en éveil, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).


### <a name="to-configure-wake-on-lan-for-a-site-for-version-1806-and-earlier"></a>Pour configurer Wake on LAN pour un site pour la version 1806 et antérieure

 Pour utiliser Wake on LAN, vous devez l’activer pour chaque site d’une hiérarchie.

1. Dans la console Configuration Manager, accédez à **Administration > Configuration du site > Sites**.
2. Cliquez sur le site principal à configurer, puis sur **Propriétés**.
3. Cliquez sur l’onglet **Wake On LAN** et configurez les options dont vous avez besoin pour ce site. Pour activer la prise en charge du proxy de mise en éveil, veillez à sélectionner **Utiliser uniquement les paquets de mise en éveil** et **Monodiffusion**. Pour plus d’informations, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Cliquez sur **OK** et répétez cette procédure pour tous les sites principaux de la hiérarchie.

![Activer Wake On LAN dans les propriétés du site](media/wol-site-properties.png)

### <a name="to-configure-wake-up-proxy-client-settings"></a>Pour configurer les paramètres client du proxy de mise en éveil

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
