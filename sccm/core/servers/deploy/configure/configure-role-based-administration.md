---
title: Configurer l’administration basée sur des rôles
titleSuffix: Configuration Manager
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 554e67e171fe5b800d231d257105531dcd633baf
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131572"
---
# <a name="configure-role-based-administration-for-configuration-manager"></a>Configurer l’administration basée sur des rôles pour Configuration Manager   

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, l’administration basée sur des rôles combine des rôles de sécurité, des étendues de sécurité et des regroupements attribués pour définir l’étendue administrative de chaque utilisateur administratif. Une étendue administrative inclut les objets qu’un utilisateur administratif peut afficher dans la console Configuration Manager et les tâches associées à ces objets que cet administrateur est autorisé à exécuter. Les configurations d'administration basée sur des rôles s'appliquent à chaque site dans une hiérarchie.  

 Si vous n’êtes pas encore familiarisé avec les concepts de l’administration basée sur des rôles, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).  

 Les informations figurant dans les procédures suivantes peuvent vous aider à créer et à configurer une administration basée sur des rôles ainsi que les paramètres de sécurité correspondants :  

-   [Créer des rôles de sécurité personnalisés](#BKMK_CreateSecRole)  

-   [Configurer des rôles de sécurité](#BKMK_ConfigSecRole)  

-   [Configurer des étendues de sécurité pour un objet](#BKMK_ConfigSecScope)  

-   [Configurer des regroupements pour gérer la sécurité](#BKMK_ConfigColl)  

-   [Créer un utilisateur administratif](#BKMK_Create_AdminUser)  

-   [Modifier l’étendue administrative d’un utilisateur administratif](#BKMK_ModAdminUser)  

##  <a name="BKMK_CreateSecRole"></a> Créer des rôles de sécurité personnalisés  
 Configuration Manager fournit plusieurs rôles de sécurité intégrés. Si vous avez besoin de rôles de sécurité supplémentaires, vous pouvez créer un rôle de sécurité personnalisé à l'aide d'une copie d'un rôle de sécurité existant, que vous modifiez par la suite. Vous pouvez créer un rôle de sécurité personnalisé pour accorder aux utilisateurs administratifs les autorisations de sécurité supplémentaires dont ils ont besoin et qui ne figurent pas dans le rôle de sécurité actuellement attribué. Un rôle de sécurité personnalisé permet de leur accorder uniquement les autorisations dont ils ont besoin sans pour autant leur attribuer un rôle de sécurité avec plus d'autorisations que nécessaire.  

 Pour créer un rôle de sécurité à l'aide d'un rôle de sécurité existant en tant que modèle, procédez comme suit.  

#### <a name="to-create-custom-security-roles"></a>Pour créer des rôles de sécurité personnalisés  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Rôles de sécurité**.  

     Utilisez l'une des procédures suivantes pour créer le rôle de sécurité :  

    -   Pour créer un rôle de sécurité personnalisé, effectuez les actions suivantes :  

        1.  Sélectionnez un rôle de sécurité existant à utiliser comme source pour le nouveau rôle de sécurité.  

        2.  Dans l’onglet **Accueil** puis dans le groupe **Rôle de sécurité**, choisissez **Copier**. Cette action crée une copie du rôle de sécurité source.  

        3.  Dans l'Assistant Copier le rôle de sécurité, spécifiez un **Nom** pour le nouveau rôle de sécurité personnalisé.  

        4.  Dans **Attributions d'opérations de sécurité**, développez chaque nœud **Opérations de sécurité** pour afficher les actions disponibles.  

        5.  Pour modifier la configuration d’une opération de sécurité, cliquez sur la flèche vers le bas dans la colonne **Valeur**, puis choisissez **Oui** ou **Non**.  

            > [!CAUTION]  
            >  Lorsque vous configurez un rôle de sécurité personnalisé, veillez à ne pas accorder les autorisations dont les utilisateurs administratifs associés à ce nouveau rôle n’ont pas besoin. Par exemple, la valeur **Modifier** pour l’opération de sécurité **Rôles de sécurité** permet aux utilisateurs administratifs de modifier un rôle auquel ils ont accès, même s’ils ne le possèdent pas.  

        6.  Après avoir configuré les autorisations, choisissez **OK** pour enregistrer le nouveau rôle de sécurité.  

    -   Pour importer un rôle de sécurité exporté à partir d’une autre hiérarchie Configuration Manager, effectuez les actions suivantes :  

        1.  Dans l’onglet **Accueil** puis dans le groupe **Créer**, choisissez **Importer un rôle de sécurité**.  

        2.  Spécifiez le fichier .xml qui contient la configuration du rôle de sécurité que vous souhaitez importer. Choisissez **Ouvrir** pour terminer la procédure et enregistrer le rôle de sécurité.  

            > [!NOTE]  
            >  Après avoir importé un rôle de sécurité, vous pouvez en modifier les propriétés pour changer les autorisations d'objet associées au rôle de sécurité.  

##  <a name="BKMK_ConfigSecRole"></a> Configurer des rôles de sécurité  
 Les groupes d'autorisations de sécurité définis pour un rôle de sécurité sont appelés des attributions d'opérations de sécurité. Les attributions d'opérations de sécurité représentent une association de types d'objet et d'actions disponibles pour chaque type d'objet. Vous pouvez modifier les opérations de sécurité disponibles pour un rôle de sécurité personnalisé, mais pas modifier les rôles de sécurité prédéfinis par Configuration Manager.  

 Utilisez la procédure suivante pour modifier les opérations de sécurité pour un rôle de sécurité.  

#### <a name="to-modify-security-roles"></a>Pour modifier des rôles de sécurité  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Rôles de sécurité**.  

3.  Sélectionnez le rôle de sécurité personnalisé à modifier.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Choisissez l’onglet **Autorisations**.  

6.  Dans **Attributions d'opérations de sécurité**, développez chaque nœud **Opérations de sécurité** pour afficher les actions disponibles.  

7.  Pour modifier la configuration d’une opération de sécurité, cliquez sur la flèche vers le bas dans la colonne **Valeur**, puis choisissez **Oui** ou **Non**.  

    > [!CAUTION]  
    >  Lorsque vous configurez un rôle de sécurité personnalisé, veillez à ne pas accorder les autorisations dont les utilisateurs administratifs associés à ce nouveau rôle n’ont pas besoin. Par exemple, la valeur **Modifier** pour l’opération de sécurité **Rôles de sécurité** permet aux utilisateurs administratifs de modifier un rôle auquel ils ont accès, même s’ils ne le possèdent pas.  

8.  Après avoir terminé la configuration des attributions de l’opération de sécurité, choisissez **OK** pour enregistrer le nouveau rôle de sécurité.  

##  <a name="BKMK_ConfigSecScope"></a> Configurer des étendues de sécurité pour un objet  
 L’association d’une étendue de sécurité à un objet est gérée à partir de l’objet et non à partir de l’étendue de sécurité. Les seules configurations directes prises en charge par l'étendue de sécurité sont les modifications apportées à son nom et à sa description. Pour modifier le nom et la description d'une étendue de sécurité lorsque vous affichez les propriétés d'étendue de sécurité, vous devez disposer de l'autorisation **Modifier** pour l'objet sécurisable **Étendues de sécurité** .  

 Lorsque vous créez un nouvel objet dans Configuration Manager, il est associé à chaque étendue de sécurité associé avec les rôles de sécurité du compte utilisé pour créer l’objet. Ce comportement se produit lorsque ces rôles de sécurité fournissent l’autorisation **Créer** ou l’autorisation **Définir l’étendue de sécurité**. Vous pouvez modifier les étendues de sécurité de l’objet après sa création.  

 Par exemple, un rôle de sécurité accordant l’autorisation de créer un groupe de limites vous est attribué. Lorsque vous créez un groupe de limites, vous n’avez aucune option à laquelle attribuer des étendues de sécurité spécifiques. En revanche, les étendues de sécurité disponibles à partir des rôles de sécurité qui vous sont associés sont attribuées automatiquement au nouveau groupe de limites. Après l’enregistrement du nouveau groupe de limites, vous pouvez modifier les étendues de sécurité qui lui sont associées.  

 Utilisez la procédure suivante pour configurer les étendues de sécurité attribuées à un objet.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Pour configurer des étendues de sécurité pour un objet  

1.  Dans la console Configuration Manager, sélectionnez un objet qui autorise l’attribution à une étendue de sécurité.  

2.  Dans l’onglet **Accueil** puis dans le groupe **Classer**, choisissez **Définir des étendues de sécurité**.  

3.  Dans la boîte de dialogue **Définir des étendues de sécurité** , activez ou désactivez les étendues de sécurité auxquelles cet objet est associé. Chaque objet prenant en charge des étendues de sécurité doit être attribué à une étendue de sécurité au moins.  

4.  Choisissez **OK** pour enregistrer les étendues de sécurité attribuées.  

    > [!NOTE]  
    >  Lorsque vous créez un objet, vous pouvez l'attribuer à plusieurs étendues de sécurité. Pour modifier le nombre d’étendues de sécurité associées à l’objet, vous devez effectuer cette opération une fois l’objet créé.  

##  <a name="BKMK_ConfigColl"></a> Configurer des regroupements pour gérer la sécurité  
 Aucune procédure de configuration de regroupements n'est disponible pour l'administration basée sur des rôles. Il n’existe pas de configuration d’administration basée sur des rôles pour les regroupements. Vous attribuez des regroupements à un utilisateur administratif lorsque vous le configurez. Les opérations de sécurité de regroupement qui sont activées dans les rôles de sécurité attribués aux utilisateurs déterminent les autorisations d’un utilisateur administratif sur les regroupements et les ressources de ces derniers (leurs membres).  

 Lorsqu'un utilisateur administratif dispose d'autorisations sur un regroupement, il dispose également d'autorisations sur des regroupements limités à ce regroupement. Par exemple, votre organisation utilise un regroupement nommé Tous les postes de travail. Il existe également un regroupement nommé Tous les postes de travail en Amérique du Nord, qui est limité au regroupement Tous les postes de travail. Si un utilisateur administratif dispose des autorisations sur Tous les postes de travail, il dispose également des mêmes autorisations sur le regroupement Tous les bureaux en Amérique du Nord.

 En outre, un utilisateur administratif ne peut pas utiliser l’autorisation **Supprimer** ou **Modifier** sur un regroupement qui lui est attribué directement. Mais il peut utiliser ces autorisations sur les regroupements limités à ce regroupement. Dans l’exemple précédent, l’utilisateur administratif peut supprimer ou modifier le regroupement Tous les bureaux en Amérique du Nord, mais pas supprimer ou modifier le regroupement Tous les postes de travail.  

##  <a name="BKMK_Create_AdminUser"></a> Créer un utilisateur administratif  
 Pour accorder aux personnes ou aux membres d’un groupe de sécurité l’accès pour gérer Configuration Manager, créez un utilisateur administratif dans Configuration Manager et spécifiez le compte Windows de l’utilisateur ou du groupe d’utilisateurs. Au moins un rôle de sécurité et une étendue de sécurité doivent être attribués à chaque utilisateur administratif dans Configuration Manager. Vous pouvez également attribuer des regroupements pour limiter l'étendue administrative de l'utilisateur administratif.  

 Utilisez les procédures suivantes pour créer de nouveaux utilisateurs administratifs.  

#### <a name="to-create-a-new-administrative-user"></a>Pour créer un nouvel utilisateur administratif  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Utilisateurs administratifs**.  

3.  Dans l’onglet **Accueil** puis dans le groupe **Créer**, choisissez **Ajouter un utilisateur ou un groupe**.  

4.  Choisissez **Parcourir**, puis sélectionnez le compte d’utilisateur ou le groupe à utiliser pour le nouvel utilisateur administratif.  

    > [!NOTE]  
    >  Pour l'administration basée sur la console, seuls les utilisateurs du domaine ou les groupes de sécurité peuvent devenir des utilisateurs administratifs.  

5.  Dans **Associated security roles (Rôles de sécurité associés)**, choisissez **Ajouter** pour ouvrir la liste des rôles de sécurité disponibles, activez la case à cocher d’un ou de plusieurs rôles de sécurité, puis choisissez **OK**.  

6.  Sélectionnez l’une des deux options suivantes pour définir le comportement de l’objet sécurisable pour le nouvel utilisateur :  

    -   **Toutes les instances des objets liés aux rôles de sécurité assignés** : Cette option associe l’utilisateur administratif avec l’étendue de sécurité **Tous** et les regroupements **Tous les systèmes** et **Tous les utilisateurs et groupes d’utilisateurs**. Les rôles de sécurité attribués à l'utilisateur définissent l'accès aux objets. Les nouveaux objets créés par cet utilisateur administratif sont attribués à l'étendue de sécurité **Par défaut** .  

    -   **Uniquement les instances d’objets assignées aux étendues de sécurité et regroupements spécifiés** : Par défaut, cette option associe l’utilisateur administratif avec l’étendue de sécurité **Par défaut** et les regroupements **Tous les systèmes** et **Tous les utilisateurs et groupes d’utilisateurs**. Toutefois, les étendues de sécurité et les regroupements réels sont limités à ceux qui sont associés au compte que vous avez utilisé pour créer le nouvel utilisateur administratif. Cette option prend en charge l'ajout ou la suppression d'étendues de sécurité et de regroupements pour personnaliser l'étendue administrative de l'utilisateur administratif.  

    > [!IMPORTANT]  
    >  Les options précédentes associent chaque étendue de sécurité et chaque regroupement attribués, à chaque rôle de sécurité attribué à l’utilisateur administratif. Vous pouvez utiliser une troisième option, **Associer des rôles de sécurité attribués à des étendues de sécurité et à des regroupements spécifiques** pour associer des rôles de sécurité individuels à des étendues de sécurité à des regroupements spécifiques. Cette troisième option est disponible après la création du nouvel utilisateur administratif, lorsque vous modifiez l'utilisateur administratif.  

7.  Selon l'option sélectionnée à l'étape 6, effectuez l'action suivante :  

    -   Si vous avez sélectionné **Toutes les instances d’objets liés aux rôles de sécurité attribués**, choisissez **OK** pour terminer cette procédure.  

    -   Si vous avez sélectionné **Uniquement les instances d’objets attribués aux étendues de sécurité et aux regroupements spécifiés**, choisissez **Ajouter** pour sélectionner des regroupements et des étendues de sécurité supplémentaires. Vous pouvez également sélectionner un ou plusieurs objets dans la liste, puis choisir **Supprimer** pour les supprimer. Choisissez **OK** pour terminer cette procédure.  

##  <a name="BKMK_ModAdminUser"></a> Modifier l’étendue administrative d’un utilisateur administratif  
 Vous pouvez modifier l'étendue administrative d'un utilisateur administratif en ajoutant ou en supprimant des rôles de sécurité, des étendues de sécurité et des regroupements associés à l'utilisateur. Chaque utilisateur administratif doit être associé à au moins un rôle de sécurité et une étendue de sécurité. Vous devrez peut-être affecter un ou plusieurs regroupements à l'étendue administrative de l'utilisateur. La plupart des rôles de sécurité interagissent avec les regroupements et ne fonctionnent pas correctement sans regroupement attribué.  

 Lorsque vous modifiez un utilisateur administratif, vous pouvez modifier le comportement des objets sécurisables au niveau de leur association avec les rôles de sécurité attribués. Les trois comportements que vous pouvez sélectionner sont les suivants :  

-   **Toutes les instances des objets liés aux rôles de sécurité assignés** : Cette option associe l’utilisateur administratif avec l’étendue **Tous** et les regroupements **Tous les systèmes** et **Tous les utilisateurs et groupes d’utilisateurs**. Les rôles de sécurité attribués à l'utilisateur définissent l'accès aux objets.  

-   **Uniquement les instances d’objets assignées aux étendues de sécurité et regroupements spécifiés** : cette option associe l'utilisateur administratif aux mêmes étendues de sécurité et regroupements qui sont associés au compte que vous utilisez pour configurer l'utilisateur administratif. Cette option prend en charge l'ajout ou la suppression de rôles de sécurité et de regroupements pour personnaliser l'étendue administrative de l'utilisateur administratif.  

-   **Associer des rôles de sécurité assignés à des étendues de sécurité et des regroupements spécifiques** : cette option vous permet de créer des associations spécifiques entre des rôles de sécurité individuels et des étendues de sécurité et des regroupements spécifiques pour l'utilisateur.  

    > [!NOTE]  
    >  Cette option est disponible uniquement lorsque vous modifiez les propriétés d'un utilisateur administratif.  

La configuration actuelle du comportement de l'objet sécurisable modifie le processus qui vous permet d'attribuer des rôles de sécurité supplémentaires. Utilisez les procédures suivantes, basées sur les différentes options des objets sécurisables, pour vous aider à gérer un utilisateur administratif.  

Utilisez la procédure suivante pour afficher et gérer la configuration des objets sécurisables pour un utilisateur administratif.  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Pour afficher et gérer le comportement de l'objet sécurisable pour un utilisateur administratif  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Choisissez l’onglet **Étendues de sécurité** pour afficher la configuration actuelle des objets sécurisables de cet utilisateur administratif.  

6.  Pour modifier le comportement de l'objet sécurisable, sélectionnez une nouvelle option pour le comportement de l'objet sécurisable. Après avoir modifié cette configuration, consultez la procédure appropriée pour obtenir des instructions supplémentaires sur la configuration des étendues de sécurité et des regroupements ainsi que des rôles de sécurité pour cet utilisateur administratif.  

7.  Choisissez **OK** pour terminer la procédure.  

Utilisez la procédure suivante pour modifier un utilisateur administratif dont le comportement d’objet sécurisable est **Toutes les instances d’objets liés aux rôles de sécurité attribués**.  

#### <a name="for-option-all-instances-of-the-objects-that-are-related-to-the-assigned-security-roles"></a>Concernant l’option : Toutes les instances des objets liés aux rôles de sécurité assignés  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Cliquez sur l’onglet **Étendues de sécurité** afin de confirmer que l’utilisateur administratif est configuré pour **Toutes les instances d’objets liés aux rôles de sécurité auxquels ils sont associés**.  

6.  Pour modifier les rôles de sécurité attribués, choisissez l’onglet **Rôles de sécurité**.  

    -   Pour attribuer des rôles de sécurité supplémentaires à cet utilisateur administratif, choisissez **Ajouter**, activez la case à cocher de chaque rôle de sécurité supplémentaire que vous souhaitez attribuer, puis choisissez **OK**.  

    -   Pour supprimer des rôles de sécurité, sélectionnez-en un ou plusieurs dans la liste, puis choisissez **Supprimer**.  

7.  Pour modifier le comportement de l’objet sécurisable, choisissez l’onglet **Étendues de sécurité** et sélectionnez une nouvelle option pour le comportement de l’objet sécurisable. Après avoir modifié cette configuration, consultez la procédure appropriée pour obtenir des instructions supplémentaires sur la configuration des étendues de sécurité et des regroupements ainsi que des rôles de sécurité pour cet utilisateur administratif.  

    > [!NOTE]  
    >  Lorsque le comportement de l’objet sécurisable est **Toutes les instances d’objets liés aux rôles de sécurité attribués**, vous ne pouvez ni ajouter ni supprimer des étendues de sécurité ou des regroupements spécifiques.  

8.  Choisissez **OK** pour terminer cette procédure.  

Utilisez la procédure suivante pour modifier un utilisateur administratif dont le comportement de l'objet sécurisable est paramétré sur **Uniquement les instances d’objets attribués aux étendues de sécurité et aux regroupements spécifiés**.  

#### <a name="for-option-only-the-instances-of-objects-that-are-assigned-to-the-specified-security-scopes-and-collections"></a>Concernant l’option : Uniquement les instances d’objets assignées aux étendues de sécurité et regroupements spécifiés  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Choisissez l’onglet **Étendues de sécurité** afin de confirmer que l’utilisateur est configuré pour **Uniquement les instances d’objets attribués aux étendues de sécurité et aux regroupements spécifiés**.  

6.  Pour modifier les rôles de sécurité attribués, choisissez l’onglet **Rôles de sécurité**.  

    -   Pour attribuer des rôles de sécurité supplémentaires à cet utilisateur, choisissez **Ajouter**, activez la case à cocher de chaque rôle de sécurité supplémentaire que vous souhaitez attribuer, puis choisissez **OK**.  

    -   Pour supprimer des rôles de sécurité, sélectionnez-en un ou plusieurs dans la liste, puis choisissez **Supprimer**.  

7.  Pour modifier les étendues de sécurité et les regroupements associés aux rôles de sécurité, choisissez l’onglet **Étendues de sécurité**.  

    -   Pour associer de nouvelles étendues de sécurité ou de nouveaux regroupements à tous les rôles de sécurité attribués à cet utilisateur administratif, choisissez **Ajouter** et sélectionnez l’une des quatre options. Si vous sélectionnez **Étendue de sécurité** ou **Regroupement**, activez la case à cocher d’un ou de plusieurs objets pour terminer cette sélection, puis choisissez **OK**.  

    -   Pour supprimer une étendue de sécurité ou un regroupement, sélectionnez l’objet puis choisissez **Supprimer**.  

8.  Choisissez **OK** pour terminer cette procédure.  

Utilisez la procédure suivante pour modifier un utilisateur administratif pour lequel le comportement de l'objet sécurisable est paramétré sur **Associer des rôles de sécurité attribués à des étendues de sécurité et à des regroupements spécifiques**.  

#### <a name="for-option-associate-assigned-security-roles-with-specific-security-scopes-and-collections"></a>Concernant l’option : Associer des rôles de sécurité assignés à des étendues de sécurité et des regroupements spécifiques  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Sécurité**, puis choisissez **Utilisateurs administratifs**.  

3.  Sélectionnez l'utilisateur administratif à modifier.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Choisissez l’onglet **Étendues de sécurité** afin de confirmer que l’utilisateur administratif est configuré pour **Associer des rôles de sécurité attribués à des étendues de sécurité et à des regroupements spécifiques**.  

6.  Pour modifier les rôles de sécurité attribués, choisissez l’onglet **Rôles de sécurité**.  

    -   Pour attribuer des rôles de sécurité supplémentaires à cet utilisateur administratif, choisissez **Ajouter**. Dans la boîte de dialogue **Ajouter un rôle de sécurité**, sélectionnez un ou plusieurs rôles de sécurité disponibles, choisissez **Ajouter**, puis sélectionnez un type d’objet à associer aux rôles de sécurité sélectionnés. Si vous sélectionnez **Étendue de sécurité** ou **Regroupement**, activez la case à cocher d’un ou de plusieurs objets pour terminer cette sélection, puis choisissez **OK**.  

        > [!NOTE]  
        >  Vous devez configurer au moins une étendue sécurité avant que les rôles de sécurité sélectionnés puissent être attribués à l'utilisateur administratif. Lorsque vous sélectionnez plusieurs rôles de sécurité, chaque étendue de sécurité et regroupement que vous configurez est associé à chacun des rôles de sécurité sélectionnés.  

    -   Pour supprimer des rôles de sécurité, sélectionnez-en un ou plusieurs dans la liste, puis choisissez **Supprimer**.  

7.  Pour modifier les étendues de sécurité et les regroupements associés à un rôle de sécurité spécifique, choisissez l’onglet **Étendues de sécurité**, sélectionnez le rôle de sécurité, puis choisissez **Modifier**.  

    -   Pour associer de nouveaux objets à ce rôle de sécurité, choisissez **Ajouter** et sélectionnez le type d’objet à associer aux rôles de sécurité sélectionnés. Si vous sélectionnez **Étendue de sécurité** ou **Regroupement**, activez la case à cocher d’un ou de plusieurs objets pour terminer cette sélection, puis choisissez **OK**.  

        > [!NOTE]  
        >  Vous devez configurer au moins une étendue de sécurité.  

    -   Pour supprimer une étendue de sécurité ou un regroupement associé à ce rôle de sécurité, sélectionnez l’objet et choisissez **Supprimer**.  

    -   Lorsque vous avez terminé de modifier les objets associés, choisissez **OK**.  

8.  Choisissez **OK** pour terminer cette procédure.  

    > [!CAUTION]  
    >  Lorsqu'un rôle de sécurité accorde aux utilisateurs administratifs l'autorisation de déployer un regroupement, ces utilisateurs administratifs peuvent distribuer des objets depuis n'importe quelle étendue de sécurité pour laquelle il disposent d'autorisations de **Lecture** , même si cette étendue de sécurité est associée à un rôle de sécurité différent.  
