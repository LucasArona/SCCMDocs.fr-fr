---
title: Comment créer des profils Wi-Fi
titleSuffix: Configuration Manager
description: Découvrez comment utiliser des profils Wi-Fi dans System Center Configuration Manager pour déployer des paramètres de réseau sans fil pour les utilisateurs de votre organisation.
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0e6a5d3b83bbf98bab8f36616622d376caa2266
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500600"
---
# <a name="create-wi-fi-profiles"></a>Créer des profils Wi-Fi

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez des profils Wi-Fi dans System Center Configuration Manager pour déployer des paramètres de réseau sans fil pour les utilisateurs de votre organisation. En déployant ces paramètres, il est plus facile pour les utilisateurs de se connecter au Wi-Fi.  

 Par exemple, vous avez un réseau Wi-Fi auquel vous voulez que tous les appareils iOS puissent se connecter. Créez un profil Wi-Fi contenant les paramètres nécessaires à la connexion au réseau sans fil. Déployez ensuite le profil pour tous les utilisateurs détenteurs d’appareils iOS dans votre hiérarchie. Les utilisateurs des appareils iOS voient le réseau de l'entreprise dans la liste des réseaux sans fil et peuvent immédiatement se connecter à ce réseau.  

 Vous pouvez configurer les types d'appareil suivants avec des profils Wi-Fi :  

-   Appareils qui exécutent Windows 8.1 32 bits  

-   Appareils qui exécutent Windows 8.1 64 bits  

-   Appareils qui exécutent Windows RT 8.1  

-   Appareils qui exécutent Windows 10 Desktop ou Mobile  

La section relative à la [création de profils Wi-Fi pour les appareils mobiles](../../mdm/deploy-use/create-wifi-profiles.md) fournit des informations sur l’utilisation des profils Wi-Fi dans Configuration Manager, afin de déployer des paramètres de réseau sans fil pour les utilisateurs d’appareils mobiles.

