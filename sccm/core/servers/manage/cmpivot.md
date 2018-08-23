---
title: CMPivot pour les données en temps réel
titleSuffix: Configuration Manager
description: Découvrez comment utiliser CMPivot dans Configuration Manager pour interroger les clients en temps réel.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 32e2d6b9-148f-45e2-8083-98c656473f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0766bc765712fc493f01eb5aa807426ec44fa5d7
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385940"
---
# <a name="cmpivot-for-real-time-data-in-configuration-manager"></a>CMPivot pour les données en temps réel dans Configuration Manager

<!--1358456-->

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager met à disposition un grand magasin de données d’appareils centralisé, que les clients utilisent pour générer des rapports. Le site collecte généralement ces données chaque semaine. Depuis la version 1806, CMPivot est un nouvel utilitaire de console, qui permet désormais d’accéder à l’état en temps réel des appareils de votre environnement. Il exécute immédiatement une requête sur tous les appareils actuellement connectés du regroupement cible, et retourne les résultats. Filtrez et regroupez ensuite ces données dans l’outil. En fournissant les données en temps réel des clients en ligne, vous pouvez répondre plus rapidement aux questions métier, résoudre les problèmes et corriger les incidents de sécurité.

Par exemple, si vous souhaitez [limiter les vulnérabilités d’exécution spéculative côté canal](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), l’une des exigences est de mettre à jour le BIOS système. Vous pouvez utiliser CMPivot pour interroger rapidement les informations relatives au BIOS système, et rechercher les clients non conformes.



## <a name="prerequisites"></a>Prérequis

Les composants suivants sont obligatoires pour l’utilisation de CMPivot :

- Mettez à niveau les appareils cibles vers la dernière version du client Configuration Manager.  

