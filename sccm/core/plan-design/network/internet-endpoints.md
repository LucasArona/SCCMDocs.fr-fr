---
title: Conditions requises pour l’accès Internet
titleSuffix: Configuration Manager
description: En savoir plus sur les points de terminaison Internet pour bénéficier de toutes les fonctionnalités de Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f5ed06951fab313a4a1453864ffefb963cc4d8e9
ms.sourcegitcommit: 20bbb870baf624c7809d3972f2d09a8d2df79cda
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/08/2019
ms.locfileid: "67623266"
---
# <a name="internet-access-requirements"></a>Conditions requises pour l’accès Internet

Certaines fonctionnalités de Configuration Manager reposent sur la connectivité Internet pour être complètes. Si votre organisation restreint la communication réseau avec Internet à l’aide d’un appareil pare-feu ou proxy, veillez à autoriser ces points de terminaison.

<!-- SCCMDocs-pr #3403 -->

## <a name="bkmk_scp"></a> Point de connexion de service

Ces configurations s’appliquent à l’ordinateur qui héberge le point de connexion de service et les éventuels pare-feu entre cet ordinateur et internet. Les deux doivent autoriser les communications via le port sortant **TCP 443** pour HTTPS et le port sortant **TCP 80** HTTP vers les emplacements Internet suivants.

Le point de connexion de service prend en charge l’utilisation d’un proxy web (avec ou sans authentification) pour utiliser ces emplacements. Pour plus d’informations, consultez [Prise en charge des serveurs proxy](/sccm/core/plan-design/network/proxy-server-support).

Pour plus d’informations sur le point de connexion de service, consultez [À propos du point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point).

