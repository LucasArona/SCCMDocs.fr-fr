---
title: Capacités de la version Technical Preview 1702
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1702 pour System Center Configuration Manager.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d817bf27302b0a894eb834c747fb3bbcb0ad3fa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56141185"
---
# <a name="capabilities-in-technical-preview-1702-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1702 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*

Cet article présente les fonctionnalités qui sont disponibles dans la version Technical Preview 1702 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Envoyer des commentaires à partir de la console Configuration Manager

Cet aperçu présente de nouvelles options pour les commentaires dans la console Configuration Manager. Les options de commentaires vous permettent d’envoyer vos commentaires directement à l’équipe de développement, par le biais du site web de commentaires Configuration Manager UserVoice.  

> L’option **Commentaires** est accessible :
> -  Dans le ruban, à l’extrême gauche de l’onglet Accueil de chaque nœud.  
>    ![Ruban](./media/feedback-home.png)

-  Quand vous cliquez avec le bouton droit sur n’importe quel objet dans la console.   
    ![Option de clic droit](./media/feedback-option.png)   

Lorsque vous cliquez sur **Commentaires**, le site de commentaires de Configuration Manager UserVoice s’affiche dans votre navigateur, à l’adresse https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Modifications pour les mises à jour et la maintenance
Les éléments suivants sont une nouveauté dans cette préversion.

**Choix de mise à jour plus simples**  
Si votre infrastructure est en droit de recevoir plusieurs mises à jour, seule la dernière mise à jour est téléchargée. Par exemple, si le numéro de version actuel de votre site est inférieur de deux ou plus à la version la plus récente disponible, seule cette dernière version de mise à jour est téléchargée automatiquement.  

Vous pouvez télécharger et installer les autres mises à jour disponibles, même quand il ne s’agit pas de la version la plus récente. Toutefois, vous recevrez un message d’avertissement indiquant que la mise à jour a été remplacée par une version plus récente. Pour télécharger une mise à jour qui est *Disponible en téléchargement*, sélectionnez la mise à jour dans la console, puis cliquez sur **Télécharger**.

**Nettoyage amélioré des anciennes mises à jour**   
Nous avons ajouté une fonction de nettoyage automatique qui supprime les téléchargements inutiles du dossier « EasySetupPayload » sur votre serveur de site.  


## <a name="peer-cache-improvements"></a>Améliorations de Cache d’homologue
À compter de cette version, un ordinateur source de cache d’homologue rejette une demande de contenu quand il remplit l’une des conditions suivantes :  
 -  Il est en mode de batterie faible.
 -  La charge de l’UC dépasse 80 % au moment où le contenu est demandé.
 -  Les E/S disque ont une valeur *AvgDiskQueueLength* supérieure à 10.
 -  Il n’y a plus de connexion disponible vers l’ordinateur.   

Vous pouvez configurer ces paramètres à l’aide de la classe de configuration de l’agent client pour la fonctionnalité de source d’homologue (*SMS_WinPEPeerCacheConfig*) quand vous utilisez le SDK System Center Configuration Manager.

Quand l’ordinateur rejette une demande de contenu, l’ordinateur demandeur continue à rechercher le contenu à partir d’autres sources dans son pool d’emplacements de sources de contenu disponibles.   

## <a name="azurediscovery"></a> Utiliser les services de domaine Azure Active Directory pour gérer des appareils, des utilisateurs et des groupes

Avec cette préversion technique, vous pouvez gérer des appareils qui sont joints à un domaine géré par les services de domaine Azure Active Directory (AD). Vous pouvez également découvrir des appareils, des utilisateurs et des groupes dans ce domaine par le biais de différentes méthodes de découverte dans Configuration Manager.

L’infrastructure de site, les clients et le domaine des Services de domaine Azure Active Directory qui exécutent la préversion technique doivent tous s’exécuter dans Azure.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Configurer Configuration Manager pour utiliser Azure AD
Pour utiliser Azure AD avec Configuration Manager, vous avez besoin des éléments suivants :
-   Un abonnement Azure
-   Azure AD avec les services de domaine
-   Un site Configuration Manager qui s’exécute sur une machine virtuelle Azure jointe à votre domaine Azure AD.
-   Des clients Configuration Manager qui s’exécutent dans le même environnement Azure AD.

