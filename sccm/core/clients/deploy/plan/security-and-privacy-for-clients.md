---
title: Sécurité et confidentialité des clients
titleSuffix: Configuration Manager
description: Découvrez la sécurité et la confidentialité pour les clients Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3dfb749695ffb7a8ecdeab5e4fbed764023eb6e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385590"
---
# <a name="security-and-privacy-for-configuration-manager-clients"></a>Sécurité et confidentialité pour les clients Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit les informations de sécurité et de confidentialité pour les clients Configuration Manager. Il inclut également des informations concernant les appareils mobiles qui sont gérés par le [connecteur Exchange Server](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="BKMK_Security_Clients"></a> Bonnes pratiques de sécurité pour les clients  

Le site Configuration Manager accepte les données d’appareils qui exécutent le client Configuration Manager. Ce comportement présente le risque que les clients attaquent le site. Par exemple, ils pourraient envoyer un inventaire incorrect ou tenter de surcharger les systèmes de site. Déployez le client Configuration Manager uniquement sur les appareils auxquels vous faites confiance. En outre, utilisez les meilleures pratiques de sécurité suivantes pour contribuer à protéger le site des appareils non autorisés ou compromis :  

#### <a name="use-public-key-infrastructure-pki-certificates-for-client-communications-with-site-systems-that-run-iis"></a>Utiliser des certificats d’infrastructure à clé publique (PKI) pour les communications client avec les systèmes de site exécutant IIS  

-   Comme propriété de site, configurez **Paramètres du système de site** pour **HTTPS uniquement**.  

-   Installez des clients avec la propriété CCMSetup `UsePKICert`.  

-   Utilisez une liste de révocation de certificats (CRL) et assurez-vous que les clients et les serveurs qui communiquent peuvent toujours y accéder.  

Les clients d’appareils mobiles et certains clients Internet exigent ces certificats. Microsoft recommande ces certificats pour toutes les connexions client sur l’intranet.  

Pour plus d’informations sur les exigences de certificat PKI et la façon dont ils sont utilisés pour protéger Configuration Manager, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


#### <a name="automatically-approve-client-computers-from-trusted-domains-and-manually-check-and-approve-other-computers"></a>Approuver automatiquement les ordinateurs clients à partir de domaines approuvés et vérifier et approuver manuellement d'autres ordinateurs  

Quand vous ne pouvez pas utiliser l’authentification PKI, l’approbation identifie un ordinateur dont vous approuvez la gestion par Configuration Manager. La hiérarchie comporte les options suivantes pour configurer l’approbation du client :  
- Manuel
- Automatique pour les ordinateurs de domaines approuvés
- Automatique pour tous les ordinateurs  

La méthode d'approbation la plus sûre consiste à approuver automatiquement les clients qui sont membres de domaines approuvés. Ensuite, vérifiez et approuvez manuellement tous les autres ordinateurs. Il n’est pas recommandé d’approuver automatiquement tous les clients, sauf si vous disposez d’autres contrôles d’accès pour empêcher l’accès des ordinateurs non approuvés à votre réseau.  

