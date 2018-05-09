---
title: Alertes et système d’état
titleSuffix: Configuration Manager
description: Configurez des alertes et utilisez le système d’état pour rester informé de l’état de votre déploiement de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 891366f7e5fa3f4fd2b8f9a8606e823f0a48c394
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="use-alerts-and-the-status-system-for-system-center-configuration-manager"></a>Utiliser des alertes et le système d’état pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configurez des alertes et utilisez le système d’état intégré pour rester informé de l’état de votre déploiement de System Center Configuration Manager.  


##  <a name="bkmk_Status"></a> Système d’état  
 Tous les composants de site principaux génèrent des messages d’état qui fournissent des commentaires sur les opérations de site et de hiérarchie.    Cette information peut vous tenir informé de l’intégrité des différents processus de site. Vous pouvez régler le système d’alerte pour ignorer le bruit concernant les problèmes connus tout en permettant une visibilité anticipée d’autres problèmes susceptibles de nécessiter votre attention.  

 Par défaut, le système d’état de Configuration Manager fonctionne sans configuration en utilisant les paramètres qui conviennent à la plupart des environnements. Toutefois, vous pouvez configurer les éléments suivants :  

-   **Outils de synthèse d’état :** vous pouvez modifier les outils de synthèse d’état sur chaque site pour contrôler la fréquence des messages d’état qui génèrent un changement d’indicateur d’état pour les quatre outils de synthèse suivants :  

    -   Outil de synthèse du déploiement d'application  

    -   Outil de synthèse des statistiques d'application  

    -   Outil de synthèse d'état des composants  

    -   Outil de synthèse d'état du système de site  

-   **Règles de filtre d’état :** vous pouvez créer des règles de filtre d’état, modifier la priorité des règles, activer ou désactiver des règles, ainsi que supprimer des règles non utilisées sur chaque site.  

    > [!NOTE]  
    >  Les règles de filtre d'état ne prennent pas en charge l'utilisation de variables d'environnement pour exécuter des commandes externes.  

-   **Rapport d’état :** vous pouvez configurer le rapport des composants client et serveur pour modifier la façon dont les messages d’état sont signalées dans un rapport au système d’état de Configuration Manager et spécifier où les messages d’état sont envoyés.  

    > [!WARNING]  
    >  Étant donné que les paramètres de rapport par défaut conviennent à la plupart des environnements, ils doivent être modifiés avec précaution. Lorsque vous augmentez le niveau du rapport d'état en choisissant de rapporter tous les détails d'état, vous pouvez augmenter la quantité de messages d'état à traiter, ce qui accroît la charge de traitement sur le site Configuration Manager. À l'inverse, une diminution du niveau du rapport d'état peut limiter l'utilité des outils de synthèse d'état.  

Étant donné que le système d’état tient à jour des configurations distinctes pour chaque site, vous devez modifier chaque site individuellement.  

###  <a name="bkmk_configstatus"></a> Procédures de configuration du système d’état  

##### <a name="to-configure-status-summarizers"></a>Pour configurer des outils de synthèse d'état  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** >**Sites**, puis sélectionnez le site dont vous voulez configurer le système d’état.  

2.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Outils de synthèse d'état**.  

3.  Dans la boîte de dialogue **Outils de synthèse d'état** , sélectionnez l'outil de synthèse d'état que vous souhaitez configurer, puis cliquez sur **Modifier** pour ouvrir les propriétés de cet outil de synthèse. Si vous modifiez l'outil de synthèse du déploiement d'application ou des statistiques d'application, passez à l'étape 5. Si vous modifiez l'outil de synthèse d'état des composants, passez à l'étape 6. Si vous modifiez l'outil de synthèse d'état du système de site, passez à l'étape 7.  

4.  Utilisez les étapes suivantes après avoir ouvert la page de propriétés de l'outil de synthèse du déploiement d'application ou l'outil de synthèse des statistiques d'application :  

    1.  Dans l'onglet **Général** de la page de propriétés des outils de synthèse, configurez les intervalles de synthèse, puis cliquez sur **OK** pour fermer la page de propriétés.  

    2.  Cliquez sur **OK** pour fermer la boîte de dialogue **Outils de synthèse d'état** et terminez cette procédure.  