Pour configurer les services de domaine Azure Active Directory, consultez [Prise en main des services de domaine Azure AD](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-getting-started).

### <a name="discover-resources"></a>Découvrir les ressources
Après avoir configuré Configuration Manager pour qu’il s’exécute dans Azure AD, vous pouvez appliquer les méthodes de découverte Active Directory suivantes pour rechercher des ressources dans Azure AD :  
- Découverte de systèmes Active Directory
- Découverte d'utilisateurs Active Directory
- Découverte de groupes Active Directory  

Pour chaque méthode utilisée, modifiez la requête LDAP pour rechercher dans les structures d’unités d’organisation Azure Active Directory plutôt que dans les conteneurs typiques d’un annuaire Active Directory local. Vous devez pour cela diriger la requête pour qu’elle effectue des recherches dans votre annuaire Active Directory dans votre abonnement Azure.  

Les exemples suivants utilisent un annuaire Azure AD nommé *contoso.onmicrosoft.com* :
- **Découverte de systèmes**   
  Azure AD stocke les appareils sous l’unité d’organisation **AADDC Computers**.  Configurez ce qui suit :  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **Découverte d’utilisateurs** AAD stocke les utilisateurs sous l’unité d’organisation **AADDC Users**.  Configurez ce qui suit :
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Découverte de groupes**  
Azure AD n’a pas d’unité d’organisation qui stocke des groupes. Au lieu de cela, utilisez la même structure générale que les requêtes Système ou Utilisateur, et configurez la requête LDAP pour qu’elle pointe vers l’unité d’organisation qui contient les groupes que vous souhaitez découvrir.

