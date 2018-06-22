---
title: Présentation d’Asset Intelligence
titleSuffix: Configuration Manager
description: Obtenez une présentation d’Asset Intelligence dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0c09160e88d8a713caadfdd9a6973fd436b4cad1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340792"
---
# <a name="introduction-to-asset-intelligence-in-system-center-configuration-manager"></a>Présentation d’Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Asset Intelligence dans System Center Configuration Manager permet d’inventorier et de gérer l’utilisation des licences logicielles dans l’entreprise en utilisant le catalogue Asset Intelligence. De nombreuses classes WMI (Windows Management Instrumentation) d’inventaire matériel améliorent l’éventail des informations collectées sur le matériel et les noms de logiciels en cours d’utilisation. Ces informations sont présentées dans plus de 60 rapports dans un format pratique. La plupart de ces rapports renvoient vers des rapports plus spécifiques qui permettent de rechercher des informations générales et d'accéder à des informations plus détaillées. Vous pouvez ajouter des informations personnalisées dans le catalogue Asset Intelligence, telles que des catégories de logiciels, des familles de logiciels, des légendes logicielles et des configurations matérielles requises personnalisées. En outre, les clients peuvent se connecter à System Center Online pour mettre à jour dynamiquement le catalogue Asset Intelligence avec les dernières informations disponibles. Les clients Microsoft peuvent également rapprocher l’utilisation des licences logicielles de l’entreprise avec les licences logicielles achetées en cours d’utilisation en important les informations de licence logicielle dans la base de données du site Configuration Manager.  

##  <a name="BKMK_AssetIntelligenceCatalog"></a> Catalogue Asset Intelligence  

 Le catalogue Asset Intelligence Configuration Manager est un ensemble de tables stockées dans la base de données de site qui contiennent les informations de catégorisation et d’identification de plus de 300 000 titres et versions de logiciels. Ces tables de base de données sont également utilisées pour gérer les configurations matérielles requises des titres de logiciels.  

 Le catalogue Asset Intelligence fournit des informations sur les licences des logiciels utilisés, Microsoft et non-Microsoft. Un ensemble prédéfini de configurations matérielles requises pour les titres de logiciels figure dans le catalogue Asset Intelligence et vous pouvez créer des informations de configuration matérielle requise définies par l'utilisateur en fonction de vos besoins. En outre, vous pouvez personnaliser les informations dans le catalogue Asset Intelligence et envoyer les informations de titres de logiciels à System Center Online pour les catégoriser.  

 Des mises à jour en bloc du catalogue Asset Intelligence qui contiennent les nouvelles versions des logiciels sont régulièrement téléchargeables. Ou bien, vous pouvez mettre à jour le catalogue de façon dynamique en utilisant le rôle de système de site du point de synchronisation Asset Intelligence.  

###  <a name="BKMK_SoftwareCategories"></a> Catégories de logiciels  
 Les catégories de logiciels Asset Intelligence permettent de catégoriser de façon large les titres de logiciels inventoriés et comme regroupements généraux de familles de logiciels plus spécifiques. Par exemple, « Société d'énergie » peut correspondre à une catégorie de logiciels, et « Pétrole », « Gaz » ou « Hydroélectrique » peuvent correspondre à des familles de logiciels dans cette catégorie. La plupart des catégories de logiciels sont prédéfinies dans le catalogue Asset Intelligence, et vous pouvez créer des catégories définies par l'utilisateur pour spécifier plus précisément les logiciels inventoriés. L'état de validation de toutes les catégories de logiciels prédéfinies est toujours **Validé**, alors que les informations de catégories de logiciels personnalisées ajoutées au catalogue Asset Intelligence ont l'état **Défini par l'utilisateur** Pour plus d’informations sur la gestion des catégories de logiciels, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Les informations de catégories de logiciels prédéfinies stockées dans le catalogue Asset Intelligence sont accessibles en lecture seule et ne peuvent pas être modifiées ni supprimées. Les utilisateurs administratifs peuvent ajouter, modifier ou supprimer des catégories de logiciels définies par l'utilisateur.  

