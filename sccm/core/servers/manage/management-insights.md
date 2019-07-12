---
title: Management insights
titleSuffix: Configuration Manager
description: Découvrez plus en détail la fonctionnalité Insights de gestion disponible dans la console Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ea90ff0b9c163dac79a96494b03252fbd1935b43
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676496"
---
# <a name="management-insights-in-configuration-manager"></a>Insights de gestion dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les insights de gestion dans Configuration Manager fournissent des informations sur l’état actuel de votre environnement. Les informations sont basées sur l’analyse des données provenant de la base de données du site. Ces informations vous aident à mieux comprendre votre environnement et à prendre des mesures en fonction de ces renseignements. Cette fonctionnalité a été publiée dans Configuration Manager version 1802. <!--1353967-->



## <a name="review-management-insights"></a>Examiner les insights de gestion 

Pour afficher les règles, votre compte nécessite l’autorisation de **lecture** sur l’objet **site**.

1. Ouvrez la console Configuration Manager.  

2. Accédez à l’espace de travail **Administration**, développez **Insights de gestion**, puis sélectionnez **Tous les insights**.  

    > [!Note]  
    > Dans la version 1810, lorsque vous sélectionnez le nœud **Insights de gestion**, celui-ci affiche le [Tableau de bord des insights de gestion](#bkmk_insights).  

3. Ouvrez le groupe d’insights de gestion que vous souhaitez examiner. Dans le ruban, sélectionnez **Afficher les insights**.  

Les quatre onglets suivants sont disponibles pour l’examen : 

- **Toutes les règles** : Affiche la liste complète des règles pour le groupe d’insights de gestion choisi.  

- **Terminé** :  Liste les règles quand aucune action n’est nécessaire.  

- **En cours** : Affiche les règles quand certains prérequis, mais pas tous, sont remplis.  

- **Action nécessaire** : Les règles nécessitant la prise de mesures sont listées. Sélectionnez **Plus de détails** pour récupérer des éléments spécifiques quand une action est nécessaire.  

Le volet **Prérequis** répertorie les éléments nécessaires pour exécuter la règle.

#### <a name="all-rules-and-prerequisites-for-the-cloud-services-group"></a>Ensemble des règles et prérequis pour le groupe de services cloud
![Insights de gestion : ensemble des règles et prérequis pour le groupe de services cloud](./media/Management-insights-all-cloud-rules.png)


Sélectionnez une règle, puis sélectionnez **Plus de détails** pour en afficher les détails.



## <a name="operations"></a>Opérations

Les règles des insights de gestion réévaluent leur mise en application selon une planification hebdomadaire. Pour réévaluer une règle à la demande, cliquez avec le bouton droit sur la règle et sélectionnez **Réévaluer**.

Le fichier journal pour les règles des insights de gestion est **SMS_DataEngine.log** sur le serveur de site.

<!--1357930-->
Depuis la version 1806, certaines règles vous permettent de prendre des mesures. Sélectionnez une règle, sélectionnez **Plus de détails**, puis sélectionnez **Entreprendre une action** si cette option est disponible. 

En fonction de la règle, cette action présente l’un des comportements suivants :  

- Dans la console, accède automatiquement au nœud dans lequel vous pouvez entreprendre des actions. Par exemple, si les insights de gestion recommandent de changer un paramètre client, le fait d’entreprendre une action vous redirige vers le nœud Paramètres du client. Vous pouvez ensuite entreprendre d’autres actions en modifiant l’objet de paramètres clients par défaut ou personnalisé.  

- Accède à une vue filtrée selon une requête. Par exemple, le fait d’entreprendre une action avec la règle de regroupements vides montre simplement la liste des collections. Vous pouvez ensuite entreprendre d’autres actions, comme supprimer un regroupement ou modifier ses règles d’adhésion.  



## <a name="bkmk_insights"></a> Tableau de bord Insights de gestion
<!--1357979-->

À compter de la version 1810, le nœud **Insights de gestion** comprend un tableau de bord graphique. Ce tableau de bord présente une vue d’ensemble de l’état des règles, ce qui vous permet de montrer plus facilement votre progression. 

Pour affiner la vue, utilisez les filtres suivants en haut du tableau de bord :
- Afficher les tâches terminées
- Facultatif
- Recommandé
- Critique

Le tableau de bord comprend les vignettes suivantes :  

- **Index des insights de gestion** : Suit la progression globale des règles d’insights de gestion. L’index est une moyenne pondérée. Les règles critiques sont celles qui comptent le plus. Les règles facultatives sont celles qui ont le moins de poids.  

- **Groupes d’insights de gestion** : Indique le pourcentage des règles dans chaque groupe, en respectant les filtres. Sélectionnez un groupe pour explorer les règles spécifiques de ce groupe.  

- **Priorité des insights de gestion** : Indique le pourcentage des règles par priorité, en respectant les filtres.   

- **Tous les insights** : Tableau des insights comprenant la priorité et l’état. Utilisez le champ **Filtre** situé en haut du tableau pour rechercher des chaînes dans les colonnes disponibles. Le tableau de bord trie les colonnes du tableau dans l’ordre suivant :
    - État : Action nécessaire, Terminé, Inconnu  
    - Priorité : Critique, Recommandé, Facultatif  
    - Dernière modification : les dates les plus anciennes se trouvent en haut de la liste   

![Capture d’écran du tableau de bord Insights de gestion](media/1357979-management-insights-dashboard.png)



## <a name="groups-and-rules"></a>Groupes et règles

Les règles sont organisées dans les groupes d’insights de gestion suivants :
- [Applications](#applications)  
- [Services cloud](#cloud-services)  
- [Regroupements](#collections)  
- [Maintenance proactive](#proactive-maintenance)  
- [Security](#security)  
- [Gestion simplifiée](#simplified-management)  
- [Centre logiciel](#software-center)  
- [Windows 10](#windows-10)  


### <a name="applications"></a>Applications

Insights pour la gestion de votre application.

- **Applications sans déploiements** : Répertorie les applications de votre environnement qui n’ont pas de déploiements actifs. Cette règle facilite la recherche et la suppression des applications inutilisées pour simplifier la liste des applications affichées dans la console. Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).  


### <a name="cloud-services"></a>Services cloud

Vous permet d’intégrer de nombreux services cloud et d’activer ainsi la gestion moderne de vos appareils. 

- **Évaluer la préparation de la cogestion** : Vous aide à comprendre les étapes nécessaires pour activer la cogestion. Cette règle comporte des prérequis. Pour plus d’informations, consultez [Vue d’ensemble de la cogestion](/sccm/comanage/overview).  

- **Configurer les services Azure à utiliser avec Configuration Manager** : Cette règle vous permet d’intégrer Configuration Manager à Azure AD, ce qui permet aux clients de s’authentifier auprès du site à l’aide d’Azure AD. Pour plus d’informations, consultez [Configurer des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).  

- **Autoriser les appareils à avoir une jonction hybride à Azure Active Directory** : Les appareils joints à Azure AD permettent aux utilisateurs de se connecter avec leurs informations d’identification de domaine tout en garantissant que les appareils répondent aux normes de conformité et de sécurité de l’organisation. Pour plus d’informations, consultez [Considérations relatives à la conception d’identités hybrides Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview).  

- **Mettre à jour les clients avec la dernière version de Windows 10** : Windows 10 version 1709 ou ultérieure améliore et modernise l’expérience informatique de vos utilisateurs. Pour plus d’informations, consultez [Rubriques importantes sur l’adoption de Windows en tant que service](/sccm/core/understand/configuration-manager-and-windows-as-service#key-articles-about-adopting-windows-as-a-service).  


### <a name="collections"></a>Regroupements

Insights qui permettent de simplifier la gestion par le nettoyage et la reconfiguration de regroupements.

- **Regroupements vides** : Répertorie les regroupements de votre environnement qui n’ont aucun membre. Pour plus d’informations, consultez [Guide pratique pour gérer des regroupements](/sccm/core/clients/manage/collections/manage-collections).  


### <a name="proactive-maintenance"></a>Maintenance proactive
<!--1352184-->
Depuis la version 1806, les règles de ce groupe mettent en évidence les éventuels problèmes de configuration que vous pouvez éviter en effectuant la maintenance des objets Configuration Manager. 

- **Groupes de limites sans système de site attribué** : Sans systèmes de site attribué, les groupes de limites ne peuvent être utilisés que pour l’attribution de site. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Groupes de limites sans membres** : Les groupes de limites ne sont pas applicables à l’attribution de site ou à la recherche de contenu s’ils n’ont aucun membre. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

- **Points de distribution ne distribuant pas de contenu aux clients** : Points de distribution n’ayant pas distribué de contenu aux clients au cours des 30 derniers jours. Ces données s’appuient sur les rapports d’historique de téléchargement des clients. Pour plus d'informations, consultez [Installer et configurer des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).  

- **Activer le nettoyage de WSUS** : Vérifie que vous avez activé l’option permettant d’exécuter le nettoyage de WSUS sur les propriétés de composant du point de mise à jour logicielle. Cette option contribue à améliorer les performances de WSUS. Pour plus d’informations, consultez [Maintenance des mises à jour logicielles](/sccm/sum/deploy-use/software-updates-maintenance).  

- **Images de démarrage inutilisées** : Images de démarrage non référencées pour l’utilisation de séquences de tâches ou le démarrage PXE. Pour plus d’informations, consultez [Gérer les images de démarrage](/sccm/osd/get-started/manage-boot-images).  

- **Éléments de configuration inutilisés** : Éléments de configuration qui ne font pas partie d’une base de référence de configuration et datent de plus de 30 jours. Pour plus d’informations, consultez [Créer des bases de référence de configuration](/sccm/compliance/deploy-use/create-configuration-baselines).  

- **Mettre à niveau les sources de cache de pair avec la dernière version du client Configuration Manager** : Identifier les clients qui servent de source de cache d’homologue mais qui n’ont pas été mis à niveau depuis une version cliente antérieure à 1806. Les clients antérieurs à 1806 ne peuvent pas être utilisés en tant que source de cache d’homologue pour les clients qui exécutent la version 1806 ou une version ultérieure. Sélectionnez **Prendre des mesures** pour ouvrir une vue d’appareil qui affiche la liste des clients.<!--1358008-->  


### <a name="security"></a>Sécurité
Insights pour améliorer la sécurité de votre infrastructure et de vos appareils. 

- **Versions de client logiciel anti-programme malveillant non prises en charge** : Plus de 10 % des clients exécutent des versions de System Center Endpoint Protection qui ne sont pas prises en charge. Pour plus d’informations, consultez [Endpoint Protection](/sccm/protect/deploy-use/endpoint-protection).  


### <a name="simplified-management"></a>Gestion simplifiée

Insights qui vous aident à simplifier la gestion quotidienne de votre environnement. 

- **Versions de client non-CB** : Répertorie tous les clients dont les versions ne sont pas une version CB (Current Branch) actuelle. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients).  


### <a name="software-center"></a>Centre logiciel

Insights pour la gestion du Centre logiciel. 

- **Diriger les utilisateurs vers le Centre logiciel au lieu du catalogue d’applications** : Vérifiez si les utilisateurs ont installé ou demandé des applications provenant du catalogue d’applications au cours des 14 derniers jours. La fonctionnalité principale du catalogue d’applications est désormais incluse dans le Centre logiciel. La prise en charge du site web du catalogue d’applications a pris fin avec la version 1806. Pour plus d’informations, consultez [Fonctionnalités dépréciées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures#deprecated-features).  

- **Utiliser la nouvelle version du Centre logiciel** : L’ancienne version du Centre logiciel n’est plus prise en charge. Configurez les clients pour qu’ils utilisent le nouveau Centre logiciel en activant le paramètre client **Utiliser le nouveau Centre logiciel** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#use-new-software-center).  


### <a name="windows-10"></a>Windows 10

Insights liés au déploiement et à la maintenance de Windows 10. Le groupe d’insights de gestion Windows 10 est disponible uniquement quand plus de la moitié des clients exécutent Windows 7, Windows 8 ou Windows 8.1.

- **Configurer la télémétrie et la clé d’ID commercial de Windows** : Pour utiliser des données d’Upgrade Readiness, configurez les appareils avec une clé d’ID commercial et activez la télémétrie. Affectez aux appareils Windows 10 un niveau de télémétrie supérieur ou égal à Avancé (limité). Pour plus d’informations, consultez [Configurer les clients pour envoyer des données à Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).  

- **Connecter Configuration Manager à Upgrade Readiness** : Tirez parti d'Upgrade Readiness pour accélérer vos déploiements de Windows 10 avant la fin de support de Windows 7. Pour plus d’informations, consultez [Intégrer Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).   

#### <a name="windows-10-management-insights-rules"></a>Règles d’insights de gestion Windows 10
![Insights de gestion : règles pour Windows 10](./media/Windows-10-insights-group.png)
