---
title: Liste des rapports
titleSuffix: Configuration Manager
description: Passez en revue la liste des rapports fournis avec Configuration Manager. Les rapports sont répartis dans différentes catégories.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b7332ed3-8003-454b-bb12-1fdf8721425c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9f4bbb8ec680248b31b1ddd8c457e62e9be44d4b
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385256"
---
# <a name="list-of-reports-in-system-center-configuration-manager"></a>Liste des rapports dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager fournit de nombreux rapports intégrés couvrant une grande partie des tâches de création de rapports que vous pourriez souhaiter effectuer. Vous pouvez également utiliser les instructions SQL dans ces rapports pour vous aider à rédiger vos propres rapports.   

Les rapports suivants sont fournis avec Configuration Manager. Les rapports sont répartis dans différentes catégories.  



## <a name="administrative-security"></a>Sécurité administrative  
 Les six rapports suivants sont répertoriés sous la catégorie **Sécurité administrative**.  

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Journal des activités d'administration**|Affiche un enregistrement des modifications administratives apportées aux utilisateurs administratifs, aux rôles de sécurité, aux étendues de sécurité et aux regroupements.|  
|**Utilisateurs administratifs et affectations de sécurité**|Affiche les utilisateurs administratifs, leurs rôles de sécurité associés et les étendues de sécurité associées à chaque rôle de sécurité pour chaque utilisateur.|  
|**Objets sécurisés par une seule étendue de sécurité**|Affiche les objets assignés par un administrateur à l’étendue de sécurité spécifiée uniquement. Ce rapport n’affiche pas les objets qui sont associés par un administrateur à plusieurs étendues de sécurité.|  
|**Sécurité pour un ou plusieurs objets Configuration Manager**|Affiche les objets sécurisables, les étendues de sécurité associées aux objets et les utilisateurs administratifs qui ont des droits sur les objets.|  
|**Récapitulatif des rôles de sécurité**|Affiche les rôles de sécurité et les administrateurs Configuration Manager associés à chaque rôle.|  
|**Récapitulatif des étendues de sécurité**|Affiche les étendues de sécurité, les utilisateurs administratifs Configuration Manager et les groupes de sécurité associés à chaque étendue.|  



## <a name="alerts"></a>Alertes  
Les deux rapports suivants sont répertoriés sous la catégorie **Alertes**.  
|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tableau de bord des alertes**|Affiche la synthèse de toutes les alertes différées qui ont été générées entre les dates de début et de fin spécifiées.|  
|**Alertes générées le plus souvent**|Affiche la synthèse des alertes qui ont été générées le plus souvent depuis la date spécifiée jusqu'à ce jour pour le composant spécifié.|  



## <a name="asset-intelligence"></a>Asset Intelligence  
Les 62 rapports suivants sont répertoriés sous la catégorie **Asset Intelligence**.  

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Matériel 01A - Synthèse des ordinateurs d'un regroupement spécifique**|Affiche la vue de synthèse d'Asset Intelligence des ordinateurs inclus dans un regroupement que vous spécifiez.|  
|**Matériel 03A - Utilisateurs d'ordinateurs principaux**|Affiche les utilisateurs et le nombre d'ordinateurs sur lesquels ils sont l'utilisateur principal.|  
|**Matériel 03B - Ordinateurs d'un utilisateur de console principal spécifique**|Affiche tous les ordinateurs pour lesquels un utilisateur spécifié est l'utilisateur principal de la console.|  
|**Matériel 04A - Ordinateurs avec plusieurs utilisateurs (partagés)**|Affiche les ordinateurs qui n'ont pas d'utilisateur principal car aucun utilisateur n'a un pourcentage de temps de connexion à la console supérieur à 66 %.|  
|**Matériel 05A - Utilisateurs de la console sur un ordinateur spécifique**|Affiche tous les utilisateurs de la console sur un ordinateur spécifié.|  
|**Matériel 06A - Ordinateurs pour lesquels aucun utilisateur de console n'a pu être déterminé**|Aide les utilisateurs administratifs à identifier les ordinateurs pour lesquels la journalisation de sécurité doit être activée.|  
|**Matériel 07A - Périphériques USB par fabricant**|Affiche les périphériques USB, regroupés par fabricant.|  
|**Matériel 07B - Périphériques USB par fabricant et description**|Affiche les périphériques USB, regroupés par fabricant et description.|  
|**Matériel 07C - Ordinateurs munis d'un périphérique USB spécifique**|Affiche tous les ordinateurs munis d'un périphérique USB spécifié.|  
|**Matériel 07D - Périphériques USB sur un ordinateur spécifique**|Affiche tous les périphériques USB sur un ordinateur spécifié.|  
|**Matériel 08A - Matériel qui n'est pas prêt pour une mise à niveau logicielle**|Affiche le matériel qui ne satisfait pas à la configuration matérielle minimale requise.|  
|**Matériel 09A - Recherche d'ordinateurs**|Affiche une synthèse des ordinateurs correspondant aux filtres de mots clés. Ces filtres sont le nom d’ordinateur, le site Configuration Manager, le domaine, l’utilisateur principal de la console, le système d’exploitation, le fabricant ou le modèle.|  
|**Matériel 10A - Ordinateurs d'un regroupement spécifié qui ont été modifiés pendant un laps de temps spécifié**|Affiche la liste des ordinateurs inclus dans un regroupement spécifié où une classe de matériel a changé pendant une période spécifiée.|  
|**Matériel 10B - Modifications apportées à un ordinateur spécifié pendant un laps de temps spécifié**|Affiche les classes qui ont changé sur l'ordinateur spécifié pendant un laps de temps spécifié.|  
|**Licence 01A - Grand livre des licences en volume Microsoft pour les relevés de licences Microsoft**|Affiche un inventaire de tous les logiciels Microsoft qui sont disponibles à partir du programme de licence en volume Microsoft.|  
|**Licence 01B - Élément du Grand livre des licences en volume Microsoft par canal de vente**|Identifie et affiche le canal de vente des logiciels de licence en volume Microsoft inventoriés.|  
|**Licence 01C - Ordinateurs possédant un élément du Grand livre des licences en volume Microsoft et canaux de vente**|Identifie et affiche les ordinateurs qui ont un élément spécifié du Grand livre des licences en volume Microsoft.|  
|**Licence 01D - Produits du Grand livre des licences en volume Microsoft sur un ordinateur spécifique**|Identifie et affiche tous les éléments du Grand livre des licences en volume Microsoft sur un ordinateur spécifié.|  
|**Licence 02A - Nombre de licences arrivant à expiration par périodes**|Affiche le nombre de licences arrivant à expiration pour une période spécifiée. Les produits affichés ont leur licence gérée par le service de gestion de licences des logiciels.|  
|**Licence 02B - Ordinateurs dont les licences arrivent à expiration**|Affiche les ordinateurs dont les licences arrivent à expiration.|  
|**Licence 02C - Informations de licence sur un ordinateur spécifique**|Affiche les produits sur un ordinateur spécifié dont les licences sont gérées par le service de gestion de licences des logiciels.|  
|**Licence 03A - Nombre de licences par état de licence**|Affiche les produits, par état de licence, dont les licences sont gérées par le service de gestion de licences des logiciels.|  
|**Licence 03B - Ordinateurs avec un état de licence spécifique**|Affiche les produits, avec un état de licence spécifié, dont les licences sont gérées par le service de gestion de licences des logiciels.|  
|**Licence 04A - Nombre de produits gérés par le service de gestion de licences des logiciels**|Affiche le nombre de produits dont les licences sont gérées par le service de gestion de licences des logiciels.|  
|**Licence 04B - Ordinateurs présentant un produit spécifique géré par le service de gestion des licences**|Affiche les ordinateurs, gérés par le service de gestion de licences des logiciels, qui contiennent un produit donné.|  
|**Licence 05A - Ordinateurs agissant en tant que service de gestion de clés**|Affiche les ordinateurs qui agissent en tant que serveurs de gestion de clés.|  
|**Licence 06A - Nombre de processeurs pour les produits avec une licence par processeur**|Affiche le nombre total de processeurs sur des ordinateurs qui utilisent des produits Microsoft prenant en charge la gestion des licences pour chaque processeur.|  
|**Licence 06B - Ordinateurs équipés d'un produit spécifique prenant en charge la gestion des licences par processeur**|Affiche la liste des ordinateurs sur lesquels est installé un produit Microsoft spécifié qui prend en charge la gestion des licences par processeur.|  
|**Licence 14A - Rapport de rapprochement des licences en volume Microsoft**|Affiche le rapprochement entre les licences logicielles achetées via le contrat de licence en volume Microsoft et le nombre réel de logiciels.|  
|**Licence 14B - Liste des logiciels Microsoft introuvables dans MVLS**|Ce rapport affiche les logiciels Microsoft en cours d'utilisation qui ne figurent pas dans le contrat de licence en volume Microsoft.|  
|**Licence 15A - Rapport de rapprochement des licences générales**|Affiche le rapprochement entre les licences logicielles générales achetées et le nombre réel de logiciels.|  
|**Licence 15B - Rapport de rapprochement des licences générales par ordinateur**|Affiche les ordinateurs qui ont installé le produit sous licence avec une version spécifiée.|  
|**Logiciel 01A - Synthèse des logiciels installés dans un regroupement spécifique**|Affiche la synthèse des logiciels installés, classés par nombre d'instances, répertoriés dans l'inventaire.|  
|**Logiciel 02A - Familles de produits pour un regroupement spécifique**|Affiche les familles de produits et le nombre de logiciels dans la famille pour un regroupement spécifié.|  
|**Logiciel 02B - Catégories de produits pour une famille de produits spécifique**|Affiche les catégories de produits dans une famille de produits spécifiée et le nombre de logiciels au sein de la catégorie.|  
|**Logiciel 02C - Logiciels dans une famille et une catégorie de produits spécifiques**|Affiche tous les logiciels qui se trouvent dans la famille et la catégorie de produits spécifiées.|  
|**Logiciel 02D - Ordinateurs équipés de logiciels spécifiques**|Affiche tous les ordinateurs sur lesquels sont installés les logiciels spécifiés.|  
|**Logiciel 02E - Logiciels installés sur un ordinateur spécifique**|Ce rapport affiche tous les logiciels installés sur un ordinateur spécifié.|  
|**Logiciel 03A - Logiciels sans catégorie**|Affiche les logiciels dont la catégorie est inconnue ou qui n'ont aucune catégorie.|  
|**Logiciel 04A - Logiciels configurés pour s'exécuter automatiquement sur les ordinateurs**|Affiche la liste des logiciels configurés pour s'exécuter automatiquement sur les ordinateurs.|  
|**Logiciel 04B - Ordinateurs dotés de logiciels spécifiques configurés pour s'exécuter automatiquement**|Affiche tous les ordinateurs dotés de logiciels spécifiques configurés pour s'exécuter automatiquement|  
|**Logiciel 04C - Logiciels configurés pour s'exécuter automatiquement sur un ordinateur spécifique**|Affiche les logiciels installés et configurés pour s'exécuter automatiquement sur un ordinateur spécifié.|  
|**Logiciel 05A - Objets d'assistance du navigateur**|Affiche les objets d’assistance du navigateur installés sur les ordinateurs dans un regroupement spécifié.|  
|**Logiciel 05B - Ordinateurs équipés d'un objet d'assistance du navigateur spécifique**|Affiche tous les ordinateurs équipés d’un objet d’assistance du navigateur spécifié.|  
|**Logiciel 05C - Objets d'assistance du navigateur sur un ordinateur spécifique**|Affiche tous les objets d’assistance du navigateur sur l’ordinateur spécifié.|  
|**Logiciel 06A - Recherche des logiciels installés**|Ce rapport fournit un récapitulatif des logiciels installés. La recherche est effectuée selon les critères suivants : nom du produit, éditeur ou version.|  
|**Logiciel 06B - Logiciels par nom de produit**|Affiche une synthèse des logiciels installés selon un nom de produit spécifié.|  
|**Logiciel 07A - Programmes exécutables récemment utilisés par nombre d'ordinateurs**|Affiche les programmes exécutables que les utilisateurs ont récemment employés. Il inclut également le nombre d’ordinateurs sur lesquels le programme a été utilisé. Le contrôle de logiciel doit être activé pour que ce site affiche ce rapport.|  
|**Logiciel 07B - Ordinateurs ayant récemment utilisé un programme exécutable spécifié**|Affiche les ordinateurs sur lesquels un programme exécutable spécifié a récemment été utilisé. Ce rapport exige que vous activiez le paramètre client de contrôle de logiciel.|  
|**Logiciel 07C - Programmes exécutables récemment utilisés sur un ordinateur spécifié**|Affiche les fichiers exécutables qui ont été récemment utilisés sur un ordinateur spécifié. Ce rapport exige que vous activiez le paramètre client de contrôle de logiciel.|  
|**Logiciel 08A - Programmes exécutables récemment utilisés par nombre d'utilisateurs**|Affiche les programmes exécutables que les utilisateurs ont récemment employés. Il inclut également un nombre d’utilisateurs qui les ont utilisés le plus récemment. Ce rapport exige que vous activiez le paramètre client de contrôle de logiciel.|  
|**Logiciel 08B - Utilisateurs ayant récemment utilisé un programme exécutable spécifié**|Affiche les utilisateurs qui ont le plus récemment utilisé un programme exécutable spécifié. Ce rapport exige que vous activiez le paramètre client de contrôle de logiciel.|  
|**Logiciel 08C - Programmes exécutables récemment utilisés par un utilisateur spécifié**|Affiche les programmes exécutables récemment utilisés par l’utilisateur spécifié. Ce rapport exige que vous activiez le paramètre client de contrôle de logiciel.|  
|**Logiciel 09A - Logiciels rarement utilisés**|Affiche les noms des logiciels qui n’ont pas été utilisés pendant une certaine période.|  
|**Logiciel 09B - Ordinateurs sur lesquels sont installés des logiciels rarement utilisés**|Affiche les ordinateurs sur lesquels sont installés des logiciels qui n’ont pas été utilisés pendant une certaine période. La période spécifiée se base sur la valeur spécifiée dans le rapport « Logiciel 09A - Logiciels rarement utilisés ».|  
|**Logiciel 10A - Titres des logiciels avec plusieurs légendes personnalisées spécifiques définies**|Affiche les titres des logiciels selon leur correspondance à tous les critères de légende personnalisée spécifiés. Il est possible de sélectionner jusqu'à trois légendes personnalisées pour affiner une recherche de titre de logiciel.|  
|**Logiciel 10B - Ordinateurs équipés d'un logiciel avec une légende personnalisée spécifique**|Affiche tous les ordinateurs d'un regroupement sur lesquels est installé un logiciel spécifique avec une légende personnalisée.|  
|**Logiciel 11A - Titres des logiciels avec une légende personnalisée spécifique définie**|Affiche les titres des logiciels selon leur correspondance à au moins un des critères de légende personnalisée spécifiés.|  
|**Software 12A - Titres des logiciels sans légende personnalisée**|Affiche tous les titres des logiciels qui n'ont pas de légende personnalisée définie.|  
|**Logiciel 14A - Recherche de logiciels dont la balise d'identification logicielle est activée**|Affiche le nombre de logiciels installés dont la balise d'identification logicielle est activée.|  
|**Logiciel 14B - Ordinateurs sur lesquels sont installés des logiciels dont la balise d'identification logicielle est activée**|Affiche tous les ordinateurs sur lesquels sont installés des logiciels qui ont une balise d'identification logicielle spécifique activée.|  
|**Logiciel 14C - Logiciels installés sur un ordinateur spécifique et dont la balise d'identification logicielle est activée**|Affiche tous les logiciels installés qui ont une balise d'identification logicielle spécifiée activée sur un ordinateur spécifié.|  



