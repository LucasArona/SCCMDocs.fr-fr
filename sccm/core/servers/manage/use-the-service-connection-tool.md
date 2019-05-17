---
title: Outil de connexion de service
titleSuffix: Configuration Manager
description: En savoir plus sur cet outil qui vous permet d’établir une connexion au service cloud Configuration Manager pour charger manuellement les informations d’utilisation.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e4964c5-43cb-4372-9a89-b62ae6a4775c
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 002ed233a679cdee928160490c8e1ee4425c7382
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496259"
---
# <a name="use-the-service-connection-tool-for-system-center-configuration-manager"></a>Utiliser l’outil de connexion de service pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez l’**Outil de connexion de service** quand votre point de connexion de service est en mode hors connexion ou quand vos serveurs de système de site Configuration Manager ne sont pas connectés à Internet. Cet outil peut vous aider à tenir votre site à jour avec les dernières mises à jour pour Configuration Manager.  

Quand vous l’exécutez, il se connecte manuellement au service cloud Configuration Manager pour charger les informations d’utilisation relatives à votre hiérarchie et pour télécharger des mises à jour. Le chargement de données d’utilisation est nécessaire pour que le service cloud vous propose les mises à jour adaptées à votre déploiement.  

## <a name="prerequisites-for-using-the-service-connection-tool"></a>Prérequis pour utiliser l’outil de connexion de service
Voici la liste des prérequis et des problèmes connus.

**Conditions préalables :**

-   Vous avez installé un point de connexion de service et sélectionné l’option **Hors connexion, connexion à la demande**.  

-   L’outil doit être exécuté à partir d’une invite de commandes.  

-   Chaque ordinateur sur lequel l’outil s’exécute (l’ordinateur du point de connexion de service et l’ordinateur connecté à Internet) doit avoir un système x64 bits ainsi que les composants suivants :  

    -   Fichiers x86 et x64 **Redistributable Visual C++** .   Par défaut, Configuration Manager installe la version x64 sur l’ordinateur qui héberge le point de connexion de service.  

         Pour télécharger une copie des fichiers Visual C++, consultez [Packages Redistributable Visual C++ pour Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=40784) dans le Centre de téléchargement Microsoft.  

    -   .NET Framework 4.5.2 ou version ultérieure.  

-   Le compte que vous utilisez pour exécuter l’outil doit avoir :
    -   Des autorisations d’**administrateur local** sur l’ordinateur hébergeant le point de connexion de service (sur lequel l’outil s’exécute)
    -   Des autorisations de**Lecture** sur la base de données de site  



-   Pour transférer des fichiers entre l’ordinateur du point de connexion de service et celui ayant accès à Internet, vous devez disposer d’un lecteur USB avec un espace libre suffisant pour stocker les fichiers et mises à jour, ou employer une autre méthode. (Ce scénario part du principe que votre site et les ordinateurs gérés ne disposent pas d’une connexion directe à Internet.)  



## <a name="use-the-service-connection-tool"></a>Utiliser l’outil de connexion de service  

 L’outil de connexion de service (**serviceconnectiontool.exe**) se trouve sur le support d’installation de Configuration Manager dans le dossier **%chemin%\smssetup\tools\ServiceConnectionTool**. Utilisez toujours l’outil de connexion de service qui correspond à votre version de Configuration Manager.


 Dans cette procédure, les exemples de ligne de commande utilisent les noms de fichiers et les emplacements de dossiers suivants (vous pouvez très bien utiliser d’autres chemins et noms de fichiers qui correspondent à votre environnement et à vos préférences) :  

-   Chemin à une clé USB où sont stockées les données pour le transfert entre les serveurs :  **D:\USB\\**  

-   Nom du fichier .cab contenant les données exportées à partir de votre site : **UsageData.cab**  

-   Nom du dossier vide dans lequel les mises à jour téléchargées pour Configuration Manager sont stockées à des fins de transfert entre les serveurs : **UpdatePacks**  

Sur l’ordinateur qui héberge le point de connexion de service :  

-   Ouvrez une invite de commandes avec des privilèges d’administration, puis changez de répertoire pour accéder à l’emplacement du fichier **serviceconnectiontool.exe**.  

     Par défaut, cet outil se trouve sur le support d’installation de Configuration Manager dans le dossier **%chemin%\smssetup\tools\ServiceConnectionTool**. Tous les fichiers dans ce dossier doivent figurer dans le même dossier pour que l’outil de connexion de service fonctionne.  

