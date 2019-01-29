---
title: Capacités de la version Technical Preview 1609
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1609 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: b999fd8ab17ba0dd28710aa4a38d6417535972f2
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898560"
---
# <a name="capabilities-in-technical-preview-1609-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1609 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*



Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1609 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    

**Problèmes connus dans cette version d’évaluation technique :**  
*  Quand vous effectuez la mise à jour vers la version d’évaluation technique 1609 pour Configuration Manager, toutes les stratégies de mise à niveau d’édition que vous avez déployées sont supprimées. Pour continuer à utiliser ces stratégies, vous devez les recréer et les déployer.


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="improvements-to-endpoint-protection"></a>Améliorations apportées à Endpoint Protection
Amélioration apportée aux paramètres de stratégie de logiciel anti-programme malveillant Endpoint Protection : vous pouvez maintenant indiquer le niveau auquel Endpoint Protection Cloud Protection Service bloque les fichiers suspects. Un nouveau paramètre permet aux administrateurs de spécifier les ordinateurs présentant des risques selon les grandes quantités de logiciels malveillants qu’ils rencontrent.

## <a name="increased-number-of-enrolled-devices"></a>Nombre accru d’appareils inscrits
Les administrateurs peuvent maintenant permettre aux utilisateurs d’inscrire jusqu’à 15 appareils dans la gestion des appareils mobiles hybride avec Intune. La limite était précédemment de 5 appareils par utilisateur.

## <a name="additional-apple-dep-settings"></a>Paramètres supplémentaires du programme DEP d’Apple

Les administrateurs peuvent maintenant configurer les paramètres suivants du programme d’inscription des appareils (DEP) d’Apple dans le profil DEP pour les appareils iOS et Mac :
- **Touch ID**
- **Zoom**
- **Siri**

Si cette option est activée, l’Assistant Installation d’Apple vous invite à spécifier ce service pendant l’activation de l’appareil.

## <a name="integration-with-upgrade-analytics"></a>Intégration à Upgrade Analytics

Upgrade Analytics vous permet d’évaluer et d’analyser la disponibilité de l’appareil et la compatibilité avec Windows 10 pour faciliter et améliorer les mises à niveau. Avec l’intégration d’Upgrade Analytics à Configuration Manager, vous pouvez accéder aux données de compatibilité de mise à niveau dans la console d’administration Configuration Manager et cibler ensuite, dans la liste des appareils, ceux qui doivent être mis à niveau ou corrigés.

