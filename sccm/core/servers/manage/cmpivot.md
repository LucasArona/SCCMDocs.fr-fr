---
title: CMPivot pour les données en temps réel
titleSuffix: Configuration Manager
description: Découvrez comment utiliser CMPivot dans Configuration Manager pour interroger les clients en temps réel.
ms.date: 04/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd914030afb8490b11666fc953d846e03090b834
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802646"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot pour les données en temps réel dans Configuration Manager

<!--1358456-->

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager met à disposition un grand magasin de données d’appareils centralisé, que les clients utilisent pour générer des rapports. Le site collecte généralement ces données chaque semaine. Depuis la version 1806, CMPivot est un nouvel utilitaire de console, qui permet désormais d’accéder à l’état en temps réel des appareils de votre environnement. Il exécute immédiatement une requête sur tous les appareils actuellement connectés du regroupement cible, et retourne les résultats. Filtrez et regroupez ensuite ces données dans l’outil. En fournissant les données en temps réel des clients en ligne, vous pouvez répondre plus rapidement aux questions métier, résoudre les problèmes et corriger les incidents de sécurité.

Par exemple, si vous souhaitez [limiter les vulnérabilités d’exécution spéculative côté canal](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), l’une des exigences est de mettre à jour le BIOS système. Vous pouvez utiliser CMPivot pour interroger rapidement les informations relatives au BIOS système, et rechercher les clients non conformes.

 > [!Tip]  
 > Certains logiciels de sécurité peuvent bloquer les scripts qui s’exécutent à partir de c:\windows\ccm\scriptstore. Cela peut empêcher l’exécution correcte des requêtes CMPivot. Certains logiciels de sécurité peuvent également générer des événements d’audit ou des alertes lors de l’exécution de CMPivot PowerShell.


## <a name="prerequisites"></a>Prérequis

Les composants suivants sont obligatoires pour l’utilisation de CMPivot :

- Mettez à niveau les appareils cibles vers la dernière version du client Configuration Manager.  

- Autorisations pour CMPivot :
  - Autorisation **Lecture** sur l’objet **Scripts SMS**
  - Autorisation **Exécuter les scripts** sur le **Regroupement**
  - Autorisation **Lecture** sur les **Rapports d’inventaire**
  - Portée par défaut. 

- Les clients cibles nécessitent au moins PowerShell version 4.

- Pour collecter des données pour les entités suivantes, les clients cibles nécessitent PowerShell version 5.0 :  
  - Administrateurs
  - Connexion
  - IPConfig
  - SMBConfig

 
## <a name="limitations"></a>Limitations

