---
title: Présentation des rapports
titleSuffix: Configuration Manager
description: En savoir plus sur l’ensemble d’outils et de ressources disponibles pour la gestion des rapports dans Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 760b159114796922e2c8707e3b7f14484591f7a2
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141491"
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>Présentation des rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les rapports fournissent un ensemble d’outils et de ressources vous permettant d’utiliser les fonctions de rapport avancées de SQL Server Reporting Services (SSRS), ainsi que les rapports détaillés du Générateur de rapports Reporting Services. La création de rapports vous permet de recueillir, d’organiser et de présenter des informations relatives aux utilisateurs, à l’inventaire logiciel et matériel, aux mises à jour logicielles, aux applications, à l’état du site et à d’autres opérations de Configuration Manager dans votre organisation. Les rapports vous permettent de disposer de nombreux rapports prédéfinis que vous pouvez utiliser comme tel ou adapter à vos besoins, et vous pouvez créer des rapports personnalisés. Utilisez les sections suivantes pour vous aider à gérer la création de rapports dans Configuration Manager.  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services offre une gamme complète d'outils et de services prêts à être utilisés pour créer, déployer et gérer des rapports pour votre organisation, ainsi que des fonctionnalités de programmation vous permettant d'étendre et de personnaliser la fonctionnalité de création de rapport. Reporting Services est une plate-forme de création de rapport basée sur un serveur qui fournit des fonctionnalités complètes de création de rapports pour une variété de sources de données.  

 Configuration Manager utilise SQL Server Reporting Services comme solution de création de rapports. L'intégration avec Reporting Services offre les avantages suivants :  

- Utilise un système de création de rapports standard pour interroger la base de données Configuration Manager.  

- Affiche les rapports à l’aide de la Visionneuse de rapports Configuration Manager ou du Gestionnaire de rapports, qui est une connexion web au rapport.  

- Fournit une performance, une disponibilité et une évolutivité élevées.  

- Fournit des abonnements pour les rapports auxquels les utilisateurs peuvent s'abonner. Par exemple, un directeur pourrait s'abonner à un envoi automatique par courrier électronique d'un rapport quotidien détaillant l'état du déploiement d'une mise à jour logicielle.  

- Exporte les rapports que les utilisateurs peuvent sélectionner dans différents formats souvent utilisés.  

  Pour plus d'informations sur Reporting Services, voir [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) dans la documentation en ligne de SQL Server 2008.  

##  <a name="BKMK_ReportingServicesPoint"></a> Point Reporting Services  
 Le point de Reporting Services est un rôle de système de site installé sur un serveur qui exécute Microsoft SQL Server Reporting Services. Le point de Reporting Services copie les définitions de rapport Configuration Manager vers Reporting Services, crée des dossiers de rapports basés sur les catégories de rapports et paramètre les stratégies de sécurité des dossiers de rapports et des rapports en fonction des autorisations basées sur les rôles pour les utilisateurs administratifs de Configuration Manager. Toutes les 10 minutes, le point de Reporting Services se connecte à Reporting Services pour réappliquer la stratégie de sécurité si elle a été modifiée, par exemple, à l'aide du Gestionnaire de rapports. Pour plus d'informations sur la planification et l'installation d'un point de Reporting Services, consultez la documentation suivante :  

-   [Planification de la création de rapports dans System Center Configuration Manager](planning-for-reporting.md)  

