---
title: Créer et déployer une stratégie de conformité d’appareil
titleSuffix: Configuration Manager
description: Découvrez comment créer et déployer des stratégies de conformité dans Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 0fd76043-d7ee-423d-8c5f-aa7e9ed58ce0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d7debd9a1eacca253b10b8f1db7495e86e3ce8c
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62258361"
---
# <a name="create-and-deploy-a-device-compliance-policy"></a>Créer et déployer une stratégie de conformité d’appareil

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="create-a-compliance-policy"></a>Créer une stratégie de conformité

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

2. Dans l'espace de travail **Ressources et Conformité**, développez **Paramètres de compatibilité**, puis choisissez **Stratégies de conformité**.  

3. Sous l'onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une stratégie de conformité**.  

4. Dans la page **Général** de l'Assistant Création d'élément de configuration, spécifiez les informations suivantes :  

    - **Nom** : Affectez un nom unique à la stratégie de conformité. Vous pouvez entrer jusqu’à 256 caractères.  

    - **Description** : Entrez une description qui donne un aperçu du profil VPN et permette son identification dans la console Configuration Manager. Vous pouvez entrer jusqu’à 256 caractères.  

    - **Type de stratégie de conformité**: Sélectionnez le type de stratégie à créer selon que l’appareil est géré ou non par Configuration Manager.  
    
    Pour les appareils gérés par Intune, optez pour les **règles de conformité applicables aux appareils gérés sans client Configuration Manager** . Cette option vous permet également de sélectionner le type de plateforme auquel appliquer cette stratégie.  

    - **Gravité de non-conformité pour les rapports** : Spécifiez le niveau de gravité signalé si cette stratégie de conformité est évaluée comme non conforme. Les degrés de gravité disponibles sont les suivants :  

        - **Aucun** : Les appareils qui ne respectent pas cette règle de conformité ne signalent une gravité d’échec pour les rapports Configuration Manager.  

        - **Informations** : Les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  

        - **Avertissement** : Les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  

        - **Critique** : Les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  

        - **Critique avec événement** : Les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Le niveau de gravité **critique avec événement** est également enregistré comme événement Windows dans le journal des événements des applications.  

5. Dans la page **Plateformes prises en charge**, choisissez les plateformes d’appareil à évaluer par cette stratégie de conformité. Vous pouvez également **Tout sélectionner** pour choisir toutes les plateformes d’appareil. Les plateformes prises en charge sont : Windows 7, Windows 8.1 et Windows 10 ; Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016.  

6. Dans la page **Règles** , vous définissez une ou plusieurs règles qui définissent la configuration dont les appareils doivent disposer pour être évalués comme étant conformes. Quand vous créez une stratégie de conformité, certaines règles sont activées par défaut, mais vous pouvez les modifier ou les supprimer. Pour obtenir la liste complète de toutes les règles, consultez la section « Règles de stratégie de conformité » plus loin dans cet article.  

    > [!NOTE]  
    > Sur les PC Windows, Windows 8.1 de version est signalée comme 6.3. Si la règle de la version du système d’exploitation est définie sur Windows 8.1 pour Windows, l’appareil sera signalé comme non conforme, même si l’appareil possède Windows 8.1. Vérifiez que vous définissez la version *signalée* correcte de Windows pour les règles de version minimale et maximale de système d’exploitation. Le numéro de version doit correspondre à la version que la commande **winver** retourne. Windows Mobile n’ont pas ce problème ; la version signalée est 8.1 comme prévu.  
    > 
    > Pour les PC Windows avec Windows 10, la version doit être définie en tant que **10.0** ainsi que la build du système d’exploitation numéro que le **winver** commande retourne.  

7. Dans la page **Résumé** de l'Assistant, passez en revue les paramètres que vous avez définis, puis terminez l'Assistant.  

    La nouvelle stratégie apparaît sous le nœud **Stratégies de conformité** de l'espace de travail **Ressources et Conformité**.  


## <a name="deploy-a-compliance-policy"></a>Déployer une stratégie de conformité

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

2. Dans l'espace de travail **Ressources et Conformité**, développez **Paramètres de compatibilité**, puis choisissez **Stratégies de conformité**.  

3. Sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer**.  

