---
title: Paramètres Windows Hello Entreprise
titleSuffix: Configuration Manager
description: Découvrez comment intégrer Windows Hello Entreprise avec Configuration Manager.
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 81086b01cef3d60af6e0c93d25b2ad937252d4ba
ms.sourcegitcommit: 94bf7d5b5beb9628cc1fdfe75451d33b5de26f8a
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152398"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Paramètres Windows Hello Entreprise dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1245704--> Configuration Manager permet d’intégrer Windows Hello Entreprise (anciennement Microsoft Passport pour Windows), qui constitue une méthode alternative de connexion pour les appareils Windows 10. Hello Entreprise utilise Active Directory ou un compte Azure Active Directory pour remplacer un mot de passe, une carte à puce ou une carte à puce virtuelle. Hello Entreprise vous permet d’utiliser un **geste utilisateur** plutôt qu’un mot de passe pour vous connecter. Un geste utilisateur peut être un simple code confidentiel, une authentification biométrique ou un appareil externe tel qu’un lecteur d’empreintes digitales.


> [!Important]  
> À compter de décembre 2017, Windows Hello pour les paramètres d’entreprise dans Configuration Manager est un [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Déploiement de Windows Server 2016 autorité Active Directory Federation Services d’inscription (RA ADFS) est plus simple, fournit une meilleure expérience utilisateur et offre une expérience d’inscription de certificat plus déterministe.  


Pour plus d’informations, consultez [Windows Hello Entreprise](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification).


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Configuration Manager s’intègre avec Windows Hello Entreprise de deux manières :  

- Vous pouvez utiliser Configuration Manager pour contrôler les gestes que les utilisateurs peuvent et ne peuvent pas utiliser pour se connecter.  

- Vous pouvez stocker des certificats d’authentification dans le fournisseur de stockage de clés Windows Hello Entreprise. Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  

- Vous pouvez déployer des stratégies Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine qui exécutent le client Configuration Manager. Cette configuration est décrite dans la section [Configurer Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Lorsque vous utilisez Configuration Manager avec Microsoft Intune (hybride), vous pouvez configurer ces paramètres sur les appareils Windows 10 et Windows 10 Mobile. Pour plus d’informations, consultez [Configurer les paramètres Windows Hello Entreprise (hybride)](/sccm/mdm/deploy-use/windows-hello-for-business-settings).



## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurer Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine

Vous pouvez contrôler les paramètres Windows Hello Entreprise sur les appareils Windows 10 joints à un domaine en créant et en déployant un profil Windows Hello Entreprise. Il s’agit de l’approche recommandée.


Si vous utilisez l’authentification par certificat, vous devez également déployer un profil de certificat, comme le décrit la section [Configurer un profil de certificat](#configure-a-certificate-profile). Si vous utilisez l’authentification par clé, il est inutile de déployer un profil de certificat.



## <a name="configure-a-windows-hello-for-business-profile"></a>Configurer un profil Windows Hello Entreprise  

Dans la console de Configuration Manager, sous **Accès aux ressources de l’entreprise**, cliquez avec le bouton droit sur **Profils Windows Hello for business** et choisissez **Nouveau** pour démarrer l’Assistant de création de profil. Fournissez les paramètres demandés par l’Assistant, passez en revue et confirmez les paramètres de la dernière page, puis cliquez sur **Fermer**. Voici un exemple de ce à quoi vos paramètres peuvent ressembler :  

![Assistant Stratégie de Windows Hello Entreprise, montrant la liste des paramètres disponibles](../media/Hello-for-Business-settings.png)



## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurer un profil de certificat pour inscrire le certificat d’inscription Windows Hello Entreprise dans Configuration Manager  

Si vous souhaitez utiliser l’ouverture de session par certificat Windows Hello Entreprise, configurez les éléments suivants :  

-   Un profil de certificat Configuration Manager.  

-   Dans le profil de certificat, sélectionnez un modèle qui recourt à l’utilisation de clé étendue pour l’ouverture de session avec carte à puce.  

-   Si vous envisagez de stocker des profils de certificat dans le conteneur de clés Windows Hello Entreprise et que le profil de certificat utilise l’utilisation améliorée de la clé pour **l’ouverture de session avec carte à puce**, vous devez configurer les autorisations suivantes pour enregistrer cette clé et garantir que le certificat est validé correctement.
Vous devez avoir au préalable créé le groupe **Administrateurs de clé** et ajouté tous les ordinateurs de point de gestion Configuration Manager comme membres de ce groupe.

Il est possible que certaines configurations ne requièrent pas de configuration des autorisations ou qu’elles nécessitent des configurations supplémentaires. Consultez le tableau suivant pour obtenir une aide supplémentaire :

|Version du client Windows|Configuration Manager 1602 ou 1606|Configuration Manager 1610|Configuration Manager 1702 ou version ultérieure|
|-|-|-|-|
|Mise à jour anniversaire Windows 10|Pas de correctif logiciel requis<br><br>Pas d’autorisation requise<br><br>Pas de mise à jour de schéma Windows requise|Pas de correctif logiciel requis (voir **Avertissement**)<br><br>Pas d’autorisation requise<br><br>Pas de mise à jour de schéma Windows requise|Configurer les autorisations<br><br>Appliquer le schéma de Windows Server 2016 à Active Directory|
|Windows 10 Creators Update ou version ultérieure|Non pris en charge|Installer [ce correctif logiciel](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v)<br><br>Configurer les autorisations<br><br>Appliquer le schéma de Windows Server 2016 à Active Directory|Configurer les autorisations<br><br>Appliquer le schéma de Windows Server 2016 à Active Directory|

> [!WARNING]
> Si le [correctif logiciel](https://support.microsoft.com/help/4010155/update-rollup-for-system-center-configuration-manager-current-branch-v) n’est pas obligatoire pour Configuration Manager 1610 et la Mise à jour anniversaire Windows 10, il peut néanmoins être installé.  Dans ce cas, vous devez configurer les autorisations et appliquer le schéma Windows Server 2016 à Active Directory.

## <a name="to-configure-permissions"></a>Configurer les autorisations

1.  Connectez-vous à un contrôleur de domaine ou à des stations de travail de gestion en tant qu’administrateur de domaine, ou avec des informations d’identification équivalentes.
2.  Ouvrez **Utilisateurs et ordinateurs Active Directory**.
3.  Dans le volet de navigation, cliquez avec le bouton droit sur votre nom de domaine, puis cliquez sur **Propriétés**.
4.  Sous l’onglet **Sécurité** de la boîte de dialogue **Propriétés** *<domain name>*, cliquez sur **Avancé**. Si l’onglet **Sécurité** n’apparaît pas, activez les **Fonctionnalités avancées** du menu **Affichage** dans **Utilisateurs et ordinateurs Active Directory**.
5.  Cliquez sur **Ajouter**.
6.  Dans la boîte de dialogue **Saisie des autorisations pour** *<domain name>*, cliquez sur **Sélectionner un principal**.
7.  Dans la boîte de dialogue **Sélectionner un utilisateur, un ordinateur, un compte de service ou un groupe**, tapez **Administrateurs de clé** dans la zone de texte **Entrer le nom de l’objet à sélectionner**. Cliquez sur **OK**.
8.  Dans la liste **S’applique à**, sélectionnez **Objets utilisateur descendants**.
9.  Faites défiler jusqu’au bas de la page et cliquez sur **Effacer tout**.
10. Dans la section **Propriétés**, sélectionnez **Lire msDS-KeyCredentialLink**.
11. Cliquez sur **OK** trois fois pour terminer la tâche.


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations, consultez [Profils de certificat](introduction-to-certificate-profiles.md).  




