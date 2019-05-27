---
title: Utiliser Asset Intelligence
titleSuffix: Configuration Manager
description: Effectuez les tâches courantes Asset Intelligence dans System Center Configuration Manager.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e8159bd9-5c2b-4d25-82f9-78fcfd732ba9
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b200594c4769fb4528c3adc7b846b2345ffeda39
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499871"
---
# <a name="how-to-use-asset-intelligence-in-system-center-configuration-manager"></a>Guide pratique pour utiliser Asset Intelligence dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations destinées à vous aider à gérer les tâches courantes Asset Intelligence dans votre hiérarchie System Center Configuration Manager :  

##  <a name="BKMK_ViewInformation"></a> Afficher les informations Asset Intelligence  
 Vous pouvez afficher les informations Asset Intelligence sur la page d'accueil **Asset Intelligence** et dans les rapports Asset Intelligence.  

###  <a name="BKMK_AssetIntelligenceHomePage"></a> Page d’accueil d’Asset Intelligence  
 La page d'accueil d' **Asset Intelligence** contient un tableau de bord récapitulant les informations du catalogue Asset Intelligence. Sur la page d'accueil, vous pouvez visualiser des informations sur la synchronisation du catalogue et l'état des logiciels inventoriés. La page d'accueil d' **Asset Intelligence** comporte les sections suivantes :  

- **Synchronisation de catalogue** : indique si Asset Intelligence est activé, l’état du point de synchronisation Asset Intelligence, la planification de la synchronisation, si la déclaration de licence du client est importée, la date/heure de la dernière mise à jour de l’état et de la prochaine mise à jour planifiée, et le nombre de modifications effectuées après l’installation du système de site du point de synchronisation Asset Intelligence.  

  > [!NOTE]  
  >  La section de synchronisation du catalogue Asset Intelligence de la page d'accueil **Asset Intelligence** s'affiche uniquement si un rôle de système de site du point de synchronisation Asset Intelligence a été installé.  

- **État des logiciels inventoriés** : indique le nombre et le pourcentage de logiciels, de catégories de logiciels et de familles de logiciels identifiés par Microsoft, identifiés par un utilisateur administratif, en attente d’identification en ligne, ou non identifiés et non en attente. Les informations affichées dans un tableau indiquent le nombre pour chacun des éléments, tandis que les informations affichées dans le graphique indiquent le pourcentage de chacun des éléments.  

  Utilisez la procédure suivante pour afficher les informations Asset Intelligence sur la page d'accueil **Asset Intelligence** .  

##### <a name="to-view-asset-intelligence-information-on-the-asset-intelligence-home-page"></a>Pour afficher les informations Asset Intelligence sur la page d'accueil Asset Intelligence  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**. Les rapports Asset Intelligence s'affichent.  

###  <a name="BKMK_AssetIntelligenceReports"></a> Rapports Asset Intelligence  
 Il existe plus de 60 rapports Asset Intelligence qui affichent les informations collectées par Asset Intelligence. La plupart de ces rapports renvoient vers des rapports plus spécifiques qui permettent de rechercher des informations générales et d'accéder à des informations plus détaillées. Les rapports Asset Intelligence se trouvent dans la console Configuration Manager, dans l’espace de travail **Surveillance**, sous le nœud **Rapports**. Les rapports fournissent des informations sur les matériels, la gestion des licences et les logiciels. Pour plus d’informations sur les rapports Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/reporting.md).  

> [!NOTE]  
>  L'exactitude des nombres de titres de logiciels et des informations de licence affichés dans les rapports Asset Intelligence peut varier par rapport au nombre réel de titres de logiciels installés ou de licences utilisées dans l'environnement. Ceci est dû aux dépendances complexes et aux limitations propres à l'inventaire des informations de licences logicielles pour les titres de logiciels installés dans les environnements d'entreprise. N'utilisez pas uniquement Asset Intelligence pour déterminer la conformité des licences logicielles achetées.  

 Utilisez la procédure suivante pour afficher les informations Asset Intelligence en utilisant les rapports Asset Intelligence.  

##### <a name="to-view-collected-asset-intelligence-information-by-using-asset-intelligence-reports"></a>Pour afficher les informations Asset Intelligence collectées en utilisant les rapports Asset Intelligence  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , développez **Rapports**et **Rapports**, puis cliquez sur **Asset Intelligence**. Les rapports Asset Intelligence s'affichent.  

    > [!WARNING]  
    >  Si aucun dossier de rapport n'existe sous le noeud **Rapports** , vérifiez que vous avez configuré la création de rapports. Pour plus d’informations, consultez [Configuration de la génération de rapports dans System Center Configuration Manager](../../../../core/servers/manage/configuring-reporting.md).  

