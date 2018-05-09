---
title: Importer des données dans Microsoft Intune
titleSuffix: Configuration Manager
description: Importer des données Configuration Manager dans Microsoft Intune
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: b552391d-abc0-48a2-a429-93605a13a66a
ms.openlocfilehash: dcd84e484f55cb799953bea83be917055ca1292a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="import-configuration-manager-data-to-microsoft-intune"></a>Importer des données Configuration Manager dans Microsoft Intune 

*S’applique à : System Center Configuration Manager (Current Branch)*    

La première phase recommandée du processus de [migration des appareils et des utilisateurs MDM hybrides vers la version autonome d’Intune](migrate-hybridmdm-to-intunesa.md) dans la configuration cloud seul consiste à utiliser l’outil d’importation de données Intune. Si vous le souhaitez, vous pouvez ignorer cette phase et passer à la phase de [préparation d’Intune à la migration des utilisateurs](migrate-prepare-intune.md). Cependant, cet outil exécute les fonctions suivantes qui peuvent vous permettre d’économiser beaucoup de temps dans la phase suivante : 
1.  Il collecte des données sur les objets que vous sélectionnez à partir de votre hiérarchie Configuration Manager. 
2.  Il fournit des détails sur les objets que vous pouvez sélectionner pour l’importation et des informations sur les raisons pour lesquelles certains objets ne peuvent pas être importés.
3.  Il importe les objets sélectionnés dans votre locataire Microsoft Intune. 

L’outil d’importation de données ne change votre environnement Configuration Manager en aucune façon, et par conséquent, vous pouvez importer des objets dans Intune et vérifier que tout fonctionne comme prévu, sans risque de laisser vos appareils MDM hybrides dans un état non géré. 

## <a name="what-objects-can-this-tool-import"></a>Quels objets cet outil peut-il importer ?
L’outil d’importation peut collecter des informations sur les types d’objets suivants dans Configuration Manager et fournir des informations sur la possibilité ou non d’importer les objets collectés : 
- Éléments de configuration
- Profils de certificat
- Profils de messagerie
- Profils VPN
- Profils Wi-Fi
- Stratégies de conformité
- Applications
- Déploiements

> [!Note]    
> L’importation de déploiements ne s’avère utile que pour les autres types d’objets que vous importez. Par exemple, si vous importez des profils VPN et des déploiements, vous ne pouvez importer que les déploiements des profils VPN que vous sélectionnez. Les déploiements dans Intune sont appelés attributions. Si vous souhaitez importer un déploiement pour un objet précédemment importé, vous devez réimporter cet objet ou créer manuellement l’affectation dans Intune sur Azure. Par exemple, si vous importez des profils VPN et non des déploiements, vous devez réexécuter l’outil et sélectionner les profils VPN et les déploiements ou créer manuellement l’affectation dans Intune sur Azure.  Si vous réexécutez l’outil, des objets en double risquent d’être créés, mais vous pouvez les supprimer ultérieurement dans Intune sur Azure.  

> [!Important]    
> Si le regroupement d’un déploiement se base sur un groupe Active Directory qui a été répliqué sur Azure Active Directory (AAD), l’outil cible automatiquement les objets qui ont migré vers les groupes si vous sélectionnez le déploiement approprié lors de l’exécution de l’outil. Quand vous avez des regroupements plus complexes ou des regroupements de membres directs, vous devez les recréer manuellement dans AAD et cibler manuellement les affectations d’objets sur eux dans Intune sur Azure.


