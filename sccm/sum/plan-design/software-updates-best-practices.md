---
title: Bonnes pratiques concernant les mises à jour logicielles
titleSuffix: Configuration Manager
description: Utilisez ces bonnes pratiques pour les mises à jour logicielles dans Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.collection: M365-identity-device-management
ms.openlocfilehash: 579ecbfc5c085ebca2fe7e8402da9b5cb1507ff1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496180"
---
# <a name="best-practices-for-software-updates-in-configuration-manager"></a>Bonnes pratiques pour les mises à jour logicielles dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article inclut des bonnes pratiques pour les mises à jour logicielles dans Configuration Manager. Nous distinguons ci-dessous les bonnes pratiques liées à l’installation initiale, d’une part, de celles liées aux opérations courantes, d’autre part.  



## <a name="bkmk_install"></a> Bonnes pratiques concernant l’installation  

Suivez les bonnes pratiques ci-dessous quand vous installez des mises à jour logicielles dans Configuration Manager.  


### <a name="bkmk_shared-susdb"></a> Utiliser une base de données WSUS partagée pour les points de mise à jour logicielle  

Lorsque vous installez plusieurs points de mise à jour logicielle sur un site principal, utilisez la même base de données WSUS pour chaque point de mise à jour logicielle d'une même forêt Active Directory. Si vous partagez la même base de données, cela permet d’atténuer considérablement, sans l’éliminer entièrement, l’impact sur les performances du client et du réseau, lequel impact peut se produire quand les clients basculent vers un nouveau point de mise à jour logicielle. Une analyse delta se produit quand même lorsqu’un client bascule vers un nouveau point de mise à jour logicielle qui partage une base de données avec l’ancien point de mise à jour logicielle, mais il s’agit d’une analyse beaucoup plus petite que celle qui se produirait si le serveur WSUS possède sa propre base de données. Pour plus d’informations sur les basculements de point de mise à jour logicielle, consultez [Basculement de point de mise à jour logicielle](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

> [!IMPORTANT]  
>  En outre, partagez les dossiers de contenu WSUS locaux quand vous utilisez une base de données WSUS partagée pour les points de mise à jour logicielle.  

Pour plus d’informations sur le partage de la base de données WSUS, consultez les billets de blog suivants :  

- [Guide pratique pour implémenter une base de données SUS partagée pour les points de mise à jour logicielle Configuration Manager](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/How-to-implement-a-shared-SUSDB-for-Configuration-Manager/ba-p/274103)  

- [Observations sur le partage par plusieurs instances WSUS d’une base de données de contenu dans le cadre de l’utilisation de System Center Configuration Manager](https://blogs.technet.microsoft.com/wsus/2014/03/22/considerations-for-multiple-wsus-instances-sharing-a-content-database-when-using-system-center-configuration-manager-but-without-network-load-balancing-nlb/)  


### <a name="bkmk_sql-instance"></a> Quand Configuration Manager et WSUS utilisent le même serveur SQL Server, l’un doit utiliser une instance nommée, et l’autre l’instance par défaut  

Quand les bases de données Configuration Manager et WSUS partagent la même instance de SQL Server, il est difficile de déterminer quelle application utilise quelles ressources. Utilisez différentes instances de SQL Server pour Configuration Manager et WSUS. Cette configuration permet de dépanner et de diagnostiquer plus facilement les éventuels problèmes d’utilisation de ressources de chaque application.  


### <a name="bkmk_store-local"></a> Spécifier le paramètre « Stocker les mises à jour localement »  

Quand vous installez WSUS, sélectionnez le paramètre **Stocker les mises à jour localement**. Grâce à ce paramètre, le serveur WSUS télécharge les termes du contrat de licence qui sont associés aux mises à jour logicielles. Il télécharge les termes du contrat pendant le processus de synchronisation et les stocke sur le disque dur local du serveur WSUS. Si vous ne sélectionnez pas ce paramètre, il se peut que l’analyse de la conformité des mises à jour logicielles comportant un contrat de licence échoue sur les ordinateurs clients. Le composant **Gestionnaire de synchronisation WSUS** du point de mise à jour logicielle vérifie, toutes les 60 minutes (intervalle par défaut), que ce paramètre est activé.  



## <a name="bkmk_operation"></a> Bonnes pratiques concernant le fonctionnement  

Suivez les bonnes pratiques ci-dessous lorsque vous utilisez des mises à jour logicielles :  


### <a name="bkmk_object-limit"></a> Limiter les mises à jour logicielles à 1 000 dans un déploiement de mises à jour logicielles unique  

Limitez le nombre de mises à jour logicielles à 1 000 dans chaque déploiement de mises à jour logicielles. Quand vous créez une règle de déploiement automatique, vérifiez que les critères spécifiés n’entraînent pas plus de 1 000 mises à jour logicielles. Si vous déployez manuellement des mises à jour logicielles, ne sélectionnez pas plus de 1 000 mises à jour.  


### <a name="bkmk_new-group"></a> Créer un groupe de mises à jour logicielles chaque fois qu’une règle de déploiement automatique s’exécute pour « Patch Tuesday » et pour des déploiements généraux  

Il existe une limite de 1 000 mises à jour logicielles dans un déploiement. Quand vous créez une règle de déploiement automatique, vous spécifiez s’il faut utiliser un groupe de mises à jour existant ou en créer un à chaque exécution de la règle. Si vous spécifiez dans une règle de déploiement automatique des critères entraînant plusieurs mises à jour logicielles et que la règle est exécutée à intervalle régulier, créez un groupe de mises à jour logicielles à chaque exécution de la règle. Ainsi, la limite de 1 000 mises à jour logicielles par déploiement ne peut pas être dépassée.  


### <a name="bkmk_same-group"></a> Utiliser un groupe de mises à jour logicielles existant pour les règles de déploiement automatique des mises à jour de définitions Endpoint Protection  

Quand vous utilisez une règle de déploiement automatique pour déployer des mises à jour de définitions Endpoint Protection fréquemment, utilisez toujours un groupe de mises à jour logicielles existant. Sinon, au fil du temps, la règle de déploiement automatique risque de créer des centaines de groupes de mises à jour logicielles. Les éditeurs de mises à jour de définitions configurent généralement ces mises à jour de telle sorte qu’elles expirent quand elles sont remplacées par quatre mises à jour plus récentes. Ainsi, le groupe de mises à jour logicielles créé par la règle de déploiement automatique ne contient jamais plus de quatre mises à jour de définitions publiées par l’éditeur en question : une active et trois remplacées.  



## <a name="see-also"></a>Voir aussi  
 [Planifier les mises à jour logicielles](/sccm/sum/plan-design/plan-for-software-updates)