4. Dans la boîte de dialogue **Déployer une stratégie de conformité**, choisissez **Parcourir** pour sélectionner le regroupement d'utilisateurs pour lesquels déployer la stratégie.  

    Par ailleurs, vous pouvez sélectionner des options pour générer des alertes quand la stratégie n’est pas conforme et définir le calendrier selon lequel cette stratégie doit être évaluée pour la conformité.  

5. Une fois que vous avez terminé, choisissez **OK**.  



## <a name="monitor-the-compliance-policy"></a>Analyser la stratégie de conformité

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Pour afficher les résultats de compatibilité dans la console Configuration Manager

1. Dans la console Configuration Manager, choisissez **Surveillance**.  

2. Dans l'espace de travail **Surveillance**, choisissez **Déploiements**.  

3. Dans la liste **Déploiements** , sélectionnez le déploiement de la stratégie de conformité dont vous souhaitez vérifier les informations de conformité.  

4. Vous pouvez consulter un résumé des informations relatives à la conformité du déploiement de la stratégie dans la page principale. Pour afficher des informations plus détaillées, sélectionnez le déploiement, puis, sous l'onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Afficher l'état** pour ouvrir la page **État du déploiement**.  

    La page **État du déploiement** contient les onglets suivants :  

    - **Conforme** : Affiche la conformité de la stratégie en fonction du nombre de biens affectés. Vous pouvez choisir une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité**, qui contient tous les utilisateurs ou périphériques conformes à cette règle. Le volet **Détails du bien** affiche les utilisateurs ou les appareils conformes à la stratégie. Pour afficher plus d’informations, double-cliquez sur un utilisateur ou un appareil de la liste.  

    - **Erreur** : Affiche une liste de toutes les erreurs pour le déploiement de stratégie sélectionné en fonction du nombre de ressources concernées. Vous pouvez choisir une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité**, qui contient tous les utilisateurs ou appareils qui ont généré des erreurs avec cette règle. Lorsque vous sélectionnez un utilisateur ou un appareil, le volet **Détails du bien** affiche les utilisateurs ou les appareils affectés par un problème. Pour afficher plus d’informations sur le problème, double-cliquez sur un utilisateur ou un appareil de la liste.  

    - **Non conforme** : Affiche une liste de toutes les règles non conformes au sein de la stratégie en fonction du nombre de ressources affectées. Vous pouvez choisir une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité**, qui contient tous les utilisateurs ou périphériques non conformes à cette règle. Lorsque vous sélectionnez un utilisateur ou un appareil, le volet **Détails du bien** affiche les utilisateurs ou les appareils affectés par un problème. Pour afficher plus d’informations sur le problème, double-cliquez sur un utilisateur ou un appareil de la liste.  

    - **Inconnu** : Affiche une liste de tous les utilisateurs et appareils qui n’ont pas signalé leur conformité pour le déploiement de stratégie sélectionné, ainsi que l’état du client actuel des appareils.  

#### <a name="to-monitor-the-compliance-status-of-an-individual-device"></a>Pour surveiller l’état de conformité d’un appareil individuel

1. Dans la console Configuration Manager, choisissez l’espace de travail **Actifs et conformité**.  

2. Choisissez **Appareils**.  

3. Pour ajouter plus de colonnes, cliquez avec le bouton droit sur une des colonnes. Vous pouvez ajouter les colonnes suivantes :  

    > [!Note]  
    > Par défaut, ces colonnes ne sont pas affichées.  

    - **ID d’appareil Azure Active Directory**: Identificateur unique de l’appareil dans Azure Active Directory.  

    - **Détails de l’erreur conformité**: Détails du message d’erreur lorsque le processus en cas de problème. Si cette colonne est vide, cela signifie qu’aucune erreur n’a été trouvée et que l’état de conformité a été correctement signalé.  

    - **Emplacement des erreurs de conformité**: Plus de détails sur l’emplacement où la conformité a échoué. Si cette colonne est vide, cela signifie qu’aucune erreur n’a été trouvée et que l’état de conformité a été correctement signalé. Exemples d’emplacements où le processus de conformité est susceptible d’échouer :  

        - Client ConfigMgr  
        - Point de gestion  
        - Intune  
        - Azure Active Directory  

    - **Heure d’évaluation de conformité**: Heure de la dernière vérification de la conformité.  

    - **Compatibilité défini temps**: Dernière fois où la conformité a été mise à jour vers Azure Active Directory.  

    - **Conformité de l’accès conditionnel**: Indique si la machine est conforme ou non aux stratégies d’accès conditionnel.  