## <a name="things-to-know-before-you-run-the-tool"></a>Éléments à connaître avant d’exécuter l’outil
- L’exécution de l’outil ne change votre environnement Configuration Manager en aucune façon.
- Nous vous recommandons de commencer par tester le processus d’importation de données à l’aide d’un locataire d’essai. Ensuite, après avoir vérifié que les données attendues ont été importées, vous pouvez reproduire le même processus avec votre locataire Intune de production.
- L’outil d’importation de données est conçu pour importer uniquement les données Configuration Manager une seule fois. Il n’effectue pas de suivi des objets dans Configuration Manager ou Intune. Toutefois, si vous le réexécutez sur le même ordinateur que précédemment, il vous indique quels objets vous avez déjà importés. L’outil ne sait pas si un objet existe toujours dans Intune ou s’il a changé. Si vous importez plusieurs fois des données dans Intune, vous risquez d’avoir des objets en double.
- Tous les paramètres de profil ne peuvent pas être importés. Par exemple, vous ne pouvez pas importer des paramètres de mode plein écran ou PFX. 
- Si vous avez une stratégie Configuration Manager avec des paramètres qui ne sont pas applicables aux plateformes sélectionnées, l’outil peut ignorer ces paramètres lors de l’importation. Le fait d’ignorer les paramètres permet de veiller à ce que la stratégie puisse être importée et prise en charge par Intune. 
- L’outil tente de vous donner la raison pour laquelle un objet ne peut pas être importé. Dans certains cas, avant d’importer des objets dans Intune, vous pouvez revenir à la console Configuration Manager, corriger le problème, redémarrer la détection des objets Configuration Manager, puis importer les objets. Parfois, vous avez besoin de recréer ces objets manuellement dans Intune.
- Il existe des profils qui dépendent d’autres objets. Si vous souhaitez importer un profil qui dépend d’un autre objet, comme un profil d’e-mail qui dépend d’un certificat, vous devez importer les deux objets en même temps, sauf si vous avez précédemment importé l’autre objet à partir du même ordinateur avec le même utilisateur.  
- Après avoir exécuté l’outil, vous pouvez avoir besoin d’effectuer des étapes manuelles supplémentaires. Par exemple, cibler des applications et des stratégies sur des groupes AAD. 

## <a name="prerequisites"></a>Prérequis
- Configuration Manager version 1610 ou ultérieure. Nous vous recommandons de spécifier le site de niveau supérieur et d’exécuter l’outil avec un utilisateur qui a accès à tous les objets dans la hiérarchie du site. L’outil découvre uniquement les objets accessibles par l’utilisateur qui exécute l’outil. 
- Un administrateur général doit exécuter l’outil d’importation de données la première fois à l’aide du paramètre ***intunedataimporter.exe - GlobalConsent*** suivant. Ensuite, un administrateur général ou un administrateur Intune peut exécuter l’outil.  


<!-- ## Objects that cannot be imported
There are some Configuration Manager objects that the importer tool cannot import to Intune. You must manually create these objects in Intune. 
- Collections based on direct membership or that are based on a query. The only collections that are imported are based on a single AD group. For all other collections, you must create the assignment in Intune and add the assignment to the appropriate objects. 
- Profiles <list what we cannot import>
- Policies <??>
- Etc.
-->

## <a name="download-the-data-importer-tool"></a>Télécharger l’outil d’importation de données
L’outil d’importation de données est disponible en téléchargement à partir du dépôt ConfigMgrTools/Intune-Data-Importer dans GitHub. Utilisez la procédure suivante pour télécharger l’outil.

1. Accédez à la page [des versions GitHub Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer/releases).
2. Pour obtenir la dernière version, cliquez sur **Microsoft.Intune.Data.Importer.exe**.
3. Enregistrez et exécutez (ou exécutez seulement) le fichier .exe, puis choisissez un dossier de destination dans lequel extraire l’outil Intune Data Importer.

## <a name="run-the-data-importer-tool"></a>Exécuter l’outil d’importation de données
L’Assistant de l’outil d’importation de données peut se diviser en trois étapes principales. Cette section fournit des informations pour vous aider à accomplir chaque section de l’Assistant et à importer correctement des données Configuration Manager dans Intune. Chaque étape continue là où l’étape précédente s’est terminée.

