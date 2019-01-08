---
title: Préversion UUP
titleSuffix: Configuration Manager
description: Instructions pour la préversion d’intégration UUP
ms.date: 12/21/2018
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: d2aac5945d4b7678acf78d215c557a34aaef9c72
ms.sourcegitcommit: f5fa9e657350ceb963a7928497d2adca9caef3d4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2018
ms.locfileid: "53748559"
---
# <a name="uup-private-preview-instructions"></a>Instructions de préversion privée UUP

> [!Note]  
> Ces informations concernent une fonctionnalité de préversion qui peut être sensiblement modifiée avant sa mise en production. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

## <a name="benefits"></a>Avantages

### <a name="feature-updates"></a>Mises à jour des fonctionnalités

Les mises à jour des fonctionnalités avec UUP sont conçues pour corriger plusieurs problèmes pour lesquels les clients demandent actuellement une maintenance. Essayez les mises à jour des fonctionnalités UUP, notamment :

- Mise à niveau directe vers le dernier niveau de conformité de sécurité. Vous n’avez plus besoin d’installer les mises à jour de sécurité immédiatement après la mise à niveau pour garantir la conformité. Chaque mois, une nouvelle mise à jour des fonctionnalités sera publiée pour inclure dernière mise à jour de sécurité cumulative. Vous n’aurez pas besoin de télécharger à nouveau ou de distribuer la majorité du contenu de mise à jour des fonctionnalités chaque mois, uniquement le composant de mise à jour de sécurité, qui est également partagé avec la mise à jour cumulative.

- Tous les FOD et modules linguistiques doivent être conservés et ne sont pas perdus pendant le processus de mise à niveau.

- Les mises à jour des fonctionnalités avec UUP prennent en charge les fichiers d’installation rapide, permettant ainsi aux clients de réduire la quantité de contenu que chaque client doit télécharger.

### <a name="cumulative-updates"></a>Mises à jour cumulatives

Les mises à jour cumulatives avec UUP permettent de distribuer hors connexion les FOD et modules linguistiques, permettant ainsi aux utilisateurs finaux de les obtenir à la demande sans accéder à Internet ni tâches fastidieuses de mise en lots pour les administrateurs.



## <a name="set-up-instructions"></a>Instructions de configuration

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1. Envoyer votre ID WSUS à votre contact préversion UUP chez Microsoft

Pour pouvoir participer à la préversion privée UUP, vous devez partager votre ID WSUS avec Microsoft afin que nous puissions mettre votre environnement sur liste verte dans la préversion. Sans cet ID, vous ne pourrez pas voir les mises à jour UUP tant que la préversion ne sera pas rendue publique.

