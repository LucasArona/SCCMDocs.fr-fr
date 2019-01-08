---
title: Étendre l’inventaire matériel
titleSuffix: Configuration Manager
description: Découvrez différentes façons d’étendre l’inventaire matériel dans System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f1fa9f1bb2e036e0208a72e744f66da5c1887593
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53423301"
---
# <a name="how-to-extend-hardware-inventory-in-system-center-configuration-manager"></a>Comment étendre l’inventaire matériel dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

L’inventaire matériel lit les informations sur les PC Windows en utilisant WMI (Windows Management Instrumentation). WMI est l’implémentation Microsoft de WBEM (Web-Based Enterprise Management), une norme sectorielle pour l’accès aux informations de gestion dans une entreprise. Dans les versions précédentes de Configuration Manager, vous étendiez l’inventaire matériel en modifiant le fichier sms_def.mof sur le serveur de site. Ce fichier contenait une liste de classes WMI qui pouvaient être lues par l’inventaire matériel. La modification de ce fichier vous permettait d’activer et de désactiver les classes existantes, et également de créer des classes à inventorier.  

Le fichier Configuration.mof permet de définir les classes de données qui doivent faire l’objet d’un inventaire matériel sur le client. Il n’a pas été modifié depuis Configuration Manager 2012. Vous pouvez créer des classes de données pour inventorier les classes de données de référentiel WMI existantes ou personnalisées ou les clés de Registre présentes sur les systèmes clients.  

 Le fichier Configuration.mof définit également et inscrit les fournisseurs WMI d'accéder aux informations de périphérique durant l'inventaire matériel. L'enregistrement des fournisseurs définit le type de fournisseur à utiliser et les classes prises en charge par le fournisseur.  

 Quand les clients Configuration Manager demandent une stratégie, le fichier Configuration.mof est attaché au corps de la stratégie. Ce fichier est ensuite téléchargé et compilé par les clients. Lorsque vous ajoutez, modifiez ou supprimez des classes de données à partir du fichier Configuration.mof, les clients compilent automatiquement ces modifications sont apportées aux classes de données liées au stock. Aucune autre action n’est requise pour inventorier les classes de données nouvelles ou modifiées sur les clients Configuration Manager. Ce fichier se trouve dans **<emplacement_installation_CM\>\Inboxes\clifiles.src\hinv\\\** sur les serveurs de site principal.  

 Dans Configuration Manager, le fichier sms_def.mof n’a plus besoin d’être modifié comme c’était le cas dans Configuration Manager 2007. Au lieu de cela, vous pouvez activer et désactiver des classes WMI, et ajouter de nouvelles classes que l’inventaire matériel collectera, à l’aide des paramètres client. Configuration Manager permet d’étendre l’inventaire matériel à l’aide des méthodes ci-dessous.  

> [!NOTE]  
>  Si vous avez changé manuellement le fichier Configuration.mof pour ajouter des classes d’inventaire personnalisées, ces changements sont remplacés quand vous effectuez la mise à jour vers la version 1602. Pour continuer à utiliser des classes personnalisées après la mise à jour, vous devez les ajouter à la section « Added extensions » du fichier Configuration.mof après la mise à jour vers 1602.  
> En revanche, vous ne devez rien modifier au-dessus de cette section, car la modification de ces sections est réservée à Configuration Manager. Une sauvegarde de votre fichier Configuration.mof personnalisé se trouve dans :  
> **<répertoire_installation_CM\>\data\hinvarchive\\**.  

