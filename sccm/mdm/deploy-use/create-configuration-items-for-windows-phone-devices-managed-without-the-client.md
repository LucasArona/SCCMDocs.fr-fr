---
title: Comment créer des éléments de configuration pour les appareils Windows Phone gérés via Microsoft Intune
titleSuffix: Configuration Manager
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: df10dc4d-c9ff-4574-bb33-8d30eb14cfe3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 29b46cc49930d47439dc5e60b72e4bf5017829b9
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139219"
---
# <a name="how-to-create-configuration-items-for-windows-phone-devices-managed-without-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration pour des appareils Windows Phone gérés sans le client System Center Configuration Manager
Utilisez l’élément de configuration System Center Configuration Manager **Windows Phone** pour gérer les paramètres des appareils Windows Phone qui sont inscrits dans Microsoft Intune ou gérés localement par Configuration Manager.  
  
### <a name="to-create-a-windows-phone-configuration-item"></a>Pour créer un élément de configuration Windows Phone  
  
1. Dans la console Configuration Manager, cliquez sur **Ressources et conformité**.  
  
2. Dans l'espace de travail **Biens et conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Éléments de configuration**.  
  
3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  
  
4. Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  
  
5. Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Windows Phone**.  
  
6. Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  
  
7. Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez les plateformes Windows Phone spécifiques chargées d’évaluer l’élément de configuration.  
  
