---
title: Questions fréquentes (FAQ) sur la taille et les performances des sites
titleSuffix: Configuration Manager
description: Réponses aux questions courantes sur le dimensionnement et les performances des sites System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 8157ee2212e18d4938beabd40f16e66a319d0b8c
ms.sourcegitcommit: cab3dba5ebfe90f28cedee03c1840c9a395160cc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65849293"
---
# <a name="system-center-configuration-manager-site-sizing-and-performance-faq"></a>Questions fréquentes (FAQ) sur la taille et les performances des sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Ce document présente les questions fréquentes sur les problèmes courants de dimensionnement et de performance des sites Configuration Manager.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Exemples et questions fréquentes sur la configuration des disques et machines

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Comment dois-je formater les disques sur mon serveur de site et SQL Server ?

Séparez les boîtes de réception Configuration Manager et les fichiers SQL sur au moins deux volumes distincts. Cette séparation vous permet d’optimiser les tailles d’allocation de clusters pour les différents types d’E/S qu’ils effectuent. 

Pour le volume qui héberge vos boîtes de réception de serveur de sites, utilisez NTFS avec des unités d’allocation 4K ou 8K. ReFS écrit 64K même pour les petits fichiers. Configuration Manager a beaucoup de petits fichiers, si bien que ReFS peut produire une surcharge de disque inutile.

Pour les disques contenant des fichiers de base de données SQL, utilisez un formatage NTFS ou ReFS, avec des unités d’allocation 64K.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Comment et où dois-je organiser mes fichiers de base de données SQL ?

Les groupes modernes de disques SSD et Stockage Premium Azure peuvent fournir des IOPS élevées sur un volume unique, avec quelques disques. En général, vous ajoutez d’autres disques à un groupe pour augmenter le stockage, et non pour augmenter le débit. Si vous utilisez des disques à broches physiques, vous avez peut-être besoin de plus d’IOPS que celles que vous pouvez générer sur un volume unique. Vous devez allouer 60 % du nombre total d’IOPS recommandé et de l’espace disque au fichier *.mdf*, 20 % au fichier *.ldf* et 20 % aux fichiers temporaires de données et de journal. Les fichiers temporaires et *.ldf* peuvent résider sur un volume unique avec 40 % (20 % + 20 %) de vos IOPS allouées.

Par défaut, SQL crée un seul fichier de données temporaire. Il est préférable d’en créer plus, pour éviter les verrous SQL et éviter d’attendre d’accéder à un fichier unique. Les opinions de la communauté varient sur le nombre optimal de fichiers de données temporaires à créer, entre quatre et huit. Les tests révèlent peu de différences entre quatre et huit fichiers, donc vous pouvez créer quatre fichiers de données temporaires *de taille identique*. Vos fichiers de données tempdb doivent occuper jusqu’à 20 à 25 % de la taille de votre base de données complète.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Y a-t-il d’autres recommandations pour la configuration des disques ?

Lorsque vous pouvez le configurer, allouez 70 % de la mémoire du contrôleur RAID aux opérations d’écriture et 30 % aux opérations de lecture. En règle générale, utilisez une configuration de groupe RAID 10 pour la base de données du site. RAID 1 est aussi acceptable pour les sites à petite échelle avec des besoins d’E/S faibles, ou si vous utilisez des disques SSD rapides. Avec des baies de disques plus grandes, configurez des disques de secours pour remplacer automatiquement les disques défaillants.

**Exemple : machine physique avec des disques physiques** 

