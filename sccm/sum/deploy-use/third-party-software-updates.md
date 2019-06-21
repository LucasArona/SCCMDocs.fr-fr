---
title: Activer les mises à jour tierces
titleSuffix: Configuration Manager
description: Activer les mises à jour tierces dans Configuration Manager
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 946b0f74-0794-4e8f-a6af-9737d877179b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3279ba7cd78ca6fc10ddb8662ac816679d01d7cf
ms.sourcegitcommit: 60d45a5df135b84146f6cfea2bac7fd4921d0469
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67194682"
---
# <a name="enable-third-party-updates"></a>Activer les mises à jour tierces 

*S’applique à : System Center Configuration Manager version 1806*

Depuis la version 1806, le nœud **Catalogues de mises à jour de logiciels tiers** de la console Configuration Manager vous permet de vous abonner à des catalogues tiers, de publier leurs mises à jour sur votre point de mise à jour logicielle, puis de les déployer sur les clients.  <!--1357605, 1352101, 1358714-->



## <a name="prerequisites"></a>Prérequis 
- Suffisamment d’espace disque dans le dossier WSUSContent du point de mise à jour logicielle de niveau supérieur pour stocker le contenu binaire source des mises à jour logicielles tierces.
    - La quantité de stockage nécessaire varie en fonction du fournisseur, du type de mise à jour, ainsi que des mises à jour que vous publiez en vue de leur déploiement.
    - Si vous avez besoin de déplacer le dossier WSUSContent sur un lecteur qui contient davantage d’espace, consultez le billet de blog [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/).
- Le service de synchronisation des mises à jour logicielles tierces nécessite un accès Internet.
    - Pour obtenir la liste des catalogues partenaires, vous devez accéder à download.microsoft.com sur le port HTTPS 443. 
    -  Accès Internet aux catalogues tiers et aux fichiers de contenu de mise à jour. Des ports supplémentaires, en plus du port 443, peuvent être nécessaires.
    - Les mises à jour tierces utilisent les mêmes paramètres de proxy que le point de mise à jour logicielle.

## <a name="additional-requirements-when-the-sup-is-remote-from-the-top-level-site-server"></a>Autre exigences quand le point de mise à jour logicielle est distant par rapport au serveur de site de niveau supérieur 

