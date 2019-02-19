---
title: Sécurité et confidentialité de l’inventaire logiciel
titleSuffix: Configuration Manager
description: Obtenez des informations de sécurité et de confidentialité pour l’inventaire logiciel dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dfd765683aa9185d10cba1ae4e4e00837926a6ab
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133678"
---
# <a name="security-and-privacy-for-software-inventory-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour l’inventaire logiciel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations de sécurité et de confidentialité pour l’inventaire logiciel dans System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Meilleures pratiques de sécurité pour l’inventaire logiciel  
 Utilisez les meilleures pratiques de sécurité suivantes lorsque vous recueillez des données d'inventaire logiciel à partir de clients :  

|Bonnes pratiques de sécurité|Informations complémentaires|  
|----------------------------|----------------------|  
|Signer et chiffrer les données d'inventaire|Lorsque les clients communiquent avec les points de gestion à l'aide du protocole HTTPS, toutes les données qu'ils envoient sont chiffrées à l'aide du protocole SSL. Toutefois, lorsque des ordinateurs clients utilisent le protocole HTTP pour communiquer avec des points de gestion sur l'intranet, les données d'inventaire client et les fichiers collectés peuvent être envoyés non signés et non chiffrés. Assurez-vous que le site est configuré pour exiger la signature et utiliser le chiffrement. En outre, si les clients peuvent prendre en charge l'algorithme SHA-256, sélectionnez l'option pour exiger SHA-256.|  
|N'utilisez pas le regroupement de fichiers pour collecter des fichiers critiques ou des informations sensibles|L’inventaire logiciel Configuration Manager utilise tous les droits du compte LocalSystem, qui permet de recueillir des copies de fichiers système critiques, tels que le Registre ou la base de données du compte de sécurité. Lorsque ces fichiers sont disponibles sur le serveur de site, un individu disposant des droits Lire la ressource ou de droits NTFS sur l'emplacement de stockage du fichier pourrait en analyser le contenu et probablement découvrir des informations essentielles sur le client, ce qui permettrait de compromettre sa sécurité.|  
|Restreindre les droits d'administrateur local sur les ordinateurs client|Un utilisateur disposant des droits d'administrateur local peut envoyer des données non valides comme informations d'inventaire.|  

### <a name="security-issues-for-software-inventory"></a>Problèmes de sécurité pour l’inventaire logiciel  
 La collecte d'inventaires engendre des vulnérabilités potentielles. Les intrus peuvent effectuer les opérations suivantes :  

- Envoyer des données non valides qui seront acceptées par le point de gestion, même lorsque le paramètre du client d'inventaire logiciel est désactivé et le regroupement de fichiers n'est pas activé.  

- Envoyer de trop grandes quantités de données dans un seul fichier et dans de nombreux fichiers, ce qui risque provoquer un déni de service.  

- Accéder aux informations d’inventaire lors de leur transfert vers Configuration Manager.  

  Si les utilisateurs savent qu'ils peuvent créer un fichier masqué appelé **Skpswi.dat** et le placer à la racine du disque dur d'un client pour l'exclure de l'inventaire logiciel, vous ne pourrez pas recueillir de données d'inventaire logiciel à partir de cet ordinateur.  

  Dans la mesure où un utilisateur bénéficiant de privilèges d’administrateur local peut envoyer n’importe quelles informations comme données d’inventaire, ne considérez pas que les données d’inventaire collectées par Configuration Manager peuvent servir de référence.  

  L'inventaire logiciel est activé par défaut comme un paramètre client.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informations de confidentialité pour l’inventaire logiciel  
 L’inventaire matériel vous permet de récupérer toutes les informations stockées dans le Registre et dans WMI sur les clients Configuration Manager. L'inventaire logiciel vous permet de découvrir tous les fichiers d'un type donné ou de collecter tous les fichiers spécifiés à partir des clients. Asset Intelligence améliore les capacités de l'inventaire en étendant l'inventaire matériel et logiciel et en ajoutant la nouvelle fonctionnalité de gestion des licences.  

 L'inventaire matériel est activé par défaut comme un paramètre client et les informations WMI recueillies sont déterminées par les options que vous sélectionnez. L'inventaire logiciel est activé par défaut, mais les fichiers ne sont pas recueillis par défaut. Le regroupement de données Asset Intelligence est automatiquement activé, bien que vous puissiez sélectionner les classes de rapport d'inventaire matériel à activer.  

 Les informations d'inventaire ne sont pas envoyées à Microsoft. Les informations d’inventaire sont stockées dans la base de données Configuration Manager. Lorsque les clients utilisent HTTPS pour se connecter à des points de gestion, les données d'inventaire qu'ils envoient au site sont chiffrées pendant le transfert. Si les clients utilisent le protocole HTTP pour se connecter à des points de gestion, vous pouvez activer le chiffrement d'inventaire. Les données d'inventaire ne sont pas stockées au format chiffré dans la base de données. Les informations sont conservées dans la base de données jusqu'à ce qu'elles soient supprimées par les tâches de maintenance du site **Supprimer les historiques d'inventaire anciens** ou **Supprimer les fichiers collectés anciens** tous les 90 jours. Vous pouvez configurer l'intervalle de suppression.  

 Avant de configurer l'inventaire matériel, l'inventaire logiciel, le regroupement de fichiers ou la collecte de données Asset Intelligence, tenez compte de vos exigences en matière de confidentialité.  
