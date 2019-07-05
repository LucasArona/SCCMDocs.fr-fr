---
title: Capacités de la version Technical Preview 1703
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1703 de System Center Configuration Manager.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bc5ebcbec87edf52d7ca7d3f9e6f4341ec60c191
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67515828"
---
# <a name="capabilities-in-technical-preview-1703-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1703 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*

Cet article présente les fonctionnalités disponibles dans la version Technical Preview 1703 de System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Déployer des applications iOS achetées en volume sur des regroupements d’appareils

Vous pouvez désormais déployer des applications sous licence sur des appareils ainsi que des utilisateurs. En fonction de la capacité des applications à prendre en charge les licences d’appareils, une licence appropriée sera réclamée lors du déploiement, comme suit :

|||||
|-|-|-|-|
|Version de Configuration Manager|L’application prend-elle en charge les licences d’appareil ?|Type de regroupement de déploiement|Licence demandée|
|Antérieure à 1702|Oui|utilisateur|Licence utilisateur|
|Antérieure à 1702|Non|utilisateur|Licence utilisateur|
|Antérieure à 1702|Oui|Appareil|Licence utilisateur|
|Antérieure à 1702|Non|Appareil|Licence utilisateur|
|1702 et versions ultérieures|Oui|utilisateur|Licence utilisateur|
|1702 et versions ultérieures|Non|utilisateur|Licence utilisateur|
|1702 et versions ultérieures|Oui|Appareil|Licence d’appareil|
|1702 et versions ultérieures|Non|Appareil|Licence utilisateur|

