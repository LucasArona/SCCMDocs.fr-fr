---
title: Créer des éléments de configuration pour les appareils Windows 8.1 et Windows 10 gérés via Microsoft Intune
titleSuffix: Configuration Manager
description: Utilisez l’élément de configuration System Center Configuration Manager Windows 10 pour gérer les paramètres des ordinateurs Windows 10.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 639fabbe1e2f51194669fc1f196d88140193a727
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-configuration-items-for-windows-81-and-windows-10-devices-managed-without-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager

  
 Utilisez l’élément de configuration System Center Configuration Manager **Windows 8.1 et Windows 10** pour gérer les paramètres des appareils Windows 8.1 et Windows 10 qui sont inscrits dans Microsoft Intune ou gérés localement par Configuration Manager.  
  
### <a name="to-create-a-windows-81-and-windows-10-configuration-item"></a>Pour créer un élément de configuration Windows 8.1 et Windows 10  
  
1.  Dans la console Configuration Manager, cliquez sur **Ressources et conformité**.  
  
2.  Dans l'espace de travail **Biens et conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Éléments de configuration**.  
  
3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  
  
4.  Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  
  
5.  Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Windows 8.1 et Windows 10**.  
  
6.  Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  
  
7.  Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez les plateformes Windows spécifiques chargées d’évaluer l’élément de configuration.  
  
