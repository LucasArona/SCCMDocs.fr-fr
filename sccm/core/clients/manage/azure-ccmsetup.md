---
title: Workflow de l’authentification Azure AD
titleSuffix: Configuration Manager
description: Détails du processus d’installation client Configuration Manager sur un appareil Windows 10 avec l’authentification Azure Active Directory
ms.date: 05/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c422e5134ca798c1a5422cd518d550ed4c188e9a
ms.sourcegitcommit: bfb8a17f60dcb9905e739045a5141ae45613fa2c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66213800"
---
# <a name="azure-ad-authentication-workflow"></a>Workflow de l’authentification Azure AD

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article est une référence technique pour le processus d’installation client Gestionnaire de configuration sur un appareil Windows 10 joint à Azure Active Directory (Azure AD). Il décrit en détail le processus de flux de travail pour l’installation de l’authentification et du client de périphérique.  
 

## <a name="azure-ad-token-request-workflow"></a>Flux de travail des requêtes de jeton Azure AD

![Diagramme de flux de travail Azure AD CCMSetup](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Requête de jeton Azure AD

Un client joint au domaine de Windows 10 Azure AD utilise les paramètres Azure AD pour demander un jeton. Les entrées suivantes sont enregistrées dans **ccmsetup.log** :

- Requête de jeton d’appareil Azure AD :

    ```
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- S’il est impossible d’obtenir un jeton d’appareil, il demande un jeton d’utilisateur Azure AD :

    ```
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Un client doit obtenir un certificat de jonction d'espace de travail (WPJ) quand il rejoint Azure AD. Si un certificat d jonction d'espace de travail n’est pas trouvé, le client ne tente pas de créer la requête en utilisant le canal de communication du service d'émission de jeton de sécurité (CCM_STS). Ce comportement existe car le client ne peut pas ajouter un jeton Azure AD à la requête. En général, l’appareil n’a pas ce certificat lorsque le client n’est pas correctement joint à Azure AD.
>
> En outre, si le jeton n’est pas valide, la passerelle de gestion cloud (CMG) ne transmet pas la requête pour les rôles de site interne. Le jeton peut être non valide si l’abonné n’est pas enregistré comme un service de gestion cloud dans Configuration Manager.


### <a name="2-configuration-manager-client-token-request"></a>2. Requête de jeton client Gestionnaire de configuration

Une fois que le client dispose d’un jeton Azure AD, il demande un jeton client Gestionnaire de configuration (CCM).

Les entrées suivantes sont enregistrées dans **ccmsetup.log** de la machine virtuelle de la passerelle de gestion cloud :

```
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 La passerelle de gestion cloud obtient la requête

Les entrées suivantes sont enregistrées dans **IIS.log** :

```
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 La passerelle de gestion cloud transfère la requête au point de connexion de passerelle de gestion cloud

Les entrées suivantes sont enregistrées dans **CMGService.log** :

```
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 Le point de connexion de passerelle de gestion cloud transforme la requête du client de passerelle de gestion cloud en requête de client de point de gestion

Les entrées suivantes sont enregistrées dans **SMS_CLOUD_PROXYCONNECTOR.log** :

```
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 Le point de gestion vérifie le jeton d’utilisateur dans la base de données du site

Les entrées suivantes sont enregistrées dans **CCM_STS.log** :

```
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0aebad80-77d2-4f0a-9639-676ee4764bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Requête de localisation du contenu

Une fois que le client obtient une réponse avec le jeton CCM, il le met en cache et l’utilise pour demander des informations sur le site et la localisation du contenu via la passerelle de gestion cloud. Les entrées suivantes sont enregistrées dans **ccmsetup.log** :

```
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Installation du client

Le périphérique télécharge le contenu du client et démarre l’installation.

### <a name="communication-validation"></a>Validation de communication

- La passerelle de gestion cloud valide le jeton client via la passerelle de gestion cloud, le point de connexion de gestion cloud et HTTP(S) et la requête de base de données du point.
- Le client vérifie le certificat de service ou le certificat de gestion de la passerelle de gestion cloud
- Autorité de certification pour le certificat de service de passerelle de gestion cloud : Le client nécessite l’autorité de certification (AC) racine du certificat de passerelle de gestion cloud sur le magasin local
- Certificat de service de passerelle de gestion cloud tiers : Les clients valident automatiquement un certificat avec son AC racine publiée sur internet


## <a name="common-issues"></a>Problèmes courants

- Autorité de certification racine non présent
- Vérification de la liste de révocation de certificats activée : publiez la liste de révocation de certificats sur internet ou utilisez l’option **/NoCRLcheck** dans la ligne de commande
- Certificat de jonction d’espace de travail introuvable : le client est inscrit auprès d’Azure AD, mais pas joint à Azure AD

L’utilisation de /NoCRLCheck convient uniquement pour l’amorçage ccmsetup. Les clients peuvent être entièrement fonctionnels si vous publiez la liste de révocation de certificats sur internet. Pour résoudre ce problème, vous pouvez désactiver la vérification de la liste de révocation de certificats sur la configuration de la communication du site client. Sinon, une fois les paramètres de sécurité actualisés par le service de localisation, les clients cessent de communiquer avec le serveur.
