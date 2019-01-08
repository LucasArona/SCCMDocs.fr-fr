---
title: Surveiller et planifier la gestion de l’alimentation
titleSuffix: Configuration Manager
description: Découvrez comment surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c0cff0787549624ab0b987fbacdb6f5b4f9c3ec1
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416212"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-system-center-configuration-manager"></a>Comment surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations suivantes pour mieux surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager.  

##  <a name="BKMK_How_to_use_reports"></a> Comment utiliser les rapports de gestion de l’alimentation  
 La gestion de l’alimentation dans Configuration Manager comprend plusieurs rapports permettant d’analyser la consommation énergétique et les paramètres d’alimentation des ordinateurs de votre organisation. Les rapports peuvent également servir à résoudre des problèmes.  

 Pour pouvoir utiliser les rapports de gestion de l'alimentation, vous devez configurer des rapports pour votre hiérarchie. Pour plus d’informations sur la création de rapports dans Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  Les informations de gestion de l’alimentation utilisées par les rapports quotidiens sont conservées dans la base de données du site Configuration Manager pendant 31 jours.  
>           Les informations de gestion de l’alimentation utilisées par les rapports mensuels sont conservées dans la base de données du site Configuration Manager pendant 13 mois.  
>   
>  Quand vous exécutez des rapports pendant les phases de surveillance, de planification et de conformité de la gestion de l’alimentation, enregistrez ou exportez les résultats de tous les rapports pour lesquels vous souhaitez conserver les données afin de les comparer ultérieurement au cas où ils seraient ensuite supprimés par Configuration Manager.  

## <a name="list-of-power-management-reports"></a>Liste des rapports de gestion de l’alimentation  
 La liste ci-dessous répertorie les rapports de gestion de l’alimentation disponibles dans Configuration Manager.  

> [!NOTE]  
>  Les rapports de gestion de l'alimentation indiquent le nombre d'ordinateurs physiques et le nombre d'ordinateurs virtuels dans un regroupement sélectionné. Toutefois, seules les informations de gestion de l'alimentation des ordinateurs physiques sont affichées dans les rapports de gestion de l'alimentation.  

###  <a name="BKMK_Activity"></a> Rapport Activité de l’ordinateur  
 Le rapport **Activité de l'ordinateur** affiche un graphique indiquant l'activité suivante pour un regroupement spécifié sur une période donnée :  

- **Ordinateur allumé** : l'ordinateur a été mis sous tension.  

- **Moniteur allumé** : l'écran a été mis sous tension.  

- **Utilisateur actif** : une activité a été détectée au niveau de la souris ou du clavier de l'ordinateur ou d'une connexion Bureau à distance à l'ordinateur.  

  Ce rapport est utilisé pendant les phases de surveillance, de planification et d'application pour comprendre le parallèle entre l'activité de l'ordinateur, l'activité de l'écran et l'activité de l'utilisateur pendant une période de 24 heures. Si vous exécutez le rapport sur un nombre de jours, les données sont agrégées pour cette période. Ce rapport peut vous aider à déterminer les heures d'activité (de pointe) et les heures d'inactivité (heures creuses) types pour le regroupement sélectionné pour déterminer quand il est nécessaire d'appliquer les modes de gestion d'alimentation configurés.  

  Le graphique indique les périodes au cours desquelles un ordinateur peut être allumé sans aucune activité de l'utilisateur. Pensez à appliquer des paramètres d'alimentation plus restrictifs durant ces périodes pour réduire les coûts d'électricité des ordinateurs qui sont sous tension, mais pas utilisés. Un ordinateur est considéré actif s'il existe une activité d'ordinateur, d'utilisateur ou de surveillance pendant au moins une minute pour une heure donnée sur le graphique. Si un ordinateur ne signale pas de données de gestion de l'alimentation, il ne figure pas dans le rapport **Activité de l'ordinateur** .  

  Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Date de début**|Dans la liste déroulante, sélectionnez la date de début du rapport.|  
