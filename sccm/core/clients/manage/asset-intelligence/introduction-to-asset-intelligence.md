---
title: Présentation d’Asset Intelligence
titleSuffix: Configuration Manager
description: Utiliser Asset Intelligence dans Configuration Manager pour inventorier et gérer l'utilisation des licences logicielles dans toute l'entreprise.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0bdfdef5-390f-4099-8bde-de51d9a89175
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf0d222c005da2b7d5b577ebdec64cd64eba536c
ms.sourcegitcommit: 4659946369d5352234f27c7682bce65a0e86c697
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/12/2018
ms.locfileid: "53303922"
---
# <a name="introduction-to-asset-intelligence-in-configuration-manager"></a>Présentation d'Asset Intelligence dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Inventoriez et gérez l'utilisation des licences logicielles dans l'entreprise en utilisant le catalogue Asset Intelligence. Asset Intelligence ajoute des classes d’inventaire matériel afin de développer l’éventail d’informations qui sont collectées par Configuration Manager. Ces informations regroupent les titres matériels et logiciels utilisés dans votre environnement. Ces informations sont présentées dans plus de 60 rapports au format pratique. La plupart de ces rapports renvoient vers des rapports plus spécifiques. Recherchez des informations générales et accédez à des informations plus détaillées. 

Ajoutez des informations personnalisées dans le catalogue Asset Intelligence. Il peut s’agir de catégories de logiciels, de familles de logiciels, de légendes logicielles et d’exigences matérielles personnalisées. Pour mettre à jour dynamiquement le catalogue Asset Intelligence avec les dernières informations disponibles, connectez-le à Microsoft Cloud. 

Utilisez Asset Intelligence pour faciliter le rapprochement de l’utilisation des licences logicielles de l’entreprise. Importez les informations de licence logicielle dans la base de données du site Configuration Manager pour les afficher à propos des logiciels en cours d’utilisation.  



## <a name="BKMK_AssetIntelligenceCatalog"></a> Catalogue Asset Intelligence  

Le catalogue Asset Intelligence est constitué d’un ensemble de tables de données qui sont stockées dans la base de données de site. Ces tables contiennent les informations de catégorisation et d’identification de plus de 300 000 titres et versions de logiciels. Elles sont également utilisées pour gérer les exigences matérielles pour des titres de logiciels spécifiques.  

Asset Intelligence fournit des informations sur les licences des logiciels utilisés, Microsoft et non-Microsoft. Un ensemble prédéfini de configurations matérielles requises pour les titres de logiciels figure dans le catalogue Asset Intelligence et vous pouvez créer des informations de configuration matérielle requise définies par l'utilisateur en fonction de vos besoins. Vous pouvez également personnaliser les informations du catalogue Asset Intelligence et importer des informations de titres de logiciels dans Microsoft Cloud pour les catégoriser.  

Des mises à jour en bloc du catalogue Asset Intelligence contenant les logiciels dernièrement sortis sont régulièrement téléchargeables. Vous pouvez également mettre à jour le catalogue de façon dynamique en utilisant le point de synchronisation Asset Intelligence.  


### <a name="BKMK_SoftwareCategories"></a> Catégories de logiciels  

Les catégories de logiciels Asset Intelligence permettent de catégoriser de façon large les titres de logiciels inventoriés et sous forme de regroupements généraux de familles de logiciels plus spécifiques. Par exemple, « Société d'énergie » peut correspondre à une catégorie de logiciels, et « Pétrole », « Gaz » ou « Hydroélectrique » peuvent correspondre à des familles de logiciels dans cette catégorie. De nombreuses catégories de logiciels sont prédéfinies dans le catalogue Asset Intelligence. Vous pouvez créer des catégories définies par l’utilisateur pour définir plus précisément des logiciels inventoriés. L'état de validation pour toutes les catégories prédéfinies de logiciels est toujours **Validé**. Les informations sur les catégories personnalisées de logiciels qui sont ajoutées au catalogue Asset Intelligence sont **Définies par l’utilisateur**. 

