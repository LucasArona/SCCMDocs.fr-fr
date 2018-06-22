---
title: Planification des tâches de migration
titleSuffix: Configuration Manager
description: Utilisez des tâches de migration pour configurer les données que vous souhaitez migrer vers votre environnement System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex
ms.openlocfilehash: 0481abfb1ed881355a489b99b0c3f7ec9c595e69
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342322"
---
# <a name="plan-a-migration-job-strategy-in-system-center-configuration-manager"></a>Planifier une stratégie pour les tâches de migration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des tâches de migration pour configurer les données spécifiques que vous souhaitez migrer vers votre environnement System Center Configuration Manager. Les tâches de migration identifient les objets que vous envisagez de migrer, et elles s'exécutent sur le site de niveau supérieur dans votre hiérarchie de destination. Vous pouvez configurer une ou plusieurs tâches de migration par site source. Ceci vous permet de migrer tous les objets simultanément ou des sous-ensembles limités de données avec chaque tâche.  

 Vous pouvez créer des tâches de migration une fois que Configuration Manager a collecté avec succès les données d’un ou de plusieurs sites à partir de la hiérarchie source. Vous pouvez migrer des données dans n'importe quel ordre à partir des sites source contenant des données. Avec un site source Configuration Manager 2007, vous ne pouvez migrer les données qu’à partir du site où un objet a été créé. Avec les sites sources exécutant System Center 2012 Configuration Manager ou ultérieur, toutes les données que vous pouvez migrer sont disponibles sur le site de plus haut niveau de la hiérarchie source.  

 Avant de migrer des clients entre hiérarchies, vérifiez que les objets que les clients utilisent ont été migrés et que ces objets sont disponibles dans la hiérarchie de destination. Par exemple, quand vous migrez depuis une hiérarchie source Configuration Manager 2007 SP2, vous pouvez recevoir une publication pour du contenu déployé sur un regroupement personnalisé qui a un client. Dans ce cas, nous vous recommandons de migrer le regroupement, la publication et le contenu associé avant de migrer le client. Ces données ne peut pas être associées au client dans la hiérarchie de destination si le contenu, le regroupement et la publication ne sont pas migrés avant la migration du client. Si un client n'est pas associé aux données liées à une publication et à un contenu exécutés précédemment, le contenu peut être proposé au client pour l'installation dans la hiérarchie de destination, ce qui peut être inutile. Si le client est migré après la migration des données, il est associé à ce contenu et à cette publication, et sauf si la publication est récurrente, le contenu n'est plus proposé pour la publication migrée.  

 Pour certains objets, la migration des données de la hiérarchie source vers la hiérarchie de destination ne suffit pas. Par exemple, pour pouvoir migrer les mises à jour logicielles des clients vers votre hiérarchie de destination, vous devez déployer un point de mise à jour logicielle actif, configurer le catalogue des produits et synchroniser le point de mise à jour logicielle avec WSUS (Windows Server Update Services) dans la hiérarchie de destination.  

 Utilisez les sections suivantes pour planifier vos tâches de migration.  

