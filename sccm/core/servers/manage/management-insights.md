---
titleSuffix: Configuration Manager
description: Découvrez plus en détail la fonctionnalité Insights de gestion disponible dans la console Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a79f83be-884c-48e6-94d6-ed0a68c22e2f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ded020bd654672bb6133c9aad15478c22498ab7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="management-insights-in-system-center-configuration-manager"></a>Insights de gestion dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les insights de gestion dans System Center Configuration Manager fournissent des informations sur l’état actuel de votre environnement. Les informations sont basées sur l’analyse des données provenant de la base de données du site. Ces informations vous aident à mieux comprendre votre environnement et à prendre des mesures en fonction de ces renseignements. Cette fonctionnalité a été publiée dans Configuration Manager version 1802. <!--1353967-->

## <a name="review-management-insights-in-the-configuration-manager-console"></a>Examiner les insights de gestion dans la console Configuration Manager 
L’autorisation de **lecture sur le site**  est nécessaire pour afficher les règles.

1. Ouvrez la console Configuration Manager. 
2. Accédez au nœud **Administration** et cliquez sur **Insights de gestion**.
3. Sélectionnez **Tous les insights**
4. Double-cliquez sur le **Nom du groupe d’insights de gestion** que vous souhaitez examiner. Vous pouvez également le mettre en surbrillance et cliquer sur **Afficher les insights** dans le ruban. 
5. Quatre onglets sont disponibles pour l’examen, ainsi que les prérequis nécessaires pour exécuter la règle. 
    - **Toutes les règles** : affiche la liste complète des règles pour le groupe d’insights de gestion choisi.
    - **Terminé** : liste les règles quand aucune action n’est nécessaire. 
    - **En cours** : affiche les règles quand certains prérequis, mais pas tous, sont remplis.
    - **Action nécessaire** : les règles nécessitant la prise de mesures sont listées. Cliquez avec le bouton droit et sélectionnez **Plus de détails** pour récupérer des éléments spécifiques quand une action est nécessaire. 
    - **Prérequis** : si une règle a besoin d’éléments terminés avant qu’ils ne puissent être exécutés, les éléments nécessaires sont affichés ici.   
    
    **Ensemble des règles et prérequis pour le groupe de services cloud** ![Insights de gestion - Ensemble des règles et prérequis pour le groupe de services cloud](./media/Management-insights-all-cloud-rules.png)

## <a name="management-insights-reevaluation-and-logging"></a>Réévaluation et journalisation des insights de gestion
Les règles des insights de gestion réévaluent leur mise en application selon une planification hebdomadaire. Vous pouvez réévaluer une règle à la demande en cliquant avec le bouton droit sur la règle et en sélectionnant **Réévaluer**.

**Fichier journal pour les règles des insights de gestion** : SMS_DataEngine.log
## <a name="management-insights-groups-and-rules"></a>Règles et groupes d’insights de gestion
Les règles sont organisées en différents groupes d’insights de gestion. Le cas échéant, les groupes et les règles sont ajoutés à la liste suivante :

**Applications** : insights pour la gestion de votre application.

- **Applications sans déploiements** : répertorie les applications de votre environnement qui n’ont pas de déploiements actifs. Cette règle facilite la recherche et la suppression des applications inutilisées pour simplifier la liste des applications affichées dans la console. 

**Services cloud** : vous permet d’intégrer de nombreux services cloud ; activation de la gestion moderne de vos appareils. 
 - **Évaluer la préparation de la cogestion** : vous aide à comprendre les étapes nécessaires pour activer la cogestion. Cette règle comporte des prérequis. 
 - **Permettre à vos appareils d’être hybrides joints à Azure Active Directory** : les appareils joints à Azure AD permettent aux utilisateurs de se connecter avec leurs informations d’identification de domaine tout en garantissant que les appareils répondent aux normes de conformité et de sécurité de l’organisation. 
 - **Moderniser votre infrastructure d’identité et d’accès** : le service cloud Azure AD avec l’authentification multifacteur intégrée protège les données sensibles et les applications à la fois localement et dans le cloud. 
 - **Mettre à niveau vos clients vers Windows 10, version 1709 ou ultérieure** : Windows 10 version 1709 ou ultérieure améliore et modernise l’expérience informatique de vos utilisateurs. 


**Regroupements** : insights qui permettent de simplifier la gestion par le nettoyage et la reconfiguration de regroupements.
   - **Regroupements vides** : répertorie les regroupements de votre environnement qui n’ont aucun membre. 

**Gestion simplifiée** : insights qui permettent de simplifier la gestion quotidienne de votre environnement. 
   - **Versions des clients obsolètes** : répertorie tous les clients dont les versions sont antérieures à deux ans. 

**Centre logiciel** : insights pour la gestion du Centre logiciel. 
   - **Diriger les utilisateurs vers le Centre logiciel au lieu du catalogue d’applications** : vérifiez si les utilisateurs ont installé ou demandé des applications provenant du catalogue d’applications au cours des 14 derniers jours. La fonctionnalité principale du catalogue d’applications est désormais incluse dans le Centre logiciel. La prise en charge du site web du catalogue d’applications prend fin avec la première mise à jour publiée après le 1er juin 2018
   - **Utiliser la nouvelle version du Centre logiciel** : la version précédente du Centre logiciel n’est plus prise en charge. Configurez les clients pour qu’ils utilisent le nouveau Centre logiciel en activant le paramètre client **Agent ordinateur** >**Utiliser le nouveau Centre logiciel**.

**Windows 10** : insights sur le déploiement et la maintenance de Windows 10. Le groupe d’insights de gestion Windows 10 est disponible quand plus de la moitié des clients exécutent Windows 7, Windows 8 ou Windows 8.1.
   - **Configurer la télémétrie et la clé d’ID commercial de Windows** : pour utiliser des données d’Upgrade Readiness, les appareils doivent être configurés avec une clé d’ID commercial et la télémétrie doit être activée. Les appareils Windows 10 doivent avoir un niveau de télémétrie supérieur ou égal à Avancé (limité).
   - **Connecter Configuration Manager à Upgrade Readiness** : tirez parti d’Upgrade Readiness pour accélérer vos déploiements de Windows 10 avant la fin de la prise en charge de Windows 7. **Configurer la télémétrie et la clé d’ID commercial de Windows** est un prérequis.

     **Règles d’insights de gestion Windows 10**
    ![Insights de gestion - Règles pour Windows 10](./media/Windows-10-insights-group.png)
    