5.  Utilisez les étapes suivantes après avoir ouvert la page de propriétés de l'outil de synthèse d'état des composants :  

    1.  Dans l'onglet **Général** de la page de propriétés des outils de synthèse, configurez les valeurs de réplication et de période seuil.  

    2.  Dans l'onglet **Seuils** , sélectionnez le **Type de Message** que vous souhaitez configurer, puis cliquez sur le nom d'un composant dans la liste **Seuils** .  

    3.  Dans la boîte de dialogue **Propriétés du seuil de l'état** , modifiez les valeurs de seuil d'avertissement et critique, puis cliquez sur **OK**.  

    4.  Répétez les étapes 6.b et 6.c au besoin et, lorsque vous avez terminé, cliquez sur **OK** pour fermer les propriétés de l'outil de synthèse.  

    5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Outils de synthèse d'état** et terminez cette procédure.  

6.  Utilisez les étapes suivantes après avoir ouvert les pages des propriétés de l'outil de synthèse d'état du système de site :  

    1.  Dans l'onglet **Général** de la page de propriétés des outils de synthèse, configurez les valeurs de réplication et de planification.  

    2.  Dans l'onglet **Seuils** , spécifiez des valeurs pour les **Seuils par défaut** afin de configurer des seuils par défaut pour les affichages d'état critique et d'avertissement.  

    3.  Pour modifier les valeurs des **Objets de stockage**spécifiques, cliquez sur l'objet dans la liste **Seuils spécifiques** et cliquez sur le bouton **Propriétés** pour pouvoir accéder et modifier les seuils critique et d'avertissement des objets de stockage. Cliquez sur **OK** pour fermer les propriétés des objets de stockage.  

    4.  Pour créer un nouvel objet de stockage, cliquez sur le bouton **Créer un objet** et spécifiez les valeurs des objets de stockage. Cliquez sur **OK** pour fermer les propriétés de l'objet.  

    5.  Pour supprimer un objet de stockage, sélectionnez l'objet, puis cliquez sur le bouton **Supprimer** .  

    6.  Répétez les étapes 7.b à 7.e si besoin. Lorsque vous avez terminé, cliquez sur **OK** pour fermer les propriétés de l'outil de synthèse.  

    7.  Cliquez sur **OK** pour fermer la boîte de dialogue **Outils de synthèse d'état** et terminez cette procédure.  

##### <a name="to-create-a-status-filter-rule"></a>Pour créer une règle de filtre d'état  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** >**Sites**, puis sélectionnez le site pour lequel vous voulez configurer le système d’état.  

2.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Règles de filtre d'état**. La boîte de dialogue **Règles de filtre d'état** s'ouvre.  

3.  Cliquez sur **Créer**.  

4.  Sur la page **Général**de l' **Assistant Création de règle de filtre d'état** , spécifiez un nom pour la nouvelle règle de filtre d'état et un critère de correspondance des messages pour la règle, puis cliquez sur **Suivant**.  

5.  Sur la page **Actions** , spécifiez les actions à entreprendre lorsqu'un message d'état correspond à la règle de filtre, puis cliquez sur **Suivant**.  

6.  Sur la page **Résumé** , consultez les détails de la nouvelle règle, puis terminez l'Assistant.  

    > [!NOTE]  
    >  Configuration Manager exige uniquement que la nouvelle règle de filtre d'état ait un nom. Si la règle est créée, mais que vous ne spécifiez pas de critère pour traiter les messages d'état, la règle de filtre d'état n'aura aucun effet. Cela vous permet de créer et d'organiser des règles avant de configurer les critères de filtre d'état pour chaque règle.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>Pour modifier ou supprimer une règle de filtre d'état  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** >**Sites**, puis sélectionnez le site pour lequel vous voulez configurer le système d’état.  

2.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Règles de filtre d'état**.  