8.  Dans la page **Paramètres de périphérique** de l’Assistant, sélectionnez le groupe de paramètres à configurer. Consultez [Informations de référence sur les paramètres d’élément de configuration Windows 8.1 et Windows 10](#BKMK_Setref) dans cette rubrique pour plus d’informations, puis cliquez sur **Suivant**.  
  
    > [!TIP]  
    >  Si le paramètre souhaité n’est pas répertorié, cochez la case **Configurer d’autres paramètres qui ne se trouvent pas dans les groupes de paramètres par défaut**.  
  
9. Dans chaque page de paramètres, configurez les paramètres dont vous avez besoin et indiquez si vous voulez les corriger quand ils ne sont pas conformes sur des périphériques (quand cela est pris en charge).  
  
10. Pour chaque groupe de paramètres, vous pouvez également configurer la gravité signalée quand un élément de configuration n’est pas conforme :  
  
    -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  
  
    -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  
  
    -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  
  
    -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  
  
    -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme événement Windows dans le journal des événements des applications.  
  
11. Dans la page **Condition d’application de la plateforme** de l’Assistant, passez en revue tous les paramètres qui ne sont pas compatibles avec les plateformes prises en charge que vous avez sélectionnées précédemment. Vous pouvez revenir sur ces paramètres et les supprimer, ou vous pouvez continuer.  
  
    > [!TIP]  
    >  La conformité des paramètres non pris en charge n’est pas évaluée.  
  
12. Effectuez toutes les étapes de l'Assistant.  
  
 Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité**.  
  
##  <a name="windows-81-and-windows-10-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration Windows 8.1 et Windows 10  
  
### <a name="password"></a>Mot de passe  
 Ces paramètres concernent uniquement les appareils exécutant Windows 10 et versions ultérieures.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Exiger des paramètres de mot de passe sur les appareils**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant qu'un mot de passe ne doive être modifié.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe déjà utilisés.|  
|**Nombre d'échecs de tentative de connexion avant que l'appareil soit réinitialisé**|Réinitialise l'appareil si le nombre d'échecs de tentative de est atteint.|  
|**Durée d’inactivité avant le verrouillage de l’appareil**|Spécifiez la durée pendant laquelle un appareil peut rester inactif (sans interaction de l’utilisateur) avant d’être verrouillé.|  
|**Complexité du mot de passe**|Choisissez si vous pouvez spécifier un code confidentiel tel que « 1234 » ou si vous devez fournir un mot de passe fort.|  
|**Qualité du mot de passe**|Sélectionnez le niveau de complexité du mot de passe requis et spécifiez si les appareils biométriques peuvent être utilisés.|  
|**Envoyer le code PIN de récupération du mot de passe au serveur Exchange Server**|-|
|**Chiffrement de l’appareil**|Activez le chiffrement sur les appareils ciblés.|  
  
###  <a name="device"></a>Appareil  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Capture d'écran**|Permet de prendre une capture d'écran de l'affichage de l'appareil.<br /><br /> (Windows 10 uniquement)|  
|**Envoi des données de diagnostic**|Autorisez l'envoi des journaux d'application.<br /><br /> (Windows 8.1 uniquement)|  
|**Envoi des données de diagnostic (Windows 10)**|Autorisez l'envoi des journaux d'application.<br /><br /> (Windows 10 uniquement)|  
|**Géolocalisation**|Autorisez l'appareil à utiliser les informations des services d'emplacement.<br /><br /> (Windows 10 uniquement)|  
|**Copier et coller**|Utilisez le copier-coller pour transférer des données entre les applications.<br /><br /> (Windows 10 uniquement)|
|**Réinitialisation aux paramètres d’usine**|Permet à l’utilisateur final de réinitialiser les paramètres initiaux de l’appareil.<br /><br /> (Windows 10 uniquement)|  
|**BlueTooth**|Autorisez l'utilisation de la fonctionnalité Bluetooth des appareils.|  
|**Mode découvrable Bluetooth**|Autorisez la découverte de l’appareil par d’autres appareils Bluetooth.<br /><br /> (Windows 10 uniquement)|  
|**Publicité Bluetooth**|Autoriser l’utilisation de la publicité Bluetooth.<br /><br /> (Windows 10 uniquement)|  
|**Enregistrement vocal**|Autorisez l’utilisation des fonctionnalités d’enregistrement de la voix de l’appareil.<br /><br /> (Windows 10 uniquement)|
|**Cortana**|Autorisez l’utilisation de l’Assistant vocal Cortana.<br /><br /> (Windows 10 uniquement)|
|**Notifications Sécurité et maintenance**|Activez ou désactivez le volet de notifications dans Windows 10. <br /><br /> (Windows 10 uniquement)|
|**Modification des paramètres de région (version de bureau uniquement)**|Empêche l’utilisateur final de changer les paramètres de région sur l’appareil.|
|**Modification des paramètres d’alimentation et de veille (poste de travail uniquement)**|Empêche l’utilisateur final de changer les paramètres d’alimentation et de veille sur l’appareil.|
|**Modification des paramètres de langue (poste de travail uniquement)**|Empêche l’utilisateur de changer les paramètres de langue sur l’appareil.|
|**Modification de l’heure du système**|Empêche l’utilisateur final de changer les date et heure sur l’appareil.|
|**Changement de nom d’appareil**|Empêche l’utilisateur final de changer le nom de l’appareil.|
  
### <a name="email-management"></a>Gestion de la messagerie  
 Ces paramètres concernent les appareils exécutant Windows 8.1 et Windows 10.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Messagerie POP et IMAP**|Autorise la connexion à des comptes de messagerie qui utilisent les normes POP et IMAP.|  
|**Durée de conservation maximum des courriers électroniques**|Durée de conservation des courriers électroniques avant qu'ils ne soient supprimés du serveur.|  
|**Formats de message autorisés**|Spécifiez si les courriers électroniques des utilisateurs peuvent être au format HTML ou au format texte brut uniquement.|  
|**Taille maximale des messages en texte brut (téléchargés automatiquement)**|Contrôle la taille maximale des courriers électroniques en texte brut lorsqu'ils sont automatiquement téléchargés.|  
|**Taille maximale des messages HTML (téléchargés automatiquement)**|Contrôle la taille maximale des courriers électroniques HTML lorsqu'ils sont automatiquement téléchargés.|  
|**Taille maximum d'une pièce jointe (téléchargée automatiquement)**|Configure la taille maximale des e-mails qui sont téléchargés automatiquement.|  
|**Synchronisation du calendrier**|Autoriser la synchronisation des calendriers sur l’appareil.|  
|**Compte de messagerie personnalisé**|Autorisez l'utilisation d'un compte non Microsoft sur l'appareil.|  
|**Rendre le compte Microsoft facultatif dans l'application Windows Mail**|Configurez cette option pour supprimer l’obligation de disposer d’un compte Microsoft dans Windows Mail.|  
  
### <a name="store"></a>Magasin  
 Ces paramètres concernent uniquement les appareils exécutant Windows 10 et versions ultérieures.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Boutique d'applications**|Permet d'accéder à l'App Store sur l'appareil.|  
|**Entrer un mot de passe pour accéder à la boutique d'applications**|Les utilisateurs doivent entrer un mot de passe pour accéder à l'App Store.|  
|**Achats dans l'application**|Autorise les utilisateurs à effectuer des achats dans l'application.|
|**Mettre à jour automatiquement les applications du Store**|Permet la mise à jour automatique des applications installées à partir du Windows Store.|
|**Utiliser uniquement le magasin privé**|Activez cette option pour n’autoriser les utilisateurs à télécharger des applications qu’à partir de votre magasin privé.|
|**Stocker le démarrage de l’application d’origine**|Désactive toutes les applications qui ont été préinstallées sur l’appareil ou téléchargées à partir du Windows Store.|
  
### <a name="browser"></a>Navigateur  
 Ces paramètres concernent les appareils exécutant Windows 8.1 et Windows 10.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Autoriser le navigateur web**|Autoriser l’utilisation du navigateur web sur l’appareil.|  
|**Remplissage automatique**|L'utilisateur peut modifier les paramètres de saisie semi-automatique dans le navigateur.|  
|**Active scripting**|Le navigateur peut exécuter des scripts, tels que les scripts ActiveX.|  
|**Plug-ins**|L'utilisateur peut ajouter des plug-ins à Internet Explorer.|  
|**Bloqueur de fenêtres publicitaires**|Active ou désactive le bloqueur de fenêtres publicitaires du navigateur.|  
|**Cookies**|Autorisez l'enregistrement des cookies sur l'appareil.|  
|**Avertissement de fraude**|Activez ou désactivez les avertissements des sites Web frauduleux potentiels.|  
  
###  <a name="internet-explorer"></a>Internet Explorer  
 Ces paramètres concernent les appareils exécutant Windows 8.1 et Windows 10.  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Toujours envoyer un en-tête Aucun tracking**|Empêche que les informations d'exploration ne soient envoyées à des sites tiers.|  
|**Zone de sécurité intranet**|Attribuer un niveau de sécurité à la zone de sécurité intranet.|  
|**Niveau de sécurité de la zone Internet**|Configurez le niveau de sécurité pour la zone Internet.|  
|**Niveau de sécurité de la zone intranet**|Configurez le niveau de sécurité pour la zone intranet.|  
|**Niveau de sécurité de la zone Sites de confiance**|Configurez le niveau de sécurité pour la zone Sites de confiance.|  
|**Niveau de sécurité de la zone des sites sensibles**|Configurez le niveau de sécurité pour la zone des sites sensibles.|  
|**Espaces de noms pour la zone intranet**|Configurer les sites web qui sont ajoutés ou supprimés dans la zone intranet.|  
|**Accéder à un site intranet pour une entrée à mot unique**|Active ou désactive le paramètre qui permet à Internet Explorer d'accéder automatiquement à un site Intranet si un nom de site valide est entré sans être précédé de HTTP :|  
|**Option de menu du mode entreprise**|Autorisez les utilisateurs à activer et désactiver le mode Entreprise à partir du menu **Outils** d’Internet Explorer.|  
|**Emplacement du rapport de journalisation (URL)**|Spécifiez une URL où les sites web visités sont enregistrés quand le Mode entreprise est actif.|  
|**Emplacement de la liste des sites en Mode entreprise (URL)**|Spécifiez l’emplacement de la liste des sites web qui utilisent le Mode entreprise quand il est actif.|  
  
###  <a name="cloud"></a>Cloud  
 Ces paramètres concernent les appareils exécutant Windows 8.1 et Windows 10.  
  
|Nom du paramètre|Détails|Windows 8.1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**Synchronisation des paramètres**|Permet la synchronisation des paramètres entre les appareils.|Oui|Oui|  
|**Synchronisation des informations d'identification**|Permet la synchronisation des informations d'identification entre les appareils.|Oui|Oui|  
|**Compte Microsoft**|Autorisez l'utilisation d'un compte Microsoft sur l'appareil.|Oui|Oui|  
|**Synchronisation des paramètres via des connexions limitées**|Autorisez la synchronisation des paramètres quand la connexion Internet est mesurée.|Oui|Oui|  
  
###  <a name="security"></a>Sécurité  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Installation du fichier non signé**|Autorise le chargement des fichiers non signés.<br /><br /> (Windows 10 uniquement)|  
|**Applications non signées**|Autorise le chargement des applications non signées.<br /><br /> (Windows 10 uniquement)|  
|**Messagerie SMS et MMS**|Autorisez les messages SMS et MMS à partir de l'appareil.<br /><br /> (Windows 10 uniquement)|  
|**Stockage amovible**|Autorisez l'utilisation du stockage amovible, comme une carte SD sur l'appareil.<br /><br /> (Windows 10 uniquement)|  
|**Appareil photo**|Autorisez l'utilisation de l'appareil photo.<br /><br /> (Windows 10 uniquement)|  
|**Communication en champ proche (NFC)**|Autorisez la communication à l'aide de NFC sur l'appareil.<br /><br /> (Windows 10 uniquement)|  
|**Mode antivol**|Détermine si le mode antivol de Windows 10 est activé.<br /><br /> (Windows 10 uniquement)|  
|**Autoriser la connexion USB**|Permet à des appareils de se connecter à cet appareil à l’aide d’une connexion USB.<br /><br /> (Windows 10 uniquement)|
|**Fichier de profil**|Configure un profil VPN de profil pour les appareils Windows RT.<br /><br /> Windows 8.1 uniquement)|  
|**Nom du profil**|Configure un profil VPN de profil pour les appareils Windows RT.<br /><br /> Windows 8.1 uniquement)|  
|**Profil pour tous les utilisateurs**|Configure un profil VPN de profil pour les appareils Windows RT.<br /><br /> Windows 8.1 uniquement)|  
  
