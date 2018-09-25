---
title: Nouvelle version 1802
titleSuffix: Configuration Manager
description: Découvrez des informations détaillées sur les modifications et les nouvelles fonctionnalités introduites dans la version 1802 de Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5bd637b1-d7a1-411b-877a-c7aae9741173
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0757e7f3fac12c2945a3eab860851b0debf28fd5
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893887"
---
# <a name="whats-new-in-version-1802-of-system-center-configuration-manager"></a>Nouveautés de la version 1802 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1802 pour la Current Branch de Configuration Manager est disponible en tant que mise à jour dans la console. Appliquez cette mise à jour sur les sites qui exécutent la version 1702, 1706 ou 1710. <!-- baseline only statement: -->Lors de l’installation d’un nouveau site, elle est également disponible sous la forme d’une version de base de référence.

En plus des nouvelles fonctionnalités, cette version inclut également des modifications supplémentaires comme des corrections de bogues. Pour plus d’informations, consultez [Récapitulatif des modifications dans Current Branch de System Center Configuration Manager version 1802](https://support.microsoft.com/help/4101375).

Les mises à jour supplémentaires suivantes pour cette version sont également disponibles :
- [Correctif cumulatif pour Current Branch de System Center Configuration Manager, version 1802](https://support.microsoft.com/help/4163547)

> [!TIP]  
> Pour installer un nouveau site, vous devez utiliser une version de base de Configuration Manager.  
>
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Installation de mises à jour sur les sites](/sccm/core/servers/manage/updates)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Les sections suivantes fournissent des détails sur les modifications et les nouvelles fonctionnalités de la version 1802 de Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1802 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastructure de site

### <a name="reassign-distribution-point"></a>Réaffecter un point de distribution
<!-- 1306937 --> De nombreux clients ont de grandes infrastructures Configuration Manager et réduisent le nombre de sites principaux ou secondaires pour simplifier leur environnement. Ils doivent néanmoins toujours conserver des points de distribution aux emplacements des filiales pour délivrer du contenu aux clients gérés. Ces points de distribution contiennent souvent plusieurs téraoctets ou plus de contenus. Ce contenu est coûteux en termes de temps et de bande passante réseau pour le distribuer à ces serveurs distants. Cette fonctionnalité vous permet de réaffecter un point de distribution à un autre site principal sans redistribuer le contenu. Cette action met à jour l’affectation du système de site tout en conservant la totalité du contenu sur le serveur. Pour plus d’informations, consultez [Réaffecter un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign).

### <a name="configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups"></a>Configurer l’Optimisation de la distribution de Windows de façon à utiliser des groupes de limites Configuration Manager
<!-- 1324696 --> Les groupes de limites Configuration Manager permettent de définir et de réguler la distribution de contenu sur le réseau de l’entreprise et dans les agences. [L’Optimisation de la distribution de Windows](/windows/deployment/update/waas-delivery-optimization) est une technologie cloud pair à pair de partage de contenu entre appareils Windows 10. À partir de cette version, vous pourrez la configurer de façon à ce qu’elle utilise vos groupes de limites pour partager du contenu entre pairs. Un nouveau paramètre client s’applique à l’identificateur de groupe de limites sous la forme de l’identificateur de groupe d’Optimisation de la distribution sur le client. Lorsque le client communique avec le service de cloud d’Optimisation de la distribution, il utilise cet identificateur pour localiser les pairs possédant le contenu souhaité. Pour plus d’informations, consultez [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).

### <a name="support-for-windows-10-arm64-devices"></a>Prise en charge des appareils Windows 10 ARM64
<!-- 1353704 --> À partir de cette version, le client Configuration Manager est pris en charge sur les appareils Windows 10 ARM64. Les fonctionnalités de gestion du client existantes devraient fonctionner avec ces nouveaux appareils, par exemple, l’inventaire matériel et logiciel, les mises à jour logicielles et la gestion des applications. Le déploiement de système d’exploitation n’est pas pris en charge pour le moment. 

### <a name="improved-support-for-cng-certificates"></a>Prise en charge améliorée des certificats CNG
<!-- 1357314 --> La version 1710 de Configuration Manager (Current Branch) prend en charge les certificats [Cryptography : Next Generation (CNG)](/sccm/core/plan-design/network/cng-certificates-overview). La version 1710 limite la prise en charge aux certificats clients dans plusieurs scénarios. 

À compter de cette version, utilisez des certificats de passerelle de gestion cloud pour les rôles serveurs HTTPS suivants :
- Point de gestion
- Point de distribution
- Point de mise à jour logicielle
- Point de migration d’état  


### <a name="boundary-group-fallback-for-management-points"></a>Groupe de limites de secours pour les points de gestion
<!-- 1324594 --> Configurez des relations de secours pour les points de gestion entre les [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups). Ce comportement offre un meilleur contrôle des points de gestion que les clients utilisent. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).


