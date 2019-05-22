---
title: Configurer les classifications et les produits
titleSuffix: Configuration Manager
description: Suivez ces étapes pour configurer les classifications et les produits de mise à jour logicielle qui doivent être synchronisés dans la console Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 02/15/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.collection: M365-identity-device-management
ms.openlocfilehash: 747e66adb8f6ce0d013073463ee2472785d3bb70
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499993"
---
#  <a name="configure-classifications-and-products-to-synchronize"></a>Configurer les classifications et les produits à synchroniser  

*S’applique à : System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>  Utilisez la procédure de cette section uniquement sur le site de niveau supérieur.  

 Les métadonnées des mises à jour logicielles sont récupérées au cours du processus de synchronisation dans Configuration Manager selon les paramètres que vous spécifiez dans les propriétés du composant du point de mise à jour logicielle. Une fois que vous avez synchronisé les mises à jour logicielles pour la première fois, ou lorsque de nouveaux produits et classifications sont disponibles, vous devez accéder aux propriétés pour sélectionner les nouveaux éléments. Pour configurer des classifications et des produits à synchroniser, procédez comme suit.  

#### <a name="to-configure-classifications-and-products-to-synchronize"></a>Pour configurer des classifications et des produits à synchroniser  

1.  Dans la console **Configuration Manager**, accédez à **Administration** > **Configuration de site** > **Sites**.

2. Sélectionnez le site d’administration centrale ou le site principal autonome.  

3.  Sur l'onglet **Accueil** dans le groupe **Paramètres** , cliquez sur **Configurer les composants de site**, puis cliquez sur **Point de mise à jour logicielle**.

4.  Sous l'onglet **Classifications** , spécifiez les classifications de mise à jour logicielle pour lesquelles vous souhaitez synchroniser les mises à jour logicielles.  

    > [!NOTE]  
    >  Chaque mise à jour logicielle fait partie d'une classification particulière qui permet d'organiser les différents types de mises à jour. Pendant le processus de synchronisation, les métadonnées des mises à jour logicielles pour les classifications spécifiées sont synchronisées. Configuration Manager vous permet de synchroniser les mises à jour logicielles avec les classifications de mise à jour suivantes :  
    >   
    > - **Mises à jour critiques** : spécifie un correctif largement distribué, répondant à un problème spécifique qui concerne un bogue critique non lié à la sécurité.  
    > - **Mises à jour de définition** : spécifie une mise à jour de logiciel largement distribuée et fréquente qui contient des ajouts à la base de données de définition d’un produit.  
    > - **Feature Packs** : spécifie de nouvelles fonctionnalités de produit, d’abord distribuées en dehors d’une mise en production et généralement incluses dans la mise en production suivante du produit.  
    > - **Mises à jour de sécurité** : spécifie un correctif largement distribué, répondant à une vulnérabilité liée à la sécurité et propre au produit.  
    > - **Service Packs** : spécifie l’ensemble cumulé et testé de tous les correctifs logiciels, mises à jour de sécurité, mises à jour critiques et mises à jour qui s’appliquent à un produit. En outre, les Service Packs peuvent contenir des correctifs supplémentaires pour des problèmes trouvés en interne depuis la mise en production du produit.  
    > - **Outils** : spécifie des utilitaires ou des fonctionnalités permettant d’effectuer une ou plusieurs tâches.  
    > - **Correctifs cumulatifs ** : spécifie un ensemble cumulé et testé de correctifs logiciels, de mises à jour de sécurité, de mises à jour critiques et de mises à jour packagés ensemble de façon à en faciliter le déploiement. Les correctifs cumulatifs concernent généralement un domaine particulier, tel que la sécurité ou un composant de produit.  
    > - **Mises à jour** : spécifie un correctif largement distribué pour un problème spécifique. Une mise à jour concerne un bogue non critique qui n’est pas lié à la sécurité.  
    > - **Mises à niveau** : spécifie des mises à niveau de fonctions et fonctionnalités Windows 10. Vos sites et points de mise à jour logicielle doivent exécuter au moins WSUS 4.0 avec le [correctif 3095113](https://support.microsoft.com/kb/3095113) pour obtenir la classification de **mise à niveau**.    
    >       

    > [!NOTE]    
    > À compter de Configuration Manager version 1706, vous pouvez cocher la case **Inclure les mises à jour du microprogramme et des pilotes Microsoft Surface** pour synchroniser les pilotes Microsoft Surface.<!--1098490--> Tous les points de mise à jour logicielle doivent exécuter Windows Server 2016 pour synchroniser correctement les pilotes Surface. Si vous activez un point de mise à jour logicielle sur un ordinateur exécutant Windows Server 2012 après avoir activé les pilotes Surface, les résultats d’analyse pour les mises à jour du pilote ne sont pas exacts. Ainsi, les données de conformité affichées dans la console Configuration Manager et dans les rapports Configuration Manager ne sont pas correctes.  
    >  
    > Cette fonctionnalité a été introduite dans la version 1706 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1710, cette fonctionnalité n’est plus une fonctionnalité en préversion.  
    >  
    > Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

5.  Sous l'onglet **Produits** , spécifiez les produits pour lesquels vous souhaitez synchroniser les mises à jour logicielles, puis cliquez sur **Fermer**.  

    > [!NOTE]  
    >  Les métadonnées de chaque mise à jour logicielle définissent les produits auxquels elles s'appliquent. Un produit est une édition spécifique d’un système d’exploitation ou d’une application (par exemple, Windows Server 2012). Une famille de produits est le système de d'exploitation ou l'application de base d'où sont issus les produits individuels. Par exemple, Windows est une famille de produits dont Windows Server 2012 fait partie. Vous pouvez spécifier une famille de produits ou des produits distincts au sein d'une famille de produits. Plus le nombre de produits que vous sélectionnez est important, plus la durée de synchronisation des mises à jour logicielles est longue.  
    >   
    >  Quand des mises à jour logicielles s’appliquent à plusieurs produits et qu’au moins un de ces produits a été sélectionné pour une synchronisation, tous les autres produits apparaissent dans la console Configuration Manager, même s’ils n’ont pas été sélectionnés. Par exemple, si Windows Server 2012 est le seul système d’exploitation que vous avez sélectionné et qu’une mise à jour logicielle s’applique à Windows 8 et à Windows Server 2012, ces deux produits apparaissent dans la console Configuration Manager.  

    > [!IMPORTANT]  
    >  Configuration Manager stocke une liste de produits et de familles de produits que vous pouvez choisir quand vous installez le point de mise à jour logicielle pour la première fois. Tant que les mises à jour logicielles ne sont pas effectuées, les produits et familles de produits publiés après la publication de Configuration Manager risquent de ne pas pouvoir être sélectionnés. La synchronisation permet de mettre à jour la liste des produits et des familles de produits pouvant être sélectionnés.  

## <a name="next-steps"></a>Étapes suivantes
Démarrez la synchronisation des mises à jour logicielles pour récupérer les mises à jour logicielles en fonction des nouveaux critères. Pour plus d’informations, consultez [Synchroniser les mises à jour logicielles](synchronize-software-updates.md).
