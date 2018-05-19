---
title: Certificats PKI de déploiement
titleSuffix: Configuration Manager
description: Suivez un exemple de procédure pas à pas pour découvrir comment créer et déployer des certificats PKI utilisés par System Center Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 376d75a2aed5fe0b14b3af309e48a75d8f392c11
ms.sourcegitcommit: defdaf493c1dc5a7a380541bc028fbd2b21c1047
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2018
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-system-center-configuration-manager-windows-server-2008-certification-authority"></a>Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet exemple de déploiement pas à pas utilise une autorité de certification Windows Server 2008. Il contient des procédures qui vous montrent comment créer et déployer les certificats d’infrastructure à clé publique (PKI) utilisés par System Center Configuration Manager. Ces procédures utilisent une autorité de certification d'entreprise (CA) et des modèles de certificats. Les étapes conviennent uniquement à un réseau de test utilisé à des fins de démonstration du concept.  

 Étant donné qu’il n’existe aucune méthode unique de déploiement des certificats requis, consultez la documentation de votre déploiement d’infrastructure à clé publique (PKI) pour prendre connaissance des procédures et des bonnes pratiques liées au déploiement des certificats requis pour un environnement de production. Pour en savoir plus sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

> [!TIP]  
>  Vous pouvez adapter les instructions de cette rubrique aux systèmes d’exploitation autres que ceux décrits dans la section Configuration requise du réseau de test. Toutefois, si vous exécutez l'autorité de certification émettrice sur Windows Server 2012, vous n'êtes pas invité à indiquer la version du modèle de certificat. Spécifiez-la plutôt sous l’onglet **Compatibilité** des propriétés du modèle :  
>   
>  -   **Autorité de certification**: **Windows Server 2003**  
> -   **Destinataire du certificat**: **Windows XP / Server 2003**  

