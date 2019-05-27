---
title: Référence de l’interface utilisateur du Centre d’aide et de support
titleSuffix: Configuration Manager
description: Découvrez comment utiliser les outils du Centre d’aide et de support.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 41cdebfe-b595-40aa-a385-32e0746255ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7858497f1ff49e5068da066cc481ca5fd38f825f
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500721"
---
# <a name="support-center-user-interface-reference"></a>Référence de l’interface utilisateur du Centre d’aide et de support

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article est une référence décrivant les interfaces utilisateur des outils du Centre d’aide et de support :
- Centre d’aide et de support
- Visionneuse du journal du Centre d’aide et de support
- Visionneuse du Centre d’aide et de support



## <a name="support-center-reference"></a>Référence du Centre d’aide et de support

Cette section décrit l’interface utilisateur de l’outil **Centre d’aide et de support**. 
- [Menu Fenêtre](#bkmk_support-window)  
- [Onglet Accueil](#bkmk_support-home)  
- [Onglet Client](#bkmk_support-client)  
- [Onglet Stratégie](#bkmk_support-policy)  
- [Onglet Contenu](#bkmk_support-content)  
- [Onglet Inventaire](#bkmk_support-inventory)  
- [Onglet Résolution des problèmes](#bkmk_support-troubleshoot)  
- [Onglet Journaux](#bkmk_support-logs)  


### <a name="bkmk_support-window"></a> Menu Fenêtre

Dans le coin supérieur gauche de la fenêtre du Centre d’aide et de support, sélectionnez la flèche dans la zone bleue pour ouvrir ce menu.

#### <a name="local-machine-connection"></a>Connexion à un ordinateur local
Le Centre d’aide et de support rassemble les fichiers journaux et effectue des opérations de résolution des problèmes sur le client qui exécute le Centre d’aide et de support.

#### <a name="remote-connection"></a>Connexion à distance
Établissez une connexion à distance avec un autre client Configuration Manager. Une fois la connexion établie, le Centre d’aide et de support rassemble les fichiers journaux et effectue des opérations de résolution des problèmes sur le client auquel il est connecté.

#### <a name="about"></a>À propos de
Fournit des informations sur le Centre d’aide et de support.

#### <a name="options"></a>Options
Dans la boîte de dialogue **Options** , vous pouvez effectuer les opérations suivantes :
- Réduire le mouvement des éléments animés de l’interface utilisateur  
- Modifier l’emplacement d’enregistrement par défaut des fichiers de groupe de données  
- Modifier l’emplacement des fichiers temporaires    
- Réinitialiser les avertissements. Les messages d’avertissement que vous avez supprimés s’affichent à nouveau lorsqu’ils sont déclenchés.  
- Rétablir la valeur par défaut du chemin des fichiers temporaires, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenter`

#### <a name="exit"></a>Quitter
Ferme le Centre d’aide et de support.



### <a name="bkmk_support-home"></a> Onglet Accueil

#### <a name="collect-selected-data"></a>Collecter les données sélectionnées
Le Centre d’aide et de support collecte des informations sur le client Configuration Manager. Par défaut, il collecte les types suivants :
- Fichiers journaux
- Collecteur de configuration client
- Système d'exploitation

Pour collecter d’autres types d’informations, cochez la case à côté du nom du type souhaité.

Sélectionnez la liste déroulante en bas du bouton **Collecter les données sélectionnées** dans le ruban, puis sélectionnez **Collecter toutes les données**. Cette action collecte l’ensemble complet des données d’état du client.

Pendant que le Centre d’aide et de support collecte des données, sélectionnez **Annuler la collecte** pour l’arrêter.

#### <a name="data-types"></a>Types de données
Lorsque vous cochez la case d’une option, le Centre d’aide et de support collecte ce type de données la prochaine fois que vous sélectionnez **Collecter les données sélectionnées**. Les types suivants sont disponibles :  

- **Fichiers journaux** : fichiers journaux client, y compris les journaux d’installation  

- **Stratégie** : collecte de la stratégie client  

- **Certificats** : informations de clé publique des certificats clients. Le Centre d’aide et de support ne collecte pas les clés privées de certificat.  

- **Collecteur de configuration client** : collecte les informations de client Gestionnaire de configuration. Vous ne pouvez pas désactiver ce type de données.  

- **Registre de client** : informations de configuration client du Registre. Le Centre d’aide et de support collecte uniquement les informations de Registre de Configuration Manager.  

- **WMI client** : informations de configuration de client de WMI. Le Centre d’aide et de support ne collecte pas la stratégie client.  

- **Résolution des problèmes** : données de dépannage en temps réel qui vous permettent de diagnostiquer les problèmes client courants liés à Active Directory, aux points de gestion, au réseau, aux attributions de stratégies et à l’inscription.  

    > [!NOTE]  
    > Ce type de données n’est pas pris en charge quand vous vous connectez à distance à un autre client.  

- **Vidages de débogage** : effectuez le vidage de débogage des processus clients et connexes. Les vidages de débogage peuvent être de grande ampleur. Activez cette option uniquement lors de la résolution de problèmes de performances du client.  

    > [!WARNING]  
    > La collecte des vidages de débogage augmente considérablement la taille des groupes de données (dans certains cas, plusieurs centaines de Mo).  
    >  
    > Les vidages de débogage peuvent contenir des informations sensibles, notamment des mots de passe, des secrets cryptographiques ou des données utilisateur. Les vidages de débogage doivent être collectés uniquement sur recommandation du service de support technique de Microsoft. Les groupes de données qui contiennent des vidages de débogage doivent être gérés avec soin afin d’être protégés contre tout accès non autorisé.  
    >  
    > Ce type de données n’est pas pris en charge quand vous vous connectez à distance à un autre client.  

- **Système d’exploitation** : collecte les informations de configuration relatives à la machine locale. Ces données incluent des informations sur l’installation de Windows, les cartes réseau et la configuration des services système. Vous ne pouvez pas désactiver ce type de données.  



### <a name="bkmk_support-client"></a> Onglet Client

#### <a name="load-or-refresh"></a>Charger ou actualiser
Le Centre d’aide et de support charge ou actualise les détails pour le client Configuration Manager.

#### <a name="control-client-agent-service"></a>Contrôler le service Agent du client
Effectuez l’une des actions suivantes sur le service Agent du client Configuration Manager (ccmexec) sur le client connecté :  

- **Redémarrer le client**  

    > [!IMPORTANT]  
    > Si le service Agent du client ne redémarre pas correctement, le client ne peut pas être géré par Configuration Manager tant que le service n’a pas démarré.  

- **Démarrer le client**  

- **Arrêter le client**  

    > [!IMPORTANT]  
    > Le client ne peut pas être géré par Configuration Manager tant que le service n’a pas démarré.  

#### <a name="properties"></a>Propriétés
Lorsque vous chargez les détails du client, le Centre d’aide et de support montre les propriétés suivantes :  

- **ID de client** : identificateur unique utilisé par Configuration Manager pour identifier le client  

- **ID du matériel** : identificateur unique utilisé par Configuration Manager pour identifier le matériel client  

- **Approuvé** : indique si le client est approuvé dans Configuration Manager  

- **État de l’inscription** : indique si le client est inscrit auprès de Configuration Manager  

- **Accessible sur Internet** : indique si le client est sur Internet  

- **Version** : numéro de version du client Gestionnaire de configuration installé  

- **Code de site** : code de site pour le site principal auquel le client est assigné  

- **Point de gestion attribué** : nom de domaine complet (FQDN) du point de gestion actuellement attribué au client  

- **Point de gestion résident** : nom de domaine complet (FQDN) du point de gestion résident  

- **Point de gestion proxy** : nom d’hôte ou nom de domaine complet (FQDN) du point de gestion proxy (le cas échéant)  

- **Code de site proxy** : Code du site secondaire (s'il existe)  

- **État du proxy** : état du point de gestion proxy du client Gestionnaire de configuration. Par exemple, **Actif** ou **En attente**.  



### <a name="bkmk_support-policy"></a> Onglet Stratégie

Utilisez les actions proposées sous cet onglet à la place de l’ancien outil [PolicySpy](/sccm/core/support/policy-spy).

#### <a name="load-policy"></a>Charger la stratégie
Cette option varie en fonction de la vue :

- **Charger la stratégie réelle** : sélectionnez **Réel** dans le groupe d’affichage, puis sélectionnez cette option dans le groupe de stratégie. Le Centre d’aide et de support charge la stratégie client que vous avez actuellement sélectionnée.  

- **Charger la stratégie demandée** : sélectionnez **Demandé** dans le groupe d’affichage, puis sélectionnez cette option dans le groupe de stratégie. Le Centre d’aide et de support charge la stratégie client demandée du client.  

- **Charger la stratégie par défaut** : sélectionnez **Par défaut** dans le groupe d’affichage, puis sélectionnez cette option dans le groupe de stratégie. Le Centre d’aide et de support charge la stratégie par défaut pour ce client.  

Sélectionnez la liste déroulante au bas de ce bouton pour accéder à des options supplémentaires :

- **Charger ou actualiser tout** : charge ou actualise simultanément la stratégie réelle, demandée et par défaut.  

#### <a name="actual-view"></a>Vue réelle
Ouvre la vue de la stratégie réelle

#### <a name="requested-view"></a>Vue demandée
Ouvre la vue de la stratégie demandée

#### <a name="default-view"></a>Vue par défaut
Ouvre la vue de la stratégie par défaut. (Les appareils obtiennent cette stratégie quand vous installez le client Configuration Manager.)

#### <a name="request-and-evaluate-policy"></a>Demander et évaluer la stratégie
Le Centre d’aide et de support demande la stratégie client à partir du point de gestion, puis évalue cette stratégie sur le client.

Sélectionnez la liste déroulante au bas de ce bouton pour accéder à des options supplémentaires :  

- **Demander une stratégie** : le Centre d’aide et de support demande la stratégie client à partir du point de gestion.  

- **Évaluer la stratégie** : le Centre d’aide et de support évalue la stratégie client sur le client.  

- **Rétablir la stratégie par défaut** : le Centre d’aide et de support indique au client Gestionnaire de configuration de réappliquer la stratégie par défaut. Il supprime toutes les stratégies machine et utilisateur sur le client.  

#### <a name="listen-for-policy-events"></a>Écouter les événements de stratégie
Le Centre d’aide et de support est à l’écoute des événements de stratégie. Sélectionnez à nouveau cette option pour désactiver l’écoute des événements de stratégie. Pour afficher les **événements de stratégie**, sélectionnez la flèche au bas de cet onglet. 

#### <a name="clear-events"></a>Effacer les événements
Le Centre d’aide et de support efface tous les événements de stratégie.



### <a name="bkmk_support-content"></a> Onglet Contenu

Affichez le contenu sur le client, y compris le contenu mis en cache. Surveillez la progression des déploiements des applications et des mises à jour logicielles. 

#### <a name="load-or-refresh"></a>Charger ou actualiser
*S’applique aux vues Contenu et Cache*

Le Centre d’aide et de support charge ou actualise la liste de contenu actuellement sur le client.

#### <a name="invoke-trigger"></a>Appeler le déclencheur
Les éléments suivants de ce menu demandent une action du client associée au contenu :  

- **Services d’emplacement**  

    - **Actualiser les emplacements des contenus** : actualise les points de distribution utilisés par les téléchargements de contenu actifs.  

    - **Actualiser les points de gestion** : met à jour la liste interne des points de gestion utilisés par le client.  

    - **Faire expirer les demandes de contenu** : met un terme à toutes les demandes d’emplacement de contenu dont la durée d’exécution est trop longue.  

  - **Évaluation du déploiement des applications** : démarre une tâche qui évalue les applications déployées.  

  - **Évaluation du déploiement des mises à jour logicielles** : démarre une tâche qui évalue les mises à jour logicielles déployées.  

  - **Analyse de la source des mises à jour logicielles** : démarre une tâche qui analyse les emplacements source des mises à jour.  

  - **Mise à jour de la liste de sources de Windows Installer** : démarre une tâche qui met à jour l’emplacement source pour les installations de Windows Installer (MSI).  

#### <a name="content-view"></a>Affichage du contenu
Consultez les applications, les packages et les mises à jour chargés sur le client. Quand vous sélectionnez une application, un package ou une mise à jour, vous pouvez afficher des détails sur ce contenu. Pour certaines applications, vous pouvez également effectuer les actions suivantes :  

 - **Actualiser** : actualiser l’affichage des détails  

 - **Vérifier ou Télécharger** : vérifier qu’une application est disponible pour le téléchargement  

 - **Installer** : installer l’application  

 - **Désinstaller** : Désinstaller l'application  

#### <a name="cache-view"></a>Vue Cache
Affichez la configuration du cache client et les détails sur le contenu du cache. Lorsque vous connectez le Centre d’aide et de support à un client local, vous pouvez également effectuer les actions suivantes :  

 - Pour modifier l’emplacement du cache, sélectionnez **Modifier** à côté du champ **Emplacement du cache**.  

 - Pour ajuster la taille du cache, sélectionnez **Modifier** à côté du champ **Taille du cache**.  

 - Pour effacer le cache client, sélectionnez **Effacer** à côté du champ **Cache utilisé**.  

Cette vue montre les propriétés suivantes :  

 - **Emplacement** : emplacement de chaque dossier de cache. Sélectionnez ce lien pour ouvrir le dossier dans l’Explorateur Windows.   
 - **ID du contenu**  
 - **ID du cache**  
 - **Size**  
 - **Dernière référence le** : cette propriété est la date à laquelle le client a lu ou écrit pour la dernière fois dans cet élément du cache.  

#### <a name="monitoring-view"></a>Vue Analyse
Sélectionnez **Analyse** pour afficher la progression des déploiements des mises à jour logicielles et d’application. Cette vue affiche les messages d'état déclenchés à partir de l'application et les messages d'événement WMI des mises à jour logicielles.

Pour chaque événement, cette vue montre les propriétés suivantes :  

 - **Heure** : heure à laquelle le client a déclenché l’événement  
 - **Type de rubrique** : type du message d’état  
 - **ID de rubrique** : ID du message d’état, utilisé pour le mappage à des événements de fichiers journaux  
 - **Type d’ID de rubrique** : sous-type du message d’état  
 - **ID d’état** : résultat de l’action que vous surveillez  
 - **Détails** et **Données d’événement** : informations supplémentaires sur les messages d’état affichés dans cette vue. Les détails d'état peuvent parfois être vides.  



### <a name="bkmk_support-inventory"></a> Onglet Inventaire

#### <a name="load-or-refresh"></a>Charger ou actualiser
Le Centre d’aide et de support charge ou actualise la liste d’inventaire client pour la vue sélectionnée.

#### <a name="invoke-trigger"></a>Appeler le déclencheur

> [!Note]  
> Pour les tâches autres que **Cycle du rapport de contrôle de logiciel**:  
> - Si vous demandez la tâche alors qu’une autre tâche d’inventaire est déjà en cours d’exécution, le client place en file d’attente la nouvelle tâche pour l’exécuter une fois que la tâche en cours et les autres tâches en file d’attente seront terminées.  
> - Suivez la progression de la tâche dans **InventoryAgent.log**.  

Les éléments suivants de ce menu demandent une action du client associée à l’inventaire :  

 - **Cycle de collecte des données de découverte (pulsation)** : déclenche la tâche du client utilisée pour collecter les informations de découverte d’appareil  

 - **Cycle de collecte de fichiers** : déclenche la tâche du client utilisée pour collecter les fichiers locaux  

 - **Cycle d’inventaire matériel** : déclenche la tâche du client utilisée pour collecter les données d’inventaire matériel  

 - **Cycle de collecte IDMIF** : déclenche la tâche du client utilisée pour collecter des données IDMIF  

 - **Cycle d’inventaire logiciel** : déclenche la tâche du client utilisée pour collecter les données d’inventaire logiciel  

 - **Cycle du rapport de contrôle de logiciel** : déclenche la tâche client utilisée pour générer un rapport de contrôle de logiciel et l’envoyer au point de gestion. Suivez la progression de cette tâche dans **SWMTRReportGen.log**.

 - **Envoyer les messages d’état non envoyés de la file d’attente** : déclenche la tâche client qui permet de vider la file d’attente de messages d’état.

 - **Avancé**  
     - **Cycle d’inventaire matériel (resynchronisation complète)**  
     - **Cycle d’inventaire logiciel (resynchronisation complète)**  


#### <a name="views"></a>Affichages
Si une fonctionnalité n’est pas activée, la vue n’affiche aucune donnée. 

- **État** : affiche les jeux de données d’inventaire que le client a collectés  

- **DDR** : informations sur les données de découverte client collectées à partir du client  

- **HINV** : informations sur les données d’inventaire matériel collectées à partir du client  

- **SINV** : informations sur les données d’inventaire matériel collectées à partir du client  

- **Regroupement de fichiers** : informations sur les fichiers collectés à partir du client  

- **IDMIF** : informations sur les données IDMIF et NOIDMIF collectées à partir du client  

- **Contrôle** : informations sur les données de contrôle de logiciel collectées à partir du client  



### <a name="bkmk_support-troubleshoot"></a> Onglet Résolution des problèmes

Résolvez certains des problèmes les plus courants liés aux clients Configuration Manager :  
- Problèmes avec Active Directory  
- Mise en réseau Windows  
- Configuration Manager   
    - Points de gestion  
    - Attribution de stratégie  
    - Enregistrement  


> [!NOTE]  
> Cet onglet n’est pas disponible quand vous vous connectez à un client Configuration Manager distant.


#### <a name="start"></a>Démarrer
Démarre la résolution des problèmes du client

- **Active Directory** : interroge Active Directory pour récupérer les informations publiées du site Configuration Manager  
- **MPCERTIFICATE** : Obtient les certificats du point de gestion  
- **MPLIST** : Obtient une liste des points de gestion  
- **MPKEYINFORMATION** : obtient les informations de clé de chiffrement des points de gestion  
- **Réseau** : Permet de résoudre les problèmes de mise en réseau  
- **Attributions de stratégies** : Récupère les attributions de stratégies  
- **Enregistrement** : vérifie que le client est inscrit auprès du site  

#### <a name="view-selected-log"></a>Afficher le journal sélectionné
Après avoir sélectionné une ligne sous l’onglet Résolution des problèmes, sélectionnez cette action pour consulter le fichier journal.

#### <a name="keep-previous-results"></a>Conserver les résultats précédents
Si vous tentez de résoudre les problèmes du client et voulez relancer la résolution des problèmes, choisissez cette option pour conserver les résultats de votre première tentative. Sinon, le Centre d’aide et de support remplace les fichiers journaux de résolution des problèmes précédents.



### <a name="bkmk_support-logs"></a> Onglet Journaux

Cette section liste les éléments de l’onglet **Journaux** de l’outil Centre d’aide et de support. 

Cet onglet est presque identique à l’outil **Visionneuse du journal**. L’outil **Visionneuse du journal** n’inclut pas les fonctionnalités **Configurer la journalisation du client** et **Groupes de journaux** décrites dans cette section. La section de [référence de la visionneuse du journal du Centre d’aide et de support](#bkmk_log-viewer) décrit en détail les autres options disponibles sous cet onglet.

#### <a name="configure-client-logging"></a>Configurer la journalisation du client

Spécifiez les options suivantes : 
- **Niveau de consignation client** : taille de fichier et niveau de détail des journaux  
- **Nombre maximal de fichiers** : permet d’autoriser plusieurs fichiers journaux d’un type donné  
- **Taille de fichier maximale** : taille en octets d’un fichier journal donné avant que le client crée un journal  

> [!NOTE]  
> Si vous définissez des valeurs trop basses, le client ne peut pas consigner d’informations utiles. Si vous définissez des valeurs trop élevées, les journaux du client peuvent consommer un volume important de stockage.  

#### <a name="log-groups"></a>Groupes de journaux

Au lieu de sélectionner manuellement les fichiers journaux à l’aide du bouton **Ouvrir les fichiers journaux**, utilisez cette liste déroulante pour ouvrir tous les fichiers journaux associés aux domaines de fonctionnalités suivants : 
- **Gestion de la configuration souhaitée**
- **Inventaire**
- **Distribution de logiciels**
- **Mises à jour logicielles**
- **Gestion des applications**
- **Stratégie**
- **Inscription client**
- **Déploiement du système d’exploitation**


## <a name="bkmk_log-viewer"></a> Référence de la visionneuse du journal du Centre d’aide et de support

Cette section décrit l’interface utilisateur de l’outil **Visionneuse du journal du Centre d’aide et de support**. 

- [Menu Fenêtre](#bkmk_log-window)  
- [Onglet Accueil](#bkmk_log-home)  

L’outil **Visionneuse du journal** est presque identique à l’onglet **Journaux** du **Centre d’aide et de support**. L’outil **Visionneuse du journal** n’inclut pas les options **Configurer la journalisation du client** et **Groupes de journaux**.


### <a name="bkmk_log-window"></a> Menu Fenêtre

Dans le coin supérieur gauche de la fenêtre Visionneuse du journal du Centre d’aide et de support, sélectionnez la flèche dans la zone bleue pour ouvrir ce menu.

#### <a name="open-logs"></a>Ouvrir les fichiers journaux
Accédez à l’emplacement des fichiers journaux à ouvrir. 

#### <a name="options"></a>Options
Dans la boîte de dialogue **Options** , vous pouvez effectuer les opérations suivantes :
- Réduire le mouvement des éléments animés de l’interface utilisateur  
- Enregistrer la visionneuse du journal en tant qu’application par défaut pour les fichiers journaux dotés de l’extension de fichier .log ou .lo_  
- Réinitialiser les avertissements. Les messages d’avertissement que vous avez supprimés s’affichent à nouveau lorsqu’ils sont déclenchés.  

#### <a name="about"></a>À propos de
Affiche des informations sur la visionneuse du journal du Centre d’aide et de support

#### <a name="close"></a>Fermer
Ferme la visionneuse du journal du Centre d’aide et de support


### <a name="bkmk_log-home"></a> Onglet Accueil

#### <a name="open-logs"></a>Ouvrir les fichiers journaux 
Le Centre d’aide et de support vous invite à sélectionner un ou plusieurs fichiers journaux à ouvrir.

Sélectionnez la liste déroulante au bas du bouton **Ouvrir les fichiers journaux** dans le ruban, puis sélectionnez l’une des options supplémentaires suivantes : 
- **Ouvrir les fichiers journaux dans l’affichage actuel** : ouvre les fichiers journaux sélectionnés dans l’affichage actuel  
- **Ouvrir les journaux dans une nouvelle fenêtre** : ouvre les fichiers journaux sélectionnés dans une nouvelle fenêtre **Visionneuse du journal**  

#### <a name="close-and-clear-logs"></a>Fermer et effacer les journaux
Ferme tous les fichiers journaux ouverts. Efface également toutes les entrées de fichier journal affichées dans la fenêtre. Le Centre d’aide et de support n’affichera plus ces entrées.

Sélectionnez la liste déroulante au bas du bouton **Fermer et effacer les journaux** dans le ruban, puis sélectionnez l’une des options supplémentaires suivantes : 
- **Effacer toutes les entrées** : Efface toutes les entrées de fichier journal affichées dans la fenêtre. Le Centre d’aide et de support n’affichera plus ces entrées.  
- **Fermer tous les journaux** : Ferme tous les fichiers journaux ouverts  

#### <a name="find"></a>Trouver
Ouvre la boîte de dialogue **Rechercher**. Entrez une chaîne à rechercher. Pour éviter les correspondances sur des chaînes courtes dans d’autres chaînes, vous pouvez choisir de rechercher des mots entiers. Vous pouvez également décider d’effectuer une recherche respectant la casse pour la chaîne.

#### <a name="find-next"></a>Rechercher suivant
Après avoir trouvé une correspondance pour la chaîne que vous recherchez, cette option affiche la correspondance suivante.

#### <a name="find-previous"></a>Rechercher précédent
Après avoir trouvé au moins deux correspondances pour la chaîne que vous recherchez, cette option affiche la correspondance précédente.

#### <a name="options"></a>Options

- **Mise à jour dynamique** : surveillez un fichier journal actuellement ouvert pour rechercher des modifications. Cette fonctionnalité ne fonctionne pas quand plusieurs fichiers journaux sont ouverts. Cette option est activée par défaut.  

- **Défilement automatique** : si vous avez également choisi l’option **Mise à jour dynamique**, cette option permet de faire défiler automatiquement la vue du journal pour afficher les dernières entrées ajoutées. Cette fonctionnalité ne fonctionne pas quand plusieurs fichiers journaux sont ouverts. Cette option est activée par défaut.  

- **Afficher les détails** : quand vous sélectionnez un message de fichier journal, les détails du message du fichier journal sont affichés au bas de l’onglet **Journaux**. Cette option est activée par défaut.  

- **Filtre rapide** : filtrez les messages de fichier journal dans tous les fichiers journaux ouverts pour rechercher une chaîne spécifique. Vous pouvez filtrer par texte du journal, nom du composant et ID de thread Pour rechercher des messages de journal similaires, cliquez avec le bouton droit sur un message de journal et sélectionnez **Filtre rapide** sur le texte du journal.  

- **Retour automatique du texte du journal** : renvoyez à la ligne les messages longs et multilignes afin qu’ils tiennent dans une seule colonne. Ce comportement facilite la lecture des messages. Cette option est activée par défaut.  

- **Affichage des entrées brutes du journal** : affiche les lignes de journal non traitées.  

- **Filtres avancés** : ouvrez la boîte de dialogue **Filtres avancés**. Pour plus d’informations, consultez [Filtres de fichier journal avancés](#bkmk_adv-filters).  

- **Liens de code d’erreur** : les codes d’erreur sont mis en surbrillance et interactifs dans le texte du journal. Cette option est activée par défaut.  

#### <a name="error-lookup"></a>Recherche d'erreurs
Entrez un code d’erreur pour le rechercher dans les fichiers journaux ouverts. Utilisez les formats de code d’erreur suivants :
 - **Entier 32 bits (signé)** : Par exemple, `-2147024891`  
 - **Entier 32 bits (non signé)** : Par exemple, `2147942405`  
 - **Hexadécimal 32 bits** : Par exemple, `0x80070005`  

#### <a name="decode-certificate"></a>Décoder un certificat
Dans la boîte de dialogue **Décoder un certificat**, collez la valeur sérialisée de n’importe quel certificat sur le client. Recherchez cette valeur dans le Registre, les fichiers journaux ou WMI. Sélectionnez **Processus** pour afficher des informations générales et des détails sur le certificat. Ces informations incluent son chemin de certification. Sélectionnez **Exporter** pour exporter le certificat en tant que fichier  **.cer**.



## <a name="bkmk_adv-filters"></a> Filtres de fichier journal avancés

Les filtres de fichier journal avancés permettent d’inclure, d’exclure ou de mettre en surbrillance des chaînes spécifiques. Ces chaînes peuvent apparaître dans un fichier journal ou un groupe de fichiers journaux lorsque vous examinez les entrées des fichiers journaux. Utilisez des recherches par caractères génériques lors de la création d’un filtre. Lorsque vous disposez d’une combinaison utile de filtres, enregistrez-les en tant que *jeu de filtres*. 

Les filtres de fichier journal avancés ont priorité sur les filtres rapides. Utilisez les deux ensemble, mais les filtres rapides s’appliquent uniquement aux données de journal affichées. Les filtres avancés déterminent les données initialement affichées avant l’application des filtres rapides.

Dans la boîte de dialogue Filtres avancés, vous pouvez créer des jeux de filtres complexes. Ces jeux de filtres recherchent les chaînes parmi de nombreux composants de fichier journal. Ces composants incluent les messages, les threads et les niveaux et composants de journalisation. Un jeu de filtres contient plusieurs instructions de filtre qui permettent d’inclure, d’exclure ou de mettre en surbrillance des messages du fichier journal. Un filtre définit une colonne de fichier journal où rechercher, un opérateur et une valeur. Cette valeur peut contenir des expressions régulières, telles que le caractère *générique* `*`.


### <a name="add-a-filter"></a>Ajouter un filtre

1. Dans la fenêtre **Visionneuse du journal** ou sous l’onglet **Journaux** du Centre d’aide et de support, sélectionnez **Filtres avancés**.  

2. Dans la boîte de dialogue Filtres avancés, sélectionnez **Ajouter**. Ensuite, sélectionnez l’une des options suivantes pour traiter les entrées de journal qui correspondent à votre filtre :  
    - **Inclure**  
    - **Exclure**  
    - **Highlight**  

3. Dans la boîte de dialogue **Configuration du filtre avancé**, choisissez une colonne et un opérateur :  

    - **Colonne** : choisir l’emplacement où rechercher les chaînes correspondant à votre filtre :  

         - **Texte du journal** : rechercher dans le texte d’un fichier journal  

         - **Gravité des journaux** : recherchez des journaux avec un niveau de gravité spécifique. Définissez ces niveaux de gravité dans le champ **Valeur**.  

         - **Composant** : rechercher un composant spécifique par nom  

         - **ID de thread** : rechercher les messages de journal dotés d’un ID de thread spécifique  

         - **Fichier source** : rechercher les messages de journal figurant dans un fichier journal spécifique  

    - **Opérateur** : choisir un opérateur pour votre filtre  

4. Entrez une valeur de filtre dans le champ **Valeur**. Si la valeur contient des expressions régulières, sélectionnez **Permettre une correspondance d’expression régulière**.  


### <a name="manage-filter-sets"></a>Gérer des jeux de filtres

  - Pour modifier un filtre, sélectionnez-le puis sélectionnez **Modifier**.  

  - Pour supprimer un filtre, sélectionnez-le puis sélectionnez **Supprimer**.  

  - Pour effacer tous les filtres, sélectionnez **Effacer**.  

  - Pour enregistrer le jeu de filtres actuel, sélectionnez **Enregistrer les filtres**. Ensuite, enregistrez votre jeu de filtres en tant que fichier **.filterset**.  

  - Pour charger un jeu de filtres enregistré, sélectionnez **Charger des filtres**. Accédez ensuite à un fichier **.filterset** précédemment enregistré.  



## <a name="bkmk_viewer"></a> Référence de la visionneuse du Centre d’aide et de support

Cette section décrit l'interface utilisateur (IU) de la **visionneuse du Centre d'aide et de support** de Configuration Manager. Les onglets disponibles varient en fonction du contenu du groupe de résolution des problèmes. Le [menu fenêtre](#bkmk_viewer-window) et l’[onglet Accueil](#bkmk_viewer-home) sont affichés par défaut.
- [Menu Fenêtre](#bkmk_viewer-window)
- [Onglet Accueil](#bkmk_viewer-home)
- [Onglet Configuration](#bkmk_viewer-config)
- [Onglet Journaux](#bkmk_viewer-logs)
- [Onglet Vidages de débogage](#bkmk_viewer-debug)
- [Onglet WMI](#bkmk_viewer-wmi)
- [Onglet Registre](#bkmk_viewer-registry)
- [Onglet Stratégie](#bkmk_viewer-policy)
- [Onglet Certificats](#bkmk_viewer-certs)
- [Onglet Résolution des problèmes](#bkmk_viewer-troubleshoot)


### <a name="bkmk_viewer-window"></a> Menu Fenêtre

Dans le coin supérieur gauche de la fenêtre Visionneuse du Centre d’aide et de support, sélectionnez la flèche dans la zone bleue pour ouvrir ce menu.

#### <a name="open-bundle"></a>Ouvrir le groupe
Accédez à l’emplacement d’un groupe de données créé par le Centre d’aide et de support.

#### <a name="about"></a>À propos de
Affiche des informations sur la visionneuse du Centre d’aide et de support.

#### <a name="options"></a>Options
Dans la boîte de dialogue **Options** , vous pouvez effectuer les opérations suivantes :
- Réduire le mouvement des éléments animés de l’interface utilisateur  
- Modifier l’emplacement des fichiers temporaires    
- Réinitialiser les avertissements. Les messages d’avertissement que vous avez supprimés s’affichent à nouveau lorsqu’ils sont déclenchés.  
- Rétablir la valeur par défaut du chemin des fichiers temporaires, `%UserProfile%\AppData\Local\Microsoft\ConfigMgrSupportCenterViewer`  


#### <a name="exit"></a>Quitter
Ferme la visionneuse du Centre d'aide et de support


### <a name="bkmk_viewer-home"></a> Onglet Accueil

#### <a name="open-bundle"></a>Ouvrir le groupe
Accédez à l’emplacement d’un groupe de données créé par le Centre d’aide et de support.

#### <a name="open-log-file"></a>Ouvrir un fichier journal
Sélectionnez un ou plusieurs fichiers journaux à ouvrir.

#### <a name="decode-certificate"></a>Décoder un certificat
Dans la boîte de dialogue **Décoder un certificat**, collez la valeur sérialisée de n’importe quel certificat sur le client. Recherchez cette valeur dans le Registre, les fichiers journaux ou WMI. Sélectionnez **Processus** pour afficher des informations générales et des détails sur le certificat. Ces informations incluent son chemin de certification. Sélectionnez **Exporter** pour exporter le certificat en tant que fichier  **.cer**.


### <a name="bkmk_viewer-config"></a> Onglet Configuration

L'onglet **Configuration** de la visionneuse du Centre d'aide et de support propose les vues suivantes à partir des données récupérées auprès des fournisseurs WMI :

#### <a name="client"></a>Client
Cette vue affiche les mêmes informations que l’onglet **Client** du Centre d’aide et de support.

#### <a name="operating-system"></a>Système d'exploitation
Détails du système d’exploitation du client. Elle utilise la classe [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="computer"></a>Ordinateur
Détails de l’ordinateur client. Elle utilise la classe [Win32_OperatingSystem](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-operatingsystem).

#### <a name="services"></a>Services
Détails des services en cours d’exécution sur l’ordinateur client. Elle utilise la classe [Win32_Service](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-service).

#### <a name="network-adapters"></a>Cartes réseau
Détails des cartes réseau installées sur l’ordinateur client. Elle utilise la classe [Win32_NetworkAdapterConfiguration](https://docs.microsoft.com/windows/desktop/CIMWin32Prov/win32-networkadapterconfiguration).


### <a name="bkmk_viewer-logs"></a> Onglet Journaux

L'onglet **Journaux** affiche une liste des fichiers journaux du groupe. Chaque ligne de cet onglet fournit le chemin, le nom et la taille du fichier journal. 

#### <a name="open"></a>Ouvrir
Après avoir sélectionné un fichier journal, sélectionnez ce bouton pour ouvrir la **visionneuse du journal**. Elle fournit un sous-ensemble des fonctionnalités affichées sous l’onglet Journaux du Centre d’aide et de support.

#### <a name="decode-certificate"></a>Décoder un certificat
Dans la boîte de dialogue **Décoder un certificat**, collez la valeur sérialisée de n’importe quel certificat sur le client. Recherchez cette valeur dans le Registre, les fichiers journaux ou WMI. Sélectionnez **Processus** pour afficher des informations générales et des détails sur le certificat. Ces informations incluent son chemin de certification. Sélectionnez **Exporter** pour exporter le certificat en tant que fichier  **.cer**.


### <a name="bkmk_viewer-debug"></a> Onglet Vidages de débogage

Chaque ligne de cet onglet fournit des détails sur les fichiers de vidage de débogage pouvant être exportés. Utilisez cet onglet pour exporter les fichiers de vidage de débogage (.dmp) en vue d’une analyse ultérieure. Cette analyse utilise un outil de débogage tel que WinDbg. 

> [!WARNING]  
> Les vidages de débogage peuvent contenir des informations sensibles, notamment des mots de passe, des secrets cryptographiques ou des données utilisateur. Collectez les vidages de débogage uniquement sur recommandation du service de support technique de Microsoft. Les groupes de données qui contiennent des vidages de débogage doivent être gérés avec soin afin d’être protégés contre tout accès non autorisé.  

#### <a name="export"></a>Exporter
Enregistrez une copie du fichier de vidage de débogage sélectionné.


### <a name="bkmk_viewer-wmi"></a> Onglet WMI

Cet onglet affiche l’ensemble des données WMI du client Configuration Manager incluses dans le groupe de données. 

#### <a name="find"></a>Trouver
Ouvre la boîte de dialogue Rechercher, qui propose les fonctionnalités suivantes :  

- **Chaîne à rechercher** : entrez une chaîne à rechercher dans le jeu de données WMI. Les caractères génériques sont pris en charge.  

- **Consulter** : choisissez si vous souhaitez chercher dans le jeu de données WMI un **Nom de classe ou d’instance**, une **Propriété** ou une **Valeur**.  

- **Mot entier seulement** : par défaut, la boîte de dialogue Rechercher recherche les chaînes qui contiennent la chaîne que vous recherchez. Cochez cette case pour ne rechercher que les chaînes qui correspondent exactement à la chaîne recherchée.  

#### <a name="find-next"></a>Rechercher suivant
Ce bouton ouvre l'instance suivante de la chaîne que vous avez indiquée dans la boîte de dialogue Rechercher dans le jeu de données WMI.

#### <a name="decode-certificate"></a>Décoder un certificat
Dans la boîte de dialogue **Décoder un certificat**, collez la valeur sérialisée de n’importe quel certificat sur le client. Recherchez cette valeur dans le Registre, les fichiers journaux ou WMI. Sélectionnez **Processus** pour afficher des informations générales et des détails sur le certificat. Ces informations incluent son chemin de certification. Sélectionnez **Exporter** pour exporter le certificat en tant que fichier  **.cer**.


### <a name="bkmk_viewer-registry"></a> Onglet Registre

Utilisez l’onglet **Registre** pour afficher les données de Registre incluses dans le groupe de données et exporter ces données en vue d’une analyse ultérieure.

#### <a name="export"></a>Exporter
Enregistrez une copie de la clé de Registre et des sous-clés que vous sélectionnez en tant que fichier de Registre (.reg).

#### <a name="find"></a>Trouver
Ouvre la boîte de dialogue Rechercher, qui propose les fonctionnalités suivantes :  

- **Chaîne à rechercher** : entrez une chaîne à rechercher dans le jeu de données WMI. Les caractères génériques sont pris en charge.  

- **Consulter** : choisissez si vous souhaitez chercher dans le jeu de données WMI un **Nom de classe ou d’instance**, une **Propriété** ou une **Valeur**.  

- **Mot entier seulement** : par défaut, la boîte de dialogue Rechercher recherche les chaînes qui contiennent la chaîne que vous recherchez. Cochez cette case pour ne rechercher que les chaînes qui correspondent exactement à la chaîne recherchée.  

#### <a name="find-next"></a>Rechercher suivant
Ce bouton ouvre l'instance suivante de la chaîne que vous avez indiquée dans la boîte de dialogue Rechercher dans le jeu de données WMI.

#### <a name="decode-certificate"></a>Décoder un certificat
Dans la boîte de dialogue **Décoder un certificat**, collez la valeur sérialisée de n’importe quel certificat sur le client. Recherchez cette valeur dans le Registre, les fichiers journaux ou WMI. Sélectionnez **Processus** pour afficher des informations générales et des détails sur le certificat. Ces informations incluent son chemin de certification. Sélectionnez **Exporter** pour exporter le certificat en tant que fichier  **.cer**.


### <a name="bkmk_viewer-policy"></a> Onglet Stratégie

L'onglet **Stratégie** permet d'afficher les données de stratégie du groupe de données. 

#### <a name="find"></a>Trouver
Ouvre la boîte de dialogue Rechercher, qui propose les fonctionnalités suivantes :  

- **Chaîne à rechercher** : entrez une chaîne à rechercher dans le jeu de données WMI. Les caractères génériques sont pris en charge.  

- **Consulter** : choisissez si vous souhaitez chercher dans le jeu de données WMI un **Nom de classe ou d’instance**, une **Propriété** ou une **Valeur**.  

- **Mot entier seulement** : par défaut, la boîte de dialogue Rechercher recherche les chaînes qui contiennent la chaîne que vous recherchez. Cochez cette case pour ne rechercher que les chaînes qui correspondent exactement à la chaîne recherchée.  

#### <a name="find-next"></a>Rechercher suivant
Ce bouton ouvre l'instance suivante de la chaîne que vous avez indiquée dans la boîte de dialogue Rechercher dans le jeu de données WMI.

#### <a name="decode-certificate"></a>Décoder un certificat
Dans la boîte de dialogue **Décoder un certificat**, collez la valeur sérialisée de n’importe quel certificat sur le client. Recherchez cette valeur dans le Registre, les fichiers journaux ou WMI. Sélectionnez **Processus** pour afficher des informations générales et des détails sur le certificat. Ces informations incluent son chemin de certification. Sélectionnez **Exporter** pour exporter le certificat en tant que fichier  **.cer**.


### <a name="bkmk_viewer-certs"></a> Onglet Certificats

L'onglet **Certificats** permet d'afficher les certificats dans le groupe de données et de les exporter.

#### <a name="view-certificate"></a>Afficher le certificat
Affiche des informations sur un certificat sélectionné.

#### <a name="export"></a>Exporter
Ouvre une boîte de dialogue **Enregistrer sous** pour enregistrer une copie du certificat sélectionné.


### <a name="bkmk_viewer-troubleshoot"></a> Onglet Résolution des problèmes

Utilisez l’onglet **Résolution des problèmes** pour afficher les fichiers journaux créés à l’aide de l’onglet Résolution des problèmes du Centre d’aide et de support.

#### <a name="view-log"></a>Afficher le journal
Après avoir sélectionné une ligne sous l’onglet **Résolution des problèmes**, sélectionnez cette option pour consulter le fichier journal avec la visionneuse du journal.