###  <a name="peak-synchronization"></a>Synchronisation de pointe  
 Ces paramètres concernent uniquement les appareils exécutant Windows 10 et versions ultérieures.  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Spécifier les heures de pointe**|Configurer la période de pointe pour la synchronisation des appareils mobiles.|  
|**Fréquence de synchronisation pendant les heures de pointe**|Configurer la fréquence à laquelle la synchronisation se produit pendant les heures de pointe que vous avez configurées.|  
|**Fréquence de synchronisation pendant les heures creuses**|Configurer la fréquence à laquelle la synchronisation se produit en dehors des heures de pointe que vous avez configurées.|  
  
###  <a name="roaming"></a>Itinérant  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Gestion des appareils en itinérance**|Permet à l’appareil d’être géré par Configuration Manager en phase d’itinérance.<br /><br /> (Windows 10 uniquement)|  
|**Téléchargement de logiciel en itinérance**|Permet de télécharger des applications et des logiciels lors de l'itinérance.<br /><br /> (Windows 10 uniquement)|  
|**Téléchargement d'e-mails en itinérance**|Autorise les téléchargements de courrier électronique lors de l'itinérance.<br /><br /> (Windows 10 uniquement)|  
|**Itinérance des données**|Autorisez l'itinérance entre réseaux lors de l'accès aux données.| 
|**VPN sur réseau de téléphonie mobile**|Permet à l’appareil d’accéder aux connexions VPN quand il est connecté à un réseau de téléphonie mobile.<br /><br /> (Windows 10 uniquement)|
|**Itinérance VPN sur réseau de téléphonie mobile**|Permet à l’appareil d’accéder aux connexions VPN quand il est en itinérance sur un réseau de téléphonie mobile.<br /><br /> (Windows 10 uniquement)| 
  
