---
title: Technical Preview 1801 | Microsoft Docs
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1801 pour System Center Configuration Manager.
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5a352ae0-355f-4fcf-b863-fb0654f51c52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 995c84e51ec72b385390f76fabfe08d60c2832d7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1801-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1801 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version Technical Preview 1801 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. 

Consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview) avant d’installer cette version Technical Preview. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problèmes connus dans cette version d’évaluation technique :**
-   **La mise à jour vers une nouvelle préversion échoue s’il existe un serveur de site en mode passif**. Si vous avez un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez désinstaller le serveur de site en mode passif avant de procéder à la mise à jour vers cette nouvelle préversion. Vous pouvez réinstaller le serveur de site en mode passif une fois votre site mis à jour.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.
<!--sms 489412-->


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## <a name="create-phased-deployments"></a>Créer des déploiements par phases
<!-- 1357405 -->
Les déploiements par phases permettent d’automatiser le déploiement coordonné et séquencé de logiciels sans devoir créer plusieurs déploiements. Dans cette version Technical Preview, l’Assistant Déploiement par phases peut être utilisé pour des séquences de tâches dans la console d’administration. Les déploiements ne sont cependant pas créés. 

### <a name="try-it-out"></a>Essayez !  
  Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.
 
**Créer un déploiement par phases pour une séquence de tâches** </br>
1. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.
2. Cliquez avec le bouton droit sur une séquence de tâches et sélectionnez **Créer un déploiement par phases**. 
3. Sous l’onglet **Général**, spécifiez un nom et une description (facultative) pour le déploiement par phases, puis sélectionnez **Créer automatiquement des phases pilote et de production par défaut**. 
4. Renseignez les champs **Regroupement pilote** et **Regroupement de production**. Sélectionnez **Suivant**.
5. Sous l’onglet **Paramètres**, choisissez une option pour chacun des paramètres de planification, puis sélectionnez **Suivant** quand vous avez terminé. 
6. Sous l’onglet **Phases**, modifiez les phases si nécessaire, puis cliquez sur **Suivant**.
7. Vérifiez vos sélections sous l’onglet **Récapitulatif**, puis cliquez sur **Suivant** pour continuer.

## <a name="co-management-reporting"></a>Rapports de cogestion
<!-- 1356648 -->
Si vous utilisez les fonctionnalités de [cogestion](/sccm/core/clients/manage/co-management-overview), vous pouvez désormais voir un tableau de bord avec des informations sur la cogestion dans votre environnement. Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, développez **Upgrade Readiness**, puis sélectionnez le tableau de bord **Cogestion**. Le tableau de bord comprend les vignettes suivantes :
- **Appareils cogérés** : le pourcentage d’appareils de votre environnement pour lesquels vous avez activé la cogestion
- **Distribution des systèmes d’exploitation** : la répartition des systèmes d’exploitation par version. Ce graphique utilise les regroupements suivants :
   - Windows 7 et 8.x
   - Windows 10 antérieur à 1709
   - Windows 10 1709 et ultérieur
  > [!NOTE] 
  > Windows 10 version 1709 et ultérieure est un prérequis pour la cogestion
- **État de la cogestion** : la répartition des réussites et des échecs des appareils selon les catégories suivantes :
   - Réussite, Joint à une version hybride d’Azure AD
   - Réussite, Joint à Azure AD
   - Échec : Échec de l’inscription automatique
- **Transition des charges de travail** : un graphique à barres montrant le nombre d’appareils que vous avez fait passer à Microsoft Intune pour les trois charges de travail disponibles : 
   - Stratégies de conformité
   - Accès aux ressources
   - Windows Update for Business

### <a name="prerequisites"></a>Prérequis
- L’ordinateur qui exécute la console Configuration Manager nécessite Internet Explorer 9 ou ultérieur.



