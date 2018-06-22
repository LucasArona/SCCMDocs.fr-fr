---
title: Gérer les paramètres des mises à jour logicielles
titleSuffix: Configuration Manager
description: Découvrez les paramètres client adaptés aux mises à jour logicielles sur votre site après avoir installé le point de mise à jour logicielle.
author: aczechowski
ms.date: 03/26/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ad44beeb662cb0cd5cf083b18721d88a5b7360c4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351613"
---
#  <a name="BKMK_ManageSUSettings"></a> Gérer les paramètres des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir synchronisé les mises à jour logicielles dans Configuration Manager, configurez et vérifiez les paramètres décrits dans les sections suivantes.

##  <a name="BKMK_ClientSettings"></a> Paramètres client pour les mises à jour logicielles  
Après avoir installé le point de mise à jour logicielle, les mises à jour logicielles sont activées sur les clients par défaut, et les paramètres client figurant dans la page **Mises à jour logicielles** affichent les valeurs par défaut. Les paramètres client s’appliquent au site tout entier et déterminent à quel moment la conformité des mises à jour logicielles est analysée et quand et comment les mises à jour logicielles sont installées sur les ordinateurs clients. Avant de déployer des mises à jour logicielles, vérifiez que les paramètres client conviennent pour des mises à jour logicielles sur votre site.  

> [!IMPORTANT]  
>  Le paramètre **Activer les mises à jour logicielles sur les clients** est activé par défaut. Si vous désactivez ce paramètre, Configuration Manager supprime les stratégies de déploiement existantes du client.  