8. Dans la page **Paramètres de périphérique** de l’Assistant, sélectionnez le groupe de paramètres à configurer. Consultez [Informations de référence sur les paramètres d’élément de configuration Windows Phone](#BKMK_Setref) dans cette rubrique pour plus d’informations, puis cliquez sur **Suivant**.  
  
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
  
    Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et conformité** .  
  
##  <a name="windows-phone-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration Windows Phone  
  
### <a name="password"></a>Mot de passe  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Exiger des paramètres de mot de passe sur les appareils**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant qu'un mot de passe ne doive être modifié.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe déjà utilisés.|  
|**Nombre d'échecs de tentative de connexion avant que l'appareil soit réinitialisé**|Réinitialise l'appareil si le nombre d'échecs de tentative de est atteint.|  
|**Complexité du mot de passe**|Choisissez si vous pouvez spécifier un code confidentiel tel que « 1234 » ou si vous devez fournir un mot de passe fort.|  
|**Envoyer le code PIN de récupération du mot de passe au serveur Exchange Server**||  
  
### <a name="device"></a>Appareil  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Capture d'écran**|Autorisez l’utilisateur à prendre une capture d’écran de l’affichage de l’appareil.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Envoi des données de diagnostic**|Autorisez l'envoi des journaux d'application.|  
|**Géolocalisation**|Autorisez l'appareil à utiliser les informations des services d'emplacement.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Copier et coller**|Utilisez le copier-coller pour transférer des données entre les applications.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**BlueTooth**|Autorisez l’utilisation de la fonctionnalité Bluetooth de l’appareil.|  
  
### <a name="email-management"></a>Gestion de la messagerie  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Messagerie POP et IMAP**|Autorise la connexion à des comptes de messagerie qui utilisent les normes POP et IMAP.|  
|**Durée de conservation maximum des courriers électroniques**|Durée de conservation des courriers électroniques avant qu'ils ne soient supprimés du serveur.|  
|**Formats de message autorisés**|Spécifiez si les courriers électroniques des utilisateurs peuvent être au format HTML ou au format texte brut uniquement.|  
|**Taille maximale des messages en texte brut (téléchargés automatiquement)**|Contrôle la taille maximale des courriers électroniques en texte brut lorsqu'ils sont automatiquement téléchargés.|  
|**Taille maximale des messages HTML (téléchargés automatiquement)**|Contrôle la taille maximale des courriers électroniques HTML lorsqu'ils sont automatiquement téléchargés.|  
|**Taille maximum d'une pièce jointe (téléchargée automatiquement)**|Configure la taille maximale des courriers électroniques qui seront téléchargés automatiquement.|  
|**Synchronisation du calendrier**||  
|**Compte de messagerie personnalisé**|Autorisez l'utilisation d'un compte non Microsoft sur l'appareil.|  
|**Rendre le compte Microsoft facultatif dans l'application Windows Mail**|Ne pas demander l’utilisation d’un compte Microsoft pour la connexion à Windows Mail.|  
  
### <a name="store"></a>Magasin  
 Ces paramètres s’appliquent aux appareils Windows Phone 8.1 uniquement.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Boutique d'applications**|Permet d'accéder à l'App Store sur l'appareil.|  
  
### <a name="browser"></a>Navigateur  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Autoriser le navigateur web**|Activez ou désactivez le navigateur Internet par défaut.|  
|**Remplissage automatique**|L'utilisateur peut modifier les paramètres de saisie semi-automatique dans le navigateur.|  
|**Active scripting**|Le navigateur peut exécuter des scripts, tels que les scripts ActiveX.|  
|**Plug-ins**|L'utilisateur peut ajouter des plug-ins à Internet Explorer.|  
|**Bloqueur de fenêtres publicitaires**|Active ou désactive le bloqueur de fenêtres publicitaires du navigateur.|  
|**Avertissement de fraude**|Activez ou désactivez les avertissements des sites Web frauduleux potentiels.|  
  
### <a name="internet-explorer"></a>Internet Explorer  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Toujours envoyer un en-tête Aucun tracking**|Empêche que les informations d'exploration ne soient envoyées à des sites tiers.|  
|**Zone de sécurité intranet**||  
|**Niveau de sécurité de la zone Internet**|Configurez le niveau de sécurité pour la zone Internet.|  
|**Niveau de sécurité de la zone intranet**|Configurez le niveau de sécurité pour la zone intranet.|  
|**Niveau de sécurité de la zone Sites de confiance**|Configurez le niveau de sécurité pour la zone Sites de confiance.|  
|**Niveau de sécurité de la zone des sites sensibles**|Configurez le niveau de sécurité pour la zone des sites sensibles.|  
|**Espaces de noms pour la zone intranet**||  
|**Accéder à un site intranet pour une entrée à mot unique**|Active ou désactive le paramètre qui permet à Internet Explorer d'accéder automatiquement à un site Intranet si un nom de site valide est entré sans être précédé de HTTP :|  
|**Option de menu du mode entreprise**|Autorisez les utilisateurs à activer et désactiver le mode Entreprise à partir du menu **Outils** d’Internet Explorer.|  
|**Emplacement du rapport de journalisation (URL)**|Spécifiez une URL où les sites web visités sont enregistrés quand le Mode entreprise est actif.|  
|**Emplacement de la liste des sites en Mode entreprise (URL)**|Spécifiez l'emplacement de la liste des sites web qui utilisent le Mode entreprise quand il est actif.|  
  
### <a name="cloud"></a>Cloud  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Synchronisation des paramètres**|Permet la synchronisation des paramètres entre les appareils.|  
|**Synchronisation des informations d'identification**|Permet la synchronisation des informations d'identification entre les appareils.|  
|**Compte Microsoft**|Autorisez l'utilisation d'un compte Microsoft sur l'appareil.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Synchronisation des paramètres via des connexions limitées**|Autorisez la synchronisation des paramètres quand la connexion Internet est mesurée.|  
  
### <a name="security"></a>Sécurité  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Installation du fichier non signé**|Autorise le chargement des fichiers non signés.|  
|**Applications non signées**|Autorise le chargement des applications non signées.|  
|**Messagerie SMS et MMS**|Autorisez les messages SMS et MMS à partir de l'appareil.|  
|**Stockage amovible**|Autorisez l'utilisation du stockage amovible, comme une carte SD sur l'appareil.|  
|**Appareil photo**|Autorisez l'utilisation de l'appareil photo.|  
|**Communication en champ proche (NFC)**|Autorisez la communication à l'aide de NFC sur l'appareil.<br /><br /> (Windows Phone 8.1 uniquement)|  
|**Autoriser la connexion USB**|Autorisez les périphériques à se connecter à cet appareil via USB.|
  
### <a name="peak-synchronization"></a>Synchronisation de pointe  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Spécifier les heures de pointe**|Spécifiez une fenêtre de temps qui sera utilisé par les deux paramètres suivants.|  
|**Fréquence de synchronisation pendant les heures de pointe**|Choisissez la fréquence de synchronisation de l’appareil pendant la période de pointe spécifiée.|  
|**Fréquence de synchronisation pendant les heures creuses**|Choisissez la fréquence de synchronisation de l’appareil en dehors de la période de pointe spécifiée.|  
  
### <a name="roaming"></a>Itinérant  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Gestion des appareils en itinérance**|Permet à l’appareil d’être géré par Configuration Manager en phase d’itinérance.|  
|**Téléchargement de logiciel en itinérance**|Permet de télécharger des applications et des logiciels lors de l'itinérance.|  
|**Téléchargement d'e-mails en itinérance**|Autorise les téléchargements de courrier électronique lors de l'itinérance.|  
|**Itinérance des données**|Autorisez l'itinérance entre réseaux lors de l'accès aux données.|  
  
### <a name="encryption"></a>Chiffrement  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Chiffrement de la carte de stockage**|Exigez le chiffrement des cartes de stockage utilisées avec l'appareil.|  
|**Chiffrement des fichiers sur l’appareil**|Requiert que les fichiers de l'appareil mobile soient chiffrés.|  
|**Demander la signature des courriers électroniques**|Requiert la signature des messages électroniques avant leur envoi.|  
|**Algorithme de signature**|Sélectionnez l’algorithme à utiliser pour signer les messages électroniques.|  
|**Demander le chiffrement des courriers électroniques**|Exigez le chiffrement des messages électroniques avant leur envoi.|  
|**Algorithme de chiffrement**|Sélectionnez l’algorithme à utiliser pour chiffrer les messages électroniques.|  
  
###  <a name="wireless-communications"></a>Communications sans fil  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Connexion réseau sans fil**|Activez ou désactivez la fonctionnalité Wi-Fi des appareils.|  
|**Connexion Wi-Fi**|Les utilisateurs peuvent utiliser leur appareil en tant que point d'accès sans fil mobile.|  
|**Décharger les données en Wi-Fi si possible**||  
|**Rapports de point d'accès Wi-Fi**||  
  
##### <a name="to-configure-a-wireless-network-connection"></a>Pour configurer une connexion réseau sans fil  
  
1.  Dans la page **Configurer les paramètres de communication sans fil de l'appareil mobile** , cliquez sur **Ajouter**.  
  
2.  Dans la boîte de dialogue **Connexion réseau sans fil** , spécifiez les informations suivantes sur la connexion sans fil qui sera configurée sur les appareils mobiles :  
  
|Paramètre|Informations complémentaires|  
|-------------|----------------------|  
|**Nom réseau (SSID)**||  
|**Connexion réseau**|Choisissez entre **Internet** et **Travail**.|  
|**Authentification**|Sélectionnez la méthode d'authentification de la connexion sans fil :<br><br> - **Ouvrir**<br> - **Partagé**<br> - **WPA**<br> - **WPA-PSK**<br> - **WPA2**<br> - **WPA2-PSK**|  
|**Chiffrement des données**|Choisissez la méthode de chiffrement utilisée par cette connexion. Les valeurs possibles varient en fonction de la méthode d' **Authentification** sélectionnée :<br><br> - **Désactivé**<br> - **WEP**<br> - **TKIP**<br> - **AES**|  
|**Index de clé**|Sélectionnez un index de clé entre **1** et **4** , qui sera utilisé avec un paramètre **Chiffrement des données** de **WEP**.|  
|**Ce réseau se connecte à Internet**|Sélectionnez cette option si vous souhaitez fournir des paramètres de proxy qui permettent aux appareils mobiles d'établir une connexion sans fil à Internet.|  
|**Paramètres du serveur proxy**|Spécifiez si nécessaire les paramètres **Serveur** et **Port** pour **HTTP**, **WAP** et **Sockets**.|  
|**Activer l'accès réseau 802.1X**|Sélectionnez cette option si vous souhaitez sécuriser la connexion en spécifiant un type EAP.|  
|**Type EAP**|Choisissez le type EAP à utiliser :<br><br> - **PEAP**<br> - **Carte à puce ou certificat**|  
    
  
###  <a name="certificates"></a>Certificats  
 Importez les certificats à installer sur les appareils mobiles.  
  
 Cliquez sur **Importer**, puis spécifiez les valeurs suivantes :  
  
-   **Fichier de certificat** : cliquez sur **Parcourir** , puis sélectionnez le fichier de certificat avec l'extension **.cer** que vous souhaitez importer.  
  
-   **Banque d'informations de destination** : choisissez une ou plusieurs banques de destination où le certificat importé sera ajouté sur l'appareil mobile :  
  
    -   **Racine**  
  
    -   **Autorité de certification**  
  
    -   **Normal**  
  
    -   **Privilégié**  
  
    -   **SPC**  
  
    -   **Homologue**  
  
-   **Rôle** : si **SPC** (Software Publisher Certificate) est sélectionné en tant que banque de destination, choisissez le rôle qui sera associé au certificat :  
  
    -   **Opérateur mobile**  
  
    -   **Gestionnaire**  
  
    -   **Utilisateur authentifié**  
  
    -   **Administrateur informatique**  
  
    -   **Utilisateur non authentifié**  
  
    -   **Serveur d’approvisionnement approuvé**  
  
### <a name="system-security"></a>Sécurité système  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Contrôle de compte d'utilisateur**|Active ou désactive le contrôle de compte d'utilisateur Windows sur l'appareil.|  
|**Pare-feu réseau**|Active ou désactive le pare-feu Windows.|  
|**Mises à jour**|Choisissez le mode de téléchargement des mises à jour logicielles Windows sur les ordinateurs. Par exemple, vous pouvez télécharger automatiquement les mises à jour, mais permettre à l'utilisateur de choisir à quel moment les installer.|  
|**Classification minimale des mises à jour**|Choisissez la classification minimale des mises à jour téléchargées sur les ordinateurs Windows : **Aucune**, **Importante**ou **Recommandée**.|  
|**SmartScreen**|Activez ou désactivez Windows SmartScreen.|  
|**Protection antivirus**|Assurez-vous que l’appareil est protégé par un logiciel antivirus.|  
|**Les signatures de la protection antivirus sont à jour**|Assurez-vous que les signatures antivirus sont à jour.|
|**Autoriser la désinscription manuelle**|Autorisez l’utilisateur à supprimer son appareil de la Gestion des appareils mobiles.|  
  
### <a name="windows-server-work-folders"></a>Dossiers de travail du serveur Windows  
 Ces paramètres s’appliquent à la fois à Windows Phone 8 et Windows Phone 8.1.  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**URL des dossiers de travail**|Configure l'emplacement d'un dossier de travail Windows Server auquel les utilisateurs peuvent se connecter à partir de leur appareil.|  
  
### <a name="allowed-and-blocked-apps-list-windows-phone-81-only"></a>Liste des applications autorisées et bloquées (Windows Phone 8.1 uniquement)  
 Elle vous permet de spécifier la liste des applications Windows Phone conformes ou non conformes dans votre entreprise. Les applications que vous spécifiez comme bloquées ne peuvent pas être installées par les utilisateurs. Si vous spécifiez une liste d'applications autorisées, les utilisateurs peuvent installer uniquement les applications de la liste.  
  
 Vous ne pouvez pas spécifier à la fois des applications autorisées et bloquées dans le même élément de configuration.  
  
> [!IMPORTANT]  
>  Si vous spécifiez une liste d’applications autorisées, vous devez vous assurer que l’application du portail d’entreprise et toutes les applications déployées sur les appareils Windows Phone 8.1 figurent dans la liste **Applications autorisées** .  
  
##### <a name="to-specify-an-allowed-or-blocked-apps-list"></a>Pour spécifier une liste des applications autorisées ou bloquées  
  
1.  Dans la page **Liste des applications autorisées et bloquées (Windows Phone 8.1)** spécifiez les informations suivantes :  
  
|||  
|-|-|  
|Paramètre|Informations complémentaires|  
|**Liste des applications bloquées**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications que les utilisateurs sont autorisés à installer.|  
|**Liste des applications autorisées**|Sélectionnez cette option si vous souhaitez spécifier une liste d'applications que les utilisateurs sont autorisés à installer.|  
|**Ajouter**|Ajoute une application à la liste sélectionnée. Spécifiez le nom de votre choix, éventuellement l’éditeur de l’application, ainsi que l’URL de l’application dans la boutique d’applications.<br /><br /> Pour spécifier l’URL, dans la page Windows Phone Store, recherchez l’application que vous voulez utiliser.<br /><br /> **Exemple :** Recherchez dans le store le **Skype** application. L’URL que vous utilisez est http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> Pour l'application du portail d'entreprise, ou des applications métiers, il est inutile de spécifier une URL complète, le GUID de l'application suffit.|  
|**Éditer**|Vous permet de modifier le nom, l'éditeur et l'URL de l'application sélectionnée.|  
|**Supprimer**|Supprime l'application sélectionnée dans la liste.|  
|**Importerer**|Importe une liste d'applications que vous avez spécifiée dans un fichier de valeurs séparées par des virgules. Utilisez le format Nom de l'application, Éditeur, URL de l'application dans le fichier.|  
  
## <a name="see-also"></a>Voir aussi  
 [Éléments de configuration pour les appareils gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