3.  Dans la boîte de dialogue **Règles de filtre d'état** , sélectionnez la règle que vous souhaitez modifier puis effectuez l'une des actions suivantes :  

    -   Cliquez sur **Augmenter la priorité** ou **Diminuer la priorité** pour modifier l'ordre de traitement de la règle de filtre d'état. Puis sélectionnez une autre action ou passez à l'étape 8 de cette procédure pour terminer cette tâche.  

    -   Cliquez sur **Désactiver** ou **Activer** pour modifier l'état de la règle. Après avoir modifié l'état de la règle, sélectionnez une autre action ou passez à l'étape 8 de cette procédure pour terminer cette tâche.  

    -   Cliquez sur **Supprimer** si vous souhaitez supprimer la règle de filtre d'état de ce site, puis cliquez sur **Oui** pour confirmer l'action. Après avoir supprimé une règle, sélectionnez une autre action ou passez à l'étape 8 de cette procédure pour terminer cette tâche.  

    -   Cliquez sur **Modifier** si vous souhaitez modifier les critères de la règle de message d'état et passez à l'étape 5 de cette procédure.  

4.  Sur l'onglet **Général** de la boîte de dialogue Propriétés de la règle de filtre d'état, modifiez la règle et les critères de correspondance des messages.  

5.  Cliquez sur l'onglet **Actions** , modifiez les actions à entreprendre lorsqu'un message d'état correspond à la règle de filtre.  

6.  Cliquez sur **OK** pour enregistrer les modifications.  

7.  Cliquez sur **OK** pour fermer la boîte de dialogue **Règles de filtre d'état** .  

##### <a name="to-configure-status-reporting"></a>Pour configurer un rapport d'état  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**, puis sélectionnez le site pour lequel vous voulez configurer le système d’état.  

2.  Dans l'onglet **Accueil** , dans le groupe **Paramètres** , cliquez sur **Configurer les composants de site**, puis sélectionnez **Rapport d'état**.  

3.  Dans la boîte de dialogue **Propriétés du composant de rapport d'état** , spécifiez les messages d'état de composant serveur et client que vous souhaitez signaler ou journaliser :  

    1.  Configurez **Rapport** pour envoyer des messages d'état au système de messages d'état de Configuration Manager.  

    2.  Configurez **Journal** pour écrire le type et la gravité des messages d'état dans le journal des événements Windows.  

4.  Cliquez sur **OK**.  

###  <a name="BKMK_MonitorSystemStatus"></a> Surveiller l’état du système de Configuration Manager  
 L’**état du système** dans Configuration Manager fournit une vue d’ensemble des opérations générales de sites et des opérations de serveur de site de votre hiérarchie. Il peut révéler des problèmes de fonctionnement des serveurs de système de site ou des composants, et vous pouvez utiliser l'état du système pour consulter des détails spécifiques pour différentes opérations de Configuration Manager. Vous surveillez l'état du système à partir du nœud **État du système** de l'espace de travail **Surveillance** dans la console Configuration Manager.  

 La plupart des composants et rôles de système de site Configuration Manager génèrent des messages d'état. Les détails des messages d'état sont consignés dans chaque journal opérationnel des composants, mais ils sont également soumis à la base de données de site lorsqu'ils sont résumés et présentés dans un cumul général de l'intégrité de chaque composant ou des systèmes de site. Ces cumuls de messages d'état fournissent des informations détaillées pour les opérations et avertissements réguliers ainsi que pour les détails de l'erreur. Vous pouvez configurer les seuils auxquels les avertissements ou les erreurs sont déclenchés et ajuster le système afin de vous assurer que les informations relatives au cumul ignorent les problèmes connus qui ne vous concernent pas tout en attirant votre attention sur les problèmes réels des serveurs ou sur les opérations liées aux composants que vous souhaitez peut-être examiner.  

 L'état du système est répliqué vers d'autres sites dans une hiérarchie en tant que données de site, pas en tant que données globales. Cela signifie que vous ne pouvez voir que l'état du site auquel votre console Configuration Manager se connecte, et les sites enfants de ce site. Ainsi, envisagez de connecter votre console Configuration Manager sur le site de niveau supérieur de votre hiérarchie lorsque vous affichez l'état du système.  

 Utilisez le tableau suivant pour identifier les différents affichages de l'état du système et les situations dans lesquelles les utiliser.  

