---
title: Gérer l'accès à la messagerie
titleSuffix: Configuration Manager
description: Apprenez à utiliser l’accès conditionnel System Center Configuration Manager pour gérer l’accès à la messagerie Exchange.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52785e1f432e1a18d1e8264dc2c78134af9f006e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-email-access-in-system-center-configuration-manager"></a>Gérer l’accès à la messagerie dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’accès conditionnel System Center Configuration Manager permet de gérer l’accès à la messagerie Exchange selon les conditions que vous spécifiez.  

Vous pouvez gérer l'accès à :  

-   Microsoft Exchange sur site  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated

Vous pouvez contrôler l'accès à Exchange Online et Exchange sur site à partir du client de messagerie intégré sur les plateformes suivantes :  

-   Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur  

-   iOS 9.0 et ultérieur  

-   Windows Phone 8.1 et versions ultérieures  

-   Application de messagerie sur Windows 8.1 et versions ultérieures

Les applications de bureau Office peuvent accéder à Exchange Online sur les PC exécutant :  

-   Office 2013 et ultérieur pour ordinateur avec [l’authentification moderne](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) activée.  

-   Windows 7.0 ou Windows 8.1  

> [!NOTE]  
>  Les PC doivent être joints au domaine ou être conformes aux stratégies définies dans Intune.  


## <a name="device-requirements"></a>Exigences relatives aux appareils
 Si vous configurez l'accès conditionnel, l'appareil dont l'utilisateur se sert pour se connecter à sa messagerie doit :  

-   Être inscrit auprès d’Intune ou d’un PC joint à un domaine.  

-   Inscrire l’appareil dans Azure Active Directory. Ceci se fait automatiquement quand l’appareil est inscrit auprès d’Intune (pour Exchange Online uniquement). Par ailleurs, l'ID Exchange ActiveSync du client doit être inscrite auprès d'Azure Active Directory (ceci ne s'applique pas aux appareils Windows et Windows Phone se connectant à Exchange sur site).  

     Pour un PC joint à un domaine, vous devez le configurer de manière à ce qu'il s'inscrive automatiquement auprès d'Azure Active Directory.  La section **Accès conditionnel pour les PC** de la rubrique [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md) répertorie l’ensemble des conditions requises pour activer l’accès conditionnel pour les PC.  

-   Être conforme à toutes les stratégies de conformité Configuration Manager déployées sur cet appareil.  

 Si une condition d'accès conditionnel n'est pas remplie, l'utilisateur reçoit un des messages suivants quand il se connecte :  

-   Si l’appareil n’est pas inscrit auprès d’Intune ou qu’il n’est pas energistré dans Azure Active Directory, l’utilisateur reçoit un message contenant des instructions pour installer l’application Portail d’entreprise, inscrire l’appareil et, pour les appareils Android et iOS, activer la messagerie, ce qui entraîne l’association de l’ID Exchange ActiveSync de l’appareil à l’enregistrement de l’appareil dans Azure Active Directory.  

-   Si l’appareil n’est pas conforme, l’utilisateur reçoit un message le dirigeant vers le portail web Intune, où il peut trouver des informations sur le problème et des solutions pour y remédier.  

**Pour les appareils mobiles :**

Vous pouvez restreindre l’accès à **Outlook Web Access (OWA)** sur Exchange Online par le biais d’un navigateur sur des appareils **iOS** et **Android** .  L’accès sera autorisé uniquement à partir des navigateurs pris en charge sur les appareils compatibles :

* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS et Android)

Les navigateurs non pris en charge seront bloqués. Les applications OWA pour iOS et Android ne sont pas prises en charge.  Elles doivent être bloquées par les règles de revendications AD FS :
* Configurez des règles de revendications AD FS pour bloquer les protocoles autres que l'authentification moderne. Des instructions détaillées sont fournies dans le scénario 3 : [bloquer tout accès à Office 365, à l’exception des applications basées sur un navigateur](https://technet.microsoft.com/library/dn592182.aspx).

 **Pour les PC :**  

-   Si l'exigence de la stratégie d'accès conditionnel est d'autoriser la **jonction à un domaine** ou la **conformité**, un message contenant des instructions sur la façon d'inscrire l'appareil s'affiche. Si le PC ne remplit pas l’une des conditions requises, l’utilisateur doit inscrire l’appareil auprès d’Intune.  

