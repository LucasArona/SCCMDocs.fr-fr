---
title: Présentation des profils de certificat
titleSuffix: Configuration Manager
description: Découvrez le fonctionnement des profils de certificat dans System Center Configuration Manager avec les services de certificats Active Directory.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5872a6a8ee69e50d0abfe5840a087aaf83ab7aa5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156608"
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Présentation des profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les profils de certificat fonctionnent avec les services de certificats Active Directory et le rôle Service d’inscription de périphérique réseau. Créez et déployez des certificats d’authentification pour les appareils gérés afin que les utilisateurs puissent accéder facilement aux ressources de l’entreprise. Par exemple, vous pouvez créer et déployer des profils de certificat pour fournir les certificats nécessaires aux utilisateurs afin d’établir des connexions VPN et sans fil.

Les profils de certificat peuvent automatiquement configurer des appareils utilisateur. Les utilisateurs accèdent aux ressources de l’entreprise, telles que les réseaux Wi-Fi et les serveurs VPN, sans avoir à installer manuellement des certificats ou à utiliser un processus hors-bande. Les profils de certificat permettent de sécuriser les ressources d’entreprise à l’aide de paramètres plus sécurisés et pris en charge par l’infrastructure à clé publique (PKI) de votre entreprise. Par exemple, vous pouvez exiger une authentification serveur pour toutes les connexions VPN et Wi-Fi, car vous avez déployé les certificats nécessaires sur les appareils gérés.   

Les profils de certificat fournissent les fonctionnalités de gestion suivantes :  

-   Inscription et renouvellement de certificats auprès d’une autorité de certification d’entreprise pour les appareils exécutant iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop et Mobile, et Android. Ces certificats peuvent ensuite être utilisés pour les connexions VPN et Wi-Fi.  

-   Déploiement de certificats d’autorité de certification intermédiaires ou racines de confiance Ces certificats configurent une chaîne d’approbation sur les appareils pour les connexions VPN et Wi-Fi, lorsque l’authentification du serveur est nécessaire.  

-   Analyse et rapport sur les certificats installés.  

**Exemple :** Tous les employés doivent pouvoir se connecter à des points d'accès Wi-Fi répartis à différents endroits dans l'entreprise. Pour faciliter les connexions utilisateurs, vous devez d’abord déployer les certificats nécessaires aux connexions Wi-Fi. Ensuite, vous devez déployer les profils Wi-Fi qui référencent le certificat.  

**Exemple :** Vous avez mis en place une infrastructure à clé publique (PKI). Vous souhaitez passer à une méthode plus souple et plus sécurisée pour le déploiement de vos certificats. Les utilisateurs doivent pouvoir accéder aux ressources de l’entreprise à partir de leurs appareils personnels, sans compromettre la sécurité. Configurez des profils de certificat avec les paramètres et protocoles pris en charge par la plateforme d’appareil spécifique. Les appareils peuvent ensuite demander automatiquement ces certificats depuis un serveur d'inscription via Internet. Ensuite, configurez des profils VPN pour utiliser ces certificats afin que l’appareil puisse accéder aux ressources d’entreprise.  



## <a name="types-of-certificate-profiles"></a>Types de profil de certificat  
 Il existe trois types de profil de certificat :  

-   **Certificat AC de confiance** : Déployez une autorité de certification racine de confiance ou un certificat d’autorité de certification intermédiaire. Ces certificats forment une chaîne d’approbation lorsque l’appareil doit authentifier un serveur.  

-   **Protocole d’inscription de certificats simple (SCEP)** : Demandez un certificat pour un utilisateur ou un appareil à l’aide du protocole SCEP. Ce type nécessite le rôle Service d’inscription de périphérique réseau sur un serveur exécutant Windows Server 2012 R2 ou ultérieur.

    Pour créer un profil de certificat du type **Protocole d’inscription de certificats simple (SCEP)**, vous devez d’abord créer un profil du type **Certificat d’autorité de certification de confiance**.

