---
title: Propriétés et paramètres d'installation du client
titleSuffix: Configuration Manager
description: Découvrez les propriétés et paramètres de la ligne de commande ccmsetup pour l’installation du client Configuration Manager.
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 735a8da57c0225aee533568eb997dc82d9816d6b
ms.sourcegitcommit: db6074317d5c68ebb5fc478be5bceeb441aa0737
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2018
---
# <a name="about-client-installation-parameters-and-properties-in-system-center-configuration-manager"></a>À propos des propriétés et des paramètres d’installation du client dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez la commande CCMSetup.exe pour installer le client Configuration Manager. Si des paramètres d’installation du client sont indiqués en ligne de commande, ils modifient le comportement de l’installation. Si vous fournissez des propriétés d’installation du client en ligne de commande, elles modifient la configuration initiale de l’agent client installé.



##  <a name="aboutCCMSetup"></a> À propos de CCMSetup.exe  
 La commande CCMSetup.exe télécharge les fichiers nécessaires pour installer le client à partir d’un point de gestion ou d’un emplacement source. Ces fichiers peuvent être les suivants :  

-   Le fichier client.msi du package Windows Installer qui installe le logiciel client.  

-   Les fichiers d’installation du service BITS (Background Intelligent Transfer Service) de Microsoft.  

-   Les fichiers d’installation de Windows Installer.  

-   Les mises à jour et correctifs du client Configuration Manager.  