Pour récupérer votre ID WSUS :

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId
```

### <a name="2-upgrade-configmgr-to-a-supported-version"></a>2. Mettre à niveau ConfigMgr vers une version prise en charge

Si vous synchronisez des fichiers d’installation rapide dans votre environnement, ConfigMgr 1810 (builds TAP, anneau Rapide ou GA acceptables) est requis pour les environnements de production, ou 1812 Technical Preview pour les environnements Technical Preview.

Si vous ne synchronisez pas des fichiers d’installation rapide dans votre environnement, le correctif logiciel ConfigMgr 1810 UUP au-dessus de 1810 GA est requis pour les environnements de production, ou 1812 Technical Preview pour les environnements Technical Preview.


#### <a name="configmgr-1810-uup-hotfix-kb4482615-from-1810-ga-slow-ring"></a>Correctif logiciel ConfigMgr 1810 (KB4482615) à partir de 1810 GA (anneau Lent)
Si vous utilisez actuellement ConfigMgr 1810 GA (anneau Lent), vous devez mettre à niveau ConfigMgr vers le correctif cumulatif UUP.

1. Appliquez la GUI du package « Correctif logiciel Configuration Manager 1810 (KB4482615) » (86450B7D-3574-4CF7-8B11-486A2C1F62A6) : ce correctif logiciel activera UUP pour les scénarios non express.  

    1. Télécharger le correctif logiciel Microsoft Download Center (le lien sera fourni une fois publié)  

    2. Après avoir téléchargé ce correctif logiciel, consultez la page web Microsoft Docs suivante pour obtenir des instructions d’installation : [Utiliser l’outil Inscription de la mise à jour pour importer des correctifs logiciels](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

    3. Pour obtenir des informations sur le télécharge des fichiers de support Microsoft, cliquez sur le numéro d’article suivant pour afficher l’article de la Base de connaissances Microsoft : [Comment obtenir des fichiers de support Microsoft à partir de services en ligne](https://support.microsoft.com/help/119591/how-to-obtain-microsoft-support-files-from-online-services)  

2. Une fois la mise à niveau vers le correctif logiciel UUP effectuée, mettez à niveau vos clients ConfigMgr pour faire correspondre. Tous les clients sur lesquels vous ciblez des mises à jour UUP doivent être mis à niveau pour éviter **un téléchargement inutile d’environ 6 Go** de contenu inutilisé sur le client.

#### <a name="configmgr-1810-uup-hotfix-kb4482615-from-1810-fast-ring"></a>Correctif logiciel ConfigMgr 1810 (KB4482615) à partir de 1810 anneau Rapide
Si vous utilisez actuellement ConfigMgr 1810 anneau Rapide, vous devrez alors mettre à niveau ConfigMgr avec deux mises à jour de maintenance mais retarder le déploiement des mises à niveau du client jusqu’à ce que vous ayez effectué les deux pour n’avoir à mettre à niveau les clients qu’une seule fois.

1. Un correctif de regroupement avec 1810 GA sera bientôt mis à votre disposition (début janvier). Différez jusqu’à ce que vous voyiez la mise à jour apparaître dans les mises à jour et la maintenance.  

2. Mise à niveau (serveurs de site uniquement, pas les clients) vers « Correctif logiciel Configuration Manager 1810 (KB4479288) » (GUID de package 930FA45E-530F-4B08-B1BF-DE3F5267B03C)  

3. Mettez à nouveau à niveau vers « Correctif logiciel Configuration Manager 1810 (KB4482615) » (GUID de package 86450B7D-3574-4CF7-8B11-486A2C1F62A6) : ce correctif logiciel activera UUP pour les scénarios non express.  

    1. Télécharger le correctif logiciel Microsoft Download Center (le lien sera fourni une fois publié)  

    2. Après avoir téléchargé ce correctif logiciel, consultez la page web Microsoft Docs suivante pour obtenir des instructions d’installation : [Utiliser l’outil Inscription de la mise à jour pour importer des correctifs logiciels](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

    3. Pour obtenir des informations sur le télécharge des fichiers de support Microsoft, cliquez sur le numéro d’article suivant pour afficher l’article de la Base de connaissances Microsoft : [Comment obtenir des fichiers de support Microsoft à partir de services en ligne](https://support.microsoft.com/help/119591/how-to-obtain-microsoft-support-files-from-online-services)  

4. Une fois la mise à niveau vers le correctif logiciel UUP effectuée, mettez à niveau vos clients ConfigMgr pour faire correspondre. Tous les clients sur lesquels vous ciblez des mises à jour UUP doivent être mis à niveau pour éviter **un téléchargement inutile d’environ 6 Go** de contenu inutilisé sur le client.

#### <a name="1812-technical-preview"></a>1812 Technical Preview 1812
1812 Technical Preview est équivalente dans les scénarios UUP pris en charge pour le correctif logiciel ConfigMgr 1810 UUP (KB4482615).

La seule différence réside dans le fait que cette mise à niveau de 1812 Technical Preview est cassée à partir du 1810.1 TP ou 1811 TP. Pour contourner ce problème, vous devrez désinstaller les clients 1810.1 TP et 1811 TP, puis installer proprement le client 1812 TP. Tous les clients sur lesquels vous ciblez des mises à jour UUP doivent se trouver sur 1812 Technical Preview (ou ultérieure) pour éviter **un téléchargement inutile d’environ 6 Go** de contenu inutilisé sur le client.


### <a name="3-update-windows-clients-to-supported-versions"></a>3. Mettre à niveau les clients Windows vers les versions prises en charge

#### <a name="for-express-installation-file-sync"></a>Pour la synchronisation de fichier d’installation express
Pour le contenu express, les versions Windows prises en charge incluent :

- **Windows 10 version 1709** avec [KB4338825](https://support.microsoft.com/help/4338825) (mise à jour de sécurité cumulative de juillet 2017) ou version ultérieure  

- **Windows 10 version 1803** avec [KB4284835](https://support.microsoft.com/help/4284835) (mise à jour de sécurité cumulative de juin 2017) ou version ultérieure  

- **Windows 10 version 1809** avec mise à jour non de sécurité cumulative de janvier à venir (ou la mise à jour de sécurité cumulative de février suivante) ou version ultérieure

#### <a name="for-non-express-installation-file-sync"></a>Pour la synchronisation de fichier d’installation non express
Pour le contenu non express, un correctif supplémentaire doit être appliqué. Ce chemin d’accès a été mis à disposition dans un format non cumulatif sur le catalogue 12/20 et sera disponible dans le format cumulatif normal fin janvier.

**Windows 10 version 1709** et **Windows 10 version 1803** avec :
- Décembre-Janvier : Les clients doivent avoir un niveau de mise à jour cumulative de base ainsi que la mise à jour non cumulative  
    - Mise à jour cumulative  
        - 1709 : [KB4338825](https://support.microsoft.com/help/4338825) (mise à jour de sécurité cumulative de juillet 2017) à la mise à jour cumulative de sécurité de janvier 2019, incluse  
        - 1803 : [KB4284835](https://support.microsoft.com/help/4284835) (mise à jour de sécurité cumulative de juin 2017) à la mise à jour de sécurité cumulative de janvier 2019, incluse  
    - Mise à jour non cumulative : Cette mise à jour est uniquement disponible dans le catalogue et ne se synchronise pas directement avec WSUS. Pour importer la mise à jour dans votre environnement afin de la déployer, consultez [Importer des mises à jour à partir du catalogue Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).  
        - 1709 : [KB4483530](https://support.microsoft.com/help/4483530)  
        - 1803 : [KB4483541](https://support.microsoft.com/help/4483541)  
- Février et ultérieurement : Pour la mise à jour cumulative, mise à jour non de sécurité cumulative de janvier à venir uniquement (ou la mise à jour de sécurité cumulative de février suivante) ou version ultérieure   

**Windows 10 version 1809** avec mise à jour non de sécurité cumulative de janvier à venir (ou la mise à jour de sécurité cumulative de février suivante) ou version ultérieure


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4. Activer l’installation express sur les clients dans les paramètres du client

Le paramètre du client pour activer l’installation express doit être défini pour les mises à jour UUP, que le contenu express soit synchronisé ou non. Ce paramètre configure ConfigMgr pour laisser le soin à WUA de déterminer le contenu nécessaire pour télécharger sur les clients, plutôt que ConfigMgr télécharge tout le contenu associé à la mise à jour UUP. Ce paramètre est requis même pour les scénarios non express en raison du contenu FOD et de module linguistique facultatif, ce qui entraîne une quantité non significative de données supplémentaire non requises par tous les clients associés à la mise à jour.

L’activation de ce paramètre n’affecte pas les téléchargements de contenu de serveur, uniquement les comportements de téléchargement du client. Il est important que vous disposiez des versions de client ConfigMgr et Windows ci-dessus avant d’activer ce paramètre si vous ne l’avez pas déjà activé, car ces versions résolvent certains problèmes de compatibilité grâce à l’approbation des mises à jour directement dans WSUS et configurent ConfigMgr pour utiliser ce canal pour les mises à jour UUP même si le contenu express n’est pas synchronisé.

Pour activer l’installation express sur les clients :

1. Dans la console Configuration Manager, accédez à **Administration** \ **Paramètres du client**  

2. Ouvrez les propriétés des paramètres du client que vous souhaitez utiliser ou créez-en une pour le déploiement si nécessaire.  

3. Sous le groupe **Mises à jour logicielles**, définissez **Activer l’installation de fichiers d’installation rapide sur les clients** sur **Oui**

![Mise en surbrillance de paramètre du client dans le groupe Mises à jour logicielles](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5. Assurez-vous que vos ADR sont définies comme vous le souhaitez 

Avant d’activer la synchronisation des mises à jour UUP, évaluez vos ADR et toute autre infrastructure de mise à jour appliquée. Si vous ne souhaitez pas que ces mises à jour soient automatiquement déployées dans le cadre de vos ADR et plans de maintenance existants, veillez à mettre à jour vos ADR pour les filtrer. Consultez [Comment rechercher des mises à jour UUP synchronisées](#how-to-find-synced-uup-updates). Par défaut, les plans de maintenance existants déploient des mises à jour non UUP uniquement, mais vous pouvez les mettre à jour pour modifier ce comportement.

Évaluez également si ces mises à jour affecteront vos rapports de conformité ou toute autre infrastructure simplement en les synchronisant, et apportez les modifications souhaitées à l’avance. Par exemple, si vous mesurez la conformité sur tous les produits, vous verrez maintenant la mise à jour Windows 10 cumulative UUP et non UUP comme non conforme ou conforme, faussant ainsi vos résultats.



## <a name="enable-uup-and-start-testing"></a>Activer UUP et démarrer le test

### <a name="select-products-and-classifications-to-sync"></a>Sélectionner les produits et classifications à synchroniser

Lorsque vous êtes prêt à commencer la synchronisation des mises à jour UUP, à essayer de les extraire, et que vous avez reçu une notification de Microsoft indiquant que nous avons activé votre WSUS pour voir le pilote, activez les nouveaux produits.

1. [Synchroniser les mises à jour logicielles](/sccm/sum/get-started/synchronize-software-updates) pour autoriser le renseignement des nouveaux produits  

2. Dans la console Configuration Manager, accédez à **Administration** \ **Configuration de site** \ **Sites**  

3. Sélectionnez votre site de niveau supérieur (CAS ou autonome principal)  

4. Ouvrez **Configurer les composants de site** \ **Point de mise à jour logicielle**  

5. Sur l’onglet **Produits**, lorsque votre serveur WSUS est ajouté à la préversion, deux nouveaux produits doivent apparaître. Ces produits contiennent le contenu UUP de préversion.  

    - **Windows 10 UUP pilote** : Mises à jour UUP de station de travail Windows  
    - **Windows Server 2016 UUP** : Mises à jour UUP de Windows Server  

6. Sur l’onglet **Classifications**, veillez à sélectionner :  

    - **Mises à jour de sécurité** : Pour afficher les mises à jour cumulatives UUP  
    - **Mises à niveau** : Pour afficher les mises à jour des fonctionnalités UUP  

7. Synchroniser les mises à jour logicielles pour afficher les nouvelles mises à jour UUP


### <a name="how-to-find-synced-uup-updates"></a>Comment rechercher les mises à jour UUP synchronisées

Lorsque vous avez synchronisé les mises à jour UUP dans votre environnement, vous souhaiterez les rechercher afin de les tester. Deux méthodes simples permettent de rechercher les mises à jour de préversion dans la console Configuration Manager.

- Étant donné que ces mises à jour de préversion se trouvent dans des produits distincts, vous pouvez toujours utiliser le produit pour filtrer ou rechercher ces mises à jour. Un filtre de produit a été ajouté aux plans de maintenance pour vous permettre de sélectionner si vous souhaitez déployer les mises à jour des fonctionnalités UUP ou non UUP.  

- Il existe une nouvelle colonne facultative, **Balise**, dans les nœuds **Toutes les mises à jour logicielles** et **Toutes les mises à jour Windows 10** de la bibliothèque de logiciels, ainsi qu’un filtre dans les ADR. Ce champ est défini sur **UUP** pour les mises à jour UUP et est vide pour les mises à jour non UUP.  


### <a name="updates-available-during-preview"></a>Mises à jour disponibles pendant la préversion

- Mises à jour cumulatives Windows 10 1709
    - Mise à jour de sécurité de décembre (12/11)
    - Mise à jour de sécurité de janvier (1/8)
    - Mise à jour non de sécurité de janvier (1/15)
    - Mise à jour de sécurité de février (2/12)  

- Mises à jour cumulatives Windows 10 1803
    - Mise à jour de sécurité de décembre (12/11)
    - Mise à jour de sécurité de janvier (1/8)
    - Mise à jour non de sécurité de janvier (1/15)
    - Mise à jour de sécurité de février (2/12)  

- Mises à jour cumulatives Windows 10 1809
    - Mise à jour de sécurité de février (2/12)  

- Mises à jour des fonctionnalités Windows 10 1803 (à partir de 1709 ou 1803)   
    - Conformité des mises à jour de sécurité de décembre (12/11)
    - Conformité des mises à jour de sécurité de janvier (1/8)
    - Conformité des mises à jour de sécurité de février (2/12)  

- Mises à jour des fonctionnalités Windows 10 1809 (à partir de 1709 ou 1803)
    - Conformité des mises à jour de sécurité de décembre (12/11)
    - Conformité des mises à jour de sécurité de janvier (1/8)
    - Conformité des mises à jour de sécurité de février (2/12)  

Si nécessaire, les mises à jour de sécurité et mars et ultérieures continueront à être publiées dans tous ces domaines tant que UUP est toujours en préversion (privée ou publique). Lorsque nous aurons terminé la préversion, seules les mises à jour cumulatives et des fonctionnalités Windows 10 Version 1809 (à partir de Windows 10 Version 1803) seront prises en charge en production.


### <a name="scenarios-to-try"></a>Scénarios à essayer

#### <a name="feature-updates"></a>Mises à jour des fonctionnalités
- Mise à niveau directe vers le niveau de conformité de sécurité de votre choix  

- Mise à niveau avec FOD et modules linguistiques installés avant la mise à niveau, ils sont conservés via la mise à niveau  

- Activez éventuellement la synchronisation des fichiers d’installation rapide pour les mises à niveau des fonctionnalités afin de réduire la quantité de contenu que chaque client doit télécharger.  

    > [!Note]  
    > Cet avantage client vient au détriment d’un téléchargement et d’une distribution serveur plus importants, comme c’est le cas pour les fichiers d’installation rapide pour les mises à jour cumulatives.  

#### <a name="cumulative-updates"></a>Mises à jour cumulatives
Pendant la préversion, assurez la conformité des à l’aide de la mise à jour du type UUP pour plusieurs mises à jour consécutives et ainsi avoir une idée des attentes.

#### <a name="content"></a>Content
La première mise à jour de chaque version majeure (1709, 1803, 1809), architecture et combinaison de langues semblera volumineuse, en nombre de fichiers et d’espace disque, par rapport à ce que vous pouviez voir dans les mises à jour non UUP précédentes. Ce contenu supplémentaire concerne principalement les FOD et modules linguistiques des mises à jour cumulatives. Pour les mises à jour des fonctionnalités, et notamment si le mode express est activé, le contenu supplémentaire est important pour cette première mise à jour. 

Toutefois, dans les mises à jour suivantes (mises à jour cumulatives et mises à jour des fonctionnalités mensuelles à des niveaux de conformité supérieurs), la quantité de nouveau contenu à télécharger et distribuer sera beaucoup plus réduite car le contenu de tous les FOD et modules linguistiques est partagé intelligemment entre les mises à jour plutôt que téléchargé à nouveau ou redistribué. Pendant la préversion, dans 1709 et 1803, ce téléchargement mensuel équivaudra approximativement à la taille des mises à jour cumulatives que vous rencontrez dans les scénarios non UUP. Toutefois, dans 1809, ceci s’améliore car le téléchargement incrémentiel de la mise à jour cumulative est beaucoup plus petit mois après mois. 

Lorsque vous examinez le contenu total téléchargé et distribué sur une période de 12 mois pour un scénario non express, 1803 sans UUP doit être équivalent approximativement à 1809 avec UUP. Ensuite, le contenu total téléchargé et distribué sur toute la durée de vie de la version dans 1809 avec UUP est inférieur. Pour le scénario express, le point de basculement est plus tôt comme pour 1809, le scénario express s’applique uniquement aux mises à jour des fonctionnalités, non aux mises à jour cumulatives, et le coût express du contenu serveur de grande taille ne s’applique ainsi qu’une seule fois par version plutôt que tous les mois.

#### <a name="supported-content-channels"></a>Canaux de contenu pris en charge
Pour la préversion, testez avec ce que vous utilisez dans vos environnements d’entreprise réels. UUP prendra en charge tous les canaux de contenu, notamment :
- Optimisation de la distribution de Windows
- Cache entre pairs Configuration Manager
- Windows BranchCache
- Déployer sans téléchargement sur le serveur (aucun package de déploiement) pour télécharger directement à partir de MU pour lequel, si vous l’utilisez, nous recommandons d’utiliser DO avec
- Autres fournisseurs de contenu tiers

Pour plus d’informations, consultez [Optimiser la distribution de Windows Update pour Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery).
