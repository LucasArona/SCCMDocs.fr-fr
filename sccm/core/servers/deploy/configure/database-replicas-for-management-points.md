---
title: Réplicas de base de données de point de gestion
titleSuffix: Configuration Manager
description: Utilisez un réplica de base de données pour réduire la charge processeur placée sur le serveur de base de données de site par les points de gestion.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b06f781b-ab25-4d9a-b128-02cbd7cbcffe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: da5ad0fd932bb94bdab42ab723dcfc71ff252140
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416371"
---
# <a name="database-replicas-for-management-points-for-system-center-configuration-manager"></a>Réplicas de base de données pour les points de gestion de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les sites principaux System Center Configuration Manager peuvent utiliser un réplica de base de données pour réduire la charge processeur placée sur le serveur de base de données du site par les points de gestion à mesure qu’ils traitent les demandes des clients.  

-   Quand un point de gestion utilise un réplica de base de données, il demande des données de l’ordinateur SQL Server qui héberge le réplica de base de données au lieu du serveur de base de données du site.  

-   Cela contribue à réduire les besoins de traitement du processeur sur le serveur de base de données du site, grâce au déchargement des tâches de traitement fréquentes liées aux clients.  Un exemple de tâche de traitement fréquente pour les clients est celui des sites comportant un grand nombre de clients qui effectuent des demandes fréquentes de stratégie de configuration de client.  


##  <a name="bkmk_Prepare"></a> Préparation à l’utilisation de réplicas de base de données  
**À propos des réplicas de base de données pour les points de gestion :**  

-   Les réplicas sont une copie partielle de la base de données du site répliquée sur une instance distincte de SQL Server :  

    -   Les sites principaux prennent en charge un réplica de base de données dédié pour chaque point de gestion au niveau du site (les sites secondaires ne prennent pas en charge les réplicas de base de données).  

    -   Un réplica de base de données unique peut être utilisé par plusieurs points de gestion d’un même site.  

    -   Un serveur SQL Server peut héberger plusieurs réplicas de base de données pour une utilisation par différents points de gestion à condition que chacun s’exécute sur une instance distincte de SQL Server.  

-   Les réplicas synchronisent une copie de la base de données du site, selon une planification fixe, à partir des données publiées par le serveur de base de données du site à cet effet.  

-   Vous pouvez configurer un point de gestion pour qu’il utilise un réplica soit au moment de l’installation du point de gestion, soit ultérieurement en reconfigurant le point de gestion déjà installé afin qu’il utilise le réplica de base de données.  

-   Vérifiez régulièrement le serveur de base de données du site et chaque serveur réplica de base de données pour vous assurer que la réplication s’effectue correctement entre eux, et que les performances du serveur réplica de base de données sont suffisantes pour les performances requises du site et du client.  

**Conditions préalables pour les réplicas de base de données :**  

