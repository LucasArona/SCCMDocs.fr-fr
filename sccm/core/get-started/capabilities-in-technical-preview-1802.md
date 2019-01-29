---
title: Technical Preview 1802 | Microsoft Docs
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1802 de System Center Configuration Manager.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 7ff02203efac1802db166fef4a1c5a65d1b72615
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898526"
---
# <a name="capabilities-in-technical-preview-1802-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1802 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*

Cet article présente les fonctionnalités disponibles dans la version Technical Preview 1802 de System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. 

Consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview) avant d’installer cette version Technical Preview. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->
## <a name="known-issues-in-this-technical-preview"></a>Problèmes connus dans cette préversion technique
- **La mise à jour vers une nouvelle préversion échoue s’il existe un serveur de site en mode passif**. Si vous avez un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez désinstaller le serveur de site en mode passif avant de procéder à la mise à jour vers cette nouvelle préversion. Vous pouvez réinstaller le serveur de site en mode passif une fois votre site mis à jour.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.
  <!--sms 489412-->


</br>

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  


## <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Transférer la charge de travail Endpoint Protection vers Intune à l’aide de la cogestion    
<!-- 1357365 --> Dans cette version, vous pouvez maintenant transférer la charge de travail Endpoint Protection de Configuration Manager à Intune après avoir activé la cogestion. Pour cela, accédez à la page des propriétés de cogestion et déplacez le curseur de Configuration Manager sur **Pilote** ou **Tout**. Pour plus d’informations, consultez [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview).


 
## <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurer l’Optimisation de la distribution de Windows de façon à utiliser des groupes de limites Configuration Manager
<!-- 1324696 --> Les groupes de limites Configuration Manager permettent de définir et de réguler la distribution de contenu sur le réseau de l’entreprise et dans les agences. [L’Optimisation de la distribution de Windows](/windows/deployment/update/waas-delivery-optimization) est une technologie cloud pair à pair de partage de contenu entre appareils Windows 10. À partir de cette version, vous pourrez la configurer de façon à ce qu’elle utilise vos groupes de limites pour partager du contenu entre pairs. Un nouveau paramètre client s’applique à l’identificateur de groupe de limites sous la forme de l’identificateur de groupe d’Optimisation de la distribution sur le client. Lorsque le client communique avec le service de cloud d’Optimisation de la distribution, il utilise cet identificateur pour localiser les pairs possédant le contenu souhaité. 

### <a name="prerequisites"></a>Prérequis
- L’Optimisation de la distribution n’est disponible que sur les clients Windows 10

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Dans la console de Configuration Manager, créez une stratégie personnalisée de paramètres d’appareils clients sur le nœud **Paramètres clients** de l’espace de travail **Administration**.
2. Sélectionnez le nouveau groupe **Optimisation de la distribution**.
3. Activez le paramètre **Utiliser les groupes de limites Configuration Manager pour l’ID de groupe d’Optimisation de la distribution**.

