---
title: Capacités de la version Technical Preview 1604
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1604 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
robots: noindex,nofollow
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 113e22c33e9e8545c382373f3ba093dba3969939
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1604-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1604 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1604 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.  

 Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.  

##  <a name="BKMK_WindowsVPP"></a> Gérer les applications achetées en volume à partir du Windows Store pour Entreprises  
 Le [Windows Store pour Entreprises](https://www.microsoft.com/en-us/business-store) est l’emplacement où vous pouvez trouver et acheter des applications pour votre organisation, isolément ou en volume. En connectant le Store à Configuration Manager, vous pouvez gérer les applications achetées en volume à partir de la console Configuration Manager, par exemple :  

-   Vous pouvez synchroniser la liste des applications achetées avec Configuration Manager.  

-   Les applications synchronisées apparaissent dans la console Configuration Manager et vous pouvez les déployer comme les autres applications  

-   Vous pouvez suivre le nombre de licences disponibles, et le nombre de celles qui sont en cours d’utilisation dans la console Configuration Manager  

### <a name="try-it-out"></a>Essayez !  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Scénario 1 : configurer la synchronisation du Windows Store pour Entreprises  

1.  Dans Azure Active Directory, inscrivez Configuration Manager en tant qu’outil de gestion « Application web et/ou API web ». Vous obtenez ainsi un ID de client dont vous aurez besoin ultérieurement.  

    1.  Dans le nœud **Active Directory** [https://manage.windowsazure.com](https://manage.windowsazure.com), sélectionnez votre annuaire Azure Active Directory, puis cliquez sur **Applications** > **Ajouter**.  

    2.  Cliquez sur **Ajouter une application développée par mon organisation**.  

    3.  Attribuez un nom à l’application, sélectionnez **Application web** et/ou **API web**, puis cliquez sur la flèche Suivant.  

    4.  Entrez la même URL pour **URL de connexion** et pour **URI ID d’application**.  L’URL peut être une chaîne quelconque qui ne doit pas nécessairement correspondre à une adresse réelle. Par exemple, vous pouvez entrer **https://&lt;votredomaine\>/sccm**.  

    5.  Effectuez toutes les étapes de l'Assistant.  

2.  Dans Azure Active Directory, créez une clé de client pour l’outil de gestion inscrit.  

    1.  Sélectionnez l’application que vous venez de créer, puis cliquez sur **Configurer**.  

    2.  Sous **Clés**, sélectionnez une durée dans la liste, puis cliquez sur **Enregistrer**.  Cela a pour effet de créer une nouvelle clé de client.  Ne quittez pas cette page tant que vous n’avez pas correctement intégré le Windows Store pour Entreprises à Configuration Manager.  

3.  Dans le Windows Store pour Entreprises, configurez Configuration Manager en tant qu’outil de gestion du Windows Store.  

    1.  Ouvrez [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) et connectez-vous si vous y êtes invité.  

    2.  Acceptez les conditions d’utilisation si nécessaire.  

    3.  Sous **Outils de gestion**, cliquez sur **Ajouter un outil de gestion**.  

    4.  Dans **Rechercher l’outil par son nom**, tapez le nom de l’application que vous avez créée précédemment dans AAD, puis cliquez sur **Ajouter**.  

    5.  Cliquez sur **Activer** en regard de l’application que vous venez d’importer.  

    6.  Dans l’Assistant **Show Offline-Licensed Apps** (Afficher les applications sous licence hors connexion), cliquez sur **Oui** si vous souhaitez autoriser l’achat d’applications sous licence hors connexion.  

4.  Achetez au moins une application au Windows Store pour Entreprises.  

5.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Windows Store pour Entreprises**.  

6.  Sous l’onglet **Accueil** du groupe **Créer**, cliquez sur **Ajouter un compte Windows Store pour Entreprises**.  

7.  Ajoutez vos ID de locataire, ID de client et clé de client à partir d’Azure Active Directory, puis fermez l’Assistant.  

8.  Une fois que vous avez terminé, le compte que vous avez configuré figure dans la liste **Windows Store for Business Accounts** (Comptes Windows Store pour Entreprises) de la console Configuration Manager.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Scénario 2 : créer et déployer une application Configuration Manager à partir d’une application sous licence hors connexion du Windows Store pour Entreprises  

1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.  

2.  La liste **Purchased Windows Store for Business apps** (Applications du Windows Store pour Entreprises achetées) affiche une liste des applications qui ont été synchronisées à partir du Windows Store. Choisissez l’application que vous voulez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une application**.  

3.  Une application Configuration Manager contenant l’application du Windows Store pour Entreprises est alors créée. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.  

##  <a name="BKMK_PFW"></a> Améliorations apportées à la gestion de Microsoft Passport for Work  
 Vous pouvez désormais déployer des stratégies Microsoft Passport for Work sur des appareils Windows 10 joints au domaine et gérés par le client Configuration Manager.  

##  <a name="bkmk_switchsup"></a> Option permettant aux clients de basculer vers un nouveau point de mise à jour logicielle  
 Dans la version d’évaluation technique 1604, vous pouvez activer l’option permettant aux clients Configuration Manager de basculer vers un nouveau point de mise à jour logicielle quand des problèmes se posent au niveau du point de mise à jour logicielle actif. Pour utiliser cette option, vous devez disposer de plusieurs points de mise à jour logicielle sur un site principal. Vous activez cette option sur un regroupement d’appareils et, une fois activée, les clients du regroupement recherchent un autre point de mise à jour logicielle lors de l’analyse suivante quand le client ne parvient pas à se connecter au point de mise à jour logicielle actif. En fonction des paramètres de configuration WSUS (classifications des mises à jour, produits, etc.), le basculement vers un nouveau point de mise à jour logicielle génère un trafic réseau supplémentaire. Par conséquent, vous ne devez utiliser cette option qu’en cas de nécessité.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Pour activer l’option de basculement vers des points de mise à jour logicielle  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité > Vue d’ensemble > Regroupements d’appareils**.  

2.  Sous l’onglet **Accueil** , dans le groupe **Regroupement** , cliquez sur **Notification du client**, puis sur **Passer au point de mise à jour logicielle suivant**.  

> [!NOTE]  
>  Cette option est disponible uniquement sur les sites qui ont plusieurs points de mise à jour logicielle.  

##  <a name="bkmk_peercache"></a> Paramètres client pour gérer les paramètres du cache du client et le cache d’homologue du client  
 La version d’évaluation technique 1604 introduit deux nouveaux paramètres client d’appareil qui affectent l’utilisation du cache d’un client. Les deux paramètres peuvent être utilisés séparément, mais sont configurés sur la même feuille de propriétés des paramètres du client, et ils se combinent pour vous aider à gérer le déploiement de contenu sur vos clients dans des emplacements distants.  

-   Le premier nouveau paramètre est celui du **cache d’homologue du client**, solution Configuration Manager intégrée pour permettre aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local. Pour pouvoir partager du contenu, les clients du cache d’homologue doivent être membres du même groupe de limites. Le cache d’homologue ne remplace pas l’utilisation d’autres solutions telles que BranchCache, mais fonctionne en parallèle afin de vous offrir davantage d’options pour étendre les solutions de déploiement de contenu traditionnelles telles que des points de distribution.  

     Après avoir déployé des paramètres client qui activent le cache d’homologue sur un regroupement, les membres de ce regroupement peuvent agir comme une source de contenu homologue pour d’autres clients dans le groupe de limites.  Le client qui opère en tant que source de contenu homologue envoie une liste des éléments disponibles qu’il a mis en cache dans son point de gestion. Ensuite, quand le client suivant dans ce groupe de limites demande ce contenu, la source de cache d’homologue est proposée comme source de contenu potentielle, ainsi que tous les points de distribution qui sont configurés pour être rapides. Le client sélectionne une source de contenu aléatoire à partir de ce pool combiné de sources de contenu. Les clients recherchent uniquement le contenu à partir d’un point de distribution configuré pour être lent quand aucun point de distribution rapide ni aucune source de cache d’homologue ne figure dans le groupe de limites.  

-   Le deuxième nouveau paramètre vous permet de **gérer la taille du cache** sur les clients. Vous pouvez définir pour le cache une taille maximale exprimée en mégaoctets et une taille maximale exprimée en pourcentage de l’espace disque du client.  Le client applique le paramètre qui est atteint en premier.  

Pour vous aider à comprendre l’utilisation du cache d’homologue du client, vous pouvez afficher le tableau de bord **Sources de données du client**. Dans la console, accédez à **Analyse > État du client > Sources de données du client**. Vous pouvez sélectionner ici une période à appliquer au tableau de bord. Ensuite, dans l’affichage, vous pouvez sélectionner le groupe de limites ou le package sur lesquels vous souhaitez afficher des informations. Lors de la consultation de celles-ci, vous pouvez pointer le curseur de la souris sur la surface pour afficher plus de détails sur les différentes sources de contenu ou de stratégie.  

 Vous pouvez également utiliser un nouveau rapport, **Sources de données du client - Résumé**, pour afficher une synthèse des sources de données du client pour chaque groupe de limites.   
**Configuration requise pour utiliser le cache d’homologue :**  

-   Vous devez configurer votre site avec un **compte d’accès réseau** ayant le **contrôle total** du dossier de cache sur chaque client. Par défaut, il s’agit de **%windir%\ccmcache**  

-   Des clients peuvent transférer du contenu à l’aide du cache d’homologue uniquement quand ils sont membres du même groupe de limites.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>Pour configurer les paramètres client du cache d’homologue du client  

1.  Les deux paramètres sont configurés dans la même page de paramètres client. Dans la console Configuration Manager, accédez à **Administration > Paramètres client**, puis ouvrez l’objet des paramètres client d’appareil à utiliser. Vous pouvez également modifier l’objet des paramètres client par défaut.  

2.  Dans la liste des paramètres disponibles, sélectionnez **Paramètres du cache des clients**.  

3.  Pour gérer la taille du cache, affectez à **Configurer la taille du cache des clients** la valeur **Oui**. Vous pouvez ensuite configurer la taille maximale du cache en mégaoctets et en pourcentage de l’espace disque du client.  

4.  Pour permettre aux clients de participer au cache d’homologue du client, affectez à **Permettre au client Configuration Manager exécutant le système d’exploitation complet de partager du contenu** la valeur **Oui**. Vous pouvez ensuite configurer les ports que les clients utilisent, notamment s’il s’agit de HTTP ou HTTPS.  

### <a name="try-it-out"></a>Essayez !  
 Essayez d’accomplir les tâches suivantes, puis utilisez les informations relatives à l’envoi de commentaires au début de cette rubrique pour nous faire savoir comment cela a fonctionné :  

1.  Modifiez les paramètres client pour spécifier une nouvelle taille pour le cache des clients et confirmez ce paramètre sur un client.  

2.  Utiliser des paramètres client pour configurer plusieurs clients pour utiliser le cache d’homologue  

3.  Déployez le contenu sur les clients de façon à ce que certains ou la plupart d’entre eux l’obtiennent d’un autre client à l’aide du cache d’homologue.  Vous pouvez vérifier la source de contenu utilisée en affichant le nouveau tableau de bord.  

    > [!NOTE]  
    >  Pour achever cette tâche avec la version d’évaluation technique et un point de distribution unique, configurez celui-ci de façon à ce qu’il soit lent pour l’emplacement réseau de tous vos clients. Ensuite, distribuez le contenu à un seul client.  Une fois que le client a obtenu le contenu, vous pouvez distribuer le contenu à des clients supplémentaires qui doivent trouver des homologues locaux à utiliser comme source de contenu avant d’utiliser le point de distribution qui est considéré comme lent à partir de l’emplacement du client.  

##  <a name="bkmk_passport"></a> Prise en charge de Passport for Work en tant que fournisseur KSP  
 Vous pouvez intégrer System Center Configuration Manager à Microsoft Passport for Work, et disposer ainsi d’une autre méthode de connexion qui utilise Active Directory ou un compte Azure Active Directory pour remplacer un mot de passe, une carte à puce ou une carte à puce virtuelle.  
Passport vous permet d’utiliser un geste utilisateur au lieu d’un mot de passe pour vous connecter. Un geste utilisateur peut être un simple code confidentiel, une authentification biométrique telle que Windows Hello ou un appareil externe tel qu’un lecteur d’empreintes digitales.  

-   Vous pouvez utiliser Configuration Manager pour contrôler les gestes que les utilisateurs peuvent et ne peuvent pas utiliser pour se connecter, et pour configurer les exigences de complexité de code confidentiel.  

-   Vous pouvez stocker des certificats d’authentification dans le fournisseur de stockage de clés de Passport for Work.  

Quand un utilisateur crée un code confidentiel Passport, Windows envoie une notification que Configuration Manager écoute.  Cela permet à Configuration Manager de déterminer rapidement quels utilisateurs ont créé un code confidentiel Passport. Ensuite, Configuration Manager peut également émettre de nouveaux certificats pour les utilisateurs si Passport est utilisé comme fournisseur de stockage de clés dans un profil de certificat.  

##  <a name="bkmk_onpremdha"></a> Attestation d’intégrité de l’appareil en local  
 L’attestation d’intégrité pour les appareils Windows 10 peut désormais être configurée pour communiquer à l’aide de l’infrastructure locale.  Les administrateurs peuvent spécifier si le signalement s’effectue via des ressources cloud ou locales.  Si l’option **local** est sélectionnée pour le rapport d’attestation d’intégrité, vous pouvez spécifier un URI pour le service. Les ordinateurs clients sans accès à Internet peuvent utiliser celui-ci pour activer et gérer des appareils à l’aide d’une attestation d’intégrité.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Activation de l’attestation d’intégrité pour les appareils locaux  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Paramètres client**, puis affectez la valeur **Oui** à **Utiliser le service d’attestation d’intégrité local**.  

2.  Spécifiez l’ **URL du service d’attestation d’intégrité local**, puis cliquez sur **OK**.  

Pour l’essayer, configurez le service d’attestation d’intégrité local à l’aide des paramètres de l’agent client.  

##  <a name="BKMK_Smart"></a> Paramètre SmartLock pour les appareils Android  
 Un nouveau paramètre, **Allow SmartLock and other trust agents** (Autoriser SmartLock et d’autres agents de confiance) a été ajouté à l’élément de configuration **Android et Samsung KNOX**, qui vous permet de contrôler la fonctionnalité SmartLock sur les appareils Android compatibles. Cette fonctionnalité du téléphone, parfois appelée agents de confiance, vous permet de désactiver ou de contourner le mot de passe de l’écran de verrouillage de l’appareil si celui-ci se trouve dans un emplacement approuvé, comme quand il est connecté à un appareil Bluetooth spécifique, ou quand il se trouve à proximité d’une balise NFC. Vous pouvez utiliser ce paramètre pour empêcher des utilisateurs finaux de configurer SmartLock.  
