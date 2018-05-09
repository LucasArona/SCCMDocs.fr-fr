---
title: Bonnes pratiques concernant les mises à jour logicielles
titleSuffix: Configuration Manager
description: Adoptez ces bonnes pratiques pour les mises à jour logicielles dans System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/06/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 0604c75aedfea5d82bd7d274c4a43edccb497f1e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>Bonnes pratiques concernant les mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique indique les bonnes pratiques à suivre pour les mises à jour logicielles dans System Center Configuration Manager. Nous distinguons ci-dessous les bonnes pratiques liées à l'installation initiale, d'une part, et les bonnes pratiques liées aux opérations courantes, d'autre part.  

## <a name="installation-best-practices"></a>Bonnes pratiques concernant l’installation  
 Suivez les bonnes pratiques ci-dessous quand vous installez des mises à jour logicielles dans Configuration Manager.  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>Utiliser une base de données WSUS partagée pour les points de mise à jour logicielle  
 Lorsque vous installez plusieurs points de mise à jour logicielle sur un site principal, utilisez la même base de données WSUS pour chaque point de mise à jour logicielle d'une même forêt Active Directory. Lorsqu'un client bascule sur un autre point de mise à jour logicielle, les performances du client et du réseau peuvent s'en trouver ralenties. En partageant la même base de données, vous réduisez considérablement l'impact de ce basculement sur les performances. Lorsqu'un client bascule sur un nouveau point de mise à jour logicielle qui utilise la même base de données que l'ancien point de mise à jour logicielle, il se peut qu'une analyse différentielle soit lancée, mais celle-ci sera beaucoup plus restreinte que celle qui aurait lieu si le serveur WSUS avait sa propre base de données.  

> [!IMPORTANT]  
>  Vous devez également partager les dossiers de contenu WSUS locaux quand vous utilisez une base de données WSUS partagée pour les points de mise à jour logicielle.  

 Pour plus d’informations sur le basculement de point de mise à jour logicielle, consultez la section [Basculement de point de mise à jour logicielle](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching) dans la rubrique [Planifier les mises à jour logicielles dans System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md).  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Lorsque Configuration Manager et WSUS utilisent le même serveur SQL Server, l'un doit utiliser une instance nommée, et l'autre l'instance par défaut de SQL Server  
 Quand les bases de données Configuration Manager et WSUS utilisent le même serveur SQL Server et partagent la même instance de SQL Server, il est difficile de déterminer quelle application utilise quelles ressources. Il est plus facile de dépanner et de diagnostiquer les éventuels problèmes d’utilisation de ressources de chaque application si Configuration Manager et WSUS utilisent différentes instances de SQL Server.  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>Spécifier le paramètre « Stocker les mises à jour localement » pour l'installation de WSUS  
 Lorsque vous installez WSUS, sélectionnez le paramètre **Stocker les mises à jour localement** . Lorsque ce paramètre est sélectionné, les termes du contrat de licence relatif aux mises à jour logicielles sont téléchargés au cours du processus de synchronisation et stockés sur le disque dur local du serveur WSUS. Si ce paramètre n'est pas sélectionné, il se peut que l'analyse de la conformité des mises à jour logicielles pour les mises à jour comportant un contrat de licence échoue sur les ordinateurs clients. Lorsque vous installez le point de mise à jour logicielle, toutes les 60 minutes (intervalle par défaut), le Gestionnaire de synchronisation WSUS vérifie que ce paramètre est activé.  

## <a name="operational-best-practices"></a>Bonnes pratiques concernant le fonctionnement  
 Suivez les bonnes pratiques ci-dessous lorsque vous utilisez des mises à jour logicielles :  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>Limiter les mises à jour logicielles à 1 000 dans un déploiement de mises à jour logicielles unique  
 Vous devez limiter le nombre de mises à jour logicielles à 1 000 pour chaque déploiement de mises à jour logicielles. À la création d'une règle de déploiement automatique, vérifiez que les critères spécifiés n'entraînent pas plus de 1 000 mises à jour logicielles. Lorsque vous déployez manuellement des mises à jour logicielles, ne sélectionnez pas plus de 1 000 mises à jour à déployer.  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>Créer un groupe de mises à jour logicielles chaque fois qu’une règle de déploiement automatique s’exécute pour « Patch Tuesday » et pour un déploiement général  
 La limite pour les mises à jour logicielles dans un déploiement de mises à jour logicielles est de 1 000. Lorsque vous créez une règle de déploiement automatique, vous spécifiez s'il faut utiliser un groupe de mises à jour existant ou en créer un à chaque exécution de la règle. Si vous spécifiez dans une règle de déploiement automatique des critères entraînant plusieurs mises à jour logicielles et que la règle est exécutée à intervalle régulier, indiquez que vous souhaitez créer un nouveau groupe de mises à jour logicielles à chaque exécution de la règle. La limite de 1000 mises à jour logicielles par déploiement ne pourra ainsi pas être dépassée.  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Utiliser un groupe de mises à jour logicielles existant pour les règles de déploiement automatique des mises à jour de définitions Endpoint Protection  
 Utilisez toujours un groupe de mises à jour logicielles existant lorsque vous appliquez une règle de déploiement automatique pour déployer des mises à jour de définitions Endpoint Protection fréquemment. Sinon, au fil du temps, des centaines de groupes de mises à jour logicielles risquent d'être créés. Généralement, les éditeurs de mises à jour de définitions configurent ces mises à jour de telle sorte qu'elles expirent lorsqu'elles sont remplacées par quatre mises à jour plus récentes. Ainsi, le groupe de mises à jour logicielles créé par la règle de déploiement automatique ne contiendra jamais plus de quatre mises à jour de définitions publiées par l'éditeur en question : une active et trois remplacées.  

## <a name="see-also"></a>Voir aussi  
 [Planifier les mises à jour logicielles dans System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md)
