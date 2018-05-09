---
title: Gérer les déploiements à haut risque
titleSuffix: Configuration Manager
description: Apprenez à configurer les paramètres du site dans System Center Configuration Manager pour avertir les administrateurs s’ils créent un déploiement à haut risque.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44c7c805baedde820bc230dc25a3186762ecc8dc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>Paramètres pour gérer les déploiements à haut risque pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Avec System Center Configuration Manager, vous pouvez configurer les paramètres du site pour avertir les administrateurs s’ils créent un déploiement de séquence de tâches à haut risque. Un déploiement à haut risque est :  

-   Un déploiement qui est installé automatiquement  

-   Un déploiement qui est susceptible d’entraîner des résultats indésirables  

 Par exemple, une séquence de tâches dont l’objectif est **Obligatoire** qui déploie un système d’exploitation est considérée comme étant à haut risque.  

 Pour réduire le risque lié à un déploiement à haut risque indésirable, vous pouvez configurer des limites de taille dans ces paramètres de vérification de déploiement :  

-   **Limites de taille des regroupements** : masquez les regroupements contenant plus de clients que votre limite quand vous créez un déploiement.  

    -   **Taille par défaut** : ce paramètre masque les regroupements, par défaut, qui contiennent plus de clients que votre limite quand vous créez un déploiement. Vous pouvez quand même voir ces regroupements lors de la création du déploiement, mais ils sont masqués par défaut. La valeur par défaut est 100. Entrez la valeur 0 pour ignorer ce paramètre.  

    -   **Taille maximale** : ce paramètre masque toujours les regroupements contenant plus de clients que votre limite quand vous créez un déploiement. La valeur par défaut est 0, qui ignore ce paramètre. La valeur **Taille maximale** doit être supérieure à la valeur **Taille par défaut** .  

     Par exemple, vous affectez la valeur 100 à **Taille par défaut** et la valeur 1000 à **Taille maximale**. Quand vous créez un déploiement à haut risque, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements qui contiennent moins de 100 clients. Si vous désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site**, la fenêtre affiche les regroupements qui contiennent moins de 1 000 clients.  

-   **Regroupements avec des serveurs de système de site**: ce paramètre permet de bloquer les déploiements, ou d’exiger la vérification avant de créer le déploiement, si le regroupement cible comporte un ordinateur ayant un rôle de système de site. Quand un déploiement est bloqué, vous devez sélectionner un autre regroupement qui remplit les critères de vérification de déploiement.  

> [!NOTE]  
>  Les déploiements à haut risque sont toujours limités aux regroupements personnalisés, aux regroupements que vous créez et au regroupement **Ordinateurs inconnus** intégré. Quand vous créez un déploiement à haut risque, vous ne pouvez pas sélectionner un regroupement intégré tel que **Tous les systèmes**.  

### <a name="to-configure-deployment-verification-for-a-site"></a>Pour configurer la vérification du déploiement pour un site  

1.  Dans la console Configuration Manager, choisissez **Administration** >**Configuration du Site** > **Sites**, puis sélectionnez le site principal à configurer.  

2.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**, puis l’onglet **Vérification du déploiement**.  

3.  Après avoir défini les configurations à utiliser, choisissez **OK** pour les enregistrer.  

### <a name="see-also"></a>Voir aussi  
 [Configurer des sites et des hiérarchies pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)
