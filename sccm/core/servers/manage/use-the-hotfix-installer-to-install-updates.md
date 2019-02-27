---
title: Programme d’installation de correctif logiciel
titleSuffix: Configuration Manager
description: Découvrez quand et comment installer des mises à jour via le programme d’installation de correctif logiciel pour Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f3058277-c597-4dac-86d1-41b6f7e62b36
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67d2fc976b08e438c6f19a7fecca03761bb099f6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124728"
---
# <a name="use-the-hotfix-installer-to-install-updates-for-system-center-configuration-manager"></a>Utiliser le programme d’installation de correctif logiciel pour installer les mises à jour de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Certaines mises à jour de System Center Configuration Manager indisponibles sur le service cloud Microsoft ne peuvent être obtenues que hors bande. C’est le cas, par exemple, d’un correctif logiciel en édition limitée destiné à résoudre un problème spécifique.   
Si vous devez installer une mise à jour (ou un correctif logiciel) reçu de Microsoft et que le fichier de cette mise à jour porte un nom se terminant par l’extension **.exe** (pas **update.exe**), vous utilisez le programme d’installation du correctif logiciel inclus dans le téléchargement de celui-ci pour installer la mise à jour directement sur le serveur de site Configuration Manager.  

 Si l’extension du nom de fichier du correctif est **.update.exe**, consultez [Importer des correctifs pour System Center Configuration Manager avec l’outil Inscription de la mise à jour](../../../core/servers/manage/use-the-update-registration-tool-to-import-hotfixes.md).  

> [!NOTE]  
>  Cette rubrique fournit des indications générales sur la façon d’installer les correctifs pour la mise à jour de System Center Configuration Manager. Pour plus d'informations sur une mise à jour spécifique, reportez-vous à l'article correspondant de la Base de connaissances du Support Microsoft.  

##  <a name="bkmk_Overview"></a> Vue d’ensemble des correctifs logiciels pour Configuration Manager  
 Les correctifs logiciels pour Configuration Manager sont similaires à ceux publiés pour d’autres produits Microsoft, tels que SQL Server. Ils se composent d’un correctif individuel ou d’un groupe de correctifs (correctif cumulatif), et sont décrits dans la Base de connaissances Microsoft.  

 Les mises à jour individuelles se composent d’une seule mise à jour ciblée qui s’applique à une version spécifique de Configuration Manager.  
Les groupes de mises à jour comprennent plusieurs mises à jour destinées à une version spécifique de Configuration Manager.  
Vous ne pouvez pas installer séparément les mises à jour individuelles incluses dans un groupe de mises à jour.  

 Si vous envisagez de créer des déploiements pour installer des mises à jour sur des ordinateurs supplémentaires, vous devez installer le groupe de mises à jour sur un serveur de site d’administration centrale ou un serveur de site principal.  

 Quand vous exécutez le groupe de mises à jour, voici ce qui se produit :  

-   Le groupe de mises à jour extrait les fichiers de mise à jour de chaque composant concerné.  

-   Il démarre un Assistant qui vous guide tout au long du processus de configuration des mises à jour et des options de déploiement associées.  

-   À la fin de l’Assistant, les mises à jour du groupe qui s’appliquent au serveur de site sont installées sur ce dernier.  

L’Assistant crée également des déploiements que vous pouvez utiliser pour installer les mises à jour sur des ordinateurs supplémentaires. Vous déployez les mises à jour sur des ordinateurs supplémentaires en appliquant une méthode de déploiement prise en charge, comme un package de déploiement de logiciel ou Microsoft System Center Updates Publisher 2011.  

 Quand il s’exécute, l’Assistant crée sur le serveur de site un fichier **.cab** à utiliser avec Updates Publisher 2011. Si vous le souhaitez, vous pouvez configurer l'Assistant pour créer également un ou plusieurs packages de déploiement de logiciels. Vous pouvez utiliser ces déploiements pour installer des mises à jour de composants, tels que les clients ou la console Configuration Manager. Vous pouvez aussi installer les mises à jour manuellement sur des ordinateurs qui n’exécutent pas le client Configuration Manager.  

 Dans Configuration Manager, une mise à jour peut porter sur les trois groupes suivants :  

