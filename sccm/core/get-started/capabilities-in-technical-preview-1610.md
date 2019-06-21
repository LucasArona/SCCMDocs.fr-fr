---
title: Capacités de la version Technical Preview 1610
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique de System Center Configuration Manager, version 1610.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f497272431d8587010ecd7dc0a8205162d9ae7fd
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286351"
---
# <a name="capabilities-in-technical-preview-1610-for-system-center-configuration-manager"></a>Fonctionnalités dans la version d’évaluation technique 1610 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*



Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique de System Center Configuration Manager, version 1610. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrer par taille de contenu dans les règles de déploiement automatique
Vous pouvez désormais filtrer sur la taille du contenu des mises à jour logicielles dans les règles de déploiement automatique. Par exemple, vous pouvez définir le filtre **Taille du contenu (Ko)** sur **< 2048** pour télécharger uniquement les mises à jour logicielles inférieures à 2 Mo. Ce filtre empêche le téléchargement automatique des mises à jour logicielles volumineuses pour une meilleure prise en charge de la maintenance de bas niveau Windows simplifiée lorsque la bande passante du réseau est limitée. Pour plus d’informations, consultez [Configuration Manager et maintenance Windows simplifiée sur des systèmes d’exploitation de bas niveau](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).

#### <a name="to-configure-the-content-size-field"></a>Pour configurer le champ Taille du contenu
Pour configurer le champ **Taille du contenu (Ko)** , accédez à la page **Mises à jour logicielles** dans l’Assistant Création d’une règle de déploiement automatique, lorsque vous créez une règle ADR ou accédez à l’onglet **Mises à jour logicielles** dans les propriétés pour une règle ADR existante.

![Champ Taille du contenu](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Fonctionnalités améliorées pour les boîtes de dialogue des logiciels requis
Quand un utilisateur reçoit des logiciels requis, dans le paramètre **Répéter et me le rappeler :** , il peut choisir parmi les valeurs suivantes de la liste déroulante :
- Ultérieurement : Spécifie que les notifications sont planifiées selon les paramètres de notification configurés dans les paramètres de l’agent du client.
- Heure fixe : Indique que la notification sera programmée pour s’afficher de nouveau après l’heure sélectionnée. Par exemple, si un utilisateur sélectionne 30 minutes, la notification s’affichera de nouveau après 30 minutes.

![Page Agent ordinateur dans les paramètres de l’agent du client](media/computeragentsettings.png)

L’intervalle de répétition maximal est toujours basé sur les valeurs de notification configurées dans les paramètres de l’agent du client à tout instant le long de la chronologie du déploiement. Par exemple, si le paramètre **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)** sur la page Agent ordinateur est configuré pour 10 heures et qu’il reste plus de 24 heures avant l’échéance du lancement de la boîte de dialogue, l’utilisateur se voit proposer un ensemble d’options de répétition toujours inférieures ou égales à 10 heures. Au fur et à mesure que l’échéance approche, la boîte de dialogue affiche moins d’options, conformément aux paramètres appropriés de l’agent du client, pour chaque composant de la chronologie du déploiement.

En outre, pour un déploiement à haut risque, tel qu’une séquence de tâches déployant un système d’exploitation, l’expérience de notification de l’utilisateur final est désormais plus intrusive. Au lieu d’une notification temporaire sur la barre des tâches, chaque fois que l’utilisateur est averti qu’une maintenance logicielle critique est nécessaire, une boîte de dialogue similaire à la suivante s’affiche sur l’ordinateur de l’utilisateur :

![Boîte de dialogue Logiciel requis](media/requiredsoftwaredialog.png)