#### <a name="to-view-intune-compliance-policies-charts"></a>Pour afficher les graphiques de stratégies de conformité Intune
1. Dans la console Configuration Manager, choisissez **Surveillance**. 

2. Dans l’espace de travail **Analyse**, accédez à **Vue d’ensemble** > **Paramètres de compatibilité** > **Stratégies de conformité**. Les graphiques suivants s’affichent :  

    - **Conformité globale des appareils**: Affiche la conformité globale des appareils pour toutes les stratégies de conformité.  

    - **Principales raisons de non-conformité**: Affiche les principales stratégies pour lesquelles les appareils ne sont pas conformes.  

3. Choisissez une section dans l’un des deux graphiques pour afficher la liste des appareils dans cette catégorie.  

#### <a name="to-view-a-health-attestation-report"></a>Pour afficher un rapport d’attestation d’intégrité

1. Dans la console Configuration Manager, choisissez **Surveillance**.  

2. Pour afficher un rapport de synthèse sur l’état de conformité actuel des appareils, choisissez **Sécurité**, puis **Attestation d’intégrité**.  

3. Pour afficher un rapport qui répertorie tous les appareils et tous les attributs d’attestation d’intégrité, choisissez **Sécurité**,puis **Attestation d’intégrité**.  



## <a name="compliance-policy-rules"></a>Règles de stratégie de conformité

- **Exiger des paramètres de mot de passe sur les appareils mobiles**: Vous pouvez forcer les utilisateurs à entrer un mot de passe avant qu'ils ne puissent accéder à leur appareil.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exiger un mot de passe pour déverrouiller un appareil inactif**: Vous pouvez forcer les utilisateurs à entrer un mot de passe pour accéder à l’appareil verrouillé.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Minutes d’inactivité avant le mot de passe**: Vous pouvez spécifier la durée d'inactivité au terme de laquelle l'utilisateur doit entrer à nouveau son mot de passe. Définissez la valeur à une des options disponibles : **1 minute**, **5 minutes**, **15 minutes**, **30 minutes**, **1 heure**.  

    Cette règle doit être utilisée avec l’option **Exiger un mot de passe pour déverrouiller un appareil inactif**. La valeur définie ici détermine quand l’appareil est considéré comme inactif puis est verrouillé. Si l’option **Exiger un mot de passe pour déverrouiller un appareil inactif**  est définie sur **True**, l’utilisateur doit entrer un mot de passe pour accéder à l’appareil verrouillé.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - Windows RT/8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exiger les mises à jour automatiques**: Vous pouvez exiger que des appareils disposant de Windows 8.1 ou version ultérieure installent automatiquement les mises à jour, et spécifier la classe de celles-ci.  

    La valeur doit être définie sur **Aucun** pour empêcher l’installation automatique. Elle doit être définie sur **Recommandé** pour installer automatiquement toutes les mises à jour recommandées. Pour installer uniquement les mises à jour marquées comme importantes, définissez la valeur sur **Important**.  

    **Prise en charge sur**:  
    - Windows Phone 8+  

- **Autoriser les mots de passe simples**: Vous pouvez autoriser les utilisateurs à créer des mots de passe simples, comme « 1234 » ou « 1111 ». Ce paramètre est désactivé par défaut.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - iOS 6+  

- **Longueur minimale de mot de passe**: Vous pouvez spécifier le nombre minimal de chiffres ou de caractères que le mot de passe de l'utilisateur doit contenir (6 par défaut).  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

    > [!NOTE]  
    > Pour les appareils qui exécutent Windows et qui sont sécurisés avec un compte Microsoft, la stratégie de conformité n’est pas évaluée correctement si l’option **Longueur minimale du mot de passe** a une valeur supérieure à 8 caractères ou si l’option **Nombre minimum de jeux de caractères** a une valeur supérieure à 2.  

