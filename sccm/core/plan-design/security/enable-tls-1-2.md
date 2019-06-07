---
title: Comment activer TLS 1.2
titleSuffix: Configuration Manager
description: Informations sur la façon d’activer TLS 1.2 pour Microsoft Configuration Manager.
ms.date: 05/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3641c3a9adce23f24a80135d996da03e12e78907
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355606"
---
# <a name="how-to-enable-tls-12-for-configuration-manager"></a>Comment activer TLS 1.2 pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit comment activer TLS 1.2 pour Configuration Manager, y compris pour des composants individuels. La mise à jour des exigences pour des fonctionnalités couramment utilisées et le dépannage de problèmes courants, sont également décrits dans cet article.

Configuration Manager s’appuie sur de nombreux composants différents pour sécuriser la communication. Le protocole qui est utilisé pour une connexion donnée dépend des capacités de tous les composants requis. Si un composant est obsolète, la communication peut utiliser un protocole plus ancien et moins sécurisé.

Pour activer correctement Configuration Manager pour prendre en charge TLS 1.2, vous devez activer TLS 1.2 pour tous les composants requis. Les composants requis dépendent de votre environnement et des fonctionnalités de Configuration Manager que vous utilisez.


## <a name="to-enable-tls-12"></a>Pour activer TLS 1.2

Pour activer TLS 1.2, vous devez d’abord activer TLS 1.2 en tant que fournisseur de sécurité pour chaque ordinateur exécutant ou interagissant avec Configuration Manager. Ensuite, activez TLS 1.2 pour les composants desquels dépend Configuration Manager pour une communication sécurisée.

### <a name="enable-the-tls-12-protocol-as-a-security-provider"></a>Activer le protocole TLS 1.2 en tant que fournisseur de sécurité

Vérifiez le paramètre de sous-clé de registre « \SecurityProviders\SCHANNEL\Protocols », comme illustré dans [Meilleures pratiques du protocole TLS avec la fonctionnalité .NET Framework](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry?).

> [!NOTE]
> TLS 1.2 est activé par défaut. Par conséquent, aucune modification de ces clés n’est requise pour l’activer. Vous pouvez apporter des modifications sous Protocoles pour désactiver TLS 1.0 et TLS 1.1, une fois que vous avez suivi le reste des conseils dans cet article et que vous avez vérifié que l’environnement fonctionne en ayant uniquement TLS 1.2 activé.

### <a name="enable-tls-12-for-dependent-components"></a>Activer TLS 1.2 pour des composants dépendants
Pour activer TLS 1.2 pour des composants desquels dépend Configuration Manager pour une communication sécurisée, vous devez :

