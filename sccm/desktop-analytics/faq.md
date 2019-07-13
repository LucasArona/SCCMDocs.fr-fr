---
title: Forum aux questions sur les postes de travail Analytique
titleSuffix: Configuration Manager
description: Forum aux questions pour l’Analytique de bureau.
ms.date: 07/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 663490349bcb61f243980c5e1a3fe1f5651d8573
ms.sourcegitcommit: 448cc0d9094a3c9e23f011c4673cd1e8b956280a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67860833"
---
# <a name="desktop-analytics-faq"></a>Analytique bureau Forum aux questions

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

## <a name="windows-upgrade"></a>Mise à niveau Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Puis-je mettre à niveau de Windows et modifier l’architecture ?

Analytique de bureau est conçu pour les bonnes mises à niveau de prise en charge. Mises à niveau sur place ne prennent pas en charge les migrations à partir de l’architecture 32 bits vers 64 bits. Si vous avez besoin migrer des ordinateurs dans ce scénario, utilisez le scénario d’actualisation. Bureau insights Analytique sont toujours utiles dans ce scénario, mais vous pouvez ignorer les instructions spécifiques à la mise à niveau.

Pour plus d’informations, voir [Actualiser un ordinateur existant avec une nouvelle version de Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Puis-je modifier du BIOS en UEFI lorsque la mise à niveau de Windows ?

Oui. Pour plus d’informations, consultez [convertir du BIOS en UEFI pendant une mise à niveau sur place](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Puis-je utiliser Desktop Analytique avec Windows 10 LTSC ?

Vous pouvez utiliser l’Analytique de bureau afin de faciliter la mise à jour des appareils à partir de Windows 10 Long-Term Servicing canal (LTSC) pour Windows 10 canal semi-annuel, Analytique de bureau ne prend en charge les mises à jour de Windows 10 LTSC. Ce canal de Windows 10 n’est pas destiné à une large utilisation et ne reçoit pas les mises à jour de fonctionnalité, il n’est pas une cible pris en charge avec l’Analytique de bureau. Pour plus d’informations, consultez [Windows comme une vue d’ensemble du service](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Puis-je réduire la quantité de temps que nécessaire pour les données sont à actualiser dans Mon portail Desktop Analytique ?

Il existe deux types de données dans le portail d’Analytique de bureau : Données d’administration et les données de diagnostic. Pour actualiser l’administrateur des données sur demande, ouvrez le menu volant devise de données et sélectionnez **appliquer les modifications**. Cette action déclenche immédiatement une actualisation à usage unique de toutes les modifications d’administrateur dans vos espaces de travail. Les modifications se propageront et sont généralement disponibles dans les 15 à 60 minutes. La synchronisation dépend de la taille de votre espace de travail et l’étendue des modifications en attente. Vous pouvez demander une actualisation des données de la demande jusqu'à six fois pendant une période de 24 heures. 

Toutes les données est mis à jour automatiquement une fois par jour, même si vous ne demandez pas une actualisation des données de la demande. Il n’existe aucun moyen pour déclencher une actualisation à la demande de données de diagnostic. Pour plus d’informations sur les différents types de données d’Analytique de bureau, consultez [latence des données](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Confidentialité

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Analytique de bureau peut être utilisé sans une connexion directe du client pour le Service de gestion des données de Microsoft ?

Non, l’ensemble du service est alimenté par les données de diagnostic Windows, ce qui nécessite que les appareils disposent cette connectivité directe.

### <a name="can-i-choose-the-data-center-location"></a>Puis-je choisir l’emplacement de centre de données ?

Pour l’Analytique des journaux Azure : Oui, lorsque vous définissez Analytique de bureau et créez l’espace de travail Analytique de journal.

Pour le Service Gestion des données de Microsoft et l’Analytique stockage Azure : Non, ces deux services sont hébergés dans les États-Unis.

### <a name="where-is-my-organizations-data-stored"></a>Où sont stockées les données de mon organisation ?

Données de diagnostic de Windows à partir de vos ordinateurs sont chiffrées, envoyées à et traitées dans les centres de données sécurisé gérés par Microsoft situés aux États-Unis. Notre analyse des données liées au bureau Analytique puis vous est fournie via la solution d’Analytique de bureau dans le portail Azure. Analytique de bureau est pris en charge dans toutes les régions Azure. Sélection d’une région Azure internationale n’empêche pas les données de diagnostic d’être envoyé à et traité dans les centres de données sécurisés de Microsoft dans le fuseau horaire.

## <a name="other"></a>Autre

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>Puis-je utiliser Desktop Analytique mes mises à niveau vers Office 365 ProPlus ?

Non, Analytique de bureau se concentre sur Windows. Microsoft a développé Analytique de bureau en étroite collaboration avec nombreux clients. Via le programme d’évaluation, les commentaires des clients a été sur la façon dont bureau Analytique amélioré leur capacité à gérer en toute confiance des déploiements de Windows. Ils également nous demandé ils [Office 365 ProPlus readiness ](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) plus étroitement intégrée avec les outils de gestion d’office dans Configuration Manager et Intune. Microsoft continuera à faire des investissements dans ces domaines, tout en restant concentré sur les scénarios de Windows dans Analytique de bureau.