###  <a name="BKMK_SoftwareFamilies"></a> Familles de logiciels  
 Les familles de logiciels Asset Intelligence permettent de définir les titres de logiciels dans les catégories de logiciels. La plupart des familles de logiciels sont prédéfinies dans le catalogue Asset Intelligence, et vous pouvez créer des catégories définies par l'utilisateur pour définir plus précisément les logiciels inventoriés. L'état de validation de toutes les familles de logiciels prédéfinies est toujours **Validé**, alors que les informations de familles de logiciels personnalisées ajoutées au catalogue Asset Intelligence ont l'état **Défini par l'utilisateur** Pour plus d’informations sur la gestion des familles de logiciels, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Les informations sur les familles de logiciels prédéfinies sont accessibles en lecture seule et ne peuvent pas être modifiées. Les utilisateurs administratifs peuvent ajouter, modifier ou supprimer des familles de logiciels définies par l'utilisateur.  

###  <a name="BKMK_CustomLabels"></a> Légendes logicielles  
 Les légendes logicielles personnalisées Asset Intelligence permettent de créer des filtres que vous pouvez utiliser pour regrouper des titres de logiciels et les afficher en utilisant des rapports Asset Intelligence. Vous pouvez utiliser des légendes logicielles pour créer des groupes de titres de logiciels ayant un attribut commun. Par exemple, vous pouvez créer la légende logicielle « Logiciel à contribution volontaire », associer la légende aux titres de logiciels à contribution volontaire et exécuter un rapport pour afficher tous les titres de logiciels avec la légende Logiciel à contribution volontaire. Les légendes logicielles ne sont pas prédéfinies. L'état de validation des légendes logicielles est toujours **Défini par l'utilisateur**. Pour plus d’informations sur la gestion des légendes logicielles, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

###  <a name="BKMK_HardwareRequirements"></a> Configuration matérielle requise  
 Vous pouvez utiliser les informations de configuration de matériel requise pour vérifier que les ordinateurs répondent à la configuration matérielle requise pour les titres de logiciels avant d'y déployer des logiciels. Vous pouvez gérer les configurations matérielles requises pour les titres de logiciels dans l'espace de travail **Biens et conformité** dans le noeud **Configuration matérielle requise** sous le noeud **Asset Intelligence** . La plupart des configurations matérielles requises sont prédéfinies dans le catalogue Asset Intelligence et vous pouvez créer des informations de configuration matérielle définies par l'utilisateur pour répondre à des besoins spécifiques. L'état de validation de toutes les configurations matérielles requises prédéfinies est toujours **Validé**, tandis que celui des informations de configuration matérielle requise définies par l'utilisateur ajoutées au catalogue Asset Intelligence est **Défini par l'utilisateur**. Pour plus d’informations sur la gestion de la configuration matérielle requise, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

> [!NOTE]  
>  Les informations de configuration matérielle requise figurant dans la console Configuration Manager sont tirées du catalogue Asset Intelligence et elles ne reposent pas sur les informations de titres de logiciels inventoriés sur les clients System Center 2012 Configuration Manager. Les informations de configuration matérielle requise ne sont pas mises à jour au cours de la synchronisation avec System Center Online. Vous pouvez créer une configuration matérielle requise définie par l'utilisateur pour le logiciel inventorié n'ayant pas de configuration matérielle.  

 Les informations suivantes s'affichent pour chaque configuration matérielle requise répertoriée :  

-   **Nom du logiciel**: spécifie le titre du logiciel associé à la configuration matérielle requise.  

-   **Vitesse min. du processeur (MHz)**: spécifie la vitesse minimale du processeur, en mégahertz (MHz), nécessaire au logiciel.  

-   **Mémoire RAM minimum (Ko)**: spécifie la quantité de mémoire vive minimale en kilo-octets (Ko) nécessaire au logiciel.  

-   **Espace disque minimum (Ko)**: spécifie l’espace disque libre minimal en Ko nécessaire au logiciel.  