### <a name="provide-permission-for-the-data-importer-tool-to-access-resources"></a>Autoriser l’outil d’importation de données à accéder aux ressources
Avant de pouvoir exécuter l’outil d’importation de données, vous devez utiliser un compte d’administrateur général pour autoriser l’outil à accéder aux ressources dans Azure. Ensuite, vous pouvez exécuter l’outil à l’aide d’un compte d’administrateur général ou d’administrateur Intune.   

1.  Un administrateur général doit exécuter l’outil la première fois à l’aide du paramètre suivant : ***intunedataimporter.exe - GlobalConsent*** 
2. Lorsque l’outil démarre, un écran de connexion s’affiche vous invitant à vous connecter en utilisant un compte doté du rôle Administrateur général dans Azure. 
3. Cliquez sur **Accepter** pour créer une application dans Azure avec des droits appropriés dans Microsoft Graph. L’outil d’importation de données a besoin de ces droits pour importer des objets dans Microsoft Intune.   

   > [!Important]
   > Lorsque vous cliquez sur **Accepter**, vous donnez l’autorisation à l’outil d’effectuer les opérations suivantes :
   > - Lire tous les groupes
   > - Se connecter et lire le profil utilisateur
   > - Lire et écrire la configuration et les stratégies des appareils Intune
   > - Lire et écrire des applications Intune
   > - Lire et écrire des stratégies de contrôle d’administration basée sur des rôles Intune
   > - Lire et écrire sur des appareils Intune
   > - Lire et écrire une configuration Intune
1. Après avoir donné le consentement, n’importe quel autre administrateur général ou administrateur Intune peut exécuter l’outil pour importer des données de Configuration Manager dans Intune sur Azure.    
        
    > [!Note]
    > Si le consentement n’a pas été donné en premier lieu par un administrateur général, l’outil peut afficher **Vous ne pouvez pas accéder à cette application** quand un administrateur Intune l’exécute et se connecte à l’abonnement Intune.