-   Rôles de serveur Configuration Manager, comprenant :  

    -   Site d'administration centrale  

    -   Site principal  

    -   Site secondaire  

    -   Fournisseur SMS distant  

-   Console Configuration Manager  

-   Client de Configuration Manager  

> [!NOTE]  
>  Les **mises à jour des rôles système de site** (dont celles destinées à la base de données du site et aux points de distribution cloud) sont installées dans le cadre de la mise à jour des services et serveurs de site par le Gestionnaire de composants de site.  
>   
>  En revanche, les mises à jour des points de distribution d’extraction sont effectuées par le Gestionnaire de distribution plutôt que par le Gestionnaire de composants de site.  

 Chaque groupe de mises à jour applicable à Configuration Manager est un fichier .exe auto-extractible (SFX) qui contient les fichiers nécessaires à l’installation de la mise à jour sur les composants concernés de Configuration Manager. En règle générale, le fichier SFX peut contenir les fichiers suivants :  

|Fichier|Détails|  
|----------|-------------|  
|&lt;Version_produit\>-QFE-KB&lt;ID_article_Base_connaissances\>-&lt;plateforme\>-&lt;langue\>.exe|Correspond au fichier de mise à jour. La ligne de commande pour ce fichier est gérée par Updatesetup.exe.<br /><br /> Par exemple :<br />CM1511RTM-QFE-KB123456-X64-ENU.exe|  
|Updatesetup.exe|Ce wrapper .msi gère l'installation du groupe de mises à jour.<br /><br /> Lorsque vous exécutez la mise à jour, Updatesetup.exe détecte la langue d'affichage de l'ordinateur sur lequel elle s'exécute. Par défaut, l'interface utilisateur de la mise à jour est l'anglais. Toutefois, si la langue d'affichage est prise en charge, l'interface utilisateur s'affiche dans la langue locale de l'ordinateur.|  
|Licence_&lt;langue\>.rtf|Le cas échéant, chaque mise à jour contient un ou plusieurs fichiers de licence en fonction des langues prises en charge.|  
|&lt;Produit&type_MàJ>-&lt;version_produit\>-&lt;ID_article_Base_connaissances\>-&lt;plateforme\>.msp|Quand la mise à jour concerne la console ou les clients Configuration Manager, le groupe de mises à jour inclut des fichiers correctifs Windows Installer (.msp) distincts.<br /><br /> Par exemple :<br /><br /> **Mises à jour de la console Configuration Manager :** ConfigMgr1511-AdminUI-KB1234567-i386.msp<br /><br /> **Mise à jour du client :** ConfigMgr1511-client-KB1234567-i386.msp<br />ConfigMgr1511-client-KB1234567-x64.msp|  

 Par défaut, le groupe de mises à jour enregistre ses actions dans un fichier .log sur le serveur de site. Le fichier journal possède le même nom que le groupe de mises à jour et est écrit dans le dossier **%SystemRoot%/Temp** .  

 Lors de son exécution, le groupe de mises à jour extrait un fichier ayant le même nom que le sien dans un dossier temporaire sur l'ordinateur, puis il exécute Updatesetup.exe. Updatesetup.exe démarre l’Assistant Mise à jour logicielle pour Configuration Manager&lt;version du produit\> &lt;Numéro d’article de la Base de connaissances\>.  

 En fonction de l’étendue de la mise à jour, l’Assistant crée une série de dossiers situés sous le dossier d’installation de System Center Configuration Manager sur le serveur de site. La structure de dossiers se présente de la façon suivante :   
 **\\\\&lt;Nom_serveur\>\SMS_&lt;Code_site\>\Hotfix\\&lt;Numéro_article_Base_connaissances\>\\&lt;Type_MàJ\>\\&lt;plateforme\>**.  

 Le tableau suivant fournit des détails sur les dossiers figurant dans la structure de dossiers :  