|**Date de fin (facultative)**|Dans la liste déroulante, sélectionnez la date de fin facultative du rapport.|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement).|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Si vous ne définissez aucune **date de fin (facultative)** , le rapport contient un lien vers le rapport suivant qui fournit des informations complémentaires.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'activité de l'ordinateur**|Cliquez sur le lien **Cliquez pour obtenir des informations détaillées** pour afficher la liste des ordinateurs actifs, inactifs et qui n'envoient aucune donnée pour la date spécifiée.<br /><br /> Pour plus d'informations, consultez [Computer Activity Details Report](#BKMK_Activity_Details) dans cette rubrique.|  

###  <a name="BKMK_Comp_Activity_by_computer"></a> Rapport Activité par ordinateur  
 Le rapport **Activité par ordinateur** contient un graphique qui indique l'activité suivante pour un ordinateur spécifié à une date donnée :  

- **Ordinateur allumé** : l'ordinateur a été mis sous tension.  

- **Moniteur allumé** : l'écran a été mis sous tension.  

- **Utilisateur actif** : une activité a été détectée au niveau de la souris ou du clavier de l'ordinateur ou d'une connexion Bureau à distance à l'ordinateur.  

  Ce rapport peut être exécuté indépendamment ou appelé par le rapport **Détails de l'activité de l'ordinateur** .  

> [!NOTE]  
>  Les informations sur l'activité des ordinateurs sont collectées depuis les ordinateurs clients durant l'inventaire matériel. L'activité pendant un mode de faible ou de forte alimentation appliqué peut être collectée, selon le moment où l'inventaire matériel est exécuté.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Date du rapport**|Dans la liste déroulante, sélectionnez une date pour ce rapport.|  
|**Nom de l'ordinateur**|Entrez le nom de l'ordinateur pour lequel vous souhaitez obtenir un rapport.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur**|Cliquez sur le lien **Cliquez pour obtenir des informations détaillées** pour afficher les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes d'alimentation appliqués de l'ordinateur sélectionné.|  

###  <a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 Le rapport **Détails de l'activité de l'ordinateur** contient la liste des ordinateurs actifs ou inactifs avec leurs fonctions de veille et de sortie de veille. Ce rapport est appelé par le [Computer Activity Report](#BKMK_Activity) et il n’est pas destiné à être exécuté directement par l’administrateur du site.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Date du rapport**|Dans la liste déroulante, sélectionnez une date à utiliser pour ce rapport.|  
|**Heure du rapport**|Dans la liste déroulante, sélectionnez une heure pour la date définie pour laquelle vous souhaitez exécuter ce rapport . Les valeurs valides sont comprises entre **0 h 00** et **23 h 00**.|  
|**État de l'ordinateur**|Dans la liste déroulante, sélectionnez l'état de l'ordinateur pour lequel vous souhaitez exécuter ce rapport. Les valeurs valides sont **Tout** (ordinateurs mis sous tension ou hors tension), **Activé** (ordinateurs mis sous tension) et **Désactivé** (ordinateurs mis hors tension, en veille ou en veille prolongée). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  
|**Compatible avec le mode veille**|Dans la liste déroulante, indiquez si vous souhaitez afficher les ordinateurs compatibles avec le mode veille dans le rapport. Les valeurs valides sont **Tout** (ordinateurs aptes et inaptes à être mis en veille), **Non** (ordinateurs inaptes à être mis en veille) et **Oui** (ordinateurs aptes à être mis en veille).|  
|**Compatible avec la sortie de veille**|Dans la liste déroulante, indiquez si vous souhaitez afficher les ordinateurs compatibles avec le mode de sortie de veille dans le rapport. Les valeurs valides sont **Tout** (ordinateurs aptes et inaptes à sortir de veille), **Non** (ordinateurs inaptes à sortir de veille) et **Oui** (ordinateurs aptes à sortir de veille).|  
|**Gestion de l'alimentation**|Dans la liste déroulante, sélectionnez les types de modes d'alimentation à afficher dans le rapport. Les valeurs valides sont **Tout** (ordinateurs auxquels aucun mode de gestion de l’alimentation ne s’applique ; ordinateurs auxquels un mode de gestion de l’alimentation s’applique ; ordinateurs exclus de la gestion de l’alimentation), **Non spécifié** (ordinateurs auxquels aucun mode de gestion de l’alimentation ne s’applique), **Défini** (ordinateurs auxquels un mode de gestion de l’alimentation s’applique) et **Exclu** (ordinateurs exclus de la gestion de l’alimentation).|  
|**Système d'exploitation**|Dans la liste déroulante, sélectionnez les systèmes d'exploitation à afficher dans le rapport ou sélectionnez **Tout** pour afficher tous les systèmes d'exploitation.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Activité par ordinateur**|Cliquez sur un nom d’ordinateur pour voir l’activité spécifique pour cet ordinateur sur une période de création de rapports choisie. Ces activités incluent **Ordinateur allumé** (l’ordinateur a-t-il été allumé ?), **Moniteur allumé** (le moniteur a-t-il été allumé ?) et **Utilisateur actif** (une activité a été détectée à partir de la souris, du clavier ou d’une connexion Bureau à distance de l’ordinateur).<br /><br /> Pour plus d'informations, consultez [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) dans cette rubrique.|  

###  <a name="BKMK_Computer_Details"></a> Rapport Détails de l’ordinateur  
 Le rapport **Détails de l'ordinateur** affiche des informations détaillées sur les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes d'alimentation appliqués à un ordinateur spécifié. Ce rapport est appelé par le rapport **Activité par ordinateur** , le rapport **Ordinateurs avec plusieurs modes de gestion de l'alimentation** , le rapport **Fonctions de gestion de l'alimentation** et le rapport **Détails des paramètres du mode de gestion de l'alimentation** . Il n'est pas destiné à être exécuté directement par l'administrateur du site.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom de l'ordinateur**|Entrez le nom de l'ordinateur pour lequel vous souhaitez obtenir un rapport.|  
|**Mode d'alimentation**|Dans la liste déroulante, sélectionnez le type de paramètres d'alimentation à afficher dans les résultats du rapport. Sélectionnez **Sur secteur** pour afficher les paramètres d’alimentation configurés quand l’ordinateur est branché sur secteur et **Sur batterie** pour afficher les paramètres d’alimentation configurés quand l’ordinateur fonctionne sur batterie.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport ne dispose pas de paramètres masqués que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Not_Reporting"></a> Rapport Pas de rapport détaillé pour l’ordinateur  
 Le rapport **Pas de rapport détaillé pour l'ordinateur** affiche la liste des ordinateurs dans un regroupement spécifique qui n'ont pas signalé d'activité d'alimentation à une date et une heure données. Ce rapport est appelé par le **Computer Activity Report** et il n’est pas destiné à être exécuté directement par l’administrateur du site.  

> [!NOTE]  
>  Les ordinateurs envoient les informations de gestion de l'alimentation dans le cadre de leur calendrier d'inventaire matériel. Avant de conclure qu'un ordinateur n'envoie pas d'informations, vérifiez qu'il a signalé un inventaire matériel.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Date du rapport**|Dans la liste déroulante, sélectionnez une date pour ce rapport.|  
|**Heure du rapport**|Dans la liste déroulante, sélectionnez une heure pour la date définie pour laquelle vous souhaitez exécuter ce rapport . Les valeurs valides sont comprises entre **0 h 00** et **23 h 00**.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Excluded"></a> Ordinateurs exclus  
 Le rapport **Ordinateurs exclus** affiche la liste des ordinateurs d’un regroupement qui ont été exclus de la gestion d’alimentation Configuration Manager.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  
|**Raison**|Dans la liste déroulante, sélectionnez la raison pour laquelle les ordinateurs ont été exclus de la gestion de l'alimentation. Vous pouvez afficher **Tout** (tous les ordinateurs exclus), **Exclusion par l’administrateur** (seuls les ordinateurs qui ont été exclus par un utilisateur administratif) et **Exclusion par l’utilisateur** (seuls les ordinateurs qui ont été exclus par un utilisateur du Centre logiciel).|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur**|Cliquez sur un nom d'ordinateur pour afficher les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes de gestion de l'alimentation appliqués à l'ordinateur sélectionné.<br /><br /> Pour plus d'informations, consultez [Computer Details Report](#BKMK_Computer_Details) dans cette rubrique.|  

###  <a name="BKMK_Multiple"></a> Ordinateurs avec plusieurs modes de gestion de l'alimentation  
 Le rapport **Ordinateurs avec plusieurs modes de gestion de l'alimentation** affiche la liste des ordinateurs qui sont membres de plusieurs regroupements, chacun appliquant des modes différents de gestion de l'alimentation. Pour chaque ordinateur ayant potentiellement des paramètres d'alimentation conflictuels, le rapport indique le nom de l'ordinateur et les modes de gestion de l'alimentation appliqués pour chaque regroupement dont l'ordinateur est membre.  

> [!IMPORTANT]  
>  Si un ordinateur est membre de plusieurs regroupements et que chaque regroupement a un mode de gestion de l’alimentation différent, le mode de gestion de l’alimentation le moins restrictif s’applique.  
>   
>  Si un ordinateur est membre de plusieurs regroupements et que chaque regroupement a une heure de mise en éveil différente, l’heure la plus proche de minuit est utilisée.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur**|Cliquez sur un nom d'ordinateur pour afficher les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes de gestion de l'alimentation appliqués à l'ordinateur sélectionné.<br /><br /> Pour plus d'informations, consultez [Computer Details Report](#BKMK_Computer_Details) dans cette rubrique.|  

###  <a name="BKMK_Consumption"></a> Rapport Consommation énergétique  
 Le rapport **Consommation énergétique** affiche les informations suivantes :  

- Un graphique indiquant la consommation électrique mensuelle totale des ordinateurs, exprimée en kilowatts/heure (kWh) dans le regroupement spécifié pour la période indiquée.  

- Un graphique indiquant la consommation électrique moyenne, exprimée en kilowatts/heure (kWh) de chaque ordinateur dans le regroupement spécifié pour la période indiquée.  

- Un tableau montrant la consommation électrique mensuelle totale, exprimée en kilowatts/heure (kWh) et la consommation électrique moyenne des ordinateurs du regroupement spécifié pour la période indiquée.  

  Ces informations peuvent être utilisées pour comprendre les tendances de consommation électrique dans votre environnement. Après avoir appliqué un mode d'alimentation aux ordinateurs du regroupement sélectionné, la consommation électrique des ordinateurs doit diminuer.  

> [!NOTE]  
>  Si vous ajoutez ou supprimez des membres dans le regroupement après avoir appliqué un mode d'alimentation, les résultats du rapport **Consommation énergétique** changent et peuvent compliquer la comparaison des résultats des phases de surveillance et de planification et de la phase d'application.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Date de début**|Dans la liste déroulante, sélectionnez la date de début du rapport.|  
|**Date de fin**|Dans la liste déroulante, sélectionnez la date de fin du rapport.|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,07** kWh.|  
|**Ordinateur portable allumé**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0,02** kWh.|  
|**Ordinateur de bureau en veille**|Spécifiez la consommation électrique d'un ordinateur de bureau qui est entré en mode veille. La valeur par défaut est **0,003** kWh.|  
|**Ordinateur portable en veille**|Spécifiez la consommation électrique d'un ordinateur portable qui est entré en mode veille. La valeur par défaut est **0,001** kWh.|  
|**Ordinateur de bureau éteint**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur portable éteint**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Moniteur d'ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,028** kWh.|  
|**Moniteur d'ordinateur portable allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0** kWh.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Consumption_by_Day"></a> Rapport Consommation énergétique journalière  
 Le rapport **Consommation énergétique journalière** affiche les informations suivantes :  

- Un graphique indiquant la consommation électrique journalière totale des ordinateurs, exprimée en kilowatts/heure (kWh), dans le regroupement spécifié pour les 31 derniers jours.  

- Un graphique indiquant la consommation électrique quotidienne moyenne en kilowatts/heure (kWh) de chaque ordinateur du regroupement spécifié au cours des 31 derniers jours.  

- Un tableau indiquant la consommation électrique quotidienne totale en kilowatts/heure (kWh) et la consommation électrique quotidienne moyenne des ordinateurs du regroupement spécifié pour les 31 derniers jours.  

  Ces informations peuvent être utilisées pour comprendre les tendances de consommation électrique dans votre environnement. Après avoir appliqué un mode d'alimentation aux ordinateurs du regroupement sélectionné, la consommation électrique des ordinateurs doit diminuer.  

> [!NOTE]  
>  Si vous ajoutez ou supprimez des membres dans le regroupement après avoir appliqué un mode d'alimentation, les résultats du rapport **Consommation énergétique** changent et peuvent compliquer la comparaison des résultats des phases de surveillance et de planification et de la phase d'application.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  
|**Device Type**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,07** kWh.|  
|**Ordinateur portable allumé**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0,02** kWh.|  
|**Ordinateur de bureau en veille**|Spécifiez la consommation électrique d'un ordinateur de bureau qui est entré en mode veille. La valeur par défaut est **0,003** kWh.|  
|**Ordinateur portable en veille**|Spécifiez la consommation électrique d'un ordinateur portable qui est entré en mode veille. La valeur par défaut est **0,001** kWh.|  
|**Ordinateur de bureau éteint**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur portable éteint**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Moniteur d'ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,028** kWh.|  
|**Moniteur d'ordinateur portable allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0** kWh.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Cost"></a> Rapport Coût énergétique  
 Le rapport **Coût énergétique** affiche les informations suivantes :  

- Un graphique indiquant le coût mensuel total d'électricité des ordinateurs du regroupement spécifié pour la période indiquée.  

- Un graphique indiquant le coût mensuel moyen d'électricité de chaque ordinateur du regroupement spécifié pour la période indiquée.  

- Un tableau affichant le coût mensuel total d'électricité et le coût mensuel moyen d'électricité des ordinateurs du regroupement spécifié au cours des 31 derniers jours.  

  Ces informations peuvent être utilisées pour comprendre les tendances de coût d'électricité dans votre environnement. Après avoir appliqué un mode d'alimentation aux ordinateurs du regroupement sélectionné, le coût d'électricité des ordinateurs doit diminuer.  

  Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Date de début**|Dans la liste déroulante, sélectionnez la date de début du rapport.|  
|**Date de fin**|Dans la liste déroulante, sélectionnez la date de fin du rapport.|  
|**Coût du kWh**|Spécifiez le coût par kWh d'électricité. La valeur par défaut est **0,09**.<br /><br /> Vous pouvez modifier la devise utilisée par ce rapport dans la section des paramètres cachés.|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,07** kWh.|  
|**Ordinateur portable allumé**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0,02** kWh.|  
|**Ordinateur de bureau en veille**|Spécifiez la consommation électrique d'un ordinateur de bureau qui est entré en mode veille. La valeur par défaut est **0,003** kWh.|  
|**Ordinateur portable en veille**|Spécifiez la consommation électrique d'un ordinateur portable qui est entré en mode veille. La valeur par défaut est **0,001** kWh.|  
|**Ordinateur de bureau éteint**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur portable éteint**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Moniteur d'ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,028** kWh.|  
|**Moniteur d'ordinateur portable allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0** kWh.|  
|**Devise**|Spécifiez le nom de la devise à utiliser pour ce rapport. La valeur par défaut est **USD ($)**.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Cost_by_Day"></a> Rapport Coût énergétique journalier  
 Le rapport **Coût énergétique journalier** affiche les informations suivantes :  

- Un graphique indiquant le coût total d'électricité quotidien des ordinateurs du regroupement spécifié pour les 31 derniers jours.  

- Un graphique indiquant le coût moyen d'électricité quotidien de chaque ordinateur du regroupement spécifié pour les 31 derniers jours.  

- Un tableau affichant le coût total d'électricité quotidien et le coût moyen d'électricité quotidien des ordinateurs du regroupement spécifié pour les 31 derniers jours.  

  Ces informations peuvent être utilisées pour comprendre les tendances de coût d'électricité dans votre environnement. Après avoir appliqué un mode d'alimentation aux ordinateurs du regroupement sélectionné, le coût d'électricité des ordinateurs doit diminuer.  

  Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  
|**Coût du kWh**|Spécifiez le coût par kWh d'électricité. La valeur par défaut est **0,09**.<br /><br /> Vous pouvez modifier la devise utilisée par ce rapport dans la section des paramètres cachés.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,07** kWh.|  
|**Ordinateur portable allumé**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0,02** kWh.|  
|**Ordinateur de bureau en veille**|Spécifiez la consommation électrique d'un ordinateur de bureau qui est entré en mode veille. La valeur par défaut est **0,003** kWh.|  
|**Ordinateur portable en veille**|Spécifiez la consommation électrique d'un ordinateur portable qui est entré en mode veille. La valeur par défaut est **0,001** kWh.|  
|**Ordinateur de bureau éteint**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur portable éteint**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Moniteur d'ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,028** kWh.|  
|**Moniteur d'ordinateur portable allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0** kWh.|  
|**Devise**|Spécifiez le nom de la devise à utiliser pour ce rapport. La valeur par défaut est **USD ($)**.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Environmental_Impact"></a> Rapport Incidence sur l’environnement  
 Le rapport **Incidence sur l'environnement** affiche les informations suivantes :  

- Un graphique indiquant la quantité mensuelle totale de CO2 générée (en tonnes) par les ordinateurs du regroupement spécifié pendant la période indiquée.  

- Un graphique indiquant la quantité mensuelle moyenne de CO2 générée (en tonnes) par chaque ordinateur du regroupement spécifié pendant la période indiquée.  

- Un tableau indiquant la quantité mensuelle totale de CO2 générée et la quantité mensuelle moyenne de CO2 générée par les ordinateurs du regroupement spécifié pendant la période indiquée.  

  Le rapport **Incidence sur l’environnement** calcule la quantité de CO2 générée (en tonnes) en utilisant la durée pendant laquelle un ordinateur ou un moniteur est resté sous tension sur une période de 24 heures.  

  Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Date de début du rapport**|Dans la liste déroulante, sélectionnez la date de début du rapport.|  
|**Date de fin du rapport**|Dans la liste déroulante, sélectionnez la date de fin du rapport.|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,07** kWh.|  
|**Ordinateur portable allumé**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0,02** kWh.|  
|**Ordinateur de bureau en veille**|Spécifiez la consommation électrique d'un ordinateur de bureau qui est entré en mode veille. La valeur par défaut est **0,003** kWh.|  
|**Ordinateur portable en veille**|Spécifiez la consommation électrique d'un ordinateur portable qui est entré en mode veille. La valeur par défaut est **0,001** kWh.|  
|**Ordinateur de bureau éteint**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur portable éteint**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Moniteur d'ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,028** kWh.|  
|**Moniteur d'ordinateur portable allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0** kWh.|  
|**Facteur carbone (tonnes/kWh)** (CO2Mix)|Spécifiez la valeur du facteur carbone (en tonnes/kWh) que vous pouvez généralement obtenir auprès de votre compagnie d'électricité. La valeur par défaut est **0,0015** tonne par kWh.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Environmental_Impact_by_Day"></a> Rapport Incidence journalière sur l’environnement  
 Le rapport **Incidence journalière sur l'environnement** affiche les informations suivantes :  

- Un graphique indiquant la quantité quotidienne totale de CO2 générée (en tonnes) par les ordinateurs du regroupement spécifié pendant les 31 derniers jours.  

- Un graphique indiquant la quantité quotidienne moyenne de CO2 générée (en tonnes) par chaque ordinateur du regroupement spécifié pendant les 31 derniers jours.  

- Un tableau indiquant la quantité quotidienne totale de CO2 générée et la quantité quotidienne moyenne de CO2 générée par les ordinateurs du regroupement spécifié pendant les 31 derniers jours.  

  Le rapport **Incidence journalière sur l’environnement** calcule la quantité de CO2 générée (en tonnes) en utilisant la durée pendant laquelle un ordinateur ou un moniteur est resté sous tension sur une période de 24 heures.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  
|**Type d'appareil**|Dans la liste déroulante, sélectionnez le type d'ordinateur pour lequel vous souhaitez obtenir un rapport. Les valeurs valides sont **Tout** (ordinateurs portables et postes de travail), **Bureau** (postes de travail uniquement) et **Ordinateur portable** (ordinateurs portables uniquement). Ces valeurs sont retournées uniquement pour la période de création de rapports sélectionnée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,07** kWh.|  
|**Ordinateur portable allumé**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0,02** kWh.|  
|**Ordinateur de bureau éteint**|Spécifiez la consommation électrique d'un ordinateur de bureau lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur portable éteint**|Spécifiez la consommation électrique d'un ordinateur portable lorsqu'il est éteint. La valeur par défaut est **0** kWh.|  
|**Ordinateur de bureau en veille**|Spécifiez la consommation électrique d'un ordinateur de bureau qui est entré en mode veille. La valeur par défaut est **0,003** kWh.|  
|**Ordinateur portable en veille**|Spécifiez la consommation électrique d'un ordinateur portable qui est entré en mode veille. La valeur par défaut est **0,001** kWh.|  
|**Moniteur d'ordinateur de bureau allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur de bureau lorsqu'il est allumé. La valeur par défaut est **0,028** kWh.|  
|**Moniteur d'ordinateur portable allumé**|Spécifiez la consommation électrique d'un moniteur d'ordinateur portable lorsqu'il est allumé. La valeur par défaut est **0** kWh.|  
|**Facteur carbone (tonnes/kWh)** (CO2Mix)|Spécifiez une valeur pour le facteur carbone (en tonnes/kWh) que vous pouvez généralement obtenir auprès de votre compagnie d'électricité. La valeur par défaut est **0,0015** tonne par kWh.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport n'établit pas de liaison à d'autres rapports de gestion de l'alimentation.  

###  <a name="BKMK_Insomnia_Computer_Details"></a> Rapport Détails de l’ordinateur non mis en veille  
 Le rapport **Détails de l'ordinateur non mis en veille** affiche la liste des ordinateurs qui ne se sont pas mis en veille ou en veille prolongée pour une raison donnée pendant une période spécifique. Ce rapport est appelé par le **Rapport sur la non mise en veille** et il n'est pas destiné à être exécuté directement par l'administrateur du site.  

 Le **rapport de non-mise en veille** indique que les ordinateurs **ne sont pas compatibles avec le mode veille** lorsqu'ils ne peuvent pas se mettre en veille et qu'ils ont été sous tension pendant toute la période de rapport définie. Le rapport affiche un ordinateur comme **Non compatible avec le mode veille prolongée** lorsqu'il ne peut pas se mettre en veille prolongée et qu'il a été sous tension pendant toute la période de rapport définie.  

> [!NOTE]  
>  La gestion de l'alimentation peut seulement collecter les causes qui ont empêché les ordinateurs exécutant Windows 7 ou Windows Server 2008 R2 de se mettre en veille ou en veille prolongée.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Intervalle du rapport (jours)**|Spécifiez le nombre de jours que doit couvrir le rapport. La valeur par défaut est **7** jours.|  
|**Cause de la non mise en veille**|Dans la liste déroulante, sélectionnez une des causes qui peuvent empêcher les ordinateurs d'entrer en mode veille ou veille prolongée.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur**|Cliquez sur le lien **Cliquez pour obtenir des informations détaillées** pour afficher les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes d'alimentation appliqués de l'ordinateur sélectionné.<br /><br /> Pour plus d'informations, consultez [Computer Details Report](#BKMK_Computer_Details) dans cette rubrique.|  

###  <a name="BKMK_Insomnia"></a> Insomnia report  
 Le **Rapport sur la non mise en veille** affiche une liste des causes courantes qui ont empêché les ordinateurs d'entrer en veille ou en veille prolongée et le nombre d'ordinateurs affectés par chaque cause pendant une période spécifique. Un certain nombre de causes peut empêcher un ordinateur d'entrer en veille ou en veille prolongée, notamment le processus en cours d'exécution sur l'ordinateur, une session de bureau à distance ouverte ou l'incapacité pour l'ordinateur d'entrer en veille ou en veille prolongée. À partir de ce rapport, vous pouvez ouvrir le rapport **Détails de l'ordinateur non mis en veille** , qui affiche une liste d'ordinateurs concernés par chaque cause d'ordinateurs qui ne sont pas en veille ou en veille prolongée.  

 Le rapport de non mise en veille affiche un ordinateur comme **Non compatible avec le mode veille** lorsqu'il ne peut pas se mettre en veille et qu'il a été sous tension pendant toute la période de rapport définie. Le rapport affiche un ordinateur comme **Non compatible avec le mode veille prolongée** lorsqu'il ne peut pas se mettre en veille prolongée et qu'il a été sous tension pendant toute la période de rapport définie.  

> [!NOTE]  
>  La gestion de l'alimentation peut seulement collecter les causes qui ont empêché les ordinateurs exécutant Windows 7 ou Windows Server 2008 R2 de se mettre en veille ou en veille prolongée.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**Intervalle du rapport (jours)**|Spécifiez le nombre de jours que doit couvrir le rapport. La valeur par défaut est **7** jours. La valeur maximale est **365** jours. Spécifiez **0** pour exécuter le rapport pour aujourd'hui.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur non mis en veille**|Cliquez sur un numéro de la colonne **Ordinateurs affectés** pour afficher une liste des ordinateurs incapables de passer en mode veille ou en mode veille prolongée en raison de la cause sélectionnée.<br /><br /> Pour plus d'informations, consultez [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) dans cette rubrique.|  

###  <a name="BKMK_Capabilites"></a> Rapport Fonctions de gestion de l’alimentation  
 Le rapport **Fonctions de gestion de l'alimentation** affiche les fonctions matérielles de gestion de l'alimentation des ordinateurs dans le regroupement spécifique. Ce rapport est généralement utilisé dans la phase de surveillance de la gestion de l'alimentation pour déterminer les fonctions de gestion de l'alimentation des ordinateurs de votre organisation. Les informations affichées dans le rapport peuvent ensuite être utilisées pour créer des regroupements d'ordinateurs auxquels seront appliqués des modes d'alimentation ou qui seront exclus de la gestion de l'alimentation. Les fonctions de gestion de l'alimentation affichées par ce rapport sont les suivantes :  

- **Compatible avec le mode veille** - Indique si l'ordinateur a la possibilité d'entrer en veille s'il est configuré pour ce faire.  

- **Compatible avec le mode veille prolongée** – Indique si l'ordinateur peut entrer en veille prolongée s'il est configuré pour ce faire.  

- **Compatible avec la sortie de veille** – Indique si l'ordinateur peut sortir du mode veille s'il est configuré pour ce faire.  

- **Compatible avec la sortie de veille prolongée** – Indique si l'ordinateur peut sortir du mode veille prolongée s'il est configuré pour ce faire.  

  Les valeurs signalées par le rapport **Fonctions de gestion de l'alimentation** indiquent les possibilités de mise en veille et en veille prolongée d'ordinateurs, tels que signalés par Windows. Toutefois, les valeurs signalées ne reflètent pas les cas où les paramètres de BIOS ou de Windows empêchent ces fonctions d'opérer.  

  Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  
|**Filtre d'affichage**|Dans la liste déroulante, sélectionnez **Non pris en charge** pour afficher uniquement les ordinateurs du regroupement spécifié qui ne sont pas aptes à être mis en veille, à être mis en veille prolongée, à sortir de veille ou à sortir de veille prolongée. Sélectionnez **Tout afficher** pour afficher tous les ordinateurs du regroupement spécifié.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Ce rapport n'a aucun paramètre masqué que vous pouvez définir.  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur**|Cliquez sur un nom d'ordinateur pour afficher les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes de gestion de l'alimentation appliqués à l'ordinateur sélectionné.<br /><br /> Pour plus d'informations, consultez [Computer Details Report](#BKMK_Computer_Details) dans cette rubrique.|  

###  <a name="BKMK_Settings"></a> Rapport Paramètres d’alimentation  
 Le rapport **Paramètres d'alimentation** affiche une liste agrégée des paramètres d'alimentation utilisés par les ordinateurs du regroupement spécifié. Pour chaque paramètre d'alimentation, les modes d'alimentation, les valeurs et les unités possibles sont affichés, ainsi que le nombre d'ordinateurs utilisant ces valeurs. Ce rapport peut être utilisé pendant la phase de surveillance de la gestion de l'alimentation pour aider l'administrateur à comprendre les paramètres d'alimentation existants utilisés par les ordinateurs du site et pour faciliter la planification de l'application optimale des paramètres d'alimentation grâce à un mode de gestion de l'alimentation. Ce rapport est également utile lors de la résolution d'erreurs afin de vérifier que ces paramètres d'alimentation ont été correctement appliqués.  

> [!NOTE]  
>  Les paramètres affichés sont collectés à partir d'ordinateurs clients pendant l'inventaire matériel. Selon le moment auquel est exécuté l'inventaire matériel, les paramètres des modes d'alimentation appliqués en heures creuses ou en heure de pointe peuvent être collectés.  

 Utilisez les paramètres suivants pour configurer ce rapport.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Nom du regroupement**|Dans la liste déroulante, sélectionnez un regroupement pour ce rapport.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Spécifiez le nombre de langues dans lesquelles vous souhaitez afficher les noms des paramètres d'alimentation signalés par les ordinateurs clients. Si vous voulez uniquement afficher la langue la plus répandue, conservez ce paramètre à sa valeur par défaut de **1**. Pour afficher toutes les langues, définissez cette valeur sur **0**.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails des paramètres du mode de gestion de l'alimentation**|Cliquez sur le nombre d’ordinateurs dans la colonne **Ordinateurs** pour afficher la liste de tous les ordinateurs qui utilisent les paramètres d’alimentation de cette ligne.<br /><br /> Pour plus d'informations, consultez [Power Settings Details Report](#BKMK_Settings_Details) dans cette rubrique.|  

###  <a name="BKMK_Settings_Details"></a> Power Settings Details report  
 Le rapport **Détails des paramètres d'alimentation** affiche d'autres informations sur les ordinateurs sélectionnés dans le rapport **Paramètres d'alimentation** . Ce rapport est appelé par le rapport **Paramètres d'alimentation** et il n'est pas destiné à être exécuté directement par l'administrateur du site.  

#### <a name="required-report-parameters"></a>Paramètres de rapport obligatoires  
 Les paramètres suivants doivent être spécifiés pour exécuter ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**Regroupement**|Dans la liste déroulante, sélectionnez le regroupement à utiliser pour ce rapport.|  
|**GUID du paramètre d'alimentation**|Dans la liste déroulante, sélectionnez le GUID du paramètre d'alimentation sur lequel vous souhaitez effectuer un rapport. Pour obtenir la liste de tous les paramètres d’alimentation et leurs utilisations, consultez [Paramètres du mode de gestion de l’alimentation disponibles](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) dans la rubrique [Comment créer et appliquer des modes de gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Power Mode**|Dans la liste déroulante, sélectionnez le type de paramètres d'alimentation à afficher dans les résultats du rapport. Sélectionnez **Sur secteur** pour afficher les paramètres d’alimentation configurés quand l’ordinateur est branché sur secteur et **Sur batterie** pour afficher les paramètres d’alimentation configurés quand l’ordinateur fonctionne sur batterie.|  
|**Index des paramètres**|Dans la liste déroulante, sélectionnez la valeur pour le nom de paramètre d'alimentation sélectionné pour lequel vous souhaitez produire un rapport. Par exemple, pour afficher tous les ordinateurs dont le paramètre **Arrêter le disque dur après** a la valeur **10** minutes, sélectionnez **Arrêter le disque dur après** pour **Nom du paramètre d’alimentation** et **10** pour **Index des paramètres**.|  

#### <a name="hidden-report-parameters"></a>Paramètres de rapport masqués  
 Vous pouvez également indiquer les paramètres masqués suivants pour modifier le comportement de ce rapport.  

|Nom du paramètre|Description|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Spécifiez le nombre de langues dans lesquelles vous souhaitez afficher les noms des paramètres d'alimentation signalés par les ordinateurs clients. Si vous voulez uniquement afficher la langue la plus répandue, conservez ce paramètre à sa valeur par défaut de **1**. Pour afficher toutes les langues, définissez cette valeur sur **0**.|  

#### <a name="report-links"></a>Liens de rapports  
 Ce rapport contient des liens vers le rapport suivant qui fournit des informations supplémentaires sur l'élément sélectionné.  

|Nom du rapport|Détails|  
|-----------------|-------------|  
|**Détails de l'ordinateur**|Cliquez sur un nom d'ordinateur pour afficher les fonctions de gestion de l'alimentation, les paramètres d'alimentation et les modes de gestion de l'alimentation appliqués à l'ordinateur sélectionné.<br /><br /> Pour plus d'informations, consultez [Computer Details Report](#BKMK_Computer_Details) dans cette rubrique.|  