1. SSL doit être activé sur le point de mise à jour logicielle quand celui-ci est distant. Un certificat d’authentification serveur généré à partir d’une autorité de certification interne ou par le biais d’un fournisseur public est donc nécessaire.
    - [Configurer SSL sur WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL)
        - Quand vous configurez SSL sur WSUS, certains services web et répertoires virtuels utilisent toujours HTTP et non HTTPS. 
        - Configuration Manager télécharge le contenu tiers des packages de mise à jour logicielle à partir de votre répertoire de contenu WSUS via HTTP.   
    - [Configurer SSL sur le point de mise à jour logicielle](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. Lors de la définition de la configuration du certificat de signature WSUS des mises à jour de tiers **Configuration Manager gère les mises à jour** dans les Propriétés du composant du point de mise à jour logicielle, les configurations suivantes sont nécessaires pour autoriser la création du certificat de signature de WSUS auto-signé : 
   - Le Registre à distance doit être activé sur le serveur de point de mise à jour logicielle.
   -  Le **compte de connexion du serveur WSUS** doit disposer d’autorisations de Registre à distance sur le serveur de point de mise à jour logicielle/WSUS. 


3. Créez la clé de Registre suivante sur le serveur de site Configuration Manager : 
    - Dans la clé de Registre `HKLM\Software\Microsoft\Update Services\Server\Setup`, créez un DWORD nommé **EnableSelfSignedCertificates** avec la valeur `1`. 

4. Pour permettre l’installation du certificat de signature WSUS auto-signé dans les magasins Éditeurs approuvés et Racine approuvée sur le serveur de point de mise à jour logicielle distant :
   - Le **compte de connexion du serveur WSUS** doit disposer d’autorisations d’administration à distance sur le serveur de point de mise à jour logicielle.

     Si cela n’est pas possible, exportez le certificat du magasin WSUS de l’ordinateur local vers les magasins Éditeurs approuvés et Racine approuvée. 

> [!NOTE] 
>Le **compte de connexion du serveur WSUS** peut être identifié sous l’onglet **Paramètres de compte et proxy** dans les propriétés de rôle Système du point de mise à jour logicielle. Si aucun compte n’est spécifié, le compte d’ordinateur du serveur de site est utilisé.

## <a name="enable-third-party-updates-on-the-sup"></a>Activer les mises à jour tierces sur le point de mise à jour logicielle
Si vous activez cette option, vous pouvez vous abonner aux catalogues de mises à jour tierces dans la console Configuration Manager. Vous pouvez ensuite publier ces mises à jour dans WSUS et les déployer sur les clients. Les étapes ci-dessous doivent être exécutées une fois par hiérarchie pour activer et configurer la fonctionnalité à utiliser. Il peut s’avérer nécessaire de réexécuter les étapes si jamais vous remplacez le serveur WSUS du point de mise à jour logicielle de niveau supérieur. 

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site**, puis sélectionnez le nœud **Sites**.
2. Sélectionnez le site de niveau supérieur dans la hiérarchie. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sélectionnez **Point de mise à jour logicielle**.
3. Basculez sous l’onglet **Mises à jour tierces**. Sélectionnez l’option **Activer les mises à jour de logiciels tiers**.

    ![Capture d’écran des propriétés du point de mise à jour logicielle tierce](media/third-party-sup-properties.PNG)


## <a name="configure-the-wsus-signing-certificate"></a>Configurer le certificat de signature WSUS
Vous devez décider si vous voulez que Configuration Manager gère automatiquement le certificat de signature WSUS tiers en utilisant un certificat auto-signé ou si vous préférez configurer manuellement le certificat. 

### <a name="automatically-manage-the-wsus-signing-certificate"></a>Gérer automatiquement le certificat de signature WSUS
Si vous n’avez pas l’obligation d’utiliser des certificats PKI, vous pouvez choisir de gérer automatiquement les certificats de signature pour les mises à jour tierces. La gestion des certificats WSUS est assurée pendant le cycle de synchronisation et est consignée dans `wsyncmgr.log`. 

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site**, puis sélectionnez le nœud **Sites**.
2. Sélectionnez le site de niveau supérieur dans la hiérarchie. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sélectionnez **Point de mise à jour logicielle**.
3. Basculez sous l’onglet **Mises à jour tierces**. Sélectionnez l’option **Configuration Manager gère le certificat**. 
4. Tout nouveau certificat de type **Signature WSUS tierce** est créé dans le nœud **Certificats**, sous **Sécurité**, dans l’espace de travail **Administration**.  

### <a name="manually-manage-the-wsus-signing-certificate"></a>Gérer manuellement le certificat de signature WSUS
Si vous avez besoin de configurer manuellement le certificat, par exemple pour utiliser un certificat PKI, vous devez utiliser l’[éditeur de mise à jour System Center](../tools/updates-publisher-options.md#update-server) ou un autre outil prévu à cet effet.  

1. Configurez le certificat de signature à l’aide de l’[éditeur de mise à jour System Center](../tools/updates-publisher-options.md#update-server).
2. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site**, puis sélectionnez le nœud **Sites**.
3. Sélectionnez le site de niveau supérieur dans la hiérarchie. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sélectionnez **Point de mise à jour logicielle**.
4. Basculez sous l’onglet **Mises à jour tierces**. Sélectionnez l’option permettant de **gérer manuellement le certificat**.


## <a name="enable-third-party-updates-on-the-clients"></a>Activer les mises à jour tierces sur les clients
Activez les mises à jour tierces sur les clients dans les paramètres client. Les paramètres définissent la stratégie de l’agent Windows Update pour [Autoriser les mises à jour signées provenant d’un emplacement intranet du service de mise à jour Microsoft](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). Ce paramètre client installe aussi le certificat de signature WSUS dans la banque Éditeurs approuvés du client. La journalisation de la gestion de certificats peut être consultée dans le fichier `updatesdeployment.log` des clients.  Exécutez ces étapes pour chaque paramètre client personnalisé que vous voulez utiliser pour les mises à jour tierces. Pour plus d’informations, consultez l’article [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates).

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Paramètres du client**.
2. Sélectionnez un paramètre client personnalisé existant ou créez-en un. 
3. Sélectionnez l’onglet **Mises à jour logicielles** dans la partie gauche. Si cet onglet n’est pas visible, vérifiez que la zone **Mises à jour logicielles** est activée.
4. Définissez **Activer les mises à jour de logiciels tiers** sur **Oui**. 


## <a name="add-a-custom-catalog"></a>Ajouter un catalogue personnalisé
Les *catalogues de partenaires* sont des catalogues d’éditeurs de logiciels dont les informations sont déjà inscrites auprès de Microsoft. Vous pouvez vous abonner à ces catalogues sans avoir à spécifier des informations supplémentaires. Les catalogues que vous ajoutez sont appelés *catalogues personnalisés*. Vous pouvez ajouter le catalogue personnalisé d’un fournisseur de mises à jour tierces à Configuration Manager. Les catalogues personnalisés doivent utiliser le protocole HTTP et les mises à jour doivent être signées numériquement. 

1. Accédez à l’espace de travail **Bibliothèque de mises à jour logicielles**, développez **Mises à jour logicielles**, puis sélectionnez le nœud **Catalogues de mises à jour de logiciels tiers**. 
   
     ![Capture d’écran du nœud de mises à jour tierces](media/third-party-updates-node.PNG)
2. Cliquez sur **Ajouter un catalogue personnalisé** dans le ruban. 

     ![Ajout d’un catalogue personnalisé de mises à jour tierces](media/third-party-updates-custom-catalog.png)
1. Dans la page **Général**, spécifiez les éléments suivants : 
    - **URL de téléchargement** : adresse HTTPS valide du catalogue personnalisé.
    - **Éditeur** : nom de l’organisation qui publie le catalogue. 
    - **Nom** : nom du catalogue à afficher dans la console Configuration Manager. 
    - **Description** : description du catalogue. 
    - **URL de support** (facultatif) : adresse HTTPS valide d’un site web d’aide sur le catalogue. 
    - **Contact de support** (facultatif) : coordonnées à contacter pour obtenir de l’aide sur le catalogue. 
2. Cliquez sur **Suivant** pour passer en revue le résumé du catalogue et poursuivre l’**Assistant Catalogue personnalisé de mises à jour logicielles tierces**.


## <a name="subscribe-to-a-third-party-catalog-and-sync-updates"></a>S’abonner à un catalogue tiers et synchroniser les mises à jour
Quand vous vous abonnez à un catalogue tiers dans la console Configuration Manager, les métadonnées de chaque mise à jour du catalogue sont synchronisées dans les serveurs WSUS pour vos points de mise à jour logicielle. La synchronisation des métadonnées permet aux clients de déterminer si les mises à jour sont applicables. Effectuez les étapes suivantes pour chaque catalogue tiers auquel vous voulez vous abonner :  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Mises à jour logicielles**, puis sélectionnez le nœud **Catalogues de mises à jour de logiciels tiers**.  
2. Sélectionnez le catalogue auquel vous abonner, puis cliquez sur **S’abonner au catalogue** dans le ruban. 
    ![Ajout d’un catalogue personnalisé de mises à jour tierces](media/third-party-updates-subscribe.png)
3. Examinez et approuvez le certificat du catalogue.  
   > [!NOTE]
   > 
   > Lorsque vous vous abonnez à un catalogue de mises à jour de logiciels tiers, le certificat que vous examinez et approuvez dans l’Assistant est ajouté au site. Ce certificat appartient au type **Catalogue des mises à jour de logiciels tiers**. Vous pouvez le gérer dans le nœud **Certificats**, situé sous **Sécurité**, dans l’espace de travail **Administration**.  
4. Effectuez toutes les étapes de l'Assistant. À l’issue de l’abonnement initial, le téléchargement du catalogue débute après quelques minutes. 
    - Le catalogue se synchronise automatiquement tous les 7 jours.
    - Cliquez sur **Synchroniser maintenant** dans le ruban pour forcer une synchronisation.
5. Une fois le catalogue téléchargé, les métadonnées de produit doivent être synchronisées de la base de données WSUS vers la base de données Configuration Manager. [Démarrez manuellement la synchronisation des mises à jour logicielles](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) pour synchroniser les informations de produit.
6. Une fois les informations de produit synchronisées, [configurez le point de mise à jour logicielle pour synchroniser le produit souhaité](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) dans Configuration Manager.  
7. [Démarrez manuellement la synchronisation des mises à jour logicielles](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) pour synchroniser les nouvelles mises à jour de produit dans Configuration Manager.  
8. À l’issue de la synchronisation, les mises à jour tierces figurent dans le nœud **Toutes les mises à jour**. Ces mises à jour sont publiées en tant que mises à jour de **métadonnées uniquement** jusqu’à ce que vous choisissiez de les publier. 
     - L’icône avec une flèche bleue représente une mise à jour logicielle de métadonnées uniquement. ![Icône de mise à jour logicielle de métadonnées uniquement](media/MetadataOnly.png)


## <a name="publish-and-deploy-third-party-software-updates"></a>Publier et déployer des mises à jour logicielles tierces 
Dès lors que les mises à jour tierces se trouvent dans le nœud **Toutes les mises à jour**, vous pouvez choisir celles qui doivent être publiées pour le déploiement. Quand vous publiez une mise à jour, les fichiers binaires sont téléchargés auprès du fournisseur et placées dans le répertoire WSUSContent du point de mise à jour logicielle de niveau supérieur. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Mises à jour logicielles**, puis sélectionnez le nœud **Toutes les mises à jour logicielles**.
2. Pour filtrer la liste des mises à jour, cliquez sur **Ajouter des critères**. Par exemple, ajoutez **Fournisseur** pour **HP**. pour afficher toutes les mises à jour de HP.  
3. Sélectionnez les mises à jour dont a besoin votre organisation. Cliquez sur **Publier le contenu des mises à jour de logiciels tiers**.
    - Cette action télécharge les fichiers binaires de mise à jour auprès du fournisseur, puis les stocke dans le dossier WSUSContent du point de mise à jour logicielle de niveau supérieur. 
4. [Démarrez manuellement la synchronisation des mises à jour logicielles](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) pour faire passer l’état des mises à jour publiées de « métadonnées uniquement » à « mises à jour déployables avec du contenu ». 
    >[!NOTE]
    >Lorsque vous publiez le contenu de mises à jour de logiciels tiers, tous les certificats utilisés pour signer le contenu sont ajoutés au site. Ces certificats appartiennent au type **Contenu des mises à jour de logiciels tiers**. Vous pouvez les gérer dans le nœud **Certificats**, situé sous **Sécurité**, dans l’espace de travail **Administration**.  

5. Examinez la progression dans SMS_ISVUPDATES_SYNCAGENT.log. Le journal se trouve sur le point de mise à jour logicielle de niveau supérieur dans le dossier des journaux du système de site.
6. Déployez les mises à jour en suivant le processus [Déployer des mises à jour logicielles](../deploy-use/deploy-software-updates.md). 
7. Dans la page **Emplacements de téléchargement** de l’**Assistant Déploiement des mises à jour logicielles**, sélectionnez l’option par défaut pour **Télécharger les mises à jour logicielles à partir d’Internet**. Dans ce scénario, le contenu a déjà été publié sur le point de mise à jour logicielle, qui est utilisé pour télécharger le contenu du package de déploiement.
8. Les clients devront exécuter une analyse et évaluer les mises à jour avant que vous puissiez voir les résultats de conformité.  Vous pouvez déclencher ce cycle manuellement sur un client, à partir du panneau de configuration Configuration Manager, en exécutant l’action **Cycle d’analyse des mises à jour de logiciels**.


## <a name="monitoring-progress-of-third-party-software-updates"></a>Surveillance de la progression du téléchargement des mises à jour de logiciels tiers 

La synchronisation des mises à jour logicielles tierces est gérée par le composant SMS_ISVUPDATES_SYNCAGENT sur le point de mise à jour logicielle par défaut de niveau supérieur. Vous pouvez afficher les messages d’état de ce composant, ou lire des informations d’état plus détaillées dans le journal SMS_ISVUPDATES_SYNCAGENT.log. Ce journal se trouve sur le point de mise à jour logicielle de niveau supérieur dans le dossier des journaux du système de site. Par défaut, ce chemin est C:\Program Files\Microsoft Configuration Manager\Logs. Pour plus d’informations sur la surveillance du processus général de gestion des mises à jour logicielles, consultez [Surveiller les mises à jour logicielles](../deploy-use/monitor-software-updates.md). 

## <a name="known-issues"></a>Problèmes connus

- L’ordinateur sur lequel est exécutée la console est utilisé pour télécharger les mises à jour à partir de WSUS et les ajouter au package de mises à jour. Le certificat de signature WSUS doit être approuvé sur l’ordinateur de la console. Dans le cas contraire, la vérification de la signature peut occasionner des problèmes pendant le téléchargement de mises à jour tierces. 
- Le service de synchronisation des mises à jour de logiciels tiers ne peut pas publier le contenu des mises à jour de métadonnées uniquement qui ont été ajoutées à WSUS par une autre application, un autre outil ou un autre script, tel que SCUP. L’action **Publier le contenu des mises à jour de logiciels tiers** échoue avec ces mises à jour. Si vous avez besoin de déployer des mises à jour tierces qui ne sont pas encore prises en charge par cette fonctionnalité, suivez l’intégralité de votre processus existant pour déployer ces mises à jour.  
-  Configuration Manager propose une nouvelle version pour le format de fichier cab de catalogue. La nouvelle version comprend les certificats des fichiers binaires du fournisseur. Ces certificats sont ajoutés au nœud **Certificats** sous **Sécurité** dans l’espace de travail **Administration** dès lors que vous avez approuvé et accordé votre confiance au catalogue.  
     - Vous pouvez toujours utiliser l’ancienne version de fichier cab de catalogue du moment que l’URL de téléchargement est https et que les mises à jour sont signées. La publication du contenu échouera, car les certificats des fichiers binaires ne se trouvent pas dans le fichier cab et sont déjà approuvés. Vous pouvez contourner ce problème en recherchant le certificat dans le nœud **Certificats**, en le débloquant, puis en publiant à nouveau la mise à jour. Si vous publiez plusieurs mises à jour signées avec différents certificats, vous devez débloquer chaque certificat utilisé.
     - Pour plus d’informations, consultez les messages d’état 11523 et 11524 dans le tableau des messages d’état suivant.
-  Lorsque le service de synchronisation des mises à jour logicielles tiers situé au-dessus du point de mise à jour logicielle de niveau supérieur nécessite un serveur proxy pour accéder à Internet, les vérifications de la signature numérique peuvent échouer. Pour résoudre ce problème, configurez les paramètres de proxy WinHTTP sur le système du site. Pour plus d’informations, consultez [commandes Netsh pour WinHTTP](https://go.microsoft.com/fwlink/p/?linkid=199086).

## <a name="status-messages"></a>Messages d'état

| MessageID       | Niveau de gravité           | Description | Cause possible| Solution possible
| ------------- |-------------| -----|----|----|
| 11516     | Erreur |Impossible de publier le contenu de la mise à jour « ID de mise à jour », car le contenu n’est pas signé.  Seul le contenu présentant des signatures valides peut être publié.  |Configuration Manager n’autorise pas la publication des mises à jour non signées.| Publiez la mise à jour d’une autre façon. </br></br>Renseignez-vous auprès du fournisseur pour savoir s’il dispose d’une mise à jour signée.|
| 11523  | Avertissement |  Le catalogue « X » ne contient pas de certificats de signature de contenu. La publication de contenu pour les mises à jour de ce catalogue risque d’échouer tant que des certificats de signature de contenu n’auront pas été ajoutés et approuvées. | Ce message peut apparaître quand vous importez un catalogue qui utilise une ancienne version du format de fichier cab.|Contactez le fournisseur du catalogue pour en obtenir une version mise à jour avec les certificats de signature de contenu. </br> </br> Les certificats des fichiers binaires n’étant pas inclus dans le fichier cab, le contenu ne sera pas publié. Vous pouvez contourner ce problème en recherchant le certificat dans le nœud **Certificats**, en le débloquant, puis en publiant à nouveau la mise à jour. Si vous publiez plusieurs mises à jour signées avec différents certificats, vous devez débloquer chaque certificat utilisé.|
| 11524| Erreur  | Impossible de publier la mise à jour « ID » du fait de l’absence de métadonnées de mise à jour. | La mise à jour a peut-être été synchronisée avec le serveur WSUS en dehors de Configuration Manager.| Synchronisez la mise à jour avec Configuration Manager avant d’essayer de publier son contenu.  </br> </br>Si un outil externe a été utilisé pour publier la mise à jour en tant que mise à jour de **métadonnées uniquement**, utilisez ce même outil pour publier le contenu de la mise à jour.|



## <a name="working-with-third-party-updates-video"></a>Utilisation de mises à jour tierces (vidéo)
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>



## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Déployer des mises à jour logicielles](./deploy-software-updates.md)