###  <a name="encryption"></a>Chiffrement  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Chiffrement de la carte de stockage**|Exigez le chiffrement des cartes de stockage utilisées avec l'appareil.<br /><br /> (Windows 10 uniquement)|  
|**Chiffrement des fichiers sur l’appareil**|Exige que les fichiers soient chiffrés sur le périphérique.|  
|**Demander la signature des courriers électroniques**|Requiert la signature des messages électroniques avant leur envoi.|  
|**Algorithme de signature**|Sélectionnez l’algorithme de signature pour les messages électroniques signés.|  
|**Demander le chiffrement des courriers électroniques**|Requiert le chiffrement des messages électroniques avant leur envoi.|  
|**Algorithme de chiffrement**|Sélectionnez l’algorithme de chiffrement des messages électroniques.|  
  
###  <a name="wireless-communications"></a>Communications sans fil  
 Ces paramètres concernent uniquement les appareils exécutant Windows 10 et versions ultérieures.  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Connexion réseau sans fil**|Activez ou désactivez la fonctionnalité Wi-Fi des appareils.|  
|**Connexion Wi-Fi**|Les utilisateurs peuvent utiliser leur appareil en tant que point d'accès sans fil mobile.|  
|**Décharger les données en Wi-Fi si possible**|Configurez cette option pour utiliser la connexion Wi-Fi sur le périphérique lorsque cela est possible.|  
|**Rapports de point d'accès Wi-Fi**|-|  
|**Configuration manuelle du Wi-Fi**|-|  
  
#### <a name="to-configure-a-wireless-network-connection"></a>Pour configurer une connexion réseau sans fil  
  
1.  Dans la page **Configurer les paramètres de communication sans fil de l'appareil mobile** , cliquez sur **Ajouter**.  
  
2.  Dans la boîte de dialogue **Connexion réseau sans fil**, spécifiez les informations suivantes sur la connexion sans fil qui est configurée sur les appareils mobiles :  
  
