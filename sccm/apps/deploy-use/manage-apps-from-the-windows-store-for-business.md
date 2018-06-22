---
title: Gérer les applications à partir du Microsoft Store pour Entreprises
titleSuffix: Configuration Manager
description: Gérez et déployez les applications à partir du Microsoft Store pour Entreprises en utilisant System Center Configuration Manager.
ms.date: 12/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4999784140ece9df49a28063e8660566f7206df0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336117"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-system-center-configuration-manager"></a>Gérer les applications à partir du Microsoft Store pour Entreprises avec System Center Configuration Manager
Le [Microsoft Store pour Entreprises](https://www.microsoft.com/business-store) vous donne accès à des applications Windows pour votre organisation que vous pouvez acheter individuellement ou en volume. En connectant le Store à Configuration Manager, vous pouvez synchroniser la liste des applications que vous avez achetées avec Configuration Manager. Vous pouvez ensuite voir ces applications dans la console Configuration Manager et les déployer comme toute autre application.


## <a name="online-and-offline-apps"></a>Applications en ligne et hors connexion

Le Microsoft Store pour Entreprises prend en charge deux types d’applications :

- **En ligne** : ce type de licence exige que les utilisateurs et les appareils se connectent au Windows Store pour obtenir une application et sa licence. Les appareils Windows 10 doivent être joints au domaine Azure Active Directory.
- **Hors connexion** : vous permet de mettre en cache les applications et les licences à déployer directement sur votre réseau local. Les appareils n’ont pas besoin de se connecter au store ou de disposer d’une connexion à Internet.

[Découvrez-en plus](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sur le Microsoft Store pour Entreprises.

Configuration Manager prend en charge la gestion des applications du Microsoft Store pour Entreprises sur les appareils Windows 10 exécutant le client Configuration Manager, ainsi que sur les appareils Windows 10 inscrits auprès de Microsoft Intune. Les fonctionnalités offertes par Configuration Manager pour les applications en ligne et hors connexion sont répertoriées ci-dessous.

> [!IMPORTANT]
> Pour utiliser Microsoft Store pour Entreprises, les appareils Windows 10 doivent exécuter la version de novembre 2015 (1511) ou une version ultérieure.


|Fonctionnalité|Applications hors connexion|Applications en ligne|
|------------|------------|------------|
|Synchronisation des données d’application dans Configuration Manager<br>(la synchronisation a lieu toutes les 24 heures)|Oui|Oui|
|Création d’applications Configuration Manager à partir d’applications du Windows Store|Oui|Oui|
|Prise en charge des applications gratuites du Windows Store|Oui|Oui|
|Prise en charge des applications payantes du Windows Store|Non|Oui<sup>1</sup>|
|Prise en charge des déploiements obligatoires sur les regroupements d’utilisateurs ou d’appareils|Oui|Oui|
|Prise en charge des déploiements disponibles sur les regroupements d’utilisateurs ou d’appareils|Oui|Oui|
|Prise en charge des applications métier à partir du Store|Oui|Oui|

<sup>1</sup>Pour déployer des applications sous licence en ligne sur des PC Windows 10 avec le client Configuration Manager, ces PC doivent exécuter la mise à jour Windows 10 Creators Update ou une version ultérieure.

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Déploiement d’applications en ligne à l’aide du Microsoft Store pour Entreprises avec des PC exécutant le client Configuration Manager
Avant de déployer des applications Microsoft Store pour Entreprise sur des PC exécutant le client Configuration Manager complet, prenez en considération les points suivants :

- Pour bénéficier de fonctionnalités complètes, les PC doivent exécuter la mise à jour Windows 10 Creators Update ou une version ultérieure.
- Les PC doivent être joints à Azure Active Directory et se trouver dans le même locataire que celui où vous avez enregistré le Microsoft Store pour Entreprises comme outil de gestion.
- Quand des PC sont connectés avec le compte administrateur intégré, ils ne peuvent pas accéder aux applications Microsoft Store pour Entreprises.
- Les PC doivent disposer d’une connexion Internet active vers le Microsoft Store pour Entreprises.

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notes concernant les PC exécutant des versions antérieures de Windows 10
Sur les PC exécutant une version de Windows 10 antérieure à la mise à jour Creators Update (avec le client Configuration Manager), les fonctionnalités suivantes s’appliquent :


- En cas d’application de l’installation par l’utilisateur qui installe l’application, si l’application atteint son échéance d’installation ou en cas de réévaluation post-installation des déploiements obligatoires :
    - L’application est « appliquée » quand l’application Microsoft Store pour Entreprises est lancée. 
    - L’utilisateur final doit ensuite effectuer l’installation à partir du Store avant que l’application ne soit installée.
    - Dans la console Configuration Manager, l’état de l’application indique un échec avec l’erreur suivante : « L’application Microsoft Store a été ouverte sur le PC client et attend que l’utilisateur termine l’installation. »
- Au prochain cycle d’évaluation de l’application :
    - Si l’application a été installée par l’utilisateur final à partir du Store, l’application affiche l’état **Réussite**. 
    - Si l’utilisateur final n’a pas essayé d’installer l’application à partir du Store :
        - Les déploiements obligatoires tentent de lancer le Store et de réappliquer l’installation de l’application.
        - Les déploiements disponibles ne sont pas réappliqués.

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>Notes supplémentaires concernant les PC exécutant des versions antérieures de Windows 10 :

- Vous ne pouvez pas déployer d’applications métier à partir du Microsoft Store pour Entreprises
- Lorsque vous déployez des applications payantes à partir du Store, les utilisateurs finaux doivent se connecter au Store et acheter eux-mêmes l’application.
- Si vous déployez une stratégie de groupe pour désactiver l’accès à la version grand public de Microsoft Store, les déploiements à partir du Microsoft Store pour Entreprises ne fonctionnent pas, même si le Microsoft Store pour Entreprises est activé.


## <a name="set-up-microsoft-store-for-business-synchronization"></a>Configurer la synchronisation du Microsoft Store pour Entreprises
La synchronisation de la liste des applications achetées par votre organisation vous permet de voir ces applications dans la console Configuration Manager.

<!-- Remove below after 1802... -->
### <a name="for-configuration-manager-versions-prior-to-1706"></a>Pour les versions de Configuration Manager antérieures à 1706

**Dans Azure Active Directory, inscrivez Configuration Manager en tant qu’outil de gestion « Application web et/ou API web ». Cette action vous donne un ID de client dont vous aurez besoin plus tard.**
1. Dans le nœud Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), sélectionnez votre annuaire Azure Active Directory, puis cliquez sur **Applications** > **Ajouter**.
2.  Cliquez sur **Ajouter une application développée par mon organisation**.
3.  Attribuez un nom à l’application, sélectionnez **Application web** et/ou **API web**, puis cliquez sur la flèche **Suivant**.
4.  Entrez la même URL pour **URL de connexion** et pour **URI ID d’application**. L’URL peut être une chaîne quelconque qui ne doit pas nécessairement correspondre à une adresse réelle. Par exemple, vous pouvez entrer *https://yourdomain/sccm*.
5.  Effectuez toutes les étapes de l'Assistant.

**Dans Azure Active Directory, créez une clé de client pour l’outil de gestion inscrit**.
1.  Sélectionnez l’application que vous venez de créer et cliquez sur **Configurer**.
2.  Sous **Clés**, sélectionnez une durée dans la liste, puis cliquez sur **Enregistrer**. Cette action crée une nouvelle clé de client. Ne quittez pas cette page tant que vous n’avez pas correctement intégré Microsoft Store pour Entreprises à Configuration Manager.

**Dans le Microsoft Store pour Entreprises, configurez Configuration Manager comme outil de gestion du Store**
1.  Ouvrez [https://businessstore.microsoft.com/managementtools](https://businessstore.microsoft.com/managementtools) et connectez-vous si vous y êtes invité.
2.  Acceptez les conditions d’utilisation si cela vous est demandé.
3.  Sous **Outils de gestion**, cliquez sur **Ajouter un outil de gestion**.
4.  Dans **Rechercher l’outil par son nom**, tapez le nom de l’application que vous avez créée précédemment dans AAD, puis cliquez sur **Ajouter**.
5.  Cliquez sur **Activer** en regard de l’application que vous avez importée.
6.  Dans la page **Gérer > Informations de compte**, sélectionnez **Afficher les applications sous licence hors connexion** si vous souhaitez autoriser l’achat d’applications sous licence hors connexion.

**Ajouter le compte Windows Store à Configuration Manager**

1. Vérifiez que vous avez acheté au moins une application dans le Microsoft Store pour Entreprises. Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Microsoft Store pour Entreprises**.
2.  Sous l’onglet **Accueil**, dans le groupe **Microsoft Store pour Entreprises**, cliquez sur **Ajouter un compte Microsoft Store pour Entreprises**. 
3.  Ajoutez vos ID de locataire, ID de client et clé de client à partir d’Azure Active Directory, puis terminez l’Assistant.
4. À la fin de l’opération, le compte apparaît sous **Microsoft Store pour Entreprises** dans la console Configuration Manager.

### <a name="for-configuration-manager-version-1706-and-later"></a>Pour Configuration Manager version 1706 et ultérieures
<!-- ...remove above after 1802 -->

1. Dans la console, accédez à **Administration** > **Services cloud** > **Services Azure**, puis choisissez **Configurer les services Azure** pour démarrer **l’Assistant Services Azure**.
2. Dans la page **Services Azure**, sélectionnez le service à configurer, puis cliquez sur **Suivant**.
3. Dans la page **Général**, entrez un nom convivial comme nom de service Azure et une description facultative, puis cliquez sur **Suivant**.
4. Dans la page **Application**, spécifiez votre environnement Azure, puis cliquez sur **Parcourir** pour ouvrir la fenêtre **Server App**.
5. Dans la fenêtre **Server App**, sélectionnez l’application serveur à utiliser, puis cliquez sur **OK**. Les applications serveur sont des applications web Azure qui contiennent les configurations pour votre compte Azure, notamment l’ID de locataire, l’ID de client et une clé secrète pour les clients. Si vous ne disposez pas d’une application serveur disponible, exécutez l’une des actions suivantes :
    - **Créer** : pour créer une application serveur, cliquez sur **Créer**. Fournissez un nom convivial pour l’application et le locataire. Une fois que vous êtes connecté à Azure, Configuration Manager crée l’application web dans Azure, notamment l’ID de client et la clé secrète à utiliser avec l’application web. Ces valeurs sont ensuite visibles dans le portail Azure.
    - **Importer** : pour utiliser une application web qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Fournissez un nom convivial pour l’application et le locataire. Ensuite, spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir **vérifié** les informations, cliquez sur **OK** pour continuer. 
6. Passez en revue la page **Informations**, puis effectuez les étapes et configurations supplémentaires indiquées. Ces configurations sont nécessaires pour utiliser le service avec Configuration Manager. Par exemple, pour configurer Microsoft Store pour Entreprises :
    - Dans Azure, vous devez inscrire Configuration Manager comme application web ou API web et enregistrer l’ID de client. Vous devez aussi spécifier une clé de client que doit utiliser l’outil de gestion (c’est-à-dire, Configuration Manager).
    - Dans le portail Microsoft Store pour Entreprises, vous devez configurer Configuration Manager comme outil de gestion du Store, activer la prise en charge pour les applications sous licence en mode hors connexion, puis acheter au moins une application. 
7. Cliquez sur **Suivant** quand vous êtes prêt à continuer.
8. Dans la page **Configurations d’application**, configurez le catalogue d’applications et la langue de ce service, puis cliquez sur **Suivant**.
9. Une fois l’Assistant terminé, la console Configuration Manager indique que vous avez configuré **Microsoft Store pour Entreprises** comme **Type de service cloud**.




## <a name="create-and-deploy-a-configuration-manager-application-from-a-microsoft-store-for-business-app"></a>Créer et déployer une application Configuration Manager à partir d’une application du Microsoft Store pour Entreprises
Après la synchronisation, créez et déployez les applications de store comme vous le feriez pour toute autre application.

1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.
2.  Choisissez l’application que vous voulez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une application**.
Une application Configuration Manager contenant l’application du Microsoft Store pour Entreprises est alors créée. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.

> [!IMPORTANT]
> Pour les appareils inscrits auprès de Microsoft Intune, les applications déployées sont uniquement accessibles à l’utilisateur qui est à l’origine de l’inscription de l’appareil. Aucun autre utilisateur ne peut accéder à l’application.

## <a name="next-steps"></a>Étapes suivantes

Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.

Pour chaque application de store que vous gérez, vous pouvez afficher des informations la concernant, notamment le nom, la plateforme et le nombre de licences que vous avez pour l’application, ainsi que le nombre de licences disponibles.

Après le déploiement d’applications en ligne, toute mise à jour de cette application proviendra directement du Microsoft Store. De plus, Configuration Manager ne vérifie pas la compatibilité des versions des applications en ligne. Windows signale simplement l’application comme étant installée.  

Quand vous déployez des applications hors connexion sur des appareils Windows 10 avec le client Configuration Manager, n’autorisez pas les utilisateurs à mettre à jour des applications externes aux déploiements Configuration Manager. Le contrôle des mises à jour des applications hors connexion est particulièrement important dans les environnements multi-utilisateurs tels que les classes. L’une des façons de désactiver le Microsoft Store consiste à utiliser la [stratégie de groupe](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Une fois que l’administrateur Microsoft Store pour entreprises a acheté une application hors connexion, ne publiez pas l’application pour des utilisateurs par le biais du store. Cette configuration garantit que les utilisateurs ne peuvent pas effectuer d’installation ou de mise à jour en ligne. Les utilisateurs recevront uniquement les mises à jour d’applications hors connexion par le biais de Configuration Manager. 