-   **Taille minimale du disque (Ko)**: spécifie l’espace disque libre minimal en Ko nécessaire au logiciel.  

-   **État de validation**: spécifie l’état de validation de la configuration matérielle requise.  

 Les configurations matérielles requises prédéfinies stockées dans le catalogue Asset Intelligence sont accessibles en lecture seule et ne peuvent pas être supprimées.  Les utilisateurs administratifs peuvent ajouter, modifier ou supprimer des configurations matérielles définies par l'utilisateur pour les titres de logiciels qui ne sont pas stockés dans le catalogue Asset Intelligence.  

##  <a name="BKMK_InventoriedSoftwareTitles"></a> Logiciels inventoriés  
 Vous pouvez afficher les informations de titres de logiciels inventoriés dans l'espace de travail **Biens et conformité** dans le noeud **Logiciels inventoriés** sous le noeud **Asset Intelligence** . L’agent du client d’inventaire matériel collecte les informations des logiciels inventoriés à partir des clients Configuration Manager en fonction des titres de logiciels stockés dans le catalogue Asset Intelligence.  

> [!WARNING]  
>  L'agent du client d'inventaire matériel collecte l'inventaire en fonction des classes de création de rapports d'inventaire matériel Asset Intelligence que vous activez. Pour plus d’informations sur l’activation des classes de création de rapports, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Par défaut, les informations suivantes s'affichent pour chaque titre de logiciel inventorié :  

-   **Nom**: spécifie le nom du logiciel inventorié.  

-   **Fournisseur**: spécifie le nom du fournisseur qui a développé le logiciel inventorié.  

-   **Version**: indique la version du produit du logiciel inventorié.  

-   **Catégorie**: spécifie la catégorie actuellement affectée au logiciel inventorié.  

-   **Famille**: spécifie la famille actuellement affectée au logiciel inventorié.  

-   **Légende** [**1**, **2**et **3**] : spécifie les légendes personnalisées associées au logiciel. Les titres de logiciels inventoriés peuvent avoir jusqu'à trois légendes personnalisées.  

-   **Nombre** : spécifie le nombre de clients Configuration Manager qui ont inventorié le logiciel.  

-   **État**: spécifie l’état de validation du logiciel inventorié.  

> [!NOTE]  
>  Vous pouvez modifier les informations de catégorisation (nom du produit, fournisseur, catégorie et famille) des logiciels inventoriés uniquement sur le site de niveau supérieur de votre hiérarchie. Lorsque vous modifiez les informations de catégorisation des logiciels prédéfinis, l'état de validation **Validé** des logiciels devient **Défini par l'utilisateur**.  

##  <a name="AssetIntelligenceSycnronizationPoint"></a> Point de synchronisation Asset Intelligence  
 Le point de synchronisation Asset Intelligence est un rôle système de site Configuration Manager utilisé pour établir une connexion à System Center Online (via le port TCP 443) pour gérer les mises à jour dynamiques des informations du catalogue Asset Intelligence. Ce rôle de site peut être installé uniquement sur le site de niveau supérieur de la hiérarchie. Vous devez configurer toutes les personnalisations de catalogue Asset Intelligence en utilisant une console Configuration Manager connectée au site de niveau supérieur. Même si toutes les mises à jour doivent être configurées sur le site de niveau supérieur, les informations de catalogue Asset Intelligence sont répliquées sur les autres sites de la hiérarchie. Le rôle de site du point de synchronisation Asset Intelligence permet de synchroniser le catalogue à la demande avec System Center Online ou de planifier la synchronisation automatique du catalogue. Outre le téléchargement des nouvelles informations du catalogue Asset Intelligence, le point de synchronisation Asset Intelligence peut envoyer les informations de titres de logiciels personnalisés à System Center Online à des fins de catégorisation. Microsoft considère tous les titres de logiciels envoyés à System Center Online pour être catégorisés comme des informations publiques. Ainsi, vous devez vérifier que vos titres de logiciels personnalisés ne contiennent pas d’informations confidentielles ou propriétaires.  

