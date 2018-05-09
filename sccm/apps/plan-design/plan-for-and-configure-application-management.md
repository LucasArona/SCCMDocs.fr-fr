---
title: Planifier et configurer la gestion des applications
titleSuffix: Configuration Manager
description: Implémentez et configurez les dépendances nécessaires au déploiement d’applications dans System Center Configuration Manager.
ms.date: 11/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18d9fe80a1c5525457579dadbfeaeafa3425202d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-for-and-configure-application-management-in-system-center-configuration-manager"></a>Planifier et configurer la gestion des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cette article pour savoir comment implémenter les dépendances nécessaires au déploiement d’applications dans System Center Configuration Manager.  

## <a name="dependencies-external-to-configuration-manager"></a>Dépendances externes à Configuration Manager  

|Dépendance|Plus d'informations|  
|------------------|----------------------|  
|Internet Information Services (IIS) est nécessaire sur les serveurs de système de site qui exécutent le point du site web du catalogue des applications, le point de service web du catalogue des applications, le point de gestion et le point de distribution.|Pour plus d’informations sur cette condition, consultez [Configurations prises en charge](../../core/plan-design/configs/supported-configurations.md).|  
|Appareils mobiles inscrits par Configuration Manager|Quand vous signez le code des applications à déployer sur des appareils mobiles, n’utilisez pas de certificat généré par un modèle Version 3 (**Windows Server 2008, Enterprise Edition**). Ce modèle de certificat crée un certificat qui est compatible avec les applications Configuration Manager pour appareils mobiles.<br /><br /> Si vous utilisez les services de certificat Active Directory pour signer le code des applications pour les applications d’appareils mobiles, n’utilisez pas de modèle de certificat Version 3.|  
|Les clients doivent être configurés pour auditer les événements de connexion si vous voulez créer automatiquement des affinités entre les utilisateurs et les appareils.|Le client Configuration Manager lit les événements d’ouverture de session de type **Opération réussie** du journal des événements de sécurité des PC afin de déterminer les affinités automatiques entre les utilisateurs et les appareils.  Ces événements sont activés par les deux stratégies d’audit suivantes :<br>**Auditer les événements d'ouverture de session de compte**<br>**Auditer les événements d'ouverture de session**<br>Pour créer automatiquement des relations entre utilisateurs et appareils, vérifiez que ces deux paramètres sont activés sur les ordinateurs clients. Vous pouvez utiliser la stratégie de groupe Windows pour configurer ces paramètres.|  

## <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager   

