---
title: Créer des applications
titleSuffix: Configuration Manager
description: Créez des applications avec des types de déploiement, des méthodes de détection et des spécifications pour installer les logiciels.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9b90dfcc0916f62905af777e45222ceebf8300f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341869"
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Créer des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application Configuration Manager propose un ou plusieurs types de déploiement. Ces types de déploiement incluent les fichiers d’installation et les informations nécessaires à l’installation du logiciel sur des appareils. Un type de déploiement comporte aussi des règles, telles que des méthodes de détection et des spécifications, qui précisent quand et comment le client installe le logiciel.  

 Créez des applications en employant les méthodes suivantes :  

-   Créer automatiquement les types d'application et de déploiement en lisant les fichiers d'installation de l'application.  

-   Créer manuellement l'application, puis ajouter des types de déploiement ultérieurement.  

-   Importer une application à partir d’un fichier.  

> [!NOTE]  
>  Pour obtenir des informations détaillées sur la création d’applications iOS, Windows Phone et Android, consultez [Créer des applications pour des appareils mobiles](../../mdm/deploy-use/create-applications.md).  



## <a name="start-the-create-application-wizard"></a>Démarrer l’Assistant Création d’une application  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application**.  



## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>Spécifier si vous souhaitez détecter automatiquement les informations de l'application ou définir manuellement les informations  

-   Détectez automatiquement les informations d’application pour créer une application de base avec un seul type de déploiement, par exemple, un fichier Windows Installer qui n’a pas de dépendances ou de spécifications. Après avoir créé une application à l'aide de cette procédure, vous pouvez la modifier pour ajouter ou changer les types de déploiement et ajouter des méthodes de détection, des dépendances ou des spécifications.  

-   Utilisez la procédure de définition manuelle des informations de l’application pour créer des applications plus complexes associant plusieurs types de déploiement, dépendances, méthodes de détection et spécifications.  

### <a name="automatically-detect-application-information"></a>Détecter automatiquement les informations sur l’application  

1.  Dans la page **Général,** de l’Assistant Création d’une application, sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d’installation**.  

2.  Dans la liste déroulante **Type** , choisissez le type de fichier d'installation d'application que vous souhaitez utiliser pour détecter les informations sur l'application. Pour plus d’informations sur les types d’installation disponibles, consultez [Types de déploiement pris en charge par Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) dans cette rubrique.  

3.  Dans la zone **Emplacement**, spécifiez le chemin UNC (au format *\\\\serveur\\partage\\\nom_fichier*) ou le lien du magasin du fichier d’installation d’application à utiliser pour détecter les informations sur l’application. Vous pouvez également cliquer sur **Parcourir** pour accéder au fichier d’installation.  

    > [!IMPORTANT]  
    >  Quand vous sélectionnez **Windows Installer (fichier \*.msi)** comme type d’application, tous les fichiers situés dans le dossier spécifié sont importés et envoyés aux points de distribution. Vérifiez que le dossier spécifié contient uniquement les fichiers nécessaires à l’installation de l’application. Configuration Manager est testé pour prendre en charge jusqu’à 20 000 fichiers d’application dans le package d’application. Si votre application contient plus de fichiers, pensez à créer plusieurs applications avec moins de fichiers.  

    >  Vous devez avoir accès au chemin UNC qui contient l’application et aux sous-dossiers où figure le contenu de l’application.  

4.  Dans la page **Importer des informations** de l’Assistant Création d’une application, consultez les informations qui ont été importées, puis choisissez **Suivant**. Si nécessaire, vous pouvez choisir **Précédent** pour revenir en arrière et corriger les erreurs éventuelles.  