3.  Sélectionnez le rapport Asset Intelligence à exécuter, puis dans l'onglet **Accueil** , dans le groupe **Groupe de rapports** , cliquez sur **Exécuter**.  

##  <a name="BKMK_SynchronizeTheCatalog"></a> Synchroniser le catalogue Asset Intelligence  
 Vous pouvez synchroniser le catalogue local Asset Intelligence avec System Center Online pour récupérer la dernière catégorisation de titres de logiciels. Quand vous demandez manuellement la synchronisation du catalogue avec System Center Online, l’achèvement du processus de synchronisation avec System Center Online peut prendre 15 minutes ou plus. Configuration Manager met à jour le paramètre **Dernière mise à jour réussie** dans la page d’accueil d’**Asset Intelligence** avec l’heure à laquelle la synchronisation se termine.  

> [!NOTE]  
>  Pour pouvoir utiliser les procédures, vous devez installer préalablement un rôle de système de site de point de synchronisation Asset Intelligence. Pour plus d’informations sur l’installation d’un point de synchronisation Asset Intelligence, consultez [Configuration d’Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/configuring-asset-intelligence.md).  

 Utilisez la procédure suivante pour créer une planification de synchronisation pour le catalogue Asset Intelligence.  

#### <a name="to-create-a-synchronization-schedule-for-the-asset-intelligence-catalog"></a>Pour créer une planification de synchronisation pour le catalogue Asset Intelligence  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**.  

3. Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Synchroniser**, puis sur **Planifier la synchronisation**.  

4. Dans la boîte de dialogue **Planification de point de synchronisation Asset Intelligence** , sélectionnez **Activer la synchronisation dans un calendrier**, puis définissez une planification simple ou personnalisée.  

5. Cliquez sur **OK** pour enregistrer les modifications.  

   > [!NOTE]  
   >  Pour plus d’informations sur la planification de la synchronisation, y compris la prochaine synchronisation planifiée, consultez le nœud **Asset Intelligence** dans l’espace de travail **Ressources et Conformité** sur le site de niveau supérieur de la hiérarchie.  

   Utilisez la procédure suivante pour synchroniser manuellement le catalogue Asset Intelligence.  

> [!WARNING]  
>  System Center Online n'accepte qu'une seule demande de synchronisation manuelle sur une période de 12 heures.  

###  <a name="BKMK_ManuallySynchronizeCatalog"></a> Pour synchroniser manuellement le catalogue Asset Intelligence  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**.  

3.  Sur l'onglet **Accueil** , dans le groupe **Créer** , cliquez successivement sur **Synchroniser**, **Synchroniser le catalogue Asset Intelligence**et **OK**.  

##  <a name="BKMK_CustomizeCatalog"></a> Personnaliser le catalogue Asset Intelligence  
 Les informations de catégorisation du catalogue Asset Intelligence envoyées par System Center Online sont stockées en lecture seule dans la base de données de site et elles ne peuvent donc pas être modifiées, ni supprimées. Toutefois, vous pouvez créer, modifier et supprimer des catégories de logiciels, des familles de logiciels, des légendes logicielles et des informations de configuration matérielle personnalisées dans le catalogue. Ensuite, vous pouvez utiliser les informations de catégorisation personnalisées à la place des informations fournies par System Center Online pour les informations de titres de logiciels définies par l'utilisateur ou existantes. Lorsque vous modifiez ou ajoutez des informations de catégorisation, les informations du catalogue sont considérées avoir été définies par l'utilisateur. Les informations de catégorisation définies par l'utilisateur ne sont pas stockées dans les mêmes tables de base de données que les informations validées du catalogue.  