|Dépendance|Plus d'informations|  
|------------------|----------------------|  
|Point de gestion|Les clients contactent un point de gestion pour télécharger la stratégie client, localiser du contenu et se connecter au catalogue des applications.<br /><br /> Si les clients ne peuvent pas accéder à un point de gestion, ils ne peuvent pas utiliser le catalogue d'applications.|  
|Point de distribution|Pour que les applications puissent être déployées sur les clients, la hiérarchie doit contenir au moins un point de distribution. Par défaut, le serveur de site possède un rôle de système de site du point de distribution activé au cours d'une installation standard. Le nombre et l'emplacement des points de distribution dépendent des exigences propres à votre entreprise.<br /><br /> Pour plus d’informations sur l’installation de points de distribution et sur la gestion de contenu, consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Paramètres du client|De nombreux paramètres client contrôlent la manière dont les applications sont installées sur le client, ainsi que l’expérience utilisateur offerte par ce dernier. En voici quelques-uns :<br /><br /><ul><li>Agent ordinateur</li><li>Redémarrage de l’ordinateur</li><li>Déploiement logiciel</li><li>Affinité entre utilisateur et appareil</li></ul> Pour plus d’informations sur ces paramètres client, consultez [À propos des paramètres client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Pour plus d’informations sur la configuration des paramètres client, consultez [Guide pratique pour configurer les paramètres client dans Configuration Manager](../../core/clients/deploy/configure-client-settings.md).|  
|Comptes d’utilisateur découverts pour le catalogue d’applications |Configuration Manager doit d’abord détecter les comptes d’utilisateur avant que les utilisateurs puissent afficher et demander des applications du catalogue des applications. Pour plus d’informations, consultez [Exécuter la découverte](/sccm/core/servers/deploy/configure/run-discovery).|  
|Client App-V 4.6 SP1 ou version supérieure, pour l'exécution des applications virtuelles|Pour créer des applications virtuelles dans Configuration Manager, les ordinateurs clients doivent disposer du client App-V 4.6 SP1 ou ultérieur.<br /><br /> Vous devez également mettre à jour le client App-V avec le correctif décrit dans l’[article 2645225 de la Base de connaissances](http://go.microsoft.com/fwlink/p/?LinkId=237322) avant de pouvoir déployer des applications virtuelles.|  
|Point de service web du catalogue des applications|Le point de service web du catalogue des applications est un rôle de système de site qui fournit au site web du catalogue des applications des informations sur les logiciels disponibles auprès de la bibliothèque de logiciels.<br /><br /> Pour plus d’informations sur la configuration de ce rôle de système de site, consultez [Configurer le Centre logiciel et le catalogue des applications (PC Windows uniquement)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) dans cet article.|  
|Point du site web du catalogue des applications|Le point du site web du catalogue des applications est un rôle de système de site fournissant aux utilisateurs une liste des logiciels disponibles.<br /><br /> Pour plus d’informations sur la configuration de ce rôle de système de site, consultez [Configurer le Centre logiciel et le catalogue des applications (PC Windows uniquement)](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only) dans cet article.|  
|Point de Reporting Services|Pour utiliser les rapports dans Configuration Manager pour la gestion d’applications, vous devez d’abord installer et configurer un point de Reporting Services.<br /><br /> Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).|  
|Autorisations de sécurité pour la gestion d'applications|Vous devez disposer des autorisations de sécurité suivantes pour pouvoir gérer des applications :<br /><br /> Le rôle de sécurité **Auteur d’application** inclut les autorisations mentionnées ci-dessus, qui sont nécessaires pour créer, modifier et mettre hors service des applications dans Configuration Manager.<br /><br /> **Pour déployer des applications :**<br /><br /> Le rôle de sécurité **Gestionnaire de déploiement d’application** intègre les autorisations mentionnées ci-dessus, qui sont nécessaires au déploiement d’applications dans Configuration Manager.<br /><br /> Le rôle de sécurité **Administrateur d’application** a toutes les autorisations des rôles de sécurité **Auteur d’application** et **Gestionnaire de déploiement d’application**.<br /><br /> Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles](../../core/servers/deploy/configure/configure-role-based-administration.md).|  

##  <a name="configure-software-center-and-the-application-catalog-windows-pcs-only"></a>Configurer le Centre logiciel et le catalogue des applications (PC Windows uniquement)  

 Dans System Center Configuration Manager, les utilisateurs ont maintenant deux options pour changer les paramètres, et pour rechercher et installer des applications :  

-   **Le nouveau Centre logiciel** : le nouveau Centre logiciel a été modernisé. Les applications qui seraient apparues uniquement dans le catalogue des applications dépendant de Silverlight (applications accessibles à l’utilisateur) apparaissent maintenant dans le Centre logiciel sous l’onglet **Applications**. Il est toujours possible d’accéder au catalogue des applications via le lien situé sous l’onglet **État de l’installation** du Centre logiciel.  

     Vous pouvez faire en sorte que les clients utilisent le nouveau Centre logiciel en activant le paramètre client **Agent ordinateur** > **Utiliser le nouveau Centre logiciel**.  

    > [!IMPORTANT]  
    >  Même si vous n’avez plus besoin de vous connecter au catalogue des applications, vous devez quand même configurer le point du site web du catalogue des applications et le point de service web du catalogue des applications comme indiqué dans la section suivante.  

-   **Le Centre logiciel précédent et le catalogue des applications** : par défaut, les utilisateurs continuent de se connecter à la précédente version du Centre logiciel et au catalogue des applications (moyennant un navigateur web compatible Silverlight) pour parcourir les applications disponibles.  

 Quelle que soit la version que vous choisissez d’utiliser, le Centre logiciel est installé automatiquement pendant l’installation du client Configuration Manager sur les PC Windows.  

    > [!TIP]  
    >  La version du Centre logiciel auxquels ont accès les utilisateurs varie en fonction des paramètres du client Configuration Manager. Vous pouvez ainsi choisir la version qui est utilisée en fonction des paramètres client personnalisés que vous déployez sur un regroupement. 

    > [!IMPORTANT]
    > Dans les prochains mois, nous allons supprimer la version précédente du Centre logiciel, qui ne sera plus disponible.
    > Vous pouvez faire en sorte que les clients utilisent le nouveau Centre logiciel en activant le paramètre client **Agent ordinateur** > **Utiliser le nouveau Centre logiciel**. 

