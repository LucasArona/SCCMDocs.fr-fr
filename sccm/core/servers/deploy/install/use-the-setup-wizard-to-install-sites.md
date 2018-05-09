---
title: Assistant Installation
titleSuffix: Configuration Manager
ms.date: 7/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c15f59ababae6908a08c28d3ec8ad46075068d52
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Utilisez l’Assistant Installation pour installer des sites System Center Configuration Manager.

*S’applique à : System Center Configuration Manager (Current Branch)*


Pour installer un nouveau site System Center Configuration Manager en utilisant une interface utilisateur guidée, vous utilisez l’Assistant Installation de Configuration Manager (setup.exe). Cet Assistant prend en charge l’installation d’un site principal ou d’un site d’administration centrale. Vous utilisez également cet Assistant pour [mettre à niveau une installation d’évaluation](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) de Configuration Manager vers une installation sous licence. Si vous ne voulez pas utiliser l’Assistant, vous pouvez utiliser à la place un [script d’installation](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) et exécuter une installation en ligne de commande sans assistance.

Pour installer un site secondaire, vous devez installer le site à partir de la console Configuration Manager. Les sites secondaires ne prennent pas en charge une installation en ligne de commande scriptée.

## <a name="bkmk_primary"></a> Installer un site d’administration centrale ou un site principal
Utilisez la procédure suivante pour installer un site d’administration centrale ou un site principal, ou encore pour mettre à niveau un site d’évaluation vers un site Configuration Manager sous licence.   

