---
title: 'Exemple de scénario : Déployer des clients Windows Embedded'
titleSuffix: Configuration Manager
description: Consultez un exemple de scénario de déploiement et de gestion de clients System Center Configuration Manager sur des appareils Windows Embedded.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fdca69faefa693299d8975ec1af60f7624bc73c2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="example-scenario-for-deploying-and-managing-system-center-configuration-manager-clients-on-windows-embedded-devices"></a>Exemple de scénario de déploiement et de gestion de clients System Center Configuration Manager sur des appareils Windows Embedded

*S’applique à : System Center Configuration Manager (Current Branch)*

Ce scénario montre comment vous pouvez gérer des appareils Windows Embedded activés pour les filtres d’écriture avec Configuration Manager. Si vos appareils incorporés ne prennent pas en charge les filtres d’écriture, ils se comportent comme des clients Configuration Manager standard et ces procédures ne s’appliquent pas.  

Coho Vineyard & Winery ouvre un centre d’accueil et a besoin de bornes qui utilisent Windows Embedded pour exécuter des présentations interactives. Le bâtiment du nouveau centre d’accueil n’étant pas proche du service informatique, les bornes doivent être gérées à distance. Outre le logiciel qui exécute les présentations, ces appareils doivent exécuter des logiciels anti-programmes malveillants actualisés pour se conformer aux stratégies de sécurité de l’entreprise. Les bornes doivent fonctionner 7 jours par semaine, sans interruption pendant les heures d’ouverture du centre d’accueil.  

 Coho utilise déjà Configuration Manager pour gérer les appareils de son réseau. Configuration Manager est configuré pour exécuter Endpoint Protection et pour installer les mises à jour logicielles et les applications. Toutefois, sachant que l’équipe informatique n’a jamais géré d’appareils Windows Embedded auparavant, Jane, administratrice de Configuration Manager, a mis en place un pilote pour gérer deux bornes situées dans le hall de réception.   

 Pour gérer ces appareils Windows Embedded à filtre d’écriture, Jane effectue les étapes suivantes pour installer le client Configuration Manager, le protéger à l’aide d’Endpoint Protection et installer le logiciel de présentation interactive.  

