---
title: Profils VPN
titleSuffix: Configuration Manager
description: Découvrez l’utilisation des profils VPN sur les appareils mobiles dans Configuration Manager.
ms.date: 06/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c90525b20107cbc926e3775f10d75b7c7083cac
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424559"
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Utilisation de profils VPN sur des appareils mobiles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des profils VPN dans Configuration Manager afin de déployer des paramètres VPN pour les utilisateurs d’appareils mobiles dans votre organisation. Lorsque vous déployez ces paramètres, vous réduisez l'effort que doit fournir l'utilisateur final pour se connecter aux ressources du réseau d'entreprise.  

Par exemple, vous souhaitez configurer tous les appareils iOS pour qu’ils se connectent à un partage de fichiers du réseau d’entreprise. Créez un profil VPN disposant des paramètres de connexion nécessaires. Déployez ensuite ce profil pour tous les utilisateurs ayant des appareils iOS. Les utilisateurs voient la connexion VPN dans la liste des réseaux disponibles et peuvent se connecter à ce réseau très facilement.  

Lorsque vous créez un profil VPN, vous pouvez inclure un large éventail de paramètres de sécurité. Par exemple, vous pouvez spécifier des certificats de validation du serveur et d’authentification du client, configurés à l’aide de profils de certificat Configuration Manager. Pour plus d’informations, consultez [Profils de certificat](../../protect/deploy-use/introduction-to-certificate-profiles.md).  



## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profils VPN si Configuration Manager est utilisé en association avec Intune

Pour déployer des profils sur des appareils iOS, Android, Windows Phone et Windows 8.1, vous devez inscrire ces derniers dans Microsoft Intune. Les appareils sur d’autres plateformes peuvent également être inscrits auprès Intune. Pour plus d’informations sur l’inscription, consultez [Inscrire des appareils dans Microsoft Intune](/intune/device-enrollment). 

Ce tableau affiche le type de connexion pris en charge pour chaque plateforme d’appareil :  

 |Type de connexion|iOS et macOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop et Mobile|  
 |---------------|---------------|-------|-----------|----------|--------------|-----------------|-----------------------------|  
 |Cisco AnyConnect|Oui<sup>1</sup>|Oui|Non|Non|Non|Non|Non|
 |Cisco (IPSec)|iOS uniquement|Non|Non|Non|Non|Non|Non|  
 |Pulse Secure|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Client F5 Edge|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Dell SonicWALL Mobile Connect|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Check Point Mobile VPN|Oui|Oui|Oui|Non|Oui|Oui|Oui|  
 |Microsoft SSL (SSTP)|Non|Non|Oui|Oui|Oui|Non|Non|  
 |Microsoft Automatic|Non|Non|Oui|Oui|Oui|Non|Oui|  
 |IKEv2|Oui (Stratégie personnalisée, iOS 9 et ultérieur)|Non|Oui|Oui|Oui|Oui|Oui|  
 |PPTP|Oui|Non|Oui|Oui|Oui|Non|Oui|  
 |L2TP|Oui|Non|Oui|Oui|Oui|Non|Oui (OMA-URI)|  