|Nom de dossier|Informations complémentaires|  
|-----------------|----------------------|  
|&lt;Nom_serveur\>|Nom du serveur de site sur lequel vous exécutez le groupe de mises à jour.|  
|SMS_&lt;code_site\>|Nom de partage du dossier d’installation de Configuration Manager.|  
|&lt;Numéro_article_Base_connaissances\>|Numéro d'identification de l'article de la Base de connaissances pour ce groupe de mises à jour.|  
|&lt;Type_MàJ\>|Type de mise à jour de Configuration Manager. L'Assistant crée un dossier distinct pour chaque type de mise à jour contenu dans le groupe de mises à jour. Les noms de dossier représentent les types de mise à jour. Il s'agit des dossiers suivants :<br /><br /> **Serveur** : comprend les mises à jour des serveurs de site, des serveurs de base de données de site et des ordinateurs qui exécutent le fournisseur SMS.<br /><br /> **Client** : Inclut les mises à jour du client Gestionnaire de configuration.<br /><br /> **AdminConsole** : Inclut les mises à jour de la console Configuration Manager<br /><br /> Outre les types de mise à jour précédents, l'Assistant crée un dossier nommé **SCUP**. Ce dossier ne représente pas un type de mise à jour. Par contre, il contient le fichier .cab pour Updates Publisher.|  
|&lt;Plateforme\>|Dossier propre à la plate-forme. Il contient les fichiers de mise à jour propres à un type de processeur.  Ces dossiers sont les suivants :<br /><br />- x64<br /><br /> - I386|  

##  <a name="bkmk_Install"></a> Comment installer des mises à jour  
 Pour installer des mises à jour, vous devez d’abord installer le groupe de mises à jour sur un serveur de site. Lorsque vous installez un groupe de mises à jour, l’Assistant Installation démarre pour effectuer cette mise à jour. Cet Assistant assure les tâches suivantes :  

-   Extraction des fichiers de mise à jour  

-   Aide à la configuration des déploiements  

-   Installation des mises à jour applicables sur les composants serveur de l’ordinateur local  

Après avoir installé le groupe de mises à jour sur un serveur de site, vous pouvez ensuite mettre à jour des composants supplémentaires pour Configuration Manager. Le tableau suivant décrit les actions de mise à jour pour ces divers composants :  

|Composant|Instructions|  
|---------------|------------------|  
|Serveur de site|Déployez les mises à jour sur un serveur de site distant si vous choisissez de ne pas installer le groupe de mises à jour directement sur ce serveur de site distant.|  
|Base de données de site|Pour les serveurs de site distants, déployez les mises à jour serveur qui incluent une mise à jour de la base de données de site si vous n'installez pas le groupe de mises à jour directement sur ce serveur de site distant.|  
|Console Configuration Manager|Après l'installation initiale de la console Configuration Manager, vous pouvez installer les mises à jour de la console Configuration Manager sur chaque ordinateur qui exécute cette dernière. Vous ne pouvez pas modifier les fichiers d'installation de la console Configuration Manager pour appliquer les mises à jour pendant l’installation initiale de la console.|  
|Fournisseur SMS distant|Installez les mises à jour pour chaque instance du fournisseur SMS qui s'exécute sur un autre ordinateur que le serveur de site sur lequel vous avez installé le groupe de mises à jour.|  
|Clients Configuration Manager|Après l'installation initiale du client Configuration Manager, vous pouvez installer les mises à jour du client Configuration Manager sur chaque ordinateur qui exécute ce dernier.|  

> [!NOTE]  
>  Vous ne pouvez déployer les mises à jour que sur les ordinateurs qui exécutent le client Configuration Manager.  

 Si vous réinstallez un client, la console Configuration Manager ou le fournisseur SMS, vous devez également réinstaller les mises à jour de ces composants.  

 Pour installer les mises à jour sur chacun des composants de Configuration Manager, utilisez les informations figurant dans les sections suivantes.  