- [Mettre à jour .NET Framework pour prendre en charge TLS 1.2](#update-net-framework-to-support-tls-12)
- [Mettre à jour SQL Server et les composants clients](#update-sql-server-and-client-components)
- [Mettre à jour Windows et WinHTTP sur Windows 8.0, Windows Server 2012 R2 et versions antérieures](#update-windows-and-winhttp)
- [Mettre à jour Windows Server Update Services (WSUS)](#update-windows-server-update-services)

#### <a name="update-net-framework-to-support-tls-12"></a>Mettre à jour .NET Framework pour prendre en charge TLS 1.2
Pour mettre à jour .NET Framework pour prendre en charge TLS 1.2, tout d’abord déterminez votre numéro de version de .NET. Pour plus d’aide, consultez [Comment déterminer les versions et les niveaux de Service Pack de Microsoft .NET Framework installés](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso).

Les versions antérieures de .NET Framework peuvent nécessiter des mises à jour ou des modifications du registre pour activer le chiffrement fort. Utilisez ces lignes directrices :

- NET Framework 4.6.2 prend en charge TLS 1.1 et TLS 1.2.  Aucune modification supplémentaire n’est requise.
- NET Framework 4.6 et versions antérieures [doit être mis à jour](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies) pour prendre en charge TLS 1.1 et TLS 1.2.

Si vous utilisez .NET Framework 4.5.1 ou 4.5.2 sur Windows 8.1, Windows RT 8.1 ou Windows Server 2012, les mises à jour appropriées et les informations détaillées sont également disponibles à partir du [Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=42883).
-  .NET framework doit être configuré pour prendre en charge le chiffrement fort. Définissez le paramètre du registre `SchUseStrongCrypto` sur `DWORD:00000001`. Cela désactive le chiffrement de flux RC4 et nécessite un redémarrage. Pour en savoir plus sur ce paramètre, consultez [Avis de sécurité Microsoft 296038](https://docs.microsoft.com/security-updates/SecurityAdvisories/2015/2960358).

Pour les applications 32 bits qui s’exécutent sur des systèmes 32 bits ou les applications 64 bits qui s’exécutent sur des systèmes 64 bits, mettez à jour la valeur de la sous-clé suivante :

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
Pour les applications 32 bits qui s’exécutent sur des systèmes 64 bits, mettez à jour la valeur de la sous-clé suivante :

```
[HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\.NETFramework\\v2.0.50727]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto" = (DWORD): 00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\
   WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions"=dword:00000001
      "SchUseStrongCrypto"=dword:00000001
```
#### <a name="update-sql-server-and-client-components"></a>Mettre à jour SQL Server et les composants clients

Microsoft SQL Server 2016 prend en charge TLS 1.1 et TLS 1.2.
Les versions antérieures et les bibliothèques dépendantes peuvent nécessiter des mises à jour. Pour plus d’informations, consultez [KB 3135244 : support TLS 1.2 pour Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server).

> [!NOTE]
> KB 3135244 décrit également les exigences pour les composants clients SQL Server. Mettez à jour chaque composant utilisé dans votre environnement.

#### <a name="update-windows-and-winhttp"></a>Mettre à jour Windows et WinHTTP

Windows 10, Windows 8.1, Windows Server 2016 et Windows Server 2012 R2 prennent en charge TLS 1.2 pour les communications client-serveur via WinHTTP prêt à l’emploi.

Windows 8.0, Windows Server 2012 et les versions antérieures de Windows n’activent pas TLS 1.1 ou 1.2 par défaut pour les communications client-serveur via HTTPS. Pour ces versions antérieures de Windows, vous devez installer [Mise à jour 3140245](https://support.microsoft.com/help/3140245) pour activer TLS 1.1 et TLS 1.2 en tant que protocoles sécurisés par défaut dans WinHTTP dans Windows et définir les valeurs de registre suivantes.

> [!IMPORTANT]
> Vous devez d’abord l’exécuter sur tous les clients de niveau inférieur **avant** l’activation de TLS 1.2 ou vous pouvez les rendre orphelins par inadvertance.

Vérifiez que le paramètre de registre `DefaultSecureProtocols` est `0xAA0`, comme suit :

```
HKEY_LOCAL_MACHINE\SOFTWARE\
   \Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\
   Wow6432Node\Microsoft\Windows\CurrentVersion\
      Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```
> [!NOTE]
> Cette modification nécessite un redémarrage.

#### <a name="update-windows-server-update-services"></a>Mettre à jour Windows Server Update Services

Pour prendre en charge TLS 1.2 pour les communications client-serveur dans WSUS sur Windows Server 2012 et Windows Server 2012 R2, vous devez appliquer la mise à jour suivante sur le serveur WSUS :
- Pour le serveur WSUS qui exécute Windows Server 2012, appliquez la [mise à jour 4022721](https://support.microsoft.com/help/4022721) ou une mise à jour ultérieure.
- Pour le serveur WSUS qui exécute Windows Server 2012 R2, appliquez la [mise à jour 4022720](https://support.microsoft.com/help/4022720) ou une mise à jour ultérieure.

## <a name="tasks-required-for-configuration-manager-features-and-scenarios"></a>Tâches requises pour les scénarios et fonctionnalités de Configuration Manager
Cette section décrit les dépendances pour les scénarios et fonctionnalités spécifiques de Configuration Manager. Pour déterminer les étapes suivantes, recherchez les éléments qui s’appliquent à votre environnement, puis vérifiez les dépendances à l’aide des étapes décrites précédemment dans [Activer TLS 1.2 pour les composants dépendants](#enable-tls-12-for-dependent-components).

|Fonctionnalité ou scénario|Tâches de mise à jour|
|--- |--- |
|Serveurs du site (central, principal ou secondaire)|[Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et vérifiez les paramètres de chiffrement fort.|
|Fournisseur SMS|[Mettez à jour SQL Server et ses composants clients](#update-sql-server-and-client-components) selon les besoins de chaque fournisseur SMS.|
|Rôles système de site|[Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et vérifiez les paramètres de chiffrement fort. [Mettez à jour SQL Server et ses composants clients](#update-sql-server-and-client-components).|
|Catalogue des applications de point de connexion du service|[Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et vérifiez les paramètres de chiffrement fort.|
|Point de rapport SRS|[Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) sur le serveur de site et les serveurs SRS. Redémarrez le service SMS_Executive en fonction des besoins.|
|Console Configuration Manager|[Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et vérifiez les paramètres de chiffrement fort.|
|Client SCCM avec les rôles de système de site HTTPS|[Mettez à jour Windows pour prendre en charge TLS 1.2 pour les communications client-serveur à l’aide de WinHTTP](#update-windows-and-winhttp).|
|Centre logiciel|[Mettez à jour .NET Framework](#update-net-framework-to-support-tls-12) et vérifiez les paramètres de chiffrement fort.|
|Point de mise à jour logicielle|[Mettez à jour WSUS](#update-windows-server-update-services).|
|Points de gestion|Mettez à jour vers le dernier client natif SQL Server pour permettre à Configuration Manager de communiquer avec les derniers composants de SQL Server prenant en charge TLS 1.2. Consultez le tableau « téléchargements des composants clients » dans [Support TLS 1.2 pour Microsoft SQL Server](https://support.microsoft.com/help/3135244).|

## <a name="known-issues"></a>Problèmes connus

Cette section fournit des conseils concernant les problèmes courants qui surviennent lorsque vous activez le support TLS 1.2.

### <a name="fips-security-policy-enabled"></a>Stratégie de sécurité FIPS activée

Si le paramètre de la stratégie de sécurité FIPS est activé pour le client ou un serveur, la négociation Secure Channel (Schannel) peut entraîner l’utilisation de TLS 1.0 même si le protocole est désactivé à l’aide du registre.

Pour procéder à des recherches, activez la journalisation des événements du canal sécurisé, puis révisez les événements Schannel dans le journal système. Pour obtenir des informations connexes, consultez [Comment restreindre l’utilisation de certains algorithmes et protocoles de chiffrement dans Schannel.dll](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc).

### <a name="sql-server-communication-failure"></a>Échec de communication de SQL Server

Si la communication de SQL Server échoue et retourne une erreur **SslSecurityError**, vérifiez les points suivants :
- .NET framework est mis à jour et a un chiffrement fort activé sur chaque ordinateur.
- SQL Server est mis à jour sur le serveur hôte.
- Les composants clients SQL sont mis à jour sur les serveurs de site, le fournisseur SMS, les serveurs de rôle de site et tous les autres systèmes qui communiquent avec SQL server.

### <a name="configuration-manager-client-communication-failures"></a>Échecs de communication avec le client Gestionnaire de configuration

Si le client Gestionnaire de configuration ne communique pas avec des points de terminaison des rôles de site, tels que des points de distribution, des points de gestion et des points de migration d’état, vérifiez que Windows a été mis à jour pour prendre en charge TLS 1.2 pour la communication client-serveur à l’aide de WinHTTP.

### <a name="srs-reporting-point-fails-and-returns-an-expected-error"></a>Point de rapport SRS échoue et retourne une erreur attendue

Si le Point de rapport SRS ne configure pas les rapports, consultez *SRSRP.log* pour vérifier l’erreur de saisie suivante :

`The underlying connection was closed:`
`An expected error occurred on a receive.`

Pour résoudre ce problème, procédez comme suit :

1. Vérifiez que .NET framework est mis à jour et a un chiffrement fort activé sur tous les ordinateurs concernés.
1. Vérifiez que le service SMS_Executive a été redémarré après l’installation de toutes les mises à jour.

### <a name="application-catalog-doesnt-initialize"></a>Le catalogue d’applications ne s’initialise pas

Si le catalogue d’applications ne s’initialise pas, consultez le fichier *ServicePortalWebSite.svclog* pour vérifier l’erreur de saisie suivante :

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

Pour résoudre ce problème, procédez comme suit :
1. Vérifiez que .NET framework est mis à jour et a un chiffrement fort activé sur tous les ordinateurs concernés.
1. Dans le dossier C:\Windows\System32\InetSrv du serveur du catalogue d’applications, créez un fichier *W2SP.exe.config* en exécutant le script suivant : 

   ```xml
   <?xml version="1.0" encoding="utf-8" ?>
   <configuration>
     <runtime>
     <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
     </runtime>
   </configuration>
   ```
   > [!NOTE]
   > Il s’agit du fichier par défaut qui serait créé si l’application était générée à l’aide de .NET Framework 4.6.3.
1. Utilisez la sécurité du transport HTTPS pour les rôles du catalogue d’applications.

   > [!NOTE]
   > Lorsque vous utilisez la sécurité des messages HTTP pour les rôles du catalogue d’applications, WCF est codé en dur pour utiliser SSL 3.0 et TLS 1.0 uniquement. Cela empêche l’utilisation de TLS 1.2.
1. Si des modifications ont été apportées, redémarrez l’ordinateur.


### <a name="software-center-or-browser-doesnt-communicate-with-application-catalog"></a>Le centre logiciel ou le navigateur ne communique pas avec le catalogue d’applications

Pour résoudre les échecs de communication entre le catalogue d’applications et le Centre logiciel ou le navigateur, vérifiez les conditions suivantes :

- .NET framework est mis à jour et a un chiffrement fort activé sur chaque ordinateur.
- Le navigateur est configuré pour prendre en charge TLS 1. Avant Windows 10, cette option a été désactivée par défaut.
- Tous les ordinateurs ont été redémarrés une fois les modifications apportées.

   > [!NOTE]
   > Pour que le Centre logiciel fonctionne avec le serveur appliqué à TLS 1.2 pour les applications accessibles à l’utilisateur, nous vous recommandons de supprimer des rôles du catalogue d’applications et de laisser le Centre logiciel communiquer avec le point de gestion. Pour plus d’informations, consultez [Supprimer le catalogue des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_remove-appcat).

### <a name="service-connection-point-upload-failures"></a>Défaillances de chargement du point de connexion de service

Si le Point de connexion de service ne télécharge pas des données vers SCCMConnectedService, vérifiez que .NET Framework est mis à jour et a un chiffrement fort activé sur chaque ordinateur. N’oubliez pas de redémarrer les ordinateurs une fois les modifications apportées.

### <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>La Console Configuration Manager affiche la boîte de dialogue Intégration Intune

Si la boîte de dialogue Intégration Intune s’affiche lorsque la console tente de se connecter au portail Intune, vérifiez que .NET Framework est mis à jour et a un chiffrement fort activé sur chaque ordinateur.  N’oubliez pas de redémarrer les ordinateurs une fois les modifications apportées.

### <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>La console Configuration Manager affiche un échec de connexion à Azure

Si la boîte de dialogue Intégration des Services Azure échoue immédiatement après avoir sélectionné **Connexion** lorsque vous essayez de créer des applications Azure AD, vérifiez que .NET Framework est mis à jour et que le chiffrement fort est activé. Un redémarrage est nécessaire pour que ces modifications entrent en vigueur.

## <a name="see-also"></a>Voir aussi

[Informations techniques de référence sur les contrôles de chiffrement](cryptographic-controls-technical-reference.md)