## <a name="steps-to-install-and-configure-the-application-catalog-and-software-center"></a>Installation et configuration du catalogue des applications et du Centre logiciel  

> [!IMPORTANT]  
>  Avant d’effectuer cette procédure, vérifiez que vous respectez tous les prérequis répertoriés ci-dessus.  

|Étapes|Détails|Plus d'informations|  
|-----------|-------------|----------------------|  
|**Étape 1 :** si vous souhaitez utiliser des connexions HTTPS, assurez-vous d'avoir déployé un certificat de serveur web sur les serveurs de système de site.|Déployez un certificat de serveur web sur les serveurs de système de site qui exécuteront le point de site web du catalogue d'applications et le point de service web du catalogue d'applications.<br /><br /> De plus, si vous voulez que les clients puissent utiliser le catalogue des applications depuis Internet, déployez un certificat de serveur web sur au moins un serveur de système de site du point de gestion et configurez-le pour les connexions client depuis Internet.|Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Étape 2 :** si vous souhaitez utiliser un certificat client PKI pour les connexions à des points de gestion, déployez un certificat d'authentification client sur les ordinateurs clients.|Même si les clients n’utilisent pas un certificat PKI client pour se connecter au catalogue d’applications, ils doivent se connecter à un point de gestion afin d’utiliser le catalogue d’applications. Vous devez déployer un certificat d'authentification client sur les ordinateurs clients dans les cas suivants :<br /><br /><ul><li>Tous les points de gestion sur l'intranet n'acceptent que les connexions client HTTPS.</li><li>Les clients se connecteront au catalogue d'applications depuis Internet.</li></ul>|Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).|  
|**Étape 3 :** installez et configurez le point de service web du catalogue d'applications et le site web du catalogue d'applications.|Vous devez installer les deux rôles de système de site sur le même site. Vous n'êtes pas obligé de les installer sur le même serveur de système de site ni dans la même forêt Active Directory. Cependant, le point de service web du catalogue des applications doit se trouver dans la même forêt que la base de données du site.|Pour plus d’informations sur le positionnement des rôles de système de site, consultez [Planifier des serveurs de système de site et des rôles de système de site](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).<br /><br /> Pour configurer le point de service web du catalogue des applications et le point de site web du catalogue des applications, consultez **Étape 3 : installation et configuration des rôles de système de site du catalogue des applications**.|  
|**Étape 4 :** configurez les paramètres client pour le catalogue des applications et le Centre logiciel.|Configurez les paramètres client par défaut si vous souhaitez que tous les utilisateurs aient le même paramètre. Vous pouvez aussi configurer des paramètres client personnalisés pour des regroupements spécifiques.|Pour plus d’informations sur les paramètres client, consultez [À propos des paramètres client](../../core/clients/deploy/about-client-settings.md).<br /><br /> Pour plus d’informations sur la configuration de ces paramètres client, consultez **Étape 4 : configurer les paramètres client pour le catalogue des applications et le Centre logiciel**.|  
|**Étape 5 :** vérifiez que le catalogue des applications est opérationnel.|Vous pouvez utiliser le catalogue des applications directement à partir d’un navigateur ou du Centre logiciel.|Voir **Étape 5 : vérifier que le catalogue des applications est opérationnel**.|  

## <a name="supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center"></a>Procédures supplémentaires d'installation et de configuration du catalogue des applications et du Centre logiciel  
 Utilisez les informations suivantes lorsque les étapes décrites dans le tableau précédent nécessitent des procédures supplémentaires.  

###  <a name="step-3-install-and-configure-the-application-catalog-site-system-roles"></a>Étape 3 : installation et configuration des rôles de système de site du catalogue des applications  
 Ces procédures configurent les rôles de système de site pour le catalogue d'applications. Selon que vous voulez installer un nouveau serveur de système de site ou utiliser un serveur de système de site existant, choisissez une des deux procédures suivantes :  