###  <a name="BKMK_SoftwareCategories"></a> Catégories de logiciels  
 Les catégories de logiciels Asset Intelligence sont utilisées pour catégoriser de façon large les titres de logiciels inventoriés et pour les regroupements généraux de familles de logiciels plus spécifiques. Par exemple, « Société d'énergie » peut correspondre à une catégorie de logiciels, et « Pétrole », « Gaz » ou « Hydroélectrique » peuvent correspondre à des familles de logiciels dans cette catégorie. La plupart des catégories de logiciels sont prédéfinies dans le catalogue Asset Intelligence et des catégories définies par l'utilisateur peuvent être créées pour définir plus précisément les logiciels inventoriés. L'état de validation de toutes les catégories de logiciels prédéfinies est toujours **Validé**, alors que les informations de catégories de logiciels personnalisées ajoutées au catalogue Asset Intelligence ont l'état **Défini par l'utilisateur**  

 Utilisez la procédure suivante pour créer une catégorie de logiciels définie par l'utilisateur.  

##### <a name="to-create-a-user-defined-software-category"></a>Pour créer une catégorie de logiciels définie par l'utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Catalogue**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une catégorie logicielle**.  

4.  Sur la page **Général** , entrez le nom de la nouvelle catégorie de logiciels et, éventuellement, une description.  

    > [!NOTE]  
    >  L'état de validation de toutes les nouvelles catégories personnalisées de logiciels est toujours **Défini par l'utilisateur**.  

     Cliquez sur **Suivant**.  

5.  Sur la page **Résumé** , vérifiez les paramètres, puis cliquez sur **Suivant**.  

6.  Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant.  

###  <a name="BKMK_SoftwareFamilies"></a> Familles de logiciels  
 Les familles de logiciels Asset Intelligence permettent de définir plus précisément les titres de logiciels dans les catégories de logiciels. Par exemple, « Société d'énergie » peut correspondre à une catégorie de logiciels, et « Pétrole », « Gaz » ou « Hydroélectrique » peuvent correspondre à des familles de logiciels dans cette catégorie. La plupart des familles de logiciels sont prédéfinies dans le catalogue Asset Intelligence et des familles additionnelles définies par l'utilisateur peuvent être créées pour définir les logiciels inventoriés. L'état de validation de toutes les familles de logiciels prédéfinies est toujours **Validé**, alors que les informations de familles de logiciels personnalisées ajoutées au catalogue Asset Intelligence ont l'état **Défini par l'utilisateur**  

 Utilisez la procédure suivante pour créer une famille de logiciels définie par l'utilisateur.  

##### <a name="to-create-a-user-defined-software-family"></a>Pour créer une famille de logiciels définie par l'utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Catalogue**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une famille logicielle**.  

4.  Sur la page **Général** , entrez le nom de la nouvelle famille de logiciels et, éventuellement, une description.  

    > [!NOTE]  
    >  L'état de validation de toutes les nouvelles familles personnalisées de logiciels est toujours **Défini par l'utilisateur**.  

5.  Sur la page **Résumé** , vérifiez les paramètres, puis cliquez sur **Suivant**.  

6.  Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant.  

###  <a name="BKMK_SoftwareLabels"></a> Légendes logicielles  
 Les légendes logicielles personnalisées Asset Intelligence permettent de créer des filtres que vous pouvez utiliser pour regrouper les titres de logiciels et les afficher en utilisant des rapports Asset Intelligence. Par exemple, vous pouvez créer une légende logicielle appelée « logiciel à contribution volontaire », l'associer à un certain nombre d'applications, puis exécuter un rapport pour afficher tous les titres ayant la légende logicelle « logiciel à contribution volontaire ». L'état de validation est **Défini par l'utilisateur** pour toutes les légendes logicielles personnalisées que vous ajoutez au catalogue Asset Intelligence.  

 Utilisez la procédure suivante pour créer une légende personnalisée définie par l'utilisateur.  

##### <a name="to-create-a-user-defined-software-label"></a>Pour créer une légende logicielle définie par l'utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Catalogue**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une légende logicielle**.  

4.  Sur la page **Général** , entrez le nom de la nouvelle famille de logiciels et, éventuellement, une description.  

    > [!NOTE]  
    >  L'état de validation de toutes les nouvelles légendes logicielles personnalisées est toujours **Défini par l'utilisateur**.  

5.  Sur la page **Résumé** , vérifiez les paramètres, puis cliquez sur **Suivant**.  

6.  Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant.  

###  <a name="BKMK_HardwareRequirements"></a> Configuration matérielle requise  
 Les informations de configuration matérielle requise permettent de vérifier que les ordinateurs répondent à la configuration matérielle requise pour les titres de logiciels avant d'y déployer les logiciels. La plupart des configurations matérielles requises sont prédéfinies dans le catalogue Asset Intelligence et vous pouvez créer des informations de configuration matérielle définies par l'utilisateur pour répondre à des besoins spécifiques. L'état de validation de toutes les configurations matérielles requises prédéfinies est toujours **Validé**, tandis que celui des informations de configuration matérielle requise définies par l'utilisateur ajoutées au catalogue Asset Intelligence est **Défini par l'utilisateur**.  

