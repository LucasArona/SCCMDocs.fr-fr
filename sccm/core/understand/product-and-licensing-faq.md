---
title: FAQ sur les produits et la gestion des licences
titleSuffix: Configuration Manager
description: Trouvez des réponses aux questions courantes sur le produit et les licences pour System Center Configuration Manager.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 01fa13c907b451a3539ca8169c3a04ebbaa1b92c
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145775"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Foire aux questions sur les branches et la gestion des licences de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch), System Center Configuration Manager (Long-Term Servicing Branch)*

Cette FAQ répond à des questions courantes sur la gestion des licences des versions Configuration Manager Current Branch et Long-Term Servicing Branch (LTSB), disponibles par le biais des programmes de gestion des licences en volume Microsoft. Cet article n’a qu’une fonction informative. Il ne remplace ni n’annule aucune documentation sur la gestion des licences de System Center Configuration Manager. Pour plus d’informations, consultez la gestion des licences des produits [System Center 2016](https://www.microsoft.com/en-us/licensing/product-licensing/system-center-2016.aspx)<!-- this link doesn't work without some language code --> et les [Termes des produits](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Les Conditions des Produits décrivent les conditions d’utilisation de tous les produits Microsoft dans la gestion des licences en volume.

Pour plus d’informations sur les fonctionnalités de Configuration Manager, consultez la [page produit](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).



### <a name="bkmk_cb"></a> Qu’est-ce que Current Branch ?  

Il s’agit du build prêt pour la production de Configuration Manager qui offre un modèle de service actif, similaire à l’expérience de Windows 10. Cette approche convient aux clients qui évoluent à une « cadence cloud » et souhaitent innover plus rapidement. Avec le modèle de service Current Branch, ils continuent de recevoir de nouvelles fonctionnalités. C’est pourquoi seuls les clients disposant d’une Software Assurance active dans leurs licences Configuration Manager, ou de droits d’abonnement équivalents, peuvent installer et utiliser la version Current Branch de Configuration Manager.


### <a name="bkmk_ltsb"></a> Qu’est-ce que Long-Term Servicing Branch (LTSB) ?  

LTSB est un build prêt pour la production de Configuration Manager, conçu pour les clients qui autorisent l’expiration de leur Software Assurance ou de leurs droits d’abonnements équivalents. LTSB offre des [fonctionnalités réduites](/sccm/core/understand/introduction-to-the-ltsb#features-that-are-not-available-in-the-ltsb-of-configuration-manager) par rapport à Current Branch. Les clients qui autorisent l’expiration de leur Software Assurance ou de leurs droits d’abonnement équivalents doivent désinstaller la version Current Branch de Configuration Manager. Ceux qui possèdent des droits de licence perpétuels sur Configuration Manager peuvent alors installer et utiliser le build LTSB de la version de Configuration Manager en vigueur au moment de l’expiration.


### <a name="bkmk_licensing-acronyms"></a> En matière de gestion des licences, que signifient les sigles *SA* et *L&SA* dans Configuration Manager ?    

**Software Assurance** (SA) et **Licence et Software Assurance** (L&SA) sont des options de licence qui accordent des droits d’utilisation de Configuration Manager. SA s’adresse aux clients qui renouvellent la SA suite à un contrat précédent. L&SA est une option qui s’adresse à un client qui achète une nouvelle licence et la SA.

- **Software Assurance (SA)** : les clients doivent avoir une SA active dans leurs licences Configuration Manager, ou des droits d’abonnement équivalents, pour pouvoir installer et utiliser l’option Current Branch de Configuration Manager.    

    - Même si la SA est facultative pour certains produits Microsoft, le seul moyen d’obtenir les droits d’utilisation de Configuration Manager Current Branch est de passer par la SA *ou des droits d’abonnement équivalents*. Pour plus d’informations, consultez les [FAQ sur Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/FAQ-Software-Assurance.aspx).<!--this link doesn't work without some language code-->

- **Microsoft License and Software Assurance (L&SA)** : les clients qui achètent de nouvelles licences Configuration Manager doivent acquérir une L&SA (Licence et SA).   

    - La SA accorde des droits d’utilisation de Current Branch.

    - Si votre SA expire alors que vous avez toujours une licence Configuration Manager, vous ne pourrez plus utiliser Current Branch. Pour plus d’informations, consultez la question [Si ma SA expire et que j’avais une L&SA, que se passe-t-il ?](#bkmk_sa-expires)

Pour plus d’informations sur les offres de licences, consultez [Comment acheter](https://www.microsoft.com/Licensing/licensing-programs/licensing-programs)<!--this link doesn't work without some language code--> et [Termes du contrat de licence du produit](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  


### <a name="bkmk_equiv-sub"></a> J’ai rencontré le terme « abonnement équivalent », de quels programmes est-il question ?   

Les abonnements équivalents font référence à des programmes comme [Enterprise Mobility + Security](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) ou [Microsoft 365 Entreprise](https://www.microsoft.com/microsoft-365/enterprise). Il peut y en avoir d’autres, mais ceux-ci sont les plus courants. Ils sont considérés dans les conditions des produits de gestion des licences en volume Microsoft comme des licences équivalentes à des licences de gestion.


### <a name="bkmk_ems-expires"></a> J’ai Enterprise Mobility + Security mais il a expiré, que dois-je faire ?  

EMS accorde des droits d’utilisation de Configuration Manager Current Branch et Long-Term Servicing Branch. Après expiration de ces droits, vous n’aurez plus le droit d’utiliser de branches et devrez procéder à une désinstallation.  


### <a name="bkmk_sa-expires"></a> Si ma SA expire et que j’avais une L&SA, que se passe-t-il ?   

Si votre SA a expiré après le 1er octobre 2016, vous pouvez conserver une licence perpétuelle pour utiliser LTSB selon le programme dans le cadre duquel vous avez acquis la L&SA. Si vous utilisez actuellement Current Branch, vous devez la désinstaller, puis installer LTSB. La migration et la conversion de Current Branch vers LTSB ne sont pas prises en charge.

Si votre SA a expiré avant le 1er octobre 2016 et que vous avez conservé une licence perpétuelle pour Configuration Manager, votre seule option pour continuer à y recourir consiste à installer et à utiliser System Center 2012 R2 Configuration Manager et ses Service Packs disponibles. Vous devez désinstaller Current Branch à l’expiration de votre SA et réinstaller cette version antérieure du produit. La migration et le passage de Configuration Manager Current Branch à des versions précédentes de Configuration Manager ne sont pas pris en charge.   

Si vous utilisez System Center Endpoint Protection et que votre SA expire, vous devez le désinstaller. System Center Endpoint Protection n’offre aucun droit *L (licence)* ni aucun droit perpétuel.<!--506238--> 


### <a name="bkmk_owncb"></a> Suis-je « propriétaire » de Current Branch ?   

Non. Vous bénéficiez d’une licence d’utilisation de Current Branch tant que vous disposez d’une SA active. Par exemple, avec *L&SA*, il ne vous reste plus que les droits *L (Licence)* quand la *SA* arrive à expiration, ce qui n’inclut pas les droits d’utilisation de Current Branch. Si votre L comporte des droits perpétuels, vous pouvez utiliser Configuration Manager LTSB au lieu de Current Branch. Si votre SA a expiré avant le 1er octobre 2016, vous pouvez également recourir à System Center 2012 R2 Configuration Manager.


### <a name="bkmk_standalone"></a> Puis-je acheter Configuration Manager en version autonome sans SA ?      

Non. Le seul moyen d’obtenir des droits d’utilisation de Configuration Manager est d’acquérir une licence avec SA ou par le biais d’un abonnement équivalent. Il existe des programmes pour les développeurs, comme MSDN, où Configuration Manager est proposé à des fins de développement et de test, mais pas pour une utilisation en production.


### <a name="bkmk_update-rights"></a> Je vois dans ma console des mises à jour disponibles pour Configuration Manager, comme la version 1810. Ai-je le droit de les installer ?   

Si vous avez une *SA* active, vous disposez des droits nécessaires. Dans le cas contraire, désinstallez Current Branch, puis installez la version LTSB de Configuration Manager. LTSB ne reçoit pas de mises à jour des versions incrémentielles de Configuration Manager, mais reçoit les mises à jour de sécurité selon le cycle de vie de support.


### <a name="bkmk_csp"></a> J’ai acheté EMS ou Microsoft 365 par le biais d’un fournisseur de solutions Cloud (CSP), ai-je les droits d’utilisation de Configuration Manager ? 

Oui. Vous disposez des droits d’utilisation de Configuration Manager pour gérer les clients couverts par la licence EMS. Commencez par télécharger et installer le [logiciel d’évaluation](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Contactez le support Microsoft pour obtenir la clé de licence.<!--issue472--> Demandez-lui de faire référence à l’ID d’article interne 4033838.<!-- SCCMDocs issue 493 --> 


### <a name="bkmk_expiration-date"></a> Est-ce que la date de fin de mon abonnement est pareille qu’une date d’expiration d’une SA ?    

Si votre *SA* ou votre abonnement est actif, vous disposez des droits d’utilisation de Configuration Manager Current Branch. Un abonnement actif équivaut à une *SA* active, mais pas à une *licence (« L »)* perpétuelle. À l’expiration de votre abonnement, désinstallez Current Branch. Vous ne disposez plus des droits d’utilisation de LTSB.  


### <a name="bkmk_sql"></a> Quels sont les droits d’utilisation associés à la technologie SQL fournie avec Configuration Manager ?    

Tous les produits System Center englobent la technologie SQL Server. Les conditions de gestion des licences Microsoft pour ces produits autorisent le client à utiliser la technologie SQL Server uniquement pour prendre en charge les composants de System Center. Les licences d’accès client SQL Server ne sont pas requises dans cet usage. 
 
Voici quelques exemples de droits d’utilisation approuvés pour les fonctionnalités SQL avec Configuration Manager :
 - Rôle de base de données de site
 - Windows Server Update Services (WSUS) pour le rôle de point de mise à jour logicielle
 - SQL Server Reporting Services (SSRS) pour le rôle de point de rapport
 - Rôle de point de service de l'entrepôt de données
 - Réplicas de base de données pour les rôles de points de gestion
 - SQL Server AlwaysOn 

La licence SQL Server incluse avec Configuration Manager prend en charge chacune des instances SQL Server installées dans le but d’héberger une base de données pour Configuration Manager. Cependant, avec cette licence, seules les bases de données de Configuration Manager figurant dans la liste précédente peuvent s’exécuter sur ce serveur SQL Server. Si une base de données d’un autre produit Microsoft ou tiers partage le serveur SQL Server, il vous faudra une licence distincte pour cette instance de SQL Server. 
 <!-- sms500967 -->


### <a name="bkmk_opmdm"></a> La gestion locale des appareils mobiles (MDM) exige-t-elle un abonnement Intune ?

Dans les versions 1806 et antérieures, un abonnement Microsoft Intune est nécessaire pour pouvoir utiliser la gestion MDM locale. Il ne sert qu’à effectuer le suivi des licences des appareils, et non à gérer ou à stocker des informations sur la gestion des appareils. Toutes les données de gestion sont stockées dans l’organisation concernée, selon l’infrastructure Configuration Manager locale.  

À compter de la version 1810, les nouveaux déploiements MDM locaux n’exigent plus de connexion Intune.<!--3607730, fka 1359124--> Votre organisation exige toujours des licences Intune pour utiliser cette fonctionnalité. À l’heure actuelle, il n’est pas possible de supprimer la connexion Intune des déploiements MDM locaux existants. Pour plus d’informations, consultez le [billet de blog du support Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

