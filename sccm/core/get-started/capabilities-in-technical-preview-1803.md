---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités disponibles dans Configuration Manager Technical Preview version 1803.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8f03013a7f040d9c0dacac3ac8d94bcaa37dd62
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677271"
---
# <a name="capabilities-in-technical-preview-1803-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1803 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans Technical Preview version 1803 pour Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités au site de votre préversion technique. 

Consultez l’article [Technical Preview](/sccm/core/get-started/technical-preview) avant d’installer cette mise à jour. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Prise en charge des points de distribution cloud comme source par les points de distribution d’extraction  
<!--1321554-->
De nombreux clients utilisent des [points de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point) dans des bureaux distants ou des filiales pour télécharger du contenu à partir d’un point de distribution source sur le réseau WAN. Si vos bureaux distants ont une meilleure connexion à Internet, ou pour réduire la charge sur vos liaisons WAN, vous pouvez désormais utiliser un [point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) dans Microsoft Azure comme source. Quand vous ajoutez une source sous l’onglet **Point de distribution d’extraction** des propriétés de point de distribution, tout point de distribution cloud du site est maintenant répertorié comme point de distribution disponible. Le comportement des deux rôles système de site reste inchangé par ailleurs. 

### <a name="prerequisites"></a>Prérequis
- Le point de distribution d’extraction a besoin d’un accès Internet pour communiquer avec Microsoft Azure.
- Le contenu doit être distribué au point de distribution cloud source.

