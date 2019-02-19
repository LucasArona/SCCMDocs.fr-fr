---
title: 'Créer des éléments de configuration pour les appareils Mac gérés par le client '
titleSuffix: Configuration Manager
description: L’élément de configuration System Center Configuration Manager Mac OS X permet de gérer les paramètres des appareils Mac OS X.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf610c3310265f8b7dd6b467640617928a51258f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56124051"
---
# <a name="how-to-create-configuration-items-for-mac-os-x-devices-managed-with-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration pour des appareils Mac OS X gérés avec le client System Center Configuration Manager
Utilisez l’élément de configuration System Center Configuration Manager **Mac OS X (personnalisé)** pour gérer les paramètres des appareils Mac OS X gérés par le client Configuration Manager.  
  
 Le système d’exploitation Mac OS X utilise des fichiers de liste de propriétés (plist) pour stocker les paramètres d’application. Utilisez les paramètres de compatibilité pour évaluer et corriger les paramètres dans un fichier de liste de propriétés. Vous pouvez également gérer les paramètres Mac OS X en écrivant un script Shell qui retourne une valeur que vous pouvez évaluer et dont vous pouvez corriger la conformité.  
  
### <a name="to-create-a-custom-mac-os-x-configuration-item"></a>Pour créer un élément de configuration Mac OS X personnalisé  
  
1. Dans la console Configuration Manager, cliquez sur **Ressources et conformité**.  
  
2. Dans l'espace de travail **Biens et conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Éléments de configuration**.  
  
3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  
  
4. Dans la page **Général** page de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une éventuelle description pour l’élément de configuration.  
  
5. Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Mac OS X (personnalisé)**.  
  
6. Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  
  
7. Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez les versions Max OS X spécifiques chargées d’évaluer l’élément de configuration.  
  
8. Dans la page **Paramètres** de l’Assistant, vous allez ajouter les nouveaux paramètres dont la compatibilité sera évaluée sur les ordinateurs Mac. Cliquez sur **Nouveau** pour ouvrir la boîte de dialogue **Créer un paramètre** .  
  
9. Dans la boîte de dialogue **Créer un paramètre** , entrez un nom unique et la description du paramètre.  
  
10. Choisissez le **type de paramètre** souhaité, puis fournissez les informations requises, comme indiqué dans le tableau suivant :  
  
    -   **Préférences Mac OS X** -  
  
        -   **ID d’application** : spécifiez l’ID d’application du fichier de liste de propriétés à partir duquel vous voulez évaluer la conformité d’une clé.  
  
             Par exemple, si vous souhaitez modifier les paramètres du navigateur Web Safari, vous pouvez utiliser **com.apple.Safari.plist**.  
  
        -   **Clé** – spécifiez le nom de la clé que vous souhaitez évaluer la conformité sur les ordinateurs Mac. Utilisez la syntaxe suivante : */<dictionnaire>\>/<nom_clé\>*.  
  
            > [!IMPORTANT]  
            >  Le nom de clé respecte la casse et il n’est pas évalué s’il diffère de celui indiqué sur l’ordinateur Mac. De plus, vous ne pouvez pas modifier le nom de clé une fois que vous l’avez spécifié. Si vous devez modifier le nom de clé, supprimez, puis recréez le paramètre.  
  
    -   **Script** -  
  
        -   **Script de découverte** : cliquez sur **Ajouter un Script**, puis entrez un script Shell pour évaluer la conformité des paramètres sur l’ordinateur Mac. Utilisez la commande **echo** dans le script Shell pour retourner des valeurs à Configuration Manager à des fins de conformité. Configuration Manager utilise les résultats retournés dans **STDOUT** pour évaluer la conformité.  
  
            > [!IMPORTANT]  
            >  N’incluez pas la commande **reboot** dans le script de découverte. Étant donné que le script de découverte s'exécute chaque fois redémarrage du client, cela entraînera l'ordinateur Mac à redémarrer en permanence.  
  
        -   **Script de correction (facultatif)** : cliquez éventuellement sur **Ajouter un script** , puis entrez un script Shell utilisé pour corriger les paramètres non compatibles trouvés sur les ordinateurs clients Mac.  
  
            > [!IMPORTANT]  
            >  Pour vous assurer de ne pas introduire de caractères de mise en forme que l’ordinateur Mac ne sait pas interpréter, évitez d’utiliser les options Copier et Coller, mais tapez le script.  
  
11. Choisissez le **Type de données** , c’est-à-dire le format dans lequel la condition retourne les données avant de les utiliser pour évaluer le paramètre.  
  
    > [!NOTE]  
    >  Le type de données **Virgule flottante** prend en charge uniquement 3 chiffres après la virgule décimale.  
    >   
    >  Configuration Manager ne prend pas en charge l’utilisation du type de données **booléen** pour les paramètres de script de l’élément de configuration Mac. Définissez plutôt le type de données sur **Entier** et assurez-vous que le script renvoie une valeur entière.  
  