###  <a name="bkmk_servers"></a> Mettre à jour les serveurs  
 Les mises à jour destinées aux serveurs peuvent englober des mises à jour pour les **sites**, la **site database**et les ordinateurs qui exécutent une instance du **fournisseur SMS**.  

####  <a name="bkmk_site"></a> Mettre à jour un site  
 Pour mettre à jour un site Configuration Manager, vous pouvez installer le groupe de mises à jour directement sur le serveur de site ou déployer les mises à jour sur un serveur de site après avoir installé le groupe de mises à jour sur un site différent.  

 Lorsque vous installez une mise à jour sur un serveur de site, le processus d'installation de mise à jour gère les autres actions nécessaires à l'application de la mise à jour, telles que la mise à jour des rôles de système de site. La base de données de site constitue une exception. La section suivante contient des informations sur la façon de mettre à jour la base de données de site.  

####  <a name="bkmk_database"></a> Mettre à jour une base de données de site  
 Pour mettre à jour la base de données de site, le processus d'installation exécute un fichier nommé **update.sql** dans la base de données de site. Vous pouvez configurer le processus de mise à jour pour mettre à jour automatiquement la base de données de site. Vous pouvez également choisir de mettre à jour manuellement la base de données de site à un moment ultérieur.  

 **Mise à jour automatique de la base de données de site**  

 Lorsque vous installez le groupe de mises à jour sur un serveur de site, vous pouvez choisir de mettre à jour la base de données de site automatiquement lors de l'installation de la mise à niveau du serveur. Cette décision concerne uniquement le serveur de site sur lequel vous installez le groupe de mises à jour et ne s'applique pas aux déploiements créés pour installer les mises à jour sur des serveurs de site distants.  

> [!NOTE]  
>  Lorsque vous choisissez de mettre à jour automatiquement la base de données de site, le processus met à jour une base de données, que celle-ci réside sur le serveur de site ou sur un ordinateur distant.  

