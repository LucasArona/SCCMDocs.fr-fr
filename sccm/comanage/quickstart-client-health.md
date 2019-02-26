---
title: Intégrité du client avec la cogestion
titleSuffix: Configuration Manager
description: Maintenir la visibilité du contrôle d’intégrité du client Configuration Manager à partir d’Intune sur le portail Azure
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5b243aac-8a1a-4f14-ba3f-5446bb483e92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6838371a80530d5ab66abd9d8a976af41513e15
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754896"
---
# <a name="client-health-with-co-management"></a>Intégrité du client avec la cogestion

L’intégrité de votre réseau est directement connectée à l’intégrité des appareils entrantes ou sortantes il. Intune peut communiquer avec un client défectueux, même lorsqu’il n’est pas sur votre réseau. Utiliser la cogestion à combiner cette fonctionnalité avec possibilité de Configuration Manager pour rapporter à 98 % des clients sains connus. Puis vous pouvez détecter, évaluer et offrent une visibilité sur tous les clients en temps réel. Intune ajoute également la prise en charge nécessaire pour les mises à niveau de conformité sur tous les clients connectés.

Dans la vidéo suivante, responsable de programme senior Rob York produit marketing Ainley Locky manager discuter et démonstration de l’intégrité du client avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Avantages

L’évaluation de l’intégrité du client est une priorité absolue. System Center 2012 Configuration Manager ajouté **CCMeval**. Cet utilitaire est externe au client Configuration Manager. Il fournit client mise à jour automatique et de surveillance d’intégrité. Toutefois, la création de rapports s’appuie sur un périphérique qui est physiquement ou virtuellement sur votre réseau interne. Cogestion permet de résoudre ce problème.

Avec la cogestion, Intune peut signaler sur l’état d’intégrité du client. Il fournit des informations d’horodatage pour la validité des données. Ces informations indiquent si vos appareils sont sains, en mesure de se connecter, vous pouvez installer des applications, ou peuvent mettre à jour vers le système d’exploitation requis builds. 

Pour obtenir une présentation détaillée de cette fonctionnalité, consultez cette vidéo à partir de la [What ' s New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) session à Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Lorsque Configuration Manager fournit l’état de l’appareil que le client est installé, mais il n’est pas, Intune peut fournir plus d’informations sans avoir à se connecter au client. Les informations de contrôle d’intégrité d’appareil dans Intune sont facile à comprendre. Si l’état est autre que **sain**, il donne des recommandations et les étapes suivantes pour dépanner et résoudre le problème.

> [!Note]  
> Les avantages suivants sont planifiées pour une version ultérieure :
> - Configuration Manager inclut des fonctionnalités supplémentaires dans CCMeval  
> - Il sera plus facile d’identifier des ordinateurs potentiellement défectueux dans Configuration Manager et Intune  
> - Vous pouvez regrouper les données de contrôle d’intégrité de client dans Intune  



## <a name="value-proposition"></a>Proposition de valeur

Avec cette fonctionnalité, vous disposez maintenant d’une source de données externe avec Intune. Il vous permet de vous permettent de déterminer les étapes suivantes lors du dépannage d’un large éventail de problèmes de client. Maintenant vous n’avez pas besoin créer des rapports supplémentaires ou d’autres outils permettent de récupérer des données du client.

Lorsque vous avez les clients intègres, vous avez facilement mis à jour conformité du correctif. Une meilleure conformité de correctif signifie une meilleure sécurité.



## <a name="configure"></a>Configurer

Pour vous familiariser avec cette fonctionnalité, utilisez les étapes suivantes :

- Mettre à jour des appareils vers Windows 10, version 1709 ou ultérieure  

- [Activer la cogestion](/sccm/comanage/how-to-enable)  
    - Vous n’avez pas besoin de basculer des charges de travail sur Intune  

- Mettre à jour votre site Configuration Manager et les clients à *version 1806* ou version ultérieure  


### <a name="review-configuration-manager-client-health-in-intune"></a>Passez en revue le contrôle d’intégrité du client Configuration Manager dans Intune

1. Connectez-vous au [portail Azure](https://portal.azure.com/).  

2. Choisissez **tous les services** > **Intune**. Intune se trouve dans le **surveillance + gestion** section.  

3. Une fois que vous avez ouvert le **Microsoft Intune** volet, dans le menu sous **aide et support**, accédez à la **dépannage** page.  

4. Utilisez le **sélectionner un utilisateur** , l’option trouver le périphérique spécifique dans le **appareils** liste, puis sélectionnez-la pour ouvrir la page de l’appareil.  

5. Informations de cogestion sont affichées en bas de la page de l’appareil. Ces informations incluent les champs suivants pour l’intégrité du client :  
    - **État de l’agent de configuration Manager**  
    - **Dernière vérification de l’agent de Configuration Manager dans le temps**  

> [!Tip]  
> Appareils inscrits dans Intune se connectent au service cloud et trois fois par jour, environ toutes les huit heures. 