|Nœud|Plus d'informations|  
|----------|----------------------|  
|État du site|Ce nœud permet d'afficher une synthèse de l'état de chaque système de site pour consulter l'intégrité de chaque serveur de système de site. L'intégrité d'un système de site est déterminée par des seuils que vous configurez pour chaque site dans l' **Outil de synthèse d'état du système de site**.<br /><br /> Vous pouvez afficher les messages d'état de chaque système de site, définir des seuils pour les messages d'état et gérer le fonctionnement des composants sur des systèmes de site à l'aide du **Gestionnaire de service de Configuration Manager**.|  
|État du composant|Utilisez ce nœud pour afficher une synthèse de l'état de chaque composant de Configuration Manager pour vérifier son bon fonctionnement. L'intégrité d'un composant est déterminée par les seuils que vous configurez pour chaque site dans l' **Outil de synthèse d'état des composants**.<br /><br /> Vous pouvez afficher les messages d'état pour chaque composant, définir des seuils pour les messages d'état et gérer le fonctionnement des composants à l'aide du **Gestionnaire de service de Configuration Manager**.|  
|Enregistrements en conflit|Utilisez ce nœud pour afficher les messages d'état de clients qui peuvent présenter des conflits de rapports.<br /><br /> Configuration Manager utilise l'ID du matériel pour tenter d'identifier les éventuels clients dupliqués et vous signale les enregistrements en conflit. Par exemple, si vous devez réinstaller un ordinateur, il est possible que l'ID du matériel soit le même, mais que le GUID utilisé par Configuration Manager soit différent.|  
|Requêtes sur les messages d'état|Utilisez ce nœud pour demander des messages d'état d'événements spécifiques ou des informations liées. Vous pouvez utiliser les requêtes de messages d'état pour trouver des messages d'état liés à des événements spécifiques.<br /><br /> Il est possible d'utiliser fréquemment des requêtes de messages d'état pour identifier quand un composant, une opération ou un objet Configuration Manager spécifique a été modifié ainsi que le compte utilisé pour effectuer cette modification. Par exemple, vous pouvez exécuter la requête intégrée pour les **Regroupements créés, modifiés ou supprimés** afin d'identifier quand un regroupement a été créé et le compte utilisateur utilisé pour créer ce regroupement.|  

####  <a name="bkmk_managestatus"></a> Gérer l’état du site et l’état des composants  
 Utilisez les informations suivantes pour gérer l'état du site et l'état du composant :  

-   Pour configurer des seuils pour le système d'état, voir [Procédures de configuration du système d’état](#bkmk_configstatus).  

-   Pour gérer les composants individuels dans Configuration Manager, utilisez le **Gestionnaire de service de Configuration Manager**.  

####  <a name="bkmk_view"></a> Afficher les messages d’état  
 Vous pouvez afficher les messages d'état des serveurs de système de site et des composants individuels.  

 Pour consulter des messages d'état dans la console Configuration Manager, sélectionnez un serveur de système de site ou un composant spécifique, puis cliquez sur **Afficher les messages**. Lorsque vous consultez des messages, vous pouvez choisir d'afficher des types de message spécifiques ou des messages d'une période indiquée. Vous pouvez également filtrer les résultats en fonction des détails du message d'état.  

##  <a name="bkmk_Alerts"></a> Alertes  
 Les alertes Configuration Manager sont générées par certaines opérations quand une condition spécifique se produit.  

-   Les alertes sont habituellement générées quand une erreur que vous devez résoudre se produit  

-   Les alertes peuvent être générées pour vous avertir qu’une condition a été détectée afin que vous puissiez continuer à surveiller la situation.  

-   Certaines alertes que vous configurez, telles que les alertes concernant l’état de Endpoint Protection et du client, tandis que les autres alertes sont configurées automatiquement  

-   Vous pouvez configurer des abonnements aux alertes qui peuvent ensuite envoyer des détails par courrier électronique, ce qui permet une plus grande sensibilisation aux problèmes clés  

 Utilisez le tableau suivant pour rechercher des informations sur la façon de configurer des alertes et des abonnements aux alertes dans Configuration Manager :  


