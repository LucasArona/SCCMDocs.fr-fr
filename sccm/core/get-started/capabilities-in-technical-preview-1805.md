---
title: Version Technical Preview 1805
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités disponibles dans Configuration Manager Technical Preview version 1805.
ms.date: 05/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: ce70f690899e6ad9413c1fcd57e3f1b47a61fd4b
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623311"
---
# <a name="capabilities-in-technical-preview-1805-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1805 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans Configuration Manager Technical Preview version 1805. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités au site de votre préversion technique. 

Consultez l’article [Technical Preview](/sccm/core/get-started/technical-preview) avant d’installer cette mise à jour. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  



## <a name="create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence"></a>Créer un déploiement en plusieurs phases configurées manuellement pour une séquence de tâches
<!--1358148-->
Il est désormais possible de [créer un déploiement par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) configurées manuellement pour une séquence de tâches. Vous pouvez ajouter jusqu’à 10 phases supplémentaires sous l’onglet **Phases** de l’Assistant Création d’un déploiement par phases. 


### <a name="try-it-out"></a>Essayez !
Suivez les instructions pour créer un déploiement en plusieurs phases que vous configurez manuellement. Envoyez-nous vos [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné. 

1. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.  

2. Cliquez avec le bouton droit sur une séquence de tâches et sélectionnez **Créer un déploiement par phases**.  

3. Sous l’onglet **Général**, donnez un nom et une description (facultative) au déploiement par phases, puis sélectionnez **Configurer manuellement toutes les phases**.  

4. Sous l’onglet **Phases**, cliquez sur **Ajouter**.  

5. Spécifiez un **nom** pour la phase, puis accédez au **Regroupement de phases** cible.  

6. Sous l’onglet **Paramètres de phase**, choisissez une option pour chacun des paramètres de planification, puis sélectionnez **Suivant** quand vous avez terminé.  

    - Critères de réussite de la phase précédente (cette option est désactivée pour la première phase).
        - **Pourcentage de réussite du déploiement** : spécifiez le pourcentage d’appareils sur lesquels le déploiement est effectué conformément aux critères de réussite de la phase précédente.  

    - Conditions pour commencer cette phase de déploiement après la réussite de la phase précédente  
        - **Commencer automatiquement cette phase après une période de report (en jours)** : choisissez le nombre de jours d’attente avant de passer à la phase suivante après la réussite de la phase précédente. 
        - **Commencer manuellement cette phase de déploiement** : choisissez cette option pour ne pas commencer cette phase automatiquement après la réussite de la précédente.  

    - Dès qu’un appareil est ciblé, installer le logiciel
        - **Dès que possible** : l’échéance d’installation sur l’appareil correspond au moment où celui-ci est ciblé.
        - **Date d’échéance (par rapport au moment où l’appareil est ciblé)** : l’échéance d’installation correspond à un certain nombre de jours après que l’appareil a été ciblé.  
     
7. Exécutez l’Assistant Paramètres de phase.

8. Sous l’onglet **Phases** de l’Assistant Création d’un déploiement par phases, vous pouvez maintenant ajouter, supprimer, réorganiser ou modifier les phases du déploiement.  

9. Exécutez l’Assistant Création d’un déploiement par phases.  



## <a name="cloud-distribution-point-support-for-azure-resource-manager"></a>Prise en charge du point de distribution cloud pour Azure Resource Manager
<!--1322209-->
Lors de la création d’une instance de [point de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure), l’Assistant offre maintenant la possibilité de créer un **déploiement Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) est une plateforme moderne permettant de gérer l’ensemble des ressources de la solution comme une seule entité, nommée [groupe de ressources](/azure/azure-resource-manager/resource-group-overview#resource-groups). Lors du déploiement d’un point de distribution cloud avec Azure Resource Manager, le site utilise Azure Active Directory (Azure AD) pour authentifier et créer les ressources cloud nécessaires. Le certificat de gestion Azure classique n’est pas nécessaire pour ce déploiement modernisé.  

L’Assistant Point de distribution cloud propose toujours l’option de **déploiement de service classique** à l’aide d’un certificat de gestion Azure. Pour simplifier le déploiement et la gestion des ressources, nous vous recommandons d’utiliser le modèle de déploiement Azure Resource Manager pour tous les points de distribution cloud. Si possible, redéployez les points de distribution cloud existants avec Resource Manager.

Configuration Manager ne migre pas les points de distribution cloud classiques existants vers le modèle de déploiement Azure Resource Manager. Créez de nouveaux points de distribution cloud à l’aide de déploiements Azure Resource Manager, puis supprimez les points de distribution cloud classiques. 

> [!IMPORTANT]  
> Cette fonctionnalité ne permet pas la prise en charge des fournisseurs de services cloud Azure. Les déploiements de points de distribution cloud avec Azure Resource Manager continuent d’utiliser le service cloud classique, que ne prend pas en charge le fournisseur de services cloud. Pour plus d’informations, consultez les [services Azure disponibles auprès du fournisseur de services cloud Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="prerequisites"></a>Prérequis  
- Intégration à [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Découverte d’utilisateurs Azure AD non requise.  

- Mêmes [exigences pour le point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_requirements), à l’exception du certificat de gestion Azure.  


### <a name="try-it-out"></a>Essayez !  
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis sélectionnez **Points de distribution cloud**. Dans le ruban, cliquez sur **Créer un point de distribution cloud**.   

2. Sur la page **Général**, sélectionnez **Déploiement Azure Resource Manager**. Cliquez sur **Se connecter** pour vous authentifier avec un compte Administrateur d’abonnement Azure. L’Assistant remplit automatiquement les champs restants à partir des informations de l’abonnement Azure AD stockées dans les prérequis de l’intégration. Si vous possédez plusieurs abonnements, sélectionnez celui que vous souhaitez utiliser. Cliquez sur **Suivant**.  

3. Dans la page **Paramètres**, fournissez le **fichier de certificat** PKI de serveur. Ce certificat définit le **FQDN du service** du point de distribution cloud utilisé par Azure. Sélectionnez la **Région**, puis une option de groupe de ressources : soit **Nouveau**, soit **Existant**. Entrez le nom du nouveau groupe de ressources, ou sélectionnez un groupe de ressources existant dans la liste déroulante.  

4. Effectuez toutes les étapes de l'Assistant.  

> [!NOTE]  
> Pour l’application serveur Azure AD sélectionnée, Azure affecte l’autorisation **contributeur** de l’abonnement.  

Suivez la progression du déploiement de service avec **cloudmgr.log** sur le point de connexion du service.



## <a name="take-actions-based-on-management-insights"></a>Agir en fonction des insights de gestion
<!--1357930-->
Certains [insights de gestion](/sccm/core/servers/manage/management-insights) permettent maintenant d’entreprendre des actions. En fonction de la règle, cette action montre l’un des comportements suivants :  

- Dans la console, accède automatiquement au nœud dans lequel vous pouvez entreprendre des actions. Par exemple, si les insights de gestion recommandent de changer un paramètre client, le fait d’entreprendre une action vous redirige vers le nœud Paramètres du client. Vous pouvez entreprendre d’autres actions en modifiant l’objet de paramètres clients par défaut ou personnalisé.  

- Accède à une vue filtrée selon une requête. Par exemple, le fait d’entreprendre une action avec la règle de regroupements vides montre simplement la liste des collections. De là, vous pouvez entreprendre d’autres actions, comme supprimer un regroupement ou modifier ses règles d’adhésion.  

Les règles d’insights de gestion suivantes sont associées à des actions de cette version :
- Sécurité
    - Versions de client logiciel anti-programme malveillant non prises en charge
- Centre logiciel
    - Utiliser la nouvelle version du Centre logiciel
- Applications
    - Applications sans déploiements
- Gestion simplifiée
    - Versions de client non-CB
- Regroupements
    - Regroupements vides 
- Services cloud
    - Mettre à jour les clients avec la dernière version de Windows 10



## <a name="transition-device-configuration-workload-to-intune-using-co-management"></a>Transférer la charge de travail de configuration des appareils vers Intune avec la cogestion
<!--1357903-->

Vous pouvez désormais transférer la charge de travail de configuration des appareils de Configuration Manager vers Intune après avoir activé la cogestion. Le transfert de cette charge de travail vous permet d’utiliser Intune pour déployer des stratégies MDM, tout en continuant à utiliser Configuration Manager pour déployer les applications. 

Pour basculer cette charge de travail, accédez à la page de propriétés de cogestion et déplacez le curseur actuellement sur Configuration Manager vers **Pilote** ou **Tout**. Pour plus d’informations, consultez [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview).

> [!Note]  
> Le fait de déplacer cette charge de travail déplace également les charges de travail **Accès aux ressources** et **Endpoint Protection**, qui constituent un sous-ensemble de la charge de travail de configuration des appareils.

Quand vous transférez cette charge de travail, vous pouvez encore déployer des paramètres Configuration Manager sur des appareils cogérés, même si Intune représente l’autorité de configuration des appareils. Cette exception peut être utilisée pour configurer les paramètres qui sont exigés par votre entreprise, mais qui ne sont pas encore disponibles dans Intune. Spécifiez cette exception sur une base de référence de configuration Configuration Manager. Activez l’option **Toujours appliquer cette base de référence, même aux clients cogérés** lors de la création de la base de référence, ou sous l’onglet **Général** des propriétés de la base de référence existante. 



## <a name="enable-distribution-points-to-use-network-congestion-control"></a>Configurer les points de distribution pour utiliser le contrôle de surcharge du réseau
<!--1358112-->

La fonctionnalité LEDBAT de Windows Server permet de gérer les transferts réseau d’arrière-plan. Pour les points de distribution qui exécutent des versions prises en charge de Windows Server, vous pouvez activer une option permettant d’ajuster le trafic réseau. Les clients utilisent uniquement la bande passante réseau lorsqu’elle est disponible. 

Pour plus d’informations sur la fonctionnalité LEDBAT de Windows, consultez le billet de blog [New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/).


### <a name="prerequisites"></a>Prérequis
- Un point de distribution sur Windows Server, version 1709  

- Il n’existe aucun prérequis concernant le client.<!--SCCMDocs issue 699-->  


### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Sélectionnez le nœud **Points de distribution**. Sélectionnez le point de distribution cible, puis cliquez sur **Propriétés** dans le ruban.  

2. Sous l’onglet **Général**, activez l’option **Ajuster la vitesse de téléchargement pour utiliser la bande passante non utilisée (Windows LEDBAT)** .  



## <a name="cloud-management-dashboard"></a>Tableau de bord de gestion cloud
<!--1358461-->
Le nouveau **tableau de bord de gestion cloud** fournit une vue centralisée de l’utilisation de la passerelle de gestion cloud. Lorsque le site est intégré à Azure AD, il affiche également les données sur les utilisateurs cloud et les appareils.  

La capture d’écran suivante montre une partie du tableau de bord de gestion cloud, comprenant deux des vignettes disponibles :  
![Vignettes du tableau de bord de gestion cloud : Trafic de la passerelle de gestion cloud et Clients actuellement en ligne](media/1358461-cmg-dashboard.png)

Cette fonctionnalité inclut également **l’analyseur de connexion de la passerelle de gestion cloud** pour la vérification en temps réel dans le cadre de la résolution des problèmes. L’utilitaire de la console vérifie l’état actuel du service, ainsi que le canal de communication qui passe par le point de connexion de la passerelle de gestion cloud vers les points de gestion qui autorisent le trafic de la passerelle.


### <a name="prerequisites"></a>Prérequis
- Une [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) active utilisée par les clients Internet  

- Intégrer le site aux [services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la gestion cloud  


### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

#### <a name="cloud-management-dashboard"></a>Tableau de bord de gestion cloud

Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**. Sélectionnez le nœud **Gestion cloud** et affichez les vignettes du tableau de bord.  

#### <a name="cmg-connection-analyzer"></a>Analyseur de connexion de la passerelle de gestion cloud

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Services cloud** et sélectionnez **Passerelle de gestion cloud**.  

2. Sélectionnez l’instance cible de la passerelle de gestion cloud, puis sélectionnez **Analyseur de connexion** dans le ruban.  

3. Dans la fenêtre Analyseur de connexion de la passerelle de gestion cloud, sélectionnez l’une des options suivantes pour l’authentification auprès du service :  

     1. **Utilisateur AD Azure** : cette option permet de simuler la communication comme avec une identité d’utilisateur cloud connectée à un appareil Windows 10 joint à Azure AD. Cliquez sur **Connexion** pour entrer les informations d’identification du compte d’utilisateur Azure AD de manière sécurisée.  

     2. **Certificat client** : cette option permet de simuler la communication comme avec un client Configuration Manager disposant d’un [certificat d’authentification client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_clientauth).  

4. Cliquez sur **Démarrer** pour démarrer l’analyse. Les résultats sont affichés dans la fenêtre de l’analyseur. Sélectionnez une entrée pour afficher plus de détails dans le champ Description.  



## <a name="cmpivot"></a>CMPivot
<!--1358456-->
Configuration Manager met à disposition un grand magasin de données d’appareils centralisé, que les clients utilisent pour générer des rapports. Toutefois, ces données peuvent être obsolètes. 

CMPivot est un nouvel utilitaire de console qui donne accès à l’état en temps réel des appareils de votre environnement. Il exécute immédiatement une requête sur tous les appareils actuellement connectés du regroupement cible, et retourne les résultats. Vous pouvez ensuite filtrer et regrouper ces données dans l’outil. En fournissant les données en temps réel des clients en ligne, vous pouvez répondre plus rapidement aux questions métier, résoudre les problèmes et corriger les incidents de sécurité.

Par exemple, si vous souhaitez [limiter les vulnérabilités d’exécution spéculative côté canal](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), l’une des exigences est de mettre à jour le BIOS système. Vous pouvez utiliser CMPivot pour interroger rapidement les informations du BIOS système et rechercher les clients non conformes. 

Dans cette capture d’écran, CMPivot affiche deux versions distinctes du BIOS avec chacune un appareil. Vous pouvez utiliser cet exemple de requête lorsque vous essayez CMPivot :  
`Registry('hklm:\\Hardware\\Description\\System\\BIOS') | where (Property == 'BIOSVersion') | summarize dcount( Device ) by Value`  

![Fenêtre CMPivot avec l’exemple de requête pour BIOSVersion](media/1358456-cmpivot-biosversion.png)

Vous pouvez cliquer sur le nombre d’appareils pour explorer les appareils. Lorsque vous affichez des appareils dans CMPivot, vous pouvez cliquer sur l’un d’eux, puis sélectionner les [actions de notification clientes](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode) suivantes :
- Exécuter un script
- Contrôle à distance
- Explorateur de ressources

Quand vous cliquez avec le bouton droit sur un appareil, vous pouvez également faire pivoter la vue de l’appareil pour afficher l’un des attributs suivants :
- Commandes de démarrage automatique
- Produits installés
- Processus
- Services
- Utilisateurs
- Connexions actives
- Mises à jour manquantes

### <a name="prerequisites"></a>Prérequis
- Les clients cibles doivent être mis à jour vers la dernière version.  

- L’administrateur Configuration Manager a besoin d’autorisations pour exécuter des scripts. Pour plus d’informations, consultez [Créer des rôles de sécurité pour les scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Actifs et conformité**, puis sélectionnez **Regroupements d’appareils**. Sélectionnez un regroupement cible, puis cliquez sur **Démarrer CMPivot** dans le ruban pour lancer l’outil.  

2. L’interface fournit davantage d’informations sur l’utilisation de l’outil. 
     - Vous pouvez entrer manuellement des chaînes de requête en haut de la page, ou cliquer sur les liens de la documentation intégrée.
     - Cliquez sur l’une des **Entités** pour l’ajouter à la chaîne de requête. 
     - Les liens concernant les **opérateurs de table**, les **fonctions d’agrégation** et les **fonctions scalaires** ouvrent une documentation de référence de langage dans le navigateur web. CMPivot utilise le même langage de requête que [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).



## <a name="improved-secure-client-communications"></a>Amélioration des communications clientes sécurisées
<!--1356889,1358228,1358460-->
L’utilisation de la communication HTTPS est recommandée pour tous les chemins de communication Configuration Manager, mais peut se révéler difficile pour certains clients en raison des frais liés à la gestion des certificats PKI. L’intégration à Azure Active Directory (Azure AD) permet d’éviter une partie de ces exigences de certificat. 

Cette version comprend des améliorations concernant la façon dont les clients communiquent avec les systèmes de site. Ces améliorations avaient deux principaux objectifs :  

- Sécuriser les communications clientes sans avoir besoin de certificats d’authentification serveur PKI  

- Permettre aux clients d’accéder de manière sécurisée au contenu des points de distribution sans avoir besoin d’un compte d’accès réseau  

> [!Note]  
> L’utilisation des certificats PKI est toujours possible pour les clients qui le souhaitent.  


### <a name="bkmk_token"></a> Scénarios
Les scénarios suivants bénéficient de ces améliorations :  

#### <a name="bkmk_token1"></a> Scénario 1 : Client vers point de gestion
<!--1356889-->
Les [appareils joints à Azure AD](/azure/active-directory/devices/concept-azure-ad-join) peuvent communiquer via une passerelle de gestion cloud avec un point de gestion configuré pour HTTP. Le serveur de site génère un certificat pour le point de gestion afin de lui permettre de communiquer via un canal sécurisé.   

> [!Note]  
> Ce comportement est différent de celui trouvé dans Configuration Manager Current Branch version 1802, qui nécessite un point de gestion HTTPS pour ce scénario. Pour plus d’informations, consultez [Activer le point de gestion pour HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

#### <a name="bkmk_token2"></a> Scénario 2 : Client vers point de distribution
<!--1358228-->
Un groupe de travail ou un client joint à Azure AD peut télécharger du contenu via un canal sécurisé à partir d’un point de distribution configuré pour HTTP.   

#### <a name="bkmk_token3"></a> Scénario 3 : Identité des appareils Azure AD 
<!--1358460-->
Un appareil joint à Azure AD ou un [appareil Azure AD hybride](/azure/active-directory/devices/concept-azure-ad-join-hybrid) peuvent communiquer de manière sécurisée avec leur site attribué, sans qu’un utilisateur Azure AD ne soit connecté. L’identité d’appareil cloud est désormais suffisante pour s’authentifier auprès du point de gestion et de la passerelle de gestion cloud.  


### <a name="prerequisites"></a>Prérequis  

- Un point de gestion configuré pour les connexions clientes HTTP. Définissez cette option sous l’onglet **Général** des propriétés du rôle de système de site.  

- Un point de distribution configuré pour les connexions clientes HTTP. Définissez cette option sous l’onglet **Général** des propriétés du rôle de système de site. N’activez pas l’option **Autoriser les clients à se connecter anonymement**.  

- Une passerelle de gestion cloud  

- Intégrer le site à Azure AD pour la gestion cloud  

    - Si vous avez déjà effectué cette intégration pour votre site, vous devez mettre à jour l’application Azure AD. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Locataires Azure Active Directory**. Sélectionnez le locataire Azure AD, sélectionnez l’application web dans le volet **Applications**, puis cliquez sur **Mettre à jour les paramètres d’application** dans le ruban.  

- Un client exécutant Windows 10 version 1803 et joint à Azure AD (cette exigence concerne seulement le [scénario 3](#bkmk_token3)). 


### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**. Sélectionnez le site, puis cliquez sur **Propriétés** dans le ruban.  

2. Passez à l’onglet **Communication de l’ordinateur client**. Sélectionnez l’option **HTTPS ou HTTP**, puis activez la nouvelle option **Use Configuration Manager-generated certificates for HTTP site systems** (Utiliser des certificats générés par Configuration Manager pour les systèmes de site HTTP).  

Consultez l’ancienne [liste des scénarios](#bkmk_token) pour valider.

> [!Tip]
> Dans cette version, un délai maximal de 30 minutes est nécessaire pour que le point de gestion reçoive puis configure le nouveau certificat du site.

Vous pouvez voir ces certificats dans la console Configuration Manager. Accédez à l’espace de travail **Administration**, développez **Sécurité**, puis sélectionnez le nœud **Certificats**. Recherchez le certificat racine **Émission de SMS**, ainsi que les certificats de rôle serveur de site émis par ce certificat racine.


### <a name="known-issues"></a>Problèmes connus
- L’utilisateur ne voit pas les applications disponibles dans le Centre logiciel.  

- Les scénarios de déploiement de système d’exploitation nécessitent toujours un compte d’accès réseau.  

- Le fait d’activer puis de désactiver rapidement et à plusieurs reprises l’option **Use Configuration Manager-generated certificates for HTTP site systems** (Utiliser des certificats générés par Configuration Manager pour les systèmes de site HTTP) peut empêcher la liaison du certificat aux rôles de système de site. Aucun certificat émis par le certificat Émission de SMS n’est lié à un site web dans Windows Server Internet Information Services (IIS). Pour contourner ce problème, supprimez tous les certificats émis par le certificat Émission de SMS dans le magasin de certificats **SMS** de Windows, puis redémarrez le service smsexec.



## <a name="improvements-for-enabling-third-party-software-update-support"></a>Améliorations concernant la prise en charge des mises à jour des logiciels tiers
<!--1357605-->
Nous avons pris en compte vos commentaires UserVoice concernant la [prise en charge des mises à jour des logiciels tiers](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co) et avons amélioré l’intégration à l’éditeur de mise à jour System Center (SCUP ). Configuration Manager Technical Preview [version 1803](/sccm/core/get-started/capabilities-in-technical-preview-1803#enable-third-party-software-update-support-on-clients) permet désormais de lire le certificat à partir de WSUS pour les mises à jour tierces, puis de déployer ce certificat sur des clients. Toutefois, vous devez encore utiliser l’outil SCUP pour créer et gérer le certificat pour la signature des mises à jour de logiciels tiers.

Dans cette version, vous pouvez paramétrer le site Configuration Manager pour qu’il configure automatiquement le certificat. Le site communique avec WSUS pour générer un certificat à cet effet. Configuration Manager continue alors à déployer ce certificat sur les clients. Cette nouvelle fonctionnalité évite d’avoir à utiliser l’outil SCUP pour créer et gérer le certificat. 

Pour plus d’informations sur l’utilisation générale de l’outil SCUP, consultez [Éditeur de mise à jour System Center](/sccm/sum/tools/updates-publisher).

### <a name="prerequisites"></a>Prérequis
- Activez puis déployez le paramètre client **Activer les mises à jour de logiciels tiers** dans le groupe **Mises à jour logicielles**.
- Si WSUS se trouve sur un serveur autre que celui du point de mise à jour logicielle, vous devez effectuer l’une des actions suivantes sur le serveur WSUS distant :
    - Activez le service d’accès à distance au Registre dans Windows  
    ou
    - Dans la clé de Registre `HKLM\Software\Microsoft\Update Services\Server\Setup`, créez un DWORD nommé **EnableSelfSignedCertificates** avec la valeur `1`. 

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site** et sélectionnez **Sites**. Sélectionnez le site de niveau supérieur, cliquez sur **Configurer les composants de site** dans le ruban, puis sélectionnez **Point de mise à jour logicielle**.  

2. Passez l’onglet **Mises à jour tierces**. Sélectionnez l’option **Activer les mises à jour de logiciels tiers**, puis sélectionnez l’option **Configuration Manager automatically manages the certificate** (Configuration Manager gère automatiquement le certificat).

3. Suivez le flux de travail SCUP typique pour importer un catalogue de mise à jour de logiciels tiers, puis déployez les mises à jour sur les clients.



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10
<!--1358500-->

Le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend un nouveau groupe, ainsi que des actions qu’il est recommandé d’ajouter en cas d’échec de la mise à niveau. Ces actions facilitent la résolution des problèmes.

### <a name="new-groups-under-run-actions-on-failure"></a>Groupes de nouveau disponibles sous **Exécuter des actions en cas d’échec**
- **Collecter les journaux** : pour collecter les journaux du client, ajoutez des étapes dans ce groupe. 
    - L’une des pratiques courantes consiste à copier les fichiers journaux sur un partage réseau. Pour établir cette connexion, utilisez l’étape [Se connecter à un dossier réseau](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder). 
    - Pour effectuer la copie, utilisez un script personnalisé ou un utilitaire en suivant l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [Exécuter le script PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).
    - Les fichiers à collecter peuvent inclure les journaux suivants :  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  
    - Pour plus d’informations sur setupact.log et sur les autres journaux d’installation de Windows, consultez [Journaux d’installation de Windows](/windows/deployment/upgrade/log-files).
    - Pour plus d’informations sur les journaux du client Configuration Manager, consultez [Journaux du client Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
    - Pour plus d’informations sur _SMSTSLogPath et sur d’autres variables utiles, consultez [Variables intégrées de séquence de tâches](/sccm/osd/understand/task-sequence-built-in-variables).

- **Exécuter des outils de diagnostic** : pour exécuter d’autres outils de diagnostic, ajoutez des étapes dans ce groupe. Ces outils doivent être automatisés pour collecter des informations supplémentaires à partir du système, dès que possible après un échec.
    - Un exemple est l’outil Windows [SetupDiag](/windows/deployment/upgrade/setupdiag). Il s’agit d’un outil de diagnostic autonome que vous pouvez utiliser pour obtenir des informations détaillées sur la raison de l’échec d’une mise à niveau Windows 10.
         - Dans Configuration Manager, [créez un package](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) pour l’outil.
         - Ajoutez l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) au groupe de votre séquence de tâches. Utilisez l’option **Package** pour référencer l’outil. La chaîne suivante est un exemple de **ligne de commande** :  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`



## <a name="cmtrace-installed-with-client"></a>CMTrace installé avec le client
<!--1357971-->

Désormais, l’outil d’affichage des journaux CMTrace est automatiquement installé avec le client Configuration Manager. Il est ajouté au répertoire d’installation du client, qui est par défaut `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace *n’est pas* automatiquement inscrit auprès de Windows pour ouvrir l’extension de fichier .log.



## <a name="improvement-to-the-configuration-manager-console"></a>Améliorations apportées à la console Configuration Manager
<!--1358202-->
Nous avons apporté les améliorations suivantes à la console Configuration Manager :

- Les listes d’appareils sous Ressources et conformité, Appareils, affichent désormais l’utilisateur actuellement connecté. Cette valeur est synchronisée avec [l’état du client](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). Elle est supprimée lorsque l’utilisateur se déconnecte. Si aucun utilisateur n’est connecté, la valeur est vide. 

### <a name="known-issues"></a>Problèmes connus
La valeur de l’utilisateur actuellement connecté est vide dans le nœud Appareils ou lorsque vous affichez une liste d’appareils sous le nœud Regroupements d’appareils. Pour contourner ce problème, téléchargez ce [script SQL](https://gallery.technet.microsoft.com/ConfigMgr-1805-BgbUpdateLiv-306ff46c). Exécutez sp_BgbUpdateLiveData.sql sur le serveur de bases de données de site, puis redémarrez les services smsexec et sms_notification_server sur le point de gestion.<!--514471-->



## <a name="improvements-to-console-feedback"></a>Améliorations apportées à la fonctionnalité Commentaires de la console
<!--1357542-->
Dans cette version, les améliorations suivantes ont été apportées à la fonctionnalité [Commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) de la console Configuration Manager :  

- Désormais, la boîte de dialogue Commentaires mémorise vos paramètres précédents, tels que les options sélectionnées et votre adresse de messagerie.  

- Les commentaires hors connexion sont maintenant pris en charge. Enregistrez vos commentaires dans la console, puis chargez-les vers Microsoft à partir d’un système connecté à Internet. Utilisez le nouvel outil de chargement des commentaires hors connexion qui se trouve ici : `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. Pour afficher les options de ligne de commande disponibles et nécessaires, exécutez l’outil avec l’option `--help`. Le système connecté a besoin d’accéder à **petrol.office.microsoft.com**.

### <a name="known-issues"></a>Problèmes connus
Lorsque vous utilisez la commande **Envoyer un sourire** ou **Envoyer un smiley mécontent** dans la console sur un ordinateur connecté à Internet, il peut arriver que le message suivant s’affiche : « Erreur lors de l'envoi des commentaires ». Si vous cliquez sur **Plus de détails**, le texte suivant apparaît : `{"Message":""}`. Cette erreur est due à un problème connu au niveau de la réponse provenant du système de commentaires back-end. Vous pouvez ignorer cette erreur. Microsoft a bien reçu vos commentaires. (Si les détails affichent un autre message, utilisez l’option de commentaires hors connexion pour réessayer d’envoyer vos commentaires à une date ultérieure.)



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Améliorations apportées aux points de distribution compatibles PXE
<!--1357580-->

Cette version comprend les améliorations suivantes lorsque vous utilisez l’option [**Activer un répondeur PXE sans service de déploiement Windows**](/sccm/core/get-started/capabilities-in-technical-preview-1802#improvements-to-pxe-enabled-distribution-points) sur un point de distribution :  

- Les règles du Pare-feu Windows sont automatiquement créées sur le point de distribution quand vous activez cette option.  
- Améliorations apportées à la journalisation des composants



## <a name="improvement-to-hardware-inventory-for-large-integer-values"></a>Amélioration apportées à l’inventaire matériel pour les valeurs d’entiers longs
<!--1357880-->
La version actuelle de l’inventaire matériel est limitée aux entiers supérieurs à 4 294 967 296 (2^32). Cette limite peut être atteinte pour les attributs, tels que les tailles de disque dur en octets. Le point de gestion ne traite pas les valeurs d’entiers supérieures à cette limite. De fait, aucune valeur n’est stockée dans la base de données. La nouvelle version prend désormais en charge les entiers de longueur 18 446 744 073 709 551 616 (2^64). 

Pour les propriétés dont la valeur ne change pas, comme la taille totale du disque, vous pouvez ne pas voir immédiatement la valeur après la mise à niveau du site. La plupart des inventaires matériels se présentent sous la forme d’un état d’écart. Le client envoie uniquement les valeurs qui changent. Pour contourner ce comportement, ajoutez une autre propriété à la même classe. Avec cette action, le client met à jour toutes les propriétés de la classe qui ont changé. 



## <a name="improvement-to-wsus-maintenance"></a>Améliorations apportées à la maintenance de WSUS
<!--1357898-->

L’Assistant de nettoyage WSUS refuse désormais les mises à jour qui ont expiré ou qui ont été remplacées selon les règles de remplacement. Ces règles sont définies dans les propriétés de composant du point de mise à jour logicielle.

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site** et sélectionnez **Sites**. Sélectionnez le site de niveau supérieur, cliquez sur **Configurer les composants de site** dans le ruban, puis sélectionnez **Point de mise à jour logicielle**.  

2. Passez à l’onglet **Règles de remplacement**. Activez l’option **Exécutez l’Assistant de nettoyage WSUS**. Spécifiez le comportement de remplacement souhaité.  

3. Examinez le fichier WSyncMgr.log.



## <a name="improvement-to-support-for-cng-certificates"></a>Améliorations apportées à la prise en charge des certificats CNG
<!--1357314-->
À compter de cette version, utilisez les [certificats CNG](/sccm/core/plan-design/network/cng-certificates-overview) pour les rôles serveurs HTTPS suivants :  
- Point d’enregistrement de certificat, y compris le serveur NDES avec le module de stratégie Configuration Manager



## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