Les [recommandations de dimensionnement](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pour un serveur de site colocalisé avec un serveur SQL comprenant **100 000** clients préconisent 1 200 IOPS pour les boîtes de réception de serveur de site et 5 000 IOPS pour les fichiers SQL Server.

La configuration de disque obtenue peut ressembler à ceci :

| Lecteurs<sup>1</sup> | RAID | Format | Contenu de volume | Nombre minimal d’IOPS nécessaire| IOPS approximativement fournies<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2x10k          | 1         | -           | Windows              |                     | -                |
| 6x15k          | 10        | NTFS 8k     | Boîtes de réception ConfigMgr    |     1 700            | 1 751             |
| 12x15k         | 10        | 64k ReFS    | SQL .mdf             | 60 % * 5 000 = 3 000     | 3 476             |
| 8x15k          | 10        | 64k ReFS    | Fichiers SQL .ldf et temporaires | 40 % * 5 000 = 2 000     | 2 322             |

1. N’inclut pas les disques de secours recommandés. 
2. Cette valeur provient des [exemples de configuration de disque](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>J’utilise Hyper-V sur Windows Server. Comment dois-je configurer les disques pour optimiser les performances de mes machines virtuelles Configuration Manager ?

Hyper-V offre des performances similaires à celles d’un serveur physique, si les ressources matérielles (cœurs de processeur et stockage direct) sont 100 % dédiées à la machine virtuelle. L’utilisation de fichiers de disque *.vhd* ou *.vhdx* de taille fixe engendre un impact sur les performances d’E/S compris entre 1 et 5 %. L’utilisation de fichiers de disque *.vhd* ou *.vhdx* de taille dynamique engendre un impact sur les performances d’E/S pouvant aller jusqu’à 25 % pour la charge de travail Configuration Manager. Si vous avez besoin de disques à taille dynamique, compensez en ajoutant 25 % de performances IOPS supplémentaires au groupe.

Quand vous exécutez votre serveur de site Configuration Manager ou SQL à l’intérieur d’une machine virtuelle, isolez les lecteurs du système d’exploitation hôte Hyper-V des lecteurs de données et du système d’exploitation de la machine virtuelle.

Pour plus d’informations sur l’optimisation des machines virtuelles, consultez [Réglage des performances des serveurs Hyper-V](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Exemple : serveur de site basé sur une machine virtuelle Hyper-V** 

Les [recommandations de dimensionnement](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pour un serveur de site colocalisé avec un serveur SQL comprenant **150 000** clients préconisent 1 800 IOPS pour les boîtes de réception de serveur de site et 7 400 IOPS pour les fichiers SQL Server.

La configuration de disque obtenue peut ressembler à ceci :

| Lecteurs<sup>1</sup> | RAID | Format<sup>2</sup> | Contenu de volume | Nombre minimal d’IOPS nécessaire| IOPS approximativement fournies<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2x10k          | 1         | -              | Système d’exploitation hôte Hyper-V           | -                    | -                |
| 2x10k          | 1         | -              | Système d’exploitation du serveur de site (machine virtuelle)       | -                    | -                |
| 2xSSD SAS      | 1         | NTFS 8k        | Boîtes de réception ConfigMgr (machine virtuelle)    | 1 800                 | 7 539             |
| 4xSSD SAS      | 10        | 64k ReFS       | SQL hôte (machine virtuelle) (tous les fichiers) | 7 400                 | 14346            |

1. N’inclut pas les disques de secours recommandés. 
2. Fichier *.vhdx* direct de taille fixe pour le lecteur de la machine virtuelle dédié au volume sous-jacent. 
3. Cette valeur provient des [exemples de configuration de disque](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Existe-t-il des suggestions pour les environnements Configuration Manager dans Microsoft Azure ?

Commencez par consulter les [questions fréquentes sur Configuration Manager dans Azure](configuration-manager-on-azure.md).

Les machines virtuelles Azure IaaS (infrastructure as a service) qui exploitent des disques Stockage Premium peut avoir des IOPS élevées. Sur ces machines virtuelles, configurez des disques supplémentaires pour les besoins d’espace disque anticipés, plutôt que pour des IOPS supplémentaires.

Stockage Azure est par nature redondant et ne nécessite pas plusieurs disques à des fins de disponibilité. Vous pouvez agréger par bandes les disques dans le Gestionnaire de disque ou les espaces de stockage pour fournir des performances et de l’espace supplémentaires.

Pour obtenir plus d’informations et des recommandations sur la manière d’optimiser les performances de Stockage Premium et d’exécuter des serveurs SQL dans des machines virtuelles IaaS Azure, consultez :

- [Optimiser les performances des applications](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Conseils pour les disques](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Exemple : serveur de site basé sur Azure** 

Les [recommandations de dimensionnement](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pour un serveur de site colocalisé avec un serveur SQL comprenant **50 000** clients préconisent huit cœurs, 32 Go et 1 200 IOPS pour les boîtes de réception de serveur de site, ainsi que 2 800 IOPS pour les fichiers SQL Server.

La machine Azure obtenue peut être une DS13v2 (huit cœurs, 56 Go) avec la configuration de disque suivante :

| Lecteurs | Format | Contient | Nombre minimal d’IOPS nécessaire| IOPS approximativement fournies<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Système d’exploitation du serveur de site     | -                    | -                |
| 1xP20 (512 Go)    | NTFS 8k       | Boîtes de réception ConfigMgr  | 1 200                 | 2 334             |
| 1xP30 (1 024 Go)   | 64k ReFS      | SQL (tous les fichiers<sup>2</sup>) | 2 800                 | 3 112             |

1. Cette valeur provient des [exemples de configuration de disque](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. Les [recommandations Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) préconisent de placer TempDB sur le lecteur *D:* SSD local, étant donné qu’il ne va pas dépasser l’espace disponible, tout en permettant de distribuer des E/S de disque supplémentaires.

**Exemple : serveur de site basé sur Azure (pour une augmentation des performances instantanée)** 

Le débit de disque Azure est limité par la taille de la machine virtuelle. La configuration indiquée dans l’exemple Azure précédent peut limiter une future expansion ou une augmentation des performances. Si vous ajoutez des disques supplémentaires lors du déploiement initial de votre machine virtuelle Azure, vous pouvez faire migrer votre machine virtuelle Azure pour en augmenter la puissance de traitement ultérieurement, avec un investissement initial minimal. Il est beaucoup plus simple de planifier en amont l’augmentation des performances de site en fonction de besoins, au lieu d’avoir à effectuer plus tard une migration compliquée.

Modifiez les disques dans l’exemple Azure précédent pour voir comment les IOPS changent.

**DS13v2** 

| Lecteurs<sup>1</sup> | Format | Contient | Nombre minimal d’IOPS nécessaire| IOPS approximativement fournies<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Système d’exploitation du serveur de site     | -                    | -                |
| 2xP20 (1 024 Go)   | NTFS 8k       | Boîtes de réception ConfigMgr  | 1 200                 | 3 984             |
| 2xP30 (2 048 Go)   | 64k ReFS      | SQL (tous les fichiers<sup>3</sup>) | 2 800                 | 3 984             |

1. Les disques sont agrégés par bandes à l’aide des espaces de stockage.
2. Cette valeur provient des [exemples de configuration de disque](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). La taille des machines virtuelles limite les performances.
3. Les [recommandations Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) préconisent de placer TempDB sur le lecteur *D:* SSD local, étant donné qu’il ne va pas dépasser l’espace disponible, tout en permettant de distribuer des E/S de disque supplémentaires.

Si vous avez besoin de performances plus élevées à l’avenir, vous pouvez faire migrer votre machine virtuelle vers une DS14v2, ce qui permet de doubler le processeur et la mémoire. La bande passante de disque supplémentaire autorisée par cette taille de machine virtuelle augmentera aussi instantanément les IOPS de disque disponibles sur vos disques précédemment configurés.

**DS14v2**

| Lecteurs<sup>1</sup> | RAID | Format | Contient | Nombre minimal d’IOPS nécessaire| IOPS approximativement fournies<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;standard&gt; | -             | Système d’exploitation du serveur de site     | -                    | -                |
| 2xP20 (1 024 Go)   | NTFS 8k       | Boîtes de réception ConfigMgr  | 1 200                 | 4 639             |
| 2xP30 (2 048 Go)   | 64k ReFS      | SQL (tous les fichiers<sup>3</sup>) | 2 800                 | 6 182             |

1. Les disques sont agrégés par bandes à l’aide des espaces de stockage.
2. Cette valeur provient des [exemples de configuration de disque](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). La taille des machines virtuelles limite les performances.
3. Les [recommandations Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) préconisent de placer TempDB sur le lecteur *D:* SSD local, étant donné qu’il ne va pas dépasser l’espace disponible, tout en permettant de distribuer des E/S de disque supplémentaires.

## <a name="other-common-sql-server-related-performance-questions"></a>Autres questions fréquentes sur les performances liées à SQL Server 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>Une exécution de SQL colocalisé avec le serveur de site est-elle préférable à son exécution sur un serveur distant ?

Les deux sont possibles, en supposant que le serveur unique est correctement dimensionné ou que la connectivité réseau est suffisante entre les deux serveurs.

SQL à distance exige le coût initial et opérationnel d’un serveur supplémentaire, mais cette pratique est courante chez la majorité des clients à grande échelle. Cette configuration présentent les avantages suivants :

- Options de disponibilité des sites accrues, comme SQL Always On
- Possibilité d’exécuter des rapports lourds avec une surcharge moindre sur le traitement de site
- Reprise d’activité plus simple dans certaines situations
- Gestion plus facile de la sécurité
- Séparation des rôles pour la gestion de SQL, notamment avec une équipe DBA distincte

SQL colocalisé exige un seul serveur et convient généralement à la plupart des clients à petite échelle. Cette configuration présentent les avantages suivants :

- Réduction des coûts liés aux machines, aux licences et à la maintenance
- Moins de points de défaillance dans le site
- Meilleur contrôle de la planification des temps d’arrêt

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Quelle quantité de RAM dois-je allouer à SQL ?

Par défaut, SQL utilise toute la mémoire disponible sur votre serveur, au détriment éventuel du système d’exploitation et d’autres processus sur la machine. Pour éviter d’éventuels problèmes de performances, il est important d’allouer de la mémoire à SQL explicitement. Sur les serveurs de site colocalisés avec les serveurs SQL, vérifiez que le système d’exploitation dispose de suffisamment de RAM pour la mise en cache des fichiers et d’autres opérations. Veillez à ce qu’il reste suffisamment de RAM pour SMSExec et d’autres processus Configuration Manager. Quand vous exécutez SQL sur un serveur distant, vous pouvez allouer la *majorité* de la mémoire à SQL, mais pas toute. Consultez les [recommandations de dimensionnement](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) pour obtenir des conseils de départ. 

Il est préférable d’arrondir à des Go entiers l’allocation de mémoire SQL Server. De plus, comme la RAM augmente considérablement, vous pouvez laisser à SQL un pourcentage plus élevé. Par exemple, quand 256 Go ou plus de RAM sont disponibles, vous pouvez configurer SQL jusqu’à 95 %, car cela laisse quand même beaucoup de mémoire au système d’exploitation. La supervision du fichier d’échange est un bon moyen de veiller à ce que le système d’exploitation et tous les processus Configuration Manager disposent de suffisamment de mémoire.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Les cœurs ne coûtent pas cher de nos jours. Est-ce que je dois tout simplement en ajouter quelques-uns à mon serveur SQL ?

Vous risquez de rencontrer des problèmes de contention de mémoire si vous avez plus de 16 cœurs physiques et pas suffisamment de RAM sur votre serveur SQL. La charge de travail Configuration Manager fonctionne mieux avec une RAM d’au moins 3 ou 4 Go par cœur disponible pour SQL. Quand vous ajoutez des cœurs à vos serveurs SQL, n’oubliez pas d’augmenter la RAM dans des quantités proportionnelles.

### <a name="will-sql-always-on-impact-my-performance"></a>Les groupes de disponibilité SQL Always On vont-ils affecter mes performances ?

En général, SQL Always On exerce un impact négligeable sur les performances du système quand une mise en réseau suffisante est disponible entre les serveurs de réplication SQL. Les fichiers journaux de base de données *.ldf* peuvent augmenter rapidement dans un environnement SQL Always On. Toutefois, l’espace occupé par les fichiers journaux est automatiquement libéré après une sauvegarde de base de données réussie. Ajoutez un travail SQL pour que la base de données Configuration Manager effectue une sauvegarde, par exemple, toutes les 24 heures, et une sauvegarde *.ldf* toutes les six heures. Pour plus d’informations sur SQL Always On et Configuration Manager, notamment sur les stratégies de sauvegarde SQL, consultez [SQL Server Always On pour une base de données de site à haut niveau de disponibilité](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="should-i-enable-sql-compression-on-my-database"></a>Dois-je activer la compression SQL sur ma base de données ?

La compression SQL n’est pas recommandée pour la base de données Configuration Manager. Bien qu’il n’existe aucun problème fonctionnel lié à l’activation de la compression sur une base de données Configuration Manager, les résultats des tests ne montrent pas d’énormes gains de taille par rapport à l’impact potentiel assez considérable sur les performances du système.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Dois-je activer le chiffrement SQL sur ma base de données ?

Tous les secrets inclus dans la base de données Configuration Manager sont déjà stockés de manière sécurisée, mais le chiffrement SQL permet d’ajouter encore une couche de sécurité. L’activation du chiffrement sur votre base de données ne pose aucun problème fonctionnel, mais les performances peuvent subir une dégradation allant jusqu’à 25 %, selon les tables que vous choisissez de chiffrer et la version de SQL que vous utilisez. Par conséquent, chiffrez avec précaution, particulièrement dans les environnements à grande échelle. Pensez également à mettre à jour vos plans de sauvegarde et de récupération afin de vérifier que vous pouvez récupérer les données chiffrées sans difficultés.

### <a name="what-version-of-sql-should-i-run"></a>Quelle version de SQL dois-je exécuter ?

Pour les versions prises en charge de SQL, consultez [Prise en charge des versions de SQL Server](../plan-design/configs/support-for-sql-server-versions.md). Du point de vue des performances, toutes les versions prises en charge de SQL répondent aux critères de performances exigés. En revanche, SQL 2012, SQL 2016 ou les versions plus récentes ont tendance à être plus performantes que SQL 2014 pour certains aspects de la charge de travail Configuration Manager. De plus, l’exécution de SQL 2014 au niveau de compatibilité SQL 2012 (110) améliore les performances en général. Au moment de l’installation, les bases de données Configuration Manager en cours d’exécution sur SQL 2012 et SQL 2014 sont définies au niveau de compatibilité 110. SQL 2016 ou les versions plus récentes sont définies au niveau de compatibilité par défaut de cette version de SQL, notamment 130 pour SQL 2016. La mise à niveau de SQL en place ne met pas à jour les niveaux de compatibilité tant que vous n’installez pas la version Current Branch majeure de Configuration Manager suivante. 

Si vous constatez des délais d’attente ou une lenteur inhabituels sur certaines requêtes SQL sur SQL 2016 ou version ultérieure, notamment quand vous utilisez RBAC dans la console d’administration, essayez de remplacer le niveau de compatibilité SQL sur la base de données Configuration Manager par 110. L’exécution au niveau de compatibilité SQL 110 sur SQL 2014 et des versions plus récentes de SQL est entièrement prise en charge. Pour plus d’informations, consultez [Expiration de la requête SQL ou console lente sur certaines requêtes de base de données Configuration Manager](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

Depuis janvier 2018, vous devez *éviter* les versions suivantes de SQL, en raison de divers problèmes liés aux performances ou autres connus :

- SQL 2012 SP3 CU1 à CU5
- SQL 2014 SP1 CU6 à SP2 CU2
- SQL 2016 RTM à CU3, SP1 CU3 à CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Dois-je implémenter des tâches d’indexation SQL supplémentaires ?

Oui, mettez à jour les index aussi souvent qu’une fois par semaine et les statistiques aussi souvent qu’une fois par jour pour améliorer les performances de SQL. Des scripts tiers et d’autres informations disponibles auprès des communautés Configuration Manager et SQL peuvent permettre d’optimiser ces tâches.

Sur les sites de grande taille, certaines tables SQL, comme CI\_CurrentComplianceStatusDetails, HinvChangeLog, peuvent être volumineuses, selon vos modèles d’utilisation. Vous aurez peut-être besoin de réduire ou modifier votre approche de maintenance pour ces tables une par une.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>À quel moment dois-je utiliser la version complète de SQL Server au lieu de SQL Express sur mes sites secondaires ?

SQL Express n’a aucune incidence significative sur les performances des sites secondaires et convient à la plupart des clients. Il est par ailleurs facile à déployer et à gérer, et constitue la configuration recommandée pour presque tous les clients, quelle que soit leur taille.

Toutefois, il existe une situation dans laquelle une installation complète de SQL Server peut être nécessaire. Si vous avez un grand nombre de points de distribution et de packages ou sources dans votre environnement, il est possible de dépasser la limite de taille de 10 Go de SQL Express. Si le nombre de packages multiplié par le nombre de points de distribution donne un résultat supérieur à 4 000 000, notamment 2 000 points de distribution avec 2 000 éléments de contenu, envisagez d’utiliser la version complète de SQL Server sur vos sites secondaires. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Dois-je modifier les paramètres MaxDOP sur ma base de données ?

Garder la valeur 0 de votre paramètre (utiliser tous les processeurs disponibles) correspond au réglage optimal pour des performances de traitement globales dans la plupart des cas.

De nombreux administrateurs Configuration Manager suivent les [recommandations et conseils liés à l’option de configuration « Degré maximal de parallélisme » dans SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Sur la plupart des gros matériels modernes, ces conseils suggèrent un paramètre maximal s’élevant à huit. Toutefois, si vous exécutez de nombreuses requêtes plus petites par rapport à votre nombre de processeurs, il peut s’avérer utile de définir un nombre plus élevé. Vous limiter à huit n’est pas nécessairement le meilleur choix sur des sites plus grands quand d’autres cœurs sont disponibles. 

Sur les serveurs SQL dotés de plus de huit cœurs, commencez avec un paramètre défini sur 0 et apportez uniquement des modifications si vous rencontrez des problèmes de performances ou de verrouillage excessif. Si vous avez besoin de modifier MaxDOP parce que vous rencontrez des problèmes de performances avec le paramètre 0, commencez avec une nouvelle valeur au moins égale ou supérieure au nombre minimal de cœurs recommandé pour le dimensionnement du serveur SQL de ce site. Utiliser une valeur inférieure exerce presque toujours un effet négatif sur les performances. Par exemple, un serveur SQL distant a besoin d’au moins 12 cœurs pour un site de 100 000 clients. Si votre serveur SQL a 16 cœurs, commencez par tester votre paramètre MaxDOP avec la valeur 12.

## <a name="other-common-performance-related-questions"></a>Autres questions fréquentes liées aux performances

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Quels dossiers du serveur de site (ou d’autres rôles) dois-je exclure pour les logiciels antivirus ?

Soyez prudent quand vous désactivez la protection antivirus sur un système. Dans les environnements sécurisés à gros volume, nous recommandons de désactiver la *supervision active* pour optimiser les performances.

Pour plus d’informations sur les exclusions d’antivirus recommandées, consultez [Exclusions d’antivirus recommandées pour Configuration Manager 2012 et les serveurs de site, systèmes de site et clients Current Branch](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Que puis-je faire pour améliorer les performances de WSUS utilisé avec Configuration Manager ?

La modification de quelques paramètres IIS clés, comme la longueur de file d’attente WsusPool et la limite de la mémoire privée WsusPool, peut améliorer les performances de WSUS, même sur des installations plus petites. Pour plus d’informations, consultez [Matériel recommandé](../plan-design/configs/recommended-hardware.md).

Vérifiez également que vous avez les dernières mises à jour installées pour le système d’exploitation exécutant WSUS :

- Windows Server 2012 : toutes les mises à jour cumulatives autre que les mises à jour de « sécurité uniquement » publiées depuis octobre 2017. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2 : toutes les mises à jour cumulatives autre que les mises à jour de « sécurité uniquement » publiées depuis août 2017. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016 : toutes les mises à jour cumulatives autre que les mises à jour de « sécurité uniquement » publiées depuis août 2017. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Quel type de maintenance dois-je exécuter sur mes serveurs WSUS ?

Consultez [Le guide complet de la maintenance de Microsoft WSUS et de Configuration Manager SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Je veux configurer une supervision des performances de base pour mon site. Que dois-je surveiller ?

La supervision traditionnelle des performances de serveur est globalement efficace pour Configuration Manager. Vous pouvez également exploiter divers packs d’administration System Center Operations Manager pour Configuration Manager, SQL Server et Windows Server pour superviser l’intégrité de base de vos serveurs. Vous pouvez également directement superviser les compteurs Analyseur de performances Windows (PerfMon) fournis par Configuration Manager. Supervisez les backlogs dans les diverses boîtes de réception pour détecter les premiers signes d’éventuels backlogs ou problèmes de performances de site.

## <a name="see-also"></a>Voir aussi

- [Recommandations pour le dimensionnement et les performances des sites](../plan-design/configs/site-size-performance-guidelines.md)
- [Questions fréquentes (FAQ) sur Configuration Manager dans Azure](configuration-manager-on-azure.md)