> [!IMPORTANT]  
>  Avant de mettre à jour la base de données de site, créez-en une sauvegarde. Vous ne pouvez pas désinstaller une mise à jour appliquée à la base de données de site. Pour plus d’informations sur la création d’une sauvegarde pour Configuration Manager, voir [Sauvegarde et récupération pour System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

 **Mise à jour manuelle de la base de données de site**  

 Si vous choisissez de ne pas mettre à jour automatiquement la base de données de site lors de l'installation du groupe de mises à jour sur le serveur de site, la mise à jour du serveur ne modifie pas la base de données du serveur de site sur lequel le groupe de mises à jour s'exécute. En revanche, des déploiements utilisant le package créé à des fins de déploiement de logiciels ou qui installe, mettent systématiquement à jour la base de données du site.  

> [!WARNING]  
>  Lorsque la mise à jour comporte des mises à jour pour le serveur de site et la base de données de site, la mise à jour n'est pas opérationnelle tant qu'elle n'est pas terminée à la fois sur le serveur de site et sur la base de données de site. Tant que la mise à jour n’est pas appliquée à la base de données du site, celui-ci est dans un état non pris en charge.  

 **Pour mettre à jour manuellement une base de données de site :**  

1.  Sur le serveur de site, arrêtez le service SMS_SITE_COMPONENT_MANAGER, puis arrêtez le service SMS_EXECUTIVE.  

2.  Fermez la console Configuration Manager.  

3.  Exécutez le script de mise à jour nommé **update.sql** sur la base de données de ce site. Pour plus d'informations sur la façon d'exécuter un script de mise à jour de base de données SQL Server, consultez la documentation de la version de SQL Server utilisée pour votre serveur de bases de données de site.  

4.  Redémarrez les services que vous avez arrêtés lors des étapes précédentes.  

5.  Pendant son installation, le groupe de mises à niveau extrait **update.sql** à l'emplacement suivant sur le serveur de site :  **\\\\&lt;Nom du serveur\>\SMS_&lt;Code de site\>\Correctif logiciel\\&lt;Numéro d’article de la Base de connaissances\>\update.sql**  

####  <a name="bkmk_provider"></a> Mettre à jour un ordinateur exécutant le fournisseur SMS  
 Après avoir installé un groupe de mises à jour incluant des mises à jour pour le fournisseur SMS, vous devez déployer la mise à jour sur chaque ordinateur qui exécute le fournisseur SMS. La seule exception est l'instance du fournisseur SMS déjà installée sur le serveur de site sur lequel vous installez le groupe de mises à jour. L'instance locale du fournisseur SMS sur le serveur de site est mise à jour lorsque vous installez le groupe de mises à jour.  

 Si vous supprimez puis réinstallez le fournisseur SMS sur un ordinateur, vous devez alors réinstaller la mise à jour pour le fournisseur SMS sur cet ordinateur.  

###  <a name="BKMK_clients"></a> Mettre à jour des clients  
 Lorsque vous installez une mise à jour incluant des mises à jour pour le clients Configuration Manager, vous avez le choix entre mettre à niveau automatiquement les clients avec l’installation de la mise à jour ou les mettre à niveau manuellement plus tard. Pour plus d’informations sur la mise à niveau automatique des clients, consultez [Comment mettre à niveau les clients pour les ordinateurs Windows dans System Center Configuration Manager](https://technet.microsoft.com/library/mt627885.aspx).  

 Vous pouvez déployer des mises à jour avec Updates Publisher ou avec un package de déploiement de logiciel, ou vous pouvez choisir d’installer manuellement la mise à jour sur chaque client. Pour plus d’informations sur l’utilisation des déploiements dans le cadre de l’installation des mises à jour, consultez la section [Déployer des mises à jour pour Configuration Manager](#BKMK_Deploy) dans cette rubrique.  

> [!IMPORTANT]  
>  Lorsque vous installez des mises à jour pour des clients, et que le groupe de mises à jour comprend des mises à jour pour des serveurs, assurez-vous d'installer également les mises à jour serveur sur le site principal auquel les clients sont attribués.  

Pour installer manuellement la mise à jour du client, sur chaque client Configuration Manager, vous devez exécuter le fichier **Msiexec.exe** et référencer le fichier .msp de mise à jour client spécifique à la plateforme.  

 Par exemple, vous pouvez utiliser la ligne de commande suivante pour une mise à jour client. Cette ligne de commande exécute MSIEXEC sur l’ordinateur client et fait référence au fichier .msp que le groupe de mises à jour a extrait sur le serveur de site : **msiexec.exe /p \\\\&lt;Nom_serveur\>\SMS_&lt;Code_site\>\Hotfix\\&lt;Numéro_article_Base_de_connaissances\>\Client\\&lt;Plateforme\>\\&lt;msp\> /L\*v &lt;fichier_journal\>REINSTALLMODE=mous REINSTALL=ALL**  

###  <a name="BKMK_console"></a> Mettre à jour des consoles Configuration Manager  
 Pour mettre à jour une console Configuration Manager, après l'installation initiale de la console, vous devez installer la mise à jour sur l'ordinateur qui exécute cette dernière.  

> [!IMPORTANT]  
>  Quand vous installez des mises à jour pour la console Configuration Manager et que le groupe de mises à jour comprend des mises à jour pour les serveurs, veillez à également installer les mises à jour de serveur sur le site que vous utilisez avec la console Configuration Manager.  

Si l’ordinateur que vous mettez à jour exécute le client Configuration Manager :  

-   Vous pouvez utiliser un déploiement pour installer la mise à jour. Pour plus d’informations sur l’utilisation des déploiements dans le cadre de l’installation des mises à jour, consultez la section [Déployer des mises à jour pour Configuration Manager](#BKMK_Deploy) dans cette rubrique.  

-   Si vous êtes connecté directement à l’ordinateur client, vous pouvez exécuter l’installation de manière interactive.  

-   Vous pouvez installer manuellement la mise à jour sur chaque ordinateur. Pour installer manuellement la mise à jour de la console Configuration Manager, sur chaque ordinateur qui exécute la console Configuration Manager, vous pouvez exécuter le fichier Msiexec.exe et faire référence au fichier .msp de mise à jour de la console Configuration Manager.  

Par exemple, vous pouvez utiliser la ligne de commande suivante pour mettre à jour une console Configuration Manager. Cette ligne de commande exécute MSIEXEC sur l’ordinateur et fait référence au fichier .msp que le groupe de mises à jour a extrait sur le serveur de site : **msiexec.exe /p \\\\&lt;Nom_serveur\>\SMS_&lt;Code_site\>\Hotfix\\&lt;Numéro_article_Base_connaissances\>\AdminConsole\\&lt;Plateforme\>\\&lt;msp\> /L\*v &lt;fichier_journal\>REINSTALLMODE=mous REINSTALL=ALL**  

##  <a name="BKMK_Deploy"></a> Déployer des mises à jour pour Configuration Manager  
 Après avoir installé le groupe de mises à jour sur un serveur de site, vous pouvez utiliser l’une des trois méthodes suivantes pour déployer des mises à jour sur des ordinateurs supplémentaires.  

###  <a name="BKMK_DeploySCUP"></a> Utiliser Updates Publisher 2011 pour installer des mises à jour  
 Lorsque vous installez le groupe de mises à jour sur un serveur de site, l’Assistant Installation crée un fichier catalogue pour l’éditeur de mise à jour, que vous pouvez utiliser pour déployer les mises à jour sur les ordinateurs concernés. L’Assistant crée toujours ce catalogue, même quand vous sélectionnez l’option **Use package and program to deploy this update**.  

 Le catalogue pour l’éditeur de mise à jour se nomme **SCUPCatalog.cab**, il est disponible à l’emplacement suivant sur l’ordinateur où s’exécute l’offre groupée de mises à jour : **\\\\&lt;Nom du serveur\>\SMS_&lt;Code du site\>\Correctif_logiciel\\&lt;Numéro d’article de la Base de connaissances\>\SCUP\SCUPCatalog.cab**  

> [!IMPORTANT]  
>  Dans la mesure où le fichier SCUPCatalog.cab est créé à l'aide de chemins spécifiques du serveur de site sur lequel le groupe de mises à jour est installé, il ne peut pas être utilisé sur d'autres serveurs de site.  

 Une fois l’exécution de l’Assistant terminée, vous pouvez importer le catalogue dans l’éditeur de mise à jour, puis utiliser les mises à jour logicielles de Configuration Manager pour déployer les mises à jour. Pour plus d’informations sur l’éditeur de mise à jour, voir [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkID=83449) dans la bibliothèque TechNet pour System Center 2012.  

 Utilisez la procédure suivante pour importer le fichier SCUPCatalog.cab vers Updates Publisher et publier les mises à jour.  

##### <a name="to-import-the-updates-to-updates-publisher-2011"></a>Pour importer les mises à jour vers Updates Publisher 2011  

1.  Démarrez la console de l’éditeur de mise à jour et cliquez sur **Importer**.  

2.  Sur la page **Type d'importation** de l'Assistant Importation de catalogue des mises à jour logicielles, sélectionnez **Specify the path to the catalog to import**(Spécifier le chemin vers ce catalogue à importer), puis spécifiez le fichier SCUPCatalog.cab.  

3.  Cliquez sur **Suivant**, puis cliquez sur **Suivant** de nouveau.  

4.  Dans la boîte de dialogue **Avertissement de sécurité - Validation du catalogue** , cliquez sur **Accepter**. Fermez l'Assistant une fois la procédure terminée.  

5.  Dans la console de l’éditeur de mise à jour, sélectionnez la mise à jour à déployer, puis cliquez sur **Publier**.  

6.  Sur la page **Options de publication** de l'Assistant Publication des mises à jour logicielles, sélectionnez le **contenu complet**, puis cliquez sur **Suivant**.  

7.  Terminez l'Assistant pour publier les mises à jour.  

###  <a name="BKMK_DeploySWDist"></a> Utiliser le déploiement logiciel pour installer des mises à jour  
 Lorsque vous installez le groupe de mises à jour sur le serveur de site d’un site principal ou d’un site d’administration centrale, vous pouvez configurer l’Assistant Installation pour créer des packages de mise à jour pour le déploiement de logiciels. Vous pouvez alors déployer chaque package sur un regroupement d'ordinateurs que vous voulez mettre à jour.  

 Pour créer un package de déploiement de logiciels, sur la page de **configuration de déploiement de mises à jour logicielles** de l'Assistant, activez la case à cocher de chaque type de package de mises à jour à mettre à jour. Les types disponibles peuvent inclure des serveurs, des console Configuration Manager et des clients. Un package distinct est créé pour chaque type de mise à jour que vous sélectionnez.  

> [!NOTE]  
>  Le package pour serveurs contient des mises à jour pour les composants suivants :  
>   
>  -   Serveur de site  
>  -   Fournisseur SMS  
>  -   Base de données de site  

 Ensuite, sur la page de **configuration de la méthode de déploiement de mises à jour logicielles** de l'Assistant, sélectionnez l'option **I will use software distribution**(Je vais utiliser la distribution de logiciels). Cette sélection indique à l'Assistant de créer les packages de déploiement de logiciels.  

 Une fois l'Assistant terminé, les packages créés apparaissent dans la console Configuration Manager, dans le nœud **Packages** de l'espace de travail **Bibliothèque de logiciels**. Vous pouvez ensuite utiliser votre processus standard pour déployer des packages logiciels sur des clients Gestionnaire de configuration. Lorsqu'un package s'exécute sur un client, il installe les mises à jour pour les composants applicables de Configuration Manager sur l'ordinateur client.  

 Pour plus d’informations sur le déploiement des packages vers des clients Configuration Manager, voir [System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

###  <a name="BKMK_DeployCollections"></a> Créer des regroupements pour déployer des mises à jour sur Configuration Manager  
 Vous pouvez déployer des mises à jour spécifiques vers les clients applicables. Les informations suivantes peuvent vous aider à créer des regroupements d’appareils pour les différents composants de Configuration Manager.  

|Composant de Configuration Manager|Instructions|  
|----------------------------------------|------------------|  
|Serveur de site d'administration centrale|Créez une requête d'adhésion directe et ajoutez l'ordinateur serveur du site d'administration centrale.|  
|Tous les serveurs de site principal|Créez une requête d'adhésion directe et ajoutez chaque ordinateur serveur de site principal.|  
|Tous les serveurs de site secondaire|Créez une requête d'adhésion directe et ajoutez chaque ordinateur serveur de site secondaire.|  
|Tous les clients x86|Créez un regroupement avec les critères de requête suivants :<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X86-based PC"**|  
|Tous les clients x64|Créez un regroupement avec les critères de requête suivants :<br /><br /> **Select \* from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceID = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemType = "X64-based PC"**|  
|Tous les ordinateurs qui exécutent la console Configuration Manager|Créez une requête d'adhésion directe et ajoutez chaque ordinateur.|  
|Ordinateurs distants exécutant une instance du fournisseur SMS|Créez une requête d'adhésion directe et ajoutez chaque ordinateur.|  

> [!NOTE]  
>  Pour mettre à jour une base de données de site, déployez la mise à jour vers le serveur de site de ce site.  

 Pour plus d’informations sur la création de regroupements, consultez [Comment créer des regroupements dans Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  