Lorsque vous exécutez la commande suivante, l’outil prépare un fichier .cab contenant des informations sur l’utilisation, et le copie vers un emplacement que vous spécifiez. Les données du fichier .cab sont basées sur le niveau des données de diagnostic et d’utilisation que votre site est configuré pour collecter. (voir [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)).  Exécutez la commande suivante pour créer le fichier .cab :  

-   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

Vous devez également copier le dossier ServiceConnectionTool avec tout son contenu sur le lecteur USB, ou le rendre disponible sur l’ordinateur que vous allez utiliser aux étapes 3 et 4.  

### <a name="overview"></a>Vue d'ensemble
#### <a name="there-are-three-primary-steps-to-using-the-service-connection-tool"></a>L’utilisation de l’outil de connexion de service nécessite trois étapes principales  

1.  **Préparer** :  Cette étape doit être exécutée sur l’ordinateur hébergeant le point de connexion de service. Quand vous exécutez l’outil, il place les données d’utilisation dans un fichier .cab et les stocke sur un lecteur USB (ou dans un autre emplacement de transfert spécifié).  

2.  **Connexion** : Lors de cette étape, vous exécutez l’outil sur un ordinateur distant qui se connecte à Internet pour charger les données d’utilisation puis télécharger les mises à jour.  

3.  **Importer** : Cette étape doit être exécutée sur l’ordinateur hébergeant le point de connexion de service. Quand vous exécutez l’outil, il importe les mises à jour que vous avez téléchargées et les ajoute à votre site pour que vous puissiez ensuite afficher et installer ces mises à jour à partir de la console Configuration Manager.  

À compter de la version 1606, quand vous vous connectez à Microsoft, vous pouvez charger plusieurs fichiers .cab à la fois (chacun à partir d’une hiérarchie différente) et spécifier un serveur proxy et un utilisateur du serveur proxy.   

#### <a name="to-upload-multiple-cab-files"></a>Pour charger plusieurs fichiers .cab
 -  Placez chaque fichier .cab que vous exportez à partir de hiérarchies distinctes dans le même dossier. Le nom de chaque fichier doit être unique, et vous pouvez les renommer manuellement si nécessaire.
 -  Ensuite, quand vous exécutez la commande pour charger des données vers Microsoft, vous spécifiez le dossier qui contient les fichiers .cab. (Avant la mise à jour 1606, vous pouviez uniquement charger des données à partir d’une seule hiérarchie à la fois, et l’outil vous obligeait à spécifier le nom du fichier .cab dans le dossier.)
 -  Plus tard, quand vous exécutez la tâche d’importation sur le point de connexion de service d’une hiérarchie, l’outil importe automatiquement uniquement les données de cette hiérarchie.  

#### <a name="to-specify-a-proxy-server"></a>Pour spécifier un serveur proxy
Vous pouvez utiliser les paramètres facultatifs suivants pour spécifier un serveur proxy (vous trouverez des informations supplémentaires sur l’utilisation de ces paramètres dans la section Paramètres de ligne de commande de cette rubrique) :
  - **-proxyserveruri [nom_domaine_complet_serveur_proxy]**  Utilisez ce paramètre pour spécifier le serveur proxy à utiliser pour cette connexion.
  -  **-proxyusername [nom_utilisateur]**  Utilisez ce paramètre quand vous devez spécifier un utilisateur du serveur proxy.

#### <a name="specify-the-type-of-updates-to-download"></a>Spécifier le type de mises à jour à télécharger
À compter de la version 1706, le comportement par défaut du téléchargement des outils a changé, et l’outil prend en charge des options pour contrôler quels fichiers vous téléchargez.
-   Par défaut, l’outil télécharge seulement la dernière mise à jour disponible qui s’applique à la version de votre site. Il ne télécharge pas les correctifs.

Pour changer ce comportement, utilisez un des paramètres suivants pour spécifier quels fichiers sont téléchargés. 

> [!NOTE]
> La version de votre site est déterminée à partir des données du fichier .cab qui est chargé quand l’outil s’exécute.
>
> Vous pouvez vérifier la version en recherchant le fichier *SiteVersion*.txt dans le fichier .cab.

