---
title: Planifier la passerelle de gestion cloud
titleSuffix: Configuration Manager
description: Planifiez et concevez la passerelle de gestion cloud pour simplifier la gestion des clients Internet.
ms.date: 10/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f7e598da0953a20412f6c8279b90a95c1d26581
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411474"
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Planifier la passerelle de gestion cloud dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*
 
<!--1101764--> La passerelle de gestion cloud fournit un moyen simple de gérer les clients Configuration Manager sur Internet. En déployant la passerelle de gestion cloud comme un service cloud dans Microsoft Azure, vous pouvez gérer les clients traditionnels qui sont itinérants sur Internet sans infrastructure supplémentaire. De même, vous n’avez pas besoin d’exposer votre infrastructure locale sur Internet. 

> [!Tip]  
> Cette fonctionnalité a été introduite dans la version 1610 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1802, cette fonctionnalité n’est plus en préversion.  


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Une fois les prérequis établis, la création de la passerelle de gestion cloud se fait via les trois étapes suivantes dans la console Configuration Manager :
1. Déployer le service cloud de la passerelle de gestion cloud sur Azure.
2. Ajouter le rôle de point de connexion de passerelle de gestion cloud. 
3. Configurer le site et les rôles de site pour le service. Une fois déployés et configurés, les clients accèdent sans problème aux rôles de site locaux, qu’ils soient sur l’intranet ou sur Internet.

Cet article fournit les connaissances de base permettant de découvrir la passerelle de gestion cloud, comment elle s’intègre dans votre environnement, et de planifier l’implémentation. 



## <a name="scenarios"></a>Scénarios 

La passerelle de gestion cloud présente des avantages dans plusieurs scénarios. Voici quelques-uns des scénarios les plus courants :  

- Gérer des clients Windows traditionnels avec une identité jointe à un domaine Active Directory. Ces clients incluent Windows 7, Windows 8.1 et Windows 10. Elle utilise des certificats d’infrastructure à clé publique pour sécuriser le canal de communication. Les activités de gestion sont les suivantes :  
    - Mises à jour logicielles et protection des points de terminaison
    - État du parc et des clients
    - Paramètres de conformité
    - Distribution de logiciels à l’appareil
    - Séquence de tâches de mise à niveau sur place de Windows 10 (à partir de la version 1802)

- Gérer les clients Windows 10 traditionnels avec une identité moderne, hybride ou cloud pure et jointe au domaine avec Azure Active Directory (Azure AD). Les clients utilisent Azure AD pour s’authentifier, au lieu de certificats d’infrastructure à clé publique. L’utilisation d’Azure AD demande une installation, une configuration et une gestion plus simples que pour les systèmes plus complexes des infrastructures à clé publique. Les activités de gestion sont les mêmes que pour le premier scénario, ainsi que :  
    - Distribution de logiciels à l’utilisateur  

- Installation du client Configuration Manager sur les appareils Windows 10 via Internet. L’utilisation d’Azure AD permet à l’appareil de s’authentifier auprès de la passerelle de gestion cloud pour l’inscription et l’affectation du client. Vous pouvez installer le client manuellement ou via une autre méthode de distribution de logiciels, comme Microsoft Intune.  

- Nouveau provisionnement des appareils avec la cogestion. La passerelle de gestion cloud n’est pas obligatoire pour la cogestion. Elle permet de réaliser un scénario de bout en bout pour les nouveaux appareils impliquant Windows AutoPilot, Azure AD, Microsoft Intune et Configuration Manager.  

### <a name="specific-use-cases"></a>Cas d’usage spécifiques
Dans ces scénarios, les cas d’usage d’appareils spécifiques suivants peuvent s’appliquer :

- Appareils itinérants, comme les ordinateurs portables  

- Appareils distants ou dans les filiales, dont la gestion est moins coûteuse et plus efficace via Internet que via un réseau WAN ou un VPN.  