5.  Dans la page **Informations générales** de l’Assistant Création d’une application, spécifiez les informations suivantes :  

    > [!NOTE]  
    >  Si Configuration Manager détecte automatiquement ces informations dans les fichiers d’installation de l’application, elles y figurent déjà. En outre, les options affichées peuvent être différentes en fonction du type d'application que vous créez.  

    -   Informations générales sur l’application, comme le nom de l’application, des commentaires et la version. Pour vous aider à trouver l’application dans la console Configuration Manager, spécifiez éventuellement une référence.  

    -   **Programme d'installation**: spécifiez le programme d'installation et les éventuelles propriétés obligatoires, nécessaires pour installer le type de déploiement de l'application.  

        > [!TIP]  
        >  Si le programme d’installation n’est pas indiqué, choisissez **Parcourir** et accédez à l’emplacement du programme d’installation.  

    -   **Comportement à l’installation** : indiquez si le type de déploiement de l’application doit être installé pour l’utilisateur actuellement connecté uniquement ou pour tous les utilisateurs. Il existe une troisième option qui consiste à installer pour tous les utilisateurs si le déploiement s’effectue sur un seul appareil ou seulement pour un utilisateur déterminé si le déploiement concerne un seul utilisateur.  

    -   **Utiliser une connexion VPN automatique (si elle est configurée)**: Si un profil VPN a été déployé sur l'appareil sur lequel l'application est exécutée, lancez la connexion VPN au démarrage de l'application (Windows 8.1 et Windows Phone 8.1 uniquement).  

         Sur les appareils Windows Phone 8.1, les connexions VPN automatiques ne sont pas prises en charge si plusieurs profils VPN ont été déployés sur l’appareil.  

         Pour plus d’informations, consultez [Profils VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Choisissez **Suivant**, examinez les informations sur l’application figurant dans la page **Résumé**, puis suivez toutes les étapes de l’Assistant Création d’une application.  

La nouvelle application s’affiche dans le nœud **Applications** de la console Configuration Manager, ce qui marque la fin de la création d’une application. Si vous voulez ajouter d’autres types de déploiement à l’application, consultez [Créer des types de déploiement pour l’application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) dans cette rubrique.  

### <a name="manually-specify-application-information"></a>Définir manuellement les informations de l’application  

1.  Dans la page **Général** de l’Assistant Création d’une application, sélectionnez **Spécifier manuellement les informations de l’application**, puis choisissez **Suivant**.  

2.  Spécifiez des informations générales sur l’application, comme le nom de l’application, des commentaires et la version. Pour vous aider à trouver l’application dans la console Configuration Manager, spécifiez éventuellement une référence.  

3.  Dans la page **Catalogue d’applications** de l’Assistant Création d’une application, spécifiez les informations suivantes :  

    -   **Langue sélectionnée** : dans la liste déroulante, sélectionnez la version linguistique de l’application que vous souhaitez installer. Choisissez **Ajouter/Supprimer** pour configurer d’autres langues pour cette application.  

    -   **Nom de l'application localisée**: indiquez le nom de l'application, dans la langue sélectionnée dans la liste déroulante **Langue sélectionnée** .  

        > [!IMPORTANT]  
        >  Vous devez spécifier un nom d’application localisée pour chaque version de langue que vous configurez.  

    -   **Catégories d’utilisateurs** : choisissez **Modifier** pour spécifier les catégories de l’application dans la langue que vous avez sélectionnée dans la liste déroulante **Langue sélectionnée**. Les utilisateurs du Centre logiciel peuvent utiliser les catégories sélectionnées pour filtrer et trier les applications disponibles.  

    -   **Documentation utilisateur** : choisissez **Parcourir** pour spécifier l’emplacement d’un fichier que les utilisateurs du Centre logiciel peuvent lire pour obtenir des informations supplémentaires sur cette application. Cet emplacement est une URL ou un chemin réseau et un nom de fichier.

    -   **Texte de lien** : spécifiez le texte qui s’affiche à la place de l’URL de l’application.  

    -   **URL de la déclaration de confidentialité**: spécifiez une URL qui accède à la déclaration de confidentialité de l'application.  

    -   **Description localisée**: entrez une description de l'application, dans la langue sélectionnée dans la liste déroulante **Langue sélectionnée** .  

    -   **Mots-clés**: entrez une liste de mots-clés, dans la langue sélectionnée dans la liste déroulante **Langue sélectionnée** . Ces mots clés aident les utilisateurs du Centre logiciel à rechercher l’application.  

    -   **Icône** : choisissez **Parcourir** pour sélectionner une icône pour cette application parmi les icônes disponibles. Si vous ne spécifiez pas d’icône, une icône par défaut est utilisée pour cette application. Désormais, vous pouvez définir une icône avec des dimensions maximales de 512 x 512 pixels.

    -   **Afficher en tant qu’application proposée et la mettre en exergue sur le portail de l’entreprise** : cette option met en avant l’application sur le portail de l’entreprise.  

4.  Dans la page **Types de déploiement** de l’Assistant Création d’une application, choisissez **Ajouter** pour créer un type de déploiement.  

 Pour plus d’informations, consultez [Créer des types de déploiement pour l’application](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Choisissez **Suivant**, examinez les informations sur l’application figurant dans la page **Résumé**, puis suivez toutes les étapes de l’Assistant Création d’une application.  

La nouvelle application s’affiche dans le nœud **Applications** de la console Configuration Manager.  



##  <a name="create-deployment-types-for-the-application"></a>Créer des types de déploiement pour l'application  
 Si vous détectez automatiquement les informations de l’application, vous devrez peut-être finaliser certaines étapes de ces procédures.  

### <a name="start-the-create-deployment-type-wizard"></a>Démarrer l’Assistant Création d’un type de déploiement  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

3.  Sélectionnez une application puis, sous l’onglet **Accueil**, dans le groupe **Application**, choisissez **Créer un type de déploiement**.  

> [!TIP]  
>  Vous pouvez également démarrer l’Assistant Création d’un type de déploiement à partir de l’Assistant Création d’une application et sous l’onglet **Types de déploiement** de la boîte de dialogue **Propriétés de** *nom_application\>*.  

### <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Spécifier s’il est nécessaire de détecter automatiquement les informations sur le type de déploiement ou de configurer manuellement les informations  
 Utilisez l’une des procédures suivantes pour détecter automatiquement ou configurer manuellement les informations relatives au type de déploiement.  

#### <a name="automatically-detect-deployment-type-information"></a>Détecter automatiquement les informations relatives au type de déploiement  

1.  Dans la page **Général** de l’Assistant Création d’un type de déploiement, sélectionnez **Identifier automatiquement les informations sur ce type de déploiement à partir des fichiers d’installation**.  

2.  Dans la zone **Type**, sélectionnez le type du fichier d’installation d’application à utiliser pour détecter les informations sur le type de déploiement.  

3.  Dans la zone **Emplacement**, spécifiez le chemin réseau ou le lien vers le Store où se trouvent les fichiers d’installation de l’application. Configuration Manager utilise ces fichiers pour détecter les informations sur le type de déploiement. Vous pouvez également choisir **Parcourir** pour rechercher le fichier d’installation.  

    > [!NOTE]  
    >  Vous devez avoir accès au chemin réseau qui contient l’application et aux sous-dossiers où figure le contenu de l’application.  

4.  Dans la page **Importer des informations** de l’Assistant Création d’un type de déploiement, consultez les informations qui ont été importées, puis choisissez **Suivant**. Vous pouvez aussi choisir **Précédent** pour revenir en arrière et corriger les erreurs éventuelles.  

5.  Dans la page **Informations générales** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    > [!NOTE]  
    >  Certaines informations relatives au type de déploiement peuvent déjà être présentes si elles ont été lues à partir des fichiers d'installation de l'application. De plus, les options affichées peuvent différer selon le type de déploiement que vous créez.  

    -   Informations générales sur le type de déploiement, comme le nom, les commentaires de l’administrateur et les langues disponibles.  

    -   **Programme d'installation**: spécifiez le programme d'installation et les éventuelles propriétés nécessaires pour installer le type de déploiement.  

    -   **Comportement à l’installation** : indiquez si vous souhaitez installer le type de déploiement pour l’utilisateur actif ou tous les utilisateurs. Il existe une troisième option qui consiste à installer pour tous les utilisateurs si le déploiement s’effectue sur un seul appareil ou seulement pour un utilisateur déterminé si le déploiement concerne un seul utilisateur.  

    -   **Utiliser une connexion VPN automatique (si elle est configurée)**: Si un profil VPN a été déployé sur l'appareil sur lequel l'application est exécutée, lancez la connexion VPN au démarrage de l'application (Windows 8.1 et Windows Phone 8.1 uniquement). Si plusieurs profils VPN ont été déployés sur un appareil Windows 8.1, le premier profil VPN déployé est utilisé par défaut.  

         Sur les appareils Windows Phone 8.1, les connexions VPN automatiques ne sont pas prises en charge si plusieurs profils VPN ont été déployés sur l’appareil.  

         Pour plus d’informations, consultez [Profils VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Choisissez **Suivant**, puis passez à [Spécifier les options de contenu pour le type de déploiement](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

#### <a name="manually-set-up-the-deployment-type-information"></a>Configurer manuellement les informations sur le type de déploiement  

1.  Dans la page **Général** de l’Assistant Création d’un type de déploiement, dans la liste déroulante **Type**, choisissez le type de fichier d’installation de l’application pour ce type de déploiement. 

2.  Sélectionnez **Spécifier manuellement les informations sur le type de déploiement**, puis cliquez sur **Suivant**.

3.  Dans la page **Informations générales** de l’Assistant Création d’un type de déploiement, attribuez un nom au type de déploiement. Spécifiez éventuellement une description et les langues pour ce type de déploiement, puis cliquez sur **Suivant**.  

4.  Continuez avec [Spécifier les options de contenu pour le type de déploiement](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

###  <a name="specify-content-options-for-the-deployment-type"></a>Spécifier les options de contenu pour le type de déploiement  

1.  Dans la page **Contenu** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    -   **Emplacement du contenu** : spécifiez l’emplacement du contenu pour ce type de déploiement ou sélectionnez **Parcourir** pour choisir le dossier de contenu du type de déploiement.  

        > [!IMPORTANT]  
        >  Le compte du système de l'ordinateur du serveur de site doit disposer d'autorisations vers l'emplacement de contenu que vous spécifiez.  

    -   **Paramètres du contenu de désinstallation** : spécifiez l’une des options suivantes :
        - **Identique au contenu d’installation** : si le contenu d’installation et le contenu de désinstallation sont identiques, sélectionnez cette option. Il s’agit de l’option par défaut.
        - **Pas de contenu de désinstallation** : si votre application ne nécessite pas de contenu pour la désinstallation, sélectionnez cette option.
        - **Différent du contenu d’installation** : si le contenu de désinstallation est différent du contenu d’installation, sélectionnez cette option. Spécifiez ensuite l’emplacement du contenu d’application qui permet de désinstaller l’application.
5. Cliquez sur **OK** pour fermer la boîte de dialogue des propriétés de type de déploiement.

    -   **Conserver le contenu dans la mémoire cache du client** : sélectionnez cette option pour préciser si le client conserve indéfiniment le contenu dans le cache. Le client conserve le contenu même si l’application est déjà installée. Cette option est utile avec certains déploiements, comme les logiciels basés sur Windows Installer. Windows Installer a besoin d’une copie locale du contenu source pour appliquer les mises à jour. Il est cependant à noter que cette option réduit l’espace disponible dans le cache. Le choix de cette option peut entraîner l'échec d'un déploiement important plus tard si l'espace disponible dans le cache est insuffisant.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau** : pour réduire la charge sur le réseau, sélectionnez cette option. Les clients téléchargent le contenu auprès d’autres clients locaux du réseau qui ont déjà téléchargé et mis en cache ce contenu. Cette option utilise la technologie Windows BranchCache.  

    -   **Programme d’installation** : spécifiez le nom du programme d’installation et les paramètres d’installation requis ou choisissez **Parcourir** pour localiser le fichier d’installation.  

    -   **Début de l’installation dans** : spécifiez éventuellement le dossier contenant le programme d’installation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client ou un chemin vers le dossier du point de distribution contenant les fichiers d’installation.  

    -   **Programme de désinstallation** : spécifiez éventuellement le nom du programme de désinstallation, ainsi que les paramètres requis, le cas échéant, ou choisissez **Parcourir** pour le localiser.  

    -   **Début de la désinstallation dans** : spécifiez éventuellement le dossier contenant le programme de désinstallation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client. Il peut aussi s’agir d’un chemin relatif sur un point de distribution du dossier contenant le package.  

    -   **Exécutez l'installation et désinstallez le programme en tant que processus 32 bits sur des clients 64 bits**: utilisez les emplacements de fichier et de Registre 32 bits sur des ordinateurs fonctionnant sous Windows pour exécuter le programme d'installation pour le type de déploiement.  

2.  Choisissez **Suivant**.  

### <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Configurer des méthodes de détection pour indiquer la présence du type de déploiement (PC Windows uniquement)  
 Cette procédure configure une méthode de détection qui indique si le type de déploiement est déjà installé.  

1.  Dans la page **Méthode de détection** de l’Assistant Création d’un type de déploiement, sélectionnez **Configurer des règles pour détecter la présence de ce type de déploiement**, puis choisissez **Ajouter une clause**.  

    > [!NOTE]  
    >  Vous pouvez également sélectionner **Utiliser un script personnalisé pour détecter la présence de ce type de déploiement**. Pour plus d’informations, consultez [Utiliser un script personnalisé pour vérifier la présence d’un type de déploiement](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type).  

2.  Dans la liste déroulante **Type de paramètre** de la boîte de dialogue **Règle de détection**, choisissez la méthode que vous souhaitez utiliser pour détecter la présence du type de déploiement. Vous pouvez choisir parmi les méthodes disponibles suivantes :  

    -   **Système de fichiers** : détecte s’il existe un fichier ou un dossier spécifié sur un appareil client. Cette détection indique que l’application est installée.  

        > [!NOTE]  
        >  Le type de paramètre **Système de fichiers** ne permet pas de spécifier un chemin UNC de partage réseau dans le champ Chemin d’accès. Vous pouvez uniquement spécifier un chemin local sur l'appareil client.  
        >   
        >  Pour rechercher le fichier ou le dossier spécifié à des emplacements de fichiers 32 bits, sélectionnez d’abord **Ce fichier ou dossier est associé à une application 32 bits sur des systèmes 64 bits**. Si le fichier ou le dossier est introuvable, la recherche vise des emplacements 64 bits.  

    -   **Registre** : détermine si une clé ou une valeur de Registre spécifiée existe sur un appareil client. Cette détection indique que l’application est installée.  

        > [!NOTE]  
        >  Pour recherche la clé de Registre spécifiée à des emplacements du Registre 32 bits, sélectionnez d’abord l’option **Cette clé de Registre est associée à une application 32 bits sur des systèmes 64 bits**. Si la clé de Registre est introuvable, la recherche vise des emplacements 64 bits.  

    -   **Windows Installer** : détermine si un fichier Windows Installer spécifié existe sur un appareil client. Cette détection indique que l’application est installée.  

3.  Spécifiez les détails concernant l’élément pour déterminer si ce type de déploiement est installé. Par exemple, vous pouvez utiliser un fichier, un dossier, une clé ou valeur de Registre ou bien un code de produit Windows Installer.  

4.  Précisez si l’élément doit exister ou respecter une règle. Par exemple, si vous détectez un fichier, sélectionnez **Le paramètre du système de fichiers doit exister sur le système cible pour indiquer la présence de cette application**.  

5.  Choisissez **Suivant** pour fermer la boîte de dialogue **Règle de détection**.  

####  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Utiliser un script personnalisé pour vérifier la présence d’un type de déploiement  

1.  Dans la page **Méthode de détection** de l’Assistant Création d’un type de déploiement, sélectionnez **Utiliser un script personnalisé pour détecter la présence de ce type de déploiement**, puis choisissez **Modifier**.  

2.  Dans la boîte de dialogue **Éditeur de script**, sélectionnez la langue du script que vous souhaitez utiliser pour détecter le type de déploiement dans la liste déroulante **Type de script**.  

3.  Entrez le script à utiliser dans la zone **Contenu du script**. Vous pouvez également coller le contenu d’un script existant dans ce champ ou choisir **Ouvrir** pour accéder à un script existant enregistré. Configuration Manager vérifie les résultats du script. Il lit les valeurs écrites par le script dans le flux de sortie standard (STDOUT), le flux d’erreurs standard (STDERR) et le code de sortie. Si le script quitte avec une valeur non nulle, il échoue et l’état de la détection d’application est inconnu. Si le code de sortie est égal à zéro et STDOUT contient des données, l’état de la détection d’application est installé.  

 Utilisez le tableau suivant pour vérifier si une application est installée à partir de la sortie d’un script :  

|Code de sortie du script|Détails|
|--------------------------------|-----------------|
|0|**Données lues à partir de STDOUT** : Vide<br /><br /> **Données lues à partir de STDERR** : Vide<br /><br /> **Résultat du script** : Réussite<br /><br /> **État de détection de l’application** : Non installé|  
|0|**Données lues à partir de STDOUT** : Vide<br /><br /> **Données lues à partir de STDERR** : Non vide<br /><br /> **Résultat du script** : Échec<br /><br /> **État de détection de l’application** : Inconnu|  
|0|**Données lues à partir de STDOUT** : Non vide<br /><br /> **Données lues à partir de STDERR** : Vide<br /><br /> **Résultat du script** : Réussite<br /><br /> **État de détection de l’application** : Installé|  
|0|**Données lues à partir de STDOUT** : Non vide<br /><br /> **Données lues à partir de STDERR** : Non vide<br /><br /> **Résultat du script** : Réussite<br /><br /> **État de détection de l’application** : Installé|  
|Valeur non nulle|**Données lues à partir de STDOUT** : Vide<br /><br /> **Données lues à partir de STDERR** : Vide<br /><br /> **Résultat du script** : Échec<br /><br /> **État de détection de l’application** : Inconnu|  
|Valeur non nulle|**Données lues à partir de STDOUT** : Vide<br /><br /> **Données lues à partir de STDERR** : Non vide<br /><br /> **Résultat du script** : Échec<br /><br /> **État de détection de l’application** : Inconnu|  
|Valeur non nulle|**Données lues à partir de STDOUT** : Non vide<br /><br /> **Données lues à partir de STDERR** : Vide<br /><br /> **Résultat du script** : Échec<br /><br /> **État de détection de l’application** : Inconnu|  
|Valeur non nulle|**Données lues à partir de STDOUT** : Non vide<br /><br /> **Données lues à partir de STDERR** : Non vide<br /><br /> **Résultat du script** : Échec<br /><br /> **État de détection de l’application** : Inconnu|  

Le tableau suivant contient des exemples de script Microsoft Visual Basic (VB) que vous pouvez utiliser pour écrire vos propres scripts de détection d’application.  

|Exemple de script Visual Basic|Description|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|Le script renvoie un code de sortie non nul, ce qui indique l'échec d'exécution correcte. Dans ce cas, l'état de la détection d'application est inconnu.|  
|**WScript.StdErr.Write "Échec du script"**<br /><br /> **WScript.Quit(0)**|Le script retourne un code de sortie égal à zéro, mais la valeur de STDERR n’est pas vide. Ce résultat indique que le script n’a pas pu s’exécuter correctement. Dans ce cas, l'état de la détection d'application est inconnu.|  
|**WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, ce qui indique la réussite d'exécution. Toutefois, la valeur de STDOUT est vide, ce qui indique que l'application n'est pas installée.|  
|**WScript.StdOut.Write "L’application est installée"**<br /><br /> **WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, ce qui indique la réussite d'exécution. La valeur de STDOUT n'est pas vide, ce qui indique que l'application est installée.|  
|**WScript.StdOut.Write "L’application est installée"**<br /><br /> **WScript.StdErr.Write "Fin"**<br /><br /> **WScript.Quit(0)**|Le script renvoie un code de sortie égal à zéro, ce qui indique la réussite d'exécution. Les valeurs de STDOUT et STDERR ne sont pas vides, ce qui indique que l'application est installée.|  

 > [!NOTE]  
 >  La taille maximale que vous pouvez utiliser pour un script est 32 Ko.  

4.  Choisissez **OK** pour fermer la boîte de dialogue **Éditeur de script**.  

### <a name="specify-user-experience-options-for-the-deployment-type"></a>Spécifier les options d’expérience utilisateur pour le type de déploiement  
 Ces paramètres indiquent comment le client installe l’application sur les appareils et ce que l’utilisateur voit.  

1.  Dans la page **Expérience utilisateur** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    -   **Comportement à l'installation**: sélectionnez l'une des options suivantes dans la liste déroulante :  

        -   **Installer pour l’utilisateur** : l’application est installée uniquement pour l’utilisateur pour lequel elle est déployée.  

        -   **Installer pour le système**: l'application est installée une seule fois et elle est disponible pour tous les utilisateurs.  

        -   **Installer pour le système si la ressource est un périphérique ; sinon, installer pour l’utilisateur** : si l’application est déployée sur un appareil, le client l’installe pour tous les utilisateurs. Si l’application est déployée pour un utilisateur, le client l’installe uniquement pour cet utilisateur.  

    -   **Condition d'ouverture de session**: spécifiez les conditions d'ouverture de session pour ce type de déploiement à partir des options suivantes :  

        -   **Uniquement quand un utilisateur a ouvert une session**  

        -   **Qu’un utilisateur ait ouvert une session ou non**  

        -   **Uniquement lorsqu’aucun utilisateur n’a de session ouverte**  

        > [!NOTE]  
        >  Par défaut, cette option est définie sur **Uniquement lorsqu’un utilisateur a ouvert une session**. Si vous sélectionnez **Installer pour l’utilisateur** dans la liste déroulante **Comportement à l’installation**, vous ne pouvez pas modifier cette option.  

    -   **Visibilité du programme d’installation** : spécifiez le mode d’exécution du type de déploiement sur les appareils clients. Les options ci-dessous sont disponibles :  

        -   **Agrandi**: le type de déploiement est exécuté de manière agrandie sur les appareils clients. Les utilisateurs voient toute l’activité de l’installation.  

        -   **Normal**: le type de déploiement est exécuté en mode normal, en fonction des valeurs par défaut du système et du programme. Ce mode est la valeur par défaut.  

        -   **Réduit**: le type de déploiement est exécuté de manière réduite sur les appareils clients. Les utilisateurs peuvent voir l'activité de l'installation dans la zone de notification ou dans la barre des tâches.  

        -   **Masqué** : le type de déploiement s’exécute sous forme masquée sur les appareils clients. Les utilisateurs ne voient aucune activité d’installation.  

    -   **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme** : indique si un utilisateur peut interagir avec l’installation du type de déploiement pour configurer les options d’installation.  

        > [!NOTE]  
        >  Si vous sélectionner l’option **Installer pour l’utilisateur** dans la liste déroulante **Comportement à l’installation**, cette option est activée par défaut.  

        > [!IMPORTANT]
        > Depuis la version 1802, ce paramètre est facultatif quand vous sélectionnez le comportement **Installer pour le système**. Cette modification vise essentiellement à autoriser un utilisateur final à interagir avec l’installation au cours d’une séquence de tâches. Par exemple, pour exécuter un processus d’installation qui invite l’utilisateur final à choisir diverses options. Certains programmes d’installation d’application ne peuvent pas se passer d’invites utilisateur ou le processus d’installation exige des valeurs de configuration spécifiques que seul l’utilisateur connaît. <!--1356976-->
        > 
        > Une installation dans un contexte système avec des utilisateurs autorisés à interagir avec l'installation ne constitue pas une configuration sécurisée. Pour plus d’informations, consultez [Sécurité et confidentialité pour la gestion d’applications](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).

    -   **Durée maximale d'exécution allouée (en minutes)**: spécifiez la durée maximale d'exécution attendue du programme sur l'ordinateur client. Ce paramètre peut être spécifié comme un nombre entier supérieur à zéro. Le paramètre par défaut est de 120 minutes.  

         Cette valeur est utilisée pour :  

        -   surveiller les résultats du type de déploiement ;  

        -   vérifier si un type de déploiement est installé quand des fenêtres de maintenance sont définies sur des appareils clients. Quand une fenêtre de maintenance est en place, un programme ne démarre que s’il reste suffisamment de temps dans la fenêtre de maintenance pour respecter le paramètre **Durée maximale d’exécution allouée**.  

        > [!IMPORTANT]  
        >  Un conflit peut se produire si la **durée maximale d'exécution allouée** est plus longue que celle de la fenêtre de maintenance planifiée. Si la durée maximale d’exécution définie par l’utilisateur est supérieure à la longueur des fenêtres de maintenance disponibles, ce type de déploiement ne s’exécute pas.  

    -   **Temps d’installation estimé (minutes)**  : indique la durée d’installation estimée du type de déploiement. Les utilisateurs voient cette durée dans le Centre logiciel.  

    -   **Spécifier un comportement de redémarrage spécifique** : indique l’action post-installation. Les options ci-dessous sont disponibles :  

        -   **Déterminer le comportement en fonction des codes de retour** : gère les redémarrages en fonction des codes configurés sous l’onglet Codes de retour. Le Centre logiciel affiche **Peut nécessiter un redémarrage**. Si un utilisateur s’est connecté pendant l’installation, il reçoit une invite en fonction de la configuration de l’expérience utilisateur du déploiement.  

        -   **Aucune action spécifique** : aucun redémarrage n’est nécessaire après l’installation. Le Centre logiciel signale qu’aucun redémarrage n’est nécessaire.  
        -   **Le programme d’installation logicielle va forcer un redémarrage du périphérique** : Configuration Manager ne contrôle pas ou ne lance pas de redémarrage, mais l’installation elle-même peut le faire sans avertissement. Utilisez ce paramètre pour empêcher que Configuration Manager signale l’échec de l’installation quand le programme d’installation lance un redémarrage. Le Centre logiciel affiche **Peut nécessiter un redémarrage**.  

        -   **Le client Configuration Manager va forcer un redémarrage obligatoire du périphérique** : Configuration Manager force un redémarrage de l’appareil après une installation réussie. Le Centre logiciel signale qu’un redémarrage est nécessaire. Si un utilisateur s’est connecté pendant l’installation, il reçoit une invite en fonction de la configuration de l’expérience utilisateur du déploiement.

### <a name="specify-requirements-for-the-deployment-type"></a>Spécifier des spécifications pour le type de déploiement  

1.  Dans la page **Spécifications** de l’Assistant Création d’un type de déploiement, choisissez **Ajouter** pour ouvrir la boîte de dialogue **Créer une spécification**, puis ajoutez une nouvelle spécification.  

    > [!NOTE]  
    >  Vous pouvez également ajouter de nouvelles spécifications sous l’onglet **Spécifications** de la boîte de dialogue **Propriétés** de *<nom_type_déploiement\>*.  

2.  Dans la liste déroulante **Catégorie**, sélectionnez une option pour indiquer si cette spécification concerne un appareil ou un utilisateur. Sélectionnez **Personnalisée** pour utiliser une condition globale créée précédemment. Quand vous sélectionnez **Personnalisé**, vous pouvez également choisir **Créer** pour créer une condition globale. Pour plus d’informations sur les conditions globales, consultez [Comment créer des conditions globales](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Si vous déployez l’application sur un regroupement d’appareils, le client ignore la spécification de la catégorie **Utilisateur** et la condition **Périphérique principal**.  
    >   
    >  Si vous avez utilisé System Center 2012 R2 Configuration Manager SP1 pour créer un package Windows et un programme ou une séquence de tâches qui exige Windows 10, puis que vous effectuez une mise à niveau vers System Center Configuration Manager, l’exigence relative à Windows 10 peut être supprimée. Pour résoudre ce problème, spécifiez à nouveau la spécification. Même si l’exigence a été supprimée de l’affichage des spécifications, elle est toujours traitée correctement sur les appareils.  

3.  Dans la liste déroulante **Condition** , sélectionnez la condition que vous souhaitez utiliser pour déterminer si l'utilisateur ou l'appareil répond aux spécifications de l'installation. Le contenu de cette liste varie en fonction de la catégorie sélectionnée.  

4.  Dans la liste déroulante **Opérateur**, sélectionnez l’opérateur à utiliser. Cet opérateur compare la condition sélectionnée à la valeur spécifiée. Il évalue si l’utilisateur ou l’appareil respecte les spécifications de l’installation. Les opérateurs disponibles varient en fonction de la condition sélectionnée.  

    > [!IMPORTANT]  
    >  Les spécifications disponibles varient selon le type d’appareil utilisé par le type de déploiement.  

5.  Dans la zone **Valeur**, spécifiez les valeurs à utiliser. Ces valeurs, ainsi que la condition et l’opérateur sélectionnés, évaluent si l’utilisateur ou l’appareil respecte les spécifications de l’installation. Les valeurs disponibles varient en fonction de la condition et de l’opérateur sélectionnés.  

6.  Choisissez **OK** pour enregistrer la spécification et fermer la boîte de dialogue **Créer une spécification**.  

### <a name="specify-dependencies-for-the-deployment-type"></a>Spécifier des dépendances pour le type de déploiement  
 Les dépendances définissent un ou plusieurs types de déploiement d'un autre type d'application qui doivent être installés avant l'installation d'un type de déploiement. Vous pouvez configurer les types de déploiement dépendants à installer automatiquement avant l’installation d’un type de déploiement.  

> [!IMPORTANT]  
>  Dans certains cas, un type de déploiement est dépendant d’un type de déploiement qui a également des dépendances. Le nombre maximal de dépendances prises en charge dans la chaîne est de 5.  

1.  Dans la page **Dépendances** de l’Assistant Création d’un type de déploiement, choisissez **Ajouter**.  

    > [!IMPORTANT]  
    >  Vous pouvez également ajouter de nouvelles dépendances sous l’onglet **Dépendances** de la boîte de dialogue **Propriétés** de *<nom_type_déploiement\>*.  

2.  Dans la boîte de dialogue **Ajouter une dépendance**, choisissez **Ajouter**.  

3.  Dans la boîte de dialogue **Spécifier l'application requise** , sélectionnez une application existante et l'un des types de déploiement d'application à utiliser en tant que dépendance.  

    > [!TIP]  
    >  Vous pouvez choisir **Afficher** pour afficher les propriétés de l’application ou du type de déploiement sélectionné.  

4.  Choisissez **OK** pour fermer la boîte de dialogue **Spécifier l’application requise**.  

5.  Si vous souhaitez qu'une application dépendante soit installée automatiquement, voir **Installation automatique** à côté de l'application dépendante.  

    > [!NOTE]  
    >  Vous n’avez pas besoin de déployer une application dépendante pour qu’elle soit automatiquement installée.  

6.  Dans la boîte de dialogue **Ajouter une dépendance**, sous **Nom du groupe de dépendances**, entrez un nom pour faire référence à ce groupe de dépendances d’applications.  

7.  Vous pouvez éventuellement utiliser les boutons **Augmenter la priorité** et **Diminuer la priorité**. Ces actions changent l’ordre dans lequel le client évalue chaque dépendance.  

8.  Choisissez **OK** pour fermer la boîte de dialogue **Ajouter une dépendance**.  

### <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confirmer les paramètres relatifs au type de déploiement et terminer l’Assistant  

1.  Examinez le **Résumé**. Choisissez **Suivant** pour créer le type de déploiement. Choisissez **Précédent** pour revenir en arrière et modifier les paramètres du type de déploiement.  

2.  Après la fermeture de la page **Progression**, passez en revue les actions prises par l’Assistant, puis choisissez **Fermer** pour terminer l’Assistant.  

3.  Si vous avez démarré l’Assistant Création d’un type de déploiement à partir de l’Assistant Création d’une application, vous revenez à la page **Types de déploiement** de l’Assistant Création d’une application.  



## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Configurer des options supplémentaires pour les types de déploiement qui contiennent des applications virtuelles  
 Utilisez les procédures suivantes pour configurer des options supplémentaires pour les types de déploiement qui incluent des applications virtuelles.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Configurer les options de contenu pour les types de déploiement App-V (Application Virtualization)  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Applications**.  

2.  Dans la liste **Applications**, sélectionnez une application contenant un type de déploiement App-V. Ensuite, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

3.  Dans la boîte de dialogue **Propriétés de** *<nom_application\>*, sous l’onglet **Types de déploiement**, sélectionnez un type de déploiement App-V, puis choisissez **Modifier**.  

4.  Dans la boîte de dialogue **Propriétés de** *<Nom du type de déploiement\>*, sous l’onglet **Contenu**, configurez les options suivantes, si nécessaire :  

    -   **Conserver le contenu dans la mémoire cache du client** : sélectionnez cette option pour vérifier que le contenu de ce type de déploiement n’est pas supprimé du cache du client Configuration Manager.  

    -   **Charger le contenu dans le cache App-V avant le lancement**: sélectionnez cette option pour vous assurer que tout le contenu de l'application virtuelle est chargé dans le cache App-V avant le démarrage de l'application. Cette option garantit aussi que le contenu de l’application n’est pas épinglé dans le cache. Le client supprime le contenu selon les besoins.  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_type_déploiement\>*.  

6.  Choisissez **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_application\>*.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Configurer les options de publication pour les types de déploiement App-V  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Applications**.  

3.  Dans la liste **Applications**, sélectionnez une application contenant un type de déploiement App-V. Ensuite, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés de** *<nom_application\>*, sous l’onglet **Types de déploiement**, sélectionnez un type de déploiement App-V, puis choisissez **Modifier**.  

5.  Dans la boîte de dialogue **Propriétés de** *<nom_type_déploiement\>*, sous l’onglet **Publication**, sélectionnez les éléments de l’application virtuelle à publier.  

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_type_déploiement\>*.  

7.  Choisissez **OK** pour fermer la boîte de dialogue **Propriétés de** *<nom_application\>*.  



## <a name="import-an-application"></a>Importer une application  
 Utilisez la procédure ci-dessous pour importer une application dans Configuration Manager. Pour plus d’informations sur l’exportation d’une application, consultez [Tâches de gestion pour les applications System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.   

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Importer l’application**.  

4.  Dans la page **Général** de l’**Assistant Importation de l’application**, choisissez **Parcourir**. Spécifiez ensuite le chemin réseau du fichier .zip contenant l’application à importer.  

5.  Dans la page **Contenu du fichier**, sélectionnez l’action à effectuer si l’application que vous essayez d’importer est un doublon d’une application existante. Vous pouvez créer une application ou ignorer la copie et ajouter une nouvelle révision à l’application existante.  

6.  Dans la page **Résumé**, passez en revue les actions à effectuer, puis terminez l’Assistant.  

 La nouvelle application s’affiche dans le nœud **Applications**.  

> [!TIP]  
>  L’applet de commande Windows PowerShell **Import-CMApplication** permet de réaliser la même opération que cette procédure. Pour plus d’informations, consultez [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  



##  <a name="deployment-types-supported-by-configuration-manager"></a>Types de déploiement pris en charge par Configuration Manager  

|Nom du type de déploiement|Plus d'informations|  
|--------------------------|----------------------|  
|**Windows Installer (\*fichier .msi)**|Crée un type de déploiement à partir d'un fichier Windows Installer.|  
|**Package d’application Windows (\*.appx, \*.appxbundle)**|Crée un type de déploiement pour Windows 8 ou version ultérieure. Sélectionnez le fichier de package d’une application Windows ou le package d’un ensemble d’applications Windows.|  
|**Package d’application Windows (dans le Windows Store)**|Crée un type de déploiement pour Windows 8 ou version ultérieure. Spécifiez un lien vers l’application dans le Windows Store ou parcourez ce dernier pour sélectionner l’application.<br /><br /> Pour déployer l’application sous forme de lien vers le Windows Store, configurez le paramètre de stratégie de groupe **Désactiver l’application du Windows Store** sur **Désactivé** ou **Non configuré**. Si ce paramètre est activé, les clients ne peuvent pas se connecter au Windows Store pour télécharger et installer des applications.<br /><br /> Les types de déploiements de Windows 8 qui utilisent un lien vers un magasin sont toujours évalués avant d’autres types de déploiements, quelle que soit leur priorité.|  
|**Programme d’installation de script**|Crée un type de déploiement spécifiant un script qui s’exécute sur des appareils clients pour installer un contenu ou pour effectuer une action.|  
|**Microsoft Application Virtualization 4**|Crée un type de déploiement à partir d’un fichier manifeste Microsoft Application Virtualization 4.|  
|**Microsoft Application Virtualization 5**|Crée un type de déploiement à partir d'un fichier de package Microsoft Application Virtualization 5.|  
|**Package d’application Windows Phone (\*fichier .xap)**|Crée un type de déploiement à partir d'un fichier de package d'application Windows Phone.|  
|**Package d’application Windows Phone (dans le Windows Phone Store)**|Crée un type de déploiement en spécifiant un lien vers l’application dans le Windows Phone Store.|  
|**Package d’application pour iOS (fichier \*.ipa)**|Crée un type de déploiement à partir d'un fichier de package d'application iOS.|  
|**Package d’application pour iOS depuis l’App Store**|Crée un type de déploiement en spécifiant un lien vers l'application iOS dans l'App Store.|  
|**Package d’application pour Android (fichier \*.apk)**|Crée un type de déploiement à partir d'un fichier de package d'application Android.|  
|**Package d’application pour Android sur Google Play**|Crée un type de déploiement en spécifiant un lien vers l'application sur Google Play.|  
|**Mac OS X**|Crée un type de déploiement pour les ordinateurs Mac à partir d'un fichier .cmmac que vous avez créé à l'aide de l'outil CMAppUtil.<br /><br /> S’applique uniquement aux ordinateurs Mac exécutant le client Configuration Manager.|  
|**Application web**|Crée un type de déploiement qui spécifie un lien vers une application Web. Le type de déploiement installe un raccourci vers l'application Web sur l'appareil de l'utilisateur.<br /><br /> Si vous avez installé Microsoft Intune Managed Browser sur des appareils iOS ou Android, vérifiez que les utilisateurs peuvent uniquement utiliser Managed Browser pour ouvrir l’application. Utilisez l’un des formats suivants quand vous spécifiez un lien vers l’application : remplacez **http:** par **http-intunemam:** ou **https:** par **https-intunemam:**<br /><br /> - **http-intunemam://<chemin de l’application web\>**<br /><br /> - **https-intunemam://<chemin de l’application web\>**<br /><br /> Vous pouvez imposer une configuration requise pour Configuration Manager afin de vérifier que les applications à associer au navigateur Managed Browser sont installées uniquement sur des appareils iOS et Android.<br /><br /> Pour plus d’informations sur Intune Managed Browser, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer via la gestion des appareils mobiles (\*.msi)**|Ce type de programme d’installation vous permet de créer et déployer des applications Windows Installer sur des PC qui exécutent Windows 10.<br /><br /> Tenez compte des points suivants quand vous utilisez ce type de programme d’installation :<br><br>- Vous ne pouvez télécharger qu’un seul fichier avec l’extension .msi.<br /><br /> - Le code de produit et la version de produit du fichier sont utilisés pour la détection d’applications.<br /><br /> - Le comportement de redémarrage par défaut de l’application est utilisé. Configuration Manager ne contrôle pas ce redémarrage.<br /><br /> - Les packages MSI par utilisateur sont installés pour un seul utilisateur.<br /><br /> - Les packages MSI par ordinateur sont installés pour tous les utilisateurs sur l’appareil.<br /><br /> - Actuellement, les packages MSI en mode double s’installent uniquement pour tous les utilisateurs sur l’appareil.<br /><br /> - Les mises à jour d’application sont prises en charge quand le code de produit MSI de chaque version est identique.|  



## <a name="next-steps"></a>Étapes suivantes

Après avoir créé une application dans Configuration Manager, l’étape suivante consiste à [déployer l’application](/sccm/apps/deploy-use/deploy-applications).