Pour plus d’informations sur l’approbation manuelle des ordinateurs, consultez [Gérer les clients à partir du nœud Appareils](/sccm/core/clients/manage/manage-clients#BKMK_ManagingClients_DevicesNode).  


#### <a name="dont-rely-on-blocking-to-prevent-clients-from-accessing-the-configuration-manager-hierarchy"></a>Ne pas se fier au blocage pour empêcher des clients d’accéder à la hiérarchie Configuration Manager  

Les clients bloqués sont rejetés par l’infrastructure Configuration Manager. Si des clients sont bloqués, ils ne peuvent pas communiquer avec les systèmes de site pour télécharger la stratégie, charger des données d’inventaire ou envoyer des messages d’état. 

Le blocage est conçu pour les scénarios suivants : 
- Pour bloquer les médias de démarrage perdus ou non fiables quand vous déployez un système d’exploitation sur des clients
- Quand tous les systèmes de site acceptent les connexions client HTTPS 

Quand des systèmes de site acceptent les connexions client HTTP, ne vous fiez pas au blocage pour protéger la hiérarchie Configuration Manager des ordinateurs non approuvés. Dans ce scénario, un client bloqué peut rejoindre le site avec un nouveau certificat auto-signé et un nouvel ID de matériel. 

La révocation de certificat est la première ligne de défense contre les certificats potentiellement compromis. Une liste de révocation de certificats est disponible uniquement à partir d’une infrastructure à clé publique (PKI) pris en charge. Le blocage des clients dans Configuration Manager fournit une seconde ligne de défense pour protéger votre hiérarchie.  

Pour plus d’informations, consultez [Déterminer si des clients doivent être bloqués](/sccm/core/clients/deploy/plan/determine-whether-to-block-clients).  


#### <a name="use-the-most-secure-client-installation-methods-that-are-practical-for-your-environment"></a>Utiliser les méthodes d’installation de client les plus sécurisées qui sont pratiques pour votre environnement  

-   Pour les ordinateurs du domaine, les méthodes d'installation du client de la stratégie de groupe et les méthodes d'installation du client basé sur des mises à jour sont plus sûres que l'installation poussée du client.  

-   Si vous appliquez des contrôles d’accès et que vous changez des contrôles, utilisez des méthodes d’acquisition d’images et d’installation manuelle.  

-   Dans la version 1806 ou une version ultérieure, utilisez l’authentification mutuelle Kerberos avec l’installation Push du client.  

Parmi toutes les méthodes d’installation des clients, l’installation Push du client est la moins sécurisée en raison des nombreuses dépendances qu’elle possède. Ces dépendances incluent les autorisations d’administrateur local, le partage Admin$ et des exceptions de pare-feu. Le nombre et le type de ces dépendances augmentent votre surface d’attaque.  

À compter de la version 1806, quand vous utilisez l’installation Push du client, le site peut exiger l’authentification mutuelle Kerberos en interdisant le recours à NTLM en secours avant d’établir la connexion. Cette amélioration permet de sécuriser la communication entre le serveur et le client. Pour plus d’informations, consultez [Guide pratique pour installer des clients à l’aide d’une installation Push du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).<!--1358204-->  

Pour plus d’informations sur les différentes méthodes d’installation de clients, consultez [Méthodes d’installation du client](/sccm/core/clients/deploy/plan/client-installation-methods).  

Dans la mesure du possible, sélectionnez une méthode d’installation du client qui nécessite le moins d’autorisations de sécurité dans Configuration Manager. Limitez les utilisateurs administratifs auxquels sont attribués des rôles de sécurité qui incluent des autorisations pouvant être utilisées à d’autres fins que le déploiement du client. Par exemple, la configuration de la mise à niveau automatique du client nécessite le rôle de sécurité **Administrateur complet**, qui accorde à un utilisateur administratif toutes les autorisations de sécurité.  

Pour plus d’informations sur les dépendances et les autorisations de sécurité exigées pour chaque méthode d’installation du client, consultez « Dépendances liées aux méthodes d’installation » dans [Prérequis pour les ordinateurs clients](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#BKMK_prereqs_computers).  


#### <a name="if-you-must-use-client-push-installation-take-additional-steps-to-secure-the-client-push-installation-account"></a>Si vous devez utiliser l'installation poussée du client, prenez des mesures supplémentaires pour sécuriser le compte d'Installation poussée du client  

Ce compte doit être membre du groupe **Administrateurs** local sur chaque ordinateur qui installe le client Configuration Manager. N’ajoutez jamais le compte d’installation Push du client au groupe **Admins du domaine**. Créez plutôt un groupe global, puis ajoutez ce groupe global au groupe **Administrateurs** local sur vos clients. Créez un objet de stratégie de groupe pour ajouter un paramètre de groupe restreint afin d’ajouter le compte d’installation Push du client au groupe **Administrateurs** local.  

Pour renforcer la sécurité, créez plusieurs comptes d’installation Push du client, chacun avec un accès administratif à un nombre limité d’ordinateurs. Si un compte est compromis, seuls les ordinateurs clients auxquels ce compte a accès sont compromis.  


#### <a name="remove-certificates-before-imaging-clients"></a>Supprimer les certificats avant l’acquisition d’images des clients  

Quand vous déployez des clients à l’aide d’images de système d’exploitation, supprimez toujours les certificats avant de capturer l’image. Ces certificats incluent des certificats PKI pour l’authentification du client, ainsi que les certificats auto-signés. Si vous ne supprimez pas ces certificats, les clients peuvent emprunter l’identité des uns et des autres. Vous ne pouvez pas vérifier les données de chaque client.  

Pour plus d'informations, consultez [Créer une séquence de tâches pour capturer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).  


#### <a name="ensure-that-the-configuration-manager-computer-clients-get-an-authorized-copy-of-these-certificates"></a>Vérifier que les clients d’ordinateur Configuration Manager obtiennent une copie autorisée de ces certificats  

-   Le certificat de la clé racine approuvée de Configuration Manager  

    Quand les deux instructions suivantes sont remplies, les clients s’appuient sur la clé racine approuvée de Configuration Manager pour authentifier des points de gestion valides :  

      - Vous n’avez pas étendu le schéma Active Directory pour Configuration Manager
      - Les clients n’utilisent de certificats PKI quand ils communiquent avec des points de gestion  

    Dans ce scénario, les clients n’ont aucun moyen de vérifier que le point de gestion est approuvé pour la hiérarchie, sauf s’ils utilisent la clé racine approuvée. Sans la clé racine approuvée, un attaquant doué pourrait diriger les clients vers un point de gestion non autorisé.  

    Quand les clients ne peuvent pas télécharger la clé racine approuvée de Configuration Manager à partir du catalogue global ou à l’aide de certificats PKI, préprovisionnez les clients avec la clé racine approuvée. Cette action garantit qu’ils ne peuvent pas être dirigés vers un point de gestion non autorisé. Pour plus d’informations, voir [Planification de la clé racine approuvée](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

-   Le certificat de signature du serveur de site  

     Les clients utilisent ce certificat pour vérifier que le serveur de site a signé la stratégie téléchargée à partir d’un point de gestion. Ce certificat est auto-signé par le serveur de site et publié dans les services de domaine Active Directory.  

     Quand les clients ne peuvent pas télécharger le certificat de signature du serveur de site à partir du catalogue global, ils le téléchargent par défaut à partir du point de gestion. Si le point de gestion est exposé à un réseau non approuvé comme Internet, installez manuellement le certificat de signature du serveur de site sur les clients. Cette action garantit qu’ils ne peuvent pas télécharger de stratégies de clients falsifiées à partir d’un point de gestion compromis.  

     Pour installer manuellement le certificat de signature de serveur de site, utilisez la propriété client.msi CCMSetup **SMSSIGNCERT**. Pour plus d’informations, consultez [À propos des propriétés d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="dont-use-automatic-site-assignment-if-the-client-downloads-the-trusted-root-key-from-the-first-management-point-it-contacts"></a>Ne pas utiliser l’attribution de site automatique si le client télécharge la clé racine approuvée à partir du premier point de gestion qu’il contacte  

Pour éviter le risque qu’un nouveau client télécharge la clé racine approuvée à partir d’un point de gestion non autorisé, utilisez l’attribution de site automatique uniquement dans les scénarios suivants :  

-   Le client peut accéder aux informations de site Configuration Manager publiées dans Active Directory Domain Services.  

-   Vous préconfigurez un client avec la clé racine approuvée.  

-   Vous utilisez des certificats PKI depuis une autorité de certification d'entreprise pour établir l'approbation entre le client et le point de gestion.  

Pour plus d’informations sur la clé racine approuvée, consultez [Planification de la clé racine approuvée](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  


#### <a name="install-client-computers-with-the-ccmsetup-clientmsi-option-smsdirectorylookupnowins"></a>Installer des ordinateurs clients avec l'option Client.msi CCMSetup SMSDIRECTORYLOOKUP=NoWINS  

La méthode d'emplacement des services la plus sûre pour les clients afin de trouver des sites et des points de gestion consiste à utiliser des services de domaine Active Directory. Parfois, cette méthode n’est pas possible pour certains environnements. Par exemple, parce que vous ne pouvez pas étendre le schéma Active Directory pour Configuration Manager, ou parce que les clients se trouvent dans une forêt ou un groupe de travail non approuvés. Si cette méthode n’est pas possible, utilisez la publication DNS comme méthode alternative de localisation de service. Si ces deux méthodes échouent, et quand le point de gestion n’est pas configuré pour les connexions client HTTPS, les clients peuvent revenir à l’utilisation de WINS.  

La publication dans WINS est moins sécurisée que les autres méthodes de publication. Configurez les ordinateurs clients pour ne pas revenir à l’utilisation de WINS en spécifiant **SMSDIRECTORYLOOKUP=NoWINS**. Si vous devez utiliser WINS comme emplacement du service, utilisez **SMSDIRECTORYLOOKUP=WINSSECURE**. Ce paramètre est la valeur par défaut. Il utilise la clé racine approuvée de Configuration Manager pour valider le certificat auto-signé du point de gestion.  

> [!NOTE]  
>  Quand vous configurez le client pour **SMSDIRECTORYLOOKUP=WINSSECURE** et qu’il trouve un point de gestion à partir de WINS, le client vérifie sa copie de la clé racine approuvée de Configuration Manager qui se trouve dans WMI.  
> 
> Si la signature sur le certificat du point de gestion correspond à la copie de la clé racine approuvée du client, le certificat est validé. Après la validation du certificat, le client commence à communiquer avec le point de gestion trouvé à l’aide de WINS.  
> 
> Si la signature sur le certificat du point de gestion ne correspond pas à la copie de la clé racine approuvée du client, le certificat n’est pas validé. Dans ce cas, le client ne communique pas avec le point de gestion trouvé à l’aide de WINS.  


#### <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Assurez-vous que les fenêtres de maintenance sont assez grandes pour déployer des mises à jour logicielles critiques  

Les fenêtres de maintenance pour les regroupements d’appareils limitent les périodes où Configuration Manager peut installer des logiciels sur ces appareils. Si vous configurez une fenêtre de maintenance trop petite, le client peut ne pas installer les mises à jour logicielles critiques. Ce comportement laisse le client vulnérable à une attaque qui est contrée par la mise à jour logicielle.  


#### <a name="take-additional-security-precautions-to-reduce-the-attack-surface-on-windows-embedded-devices-with-write-filters"></a>Prendre des précautions de sécurité supplémentaires pour réduire la surface d’attaque sur les appareils Windows Embedded disposant de filtres d’écriture  

Quand vous activez des filtres d’écriture sur les appareils Windows Embedded, l’ensemble des installations ou changements de logiciels sont effectués uniquement dans le segment de recouvrement. Ces changements ne sont pas conservés après le redémarrage de l’appareil. Si vous utilisez Configuration Manager pour désactiver les filtres d’écriture, pendant cette période, l’appareil intégré est vulnérable aux changements apportés à tous les volumes. Ces volumes incluent les dossiers partagés.  

Configuration Manager verrouille l’ordinateur pendant cette période afin que seuls les administrateurs locaux puissent se connecter. Dans la mesure du possible, prenez des précautions de sécurité supplémentaires pour protéger l’ordinateur. Par exemple, activez des restrictions supplémentaires sur le pare-feu.  

Si vous utilisez des fenêtres de maintenance pour conserver les changements, planifiez soigneusement la durée de ces fenêtres. Réduisez le temps pendant lequel les filtres d’écriture sont désactivés, mais faites en sorte qu’ils soient suffisamment longs pour permettre aux installations logicielles et aux redémarrages de s’effectuer.  


#### <a name="use-the-latest-client-version-with-software-update-based-client-installation"></a>Utiliser la dernière version du client avec l’installation du client basée sur une mise à jour logicielle

Si vous utilisez l’installation du client basée sur une mise à jour logicielle, et que vous installez une version ultérieure du client sur le site, mettez à jour la mise à jour logicielle publiée. Les clients reçoivent alors la version la plus récente à partir du point de mise à jour logicielle.  

Quand vous mettez à jour le site, la mise à jour logicielle pour le déploiement du client qui est publié sur le point de mise à jour logicielle n’est pas exécutée automatiquement. Republiez le client Configuration Manager sur le point de mise à jour logicielle, puis mettez à jour le numéro de version.  

Pour plus d’informations, consultez [Guide pratique pour installer des clients Configuration Manager à l’aide d’une installation basée sur les mises à jour logicielles](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientSUP).  


#### <a name="only-suspend-bitlocker-pin-entry-on-trusted-and-restricted-access-devices"></a>Interrompre l’entrée du code confidentiel BitLocker uniquement sur les appareils approuvés et d’accès restreint  

Configurez le paramètre client **Interrompre l’entrée du code confidentiel BitLocker au redémarrage** sur **Toujours** uniquement pour les ordinateurs que vous approuvez et qui ont un accès physique limité.

Quand vous définissez ce paramètre client sur **Toujours**, Configuration Manager peut effectuer l’installation du logiciel. Ce comportement permet d’installer des mises à jour logicielles critiques et reprendre les services. Si un attaquant intercepte le processus de redémarrage, il peut prendre le contrôle de l’ordinateur. Utilisez ce paramètre seulement quand vous approuvez l’ordinateur et quand l’accès physique à l’ordinateur est limité. Par exemple, ce paramètre peut convenir aux serveurs d’un centre de données.  

Pour plus d’informations sur ce paramètre client, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#suspend-bitlocker-pin-entry-on-restart).  


#### <a name="dont-bypass-powershell-execution-policy"></a>Ne pas ignorer la stratégie d’exécution de PowerShell   

Si vous configurez le paramètre du client Configuration Manager de la **Stratégie d’exécution de PowerShell** sur **Ignorer**, Windows autorise l’exécution de scripts PowerShell non signés. Ce comportement pourrait autoriser l’exécution de programmes malveillants sur des ordinateurs clients. Quand votre organisation exige cette option, utilisez un paramètre client personnalisé. Attribuez-le uniquement aux ordinateurs clients qui doivent exécuter des scripts PowerShell non signés.  

Pour plus d’informations sur ce paramètre client, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#powershell-execution-policy).  



##  <a name="bkmk_mobile"></a> Bonnes pratiques de sécurité pour les appareils mobiles  


#### <a name="install-the-enrollment-proxy-point-in-a-perimeter-network-and-the-enrollment-point-in-the-intranet"></a>Installer le point proxy d'inscription dans un réseau de périmètre et le point d'inscription dans l'Intranet  

Pour les appareils mobiles Internet que vous inscrivez à l’aide de Configuration Manager, installez le point proxy d’inscription dans un réseau de périmètre et le point d’inscription sur l’intranet. Cette séparation des rôles permet de protéger le point d'inscription contre une attaque. Si un attaquant compromet le point d’inscription, il peut obtenir des certificats pour l’authentification. Il peut aussi voler les informations d’identification des utilisateurs qui inscrivent leurs appareils mobiles.  


#### <a name="configure-the-password-settings-to-help-protect-mobile-devices-from-unauthorized-access"></a>Configurer les paramètres de mot de passe pour protéger les appareils mobiles contre les accès non autorisés  

*Pour les appareils mobiles qui sont inscrits par Configuration Manager* : utilisez un élément de configuration d’appareil mobile pour configurer la complexité du mot de passe comme le code confidentiel. Spécifiez au moins la longueur de mot de passe minimale par défaut.  

*Pour les appareils mobiles sur lesquels le client Configuration Manager n’est pas installé mais qui sont gérés par le connecteur Exchange Server* : configurez les **Paramètres du mot de passe** pour le connecteur Exchange Server, de sorte que la complexité du mot de passe soit le code confidentiel. Spécifiez au moins la longueur de mot de passe minimale par défaut.  


#### <a name="only-allow-applications-to-run-that-are-signed-by-companies-that-you-trust"></a>Autoriser l’exécution des applications uniquement quand elles sont signées par des entreprises approuvées  

Empêchez la falsification des informations d’inventaire et des informations d’état en autorisant l’exécution des applications uniquement quand elles sont signées par des entreprises que vous approuvez. N’autorisez pas les appareils à installer des fichiers non signés.  

*Pour les appareils mobiles qui sont inscrits par Configuration Manager* : utilisez un élément de configuration d’appareil mobile pour configurer le paramètre de sécurité **Applications non signées** sur **Interdites**. Configurez les **Installations de fichiers non signés** comme une source approuvée.  

*Pour les appareils mobiles sur lesquels le client Configuration Manager n’est pas installé mais qui sont gérés par le connecteur Exchange Server* : configurez les **Paramètres d’application** pour le connecteur Exchange Server, de sorte que l’**Installation de fichiers non signés** et les **Applications non signées** soient **Interdites**.  


#### <a name="lock-mobile-devices-when-not-in-use"></a>Verrouiller les appareils mobiles quand ils ne sont pas en cours d’utilisation  

Empêchez les attaques par élévation de privilèges en verrouillant l’appareil mobile quand il n’est pas en cours d’utilisation.

*Pour les appareils mobiles qui sont inscrits par Configuration Manager* : utilisez un élément de configuration d’appareil mobile pour configurer le paramètre de mot de passe **Durée d’inactivité en minutes avant le verrouillage de l’appareil mobile**.  

*Pour les appareils mobiles sur lesquels le client Configuration Manager n’est pas installé mais qui sont gérés par le connecteur Exchange Server* : configurez les **Paramètres du mot de passe** pour le connecteur Exchange Server afin de configurer la **Durée d’inactivité en minutes avant le verrouillage de l’appareil mobile**.  


#### <a name="restrict-the-users-who-can-enroll-their-mobile-devices"></a>Limiter les utilisateurs pouvant inscrire leurs appareils mobiles  

permet d'éviter l'élévation de privilèges en limitant les utilisateurs qui peuvent inscrire leurs appareils mobiles. Utilisez un paramètre client personnalisé plutôt que les paramètres clients par défaut, pour que seuls les utilisateurs autorisés puissent inscrire leurs appareils mobiles.  


#### <a name="user-device-affinity-guidance-for-mobile-devices"></a>Conseils en matière d’affinité entre utilisateur et appareil pour les appareils mobiles  

Ne déployez pas d’applications sur les utilisateurs qui ont des appareils mobiles inscrits par Configuration Manager ou Windows Intune dans les cas suivants :  

-   L'appareil mobile est utilisé par plusieurs personnes.  

-   L'appareil est inscrit par un administrateur pour le compte d’un utilisateur.  

-   L’appareil est transféré à une autre personne sans mise hors service puis réinscription de l’appareil.  

L’inscription de l’appareil crée une relation d’affinité entre utilisateur et appareil. Cette relation mappe l’utilisateur qui effectue l’inscription à l’appareil mobile. Si un autre utilisateur utilise l’appareil mobile, il peut exécuter les applications déployées sur l’utilisateur d’origine, ce qui peut entraîner une élévation de privilèges. De même, si un administrateur inscrit l’appareil mobile pour un utilisateur, les applications déployées à l’utilisateur ne sont pas installées sur l’appareil mobile. À la place, les applications déployées sur l’administrateur peuvent être installées.  

Contrairement à l’affinité entre utilisateur et appareil pour les ordinateurs Windows, vous ne pouvez pas définir manuellement les informations d’affinité entre utilisateur et appareil pour les appareils mobiles inscrits par Microsoft Intune.  

Si vous transférez la propriété d’un appareil mobile inscrit par Intune, retirez d’abord l’appareil mobile d’Intune. Cette action supprime la relation d’affinité entre utilisateur et appareil. Demandez ensuite à l’utilisateur actuel de réinscrire l’appareil.  


#### <a name="make-sure-that-users-enroll-their-own-mobile-devices-for-microsoft-intune"></a>Vérifier que les utilisateurs inscrivent leurs propres appareils mobiles pour Microsoft Intune  

Une relation d’affinité entre utilisateur et appareil est créée lors de l’inscription. Cette action mappe l’utilisateur qui effectue l’inscription à l’appareil mobile. Si un administrateur inscrit l’appareil mobile pour un utilisateur, les applications déployées sur l’utilisateur ne sont pas installées sur l’appareil mobile. À la place, les applications déployées sur l’administrateur peuvent être installées.  


#### <a name="protect-the-connection-between-the-configuration-manager-site-server-and-the-exchange-server"></a>Protéger la connexion entre le serveur de site Configuration Manager et le serveur Exchange Server   

Si le serveur Exchange Server est sur site, utilisez IPsec. Exchange hébergé sécurise automatiquement la connexion à l’aide de SSL.  


#### <a name="use-the-principle-of-least-privileges-for-the-connector"></a>Utiliser le principe des privilèges minimum pour le connecteur  

Pour obtenir la liste des applets de commande minimales qu’exige le connecteur Exchange Server, consultez [Gérer les appareils mobiles avec Configuration Manager et Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



##  <a name="bkmk_macs"></a> Bonnes pratiques de sécurité pour les ordinateurs Mac  


#### <a name="store-and-access-the-client-source-files-from-a-secured-location"></a>Stocker les fichiers sources du client et y accéder à partir d’un emplacement sécurisé  

Avant d’installer ou d’inscrire le client sur un ordinateur Mac, Configuration Manager ne vérifie pas si ces fichiers sources du client ont été falsifiés. Téléchargez ces fichiers à partir d’une source digne de confiance. Stockez-les et accédez-y de manière sécurisée.  


#### <a name="monitor-and-track-the-validity-period-of-the-certificate"></a>Surveiller et effectuer le suivi de la période de validité du certificat  

Pour garantir la pérennité des activités, surveillez et effectuez le suivi de la période de validité des certificats que vous utilisez pour les ordinateurs Mac. Configuration Manager ne prend pas en charge le renouvellement automatique de ce certificat et ne vous avertit pas que le certificat est sur le point d’expirer. La période de validité standard est d’un an.  

Pour plus d’informations sur le renouvellement du certificat, consultez [Renouvellement manuel du certificat client Mac](/sccm/core/clients/deploy/deploy-clients-to-macs#renewing-the-mac-client-certificate).  


#### <a name="configure-the-trusted-root-certificate-for-ssl-only"></a>Configurer le certificat racine approuvé pour SSL uniquement  

Pour éviter une élévation des privilèges, configurez le certificat pour l’autorité de certification racine approuvée afin qu’il soit approuvé pour le protocole SSL uniquement.

Quand vous inscrivez des ordinateurs Mac, un certificat utilisateur destiné à gérer le client Configuration Manager est automatiquement installé. Ce certificat utilisateur inclut les certificats racines approuvés dans sa chaîne d’approbation. Pour limiter l’approbation de ce certificat racine au protocole SSL, utilisez la procédure suivante :  

1.  Sur l'ordinateur Mac, ouvrez une fenêtre de terminal.  

2.  Entrez la commande suivante : `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access`  

3.  Dans la boîte de dialogue **Accès au trousseau**, dans la section **Trousseaux**, cliquez sur **Système**. Ensuite, dans la section **Catégorie**, cliquez sur **Certificats**.  

4.  Localisez le certificat d’autorité de certification racine pour le certificat client Mac, puis double-cliquez dessus.  

5.  Dans la boîte de dialogue du certificat d'autorité de certification racine, développez la zone **Confiance** , puis apportez les modifications suivantes :  

    1.  **Lors de l’utilisation de ce certificat** : remplacez le paramètre **Toujours faire confiance** par **Utiliser les valeurs système par défaut**.  

    2.  **SSL (Secure Sockets Layer)**  : remplacez **aucune valeur spécifiée** par **Toujours faire confiance**.  

6.  Fermez la boîte de dialogue. Quand vous y êtes invité, entrez le mot de passe de l’administrateur, puis cliquez sur **Mettre à jour les paramètres**.  

Une fois cette procédure terminée, le certificat racine est approuvé uniquement pour valider le protocole SSL. Les autres protocoles qui sont maintenant non approuvés avec ce certificat racine incluent S/MIME (Courrier sécurisé), EAP (Extensible Authentication) ou la signature du code.  

> [!NOTE]  
>  Utilisez également cette procédure si vous avez installé le certificat client indépendamment de Configuration Manager.  



##  <a name="BKMK_SecurityIssues_Clients"></a> Problèmes de sécurité pour les clients Configuration Manager  

Les problèmes de sécurité suivants ne peuvent pas être atténués :  


#### <a name="status-messages-arent-authenticated"></a>Les messages d’état ne sont pas authentifiés  

Aucune authentification n'est effectuée sur les messages de statut. Lorsqu'un point de gestion accepte les connexions client HTTP, n'importe quel appareil peut envoyer des messages de statut au point de gestion. Si le point de gestion n’accepte que les connexions client HTTPS, un appareil doit avoir un certificat d’authentification client valide, mais peut également envoyer des messages d’état. Le point de gestion ignore tout message d’état non valide reçu d’un client.  

Il existe quelques attaques potentielles contre cette vulnérabilité : 
- Un attaquant pourrait envoyer un message d’état erroné pour adhérer à un regroupement basé sur des requêtes de messages d’état. 
- Un client pourrait déclencher un refus de service contre le point de gestion en l'inondant de messages de statut. 
- Si les messages de statut déclenchent des actions dans les règles de filtrage des messages de statut, un attaquant pourrait déclencher la règle de filtrage des messages de statut. 
- Un attaquant pourrait envoyer un message d’état qui rendrait les informations de rapport inexactes.  


#### <a name="policies-can-be-retargeted-to-non-targeted-clients"></a>Des stratégies peuvent être reciblées vers des clients non ciblés  

Un attaquant pourrait utiliser plusieurs méthodes pour faire en sorte qu'une stratégie ciblée sur un seul client soit appliquée à un client totalement différent. Par exemple, un attaquant au niveau d’un client approuvé pourrait envoyer de fausses informations de découverte ou d’inventaire pour que l’ordinateur soit ajouté à un regroupement auquel il ne devrait pas appartenir. Ce client reçoit ensuite tous les déploiements sur ce regroupement. 

Des contrôles existent pour empêcher des attaquants de modifier directement une stratégie. Toutefois, des attaquants pourraient prendre une stratégie existante qui reformate et redéploie un système d’exploitation et l’envoyer vers un autre ordinateur. Cette stratégie redirigée pourrait créer un déni de service. Ces types d'attaques demanderaient un minutage précis et des connaissances approfondies de l'infrastructure de Configuration Manager.  


#### <a name="client-logs-allow-user-access"></a>Les journaux du client permettent l'accès utilisateur  

Tous les fichiers journaux du client accordent au groupe **Utilisateurs** un accès en *Lecture*, et à l’utilisateur spécial **Interactif** un accès en *Écriture*. Si vous activez la journalisation détaillée, des attaquants peuvent lire les fichiers journaux pour y rechercher des informations sur la compatibilité ou les vulnérabilités du système. Les processus comme les logiciels que le client installe dans un contexte d’un utilisateur doivent écrire dans les journaux avec un compte d’utilisateur doté de droits restreints. Ce comportement signifie qu’un attaquant pourrait également écrire dans les journaux avec un compte doté de droits restreints.  

Le risque le plus sérieux est qu’un attaquant puisse supprimer des informations dans les fichiers journaux. Un administrateur pourrait avoir besoin de ces informations pour l’audit et la détection des intrusions.  


#### <a name="a-computer-could-be-used-to-obtain-a-certificate-thats-designed-for-mobile-device-enrollment"></a>Un ordinateur peut être utilisé pour obtenir un certificat destiné à l’inscription d’appareils mobiles  

Quand Configuration Manager traite une demande d’inscription, il ne peut pas vérifier qu’elle émane d’un appareil mobile plutôt que d’un ordinateur. Si la demande provient d'un ordinateur, il peut installer un certificat PKI qui lui permet ensuite de s'inscrire avec Configuration Manager. 

Pour prévenir une attaque par élévation de privilèges dans ce scénario, n’autorisez que les utilisateurs approuvés à inscrire leurs appareils mobiles. Surveillez attentivement les activités d'inscription d’appareil dans le site.  


#### <a name="a-blocked-client-can-still-send-messages-to-the-management-point"></a>Un client bloqué peut toujours envoyer des messages au point de gestion

Quand vous bloquez un client auquel vous ne faites plus confiance, mais qui a établi une connexion réseau pour la notification du client, Configuration Manager ne déconnecte pas la session. Le client bloqué peut continuer à envoyer des paquets à son point de gestion jusqu'à ce que le client se déconnecte du réseau. Ces paquets sont seulement des paquets persistants de petite taille. Ce client ne peut pas être géré par Configuration Manager tant qu’il n’est pas débloqué.  


#### <a name="automatic-client-upgrade-doesnt-verify-the-management-point"></a>La mise à niveau automatique du client ne vérifie pas le point de gestion

Quand vous utilisez la mise à niveau automatique du client, ce dernier peut être dirigé vers un point de gestion pour télécharger les fichiers sources du client. Dans ce cas, le client ne vérifie pas le point de gestion comme une source fiable.  


#### <a name="when-users-first-enroll-mac-computers-theyre-at-risk-from-dns-spoofing"></a>Quand les utilisateurs inscrivent des ordinateurs Mac pour la première fois, ils sont exposés à l’usurpation DNS  

Quand l’ordinateur Mac se connecte au point proxy d’inscription lors de l’inscription, il est peu probable qu’il possède déjà le certificat d’autorité de certification racine approuvé. À ce stade, l’ordinateur Mac n’approuve pas le serveur et invite l’utilisateur à continuer. Si un serveur DNS non autorisé résout le nom de domaine complet (FQDN) du point proxy d’inscription, il peut diriger l’ordinateur Mac vers un point proxy d’inscription non autorisé pour installer des certificats à partir d’une source non approuvée. Pour réduire ce risque, suivez les meilleures pratiques afin d'éviter l'usurpation DNS dans votre environnement.  


#### <a name="mac-enrollment-doesnt-limit-certificate-requests"></a>L’inscription d’ordinateurs Mac ne limite pas les demandes de certificat  

Les utilisateurs peuvent réinscrire leurs ordinateurs Mac, en demandant chaque fois un certificat client. Configuration Manager ne vérifie pas s’il existe plusieurs demandes ni ne limite le nombre de certificats demandés à partir d’un seul ordinateur. Un utilisateur non autorisé pourrait exécuter un script qui répète la demande d’inscription de ligne de commande. Cette attaque pourrait entraîner un déni de service sur le réseau ou sur l’autorité de certification émettrice. Pour réduire ce risque, surveillez attentivement l'autorité de certification émettrice pour ce type de comportement suspect. Bloquez immédiatement à partir de la hiérarchie Configuration Manager tout ordinateur qui présente ce modèle de comportement.  


#### <a name="a-wipe-acknowledgment-doesnt-verify-that-the-device-has-been-successfully-wiped"></a>Un accusé de réception de réinitialisation ne vérifie pas que l’appareil a bien été réinitialisé  

Quand vous lancez une action de réinitialisation pour un appareil mobile et que Configuration Manager accuse réception de la réinitialisation, la vérification indique que Configuration Manager a bien *envoyé* le message. Il ne vérifie pas que l’appareil a *traité* la demande. 

Pour les appareils mobiles gérés par le connecteur Exchange Server, un accusé de réception de réinitialisation vérifie que la commande a été reçue par Exchange, et non par l’appareil.  


#### <a name="if-you-use-the-options-to-commit-changes-on-windows-embedded-devices-accounts-might-be-locked-out-sooner-than-expected"></a>Si vous utilisez les options permettant de valider des changements sur des appareils Windows Embedded, les comptes peuvent être verrouillés plus tôt que prévu  

Si l’appareil Windows Embedded exécute une version de système d’exploitation antérieure à Windows 7, et qu’un utilisateur tente de se connecter alors que les filtres d’écriture sont désactivés par Configuration Manager, Windows n’autorise que la moitié du nombre configuré de tentatives incorrectes avant le verrouillage du compte. 

Par exemple, vous configurez la stratégie de domaine pour un **Seuil de verrouillage de comptes** à six tentatives. Un utilisateur entre son mot de passe incorrectement trois fois, et le compte est verrouillé. Ce comportement crée en fait un déni de service. Si les utilisateurs doivent se connecter à des appareils intégrés dans ce scénario, avertissez-les du risque d’un seuil de verrouillage réduit.  



##  <a name="BKMK_Privacy_Clients"></a> Informations de confidentialité pour les clients Configuration Manager  

Quand vous déployez le client Configuration Manager, vous activez des paramètres client pour les fonctionnalités Configuration Manager. Les paramètres que vous utilisez pour configurer les fonctionnalités peuvent s’appliquer à tous les clients dans la hiérarchie Configuration Manager. Ce comportement est le même, qu’ils soient directement connectés au réseau interne, qu’ils soient connectés par le biais d’une session distante ou qu’ils soient connectés à Internet.  

Les informations sur le client sont stockées dans la base de données Configuration Manager de votre serveur SQL et ne sont pas envoyées à Microsoft. Les informations sont conservées dans la base de données jusqu’à leur suppression par les tâches de maintenance du site **Supprimer les données de découverte anciennes**, tous les 90 jours. Vous pouvez configurer l'intervalle de suppression. 

Certaines données de diagnostic et d’utilisation résumées ou agrégées sont envoyées à Microsoft. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

Avant de configurer le client Configuration Manager, réfléchissez à vos besoins en matière de confidentialité.  


### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informations sur la confidentialité des appareils mobiles qui sont inscrits par Configuration Manager  

Pour obtenir des informations de confidentialité quand vous inscrivez un appareil mobile par Configuration Manager, consultez [Déclaration de confidentialité de System Center Configuration Manager - Addendum relatif aux appareils mobiles](/sccm/core/misc/privacy/privacy-statement-mobile-device-addendum).  


### <a name="client-status"></a>État du client  

Configuration Manager surveille l’activité des clients. Il évalue régulièrement le client Configuration Manager, et peut résoudre les problèmes liés au client et à ses dépendances. L’état du client est activé par défaut. Il utilise les mesures côté serveur pour vérifier l’activité du client. L’état du client utilise les actions côté client pour les auto-contrôles, la correction, ainsi que l’envoi d’informations sur l’état du client au site. Le client exécute les auto-contrôles en fonction d’une planification que vous configurez. Le client envoie les résultats des contrôles au site Configuration Manager. Ces informations sont chiffrées lors du transfert.  

Les informations d’état du client sont stockées dans la base de données Configuration Manager de votre serveur SQL, et ne sont pas envoyées à Microsoft. Elles ne sont pas stockées au format chiffré dans la base de données du site. Elles sont conservées dans la base de données jusqu’à ce qu’elles en soient supprimées en fonction de la valeur configurée pour le paramètre d’état du client **Conserver l’historique de l’état du client pendant le nombre de jours suivant**. La valeur par défaut pour ce paramètre est 31 jours.  

Avant d'installer le client Configuration Manager avec vérification de l'état du client, pensez à vos besoins en matière de confidentialité.  



##  <a name="BKMK_Privacy_ExchangeConnector"></a> Informations de confidentialité pour les appareils mobiles qui sont gérés à l’aide du connecteur Exchange Server  

Le connecteur Exchange Server détecte et gère les appareils qui se connectent à un serveur Exchange Server sur site ou hébergé en utilisant le protocole ActiveSync. Les enregistrements trouvés par le connecteur Exchange Server sont stockés dans la base de données Configuration Manager de votre serveur SQL. Les informations sont collectées à partir d’Exchange Server. Elles ne contiennent pas d’informations supplémentaires par rapport à ce que les appareils mobiles envoient à Exchange Server.  

Les informations des appareils mobiles ne sont pas envoyées à Microsoft. Elles sont stockées dans la base de données Configuration Manager de votre serveur SQL. Elles sont conservées dans la base de données jusqu’à leur suppression par la tâche de maintenance du site **Supprimer les données de découverte anciennes**, tous les 90 jours. Vous configurez l’intervalle de suppression.  

Avant d'installer et de configurer le connecteur Exchange Server, pensez à vos besoins en matière de confidentialité.  
