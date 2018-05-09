---
title: Lier des utilisateurs et des périphériques avec l’affinité entre utilisateur et périphérique
titleSuffix: Configuration Manager
description: Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil et déployez automatiquement des applications sur tous les appareils associés à un utilisateur.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 40bab1725b074bc549eeb9e9764ab8a1dd8b83e7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="link-users-and-devices-with-user-device-affinity-in-system-center-configuration-manager"></a>Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’affinité entre utilisateur et appareil dans System Center Configuration Manager (Configuration Manager) associe un utilisateur à un ou plusieurs appareils. Vous n’avez alors pas besoin de connaître les noms des appareils d’un utilisateur pour déployer une application sur cet utilisateur. Au lieu de déployer l’application sur chacun des appareils de l’utilisateur, vous déployez l’application auprès de l’utilisateur. Ensuite, l’affinité entre utilisateur et appareil entraîne l’installation automatique de l’application sur tous les appareils associés à cet utilisateur.  

 Vous pouvez définir des appareils principaux, qui sont généralement les appareils utilisés quotidiennement par les utilisateurs pour effectuer leur travail. Quand vous créez une affinité entre un utilisateur et un appareil, vous profitez d’un plus grand nombre d’options de déploiement d’applications. Par exemple, si un utilisateur requiert Microsoft Visio, vous pouvez l'installer sur le périphérique principal de l'utilisateur à l'aide d'un déploiement Windows Installer. Toutefois, sur un appareil qui n’est pas un appareil principal, vous pouvez déployer Visio sous forme d’application virtuelle. Vous pouvez également utiliser l’affinité entre utilisateur et appareil pour prédéployer des logiciels sur l’appareil d’un utilisateur quand celui-ci n’est pas connecté pour que, dès que l’utilisateur se connecte, l’application soit déjà installée et prête à être utilisée.  

 Vous devez gérer les informations d'affinité entre appareil et utilisateur pour les ordinateurs. Configuration Manager gère automatiquement les affinités entre utilisateurs et appareils pour les appareils mobiles inscrits.  

## <a name="manually-set-up-user-device-affinity"></a>Configurer manuellement l’affinité entre utilisateur et appareil  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Appareils**.  

3.  Sélectionnez un appareil dans la liste. Sous l’onglet **Accueil**, dans le groupe **Appareil**, choisissez **Modifier les utilisateurs principaux**.  

4.  Dans la boîte de dialogue **Modifier les utilisateurs principaux**, recherchez et sélectionnez les utilisateurs que vous souhaitez ajouter en tant qu’utilisateurs principaux pour l’appareil sélectionné. Choisissez **Ajouter**.  

    > [!NOTE]  
    > La liste **Utilisateurs principaux** indique quels utilisateurs sont déjà les utilisateurs principaux de cet appareil, ainsi que la méthode par laquelle la relation entre utilisateur et appareil a été attribuée.  

## <a name="set-up-primary-devices-for-a-user"></a>Configurer les appareils principaux pour un utilisateur  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Utilisateurs**.  

3.  Sélectionnez un utilisateur dans la liste. Ensuite, sous l’onglet **Appareil**, choisissez **Modifier les appareils principaux**.  

4.  Dans la boîte de dialogue **Modifier les appareils principaux**, recherchez et sélectionnez les appareils que vous souhaitez ajouter en tant qu’appareils principaux pour l’utilisateur sélectionné. Choisissez **Ajouter**.  

    > [!NOTE]  
    > La liste **Appareils principaux** indique quels appareils sont déjà configurés en tant qu’appareils principaux pour cet utilisateur, ainsi que la méthode par laquelle la relation entre utilisateur et appareil a été attribuée.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Créer automatiquement des affinités entre utilisateur et appareil (ordinateurs Windows uniquement)  
 Configuration Manager lit les données sur les ouvertures de session des utilisateurs dans le journal des événements Windows. Pour créer automatiquement des affinités entre des utilisateurs et des appareils, vous devez activer les deux options suivantes dans la stratégie de sécurité locale des ordinateurs clients, afin de stocker les événements d’ouverture de session dans le journal des événements Windows :  

