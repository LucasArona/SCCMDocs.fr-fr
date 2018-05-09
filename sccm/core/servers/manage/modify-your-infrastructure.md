---
title: Modifier l’infrastructure
titleSuffix: Configuration Manager
description: Découvrez comment apporter des modifications ou prendre des mesures qui affecteront l’infrastructure Configuration Manager que vous avez déployée.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7f798fdb1183b852bded92711cc5f489666f4f2a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>Modifier votre infrastructure System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé un ou plusieurs sites, vous pouvez être amené à modifier les configurations ou à effectuer des actions qui affectent l’infrastructure que vous avez déployée.  


##  <a name="BKMK_ManageSMSprovider"></a> Gérer le fournisseur SMS  
 Le fournisseur SMS (fichier de bibliothèque de liens dynamiques smsprov.dll) procure le point de contact administratif pour une ou plusieurs consoles Configuration Manager. Lorsque vous installez plusieurs fournisseurs SMS, vous pouvez fournir une redondance pour l'administration de votre site et hiérarchie par des points de contact.  

 Sur chaque site Configuration Manager, vous pouvez réexécuter le programme d’installation pour :  

-   ajouter une instance du fournisseur SMS (chaque instance supplémentaire du fournisseur SMS doit se trouver sur un ordinateur distinct) ;  

