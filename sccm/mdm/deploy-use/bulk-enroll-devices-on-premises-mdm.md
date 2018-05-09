---
title: Inscrire en bloc des appareils pour la gestion MDM locale
titleSuffix: Configuration Manager
description: Inscrivez en bloc des appareils de manière automatisée avec la gestion des appareils mobiles locale dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 437f6e6068fb56f1a906cbb8bea24cd3c707f0e3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Comment inscrire en bloc des appareils avec la gestion des appareils mobiles (MDM) locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


L’inscription en bloc dans la gestion des appareils mobiles locale dans System Center Configuration Manager est un mécanisme d’inscription d’appareils plus automatisé que l’inscription d’utilisateur, qui nécessite que les utilisateurs entrent leurs informations d’identification pour inscrire l’appareil.  L’inscription en bloc utilise un package d’inscription pour authentifier l’appareil lors de l’inscription. Le package (un fichier .ppkg) contient un profil de certificat et éventuellement un profil Wi-Fi si l’appareil a besoin d’une connectivité intranet pour prendre en charge l’inscription.  

> [!NOTE]  
>  Dans la gestion des appareils mobiles locale, la version Current Branch de Configuration Manager prend en charge l’inscription des appareils exécutant les systèmes d’exploitation suivants :  
>   
> -  Windows 10 Entreprise  
> -   Windows 10 Professionnel  
> -   Windows 10 Collaboration  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Entreprise
> -   Windows 10 IoT Entreprise   

Les tâches suivantes expliquent comment inscrire en bloc des ordinateurs et des appareils pour la gestion des appareils mobiles locale :  

