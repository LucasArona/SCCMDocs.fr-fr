---
title: Capacités de la version Technical Preview 1607
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1607 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3bc18a9d061100e63d241c5078ea7dbac75db3f8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1607-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1607 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1607 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="dmp_edition"></a>Améliorations apportées à la stratégie de mise à niveau de l’édition Windows 10

Dans cette version, les améliorations suivantes ont été apportées à cette stratégie :

* Vous pouvez maintenant utiliser la stratégie de mise à niveau d’édition avec des PC Windows 10 qui exécutent le client Configuration Manager en plus des PC Windows 10 inscrits avec Microsoft Intune.
* Vous pouvez effectuer la mise à niveau à partir de Windows 10 Professionnel vers l’une des plateformes de l’Assistant qui sont compatibles avec votre matériel.

[En savoir plus sur la stratégie de mise à niveau de l’édition Windows 10](/sccm/compliance/deploy-use/upgrade-windows-version)

### <a name="try-it-out"></a>Essayez !

1. Utilisez les informations de la [rubrique sur la stratégie de mise à niveau d’édition existante](/sccm/compliance/deploy-use/upgrade-windows-version) pour créer une stratégie de mise à niveau d’édition.
2. Déployez cette stratégie sur un PC Windows 10 exécutant le client Configuration Manager.
Une fois que la stratégie atteint un PC Windows ciblé, l’ordinateur est redémarré dans les deux heures pour appliquer la mise à niveau. Vous ne pouvez pas supprimer ce redémarrage. Assurez-vous d’informer les utilisateurs sur lesquels vous déployez la stratégie ou planifiez l’exécution de la stratégie en dehors des heures de travail des utilisateurs.

### <a name="known-issue-with-this-release"></a>Problèmes connus pour cette version
Dans les paramètres du client Configuration Manager, vous pouvez voir les paramètres pour **Mise à niveau d’édition**. Dans cette version, ces paramètres ne fonctionnent pas. Utilisez les instructions fournies plus haut pour mettre à niveau Windows 10 vers une version plus récente.

## <a name="customizable-branding-for-software-center-dialogs"></a>Personnalisation des boîtes de dialogue du Centre logiciel

Une marque personnalisée pour le Centre logiciel a été introduite dans Configuration Manager version 1602. Dans la version d’évaluation technique 1607, cette marque est désormais étendue à toutes les boîtes de dialogue associées et les notifications de la barre des tâches pour fournir une expérience plus cohérente aux utilisateurs du Centre logiciel.

### <a name="try-it-out"></a>Essayez !

Une marque personnalisée pour le Centre logiciel est appliquée selon les règles suivantes :

1. Si le rôle de serveur de site du point du site web du catalogue des applications n’est pas installé, le Centre logiciel affiche le nom d’organisation spécifié dans le paramètre client de l’**Agent ordinateur** **Nom d’organisation affiché dans le Centre logiciel**. Pour obtenir des instructions, consultez [Guide pratique pour configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).

2. Si le rôle de serveur site de point du site web du catalogue des applications est installé, le Centre logiciel affiche le nom d’organisation et la couleur spécifiés dans les propriétés du rôle de serveur de site du point du site web du catalogue des applications. Pour plus d’informations, consultez [Options de configuration pour le point du site web du catalogue des applications](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website).

3. Si un abonnement Microsoft Intune est configuré et connecté à l’environnement Configuration Manager, le Centre logiciel affiche le nom d’organisation, la couleur et le logo de la société spécifiés dans les propriétés de l’abonnement Intune. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](/mdm/deploy-use/configure-intune-subscription).

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>Utiliser la même carte réseau pour plusieurs déploiements établis par PXE
Dans la version d’évaluation technique 1607, quand vous utilisez une carte Ethernet pour mettre en image plusieurs appareils (par exemple, une carte Ethernet USB que vous utilisez sur plusieurs appareils), vous pouvez activer un nouveau paramètre qui vous permet d’entrer des identificateurs de matériel pour les cartes Ethernet. Configuration Manager ignore les identificateurs de matériel dans la liste lors de l’installation PXE et pour l’inscription des clients.

Pour plus d’informations sur ce problème, consultez le [blog de l’équipe de support OSD Configuration Manager](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/).  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>Activer la fonctionnalité pour gérer les identificateurs de matériel dupliqués  
1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Services cloud** > **Mises à jour et maintenance** > **Fonctionnalités**.
2. Dans le volet d’informations, sélectionnez **Gérer les identificateurs matériels dupliqués**.
3. Sous l’onglet **Accueil**, dans le groupe **Fonctionnalités**, cliquez sur **Activer**.

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Ajouter des identificateurs de matériel que Configuration Manager doit ignorer  
1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Sites**.
2. Dans l'onglet **Accueil** , dans le groupe **Sites** , cliquez sur **Paramètres de hiérarchie**.
3. Accédez à l’onglet **Approbation client et enregistrements en conflit**.
4. Cliquez sur **Ajouter** dans la section **Identificateurs de matériel dupliqués** pour ajouter de nouveaux identificateurs de matériel.