Pour plus d’informations sur Azure AD, consultez les articles suivants :  
 - [Services de domaine Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds) sur azure.microsoft.com.
 - [Documentation des Services de domaine Active Directory](https://docs.microsoft.com/azure/active-directory-domain-services) sur docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Améliorations apportées aux stratégies de conformité des appareils pour l’accès conditionnel

Une nouvelle règle de stratégie de conformité de l’appareil est disponible pour vous aider à bloquer l’accès aux ressources d’entreprise qui prennent en charge l’accès conditionnel, quand des utilisateurs utilisent des applications qui figurent dans une liste d’applications non conformes. La liste des applications non conformes peut être définie par l’administrateur lors de l’ajout de la nouvelle règle de conformité **Applications qui ne peuvent pas être installées**. Cette règle exige que l’administrateur entre le **Nom de l’application**, l’**ID de l’application** et l’**Éditeur de l’application**  (facultatif) lors de l’ajout d’une application à la liste des applications non conformes. Ce paramètre s’applique uniquement aux appareils iOS et Android.

Cela permet également aux organisations de réduire les fuites de données via des applications non sécurisées, et d’empêcher la consommation excessive de données par certaines applications.

- Consultez cet article pour en savoir plus sur le [fonctionnement des stratégies de conformité des appareils](https://docs.microsoft.com/sccm/protect/deploy-use/device-compliance-policies).
- Consultez cet article pour en savoir plus sur [la façon de créer des stratégies de conformité des appareils](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy).

### <a name="try-it-out"></a>Faîtes un essai

**Scénario :** Identifier les applications susceptibles de provoquer des fuites de données en envoyant des données d’entreprise hors de l’entreprise, ou les applications qui provoquent une consommation excessive de données, puis [créer une stratégie de conformité de l’appareil avec accès conditionnel](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy) qui ajoute ces applications à la liste des applications non conformes. Cela bloquera l’accès aux ressources d’entreprise qui prennent en charge l’accès conditionnel, jusqu’à ce que l’utilisateur puisse supprimer l’application bloquée.

## <a name="antimalware-client-version-alert"></a>Alerte de version du client de logiciel anti-programme malveillant
À compter de cette préversion, Configuration Manager Endpoint Protection fournit une alerte si plus de 20 % (par défaut) des clients gérés utilisent une version du client de logiciel anti-programme malveillant (par exemple Windows Defender ou Endpoint Protection client) qui a expiré.

### <a name="try-it-out"></a>Faîtes un essai
Vérifiez qu’Endpoint Protection est activé sur tous les clients de bureau et serveur à l’aide de la stratégie de paramètres client. Vous pouvez maintenant afficher **Version du client de logiciel anti-programme malveillant** et **État du déploiement d’Endpoint Protection** en accédant à **Actifs et Conformité** > **Vue d’ensemble** > **Appareils** > **Tous les clients bureau et serveur**. Pour vérifier une alerte, affichez **Alertes** dans l’espace de travail **Surveillance**. Si plus de 20 % des clients gérés exécutent une version de logiciel anti-programme malveillant ayant expiré, l’alerte « La version du client de logiciel anti-programme malveillant est obsolète » s’affiche. Cette alerte n’apparaît pas sous l’onglet **Surveillance** > **Vue d’ensemble**. Pour mettre à jour les clients de logiciel anti-programme malveillant ayant expiré, activez les mises à jour logicielles pour les clients de logiciel anti-programme malveillant.

Pour configurer le pourcentage auquel l’alerte est générée, développez **Surveillance** > **Alertes** > **Toutes les alertes**, double-cliquez sur **Clients de logiciel anti-programme malveillant obsolètes** et modifiez l’option **Générez une alerte si le pourcentage de clients gérés avec une version obsolète du client de logiciel anti-programme malveillant est supérieur à**.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Évaluation de la conformité des mises à jour Windows Update for Business
Vous pouvez désormais configurer une règle de mise à jour de stratégie de conformité pour inclure un résultat d’évaluation Windows Update for Business dans le cadre de l’évaluation de l’accès conditionnel.
> [!IMPORTANT]
> Vous devez avoir Windows 10 Insider Preview Build 15019 ou version ultérieure pour pouvoir utiliser l’évaluation de la conformité pour les mises à jour Windows Update for Business.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Autoriser Windows Update for Business à gérer les mises à jour de Windows 10
Pour recueillir des informations d’évaluation de conformité pour les mises à jour Windows Update for Business, appliquez la procédure suivante pour configurer le paramètre d’agent client pour autoriser explicitement Windows Update for Business à gérer les mises à jour de Windows 10.
1. Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client**.
2. Dans les propriétés des paramètres client, accédez à **Mises à jour logicielles**, puis sélectionnez **Oui** pour le paramètre **Gérer les mises à jour de Windows 10 avec Windows Update for Business**.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Créer une stratégie de conformité pour l’évaluation Windows Update for Business
1. Dans la console Configuration Manager, accédez à **Actifs et Conformité** > **Paramètres de conformité** > **Stratégies de conformité**.
2. Cliquez sur **Créer une stratégie de conformité** ou sélectionnez une stratégie de conformité existante à modifier.
3. Dans la page Général, entrez un nom et une description, sélectionnez **Règles de conformité pour les appareils gérés avec le client Configuration Manager**, définissez la gravité de non-conformité pour les rapports, puis cliquez sur **Suivant**.
4. Dans la page Plateformes prises en charge, sélectionnez **Windows 10**, puis cliquez sur **Suivant**.
5. Dans la page Règles, cliquez sur **Nouveau** puis, comme **Condition**, choisissez **Exiger la conformité Windows Update for Business**. Le paramètre **Valeur** prend automatiquement la valeur **True**.

La nouvelle stratégie s'affiche sous le nœud **Stratégies de conformité** de l'espace de travail **Actifs et Conformité** .

### <a name="deploy-a-compliance-policy"></a>Déployer une stratégie de conformité
1. Dans la console Configuration Manager, accédez à **Actifs et Conformité** > **Paramètres de conformité**, puis cliquez sur **Stratégies de conformité**.
2. Sous l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.
3. Dans la boîte de dialogue **Déployer une stratégie de conformité** , cliquez sur **Parcourir** pour sélectionner le regroupement d'utilisateurs pour lesquels déployer la stratégie.
   En outre, vous pouvez sélectionner des options pour générer des alertes quand la stratégie n'est pas conforme et configurer le calendrier selon lequel cette stratégie sera évaluée pour la conformité.
4. Une fois terminé, cliquez sur **OK**.

### <a name="monitor-the-compliance-policy"></a>Analyser la stratégie de conformité
Après avoir créé la stratégie de conformité, vous pouvez surveiller les résultats de conformité dans la console Configuration Manager. Pour plus d’informations, consultez [Surveiller la stratégie de conformité](https://docs.microsoft.com/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Améliorations apportées aux paramètres du Centre logiciel et aux messages de notification pour les séquences de tâches à fort impact
Cette version inclut les améliorations suivantes des paramètres du Centre logiciel et des messages de notification pour les séquences de tâches de déploiement à fort impact :

- Dans les propriétés de la séquence de tâches, vous pouvez maintenant configurer n’importe quelle séquence de tâches, notamment celles non liées au système d’exploitation, comme déploiement à haut risque. Toute séquence de tâches qui remplit certaines conditions est définie automatiquement comme séquence à fort impact. Pour plus d’informations, consultez [Paramètres pour gérer les déploiements à haut risque pour System Center Configuration Manager](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Dans les propriétés de la séquence de tâches, vous pouvez choisir d’utiliser le message de notification par défaut ou créer votre propre message de notification personnalisé pour les déploiements à fort impact.
- Dans les propriétés de la séquence de tâches, vous pouvez configurer les propriétés du Centre logiciel, notamment exiger un redémarrage ou définir la taille de téléchargement de la séquence de tâches et la durée d’exécution estimée.
- Le message de déploiement à fort impact par défaut pour les mises à niveau sur place signale désormais que vos applications, vos données et vos paramètres sont migrés automatiquement. Auparavant, le message par défaut pour toute installation de système d’exploitation indiquait que tous les paramètres, les données et les applications seraient perdues, ce qui était faux pour une mise à niveau sur place.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Définir une séquence de tâches comme séquence de tâches à fort impact
Appliquez la procédure suivante pour définir une séquence de tâches à fort impact.
> [!NOTE]
> Toute séquence de tâches qui remplit certaines conditions est définie automatiquement comme séquence à fort impact. Pour plus d’informations, consultez [Paramètres pour gérer les déploiements à haut risque pour System Center Configuration Manager](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquences de tâches**.
2. Sélectionnez la séquence de tâches à modifier, puis cliquez sur **Propriétés**.
3. Sous l’onglet **Notification utilisateur**, sélectionnez **Il s’agit d’une séquence de tâches avec un impact élevé**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Créer une notification personnalisée pour les déploiements à haut risque
1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquences de tâches**.
2. Sélectionnez la séquence de tâches à modifier, puis cliquez sur **Propriétés**.
3. Sous l’onglet **Notification utilisateur**, sélectionnez **Utiliser du texte personnalisé**.
   > [!NOTE]
   >  Vous pouvez définir le texte de notification utilisateur uniquement quand **Il s’agit d’une séquence de tâches avec un impact élevé** est sélectionné.

4. Configurez les paramètres suivants (maximum 255 caractères pour chaque zone de texte) :

   **Texte du titre de la notification utilisateur :** Spécifie le texte en bleu qui s’affiche sur la notification utilisateur du Centre logiciel. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « Confirmez que vous voulez mettre à niveau le système d’exploitation sur cet ordinateur ».

   **Texte du message de la notification utilisateur :** Trois zones de texte fournissent le corps de la notification personnalisée.
   - Première zone de texte : Spécifie le corps principal du texte, contenant généralement des instructions destinées à l’utilisateur. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « La mise à niveau du système d’exploitation peut prendre un certain temps et entraîner plusieurs redémarrages de votre ordinateur ».
   - Deuxième zone de texte : Spécifie le texte en gras dans le corps principal du texte. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « Cette mise à niveau sur place installe le nouveau système d’exploitation et migre automatiquement vos applications, vos données et vos paramètres ».
   - Troisième zone de texte : Spécifie la dernière ligne de texte sous le texte en gras. Par exemple, dans la notification utilisateur par défaut, cette section contient quelque chose comme « Cliquez sur Installer pour commencer. Sinon, cliquez sur Annuler. ».   

   Supposons que vous configurez la notification personnalisée suivante dans les propriétés.

   ![Notification personnalisée pour une séquence de tâches](./media/user-notification.png)

   Le message de notification suivant s’affiche quand l’utilisateur final ouvre l’installation à partir du Centre logiciel.

   ![Notification personnalisée pour une séquence de tâches](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurer les propriétés du Centre logiciel
Appliquez la procédure suivante pour configurer les détails de la séquence de tâches affichés dans le Centre logiciel. Ces détails sont fournis uniquement à titre d’informations.  
1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Systèmes d’exploitation** > **Séquences de tâches**.
2. Sélectionnez la séquence de tâches à modifier, puis cliquez sur **Propriétés**.
3. Sous l’onglet **Général**, les paramètres suivants du Centre logiciel sont disponibles :
   - **Redémarrage requis** : Indique à l’utilisateur si un redémarrage est nécessaire lors de l’installation.
   - **Taille du téléchargement (Mo)** : Spécifie le nombre de mégaoctets affichés dans le Centre logiciel pour la séquence de tâches.  
   - **Durée d’exécution estimée (minutes)** : Spécifie la durée d’exécution estimée, en minutes, affichée dans le Centre logiciel pour la séquence de tâches.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application

Dans la boîte de dialogue *<deployment type name>* **Propriétés** d’un type de déploiement, sous l’onglet Comportement à l’installation, vous pouvez désormais spécifier un ou plusieurs fichiers exécutables qui, s’ils sont en cours d’exécution, bloqueront l’installation du type de déploiement. L’utilisateur doit fermer le fichier exécutable en cours d’exécution (ou il peut être fermé automatiquement pour les déploiements dont l’objet est défini sur Obligatoire) pour que le type de déploiement puisse être installé.

### <a name="try-it-out"></a>Essayez.

1.  Dans les propriétés d’un type de déploiement Configuration Manager, choisissez l’onglet **Comportement à l’installation**.
2.  Choisissez **Ajouter** pour ajouter un ou plusieurs noms de fichiers exécutables à vérifier. Vous pouvez également ajouter un nom d’affichage pour que les utilisateurs puissent identifier plus facilement les applications dans la liste.
3.  Si l’objet du déploiement sera Obligatoire, dans l’Assistant Déploiement logiciel, vous pouvez éventuellement choisir de **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**.

Si l’application a été déployée en tant que **Disponible** et qu’un utilisateur final tente d’installer une application, il est invité à fermer les fichiers exécutables en cours d’exécution que vous avez spécifiés avant de poursuivre l’installation.

Si l’application a été déployée en tant que **Obligatoire** et que l’option **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement** est sélectionnée, une boîte de dialogue signale à l’utilisateur que les fichiers exécutables que vous avez spécifiés seront fermés automatiquement quand l’installation de l’application arrivera à échéance. Vous pouvez planifier ces boîtes de dialogue dans **Paramètres client** > **Agent ordinateur**. Si vous ne souhaitez pas que l’utilisateur final voit ces messages, sélectionnez **Masquer dans le Centre logiciel et toutes les notifications** sous l’onglet **Expérience utilisateur** des propriétés du déploiement.

Si l’application a été déployée en tant que **Obligatoire** et que l’option **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement** n’est pas sélectionnée, l’installation de l’application échoue si une ou plusieurs des applications spécifiées sont en cours d’exécution.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Créer des certificats PFX avec prise en charge S/MIME

Vous pouvez maintenant créer un profil de certificat PFX qui prend en charge S/MIME, et le déployer sur les utilisateurs.  Ce certificat peut ensuite être utilisé pour le chiffrement et le déchiffrement S/MIME sur tous les appareils que l’utilisateur a inscrits.

En outre, vous pouvez maintenant spécifier plusieurs autorités de certification sur plusieurs rôles de système de site de Point d’enregistrement de certificat, et affecter ensuite les autorités de certification qui traitent les demandes dans le cadre du profil de certificat.

Pour les appareils iOS, vous pouvez associer un profil de certificat PFX à un profil de messagerie et activer le chiffrement S/MIME.  Cela active S/MIME dans le client de messagerie natif sur iOS, et lui associe le certificat de chiffrement S/MIME correct.

Pour plus d’informations sur les certificats dans Configuration Manager, consultez [Présentation des profils de certificat dans System Center Configuration Manager]( https://docs.microsoft.com/sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Nouveaux paramètres de conformité des appareils iOS

Nous avons ajouté de nouveaux paramètres, que vous pouvez utiliser dans les éléments de configuration de vos appareils iOS. Il s’agit de paramètres qui existaient précédemment dans Microsoft Intune dans une configuration autonome et qui sont maintenant disponibles quand vous utilisez Intune avec Configuration Manager. Si vous avez besoin d’aide avec l’un de ces paramètres, consultez [Paramètres de la stratégie d’iOS dans Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/ios-policy-settings-in-microsoft-intune).

- **Synchroniser les données des applications gérées dans iCloud**
- **Handoff pour continuer les activités sur un autre appareil**
- **Partage de photos iCloud**
- **Photothèque iCloud**
- **Faire confiance aux nouveaux créateurs d’applications d’entreprise**
- **Autoriser l’utilisateur à télécharger du contenu indiqué comme étant de la « Littérature érotique » à partir de l’iBooks Store** (mode supervisé uniquement)
- **Obliger les Apple Watch jumelées à utiliser la fonctionnalité Wrist Detect**
- **Mot de passe pour les demandes sortantes AirPlay**
- **Modifier les paramètres de compte** (mode supervisé uniquement)
- **Modifications des paramètres d’utilisation des données mobiles des applications** (mode supervisé uniquement)
- **Effacer tout le contenu et les paramètres** (mode supervisé uniquement)
- **Configurer des restrictions sur l’appareil** (mode supervisé uniquement)
- **Utiliser le jumelage d’hôtes pour contrôler les appareils avec lesquels un appareil iOS peut être jumelé** (mode supervisé uniquement)
- **Installer des profils de configuration et des certificats** (mode supervisé uniquement)
- **Modification du nom d’appareil** (mode supervisé uniquement)
- **Modification du code secret** (mode supervisé uniquement)
- **Jumelage de l’Apple Watch** (mode supervisé uniquement)
- **Modification des paramètres de notification** (mode supervisé uniquement)
- **Modification du papier peint** (mode supervisé uniquement)
- **Modification des paramètres d’envoi des diagnostics** (mode supervisé uniquement)
- **Modification de Bluetooth** (mode supervisé uniquement)
- **AirDrop** (mode supervisé uniquement)
- **Utiliser Siri pour interroger le contenu généré par l’utilisateur à partir d’Internet** (mode supervisé uniquement)
- **Filtre de vulgarité de Siri** (mode supervisé uniquement)
- **Retourner les résultats d’Internet dans la recherche Spotlight** (mode supervisé uniquement)
- **Recherche de définition de mot** (mode supervisé uniquement)
- **Claviers prédictifs** (mode supervisé uniquement)
- **Correction automatique** (mode supervisé uniquement)
- **Vérification orthographique au clavier** (mode supervisé uniquement)
- **Raccourcis clavier** (mode supervisé uniquement) <!--- - **Enterprise app trust settings modification** --->
- **Installation d’applications à l’aide d’Apple Configurator et iTunes uniquement** (mode supervisé uniquement)
- **Téléchargements d’application automatiques** (mode supervisé uniquement)
- **Modifier les paramètres de l’application Localiser mes amis** (mode supervisé uniquement)
- **Accès à l’iBooks Store** (mode supervisé uniquement)
- **Application Messages** (mode supervisé uniquement)
- **Podcasts** (mode supervisé uniquement)
- **Apple Music** (mode supervisé uniquement)
- **iTunes Radio** (mode supervisé uniquement)
- **Apple News** (mode supervisé uniquement)
- **Centre de jeux** (mode supervisé uniquement)
- **Traiter AirDrop comme une destination non gérée**

## <a name="android-for-work-support"></a>Prise en charge d’Android for Work

À compter de la version Technical Preview 1702, vous pouvez lier un compte Google à votre client de gestion des appareils mobiles hybride. Cela vous permet d’effectuer les opérations suivantes :

- Inscrire des [appareils Android pris en charge](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) comme Android for Work, et créer des profils professionnels sur ces appareils inscrits
- Approuver des applications dans le magasin Play for Work, les synchroniser avec la console Configuration Manager, puis les déployer sur les profils professionnels des appareils
- Créer et déployer des éléments de configuration pour configurer des paramètres de mot de passe et de profil professionnel pour les appareils
- Créer et déployer des éléments de stratégie de conformité et des profils d’accès aux ressources pour Android pour les appareils Android for Work comme vous le faites déjà pour les appareils Android
- Effectuer une réinitialisation sélective sur des appareils Android for Work

Quand vous inscrivez un appareil comme Android for Work, cela crée un profil professionnel sur l’appareil qu’Intune peut gérer. Ce profil professionnel existe côte à côte avec le profil personnel sur l’appareil Android. Les utilisateurs peuvent facilement basculer entre les applications de profil professionnel et les applications de profil personnel. Vous ne pouvez pas gérer les éléments dans le profil personnel. Les données et les applications personnelles restent non gérées. Configuration Manager a un contrôle total sur le profil professionnel et son contenu, et peut le supprimer de l’appareil.

Android for Work est une plateforme distincte d’Android, et vous devrez choisir la forme de gestion à utiliser pour les appareils Android qui prennent en charge les profils professionnels.

### <a name="try-it-out"></a>Essayez !
Les sections suivantes décrivent la gestion Android for Work.

#### <a name="enable-android-for-work-management"></a>Activer la gestion Android for Work
1. Créez un compte Google sur https://accounts.google.com/SignUp, que vous utiliserez comme compte d’administrateur Android for Work. Ce compte sera associé à toutes les tâches de gestion Android for Work pour ce locataire Intune. Ce compte Google peut être partagé par les administrateurs qui gèrent des appareils Android. Il s’agit du compte Google utilisé par votre organisation pour gérer et publier des applications dans la console Play for Work. Vous utiliserez ce compte pour approuver les applications dans le magasin Play for Work. Veillez donc à prendre note du nom du compte et du mot de passe.
2. Activez l’inscription Android en liant le compte Google au client Intune géré dans Configuration Manager :
   1. Accédez à **Administration** > **Vue d’ensemble** > **Services Cloud** > **Abonnements Microsoft Intune** et sélectionnez votre abonnement Intune.
   2. Dans le ruban, cliquez sur **Configurer des plateformes** > **Android** et vérifiez que l’option **Activer l’inscription Android** est activée.
   3. Dans le ruban, cliquez sur **Configurer des plateformes** > **Android for Work**.
   4. Dans la boîte de dialogue, cliquez sur **Configurer Android for Work dans la console Intune**. La console Intune s’ouvre dans votre navigateur web.
   5. Utilisez vos informations d’identification d’administrateur Intune pour vous connecter au portail Intune.
   6. Cliquez sur **Configurer** pour ouvrir le site web Android for Work de Google Play.
   7. Dans la page de connexion de Google, entrez les informations d’identification du compte Google de l’étape 1, puis fournissez les informations relatives à votre société.
3. Quand vous revenez au portail Intune, Android for Work est activé et vous avez trois options d’inscription pour les appareils Android for Work :
   - **Gérer tous les appareils comme Android** - (Désactivé) Tous les appareils Android, notamment ceux qui prennent en charge Android for Work, sont inscrits comme appareils Android conventionnels.
   - **Gérer les appareils pris en charge comme Android for Work** - (Activé) Tous les appareils qui prennent en charge Android for Work sont inscrits comme appareils Android for Work. Tout appareil Android qui ne prend pas en charge Android for Work est inscrit comme appareil Android conventionnel.
   - **Gérer les appareils pris en charge pour les utilisateurs uniquement dans ces groupes comme Android for Work** - (Test) Vous permet de cibler la gestion Android for Work à un ensemble limité d’utilisateurs. Seuls les membres des groupes sélectionnés qui inscrivent un appareil qui prend en charge Android for Work sont inscrits comme appareils Android for Work. Tous les autres sont inscrits comme appareils Android.
  
> [!NOTE]
> Un problème connu empêche le bon fonctionnement de l’option **Gérer les appareils pris en charge pour les utilisateurs uniquement dans ces groupes comme Android for Work**. Les appareils des utilisateurs dans les groupes Azure AD spécifiés sont inscrits en tant qu’appareils Android et non en tant qu’appareils Android for Work. Pour tester Android for Work, vous devez utiliser **Gérer les appareils pris en charge comme Android for Work**.


  Pour activer l’inscription Android for Work, vous devez choisir la deuxième ou la troisième option. L’option **Gérer les appareils pris en charge pour les utilisateurs uniquement dans ces groupes comme Android for Work** exige que vous configuriez d’abord des groupes de sécurité Azure Active Directory.

Vous verrez le nom du compte et le nom de l’organisation dans le portail Intune une fois la liaison établie. À ce stade, vous pouvez fermer les deux navigateurs.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Approuver et déployer des applications Android for Work
Effectuez les étapes suivantes pour approuver des applications dans le magasin Play for Work, les synchroniser avec la console Configuration Manager et les déployer sur des appareils Android for Work gérés. Pour déployer des applications sur les profils professionnels des utilisateurs, vous devez approuver les applications dans Play for Work, puis les synchroniser avec la console Configuration Manager.

1. Ouvrez un navigateur et accédez à : https://play.google.com/work.
2. Connectez-vous à l’aide du compte d’administrateur Google que vous avez lié à votre client Intune.
3. Recherchez les applications que vous souhaitez déployer dans votre environnement et cliquez sur **Approuver** pour chacune d’elles.
4. Dans la console Configuration Manager, accédez à **Administrateur** > **Vue d’ensemble** > **Services Cloud** > **Android for Work** et cliquez sur **Synchroniser**.
5. Patientez jusqu’à 10 minutes que les applications soient synchronisées, puis accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des applications** > **Informations de licence pour les applications du Store**.
6. Cliquez sur une application synchronisée à partir de Play for Work, puis cliquez sur **Créer une application**.
7. Terminez l’Assistant, puis cliquez sur **Fermer**.
8. Accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des applications** > **Applications**, sélectionnez une application Android for Work et déployez-la normalement.

Pour synchroniser des applications Play for Work avec Configuration Manager, vous devez approuver au moins une application sur le site web Play for Work.

#### <a name="enroll-an-android-for-work-device"></a>Inscrire un appareil Android for Work
L’inscription des appareils Android for Work est similaire à celles des appareils Android. Téléchargez et exécutez l’application Portail d’entreprise pour Android sur votre appareil mobile. Vous serez invité à créer un profil professionnel dans le cadre du processus d’inscription.  Une fois le profil professionnel créé, vous devez basculer vers la version gérée du portail d’entreprise. Le portail d’entreprise géré est marqué d’un petit porte-documents orange dans le coin inférieur droit.

#### <a name="create-and-deploy-a-configuration-item"></a>Créer et déployer un élément de configuration
Android for Work a deux groupes de paramètres pour les éléments de configuration :
- Mot de passe
- Profil professionnel

Vous pouvez configurer le partage de contenu entre les profils professionnels, ainsi que les éléments de configuration suivants sur les appareils exécutant Android 6 ou version ultérieure :
- Le comportement des applications qui demandent des autorisations spécifiques
- Si les notifications pour les applications dans le profil professionnel sont visibles dans l’écran de verrouillage

Pour essayer cela, créez un élément de configuration par l’intermédiaire du flux de travail standard, choisissez **Android for Work** dans la page **Général** et configurez les paramètres pour chacun des groupes de paramètres, en ajoutant l’élément de configuration à une base de référence et en procédant au déploiement normalement. Ces paramètres s’appliqueront uniquement aux appareils inscrits comme Android for Work, et pas à ceux inscrits comme Android.

#### <a name="perform-selective-wipe"></a>Effectuer une réinitialisation sélective
Les appareils inscrits comme Android for Work peuvent uniquement être réinitialisés de manière sélective, car vous gérez uniquement le profil professionnel. Cela empêche que le profil personnel ne soit réinitialisé. La réinitialisation sélective sur un appareil Android for Work supprime le profil professionnel, notamment toutes les applications et données, et désinscrit l’appareil.

Pour effectuer une réinitialisation sélective d’un appareil Android for Work, appliquez le [processus de réinitialisation sélective](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) normal dans la console Configuration Manager.

#### <a name="known-issues-for-android-for-work"></a>Problèmes connus liés à Android for Work
**Échec du déploiement des profils e-mail Android for Work à la suite de la configuration d’une planification de la synchronisation** L’interface utilisateur de Configuration Manager pour les profils e-mail Android for Work comprend une option « Planification ». Sur d’autres plateformes, cette option permet à l’administrateur de configurer une planification pour synchroniser les e-mails et les autres données de comptes e-mail avec les appareils mobiles ciblés par le déploiement. Toutefois, cette option ne fonctionne pas pour les profils e-mail Android for Work. Si vous sélectionnez une option autre que « Non configuré », tout déploiement du profil sur un appareil échoue.
