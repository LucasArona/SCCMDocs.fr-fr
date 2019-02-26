---
title: Configurer Azure AD hybride
titleSuffix: Configuration Manager
description: Si votre environnement comporte actuellement des appareils Windows 10 joints au domaine, configurez hybride Azure AD avant d’activer la cogestion
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec02f740485d3f8b466cde0a644aaaa8885b91f2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754852"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurer hybride Azure AD pour la cogestion

Si vous avez des appareils Windows 10 joints à Active Directory en local, avant d’activer la cogestion dans Configuration Manager, vous devez tout d’abord joindre ces appareils à Azure Active Directory (Azure AD). Ce processus est appelé une jointure hybrid Azure AD. 

Dans la vidéo suivante, responsable de programme senior Sandeep Deo responsable marketing produit Adam Harbour discuter et configuration des périphériques dans Azure AD de démonstration :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Hybride Azure AD-jointure traiter automatiquement inscrit vos appareils joints au domaine local avec Azure AD. Pour plus d’informations sur ce processus, consultez les articles suivants :
- [Introduction à la gestion des appareils dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Comment planifier votre jonction hybride Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Une jointure Hybrid Azure AD est un des fondements de la clé pour la cogestion. Ce processus peut s’avérer difficile pour certains clients, par exemple :
- Votre organisation utilise une solution d’identité tiers 
- La complexité de la configuration d’Active Directory Federation Services (ADFS)

Résolution de ces défis peut prendre quelques conseils. Cet article vous aide à réduire les retards.


## <a name="how-to-do-it"></a>Marche à suivre

Les appareils sont similaires aux utilisateurs lors de la création d’une identité que vous souhaitez protéger. Pour protéger les identités d’un appareil à tout moment et dans n’importe quel emplacement, vous devez placer l’identité de cet appareil dans Azure AD.

Selon le type de domaine que vous utilisez, il existe deux méthodes principales pour ce faire. Configurer hybride Azure AD join pour un des types de domaines suivants :  
- [Domaines fédérés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domaines gérés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Les deux méthodes précédentes offriront la meilleure expérience. Pour plus d’informations, notamment le processus entièrement manuel, consultez les articles suivants :
- [Configurer manuellement des appareils hybrides joints à Azure AD](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [L’authentification directe d’ADFS pour Azure AD hybride](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), qui inclut la découverte d’Azure AD  

Des conseils de dépannage, consultez le [une jointure hybrid Azure AD Windows 10 guide de dépannage](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Étude de cas

Une société de logiciels d’envergure européenne avec plus de 100 000 utilisateurs dans son réseau a eu une approche granulaire et en plusieurs phases l’activation de jonction hybride Azure AD.

Pendant la phase de planification, dans la mesure où une jointure hybrid Azure AD est un élément clé prenant en charge la cogestion, les administrateurs Configuration Manager a travaillé avec l’équipe d’identité. Cette société de logiciels de nombreuses règles AD FS, et certains d'entre eux avaient complexes. Pour relever ce défi, l’équipe d’identité passé en revue les règles ADFS existants avant l’activation de la jointure Azure AD hybride. L’équipe informatique a également choisi Mettre à niveau Azure AD Connect vers la dernière version. Azure AD Connect propose désormais un flux de processus automatisé pour l’activation de jonction hybride Azure AD.

Après la réussite du déploiement et de test dans leur environnement de préproduction, ce client activé hybride Azure AD join pour les ressources de production dans son ensemble. En une semaine, ils avaient tous les appareils Windows 10 gérés conjointement.



## <a name="contact-fasttrack"></a>Contactez FastTrack

Si vous avez besoin de configuration de l’assistance d’Azure AD à tout moment dans le processus, accédez à [Microsoft FastTrack](https://Microsoft.com/FastTrack/), connectez-vous, puis demander une assistance. 

Pour plus d’informations, consultez [obtenir de l’aide de FastTrack](/sccm/comanage/quickstart-fasttrack). 