### <a name="manually-map-collections-to-azure-ad-groups"></a>Mapper manuellement des collections à des groupes Azure AD
Lorsque vous exécutez l’outil Data Importer, celui-ci extrait le nom du groupe AD à partir des collections avec une règle unique qui cible un groupe AD unique. Lorsque les affectations sont créées dans Intune, Data Importer recherche un groupe Azure AD avec le même nom que le groupe AD et, le cas échéant, affecte l’objet importé à ce groupe Azure AD. Vous pouvez remplacer le nom du groupe AD trouvé par Data Importer pour une collection et fournir un ou plusieurs groupes Azure AD à utiliser pour cette collection. Le fait d’utiliser le fichier de mappage de collection vous permet de mapper des collections en général non importables avec Data Importer à des groupes Azure AD.
#### <a name="find-the-collections-that-cannot-be-imported"></a>Rechercher les collections qui ne peuvent pas être importées
Vous pouvez obtenir la liste de toutes les collections qui ne peuvent pas être importées afin de les ajouter à votre fichier .csv de mappage de collection. 
1. Exécutez l’outil Data Importer et sélectionnez les objets à importer. Utilisez les procédures décrites dans [Phase 1 : Découvrir les objets Configuration Manager et collecter les données](#phase-1:-discover-configuration-manager-objects-and-collect-data) et [Phase 2 : Résoudre les problèmes et sélectionner les objets à importer](#phase-2:-resolve-issues-and-select-the-objects-to-import) pour découvrir et choisir les objets. Puis, sur la page **Résumé**, choisissez **Exporter les détails** pour créer un fichier .csv contenant les détails de tous les éléments sélectionnés pour l’importation, notamment les objets qui ne peuvent pas être importés et les déploiements. 
2. Ouvrez le fichier .csv dans Microsoft Excel et filtrez les données sur le **Déploiement** pour la colonne **Type** et **Non** pour la colonne **Importable**. La colonne du nom de la collection répertorie toutes les collections qui doivent être ajoutées à un fichier de mappage de collection afin que ces déploiements puissent être importés.

#### <a name="create-the-collection-mapping-file"></a>Créer le fichier de mappage de collection
Le fichier de mappage de collection est un fichier CSV (valeurs séparées par des virgules) dans lequel la première colonne est la colonne du nom de la collection Configuration Manager et la deuxième colonne est le nom du groupe Azure AD à utiliser pour cette collection. Pour indiquer plusieurs groupes Azure AD pour une seule collection Configuration Manager, créez plusieurs lignes dans le fichier CSV avec le nom de cette collection. L’exemple suivant illustre un fichier CSV contenant deux collections. La première collection est mappée à un seul groupe Azure AD et la deuxième collection est mappée à deux groupes Azure AD.

![Exemple de fichier CSV de mappage de collection](..\media\migrate-collectionmapping.png)

#### <a name="start-the-data-importer-tool-using-collection-mapping"></a>Démarrer l’outil Data Importer à l’aide du mappage de collection
Pour utiliser un fichier de mappage de collection, vous devez démarrer l’outil Data Importer à l’aide du paramètre de ligne de commande *-CollectionMappingFile* et du chemin d’accès complet au fichier .csv de mappage de collection que vous créez. Par exemple :

```IntuneDataImporter.exe -CollectionMappingFile c:\Users\myuser\Documents\collectionmapping.csv```

> [!Note]
> Data Importer n’affiche aucune donnée dans une page d’assistant pour indiquer le chargement du fichier de mappage de collection. Toutefois, l’outil affiche les erreurs rencontrées lors de la lecture du fichier .csv. En outre, sur la page **Résumé** de l’assistant, vous pouvez passer en revue les types **Déploiement**. L’outil affiche **Oui** dans la colonne Importable et répertorie les groupes Azure AD qu’il affectera à des objets dans la colonne **Remarques**.

### <a name="phase-1-discover-configuration-manager-objects-and-collect-data"></a>Phase 1 : Découvrir les objets Configuration Manager et collecter les données
Dans la phase 1, vous sélectionnez les objets à découvrir et demander à l’outil de collecter des informations sur les objets sélectionnés. 
1. Ouvrez l’outil et cliquez sur **Démarrer**.  
2. Lisez les informations, puis cliquez sur **Suivant**. 
3. Choisissez si vous voulez importer un jeu de données précédemment exporté ou sélectionnez les types d’objets à importer :
   - **Importer un jeu de données précédemment exporté** : choisissez **Importer un jeu de données exporté à partir d’une exécution précédente d’Intune Data Importer**, et cliquez sur **Parcourir** pour **Dossier des données exportées** afin de sélectionner un jeu de données que vous avez précédemment exporté à l’aide de l’outil Data Importer. L’utilisateur qui importe le jeu de données doit être le même que celui qui a exporté les données. Après avoir importé les données, un résumé des objets s’affiche sur la page **Résumé** de l’assistant. Si le résumé semble correct, passez directement à [Phase 3 : Importer l’objet sélectionné dans Intune](phase-3:-import-selected-object-to-intune).
 
      > [!Note]
      > Après avoir découvert et sélectionné les objets dans votre site à importer, vous pouvez exporter les objets vers un jeu de données dans la page **Se connecter à Intune** de l’assistant. Vous pouvez alors importer le jeu de données sur cette page. Le jeu de données est chiffré à l’aide des informations d’identification de l’utilisateur Windows connecté, donc seul l’utilisateur ayant exporté le jeu de données peut importer celui-ci dans l’outil. 
   - **Sélectionner les types d’objets à importer** : choisissez **Sélectionner les types d’objets à importer** pour sélectionner les types d’objets à importer et découvrir des objets dans votre environnement. Indiquez les informations suivantes sur votre site et les objets à importer.
      - **Nom du serveur de site** : indiquez le nom de domaine complet du serveur de site pour importer des objets. L’outil découvre uniquement les objets accessibles par l’utilisateur qui exécute l’outil. En général, vous spécifiez le site de niveau supérieur et exécutez l’outil avec un utilisateur qui a accès à tous les objets dans la hiérarchie du site.
      - **Code de site** : indiquez le code de site du serveur de site. Ce code à trois lettres se trouve en haut de la console Configuration Manager.
      - **Types d’objets à importer** : choisissez les objets que vous souhaitez que l’outil collecte. Vous pouvez choisir **Sélectionner tout** pour choisir tous les objets ou sélectionner des types d’objets individuels. 
4.  Cliquez sur **Suivant** pour démarrer la découverte des objets sur le site. L’outil affiche la progression de chacun des types d’objets. 
    - Lorsque l’outil ne découvre aucune donnée pour un type d’objet sélectionné, la barre de progression se remplit immédiatement pour ce type d’objet.
    - Les objets que vous n’avez pas sélectionnés ne s’affichent pas dans la page de **collecte** de données. 
    - Vous pouvez réexécuter l’outil pour les objets qui n’ont pas été collectés ou que vous avez annulés pendant le processus de collecte.

### <a name="phase-2-resolve-issues-and-select-the-objects-to-import"></a>Phase 2 : Résoudre les problèmes et sélectionner les objets à importer  
Dans la phase 2, vous passez en revue les objets détectés par l’outil, vous résolvez les problèmes qui empêchent l’importation d’objets dans Intune et vous sélectionnez les objets à importer. Si vous corrigez des problèmes, revenez à la page de **découverte de l’environnement** de l’Assistant pour redécouvrir les objets. 
5.  Cliquez sur **Suivant** pour passer en revue les objets collectés. Une page de sélection d’éléments est disponible pour chaque type d’objet collecté. 
 <!--   > [!Tip]     
    > On each item selection page, you can create a filter to help you find the objects that you want to import. However, take note of the following:
    > - When you are on an item selection page and the view is filtered, the Select all checkboxes only apply to the displayed items. Any hidden objects because of a filter are not included when using the checkboxes.
    > - Objects are always grouped under their parent item even when you sort or filter the objects.
-->
6.  Dans chaque page de sélection d’éléments, triez les objets par la colonne Importable et examinez les objets qui ne peuvent pas être importés. Les informations contenues dans la colonne Remarques fournissent des détails sur la raison pour laquelle l’outil ne peut pas importer l’objet. 
7.  Maintenant, vous devez décider si vous souhaitez corriger les problèmes pour les objets non importables. Si vous corrigez un ou plusieurs problèmes, cliquez sur Précédent jusqu’a ce que vous accédiez à la page de sélection de données de Configuration Manager, puis recollectez les données pour voir si le problème est résolu. Vous pouvez continuer à résoudre des problèmes tant que vous n’êtes pas satisfait des objets pouvant être importés. 
8.  Dans chaque page de sélection d’éléments, sélectionnez les objets que vous voulez importer. Les colonnes suivantes sont listées :
    - **Nom** : nom de l’objet Configuration Manager. 
    - **Importable** : indique si un objet peut être importé. Vous pouvez uniquement choisir des objets qui ont Oui dans la colonne Importable. 
    - **Plateforme** : indique la plateforme prise en charge par l’objet.
    - **Déjà importé** : indique si l’objet a déjà été importé à l’aide de l’outil sur cet ordinateur. 
    - **Est remplacée** (pour les applications) : indique si l’application est remplacée par une autre. Vous devez cocher la case **Afficher les applications remplacées** au sommet de la page pour afficher les applications remplacées.
    - **Remarques** : fournit des informations sur la raison pour laquelle un objet ne peut pas être importé. La colonne **Remarques** affiche aussi des informations sur les paramètres ignorés (pour certains types d’objets), mais l’objet peut quand même être importé sans ces paramètres.
    - **Bases de référence de configuration** (pour les éléments de configuration) : indique les bases de référence de configuration associées à un élément de configuration.
    - **Certificat requis** (pour les stratégies et profils) : indique si un certificat est associé à l’objet. Lorsqu’un certificat est associé à l’objet, vous devez également l’importer.
9.  Une fois que vous avez choisi les objets à importer, ils sont répertoriés dans la page Résumé. Les actions suivantes sont disponibles : 
    - **Exporter les détails** : crée un fichier .csv qui contient les informations affichées à l’écran. Il indique aussi les objets qui ne peuvent pas être importés, ainsi que le motif. Vous pouvez conserver ce fichier pour vos archives. 
    - **Exporter les données d’erreur** : exporte un fichier compressé qui contient des informations sur les données que l’outil n’a pas été en mesure de convertir ou d’importer. 

### <a name="phase-3-import-selected-objects-to-intune"></a>Phase 3 : Importer les objets sélectionnés dans Intune
Dans la phase 3, connectez-vous à Intune et importez les objets sélectionnés. 
10. Cliquez sur **Suivant**, puis sur **Se connecter à Intune** pour vous connecter au locataire Intune pour l’importation de données ou choisissez d’exporter les données.

    - **Exporter** : après avoir découvert et sélectionné les objets dans votre site à importer, vous pouvez exporter les objets vers un jeu de données. Ceci vous permet de découvrir des objets à partir d’un ordinateur qui n’a pas accès à Internet, d’exporter les données, puis d’importer les données à partir d’un ordinateur qui a accès à Internet. Le jeu de données est chiffré à l’aide des informations d’identification de l’utilisateur Windows connecté, donc seul l’utilisateur ayant exporté le jeu de données peut importer celui-ci dans l’outil. Si vous choisissez cette option, indiquez le chemin d’accès aux données exportées. 
      1. Cliquez sur **Exporter** sur la page **Se connecter à Intune**. 
      2. Cliquez sur **Parcourir** pour sélectionner le dossier de destination de l’exportation. Le dossier doit être vide. 
      3. Cliquez sur **Démarrer** pour exporter les données et une fois l’exportation terminée, cliquez sur **Fermer** pour fermer l’assistant et Data Importer.
      4. Démarrez Data Importer sur un autre ordinateur qui a accès à Internet à l’aide des mêmes informations d’identification et sélectionnez **Importer un jeu de données précédemment exporté** sur la deuxième page de l’assistant. Une fois les données importées, l’assistant vous guide vers la page **Se connecter à Intune**. 
    - **Se connecter à Intune** : vous devez vous connecter avec un compte d’administrateur général ou d’administrateur Intune. Une fois connecté, le processus d’importation démarre.
    
      > [!Important]
      > Nous vous recommandons de commencer par tester le processus d’importation de données à l’aide d’un locataire d’essai. Ensuite, après avoir vérifié que les données attendues ont été importées, vous pouvez reproduire le même processus avec votre locataire Intune de production.
12. La page de progression indique la progression de l’importation des objets. Cliquez sur **Suivant** lorsque l’importation est terminée. 
13. Dans la page Fin, les objets importés sont répertoriés. Vérifiez l’état de tous les objets qui ont rencontré une erreur pendant le processus d’importation. Les actions suivantes sont disponibles : 
    - **Exporter les détails** : crée un fichier .csv qui contient les informations affichées à l’écran. Vous pouvez conserver ce fichier pour vos archives. 
    - **Exporter les données d’erreur** : exporte un fichier compressé qui contient des informations sur les données que l’outil n’a pas été en mesure de convertir ou d’importer.

## <a name="next-steps"></a>Étapes suivantes
Après avoir importé les données dans Intune, vous devez effectuer des étapes pour [préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md). 