-   **-downloadall** : cette option télécharge tout, notamment les mises à jour et les correctifs, quelle que soit la version de votre site.
-   **-downloadhotfix** : cette option télécharge tous les correctifs, quelle que soit la version de votre site.
-   **-downloadsiteversion** : cette option télécharge les mises à jour et les correctifs dont la version est supérieure à celle de votre site.

Exemple de ligne de commande utilisant *- downloadsiteversion* :
- **serviceconnectiontool.exe -connect  *-downloadsiteversion* -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**




### <a name="to-use-the-service-connection-tool"></a>Pour utiliser l’outil de connexion de service  

1. Sur l’ordinateur qui héberge le point de connexion de service :  

   -   Ouvrez une invite de commandes avec des privilèges d’administration, puis changez de répertoire pour accéder à l’emplacement du fichier **serviceconnectiontool.exe**.   

2. Exécutez la commande suivante pour que l’outil prépare un fichier .cab contenant des informations sur l’utilisation et le copie vers un emplacement que vous spécifiez :  

   -   **serviceconnectiontool.exe -prepare -usagedatadest D:\USB\UsageData.cab**  

   Si vous allez charger des fichiers .cab à partir de plusieurs hiérarchies en même temps, chaque fichier .cab dans le dossier doit avoir un nom unique. Vous pouvez renommer manuellement les fichiers que vous ajoutez au dossier.

   Si vous souhaitez afficher les informations d’utilisation collectées pour le chargement sur le service cloud Configuration Manager, exécutez la commande suivante pour exporter les mêmes données dans un fichier .csv que vous pouvez ensuite afficher à l’aide d’une application comme Excel :  

   -   **serviceconnectiontool.exe -export -dest D:\USB\UsageData.csv**  

3. Une fois l’étape de préparation terminée, connectez le lecteur USB (ou transférez les données exportées au moyen d’une autre méthode) à un ordinateur ayant accès à Internet.  

4. Sur l’ordinateur connecté à Internet, ouvrez une invite de commandes avec des privilèges d’administration, puis changez de répertoire pour accéder à l’emplacement contenant une copie de l’outil  **serviceconnectiontool.exe** et les fichiers supplémentaires de ce dossier.  