> [!IMPORTANT]  
>  Les informations de configuration matérielle requise figurant dans la console Configuration Manager sont tirées du catalogue Asset Intelligence sur l’ordinateur local et ne reposent pas sur les informations de titres de logiciels inventoriés sur les clients System Center 2012 Configuration Manager. Les informations de configuration matérielle requise ne sont pas mises à jour au cours de la synchronisation avec System Center Online. Vous pouvez créer une configuration matérielle requise définie par l'utilisateur pour le logiciel inventorié n'ayant pas de configuration matérielle.  

 Utilisez la procédure suivante pour créer une configuration matérielle requise définie par l'utilisateur.  

##### <a name="to-create-a-user-defined-hardware-requirements"></a>Pour créer une configuration matérielle requise définie par l'utilisateur  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Configuration matérielle requise**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer la configuration matérielle requise**.  

4. Sur la page **Général** , spécifiez les informations suivantes :  

   1. **Nom du logiciel** : spécifie le titre du logiciel auquel la configuration matérielle requise est associée. Le titre du logiciel ne peut pas exister déjà dans le catalogue Asset Intelligence.  

   2. **État de validation** : indique l’état de validation, tel que **Défini par l’utilisateur**, de la configuration matérielle requise. Vous ne pouvez pas modifier ce paramètre.  

   3. **Vitesse min. du processeur (MHz)** : spécifie la vitesse minimale du processeur (en mégahertz (MHz)) nécessaire au logiciel.  

   4. **Mémoire RAM minimum (Ko)** : spécifie la quantité de mémoire RAM minimale en kilo-octets (Ko) nécessaire au logiciel.  

   5. **Espace disque minimum (Ko)** : spécifie l’espace disque libre minimal en Ko nécessaire au logiciel.  

   6. **Taille minimale du disque (Ko)** : spécifie la taille minimale en Ko du disque dur nécessaire au logiciel.  

      Cliquez sur **Suivant**.  

5. Sur la page **Résumé** , vérifiez les paramètres, puis cliquez sur **Suivant**.  

6. Sur la page **Dernière étape** , cliquez sur **Fermer** pour quitter l'Assistant.  

###  <a name="BKMK_ModifyCategorization"></a> Modifier les informations de catégorisation des logiciels inventoriés  
 Le logiciel prédéfini dans le catalogue Asset Intelligence est configuré avec des informations de catégorisation spécifiques, telles que le nom du produit, le fournisseur, la catégorie du logiciel et la famille du logiciel. Lorsque les informations de catégorisation prédéfinies ne répondent pas à vos besoins, vous pouvez modifier les informations dans les propriétés du titre du logiciel. Lorsque vous modifiez les informations de catégorisation des logiciels prédéfinis, l'état de validation **Validé** des modifications de logiciels devient **Défini par l'utilisateur**.  

> [!IMPORTANT]  
>  Les informations de catégorisation peuvent être uniquement modifiées sur le site de niveau supérieur.  

 Utilisez la procédure suivante pour modifier les informations de catégorisation des logiciels inventoriés.  

##### <a name="to-modify-the-categorizations-for-software-titles"></a>Pour modifier les catégorisations des titres de logiciels  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Logiciels inventoriés**.  

3. Sélectionnez le ou les titres de logiciels dont vous voulez modifier les catégorisations.  

4. Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5. Sur l'onglet **Général** , vous pouvez modifier les informations de catégorisation suivantes :  

   -   **Nom du produit** : spécifie le titre du logiciel inventorié.  

   -   **Fournisseur** : spécifie le nom du fournisseur qui a développé le logiciel inventorié.  

   -   **Catégorie** : spécifie la catégorie affectée au logiciel inventorié.  

   -   **Famille** : spécifie la famille affectée au logiciel inventorié.  

6. Cliquez sur **OK** pour enregistrer les modifications.  

   Utilisez la procédure suivante pour restaurer les informations de catégorisation d'origine d'un logiciel.  