Pour en savoir plus sur Upgrade Analytics, consultez [Bien démarrer avec Upgrade Analytics](https://technet.microsoft.com/itpro/windows/deploy/upgrade-analytics-get-started).

## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Types de connexion natifs pour les profils hybrides VPN Windows 10

Quand vous utilisez Configuration Manager avec Intune, vous pouvez maintenant créer des profils VPN Windows 10 avec des types de connexion Microsoft Automatic, IKEv2, PPTP et L2TP dans la console Configuration Manager sans utiliser l’OMA-URI.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Améliorations de l’intégration du Windows Store pour Entreprises à Configuration Manager

Dans cette version, nous avons mis à jour [l’intégration du Windows Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) avec ces nouvelles fonctionnalités :

**Mise à jour :** dans la préversion technique actuelle, la fonctionnalité de synchronisation immédiate n’est pas fonctionnelle.

- Auparavant, vous pouviez uniquement déployer des applications gratuites à partir du Windows Store pour Entreprises. Configuration Manager prend maintenant aussi en charge le déploiement d’applications sous licence en ligne payantes (pour les appareils Intune inscrits uniquement).
- Vous pouvez désormais lancer une synchronisation immédiate entre le Windows Store pour Entreprises et Configuration Manager.
- Vous pouvez maintenant modifier la clé secrète du client que vous avez obtenue à partir d’Azure Active Directory

### <a name="try-it-out"></a>Essayez !

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Acheter et synchroniser une application sous licence en ligne payante

1. Achetez une application sous licence en ligne payante dans le Windows Store pour Entreprises.
2. Dans l’espace de travail **Administration** de la console Configuration Manager, cliquez sur **Services cloud** > **Mises à jour et maintenance** > **Windows Store pour Entreprises**.
3. Sous l’onglet **Accueil**, dans le groupe **Synchroniser**, cliquez sur **Synchroniser maintenant**.
4. Aussitôt après, l’application que vous avez achetée apparaît dans le nœud **Informations de licence pour les applications du Store** de l’espace de travail **Gestion des applications**.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Créer et déployer une application Configuration Manager à partir des données de l’application synchronisée

La procédure pour créer et déployer une application Configuration Manager à partir d’une application du Windows Store payante est identique à celle pour créer une application à partir d’une application gratuite. Consultez la section **Créer et déployer une application Configuration Manager à partir d’une application du Windows Store pour Entreprises** dans [Gérer des applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Modifier la clé secrète du client à partir d’Azure Active Directory

1. Dans l’espace de travail **Administration** de la console Configuration Manager, cliquez sur **Services cloud** > **Mises à jour et maintenance** > **Windows Store pour Entreprises**.
2. Sélectionnez votre compte Windows Store pour Entreprises, puis cliquez sur **Propriétés**.
3. Dans la boîte de dialogue **Windows Store for Business Account Properties** (Propriétés du compte Windows Store pour Entreprises), entrez une nouvelle clé dans le champ **Clé secrète du client**, puis cliquez sur **Vérifier**. Une fois la vérification effectuée, cliquez sur **Appliquer**, puis fermez la boîte de dialogue.


## <a name="new-compliance-settings-for-configuration-items"></a>Nouveaux paramètres de compatibilité pour les éléments de configuration

Nous avons ajouté de nombreux nouveaux paramètres que vous pouvez utiliser dans vos éléments de configuration pour diverses plateformes d’appareils.
Il s’agit de paramètres qui existaient précédemment dans Microsoft Intune dans une configuration autonome et qui sont maintenant disponibles quand vous utilisez Intune avec Configuration Manager.
Si vous avez besoin d’aide pour utiliser l’un de ces paramètres, ouvrez [Gérer des paramètres et des fonctionnalités sur vos appareils avec des stratégies Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies), puis sélectionnez la sous-rubrique de paramètres pour la plateforme souhaitée.


### <a name="new-settings-for-android-devices"></a>Nouveaux paramètres pour les appareils Android

#### <a name="password-settings"></a>Paramètres de mot de passe

- **Mémoriser l’historique des mots de passe**
- **Autoriser le déverrouillage par empreinte digitale**

#### <a name="security-settings"></a>Paramètres de sécurité

- **Exiger le chiffrement sur les cartes de stockage**
- **Autoriser la capture d’écran**
- **Autoriser la soumission des données de diagnostic**

#### <a name="browser-settings"></a>Paramètres du navigateur

- **Autoriser le navigateur web**
- **Autoriser le remplissage automatique**
- **Autoriser le bloqueur de fenêtres publicitaires**
- **Autoriser les cookies**
- **Autoriser les scripts actifs**

#### <a name="app-settings"></a>Paramètres de l’application

- **Autoriser Google Play Store**

#### <a name="device-capability-settings"></a>Paramètres de capacité des appareils

- **Autoriser le stockage amovible**
- **Autoriser la connexion Wi-Fi**
- **Autoriser la géolocalisation**
- **Autoriser NFC**
- **Autoriser Bluetooth**
- **Autoriser l’itinérance vocale**
- **Autoriser l’itinérance des données**
- **Autoriser les messages SMS/MMS**
- **Autoriser l’assistant vocal**
- **Autoriser la composition vocale**
- **Autoriser la fonction copier-coller**


### <a name="new-settings-for-ios-devices"></a>Nouveaux paramètres pour les appareils iOS

#### <a name="password-settings"></a>Paramètres de mot de passe

- **Nombre de caractères complexes requis dans le mot de passe**
- **Autoriser les mots de passe simples**
- **Minutes d’inactivité avant demande du mot de passe**
- **Mémoriser l’historique des mots de passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Nouveaux paramètres pour les appareils Mac OS X

#### <a name="password-settings"></a>Paramètres de mot de passe

- **Nombre de caractères complexes requis dans le mot de passe**
- **Autoriser les mots de passe simples**
- **Mémoriser l’historique des mots de passe**
- **Minutes d’inactivité avant activation de l’écran de veille**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nouveaux paramètres pour les appareils Windows 10 Desktop et Mobile

#### <a name="password-settings"></a>Paramètres de mot de passe

- **Nombre minimum de jeux de caractères**
- **Mémoriser l’historique des mots de passe**
- **Exiger un mot de passe quand l’appareil quitte un état inactif**

#### <a name="security-settings"></a>Paramètres de sécurité

- **Exiger le chiffrement sur l’appareil mobile**
- **Autoriser la désinscription manuelle**

#### <a name="device-capability-settings"></a>Paramètres de capacité des appareils

- **Autoriser une connexion VPN sur un réseau cellulaire**
- **Autoriser l’itinérance VPN sur un réseau cellulaire**
- **Autoriser la réinitialisation du téléphone**
- **Autoriser la connexion USB**
- **Autoriser Cortana**
- **Autoriser les notifications du centre de notifications**

### <a name="new-settings-for-windows-10-team-devices"></a>Nouveaux paramètres pour les appareils Windows 10 Collaboration

#### <a name="device-settings"></a>Paramètres de l’appareil

- **Activer Azure Operational Insights**
- **Activer la projection sans fil Miracast**
- **Choisir les informations relatives à la réunion affichées sur l’écran d’accueil**
- **URL de l’image d’arrière-plan de l’écran de verrouillage**


### <a name="new-settings-for-windows-81-devices"></a>Nouveaux paramètres pour les appareils Windows 8.1

#### <a name="applicability-settings"></a>Paramètres de mise en application

- **Appliquer toutes les configurations à Windows 10**

#### <a name="password-settings"></a>Paramètres de mot de passe

- **Type de mot de passe requis**
- **Nombre minimum de jeux de caractères**
- **Longueur minimale du mot de passe**
- **Nombre d’échecs de connexion successifs autorisé avant réinitialisation de l’appareil**
- **Minutes d’inactivité avant arrêt de l’écran**
- **Expiration du mot de passe (jours)**
- **Mémoriser l’historique des mots de passe**
- **Empêcher la réutilisation des mots de passe précédents**
- **Autoriser un mot de passe image et un code confidentiel**

#### <a name="browser-settings"></a>Paramètres du navigateur

- **Autoriser la détection automatique des réseaux intranet**


### <a name="new-settings-for-windows-phone-81-devices"></a>Nouveaux paramètres pour les appareils Windows Phone 8.1

#### <a name="applicability-settings"></a>Paramètres de mise en application

- **Appliquer toutes les configurations à Windows 10**

#### <a name="password-settings"></a>Paramètres de mot de passe

- **Nombre minimum de jeux de caractères**
- **Autoriser les mots de passe simples**
- **Mémoriser l’historique des mots de passe**

#### <a name="device-capability-settings"></a>Paramètres de capacité des appareils

- **Autoriser la connexion automatique aux points d’accès Wi-Fi gratuits**


## <a name="improvements-for-boundary-groups"></a>Améliorations pour les groupes de limites
Cette préversion apporte des modifications importantes aux groupes de limites et à leur fonctionnement avec les points de distribution. Ces modifications permettent de simplifier la conception de votre infrastructure de contenu tout en vous donnant davantage de contrôle sur quand et comment les clients doivent effectuer des recherches en secours dans d’autres points de distribution comme emplacements sources de contenu. Cela inclut à la fois les points de distribution cloud et locaux.

Ces améliorations remplacent les concepts et les comportements qui peuvent vous être familiers aujourd’hui (comme la configuration des points de distribution pour être rapides ou lents) par un nouveau modèle qui doit être plus facile à configurer et à gérer. Ces modifications sont également un point de départ pour les futurs changements qui vont améliorer les autres rôles de système de site que vous associez à des groupes de limites.  

La mise à niveau vers la version 1609 convertit les configurations de vos groupes de limites actuels pour les adapter au nouveau modèle, afin que ces modifications ne perturbent pas les configurations de distribution de contenu (consultez [Mettre à jour des groupes de limites existants vers le nouveau modèle](/sccm/core/get-started/capabilities-in-technical-preview-1609#bkmk_update)).

Les sections suivantes détaillent les modifications introduites dans cette préversion, le fonctionnement du nouveau modèle et les effets attendus de la mise à niveau d’un site qui a déjà des groupes de limites configurés.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Modifications de l’interface utilisateur et du comportement pour les groupes de limites et les emplacements de contenu
Voici les principales modifications apportées aux groupes de limites et à la manière dont les clients recherchent le contenu. La plupart de ces modifications et concepts fonctionnent ensemble.
- **Les configurations rapides ou lentes sont supprimées :** Vous ne configurez plus des points de distribution individuels pour qu’ils soient rapides ou lents.  Au lieu de cela, chaque système de site associé à un groupe de limites est traité de la même façon. En raison de cette modification, l’onglet **References** (Références) des propriétés du groupe de limites ne prend plus en charge la configuration rapide ou lente.
- **Nouveau groupe de limites par défaut sur chaque site :**  Chaque site principal possède un nouveau groupe de limites par défaut nommé ***Groupe-limites-site-défaut\<code_site>***.  Quand un client n’est pas à un emplacement réseau qui est affecté à un groupe de limites, ce client utilise les systèmes de site associés au groupe par défaut à partir de son site affecté. Envisagez d’utiliser ce groupe de limites en remplacement de la notion d’emplacement de secours pour le contenu.    
  -  **« Autoriser les emplacements sources de secours pour le contenu »** est supprimé : vous ne configurez plus explicitement un point de distribution de secours à utiliser, et les options associées sont supprimées de l’interface utilisateur.

  En outre, le résultat de la définition du paramètre **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** sur un type de déploiement pour les applications a changé. Ce paramètre sur un type de déploiement permet maintenant à un client d’utiliser le groupe de limites de site par défaut comme emplacement source de contenu.

  -  **Relations des groupes de limites :** chaque groupe de limites peut être lié à un ou plusieurs groupes de limites supplémentaires. Ces liens forment des relations qui sont configurées sous le nouvel onglet des propriétés du groupe de limites nommé **Relations** :
  -   Chaque groupe de limites auquel un client est directement associé est appelé groupe de limites **actuel**.  
  -   Tout groupe de limites qu’un client peut utiliser en raison d’une association entre le groupe de limites *actuel* de ce client et un autre groupe est appelé groupe de limites **voisin**.
  -  Vous ajoutez des groupes de limites qui peuvent être utilisés comme groupe de limites *voisin* sous l’onglet **Relations**. Vous pouvez également configurer une durée en minutes qui détermine quand un client qui ne parvient pas à trouver le contenu à partir d’un point de distribution dans le groupe *actuel* doit commencer à effectuer des recherches dans les emplacements de contenu de ces groupes de limites *voisins*.

      Quand vous ajoutez ou modifiez la configuration d’un groupe de limites, vous avez la possibilité de bloquer le secours sur ce groupe de limites spécifique à partir du groupe actuel que vous configurez.

  Pour utiliser la nouvelle configuration, vous définissez des associations explicites (liens) entre un groupe de limites et un autre, et configurez tous les points de distribution de ce groupe associé avec la même durée en minutes. La durée que vous configurez détermine quand un client qui ne parvient pas à trouver une source de contenu dans son groupe de limites *actuel* peut commencer à rechercher des sources de contenu dans ce groupe de limites voisin.

  En plus des groupes de limites que vous configurez explicitement, chaque groupe de limites a un lien implicite vers le groupe de limites de site par défaut. Ce lien devient actif après 120 minutes, moment auquel le groupe de limites de site par défaut devient un groupe de limites voisin qui permet aux clients d’utiliser les points de distribution associés à ce groupe de limites comme emplacements sources de contenu.

  Ce comportement remplace ce qui était précédemment désigné sous le nom de secours pour le contenu.  Vous pouvez remplacer ce comportement par défaut de 120 minutes en associant explicitement le groupe de limites de site par défaut à un groupe *actuel* et en définissant une durée spécifique en minutes ou en bloquant totalement le secours pour empêcher son utilisation.


- **Les clients tentent d’obtenir le contenu à partir de chaque point de distribution pendant 2 minutes au maximum :** quand un client recherche un emplacement source de contenu, il tente d’accéder à chaque point de distribution pendant 2 minutes avant d’essayer ensuite un autre point de distribution. Il s’agit d’un changement par rapport aux versions précédentes où les clients tentaient de se connecter à un point de distribution pendant 2 heures au maximum.

  - Le premier point de distribution qu’un client tente d’utiliser est sélectionné au hasard dans le pool des points de distribution disponibles du groupe (ou des groupes) de limites *actuel(s)* du client.

  - Après deux minutes, si le client n’a pas trouvé le contenu, il bascule vers un nouveau point de distribution et tente d’obtenir le contenu de ce serveur. Ce processus se répète toutes les deux minutes jusqu’à ce que le client trouve le contenu ou atteigne le dernier serveur dans son pool.

  - Si un client ne peut pas trouver un emplacement source de contenu valide dans son pool *actuel* avant la période de secours sur un groupe de limites *voisin*, le client ajoute alors les points de distribution de ce groupe *voisin* à la fin de sa liste actuelle, puis effectue des recherches dans le groupe étendu d’emplacements sources qui inclut les points de distribution des deux groupes de limites.

      > [!TIP]  
      > Quand vous créez un lien explicite entre le groupe de limites actuel et le groupe de limites de site par défaut, puis définissez une durée de secours inférieure à celle d’un lien vers un groupe de limites voisin, les clients commencent à effectuer des recherches dans les emplacements sources du groupe de limites de site par défaut avant d’inclure le groupe voisin.

  - Quand le client ne parvient pas à obtenir le contenu du dernier serveur dans le pool, il recommence le processus.


### <a name="how-the-new-model-works"></a>Fonctionnement du nouveau modèle
Quand vous configurez des groupes de limites, vous associez les limites (emplacements réseau) et les rôles de système de site, comme les points de distribution, au groupe de limites. Cela permet de lier les clients aux serveurs de système de site tels que les points de distribution qui se trouvent près des clients sur le réseau.   
-   Vous pouvez attribuer la même limite à plusieurs groupes de limites
-   Les serveurs de système de site, tels que les points de distribution, peuvent être associés à plusieurs groupes de limites, ce qui les rend disponibles pour une plus grande plage d’emplacements réseau
-   Si un point de distribution n’est associé à aucun groupe de limites, les clients ne sont pas en mesure d’utiliser ce point de distribution comme emplacement source de contenu.

À compter de cette version d’évaluation technique, vous définissez les relations de groupes de limites afin de configurer le comportement de secours pour les emplacements sources de contenu. Ce nouveau comportement est configuré sous le nouvel onglet **Relations** des propriétés du groupe de limites et remplace la configuration des systèmes de site (lente ou rapide) ainsi que la configuration d’un groupe de limites pour autoriser l’emplacement source de secours pour le contenu.

Sous l’onglet Relations, vous ajoutez d’autres groupes de limites pour configurer une relation à ces groupes. Chaque relation est un lien unidirectionnel entre le groupe de limites **actuel** et le groupe de limites que vous ajoutez, appelé **voisin**. Pour chaque lien créé, vous pouvez configurer des points de distribution avec une durée de secours en minutes. Cette durée permet de déterminer le délai après lequel les clients dans le groupe de limites *actuel* peuvent commencer à utiliser les points de distribution dans le groupe de limites *voisin* s’ils ne peuvent pas trouver un emplacement source de contenu valide dans leur groupe de limites actuel.

Quand un client ne peut pas trouver le contenu et commence à effectuer des recherches dans des emplacements de groupes de limites voisins, il augmente le pool des points de distribution disponibles pour ce client de manière contrôlée.  

-   Un groupe de limites peut avoir plusieurs relations. Cela vous permet de configurer le secours sur différents voisins pour qu’il intervienne après différentes périodes de temps.
-   Les clients vont uniquement utiliser en secours un groupe de limites qui est un voisin direct de leur groupe de limites actuel.
-   Quand un client est membre de plusieurs groupes de limites, le groupe de limites actuel est défini en tant qu’union de tous les groupes de limites de ce client.  Ce client peut ensuite utiliser en secours un voisin de n’importe lequel de ces groupes de limites d’origine.

Outre les liens que vous définissez, il existe un lien implicite qui est créé automatiquement entre les groupes de limites que vous créez et le groupe de limites par défaut qui est automatiquement créé pour chaque site. Ce lien automatique :
-   est utilisé par les clients qui ne sont pas sur une limite associée à un groupe de limites de votre hiérarchie et qui utilisent automatiquement le groupe de limites par défaut de leur site assigné pour identifier les emplacements sources de contenu valides ;   
-   est une option de secours par défaut entre le groupe de limites actuel et le groupe de limites de site par défaut qui est utilisé après 120 minutes.

**Exemple d’utilisation du nouveau modèle :**     
Vous créez trois groupes de limites qui ne partagent pas de limites ni de serveurs de système de site :
-   Groupe BG_A avec les points de distribution DP_A1 et DP_A2 associés au groupe
-   Groupe BG_B avec les points de distribution DP_B1 et DP_B2 associés au groupe
-   Groupe BG_C avec les points de distribution DP_C1 et DP_C2 associés au groupe

Vous ajoutez les emplacements réseau de vos clients en tant que limites uniquement au groupe de limites BG_A, puis vous configurez des relations à partir de ce groupe de limites vers les deux autres groupes de limites :
-   Vous configurez des points de distribution pour le premier groupe *voisin* (BG_B) à utiliser après 10 minutes. Ce groupe contient les points de distribution DP_B1 et DP_B2. Les deux sont correctement connectés aux emplacements des premiers groupes de limites.
-   Vous configurez le deuxième groupe *voisin* (BG_C) à utiliser après 20 minutes. Ce groupe contient les points de distribution DP_C1 et DP_C2. Les deux se trouvent sur un réseau étendu à distance des deux autres groupes de limites.
-   Vous ajoutez également un point de distribution supplémentaire qui se trouve sur le serveur de site au groupe de limites de site par défaut du site. Il s’agit de l’emplacement source de contenu que vous préférez le moins, mais il se trouve au milieu de tous les groupes de limites.

    Exemple de groupes de limites et de durées de secours :

     ![BG_Fallback](media/BG_Fallback.png)


Avec cette configuration :
-   Le client commence la recherche de contenu dans les points de distribution de son groupe de limites *actuel* (BG_A), en passant deux minutes dans chaque point avant de passer au suivant dans le groupe. Le pool des emplacements sources de contenu valides du client inclut DP_A1 et DP_A2.
-   Si le client ne parvient pas à trouver le contenu dans son groupe de limites *actuel* après une recherche de 10 minutes, il ajoute alors les points de distribution du groupe de limites BG_B à sa recherche. Il continue ensuite à rechercher le contenu dans un point de distribution de son pool combiné de points de distribution qui inclut maintenant ceux des groupes de limites BG_A et BG_B. Le client continue de contacter chaque point de distribution pendant deux minutes avant de passer au point de distribution suivant de son pool. Le pool des emplacements sources de contenu valides du client inclut DP_A1, DP_A2, DP_B1 et DP_B2.
-   Après 10 minutes supplémentaires (20 minutes au total), si le client n’a toujours pas trouvé un point de distribution avec du contenu, il étend son pool de points de distribution disponibles pour inclure ceux du deuxième groupe *voisin*, le groupe de limites BG_C. Le client dispose désormais de 6 points de distribution pour sa recherche (DP_A1, DP_A2, DP_B1, DP_B2, DP_C1 et DP_C2) et continue de changer de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.
-   Si le client n’a pas trouvé le contenu après un total de 120 minutes, il revient en arrière pour inclure le *groupe de limites de site par défaut* dans le cadre de sa recherche continue. Le pool des points de distribution inclut désormais tous les points de distribution des trois groupes de limites configurés et le point de distribution final situé sur l’ordinateur serveur de site.  Le client continue alors sa recherche de contenu, en changeant de point de distribution toutes les deux minutes jusqu’à ce qu’il trouve le contenu.

En configurant les différents groupes voisins pour être disponibles à différents moments, vous contrôlez quand des points de distribution spécifiques sont ajoutés en tant qu’emplacement source de contenu et quand, ou si, le client utilise le secours sur le groupe de limites de site par défaut comme filet de protection pour le contenu qui n’est pas disponible à partir de tout autre emplacement.


### <a name="bkmk_update"></a>Mettre à jour des groupes de limites existants vers le nouveau modèle
Quand vous installez la version 1609 et mettez à jour votre site, les configurations suivantes sont automatiquement effectuées. Elles sont destinées à vérifier que votre comportement de secours actuel reste disponible jusqu’à ce que vous configuriez de nouvelles relations et de nouveaux groupes de limites.  
- Des points de distribution non protégés sur un site sont ajoutés au groupe de limites *Groupe-limites-site-défaut\<code_site>* de ce site.
- Une copie de chaque groupe de limites existant qui inclut un serveur de site configuré avec une connexion lente est créée. Le nom du nouveau groupe est ***\<nom du groupe de limites d’origine>-Slow-Tmp*** :  
  -   Les systèmes de site qui disposent d’une connexion rapide restent dans le groupe de limites d’origine.
  -   Une copie des systèmes de site qui ont une connexion lente est ajoutée à la copie du groupe de limites. Les systèmes de site d’origine configurés comme lents restent dans le groupe de limites d’origine pour la compatibilité descendante, mais ne sont pas utilisés à partir de ce groupe de limites.
  -   Cette copie du groupe de limites n’a pas de limites associées. Toutefois, un lien de secours est créé entre le groupe d’origine et la nouvelle copie du groupe de limites dont la durée de secours a la valeur zéro.

  Le tableau suivant identifie le nouveau comportement de secours que vous pouvez attendre de la combinaison des configurations des points de distribution et des paramètres de déploiement d’origine :

Configuration du déploiement d’origine pour « Ne pas exécuter le programme » sur un réseau lent  |Configuration du point de distribution d’origine pour « Allow client to use a fallback source location for content » (Autoriser le client à utiliser un emplacement source de secours pour le contenu)  |Nouveau comportement de secours  
---------|---------|---------
Sélectionnée     |  Sélectionnée    |  **Pas de secours** : utilisez uniquement les points de distribution dans le groupe de limites actuel       
Sélectionnée     |  Non sélectionnée|  **Pas de secours** : utilisez uniquement les points de distribution dans le groupe de limites actuel       
Non sélectionnée |  Non sélectionnée|  **Secours sur le voisin** : utilisez les points de distribution dans le groupe de limites actuel, puis ajoutez les points de distribution du groupe de limites voisin. Sauf si un lien explicite vers le groupe de limites de site par défaut est configuré, les clients ne vont pas utiliser ce groupe en secours.    
Non sélectionnée | Sélectionnée     |   **Secours normal** : utilisez les points de distribution dans le groupe de limites actuel, puis ceux des groupes de limites de site par défaut et voisin

 Toutes les autres configurations de déploiement entraînent un comportement de **secours normal**.  



## <a name="office-365-client-management-dashboard"></a>Tableau de bord Gestion des clients Office 365  
La version d’évaluation technique 1609 pour Configuration Manager introduit un nouveau tableau de bord. Pour afficher le tableau de bord, dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.
>[!NOTE]
>Dans l’espace de travail **What’s New** (Nouveautés) de la console Configuration Manager, le nouveau tableau de bord est nommé de façon incorrecte **Office 365 Servicing dashboard** (Tableau de bord de maintenance Office 365).

Le tableau de bord affiche des graphiques pour les éléments suivants :

- Nombre de clients Office 365
- Versions du client Office 365
- Langues du client Office 365
- Canaux du client Office 365     
Pour plus d’informations, consultez [Présentation des canaux de mise à jour pour Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Règles de déploiement automatique avec Office 365 Client sélectionné dans l’ensemble des produits disponibles.

Vous pouvez effectuer les opérations suivantes dans le tableau de bord :
- En haut du tableau de bord, utilisez le paramètre de liste déroulante **Regroupement** pour filtrer les données de tableau de bord selon les membres d’un regroupement spécifique.
- Dans la partie supérieure droite du tableau de bord, cliquez sur **Office 365 Installer** (Programme d’installation d’Office 365) afin de démarrer l’Assistant Installation d’Office 365 Client pour déployer des applications Office 365 sur les clients. Pour plus d’informations, consultez [Déployer des applications Office 365 sur des clients](#deploy-office-365-apps-to-clients).
- Dans la partie centrale droite du tableau de bord, cliquez sur **Create an ADR** (Créer une ADR) afin d’ouvrir l’Assistant Création d’une règle de déploiement automatique pour créer une règle de déploiement automatique (ADR). Pour créer une ADR pour les applications Office 365, sélectionnez **Office 365 Client** quand vous choisissez le produit. Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- Dans la partie inférieure droite du tableau de bord, cliquez sur **Create Client Agent Settings** (Créer les paramètres de l’agent du client) pour ouvrir les paramètres de l’agent du client. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings).



Pour plus d’informations sur les mises à jour d’Office 365 ProPlus, consultez [Gérer les mises à jour d’Office 365 ProPlus avec Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="deploy-office-365-apps-to-clients"></a>Déployer des applications Office 365 sur des clients
Dans cette version, à partir du tableau de bord Gestion des clients Office 365, vous pouvez démarrer le programme d’installation d’Office 365 qui vous permet de configurer les paramètres d’installation Office 365, de télécharger des fichiers à partir de réseaux de distribution de contenu Office et de déployer les fichiers en tant qu’application dans Configuration Manager.

### <a name="limitations-of-office-365-deployment"></a>Limitations du déploiement Office 365
- Des problèmes peuvent se poser quand vous essayez d’importer les paramètres client existants (XML) dans l’Assistant d’installation d’application Office 365. Vous pouvez configurer manuellement les paramètres client sans problème.

#### <a name="to-deploy-office-365-apps-to-clients"></a>Pour déployer des applications Office 365 sur des clients
1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.
2. Cliquez sur **Office 365 Installer** (Programme d’installation d’Office 365) dans le volet supérieur droit. L’Assistant Installation d’Office 365 Client s’ouvre.
3. Dans la page **Application Settings** (Paramètres de l’application), indiquez le nom et une description de l’application, entrez l’emplacement de téléchargement pour les fichiers, puis cliquez sur **Suivant**. Notez que l’emplacement doit être spécifié sous la forme &#92;&#92;*serveur*&#92;*partage*.
4. Dans la page **Import Client Settings** (Importer les paramètres client), choisissez s’il convient d’importer les paramètres client Office 365 à partir d’un fichier de configuration XML existant ou de spécifier manuellement les paramètres, puis de cliquer sur **Suivant**.
Quand vous avez un fichier de configuration, entrez l’emplacement du fichier et passez à l’étape 7. Notez que l’emplacement doit être spécifié sous la forme &#92;&#92;*serveur*&#92;*partage*&#92;*nom_fichier*.XML.

    > [!IMPORTANT]
    >Des problèmes peuvent se poser quand vous essayez d’importer les paramètres client existants (XML) dans cette version d’évaluation technique.

5. Dans la page **Client Products** (Produits clients), sélectionnez la suite Office 365 que vous utilisez, les applications à inclure, les produits Office supplémentaires qui doivent être ajoutés, puis cliquez sur **Suivant**.
6. Dans la page **Paramètres client**, choisissez les paramètres à inclure, puis cliquez sur **Suivant**.
7. Dans la page **Déploiement**, choisissez de déployer ou non l’application, puis cliquez sur **Suivant**.
Si vous choisissez de ne pas déployer le package dans l’Assistant, passez à l’étape 9.
8. Configurez le reste des pages de l’Assistant comme vous le feriez pour un déploiement d’application standard. Pour plus d’informations, consultez [Créer et déployer une application](/sccm/apps/get-started/create-and-deploy-an-application).
9. Effectuez toutes les étapes de l'Assistant.
10. Vous pouvez déployer ou modifier l’application de la même façon que toute autre application dans Configuration Manager à partir de **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des applications** > **Applications**.

>[!NOTE]
>Après avoir déployé des applications Office 365, vous pouvez créer des règles de déploiement automatique pour mettre à jour les applications. Pour créer une ADR pour les applications Office 365, cliquez sur **Create an ADR** (Créer une ADR) et sélectionnez **Office 365 Client** quand vous choisissez le produit. Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="BKMK_UEFIConversion"></a>Améliorations apportées à la conversion du BIOS en UEFI
Vous pouvez maintenant personnaliser une séquence de tâches de déploiement de système d’exploitation avec une nouvelle variable, TSUEFIDrive, afin que l’étape Redémarrer l’ordinateur prépare une partition FAT32 sur le disque dur pour la transition vers UEFI. La procédure suivante fournit un exemple de création des étapes de séquence de tâches pour préparer le disque dur pour la conversion du BIOS en UEFI.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>Pour préparer la partition FAT32 pour la conversion en UEFI :
Dans une séquence de tâches existante pour installer un système d’exploitation, vous allez ajouter un nouveau groupe avec les étapes permettant d’effectuer la conversion du BIOS en UEFI.

1. Créez un groupe de séquences de tâches après les étapes de capture des fichiers et paramètres, et avant les étapes d’installation du système d’exploitation. Par exemple, créez un groupe après le groupe **Capturer les fichiers et les paramètres** nommé **BIOS-en-UEFI**.
2. Sous l’onglet **Options** du nouveau groupe, ajoutez une nouvelle variable de séquence de tâches comme condition où **_SMSTSBootUEFI** est **différent** de **true**. Vous empêchez ainsi l’exécution des étapes dans le groupe quand un ordinateur est déjà en mode UEFI.
![Groupe BIOS-en-UEFI](media/BIOS-to-UEFI-group.png)
3. Sous le nouveau groupe, ajoutez l’étape de séquence de tâches **Redémarrer l’ordinateur**. Dans **Spécifiez l’élément à exécuter après le redémarrage**, sélectionnez **L’image de démarrage attribuée à cette séquence de tâches** pour démarrer l’ordinateur dans Windows PE.  
4. Sous l’onglet **Options**, ajoutez une variable de séquence de tâches comme condition où **_SMSTSInWinPE est égal à False**. Vous empêchez ainsi l’exécution de cette étape si l’ordinateur est déjà dans Windows PE.

    ![Étape Redémarrer l’ordinateur](media/Restart-in-Windows-PE.png)
5. Ajoutez une étape pour démarrer l’outil OEM qui convertira le microprogramme du BIOS en UEFI. Il s’agit en général de l’étape de séquence de tâches **Exécuter la ligne de commande** avec une ligne de commande pour démarrer l’outil OEM.
5.  Ajoutez l’étape de séquence de tâches Formater et partitionner le disque pour partitionner et formater le disque dur. Dans l’étape, procédez comme suit :
    1.  Créez la partition FAT32 qui va être convertie en UEFI avant l’installation du système d’exploitation. Choisissez **GPT** pour **Type de disque**.
    ![Étape Formater et partitionner le disque](media/Format-and-partition-disk.png)
    2.  Accédez aux propriétés de la partition FAT32. Entrez **TSUEFIDrive** dans le champ **Variable**. Quand la séquence de tâches détecte cette variable, elle prépare la transition vers UEFI avant le redémarrage de l’ordinateur.
    ![Propriétés de la partition](media/Partition-properties.png)
    3. Créez une partition NTFS que le moteur de séquence de tâches utilise pour enregistrer son état et pour stocker les fichiers journaux.
6.  Ajoutez l’étape de séquence de tâches **Redémarrer l’ordinateur**. Dans **Spécifiez l’élément à exécuter après le redémarrage**, sélectionnez **L’image de démarrage attribuée à cette séquence de tâches** pour démarrer l’ordinateur dans Windows PE.  




## <a name="intune-compliance-charts"></a>Graphiques de conformité Intune
Dans cette version, vous pouvez obtenir un aperçu rapide de la conformité globale des appareils et les principales raisons de non-conformité à l’aide des nouveaux graphiques sous l’**espace de travail Analyse** dans la console Configuration Manager.

#### <a name="to-view-the-intune-compliance-charts"></a>Pour afficher les graphiques de conformité Intune
1. Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **Paramètres de compatibilité**.
2. Le graphique **Overall Device Compliance** (Conformité globale des appareils) est affiché.
3. Cliquez sur le nœud **Stratégies de conformité** pour afficher les graphiques **Overall Device Compliance** (Conformité globale des appareils) et **Top Non-Compliance Reasons** (Principales raisons de non-conformité).

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Limitations des graphiques de conformité Intune dans la version d’évaluation technique 1609
- L’exploration au niveau du détail pour le graphique **Overall Device Compliance** (Conformité globale des appareils) génère une erreur.
- Le graphique **Top Non-compliance Reasons** (Principales raisons de non-conformité) affiche le nom de la stratégie et non les raisons de non-conformité individuelles. Vous pouvez cliquer sur la stratégie pour accéder à plus d’informations et afficher les appareils qui ne sont pas conformes pour cette stratégie.

### <a name="try-it-out"></a>Essayez
Complétez les sections suivantes dans l’ordre :

#### <a name="check-overall-compliance-chart"></a>Examiner le graphique Overall Device Compliance (Conformité globale des appareils)
1. Ajoutez au moins deux stratégies de conformité iOS dans Configuration Manager. Une stratégie doit avoir un ensemble de paramètres pour les appareils (par exemple, affectez la valeur 6 à la longueur du code confidentiel). L’autre stratégie doit avoir un autre ensemble de paramètres (par exemple, la complexité du code confidentiel). Les paramètres des stratégies ne doivent pas se chevaucher ni être en conflit.
2. Déployez les deux stratégies sur un ensemble d’utilisateurs.
3. Inscrivez deux appareils iOS dans Intune en utilisant le même compte d’utilisateur, et un compte qui a reçu les stratégies à l’étape précédente. Les appareils ne doivent pas répondre aux critères de la stratégie de conformité.
4. Dans Configuration Manager, examinez le graphique **Overall Device Compliance** (Conformité globale des appareils). Les deux appareils doivent être signalés comme non conformes.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Examiner le graphique Top Non-compliance Reasons (Principales raisons de non-conformité)
5. Examinez le graphique **Top Non-compliance Reasons** (Principales raisons de non-conformité). Ce graphique répertorie les 5 principales raisons de non-conformité mais, quand uniquement deux paramètres de compatibilité ont été définis sur les stratégies, seules les 2 principales raisons de non-conformité sont affichées.
6. Cliquez sur l’une des sections dans le graphique. Les deux appareils doivent apparaître dans la vue filtrée sous **Ressources et Conformité** > **Vue d’ensemble** > **Appareil**.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Rendre les appareils conformes et examiner les graphiques
7. Rendez l’un des appareils conforme avec l’une des stratégies. Examinez de nouveau le graphique **Overall Device Compliance** (Conformité globale des appareils). Le graphique doit afficher un appareil conforme et un appareil non conforme.
8. Rendez l’autre appareil conforme avec la même stratégie. Vous allez ainsi rendre un appareil conforme avec les deux stratégies et un appareil conforme avec uniquement l’une des stratégies.
9. Examinez le graphique **Top Non-compliance Reasons** (Principales raisons de non-conformité). Une seule raison de non-conformité doit être répertoriée.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Voir aussi
[Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md)
