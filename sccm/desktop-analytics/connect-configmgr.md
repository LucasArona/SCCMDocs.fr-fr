---
title: Connecter le Gestionnaire de configuration
titleSuffix: Configuration Manager
description: Guide pratique pour la connexion de Configuration Manager avec l’Analytique de bureau.
ms.date: 06/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bdfed49a68963dc0d46a38810f0ac9dc8041d3fc
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/13/2019
ms.locfileid: "67038782"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Comment connecter Configuration Manager avec l’Analytique de bureau

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Analytique de bureau est étroitement intégré avec Configuration Manager. Tout d’abord, assurez-vous que le site est à jour pour prendre en charge des fonctionnalités les plus récentes. Puis créez la connexion de bureau Analytique dans Configuration Manager. Enfin, surveiller l’intégrité de la connexion.


## <a name="bkmk_hotfix"></a> Mettre à jour le site

Tout d’abord, assurez-vous que votre site Configuration Manager est en cours d’exécution au moins la version 1902. Pour plus d’informations, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates).

Vous devez également installer la version 1902 correctif cumulatif (4500571) pour prendre en charge l’intégration avec l’Analytique de bureau. Pour plus d’informations sur cette mise à jour, consultez [correctif cumulatif pour Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4500571).

1. Mettre à jour le site avec le correctif cumulatif pour version 1902. Pour plus d’informations, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates).  

2. Mettre à jour des clients. Pour simplifier ce processus, envisagez d’utiliser la mise à niveau automatique des clients. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Se connecter au service

Utilisez cette procédure pour connecter Configuration Manager à l’Analytique de bureau et configurer les paramètres de l’appareil. Cette procédure est un processus unique pour attacher votre hiérarchie vers le service cloud.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**. Sélectionnez **configurer les Services Azure** dans le ruban.  

2. Sur le **Azure Services** page de l’Assistant Services Azure, configurez les paramètres suivants :  

    - Spécifiez un **Nom** pour l’objet dans Configuration Manager.  

    - Spécifiez une **Description** facultative pour vous aider à identifier le service.  

    - Sélectionnez **Desktop Analytique** dans la liste des services disponibles.  
  
   Sélectionnez **Suivant**.  

3. Sur le **application** page, sélectionnez l’option appropriée **environnement Azure**. Puis sélectionnez **Parcourir** pour l’application web.  

4. Si vous avez une application existante que vous souhaitez réutiliser pour ce service, choisissez-le dans la liste, puis sélectionnez **OK**.  

5. Dans la plupart des cas, vous pouvez créer une application pour la connexion de bureau Analytique avec cet Assistant. Sélectionnez **créer**.<!-- 3572123 -->  

    > [!Tip]  
    > Si vous ne pouvez pas créer l’application à partir de cet Assistant, vous pouvez créer manuellement l’application dans Azure AD et ensuite importer dans Configuration Manager. Pour plus d’informations, consultez [application de créer et d’importation pour le Gestionnaire de Configuration](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager).  

6. Configurez les paramètres suivants dans le **créer une Application serveur** fenêtre :  

    - **Nom de l'application** : Un nom convivial pour l’application dans Azure AD.

    - **URL de la page d'accueil** : cette valeur n’est pas utilisée par Configuration Manager, mais elle est exigée par Azure AD. Par défaut, cette valeur est `https://ConfigMgrService`.  

    - **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Il est dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est `https://ConfigMgrService`.  

    - **Période de validité de la clé secrète** : choisissez **1 an** ou **2 ans** dans la liste déroulante. Un an est la valeur par défaut.  

    Sélectionnez **connectez-vous** . Après vous être authentifié correctement auprès d’Azure, la page affiche le **Nom du locataire Azure AD** pour référence.
        
    > [!Note]  
    > Effectuez cette étape en tant qu’un **administrateur d’entreprise**. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure.  

    Sélectionnez **OK** pour créer l’application web dans Azure AD et fermer la boîte de dialogue Créer une application serveur. Dans la boîte de dialogue application serveur, sélectionnez **OK**. Puis sélectionnez **suivant** sur la page application de l’Assistant Services Azure.  