> [!NOTE]  
>  Lorsque vous envoyez un titre de logiciel non catégorisé et qu'au moins quatre clients ont demandé la catégorisation du titre, les programmes de recherche System Center Online identifient et catégorisent les informations du titre logiciel et rendent les informations de catégorisation accessibles à tous les clients qui utilisent le service en ligne. Les titres de logiciels ayant le plus grand nombre de demandes de catégorisation sont affectés de la priorité de catégorisation la plus élevée. Les logiciels personnalisés et les applications métier sont peu susceptibles de recevoir une catégorie, et nous vous conseillons de ne pas envoyer ces logiciels à Microsoft pour catégorisation.  

> [!NOTE]  
>  Le rôle de système de site du point de synchronisation Asset Intelligence est nécessaire pour se connecter System Center Online. Pour plus d’informations sur l’installation d’un point de synchronisation Asset Intelligence, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

##  <a name="BKMK_AssetIntelligenceHomePage"></a> Page d’accueil d’Asset Intelligence  
 Le nœud **Asset Intelligence** dans l’espace de travail **Biens et conformité** est la page d’accueil d’Asset Intelligence dans Configuration Manager. La page d'accueil d' **Asset Intelligence** contient une vue de tableau de bord récapitulant les informations du catalogue Asset Intelligence.  

> [!NOTE]  
>  La page d'accueil d' **Asset Intelligence** n'est pas automatiquement actualisée lorsqu'elle s'affiche.  

 La page d'accueil **Asset Intelligence** contient les sections suivantes :  

-   **Synchronisation de catalogue**: indique si Asset Intelligence est activé et l’état actuel du point de synchronisation Asset Intelligence. Cette section indique également la planification de la synchronisation, si la déclaration de licence du client est importée, la date de la dernière mise à jour de l’état et l’heure de la prochaine mise à jour planifiée, ainsi que le nombre de modifications effectuées après l’installation du système de site du point de synchronisation Asset Intelligence.  

    > [!NOTE]  
    >  La section de synchronisation du catalogue Asset Intelligence de la page d’accueil **Asset Intelligence** s’affiche uniquement si un rôle de système de site du point de synchronisation Asset Intelligence a été installé.  

-   **État des logiciels inventoriés**: indique le nombre et le pourcentage de logiciels, catégories de logiciels et familles de logiciels inventoriés qui sont identifiés par Microsoft, identifiés par un administrateur, en attente d’identification en ligne ou non identifiés et pas en attente. Les informations affichées dans un tableau indiquent le nombre pour chacun des éléments, tandis que les informations affichées dans le graphique indiquent le pourcentage de chacun des éléments.  

##  <a name="BKMK_AssetIntelligenceReports"></a> Rapports Asset Intelligence  
 Les rapports Asset Intelligence se trouvent dans la console Configuration Manager, dans l’espace de travail **Surveillance** dans le dossier Asset Intelligence sous le nœud **Rapports**. Les rapports fournissent des informations sur les matériels, la gestion des licences et les logiciels. Pour plus d’informations sur les rapports de Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  La précision du nombre de logiciels installés et des informations de licence affichés dans les rapports Asset Intelligence peut varier par rapport au nombre réel de logiciels installés ou de licences utilisées dans l’environnement. Cette variation est due aux dépendances et limitations complexes qu’implique l’inventaire des informations de licence des logiciels installés dans les environnements d’entreprise. N'utilisez pas les rapports Asset Intelligence comme seule source pour déterminer la conformité des licences logicielles achetées.  

###  <a name="BKMK_HardwareReports"></a> Rapports matériels Asset Intelligence  
 Les rapports matériels Asset Intelligence fournissent des informations sur les ressources matérielles de l'organisation. En utilisant les informations d’inventaire matériel, comme la vitesse, la mémoire, les périphériques, etc., les rapports matériels Asset Intelligence peuvent contenir des informations sur les appareils USB, le matériel à mettre à niveau et même les ordinateurs qui ne sont pas prêts à recevoir une mise à niveau logicielle donnée.  