## <a name="improvements-to-automatic-deployment-rule-evaluation-schedule"></a>Améliorations apportées à la planification de l’évaluation des règles de déploiement automatique
<!-- 1357133 -->
Suite à vos [commentaires sur User Voice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8819518-software-update-patch-tuesday-scheduling), vous pouvez maintenant planifier l’évaluation des règles déploiement automatique en décalé par rapport à un jour de référence. Par exemple, un décalage de deux jours après le deuxième mardi du mois évalue la règle le jeudi qui suit. 

### <a name="try-it-out"></a>Essayez !  
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné. <br/>

**Créer une planification personnalisée qui évalue un décalage des règles de déploiement automatique par rapport à un jour de référence** </br>
1.  Dans l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles** et sélectionnez **Règles de déploiement automatique**.
2. Cliquez avec le bouton droit sur **Règles de déploiement automatique** et choisissez **Créer une règle de déploiement automatique**. 
3. Suivez les invites pour renseigner les onglets **Général**, **Paramètres de déploiement** et **Mises à jour logicielles**. 
4. Sous l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier** et **Personnaliser**.
5. Pour le calendrier personnalisé, sélectionnez **Mensuel** et désignez un jour de référence, par exemple le deuxième mardi. 
6. Cochez **Décalage (en jours)** et sélectionnez le nombre de jours pour le décalage, puis cliquez sur **OK** quand vous avez terminé.  
7. Effectuez le reste des étapes de **l’Assistant Création d’une règle de déploiement automatique**. 



## <a name="reassign-distribution-point"></a>Réaffecter un point de distribution
<!-- 1306937 -->
De nombreux clients ont de grandes infrastructures Configuration Manager et réduisent le nombre de sites principaux ou secondaires pour simplifier leur environnement. Ils doivent néanmoins toujours conserver des points de distribution aux emplacements des filiales pour délivrer du contenu aux clients gérés. Ces points de distribution contiennent souvent plusieurs téraoctets ou plus de contenus. Ce contenu est coûteux en termes de temps et de bande passante réseau pour le distribuer à ces serveurs distants. 

Cette fonctionnalité vous permet de réaffecter un point de distribution à un autre site principal sans redistribuer le contenu. Cette action met à jour l’affectation du système de site tout en conservant la totalité du contenu sur le serveur. Si vous devez réaffecter plusieurs points de distribution, effectuez d’abord cette action sur un seul point de distribution, puis poursuivez avec les serveurs supplémentaires, un par un.

> [!IMPORTANT]
> Le serveur de système de site peut seulement héberger le rôle de point de distribution. Si le serveur de système de site héberge un autre rôle serveur Configuration Manager, comme le point de migration d’état, vous ne pouvez pas réaffecter le point de distribution. Vous ne pouvez pas réaffecter un point de distribution cloud. 

Cette option ne fonctionne pas avec cette version en raison de la limitation de la version Technical Preview à un seul site principal. Étudiez le scénario, puis envoyez vos **commentaires** sous l’onglet **Accueil** du ruban, concernant les fonctionnalités de cette action.
1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Points de distribution**.
2. Cliquez avec le bouton droit sur le point de distribution cible, puis sélectionnez **Réaffecter le point de distribution**. 
  ![Réaffecter un point de distribution](media/1306937-reassign-dp.png)
3. Sélectionnez le serveur de site et le code de site auquel vous voulez réaffecter ce point de distribution. 
  ![Sélectionner un serveur de site](media/1306937-select-site.png)



## <a name="improvements-to-hardware-inventory"></a>Améliorations apportées à l’inventaire matériel
<!-- 1357389 -->
Pour les classes nouvellement ajoutées, des chaînes supérieures à 255 caractères peuvent être spécifiées pour les propriétés d’inventaire matériel qui ne sont pas des clés.

### <a name="try-it-out"></a>Essayez !  
Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.<br/>