## <a name="client-push"></a>Installation Push du client  
Les quatre rapports suivants sont répertoriés sous la catégorie **Push client**.  

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Détails de l'état de l'installation Push du client**|Affiche des informations sur le processus d'installation Push du client pour tous les sites.|  
|**Détails de l'état de l'installation Push du client pour un site spécifié**|Affiche des informations sur le processus d'installation Push du client pour un site spécifié.|  
|**Synthèse de l'état de l'installation Push du client**|Affiche la synthèse de l'état de l'installation Push du client pour tous les sites.|  
|**Synthèse de l'état de l'installation Push du client pour un site spécifié**|Affiche la synthèse de l'état de l'installation Push du client pour un site spécifié.|  



## <a name="client-status"></a>État du client  
Les sept rapports suivants sont répertoriés sous la catégorie **État du client**.  

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Détails des corrections du client**|Affiche les détails des actions de correction du client pour un regroupement que vous spécifiez.|  
|**Synthèse des corrections du client**|Affiche la synthèse des actions de correction du client pour un regroupement spécifié.|  
|**Historique de l'état du client**|Affiche l'historique de l'état général du client dans le site.|  
|**Résumé de l'état du client**|Affiche les résultats de la vérification des clients actifs pour un regroupement donné.|  
|**Temps client pour demande de stratégie**|Affiche le pourcentage de clients qui ont demandé une stratégie au moins une fois au cours des 30 derniers jours. Chaque jour représente un pourcentage du nombre total de clients qui ont demandé une stratégie depuis le premier jour du cycle.|  
|**Clients avec détails des clients sains ayant échoué**|Affiche des détails sur les clients pour lesquels la vérification de l'intégrité a échoué pour un regroupement spécifié.|  
|**Détails des clients inactifs**|Affiche la liste détaillée des clients inactifs pour un regroupement donné.|  



## <a name="company-resource-access"></a>Accès aux ressources d'entreprise  
Les trois rapports suivants sont répertoriés sous la catégorie **Accès aux ressources de l'entreprise**. 

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Historique d'émission des certificats**|Affiche l’historique des certificats émis par le point d’enregistrement de certificat pour les utilisateurs et appareils pendant la plage de dates spécifiée.|  
|**Liste de biens par état d'émission de certificat**|Affiche les appareils ou utilisateurs qui sont dans un état d'émission de certificat spécifié à la suite de l'évaluation d'un profil de certificat spécifié.|  
|**Liste de biens dont la date d'expiration des certificats approche**|Affiche les appareils ou utilisateurs qui ont des certificats qui expirent à la date spécifiée ou avant.|  



## <a name="compliance-and-settings-management"></a>Gestion de la conformité et des paramètres  
Les 22 rapports suivants sont répertoriés sous la catégorie **Gestion de la conformité et des paramètres**. 

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Historique des compatibilités d'une ligne de base de configuration**|Affiche l'historique des modifications apportées aux compatibilités d'une ligne de base de configuration pendant la plage de dates spécifiée.|  
|**Historique des compatibilités d'un élément de configuration**|Affiche l'historique des modifications apportées aux compatibilités d'un élément de configuration pendant la plage de dates spécifiée.|  
|**Conformité de l’accès conditionnel pour l’utilisateur**|Affiche la conformité de l’accès conditionnel détaillée pour un utilisateur spécifique.|
|**Rapport de conformité de l’accès conditionnel**|Rapport de conformité de l’accès conditionnel pour chaque stratégie de conformité ciblée.|
|**Détails des règles de compatibilité des éléments de configuration dans la ligne de base de configuration d'un composant**|Affiche des informations sur les règles évaluées comme compatibles pour un élément de configuration spécifié pour un appareil ou un utilisateur spécifié.|  
|**Détails des règles en conflit pour les éléments de configuration de la ligne de base de configuration d'un composant**|Affiche des informations sur les règles d’un élément de configuration déployé en conflit avec d’autres règles. Les autres règles peuvent être contenues dans le même élément de configuration déployé ou dans un autre.|  
|**Détails des erreurs des éléments de configuration dans la ligne de base de configuration d'un composant**|Affiche des informations sur les erreurs générées par un élément de configuration spécifié pour un utilisateur ou un périphérique spécifié.|  
|**Détails des règles de non-compatibilité des éléments de configuration dans la ligne de base de configuration d'un composant**|Affiche des informations sur les règles évaluées comme non compatibles pour un élément de configuration spécifié, pour un périphérique ou un utilisateur spécifié.|  
|**Détails des règles corrigées des éléments de configuration dans la ligne de base de configuration d'un composant**|Affiche des informations sur les règles corrigées par un élément de configuration spécifié pour un utilisateur ou un périphérique spécifié.|  
|**Liste des composants par état de compatibilité d'une ligne de base de configuration**|Affiche les périphériques ou utilisateurs d'un état de compatibilité spécifié selon l'évaluation d'une ligne de base de configuration spécifié.|  
|**Liste des composants par état de compatibilité pour un élément de configuration d'une ligne de base de configuration**|Affiche les périphériques ou utilisateurs d'un état de compatibilité spécifié selon l'évaluation d'un élément de configuration spécifié.|  
|**Liste d'applications et de périphériques non conformes pour un utilisateur spécifié**|Affiche des informations sur les utilisateurs et les périphériques qui ont installé des applications non conformes avec une stratégie que vous avez spécifiée.|  
|**Liste des règles en conflit avec la règle spécifique d'un composant**|Affiche une liste de règles qui sont en conflit avec une règle spécifiée pour un élément de configuration déployé.|  
|**Liste des composants inconnus d'une ligne de base de configuration**|Affiche la liste des périphériques ou utilisateurs qui n'ont pas encore renvoyé de données de compatibilité pour une ligne de base de configuration spécifiée.|  
|**Liste des composants inconnus d'un élément de configuration**|Affiche la liste des périphériques ou utilisateurs qui n'ont pas encore renvoyé de données de compatibilité pour un élément de configuration spécifié.|  
|**Résumé des règles et des erreurs des éléments de configuration dans une ligne de base de configuration d'un composant**|Affiche une synthèse de l’état de compatibilité des règles et toutes les erreurs de réglage pour un élément de configuration spécifié. L’élément de configuration doit être déployé sur un appareil ou utilisateur.|  
|**Résumé de conformité par ligne de base de configuration**|Affiche le résumé de la compatibilité générale des lignes de base de configuration déployées dans la hiérarchie.|  
|**Résumé de compatibilité par élément de configuration pour une ligne de base de configuration**|Affiche le résumé de la compatibilité des éléments de configuration dans une ligne de base de configuration spécifiée.|  
|**Résumé de la conformité par stratégies de configuration**|Affiche le résumé de la conformité des stratégies de configuration.|  
|**Résumé de la compatibilité de la ligne de base de configuration d'un regroupement**|Affiche une synthèse de la compatibilité générale d’une base de référence de configuration spécifiée. L’élément de configuration doit être déployé sur le regroupement spécifié.|  
|**Résumé des utilisateurs ayant des applications non conformes**|Affiche des informations sur les utilisateurs qui ont installé des applications non conformes avec une stratégie que vous avez spécifiée.|  
|**Acceptation des conditions générales**|Affiche les éléments des conditions générales et la version que chaque utilisateur a acceptés.|  