-   supprimer une instance du fournisseur SMS (pour supprimer le dernier fournisseur SMS pour un site, vous devez désinstaller le site).  

 Vous pouvez surveiller le processus d'installation ou de suppression du fournisseur SMS en consultant le fichier **ConfigMgrSetup.log** dans le dossier racine du serveur du site sur lequel vous exécutez le programme d'installation.  

 Avant de modifier le fournisseur SMS sur un site, familiarisez-vous avec les informations contenues dans [Planifier le fournisseur SMS pour System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>Pour gérer la configuration du fournisseur SMS pour un site  

1.  Exécutez **Installation de Configuration Manager** à partir de **&lt;dossier_installation_du_site_Configuration_Manager\>\BIN\X64\setup.exe**.  

2.  Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.  

3.  Sur la page **Maintenance de site** , sélectionnez **Modifier la configuration du fournisseur SMS**, puis cliquez sur **Suivant**.  

4.  Sur la page **Gérer les fournisseurs SMS** , sélectionnez l'une des options suivantes et effectuez toutes les étapes de l'Assistant comme indiqué :  

    -   Pour ajouter un fournisseur SMS supplémentaires sur ce site :  

         Sélectionnez **Ajouter un nouveau fournisseur SMS**, spécifiez le nom de domaine complet d'un ordinateur qui hébergera le fournisseur SMS mais qui n'héberge aucun fournisseur SMS actuellement, puis cliquez sur **Suivant**.  

    -   Pour supprimer un fournisseur SMS d'un serveur :  

         Sélectionnez **Désinstaller le fournisseur SMS spécifié**, sélectionnez le nom de l'ordinateur dont vous souhaitez supprimer le fournisseur SMS, cliquez sur **Suivant**, puis confirmez l'action.  

        > [!TIP]  
        >  Pour déplacer le fournisseur SMS entre deux ordinateurs, vous devez installer le fournisseur SMS sur le nouvel ordinateur et supprimer le fournisseur SMS de l'emplacement d'origine. Il n'existe aucune option spéciale pour déplacer le fournisseur SMS entre les ordinateurs en un seul processus.  

 Une fois toutes les étapes de l'Assistant Installation effectuées, la configuration du fournisseur SMS est terminée. Dans l'onglet **Général** dans la boîte de dialogue **Propriétés** du site, vous pouvez vérifier les ordinateurs disposant d'un fournisseur SMS installé pour un site.  

##  <a name="bkmk_Console"></a> Gérer la console Configuration Manager  
 Voici les tâches que vous pouvez effectuer pour gérer la console Configuration Manager :  

-   **Modifier la langue qui s’affiche dans la console Configuration Manager** – Pour modifier les langues installées, consultez [Gérer la langue de la console Configuration Manager](#BKMK_ManageConsoleLanguages) dans cette rubrique.  

-   **Installer d’autres consoles** – Pour installer des consoles supplémentaires, consultez [Installer des consoles System Center Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).  

-   **Configurer DCOM** – Pour configurer une autorisation DCOM pour permettre aux consoles distantes du serveur de site de se connecter, consultez [Configurer les autorisations DCOM pour les consoles Configuration Manager distantes](#BKMK_ConfigDCOMforRemoteConsole) dans cette rubrique.  

-   **Modifier les autorisations pour limiter ce que voient les utilisateurs administratifs dans la console** – Pour modifier les autorisations d’administration qui limitent ce que les utilisateurs peuvent voir et faire dans la console, consultez [Modifier l’étendue administrative d’un utilisateur administratif](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser).     

###  <a name="BKMK_ManageConsoleLanguages"></a> Gérer la langue de la console Configuration Manager  
 Lors de l’installation du serveur de site, les fichiers d’installation de la console Configuration Manager et les modules linguistiques pris en charge pour le site sont copiés dans le sous-dossier **&lt;chemin_installation_Configuration_Manager\>\Tools\ConsoleSetup** du serveur de site.  

-   Quand vous démarrez l’installation de la console Configuration Manager à partir de ce dossier sur le serveur de site, les fichiers de la console Configuration Manager et du module linguistique pris en charge sont copiés sur l’ordinateur.  

-   Si le module linguistique correspondant au paramètre de langue défini sur l’ordinateur est disponible, la console Configuration Manager s’ouvre dans cette langue.  

-   Si le module linguistique associé n’est pas disponible pour la console Configuration Manager, la console s’ouvre en anglais.  

Par exemple, considérez un scénario dans lequel vous installez la console Configuration Manager à partir d’un serveur de site prenant en charge l’anglais, l’allemand et le français. Si vous ouvrez la console Configuration Manager sur un ordinateur avec un paramètre de langue configuré pour le français, la console s’ouvre en français. Par contre, si vous ouvrez la console Configuration Manager sur un ordinateur avec un paramètre de langue configuré pour le japonais, la console s’ouvre en anglais, car le module linguistique japonais n’est pas disponible.  

 Chaque fois que la console Configuration Manager s’ouvre, les paramètres configurés pour la langue de l’ordinateur sont déterminés, la disponibilité d’un module linguistique associé pour la console Configuration Manager est vérifiée et le module linguistique correspondant est utilisé. Si vous voulez ouvrir la console Configuration Manager en anglais sans tenir compte des paramètres de langue configurés sur l’ordinateur, vous devez supprimer ou renommer manuellement les fichiers du module linguistique sur l’ordinateur.  

 Utilisez les procédures suivantes pour démarrer la console Configuration Manager en anglais quels que soient les paramètres régionaux configurés sur l’ordinateur.  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Pour installer une version en anglais uniquement de la console Configuration Manager sur des ordinateurs  

1.  Dans l’Explorateur Windows, accédez à **&lt;chemin_installation_Configuration_Manager\>\Tools\ConsoleSetup\LanguagePack**.  

2.  Renommez les fichiers **.msp** et **.mst** . Par exemple, vous pouvez remplacer **&lt;nom_fichier\>.MSP** par **&lt;nom_fichier\>.MSP.disabled**.  

3.  Installez la console Configuration Manager sur l’ordinateur.  

    > [!IMPORTANT]  
    >  Une fois les nouvelles langues de serveur configurées pour le serveur de site, les fichiers .msp et .mst sont recopiés dans le dossier **LanguagePack**. Vous devez répéter cette procédure pour installer de nouvelles consoles Configuration Manager en anglais uniquement.  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Pour désactiver temporairement la langue d'une console sur une installation existante de la console Configuration Manager  

1.  Sur l’ordinateur qui exécute la console Configuration Manager, fermez la console Configuration Manager.  

2.  Dans l’Explorateur Windows, accédez à &lt;*chemin_installation_console*>\Bin\ sur l’ordinateur de la console Configuration Manager.  

3.  Renommez le dossier de langue approprié selon la langue configurée sur l'ordinateur. Par exemple, si les paramètres de langue pour l'ordinateur sont configurés pour l'allemand, renommez le dossier **de** , **de.disabled**.  

4.  Pour ouvrir la console Configuration Manager dans la langue configurée pour l’ordinateur, rétablissez le nom d’origine du dossier. Par exemple, renommez **de.disabled** , **de**.  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configurer les autorisations DCOM pour les consoles Configuration Manager distantes  
 Le compte d’utilisateur exécutant la console Configuration Manager exige des autorisations pour accéder à la base de données de site par le biais du fournisseur SMS. Toutefois, chaque utilisateur administratif qui utilise une console Configuration Manager distante doit posséder également des autorisations DCOM d’**activation à distance** sur :  

-   L'ordinateur de serveur de site ;  

-   chaque ordinateur qui héberge une instance du fournisseur SMS.  

 Le groupe de sécurité nommé **Administrateurs SMS** accorde des autorisations d’accès au fournisseur SMS sur un ordinateur et permet également d’accorder les autorisations DCOM requises. (Quand le fournisseur SMS s’exécute sur un serveur membre, il s’agit d’un groupe local dans l’ordinateur. Quand le fournisseur SMS s’exécute sur un contrôleur de domaine, il s’agit d’un groupe de domaine local.)  

> [!IMPORTANT]  
>  La console Configuration Manager utilise WMI (Windows Management Instrumentation) pour se connecter au fournisseur SMS, et WMI utilise DCOM en interne. Par conséquent, lorsque la console Configuration Manager est exécutée sur un ordinateur autre que le fournisseur SMS, Configuration Manager exige des autorisations pour activer un serveur DCOM sur l’ordinateur fournisseur SMS. Par défaut, l'activation à distance est accordée uniquement aux membres du groupe Administrateurs intégré. Accorder une autorisation d'activation à distance au groupe Administrateurs SMS reviendrait à permettre à un membre de ce groupe d'effectuer des attaques DCOM à l'encontre de l'ordinateur du fournisseur SMS. La surface d'attaque de l'ordinateur s'en trouverait également augmentée. Vous pouvez réduire l'étendue de cette menace en surveillant attentivement les membres du groupe Administrateurs SMS.  

 Utilisez la procédure ci-après pour configurer chaque site d’administration centrale, serveur de site principal et ordinateur sur lequel est installé le fournisseur SMS pour accorder l’accès à distance à la console Configuration Manager aux utilisateurs administratifs.  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Pour configurer des autorisations DCOM pour les connexions à distance à la console Configuration Manager  

1.  Ouvrez  **Services de composants** en exécutant **Dcomcnfg.exe**.  

2.  Dans **Services de composants**, cliquez sur **Racine de la console** >  **Services de composants** > **Ordinateurs**, puis cliquez sur **Poste de travail**. Dans le menu **Action** , cliquez sur **Propriétés**.  

3.  Dans la boîte de dialogue **Propriétés du poste de travail** , sous l'onglet **Sécurité COM** , dans la section **Autorisations d'exécution et d'activation** , cliquez sur **Modifier les limites**.  

4.  Dans la boîte de dialogue **Autorisations d'exécution et d'activation** , cliquez sur **Ajouter**.  

5.  Dans la boîte de dialogue **Sélectionner Utilisateur, ordinateurs, comptes de service ou groupes** , dans la zone **Entrez les noms d'objets à sélectionner (exemples)** , tapez **SMS Admins**, puis cliquez sur **OK**.  

    > [!NOTE]  
    >  Vous devrez peut-être modifier la valeur du paramètre de **À partir de cet emplacement** pour localiser le groupe Administrateurs SMS. Lorsque le fournisseur SMS s'exécute sur un serveur membre, il s'agit d'un groupe local dans l'ordinateur. Lorsque le fournisseur SMS s'exécute sur un contrôleur de domaine, il s'agit d'un groupe de domaine local.  

6.  Dans la section **Autorisations pour les administrateurs SMS** , sélectionnez la case à cocher **Activation à distance** pour autoriser l'activation à distance.  

7.  Cliquez sur **OK** , cliquez de nouveau sur **OK** , puis fermez **Gestion de l'ordinateur**. Votre ordinateur est maintenant configuré pour autoriser l’accès à distance à la console Configuration Manager aux membres du groupe Administrateurs SMS.  

 Répétez cette procédure sur chaque ordinateur de fournisseur SMS pouvant prendre en charge les consoles Configuration Manager à distance.  

##  <a name="bkmk_dbconfig"></a> Modifier la configuration de base de données de site  
 Après avoir installé un site, vous pouvez modifier la configuration de la base de données de site et le serveur de base de données de site en exécutant l'installation sur un serveur de site d'administration centrale ou un serveur de site principal. Vous pouvez déplacer la base de données de site vers une nouvelle instance de SQL Server sur le même ordinateur ou vers un autre ordinateur exécutant une version de SQL Server prise en charge. Ces modifications et les modifications associées ne sont pas prises en charge pour la configuration de base de données sur des sites secondaires.  

 Pour plus d’informations sur les limites de prise en charge, consultez [Support policy for manual database changes in a Configuration Manager environment](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  Lorsque vous modifiez la configuration de la base de données pour un site, Configuration Manager redémarre ou réinstalle les services Configuration Manager sur le serveur de site et les serveurs de système de site distants qui communiquent avec la base de données.  

**Pour modifier la configuration de la base de données**, vous devez exécuter le programme d’installation sur le serveur de site, puis sélectionner l’option **Effectuer une maintenance de site ou réinitialiser ce site**. Ensuite, sélectionnez l'option **Modifier la configuration de SQL Server** . Vous pouvez modifier les configurations de base de données de site suivantes :  

-   Le serveur Windows qui héberge la base de données.  

-   L'instance de SQL Server en cours d'utilisation sur un serveur qui héberge la base de données SQL Server.  

-   Nom de la base de données.  

-   Port SQL Server utilisé par Configuration Manager  

-   Port SQL Server Service Broker utilisé par Configuration Manager  

**Si vous déplacez la base de données de site, vous devez configurer les éléments suivants :**  

-   **Configurer l’accès :** quand vous déplacez la base de données de site vers un nouvel ordinateur, ajoutez le compte d’ordinateur du serveur de site au groupe **Administrateurs locaux** sur l’ordinateur exécutant SQL Server. Si vous utilisez un cluster SQL Server pour la base de données de site, vous devez ajouter le compte d'ordinateur au groupe **Administrateurs locaux** de chaque ordinateur du nœud de cluster Windows Server.  

-   **Activer l’intégration du CLR (Common Language Runtime) :**  quand vous déplacez la base de données vers une nouvelle instance de SQL Server ou vers un nouvel ordinateur SQL Server, vous devez activer l’intégration du CLR. Pour activer le CLR, utilisez **SQL Server Management Studio** pour vous connecter à l’instance de SQL Server qui héberge la base de données de site, puis exécutez la procédure stockée suivante en tant que requête : **sp_configure ’clr enabled’,1; reconfigure**.  
-  **Garantir que le nouvel ordinateur SQL Server a accès à l’emplacement de sauvegarde :** quand vous utilisez un chemin UNC pour le stockage de la sauvegarde de la base de données de site, après avoir déplacé la base de données vers un nouveau serveur, dont un déplacement vers un groupe de disponibilité SQL Server AlwaysOn ou un cluster SQL Server, vérifiez que le compte d’ordinateur du nouvel ordinateur SQL Server a des autorisations en **écriture** sur l’emplacement UNC.  


> [!IMPORTANT]  
>  Avant de déplacer une base de données possédant un ou plusieurs réplicas de base de données de points de gestion, vous devez supprimer les réplicas de base de données. Une fois la base de données déplacée, vous pouvez reconfigurer les réplicas de base de données. Pour plus d'informations, consultez [Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

##  <a name="bkmk_SPN"></a> Gérer le SPN pour le serveur de base de données de site  
Vous pouvez choisir le compte exécutant les services SQL pour la base de données du site :  

-   Quand les services s’exécutent avec le compte système d’ordinateurs, le SPN est enregistré automatiquement pour vous.  

-   Quand les services s’exécutent avec un compte d’utilisateur local de domaine, vous devez enregistrer manuellement le SPN pour vous assurer que les clients SQL et autre système de site peuvent effectuer l’authentification Kerberos. Sans l’authentification Kerberos, la communication avec la base de données peut échouer.  

La documentation de SQL Server peut vous aider à [enregistrer manuellement le SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx)et fournit des informations supplémentaires sur les SPN et les connexions Kerberos.  

> [!IMPORTANT]  
>  -   Quand vous créez un SPN pour un serveur SQL Server en cluster, vous devez spécifier le nom virtuel du cluster SQL Server comme nom d’ordinateur SQL Server.  
> -   La commande permettant d’enregistrer un SPN pour une instance nommée de SQL Server est la même que celle utilisée pour l’enregistrement du SPN d’une instance par défaut, la seule différence étant que le numéro de port doit correspondre au port utilisé par l’instance nommée.  

Vous pouvez enregistrer un SPN pour le compte de service SQL Server du serveur de base de données de site à l’aide de l’outil **Setspn** . Vous devez exécuter l'outil Setspn sur un ordinateur qui réside dans le domaine de SQL Server et qui doit utiliser les informations d'identification de l'administrateur de domaine pour pouvoir l'exécuter.  

 Les procédures suivantes sont des exemples de gestion de SPN pour le compte de service SQL Server qui utilise l'outil Setspn sur Windows Server 2008 R2. Pour obtenir des instructions spécifiques à propos de Setspn, voir [Présentation de Setspn](http://go.microsoft.com/fwlink/p/?LinkId=226343)ou une documentation similaire, spécifique à votre système d'exploitation.  

> [!NOTE]  
>  Les procédures suivantes font référence à l'outil en ligne de commande Setspn. L'outil en ligne de commande Setspn est inclus lorsque vous installez les outils de support Windows Server 2003 à partir du CD du produit ou depuis le [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=100114). Pour plus d'informations sur l'installation des outils de support Windows à partir du CD du produit, voir [Installer des outils de support Windows](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>Pour créer manuellement un nom principal de service (SPN) d'utilisateur de domaine pour le compte du service SQL Server  

1.  Dans le menu **Démarrer** , cliquez sur **Exécuter**et entrez **cmd** dans la boîte de dialogue Exécuter.  

2.  Sur la ligne de commande, accédez au répertoire d'installation des outils de support de Windows Server. Par défaut, ces outils se trouvent dans le répertoire **C:\Program Files\Support Tools** .  

3.  Entrez une commande valide pour créer le SPN. Pour créer le SPN, vous pouvez utiliser le nom NetBIOS ou le nom de domaine complet (FQDN) de l'ordinateur exécutant SQL Server. Toutefois, vous devez créer un SPN pour le nom NetBIOS et le nom de domaine complet.  

    > [!IMPORTANT]  
    >  Lorsque vous créez un SPN pour un SQL Server en cluster, vous devez spécifier le nom virtuel du cluster SQL Server comme nom d'ordinateur SQL Server.  

    -   Pour créer un SPN pour le nom NetBIOS de l’ordinateur SQL Server, tapez la commande suivante : **setspn -A MSSQLSvc/&lt;nom_ordinateur_SQL_Server\>:1433 &lt;Domaine\Compte>**  

    -   Pour créer un SPN pour le nom de domaine complet de l’ordinateur SQL Server, tapez la commande suivante : **setspn -A MSSQLSvc/&lt;nom_de_domaine_complet_SQL_Server\>:1433 &lt;Domaine\Compte**  

    > [!NOTE]  
    >  La commande permettant d'enregistrer un SPN pour une instance nommée de SQL Server est la même que celle utilisée pour l'enregistrement du SPN d'une instance par défaut, sauf que le numéro de port doit correspondre au port utilisé par l'instance nommée.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>Pour vérifier si le SPN d'utilisateur de domaine est inscrit correctement en utilisant la commande Setspn  

1.  Dans le menu **Démarrer** , cliquez sur **Exécuter**et entrez **cmd** dans la boîte de dialogue **Exécuter** .  

2.  À l’invite de commandes, entrez la commande suivante : **setspn -L &lt;domaine\compte_de_service_SQL>**.  

3.  Examinez le **Nom principal de service** inscrit pour vous assurer qu'un SPN valide a été créé pour SQL Server.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>Pour vérifier que le SPN d'utilisateur de domaine est enregistré correctement lors de l'utilisation de la console MMC ADSIEdit  

1.  Dans le menu **Démarrer** , cliquez sur **Exécuter**, puis entrez **adsiedit.msc** pour démarrer la console MMC ADSIEdit.  

2.  Si nécessaire, connectez-vous au domaine du serveur de site.  

3.  Dans le volet de la console, développez le domaine du serveur de site, développez **DC=&lt;nom_serveur_unique\>**, développez **CN=Users**, cliquez avec le bouton droit sur **CN=&lt;utilisateur_compte_de_service\>**, puis cliquez sur **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés CN=&lt;utilisateur_compte_de_service\>**, consultez la valeur de **servicePrincipalName** pour vérifier qu’un SPN valide a été créé et associé à l’ordinateur SQL Server approprié.  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Pour indiquer un compte d'utilisateur de domaine à la place du système local comme compte du service SQL Server  

1.  Créez ou sélectionnez un compte d'utilisateur de domaine ou de système local en tant que compte du service SQL Server.  

2.  Ouvrez le **Gestionnaire de configuration SQL Server**.  

3.  Cliquez sur **Services SQL Server**, puis double-cliquez sur **SQL Server&lt;NOM_INSTANCE\>**.  

4.  Dans l'onglet **Ouvrir une session** , sélectionnez **Ce compte**et entrez le nom et le mot de passe du compte d'utilisateur de domaine créé à l'étape 1. Vous pouvez également cliquer sur **Parcourir** pour rechercher le compte d'utilisateur dans les services de domaine Active Directory, puis cliquer sur **Appliquer**.  

5.  Cliquez sur **Oui** dans la boîte de dialogue **Confirmer la modification du compte** pour confirmer le changement de compte de service et redémarrer le service SQL Server.  

6.  Cliquez sur **OK** après modification du compte de service.  

##  <a name="bkmk_reset"></a> Exécuter une réinitialisation de site  
 Quand une réinitialisation de site s’exécute sur un site d’administration centrale ou sur un site principal, le site :  

-   réapplique les autorisations de fichiers et de Registre Configuration Manager par défaut ;  

-   réinstalle tous les composants de site et tous les rôles de système de site sur le site.  

Les sites secondaires ne prennent pas en charge la réinitialisation du site.  

Les réinitialisations de site peuvent être exécutées manuellement, quand vous le souhaitez, mais peuvent également s’exécuter automatiquement une fois que vous avez modifié la configuration du site.  

Par exemple, si les comptes utilisés par les composants Configuration Manager ont été modifiés, vous devez envisager de réinitialiser le site manuellement ; ainsi mis à jour, les composants de site peuvent utiliser les nouvelles informations de compte. Toutefois, si vous modifiez les langues du client ou du serveur sur un site, Configuration Manager réinitialise automatiquement le site, car cette action est nécessaire avant que le site puisse utiliser cette modification.  

> [!NOTE]  
>  La réinitialisation d’un site ne réinitialise pas les autorisations d’accès aux objets non-Configuration Manager.  

Quand une réinitialisation de site s’exécute :  

1.  L’installation s’arrête et redémarre le service **SMS_SITE_COMPONENT_MANAGER** ainsi que les composants de thread du service **SMS_EXECUTIVE** .  

2.  Le programme d’installation supprime, puis recrée, le dossier partagé du système de site et le composant **SMS Executive** sur l’ordinateur local et sur les ordinateurs de système de site distants.  

3.  Le programme d’installation redémarre le service **SMS_SITE_COMPONENT_MANAGER** , et ce service installe les services **SMS_EXECUTIVE** et **SMS_SQL_MONITOR** .  

La réinitialisation d'un site restaure, également, les objets suivants :  

-   Les clés de Registre **SMS** ou **NAL** et toutes les sous-clés par défaut dépendant de ces clés.  

-   L’arborescence du répertoire de fichiers Configuration Manager et tous les fichiers par défaut ou tous les sous-répertoires de cette arborescence du répertoire de fichiers.  

**Configuration requise pour exécuter une réinitialisation du site**  

Le compte que vous utilisez pour effectuer une réinitialisation du site doit disposer des autorisations suivantes :  

-   Le compte que vous utilisez pour effectuer une réinitialisation du site doit disposer des autorisations suivantes :  

    -   **Site d’administration centrale**: le compte que vous utilisez pour réinitialiser un site de ce site doit être un administrateur local situé sur le serveur de site d'administration centrale et doit disposer de privilèges équivalents au rôle de sécurité de l'administration basée sur le rôle **Administrateur complet** .  

    -   **Site principal**: le compte que vous utilisez pour réinitialiser un site de ce site doit être un administrateur local situé sur le serveur de site principal et doit disposer de privilèges équivalents au rôle de sécurité de l'administration basée sur le rôle **Administrateur complet** . Si le site principal se trouve dans une hiérarchie disposant d'un site d'administration centrale, ce compte doit également être un administrateur local sur le serveur du site d'administration centrale.  

**Limitations d’une réinitialisation de site**
  - Depuis la version 1602, vous ne pouvez pas utiliser une réinitialisation de site pour modifier les modules linguistiques serveur ou client qui ont été installés sur les sites tant que la hiérarchie est configurée pour prendre en charge les [tests des mises à niveau du client dans un regroupement de préproduction](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="to-perform-a-site-reset"></a>Pour effectuer une réinitialisation de site  

1.  Exécutez **Installation de Configuration Manager** à partir de **&lt;dossier_installation_du_site_Configuration_Manager\>\BIN\X64\setup.exe**.  

    > [!TIP]  
    >  Vous pouvez également exécuter une réinitialisation de site en démarrant le programme d’installation de Configuration Manager dans le menu **Démarrer** de l’ordinateur serveur de site ou depuis le média source Configuration Manager.  

2.  Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.  

3.  Sur la page **Maintenance de site** , sélectionnez **Réinitialiser le site sans modification de la configuration**, puis cliquez sur **Suivant**.  

4.  Cliquez sur **Oui** pour démarrer la réinitialisation du site.  

Une fois la réinitialisation du site terminée, cliquez sur **Fermer** pour terminer cette procédure.  

##  <a name="bkmk_sitelang"></a> Gérer les modules linguistiques sur un site  
Après l’installation d’un site, vous pouvez modifier les modules linguistiques client et serveur en cours d’utilisation :  

**Modules linguistiques serveur :**  

-   **S’applique à :**  

     Installations de la console Configuration Manager  

     Nouvelles installations de rôles de système de site applicables  

-   **Détails :**  

     Après la mise à jour des modules linguistiques serveur d’un site, vous pouvez ajouter la prise en charge des modules linguistiques dans les consoles Configuration Manager.  

     Pour ajouter la prise en charge d’un module linguistique serveur dans une console Configuration Manager, vous devez installer la console Configuration Manager à partir du dossier **ConsoleSetup** d’un serveur de site dans lequel figure le module linguistique que vous souhaitez utiliser. Si la console Configuration Manager est déjà installée, vous devez commencer par la désinstaller, afin de permettre à la nouvelle installation d’identifier la liste actuelle des modules linguistiques pris en charge.  

**Modules linguistiques client :**  

-   **S’applique à :**  

     Les modifications apportées aux modules linguistiques client mettent à jour les fichiers sources d’installation du client, pour que les nouvelles installations et mises à niveau de client ajoutent la prise en charge de la liste des langues client mise à jour.  

-   **Détails :**  

     Après la mise à jour des modules linguistique client d'un site, vous devez installer chacun des clients qui utiliseront les modules linguistiques en utilisant les fichiers sources qui incluent les modules linguistiques client.  

Pour plus d’informations sur les langues client et serveur prises en charge par Configuration Manager, consultez [Modules linguistiques dans System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md).  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>Pour modifier les modules linguistiques pris en charge par un site  

1.  Sur le serveur de site, exécutez le programme d’installation de Configuration Manager à partir de **&lt;dossier_installation_du_site_Configuration_Manager\>\BIN\X64\setup.exe**.  

2.  Sur la page **Mise en route** , sélectionnez **Effectuer une maintenance de site ou réinitialiser ce site**, puis cliquez sur **Suivant**.  

3.  Sur la page **Maintenance de site** , sélectionnez **Modifier la configuration de la langue**, puis cliquez sur **Suivant**.  

4.  Sur la page **Téléchargements requis** , sélectionnez **Télécharger les fichiers requis** pour acquérir des mises à jour de modules linguistiques ou **Utiliser des fichiers précédemment téléchargés** pour utiliser les fichiers précédemment téléchargés incluant les modules linguistiques que vous souhaitez ajouter au site. Cliquez sur **Suivant** pour valider les fichiers et continuer.  

5.  Sur la page **Sélection de la langue du serveur** , activez les cases à cocher correspondant aux langues serveur prises en charge par ce site, puis cliquez sur **Suivant**.  

6.  Sur la page **Sélection de la langue client** , activez les cases à cocher correspondant aux langues client prises en charge par ce site, puis cliquez sur **Suivant**.  

7.  Cliquez sur **Suivant**pour modifier les langues prises en charge au niveau du site.  

    > [!NOTE]  
    >  Configuration Manager lance une réinitialisation de site qui réinstalle également tous les rôles de système de site au niveau du site.  

8.  Cliquez sur **Fermer** pour terminer cette procédure.  

##  <a name="BKMK_ModDBAlert"></a> Modifier le seuil d’alerte du serveur de base de données  
 Par défaut, Configuration Manager génère des alertes lorsque l’espace disque libre sur un serveur de base de données de site est faible. Les valeurs par défaut sont définies pour générer un avertissement lorsque l'espace disque libre est de 10 Go ou moins et une alerte critique lorsque l'espace disque libre est de 5 Go ou moins. Vous pouvez modifier ces valeurs ou désactiver les alertes pour chaque site.  

 Pour modifier ces paramètres :  

1.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.  

2.  Sélectionnez le site que vous souhaitez configurer et ouvrez les **Propriétés** de ce site.  

3.  Dans la boîte de dialogue **Propriétés** du site, sélectionnez l’onglet **Alerte**, puis modifiez les paramètres.  

4.  Cliquez sur **OK** pour fermer la boîte de dialogue des propriétés de site.  