|Paramètre|Plus d'informations|  
|-------------|----------------------|  
|**Nom réseau (SSID)**|Entrez le nom du réseau Wi-Fi.|  
|**Connexion réseau**|Choisissez entre **Internet** et **Travail**.|  
|**Authentification**|Sélectionnez la méthode d'authentification de la connexion sans fil :<br /><br /> - **Ouvrir**<br /><br /> - **Partagé**<br /><br /> - **WPA**<br /><br /> - **WPA-PSK**<br /><br /> - **WPA2**<br /><br /> - **WPA2-PSK**|  
|**Chiffrement des données**|Choisissez la méthode de chiffrement utilisée par cette connexion. Les valeurs possibles varient en fonction de la méthode **d’Authentification** sélectionnée :<br /><br /> - **Désactivé**<br /><br /> - **WEP**<br /><br /> - **TKIP**<br /><br /> - **AES**|  
|**Index de clé**|Sélectionnez un index de clé entre **1** et **4**, qui est utilisé avec un paramètre **Chiffrement des données** de **WEP**.|  
|**Ce réseau se connecte à Internet**|Sélectionnez cette option si vous souhaitez fournir des paramètres de proxy qui permettent aux appareils mobiles d'établir une connexion sans fil à Internet.|  
|**Paramètres du serveur proxy**|Spécifiez si nécessaire les paramètres **Serveur** et **Port** pour **HTTP**, **WAP** et **Sockets**.|  
|**Activer l'accès réseau 802.1X**|Sélectionnez cette option si vous souhaitez sécuriser la connexion en spécifiant un type EAP.|  
|**Type EAP**|Choisissez le type EAP à utiliser :<br /><br /> - **PEAP**<br> - **Carte à puce ou certificat**|  
  
  
  
### <a name="certificates"></a>Certificats  
 Importez les certificats à installer sur les appareils mobiles.  
  
 Cliquez sur **Importer**, puis spécifiez les valeurs suivantes :  
  
-   **Fichier de certificat** : cliquez sur Parcourir, puis sélectionnez le fichier de certificat avec l’extension **.cer** que vous souhaitez importer.  
  
-   **Banque d’informations de destination** : choisissez une ou plusieurs banques de destination où le certificat importé est ajouté sur l’appareil mobile :  
  
    -   **Racine**  
  
    -   **Autorité de certification**  
  
    -   **Normal**  
  
    -   **Privilégié**  
  
    -   **SPC**  
  
    -   **Homologue**  
  
-   **Rôle** : si **SPC** (Software Publisher Certificate) est sélectionné en tant que banque de destination, choisissez le rôle qui est associé au certificat :  
  
    -   **Opérateur mobile**  
  
    -   **Gestionnaire**  
  
    -   **Utilisateur authentifié**  
  
    -   **Administrateur informatique**  
  
    -   **Utilisateur non authentifié**  
  
    -   **Serveur d’approvisionnement approuvé**  
  
### <a name="system-security"></a>Sécurité système  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Contrôle de compte d'utilisateur**|Active ou désactive le contrôle de compte d'utilisateur Windows sur l'appareil.|  
|**Pare-feu réseau**|Active ou désactive le pare-feu Windows.<br /><br /> (Windows 8.1 uniquement)|  
|**Mises à jour (Windows 8.1 et versions antérieures)**|Choisissez le mode de téléchargement des mises à jour logicielles Windows sur les ordinateurs. Par exemple, vous pouvez télécharger automatiquement les mises à jour, mais permettre à l'utilisateur de choisir à quel moment les installer.|  
|**Classification minimale des mises à jour**|Choisissez la classification minimale des mises à jour téléchargées sur les ordinateurs Windows : **Aucune**, **Importante** ou **Recommandée**.|  
|**Mises à jour (Windows 10)**|Choisissez le mode de téléchargement des mises à jour logicielles Windows sur les ordinateurs. Par exemple, vous pouvez télécharger automatiquement les mises à jour, mais permettre à l'utilisateur de choisir à quel moment les installer.<br /><br /> (Windows 10 uniquement)|  
|**Jour d’installation**|Choisissez le jour où les mises à jour sont installées.<br /><br /> (Windows 10 uniquement)|  
|**Heure d’installation**|Choisissez l’heure à laquelle les mises à jour sont installées.<br /><br /> (Windows 10 uniquement)|  
|**SmartScreen**|Activez ou désactivez Windows SmartScreen.|  
|**Protection antivirus**|Sélectionnez cette option pour vous assurer qu’un logiciel antivirus est installé sur l’appareil.|  
|**Les signatures de la protection antivirus sont à jour**|Sélectionnez cette option pour vous assurer que les fichiers de signature antivirus sont à jour.|  
|**Fonctionnalités de la version préliminaire**|Permet à Microsoft de déployer des versions préliminaires de paramètres et de fonctionnalités sur le périphérique.<br /><br /> (Windows 10 uniquement)|  
|**Installation manuelle du certificat racine**|(Windows 10 uniquement)| 
|**Autoriser la désinscription manuelle**|Permet à l’utilisateur de se désinscrire de la gestion par une solution de gestion des appareils mobiles.| 
  
###  <a name="windows-server-work-folders"></a>Dossiers de travail du serveur Windows  
 Ces paramètres concernent les appareils exécutant Windows 8.1 et Windows 10.  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**URL des dossiers de travail**|Configure l'emplacement d'un dossier de travail Windows Server auquel les utilisateurs peuvent se connecter à partir de leur appareil.|  
  