## <a name="device-management"></a>Gestion des appareils  
Les 37 rapports suivants sont répertoriés sous la catégorie **Gestion des périphériques**. 

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les appareils mobiles de l’entreprise**|Affiche tous les appareils mobiles de l’entreprise.|
|**Tous les clients de périphériques mobiles**|Affiche des informations sur tous les clients d’appareils mobiles. Les appareils qui sont gérés par le connecteur Exchange Server ne sont pas inclus.|  
|**Problèmes de certificat sur les périphériques mobiles gérés par le client Configuration Manager pour Windows CE et qui ne sont pas sains**|Affiche des informations détaillées sur les problèmes de certificat sur les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Échecs de déploiement du client pour les périphériques mobiles gérés par le client Configuration Manager pour Windows CE**|Affiche des informations détaillées sur les échecs de déploiement pour les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Détails sur l'état de déploiement du client pour les périphériques mobiles gérés par le client Configuration Manager pour Windows CE**|Affiche des informations sur l’état de déploiement pour les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Déploiements réussis du client pour les périphériques mobiles gérés par le client Configuration Manager pour Windows CE**|Affiche des informations détaillées sur la réussite du déploiement pour les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Problèmes de communication sur les périphériques mobiles gérés par le client Configuration Manager pour Windows CE et qui ne sont pas sains**|Ce rapport contient des informations détaillées sur les problèmes de communication sur les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**État de conformité de la stratégie de boîte aux lettres ActiveSync par défaut pour les appareils mobiles gérés par le connecteur du serveur Exchange Server**|Affiche une synthèse de l’état de compatibilité avec la stratégie de boîte aux lettres Exchange ActiveSync par défaut pour les appareils mobiles gérés par le connecteur du serveur Exchange Server.|  
|**Nombre de périphériques mobiles par configurations d'affichage**|Ce rapport affiche le nombre d’appareils mobiles par paramètres d'affichage.|  
|**Nombre de périphériques mobiles par système d'exploitation**|Affiche le nombre d’appareils mobiles par système d'exploitation.|  
|**Nombre de périphériques mobiles par mémoire programme**|Affiche le nombre d’appareils mobiles par mémoire programme.|  
|**Nombre de périphériques mobiles par configurations de mémoire de stockage**|Nombre d’appareils mobiles par configurations de mémoire de stockage|  
|**Informations d'intégrité détaillées pour les périphériques mobiles gérés par le client Configuration Manager pour Windows CE**|Affiche des informations d'intégrité détaillées pour les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Récapitulatif de l'intégrité pour les périphériques mobiles gérés par le client Configuration Manager pour Windows CE**|Affiche des informations de synthèse de l'intégrité pour les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Périphériques mobiles inactifs qui sont gérés par le connecteur du serveur Exchange Server**|Affiche les appareils mobiles qui sont gérés par le connecteur du serveur Exchange Server et qui ne se sont pas connectés à Exchange Server depuis un nombre de jours spécifié.|  
|**Liste des appareils par état d'accès conditionnel**|Affiche des informations sur la conformité actuelle et sur l'état d'accès conditionnel des appareils. Vous pouvez utiliser ce rapport avec les stratégies d'accès conditionnel. Ce rapport est disponible depuis la version 1602 de Configuration Manager.|  
|**Liste des appareils par état d’attestation d’intégrité**|Affiche une liste d’appareils avec des attributs signalés par le service d’attestation d’intégrité|
|**Liste des périphériques inscrits par utilisateur dans Windows Intune**|Affiche tous les appareils qu’un utilisateur a inscrits dans Microsoft Intune.|  
|**Liste des appareils d’une catégorie spécifique**|Affiche des informations sur tous les appareils d’une catégorie spécifique.|
|**Problèmes de client local sur les périphériques mobiles gérés par le client Configuration Manager pour Windows CE et qui ne sont pas sains**|Ce rapport contient des informations détaillées sur les problèmes de client local sur les appareils mobiles gérés par le client Configuration Manager pour Windows CE.|  
|**Informations sur le client de périphérique mobile**|Affiche des informations sur les appareils mobiles sur lesquels le client Gestionnaire de configuration est installé. Vous pouvez utiliser ce rapport pour vérifier quels appareils mobiles peuvent communiquer correctement avec un point de gestion.|  
|**Détails de la compatibilité des périphériques mobiles pour le connecteur du serveur Exchange Server**|Affiche les détails de compatibilité de l’appareil mobile pour une stratégie de boîte aux lettres Exchange ActiveSync par défaut qui est configurée à l'aide du connecteur du serveur Exchange Server.|  
|**Périphériques mobiles par système d'exploitation**|Affiche les appareils mobiles par système d'exploitation.|  
|**Appareils mobiles jailbroken ou rootés**|Affiche les appareils mobiles qui sont jailbreakés ou rootés.|  
|**Périphériques mobiles non gérés car inscrits mais non affectés à un site**|Affiche les appareils mobiles qui ont été inscrits dans Configuration Manager et qui possèdent un certificat, mais qui n’ont pas terminé l’attribution de site.|  
|**Périphériques mobiles et quantité spécifique de mémoire programme libre**|Affiche tous les appareils mobiles ainsi que la quantité spécifiée de mémoire programme libre.|  
|**Périphériques mobiles avec une quantité spécifique de mémoire de stockage amovible libre**|Affiche tous les appareils mobiles ainsi que la quantité spécifiée de mémoire amovible libre.|  
|**Périphériques mobiles rencontrant des problèmes de renouvellement de certificat**|Affiche les appareils mobiles inscrits qui n'ont pas réussi à renouveler leur certificat. Si vous ne renouvelez pas le certificat avant la période d’expiration, les appareils mobiles ne sont plus gérés.|  
|**Périphériques mobiles avec une mémoire programme faible (inférieure à l'espace libre spécifié en Ko)**|Affiche les appareils mobiles pour lesquels la mémoire programme est inférieure à une taille spécifiée en Ko.|  
|**Périphériques mobiles avec une mémoire de stockage amovible faible (inférieure à l'espace libre spécifié en Ko)**|Affiche les appareils mobiles pour lesquels la mémoire de stockage amovible est inférieure à une taille spécifiée en Ko.|  
|**Nombre d’appareils inscrits par utilisateur dans Microsoft Intune**|Affiche les utilisateurs activés pour l’abonnement Microsoft Intune. Il indique également le nombre total d’appareils inscrits pour chaque utilisateur.|  
|**Demandes de mise hors service et de réinitialisation en attente pour les appareils mobiles**|Affiche les demandes de nettoyage en attente pour des appareils mobiles.|  
|**Périphériques mobiles récemment inscrits et affectés**|Ce rapport affiche les appareils mobiles récemment inscrits dans Configuration Manager et affectés avec succès à un site.|  
|**Périphériques mobiles récemment nettoyés**|Affiche la liste des appareils mobiles récemment nettoyés avec succès.|  
|**Synthèse des paramètres pour les périphériques mobiles gérés par le connecteur du serveur Exchange Server**|Affiche le nombre d’appareils mobiles appliquant les paramètres pour chaque stratégie de boîte aux lettres Exchange ActiveSync par défaut gérée par le connecteur du serveur Exchange Server.|  
|**État détaillé de clés de chargement de version test Windows RT**|Affiche des informations d'état détaillées pour une clé de chargement de version test Windows RT spécifiée.|  
|**Résumé des clés de chargement de version test Windows RT**|Affiche l'état des clés de chargement de version test Windows RT.|  



## <a name="driver-management"></a>Gestion des pilotes  
Les 13 rapports suivants sont répertoriés sous la catégorie **Gestion des pilotes**. 

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les pilotes**|Affiche la liste de tous les pilotes.|  
|**Tous les pilotes pour une plateforme spécifique**|Affiche tous les pilotes pour une plateforme spécifiée.|  
|**Tous les pilotes d'une image de démarrage spécifique**|Affiche tous les pilotes d'une image de démarrage spécifiée.|  
|**Tous les pilotes d'une catégorie spécifique**|Affiche tous les pilotes d'une catégorie spécifiée.|  
|**Tous les pilotes d'un package spécifique**|Affiche tous les pilotes d'un package spécifié.|  
|**Catégories d'un pilote spécifique**|Affiche les catégories d'un pilote spécifié.|  
|**Ordinateurs qui n'ont pas pu installer des pilotes pour un regroupement spécifique**|Affiche les ordinateurs qui n'ont pas pu installer des pilotes pour un regroupement spécifique.|  
|**Rapport de correspondance du catalogue de pilotes pour un regroupement spécifique**|Affiche le rapport de correspondance du catalogue de pilotes pour un regroupement spécifié.|  
|**Rapport de correspondance du catalogue de pilotes pour un ordinateur spécifique**|Affiche le rapport de correspondance du catalogue de pilotes pour un ordinateur spécifié.|  
|**Rapport de correspondance du catalogue de pilotes pour un périphérique spécifique sur un ordinateur spécifique**|Affiche le rapport de correspondance du catalogue de pilotes pour un périphérique spécifique sur un ordinateur spécifique.|  
|**Rapport de correspondance du catalogue de pilotes pour les ordinateurs d'un regroupement spécifique avec un périphérique spécifique**|Affiche le rapport de correspondance du catalogue de pilotes pour les ordinateurs d'un regroupement spécifique avec un périphérique spécifique.|  
|**Pilotes dont l'installation a échoué sur un ordinateur spécifique**|Affiche les pilotes dont l'installation a échoué sur un ordinateur spécifique.|  
|**Plateformes prises en charge pour un pilote spécifique**|Affiche les plateformes prises en charge pour un pilote spécifié.|  



## <a name="endpoint-protection"></a>Endpoint Protection  
Les six rapports suivants sont répertoriés sous la catégorie **Endpoint Protection**. 
|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Rapport d'activité des logiciels anti-programme malveillant**|Affiche une vue d'ensemble de l'activité des logiciels anti-programme malveillant.|  
|**Historique et état global du logiciel anti-programme malveillant**|Affiche l'historique et l'état global du logiciel anti-programme malveillant.|  
|**Détails des programmes malveillants de l'ordinateur**|Affiche les détails relatifs à un ordinateur spécifié ainsi que la liste des programmes malveillants détectés sur cet ordinateur.|  
|**Ordinateurs infectés**|Affiche la liste des ordinateurs sur lesquels une menace spécifiée a été détectée.|  
|**Utilisateurs récurrents par menace**|Affiche la liste des utilisateurs qui ont le plus grand nombre de menaces détectées.|  
|**Liste des menaces utilisateur**|Affiche la liste des menaces trouvées pour un compte d'utilisateur spécifique.|  



## <a name="hardware---cd-rom"></a>Matériel - CD-ROM  
Les quatre rapports suivants sont répertoriés sous la catégorie **Matériel - CD-ROM**. 
|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Informations de CD-ROM pour un ordinateur spécifique**|Affiche des informations sur les lecteurs de CD-ROM d'un ordinateur spécifié.|  
|**Ordinateurs disposant d'un CD-ROM d'un fabricant spécifique**|Affiche la liste des ordinateurs qui contiennent un lecteur de CD-ROM conçu par un fabricant que vous spécifiez.|  
|**Compter les lecteurs de CD-ROM par fabricant**|Affiche le nombre de lecteurs de CD-ROM inventoriés par fabricant.|  
|**Historique - Historique CD-ROM pour un ordinateur spécifique**|Affiche l'historique de l'inventaire des lecteurs de CD-ROM sur un ordinateur spécifié.|  



## <a name="hardware---disk"></a>Matériel - Disque  
Les huit rapports suivants sont répertoriés sous la catégorie **Matériel - disque**. 

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs avec un disque dur d'une taille spécifique**|Affiche la liste des ordinateurs dont les disques durs sont de la taille spécifiée.|  
|**Ordinateurs avec un espace disque libre faible (inférieur au pourcentage libre spécifié)**|Affiche la liste des ordinateurs inclus dans un regroupement spécifié dont l'espace disque libre est inférieur à celui spécifié.|  
|**Ordinateurs avec un espace disque libre faible (inférieur au nombre de Mo libre spécifié)**|Affiche la liste des ordinateurs dont l'espace disque est faible. La quantité d'espace libre à rechercher est spécifiée en Mo.|  
|**Compter les configurations de disque physique**|Affiche le nombre de disques durs inventoriés par capacité du disque.|  
|**Informations de disques concernant un ordinateur spécifique - Disques logiques**|Affiche des informations de synthèse sur les disques logiques d'un ordinateur spécifié.|  
|**Informations de disques concernant un ordinateur spécifique - Partitions**|Affiche des informations de synthèse sur les partitions de disques d'un ordinateur spécifié.|  
|**Informations de disques concernant un ordinateur spécifique - Disques physiques**|Affiche des informations de synthèse sur les disques physiques d'un ordinateur spécifié.|  
|**Historique - Historique de l'espace disque logique pour un ordinateur spécifique**|Affiche l'historique de l'inventaire des lecteurs de disques logiques sur un ordinateur spécifié.|  



## <a name="hardware---general"></a>Matériel – Général  
Les cinq rapports suivants sont répertoriés sous la catégorie **Matériel - Général**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Informations concernant un ordinateur spécifique**|Affiche des informations de synthèse pour un ordinateur spécifié.|  
|**Ordinateurs dans un groupe de travail ou un domaine spécifique**|Affiche la liste des ordinateurs inclus dans un groupe de travail ou un domaine spécifié.|  
|**Classes d'inventaire affectées à un regroupement spécifique**|Affiche les classes d'inventaire affectées à un regroupement spécifié.|  
|**Classes d'inventaire activées sur un ordinateur spécifique**|Affiche les classes d'inventaire activées sur un ordinateur spécifié.|  
|**Informations d’appareil Windows AutoPilot**|Affiche les informations de l’appareil client nécessaires pour l’inscription Windows AutoPilot.|



## <a name="hardware---memory"></a>Matériel - Mémoire  
Les cinq rapports suivants sont répertoriés sous la catégorie **Matériel - Mémoire**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs sur lesquels la mémoire physique a changé**|Affiche la liste des ordinateurs dont la quantité de mémoire vive a changé depuis le dernier cycle d'inventaire.|  
|**Ordinateurs disposant d'une quantité de mémoire spécifique**|Affiche la liste des ordinateurs disposant d'une quantité spécifiée de mémoire vive (mémoire physique totale arrondie au mégaoctet le plus proche).|  
|**Ordinateurs avec peu de mémoire vive (inférieure ou égale à la quantité de Mo spécifiée)**|Affiche la liste des ordinateurs disposant de peu de mémoire. La quantité de mémoire à rechercher est spécifiée en Mo.|  
|**Compter les configurations de mémoire**|Affiche le nombre d'ordinateurs inventoriés par quantité de mémoire vive.|  
|**Informations de mémoire pour un ordinateur spécifique**|Affiche des informations de synthèse sur la mémoire d'un ordinateur spécifié.|  



## <a name="hardware---modem"></a>Matériel - Modem  
Les trois rapports suivants sont répertoriés sous la catégorie **Matériel - Modem**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs disposant d'un modem d'un fabricant spécifique**|Affiche la liste des ordinateurs qui disposent d'un modem conçu par un fabricant spécifique.|  
|**Compter les modems par fabricant**|Affiche le nombre de modems inventoriés pour chaque fabricant.|  
|**Informations de modem pour un ordinateur spécifique**|Affiche des informations de synthèse sur le modem d'un ordinateur spécifié.|  



## <a name="hardware---network-adapter"></a>Matériel - Carte réseau  
Les rapports suivants sont répertoriés sous la catégorie **Matériel - Carte réseau**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs équipés d'une carte réseau spécifique**|Affiche la liste des ordinateurs dotés d'une carte réseau spécifiée.|  
|**Compter les cartes réseau par type**|Affiche le nombre de cartes réseau inventoriées par type.|  
|**Informations de carte réseau pour un ordinateur spécifique**|Affiche des informations sur les cartes réseau installées sur un ordinateur spécifié.|  



## <a name="hardware---processor"></a>Matériel - Processeur  
Les cinq rapports suivants sont répertoriés sous la catégorie **Matériel - Processeur**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs ayant une fréquence de processeur spécifique**|Affiche la liste des ordinateurs dont un processeur est cadencé à la fréquence spécifiée.|  
|**Ordinateurs équipés de processeurs rapides (d'une fréquence supérieure ou égale à la fréquence spécifiée)**|Affiche la liste des ordinateurs dotés de processeurs dont la fréquence est plus rapide que la fréquence spécifiée.|  
|**Ordinateurs équipés de processeurs lents (d'une fréquence inférieure ou égale à la fréquence spécifiée)**|Affiche la liste des ordinateurs dotés de processeurs cadencés à une fréquence inférieure ou égale à la fréquence d'horloge spécifiée.|  
|**Compter les vitesses de processeur**|Affiche le nombre d'ordinateurs inventoriés par fréquence de processeur.|  
|**Informations de processeur pour un ordinateur spécifique**|Affiche des informations sur les processeurs installés sur un ordinateur spécifié.|  



## <a name="hardware---scsi"></a>Matériel - SCSI  
Les cinq rapports suivants sont répertoriés sous la catégorie **Matériel - SCSI**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs équipés d'un type de carte SCSI spécifique**|Affiche la liste des ordinateurs sur lesquels une carte SCSI spécifiée est installée.|  
|**Compter les types de contrôleurs SCSI**|Affiche le nombre de contrôleurs SCSI inventoriés par type de carte.|  
|**Informations de cartes SCSI pour un ordinateur spécifique**|Affiche des informations sur les cartes SCSI installées sur un ordinateur spécifié.|  



## <a name="hardware---security"></a>Matériel - Sécurité
Le rapport suivant est répertoriés sous la catégorie **Matériel - Sécurité**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Détails des états du microprogramme sur les appareils**|Affiche les détails des états de l’UEFI, de SecureBoot et du TPM|  



## <a name="hardware---sound-card"></a>Matériel - Carte audio  
Les trois rapports suivants sont répertoriés sous la catégorie **Matériel - SCSI**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs équipés d'une carte son spécifique**|Affiche la liste des ordinateurs dotés d'une carte son spécifiée.|  
|**Compter les cartes audio**|Affiche le nombre d'ordinateurs inventoriés par type de carte audio.|  
|**Informations de cartes son pour un ordinateur spécifique**|Affiche des informations de synthèse sur les cartes son d'un ordinateur spécifié.|  



## <a name="hardware---video-card"></a>Matériel – Carte vidéo  
Les trois rapports suivants sont répertoriés sous la catégorie **Matériel - Carte vidéo**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs équipés d'une carte vidéo spécifique**|Affiche la liste des ordinateurs dotés d'une carte vidéo spécifiée.|  
|**Compter les cartes vidéo par type**|Affiche une liste de toutes les cartes vidéo installées sur les ordinateurs. Il montre également le nombre de chaque type de carte vidéo.|  
|**Informations de cartes graphiques pour un ordinateur spécifique**|Affiche des informations de synthèse sur les cartes vidéo installées sur un ordinateur spécifié.|  



## <a name="migration"></a>Migration  

Les cinq rapports suivants sont répertoriés sous la catégorie **Migration**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Clients dans la liste des exclusions**|Affiche les clients exclus de la migration.|  
|**Dépendance sur un regroupement Configuration Manager**|Affiche les objets qui dépendent d'un regroupement de la hiérarchie source.|  
|**Propriétés de la tâche de migration**|Ce rapport affiche le contenu de la tâche de migration spécifiée.|  
|**Tâches de migration**|Ce rapport affiche la liste des tâches de migration.|  
|**Objets en échec de migration**|Affiche la liste des objets qui n'a pas pu migrer pendant la dernière tentative.|  



## <a name="network"></a>Réseau  

Les six rapports suivants sont répertoriés sous la catégorie **Réseau**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Compter les adresses IP par sous-réseau**|Affiche le nombre d'adresses IP inventoriées pour chaque sous-réseau IP.|  
|**IP - Tous les sous-réseaux par masque de sous-réseau**|Affiche la liste des sous-réseaux IP et des masques de sous-réseau.|  
|**IP - Ordinateurs dans un sous-réseau spécifique**|Affiche la liste des ordinateurs et des informations IP pour un sous-réseau IP spécifié.|  
|**IP - Informations pour un ordinateur spécifique**|Affiche des informations de synthèse sur le protocole Internet d'un ordinateur spécifié.|  
|**IP - Informations pour une adresse IP spécifique**|Affiche des informations de synthèse sur une adresse IP spécifiée.|  
|**MAC - Ordinateurs pour une adresse MAC spécifique**|Affiche le nom et l'adresse IP des ordinateurs dont l'adresse MAC est celle spécifiée.|  



## <a name="operating-system"></a>Système d'exploitation  

Les 10 rapports suivants sont répertoriés sous la catégorie **Système d'exploitation**.


|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Historique des versions du système d'exploitation de l'ordinateur**|Affiche l'historique de l'inventaire du système d'exploitation sur un ordinateur spécifié.|  
|**Ordinateurs équipés d'un système d'exploitation spécifique**|Affiche les ordinateurs équipés d'un système d'exploitation spécifié.|  
|**Ordinateurs équipés d'un système d'exploitation et d'un Service Pack spécifiques**|Affiche les ordinateurs équipés d'un système d'exploitation et d'un Service Pack spécifiés.|  
|**Nombre de versions du système d'exploitation**|Affiche le nombre d'ordinateurs inventoriés par système d'exploitation.|  
|**Compter les systèmes d'exploitation et les Service Packs**|Affiche le nombre d'ordinateurs inventoriés par combinaison de système d'exploitation et de Service Pack.|  
|**Services - Ordinateurs exécutant un service spécifique**|Affiche la liste des ordinateurs qui exécutent un service spécifié.|  
|**Services - Ordinateurs exécutant le service d'accès à distance**|Affiche la liste des ordinateurs qui exécutent le serveur d'accès à distance.|  
|**Services - Informations de services concernant un ordinateur spécifique**|Affiche des informations de synthèse sur les services d'un ordinateur spécifié.|  
|**Détails de la maintenance de Windows 10 pour un regroupement spécifique**|Affiche des informations générales sur la maintenance de Windows 10 pour un regroupement spécifique.|
|**Ordinateurs Windows Server**|Affiche la liste des ordinateurs qui exécutent des systèmes d'exploitation Windows Server.|  



## <a name="power-management"></a>Gestion de l'alimentation  

Les 18 rapports suivants sont répertoriés sous la catégorie **Gestion de l'alimentation**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Gestion de l'alimentation - Activité de l'ordinateur**|Affiche un graphique illustrant l’activité du moniteur, de l’ordinateur et de l’utilisateur pour un regroupement spécifique au cours d’une période donnée.|  
|**Gestion de l'alimentation - Activité par ordinateur**|Affiche un graphique illustrant l’activité du moniteur, de l’ordinateur et de l’utilisateur pour un ordinateur spécifié à une date spécifiée.|  
|**Gestion de l'alimentation - Détails de l'activité de l'ordinateur**|Affiche la liste des fonctions de veille et de sortie de veille pour les ordinateurs d'un regroupement spécifié à une heure et une date données.|  
|**Gestion de l'alimentation - Détails de l'ordinateur**|Affiche des informations détaillées sur les fonctions de gestion de l’alimentation, les paramètres d’alimentation et les modes de gestion de l’alimentation appliqués à un ordinateur spécifié.|  
|**Gestion de l'alimentation - Pas de rapport détaillé pour l'ordinateur**|Affiche la liste des ordinateurs ne rendant compte d'aucune activité d'alimentation pour une heure et une date données.|  
|**Gestion de l'alimentation – Ordinateurs exclus**|Affiche la liste des ordinateurs exclus du mode de gestion de l'alimentation.|  
|**Gestion de l'alimentation - Ordinateurs avec plusieurs modes de gestion de l'alimentation**|Affiche la liste des ordinateurs auxquels plusieurs paramètres d'alimentation en conflit sont appliqués.|  
|**Gestion de l'alimentation - Consommation énergétique**|Affiche la consommation énergétique mensuelle totale (en kWh) pour un regroupement donné sur une période de temps précise.|  
|**Gestion de l'alimentation - Consommation énergétique journalière**|Affiche la consommation énergétique totale (en kWh) au cours des 31 derniers jours pour un regroupement donné.|  
|**Gestion de l'alimentation - Coût énergétique**|Affiche le coût de la consommation énergétique mensuelle totale pour un regroupement donné sur une période de temps précise.|  
|**Gestion de l'alimentation - Coût énergétique journalier**|Affiche le coût énergétique total pour un regroupement donné au cours des 31 derniers jours.|  
|**Gestion de l'alimentation - Incidence sur l'environnement**|Affiche un graphique montrant les émissions de dioxyde de carbone (CO2) générées par un regroupement spécifié sur une période de temps précise.|  
|**Gestion de l'alimentation - Incidence journalière sur l'environnement**|Affiche un graphique montrant les émissions de CO2 générées par un regroupement spécifié au cours des 31 derniers jours.|  
|**Gestion de l'alimentation - Détails de l'ordinateur non mis en veille**|Affiche des informations détaillées sur les ordinateurs qui ne se sont pas mis en veille ou veille prolongée sur une période donnée.|  
|**Gestion de l'alimentation - Rapport sur la non-mise en veille**|Affiche une liste de causes courantes empêchant les ordinateurs de se mettre en veille ou veille prolongée. Il indique également le nombre d’ordinateurs affectés par chaque cause sur une période donnée.|  
|**Gestion de l'alimentation - Fonctions de gestion de l'alimentation**|Affiche les fonctions de gestion de l'alimentation des ordinateurs inclus dans le regroupement spécifié.|  
|**Gestion de l'alimentation - Paramètres du mode de gestion de l'alimentation**|Affiche la liste globale des paramètres d'alimentation utilisés par les ordinateurs d'un regroupement spécifié.|  
|**Gestion de l'alimentation - Détails des paramètres du mode de gestion de l'alimentation**|Permet d’afficher d’autres informations sur les ordinateurs qui ont été spécifiés dans le rapport **Gestion de l’alimentation – Paramètres du mode de gestion de l’alimentation**.|  



## <a name="replication-traffic"></a>Trafic de réplication  
Les 10 rapports suivants sont répertoriés sous la catégorie **Trafic de réplication**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Trafic global de réplication des données par lien (courbes)**|Affiche le trafic total global de réplication des données sur un lien spécifié pendant un nombre de jours spécifiés.|  
|**Trafic global de réplication des données par lien (secteurs)**|Affiche le trafic total global de réplication des données sur un lien spécifié pendant un nombre de jours spécifiés.|  
|**Trafic de réplication par hiérarchie en fonction du lien**|Affiche le trafic de réplication total pour chaque lien de la hiérarchie pendant un nombre de jours spécifié.|  
|**Trafic par lien des dix principaux groupes de réplication par hiérarchie (secteurs)**|Affiche le trafic de réplication pour les 10 principaux groupes de réplication sur la totalité de la hiérarchie identifiée par un lien.|  
|**Trafic de réplication des liens**|Affiche la totalité du trafic de réplication pour toutes les données pendant un nombre de jours spécifié.|  
|**Trafic du groupe de réplication par lien**|Affiche le trafic réseau du groupe de réplication via un lien spécifié de réplication de bases de données pendant un nombre de jours spécifié.|  
|**Trafic de réplication de données de site par lien (courbes)**|Affiche le trafic total de réplication de données de site sur un lien spécifié pendant un nombre de jours spécifié.|  
|**Trafic de réplication de données de site par lien (secteurs)**|Affiche le trafic total de réplication de données de site sur un lien spécifié pendant un nombre de jours spécifié.|  
|**Total du trafic de réplication par hiérarchie (courbes)**|Affiche la réplication de données globales et de site consolidées par hiérarchie pour chaque direction de chaque lien pendant un nombre de jours spécifié.|  
|**Total du trafic de réplication par hiérarchie (secteurs)**|Affiche la réplication de données globales et de site consolidées par hiérarchie pour chaque direction de chaque lien pendant un nombre de jours spécifié.|  



## <a name="site---client-information"></a>Site - Informations client  
Les 19 rapports suivants sont répertoriés sous la catégorie **Site - Informations client**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Rapport détaillé d'état d'attribution des clients**|Affiche des informations détaillées sur l'état d'attribution des clients.|  
|**Détails sur l'échec de l'attribution des clients**|Affiche des informations détaillées sur les échecs d'attribution de clients.|  
|**Détails de l'état d'attribution des clients**|Affiche des informations générales sur l'état d'attribution des clients.|  
|**Détails sur la réussite de l'attribution des clients**|Affiche des informations détaillées sur les clients dont l'attribution a réussi.|  
|**Rapport d'échec du déploiement des clients**|Affiche des informations détaillées sur les clients dont le déploiement a échoué.|  
|**Détails de l'état du déploiement des clients**|Affiche des informations de synthèse sur l'état des installations des clients.|  
|**Rapport de réussite du déploiement des clients**|Affiche des informations détaillées sur les clients dont le déploiement a réussi.|  
|**Clients non compatibles avec une communication HTTPS**|Affiche des informations détaillées sur chaque client exécutant l’outil HTTPS Communication Readiness et signalé comme étant dans l’impossibilité de communiquer via HTTPS.|  
|**Ordinateurs attribués mais non installés pour un site précis**|Affiche une liste d’ordinateurs attribués à un site précis, mais qui ne rendent pas compte à ce site.|  
|**Ordinateurs avec une version spécifique du client Configuration Manager**|Affiche une liste d'ordinateurs exécutant une version spécifique du logiciel client Configuration Manager.|  
|**Nombre de clients et protocole utilisé pour la communication**|Affiche le résumé des méthodes de communication utilisées par les clients (HTTP ou HTTPS).|  
|**Nombre de clients affectés et installés pour chaque site**|Affiche le nombre d'ordinateurs attribués et installés pour chaque site. Les clients possédant un emplacement réseau associé à plusieurs sites ne sont considérés comme installés que s'ils sont sous la supervision de ce site.|  
|**Nombre de clients compatibles avec une communication HTTPS**|Affiche des informations détaillées sur chaque client exécutant l’outil HTTPS Communication Readiness et signalé comme étant en mesure ou non de communiquer via HTTPS.|  
|**Nombre de clients pour chaque site**|Affiche le nombre de clients de Configuration Manager installés par code de site.|  
|**Nombre de clients de Configuration Manager par versions de client**|Affiche le nombre d’ordinateurs découverts par la version de client Configuration Manager.|  
|**Détail des problèmes signalés jusqu'au point d'état de secours pour un regroupement spécifié**|Affiche des informations détaillées pour les problèmes signalés par les clients dans un regroupement spécifié. Un point d’état de secours doit avoir été attribué à ces clients.|  
|**Détails des problèmes signalés jusqu'au point d'état de secours pour un site spécifié**|Affiche des informations détaillées sur les problèmes signalés par les clients dans un site spécifié. Un point d’état de secours doit avoir été attribué à ces clients.|  
|**Récapitulatif des problèmes signalés jusqu'au point d'état de secours**|Affiche des informations sur tous les problèmes signalés par les clients. Un point d’état de secours doit avoir été attribué à ces clients.|  
|**Récapitulatif des problèmes signalés jusqu'au point d'état de secours pour un regroupement spécifique**|Affiche des informations de synthèse pour les problèmes signalés par les clients dans un regroupement spécifié. Un point d’état de secours doit avoir été attribué à ces clients.|  



## <a name="site---discovery-and-inventory-information"></a>Site - Informations de découverte et d'inventaire  
Les 10 rapports suivants sont répertoriés sous la catégorie **Site - Informations de découverte et d'inventaire**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Clients qui n'ont pas émis de rapports récemment (pendant le nombre de jours spécifié)**|Affiche la liste des clients qui n'ont pas signalé de données de découverte, d'inventaire matériel ou d'inventaire logiciel pendant un nombre de jours spécifié.|  
|**Ordinateurs découverts par un site spécifique**|Affiche une liste de tous les ordinateurs découverts par le site spécifié. Il montre également la date de la dernière découverte.|  
|**Ordinateurs récemment découverts par une méthode de découverte**|Affiche une liste des ordinateurs découverts par le site pendant le nombre de jours spécifié. Il répertorie également les agents qui les ont découverts. Un même ordinateur peut apparaître plusieurs fois dans la liste s’il a été découvert par plusieurs agents.|  
|**Ordinateurs non découverts récemment (dans un nombre de jours spécifié)**|Affiche une liste des ordinateurs qui n’ont pas été découverts récemment par le site. Il indique également le nombre de jours depuis leur découverte.|  
|**Ordinateurs non inventoriés récemment (dans un nombre de jours spécifié)**|Affiche une liste des ordinateurs qui n’ont pas été inventoriés récemment par le site. Il indique également les dates des derniers inventaires des ordinateurs par le client.|  
|**Ordinateurs susceptibles de partager le même identifiant Configuration Manager unique**|Affiche la liste des ordinateurs qui ont modifié leur nom. Un changement de nom est un symptôme possible d’un ordinateur qui partage un identificateur unique Configuration Manager avec un autre ordinateur.|  
|**Ordinateurs ayant des adresses MAC en double**|Affiche les ordinateurs qui partagent une adresse MAC.|  
|**Compter les ordinateurs dans les domaines de ressources ou groupes de travail**|Affiche le nombre d'ordinateurs dans chaque domaine de ressources ou groupe de travail.|  
|**Informations de découverte pour un ordinateur spécifique**|Affiche la liste des agents et des sites qui ont découvert un ordinateur spécifié.|  
|**Dates d'inventaire pour un ordinateur spécifique**|Affiche la date et l'heure de la dernière exécution de l'inventaire sur un ordinateur spécifié.|  



## <a name="site---general"></a>Site - Général  
Les trois rapports suivants sont répertoriés sous la catégorie **Site - Général**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs dans un site spécifique**|Affiche la liste des ordinateurs clients dans un site spécifié.|  
|**État du site pour la hiérarchie**|Affiche la liste des sites de la hiérarchie avec leur version et leurs informations d'état.|  
|**État de la mise à jour Configuration Manager au sein de la hiérarchie**|Affiche des informations sur les mises à jour de sites Configuration Manager pour la hiérarchie.|  



## <a name="site---server-information"></a>Site - Informations sur le serveur  
Le rapport suivant est répertorié sous la catégorie **Site - Informations sur le serveur**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Rôles de système de site et serveurs de système de site pour un site spécifique**|Affiche la liste des serveurs et rôles de système de site pour un site spécifié.|  



## <a name="software---companies-and-products"></a>Logiciel - Sociétés et produits  
Les 15 rapports suivants sont répertoriés sous la catégorie **Logiciel - Sociétés et produits**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les produits inventoriés pour un éditeur de logiciels spécifique**|Affiche la liste des produits logiciels inventoriés et de leurs versions pour un éditeur de logiciels spécifié.|  
|**Tous les éditeurs de logiciels**|Affiche la liste de toutes les entreprises qui éditent les logiciels inventoriés.|  
|**Toutes les applications Windows**|Affiche une synthèse des applications Windows installées. La recherche est effectuée selon les critères suivants : nom de l’application, architecture ou éditeur.|  
|**Ordinateurs sur lesquels existe un produit spécifique**|Affiche la liste des ordinateurs sur lesquels un produit spécifié est inventorié, ainsi que les versions de ce produit.|  
|**Ordinateurs sur lesquels existe un produit et une version spécifiques**|Affiche la liste des ordinateurs sur lesquels une version spécifiée d'un produit est inventoriée.|  
|**Ordinateurs équipés d'un logiciel spécifique inscrit dans Ajout/Suppression de programmes**|Affiche le résumé de tous les ordinateurs équipés d'un logiciel spécifié inscrit dans Ajout/Suppression de programmes ou Programmes et fonctionnalités.|  
|**Nombre de tous les produits et versions inventoriés**|Affiche la liste des produits logiciels et versions inventoriés, ainsi que le nombre d'ordinateurs sur lesquels chacun est installé.|  
|**Compter les produits et versions inventoriés pour un produit spécifique**|Affiche la liste des versions inventoriées d'un produit spécifié, ainsi que le nombre d'ordinateurs sur lesquels chacune est installée.|  
|**Décompte de toutes les instances de logiciels inscrits avec Ajout/Suppression de programmes**|Affiche le résumé de toutes les instances de logiciels installées et inscrites avec Ajout/Suppression de programmes ou Programmes et fonctionnalités sur des ordinateurs au sein du regroupement spécifié.|  
|**Décompte des instances d'un logiciel spécifique inscrit avec Ajout/Suppression de programmes**|Affiche le nombre d'instances des packages logiciels spécifiés installés et inscrits dans Ajout/Suppression de programmes ou Programmes et fonctionnalités.|  
|**Nombre de navigateurs par défaut**|Affiche le nombre de clients ayant spécifié un certain navigateur web par défaut sous Windows. </br>Utilisez la référence suivante pour les valeurs BrowserProgID courantes :</br> - AppXq0fevzme2pys62n3e0fbqa7peapykr8v : Microsoft Edge</br> - IE.HTTP : Microsoft Internet Explorer</br> - ChromeHTML : Google Chrome</br> - OperaStable : Opera Software</br> - FirefoxURL-308046B0AF4A39CB : Mozilla Firefox</br> - Inconnu : le système d’exploitation client ne prend pas en charge la requête, la requête n’a pas été exécutée ou un utilisateur ne s’est pas connecté|
|**Installations des applications Windows spécifiées**|Ce rapport répertorie tous les ordinateurs dotés d’une application Windows spécifiée.|  
|**Produits sur un ordinateur spécifique**|Affiche le résumé des produits logiciels inventoriés et de leurs fabricants sur un ordinateur spécifié.|  
|**Logiciels inscrits dans Ajout/Suppression de programmes sur un ordinateur spécifique**|Affiche le résumé des logiciels installés sur un ordinateur spécifié et inscrits dans Ajout/Suppression de programmes ou Programmes et fonctionnalités.|  
|**Applications Windows installées pour l’utilisateur spécifié**|Affiche toutes les applications Windows installées pour l’utilisateur spécifié|  



## <a name="software---files"></a>Fichiers logiciels  
Les rapports suivants sont répertoriés sous la catégorie **Fichiers logiciels**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les fichiers inventoriés pour un produit spécifique**|Affiche le résumé des fichiers inventoriés qui sont associés à un produit logiciel spécifié.|  
|**Tous les fichiers inventoriés sur un ordinateur spécifique**|Affiche le résumé de tous les fichiers inventoriés sur un ordinateur spécifié.|  
|**Comparer l'inventaire logiciel de deux ordinateurs**|Affiche les différences entre les inventaires logiciels signalés pour deux ordinateurs spécifiés.|  
|**Ordinateurs sur lesquels existe un fichier spécifique**|Affiche la liste des ordinateurs qui ont collecté un inventaire logiciel pour un nom de fichier spécifié. Si un ordinateur comporte plusieurs copies du fichier, il peut apparaître plusieurs fois dans la liste.|  
|**Compter les ordinateurs avec un nom de fichier spécifique**|Affiche le nombre d'ordinateurs qui ont collecté un inventaire logiciel pour un fichier spécifié.|  



## <a name="software-distribution---application-monitoring"></a>Distribution de logiciels - Surveillance des applications  
Les 10 rapports suivants sont répertoriés sous la catégorie **Distribution de logiciels - Surveillance des applications**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les déploiements d'applications (avancé)**|Affiche des informations de synthèse approfondies pour tous les déploiements d'applications.|  
|**Tous les déploiements d'applications (standard)**|Affiche des informations de synthèse pour tous les déploiements d'applications.|  
|**Compatibilité de l'application**|Affiche des informations de compatibilité pour l'application spécifiée au sein du regroupement spécifié.|  
|**Déploiements de l'application par bien**|Affiche les applications déployées sur un appareil ou utilisateur spécifié.|  
|**Erreurs d'infrastructure de l'application**|Affiche les erreurs d'infrastructure de l'application. Celles-ci peuvent inclure des erreurs d’infrastructure internes ou des erreurs résultant de règles de configuration requise non valides.|  
|**État détaillé de l'utilisation de l'application**|Affiche des détails sur l'utilisation des applications installées.|  
|**État récapitulatif de l'utilisation de l'application**|Affiche le résumé de l'utilisation des applications installées.|  
|**Applications iOS dont le déploiement a échoué (application déjà installée)**|Affiche les informations de conformité pour l’application iOS sélectionnée. Vous avez déployé cette application en tant que « Package d’application pour iOS depuis App Store » que vous avez aussi associée à une stratégie de gestion des applications mobiles. Ce rapport est utilisé pour afficher les utilisateurs et les appareils pour lesquels l’application n’a pas pu être installée, car elle avait déjà été installée manuellement par l’utilisateur.|  
|**Déploiements de séquences de tâches contenant l'application**|Affiche les déploiements de séquences de tâches qui installent une application spécifiée.|  
|**Demandes d'utilisateur pour une application Android**|Affiche les utilisateurs qui ont demandé à installer une application Android.|  



## <a name="software-distribution---collections"></a>Distribution de logiciels - Regroupements  
Les trois rapports suivants sont répertoriés sous la catégorie **Distribution de logiciels - Regroupements**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les regroupements**|Affiche tous les regroupements inclus dans la hiérarchie.|  
|**Toutes les ressources dans un regroupement spécifique**|Affiche toutes les ressources dans un regroupement spécifié.|  
|**Fenêtres de maintenance disponibles pour un client spécifié**|Affiche toutes les fenêtres de maintenance applicables au client spécifié.|  



## <a name="software-distribution---content"></a>Distribution de logiciels - Contenu  
Les 16 rapports suivants sont répertoriés sous la catégorie **Distribution de logiciels - Contenu**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Toutes les distributions de contenus actifs**|Affiche tous les points de distribution sur lesquels du contenu est en cours d'installation ou de suppression.|  
|**Tout le contenu**|Affiche toutes les applications et packages d'un site.|  
|**Tous les contenus dans un point de distribution spécifique**|Affiche tout le contenu actuellement installé sur un point de distribution spécifié.|  
|**Tous les points de distribution**|Affiche des informations sur les points de distribution de chaque site.|  
|**Tous les messages d'état pour un package spécifique sur un point de distribution spécifique**|Affiche tous les messages d'état pour un package spécifié sur un point de distribution spécifié.|  
|**État de distribution du contenu de l'application**|Affiche des informations sur l'état de distribution du contenu de l'application.|  
|**Applications ciblées pour le groupe de points de distribution**|Affiche des informations sur le contenu de l'application qui a été déployé sur un groupe de points de distribution spécifié.|  
|**Applications qui ne sont pas synchronisées dans un groupe de points de distribution spécifié**|Affiche les applications pour lesquelles des fichiers de contenu associés n'ont pas été mis à jour avec la version la plus récente sur un groupe de points de distribution spécifié.|  
|**Groupe de points de distribution**|Affiche des informations sur un groupe de points de distribution spécifié.|  
|**Résumé de l'utilisation des points de distribution**|Affiche le résumé de l'utilisation de chaque point de distribution.|  
|**État de distribution d'un package donné**|Affiche l'état de distribution du contenu du package spécifié sur chaque point de distribution.|  
|**Packages ciblés pour le groupe de points de distribution**|Affiche des informations sur les packages qui ciblent un groupe de points de distribution spécifié.|  
|**Packages non synchronisés sur un groupe de points de distribution spécifié**|Affiche les packages pour lesquels des fichiers de contenu associés n'ont pas été mis à jour avec la version la plus récente sur un groupe de points de distribution spécifié.|  
|**Rejet du contenu par une source de cache d’homologue**|Affiche le nombre de rejets par une source de cache d’homologue par groupe de limites.|
|**Rejet du contenu par une source de cache d’homologue par condition**|Affiche les sources de cache d’homologue ayant rejeté la diffusion de contenu en fonction d’une condition.|
|**Détails du rejet du contenu par une source de cache d’homologue**|Affiche le nom du contenu rejeté par une source d’homologue.|



## <a name="software-distribution---package-and-program-deployment"></a>Distribution de logiciels - Déploiement du package et du programme 
Les cinq rapports suivants sont répertoriés sous la catégorie **Distribution de logiciels - Déploiement du package et du programme**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les déploiements d'un package et d'un programme donnés**|Affiche des informations sur tous les déploiements d'un package et d'un programme spécifiés.|  
|**Tous les déploiements de packages et de programmes**|Affiche tous les déploiements de packages et de programmes sur ce site.|  
|**Tous les déploiements de packages et de programmes dans un regroupement donné**|Affiche tous les déploiements de packages et de programmes dans un regroupement spécifié.|  
|**Tous les déploiements de packages et de programmes sur un ordinateur donné**|Affiche tous les déploiements de packages et de programmes qui s'appliquent à un ordinateur spécifié.|  
|**Tous les déploiements de programmes et de packages vers un utilisateur spécifique**|Affiche tous les déploiements de packages et de programmes vers un utilisateur spécifié.|  



## <a name="software-distribution---package-and-program-deployment-status"></a>Distribution de logiciels - État du déploiement du package et du programme  
Les cinq rapports suivants sont répertoriés sous la catégorie **Distribution de logiciels - État du déploiement du package et du programme**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les déploiements de packages et de programmes de ressources système avec leur état**|Affiche tous les déploiements de packages et de programmes pour le site avec l'état récapitulatif de chaque déploiement.|  
|**Toutes les ressources système pour un déploiement de packages et de programmes spécifié dans un état spécifié**|Affiche la liste des ressources qui sont dans un état spécifié pour un déploiement de packages et de programmes spécifié.|  
|**Graphique - État d'avancement du déploiement de packages et de programmes chaque heure**|Affiche le pourcentage d’ordinateurs ayant installé avec succès le package. La liste classe toutes les heures depuis la création du déploiement de packages et de programmes par un administrateur. Ce pourcentage sert à suivre le temps moyen nécessaire au déploiement de packages et de programmes.|  
|**État du déploiement de packages et de programmes pour un client et un déploiement donnés**|Affiche les messages d'état signalés pour un ordinateur et un déploiement de packages et de programmes spécifiés.|  
|**État du déploiement d'un package et d'un programme spécifiques**|Affiche la synthèse d'état d'un déploiement de packages et de programmes spécifié.|  



## <a name="software-metering"></a>Contrôle de logiciel  
Les 13 rapports suivants sont répertoriés sous la catégorie **Contrôle de logiciel**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Toutes les règles de contrôle de logiciel appliquées à ce site**|Affiche la liste de toutes les règles de contrôle de logiciel au niveau du site.|  
|**Ordinateurs disposant d'un programme contrôlé mais qui ne l'ont pas encore exécuté depuis une date donnée**|Affiche tous les ordinateurs avec l’application contrôlée spécifiée, mais aucun utilisateur n’a exécuté ce programme depuis la date spécifiée.|  
|**Ordinateurs ayant exécuté un programme contrôlé spécifique**|Affiche la liste des ordinateurs qui ont exécuté des programmes correspondant à la règle de contrôle de logiciel spécifiée pendant le mois et l'année spécifiés.|  
|**Utilisation simultanée de tous les programmes contrôlés**|Affiche le nombre maximal d'utilisateurs qui ont exécuté simultanément chaque logiciel contrôlé pendant le mois et l'année spécifiés.|  
|**Analyse de la tendance d'utilisation simultanée d'un programme contrôlé spécifique**|Affiche le nombre maximal d'utilisateurs qui ont exécuté simultanément le logiciel contrôlé spécifié au cours de chaque mois de l'année précédente.|  
|**Base d'installation pour tous les logiciels contrôlés**|Affiche le nombre d'ordinateurs qui ont des logiciels contrôlés installés, comme indiqué par l'inventaire logiciel. Ce rapport nécessite que l’ordinateur collecte l’inventaire logiciel.|  
|**Progression du résumé du contrôle de logiciel**|Affiche l'heure à laquelle les données de contrôle synthétisées les plus récentes ont été traitées sur le serveur de site. Les rapports de contrôle de logiciel reflètent uniquement les données de contrôle traitées avant ces dates.|  
|**Résumé de l'utilisation dans la journée pour un programme de logiciel contrôlé spécifique**|Affiche le nombre moyen d'utilisations d'un programme particulier au cours des 90 derniers jours, par heure et par jour.|  
|**Utilisation simultanée de tous les programmes de logiciels contrôlés**|Affiche le nombre d’utilisateurs qui ont exécuté des programmes correspondant à chaque règle de contrôle de logiciel pendant le mois et l’année spécifiés. Ces règles concernent les logiciels installés localement ou l’utilisation des services Terminal Server.|  
|**Utilisation totale de tous les logiciels contrôlés sur les serveurs Windows Terminal Server**|Affiche le nombre d'utilisateurs qui ont exécuté des programmes correspondant à chaque règle de contrôle de logiciel à l'aide des services Terminal Server pendant le mois et l'année spécifiés.|  
|**Analyse de la tendance d'utilisation totale pour un programme contrôlé spécifique**|Affiche le nombre d’utilisateurs qui ont exécuté des programmes correspondant à la règle de contrôle de logiciel spécifiée pendant chaque mois de l’année précédente. Ces règles concernent les logiciels installés localement ou l’utilisation des services Terminal Server.|  
|**Analyse de la tendance d'utilisation totale pour un logiciel contrôlé spécifique sur les serveurs Windows Terminal Server**|Affiche le nombre d’utilisateurs qui ont exécuté des programmes correspondant à la règle de contrôle de logiciel spécifiée pendant chaque mois de l’année précédente. Ces règles concernent l’utilisation des services Terminal Server.|  
|**Utilisateurs ayant exécuté un programme contrôlé spécifique**|Affiche une liste d’utilisateurs qui ont exécuté des programmes correspondant à la règle de contrôle de logiciel spécifiée pendant le mois et l’année spécifiés.|  



## <a name="software-updates---a-compliance"></a>Mises à jour logicielles - Compatibilité A  
Les huit rapports suivants sont répertoriés sous la catégorie **Mises à jour logicielles - Compatibilité A**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Compatibilité 1 - Compatibilité globale**|Affiche les données de compatibilité globale d'un groupe de mises à jour logicielles.|  
|**Conformité 2 - Mise à jour logicielle spécifique**|Affiche les données de compatibilité d'une mise à jour logicielle spécifiée.|  
|**Compatibilité 3 - Groupe de mises à jour (par mise à jour)**|Affiche les données de compatibilité des mises à jour logicielles définies dans un groupe de mises à jour logicielles.|  
|**Compatibilité 4 - Mises à jour par fabricant-mois-année**|Affiche les données de compatibilité des mises à jour logicielles publiées par un fournisseur pendant un mois et une année spécifiés.|  
|**Compatibilité 5 - Ordinateur spécifique**|Ce rapport renvoie les données de compatibilité des mises à jour logicielles pour un ordinateur spécifié. Pour limiter la quantité d'informations renvoyées, vous pouvez spécifier le fournisseur et la classification des mises à jour logicielles.|  
|**Compatibilité 6 - États de mises à jour logicielles spécifiques (secondaire)**|Affiche le nombre et le pourcentage d'ordinateurs dans chaque état de compatibilité pour la mise à jour logicielle spécifiée.|  
|**Compatibilité 7 - Ordinateurs dans un état de compatibilité spécifique pour un groupe de mises à jour (secondaire)**|Affiche tous les ordinateurs d'un regroupement qui sont dans un état de compatibilité globale spécifié par rapport à un groupe de mises à jour logicielles.|  
|**Compatibilité 8 - Ordinateurs dans un état de compatibilité spécifique pour une mise à jour (secondaire)**|Affiche tous les ordinateurs d'un regroupement qui sont dans un état de compatibilité spécifié pour une mise à jour logicielle.|  
|**Conformité 9 – Conformité et intégrité globales**|Affiche les données de conformité et d’intégrité globales d’un groupe de mises à jour logicielles. (depuis la version 1806)| 


## <a name="software-updates---b-deployment-management"></a>Mises à jour logicielles - Gestion du déploiement B  
Les huit rapports suivants sont répertoriés sous la catégorie **Mises à jour logicielles - Gestion du déploiement B**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Gestion 1 - Déploiements d'un groupe de mises à jour**|Affiche tous les déploiements qui contiennent toutes les mises à jour logicielles définies dans un groupe de mises à jour logicielles spécifié.|  
|**Gestion 2 - Mises à jour requises mais non déployées**|Affiche toutes les mises à jour logicielles propres à un fournisseur qui ont été détectées comme obligatoires par les clients, mais qui n’ont pas été déployées sur un regroupement spécifié par un administrateur.|  
|**Gestion 3 - Mises à jour dans un déploiement**|Affiche les mises à jour logicielles contenues dans un déploiement spécifié.|  
|**Gestion 4 - Déploiements ciblant un regroupement**|Affiche tous les déploiements de mises à jour logicielles qui ciblent un regroupement spécifié.|  
|**Gestion 5 - Déploiements ciblant un ordinateur**|Affiche tous les déploiements de mises à jour logicielles sur un ordinateur spécifié.|  
|**Gestion 6 - Déploiements contenant une mise à jour spécifique**|Affiche tous les déploiements qui contiennent une mise à jour logicielle spécifiée et le regroupement cible associé au déploiement.|  
|**Gestion 7 - Mises à jour dans un déploiement dont le contenu manque**|Affiche les mises à jour logicielles incluses dans un déploiement spécifié qui n’ont pas récupéré tout le contenu associé. Cet état empêche les clients d’installer ces mises à jour et d’atteindre 100 % de compatibilité pour le déploiement.|  
|**Gestion 8 - Contenu d'ordinateurs manquant (secondaire)**|Affiche tous les ordinateurs qui nécessitent la mise à jour logicielle spécifiée, mais le contenu associé n’est pas encore distribué à un point de distribution.|  



## <a name="software-updates---c-deployment-states"></a>Mises à jour logicielles - États du déploiement C  
Les six rapports suivants sont répertoriés sous la catégorie **Mises à jour logicielles - États du déploiement C**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**États 1 - États d'application pour un déploiement**|Affiche les états d'application du déploiement de mises à jour logicielles spécifié, qui correspond généralement à la deuxième étape de l'évaluation d'un déploiement.|  
|**États 2 - États d'évaluation pour un déploiement**|Affiche l'état d'évaluation du déploiement de mises à jour logicielles spécifié, qui correspond généralement à la première étape de l'évaluation d'un déploiement.|  
|**États 3 - États d'un déploiement et d'un ordinateur**|Affiche les états de toutes les mises à jour logicielles incluses dans le déploiement spécifié pour un ordinateur spécifié.|  
|**États 4 - Ordinateurs présentant l'état spécifique d'un déploiement (secondaire)**|Affiche tous les ordinateurs présentant un état spécifié pour un déploiement de mises à jour logicielles.|  
|**États 5 - États pour une mise à jour dans un déploiement (secondaire)**|Affiche le résumé des états pour une mise à jour logicielle spécifiée ciblée par un déploiement spécifié.|  
|**États 6 - Ordinateurs présentant un état d'application spécifique pour une mise à jour (secondaire)**|Affiche tous les ordinateurs dans un état d'application spécifié pour une mise à jour logicielle spécifiée.|  



## <a name="software-updates---d-scan"></a>Mises à jour logicielles - Analyse D  
Les quatre rapports suivants sont répertoriés sous la catégorie **Mises à jour logicielles - Analyse D**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Analyse 1 - Derniers états d'analyse par regroupement**|Spécifiez un regroupement pour afficher le nombre d’ordinateurs dans chaque état d’analyse de conformité. Les clients retournent l’état pendant la dernière analyse de conformité.|  
|**Analyse 2 - Derniers états d'analyse par site**|Spécifiez un site pour afficher le nombre d’ordinateurs dans chaque état d’analyse de conformité. Les clients retournent l’état pendant la dernière analyse de conformité.|  
|**Analyse 3 - Clients d'un regroupement signalant un état spécifique (secondaire)**|Affiche tous les ordinateurs d'un regroupement spécifié et dans un état d'analyse de compatibilité spécifié pendant leur dernière analyse de compatibilité.|  
|**Analyse 4 - Clients d'un site signalant un état spécifique (secondaire)**|Spécifiez un site pour afficher tous les ordinateurs avec un état d’analyse de conformité spécifié. Les clients retournent l’état pendant leur dernière analyse de conformité.|  



## <a name="software-updates---e-troubleshooting"></a>Mises à jour logicielles - Dépannage E  

Les quatre rapports suivants sont répertoriés sous la catégorie **Mises à jour logicielles - Dépannage E**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Dépannage 1 - Erreurs d'analyse**|Affiche les erreurs d'analyse au niveau du site et le nombre d'ordinateurs qui rencontrent chaque erreur.|  
|**Dépannage 2 – Erreurs de déploiement**|Affiche les erreurs de déploiement au niveau du site et le nombre d'ordinateurs qui rencontrent chaque erreur.|  
|**Dépannage 3 - Échecs d'ordinateurs avec une erreur d'analyse spécifique (secondaire)**|Affiche la liste des ordinateurs qui n'ont pas réussi une analyse en raison d'une erreur spécifiée.|  
|**Dépannage 4 - Échecs d'ordinateurs avec une erreur de déploiement spécifique (secondaire)**|Affiche la liste des ordinateurs sur lesquels le déploiement de la mise à jour échoue en raison d'une erreur spécifiée.|  



## <a name="state-migration"></a>Migration de l'état  
Les trois rapports suivants sont répertoriés sous la catégorie **Migration de l'état**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Informations sur la migration de l'état d'un ordinateur source spécifique**|Affiche des informations sur la migration de l'état d'un ordinateur spécifié.|  
|**Informations de migration d'état d'un point de migration d'état spécifique**|Affiche des informations sur la migration de l'état d'un point de migration d'état spécifié.|  
|**Points de migration d'état d'un site spécifique**|Affiche les points de migration d'état d'un site spécifié.|  



## <a name="status-messages"></a>Messages d'état  
Les 12 rapports suivants sont répertoriés sous la catégorie **Messages d'état**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les messages pour un ID de message spécifique**|Affiche la liste des messages d'état qui ont un ID de message spécifié.|  
|**Clients signalant des erreurs pendant les 12 dernières heures pour un site spécifique**|Affiche la liste des ordinateurs et des composants qui signalent des erreurs pendant les 12 dernières heures et le nombre d'erreurs signalées.|  
|**Messages de composants pour les 12 dernières heures**|Affiche la liste des messages de composants pendant les 12 dernières heures pour un code de site, un ordinateur et un composant spécifiés.|  
|**Messages de composants pendant la dernière heure**|Affiche une liste des messages d’état créés pendant la dernière heure par un composant donné sur un ordinateur indiqué d’un site spécifié.|  
|**Compter les messages de composants pendant la dernière heure pour un site spécifique**|Affiche le nombre de messages d'état par composant et gravité signalés dans la dernière heure dans un site spécifié.|  
|**Compter les erreurs survenues dans les 12 dernières heures**|Affiche le nombre de messages d'erreur de composants serveur dans les 12 dernières heures.|  
|**Erreurs irrécupérables (par composant)**|Affiche la liste des ordinateurs qui signalent des erreurs irrécupérables par composant.|  
|**Erreurs irrécupérables (par nom d'ordinateur)**|Affiche la liste des ordinateurs qui signalent des erreurs irrécupérables par nom d'ordinateur.|  
|**Les 1 000 derniers messages pour un ordinateur spécifique (erreurs et avertissements)**|Affiche le résumé des 1000 derniers messages d'état d'erreur et d'avertissement pour un ordinateur spécifié.|  
|**1 000 derniers messages pour un ordinateur spécifique (avertissements d'erreur et informations)**|Affiche le résumé des 1000 derniers messages d'état d'erreur, d'avertissement et d'information pour un ordinateur spécifié.|  
|**Les 1 000 derniers messages pour un ordinateur spécifique (erreurs)**|Affiche le résumé des 1000 derniers messages d'état d'erreur du composant serveur pour un ordinateur spécifié.|  
|**Les 1 000 derniers messages pour un composant serveur spécifique**|Affiche le résumé des 1000 messages d'état les plus récents pour un composant serveur spécifié.|  



## <a name="status-messages---audit"></a>Messages d'état - Audit  

Les trois rapports suivants sont répertoriés sous la catégorie **Messages d'état - Audit**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les messages d'audit pour un utilisateur spécifique**|Affiche le résumé de tous les messages d'état d'audit pour un utilisateur spécifié. Les messages d’audit décrivent les opérations effectuées dans la console Configuration Manager pour ajouter, modifier ou supprimer des objets dans Configuration Manager.|  
|**Contrôle à distance - Tous les ordinateurs contrôlés à distance par un utilisateur spécifique**|Affiche le résumé des messages d'état indiquant un contrôle à distance des ordinateurs clients par un utilisateur spécifié.|  
|**Contrôle à distance - Toutes les informations de contrôle à distance**|Affiche le résumé des messages d'état associés au contrôle à distance des ordinateurs clients.|  



## <a name="task-sequence---deployment-status"></a>État du déploiement de séquence de tâches  
Les 11 rapports suivants sont répertoriés sous la catégorie **Séquence de tâches - État du déploiement**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Toutes les ressources système pour un déploiement de séquences de tâches dans un état spécifié**|Affiche la liste des ordinateurs de destination pour le déploiement de séquences de tâches spécifié dans un état de déploiement spécifié.|  
|**Toutes les ressources système pour un déploiement de séquences de tâches qui est dans un état spécifique et disponible pour les ordinateurs inconnus**|Affiche la liste des ordinateurs de destination pour le déploiement de séquences de tâches spécifié présentant l'état de déploiement spécifié.|  
|**Nombre de ressources système auxquelles des déploiements de séquences de tâches sont affectés mais pas encore exécutés**|Affiche le nombre d'ordinateurs qui ont accepté des séquences de tâches, mais qui n'en ont pas encore exécuté une.|  
|**Historique d'un déploiement de séquences de tâches sur un ordinateur**|Affiche l'état de chaque étape du déploiement de séquences de tâches spécifié sur l'ordinateur de destination spécifié. Si aucun rapport n'est créé, la séquence de tâches n'a pas commencé sur l'ordinateur.|  
|**Liste des ordinateurs ayant dépassé la durée spécifique d'exécution d'un déploiement de séquences de tâches**|Affiche la liste des ordinateurs de destination qui ont dépassé la durée spécifiée d'exécution d'une séquence de tâches.|  
|**Durée d'exécution d'un déploiement de séquences de tâches spécifique sur un ordinateur de destination spécifique**|Affiche le temps total nécessaire pour réussir une séquence de tâches spécifiée sur un ordinateur spécifié.|  
|**Durée d'exécution de chaque étape d'un déploiement de séquences de tâches sur un ordinateur de destination spécifique**|Affiche le temps nécessaire pour exécuter chaque chaque étape du déploiement de séquences de tâches spécifié sur l'ordinateur de destination spécifié.|  
|**État d'un déploiement de séquences de tâches spécifique pour un ordinateur spécifique**|Affiche la synthèse d'état d'un déploiement de séquences de tâches spécifié sur un ordinateur spécifié.|  
|**État d'un déploiement de séquences de tâches sur un ordinateur de destination inconnu**|Affiche l'état du déploiement de séquences de tâches spécifié sur l'ordinateur de destination inconnu spécifié.|  
|**Résumé des états d'un déploiement de séquences de tâches spécifique**|Affiche la synthèse d'état de toutes les ressources qui ont été ciblées par un déploiement.|  
|**Récapitulatif des états d'un déploiement de séquences de tâches disponible pour des ordinateurs inconnus**|Affiche la synthèse d’état de toutes les ressources ciblées par le déploiement spécifié et disponible pour un regroupement qui contient des ordinateurs inconnus.|  



## <a name="task-sequence---deployments"></a>Séquence de tâches - Déploiements  
Les 11 rapports suivants sont répertoriés sous la catégorie **Séquence de tâches - Déploiements**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Toutes les ressources système actuellement dans un groupe ou une phase spécifique du déploiement d'une séquence de tâches spécifique**|Affiche la liste des ordinateurs en cours d'exécution dans un groupe spécifié ou dans une étape de déploiement de séquences de tâches spécifiée.|  
|**Toutes les ressources système pour lesquelles un déploiement d'une séquence de tâches a échoué dans un groupe ou une phase spécifique**|Affiche la liste des ordinateurs en échec au sein d'un groupe spécifié ou pendant une phase spécifiée du déploiement de séquences de tâches spécifié.|  
|**Tous les déploiements de séquences de tâches**|Affiche les détails de tous les déploiements de séquences de tâches lancés à partir du site actuel.|  
|**Tous les déploiements de séquences de tâches disponibles pour les ordinateurs inconnus**|Affiche les détails de tous les déploiements de séquences de tâches lancés à partir du site et déployés sur des regroupements qui contiennent des ordinateurs inconnus.|  
|**Nombre d'échecs dans chaque phase ou groupe d'une séquence de tâches spécifique**|Affiche le nombre d'échecs dans chaque phase ou groupe de la séquence de tâches spécifiée.|  
|**Nombre d'échecs dans chaque phase ou groupe d'un déploiement de séquences de tâches spécifique**|Affiche le nombre d'échecs dans chaque phase ou groupe du déploiement de séquences de tâches spécifié.|  
|**État du déploiement de tous les déploiements de séquences de tâches**|Affiche la progression globale de tous les déploiements de séquences de tâches.|  
|**Progression d'une séquence de tâches en cours d'exécution**|Affiche la progression de la séquence de tâches spécifiée.|  
|**Progression d'un déploiement de séquences de tâches en cours**|Affiche les informations de synthèse du déploiement de séquences de tâches spécifié.|  
|**Progression de tous les déploiements d'une séquence de tâches spécifique**|Affiche la progression de tous les déploiements de la séquence de tâches spécifiée.|  
|**Rapport récapitulatif d'un déploiement de séquences de tâches**|Affiche les informations de synthèse du déploiement de séquences de tâches spécifié.|  



## <a name="task-sequence---progress"></a>Séquence de tâches - Progression  
Les cinq rapports suivants sont répertoriés sous la catégorie **Séquence de tâches - Progression**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Graphique - Progression hebdomadaire d'une séquence de tâches**|Affiche la progression hebdomadaire d'une séquence de tâches à partir de la date de déploiement.|  
|**Progression d'une séquence de tâches**|Affiche la progression de la séquence de tâches spécifiée.|  
|**Progression de toutes les séquences de tâches**|Affiche le résumé de la progression de toutes les séquences de tâches.|  
|**Progression des séquences de tâches pour les déploiements de systèmes d'exploitation**|Affiche la progression de toutes les séquences de tâches qui déploient des systèmes d'exploitation.|  
|**État de tous les ordinateurs inconnus**|Affiche une liste des ordinateurs qui étaient inconnus au moment où ils ont exécuté un déploiement de séquences de tâches, et indique si ce sont désormais des ordinateurs connus.|  



## <a name="task-sequences---references"></a>Séquences de tâches - Références  
Le rapport suivant est répertoriés sous la catégorie **Séquence de tâches - Références**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Contenu référencé par une séquence de tâches spécifique**|Affiche le contenu qui est référencé par une séquence de tâches spécifiée.|  



<!--
## Upgrade Assessment  
The following 11 reports are listed under the **Upgrade Assessment** category.

|Report name|Description|  
|-----------------|-----------------|  
|**Application status for a specific computer**|Displays the compatibility of applications that are installed on a computer for a specified operating system.|  
|**Application status for computers in a specific collection**|Displays the overall status for computers in a collection to let you assess them for upgrade to a specified operating system based on the applications on each computer. Use this report to determine which computers have compatible applications before you deploy an operating system.|  
|**Application status summary**|Displays a summary of the application status for a specified operating system. Use this report to determine application compatibility before you deploy an operating system.|  
|**Computers with a specific application installed**|Displays computers with a specified application installed.|  
|**Computers with a specific hardware device**|Displays computers that have a specific hardware device.|  
|**Hardware device status for a specific computer**|Displays the compatibility status of hardware devices for a specified operating system that are found on a specified computer.|  
|**Hardware device status for computers in a specific collection**|Displays the overall status for hardware devices for a specified operating system for computers in a specified collection. Use this report to determine hardware compatibility before you deploy an operating system.|  
|**Hardware device status summary**|Displays a summary of hardware device status for a specified operating system. You can use this report to determine hardware device compatibility before you deploy an operating system.|  
|**Operating system hardware requirements**|Displays the minimum and recommended hardware criteria for operating systems.|  
|**Operating system requirement status for computers in a specific collection**|Displays the status of operating system requirements for the specified operating system for computers in a specified collection. Use this report to determine if a computer meets the specified operating system requirements for CPU processor speed, memory size, and hard disk space.|  
|**Upgrade assessment summary**|Displays the upgrade assessment summary. You can use this report to assess the overall status for upgrade compatibility.|  
-->



## <a name="user---device-affinity"></a>Affinité entre appareil et utilisateur  

Les deux rapports suivants sont répertoriés sous la catégorie **Utilisateur - Affinité des périphériques**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Associations d'affinités entre périphérique et utilisateur par regroupement en attente**|Ce rapport affiche toutes les attributions d'affinités entre utilisateur et périphérique en attente, selon les données d'utilisation, pour les membres d'un regroupement.|  
|**Associations d'affinités entre périphérique et utilisateur par regroupement**|Affiche toutes les associations entre appareil et utilisateur pour le regroupement spécifié et regroupe les résultats par type de regroupement (par exemple, utilisateur ou appareil).|  



## <a name="user-data-and-profiles-health"></a>Intégrité du profil et des données utilisateur  
Les quatre rapports suivants sont répertoriés sous la catégorie **Intégrité du profil et des données utilisateur**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Rapport d'intégrité de la redirection de dossiers - Détails**|Affiche les détails de l’état d’intégrité de la redirection de dossiers pour chacun des dossiers redirigés d’un utilisateur donné.|  
|**Rapport d'intégrité des profils utilisateur itinérants - Détails**|Affiche les détails de l’état d’intégrité du profil utilisateur itinérant d’un utilisateur spécifié.|  
|**Rapport d'intégrité des données et profils utilisateur - Détails**|Affiche les détails sur les erreurs ou les avertissements pour la redirection de dossiers ou les profils utilisateur itinérants. Ce rapport est la cible des détails à partir du rapport de synthèse.|  
|**Rapport d'intégrité des données et profils utilisateur - Résumé**|Affiche le résumé des états d'intégrité pour la redirection de dossiers et les profils utilisateur itinérants.|  



## <a name="users"></a>Utilisateurs  
Les trois rapports suivants sont répertoriés sous la catégorie **Utilisateurs**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Ordinateurs pour un nom d'utilisateur spécifique**|Affiche la liste des ordinateurs qui ont été utilisés par un utilisateur spécifié.|  
|**Compter les utilisateurs par domaine**|Affiche le nombre d'utilisateurs dans chaque domaine.|  
|**Utilisateurs dans un domaine spécifique**|Affiche la liste des utilisateurs et de leurs ordinateurs dans un domaine spécifié.|  



## <a name="virtual-applications"></a>Applications virtuelles  
Les sept rapports suivants sont répertoriés sous la catégorie **Applications virtuelles**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Résultats de l'environnement virtuel App-V**|Affiche des informations sur un environnement virtuel spécifié qui se trouve dans un état spécifié pour un regroupement spécifié.|  
|**Résultats de l'environnement virtuel App-V pour un composant**|Affiche des informations sur un environnement virtuel spécifié pour un composant donné. Il montre également tous les types de déploiements pour l’environnement virtuel spécifié.|  
|**État de l'environnement virtuel App-V**|Affiche des informations de compatibilité d'un environnement virtuel spécifié pour un regroupement spécifié.|  
|**Ordinateurs avec une application virtuelle spécifique**|Affiche le résumé des ordinateurs pour lesquels le raccourci de l'application App-V créé est spécifié comme utilisant Application Virtualization Management Sequencer.|  
|**Ordinateurs avec un package d'application virtuelle spécifique**|Affiche une synthèse des ordinateurs avec le package d’application App-V spécifié.|  
|**Total des instances de packages d'application virtuelle**|Afficher le nombre de packages d'application App-V détectés.|  
|**Total des instances d'applications virtuelles**|Affiche le nombre d'applications App-V détectées.|  



## <a name="volume-purchase-programs---apple"></a>Programmes d’achat en volume (VPP) - Apple
Le rapport suivant est répertorié sous la catégorie **Programmes d’achat en volume - Apple**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Applications du programme d’achat en volume (VPP) Apple pour iOS avec les nombres de licences**|Affiche toutes les applications iPhone, iPad et iPod Touch concédées sous licence par le biais du programme d’achat en volume (VPP) d’Apple. Ce rapport inclut également le nombre total de licences achetées ainsi que les licences consommées par application.|  



## <a name="vulnerability-assessment"></a>Évaluation de la vulnérabilité
Le rapport suivant est répertorié sous la catégorie **Évaluation de la vulnérabilité**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Rapport global d’évaluation de la vulnérabilité**|Identifie les vulnérabilités de conformité, de sécurité et d’administration d’un ordinateur spécifique|  



## <a name="wake-on-lan"></a>Éveil par appel réseau  
Les sept rapports suivants sont répertoriés sous la catégorie **Wake On LAN**.

|Nom du rapport|Description|  
|-----------------|-----------------|  
|**Tous les ordinateurs ciblés pour une activité d'éveil par appel réseau**|Indiquez le type de déploiement pour afficher une liste d’ordinateurs ciblés pour une activité Wake On LAN.|  
|**Tous les objets en attente de mise en éveil**|Affiche les objets qui sont programmés pour la mise en éveil.|  
|**Tous les sites activés pour l'éveil par appel réseau**|Affiche la liste de tous les sites de la hiérarchie qui sont activés pour l'éveil par appel réseau.|  
|**Erreurs reçues lors de l'envoi des paquets de mise en éveil pour une période donnée**|Affiche les erreurs reçues lors de l'envoi des paquets de mise en éveil aux ordinateurs pendant une période donnée.|  
|**Historique de l'activité d'éveil par appel réseau**|Affiche l'historique de l'activité d'éveil qui a eu lieu depuis un certain temps.|  
|**Détails sur l'état du déploiement de proxy de mise en éveil**|Affiche des informations sur l'état du déploiement de proxy de mise en éveil pour chaque appareil d'un regroupement spécifié.|  
|**Résumé de l'état de déploiement du proxy de mise en éveil**|Affiche le résumé de l'état de déploiement du proxy de mise en éveil pour un regroupement spécifié.|  