> [!NOTE]  
>  Certaines données utilisateur dans les rapports Asset Intelligence sont collectées depuis le journal des événements de la sécurité du système. Pour améliorer l’exactitude des rapports, il est recommandé de nettoyer ce journal quand vous réaffectez un ordinateur à un autre utilisateur.  

###  <a name="BKMK_LicenseManagementReports"></a> Rapports de gestion de licences Asset Intelligence  
 Les rapports de gestion des licences Asset Intelligence fournissent des données sur les licences en cours d’utilisation. Le rapport Grand livre des licences répertorie les applications Microsoft installées dans un format semblable à un relevé de licences Microsoft. Il fournit une méthode pratique de mise en correspondance des licences achetées et des licences utilisées. D’autres rapports de gestion des licences fournissent des informations sur les ordinateurs faisant office de serveurs exécutant le Service de gestion de clés (KMS) pour les statistiques d’activation du système d’exploitation.  

> [!IMPORTANT]  
>  Plusieurs rapports de gestion des licences Asset Intelligence présentent des informations sur la fonction du Service de gestion de clés, une méthode d'administration des licences en volume. Si aucun serveur KMS n'a été implémenté, certains rapports ne contiendront aucune donnée. Pour plus d'informations sur KMS, recherchez KMS sur [Microsoft TechNet](http://go.microsoft.com/fwlink/?linkid=3225).  

###  <a name="BKMK_SoftwareReports"></a> Rapports logiciels Asset Intelligence  
 Les rapports logiciels Asset Intelligence fournissent des informations sur les familles de logiciels, les catégories et les titres de logiciels qui sont installés sur les ordinateurs de l'organisation. Ils contiennent, entre autres, des informations sur les objets Application d'assistance du navigateur et les logiciels qui démarrent automatiquement. Ces rapports peuvent permettre d'identifier les logiciels de publicité, les logiciels espions et d'autres programmes malveillants, ainsi que les redondances logicielles afin de rationaliser l'achat et le support des logiciels.  

###  <a name="BKMK_SoftwareIdTagReports"></a> Rapports sur les balises d’identification logicielle Asset Intelligence  
 Rapports de balise d'identification de logiciels Asset Intelligence fournissent des informations sur les logiciels qui contient une balise d'identification logicielle conforme à ISO/IEC 19770-2. Ces balises d’identification logicielle fournissent des informations faisant autorité servant à identifier les logiciels installés. Quand vous activez la classe de rapport d’inventaire matériel SMS_SoftwareTag, Configuration Manager collecte des informations sur les logiciels dotés de balises d’identification logicielle. Les rapports suivants fournissent des informations sur les logiciels :  

-   **Logiciels 14A - Recherche de logiciels dont la balise d’identification logicielle est activée** : ce rapport indique le nombre de logiciels installés qui ont une balise d’identification logicielle activée.  

-   **Logiciels 14B - Ordinateurs sur lesquels sont installés des logiciels ayant une balise d’identification logicielle spécifique activée** : ce rapport répertorie tous les ordinateurs qui ont installé des logiciels dotés d’une balise d’identification logicielle spécifique activée.  

-   **Logiciels 14C - Balise d’identification logicielle installée activée sur un ordinateur spécifique** : ce rapport répertorie tous les logiciels installés dotés d’une balise d’identification logicielle spécifique activée sur un ordinateur spécifique.  

###  <a name="BKMK_ReportingLImitations"></a> Limites des rapports Asset Intelligence  
 Les rapports Asset Intelligence peuvent fournir une grande quantité d'informations sur les titres de logiciels installés et les licences logicielles achetées en cours d'utilisation. Toutefois, n'utilisez pas ces informations comme seule source pour déterminer la conformité des licence logicielles achetées.  

