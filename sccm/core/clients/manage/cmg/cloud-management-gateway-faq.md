---
title: Questions fréquentes (FAQ) concernant la passerelle de gestion cloud (CMG, Cloud Management Gateway)
description: Utilisez cet article pour répondre aux questions fréquemment posées concernant la passerelle de gestion cloud
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcc535c007fc081d2597e5c6dafc159ed1176f39
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156870"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Questions fréquentes (FAQ) sur la passerelle de gestion cloud

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article répond aux questions que vous vous posez fréquemment concernant la passerelle de gestion cloud (CMG, Cloud Management Gateway). Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Forum aux questions

### <a name="what-certificates-do-i-need"></a>De quels certificats ai-je besoin ?

Pour des informations plus détaillées, consultez [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>Ai-je besoin d’Azure ExpressRoute ?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) vous permet d’étendre votre réseau local dans Microsoft Cloud. ExpressRoute, ou d’autres connexions de réseau virtuel du même type, ne sont pas nécessaires pour la passerelle de gestion cloud Configuration Manager. La conception de la passerelle de gestion cloud permet aux clients Internet de communiquer via le service Azure avec des systèmes de site locaux sans aucune configuration réseau supplémentaire. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

Si votre organisation utilise ExpressRoute, une bonne pratique de sécurité consiste à isoler l’abonnement Azure pour la passerelle de gestion cloud. Cette configuration garantit que le service de passerelle de gestion cloud n’est pas connecté par inadvertance de cette manière. Pour plus d’informations, consultez [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Ai-je besoin d’assurer la maintenance des machines virtuelles Azure ?

Aucune maintenance n’est nécessaire. La conception de la passerelle de gestion cloud utilise Azure PaaS (Platform as a Service). Configuration Manager utilise l’abonnement que vous fournissez pour créer les machines virtuelles, le stockage et le réseau nécessaires. Azure sécurise et met à jour les machines virtuelles. Ces machines virtuelles ne font pas partie de votre environnement local, comme c’est le cas avec IaaS (Infrastructure as a Service). La passerelle de gestion cloud est un service PaaS qui étend votre environnement Configuration Manager dans le cloud. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>J’utilise déjà la gestion du client basée sur Internet (IBCM, Internet-Based Client Management). Si j’ajoute la passerelle de gestion cloud (CMG), comment se comportent les clients ?

Si vous avez déjà déployé la [gestion du client basée sur Internet ](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), vous pouvez également déployer la passerelle de gestion cloud. Les clients reçoivent la stratégie pour les deux services. Quand ils se déplacent et utilisent Internet, ils sélectionnent et utilisent de façon aléatoire l’un de ces services Internet.


### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-subscription-as-the-subscription-that-hosts-the-cmg-cloud-service"></a>Les comptes d’utilisateurs doivent-ils être dans le même abonnement Azure que celui qui héberge le service cloud de passerelle de gestion cloud ?
<!--SCCMDocs-pr issue #2873--> Si votre environnement a plusieurs abonnements, vous pouvez déployer la passerelle de gestion cloud dans n’importe quel abonnement pouvant héberger des services cloud Azure. 

Cette question est courante dans les scénarios suivants :  

- Quand vous avez des environnements Active Directory et Azure AD de test et de production distincts, mais un seul abonnement d’hébergement Azure centralisé  

- Votre utilisation d’Azure a augmenté naturellement pour différentes équipes  

Quand vous utilisez un déploiement Resource Manager, intégrez le locataire Azure AD associé. Cette connexion permet à Configuration Manager de s’authentifier auprès d’Azure pour créer, déployer et gérer la passerelle de gestion cloud.  

Si vous utilisez l’authentification Azure AD pour les utilisateurs et les appareils gérés via la passerelle de gestion cloud, intégrez ce locataire Azure AD. Pour plus d’informations sur les services Azure pour la gestion cloud, consultez [Configurer les services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Quand vous intégrez chaque locataire Azure AD, une même passerelle de gestion cloud peut fournir l’authentification Azure AD pour plusieurs locataires, quel que soit l’emplacement d’hébergement.



## <a name="next-steps"></a>Étapes suivantes

- [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurer la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Taille et scalabilité de la passerelle de gestion cloud en chiffres](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)