### <a name="revert-categorization-information-to-original-settings-for-software"></a>Restaurer les paramètres d’origine des informations de catégorisation des logiciels  
 Configuration Manager stocke les informations de catégorisation obtenues de System Center Online dans la base de données. Les informations ne peuvent pas être supprimées. Une fois les informations modifiées, vous pouvez restaurer les informations de catégorisation System Center Online. Vous pouvez également restaurer les paramètres d'origine des logiciels inventoriés qui ne figurent pas dans le catalogue Asset Intelligence.  

 Utilisez la procédure suivante pour restaurer les paramètres d'origine des informations de catégorisation.  

##### <a name="to-revert-categorization-information-to-original-settings"></a>Pour restaurer les paramètres d'origine des informations de catégorisation  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Logiciels inventoriés**.  

3.  Sélectionnez le ou les titres de logiciels dont vous voulez restaurer les paramètres d'origine. Seuls les logiciels ayant l'état **Défini par l'utilisateur** peuvent faire l'objet d'une restauration.  

    > [!TIP]  
    >  Cliquez sur la colonne **État** pour trier selon l'état de validation. Le tri vous permet de voir tous les logiciels en fonction de leur état de validation et de sélectionner rapidement plusieurs éléments pour rétablir les paramètres d'origine.  

4.  Dans l'onglet **Accueil** , dans le groupe **Produit** , cliquez sur **Restaurer**.  

5.  Cliquez sur **Oui** pour restaurer les informations de catégorisation d'origine du logiciel.  

6.  Lorsque vous restaurez les informations de catégorisation d'un logiciel qui se trouve dans le catalogue Asset Intelligence, l'état de validation passe de **Défini par l'utilisateur** à **Validé**. Lorsque vous restaurez un logiciel qui n'est pas dans le catalogue, l'état de validation passe de **Défini par l'utilisateur** à **Sans catégorie**.  

##  <a name="BKMK_RequestCatalogUpdate"></a> Demander une mise à jour du catalogue pour les logiciels sans catégorie  
 Les informations sur les noms de logiciels sans catégorie peuvent être soumises à System Center Online afin d'être examinées et catégorisées. Une fois qu'un logiciel sans catégorie est soumis et s'il existe au moins 4 demandes de catégorisation de la part de clients pour le même logiciel, les fonctions de recherche identifient, classent, puis mettent les informations de catégorisation des logiciels à la disposition de tous les clients qui utilisent le service System Center Online. Microsoft donne la priorité la plus élevée aux logiciels qui possèdent le plus de requêtes de catégorisation. Les logiciels personnalisés et les applications métier sont peu susceptibles de recevoir une catégorie, et nous vous conseillons de ne pas envoyer ces logiciels à Microsoft pour catégorisation.  

 Lorsque des informations sur les noms de logiciels sont soumises à System Center Online pour catégorisation, les conditions suivantes s'appliquent :  

-   Seules les informations de base sur les noms de logiciels sont transmises à System Center Online, et elles peuvent être vérifiées avant leur soumission.  

-   Aucune information de licence de logiciel n'est transmise.  

-   Les noms de logiciels téléchargés sont ouvertement publiés dans le catalogue de System Center Online et peuvent être téléchargés par d'autres clients.  

-   La source du nom du logiciel n'est pas stockée dans le catalogue de System Center Online. Toutefois, il est recommandé de ne pas soumettre à System Center Online des noms d'applications contenant des informations propriétaires ou confidentielles.  

> [!NOTE]  
>  Pour en savoir plus sur les informations de confidentialité Asset Intelligence, consultez [Sécurité et confidentialité pour Asset Intelligence dans System Center Configuration Manager](../../../../core/clients/manage/asset-intelligence/security-and-privacy-for-asset-intelligence.md).  

 Procédez comme suit pour demander à System Center Online la catégorisation d'un nom de logiciel du catalogue Asset Intelligence.  

#### <a name="to-request-a-catalog-update-for-uncategorized-software-titles"></a>Pour demander une mise à jour du catalogue pour les logiciels sans catégorie  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Logiciels inventoriés**.  