### <a name="cloud-distribution-point-site-affinity"></a>Affinité de site de point de distribution cloud
<!--503719--> Cette fonctionnalité profite aux clients qui ont une hiérarchie multisite, géographiquement dispersée, utilisant des points de distribution cloud. Quand un client Internet recherchait du contenu, il n’y avait aucun ordre dans la liste des points de distribution cloud reçus par le client. Ce comportement avait comme conséquence que les clients Internet pouvaient recevoir le contenu de points de distribution cloud géographiquement distants. Le téléchargement du contenu d’un serveur distant est généralement plus lent que celui d’un serveur plus proche.
 
Avec l’affinité de site de point de distribution cloud, un client Internet reçoit une liste ordonnée. Cette liste établit la priorité des points de distribution cloud à partir du site affecté au client. Ce comportement permet à l’administrateur de conserver le but de sa conception pour les téléchargements de contenu à partir des ressources de site.
 

## <a name="management-insights"></a>Management insights
<!-- 1353967 --> Les insights de gestion dans System Center Configuration Manager fournissent des informations sur l’état actuel de votre environnement. Les informations sont basées sur l’analyse des données provenant de la base de données du site. Ces informations vous aident à mieux comprendre votre environnement et à prendre des mesures en fonction de ces renseignements. Pour plus d’informations, consultez [Insights de gestion](/sccm/core/servers/manage/management-insights)

Dans Configuration Manager 1802, les insights suivants sont disponibles :
- Applications :
    - Applications sans déploiements
- Services cloud : <!--1356412-->
    - Évaluer la préparation de la cogestion 
    - Permettre à vos appareils d’être hybrides joints à Azure Active Directory
    - Moderniser votre infrastructure d’identité et d’accès
    -  Mettre à niveau vos clients vers Windows 10, version 1709 ou ultérieure 
- Regroupements :
    - Regroupements vides
- Gestion simplifiée :  <!--1355148-->
    - Versions des clients obsolètes  
- Centre logiciel : 
    - Diriger les utilisateurs vers le Centre logiciel au lieu du catalogue d’applications  
    - Utiliser la nouvelle version du Centre logiciel 
- Windows 10 : <!--1357421-->
    - Configurer la télémétrie et la clé d’ID commercial de Windows 
    - Connecter Configuration Manager à Upgrade Readiness 
   
<!-- ## Migration  -->



## <a name="client-management"></a>Gestion des clients

