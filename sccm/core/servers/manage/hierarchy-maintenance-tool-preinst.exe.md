---
title: Outil de maintenance de la hiérarchie
titleSuffix: Configuration Manager
description: Découvrez comment utiliser l’outil de maintenance hiérarchique, et en quoi il est utile. Inclut des informations techniques de référence sur les options de ligne de commande.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4dd1bf9b4085b6e1591d5841bfc307398505f5d1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-system-center-configuration-manager"></a>Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’outil de maintenance hiérarchique (Preinst.exe) transfère des commandes au service Gestionnaire de hiérarchie de System Center Configuration Manager, si ce service est en cours d’exécution. Quand vous installez un site Configuration Manager, l’outil de maintenance hiérarchique est automatiquement installé. Preinst.exe se trouve dans le dossier partagé \\&lt;*nom_serveur_site*>\SMS_&lt;*code_site*\bin\X64\00000409 sur le serveur de site.  

 Vous pouvez utiliser l'outil de maintenance hiérarchique dans les cas suivants :  

-   Quand l'échange de clé sécurisé est requis, il existe des situations dans lesquelles vous devez effectuer manuellement l'échange initial de clé publique entre les sites. Pour plus d'informations, consultez [Échanger manuellement des clés publiques entre des sites](#BKMK_ManuallyExchangeKeys) dans cette rubrique.  

-   Pour supprimer les tâches actives qui concernent un site de destination qui n'est plus disponible.  

-   Pour supprimer un serveur de site de la console Configuration Manager quand vous ne pouvez pas désinstaller le site à l’aide du programme d’installation. Par exemple, si vous supprimez physiquement un site Configuration Manager sans exécuter d’abord le programme d’installation pour désinstaller le site, les informations du site sont conservées dans la base de données du site parent, lequel continuera d’essayer de communiquer avec le site enfant supprimé. Pour résoudre ce problème, vous devez exécuter l’outil de maintenance hiérarchique et supprimer manuellement le site enfant de la base de données du site parent.  

-   Pour arrêter simultanément tous les services Configuration Manager sur un site, et éviter ainsi d’avoir à les arrêter un à un.  

-   Lorsque vous restaurez un site, vous pouvez utiliser l'option CHILDKEYS pour distribuer les clés publiques à partir de plusieurs sites enfants vers le site de récupération.  

Pour exécuter l'outil de maintenance hiérarchique, l'utilisateur doit disposer de privilèges d'administration sur l'ordinateur local. De plus, l'utilisateur doit disposer de façon explicite du droit de sécurité d'administration du site. Le fait d'hériter de ce droit par l'appartenance à un groupe qui dispose de ce droit n'est pas suffisant.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Options de ligne de commande de l'outil de maintenance hiérarchique  
Lorsque vous utilisez l'outil de maintenance hiérarchique, vous devez l'exécuter localement sur le site d'administration centrale, le site principal ou le serveur de site secondaire.  

Pour exécuter l’outil de maintenance hiérarchique, utilisez la syntaxe suivante : preinst.exe /&lt;option\>. Les options de ligne de commande sont les suivantes.  

 **/DELJOB &lt;*Code_site*>**  : utilisez cette option sur un site pour supprimer l’ensemble des travaux ou commandes entre le site actuel et le site de destination spécifié.  

 **/DELSITE &lt;*code_site_enfant_à_supprimer*>**  : utilisez cette option sur un site parent pour supprimer les données des sites enfants dans la base de données de site du site parent. En règle générale, cette option est utilisée si un ordinateur du serveur de site est désactivé avant de désinstaller le site à partir de celui-ci.  

> [!NOTE]  
>  L'option /DELSITE ne désinstalle pas le site sur l'ordinateur spécifié par le paramètre ChildSiteCodeToRemove. Cette option supprime uniquement les informations du site dans la base de données de site Configuration Manager.  

**/DUMP &lt;*code_site*>**  : utilisez cette option sur le serveur de site local pour écrire des images de contrôle de site dans le dossier racine du lecteur sur lequel le site est installé. Vous pouvez écrire une image de contrôle de site spécifique dans le dossier ou écrire tous les fichiers de contrôle de site de la hiérarchie.  

-   /DUMP &lt;*code_site*> écrit l’image de contrôle de site uniquement pour le site spécifié.  

-   /DUMP écrit les fichiers de contrôle de site pour tous les sites.  

Une image est une représentation binaire du fichier de contrôle de site, stockée dans la base de données de site Configuration Manager. L'image du fichier de contrôle de site enregistrée représente la somme de l'image de base et des images delta en attente.  

Une fois l’image du fichier de contrôle de site supprimée à l’aide de l’outil de maintenance hiérarchique, le nom du fichier est au format sitectrl_&lt;*code_site*>.ct0.  

**/STOPSITE** : utilisez cette option sur le serveur de site local pour lancer un cycle d’arrêt du service Gestionnaire de composant de site dans Configuration Manager, ce qui réinitialise partiellement le site. L’exécution de ce cycle d’arrêt entraîne l’arrêt de certains services Configuration Manager sur un serveur de site et ses systèmes de site distants. Ces services sont marqués en vue d'être réinstallés. À la suite de ce cycle d'arrêt, certains mots de passe sont automatiquement modifiés lorsque les services sont réinstallés.  

> [!NOTE]  
>  Si vous souhaitez enregistrer un arrêt, une réinstallation et un changement de mot de passe pour le Gestionnaire de composants de site, activez l'enregistrement de ce composant avant de vous servir de cette option de ligne de commande.  