####  <a name="BKMK_ExampleDependencies"></a> Exemples de dépendances  
 La précision de la quantité affichée dans les rapports Asset Intelligence installé les logiciels et les informations de licence peuvent varier des quantités réelles actuellement utilisées. Cette variation est due aux dépendances complexes qu’implique l’inventaire des informations de licence des logiciels en cours d’utilisation dans les environnements d’entreprise. Les exemples suivants montrent les dépendances liées à l’inventaire des logiciels installés dans l’entreprise en utilisant Asset Intelligence, qui sont susceptibles d’affecter l’exactitude des rapports Asset Intelligence :  

 **Dépendances d'inventaire matériel sur les clients**  
 Les rapports Asset Intelligence des logiciels installés sont basés sur les données collectées sur les clients Configuration Manager en étendant l’inventaire matériel afin d’activer la création de rapports Asset Intelligence. En raison de ces dépendances par rapport à la création de rapports d’inventaire matériel, les rapports Asset Intelligence contiennent uniquement les données des clients Configuration Manager qui ont terminé le processus d’inventaire matériel avec les classes de rapport Asset Intelligence WMI requises activées. En outre, puisque les clients Configuration Manager exécutent les processus d’inventaire matériel selon un calendrier défini par l’utilisateur administratif, il peut exister un décalage au niveau des rapports de données, qui affecte l’exactitude des rapports Asset Intelligence. Par exemple, un logiciel sous licence inventorié peut être désinstallé après que le client a terminé un cycle d’inventaire matériel. Toutefois, le logiciel apparaît comme étant installé dans les rapports Asset Intelligence jusqu’au prochain cycle de rapports d’inventaire matériel du client.  

 **Dépendances de package de logiciel**  
 Étant donné que les rapports Asset Intelligence reposent sur les données des logiciels installés collectées en utilisant des processus standard d’inventaire matériel de client Configuration Manager, certaines données de logiciels peuvent ne pas être collectées correctement. Par exemple, les installations logicielles non conformes aux processus d’installation standard ou modifiées avant l’installation peuvent générer des rapports Asset Intelligence inexacts.  

####  <a name="BKMK_LegalLimitations"></a> Limitations légales  
 Les informations affichées dans les rapports Asset Intelligence sont soumises à de nombreuses limitations. Ces informations ne représentent pas un avis juridique, comptable ou professionnel. Les informations fournies par les rapports Asset Intelligence sont données à titre indicatif et ne doivent pas être utilisées dans le seul but de déterminer la conformité des licences d’utilisation de logiciels.  

 Les exemples de limitations suivants sont impliqués dans le processus d'inventaire des logiciels installés et des licences utilisant Asset Intelligence dans l'entreprise et susceptibles d'affecter la précision des rapports Asset Intelligence :  

 **Limitations quantitatives de l'utilisation des licences Microsoft**  
 -   La quantité de licences logicielles Microsoft achetées est déterminée à partir des informations fournies par les administrateurs et elle doit être examinée en détail afin de garantir que le nombre correct de licences d'utilisation de logiciels est indiqué.  

-   La quantité indiquée de licences logicielles Microsoft révèle des informations qui ne concernent que les licences logicielles Microsoft achetées via les programmes de licences en volume et ne reflète pas d’informations relatives aux licences logicielles acquises auprès d’un revendeur, d’un fabricant d’ordinateurs OEM ou d’un autre point de vente de licences d’utilisation de logiciels.  

-   Les licences logicielles acquises au cours des 45 derniers jours peuvent ne pas figurer dans la liste des licences logicielles Microsoft fournie, selon les besoins et calendriers des rapports du revendeur de logiciels.  

-   Les transferts de licences logicielles résultant des fusions ou rachats d'entreprises, peuvent ne pas être inclus dans le nombre de licences logicielles Microsoft.  