5. Exécutez la commande suivante pour commencer le chargement des informations d’utilisation et le téléchargement des mises à jour pour Configuration Manager :  

   -   **serviceconnectiontool.exe -connect -usagedatasrc D:\USB -updatepackdest D:\USB\UpdatePacks**

   Pour obtenir plus d’exemples de cette ligne de commande, consultez la section [Options de ligne de commande](../../../core/servers/manage/use-the-service-connection-tool.md#bkmk_cmd) plus loin dans cette rubrique.

   > [!NOTE]  
   >  Quand vous exécutez la ligne de commande pour vous connecter au service cloud Configuration Manager, une erreur semblable à la suivante peut se produire :  
   >   
   >  -   Exception non gérée : System.UnauthorizedAccessException :  
   >   
   >      L’accès au chemin « C:\  
   >     Users\br\AppData\Local\Temp\extractmanifestcab\95F8A562.sql » est refusé.  
   >   
   > Vous pouvez ignorer cette erreur sans risque. Fermez la fenêtre d’erreur et continuez.  

6. Une fois le téléchargement des mises à jour pour Configuration Manager terminé, connectez le lecteur USB (ou transférez les données exportées au moyen d’une autre méthode) à l’ordinateur qui héberge le point de connexion de service.  

7. Sur l’ordinateur qui héberge le point de connexion de service, ouvrez une invite de commandes avec des privilèges d’administration, changez de répertoire pour accéder à l’emplacement contenant **serviceconnectiontool.exe**, puis exécutez la commande suivante :  

   -   **serviceconnectiontool.exe -import -updatepacksrc D:\USB\UpdatePacks**  

8. Une fois l’importation terminée, vous pouvez fermer l’invite de commandes. (Seules les mises à jour pour la hiérarchie applicable sont importées.)  

9. Ouvrez la console Configuration Manager, puis accédez à **Administration** > **Mises à jour et maintenance**. Les mises à jour qui ont été importées peuvent désormais être installées. (Avant la version 1702, les mises à jour et la maintenance s’effectuaient via le menu **Administration** > **Services cloud**.)

   Pour plus d’informations, consultez [Installer des mises à jour dans la console pour System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

## <a name="bkmk_cmd"></a> Fichiers journaux

**ServiceConnectionTool.log**

Chaque fois que vous exécutez l’outil de connexion de service, un fichier journal nommé **ServiceConnectionTool.log** est généré dans le même emplacement que l’outil.  Ce fichier journal fournira de simples détails sur l’exécution de l’outil en fonction des commandes utilisées.  Un fichier journal existant est remplacé chaque fois que vous exécutez l’outil.

**ConfigMgrSetup.log**

Lorsque vous utilisez l’outil pour vous connecter et télécharger les mises à jour, un fichier journal appelé **ConfigMgrSetup.log** est créé à la racine du lecteur système.  Ce fichier journal fournira des informations plus détaillées, notamment la liste des fichiers téléchargés, extraits, et si les vérifications de hachage ont réussi.

## <a name="bkmk_cmd"></a> Options de ligne de commande  
 Pour afficher de l’aide sur l’outil de point de connexion de service, ouvrez une invite de commandes dans le dossier contenant l’outil, puis exécutez la commande suivante :  **serviceconnectiontool.exe**.  


|Options de ligne de commande|Détails|  
|---------------------------|-------------|  
|**-prepare -usagedatadest [lecteur:][chemin][nom_fichier.cab]**|Cette commande stocke les données d’utilisation actuelles dans un fichier .cab.<br /><br /> Exécutez cette commande en tant qu’ **administrateur local** sur le serveur qui héberge le point de connexion de service.<br /><br /> Exemple :   **-prepare -usagedatadest D:\USB\Usagedata.cab**|    
|**-connect -usagedatasrc [lecteur:][chemin] -updatepackdest [lecteur:][chemin] -proxyserveruri [nom_domaine_complet_serveur_proxy] -proxyusername [nom_utilisateur]** <br /> <br /> Si vous utilisez une version de Configuration Manager antérieure à la version 1606, vous devez spécifier le nom du fichier .cab et vous ne pouvez pas utiliser les options d’un serveur proxy.  Les paramètres de commande pris en charge sont les suivants : <br /> **-connect -usagedatasrc [lecteur:][chemin][nom_fichier] -updatepackdest [lecteur:][chemin]** |Cette commande se connecte au service cloud Configuration Manager pour charger les fichiers .cab de données d’utilisation à partir de l’emplacement spécifié et pour télécharger le contenu de console et les packs de mise à jour disponibles. Les options pour les serveurs proxy sont facultatives.<br /><br /> Exécutez cette commande en tant qu’ **administrateur local** sur un ordinateur capable de se connecter à Internet.<br /><br /> Exemple de connexion sans serveur proxy : **-connect -usagedatasrc D:\USB\ -updatepackdest D:\USB\UpdatePacks** <br /><br /> Exemple de connexion quand vous utilisez un serveur proxy : **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks -proxyserveruri itgproxy.redmond.corp.microsoft.com -proxyusername Meg** <br /><br /> Si vous utilisez une version antérieure à la version 1606, vous devez spécifier un nom de fichier pour le fichier .cab et vous ne pouvez pas spécifier de serveur proxy. Utilisez l’exemple de ligne de commande suivant : **-connect -usagedatasrc D:\USB\Usagedata.cab -updatepackdest D:\USB\UpdatePacks**|      
|**-import -updatepacksrc [lecteur:][chemin]**|Cette commande importe les packages de mise à jour et le contenu de la console que vous avec précédemment téléchargés dans la console Configuration Manager.<br /><br /> Exécutez cette commande en tant qu’ **administrateur local** sur le serveur qui héberge le point de connexion de service.<br /><br /> Exemple :  **-import -updatepacksrc D:\USB\UpdatePacks**|  
|**-export -dest [lecteur:][chemin][nom_fichier.csv]**|Cette commande exporte les données d’utilisation dans un fichier .csv que vous pouvez ensuite afficher.<br /><br /> Exécutez cette commande en tant qu’ **administrateur local** sur le serveur qui héberge le point de connexion de service.<br /><br /> Exemple : **-export -dest D:\USB\usagedata.csv**|  
