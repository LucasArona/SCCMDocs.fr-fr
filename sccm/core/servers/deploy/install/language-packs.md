---
title: Modules linguistiques
titleSuffix: Configuration Manager
description: Découvrez la prise en charge linguistique disponible dans Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 238165dfe6822e05e64b725546837b3b4f0c496b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65497989"
---
# <a name="language-packs-in-configuration-manager"></a>Modules linguistiques dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des détails techniques sur la prise en charge linguistique dans Configuration Manager. Les clients et serveurs du site Configuration Manager sont considérés comme étant indépendants de la langue. Ajoutez la prise en charge des langues d’affichage en installant les **modules linguistiques du serveur** ou les **modules linguistiques du client** sur le site d’administration centrale et sur les sites principaux. Vous sélectionnez les langues de serveur et de client à prendre en charge sur ce site parmi les fichiers de modules linguistiques disponibles au cours du processus d’installation.
 
Installez plusieurs langues sur chaque site. Il vous suffit d’installer les langues que vous utilisez.  

- Chaque site prend en charge plusieurs langues pour les consoles Configuration Manager.  

- Sur chaque site, vous pouvez installer des modules linguistiques client individuels et ajouter ainsi une prise en charge uniquement des langues client souhaitées.  

Lorsque vous installez la prise en charge pour une langue qui correspond aux composants suivants :  

- Langue d’affichage d’un ordinateur : les consoles Configuration Manager et l’interface utilisateur client qui s’exécutent sur cet ordinateur affichent les informations dans cette langue.  

- La préférence de langue qui est en cours d’utilisation par le navigateur web d’un ordinateur : les connexions aux informations Web, notamment le catalogue d’applications et SQL Server Reporting Services, s’affichent dans cette langue.  


Lorsque vous exécutez le programme d’installation de Configuration Manager, les fichiers de modules linguistiques sont téléchargés dans le cadre des fichiers prérequis et redistribuables. Vous pouvez également utiliser le [Téléchargeur d’installation](setup-downloader.md) pour télécharger ces fichiers avant d’exécuter le programme d’installation.   



## <a name="server-languages"></a>Langues du serveur  

Aidez-vous du tableau suivant pour mapper un ID de paramètres régionaux à la langue que vous souhaitez prendre en charge sur des serveurs. Pour plus d’informations sur les ID de paramètres régionaux, consultez [ID de paramètres régionaux attribués par Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Langue du serveur|ID de paramètres régionaux (LCID)|Code en trois lettres|  
|---------------------|------------------------|-----------------------|  
|Anglais (par défaut)|0409|ENU|  
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



## <a name="client-languages"></a>Langues du client  

Aidez-vous du tableau suivant pour mapper un ID de paramètres régionaux à la langue que vous voulez prendre en charge sur des ordinateurs clients. Pour plus d’informations sur les ID de paramètres régionaux, consultez [ID de paramètres régionaux attribués par Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=252609).  

|Langue du client|ID de paramètres régionaux (LCID)|Code en trois lettres|  
|---------------------|------------------------|-----------------------|  
|Anglais (par défaut)|0409|ENG|  
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



## <a name="identify-installed-language-packs"></a>Identifier les modules linguistiques installés  
Pour savoir quels modules linguistiques sont installés sur un ordinateur qui exécute le client Configuration Manager, recherchez l’ID de paramètres régionaux (LCID) des modules linguistiques installés dans le Registre de l’ordinateur. Ces informations sont disponibles dans le chemin de registre suivant :  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Personnalisez l’inventaire matériel pour rassembler ces informations. Puis, générez un rapport personnalisé pour afficher les détails linguistiques. Pour plus d’informations sur l’inventaire matériel personnalisé, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory). Pour plus d'informations sur la création de rapports, consultez [Gérer les rapports Configuration Manager](/sccm/core/servers/manage/operations-and-maintenance-for-reporting#BKMK_ManageReports).  