|Méthode|Informations complémentaires|  
|------------|----------------------|  
|Activer ou désactiver les classes d'inventaire existantes|Activez ou désactivez les classes d’inventaire par défaut ou créez des paramètres client personnalisés qui vous permettent de collecter différentes classes d’inventaire matériel depuis les regroupements de clients définis. Consultez la procédure [Pour activer ou désactiver les classes existantes d’inventaire](#BKMK_Enable) de cet article.|  
|Ajouter une nouvelle classe d'inventaire|Ajoutez une nouvelle classe d’inventaire à partir de l’espace de noms WMI d’un autre appareil. Consultez la procédure [Pour ajouter une nouvelle classe d’inventaire](#BKMK_Add) de cet article.|  
|Importer et exporter des classes d'inventaire matériel|Importez et exportez des fichiers MOF (Managed Object Format) qui contiennent des classes d’inventaire à partir de la console Configuration Manager. Consultez les procédures [Pour importer des classes d’inventaire matériel](#BKMK_Import) et [Pour exporter des classes d’inventaire matériel](#BKMK_Export) de cet article.|  
|Créer des fichiers NOIDMIF|Utilisez des fichiers NOIDMIF pour collecter des informations sur les appareils clients qui ne peuvent pas être inventoriés par Configuration Manager. Par exemple, vous pouvez souhaiter recueillir des informations numéros de périphérique actif qui existe uniquement en tant qu'étiquette sur le périphérique. Inventaire NOIDMIF est automatiquement associé à l'appareil client collectées à partir de. Consultez [Pour créer des fichiers NOIDMIF](#BKMK_NOIDMIF) dans cet article.|  
|Créer les fichiers IDMIF|Utilisez des fichiers IDMIF pour collecter des informations sur les ressources de votre organisation qui ne sont associées à aucun client Configuration Manager, par exemple, les projecteurs, les photocopieurs et les imprimantes réseau. Consultez [Pour créer des fichiers IDMIF](#BKMK_IDMIF) dans cet article.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Procédures pour étendre l’inventaire matériel  
Ces procédures vous aident à configurer les paramètres client par défaut pour l'inventaire matériel et elles s'appliquent à tous les clients de votre hiérarchie. Pour appliquer ces paramètres à certains clients uniquement, créez un paramètre d’appareil client personnalisé et affectez-le à un regroupement de clients spécifiques. Consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="BKMK_Enable"></a> Pour activer ou désactiver les classes existantes d'inventaire  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut**, choisissez **Inventaire matériel**.  

6.  Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d'inventaire matériel** , sélectionnez ou désélectionnez les classes et les propriétés de classe que doit collecter l'inventaire matériel. Vous pouvez développer une classe pour sélectionner ou désélectionner des propriétés individuelles dans la classe. Utilisez le champ **Rechercher des classes d'inventaire** pour rechercher des classes individuelles.  

    > [!IMPORTANT]  
    >  Quand vous ajoutez de nouvelles classes à l’inventaire matériel Configuration Manager, la taille du fichier d’inventaire collecté et envoyé au serveur de site augmente. Cela peut nuire aux performances de votre réseau et du site Configuration Manager. Activez uniquement les classes d'inventaire à collecter.  


###  <a name="BKMK_Add"></a> Pour ajouter une nouvelle classe d'inventaire  

Vous pouvez uniquement ajouter des classes d’inventaire à partir du serveur de niveau supérieur de la hiérarchie en modifiant les paramètres client par défaut. Cette option n'est pas disponible lorsque vous créez des paramètres de périphérique personnalisés.

1. Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

2. Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

3. Dans la boîte de dialogue **Paramètres client par défaut**, choisissez **Inventaire matériel**.  

4. Dans la liste **Paramètres de l’appareil**, choisissez **Définir des classes**.  

5. Dans la boîte de dialogue **Classes d’inventaire matériel**, choisissez **Ajouter**.  

6. Dans la boîte de dialogue **Ajouter une classe d'inventaire matériel** , cliquez sur **Ajouter**.  

7. Dans la boîte de dialogue **Connexion à Windows Management Instrumentation (WMI)** , définissez le nom de l'ordinateur depuis lequel vous allez extraire les classes WMI et l'espace de noms WMI à utiliser pour récupérer les classes. Si vous souhaitez récupérer toutes les classes sous l'espace de noms WMI spécifié, cliquez sur **Récursive**. Si l'ordinateur auquel vous vous connectez n'est pas l'ordinateur local, fournissez les informations d'identification d'un compte autorisé à accéder à WMI sur l'ordinateur distant.  

8. Choisissez **Connexion**.  

9. Dans la boîte de dialogue **Ajouter une classe d’inventaire matériel**, dans la liste des **classes d’inventaire**, sélectionnez les classes WMI à ajouter à l’inventaire matériel Configuration Manager.  

10. Si vous souhaitez modifier des informations sur la classe WMI sélectionnée, choisissez **Modifier** et, dans la boîte de dialogue **Qualificatifs de classe**, fournissez les informations suivantes :  

    - **Nom complet** : ce nom sera affiché dans l’Explorateur de ressources.  

    - **Propriétés** : définissez l’unité dans laquelle s’affiche chaque propriété de la classe WMI.  

      Vous pouvez également désigner des propriétés comme propriété de clé pour identifier de façon unique chaque instance de la classe. Si aucune clé n'est définie pour la classe et que plusieurs instances de la classe sont signalées par le client, seule la dernière instance trouvée est stockée dans la base de données.  

      Une fois la configuration des propriétés terminée, cliquez sur **OK** pour fermer la boîte de dialogue **Qualificatifs de classe** et les autres boîtes de dialogue ouvertes. 

###  <a name="BKMK_Import"></a> Pour importer des classes d'inventaire matériel  

Vous pouvez importer uniquement des classes d'inventaire lorsque vous modifiez les paramètres par défaut du client. Toutefois, vous pouvez utiliser des paramètres client personnalisés pour importer des informations qui n’incluent pas de changement de schéma, comme le changement de la propriété d’une classe existante en remplaçant la valeur **True** par **False**.  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut**, choisissez **Inventaire matériel**.  

6.  Dans la liste **Paramètres de l’appareil**, choisissez **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d’inventaire matériel**, choisissez **Importer**.  

8.  Dans la boîte de dialogue **Importer**, sélectionnez le fichier MOF (Managed Object Format) à importer, puis choisissez **OK**. Passez en revue les éléments qui seront importés, puis cliquez sur **Importer**.  

###  <a name="BKMK_Export"></a> Pour exporter des classes d'inventaire matériel  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres client par défaut**, choisissez **Inventaire matériel**.  

6.  Dans la liste **Paramètres de l’appareil**, choisissez **Définir des classes**.  

7.  Dans la boîte de dialogue **Classes d’inventaire matériel**, choisissez **Exporter**.  

    > [!NOTE]  
    >  Lorsque vous exportez des classes, toutes les classes sélectionnées sont exportées.  

8.  Dans la boîte de dialogue **Exporter**, spécifiez le fichier MOF (Managed Object Format) vers lequel vous voulez exporter les classes, puis choisissez **Enregistrer**.  

### <a name="bkmk_GreaterThan255"></a> Configurer l’inventaire matériel pour collecter les chaînes comportant plus de 255 caractères
À compter de Configuration Manager 1802, vous pouvez spécifier une longueur de chaînes supérieure à 255 caractères pour les propriétés de l’inventaire matériel. Cette modification s’applique seulement aux classes nouvellement ajoutées et aux propriétés de l’inventaire matériel qui ne sont pas des clés. <!-- 1357389 -->

1. Dans l’espace de travail **Administration**, cliquez sur **Paramètres client**, mettez en surbrillance un appareil client à modifier, cliquez avec le bouton droit, puis sélectionnez **Propriétés**.

2. Sélectionnez **Inventaire matériel**, puis **Définir des classes** et **Ajouter**.

3. Cliquez sur le bouton **Connecter**.

4. Renseignez **Nom de l’ordinateur** et **Espace de noms WMI**, et sélectionnez **Récursif** si nécessaire. Fournissez si nécessaire les informations d’identification pour la connexion. Cliquez sur **Connecter** pour afficher les classes de l’espace de noms.

5. Sélectionnez une nouvelle classe, puis cliquez sur **Modifier**.

6. Remplacez la **Longueur** de votre propriété autre que la clé et qui est une chaîne par une valeur supérieure à 255. Cliquez sur **OK**. 

7. Vérifiez que la propriété modifiée est sélectionnée pour **Ajouter une classe d’inventaire matériel** et cliquez sur **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Comment utiliser les fichiers MIF (Management Information Format) pour étendre l’inventaire matériel  
 Utilisez des fichiers MIF (Management Information Format) pour étendre les informations d’inventaire matériel recueillies auprès des clients par Configuration Manager. Au cours de l'inventaire matériel, les informations stockées dans les fichiers MIF sont ajoutées au rapport d'inventaire du client et stockées dans la base de données de site. Vous pourrez utiliser les données depuis cet emplacement de la même manière que vous utilisez les données d'inventaire du client par défaut. Il existe deux types de fichiers MIF : NOIDMIF et IDMIF.

> [!IMPORTANT]  
>  Avant d’ajouter les informations de fichiers MIF à la base de données Configuration Manager, vous devez créer ou importer des informations de classe pour eux. Pour plus d’informations, consultez les sections [Pour ajouter une nouvelle classe d’inventaire](#BKMK_Add) et [Pour importer des classes d’inventaire matériel](#BKMK_Import) de cet article.  

###  <a name="BKMK_NOIDMIF"></a> Pour créer des fichiers NOIDMIF  
 Les fichiers NOIDMIF permettent d’ajouter à un inventaire matériel client des informations qui ne peuvent normalement pas être collectées par Configuration Manager et qui sont associées à un appareil client particulier. Par exemple, de nombreuses sociétés affectent à chaque ordinateur de l’organisation un numéro de ressource, puis classent ces numéros manuellement. Quand vous créez un fichier NOIDMIF, ces informations peuvent être ajoutées à la base de données Configuration Manager et être utilisées pour les requêtes et la génération de rapports. Pour plus d’informations sur la création de fichiers NOIDMIF, consultez la documentation du Kit de développement logiciel (SDK) Configuration Manager.  

> [!IMPORTANT]  
>  Quand vous créez un fichier NOIDMIF, il doit être enregistré dans un format codé ANSI. Les fichiers NOIDMIF enregistrés au format encodé UTF-8 ne peuvent pas être lus par Configuration Manager.  

 Après avoir créé un fichier NOIDMIF, stockez-le dans le dossier *%Windir%***\CCM\Inventory\Noidmifs** sur chaque client. Configuration Manager collecte les informations des fichiers NODMIF de ce dossier lors du prochain cycle d’inventaire matériel planifié.  

###  <a name="BKMK_IDMIF"></a> Pour créer des fichiers IDMIF  
 Les fichiers IDMIF permettent d’ajouter à la base de données Configuration Manager des informations sur les ressources qui ne pourraient normalement pas être inventoriées par Configuration Manager et qui ne sont associées à aucun appareil client particulier. Par exemple, vous pouvez utiliser des fichiers IDMIF pour collecter des informations sur les projecteurs, lecteurs DVD, photocopieurs ou autres équipements qui ne disposent pas d’un client Configuration Manager. Pour plus d’informations sur la création de fichiers IDMIF, consultez la documentation du Kit de développement logiciel (SDK) Configuration Manager.  

 Après avoir créé un fichier IDMIF, stockez-le dans le dossier *%Windir%***\CCM\Inventory\Idmifs** sur les ordinateurs clients. Configuration Manager collecte les informations de ce fichier lors du prochain cycle d’inventaire matériel planifié. Vous devez déclarer de nouvelles classes pour les informations contenues dans le fichier en les ajoutant ou en les important.  

> [!NOTE]
> Les fichiers MIF peuvent contenir de grandes quantités de données et le regroupement de ces données pourrait affecter négativement les performances de votre site. Activez la collecte de fichiers MIF uniquement quand cela est nécessaire et configurez l’option **Taille maximale du fichier MIF personnalisé (Ko)** dans les paramètres d’inventaire matériel. Pour plus d’informations, consultez [Présentation de l’inventaire matériel dans System Center Configuration Manager](introduction-to-hardware-inventory.md).