### <a name="allowed-and-blocked-apps-windows-phone-only"></a>Applications autorisées et bloquées (Windows Phone uniquement)  
 Permet de spécifier la liste des applications gérées par Intune qui sont conformes ou non conformes au sein de votre entreprise. Windows Phone peut autoriser ou bloquer l’installation de ces applications.  
  
 Vous ne pouvez pas spécifier à la fois les applications conformes et non conformes dans le même élément de configuration.  
  
#### <a name="to-specify-apps-that-are-allowed-or-blocked"></a>Pour spécifier les applications autorisées ou bloquées  
  
Dans la page **Liste des applications autorisées et bloquées**, spécifiez les informations suivantes :  
  
|Paramètre|Plus d'informations|  
    |-------------|----------------------|  
    |**Liste des applications bloquées**|Sélectionnez cette option si vous souhaitez spécifier une liste d’applications que les utilisateurs ne sont pas autorisés à installer.|  
    |**Liste des applications autorisées**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications que les utilisateurs sont autorisés à installer. L’installation de toutes les autres applications est bloquée.|  
    |**Ajouter**|Ajoute une application à la liste sélectionnée. Spécifiez le nom de votre choix, éventuellement l’éditeur de l’application, ainsi que l’URL de l’application dans la boutique d’applications.<br /><br /> Pour spécifier l’URL, dans le Windows Store, recherchez l’application à utiliser.<br /><br /> Ouvrez la page de l'application, puis copiez l'URL dans le Presse-papiers. Vous pouvez maintenant utiliser cette URL dans la liste des applications autorisées ou bloquées.<br /><br /> **Exemple :** recherchez l’application **Skype** dans le Store. L’URL que vous utilisez est **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Éditer**|Vous permet de modifier le nom, l'éditeur et l'URL de l'application sélectionnée.|  
    |**Supprimer**|Supprime l'application sélectionnée dans la liste.|  
    |**Importerer**|Importe une liste d'applications que vous avez spécifiée dans un fichier de valeurs séparées par des virgules. Utilisez le format Nom de l'application, Éditeur, URL de l'application dans le fichier.|  
  
### <a name="windows-10-team"></a>Équipe Windows 10  
 Ces paramètres concernent uniquement les appareils exécutant Windows 10 Collaboration.  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Autoriser l’écran à sortir de veille automatiquement quand les capteurs détectent la présence d’une personne dans la pièce**|Permet à l’appareil de sortir automatiquement quand son capteur détecte la présence d’une personne dans la pièce.|  
|**Code PIN exigé pour la projection sans fil**|Indique si vous devez entrer un code confidentiel avant de pouvoir utiliser les fonctionnalités de projection sans fil de l’appareil.|  
|**Fenêtre de maintenance**|Configure la fenêtre quand des mises à jour peuvent avoir lieu sur l’appareil. Vous pouvez configurer l’heure de début de la fenêtre et la durée (de 1 à 5 heures).|
|**Azure Operational Insights**|Azure Operational Insights, qui fait partie de la suite Microsoft Operations Manager, collecte, stocke et analyse les données des fichiers journaux provenant des appareils Windows 10 Collaboration.<br>Pour vous connecter à Azure Operational Insights, vous devez spécifier un ID d’espace de travail et une Clé d’espace de travail.| 
|**Projection sans fil Miracast**|Activez cette option si vous voulez permettre à l’appareil Windows 10 Collaboration d’utiliser des appareils compatibles Miracast pour la projection.<br>Si vous activez cette option, dans **Choisir un canal Miracast**, sélectionnez le canal Miracast utilisé projeter du contenu.|
|**Informations sur la réunion affichées sur l’écran d’accueil**|Si vous activez cette option, vous pouvez choisir les informations qui sont affichées sur la vignette **Réunions** de l’écran **Bienvenue**. Vous pouvez :<br><br>- **Afficher uniquement l’organisateur et l’heure**<br>- **Afficher l’organisateur, l’heure et l’objet (objet masqué pour les réunions privées)**|
|**URL de l’image d’arrière-plan de l’écran de verrouillage**|Utilisez ce paramètre pour afficher un arrière-plan personnalisé sur l’écran **Bienvenue** des appareils Windows 10 Collaboration à partir de l’URL que vous spécifiez.<br>L’image doit être au format PNG et l’URL doit commencer par **https://**.| 
  
### <a name="windows-information-protection"></a>Protection des informations Windows  

