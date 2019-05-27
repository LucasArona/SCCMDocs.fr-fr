---
title: Assistant Installation
titleSuffix: Configuration Manager
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92c51158412b8bc9737c4851fc43dc2a7776488b
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501254"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Utilisez l’Assistant Installation pour installer des sites Configuration Manager.

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour installer un nouveau site Configuration Manager avec une interface utilisateur guidée, utilisez l’Assistant Installation de Configuration Manager (setup.exe). Cet Assistant prend en charge l’installation d’un site principal ou d’un site d’administration centrale. Il permet également de [mettre à niveau une installation d’évaluation](/sccm/core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install) de Configuration Manager pour obtenir une installation sous licence complète. Si vous ne voulez pas utiliser l’Assistant, vous pouvez utiliser à la place un [script d’installation](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites) et exécuter une installation en ligne de commande sans assistance.

Installez un site secondaire avec la console Configuration Manager. Les sites secondaires ne prennent pas en charge une installation en ligne de commande scriptée.



## <a name="bkmk_primary"></a> Installer un site d’administration centrale ou un site principal

Suivez la procédure ci-dessous pour installer un site d’administration centrale ou un site principal, ou pour mettre à niveau un site d’évaluation en un site Configuration Manager sous licence complète.   

Avant de commencer l’installation du site, vous devez être familiarisé avec le contenu des articles suivants :
- [Préparer l’installation des sites](/sccm/core/servers/deploy/install/prepare-to-install-sites)
- [Conditions préalables à l’installation d’un site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites)

Si vous installez un site d’administration centrale dans le cadre d’un scénario d’extension de site, lisez [Étendre un site principal autonome](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand) avant de suivre la procédure ci-dessous.

### <a name="bkmk_installpri"></a> Processus d’installation d’un site principal ou d’un site d’administration centrale

1. Sur l’ordinateur sur lequel vous voulez installer le site, exécutez `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` pour lancer **l’Assistant Installation de System Center Configuration Manager**.  

    > [!NOTE]  
    > Quand vous installez un site d’administration centrale pour étendre un site principal autonome, ou que vous installez un nouveau site principal enfant dans une hiérarchie existante, utilisez le support d’installation (fichiers sources) correspondant à la version du ou des sites existants. Si vous avez installé des mises à jour dans la console qui ont changé la version des sites installés précédemment, n’utilisez pas le support d’installation d’origine. Utilisez plutôt les fichiers sources du [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) d’un site mis à jour. Configuration Manager vous impose d’utiliser des fichiers sources qui correspondent à la version du site existant auquel votre nouveau site doit se connecter.  

2. Dans la page **Avant de commencer**, choisissez **Suivant**.  

3. Dans la page **Prise en main**, sélectionnez le type de site à installer :  

    - **Site d’administration centrale** comme premier site d’une nouvelle hiérarchie, ou lors du développement d’un site principal autonome :  

        Sélectionnez **Installer un site d’administration centrale Configuration Manager**.  

        Dans la suite de cette procédure, vous aurez le choix entre installer un site d’administration centrale comme premier site d’une nouvelle hiérarchie et installer un site d’administration centrale par extension d’un site principal autonome.  

    - **Site principal**, comme site principal autonome constituant le premier site d’une nouvelle hiérarchie, comme site principal enfant :  

        Sélectionnez **Installer un site principal Configuration Manager**.  

        > [!TIP]  
        > En règle générale, vous devez sélectionner l’option **Utiliser les options d’installation par défaut pour un site principal autonome** uniquement pour installer un site principal autonome dans un environnement de test. Lorsque cette option est sélectionnée, le programme d’installation effectue les actions suivantes :  
        > 
        > - configure automatiquement le site comme site principal autonome ;  
        > - utilise un chemin d’installation par défaut ;  
        > - utilise une installation locale de l’instance par défaut de SQL Server pour la base de données du site ;  
        > - installe un point de gestion et un point de distribution sur l’ordinateur serveur de site ;  
        > - configure le site en anglais et dans la langue d’affichage du système d’exploitation sur le serveur de site principal si elle correspond à l’une des langues prises en charge par Configuration Manager.  