> [!NOTE]  
>  Le catalogue d'applications ne peut pas être installé sur un site secondaire ni sur un site d'administration centrale.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-new-site-system-server"></a>Pour installer et configurer les systèmes de site du catalogue d'applications : Nouveau serveur de système de site  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un serveur de système de site**.  

4.  Dans la page **Général**, spécifiez les paramètres généraux du système de site, puis choisissez **Suivant**.  

    > [!TIP]  
    >  Si vous voulez que les ordinateurs clients puissent utiliser le catalogue des applications via Internet, spécifiez le nom de domaine complet Internet.  

5.  Dans la page **Sélection du rôle système**, sélectionnez **Point de service Web du catalogue des applications** et **Point du site Web du catalogue des applications** dans la liste des rôles disponibles, puis choisissez **Suivant**.  

6.  Effectuez les étapes restantes.  

####  <a name="to-install-and-configure-the-application-catalog-site-systems-existing-site-system-server"></a>Pour installer et configurer les systèmes de site du catalogue d'applications : Serveur de système de site existant  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur à utiliser pour le catalogue des applications.  

3.  Sous l’onglet **Accueil**, dans le groupe **Serveur**, choisissez **Ajouter des rôles de système de site**.  

4.  Dans la page **Général**, spécifiez les paramètres généraux du système de site, puis choisissez **Suivant**.  

    > [!TIP]  
    >  Si vous voulez que les ordinateurs clients puissent utiliser le catalogue des applications via Internet, spécifiez le nom de domaine complet Internet.  

5.  Dans la page **Sélection du rôle système**, sélectionnez **Point de service Web du catalogue des applications** et **Point du site Web du catalogue des applications** dans la liste des rôles disponibles, puis choisissez **Suivant**.  

6.  Effectuez les étapes restantes.  

7. Vérifiez l'installation de ces rôles de système de site à l'aide de messages d'état et en examinant les fichiers journaux :  

    Messages d'état : Utiliser les composants **SMS_PORTALWEB_CONTROL_MANAGER** et **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Par exemple, l'ID d'état **1015** pour **SMS_PORTALWEB_CONTROL_MANAGER** confirme que le Gestionnaire de composants de site a correctement installé le point de site web du catalogue d'applications.  

    Fichiers journaux : Rechercher **SMSAWEBSVCSetup.log** et **SMSPORTALWEBSetup.log**.  

    Pour plus d’informations, recherchez les fichiers journaux **awebsvcMSI.log** et **portlwebMSI.log**.  