## <a name="in-this-section"></a>Dans cette section  
 Les sections suivantes contiennent des exemples de procédures pas à pas pour créer et déployer les certificats suivants à utiliser avec System Center Configuration Manager :  

 [Configuration requise du réseau de test](#BKMK_testnetworkenvironment)  

 [Présentation des certificats](#BKMK_overview2008)  

 [Déployer le certificat de serveur web pour les systèmes de site qui exécutent IIS](#BKMK_webserver2008_cm2012)  

 [Déployer le certificat de service pour les points de distribution cloud](#BKMK_clouddp2008_cm2012)  

 [Déployer le certificat client pour les ordinateurs Windows](#BKMK_client2008_cm2012)  

 [Déployer le certificat client pour les points de distribution](#BKMK_clientdistributionpoint2008_cm2012)  

 [Déployer le certificat d’inscription pour les appareils mobiles](#BKMK_mobiledevices2008_cm2012)  

 [Déployer les certificats pour AMT](#BKMK_AMT2008_cm2012)  

 [Déployer le certificat client pour les ordinateurs Mac](#BKMK_MacClient_SP1)  

##  <a name="BKMK_testnetworkenvironment"></a> Configuration requise du réseau de test  
 Dans ces instructions étape par étape, les impératifs de configuration sont les suivants :  

-   Le réseau de test exécute les services de domaine Active Directory avec Windows Server 2008, et il est installé en tant que domaine unique au sein d'une même forêt.  

-   Vous disposez d’un serveur membre exécutant Windows Server 2008 Enterprise Edition sur lequel est installé le rôle Services de certificats Active Directory, et il est configuré comme autorité de certification racine d’entreprise.  

-   Un ordinateur équipé de Windows Server 2008 (Standard Edition ou Enterprise Edition, R2 ou version ultérieure) doit être désigné comme serveur membre, et les services Internet (IIS) doivent être installés sur cet ordinateur. Cet ordinateur est le serveur de système de site System Center Configuration Manager que vous configurez avec un nom de domaine complet intranet (pour la prise en charge des connexions clientes sur l’intranet) et un nom de domaine complet Internet si vous devez prendre en charge des appareils mobiles inscrits auprès de System Center Configuration Manager et de clients sur Internet.  

-   Vous disposez d’un client Windows Vista équipé du dernier Service Pack, et cet ordinateur configuré avec un nom d’ordinateur incluant des caractères ASCII est lié au domaine. Cet ordinateur est un ordinateur client System Center Configuration Manager.  

-   Vous pouvez vous connecter sous un compte d’administrateur de domaine racine ou d’entreprise et utiliser ce compte pour effectuer toutes les procédures présentées dans cet exemple de déploiement.  

##  <a name="BKMK_overview2008"></a> Présentation des certificats  
 Le tableau suivant présente les types de certificats PKI pouvant être nécessaires pour System Center Configuration Manager et décrit leur utilisation.  

|Certificat requis|Description du certificat|  
|-----------------------------|-----------------------------|  
|Certificat de serveur Web pour les systèmes de site qui exécutent IIS|Ce certificat permet de chiffrer les données et d'authentifier le serveur auprès des clients. Il doit être installé indépendamment de System Center Configuration Manager sur des serveurs de systèmes de site qui exécutent IIS (Internet Information Services) et qui sont configurés dans System Center Configuration Manager pour utiliser HTTPS.<br /><br /> Pour plus d’informations sur les étapes permettant de configurer et d’installer ce certificat, consultez [Déployer le certificat de serveur web pour les systèmes de site qui exécutent IIS](#BKMK_webserver2008_cm2012) dans cette rubrique.|  
|Certificat de service pour la connexion des clients aux points de distribution cloud|Pour plus d’informations sur les étapes permettant de configurer et d’installer ce certificat, consultez [Déployer le certificat de service pour les points de distribution cloud](#BKMK_clouddp2008_cm2012) dans cette rubrique.<br /><br /> **Important :** Ce certificat est utilisé conjointement avec le certificat de gestion Microsoft Azure. Pour plus d’informations sur le certificat de gestion, consultez [Guide pratique pour créer un certificat de gestion](http://go.microsoft.com/fwlink/p/?LinkId=220281) et [Guide pratique pour ajouter un certificat de gestion à un abonnement Windows Azure](http://go.microsoft.com/fwlink/?LinkId=241722) dans la section Plateforme Windows Azure de MSDN Library.|  
|Certificat client pour les ordinateurs Windows|Ce certificat est utilisé pour authentifier les ordinateurs clients System Center Configuration Manager auprès des systèmes de site qui sont configurés pour utiliser HTTPS. Sur les points de gestion et les points de migration d’état, il permet de surveiller leur état de fonctionnement quand ils sont configurés pour utiliser HTTPS. Il doit être installé indépendamment de System Center Configuration Manager sur les ordinateurs.<br /><br /> Pour plus d’informations sur les étapes permettant de configurer et d’installer ce certificat, consultez [Déployer le certificat client pour les ordinateurs Windows](#BKMK_client2008_cm2012) dans cette rubrique.|  
|Certificat client pour les points de distribution|Ce certificat a deux objectifs :<br /><br /> Ce certificat est utilisé pour authentifier le point de distribution auprès d'un point de gestion HTTPS avant que le point de distribution n'envoie des messages d'état.<br /><br /> Lorsque l'option du point de distribution **Activer la prise en charge PXE pour les clients** est sélectionnée, le certificat est envoyé aux ordinateurs qui effectuent un démarrage PXE afin qu'ils puissent se connecter à un point de gestion HTTPS pendant le déploiement du système d'exploitation.<br /><br /> Pour plus d’informations sur les étapes permettant de configurer et d’installer ce certificat, consultez [Déployer le certificat client pour les points de distribution](#BKMK_clientdistributionpoint2008_cm2012) dans cette rubrique.|  
|Certificat d'inscription pour les appareils mobiles|Ce certificat est utilisé pour authentifier les clients d’appareils mobiles System Center Configuration Manager auprès des systèmes de site qui sont configurés pour utiliser HTTPS. Il doit être installé dans le cadre de l’inscription d’appareil mobile dans System Center Configuration Manager. Ensuite, vous choisissez le modèle de certificat configuré comme paramètre de client d’appareil mobile.<br /><br /> Pour plus d’informations sur les étapes permettant de configurer ce certificat, consultez [Déployer le certificat d’inscription pour les appareils mobiles](#BKMK_mobiledevices2008_cm2012) dans cette rubrique.|  
|Certificats pour Intel AMT|Trois certificats sont associés à la gestion hors bande pour les ordinateurs Intel AMT :<ul><li>un certificat de configuration AMT (Active Management Technology) ;</li><li>un certificat de serveur web AMT ;</li><li>en option, un certificat d’authentification client pour les réseaux filaires ou sans fil 802.1X.</li></ul>Le certificat de configuration AMT doit être installé indépendamment de System Center Configuration Manager sur l’ordinateur de point de service hors bande. Ensuite, vous choisissez le certificat installé dans les propriétés du point de service hors bande. Le certificat de serveur web AMT ainsi que le certificat d’authentification client sont installés pendant la configuration et la gestion d’AMT. Ensuite, vous choisissez les modèles de certificats configurés dans les propriétés du composant de gestion hors bande.<br /><br /> Pour plus d’informations sur les étapes permettant de configurer ces certificats, consultez [Déployer les certificats pour AMT](#BKMK_AMT2008_cm2012) dans cette rubrique.|  
|Certificat client pour les ordinateurs Mac|Vous pouvez obtenir et installer ce certificat à partir d’un ordinateur Mac quand vous utilisez l’inscription System Center Configuration Manager. Ensuite, vous choisissez le modèle de certificat configuré comme paramètre de client d’appareil mobile.<br /><br /> Pour plus d’informations sur les étapes permettant de configurer ce certificat, consultez [Déployer le certificat client pour les ordinateurs Mac](#BKMK_MacClient_SP1) dans cette rubrique.|  

##  <a name="BKMK_webserver2008_cm2012"></a> Déployer le certificat de serveur web pour les systèmes de site qui exécutent IIS  
 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Créer et émettre le modèle de certificat de serveur web sur l’autorité de certification  

-   Demander le certificat de serveur web  

-   Configurer IIS en vue d’utiliser le certificat de serveur web  

###  <a name="BKMK_webserver22008"></a> Créer et émettre le modèle de certificat de serveur web sur l’autorité de certification  
 Cette procédure crée un modèle de certificat pour les systèmes de site System Center Configuration Manager et l’ajoute à l’autorité de certification.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat de serveur Web sur l'autorité de certification  

1.  Créez un groupe de sécurité nommé **Serveurs ConfigMgr IIS** qui contient les serveurs membres où installer les systèmes de site System Center Configuration Manager qui vont exécuter IIS.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console **Modèles de certificats**.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat de serveur web ConfigMgr**) pour générer les certificats web à utiliser sur les systèmes de site Configuration Manager.  

6.  Choisissez l’onglet **Nom de l’objet** et vérifiez que l’option **Fournir dans la demande** est sélectionnée.  

7.  Sous l’onglet **Sécurité**, supprimez l’autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l’entreprise**.  

8.  Choisissez **Ajouter**, entrez **Serveurs ConfigMgr IIS** dans la zone de texte, puis choisissez **OK**.  

9. Choisissez l’autorisation **Inscription** pour ce groupe et ne désactivez pas l’autorisation **Lecture**.  

10. Choisissez **OK**, puis fermez la **console Modèles de certificats**.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat de serveur web ConfigMgr**, puis choisissez **OK**.  

13. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

###  <a name="BKMK_webserver32008"></a> Demander le certificat de serveur web  
 Cette procédure vous permet de spécifier les valeurs de nom de domaine complet intranet et Internet qui seront configurées dans les propriétés de serveur de système de site, puis installe le certificat de serveur web sur le serveur membre qui exécute IIS.  

##### <a name="to-request-the-web-server-certificate"></a>Pour demander le certificat de serveur Web  

1.  Redémarrez le serveur membre qui exécute IIS pour vérifier que l’ordinateur peut accéder au modèle de certificat créé via les autorisations **Lecture** et **Inscription** configurées.  

2.  Choisissez **Démarrer**, **Exécuter**, puis tapez **mmc.exe.** Dans la console vide, choisissez **Fichier**, puis **Ajouter/Supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis **Ajouter**.  

4.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats**, choisissez **Compte d’ordinateur**, puis **Suivant**.  

5.  Dans la boîte de dialogue **Sélectionner un ordinateur**, vérifiez que l’option **L’ordinateur local (l’ordinateur sur lequel cette console s’exécute)** est sélectionnée, puis choisissez **Terminer**.  

6.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **OK**.  

7.  Dans la console, développez **Certificats (ordinateur local)**, puis choisissez **Personnel**.  

8.  Cliquez avec le bouton droit sur **Certificats**, choisissez **Toutes les tâches**, puis **Demander un nouveau certificat**.  

9. Dans la page **Avant de commencer**, choisissez **Suivant**.  

10. Si vous voyez la page **Sélectionner la stratégie d’inscription de certificat**, choisissez **Suivant**.  

11. Dans la page **Demander des certificats**, identifiez le **Certificat de serveur web ConfigMgr** dans la liste des certificats disponibles, puis choisissez **L’inscription pour obtenir ce certificat nécessite des informations supplémentaires. Cliquez ici pour configurer les paramètres**.  

12. Dans la boîte de dialogue **Propriétés du certificat**, dans l’onglet **Objet**, n’apportez pas de modifications à **Nom de l’objet**. Cela signifie que la zone **Valeur** de la section **Nom d'objet** reste vierge. Au lieu de cela, dans la section **Autre nom**, choisissez la liste déroulante **Type**, puis **DNS**.  

13. Dans la zone **Valeur**, spécifiez les valeurs de nom de domaine complet que vous allez indiquer dans les propriétés de système de site System Center Configuration Manager, puis choisissez **OK** pour fermer la boîte de dialogue **Propriétés du certificat**.  

     Exemples :  

    -   Si le système de site accepte uniquement les connexions clientes à partir de l’intranet et que le nom de domaine complet intranet du serveur de système de site est **server1.internal.contoso.com**, entrez **server1.internal.contoso.com**, puis choisissez **Ajouter**.  

    -   Si le système de site accepte uniquement les connexions client à partir de l'Intranet et d'Internet, et le nom de domaine complet Intranet du serveur de système de site est **server1.internal.contoso.com** , et le nom de domaine complet Internet du serveur de système de site est **server.contoso.com**:  

        1.  Entrez **server1.internal.contoso.com**, puis choisissez **Ajouter**.  

        2.  Entrez **server.contoso.com**, puis choisissez **Ajouter**.  

        > [!NOTE]  
        >  Vous pouvez spécifier les noms de domaine complets pour System Center Configuration Manager dans n’importe quel ordre. Cependant, vérifiez que tous les appareils qui utiliseront le certificat, tels que les appareils mobiles et les serveurs web proxy, peuvent utiliser un autre nom de l’objet (SAN) du certificat et plusieurs valeurs dans cet autre nom. Si la prise en charge par les appareils des valeurs SAN dans les certificats est limitée, envisagez de modifier l'ordre des noms de domaine complets ou utilisez la valeur Objet à la place.  

14. Dans la page **Demander des certificats**, choisissez **Certificat de serveur web ConfigMgr** dans la liste des certificats disponibles, puis choisissez **Inscrire**.  

15. Dans la page **Résultats de l’installation des certificats**, attendez que le certificat soit installé, puis choisissez **Terminer**.  

16. Fermez la fenêtre **Certificats (ordinateur local)**.  

###  <a name="BKMK_webserver42008"></a> Configurer IIS en vue d’utiliser le certificat de serveur web  
 Cette procédure lie le certificat installé au **Site Web par défaut**IIS.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>Pour configurer IIS en vue d’utiliser le certificat de serveur web  

1.  Sur le serveur membre sur lequel IIS est installé, choisissez **Démarrer**, **Programmes**, **Outils d’administration**, puis **Gestionnaire des services Internet (IIS)**.  

2.  Développez **Sites**, cliquez avec le bouton droit sur **Site Web par défaut**, puis choisissez **Modifier les liaisons**.  

3.  Choisissez l’entrée **https**, puis **Modifier**.  

4.  Dans la boîte de dialogue **Modifier la liaison de site**, sélectionnez le certificat que vous avez demandé à l’aide du modèle Certificat de serveur web ConfigMgr, puis choisissez **OK**.  

    > [!NOTE]  
    >  Si vous ne savez pas quel est le certificat correct, choisissez-en un, puis choisissez **Afficher**. Cela vous permet de comparer les détails du certificat sélectionné aux certificats affichés dans le composant logiciel enfichable Certificats. Par exemple, le composant logiciel enfichable Certificats affiche le modèle de certificat qui a été utilisé pour demander le certificat. Vous pouvez ensuite comparer l’empreinte numérique du certificat qui a été demandé en utilisant le modèle Certificat de serveur web ConfigMgr à l’empreinte numérique du certificat actuellement sélectionné dans la boîte de dialogue **Modifier la liaison de site**.  

5.  Choisissez **OK** dans la boîte de dialogue **Modifier la liaison de site**, puis **Fermer**.  

6.  Fermez le **Gestionnaire des services Internet (IIS)**.  

 Le serveur membre est désormais configuré avec un certificat de serveur web System Center Configuration Manager.  

> [!IMPORTANT]  
>  Quand vous installez le serveur de système de site System Center Configuration Manager sur cet ordinateur, assurez-vous de spécifier le même nom de domaine complet dans les propriétés de système de site que vous avez spécifié lors de la demande du certificat.  

##  <a name="BKMK_clouddp2008_cm2012"></a> Déployer le certificat de service pour les points de distribution cloud  

Les procédures de ce déploiement de certificat sont les suivantes :  

-   [Créer et émettre un modèle de certificat de serveur web personnalisé sur l’autorité de certification](#BKMK_clouddpcreating2008)  

-   [Demander le certificat de serveur web personnalisé](#BKMK_clouddprequesting2008)  

-   [Exporter le certificat de serveur web personnalisé pour les points de distribution cloud](#BKMK_clouddpexporting2008)  

###  <a name="BKMK_clouddpcreating2008"></a> Créer et émettre un modèle de certificat de serveur web personnalisé sur l’autorité de certification  
 Cette procédure permet de créer un modèle de certificat personnalisé basé sur le modèle de certificat de serveur web. Le certificat est destiné aux points de distribution cloud System Center Configuration Manager, et la clé privée doit être exportable. Vous devez ajouter le modèle de certificat à l'autorité de certification après sa création.  

> [!NOTE]  
>  Cette procédure utilise un modèle de certificat différent du modèle de certificat de serveur web créé pour les systèmes de site qui exécutent IIS. Même si les deux certificats nécessitent une fonctionnalité d’authentification du serveur, le certificat pour les points de distribution cloud vous demande d’entrer une valeur définie personnalisée dans le champ Nom de l’objet et la clé privée doit être exportée. Comme bonne pratique de sécurité, ne configurez pas les modèles de certificats pour autoriser l’exportation de la clé privée, sauf si cette configuration est requise. Le point de distribution cloud nécessite cette configuration, car vous devez importer le certificat en tant que fichier, au lieu de le choisir dans le magasin de certificats.  
>   
>  Quand vous créez un modèle de certificat pour ce certificat, vous pouvez limiter les ordinateurs qui peuvent demander un certificat dont la clé privée peut être exportée. Sur un réseau de production, vous pouvez également envisager d’apporter les modifications suivantes à ce certificat :  
>   
>  -   Demander l’approbation d’installer le certificat, pour plus de sécurité.  
> -   Augmenter la période de validité du certificat. Étant donné que vous devez exporter, puis importer le certificat chaque fois avant son expiration, une augmentation de la période de validité permet de réduire la fréquence de cette procédure. Cependant, une augmentation de la période de validité diminue également la sécurité du certificat, car une personne malveillante a plus de temps pour déchiffrer la clé privée et voler le certificat.  
> -   Utilisez une valeur personnalisée dans le champ Autre nom de l'objet pour aider à identifier ce certificat parmi les certificats de serveur Web standard que vous utilisez avec IIS.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat de serveur web personnalisé sur l’autorité de certification  

1.  Créez un groupe de sécurité nommé **Serveurs de site ConfigMgr** qui contient les serveurs membres où installer les serveurs de site principal System Center Configuration Manager qui vont gérer les points de distribution cloud.  

2.  Sur le serveur membre qui exécute la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console de gestion des modèles de certificats.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat de point de distribution cloud ConfigMgr**) pour générer le certificat de serveur web pour les points de distribution cloud.  

6.  Choisissez l’onglet **Traitement de la demande**, puis **Autoriser l’exportation de la clé privée**.  

7.  Choisissez l’onglet **Sécurité** et supprimez l’autorisation **Inscription** du groupe de sécurité **Administrateurs de l’entreprise**.  

8.  Choisissez **Ajouter**, entrez **Serveurs de site ConfigMgr** dans la zone de texte, puis choisissez **OK**.  

9. Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

    > [!NOTE]
    > Vérifiez que l’option **Taille de clé minimale** sous l’onglet **Chiffrement** a été définie sur **2048**

10. Choisissez **OK**, puis fermez la **console Modèles de certificats**.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat de point de distribution cloud ConfigMgr**, puis choisissez **OK**.  

13. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

###  <a name="BKMK_clouddprequesting2008"></a> Demander le certificat de serveur web personnalisé  
 Cette procédure permet de demander, puis d’installer le certificat de serveur web personnalisé sur le serveur membre qui exécutera le serveur de site.  

##### <a name="to-request-the-custom-web-server-certificate"></a>Pour demander le certificat de serveur Web personnalisé  

1.  Redémarrez le serveur membre après avoir créé et configuré le groupe de sécurité **Serveurs de site ConfigMgr** pour vérifier que l’ordinateur peut accéder au modèle de certificat créé via les autorisations **Lecture** et **Inscription** configurées.  

2.  Choisissez **Démarrer**, **Exécuter**, puis entrez **mmc.exe.** Dans la console vide, choisissez **Fichier**, puis **Ajouter/Supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis **Ajouter**.  

4.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats**, choisissez **Compte d’ordinateur**, puis **Suivant**.  

5.  Dans la boîte de dialogue **Sélectionner un ordinateur**, vérifiez que l’option **L’ordinateur local (l’ordinateur sur lequel cette console s’exécute)** est sélectionnée, puis choisissez **Terminer**.  

6.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **OK**.  

7.  Dans la console, développez **Certificats (ordinateur local)**, puis choisissez **Personnel**.  

8.  Cliquez avec le bouton droit sur **Certificats**, choisissez **Toutes les tâches**, puis **Demander un nouveau certificat**.  

9. Dans la page **Avant de commencer**, choisissez **Suivant**.  

10. Si vous voyez la page **Sélectionner la stratégie d’inscription de certificat**, choisissez **Suivant**.  

11. Dans la page **Demander des certificats**, identifiez le **Certificat de point de distribution cloud ConfigMgr** dans la liste des certificats disponibles, puis choisissez **L’inscription pour obtenir ce certificat nécessite des informations supplémentaires. Cliquez ici pour configurer les paramètres**.  

12. Dans la boîte de dialogue **Propriétés du certificat**, dans l’onglet **Objet**, choisissez **Nom commun** pour le champ **Nom de l’objet** comme **Type**.  

13. Dans le champ **Valeur** , spécifiez un nom de service et votre nom de domaine à l'aide d'un format de nom de domaine complet. Par exemple : **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Le nom de service doit être unique dans votre espace de noms. Utilisez le système de noms de domaine pour créer un alias (enregistrement CNAME) pour mapper le nom de ce service à un identificateur (GUID) généré automatiquement et une adresse IP à partir de Windows Azure.  

14. Choisissez **Ajouter**, puis **OK** pour fermer la boîte de dialogue **Propriétés du certificat**.  

15. Dans la page **Demander des certificats**, choisissez **Certificat de point de distribution cloud ConfigMgr** dans la liste des certificats disponibles, puis choisissez **Inscrire**.  

16. Dans la page **Résultats de l’installation des certificats**, attendez que le certificat soit installé, puis choisissez **Terminer**.  

17. Fermez la fenêtre **Certificats (ordinateur local)**.  

###  <a name="BKMK_clouddpexporting2008"></a> Exporter le certificat de serveur web personnalisé pour les points de distribution cloud  
 Cette procédure permet d'exporter le certificat de serveur Web personnalisé dans un fichier, afin qu'il puisse être importé lorsque vous créez le point de distribution cloud.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>Pour exporter le certificat de serveur Web personnalisé pour les points de distribution cloud  

1.  Dans la console **Certificats (ordinateur local)**, cliquez avec le bouton droit sur le certificat que vous venez d’installer, choisissez **Toutes les tâches**, puis **Exporter**.  

2.  Dans l’Assistant Exportation de certificats, choisissez **Suivant**.  

3.  Dans la page **Exporter la clé privée**, choisissez **Oui, exporter la clé privée**, puis **Suivant**.  

    > [!NOTE]  
    >  Si cette option n'est pas disponible, cela signifie que le certificat a été créé sans l'option permettant d'exporter la clé privée. Dans ce scénario, vous ne pouvez pas exporter le certificat dans le format requis. Vous devez configurer le modèle de certificat pour autoriser l’exportation de la clé privée, puis redemander le certificat.  

4.  Dans la page **Format de fichier d’exportation**, vérifiez que l’option **Échange d’informations personnelles - PKCS #12 (.PFX)** est sélectionnée.  

5.  Dans la page **Mot de passe**, spécifiez un mot de passe fort pour protéger le certificat exporté avec sa clé privée, puis choisissez **Suivant**.  

6.  Dans la page **Fichier à exporter**, spécifiez le nom du fichier que vous voulez exporter, puis choisissez **Suivant**.  

7.  Pour fermer l’Assistant, choisissez **Terminer** dans la page **Assistant Exportation de certificat**, puis **OK** dans la boîte de dialogue de confirmation.  

8.  Fermez la fenêtre **Certificats (ordinateur local)**.  

9. Stockez le fichier de façon sécurisée et vérifiez que vous pouvez y accéder à partir de la console System Center Configuration Manager.  

 Le certificat est prêt à l'importation dès que vous créez un point de distribution cloud.  

##  <a name="BKMK_client2008_cm2012"></a> Déployer le certificat client pour les ordinateurs Windows  
 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Créer et émettre le modèle de certificat Authentification de station de travail sur l’autorité de certification  

-   Configurer l’inscription automatique du modèle Authentification de station de travail à l’aide d’une stratégie de groupe  

-   Inscrire automatiquement le certificat Authentification de station de travail et vérifier son installation sur les ordinateurs  

###  <a name="BKMK_client02008"></a> Créer et émettre le modèle de certificat Authentification de station de travail sur l’autorité de certification  
 Cette procédure crée un modèle de certificat pour les ordinateurs clients System Center Configuration Manager et l’ajoute à l’autorité de certification.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat d’authentification de station de travail sur l’autorité de certification  

1.  Sur le serveur membre qui exécute la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console de gestion des modèles de certificats.  

2.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Authentification de station de travail** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

3.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

4.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat client ConfigMgr**) pour générer les certificats clients à utiliser sur les ordinateurs clients Configuration Manager.  

5.  Choisissez l’onglet **Sécurité**, sélectionnez le groupe **Ordinateurs du domaine**, puis les autorisations supplémentaires **Lecture** et **Inscription automatique**. Ne désactivez pas l'option **Inscrire**.  

6.  Choisissez **OK**, puis fermez la **console Modèles de certificats**.  

7.  Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

8.  Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat client ConfigMgr**, puis choisissez **OK**.  

9. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

###  <a name="BKMK_client12008"></a> Configurer l’inscription automatique du modèle Authentification de station de travail à l’aide d’une stratégie de groupe  
 Cette procédure permet de configurer la stratégie de groupe pour inscrire automatiquement le certificat client sur les ordinateurs.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>Pour configurer l’inscription automatique du modèle Authentification de station de travail à l’aide d’une stratégie de groupe  

1.  Sur le contrôleur de domaine, choisissez **Démarrer**, **Outils d’administration**, puis **Gestion des stratégies de groupe**.  

2.  Accédez à votre domaine, cliquez dessus avec le bouton droit, puis choisissez **Créer un objet GPO dans ce domaine, et le lier ici**.  

    > [!NOTE]  
    >  Cette étape utilise la bonne pratique permettant de créer une stratégie de groupe pour des paramètres personnalisés ; elle ne modifie pas la stratégie de domaine par défaut qui est installée avec les services de domaine Active Directory. Quand vous affectez cette stratégie de groupe au niveau du domaine, vous l’appliquez à tous les ordinateurs de ce domaine. Dans un environnement de production, vous pouvez limiter l’inscription automatique aux ordinateurs sélectionnés. Vous pouvez affecter la stratégie de groupe au niveau d’une unité d’organisation, ou vous pouvez filtrer la stratégie de groupe du domaine avec un groupe de sécurité pour qu’elle s’applique uniquement aux ordinateurs du groupe. Si vous limitez l’inscription automatique, veillez à inclure le serveur configuré comme point de gestion.  

3.  Dans la boîte de dialogue **Nouvel objet GPO**, entrez un nom pour la nouvelle stratégie de groupe, par exemple **Certificats - Inscription automatique**, puis choisissez **OK**.  

4.  Dans le volet des résultats, sous l’onglet **Objets de stratégie de groupe liés**, cliquez avec le bouton droit sur la nouvelle stratégie de groupe, puis choisissez **Modifier**.  

5.  Dans l’**Éditeur de gestion des stratégies de groupe**, développez **Stratégies** sous **Configuration ordinateur**, puis accédez à **Paramètres Windows** / **Paramètres de sécurité** / **Stratégies de clé publique**.  

6.  Cliquez avec le bouton droit sur le type d’objet nommé **Client des services de certificats - Inscription automatique**, puis choisissez **Propriétés**.  

7.  Dans la liste déroulante **Modèle de configuration**, choisissez **Activé**, **Renouveler les certificats expirés, mettre à jour les certificats en attente et supprimer les certificats révoqués**, **Mettre à jour les certificats qui utilisent les modèles de certificats**, puis **OK**.  

8.  Fermez la fenêtre **Gestion des stratégies de groupe**.  

###  <a name="BKMK_client22008"></a> Inscrire automatiquement le certificat Authentification de station de travail et vérifier son installation sur les ordinateurs  
 Cette procédure permet d'installer le certificat client sur les ordinateurs et de vérifier l'installation.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>Pour inscrire automatiquement le certificat Authentification de station de travail et vérifier son installation sur l’ordinateur client  

1.  Redémarrez la station de travail et attendez quelques minutes avant de vous connecter.  

    > [!NOTE]  
    >  Le redémarrage de l'ordinateur constitue la méthode la plus fiable pour l'inscription automatique des certificats.  

2.  Connectez-vous avec un compte disposant de privilèges d’administrateur.  

3.  Dans la zone de recherche, entrez **mmc.exe.** et appuyez sur **Entrée**.  

4.  Dans la console de gestion vide, choisissez **Fichier**, puis **Ajouter/Supprimer un composant logiciel enfichable**.  

5.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis **Ajouter**.  

6.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats**, choisissez **Compte d’ordinateur**, puis **Suivant**.  

7.  Dans la boîte de dialogue **Sélectionner un ordinateur**, vérifiez que l’option **L’ordinateur local (l’ordinateur sur lequel cette console s’exécute)** est sélectionnée, puis choisissez **Terminer**.  

8.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **OK**.  

9. Dans la console, développez **Certificats (ordinateur local)**, **Personnel**, puis choisissez **Certificats**.  

10. Dans le volet des résultats, vérifiez qu’un certificat indique **Authentification du client** dans la colonne **Rôle prévu** et que **Certificat client ConfigMgr** figure dans la colonne **Modèle de certificat**.  

11. Fermez la fenêtre **Certificats (ordinateur local)**.  

12. Répétez les étapes 1 à 11 pour le serveur membre afin de vérifier que le serveur qui sera configuré comme point de gestion dispose également d’un certificat client.  

 L’ordinateur est maintenant configuré avec un certificat client System Center Configuration Manager.  

##  <a name="BKMK_clientdistributionpoint2008_cm2012"></a> Déployer le certificat client pour les points de distribution  

> [!NOTE]  
>  Ce certificat peut également être utilisé pour les images de média qui n'utilisent pas le démarrage PXE, car la configuration requise pour le certificat est la même.  

 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Créer et émettre un modèle de certificat Authentification de station de travail personnalisé sur l’autorité de certification  

-   Demander le certificat Authentification de station de travail personnalisé  

-   Exporter le certificat client pour les points de distribution  

###  <a name="BKMK_clientdistributionpoint02008"></a> Créer et émettre un modèle de certificat Authentification de station de travail personnalisé sur l’autorité de certification  
 Cette procédure permet de créer un modèle de certificat personnalisé pour les points de distribution System Center Configuration Manager afin que la clé privée puisse être exportée, et d’ajouter le modèle de certificat à l’autorité de certification.  

> [!NOTE]  
>  Cette procédure utilise un modèle de certificat différent du modèle de certificat créé pour les ordinateurs clients. Même si les deux certificats nécessitent une fonctionnalité d’authentification du client, le certificat pour les points de distribution requiert l’exportation de la clé privée. Comme bonne pratique de sécurité, ne configurez pas les modèles de certificats pour autoriser l’exportation de la clé privée, sauf si cette configuration est requise. Le point de distribution nécessite cette configuration, car vous devez importer le certificat en tant que fichier, au lieu de le choisir dans le magasin de certificats.  
>   
>  Quand vous créez un modèle de certificat pour ce certificat, vous pouvez limiter les ordinateurs qui peuvent demander un certificat dont la clé privée peut être exportée. Dans notre exemple de déploiement, il s’agit du groupe de sécurité que vous avez créé précédemment pour les serveurs de système de site System Center Configuration Manager qui exécutent IIS. Sur un réseau de production qui distribue les rôles de système de site IIS, envisagez de créer un groupe de sécurité pour les serveurs exécutant des points de distribution, afin de limiter le certificat à ces serveurs de système de site uniquement. Vous pouvez également considérer d'apporter les modifications suivantes à ce certificat :  
>   
>  -   Demander l’approbation d’installer le certificat, pour plus de sécurité.  
> -   Augmenter la période de validité du certificat. Étant donné que vous devez exporter, puis importer le certificat chaque fois avant son expiration, une augmentation de la période de validité permet de réduire la fréquence de cette procédure. Cependant, une augmentation de la période de validité diminue également la sécurité du certificat, car une personne malveillante a plus de temps pour déchiffrer la clé privée et voler le certificat.  
> -   Utiliser une valeur personnalisée dans le champ Objet du certificat ou Autre nom de l'objet pour aider à identifier ce certificat parmi les certificats de client standard. Cela peut s'avérer particulièrement utile si vous utilisez le même certificat pour plusieurs points de distribution.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat Authentification de station de travail personnalisé sur l'autorité de certification  

1.  Sur le serveur membre qui exécute la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console de gestion des modèles de certificats.  

2.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Authentification de station de travail** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

3.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

4.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat de point de distribution client ConfigMgr**) pour générer le certificat d’authentification client pour les points de distribution.  

5.  Choisissez l’onglet **Traitement de la demande**, puis **Autoriser l’exportation de la clé privée**.  

6.  Choisissez l’onglet **Sécurité** et supprimez l’autorisation **Inscription** du groupe de sécurité **Administrateurs de l’entreprise**.  

7.  Choisissez **Ajouter**, entrez **Serveurs ConfigMgr IIS** dans la zone de texte, puis choisissez **OK**.  

8.  Sélectionnez l'autorisation **Inscription** pour ce groupe et ne désactivez pas l'autorisation **Lecture** .  

9. Choisissez **OK**, puis fermez la **console Modèles de certificats**.  

10. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

11. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat de point de distribution client ConfigMgr**, puis choisissez **OK**.  

12. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

###  <a name="BKMK_clientdistributionpoint12008"></a> Demander le certificat Authentification de station de travail personnalisé  
 Cette procédure permet de demander, puis d’installer le certificat client personnalisé sur le serveur membre qui exécute IIS et qui sera configuré comme point de distribution.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>Pour demander le certificat d'authentification de station de travail personnalisé  

1.  Choisissez **Démarrer**, **Exécuter**, puis entrez **mmc.exe.** Dans la console vide, choisissez **Fichier**, puis **Ajouter/Supprimer un composant logiciel enfichable**.  

2.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis **Ajouter**.  

3.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats**, choisissez **Compte d’ordinateur**, puis **Suivant**.  

4.  Dans la boîte de dialogue **Sélectionner un ordinateur**, vérifiez que l’option **L’ordinateur local (l’ordinateur sur lequel cette console s’exécute)** est sélectionnée, puis choisissez **Terminer**.  

5.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **OK**.  

6.  Dans la console, développez **Certificats (ordinateur local)**, puis choisissez **Personnel**.  

7.  Cliquez avec le bouton droit sur **Certificats**, choisissez **Toutes les tâches**, puis **Demander un nouveau certificat**.  

8.  Dans la page **Avant de commencer**, choisissez **Suivant**.  

9. Si vous voyez la page **Sélectionner la stratégie d’inscription de certificat**, choisissez **Suivant**.  

10. Dans la page **Demander des certificats**, choisissez **Certificat de point de distribution client ConfigMgr** dans la liste des certificats disponibles, puis choisissez **Inscrire**.  

11. Dans la page **Résultats de l’installation des certificats**, attendez que le certificat soit installé, puis choisissez **Terminer**.  

12. Dans le volet des résultats, vérifiez qu’un certificat indique **Authentification du client** dans la colonne **Rôle prévu** et que **Certificat de point de distribution client ConfigMgr** figure dans la colonne **Modèle de certificat**.  

13. Ne fermez pas la fenêtre **Certificats (ordinateur local)**.  

###  <a name="BKMK_exportclientdistributionpoint22008"></a> Exporter le certificat client pour les points de distribution  
 Cette procédure permet d’exporter le certificat Authentification de station de travail personnalisé vers un fichier afin qu’il puisse être importé dans les propriétés du point de distribution.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>Pour exporter le certificat du client pour les points de distribution  

1.  Dans la console **Certificats (ordinateur local)**, cliquez avec le bouton droit sur le certificat que vous venez d’installer, choisissez **Toutes les tâches**, puis **Exporter**.  

2.  Dans l’Assistant Exportation de certificats, choisissez **Suivant**.  

3.  Dans la page **Exporter la clé privée**, choisissez **Oui, exporter la clé privée**, puis **Suivant**.  

    > [!NOTE]  
    >  Si cette option n'est pas disponible, cela signifie que le certificat a été créé sans l'option permettant d'exporter la clé privée. Dans ce scénario, vous ne pouvez pas exporter le certificat dans le format requis. Vous devez configurer le modèle de certificat pour autoriser l’exportation de la clé privée, puis redemander le certificat.  

4.  Dans la page **Format de fichier d’exportation**, vérifiez que l’option **Échange d’informations personnelles - PKCS #12 (.PFX)** est sélectionnée.  

5.  Dans la page **Mot de passe**, spécifiez un mot de passe fort pour protéger le certificat exporté avec sa clé privée, puis choisissez **Suivant**.  

6.  Dans la page **Fichier à exporter**, spécifiez le nom du fichier que vous voulez exporter, puis choisissez **Suivant**.  

7.  Pour fermer l’Assistant, choisissez **Terminer** dans la page **Assistant Exportation de certificat**, puis **OK** dans la boîte de dialogue de confirmation.  

8.  Fermez la fenêtre **Certificats (ordinateur local)**.  

9. Stockez le fichier de façon sécurisée et vérifiez que vous pouvez y accéder à partir de la console System Center Configuration Manager.  

 Le certificat est maintenant prêt à être importé dès que vous configurez le point de distribution.  

> [!TIP]  
>  Vous pouvez utiliser le même fichier de certificat lors de la configuration d’images de média pour un déploiement de système d’exploitation qui n’utilise pas le démarrage PXE, et la séquence de tâches d’installation de l’image doit contacter un point de gestion qui requiert des connexions clientes HTTPS.  

##  <a name="BKMK_mobiledevices2008_cm2012"></a> Déployer le certificat d’inscription pour les appareils mobiles  
 Ce déploiement de certificat a une procédure unique pour créer et émettre le modèle de certificat d'inscription sur l'autorité de certification.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Créer et émettre le modèle de certificat d’inscription sur l’autorité de certification  
 Cette procédure crée un modèle de certificat d’inscription pour les appareils mobiles System Center Configuration Manager et l’ajoute à l’autorité de certification.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat d'inscription sur l'autorité de certification  

1.  Créez un groupe de sécurité avec des utilisateurs qui vont inscrire des appareils mobiles dans System Center Configuration Manager.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console de gestion Modèles de certificats.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Session authentifiée** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat d’inscription d’appareil mobile ConfigMgr**) pour générer les certificats d’inscription pour les appareils mobiles devant être gérés par System Center Configuration Manager.  

6.  Choisissez l’onglet **Nom de l’objet**, vérifiez que l’option **Construire à partir de ces informations Active Directory** est sélectionnée, sélectionnez **Nom commun** pour **Format du nom de l’objet :**, puis effacez **Nom d’utilisateur principal (UPN)** dans **Inclure cette information dans le nom de substitution du sujet**.  

7.  Choisissez l’onglet **Sécurité**, le groupe de sécurité avec des utilisateurs qui ont des appareils mobiles à inscrire, puis l’autorisation supplémentaire **Inscription**. Ne désactivez pas l'option **Lecture**.  

8.  Choisissez **OK**, puis fermez la **console Modèles de certificats**.  

9. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

10. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat d’inscription d’appareil mobile ConfigMgr**, puis choisissez **OK**.  

11. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez la console Autorité de certification.  

 Le modèle de certificat d’inscription d’appareil mobile est maintenant prêt à être sélectionné dès que vous configurez un profil d’inscription d’appareil mobile dans les paramètres client.  

##  <a name="BKMK_AMT2008_cm2012"></a> Déployer les certificats pour AMT  
 Les procédures de ce déploiement de certificat sont les suivantes :  

-   Créer, émettre et installer le certificat de configuration AMT  

-   Créer et émettre le certificat de serveur web pour les ordinateurs AMT  

-   Créer et émettre les certificats d’authentification clients pour les ordinateurs AMT 802.1X  

###  <a name="BKMK_AMTprovisioning2008"></a> Créer, émettre et installer le certificat de configuration AMT  
 Créez le certificat de configuration avec votre autorité de certification interne quand les ordinateurs AMT sont configurés avec l’empreinte numérique du certificat de votre autorité de certification racine interne. Quand ce n’est pas le cas et que vous devez utiliser une autorité de certification externe, suivez les instructions de la société émettrice du certificat de configuration AMT, qui exige souvent le certificat du site web public de l’entreprise. Vous pouvez également trouver des instructions détaillées sur l’autorité de certification externe que vous avez choisie sur le [site web Intel vPro Expert Center: Microsoft vPro Manageability](http://go.microsoft.com/fwlink/?LinkId=132001).  

> [!IMPORTANT]  
>  Il se peut que des autorités de certification externes ne prennent pas en charge l'identificateur d'objet de configuration Intel AMT. Dans ce cas, fournissez l’attribut de l’unité d’organisation **Intel(R) Client Setup Certificate**.  

 Quand vous demandez un certificat de configuration AMT auprès d’une autorité de certification externe, installez le certificat dans le magasin de certificats personnels de l’ordinateur sur le serveur membre qui va héberger le point de service hors bande.  

##### <a name="to-request-and-issue-the-amt-provisioning-certificate"></a>Pour demander et émettre le certificat de configuration AMT  

1.  Créez un groupe de sécurité qui contient les comptes d’ordinateurs des serveurs de système de site qui exécuteront le point de service hors bande.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console **Modèles de certificats**.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Configuration AMT ConfigMgr**) pour générer le modèle de certificat de configuration AMT.  

6.  Choisissez l’onglet **Nom de l’objet**, **Construire à partir de ces informations Active Directory**, puis **Nom commun**.  

7.  Choisissez l’onglet **Extensions**, vérifiez que l’option **Stratégies d’application** est activée, puis choisissez **Modifier**.  

8.  Dans la boîte de dialogue **Modifier l’extension des stratégies d’application**, choisissez **Ajouter**.  

9. Dans la boîte de dialogue **Ajouter une stratégie d’application**, choisissez **Nouveau**.  

10. Dans la boîte de dialogue **Nouvelle stratégie d’application**, entrez **Configuration AMT** dans le champ **Nom**, puis le numéro suivant dans le champ **Identificateur d’objet** : **2.16.840.1.113741.1.2.3**.  

11. Choisissez **OK**, puis une nouvelle fois **OK** dans la boîte de dialogue **Ajouter une stratégie d’application**.  

12. Choisissez **OK** dans la boîte de dialogue **Modifier l’extension des stratégies d’application**.  

13. Dans la boîte de dialogue **Propriétés du nouveau modèle**, les éléments suivants sont répertoriés comme description de **Stratégies d’application** : **Authentification du serveur** et **Configuration AMT**.  

14. Sous l’onglet **Sécurité**, supprimez l’autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l’entreprise**.  

15. Choisissez **Ajouter**, entrez le nom d’un groupe de sécurité qui contient le compte d’ordinateur pour le rôle de système de site du point de service hors bande, puis choisissez **OK**.  

16. Choisissez l’autorisation **Inscription** pour ce groupe et ne désactivez pas l’autorisation **Lecture**.  

17. Choisissez **OK**, puis fermez la console **Modèles de certificats**.  

18. Dans **Autorité de certification**, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

19. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Configuration AMT ConfigMgr**, puis choisissez **OK**.  

    > [!NOTE]  
    >  Si vous ne pouvez pas effectuer l'étape 18 ou 19, vérifiez que vous utilisez Windows Server 2008 Enterprise Edition. Bien que vous puissiez configurer des modèles dans Windows Server Standard Edition et les services de certificats, vous ne pouvez déployer des certificats à l’aide de modèles de certificats modifiés que dans Windows Server 2008 Enterprise Edition.  

20. Ne fermez pas l' **autorité de certification**.  

 Le certificat de configuration AMT de votre autorité de certification interne est maintenant prêt à être installé sur l’ordinateur du point de service hors bande.  

##### <a name="to-install-the-amt-provisioning-certificate"></a>Pour installer le certificat de configuration AMT  

1.  Redémarrez le serveur membre qui exécute IIS pour vérifier qu’il peut accéder au modèle de certificat via l’autorisation définie.  

2.  Choisissez **Démarrer**, **Exécuter**, puis entrez **mmc.exe.** Dans la console vide, choisissez **Fichier**, puis **Ajouter/Supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **Certificats** dans la liste **Composants logiciels enfichables disponibles**, puis **Ajouter**.  

4.  Dans la boîte de dialogue **Composant logiciel enfichable des certificats**, choisissez **Compte d’ordinateur**, puis **Suivant**.  

5.  Dans la boîte de dialogue **Sélectionner un ordinateur**, vérifiez que l’option **L’ordinateur local (l’ordinateur sur lequel cette console s’exécute)** est sélectionnée, puis choisissez **Terminer**.  

6.  Dans la boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables**, choisissez **OK**.  

7.  Dans la console, développez **Certificats (ordinateur local)**, puis choisissez **Personnel**.  

8.  Cliquez avec le bouton droit sur **Certificats**, choisissez **Toutes les tâches**, puis **Demander un nouveau certificat**.  

9. Dans la page **Avant de commencer**, choisissez **Suivant**.  

10. Si vous voyez la page **Sélectionner la stratégie d’inscription de certificat**, choisissez **Suivant**.  

11. Dans la page **Demander des certificats**, sélectionnez **Configuration AMT** dans la liste des certificats disponibles, puis choisissez **Inscrire**.  

12. Dans la page **Résultats de l’installation des certificats**, attendez que le certificat soit installé, puis choisissez **Terminer**.  

13. Fermez la fenêtre **Certificats (ordinateur local)**.  

 Le certificat de configuration AMT de votre autorité de certification interne est maintenant installé et peut être sélectionné dans les propriétés du point de service hors bande.  

### <a name="create-and-issue-the-web-server-certificate-for-amt-based-computers"></a>Créer et émettre le certificat de serveur web pour les ordinateurs AMT  
 Procédez comme suit pour préparer les certificats de serveur Web pour les ordinateurs basés sur AMT.  

##### <a name="to-create-and-issue-the-web-server-certificate-template"></a>Pour créer et émettre le modèle de certificat de serveur web  

1.  Créez un groupe de sécurité vide qui contient les comptes d’ordinateurs AMT créés par System Center Configuration Manager lors de la configuration AMT.  

2.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console **Modèles de certificats**.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Serveur Web** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition.**  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat de serveur web AMT ConfigMgr**) pour générer les certificats web à utiliser pour la gestion hors bande sur les ordinateurs AMT.  

6.  Choisissez l’onglet **Nom de l’objet**, **Construire à partir de ces informations Active Directory**, **Nom commun** pour **Format du nom de l’objet**, puis effacez **Nom d’utilisateur principal (UPN)** pour l’autre nom de l’objet.  

7.  Sous l’onglet **Sécurité**, supprimez l’autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l’entreprise**.  

8.  Choisissez **Ajouter** et entrez le nom du groupe de sécurité que vous avez créé pour la configuration AMT, puis choisissez **OK**.  

9. Choisissez ces autorisations **Autoriser** applicables à ce groupe de sécurité : **Lecture** et **Inscription**.  

10. Choisissez **OK**, puis fermez la console **Modèles de certificats**.  

11. Dans la console **Autorité de certification**, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat de serveur web AMT ConfigMgr**, puis choisissez **OK**.  

13. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

 Le modèle de serveur web AMT est maintenant prêt pour la configuration d’ordinateurs AMT avec des certificats de serveur web. Choisissez ce modèle de certificat dans les propriétés du composant de gestion hors bande.  

### <a name="create-and-issue-the-client-authentication-certificates-for-8021x-amt-based-computers"></a>Créer et émettre les certificats d’authentification clients pour les ordinateurs AMT 802.1X  
 Utilisez la procédure suivante si les ordinateurs basés sur AMT utilisent des certificats clients pour les réseaux filaires ou sans fil authentifiés par 802.1X.  

##### <a name="to-create-and-issue-the-client-authentication-certificate-template-on-the-ca"></a>Pour créer et émettre le modèle de certificat d'authentification client sur l'autorité de certification  

1.  Sur le serveur membre sur lequel les services de certificats sont installés, dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console **Modèles de certificats**.  

2.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Authentification de station de travail** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition.**  

3.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat d’authentification client AMT 802.1X ConfigMgr**) pour générer les certificats clients à utiliser pour la gestion hors bande sur les ordinateurs AMT.  

4.  Choisissez l’onglet **Nom de l’objet**, **Construire à partir de ces informations Active Directory**, puis **Nom commun** pour **Format du nom de l’objet**. Effacez **Nom DNS** pour l’autre nom de l’objet, puis choisissez **Nom d’utilisateur principal (UPN)**.  

5.  Sous l’onglet **Sécurité**, supprimez l’autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l’entreprise**.  

6.  Choisissez **Ajouter**, entrez le nom du groupe de sécurité que vous spécifiez dans les propriétés du composant de gestion hors bande pour contenir les comptes des ordinateurs AMT, puis choisissez **OK**.  

7.  Sélectionnez ces autorisations **Autoriser** applicables à ce groupe de sécurité : **Lecture** et **Inscription**.  

8.  Choisissez **OK**, puis fermez la console de gestion **Modèles de certificats**, **certtmpl - [Modèles de certificats]**.  

9. Dans la console de gestion **Autorité de certification**, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

10. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat d’authentification client AMT 802.1X ConfigMgr**, puis choisissez **OK**.  

11. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

 Le modèle de certificat d'authentification client est maintenant prêt à émettre des certificats d'ordinateurs AMT utilisables pour l'authentification client 802.1X. Choisissez ce modèle de certificat dans les propriétés du composant de gestion hors bande.  

##  <a name="BKMK_MacClient_SP1"></a> Déployer le certificat client pour les ordinateurs Mac  

Ce déploiement de certificat a une procédure unique pour créer et émettre le modèle de certificat d'inscription sur l'autorité de certification.  

###  <a name="BKMK_MacClient_CreatingIssuing"></a> Créer et émettre un modèle de certificat client Mac sur l’autorité de certification  
 Cette procédure crée un modèle de certificat personnalisé pour les ordinateurs Mac System Center Configuration Manager et l’ajoute à l’autorité de certification.  

> [!NOTE]  
>  Cette procédure utilise un modèle de certificat différent du modèle de certificat que vous avez peut-être créé pour des ordinateurs clients Windows ou pour des points de distribution.  
>   
>  Quand vous créez un modèle de certificat pour ce certificat, vous pouvez limiter la demande de certificat aux utilisateurs autorisés.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>Pour créer et émettre le modèle de certificat client Mac sur l'autorité de certification  

1.  Créez un groupe de sécurité qui contient les comptes des utilisateurs administratifs qui vont inscrire le certificat sur l’ordinateur Mac à l’aide de System Center Configuration Manager.  

2.  Sur le serveur membre qui exécute la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, puis choisissez **Gérer** pour charger la console de gestion des modèles de certificats.  

3.  Dans le volet des résultats, cliquez avec le bouton droit sur l’entrée qui affiche **Session authentifiée** dans la colonne **Nom complet du modèle**, puis choisissez **Dupliquer le modèle**.  

4.  Dans la boîte de dialogue **Dupliquer le modèle**, vérifiez que l’option **Windows Server 2003, Enterprise Edition** est sélectionnée, puis choisissez **OK**.  

    > [!IMPORTANT]  
    >  Ne sélectionnez pas **Windows Server 2008, Enterprise Edition**.  

5.  Dans la boîte de dialogue **Propriétés du nouveau modèle**, sous l’onglet **Général**, entrez un nom de modèle (par exemple, **Certificat client Mac ConfigMgr**) pour générer le certificat client Mac.  

6.  Choisissez l’onglet **Nom de l’objet**, vérifiez que l’option **Construire à partir de ces informations Active Directory** est sélectionnée, choisissez **Nom commun** pour **Format du nom de l’objet :**, puis effacez **Nom d’utilisateur principal (UPN)** dans **Inclure cette information dans le nom de substitution du sujet**.  

7.  Sous l’onglet **Sécurité**, supprimez l’autorisation **Inscription** des groupes de sécurité **Administrateurs du domaine** et **Administrateurs de l’entreprise**.  

8.  Choisissez **Ajouter**, spécifiez le groupe de sécurité que vous avez créé lors de la première étape, puis choisissez **OK**.  

9. Choisissez l’autorisation **Inscription** pour ce groupe et ne désactivez pas l’autorisation **Lecture**.  

10. Choisissez **OK**, puis fermez la **console Modèles de certificats**.  

11. Dans la console Autorité de certification, cliquez avec le bouton droit sur **Modèles de certificats**, choisissez **Nouveau**, puis **Modèle de certificat à délivrer**.  

12. Dans la boîte de dialogue **Activer les modèles de certificat**, choisissez le nouveau modèle que vous venez de créer, **Certificat client Mac ConfigMgr**, puis choisissez **OK**.  

13. Si vous n’avez pas besoin de créer ni d’émettre d’autres certificats, fermez **Autorité de certification**.  

 Le modèle de certificat client Mac est maintenant prêt à être sélectionné dès que vous configurez les paramètres client pour l’inscription.
