---
title: Configuration de la gestion de l’alimentation
titleSuffix: Configuration Manager
description: Configurez la gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9561528d8f02cf5909c83a88a276e1d263343589
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142236"
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>Configuration de la gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de pouvoir utiliser la gestion de l’alimentation dans System Center Configuration Manager, vous devez effectuer les étapes de configuration suivantes.  

## <a name="enable-and-configure-power-management-client-settings"></a>Activer et configurer les paramètres client de gestion de l’alimentation  
 Cette procédure configure les paramètres client par défaut pour la gestion de l'alimentation et s'appliquera à tous les ordinateurs de votre hiérarchie. Si vous souhaitez que ces paramètres s'appliquent uniquement à certains ordinateurs, créez un paramètre client de périphérique personnalisé et affectez-le à un regroupement contenant les ordinateurs pour lesquels vous souhaitez utiliser la gestion de l'alimentation. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>Pour activer la gestion de l'alimentation et configurer les paramètres client  

1. Dans la console Configuration Manager, cliquez sur **Administration**.  

2. Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3. Cliquez sur **Paramètres client par défaut**.  

4. Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5. Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Gestion de l'alimentation**.  

6. Configurez la valeur suivante pour les paramètres client de gestion de l’alimentation :  

   -   **Autoriser la gestion de l'alimentation des périphériques** – Dans la liste déroulante, sélectionnez **Vrai** pour activer la gestion de l'alimentation.  

7. Configurez les paramètres client dont vous avez besoin. Pour obtenir la liste des paramètres client de gestion de l’alimentation que vous pouvez configurer, consultez la section [Gestion de l’alimentation](../../../../core/clients/deploy/about-client-settings.md#power-management) dans la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).  

8. Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres client par défaut** .  

   Les ordinateurs clients sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un client unique, consultez [Comment gérer les clients dans System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

## <a name="exclude-computers-from-power-management"></a>Exclure des ordinateurs de la gestion de l’alimentation  
 Vous pouvez empêcher les regroupements d'ordinateurs de recevoir les paramètres de gestion de l'alimentation. Si un ordinateur est membre d'un regroupement qui est exclu des paramètres de gestion de l'alimentation, cet ordinateur n'applique pas les paramètres de gestion de l'alimentation, même s'il est membre d'un autre regroupement qui applique les paramètres de gestion de l'alimentation.  

 Vous pouvez exclure des ordinateurs de la gestion de l’alimentation pour l’une des raisons suivantes :  

-   Une exigence métier requiert que les ordinateurs soient constamment allumés.  

-   Vous avez créé un regroupement de contrôle d'ordinateurs sur lesquels vous ne souhaitez pas appliquer les paramètres de gestion de l'alimentation.  

-   Certains de vos ordinateurs sont incapables d'appliquer des paramètres de gestion de l'alimentation.  

-   Vous voulez exclure des ordinateurs qui exécutent Windows Server à partir de la gestion de l'alimentation.  

> [!NOTE]  
>  Si l'option **Autoriser les utilisateurs à exclure leur périphérique de la gestion de l'alimentation** est configurée dans les paramètres client, les utilisateurs peuvent exclure leurs propres ordinateurs de la gestion de l'alimentation à l'aide du Centre logiciel.  

 Pour savoir quels ordinateurs ont été exclus de la gestion de l'alimentation, exécutez le rapport **Ordinateurs exclus**. Pour plus d’informations sur ce rapport, consultez [Ordinateurs exclus](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded) dans [Guide pratique pour surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Les paramètres d'alimentation appliqués aux ordinateurs qui exécutent Windows XP ou Windows Server 2003 ne sont pas rétablis selon leurs valeurs d'origine, même si vous excluez l'ordinateur de la gestion de l'alimentation. Sur les versions ultérieures de Windows, l'exclusion d'un ordinateur de la gestion de l'alimentation entraîne le rétablissement des valeurs d'origine de tous les paramètres d'alimentation. Il est impossible de rétablir les valeurs d'origine de chaque paramètre d'alimentation.  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>Pour exclure un regroupement d'ordinateurs de la gestion de l'alimentation  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements de périphériques**.  

3. Dans la liste **Regroupements de périphériques** , sélectionnez le regroupement que vous souhaitez exclure de la gestion de l'alimentation, puis, dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4. Sous l’onglet **Gestion de l’alimentation** de la boîte de dialogue **Propriétés de** <em><Nom du regroupement\></em>, sélectionnez **Ne jamais appliquer les paramètres de gestion de l’alimentation aux ordinateurs de ce regroupement**.  

5. Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de** <em><Nom du regroupement\></em> et pour enregistrer vos paramètres.  
