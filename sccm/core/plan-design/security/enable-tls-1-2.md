---
title: Comment activer TLS 1.2
titleSuffix: Configuration Manager
description: Informations sur la façon d’activer TLS 1.2 pour Configuration Manager.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ddd2a5cb74dfc9de48299b00fddeb8f849ce9e3
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748160"
---
# <a name="how-to-enable-tls-12"></a>Comment activer TLS 1.2

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit comment activer TLS 1.2 pour Configuration Manager, y compris pour des composants individuels. La mise à jour des exigences pour des fonctionnalités couramment utilisées et le dépannage de problèmes courants, sont également décrits dans cet article.

Configuration Manager s’appuie sur de nombreux composants différents pour sécuriser la communication. Le protocole qui est utilisé pour une connexion donnée dépend des capacités de tous les composants requis. Si un composant est obsolète, la communication peut utiliser un protocole plus ancien et moins sécurisé.

Pour activer correctement Configuration Manager pour prendre en charge TLS 1.2, activez d’abord TLS 1.2 pour tous les composants requis. Les composants requis dépendent de votre environnement et des fonctionnalités de Configuration Manager que vous utilisez.

Démarrez ce processus avec les clients, en particulier les versions précédentes de Windows. Avant d’activer TLS 1.2 sur les serveurs Configuration Manager, assurez-vous que tous les clients prennent en charge TLS 1.2. Sinon, les clients ne pourront pas communiquer avec les serveurs et risquent d’être orphelins.


## <a name="tasks-for-features-and-scenarios"></a>Tâches pour les fonctionnalités et les scénarios

Pour activer TLS 1.2 pour les composants desquels dépend Configuration Manager pour une communication sécurisée, vous devez :