-   **Auditer les événements d'ouverture de session de compte**  
-   **Auditer les événements d'ouverture de session**  

 Pour configurer ces paramètres, utilisez la stratégie de groupe Windows.  

> [!IMPORTANT]  
> Si une erreur provoque l’ajout d’un nombre important d’entrées au journal des événements Windows, il se peut qu’un autre journal des événements soit créé. Dans ce cas, Configuration Manager risque de ne plus pouvoir accéder aux événements d'ouverture de session existants.  
>   
> Soyez prudent lors de l’activation des paramètres **Auditer les événements de connexion aux comptes** et **Auditer les événements de connexion** dans Windows XP. Par défaut, la stratégie de rétention est de 7 jours et il est très probable que ces événements remplissent le journal des événements de sécurité. Les utilisateurs standard ne pourront pas se connecter si le journal des événements est plein. Pour éviter ce problème pour le journal des événements de sécurité, affectez à la stratégie **Méthode de conservation** la valeur **Remplacer les événements si nécessaire**. Pour autoriser des données suffisantes pour l’affinité entre utilisateur et appareil, affectez également à la stratégie de taille maximale du journal des événements de sécurité une valeur raisonnable, par exemple 5 à 20 Mo.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Configurer le site pour créer automatiquement des affinités entre utilisateur et appareil  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client**.  

2.  Pour modifier les paramètres du client par défaut, sélectionnez **Paramètres client par défaut** puis, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**. Pour créer des paramètres de l’agent du client personnalisés, sélectionnez le nœud **Paramètres du client** puis, sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer des paramètres de périphérique client personnalisés**.  

    > [!NOTE]  
    > Si vous modifiez les paramètres client par défaut, ils seront déployés sur tous les ordinateurs de la hiérarchie. Pour plus d'informations sur la configuration des paramètres client, voir [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

3.  Pour **Affinité entre utilisateur et périphérique**, définissez les éléments suivants :  

    -   **User device affinity threshold (minutes)** (Seuil de l’affinité entre utilisateur et appareil (minutes)). Définissez une période (en minutes) pendant laquelle l’appareil est utilisé avant la création d’une affinité entre utilisateur et appareil.  

    -   **User device affinity threshold (days)** (Seuil de l’affinité entre utilisateur et appareil (jours)). Définissez une période (en jours) pendant laquelle le seuil de l’affinité basé sur l’utilisation est mesuré.  

    -   **Configurer automatiquement l’affinité entre utilisateur et appareil à partir des données d’utilisation**. Pour laisser le site créer automatiquement des affinités entre utilisateur et appareil, sélectionnez **True** dans la liste déroulante. Si vous sélectionnez **False**, vous devez approuver toutes les attributions d’affinité entre utilisateur et appareil.  

    > [!TIP]  
    > **Exemple** : si vous affectez à **User device affinity threshold (minutes)** (Seuil de l’affinité entre utilisateur et appareil (minutes)) la valeur **60** minutes et à **User device affinity threshold (days)** (Seuil de l’affinité entre utilisateur et appareil (jours)) la valeur **5** jours, l’utilisateur doit utiliser l’appareil pendant au moins 60 minutes sur une période de 5 jours pour qu’une affinité entre utilisateur et appareil puisse être automatiquement créée.  

Après la création automatique d'une affinité entre utilisateur et appareil, Configuration Manager continue de surveiller les seuils d'affinité entre utilisateur et appareil. Si l’activité de l’utilisateur pour cet appareil devient inférieure aux seuils configurés, l’affinité entre utilisateur et appareil est supprimée. Affectez à **User device affinity threshold (days)** (Seuil de l’affinité entre utilisateur et appareil (jours)) une valeur d’au moins **7** jours pour éviter la suppression d’une affinité entre utilisateur et appareil automatiquement configurée quand l’utilisateur n’est pas connecté, par exemple pendant le week-end.  