12. Cliquez sur **OK** pour enregistrer le paramètre et fermer la boîte de dialogue **Créer un paramètre** , puis continuez à ajouter autant de paramètres que nécessaire.  
  
13. Dans la page **Règles de compatibilité** de l’Assistant, vous spécifiez les conditions qui définissent la compatibilité d’un élément de configuration. Pour pouvoir évaluer la compatibilité d’un paramètre, celui-ci doit comporter au moins une règle de compatibilité. Cliquez sur **Nouveau** pour ajouter une nouvelle règle.  
  
14. Dans la boîte de dialogue **Créer une règle** , indiquez les informations suivantes :  
  
    -   **Nom :** Entrez un nom pour la règle de compatibilité.  
  
    -   **Description :** Entrez une description pour la règle de compatibilité.  
  
    -   **Paramètre sélectionné :** Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Paramètre de sélection**. Sélectionnez le paramètre que vous souhaitez définir une règle, ou cliquez sur **nouveau paramètre**. Lorsque vous avez terminé, cliquez sur **Sélectionner**.  
  
        > [!TIP]  
        >  Vous pouvez également cliquer sur **Propriétés** pour afficher des informations sur le paramètre actuellement sélectionné.  
  
    -   **Type de règle :** Sélectionnez le type de règle de compatibilité que vous souhaitez utiliser :  
  
        -   **Valeur :** Créez une règle qui compare la valeur renvoyée par l’élément de configuration par rapport à une valeur que vous spécifiez.  
  
        -   **Existentiel** : créez une règle qui évalue le paramètre, selon qu’il existe sur un périphérique.  
  
    -   Pour un type de règle **Valeur**, spécifiez les informations suivantes :  
  
        -   Le paramètre doit respecter la règle suivante : sélectionnez un opérateur et une valeur dont la compatibilité est évaluée avec le paramètre sélectionné. Vous pouvez utiliser les opérateurs suivants :  
  
            -   **Égal à**  
  
            -   **Non égal à**  
  
            -   **Supérieur à**  
  
            -   **Inférieur à**  
  
            -   **Entre**  
  
            -   **Supérieur ou égal à**  
  
            -   **Inférieur ou égal à**  
  
            -   **L’un des** : dans la zone de texte, spécifiez une seule entrée sur chaque ligne.  
  
            -   **Aucun des** : dans la zone de texte, spécifiez une seule entrée sur chaque ligne.  
  
        -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** : sélectionnez cette option si vous voulez que Configuration Manager corrige automatiquement les règles non compatibles.  
  
            > [!IMPORTANT]  
            >  Vous ne pouvez corriger que les règles non compatibles lorsque l'opérateur de règle est défini sur **Égal à**.  
  
        -   **Signaler la non-compatibilité si l’instance de ce paramètre est introuvable** : l’élément de configuration signale une non-compatibilité si ce paramètre est introuvable sur l’ordinateur Mac.  
  
    -   **Gravité de non-compatibilité pour les rapports** : spécifiez le niveau de gravité signalé en cas d’échec de cette règle de compatibilité. Les niveaux de gravité disponibles sont les suivants :  
  
        -   **Aucun** : les ordinateurs qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  
  
        -   **Informations** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  
  
        -   **Avertissement** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  
  
        -   **Critique** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  
  
        -   **Critique avec événement** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également consigné par l’ordinateur client Mac.  
  
    -   Pour un type de règle **Existentiel**, spécifiez les informations suivantes :  
  
        -   Choisissez parmi :  
  
            -   **Le paramètre doit exister sur les périphériques clients**  
  
            -   **Le paramètre ne doit pas exister sur les appareils clients**  
  
        -   **Gravité de la non conformité pour les rapports :** spécifiez le niveau de gravité qui est signalé en cas d’échec de cette règle de compatibilité. Les niveaux de gravité disponibles sont les suivants :  
  
            -   **Aucun** : les ordinateurs qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  
  
            -   **Informations** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  
  
            -   **Avertissement** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  
  
            -   **Critique** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  
  
            -   **Critique avec événement** : les ordinateurs qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également consigné par l’ordinateur client Mac.  
  
        > [!NOTE]  
        >  Les options affichées peuvent varier selon le type de paramètre pour lequel vous configurez une règle.  
  
    -   Cliquez sur **OK** pour fermer la boîte de dialogue **Créer une règle** .  
  
15. Dans la page **Résumé** , vérifiez les paramètres du nouvel élément de configuration, puis terminez l’Assistant.  
  
    Le nouvel élément de configuration s’affiche dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité** .  
  
    Si vous souhaitez maintenant ajouter cet élément de configuration à une base de référence de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Éléments de configuration pour les appareils gérés avec le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