Avec l’augmentation du nombre d’appareils appartenant aux employés au sein de l’entreprise, il existe un risque accru de fuites accidentelles de données via les applications et les services, tels que le courrier électronique, les réseaux sociaux et le cloud public, qui sont en dehors du contrôle de l’entreprise. C’est par exemple le cas quand un employé envoie les dernières photos de conception à partir de son compte de messagerie personnel, quand il copie et colle des informations sur des produits dans un tweet ou quand il enregistre un rapport des ventes en cours dans son stockage cloud public.

La Protection des informations Windows (WIP) vous protège contre ces fuites de données potentielles sans interférer avec l’expérience de l’employé. WIP contribue aussi à protéger les données et les applications d’entreprise contre les fuites accidentelles de données sur les appareils d’entreprise et les appareils personnels que les employés apportent sur leur lieu de travail, sans exiger de modifications au niveau de votre environnement ou d’autres applications.

 Les paramètres des éléments de configuration WIP de Configuration Manager permettent de gérer la liste des applications protégées par EDP, les emplacements réseau de l’entreprise, le niveau de protection et les paramètres de chiffrement.

Pour plus d’informations sur la configuration de la protection des données d’entreprise avec Configuration Manager, consultez [Protéger vos données d’entreprise à l’aide de la Protection des informations Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).


### <a name="microsoft-edge"></a>Microsoft Edge  
Ces paramètres concernent les appareils exécutant Windows 10 et versions ultérieures.  
  