4. Sur la page **Clé du produit** :  

    - Choisissez d’installer Configuration Manager en tant que version d’évaluation ou version sous licence.  

        - Si vous sélectionnez une version sous licence, entrez votre clé de produit, puis choisissez **Suivant**.  

        - Si vous sélectionnez une édition d’évaluation, choisissez **Suivant**. (Vous pouvez mettre à niveau une installation d’évaluation vers une installation complète ultérieurement.)  

    - Vous pouvez également spécifier la **date d’expiration de la Software Assurance** de votre contrat de licence pour vous en souvenir. Si vous n’entrez pas cette date pendant l’installation, vous pourrez la spécifier plus tard dans la console Configuration Manager.  

        > [!NOTE]   
        > Microsoft ne valide pas la date d’expiration entrée et ne l’utilise pas pour la validation de la licence. Elle peut vous servir de rappel. Cette date est utile, car Configuration Manager vérifie régulièrement les nouvelles mises à jour de logiciels proposées en ligne. Vous devez disposer d’une licence Software Assurance à jour pour pouvoir utiliser ces mises à jour supplémentaires.    

    Pour plus d’informations, consultez [Licences et branches](/sccm/core/understand/learn-more-editions).  

5. Dans la page **Termes du contrat de licence logiciel Microsoft** , lisez et acceptez les termes du contrat de licence.  

6. Dans la page **Licences requises** , lisez et acceptez les termes du contrat de licence pour les logiciels requis. Le programme d’installation télécharge et installe automatiquement les logiciels sur les systèmes ou les clients du site, si nécessaire. Acceptez toutes les conditions avant de passer à la page suivante.  

7. Sur la page **Téléchargements requis**, spécifiez si le programme d’installation doit télécharger les tout derniers fichiers redistribuables requis sur Internet ou utiliser d’anciens fichiers téléchargés :  

    - Si vous souhaitez que le programme d’installation télécharge les fichiers cette fois-ci, sélectionnez **Télécharger les fichiers requis**. Ensuite, spécifiez un emplacement de stockage.  

    - Si vous avez déjà téléchargé les fichiers à l’aide du [Téléchargeur d’installation](/sccm/core/servers/deploy/install/setup-downloader), sélectionnez **Utiliser des fichiers déjà téléchargés**. Ensuite, spécifiez le dossier de téléchargement.  

        > [!TIP]  
        > Si vous utilisez des fichiers téléchargés précédemment, vérifiez que le dossier de téléchargement indiqué contient la version la plus récente des fichiers.  

8. Dans la page **Sélection de la langue du serveur**, sélectionnez les langues disponibles pour la console Configuration Manager et les rapports. (L’anglais est sélectionné par défaut et ne peut pas être supprimé.) Pour plus d’informations, voir [Modules linguistiques](/sccm/core/servers/deploy/install/language-packs).  

9. Sur la page **Sélection de la langue client**, sélectionnez les langues accessibles aux ordinateurs clients. Précisez également si vous souhaitez activer toutes les langues client pour les clients d’appareil mobile. (L’anglais est sélectionné par défaut et ne peut pas être supprimé.)  

    > [!IMPORTANT]  
    > Si vous utilisez un site d’administration centrale, veillez y à inclure toutes les langues client configurées au niveau de chaque site principal enfant. Les clients qui effectuent l’installation à partir d’un point de distribution ont accès aux langues client issues du site de niveau supérieur, tandis que ceux qui utilisent un point de gestion ont accès aux langues client provenant du site principal qui lui a été attribué.  