- Fusions et acquisitions, où il peut être plus facile de joindre des appareils à Azure AD et de les gérer via une passerelle de gestion cloud.  

> [!Important]
> Par défaut, tous les clients reçoivent une stratégie pour une passerelle de gestion cloud et commencent à l’utiliser quand ils sont basés sur Internet. Selon le scénario et le cas d’usage qui s’appliquent à votre organisation, il peut être nécessaire de délimiter l’utilisation de la passerelle de gestion cloud. Pour plus d’informations, consultez le paramètre client [Autoriser les clients à utiliser une passerelle de gestion cloud](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).


## <a name="topology-design"></a>Conception de la topologie

### <a name="cmg-components"></a>Composants de la passerelle de gestion cloud
Le déploiement et le fonctionnement de la passerelle de gestion cloud incluent les composants suivants :  

- Le **service cloud de passerelle de gestion cloud** dans Azure authentifie et transfère les demandes des clients Configuration Manager au point de connexion de la passerelle de gestion cloud.  
 
- Le rôle de système de site **Point de connexion de passerelle de gestion cloud** permet une connexion cohérente et hautes performances entre le réseau local et le service de passerelle de gestion cloud dans Azure. Il publie également les paramètres sur la passerelle de gestion cloud, notamment les informations de connexion et les paramètres de sécurité. Le point de connexion de la passerelle de gestion cloud transfère les demandes des clients de la passerelle de gestion cloud vers les rôles locaux en fonction des mappages d’URL.

- Le rôle de système de site [**Point de connexion de service**](/sccm/core/servers/deploy/configure/about-the-service-connection-point) exécute le composant du gestionnaire de service cloud, qui gère toutes les tâches de déploiement de la passerelle de gestion cloud. En outre, il surveille et transmet les informations d’intégrité du service et de journalisation à partir d’Azure AD. Vérifiez que votre point de connexion de service est en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).  

- Le rôle de système de site **Point de gestion** traite normalement les demandes des clients des services.  

- Le rôle de système de site **Point de mise à jour logicielle** traite normalement les demandes des clients des services.  

- **Les clients Internet** se connectent à la passerelle de gestion cloud pour accéder aux composants de Configuration Manager local.

- La passerelle de gestion cloud utilise un service web **HTTPS basé sur un certificat** pour sécuriser la communication réseau avec les clients.  

- Les clients Internet utilisent **des certificats d’infrastructure à clé publique ou Azure AD** pour l’identité et l’authentification.  

- Un [**point de distribution cloud**](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) fournit du contenu aux clients Internet selon les besoins.  

    - À compter de la version 1806, une passerelle de gestion cloud peut également distribuer du contenu aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure. Pour plus d’informations, consultez [Modifier une passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).<!--1358651-->  