-   Si l'exigence de la stratégie d'accès conditionnel est configurée pour autoriser uniquement les appareils Windows joints à un domaine, l'appareil est bloqué et un message invitant l'utilisateur à contacter l'administrateur informatique s'affiche.  

 Vous pouvez bloquer l'accès à la messagerie Exchange à partir du client de messagerie Exchange ActiveSync intégré aux appareils sur les plateformes suivantes :  

-   Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur  

-   iOS 9.0 et ultérieur  

-   Windows Phone 8.1 et versions ultérieures  

-   Application **Courrier** sur Windows 8.1 et versions ultérieures  

 L’application Outlook pour iOS et Android, ainsi que l’application de bureau Outlook 2013 et ultérieur, sont prises en charge uniquement pour Exchange Online.  

 Le **connecteur Exchange local** entre Configuration Manager et Exchange est nécessaire au fonctionnement de l’accès conditionnel.  

 Vous pouvez configurer une stratégie d’accès conditionnel pour Exchange sur site à partir de la console Configuration Manager. Quand vous configurez une stratégie d’accès conditionnel pour Exchange Online, vous pouvez commencer le processus dans la console Configuration Manager, ce qui lance la console Intune, dans laquelle vous pouvez terminer le processus.  

## <a name="configure-conditional-access"></a>Configurer un accès conditionnel
### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Étape 1 : Évaluer l’impact de la stratégie d’accès conditionnel  
 Une fois que vous avez configuré le **connecteur Exchange local**, vous pouvez utiliser le rapport **Liste des appareils par état d’accès conditionnel** de Configuration Manager pour identifier les appareils dont l’accès à Exchange sera bloqué suite à la configuration de la stratégie d’accès conditionnel. Ce rapport requiert également les éléments suivants :  

-   Un abonnement à Intune.  

-   Le point de connexion de service doit être configuré et déployé.  

 Dans les paramètres du rapport, sélectionnez le groupe Intune à évaluer et, si nécessaire, les plateformes d’appareils auxquelles la stratégie doit être appliquée.  

 Pour plus d’informations sur la façon d’exécuter des rapports, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

 Après avoir exécuté le rapport, examinez ces quatre colonnes pour déterminer si un utilisateur sera bloqué :  

-   **Canal de gestion** : indique si l’appareil est géré par Intune, Exchange ActiveSync ou les deux à la fois.  

-   **Inscrit auprès d’AAD** : indique si l’appareil est inscrit auprès d’Azure Active Directory (ce qui s’appelle une « jonction d’espace de travail »).  

-   **Conforme** : indique si l’appareil est conforme aux stratégies de conformité que vous avez déployées.  

-   **EAS activé** : l’ID ActiveSync Exchange des appareils iOS et Android doit être associé à l’enregistrement d’inscription de l’appareil dans Azure Active Directory. Ceci se produit quand l'utilisateur clique sur le lien **Activer la messagerie** dans l'e-mail de mise en quarantaine.  

    > [!NOTE]  
    >  Les appareils Windows Phone affichent toujours une valeur dans cette colonne.  

 Les appareils qui font partie d'un groupe ou d'un regroupement ciblé verront leur accès à Exchange bloqué, sauf si les valeurs de colonne correspondent à celles qui sont répertoriées dans le tableau suivant :  

|Canal de gestion|Enregistré avec AAD|conformité|EAS activé|Action résultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Géré par Microsoft Intune et Exchange ActiveSync**|Oui|Oui|**Oui** ou **Non** s'affiche.|Accès à la messagerie accordé|  
|Toute autre valeur|Non|Non|Aucune valeur affichée|Accès à la messagerie bloqué|  

 Vous pouvez exporter le contenu du rapport et utiliser la colonne **Adresse de messagerie** pour informer les utilisateurs qu'ils ne pourront pas accéder à la messagerie.  

### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Étape 2 : Configurer des groupes ou des regroupements d’utilisateurs pour la stratégie d’accès conditionnel  
 Vous ciblez les stratégies d'accès conditionnel vers différents groupes ou regroupements d'utilisateurs en fonction du type de stratégie. Ces groupes contiennent les utilisateurs qui seront ciblés par la stratégie ou exemptés de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu'il utilise doit être conforme à cette stratégie pour qu'il puisse accéder à la messagerie.  