|Action|Informations complémentaires|  
|------------|----------------------|  
|Configurer des alertes Endpoint Protection pour un regroupement|Voir **Comment configurer des alertes pour Endpoint Protection dans Configuration Manager** dans [Configuration de Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/configure-endpoint-protection.md).|  
|Configurer des alertes d’état du client pour un regroupement|Voir [Guide pratique pour configurer l’état du client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).|  
|Gérer les alertes Configuration Manager|Consultez la section [Management tasks for alerts](#BKMK_Manage) de cette rubrique.|  
|Configurer les abonnements par courrier électronique aux alertes|Consultez la section [Management tasks for alerts](#BKMK_Manage) de cette rubrique.|  
|Surveiller les alertes|Consultez la section [Surveiller les alertes](#BKMK_MonitorAlerts)|  

###  <a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>Pour gérer les alertes générales  

1.  Dans la console Configuration Manager, accédez à **Surveillance** > **Alertes**, puis sélectionnez une tâche de gestion.  

  Utilisez le tableau suivant pour obtenir plus d'informations sur les tâches de gestion qui pourraient nécessiter certaines informations avant de les sélectionner.  

|Tâche de gestion|Détails|  
    |---------------------|-------------|  
    |**Configurer**|Ouvre la boîte de dialogue *Propriétés de* **&lt;nom de l’alerte\>** où vous pouvez modifier le nom, la gravité et les seuils de l’alerte sélectionnée. Si vous modifiez la gravité de l’alerte, cette configuration affecte la façon dont les alertes sont affichées dans la console Configuration Manager.|  
    |**Modifier les commentaires**|Entrez un commentaire pour les alertes sélectionnées. Ces commentaires s’affichent avec l’alerte dans la console Configuration Manager.|  
    |**Reporter**|Suspend la surveillance de l’alerte jusqu’à la date spécifiée. À ce moment-là, l’état de l’alerte est mis à jour.<br /><br /> Vous pouvez reporter une alerte uniquement quand celle-ci est active.|  
    |**Créer un abonnement**|Ouvre la boîte de dialogue **Nouvel abonnement** où vous pouvez créer un abonnement par courrier électronique à l’alerte sélectionnée.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>Pour configurer des alertes d’état du client pour un regroupement  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** >   **Regroupements d’appareils**.  

2.  Dans la liste **Regroupements de périphériques** , sélectionnez le regroupement pour lequel vous souhaitez configurer des alertes, puis cliquez sur **Propriétés** dans l'onglet **Accueil** , du groupe **Propriétés**.  

    > [!NOTE]  
    >  Vous ne pouvez pas configurer d'alertes pour les regroupements d'utilisateurs.  

3.  Sous l'onglet **Alertes** de la boîte de dialogue **Propriétés de** *&lt;Nom du regroupement*\>, cliquez sur **Ajouter**.  

    > [!NOTE]  
    >  L'onglet **Alertes** n'est visible que si le rôle de sécurité auquel vous êtes associé dispose d'autorisations pour les alertes.  

4.  Dans la boîte de dialogue **Ajouter de nouvelles alertes de regroupement** , choisissez les alertes que vous souhaitez générer lorsque les seuils d'état du client passent sous une valeur spécifique, puis cliquez sur **OK**.  

5.  Dans la liste **Conditions** de l'onglet **Alertes** , sélectionnez chaque alerte relative à l'état du client, puis spécifiez les informations suivantes.  

    -   **Nom d’alerte** – Acceptez le nom par défaut ou entrez un nouveau nom pour l’alerte.  

    -   **Gravité d’alerte** – Dans la liste déroulante, choisissez la gravité d’alerte qui sera affichée dans la console Configuration Manager.  

    -   **Déclencher l'alerte** : spécifiez le pourcentage seuil pour l'alerte.  

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de** *&lt;Nom du regroupement*\>.  

##### <a name="to-configure-email-notification-for-alerts"></a>Pour configurer une notification par courrier électronique pour les alertes  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Alertes**  > **Inscriptions**.  

2.  Sous l'onglet **Accueil** , du groupe **Créer** , cliquez sur **Configurer la notification par courrier électronique**.  

3.  Dans la boîte de dialogue **Propriétés du composant de notification de courrier électronique** , définissez ce qui suit :  

    -   **Activer les notifications par courrier électronique pour les alertes** : cochez cette case pour permettre à Configuration Manager d’utiliser un serveur SMTP pour envoyer des alertes par e-mail.  

    -   **Nom de domaine complet ou adresse IP du serveur SMTP pour envoyer des alertes par courrier électronique**: entrez le nom de domaine complet (FQDN) ou l’adresse IP et le port SMTP du serveur de messagerie à utiliser pour ces alertes.  

    -   **Compte de connexion au serveur SMTP** : spécifiez la méthode d’authentification que Configuration Manager doit utiliser pour se connecter au serveur de messagerie.  

    -   **Adresse de l’expéditeur pour les alertes de courrier électronique**: spécifiez l’adresse électronique à partir de laquelle les courriers électroniques d’alerte sont envoyés.  

    -   **Tester le serveur SMTP**: envoie un courrier électronique de test à l’adresse électronique spécifiée dans **Adresse de l’expéditeur pour les alertes de courrier électronique**.  

4.  Cliquez sur **OK** pour enregistrer les paramètres et fermer la boîte de dialogue des **Propriétés du composant de notification de courrier électronique** .  

##### <a name="to-subscribe-to-email-alerts"></a>Pour vous abonner aux alertes par courrier électronique  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Alertes** .  

2.  Sélectionnez une alerte, puis sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Créer un abonnement**.  

3.  Dans la boîte de dialogue **Nouvel abonnement** , spécifiez les éléments suivants :  

    -   **Nom**: entrez le nom permettant d’identifier l’abonnement par courrier électronique. Vous pouvez entrer jusqu'à 255 caractères.  

    -   **Adresse de messagerie**: entrez les adresses de messagerie de destination de l’alerte. Vous pouvez séparer plusieurs adresses de messagerie par un point-virgule.  

    -   **Langue de messagerie**: dans la liste, spécifiez la langue du courrier électronique.  

4.  Cliquez sur **OK** pour fermer la boîte de dialogue **Nouvel abonnement** et créer l'abonnement par courrier électronique.  

    > [!NOTE]  
    >  Vous pouvez supprimer et modifier les abonnements dans l'espace de travail **Surveillance** lorsque vous développez le nœud **Alertes** , puis cliquez sur le nœud **Abonnements** .  

###  <a name="BKMK_MonitorAlerts"></a> Surveiller les alertes  
 Vous pouvez consulter les alertes dans le nœud **Alertes** de l'espace de travail **Surveillance** . Les alertes présentent l'un des états d'alerte suivants :  

-   **Jamais déclenché**: la condition de l’alerte n’a pas été remplie.  

-   **Actif**: la condition de l’alerte est remplie.  

-   **Annulé**: la condition d’une alerte active n’est plus remplie. Cet état indique que la condition qui a entraîné l'alerte est maintenant résolue.  

-   **Reporté à plus tard** : un utilisateur administratif a configuré Configuration Manager pour évaluer l’état de l’alerte ultérieurement.  

-   **Désactivé**: l’alerte a été désactivée par un utilisateur administratif. Lorsqu'une alerte présente cet état, Configuration Manager ne la met pas à jour même si l'état de l'alerte change.  

 Vous pouvez effectuer l'une des actions suivantes lorsque Configuration Manager génère une alerte :  

-   Corrigez la condition qui a généré l'alerte, par exemple, corrigez un problème réseau ou un problème de configuration qui a généré l'alerte. Une fois que Configuration Manager a détecté que le problème n'existe plus, l'état de l'alerte passe à **Annuler**.  

-   Si l'alerte est un problème connu, vous pouvez reporter l'alerte pendant une durée spécifique. À ce moment, Configuration Manager met à jour l'alerte à son état actuel.  

     Vous pouvez reporter une alerte uniquement lorsque celle-ci est active.  

-   Vous pouvez modifier le **Commentaire** d'une alerte afin d'informer les autres utilisateurs administratifs que cette alerte est surveillée. Par exemple, dans le commentaire, vous pouvez identifier comment résoudre la condition, fournir des informations sur l'état actuel de la condition ou expliquer la raison du report de l'alerte.  