Pour plus d’informations sur la configuration des paramètres client, consultez [Guide pratique pour configurer les paramètres client dans Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

Pour plus d’informations sur les paramètres client, consultez [À propos des paramètres client dans Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

##  <a name="BKMK_GroupPolicy"></a> Paramètres de stratégie de groupe pour les mises à jour logicielles  
L’Agent Windows Update (WUA) utilise des paramètres de stratégie de groupe spécifiques sur les ordinateurs clients pour se connecter au serveur WSUS qui s’exécute sur le point de mise à jour logicielle. Ces paramètres de stratégie de groupe servent aussi à analyser la conformité des mises à jour logicielles et à mettre à jour automatiquement les mises à jour logicielles et l’Agent WUA.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>Spécifier la stratégie locale d’emplacement intranet du service Microsoft Update  
Lorsque vous créez le point de mise à jour logicielle pour un site, les clients reçoivent une stratégie ordinateur qui précise le nom du serveur du point de mise à jour logicielle et configure la stratégie locale **Spécifier l'emplacement Intranet du service de mise à jour Microsoft** sur l'ordinateur. L'Agent Windows Update (WUA) extrait le nom du serveur qui est spécifié dans le paramètre **Configurer le service intranet de mise à jour pour la détection des mises à jour** , puis se connecte à ce serveur au moment d'évaluer la conformité des mises à jour logicielles. Quand vous créez une stratégie de domaine pour le paramètre **Spécifier l’emplacement intranet du service de mise à jour Microsoft** , elle remplace la stratégie locale et il est possible que l’Agent WUA se connecte à un autre serveur que le point de mise à jour logicielle. Si cela se produit, le client peut analyser la conformité des mises à jour logicielles d'après différents produits, classifications et langues. Par conséquent, vous ne devez pas configurer la stratégie Active Directory pour les ordinateurs clients.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>Autoriser le contenu signé à partir de la stratégie de groupe d’emplacement intranet du service Microsoft Update  
Pour que l'agent WUA installé sur les ordinateurs recherche les mises à jour logicielles créées et publiées à l'aide de l'éditeur de mise à jour System Center, vous devez activer le paramètre de stratégie de groupe **Autoriser les contenus signés provenant d'un emplacement intranet du service de Mise à jour Microsoft** . Une fois le paramètre de stratégie activé, WUA accepte les mises à jour logicielles reçues via un emplacement Intranet, à condition qu'elles soient signées dans le magasin de certificats **Éditeurs approuvés** de l'ordinateur local. Pour plus d'informations sur les paramètres de stratégie de groupe requis pour l'éditeur de mise à jour, voir [Updates Publisher 2011 Documentation Library (Bibliothèque de documentation Updates Publisher 2011)](http://go.microsoft.com/fwlink/p/?LinkId=232476).  

### <a name="automatic-updates-configuration"></a>Configuration des mises à jour automatiques  
Le service Mises à jour automatiques permet de recevoir des mises à jour de sécurité et d'autres éléments téléchargés sur des ordinateurs clients. Ce service peut être configuré par le biais du paramètre de stratégie de groupe **Configuration du service Mises à jour automatiques** ou par le biais du Panneau de configuration de l'ordinateur local. Lorsque le service Mises à jour automatiques est activé, les ordinateurs clients reçoivent des notifications de mise à jour, et ils téléchargent et installent les mises à jour requises, en fonction des paramètres configurés. Si le service Mises à jour automatiques est utilisé conjointement avec des mises à jour logicielles, chaque ordinateur client peut afficher des icônes de notification et des notifications contextuelles pour la même mise à jour. En outre, si un redémarrage est nécessaire, chaque ordinateur client peut afficher une boîte de dialogue de redémarrage pour la même mise à jour.  

### <a name="self-update"></a>Mise à jour automatique  
Lorsque le service Mises à jour automatiques est activé sur les ordinateurs clients, l'agent WUA procède à une mise à jour automatique dès qu'une nouvelle version est disponible ou si des problèmes liés à un composant WUA surviennent. Lorsque le service Mises à jour automatiques n'est pas configuré ou est désactivé, et que les ordinateurs clients disposent d'une version antérieure de WUA, ces derniers doivent exécuter le fichier d'installation de WUA.  

## <a name="software-updates-properties"></a>Propriétés des mises à jour logicielles
Les propriétés de mise à jour logicielle fournissent des informations sur les mises à jour logicielles et leur contenu associé. Vous pouvez également utiliser ces propriétés pour configurer les paramètres des mises à jour logicielles. Lorsque vous ouvrez les propriétés de plusieurs mises à jour logicielles, seuls les onglets **Durée maximale d'exécution** et **Gravité personnalisée** s'affichent.   

Pour ouvrir les propriétés de mise à jour logicielle, procédez comme suit.  

#### <a name="to-open-software-update-properties"></a>Pour ouvrir les propriétés de mise à jour logicielle  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  
2.  Dans l'espace de travail Bibliothèque de logiciels, développez **Mises à jour logicielles**et cliquez sur **Toutes les mises à jour logicielles**.  
3.  Sélectionnez une ou plusieurs mises à jour logicielles, puis, sous l'onglet **Accueil** , cliquez sur **Propriétés** dans le groupe **Propriétés** .  

   > [!NOTE]  
   >  Dans le nœud **Toutes les mises à jour logicielles**, Configuration Manager affiche uniquement les mises à jour logicielles classées selon les critères **Critique** et **Sécurité** qui ont été publiées au cours des 30 derniers jours.  

###  <a name="BKMK_SoftwareUpdatesInformation"></a> Consulter les informations relatives aux mises à jour logicielles  
Dans les propriétés de mise à jour logicielle, vous pouvez consulter des informations détaillées sur une mise à jour logicielle. Les informations détaillées ne sont pas affichées lorsque vous sélectionnez plusieurs mises à jour logicielles. Les sections suivantes décrivent les informations disponibles pour une mise à jour logicielle sélectionnée.  

####  <a name="BKMK_SoftwareUpdateDetails"></a> Détails des mises à jour logicielles  
Sous l'onglet **Détails de la mise à jour** , vous pouvez consulter les informations récapitulatives suivantes relatives à la mise à jour logicielle sélectionnée :  

- **ID du bulletin**: indique l’ID du bulletin associé aux mises à jour logicielles de sécurité. Vous trouverez des détails sur le bulletin de sécurité en effectuant une recherche sur l'ID du bulletin sur la page Web [Recherche des bulletins de sécurité de Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=58313) .  

- **Article ID**: indique l’ID de l’article pour la mise à jour logicielle. L'article référencé fournit des informations détaillées sur la mise à jour logicielle et le problème qu'elle corrige ou améliore.  

- **Date de révision**: indique la date à laquelle la mise à jour logicielle a été modifiée pour la dernière fois.  

- **Taux de gravité maximal**: indique le taux de gravité défini par le fournisseur pour la mise à jour logicielle.  

- **Description**: fournit une vue d’ensemble de la condition que la mise à jour logicielle corrige ou améliore.  

- **Langues applicables**: indique les langues pour lesquelles la mise à jour logicielle est applicable.  

- **Produits affectés**: indique les produits pour lesquels la mise à jour logicielle est applicable.  

####  <a name="BKMK_ContentInformation"></a> Informations de contenu  
Sous l'onglet **Informations de contenu** , consultez les informations suivantes sur le contenu associé à la mise à jour logicielle sélectionnée :  

-   **ID du contenu**: indique l’ID du contenu pour la mise à jour logicielle.  

-   **Téléchargé** : indique si Configuration Manager a téléchargé les fichiers de la mise à jour logicielle.  

-   **Langue**: indique les langues de la mise à jour logicielle.  

-   **Chemin source**: indique le chemin des fichiers sources de la mise à jour logicielle.  

-   **Taille (Mo)**: indique la taille des fichiers sources de la mise à jour logicielle.  

####  <a name="BKMK_CustomBundleInformation"></a> Informations sur le groupement personnalisé  
Dans l'onglet **Informations sur le groupement personnalisé** , consultez les informations sur le groupement personnalisé pour la mise à jour logicielle. Lorsque la mise à jour logicielle sélectionnée contient des mises à jour logicielles regroupées situées dans le fichier de mise à jour logicielle, celles-ci sont affichées dans la section **Informations sur le groupement** . Cet onglet n'affiche pas les mises à jour logicielles groupées qui apparaissent sous l'onglet **Informations de contenu** , notamment les fichiers de mise à jour des différentes langues.  

####  <a name="BKMK_SupersedenceInformation"></a> Informations de remplacement  
Sous l'onglet **Informations de remplacement** , vous pouvez voir les informations suivantes sur le remplacement de la mise à jour logicielle :  

- **Cette mise à jour a été remplacée par les mises à jour suivantes**: indique les mises à jour logicielles qui remplacent cette mise à jour, ce qui signifie que les mises à jour répertoriées sont plus récentes. Dans la plupart des cas, vous allez déployer l'une des mises à jour logicielles qui remplace la mise à jour logicielle. Les mises à jour logicielles qui sont répertoriées dans la liste contiennent des liens hypertexte vers des pages Web qui fournissent davantage d'informations sur les mises à jour logicielles. Lorsque cette mise à jour n'est pas remplacée, l'option **Aucune** s'affiche.  

- **Cette mise à jour remplace les mises à jour suivantes**: spécifie les mises à jour logicielles remplacées par cette mise à jour logicielle, ce qui signifie que cette mise à jour logicielle est plus récente. Dans la plupart des cas, vous allez déployer cette mise à jour logicielle pour qu'elle se substitue aux mises à jour logicielles remplacées. Les mises à jour logicielles qui sont répertoriées dans la liste contiennent des liens hypertexte vers des pages Web qui fournissent davantage d'informations sur les mises à jour logicielles. Lorsque cette mise à jour n'en remplace aucune autre, **Aucun** s'affiche.  

###  <a name="BKMK_SoftwareUpdatesSettings"></a> Configurer les paramètres de mise à jour logicielle  
Dans les propriétés, vous pouvez configurer les paramètres d'une ou plusieurs mises à jour logicielles. Vous pouvez configurer la plupart des paramètres des mises à jour logicielles uniquement au niveau du site d'administration centrale ou du site principal autonome. Aidez-vous des sections suivantes pour configurer les paramètres des mises à jour logicielles.  

####  <a name="BKMK_SetMaxRunTime"></a> Définir la durée maximale d’exécution  
Sous l'onglet **Durée maximale d'exécution** , définissez la durée maximale dont dispose une mise à jour logicielle pour s'exécuter sur des ordinateurs clients. Si la mise à jour prend plus de temps que la durée maximale d’exécution, Configuration Manager crée un message d’état et cesse de surveiller le déploiement de l’installation des mises à jour logicielles. Vous pouvez configurer ce paramètre uniquement sur le site d'administration centrale ou un site principal autonome.  

Configuration Manager utilise aussi ce paramètre pour déterminer s’il est nécessaire de lancer l’installation des mises à jour logicielles au cours d’une fenêtre de maintenance configurée. Si la durée maximale d'exécution est supérieure au temps restant défini dans la fenêtre de maintenance, l'installation des mises à jour logicielles est reportée jusqu'au démarrage de la fenêtre de maintenance suivante. Si plusieurs mises à jour logicielles doivent être installées sur un ordinateur client via une fenêtre de maintenance configurée (plage de temps), la mise à jour logicielle dont la durée d'exécution maximale est la plus courte sera tout d'abord installée, suivie de celle présentant la durée la plus courte suivante, et ainsi de suite. Avant d'installer chaque mise à jour logicielle, le client vérifie que la fenêtre de maintenance disponible est suffisante pour permettre l'installation de la mise à jour logicielle. Après le début de l'installation d'une mise à jour logicielle, celle-ci se poursuit même si elle n'est pas terminée avant la fermeture de la fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance, consultez [Comment utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../core/clients/manage/collections/use-maintenance-windows.md).  

Sous l'onglet **Durée maximale d'exécution** , vous pouvez afficher et configurer les paramètres suivants :  

- **Durée maximale d’exécution** : indique le nombre maximal de minutes dont dispose le processus d’installation de mises à jour logicielles avant que l’installation ne soit plus contrôlée par Configuration Manager. Ce paramètre permet également de déterminer s'il reste suffisamment de temps disponible pour installer la mise à jour avant la fin de la fenêtre de maintenance. Le paramètre par défaut est de 60 minutes pour les Service Packs. Pour les autres types de mises à jour logicielles, la valeur par défaut est 10 minutes si vous avez effectué une nouvelle installation de Configuration Manager version 1511 ou ultérieure, et 5 minutes si vous avez effectué une mise à niveau depuis une version précédente. La plage des valeurs est comprise entre 5 et 9999 minutes.  

> [!IMPORTANT]  
>  Veillez à affecter à la durée maximale d'exécution une valeur inférieure à la durée de la fenêtre de maintenance configurée. Sinon, l'installation des mises à jour logicielles n'est jamais lancée.  

####  <a name="BKMK_SetCustomSeverity"></a> Définir la gravité personnalisée  
Dans les propriétés d'une mise à jour logicielle, vous pouvez utiliser l'onglet **Gravité personnalisée** pour configurer des valeurs de gravité personnalisée pour les mises à jour logicielles. Cela peut s'avérer nécessaire si les valeurs de gravité prédéfinies ne répondent pas à vos besoins. Les valeurs personnalisées sont répertoriées dans la colonne **Gravité personnalisée** de la console Configuration Manager. Vous pouvez trier les mises à jour logicielles selon les valeurs de gravité personnalisée définies ou créer des requêtes et des rapports capables de filtrer ces valeurs. Vous pouvez configurer ce paramètre uniquement sur le site d'administration centrale ou le site principal autonome.  

Vous pouvez configurer les paramètres suivants sous l'onglet **Gravité personnalisée** .  

- **Gravité personnalisée**: définit une valeur de gravité personnalisée pour les mises à jour logicielles. Sélectionnez **Critique**, **Important**, **Modéré**ou **Faible** dans la liste. Par défaut, la valeur de la gravité personnalisée n'est pas renseignée.

## <a name="crl-checking-for-software-updates"></a>Vérification de la liste de révocation de certificats pour les mises à jour logicielles
Par défaut, la liste de révocation de certificats n’est pas contrôlée pendant la vérification de la signature des mises à jour logicielles System Center Configuration Manager. La vérification de la liste de révocation de certificats à chaque utilisation d'un certificat est une sécurité supplémentaire qui permet de ne pas utiliser de certificat révoqué. Toutefois, elle implique un délai de connexion et un traitement supplémentaire sur l'ordinateur qui l'effectue.  

Si vous l’utilisez, la vérification de la liste de révocation de certificats doit être activée sur les consoles Configuration Manager qui traitent les mises à jour logicielles.  

#### <a name="to-enable-crl-checking"></a>Pour activer la vérification de la liste de révocation de certificats  
Sur l’ordinateur effectuant la vérification de la liste de révocation de certificats, à partir du DVD du produit, exécutez la commande suivante à partir d’une invite de commandes : **\SMSSETUP\BIN\X64\\**<*langue*>**\UpdDwnldCfg.exe/checkrevocation**.  

Par exemple, pour l’anglais (US), exécutez **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**  