-   **Stratégie Exchange Online** : cible des groupes de sécurité Azure Active Directory. Vous pouvez configurer ces groupes dans le **Centre d'administration Office 365**ou dans le **Portail de compte Intune**.  

-   **Stratégie Exchange sur site** : cible des regroupements d’utilisateurs Configuration Manager. Vous pouvez les configurer dans l'espace de travail **Ressources et Conformité** .  

 Vous pouvez spécifier deux types de groupes dans chaque stratégie :  

-   **Groupes ciblés** : groupes ou regroupements d’utilisateurs auxquels la stratégie est appliquée.  

-   **Groupes exemptés** : groupes ou regroupements d’utilisateurs exempts de la stratégie (facultatif).  

 Si un utilisateur se trouve dans les deux, il est exempté de la stratégie.  

 Seuls les groupes ou les regroupements qui sont ciblés par la stratégie d'accès conditionnel sont évalués pour l'accès à Exchange.  

### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Étape 3 : Configurer et déployer une stratégie de conformité  
 Vérifiez que vous avez créé et déployé une stratégie de conformité pour tous les appareils qui seront ciblés par la stratégie d'accès conditionnel Exchange.  

 Pour plus d’informations sur la configuration de la stratégie de conformité, consultez [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](device-compliance-policies.md).  

> [!IMPORTANT]  
>  Si vous n'avez pas déployé de stratégie de conformité et que vous activez la stratégie d'accès conditionnel Exchange, l'accès sera autorisé à tous les appareils ciblés.  

 Quand vous êtes prêt, passez à l' **Étape 4**.  

### <a name="step-4-configure-the-conditional-access-policy"></a>Étape 4 : Configurer la stratégie d’accès conditionnel  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Pour Exchange Online (et les locataires dans le nouvel environnement Exchange Online Dedicated)