-   [Types de tâche de migration](#Types_of_Migration)  

-   [Planification générale de toutes les tâches de migration](#About_Migration_Jobs)  

-   [Planification des tâches de migration de regroupements](#About_Collection_Migration)  

-   [Planification des tâches de migration d’objets](#About_Object_Migration)  

-   [Planification des tâches de migration d’objets déjà migrés](#About_Object_Migrations)  

##  <a name="Types_of_Migration"></a> Types de tâches de migration  
 Configuration Manager prend en charge les types de tâche de migration suivants. Chaque type de tâche est conçu pour vous aider à définir les objets que vous pouvez inclure dans cette tâche.  

 **Migration de regroupements** (prise en charge uniquement pour la migration depuis Configuration Manager 2007 SP2) : Migre les objets liés aux regroupements de votre choix. Par défaut, la migration d’un regroupement inclut tous les objets qui sont associés aux membres du regroupement. Vous pouvez exclure des instances d'objet spécifiques lors de l'utilisation d'une tâche de migration de regroupement.  

 **Migration d’objets** : Migre des objets individuels de votre choix. Vous sélectionnez uniquement les données à migrer.  

 **Migration d’objets déjà migrés** : Migre les objets que vous avez déjà migrés, quand ces objets ont été mis à jour dans la hiérarchie source après leur dernière migration.  

###  <a name="Objects_that_can_migrate"></a> Objets que vous pouvez migrer  
 Tous les objets ne peuvent pas migrer en fonction du type de tâche de migration. La liste suivant indique le type des objets que vous pouvez migrer à l’aide de chaque type de tâche de migration.  

> [!NOTE]  
>  Les tâches de migration de regroupements sont disponibles uniquement quand vous migrez des objets à partir d’une hiérarchie source Configuration Manager 2007 SP2.  

 **Types de tâche que vous pouvez utiliser pour migrer chaque objet**  

-   **Publications** (disponibles pour une migration à partir des sites sources Configuration Manager 2007 pris en charge)  

    -   Migration du regroupement  


-   **Catalogue Asset Intelligence**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Configuration matérielle requise pour Asset Intelligence**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Liste de logiciels Asset Intelligence**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Limites**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Bases de référence de configuration**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Éléments de configuration**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Fenêtres de maintenance**  

    -   Migration du regroupement  


-   **Images de démarrage de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de pilotes de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Pilotes de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Images de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de déploiement du système d’exploitation**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de distribution de logiciels**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Règles de contrôle de logiciel**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages de déploiement de mises à jour logicielles**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Modèles de déploiement de mises à jour logicielles**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Déploiements de mises à jour logicielles**  

    -   Migration du regroupement  


-   **Listes de mises à jour logicielles**  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Séquences de tâches**  

    -   Migration du regroupement  

    -   Migration d'objet  

    -   Migration d'objets migrés précédemment  

-   **Packages d’applications virtuelles**  

    -   Migration du regroupement  

    -   Migration d'objet  

    > [!IMPORTANT]  
    >  Bien que vous puissiez migrer un package d'application virtuelle en utilisant la migration d'objet, vous ne pouvez pas le migrer en utilisant le type de tâche de migration **Migration d'objets migrés précédemment**. Vous devez plutôt supprimer le package d'application virtuelle migré du site de destination, puis créer une tâche de migration pour migrer l'application virtuelle.  

##  <a name="About_Migration_Jobs"></a> Planification générale de toutes les tâches de migration  
 Utilisez l’Assistant Création de tâche de migration pour créer une tâche de migration pour migrer des objets vers votre hiérarchie de destination. Le type de tâche de migration que vous créez détermine les objets pouvant être migrés. Vous pouvez créer et utiliser plusieurs tâches de migration pour migrer des données à partir du même site source ou de plusieurs sites source. L'utilisation d'un type de tâche de migration n'empêche pas l'utilisation d'un autre type de tâche de migration.  

 Une fois la tâche de migration exécutée, son état devient **Terminé** , et vous ne pouvez plus la réexécuter. Toutefois, vous pouvez créer une tâche de migration pour migrer les objets migrés par la tâche d'origine, sans compter que la nouvelle tâche de migration peut inclure des objets supplémentaires également. Quand vous créez des tâches de migration supplémentaires, les objets déjà migrés s’affichent avec l’état **Migré**. Vous pouvez sélectionner ces objets pour les migrer à nouveau, mais si les objets n’ont pas été mis à jour dans la hiérarchie source, il est inutile de les migrer à nouveau. Si un objet a été mis à jour dans la hiérarchie source après sa migration, vous pouvez identifier l'objet lorsque vous utilisez le type de tâche de migration **Objets modifiés après la migration**.  

 Vous pouvez supprimer une tâche de migration avant son exécution. Cependant, une fois qu’une tâche de migration a été effectuée, elle reste visible dans la console Configuration Manager et ne peut pas être supprimée. Chaque tâche de migration terminée ou qui n’a pas encore été exécutée reste visible dans la console Configuration Manager jusqu’à ce que le processus de migration soit fini et que vous ayez nettoyé les données de migration.  

> [!NOTE]  
>  Après avoir terminé la migration en utilisant l’action **Nettoyer les données de migration**, vous pouvez reconfigurer la même hiérarchie comme hiérarchie source active pour restaurer la visibilité des objets précédemment migrés.  

 Pour afficher les objets contenus dans une tâche de migration au sein de la console Configuration Manager, sélectionnez la tâche de migration, puis choisissez l’onglet **Objets dans la tâche**.  

 Utilisez les informations dans les sections suivantes pour planifier toutes les tâches de migration.  

### <a name="data-selection"></a>Sélection de données  
 Lorsque vous créez une tâche de migration de regroupement, vous devez sélectionner au moins un regroupement. Une fois les regroupements sélectionnés, l’Assistant Création de tâche de migration affiche les objets associés aux regroupements. Par défaut, tous les objets associés aux regroupements sélectionnés sont migrés, mais vous pouvez désélectionner les objets à ne pas migrer avec cette tâche. Quand vous désélectionnez un objet qui a des objets dépendants, ces derniers sont également désélectionnés. Tous les objets désélectionnés sont ajoutés à une liste d’exclusion. Les objets dans une liste d'exclusion sont éliminés de la sélection automatique pour les prochaines tâches de migration. Vous devez modifier manuellement la liste d'exclusion pour supprimer les objets qui doivent être sélectionnés automatiquement pour les tâches de migration suivantes.  

### <a name="site-ownership-for-migrated-content"></a>Propriétaire de site pour le contenu migré  
 Lorsque vous migrez du contenu pour des déploiements, vous devez attribuer l'objet de contenu à un site dans la hiérarchie de destination. Ce site devient alors le propriétaire de ce contenu dans la hiérarchie de destination. Bien que le site de niveau supérieur de votre hiérarchie de destination soit le site qui migre les métadonnées du contenu, c'est le site attribué qui accède aux fichiers source d'origine du contenu dans le réseau.  

 Pour réduire la bande passante réseau utilisée lors de la migration, transférez la propriété du contenu au site disponible le plus proche. Dans la mesure où les informations sur le contenu sont partagées globalement dans System Center Configuration Manager, elles sont disponibles sur tous les sites.  

 Les informations sur le contenu sont partagées avec tous les sites de la hiérarchie de destination en utilisant la réplication de base de données. Cependant, le contenu que vous affectez à un site principal puis que vous déployez sur des points de distribution sur d’autres sites principaux est transféré via la réplication basée sur les fichiers. Ce transfert est routé via le site administration centrale, puis vers chaque site principal supplémentaire. En centralisant les packages que vous prévoyez de distribuer sur plusieurs sites principaux avant la migration ou au cours de la migration quand vous définissez un site comme propriétaire du contenu, vous pouvez réduire les transferts de données sur les réseaux à faible bande passante.  

### <a name="role-based-administration-security-scopes-for-migrated-data"></a>Étendues de sécurité de l’administration basée sur des rôles pour les données migrées  
 Lorsque vous migrez des données vers une hiérarchie de destination, vous devez affecter une ou plusieurs étendues de sécurité d'administration basée sur des rôles aux objets dont les données sont migrées. Ainsi, seuls les utilisateurs administratifs appropriés peuvent accéder à ces données après la migration. Les étendues de sécurité que vous spécifiez sont définies par la tâche de migration et sont appliquées à chaque objet migré par cette tâche. Si vous voulez appliquer des étendues de sécurité différentes à différents ensembles d’objets et affecter ces étendues au cours de la migration, vous devez migrer les différents ensembles d’objets en utilisant différentes tâches de migration.  

 Avant de configurer une tâche de migration, vérifiez comment l’administration basée sur des rôles fonctionne dans System Center Configuration Manager. Si nécessaire, configurez une ou plusieurs étendues de sécurité pour les données à migrer pour définir les utilisateurs autorisés à accéder aux objets migrés dans la hiérarchie de destination.  

 Pour plus d’informations sur les étendues de sécurité et l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles pour System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Vérification des actions de migration  
 Quand vous configurez une tâche de migration, l’Assistant Création de tâche de migration affiche une liste des actions à effectuer pour garantir la réussite de la migration, ainsi qu’une liste des actions entreprises par Configuration Manager pendant la migration des données sélectionnées. Lisez attentivement ces informations pour vérifier le résultat attendu.  

### <a name="schedule-migration-jobs"></a>Planifier des tâches de migration  
 Par défaut, une tâche de migration s'exécute immédiatement après sa création. Vous pouvez cependant spécifier le moment d’exécution de la tâche de migration quand vous créez la tâche ou en modifiant les propriétés de la tâche. Vous pouvez planifier l’exécution de la tâche de migration comme suit :  

-   Exécuter la tâche maintenant  

-   Exécuter la tâche à une heure de début spécifique  

-   Ne pas exécuter la tâche  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Spécifier la résolution des conflits de données migrées  
 Par défaut, les tâches de migration ne remplacent pas les données dans la base de données de destination, sauf si vous configurez la tâche de migration pour qu’elle ignore ou remplace les données déjà migrées vers la base de données de destination.  

##  <a name="About_Collection_Migration "></a> Planifier des tâches de migration de regroupements  
 Les tâches de migration de regroupements sont disponibles uniquement quand vous migrez des données à partir d’une hiérarchie source qui exécute une version prise en charge de Configuration Manager 2007. Vous devez spécifier un ou plusieurs regroupements à migrer lorsque vous utilisez la migration basée sur le regroupement. Pour chaque regroupement que vous spécifiez, la tâche de migration sélectionne automatiquement tous les objets associés pour les migrer. Par exemple, si vous sélectionnez un regroupement d'utilisateurs, les membres du regroupement sont identifiés et vous pouvez migrer les déploiements associés au regroupement. Vous pouvez également sélectionner d'autres objets de déploiement à migrer associés à ces membres. Tous ces éléments sélectionnés sont ajoutés à la liste des objets qui peuvent être migrés.  

 Quand vous migrez un regroupement, System Center Configuration Manager migre également les paramètres du regroupement, notamment les fenêtres de maintenance et les variables du regroupement. Il ne peut cependant pas migrer les paramètres du regroupement pour l’approvisionnement du client AMT.  

 Utilisez les informations des sections suivantes pour découvrir les configurations supplémentaires qui peuvent s’appliquer aux tâches de migration basées sur le regroupement.  

### <a name="exclude-objects-from-collection-migration-jobs"></a>Exclure des objets d’une tâche de migration de regroupement  
 Vous pouvez exclure des objets d'une tâche de migration de regroupement. Quand vous excluez un objet d’une tâche de migration de regroupement, l’objet est ajouté à une liste d’exclusion globale qui contient tous les objets que vous avez exclus des tâches de migration créées pour un site source dans la hiérarchie source actuelle. Les objets dans la liste d'exclusion peuvent toujours être migrés dans les tâches suivantes, mais ils ne sont pas inclus automatiquement lorsque vous créez une tâche de migration basée sur le regroupement.  

 Vous pouvez modifier la liste d'exclusion pour supprimer des objets que vous avez exclus. Lorsque vous supprimez un objet de la liste d'exclusion, il est automatiquement sélectionné lorsqu'un regroupement associé est défini lors de la création d'une tâche de migration.  

### <a name="unsupported-collections"></a>Regroupements non pris en charge  
 Configuration Manager peut migrer les regroupements d’utilisateurs par défaut, les regroupements d’appareils et la plupart des regroupements personnalisés à partir d’une hiérarchie source Configuration Manager 2007. Toutefois, Configuration Manager ne peut pas migrer les regroupements qui contiennent des utilisateurs et des appareils dans le même regroupement.  

 Vous ne pouvez pas migrer les regroupements suivants :  

-   Un regroupement qui contient des utilisateurs et des appareils.  

-   Un regroupement qui contient une référence à un regroupement correspondant à un type de ressource différent. tel qu'un regroupement de périphériques ayant un sous-regroupement ou un lien à un regroupement d'utilisateurs. Dans cet exemple, seul le regroupement de plus haut niveau migre.  

-   Un regroupement qui contient une règle pour inclure des ordinateurs inconnus. Le regroupement est migré, mais la règle d'inclusion d'ordinateurs inconnus n'est pas migrée.  

### <a name="empty-collections"></a>Regroupements vides  
 Un regroupement vide est un regroupement qui n'a aucune ressource associée. Quand Configuration Manager migre un regroupement vide, il convertit le regroupement en un dossier d’organisation qui ne contient aucun utilisateur ou appareil. Ce dossier est créé avec le nom du regroupement vide sous le nœud **Regroupements d’utilisateurs** ou **Regroupements de périphériques** dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Regroupements liés et sous-regroupements  
 Quand vous migrez des regroupements liés à d’autres regroupements ou ayant des sous-regroupements, Configuration Manager crée un dossier sous le nœud **Regroupements d’utilisateurs** ou **Regroupements d’appareils** en plus des regroupements et sous-regroupements liés.  

### <a name="collection-dependencies-and-include-objects"></a>Dépendances de regroupements et inclusion d’objets  
 Quand vous spécifiez un regroupement à migrer dans l’Assistant Création de tâche de migration, tous les regroupements qui en dépendent sont automatiquement sélectionnés pour être inclus dans la tâche. Ce comportement garantit que toutes les ressources nécessaires sont disponibles après la migration.  

 Par exemple, vous sélectionnez un regroupement pour les appareils qui exécutent Windows 7 et qui est nommé **Win_7**. Ce regroupement est limité à un regroupement contenant tous vos systèmes d’exploitation clients, nommé **All_Clients**. Le regroupement **All_Clients** sera automatiquement sélectionné pour la migration.  

### <a name="collection-limiting"></a>Limitation au regroupement  
 Avec System Center Configuration Manager, les regroupements sont des données globales et sont évalués au niveau de chaque site de la hiérarchie. Par conséquent, pensez à limiter l’étendue d’un regroupement après sa migration. Pendant la migration, vous pouvez identifier un regroupement à partir de la hiérarchie de destination à utiliser pour limiter l'étendue du regroupement que vous migrez, de sorte que le regroupement migré n'inclut pas de membres imprévus.  

 Par exemple, dans Configuration Manager 2007, les regroupements sont évalués au niveau du site qui les crée et au niveau des sites enfants. Une publication peut être déployée vers un site enfant seulement, et cela limiterait l'étendue de cette publication à ce site enfant. En comparaison, avec System Center Configuration Manager, les regroupements sont évalués au niveau de chaque site, et les publications associées sont ensuite évaluées pour chaque site. La limitation au regroupement vous permet d'affiner les membres du regroupement à partir d'un autre regroupement afin d'éviter l'ajout de membres du regroupement imprévus.  

### <a name="site-code-replacement"></a>Remplacement du code de site  
 Quand vous migrez un regroupement ayant des critères qui identifient un site Configuration Manager 2007, vous devez spécifier un site spécifique dans la hiérarchie de destination. Cela garantit que le regroupement migré reste fonctionnel dans votre environnement de destination et que son étendue n'augmente pas.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Spécifier le comportement pour les publications migrées  
 Par défaut, les tâches de migration basée sur des regroupements désactivent les publications qui migrent vers la hiérarchie de destination. Cela inclut tous les programmes qui sont associés à la publication. Quand vous créez une tâche de migration basée sur un regroupement qui a des publications, l’option **Activer les programmes à déployer dans Configuration Manager après la migration d’une publication** apparaît dans la page **Paramètres** de l’Assistant Création de tâche de migration. Si vous sélectionnez cette option, les programmes associés aux publications sont activés après qu'ils ont migré. Au titre des bonnes pratiques, ne sélectionnez pas cette option. Au lieu de cela, activez les programmes une fois qu’ils ont migré quand vous pouvez vérifier les clients qui les recevront.  

> [!NOTE]  
>  L’option **Activer les programmes à déployer dans Configuration Manager après la migration d’une publication** s’affiche uniquement quand vous créez une tâche de migration basée sur un regroupement et quand la tâche de migration contient des publications.  

 Pour activer un programme après la migration, décochez **Désactiver ce programme sur les ordinateurs qui le publient** sous l’onglet **Avancé** des propriétés du programme.  

##  <a name="About_Object_Migration"></a> Planifier des tâches de migration d’objets  
 Contrairement à la migration des regroupements, vous devez sélectionner chaque objet et instance d'objet que vous souhaitez migrer. Vous pouvez sélectionner des objets individuels (comme les publications d’une hiérarchie Configuration Manager 2007, ou une publication d’une hiérarchie System Center 2012 Configuration Manager ou System Center Configuration Manager) à ajouter à la liste d’objets à migrer pour une tâche de migration spécifique. Tous les objets que vous n'ajoutez pas à la liste de migration ne sont pas migrés vers le site de destination par la tâche de migration d'objet.  

 Les tâches de migration basées sur un objet ne sont associées à aucune autre configuration supplémentaire à planifier au-delà de celles applicables à toutes les tâches de migration.  

##  <a name="About_Object_Migrations"></a> Planifier des tâches de migration d’objets déjà migrés  
 Si un objet que vous avez déjà migré vers la hiérarchie de destination est mis à jour dans la hiérarchie source, vous pouvez migrer de nouveau l'objet en utilisant le type de tâche **Objets modifiés après la migration** . Par exemple, quand vous renommez ou que vous mettez à jour les fichiers source d’un package dans la hiérarchie source, la version du package est incrémentée dans la hiérarchie source. Après l'incrémentation de version du package, le package peut être identifié pour la migration par ce type de tâche.  

 Ce type de tâche est similaire au type de migration d'objet, à l'exception du fait que lorsque vous sélectionnez des objets à migrer, vous pouvez choisir uniquement parmi des objets qui ont été mis à jour après avoir été migrés par une tâche de migration précédente.   

 Quand vous sélectionnez ce type de tâche, le comportement de résolution des conflits sur la page **Paramètres** de l’Assistant Création de tâche de migration est configuré pour remplacer les objets précédemment migrés. Ce paramètre ne peut pas être modifié.  

> [!NOTE]  
>  Cette tâche de migration peut identifier les objets qui sont automatiquement mis à jour par hiérarchie source, en plus des objets mis à jour par un utilisateur administratif.  