Pour plus d’informations sur la gestion des catégories de logiciels, consultez la page [Configuration d’Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

> [!NOTE]  
> Les informations de catégories prédéfinies de logiciels qui sont stockées dans le catalogue Asset Intelligence sont accessibles en lecture seule. Vous ne pouvez pas les modifier ni les supprimer. Les utilisateurs administratifs peuvent ajouter, modifier ou supprimer des catégories de logiciels définies par l'utilisateur.  


### <a name="BKMK_SoftwareFamilies"></a> Familles de logiciels  

Les familles de logiciels Asset Intelligence permettent de définir les titres de logiciels inventoriés dans les catégories de logiciels. De nombreuses familles de logiciels sont prédéfinies dans le catalogue Asset Intelligence. Vous pouvez créer des catégories définies par l’utilisateur pour définir plus précisément des logiciels inventoriés. L'état de validation pour toutes les familles prédéfinies de logiciels est toujours **Validé**. Les informations sur les familles personnalisées de logiciels qui sont ajoutées au catalogue Asset Intelligence sont **Définies par l’utilisateur**. 

Pour plus d’informations sur la gestion des familles de logiciels, consultez la page [Configuration d’Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

> [!NOTE]  
> Les informations sur les familles prédéfinies de logiciels sont accessibles en lecture seule et ne peuvent pas être modifiées. Les utilisateurs administratifs peuvent ajouter, modifier ou supprimer des familles de logiciels définies par l'utilisateur.  


### <a name="BKMK_CustomLabels"></a> Légendes logicielles  

Les légendes logicielles personnalisées Asset Intelligence vous permettent de créer des filtres pour regrouper des titres de logiciels et les afficher en utilisant des rapports Asset Intelligence. Utiliser les légendes logicielles pour créer des groupes de titres de logiciels ayant un attribut commun. Par exemple, vous pouvez créer la légende logicielle « Logiciel à contribution volontaire », l’associer aux titres de logiciels du même type qui sont inventoriés et exécuter un rapport pour afficher tous les titres de logiciels portant cette légende. Il n’existe aucune légende prédéfinie. L'état de validation des légendes logicielles est toujours **Défini par l'utilisateur**. 

Pour plus d’informations sur la gestion des légendes de logiciels, consultez la page [Configuration d’Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  


### <a name="BKMK_HardwareRequirements"></a> Configuration matérielle requise  

Utilisez les informations de configuration matérielle requise pour vérifier que les ordinateurs répondent aux exigences matérielles pour les titres de logiciels avant tout déploiement. Gérez les exigences matérielles pour les titres de logiciels dans l'espace de travail **Biens et conformité** du nœud **Configuration matérielle requise** qui se trouve sous le nœud **Asset Intelligence**. 

De nombreuses exigences matérielles sont prédéfinies dans le catalogue Asset Intelligence. Créez de nouvelles informations relatives à la configuration matérielle requise définies par l’utilisateur pour répondre à des besoins spécifiques. L'état de validation des exigences matérielles prédéfinies est toujours **Validé**. Les informations sur les exigences matérielles que l’utilisateur définit et ajoute au catalogue Asset Intelligence sont **Définies par l’utilisateur**. 

Pour plus d’informations sur la gestion des exigences matérielles, consultez la page [Configuration d’Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

> [!NOTE]  
> Les exigences matérielles affichées dans la console Configuration Manager sont récupérées à partir du catalogue Asset Intelligence. Elles ne s’appuient pas sur les informations de titres de logiciels inventoriés à partir de clients. 
> 
> Les informations de configuration matérielle requise ne sont pas mises à jour au cours de la synchronisation avec Microsoft. 
> 
> Vous pouvez créer une configuration matérielle requise définie par l'utilisateur pour le logiciel inventorié n'ayant pas de configuration matérielle.  

Les informations suivantes s'affichent pour chaque configuration matérielle requise répertoriée :  

- **Titre du logiciel** : Titre du logiciel associé à la configuration matérielle requise  

- **Vitesse min. du processeur (MHz)** : Vitesse minimale du processeur en mégahertz (MHz) nécessaire au titre de logiciel  

- **Mémoire RAM minimum (Ko)** : Quantité de mémoire vive minimale en kilo-octets (Ko) nécessaire au titre de logiciel  

- **Espace disque minimum (Ko)** : Espace disque libre minimal en Ko nécessaire au titre de logiciel  

- **Taille minimale du disque (Ko)** : Espace disque libre minimal en Ko nécessaire au titre de logiciel  

- **État de validation** : État de validation de la configuration matérielle requise  

Les exigences matérielles prédéfinies stockées dans le catalogue Asset Intelligence sont accessibles en lecture seule et ne peuvent pas être supprimées. Les utilisateurs administratifs peuvent ajouter, modifier ou supprimer des exigences matérielles définies par l'utilisateur pour les titres de logiciels qui ne sont pas stockés dans le catalogue Asset Intelligence.  



## <a name="BKMK_InventoriedSoftwareTitles"></a> Logiciels inventoriés  

Pour afficher les informations des titres de logiciels inventoriés dans la console Configuration Manager, accédez à l'espace de travail **Biens et conformité**, développez le nœud **Asset Intelligence** et sélectionnez le nœud **Logiciels inventoriés**. L’agent d’inventaire matériel collecte les informations des logiciels inventoriés à partir des clients Configuration Manager en fonction des titres de logiciels qui sont stockés dans le catalogue Asset Intelligence.  

> [!Note]  
> L'agent d'inventaire matériel collecte l'inventaire en fonction des classes de création de rapports d'inventaire matériel Asset Intelligence que vous activez. Pour plus d’informations sur l’activation des classes de création de rapports, consultez la page [Configuration d’Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

Par défaut, les informations suivantes s'affichent pour chaque titre de logiciel inventorié :  

- **Nom** : Nom du titre de logiciel inventorié  

- **Fournisseur** : Nom du fournisseur qui a développé le titre de logiciel inventorié  

- **Version** : Version du produit du titre de logiciel inventorié  

- **Catégorie** : Catégorie qui est actuellement affectée au titre de logiciel inventorié  

- **Famille** : Famille qui est actuellement affectée au titre de logiciel inventorié  

- **Légende** [**1**, **2** et **3**] : Légendes personnalisées associées au titre de logiciel Les titres de logiciels inventoriés peuvent avoir jusqu'à trois légendes personnalisées.  

- **Nombre** : Nombre de clients Configuration Manager qui ont inventorié le titre de logiciel  

- **État** : État de validation du titre de logiciel inventorié  

> [!NOTE]  
> Vous pouvez modifier les informations de catégorisation des logiciels inventoriés uniquement sur le site de niveau supérieur de votre hiérarchie. Ces informations regroupent le nom du produit, le fournisseur, la catégorie de logiciels et famille de logiciels. Lorsque vous modifiez les informations de catégorisation des logiciels prédéfinis, l'état de validation **Validé** des logiciels devient **Défini par l'utilisateur**.  



## <a name="AssetIntelligenceSycnronizationPoint"></a> Point de synchronisation Asset Intelligence  

Le point de synchronisation Asset Intelligence est un rôle de système de site Configuration Manager. Il sert à se connecter à Microsoft Cloud sur le port TCP 443 afin de gérer les mises à jour dynamiques des informations du catalogue. Installez ce rôle de site uniquement sur le site de niveau supérieur de la hiérarchie. Configurez toutes les personnalisations de catalogue Asset Intelligence en utilisant une console Configuration Manager connectée au site de niveau supérieur. 

Lorsque vous configurez toutes les mises à jour sur le site de niveau supérieur, les informations du catalogue Asset Intelligence sont répliquées sur les autres sites de la hiérarchie. Le rôle de site vous permet de demander une synchronisation du catalogue à la demande avec Microsoft ou de programmer la synchronisation automatique du catalogue. Outre le téléchargement des nouvelles informations du catalogue, le point de synchronisation Asset Intelligence peut envoyer les informations des titres de logiciels personnalisées à Microsoft à des fins de catégorisation. Microsoft considère tous les titres de logiciels téléchargés comme des informations publiques. Assurez-vous que vos titres de logiciels personnalisés ne contiennent pas d’informations confidentielles ou propriétaires.  

Lorsque vous soumettez un titre de logiciel non catégorisé, Microsoft ne l’examine pas tant que quatre demandes de catégorisation n’ont pas été reçues de la part de clients pour le même titre de logiciel. Ensuite, les chercheurs Microsoft identifient et catégorisent les informations de catégorisation du titre de logiciel, puis les mettent à disposition de tous les clients qui utilisent le service en ligne. Les titres de logiciels ayant le plus grand nombre de demandes de catégorisation sont affectés de la priorité de catégorisation la plus élevée. Il y a peu de chances que les logiciels personnalisés et les applications cœur de métier soient catégorisés. Ne soumettez pas de demandes de catégorisation à Microsoft pour ces titres de logiciels.  

Un point de synchronisation Asset Intelligence est nécessaire pour se connecter à Microsoft Cloud. Pour plus d’informations sur l’installation du rôle, consultez la page [Configuration d’Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  



## <a name="BKMK_AssetIntelligenceHomePage"></a> Page d’accueil d’Asset Intelligence  

Le nœud **Asset Intelligence** de l’espace de travail **Biens et conformité** constitue la page d’accueil d’Asset Intelligence dans Configuration Manager. Cette page d'accueil affiche une vue de tableau de bord récapitulant les informations du catalogue Asset Intelligence.  

> [!NOTE]  
> La page d'accueil d'**Asset Intelligence** n'est pas automatiquement actualisée lorsque vous la consultez.  

La page d'accueil **Asset Intelligence** inclut les sections suivantes :  

- **Synchronisation de catalogue** : Informations indiquant si Asset Intelligence est activé, ainsi que l’état actuel du point de synchronisation Asset Intelligence.  

    > [!NOTE]  
    > La page d’accueil affiche uniquement cette section lorsque vous installez un point de synchronisation Asset Intelligence.  

    Cette section fournit également les informations suivantes :  

    - Calendrier des synchronisations  

    - Si vous avez importé une déclaration de licence cliente   

    - La dernière mise à jour de l’état  

    - L’heure de la prochaine mise à jour planifiée  

    - Le nombre de modifications après que vous avez installé le point de synchronisation Asset Intelligence   

- **État des logiciels inventoriés** : Nombre et pourcentage de logiciels inventoriés, de catégories de logiciels et de familles de logiciels qui sont identifiés par Microsoft ou par un administrateur, qui sont en attente d'identification en ligne ou non identifiés et non en attente. Les informations affichées dans un tableau indiquent le nombre pour chacun des éléments, tandis que les informations affichées dans le graphique indiquent le pourcentage de chacun des éléments.  



## <a name="BKMK_AssetIntelligenceReports"></a> Rapports Asset Intelligence  

Les rapports Asset Intelligence se trouvent dans la console Configuration Manager, dans l’espace de travail **Surveillance** dans le dossier **Asset Intelligence** sous le nœud **Rapports**. Les rapports fournissent des informations sur les matériels, la gestion des licences et les logiciels. Pour plus d'informations sur les rapports dans Configuration Manager, consultez la page [Rapports](/sccm/core/servers/manage/reporting).  

> [!NOTE]  
> La précision du nombre de titres de logiciels installés et des informations de licence affichés dans les rapports Asset Intelligence peut varier par rapport au nombre réel de titres de logiciels installés ou de licences utilisées dans l’environnement. Cette variation est due aux dépendances et limitations complexes qu’implique l’inventaire des informations de licence des logiciels installés dans les environnements d’entreprise. N'utilisez pas les rapports Asset Intelligence comme seule source pour déterminer la conformité des licences logicielles achetées.  


### <a name="BKMK_HardwareReports"></a> Rapports matériels  

Les rapports matériels Asset Intelligence fournissent des informations sur les ressources matérielles de l'organisation. En utilisant les informations d’inventaire matériel, comme la vitesse, la mémoire ou les périphériques, les rapports matériels Asset Intelligence peuvent contenir des informations sur les appareils USB, le matériel à mettre à niveau et même les ordinateurs qui ne sont pas prêts à recevoir une mise à niveau logicielle donnée.  

> [!NOTE]  
> Certaines données utilisateur des rapports Asset Intelligence sont collectées depuis le journal des événements de sécurité Windows. Pour améliorer l’exactitude des rapports, nettoyez ce journal quand vous réaffectez un ordinateur à un autre utilisateur.  


### <a name="BKMK_LicenseManagementReports"></a> Rapports de gestion des licences  

Les rapports de gestion des licences Asset Intelligence fournissent des données sur les licences en cours d’utilisation. Le rapport **Grand livre des licences** répertorie les applications Microsoft installées dans un format semblable à un relevé de licences Microsoft. Ce format fournit une méthode pratique de mise en correspondance des licences acquises et des licences utilisées. D’autres rapports de gestion des licences fournissent des informations sur les ordinateurs faisant office de serveurs exécutant le service de gestion de clés (KMS) pour les statistiques d’activation Windows.  

> [!IMPORTANT]  
> Plusieurs rapports de gestion des licences Asset Intelligence présentent des informations sur la fonction du service de gestion de clés KMS, une méthode d'administration des licences en volume. Si vous n’avez pas implémenté de serveur KMS, certains rapports ne contiendront aucune donnée.  


### <a name="BKMK_SoftwareReports"></a> Rapports logiciels  

Les rapports logiciels Asset Intelligence fournissent des informations sur les familles, catégories et titres de logiciels qui sont installés sur les ordinateurs de l'organisation. Par exemple, ces rapports contiennent des informations sur les objets application d'assistance du navigateur et les logiciels qui démarrent automatiquement. Ces rapports peuvent servir à identifier les logiciels de publicité, les logiciels espions et les programmes malveillants. Vous pouvez également les utiliser pour identifier des redondances logicielles afin de rationaliser la prise en charge et l’acquisition de logiciels.  


### <a name="BKMK_SoftwareIdTagReports"></a> Rapports sur les balises d’identification logicielle  

Les rapports sur les balises d'identification de logiciels Asset Intelligence fournissent des informations sur les logiciels qui contiennent une balise d'identification logicielle conforme ISO/IEC 19770-2. Les balises d'identification logicielle fournissent des informations d’autorité permettant d’identifier les logiciels installés. Quand vous activez la classe de rapport d’inventaire matériel **SMS_SoftwareTag**, Configuration Manager collecte des informations sur les logiciels dotés de balises d’identification logicielle. 

Les rapports suivants fournissent des informations sur les logiciels :  

- **Logiciel 14A – Recherche de logiciels dont la balise d'identification logicielle est activée** : Nombre de logiciels installés dont la balise d'identification logicielle est activée  

- **Logiciel 14B – Ordinateurs sur lesquels sont installés des logiciels dont la balise d'identification logicielle est activée** : Tous les ordinateurs sur lesquels sont installés des logiciels qui ont une balise d'identification logicielle spécifique activée  

- **Logiciel 14C – Logiciels installés sur un ordinateur spécifique et dont la balise d'identification logicielle est activée** : Tous les logiciels installés ayant une balise d'identification logicielle spécifique sur un ordinateur particulier  


### <a name="BKMK_ReportingLImitations"></a> Limites des rapports  

Les rapports Asset Intelligence peuvent fournir une grande quantité d'informations sur les titres de logiciels installés et les licences logicielles acquises en cours d'utilisation. N'utilisez pas ces informations comme seule source pour déterminer la conformité des licences logicielles acquises.  

#### <a name="BKMK_ExampleDependencies"></a> Exemples de dépendances  
La précision de la quantité affichée dans les rapports Asset Intelligence pour les titres de logiciels installés et les informations de licence peuvent varier par rapport aux quantités réelles actuellement utilisées. Cette variation est due aux dépendances complexes qu’implique l’inventaire des informations de licence des logiciels en cours d’utilisation dans les environnements d’entreprise. Les exemples suivants montrent les dépendances liées à l’inventaire des logiciels installés dans l’entreprise en utilisant Asset Intelligence, qui sont susceptibles d’affecter l’exactitude des rapports Asset Intelligence :  

- **Dépendances d'inventaire matériel sur les clients** : Les rapports Asset Intelligence sur les logiciels installés sont basés sur les données collectées à partir des clients Configuration Manager en étendant l'inventaire matériel afin d'activer la création de rapports Asset Intelligence. Compte tenu de cette dépendance sur la création de rapports d'inventaire matériel, les rapports Asset Intelligence contiennent uniquement les données des clients qui exécutent correctement les processus d'inventaire matériel avec les classes de rapport WMI Asset Intelligence requises activées. Puisque les clients Configuration Manager exécutent les processus d’inventaire matériel selon un calendrier défini par l’utilisateur administratif, il peut exister un décalage au niveau des rapports de données, qui affecte l’exactitude des rapports Asset Intelligence. 

    Par exemple, un logiciel sous licence inventorié peut être désinstallé après que le client a terminé un cycle d’inventaire matériel. Les rapports Asset Intelligence affichent le titre de logiciel tel qu’installé jusqu’au prochain cycle de rapports d’inventaire matériel du client.  

- **Dépendances de package de logiciel** : Les rapports Asset Intelligence reposent sur les données des titres de logiciels installés qui sont collectées en utilisant des processus standard d’inventaire matériel de client Configuration Manager. Il se peut que certaines données de logiciels ne soient pas correctement collectées. Exemples susceptibles d’entraîner la création de rapports Asset Intelligence inexacts :  

    - Installations de logiciels qui ne sont pas conformes aux processus d’installation standard  

    - Installations de logiciels qui ont été modifiés avant installation   

#### <a name="BKMK_LegalLimitations"></a> Limitations légales  
Les informations affichées dans les rapports Asset Intelligence sont soumises à de nombreuses limitations. Elles ne constituent en aucun cas un conseil juridique, comptable ou professionnel. Les informations fournies par les rapports Asset Intelligence sont valables à titre indicatif uniquement. Ne les utilisez pas comme seule source d’information pour déterminer la conformité de l’utilisation des licences logicielles.  

Les limitations suivantes illustrent des utilisations d’Asset Intelligence susceptibles d’affecter la précision des rapports :  

- **Limitations quantitatives de l'utilisation des licences Microsoft** :  

    - La quantité de licences logicielles Microsoft acquises repose sur les informations fournies par les administrateurs. Examinez ces informations pour vérifier l’exactitude du nombre de licences logicielles.  

    - La quantité de licences logicielles Microsoft indiquée inclut des informations uniquement sur les licences logicielles Microsoft acquises via des programmes de licences en volume. Elle ne reflète pas les informations de licences logicielles acquises auprès des canaux de vente au détail, OEM ou autre.  

    - Les licences logicielles acquises au cours des 45 derniers jours peuvent ne pas figurer dans la liste des licences logicielles Microsoft fournie, selon les besoins et calendriers des rapports du revendeur de logiciels.  

    - Les transferts de licences logicielles résultant des fusions ou rachats d'entreprises, peuvent ne pas être inclus dans le nombre de licences logicielles Microsoft.  

    - Les conditions non standard d'un contrat de licences en volume Microsoft (MVLS) peuvent affecter le nombre de licences logicielles indiqué. Il se peut qu’une analyse supplémentaire par un représentant Microsoft soit nécessaire.  

- **Limitations quantitatives des logiciels installés** : Les clients Configuration Manager doivent terminer correctement les cycles de diffusion d’inventaire matériel pour que les rapports Asset Intelligence reflètent précisément la quantité de logiciels installés. Il peut y avoir un décalage entre l’installation ou la désinstallation d’un logiciel sous licence après un cycle de création de rapports d’inventaire matériel réussi. Il se peut que cette action ne soit pas reflétée dans les rapports Asset Intelligence exécutés avant l’inventaire matériel suivant planifié par le client.  

- **Limitations relatives au rapprochement de licences** : Le rapprochement entre le nombre de titres de logiciels installés et le nombre de licences logicielles acquises est calculé en comparant le nombre de licences spécifié par l’administrateur et le nombre de logiciels installés collectés lors des inventaires matériels du client Configuration Manager en fonction du calendrier défini par l’administrateur. Cette comparaison ne constitue pas l'avis final de Microsoft concernant les licences. L'avis concernant les licences dépend en réalité de chaque nom de licence d'utilisation de logiciel et des droits d'utilisation accordés par le contrat de licence.  



## <a name="BKMK_ValidationStates"></a> États de validation Asset Intelligence  

Les états de validation Asset Intelligence représentent les états de validation actuels sources des informations du catalogue Asset Intelligence. Le tableau suivant présente les états de validation possibles d'Asset Intelligence et les actions de l'administrateur susceptibles de les déclencher.  

| État | Définition | Action de l'administrateur | Commentaire |  
|---------------|--------------------|------------------------------|-----------------|  
|**Validé**|Les chercheurs Microsoft ont défini l’élément de catalogue|Aucun|Meilleur état|  
|**Défini par l'utilisateur**|Les chercheurs Microsoft n’ont pas défini l’élément de catalogue|Personnaliser les informations du catalogue en local|Cet état est affiché dans les rapports Asset Intelligence|  
|**En attente**|Les chercheurs Microsoft n’ont pas défini l’élément de catalogue, mais vous avez soumis l’élément à Microsoft pour catégorisation|Aucune action supplémentaire suite à la demande de catégorisation|L'élément du catalogue conserve cet état jusqu'à ce que les chercheurs Microsoft classent l'élément dans une catégorie et que vous synchronisiez votre catalogue Asset Intelligence.|  
|**Peut être mis à jour**|Un élément du catalogue défini par un utilisateur a été catégorisé différemment par Microsoft lors de la synchronisation du catalogue.|Exécutez l'action **Résoudre le conflit** pour décider si vous allez utiliser les nouvelles informations de catégorisation ou la précédente valeur définie par l'utilisateur. Pour plus d’informations sur la résolution des conflits, consultez la page [Opérations pour Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/operations-for-asset-intelligence).|Une fois que vous avez résolu un conflit de catégorisation, l’élément n’est plus validé comme étant en conflit sauf si des mises à jour de catégorisation ultérieures apportent de nouvelles informations sur cet élément.|  
|**Sans catégorie**|L'élément du catalogue n'a pas été défini par les chercheurs Microsoft, il n'a pas été soumis à Microsoft pour catégorisation et l'administrateur ne lui a pas attribué de valeur de catégorisation définie par l'utilisateur.|Effectuez une demande de catégorisation ou personnalisez les informations du catalogue local. Pour plus d'informations, consultez la page [Opérations pour Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/operations-for-asset-intelligence).|Aucun|  

> [!NOTE]  
> L'état de validation des éléments de catalogue que vous avez soumis à Microsoft à des fins de catégorisation est **En attente** sur un site d'administration centrale mais sur les sites principaux enfants, l'état de validation affiché pour ces éléments continue d'être **Sans catégorie** .  

Pour obtenir des exemples du moment où un état de validation peut passer d'un état à un autre, consultez la page [Exemples de transitions d’états de validation pour Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/example-validation-state-transitions-for-asset-intelligence).  