> [!TIP]  
> Le point de connexion de service utilise le service Microsoft Intune lorsqu’il se connecte à `go.microsoft.com` ou `manage.microsoft.com`. Un problème est connu sur le connecteur Intune qui rencontre une défaillance de connectivité si le certificat racine Baltimore CyberTrust n’est pas installé, a expiré ou est endommagé sur le point de connexion de service. Pour plus d’informations, consultez [KB 3187516 : le point de connexion de service ne télécharge pas les mises à jour](https://support.microsoft.com/help/3187516).  

### <a name="updates-and-servicing"></a>Mises à jour et maintenance

Pour plus d’informations sur cette fonction, consultez [Mises à jour et maintenance pour Configuration Manager](/sccm/core/servers/manage/updates).

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### <a name="microsoft-intune"></a>Microsoft Intune

Pour plus d’informations sur cette fonction, consultez [MDM hybride avec Configuration Manager et Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

### <a name="windows-10-servicing"></a>Maintenance de Windows 10

Pour plus d’informations sur cette fonction, consultez [Gérer Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### <a name="azure-services"></a>Services Azure

Pour plus d’informations sur cette fonction, consultez l’article [Configurer les services Azure à utiliser avec Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).

- `management.azure.com`  


## <a name="co-management"></a>Cogestion

Si vous inscrivez des appareils Windows 10 à Microsoft Intune pour la cogestion, assurez-vous que ces appareils peuvent accéder aux points de terminaison requis par Intune. Pour plus d'informations, consultez [Points de terminaison réseau pour les partenaires Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).


## <a name="bkmk_cloud"></a> Services cloud

<!-- SCCMDocs-pr #3402 -->

Cette section traite des fonctionnalités suivantes :

- Passerelle de gestion cloud (CMG)
- Point de distribution cloud (CDP)
- Azure Active Directory (Azure AD)
- Découverte basée sur Azure Active Directory

Pour le déploiement du service CMG/CDP, le **point de connexion de service** doit pouvoir d’accéder à :

- Les points de terminaison Azure spécifiques sont différents pour chaque environnement, en fonction de la configuration. Configuration Manager stocke ces points de terminaison dans la base de données du site. Pour obtenir la liste des points de terminaison Azure, interrogez la table **AzureEnvironments** dans SQL Server.  

Le **point de connexion CMG** doit pouvoir accéder aux points de terminaison service suivants :

- ServiceManagementEndpoint : `https://management.core.windows.net/`  

- StorageEndpoint : `blob.core.windows.net` et `table.core.windows.net`

Pour la récupération du jeton Azure Active Directory par la **console Configuration Manager** et par le **client** :

- ActiveDirectoryEndpoint `https://login.microsoftonline.com/`  

Pour la détection d’utilisateurs Azure AD, le **point de connexion de service** doit pouvoir accéder à :

- Version 1810 et versions antérieures : Point de terminaison Azure AD Graph `https://graph.windows.net/`  

- Version 1902 et versions ultérieures : Point de terminaison Microsoft Graph `https://graph.microsoft.com/`

Le système de site du point de connexion de la passerelle de gestion cloud du point de gestion cloud (CMG) prend en charge l’utilisation d’un proxy web. Pour plus d’informations sur la configuration de ce rôle pour un proxy, consultez [Prise en charge d’un serveur proxy](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). Le point de connexion CMG a uniquement besoin de se connecter aux points de terminaison de service de la passerelle de gestion cloud. Il n’a pas besoin d’accéder à d’autres points de terminaison Azure.

Pour plus d’informations sur la passerelle de gestion cloud, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="bkmk_sum"></a> Mises à jour logicielles

Autoriser le point de mise à jour logicielle actif à accéder aux points de terminaison suivants afin que WSUS et les mises à jour automatiques puissent communiquer avec le service de cloud Microsoft Update :  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `http://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

Pour plus d’informations sur les mises à jour logicielles, consultez [Planifier les mises à jour logicielles](/sccm/sum/plan-design/plan-for-software-updates).

### <a name="intranet-firewall"></a>Pare-feu Intranet

Vous devrez peut-être ajouter des points de terminaison à un pare-feu situé entre les deux systèmes de site dans les cas suivants :

- Si les sites enfants ont un point de mise à jour logicielle
- S’il existe un point de mise à jour logicielle actif distant basé sur Internet sur un site

#### <a name="software-update-point-on-the-child-site"></a>Point de mise à jour logicielle sur le site enfant

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  


## <a name="manage-office-365"></a>Gérer Office 365

Si vous utilisez Configuration Manager pour déployer et mettre à jour d’Office 365, autorisez les points de terminaison suivants :

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` pour synchroniser le point de mise à jour logicielle pour les mises à jour du client Office 365

- `config.office.com` pour créer des configurations personnalisées pour les déploiements d’Office 365


## <a name="configuration-manager-console"></a>Console Configuration Manager

Les ordinateurs avec la console Configuration Manager requièrent un accès aux points de terminaison Internet suivants pour des fonctionnalités spécifiques :

### <a name="in-console-feedback"></a>Commentaires dans la console

- `http://petrol.office.microsoft.com`

Pour plus d’informations sur cette fonctionnalité, consultez [Commentaires produit](/sccm/core/understand/find-help#product-feedback).

### <a name="community-workspace-documentation-node"></a>Espace de travail Communauté, nœud de documentation

- `https://aka.ms`

- `https://raw.githubusercontent.com`

Pour plus d’informations sur ce nœud de console, consultez [Utilisation de la console Configuration Manager](/sccm/core/servers/manage/admin-console).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### <a name="monitoring-workspace-site-hierarchy-node"></a>Espace de travail de surveillance, nœud de hiérarchie de site

Si vous utilisez la **vue géographique**, autorisez l’accès au point de terminaison suivant :

- `http://maps.bing.com`


## <a name="desktop-analytics"></a>Analyses du bureau

Pour plus d’informations sur les points de terminaison requis pour le service de cloud d’Analytique du bureau, consultez [Activer le partage de données](/sccm/desktop-analytics/enable-data-sharing#endpoints).


## <a name="microsoft-public-ip-addresses"></a>Adresses IP publiques Microsoft

Pour plus d’informations sur les plages d’adresses IP Microsoft, consultez [Espace IP public Microsoft](https://www.microsoft.com/download/details.aspx?id=53602). Ces adresses se mettent à jour régulièrement. Il n’existe aucune granularité par service, n’importe quelle adresse IP de ces plages peut être utilisée.


## <a name="see-also"></a>Voir aussi

- [Ports utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/ports)

- [Prise en charge du serveur proxy dans Configuration Manager](/sccm/core/plan-design/network/proxy-server-support)