- **Chiffrement des fichiers sur le périphérique mobile**: Vous pouvez exiger le chiffrement de l'appareil pour la connexion aux ressources. Les appareils qui exécutent Windows Phone 8 sont automatiquement chiffrés. Les appareils qui exécutent iOS sont chiffrés quand vous configurez le paramètre **Demander des paramètres de mot de passe sur les périphériques mobiles**. Ce paramètre est activé par défaut.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Appareil ne doit pas être jailbreaké ou rooté**: Si vous activez ce paramètre, appareils jailbreakés (iOS) ou rootés (Android) ne sont pas conformes. Ce paramètre est désactivé par défaut.  

    **Prise en charge sur**:  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Profil de messagerie doit être géré par Intune**: Lorsque vous définissez cette option sur **Oui**, l’appareil doit utiliser le profil d’e-mail déployé sur l’appareil. L’appareil est considéré comme non conforme si le profil d’e-mail n’est pas déployé sur le groupe d’utilisateurs ciblé par la stratégie de conformité.  

    Il est également non conforme si l’utilisateur a déjà défini un compte de messagerie sur l’appareil qui correspond au profil de messagerie Intune déployé sur l’appareil. Dans ce cas, Intune ne peut pas remplacer le profil provisionné par l’utilisateur et ne peut donc pas le gérer. L’utilisateur peut mettre l’appareil en conformité en supprimant les paramètres de messagerie existants, ce qui permet à Intune d’installer le profil de messagerie géré.  

    Pour plus d’informations sur les profils de messagerie, consultez [activer l’accès à la messagerie d’entreprise à l’aide de profils de messagerie avec Microsoft Intune](https://docs.microsoft.com/intune/email-settings-configure). Ce paramètre est désactivé par défaut.  

    **Prise en charge sur**:  
    - iOS 6+  

- **Profil de messagerie**: Si l'option **Le compte de messagerie doit être géré par Intune** est sélectionnée, choisissez **Sélectionner** pour choisir le profil de messagerie qui doit gérer les appareils. Le profil de messagerie doit être présent sur l'appareil.  

    **Prise en charge sur**:  
    - iOS 6+  

- **Système d’exploitation minimal requis**: Quand un appareil ne satisfait la condition de version minimale du système d’exploitation que vous spécifiez, il est signalé comme non conforme. Un lien avec des informations sur la mise à niveau s’affiche. L’utilisateur peut choisir de mettre à niveau son appareil. Une fois cette opération effectuée, il peut accéder aux ressources de l’entreprise.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Version du système d’exploitation maximale autorisée**: Quand un appareil utilise une version du système d’exploitation ultérieure à celle que vous spécifiez dans la règle, l’accès aux ressources de l’entreprise est bloqué et l’utilisateur est invité à contacter son administrateur. Tant que vous n’avez pas modifié la règle pour autoriser la version du système d’exploitation, cet appareil ne peut pas être utilisé pour accéder aux ressources de l’entreprise.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - Windows 8.1  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exiger que les appareils soient signalés comme intègres**: Vous pouvez définir une règle exigeant que les appareils Windows 10 soient signalés comme intègres dans les stratégies de conformité nouvelles ou existantes. Si vous activez ce paramètre, les appareils Windows 10 sont évalués via le service d’attestation d’intégrité pour les points de données suivants :  

    - **BitLocker est activé**: Lorsque BitLocker est activé, l’appareil peut protéger les données stockées sur le lecteur contre tout accès non autorisé, lorsque le système est mis hors tension ou en veille prolongée.  

        Le chiffrement de lecteur BitLocker Windows chiffre toutes les données stockées sur le volume hébergeant le système d’exploitation Windows. BitLocker utilise le Module de plateforme sécurisée (TPM) pour protéger le système d’exploitation Windows et les données utilisateur. Il contribue également à prévenir la falsification d’un ordinateur, même si celui-ci est laissé sans assistance, perdu ou volé.  

        Si l’ordinateur est équipé d’un TPM compatible, BitLocker utilise celui-ci pour verrouiller les clés de chiffrement qui protègent les données. Par conséquent, les clés sont inaccessibles tant que le TPM n’a pas vérifié l’état de l’ordinateur.  

    - **L’intégrité du code est activée**: L’intégrité du code est une fonctionnalité qui valide l’intégrité d’un fichier de pilote ou système chaque fois qu’il est chargé en mémoire. L’intégrité du code détecte si un pilote ou un fichier système non signé est chargé dans le noyau. Elle détecte également si un fichier système a été modifié par un logiciel malveillant exécuté par un compte d’utilisateur disposant de privilèges d’administrateur.  

    - **Le démarrage sécurisé est activé**: Lorsque le démarrage sécurisé est activé, le système est contraint de démarrer dans un état approuvé par défaut. En outre, lorsque le démarrage sécurisé est activé, les composants principaux utilisés pour démarrer la machine doivent avoir des signatures de chiffrement appropriées, approuvées par le fabricant de l’appareil. Le microprogramme UEFI vérifie cela avant de laisser la machine démarrer. Si tous les fichiers ont été falsifiés, leur signature, le système ne démarre pas.  

    - **Logiciel anti-programme malveillant à lancement anticipé est activé**: Ce paramètre s’applique uniquement aux PC. Le logiciel anti-programme malveillant à lancement anticipé assure la protection des ordinateurs de votre réseau au démarrage et avant l’initialisation de pilotes tiers.  

        Cette règle est désactivée par défaut.  

    Pour plus d’informations, consultez [Healthattestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).  

    **Prise en charge sur**:  
    - Windows 10 et Windows 10 Mobile  

    > [!NOTE]  
    > Depuis Configuration Manager 1802, le centre logiciel affiche l’élément de l’attestation d’intégrité l’appareil n’est pas conforme. <!--1235616-->   
    > ![Conformité des appareils d’attestation d’intégrité dans le centre logiciel](./media/Software-Center-noncompliant.PNG)  

- **Les applications qui ne peut pas être installées sur l’appareil**: Si les utilisateurs installent une application à partir de la liste des applications non conformes de l’administrateur, ils seront bloqués lorsqu’ils tenteront d’accéder à la messagerie de l’entreprise et à d’autres ressources de l’entreprise qui prennent en charge l’accès conditionnel. Cette règle requiert le nom de l’application et l’ID de l’application lors de l’ajout d’une application à la liste des applications non conformes définies par l’administrateur. L’éditeur de l’application peut également être ajouté, mais ce n’est pas obligatoire.  

    **Prise en charge sur**:  
    - iOS 6+  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Type de mot de passe requis**: Spécifie si les utilisateurs doivent créer un mot de passe de type alphanumérique ou numérique. Pour les mots de passe alphanumériques, vous spécifiez également le nombre minimal de jeux de caractères que le mot de passe doit avoir. Les quatre jeux de caractères sont : lettres minuscules, lettres majuscules, symboles et chiffres.  

    **Prise en charge sur**:  
    - Windows Phone 8+  
    - Windows 8.1+  
    - iOS 6+  

- **Bloquer le débogage USB sur appareil**: Vous n’êtes pas obligé de configurer ce paramètre, car le débogage USB est déjà désactivé sur Android pour les appareils de travail.  

    **Prise en charge sur**:  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Bloquer des applications provenant de sources inconnues**: Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues. Vous n’êtes pas obligé de configurer ce paramètre comme appareils Android for Work limitent systématiquement l’installation à partir de sources inconnues.  

    **Prise en charge sur**:  
    - Android 4.0+  
    - Samsung KNOX Standard 4.0+  

- **Exiger l’analyse des menaces sur les applications**: Ce paramètre spécifie que la fonction vérifier les applications est activée sur l’appareil.  

    **Prise en charge sur**:  
    - Android 4.2 à 4.4  
    - Samsung KNOX Standard 4.0+  


### <a name="find-an-app-id"></a>Trouver l’ID d’une application

L’ID d’une application est un identificateur qui identifie de façon unique l’application dans les services d’application Apple et Google. Par exemple, `com.contoso.myapp`. Pour rechercher un ID :

- **Android**: Recherchez l’application ID dans le Google Play la banque des URL qui a été utilisée pour créer l’application. Un exemple d’ID d’application est : `...?id=com.companyname.appname&hl=en`  

- **iOS**  
    1. Rechercher le numéro d’identification dans l’URL du magasin iTunes. Exemple : `/id875948587?mt=8`  

    2. Dans un navigateur web, accédez à l’URL suivante, en remplaçant le chiffre avec le numéro d’identification que vous venez de trouver. Par exemple, `https://itunes.apple.com/lookup?id=875948587`  

    3. Téléchargez et ouvrez le fichier texte.  

    4. Recherchez le texte **bundleId**. Exemple : `"bundleId":"com.companyname.appname"`  