> [!NOTE]  
>  Dans Configuration Manager, vous ne pouvez pas exécuter directement le fichier Client.msi.  

 CCMSetup.exe fournit des [paramètres de ligne de commande](#ccmsetup-exe-command-line-parameters) pour personnaliser l’installation. Ils sont précédés d’une barre oblique inverse et, par convention, sont en minuscules. La valeur d’un paramètre, si nécessaire, est spécifiée à l’aide d’un signe deux-points directement suivi de la valeur souhaitée. Vous pouvez également fournir des propriétés qui modifient le comportement de client.msi dans la ligne de commande de CCMSetup.exe. Par convention, les propriétés sont tout en majuscules. La valeur d’une propriété est spécifiée à l’aide d’un signe égal directement suivi de la valeur souhaitée.  

> [!IMPORTANT]  
>  Spécifiez les paramètres de CCMSetup avant de spécifier les propriétés de client.msi.  

 CCMSetup.exe et les fichiers de prise en charge se trouvent sur le serveur de site dans le dossier **Client** du dossier d’installation de Configuration Manager. Ce dossier est partagé sur le réseau sous **&lt;Nom_Serveur_Site\>\SMS_&lt;Code_Site\>\Client**.  

 À l'invite de commandes, la commande CCMSetup.exe utilise le format suivant :  

 `CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

 Par exemple :  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 Cet exemple effectue les opérations suivantes :  

-   Force le point de gestion SMSMP01 à demander la liste des points de distribution pour télécharger les fichiers d’installation du client.  

-   Force l’arrêt de l’installation si une version du client existe déjà sur l’ordinateur.  

-   Ordonne à client.msi d'attribuer le client au code de site S01.  

-   Ordonne à client.msi d'utiliser le point d'état de secours nommé SMSFP01.  

> [!NOTE]  
>  Si la valeur d’un paramètre contient des espaces, placez-la entre guillemets.  


> [!IMPORTANT]  
>  Si vous avez étendu le schéma Active Directory pour Configuration Manager, le site publie de nombreuses propriétés d’installation du client dans les services de domaine Active Directory. Le client Configuration Manager lit automatiquement ces propriétés. Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory](about-client-installation-properties-published-to-active-directory-domain-services.md).  



##  <a name="ccmsetupexe-command-line-parameters"></a>Paramètres de ligne de commande de CCMSetup.exe  

### <a name=""></a>/?  

Ouvre la boîte de dialogue **CCMSetup**, qui affiche les paramètres de ligne de commande de ccmsetup.exe.  

Exemple : **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;Chemin\>  

 Spécifie l’emplacement de téléchargement des fichiers. Utilisez un chemin local ou UNC. Les fichiers sont téléchargés à l'aide du protocole SMB (server message block). Pour utiliser **/source**, le compte d’utilisateur Windows pour l’installation du client doit avoir les autorisations Lecture sur l’emplacement.

> [!NOTE]  
>  Vous pouvez utiliser le paramètre **/source** plusieurs fois dans une ligne de commande pour spécifier d’autres emplacements de téléchargement.  

 Exemple : **ccmsetup.exe /source:"\\\ordinateur\dossier"**  

### <a name="mpltserver"></a>/mp:&lt;serveur\>

 Spécifie un point de gestion source auquel les ordinateurs se connectent. Les ordinateurs utilisent ce point de gestion pour trouver le point de distribution le plus proche pour les fichiers d’installation. En l’absence de point de distribution ou si les ordinateurs ne peuvent pas télécharger les fichiers auprès des points de distribution au terme d’un délai de quatre heures, ils téléchargent les fichiers auprès du point de gestion spécifié.  

> [!IMPORTANT]  
>  Ce paramètre permet de spécifier un point de gestion initial utilisé par les ordinateurs qui recherchent une source de téléchargement. Il peut s’agir de n’importe quel point de gestion sur n’importe quel site. Elle *n’affecte pas* le client à un point de gestion.   

 Les ordinateurs téléchargent les fichiers via une connexion HTTP ou HTTPS, selon la configuration du rôle de système de site des connexions client. Si cette fonctionnalité est configurée, le téléchargement utilise la limitation BITS. Si tous les points de distribution et de gestion sont configurés seulement pour les connexions client HTTPS, vérifiez que l’ordinateur client a un certificat client valide.  

Vous pouvez utiliser le paramètre de ligne de commande **/mp** pour spécifier plusieurs points de gestion. Si l’ordinateur ne parvient pas à se connecter au premier, il essaie le suivant dans la liste spécifiée. Quand vous spécifiez plusieurs points de gestion, séparez les valeurs par des points-virgules.

Si le client se connecte à un point de gestion via HTTPS, vous devez en général spécifier le nom de domaine complet, et non le nom de l’ordinateur. La valeur doit correspondre au nom d’objet ou à l’autre nom d’objet du certificat PKI du point de gestion. Même si Configuration Manager permet d’utiliser un nom d’ordinateur dans le certificat pour les connexions intranet, il est recommandé d’utiliser un nom de domaine complet.

Exemple utilisant le nom d’ordinateur : `ccmsetup.exe /mp:SMSMP01`  

Exemple utilisant le nom de domaine complet : `ccmsetup.exe /mp:smsmp01.contoso.com`  

Ce paramètre peut spécifier l’URL d’une passerelle de gestion cloud. Utilisez cette URL pour installer le client sur un appareil Internet. Pour obtenir la valeur de ce paramètre, suivez les étapes ci-dessous :
- Créez une passerelle de gestion cloud.
- Sur un client actif, ouvrez une invite de commandes Windows PowerShell en tant qu’administrateur. 
- Exécutez la commande suivante : `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Ajoutez le préfixe « https:// » à utiliser avec le paramètre **/mp**.

Exemple pour l’utilisation de l’URL de la passerelle de gestion cloud : `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Si elle est spécifiée, l’URL de la passerelle de gestion cloud pour le paramètre **/mp** doit commencer par **https://**.


### <a name="retryltminutes"></a>/retry:&lt;Minutes\>

Intervalle entre les tentatives si CCMSetup.exe ne réussit pas à télécharger les fichiers d’installation. CCMSetup renouvelle les tentatives jusqu’à atteindre la limite indiquée dans le paramètre **downloadtimeout**.  

Exemple : `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Empêche l’exécution de CCMSetup comme service (comportement par défaut). Quand CCMSetup est exécuté en tant que service, il s’exécute dans le contexte du compte système local de l’ordinateur. Ce compte peut ne pas disposer des droits suffisants pour accéder aux ressources réseau nécessaires à l’installation. Avec **/noservice**, CCMSetup.exe s’exécute dans le contexte du compte d’utilisateur que vous utilisez pour démarrer l’installation. Par ailleurs, si vous utilisez un script pour exécuter CCMSetup.exe avec le paramètre **/service**, CCMSetup.exe s’arrête après démarrage du service et risque de ne pas retourner correctement les détails de l’installation.   

Exemple : `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Indique que CCMSetup doit s'exécuter comme un service qui utilise le compte système local.  

Exemple : `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Indique que le logiciel client doit être désinstallé. Pour plus d’informations, consultez [Guide pratique pour gérer des clients](../manage/manage-clients.md).  

Exemple : `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Ce paramètre spécifie que l’installation doit s’arrêter si une version du client est déjà installée.  

Exemple : `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Indique que CCMSetup doit forcer l’ordinateur client à redémarrer si nécessaire pour terminer l’installation. Si ce paramètre n’est pas spécifié, CCMSetup s’arrête quand un redémarrage est nécessaire. Il continue après le redémarrage manuel suivant.  

 Exemple : `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;Priorité\>

 Indique la priorité de téléchargement lorsque les fichiers d'installation du client sont téléchargés via une connexion HTTP. Les valeurs possibles sont les suivantes :  

-   FOREGROUND (avant-plan)  

-   HIGH (élevée)  

-   NORMAL (normale)  

-   LOW (faible)  

 La valeur par défaut est NORMAL.  

 Exemple : `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;Minutes\>

Durée (en minutes) pendant laquelle CCMSetup essaie de télécharger les fichiers d’installation avant d’arrêter. La valeur par défaut est de **1440** minutes (un jour).  

Exemple : `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

Quand cette propriété est spécifiée, le client utilise un certificat PKI qui inclut l’authentification du client, le cas échéant. Si le client ne peut pas trouver un certificat valide, il utilise une connexion HTTP avec un certificat auto-signé. Ce comportement est le même si ce paramètre n’est pas utilisé.

> [!NOTE]  
>  Dans certains cas, il n’est pas nécessaire de spécifier ce paramètre lors de l’installation d’un client ; vous utilisez alors néanmoins un certificat client. C’est le cas, notamment, de l’installation d’un client via une installation Push et de l’installation d’un client basée sur un point de mise à jour logicielle. Toutefois, vous devrez spécifier ce paramètre à chaque fois que vous installerez un client manuellement et utiliser le paramètre **/mp** pour indiquer un point de gestion configuré pour accepter uniquement les connexions client HTTPS. Il est aussi nécessaire de préciser ce paramètre pour installer un client à des fins de communication Internet uniquement. Utilisez la propriété CCMALWAYSINF=1 conjointement avec les propriétés correspondant au point de gestion Internet (CCMHOSTNAME) et le code de site (SMSSITECODE). Pour plus d’informations sur la gestion des clients Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Exemple : `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Spécifie qu’un client ne doit pas vérifier la liste de révocation de certificats (CRL) quand il communique via HTTPS avec un certificat PKI.  

 Quand cette propriété n’est pas spécifiée, le client vérifie la liste de révocation de certificats avant d’établir une connexion HTTPS.  

 Pour plus d’informations sur la vérification de la liste de révocation de certificats par le client, consultez [Planification de la révocation de certificats PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

 Exemple : `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;fichier_configuration\>

Spécifie le nom d’un fichier texte qui répertorie les propriétés d’installation du client.

- Si vous ne spécifiez pas le paramètre **/noservice** de CCMSetup, ce fichier doit se trouver dans le dossier CCMSetup, c’est-à-dire %Windir%\\Ccmsetup pour les systèmes d’exploitation 32 bits et 64 bits.
- Si le paramètre **/noservice** est précisé, ce fichier doit se trouver dans le dossier à partir duquel vous exécutez CCMSetup.exe.  

Exemple : `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Pour fournir le format de fichier correct, utilisez le fichier mobileclienttemplate.tcf qui se trouve dans le répertoire &lt;Configuration Manager\>\\bin\\&lt;plateforme\> sur le serveur de site . Ce fichier contient également des commentaires sur les sections et leur utilisation. Spécifiez les propriétés d'installation du client dans la section [Client Install], à la suite du texte ci-après : **Install=INSTALL=ALL**.  

Exemple d’entrée de section [Client Install] : `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nom_fichier\>

 Spécifie que CCMSetup.exe ne doit pas installer le programme prérequis spécifié lors de l’installation du client Configuration Manager. Ce paramètre accepte plusieurs valeurs. Pour séparer chaque valeur, utilisez le point-virgule (;).  


 Exemples : `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` ou `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 Spécifiez que CCMSetup.exe désinstalle le client existant et installe un nouveau client.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;fonctionnalité\>

Spécifie que CCMSetup.exe n’installe pas la fonctionnalité spécifiée lors de l’installation du client.  

Exemple : `CCMSetup.exe /ExcludeFeatures:ClientUI` n’installe pas le Centre logiciel sur le client.  

> [!NOTE]  
>  **ClientUI** est la seule valeur prise en charge avec le paramètre **/ExcludeFeatures**.  



##  <a name="ccmsetupReturnCodes"></a> Codes de retour de CCMSetup.exe  
 La commande CCMSetup.exe fournit les codes de retour suivants à la fin de son exécution. Pour résoudre les problèmes, examinez le fichier ccmsetup.log sur l’ordinateur client pour déterminer le contexte et obtenir des détails supplémentaires sur les codes de retour.  

|Code de retour|Signification|  
|-----------------|-------------|  
|0|Opération réussie|  
|6|Erreur|  
|7|Redémarrage obligatoire|  
|8|Programme d’installation déjà en cours d’exécution|  
|9|Échec d’évaluation de condition préalable|  
|10|Échec de validation de hachage de manifeste de configuration|  



## <a name="ccmsetupMsiProps"></a> Propriétés de Ccmsetup.msi  
 Les propriétés suivantes peuvent modifier le comportement à l’installation de ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD 

Spécifie des propriétés et des paramètres de ligne de commande qui sont transmis à ccmsetup.exe après son installation par ccmsetup.msi. Placez les autres propriétés entre guillemets. Utilisez cette propriété lors de l’amorçage du client Configuration Manager à l’aide de la méthode d’installation d’Intune MDM. 

Exemple : `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

 > [!Tip]
 > Microsoft Intune limite la ligne de commande à 1 024 caractères. 



##  <a name="clientMsiProps"></a> Propriétés de Client.msi  
 Les propriétés suivantes peuvent modifier le comportement d’installation de client.msi. Si vous utilisez la méthode d'installation push du client, vous pouvez également spécifier les propriétés sous l'onglet **Client** de la boîte de dialogue **Propriétés de l'installation push du client** .  


### <a name="aadclientappid"></a>AADCLIENTAPPID

Spécifie l’identificateur d’application cliente Azure Active Directory (Azure AD). L’application cliente est créée ou importée quand vous [configurez des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la gestion cloud. Un administrateur Azure peut obtenir la valeur de cette propriété auprès du portail Azure. Pour plus d’informations, consultez [Obtenir l’ID de l’application](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key). Pour la propriété **AADCLIENTAPPID**, cet ID d’application concerne le type d’application « Native ».

Exemple : `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

Spécifie l’identificateur d’application serveur Azure AD. L’application serveur est créée ou importée quand vous [configurez des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la gestion cloud. Lors de la création de l’application serveur, dans la boîte de dialogue Créer une application serveur, cette propriété est **l’URI ID d’application**.

Un administrateur Azure peut obtenir la valeur de cette propriété auprès du portail Azure. Dans le panneau **Azure Active Directory**, recherchez l’application serveur sous **Inscriptions des applications**. Cette application est du type « Application/API web ». Ouvrez l’application, cliquez sur **Paramètres**, puis sur **Propriétés**. Utilisez la valeur de **URI ID d’application** pour cette propriété d’installation du client AADRESOURCEURI.

Exemple : `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

Spécifie l’identificateur du locataire Azure AD. Ce client est lié à Configuration Manager quand vous [configurez des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la gestion cloud. Pour obtenir la valeur de cette propriété, utilisez les étapes suivantes :
- Sur un appareil Windows 10 qui est joint au même locataire Azure AD, ouvrez une invite de commandes.
- Exécutez la commande suivante : `dsregcmd.exe /status`
- Dans la section État de l’appareil, recherchez la valeur de **TenantId**. Par exemple, `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

 > [!Note]
 > Un administrateur Azure peut également obtenir cette valeur dans le portail Azure. Pour plus d’informations, consultez [Obtenir l’ID de locataire](/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-tenant-id).

Exemple : `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Indique un ou plusieurs groupes ou comptes d'utilisateurs Windows auxquels accorder l'accès aux paramètres et stratégies du client. Cette propriété est utile si l’administrateur de Configuration Manager ne dispose pas d’informations d’identification d’administration locale sur l’ordinateur client. Indiquez une liste de comptes séparés par des points-virgules.  

Exemple : `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Spécifie que l’ordinateur est autorisé à redémarrer si nécessaire après l’installation du client.  

> [!IMPORTANT]  
>  L’ordinateur redémarre sans avertissement, même si un utilisateur y est connecté.  

Exemple : **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Définissez sa valeur sur **1** pour spécifier que le client est toujours un client Internet et ne se connecte jamais à l’intranet. Le type de connexion du client affiche **Toujours Internet**.  

 Utilisez cette propriété en combinaison avec CCMHOSTNAME, qui spécifie le nom de domaine complet du point de gestion Internet. Utilisez-la également avec le paramètre /UsePKICert de CCMSetup et avec le code de site.  

 Pour plus d’informations sur la gestion des clients Internet, consultez [Éléments à prendre en considération pour les communications de clients à partir d’Internet ou d’une forêt non approuvée](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Exemple : `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Spécifie la liste des émetteurs de certificats, qui est une liste de certificats issus d’autorités de certification racines de confiance que le site Configuration Manager a approuvées.  

 Pour plus d’informations sur la liste des émetteurs de certificats et sur la façon dont les clients l’utilisent lors du processus de sélection de certificat, consultez [Planification de la sélection des certificats client PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

 Cette valeur est une correspondance qui respecte la casse pour les attributs d’objet qui se trouvent dans le certificat d’autorité de certification racine. Les attributs peuvent être séparés par une virgule (,) ou un point-virgule (;). Spécifiez plusieurs certificats d’autorité de certification racine en utilisant une barre de séparation. Exemple :  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Pour copier **CertificateIssuers=&lt;chaîne\>** pour le site, référencez le fichier mobileclient.tcf dans le dossier du &lt;répertoire Configuration Manager\>\bin\\&lt;plateforme\> sur le serveur de site.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Spécifie les critères de sélection des certificats si le client a plusieurs certificats pour la communication HTTPS. Ce certificat est un certificat valide incluant les fonctionnalités d’authentification du client.  

 Vous pouvez rechercher une correspondance exacte (utilisez **Subject:**) ou une correspondance partielle (utilisez **SubjectStr:)** dans le nom d’objet ou l’autre nom de l’objet. Exemples :  

 `CCMCERTSEL="Subject:computer1.contoso.com"` recherche un certificat avec une correspondance exacte au nom d’ordinateur « computer1,contoso.com » dans le nom d’objet ou l’autre nom de l’objet.  

 `CCMCERTSEL="SubjectStr:contoso.com"` recherche un certificat contenant « contoso.com » dans le nom d’objet ou l’autre nom de l’objet.  

 Vous pouvez également utiliser un identificateur d'objet (OID) ou des attributs de nom unique dans les attributs du nom d'objet ou de l'autre nom de l'objet, par exemple :  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` recherche l’attribut d’unité organisationnelle exprimé comme identificateur d’objet et nommé Computers.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` recherche l’attribut d’unité organisationnelle exprimé comme nom unique et nommé Computers.  

> [!IMPORTANT]  
>  Si vous utilisez la zone Nom d’objet, **Subject:** respecte la casse, mais **SubjectStr:** ne la respecte pas.  
>   
>  Si vous utilisez la zone Autre nom de l’objet, **Subject:** et **SubjectStr:** respectent la casse tous les deux.  

 La liste complète des attributs que vous pouvez utiliser pour la sélection de certificat figure dans [Valeurs d’attribut prises en charge pour les critères de sélection de certificat PKI](#BKMK_attributevalues).  

 Si plusieurs certificats correspondent à la recherche et si la propriété que CCMFIRSTCERT a été définie sur 1, le certificat dont la période de validité est la plus longue est sélectionné.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Spécifie un autre nom de magasin de certificats si le certificat client pour HTTPS ne se trouve pas dans le magasin de certificats par défaut de **Personnel** du magasin Ordinateur.  

 Exemple : `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Active l’enregistrement du débogage dans le journal (journalisation). Les valeurs peuvent être définies sur 0 (désactivée, par défaut) ou sur 1 (activée). Cette propriété fait que le client enregistre dans le journal des informations détaillées pour le dépannage. Au titre de bonne pratique, évitez d’utiliser cette propriété dans les sites en production. Cela peut aboutir à une journalisation excessive, ce qui peut rendre difficile la recherche des informations pertinentes dans les fichiers journaux. Définissez aussi CCMENABLELOGGING sur TRUE pour activer la journalisation du débogage.  

  Exemple : `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Par défaut, cette propriété est définie sur TRUE pour activer la journalisation. Les fichiers journaux sont stockés dans le dossier **Logs** du dossier d’installation du client Configuration Manager. Par défaut, ce dossier est %Windir%\CCM\Logs.  

  Exemple : `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 Fréquence d’exécution de l’outil d’évaluation de l’intégrité du client (ccmeval.exe). La valeur peut être comprise entre **1** et **1440** minutes. Par défaut, il est exécuté une fois par jour.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 Heure d’exécution de l’outil d’évaluation de l’intégrité du client (ccmeval.exe), entre **0** (minuit) et **23** (23 h). S’exécute à minuit par défaut.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Si la valeur est définie sur 1, cette propriété spécifie que le client doit sélectionner le certificat PKI dont la période de validité est la plus longue. Ce paramètre peut être nécessaire si vous utilisez la protection d’accès réseau avec application d’IPsec.  

 Exemple : `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 Si le client est géré sur Internet, cette propriété spécifie le nom de domaine complet du point de gestion Internet.  

 Ne spécifiez pas cette option avec la propriété d’installation SMSSITECODE=AUTO. Les clients Internet doivent être affectés directement à leur site Internet.  

 Exemple : `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Cette propriété peut spécifier l’adresse d’une passerelle de gestion cloud. Pour obtenir la valeur de cette propriété, utilisez les étapes suivantes :
- Créez une passerelle de gestion cloud.
- Sur un client actif, ouvrez une invite de commandes Windows PowerShell en tant qu’administrateur. 
- Exécutez la commande suivante : `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Utilisez la valeur retournée telle quelle avec la propriété **CCMHOSTNAME**.

Exemple : `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Quand vous spécifiez l’adresse d’une passerelle de gestion cloud pour la propriété **CCMHOSTNAME**, n’ajoutez *pas* un préfixe comme **https://**. Ce préfixe est utilisé seulement avec l’URL **/mp** d’une passerelle de gestion cloud.



### <a name="ccmhttpport"></a>CCMHTTPPORT

 Indique le port que le client doit utiliser lors de la communication sur HTTP avec des serveurs de système de site. Le port 80 est le port par défaut.  

 Exemple : `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Indique le port que le client doit utiliser lors de la communication sur HTTPS avec des serveurs de système de site. Le port 443 est le port par défaut.  

Exemple : `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Indique le dossier dans lequel les fichiers du client Configuration Manager sont installés, *%Windir%* \CCM par défaut. Quel que soit l’emplacement d’installation de ces fichiers, le fichier Ccmcore.dll est toujours installé dans le dossier *%Windir%\System32*. En outre, sur un système d’exploitation 64 bits, une copie du fichier Ccmcore.dll est toujours installée dans le dossier *%Windir%* \SysWOW64. Ce fichier prend en charge les applications 32 bits qui utilisent la version 32 bits des API client du SDK Configuration Manager.  

 Exemple : `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Indique le niveau de détails à écrire dans les fichiers journaux de Configuration Manager. Spécifiez un entier entre 0 et 3, où 0 représente la journalisation la plus complète et où 3 ne consigne que les erreurs. La valeur par défaut est 1.  

Exemple : `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quand un fichier journal de Configuration Manager atteint la taille maximale, le client le renomme en tant que sauvegarde et crée un nouveau fichier journal. La taille maximale est de 250 000 octets par défaut ou celle de la valeur spécifiée par la propriété CCMLOGMAXSIZE.

Cette propriété spécifie combien de versions précédentes du fichier journal doivent être conservées. La valeur par défaut est 1. Si la valeur est définie sur 0, aucun ancien fichier journal n'est conservé.  

Exemple : `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Taille maximale du fichier journal, en octets. Quand un journal atteint la taille spécifiée, le client le renomme en tant que fichier d’historique et crée un nouveau fichier. Cette propriété doit être définie sur au moins 10 000 octets. La valeur par défaut est de 250 000 octets.  

Exemple : `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Si elle est définie sur TRUE, cette propriété désactive la possibilité pour les utilisateurs administratifs de changer le site affecté dans le panneau de configuration de **Configuration Manager**.  

 Exemple : **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Si elle est définie sur TRUE, cette propriété désactive la possibilité pour les utilisateurs administratifs de changer les paramètres du dossier du cache client dans le panneau de configuration de **Configuration Manager**.  

Exemple : `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Spécifie un domaine DNS pour que les clients localisent les points de gestion qui sont publiés dans DNS. Lorsqu'un point de gestion est localisé, il indique au client d'autres points de gestion dans la hiérarchie. Ce comportement signifie qu’il n’est pas nécessaire que le point de gestion localisé à l’aide de la publication DNS provienne du site du client, mais qu’il peut s’agir de n’importe quel point de gestion de la hiérarchie.  

> [!NOTE]  
>  Vous ne devez pas spécifier cette propriété si le client se trouve dans le même domaine qu’un point de gestion publié. Dans ce cas, le domaine du client est automatiquement utilisé pour rechercher des points de gestion dans DNS.  

 Pour plus d’informations sur la publication DNS comme méthode de localisation de services pour les clients Configuration Manager, consultez [Emplacement du service et façon dont les clients déterminent leur point de gestion attribué](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

> [!NOTE]  
>  Par défaut, la publication DNS n’est pas activée dans Configuration Manager.  

 Exemple : `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Indique le point d’état de secours qui reçoit et traite les messages d’état envoyés par les ordinateurs clients Configuration Manager.  

Pour plus d’informations sur le point d’état de secours, consultez [Déterminer si vous avez besoin d’un point d’état de secours](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

Exemple : `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Spécifie que la présence de la version minimale requise de Microsoft Application Virtualization (App-V) n’est pas vérifiée avant l’installation du client.  

> [!IMPORTANT]  
>  Si vous installez le client Configuration Manager sans installer App-V, vous ne pouvez pas déployer des applications virtuelles.  

 Exemple : `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Spécifie que le client signale l’état, mais ne corrige pas les problèmes qu’il trouve.  

Exemple : `CCMSetup.exe NOTIFYONLY=TRUE`  

Pour plus d’informations, consultez [Guide pratique pour configurer l’état du client](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Si un client a la mauvaise clé racine approuvée de Configuration Manager et ne peut pas contacter de point de gestion approuvé pour recevoir la nouvelle clé racine approuvée, utilisez cette propriété pour supprimer manuellement l’ancienne clé racine approuvée. Cette situation peut se produire quand vous déplacez un client d’une hiérarchie de site à une autre. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS.  

 Exemple : `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Permet la réattribution de site automatique pour les mises à niveau du client si cette propriété est utilisée avec [SMSSITECODE](#smssitecode)=AUTO.

Exemple : `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Spécifie l'emplacement du dossier de cache du client sur l'ordinateur client, qui stocke les fichiers temporaires. Par défaut, l’emplacement est *%Windir\ccmcache*.  

Exemple : `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Cette propriété peut être utilisée avec la propriété SMSCACHEFLAGS pour contrôler l’emplacement du dossier du cache du client.  

Exemple : `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` installe le dossier du cache du client sur le lecteur de disque disponible le plus grand du client.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Spécifie davantage les détails d'installation pour le dossier mis dans la mémoire cache du client. Vous pouvez utiliser les propriétés de SMSCACHEFLAGS individuellement ou en combinaison, séparées par des points-virgules. Si cette propriété n’est pas spécifiée, le dossier du cache client est installé en fonction de la propriété SMSCACHEDIR, il n’est pas compressé et la valeur de SMSCACHESIZE est utilisée pour sa taille en Mo.  

Ce paramètre est ignoré lorsque vous mettez à niveau un client existant.  

Propriétés :  

-   PERCENTDISKSPACE : indique la taille du dossier sous forme de pourcentage de l’espace disque total. Si vous indiquez cette propriété, vous devez également indiquer la propriété SMSCACHESIZE comme valeur de pourcentage à utiliser.  

-   PERCENTFREEDISKSPACE : indique la taille du dossier sous forme de pourcentage de l’espace disque disponible. Si vous indiquez cette propriété, vous devez également indiquer la propriété SMSCACHESIZE comme valeur de pourcentage à utiliser. Par exemple, si le disque dispose de 10 Mo libres et que SMSCACHESIZE indique 50, cela signifie que la taille du dossier est définie sur 5 Mo. Vous ne pouvez pas utiliser cette propriété avec la propriété PERCENTDISKSPACE.  

-   MAXDRIVE : indique que le dossier doit être installé sur le disque le plus volumineux disponible. Cette valeur est ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

-   MAXDRIVESPACE : indique que le dossier doit être installé sur le lecteur de disque possédant l’espace disponible le plus important. Cette valeur est ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

-   NTFSONLY : indique que le dossier peut être installé uniquement sur des lecteurs de disque NTFS. Cette valeur est ignorée si un chemin a été spécifié avec la propriété SMSCACHEDIR.  

-   COMPRESS : spécifie que le dossier doit être conservé sous une forme compressée.  

-   FAILIFNOSPACE : indique que le logiciel client doit être supprimé si l’espace est insuffisant pour installer le dossier.  

Exemple : `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Des paramètres client sont disponibles pour spécifier la taille du dossier du cache client. L’ajout de ces paramètres du client remplace l’utilisation de SMSCACHESIZE comme propriété client.msi pour spécifier la taille du cache du client. Pour plus d’informations, consultez les [paramètres du client pour la taille du cache](about-client-settings.md#client-cache-settings).  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  Si un nouveau package qui doit être téléchargé peut provoquer le dépassement de la taille maximale du dossier et que le dossier ne peut pas être vidé pour libérer un espace suffisant, le téléchargement du package échoue, et le programme ou l’application ne s’exécute pas.  

Ce paramètre est ignoré quand vous mettez à niveau un client existant et quand le client télécharge des mises à jour logicielles.  

Exemple : `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Si vous réinstallez un client, vous ne pouvez pas utiliser les propriétés d’installation SMSCACHESIZE ou SMSCACHEFLAGS pour définir une taille de cache inférieure à la taille antérieure. Si vous essayez d’effectuer cette action, votre valeur est ignorée. La taille du cache est automatiquement définie à la taille antérieure.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Indique l’emplacement et l’ordre dans lesquels le programme d’installation de Configuration Manager vérifie les paramètres de configuration. La propriété est une chaîne d’un ou plusieurs caractères, chacun définissant une source de configuration spécifique. Utilisez les caractères R, P, M et U seuls ou en combinaison :  

-   R : vérification des paramètres de configuration dans le Registre.  

   Pour plus d’informations, consultez [Informations sur le stockage des propriétés d’installation du client dans le Registre](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

-   P : vérification des paramètres de configuration dans les propriétés d’installation fournies à l’invite de commandes.  

-   M : vérification des paramètres existants à l’occasion de la mise à niveau d’un ancien client avec le logiciel client Configuration Manager.  

-   U : mise à niveau du client installé vers une version plus récente (et utilisation du code de site attribué).  

 Par défaut, l’installation du client utilise `PU` pour vérifier d’abord les propriétés d’installation, puis les paramètres existants.  

 Exemple : `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Indique si le client peut utiliser les services WINS (Windows Internet Name Service) pour trouver un point de gestion qui accepte les connexions HTTP. Les clients utilisent cette méthode quand ils ne peuvent pas trouver de point de gestion dans les services de domaine Active Directory ou dans DNS.  

 Cette propriété n’a pas d’impact sur le fait que le client utilise ou non WINS pour la résolution de noms.  

 Vous pouvez configurer deux modes différents pour cette propriété :  

-   NOWINS : cette valeur est le paramètre le plus sûr pour cette propriété et empêche les clients de rechercher un point de gestion dans WINS. Lorsque vous utilisez ce paramètre, les clients doivent disposer d'une autre méthode de localisation d'un point de gestion sur l'Intranet, telle que les services de domaine Active Directory ou en utilisant la publication DNS.  

-   WINSSECURE (valeur par défaut) : dans ce mode, un client qui utilise la communication HTTP peut utiliser WINS pour trouver un point de gestion. Toutefois, le client doit disposer d'une copie de la clé racine approuvée avant de pouvoir se connecter correctement au point de gestion. Pour plus d’informations, voir [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  


 Exemple : `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Spécifie un point de gestion initial à utiliser par le client Configuration Manager.  

> [!IMPORTANT]  
>  Si le point de gestion accepte uniquement les connexions clientes sur HTTPS, vous devez ajouter le préfixe https:// au nom du point de gestion.  

Exemple : `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Exemple : `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Indique la clé racine approuvée de Configuration Manager lorsque celle-ci ne peut pas être récupérée à partir des services de domaine Active Directory. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS. Pour plus d’informations, voir [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Exemple : `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Utilisée pour réinstaller la clé racine approuvée de Configuration Manager. Indique le chemin d'accès complet et le nom de fichier d'un fichier contenant la clé racine approuvée. Cette propriété s'applique aux clients qui utilisent la communication client HTTP et HTTPS. Pour plus d’informations, voir [Planification de la clé racine approuvée](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Exemple : 'CCMSetup.exe SMSROOTKEYPATH=&lt;chemin_complet_et_nom_de_fichier\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Spécifie le chemin d'accès complet et le nom de fichier .cer du certificat auto-signé exporté sur le serveur de site.  

 Ce certificat est stocké dans le magasin de certificats **SMS** et porte le nom d'objet **Serveur de site** et le nom convivial **Certificat de signature du serveur de site**.  

 Exemple : **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;chemin _complet_et_nom_de_fichier\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Spécifie le site Configuration Manager auquel affecter le client. Cette valeur peut être un code de site à trois caractères ou le mot AUTO. Si vous spécifiez AUTO ou si vous ne spécifiez pas cette propriété, le client tente de déterminer l’affectation de son site à partir des services de domaine Active Directory ou d’un point de gestion spécifié. Pour activer AUTO pour les mises à niveau du client, vous devez également affecter à [SITEREASSIGN](#sitereassign) la valeur TRUE.    

> [!NOTE]  
>  N’utilisez pas AUTO si vous spécifiez également le point de gestion Internet (CCMHOSTNAME). Dans ce cas, vous devez directement attribuer le client à son site.  

 Exemple : `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valeurs d’attribut prises en charge pour les critères de sélection de certificat PKI  
 Configuration Manager prend en charge les valeurs d’attribut suivantes pour les critères de sélection de certificat PKI :  

|Attribut d'OID|Attribut de nom unique|Définition de l'attribut|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Composant de domaine|  
|1.2.840.113549.1.9.1|E ou E-mail|Adresse de messagerie|  
|2.5.4.3|CN|Nom commun|  
|2.5.4.4|SN|Nom d'objet|  
|2.5.4.5|SERIALNUMBER|Numéro de série|  
|2.5.4.6|C|Code du pays|  
|2.5.4.7|L|Localité|  
|2.5.4.8|S ou ST|Nom de département/province|  
|2.5.4.9|STREET|Adresse|  
|2.5.4.10|O|Nom de l'organisation|  
|2.5.4.11|OU|Unité d'organisation|  
|2.5.4.12|T ou Title|Titre|  
|2.5.4.42|G ou GN ou GivenName|Prénom|  
|2.5.4.43|I ou Initials|Initiales|  
|2.5.29.17|(aucune valeur)|Autre nom de l'objet|  