### <a name="azure-resource-manager"></a>Azure Resource Manager
<!-- 1324735 --> À compter de la version 1802, vous pouvez créer la passerelle de gestion cloud en utilisant un **déploiement Azure Resource Manager**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) est une plateforme moderne permettant de gérer l’ensemble des ressources de la solution comme une seule entité, nommée [groupe de ressources](/azure/azure-resource-manager/resource-group-overview#resource-groups). Lors du déploiement d’une Passerelle CMG avec Azure Resource Manager, le site utilise Azure Active Directory (Azure AD) pour authentifier et créer les ressources cloud nécessaires. Le certificat de gestion Azure classique n’est pas nécessaire pour ce déploiement modernisé.  

L’Assistant CMG propose toujours l’option de **déploiement de service classique** à l’aide d’un certificat de gestion Azure. Pour simplifier le déploiement et la gestion des ressources, l’utilisation du modèle de déploiement Azure Resource Manager est recommandé pour toutes les nouvelles instances de passerelle de gestion cloud. Si possible, redéployez les instances CMG existantes avec Resource Manager. Pour plus d’informations, consultez [Modifier une passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).

> [!IMPORTANT]  
> Cette fonctionnalité ne permet pas la prise en charge des fournisseurs de services cloud Azure. Le déploiement de la passerelle de gestion cloud avec Azure Resource Manager continue d’utiliser le service cloud classique, que le fournisseur de services cloud ne prend pas en charge. Pour plus d’informations, consultez les [services Azure disponibles auprès du fournisseur de services cloud Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services). 


### <a name="hierarchy-design"></a>Conception de hiérarchie

Créez la passerelle de gestion cloud sur le site de plus haut niveau de votre hiérarchie. S’il s’agit d’un site d’administration centrale, créez des points de connexion de passerelle de gestion cloud sur les sites principaux enfants. Le composant du gestionnaire de service cloud se trouve sur le point de connexion du service, qui est également sur le site d’administration centrale. Cette conception permet si nécessaire de partager le service entre différents sites principaux.

Vous pouvez créer plusieurs services de passerelle de gestion cloud dans Azure et plusieurs points de connexion de passerelle de gestion cloud. Des points de connexion de passerelle de gestion cloud multiples permettent l’équilibrage de charge du trafic client depuis la passerelle de gestion cloud vers les rôles locaux. Pour réduire la latence du réseau, affectez la passerelle de gestion cloud associée à la même région géographique que le site principal.

 > [!Note]  
 > Les clients Internet et la passerelle de gestion cloud ne sont dans aucun groupe de limites.

D’autres facteurs, comme le nombre de clients à gérer, impactent également votre conception de la passerelle de gestion cloud. Pour plus d’informations, consultez [Performances et échelle](#performance-and-scale).

#### <a name="example-1-standalone-primary-site"></a>Exemple 1 : Site principal autonome

Contoso a un site principal autonome dans un centre de données local à son siège social de New York. 
- Le département informatique crée une passerelle de gestion cloud dans la région Azure États-Unis de l’Est pour réduire la latence du réseau. 
- Il crée deux points de connexion de passerelle de gestion cloud, les deux étant liés au même service de passerelle de gestion cloud.  

Quand les clients se déplacent et utilisent Internet, ils communiquent avec la passerelle de gestion cloud dans la région Azure États-Unis de l’Est. La passerelle de gestion cloud transfère cette communication via les deux points de connexion de passerelle de gestion cloud.

#### <a name="example-2-hierarchy-with-site-specific-cmg"></a>Exemple 2 : Hiérarchie avec une passerelle de gestion cloud spécifique au site

Fourth Coffee a un site d’administration centrale dans un centre de données local à son siège social de Seattle. Un site principal se trouve dans le même centre de données, et l’autre site principal se trouve dans son bureau européen principal à Paris. 
- Sur le site d’administration centrale, le département informatique crée deux services de passerelle de gestion cloud :
     - Une passerelle de gestion cloud dans la région Azure États-Unis de l’Ouest.
     - Une passerelle de gestion cloud dans la région Azure Europe de l’Ouest.
- Sur le site principal de Seattle, il crée un point de connexion de passerelle de gestion cloud lié à la passerelle de gestion cloud États-Unis de l’Ouest.
- Sur le site principal de Paris, il crée un point de connexion de passerelle de gestion cloud lié à la passerelle de gestion cloud Europe de l’Ouest.

Quand les clients basés à Seattle se déplacent et utilisent Internet, ils communiquent avec la passerelle de gestion cloud dans la région Azure États-Unis de l’Ouest. La passerelle de gestion cloud transfère cette communication au point de connexion de passerelle de gestion cloud basé à Seattle.

De même, quand les clients basés à Paris se déplacent et utilisent Internet, ils communiquent avec la passerelle de gestion cloud dans la région Azure Europe de l’Ouest. La passerelle de gestion cloud transfère cette communication au point de connexion de passerelle de gestion cloud basé à Paris. Quand des utilisateurs basés à Paris se déplacent au siège de la société à Seattle, leurs ordinateurs continuent de communiquer avec la passerelle de gestion cloud dans la région Azure Europe de l’Ouest. 

 > [!Note]  
 > Fourth Coffee a envisagé la création d’un autre point de connexion de passerelle de gestion cloud sur le site principal de Paris lié à la passerelle de gestion cloud États-Unis de l’Ouest. Les clients basés à Paris utiliseraient alors les deux passerelles de gestion cloud, quel que soit l’endroit où ils se trouvent. Si cette configuration permet d’équilibrer le trafic et offre une redondance du service, elle peut également entraîner des délais quand des clients basés à Paris communiquent avec la passerelle de gestion cloud basée aux États-Unis. Les clients Configuration Manager ne sont actuellement pas informés de leur région géographique et ne cherchent donc pas à préférer une passerelle de gestion cloud qui est géographiquement plus proche. Les clients utilisent de façon aléatoire une passerelle de gestion cloud disponible.



## <a name="requirements"></a>spécifications

- Un **abonnement Azure** pour héberger la passerelle de gestion cloud.  

    - Un **administrateur Azure** doit participer à la création initiale de certains composants, en fonction de votre conception. Cette personne n’a pas besoin d’autorisations dans Configuration Manager.  

- Au moins un serveur Windows local pour héberger le **point de connexion de passerelle de gestion cloud**. Vous pouvez colocaliser ce rôle avec d’autres rôles système de site Configuration Manager.  

- Le **point de connexion de service**  doit être en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).   

- Un [**certificat d’authentification serveur**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_serverauth) pour la passerelle de gestion cloud.  

- Si vous utilisez la méthode de déploiement classique Azure, vous devez utiliser un [**certificat de gestion Azure**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_azuremgmt).  

    > [!TIP]  
    > À compter de Configuration Manager version 1802, Microsoft recommande d’utiliser le modèle de déploiement **Azure Resource Manager**. Il ne nécessite pas ce certificat de gestion.  

- **D’autres certificats** peuvent être nécessaires, en fonction de la version du système d’exploitation et du modèle d’authentification de votre client. Pour plus d’informations, consultez [Certificats de passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

    - À compter de la version 1802, vous devez configurer tous les [**points de gestion activés pour la passerelle de gestion cloud afin d’utiliser le protocole HTTPS**](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

    - À compter de la version 1806, quand vous utilisez l’option de site destinée à **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**, le point de gestion peut être HTTP. Pour plus d’informations, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).  


- L’intégration à **Azure AD** peut être nécessaire pour les clients Windows 10. Pour plus d’informations, consultez [Configurer des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- Les clients doivent utiliser **IPv4**.  



## <a name="specifications"></a>Spécifications

- Toutes les versions de Windows listées dans [Systèmes d’exploitation pris en charge pour les clients et les appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sont prises en charge pour la passerelle de gestion cloud.  

- La passerelle de gestion cloud prend en charge les rôles Point de gestion et Point de mise à jour logicielle.  

- La passerelle de gestion cloud ne prend pas en charge les clients qui communiquent seulement avec des adresses IPv6.<!--495606-->  

- Les points de mise à jour logicielle utilisant un équilibreur de charge réseau ne fonctionnent pas avec la passerelle de gestion cloud. <!--505311-->  

- À compter de la version 1802, les déploiements de passerelle de gestion cloud avec le modèle Azure Resource Manager ne permettent pas la prise en charge des fournisseurs de services cloud Azure. Le déploiement de la passerelle de gestion cloud avec Azure Resource Manager continue d’utiliser le service cloud classique, que le fournisseur de services cloud ne prend pas en charge. Pour plus d’informations, consultez les [services Azure disponibles dans les fournisseurs de services cloud Azure](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### <a name="support-for-configuration-manager-features"></a>Prise en charge des fonctionnalités de Configuration Manager
Le tableau suivant détaille la prise en charge par la passerelle de gestion cloud des fonctionnalités de Configuration Manager :


|Fonctionnalité  |Assistance  |
|---------|---------|
| Mises à jour logicielles     | ![Pris en charge](media/green_check.png) |
| Endpoint Protection     | ![Pris en charge](media/green_check.png) |
| Inventaire matériel et logiciel     | ![Pris en charge](media/green_check.png) |
| État du client et notifications     | ![Pris en charge](media/green_check.png) |
| Exécuter les scripts     | ![Pris en charge](media/green_check.png) |
| Paramètres de conformité     | ![Pris en charge](media/green_check.png) |
| Installation du client<br>(avec intégration d’Azure AD)     | ![Pris en charge](media/green_check.png)  (1706) |
| Distribution de logiciels (ciblée sur des appareils)     | ![Pris en charge](media/green_check.png) |
| Distribution de logiciels (ciblée sur des utilisateurs, obligatoires)<br>(avec intégration d’Azure AD)     | ![Pris en charge](media/green_check.png)  (1710) |
| Distribution de logiciels (ciblée sur des utilisateurs, disponibles)<br>([toutes les exigences](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices)) | ![Pris en charge](media/green_check.png)  (1802) |
| Séquence de tâches de mise à niveau sur place de Windows 10     | ![Pris en charge](media/green_check.png)  (1802) |
| CMPivot     | ![Pris en charge](media/green_check.png)  (1806) |
| Tous les autres scénarios de séquence de tâches     | ![Non pris en charge](media/Red_X.png) |
| Installation Push du client     | ![Non pris en charge](media/Red_X.png) |
| Attribution automatique du site     | ![Non pris en charge](media/Red_X.png) |
| Catalogue d’applications     | ![Non pris en charge](media/Red_X.png) |
| Demandes d’approbation de logiciel     | ![Non pris en charge](media/Red_X.png) |
| Console Configuration Manager     | ![Non pris en charge](media/Red_X.png) |
| outils de contrôle à distance.     | ![Non pris en charge](media/Red_X.png) |
| Site web de création de rapports     | ![Non pris en charge](media/Red_X.png) |
| Éveil par appel réseau     | ![Non pris en charge](media/Red_X.png) |
| Clients Mac, Linux et UNIX     | ![Non pris en charge](media/Red_X.png) |
| Cache d’homologue     | ![Non pris en charge](media/Red_X.png) |
| Gestion des appareils mobiles locale     | ![Non pris en charge](media/Red_X.png) |


|Clé|
|--|
|![Pris en charge](media/green_check.png) = Cette fonctionnalité est prise en charge avec la passerelle de gestion cloud par toutes les versions prises en charge de Configuration Manager  |
|![Prise en charge](media/green_check.png) (*AAMM*) = cette fonctionnalité est prise en charge avec la passerelle de gestion cloud depuis la version *AAMM* de Configuration Manager  |
|![Non pris en charge](media/Red_X.png) = Cette fonctionnalité n’est pas prise en charge avec la passerelle de gestion cloud. |



## <a name="cost"></a>Coût

>[!IMPORTANT]  
>Les informations suivantes sur les coûts sont données à titre d’estimation seulement. Votre environnement peut avoir d’autres variables qui affectent le coût total d’utilisation de la passerelle de gestion cloud.

La passerelle de gestion cloud utilise les composants Azure suivants, qui impliquent des frais pour le compte de l’abonnement Azure :

#### <a name="virtual-machine"></a>Machine virtuelle

- La passerelle de gestion cloud utilise les services cloud Azure comme PaaS (plateforme en tant que service). Ce service utilise des machines virtuelles qui génèrent des coûts de calcul.  

- Dans Configuration Manager version 1706, la passerelle de gestion cloud utilise une machine virtuelle Standard A2.  

- À compter de Configuration Manager version 1710, la passerelle de gestion cloud utilise une machine virtuelle Standard A2 V2.  

- Vous choisissez le nombre d’instances de machine virtuelle qui prennent en charge la passerelle de gestion cloud. La valeur par défaut est 1 et 16 est le maximum. Ce nombre est défini lors de la création de la passerelle de gestion cloud et il peut être changé ultérieurement pour faire évoluer le service en fonction des besoins.

- Pour plus d’informations sur le nombre de machines virtuelles dont vous avez besoin pour prendre en charge vos clients, consultez [Performances et évolutivité](#performance-and-scale).

- Pour vous aider à déterminer les coûts potentiels, consultez la [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/).

    > [!NOTE]  
    > Les coûts des machines virtuelles varient selon la région.

#### <a name="outbound-data-transfer"></a>Transfert de données sortantes

- Les frais sont calculés d’après les données qui sortent d’Azure (sortie ou téléchargement). Les flux de données entrant dans Azure sont gratuits (entrée ou chargement). Les flux de données de la passerelle de gestion cloud sortant d’Azure incluent la stratégie pour le client, les notifications au client et les réponses au client transférées au site par la passerelle de gestion cloud. Ces réponses incluent les rapports d’inventaire, les messages d’état et l’état de conformité.  

- Même si aucun client ne communique avec une passerelle de gestion cloud, certaines communications d’arrière-plan engendrent du trafic réseau entre la passerelle de gestion cloud et le site local.  

- Consultez le **Transfert de données sortantes (Go)** dans la console Configuration Manager. Pour plus d’informations, consultez [Surveiller les clients sur une passerelle de gestion cloud](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway).  

- Pour vous aider à déterminer les coûts potentiels, consultez les [détails de la tarification de la bande passante](https://azure.microsoft.com/pricing/details/bandwidth/). La tarification pour le transfert de données est à plusieurs niveaux. Plus votre utilisation augmente, moins vous payez par gigaoctet.  

- *À titre d’estimation seulement*, prévoyez environ 100 à 300 Mo par client par mois pour les clients Internet. L’estimation la plus basse est pour une configuration de client par défaut. L’estimation la plus haute est pour une configuration de client plus active. Votre utilisation réelle peut varier en fonction de la façon dont vous configurez les paramètres du client.  

   > [!NOTE]  
   > La réalisation d’autres actions, comme le déploiement de mises à jour logicielles ou d’applications, fait augmenter la quantité de données sortantes transférées depuis Azure.

#### <a name="content-storage"></a>Stockage de contenu

- Les clients Internet obtiennent gratuitement le contenu des mises à jour de logiciels Microsoft auprès de Windows Update. Ne distribuez pas des packages de mises à jour avec du contenu de mise à jour Microsoft sur un point de distribution cloud, sinon des frais de stockage et de sortie de données vous sont facturés.  

- Pour tout autre contenu nécessaire, comme des applications ou des mises à jour de logiciels tiers, vous devez distribuer sur un point de distribution cloud. Actuellement, la passerelle de gestion cloud prend en charge le point de distribution cloud seulement pour l’envoi de contenu à des clients.  

- Pour plus d’informations, consultez le coût d’utilisation des [points de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  

- À compter de la version 1806, une passerelle de gestion cloud peut également distribuer du contenu aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure. Pour plus d’informations, consultez [Modifier une passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#modify-a-cmg).<!--1358651-->  


#### <a name="other-costs"></a>Autres coûts

- Chaque service cloud a une adresse IP dynamique. Chaque passerelle de gestion cloud distincte utilise une nouvelle adresse IP dynamique. L’ajout de machines virtuelles supplémentaires par passerelle de gestion cloud n’augmente pas le nombre de ces adresses.  



## <a name="performance-and-scale"></a>Performances et évolutivité

Pour plus d’informations sur l’évolutivité de la passerelle de gestion cloud, consultez [Taille et échelle en chiffres](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg).

Les recommandations suivantes peuvent vous aider à améliorer les performances de la passerelle de gestion cloud :

- Si possible, configurez la passerelle CMG, le point de connexion CMG et le serveur de site Configuration Manager dans la même région pour réduire la latence du réseau.  

- Actuellement, la connexion entre le client Configuration Manager et la passerelle de gestion cloud ne tient pas compte de la région.  

- Pour un service à haute disponibilité, créez au moins deux services de passerelle de gestion cloud et deux points de connexion de passerelle de gestion cloud par site.  

- Faites évoluer la passerelle de gestion cloud pour prendre en charge plus de clients en ajoutant d’autres instances de machine virtuelle. L’équilibrage de charge Azure contrôle les connexions des clients au service.  

- Créez plusieurs points de connexion CMG pour répartir la charge entre ces points. La passerelle de gestion cloud distribue le trafic à ses points de connexion de passerelle de gestion cloud via un tourniquet (round-robin).  

- Quand la passerelle de gestion cloud subit une charge élevée en raison d’un dépassement du nombre de clients pris en charge, elle gère néanmoins les demandes, mais des délais sont possibles.  


> [!Note]  
> Si Configuration Manager n’a aucune limite matérielle quant au nombre de clients pour un point de connexion de passerelle de gestion cloud, Windows Server a une plage de ports dynamiques TCP maximale par défaut de 16 384. Si un site Configuration Manager gère plus de 16 384 clients avec un seul point de connexion de passerelle de gestion cloud, vous devez augmenter la limite de Windows Server. Tous les clients gèrent un canal pour les notifications des clients, qui détient un port ouvert sur le point de connexion de la passerelle de gestion cloud. Pour plus d’informations sur l’utilisation de la commande netsh pour augmenter cette limite, consultez [Article du Support Microsoft 929851](https://support.microsoft.com/help/929851).



## <a name="ports-and-data-flow"></a>Ports et flux de données

Vous n’avez pas besoin d’ouvrir des ports entrants sur votre réseau local. Le point de connexion du service et le point de connexion de la passerelle de gestion cloud lancent toutes les communications avec Azure et la passerelle de gestion cloud. Ces deux rôles de système de site doivent être en mesure de créer des connexions sortantes vers le cloud Microsoft. Le point de connexion du service déploie et surveille le service dans Azure : il doit donc être en mode en ligne. Le point de connexion de la passerelle de gestion cloud se connecte à la passerelle de gestion cloud pour gérer les communications entre la passerelle et les rôles de système de site locaux.

Le diagramme suivant est un flux de données conceptuel de base pour la passerelle de gestion cloud : ![Flux de données de passerelle de gestion cloud](media/cmg-data-flow.png)
   1. Le point de connexion du service se connecte à Azure via le port HTTPS 443. Il s’authentifie avec Azure AD ou avec le certificat de gestion Azure. Le point de connexion du service déploie la passerelle de gestion cloud dans Azure. La passerelle de gestion cloud crée le service cloud HTTPS en utilisant le certificat d’authentification serveur.  

   2. Le point de connexion de la passerelle de gestion cloud se connecte à la passerelle dans Azure via TCP-TLS ou HTTPS. Il laisse la connexion ouverte et crée le canal pour la communication bidirectionnelle à venir.   

   3. Le client se connecte à la passerelle de gestion cloud sur le port HTTPS 443. Il s’authentifie avec Azure AD ou avec le certificat d’authentification client.  

   4. La passerelle de gestion cloud transfère la communication client via la connexion existante au point de connexion de la passerelle de gestion cloud. Vous n’avez pas besoin d’ouvrir des ports de pare-feu entrants.  

   5. Le point de connexion de la passerelle de gestion cloud transfère la communication client au point de gestion local et au point de mise à jour logicielle.  

### <a name="required-ports"></a>Ports nécessaires
Ce tableau répertorie les ports et les protocoles réseau nécessaires. Le *client* est l’appareil qui lance la connexion, qui nécessite un port sortant. Le *serveur*  est l’appareil qui accepte la connexion, qui nécessite un port entrant. 

| Client  | Protocole | Port  | Serveur  | Description  |
|---------|---------|---------|---------|---------|
| point de connexion de service     | HTTPS | 443        | Azure        | Déploiement CMG |
| Point de connexion CMG     |  TCP-TLS | 10140-10155        | Service de passerelle de gestion cloud        | Protocole préféré pour créer le canal de passerelle de gestion cloud<sup>1</sup> |
| Point de connexion CMG     | HTTPS | 443        | Service de passerelle de gestion cloud       | Protocole de repli pour générer le canal de passerelle de gestion cloud sur une seule instance de machine virtuelle<sup>2</sup> |
| Point de connexion CMG     |  HTTPS   | 10124-10139     | Service de passerelle de gestion cloud       | Protocole de repli pour générer le canal de passerelle de gestion cloud sur deux ou plusieurs instances de machine virtuelle<sup>3</sup> |
| Client     |  HTTPS | 443         | CMG        | Communication client générale |
| Point de connexion CMG      | HTTPS ou HTTP | 443 ou 80         | Point de gestion<br>(version 1706 ou 1710) | Trafic local, le port dépend de la configuration du point de gestion |
| Point de connexion CMG      | HTTPS | 443      | Point de gestion<br>(version 1802) | Le trafic de local doit être sur HTTPS |
| Point de connexion CMG      | HTTPS ou HTTP | 443 ou 80         | Point de mise à jour logicielle | Trafic local, le port dépend de la configuration du point de mise à jour logicielle |

<sup>1</sup> Le point de connexion de la passerelle de gestion cloud tente d’abord d’établir une connexion TCP-TLS à long terme avec chaque instance de machine virtuelle de la passerelle. Il se connecte à la première instance de machine virtuelle sur le port 10140. La deuxième instance de machine virtuelle utilise le port 10141, jusqu’à la seizième sur le port 10155. Une connexion TCP-TLS offre les meilleures performances, mais elle ne prend pas en charge le proxy Internet. Si le point de connexion de la passerelle de gestion cloud ne peut pas se connecter via TCP-TLS, elle passe à l’alternative de secours HTTPS<sup>2</sup>.  

<sup>2</sup> Si le point de connexion de la passerelle de gestion cloud ne peut pas se connecter à la passerelle via TCP-TLS<sup>1</sup>, il se connecte à l’équilibreur de charge réseau Azure via HTTPS 443 pour une seule instance de machine virtuelle.  

<sup>3</sup> S’il existe plusieurs instances de machine virtuelle, le point de connexion de la passerelle de gestion cloud utilise le protocole HTTPS 10124 avec première instance de machine virtuelle, et non pas HTTPS 443. Il se connecte à la deuxième instance de machine virtuelle via HTTPS 10125, jusqu’à la seizième sur le port HTTPS 10139.


### <a name="internet-access-requirements"></a>Conditions requises pour l’accès Internet

Le système de site du point de connexion de la passerelle de gestion cloud prend en charge l’utilisation d’un proxy web. Pour plus d’informations sur la configuration de ce rôle pour un proxy, consultez [Prise en charge d’un serveur proxy](/sccm/core/plan-design/network/proxy-server-support#to-set-up-the-proxy-server-for-a-site-system-server). Le point de connexion de la passerelle de gestion cloud nécessite une connexion aux points de terminaison suivants :  

- Les points de terminaison Azure spécifiques sont différents pour chaque environnement, en fonction de la configuration. Configuration Manager stocke ces points de terminaison dans la base de données du site. Pour obtenir la liste des points de terminaison Azure, interrogez la table **AzureEnvironments** dans SQL Server.  

- ServiceManagementEndpoint (https://management.core.windows.net/)  

- StorageEndpoint (core.windows.net)  

- Pour la récupération du jeton Azure AD par la console Configuration Manager et le client : ActiveDirectoryEndpoint ()https://login.microsoftonline.com/)  

- Pour la découverte des utilisateurs Azure AD : point de terminaison du graphe AAD (https://graph.windows.net/)  



## <a name="next-steps"></a>Étapes suivantes

- [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Taille et scalabilité de la passerelle de gestion cloud en chiffres](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
- [Questions fréquentes (FAQ) sur la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Configurer la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
