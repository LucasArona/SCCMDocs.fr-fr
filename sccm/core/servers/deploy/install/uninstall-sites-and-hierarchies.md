---
title: Désinstaller des sites
titleSuffix: Configuration Manager
description: Utilisez ces informations comme référence pour désinstaller un site System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d466edd2-97f0-44c1-a73e-d71abbdbf4a8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0f87975d660a94d04cdd7d0e10816b6e2815fe53
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="uninstall-sites-and-hierarchies-in-system-center-configuration-manager"></a>Désinstaller des sites et des hiérarchies dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations suivantes comme référence si vous devez désinstaller un site System Center Configuration Manager.  

Pour retirer une hiérarchie comportant plusieurs sites, l’ordre de suppression est important. Commencez par désinstaller les sites en bas de la hiérarchie, puis remontez la hiérarchie :  

1.  Supprimez les sites secondaires rattachés aux sites principaux.  
2.  Supprimez les sites principaux.
3.  Une fois tous les sites principaux supprimés, vous pouvez désinstaller le site d’administration centrale.  


##  <a name="BKMK_RemoveSecondarysite"></a> Supprimer un site secondaire d’une hiérarchie  
Vous ne pouvez pas déplacer ou réattribuer un site secondaire à un nouveau site principal parent. Pour supprimer un site secondaire d’une hiérarchie, vous devez le supprimer de son site parent direct. Pour ce faire, utilisez l’Assistant Suppression d’un site secondaire de la console Configuration Manager. Lors de la suppression d’un site secondaire, vous devez choisir entre le supprimer et le désinstaller :  

-   **Désinstaller le site secondaire**. Utilisez cette option pour supprimer un site secondaire fonctionnel accessible à partir du réseau. Cette option désinstalle Configuration Manager du serveur de site secondaire et supprime toutes les informations relatives au site et ses ressources de la hiérarchie de sites Configuration Manager. Si Configuration Manager a installé SQL Server Express dans le cadre de l’installation du site secondaire, SQL Express est désinstallé en même temps que le site secondaire. En revanche, si SQL Server Express a été installé avant le site secondaire, Configuration Manager ne désinstalle pas SQL Server Express.  

-   **Supprimer le site secondaire**. Utilisez cette option dans l'un des cas de figure suivants :  

    -   L’installation d’un site secondaire a échoué  
    -   Le site secondaire continue de figurer dans la console Configuration Manager après sa désinstallation

    Cette option supprime toutes les informations relatives au site et ses ressources de la hiérarchie Configuration Manager, mais laisse Configuration Manager installé sur le serveur de site secondaire.  

    > [!NOTE]  
    >  Vous pouvez également utiliser l’outil de maintenance hiérarchique et l’option **/DELSITE** pour supprimer un site secondaire. Pour plus d’informations, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

#### <a name="to-uninstall-or-delete-a-secondary-site"></a>Pour désinstaller ou supprimer un site secondaire  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d’administration sur l’ordinateur de site secondaire  
    -   Droits d’administrateur local sur le serveur de base de données de site distant pour le site principal, s’il est distant  
    -   Rôle de sécurité d’administrateur d’infrastructure ou d’administrateur complet sur le site principal parent  
    -   Droits d’administrateur système sur la base de données de site du site secondaire  

2.  Dans la console Configuration Manager, sélectionnez **Administration**.  
3.  Dans l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**.  
4.  Sélectionnez le serveur de site secondaire à supprimer.  
5.  Sous l’onglet **Accueil**, dans le groupe **Site**, sélectionnez **Supprimer**.  
6.  Dans la page **Général**, indiquez si vous souhaitez désinstaller ou supprimer le site secondaire, puis cliquez sur **Suivant**.  
7.  Vérifiez les paramètres de la page **Résumé**, puis sélectionnez **Suivant**.  
8.  Dans la page **Dernière étape**, sélectionnez **Fermer** pour quitter l’Assistant.  

##  <a name="BKMK_UninstallPrimary"></a> Désinstaller un site principal  
Vous pouvez exécuter le programme d’installation de Configuration Manager pour désinstaller un site principal auquel aucun site secondaire n’est associé. Avant de désinstaller un site principal, prenez connaissance des remarques suivantes :  

-   Quand des clients Configuration Manager se trouvent dans les limites configurées au niveau du site et que le site principal fait partie d’une hiérarchie Configuration Manager, envisagez d’ajouter les limites à un autre site principal de la hiérarchie avant de désinstaller le site principal.  
-   Lorsque le serveur de site principal n'est plus disponible, vous devez utiliser l'outil de maintenance hiérarchique au niveau du site d'administration centrale afin de supprimer le site principal de la base de données de site. Pour plus d’informations, consultez [Outil de maintenance hiérarchique (Preinst.exe) pour System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

Pour désinstaller un site principal, suivez les instructions ci-dessous.  

#### <a name="to-uninstall-a-primary-site"></a>Pour désinstaller un site principal  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d’administrateur local sur le serveur de site d’administration centrale  
    -   Droits d’administrateur local sur le serveur de base de données de site distant pour le site d’administration centrale, s’il est distant
    -   Droits d'administrateur système sur la base de données du site d'administration centrale  
    -   Droits d’administrateur local sur l’ordinateur de site principal  
    -   Droits d’administrateur local sur le serveur de base de données de site distant pour le site principal, s’il est distant  
    -   Nom d’utilisateur associé au rôle de sécurité Administrateur d’infrastructure ou au rôle Administrateur complet sur le site d’administration centrale  

