---
title: Gérer les déploiements à haut risque
titleSuffix: Configuration Manager
description: Découvrez comment utiliser Configuration Manager afin de configurer les paramètres de site pour vérifier les déploiements et avertir les administrateurs s’ils créent un déploiement à haut risque.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab2203b948887a94577826573ccdf3376637eca2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386020"
---
# <a name="settings-to-manage-high-risk-deployments-for-configuration-manager"></a>Paramètres de gestion des déploiements à haut risque pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Avec Configuration Manager, vous pouvez configurer les paramètres de site pour la vérification des déploiements. Ces paramètres permettent d’avertir les administrateurs s’ils créent un déploiement de séquence de tâches à haut risque. Un déploiement à haut risque est :  

-   Un déploiement qui est installé automatiquement  

-   Un déploiement qui est susceptible d’entraîner des résultats indésirables  

Par exemple, une séquence de tâches dont l’objectif est **Obligatoire**, et qui déploie un système d’exploitation, est considérée comme une action à haut risque.  

Pour réduire le risque lié à un déploiement à haut risque indésirable, vous pouvez configurer des limites de taille dans ces paramètres de vérification de déploiement :  

-   **Limites de taille des regroupements** : quand vous créez un déploiement, masquez les regroupements qui contiennent plus de clients que votre limite.  

     -   **Taille par défaut** : quand vous créez un déploiement, ce paramètre masque les regroupements par défaut qui incluent plus de clients que cette limite. Vous pouvez toujours voir ces regroupements durant la création du déploiement, mais ils sont masqués par défaut. La valeur par défaut est **100**. Pour ignorer ce paramètre, entrez la valeur **0**.  

     -   **Taille maximale** : quand vous créez un déploiement, ce paramètre masque toujours les regroupements avec plus de clients que cette limite. Avec la valeur par défaut **0**, ce paramètre est ignoré. La valeur **Taille maximale** doit être supérieure à la valeur **Taille par défaut** .  

     Par exemple, vous affectez la valeur 100 à **Taille par défaut** et la valeur 1000 à **Taille maximale**. Quand vous créez un déploiement à haut risque, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements qui comprennent moins de 100 clients. Si vous désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site**, la fenêtre affiche les regroupements qui comprennent moins de 1 000 clients.  

-   **Regroupements avec des serveurs de système de site** : quand le regroupement cible comprend un ordinateur ayant un rôle de système de site, ce paramètre bloque les déploiements ou impose une vérification avant leur création. Quand un déploiement est bloqué, sélectionnez un autre regroupement qui répond aux critères de vérification du déploiement pour continuer à créer le déploiement.  

> [!NOTE]  
>  Les déploiements à haut risque sont toujours limités aux regroupements personnalisés, aux regroupements que vous créez et au regroupement **Ordinateurs inconnus** intégré. Quand vous créez un déploiement à haut risque, vous ne pouvez pas sélectionner un regroupement intégré, par exemple **Tous les systèmes**.  

### <a name="configure-deployment-verification-for-a-site"></a>Configurer la vérification d’un déploiement pour un site  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, sélectionnez **Sites**, puis sélectionnez le site principal à configurer.  

2.  Cliquez dans le ruban sur **Propriétés**, puis accédez à l’onglet **Vérification du déploiement**.  

3.  Après avoir défini les configurations à utiliser, cliquez sur **OK** pour enregistrer la configuration.  


### <a name="see-also"></a>Voir aussi  
 [Configurer des sites et des hiérarchies](/sccm/core/servers/deploy/configure/configure-sites-and-hierarchies)
