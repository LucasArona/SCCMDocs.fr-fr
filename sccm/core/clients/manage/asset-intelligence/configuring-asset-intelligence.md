---
title: Configurer Asset Intelligence
titleSuffix: Configuration Manager
description: Configurez Asset Intelligence dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 08e0382d-de05-4a76-ba5c-7223173f7066
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33c10c82207d079dc5abd53c53673627888df955
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499738"
---
# <a name="configure-asset-intelligence-in-system-center-configuration-manager"></a>Configurer Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Asset Intelligence permet d’inventorier et de gérer l’utilisation des licences logicielles.   

## <a name="steps-to-configure-asset-intelligence"></a>Étapes de configuration d’Asset Intelligence  
   

- **Étape 1** : Pour collecter les données d’inventaire pour les rapports Asset Intelligence, vous devez activer l’agent d’inventaire matériel, comme cela est expliqué dans [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).
- **Étape 2** : [Activer les classes de création de rapports d’inventaire matériel Asset Intelligence](#BKMK_EnableAssetIntelligence).  
- **Étape 3** : [Installer un point de synchronisation Asset Intelligence](#BKMK_InstallAssetIntelligenceSynchronizationPoint)
- **Étape 4** : [Activer l’audit des événements de connexion réussie](#BKMK_EnableSuccessLogonEvents)  
- **Étape 5** : [Importer les informations de licence logicielle](#BKMK_ImportSoftwareLicenseInformation)  
- **Étape 6** : [Configurer les tâches de maintenance Asset Intelligence](#BKMK_ConfigureMaintenanceTasks) 


###  <a name="BKMK_EnableAssetIntelligence"></a> Activer les classes de création de rapports d’inventaire matériel Asset Intelligence  
 Pour activer Asset Intelligence sur les sites Configuration Manager, vous devez activer au moins une des classes de création de rapports d’inventaire matériel Asset Intelligence. Vous pouvez activer les classes sur la page d'accueil **Asset Intelligence** ou, dans l'espace de travail **Administration** , dans le nœud **Paramètres client** , dans les propriétés des paramètres client. Procédez selon l'une des méthodes suivantes :  

##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-the-asset-intelligence-home-page"></a>Pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence depuis la page d'accueil Asset Intelligence  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Asset Intelligence**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Asset Intelligence**, choisissez **Modifier les classes d’inventaire**.   

4.  Pour activer la création de rapports Asset Intelligence, sélectionnez **Activer toutes les classes de création de rapports Asset Intelligence** ou **Activer uniquement les classes de création de rapports Asset Intelligence sélectionnées**, puis sélectionnez au moins une classe de création de rapports dans les classes affichées.  

    > [!NOTE]  
    >  Les rapports Asset Intelligence qui dépendent des classes d'inventaire matériel que vous activez en utilisant cette procédure n'affichent pas de données tant que les clients n'ont pas établi et retourné un inventaire matériel.  


##### <a name="to-enable-asset-intelligence-hardware-inventory-reporting-classes-from-client-settings-properties"></a>Pour activer les classes de création de rapports d'inventaire matériel Asset Intelligence depuis les propriétés des paramètres client  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Paramètres client** > **Paramètres d’agent client par défaut**. Si vous avez créé des paramètres client personnalisés, vous pouvez sélectionner ces paramètres à la place.  

3.  Sous l’onglet **Accueil** > groupe **Propriétés**, choisissez **Propriétés**.   

4.  Choisissez **Inventaire matériel** > **Déf. classes**. .  

5.  Choisissez **Filtrer par catégorie** > **Classes de création de rapports Asset Intelligence**. La liste des classes est actualisée avec uniquement les classes de création de rapports d'inventaire matériel Asset intelligence.  

6.  Sélectionnez au moins une classe de création de rapports dans la liste.  

    > [!NOTE]  
    >  Les rapports Asset Intelligence qui dépendent des classes d'inventaire matériel que vous activez en utilisant cette procédure n'affichent pas de données tant que les clients n'ont pas établi et retourné un inventaire matériel.  
  

###  <a name="BKMK_InstallAssetIntelligenceSynchronizationPoint"></a> Installer un point de synchronisation Asset Intelligence  

Le rôle de système de site du point de synchronisation Asset Intelligence permet de connecter des sites Configuration Manager à System Center Online pour synchroniser les informations du catalogue Asset Intelligence. Le point de synchronisation Asset Intelligence peut uniquement être installé sur un système de site de niveau supérieur dans la hiérarchie Configuration Manager. De plus, il a besoin d’un accès Internet pour se synchroniser avec System Center Online via le port TCP 443.

Outre le téléchargement des nouvelles informations du catalogue Asset Intelligence, le point de synchronisation Asset Intelligence peut envoyer les informations de titres de logiciels personnalisés à System Center Online à des fins de catégorisation. Microsoft considère tous les titres de logiciels téléchargés comme des informations publiques. Assurez-vous que vos titres de logiciels personnalisés ne contiennent pas d’informations confidentielles ou propriétaires. Pour plus d’informations sur la demande de catégorisation des titres de logiciels, consultez [Demander une mise à jour du catalogue pour les logiciels sans catégorie](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_RequestCatalogUpdate).  

##### <a name="to-install-an-asset-intelligence-synchronization-point-site-system-role"></a>Pour installer un rôle de système de site de point de synchronisation Asset Intelligence  

1.  Dans la console Configuration Manager, choisissez **Administration**> **Configuration du site** > **Serveurs et rôles de système de site**.  

3.  Ajoutez le rôle de système de site du point de synchronisation Asset Intelligence à un serveur de système de site nouveau ou existant :  

    -  Pour un **Nouveau serveur de système de site** : Dans l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un serveur de système de site** pour démarrer l’Assistant.   

        > [!NOTE]  
        >  Par défaut, quand Configuration Manager installe un rôle système de site, les fichiers d’installation sont installés sur le premier disque dur formaté NTFS disponible qui a le plus d’espace disque libre. Pour empêcher Configuration Manager d’effectuer l’installation sur des disques particuliers, créez un fichier vide « No_sms_on_drive.sms » et copiez-le dans le dossier racine du disque avant d’installer le serveur de système de site.  

    -  Pour un **Serveur de système de site existant** : Choisissez le serveur sur lequel vous souhaitez installer le rôle de système de site du point de synchronisation Asset Intelligence. Quand vous choisissez un serveur, la liste des rôles de système de site déjà installés sur le serveur s’affiche dans le volet Détails.  

         Sous l’onglet **Accueil**, dans le groupe **Serveur**, choisissez **Ajouter des rôles de système de site** pour démarrer l’Assistant.  

4.  Renseignez la page **Général**. Lorsque vous ajoutez le point de synchronisation Asset Intelligence à un serveur de système de site existant, vérifiez les valeurs qui ont été précédemment configurées.  

5.  Dans la page **Sélection du rôle système**, sélectionnez **Point de synchronisation Asset Intelligence** dans la liste des rôles disponibles.  

6.  Dans la page des **paramètres de connexion du point de synchronisation Asset Intelligence**, choisissez **Suivant**.  

     Par défaut, le paramètre **Utiliser ce point de synchronisation Asset Intelligence** est sélectionné et ne peut pas être configuré sur cette page. Comme System Center Online accepte le trafic réseau uniquement sur le port TCP 443, le paramètre de **numéro de port SSL** ne peut pas être défini dans cette page de l'Assistant.  

7.  Éventuellement, spécifiez le chemin du fichier de certificat d’authentification (.pfx) System Center Online. En règle générale, vous ne spécifiez pas un chemin d'accès pour le certificat, car le certificat de connexion est préparé automatiquement pendant l'installation du rôle de site.  

8.  Dans la page **Paramètres du serveur proxy**, indiquez si le point de synchronisation Asset Intelligence doit utiliser un serveur proxy lors de la connexion à System Center Online pour synchroniser le catalogue et si des données d’identification sont nécessaires pour se connecter au serveur proxy.  

    > [!WARNING]  
    >  Si un serveur proxy est nécessaire pour la connexion à System Center Online, le certificat de connexion peut être également supprimé si le mot de passe du compte d'utilisateur expire pour le compte défini pour l'authentification du serveur proxy.  

9. Sur la page **Calendrier des synchronisations** , indiquez si vous souhaitez synchroniser le catalogue Asset Intelligence dans un calendrier. Lorsque vous activez le calendrier des synchronisations, vous pouvez définir un calendrier de synchronisation simple ou personnalisé. Pendant la synchronisation planifiée, le point de synchronisation Asset Intelligence se connecte à System Center Online pour récupérer le dernier catalogue Asset Intelligence. Vous pouvez synchroniser manuellement le catalogue Asset Intelligence depuis le nœud Asset Intelligence dans la console Configuration Manager. Pour savoir comment synchroniser manuellement le catalogue Asset Intelligence, consultez la section [Pour synchroniser manuellement le catalogue Asset Intelligence](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ManuallySynchronizeCatalog) dans la rubrique [Opérations pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).  

10. Effectuer toutes les étapes de l'Assistant 

###  <a name="BKMK_EnableSuccessLogonEvents"></a> Activer l’audit des événements de connexion réussie  
 Quatre rapports Asset Intelligence affichent des informations extraites des journaux d'événements de sécurité Windows sur les ordinateurs client. Voici comment configurer les paramètres d’ouverture de session de la stratégie de sécurité des ordinateurs pour activer l’audit des événements associés aux ouvertures de session qui aboutissent.  

##### <a name="to-enable-success-logon-event-logging-by-using-a-local-security-policy"></a>Pour activer la journalisation des événements associés aux ouvertures de session qui aboutissent en utilisant une stratégie de sécurité locale  

1.  Sur un ordinateur client Configuration Manager, choisissez **Démarrer** > **Outils d’administration** > **Stratégie de sécurité locale**.  

2.  Dans la boîte de dialogue **Stratégie de sécurité locale**, sous **Paramètres de sécurité**, développez **Stratégies locales**, puis choisissez **Stratégie d’audit**.  

3.  Dans le volet des résultats, double-cliquez sur **Auditer les événements de connexion**, cochez la case **Succès** et choisissez **OK**.  

##### <a name="to-enable-success-logon-event-logging-by-using-an-active-directory-domain-security-policy"></a>Pour activer la journalisation des événements d'ouverture de session qui aboutissent en utilisant une stratégie de sécurité du domaine Active Directory  

1.  Sur un ordinateur contrôleur de domaine, choisissez **Démarrer**, pointez sur **Outils d’administration**, puis choisissez **Stratégie de sécurité du domaine**.  

2.  Dans la boîte de dialogue **Stratégie de sécurité locale**, sous **Paramètres de sécurité**, développez **Stratégies locales**, puis choisissez **Stratégie d’audit**.  

3.  Dans le volet des résultats, double-cliquez sur **Auditer les événements de connexion**, cochez la case **Succès** et choisissez **OK**.  

###  <a name="BKMK_ImportSoftwareLicenseInformation"></a> Importer les informations de licence logicielle  
 Les sections suivantes décrivent les procédures permettant d’importer des informations de licences logicielles Microsoft et générales dans la base de données de site Configuration Manager en utilisant l’Assistant Importer des licences logicielles. Lorsque vous importez des informations de licence de logiciel vers la base de données de site depuis des fichiers de déclaration de licence, le compte de l'ordinateur serveur de site doit disposer des autorisations **Contrôle intégral** pour le système de fichiers NTFS du partage de fichiers utilisé pour importer les informations de licence de logiciel.  

> [!IMPORTANT]  
>  Les informations de licence logicielle importées dans la base de données de site remplacent les informations existantes. Vérifiez que le fichier d'informations de licence logicielle que vous utilisez avec Assistant Importer des licences logicielles contient la liste complète des informations de licence logicielle nécessaires.  

##### <a name="to-import-software-license-information-into-the-asset-intelligence-catalog"></a>Pour importer des informations de licence logicielle vers le catalogue Asset Intelligence  

1.  Dans l’espace de travail **Ressources et Conformité**, choisissez **Asset Intelligence**.  

2.  Sous l’onglet **Accueil**, dans le groupe **Asset Intelligence**, choisissez **Importer des licences logicielles**.   

4.  Sur la page **Importer** , spécifiez si vous importez un fichier MVLS (Microsoft Volume Licensing) (.xml ou .csv) ou un fichier de déclaration de licence générale (.csv). Pour plus d'informations sur la création d'un fichier de déclaration de licence générale, voir [Créer un fichier d’informations de déclaration de licence générale à importer](#BKMK_CreateGeneralLicenseStatement) plus loin dans cette rubrique.  

    > [!WARNING]  
    >  Pour télécharger un fichier MVLS de format .csv que vous pouvez importer vers le catalogue Asset Intelligence, consultez [Centre de gestion des licences en volume Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=226547). Pour accéder à ces informations, vous devez disposer d'un compte enregistré sur le site Web. Vous devez contacter votre responsable de compte Microsoft pour plus d'informations sur la façon d'obtenir votre fichier MVLS de format .xml.  

5.  Entrez le chemin d’accès UNC du fichier de déclaration de licence ou choisissez **Parcourir** pour sélectionner un dossier réseau partagé et un fichier.  

    > [!NOTE]  
    >  Le dossier partagé doit être correctement sécurisé pour empêcher tout accès non autorisé au fichier d'informations de licence. En outre, le compte de l'ordinateur sur lequel l'Assistant est exécuté doit avoir les autorisations de contrôle intégral sur le partage contenant le fichier d'importation de licence.  

6. Effectuez toutes les étapes de l'Assistant.  

###  <a name="BKMK_CreateGeneralLicenseStatement"></a> Créer un fichier d’informations de déclaration de licence générale à importer  
 Une déclaration de licence générale peut également être importée vers le catalogue Asset Intelligence en utilisant un fichier d'importation de licence de format .csv (délimité par des virgules) créé manuellement.  

> [!NOTE]  
>  Seuls les champs **Nom**, **Éditeur**, **Version**et **Quantité effective** sont requis, mais ils doivent tous être entrés sur la première ligne du fichier d'importation de licence. Tous les champs de date doivent être affichés dans le format suivant : Jour/mois/année, par exemple 04/08/2008.  

Asset Intelligence fait correspondre les produits que vous spécifiez dans la déclaration de licence générale en utilisant le nom du produit et la version du produit, mais pas le nom de l'éditeur. Vous devez utiliser un nom de produit dans la déclaration de licence générale qui correspond exactement au nom de produit stocké dans la base de données du site. Asset Intelligence utilise le nombre **Quantité effective** donné dans la déclaration de licence générale et le compare au nombre de produits installés trouvés dans l’inventaire Configuration Manager.  

> [!TIP]  
>  Pour obtenir la liste complète des noms de produits stockés dans la base de données du site Configuration Manager, vous pouvez exécuter la requête suivante sur la base de données du site : SELECT ProductName0 FROM v_GS_INSTALLED_SOFTWARE.  

 Vous pouvez spécifier les versions exactes pour un produit ou spécifier une partie de la version, comme par exemple uniquement la version principale. Les exemples suivants présentent les correspondances de version obtenues pour une entrée de version de déclaration générale de licence pour un produit spécifique.  

|Entrée de déclaration de licence générale|Correspondance avec les entrées de la base de données de site|  
|-------------------------------------|------------------------------------|  
|Nom : « MySoftware », ProductVersion0 : « 2 »|ProductName0 : « Mysoftware », ProductVersion0 : « 2.01.1234 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.02.5678 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.05.1234 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.05.5678 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.05.3579.000 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.10.1234 »|  
|Nom : « MySoftware », Version « 2.05 »|ProductName0 : « MySoftware », ProductVersion0 : « 2.05.1234 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.05.5678 »<br /><br /> ProductName0 : « MySoftware », ProductVersion0 : « 2.05.3579.000 »|  
|Nom : « Mysoftware », Version « 2 »<br /><br /> Nom : « MySoftware », Version « 2.05 »|Erreur lors de l'importation. L'importation échoue lorsque plusieurs entrées correspondent à la même version du produit.|  
  

##### <a name="to-create-a-general-license-statement-import-file-by-using-microsoft-excel"></a>Pour créer un fichier d'importation de déclaration de licence générale à l'aide de Microsoft Excel  

1.  Ouvrez Microsoft Excel et créez une nouvelle feuille de calcul.  

2.  Sur la première ligne de la nouvelle feuille de calcul, saisissez tous les noms de champs de données des licences logicielles.  

3.  À partir de la deuxième ligne, entrez les informations de licence logicielle requises. Assurez-vous que tous les champs de données des licences logicielles requis sont saisis sur les lignes suivantes pour chaque licence logicielle qui doit être importée. Le nom de logiciel saisi dans la feuille de calcul doit être le même que le nom de logiciel affiché dans l'Explorateur de ressources pour un ordinateur client, après avoir exécuté l'inventaire matériel.  

4.  Enregistrez le fichier au format .csv.  

5.  Copiez le fichier .csv dans le partage de fichiers utilisé pour l'importation des informations de licence logicielle dans le catalogue Asset Intelligence.  

6.  Dans la console Configuration Manager, utilisez l’Assistant Importer des licences logicielles pour importer le nouveau fichier .csv.  

7.  Générez le **rapport de rapprochement des licences logicielles tierces (licence 15A)** d’Asset Intelligence pour vérifier que les informations de licence ont bien été importées dans le catalogue Asset Intelligence.  

> [!NOTE]  
>  Pour obtenir un exemple de fichier de licence logicielle générale que vous pouvez utiliser à des fins de test, consultez [Exemple de fichier d’importation de licence générale Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-asset-intelligence-general-license-import.md).  

#### <a name="sample-table-to-describe-software-licenses"></a>Exemple de tableau utilisé pour décrire des licences logicielles  
 Lors de la création d'un fichier d'importation de déclaration de licence générale, les informations figurant dans le tableau suivant peuvent être utilisées pour décrire les licences logicielles à importer dans le catalogue Asset Intelligence.  

|Nom de la colonne|Type de données|Obligatoire|Exemple|  
|-----------------|---------------|--------------|-------------|  
|Nom|Jusqu'à 255 caractères|Oui|Nom du logiciel|  
|Éditeur|Jusqu'à 255 caractères|Oui|Éditeur du logiciel|  
|Version|Jusqu'à 255 caractères|Oui|Version du logiciel|  
|Langage|Jusqu'à 255 caractères|Oui|Langue du logiciel|  
|Quantité effective|Valeur entière|Oui|Nombre de licences achetées|  
|Numéro BC|Jusqu'à 255 caractères|Non|Informations sur les BC|  
|Nom du revendeur|Jusqu'à 255 caractères|Non|Informations sur le revendeur|  
|Date d'achat|Date au format suivant : MM/JJ/AAAA|Non|Date d'achat de la licence|  
|Achat de la prise en charge|Valeur en bits|Non|0 ou 1 : Entrez 0 pour Oui ou 1 pour Non|  
|Date d'expiration de la prise en charge|Date au format suivant : MM/JJ/AAAA|Non|Date de fin de la prise en charge achetée|  
|Commentaires|Jusqu'à 255 caractères|Non|Commentaires facultatifs|  

###  <a name="BKMK_ConfigureMaintenanceTasks"></a> Configurer les tâches de maintenance Asset Intelligence  
 Les tâches de maintenance suivantes sont disponibles pour Asset Intelligence :  

-   **Vérifier le titre de l’application à l’aide des informations d’inventaire** : Vérifie que le titre du logiciel indiqué dans l’inventaire logiciel est rapproché du titre du logiciel dans le catalogue Asset Intelligence. Par défaut, cette tâche est activée et planifiée pour être exécutée le samedi entre 00 h 00 et 5 h 00. Cette tâche de maintenance est uniquement disponible sur le site de niveau supérieur de la hiérarchie Configuration Manager.  

-   **Résumer les données du logiciel installé** : Fournit les informations affichées dans l’espace de travail**Ressources et conformité**, dans le nœud **Logiciels inventoriés**, sous le nœud **Asset Intelligence**. Quand la tâche s’exécute, Configuration Manager compte les titres de logiciels inventoriés sur le site principal. Par défaut, cette tâche est activée et planifiée pour être exécutée tous les jours entre 00 h 00 et 5 h 00. Cette tâche de maintenance est disponible uniquement sur les sites principaux.  

##### <a name="to-configure-asset-intelligence-maintenance-tasks"></a>Pour configurer les tâches de maintenance Asset Intelligence  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Sites**.  

3.  Sélectionnez le site sur lequel vous allez configurer la tâche de maintenance Asset Intelligence.  

4.  Sous l’onglet **Accueil**, dans le groupe **Paramètres**, choisissez **Maintenance de site**. Sélectionnez une tâche, puis choisissez **Modifier** pour modifier les paramètres. 

    Nous vous recommandons de définir la période aux heures creuses d’utilisation du site. La période représente l'intervalle de temps au cours duquel la tâche peut être exécutée. Elle est définie par les paramètres **Démarrer après** et **Heure de début au plus tard** spécifiés dans la boîte de dialogue **Propriétés de la tâche** .  

    Vous pouvez lancer immédiatement la tâche en sélectionnant le jour actuel et en réglant la valeur **Démarrer après** quelques minutes après le moment présent.  

7.  Choisissez **OK** pour enregistrer vos paramètres. La tâche est désormais exécutée conformément à sa planification.  

    > [!NOTE]  
    >  Si l’exécution d’une tâche échoue à la première tentative, Configuration Manager retente de l’exécuter jusqu’à la réussite de l’opération ou l’expiration de la période d’exécution planifiée.  