- [Activer le protocole TLS 1.2 en tant que fournisseur de sécurité](#enable-tls-12-protocol-as-a-security-provider)
- [Mettre à jour .NET Framework pour prendre en charge TLS 1.2](#update-net-framework-to-support-tls-12)
- [Mettre à jour SQL Server et les composants clients](#update-sql-server-and-client-components)
- [Mettre à jour Windows et WinHTTP sur Windows 8.0, Windows Server 2012 R2 et versions antérieures](#update-windows-and-winhttp)
- [Mettre à jour Windows Server Update Services (WSUS)](#update-windows-server-update-services-wsus)

Cette section décrit les dépendances pour les scénarios et fonctionnalités spécifiques de Configuration Manager. Pour déterminer les prochaines étapes, recherchez les éléments qui s’appliquent à votre environnement.

|Fonctionnalité ou scénario|Tâches de mise à jour|
|--- |--- |
|Serveurs du site (central, principal ou secondaire)| - [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Vérifier les paramètres de chiffrement fort|
|Serveur de bases de données du site|[Mettre à jour SQL Server et ses composants clients](#update-sql-server-and-client-components)|
|Serveurs de sites secondaires|[Mettre à jour SQL Server et ses composants clients](#update-sql-server-and-client-components) vers une version compatible de SQL Express|
|Rôles système de site| - [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12) et vérifier les paramètres de chiffrement fort <br/> - [Mettre à jour SQL Server et ses composants clients](#update-sql-server-and-client-components) sur les rôles qui le nécessitent, notamment [SQL Server Native Client](#sql-server-native-client)|
|Point de Reporting Services|- [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12) sur le site du serveur, les serveurs SQL Reporting Services et tous les ordinateurs avec la console<br/> - Redémarrer le service SMS_Executive en fonction des besoins|
|Point de mise à jour logicielle|[Mettre à jour WSUS](#update-windows-server-update-services-wsus)|
|Console Configuration Manager| - [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Vérifier les paramètres de chiffrement fort|
|Client Configuration Manager avec les rôles de système de site HTTPS|[Mettre à jour Windows pour prendre en charge TLS 1.2 pour les communications client-serveur à l’aide de WinHTTP](#update-windows-and-winhttp)|
|Centre logiciel| - [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12)<br/> - Vérifier les paramètres de chiffrement fort|
|Clients Windows 7| *Avant* d’activer TLS 1.2 sur les composants serveur, [mettre à jour Windows pour prendre en charge TLS 1.2 pour les communications client-serveur à l’aide de WinHTTP](#update-windows-and-winhttp). Si vous activez d’abord TLS 1.2 sur les composants serveur, vous risquez de rendre orphelines des versions antérieures de clients.|


## <a name="enable-tls-12-protocol-as-a-security-provider"></a>Activer le protocole TLS 1.2 en tant que fournisseur de sécurité

Vérifiez le paramètre de sous-clé de registre `\SecurityProviders\SCHANNEL\Protocols`, comme illustré dans [Meilleures pratiques du protocole TLS avec la fonctionnalité .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry).

> [!NOTE]
> TLS 1.2 est activé par défaut. Par conséquent, aucune modification de ces clés n’est requise pour l’activer. Vous pouvez apporter des modifications sous Protocoles pour désactiver TLS 1.0 et TLS 1.1, une fois que vous avez suivi le reste des conseils dans cet article et que vous avez vérifié que l’environnement fonctionne en ayant uniquement TLS 1.2 activé.


## <a name="update-net-framework-to-support-tls-12"></a>Mettre à jour .NET Framework pour prendre en charge TLS 1.2

### <a name="determine-net-version"></a>Déterminer la version .NET

Tout d’abord, déterminez votre numéro de version de .NET. Pour plus d’informations, consultez [Comment déterminer les versions et les niveaux de Service Pack de Microsoft .NET Framework installés](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

### <a name="install-net-updates"></a>Installer des mises à jour .NET

Certaines versions de .NET Framework peuvent nécessiter des mises à jour pour activer le chiffrement fort. Utilisez ces lignes directrices :

- NET Framework 4.6.2 et versions ultérieures prend en charge TLS 1.1 et TLS 1.2. Confirmer les paramètres du Registre, mais aucune modification supplémentaire n’est requise.

- Mettre à jour NET Framework 4.6 et versions antérieures pour prendre en charge TLS 1.1 et TLS 1.2. Pour plus d’informations, consultez [Versions et dépendances du .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Si vous utilisez .NET Framework 4.5.1 ou 4.5.2 sur Windows 8.1 ou Windows Server 2012, les mises à jour appropriées et les informations détaillées sont également disponibles à partir du [Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=42883).

### <a name="configure-for-strong-cryptography"></a>Configuration pour le chiffrement fort

Configurer .NET framework pour prendre en charge le chiffrement fort. Définissez le paramètre du registre `SchUseStrongCrypto` sur `DWORD:00000001`. Cette valeur désactive le chiffrement de flux RC4 et nécessite un redémarrage. Pour plus d’informations sur ce paramètre, consultez [Avis de sécurité Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Veillez à définir les clés de Registre suivantes sur tous les ordinateurs qui communiquent sur le réseau avec un système prenant en charge TLS 1.2. Par exemple, les clients Configuration Manager, ou tout rôle de système de site distant non installé sur le serveur du site.

Pour les applications 32 bits qui s’exécutent sur des systèmes 32 bits ou les applications 64 bits qui s’exécutent sur des systèmes 64 bits, mettez à jour la valeur de la sous-clé suivante :

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

Pour les applications 32 bits qui s’exécutent sur des systèmes 64 bits, mettez à jour la valeur de la sous-clé suivante :

```Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> Le paramètre `SchUseStrongCrypto` permet à .NET d’utiliser TLS 1.1 et TLS 1.2. Le paramètre `SystemDefaultTlsVersions` permet à .NET d’utiliser la configuration du système d’exploitation. Pour plus d’informations, consultez [Bonnes pratiques TLS avec .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls).


## <a name="update-sql-server-and-client-components"></a>Mettre à jour SQL Server et les composants clients

Microsoft SQL Server 2016 et les versions ultérieures prennent en charge TLS 1.1 et TLS 1.2. Les versions antérieures et les bibliothèques dépendantes peuvent nécessiter des mises à jour. Pour plus d’informations, consultez [KB 3135244 : support TLS 1.2 pour Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

Les serveurs de sites secondaires doivent utiliser au moins SQL Server 2016 Express avec Service Pack 2 (13.2.50.26) ou version ultérieure.

### <a name="sql-server-native-client"></a>SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) décrit également les exigences pour les composants clients SQL Server.

Veillez également à mettre à jour SQL Server Native Client avec au moins SQL 2012 SP4 (11.*.7001.0). Depuis la version 1810, cette exigence constitue une [vérification de la configuration requise (avertissement)](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-server-native-client).

Configuration Manager utilise SQL Server Native Client sur les rôles de système de site suivants :

- Serveur de bases de données du site
- Serveur de site : site d’administration centrale, site principal ou site secondaire
- Point de gestion
- Point de gestion d’appareil
- Point de migration d’état
- Fournisseur SMS
- Point de mise à jour logicielle
- Point de distribution multidiffusion
- Point de service de mise à jour Asset Intelligence
- Point de Reporting Services
- Service web du catalogue des applications
- Point d'inscription
- Point Endpoint Protection
- point de connexion de service
- Point d'enregistrement de certificat
- Point de service de l’entrepôt de données


## <a name="update-windows-and-winhttp"></a>Mettre à jour Windows et WinHTTP

Windows 8.1, Windows Server 2012 R2, Windows 10, Windows Server 2016 et les versions ultérieures de Windows offrent une prise en charge native de TLS 1.2 pour les communications client-serveur via WinHTTP.

Les versions antérieures de Windows, par exemple Windows 7 ou Windows Server 2012 n’activent pas TLS 1.1 ou 1.2 par défaut pour les communications client-serveur via HTTPS. Pour ces versions antérieures de Windows, installez [Mise à jour 3140245](https://support.microsoft.com/help/3140245) pour activer TLS 1.1 et TLS 1.2 en tant que protocoles sécurisés par défaut pour WinHTTP dans Windows. Définissez ensuite les valeurs de registre suivantes :

> [!IMPORTANT]
> Activez ces paramètres sur tous les clients *avant* d’activer TLS 1.2 sur les serveurs Configuration Manager. Sinon, vous risquez de les rendre orphelins par inadvertance.

Vérifiez la valeur du paramètre de registre `DefaultSecureProtocols`, par exemple :

```Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

Si vous avez modifié cette valeur, redémarrez l’ordinateur.

> [!Note]  
> L’exemple ci-dessus montre la valeur `0xAA0` pour le paramètre WinHTTP `DefaultSecureProtocols`. [KB 3140245 : Mettre à jour pour activer TLS 1.1 et TLS 1.2 en tant que protocoles sécurisés par défaut dans WinHTTP dans Windows](https://support.microsoft.com/help/3140245) répertorie la valeur hexadécimale pour chaque protocole. Par défaut dans Windows, cette valeur est `0x0A0` afin d’activer SSL 3.0 et TLS 1.0 pour WinHTTP. L’exemple ci-dessus conserve ces valeurs par défaut et active également TLS 1.1 et TLS 1.2 pour WinHTTP. Cette configuration garantit que la modification ne perturbe aucune autre application qui dépend toujours de SSL 3.0 ou TLS 1.0. Vous pouvez utiliser la valeur `0xA00` pour autoriser uniquement les TLS 1.1 et TLS 1.2. Configuration Manager prend en charge le protocole le plus sécurisé que Windows négocie entre les deux appareils.
>
> Si vous souhaitez complètement désactiver SSL 3.0 et TLS 1.0, utilisez le paramètre des protocoles SChannel désactivés dans Windows. Pour plus d’informations, consultez [Comment restreindre l’utilisation de certains algorithmes et protocoles de chiffrement dans Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).


## <a name="update-windows-server-update-services-wsus"></a>Mettre à jour Windows Server Update Services (WSUS)

Pour prendre en charge TLS 1.2 pour les communications client-serveur dans WSUS sur Windows Server 2012 et Windows Server 2012 R2, installez la mise à jour suivante sur le serveur WSUS :

- Pour le serveur WSUS qui exécute Windows Server 2012, installez la [mise à jour 4022721](https://support.microsoft.com/help/4022721) ou une mise à jour ultérieure.
- Pour le serveur WSUS qui exécute Windows Server 2012 R2, installez la [mise à jour 4022720](https://support.microsoft.com/help/4022720) ou une mise à jour ultérieure.


## <a name="known-issues"></a>Problèmes connus

Cette section fournit des conseils concernant les problèmes courants qui surviennent lorsque vous activez le support TLS 1.2.

### <a name="unsupported-platforms"></a>Plateformes non prises en charge

Les plates-formes clientes suivantes sont prises en charge par Configuration Manager, mais pas dans un environnement TLS 1.2 :

- Windows Server 2008
- Windows CE
- Apple OS X
- appareils Windows 10 gérés avec une solution MDM locale

### <a name="reports-dont-show-in-the-console"></a>Les rapports n’apparaissent pas dans la console

Si les rapports n’apparaissent pas dans la console Configuration Manager, veillez à mettre à jour l’ordinateur sur lequel vous exécutez la console. Vous devez [mettre à jour .NET Framework](#update-net-framework-to-support-tls-12) et activer le chiffrement fort.

### <a name="fips-security-policy-enabled"></a>Stratégie de sécurité FIPS activée

Si vous activez le paramètre de la stratégie de sécurité FIPS pour le client ou un serveur, la négociation Secure Channel (Schannel) peut entraîner l’utilisation de TLS 1.0. Ce comportement se produit même si vous désactivez le protocole dans le Registre.

Pour procéder à des recherches, activez la journalisation des événements du canal sécurisé, puis révisez les événements Schannel dans le journal système. Pour plus d’informations, consultez [Comment restreindre l’utilisation de certains algorithmes et protocoles de chiffrement dans Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Échec de communication de SQL Server

Si la communication de SQL Server échoue et retourne une erreur **SslSecurityError**, vérifiez les paramètres suivants :

- [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12) et activer le chiffrement fort sur chaque ordinateur
- [Mettre à jour SQL Server](#update-sql-server-and-client-components) sur le serveur hôte
- [Mettre à jour les composants clients SQL](#update-sql-server-and-client-components) sur tous les systèmes qui communiquent avec SQL. Par exemple, les serveurs de site, le fournisseur SMS et les serveurs de rôle de site.

### <a name="configuration-manager-client-communication-failures"></a>Échecs de communication avec le client Gestionnaire de configuration

Si le client Configuration Manager ne communique pas avec des rôles de site, vérifiez que vous avez [mis à jour Windows](#update-windows-and-winhttp) pour prendre en charge TLS 1.2 pour la communication client-serveur à l’aide de WinHTTP. Les rôles de site courants incluent les points de distribution, les points de gestion et les points de migration d'état.

### <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Un point de Reporting Services échoue et retourne une erreur attendue

Si le point de Reporting Services ne configure pas les rapports, consultez **SRSRP.log** pour vérifier l’erreur de saisie suivante :

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Pour résoudre ce problème, procédez comme suit :

1. [Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et activez le chiffrement fort sur tous les ordinateurs concernés.

1. Après avoir installé les mises à jour, redémarrez le service SMS_Executive.

### <a name="application-catalog-doesnt-initialize"></a>Le catalogue d’applications ne s’initialise pas

> [!Important]  
> Le catalogue des applications est déconseillé. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Si le catalogue d’applications ne s’initialise pas, consultez le fichier **ServicePortalWebSite.svclog** pour vérifier l’erreur de saisie suivante :

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Pour résoudre ce problème, procédez comme suit :

1. [Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et activez le chiffrement fort sur tous les ordinateurs concernés.

1. Dans le dossier `%WinDir%\System32\InetSrv` du serveur du catalogue d’applications, créez un fichier **W2SP.exe.config** contenant les éléments suivants :

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > Il s’agit du fichier par défaut créé si l’application était générée à l’aide de .NET Framework 4.6.3.

1. Utilisez la sécurité du transport HTTPS pour les rôles du catalogue d’applications.

    > [!Important]
    > Lorsque vous utilisez la sécurité des messages HTTP pour les rôles du catalogue d’applications, WCF est codé en dur pour utiliser SSL 3.0 et TLS 1.0 uniquement. Cela empêche l’utilisation de TLS 1.2.

1. Si vous avez apporté des modifications, redémarrez l’ordinateur.

### <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>Le Centre logiciel ou le navigateur ne communique pas avec le catalogue d’applications

> [!Important]  
> Le catalogue des applications est déconseillé. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

La meilleure méthode pour que le Centre logiciel fonctionne avec des applications disponibles pour l’utilisateur dans un site prenant en charge TLS 1.2 consiste à supprimer le rôle du catalogue d’applications. Autorisez ensuite le Centre logiciel à communiquer directement avec un point de gestion. Pour plus d’informations, consultez [Supprimer le catalogue des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

Si vous devez résoudre les échecs de communication entre le catalogue d’applications et le Centre logiciel, vérifiez les conditions suivantes :

- [Mettre à jour .NET Framework](#update-net-framework-to-support-tls-12) et activer le chiffrement fort sur chaque ordinateur.

- Après avoir apporté les modifications, redémarrez tous les ordinateurs concernés.

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

### <a name="service-connection-point-upload-failures"></a>Défaillances de chargement du point de connexion de service

Si le point de connexion de service ne charge pas des données vers SCCMConnectedService, [mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et activez le chiffrement fort sur chaque ordinateur. N’oubliez pas de redémarrer les ordinateurs une fois les modifications apportées.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La Console Configuration Manager affiche la boîte de dialogue Intégration Intune

Si la boîte de dialogue Intégration Intune s’affiche lorsque la console tente de se connecter au portail Intune, [mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et activez le chiffrement fort activé sur chaque ordinateur. N’oubliez pas de redémarrer les ordinateurs une fois les modifications apportées.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La console Configuration Manager affiche un échec de connexion à Azure

Lorsque vous tente de créer des applications dans Azure Active Directory (Azure AD), si la boîte de dialogue Intégration des Services Azure échoue immédiatement après avoir sélectionné **Connexion**, [mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et activez le chiffrement fort. N’oubliez pas de redémarrer les ordinateurs une fois les modifications apportées.

### <a name="configuration-manager-cloud-services-and-tls-12"></a>Services cloud Configuration Manager et TLS 1.2

Depuis la version 1802, les machines virtuelles Azure utilisées par la passerelle de gestion cloud et les points de distribution cloud prennent en charge TLS 1.2. Les clients pris en charge sur la version 1802 ou les versions ultérieures utilisent automatiquement TLS 1.2.

Le fichier **SMSAdminui.log** peut contenir une erreur similaire à l’exemple suivant :

```
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

Dans le journal des événements système, l’ID d’événement SChannel 36874 peut être consigné avec la description suivante : `An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->


## <a name="see-also"></a>Voir aussi

- [Meilleures pratiques Transport Layer Security (TLS) avec .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)

- [KB 3135244 : support TLS 1.2 pour Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

- [Informations techniques de référence sur les contrôles de chiffrement](cryptographic-controls-technical-reference.md)
