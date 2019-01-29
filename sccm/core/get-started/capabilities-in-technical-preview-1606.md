---
title: Capacités de la version Technical Preview 1606
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1606 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: b03408db6c6cc87ccfe8d7b1b1353ee39a11c1da
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54898441"
---
# <a name="capabilities-in-technical-preview-1606-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1606 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager Technical Preview*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1606 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    

**Problèmes connus dans cette version d’évaluation technique :**  
*  Lorsque vous mettez à jour la version d’évaluation technique 1604 vers la version 1605, puis vers la version 1606, la mise à jour peut échouer et une erreur similaire à la suivante est enregistrée dans le fichier **cmupdate.log** :

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    Si cela se produit, dans le nœud **Mises à jour et maintenance**, cliquez sur **Rechercher les mises à jour**, puis **réessayez** l’installation de la mise à jour.
    ***

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="dmp_category"></a> Classer automatiquement des appareils dans des regroupements
Vous pouvez créer des catégories d’appareils pour classer automatiquement les appareils dans des regroupements d’appareils quand vous utilisez Configuration Manager avec Microsoft Intune. Les utilisateurs sont alors invités à choisir une catégorie d’appareils quand ils inscrivent un appareil dans Intune. Vous pouvez aussi modifier la catégorie d’un appareil à partir de la console Configuration Manager.

**Important :** Cette fonctionnalité est opérationnelle avec la version de **juin 2016** de Microsoft Intune. Vérifiez que vous avez effectué la mise à jour vers cette version avant d’essayer ces procédures.

### <a name="try-it-out"></a>Essayez !

### <a name="create-a-set-of-device-categories"></a>Créer un ensemble de catégories d’appareils
1.  Dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager, développez **Vue d’ensemble**, puis cliquez sur **Regroupements d’appareils**.
2.  Sous l’onglet **Accueil**, dans le groupe **Catégories**, cliquez sur **Gérer les catégories d’appareils**.
3.  Dans la boîte de dialogue **Gérer les catégories d’appareils**, vous pouvez créer, modifier ou supprimer des catégories. Essayez de créer une nouvelle catégorie.

### <a name="associate-a-collection-with-a-device-category"></a>Associer un regroupement à une catégorie d’appareils
Quand vous associez un regroupement à une catégorie d’appareils, tous les appareils de la catégorie que vous spécifiez sont ajoutés à ce regroupement.
1.  Dans la boîte de dialogue **Propriétés** d’un regroupement d’appareils, cliquez sur **Ajouter une règle** > **Règle de catégorie d’appareils**.
2.  Dans la boîte de dialogue **Créer une règle d’adhésion de catégorie d’appareils**, sélectionnez la catégorie à appliquer à tous les appareils du regroupement.
3.  Fermez la boîte de dialogue **Créer une règle d’adhésion de catégorie d’appareils** et celle des propriétés du regroupement.

### <a name="change-the-category-of-a-device"></a>Changer la catégorie d’un appareil
1.  Dans l’espace de travail **Ressources et Conformité** de la console Configuration Manager, développez **Vue d’ensemble**, puis cliquez sur **Appareils**.
2.  Sélectionnez un appareil dans la liste **Appareils** et, sous l’onglet **Accueil**, dans le groupe **Appareil**, cliquez sur **Changer la catégorie**.
3.  Dans la boîte de dialogue **Modifier la catégorie d’appareils**, choisissez la catégorie à appliquer à cet appareil, puis cliquez sur **OK**.

## <a name="dmp_grace"></a> Période de grâce de mise en œuvre des déploiements d’applications et de mises à jour logicielles obligatoires

Dans certains cas, vous pouvez accorder plus de temps aux utilisateurs pour installer les mises à jour logicielles ou les déploiements d’applications obligatoires au-delà des échéances que vous avez configurées. Cela est généralement nécessaire lorsqu’un ordinateur a été éteint pendant une période de temps prolongée et qu’il doit installer un grand nombre de déploiements d’applications ou de mises à jour.
Par exemple, si un utilisateur final vient de rentrer de congés, il peut être amené à patienter longtemps pendant l’installation des déploiements d’applications en retard.
Pour résoudre ce problème, vous pouvez désormais définir une période de grâce de mise en œuvre en déployant des paramètres du client Configuration Manager sur un regroupement.

