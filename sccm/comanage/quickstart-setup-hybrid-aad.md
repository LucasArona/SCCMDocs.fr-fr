---
title: Configurer Azure AD hybride
titleSuffix: Configuration Manager
description: Si votre environnement comporte actuellement des appareils Windows 10 joints au domaine, configurez Azure AD hybride avant d’activer la cogestion
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754852"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Configurer Azure AD hybride pour la cogestion

Si vous avez des appareils Windows 10 joints à Active Directory en local, avant d’activer la cogestion dans Configuration Manager, vous devez tout d’abord joindre ces appareils à Azure AD (Azure Active Directory). Ce processus est appelé jonction Azure AD hybride. 

Dans la vidéo suivante, le program manager senior, Sandeep Deo, et le directeur du marketing produit, Adam Harbour, parlent et font la démonstration de la configuration des appareils dans Azure AD :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Le processus de jonction Azure AD hybride inscrit automatiquement vos appareils joints au domaine local auprès d’Azure AD. Pour plus d’informations sur ce processus, consultez les articles suivants :
- [Introduction à la gestion des appareils dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [Guide pratique pour planifier la jonction Azure AD hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

La jonction Azure AD hybride est l’un des éléments de base pour la cogestion. Ce processus peut s’avérer difficile pour certains clients, par exemple :
- Votre organisation utilise une solution d’identité tierce 
- La complexité de la configuration des services de fédération Active Directory (AD FS)

Quelques conseils peuvent être nécessaires pour relever ces défis. Cet article vous aide à atténuer les retards.


## <a name="how-to-do-it"></a>Marche à suivre

Les appareils sont similaires aux utilisateurs lors de la création d’une identité que vous souhaitez protéger. Pour protéger l’identité d’un appareil à tout moment et à n’importe quel emplacement, vous devez placer l’identité de cet appareil dans Azure AD.

Selon le type de domaine que vous utilisez, il existe deux méthodes principales pour ce faire. Configurez la jonction Azure AD hybride pour l’un des types de domaines suivants :  
- [Domaines fédérés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Domaines gérés](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Les deux méthodes précédentes proposent la meilleure expérience. Pour obtenir des informations plus détaillées, notamment le processus entièrement manuel, consultez les articles suivants :
- [Configurer manuellement des appareils joints à Azure AD hybride](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [Authentification directe AD FS pour Azure AD hybride](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), qui inclut la découverte Azure AD  

Pour des conseils de dépannage, consultez le [guide de résolution des problèmes de jonction Azure AD hybride Windows 10](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Étude de cas

Un important éditeur de logiciels européen avec plus de 100 000 utilisateurs dans son réseau a choisi une approche précise et par phases pour activer la jonction Azure AD hybride.

Pendant la phase de planification, dans la mesure où la jonction Azure AD hybride est un élément clé prenant en charge la cogestion, les administrateurs Configuration Manager ont travaillé avec l’équipe en charge des identités. Cet éditeur de logiciels suivait de nombreuses règles AD FS, et certaines d’entre elles étaient complexes. Pour relever ce défi, l’équipe en charge des identités a passé en revue les règles AD FS existantes avant l’activation de la jonction Azure AD hybride. L’équipe informatique a également choisi de mettre à niveau Azure AD Connect avec la dernière version. Azure AD Connect propose désormais un flux de processus automatisé pour l’activation de la jonction Azure AD hybride.

Après la réussite du déploiement et des tests dans son environnement de préproduction, ce client a activé la jonction Azure AD hybride pour l’ensemble du domaine de production. En l’espace d’une semaine, tous les appareils Windows 10 étaient cogérés.



## <a name="contact-fasttrack"></a>Contacter FastTrack

Si vous avez besoin d’assistance concernant la configuration d’Azure AD à n’importe quelle étape du processus, accédez à [Microsoft FastTrack](https://Microsoft.com/FastTrack/), connectez-vous, puis demandez de l’aide. 

Pour plus d’informations, consultez [Obtenir l’aide de FastTrack](/sccm/comanage/quickstart-fasttrack). 

