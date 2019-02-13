---
title: 'Configurer des certificats '
titleSuffix: Configuration Manager
description: Configurez des certificats pour les communications approuvées pour la gestion des appareils mobiles locale dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2a7d7170-1933-40e9-96d6-74a6eb7278e2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8443430b55ee61e9ad5eeac1e70342dfa6e85851
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122370"
---
# <a name="set-up-certificates-for-trusted-communications-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Configurer des certificats pour les communications approuvées pour la gestion des appareils mobiles locale dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion des appareils mobiles locale System Center Configuration Manager exige de configurer des rôles de système de site de point d’inscription, de point proxy d’inscription, de point de distribution et de point de gestion d’appareil pour assurer des communications fiables avec les appareils gérés. Tout serveur de système de site hébergeant un ou plusieurs de ces rôles doit avoir un certificat PKI unique lié au serveur web sur ce système. Un certificat avec la même racine que le certificat sur les serveurs doit également être stocké sur les appareils gérés afin d’établir une communication fiable avec ceux-ci.  

 Pour les appareils joints au domaine, les Services de certificats Active Directory installent le certificat nécessaire avec la racine approuvée automatiquement sur tous les appareils. Pour les appareils non joints au domaine, vous devez obtenir un certificat valide avec une racine approuvée par d’autres moyens. Si vous utilisez l’autorité de certification du site comme racine approuvée (qui est la même que celle qu’Active Directory utilise pour les appareils joints au domaine), les serveurs de système de site pour le point d’inscription et le point proxy d’inscription doivent avoir un certificat lié à eux émis par cette autorité de certification.  

 Chaque appareil à gérer doit également disposer d’un certificat avec la même racine installée pour prendre en charge les communications approuvées avec les rôles système de site. Pour les appareils inscrits en bloc, vous pouvez inclure le certificat dans le package d’inscription ajouté à l’appareil pour l’inscription de celui-ci quand un utilisateur le démarre pour la première fois. Pour les appareils inscrits par l’utilisateur, vous devez ajouter le certificat par e-mail, par téléchargement sur le web ou par une autre méthode.  

 En tant que solution de remplacement pour des appareils non joints au domaine, vous pouvez utiliser la racine d’une autorité de certification publique connue (comme Verisign ou GoDaddy) pour émettre le certificat de serveur, ce qui évite de devoir installer manuellement un certificat sur l’appareil, car la plupart des appareils approuvent en mode natif les connexions à des serveurs utilisant la même racine d’autorité de certification publique. Il s’agit d’une alternative utile pour les appareils inscrits par l’utilisateur, quand il n’est pas possible d’installer les certificats approuvés via l’autorité de certification du site sur chaque appareil.  