### <a name="cloud-management-gateway-support-for-azure-resource-manager"></a>Prise en charge de la Passerelle de gestion cloud pour Azure Resource Manager
<!-- 1324735 --> Lors de la création d’une instance de [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), l’Assistant offre maintenant la possibilité de créer un **déploiement Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) est une plateforme moderne permettant de gérer l’ensemble des ressources de la solution comme une seule entité, nommée [groupe de ressources](/azure/azure-resource-manager/resource-group-overview#resource-groups). Lors du déploiement d’une Passerelle CMG avec Azure Resource Manager, le site utilise Azure Active Directory (Azure AD) pour authentifier et créer les ressources cloud nécessaires. Le certificat de gestion Azure classique n’est pas nécessaire pour ce déploiement modernisé. Pour plus d’informations, consultez [Conception de la topologie de passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway#azure-resource-manager).

> [!IMPORTANT]
> Cette fonctionnalité ne permet pas la prise en charge des fournisseurs de services cloud Azure. Le déploiement de la passerelle de gestion cloud avec Azure Resource Manager continue d’utiliser le service cloud classique, que le fournisseur de services cloud ne prend pas en charge. Pour plus d’informations, consultez [Services Azure disponibles auprès du fournisseur de services cloud Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### <a name="improvements-to-cloud-management-gateway"></a>Améliorations apportées à la passerelle de gestion cloud  

- À compter de cette version, la **passerelle de gestion cloud** n’est plus une fonctionnalité en préversion.  

- La documentation des fonctionnalités a été revue et améliorée. Pour plus d’informations, consultez les articles suivants :
    - [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
    - [Taille et scalabilité de la passerelle de gestion cloud en chiffres](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
    - [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
    - [Questions fréquentes (FAQ) sur la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
    - [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
    - [Configurer la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  


### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a>Configurer l’inventaire matériel pour collecter les chaînes supérieures à 255 caractères
<!-- 1357389 --> Vous pouvez configurer la longueur des chaînes à une taille supérieure à 255 caractères pour les propriétés de l’inventaire matériel. Cette modification s’applique seulement aux classes nouvellement ajoutées et aux propriétés de l’inventaire matériel qui ne sont pas des clés. Pour plus d’informations, consultez l’article [Étendre l’inventaire matériel](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255). 

 ### <a name="deprecation-announcement-for-linux-and-unix-client-support"></a>Annonce de la dépréciation de la prise en charge des clients Linux et Unix
 <!--510139--> Microsoft prévoit de déprécier la prise en charge des clients Linux et UNIX dans System Center Configuration Manager d’ici un an environ, de sorte que les clients ne seront pas inclus dans SCCM version 1902 dans le calendrier anticipé de 2019. Dans le dernier calendrier 2018, la version 1810 de Configuration Manager est la dernière version à inclure les clients Linux et UNIX qui seront pris en charge pour le cycle de vie complet de Configuration Manager 1810. Après Configuration Manager 1810, les clients devraient envisager d’utiliser Microsoft Azure Management pour gérer les serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.

### <a name="surface-device-dashboard"></a>Tableau de bord des appareils Surface
<!--1355788--> Le tableau de bord des appareils Surface fournit des informations sur les appareils Surface trouvés dans votre environnement. Dans la console, accédez à **Surveillance** > **Appareils Surface**. Vous pouvez voir les éléments suivants :
- Le pourcentage d’appareils Surface
- Le pourcentage de modèles Surface
- Les cinq principales versions de microprogramme

Pour plus d’informations, consultez l’article [Tableau de bord Surface](/sccm/core/clients/manage/surface-device-dashboard).

### <a name="change-in-the-configuration-manager-client-install"></a>Changement dans l’installation du client Configuration Manager
<!--1356195--> À compter de cette version, Silverlight n’est plus installé automatiquement sur les appareils clients. Pour plus d’informations, consultez [Prérequis pour le déploiement de clients sur des ordinateurs Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#bkmk_ExternalDependencies).

## <a name="co-management"></a>Cogestion

### <a name="transition-endpoint-protection-workload-to-intune-using-co-management"></a>Transférer la charge de travail Endpoint Protection vers Intune à l’aide de la cogestion
<!-- 1357365 --> La charge de travail Endpoint Protection peut être transférée à Intune après activation de la cogestion. Pour cela, accédez à la page des propriétés de cogestion et déplacez le curseur de Configuration Manager sur **Pilote** ou **Tout**. Pour plus d’informations sur les charges de travail, consultez [Charges de travail pouvant être transférées à Intune](/sccm/core/clients/manage/co-management-switch-workloads#Workloads-able-to-be-transitioned-to-Intune). Pour plus d’informations sur la cogestion, consultez [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview).
 
### <a name="co-management-dashboard-in-system-center-configuration-manager"></a>Tableau de bord de cogestion dans System Center Configuration Manager
<!--1356648--> À compter de cette version, vous pouvez consulter un tableau de bord avec des informations sur la cogestion. Le tableau de bord vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphes peuvent vous aider à identifier les appareils qui demandent une attention particulière. Pour plus d’informations, consultez l’article [Tableau de bord de cogestion](\sccm\core\clients\manage\client-management-dashboard). 


## <a name="compliance-settings"></a>Paramètres de conformité

### <a name="microsoft-edge-browser-policies"></a>Stratégies du navigateur Microsoft Edge
<!-- 1357310 --> Pour les clients qui utilisent le navigateur web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) sur des clients Windows 10, créez une stratégie de paramètres de conformité Configuration Manager pour configurer plusieurs paramètres Microsoft Edge. Pour plus d’informations, consultez [Créer un profil de navigateur Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles). 



## <a name="application-management"></a>Gestion des applications

### <a name="allow-user-interaction-when-installing-an-application"></a>Autoriser l’interaction utilisateur lors de l’installation d’une application
<!-- 1356976 --> Autorisez un utilisateur final à interagir avec l’installation d’une application pendant l’exécution de la séquence de tâches. Par exemple, exécutez un processus d’installation qui invite l’utilisateur final à choisir diverses options. Certains programmes d’installation d’application ne peuvent pas se passer d’invites utilisateur ou le processus d’installation nécessite des valeurs de configuration spécifiques que seul l’utilisateur connaît. Cette fonctionnalité vous permet de gérer ces scénarios d’installation. Pour plus d’informations, consultez [Spécifier des options d’expérience utilisateur pour le type de déploiement](/sccm/apps/deploy-use/create-applications#specify-user-experience-options-for-the-deployment-type).

### <a name="do-not-automatically-upgrade-superseded-applications"></a>Ne pas mettre automatiquement à niveau les applications remplacées
<!-- 1351266 --> Configurez un déploiement d’application pour ne pas mettre à niveau automatiquement les versions remplacées. Désormais, quand vous créez le déploiement, dans la page **Paramètres du déploiement** de l’**Assistant Déploiement logiciel**, pour un objectif d’installation **Disponible**, vous pouvez activer ou désactiver l’option **Mettre automatiquement à niveau toutes les versions remplacées de cette application**. Pour plus d’informations, consultez [Spécifier des paramètres de déploiement](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

### <a name="approve-application-requests-for-users-per-device"></a>Approuver les demandes d’application pour les utilisateurs appareil par appareil
<!-- 1357015 --> À compter de cette version, lorsqu’un utilisateur demande une application qui nécessite une approbation, le nom de l’appareil fait partie de la demande. Si l’administrateur approuve la demande, l’utilisateur ne pourra installer l’application que sur cet appareil. Il devra soumettre une autre demande pour installer l’application sur un autre appareil. Pour plus d’informations, consultez [Spécifier des paramètres de déploiement](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings).

 > [!Note]  
 > Cette fonctionnalité est facultative. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  


### <a name="run-scripts-improvements"></a>Améliorations apportées à l’exécution de scripts 
<!-- 1236459 --> À compter de cette version, la fonctionnalité **Exécuter les scripts** n’est plus en préversion. La sortie du script est désormais retournée au format JSON. Pour plus d’informations, consultez [Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).


## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation

### <a name="windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway"></a>Séquence de tâches de mise à niveau sur place de Windows 10 via la Passerelle de gestion cloud
<!-- 1357149 --> La [séquence de tâches de mise à niveau sur place](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) de Windows 10 prend maintenant en charge le déploiement vers des clients basés sur Internet et gérés par le biais de la [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Cette capacité permet aux utilisateurs distants de passer plus facilement à Windows 10, sans avoir à se connecter au réseau d’entreprise. Pour plus d'informations, voir [Déployer une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-windows-10-in-place-upgrade-task-sequence"></a>Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10
<!-- 1357425 --> Le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend maintenant des groupes supplémentaires, avec des actions recommandées à ajouter avant ou après le processus de mise à niveau. Ces actions sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils sur Windows 10. Pour plus d’informations, consultez [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-to-prepare-for-upgrade).

### <a name="improvements-to-operating-system-deployment"></a>Améliorations apportées au déploiement des systèmes d’exploitation
Cette version inclut les améliorations suivantes pour le déploiement de système d’exploitation :
 - Dans Windows PE, lors du lancement de cmtrace.exe, vous n’êtes plus invité à choisir s’il faut utiliser ce programme comme visionneuse par défaut pour les fichiers journaux. <!-- SMS 500897 -->
 - Ajoutez des images de démarrage à l’étape de séquence de tâches [Télécharger le contenu du package](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent).
 - Améliorations apportées à l’étape [Exécuter une séquence de tâches](/sccm/osd/understand/task-sequence-steps#child-task-sequence) : <!-- 1261338 -->   
     - Prise en charge de tous les scénarios de déploiement de système d’exploitation à partir du Centre logiciel, de l’environnement PXE (Preboot Execution Environment) et de médias.
     - Améliorations apportées à des actions de console comme la copie, l’importation, l’exportation et l’avertissement lors de la suppression d’objets.
     - Prise en charge de l’Assistant [Création d’un fichier de contenu préparé](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).
     - Intégration à la vérification du déploiement. Pour plus d’informations, consultez [Déploiements de séquences de tâches à haut risque](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS). 
     - Vous pouvez désormais utiliser l’étape d’exécution de la séquence de tâches sur plusieurs niveaux de séquences de tâches, et non uniquement sur une relation parent-enfant unique. Les relations multiniveaux ajoutent de la complexité, alors utilisez-les avec précaution. Les références circulaires sont toujours vérifiées dans ces relations.
    
### <a name="deployment-templates-for-task-sequences"></a>Modèles de déploiement pour les séquences de tâches
<!-- 1357391 --> L’[Assistant Déploiement de séquences](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) de tâches peut maintenant créer un modèle de déploiement. Celui-ci peut être enregistré et appliqué à une séquence de tâches existante ou nouvelle pour créer un déploiement. 

### <a name="phased-deployments-for-task-sequences"></a>Déploiements par phases pour des séquences de tâches
<!--1356837--> Les déploiements par phases sont une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). Les déploiements par phases automatisent le lancement coordonné et séquencé d’une séquence de tâches sur plusieurs regroupements. Vous pouvez [créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) avec deux phases par défaut ou configurer manuellement plusieurs phases. Le déploiement par phrases de séquences de tâches ne prend pas en charge l’installation PXE ou à partir d’un support.




## <a name="software-center"></a>Centre logiciel

### <a name="install-multiple-applications-in-software-center"></a>Installer plusieurs applications dans le Centre logiciel
<!-- 1357126 --> Si un utilisateur final ou un technicien a besoin d’installer plusieurs applications sur un appareil, le Centre logiciel prend désormais en charge l’installation de plusieurs applications sélectionnées. Ce comportement permet à l’utilisateur de ne pas perdre de temps, car il n’est pas obligé d’attendre qu’une installation soit terminée pour commencer la suivante. Pour plus d’informations, consultez [Installer plusieurs applications](/sccm/core/understand/software-center#install-multiple-applications) dans le guide utilisateur du nouveau Centre logiciel.

### <a name="use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices"></a>Utiliser le Centre logiciel pour parcourir et installer des applications accessibles aux utilisateurs sur des appareils joints à Azure AD
<!-- 1322613 --> Les utilisateurs peuvent maintenant parcourir et installer les applications accessibles aux utilisateurs sur des appareils Azure Active Directory (Azure AD) en utilisant le Centre logiciel. Pour plus d’informations, consultez [Déployer des applications disponibles pour l’utilisateur sur des appareils joints à Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).

### <a name="hide-installed-applications-in-software-center"></a>Masquer les applications installées dans le Centre logiciel
<!--1357592--> Il est maintenant possible de masquer les applications installées dans le Centre logiciel. Celles qui sont déjà installées ne s’affichent plus sous l’onglet Applications quand cette option est activée sous les paramètres clients. Cette option est définie par défaut quand vous installez ou mettez à niveau vers Configuration Manager 1802.  Les applications installées sont toujours disponibles pour examen sous l’onglet de l’état d’installation. [Masquer les applications installées dans le Centre logiciel](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) contient des informations supplémentaires.   

### <a name="hide-unapproved-applications-in-software-center"></a>Masquer les applications non approuvées dans le Centre logiciel
 <!--1355146--> Quand cette option est activée pour les clients, les applications disponibles pour l’utilisateur qui nécessitent une approbation sont masquées dans le Centre logiciel.  [Masquer les applications non approuvées dans le Centre logiciel](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) contient des informations supplémentaires.  

### <a name="software-center-shows-user-additional-compliance-information"></a>Le Centre logiciel affiche des informations de conformité supplémentaires de l’utilisateur
<!-- 1235616 --> Lors de l’utilisation de l’état de l’attestation d’intégrité de l’appareil en tant que règle de stratégie de conformité pour l’accès conditionnel aux ressources d’entreprise, le Centre logiciel montre désormais à l’utilisateur le paramètre d’attestation d’intégrité de l’appareil qui n’est pas conforme.


 ## <a name="software-updates"></a>Mises à jour logicielles 

### <a name="schedule-automatic-deployment-rule-evaluation-to-be-offset-from-a-base-day"></a>Planifiez l’évaluation des règles de déploiement automatique pour la décaler à partir d’un jour de base. 
<!--1357133--> Les règles de déploiement automatique peuvent être planifiées pour évaluer le décalage à partir d’un jour de base. Cela signifie que si le correctif Mardi tombe en fait un mercredi pour vous, vous pouvez définir le calendrier d’évaluation pour le deuxième mardi du mois avec un décalage d’un jour. Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule). 



## <a name="reporting"></a>Rapports

### <a name="report-for-default-browser-counts"></a>Rapports pour le nombre de navigateurs par défaut
<!-- 1357830 --> Il existe maintenant un nouveau rapport qui affiche le nombre de clients ayant spécifié un certain navigateur web par défaut sous Windows. Consultez le rapport **Nombre de navigateurs par défaut** dans le groupe de rapports **Logiciel - Sociétés et produits**. Pour plus d’informations, consultez [Liste des rapports](/sccm/core/servers/manage/list-of-reports#software---companies-and-products).

### <a name="report-on-windows-autopilot-device-information"></a>Générer un rapport sur les informations d’appareil Windows AutoPilot
<!-- 1351442 --> Windows AutoPilot est une solution permettant d’intégrer et de configurer de nouveaux appareils Windows 10 d’une manière moderne. Pour plus d’informations, consultez [Vue d’ensemble de Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). Pour inscrire un appareil existant auprès de Windows AutoPilot, vous pouvez charger les informations de l’appareil dans Microsoft Store pour Entreprises et Éducation : numéro de série, identificateur de produit Windows et identificateur matériel. Utilisez Configuration Manager pour collecter et communiquer ces informations sur les appareils avec le nouveau rapport, **Informations d’appareil Windows AutoPilot**, dans le nœud de rapports **Matériel - Général**. Pour plus d’informations, consultez [Nouveaux appareils Windows 10](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) en préparation à la cogestion.

### <a name="report-on-windows-10-servicing-details-for-a-specific-collection"></a>Rapport sur les détails de la maintenance de Windows 10 pour un regroupement spécifique
<!--1357653--> Le **rapport Détails de la maintenance de Windows 10 pour un regroupement spécifique** montre des informations générales sur la maintenance de Windows 10 pour un regroupement spécifique. Il affiche l’ID de la ressource, le nom NetBIOS, le nom du système d’exploitation et de sa version, la build, la branche du système d’exploitation et l’état du service de maintenance pour les appareils Windows 10. Pour plus d’informations, consultez [Liste des rapports](/sccm/core/servers/manage/list-of-reports#operating-system).



<!-- ## Inventory  -->



<!-- ## Mobile device management -->



 ## <a name="protect-devices"></a>Protéger les appareils

### <a name="improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard"></a>Améliorations apportées aux stratégies de Configuration Manager pour Windows Defender Exploit Guard
<!-- 1356220 --> Des paramètres de stratégie supplémentaires pour les composants [Réduction de la surface d’attaque](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_ASR) et [Accès contrôlé aux dossiers ](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy#BKMK_CFA)ont été ajoutés à Configuration Manager pour [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

### <a name="new-host-interaction-settings-for-windows-defender-application-guard"></a>Nouveaux paramètres d’interaction d’hôte pour Windows Defender Application Guard
<!-- 1356256 --> Pour les appareils avec Windows 10 version 1709 et ultérieur, il existe deux nouveaux paramètres d’interaction d’hôte pour [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) : 
- Vous pouvez autoriser les sites web à accéder au processeur graphique virtuel de l’hôte. 
- Les fichiers téléchargés dans le conteneur peuvent être conservés sur l’hôte. 




## <a name="configuration-manager-console"></a>Console Configuration Manager

### <a name="improvements-to-the-configuration-manager-console"></a>Améliorations apportées à la console Configuration Manager 
Cette version comprend les améliorations suivantes apportées à la console Configuration Manager.
- Les listes d’appareils sous Ressources et conformité, Appareils, affichent désormais l’utilisateur principal par défaut. Cette colonne s’affiche seulement dans le nœud Appareils. Le dernier utilisateur connecté peut également être ajouté en tant que colonne facultative.<!-- 1357280 --> Activez les paramètres clients [Affinité entre utilisateur et appareil](/sccm/core/clients/deploy/about-client-settings#user-and-device-affinity) pour le site, de façon à associer à un utilisateur principal à un appareil.
- Quand un regroupement est membre d’un autre regroupement et qu’il est renommé, le nouveau nom est mis à jour dans les règles d’adhésion.<!--1357282--> 
- Lors de l’utilisation du contrôle à distance sur un client avec plusieurs moniteurs ayant une mise à l’échelle différente des ppp, le curseur de la souris est maintenant correctement mappé entre eux. <!--433170-->
- Le [tableau de bord Gestion des clients Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) affiche une liste des appareils concernés quand des sections de graphe sont sélectionnées. <!--1357281 --> 



## <a name="next-steps"></a>Étapes suivantes
Quand vous êtes prêt à installer cette version, consultez [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).
