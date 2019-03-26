---
title: Gérer Windows en tant que service
titleSuffix: Configuration Manager
description: Affichez l’état de Windows as a Service (WaaS) à l’aide de Configuration Manager, créez des plans de maintenance pour former des anneaux de déploiement et affichez des alertes quand la fin de support des clients Windows 10 est proche.
ms.date: 03/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 614ccc06a3fef5cca54c7eb1c32952e8531aedfa
ms.sourcegitcommit: d71e558db2da124357b840332e2da671b3810507
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58269057"
---
# <a name="manage-windows-as-a-service-using-system-center-configuration-manager"></a>Gérer Windows as a Service (WaaS) à l’aide de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Dans Configuration Manager, vous pouvez voir l’état de Windows as a Service (WaaS) dans votre environnement. Créez des plans de maintenance pour former des anneaux de déploiement et vérifiez que les systèmes Windows 10 sont mis à jour quand de nouvelles builds sont publiées. Vous pouvez également voir des alertes pour les clients Windows 10 quand la fin de support de leur build Canal semi-annuel approche.  

 Pour plus d’informations sur les options de maintenance de Windows 10, consultez [Vue d’ensemble de Windows as a Service](/windows/deployment/update/waas-overview#servicing-channels).  

 Aidez-vous des informations des sections suivantes pour gérer Windows as a Service.



##  <a name="BKMK_Prerequisites"></a> Conditions préalables  
 Pour voir les données dans le tableau de bord de maintenance de Windows 10, vous devez effectuer les actions suivantes :  

-   Les ordinateurs Windows 10 doivent utiliser les mises à jour logicielles de Configuration Manager avec les services WSUS (Windows Server Update Services) pour la gestion des mises à jour logicielles. Quand un ordinateur utilise Windows Update pour Entreprise (ou Windows Insiders) pour la gestion des mises à jour logicielles, il n’est pas évalué dans les plans de maintenance de Windows 10. Pour plus d'informations, voir [Intégration avec Windows Update for Business dans Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   WSUS 4.0 avec le [correctif logiciel 3095113](https://support.microsoft.com/kb/3095113) doit être installé sur les points de mise à jour logicielle et les serveurs de site. Ce correctif ajoute la classification de mise à jour logicielle **Mises à niveau**. Pour plus d’informations, consultez [Prérequis pour les mises à jour logicielles](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   WSUS 4.0 avec le [correctif logiciel 3159706](https://support.microsoft.com/kb/3159706) doit être installé sur les points de mise à jour logicielle et les serveurs de site pour mettre à niveau les ordinateurs avec la mise à jour anniversaire Windows 10 ou une version ultérieure. Pour installer ce correctif logiciel, vous devez effectuer manuellement certaines étapes, comme décrit dans l’article du support technique. Pour plus d’informations, consultez le [Blog de l’équipe Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/).

-   Activez la découverte par pulsations d’inventaire. Les données affichées dans le tableau de bord de maintenance de Windows 10 sont trouvées à l’aide de la détection. Pour plus d’informations, consultez [Configurer la découverte par pulsations d’inventaire](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).  

     Les informations de canal et de build Windows 10 suivantes sont découvertes et stockées dans les attributs suivants :  

    -   **Branche de disponibilité du système d’exploitation** : Spécifie le canal du système d’exploitation. Par exemple, **0** = Canal semi-annuel - ciblé (ne pas reporter les mises à jour), **1** = Canal semi-annuel (différer les mises à jour), **2** = Canal de maintenance à long terme (LTSC)

    -   **Build du système d’exploitation** : spécifie le numéro de build du système d’exploitation. Par exemple, **10.0.10240** (RTM) ou **10.0.10586** (version 1511)  

-   Le point de connexion de service doit être installé et configuré pour le mode **En ligne, connexion permanente** afin de voir les données dans le tableau de bord de maintenance de Windows 10. En mode hors connexion, vous ne voyez pas les mises à jour des données dans le tableau de bord tant que vous n’avez pas obtenu les mises à jour de maintenance de Configuration Manager. Pour plus d’informations, consultez [À propos du point de connexion de service](../../core/servers/deploy/configure/about-the-service-connection-point.md).  


-   Internet Explorer 9 ou version ultérieure doit être installé sur l’ordinateur qui exécute la console Configuration Manager.  

-   Les mises à jour logicielles doivent être configurées et synchronisées. Sélectionnez la classification **Mises à niveau** et synchronisez les mises à jour logicielles pour que les mises à niveau de fonctionnalités Windows 10 soient disponibles dans la console Configuration Manager. Pour plus d’informations, consultez [Préparer la gestion des mises à jour logicielles](../../sum/get-started/prepare-for-software-updates-management.md).  

##  <a name="BKMK_ServicingDashboard"></a> Tableau de bord de maintenance de Windows 10  
 Le tableau de bord de maintenance de Windows 10 fournit des informations sur les ordinateurs Windows 10 de votre environnement, les plans de maintenance actifs, les informations de conformité et ainsi de suite. Les données du tableau de bord de maintenance de Windows 10 dépendent de l’installation du point de connexion de service. Le tableau de bord comporte les vignettes suivantes :  

-   **Vignette Utilisation Windows 10** : Fournit des informations détaillées sur les builds publiques de Windows 10. Les builds Windows Insiders sont répertoriées comme **autres** , de même que celles qui ne sont pas encore connues de votre site. Le point de connexion de service télécharge les métadonnées qui lui donnent des informations sur les builds Windows, puis ces données sont comparées aux données de découverte.  

-   **Vignette Boucles Windows 10** : Fournit une vue détaillée de Windows 10 par canal et état de préparation. Le segment LTSC inclut toutes les versions LTSC. La première vignette détaille les versions spécifiques, par exemple, Windows 10 LTSC 2015.   

-   **Vignette Créer un plan de maintenance** : Permet de créer rapidement un plan de maintenance. Vous spécifiez le nom, le regroupement (seuls les 10 premiers regroupements sont affichés par taille, le plus petit en premier), le package de déploiement (seuls les 10 derniers packages modifiés sont affichés) et l’état de préparation. Des valeurs par défaut sont utilisées pour les autres paramètres. Cliquez sur **Paramètres avancés** pour démarrer l’Assistant Créer un plan de maintenance, dans lequel vous pouvez configurer tous les paramètres du plan de maintenance.  

-   **Vignette Expiré**: affiche le pourcentage d’appareils qui utilisent une build de Windows 10 qui est au-delà de sa fin de vie. Configuration Manager détermine ce pourcentage à partir des métadonnées téléchargées par le point de connexion de service et le compare aux données de découverte. Une build qui a dépassé sa fin de vie ne reçoit plus de mises à jour cumulatives mensuelles, qui comprennent des mises à jour de sécurité. Vous devez mettre à niveau les ordinateurs de cette catégorie vers la version de build suivante. Configuration Manager arrondit au nombre entier supérieur. Par exemple, si vous avez 10 000 ordinateurs et qu’un seul utilise une build expirée, la vignette affiche 1 %.  

-   **Vignette Expiration proche**: affiche le pourcentage d’ordinateurs qui utilisent une build qui est proche de sa fin de vie (dans les quatre mois qui précèdent, environ), de manière analogue à la vignette **Expiré** . Configuration Manager arrondit au nombre entier supérieur.  

-   **Vignette Alertes**: affiche les alertes actives.  

-   **Vignette Surveillance du plan de maintenance**: affiche les plans de maintenance que vous avez créés et un graphique de conformité pour chacun. Cette vignette donne un aperçu rapide de l’état actuel des déploiements de plan de maintenance. Si une boucle de déploiement précédente répond à vos attentes en matière de conformité, vous pouvez sélectionner un plan de maintenance (boucle de déploiement) ultérieur et cliquer sur **Déployer maintenant** au lieu d’attendre que les règles du plan de maintenance soient déclenchées automatiquement.  

-   **Vignette Builds Windows 10** : Affiche une chronologie fixe qui fournit une vue d’ensemble des builds Windows 10 actuellement publiées, et donne une idée générale du moment où les builds passent à des états différents.  

> [!IMPORTANT]  
>  Les informations affichées dans le tableau de bord de maintenance de Windows 10 (telles que le cycle de vie de prise en charge des versions de Windows 10) sont fournies à des fins de commodité et destinées uniquement à une utilisation en interne dans votre société. Vous ne devez pas vous fier uniquement à ces informations pour confirmer la conformité des mises à jour. Veillez à vérifier l’exactitude des informations qui vous sont fournies.  

## <a name="servicing-plan-workflow"></a>Flux de travail de plan de maintenance  
 Les plans de maintenance de Windows 10 dans Configuration Manager s’apparentent à des règles de déploiement automatique pour les mises à jour logicielles. Vous créez un plan de maintenance avec les critères suivants évalués par Configuration Manager :  

- **Classification Mises à niveau**: seules les mises à jour figurant dans la classification **Mises à niveau** sont évaluées.  

- **État de disponibilité**: l’état de disponibilité défini dans le plan de maintenance est comparé à celui pour la mise à niveau. Les métadonnées pour la mise à niveau sont récupérées quand le point de connexion de service recherche des mises à jour.  

- **Report**: nombre de jours que vous spécifiez en réponse à la question **Combien de jours après la publication par Microsoft d’une nouvelle mise à niveau voulez-vous attendre avant un déploiement dans votre environnement ?** dans le plan de maintenance. Si la date actuelle est la date de publication plus le nombre de jours configuré, Configuration Manager évalue s’il faut ajouter une mise à niveau dans le déploiement.  

  Quand une mise à niveau répond aux critères, le plan de maintenance l’ajoute au package de déploiement, distribue le package aux points de distribution et déploie la mise à niveau vers le regroupement en fonction des paramètres que vous configurez dans le plan de maintenance. Vous pouvez surveiller les déploiements dans la vignette Surveillance du plan de maintenance du tableau de bord Maintenance de Windows 10. Pour plus d’informations, consultez [Surveiller les mises à jour logicielles](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="BKMK_ServicingPlan"></a> Plan de maintenance de Windows 10  
 Quand vous déployez Windows 10 Canal semi-annuel, vous pouvez créer un ou plusieurs plans de maintenance pour définir les boucles de déploiement que vous souhaitez dans votre environnement, puis les surveiller dans le tableau de bord de maintenance de Windows 10. Les plans de maintenance utilisent seulement la classification des mises à jour logicielles **Mises à niveau** et non pas les mises à jour cumulatives pour Windows 10. Pour ces mises à jour, vous devez toujours effectuer le déploiement à l’aide du flux de travail des mises à jour logicielles. L’expérience de l’utilisateur final avec un plan de maintenance est la même qu’avec les mises à jour logicielles, y compris les paramètres que vous configurez dans le plan de maintenance.  

> [!NOTE]  
>  Vous pouvez utiliser une séquence de tâches pour déployer une mise à niveau pour chaque build de Windows 10, mais cela nécessite davantage d’opérations manuelles. Il vous faudrait importer les fichiers sources mis à jour en tant que package de mise à niveau du système d’exploitation, puis créer et déployer la séquence de tâches sur l’ensemble d’ordinateurs approprié. Toutefois, une séquence de tâches fournit des options personnalisées supplémentaires, telles que les actions de prédéploiement et de post-déploiement.  

 Vous pouvez créer un plan de maintenance de base à partir du tableau de bord de maintenance de Windows 10. Une fois que vous avez spécifié le nom, le regroupement (seuls les 10 premiers regroupements sont affichés par taille, le plus petit en premier), le package de déploiement (seuls les 10 derniers packages modifiés sont affichés) et l’état de préparation, Configuration Manager crée le plan de maintenance avec des valeurs par défaut pour les autres paramètres. Vous pouvez également démarrer l’Assistant Créer un plan de maintenance pour configurer tous les paramètres. Pour créer un plan de maintenance à l’aide de l’Assistant Créer un plan de maintenance, appliquez la procédure suivante.  

> [!NOTE]  
>  Vous pouvez gérer le comportement des déploiements à haut risque. Un déploiement à haut risque est un déploiement qui est installé automatiquement et qui est susceptible d'entraîner des résultats indésirables. Par exemple, une séquence de tâches ayant comme objectif **Obligatoire** qui déploie Windows 10 est considérée comme un déploiement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### <a name="to-create-a-windows-10-servicing-plan"></a>Pour créer un plan de maintenance de Windows 10  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l’espace de travail Bibliothèque de logiciels, développez **Maintenance de Windows 10**, puis cliquez sur **Plans de maintenance**.  

3. Sous l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un plan de maintenance**. L’Assistant Créer un plan de maintenance s’ouvre.  

4. Sur la page **Général** , configurez les paramètres suivants :  

   -   **Nom**: spécifiez le nom du plan de maintenance. Le nom doit être unique, décrire clairement l’objectif de la règle et être identifiable parmi d’autres dans le site Configuration Manager.  

   -   **Description**: spécifiez la description du plan de maintenance. La description doit fournir une vue d’ensemble du plan de maintenance et toute autre information pertinente permettant de l’identifier et de le différencier des autres plans dans le site Configuration Manager. Le champ de description facultatif est limité à 256 caractères et est vierge par défaut.  

5. Dans la page Plan de maintenance, configurez les paramètres suivants :  

   -   **Regroupement cible**: spécifie le regroupement cible à utiliser pour le plan de maintenance. Les membres du regroupement reçoivent les mises à niveau de Windows 10 qui sont définies dans le plan de maintenance.  

       > [!NOTE]  
       >  Quand vous effectuez un déploiement à haut risque, par exemple, un plan de maintenance, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements personnalisés qui répondent aux paramètres de vérification de déploiement configurés dans les propriétés du site.
       >    
       > Les déploiements à haut risque sont toujours limités aux regroupements personnalisés, aux regroupements que vous créez et au regroupement **Ordinateurs inconnus** intégré. Quand vous créez un déploiement à haut risque, vous ne pouvez pas sélectionner un regroupement intégré tel que **Tous les systèmes**. Désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site** pour afficher tous les regroupements personnalisés qui contiennent moins de clients que la taille maximale configurée. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
       >  
       > Les paramètres de vérification de déploiement sont basés sur l'appartenance actuelle du regroupement. Une fois le plan de maintenance déployé, l’appartenance du regroupement n’est pas réévaluée pour les paramètres de déploiement à haut risque.  
       >  
       > Supposons que vous affectez la valeur 100 à **Taille par défaut** et la valeur 1000 à **Taille maximale**. Quand vous créez un déploiement à haut risque, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements qui contiennent moins de 100 clients. Si vous désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site**, la fenêtre affiche les regroupements qui contiennent moins de 1 000 clients.  
       >
       > Quand vous sélectionnez un regroupement qui contient un rôle de site, le critère suivant s’applique :    
       >   
       >    - Si le regroupement contient un serveur de système de site et que dans les paramètres de vérification de déploiement vous choisissez de bloquer les regroupements contenant des serveurs de système de site, une erreur se produit et vous ne pouvez pas continuer.    
       >    - Si le regroupement contient un serveur de système de site et que dans les paramètres de vérification de déploiement vous choisissez d'afficher un avertissement dans le cas où des regroupements contiennent des serveurs de système de site, si  le regroupement dépasse la valeur de taille par défaut, ou si le regroupement contient un serveur, l'Assistant Déploiement logiciel affiche un avertissement de risque élevé. Vous devez accepter de créer un déploiement à risque élevé et un message d'état d'audit est créé.  

6. Dans la page Boucle de déploiement, configurez les paramètres suivants :  

   -   **Spécifiez l’état de disponibilité Windows auquel ce plan de maintenance doit s’appliquer** : sélectionnez l’une des options suivantes :  

       -   **Canal semi-annuel (ciblé)** : Dans le modèle de maintenance, les mises à jour de fonctionnalités sont disponibles dès leur publication par Microsoft.

       -   **Canal semi-annuel** : Ce canal de maintenance est généralement utilisé pour les vastes déploiements. Les clients Windows 10 en Canal semi-annuel reçoivent la même build de Windows 10 que les appareils du canal ciblé, mais un peu plus tard.

       Pour plus d’informations sur les canaux de maintenance et les options qui vous conviennent le mieux, consultez [Canaux de maintenance](/windows/deployment/update/waas-overview#servicing-channels).

   -   **Combien de jours après la publication par Microsoft d’une nouvelle mise à niveau voulez-vous attendre avant un déploiement dans votre environnement** : Si la date actuelle est la date de publication plus le nombre de jours configuré pour ce paramètre, Configuration Manager évalue s’il faut ajouter une mise à niveau dans le déploiement.


7. Dans la page Mises à niveau, configurez les critères de recherche pour filtrer les mises à niveau ajoutées au plan de maintenance. Seules les mises à jour qui remplissent les critères spécifiés sont ajoutées au déploiement associé. Les filtres de propriétés suivantes sont disponibles : <!--3098809, 3113836, 3204570 -->

   - **Architecture** (depuis la version 1810)
   - **Langue**
   - **Catégorie de produit** (depuis la version 1810)
   - **Obligatoire**
      > [!Important]    
      > Dans vos critères de recherche, nous vous recommandons de définir le champ **Obligatoire** avec la valeur **>=1**. Ce critère permet d’ajouter seulement les mises à jour applicables au plan de maintenance.
   - **Remplacée** (depuis la version 1810)
   - **Titre**

    Cliquez sur **Aperçu** pour afficher les mises à niveau qui répondent aux critères spécifiés.  

8. Sur la page Calendrier de déploiement, configurez les paramètres suivants :  

   -   **Calendrier d’évaluation** : indiquez si Configuration Manager évalue la durée disponible et la date d’échéance de l’installation à l’heure UTC ou à l’heure locale de l’ordinateur exécutant la console Configuration Manager.  

       > [!NOTE]  
       >  Si vous sélectionnez l’heure locale, puis **Dès que possible** pour le **Temps disponible du logiciel** ou **Échéance d’installation**, l’heure actuelle sur l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer quand les mises à jour sont disponibles ou quand elles sont installées sur un client. Si le client est dans un autre fuseau horaire, ces actions se produisent quand l’heure du client atteint l’heure de l’évaluation.  

   -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

       -   **Dès que possible**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement et peuvent obtenir les mises à jour disponibles à l'installation.  

       -   **Heure spécifique**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et heure précises. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement. Toutefois, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles à l'installation avant la date et l'heure configurées.  

   -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement :  

       -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

       -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Configuration Manager détermine l’échéance d’installation des mises à jour logicielles en ajoutant l’intervalle **Heure spécifique** configuré au **Temps disponible du logiciel**.  

           > [!NOTE]  
           >  L'heure d'échéance de l'installation réelle est l'heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre 2 heures. Elle permet de réduire l’impact lié à l’installation simultanée, par tous les ordinateurs clients du regroupement de destination, des mises à jour incluses dans le déploiement.  
           >   
           >  Vous pouvez configurer le paramètre client **Agent ordinateur** , **Désactiver la randomisation des échéances** , pour désactiver le délai de randomisation de l’installation des mises à jour requises. Pour plus d’informations, voir [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

9. Sur la page Expérience utilisateur, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur**: indiquez si vous souhaitez afficher les notifications des mises à jour dans le Centre logiciel sur l’ordinateur client d’après la valeur **Temps disponible du logiciel** configurée et si des notifications doivent s’afficher sur les ordinateurs clients.  

    -   **Comportement à l’échéance**: spécifiez le comportement qui doit se produire quand l’échéance est atteinte pour le déploiement des mises à jour. Indiquez si vous souhaitez installer les mises à jour incluses dans le déploiement. Spécifiez également si un redémarrage du système doit être effectué après l’installation des mises à jour, quelle que soit la fenêtre de maintenance configurée. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportement de redémarrage du périphérique**: indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé une fois les mises à jour installées, et si un redémarrage du système est nécessaire pour terminer l’installation.  

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded**: quand vous déployez des mises à jour sur des appareils Windows Embedded pour lesquels le filtre d’écriture est activé, vous pouvez choisir d’installer la mise à jour sur le segment de recouvrement temporaire et valider les modifications ultérieurement ou à l’échéance de l’installation ou bien pendant une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

        > [!NOTE]  
        >  Quand vous déployez une mise à jour sur un appareil Windows Embedded, assurez-vous que l’appareil fait partie des membres d’un regroupement pour lequel une fenêtre de maintenance a été configurée.  

10. Sur la page Package de déploiement, sélectionnez un package de déploiement existant ou configurez les paramètres suivants pour créer un package de déploiement :  

    1.  **Nom**: spécifiez le nom du package de déploiement. Ce nom doit être unique et décrit le contenu du package. Il est limité à 50 caractères.  

    2.  **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description est limitée à 127 caractères.  

    3.  **Source du package**: spécifie l’emplacement des fichiers sources des mises à jour logicielles. Tapez un chemin réseau pour l’emplacement source, par exemple **\\\serveur\nom_partage\chemin**ou cliquez sur **Parcourir** pour rechercher l’emplacement réseau. Créez le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

        > [!NOTE]  
        >  L'emplacement source du package de déploiement que vous spécifiez ne peut pas être utilisé par un autre package de déploiement de logiciel.  

        > [!IMPORTANT]  
        >  Le compte d'ordinateur du fournisseur SMS et l'utilisateur qui exécute l'Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations NTFS en **Écriture** sur l'emplacement de téléchargement. Vous devez soigneusement limiter l'accès à l'emplacement de téléchargement pour éviter que des personnes malintentionnées ne falsifient les fichiers sources des mises à jour logicielles.  

        > [!IMPORTANT]  
        >  Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Mais le cas échéant, vous devez d'abord copier le contenu à partir de la source du package d'origine vers le nouvel emplacement source du package.  

    4.  **Priorité d’expédition**: spécifiez la priorité d’envoi pour le package de déploiement. Configuration Manager utilise la priorité d’expédition du package de déploiement quand il envoie le package aux points de distribution. Les packages de déploiement sont envoyés par ordre de priorité : Haute, Moyenne ou Faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. S’il n’y a pas de backlog, le package est traité immédiatement, quelle que soit sa priorité.  

11. Dans la page Points de distribution, spécifiez les points de distribution ou les groupes de points de distribution qui hébergent les fichiers de mise à jour. Pour plus d’informations sur les points de distribution, consultez [Configurer un point de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).

    > [!NOTE]  
    >  Cette page est disponible uniquement lorsque vous créez un nouveau package de déploiement de mise à jour logicielle.  

12. Dans la page Emplacement de téléchargement, indiquez si les fichiers de mise à jour doivent être téléchargés à partir d’Internet ou de votre réseau local. Configurez les paramètres suivants :  

    -   **Télécharger les mises à jour logicielles depuis Internet**: sélectionnez ce paramètre pour télécharger les mises à jour à partir d’un emplacement spécifié sur Internet. Ce paramètre est activé par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger les mises à jour à partir d’un répertoire local ou d’un dossier partagé. Ce paramètre s'avère utile lorsque l'ordinateur exécutant l'Assistant ne dispose d'aucun accès à Internet. N’importe quel ordinateur connecté à Internet peut préalablement télécharger les mises à jour et les stocker à un emplacement sur le réseau local qui est accessible à partir de l’ordinateur qui exécute l’Assistant.  

13. Dans la page Sélection de la langue, sélectionnez les langues pour lesquelles les mises à jour sélectionnées sont téléchargées. Les mises à jour sont téléchargées uniquement si elles sont disponibles dans les langues sélectionnées. Les mises à jour qui ne sont pas propres à une langue sont toujours téléchargées. Par défaut, l'Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qui ne sont pas prises en charge par une mise à jour, le téléchargement de cette mise à jour échoue.  

14. Dans la page Résumé, examinez les paramètres et cliquez sur **Suivant** pour créer le plan de maintenance.  

    Une fois l’Assistant terminé, le plan de maintenance est exécuté. Il ajoute à un groupe de mises à jour logicielles les mises à jour qui correspondent aux critères spécifiés, télécharge les mises à jour dans la bibliothèque de contenu sur le serveur de site, distribue les mises à jour aux points de distribution configurés, puis déploie le groupe de mises à jour logicielles sur les clients du regroupement cible.  

##  <a name="BKMK_ModifyServicingPlan"></a> Modifier un plan de maintenance  
Après avoir créé un plan de maintenance de base à partir du tableau de bord de maintenance de Windows 10, ou si vous devez modifier les paramètres d’un plan de maintenance existant, vous pouvez accéder à ses propriétés.

> [!NOTE]
> Vous pouvez configurer des paramètres dans les propriétés du plan de maintenance qui ne sont pas disponibles dans l’Assistant quand vous créez le plan. L’Assistant utilise les valeurs par défaut pour les paramètres des éléments suivants : paramètres de téléchargement, paramètres de déploiement et alertes.  

Pour modifier les propriétés d’un plan de maintenance, appliquez la procédure suivante.  

#### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Pour modifier les propriétés d’un plan de maintenance  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail Bibliothèque de logiciels, développez **Maintenance de Windows 10**, cliquez sur **Plans de maintenance**, puis sélectionnez le plan de maintenance que vous souhaitez modifier.  

3.  Sous l’onglet **Accueil** cliquez sur **Propriétés** pour ouvrir les propriétés du plan de maintenance sélectionné.

    Les paramètres suivants sont disponibles dans les propriétés du plan de maintenance qui n’ont pas été configurées dans l’Assistant :

    **Paramètres de déploiement** : dans la page Paramètres de déploiement, configurez les paramètres suivants :  

    -   **Type de déploiement**: indique le type de déploiement pour le déploiement des mises à jour logicielles. Sélectionnez **Obligatoire** pour créer un déploiement de mises à jour logicielles obligatoire où les mises à jour logicielles sont installées automatiquement sur les clients selon une échéance d'installation configurée. Sélectionnez **Disponible** pour créer un déploiement de mises à jour logicielles facultatives que les utilisateurs peuvent installer à partir du Centre logiciel.  

        > [!IMPORTANT]  
        >  Après avoir créé le déploiement de mises à jour logicielles, vous ne pourrez pas modifier ultérieurement le type de déploiement.  

        > [!NOTE]  
        >  Un groupe de mises à jour logicielles déployé avec l’option **Obligatoire** est téléchargé en arrière-plan et respecte les paramètres BITS, s’ils sont configurés.  
        >  
        > Toutefois, les groupes de mises à jour logicielles déployés avec l’option **Disponible** sont téléchargés au premier plan et ignorent les paramètres BITS.  

    -   **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis**: indiquez si l’éveil par appel réseau (Wake On LAN) doit être activé à l’échéance pour envoyer des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles du déploiement. Tous les ordinateurs en mode veille à l’échéance de l’installation sont mis en éveil pour que l’installation des mises à jour logicielles puisse démarrer. Les clients en mode veille qui ne nécessitent pas les mises à jour logicielles incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n'est pas activé et il est disponible uniquement lorsque le **Type de déploiement** est défini sur **Obligatoire**.  

        > [!WARNING]  
        >  Pour que vous puissiez utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour utiliser l'éveil par appel réseau.  

    -   **Niveau de détail**: indiquez le niveau de détail pour les messages d’état qui sont signalés par les ordinateurs clients.  

    **Paramètres de téléchargement** : sous l’onglet Paramètres de téléchargement, configurez les paramètres suivants :  

    - Indiquez si le client télécharge et installe les mises à jour logicielles quand il est connecté à un réseau lent ou qu’il utilise un emplacement de secours pour le contenu.  

    - Indiquez si le client doit télécharger et installer les mises à jour logicielles à partir d'un point de distribution de secours quand le contenu pour les mises à jour logicielles n'est pas disponible sur un point de distribution préféré.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations sur BranchCache, consultez [Concepts fondamentaux de la gestion de contenu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Indiquez si les clients doivent télécharger les mises à jour logicielles à partir de Microsoft Update si elles ne sont pas disponibles sur des points de distribution.
        > [!IMPORTANT]
        > N’utilisez pas ce paramètre pour les mises à jour de maintenance de Windows 10. Configuration Manager (au moins jusqu’à la version 1610) ne peut pas télécharger les mises à jour de maintenance de Windows 10 à partir de Microsoft Update.

    -   Indiquez si les clients peuvent procéder au téléchargement une fois l’échéance de l’installation dépassée dans le cas où ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.   

    **Alertes** : Sous l’onglet Alertes, configurez la manière dont Configuration Manager et System Center Operations Manager génèrent les alertes pour ce déploiement. Vous pouvez configurer des alertes uniquement lorsque **Type de déploiement** est défini sur **Obligatoire** sur la page Paramètres de déploiement.  

    > [!NOTE]  
    >  Vous pouvez consulter les récentes alertes de mises à jour logicielles à partir du nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

**Pour plus d’informations :** <br/>
[Notions de base de Configuration Manager as a service et Windows as a service](/sccm/core/understand/configuration-manager-and-windows-as-service.md)