10. Sur la page **Paramètres d’installation et du site**, spécifiez les paramètres suivants pour le nouveau site en cours d’installation :  

    - **Code de site** : [chaque code de site d’une hiérarchie doit être unique](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_sitecodes). Utilisez trois caractères alphanumériques : de A à Z et de 0 à 9. Le code de site étant utilisé dans les noms de dossiers, évitez les noms réservés à Windows, à savoir :    
        - AUX  
        - CON    
        - NUL    
        - PRN    
        - SMS  

        > [!NOTE]  
        > Le programme d’installation ne vérifie pas si le code de site que vous spécifiez est déjà utilisé ou s’il s’agit d’un nom réservé.  

    - **Nom du site** : Chaque site doit posséder un nom convivial pour faciliter son identification.  

    - **Dossier d’installation** : chemin de l’installation de Configuration Manager. Vous ne pouvez pas modifier cet emplacement après l’installation du site. Ce chemin ne doit pas contenir de caractères Unicode, ni d’espaces en fin de chaîne.  

11. Dans la page **Installation de site**, utilisez l’option suivante correspondant à votre scénario :  

    - **J’installe un site d’administration centrale :**  

        Dans la page **Installation du site d’administration centrale**, sélectionnez **Installer en tant que premier site d’une nouvelle hiérarchie**, puis choisissez sur **Suivant** pour continuer.  

    - **J’étends un site principal autonome dans une hiérarchie comportant un site d’administration centrale :**  

        Sur la page **Installation du site d’administration centrale**, sélectionnez **Étendre un site principal autonome existant dans une hiérarchie**. Ensuite, spécifiez le nom de domaine complet du serveur de site principal autonome, puis choisissez **Suivant** pour continuer.  

        Le support que vous utilisez pour installer le nouveau site d’administration centrale doit correspondre à la version du site principal.  

    - **J’installe un site principal autonome :**  

        Dans la page **Installation du site principal**, sélectionnez**Installer le site principal en tant que site autonome**, puis choisissez **Suivant**.  

    - **J’installe un site principal enfant :**  

        Sur la page **Installation du site principal**, sélectionnez **Joindre le site principal à une hiérarchie existante**. Ensuite, spécifiez le nom de domaine complet du site d’administration centrale, puis choisissez **Suivant**.  

12. Dans la page **Informations sur la base de données**, spécifiez les informations suivantes :  

    - **Nom du serveur SQL Server (FQDN) :** par défaut, cette valeur correspond à l’ordinateur serveur de site.  

        Si vous utilisez un port personnalisé, ajoutez ce port au nom FQDN du serveur SQL Server. Faites suivre le nom FQDN du serveur SQL Server d’une virgule, puis du numéro de port. Par exemple, pour le serveur *SQLServer1.fabrikam.com*, spécifiez ainsi le port *1551* : `SQLServer1.fabrikam.com,1551`.  

    - **Nom de l’instance :** par défaut, cette valeur est vide. L’instance par défaut de SQL est utilisée sur l’ordinateur serveur de site.  

    - **Nom de la base de données** : par défaut, cette valeur est définie sur `CM_<Sitecode>`. Vous pouvez la personnaliser.  

    - **Port Service Broker :** la valeur prédéfinie indique d’utiliser le port SQL Server Service Broker (SSB) par défaut (4022). SQL l’utilise communiquer directement avec des bases de données d’autres sites.  

13. Sur la deuxième page **Informations sur la base de données**, vous pouvez spécifier des emplacements personnalisés pour le fichier de données SQL Server et le fichier journal SQL Server pour la base de données du site :  

    - Par défaut, elle utilise les emplacements de fichier par défaut pour SQL Server.  

    - Avec un cluster SQL Server, il n’est pas possible de spécifier des emplacements de fichiers personnalisés.  

    - Le vérificateur des prérequis n’effectue pas de contrôle de l’espace disque disponible aux emplacements de fichiers personnalisés.  