3.  Sélectionnez un ou plusieurs noms de produits à soumettre à System Center Online pour catégorisation. Seuls les noms de logiciels inventoriés sans catégorie peuvent être soumis. Si un logiciel inventorié a été catégorisé par un administrateur, entraînant un état défini par l'utilisateur, vous devez cliquer dessus avec le bouton droit, puis cliquer sur **Restaurer** pour rétablir le logiciel dans l'état **Sans catégorie** avant qu'il puisse être soumis à System Center Online pour catégorisation.  

    > [!NOTE]  
    >  Configuration Manager peut traiter jusqu’à 100 titres de logiciels à la fois pour catégorisation. Si vous sélectionnez plus de 100 logiciels, seuls les 100 premiers logiciels seront traités. Vous devez sélectionner les logiciels restants pour catégorisation par lots de moins de 100.  

    > [!TIP]  
    >  Cliquez sur la colonne **État** pour trier selon l'état de validation. Cela vous permet de voir tous les noms de produit sans catégorie et de sélectionner rapidement plusieurs éléments à soumettre pour catégorisation.  

4.  Dans l'onglet **Accueil** , dans le groupe **Produit** , cliquez sur **Demander une mise à jour du catalogue**.  

5.  Consultez le message de confidentialité de soumission de catégorisation de System Center Online. Cliquez sur **Détails** pour afficher les informations qui seront envoyées à System Center Online.  

6.  Sélectionnez **J'ai bien lu et compris ce message**, puis cliquez sur **OK** pour autoriser les logiciels sélectionnés à être soumis à la catégorisation.  

7.  Vérifiez que l'état des noms de produits logiciels inventoriés soumis à System Center Online pour catégorisation est passé de **Sans catégorie** à **En attente**.  

    > [!NOTE]  
    >  L'état de validation du logiciel soumis à System Center Online pour catégorisation est **En attente** sur un site d'administration centrale mais sur les sites principaux enfant, l'état de validation affiché pour ces éléments continue d'être **Sans catégorie** .  

##  <a name="BKMK_ResolveSoftwareDetails"></a> Résoudre les conflits de détails de logiciel  
 Suite à la réception par System Center Online de détails de catégorisation de logiciels nouvellement mis à jour et qui entrent en conflit avec des informations détaillées de logiciels existants, vous pouvez choisir la manière dont le conflit sera résolu. L'état de validation d'un logiciel en conflit est **Peut être mis à jour**. Après la résolution d'un conflit de détails de logiciel, les informations de catégorisation de logiciels sont conservées dans le catalogue Asset Intelligence en fonction des paramètres que vous avez définis. Un conflit de détails de logiciel ne peut pas se produire plusieurs fois pour la même valeur de catégorisation de logiciels à moins que la valeur System Center Online soit modifiée après la résolution du conflit.  

 Procédez comme suit pour résoudre un conflit de détails de logiciel.  

#### <a name="to-resolve-a-software-details-conflict"></a>Pour résoudre un conflit de détails de logiciel  

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2. Dans l'espace de travail **Biens et conformité** , cliquez sur **Asset Intelligence**, puis sur **Logiciels inventoriés**.  

3. Passez en revue la colonne **État** pour les logiciels dont l'état est **Peut être mis à jour** .  

4. Sélectionnez le logiciel pour lequel vous devez résoudre un conflit, puis sur l'onglet **Accueil** , dans le groupe **Produit** , puis cliquez sur **Résoudre le conflit**.  

5. Passez en revue les informations suivantes :  

   -   **Valeur locale** : spécifie les informations de catégorisation de logiciels dans le catalogue Asset Intelligence qui sont en conflit avec les détails de catégorisation les plus récents de System Center Online.  

   -   **Valeur téléchargée** : spécifie les nouvelles informations de catégorisation de logiciels System Center Online pour les informations de catégorisation de logiciels en conflit dans le catalogue Asset Intelligence.  

6. Sélectionnez l'un des paramètres suivants pour résoudre le conflit de détails du logiciel :  

   - **Ne changez pas la valeur des informations de catalogue modifiées localement** : résout le conflit des détails des logiciels en retenant les informations de catégorisation des logiciels du catalogue Asset Intelligence. Lorsque vous sélectionnez ce paramètre, l'état du logiciel passe de **Peut être mis à jour** à **Défini par l'utilisateur**.  

   - **Remplacez la valeur des informations de catalogue modifiées localement par la valeur System Center Online téléchargée** : résout le conflit des détails des logiciels en remplaçant les informations de catégorisation des logiciels existantes du catalogue Asset Intelligence par les nouvelles informations obtenues depuis System Center Online. Lorsque vous sélectionnez ce paramètre, l'état du logiciel passe de **Peut être mis à jour** à **Validé**.  

     Cliquez sur **OK** pour enregistrer la résolution du conflit.  
