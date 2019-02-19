---
title: Point de distribution cloud
titleSuffix: Configuration Manager
description: Planifiez et concevez la distribution de contenu logiciels via Microsoft Azure avec des points de distribution cloud dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f251d1356c0cc04ce285aa0ea9a131e5f21ee0f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156972"
---
# <a name="use-a-cloud-distribution-point-in-configuration-manager"></a>Utiliser un point de distribution cloud dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un point de distribution cloud est un point de distribution Configuration Manager qui est hébergé en tant que plateforme PaaS (Platform-as-a-Service) dans Microsoft Azure. Ce service prend en charge les scénarios suivants :  

- Fournir du contenu logiciel à des clients Internet sans infrastructure locale supplémentaire  

- Rendre votre système de distribution de contenu disponible dans le cloud  

- Réduire la nécessité de points de distribution traditionnels  


Cet article vous permet de découvrir plus d’informations sur le point de distribution cloud, de planifier son utilisation et de concevoir votre implémentation. Il comprend les sections suivantes :
- [Fonctionnalités et avantages](#bkmk_features)
- [Conception de la topologie](#bkmk_topology)
- [Requirements](#bkmk_requirements)
- [Spécifications](#bkmk_spec)
- [Coût](#bkmk_cost)
- [Performances et évolutivité](#bkmk_perf)
- [Ports et flux de données](#bkmk_dataflow)
- [Certificats](#bkmk_certs)
- [Forum aux questions](#bkmk_faq)



## <a name="bkmk_features"></a> Fonctionnalités et avantages

### <a name="features"></a>Fonctionnalités

Le point de distribution cloud prend en charge plusieurs fonctionnalités également proposées par les points de distribution locaux :  

-   Gérer les points de distribution cloud individuellement ou comme membres de groupes de points de distribution  

-   Utiliser un point de distribution cloud comme emplacement de contenu de secours  

-   Prend en charge des clients intranet et Internet  


### <a name="benefits"></a>Avantages

Le point de distribution cloud offre les autres avantages suivants :  

-   Le site chiffre le contenu avant de l’envoyer au point de distribution cloud dans Azure.  

-   Pour répondre aux demandes de contenu changeantes effectuées par les clients, vous pouvez mettre à l’échelle manuellement le service cloud dans Azure. Cette action ne nécessite pas l’installation et le provisionnement de points de distribution supplémentaires dans Configuration Manager.  

-   Prend en charge le téléchargement de contenu à partir de clients configurés pour d’autres technologies liées à du contenu, comme Windows BranchCache et d’autres fournisseurs de contenu.  

-   À compter de la version 1806, utilisez les points de distribution cloud comme emplacements sources pour les points de distribution d’extraction.  


## <a name="bkmk_topology"></a> Conception de la topologie

Le déploiement et le fonctionnement du point de distribution cloud incluent les composants suivants :  

- Un **service cloud** dans Azure. Le site distribue le contenu à ce service, qui le stocke dans le stockage cloud Azure. Le point de gestion fournit aux clients cet emplacement de contenu dans la liste des sources disponibles appropriées.  

- Un rôle de système de site **Point de gestion** traite normalement les demandes des clients des services.  

    - Les clients locaux utilisent généralement un point de gestion local.  

    - Les clients Internet utilisent une [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) ou un [point de gestion Internet](/sccm/core/clients/manage/plan-internet-based-client-management).  

- Le point de distribution cloud utilise un service web **HTTPS basé sur un certificat** pour sécuriser la communication réseau avec les clients. Les clients doivent approuver ce certificat.  


### <a name="azure-resource-manager"></a>Azure Resource Manager
<!--1322209--> À compter de la version 1806, créez un point de distribution cloud en utilisant un **déploiement Azure Resource Manager**. [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) est une plateforme moderne permettant de gérer l’ensemble des ressources de la solution comme une seule entité, nommée [groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups). Lors du déploiement d’un point de distribution cloud avec Azure Resource Manager, le site utilise Azure Active Directory (Azure AD) pour authentifier et créer les ressources cloud nécessaires. Le certificat de gestion Azure classique n’est pas nécessaire pour ce déploiement modernisé.  

> [!Note]  
> Cette fonctionnalité ne permet pas la prise en charge des fournisseurs de services cloud Azure. Les déploiements de points de distribution cloud avec Azure Resource Manager continuent d’utiliser le service cloud classique, que ne prend pas en charge le fournisseur de services cloud. Pour plus d’informations, consultez les [services Azure disponibles auprès du fournisseur de services cloud Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

L’Assistant Point de distribution cloud propose toujours l’option de **déploiement de service classique** à l’aide d’un certificat de gestion Azure. Pour simplifier le déploiement et la gestion des ressources, Microsoft recommande d’utiliser le modèle de déploiement Azure Resource Manager pour tous les nouveaux points de distribution cloud. Si possible, redéployez les points de distribution cloud existants avec Resource Manager.

> [!Important]  
> Depuis la version 1810, l’utilisation du déploiement de service Classic dans Azure est déprécié dans Configuration Manager. Cette version est la dernière à prendre en charge la création de ces déploiements Azure. Cette fonctionnalité sera supprimée dans la première version de Configuration Manager publiée après le 1er juillet 2019. Déplacez votre passerelle de gestion cloud et vos points de distribution cloud vers des déploiements Azure Resource Manager avant cette date. <!--SCCMDocs-pr issue #2993-->  

Configuration Manager ne migre pas les points de distribution cloud classiques existants vers le modèle de déploiement Azure Resource Manager. Créez de nouveaux points de distribution cloud à l’aide de déploiements Azure Resource Manager, puis supprimez les points de distribution cloud classiques. 


### <a name="hierarchy-design"></a>Conception de hiérarchie

L’endroit où vous créez le point de distribution cloud varie selon les clients qui doivent accéder au contenu. À compter de la version 1806, il existe trois types de points de distribution cloud :  

- Déploiement de service Classic : créez ce type uniquement sur un site principal.  

- Déploiement d’Azure Resource Manager : créez ce type sur un site principal ou sur le site d’administration centrale.  

- La passerelle de gestion cloud peut également délivrer du contenu à des clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).<!--1358651-->  


Pour déterminer s’il faut inclure les points de distribution cloud dans des groupes de limites, prenez en compte les comportements suivants :  

- Les clients Internet ne s’appuient pas sur des groupes de limites. Ils utilisent seulement des points de distribution accessibles sur Internet ou des points de distribution cloud. Si vous utilisez seulement des points de distribution cloud pour traiter ces types de clients, vous n’avez pas besoin de les inclure dans les groupes de limites.  

- Si vous voulez que les clients sur votre réseau interne utilisent un point de distribution cloud, celui-ci doit se trouver dans le même groupe de limites que les clients. Les clients placent les points de distribution cloud en dernière priorité dans leur liste de sources de contenu, car un coût est associé au téléchargement de contenu en dehors d’Azure. Ainsi, un point de distribution cloud est généralement utilisé comme source de secours pour les clients intranet. Si vous voulez une conception où le cloud est utilisé en premier, concevez vos groupes de limites pour répondre à cette exigence métier. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).  


Même si vous installez des points de distribution cloud dans des régions spécifiques d’Azure, les clients ne sont pas informés des régions Azure. Ils sélectionnent un point de distribution cloud de façon aléatoire. Si vous installez des points de distribution cloud dans plusieurs régions et qu’un client en reçoit plusieurs dans la liste des emplacements de contenu, le client peut ne pas utiliser un point de distribution cloud de la même région Azure.  


### <a name="backup-and-recovery"></a>Sauvegarde et récupération  

Quand vous utilisez un point de distribution cloud dans votre hiérarchie, aidez-vous des informations suivantes pour planifier la sauvegarde et la récupération :  

- Quand vous utilisez la tâche de maintenance **Serveur de site de sauvegarde**, Configuration Manager inclut automatiquement les configurations pour le point de distribution cloud.  

- Sauvegardez et enregistrez une copie du certificat d’authentification serveur. Si vous utilisez le déploiement de service classique dans Azure, sauvegardez et enregistrez également une copie du certificat de gestion Azure. Quand vous restaurez le site principal Configuration Manager sur un autre serveur, vous devez réimporter les certificats.  



##  <a name="bkmk_requirements"></a> Spécifications

- Vous avez besoin d’un **abonnement Azure** pour héberger le service.  

    - Un **administrateur Azure** doit participer à la création initiale de certains composants, en fonction de votre conception. Cette personne n’a pas besoin d’autorisations dans Configuration Manager.  

- Le serveur de site nécessite un **accès Internet** pour déployer et gérer le service cloud.  

- Lorsque vous utilisez la méthode de déploiement **Azure Resource Manager**, intégrez Configuration Manager à [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**. La *découverte des utilisateurs* Azure AD n’est pas nécessaire.  

- Si vous utilisez la méthode de déploiement classique Azure, vous avez besoin d’un **certificat de gestion Azure**. Pour plus d’informations, consultez la section [Certificats](#bkmk_certs) ci-dessous.   

    > [!TIP]  
    > À compter de Configuration Manager version 1806, utilisez le modèle de déploiement **Azure Resource Manager**. Il ne nécessite pas ce certificat de gestion.  
    > 
    > La méthode de déploiement classique est dépréciée depuis la version 1810.   

- Un **certificat d’authentification serveur**. Pour plus d’informations, consultez la section [Certificats](#bkmk_certs) ci-dessous.  

    - Pour réduire la complexité, Microsoft recommande d’utiliser un fournisseur de certificat public pour le certificat d’authentification serveur. Pour cela, vous avez également besoin d’un **alias CNAME du DNS** pour que les clients puissent résoudre le nom du service cloud.  

- Définissez le paramètre client **Autoriser l’accès au point de distribution cloud** sur **Oui** dans le groupe **Services cloud**. Par défaut, cette valeur est définie sur **Non**.  

- Les appareils clients nécessitent une **connectivité Internet**, et vous devez utiliser **IPv4**.  



## <a name="bkmk_spec"></a> Spécifications

- Le point de distribution cloud prend en charge toutes les versions de Windows listées dans [Systèmes d’exploitation pris en charge pour les clients et les appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

- Un administrateur distribue les types de contenu logiciel pris en charge suivants :  
  - Applications
  - Packages
  - Packages de mise à niveau de système d’exploitation
  - Mises à jour de logiciels de tiers  

    > [!Important]  
    > Si la console Configuration Manager ne bloque pas la distribution des mises à jour logicielles de Microsoft vers un point de distribution cloud, vous payez des coûts Azure pour stocker du contenu que les clients n’utilisent pas. Les clients Internet obtiennent toujours le contenu des mises à jour logicielles de Microsoft auprès du service cloud Microsoft Update. Ne distribuez pas les mises à jour logicielles de Microsoft sur un point de distribution cloud.    

- À compter de la version 1806, configurez un point de distribution d’extraction pour l’utilisation d’un point de distribution cloud comme source. Pour plus d’informations, consultez [À propos des points de distribution sources](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point#about-source-distribution-points).<!--1321554-->  


### <a name="deployment-settings"></a>Paramètres de déploiement

- Quand vous déployez une séquence de tâches avec comme option **Télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches**, le point de gestion n’inclut pas de point de distribution cloud comme emplacement de contenu. Déployez la séquence de tâches avec comme option **Télécharger tout le contenu localement avant de démarrer la séquence de tâches** pour que les clients utilisent un point de distribution cloud.  

- Un point de distribution cloud ne prend pas en charge les déploiements de packages avec comme option **Exécuter le programme à partir du point de distribution**. Utilisez l’option de déploiement **Télécharger le contenu à partir du point de distribution et l’exécuter localement**.  


### <a name="limitations"></a>Limitations  

- Vous ne pouvez pas utiliser un point de distribution cloud pour les déploiements de PXE ou en multidiffusion.  

- Un point de distribution cloud ne prend pas en charge les applications de streaming App-V.  

- Vous ne pouvez pas [préparer du contenu](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent) sur un point de distribution cloud. Le gestionnaire de distribution du site principal qui gère le point de distribution cloud transfère tout le contenu.  

- Vous ne pouvez pas configurer un point de distribution cloud comme point de distribution d’extraction.  



##  <a name="bkmk_cost"></a> Coût   
<!--501018-->
> [!IMPORTANT]  
> Les informations suivantes sur les coûts sont données à titre d’estimation seulement. Votre environnement peut avoir d’autres variables qui affectent le coût total d’utilisation d’un point de distribution cloud.  

Configuration Manager inclut les options suivantes qui facilitent le contrôle des coûts et la surveillance de l’accès aux données :  

- Contrôlez et surveillez la quantité de contenu que vous stockez dans un service cloud. Pour plus d’informations, consultez [Surveiller les points de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Configurer Configuration Manager pour être averti quand les seuils mensuels des téléchargements des clients sont atteints ou dépassés. Pour plus d’informations, consultez [Alertes de seuil de transfert de données](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_alerts).   

- Pour réduire le nombre de transferts de données que les clients effectuent à partir des points de distribution cloud, utilisez une des technologies suivantes de cache entre pairs :  
  - Cache entre pairs Configuration Manager
  - Windows BranchCache
  - Optimisation de la distribution de Windows 10  

    Pour plus d’informations, consultez [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).   


### <a name="components"></a>Composants

Un point de distribution cloud utilise les composants Azure suivants, qui impliquent des frais pour le compte de l’abonnement Azure :  

> [!Tip]  
> À compter de la version 1806, la passerelle de gestion cloud peut également délivrer du contenu à des clients. Cette fonctionnalité réduit les coûts en consolidant les machines virtuelles Azure. Pour plus d’informations, consultez [Coût pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#cost).  

#### <a name="virtual-machine"></a>Machine virtuelle
- Le point de distribution cloud utilise les services cloud Azure comme plateforme PaaS. Ce service utilise des machines virtuelles qui génèrent des coûts de calcul.  

- Chaque service du point de distribution cloud utilise deux machines virtuelles A0 Standard.  

- Pour vous aider à déterminer les coûts potentiels, consultez la [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/).

    > [!NOTE]  
    > Les coûts des machines virtuelles varient selon la région.

#### <a name="outbound-data-transfer"></a>Transfert de données sortantes
- Les flux de données entrant dans Azure sont gratuits (entrée ou chargement). La distribution de contenu depuis le site vers le point de distribution cloud est un chargement dans Azure.  

- Les frais sont calculés d’après les données qui sortent d’Azure (sortie ou téléchargement). Les flux de données de point de distribution cloud sortant d’Azure sont des contenus logiciels que les clients téléchargent.  

- Pour plus d’informations, consultez [Surveiller les points de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure#bkmk_monitor).  

- Pour vous aider à déterminer les coûts potentiels, consultez les [détails de la tarification de la bande passante](https://azure.microsoft.com/pricing/details/bandwidth/). La tarification pour le transfert de données est à plusieurs niveaux. Plus votre utilisation augmente, moins vous payez par gigaoctet.  

#### <a name="content-storage"></a>Stockage de contenu
- Les clients Internet obtiennent gratuitement le contenu des mises à jour logicielles de Microsoft auprès du service cloud Microsoft Update. Ne distribuez pas les packages de déploiement de mises à jour logicielles avec les mises à jour logicielles de Microsoft sur un point de distribution cloud. Sinon, vous engendrez des coûts de stockage de données pour du contenu que les clients n’utilisent jamais.  

- Les points de distribution cloud utilisent le stockage d’objets blob standard suivant, en fonction du modèle de déploiement :  

    - Un déploiement classique utilise le stockage Azure géoredondant (GRS). Pour plus d’informations, consultez [Stockage géoredondant](https://docs.microsoft.com/azure/storage/common/storage-redundancy-grs).  

    - Un déploiement Azure Resource Manager utilise le stockage Azure localement redondant (LRS). Ce changement réduit le coût du compte de stockage. Le déploiement classique n’utilisait pas les fonctionnalités supplémentaires du GRS. Pour plus d’informations, consultez [Stockage localement redondant](https://docs.microsoft.com/azure/storage/common/storage-redundancy-lrs).  

#### <a name="other-costs"></a>Autres coûts
- Chaque service cloud a une adresse IP dynamique. Chaque point de distribution cloud distinct utilise une nouvelle adresse IP dynamique. L’ajout de machines virtuelles supplémentaires par service cloud n’augmente pas le nombre de ces adresses.  



##  <a name="bkmk_dataflow"></a> Ports et flux de données   

Il existe deux flux de données principaux pour le point de distribution cloud :  

- Le serveur de site se connecte à Azure pour configurer le service du point de distribution cloud  

- Un client se connecte au point de distribution cloud pour télécharger du contenu  


### <a name="site-server-to-azure"></a>Serveur de site vers Azure

Vous n’avez pas besoin d’ouvrir des ports entrants sur votre réseau local. Le serveur de site établit toutes les communications avec Azure et le point de distribution cloud pour déployer, mettre à jour et gérer le service cloud. Le serveur de site doit être en mesure de créer des connexions sortantes vers le cloud Microsoft. Le principe est le même que lorsque vous installez le rôle de système de site du point de distribution sur un site spécifique.  


### <a name="client-to-cloud-distribution-point"></a>Client vers point de distribution cloud

Vous n’avez pas besoin d’ouvrir des ports entrants sur votre réseau local. Les clients Internet communiquent directement avec le service Azure. Les clients sur votre réseau interne qui utilisent un point de distribution cloud doivent être en mesure de se connecter au cloud Microsoft. 

Pour plus d’informations sur la priorité des emplacements de contenu et quand les clients intranet utilisent un point de distribution cloud, consultez [Priorités des sources de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority).

Quand un client utilise un point de distribution cloud comme emplacement de contenu :  

1. Le point de gestion donne un jeton d’accès au client, ainsi que la liste des sources de contenu. Ce jeton est valide pour 24 heures et donne au client un accès au point de distribution cloud.  

2. Le point de gestion répond à la demande d’emplacement du client avec le **nom de domaine complet du service** du point de distribution cloud. Cette propriété est la même que le nom commun du certificat d’authentification serveur.  

    Si vous utilisez votre nom de domaine, par exemple WallaceFalls.contoso.com, le client essaie d’abord de résoudre ce nom de domaine complet. Vous avez besoin d’un alias CNAME dans le DNS accessible via Internet de votre domaine pour que les clients puissent résoudre le nom du service Azure, par exemple : WallaceFalls.cloudapp.net.  

3. Le client résout ensuite le nom du service Azure, par exemple WallaceFalls.cloudapp.net, en une adresse IP valide. Cette réponse doit être gérée par le DNS d’Azure.  

4. Le client se connecte au point de distribution cloud. Azure équilibre la charge de la connexion sur une des instances de machine virtuelle. Le client s’authentifie lui-même avec le jeton d’accès.  

5. Le point de distribution cloud authentifie le jeton d’accès du client, puis donne au client l’emplacement exact du contenu dans Stockage Azure.  

6. Si le client approuve le certificat d’authentification serveur du point de distribution cloud, il se connecte à Stockage Azure pour télécharger le contenu. 



##  <a name="bkmk_perf"></a> Performances et évolutivité   
<!--494872-->

Comme avec la conception de tout autre point de distribution, prenez en compte les facteurs suivants :  
- Le nombre de connexions clientes simultanées
- La taille du contenu que les clients téléchargent
- La durée acceptable pour répondre à vos besoins métier 

En fonction de la [conception de votre topologie](#bkmk_topology), si les clients peuvent choisir entre plusieurs points de distribution cloud pour un contenu donné, ils choisissent naturellement de façon aléatoire entre ces services cloud. Si vous distribuez seulement certains éléments de contenu à un point de distribution cloud, et qu’un grand nombre de clients essaient de télécharger ce contenu en même temps, cette activité engendre une charge plus élevée sur ce même point de distribution cloud. L’ajout d’un point de distribution cloud supplémentaire inclut également un service Stockage Azure distinct. Pour plus d’informations sur la façon dont le client communique avec les composants du point de distribution cloud et télécharge le contenu, consultez [Ports et flux de données](#bkmk_dataflow).  

Le point de distribution cloud utilise deux machines virtuelles Azure comme frontend pour le stockage Azure. Ce déploiement par défaut répond aux besoins de la plupart des clients. Dans certains cas extrêmes, avec un grand nombre de connexions clientes simultanées (par exemple 150 000 clients), la capacité de traitement des machines virtuelles Azure ne peut pas faire face aux demandes des clients. Vous ne pouvez pas redimensionner les machines virtuelles Azure utilisées pour le point de distribution cloud. Vous ne pouvez pas configurer le nombre d’instances de machine virtuelle pour le point de distribution cloud dans Configuration Manager, mais vous pouvez si nécessaire reconfigurer le service cloud dans le portail Azure. Ajoutez manuellement d’autres instances de machine virtuelle ou configurez le service pour qu’il se mette à l’échelle automatiquement. 

> [!Important]  
> Quand vous mettez à jour Configuration Manager, le site redéploie le service cloud. Si vous reconfigurez manuellement le service cloud dans le portail Azure, le nombre d’instances est rétabli à deux, qui est la valeur par défaut.  

Le service Stockage Azure prend en charge 500 demandes par seconde pour un même fichier. Un test des performances d’un point de distribution cloud a pris en charge la distribution d’un même fichier de 100 Mo à 50 000 clients en 24 heures.<!--512106-->  



##  <a name="bkmk_certs"></a> Certificats  

En fonction de la conception de votre point de distribution cloud, vous avez besoin d’un ou plusieurs certificats numériques.  


### <a name="general-information"></a>Informations générales
<!--SCCMDocs issue #779--> Les certificats pour les points de distribution cloud prennent en charge les configurations suivantes :  

- **Longueur de clé de 4 096 bits**  

- À compter de la version 1710, prise en charge des certificats **Version 3**. Pour plus d’informations, consultez [Vue d’ensemble des certificats CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- À compter de la version 1802, lorsque vous configurez Windows avec la stratégie suivante : **Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature**  

- À compter de la version 1802, prise en charge de **TLS 1.2**. Pour plus d’informations, consultez [Informations techniques de référence sur les contrôles de chiffrement](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  


### <a name="azure-management-certificate"></a>Certificat de gestion Azure

*Ce certificat est obligatoire pour les déploiements de services classiques. Par contre, il ne l’est pas pour les déploiements Azure Resource Manager.*

Si vous utilisez la méthode de déploiement classique Azure, vous avez besoin d’un **certificat de gestion Azure**. Pour plus d’informations, consultez la section [Certificat de gestion Azure](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#azure-management-certificate) de l’article sur les certificats de passerelle de gestion cloud. Le serveur de site Configuration Manager utilise ce certificat pour s’authentifier auprès d’Azure, pour créer et gérer le déploiement classique.  

> [!TIP]  
> À compter de Configuration Manager version 1806, utilisez le modèle de déploiement **Azure Resource Manager**. Il ne nécessite pas ce certificat de gestion.  
> 
> La méthode de déploiement classique est dépréciée depuis la version 1810.   

Pour réduire la complexité, utilisez le même certificat de gestion Azure pour tous les déploiements classiques de points de distribution cloud et de passerelles de gestion cloud, sur tous les abonnements Azure et tous les sites Configuration Manager.


### <a name="server-authentication-certificate"></a>Certificat d'authentification serveur

*Ce certificat est obligatoire pour tous les déploiements de point de distribution cloud.*

Pour plus d’informations, consultez [Certificat d’authentification serveur de passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate) et si nécessaire, les sous-sections suivantes :  
- Certificat racine approuvé de passerelle de gestion cloud pour les clients
- Certificat d’authentification serveur émis par le fournisseur public
- Certificat d’authentification serveur émis par l’infrastructure à clé publique d’entreprise

Le point de distribution cloud utilise ce type de certificat de la même façon que la passerelle de gestion cloud. Les clients doivent également approuver ce certificat. Pour réduire la complexité, Microsoft recommande d’utiliser un certificat émis par un fournisseur public. 

Sauf si vous utilisez un certificat générique, ne réutilisez pas le même certificat. Chaque instance du point de distribution cloud et de la passerelle de gestion cloud nécessite un certificat d’authentification serveur unique. 

Pour plus d’informations sur la création de ce certificat à partir d’une infrastructure à clé publique, consultez [Déployer le certificat de service pour des points de distribution cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).  



##  <a name="bkmk_faq"></a> Forum aux questions   

### <a name="does-a-client-need-a-certificate-to-download-content-from-a-cloud-distribution-point"></a>Un client a-t-il besoin d’un certificat pour télécharger du contenu à partir d’un point de distribution cloud ?

Un certificat d’authentification client n’est pas nécessaire. Le client n’a besoin d’approuver le certificat d’authentification serveur utilisé par le point de distribution cloud. Si ce certificat est émis par un fournisseur de certificat public, la plupart des appareils Windows incluent déjà des certificats racine approuvés pour ces fournisseurs. Si vous avez émis un certificat d’authentification serveur à partir de l’infrastructure à clé publique de votre organisation, vos clients doivent approuver les certificats d’émission dans toute la chaîne. Cette chaîne inclut l’autorité de certification racine, ainsi que toutes les autorités de certification intermédiaires. En fonction de la conception de votre infrastructure à clé publique, ce certificat peut introduire une complexité supplémentaire dans le déploiement du point de distribution cloud. Pour éviter cette complexité, Microsoft recommande d’utiliser un fournisseur de certificat public déjà approuvé par vos clients.  


### <a name="can-my-on-premises-clients-use-a-cloud-distribution-point"></a>Mes clients locaux peuvent-ils utiliser un point de distribution cloud ?

Oui. Si vous voulez que les clients sur votre réseau interne utilisent un point de distribution cloud, celui-ci doit se trouver dans le même groupe de limites que les clients. Les clients placent les points de distribution cloud en dernière priorité dans leur liste de sources de contenu, car un coût est associé au téléchargement de contenu en dehors d’Azure. Ainsi, un point de distribution cloud est généralement utilisé comme source de secours pour les clients intranet. Si vous voulez une conception où le cloud est utilisé en premier, concevez vos groupes de limites en conséquence. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).  


### <a name="do-i-need-azure-expressroute"></a>Ai-je besoin d’Azure ExpressRoute ?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) vous permet d’étendre votre réseau local dans Microsoft Cloud. ExpressRoute ou d’autres connexions de réseau virtuel du même type ne sont pas nécessaires pour le point de distribution cloud de Configuration Manager.  

Si votre organisation utilise ExpressRoute, isolez l’abonnement Azure pour le point de distribution cloud de l’abonnement qui utilise ExpressRoute. Cette configuration garantit que le point de distribution cloud n’est pas connecté accidentellement de cette manière.  


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Ai-je besoin d’assurer la maintenance des machines virtuelles Azure ?

Aucune maintenance n’est nécessaire. La conception du point de distribution cloud utilise la plateforme PaaS Azure. Configuration Manager utilise l’abonnement que vous fournissez pour créer les machines virtuelles, le stockage et le réseau nécessaires. Azure sécurise et met à jour les machines virtuelles. Ces machines virtuelles ne font pas partie de votre environnement local, comme c’est le cas avec IaaS (Infrastructure as a Service). Le point de distribution cloud est une plateforme PaaS qui étend votre environnement Configuration Manager dans le cloud. Pour plus d’informations, consultez [Avantages d’un modèle de service cloud PaaS pour la sécurité](https://docs.microsoft.com/azure/security/security-paas-deployments#security-advantages-of-a-paas-cloud-service-model).  


### <a name="does-the-cloud-distribution-point-use-azure-cdn"></a>Le point de distribution cloud utilise-t-il Azure CDN ?

Le réseau de distribution de contenu (CDN) Azure est une solution globale pour la distribution rapide de contenu à haut débit en mettant en cache le contenu sur des nœuds physiques stratégiquement placés dans le monde entier. Pour plus d’informations, consultez [Présentation d’Azure CDN](https://docs.microsoft.com/azure/cdn/cdn-overview).

Le point de distribution cloud Configuration Manager ne prend actuellement pas en charge Azure CDN.



## <a name="next-steps"></a>Étapes suivantes
[Installer des points de distribution cloud](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure)