> [!Note]  
> Cette fonctionnalité implique des frais sur votre abonnement Azure pour le stockage de données et la sortie de réseau. Pour plus d’informations, consultez le [Coût d’utilisation d’une distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Prise en charge du téléchargement partiel dans le cache d’homologue client pour réduire l’utilisation du réseau WAN
<!--1357346-->
Les sources de cache d’homologue client peuvent désormais diviser le contenu en plusieurs parties. Ces parties diminuent le transfert de réseau afin de réduire l’utilisation du réseau WAN. Le point de gestion fournit un suivi plus détaillé des parties du contenu. Il essaie de supprimer plusieurs téléchargements du même contenu par groupe de limites. 

### <a name="example-scenario"></a>Exemple de scénario
Contoso a un seul site principal avec deux groupes de limites : Un siège social et une filiale. Il existe une relation de repli de 30 minutes entre les groupes de limites. Le point de gestion et le point de distribution du site se trouvent uniquement dans la limite du siège social. L’emplacement de la filiale n’a aucun point de distribution local. Deux des quatre clients au niveau de la filiale sont configurés comme sources de cache d’homologue. 

![Schéma de la configuration réseau comme décrite pour l’exemple de scénario](media/1357346-peer-cache-source-parts.png)

1. Vous ciblez un déploiement avec du contenu sur les quatre clients de la filiale. Vous avez distribué du contenu uniquement au point de distribution.
2. Client3 et Client4 n’ont pas de source locale pour le déploiement. Le point de gestion indique aux clients de patienter 30 minutes avant de revenir au groupe de limites distantes.
3. Client1 (PCS1) est la première source de cache d’homologue pour actualiser la stratégie avec le point de gestion. Étant donné que ce client est activé comme source de cache d’homologue, le point de gestion lui indique de commencer immédiatement le téléchargement de la partie A à partir du point de distribution.  
4. Quand Client2 (PCS2) contacte le point de gestion, comme la partie A est déjà en cours mais pas encore terminée, le point de gestion lui indique de commencer immédiatement le téléchargement de la partie B à partir du point de distribution.
5. PCS1 termine le téléchargement de la partie A et en avertit immédiatement le point de gestion. Comme la partie B est déjà en cours mais pas encore terminée, le point de gestion lui indique de commencer le téléchargement de la partie C à partir du point de distribution.
6. PCS2 termine le téléchargement de la partie B et en avertit immédiatement le point de gestion. Le point de gestion lui indique de commencer le téléchargement de la partie D à partir du point de distribution. 
7. PCS1 termine le téléchargement de la partie C et en avertit immédiatement le point de gestion. Le point de gestion l’informe qu’aucune autre partie n’est disponible à partir du point de distribution distant. Le point de gestion lui indique de télécharger la partie B à partir de son homologue local, PCS2.
8. Ce processus se poursuit jusqu’à ce que les deux sources de cache d’homologue client aient toutes les parties de l’une et de l’autre. Le point de gestion établit la priorité des parties à partir du point de distribution distant avant d’indiquer aux sources de cache d’homologue de télécharger des parties à partir des homologues locaux. 
9. Client3 est le premier à actualiser la stratégie au terme de la période de repli de 30 minutes. Il vérifie de nouveau auprès du point de gestion, qui indique au client des nouvelles sources locales. Au lieu de télécharger le contenu en totalité à partir du point de distribution sur le réseau WAN, il télécharge le contenu en totalité à partir de l’une des sources de cache d’homologue client. Les clients établissent la priorité des sources d’homologue local. 

> [!Note]  
> Si le nombre de sources de cache d’homologue client est supérieur au nombre de parties du contenu, le point de gestion indique aux sources de cache d’homologue supplémentaires d’attendre une action de repli comme un client normal. 


### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Configurez normalement des [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups) et des [sources de cache d’homologue](/sccm/core/plan-design/hierarchy/client-peer-cache).
2. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**. Cliquez sur **Paramètres de hiérarchie** dans le ruban. 
3. Sous l’onglet **Général**, activez l’option permettant de **configurer les sources de cache d’homologue client pour diviser du contenu en parties**. 
4. Créez un déploiement obligatoire avec du contenu.  

   > [!Note]  
   > Cette fonctionnalité fonctionne uniquement quand le client télécharge le contenu en arrière-plan, comme avec un déploiement obligatoire. Les téléchargements à la demande, comme quand l’utilisateur installe un déploiement disponible dans le Centre logiciel, se comportent comme d’habitude.  

1. Pour les voir gérer le téléchargement du contenu en parties, examinez le fichier **ContentTransferManager.log** sur la source de cache d’homologue client et le fichier **MP_Location.log** sur le point de gestion.  
 



## <a name="maintenance-windows-in-software-center"></a>Fenêtres de maintenance dans le Centre logiciel
<!--1358131-->
Le Centre logiciel affiche maintenant la fenêtre de maintenance planifiée suivante. Sous l’onglet État de l’installation, passez de la vue Tous à la vue À venir. Elle affiche la période et la liste des déploiements qui sont planifiés. La liste est vide s’il n’existe aucune fenêtre de maintenance future. 

![Le Centre logiciel affichant la liste des déploiements à venir sous l’onglet État de l’installation](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Onglet personnalisé pour une page web du Centre logiciel
<!--1358132-->
Vous pouvez maintenant créer un onglet personnalisé pour ouvrir une page web dans le Centre logiciel. Cette fonctionnalité vous permet d’afficher du contenu à vos utilisateurs finaux d’une façon cohérente et fiable. La liste suivante comprend quelques exemples :
- Contacter le service informatique : informations sur la façon de contacter le service informatique de votre organisation
- Centre de support informatique : Actions informatiques en libre-service telles que la recherche dans une base de connaissances ou l’ouverture d’un ticket de support.
- Documentation pour les utilisateurs finaux : articles destinés aux utilisateurs de votre organisation sur différents sujets informatiques comme l’utilisation d’applications ou la mise à niveau vers Windows 10.


### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Dans la console Configuration Manager, sur le nœud **Paramètres clients** de l’espace de travail **Administration**, ouvrez la stratégie **Paramètres client par défaut**.
2. Sélectionnez le groupe **Centre logiciel**.
3. Pour **Paramètres du Centre logiciel**, cliquez sur **Personnaliser**.
4. Passez à l’onglet **Onglets**.
5. Activez l’option permettant de **spécifier un onglet personnalisé pour le Centre logiciel**.
    1. Entrez un nom dans le champ de texte **Nom de l’onglet**. C’est le nom que voit l’utilisateur dans le Centre logiciel.
    2. Entrez une URL valide dans le champ de texte**URL du contenu**. Cette URL est le contenu que le Centre logiciel affiche quand les utilisateurs cliquent sur cet onglet.

> [!Tip]  
> Le Centre logiciel utilise des composants Internet Explorer pour le rendu de la page web.

## <a name="enable-third-party-software-update-support-on-clients"></a>Activer la prise en charge des mises à jour de logiciels tiers sur des clients

Vous pouvez maintenant activer la configuration des clients Configuration Manager pour les mises à jour de logiciels tiers. Quand vous **activez les mises à jour de logiciels tiers** pour les propriétés du composant de point de mise à jour logicielle, le point de mise à jour logicielle télécharge le certificat de signature utilisé par WSUS pour les mises à jour tierces. <!--1357605-->

Le fait de sélectionner l’option **Activer les mises à jour de logiciels tiers** dans les paramètres clients effectue les opérations suivantes : 
- Sur le client, cela définit la stratégie pour « Autoriser les mises à jour signées provenant d’un emplacement intranet du service de mise à jour Microsoft ». 
- Cela installe le certificat de signature dans la banque d’éditeurs approuvés sur le client. 

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Sur le site le plus haut dans la hiérarchie Configuration Manager, accédez au nœud **Administration**, développez **Configuration du site**, puis **Sites**.
2. Cliquez avec le bouton droit sur votre serveur de site le plus en haut et sélectionnez **Configurer les composants de site**, puis **Point de mise à jour logicielle**.
3. Cliquez sur l’onglet **Mises à jour tierces**, puis cochez **Activer les mises à jour de logiciels tiers**.
4. Ouvrez **Paramètres client**, puis accédez aux paramètres de **Mises à jour logicielles**.
5. Vérifiez que l’option **Activer les mises à jour de logiciels tiers** a la valeur **Oui**.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Activer le copier/coller des détails de composants à partir d’affichages d’analyse
Suite à vos [commentaires User Voice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det), vous pouvez maintenant activer la fonctionnalité copier/coller dans le volet des détails de composants dans les affichages d’analyse de l’état du déploiement et de la distribution.  <!--1357552-->

## <a name="scap-extensions"></a>Extensions SCAP
La préversion des Extensions SCAP est disponible dans le dossier Cd.latest sous SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. Cette préversion des Extensions SCAP peut être installée sur toutes les versions actuellement prises en charge de Configuration Manager Current Branch et LTSB 1606. Pour plus d’informations, consultez [À propos des Extensions SCAP (Security Content Automation Protocol)](/sccm/compliance/plan-design/scap/about-scap).



## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
