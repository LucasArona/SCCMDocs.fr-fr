---
title: Lignes directrices concernant la taille et les performances du site
titleSuffix: Configuration Manager
description: Résultats, méthodologie et conseils pour les tests de performances liés à la taille des sites
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: f6374e6237d586bb995e701e5577bfc553a5a689
ms.sourcegitcommit: cab3dba5ebfe90f28cedee03c1840c9a395160cc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65849283"
---
# <a name="system-center-configuration-manager-site-size-and-performance-guidelines"></a>Conseils sur la taille et les performances des sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager est le leader du marché en scalabilité et en performances. Une autre documentation les [limites maximales de scalabilité prises en charge](size-and-scale-numbers.md) et les [recommandations en termes de matériel](recommended-hardware.md) pour l’exécution des sites dans les plus grandes tailles d’environnement. Cet article donne des conseils supplémentaires sur les performances pour les environnements de toutes tailles. Ce guide peut vous aider à estimer de façon plus précise le matériel dont vous avez besoin pour déployer Configuration Manager.

Cet article se concentre sur le plus gros contributeur aux goulots d’étranglement de Configuration Manager : le sous-systèmes des entrées/sorties disque, ou IOPS. L’article :

- Présente les détails et les résultats des tests consacrés aux E/S
- Explique comment reproduire les tests avec vos environnements et votre matériel
- Suggère des spécifications d’IOPS disque pour différentes tailles d’environnement 

## <a name="performance-test-methodology"></a>Méthodologie des tests de performances

Vous pouvez déployer Configuration Manager de différentes façons, mais il est important de comprendre quelques variables dans les discussions sur le dimensionnement. Une variable est l’*intervalle des fonctionnalités*, par exemple un cycle d’inventaire. Une autre variable est le nombre d’utilisateurs, de déploiements de logiciels ou d’autres *objets* que le système référence ou qu’il déploie. Les tests de performances appliquent ces variables dans le cadre d’une *charge*. La charge génère des objets à un débit standard pour les clients en entreprise en utilisant des déploiements de production dans des environnements de différentes tailles.

> [!NOTE] 
> Les données de télémétrie du client permettent de tester les builds de la branche actuelle avec des scénarios, des configurations et des paramètres courants pour la plupart des clients. Les recommandations de cet article sont basées sur ces moyennes. Vos expériences peuvent varier en fonction de la taille et de la configuration de votre environnement. D’une façon générale, Configuration Manager nécessite du bon sens quand il est question d’objets et d’intervalles. Le simple fait que vous pouvez collecter tous les fichiers sur un système ou définir l’intervalle d’un cycle sur une minute ne signifie pas que vous devez le faire.

Les sections suivantes décrivent certains paramètres et configurations importants à utiliser lors des tests et de la modélisation des besoins de traitement pour de grandes entreprises. Ces conseils aident à définir des attentes de base en matières de performances des systèmes pour les tailles de matériel suggérées.

### <a name="feature-intervals-settings"></a>Paramètres d’intervalles des fonctionnalités 
La plupart des tests doivent utiliser des intervalles par défaut pour les cycles importants dans le système. Par exemple, les tests de l’inventaire matériel se produisent une fois par semaine avec un fichier *.mof* plus grand que le fichier par défaut. Certains intervalles de fonctionnalités, récurrents, en particulier les cycles d’inventaire matériel et logiciel, peuvent avoir des effets significatifs sur les caractéristiques des performances d’un environnement. Les environnements qui permettent des intervalles par défaut agressifs pour la collecte de données ont besoin d’un matériel surdimensionné en proportion directe avec l’augmentation de l’activité. Par exemple, supposons que vous avez 25 000 postes de travail clients et que vous voulez collecter l’inventaire matériel deux fois plus vite que l’intervalle par défaut. Vous devez commencer par dimensionner le matériel de votre site comme si vous aviez 50 000 clients.

### <a name="objects"></a>Objets 
Les tests doivent utiliser la *moyenne supérieure* des objets que les grandes entreprises tendent à utiliser avec le système. Les valeurs classiques sont des milliers de regroupements et d’applications, qui sont déployés sur des centaines de milliers d’utilisateurs ou de systèmes. Les tests doivent s’exécuter simultanément sur *tous* les objets du système à ces limites. De nombreux clients tirent parti de plusieurs fonctionnalités, mais ils n’utilisent en général pas toutes les fonctionnalités du produit à ces limites supérieures. Des tests effectués avec toutes les fonctionnalités du produit permettent de garantir les meilleures performances possibles à l’échelle du système et donnent de la marge pour des fonctionnalités que certains clients peuvent utiliser au-dessus de la moyenne. 