Avant de commencer l’installation du site, vous devez être familiarisé avec le contenu des articles suivants :
 -  [Préparer l’installation des sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Prérequis à l’installation des sites](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Si vous installez un site d’administration centrale dans le cadre d’un scénario de développement de site, lisez la section [Développer un site principal autonome](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) de cette rubrique avant d’utiliser la procédure suivante.

### <a name="bkmk_installpri"></a> Pour installer un site principal ou un site d’administration centrale

1.  Sur l’ordinateur sur lequel vous voulez installer le site, exécutez **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** pour démarrer l’**Assistant Installation de System Center Configuration Manager**.  

    > [!NOTE]  
    > Quand vous installez un site d’administration centrale pour développer un site principal autonome, ou que vous installez un nouveau site principal enfant dans une hiérarchie existante, vous devez utiliser le média d’installation (fichiers sources) qui correspondent à la version du ou des sites existants. Si vous avez installé des mises à jour dans la console qui ont changé la version des sites installés précédemment, n’utilisez pas le support d’installation d’origine. Utilisez plutôt les fichiers sources du [dossier CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) d’un site mis à jour. Configuration Manager vous impose d’utiliser des fichiers sources qui correspondent à la version du site existant auquel votre nouveau site doit se connecter.  

2.  Dans la page **Avant de commencer**, choisissez **Suivant**.  

3.  Dans la page **Prise en main**, sélectionnez le type de site à installer :  

    -   **Site d’administration centrale** comme premier site d’une nouvelle hiérarchie, ou lors du développement d’un site principal autonome :  

        Sélectionnez **Installer un site d’administration centrale Configuration Manager**.  

         À une étape ultérieure de cette procédure, vous aurez le choix entre installer un site d’administration centrale en tant que premier site d’une nouvelle hiérarchie ou installer un site d’administration centrale par extension d’un site principal autonome.  

    -    **Site principal**, comme site principal autonome constituant le premier site d’une nouvelle hiérarchie, comme site principal enfant :  

        Sélectionnez **Installer un site principal Configuration Manager**.  

        > [!TIP]  
        > En règle générale, vous devez sélectionner l’option **Utiliser les options d’installation par défaut pour un site principal autonome** uniquement pour installer un site principal autonome dans un environnement de test. Quand vous sélectionnez cette option, le programme d’installation :  

        > -   configure automatiquement le site comme site principal autonome ;  
        > -   utilise un chemin d’installation par défaut ;  
        > -   utilise une installation locale de l’instance par défaut de SQL Server pour la base de données du site ;  
        > -   installe un point de gestion et un point de distribution sur l’ordinateur serveur de site ;  
        > -   configure le site en anglais et dans la langue d’affichage du système d’exploitation sur le serveur de site principal si elle correspond à l’une des langues prises en charge par Configuration Manager.  

4.  Sur la page **Clé du produit** :
    - Choisissez d’installer Configuration Manager en tant que version d’évaluation ou version sous licence.  

      -   Si vous sélectionnez une version sous licence, entrez votre clé de produit, puis choisissez **Suivant**.  

      -   Si vous sélectionnez une édition d’évaluation, choisissez **Suivant**. (Vous pouvez mettre à niveau une installation d’évaluation vers une installation complète ultérieurement.)  
    - À compter de la version Release d’octobre 2016 du support de base de référence de la version 1606 de System Center Configuration Manager, vous pouvez spécifier la date d’expiration de votre contrat Software Assurance. Dans cette page, vous avez la possibilité de spécifier la **date d’expiration de la Software Assurance** de votre contrat de licence en guise de rappel pratique pour vous. Si vous n’entrez pas cette date pendant l’installation, vous pouvez la spécifier ultérieurement dans la console Configuration Manager.

      > [!NOTE]   
      > Microsoft ne valide pas la date d’expiration que vous entrez et ne l’utilise pas pour la validation de la licence. Vous pouvez ainsi l’utiliser en guise de rappel de votre date d’expiration. Ce rappel est pratique, car Configuration Manager vérifie régulièrement les nouvelles mises à jour logicielles proposées en ligne, et l’état de votre licence Software Assurance doit être actualisé pour que vous soyez autorisé à utiliser ces mises à jour supplémentaires.    

      Pour plus d’informations, consultez [Licences et branches pour System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

5.  Dans la page **Termes du contrat de licence logiciel Microsoft** , lisez et acceptez les termes du contrat de licence.  

6.  Dans la page **Licences requises** , lisez et acceptez les termes du contrat de licence pour les logiciels requis. Le programme d’installation télécharge et installe automatiquement les logiciels sur les systèmes ou les clients du site, si nécessaire. Vous devez cocher toutes les cases pour pouvoir passer à la page suivante.  

7.  Dans la page **Téléchargements requis** , spécifiez si le programme d’installation doit télécharger les tout derniers fichiers redistribuables requis à partir d’Internet ou utiliser des fichiers téléchargés précédemment :  

    -   Si vous souhaitez que le programme d’installation télécharge les fichiers à ce stade, sélectionnez **Télécharger les fichiers requis** , puis spécifiez l’emplacement où stocker les fichiers.  

    -   Si vous avez précédemment téléchargé les fichiers à l'aide du [téléchargeur d'installation](../../../../core/servers/deploy/install/setup-downloader.md), sélectionnez **Utiliser des fichiers précédemment téléchargés**, puis spécifiez le dossier de téléchargement.  

        > [!TIP]  
        > Si vous utilisez des fichiers téléchargés précédemment, vérifiez que le dossier de téléchargement indiqué contient la version la plus récente des fichiers.  

8.  Dans la page **Sélection de la langue du serveur**, sélectionnez les langues disponibles pour la console Configuration Manager et les rapports. (L’anglais est sélectionné par défaut et ne peut pas être supprimé.)  

9. Dans la page **Sélection de la langue client**, sélectionnez les langues disponibles pour les ordinateurs clients, puis spécifiez si vous voulez activer toutes les langues du client pour les clients d’appareils mobiles. (L’anglais est sélectionné par défaut et ne peut pas être supprimé.)  

    > [!IMPORTANT]  
    > Quand vous utilisez un site d’administration centrale, vérifiez que les langues du client que vous configurez sur ce site incluent toutes les langues du client que vous configurez au niveau de chaque site principal enfant. En effet, les clients qui effectuent l’installation à partir d’un point de distribution ont accès aux langues du client à partir du site de niveau supérieur, tandis que les clients qui effectuent l’installation à partir d’un point de gestion ont accès aux langues du client à partir de leur site principal attribué.  

10. Dans la page **Paramètres d’installation et du site**, spécifiez les éléments suivants pour le nouveau site que vous installez :  

    -   **Code de site** [: dans une hiérarchie, le code de chaque site doit être unique](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) et constitué de trois caractères alphanumériques (A à Z et 0 à 9). Étant donné que le code de site est utilisé dans les noms de dossier, n’utilisez pas de noms réservés à Windows pour le site, à savoir :    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        > Le programme d’installation ne vérifie pas si le code de site que vous spécifiez est déjà utilisé ou s’il s’agit d’un nom réservé.  

    -   **Nom du site** : chaque site doit posséder un nom convivial pour faciliter son identification.  

    -   **Dossier d’installation** : chemin du dossier de l’installation de Configuration Manager. Vous ne pouvez pas modifier cet emplacement après l’installation du site. De plus, ce chemin ne doit pas contenir de caractères Unicode, ni d’espaces en fin de chaîne.  

11. Dans la page **Installation de site**, utilisez l’option suivante correspondant à votre scénario :  

    -   **J’installe un site d’administration centrale :**  

         Dans la page **Installation du site d’administration centrale**, sélectionnez **Installer en tant que premier site d’une nouvelle hiérarchie**, puis choisissez sur **Suivant** pour continuer.  

    -   **J’étends un site principal autonome en une hiérarchie comportant un site d’administration centrale :**  

         Dans la page **Installation du site d’administration centrale**, sélectionnez **Étendre un site principal autonome existant dans une hiérarchie**, spécifiez le nom de domaine complet (FQDN) du serveur de site principal autonome, puis choisissez **Suivant** pour continuer.  

         Le support que vous utilisez pour installer le nouveau site d’administration centrale doit correspondre à la version du site principal.  

    -   **J’installe un site principal autonome :**  

         Dans la page **Installation du site principal**, sélectionnez**Installer le site principal en tant que site autonome**, puis choisissez **Suivant**.  

    -   **J’installe un site principal enfant :**  

         Dans la page **Installation du site principal**, sélectionnez **Joindre le site principal à une hiérarchie existante**, spécifiez le nom de domaine complet (FQDN) pour le site d’administration centrale, puis choisissez **Suivant**.  

12. Dans la page **Informations sur la base de données**, spécifiez les informations suivantes :  

    -   **Nom du SQL Server (FQDN)** : par défaut, il s’agit de l’ordinateur serveur de site.

     Si vous utilisez un port personnalisé, ajoutez ce port au nom FQDN du serveur SQL Server. Pour ce faire, faites suivre le nom FQDN du serveur d’une virgule, puis du numéro de port.   Par exemple, pour le serveur *SQLServer1.fabrikam.com*, procédez ainsi pour spécifier le port *1551* : **SQLServer1.fabrikam.com,1551**

    -   **Nom de l’instance** : par défaut, cette valeur est vide. L’instance par défaut de SQL est utilisée sur l’ordinateur serveur de site.  

    -   **Nom de base de données** : par défaut, la valeur définie est CM_&lt;codeSite\>. Vous êtes libre de spécifier un autre nom de votre choix.  

    -   **Port Service Broker** : la valeur prédéfinie indique d’utiliser le port SQL Server Service Broker (SSB) par défaut (4022). SQL l’utilise communiquer directement avec des bases de données d’autres sites.  

13. Dans la deuxième page **Informations sur la base de données**, vous pouvez spécifier des emplacements autres que ceux par défaut pour le fichier de données SQL Server et le fichier journal SQL Server pour la base de données du site :  

    -   Les emplacements de fichier par défaut pour SQL Server sont indiqués.  

    -   Cette possibilité de spécifier des emplacements de fichiers autres que les emplacements par défaut n’est pas disponible quand vous utilisez un cluster SQL Server.  

    -   L’Outil de vérification des prérequis ne vérifie pas l’espace disque disponible aux emplacements de fichiers autres que les emplacements par défaut.  

14. Dans la page **Paramètres du fournisseur SMS** , spécifiez le nom de domaine complet (FQDN) du serveur sur lequel vous souhaitez installer le fournisseur SMS.  

    -   Le serveur de site est spécifié par défaut.  

    -   Une fois le site installé, vous pouvez configurer d’autres fournisseurs SMS.  

15. Dans la page **Paramètres de communication du client** , choisissez de configurer tous les systèmes de site pour accepter uniquement les communications HTTPS en provenance de clients ou de configurer la méthode de communication pour chaque rôle de système de site.  

    Quand vous sélectionnez **Tous les rôles de système de site acceptent uniquement les communications HTTPS depuis les clients**, l’ordinateur client doit avoir un certificat PKI valide pour l’authentification du client. Pour plus d’informations sur la configuration requise des certificats PKI, consultez [Configuration requise des certificats PKI pour Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    > [!NOTE]  
    > Effectuez cette étape uniquement si vous installez un site principal. Si vous installez un site d’administration centrale, ignorez cette étape.  

16. Sur la page **Rôles système de site** , choisissez d'installer un point de gestion ou un point de distribution. Pour chaque rôle de votre choisissez de faire installer par le programme d’installation :  

    -   Vous devez entrer le **nom de domaine complet (FQDN)** de l’ordinateur qui hébergera le rôle et choisir la méthode de connexion client que le serveur prendra en charge (HTTP ou HTTPS).  

    -   Si vous avez sélectionné **Tous les rôles de système de site acceptent uniquement les communications HTTPS depuis les clients** dans la page précédente, les paramètres de connexion client sont configurés automatiquement pour HTTPS et vous ne pouvez pas les modifier sans revenir en arrière et changer le paramètre.  

    > [!NOTE]  
    > Effectuez cette étape uniquement si vous installez un site principal. Si vous installez un site d’administration centrale, ignorez cette étape.  

    > [!NOTE]  
    > Pour installer des rôles de système de site, le programme d’installation utilise le **compte d’installation du système de site**. Par défaut, il utilise le compte d’ordinateur du site principal. Ce compte doit avoir des autorisations d’administrateur local sur un ordinateur distant pour installer le rôle de système de site. Si ce compte ne possède pas les autorisations requises, désélectionnez les rôles de système de site et installez-les ultérieurement à partir de la console Configuration Manager, après avoir configuré des comptes supplémentaires à utiliser en tant que comptes d’installation du système de site.  

17. Dans la page **Données d’utilisation**, consultez les informations relatives aux données que Microsoft collecte, puis choisissez **Suivant**.  

18. La page **Configuration du point de connexion de service** s’affiche pendant l’installation uniquement dans les cas suivants :  

    -   quand vous installez un site principal autonome ;  

    -   quand vous installez un site d’administration centrale.  

    > [!NOTE]  
    > Si vous installez un site principal enfant, ignorez cette étape (cette page n’est pas disponible).  

     Si vous installez un site d’administration centrale dans le cadre d’un scénario de développement de site et que ce rôle est déjà installé sur le site principal autonome, vous devez désinstaller ce rôle du site principal autonome. Une seule instance de ce rôle est autorisée dans une hiérarchie, et uniquement sur le site de niveau supérieur de la hiérarchie.  

     Après avoir sélectionné une configuration pour le **point de connexion de service**, choisissez **Suivant**. (Une fois l’installation terminée, vous pouvez modifier cette configuration à partir de la console Configuration Manager.)  

19. Dans la page **Résumé des paramètres**, vérifiez le paramètre que vous avez sélectionné. Quand vous êtes prêt, choisissez **Suivant** pour démarrer l’Outil de vérification des prérequis.  

20. La page **Vérification de la configuration requise pour l’installation** répertorie tous les problèmes détectés.  

    -   Quand l’outil de vérification de la configuration requise détecte un problème, choisissez un élément affiché dans la liste pour obtenir des détails sur la façon de résoudre le problème.  

    -   Avant de poursuivre l’installation du site, vous devez résoudre chaque élément présentant l’état **Échec**. Les éléments présentant l’état **Avertissement** doivent être résolus, mais ils ne bloquent pas l’installation du site.  

    -   Après avoir résolu les problèmes, choisissez **Vérifier** pour réexécuter l’Outil de vérification des prérequis.  

     Quand l’Outil de vérification des prérequis ne rencontre plus aucun état **Échec**, vous pouvez choisir **Commencer l’installation** pour démarrer l’installation du site.  

    > [!TIP]  
    > Outre les commentaires formulés dans l’Assistant, vous pouvez trouver des informations supplémentaires sur les problèmes liés aux prérequis dans le fichier **ConfigMgrPrereq.log**, situé à la racine du lecteur système de l’ordinateur sur lequel vous effectuez l’installation. Pour obtenir une liste complète des règles et des descriptions des prérequis à l’installation, voir [Liste des vérifications des prérequis pour System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

21. Dans la page **Installation** , le programme d’installation affiche l’état de l’installation. Une fois l’installation du serveur de site principal terminée, vous avez la possibilité de **Fermer** l’Assistant Installation. Quand vous fermez l’Assistant, l’installation et les configurations de site initiales continuent en arrière-plan.  

    -   Vous pouvez connecter une console Configuration Manager au site avant la fin de l’installation. Dans ce cas, cette console est connectée en lecture seule, ce qui signifie qu’elle permet l’affichage des objets et des paramètres, mais pas leur modification.  

    -   Vous devez attendre la fin de l’installation pour pouvoir connecter une console permettant de modifier les objets et paramètres.  


## <a name="bkmk_expand"></a> Développer un site principal autonome
Après avoir installé un site principal autonome comme premier site, vous pouvez développer ce site ultérieurement dans une plus grande hiérarchie en installant un site d’administration centrale.   

Quand vous développez un site principal autonome, vous installez un nouveau site d’administration centrale qui utilise la base de données du site principal autonome existant comme référence. Après l’installation du nouveau site d’administration centrale, le site principal autonome est utilisé comme site principal enfant.

-   Seul un site principal autonome peut être étendu dans une nouvelle hiérarchie.  

-   Un seul site principal autonome peut être étendu dans une hiérarchie spécifique. Vous ne pouvez pas utiliser cette option pour joindre d’autres sites principaux autonomes dans la même hiérarchie. À la place, utilisez une migration pour migrer des données d’une hiérarchie vers une autre.  

-   Après avoir étendu un site autonome dans une hiérarchie comportant un site d’administration centrale, vous pouvez ajouter des sites principaux enfants.  

-   Pour supprimer un site principal d’une hiérarchie ayant un site d’administration centrale, vous devez le désinstaller.  

Pour étendre le site, utilisez l’Assistant Installation de System Center Configuration Manager pour installer un nouveau site d’administration centrale, en prenant les précautions suivantes :  

-   Vous devez installer le site d’administration centrale en utilisant la même version de Configuration Manager que celle utilisée pour le site principal autonome.  

-   Dans la page **Prise en main** de l’Assistant Installation, sélectionnez l’option d’installation d’un site d’administration centrale. À un stade ultérieur, le programme d’installation vous permettra de choisir l’option de développement d’un site principal autonome existant.  

-   Quand vous configurez la page **Sélection de la langue client** pour le nouveau site d’administration centrale, sélectionnez les mêmes langues client que celles configurées pour le site principal autonome que vous développez.  

-   Dans la page **Installation de site**, sélectionnez l’option de développement du site principal autonome.  

Pour développer un site principal autonome, consultez tout d’abord la [configuration requise pour développer un site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand), puis utilisez la procédure *[Pour installer un site principal ou un site d’administration centrale](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, décrite précédemment dans cet article.


## <a name="bkmk_secondary"></a> Installer un site secondaire
 Vous pouvez utiliser la console Configuration Manager pour installer un site secondaire.  

-   Si la console que vous utilisez n’est pas connectée au site principal qui sera le site parent du nouveau site secondaire, la commande d’installation du site sera répliquée sur le site principal approprié.  

-   Avant de commencer l’installation du site, vérifiez que votre compte d’utilisateur dispose des autorisations requises et que l’ordinateur qui va héberger le nouveau site secondaire remplit toutes les conditions préalables à une utilisation comme serveur de site secondaire.  

-   Quand vous installez le site secondaire, Configuration Manager configure le nouveau site pour utiliser les ports de communication client configurés sur le site principal parent.  

### <a name="bkmk_installsecondary"></a> Pour installer un site secondaire  


1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**. Sélectionnez le site qui sera le site principal parent du nouveau site secondaire.  

2.  Choisissez **Créer un site secondaire** pour démarrer l’**Assistant Création de site secondaire**.  

3.  Dans la page **Avant de commencer**, vérifiez que le site principal répertorié est le site à utiliser comme parent du nouveau site secondaire. Ensuite, choisissez **Suivant**.  

4.  Dans la page **Général** , indiquez les informations suivantes :  

    -   **Code de site** : dans une hiérarchie, le code de chaque site doit être unique et constitué de trois caractères alphanumériques (A à Z et 0 à 9). Étant donné que le code de site est utilisé dans les noms de dossier, n’utilisez pas de noms réservés à Windows pour le site, à savoir :  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       > Le programme d’installation ne vérifie pas si le code de site que vous spécifiez est déjà utilisé ou s’il s’agit d’un nom réservé.  

    -   **Nom du serveur de site** : nom de domaine complet du serveur sur lequel le nouveau site secondaire sera installé.  

    -   **Nom du site** : chaque site doit posséder un nom convivial pour faciliter son identification.  

    -   **Dossier d’installation** : chemin du dossier de l’installation de Configuration Manager. Vous ne pouvez pas modifier cet emplacement après l’installation du site. Ce chemin ne doit pas contenir de caractères Unicode, ni d’espaces en fin de chaîne.  

    > [!IMPORTANT]  
    > Après avoir spécifié les détails dans cette page, vous pouvez choisir **Résumé** pour utiliser les paramètres par défaut pour le reste des options de site secondaire et accéder directement à la page **Résumé** de l’Assistant.  

    > -   Utilisez cette option uniquement si vous êtes familiarisé avec les paramètres par défaut de cet Assistant et s’il s’agit des paramètres que vous souhaitez utiliser.  
    > -   Les groupes de limites ne sont pas associés au point de distribution quand vous utilisez les paramètres par défaut. Par conséquent, tant que vous n’avez pas configuré de groupes de limites incluant le serveur de site secondaire, les clients n’utilisent pas le point de distribution installé sur ce site secondaire comme emplacement source du contenu.  

5.  Dans la page **Fichiers sources d’installation** , choisissez la façon dont l’ordinateur du site secondaire obtient les fichiers sources pour l’installation du site.  

     Si vous utilisez des fichiers sources stockés sur le réseau ou sur l’ordinateur du site secondaire :  

    -   L’emplacement des fichiers sources doit inclure un dossier nommé **Redist** contenant tous les fichiers précédemment téléchargés à l’aide du Téléchargeur d’installation.  

    -   Si des fichiers du dossier **Redist** ne sont pas disponibles, le programme d’installation ne peut pas installer le site secondaire.  

    -   Le compte de l’ordinateur du site secondaire doit disposer d’autorisations de **lecture** sur le dossier et le partage des fichiers sources.  

6.  Dans la page **Paramètres SQL Server** , spécifiez la version de SQL Server à utiliser, puis configurez les paramètres associés.  

    > [!NOTE]  
    > Le programme d’installation ne valide pas les informations que vous entrez dans cette page avant de démarrer l’installation. Avant de continuer, vérifiez ces paramètres.  

     **Installer et configurer une copie locale de SQL Express sur l'ordinateur de site secondaire**  

    -   **Port de service de SQL Server**: spécifiez le port de service de SQL Server que SQL Server Express doit utiliser. Le port de service est généralement configuré pour utiliser le port TCP 1433, mais vous pouvez configurer un autre port.  

    -   **Port SQL Server Broker**: spécifiez le port SQL Server Service Broker (SSB) que SQL Server Express doit utiliser. Le Service Broker est généralement configuré pour utiliser le port TCP 4022, mais vous pouvez configurer un port différent. Vous devez spécifier un port valide qu’aucun autre site ou service n’utilise, et qu’aucune restriction de pare-feu ne bloque.  

    > [!IMPORTANT]  
    > Quand Configuration Manager installe SQL Server Express, il installe SQL Server Express 2012 sans Service Pack :  

    > -   Pour permettre la prise en charge du site secondaire, après son installation, vous devez mettre à niveau SQL Server Express 2012 avec [une version prise en charge](/sccm/core/plan-design/configs/support-for-sql-server-versions#bkmk_SQLVersions).
    > -   De plus, si l’installation du nouveau site secondaire échoue avant de se terminer, mais achève l’installation de SQL Server Express 2012, vous devez mettre à jour cette instance de SQL Server Express pour que Configuration Manager puisse réessayer d’installer correctement le site secondaire.  

     **Utiliser une instance SQL Server existante**  

    -   **Nom de domaine complet de SQL Server** : vérifiez le nom de domaine complet de l’ordinateur exécutant SQL Server. Vous devez utiliser un serveur local exécutant SQL Server pour héberger la base de données de site secondaire, et vous ne pouvez pas modifier ce paramètre.  

    -   **Instance SQL Server**: spécifiez l’instance SQL Server à utiliser en tant que base de données du site secondaire. Laissez cette option vide pour utiliser l'instance par défaut.  

    -   **Nom de base de données de site ConfigMgr**: spécifiez le nom à utiliser pour la base de données du site secondaire.  

    -   **Port SQL Server Broker**: spécifiez le port SQL Server Service Broker (SSB) que SQL Server doit utiliser. Vous devez spécifier un port valide qu'aucun autre site ou service n'utilise, et qu'aucune restriction de pare-feu ne bloque.  

    > [!TIP]  
    > Pour obtenir la liste des versions de SQL Server prises en charge par System Center Configuration Manager, consultez [Versions SQL Server prises en charge](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

7.  Dans la page **Point de distribution** , configurez les paramètres du point de distribution à installer sur le serveur de site secondaire.  

     **Paramètres obligatoires :**  

    -   **Spécifiez la façon dont les appareils clients communiquent avec le point de distribution** : choisissez HTTP ou HTTPS.  

    -   **Créez un certificat auto-signé ou importez un certificat client PKI** : choisissez entre l’utilisation d’un certificat auto-signé (qui permet également d’autoriser les connexions anonymes de clients Configuration Manager à la bibliothèque de contenu) et l’importation d’un certificat à partir de votre infrastructure à clé publique (PKI).  

         Ce certificat sert à authentifier le point de distribution auprès d’un point de gestion avant que ce point de distribution envoie des messages d’état.  

         Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI pour Configuration Manager](https://technet.microsoft.com/library/gg699362.aspx).  

    **Paramètres facultatifs :**  

    -   **Installer et configurer IIS si requis par Configuration Manager** : sélectionnez ce paramètre pour permettre à Configuration Manager d’installer et de configurer Internet Information Services (IIS) sur le serveur si IIS n’est pas déjà installé. Les services Internet doivent être installés sur tous les points de distribution.  

        > [!NOTE]  
        > Bien que ce paramètre soit facultatif, IIS doit être installé sur le serveur pour qu’un point de distribution puisse être correctement installé.  

    -   **Activer et configurer BranchCache pour ce point de distribution**.  

    -   **Description**. Description conviviale du point de distribution pour faciliter son identification.  

    -   **Activer ce point de distribution pour le contenu préparé**.  

8.  Dans la page **Paramètres du lecteur** , spécifiez les paramètres du lecteur pour le point de distribution du site secondaire.  

     Vous pouvez configurer jusqu’à deux lecteurs de disque pour la bibliothèque de contenu et deux lecteurs de disque pour le partage de package. Toutefois, Configuration Manager peut utiliser des lecteurs supplémentaires quand les deux premiers atteignent la réserve d’espace disque configurée. La page **Paramètres du lecteur** permet de configurer la priorité des lecteurs de disque et la quantité d’espace disque libre restant sur chaque lecteur de disque.  

    -   **Réserve d’espace libre sur le lecteur (Mo)**  : la valeur que vous configurez pour ce paramètre détermine la quantité d’espace libre sur un lecteur avant que Configuration Manager choisisse un autre lecteur et poursuive le processus de copie sur ce lecteur. Les fichiers de contenu peuvent s'étendre sur plusieurs lecteurs.  

    -   **Emplacements du contenu**: Spécifiez les emplacements de contenu pour le partage de bibliothèque et de package de contenu. Configuration Manager copie le contenu à l’emplacement de contenu principal jusqu’à ce que la quantité d’espace libre atteigne la valeur spécifiée dans **Réserve d’espace libre sur le lecteur (Mo)**.

     Par défaut, les emplacements du contenu sont définis sur **Automatique**. L’emplacement de contenu principal est défini sur le lecteur de disque disposant le plus d’espace lors de l’installation. L’emplacement secondaire, quant à lui, est attribué au deuxième lecteur de disque disposant le plus d’espace. Quand le lecteur principal et le lecteur secondaire atteignent la réserve d’espace libre sur le lecteur, Configuration Manager sélectionne un autre lecteur disponible ayant le plus d’espace disque libre et poursuit le processus de copie.  

9. Sur la page **Validation du contenu** , indiquez si vous souhaitez valider l'intégrité des fichiers de contenu sur le point de distribution.  

    -   Quand vous activez la validation de contenu selon un calendrier, Configuration Manager démarre le processus à l’heure planifiée, et tout le contenu est vérifié sur le point de distribution.  

    -   Vous pouvez également configurer le paramètre **Priorité de la validation du contenu**.  

    -   Pour afficher les résultats du processus de validation du contenu, dans la console Configuration Manager, accédez à **Analyse** > **État de distribution** > **État du contenu**. Le contenu de chaque type de package (par exemple, application, package de mises à jour logicielles et image de démarrage) s'affiche.  

10. Dans la page **Groupes de limites**, gérez les groupes de limites auxquels ce point de distribution est affecté :  

    -   Lors d'un déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé au point de distribution pour l'utiliser comme emplacement source pour le contenu.  

    -   Vous pouvez sélectionner l'option **Autoriser l'emplacement source de secours pour le contenu** afin de permettre aux clients situés en-dehors de ces groupes de limites de revenir et d'utiliser le point de distribution comme emplacement source pour le contenu lorsque aucun point de distribution préféré n'est disponible.  

     Pour plus d’informations sur les points de distribution préférés, consultez la rubrique [Concepts fondamentaux de la gestion de contenu](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Dans la page **Résumé**, vérifiez les paramètres, puis choisissez **Suivant** pour installer le site secondaire. Quand l’Assistant affiche la page **Dernière étape**, vous pouvez fermer l’Assistant. L’installation du site secondaire se poursuit en arrière-plan.  


### <a name="bkmk_verify"></a> Pour vérifier l’état d’installation du site secondaire  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**.  

2.  Sélectionnez le serveur de site secondaire que vous installez, puis choisissez **Afficher l’état d’installation**.  

    > [!TIP]  
    > Quand vous installez plusieurs sites secondaires à la fois, l’Outil de vérification des prérequis s’exécute sur un seul site à la fois ; il doit terminer de vérifier un site avant de pouvoir passer au site suivant.  
