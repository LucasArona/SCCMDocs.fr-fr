---
title: Intégrité des clients avec la cogestion
titleSuffix: Configuration Manager
description: Superviser l’intégrité des clients Configuration Manager à partir d’Intune sur le portail Azure
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754896"
---
# <a name="client-health-with-co-management"></a>Intégrité des clients avec la cogestion

L’intégrité de votre réseau est directement liée à l’intégrité des appareils qui y rentrent et qui en sortent. Intune peut communiquer avec un client non sain, même si celui-ci n’est pas sur votre réseau. Utilisez la cogestion pour combiner cette fonctionnalité avec la capacité de Configuration Manager à rendre compte de 98 % des clients sains connus. Ainsi, vous pourrez détecter, évaluer et fournir une visibilité sur tous les clients en temps réel. Intune fournit également la prise en charge nécessaire pour les mises à niveau de conformité sur tous les clients connectés.

Dans la vidéo suivante, le program manager senior, Rob York, et le directeur du marketing produit, Locky Ainley, parlent et font la démonstration de l’intégrité des clients avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Client-Health-Monitoring-with-Co-Management/player]



## <a name="benefits"></a>Avantages

L’évaluation de l’intégrité des clients est une priorité absolue. **CCMeval** a été ajouté dans System Center 2012 Configuration Manager. Cet utilitaire est externe au client Configuration Manager. Il permet de superviser l’intégrité des clients et de la corriger automatiquement. Toutefois, ce type de rapport s’appuie sur un appareil qui est physiquement ou virtuellement sur votre réseau interne. La cogestion permet de résoudre ce problème.

Avec la cogestion, Intune peut produire des rapports sur l’état d’intégrité des clients. Il fournit des informations d’horodatage pour la validité des données. Ces informations vous indiquent si vos appareils sont sains, capables de se connecter, capables d’installer des applications ou d’effectuer des mises à jour vers les builds de système d’exploitation requises. 

Pour une présentation détaillée de cette fonctionnalité, regardez cette vidéo de la session [What’s New in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/64591) de la conférence Ignite 2018.

> [!VIDEO https://www.youtube.com/embed/UAW2KBUq7DM?start=518]


Quand Configuration Manager fournit un état d’appareil en indiquant que le client est installé alors qu’il ne l’est pas, Intune peut donner plus d’informations sans avoir à se connecter au client. Les informations d’intégrité d’appareil dans Intune sont faciles à comprendre. Si l’état n’est pas **Sain**, il donne des recommandations et des étapes à suivre pour corriger le problème.

> [!Note]  
> Dans une prochaine version, les avantages suivants sont prévus :
> - Configuration Manager inclura des fonctionnalités supplémentaires dans CCMeval.  
> - Il sera plus facile d’identifier des ordinateurs potentiellement non sains dans Configuration Manager et Intune.  
> - Vous pourrez regrouper les données d’intégrité des clients dans Intune.  



## <a name="value-proposition"></a>Proposition de valeur

Avec cette fonctionnalité, vous disposez maintenant d’une source de données externe avec Intune. Elle vous permet de déterminer les prochaines étapes lors du dépannage d’un grand ensemble de problèmes client. Maintenant, vous n’avez pas besoin de créer de rapports supplémentaires ou d’utiliser d’autres outils pour récupérer les données de clients.

Quand vous avez des clients sains, vous mettez facilement à jour la conformité des correctifs. Une meilleure conformité des correctifs est synonyme d’une meilleure sécurité.



## <a name="configure"></a>Configurer

Pour commencer à utiliser cette fonctionnalité, suivez ces étapes :

- Mettre à jour vos appareils vers Windows 10, version 1709 ou ultérieure  

- [Activer la cogestion](/sccm/comanage/how-to-enable)  
    - Vous n’avez besoin de basculer aucune charge de travail dans Intune  

- Mettre à jour votre site Configuration Manager et les clients avec la *version 1806* ou ultérieure  


### <a name="review-configuration-manager-client-health-in-intune"></a>Consulter l’intégrité du client Configuration Manager dans Intune

1. Connectez-vous au [portail Azure](https://portal.azure.com/).  

2. Choisissez **Tous les services** > **Intune**. Intune se trouve dans la section **Surveillance + Gestion**.  

3. Une fois que vous avez ouvert le volet **Microsoft Intune** dans le menu sous **Aide et support**, accédez à la page **Dépannage**.  

4. Utilisez l’option **Sélectionner un utilisateur**, recherchez l’appareil spécifique dans la liste **Appareils**, puis sélectionnez-le pour ouvrir la page de l’appareil.  

5. Les informations de cogestion s’affichent en bas de la page de l’appareil. Elles comprennent les champs suivants pour l’intégrité des clients :  
    - **État de l’agent Configuration Manager**  
    - **Heure du dernier enregistrement de l’agent Configuration Manager**  

> [!Tip]  
> Les appareils inscrits à Intune se connectent au service cloud trois fois par jour, environ toutes les huit heures. 
