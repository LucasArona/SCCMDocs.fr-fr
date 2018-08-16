---
title: Surveiller l’état d’Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment surveiller Endpoint Protection dans votre hiérarchie System Center Configuration Manager.
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f4a1335c-bb3d-493e-a124-83a32a107dc8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f4e1ea4cb097381467774af9c3161079419d6840
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348767"
---
# <a name="how-to-monitor-endpoint-protection-status"></a>Guide pratique pour surveiller l’état d’Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez surveiller Endpoint Protection dans votre hiérarchie Microsoft System Center Configuration Manager à l’aide du nœud **État Endpoint Protection** sous **Sécurité** dans l’espace de travail **Surveillance**, à l’aide du nœud **Endpoint Protection** dans l’espace de travail **Ressources et Conformité** et à l’aide de rapports.  

##  <a name="BKMK_1"></a> Guide pratique pour surveiller Endpoint Protection à l’aide du nœud État Endpoint Protection  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l’espace de travail **Surveillance**, développez **Sécurité**, puis cliquez sur **État Endpoint Protection**.  

3.  Dans la liste **Regroupement** , sélectionnez le regroupement pour lequel vous souhaitez afficher des informations sur l'état.  

    > [!IMPORTANT]  
    >  Les regroupements peuvent être sélectionnés dans les cas suivants :  
    >   
    >  -   Quand vous sélectionnez **Afficher ce regroupement dans le tableau de bord Endpoint Protection** sous l’onglet **Alertes** de la boîte de dialogue *Propriétés de <nom_regroupement\>****.  
    > -   Quand vous déployez une stratégie de logiciel anti-programme malveillant Endpoint Protection sur le regroupement.  
    > -   Quand vous activez et déployez les paramètres client Endpoint Protection sur le regroupement.  

4.  Examinez les informations affichées dans le **état de sécurité** et **état opérationnel** sections. Vous pouvez cliquer sur n'importe quel lien d'état pour créer un regroupement temporaire dans le nœud **Périphériques** de l'espace de travail **Ressources et Conformité**. Le regroupement temporaire contient les ordinateurs dont l'état est sélectionné.  

    > [!IMPORTANT]  
    >  Les informations affichées dans le nœud **État Endpoint Protection** se basent sur les dernières données de synthèse de la base de données Configuration Manager et peuvent ne pas être actualisées. Si vous voulez récupérer les dernières données, sous l’onglet **Accueil** , cliquez sur **Exécuter le résumé**ou cliquez sur **Planifier le résumé** pour régler l’intervalle de résumé.  

##  <a name="BKMK_2"></a> Guide pratique pour surveiller Endpoint Protection dans l’espace de travail Ressources et Conformité  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité**, exécutez l'une des actions suivantes :  

    -   Cliquez sur **Périphériques**. Dans la liste **Périphériques** , sélectionnez un ordinateur, puis cliquez sur l'onglet **Détail du programme malveillant** .  

    -   Cliquez sur **Regroupements de périphériques**. Dans la liste **Regroupements d’appareils** , sélectionnez le regroupement qui contient l’ordinateur que vous voulez surveiller puis, sous l’onglet **Accueil** , dans le groupe **Regroupement** , cliquez sur **Afficher les membres**.  

3.  Dans la liste *<Nom_regroupement\>*, sélectionnez un ordinateur, puis cliquez sur l’onglet **Détail du programme malveillant**.  

##  <a name="BKMK_3"></a> Guide pratique pour surveiller Endpoint Protection à l’aide de rapports  
 Utilisez les rapports suivants pour obtenir des informations sur Endpoint Protection dans votre hiérarchie. Vous pouvez aussi vous servir de ces rapports pour résoudre les problèmes liés à Endpoint Protection. Pour plus d’informations sur la configuration de la création de rapports dans Configuration Manager, consultez [Création de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md) et [Fichiers journaux dans System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md). Les rapports Endpoint Protection sont dans le dossier Endpoint Protection.  

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Rapport d'activité des logiciels anti-programme malveillant**|Affiche une vue d'ensemble de l'activité des logiciels anti-programme malveillant pour un regroupement spécifié.|  
|**Ordinateurs infectés**|Affiche une liste des ordinateurs sur lesquels une menace spécifique est détectée.|  
|**Utilisateurs récurrents par menace**|Affiche la liste des utilisateurs ayant le plus grand nombre de menaces détectées.|  
|**Liste des menaces utilisateur**|Affiche une liste des menaces qui ont été trouvées pour un compte d'utilisateur spécifié.|  

## <a name="malware-alert-levels"></a>Niveaux d'alerte contre les logiciels malveillants  
 Utilisez le tableau suivant pour identifier les différents niveaux d’alerte Endpoint Protection qui peuvent apparaître dans les rapports ou dans la console Configuration Manager.  

|Niveau d'alerte|Description|  
|-----------------|-----------------|  
|**Échec**|Endpoint Protection n’a pas pu remédier au logiciel malveillant. Vérifiez les journaux pour plus de détails de l'erreur.<br /><br /> **Remarque :** pour obtenir la liste des fichiers journaux Configuration Manager et Endpoint Protection, consultez la section « Endpoint Protection » dans la rubrique [Fichiers journaux dans System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md).|  
|**Supprimé**|Endpoint Protection a correctement supprimé le logiciel malveillant.|  
|**En quarantaine**|Endpoint Protection a déplacé le logiciel malveillant vers un emplacement sécurisé et a empêché son exécution en attendant que vous le supprimiez ou que vous en autorisiez l’exécution.|  
|**Nettoyage effectué**|Les logiciels malveillants ont été supprimés du fichier infecté.|  
|**Autorisé**|Un utilisateur administratif est activée, le logiciel qui contient le logiciel malveillant de s'exécuter.|  
|**Aucune Action**|Endpoint Protection n’a pris aucune mesure contre le logiciel malveillant. Cela peut se produire si l'ordinateur est redémarré une fois le logiciel malveillant est détecté et le logiciel malveillant n'est plus détecté ; par exemple, si un réseau mappé lecteur sur le logiciel malveillant est détecté n'est pas reconnecté lorsque l'ordinateur redémarre.|  
|**Bloqué**|Endpoint Protection a empêché le logiciel malveillant de s’exécuter. Cela peut se produire si un processus sur l'ordinateur se trouve à contenir des logiciels malveillants.|