-   **Configuration requise de SQL Server :**  

    -   Le serveur SQL Server qui héberge le réplica de base de données doit présenter la même configuration que le serveur de base de données du site. En revanche, le serveur réplica n’est pas tenu d’exécuter la même version ou édition de SQL Server que le serveur de base de données du site, tant qu’il exécute une version et une édition prises en charge de SQL Server. Pour plus d’informations, consultez [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

    -   Le service SQL Server sur l’ordinateur qui héberge la base de données réplica doit s’exécuter en tant que compte **système** .  

    -   La **réplication SQL Server** doit être installée sur les serveurs SQL Server qui hébergent la base de données du site et le réplica de base de données.  

    -   La base de données du site doit **publier** le réplica de base de données, et chaque serveur réplica de base de données distant doit **s’abonner** aux données publiées.  

    -   Les serveurs SQL Server qui hébergent la base de données du site et le réplica de base de données doivent être configurés pour prendre en charge une taille de réplication de texte maximale ( **Max Text Repl Size** ) de 2 Go. Pour obtenir un exemple de configuration de cette option pour SQL Server 2012, voir [Configurer l'option de configuration du serveur max text repl size](http://go.microsoft.com/fwlink/p/?LinkId=273960).  

-   **Certificat auto-signé** : Pour configurer un réplica de base de données, vous devez créer un certificat auto-signé sur le serveur réplica de base de données et le rendre disponible pour chaque point de gestion devant utiliser ce serveur.  

    -   Le certificat est automatiquement disponible pour un point de gestion installé sur le serveur de réplica de base de données.  

    -   Pour rendre ce certificat disponible pour un point de gestion distant, vous devez exporter le certificat, puis l’ajouter au magasin de certificats **Personnes autorisées** sur le point de gestion distant.  

-   **Notification du client :** Pour prendre en charge la notification de client avec un réplica de base de données pour un point de gestion, vous devez configurer la communication entre le serveur de base de données du site et le serveur de réplica de base de données pour **SQL Server Service Broker**. Pour cela, vous devez :  

    -   Configurer chaque base de données avec les informations relatives à l’autre base de données  

    -   Échanger les certificats entre les deux bases de données pour permettre une communication sécurisée  

**Limitations relatives à l’utilisation de réplicas de base de données :**  

-   Si votre site est configuré pour publier des réplicas de base de données, vous devez suivre les procédures suivantes à la place des instructions standard :  

    -   [Désinstallation d’un serveur de site qui publie un réplica de base de données](#BKMK_DBReplicaOps_Uninstall)  

    -   [Déplacement d’une base de données d’un serveur de site qui publie un réplica de base de données](#BKMK_DBReplicaOps_Move)  

-   **Mises à niveau vers System Center Configuration Manager** : Avant d’effectuer la mise à niveau d’un site System Center 2012 Configuration Manager vers System Center Configuration Manager Current Branch ou la mise à jour de Configuration Manager Current Branch vers la dernière version, vous devez désactiver les réplicas de base de données pour les points de gestion.  Après avoir mis à niveau votre site, reconfigurez les réplicas de base de données pour les points de gestion.  

-   **Plusieurs réplicas sur un même serveur SQL Server :**  Si vous configurez un serveur réplica de base de données pour héberger plusieurs réplicas de base de données pour des points de gestion (chaque réplica devant être sur une instance distincte), vous devez utiliser un script de configuration modifié (voir l’étape 4 de la section suivante) afin que le certificat auto-signé utilisé par les réplicas de base de données précédemment configurés sur ce serveur ne soit pas remplacé.  

##  <a name="BKMK_DBReplica_Config"></a> Configuration des réplicas de base de données  
Pour configurer un réplica de base de données, procédez comme suit :  

-   [Étape 1 : Configuration du serveur de base de données du site pour publier le réplica de base de données](#BKMK_DBReplica_ConfigSiteDB)  

-   [Étape 2 : Configuration du serveur réplica de base de données](#BKMK_DBReplica_ConfigSrv)  

-   [Étape 3 : Configuration des points de gestion pour utiliser le réplica de base de données](#BKMK_DBReplica_ConfigMP)  

-   [Étape 4 : Configuration d’un certificat auto-signé pour le serveur réplica de base de données](#BKMK_DBReplica_Cert)  

-   [Étape 5 : Configuration de Service Broker SQL Server pour le serveur réplica de base de données](#BKMK_DBreplica_SSB)  

###  <a name="BKMK_DBReplica_ConfigSiteDB"></a> Étape 1 : Configuration du serveur de base de données du site pour publier le réplica de base de données  
 Utilisez la procédure suivante comme exemple pour configurer le serveur de base de données de site sur un ordinateur Windows Server 2008 R2 pour publier le réplica de la base de données. Si vous disposez d'une version du système d'exploitation différente, consultez la documentation de votre version de système d'exploitation et adaptez les étapes de la présente procédure en fonction de vos besoins.  

##### <a name="to-configure-the-site-database-server"></a>Pour configurer le serveur de base de données de site  

1.  Sur le serveur de base de données de site, définissez le démarrage automatique de l'Agent SQL Server.  

2.  Sur le serveur de base de données de site, créez un groupe d'utilisateurs local nommé **ConfigMgr_MPReplicaAccess**. Vous devez ajouter le compte d'ordinateur pour chaque serveur de réplica de base de données que vous utilisez sur ce site à ce groupe afin de permettre la synchronisation entre ces serveurs de réplica de base de données et le réplica de base de données publié.  

3.  Sur le serveur de base de données de site, configurez un fichier de partage nommé **ConfigMgr_MPReplica**.  

4.  Ajoutez les autorisations suivantes au partage **ConfigMgr_MPReplica** :  

    > [!NOTE]  
    >  Si l'Agent SQL Server utilise un compte autre que le compte système local, remplacez SYSTEM par ce nom de compte dans la liste ci-après.  

    -   **Autorisations de partage**:  

        -   SYSTEM : **Écriture**  

        -   ConfigMgr_MPReplicaAccess : **Lecture**  

    -   **Autorisations NTFS**:  

        -   SYSTEM : **Contrôle intégral**  

        -   ConfigMgr_MPReplicaAccess : **Lecture**, **Lecture et exécution**, **Répertorier le contenu du dossier**  

5.  Utilisez **SQL Server Management Studio** pour vous connecter à la base de données de site et exécutez la procédure stockée suivante en tant que requête : **spCreateMPReplicaPublication**  

Lorsque la procédure stockée est terminée, le serveur de base de données de site est configuré pour publier le réplica de la base de données.  

###  <a name="BKMK_DBReplica_ConfigSrv"></a> Étape 2 : Configuration du serveur réplica de base de données  
Le serveur de réplica de base de données est un ordinateur exécutant SQL Server et hébergeant un réplica de la base de données de site destiné aux points de gestion. Selon une planification fixe, le serveur de réplica de base de données synchronise sa copie de la base de données avec le réplica de base de données qui est publié par le serveur de base de données de site.  

Le serveur de réplica de base de données doit répondre aux mêmes exigences que le serveur de base de données de site. Cependant, le serveur de réplica de la base de données peut exécuter une édition ou version de SQL Server différente de celle du serveur de base de données de site. Pour plus d’informations sur les versions de SQL Server prises en charge, consultez la rubrique [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) .  

> [!IMPORTANT]  
>  Le service SQL Server sur l'ordinateur qui héberge la base de données de réplica doit s'exécuter comme un compte système.  

Utilisez la procédure suivante comme exemple pour configurer un serveur de réplica de base de données sur un ordinateur Windows Server 2008 R2. Si vous disposez d'une version du système d'exploitation différente, consultez la documentation de votre version de système d'exploitation et adaptez les étapes de la présente procédure en fonction de vos besoins.  

##### <a name="to-configure-the-database-replica-server"></a>Pour configurer le serveur de réplica de base de données  

1. Sur le serveur de réplica de base de données, définissez le démarrage automatique de l'Agent SQL Server.  

2. Sur le serveur de réplica de base de données, utilisez **SQL Server Management Studio** pour vous connecter au serveur local, accédez au dossier **Réplication** , cliquez sur Abonnements locaux, puis sélectionnez **Nouvel abonnement** pour ouvrir l' **Assistant Nouvel abonnement**.  

   1. Sur la page **Publication** , dans la liste **Éditeur** , sélectionnez **Rechercher un serveur de publication SQL**, entrez le nom du serveur de base de données de site, puis cliquez sur **Connecter**.  

   2. Sélectionnez **ConfigMgr_MPReplica**, puis cliquez sur **Suivant**.  

   3. Sur la page **Emplacement de l'Agent de distribution** , sélectionnez **Exécuter chaque agent sur son Abonné (abonnements par extraction de données (pull))**, puis cliquez sur **Suivant**.  

   4. Sur la page **Abonnés** , effectuez l'une des opérations ci-après.  

      -   Sélectionnez une base de données existante à partir du serveur de réplica de base de données à utiliser pour le réplica de base de données, puis cliquez sur **OK**.  

      -   Sélectionnez **Nouvelle base de données** pour créer une base de données pour le réplica de base de données. Sur la page **Nouvelle base de données** , spécifiez un nom de base de données, puis cliquez sur **OK**.  

   5. Cliquez sur **Suivant** pour continuer.  

   6. Dans la page **Sécurité de l’Agent de distribution**, cliquez sur le bouton des propriétés **(.…)** dans le champ Connexion de l’Abonné de la boîte de dialogue, puis configurez les paramètres de sécurité pour la connexion.  

      > [!TIP]  
      >  Le bouton des propriétés, **(....)**, se trouve dans la quatrième colonne de la zone d’affichage.  

      **Paramètres de sécurité :**  

      - Configurez le compte qui exécute le processus de l'Agent de distribution (le compte de processus) :  

        -   Si l'Agent SQL Server s'exécute en tant que système local, sélectionnez **Exécuter sous le compte du service de l'Agent SQL Server (non recommandé pour des raisons de sécurité.)**.  

        -   Si l'Agent SQL Server s'exécute à l'aide d'un autre compte, sélectionnez **Exécuter sous le compte Windows suivant**, puis configurez ce compte. Vous pouvez spécifier un compte Windows ou un compte SQL Server.  

        > [!IMPORTANT]  
        >  Vous devez accorder au compte qui exécute l'Agent de distribution des autorisations sur l'éditeur comme un abonnement par extraction. Pour plus d’informations sur la configuration de ces autorisations, consultez [Sécurité de l’Agent de distribution](http://go.microsoft.com/fwlink/p/?LinkId=238463) dans la bibliothèque TechNet de SQL Server.  

      - Pour **Se connecter au serveur de distribution**, sélectionnez **En imitant le compte de processus**.  

      - Pour **Connexion à l'Abonné**, sélectionnez **En imitant le compte de processus**.  

        Après la configuration des paramètres de sécurité de connexion, cliquez sur **OK** pour les enregistrer, puis cliquez sur **Suivant**.  

   7. Sur la page **Planification des synchronisations** , dans la zone de liste **Planification de l'agent** , sélectionnez **Définir la planification**, puis configurez **Nouvelle planification du travail**. Définissez la fréquence sur **Quotidienne**, toutes les **5 minute(s)**, et la durée sur **aucune date de fin**. Cliquez sur **Suivant** pour enregistrer la planification, puis cliquez sur **Suivant** de nouveau.  

   8. Sur la page **Actions de l'Assistant** , activez la case à cocher **Créer les abonnements**, puis cliquez sur **Suivant**.  

   9. Dans la page **Terminer l'Assistant** , cliquez sur **Terminer**, puis cliquez sur **Fermer** pour fermer l'Assistant.  

3. Immédiatement après la fin de l’exécution de l’Assistant Nouvel abonnement, utilisez **SQL Server Management Studio** pour vous connecter à la base de données du serveur de réplication de base de données, puis exécutez la requête suivante pour activer la propriété de base de données TRUSTWORTHY :  `ALTER DATABASE <MP Replica Database Name> SET TRUSTWORTHY ON;`  

4. Vérifiez l'état de la synchronisation pour valider la réussite de l'abonnement :  

   -   Sur l'ordinateur de l'abonné :  

       -   Dans **SQL Server Management Studio**, connectez-vous au serveur de réplica de base de données, puis développez le dossier **Réplication**.  

       -   Développez **Abonnements locaux**, cliquez avec le bouton droit sur l'abonnement à la publication de la base de données de site, puis sélectionnez **Afficher l'état de synchronisation**.  

   -   Sur l'ordinateur de l'éditeur :  

       -   Dans **SQL Server Management Studio**, connectez-vous à l'ordinateur de base de données de site, cliquez avec le bouton droit sur le dossier **Réplication** , puis sélectionnez **Lancer le moniteur de réplication**.  

5. Pour activer l'intégration du CLR pour le réplica de base de données, utilisez **SQL Server Management Studio** pour vous connecter au réplica de base de données sur le serveur de réplica de base de données, puis exécutez la procédure stockée suivante en tant que requête : **exec sp_configure 'clr enabled', 1; RECONFIGURE WITH OVERRIDE**  

6. Pour chaque point de gestion qui utilise un serveur de réplica de base de données, ajoutez le compte d'ordinateur de ce point de gestion au groupe local **Administrateurs** sur le serveur de réplica de base de données.  

   > [!TIP]  
   >  Cette étape n'est pas nécessaire pour un point de gestion qui s'exécute sur le serveur de réplica de base de données.  

   Le réplica de base de données est maintenant prêt à l'utilisation par un point de gestion.  

###  <a name="BKMK_DBReplica_ConfigMP"></a> Étape 3 : Configuration des points de gestion pour utiliser le réplica de base de données  
 Vous pouvez configurer un point de gestion sur un site principal pour utiliser un réplica de base de données lorsque vous installez un rôle de point de gestion, ou bien, vous pouvez reconfigurer un point de gestion existant pour utiliser le réplica de base de données.  

 Pour configurer un point de gestion pour utiliser un réplica de base de données, utilisez les informations suivantes :  

-   **Pour configurer un nouveau point de gestion :** Sur la page **Base de données du point de gestion** de l’assistant d’installation du point de gestion, sélectionnez **Utiliser un réplica de la base de données**, puis spécifiez le nom de domaine complet de l’ordinateur hébergeant le réplica de base de données. Ensuite, sous **Nom de base de données de site ConfigMgr**, spécifiez le nom de base de données du réplica de base de données sur cet ordinateur.  

-   **Pour configurer un point de gestion précédemment installé** : Sur la page des propriétés du point de gestion, sélectionnez l’onglet **Base de données du point de gestion**, sélectionnez **Utiliser un réplica de la base de données**, puis spécifiez le nom de domaine complet de l’ordinateur hébergeant le réplica de base de données. Ensuite, sous **Nom de base de données de site ConfigMgr**, spécifiez le nom de base de données du réplica de base de données sur cet ordinateur.  

-   **Pour chaque point de gestion qui utilise un réplica de base de données**, vous devez ajouter manuellement le compte d'ordinateur du serveur de point de gestion au rôle **db_datareader** pour le réplica de base de données.  

Outre la configuration du point de gestion pour utiliser le serveur de réplica de base de données, vous devez activer l'option **Authentification Windows** dans **IIS** sur le point de gestion :  

1.  Ouvrez **Gestionnaire des services Internet (IIS)**.  

2.  Sélectionnez le site Web utilisé par le point de gestion, puis cliquez sur **Authentification**.  

3.  Définissez **Authentification Windows** sur **Activé**, puis fermez le **Gestionnaire des services Internet (IIS)**.  

###  <a name="BKMK_DBReplica_Cert"></a> Étape 4 : Configuration d’un certificat auto-signé pour le serveur réplica de base de données  
 Vous devez créer un certificat auto-signé sur le serveur de réplica de base de données et le rendre disponible pour chaque point de gestion qui utilisera ce serveur.  

 Le certificat est automatiquement disponible pour un point de gestion installé sur le serveur de réplica de base de données. Cependant, pour rendre ce certificat disponible pour les points de gestion distants, vous devez exporter le certificat, puis l'ajouter au magasin de certificats Personnes autorisées sur le point de gestion distant.  

 Utilisez les procédures suivantes comme exemple pour configurer le certificat auto-signé sur le serveur de réplica de base de données d'un ordinateur Windows Server 2008 R2. Si vous disposez d'une version du système d'exploitation différente, consultez la documentation de votre version de système d'exploitation et adaptez les étapes des présentes procédures en fonction de vos besoins.  

##### <a name="to-configure-a-self-signed-certificate-for-the-database-replica-server"></a>Pour configurer un certificat auto-signé pour le serveur de réplica de base de données  

1.  Sur le serveur de réplica de base de données, ouvrez une invite de commande PowerShell avec des privilèges d'administration, puis exécutez la commande suivante : **set-executionpolicy UnRestricted**  

2.  Copiez le script PowerShell suivant et enregistrez-le sous un fichier portant le nom **CreateMPReplicaCert.ps1**. Placez une copie de ce fichier dans le dossier racine de la partition système du serveur de réplica de base de données.  

    > [!IMPORTANT]  
    >  Si vous configurez plusieurs réplicas de base de données sur un serveur SQL Server unique, pour chaque nouveau réplica que vous configurez, vous devez utiliser une version modifiée de ce script pour cette procédure. Consultez  [Script complémentaire pour les réplicas de base de données supplémentaires sur un même serveur SQL Server](#bkmk_supscript).  

    ```  
    # Script for creating a self-signed certificate for the local machine and configuring SQL Server to use it.  

    Param($SQLInstance)  

    $ConfigMgrCertFriendlyName = "ConfigMgr SQL Server Identification Certificate"  

    # Get local computer name  
    $computerName = "$env:computername"  

    # Get the sql server name  
    #$key="HKLM:\SOFTWARE\Microsoft\SMS\MP"  
    #$value="SQL Server Name"  
    #$sqlServerName= (Get-ItemProperty $key).$value  
    #$dbValue="Database Name"  
    #$sqlInstance_DB_Name= (Get-ItemProperty $key).$dbValue  

    $sqlServerName = [System.Net.Dns]::GetHostByName("localhost").HostName   
    $sqlInstanceName = "MSSQLSERVER"  
    $SQLServiceName = "MSSQLSERVER"  

    if ($SQLInstance -ne $Null)  
    {  
        $sqlInstanceName = $SQLInstance  
        $SQLServiceName = "MSSQL$" + $SQLInstance  
    }  

    # Delete existing cert if one exists  
    function Get-Certificate($storename, $storelocation)  
    {   
        $store=new-object System.Security.Cryptography.X509Certificates.X509Store($storename,$storelocation)   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Certificates   
    }   

    $cert = Get-Certificate "My" "LocalMachine" | ?{$_.FriendlyName -eq $ConfigMgrCertFriendlyName}   
    if($cert -is [Object])  
    {  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()  

        # Remove this cert from Trusted People too...  
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("TrustedPeople","LocalMachine")   
        $store.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)   
        $store.Remove($cert)  
        $store.Close()      
    }  

    # Create the new cert  
    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"  
    $name.Encode("CN=" + $sqlServerName, 0)  

    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"  
    $key.ProviderName = "Microsoft RSA SChannel Cryptographic Provider"  
    $key.KeySpec = 1  
    $key.Length = 1024  
    $key.SecurityDescriptor = "D:PAI(A;;0xd01f01ff;;;SY)(A;;0xd01f01ff;;;BA)(A;;0x80120089;;;NS)"  
    $key.MachineContext = 1  
    $key.Create()  

    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"  
    $serverauthoid.InitializeFromValue("1.3.6.1.5.5.7.3.1")  
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"  
    $ekuoids.add($serverauthoid)  
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"  
    $ekuext.InitializeEncode($ekuoids)  

    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"  
    $cert.InitializeFromPrivateKey(2, $key, "")  
    $cert.Subject = $name  
    $cert.Issuer = $cert.Subject  
    $cert.NotBefore = get-date  
    $cert.NotAfter = $cert.NotBefore.AddDays(3650)  
    $cert.X509Extensions.Add($ekuext)  
    $cert.Encode()  

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"  
    $enrollment.InitializeFromRequest($cert)  
    $enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"  
    $certdata = $enrollment.CreateRequest(0x1)  
    $enrollment.InstallResponse(0x2, $certdata, 0x1, "")  

    # Add this cert to the trusted peoples store  
    [Byte[]]$bytes = [System.Convert]::FromBase64String($certdata)  

    $trustedPeople = new-object System.Security.Cryptography.X509certificates.X509Store "TrustedPeople", "LocalMachine"  
    $trustedPeople.Open([Security.Cryptography.X509Certificates.OpenFlags]::ReadWrite)  
    $trustedPeople.Add([Security.Cryptography.X509Certificates.X509Certificate2]$bytes)  
    $trustedPeople.Close()  

    # Get thumbprint from cert  
    $sha = new-object System.Security.Cryptography.SHA1CryptoServiceProvider  
    $certHash = $sha.ComputeHash($bytes)  
    $certHashCharArray = "";  
    $certThumbprint = "";  

    # Format the bytes into a hexadecimal string  
    foreach($byte in $certHash)  
    {  
        $temp = ($byte | % {"{0:x}" -f $_}) -join ""  
        $temp = ($temp | % {"{0,2}" -f $_})  
        $certHashCharArray = $certHashCharArray+ $temp;  
    }  
    $certHashCharArray = $certHashCharArray.Replace(' ', '0');  

    # SQL needs the thumbprint in lower case  
    foreach($char in $certHashCharArray)  
    {  
        [System.String]$myString = $char;  
        $certThumbprint = $certThumbprint + $myString.ToLower();  
    }  

    # Configure SQL to use this cert  
    $path = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\Instance Names\SQL"  
    $subKey = (Get-ItemProperty $path).$sqlInstanceName  
    $realPath = "HKLM:\SOFTWARE\Microsoft\Microsoft SQL Server\" + $subKey + "\MSSQLServer\SuperSocketNetLib"  
    $certKeyName = "Certificate"  
    Set-ItemProperty -path $realPath -name $certKeyName -Type string -Value $certThumbprint  

    # restart sql service  
    Restart-Service $SQLServiceName -Force  
    ```  

3.  Sur le serveur de réplica de base de données, exécutez la commande suivante, s'appliquant à la configuration de votre serveur SQL Server :  

    -   Pour une instance par défaut de SQL Server : Cliquez avec le bouton droit sur le fichier **CreateMPReplicaCert.ps1**, puis sélectionnez **Exécuter avec PowerShell**. Lorsque le script s'exécute, celui-ci crée le certificat auto-signé et configure SQL Server pour utiliser le certificat.  

    -   Pour une instance nommée de SQL Server : Utilisez PowerShell pour exécuter la commande **%path%\CreateMPReplicaCert.ps1 xxxxxx** où **xxxxxx** est le nom de l’instance de SQL Server.  

    -   Une fois le script terminé, vérifiez que l'agent  SQL Server est en cours d'exécution. Si ce n'est pas le cas, redémarrez SQL Server Agent.  

##### <a name="to-configure-remote-management-points-to-use-the-self-signed-certificate-of-the-database-replica-server"></a>Pour configurer des points de gestion à distance pour utiliser le certificat auto-signé du serveur de réplica de base de données  

1.  Sur le serveur réplica de base de données, effectuez les opérations suivantes pour exporter le certificat auto-signé du serveur :  

    1.  Cliquez sur **Démarrer**, cliquez sur **Exécuter**, puis tapez **mmc.exe**. Dans la console vide, cliquez sur **Fichier**, puis sur **Ajouter/Supprimer un composant logiciel enfichable**.  

    2.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , sélectionnez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis cliquez sur **Ajouter**.  

    3.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats** , cliquez sur **Compte d'ordinateur**, puis sur **Suivant**.  

    4.  Dans la boîte de dialogue **Sélectionner un ordinateur** , vérifiez que **L'ordinateur local (l'ordinateur sur lequel cette console s'exécute)** est sélectionné, puis cliquez sur **Terminer**.  

    5.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** , cliquez sur **OK**.  

    6.  Dans la console, développez **Certificats (ordinateur local)**, développez **Personnel**, puis sélectionnez **Certificats**.  

    7.  Cliquez avec le bouton droit sur le certificat portant le nom convivial **certificat d'identification ConfigMgr SQL Server**, cliquez sur **Toutes les tâches**, puis sélectionnez **Exporter**.  

    8.  Effectuez toutes les étapes de l' **Assistant Exportation de certificat** à l'aide des options par défaut et enregistrez le certificat avec l'extension de nom de fichier **.cer** .  

2.  Effectuez les opérations suivantes sur l'ordinateur du point de gestion pour ajouter le certificat auto-signé pour le serveur de réplica de base de données dans le magasin de certificats Personnes autorisées sur le point de gestion :  

    1.  Répétez les étapes précédentes de 1.a à 1.e pour configurer le composant logiciel enfichable MMC **Certificat** sur l’ordinateur du point de gestion.  

    2.  Dans la console, développez **Certificats (ordinateur local)** et **Personnes autorisées**, cliquez avec le bouton droit sur **Certificats**, sélectionnez **Toutes les tâches**, puis sélectionnez **Importer** pour lancer l' **Assistant Importation de certificat**.  

    3.  Sur la page **Fichier à importer** , cliquez sur le certificat sauvegardé à l'étape 1.h, puis cliquez sur **Suivant**.  

    4.  Sur la page **Magasin de certificats** , sélectionnez **Placer tous les certificats dans le magasin suivant**, lorsque le **Magasin de certificats** est paramétré sur **Personnes autorisées**, puis cliquez sur **Suivant**.  

    5.  Cliquez sur **Terminer** pour fermer l'Assistant et terminer la configuration des certificats sur le point de gestion.  

###  <a name="BKMK_DBreplica_SSB"></a> Étape 5 : Configuration de Service Broker SQL Server pour le serveur réplica de base de données  
Pour prendre en charge la notification de client avec un réplica de base de données pour un point de gestion, vous devez configurer la communication entre le serveur de base de données de site et le serveur de réplica de base de données pour SQL Server Service Broker. Cela nécessite la configuration de chaque base de données avec des informations sur l'autre base de données et d'échanger les certificats entre les deux bases de données pour une communication sécurisée.  

> [!NOTE]  
>  Avant de pouvoir utiliser la procédure suivante, le serveur de réplica de la base de données doit réussir la synchronisation initiale avec le serveur de base de données de site.  

 La procédure suivante ne modifie pas le port Service Broker configuré dans SQL Server pour le serveur de base de données de site ou le serveur de réplica de la base de données. Au lieu de cela, cette procédure configure chaque base de données pour qu'elle communique avec l'autre base de données en utilisant le port Service Broker correct.  

 Exécutez la procédure suivante pour configurer le Service Broker pour le serveur de base de données de site et le serveur de réplica de la base de données.  

##### <a name="to-configure-the-service-broker-for-a-database-replica"></a>Pour configurer le Service Broker pour un réplica de base de données  

1. Utilisez **SQL Server Management Studio** pour vous connecter à la base de données du serveur réplica de base de données, puis exécutez la requête suivante pour activer Service Broker sur le serveur réplica de base de données : **ALTER DATABASE &lt;Nom de la base de données réplica\> SET ENABLE_BROKER, HONOR_BROKER_PRIORITY ON WITH ROLLBACK IMMEDIATE**  

2. Cliquez ensuite sur le serveur de réplica de la base de données, configurez le Service Broker pour la notification de client et exportez le certificat Service Broker. Pour cela, exécutez une procédure stockée SQL Server qui configure le Service Broker et exporte le certificat comme une seule action. Lorsque vous exécutez la procédure stockée, vous devez définir le nom de domaine complet du serveur de réplica de la base de données, le nom de la base de données des réplicas de la base de données, ainsi qu'un emplacement pour l'exportation du fichier de certificat.  

    Exécutez la requête suivante pour configurer les informations requises sur le serveur de réplica de la base de données et pour exporter le certificat depuis le serveur de réplica de la base de données : **EXEC sp_BgbConfigSSBForReplicaDB '&lt;Nom de domaine complet SQL Server réplica\>', '&lt;Nom de la base de données réplica\>', '&lt;Chemin d’accès au fichier de sauvegarde de certificat\>'**  

   > [!NOTE]  
   >  Lorsque le serveur de réplica de base de données ne se trouve pas sur l'instance par défaut de SQL Server, dans cette étape, vous devez définir le nom de l'instance en plus du nom de la base de données réplica. Pour cela, remplacez **&lt;nom_base_de_données_réplica\>** par **&lt;nom_instance\\nom_base_de_données_réplica\>**.  

    Une fois le certificat exporté depuis le serveur de réplica de base de données, placez une copie du certificat sur le serveur de base de données de sites principaux.  

3. Utilisez **SQL Server Management Studio** pour vous connecter à la base de données du site principal. Après la connexion à la base de données des sites principaux, exécutez une requête pour importer le certificat et spécifiez le port Service Broker utilisé sur le serveur de réplica de base de données, le nom de domaine complet du serveur de réplica de base de données et le nom de la base de données de réplicas de base de données. Cela configure la base de données de sites principaux de sorte qu'elle utilise Service Broker pour communiquer avec la base de données du serveur de réplica de base de données.  

    Exécutez la requête suivante pour importer le certificat depuis le serveur de réplica de base de données et spécifier les informations requises : **EXEC sp_BgbConfigSSBForRemoteService 'REPLICA', '&lt;Port Service Broker SQL\>', '&lt;Chemin d’accès au fichier de certificat\>', '&lt;Nom de domaine complet SQL Server réplica\>', '&lt;Nom de la base de données réplica\>'**  

   > [!NOTE]  
   >  Lorsque le serveur de réplica de base de données ne se trouve pas sur l'instance par défaut de SQL Server, dans cette étape, vous devez définir le nom de l'instance en plus du nom de la base de données réplica. Pour cela, remplacez **&lt;nom_base_de_données_réplica\>** par **\nom_instance\\nom_base_de_données_réplica\>**.  

4. Ensuite, sur le serveur de base de données de site, exécutez la commande suivante pour exporter le certificat du serveur de base de données de site : **EXEC sp_BgbCreateAndBackupSQLCert '&lt;Chemin d’accès au fichier de sauvegarde de certificat\>'**  

    Une fois le certificat exporté depuis le serveur de base de données de site, placez une copie du certificat sur le serveur de réplica de base de données.  

5. Utilisez **SQL Server Management Studio** pour vous connecter à la base de données de serveur de réplica de base de données. Après la connexion à la base de données du serveur de réplica de base de données, exécutez une requête pour importer le certificat et spécifier le code de site du site principal et le port Service Broker utilisé sur le serveur de base de données de site. Cela configure le serveur de réplica de base de données de sorte qu'il utilise Service Broker pour communiquer avec la base de données du site principal.  

    Exécutez la requête suivante pour importer le certificat du serveur de base de données de site : **EXEC sp_BgbConfigSSBForRemoteService '&lt;Code de site\>', '&lt;Port Service Broker SQL\>', '&lt;Chemin d’accès du fichier de certificat\>'**  

   Après la configuration de la base de données de site et de la base de données de réplica de base de données, le gestionnaire de notification sur le site principal prend quelques minutes pour configurer la conversation Service Broker pour la notification de client depuis la base de données du site principal vers le réplica de la base de données.  

###  <a name="bkmk_supscript"></a> Script complémentaire pour les réplicas de base de données supplémentaires sur un même serveur SQL Server  
 Si vous utilisez le script de l’étape 4 pour configurer un certificat auto-signé pour le serveur réplica de base de données sur un serveur SQL Server comportant déjà un réplica de base de données que vous voulez continuer à utiliser, vous devez utiliser une version modifiée du script d’origine. Les modifications suivantes empêchent le script de supprimer un certificat existant sur le serveur, et créent les certificats suivants avec un nom convivial unique.  Modifiez le script d’origine comme suit :  

-   Commentez (pour empêcher l’exécution) chaque ligne entre les entrées du script **# Delete existing cert if one exists** et **# Create the new cert**. Pour ce faire, ajoutez le signe  **#**  au tout début de chaque ligne concernée.  

-   Pour chaque réplica de base de données suivant que vous configurez à l’aide de ce script, mettez à jour le nom convivial du certificat.  Pour cela, modifiez la ligne **$enrollment.CertificateFriendlyName = "ConfigMgr SQL Server Identification Certificate"** en remplaçant **ConfigMgr SQL Server Identification Certificate** par un nouveau nom, tel que  **ConfigMgr SQL Server Identification Certificate1**.  

##  <a name="BKMK_DBReplicaOps"></a> Gestion des configurations de réplica de base de données  
 Lorsque vous utilisez un réplica de base de données d'un site, utilisez les informations indiquées dans les sections suivantes pour compléter la procédure de désinstallation d'un réplica de base de données, désinstallation d'un site utilisant un réplica de base de données ou déplacement de la base de données de site vers une nouvelle installation de SQL Server. Lorsque vous utilisez les informations indiquées dans les sections suivantes pour supprimer des publications, suivez les instructions de suppression d'une réplication transactionnelle pour la version de SQL Server que vous utilisez pour le réplica de base de données. Par exemple, si vous utilisez SQL Server 2008 R2, consultez [Procédure : supprimer une publication (programmation Transact-SQL de la réplication)](http://go.microsoft.com/fwlink/p/?LinkId=273934).  

> [!NOTE]  
>  Après avoir restauré une base de données de site configurée pour des réplicas de base de données et avant de pouvoir utiliser les réplicas de base de données, vous devez reconfigurer chaque réplica de base de données en recréant les publications et les abonnements.  

###  <a name="BKMK_UninstallDbReplica"></a> Désinstallation d’un réplica de base de données  
 Lorsque vous utilisez un réplica de base de données pour un point de gestion, il peut être nécessaire de désinstaller le réplica de base de données pendant un certains temps, puis de le reconfigurer pour l'utiliser. Par exemple, vous devez supprimer les réplicas de base de données avant la mise à niveau d’un site Configuration Manager vers un nouveau Service Pack. Après la mise à niveau du site, vous pouvez restaurer le réplica de base de données pour l'utiliser.  

 Utilisez les étapes suivantes pour désinstaller un réplica de base de données.  

1.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Configuration du site**, sélectionnez **Serveurs et rôles de système de site** puis, dans le volet d’informations, sélectionnez le serveur de système de site hébergeant le point de gestion qui utilise le réplica de base de données à désinstaller.  

2.  Dans le volet **Rôles système de site** , cliquez avec le bouton droit sur **Point de gestion** , puis sélectionnez **Propriétés**.  

3.  Sous l'onglet **Base de données du point de gestion** , sélectionnez **Utiliser la base de données du site** pour configurer le point de gestion de sorte qu'il utilise la base de données de site à la place du réplica de base de données. Cliquez ensuite sur **OK** pour enregistrer la configuration.  

4.  Ensuite, utilisez **SQL Server Management Studio** pour effectuer les tâches suivantes :  

    -   Supprimer la publication pour le réplica de base de données de la base de données du serveur de site.  

    -   Supprimer l'abonnement pour le réplica de base de données du serveur de réplica de base de données.  

    -   Supprimer la base de données réplica du serveur de réplica de base de données.  

    -   Désactiver la publication et la distribution sur le serveur de base de données de site. Pour désactiver la publication et la distribution, cliquez avec le bouton droit sur le dossier de réplication, puis cliquez sur **Désactiver la publication et la distribution**.  

5.  Après la suppression de la publication, de l'abonnement, de la base de données réplica et la désactivation de la publication sur le serveur de base de données de site, le réplica de base de données est désinstallé.  

###  <a name="BKMK_DBReplicaOps_Uninstall"></a> Désinstallation d’un serveur de site qui publie un réplica de base de données  
 Avant de désinstaller un site qui publie un réplica de la base de données, procédez comme suit pour nettoyer la publication ainsi que tous les abonnements.  

1.  Utilisez **SQL Server Management Studio** pour supprimer la publication du réplica de la base de donnée depuis la base de données du serveur de site.  

2.  Utilisez **SQL Server Management Studio** pour supprimer l'abonnement de réplica de base de données de chaque serveur SQL distant qui héberge un réplica de base de données pour ce site.  

3.  Désinstallez le site.  

###  <a name="BKMK_DBReplicaOps_Move"></a> Déplacement d’une base de données d’un serveur de site qui publie un réplica de base de données  
 Lorsque vous déplacez la base de données de site vers un nouvel ordinateur, procédez comme suit :  

1.  Utilisez **SQL Server Management Studio** pour supprimer la publication du réplica de la base de donnée depuis la base de données du serveur de site.  

2.  Utilisez **SQL Server Management Studio** pour supprimer l'abonnement au réplica de la base de données de chaque serveur de réplica de base de données pour ce site.  

3.  Déplacez la base de données vers le nouvel ordinateur SQL Server. Pour plus d'informations, consultez la section [Modifier la configuration de base de données de site](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_dbconfig) dans la rubrique [Modifier votre infrastructure System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md) .  

4.  Recréez la publication pour le réplica de la base de données sur le serveur de la base de données du site. Pour plus d'informations, consultez [Étape 1 : Configuration du serveur de base de données du site pour publier le réplica de base de données](#BKMK_DBReplica_ConfigSiteDB) dans cette rubrique.  

5.  Recréez les abonnements pour le réplica de la base de données sur chaque serveur de réplica de base de données. Pour plus d'informations, consultez [Étape 2 : Configuration du serveur réplica de base de données](#BKMK_DBReplica_ConfigSrv) dans cette rubrique.  