> [!IMPORTANT]  
>  Pour déployer des profils sur des appareils Android, iOS, Windows Phone et sur des appareils Windows 8.1 ou version ultérieure inscrits, ces appareils doivent être inscrits dans Microsoft Intune. Pour plus d’informations sur la façon d’inscrire vos appareils, consultez [Inscrire des appareils pour la gestion dans Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Lorsque vous créez un profil Wi-Fi, vous pouvez inclure un large éventail de paramètres de sécurité. Ceux-ci incluent des certificats pour l’authentification de client et la validation de serveur qui ont été émis à l’aide des profils de certificat Configuration Manager. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="create-a-wi-fi-profile"></a>Créer un profil Wi-Fi  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Paramètres de compatibilité** >  **Accès aux ressources de l’entreprise**  > **Profils Wi-Fi**.  

2. Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un profil Wi-Fi**.  

3. Dans la page **Général**, entrez un nom unique et une description pour le profil Wi-Fi.  Si vous souhaitez utiliser les paramètres d’un autre profil Wi-Fi, sélectionnez **Importer un élément de profil Wi-Fi existant à partir d’un fichier**.  

   > [!IMPORTANT]  
   >  Assurez-vous que le profil Wi-Fi que vous importez contient du code XML valide pour un profil Wi-Fi. Configuration Manager ne valide pas le profil lorsque vous importez le fichier.  

4. Dans **Gravité de non-compatibilité pour les rapports** spécifiez le niveau de gravité signalé en cas de non-compatibilité du profil Wi-Fi sur des appareils clients (par exemple, en cas d’échec de l’installation du profil). Les niveaux de gravité disponibles sont les suivants :  

   -   **Aucun**: les ordinateurs qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  

   -   **Informations**: les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  

   -   **Avertissement**: les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  

   -   **Critique**: les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  

   -   **Critique avec événement**: les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme un événement Windows dans le journal des événements des applications.  

5. Dans la page **Profil Wi-Fi**, indiquez le nom qui sera affiché sur les appareils comme nom de réseau.  

   > [!IMPORTANT]  
   >  Configuration Manager ne prend pas en charge l’utilisation des caractères apostrophe (**â€˜**) ni virgule (**,**) dans le nom du réseau.  

6. Spécifiez le **SSID** qui respecte la casse.
7. Choisissez les autres options de connectivité appropriées, notamment les suivantes.   **Se connecter quand le réseau ne diffuse pas son nom (SSID)**, s’il est possible que le SSID soit masqué  

8. Dans la page **Configuration de la sécurité**, sélectionnez le protocole de sécurité utilisé par le réseau sans fil ou sélectionnez **Aucune authentification (Open)** si le réseau n’est pas sécurisé.
   > [!IMPORTANT]
   >  Si vous créez un profil Wi-Fi pour la gestion des appareils mobiles locale, la branche CB (Current Branch) de Configuration Manager prend uniquement en charge les configurations de sécurité Wi-Fi suivantes :  
   > 
   >  Types de sécurité : **WPA2-Entreprise** ou **WPA2-Personnel**  
   > Types de chiffrement : **AES** ou **TKIP**  
   > Types EAP : **Carte à puce ou autre certificat** ou **PEAP**  
   > 
   > Pour les appareils Android, les types de sécurité **WPA - Personnel**, **WPA2 - Personnel** et **WEP** ne sont pas pris en charge.  

9. sélectionnez la méthode de chiffrement utilisée par le réseau sans fil.  

10. sélectionnez le type EAP qui est utilisé pour l'authentification auprès du réseau sans fil.  

     Pour les appareils Windows Phone uniquement : les types EAP **LEAP** et **EAP-FAST** ne sont pas pris en charge.  

11. Cliquez sur **Configurer** pour spécifier les propriétés du type EAP sélectionné. Cette option peut ne pas être disponible pour certains types de protocoles EAP sélectionnés.  

    > [!IMPORTANT]  
    >  Lorsque vous cliquez sur **Configurer**, une boîte de dialogue Windows s'ouvre. Pour cette raison, vous devez vous assurer que le système d’exploitation de l’ordinateur qui exécute la console Configuration Manager prend en charge la configuration du type de protocole EAP sélectionné.  
    >   
    >  Pour les appareils iOS, si vous avez choisi une méthode autre qu'EAP pour l'authentification, quelle que soit la méthode choisie, MS-CHAP v2 est utilisé pour la connexion.  

12. Si vous souhaitez stocker les informations d’identification des utilisateurs pour qu’ils ne soient pas obligés de les entrer à chaque ouverture de session, sélectionnez **Conserver les informations d’identification de l’utilisateur à chaque ouverture de session**.  

13. **Pour les appareils iOS uniquement:**  
    configurez les informations pour tous les certificats qui sont requis pour la connexion Wi-Fi. Vous devez configurer le certificat client et le nom du certificat de serveur approuvé ou le certificat racine comme suit :  

    - **Noms de certificat de serveur approuvé**: si le serveur auquel se connecte l’appareil utilise un certificat d’authentification de serveur pour identifier le serveur et sécuriser le canal de communication, entrez le ou les noms sous le nom d’objet de ce certificat ou l’autre nom d’objet de ce certificat. Le ou les noms sont généralement le nom de domaine complet du serveur. Par exemple, si le certificat de serveur est identifié par le nom commun srv1.contoso.com dans l'objet du certificat, entrez **srv1.contoso.com**. Si le certificat de serveur est identifié par plusieurs noms spécifiés dans l'autre nom d'objet, entrez chaque nom, séparé par un point-virgule.  

      > [!TIP]  
      >  Si le certificat client sélectionné pour le protocole EAP ou pour l'authentification client d'un appareil iOS est utilisé à des fins d'authentification sur un serveur RADIUS, tel qu'un serveur exécutant NPS, l'autre nom de l'objet doit être défini sur le nom d'utilisateur principal.  

    - **Sélectionner des certificats racines pour la validation du serveur**: si le serveur auquel se connecte l’appareil utilise un certificat d’authentification de serveur non approuvé par l’appareil, sélectionnez le profil de certificat qui contient le certificat racine pour le certificat de serveur pour créer une chaîne de certificats de confiance sur l’appareil.  

    - **Sélectionner un certificat client pour l'authentification du client**: si le serveur ou l'appareil réseau requiert un certificat client pour authentifier l'appareil de connexion, sélectionnez le profil de certificat qui contient le certificat d'authentification du client.  

      > [!NOTE]  
      >  Pour pouvoir sélectionner le certificat racine et le certificat client, vous devez tout d'abord les configurer et les déployer comme un profil de certificat. Pour plus d’informations sur les profils de certificat, consultez [Profils de certificat dans System Center Configuration Manager](introduction-to-certificate-profiles.md).  

14. Dans la page **Paramètres avancés**, spécifiez des paramètres avancés pour le profil Wi-Fi, tels que le mode d’authentification, les options d’authentification unique et la conformité aux normes FIPS (Federal Information Processing Standards). Pour plus d’informations sur ces options, voir la documentation de Windows. Les paramètres avancés peuvent varier ou ne pas être disponibles selon les options sélectionnées sur la page **Configuration de la sécurité** de l'Assistant.  

15. Dans la page **Paramètres proxy**, cochez la case **Configurer les paramètres du proxy pour ce profil Wi-Fi** si votre connexion sans fil utilise un serveur proxy, puis fournissez les informations de configuration.  

16. Dans la page **Plateformes prises en charge**, sélectionnez les systèmes d’exploitation dans lesquels vous voulez installer le profil Wi-Fi. Sinon, cliquez sur **Sélectionner tout** pour installer le profil Wi-Fi sur tous les systèmes d'exploitation disponibles.  

### <a name="next-steps"></a>Étapes suivantes
 Pour plus d’informations sur le déploiement du profil Wi-Fi, consultez [Comment déployer des profils Wi-Fi dans System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  
