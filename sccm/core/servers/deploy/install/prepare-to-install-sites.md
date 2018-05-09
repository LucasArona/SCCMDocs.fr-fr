---
title: Préparer l’installation des sites
titleSuffix: Configuration Manager
description: Si vous avez l’intention d’installer plusieurs sites Configuration Manager, lisez ces informations pour vous aider à gagner du temps et éviter toute erreur.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f07a321ac6f10f5287a88d0df7064920f538ae5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-to-install-system-center-configuration-manager-sites"></a>Préparer l’installation de sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour préparer dans les meilleures conditions le déploiement d’un ou plusieurs sites System Center Configuration Manager, prenez connaissance des informations contenues dans cet article. Ces étapes peuvent vous faire gagner du temps durant l’installation de plusieurs sites et vous éviter des faux pas qui pourraient vous contraindre à réinstaller un ou plusieurs sites.

> [!TIP]
> Lors de la gestion de l’infrastructure de site et de hiérarchie de System Center Configuration Manager, les termes *mise à niveau*, *mise à jour* et *installation* sont utilisés pour décrire trois concepts distincts. Pour connaître la signification et l’usage de chaque terme, consultez [À propos de la mise à niveau, de la mise à jour et de l’installation de l’infrastructure de site et de hiérarchie](/sccm/core/understand/upgrade-update-install).

## <a name="bkmk_options"></a> Options d’installation de différents types de sites
Quand vous installez une nouvelle version de Configuration Manager, la version des fichiers sources que vous pouvez utiliser dépend de la version des sites qui se trouvent déjà dans la hiérarchie (le cas échéant). Les méthodes d’installation disponibles dépendent du type de site que vous souhaitez installer.  

