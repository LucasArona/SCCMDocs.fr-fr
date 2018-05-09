---
title: Questions fréquentes (FAQ) concernant la passerelle de gestion cloud (CMG, Cloud Management Gateway)
description: Utilisez cet article pour répondre aux questions fréquemment posées concernant la passerelle de gestion cloud
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: 3b178ce27b91701d52d5ea350de85216e1250442
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Questions fréquentes (FAQ) sur la passerelle de gestion cloud

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article répond aux questions que vous vous posez fréquemment concernant la passerelle de gestion cloud (CMG, Cloud Management Gateway). Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="frequently-asked-questions"></a>Forum aux questions

### <a name="what-certificates-do-i-need"></a>De quels certificats ai-je besoin ?

Pour des informations plus détaillées, consultez [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).


### <a name="do-i-need-azure-expressroute"></a>Ai-je besoin d’Azure ExpressRoute ?

[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) vous permet d’étendre votre réseau local dans Microsoft Cloud. ExpressRoute, ou d’autres connexions de réseau virtuel du même type, ne sont pas exigés pour la passerelle de gestion cloud Configuration Manager. La conception de la passerelle de gestion cloud permet aux clients Internet de communiquer via le service Azure avec des systèmes de site locaux sans aucune configuration réseau supplémentaire. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

Si votre organisation utilise ExpressRoute, une bonne pratique de sécurité consiste à isoler l’abonnement Azure pour la passerelle de gestion cloud. Cette configuration garantit que le service de passerelle de gestion cloud n’est pas connecté par inadvertance de cette manière. Pour plus d’informations, consultez [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway).


### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Ai-je besoin d’assurer la maintenance des machines virtuelles Azure ?

Aucune maintenance n’est nécessaire. La conception de la passerelle de gestion cloud utilise Azure PaaS (Platform as a Service). Configuration Manager utilise l’abonnement que vous fournissez pour créer les machines virtuelles, le stockage et le réseau nécessaires. Azure sécurise et met à jour les machines virtuelles. Ces machines virtuelles ne font pas partie de votre environnement local, comme c’est le cas avec IaaS (Infrastructure as a Service). La passerelle de gestion cloud est un service PaaS qui étend votre environnement Configuration Manager dans le cloud. 


### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>J’utilise déjà la gestion du client basée sur Internet (IBCM, Internet-Based Client Management). Si j’ajoute la passerelle de gestion cloud (CMG), comment se comportent les clients ?

Si vous avez déjà déployé la [gestion du client basée sur Internet ](/sccm/core/clients/manage/plan-internet-based-client-management) (IBCM), vous pouvez également déployer la passerelle de gestion cloud. Les clients reçoivent la stratégie pour les deux services. Quand ils se déplacent et utilisent Internet, ils sélectionnent et utilisent de façon aléatoire l’un de ces services Internet.


## <a name="next-steps"></a>Étapes suivantes

- [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurer la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
- [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
- [Taille et scalabilité de la passerelle de gestion cloud en chiffres](/sccm/core/plan-design/configs/size-and-scale-numbers#bkmk_cmg)