>[!NOTE]
>Vous pouvez aussi créer une stratégie d’accès conditionnel dans la console de gestion Azure AD. Celle-ci vous permet de créer les stratégies d’accès conditionnel aux appareils (appelées dans Azure AD « stratégies d’accès conditionnel en fonction de l’appareil ») en plus des autres stratégies d’accès conditionnel comme l’authentification multifacteur. Vous pouvez aussi définir des stratégies d’accès conditionnel pour des applications d’entreprise tierces comme Salesforce et Box prises en charge par Azure AD. Pour plus d’informations, consultez [Guide pratique pour définir la stratégie d’accès conditionnel en fonction de l’appareil Azure Active Directory pour contrôler l’accès aux applications connectées Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-policy-connected-applications/).

 Le flux suivant est utilisé par les stratégies d'accès conditionnel pour Exchange Online pour évaluer s'il faut autoriser ou bloquer des appareils.  

 ![Accès conditionnel8&#45;1](media/ConditionalAccess8-1.png)  

 Pour accéder à la messagerie, l'appareil doit :  

-   Être inscrit dans Intune.  

-   Les PC doivent être joints à un domaine ou inscrits et conformes aux stratégies définies dans Intune.  

-   Inscrire l’appareil dans Azure Active Directory (cela se produit automatiquement quand l’appareil est inscrit auprès d’Intune).  

     Pour les PC joints à un domaine, vous devez le configurer pour qu’il [s’inscrive automatiquement](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) auprès d’Azure Active Directory.  

-   Activer la messagerie, ce qui entraîne l’association de l’ID Exchange ActiveSync de l’appareil à l’enregistrement de l’appareil dans Azure Active Directory (s’applique uniquement aux appareils iOS et Android).  

-   Être conforme à toutes les stratégies de conformité déployées  

 L'état de l'appareil est stocké dans Azure Active Directory, qui autorise ou bloque l'accès à la messagerie en fonction des conditions évaluées.  

 Si une condition n'est pas remplie, l'utilisateur reçoit l'un des messages suivants quand il tente de se connecter :  

-   Si l'appareil n'est pas inscrit ou qu'il n'est pas inscrit dans Azure Active Directory, l'utilisateur reçoit un message contenant des instructions pour installer l'application Portail d'entreprise, inscrire l'appareil.  

-   Si l’appareil n’est pas conforme, l’utilisateur reçoit un message le dirigeant vers le site web ou l’application Portail d’entreprise, où il peut trouver des informations sur le problème et des solutions pour y remédier.  

-   Sur un PC :  

    -   Si la stratégie est définie de manière à exiger la jonction à un domaine et que le PC n'est pas joint à un domaine, un message invitant l'utilisateur à contacter l'administrateur informatique s'affiche.  

    -   Si la stratégie définie exige la jonction à un domaine ou la conformité, le PC ne répond pas aux conditions et un message contenant des instructions sur la façon d'installer l'application Portail d'entreprise et d'inscrire l'appareil s'affiche.  

 Le message s'affiche sur l'appareil à l'attention des utilisateurs et des locataires Exchange Online dans le nouvel environnement Exchange Online Dedicated, ainsi que dans la boîte de réception des utilisateurs d'appareils Exchange Online Dedicated hérités et Exchange sur site.  

> [!NOTE]  
>  Les règles d’accès conditionnel Configuration Manager permettent de remplacer, autoriser, bloquer et mettre en quarantaine les règles définies dans la console d’administration Exchange Online.  

> [!NOTE]  
>  La stratégie d’accès conditionnel doit être configurée dans la console Intune. Les étapes suivantes commencent en accédant à la console Intune via Configuration Manager. Si vous y êtes invité, connectez-vous en utilisant les informations d’identification que vous avez utilisées pour configurer le point de connexion de service entre Configuration Manager et Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Pour activer la stratégie Exchange Online  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Développez **Paramètres de conformité**, développez **Accès conditionnel**, puis cliquez sur **Exchange Online**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Liens**, cliquez sur **Configurer la stratégie d’accès conditionnel dans la console Intune**. Vous pouvez être amené à fournir le nom d’utilisateur et le mot de passe du compte utilisé pour connecter Configuration Manager à un administrateur général du service Intune.  

     La console d’administration Intune s’ouvre.  

4.  Dans la console [console d'administration Microsoft Intune](https://manage.microsoft.com), cliquez sur **Stratégie** > **Accès conditionnel** > **Exchange Online Stratégie**.  

     ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5.  Dans la page **Stratégie Exchange Online** , sélectionnez **Activer la stratégie d'accès conditionnel pour Exchange Online**. Si vous activez cette option, l'appareil doit être conforme à la stratégie. Si elle n'est pas activée, l'accès conditionnel n'est pas appliqué.  

    > [!NOTE]  
    >  Si vous n'avez pas déployé de stratégie de conformité et que vous activez la stratégie Exchange Online, tous les appareils ciblés sont signalés comme conformes.  
    >   
    >  Quel que soit l’état de conformité, tous les utilisateurs ciblés par la stratégie doivent inscrire leurs appareils auprès d’Intune.  

6.  Sous **Accès à l’application**, pour Outlook et d’autres applications utilisant une authentification moderne, vous pouvez choisir de restreindre l’accès aux appareils conformes pour chaque plateforme.  Les appareils Windows doivent être soit joints à un domaine, soit inscrits dans Intune et conformes.  

    > [!TIP]  
    >  L'**authentification moderne** permet aux clients Office de bénéficier de la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library).  
    >   
    >  -   L'authentification ADAL permet aux clients Office de procéder à une authentification basée sur un navigateur (également appelée authentification passive).  Pour s'authentifier, l'utilisateur est dirigé vers une page web de connexion.  
    > -   Cette nouvelle méthode de connexion autorise de nouveaux scénarios tels que l'accès conditionnel basé sur la **compatibilité des appareils** et sur l'exécution préalable de l' **authentification multifacteur** .  
    >   
    >  Cet [article](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) contient des informations plus détaillées sur le fonctionnement de l’authentification moderne.  

     En utilisant Exchange Online avec Configuration Manager et Intune, vous pouvez non seulement gérer les appareils mobiles avec un accès conditionnel, mais aussi les ordinateurs de bureau. Les PC doivent être soit joints à un domaine, soit inscrits dans Intune et conformes. Vous pouvez définir les conditions suivantes :  

    -   **Les appareils doivent être joints à un domaine ou conformes.** Les PC doivent être joints à un domaine ou conformes aux stratégies. Si un PC ne remplit pas l’une de ces conditions requises, l’utilisateur est invité à inscrire l’appareil auprès d’Intune.  

    -   **Les appareils doivent être joints à un domaine** . Les PC doivent être joints à un domaine pour accéder à Exchange Online. Si un PC n’est pas joint à un domaine, l’accès à la messagerie électronique est bloqué et l’utilisateur est invité à contacter l’administrateur informatique.  

    -   **Les appareils doivent être conformes** Les PC doivent être inscrits auprès d’Intune et être conformes. Si un PC n’est pas inscrit, un message contenant des instructions sur la procédure d’inscription à suivre s’affiche.  

7.  Sous **Outlook Web Access (OWA)**, vous pouvez choisir d’autoriser l’accès à Exchange Online uniquement par le biais des navigateurs pris en charge : Safari (iOS) et Chrome (Android). L’accès à partir d’autres navigateurs sera bloqué. Les mêmes restrictions de plateforme que celles que vous avez sélectionnées pour l’accès aux applications pour Outlook s’appliquent également ici.

    Sur les appareils **Android** , les utilisateurs doivent activer l’accès du navigateur.  Pour cela, l’utilisateur final doit activer l’option « Activer l’accès du navigateur » sur l’appareil inscrit en procédant comme suit :
     1. Lancez **l’application Portail d’entreprise**.
     2. Accédez à la page **Paramètres** via les trois points (...) ou le bouton de menu matériel.
      3.    Appuyez sur le bouton **Activer l’accès du navigateur** .
      4.    Dans le navigateur Chrome, déconnectez-vous d’Office 365 et redémarrez Chrome.

     Sur les plateformes **iOS et Android** , pour identifier l’appareil utilisé pour accéder au service, Azure Active Directory émet un certificat TLS (Transport Layer Security) pour l’appareil.  L’appareil affiche le certificat et invite l’utilisateur final à le sélectionner, comme indiqué dans les captures d’écran ci-dessous. L’utilisateur final doit sélectionner ce certificat pour pouvoir continuer à utiliser le navigateur.

     **iOS**

     ![capture d’écran de l’invite de certificat sur un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Android**

    ![capture d’écran de l’invite de certificat sur un appareil Android](media/mdm-browser-ca-android-cert-prompt.png)

7.  Pour**Applications de messagerie Exchange ActiveSync**, vous pouvez choisir de bloquer l’accès de la messagerie à Exchange Online si l’appareil n’est pas conforme. Vous pouvez aussi autoriser ou bloquer l’accès à la messagerie quand Intune ne peut pas gérer l’appareil.  

8.  Sous **Groupes ciblés**, sélectionnez les groupes de sécurité Active Directory auxquels la stratégie sera appliquée.  

    > [!NOTE]  
    >  Pour les utilisateurs qui figurent dans les groupes cibles, les stratégies Intune remplacent les stratégies et les règles Exchange.  
    >   
    >  Exchange applique les règles d'autorisation, de blocage et de mise en quarantaine d'Exchange, ainsi que les stratégies Exchange, si :  
    >   
    >  -   L'utilisateur n'a pas de licence Intune.  
    > -   L'utilisateur a une licence Intune, mais n'appartient à aucun groupe de sécurité ciblé dans la stratégie d'accès conditionnel.  

9. Sous **Groupes exemptés**, sélectionnez les groupes de sécurité Active Directory exemptés de cette stratégie. Si un utilisateur figure à la fois dans les groupes ciblés et dans les groupes exemptés, il est exempté de la stratégie et a accès à sa messagerie électronique.  

10. Une fois terminé, cliquez sur **Enregistrer**.  

-   La stratégie d’accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

-   Quand un utilisateur crée un compte de messagerie, l’appareil est bloqué immédiatement.  

-   Si un utilisateur bloqué inscrit l’appareil auprès d’Intune (ou remédie à la non-conformité), l’accès à la messagerie est débloqué dans les 2 minutes.  

-   Si l’utilisateur annule l’inscription de son appareil, la messagerie électronique est bloquée après environ 6 heures.  

### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Pour Exchange sur site (et les locataires dans l’environnement Exchange Online Dedicated hérité)  
 Le flux suivant est utilisé par les stratégies d’accès conditionnel pour Exchange sur site et les locataires dans l’environnement Exchange Online Dedicated hérité pour évaluer s’il faut autoriser ou bloquer des appareils.  

 ![Accès conditionnel8&#45;2](media/ConditionalAccess8-2.png)  

##### <a name="to-enable-the-exchange-on-premises-policy"></a>Pour activer la stratégie Exchange sur site  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Développez **Paramètres de conformité**, développez **Accès conditionnel**, puis cliquez sur **Exchange local**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Exchange local** , cliquez sur **Configurer la stratégie d'accès conditionnel**.  

4.  **Depuis la version 1602 de Configuration Manager**, dans la page **Général** de **l’Assistant Configuration de la stratégie d’accès conditionnel**, spécifiez si vous souhaitez remplacer la règle par défaut d’Exchange Active Sync. Cliquez sur cette option si vous souhaitez que les appareils inscrits et conformes aient toujours accès à la messagerie, même si la règle par défaut est définie pour mettre en quarantaine ou bloquer l’accès.  

    > [!NOTE]  
    >  Il existe un problème avec le remplacement par défaut pour les appareils Android. Si la règle d’accès par défaut du serveur Exchange a la valeur **Bloquer** et si la stratégie d’accès conditionnel Exchange est activée avec l’option de remplacement de la règle par défaut, les appareils Android des utilisateurs ciblés risquent de ne pas être débloqués même si les appareils sont inscrits auprès d’Intune et conformes.  Pour contourner ce problème, affectez à la règle d’accès par défaut d’Exchange la valeur **Quarantaine**. L’appareil n’obtient pas l’accès à Exchange par défaut, et l’administrateur peut recevoir d’Exchange Server un rapport sur la liste des appareils en quarantaine.  

     Si vous n’avez pas défini de compte pour le courrier électronique de notification lors de la configuration du connecteur Exchange, un avertissement s’affiche dans cette page et le bouton **Suivant** est désactivé.  Pour pouvoir continuer, vous devez configurer les paramètres d’e-mail de notification dans le connecteur Exchange, puis revenir à **l’Assistant Configuration de la stratégie d’accès conditionnel** pour terminer la procédure.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

     Cliquez sur **Suivant**.  

5.  Dans la page **Regroupements ciblés** , ajoutez un ou plusieurs regroupements d'utilisateurs. Pour accéder à Exchange, les utilisateurs de ces regroupements doivent inscrire leurs appareils auprès d’Intune et être conformes aux stratégies de conformité que vous avez déployées.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

     Cliquez sur **Suivant**.  

6.  Dans la page **Regroupements exemptés** , ajoutez les regroupements d'utilisateurs que vous voulez exempter de la stratégie d'accès conditionnel. Les utilisateurs de ces groupes n’ont pas besoin d’inscrire leurs appareils auprès d’Intune ni d’être conformes aux stratégies de conformité déployées pour accéder à Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

     Si un utilisateur figure à la fois dans les listes des groupes ciblés et des groupes exemptés, il est exempté de la stratégie d'accès conditionnel.  

     Cliquez sur **Suivant**.  

7.  Dans la page **Modifier la notification à l’utilisateur**, configurez le message électronique qu’envoie Intune aux utilisateurs avec des instructions sur la procédure pour débloquer leur appareil (en plus du message envoyé par Exchange).  

     Vous pouvez modifier le message par défaut et utiliser des balises HTML pour mettre en forme le texte. Vous pouvez également envoyer un courrier électronique à l’avance à vos employés pour les informer des modifications à venir et leur fournir des instructions sur l’inscription de leurs appareils.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    >  Le message électronique de notification Intune contenant les instructions de correction est remis dans la boîte aux lettres Exchange de l’utilisateur. Par conséquent, si l’appareil de l’utilisateur est bloqué avant la réception du message électronique, l’utilisateur peut utiliser un appareil non bloqué ou recourir à une autre méthode pour accéder à Exchange et consulter le message.  

    > [!NOTE]  
    >  Pour que le message électronique de notification puisse être envoyé par Exchange, vous devez configurer le compte utilisé pour l'envoyer. Vous faites cela quand vous configurez les propriétés du connecteur Exchange Server.  
    >   
    >  Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

     Cliquez sur **Suivant**.  

8.  Sur la page  **Résumé** , vérifiez les paramètres, puis terminez l'Assistant.  

-   La stratégie d'accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

-   Une fois qu’un utilisateur a configuré un profil Exchange ActiveSync, le blocage de son appareil peut prendre entre une et trois heures (s’il n’est pas géré par Intune).  

-   Si un utilisateur bloqué inscrit alors l’appareil auprès d’Intune (ou remédie à la non-conformité), l’accès à la messagerie électronique est débloqué dans les deux minutes.  

-   Si l’utilisateur annule l’inscription auprès d’Intune, le blocage de son appareil peut prendre entre une et trois heures.  

### <a name="see-also"></a>Voir aussi  
 [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)
