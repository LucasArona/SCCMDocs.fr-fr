---
title: Questions fréquentes (FAQ) sur les données de diagnostic et d’utilisation
titleSuffix: Configuration Manager
description: Consultez les questions fréquemment posées sur les données de diagnostic et d’utilisation pour System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4174c68d5a6ccd31355d976b7830b6d09f39d91
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Questions fréquemment posées sur les données d’utilisation et de diagnostic pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit les réponses aux questions fréquemment posées sur les données de diagnostic et d’utilisation dans Configuration Manager.

## <a name="faqs"></a>FAQ

###  <a name="bkmk_off"></a> Comment désactiver la télémétrie ?  
La télémétrie ne peut pas être désactivée. Toutefois, vous pouvez choisir le niveau des données de télémétrie collectées. Pour définir le moment auquel les données de télémétrie sont envoyées, utilisez le point de connexion de service en mode hors connexion.

La version Current Branch de Configuration Manager doit être mise à jour régulièrement pour pouvoir prendre en charge les nouvelles versions de Windows 10 et de Microsoft Intune. Microsoft nécessite au moins des données de base pour le diagnostic et l’utilisation. Ces données sont utilisées pour conserver le produit à jour et améliorer l’expérience de mise à jour, ainsi que la qualité et la sécurité du produit.

###  <a name="bkmk_retention"></a> Quelle est la période de rétention des données ?  
 Les données d’utilisation et de diagnostic sont conservées un an.  

###  <a name="bkmk_update"></a> Des données d’utilisation et de diagnostic sont-elles envoyées lors de l’installation ou de la mise à jour du produit ?  
 Non. Des données d’utilisation et de diagnostic sont envoyées uniquement une fois le site installé et opérationnel.  

###  <a name="bkmk_frequency"></a> À quelle fréquence les données sont-elles envoyées ?  
 Les procédures stockées SQL s’exécutent tous les sept jours, à partir de la date d’installation du site. En mode en ligne, le point de connexion de service est configuré pour charger les données après l’exécution de requêtes. En mode hors connexion, l’administrateur utilise l’outil de connexion de service pour charger les données. Pour utiliser les données hors connexion, vous devez attendre sept jours après l’installation du site.  

###  <a name="bkmk_network"></a> Les données peuvent-elles être utilisées pour former un mappage réseau ?  
 Comme indiqué dans la description des niveaux de données d’utilisation et de diagnostic, les détails du site incluent les informations de fuseau horaire de chaque site. Celles-ci peuvent fournir des insights concernant la géolocalisation large et la dispersion globale des sites dans une hiérarchie. Ces données ne contiennent aucune information relative au réseau, comme des adresses IP ou des informations géographiques plus détaillées. Pour plus d’informations, consultez la liste des [articles sur les données d’utilisation et de diagnostic](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data#articles), puis recherchez les niveaux de collecte des données de diagnostic et d’utilisation correspondant à la version que vous utilisez.


###  <a name="bkmk_tables"></a> Pouvez-vous voir les données figurant dans des tables personnalisées ?  
 Non. Configuration Manager collecte des données de diagnostic et d’utilisation au moyen de procédures stockées SQL. Ces procédures stockées s’exécutent sur les tables de produit par défaut de la base de données. Toutes ces tables SQL ont le préfixe **TEL_**. Dans le cadre de la requête de détection de schéma SQL, tous les noms de tables sont hachés à des fins de comparaison avec les valeurs par défaut connues. Ce comportement détermine l’existence de tables personnalisées dans la base de données. La présence de tables personnalisées indique que le schéma de la base de données par défaut a été étendu. Il n’inclut pas les données stockées dans ces tables.  

###  <a name="bkmk_databases"></a> Pouvez-vous voir les noms d’autres bases de données, ou des données dans d’autres bases de données ? 
 Non. Les procédures stockées pour la collecte des données sont limités à la base de données du site.  

### <a name="bkmk_gdpr"></a> Configuration Manager est-il soumis au règlement général sur la protection des données (RGPD) ?
 Non. Configuration Manager n’est pas soumis au règlement général sur la protection des données. Il s’agit d’un produit installé en local que vous déployez, gérez et exécutez directement. Les données d’utilisation et de diagnostic collectées par Microsoft sont destinées à améliorer l’expérience d’installation, ainsi que la qualité et la sécurité des futures versions. Ces données sont soumises au règlement général sur la protection des données. Aucune information d’identification de l’utilisateur final et aucun identificateur de pseudonyme de l’utilisateur final ne sont collectés et transmis à Microsoft. Pour plus d’informations sur le règlement général sur la protection des données, consultez le [Centre de confidentialité Microsoft sur le règlement général sur la protection des données](https://microsoft.com/gdpr). Pour plus d’informations sur les données Configuration Manager, consultez [Données d’utilisation et de diagnostic](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).


## <a name="see-also"></a>Voir aussi  
 [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)
