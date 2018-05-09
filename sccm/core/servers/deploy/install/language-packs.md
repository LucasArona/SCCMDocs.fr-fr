---
title: Modules linguistiques
titleSuffix: Configuration Manager
description: Découvrez la prise en charge linguistique disponible dans System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a198e15a1ef389d792acc73f2253aa4a704ac35a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="language-packs-in-system-center-configuration-manager"></a>Modules linguistiques dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique fournit des détails techniques sur la prise en charge linguistique dans System Center Configuration Manager.  

## <a name="BKMK_SupLanguagePacks"></a> Langues du système d’exploitation prises en charge  
 Vous pouvez installer la prise en charge des langues d’affichage des tableaux suivants en installant les **modules linguistiques du serveur** ou les **modules linguistiques du client** sur le site d’administration centrale et sur les sites principaux. Vous sélectionnez les langues de serveur et de client à prendre en charge sur ce site parmi les fichiers de modules linguistiques disponibles au cours du processus d’installation.

 Les fichiers de modules linguistiques sont téléchargés quand vous exécutez le programme d’installation dans le cadre du téléchargement des fichiers prérequis et redistribuables. Vous pouvez également utiliser le [Téléchargeur d’installation](setup-downloader.md) pour télécharger ces fichiers avant d’exécuter le programme d’installation.   

 Aidez-vous du tableau suivant pour mapper un ID de paramètres régionaux à la langue que vous voulez prendre en charge sur des serveurs ou des ordinateurs clients. Pour plus d’informations sur les ID de paramètres régionaux, consultez [ID de paramètres régionaux attribués par Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=252609).  

### <a name="server-languages"></a>Langues du serveur  

|Langue du serveur|ID de paramètres régionaux (LCID)|Code en trois lettres|  
|---------------------|------------------------|-----------------------|  
|Anglais (par défaut)|0409|ENU|  
|Chinois (traditionnel, Hong Kong R.A.S.)|0c04|ZHH|  
|Chinois (simplifié)|0804|CHS|  
|Chinois (traditionnel, Taïwan)|0404|CHT|  
|Tchèque|0405|CSY|  
|Néerlandais - Pays-bas|0413|NLD|  
|Français|040c|FRA|  
|Allemand|0407|DEU|  
|Hongrois|040e|HUN|  
|Italien - Italie|0410|ITA|  
|Japonais|0411|JPN|  
|Coréen|0412|KOR|  
|Polonais|0415|PLK|  
|Portugais - Brésil|0416|PTB|  
|Portugais - Portugal|0816|PTG|  
|Russe|0419|RUS|  
|Espagnol - Espagne|0c0a|ESN|  
|Suédois|041d|SVE|  
|Turc|041f|TRK|  

### <a name="client-languages"></a>Langues du client  

|Langue du client|ID de paramètres régionaux (LCID)|Code en trois lettres|  
|---------------------|------------------------|-----------------------|  
|Anglais (par défaut)|0409|ENG|  
|Chinois (traditionnel, Hong Kong R.A.S.)|0c04|ZHH|  
|Chinois simplifié|0804|CHS|  
|Chinois (traditionnel, Taïwan)|0404|CHT|  
|Tchèque|0405|CSY|  
|Danois|0406|DAN|  
|Néerlandais - Pays-bas|0413|NLD|  
|Finnois|040b|FIN|  
|Français|040c|FRA|  
|Allemand|0407|DEU|  
|Grec|0408|ELL|  
|Hongrois|040e|HUN|  
|Italien - Italie|0410|ITA|  
|Japonais|0411|JPN|  
|Coréen|0412|KOR|  
|Norvégien|0414|NOR|  
|Polonais|0415|PLK|  
|Portugais (Brésil)|0416|PTB|  
|Portugais (Portugal)|0816|PTG|  
|Russe|0419|RUS|  
|Espagnol - Espagne|0c0a|ESN|  
|Suédois|041d|SVE|  
|Turc|041f|TRK|  

### <a name="mobile-device-client-languages"></a>Langues du client d’appareil mobile  
 Quand vous ajoutez des prises en charge linguistiques pour des appareils mobiles, toutes les langues du client d’appareil mobile prises en charge sont incluses. Vous ne pouvez pas sélectionner individuellement les modules linguistiques pour la prise en charge linguistique sur les appareils mobiles.  

### <a name="identify-installed-language-packs"></a>Identifier les modules linguistiques installés  
Pour savoir quels modules linguistiques sont installés sur un ordinateur qui exécute le client Configuration Manager, recherchez l’ID de paramètres régionaux (LCID) des modules linguistiques installés dans le Registre de l’ordinateur. Ces informations sont disponibles à l’emplacement suivant :

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

Vous pouvez utiliser un inventaire matériel pour collecter ces informations, puis créer un rapport personnalisé contenant des informations détaillées sur les langues. Pour plus d’informations sur la collecte d’un inventaire matériel personnalisé, consultez [Guide pratique pour configurer l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md). Pour plus d’informations sur la création de rapports, consultez la section [Gérer des rapports de Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) dans la rubrique [Opérations et maintenance pour les rapports dans System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md).  
