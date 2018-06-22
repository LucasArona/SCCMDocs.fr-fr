---
title: Sécurité et confidentialité des clients
titleSuffix: Configuration Manager
description: En savoir plus sur la sécurité et la confidentialité pour les clients dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 89b7664067747c9afb04c3a5dd059e81cfb2716e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341234"
---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article contient des informations de sécurité et de confidentialité pour les clients de System Center Configuration Manager et pour les appareils mobiles qui sont gérés par le connecteur Exchange Server :  

##  <a name="BKMK_Security_Cliients"></a> Bonnes pratiques de sécurité pour les clients  
 Quand Configuration Manager accepte les données provenant d'appareils qui exécutent le client Configuration Manager, il existe un risque que les clients attaquent le site. Par exemple, ils pourraient envoyer un inventaire incorrect ou tenter de surcharger les systèmes de site. Déployez le client Configuration Manager uniquement sur les appareils auxquels vous faites confiance. En outre, utilisez les meilleures pratiques de sécurité suivantes pour contribuer à protéger le site des appareils non autorisés ou compromis :  

 **Utilisez des certificats d’infrastructure à clé publique (PKI) pour les communications client avec les systèmes de site exécutant IIS.**  

-   Comme propriété de site, configurez **Paramètres du système de site** pour **HTTPS uniquement**.  

-   Installer des clients avec la propriété CCMSetup **/UsePKICert**  