7. Sur le **données de Diagnostic** page, configurez les paramètres suivants :  

    - **ID commercial**: cette valeur doit remplir automatiquement avec l’ID de. votre organisation Si elle ne, assurez-vous que votre serveur proxy est configuré pour autoriser toutes les [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints) avant de continuer. Vous pouvez également récupérer votre ID Commercial manuellement à partir de la [portail d’Analytique de bureau](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).  

    - **Niveau de données de diagnostic de Windows 10**: sélectionnez au moins **base**. Consultez [niveaux de données de Diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **Autoriser le nom de l’appareil dans les données de diagnostic**: sélectionnez **activer**  

        > [!Note]  
        > À compter de Windows 10 version 1803, le nom de l’appareil n’est pas envoyé à Microsoft par défaut. Si vous n’envoyez pas le nom du périphérique, il apparaît dans l’Analytique de bureau comme « Inconnu ». Ce comportement peut rendre difficile d’identifier et évaluer les appareils.  

   Sélectionnez **Suivant**. Le **fonctionnalités disponibles** page affiche les fonctionnalités d’Analytique de bureau qui sont disponibles avec les paramètres de données de diagnostic à partir de la page précédente. Sélectionnez **suivant** pour continuer ou **précédent** pour apporter des modifications.  

    ![Exemple de page de fonctionnalités disponibles dans l’Assistant Services Azure](media/available-functionality.png)

8. Sur le **Collections** page, configurez les paramètres suivants :  

    - **Nom complet** : Le portail d’Analytique de bureau affiche cette connexion de Configuration Manager à l’aide de ce nom. Il permet de faire la distinction entre des hiérarchies différentes. Par exemple, *laboratoire de test* ou *production*.  

    - **Regroupement cible**: Cette collection inclut tous les appareils Configuration Manager configure avec votre ID commercial et les paramètres de données de diagnostic. Il est l’ensemble des appareils Configuration Manager se connecte au service d’Analytique de bureau.  

    - **Appareils du regroupement cible utilisent un proxy authentifié par l’utilisateur pour les communications sortantes**: Par défaut, cette valeur est **non**. Si nécessaire dans votre environnement, la valeur est **Oui**.  

    - **Sélectionner des regroupements spécifiques pour se synchroniser avec le bureau Analytique**: Sélectionnez **ajouter** pour inclure des collections supplémentaires à partir de votre **regroupement cible** hiérarchie. Ces collections sont disponibles dans le portail d’Analytique de bureau pour le regroupement des plans de déploiement. Veillez à inclure les collections d’exclusion de pilote et de pilote.  <!-- 4097528 -->  

        > [!Important]  
        > Ces collections continuent à synchroniser en tant que leurs changements d’appartenance. Par exemple, votre plan de déploiement utilise une collection avec une règle d’adhésion de Windows 7. Comme ces appareils mise à niveau vers Windows 10 et Configuration Manager évalue l’appartenance au regroupement, ces appareils déposent hors de la collecte et le plan de déploiement.  


9. Effectuez toutes les étapes de l'Assistant.  

Configuration Manager crée une stratégie de paramètres pour configurer les appareils du regroupement cible. Cette stratégie inclut les paramètres de données de diagnostic pour permettre aux appareils d’envoyer des données à Microsoft. Par défaut, les clients de mettre à jour stratégie toutes les heures. Après avoir reçu les nouveaux paramètres, il peut être plus de plusieurs heures avant que les données sont disponibles dans l’Analytique de bureau.



## <a name="bkmk_monitor"></a> Surveiller l’intégrité de la connexion

Surveiller la configuration de vos appareils pour l’Analytique de bureau. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Desktop Analytique maintenance** nœud, puis sélectionnez le **intégrité de la connexion** tableau de bord.  

Pour plus d’informations, consultez [surveiller l’intégrité de la connexion](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager synchronise vos collections dans les 60 minutes de la création de la connexion. Dans le portail d’Analytique de bureau, accédez à **pilote Global**et consultez vos regroupements de périphériques de Configuration Manager.



## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour inscrire des appareils pour l’Analytique de bureau.
> [!div class="nextstepaction"]  
> [Inscrire des appareils](/sccm/desktop-analytics/enroll-devices)  