Après le démarrage du cycle d'arrêt, il fonctionne automatiquement en ignorant les composants et les ordinateurs qui ne répondent pas. Toutefois, si le service Gestionnaire de composants de site ne peut pas accéder à un système de site distant pendant le cycle d'arrêt, les composants installés sur ce système de site sont réinstallés au prochain démarrage du Gestionnaire de composants de site. Lors de son redémarrage, le service Gestionnaire de composants de site tente plusieurs réinstallations de tous les services marqués en vue d'une réinstallation, jusqu'à ce qu'il réussisse.  

Vous pouvez redémarrer le service Gestionnaire de composants de site avec le Gestionnaire de services. Après son redémarrage, tous les services affectés sont désinstallés, réinstallés et redémarrés. Lorsque vous avez utilisé l'option /STOPSITE pour initialiser un cycle d'arrêt, vous ne pouvez pas éviter les cycles de réinstallation après le redémarrage du service Gestionnaire de composants de site.  

**/KEYFORPARENT** - Utilisez cette option sur un site pour distribuer la clé publique du site à un site parent.  

L’option /KEYFORPARENT copie la clé publique du site dans le fichier &lt;*code_site*>.CT4 situé à la racine du lecteur des fichiers programme. Après avoir exécuté preinst.exe avec cette option, copiez manuellement le fichier &lt;*code_site*>.CT4 dans le dossier ...\Inboxes\hman.box (et non pas hman.box\pubkey) du site parent.  

**/KEYFORCHILD** - Utilisez cette option sur un site pour distribuer la clé publique du site à un site enfant.  

L’option /KEYFORCHILD copie la clé publique du site dans le fichier &lt;*code_site*>.CT5 à la racine du lecteur des fichiers programme. Après avoir exécuté preinst.exe avec cette option, copiez manuellement le fichier &lt;*code_site*>.CT5 dans le dossier ...\Inboxes\hman.box (et non pas hman.box\pubkey) du site enfant.  

**/CHILDKEYS** - Vous pouvez utiliser cette option sur les sites enfants d’un site que vous récupérez. Utilisez cette option pour distribuer les clés publiques de plusieurs sites enfants sur le site en cours de récupération.  

L’option /CHILDKEYS copie la clé du site sur lequel vous exécutez l’option, et toutes les clés publiques des sites enfants de ce site, dans le fichier &lt;*code_site*>.CT6.  

Après avoir exécuté preinst.exe avec cette option, copiez manuellement le fichier &lt;*code_site*>.CT6 dans le dossier ...\Inboxes\hman.box (et non pas hman.box\pubkey) du site en cours de récupération.  

**/PARENTKEYS** - Vous pouvez utiliser cette option sur le site parent d’un site que vous récupérez. Utilisez cette option pour distribuer les clés publiques de tous les sites parents sur le site en cours de récupération.  

L’option /PARENTKEYS copie la clé du site sur lequel vous exécutez l’option, ainsi que les clés de chaque site parent situé au-dessus de ce site, dans le fichier &lt;code_site\>.CT7.  

Après avoir exécuté preinst.exe avec cette option, copiez manuellement le fichier &lt;*code_site*>.CT7 dans le dossier ...\Inboxes\hman.box (et non pas hman.box\pubkey) du site en cours de récupération.  

##  <a name="BKMK_ManuallyExchangeKeys"></a> Échanger manuellement des clés publiques entre des sites  
Par défaut, l’option **Nécessite l’échange de clés sécurisées** est activée pour les sites Configuration Manager. Quand l'échange de clé sécurisé est requis, il existe deux situations dans lesquelles vous devez effectuer manuellement l'échange initial de clé entre les sites :  

-   Le schéma Active Directory n’a pas été étendu pour Configuration Manager.  

-   Les sites Configuration Manager ne publient pas de données de site dans Active Directory.  

Vous pouvez utiliser l'outil de maintenance hiérarchique pour exporter les clés publiques pour chaque site. Une fois qu'elles ont été exportées, vous devez échanger manuellement les clés entre les sites.  

> [!NOTE]  
>  Après l'échange manuel des clés, vous pouvez consulter le fichier journal **hman.log** , qui enregistre les modifications de la configuration du site et la publication des informations du site vers les services de domaine Active Directory, sur le serveur du site parent pour vous assurer que le site principal a traité la nouvelle clé publique.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Pour transférer manuellement la clé publique du site enfant vers le site parent  

1.  Lorsque vous êtes connecté au site enfant, ouvrez une invite de commande et naviguez jusqu'à l'emplacement de **Preinst.exe**.  

2.  Tapez la commande suivante pour exporter la clé publique du site enfant : **Preinst /keyforparent**  

3.  L’option /keyforparent copie la clé publique du site enfant dans le fichier **&lt;code_site\>.CT4** situé à la racine du lecteur système.  

4.  Déplacez le fichier **&lt;code_site\>.CT4** vers le dossier **&lt;répertoire_installation\>\inboxes\hman.box** du site parent.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Pour transférer manuellement la clé publique du site parent vers le site enfant  

1.  Lorsque vous êtes connecté au site parent, ouvrez une invite de commande et naviguez jusqu'à l'emplacement de **Preinst.exe**.  

2.  Tapez la commande suivante pour exporter la clé publique du site parent : **Preinst /keyforchild**.  

3.  L’option /keyforchild copie la clé publique du site parent dans le fichier **&lt;code_site\>.CT5** situé à la racine du lecteur système.  

4.  Déplacez le fichier **&lt;code_site\>.CT5** vers le dossier **&lt;répertoire_installation\>\inboxes\hman.box** du site enfant.  