- Dans une hiérarchie, connectez la console Configuration Manager à un *site principal* pour exécuter CMPivot. L’action **Démarrer CMPivot** n’apparaît pas dans la console quand elle est connectée à un site d’administration centrale (CAS).
  - À compter de Configuration Manager version 1902, vous pouvez exécuter CMPivot à partir d’un site d’administration centrale. Dans certains environnements, des autorisations supplémentaires sont nécessaires. Pour plus d’informations, consultez [CMPivot à compter de la version 1902](#bkmk_cmpivot1902).

- CMPivot ne retourne que les données des clients connectés au site actuel.  

- Si un regroupement contient des appareils d’un autre site, les résultats de CMPivot concernent uniquement les appareils du site actuel.  

- Vous ne pouvez pas personnaliser les propriétés des entités, les colonnes des résultats ou les actions des appareils.  

- Vous pouvez uniquement exécuter une seule instance à la fois de CMPivot sur un ordinateur qui dispose de la console Configuration Manager.  

- Dans la version 1806, la requête pour l’entité **Administrateurs** ne fonctionne que si le groupe est nommé « Administrators ». Il ne fonctionne pas si le nom du groupe est localisé. Par exemple, « Administrateurs » en Français.<!--SCCMDocs issue 759-->  


## <a name="start-cmpivot"></a>Démarrer CMPivot

1. Dans la console Configuration Manager, connectez-vous au site principal. Accédez à l’espace de travail **Ressources et Conformité**, puis sélectionnez le nœud **Regroupements d’appareils**. Sélectionnez un regroupement cible, puis cliquez sur **Démarrer CMPivot** dans le ruban pour lancer l’outil.  

    > [!Tip]  
    > Si vous ne voyez pas cette option, vérifiez les configurations suivantes :  
    > 
    > - Vérifiez auprès d’un administrateur de site que votre compte dispose des autorisations nécessaires. Pour plus d’informations, consultez [Prérequis](#prerequisites).  
    > 
    > - Connectez la console à un *site principal*.  

2. L’interface fournit davantage d’informations sur l’utilisation de l’outil.  

     - Entrez manuellement les chaînes de requête en haut de la fenêtre, ou cliquez sur les liens dans la documentation en ligne.  

     - Cliquez sur l’une des **Entités** pour l’ajouter à la chaîne de requête.  

     - Les liens concernant les **opérateurs de table**, les **fonctions d’agrégation** et les **fonctions scalaires** ouvrent une documentation de référence de langage dans le navigateur web. CMPivot utilise le même langage de requête que [Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).  

3. Gardez la fenêtre CMPivot ouverte pour voir les résultats des clients. Quand vous fermez la fenêtre CMPivot, la session s’achève.  

    > [!Note]  
    > Si la requête a été envoyée, les clients continuent d’adresser une réponse au message d’état à destination du serveur.  



## <a name="how-to-use-cmpivot"></a>Guide pratique pour utiliser CMPivot

![Exemple de fenêtre CMPivot](media/1358456-cmpivot-sample.png)

La fenêtre CMPivot contient les éléments suivants :  

1. Le regroupement ciblé par CMPivot est indiqué dans la barre de titre en haut de la fenêtre, ainsi que dans la barre d’état en bas de la fenêtre. Par exemple, « PM_Team_Machines » dans la capture d’écran ci-dessus.  

2. Le volet de gauche liste les **entités** disponibles sur les clients. Certaines entités dépendent de WMI, tandis que d’autres utilisent PowerShell pour obtenir les données auprès des clients.   

    - Cliquez avec le bouton droit sur une entité pour les actions suivantes :  

       - **Insérer** : permet d’ajouter l’entité à la requête à la position actuelle du curseur. La requête ne s’exécute pas automatiquement. Il s’agit de l’action par défaut quand vous double-cliquez sur une entité. Utilisez cette action quand vous créez une requête.  

       - **Requête pour tout** : permet d’exécuter une requête pour cette entité, en incluant toutes les propriétés. Utilisez cette action pour interroger rapidement une seule entité.  

       - **Requête par appareil** : permet d’exécuter une requête pour cette entité, et de regrouper les résultats. Par exemple, `Disk | summarize dcount( Device ) by Name`  

    - Développez une entité pour voir les propriétés spécifiques disponibles pour chaque entité. Double-cliquez sur une propriété pour l’ajouter à la requête, à la position actuelle du curseur.  

3. L’onglet **Accueil** affiche des informations générales sur CMPivot, notamment des liens vers des exemples de requêtes et de la documentation d’aide.  

4. L’onglet **Requête** affiche le volet de requête, le volet de résultats et la barre d’état. L’onglet Requête est sélectionné dans l’exemple de capture d’écran ci-dessus.  

5. Le volet de requête est l’emplacement où vous créez ou tapez une requête à exécuter sur les clients du regroupement.  

    - CMPivot utilise un sous-ensemble du même langage de requête qu’[Azure Log Analytics](https://docs.microsoft.com/azure/kusto/query/).  

    - Coupez, copiez ou collez du contenu dans le volet de requête.  

    - Par défaut, ce volet utilise IntelliSense. Par exemple, si vous commencez à taper `D`, IntelliSense suggère toutes les entités qui commencent par cette lettre. Sélectionnez une option, puis appuyez sur la touche Tab pour l’insérer. Tapez le caractère correspondant à une barre verticale, suivi d’un espace `| `, pour qu’IntelliSense suggère tous les opérateurs de table. Insérez `summarize`, puis tapez un espace, pour qu’IntelliSense suggère toutes les fonctions d’agrégation. Pour plus d’informations sur ces opérateurs et ces fonctions, cliquez dans CMPivot sur l’onglet **Accueil**.  

    - Le volet de requête offre également les possibilités suivantes :  

        - Exécuter la requête  

        - Avancer et reculer dans l’historique des requêtes  

        - Créer un regroupement d’adhésion directe  

        - Exporter les résultats de la requête au format CSV ou vers le Presse-papiers  

6. Le volet de résultats affiche les données retournées par les clients actifs pour la requête.  

   - Les colonnes disponibles varient en fonction de l’entité et de la requête.  

   - Cliquez sur un nom de colonne pour trier les résultats en fonction de cette propriété.  

   - Cliquez avec le bouton droit sur un nom de colonne pour regrouper les résultats en fonction d’informations identiques, ou pour trier ces résultats.  

   - Cliquez avec le bouton droit sur un nom d’appareil pour effectuer les actions supplémentaires suivantes sur l’appareil :  

      - **Ajouter un tableau croisé dynamique à** : permet d’interroger une autre entité sur cet appareil.  

      - **Exécuter le script** : permet de lancer l’Assistant Exécuter le script pour exécuter un script PowerShell existant sur cet appareil. Pour plus d’informations, consultez [Exécuter un script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

      - **Contrôle à distance** : permet de lancer une session de contrôle à distance Configuration Manager sur cet appareil. Pour plus d’informations, consultez [Guide pratique pour administrer à distance un ordinateur client Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

      - **Explorateur de ressources** : permet de lancer l’Explorateur de ressources Configuration Manager pour cet appareil. Pour plus d’informations, consultez [Afficher l’inventaire matériel](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) ou [Afficher l’inventaire logiciel](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

   - Cliquez avec le bouton droit sur une cellule qui ne contient pas d’appareil pour effectuer les actions supplémentaires suivantes :  

     - **Copier** : permet de copier le texte de la cellule dans le Presse-papiers.  

     - **Afficher les appareils avec** : permet d’interroger les appareils ayant cette valeur de propriété. Par exemple, à partir des résultats de la requête `OS`, sélectionnez cette option sur une cellule de la ligne Version : `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

     - **Afficher les appareils sans** : permet d’interroger les appareils n’ayant pas cette valeur de propriété. Par exemple, à partir des résultats de la requête `OS`, sélectionnez cette option sur une cellule de la ligne Version : `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

     - **Rechercher sur Bing** : permet de lancer le navigateur web par défaut sur www.bing.com avec cette valeur en tant que chaîne de requête.  

   - Cliquez sur un lien hypertexte pour sélectionner une vue de ces informations spécifiques.  

   - Le volet de résultats n’affiche pas plus de 20 000 lignes. Modifiez la requête pour filtrer davantage les données, ou redémarrez CMPivot sur un regroupement plus petit.  

7. La barre d’état affiche les informations suivantes (de gauche à droite) :  

   - État de la requête actuelle pour le regroupement cible. Cet état comprend les informations suivantes :  
     - Nombre de clients actifs ayant effectué la requête (3)  
     - Nombre total de clients (5)  
     - Nombre de clients hors connexion (2)  
     - Clients ayant retourné un échec (0)  

       Exemple : `Query completed on 3 of 5 clients (2 clients offline and 0 failure)`  

   - ID de l’opération du client. Exemple : `id(16780221)`  

   - Regroupement actuel. Exemple : `PM_Team_Machines`  

   - Nombre total de lignes dans le volet de résultats. Par exemple, `1 objects`  



## <a name="example-scenarios"></a>Exemples de scénarios

Les sections suivantes fournissent des exemples d’utilisation de CMPivot dans votre environnement :


### <a name="example-1-stop-a-running-service"></a>Exemple 1 : Arrêter un service en cours d’exécution

Votre administrateur de la sécurité vous demande d’arrêter et de désactiver le service Explorateur d’ordinateurs aussi vite que possible sur tous les appareils du service de comptabilité. Vous démarrez CMPivot sur un regroupement de tous les appareils de la comptabilité, puis vous sélectionnez **Requête pour tout** sur l’entité **Service**. 

`Service`

Quand les résultats apparaissent, cliquez avec le bouton droit sur la colonne **Nom**, puis sélectionnez **Grouper par**. 

`Service | summarize dcount( Device ) by Name`

Dans la ligne du service **Explorateur**, cliquez sur le numéro contenant un lien hypertexte dans la colonne **dcount_**. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Sélectionnez plusieurs appareils, cliquez avec le bouton droit sur la sélection, puis choisissez **Exécuter le script**. Cette action entraîne le lancement de l’Assistant Exécution du script, à partir duquel vous exécutez un script existant pour arrêter et désactiver un service. Avec CMPivot, répondez rapidement à l’incident de sécurité pour tous les ordinateurs actifs, et visualisez les résultats dans l’Assistant Exécution du script. Créez ensuite une base de référence de configuration pour corriger les autres ordinateurs du regroupement, quand ils seront actifs. 

![Exemple CMPivot illustrant le service Explorateur et l’action Exécuter un script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exemple 2 : Résoudre de manière proactive les défaillances des applications  

Pour effectuer une maintenance opérationnelle proactive, exécutez CMPivot une fois par semaine sur un regroupement de serveurs que vous gérez, puis sélectionnez **Requête pour tout** sur l’entité **AppCrash**. Cliquez avec le bouton droit sur la colonne **Nom de fichier**, puis sélectionnez **Tri croissant**. Un appareil retourne sept résultats pour sqlsqm.exe avec un horodatage à 03 h 00 environ tous les jours. Sélectionnez le nom du fichier dans l’une des lignes, cliquez avec le bouton droit sur celui-ci, puis sélectionnez **Rechercher sur Bing**. En parcourant les résultats de la recherche dans le navigateur web, vous trouvez un article du Support Microsoft sur ce problème, qui contient des informations supplémentaires et une solution. 


### <a name="example-3-bios-version"></a>Exemple 3 : Version du Bios

Si vous souhaitez [atténuer les vulnérabilités d’exécution spéculative côté canal](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), l’une des exigences à suivre consiste à mettre à jour le BIOS système. Commencez par une requête pour l’entité **BIOS**. Utilisez ensuite **Grouper par** avec la propriété **Version**. Cliquez ensuite avec le bouton droit sur une valeur spécifique, par exemple « LENOVO - 1140 », puis sélectionnez **Afficher les appareils avec**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exemple 4 : Espace disque disponible

Vous devez stocker temporairement un gros fichier sur un serveur de fichiers réseau, mais vous ne savez pas quel est celui qui dispose d’une capacité suffisante. Démarrez CMPivot sur un regroupement de serveurs de fichiers, puis interrogez l’entité **Disk**. Modifiez la requête pour que CMPivot retourne rapidement une liste de serveurs actifs avec des données de stockage en temps réel :  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`


## <a name="bkmk_cmpivot"></a> CMPivot à compter de la version 1810
<!--1359068, 3607759-->

À compter de Configuration Manager version 1810, CMPivot inclut les améliorations suivantes :

- [Utilitaire CMPivot et performances](#bkmk_cmpivot-perf)
- [Fonctions scalaires](#bkmk_cmpivot-functions)  
- [Visualisations de rendu](#bkmk_cmpivot-charts)  
- [Inventaire matériel](#bkmk_cmpivot-hinv)  
- [Opérateurs scalaires](#bkmk_cmpivot-operators)  
- [Résumé de la requête](#bkmk_cmpivot-summary)  
- [Messages d’état d’audit](#cmpivot-audit-status-messages)

### <a name="bkmk_cmpivot-perf"></a> Utilitaire CMPivot et performances

- CMPivot retournera jusqu’à 100 000 cellules au lieu de 20 000 lignes.
  - Si l’entité a 5 propriétés, ce qui signifie 5 colonnes, jusqu’à 20 000 lignes s’afficheront.
  - Pour une entité avec 10 propriétés, jusqu’à 10 000 lignes s’afficheront.
  - Les données totales affichées seront inférieures ou égales à 100 000 cellules.
- Sous l’onglet Résumé de la requête, sélectionnez le nombre d’appareils en Échec ou Hors connexion, puis sélectionnez l’option permettant de **Créer un regroupement**. Cette option facilite le ciblage de ces appareils avec un déploiement de mise à jour.
- Enregistrez les requêtes **favorites** en cliquant sur l’icône représentant un dossier.
   ![Exemple d’enregistrement d’une requête favorite dans CMPivot](media/cmpivot-favorite.png)

- Les clients mis à jour vers la version 1810 retournent une sortie de moins de 80 Ko au site via un canal de communication rapide.
  - Cette modification améliore les performances d’affichage de la sortie de script ou de requête.
  - Si la sortie de script ou de requête est supérieure à 80 Ko, le client envoie les données via un message d’état.
  - Si le client n’est pas mis à jour avec la version du client 1810, il continue d’utiliser des messages d’état.

### <a name="bkmk_cmpivot-functions"></a> Fonctions scalaires
CMPivot prend en charge les fonctions scalaires suivantes :
- **ago()** : soustrait l’intervalle de temps donné de l’heure horloge UTC actuelle  
- **datetime_diff()** : calcule la différence de calendrier entre deux valeurs DateHeure  
- **now()** : retourne l’heure horloge UTC actuelle  
- **bin()** : arrondit les valeurs à l’entier inférieur multiple d’une taille de compartiment donnée  

> [!Note]  
> Les données de type datetime représentent un instant dans le temps, généralement exprimé sous forme de date et heure du jour. Les valeurs de temps sont mesurées en unités de 1 seconde. Une valeur datetime se trouve toujours dans le fuseau horaire UTC. Exprimez toujours les littéraux de date et d’heure au format ISO 8601, par exemple, `yyyy-mm-dd HH:MM:ss`  

#### <a name="examples"></a>Exemples
- `datetime(2015-12-31 23:59:59.9)` : littéral de date et d’heure spécifique   
- `now()` : heure actuelle  
- `ago(1d)` : heure actuelle moins un jour  


### <a name="bkmk_cmpivot-charts"></a> Visualisations de rendu

CMPivot intègre désormais une prise en charge de base pour l’[opérateur render](https://docs.microsoft.com/azure/kusto/query/renderoperator) de Log Analytics. Cette prise en charge englobe les types suivants :  
- **barchart** : la première colonne est l’axe X et peut être de type texte, DateHeure ou numérique. Les deuxièmes colonnes doivent être de type numeric et s’affichent sous forme de bande horizontale.  
- **columnchart** : semblable au type barchart, mais avec des bandes verticales et non horizontales.  
- **piechart** : la première colonne correspond à l’axe des couleurs, la deuxième est de type numérique.  
- **timechart** : graphique linéaire. La première colonne est l’axe X et doit être de type datetime. La deuxième colonne est l’axe Y.  

#### <a name="example-bar-chart"></a>Exemple : graphique à barres
La requête suivante affiche les dernières applications utilisées sous forme de graphique à barres :

```
CCMRecentlyUsedApplications
| summarize dcount( Device ) by ProductName
| top 10 by dcount_
| render barchart
```
![Exemple de visualisation de graphique à barres CMPivot](media/1359068-cmpivot-barchart.png)

#### <a name="example-time-chart"></a>Exemple : graphique de temps
Pour afficher des graphiques de temps, utilisez le nouvel opérateur **bin()** pour regrouper des événements dans le temps. La requête suivante montre à quels moments les appareils ont démarré au cours des sept derniers jours :

``` 
OperatingSystem 
| where LastBootUpTime <= ago(7d)
| summarize count() by bin(LastBootUpTime,1d)
| render timechart
```
![Exemple de visualisation de graphique de temps CMPivot](media/1359068-cmpivot-timechart.png)

#### <a name="example-pie-chart"></a>Exemple : graphique à secteurs
La requête suivante affiche toutes les versions du système d’exploitation dans un graphique à secteurs :

```
OperatingSystem 
| summarize count() by Caption
| render piechart
```
![Exemple de visualisation de graphique à secteurs CMPivot](media/1359068-cmpivot-piechart.png)


### <a name="bkmk_cmpivot-hinv"></a> Inventaire matériel
Utilisez CMPivot pour interroger une classe d’inventaire matériel. Ces classes incluent les extensions personnalisées que vous créez pour l’inventaire matériel. CMPivot retourne immédiatement les résultats mis en cache de la dernière analyse d’inventaire matériel stockée dans la base de données de site. Dans le même temps, il met à jour les résultats avec les données actives des clients en ligne, si nécessaire.

La saturation de la couleur des données dans la table de résultats ou le graphique indique si les données sont actives ou mises en cache. Par exemple, le bleu foncé représente les données en temps d’un client en ligne. Le bleu clair correspond aux données mises en cache.

#### <a name="example"></a>Exemple
```
LogicalDisk
| summarize sum( FreeSpace ) by Device
| order by sum_ desc
| render columnchart
```
![Exemple de requête d’inventaire CMPivot avec visualisation d’histogramme](media/1359068-cmpivot-inventory.png)

#### <a name="limitations"></a>Limitations
- Les entités d’inventaire matériel suivantes ne sont pas prises en charge :  
    - Propriétés de tableau, par exemple l’adresse IP  
    - Real32/Real64 <!--example?-->  
    - Propriétés d’objet incorporé <!--example?-->  
- Les noms d’entités d’inventaire doivent commencer par un caractère
- Vous ne pouvez pas remplacer les entités intégrées en créant une entité d’inventaire de même nom  


### <a name="bkmk_cmpivot-operators"></a> Opérateurs scalaires
CMPivot comprend les opérateurs scalaires suivants :  

> [!Note]  
> - LHS : chaîne située à gauche de l’opérateur  
> - RHS : chaîne située à droite de l’opérateur  


|Opérateur|Description|Exemple (donne true)|
|--------|-----------|---------------------|
|==|Égal à|`"aBc" == "aBc"`|
|!=|Différent de|`"abc" != "ABC"`|
|like|LHS contient une correspondance pour RHS|`"FabriKam" like "%Brik%"`|
|!like|LHS ne contient pas de correspondance pour RHS|`"Fabrikam" !like "%xyz%"`|
|contient|RHS apparaît comme une sous-séquence de LHS|`"FabriKam" contains "BRik"`|
|!contains|RHS ne figure pas dans LHS|`"Fabrikam" !contains "xyz"`|
|startswith|RHS est une sous-séquence initiale de LHS|`"Fabrikam" startswith "fab"`|
|!startswith|RHS n’est pas une sous-séquence initiale de LHS|`"Fabrikam" !startswith "kam"`|
|endswith|RHS est une sous-séquence fermante de LHS|`"Fabrikam" endswith "Kam"`|
|!endswith|RHS n’est pas une sous-séquence fermante de LHS|`"Fabrikam" !endswith "brik"`|


### <a name="bkmk_cmpivot-summary"></a> Résumé de la requête

Sélectionnez l’onglet **Résumé de la requête** au bas de la fenêtre CMPivot. Cet état vous permet d’identifier les clients qui se trouvent en mode hors connexion ou de résoudre les erreurs qui peuvent se produire. Sélectionnez une valeur dans la colonne Nombre pour ouvrir la liste des appareils présentant cet état. 

Par exemple, sélectionnez le nombre d’appareils présentant l’état Échec. Consultez le message d’erreur associé et exportez une liste de ces appareils. Si l’erreur est liée à la non-reconnaissance d’une applet de commande spécifique, créez un regroupement à partir de la liste d’appareils exportée pour déployer une mise à jour Windows PowerShell.  

### <a name="cmpivot-audit-status-messages"></a>Messages d’état d’audit CMPivot

À compter de la version 1810, quand vous exécutez CMPivot, un message d’état d’audit est créé avec l’**ID de message 40805**. Vous pouvez voir les messages d’état en accédant à **Supervision** < **État du système** < **Requêtes sur les messages d’état**. Vous pouvez exécuter **Tous les messages d’état de l’audit pour un utilisateur spécifique** , **Tous les messages d’état de l’audit pour un site spécifique** ou créer votre propre requête de message d’état.

Le format suivant est utilisé pour le message :

MessageId 40805 : L’utilisateur &lt;Nom_utilisateur> a exécuté le script &lt;Guid_script> avec le hachage &lt;Hachage_script> sur le regroupement &lt;ID_collection>.

- 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 est la valeur Guid_script pour CMPivot.
- La valeur Hachage_script est indiquée dans le fichier scripts.log du client.
- Vous pouvez également voir le hachage stocké dans le score de script du client. Le nom de fichier sur le client est &lt;Guid_script>_&lt;Hachage_script>.
    - Exemple de nom de fichier : C:\Windows\CCM\ScriptStore\7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14_abc1d23e45678901fabc123d456ce789fa1b2cd3e456789123fab4c56789d0123.ps
   

![Exemple de messages d’état d’audit CMPivot](media/cmpivot-audit-status-message.png)

## <a name="bkmk_cmpivot1902"></a> CMPivot à compter de la version 1902
<!--3610960-->
À compter de Configuration Manager version 1902, vous pouvez exécuter CMPivot à partir du site d’administration centrale (CAS) dans une hiérarchie. Le site principal gère néanmoins toujours la communication avec le client. Lors de l’exécution de CMPivot à partir du site d’administration centrale, il communique avec le site principal via le canal d’abonnement aux messages à haut débit. Cette communication ne repose pas sur la réplication SQL standard entre les sites.

L’exécution de CMPivot sur le site d’administration centrale nécessite des autorisations supplémentaires quand SQL ou le fournisseur ne se trouvent pas sur le même ordinateur ou dans le cas d’une configuration SQL Always On. Avec ces configurations à distance, vous avez un « scénario de double tronçon » pour CMPivot.

Pour obtenir CMPivot afin de travailler sur le site d’administration centrale dans un tel « scénario de double tronçon », vous pouvez définir une délégation contrainte. Pour comprendre les implications de cette configuration au niveau de la sécurité, consultez l’article [Délégation Kerberos contrainte](https://docs.microsoft.com/windows-server/security/kerberos/kerberos-constrained-delegation-overview). Si vous avez plusieurs configurations à distance, comme SQL ou le fournisseur SCCM, colocalisées ou non, avec le site d’administration centrale, vous pouvez avoir besoin d’une combinaison de paramètres d’autorisation. Voici les étapes que vous devez effectuer :

### <a name="cas-has-a-remote-sql-server"></a>Le site d’administration centrale a un serveur SQL Server distant

1. Accédez à l’instance SQL Server de chaque site principal.
   1. Ajoutez le serveur SQL distant du site d’administration centrale et le serveur du site d’administration centrale au groupe [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
   ![Groupe Configmgr_DviewAccess sur l’instance SQL Server d’un site principal](media/cmpivot-dviewaccess-group.png)
1. Accédez à Utilisateurs et ordinateurs Active Directory.
   1. Pour chaque serveur de site principal, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.
      1. Sous l’onglet Délégation, choisissez la troisième option, **N’approuver cet ordinateur que pour la délégation aux services spécifiés**. 
      1. Choisissez **Utiliser uniquement Kerberos**.
      1. Ajoutez le service SQL Server du site d’administration centrale avec le port et l’instance.
      1. Vérifiez que ces modifications sont conformes à la stratégie de sécurité de votre entreprise.
   1. Pour le site d’administration centrale, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.
      1. Sous l’onglet Délégation, choisissez la troisième option, **N’approuver cet ordinateur que pour la délégation aux services spécifiés**. 
      1. Choisissez **Utiliser uniquement Kerberos**.
      1. Ajoutez le service SQL Server de chaque site principal avec le port et l’instance.
      1. Vérifiez que ces modifications sont conformes à la stratégie de sécurité de votre entreprise.

   ![Exemple de délégation AD CMPivot pour les doubles tronçons](media/cmpivot-ad-delegation.png)

### <a name="cas-has-a-remote-provider"></a>Le site d’administration centrale a un fournisseur distant

1. Accédez à l’instance SQL Server de chaque site principal.
   1. Ajoutez le compte d’ordinateur de fournisseur du site d’administration centrale et le serveur du site d’administration centrale au groupe [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
1. Accédez à Utilisateurs et ordinateurs Active Directory.
   1. Sélectionnez l’ordinateur de fournisseur du site d’administration centrale, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.
      1. Sous l’onglet Délégation, choisissez la troisième option, **N’approuver cet ordinateur que pour la délégation aux services spécifiés**. 
      1. Choisissez **Utiliser uniquement Kerberos**.
      1. Ajoutez le service SQL Server de chaque site principal avec le port et l’instance.
      1. Vérifiez que ces modifications sont conformes à la stratégie de sécurité de votre entreprise.
   1. Sélectionnez le serveur du site d’administration centrale, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.
      1. Sous l’onglet Délégation, choisissez la troisième option, **N’approuver cet ordinateur que pour la délégation aux services spécifiés**. 
      1. Choisissez **Utiliser uniquement Kerberos**.
      1. Ajoutez le service SQL Server de chaque site principal avec le port et l’instance.
      1. Vérifiez que ces modifications sont conformes à la stratégie de sécurité de votre entreprise.
1. Redémarrez l’ordinateur de fournisseur distant du site d’administration centrale.

### <a name="sql-always-on"></a>SQL Always On

1. Accédez à l’instance SQL Server de chaque site principal.
   1. Ajoutez le serveur du site d’administration centrale au groupe [Configmgr_DviewAccess](/sccm/core/plan-design/hierarchy/accounts#configmgr_dviewaccess).
1. Accédez à Utilisateurs et ordinateurs Active Directory.
   1. Pour chaque serveur de site principal, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.
      1. Sous l’onglet Délégation, choisissez la troisième option, **N’approuver cet ordinateur que pour la délégation aux services spécifiés**. 
      1. Choisissez **Utiliser uniquement Kerberos**.
      1. Ajoutez les comptes de service SQL Server du site d’administration centrale pour les nœuds SQL avec le port et l’instance.
      1. Vérifiez que ces modifications sont conformes à la stratégie de sécurité de votre entreprise.
   1. Sélectionnez le serveur du site d’administration centrale, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.
      1. Sous l’onglet Délégation, choisissez la troisième option, **N’approuver cet ordinateur que pour la délégation aux services spécifiés**. 
      1. Choisissez **Utiliser uniquement Kerberos**.
      1. Ajoutez le service SQL Server de chaque site principal avec le port et l’instance.
      1. Vérifiez que ces modifications sont conformes à la stratégie de sécurité de votre entreprise.
1. Vérifiez que le [nom de principal du service (SPN) est publié](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/listeners-client-connectivity-application-failover?view=sql-server-2017#SPNs) pour le nom d’écouteur SQL du site d’administration centrale et le nom d’écouteur SQL de chaque site principal.
1. Redémarrez les serveurs SQL principaux.
1. Redémarrez le serveur du site d’administration centrale et les serveurs SQL du site d’administration centrale.


## <a name="inside-cmpivot"></a>À l’intérieur de CMPivot

CMPivot envoie des requêtes aux clients à l’aide du « canal rapide » de Configuration Manager. Ce canal de communication entre le serveur et le client est également utilisé par d’autres fonctionnalités telles que les actions de notification du client, l’état du client et Endpoint Protection. Les clients retournent les résultats via un système similaire rapide, les messages d’état. Les messages d’état sont temporairement stockés dans la base de données. Pour plus d’informations sur les ports utilisés pour la notification du client, consultez l’article [Ports](/sccm/core/plan-design/hierarchy/ports#BKMK_PortsClient-MP).

Les requêtes et les résultats ne sont que du texte. Les entités **InstallSoftware** et **Process** retournent certains des jeux de résultats les plus importants. Durant le test de performance, la plus grande taille de fichier de message d’état d’un client pour ces requêtes était inférieure à **1 Ko**. Mise à l’échelle dans un grand environnement comportant 50 000 clients actifs, cette requête à usage unique génère moins de 50 Mo de données sur le réseau. Tous les éléments de la page d’accueil qui sont soulignés retourneront moins de 1 Ko d’informations par client.

![Exemple d’entités CMPivot soulignées](media/cmpivot-underlined-entities.png)

À compter de Configuration Manager 1810, CMPivot peut interroger les données d’inventaire matériel, dont les classes d’inventaire matériel étendues. Ces nouvelles entités (celles non soulignées dans la page d’accueil) peuvent retourner des jeux de données beaucoup plus volumineux, en fonction de la quantité de données définie pour une propriété d’inventaire matériel donnée. Par exemple, l’entité « InstalledExecutable » peut retourner plusieurs Mo de données par client, en fonction des données spécifiques que vous interrogez. Soyez attentif aux performances et à la scalabilité sur vos systèmes lors du retour de jeux de données d’inventaire matériel plus volumineux à partir de regroupements plus grands à l’aide de CMPivot.

Une requête expire après une heure. Par exemple, un regroupement contient 500 appareils, et 450 des clients sont en ligne. Ces appareils actifs reçoivent la requête et retournent les résultats quasiment immédiatement. Si vous laissez la fenêtre de CMPivot ouverte, quand les 50 autres clients sont en ligne, ils reçoivent également la requête et retournent les résultats. 

## <a name="log-files"></a>Fichiers journaux

 Les interactions CMPivot sont journalisées dans les fichiers journaux suivants :

**Côté serveur :**
- SmsProv.log
- BgbServer.log
- StateSys.log

**Côté client :**
 - CCMNotificationAgent.log
 - Scripts.log
 - StateMessage.log

Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files) et [Résolution des problèmes liés à CMPivot](/sccm/core/servers/manage/cmpivot-tsg.md).

## <a name="next-steps"></a>Étapes suivantes
 
[Résolution des problèmes liés à CMPivot](/sccm/core/servers/manage/cmpivot-tsg.md)

[Créer et exécuter des scripts PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)


