---
title: Gérer les mises à jour rapides de Windows 10
titleSuffix: Configuration Manager
description: Configuration Manager prend en charge les fichiers d’installation rapide pour Windows 10, permettant des téléchargements plus petits et des durées d’installation plus courtes sur les clients.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/15/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b8d8af88-e8ac-4deb-921b-975e2d2afd80
ms.openlocfilehash: 5f29b7a5d82b58358bdecd5508391db219b2cedc
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36260922"
---
# <a name="manage-express-installation-files-for-windows-10-updates"></a>Gérer les fichiers d’installation rapide pour les mises à jour de Windows 10

Configuration Manager prend en charge les fichiers d’installation rapide pour les mises à jour de Windows 10. Configurer le client pour télécharger uniquement les modifications entre la mise à jour qualitative de Windows 10 pendant le mois en cours et la mise à jour du mois précédent. Sans les fichiers d’installation rapide, les clients Configuration Manager téléchargent chaque mois l’intégralité de la mise à jour cumulative de Windows 10 (y compris les mises à jour des mois précédents). L’utilisation de fichiers d’installation rapide permet des téléchargements plus petits et des durées d’installation plus courtes sur les clients.

Pour savoir comment utiliser Configuration Manager pour gérer le contenu de mise à jour afin de rester à jour avec Windows 10, consultez [Optimiser la distribution des mises à jour Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).  


> [!IMPORTANT]  
> La prise en charge de système d’exploitation client est disponible dans Windows 10, version 1607, avec une mise à jour de l’Agent de mise à jour de Windows. Cette mise à jour est incluse dans les mises à jour publiées le 11 avril 2017. Pour plus d’informations sur ces mises à jour, consultez l’[article de support 4015217](http://support.microsoft.com/kb/4015217). Les mises à jour ultérieures s’appuient sur l’installation rapide pour des téléchargements plus petits. Les versions antérieures de Windows 10 et la version 1607 de Windows 10 sans cette mise à jour ne prennent pas en charge les fichiers d’installation rapide.  


### <a name="enable-the-site-to-download-express-installation-files-for-windows-10-updates"></a>Activer le site pour télécharger des fichiers d’installation rapide pour les mises à jour de Windows 10
Pour démarrer la synchronisation des métadonnées pour les fichiers d’installation rapide Windows 10, activez-les dans les propriétés du point de mise à jour logicielle.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Sélectionnez le site d’administration centrale ou le site principal autonome.  

3. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sur **Point de mise à jour logicielle**. Commutez sur l’onglet **Fichiers de mise à jour** et sélectionnez **Télécharger les fichiers complets de toutes les mises à jour approuvées et les fichiers d’installation rapide pour Windows 10**.

> [!NOTE]    
> Vous ne pouvez pas configurer le composant Point de mise à jour logicielle de manière à télécharger *uniquement* les mises à jour rapides.  Le site télécharge les fichiers d’installation rapide en plus des fichiers complets. Ceci augmente la quantité de contenu stocké dans la bibliothèque de contenu et distribué à vos points de distribution, où il est également stocké.

> [!Tip]  
> Pour déterminer l’espace réellement utilisé sur le disque par le fichier, examinez la propriété **Taille sur le disque** du fichier. Cette propriété devrait être considérablement plus petite que la valeur Taille. Pour plus d’informations, consultez [FAQ pour optimiser la distribution de mises à jour Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_faq).  


### <a name="enable-clients-to-download-and-install-express-installation-files"></a>Activer les clients pour télécharger et installer les fichiers d’installation rapide
Pour activer la prise en charge des fichiers d’installation rapide sur les clients, activez les fichiers d’installation rapide dans le groupe **Mises à jour logicielles** des paramètres du client. Ce paramètre crée un écouteur HTTP qui écoute les demandes de téléchargement des fichiers d’installation rapide sur le port que vous spécifiez.

> [!NOTE]    
> Il s’agit d’un port local utilisé par les clients pour écouter les demandes provenant de l’optimisation de la distribution ou de BITS (Service de transfert intelligent en arrière-plan) pour télécharger le contenu rapide à partir du point de distribution. Il n’est pas nécessaire d’ouvrir ce port sur les pare-feu, car tout le trafic est sur l’ordinateur local.  

Quand vous déployez les paramètres du client pour activer cette fonctionnalité sur le client, ils tentent de télécharger le delta entre la mise à jour cumulative de Windows 10 du mois en cours et la mise à jour du mois précédent. Les clients doivent exécuter une version de Windows 10 qui prend en charge les fichiers d’installation rapide.  

1. Activez la prise en charge des fichiers d’installation rapide dans les propriétés du composant du point de mise à jour logicielle (procédure précédente).  

2. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez **Paramètres du client**.  

3. Sélectionnez les paramètres du client appropriés et cliquez sur **Propriétés** sur le ruban.  

4. Sélectionnez le groupe **Mises à jour logicielles**. Configurez sur **Oui** le paramètre **Activer l’installation des mises à jour rapides sur les clients**. Configurer **le Port utilisé pour télécharger du contenu pour les mises à jour rapides** avec le port utilisé par l’écouteur HTTP sur le client.  