2.  Démarrez le programme d’installation de Configuration Manager sur le serveur de site principal en utilisant l’une des méthodes suivantes :  

    -   Dans le menu **Démarrer**, sélectionnez **Installation de Configuration Manager**.  
    -   Ouvrez Setup.exe à partir de &lt;*SupportInstallationConfigMgr*>\SMSSETUP\BIN\X64.  
    -   Ouvrez Setup.exe à partir de &lt;*CheminInstallationConfigMgr*>\BIN\X64.  

3.  Dans la page **Avant de commencer**, sélectionnez **Suivant**.  
4.  Dans la page **Mise en route**, sélectionnez **Désinstaller le site Configuration Manager**, puis sélectionnez **Suivant**.  
5.  Dans la page **Désinstaller le site Configuration Manager**, indiquez si vous souhaitez supprimer la base de données de site du serveur de site principal et si vous souhaitez supprimer la console Configuration Manager. Par défaut, le programme d'installation supprime les deux éléments.  

    > [!IMPORTANT]  
    >  Lorsqu'un site secondaire est associé au site principal, vous devez au préalable supprimer le site secondaire pour pouvoir désinstaller le site principal.  

6.  Sélectionnez **Oui** pour confirmer la désinstallation du site principal Configuration Manager.  

##  <a name="BKMK_UninstallPrimaryDistViews"></a> Désinstaller un site principal configuré avec des vues distribuées  
 Pour pouvoir désinstaller un site principal enfant dont le lien de réplication vers le site d’administration centrale contient des vues distribuées, vous devez désactiver les vues distribuées dans votre hiérarchie. Avant de désinstaller un site principal, aidez-vous des informations ci-dessous pour désactiver les vues distribuées.  

#### <a name="to-uninstall-a-primary-site-that-is-configured-with-distributed-views"></a>Pour désinstaller un site principal configuré avec des vues distribuées  

1.  Avant de désinstaller un site principal, vous devez désactiver les vues distribuées sur chaque lien de la hiérarchie reliant le site d’administration centrale et un site principal.  
2.  Après avoir désactivé les vues distribuées sur chaque lien, vérifiez que les données du site principal sont bien réinitialisées au niveau du site d’administration centrale. Pour surveiller l’initialisation des données, dans la console Configuration Manager, dans l’espace de travail **Surveillance**, affichez le lien dans le nœud **Réplication de la base de données**.  
3.  Une fois les données réinitialisées auprès du site d'administration centrale, vous pouvez désinstaller le site principal. Pour désinstaller un site principal, consultez [Désinstaller un site principal](#BKMK_UninstallPrimary).  
4.  Une fois le site principal entièrement désinstallé, vous pouvez reconfigurer les vues distribuées sur les liens vers les sites principaux.  

    > [!IMPORTANT]  
    >  Si vous désinstallez le site principal avant de désactiver les vues distribuées de chaque site ou avant de réinitialiser les données du site principal au niveau du site d’administration centrale, la réplication des données entre les sites principaux et le site d’administration centrale risque d’échouer. Dans ce scénario, vous devez désactiver les vues distribuées pour chaque lien de la hiérarchie de sites, puis une fois que les données ont bien été réinitialisées au niveau du site d’administration centrale, vous pouvez reconfigurer les vues distribuées.  

##  <a name="BKMK_UninstallCAS"></a> Désinstaller le site d’administration centrale  
 Vous pouvez exécuter le programme d’installation de Configuration Manager pour désinstaller un site d’administration centrale qui n’a pas de sites principaux enfants. Pour désinstaller un site d'administration centrale, suivez les instructions ci-dessous.  

#### <a name="to-uninstall-a-central-administration-site"></a>Pour désinstaller un site d'administration centrale  

1.  Vérifiez que l'utilisateur administratif exécutant le programme d'installation possède les droits de sécurité suivants :  

    -   Droits d’administrateur local sur le serveur de site d’administration centrale  
    -   Droits d’administrateur local sur le serveur de base de données de site pour le site d’administration centrale, si le serveur de base de données de site n’est pas installé sur le serveur de site 

2.  Démarrez le programme d’installation de Configuration Manager sur le serveur de site d’administration centrale en utilisant l’une des méthodes suivantes :  

    -   Dans le menu **Démarrer**, cliquez sur **Installation de Configuration Manager**.  
    -   Ouvrez Setup.exe à partir de &lt;*SupportInstallationConfigMgr*>\SMSSETUP\BIN\X64.  
    -   Ouvrez Setup.exe à partir de &lt;*CheminInstallationConfigMgr*>\BIN\X64.  

3.  Dans la page **Avant de commencer**, sélectionnez **Suivant**.  
4.  Dans la page **Mise en route**, sélectionnez **Désinstaller le site Configuration Manager**, puis sélectionnez **Suivant**.  
5.  Dans la page **Désinstaller le site Configuration Manager**, indiquez si vous souhaitez supprimer la base de données de site du serveur de site d’administration centrale et si vous souhaitez supprimer la console Configuration Manager. Par défaut, le programme d'installation supprime les deux éléments.  

    > [!IMPORTANT]  
    >  Si un site principal est associé au site d'administration centrale, vous devez désinstaller le site principal pour pouvoir désinstaller le site d'administration centrale.  

6.  Sélectionnez **Oui** pour confirmer la désinstallation du site d’administration centrale Configuration Manager.  