-   Utilisez une liste de révocation de certificats (CRL) et assurez-vous que les clients et les serveurs qui communiquent peuvent toujours y accéder.  

 Ces certificats sont requis pour les clients des appareils mobiles et pour les connexions d'ordinateurs clients sur Internet et, à l'exception des points de distribution, ils sont recommandés pour toutes les connexions client sur l'Intranet.  

 Pour plus d’informations sur les spécifications requises des certificats PKI et comment ils sont utilisés pour protéger Configuration Manager, voir [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Approuver automatiquement les ordinateurs clients à partir de domaines approuvés et vérifier et approuver manuellement d'autres ordinateurs**  

 Vous pouvez configurer l'approbation pour la hiérarchie comme manuelle, automatique pour les ordinateurs de domaines approuvés ou automatique pour tous les ordinateurs. La méthode d'approbation la plus sûre consiste à approuver automatiquement les clients qui sont membres de domaines approuvés, puis à vérifier et approuver manuellement tous les autres ordinateurs. Il n'est pas recommandé d'approuver automatiquement tous les clients, sauf si vous disposez d'autres contrôles d'accès pour empêcher l'accès des ordinateurs non approuvés à votre réseau.  

 L'approbation identifie un ordinateur dont vous approuvez la gestion par Configuration Manager lorsque vous ne pouvez pas utiliser l'authentification PKI.  

 Pour plus d’informations sur l’approbation manuelle des ordinateurs, voir [Gérer les clients à partir du nœud Appareils](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 **Ne vous fiez pas au blocage pour empêcher certains clients d'accéder à la hiérarchie Configuration Manager**  

 L'infrastructure Configuration Manager rejette les clients bloqués afin qu’ils ne puissent pas communiquer avec les systèmes de site pour télécharger la stratégie, charger les données d'inventaire ou envoyer des messages d'état. Toutefois, ne vous fiez pas au blocage pour protéger la hiérarchie Configuration Manager des ordinateurs non approuvés lorsque des systèmes de site acceptent les connexions client HTTP. Dans ce scénario, un client bloqué peut se reconnecter au site avec un nouveau certificat auto-signé et un nouvel ID de matériel. Ce blocage vise à bloquer le support de démarrage perdu ou compromis pendant le déploiement d'un système d'exploitation sur des clients et quand tous les systèmes de site acceptent des connexions client HTTPS. Si vous utilisez une infrastructure à clés publiques (PKI) et si elle prend en charge une liste de révocation de certificats, envisagez toujours de définir la révocation de certificats comme première ligne de défense contre les certificats potentiellement compromis. Le blocage des clients dans Configuration Manager fournit une seconde ligne de défense pour protéger votre hiérarchie.  

 Pour plus d’informations, voir [Déterminer si des clients doivent être bloqués dans System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

 **Utilisez les méthodes d'installation de client plus sécurisées qui sont pratiques pour votre environnement :**  

-   Pour les ordinateurs du domaine, les méthodes d'installation du client de la stratégie de groupe et les méthodes d'installation du client basé sur des mises à jour sont plus sûres que l'installation poussée du client.  

-   L'acquisition d'images et l'installation manuelle peuvent être très sûres si vous appliquez des contrôles d'accès et modifiez des contrôles.  

 Parmi toutes les méthodes d'installation des clients, l'installation poussée du client est la moins sûre en raison des nombreuses dépendances qu'elle possède, notamment les autorisations d'administrateur local, le partage Admin$ et de nombreuses exceptions de pare-feu. Ces dépendances augmentent votre surface d'attaque.  

 Pour plus d’informations sur les différentes méthodes d’installation de clients, voir [Méthodes d’installation du client dans System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md).  

 De plus, dans la mesure du possible, sélectionnez une méthode d'installation du client qui nécessite le moins d'autorisations de sécurité dans Configuration Manager et limitez les utilisateurs administratifs auxquels sont affectés des rôles de sécurité qui incluent des autorisations pouvant être utilisées à d'autres fins que le déploiement du client. Par exemple, la mise à niveau automatique du client nécessite le rôle de sécurité **Administrateur complet** , qui accorde à un utilisateur administratif toutes les autorisations de sécurité.  

 Pour plus d’informations sur les dépendances et les autorisations de sécurité requises pour chaque méthode d’installation du client, voir « Dépendances liées aux méthodes d'installation » dans [Configuration requise pour les clients d'ordinateurs](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

 **Si vous devez utiliser l'installation Push du client, prenez des mesures supplémentaires pour sécuriser le compte d'installation Push du client**  

 Bien que ce compte doive être membre du groupe **Administrateurs** local sur chaque ordinateur qui installera le logiciel client Configuration Manager, n'ajoutez jamais le compte d'installation Push du client au groupe **Administrateurs de domaine**. Créez plutôt un groupe global, puis ajoutez ce groupe global au groupe **Administrateurs** local sur vos ordinateurs clients. Vous pouvez également créer un objet de stratégie de groupe pour ajouter un paramètre de groupe restreint afin d'ajouter le compte d'installation poussée du client au groupe **Administrateurs** local.  

 Pour renforcer la sécurité, créez plusieurs comptes d’installation poussée du client, disposant chacun d’un accès administratif à un nombre limité d’ordinateurs, de sorte que si un compte est compromis, seuls les ordinateurs clients auxquels ce compte a accès sont compromis.  

 **Supprimez les certificats avant l'acquisition d'images de l'ordinateur client**  

 Si vous prévoyez de déployer des clients en utilisant la technologie d'acquisition d'images, supprimez toujours les certificats tels que les certificats PKI qui incluent l'authentification du client et les certificats auto-signés avant de capturer l'image. Si vous ne supprimez pas ces certificats, les clients pourront emprunter l'identité l'un de l'autre et vous ne serez pas en mesure de vérifier les données pour chaque client.  

 Pour plus d'informations sur l'utilisation de Sysprep pour préparer un ordinateur à l'acquisition d'images, voir la documentation de votre déploiement Windows.  

 **Assurez-vous que les clients d'ordinateur Configuration Manager obtiennent une copie autorisée de ces certificats :**  

-   La clé racine approuvée de Configuration Manager  

     Si vous n'avez pas développé le schéma Active Directory pour Configuration Manager et si les clients n'utilisent pas de certificats PKI lorsqu'ils communiquent avec des points de gestion, les clients font appel à la clé racine approuvée de Configuration Manager pour authentifier les points de gestion valides. Dans ce scénario, les clients n'ont aucun moyen de vérifier que le point de gestion est un point de gestion approuvé pour la hiérarchie, sauf s'ils utilisent la clé racine approuvée. Sans la clé racine approuvée, un attaquant doué pourrait diriger les clients vers un point de gestion non autorisé.  

     Lorsque les clients ne peuvent pas télécharger la clé racine approuvée de Configuration Manager à partir du catalogue global ou en utilisant des certificats PKI, mettez en service anticipé les clients qui possèdent la clé racine approuvée pour être sûr qu'ils ne peuvent pas être dirigés vers un point de gestion non autorisé. Pour plus d’informations, voir [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

-   Le certificat de signature du serveur de site  

     Les clients utilisent le certificat de signature du serveur de site pour vérifier que le serveur de site a signé la stratégie de clients qu'ils téléchargent à partir d'un point de gestion. Ce certificat est auto-signé par le serveur de site et publié dans les services de domaine Active Directory.  

     Lorsque les clients ne peuvent pas télécharger le certificat de signature de serveur de site à partir du catalogue global, par défaut ils le téléchargent à partir du point de gestion. Lorsque le point de gestion est exposé à un réseau non approuvé (par exemple, Internet), installez manuellement le certificat de signature de serveur de site sur les clients pour vous assurer qu'ils ne peuvent pas exécuter de stratégies de clients qui ont été falsifiées à partir d'un point de gestion compromis.  

     Pour installer manuellement le certificat de signature de serveur de site, utilisez la propriété client.msi CCMSetup **SMSSIGNCERT**. Pour plus d’informations, voir [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 **Ne pas utiliser l'attribution automatique de site si le client envisage de télécharger la clé racine approuvée à partir du premier point de gestion qu'il contacte**  

 Cette pratique recommandée en termes de sécurité est liée à l'entrée précédente. Pour éviter le risque qu'un nouveau client télécharge la clé racine approuvée à partir d'un point de gestion factice, utilisez l'attribution automatique de site dans les scénarios suivants uniquement :  

-   Le client peut accéder aux informations de site Configuration Manager publiées dans les services de domaine Active Directory.  

-   Vous préconfigurez un client avec la clé racine approuvée.  

-   Vous utilisez des certificats PKI depuis une autorité de certification d'entreprise pour établir l'approbation entre le client et le point de gestion.  

 Pour plus d'informations sur la clé racine approuvée, voir [Planification de la clé racine approuvée](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 **Installer des ordinateurs clients avec l'option Client.msi CCMSetup SMSDIRECTORYLOOKUP=NoWINS**  

 La méthode d'emplacement des services la plus sûre pour les clients afin de trouver des sites et des points de gestion consiste à utiliser des services de domaine Active Directory. Si cela n'est pas possible, par exemple, parce que vous ne pouvez pas développer le schéma Active Directory pour Configuration Manager ou parce que les clients se trouvent dans une forêt ou un groupe de travail non approuvé, vous pouvez utiliser la publication DNS comme autre méthode d'emplacement des services. Si ces deux méthodes échouent, les clients peuvent recourir à l'utilisation de WINS lorsque le point de gestion n'est pas configuré pour les connexions client HTTPS.  

 Dans la mesure où la publication vers WINS est moins sûre que les autres méthodes de publication, configurez les ordinateurs clients de sorte qu'ils ne recourent pas à l'utilisation de WINS en spécifiant SMSDIRECTORYLOOKUP=NoWINS. Si vous devez utiliser WINS pour l'emplacement des services, utilisez SMSDIRECTORYLOOKUP=WINSSECURE (paramètre par défaut), qui utilise la clé racine approuvée de Configuration Manager pour valider le certificat auto-signé du point de gestion.  

> [!NOTE]  
>  Lorsque le client est configuré pour SMSDIRECTORYLOOKUP=WINSSECURE et trouve un point de gestion à partir de WINS, le client vérifie sa copie de la clé racine approuvée de Configuration Manager qui se trouve dans WMI. Si la signature du certificat du point de gestion correspond à la copie du client de la clé racine approuvée, le certificat est validé et le client communique avec le point de gestion trouvé à l'aide de WINS. Si la signature du certificat du point de gestion ne correspond pas à la copie du client de la clé racine approuvée, le certificat n'est pas validé et le client ne communique pas avec le point de gestion trouvé à l'aide de WINS.  

 **Assurez-vous que les fenêtres de maintenance sont assez grandes pour déployer des mises à jour logicielles critiques**  

 Vous pouvez configurer des fenêtres de maintenance pour les regroupements d'appareils afin de limiter les périodes où Configuration Manager peut installer des logiciels sur ces appareils. Si vous configurez une fenêtre de maintenance trop petite, le client peut ne pas installer les mises à jour logicielles critiques et se retrouver vulnérable à l'attaque qui aurait été contrée par la mise à jour logicielle.  

 **Dans le cas d'appareils Windows Embedded avec des filtres d'écriture, prendre des précautions de sécurité supplémentaires pour réduire la surface d'attaque si Configuration Manager désactive les filtres d'écriture dans le but de conserver les installations logicielles et les modifications**  

 Lorsque des filtres d'écriture sont activés sur des appareils Windows Embedded, les installations logicielles ou les modifications sont apportées dans le segment de recouvrement uniquement et ne sont pas conservées après le redémarrage de l'appareil. Si vous utilisez Configuration Manager pour désactiver temporairement les filtres d'écriture dans le but de conserver les installations logicielles et les modifications, pendant cette période, l'appareil intégré est vulnérable aux modifications apportées à tous les volumes, y compris les dossiers partagés.  

 Bien que Configuration Manager verrouille l'ordinateur pendant cette période afin que seuls les administrateurs locaux puissent se connecter, prenez des précautions de sécurité supplémentaires pour aider à protéger l'ordinateur lorsque cela est possible. Par exemple, activez des restrictions supplémentaires sur le pare-feu et déconnectez l'appareil du réseau.  

 Si vous utilisez des fenêtres de maintenance pour conserver les modifications, planifiez soigneusement la durée de ces fenêtres pour réduire le temps de désactivation des filtres d'écriture mais permettre les installations logicielles et les redémarrages.  

 **Si vous utilisez l'installation de client basée sur des mises à jour logicielles et installez une version ultérieure du client sur le site, exécutez la mise à jour logicielle publiée sur le point de mise à jour logicielle afin que le client reçoive la version la plus récente**  

 Si vous installez une version ultérieure du client sur le site, par exemple, vous mettez le site à niveau, la mise à jour logicielle pour le déploiement de client qui est publiée sur le point de mise à jour logicielle n'est pas exécutée automatiquement. Vous devez republier le client Configuration Manager sur le point de mise à jour logicielle et cliquer sur **Oui** pour mettre à jour le numéro de version.  

 Pour plus d’informations, voir la procédure « Pour publier le client Configuration Manager dans le point de mise à jour logicielle » dans [Comment installer des clients Configuration Manager à l'aide d'une installation basée sur les mises à jour logicielles](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

 **Configurez le paramètre de l’appareil client de l’Agent ordinateur Interrompre l’entrée du code confidentiel BitLocker au redémarrage sur Toujours uniquement pour les ordinateurs auxquels vous faites confiance et qui ont un accès physique limité**  

 Lorsque vous définissez ce paramètre client sur **Toujours**, Configuration Manager peut terminer l'installation du logiciel afin de s'assurer que les mises à jour logicielles critiques sont installées et que les services ont repris. Toutefois, si un attaquant intercepte le processus de redémarrage, il peut prendre le contrôle de l'ordinateur. Utilisez ce paramètre uniquement lorsque vous faites confiance à l'ordinateur et lorsque l'accès physique à l'ordinateur est limité. Par exemple, ce paramètre peut convenir aux serveurs d'un centre de données.  

 **Ne configurez pas le paramètre de l’appareil client de l’Agent ordinateur Stratégie d’exécution de PowerShell sur Ignorer.**  

 Ce paramètre client permet au client Configuration Manager d'exécuter des scripts PowerShell non signés, ce qui peut autoriser l'exécution de programmes malveillants sur des ordinateurs clients. Si vous devez sélectionner cette option, utilisez un paramètre client personnalisé et affectez-le uniquement aux ordinateurs clients qui doivent exécuter des scripts PowerShell non signés.  

##  <a name="bkmk_mobile"></a> Bonnes pratiques de sécurité pour les appareils mobiles  
 **Pour les appareils mobiles que vous inscrivez à Configuration Manager et qui seront pris en charge sur Internet : Installer le point proxy d'inscription dans un réseau de périmètre et le point d'inscription dans l'Intranet**  

 Cette séparation des rôles permet de protéger le point d'inscription contre une attaque. Si le point d'inscription est compromis, un attaquant peut obtenir des certificats pour authentification et voler les informations d'identification des utilisateurs qui inscrivent leurs appareils mobiles.  

 **Pour les appareils mobiles : Configurez les paramètres de mot de passe pour protéger les appareils mobiles contre les accès non autorisés**  

 Pour les appareils mobiles qui sont inscrits par Configuration Manager: Utilisez un élément de configuration d'appareil mobile pour configurer la complexité du mot de passe comme étant le code confidentiel et au moins la longueur par défaut pour la longueur minimale du mot de passe.  

 Pour les appareils mobiles sur lesquels le client Configuration Manager n'est pas installé mais qui sont gérés par le connecteur Exchange Server  : Configurez les **Paramètres de mot de passe** pour le connecteur Exchange Server, de sorte que la complexité du mot de passe soit le code confidentiel et spécifier au moins la longueur par défaut pour la longueur minimale du mot de passe.  

 **Pour les appareils mobiles : Empêchez la falsification des informations d'inventaire et des informations d'état en autorisant l'exécution des applications uniquement lorsqu'elles sont signées par des entreprises approuvées et ne pas autoriser l'installation de fichiers non signés**  

 Pour d'autres appareils mobiles qui sont inscrits par Configuration Manager : Utilisez un élément de configuration d'appareil mobile pour configurer le paramètre de sécurité **Applications non signée**s comme **Interdites** et configurez les **Installations de fichiers non signés** comme une source approuvée.  

 Pour les appareils mobiles sur lesquels le client Configuration Manager n'est pas installé mais qui sont gérés par le connecteur Exchange Server : Configurez les **Paramètres d'application** pour le connecteur Exchange Server, de sorte que l'**Installation de fichiers non signés** et les **Applications non signées** soient configurées comme **Interdites**.  

 **Pour les appareils mobiles : Empêchez l'élévation des attaques de privilège en verrouillant l'appareil mobile lorsqu'il n'est pas autorisé**  

 Pour d'autres appareils mobiles qui sont inscrits par Configuration Manager : Utiliser un élément de configuration d'appareil mobile pour configurer le paramètre de mot de passe **Durée d'inactivité en minutes avant le verrouillage du périphérique mobile**.  

 Pour les appareils mobiles sur lesquels le client Gestionnaire de configuration n'est pas installé mais qui sont gérés par le connecteur Exchange Server : Configurez les **Paramètres de mot de passe** pour le connecteur Exchange Server afin de configurer la **Durée d'inactivité en minutes avant le verrouillage du périphérique mobile** .  

 **Pour les appareils mobiles : Empêchez l'élévation de privilèges en limitant les utilisateurs qui peuvent inscrire leurs appareils mobiles**  

 Utilisez un paramètre client personnalisé plutôt que les paramètres clients par défaut, pour que seuls les utilisateurs autorisés puissent inscrire leurs appareils mobiles.  

 **Pour les appareils mobiles : Ne déployez pas d’applications pour les utilisateurs qui possèdent des appareils mobiles inscrits par Configuration Manager ou Microsoft Intune dans les cas suivants :**  

-   Lorsque l'appareil mobile est utilisé par plusieurs personnes.  

-   Lorsque l'appareil est inscrit par un administrateur pour le compte d'un utilisateur.  

-   Lorsque l'appareil est transféré à une autre personne sans retirer puis réinscrire l'appareil.  

 Une relation d'affinité entre appareil et utilisateur est créée lors de l'inscription, qui mappe l'utilisateur effectuant l'inscription à l'appareil mobile. Si un autre utilisateur utilise l'appareil mobile, il pourra exécuter les applications que vous déployez sur l'utilisateur d'origine, ce qui peut entraîner une élévation de privilèges. De même, si un autre administrateur inscrit l'appareil mobile pour un utilisateur, les applications déployées sur l'utilisateur ne sont pas installées sur l'appareil mobile, mais les applications déployées sur l'administrateur peuvent être installées.  

 Contrairement à l'affinité entre appareil et utilisateur pour les ordinateurs Windows, vous ne pouvez pas définir manuellement les informations d'affinité entre appareil et utilisateur pour les appareils mobiles qui sont inscrits par Microsoft Intune.  

 Si vous transférez la propriété d'un appareil mobile inscrit par Intune, retirez l'appareil mobile de Intune pour supprimer l'affinité entre appareil et utilisateur, puis demandez à l'utilisateur actuel de réinscrire l'appareil.  

 **Pour les appareils mobiles : Assurez-vous que les utilisateurs inscrivent leurs appareils mobiles pour Microsoft Intune**  

 Dans la mesure où une relation d'affinité entre appareil et utilisateur est créée lors de l'inscription qui mappe l'utilisateur effectuant l'inscription sur l'appareil mobile, si un administrateur inscrit l'appareil mobile pour un utilisateur, les applications déployées sur l'utilisateur ne sont pas installées sur l'appareil mobile, mais les applications déployées sur l'administrateur peuvent être installées.  

 **Pour le connecteur Exchange Server : Assurez-vous que la connexion entre le serveur de site Configuration Manager et l'ordinateur Exchange Server est protégée**  

 Utiliser IPsec si le serveur Exchange Server est sur le site ; Exchange hébergé sécurise automatiquement la connexion par SSL.  

 **Pour le connecteur Exchange Server : Utilisez le principe des privilèges minimum pour le connecteur**  

 Pour obtenir la liste des applets de commande dont le connecteur Exchange Server a besoin au minimum, voir [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

##  <a name="bkmk_macs"></a> Bonnes pratiques de sécurité pour les ordinateurs Mac  
 **Pour les ordinateurs Mac : Stockez et accédez aux fichiers sources du client à partir d'un emplacement sécurisé.**  

 Configuration Manager ne vérifie pas si ces fichiers source du client ont été falsifiés avant d'installer ou d'inscrire le client sur un ordinateur Mac. Téléchargez ces fichiers à partir d'une source digne de confiance, enregistrez-les et accédez-y en toute sécurité.  

 **Pour les ordinateurs Mac : Indépendamment de Configuration Manager, surveillez et effectuez le suivi de la période de validité du certificat d'inscription des utilisateurs.**  

 Pour garantir la pérennité des activités, surveillez et effectuez le suivi de la période de validité des certificats que vous utilisez pour les ordinateurs Mac. Configuration Manager ne prend pas en charge le renouvellement automatique de ce certificat et ne vous avertit pas que le certificat est sur le point d'expirer. La période de validité type est de 1 an.  

 Pour plus d’informations sur le renouvellement du certificat, voir [Renouvellement manuel du certificat client Mac](../../../../core/clients/deploy/deploy-clients-to-macs.md#renewing-the-mac-client-certificate).  

 **Pour les ordinateurs Mac : Envisagez de configurer le certificat d’Autorité de certification racine approuvé de manière à ce qu’il soit approuvé pour le protocole SSL uniquement afin d’empêcher une élévation des privilèges.**  

 Lorsque vous inscrivez des ordinateurs Mac, un certificat utilisateur destiné à gérer le client Configuration Manager est automatiquement installé, ainsi que le certificat racine approuvé auquel est lié le certificat utilisateur. Si vous voulez limiter l'approbation de ce certificat racine au protocole SSL uniquement, vous pouvez procéder comme suit.  

 Une fois cette procédure exécutée, le certificat racine n'est pas approuvé pour valider les protocoles autres que SSL : par exemple, Courrier sécurisé (S/MIME), Protocole EAP (Extensible Authentication), ou la signature de code.  

> [!NOTE]  
>  Vous pouvez également utiliser cette procédure si vous avez installé le certificat client indépendamment de Configuration Manager.  

 Pour limiter le certificat d'autorité de certification racine pour le protocole SSL uniquement :  

1.  Sur l'ordinateur Mac, ouvrez une fenêtre de terminal.  

2.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  Dans la boîte de dialogue **Trousseau d'accès** , dans la zone **Trousseau** , cliquez sur **Système**, puis dans la zone **Catégorie** , cliquez sur **Certificats**.  

4.  Recherchez et double-cliquez sur le certificat d'autorité de certification racine pour le certificat client Mac.  

5.  Dans la boîte de dialogue du certificat d'autorité de certification racine, développez la zone **Confiance** , puis apportez les modifications suivantes :  

    1.  Pour le paramètre **Lors de l'utilisation de ce certificat** , remplacez le paramètre par défaut **Toujours faire confiance** par **Utiliser les valeurs système par défaut**.  

    2.  Pour le paramètre **Secure Sockets Layer (SSL)** , remplacez le paramètre **aucune valeur spécifiée** par **Toujours faire confiance**.  

6.  Fermez la boîte de dialogue et lorsque vous y êtes invité, entrez le mot de passe de l'administrateur, puis cliquez sur **Mettre à jour les paramètres**.  

##  <a name="BKMK_SecurityIssues_Clients"></a> Problèmes de sécurité pour les clients Configuration Manager  
 Les problèmes de sécurité suivants ne peuvent pas être atténués :  

-   Les messages de statut ne sont pas authentifiés  

     Aucune authentification n'est effectuée sur les messages de statut. Lorsqu'un point de gestion accepte les connexions client HTTP, n'importe quel appareil peut envoyer des messages de statut au point de gestion. Si le point de gestion n'accepte que les connexions client HTTPS, un appareil doit obtenir un certificat d'authentification client valide provenant d'une autorité de certification racine de confiance, mais peut également envoyer des messages de statut par la suite. Si un client envoie un message de statut non valide, il est supprimé.  

     Il existe donc peu d'attaques potentielles contre cette vulnérabilité. Un attaquant pourrait envoyer un message de statut erroné pour adhérer à un regroupement basé sur des requêtes de messages de statut. Un client pourrait déclencher un refus de service contre le point de gestion en l'inondant de messages de statut. Si les messages de statut déclenchent des actions dans les règles de filtrage des messages de statut, un attaquant pourrait déclencher la règle de filtrage des messages de statut. Un attaquant pourrait également envoyer un message de statut qui rendrait les informations de rapport incorrectes.  

-   Des stratégies peuvent être reciblées vers des clients non ciblés  

     Un attaquant pourrait utiliser plusieurs méthodes pour faire en sorte qu'une stratégie ciblée sur un seul client soit appliquée à un client totalement différent. Par exemple, un attaquant au niveau d'un client approuvé pourrait envoyer de fausses informations de découverte ou d'inventaire pour que l'ordinateur soit ajouté à un regroupement auquel il ne devrait pas appartenir, puis recevoir tous les déploiements de celui-ci. Bien que des contrôles existent pour aider à empêcher les attaquants de modifier la stratégie directement, des attaquants pourraient prendre une stratégie existante pour reformater ou redéployer un système d'exploitation et l'envoyer à un autre ordinateur, créant ainsi un refus de service. Ces types d'attaques demanderaient un minutage précis et des connaissances approfondies de l'infrastructure de Configuration Manager.  

-   Les journaux du client permettent l'accès utilisateur  

     Tous les fichiers journaux des clients accordent un accès en lecture aux utilisateurs et un accès en écriture aux utilisateurs interactifs. Si vous activez la journalisation détaillée, des attaquants peuvent lire les fichiers journaux pour y rechercher des informations sur la compatibilité ou les vulnérabilités du système. Les processus tels que l'installation de logiciels, effectués dans un contexte de l'utilisateur, doivent être capables d'écrire vers les journaux avec un compte d'utilisateur doté de droits limités. Cela signifie qu'un attaquant pourrait également écrire vers les journaux avec un compte doté de droits limités.  

     Le risque le plus sérieux est qu'un attaquant puisse supprimer des informations des fichiers journaux, dont un administrateur pourrait avoir besoin pour l'audit et la détection d'intrus.  

-   Un ordinateur peut être utilisé pour obtenir un certificat conçu pour l'inscription d'appareils mobiles  

     Lorsque Configuration Manager traite une demande d'inscription, il ne peut pas vérifier qu'elle émane d'un appareil mobile plutôt que d'un ordinateur. Si la demande provient d'un ordinateur, il peut installer un certificat PKI qui lui permet ensuite de s'inscrire avec Configuration Manager. Pour prévenir une attaque par élévation de privilèges dans ce scénario, n'autorisez que les utilisateurs approuvés à inscrire leurs appareils mobiles et surveillez attentivement les activités d'inscription.  

-   La connexion d'un client au point de gestion n'est pas abandonnée si vous bloquez un client, et celui-ci peut continuer à envoyer des paquets de notification client au point de gestion, par exemple, des messages de conservation d'activité  

     Lorsque vous bloquez un client auquel vous ne faites plus confiance, et qui a établi une communication de notification client, Configuration Manager ne déconnecte pas la session. Le client bloqué peut continuer à envoyer des paquets à son point de gestion jusqu'à ce que le client se déconnecte du réseau. Ces paquets sont seulement des paquets de petite taille, des paquets de conservation d'activité, et ces clients ne peuvent pas être gérés par Configuration Manager jusqu'à ce qu'ils soient débloqués.  

-   Lorsque vous utilisez la mise à niveau automatique des clients et que le client est dirigé vers un point de gestion pour télécharger les fichiers source du client, le point de gestion n'est pas vérifié comme une source fiable  

-   Lorsque les utilisateurs inscrivent des ordinateurs Mac pour la première fois, ils sont exposés à l'usurpation DNS  

     Lorsque l'ordinateur Mac se connecte au point proxy d'inscription lors de l'inscription, il est peu probable que l'ordinateur Mac possède déjà le certificat d'autorité de certification racine. À ce stade, le serveur est non approuvé par l'ordinateur Mac et il invite l'utilisateur à continuer. Si le nom de domaine complet du point proxy d'inscription est résolu par un serveur DNS non autorisé, il peut diriger l'ordinateur Mac vers un point proxy d'inscription non autorisé et installer des certificats à partir d'une source non approuvée. Pour réduire ce risque, suivez les meilleures pratiques afin d'éviter l'usurpation DNS dans votre environnement.  

-   L'inscription d'ordinateurs Mac ne limite pas les demandes de certificat  

     Les utilisateurs peuvent réinscrire leurs ordinateurs Mac, en demandant chaque fois un certificat client. Configuration Manager ne vérifie pas s'il existe plusieurs demandes ni limite le nombre de certificats demandés à partir d'un seul ordinateur. Un utilisateur non autorisé pourrait exécuter un script qui répète la demande d'inscription de ligne de commande, provoquant un déni de service sur le réseau ou sur l'autorité de certification (CA) émettrice. Pour réduire ce risque, surveillez attentivement l'autorité de certification émettrice pour ce type de comportement suspect. Un ordinateur qui présente ce modèle de comportement doit immédiatement être bloqué de la hiérarchie Configuration Manager.  

-   Un accusé de réception de réinitialisation ne vérifie pas que l'appareil a bien été réinitialisé  

     Lorsque vous lancez une action de réinitialisation pour un appareil mobile et Configuration Manager affiche l'état de la réinitialisation pour laquelle un accusé de réception est attendu, la vérification indique que Configuration Manager a bien envoyé le message et non que l'appareil a effectué une action sur celui-ci. En outre, pour les appareils mobiles qui sont gérés par le connecteur Exchange Server, un accusé de réception de réinitialisation vérifie que la commande a été reçue par Exchange, et non par l'appareil.  

-   Si vous utilisez les options de validation des modifications sur des appareils Windows Embedded, les comptes peuvent être verrouillés plus tôt que prévu  

     Si l’appareil Windows Embedded exécute un système d’exploitation antérieur à Windows 7, et qu’un utilisateur tente de se connecter alors que les filtres d’écriture sont désactivés pour valider des modifications apportées par Configuration Manager, le nombre de tentatives de connexion incorrectes permis avant le verrouillage du compte est réduit de moitié. Par exemple, si le **Seuil de verrouillage de compte** est configuré sur 6, et que l'utilisateur entre son mot de passe incorrectement 3 fois, le compte est bloqué, ce qui crée une situation de déni de service.  Si les utilisateurs doivent se connecter aux appareils intégrés dans ce scénario, avertissez-les du risque d'un seuil de verrouillage réduit.  

##  <a name="BKMK_Privacy_Cliients"></a> Informations de confidentialité pour les clients Configuration Manager  
 Lorsque vous déployez le client Configuration Manager, vous activez des paramètres clients afin de pouvoir utiliser les fonctionnalités de gestion de Configuration Manager. Les paramètres que vous utilisez pour configurer les fonctionnalités peuvent s'appliquer à tous les clients de la hiérarchie Configuration Manager, qu'ils soient directement connectés au réseau d'entreprise, connectés via une session distante ou connectés à Internet mais pris en charge par Configuration Manager.  

 Les informations sur le client sont stockées dans la base de données Configuration Manager et ne sont pas envoyées à Microsoft. Les informations sont conservées dans la base de données jusqu'à leur suppression par les tâches de maintenance du site **Supprimer les données de découverte anciennes** , tous les 90 jours. Vous pouvez configurer l'intervalle de suppression.  

 Avant de configurer le client Configuration Manager, réfléchissez à vos besoins en matière de confidentialité.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informations sur la confidentialité des appareils mobiles qui sont inscrits par Configuration Manager  
 Pour des informations sur la confidentialité quand vous inscrivez un appareil mobile par Configuration Manager, voir [Déclaration de confidentialité de System Center Configuration Manager - Addendum relatif aux appareils mobiles](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### <a name="client-status"></a>État du client  
 Configuration Manager surveille l'activité des clients et l'évalue périodiquement, et peut corriger le client Configuration Manager et ses dépendances. L'état du client est activé par défaut et il utilise les mesures côté serveur pour vérifier l'activité du client, ainsi que les actions côté client pour les auto-contrôles, la correction et pour l'envoi d'informations sur l'état du client au site Configuration Manager. Le client exécute les auto-contrôles en fonction d'un calendrier que vous pouvez configurer. Le client envoie les résultats des contrôles au site Configuration Manager. Ces informations sont chiffrées lors du transfert.  

 Les informations sur l’état du client sont stockées dans la base de données Configuration Manager et ne sont pas envoyées à Microsoft. Les informations ne sont pas stockées sous forme chiffrée dans la base de données du site. Ces informations sont conservées dans la base de données jusqu'à ce qu'elles en soient supprimées en fonction de la valeur configurée pour le paramètre de l'état du client **Conserver l'historique de l'état du client pendant le nombre de jours suivant** . La valeur par défaut pour ce paramètre est 31 jours.  

 Avant d'installer le client Configuration Manager avec vérification de l'état du client, pensez à vos besoins en matière de confidentialité.  

##  <a name="BKMK_Privacy_ExchangeConnector"></a> Informations de confidentialité pour les appareils mobiles qui sont gérés à l’aide du connecteur Exchange Server  
 Le connecteur Exchange Server détecte et gère les appareils qui se connectent à Exchange Server (hébergés ou sur site) en utilisant le protocole ActiveSync. Les enregistrements trouvés par le connecteur Exchange Server sont stockés dans la base de données Configuration Manager. Les informations sont collectées à partir d'Exchange Server. Elles ne contiennent pas d'informations supplémentaires par rapport à ce que les appareils mobiles envoient à Exchange Server.  

 Les informations de l'appareil mobile ne sont pas envoyées à Microsoft. Ensuite, les informations de compatibilité sont stockées dans la base de données de Configuration Manager. Les informations sont conservées dans la base de données jusqu'à leur suppression par les tâches de maintenance du site **Supprimer les données de découverte anciennes** , tous les 90 jours. Vous pouvez configurer l'intervalle de suppression.  

 Avant d'installer et de configurer le connecteur Exchange Server, pensez à vos besoins en matière de confidentialité.  