-   Les conditions non standard d'un contrat de licences en volume Microsoft (MVLS) peuvent affecter le nombre de licences logicielles indiqué, et ainsi nécessiter une analyse supplémentaire par un représentant Microsoft.  

 **Limitations quantitatives des logiciels installés**  
 Les clients Configuration Manager doivent terminer correctement les cycles de diffusion d’inventaire matériel pour que les rapports Asset Intelligence reflètent précisément la quantité de logiciels installés. En outre, il peut y avoir un décalage entre l’installation ou la désinstallation d’un logiciel sous licence après un cycle de diffusion d’inventaire matériel réussi. Ce décalage ne sera pas indiqué dans les rapports Asset Intelligence avant le prochain cycle de diffusion d’inventaire matériel.  

 **Limitations relatives au rapprochement des licences**  
 Le rapprochement entre le nombre de logiciels installés et le nombre de licences logicielles achetées est calculé en comparant le nombre de licences spécifié par l’administrateur et le nombre de logiciels installés collectés lors des inventaires matériels du client Configuration Manager en fonction du calendrier défini par l’administrateur. Cette comparaison ne constitue pas l'avis final de Microsoft concernant les licences. L'avis concernant les licences dépend en réalité de chaque nom de licence d'utilisation de logiciel et des droits d'utilisation accordés par le contrat de licence.  

##  <a name="BKMK_ValidationStates"></a> États de validation Asset Intelligence  
 Les états de validation Asset Intelligence représentent les états de validation actuels sources des informations du catalogue Asset Intelligence. Le tableau suivant présente les états de validation possibles d'Asset Intelligence et les actions de l'administrateur susceptibles de les déclencher.  

|**État**|**Définition**|**Action de l'administrateur**|**Commentaireaire**|  
|---------------|--------------------|------------------------------|-----------------|  
|**Validé**|L’élément du catalogue a été défini par les fonctions de recherche de System Center Online.|aucune.|Meilleur état.|  
|**Défini par l'utilisateur**|L'élément du catalogue n'a pas été défini par les fonctions de recherche de System Center Online.|Personnaliser les informations du catalogue en local.|Cet état est affiché dans les rapports Asset Intelligence.|  
|**En attente**|L’élément du catalogue n’a pas été défini par les fonctions de recherche de System Center Online, mais il a été soumis à System Center Online en vue d’une catégorisation.|Demander la catégorisation depuis System Center Online.|L'élément du catalogue conserve cet état jusqu'à ce que les fonctions de recherche de System Center Online classe l'élément dans une catégorie et le catalogue Asset Intelligence est synchronisé.|  
|**Peut être mis à jour**|Un élément du catalogue défini par un utilisateur a été catégorisé différemment par System Center Online lors de la synchronisation de catalogue suivante.|Personnaliser le catalogue Asset Intelligence local afin de classer un élément comme étant défini par un utilisateur.|Vous pouvez exécuter l'action Résoudre le conflit pour décider si vous allez utiliser les nouvelles informations de catégorisation ou la précédente valeur définie par l'utilisateur. Pour plus d’informations sur la résolution des conflits, consultez [Opérations pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  
|**Sans catégorie**|L'élément du catalogue n'a pas été défini par les fonctions de recherche de System Center Online, il n'a pas été soumis à System Center Online pour la catégorisation et l'administrateur n'a pas attribué une valeur de catégorisation définie par l'utilisateur.|aucune.|Nécessite une catégorisation ou la personnalisation des informations du catalogue local.<br /><br /> Pour plus d’informations sur la demande de catégorisation, consultez [Opérations pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).<br /><br /> Pour plus d’informations sur la modification de la catégorie du logiciel, consultez [Opérations pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md).|  

> [!NOTE]  
>  L'état de validation des éléments de catalogue soumis à System Center Online à des fins de catégorisation est **En attente** sur un site d'administration centrale mais sur les sites principaux enfant, l'état de validation affiché pour ces éléments continue d'être **Sans catégorie** .  

> [!NOTE]  
>  À l’issue de la résolution d’un conflit de catégorisation, l’élément n’est plus validé comme étant un élément en conflit sauf si des mises à jour de catégorisation ultérieures apportent de nouvelles informations sur cet élément.  

 Pour obtenir des exemples du moment où un état de validation peut passer à un autre état, consultez [Exemples de transitions d’état de validation pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence.md).  