Avant d’installer un site, veillez à élaborer le plan de votre hiérarchie et à déterminer le type de site que vous voulez installer. Pour plus d’informations, consultez [Concevoir une hiérarchie de sites](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Premier site
Le premier site que vous installez dans une hiérarchie doit être un site principal autonome ou un site d’administration centrale.

**Support d’installation** : pour installer un site d’administration centrale ou un site principal autonome comme premier site d’une nouvelle hiérarchie, vous devez [utiliser une version de base de référence](../../../../core/servers/manage/updates.md#bkmk_Baselines) de Configuration Manager. N’installez pas le premier site d’une nouvelle hiérarchie à l’aide de fichiers sources mis à jour extraits du [dossier CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) d’un site.

**Méthode d’installation** : vous pouvez installer l’un ou l’autre type de site en vous aidant de l’[Assistant Installation de Configuration Manager](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md). Vous pouvez aussi configurer un script à utiliser avec une [installation scriptée en ligne de commande](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).


### <a name="additional-sites"></a>Sites supplémentaires
Après avoir installé le site initial, vous pouvez à tout moment ajouter d’autres sites. Vous disposez des options suivantes pour ajouter des sites (jusqu’aux [limites autorisées](../../../../core/plan-design/configs/size-and-scale-numbers.md)) :

|Site existant|Type de site supplémentaire que vous pouvez installer|
|---|---|
|Site d'administration centrale|Site principal enfant|
|Site principal enfant|Site secondaire|
|Site principal autonome|Site secondaire (vous pouvez étendre le site principal, ce qui convertit le site principal autonome en site principal enfant)|

**Support d’installation** : quand vous installez un site d’administration centrale pour étendre un site principal autonome, ou que vous installez un nouveau site principal enfant dans une hiérarchie existante, vous devez utiliser le support d’installation (qui contient les fichiers sources) qui correspond à la version du ou des sites existants.

> [!IMPORTANT]
> Si vous avez installé des mises à jour dans la console qui ont changé la version des sites installés précédemment, n’utilisez pas le support d’installation d’origine. Utilisez plutôt les fichiers sources du [dossier CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) d’un site mis à jour. Configuration Manager vous impose d’utiliser des fichiers sources qui correspondent à la version du site existant auquel votre nouveau site doit se connecter.

Un site secondaire doit être installé à partir de la console Configuration Manager. De cette façon, les sites secondaires sont toujours installés à l’aide des fichiers sources à partir du site principal parent.

**Méthode d’installation** : la méthode que vous utilisez pour installer des sites supplémentaires dépend du type de site que vous voulez installer.
-   **Ajouter un site d’administration centrale** : vous pouvez utiliser l’Assistant Installation de Configuration Manager ou une ligne de commande scriptée pour installer le nouveau site d’administration centrale comme site parent de votre site principal autonome existant. Pour plus d’informations, consultez [Extension d’un site principal autonome](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
-   **Ajouter un site principal enfant** : vous pouvez utiliser l’Assistant Installation de Configuration Manager ou une installation en ligne de commande pour ajouter un site principal enfant sous un site d’administration centrale.
-   **Ajouter un site secondaire** : utilisez la console Configuration Manager pour installer un site secondaire comme site enfant sous un site principal. Les autres méthodes ne sont pas prises en charge pour l’ajout de sites secondaires.

## <a name="bkmk_tasks"></a>  Tâches courantes à effectuer avant de commencer une installation
-   **Déterminer la topologie de la hiérarchie que vous allez utiliser pour votre déploiement**    
Pour plus d’informations, consultez [Concevoir une hiérarchie de sites pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

-   **Préparer et configurer des serveurs individuels pour respecter les prérequis et les configurations prises en charge en vue d’une utilisation avec Configuration Manager**         
Pour plus d’informations, consultez [Prérequis des sites et systèmes de site](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

-   **Installer et configurer SQL Server pour héberger la base de données du site**     
Pour plus d’informations, consultez [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   **Préparer votre environnement réseau pour prendre en charge Configuration Manager**      
Pour plus d’informations, consultez [Configurer les pare-feu, les ports et les domaines pour préparer votre infrastructure pour Configuration Manager](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Si vous prévoyez d’utiliser une infrastructure à clé publique (PKI), préparer votre infrastructure et vos certificats**      
Pour plus d’informations, consultez [Configuration requise des certificats PKI pour Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

-   **Installer les dernières mises à jour de sécurité sur les ordinateurs que vous devez utiliser comme serveurs de site ou serveurs de système de site et les redémarrer si nécessaire**

## <a name="bkmk_sitecodes"></a>  À propos des noms de site et des codes de site
Les codes de site et les noms de site permettent d’identifier et de gérer les sites dans une hiérarchie Configuration Manager. Dans la console Configuration Manager, le code de site et le nom de site s’affichent au format &lt;*code_site*\> - &lt;*nom_site*\>. Chaque code de site que vous utilisez dans votre hiérarchie doit être unique. Si le schéma Active Directory est étendu pour Configuration Manager et que vos sites publient des données, les codes de site utilisés dans une forêt Active Directory doivent être uniques, même s’ils sont utilisés dans une autre hiérarchie Configuration Manager ou s’ils ont été utilisés dans des installations précédentes de Configuration Manager. Veillez à planifier correctement vos codes et noms de site avant de déployer votre hiérarchie.

### <a name="specify-a-site-code-and-site-name"></a>Spécifier un code de site et un nom de site
Quand vous exécutez le programme d’installation de Configuration Manager, vous êtes invité à fournir un code de site et un nom de site pour le site d’administration centrale, et pour l’installation de chaque site principal et secondaire. Un code de site doit identifier chaque site de façon unique dans la hiérarchie. Le code de site étant utilisé dans les noms de dossiers, n’utilisez jamais les noms suivants comme code de site, notamment les noms réservés à Configuration Manager et à Windows :
  -  AUX
  -  CON
  -  NUL
  -  PRN
  -  SMS

> [!NOTE]
> Le programme d’installation de Configuration Manager ne vérifie pas si un code de site est déjà utilisé.

Pour entrer le code de site pour un site quand vous exécutez le programme d’installation de Configuration Manager, vous devez entrer trois caractères alphanumériques. Seules les lettres de *A* à *Z* et les nombres de *0* à *9*, dans n’importe quelle combinaison, sont autorisés dans les codes de site. La séquence de lettres ou de chiffres n'influe en rien sur la communication entre les sites. Par exemple, il n’est pas nécessaire de nommer un site principal *ABC* et un site secondaire *DEF*.

Le nom du site est un identificateur de nom convivial pour ce site. Vous pouvez utiliser uniquement les caractères de *A* à *Z*, de *a* à *z* et de *0* à *9*, ainsi que le tiret (*-*) dans les noms des sites.

> [!IMPORTANT]
> La modification du code de site ou du nom de site après l’installation du site n’est pas prise en charge.

### <a name="reuse-a-site-code"></a>Réutiliser un code de site
Les codes de site ne peuvent pas être utilisés plusieurs fois dans une hiérarchie Configuration Manager pour un site d’administration centrale ou un site principal, même si le site et le code de site d’origine ont été désinstallés. Si vous réutilisez un code de site, vous risquez d’avoir des conflits d’ID d’objet dans votre hiérarchie. Vous pouvez réutiliser le code de site d’un site secondaire si ce site secondaire et le code de site ne sont plus utilisés dans votre hiérarchie Configuration Manager ou dans la forêt Active Directory.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limites et restrictions concernant les sites installés
Avant d’installer un site, vous devez connaître les limitations suivantes qui s’appliquent aux sites et aux hiérarchies :
-   Après l’exécution du programme d’installation, vous ne pouvez modifier les propriétés suivantes du site qu’en désinstallant le site et en le réinstallant avec les nouvelles valeurs :  
  -   Répertoire d’installation des fichiers programmes  
  -   Code de site  
  -   Description du site  
-   Si votre hiérarchie comprend un site d’administration centrale :  
  -   Configuration Manager ne permet pas de retirer un site principal enfant d’une hiérarchie pour en faire un site principal autonome ou pour le rattacher à une autre hiérarchie. Au lieu de cela, vous devez désinstaller le site principal enfant et le réinstaller comme nouveau site principal autonome ou comme site enfant du site d’administration centrale d’une autre hiérarchie.  


## <a name="bkmk_optionalsteps"></a>  Étapes facultatives avant d’exécuter le programme d’installation
**Exécuter manuellement le[Téléchargeur d’installation](../../../../core/servers/deploy/install/setup-downloader.md)**

Pour télécharger les fichiers d’installation mis à jour pour Configuration Manager, vous pouvez exécuter le Téléchargeur d’installation. Si l’ordinateur sur lequel vous voulez exécuter le programme d’installation n’est pas connecté à Internet, ou si vous prévoyez d’installer plusieurs serveurs de site, utilisez le Téléchargeur d’installation pour télécharger les mises à jour requises du programme d’installation. Voici des informations supplémentaires :
-  Par défaut, le programme d’installation se connecte à Internet pour télécharger les fichiers du programme d’installation mis à jour.
-  Par défaut, les fichiers sont stockés dans le dossier Redist.
-  Vous pouvez diriger le programme d’installation vers un emplacement sur votre réseau où vous avez précédemment stocké une copie de ces fichiers.

**Exécuter manuellement l’[Outil de vérification des conditions préalables](../../../../core/servers/deploy/install/prerequisite-checker.md)**

Pour identifier et résoudre les problèmes avant d’exécuter le programme d’installation pour installer un site et avant d’installer un rôle de système de site sur un serveur, vous pouvez exécuter l’Outil de vérification des prérequis. Cet outil permet de vérifier que l’ordinateur remplit les conditions requises pour héberger le site ou le rôle de système de site. Voici des informations supplémentaires :
 -  Par défaut, le programme d’installation exécute l’Outil de vérification des prérequis.
 -  En cas d’erreur, le programme d’installation s’arrête jusqu’à ce que le problème soit résolu.

**Identifier des ports facultatifs**

Vous pouvez identifier des ports facultatifs pouvant être utilisés par les clients et les systèmes de site. Voici des informations supplémentaires :
 -  Par défaut, les systèmes de site et les clients utilisent des ports prédéfinis pour communiquer.
 -  Pendant l’installation, vous pouvez configurer d’autres ports.

 Pour plus d’informations, consultez [Ports utilisés dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/ports.md).
