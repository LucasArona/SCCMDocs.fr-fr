---
title: Publication et schéma Active Directory
titleSuffix: Configuration Manager
description: L’extension du schéma Active Directory pour System Center Configuration Manager permet de simplifier le processus de déploiement et de configuration des clients.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6f0590a626cf75ed78e42235768a0d97a9fc3026
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="prepare-active-directory-for-site-publishing"></a>Préparer Active Directory pour la publication de site

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous étendez le schéma Active Directory pour System Center Configuration Manager, les nouvelles structures que vous introduisez dans Active Directory sont utilisées par les sites System Center Configuration Manager pour publier des informations importantes, à un emplacement sécurisé facilement accessible par les clients.  

Si vous gérez localement des clients, nous vous conseillons d’utiliser Configuration Manager avec un schéma Active Directory étendu. Un schéma étendu peut simplifier le processus de déploiement et de configuration des clients. Un schéma étendu permet également aux clients de localiser efficacement des ressources comme les serveurs de contenu et d’autres services fournis par les différents rôles de système de site Configuration Manager.  

-   Si vous ne savez pas si vous avez intérêt à utiliser un schéma étendu pour le déploiement dans Configuration Manager, consultez [Extensions de schéma pour System Center Configuration Manager](../../../core/plan-design/network/schema-extensions.md) pour vous aider à prendre cette décision.  

-   Si vous n’utilisez pas de schéma étendu, vous pouvez configurer d’autres méthodes, telles que DNS et WINS, pour rechercher des services et des serveurs de système de site. Ces méthodes d’emplacement de service nécessitent des configurations supplémentaires et ne sont pas la méthode préférée pour l’emplacement du service par les clients. Pour en savoir plus, consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Si votre schéma Active Directory a déjà été étendu pour Configuration Manager 2007 ou System Center 2012 Configuration Manager, vous n’avez pas d’autres tâches à effectuer. Les extensions de schéma demeurent inchangées et sont déjà en place.  

L’extension du schéma est une opération qui s’effectue une seule fois pour n’importe quelle forêt. Pour étendre le schéma Active Directory étendu, puis l’utiliser, procédez comme suit :  

## <a name="step-1-extend-the-schema"></a>Étape 1. Étendre le schéma  
Pour étendre le schéma pour Configuration Manager, vous devez :  

-   Utiliser un compte qui est membre du groupe de sécurité Administrateurs du schéma.  

-   Être connecté à un contrôleur de domaine principal du schéma.  

-   Exécuter l’outil **Extadsch.exe** , ou utiliser l’utilitaire de ligne de commande LDIFDE avec le fichier **ConfigMgr_ad_schema.ldf** . L’outil et le fichier se trouvent dans le dossier **SMSSETUP\BIN\X64** sur le média d’installation de Configuration Manager.  

#### <a name="option-a-use-extadschexe"></a>Option A : utiliser Extadsch.exe  

1.  Exécutez le fichier **extadsch.exe** pour ajouter les nouvelles classes et les nouveaux attributs au schéma Active Directory.  

    > [!TIP]  
    >  Exécutez cet outil à partir de la ligne de commande pour afficher les commentaires pendant son exécution.  

2.  Pour vérifier que l’extension du schéma a réussi, examinez extadsch.log à la racine du lecteur du système.  

#### <a name="option-b-use-the-ldif-file"></a>Option B : utiliser le fichier LDIF  

1.  Modifiez le fichier **ConfigMgr_ad_schema.ldf** pour définir le domaine racine Active Directory à étendre :  

    -   Remplacez toutes les instances du texte **DC=x** dans le fichier par le nom complet du domaine à étendre.  

    -   Par exemple, si le nom complet du domaine à étendre est widgets.microsoft.com, remplacez toutes les instances de DC=x dans le fichier par **DC=widgets, DC=microsoft, DC=com**.  

2.  À l’aide de l’utilitaire de ligne de commande LDIFDE, importez le contenu du fichier **ConfigMgr_ad_schema.ldf** dans Active Directory Domain Services :  

    -   Par exemple, la ligne de commande suivante importe les extensions de schéma dans Active Directory Domain Services, active la journalisation détaillée et crée un fichier journal pendant l’importation : **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;emplacement_de_stockage_du_fichier_journal\>**.  

3.  Pour vérifier si l’extension du schéma a réussi, examinez le fichier journal créé par la ligne de commande exécutée à l’étape précédente.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Étape 2.  Créer le conteneur System Management et accorder des autorisations de sites au nouveau conteneur  
 Après avoir étendu le schéma, vous devez créer un conteneur nommé **System Management** dans Active Directory Domain Services (AD DS) :  

-   Vous créez ce conteneur une fois pour toutes dans chaque domaine comportant un site principal ou secondaire qui publiera des données dans Active Directory.  

-   Pour chaque conteneur, vous accordez des autorisations au compte d’ordinateur de chaque serveur de site principal et secondaire appelé à publier les données sur ce domaine. Chaque compte doit avoir un **contrôle total** sur le conteneur avec l’autorisation avancée **Appliquer à** égale à **cet objet et tous ceux descendants**.  

#### <a name="to-add-the-container"></a>Pour ajouter le conteneur  

1.  Utilisez un compte possédant l’autorisation **Créer tous les objets enfants** sur le conteneur **Système** dans les services de domaine Active Directory.  

2.  Exécutez **ADSI Edit** (adsiedit.msc) et connectez-vous au domaine du serveur de site.  

3.  Créez le conteneur :  

    -   Développez **Domaine** &lt;nom_de_domaine_complet_ordinateur\>, développez &lt;nom_unique\>, cliquez avec le bouton droit sur **CN=System**, choisissez **Nouveau**, puis **Objet**.  

    -   Dans la boîte de dialogue **Créer un objet**, choisissez **Conteneur**, puis **Suivant**.  

    -   Dans la zone **Valeur**, entrez **System Management**, puis choisissez **Suivant**.  

4.  Accordez les autorisations appropriées :  

    > [!NOTE]  
    >  Si vous préférez, vous pouvez utiliser d’autres outils, tels que l’outil d’administration Utilisateurs et ordinateurs Active Directory (DSA.msc) pour ajouter des autorisations au conteneur.  

    -   Cliquez avec le bouton droit sur **CN=System Management**, puis choisissez **Propriétés**.  

    -   Choisissez l’onglet **Sécurité**, **Ajouter**, puis ajoutez le compte d’ordinateur de serveur de site avec l’autorisation **Contrôle intégral**.  

    -   Choisissez **Avancé**, choisissez le compte d’ordinateur du serveur de site, puis choisissez **Modifier**.  

    -   Dans la liste **Appliquer à**, choisissez **cet objet et tous ceux descendants**.  

5.  Choisissez **OK** pour fermer la console et enregistrer la configuration.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Étape 3. Configurer les sites pour la publication de données sur Active Directory Domain Services  
 Après avoir configuré le conteneur, accordé les autorisations appropriées et installé un site principal Configuration Manager, vous pouvez configurer ce site pour la publication de données dans Active Directory.  

 Pour plus d’informations sur la publication, consultez [Publier des données de site pour System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