- L’administrateur Configuration Manager doit disposer de l’autorisation **Lecture** sur l’objet **Scripts SMS** et de l’autorisation **Exécuter les scripts** sur l’objet **Regroupement**. Le rôle d’**exécuteur de scripts** dispose de ces autorisations. Pour plus d’informations, consultez [Créer des rôles de sécurité pour les scripts](/sccm/apps/deploy-use/create-deploy-scripts#bkmk_ScriptRoles).  

- Pour collecter des données pour les entités suivantes, les clients cibles nécessitent PowerShell version 5.0 :  
    - Administrateurs
    - Connexion
    - IPConfig
    - SMBConfig 



## <a name="limitations"></a>Limitations

- Dans une hiérarchie, connectez la console Configuration Manager à un *site principal* pour exécuter CMPivot. L’action **Démarrer CMPivot** n’apparaît pas dans la console quand elle est connectée à un site d’administration centrale.  

- CMPivot ne retourne que les données des clients connectés au site actuel.  

- Si un regroupement contient des appareils d’un autre site, les résultats de CMPivot concernent uniquement les appareils du site actuel.  

- Vous ne pouvez pas personnaliser les propriétés des entités, les colonnes des résultats ou les actions des appareils.  

- Vous pouvez uniquement exécuter une seule instance à la fois de CMPivot sur un ordinateur qui dispose de la console Configuration Manager.  



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

     - Les liens concernant les **opérateurs de table**, les **fonctions d’agrégation** et les **fonctions scalaires** ouvrent une documentation de référence de langage dans le navigateur web. CMPivot utilise le même langage de requête que [Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).  

3. Gardez la fenêtre CMPivot ouverte pour voir les résultats des clients. Quand vous fermez la fenêtre CMPivot, la session s’achève.  

    > [!Note]  
    > Si la requête a été envoyée, les clients continuent d’adresser une réponse au message d’état à destination du serveur.  



## <a name="how-to-use-cmpivot"></a>Guide pratique pour utiliser CMPivot

![Exemple de fenêtre CMPivot](media/1358456-cmpivot-sample.png)

La fenêtre CMPivot contient les éléments suivants :  

1. Le regroupement ciblé par CMPivot est indiqué dans la barre de titre en haut de la fenêtre, ainsi que dans la barre d’état en bas de la fenêtre. Par exemple, **Tous les systèmes** dans la capture d’écran ci-dessus.  

2. Le volet de gauche liste les **entités** disponibles sur les clients. Certaines entités dépendent de WMI, tandis que d’autres utilisent PowerShell pour obtenir les données auprès des clients.   

    - Cliquez avec le bouton droit sur une entité pour les actions suivantes :  

       - **Insérer** : permet d’ajouter l’entité à la requête à la position actuelle du curseur. La requête ne s’exécute pas automatiquement. Il s’agit de l’action par défaut quand vous double-cliquez sur une entité. Utilisez cette action quand vous créez une requête.  

       - **Requête pour tout** : permet d’exécuter une requête pour cette entité, en incluant toutes les propriétés. Utilisez cette action pour interroger rapidement une seule entité.  

       - **Requête par appareil** : permet d’exécuter une requête pour cette entité, et de regrouper les résultats. Par exemple, `Disk | summarize dcount( Device ) by Name`  

    - Développez une entité pour voir les propriétés spécifiques disponibles pour chaque entité. Double-cliquez sur une propriété pour l’ajouter à la requête, à la position actuelle du curseur.  

3. L’onglet **Accueil** affiche des informations générales sur CMPivot, notamment des liens vers des exemples de requêtes et de la documentation d’aide.  

4. L’onglet **Requête** affiche le volet de requête, le volet de résultats et la barre d’état. L’onglet Requête est sélectionné dans l’exemple de capture d’écran ci-dessus.  

5. Le volet de requête est l’emplacement où vous créez ou tapez une requête à exécuter sur les clients du regroupement.  

    - CMPivot utilise un sous-ensemble du même langage de requête qu’[Azure Log Analytics](https://docs.loganalytics.io/docs/Language-Reference/Change-log).  

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

       - **Ajouter un tableau croisé dynamique à** : permet d’interroger une autre entité sur cet appareil.  

       - **Exécuter le script** : permet de lancer l’Assistant Exécuter le script pour exécuter un script PowerShell existant sur cet appareil. Pour plus d’informations, consultez [Exécuter un script](/sccm/apps/deploy-use/create-deploy-scripts#run-a-script).  

       - **Contrôle à distance** : permet de lancer une session de contrôle à distance Configuration Manager sur cet appareil. Pour plus d’informations, consultez [Guide pratique pour administrer à distance un ordinateur client Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).  

       - **Explorateur de ressources** : permet de lancer l’Explorateur de ressources Configuration Manager pour cet appareil. Pour plus d’informations, consultez [Afficher l’inventaire matériel](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory) ou [Afficher l’inventaire logiciel](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

    - Cliquez avec le bouton droit sur une cellule qui ne contient pas d’appareil pour effectuer les actions supplémentaires suivantes :  

       - **Copier** : permet de copier le texte de la cellule dans le Presse-papiers.  

       - **Afficher les appareils avec** : permet d’interroger les appareils ayant cette valeur de propriété. Par exemple, à partir des résultats de la requête `OS`, sélectionnez cette option sur une cellule de la ligne Version : `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ > 0)`  

       - **Afficher les appareils sans** : permet d’interroger les appareils n’ayant pas cette valeur de propriété. Par exemple, à partir des résultats de la requête `OS`, sélectionnez cette option sur une cellule de la ligne Version : `OS | summarize countif( (Version == '10.0.17134') ) by Device | where (countif_ == 0) | project Device`  

       - **Rechercher sur Bing** : permet de lancer le navigateur web par défaut sur www.bing.com avec cette valeur en tant que chaîne de requête.  

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


### <a name="example-1-stop-a-running-service"></a>Exemple 1 : Arrêter un service en cours d’exécution

Votre administrateur de la sécurité vous demande d’arrêter et de désactiver le service Explorateur d’ordinateurs aussi vite que possible sur tous les appareils du service de comptabilité. Vous démarrez CMPivot sur un regroupement de tous les appareils de la comptabilité, puis vous sélectionnez **Requête pour tout** sur l’entité **Service**. 

`Service`

Quand les résultats apparaissent, cliquez avec le bouton droit sur la colonne **Nom**, puis sélectionnez **Grouper par**. 

`Service | summarize dcount( Device ) by Name`

Dans la ligne du service **Explorateur**, cliquez sur le numéro contenant un lien hypertexte dans la colonne **dcount_**. 

`Service | where (Name == 'Browser') | summarize count() by Device`

Sélectionnez plusieurs appareils, cliquez avec le bouton droit sur la sélection, puis choisissez **Exécuter le script**. Cette action entraîne le lancement de l’Assistant Exécution du script, à partir duquel vous exécutez un script existant pour arrêter et désactiver un service. Avec CMPivot, répondez rapidement à l’incident de sécurité pour tous les ordinateurs actifs, et visualisez les résultats dans l’Assistant Exécution du script. Créez ensuite une base de référence de configuration pour corriger les autres ordinateurs du regroupement, quand ils seront actifs. 

![Exemple CMPivot illustrant le service Explorateur et l’action Exécuter un script](media/cmpivot-example1.png)


### <a name="example-2-proactively-resolve-application-failures"></a>Exemple 2 : Résoudre de manière proactive les défaillances des applications  

Pour effectuer une maintenance opérationnelle proactive, exécutez CMPivot une fois par semaine sur un regroupement de serveurs que vous gérez, puis sélectionnez **Requête pour tout** sur l’entité **AppCrash**. Cliquez avec le bouton droit sur la colonne **Nom de fichier**, puis sélectionnez **Tri croissant**. Un appareil retourne sept résultats pour sqlsqm.exe avec un horodatage à 03 h 00 environ tous les jours. Sélectionnez le nom du fichier dans l’une des lignes, cliquez avec le bouton droit sur celui-ci, puis sélectionnez **Rechercher sur Bing**. En parcourant les résultats de la recherche dans le navigateur web, vous trouvez un article du Support Microsoft sur ce problème, qui contient des informations supplémentaires et une solution. 


### <a name="example-3-bios-version"></a>Exemple 3 : Version du BIOS

Si vous souhaitez [atténuer les vulnérabilités d’exécution spéculative côté canal](https://blogs.technet.microsoft.com/configurationmgr/2018/01/08/additional-guidance-to-mitigate-speculative-execution-side-channel-vulnerabilities/), l’une des exigences à suivre consiste à mettre à jour le BIOS système. Commencez par une requête pour l’entité **BIOS**. Utilisez ensuite **Grouper par** avec la propriété **Version**. Cliquez ensuite avec le bouton droit sur une valeur spécifique, par exemple « LENOVO - 1140 », puis sélectionnez **Afficher les appareils avec**.  

`Bios | summarize countif( (Version == 'LENOVO - 1140') ) by Device | where (countif_ > 0)`


### <a name="example-4-free-disk-space"></a>Exemple 4 : Espace disque libre

Vous devez stocker temporairement un gros fichier sur un serveur de fichiers réseau, mais vous ne savez pas quel est celui qui dispose d’une capacité suffisante. Démarrez CMPivot sur un regroupement de serveurs de fichiers, puis interrogez l’entité **Disk**. Modifiez la requête pour que CMPivot retourne rapidement une liste de serveurs actifs avec des données de stockage en temps réel :  

`Disk | where (Description == 'Local Fixed Disk') | where isnotnull( FreeSpace ) | order by FreeSpace asc`



## <a name="inside-cmpivot"></a>À l’intérieur de CMPivot

CMPivot envoie des requêtes aux clients à l’aide du « canal rapide » de Configuration Manager. Ce canal de communication entre le serveur et le client est également utilisé par d’autres fonctionnalités telles que les actions de notification du client, l’état du client et Endpoint Protection. Les clients retournent les résultats via un système similaire rapide, les messages d’état. Les messages d’état sont temporairement stockés dans la base de données. 

Les requêtes et les résultats ne sont que du texte. Les entités **InstallSoftware** et **Process** retournent certains des jeux de résultats les plus importants. Durant le test de performance, la plus grande taille de fichier de message d’état d’un client pour ces requêtes était inférieure à **1 Ko**. Mise à l’échelle dans un grand environnement comportant 50 000 clients actifs, cette requête à usage unique génère moins de 50 Mo de données sur le réseau.  

Une requête expire après une heure. Par exemple, un regroupement contient 500 appareils, et 450 des clients sont en ligne. Ces appareils actifs reçoivent la requête et retournent les résultats quasiment immédiatement. Si vous laissez la fenêtre de CMPivot ouverte, quand les 50 autres clients sont en ligne, ils reçoivent également la requête et retournent les résultats. 



## <a name="see-also"></a>Voir aussi
[Créer et exécuter des scripts PowerShell](/sccm/apps/deploy-use/create-deploy-scripts)