1. Dans l’espace de travail **Administration**, cliquez sur **Paramètres client**, mettez en surbrillance un appareil client à modifier, cliquez avec le bouton droit, puis sélectionnez **Propriétés**. 
2. Sélectionnez **Inventaire matériel**, puis **Définir des classes** et **Ajouter**.
3. Cliquez sur le bouton **Connecter**.
4. Renseignez **Nom de l’ordinateur** et **Espace de noms WMI**, et sélectionnez **Récursif** si nécessaire. Fournissez si nécessaire les informations d’identification pour la connexion. Cliquez sur **Connecter** pour afficher les classes de l’espace de noms.
5. Sélectionnez une nouvelle classe, puis cliquez sur **Modifier**.
6. Changez la **Longueur** d’au moins une propriété autre que la clé et qui soit une chaîne, pour une valeur supérieure à 255. Cliquez sur **OK**. 
7. Vérifiez que la propriété modifiée est sélectionnée pour **Ajouter une classe d’inventaire matériel** et cliquez sur **OK**. 
8. Collectez l’inventaire matériel avec la classe que vous venez d’ajouter, qui contient une propriété avec une longueur supérieure à 255 caractères. 



## <a name="improvements-to-client-settings-for-software-center"></a>Améliorations apportées aux paramètres des clients pour le Centre logiciel
<!-- 1351224 & 1355146 -->
Dans cette version Technical Preview, des améliorations ont été apportées à la personnalisation du Centre logiciel sous les paramètres client. 

1. Les paramètres client pour le Centre logiciel ont maintenant un bouton **Personnaliser**.
2. Un aperçu a été ajouté pour montrer à quoi ressemble la bannière du Centre logiciel.<!--1351224-->
    - Si aucun logo n’est sélectionné, l’aperçu montre le texte et la couleur du nom de l’entreprise.
    - Si un logo est sélectionné, l’aperçu montre le logo et le texte du nom de l’entreprise.  
3.  **Masquer les applications non approuvées dans le Centre logiciel** est un nouveau paramètre du Centre logiciel. Quand cette option est activée, les applications disponibles pour l’utilisateur qui nécessitent une approbation sont masquées dans le Centre logiciel.<!--1355146-->

### <a name="try-it-out"></a>Essayez !  
 Essayez d’effectuer les tâches. Envoyez ensuite des **commentaires** à partir de l’onglet **Accueil** du ruban et faites-nous savoir comment cela a fonctionné.

1. Dans l’espace de travail **Administration**, cliquez sur **Paramètres client**. Sélectionnez un paramètre d’appareil client à modifier. Cliquez avec le bouton droit sur celui-ci, sélectionnez **Propriétés**, puis **Centre logiciel**.
2.  Cliquez sur le bouton **Personnaliser**. Testez les différents paramètres de personnalisation, notamment l’aperçu.
3. Activez le paramètre **Masquer des applications non approuvées dans le Centre logiciel**. Observez les changements dans le Centre logiciel. 



## <a name="new-settings-for-windows-defender-application-guard"></a>Nouveaux paramètres pour Windows Defender Application Guard
<!-- 1356256 -->
Pour les appareils avec Windows 10 version 1709 et ultérieur, il existe deux nouveaux paramètres d’interaction d’hôte pour [Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy). 
1. Vous pouvez autoriser les sites web à accéder au processeur graphique virtuel de l’hôte. 
2. Les fichiers téléchargés dans le conteneur peuvent être conservés sur l’hôte. </br>



## <a name="improvements-to-run-scripts"></a>Améliorations apportées à l’exécution de scripts
<!-- 1236459 -->
La fonctionnalité [**Exécuter les scripts**](/sccm/apps/deploy-use/create-deploy-scripts) vous permet désormais d’importer et d’exécuter des scripts PowerShell signés. 
- Pour conserver l’intégrité des scripts, vous devez importer les scripts signés et non pas utiliser le copier/coller. 
- Vous ne pouvez pas modifier les scripts signés après les avoir importés.
    
>[!IMPORTANT]
>Cette version Technical Preview a deux limitations temporaires.
>- Les scripts peuvent seulement être importés dans la fonctionnalité Exécuter les scripts et ils ne peuvent pas être modifiés directement à partir de la console.
>- Les scripts importés avec un encodage non-Unicode risquent de ne pas s’afficher correctement dans la console. Ils s’exécutent néanmoins tels qu’ils ont été écrits à l’origine.





## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
