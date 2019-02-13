---
title: Gérer l'accès à la messagerie
titleSuffix: Configuration Manager
description: Découvrez comment utiliser l’accès conditionnel de Configuration Manager pour gérer l’accès à la messagerie Exchange.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f976b63b4580b5df9c6e609ff6b361538860c41c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137641"
---
# <a name="manage-email-access-in-configuration-manager"></a>Gérer l’accès à la messagerie dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez le Gestionnaire de Configuration accès conditionnel pour gérer l’accès à la messagerie Exchange selon des conditions que vous spécifiez.  

Vous pouvez gérer l'accès à :  

- Microsoft Exchange sur site  

- Microsoft Exchange Online  

- Exchange Online Dedicated  

Vous pouvez contrôler l'accès à Exchange Online et Exchange sur site à partir du client de messagerie intégré sur les plateformes suivantes :  

- Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur  

- iOS 9.0 et ultérieur  

- Windows Phone 8.1 et versions ultérieures  

- Application de messagerie sur Windows 8.1 et versions ultérieures  

Les applications de bureau Office peuvent accéder à Exchange Online sur les PC exécutant :  

- Office 2013 et ultérieur pour ordinateur avec [l’authentification moderne](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) activée.  

- Windows 7.0 ou Windows 8.1  

> [!NOTE]  
> Les PC doivent être joints au domaine ou être conformes aux stratégies définies dans Intune.  


## <a name="device-requirements"></a>Exigences relatives aux appareils
Si vous configurez l'accès conditionnel, l'appareil dont l'utilisateur se sert pour se connecter à sa messagerie doit :  

- Être inscrit auprès d’Intune ou d’un PC joint à un domaine.  

