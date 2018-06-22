---
title: Créer un rôle de système de site de point Endpoint Protection
titleSuffix: Configuration Manager
description: Apprenez à configurer Endpoint Protection de façon à gérer la sécurité et les programmes malveillants sur les ordinateurs clients Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ffca1ddec5b6504ccb2b6646336f56d40e44ac4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350644"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>Créer un rôle de système de site de point Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

 Pour que vous puissiez utiliser Endpoint Protection, le rôle de système de site de point Endpoint Protection doit avoir été installé. Il doit être installé sur un seul serveur de système de site et en haut de la hiérarchie sur un site d'administration centrale ou un site principal autonome.

 Utilisez l’une des procédures suivantes selon que vous voulez installer un nouveau serveur de système de site pour Endpoint Protection ou utiliser un serveur de système de site existant :
 - [Installation sur un nouveau serveur de système de site](#new-site-system-server)
 - [Installation sur un serveur de système de site existant](#existing-site-system-server)

> [!IMPORTANT]
>  Quand vous installez un point Endpoint Protection, un client Endpoint Protection est installé sur le serveur hébergeant le point Endpoint Protection. Les analyses et les services sont désactivés sur ce client pour lui permettre de coexister avec une solution existante anti-programme malveillant installée sur le serveur. Si vous activez ultérieurement ce serveur pour confier la gestion à Endpoint Protection et que vous sélectionnez l’option de suppression de solution tierce anti-programme malveillant, le produit tiers n’est pas supprimé. Vous devez désinstaller ce produit manuellement.

## <a name="new-site-system-server"></a>Nouveau serveur de système de site

1.  Dans la console Configuration Manager, cliquez sur **Administration**.

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Serveurs et rôles de système de site**.

3.  Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un serveur de système de site**.

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.

5.  Sur la page **Sélection du rôle système** , sélectionnez **Point Endpoint Protection** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.

6.  Sur la page **Endpoint Protection** , sélectionnez la case à cocher **J'accepte les termes du contrat de licence Endpoint Protection** et cliquez sur **Suivant**.

    > [!IMPORTANT]
    >  Vous ne pouvez pas utiliser Endpoint Protection dans Configuration Manager, à moins que vous acceptiez les termes du contrat de licence.

7.  Dans la page **Cloud Protection Service**, sélectionnez le niveau d’information à envoyer à Microsoft pour aider au développement de nouvelles définitions, puis cliquez sur **Suivant**.

    > [!NOTE]
    >  Cette option configure les paramètres de Cloud Protection Service (anciennement Microsoft Active Protection Service ou MAPS) utilisés par défaut. Vous pouvez ensuite configurer des paramètres personnalisés pour chaque stratégie anti-programme malveillant que vous créez. Rejoignez Cloud Protection Service pour contribuer à renforcer la protection de vos ordinateurs en fournissant à Microsoft des exemples de programmes malveillants et permettre ainsi de tenir à jour les définitions anti-programme malveillant. De plus, quand vous rejoignez Cloud Protection Service, le client Endpoint Protection peut utiliser le service de signature dynamique pour télécharger les nouvelles définitions avant leur publication sur Windows Update. Pour plus d’informations, consultez [Comment créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Effectuez toutes les étapes de l'Assistant.


## <a name="existing-site-system-server"></a>Serveur de système de site existant

1.  Dans la console Configuration Manager, cliquez sur **Administration**.

2.  Dans l’espace de travail **Administration**, développez **Configuration du site**, cliquez sur **Serveurs et rôles de système de site**, puis sélectionnez le serveur à utiliser pour Endpoint Protection.

3.  Sous l'onglet **Accueil** , dans le groupe **Serveur** , cliquez sur **Ajouter des rôles de système de site**.

4.  Sur la page **Général** , spécifiez les paramètres généraux du système de site, puis cliquez sur **Suivant**.

5.  Sur la page **Sélection du rôle système** , sélectionnez **Point Endpoint Protection** dans la liste des rôles disponibles, puis cliquez sur **Suivant**.

6.  Sur la page **Endpoint Protection** , sélectionnez la case à cocher **J'accepte les termes du contrat de licence Endpoint Protection** et cliquez sur **Suivant**.

    > [!IMPORTANT]
    >  Vous ne pouvez pas utiliser Endpoint Protection dans Configuration Manager, à moins que vous acceptiez les termes du contrat de licence.

7.  Dans la page **Cloud Protection Service**, sélectionnez le niveau d’information à envoyer à Microsoft pour aider au développement de nouvelles définitions, puis cliquez sur **Suivant**.

    > [!NOTE]
    >  Cette option configure les paramètres Cloud Protection Service (anciennement MAPS) utilisés par défaut. Vous pouvez configurer des paramètres personnalisés pour chaque stratégie anti-programme malveillant que vous configurez. Pour plus d’informations, consultez [Guide pratique pour créer et déployer des stratégies de logiciel anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md).

8.  Effectuez toutes les étapes de l'Assistant.