###  <a name="step-4-configure-the-client-settings-for-the-application-catalog-and-software-center"></a>Étape 4 : configuration des paramètres client pour le catalogue des applications et le Centre logiciel  
 Cette procédure configure les paramètres client par défaut qui s'appliquent au catalogue des applications et au Centre logiciel pour l'ensemble des appareils de la hiérarchie. Si vous voulez que ces paramètres s’appliquent seulement à certains appareils, créez un paramètre client personnalisé et déployez-le sur un regroupement contenant ces appareils. Pour plus d'informations sur la création d'un paramètre d’appareil personnalisé, consultez la section [Comment créer et déployer des paramètres client personnalisés](../../core/clients/deploy/configure-client-settings.md#create-and-deploy-custom-client-settings) dans le la page [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Consultez et configurez les paramètres relatifs aux notifications utilisateur, au catalogue d'applications et au Centre logiciel. Par exemple :  

    1.  Groupe**Agent ordinateur** :  

        -   **Point de site Web du catalogue d'applications par défaut**.  

        -   **Ajouter un site Web du catalogue d'applications par défaut à la zone des sites de confiance d'Internet Explorer**.  

        -   **Nom d'organisation affiché dans le Centre logiciel**.  

            > [!TIP]  
            >  Pour spécifier le nom d’organisation affiché dans le catalogue des applications et configurer le thème du site web, utilisez l’onglet **Personnalisation** des propriétés du site web du catalogue des applications.  

        -   **Utiliser le nouveau Centre logiciel**. Choisissez la valeur **Oui** si vous voulez utiliser le nouveau Centre logiciel. Celui-ci permet aux utilisateurs finaux d’effectuer des recherches parmi les applications disponibles et de les installer sans avoir à accéder au catalogue des applications (ce qui nécessite un navigateur web compatible Silverlight).  

        -   **Autorisations d'installation**.  

        -   **Afficher les notifications de nouveaux déploiements**.  

    2.  Groupe**Gestion de l'alimentation** :  

        -   **Autoriser les utilisateurs à exclure leur appareil de la gestion de l'alimentation**.  

    3.  Groupe**Outils de contrôle à distance** :  

        -   **Les utilisateurs peuvent modifier les paramètres de stratégie ou de notification dans le Centre logiciel**.  

    4.  Groupe**Affinité entre utilisateur et périphérique** :  

        -   **Autoriser les utilisateurs à définir leurs périphériques principaux**.  

    > [!NOTE]  
    >  Pour plus d'informations sur les paramètres client, voir [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

5.  Choisissez **OK** pour fermer la boîte de dialogue **Paramètres client par défaut**.  

Les ordinateurs clients sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour lancer la récupération de stratégie pour un seul client, consultez [Guide pratique pour gérer les clients](../../core/clients/manage/manage-clients.md).

#### <a name="to-customize-software-center-branding"></a>Personnaliser la marque du Centre logiciel

Une marque personnalisée pour le Centre logiciel est appliquée selon les règles suivantes :

1. Si le rôle de serveur de site du point du site web du catalogue des applications n’est pas installé, le Centre logiciel affiche le nom d’organisation spécifié dans le paramètre client de l’**Agent ordinateur** **Nom d’organisation** affiché dans le Centre logiciel. Pour obtenir des instructions, consultez [Guide pratique pour configurer les paramètres client](https://docs.microsoft.com/sccm/core/clients/deploy/configure-client-settings).
2. Si le rôle de serveur site de point du site web du catalogue des applications est installé, le Centre logiciel affiche le nom d’organisation et la couleur spécifiés dans les propriétés du rôle de serveur de site du point du site web du catalogue des applications. Pour plus d’informations, consultez [Options de configuration pour le point du site web du catalogue des applications](https://docs.microsoft.com/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#BKMK_ApplicationCatalog_Website).
3. Si un abonnement Microsoft Intune est configuré et connecté à Configuration Manager, le Centre logiciel affiche le nom d’organisation, la couleur et le logo de l’entreprise spécifiés dans les propriétés de l’abonnement Intune. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).

#### <a name="to-manually-set-software-center-branding"></a>Pour définir manuellement la marque du Centre logiciel
<!-- 1351224 -->
Avec la version 1710, vous pouvez ajouter manuellement des éléments de personnalisation d’entreprise et spécifier la visibilité des onglets du Centre logiciel. Vous pouvez ajouter votre nom de société Centre logiciel spécifique, définir un modèle de couleurs de configuration Centre logiciel, un logo de société et les onglets visibles pour les périphériques clients.

1. Dans la console **Configuration Manager**, cliquez sur **Administration** > **Paramètres client**. Cliquez sur l’instance de paramètre de client souhaitée.
2. Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.
3. Dans la boîte de dialogue **Paramètres par défaut**, choisissez **Centre logiciel**.
4. Sélectionnez **Oui** pour **sélectionner de nouveaux paramètres afin de spécifier les informations de l’entreprise** et permettre la modification des paramètres de personnalisation du Centre logiciel.
5. Spécifiez le **nom de votre entreprise**.
6. Sélectionnez votre **modèle de couleurs pour le Centre logiciel**.
7. Cliquez sur **Parcourir** pour sélectionner votre logo pour le Centre logiciel. Le logo doit être de type JPEG ou PNG et au format 400 x 100 pixels, avec une taille maximale de 750 Ko.
8. Sélectionnez **OUI** pour afficher les onglets dans le Centre logiciel pour les périphériques clients. Au moins un onglet doit être visible :

    -  Activer l’onglet Applications
    -  Activer l’onglet Mises à jour
    -  Activer l’onglet Systèmes d'exploitation
    -  Activer l’onglet État de l’installation
    -  Activer l’onglet Conformité de l’appareil
    -  Activer l’onglet Options

> [!IMPORTANT]  
>  La personnalisation du Centre logiciel est synchronisée avec le service Intune tous les 14 jours. Par conséquent, il peut passer un certain temps avant que les modifications que vous apportez dans Intune ne s’affichent dans Configuration Manager.

###  <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Étape 5 : vérifier que le catalogue des applications est opérationnel  
 Utilisez les procédures suivantes pour vérifier que le catalogue d'applications est opérationnel. Vous pouvez utiliser le catalogue des applications directement à partir d’un navigateur ou du Centre logiciel.  

> [!NOTE]  
>  Le catalogue des applications nécessite Microsoft Silverlight, qui est automatiquement installé comme prérequis pour le client Configuration Manager. Si vous utilisez le catalogue des applications directement à partir d’un navigateur sur un ordinateur où le client Configuration Manager n’est pas installé, vérifiez d’abord que Microsoft Silverlight est installé sur l’ordinateur.  

> [!TIP]  
>  L’absence des prérequis fait partie des causes les plus fréquentes des dysfonctionnements du catalogue des applications après l’installation. Vérifiez la configuration requise en matière de rôles de système de site pour les rôles de système de site du catalogue des applications. Vous pouvez pour cela vous aider de l’article [Configurations prises en charge](../../core/plan-design/configs/supported-configurations.md).  

> [!NOTE]  
>  Si vous êtes connecté avec un compte d’administrateur de domaine, les messages de notification en provenance du client Configuration Manager (par exemple les messages indiquant que de nouveaux logiciels sont disponibles) ne s’affichent pas.  

### <a name="to-use-the-application-catalog-directly-from-a-browser"></a>Pour utiliser le catalogue des applications directement depuis un navigateur  

-   Dans un navigateur, entrez l’adresse du site web du catalogue des applications et vérifiez que la page web affiche les trois onglets : **Catalogue des applications**, **Mes demandes d’application**et **Mes appareils**.  

     Sélectionnez et utilisez l’adresse appropriée dans la liste suivante pour le catalogue des applications, où &lt;serveur&gt; est le nom de l’ordinateur, le nom de domaine complet de l’intranet ou le nom de domaine complet Internet :  

    -   Connexions clientes HTTPS et paramètres de rôle de système de site par défaut : **https://&lt;serveur&gt;/CMApplicationCatalog**  

    -   Connexions clientes HTTP et paramètres de rôle de système de site par défaut : **http://&lt;serveur&gt;/CMApplicationCatalog**  

    -   Connexions clientes HTTPS et paramètres de rôle de système de site personnalisés : **https://&lt;serveur&gt;:&lt;port&gt;/&lt;nom_application_web&gt;**  

    -   Connexions clientes HTTP et paramètres de rôle de système de site personnalisés : **http://&lt;serveur&gt;:&lt;port&gt;/&lt;nom_application_web&gt;**  

### <a name="to-use-the-application-catalog-from-software-center-does-not-apply-to-the-new-version-of-software-center"></a>Pour utiliser le catalogue des applications à partir du Centre logiciel (ne s’applique pas à la nouvelle version du Centre logiciel)  

1.  Sur un ordinateur client, choisissez **Démarrer** > **Tous les programmes** > **Microsoft System Center 2012** > **Configuration Manager** > **Centre logiciel**.  

2.  Si vous avez précédemment configuré un nom d'organisation en tant que paramètre client pour le Centre logiciel, vérifiez qu'il s'affiche comme prévu.  

3.  Choisissez **Rechercher d’autres applications à partir du catalogue des applications** et vérifiez que la page affiche les trois onglets : **Catalogue des applications**, **Mes demandes d’application** et **Mes appareils**.  

> [!WARNING]  
>  Après avoir installé les rôles de système de site du catalogue des applications, vous ne voyez pas immédiatement le catalogue des applications quand vous choisissez le lien **Rechercher d’autres applications à partir du catalogue des applications** du Centre logiciel. Le catalogue d'applications n'est disponible depuis le Centre logiciel qu'une fois que le client a téléchargé sa stratégie client ou jusqu'à 25 heures après l'installation des rôles de système de site du catalogue d'applications.  