> [!IMPORTANT]  
>  Il existe différentes façons de configurer les certificats pour assurer des communications fiables entre les appareils et les serveurs de système de site à des fins de gestion des appareils mobiles locale. Les informations fournies dans cet article sont destinées à illustrer une manière de procéder. Cette méthode requiert que vous exécutiez un serveur au sein de votre site avec le rôle Services de certificats Active Directory et les services du rôle Autorité de Certification et Inscription de l’autorité de certification via le Web installés. Pour obtenir plus d’informations et des conseils sur ce rôle Windows Server, consultez [Services de certificats Active Directory](http://go.microsoft.com/fwlink/p/?LinkId=115018).  

 Pour configurer le site Configuration Manager pour les communications SSL nécessaires à la gestion des appareils mobiles locale, exécutez ces étapes générales :  

-   [Configurer l’autorité de certification (AC) pour la publication de listes de révocation de certificats](#bkmk_configCa)  

-   [Créer le modèle de certificat de serveur web sur l’autorité de certification](#bkmk_certTempl)  

-   [Demander le certificat de serveur web pour chaque rôle de système de site](#bkmk_requestCert)  

-   [Lier le certificat au serveur web](#bkmk_bindCert)  

-   [Exporter le certificat ayant la même racine que le certificat de serveur web](#bkmk_exportCert)  

##  <a name="bkmk_configCa"></a> Configurer l’autorité de certification (AC) pour la publication de listes de révocation de certificats  
 Par défaut, l’autorité de certification (AC) utilise des listes de révocation de certificats (CRL) LDAP qui autorisent les connexions pour des appareils joints au domaine. Vous devez ajouter des listes de révocation de certificats basées sur HTTP à l’autorité de certification pour permettre que des appareils non joints au domaine soient approuvés avec des certificats émis par l’autorité de certification. Ces certificats sont nécessaires aux communications SSL entre les serveurs hébergeant les rôles de système de site Configuration Manager et les appareils inscrits pour la gestion des appareils mobiles locale.  

 Procédez de la manière décrite ci-dessous pour configurer l’autorité de certification afin qu’elle publie automatiquement les informations de liste de révocation de certificats pour l’émission de certificats qui autorisent des connexions approuvées pour des appareils joints et non joints au domaine :  

1.  Sur le serveur exécutant l’autorité de certification pour votre site, cliquez sur **Démarrer** > **Outils d’administration** > **Autorité de certification**.  

2.  Dans la console Autorité de certification, cliquez avec le bouton droit sur **CertificateAuthority**, puis cliquez sur **Propriétés**.  

3.  Dans les propriétés CertificateAuthority, cliquez sur l’onglet **Extensions**, puis vérifiez que l’option **Sélectionner l’extension** a la valeur **Points de distribution de liste de révocation de certificats (CDP)**  

4.  Sélectionnez **http://<NomDNSServeur\>/CertEnroll/<NomAutoritéCert\><SuffixeNomListeCRL\><ListeCRLDeltaAutorisée\>.crl**. Sélectionnez également les trois options ci-dessous :  

    -   **Inclure dans les listes de révocation des certificats afin de pouvoir rechercher les listes de révocation des certificats delta.**  

    -   **Inclure dans l’extension CDP des certificats émis.**  

    -   **Inclure dans l’extension IDP des listes de révocation de certificats émises.**  

5.  Cliquez sur l’onglet **Module de sortie**, sur **Propriétés...**, puis sélectionnez **Autoriser la publication des certificats dans le système de fichier**.  

6.  Cliquez sur **OK** lors de la notification que les Services de certificats Active Directory doivent être redémarrés.  

7.  Cliquez avec le bouton droit sur **Certificats révoqués**, cliquez sur **Toutes les tâches**, puis sur **Publier**.  

8.  Dans la boîte de dialogue Publier la liste de révocation de certificats, sélectionnez **Liste de révocation de certificats delta uniquement**, puis cliquez sur **OK**.  

##  <a name="bkmk_certTempl"></a> Créer le modèle de certificat de serveur web sur l’autorité de certification  
 Après publication de la nouvelle liste de révocation de certificats sur l’autorité de certification, l’étape suivante consiste à créer un modèle de certificat de serveur web. Ce modèle est requis pour émettre des certificats pour les serveurs hébergeant les rôles système de site point d’inscription, point proxy d’inscription, point de distribution et point de gestion d’appareil. Ces serveurs sont des points de terminaison SSL pour les communications approuvées entre les rôles système de site et les appareils inscrits.    Procédez de la manière décrite ci-dessous pour créer le modèle de certificat :  

1.  Créez un groupe de sécurité nommé **Serveurs ConfigMgr MDM**, contenant les serveurs exécutant les systèmes de site qui nécessitent des communications approuvées avec les appareils inscrits.  

2.  Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis cliquez sur **Gérer** pour charger la console Modèles de certificat.  

3.  Dans le volet de résultats, cliquez avec le bouton droit sur l'entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis cliquez sur **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle** , assurez-vous que l'option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**. Configuration Manager ne prend pas en charge les modèles de certificat de Windows Server 2008 pour assurer des communications fiables utilisant le protocole HTTPS.  

    > [!NOTE]  
    >  Si l’autorité de certification que vous utilisez est sur Windows Server 2012, vous n’êtes pas invité à spécifier la version du modèle de certificat quand vous cliquez sur **Dupliquer le modèle**. Spécifiez-la plutôt sous l'onglet **Compatibilité** des propriétés du modèle, comme suit :  
    >   
    >  **Autorité de certification** : **Windows Server 2003**  
    >   
    >  **Destinataire du certificat** : **Windows XP/Server 2003**  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle pour générer les certificats web à utiliser sur les systèmes de site Configuration Manager, par exemple **Serveur web ConfigMgr MDM**.  

6.  Cliquez sur l’onglet **Nom du sujet**, sélectionnez **Construire à partir de ces informations Active Directory** et, pour le format du nom du sujet, spécifiez **Nom DNS**. Décochez la case de l’autre nom du sujet si l’option **Nom d’utilisateur principal (UPN)** est activée.  

7.  Sous l'onglet **Sécurité** , supprimez l'autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l'entreprise**.  

8.  Cliquez sur **Ajouter**, entrez **Serveurs ConfigMgr MDM** dans la zone de texte, puis cliquez sur **OK**.  

9. Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

10. Cliquez sur **OK**, puis fermez la console Modèles de certificat.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, cliquez sur **Nouveau**, puis cliquez sur **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat**, sélectionnez le modèle que vous venez de créer, **Serveur web ConfigMgr MDM**, puis cliquez sur **OK**.  

##  <a name="bkmk_requestCert"></a> Demander le certificat de serveur web pour chaque rôle de système de site  
 Les appareils inscrits pour la gestion des appareils mobiles locale doivent approuver les points de terminaison SSL hébergeant le point d’inscription, le point proxy d’inscription, le point de distribution et le point de gestion d’appareil.  Les étapes ci-dessous décrivent comment demander le certificat de serveur web pour IIS. Vous devez faire cela pour chaque serveur (point de terminaison SSL) hébergeant l’un des rôles de système de site nécessaires à la gestion des appareils mobiles locale.  

1. Sur le serveur de site principal, ouvrez une invite de commandes avec des droits d’administrateur, tapez **MMC** et appuyez sur **Entrée**.  

2. Dans la console MMC, cliquez sur **Fichier** > **Ajouter/supprimer un composant logiciel enfichable**.  

3. Dans le composant logiciel enfichable Certificats, sélectionnez **Certificats**, cliquez sur **Ajouter**, sélectionnez **Compte d’ordinateur**, cliquez sur **Suivant**, sur **Terminer**, puis sur **OK** pour fermer la fenêtre Ajouter/supprimer un composant logiciel enfichable.  

4. Cliquez avec le bouton droit sur **Personnel**, puis cliquez sur **Toutes les tâches** > **Demander un nouveau certificat**.  

5. Dans l’Assistant Inscription de certificats, cliquez sur **Suivant**, sélectionnez **Stratégie d’inscription à Active Directory**, puis cliquez sur **Suivant**.  

6. Cochez la case en regard du certificat de serveur web (**Serveur web ConfigMgr MDM**), puis cliquez sur **Inscrire**.  

7. Une fois que le certificat est inscrit, cliquez sur **Terminer**.  

   Étant donné que chaque serveur a besoin d’un certificat de serveur web unique, vous devez répéter ce processus pour chaque serveur hébergeant l’un des rôles de système de site nécessaire à la gestion des appareils mobiles locale.  Si un serveur héberge tous les rôles système de site, vous ne devez demander qu’un seul certificat de serveur web.  

##  <a name="bkmk_bindCert"></a> Lier le certificat au serveur web  
 Le nouveau certificat doit maintenant être lié au serveur web de chaque serveur de système de site hébergeant les rôles de système de site nécessaires à la gestion des appareils mobiles locale. Procédez de la manière décrite ci-dessous pour chaque serveur hébergeant les rôles système de site point d’inscription et point proxy d’inscription. Si un serveur héberge tous les rôles système de site, vous ne devez suivre ces étapes qu’une seule fois. Vous n’avez pas à effectuer cette tâche pour les rôles système de site point de distribution et point de gestion d’appareil, car ils reçoivent automatiquement le certificat requis lors de l’inscription.  

1.  Sur le serveur hébergeant le point d’inscription, le point proxy d’inscription, le point de distribution ou le point de gestion d’appareil, cliquez sur **Démarrer** > **Outils d’administration** > **Gestionnaire des services Internet**.  

2.  Sous Connexions, accédez à l’option **Site web par défaut**, cliquez dessus avec le bouton droit, puis cliquez sur **Modifier les liaisons...**  

3.  Dans la boîte de dialogue Liaisons de sites, cliquez sur **https**, puis sur **Modifier...**  

4.  Dans la boîte de dialogue Modifier la liaison de site, sélectionnez le certificat que vous venez d’inscrire pour le **certificat SSL**, cliquez sur **OK**, puis sur **Fermer**.  

5.  Dans la console Gestionnaire des services Internet, sous Connexions, sélectionnez le serveur web et, dans le volet Actions à droite, cliquez sur **Redémarrer**.  

##  <a name="bkmk_exportCert"></a> Exporter le certificat ayant la même racine que le certificat de serveur web  
 Les Services de certificats Active Directory installent généralement le certificat requis de l’autorité de certification sur tous les appareils joints au domaine. En revanche, les appareils non joints au domaine ne sont pas en mesure de communiquer avec les rôles système de site sans certificat de l’autorité de certification racine. Pour obtenir le certificat requis pour que les appareils puissent communiquer avec les rôles système de site, vous pouvez l’exporter à partir du certificat lié au serveur web.  

 Pour exporter le certificat racine du certificat du serveur web, procédez comme suit.  

1.  Dans le Gestionnaire des services Internet, cliquez sur **Site web par défaut** puis, dans le volet Action situé à droite, cliquez sur **Liaisons...**  

2.  Dans la boîte de dialogue Liaisons de sites, cliquez sur **https**, puis sur **Modifier...**  

3.  Vérifiez que le certificat de serveur web est bien sélectionné, puis cliquez sur **Afficher…**  

4.  Dans les propriétés du certificat de serveur web, cliquez sur **Chemin d’accès de certification**, sur la racine en haut du chemin d’accès de certification, puis sur **Afficher le certificat**.  

5.  Dans les propriétés du certificat racine, cliquez sur **Détails**, puis sur **Copier dans un fichier...**  

6.  Dans l’Assistant Exportation de certificat, cliquez sur **Suivant**.  

7.  Vérifiez que l’option **X.509 binaire encodé DER (.cer)** est activée pour le format, puis cliquez sur **Suivant**.  

8.  Pour le nom du fichier, cliquez sur **Parcourir...**, choisissez un emplacement pour enregistrer le fichier de certificat, nommez le fichier, puis cliquez sur **Enregistrer**.  

     Les appareils à inscrire devant accéder à ce fichier pour importer le certificat racine, vous devez choisir un emplacement commun accessible à la plupart des ordinateurs et appareils, ou enregistrer le fichier provisoirement dans un emplacement pratique (tel que le lecteur C), puis le déplacer ultérieurement vers un emplacement commun.  

     Cliquez sur **Suivant**.  

9. Vérifiez les paramètres, puis cliquez sur **Terminer**.  