Pour plus d’informations :
- [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Guide pratique pour configurer les paramètres client](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Refuser les demandes d’application précédemment approuvées

En tant qu’administrateur, vous pouvez maintenant refuser une demande d’application précédemment approuvée. Une fois refusée, pour installer ultérieurement cette application, les utilisateurs doivent resoumettre une demande. Un refus ne désinstalle pas l’application ; au lieu de cela, il force la réapprobation de toute nouvelle demande de cette application par cet utilisateur. Auparavant, le refus d’une demande d’application était uniquement disponible pour les demandes d’application qui n’avaient pas été approuvées.

#### <a name="try-it-out"></a>Faîtes un essai
Pour refuser une demande approuvée d’application :

1.  Dans la console Configuration Manager, [créez et déployez une application](https://docs.microsoft.com/sccm/apps/deploy-use/create-applications) qui nécessite une approbation.
2.  Sur un ordinateur client, ouvrez le Centre logiciel et soumettez une demande pour l’application.
3.  Dans la console Configuration Manager, approuvez la demande d’application.
4.  Refusez la demande d’application approuvée : Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des applications** > **Demandes d’approbation** et sélectionnez la demande d’application que vous souhaitez refuser.  Dans le ruban, cliquez sur **Refuser**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Exclure des clients de la mise à niveau automatique
La version d’évaluation technique 1610 introduit un nouveau paramètre, que vous pouvez utiliser pour empêcher un regroupement de clients d’installer automatiquement les versions mises à jour du client.  Cela s’applique à la mise à niveau automatique ainsi qu’à d’autres méthodes, telles que la mise à niveau de logiciels basée sur la mise à jour, les scripts d’ouverture de session et la stratégie de groupe. Cela peut être utilisé pour un regroupement d’ordinateurs ayant besoin de plus grands soins, lors de la mise à niveau du client. Un client qui se trouve dans un regroupement exclu ignore les demandes d’installation du logiciel client mis à jour.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Configurer l’exclusion de la mise à niveau automatique
Pour configurer des exclusions de mise à niveau automatique :
1. Dans la console Configuration Manager, ouvrez **Paramètres de hiérarchie** sous **Administration > Configuration du site > Sites**, puis sélectionnez l’onglet **Mise à niveau des clients**.
2. Cochez la case **Exclure les clients spécifiés de la mise à niveau**, puis pour **Regroupement à exclure**, sélectionnez le regroupement que vous souhaitez exclure. Vous pouvez sélectionner un seul regroupement à exclure.
3. Cliquez sur **OK** pour fermer et enregistrer la configuration. Ensuite, une fois que les clients ont mis à jour la stratégie, les clients figurant dans le regroupement exclu n’installent plus automatiquement les mises à jour du logiciel client.

   ![Paramètres d’exclusion de mise à niveau automatique](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Même si l’interface utilisateur indique que les clients ne seront pas mis à niveau, quelle que soit la méthode, il existe deux méthodes que vous pouvez utiliser pour remplacer ces paramètres. L’installation Push du client et une installation manuelle du client peuvent être utilisées pour remplacer cette configuration. Pour plus d’informations, consultez la section suivante.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>Guide pratique pour mettre à niveau un client figurant dans un regroupement exclu
Quand un regroupement est configuré comme exclu, les membres de ce regroupement peuvent mettre à niveau leur logiciel client par seulement deux méthodes, qui ont priorité sur l’exclusion :
- **Installation Push du client** : Vous pouvez utiliser l’installation Push du client pour mettre à niveau un client figurant dans un regroupement exclu. Cela est autorisé, car cela est considéré comme l’intention de l’administrateur et vous permet de mettre à niveau les clients sans retirer le regroupement complet de l’exclusion.       
- **Installation manuelle du client** : Vous pouvez mettre à niveau manuellement les clients qui se trouvent dans un regroupement exclu en utilisant le commutateur de ligne de commande suivant avec ccmsetup :  ***/ignoreskipupgrade***

  Si vous tentez de mettre à niveau manuellement un client qui est membre du regroupement exclu et que vous n’utilisez pas ce commutateur, le client n’installe pas le nouveau logiciel client. Pour plus d’informations, consultez [Comment installer les clients Configuration Manager manuellement](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).

Pour plus d’informations sur les méthodes d’installation de client, consultez [Comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers).

## <a name="windows-defender-configuration-settings"></a>Paramètres de configuration de Windows Defender

Vous pouvez maintenant configurer les paramètres du client Windows Defender sur des ordinateurs Windows 10 inscrits auprès d’Intune à l’aide d’éléments de configuration de la console Configuration Manager.

Plus précisément, vous pouvez configurer les paramètres suivants de Windows Defender :
- Autoriser la surveillance en temps réel
- Autoriser la surveillance du comportement
- Activer le système NIS (Network Inspection System)
- Analyser tous les téléchargements
- Autoriser l’analyse des scripts
- Surveiller l’activité des fichiers et des programmes
  - Fichiers surveillés
- Durée du suivi des logiciels malveillants dont le cas a été résolu (en jours)
- Autoriser l’accès à l’interface utilisateur du client
- Planifier une analyse du système
  - Jour planifié
  - Heure planifiée
- Planifier une analyse quotidienne rapide
  - Heure planifiée
- Limiter l’utilisation du processeur pendant une analyse	 Analyser les fichiers d’archives
- Analyser les messages électroniques
- Analyser les lecteurs amovibles
- Analyser les lecteurs mappés
- Analyser les fichiers ouverts à partir de partages réseau
- Intervalle de mise à jour des signatures
- Activer la protection cloud
- Demander aux utilisateurs d’envoyer des exemples
- Détection des applications potentiellement indésirables
- Fichiers/dossiers exclus
- Extensions de fichier exclus
- Processus exclus

> [!NOTE]
> Ces paramètres peuvent uniquement être configurés sur des ordinateurs clients exécutant la mise à jour de novembre (1511) de Windows 10 ou ultérieure.

### <a name="try-it-out"></a>Essayez !

1.  Dans la console de Configuration Manager, cliquez sur **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de compatibilité** > **Éléments de configuration**, puis créez un **Élément de configuration**.
2.  Entrez un nom, sélectionnez **Windows 8.1 et Windows 10** sous **Paramètres pour les appareils gérés sans le client Configuration Manager**, puis cliquez sur **Suivant**.
3.  Vérifiez que les options **Tout Windows 10 (64 bits)** et **Tout Windows 10 (32 bits)** sont sélectionnées dans la page **Plateformes prises en charge**, puis cliquez sur **Suivant**.
4.  Sélectionnez le groupe de paramètres **Windows Defender**, puis cliquez sur **Suivant**.
5.  Configurez les paramètres souhaités dans cette page, puis cliquez sur **Suivant**.
6.  Effectuez toutes les étapes de l'Assistant.
7.  Ajoutez cet élément de configuration à une base de référence de configuration, puis déployez cette base de référence sur les ordinateurs exécutant la mise à jour de novembre de Windows 10 (1511) ou version ultérieure.

> [!NOTE]
> N’oubliez pas de cocher la case **Résoudre les paramètres non compatibles** durant le déploiement de la base de référence de configuration.

## <a name="request-policy-sync-from-administrator-console"></a>Synchronisation de la stratégie de demande à partir de la console administrateur

Vous pouvez désormais demander une synchronisation de la stratégie pour un appareil mobile à partir de la console Configuration Manager, au lieu d’avoir à la demander sur l’appareil. Les informations sur l’état de la demande de synchronisation sont disponibles dans une nouvelle colonne, appelée **État de la synchronisation à distance** dans la vue des appareils. L’état apparaît également dans la section **Données de découverte** de la boîte de dialogue **Propriétés** pour chaque appareil mobile.

### <a name="try-it-out"></a>Essayez !

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > Appareils.
2.  Dans le menu **Actions de l’appareil à distance**, sélectionnez **Envoyer une demande de synchronisation**.

La synchronisation peut prendre de cinq à dix minutes. Les modifications apportées à la stratégie sont synchronisées avec l’appareil. Vous pouvez suivre l’état de la demande de synchronisation dans la colonne **État de la synchronisation à distance** de la vue **Appareils** ou dans la boîte de dialogue **Propriétés** de l’appareil.

## <a name="additional-security-role-support"></a>Prise en charge des rôles de sécurité supplémentaires

Outre le rôle Administrateur complet, les rôles de sécurité intégrés suivants ont maintenant un accès complet aux éléments dans le nœud **Appareils d’entreprise**, notamment **Appareils prédéclarés**, **Profils d’inscription iOS** et **Profils d’inscription Windows** : •   **Gestionnaire de biens** •   **Gestionnaire d’accès aux ressources de l’entreprise**

L’accès en lecture seule à ces zones de la console Configuration Manager est toujours accordé au rôle **Analyste en lecture seule**.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Accès conditionnel pour les profils VPN Windows 10

Vous pouvez maintenant exiger que les appareils Windows 10 inscrits dans Azure Active Directory soient conformes pour pouvoir avoir un accès VPN via les profils VPN Windows 10 créés dans la console Configuration Manager. Ceci est possible grâce à la nouvelle case à cocher **Activer l’accès conditionnel pour cette connexion VPN** dans la page **Méthode d’authentification** de l’Assistant Profil VPN et les propriétés de profil VPN pour les profils VPN Windows 10. Vous pouvez également spécifier un certificat distinct pour l’authentification unique si vous activez l’accès conditionnel pour le profil.

## <a name="see-also"></a>Voir aussi
[Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md)
