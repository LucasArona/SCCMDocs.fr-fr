---
title: Blocage de clients
titleSuffix: Configuration Manager
description: Bloquez l’accès client pour la sécurité du système à l’aide de System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 54ef5fbb-521d-4ca5-a1c5-61e6f538d71e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a90e100c242514eb2526e16bb68e379a2326572f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56136913"
---
# <a name="determine-whether-to-block-clients-in-system-center-configuration-manager"></a>Déterminer si des clients doivent être bloqués dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Si un ordinateur client ou un appareil mobile client n’est plus approuvé, vous pouvez bloquer ce client dans la console System Center 2012 Configuration Manager. L’infrastructure Configuration Manager rejette les clients bloqués afin qu’ils ne puissent pas communiquer avec les systèmes de site pour télécharger la stratégie, charger les données d’inventaire ou envoyer des messages d’état.  

 Vous devez bloquer et débloquer les clients depuis leur site attribué plutôt que depuis un site secondaire ou un site d'administration centrale.  

> [!IMPORTANT]  
>  Le blocage dans Configuration Manager aide à sécuriser le site Configuration Manager, mais ne vous fiez pas à cette fonctionnalité pour protéger le site contre les ordinateurs ou les appareils mobiles non approuvés si vous autorisez les clients à communiquer avec les systèmes du site à l’aide de HTTP, car un client bloqué peut de nouveau joindre le site avec un nouveau certificat auto-signé et un nouvel ID matériel. À la place, utilisez la fonctionnalité de blocage pour bloquer les supports de démarrage perdus ou non fiables, que vous utilisez pour déployer les systèmes d'exploitation, et lorsque les systèmes de site acceptent les connexions client HTTPS.  

 Les clients accédant au site à l'aide du certificat proxy ISV ne peuvent pas être bloqués. Pour plus d’informations sur le certificat de proxy ISV, consultez le kit SDK de System Center Configuration Manager.  

 Si vos systèmes de site acceptent les connexions client HTTPS et que votre infrastructure de clé publique (PKI) prend en charge une liste de révocation de certificats, envisagez toujours de définir la révocation de certificat comme première ligne de défense contre les certificats potentiellement compromis. Le blocage des clients dans Configuration Manager fournit une seconde ligne de défense pour protéger votre hiérarchie.  

##  <a name="BKMK_Block_vs_CRL"></a> Éléments à prendre en considération pour le blocage des clients  

-   Cette option est disponible pour les connexions client HTTP et HTTPS, mais sa sécurité est limitée lorsque les clients se connectent à des systèmes de site en utilisant le protocole HTTP.  

-   Les utilisateurs administratifs de Configuration Manager ont l’autorité nécessaire pour bloquer un client et cette action est entreprise dans la console Configuration Manager.  

-   La communication client est rejetée uniquement à partir de la hiérarchie Configuration Manager.  

    > [!NOTE]  
    >  Le même client peut s’inscrire auprès d’une autre hiérarchie Configuration Manager.  

-   Le client est immédiatement bloqué hors du site Configuration Manager.  

-   Permet de protéger les systèmes de site des ordinateurs et des appareils mobiles potentiellement compromis.  

## <a name="considerations-for-using-certificate-revocation"></a>Éléments à prendre en considération pour l’utilisation de la révocation de certificats  

-   Cette option est disponible pour les connexions HTTPS des clients Windows si l’infrastructure à clé publique prend en charge une liste de révocation de certificats (CRL).  

     Les clients Mac contrôlent systématiquement la liste de révocation de certificats, et cette fonctionnalité ne peut pas être désactivée.  

     Même si les clients d’appareils mobiles n’utilisent pas de listes de révocation de certificats pour vérifier les certificats des systèmes de site, leurs certificats peuvent être révoqués et vérifiés par Configuration Manager.  

-   Les administrateurs de l’infrastructure de clé publique ont l’autorité nécessaire pour révoquer un certificat et cette action est entreprise hors de la console Configuration Manager.  

-   Les communications client peuvent être rejetées à partir de tout ordinateur ou appareil mobile nécessitant ce certificat de client.  

-   Il y aura probablement un délai entre la révocation d'un certificat et le téléchargement par les systèmes de site de la liste de révocation de certificats (CRL) modifiée.  

-   Pour de nombreux déploiements PKI, ce délai peut être d'un ou de plusieurs jours. Par exemple, dans les services de certificats Active Directory, la période d'expiration par défaut est d'une semaine pour une liste de révocation de certificats complète et d'un jour pour une liste de révocation de certificats delta.  

-   Permet de protéger les systèmes de site et les clients contre des ordinateurs et des appareils mobiles potentiellement compromis.  

    > [!NOTE]  
    >  Il est possible d'améliorer la protection des systèmes de site qui exécutent IIS contre des clients inconnus en configurant une liste de certificats de confiance (CTL) dans IIS.  