1.  Jane s’informe de la manière dont les appareils Windows Embedded utilisent les filtres d’écriture, puis de la manière dont Configuration Manager peut simplifier cette utilisation en désactivant, puis en réactivant automatiquement ces filtres d’écriture, dans le but de conserver une installation logicielle.  

     Pour plus d’informations, consultez [Planification du déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2.  Avant d’installer le client Configuration Manager, Jane crée un regroupement d’appareils basé sur une requête pour les appareils Windows Embedded. Comme l’entreprise utilise des formats d’attribution de noms standard pour identifier ses ordinateurs, Jane peut identifier les appareils Windows Embedded de façon univoque par les six premières lettres du nom de l’ordinateur : **WEMDVC**. Elle utilise la requête WQL suivante pour créer ce regroupement : **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

     Ce regroupement lui permet de gérer les appareils Windows Embedded avec des options de configuration différentes des autres appareils. Elle utilise ce regroupement pour contrôler les redémarrages, déployer Endpoint Protection avec les paramètres du client et déployer l'application de présentation interactive.  

     Voir [Comment créer des regroupements dans System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md).  

3.  Jane configure le regroupement pendant une fenêtre de maintenance pour veiller à ce que les redémarrages nécessaires pour installer l'application de présentation et toutes les éventuelles mises à jour ne se produisent pas pendant les heures d'ouverture du centre d'accueil. Le centre est ouvert de 9h00 à 18h00, du lundi au dimanche. Elle configure la fenêtre de maintenance de sorte à ce qu'elle se produise tous les jours, de 18h30 à 6h00.  

4.  Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5.  Jane configure ensuite un paramètre client personnalisé pour les appareils en vue d'installer le client Endpoint Protection en sélectionnant **Oui** pour les paramètres suivants, puis elle déploie ce paramètre client personnalisé sur le regroupement d’appareils Windows Embedded :  

    -   **Installer le client Endpoint Protection sur les ordinateurs clients**  

    -   **Pour les appareils Windows Embedded munis de filtres d'écriture, valider l'installation du client Endpoint Protection (nécessite un redémarrage)**  

    -   **Autoriser l'installation et le redémarrage du client Endpoint Protection en dehors des fenêtres de maintenance**  

     Quand le client Configuration Manager est installé, ces paramètres permettent d’installer le client Endpoint Protection et de garantir qu’il est maintenu dans le système d’exploitation pendant l’installation, au lieu d’être seulement écrit dans le segment de recouvrement. Les stratégies de sécurité de l'entreprise exigent une installation permanente du logiciel anti-programme malveillant et Jane ne veut pas prendre le risque de laisser les bornes sans protection même pendant un court instant alors qu'ils redémarrent.  

    > [!NOTE]  
    >  Les redémarrages requis pour installer le client Endpoint Protection ne se produisent qu'une seule fois, pendant la période d'installation des appareils et avant que le centre d'accueil ne soit opérationnel. À la différence du déploiement périodique d’applications ou de mises à jour de définitions logicielles, la prochaine installation du client Endpoint Protection sur le même appareil aura probablement lieu quand l’entreprise procédera à la mise à niveau vers la prochaine version de Configuration Manager.  

     Pour plus d’informations, consultez [Configuration d’Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md).  

6.  Maintenant que les paramètres de configuration du client sont en place, Jane prépare l’installation des clients Configuration Manager. Avant de pouvoir installer les clients, elle doit désactiver manuellement le filtre d'écriture sur les appareils Windows Embedded. Elle lit la documentation du fabricant qui accompagne les bornes et suit les instructions pour désactiver les filtres d'écriture.  

     Jane renomme l’appareil pour qu’il utilise le format d’attribution de noms standard de l’entreprise, puis elle installe le client manuellement en exécutant CCMSetup à l’aide de la commande suivante, à partir d’un lecteur mappé qui contient les fichiers sources du client : **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

     Cette commande permet d'installer le client, d'affecter le client au point de gestion dont le nom de domaine complet de l'intranet est **mpserver.cohovineyardandwinery.com**, puis d'affecter le client au site principal nommé **CO1**.  

     Jane sait qu'il faut toujours un certain temps pour que les clients s'installent et renvoient leur état au site. Par conséquent, elle patiente avant de confirmer l'installation correcte des clients, leur affectation au site et leur affichage en tant que clients dans le regroupement qu'elle a créé pour les appareils Windows Embedded.  

     Comme contrôle supplémentaire, elle vérifie les propriétés de Configuration Manager dans le Panneau de configuration sur les appareils et les compare aux ordinateurs Windows standard gérés par le site. Par exemple, sous l'onglet **Composants** , l'élément **Agent de l'inventaire matériel** affiche **Activé**et sous l'onglet **Actions** figurent 11 actions disponibles, notamment **Cycle d'évaluation du déploiement de l'application** et **Cycle de collecte de données de découverte**.  

     Certaine que les clients sont correctement installés et affectés, et que le point de gestion leur envoie la stratégie client, Jane active ensuite manuellement les filtres d'écriture en suivant les instructions du fabricant.  

     Pour plus d'informations, voir :  

    -   [Guide pratique pour déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

    -   [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7.  Maintenant que le client Configuration Manager est installé sur les appareils Windows Embedded, Jane vérifie qu’elle peut les gérer de la même manière que les clients Windows standard. Par exemple, à partir de la console Configuration Manager, elle peut les gérer à distance à l’aide du contrôle à distance, leur appliquer la stratégie et afficher les propriétés du client, ainsi que l’inventaire matériel.  

     Comme ces appareils sont joints à un domaine Active Directory, elle n’a pas besoin de les confirmer manuellement en tant que clients approuvés ; pour cela, elle utilise la console Configuration Manager.  

     Pour plus d'informations, voir [Comment gérer des clients dans Configuration Manager](../../../core/clients/manage/manage-clients.md).  

8.  Pour installer le logiciel de présentation interactive, Jane exécute l' **Assistant Déploiement logiciel** et configure une application requise. Sur la page **Expérience utilisateur** de l'Assistant, dans la section **Traitement des filtres d'écriture pour les appareils Windows Embedded** , elle accepte l'option par défaut qui sélectionne **Valider les changements à l'échéance ou pendant une fenêtre de maintenance (redémarrage requis)**.  

     Jane garde cette option par défaut pour les filtres d'écriture pour garantir la conservation de l'application après un redémarrage, afin qu'elle soit toujours disponible pour les visiteurs qui utilisent les bornes. La fenêtre de maintenance quotidienne offre une période sans risque au cours de laquelle les redémarrages d'installation et les mises à jour peuvent se produire.  

     Jane déploie l'application sur le regroupement d’appareils Windows Embedded.  

     Pour plus d’informations, consultez [Comment déployer des applications avec System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Pour configurer les mises à jour de définitions pour Endpoint Protection, Jane utilise des mises à jour logicielles et exécute l'Assistant Création d'une règle de déploiement automatique. Elle sélectionne le modèle **Mises à jour de définitions** pour préremplir l'Assistant avec les paramètres appropriés à Endpoint Protection.  

     Ces paramètres incluent les éléments suivants sur la page **Expérience utilisateur** de l'Assistant :  

    -   **Comportement à l’échéance**: la case **Installation du logiciel** n’est pas cochée.  

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded**: la case **Valider les changements à l’échéance ou pendant une fenêtre de maintenance (redémarrage requis)** n’est pas cochée.  

     Jane conserve ces paramètres par défaut. Associées à cette configuration, ces deux options permettent d'installer toutes les définitions de mises à jour logicielles pour Endpoint Protection dans le segment de recouvrement pendant la journée, sans attendre leur installation et leur validation au cours de la fenêtre de maintenance. Cette configuration respecte mieux la stratégie de sécurité de l'entreprise en ce qui concerne l'exécution par les ordinateurs d'une protection actualisée contre les programmes malveillants.  

    > [!NOTE]  
    >  Contrairement aux installations logicielles des applications, les définitions de mises à jour logicielles pour Endpoint Protection peuvent se produire très fréquemment, voire même plusieurs fois par jour. Il s'agit souvent de petits fichiers. Pour ces types de déploiements liés à la sécurité, il s'avère souvent bénéfique de toujours procéder à l'installation dans le segment de recouvrement plutôt que d'attendre la fenêtre de maintenance. Le client Configuration Manager réinstalle rapidement les mises à jour de définitions logicielles si le l’appareil redémarre, car cette action lance un contrôle d’évaluation sans attendre la prochaine évaluation planifiée.  

     Jane sélectionne le regroupement d’appareils Windows Embedded pour la règle de déploiement automatique.  

     Pour plus d'informations, voir  
                  Étape 3 : configurer les mises à jour logicielles de Configuration Manager pour fournir des mises à jour de définitions aux ordinateurs clients dans [Configuration d’Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md)  

10. Jane décide de configurer une tâche de maintenance qui valide régulièrement toutes les modifications apportées au segment de recouvrement. Cette tâche consiste à prendre en charge le déploiement des définitions de mises à jour logicielles, afin de réduire le nombre de mises à jour qui s'accumulent et doivent être à nouveau installées, chaque fois que l’appareil redémarre. Elle sait, par expérience, que cela permet aux logiciels anti-programmes malveillants de s'exécuter plus efficacement.  

    > [!NOTE]  
    >  Ces définitions de mises à jour logicielles seraient automatiquement validées dans l'image si les appareils embarqués exécutaient une autre tâche de gestion prenant en charge la validation des modifications. Par exemple, l'installation d'une nouvelle version du logiciel de présentation interactive permettrait également de valider les modifications pour les définitions de mises à jour logicielles. Ou bien, l'installation mensuelle de mises à jour logicielles standard au cours de la fenêtre de maintenance permettrait également de valider les modifications pour les définitions de mises à jour logicielles. En revanche, dans ce scénario, où les mises à jour logicielles standard ne s'exécutent pas et le logiciel de présentation interactive a peu de chances d'être souvent mis à jour, des mois peuvent passer avant que les mises à jour de définitions logicielles ne soient automatiquement validées dans l'image.  

     Jane crée d'abord une séquence de tâches personnalisée sans autre paramètre que le nom. Elle exécute l'Assistant Création d'une séquence de tâches :  

    1.  Sur la page **Créer une séquence de tâches** , sélectionnez **Créez une séquence de tâches personnalisée**, puis cliquez sur **Suivant**.  

    2.  Sur la page **Informations sur la séquence de tâches** , elle entre **Maintenance task to commit changes on embedded devices** pour le nom de la séquence de tâches, puis clique sur **Suivant**.  

    3.  Sur la page **Résumé** , elle sélectionne **Suivant**et termine l'Assistant.  

     Jane déploie ensuite cette séquence de tâches personnalisée sur le regroupement d’appareils Windows Embedded, puis elle configure la planification pour une exécution mensuelle. Dans le cadre des paramètres de déploiement, elle active la case à cocher **Valider les changements à l'échéance ou pendant une fenêtre de maintenance (redémarrage requis)** pour conserver les modifications après un redémarrage. Pour configurer ce déploiement, elle sélectionne la séquence de tâches personnalisée qu'elle vient de créer, puis sous l'onglet **Accueil** , dans le groupe **Déploiement** , elle clique sur **Déployer** pour démarrer l'Assistant Déploiement logiciel :  

    1.  Sur la page **Général** , elle sélectionne le regroupement d’appareils Windows Embedded, puis elle clique sur **Suivant**.  

    2.  Sur la page **Paramètres de déploiement** , elle sélectionne **Obligatoire** pour l'option **Objet**, puis elle clique sur **Suivant**.  

    3.  Sur la page **Planification** , elle clique sur **Nouveau** pour spécifier une planification hebdomadaire au cours de la fenêtre de maintenance, puis elle clique sur **Suivant**.  

    4.  Elle termine l'Assistant sans apporter d'autres modifications.  

     Pour plus d'informations, voir  
                  [Gérer les séquences de tâches pour automatiser des tâches dans System Center Configuration Manager](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Pour que les bornes fonctionnent automatiquement, Jane écrit un script permettant de configurer les appareils comme suit :  

    -   Ouverture de session automatique via un compte invité sans mot de passe.  

    -   Exécution automatique du logiciel de présentation interactive au démarrage.  

     Jane utilise des packages et des programmes pour déployer ce script sur le regroupement d’appareils Windows Embedded. Lors de l'exécution de l'Assistant Déploiement logiciel, elle active là encore la case à cocher **Valider les changements à l'échéance ou pendant une fenêtre de maintenance (redémarrage requis)** pour conserver les modifications après un redémarrage.  

     Pour plus d’informations, consultez [Packages et programmes dans System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

12. Le matin suivant, Jane contrôle les appareils Windows Embedded. Elle vérifie les éléments suivants :  

    -   La borne a ouvert automatiquement une session en utilisant le compte invité.  

    -   Le logiciel de présentation interactive est en cours d'exécution.  

    -   Le client Endpoint Protection est installé et dispose des dernières définitions de mises à jour logicielles.  

    -   L’appareil a bien redémarré au cours de la fenêtre de maintenance.  

     Pour plus d'informations, voir :  

    -   [Guide pratique pour surveiller Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    -   [Surveiller des applications avec System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console)  

13. Jane surveille les bornes et indique à son responsable que ces bornes sont correctement gérées. Ainsi, le centre d'accueil passe une commande de 20 bornes.  

     Pour éviter de devoir installer manuellement le client Configuration Manager, ce qui nécessiterait de désactiver et d’activer manuellement les filtres d’écriture, Jane s’assure que la commande comprend une image personnalisée qui intègre déjà l’installation et l’affectation de site du client Configuration Manager. En outre, les noms des appareils sont attribués conformément au format choisi par la société.  

     Les bornes sont livrées au centre d'accueil une semaine après son ouverture. Pendant ce laps de temps, les bornes sont connectées au réseau. Toutes les opérations de gestion des appareils sont automatisées et aucun administrateur n'est requis localement. Jane vérifie que les bornes fonctionnent comme prévu :  

    -   Les clients installés sur les bornes réalisent une attribution de site et téléchargent la clé racine approuvée auprès des services de domaine Active Directory.  

    -   Les clients installés sur les bornes sont ajoutés automatiquement au regroupement d’appareils Windows Embedded et leur fenêtre de maintenance est configurée.  

    -   Le client Endpoint Protection est installé et dispose des dernières définitions de mises à jour logicielles, pour la protection contre les programmes malveillants.  

    -   Le logiciel de présentation interactive est installé et s'exécute automatiquement. Il est entièrement prêt à l'emploi pour les visiteurs.  

14. Au terme de cette configuration initiale, les redémarrages éventuellement nécessaires pour l'installation des mises à jour ont lieu seulement lorsque le centre d'accueil est fermé au public.  
