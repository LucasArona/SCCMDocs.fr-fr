---
title: Sécurité et confidentialité pour les mises à jour logicielles
titleSuffix: Configuration Manager
description: Adoptez ces bonnes pratiques pour la sécurité des mises à jour logicielles et découvrez comment Configuration Manager gère les informations de confidentialité.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 437710d32d979a687a4075761bb1ce3b76dcda51
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493595"
---
# <a name="security-and-privacy-for-software-updates-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations de sécurité et de confidentialité pour les mises à jour logicielles dans System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Bonnes pratiques concernant les mises à jour logicielles  
 Utilisez ces meilleures pratiques de sécurité lorsque vous déployez des mises à jour logicielles vers des clients :  

-   Ne modifiez pas les autorisations par défaut des packages de mises à jour logicielles.  

     Par défaut, les packages de mises à jour logicielles sont définis pour permettre aux administrateurs d'avoir un **Contrôle intégral** et aux utilisateurs d'avoir un accès en **Lecture** . La modification de ces autorisations pourrait permettre à un attaquant d'ajouter, de retirer ou de supprimer des mises à jour logicielles.  

-   Contrôlez l'accès à l'emplacement de téléchargement des mises à jour logicielles.  

     Les comptes d'ordinateur pour le fournisseur SMS, le serveur de site et l'utilisateur administratif qui téléchargeront les mises à jour logicielles vers l'emplacement de téléchargement doivent avoir un accès en **Écriture** à cet emplacement. Limitez l'accès à l'emplacement de téléchargement pour éviter que des personnes malveillantes ne falsifient les fichiers sources des mises à jour logicielles.  

     En outre, si vous utilisez un partage UNC pour l'emplacement de téléchargement, sécurisez le canal réseau à l'aide d'une signature IPsec ou SMB pour éviter la falsification des fichiers sources des mises à jour logicielles lorsqu'ils sont transférés sur le réseau.  

-   Utilisez le temps universel coordonné (UTC) pour évaluer les temps de déploiement.  

     Si vous utilisez l'heure locale au lieu de l'heure UTC, les utilisateurs pourraient retarder l'installation des mises à jour logicielles en changeant le fuseau horaire sur leurs ordinateurs.  

-   Activez SSL sur WSUS, puis suivez les meilleures pratiques pour la sécurisation de Windows Server Update Services (WSUS).  

     Identifiez et adoptez les bonnes pratiques de sécurité pour la version de WSUS que vous utilisez avec Configuration Manager.  

    > [!IMPORTANT]  
    >  Si vous configurez le point de mise à jour logicielle pour activer les communications SSL pour le serveur WSUS, vous devez configurer SSL pour les racines virtuelles sur le serveur WSUS.  

-   Activez la vérification de la liste de révocation de certificats.  

     Par défaut, Configuration Manager ne consulte pas la liste de révocation de certificats (CRL) pour vérifier la signature des mises à jour logicielles avant de les déployer sur les ordinateurs. La vérification de la liste de révocation de certificats à chaque utilisation d'un certificat est une sécurité supplémentaire qui permet de ne pas utiliser de certificat révoqué. Toutefois, elle implique un délai de connexion et un traitement supplémentaire sur l'ordinateur qui l'effectue.  

     Pour plus d’informations sur l’activation de la vérification de la liste de révocation des certificats pour les mises à jour logicielles, consultez [Guide pratique pour activer la vérification de la liste de révocation de certificats pour les mises à jour logicielles dans System Center Configuration Manager](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Configurez WSUS pour utiliser un site Web personnalisé.  

     Lorsque vous installez WSUS sur le point de mise à jour logicielle, vous avez la possibilité d'utiliser le site Web IIS par défaut existant ou créer un site Web WSUS personnalisé. Créez un site Web personnalisé pour WSUS de sorte que les services Internet hébergent les services WSUS dans un site Web virtuel dédié plutôt que de partager le même site Web que celui utilisé par les autres systèmes de site Configuration Manager ou d'autres applications.  

     Pour plus d’informations, consultez [Configurer WSUS pour utiliser un site web personnalisé](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informations de confidentialité pour les mises à jour logicielles  
 Les mises à jour logicielles analysent vos ordinateurs clients pour connaître les mises à jour requises et renvoient les informations à la base de données de site. Pendant le processus de mise à jour logicielle, Configuration Manager peut faire circuler, entre les clients et les serveurs, des informations qui permettent d’identifier les comptes d’ordinateur et d’ouverture de session.  

 Configuration Manager gère les informations d’état relatives au processus de déploiement de logiciels. Les informations d'état ne sont pas chiffrées au cours de la transmission ou du stockage. Les informations d’état sont stockées dans la base de données Configuration Manager et sont supprimées par les tâches de maintenance de la base de données. Aucune information d'état n'est renvoyée à Microsoft.  

 L’utilisation des mises à jour logicielles Configuration Manager pour installer les mises à jour logicielles sur les ordinateurs clients peut être soumise à un contrat de licence indépendant du contrat de licence logiciel de System Center Configuration Manager. Consultez et acceptez toujours les termes du contrat de licence logicielle pour pouvoir installer les mises à jour logicielles à l’aide de Configuration Manager.  

 Configuration Manager n’implémente pas les mises à jour logicielles par défaut et requiert plusieurs étapes de configuration avant de collecter les informations.  

 Avant de configurer les mises à jour logicielles, réfléchissez à vos besoins en matière de confidentialité.  