## <a name="import-user-device-affinities-from-a-file"></a>Importer des affinités entre utilisateur et périphérique à partir d’un fichier  
 Pour créer plusieurs relations simultanément, vous pouvez importer un fichier contenant les détails des affinités entre des utilisateurs et des appareils. Pour que cette procédure fonctionne, les appareils concernés doivent avoir été découverts et faire partie des ressources de la base de données Configuration Manager.  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Utilisateurs** ou **Appareils**.  

2.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Importer une affinité entre utilisateur et périphérique**.  

3.  Dans l’Assistant Importation d’affinités entre utilisateur et périphérique, dans la page **Choisir un mappage**, définissez ce qui suit :  

    -   **Nom du fichier**. Spécifiez un fichier de valeurs séparées par des virgules (CSV) contenant une liste d’utilisateurs et d’appareils entre lesquels vous souhaitez créer une affinité. Dans ce fichier, chaque paire utilisateur-appareil doit se trouver sur sa propre ligne, avec les valeurs séparées par une virgule. Utilisez le format <*Domaine*>&#92;<*nom_utilisateur*>,<*nom_NetBIOS_appareil*>.  

    -   **Ce fichier contient des en-têtes de colonnes à titre de référence**. Si le fichier .csv présente un en-tête sur la ligne supérieure, sélectionnez cette option pour ignorer cette ligne lors de l’importation.  

4.  Si le fichier que vous importez comporte plus de deux éléments sur chaque ligne, vous pouvez utiliser les commandes **Colonne** et **Attribuer** pour indiquer quelles colonnes représentent les utilisateurs et les appareils, et quelles colonnes doivent être ignorées lors de l’importation.  

5.  Choisissez **Suivant** et terminez l’Assistant Importation d’affinités entre utilisateur et périphérique.  

## <a name="let-users-create-their-own-device-affinities"></a>Laisser les utilisateurs créer leurs propres affinités entre utilisateurs et appareils  
 Utilisez les procédures suivantes afin de configurer un utilisateur pour qu’il crée sa propre affinité entre utilisateur et appareil dans l’application du Centre logiciel.  

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Configurer le site de façon à autoriser les demandes d’affinité entre utilisateur et appareil créées par l’utilisateur  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres du client**.  

2.  Pour modifier les paramètres du client par défaut, sélectionnez **Paramètres client par défaut** puis, sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**. Pour créer des paramètres de l’agent du client personnalisés, sélectionnez le nœud **Paramètres du client** puis, sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer des paramètres utilisateur client personnalisés**.  

    > [!NOTE]  
    > Si vous modifiez les paramètres client par défaut, ils seront déployés sur tous les ordinateurs de la hiérarchie. Pour plus d’informations sur la configuration des paramètres client, voir [Configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).  

3.  Sélectionnez le paramètre client **Affinité entre utilisateur et périphérique** puis, dans la liste déroulante **Autoriser les utilisateurs à définir leurs périphériques principaux** , sélectionnez **Vrai**.  

### <a name="set-up-a-user-device-affinity"></a>Configurer une affinité entre utilisateur et appareil  

1.  Dans le catalogue d’applications, choisissez **Mes systèmes**.  

2.  Sélectionnez l’option **J’utilise régulièrement cet ordinateur pour faire mon travail**.  

## <a name="manage-user-device-affinity-requests-from-users"></a>Gérer les demandes d’affinité entre utilisateur et périphérique faites par les utilisateurs  
 Quand le paramètre client **Configurer automatiquement l’affinité entre utilisateur et périphérique à partir des données d’utilisation** est défini sur **Faux**, vous devez approuver toutes les attributions d’affinité entre utilisateur et périphérique.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Pour approuver ou refuser une demande d’affinité entre utilisateur et appareil  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , sélectionnez le regroupement d'utilisateurs ou d'appareils dont vous souhaitez gérer les demandes d'affinité.  

3.  Sous l’onglet **Accueil**, dans le groupe **Regroupement**, choisissez **Gérer les demandes d’affinité**.  

4.  Dans la boîte de dialogue **Gérer les demandes d’affinité entre périphérique et utilisateur**, sélectionnez une demande d’affinité, puis choisissez **Approuver** ou **Refuser**.  