### <a name="loads"></a>Charges 
Les tests doivent également s’exécuter sur des charges supérieures à celles d’une *journée moyenne*, en effectuant des simulations qui génèrent des pics d’utilisation sur le système. Un exemple est la simulation de déploiements de Patch Tuesday pour vérifier que le système peut retourner rapidement des données de conformité des mises à jour au cours de ces journées de pics d’activité. Un autre exemple est la simulation de l’activité du site pendant une attaque généralisée d’un programme malveillant, pour vérifier que la notification et la réponse en temps voulu sont possibles. Bien que des machines déployées avec la taille recommandée puissent être sous-utilisées pour une journée donnée, plusieurs situations extrêmes nécessitent une certaine marge pour le traitement.

### <a name="configurations"></a>Configurations
Exécutez des tests sur une gamme de matériels physiques, Hyper-V et Azure, avec un mélange des systèmes d’exploitation pris en charge et de versions de SQL Server. Vérifiez toujours les cas qui sont les pires pour la configuration prise en charge. En général, Hyper-V et Azure retournent des résultats en matière de performances comparables à un matériel physique équivalent quand ils sont configurés de façon similaire. Les systèmes d’exploitation serveur plus récents tendent vers des performances égales ou meilleures que celles des systèmes d’exploitation serveur plus anciens. Bien que toutes les plateformes prises en charge répondent à la configuration minimale requise, en général, les dernières versions des produits pris en charge, comme Windows et SQL, produisent même de meilleures performances. 