- Inscrire l’appareil dans Azure Active Directory. Ceci se fait automatiquement quand l’appareil est inscrit auprès d’Intune (pour Exchange Online uniquement). Par ailleurs, l'ID Exchange ActiveSync du client doit être inscrite auprès d'Azure Active Directory (ceci ne s'applique pas aux appareils Windows et Windows Phone se connectant à Exchange sur site).  

    Pour un PC joint à un domaine, vous devez le configurer de manière à ce qu'il s'inscrive automatiquement auprès d'Azure Active Directory. Le **accès conditionnel pour PC** section dans le [gérer l’accès aux services](../../protect/deploy-use/manage-access-to-services.md) article répertorie l’ensemble complet des conditions requises pour activer l’accès conditionnel pour PC.  

- Être conforme à toutes les stratégies de conformité Configuration Manager déployées sur cet appareil.  

    Si une condition d’accès conditionnel n’est pas remplie, l’utilisateur reçoit l’un des messages suivants lors de la connexion :  

- Si l’appareil n’est pas inscrit avec Intune, ou n’est pas inscrit dans Azure Active Directory, un message s’affiche avec des instructions expliquant comment installer l’application portail d’entreprise, inscrire l’appareil et (pour les appareils Android et iOS), activer la messagerie, qui associe le ID de l’appareil Exchange ActiveSync avec l’enregistrement d’appareil dans Azure Active Directory.  

- Si l’appareil n’est pas conforme, un message s’affiche qui dirige l’utilisateur vers le portail web Intune où il peut trouver des informations sur le problème et comment y remédier.  

#### <a name="for-mobile-devices"></a>Pour les appareils mobiles

Vous pouvez restreindre l’accès à **Outlook Web Access (OWA)** sur Exchange Online par le biais d’un navigateur sur des appareils **iOS** et **Android** . L’accès sera autorisé uniquement à partir des navigateurs pris en charge sur les appareils compatibles :  

- Safari (iOS)  
- Chrome (Android)  
- Managed Browser (iOS et Android)  

Les navigateurs non pris en charge seront bloqués. Les applications OWA pour iOS et Android ne sont pas pris en charge. Elles doivent être bloquées par les règles de revendications AD FS :  

- Configurez des règles de revendications AD FS pour bloquer les protocoles autres que l'authentification moderne. Obtenir des instructions détaillées sont fournies dans le scénario 3 à [bloquer tout accès à O365, à l’exception des applications basées sur un navigateur](https://technet.microsoft.com/library/dn592182.aspx).  

#### <a name="for-pcs"></a>Pour les PC

- Si l'exigence de la stratégie d'accès conditionnel est d'autoriser la **jonction à un domaine** ou la **conformité**, un message contenant des instructions sur la façon d'inscrire l'appareil s'affiche. Si le PC ne remplit pas l’une des conditions requises, l’utilisateur doit inscrire l’appareil auprès d’Intune.  

- Si l'exigence de la stratégie d'accès conditionnel est configurée pour autoriser uniquement les appareils Windows joints à un domaine, l'appareil est bloqué et un message invitant l'utilisateur à contacter l'administrateur informatique s'affiche.  

Vous pouvez bloquer l'accès à la messagerie Exchange à partir du client de messagerie Exchange ActiveSync intégré aux appareils sur les plateformes suivantes :  

- Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur  

- iOS 9.0 et ultérieur  

- Windows Phone 8.1 et versions ultérieures  

- Application **Courrier** sur Windows 8.1 et versions ultérieures  

L’application Outlook pour iOS et Android, ainsi que l’application de bureau Outlook 2013 et ultérieur, sont prises en charge uniquement pour Exchange Online.  

Le **connecteur Exchange local** entre Configuration Manager et Exchange est nécessaire au fonctionnement de l’accès conditionnel.  

Vous pouvez configurer une stratégie d’accès conditionnel pour Exchange sur site à partir de la console Configuration Manager. Quand vous configurez une stratégie d’accès conditionnel pour Exchange Online, vous pouvez commencer le processus dans la console Configuration Manager, ce qui lance la console Intune, dans laquelle vous pouvez terminer le processus.  



## <a name="configure-conditional-access"></a>Configurer un accès conditionnel

### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>Étape 1 : Évaluer l’impact de la stratégie d’accès conditionnel  

Une fois que vous avez configuré le **connecteur Exchange sur site**, vous pouvez utiliser le Gestionnaire de Configuration **liste des appareils par état d’accès conditionnel** rapport pour identifier les appareils qui ne peuvent pas Après avoir configuré la stratégie d’accès conditionnel, l’accès à Exchange. Ce rapport requiert également les éléments suivants :  

- Un abonnement à Intune.  

- Le point de connexion de service doit être configuré et déployé.  

Dans les paramètres du rapport, sélectionnez le groupe Intune à évaluer et, si nécessaire, les plateformes d’appareils auxquelles la stratégie doit être appliquée.  

Pour plus d'informations sur la façon d'exécuter des rapports, consultez [Reporting in Configuration Manager](/sccm/core/servers/manage/reporting).  

Après avoir exécuté le rapport, examinez ces quatre colonnes pour déterminer si un utilisateur sera bloqué :  

- **Canal de gestion**: L’appareil est géré par Intune, Exchange ActiveSync ou les deux.  

- **Inscrit auprès d’AAD**: L’appareil est inscrit avec Azure Active Directory (appelé jonction).  

- **Conforme** : L’appareil est conforme aux stratégies de conformité que vous avez déployé.  

- **EAS activé**: appareils iOS et Android doit être l’ID ActiveSync Exchange associé à l’enregistrement de l’inscription d’appareil dans Azure Active Directory. Ceci se produit quand l'utilisateur clique sur le lien **Activer la messagerie** dans l'e-mail de mise en quarantaine.  

    > [!NOTE]  
    > Les appareils Windows Phone affichent toujours une valeur dans cette colonne.  

Les appareils qui font partie d'un groupe ou d'un regroupement ciblé verront leur accès à Exchange bloqué, sauf si les valeurs de colonne correspondent à celles qui sont répertoriées dans le tableau suivant :  

|Canal de gestion|Enregistré avec AAD|conformité|EAS activé|Action résultante|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Géré par Microsoft Intune et Exchange ActiveSync**|Oui|Oui|**Oui** ou **Non** s'affiche.|Accès à la messagerie accordé|  
|Toute autre valeur|Non|Non|Aucune valeur affichée|Accès à la messagerie bloqué|  

Vous pouvez exporter le contenu du rapport et utiliser la colonne **Adresse de messagerie** pour informer les utilisateurs qu'ils ne pourront pas accéder à la messagerie.  


### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>Étape 2 : Configurer des groupes d’utilisateurs ou des regroupements pour la stratégie d’accès conditionnel  

Vous ciblez les stratégies d'accès conditionnel vers différents groupes ou regroupements d'utilisateurs en fonction du type de stratégie. Ces groupes contiennent les utilisateurs qui seront ciblés par la stratégie ou exemptés de celle-ci. Quand un utilisateur est ciblé par une stratégie, chaque appareil qu'il utilise doit être conforme à cette stratégie pour qu'il puisse accéder à la messagerie.  

- **Pour la stratégie Exchange Online**: pour les groupes de sécurité Azure Active Directory. Vous pouvez configurer ces groupes dans le **Centre d'administration Office 365**ou dans le **Portail de compte Intune**.  

- **Pour la stratégie Exchange sur site**: pour les regroupements d’utilisateurs Configuration Manager. Vous pouvez les configurer dans l'espace de travail **Ressources et Conformité** .  

Vous pouvez spécifier deux types de groupes dans chaque stratégie :  

- **Groupes ciblés**: Groupes d’utilisateurs ou des regroupements auxquels la stratégie est appliquée.  

- **Groupes exemptés**: Groupes d’utilisateurs ou des regroupements qui sont exempts de la stratégie (facultatif)  

Si un utilisateur se trouve dans les deux, il est exempté de la stratégie.  

Seuls les groupes ou les regroupements qui sont ciblés par la stratégie d'accès conditionnel sont évalués pour l'accès à Exchange.  


### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>Étape 3 : Configurer et déployer une stratégie de conformité  

Vérifiez que vous avez créé et déployé une stratégie de conformité pour tous les appareils qui seront ciblés par la stratégie d'accès conditionnel Exchange.  

Pour plus d’informations sur la configuration de la stratégie de conformité, consultez [Gérer les stratégies de conformité d’appareils](device-compliance-policies.md).  

> [!IMPORTANT]  
> Si vous n’avez pas déployé une stratégie de conformité et que vous activez ensuite une stratégie d’accès conditionnel Exchange, tous les appareils ciblés pourront accéder.  


### <a name="step-4-configure-the-conditional-access-policy"></a>Étape 4 : Configurer la stratégie d’accès conditionnel  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Pour Exchange Online (et les locataires dans le nouvel environnement Exchange Online Dedicated)

> [!NOTE]  
> Vous pouvez aussi créer une stratégie d’accès conditionnel dans la console de gestion Azure AD. Celle-ci vous permet de créer les stratégies d’accès conditionnel aux appareils (appelées dans Azure AD « stratégies d’accès conditionnel en fonction de l’appareil ») en plus des autres stratégies d’accès conditionnel comme l’authentification multifacteur. Vous pouvez aussi définir des stratégies d’accès conditionnel pour des applications d’entreprise tierces comme Salesforce et Box prises en charge par Azure AD. Pour plus d’informations, consultez [How To : Exiger que les appareils gérés pour accéder aux applications de cloud avec l’accès conditionnel](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

Le flux suivant est utilisé par les stratégies d'accès conditionnel pour Exchange Online pour évaluer s'il faut autoriser ou bloquer des appareils.  

![Flux d’accès conditionnel](media/ConditionalAccess8-1.png)  

Pour accéder à la messagerie, l'appareil doit :  

- Être inscrit dans Intune.  

- Les PC doivent être joints au domaine ou être inscrits et conformes aux stratégies définies dans Intune  

- Inscrire l’appareil dans Azure AD. Cela se produit automatiquement quand l’appareil est inscrit auprès d’Intune. Pour les PC joints à un domaine, vous devez la définir jusqu'à [s’inscrive automatiquement](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-manual-steps) avec Azure AD.  

- Activer la messagerie, ce qui entraîne l’association de l’ID Exchange ActiveSync de l’appareil à l’enregistrement de l’appareil dans Azure Active Directory (s’applique uniquement aux appareils iOS et Android).  

- Être conforme à toutes les stratégies de conformité déployées  

L'état de l'appareil est stocké dans Azure Active Directory, qui autorise ou bloque l'accès à la messagerie en fonction des conditions évaluées.  

Si une condition n’est pas remplie, l’utilisateur reçoit l’un des messages suivants lorsqu’ils se connectent :  

- Si l’appareil n’est pas inscrit ou inscrit dans Azure AD, un message s’affiche avec des instructions expliquant comment installer l’application portail d’entreprise et inscrire  

- Si l’appareil n’est pas conforme, un message s’affiche qui dirige l’utilisateur vers le site Web portail d’entreprise Intune ou de l’application de portail d’entreprise où il peut trouver des informations sur le problème et comment y remédier.  

- Sur un PC :  

    - Si la stratégie est définie pour exiger la jonction de domaine et le PC n’est pas joint au domaine, un message s’affiche pour contacter l’administrateur informatique.  

    - Si la stratégie est définie pour exiger la jonction de domaine ou conforme et le PC ne répond pas aux conditions, un message s’affiche avec des instructions expliquant comment installer l’application portail d’entreprise et inscrire.  

Le message s'affiche sur l'appareil à l'attention des utilisateurs et des locataires Exchange Online dans le nouvel environnement Exchange Online Dedicated, ainsi que dans la boîte de réception des utilisateurs d'appareils Exchange Online Dedicated hérités et Exchange sur site.  

> [!NOTE]  
> Les règles d’accès conditionnel Configuration Manager permettent de remplacer, autoriser, bloquer et mettre en quarantaine les règles définies dans la console d’administration Exchange Online.  
> 
> La stratégie d’accès conditionnel doit être configurée dans la console Intune. Les étapes suivantes commencent en accédant à la console Intune via Configuration Manager. Si vous y êtes invité, connectez-vous en utilisant les informations d’identification qui ont été utilisées pour configurer le point de connexion de service entre Configuration Manager et Intune.  

##### <a name="to-enable-the-exchange-online-policy"></a>Pour activer la stratégie Exchange Online  

1. Dans la console Configuration Manager, sélectionnez **biens et conformité**.  

2. Développez **paramètres de compatibilité**, développez **accès conditionnel**, puis sélectionnez **Exchange Online**.  

3. Sur le **accueil** sous l’onglet le **liens** groupe, sélectionnez **configurer la stratégie d’accès conditionnel dans la Intune Console**. Vous pouvez être amené à fournir le nom d’utilisateur et le mot de passe du compte utilisé pour connecter Configuration Manager à un administrateur général du service Intune. La console d’administration Intune s’ouvre.  

4. Dans le portail Microsoft Intune, sélectionnez **stratégie** > **accès conditionnel** > **stratégie Exchange Online**.  

    ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5. Dans la page **Stratégie Exchange Online** , sélectionnez **Activer la stratégie d'accès conditionnel pour Exchange Online**. Si vous activez cette option, l'appareil doit être conforme à la stratégie. Si ce n’est pas activé l’accès conditionnel n’est pas appliqué.  

    > [!NOTE]  
    > Si vous n’avez pas déployé une stratégie de conformité et que vous activez la stratégie Exchange Online, tous les appareils ciblés sont considérés comme conformes.  
   >   
   >  Quel que soit l’état de conformité, tous les utilisateurs ciblés par la stratégie doivent inscrire leurs appareils auprès d’Intune.  

6. Sous **accès aux applications**, pour Outlook et d’autres applications à l’aide de l’authentification moderne, vous pouvez choisir de restreindre l’accès aux appareils conformes pour chaque plateforme. Les appareils Windows doivent être soit joints à un domaine, soit inscrits dans Intune et conformes.  

    > [!TIP]  
    > L'**authentification moderne** permet aux clients Office de bénéficier de la connexion basée sur la bibliothèque ADAL (Active Directory Authentication Library).  
    > 
    > - L'authentification ADAL permet aux clients Office de procéder à une authentification basée sur un navigateur (également appelée authentification passive). Pour s'authentifier, l'utilisateur est dirigé vers une page web de connexion.  
    > - Cette nouvelle méthode de connexion autorise de nouveaux scénarios tels que l'accès conditionnel basé sur la **compatibilité des appareils** et sur l'exécution préalable de l' **authentification multifacteur** .  
    > 
    >  Pour plus d’informations, consultez [Fonctionnement de l’authentification moderne pour les applications clientes Office 2013 et Office 2016](https://docs.microsoft.com/office365/enterprise/modern-auth-for-office-2013-and-2016).  

    En utilisant Exchange Online avec Configuration Manager et Intune, vous pouvez non seulement gérer les appareils mobiles avec un accès conditionnel, mais aussi les ordinateurs de bureau. PC doivent être joint au domaine, ou être inscrits dans Intune et conformes. Vous pouvez définir les conditions suivantes :  

    - **Les appareils doivent être joints à un domaine ou conformes.** PC doivent être joint au domaine ou conformes aux stratégies. Si un PC ne remplit pas une de ces conditions, l’utilisateur est invité à inscrire l’appareil avec Intune.  

    - **Les appareils doivent être joints à un domaine** Les PC doivent être joints au domaine pour accéder à Exchange Online. Si un PC n’est pas joint au domaine, l’accès à la messagerie électronique est bloqué et l’utilisateur est invité à contacter l’administrateur informatique.  

    - **Les appareils doivent être conformes** Les PC doivent être inscrits auprès d’Intune et être conformes. Si un PC n’est pas inscrit, un message contenant des instructions sur l’inscription s’affiche.  

7. Sous **l’accès web Outlook (OWA)**, vous pouvez choisir d’autoriser l’accès à Exchange Online uniquement via les navigateurs pris en charge : Safari (iOS) et Chrome (Android). L’accès à partir d’autres navigateurs sera bloqué. Les mêmes restrictions de plateforme que celles que vous avez sélectionnées pour l’accès aux applications pour Outlook s’appliquent également ici.  

    - Sur les appareils **Android** , les utilisateurs doivent activer l’accès du navigateur. Pour effectuer cette action, l’utilisateur doit activer l’option « Activer l’accès navigateur » sur l’appareil inscrit comme suit :  

        1. Lancez **l’application Portail d’entreprise**.  

        2. Accédez à la page **Paramètres** via les trois points (...) ou le bouton de menu matériel.  

        3. Appuyez sur le bouton **Activer l’accès du navigateur** .  

        4. Dans le navigateur Chrome, déconnectez-vous d’Office 365 et redémarrez Chrome.  

    - Sur **iOS et Android** plateformes, pour identifier le périphérique qui est utilisé pour accéder au service, Azure AD émet un certificat TLS à l’appareil. L’appareil affiche le certificat avec une invite demandant à l’utilisateur de sélectionner le certificat, comme indiqué dans les captures d’écran ci-dessous. L’utilisateur doit sélectionner ce certificat avant de pouvoir continuer à utiliser le navigateur.  

        - **iOS**  

        ![capture d’écran de l’invite de certificat sur un ipad](media/mdm-browser-ca-ios-cert-prompt_v2.png)  

        - **Android**  

        ![capture d’écran de l’invite de certificat sur un appareil Android](media/mdm-browser-ca-android-cert-prompt.png)  

8. Pour**Applications de messagerie Exchange ActiveSync**, vous pouvez choisir de bloquer l’accès de la messagerie à Exchange Online si l’appareil n’est pas conforme. Vous pouvez aussi autoriser ou bloquer l’accès à la messagerie quand Intune ne peut pas gérer l’appareil.  

9. Sous **Groupes ciblés**, sélectionnez les groupes de sécurité Active Directory auxquels la stratégie sera appliquée.  

    > [!NOTE]  
    > Pour les utilisateurs qui se trouvent dans les groupes ciblés, les stratégies Intune remplacent les stratégies et les règles Exchange.  
    > 
    > Exchange applique les règles d'autorisation, de blocage et de mise en quarantaine d'Exchange, ainsi que les stratégies Exchange, si :  
    > 
    > - L'utilisateur n'a pas de licence Intune.  
    > - L’utilisateur a une licence pour Intune, mais l’utilisateur n’appartient pas à des groupes de sécurité ciblés dans la stratégie d’accès conditionnel.  

10. Sous **Groupes exemptés**, sélectionnez les groupes de sécurité Active Directory exemptés de cette stratégie. Si un utilisateur figure dans les groupes ciblés et exemptés, ils seront exemptés de la stratégie et auront accès à sa messagerie.  

11. Une fois terminé, cliquez sur **Enregistrer**.  


Passez en revue les notes suivantes sur cette stratégie :  

- Vous n’êtes pas obligé de déployer la stratégie d’accès conditionnel ; Il prend effet immédiatement.  

- Quand un utilisateur crée un compte de messagerie, l’appareil est bloqué immédiatement.  

- Si un utilisateur bloqué inscrit l’appareil auprès d’Intune (ou remédie à la non-conformité), l’accès à la messagerie est débloqué dans les 2 minutes.  

- Si l’utilisateur annule l’inscription de son appareil, la messagerie électronique est bloquée après environ 6 heures.  


### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Pour Exchange sur site (et les locataires dans l’environnement Exchange Online Dedicated hérité)  
Le flux suivant est utilisé par les stratégies d’accès conditionnel pour Exchange sur site et les locataires dans l’environnement Exchange Online Dedicated hérité pour évaluer s’il faut autoriser ou bloquer des appareils.  

![Accès conditionnel8&#45;2](media/ConditionalAccess8-2.png)  

#### <a name="to-enable-the-exchange-on-premises-policy"></a>Pour activer la stratégie Exchange sur site  

1. Dans la console Configuration Manager, sélectionnez **biens et conformité**.  

2. Développez **paramètres de compatibilité**, développez **accès conditionnel**, puis sélectionnez **Exchange sur site**.  

3. Sur le **accueil** sous l’onglet le **Exchange sur site** groupe, sélectionnez **configurer la stratégie d’accès conditionnel**.  

4. Sur le **général** page de la **configurer Assistant stratégie d’accès conditionnel**, spécifiez si vous souhaitez remplacer la règle par défaut de Exchange Active Sync. Sélectionnez cette option si vous souhaitez inscrits et accéder aux appareils conformes aient toujours accès à la messagerie, même si la règle par défaut est définie pour la mise en quarantaine ou bloquer.  

    > [!NOTE]  
    > Il existe un problème avec le remplacement par défaut pour les appareils Android. Si la règle d’accès par défaut du serveur Exchange a la valeur **Bloquer** et si la stratégie d’accès conditionnel Exchange est activée avec l’option de remplacement de la règle par défaut, les appareils Android des utilisateurs ciblés risquent de ne pas être débloqués même si les appareils sont inscrits auprès d’Intune et conformes. Pour contourner ce problème, affectez à la règle d’accès par défaut d’Exchange la valeur **Quarantaine**. L’appareil n’accéder à Exchange par défaut, et l’administrateur peut obtenir un rapport à partir du serveur Exchange dans la liste des appareils qui sont mis en quarantaine.  

    Si vous n’avez pas le programme d’installation un compte de messagerie de notification lorsque vous configurez le connecteur Exchange, vous verrez un avertissement sur cette page et le **suivant** bouton est désactivé.  Pour pouvoir continuer, vous devez configurer les paramètres d’e-mail de notification dans le connecteur Exchange, puis revenir à **l’Assistant Configuration de la stratégie d’accès conditionnel** pour terminer la procédure.  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

5. Dans la page **Regroupements ciblés** , ajoutez un ou plusieurs regroupements d'utilisateurs. Pour accéder à Exchange, les utilisateurs de ces regroupements doivent inscrire leurs appareils auprès d’Intune et être conformes aux stratégies de conformité que vous avez déployées.  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

6. Dans la page **Regroupements exemptés** , ajoutez les regroupements d'utilisateurs que vous voulez exempter de la stratégie d'accès conditionnel. Les utilisateurs de ces groupes, n’inscrivent leurs appareils avec Intune et ne pas besoin être conformes aux stratégies de conformité déployées pour accéder à Exchange.  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

    Si un utilisateur figure à la fois dans les listes des groupes ciblés et des groupes exemptés, il est exempté de la stratégie d'accès conditionnel.  

7. Dans la page **Modifier la notification à l’utilisateur**, configurez le message électronique qu’envoie Intune aux utilisateurs avec des instructions sur la procédure pour débloquer leur appareil (en plus du message envoyé par Exchange).  

    Vous pouvez modifier le message par défaut et utiliser des balises HTML pour mettre en forme le texte. Vous pouvez également envoyer un courrier électronique à l’avance à vos employés pour les informer des modifications à venir et leur fournir des instructions sur l’inscription de leurs appareils.  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    > Le message électronique de notification Intune contenant les instructions de correction est remis dans la boîte aux lettres Exchange de l’utilisateur. Par conséquent, si l’appareil de l’utilisateur est bloqué avant la réception du message électronique, l’utilisateur peut utiliser un appareil non bloqué ou recourir à une autre méthode pour accéder à Exchange et consulter le message.  
    > 
    > Dans l’ordre pour Exchange envoyer l’e-mail de notification, configurez le compte qui sera utilisé pour envoyer l’e-mail de notification. Vous faites cela quand vous configurez les propriétés du connecteur Exchange Server.  
    >   
    > Pour plus d’informations, consultez [Gérer des appareils mobiles à l’aide de Configuration Manager et d’Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  

8. Sur le **Résumé** page, passez en revue vos paramètres, puis terminez l’Assistant.  


Passez en revue les notes suivantes sur cette stratégie :  

- La stratégie d’accès conditionnel prend effet immédiatement. Il est donc inutile de la déployer.  

- Une fois qu’un utilisateur a configuré un profil Exchange ActiveSync, il peut prendre 1 à 3 heures pour l’appareil soient bloqués (si elle n’est pas gérée par Intune).  

- Si un utilisateur bloqué puis inscrit l’appareil avec Intune (ou corrige la non-conformité), accès à la messagerie sera débloqué dans les deux minutes.  

- Si l’utilisateur annule-inscription auprès d’Intune peut prendre 1 à 3 heures pour l’appareil devant être bloqués.  


## <a name="see-also"></a>Voir aussi  

[Gérer l’accès aux services](/sccm/protect/deploy-use/manage-access-to-services)