|Nom du paramètre|Détails|  
|------------------|-------------| 
|Microsoft Edge|Autoriser l’utilisation du navigateur web Edge sur l’appareil.| 
|**Autoriser les suggestions de recherche dans la barre d’adresse**|Permet à votre moteur de recherche de suggérer des sites lorsque vous tapez des expressions de recherche.|  
|**Autoriser l’envoi du trafic intranet vers Internet Explorer**||  
|**Autoriser l’absence de suivi**|La fonctionnalité Do Not Track (Ne pas me suivre) informe des sites web que vous ne souhaitez qu’ils suivent votre visite sur un site.|  
|**Activer SmartScreen**|Utilisez SmartScreen pour vérifier que les fichiers que vos utilisateurs téléchargent ne contiennent pas de code malveillant.|  
|**Autoriser les fenêtres contextuelles**|Autoriser ou désactiver les Fenêtres contextuelles du navigateur.|  
|**Autoriser les cookies**|Autoriser ou désactiver les cookies.|  
|**Autoriser le remplissage automatique**|Autoriser l’utilisation de la fonctionnalité de remplissage automatique du navigateur Edge.|  
|**Autoriser le gestionnaire de mots de passe**|Autoriser l’utilisation de la fonctionnalité de gestionnaire des mots de passe du navigateur Microsoft Edge.|  
|**Emplacement de la liste des sites en mode entreprise**|Indique où trouver la liste des sites web qui s’ouvrent en Mode entreprise. Les utilisateurs ne peuvent pas modifier cette liste.|
|**Bloquer l’accès à about:flags**|Empêcher l’utilisateur final d’accéder à la page about:flags dans Edge qui contient les paramètres de développeur et expérimentaux.|
|**Remplacement de l’invite de commandes SmartScreen**|Autoriser l’utilisateur final à ignorer les avertissements du filtre SmartScreen concernant les sites web potentiellement malveillants.|
|**Remplacement de l’invite de commandes SmartScreen pour les fichiers**|Autoriser l’utilisateur final à ignorer les avertissements du filtre SmartScreen concernant le téléchargement de fichiers potentiellement malveillants.|
|**Adresse IP localhost WebRTC**|Empêcher l’affichage de l’adresse IP localhost de l’utilisateur quand celui-ci passe des appels téléphoniques à l’aide du protocole RTC web.|
|**Moteur de recherche par défaut**|Spécifier le moteur de recherche par défaut à utiliser. Les utilisateurs finaux peuvent changer cette valeur à tout moment.|
|**URL OpenSearch XML**|Vous pouvez utiliser un fichier XML OpenSearch afin de créer un service de recherche pour Microsoft Edge.<br>Pour plus d’informations, consultez [OpenSearch](https://msdn.microsoft.com/library/windows/desktop/dd940337).|
|**Pages d’accueil (version de bureau uniquement)**|Ajouter une liste de sites que vous souhaitez utiliser en tant que pages d’accueil dans le navigateur Microsoft Edge (version de bureau uniquement).|  


### <a name="windows-defender"></a>Windows Defender
Ces paramètres concernent les appareils exécutant Windows 10 et versions ultérieures.
 
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Autoriser la surveillance en temps réel**|Active l’analyse en temps réel pour les logiciels malveillants, les logiciels espions et d’autres logiciels indésirables.|
|**Autoriser la surveillance du comportement**|Permet à Defender de rechercher certains modèles connus d’activité suspecte sur les appareils.|
|**Activer le système NIS (Network Inspection System)**|Le système NIS (Network Inspection System) vous aide à protéger les appareils contre les attaques réseau à l’aide de signatures de vulnérabilités connues provenant de Microsoft Endpoint Protection Center pour détecter et bloquer le trafic malveillant.|
|**Analyser tous les téléchargements**|Contrôle si Defender analyse tous les fichiers téléchargés depuis Internet.|
|**Autoriser l’analyse des scripts**|Permet à Defender d’analyser les scripts utilisés dans Internet Explorer.|
|**Surveiller l’activité des fichiers et des programmes**|Permet à Defender de surveiller l’activité des programmes et des fichiers sur les appareils.
|**Durée du suivi des logiciels malveillants dont le cas a été résolu (en jours)**|Permet à Defender de continuer à effectuer le suivi des logiciels malveillants résolus pour le nombre de jours que vous spécifiez, ce qui vous permet de vérifier manuellement les appareils précédemment affectés. Si vous définissez le nombre de jours à 0, les logiciels malveillants restent dans le dossier Quarantaine et ne sont pas supprimés automatiquement.|
|**Autoriser l’accès à l’interface utilisateur du client**|Détermine si l’interface utilisateur de Windows Defender est masquée aux utilisateurs.<br>Quand ce paramètre est changé, il prend effet lors du redémarrage suivant de l’ordinateur de l’utilisateur.|
|**Planifier une analyse du système**|Permet de planifier une analyse du système complète ou rapide qui se produit régulièrement au jour et à l’heure que vous sélectionnez.|
|**Planifier une analyse quotidienne rapide**|Permet de planifier une analyse rapide qui se produit tous les jours à l’heure que vous sélectionnez
|**Limiter l’utilisation de l’UC pendant une analyse**|Permet de limiter la quantité d’UC que les analyses sont autorisées à utiliser (de 1 à 100).|
|**Analyser les fichiers d’archive**|Permet à Defender d’analyser les fichiers archivés, comme les fichiers .zip ou .cab.|
|**Analyser les e-mails**|Permet à Defender d’analyser les e-mails dès qu’ils arrivent sur l’appareil.|
|**Analyser les lecteurs amovibles**|Permet à Defender d’analyser les lecteurs amovibles, comme les clés USB.|
|**Analyser les lecteurs mappés**|Permet à Defender d’analyser les fichiers sur des lecteurs réseau mappés.<br>Si les fichiers sur le disque sont en lecture seule, Defender ne peut pas y supprimer les logiciels malveillants détectés.|
|**Analyser les fichiers ouverts à partir de dossiers partagés sur le réseau**|Permet à Defender d’analyser les fichiers sur des lecteurs réseau partagés (par exemple ceux qui sont accessibles à partir d’un chemin UNC)<br>Si les fichiers sur le disque sont en lecture seule, Defender ne peut pas y supprimer les logiciels malveillants détectés.|
|**Intervalle de mise à jour des signatures**|Spécifie l’intervalle auquel Defender recherche de nouveaux fichiers de signatures.
|**Activer la protection cloud**|Autorise ou bloque la réception par Microsoft Active Protection Service d’informations sur l’activité des logiciels malveillants en provenance des appareils que vous gérez. Ces informations sont utilisées pour améliorer le service.|
|**Demander aux utilisateurs d’envoyer des exemples**|Contrôle si les fichiers susceptibles de nécessiter davantage d’analyse sont automatiquement envoyés à Microsoft pour déterminer s’ils sont malveillants.|
|**Détection des applications potentiellement indésirables**|Protège les postes de travail Windows inscrits contre l’exécution de logiciels classés par Windows Defender comme potentiellement indésirables. Vous pouvez protéger contre l’exécution de ces applications ou utiliser le mode audit pour signaler quand une application potentiellement indésirable est installée.|
|**Exclusion de fichiers et de dossiers**|Ajoute un ou plusieurs fichiers et dossiers, comme C:\Chemin ou %ProgramFiles%\Chemin\nom_fichier.exe, à la liste des exclusions. Ces fichiers et dossiers ne sont pas inclus dans les analyses en temps réel ou planifiées.|
|**Exclusions des extensions de fichier**|Ajoute une ou plusieurs extensions de fichier, comme jpg ou txt, à la liste des exclusions. Les fichiers avec ces extensions ne sont pas inclus dans les analyses en temps réel ou planifiées.|
|**Exclusions des processus**|Ajoute un ou plusieurs processus du type .exe, .com ou .scr à la liste des exclusions. Ces processus ne sont pas inclus dans les analyses en temps réel ou planifiées.|

  
## <a name="see-also"></a>Voir aussi  
 [Éléments de configuration pour les appareils gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)