Pour plus d’informations, consultez l’option **Groupe** du mode de distribution dans [Options d’Optimisation de la distribution](/windows/deployment/update/waas-delivery-optimization#group-id).



## <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Séquence de tâches de mise à niveau sur place de Windows 10 via la Passerelle de gestion cloud
<!-- 1357149 -->

La [séquence de tâches de mise à niveau sur place](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) de Windows 10 prend maintenant en charge le déploiement vers des clients basés sur Internet et gérés par le biais de la [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Cette capacité permet aux utilisateurs distants de passer plus facilement à Windows 10, sans avoir à se connecter au réseau d’entreprise. 

Veillez à ce que tout le contenu référencé par la séquence de tâches de mise à niveau sur place soit distribué sur un [point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Sinon, les appareils ne pourront pas exécuter la séquence de tâches.

Lorsque vous déployez une séquence de tâches de mise à niveau, utilisez les paramètres suivants :
- **Autoriser la séquence de tâches à s’exécuter pour le client sur Internet**, sous l’onglet Expérience utilisateur du déploiement.
- **Télécharger tout le contenu localement avant de démarrer la séquence de tâches**, sur la page Points de distribution du déploiement. Les autres options, comme **Télécharger le contenu localement si nécessaire pour la séquence de tâches en cours d’exécution**, ne fonctionnent pas dans ce scénario. Le moteur de séquence de tâches est actuellement incapable de récupérer du contenu à partir d’un point de distribution cloud. Le client Configuration Manager doit télécharger le contenu à partir du point de distribution cloud avant de démarrer la séquence de tâches.
- (*Facultatif*) **Prétélécharger le contenu pour cette séquence de tâches**, sous l’onglet Général du déploiement. Pour plus d’informations, consultez la section [Configurer le contenu précache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).



## <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10
<!-- 1357425 --> Le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend maintenant des groupes supplémentaires, avec des actions recommandées à ajouter avant ou après le processus de mise à niveau. Ces actions sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils sur Windows 10. 

### <a name="new-groups-under-prepare-for-upgrade"></a>Nouveaux groupes sous **Préparer la mise à niveau**
- **Vérifications de la batterie** : Ajoutez des étapes dans ce groupe pour vérifier si l'ordinateur utilise la batterie ou l'alimentation secteur. Cette action doit être effectuée par un utilitaire ou un script personnalisé.
- **Vérifications de la connexion réseau/câblée** : Ajoutez des étapes dans ce groupe pour vérifier si l'ordinateur est connecté à un réseau et n'utilise pas de connexion sans fil. Cette action doit être effectuée par un utilitaire ou un script personnalisé.
- **Supprimer les applications incompatibles** : Ajoutez des étapes dans ce groupe pour supprimer les applications incompatibles avec cette version de Windows 10. Il existe différentes façons de désinstaller une application selon les cas. Si l’application utilise Windows Installer, copiez la ligne de commande **Programme de désinstallation** de l’onglet **Programmes** dans les propriétés de type de déploiement de Windows Installer de l’application. Ensuite, ajoutez dans ce groupe une étape **Exécuter la ligne de commande** comportant la ligne de commande du programme de désinstallation. Par exemple : </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Supprimer les pilotes incompatibles** : Ajoutez des étapes dans ce groupe pour supprimer les pilotes incompatibles avec cette version de Windows 10.
- **Supprimer/suspendre la sécurité tierce** : Ajoutez des étapes dans ce groupe pour supprimer ou suspendre les programmes de sécurité tiers, comme les antivirus.
   - Si vous utilisez un programme de chiffrement de disque tiers, indiquez son pilote de chiffrement à l’installation de Windows avec [l’option de ligne de commande](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Ajoutez une étape [Définir une variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) à la séquence de tâches dans ce groupe. Affectez la valeur **OSDSetupAdditionalUpgradeOptions** à la variable de séquence de tâches. Définissez la valeur **/ReflectDriver** avec le chemin d’accès au pilote. Cette [variable d’action de séquence de tâches](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) ajoute la ligne de commande d’installation de Windows utilisée par la séquence de tâches. Contactez votre éditeur de logiciels pour obtenir de l’aide sur ce processus.

### <a name="new-groups-under-post-processing"></a>Nouveaux groupes sous **Post-traitement**
- **Appliquer des pilotes basés sur l'installation** : Ajoutez des étapes dans ce groupe pour installer des pilotes basés sur l'installation (.exe) à partir de packages.
- **Installer/activer une sécurité tierce** : Ajoutez des étapes dans ce groupe pour installer ou activer des programmes de sécurité tiers, comme des antivirus. 
- **Définir les applications Windows par défaut et les associations** : Ajoutez des étapes dans ce groupe pour définir les applications Windows par défaut et les associations de fichiers. Tout d’abord, préparez un ordinateur de référence avec les associations d’applications de votre choix. Ensuite, exécutez la commande suivante pour exporter : </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Ajoutez le fichier XML à un package. Ensuite, ajoutez une étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) dans ce groupe. Indiquez le package contenant le fichier XML, puis spécifiez la ligne de commande suivante : </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Pour plus d’informations, consultez la page [Exporter ou importer des associations d’applications par défaut](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Appliquer les personnalisations** : Ajoutez des étapes dans ce groupe pour appliquer les personnalisations du menu Démarrer, comme l'organisation de groupes de programmes. Pour plus d’informations, consultez la section [Personnaliser l’écran de démarrage](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### <a name="additional-recommendations"></a>Recommandations supplémentaires
- Consultez la documentation Windows pour [Résoudre les erreurs de mise à niveau de Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Cet article comporte également des informations détaillées sur le processus de mise à niveau.
- À l’étape **Vérifier la préparation** par défaut, activez **Garantir un espace disque libre minimal (Mo)**. Choisissez une valeur au moins égale à **16384** (16 Go) pour un package de mise à niveau d’un système d'exploitation 32 bits, ou à **20480** (20 Go) pour 64 bits. 
- Utilisez la [variable de séquence de tâches intégrée](/sccm/osd/understand/task-sequence-built-in-variables) **SMSTSDownloadRetryCount** pour réessayer de télécharger la stratégie. Actuellement, le client retente deux fois par défaut ; cette variable est définie sur deux (2). Si vos clients ne sont pas connectés à un réseau d’entreprise câblé, les tentatives supplémentaires les aideront à récupérer la stratégie. Cette variable n’a aucun effet secondaire, en dehors du fait qu’elle retarde l’échec si elle ne parvient pas à télécharger la stratégie.<!-- 501016 --> Augmentez également la variable **SMSTSDownloadRetryDelay** (valeur par défaut : 15 secondes).
- Effectuez une évaluation de compatibilité inline. 
   - Ajoutez une deuxième étape **Mettre à niveau le système d’exploitation** au début du groupe **Préparer la mise à niveau**. Nommez-la *Mettre à niveau l’évaluation*. Spécifiez le même package de mise à niveau, puis activez l’option **Effectuer l’analyse de compatibilité de l’installation de Windows sans démarrer la mise à niveau**. Activez **Continuer en cas d’erreur** dans l’onglet Options. 
   - Juste après cette étape *Mettre à niveau l’évaluation*, ajoutez une étape **Exécuter la ligne de commande**. Spécifiez la ligne de commande suivante :</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Dans l'onglet **Options**, ajoutez la condition suivante : </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Ce code de retour est l’équivalent décimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), qui correspond à la réussite d’une analyse de compatibilité sans problème. Si l’étape *Mettre à niveau l’évaluation* réussit et retourne ce code, cette étape est ignorée. En revanche, si l’étape d’évaluation retourne un autre code de retour, cette étape échoue à effectuer la séquence de tâches avec le code de retour issu de l’analyse de compatibilité de l’installation de Windows.
   - Pour plus d’informations, consultez la section [Mettre à niveau le système d’exploitation](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Si vous souhaitez faire passer l’appareil du BIOS au standard UEFI au cours de cette séquence de tâches, consultez la section [Passer du BIOS au standard UEFI pendant une mise à niveau sur place](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Envoyer vos **Commentaires** dans l’onglet **Accueil** du ruban si vous avez d’autres recommandations ou suggestions.



## <a name="improvements-to-pxe-enabled-distribution-points"></a>Améliorations apportées aux points de distribution compatibles PXE
<!-- 1357580 --> Pour préciser le comportement de la [nouvelle fonctionnalité PXE](/sccm/core/get-started/capabilities-in-technical-preview-1706#pxe-network-boot-support-for-ipv6) introduite dans la préversion technique 1706, nous avons renommé l’option **Prise en charge IPv6**. Sur l’onglet **PXE** des propriétés des points de distribution, cochez **Activer un répondeur PXE sans les Services de déploiement Windows**. 

Cette option active un répondeur PXE sur le point de distribution, qui n’a pas besoin des Services de déploiement Windows (WDS). Si vous activez cette nouvelle option sur un point de distribution qui est déjà compatible PXE, Configuration Manager suspend les services WDS. Si vous la désactivez tout en choisissant **d’Activer la prise en charge PXE pour les clients**, le point de distribution réactive les services WDS.

Les services WDS n’étant pas obligatoires, le point de distribution compatible PXE peut être un système d’exploitation client ou serveur, y compris Windows Server Core. Ce nouveau service de répondeur PXE continue à prendre en charge IPv6, et améliore également la flexibilité des points de distribution compatibles PXE dans les agences.

> [!NOTE]
> Ce service utilise la même technologie fondamentale sur le [service de répondeur PXE client](/sccm/core/get-started/capabilities-in-technical-preview-1712#client-based-pxe-responder-service) dans la version Technical Preview 1712. Cette fonctionnalité n’implique pas le traitement du rôle de point de distribution.

### <a name="multicast"></a>Multidiffusion
Pour pouvoir activer et configurer la multidiffusion sur l’onglet **Multidiffusion** des propriétés du point de la distribution, il faut que ce dernier utilise les services WDS. 
- Si vous choisissez **d’Activer la prise en charge de PXE pour les clients** et **d’Activer la multidiffusion pour envoyer des données simultanément à plusieurs clients**, vous ne pourrez pas **Activer un répondeur PXE sans les Services de déploiement Windows**.
- Si vous choisissez **d’Activer la prise en charge PXE pour les clients** et **d’Activer un répondeur PXE sans les Services de déploiement Windows**, vous ne pourrez pas **Activer la multidiffusion pour envoyer des données simultanément à plusieurs clients**.



## <a name="deployment-templates-for-task-sequences"></a>Modèles de déploiement pour les séquences de tâches
<!-- 1357391 --> L’assistant de déploiement de séquences de tâches peut maintenant créer un modèle de déploiement. Celui-ci peut être enregistré et appliqué à une séquence de tâches existante ou nouvelle pour créer un déploiement. 

### <a name="try-it-out"></a>Essayez !  
Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné. 

 **Créer un modèle de déploiement pour un nouveau déploiement de séquence de tâches** <br/> 
1. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.
2. Cliquez avec le bouton droit sur une séquence de tâches et sélectionnez **Déployer**. 
3. Sur l’onglet **Général**, sachez qu’il existe maintenant une option permettant de **Sélectionner un modèle de déploiement**. 
4. Suivez les étapes de **l’Assistant Déploiement logiciel** en sélectionnant les paramètres de déploiement de la séquence de tâches. 
5. Lorsque vous atteignez l’onglet **Résumé** de **l’Assistant Déploiement logiciel**, cliquez sur **Enregistrer comme modèle**.
6. Donnez un nom au modèle et sélectionnez les paramètres à enregistrer dans le modèle. 
7. Cliquez sur **Enregistrer**. Le modèle est maintenant utilisable avec l’option **Sélectionner un modèle de déploiement**.



## <a name="product-lifecycle-dashboard"></a>Tableau de bord Cycle de vie du produit
<!--1319632--> Le nouveau [tableau de bord Cycle de vie du produit](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard) affiche l’état de la stratégie de cycle de vie des produits Microsoft installés sur des appareils gérés avec Configuration Manager. Il fournit des informations sur les produits Microsoft de votre environnement, leur état de support et leur date de fin de support. Vous pouvez l’utiliser pour comprendre la disponibilité du support de chacun des produits. 

Pour accéder au tableau de bord Cycle de vie dans la console de Configuration Manager, accédez à **Biens et conformité** >**Asset Intelligence** >**Cycle de vie du produit**.



## <a name="improvements-to-reporting"></a>Améliorations apportées à la création de rapports
<!--1357653--> À partir de [vos commentaires](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and), nous avons ajouté un nouveau rapport, **Détails des services de maintenance Windows 10 pour une collection donnée**. Il affiche l’ID de la ressource, le nom NetBIOS, le nom du système d’exploitation et de sa version, la build, la branche du système d’exploitation et l’état du service de maintenance pour les appareils Windows 10. Pour le consulter, accédez à **Monitoring** >**Création de rapports** >**Rapports** >**Systèmes d’exploitation**  > **Détails des Services de maintenance Windows 10 pour une collection donnée**.



## <a name="improvements-to-software-center"></a>Améliorations apportées au Centre logiciel
<!--1357592--> Grâce à [vos commentaires](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid), il est maintenant possible de masquer les applications installées dans le Centre logiciel. Celles qui sont déjà installées ne s’afficheront plus dans l’onglet Applications lorsque cette option est activée. 

### <a name="try-it-out"></a>Essayez !
Activez le paramètre **Masquer les applications installées dans le Centre logiciel** dans les paramètres clients du Centre logiciel. Observez le comportement sur le Centre logiciel lorsque l’utilisateur final installe une application.



## <a name="improvements-to-run-scripts"></a>Améliorations apportées à l’exécution de scripts
<!--1236459--> La fonctionnalité [Exécuter des scripts](/sccm/apps/deploy-use/create-deploy-scripts) retourne maintenant le script de sortie suivant la mise en forme JSON. Ce format retourne toujours une sortie de script lisible. Il est possible que les scripts qui ne parviennent pas à s’exécuter ne génèrent pas de sortie. 



## <a name="boundary-group-fallback-for-management-points"></a>Groupe de limites de secours pour les points de gestion
<!-- 1324594 --> À partir de cette version, vous pourrez configurer des relations de secours pour les points de gestion entre [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups). Ce comportement offre un meilleur contrôle des points de gestion que les clients utilisent. L’onglet **Relations** des propriétés du groupe de limites comporte une nouvelle colonne pour le point de gestion. Lors de l’ajout d’un nouveau groupe de limites de secours, le temps de secours du point de gestion est actuellement toujours égal à zéro (0). Ce comportement est identique pour le **Comportement par défaut** dans le groupe de limites de site par défaut.

Auparavant, un problème se produisait souvent pour les points de gestion protégés présents dans un réseau sécurisé. Les clients du réseau d’entreprise principal recevaient une stratégie comprenant ce point de gestion protégé, même s’ils ne pouvaient pas communiquer avec lui à travers un pare-feu. Pour résoudre ce problème, utilisez l’option **Jamais d’action de secours** pour que les clients n’utilisent en secours que les points de gestion avec lesquels ils peuvent communiquer.

Lors de la mise à niveau du site vers cette version, Configuration Manager ajoute tous les points de gestion sans accès via Internet au groupe de limites de site par défaut. Ce comportement de mise à niveau permet de s’assurer que les versions antérieures des clients continuent de communiquer avec les points de gestion. Pour tirer pleinement parti de cette fonctionnalité, déplacez vos points de gestion vers les groupes de limites de votre choix.

L’action de secours du groupe de limites de point de gestion ne modifie pas le comportement lors de l’installation du client (ccmsetup). Si la ligne de commande ne spécifie pas le point de gestion initial avec le paramètre/MP, le nouveau client reçoit la liste complète des points de gestion disponibles. Pour son processus d’amorçage initial, le client utilise le premier point de gestion auquel il peut accéder. Une fois inscrit auprès du site, il recevra la liste des points de gestion convenablement triée avec ce nouveau comportement. 

### <a name="prerequisites"></a>Prérequis
- Activez les [points de gestion préférés](/sccm/core/servers/deploy/configure/boundary-groups#preferred-management-points). Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site** et sélectionnez **Sites**. Cliquez sur **Paramètres de hiérarchie** dans le ruban. Dans l’onglet **Général**, activez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**. 

### <a name="known-issues"></a>Problèmes connus
- Les processus de déploiement de système d’exploitation ne prennent pas en charge les groupes de limites.

### <a name="troubleshooting"></a>Résolution des problèmes
De nouvelles entrées apparaissent dans **LocationServices.log**. L’attribut **Localité** identifie l’un des états suivants :
- 0 : Inconnu.
- 1 : Le point de gestion spécifié se trouve uniquement dans le groupe de limites de site par défaut pour l’action de secours.
- 2 : Le point de gestion spécifié se trouve dans un groupe de limites voisin ou distant. S’il est à la fois dans le groupe de limites de site par défaut et dans un groupe voisin, la localité est 2.
- 3 : Le point de gestion spécifié se trouve dans le groupe de limites local ou actif. S’il est à la fois dans le groupe de limites actif et dans un groupe voisin ou le groupe de limites de site par défaut, la localité est 3. Si vous n’activez pas le paramètre des points de gestion préférés dans les Paramètres de hiérarchie, la localité est toujours 3, quel que soit le groupe de limites du point de gestion.

Les clients utilisent en premier les points de gestion locaux (localité 3), puis distants (localité 2) et enfin de secours (localité 1). 

Lorsqu’un client reçoit des cinq erreurs en dix minutes et ne parvient pas à communiquer avec l’un des points de gestion de son groupe de limites actif, il tente de contacter un point de gestion d’un groupe de limites voisin ou du groupe de limites de site par défaut. Si le point de gestion du groupe de limites actif revient en ligne par la suite, le client retournera au point de gestion local lors du prochain cycle d’actualisation. Ce cycle a une durée de 24 heures, ou se termine au redémarrage du service de l’agent Configuration Manager.



## <a name="improved-support-for-cng-certificates"></a>Prise en charge améliorée des certificats CNG
<!-- 1357314 --> La version 1710 de Configuration Manager (Current Branch) prend en charge [les certificats CNG (Cryptography : Next Generation)](/sccm/core/plan-design/network/cng-certificates-overview). La version 1710 limite la prise en charge aux certificats clients dans plusieurs scénarios. 

À partir de cette version Technical Preview, utilisez des certificats CNG pour les rôles serveurs HTTPS suivants :
- Point de gestion
- Point de distribution
- Point de mise à jour logicielle

La liste des [scénarios pris en charge](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios) reste la même.



## <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Prise en charge de la Passerelle de gestion cloud pour Azure Resource Manager
<!-- 1324735 --> Lors de la création d’une instance de [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), l’Assistant offre maintenant la possibilité de créer un **déploiement Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) est une plateforme moderne permettant de gérer l’ensemble des ressources de la solution comme une seule entité, nommée [groupe de ressources](/azure/azure-resource-manager/resource-group-overview#resource-groups). Lors du déploiement d’une Passerelle CMG avec Azure Resource Manager, le site utilise Azure Active Directory (Azure AD) pour authentifier et créer les ressources cloud nécessaires. Le certificat de gestion Azure classique n’est pas nécessaire pour ce déploiement modernisé.  

L’Assistant CMG propose toujours l’option de **déploiement de service classique** à l’aide d’un certificat de gestion Azure. Pour simplifier le déploiement et la gestion des ressources, nous vous recommandons d’utiliser le modèle de déploiement Azure Resource Manager pour toutes les nouvelles instances CMG. Si possible, redéployez les instances CMG existantes avec Resource Manager.

Configuration Manager ne migre pas les instances CMG classiques existantes vers le modèle de déploiement Azure Resource Manager. Créez de nouvelles instances CMG selon un déploiement Azure Resource Manager, puis supprimez les instances CMG classiques. 

> [!IMPORTANT]
> Cette fonctionnalité ne permet pas la prise en charge des fournisseurs de services cloud Azure. Le déploiement CMG avec Azure Resource Manager continue d’utiliser le service cloud classique, que ne prend pas en charge le fournisseur de services cloud. Pour plus d’informations, consultez les [services Azure disponibles auprès du fournisseur de services cloud Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="prerequisites"></a>Prérequis
- Intégration à [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Découverte d’utilisateurs Azure AD non requise.
- Mêmes [exigences pour la Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway), à l’exception du certificat de gestion Azure.

### <a name="try-it-out"></a>Essayez !  
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Dans l’espace de travail **Administration** de la console de Configuration Manager, développez **Services cloud**, puis sélectionnez **Passerelle de gestion cloud**. Cliquez sur **Créer une Passerelle de gestion cloud** dans le ruban. 
2. Sur la page **Général**, sélectionnez **Déploiement Azure Resource Manager**. Cliquez sur **Se connecter** pour vous authentifier avec un compte Administrateur d’abonnement Azure. L’Assistant remplit automatiquement les champs restants à partir des informations de l’abonnement Azure AD stockées dans les prérequis de l’intégration. Si vous possédez plusieurs abonnements, sélectionnez celui que vous souhaitez utiliser. Cliquez sur **Suivant**.  
3. Sur la page **Paramètres**, fournissez le fichier de certificat PKI de serveur, comme d’habitude. Ce certificat définit le nom du service CMG dans Azure. Sélectionnez la **Région**, puis une option de groupe de ressources : soit **Nouveau**, soit **Existant**. Entrez le nom du nouveau groupe de ressources, ou sélectionnez un groupe de ressources existant dans la liste déroulante. 
4. Effectuez toutes les étapes de l'Assistant.

> [!NOTE] 
> Pour l’application serveur Azure AD sélectionnée, Azure affecte l’autorisation **contributeur** de l’abonnement. 

Suivez la progression du déploiement de service avec **cloudmgr.log** sur le point de connexion du service.



## <a name="approve-application-requests-for-users-per-device"></a>Approuver les demandes d’application pour les utilisateurs appareil par appareil
<!-- 1357015 --> À compter de cette version, lorsqu’un utilisateur demande une application qui nécessite une approbation, le nom de l’appareil fait partie de la demande. Si l’administrateur approuve la demande, l’utilisateur ne pourra installer l’application que sur cet appareil. Il devra soumettre une autre demande pour installer l’application sur un autre appareil. 

> [!NOTE]
> Cette fonctionnalité est facultative. Lors du passage à cette version, activez cette fonctionnalité dans l’Assistant Mise à jour. Vous pourrez également le faire par la suite dans la console. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

### <a name="prerequisites"></a>Prérequis
- Mettre à niveau le client Configuration Manager (dernière version)
- Activer le paramètre client **Utiliser le nouveau Centre logiciel** dans le groupe [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent)

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Déployez une application en la rendant accessible à un regroupement d’utilisateurs.
2. Sur la page **Paramètres de déploiement**, activez l’option suivante : **Un administrateur doit approuver la demande de cette application sur l’appareil**.
3. En tant qu’utilisateur ciblé, utilisez le Centre logiciel pour soumettre une demande pour l’application. 
4. Affichez **Demandes d’approbation** sous **Gestion des applications** dans l’espace de travail **Bibliothèque de logiciels** de la console de Configuration Manager. Il y a maintenant une colonne **Appareil** dans la liste de chaque demande. À chaque action effectuée sur la demande, la boîte de dialogue Demande d’application comprend également le nom de l’appareil utilisé par l’utilisateur pour envoyer la demande.



## <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utiliser le Centre logiciel pour parcourir et installer des applications accessibles aux utilisateurs sur des appareils joints à Azure AD
<!-- 1322613 --> Les utilisateurs peuvent maintenant parcourir et installer les applications accessibles aux utilisateurs sur des appareils Azure Active Directory (Azure AD) en utilisant le Centre logiciel.  

### <a name="prerequisites"></a>Prérequis
- Activer HTTPS sur le point de gestion
- Intégrer le site avec [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure)
- Déployer une application en la rendant accessible à un regroupement d’utilisateurs
- Distribuer le contenu de l’application sur un [point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)
- Activer le paramètre client **Utiliser le nouveau Centre logiciel** dans le groupe [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent)
- Le client doit être : 
   - Windows 10
   - Joint à Azure AD, autrement dit joint à un domaine cloud
- Pour prendre en charge les clients basés sur Internet :
    - [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) 
    - Activez le paramètre client : **Autoriser les demandes de stratégies utilisateurs provenant de clients Internet** dans le groupe [Stratégie client](/sccm/core/clients/deploy/about-client-settings#client-policy)
- Pour prendre en charge les clients sur le réseau d’entreprise :
    - Ajouter le point de distribution cloud à un groupe de limites utilisé par les clients
    - Les clients doivent être en mesure de résoudre le nom de domaine complet (FQDN) du point de gestion compatible HTTPS



## <a name="report-on-windows-autopilot-device-information"></a>Générer un rapport sur les informations d’appareil Windows AutoPilot
<!-- 1351442 --> Windows AutoPilot est une solution permettant d’intégrer et de configurer de nouveaux appareils Windows 10 d’une manière moderne. Pour plus d'informations, consultez la page [Vue d’ensemble de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Pour inscrire un appareil existant auprès de Windows AutoPilot, vous pouvez charger les informations de l’appareil dans Microsoft Store pour Entreprises et Éducation : numéro de série, identificateur de produit Windows et identificateur matériel. Utilisez Configuration Manager pour collecter et consigner ces informations sur l’appareil. 

### <a name="prerequisites"></a>Prérequis
- Ces informations sur l’appareil s’appliquent uniquement aux clients sous Windows 10 version 1703 et versions ultérieures

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Dans l’espace de travail **Monitoring** de la console de Configuration Manager, développez le nœud **Création de rapports**, puis **Rapports**, et sélectionnez le nœud **Matériel – Général**.
2. Exécutez le nouveau rapport, **Informations sur les appareils Windows AutoPilot**, et affichez les résultats. 
3. Dans la visionneuse de rapports, cliquez sur l’icône **Exporter**, puis sélectionnez l’option **CSV (délimité par des virgules)**.
4. Après avoir enregistré le fichier, chargez les données dans Microsoft Store pour Entreprises et Éducation. Pour plus d’informations, consultez la page [Ajouter des appareils dans Microsoft Store pour Entreprises et Éducation](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Améliorations apportées aux stratégies de Configuration Manager pour Windows Defender Exploit Guard
<!-- 1356220 --> Des paramètres de stratégie supplémentaires pour les composants Réduction de la surface d’attaque et Accès contrôlé aux dossiers ont été ajoutés à Configuration Manager pour [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

**Nouveaux paramètres pour l’accès contrôlé aux dossiers**<br/>
Il existe deux options supplémentaires pour configurer l’accès contrôlé aux dossiers : **Bloquer uniquement les secteurs de disque** et **Auditer uniquement les secteurs de disque**. Ces deux paramètres permettent de n’autoriser l’accès contrôlé aux dossiers que pour les secteurs de démarrage et n’activent pas la protection de dossiers spécifiques ou des dossiers protégés par défaut. 

**Nouveaux paramètres pour la réduction de la surface d’attaque**
- Utilise une protection avancée contre les ransomware.
- Bloque les vols d’informations d’identification dans le sous-système d’autorité de sécurité locale Windows. 
- Bloque l’exécution des fichiers exécutables, sauf s’ils répondent à des critères de prévalence, d’âge ou de liste approuvée. 
- Bloque les processus non approuvés et non signés qui s’exécutent par USB.



## <a name="microsoft-edge-browser-policies"></a>Stratégies du navigateur Microsoft Edge
<!-- 1357310 --> Les clients qui utilisent le navigateur web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) sur des clients Windows 10 peuvent maintenant créer une stratégie de paramètres de conformité Configuration Manager pour configurer plusieurs paramètres Microsoft Edge. Actuellement, cette stratégie comprend les paramètres suivants :
- **Définir Microsoft Edge comme navigateur par défaut** : configure le paramètre d’application Windows 10 par défaut avec le navigateur web Microsoft Edge
- **Autoriser la liste déroulante de la barre d'adresses** : Windows 10 version 1703 ou ultérieure est requise. Pour plus d’informations, consultez la section [Stratégie de navigateur AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Autoriser la synchronisation des favoris entre navigateurs Microsoft** : Windows 10 version 1703 ou ultérieure est requise. Pour plus d’informations, consultez la section [Stratégie de navigateur SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Autoriser l'effacement des données de navigation en quittant** : Windows 10 version 1703 ou ultérieure est requise. Pour plus d’informations, consultez la section [Stratégie de navigateur ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Autoriser les en-têtes Do Not Track** : Pour plus d’informations, consultez la section [Stratégie de navigateur AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Autoriser le remplissage automatique** : Pour plus d’informations, consultez la section [Stratégie de navigateur AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Autoriser les cookies** : Pour plus d’informations, consultez la section [Stratégie de navigateur AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Autoriser le bloqueur de fenêtres publicitaires** : Pour plus d’informations, consultez la section [Stratégie de navigateur AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Autoriser les suggestions de recherche dans la barre d’adresse** : Pour plus d’informations, consultez la section [Stratégie de navigateur AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Autoriser l'envoi de trafic intranet vers Internet Explorer** : Pour plus d’informations, consultez la section [Stratégie de navigateur SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Autoriser le gestionnaire de mots de passe** : Pour plus d’informations, consultez la page [Stratégie de navigateur AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Autoriser les outils de développement** : Pour plus d’informations, consultez la page [Stratégie de navigateur AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Autoriser les extensions** : Pour plus d’informations, consultez la page [Stratégie de navigateur AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

### <a name="prerequisites"></a>Prérequis
- Client Windows 10 joint à Azure Active Directory. 

### <a name="known-issues"></a>Problèmes connus
- Les appareils joints à un domaine locaux ne peuvent pas appliquer cette stratégie dans cette version. Ce problème concerne également les appareils joints à un domaine hybrides.

### <a name="try-it-out"></a>Essayez !  
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

**Créer la stratégie**
1. Dans la console de Configuration Manager, accédez à l’espace de travail **Actifs et conformité**. Développez **Paramètres de conformité** et sélectionnez le nouveau nœud **Profils de navigateur Microsoft Edge**. Cliquez sur l’option du ruban **Créer une stratégie de navigateur Microsoft Edge**.
2. Donnez un **Nom** à la stratégie et, éventuellement, une **Description** ; ensuite, cliquez sur **Suivant**.
3. Sur la page **Paramètres**, remplacez la valeur des paramètres à inclure dans cette stratégie par **Configuré**, puis cliquez sur **Suivant**.
4. Sur la page **Plateformes prises en charge**, sélectionnez les architectures et les versions de système d’exploitation auxquelles s’applique cette stratégie, puis cliquez sur **Suivant**. 
5. Effectuez toutes les étapes de l'Assistant.

**Déployer la stratégie**
1. Sélectionnez votre stratégie et cliquez sur l’option de ruban **Déployer**.
2. Cliquez sur **Parcourir** et sélectionnez le regroupement d'utilisateurs ou d'appareils sur lequel la stratégie sera déployée. 
3. Sélectionnez d’autres options si nécessaire. Générez des alertes lorsque la stratégie n’est pas conforme. Définissez la planification selon laquelle le client évaluera la conformité à cette stratégie.
4. Cliquez sur **OK** pour créer le déploiement.

Comme toute stratégie de paramètres de conformité, le client corrige les paramètres selon le calendrier spécifié par vos soins. [Effectuez le monitoring et créez des rapports sur la conformité des appareils](/sccm/compliance/deploy-use/monitor-compliance-settings) dans la console de Configuration Manager.



## <a name="report-for-default-browser-counts"></a>Rapports pour le nombre de navigateurs par défaut
<!-- 1357830 --> Il existe maintenant un nouveau rapport qui affiche le nombre de clients ayant spécifié un certain navigateur web par défaut sous Windows. 

### <a name="known-issues"></a>Problèmes connus
- Lorsque vous ouvrez le rapport pour la première fois, il affiche uniquement le nombre, et non la valeur BrowserProgID. Pour contourner ce problème, remplacez la requête du rapport par la syntaxe suivante :  
    `select BrowserProgId00 as BrowserProgId, Count(*) as Count`  
    `from DEFAULT_BROWSER_DATA as dbd`  
    `group by BrowserProgId00`

### <a name="try-it-out"></a>Essayez !  
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.
1. Dans l’espace de travail **Monitoring** de la console de **Configuration Manager**, développez le nœud **Création de rapports**, puis **Rapports**, et sélectionnez **Logiciel – Sociétés et produits**.
2. Exécutez le rapport **Nombres de navigateurs par défaut**.

Utilisez la référence suivante pour les valeurs BrowserProgID courantes :
- **AppXq0fevzme2pys62n3e0fbqa7peapykr8v** : Microsoft Edge
- **IE.HTTP** : Microsoft Internet Explorer
- **ChromeHTML** : Google Chrome
- **OperaStable** : Opera Software
- **FirefoxURL-308046B0AF4A39CB** : Mozilla Firefox



## <a name="support-for-windows-10-arm64-devices"></a>Prise en charge des appareils Windows 10 ARM64
<!-- 1353704 --> À partir de cette version, le client Configuration Manager est pris en charge sur les appareils Windows 10 ARM64. Les fonctionnalités de gestion du client existantes devraient fonctionner avec ces nouveaux appareils, par exemple, l’inventaire matériel et logiciel, les mises à jour logicielles et la gestion des applications. Le déploiement de système d’exploitation n’est pas pris en charge pour le moment. 

## <a name="changes-to-phased-deployments"></a>Modifications apportées aux déploiements par phases
<!-- 1357405 --> Les déploiements par phases permettent d’automatiser le déploiement coordonné et séquencé de logiciels sur plusieurs regroupements. Dans cette version Technical Preview, l’Assistant Déploiement par phases peut être utilisé pour des séquences de tâches dans la console d’administration, et des déploiements sont créés. Toutefois, la deuxième phase ne démarre pas automatiquement une fois les critères de réussite de la première phase remplis. Vous pouvez la démarrer manuellement avec une instruction SQL.   

### <a name="try-it-out"></a>Essayez !  
  Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.
 
**Créer un déploiement par phases pour une séquence de tâches** </br>
1. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.
2. Cliquez avec le bouton droit sur une séquence de tâches et sélectionnez **Créer un déploiement par phases**. 
3. Sous l’onglet **Général**, donnez un nom et une description (facultative) au déploiement par phases, puis sélectionnez **Créer automatiquement un déploiement en deux phases par défaut**. 
4. Renseignez les champs **Premier regroupement** et **Deuxième regroupement**. Sélectionnez **Suivant**.
5. Sous l’onglet **Paramètres**, choisissez une option pour chacun des paramètres de planification, puis sélectionnez **Suivant** quand vous avez terminé. 
6. Sous l’onglet **Phases**, modifiez les phases si nécessaire, puis cliquez sur **Suivant**.
7. Vérifiez vos sélections sous l’onglet **Récapitulatif**, puis cliquez sur **Suivant** pour continuer.
8. Une fois les critères de réussite de la première phase atteints, suivez les instructions pour lancer la deuxième phase avec une instruction SQL.
 
**Démarrer la deuxième phase avec une instruction SQL**
1. Identifiez la valeur PhasedDeploymentID du déploiement que vous avez créé avec la requête SQL suivante :<br/> `Select * from PhasedDeployment`
2. Exécutez l’instruction suivante pour démarrer la phase de production :<br/> `UPDATE PhasedDeployment SET EvaluatePhasedDeployment = 1, Action = 3 WHERE PhasedDeploymentID = <Phased Deployment ID>`


## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