<sup>1</sup> À partir de la version 1802, l’utilisation du type de connexion Cisco AnyConnect varie.<!--1357393-->  
   - Utilisez l’option **Cisco Legacy AnyConnect** pour les profils VPN dans les versions suivantes :
       - iOS avec Cisco AnyConnect 4.0.5 ou version antérieure
       - macOS avec toutes les versions de Cisco AnyConnect
   - Utilisez l’option **Cisco AnyConnect** pour les profils VPN dans les versions suivantes :
       - iOS avec Cisco AnyConnect 4.0.7 ou version ultérieure

     > [!Tip]  
     > Cisco AnyConnect 4.0.07x et versions ultérieures pour iOS ont été introduits dans la version 1802 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la [mise à jour 4163547](https://support.microsoft.com/help/4163547) de la version 1802, cette fonctionnalité n’est plus en préversion.  
  
  
> [!Note]  
> Les versions F5 Access 3.0 et ultérieures pour iOS ne sont pas prises en charge pour les profils VPN dans une gestion hybride des appareils mobiles. Ce produit est également appelé F5 Access 2018. Si vous avez besoin de créer des profils VPN pour ce client VPN, utilisez la version autonome d’Intune. Les prochaines versions d’iOS, y compris la version 12, ne prendront pas en charge F5 Access 2.1 ou versions antérieures. Pour plus d’informations, consultez le [blog de l’équipe de support Microsoft Intune](https://aka.ms/iOS12_and_VPN).


## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Fonctionnalités VPN Windows 10 disponibles quand vous utilisez Configuration Manager avec Intune  

Les options suivantes sont disponibles pour tous les types de connexion sur Windows 10 :

- **Contourner le VPN lorsque connecté au réseau Wi-Fi d’entreprise**: La connexion VPN n’est pas utilisée quand l’appareil est connecté au réseau Wi-Fi d’entreprise. Entrez le nom du réseau approuvé permettant de déterminer si l’appareil est connecté au réseau de l’entreprise.  

- **Règles de trafic réseau**: Définissez les protocoles, port local, port distant et plages d’adresses à activer pour la connexion VPN.  

     > [!Note]  
     > Si vous ne créez pas de règle de trafic réseau, tous les protocoles, tous les ports et toutes les plages d’adresses sont activés. Une fois que vous avez créé une règle, seuls les protocoles, les ports et les plages d’adresses que vous spécifiez dans cette règle ou dans des règles supplémentaires sont utilisés par la connexion VPN.  
  
- **Itinéraires**: Itinéraires qui utilisent la connexion VPN. La création de plus de 60 itinéraires peut entraîner l’échec de la stratégie.  

- **Serveurs DNS**: Serveurs DNS utilisés par la connexion VPN une fois la connexion établie.  

- **Les applications qui se connectent automatiquement au VPN**: Vous pouvez ajouter des applications ou importer des listes d’applications qui utilisent automatiquement la connexion VPN. Le type d’application détermine l’identificateur de l’application. Pour une application de bureau, fournissez le chemin de fichier de l’application. Pour une application universelle, indiquez le nom de la famille de packages (PFN). Pour savoir comment rechercher le nom PFN pour une application, consultez [Rechercher le nom de la famille de packages pour le VPN par application](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md).  

     > [!IMPORTANT]  
     > Sécurisez toutes les listes d’applications associées que vous compilez pour les utiliser dans la configuration du VPN par application. Si un utilisateur non autorisé change votre liste et si vous l’importez dans la liste d’applications du VPN par application, vous risquez de permettre à certaines applications non autorisées d’accéder au VPN. Une façon de sécuriser les listes d’applications consiste à utiliser une liste de contrôle d’accès (ACL).  



## <a name="create-vpn-profiles"></a>Création de profils VPN


1. Dans la console Configuration Manager, dans l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, **Accès aux ressources de l’entreprise**, puis sélectionnez **Profils VPN**. 

2. Cliquez dans le ruban sur **Créer un profil VPN**.  

3. Dans la page **Général**, spécifiez un **Nom**, puis sélectionnez le **Type de profil VPN**.   
     > [!NOTE]  
     > Le nom d’un profil VPN qui utilise des fonctionnalités VPN Windows 10 ne peut pas être au format Unicode ni contenir des caractères spéciaux.


4. Si la page **Plateformes prises en charge** est disponible, sélectionnez les versions d’OS correspondant au type de profil VPN spécifié. Choisissez **Sélectionner tout** pour installer le profil VPN sur toutes les versions d’OS disponibles.  

5. Configurez la connexion VPN dans la page **Connexion**. Pour plus d’informations sur ces options, consultez l’étape relative à la page Connexion dans [Créer un profil VPN](/sccm/protect/deploy-use/create-vpn-profiles#create-a-vpn-profile).  

6. Dans la page **Méthode d’authentification**, spécifiez les paramètres suivants :  

   - **Méthode d’authentification**: Sélectionnez la méthode d’authentification qui utilise la connexion VPN. Les méthodes disponibles peuvent varier selon le type de connexion, comme indiqué dans le tableau suivant.  

     |Méthode d'authentification|Types de&nbsp;connexion&nbsp;pris en charge|  
     |---------------------------|--------------------------------|  
     |**Certificats**<br /><br /> **Remarques** :<ul><li>Si le certificat client est utilisé pour l’authentification auprès d’un serveur RADIUS, par exemple un serveur NPS (Network Policy Server), affectez le nom d’utilisateur principal à l’autre nom de l’objet dans le certificat.</li><li>Pour les déploiements Android, sélectionnez l’identificateur EKU et la valeur de hachage de l’empreinte numérique de l’émetteur du certificat. Sinon, les utilisateurs doivent sélectionner manuellement le certificat approprié.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Cisco Legacy AnyConnect</li><li>Pulse Secure</li><li>Client F5 Edge</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
     |**Nom d'utilisateur et mot de passe**|<ul><li>Pulse Secure</li><li>Client F5 Edge</li><li>Dell SonicWALL Mobile Connect</li><li> Check Point Mobile VPN</li></ul>|  
     |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
     |**Microsoft PEAP (Protected EAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Mot de passe sécurisé Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Carte à puce ou autre certificat**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**RSA SecurID** (iOS uniquement)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatic</li><li>PPTP</li><li>L2TP</li></ul>|  
     |**Utiliser des certificats d’ordinateur**|<ul><li>IKEv2</li></ul>|  

      Selon les options sélectionnées, vous devrez peut-être spécifier d'autres informations, par exemple :  

     - **N’oubliez pas les informations d’identification de l’utilisateur à chaque ouverture de session**: Informations d’identification sont mémorisées pour que les utilisateurs n’ont pas à les entrer chaque fois qu’ils se connectent.  

     - **Sélectionner un certificat client pour l’authentification client**: Sélectionnez le client créé précédemment [certificat SCEP](create-pfx-certificate-profiles.md) qui est utilisé pour authentifier la connexion VPN.   

       > [!NOTE]  
       >  Pour les appareils iOS, le profil SCEP sélectionné est incorporé au profil VPN. Pour les autres plateformes, une règle d’applicabilité est ajoutée afin d’empêcher l’installation du profil VPN en cas d’absence ou de non-conformité du certificat.  
       >   
       >  Si le certificat SCEP que vous spécifiez n’est pas conforme ou n’a pas été déployé, le profil VPN n’est pas installé sur l’appareil.
       >  
       >  Les appareils qui exécutent iOS prennent uniquement en charge RSA SecurID et MSCHAP v2 comme méthode d’authentification quand le type de connexion est PPTP. Pour éviter toute erreur, déployez un profil VPN PPTP distinct sur les appareils qui exécutent iOS.   

     - **Accès conditionnel**  
         - Choisissez **Activer l’accès conditionnel pour cette connexion VPN** pour vérifier que les appareils qui se connectent au VPN ont été testés en vue de la conformité de l’accès conditionnel avant la connexion. Pour plus d’informations, consultez [Stratégies de conformité des appareils](/sccm/protect/deploy-use/device-compliance-policies).  

         - Choisissez **Activer l’authentification unique avec certificat de remplacement** pour choisir un certificat autre que le certificat d’authentification VPN pour la conformité des appareils. Si vous choisissez cette option, indiquez les valeurs de **Utilisation améliorée de la clé** (liste séparée par des virgules) et **Hachage de l’émetteur** pour le certificat approprié que le client VPN doit localiser.  

       - Pour **Protection des informations Windows**, indiquez l’identité d’entreprise gérée par l’entreprise, qui est généralement le domaine principal de votre organisation, par exemple, *contoso.com*. Vous pouvez spécifier plusieurs domaines appartenant à votre organisation en les séparant par le caractère « | ». Par exemple, *contoso.com|newcontoso.com*. Pour plus d’informations, consultez [Créer et déployer une stratégie de protection d’applications pour la protection des informations Windows avec Intune](/intune/windows-information-protection-policy-create).   

       ![Assistant Création d’un profil VPN, page Méthode d’authentification](media/vpn-conditional-access.png)

       Quand elle est prise en charge par la version client Windows, l’option **Configurer** est disponible pour la méthode d’authentification. Cette option vous permet d’ouvrir la boîte de dialogue des propriétés de Windows pour configurer la méthode d’authentification. Si l’option **Configurer** est désactivée, utilisez d’autres moyens pour configurer les propriétés de la méthode d’authentification.  

7. Sur la page **Paramètres du proxy** de l'**Assistant Création d'un profil VPN**, cochez la case **Configurer les paramètres du proxy pour ce profil VPN** si votre connexion VPN utilise un serveur proxy. Indiquez ensuite les informations sur le serveur proxy. Pour plus d’informations, consultez la documentation de Windows Server.  

   > [!NOTE]  
   >  Sur les ordinateurs Windows 8.1, le profil VPN n’affiche pas les informations de proxy tant que vous n’êtes pas connecté au VPN avec cet ordinateur.  


8. Configurez des paramètres DNS supplémentaires, si nécessaire.  

9. Fermez l'Assistant. Le nœud **Profils VPN** dans l'espace de travail **Ressources et Conformité** affiche le nouveau profil VPN.  



## <a name="next-steps"></a>Étapes suivantes  
Pour plus d’informations sur le déploiement de profils VPN, consultez [Déployer des profils Wi-Fi, VPN, de messagerie et de certificat](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

 Aidez-vous des articles suivants pour planifier, configurer, utiliser et gérer les profils VPN :  

-   [Prérequis pour les profils VPN](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sécurité et confidentialité pour les profils VPN](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)