La variation la plus importante vient des versions de SQL Server utilisées. Pour plus d’informations sur les versions de SQL Server, consultez [Quelle version de SQL dois-je exécuter ?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Principaux éléments déterminants pour les performance

Vous pouvez tester et mesurer les performances de Configuration Manager avec un large éventail de paramètres, de différentes façons et avec différentes tailles de site. Les paramètres et les objets suivants peuvent affecter considérablement les performances. Veillez à les prendre en compte lors des tests et de la modélisation des performances dans votre environnement.

> [!CAUTION]
> Si peu d’aspects de Configuration Manager ont des valeurs maximales officielles ou des limites de l’interface utilisateur empêchant une utilisation excessive, le fait d’aller au-delà des recommandations peut avoir des effets négatifs importants sur les performances d’un site. Dépasser les niveaux recommandés ou ignorer les recommandations de taille nécessite généralement un matériel plus puissant, et peut rendre votre environnement impossible à maintenir tant que vous ne réduisez pas la fréquence ou le nombre d’objets différents.

### <a name="hardware-inventory"></a>Inventaire matériel
Pour tester les performances de base de référence, définissez la collecte de l’inventaire matériel à une fois par semaine, avec la taille de fichier *.mof* par défaut plus environ 20 % de propriétés supplémentaires. N’activez pas toutes les propriétés et collectez seulement les propriétés dont vous avez réellement besoin. Soyez spécialement attentif lors de la collecte des propriétés, comme la mémoire virtuelle disponible, qui changeront *toujours* à *chaque* cycle d’inventaire. La collecte de ces propriétés peut provoquer une activité excessive sur chaque cycle d’inventaire auprès de chaque client.

### <a name="software-inventory"></a>Inventaire logiciel
Pour tester les performances de base de référence, définissez la collecte de l’inventaire logiciel à une fois par semaine, avec un niveau de détails *Produit uniquement*. La collecte de nombreux fichiers peut engendrer une charge significative sur le sous-système d’inventaire. Évitez de spécifier des filtres qui pourraient aboutir à la collecte de milliers de fichiers sur un grand nombre de clients, comme *\*.exe* ou *\*.dll*.

### <a name="collections"></a>Regroupements
Les tests des performances de base de référence peuvent inclure plusieurs milliers de regroupements avec une variété de paramètres d’étendue, de taille, de complexité et de mises à jour. Les performances d’un site ne sont pas directement fonction du nombre de regroupements sur un site. Les performances sont également le produit croisé de la complexité des requêtes de regroupement, des mises à jour complètes et incrémentielles et de la fréquence des modifications, des dépendances entre les regroupements et du nombre de clients dans les regroupements.

Là où c’est possible, réduisez les regroupements qui ont des requêtes de règles dynamiques coûteuses en ressources ou complexes. Pour les regroupements qui nécessitent ces types de règles, définissez des intervalles de mise à jour appropriés et des dates/heures de mise à jour de façon à minimiser l’impact de la réévaluation des regroupements sur le système. Par exemple, mettez à jour à minuit au lieu de le faire à 8h00.

L’activation des mises à jour incrémentielles sur des regroupements garantit des mises à jour rapides et en temps voulu de l’appartenance aux regroupements. Mais même si les mises à jour incrémentielles sont efficaces, elles représentent toujours une charge sur le système. Équilibrez la fréquence des changements que vous anticipez avec la nécessité des mises à jour en temps réel sur l’appartenance. Par exemple, supposons que vous attendez des changements importants dans les membres d’un regroupement, mais que vous ne demandez pas de mises à jour de l’appartenance en temps réel. Il est plus efficace, et cela produit une charge moindre sur le système, de mettre à jour le regroupement avec une mise à jour complète planifiée à un certain intervalle que d’activer des mises à jour incrémentielles. 

Quand vous activez des mises à jour incrémentielles, réduisez les mises à jour complètes planifiées sur les mêmes regroupements. Elles constituent seulement une méthode de secours de l’évaluation, dans la mesure où les mises à jour incrémentielles doivent normalement conserver à jour votre appartenance au regroupement quasi en temps réel. [Bonnes pratiques pour les regroupements](../../clients/manage/collections/best-practices-for-collections.md#do-not-use-incremental-updates-for-a-large-number-of-collections) recommande un nombre total maximal de regroupements pour les mises à jour incrémentielles, mais comme l’article le souligne, votre expérience peut varier en fonction de nombreux facteurs.

Les regroupements ayant seulement des règles d’appartenance directe et avec une limitation au regroupement qui n’effectue pas de mises à jour incrémentielles n’ont pas besoin de mises à jour complètes planifiées. Désactivez les planifications de mise à jour pour ces types de regroupements pour éviter une charge non nécessaire sur le système. Si la limitation au regroupement utilise des mises à jour incrémentielles, les regroupements avec seulement des règles d’appartenance directe peuvent ne pas refléter les mises à jour de l’appartenance pendant jusqu’à 24 heures ou jusqu’à ce qu’une actualisation planifiée se produise.

Alors que ce n’est pas une bonne pratique, certaines organisations créent des centaines voire même des milliers de regroupements dans le cadre de différents processus métier. Si vous utilisez une automatisation pour créer des regroupements, il est important d’activer les mises à jour incrémentielles nécessaires correctement. Réduisez au minimum et répartissez dans le temps les planifications de mise à jour complète pour éviter qu’un trop grand nombre d’évaluations des regroupements se produisent au cours d’une même période de temps. Établissez un processus de nettoyage régulier pour supprimer les regroupements inutilisés, en particulier si vous créez automatiquement des regroupements dont vous n’avez plus besoin au bout d’un certain temps.

Rappelez-vous que Configuration Manager crée des stratégies pour tous les objets dans vos regroupements quand vous ciblez des tâches comme des déploiements sur ces objets. Les changements d’appartenance, via une actualisation planifiée ou des mises à jour incrémentielles, peuvent créer de nombreuses autres tâches pour l’ensemble du système. Les builds les plus récentes de la branche actuelle ont des optimisations de stratégie spéciales pour les regroupements Tous les systèmes et Tous les utilisateurs. Lors du ciblage de toute votre entreprise, utilisez les regroupements intégrés au lieu d’un clone de ceux-ci.

Pour examiner les performances des regroupements de façon plus approfondie, vous pouvez utiliser le Collection Evaluation Viewer (CEViewer) dans le [Kit de ressources de Configuration Manager](https://www.microsoft.com/download/details.aspx?id=50012).

### <a name="discovery-methods"></a>Méthodes de découverte
Pour tester les performances de base de référence, exécutez des méthodes de découverte basées sur le serveur une fois par semaine, en activant la découverte delta de façon appropriée pour conserver les données actualisées pendant la semaine. Les tests doivent normalement découvrir une quantité d’objets proportionnelle à la taille de l’entreprise simulée. Le test de performances de base de référence pour la découverte par pulsations d’inventaire doit également être exécuté une fois par semaine.

Les données de la découverte sont des données globales. Un problème courant liés aux performances est une configuration incorrecte des méthodes de découverte basées sur le serveur dans une hiérarchie, provoquant la découverte en double des mêmes ressources de plusieurs sites principaux. Configurez avec soin les méthodes de découverte de façon à optimiser la communication avec le service cible, comme les contrôleurs de domaine Active Directory, tout en évitant la duplication de la même étendue de découverte sur plusieurs sites principaux.

## <a name="general-sizing-guidelines"></a>Conseils généraux sur le dimensionnement 

Basé sur la [méthodologie des tests de performances](#performance-test-methodology) qui précède, le tableau suivant donne des conseils généraux sur la configuration matérielle *minimale* requise pour un nombre spécifique de clients gérés. Ces valeurs doivent permettre à la plupart des entreprises ayant le nombre spécifié de clients de traiter les objets suffisamment vite pour administrer le site spécifié. Le prix de la puissance de calcul continue à décroître chaque année, et certaines des exigences ci-dessous représentent peu de chose en termes de configurations matérielles des serveurs modernes. Le matériel dont le dimensionnement est au-delà des recommandations suivantes augmente proportionnellement les performances pour les sites qui nécessitent une puissance de traitement supplémentaire ou qui ont des modèles d’utilisation spéciale du produit. 

| Postes de travail clients  | Type de site/rôle  | Cœurs<sup>1</sup>   | Mémoire (Go)   | Allocation de mémoire SQL  | IOPS :  Boîtes de réception<sup>2</sup>  | IOPS : SQL<sup>2</sup>   | Espace de stockage nécessaire (Go)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25 000  | Site d’administration centrale ou principal, avec rôle de base de données de site sur le même serveur   | 6   | 24  | 65 % | 600  | 1 700 | 350  |
| 25 000  | Site d’administration centrale ou principal                                              | 4   | 8   |     | 600  |      | 100  |
|      | SQL à distance                                                  | 4   | 16  | 70 % |      | 1 700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50 000  | Site d’administration centrale ou principal, avec rôle de base de données de site sur le même serveur   | 8   | 32  | 70 % | 1 200 | 2 800 | 600  |
| 50 000  | Site d’administration centrale ou principal                                              | 4   | 8   |     | 1 200 |      | 200  |
|      | SQL à distance                                                  | 8   | 24  | 70 % |      | 2 800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100 000 | Site d’administration centrale ou principal, avec rôle de base de données de site sur le même serveur   | 12  | 64  | 70 % | 1 200 | 5000 | 1 100 |
| 100 000 | Site d’administration centrale ou principal                                              | 6   | 12  |     | 1 200 |      | 300  |
|      | SQL à distance                                                  | 12  | 48  | 80 % |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150 000 | Site d’administration centrale ou principal, avec rôle de base de données de site sur le même serveur   | 16  | 96  | 70 % | 1 800 | 7 400 | 1 600 |
| 150 000 | Site d’administration centrale ou principal                                   | 8   | 16   |     | 1 800  |         | 400   |
|      | SQL à distance                                       | 16  | 72   | 90 % |       | 7 400    | 1 200  |
|      |                                                             |     |     |     |      |      |      |
| 700 000 | Site d’administration centrale, avec rôle de base de données de site sur le même serveur   | 20+ | 128+ | 80 % | 1 800+ | 9 000+   | 5 000+ |
| 700 000 | Site d’administration centrale                                              | 8+  | 16+  |     | 1 800+ |         | 500+  |
|      | SQL à distance                                       | 16+ | 96+  | 90 % |       | 9 000+   | 4 500+ |
|      |                                                             |     |     |     |      |      |      |
| 5 000   | Site secondaire                                   | 4   | 8    |     | 500   | -       | 200   |
| 15 000  | Site secondaire                                   | 8   | 16   |     | 500   | -       | 300   |

**Remarques**

1. **Cœurs** : Configuration Manager effectue de nombreux traitements simultanés : il a donc besoin d’un nombre minimal de cœurs de CPU pour les différentes tailles de site. Les cœurs sont plus rapides chaque année, mais il est important de vérifier qu’un nombre minimal de cœurs travaillent en parallèle. En général, les CPU des serveurs produites après 2015 satisfont aux besoins en performances de base pour les cœurs spécifiés dans le tableau. Configuration Manager tire parti des cœurs supplémentaires qui sont au-delà des recommandations, mais en règle générale, une fois que vous avez le nombre minimal de cœurs suggéré, il est préférable d’effectuer des investissements dans les ressources CPU pour augmenter la vitesse des cœurs existants au lieu d’ajouter des cœurs plus lents. Par exemple, Configuration Manager a de meilleures performances sur des tâches de traitement importantes avec 16 cœurs rapides qu’avec 24 cœurs plus lents, en supposant que d’autres ressources système comme les IOPS disque sont disponibles en quantité suffisante.
   
   La relation entre les cœurs et la mémoire est également importante. En général, le fait de disposer de moins de 3 à 4 Go de RAM par cœur réduit la capacité de traitement totale sur vos serveurs SQL. Vous avez besoin de davantage de RAM par cœur quand SQL est colocalisé avec les composants du serveur de site.
   
   > [!NOTE]
   > Tous les tests définissent des modes de gestion de l’alimentation des machines pour permettre une consommation d’énergie et des performances maximales des CPU.
   
2. **IOPS : Boîtes de réception et IOPS : SQL** fait référence aux besoins en IOPS pour les lecteurs logiques Configuration Manager et SQL. La colonne **IOPS : Boîtes de réception** indique les exigences d’IOPS pour le lecteur logique où se trouvent les répertoires de la boîte de réception de Configuration Manager. La colonne **IOPS : SQL** indique le total des besoins en IOPS pour le ou les lecteurs logiques utilisés par les différents fichiers SQL. Ces colonnes sont différentes, car les deux disques doivent avoir un formatage différent. Pour plus d’informations, et pour obtenir des exemples sur les configurations de disque SQL suggérées et de bonnes pratiques pour les fichiers, notamment des informations sur le fractionnement des fichiers sur plusieurs volumes, consultez le [Forum aux questions sur le dimensionnement et les performances des sites](../../understand/site-size-performance-faq.md).
   
   Ces deux colonnes concernant les IOPS utilisent des données provenant de l’outil standard de l’industrie, *Diskspd*. Consultez [Comment mesurer les performances des disques](#how-to-measure-disk-performance) pour obtenir des instructions sur la reproduction de ces mesures. En règle générale, dès lors que vous satisfaites aux exigences de base en termes de CPU et de mémoire, c’est le sous-système de stockage qui a l’impact le plus important sur les performances du site : les améliorations que vous y apportez donneront le meilleur retour sur investissement.
   
3.  **Espace de stockage nécessaire :** Ces valeurs réelles peuvent différer des autres recommandations documentées. Nous fournissons ces chiffres uniquement à titre de recommandation générale ; les exigences individuelles peuvent varier considérablement. Planifiez soigneusement les besoins en espace disque avant l’installation du site. Partons du principe qu’une certaine quantité de ce stockage constitue de l’espace disque libre la plupart du temps. Vous pouvez utiliser cet espace de mémoire tampon dans un scénario de récupération ou pour des scénarios de mise à niveau nécessitant de l’espace disque libre pour l’expansion du package d’installation. Votre site peut nécessiter du stockage supplémentaire pour la collecte de grandes quantités de données, pour des périodes de conservation des données plus longues et pour de grandes quantités de contenu de distribution de logiciels. Vous pouvez également stocker ces éléments sur des volumes distincts ayant un débit inférieur.

## <a name="how-to-measure-disk-performance"></a>Comment mesurer les performances des disques 

Vous pouvez utiliser l’outil standard de l’industrie *Diskspd* pour obtenir des suggestions standardisées pour les IOPS nécessaires aux environnements Configuration Manager de différentes tailles. Bien que non exhaustives, les étapes de test et les lignes de commande suivantes fournissent un moyen simple et reproductible d’estimer le débit du sous-système disque de vos serveurs. Vous pouvez comparer vos résultats à la valeur minimale recommandée pour les IOPS dans le tableau [Conseils généraux sur le dimensionnement](#general-sizing-guidelines). 

Consultez [Exemples de configurations de disque](#example-disk-configurations) pour les résultats des tests provenant de différentes configurations matérielles dans des environnements lab. Vous pouvez utiliser les données comme point de départ approximatif lors de la conception à partir de zéro du sous-système de stockage pour un nouvel environnement.

### <a name="to-test-disk-iops"></a>Pour tester les IOPS des disques  
1. Téléchargez l’utilitaire *Diskspd* ici : [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Vérifiez que vous disposez d’au moins 100 Go d’espace disque libre. Désactivez toutes les applications qui pourraient interférer ou provoquer une charge supplémentaire sur le disque, comme l’analyse antivirus active du répertoire, SQL ou SMSExec.
   
1. Exécutez *Diskspd* à partir d’une invite de commandes avec privilèges élevés. 
   
   Effectuez deux exécutions consécutives de l’outil pour le volume que vous voulez tester. Le premier test effectue des opérations d’écriture aléatoires d’une taille de 64 Ko pendant une minute. Ce test garantit le chargement du cache du contrôleur et l’allocation d’espace disque, au cas où le volume a une expansion dynamique. Ignorez les résultats du premier test. Le deuxième test doit suivre *immédiatement* le premier test, puis exécuter la même charge pendant cinq minutes.
   
   Par exemple, utilisez les lignes de commande spécifiques suivantes pour tester le volume G:\\.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Examinez la sortie du second test pour regarder le total des IOPS dans la colonne **I/O per s**. Dans l’exemple suivant, le total des IOPS est **3929,18**.
   
   ```
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------| 
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    | 
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    | 
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    | 
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    | 
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    | 
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Exemples de configurations de disque

Les tableaux suivants indiquent les résultats de l’exécution des étapes de test dans [Comment mesurer les performances des disques](#how-to-measure-disk-performance) avec différentes configurations de lab de test. Utilisez les données comme point de départ *approximatif* lors de la conception à partir de zéro du sous-système de stockage pour un nouvel environnement. 

### <a name="physical-machines-and-hyper-v"></a>Machines physiques et Hyper-V 
Le matériel s’améliore en permanence. Vous pouvez vous attendre à ce que de nouvelles générations de matériel et des combinaisons différentes de matériels, comme les disques SSD et les SAN, dépassent les performances indiquées ci-dessous. Ces résultats constituent un point de départ de base à prendre en compte lors de la conception d’un serveur ou lors des discussions avec votre fournisseur de matériel.

Le tableau suivant présente les résultats des tests avec plusieurs sous-systèmes de disques, notamment des disques durs classiques et SSD, dans différentes configurations de lab de test. Toutes les configurations formatent les disques avec des clusters de 64 Ko et les attachent à un contrôleur de disque de classe entreprise. En plus du nombre de disques en RAID, elles ont chacune au moins un disque de rechange.

| Type de disque   | Nombre de disques, n’incluant pas +1 disque de rechange | RAID     | IOPS mesurés  |
|------------------|----------------------------------------------------|---------------|---------------|
| SAS - 15 000          | 2                                                  |           1   | 620           |
| SAS - 15 000          | 4                                                  |           10  | 1 206          |
| SAS - 15 000          | 6                                                  |           10  | 1 751          |
| SAS - 15 000          | 8                                                  |           10  | 2 322          |
| SAS - 15 000          | 10                                                 |           10  | 2 882          |
| SAS - 15 000          | 12                                                 |           10  | 3 476          |
| SAS - 15 000          | 16                                                 |           10  | 4 236          |
| SAS - 15 000          | 20                                                 |           10  | 5 148          |
| SAS - 15 000          | 30                                                 |           10  | 7 398          |
| SAS - 15 000          | 40                                                 |           10  | 9 913          |
| SATA SSD         | 2                                                  |           1   | 3 300          |
| SATA SSD         | 4                                                  |           10  | 5 542          |
| SATA SSD         | 6                                                  |           10  | 7201          |
| SAS SSD          | 2                                                  |           1   | 7 539          |
| SAS SSD          | 4                                                  |           10  | 14346         |
| SAS SSD          | 6                                                  |           10  | 15 607         |

Voici les périphériques utilisés dans l’exemple. Ces informations ne constituent pas une recommandation pour un modèle ou un fabricant de matériel spécifique. 

| Type de disque    | Modèle      | Contrôleur RAID | Mémoire cache et configuration |
|-------------------|-----------------|----------------------|-------------------------------------|
| DD SAS 15 000 TOURS/MIN    | HP EH0300JDYTH  | Smart Array P822     | 2 Go, 20 % lecture / 80 % écriture           |
| SATA SSD          | ATA MK0200GCTYV | Smart Array P420i    | 1 Go, 20 % lecture / 80 % écriture           |
| SAS SSD           | HP MO0800 JEFPB | Smart Array P420i    | 1 Go, 20 % lecture / 80 % écriture           |

### <a name="azure-machine-and-disk-performance"></a>Machine Azure et performances des disques 
Les performances des disques Azure dépendent de plusieurs facteurs, comme la taille de la machine virtuelle Azure, et le nombre et le type de disques qu’elle utilise. Azure ajoute en permanence de nouveaux types de machine et de nouvelles vitesses de disque qui diffèrent selon le graphique suivant. Pour plus d’informations sur l’exécution de Configuration Manager sur Azure et des informations supplémentaires sur les E/S disque dans Azure, consultez [Forum aux questions sur Configuration Manager sur Azure](../../understand/configuration-manager-on-azure.md).

Tous les disques sont formatés en NTFS avec une taille de cluster de 64 Ko, et les lignes avec plusieurs disques sont configurées en tant que volumes agrégés par bandes via l’utilitaire Gestionnaire de disques Windows.

| Machine virtuelle Azure| Disque Azure| Nombre de disques | Espace disponible | IOPS mesurés   | Facteur de limitation   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 Mo                    | 965   | Taille de machine virtuelle Azure   |
| **DS2/DS11**                              | P20                     | 2                   | 1 024 Mo                   | 996   | Taille de machine virtuelle Azure   |
| **DS2/DS11**                              | P30                     | 1                   | 1 024 Mo                   | 996   | Taille de machine virtuelle Azure   |
| **DS2/DS11**                              | P30                     | 2                   | 2 048 Mo                   | 996   | Taille de machine virtuelle Azure   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 Mo                    | 1 994  | Taille de machine virtuelle Azure   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1 024 Mo                   | 1 992  | Taille de machine virtuelle Azure   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1 024 Mo                   | 1 993  | Taille de machine virtuelle Azure   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2 048 Mo                   | 1 992  | Taille de machine virtuelle Azure   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 Mo                    | 2 334  | Disque P20        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1 024 Mo                   | 3 984  | Taille de machine virtuelle Azure   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1 536 Mo                   | 3 984  | Taille de machine virtuelle Azure   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1 024 Mo                   | 3 112  | Disque P30        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2 048 Mo                   | 3 984  | Taille de machine virtuelle Azure   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3 072 Mo                   | 3 996  | Taille de machine virtuelle Azure   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 Mo                    | 2 335  | Disque P20        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1 024 Mo                   | 4 639  | Disque P20        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1 536 Mo                   | 6 913  | Disque P20        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2 048 Mo                   | 7 966  | Taille de machine virtuelle Azure   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1 024 Mo                   | 3 112  | Disque P30        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2 048 Mo                   | 6 182  | Disque P30        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3 072 Mo                   | 7 963  | Taille de machine virtuelle Azure   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4 096 Mo                   | 7 968  | Taille de machine virtuelle Azure   |
| **DS15**                                  | P30                     | 1                   | 1 024 Mo                   | 3 113  | Disque P30        |
| **DS15**                                  | P30                     | 2                   | 2 048 Mo                   | 6 184  | Disque P30        |
| **DS15**                                  | P30                     | 3                   | 3 072 Mo                   | 9225  | Disque P30        |
| **DS15**                                  | P30                     | 4                   | 4 096 Mo                   | 10 200 | Taille de machine virtuelle Azure   |

## <a name="see-also"></a>Voir aussi

- [Forum aux questions concernant le dimensionnement et les performances des sites](../../understand/site-size-performance-faq.md)
- [Configuration Manager sur Azure – Forum aux questions](../../understand/configuration-manager-on-azure.md)
- [Taille et échelle en chiffres](size-and-scale-numbers.md)
- [Matériel recommandé](recommended-hardware.md)

