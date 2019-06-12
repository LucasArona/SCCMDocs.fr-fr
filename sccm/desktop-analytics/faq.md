---
title: Forum aux questions sur les postes de travail Analytique
titleSuffix: Configuration Manager
description: Forum aux questions pour l’Analytique de bureau.
ms.date: 06/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1187688813c2d7a3308ed5ed53e29cb90640dda8
ms.sourcegitcommit: 0bd336e11c9a7f2de05656496a1bc747c5630452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66834840"
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