-   **Échange d’informations personnelles (.pfx)** : Demandez un certificat .pfx (également appelé PKCS #12) pour un appareil ou un utilisateur.<!--1321368-->  

    Vous pouvez créer des profils de certificat PFX en [important des informations d’identification](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) à partir de certificats existants ou en [définissant une autorité de certification](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) pour traiter les demandes.

    > [!Note]  
    > Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    À compter de la version 1706, vous pouvez utiliser Microsoft ou Entrust comme autorités de certification pour les certificats **Échange d’informations personnelles (.pfx)**.


## <a name="requirements-and-supported-platforms"></a>Configuration requise et plateformes prises en charge  
Pour déployer des profils de certificat qui utilisent le protocole SCEP, installez le point d’enregistrement de certificat sur un serveur de système de site. Vous devez également installer un module de stratégie pour le Service d’inscription de périphérique réseau (le module de stratégie de Configuration Manager) sur un serveur qui exécute Windows Server 2012 R2 ou ultérieur. Ce serveur nécessite le rôle Services de certificats Active Directory, ainsi qu’un Service d’inscription de périphérique réseau actif et accessible aux appareils qui nécessitent les certificats. Pour les appareils qui sont inscrits par Microsoft Intune, le Service d’inscription de périphérique réseau doit être accessible à partir d’Internet. C’est le cas, par exemple, dans un sous-réseau filtré (également appelé « réseau de périmètre »).  

Les certificats PFX nécessitent également un point d’enregistrement de certificat. Vous devez également spécifier l’autorité de certification du certificat, ainsi que les informations d’identification d’accès correspondantes. À compter de la version 1706, vous pouvez spécifier Microsoft ou Entrust comme autorités de certification.  

Pour plus d’informations sur la façon dont le service NDES prend en charge un module de stratégie pour que Configuration Manager puisse déployer des certificats, consultez [Utilisation d’un module de stratégie avec le service d’inscription de périphérique réseau](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

Configuration Manager prend en charge le déploiement de certificats sur différents magasins de certificats situés sur divers types d’appareils et systèmes d’exploitation, en fonction des exigences. Les appareils et les systèmes d'exploitation suivants sont pris en charge :  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop et Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être [inscrits dans Microsoft Intune](/intune/device-enrollment).   

Un scénario type pour Configuration Manager consiste à installer des certificats d’autorité de certification racines de confiance pour authentifier des serveurs Wi-Fi et VPN, lorsque la connexion utilise les protocoles d’authentification EAP-TLS, EAP-TTLS et PEAP, ainsi que les protocoles de tunneling IKEv2, L2TP/IPsec et Cisco IPsec VPN.  

Un certificat d’autorité de certification racine d’entreprise doit être installé sur l’appareil avant que celui-ci puisse exiger des certificats à l’aide d’un profil de certificat SCEP.  

Vous pouvez spécifier des paramètres dans un profil de certificat SCEP afin d’exiger des certificats personnalisés pour différents environnements ou besoins de connectivité. **L’Assistant Créer un profil de certificat** comporte deux pages pour les paramètres d’inscription. La première, **Inscription SCEP**, contient les paramètres de la demande d’inscription et l’emplacement auquel installer le certificat. La seconde, **Propriétés du certificat**, décrit le certificat demandé.  

## <a name="deploying-certificate-profiles"></a>Déploiement de profils de certificat  
 Lorsque vous déployez un profil de certificat, les fichiers de certificat dans le profil sont installés sur des appareils clients. Tous les paramètres SCEP sont également déployés et les demandes SCEP sont traitées sur l’appareil client. Vous pouvez déployer des profils de certificat sur des regroupements d’utilisateurs ou d’appareils, et spécifier le magasin de destination pour chaque certificat. Les règles de mise en application déterminent si les certificats peuvent être installés sur l’appareil. Quand vous déployez des profils de certificat sur des regroupements d’utilisateurs, l’affinité entre appareil et utilisateur détermine les appareils qui doivent installer les certificats. Quand des profils de certificat contenant des certificats d’utilisateur sont déployés sur des regroupements d’appareils, par défaut, les certificats sont installés sur chacun des appareils principaux de l’utilisateur. Vous pouvez modifier ce comportement pour installer le certificat sur l’un des appareils de l’utilisateur dans la page **Inscription SCEP** de l’**Assistant Création d’un profil de certificat**. Si les appareils sont des ordinateurs de groupe de travail, les certificats utilisateur ne sont pas déployés.  

## <a name="monitoring-certificate-profiles"></a>Surveillance des profils de certificat  

Vous pouvez surveiller les déploiements de profil de certificat en affichant les résultats ou les rapports de conformité. Ces approches sont décrites dans [Guide pratique pour surveiller des profils de certificat](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Révocation automatique de certificats  
 System Center Configuration Manager révoque automatiquement les certificats utilisateur et ordinateur qui ont été déployés à l’aide de profils de certificat dans les circonstances suivantes :  

- L’appareil est mis hors service depuis la gestion de System Center Configuration Manager.  

- Une réinitialisation sélective est appliquée à l'appareil.  

- L’appareil est bloqué depuis la hiérarchie System Center Configuration Manager.  

  Pour révoquer les certificats, le serveur de site envoie une commande de révocation à l'autorité de certification émettrice. Le motif de révocation est la **cessation de fonctionnement**.  