### <a name="try-it-out"></a>Essayez !

Pour configurer la période de grâce, procédez comme suit :

1.  Dans la page **Agent ordinateur** des paramètres du client, configurez la nouvelle propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** avec une valeur comprise entre **1** et **120** heures.
2.  Dans un nouveau déploiement d’application requis, ou dans les propriétés d’un déploiement existant, dans la page **Planification**, cochez la case **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres client**.
Tous les déploiements pour lesquels cette case à cocher est activée et qui sont destinés à des appareils sur lesquels vous avez également déployé le paramètre du client utiliseront la période de grâce de mise en œuvre.

Si vous configurez une période de grâce de mise en œuvre et cochez la case, une fois que l’échéance d’installation d’application est atteinte, l’application est installée dans la première fenêtre non professionnelle que l’utilisateur a configurée jusqu’à cette période de grâce. Toutefois, l’utilisateur peut toujours ouvrir le Centre logiciel et installer l’application à tout moment, s’il le souhaite. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard.
Des options similaires ont été ajoutées dans l’Assistant de déploiement de mises à jour logicielles, dans l’Assistant des règles de déploiement automatique et dans les pages de propriétés.

##  <a name="dmp_devg"></a>Utilisation de Configuration Manager comme programme d’installation géré avec Device Guard

Device Guard est une fonctionnalité de Windows 10 qui utilise des fonctionnalités matérielles et logicielles pour contrôler de manière stricte ce qui est autorisé à s’exécuter sur l’appareil.