-   [Créer un profil de certificat](#bkmk_createCert)  

-   [Créer un profil Wi-Fi](#CreateWifi)  

-   [Créer un profil d’inscription](#bkmk_createEnroll)  

-   [Créer un fichier de package d’inscription (ppkg)](#bkmk_createPpkg)  

-   [Utiliser le package pour l’inscription en bloc d’un appareil](#bkmk_getPpkg)  

-   [Vérifier l’inscription d’un appareil](#bkmk_verifyEnroll)  

##  <a name="bkmk_createCert"></a> Créer un profil de certificat  
 Le composant principal du package d’inscription est un profil de certificat, qui est utilisé pour configurer automatiquement un certificat racine approuvé sur l’appareil à inscrire.  Ce certificat racine est obligatoire pour la fiabilité des communications entre les appareils et les rôles de système de site nécessaires pour la gestion des appareils mobiles locale. Sans le certificat racine, l’appareil ne serait pas approuvé lors des connexions HTTPS entre lui-même et les serveurs hébergeant les rôles de système de site de point d’inscription, point proxy d’inscription, point de distribution et point de gestion des appareils.  

 Pendant la préparation du système pour la gestion des appareils mobiles locale, vous exportez un certificat racine que vous pouvez utiliser dans le profil de certificat du package d’inscription. Pour obtenir des instructions sur la façon d’obtenir le certificat racine approuvé, consultez [Exporter le certificat avec la même racine que le certificat de serveur web](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).  

 Utilisez le certificat racine exporté pour créer un profil de certificat. Pour obtenir des instructions, consultez [Comment créer des profils de certificat dans System Center Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).  

##  <a name="CreateWifi"></a> Créer un profil Wi-Fi  
 L’autre composant du package utilisé pour l’inscription en bloc est un profil Wi-Fi. Certains appareils peuvent ne pas disposer de la connectivité réseau nécessaire pour prendre en charge l’inscription jusqu’à ce que les paramètres réseau soient configurés. Le fait d’inclure un profil Wi-Fi dans le package d’inscription fournit un moyen d’établir une connectivité réseau pour l’appareil.  

 Pour créer un profil Wi-Fi dans Configuration Manager, suivez les instructions fournies dans [Comment créer des profils Wi-Fi dans System Center Configuration Manager](../../protect/deploy-use/create-wifi-profiles.md).  

> [!IMPORTANT]  
>Gardez à l’esprit les deux problèmes suivants quand vous créez un profil Wi-Fi pour l’inscription en bloc :
>
> - La branche CB (Current Branch) de Configuration Manager prend uniquement en charge les configurations de sécurité Wi-Fi suivantes pour la gestion des appareils mobiles locale :  
>   
>   - Types de sécurité : **WPA2-Entreprise** ou **WPA2-Personnel**  
>   - Types de chiffrement : **AES** ou **TKIP**  
>   - Types EAP : **Carte à puce ou autre certificat** ou **PEAP**  
>
>
> - Bien que Configuration Manager dispose d’un paramètre pour les informations du serveur proxy dans le profil Wi-Fi, il ne configure pas le serveur proxy quand l’appareil est inscrit. Si vous devez configurer un serveur proxy avec vos appareils inscrits, vous pouvez déployer les paramètres à l’aide des éléments de configuration une fois que les appareils sont inscrits ou créer le deuxième package à l’aide du Concepteur de configuration et d’acquisition d’images Windows pour un déploiement à côté du package d’inscription en bloc.

##  <a name="bkmk_createEnroll"></a> Créer un profil d’inscription  
 Le profil d’inscription vous permet de spécifier les paramètres nécessaires à l’inscription des appareils, notamment un profil de certificat qui configure de manière dynamique un certificat racine approuvé sur l’appareil et un profil Wi-Fi qui configure les paramètres réseau si nécessaire.  

 Avant de créer un profil d’inscription, veillez à créer un profil de certificat et un profil Wi-Fi (si nécessaire). Pour plus d'informations, consultez [Créer un profil de certificat](#bkmk_createCert) et [Créer un profil Wi-Fi](#CreateWifi)  

#### <a name="to-create-an-enrollment-profile"></a>Pour créer un profil d’inscription  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** >**Vue d’ensemble** >**Tous les appareils de l’entreprise** >**Windows** >**Profils d’inscription**.  

2.  Cliquez avec le bouton droit sur **Profil d’inscription** , puis cliquez sur **Créer un profil**.  

3.  Dans l’Assistant Création d’un profil d’inscription, entrez un nom pour le profil, vérifiez que **Local** est sélectionné pour **Autorité de gestion**, puis cliquez sur **Suivant**.  

4.  Sélectionnez le code de site, puis cliquez sur **Suivant**.  

5.  Sélectionnez **Intranet uniquement**, sélectionnez les points proxy d’inscription que l’appareil utilise pour lancer le processus d’inscription, puis cliquez sur **Suivant**.  

6.  Sélectionnez le profil de certificat contenant le certificat racine approuvé (il s’agit du profil que vous avez créé dans [Create a certificate profile](#bkmk_createCert)), puis cliquez sur **Suivant**.  

7.  Sélectionnez le profil Wi-Fi contenant les paramètres réseau nécessaires pour que les appareils se connectent à l’intranet (il s’agit du profil que vous avez créé dans [Create a Wi-Fi profile](#CreateWifi)), puis cliquez sur **Suivant**.  

    > [!NOTE]  
    >  Si vous n’utilisez pas de profil Wi-Fi pour votre package d’inscription, ignorez cette étape.  

8.  Vérifiez les paramètres du profil d’inscription, puis cliquez sur **Suivant**. Cliquez sur **Fermer** pour quitter l'Assistant.  

##  <a name="bkmk_createPpkg"></a> Créer un fichier de package d’inscription (ppkg)  
 Le package d’inscription est le fichier que vous utilisez pour inscrire en bloc des appareils pour la gestion des appareils mobiles locale.  Ce fichier doit être créé avec Configuration Manager. Vous pouvez créer des types de packages similaires à l’aide du Concepteur de configuration et d’acquisition d’images Windows, mais seuls les packages que vous créez dans Configuration Manager peuvent être utilisés pour inscrire des appareils pour la gestion des appareils mobiles locale du début à la fin. Les packages créés avec Windows ICD peuvent uniquement fournir le nom d’utilisateur principal (UPN) nécessaire à l’inscription. Ils ne peuvent pas exécuter le processus d’inscription proprement dit.  

 Le processus de création du package d’inscription exige l’utilisation du Kit de déploiement et d’évaluation Windows (Windows ADK) pour Windows 10.  Sur le serveur exécutant la console Configuration Manager, vérifiez que la version 1511 de Windows ADK est installée. Pour plus d’informations, consultez la section ADK dans [Télécharger le kit Windows ADK](https://msdn.microsoft.com/windows/hardware/dn913721.aspx)  

> [!TIP]  
>  Si vous supprimez un package d’inscription de la console Configuration Manager, il ne peut pas être utilisé pour inscrire des appareils. Vous pouvez utiliser la suppression de package comme moyen de gérer les packages que vous ne souhaitez plus utiliser pour l’inscription en bloc des appareils.  

#### <a name="to-create-an-enrollment-package-ppkg-file"></a>Pour créer un fichier de package d’inscription (ppkg)  

1.  Cliquez avec le bouton droit sur le profil que vous venez de créer (dans [Créer un profil d’inscription](#bkmk_createEnroll), cliquez sur **Exporter**).  

2.  Cliquez sur **Parcourir**, recherchez un emplacement où vous souhaitez enregistrer le fichier .ppkg, entrez un nom pour le package, puis cliquez sur **Enregistrer**.  

3.  Si vous souhaitez protéger le package avec un mot de passe, cochez la case à côté de **Chiffrer le package**, puis cliquez sur **Exporter** et patientez environ 10 secondes que l’exportation se termine.  

    > [!NOTE]  
    >  Si vous avez chiffré le package, Configuration Manager fournit un message contenant le mot de passe déchiffré. Veillez à enregistrer les informations de mot de passe, car vous en aurez besoin pour approvisionner le package sur les appareils.  

4.  Cliquez sur **OK**.  

##  <a name="bkmk_getPpkg"></a> Utiliser le package pour l’inscription en bloc d’un appareil  
 Vous pouvez utiliser le package pour inscrire des appareils avant ou après que l’appareil a été approvisionné par le biais du processus OOBE (Out-Of-Box experience).   Le package d’inscription peut également être inclus dans le cadre d’un package d’approvisionnement d’un fabricant d’ordinateurs OEM.  

 Le package doit être physiquement remis à l’appareil pour qu’il l’utilise pour l’inscription en bloc. Vous pouvez remettre le package d’inscription à l’appareil de différentes manières en fonction de vos besoins, notamment :  

-   Copier à partir du système de fichiers  

-   Joindre à un e-mail  

-   Copier via une connexion Communication en champ proche (NFC)  

-   Copier à partir d’une carte mémoire  

-   Scanner le code-barres  

-   Copier à partir d’un appareil attaché  

-   Inclure dans un package d’approvisionnement OEM  

#### <a name="to-bulk-enroll-a-device"></a>Pour inscrire en bloc un appareil  

1.  Sur l’appareil à inscrire, recherchez le package d’inscription (à l’aide de l’Explorateur de fichiers) et double-cliquez sur le fichier .ppkg.  

2.  Cliquez sur **Oui** en réponse au message de Contrôle de compte d’utilisateur.  

3.  Dans la boîte de dialogue vous demandant si le package provient d’une source fiable, cliquez sur **Oui, l’ajouter**.  

     Le processus d’inscription démarre et prend environ cinq minutes.  

4.  Ouvrez **Paramètres**.  

5.  Cliquez sur  **Comptes** > **Accès professionnel**. Une fois l’inscription terminée, un compte apparaît sous **CompanyApps**.  

6.  Cliquez sur le compte, puis sur **Synchroniser** pour démarrer la gestion avec Configuration Manager.  

##  <a name="bkmk_verifyEnroll"></a> Vérifier l’inscription d’un appareil  
 Vous pouvez vérifier que les appareils ont été inscrits correctement dans la console Configuration Manager.  

-   Démarrez la console Configuration Manager.  

-   Cliquez sur **Ressources et Conformité** > **Vue d’ensemble** > **Appareils**. L’appareil inscrit apparaît dans la liste.  