14. Dans la page **Paramètres du fournisseur SMS** , spécifiez le nom de domaine complet (FQDN) du serveur sur lequel vous souhaitez installer le fournisseur SMS.  

    - Par défaut, elle spécifie le serveur de site.  

    - Une fois le site installé, vous pouvez configurer d’autres fournisseurs SMS. Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

15. Dans la page **Paramètres de communication du client** , choisissez de configurer tous les systèmes de site pour accepter uniquement les communications HTTPS en provenance de clients ou de configurer la méthode de communication pour chaque rôle de système de site.  

    Quand vous sélectionnez **Tous les rôles de système de site acceptent uniquement les communications HTTPS depuis les clients**, l’ordinateur client doit avoir un certificat PKI valide pour l’authentification du client. Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    > [!NOTE]  
    > Effectuez cette étape uniquement si vous installez un site principal. Si vous installez un site d’administration centrale, ignorez cette étape.  

16. Sur la page **Rôles système de site** , choisissez d'installer un point de gestion ou un point de distribution. Pour chaque rôle de votre choisissez de faire installer par le programme d’installation :  

    - Entrez le **FQDN** du serveur qui hébergera le rôle. Ensuite, choisissez la méthode de connexion client que gèrera le serveur : HTTP ou HTTPS.  

    - Si vous avez sélectionné **Tous les rôles de système de site acceptent uniquement les communications HTTPS issues des clients** sur la page précédente, les paramètres de connexion client sont configurés automatiquement pour HTTPS. Ce paramètre n’est pas modifiable, à moins de revenir à la page précédente.  

    > [!NOTE]  
    > Effectuez cette étape uniquement si vous installez un site principal. Si vous installez un site d’administration centrale, ignorez cette étape.  

    > [!NOTE]  
    > Pour installer des rôles de système de site, le programme d’installation utilise le **compte d’installation du système de site**. Par défaut, il utilise le compte d’ordinateur du site principal. Ce compte doit avoir des autorisations d’administrateur local sur un ordinateur distant pour installer le rôle de système de site. Si ce compte ne possède pas les autorisations requises, désélectionnez les rôles de système de site et installez-les ultérieurement à partir de la console Configuration Manager, après avoir configuré des comptes supplémentaires à utiliser en tant que comptes d’installation du système de site. Pour plus d’informations, voir [Comptes](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

17. Dans la page **Données d’utilisation**, consultez les informations relatives aux données que Microsoft collecte, puis choisissez **Suivant**. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

18. La page **Configuration du point de connexion de service** n’est disponible que dans les scénarios suivants :  

    - quand vous installez un site principal autonome ;  

    - quand vous installez un site d’administration centrale.  

    > [!NOTE]  
    > Si vous installez un site principal enfant, ignorez cette étape.  

     Si vous installez un site d’administration centrale dans le cadre d’un scénario d’extension de site et que ce rôle est déjà installé sur le site principal autonome, commencez par désinstaller ce rôle du site principal autonome. Une hiérarchie n’admet qu’une seule instance de ce rôle, et seulement sur le site de niveau supérieur.  

     Après avoir sélectionné une configuration pour le **point de connexion de service**, choisissez **Suivant**. Une fois l’installation terminée, cette configuration sera modifiable dans la console Configuration Manager. Pour plus d’informations, consultez [À propos du point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point).  

19. Dans la page **Résumé des paramètres**, vérifiez le paramètre que vous avez sélectionné. Quand vous êtes prêt, choisissez **Suivant** pour démarrer l’Outil de vérification des prérequis.  

20. La page **Vérification des prérequis de l’installation** liste tous les problèmes identifiables par le vérificateur.  

    - Quand l’outil de vérification de la configuration requise détecte un problème, choisissez un élément affiché dans la liste pour obtenir des détails sur la façon de résoudre le problème.  

    - Pour pouvoir continuer à installer le site, résolvez les éléments en **Échec**. Les éléments présentant l’état **Avertissement** doivent de préférence être également résolus, mais ils ne bloquent pas l’installation du site.  

    - Après avoir résolu les problèmes, choisissez **Vérifier** pour réexécuter l’Outil de vérification des prérequis.  

        Dès lors que le vérificateur des prérequis s’exécute sans plus rencontrer d’état **Échec**, vous pouvez choisir **Commencer l’installation** pour lancer l’installation du site.  

    > [!TIP]  
    > Outre les commentaires fournis par l’Assistant, vous trouverez des informations complémentaires sur les problèmes liés aux prérequis dans le fichier **ConfigMgrPrereq.log**. Il se trouve à la racine du lecteur système de l’ordinateur sur lequel le site est en cours d’installation. Pour plus d’informations, voir [Liste des vérifications des prérequis](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

21. Dans la page **Installation** , le programme d’installation affiche l’état de l’installation. Une fois l’installation du serveur de site principal terminée, vous pouvez **Fermer** l’Assistant Installation. Quand vous fermez l’Assistant, l’installation et les configurations de site initiales continuent en arrière-plan.  

    - Vous pouvez connecter une console Configuration Manager au site avant la fin de l’installation. Cette console est connectée en lecture seule, ce qui signifie qu’elle permet l’affichage des objets et des paramètres, mais pas leur modification.  

    - Vous devez attendre la fin de l’installation pour pouvoir connecter une console permettant de modifier les objets et paramètres.  



## <a name="bkmk_expand"></a> Développer un site principal autonome

Après avoir installé un site principal autonome comme premier site, vous pouvez développer ce site ultérieurement dans une plus grande hiérarchie en installant un site d’administration centrale.   

Quand vous développez un site principal autonome, vous installez un nouveau site d’administration centrale qui utilise la base de données du site principal autonome existant comme référence. Après l’installation du nouveau site d’administration centrale, le site principal autonome est utilisé comme site principal enfant.

- Un site principal autonome ne peut être étendu que dans une nouvelle hiérarchie.  

- Seul un site principal autonome peut être étendu dans une hiérarchie donnée. Vous ne pouvez pas utiliser cette option pour joindre d’autres sites principaux autonomes dans la même hiérarchie. Utilisez plutôt l’Assistant Migration pour migrer les données d’une hiérarchie à l’autre. Pour plus d’informations, consultez [Faire migrer des données entre des hiérarchies](/sccm/core/migration/migrate-data-between-hierarchies).  

- Après avoir étendu un site autonome dans une hiérarchie comportant un site d’administration centrale, vous pouvez ajouter des sites principaux enfants.  

- Pour supprimer un site principal d’une hiérarchie comportant un site d’administration centrale, commencez par désinstaller le site principal.  


Pour étendre le site, utilisez l’Assistant Installation de Configuration Manager pour installer un nouveau site d’administration centrale, en prenant les précautions suivantes :  

- Installez le site d’administration centrale en utilisant la même version de Configuration Manager que celle du site principal autonome.  

- Sur la page **Bien démarrer** de l’Assistant Installation, sélectionnez l’option permettant d’installer un site d’administration centrale. À un stade ultérieur, le programme d’installation vous permettra de choisir l’option de développement d’un site principal autonome existant.  

- Quand vous configurez la page **Sélection de la langue client** pour le nouveau site d’administration centrale, sélectionnez les langues client configurées pour le site principal autonome que vous étendez.  

- Sur la page **Installation du site**, sélectionnez l’option permettant d’étendre le site principal autonome.  


Pour étendre un site principal autonome, commencez par consulter les [prérequis pour étendre un site](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#bkmk_expand). Ensuite, suivez la procédure [Installer un site principal ou un site d’administration centrale](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_installpri) décrite précédemment dans cet article.




## <a name="bkmk_secondary"></a> Installer un site secondaire

Utilisez la console Configuration Manager pour installer un site secondaire.  

- Si la console utilisée n’est pas connectée au site principal qui sera le site parent du nouveau site secondaire, la commande d’installation du site est répliquée sur le site principal concerné.  

- Avant de commencer l’installation du site, vérifiez que votre compte d’utilisateur dispose des autorisations requises. Assurez-vous également que le serveur qui hébergera le nouveau site secondaire remplit tous les prérequis pour servir de serveur de site secondaire.  

- Quand vous installez le site secondaire, Configuration Manager configure le nouveau site pour utiliser les ports de communication client configurés sur le site principal parent.  


### <a name="bkmk_installsecondary"></a> Processus d’installation d’un site secondaire  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site qui sera le site principal parent du nouveau site secondaire.  

2. Pour lancer **l’Assistant Création de site secondaire**, choisissez **Créer un site secondaire** dans le ruban.  

3. Sur la page **Avant de commencer**, vérifiez que le site principal présenté est bien le site à utiliser comme parent du nouveau site secondaire. Ensuite, choisissez **Suivant**.  

4. Sur la page **Général** , spécifiez les paramètres suivants :  

    - **Code de site** : chaque code de site d’une hiérarchie doit être unique. Utilisez trois caractères alphanumériques : de A à Z et de 0 à 9. Le code de site étant utilisé dans les noms de dossiers, évitez les noms réservés à Windows, à savoir :  

        - AUX    
        - CON    
        - NUL    
        - PRN  
        - SMS  

    > [!NOTE]  
    > Le programme d’installation ne vérifie pas si le code de site que vous spécifiez est déjà utilisé ou s’il s’agit d’un nom réservé.  

    - **Nom de serveur de site** : nom de domaine complet du serveur sur lequel le nouveau site secondaire sera installé.  

    - **Nom du site** : Chaque site doit posséder un nom convivial pour faciliter son identification.  

    - **Dossier d’installation** : chemin de l’installation de Configuration Manager. Vous ne pouvez pas modifier cet emplacement après l’installation du site. Ce chemin ne doit pas contenir de caractères Unicode, ni d’espaces en fin de chaîne.  

    > [!IMPORTANT]  
    > Une fois que vous avez spécifié les détails demandés sur cette page, vous pouvez choisir **Résumé** pour accéder directement à la page **Résumé** de l’Assistant. Cette action a pour effet d’utiliser les paramètres par défaut pour les autres options du site secondaire.  
    > 
    > - N’utilisez-la que si vous connaissez les paramètres par défaut de cet Assistant et que vous souhaitez les utiliser.  
    > - Avec les paramètres par défaut, les groupes de limites ne sont pas associés au point de distribution. Tant que vous n’avez pas configuré de groupes de limites incluant le serveur de site secondaire, les clients n’utilisent pas le point de distribution installé sur ce site secondaire comme emplacement source de contenu.  

5. Dans la page **Fichiers sources d’installation** , choisissez la façon dont l’ordinateur du site secondaire obtient les fichiers sources pour l’installation du site.  

    Si vous utilisez les fichiers sources CD.Latest partagés sur le réseau ou copiés localement sur le serveur de site secondaire cible :  

    - **Version 1802 ou antérieure**

        - L’emplacement du fichier source CD.Latest comporte un dossier nommé **Redist**. Déplacez ce dossier **Redist** pour en faire un sous-dossier du dossier **SMSSETUP**.  

            > [!Note]  
            > S’il se produit des erreurs d’incompatibilité de hachage pendant l’installation, mettez à jour le dossier **Redist**. Utilisez le [Téléchargeur d’installation](/sccm/core/servers/deploy/install/setup-downloader) pour obtenir la dernière version des fichiers. Copiez également tous les fichiers qui provoquent une erreur d’incompatibilité de hachage du dossier **Redist** mis à jour vers le dossier **SMSSETUP\BIN\X64**. 

    - **Version 1806 ou ultérieure**<!-- SCCMDocs-pr issue 3164 -->

        - L’emplacement du fichier source CD.Latest comporte un dossier nommé **Redist**. Déplacez ce dossier **Redist** pour en faire un sous-dossier du dossier **SMSSETUP**.  

        - Copiez les fichiers suivants du dossier **Redist** vers le dossier **SMSSETUP\BIN\X64** :   
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Si certains fichiers du dossier **Redist** ne sont pas disponibles, le programme d’installation ne peut pas installer le site secondaire.  

    - Le compte d’ordinateur du serveur de site secondaire doit disposer d’autorisations d’accès en **Lecture** au dossier et au partage de fichiers sources.  

6. Dans la page **Paramètres SQL Server** , spécifiez la version de SQL Server à utiliser, puis configurez les paramètres associés.  

    > [!NOTE]  
    > Le programme d’installation ne valide pas les informations que vous entrez dans cette page avant de démarrer l’installation. Avant de continuer, vérifiez ces paramètres.  

    - **Installer et configurer une copie locale de SQL Express sur l'ordinateur de site secondaire**  

        - **Port de service de SQL Server** : Spécifiez le port de service de SQL Server pour SQL Server Express à utiliser. Le port de service est généralement configuré pour utiliser le port TCP 1433, mais vous pouvez configurer un autre port.  

        - **Port SQL Server Broker** : Spécifiez le port SQL Server Service Broker (SSB) pour SQL Server Express à utiliser. Le Service Broker est généralement configuré pour utiliser le port TCP 4022, mais vous pouvez configurer un port différent. Spécifiez un port valide qui ne soit ni utilisé par un autre site ou service, ni bloqué par des restrictions de pare-feu.  

    - **Utiliser une instance SQL Server existante**  

        - **Nom de domaine complet de SQL Server** : Vérifiez le nom de domaine complet de l’ordinateur exécutant SQL Server. Vous devez utiliser un serveur local exécutant SQL Server pour héberger la base de données de site secondaire, et vous ne pouvez pas modifier ce paramètre.  

        - **Instance SQL Server** : Spécifiez l’instance SQL Server à utiliser en tant que base de données du site secondaire. Laissez cette option vide pour utiliser l'instance par défaut.  

        - **Nom de base de données de site ConfigMgr** : Spécifiez le nom à utiliser pour la base de données de site secondaire.  

        - **Port SQL Server Broker** : Spécifiez le port SQL Server Service Broker (SSB) que SQL Server doit utiliser. Spécifiez un port valide qui ne soit ni utilisé par un autre site ou service, ni bloqué par des restrictions de pare-feu.  

    > [!TIP]  
    > Pour connaître la liste des versions de SQL Server prises en charge par System Center Configuration Manager, voir [Versions de SQL Server prises en charge](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

7. Dans la page **Point de distribution** , configurez les paramètres du point de distribution à installer sur le serveur de site secondaire.  

    - **Paramètres obligatoires :**  

        - **Configurez la manière dont les appareils clients communiquent avec le point de distribution** : Choisissez HTTP ou HTTPS.  

        - **Créez un certificat auto-signé ou importez un certificat client PKI** : Choisissez entre utiliser un certificat auto-signé et importer un certificat à partir de votre infrastructure PKI. Un certificat auto-signé permet également d’autoriser les connexions anonymes de clients Configuration Manager à la bibliothèque de contenu. Ce certificat sert à authentifier le point de distribution auprès d’un point de gestion avant que ce point de distribution envoie des messages d’état. Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Paramètres facultatifs :**  

        - **Installer et configurer IIS si requis par Configuration Manager** : sélectionnez ce paramètre pour permettre à Configuration Manager d’installer et de configurer Internet Information Services (IIS) sur le serveur s’ils ne sont pas déjà installés. IIS est requis sur tous les points de distribution.  

            > [!NOTE]  
            > Bien que ce paramètre soit facultatif, IIS doit être installé sur le serveur pour qu’un point de distribution puisse être correctement installé.  

        - **Activer et configurer BranchCache pour ce point de distribution**  

        - **Description** : description conviviale du point de distribution facilitant son identification.  

        - **Activer ce point de distribution pour le contenu préparé**  

8. Dans la page **Paramètres du lecteur** , spécifiez les paramètres du lecteur pour le point de distribution du site secondaire.  

    Vous pouvez configurer jusqu’à deux lecteurs de disque pour la bibliothèque de contenu et deux lecteurs de disque pour le partage de package. Toutefois, Configuration Manager peut utiliser des lecteurs supplémentaires quand les deux premiers atteignent la réserve d’espace disque configurée. La page **Paramètres du lecteur** permet de configurer la priorité des lecteurs de disque et la quantité d’espace disque libre restant sur chaque lecteur de disque.  

    - **Réserve d’espace libre sur le lecteur (Mo)** : La valeur que vous configurez pour ce paramètre détermine la quantité d’espace libre sur un lecteur avant que Configuration Manager choisisse un autre lecteur et poursuive le processus de copie sur ce lecteur. Les fichiers de contenu peuvent s'étendre sur plusieurs lecteurs.  

    - **Emplacements du contenu** : Spécifiez les emplacements de contenu pour la bibliothèque de contenu et le partage de package. Configuration Manager copie le contenu à l’emplacement de contenu principal jusqu’à ce que la quantité d’espace libre atteigne la valeur spécifiée pour **Réserve d’espace sur le lecteur (Mo)** .  

    Par défaut, les emplacements du contenu sont définis sur **Automatique**. L’emplacement de contenu principal est défini sur le lecteur de disque disposant le plus d’espace lors de l’installation. L’emplacement secondaire, quant à lui, est attribué au deuxième lecteur de disque disposant le plus d’espace. Quand le lecteur principal et le lecteur secondaire atteignent la réserve d’espace libre sur le lecteur, Configuration Manager sélectionne un autre lecteur disponible ayant le plus d’espace disque libre et poursuit le processus de copie.  

9. Sur la page **Validation du contenu** , indiquez si vous souhaitez valider l'intégrité des fichiers de contenu sur le point de distribution.  

    - Quand vous activez la validation de contenu selon une planification, Configuration Manager démarre le processus à l’heure planifiée. Tout le contenu du point de distribution est vérifié.  

    - Vous pouvez également configurer le paramètre **Priorité de la validation du contenu**.  

    - Pour afficher les résultats du processus de validation du contenu, accédez à l’espace de travail **Monitoring** dans la console Configuration Manager, développez **État de distribution** et sélectionnez le nœud **État du contenu**. Le contenu apparaît pour chaque type de package : applications, mises à jour de logiciels et images de démarrage.  

10. Dans la page **Groupes de limites**, gérez les groupes de limites auxquels ce point de distribution est affecté :  

    - Lors d’un déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé au point de distribution pour pouvoir l’utiliser comme emplacement source du contenu.  

    - Vous pouvez sélectionner l'option **Autoriser l'emplacement source de secours pour le contenu** afin de permettre aux clients situés en-dehors de ces groupes de limites de revenir et d'utiliser le point de distribution comme emplacement source pour le contenu lorsque aucun point de distribution préféré n'est disponible.  

        Pour plus d’informations, voir [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management).  

11. Dans la page **Résumé**, vérifiez les paramètres, puis choisissez **Suivant** pour installer le site secondaire. Quand l’Assistant affiche la page **Dernière étape**, vous pouvez fermer l’Assistant. L’installation du site secondaire se poursuit en arrière-plan.  


### <a name="bkmk_verify"></a> Vérifier l’état d’installation du site secondaire  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Sélectionnez le site secondaire en cours d’installation, puis choisissez **Afficher l’état d’installation** dans le ruban.  

    > [!TIP]  
    > En cas d’installation de plusieurs sites secondaires, le vérificateur des prérequis s’exécute sur un seul à la fois. Il doit en terminer un pour pouvoir commencer à vérifier le suivant.  