Vous pouvez lire une présentation détaillée de ce que fait Device Guard et de la manière dont il fonctionne dans [cet article Technet](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

Dans cette version, Configuration Manager peut interagir avec Device Guard et [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) afin que les fichiers exécutables et DLL qui sont déployés avec Configuration Manager soient automatiquement approuvés quand ils proviennent d’un programme d’installation géré. Cela signifie que ces fichiers seront autorisés à s’exécuter sur l’appareil cible, alors que d’autres logiciels ne pourront pas s’exécuter, sauf s’ils sont explicitement autorisés à le faire par d’autres règles AppLocker.  

Actuellement, cette fonctionnalité n’est pas configurable à partir de la console Configuration Manager. Configurer cette stratégie vous oblige à configurer une clé de Registre sur chaque client et à configurer les services Windows sur le client.
Une fois cette opération effectuée, configurez le fichier de stratégie AppLocker. Après avoir configuré le fichier de stratégie, vous pouvez le déployer sur un appareil client compatible quelconque.


Comme toutes les stratégies AppLocker, les stratégies avec des règles de programme d’installation géré peuvent s’exécuter dans deux modes :

- Mode audit : Rien n’empêche les applications de s’exécuter, mais toutes les applications qui auraient été bloquées sont signalées dans un fichier journal (cette opération sera prise en charge dans une version ultérieure de Configuration Manager).
- Mise en œuvre activée : Les applications sont bloquées et ne peuvent pas s’exécuter.

Des informations complémentaires sur l’utilisation de Device Guard avec Configuration Manager sont disponibles dans le blog [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Articles complémentaires :

- [Présentation de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Compatibilité et certification de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Guide de déploiement de Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

  ##  <a name="dmp_onprem"></a> Points de gestion d’appareils multiples pour la gestion des appareils mobiles locale  
  Avec la version d’évaluation technique 1606, la gestion des appareils mobiles (MDM) locale prend en charge une nouvelle fonctionnalité de la mise à jour anniversaire de Windows 10, qui configure automatiquement un appareil inscrit pour bénéficier de plusieurs points de gestion d’appareil disponibles. Cette fonctionnalité permet à l’appareil de basculer vers un autre point de gestion d’appareil quand celui qu’il utilise normalement n’est pas disponible. Cette fonctionnalité fonctionne uniquement pour les PC dotés de la mise à jour anniversaire de Windows 10.  

### <a name="try-it-out"></a>Essayez !  

1.  Installez plusieurs points de gestion d’appareil dans votre hiérarchie.  

2.  Inscrivez un appareil doté de la mise à jour anniversaire de Windows 10 pour la gestion des appareils mobiles locale.  

Pour plus d’informations sur la façon de préparer votre site et d’inscrire des appareils pour la gestion des appareils mobiles locale, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud_proxy"></a>Service proxy cloud pour la gestion des clients sur Internet

Le service proxy cloud fournit un moyen simple de gérer les clients Configuration Manager sur Internet. Ce service, qui est déployé sur Microsoft Azure et requiert un abonnement Azure, se connecte à votre infrastructure Configuration Manager locale à l’aide d’un nouveau rôle nommé Point du connecteur de proxy cloud. Après son déploiement et sa configuration, les clients peuvent accéder aux rôles de système de site Configuration Manager locaux, qu’ils soient connectés au réseau privé interne ou à Internet.

Vous utilisez la console Configuration Manager pour déployer le service sur Azure, ajouter le rôle de point du connecteur de proxy cloud et configurer les rôles de système de site pour autoriser le trafic du proxy cloud. Le service proxy cloud ne prend en charge actuellement que les rôles de point de gestion, de point de distribution et de point de mise à jour logicielle.

Les certificats clients et les certificats Secure Socket Layer (SSL) sont requis pour authentifier les ordinateurs et chiffrer les communications entre les différents niveaux du service. En règle générale, les ordinateurs clients reçoivent un certificat client via la mise en œuvre d’une stratégie de groupe. Pour chiffrer le trafic entre les clients et le serveur de système de site hébergeant les rôles, vous devez créer un certificat SSL personnalisé à partir de l’autorité de certification. En plus de ces deux types de certificats, vous devez également configurer un certificat de gestion sur Azure, permettant à Configuration Manager de déployer le service proxy cloud.  

### <a name="requirements-for-cloud-proxy-service-in-tp-1606"></a>Configuration requise pour le service proxy cloud dans la version d’évaluation technique 1606
- Les ordinateurs clients et le serveur de système de site doivent exécuter le point du connecteur de proxy cloud.
- Certificats SSL personnalisés provenant de l’autorité de certification interne : utilisés pour chiffrer la communication en provenance des ordinateurs clients et authentifier l’identité du service proxy cloud.
- Abonnement Azure pour les services cloud.
- Certificat de gestion Azure : utilisé pour authentifier Configuration Manager auprès d’Azure.

### <a name="limitations-of-cloud-proxy-service-in-tp-1606"></a>Limitations du service proxy cloud dans la version d’évaluation technique 1606

- Prend en charge uniquement les rôles de point de gestion, de point de distribution et de point de mise à jour logicielle.
- Les stratégies utilisateur ne sont pas prises en charge.
- Ne peut pas être utilisé avec la [gestion des appareils mobiles locale](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) dans Configuration Manager.
- Pris en charge uniquement sur la plateforme de cloud public d’Azure.


### <a name="try-it-out"></a>Essayez !

Le processus de déploiement du service proxy cloud inclut les étapes suivantes :

1. Créez et émettez un certificat SSL personnalisé pour le service proxy cloud.
1. Exportez la racine du certificat client.
2. Chargez le certificat de gestion dans Azure.
3. Configurez le service proxy cloud dans la console Configuration Manager.
4. Configurez le site principal pour utiliser l’authentification de certificat client.
5. Ajoutez le point du connecteur de proxy cloud à votre site.
6. Configurez les rôles de système de site pour accepter le trafic du proxy cloud.

Les sections suivantes fournissent plus d’informations sur ces étapes.

#### <a name="create-a-custom-ssl-certificate"></a>Créer un certificat SSL personnalisé

Vous pouvez créer un certificat SSL personnalisé pour le service proxy cloud de la même façon que vous le feriez pour un point de distribution basé sur le cloud. Suivez les instructions pour le [déploiement du certificat de service pour les points de distribution cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), mais procédez différemment pour ce qui suit :

* Lorsque vous configurez le nouveau modèle de certificat, accordez les autorisations **Lecture** et **Inscription** au groupe de sécurité que vous configurez pour les serveurs Configuration Manager.

#### <a name="export-the-client-certificates-root"></a>Exporter la racine du certificat client

Le moyen le plus simple pour exporter la racine des certificats clients utilisés sur le réseau consiste à ouvrir un certificat client sur l’une des machines jointes au domaine qui en possède un, et de le copier.

>[!NOTE]
>Des certificats clients sont requis sur chaque ordinateur que vous voulez gérer avec le service proxy cloud et sur le serveur de système de site qui héberge le point du connecteur de proxy cloud. Si vous devez ajouter un certificat client à l’une quelconque de ces machines, consultez [Déploiement du certificat client pour les ordinateurs Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).

1. Dans la fenêtre Exécuter, tapez **mmc** et appuyez sur Entrée.
2. Dans le menu Fichier de la console de gestion, cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.
3. Dans la boîte de dialogue Ajouter ou supprimer des composants logiciels enfichables, cliquez sur **Certificats**, sur **Ajouter >**, sur **Compte d’ordinateur**, sur **Suivant**, sur **Ordinateur local**, puis sur **Terminer**. Cliquez sur **OK** pour fermer la boîte de dialogue.
4. Accédez à **Certificats > Personnel > Certificats**.
5. Double-cliquez sur le certificat pour l’authentification du client sur l’ordinateur, cliquez sur l’onglet Chemin d’accès de certification et double-cliquez sur l’autorité racine (en haut du chemin d’accès).
6.  Cliquez sur l’onglet Détails, puis cliquez sur **Copier dans un fichier**.
7. Terminez l’Assistant Exportation de certificat en utilisant le format de certificat par défaut. Notez le nom et l’emplacement du certificat racine que vous créez. Vous en aurez besoin pour configurer le service proxy cloud dans une étape ultérieure.

#### <a name="upload-the-management-certificate-to-azure"></a>Charger le certificat de gestion dans Azure

Un certificat de gestion Azure est requis pour que Configuration Manager puisse accéder à l’API Azure et configurer le service proxy cloud. Pour plus d’informations et des instructions sur la manière de charger un certificat de gestion, consultez les articles suivants dans la documentation Azure :
- [Vue d’ensemble des certificats pour Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Téléchargement d’un certificat de gestion API dans Azure Management](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Veillez à copier l’ID d’abonnement associé au certificat de gestion. Vous en aurez besoin pour configurer le service proxy cloud dans la console Configuration Manager.

#### <a name="set-up-cloud-proxy-service"></a>Configurer le service proxy cloud

1. Ouvrez la console Configuration Manager, puis accédez à **Administration > Services cloud > Service proxy cloud**.
2. Cliquez sur **Créer un service proxy cloud**.
3. Dans l’Assistant Création d’un service proxy cloud, entrez votre ID d’abonnement Azure (copié à partir du portail de gestion Azure), cliquez sur Parcourir et sélectionnez le fichier de certificat que vous avez chargé comme certificat de gestion Azure. Cliquez sur **Suivant**. Attendez quelques instants que la console se connecte à Azure.
4. Remplissez les détails supplémentaires dans l’Assistant :
    - Spécifiez la clé privée (fichier .pfx) que vous avez exportée à partir du certificat SSL personnalisé.
    - Spécifiez le certificat racine exporté à partir du certificat client.
    - Spécifiez le même nom de domaine complet de service que vous avez utilisé lorsque vous avez créé le nouveau modèle de certificat.
    - Décochez la case à côté de **Vérifier la révocation des certificats clients** (sauf si vous publiez publiquement les informations de votre liste de révocation de certificats).
    - Cliquez sur **Suivant** lorsque vous avez terminé.
5. Vérifiez les paramètres et cliquez sur **Suivant**. Configuration Manager commence à configurer le service. Une fois que l’Assistant a terminé, vous pouvez cliquer sur **Fermer**, mais il faudra entre 5 et 15 minutes pour configurer complètement le service dans Azure. Vérifiez la colonne **État** du service proxy cloud nouvellement configuré pour déterminer quand le service est prêt.

#### <a name="configure-primary-site-for-client-certification-authentication"></a>Configurer le site principal pour l’authentification de certification de client

1. Dans la console Configuration Manager, accédez à **Administration > Configuration du site > Sites**.
2. Sélectionnez le site principal pour les clients que vous souhaitez gérer via le service proxy cloud, puis cliquez sur **Propriétés**.
3. Sous l’onglet Communications des ordinateurs clients de la feuille de propriétés du site principal, cochez la case à côté de **Utiliser le certificat client PKI (fonctionnalité d’authentification du client) lorsqu’il est disponible**.
4. Veillez à décocher la case à côté de **Les clients vérifient la liste de révocation des certificats (CRL) pour les systèmes de site**. Cette option serait nécessaire seulement si vous publiiez publiquement votre liste de révocation de certificats.
5. Cliquez sur **OK**.

#### <a name="add-the-cloud-proxy-connector-point"></a>Ajouter le point du connecteur de proxy cloud

Le point du connecteur de proxy cloud est un nouveau rôle de système de site permettant de communiquer avec le service proxy cloud. Pour ajouter le point du connecteur de proxy cloud, suivez les instructions de la rubrique [Ajouter des rôles de système de site pour System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### <a name="configure-roles-for-cloud-proxy-traffic"></a>Configurer des rôles pour le trafic du proxy cloud

La dernière étape de la configuration du service proxy cloud consiste à configurer les rôles de système de site pour qu’ils acceptent le trafic du proxy cloud. Pour la version d’évaluation technique 1606, seuls les rôles de point de gestion, de point de distribution et de point de mise à jour logicielle sont pris en charge pour le service proxy cloud. Vous devez configurer chaque rôle séparément.

1. Dans la console Configuration Manager, accédez à **Administration > Configuration du site > Serveurs et rôles de système de site**.
2. Cliquez sur le serveur de système de site pour le rôle que vous souhaitez configurer pour le trafic du proxy cloud.
3. Cliquez sur le rôle, puis sur **Propriétés**.
4. Dans la feuille de propriétés du rôle, sous Connexions client, choisissez **HTTPS**, cochez la case à côté de **Autoriser le trafic du proxy cloud de Configuration Manager**, puis cliquez sur **OK**. Répétez ces étapes pour les autres rôles.

#### <a name="check-status-on-a-client-on-the-internet"></a>Vérifier l’état d’un client sur Internet

Une fois que le service et les rôles ont été entièrement configurés, les clients internes obtiennent l’emplacement du service proxy cloud à la prochaine demande d’emplacement. Les clients avec les informations d’emplacement mises à jour peuvent alors communiquer avec Configuration Manager sur Internet. Le cycle d’interrogation pour les demandes d’emplacement est de 24 heures. Si vous ne souhaitez pas attendre la demande d’emplacement normalement planifiée, vous pouvez forcer la demande en redémarrant le service hôte de l’agent SMS (ccmexec.exe) sur l’ordinateur.

Une fois que les clients possèdent les nouvelles informations d’emplacement pour le service proxy cloud, essayez de vérifier l’état des clients qui ne sont plus sur le réseau privé interne, mais qui ont accès à Internet. Vous pouvez également surveiller le trafic sur le service proxy cloud en accédant à **Administration > Services cloud > Service proxy cloud**, en sélectionnant le service dans le volet Liste et en consultant les informations de trafic dans le volet d’informations.   

## <a name="manage_o365"></a>Gérer l’agent Office 365 Client dans Configuration Manager  

À partir de la version d’évaluation technique 1606, vous pouvez utiliser un paramètre de l’agent client Configuration Manager, à la place d’une stratégie de groupe, pour permettre aux clients Office 365 de recevoir des mises à jour à partir de Configuration Manager. Après avoir configuré ce paramètre et déployé les mises à jour Office 365, l’agent client Configuration Manager communique avec l’agent Office 365 Client pour télécharger les mises à jour Office 365 à partir d’un point de distribution et les installer. Configuration Manager effectue également l’inventaire du paramètre de l’agent client.

Pour plus d’informations, consultez [Gérer les mises à jour Office 365 ProPlus](https://technet.microsoft.com/library/mt741983.aspx).

### <a name="set-the-configuration-manager-client-setting-to-manage-the-office-365-client-agent"></a>Définir le paramètre du client Configuration Manager pour gérer l’agent Office 365 Client
1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Vue d’ensemble** > **Paramètres client**.
2. Ouvrez les paramètres d’appareil appropriés pour activer l’agent client. Pour plus d’informations sur les paramètres par défaut et personnalisés du client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).
3. Cliquez sur **Mises à jour logicielles** et sélectionnez **Oui** pour le paramètre **Activer la gestion de l’agent Office 365 Client**.  


## <a name="osdpreservedriveletter"></a>La variable de séquence de tâches OSDPreserveDriveLetter est dépréciée
La variable de séquence de tâches OSDPreverveDriveLetter détermine si la séquence de tâches utilise ou non la lettre de lecteur capturée dans le fichier WIM d’image de système d’exploitation au moment où vous appliquez cette image à un ordinateur de destination.
- Cette variable de séquence de tâches est déconseillée à partir de la version d’évaluation technique 1606.

Lors d’un déploiement de système d’exploitation, par défaut, le programme d’installation Windows détermine désormais la meilleure lettre de lecteur à utiliser (généralement C:). Si vous souhaitez spécifier un autre lecteur à utiliser, vous pouvez modifier l’emplacement dans l’étape de séquence de tâches Appliquer le système d’exploitation. Accédez au paramètre **Sélectionnez l’emplacement où vous souhaitez appliquer ce système d’exploitation**, sélectionnez **Lettre de lecteur logique spécifique**, puis choisissez le lecteur que vous souhaitez utiliser. Il doit y avoir un lecteur affecté à la lettre que vous sélectionnez sur l’ordinateur de destination. 

## <a name="updatesandservicing"></a>Modifications pour le nœud Mises à jour et maintenance
Dans la version d’évaluation technique 1606, plusieurs modifications ont été introduites qui s’appliquent aux mises à jour et à la maintenance dans la console Configuration Manager :
- **Changement de nom du nœud :**

    Dans l’espace de travail **Surveillance**, le nœud **État de maintenance du site** a été renommé en **État des mises à jour et de la maintenance**.
- **État de l’installation plus détaillé :**

    Quand vous affichez l’état de l’installation d’une mise à jour pour un site, la console affiche maintenant les détails pour chacune des actions suivantes :
    - **Téléchargement** (Cela s’applique uniquement au site de niveau supérieur où est installé le rôle de système de site de point de connexion de service)
    - **Réplication**
    - **Vérification des prérequis**
    - **Installation**

  De plus, des informations plus détaillées sont maintenant fournies pour chaque étape, notamment le fichier journal que vous pouvez consulter pour obtenir plus d’informations.  
-   **Nouvelle option pour retenter l’installation après l’échec de la vérification des prérequis :**

    Dans les espaces de travail **Administration** et **Surveillance**, le nœud **Mises à jour et maintenance** affiche le nouveau bouton **Ignorer les avertissements de configuration requise** sur le ruban.

    Quand vous installez des mises à jour sans utiliser l’option Ignorer les avertissements de configuration requise (à partir de l’Assistant Mises à jour) et que l’installation des mises à jour s’arrête avec un état **Avertissement de configuration requise**, vous pouvez maintenant sélectionner le bouton **Ignorer les avertissements de configuration requise** dans le ruban pour ignorer les avertissements et continuer automatiquement l’installation des mises à jour.  



- **Vue plus claire des mises à jour :**

    Quand vous affichez le nœud **Mises à jour et maintenance**, vous voyez maintenant uniquement la dernière mise à jour que vous avez installée, ainsi que les nouvelles mises à jour prêtes à être installées. Pour afficher les mises à jour précédemment installées, cliquez sur le nouveau bouton **Historique** dans le ruban.  

-   **Option renommée pour la pré-production :**

    Dans le nœud Mises à jour et maintenance, le bouton qui était appelé **Options du client** a été renommé **Promouvoir le client de préproduction**.