Pour plus d’informations sur les applications iOS achetées en volume, consultez [Gérer des applications iOS achetées en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

## <a name="direct-links-to-applications-in-software-center"></a>Liens directs aux applications dans le Centre logiciel

Vous pouvez désormais fournir aux utilisateurs finaux un lien direct à une application du Centre logiciel. De cette façon, ils ne sont pas obligés d’ouvrir le Centre logiciel et de rechercher une application pour l’installer. Cette fonctionnalité est uniquement disponible pour les applications Configuration Manager ; elle ne s’applique pas aux packages, programmes ou séquences de tâches.

### <a name="try-it-out"></a>Faîtes un essai                 

Utilisez le format d’URL suivant pour ouvrir le Centre logiciel à une application particulière :

**Softwarecenter:SoftwareId=_Identificateur de l’application_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>Comment obtenir l’identificateur d’une application

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2.  Dans l’espace de travail Bibliothèque de logiciels, développez **Gestion des applications**, puis cliquez sur **Applications**.
3.  Dans l’affichage **Applications**, cliquez avec le bouton droit sur l’un des en-têtes de colonne. Ensuite, dans la liste, sélectionnez **ID unique de l’élément de configuration**. L’ID unique de chaque application s’affiche alors dans la liste.
4.  Notez l’**ID unique de CI** de l’application vers laquelle vous souhaitez pointer, par exemple : **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5.  Ensuite, supprimez le texte situé après le GUID de l’application (dans ce cas, **/2**). Il vous reste alors l’identificateur de l’application.
6.  Enfin, pour terminer la création du lien, faites-le précéder de **Softwarecenter:SoftwareID=** . À l’aide de l’exemple ci-dessus, le lien final ressemble à ceci : **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Les utilisateurs finaux peuvent utiliser ce lien pour ouvrir directement le Centre logiciel à l’application spécifiée.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Certificats PFX pour les ordinateurs clients Configuration Manager exécutant Windows

Vous pouvez désormais déployer des profils de certificat PFX importés dans des ordinateurs clients Configuration Manager exécutant Windows 10.

### <a name="try-it-out"></a>Essayer

Suivez les instructions fournies dans [Comment créer des profils de certificat PFX](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) pour importer un profil PFX, le déployer et vérifier si le certificat a été installé pour l’utilisateur ciblé.



## <a name="configure-azure-services-wizard"></a>Assistant Configuration des services Azure
L’Assistant **Configuration des services Azure** est une nouveauté de la version Technical Preview 1703. Cet Assistant propose une expérience de configuration commune qui remplace les différents flux de travail associés à la configuration des services cloud que vous utilisez avec Configuration Manager. Pour cela, une **application web Azure** fournit les détails de l’abonnement et de la configuration, ce qui vous évite de les entrer chaque fois que vous configurez un nouveau service ou composant Configuration Manager avec Azure.

Dans la version Technical Preview 1703, cet Assistant permet uniquement de configurer le Windows Store pour Entreprises.  Pour configurer d’autres services cloud, effectuez les flux de travail propres à chacun d’eux.

-   Utilisez les informations contenues dans cette rubrique d’aperçu pour remplacer les étapes de configuration de la section [Configurer la synchronisation avec le Windows Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_setup) de la rubrique Current Branch [Gérer les applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-   Pour plus d’informations sur les applications web, consultez [Authentification et autorisation dans Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview) et [Vue d’ensemble des applications web](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Prérequis et planification
Quand vous configurez une connexion entre Configuration Manager et le Windows Store pour Entreprises, vous devez fournir un dossier où le contenu d’application synchronisé à partir du Windows Store sera conservé. Pour vous assurer que ce dossier est sécurisé et que son contenu peut être déployé sur des appareils, vérifiez que les autorisations suivantes sont en place :
-   L’ordinateur sur lequel vous installez le rôle de système de site de point de connexion de service (le site de niveau supérieur dans la hiérarchie) doit disposer d’autorisations en lecture et en écriture sur le dossier que vous avez spécifié lors de l’utilisation du compte **Computer$** .  

-   L’auteur de l’application doit avoir des autorisations en lecture sur le dossier spécifié.  

-   Le compte **Computer$** de chaque ordinateur qui héberge une instance du fournisseur SMS doit être en mesure d’utiliser le dossier spécifié.

Dans Azure Active Directory, inscrivez Configuration Manager comme outil de gestion d’applications web ou d’API web. Vous obtenez un ID de client dont vous aurez besoin par la suite.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Utiliser l’Assistant pour configurer le service cloud Windows Store pour Entreprises

1. Dans la console, accédez à **Administration** > **Présentation** > **Gestion des services cloud** > **Azure** > **Services Azure**, puis choisissez **Configurer les services Azure** pour démarrer l’**Assistant Services Azure**.

2. Dans la page **Services Azure**, sélectionnez le service à configurer, puis cliquez sur **Suivant**. Dans cette préversion, seul le Windows Store pour Entreprises peut être configuré.

3. Dans la page **Général**, entrez un nom convivial comme **Nom du service Azure** ainsi qu’une description facultative, puis cliquez sur **Suivant**.

4. Dans la page **Application**, spécifiez votre environnement Azure, puis cliquez sur **Parcourir** pour ouvrir la fenêtre Server App.

5. Dans la fenêtre **Server App**, sélectionnez l’application serveur à utiliser, puis cliquez sur **OK**.
   Les applications serveur sont des applications web Azure qui contiennent les configurations pour votre compte Azure, notamment l’ID de locataire, l’ID de client et une clé secrète pour les clients. Si vous ne disposez pas d’une application serveur disponible, choisissez l’une des méthodes suivantes :
   - **Créer** : pour créer une application serveur, cliquez sur **Créer**. Fournissez un nom convivial pour l’application et le locataire. Une fois que vous êtes connecté à Azure, Configuration Manager crée l’application web dans Azure, notamment l’ID de client et la clé secrète à utiliser avec l’application web. Ces informations sont ensuite disponibles dans le portail Azure.
   - **Importer** : pour utiliser une application web qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Indiquez un nom convivial pour l’application et le locataire, puis spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir **vérifié** les informations, cliquez sur **OK** pour continuer.  </br></br>

6. Passez en revue la page **Informations**, puis effectuez les étapes et configurations supplémentaires indiquées. Ces configurations sont nécessaires pour utiliser le service avec Configuration Manager.
   Par exemple, pour configurer le Windows Store pour Entreprises :

   1. Dans Azure, vous devez inscrire Configuration Manager comme application web ou API web et enregistrer l’ID de client. Vous devez aussi spécifier une clé de client que doit utiliser l’outil de gestion (c’est-à-dire, Configuration Manager).

   2.    Dans la console Windows Store pour Entreprises, vous devez configurer Configuration Manager comme outil de gestion du magasin, activer la prise en charge pour les applications sous licence en mode hors connexion, puis acheter au moins une application.   </br>

   Cliquez sur **Suivant** quand vous êtes prêt à continuer.

7. Dans la page **Configurations d’application**, configurez le catalogue d’applications et la langue de ce service, puis cliquez sur **Suivant**.
8. Une fois l’Assistant terminé, la console Configuration Manager indique que vous avez configuré **Windows Store pour Entreprises** comme **Type de service cloud**.

Vous pouvez maintenant utiliser le reste du [contenu Current Branch](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) pour synchroniser, créer, déployer et surveiller les applications Windows Store pour Entreprises.

### <a name="modify-a-cloud-service-configuration"></a>Modifier la configuration d’un service cloud
Vous pouvez afficher et réviser les propriétés d’un service cloud pour modifier sa configuration.

Dans la console, accédez à **Administration** > **Présentation** > **Gestion des services cloud** > **Azure** > **Services Azure**, choisissez **Configurer les services Azure**, sélectionnez un service cloud, puis choisissez **Propriétés**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Convertir du BIOS en UEFI pendant une mise à niveau sur place
Windows 10 Creators Update inclut un outil de conversion simple qui automatise le processus de repartitionnement du disque dur pour le matériel compatible UEFI et intègre l’outil de conversion dans le processus de mise à niveau sur place de Windows 7 vers Windows 10. Lorsque vous combinez cet outil avec la séquence de tâches de mise à niveau du système d’exploitation et l’outil OEM qui convertit le microprogramme du BIOS en UEFI, vous pouvez convertir vos ordinateurs du BIOS en UEFI pendant une mise à niveau sur place vers Windows 10 Creators Update. Pour plus d’informations, consultez [Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Groupes de séquences de tâches réductibles
Cette version permet de développer et réduire des groupes de séquences de tâches. Vous pouvez développer ou réduire des groupes individuels ou tous les groupes à la fois.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Paramètres du client pour configurer Windows Analytics pour Upgrade Readiness
À compter de cette version, vous pouvez utiliser les paramètres client d’appareil pour simplifier la configuration des données de télémétrie Windows nécessaires pour utiliser des solutions [Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) comme [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) avec Configuration Manager. Configuration Manager peut récupérer les données de Windows Analytics qui fournissent des informations importantes sur l’état actuel de votre environnement en fonction des données de télémétrie Windows transmises par vos ordinateurs clients. Les données de télémétrie Windows sont transmises par les ordinateurs clients au service de télémétrie Windows, puis les informations pertinentes sont transférées aux solutions Windows Analytics hébergées sur un des espaces de travail OMS de votre organisation. Upgrade Readiness est une solution Windows Analytics qui peut vous aider à hiérarchiser les décisions liées aux mises à niveau de Windows sur vos appareils gérés.

Pour plus d’informations sur les paramètres de télémétrie Windows, consultez [Configurer la télémétrie Windows dans votre organisation](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization).

### <a name="prerequisites"></a>Prérequis
- Vous devez configurer votre site de façon à ce qu’il utilise le service cloud Upgrade Readiness. Pour plus d’informations, consultez [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)

### <a name="configure-windows-analytics-client-settings"></a>Configurer les paramètres client Windows Analytics
Pour configurer Windows Analytics, dans la console Configuration Manager, accédez à **Administration** > **Paramètres client**, double-cliquez sur **Créer des paramètres client d’appareil personnalisés par défaut**, puis sélectionnez **Windows Analytics**.  

Naviguez vers l’onglet des paramètres **Windows Analytics** puis configurez les éléments suivants :
- **ID commercial**  
La clé d’ID commercial mappe les informations des appareils que vous gérez à l’espace de travail OMS qui héberge les données Windows Analytics de votre organisation. Si vous avez déjà configuré une clé d’ID commercial avec Upgrade Readiness, utilisez cet ID. Si vous ne disposez pas encore d’une clé ID commercial, consultez [Générer une clé d’ID commercial]( https://technet.microsoft.com /itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

- Définir un **Niveau de télémétrie pour les appareils Windows 10**   
Pour plus d’informations sur les données collectées par chaque niveau de télémétrie Windows 10, consultez [Configurer la télémétrie Windows dans votre organisation]( https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

- **Participer à la collecte de données commerciales sur les appareils Windows 7, 8 et 8.1**   
Pour plus d’informations sur les données collectées à partir de ces systèmes d’exploitation quand vous choisissez de participer, téléchargez le fichier .pdf [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) disponible sur le site web de Microsoft.

- **Configurer la collecte de données dans Internet Explorer** Sur les appareils exécutant Windows 8.1 ou version antérieure, Internet la collecte de données dans Internet Explorer permet à Upgrade Readiness de détecter les incompatibilités d’application web qui risquent d’empêcher une mise à niveau sans heurts vers Windows 10. La collecte des données dans Internet Explorer peut être activée pour chaque zone internet. Pour plus d’informations sur les zones internet, consultez [À propos des zones de sécurité des URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).
