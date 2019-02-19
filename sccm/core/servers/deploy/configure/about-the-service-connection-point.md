---
title: point de connexion de service
titleSuffix: Configuration Manager
description: Découvrez ce rôle système de site Configuration Manager, puis comprenez et planifiez sa plage d’utilisations.
ms.date: 08/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7a6040fd6b429eb94187026b8b6a98ea1386d5c6
ms.sourcegitcommit: fd16fc2b681608fd6def5bad2cedffbcd1f2423a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/18/2019
ms.locfileid: "56405639"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>À propos du point de connexion de service dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le point de connexion de service est un rôle de système de site qui remplit plusieurs fonctions importantes pour la hiérarchie. Avant de configurer le point de connexion de service, vous devez comprendre et planifier sa plage d’utilisation. La planification de l’utilisation peut affecter la manière dont vous configurez ce rôle de système de site :  

- **Gérer les appareils mobiles avec Microsoft Intune** : Ce rôle remplace le connecteur Windows Intune utilisé par les versions précédentes de Configuration Manager et peut être configuré avec les détails de votre abonnement Intune. Pour plus d’informations, consultez [Gestion hybride des appareils mobiles (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management).  

- **Gérer des appareils mobiles avec une gestion des données de référence locale** : Ce rôle assure la prise en charge des appareils locaux que vous gérez et qui ne se connectent pas à Internet. Pour plus d'informations, consultez [Gérer des appareils mobiles avec une infrastructure locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  

- **Charger les données d’utilisation à partir de votre infrastructure Configuration Manager** : Vous pouvez contrôler le niveau ou la quantité de détails que vous chargez. Les données chargées permettent ce qui suit :  

    - identifier et résoudre les problèmes de manière proactive ;  

    - améliorer nos produits et services ;  

    - identifier les mises à jour pour Configuration Manager applicables à la version de Configuration Manager que vous utilisez.  

    Pour plus d’informations sur les données collectées par chaque niveau et sur la façon de changer le niveau de regroupement après l’installation du rôle, consultez la page [Données d’utilisation et de diagnostic](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data). Ensuite, suivez le lien correspondant à la version de Configuration Manager que vous utilisez.  

    Pour plus d’informations, consultez [Paramètres et niveaux de données d’utilisation](/sccm/core/servers/deploy/install/setup-reference#bkmk_usage).  

- **Télécharger les mises à jour applicables à votre infrastructure Configuration Manager** : Seules les mises à jour appropriées pour votre infrastructure sont disponibles, en fonction des données d’utilisation que vous chargez.  

- **Chaque hiérarchie prend en charge une seule instance de ce rôle** :  

    - Ce rôle de système de site ne peut être installé que sur le site de niveau supérieur de votre hiérarchie (site d’administration centrale ou site principal autonome).  

    - Si vous étendez un site principal autonome à une hiérarchie plus importante, vous devez désinstaller ce rôle du site principal pour pouvoir l’installer ensuite sur le site d’administration centrale.  


##  <a name="bkmk_modes"></a> Modes opératoires  
Le point de connexion de service prend en charge deux modes de fonctionnement :  

- En **mode en ligne**, le point de connexion de service recherche automatiquement les mises à jour toutes les 24 heures. Il télécharge dans la console Configuration Manager les nouvelles mises à jour disponibles pour la version actuelle de vos infrastructure et produits.  

- En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft. Pour importer manuellement les mises à jour disponibles, utilisez [l’outil de connexion de service](/sccm/core/servers/manage/use-the-service-connection-tool).  

Quand vous basculez entre le mode en ligne ou hors connexion après avoir installé le point de connexion de service, vous devez redémarrer le thread SMS_DMP_DOWNLOADER du service SMS_Executive Configuration Manager pour appliquer cette modification. Vous pouvez utiliser Configuration Manager Service Manager pour redémarrer uniquement le thread SMS_DMP_DOWNLOADER du service SMS_Executive. Vous pouvez également redémarrer le service SMS_Executive pour Configuration Manager, ce qui redémarre la plupart des composants de site. Sinon, vous pouvez attendre une tâche planifiée, comme une sauvegarde de site, qui arrête puis redémarre ensuite le service SMS_Executive pour vous.  

Pour utiliser le Gestionnaire de service de Configuration Manager, dans la console, accédez à **Surveillance** > **État du système** > **État du composant**, choisissez **Démarrer**, puis **Gestionnaire de service de Configuration Manager**. Dans le Gestionnaire de service :  

- Dans le volet de navigation, développez le site, développez **Composants**, puis choisissez le composant à redémarrer.  

- Dans le volet d’informations, cliquez avec le bouton droit sur le composant, puis choisissez **Requête**.  

- Une fois l’état du composant confirmé, recliquez avec le bouton droit sur le composant, puis choisissez **Arrêter**.  

- **Réinterrogez** le composant pour confirmer qu’il est arrêté. Recliquez avec le bouton droit sur le composant, puis choisissez **Démarrer**.  

> [!IMPORTANT]  
> Le processus qui ajoute un abonnement Microsoft Intune au point de connexion de service définit automatiquement le rôle de système de site en ligne. Le point de connexion de service ne prend pas en charge le mode hors connexion en cas de configuration avec un abonnement Intune.  

**Quand le rôle s’installe sur un ordinateur distant du serveur de site :**  

- Le compte d’ordinateur du serveur de site doit être un administrateur local sur l’ordinateur qui héberge une connexion de service distant.

- Vous devez configurer le serveur de système de site qui héberge le rôle avec un compte d’installation du système de site.  

- Le gestionnaire de distribution sur le serveur de site utilise le compte d’installation du système de site pour transférer les mises à jour à partir du point de connexion de service.

##  <a name="bkmk_urls"></a> Conditions requises pour l’accès Internet  
Pour activer le fonctionnement, l’ordinateur qui héberge le point de connexion de service et les éventuels pare-feu entre cet ordinateur et Internet doivent transmettre les communications via le port sortant **TCP 443** pour HTTPS et le port sortant **TCP 80** pour HTTP aux emplacements Internet suivants. Le point de connexion de service prend également en charge l’utilisation d’un proxy web (avec ou sans authentification) pour utiliser ces emplacements. Si vous devez configurer un compte de proxy web, consultez la page [Prise en charge du serveur proxy](/sccm/core/plan-design/network/proxy-server-support).

> [!TIP]  
> Le point de connexion de service utilise le service Microsoft Intune lorsqu’il se connecte à go.microsoft.com ou manage.Microsoft.com. Un problème est connu sur le connecteur Intune qui rencontre une défaillance de connectivité si le certificat racine Baltimore CyberTrust n’est pas installé, a expiré ou est endommagé sur le point de connexion de service. Pour plus d’informations, consultez la page [Le point de connexion de service ne télécharge pas les mises à jour](https://support.microsoft.com/help/3187516).  

#### <a name="updates-and-servicing"></a>Mises à jour et maintenance

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

#### <a name="microsoft-intune"></a>Microsoft Intune

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

#### <a name="windows-10-servicing"></a>Maintenance de Windows 10

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

#### <a name="azure-services"></a>Services Azure

- `management.azure.com`  

## <a name="install-the-service-connection-point"></a>Installer le point de connexion de service
Quand vous exécutez le **programme d’installation** pour installer le site de plus haut niveau d’une hiérarchie, vous avez la possibilité d’installer le point de connexion de service.

Après l’exécution du programme d’installation ou si vous réinstallez le rôle de système de site, utilisez l’Assistant **Ajout des rôles de système de site** ou l’Assistant **Créer un serveur de système de Site** pour installer le système de site sur un serveur au plus haut niveau de votre hiérarchie (c’est-à-dire le site d’administration centrale ou un site principal autonome). Les deux Assistants se trouvent sous l’onglet **Accueil** dans la console, dans **Administration** > **Configuration du site** > **Serveurs et rôles de système de Site**.



## <a name="log-files-used-by-the-service-connection-point"></a>Fichiers journaux utilisés par le point de connexion de service
Pour consulter des informations sur les chargements vers Microsoft, affichez **Dmpuploader.log** sur l’ordinateur qui exécute le point de connexion de service.  Pour voir les téléchargements, y compris la progression du téléchargement des mises à jour, affichez **Dmpdownloader.log**. Pour obtenir la liste complète des journaux liés au point de connexion de service, consultez [Point de connexion de service](/sccm/core/plan-design/hierarchy/log-files#BKMK_WITLog) dans l’article sur les fichiers journaux de Configuration Manager.

Vous pouvez également utiliser les organigrammes suivants pour comprendre le flux des processus et les entrées du journal principales pour le téléchargement et la réplication des mises à jour vers d’autres sites :
- [Organigramme - Téléchargement des mises à jour](/sccm/core/servers/manage/download-updates-flowchart)
- [Organigramme - Réplication de mise à jour](/sccm/core/servers/manage/update-replication-flowchart)
