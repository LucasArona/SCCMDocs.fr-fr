---
title: Forum aux questions sur le produit et les licences
titleSuffix: Configuration Manager
description: Trouvez des réponses aux questions courantes sur le produit et les licences pour System Center Configuration Manager.
ms.date: 04/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ee8d611f-aa0c-4efd-b0ad-dbd14d0a0623
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 781ffffac4367fb899c37c50492390a65244e17d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340305"
---
# <a name="frequently-asked-questions-for-configuration-manager-branches-and-licensing"></a>Foire aux questions sur les branches et la gestion des licences de Configuration Manager

 *S’applique à : System Center Configuration Manager (Current Branch), System Center Configuration Manager (Long-Term Servicing Branch)*

## <a name="summary"></a>Résumé
Cette FAQ répond à des questions courantes sur la gestion des licences des versions System Center Configuration Manager Current Branch et Long Term Servicing Branch (LTSB), disponibles par le biais des programmes de gestion des licences en volume Microsoft. Cet article n’a qu’une fonction informative. Il ne remplace ni n’annule aucune documentation sur la gestion des licences de System Center Configuration Manager. Pour plus d’informations, consultez la gestion des licences des produits [System Center 2016](https://www.microsoft.com/en-us/licensing/product-licensing/system-center-2016.aspx)<!-- this link doesn't work without some language code --> et les [Conditions des produits](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=53). Les Conditions des Produits décrivent les conditions d’utilisation de tous les produits Microsoft dans la gestion des licences en volume.

Pour plus d’informations sur les fonctionnalités de System Center Configuration Manager, consultez la [page produit](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).




## <a name="product-and-licensing-faq"></a>FAQ sur les produits et la gestion des licences

### <a name="bkmk_cb"></a>Qu’est-ce que Current Branch ?  
Il s’agit de la build prête pour la production de System Center Configuration Manager qui fournit un modèle de maintenance actif. Ce modèle de maintenance ressemble à l’expérience avec Windows 10 ou l’option d’installation de Windows Server 2016 Nano Server. Cette approche convient aux clients qui évoluent à une « cadence cloud » et souhaitent innover plus rapidement. Avec le modèle de maintenance Current Branch, les clients System Center Configuration Manager continuent de recevoir de nouvelles fonctionnalités. C’est pourquoi seuls les clients avec une Software Assurance active dans leurs licences System Center Configuration Manager, ou des droits d’abonnement équivalents, peuvent installer et utiliser l’option Current Branch de System Center Configuration Manager.


### <a name="bkmk_ltsb"></a> Qu’est-ce que Long Term Servicing Branch (LTSB) ?  
Long-Term Servicing Branch est une version de production de System Center Configuration Manager. Elle est conçue pour les clients qui autorisent l’expiration de leur Software Assurance ou de leurs droits d’abonnements équivalents. Par rapport à Current Branch, LTSB a des [fonctionnalités réduites](/sccm/core/understand/introduction-to-the-ltsb#features-that-are-not-available-in-the-ltsb-of-configuration-manager). Les clients qui autorisent l’expiration de Software Assurance ou des droits d’abonnement équivalents doivent désinstaller Current Branch de System Center Configuration Manager. Les clients dotés de droits de licence perpétuels sur System Center Configuration Manager peuvent ensuite installer et utiliser la build LTSB de la version de System Center Configuration Manager qui est en vigueur au moment de l’expiration.


### <a name="bkmk_licensing-acronyms"></a> J’ai vu les termes SA et L&SA dans le texte sur les licences. Que veulent dire ces acronymes dans System Center Configuration Manager ?    
SA (Software Assurance) et L&SA (Licence et Software Assurance) sont des options de licence qui accordent des droits d’utilisation de System Center Configuration Manager. SA est une option qui s’adresse à un client qui renouvelle la SA suite à un contrat précédent. L&SA est une option qui s’adresse à un client qui achète une nouvelle licence et la SA.
  - **Software Assurance (SA)**  : Les clients doivent avoir une SA active dans leurs licences System Center Configuration Manager, ou des droits d’abonnement équivalents, pour pouvoir installer et utiliser l’option Current Branch de System Center Configuration Manager.    

    - Même si la SA est facultative pour certains produits Microsoft, la seule façon d’obtenir les droits d’utiliser System Center Configuration Manager Current Branch est avec la SA *(ou des droits d’abonnement équivalents)*. Pour plus d’informations, consultez les [questions fréquentes (FAQ) sur la Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/FAQ-Software-Assurance.aspx).<!--this link doesn't work without some language code-->

  - **Microsoft License and Software Assurance (L&SA)**  : Les clients qui achètent de nouvelles licences pour System Center Configuration Manager doivent acquérir une L&SA (Licence et SA).   

    - La SA accorde les droits d’utilisation de Current Branch.

    - Si votre SA expire et que vous avez toujours une licence System Center Configuration Manager, vous ne pourrez plus utiliser Current Branch. Pour plus d’informations, consultez la question [Si ma SA expire et que j’avais une L&SA, que se passe-t-il ?](#bkmk_sa-expires)

Pour plus d’informations sur les offres de licences, consultez [Comment acheter](https://www.microsoft.com/en-us/licensing/licensing-programs) <!--this link doesn't work without some language code--> et [Termes du contrat de licence du produit](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=64).  


### <a name="bkmk_equiv-sub"></a> J’ai rencontré le terme « abonnement équivalent », de quels programmes est-il question ?   
Les abonnements équivalents font référence à des programmes comme [Enterprise Mobility + Security](http://www.microsoftvolumelicensing.com/ProductResults.aspx?doc=Product%20Terms,OST&fid=51) (EMS) ou [Microsoft 365 Entreprise](https://www.microsoft.com/microsoft-365/enterprise). Il peut y en avoir d’autres, mais ceux-ci sont les plus courants. Ils sont considérés dans les conditions des produits de gestion des licences en volume Microsoft comme des licences équivalentes à des licences de gestion.


### <a name="bkmk_ems-expires"></a> J’ai Enterprise Mobility + Security mais il a expiré, que dois-je faire ?  
EMS accorde les droits d’utilisation de System Center Configuration Manager (Current Branch et Long Term Servicing Branch). Après expiration de ces droits, vous n’aurez plus le droit d’utiliser de branches et devrez procéder à une désinstallation.  


### <a name="bkmk_sa-expires"></a> Si ma SA expire et que j’avais une L&SA, que se passe-t-il ?   
Si votre SA a expiré après le 1er octobre 2016, selon le programme dans le cadre duquel vous avez acquis la L&SA, vous pouvez conserver une licence perpétuelle pour utiliser LTSB (Long Term Servicing Branch). Si vous utilisez la version Current Branch, vous devez la désinstaller, puis installer LTSB. Il n’existe aucune prise en charge de la migration ni de la conversion vers LTSB à partir de Current Branch.

Si votre SA a expiré avant le 1er octobre 2016 et que vous avez conservé une licence perpétuelle pour System Center Configuration Manager, votre seule option pour continuer à l’utiliser consiste à installer et utiliser System Center 2012 R2 Configuration Manager et ses Service Packs disponibles. Vous deviez désinstaller Current Branch lors de l’expiration de votre SA et réinstaller cette version antérieure du produit. Il n’existe aucune prise en charge de la migration ni du passage à une version antérieure depuis System Center Configuration Manager Current Branch vers des versions précédentes de Configuration Manager.   


### <a name="bkmk_owncb"></a> Suis-je « propriétaire » de Current Branch ?   
Non. Vous bénéficiez d’une licence pour utiliser Current Branch pendant que vous avez une SA active. Par exemple, avec *L&SA*, quand la *SA* arrive à expiration, il ne vous reste plus que les droits *L (Licence)*, ce qui n’inclut pas les droits d’utilisation de Current Branch. Si votre L (Licence) fournit des droits perpétuels, vous pouvez utiliser LTSB (Long Term Servicing Branch) de System Center Configuration Manager (ou System Center 2012 R2 Configuration Manager si votre SA a expiré avant le 1er octobre 2016) à la place de Current Branch.


### <a name="bkmk_standalone"></a> Puis-je acheter System Center Configuration Manager autonome sans SA ?      
Non. La seule façon d’obtenir les droits d’utiliser System Center Configuration Manager est d’acquérir une licence avec SA ou via un abonnement équivalent. Il existe des programmes pour développeurs (comme MSDN) où System Center Configuration Manager est proposé à des fins de développement et de test, mais pas pour une utilisation en production.


### <a name="bkmk_update-rights"></a> Je vois des mises à jour pour System Center Configuration Manager proposées depuis ma console, comme la version 1610. Ai-je le droit de les installer ?   
Si vous avez une *SA* active, vous pouvez. Si vous n’avez pas de SA active, vous devez désinstaller Current Branch, puis installer LTSB de System Center Configuration Manager. LTSB ne reçoit pas de mises à jour pour les versions incrémentielles de System Center Configuration Manager, mais reçoit les mises à jour de sécurité selon le cycle de vie de prise en charge.


### <a name="bkmk_csp"></a> J’ai acheté EMS ou Microsoft 365 via un fournisseur de solutions cloud (CSP), ai-je les droits pour utiliser System Center Configuration Manager ? 
Oui, vous disposez des droits d’utilisation de System Center Configuration Manager pour gérer les clients couverts par la licence EMS. Commencez par télécharger et installer le [logiciel d’évaluation](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection). Contactez le support Microsoft pour obtenir la clé de licence.<!--issue472-->  


### <a name="bkmk_expiration-date"></a> Est-ce que la date de fin de mon abonnement est pareille qu’une date d’expiration d’une SA ?    
Si la *SA* ou votre abonnement est actif, vous disposez des droits d’utilisation pour System Center Configuration Manager Current Branch. Un abonnement actif équivaut à une *SA* active, mais pas à une *licence (« L »)* perpétuelle. Une fois votre abonnement terminé, vous devez désinstaller Current Branch et vous n’avez pas le droit d’utiliser LTSB.  

  
### <a name="bkmk_sql"></a> Quels sont les droits d’utilisation associés à la technologie SQL fournie avec System Center Configuration Manager ?    
Tous les produits System Center englobent la technologie SQL Server. Les conditions de gestion des licences Microsoft pour ces produits autorisent le client à utiliser la technologie SQL Server uniquement pour prendre en charge les composants de System Center. Les licences d’accès client SQL Server ne sont pas requises dans cet usage. 
 
Voici quelques exemples de droits d’utilisation approuvés pour les fonctionnalités SQL avec System Center Configuration Manager :
 - Rôle de base de données de site
 - Windows Server Update Services (WSUS) pour le rôle de point de mise à jour logicielle
 - SQL Server Reporting Services (SSRS) pour le rôle de point de rapport
 - Rôle de point de service de l'entrepôt de données
 - Réplicas de base de données pour les rôles de points de gestion
 - SQL Server AlwaysOn 

La licence SQL Server incluse avec System Center Configuration Manager prend en charge chacune des instances de SQL Server qui seront installées afin d’héberger une base de données pour Configuration Manager. Cependant, avec cette licence, seules les bases de données de Configuration Manager figurant dans la liste précédente peuvent s’exécuter sur ce serveur SQL Server. Si une base de données d’un autre produit Microsoft ou tiers partage le serveur SQL Server, il vous faudra une licence distincte pour cette instance de SQL Server. 
 <!-- sms500967 -->