-   [Configuration des rapports dans System Center Configuration Manager](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Rapports de Configuration Manager  
 Configuration Manager offre des définitions de rapports pour plus de 400 rapports dans plus de 50 dossiers de rapports qui sont copiés dans le dossier de rapports racine dans SQL Server Reporting Services lors du processus d’installation du point de Reporting Services. Les rapports sont affichés sur la console Configuration Manager et sont organisés dans des sous-dossiers en fonction de la catégorie de rapport. Les rapports ne se propagent pas en amont ou en aval dans la hiérarchie Configuration Manager, mais s’exécutent uniquement par rapport à la base de données du site dans lequel ils sont créés. Toutefois, étant donné que Configuration Manager réplique les données globales dans toute la hiérarchie, vous avez accès aux informations de toute la hiérarchie. Lorsqu'un rapport récupère des données depuis la base de donnée d'un site, il a accès aux données du site lui-même ainsi qu'à celles des sites enfants, pour chaque site de la hiérarchie. Comme les autres objets Configuration Manager, un utilisateur administratif doit disposer des autorisations appropriées pour l’exécution ou la modification de rapports. Pour exécuter un rapport, un utilisateur administratif doit avoir l'autorisation **Exécuter le rapport** pour cet objet. Pour créer ou modifier un rapport, un utilisateur administratif doit avoir l'autorisation **Modifier le rapport** pour cet objet.  

###  <a name="BKMK_CreatingReports"></a> Création et modification de rapports  
 Configuration Manager utilise le Générateur de rapports Microsoft SQL Server comme outil exclusif pour la création et l’édition des rapports basés sur des modèles ou sur SQL. Quand vous créez ou modifiez un rapport sur la console Configuration Manager, le Générateur de rapports s’ouvre. Pour plus d’informations sur la gestion des rapports, consultez [Opérations et maintenance pour les rapports dans System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

###  <a name="BKMK_RunningReports"></a> Exécution des rapports  
 Quand vous exécutez un rapport depuis la console Configuration Manager, la Visionneuse de rapports s’ouvre et se connecte à Reporting Services. Une fois que vous avez spécifié les paramètres de rapport requis, Reporting Services récupère les données et affiche les résultats dans la visionneuse. Vous pouvez également vous connecter à SQL Services Reporting Services, à la source de données pour le site et exécuter des rapports.  

###  <a name="BKMK_ReportPrompts"></a> Invites de rapport  
 Dans Configuration Manager, une invite de rapport ou un paramètre de rapport est une propriété de rapport que vous pouvez configurer quand un rapport est créé ou modifié. Les invites de rapport sont créées dans le but de limiter ou de cibler les données extraites par un rapport. Un rapport peut contenir plusieurs invites, tant que celles-ci portent un nom unique et qu'elles contiennent uniquement des caractères alphanumériques conformes aux règles SQL Server pour les identificateurs.  

 Lorsque vous exécutez un rapport, l'invite appelle la valeur d'un paramètre requis et, en fonction de cette valeur, récupère les données du rapport. Par exemple, le rapport **Informations concernant un ordinateur spécifique** récupère les informations concernant un ordinateur spécifique et invite l'utilisateur administratif à entrer un nom d'ordinateur. Reporting Services transmet ensuite la valeur spécifiée à une variable définie dans l'instruction SQL du rapport.  

###  <a name="BKMK_ReportLinks"></a> Liens de rapports  
 Dans Configuration Manager, les liens de rapports sont utilisés dans un rapport source pour permettre aux utilisateurs administratifs d’accéder facilement aux données supplémentaires, notamment les informations détaillées sur chaque élément contenu dans le rapport source. Si le rapport de destination nécessite l'exécution d'une ou de plusieurs invites d'exécution, le rapport source doit contenir une colonne avec les valeurs appropriées pour chaque invite. Vous devez spécifier le numéro de colonne qui fournit la valeur de l'invite. Par exemple, vous pouvez lier un rapport qui répertorie les ordinateurs nouvellement découverts à un rapport contenant les derniers messages reçus sur un ordinateur spécifique. Lorsque le lien est créé, vous pouvez indiquer que la colonne 2 du rapport source contient les noms d'ordinateurs ; il s'agit d'une invite requise pour le rapport de destination. Lorsque le rapport source est exécuté, les icônes de lien s'affichent à gauche de chaque ligne de données. Lorsque vous cliquez sur l'icône d'une ligne, la Visionneuse de rapports transmet la valeur dans la colonne spécifiée de cette ligne comme valeur d'invite nécessaire pour afficher le rapport de destination. Un rapport peut être configuré avec un seul lien, et ce lien peut être connecté à une seule ressource de destination.  

> [!WARNING]  
>  Si vous déplacez un rapport de destination vers un dossier de rapport différent, l'emplacement du rapport de destination change. Le lien de rapport du rapport source n'est pas automatiquement mis à jour avec le nouvel emplacement et le lien de rapport ne fonctionnera pas dans le rapport source.  

##  <a name="BKMK_ReportFolders"></a> Dossiers de rapports  
 Dans System Center Configuration Manager, les dossiers de rapports permettent de trier et de filtrer les rapports qui sont stockés dans Reporting Services. Les dossiers de rapport sont particulièrement utiles lorsque vous devez gérer plusieurs rapports. Lorsque vous installez un point de Reporting Services, les rapports sont copiés vers Reporting Services et organisés en plus de 50 dossiers de rapports. Les dossiers de rapports sont en lecture seule. Vous pouvez les modifier dans la console Configuration Manager.  

##  <a name="BKMK_ReportSubscriptions"></a> Abonnements aux rapports  
 Un abonnement aux rapports dans Reporting Services est une demande récurrente de la remise d'un rapport à un moment donné ou en réponse à un événement et dans un format d'application que vous spécifiez à l'inscription. Les abonnements représentent une alternative à l'exécution d'un rapport à la demande. Les rapports à la demande nécessitent la sélection active du rapport, à chaque fois que vous souhaitez le visualiser. En revanche, les abonnements peuvent être utilisés pour planifier, puis automatiser la remise d'un rapport.  

 Vous pouvez gérer les abonnements aux rapports dans la console Configuration Manager. Elles sont traitées sur le serveur de rapports. Les abonnements sont distribués à l'aide des extensions de remise qui sont déployées sur le serveur. Par défaut, vous pouvez créer des abonnements qui envoient des rapports à un dossier partagé ou à une adresse électronique. Pour plus d’informations sur la gestion des abonnements au rapport, consultez [Opérations et maintenance pour les rapports dans System Center Configuration Manager](operations-and-maintenance-for-reporting.md).  

##  <a name="BKMK_ReportBuilder"></a> Générateur de rapports  
 Configuration Manager utilise le Générateur de rapports Microsoft SQL Server Reporting Services en tant qu’unique outil de création et de modification des rapports basés sur un modèle et des rapports basés sur SQL. Quand vous lancez l’action pour créer ou modifier un rapport dans la console Configuration Manager, le Générateur de rapports s’ouvre. Lorsque vous créez ou modifiez un rapport pour la première fois, le Générateur de rapports est installé automatiquement. La version du Générateur de rapports associée à la version installée de SQL Server s’ouvre quand vous exécutez ou modifiez des rapports.  

 L'installation du Générateur de rapports ajoute la prise en charge de plus de 20 langues. Lorsque vous exécutez le Générateur de rapports, il affiche les données dans la langue du système d'exploitation qui s'exécute sur l'ordinateur local. Si le Générateur de rapports ne supporte pas cette langue, les données sont affichées en anglais. Le Générateur de rapports prend en charge toutes les fonctionnalités de SQL Server 2008 Reporting Services, qui inclut les fonctionnalités suivantes :  

- Il offre un environnement de création de rapports intuitif dont l'apparence est similaire à celle de Microsoft Office.  

- Il offre une mise en page flexible du rapport de SQL Server 2008 Report Definition Language (RDL).  

- Il fournit divers types d'affichage des données, dont des graphiques et des jauges.  

- Il fournit des zones de texte enrichi.  

- Il permet des exportations vers Microsoft Word.  

  Vous pouvez également ouvrir le Générateur de rapports depuis SQL Server Reporting Services.  

##  <a name="BKMK_ReportModels"></a> Modèles de rapports dans SQL Server Reporting Services  
 Dans Configuration Manager, SQL Reporting Services utilise des modèles de rapport pour aider l’utilisateur administratif à sélectionner les éléments de la base de données à inclure dans les rapports basés sur un modèle. L'utilisateur administratif chargé de générer le rapport peut choisir entre les vues et éléments spécifiques exposés dans le modèle de rapport. Au moins un modèle de rapport doit être disponible pour pouvoir générer des rapports basés sur un modèle. Les modèles de rapport sont dotés des fonctions ci-après :  

- Vous pouvez donner des noms plus pratiques aux champs des bases de données et aux vues pour faciliter la création de rapports. La connaissance de la structure de la base de données n'est pas nécessaire pour produire des rapports.  

- Vous pouvez regrouper des éléments de façon logique.  

- Vous pouvez définir des relations entre les éléments.  

- Vous pouvez sécuriser les éléments du modèle de manière à ce que les utilisateurs administratifs ne puissent visualiser que les données auxquelles ils sont autorisés à accéder.  

  Même si Configuration Manager fournit des exemples de modèles de rapport, vous pouvez également définir des modèles de rapport afin de répondre aux besoins de votre entreprise. Pour plus d’informations sur la création des modèles de rapport, consultez [Création de modèles de rapport personnalisés pour System Center Configuration Manager dans SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

## <a name="next-steps"></a>Étapes suivantes
[Planification de la création de rapports](planning-for-reporting.md)
