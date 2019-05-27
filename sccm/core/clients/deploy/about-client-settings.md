---
title: Paramètres du client
titleSuffix: Configuration Manager
description: Découvrir les paramètres par défaut et personnalisés pour contrôler les comportements du client
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3271c0fbd8673e33d7a7bf6a9c6da4b0ce978377
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66176788"
---
# <a name="about-client-settings-in-configuration-manager"></a>À propos des paramètres client dans Configuration Manager

*S’applique à : System Center Configuration Manager (current branch)*

Vous pouvez gérer tous les paramètres client dans la console Configuration Manager à partir du nœud **Paramètres client** de l’espace de travail **Administration**. Configuration Manager est fourni avec un ensemble de paramètres par défaut. Quand vous modifiez les paramètres client par défaut, ces paramètres sont appliqués à tous les clients de la hiérarchie. Vous pouvez également configurer des paramètres client personnalisés, qui remplacent les paramètres client par défaut lorsque vous les affectez à des regroupements. Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).

Les sections suivantes décrivent en détail les paramètres et les options.  


## <a name="background-intelligent-transfer-service-bits"></a>service de transfert intelligent en arrière-plan (BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>Limiter la bande passante réseau maximale pour les transferts BITS en arrière-plan

Quand cette option est **Oui**, les clients utilisent la limitation de bande passante BITS. Pour configurer les autres paramètres de ce groupe, vous devez activer ce paramètre.

### <a name="throttling-window-start-time"></a>Heure de début de la fenêtre de limitation

Spécifiez l’heure locale de début de la fenêtre de limitation BITS.  

### <a name="throttling-window-end-time"></a>Heure de fin de la fenêtre de limitation

Spécifiez l’heure locale de fin de la fenêtre de limitation BITS. Si l’heure de fin est égale à l’**heure de début de la fenêtre de limitation**, la limitation BITS est toujours activée.  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>Taux de transfert maximal dans la fenêtre de limitation (Kbit/s)

Spécifie le taux de transfert maximal que les clients peuvent utiliser pendant la fenêtre.  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>Autoriser les téléchargements BITS en dehors de la fenêtre de limitation

Permet aux clients d’utiliser des paramètres BITS distincts en dehors de la fenêtre spécifiée.  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>Taux de transfert maximal en dehors de la fenêtre de limitation (Kbit/s)

Spécifiez le taux de transfert maximal que les clients peuvent utiliser en dehors de la fenêtre de limitation BITS.  



## <a name="client-cache-settings"></a>Paramètres du cache du client

### <a name="configure-branchcache"></a>Configurer BranchCache

Configurez l’ordinateur client pour [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#branchcache). Pour autoriser la mise en cache BranchCache sur le client, définissez **Activer BranchCache** sur **Oui**.

- **Activer BranchCache** : Active BranchCache sur les ordinateurs clients.

- **Taille maximale du cache BranchCache (pourcentage du disque)**  : Pourcentage du disque que vous autorisez BranchCache à utiliser.

### <a name="configure-client-cache-size"></a>Configurer la taille du cache des clients

Le cache du client Configuration Manager sur les ordinateurs Windows stocke les fichiers temporaires utilisés pour installer des applications et des programmes. Si cette option est définie sur **Non**, la taille par défaut est de 5 120 Mo.

Si choisissez **Oui**, spécifiez :

- **Taille maximale du cache (Mo)**
- **Taille maximale du cache (pourcentage du disque)**  : La taille du cache du client augmente jusqu’à la taille maximale en mégaoctets (Mo) ou au pourcentage du disque, selon la valeur la moins élevée des deux.

### <a name="enable-configuration-manager-client-in-full-os-to-share-content"></a>Permettre au client Configuration Manager exécutant le système d'exploitation complet de partager du contenu

Active le [cache d’homologue](/sccm/core/plan-design/hierarchy/client-peer-cache) pour les clients Configuration Manager. Choisissez **Oui**, puis spécifiez le port par lequel le client communique avec l’ordinateur homologue.

- **Port pour la diffusion réseau initiale** (par défaut : 8004) : Configuration Manager utilise ce port dans Windows PE ou dans le système d’exploitation Windows complet. Le moteur de séquence de tâches dans Windows PE envoie la diffusion pour obtenir les emplacements du contenu avant de démarrer la séquence de tâches.<!--SCCMDocs issue 910-->

- **Port pour le téléchargement de contenu à partir d’un pair** (par défaut : 8003) : Configuration Manager configure automatiquement les règles de Pare-feu Windows pour autoriser ce trafic. Si vous utilisez un autre pare-feu, vous devez configurer manuellement des règles pour autoriser ce trafic.



## <a name="client-policy"></a>Stratégie du client  

### <a name="client-policy-polling-interval-minutes"></a>Intervalle d'interrogation de stratégie client (minutes)

Spécifie la fréquence à laquelle les clients Configuration Manager suivants téléchargent la stratégie client :

- Ordinateurs Windows (par exemple, ordinateurs de bureau, serveurs, ordinateurs portables)  
- Appareils mobiles inscrits par Configuration Manager  
- Ordinateurs Mac  
- Ordinateurs qui exécutent Linux ou UNIX  

Cette valeur est de 60 minutes par défaut. La réduction de cette valeur a pour effet que les clients interrogent le site plus fréquemment. Avec un grand nombre de clients, ce comportement peut avoir un impact négatif sur les performances du site. L’[aide sur la taille et l’échelle](/sccm/core/plan-design/configs/size-and-scale-numbers) est basée sur la valeur par défaut. L’augmentation de cette valeur a pour effet que les clients interrogent le site moins fréquemment. Toute modification apportée aux stratégies des clients, notamment les nouveaux déploiements, rend le téléchargement et le traitement plus longs pour les clients.<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>Activer la stratégie utilisateur sur les clients

Quand vous affectez la valeur **Oui** à cette option et que vous utilisez la [découverte d’utilisateurs](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser), les clients reçoivent les applications et programmes destinés à l’utilisateur connecté.  

Le catalogue d’applications reçoit la liste des logiciels disponibles pour les utilisateurs à partir du serveur de site. Par conséquent, ce paramètre ne doit pas obligatoirement être **Oui** pour que les utilisateurs voient et demandent des applications dans le catalogue d’applications. Si ce paramètre est défini sur **Non**, les utilisateurs ne peuvent pas installer les applications qu’ils voient dans le catalogue d’applications.  

De plus, si ce paramètre est défini sur **Non**, les utilisateurs ne reçoivent pas les applications exigées que vous déployez sur les utilisateurs. Ils ne reçoivent pas non plus d’autres tâches de gestion dans les stratégies utilisateur.  

Ce paramètre s’applique aux utilisateurs si leur ordinateur se trouve sur l’intranet ou Internet. Il doit avoir la valeur **Oui** si vous souhaitez également activer les stratégies utilisateur sur Internet.  

### <a name="enable-user-policy-requests-from-internet-clients"></a>Autoriser les demandes de stratégie utilisateur depuis des clients Internet

Définissez cette option sur **Oui** pour que les utilisateurs reçoivent la stratégie utilisateur sur les ordinateurs basés sur Internet. Les conditions suivantes s’appliquent également :  

- Le client et le site sont configurés pour la [gestion des clients Internet](/sccm/core/clients/manage/plan-internet-based-client-management) ou pour une [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Le paramètre **Activer la stratégie utilisateur sur les clients** est défini sur **Oui**.  

- Le point de gestion basé sur Internet authentifie correctement l’utilisateur à l’aide de l’authentification Windows (Kerberos ou NTLM). Pour plus d’informations, consultez [Éléments à prendre en considération pour les communications clients à partir d’Internet](/sccm/core/plan-design/hierarchy/communications-between-endpoints#BKMK_clientspan).  

- À compter de la version 1710, la passerelle de gestion cloud peut authentifier l’utilisateur avec Azure Active Directory. Pour plus d’informations, consultez [Déployer des applications disponibles pour l’utilisateur sur des appareils joints à Azure AD](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices).  

Si vous affectez la valeur **Non** à cette option, ou si l’une des conditions ci-dessus n’est pas remplie, un ordinateur sur Internet reçoit uniquement les stratégies ordinateur. Dans ce cas, les utilisateurs peuvent toujours voir, demander et installer des applications à partir d'un catalogue d'applications basé sur Internet. Si ce paramètre a la valeur **Non**, mais que **Activer la stratégie utilisateur sur les clients** a la valeur **Oui**, les utilisateurs ne reçoivent les stratégies utilisateur qu’une fois l’ordinateur connecté à l’intranet.  

> [!NOTE]  
> Pour la gestion des clients basée sur Internet, les demandes d’approbation d’applications des utilisateurs ne nécessitent pas de stratégies utilisateur ou d’authentification utilisateur. La passerelle de gestion cloud ne prend pas en charge les demandes d’approbation d’applications.  



## <a name="cloud-services"></a>Services cloud

### <a name="allow-access-to-cloud-distribution-point"></a>Autoriser l'accès au point de distribution cloud

Définissez cette option sur **Oui** pour que les clients obtiennent du contenu à partir d’un point de distribution cloud. Ce paramètre ne nécessite pas que l’appareil soit basé sur Internet.

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>Inscrire automatiquement les nouveaux appareils joints au domaine Windows 10 auprès d'Azure Active Directory

Quand vous configurez Azure Active Directory pour prendre en charge la jointure hybride, Configuration Manager configure les appareils Windows 10 pour cette fonctionnalité. Pour plus d’informations, consultez [Guide pratique pour configurer des appareils hybrides joints à Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup).

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>Autoriser les clients à utiliser une passerelle de gestion cloud

Par défaut, tous les clients Internet itinérants utilisent n’importe quelle [passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) disponible. Vous pouvez affecter la valeur **Non** à ce paramètre par exemple quand vous souhaitez limiter l’étendue du service, comme lors d’un projet pilote, ou pour réduire les coûts.



## <a name="compliance-settings"></a>Paramètres de conformité  

### <a name="enable-compliance-evaluation-on-clients"></a>Activer l'évaluation de compatibilité sur les clients

Définissez cette option sur **Oui** pour configurer les autres paramètres de ce groupe.

### <a name="schedule-compliance-evaluation"></a>Planifier l'évaluation de compatibilité

Sélectionnez **Planifier** pour créer le calendrier par défaut pour les déploiements de la base de référence de configuration. Cette valeur est configurable pour chaque ligne de base dans la boîte de dialogue **Déployer la ligne de base de la configuration**.  

### <a name="enable-user-data-and-profiles"></a>Activer les données et profils utilisateurs

Choisissez **Oui** si vous souhaitez déployer des éléments de configuration de [données et de profils utilisateur](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).



## <a name="computer-agent"></a>Agent ordinateur  

### <a name="user-notifications-for-required-deployments"></a>Notifications à l’utilisateur pour les déploiements obligatoires

Pour plus d’informations sur les trois paramètres suivants, consultez [Notifications à l’utilisateur pour les déploiements obligatoires](/sccm/apps/deploy-use/deploy-applications#user-notifications-for-required-deployments) :

- **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)**
- **Échéance du déploiement inférieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)**
- **Échéance du déploiement inférieure à 1 heure, effectuer un rappel à l’utilisateur toutes les (minutes)**

### <a name="default-application-catalog-website-point"></a>Point de site Web du catalogue d'applications par défaut

> [!Note]  
> À compter de la version 1806, le point du site Web du catalogue des applications n’est plus *requis*, mais il est toujours *pris en charge*. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).
>
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

Configuration Manager utilise ce paramètre pour connecter les utilisateurs au catalogue d’applications du Centre logiciel. Sélectionnez **Définir un site Web** pour spécifier un serveur qui héberge le point du site web du catalogue d’applications. Entrez son nom NetBIOS ou son nom de domaine complet, spécifiez la détection automatique, ou spécifiez une URL pour les déploiements personnalisés. Dans la plupart des cas, la détection automatique constitue le meilleur choix.

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>Ajoute un site Web du catalogue d'applications par défaut à la zone des sites de confiance d'Internet Explorer

> [!Note]  
> À compter de la version 1806, le point du site Web du catalogue des applications n’est plus *requis*, mais il est toujours *pris en charge*. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).
>
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

Si cette option a la valeur **Oui**, le client ajoute automatiquement l’URL actuelle du site web du catalogue d’applications par défaut à la zone des sites de confiance dans Internet Explorer.  

Ce paramètre garantit que le paramètre Internet Explorer en mode protégé n’est pas activé. Si le mode protégé est activé, le client Configuration Manager peut ne pas être en mesure d’installer des applications à partir du catalogue d’applications. Par défaut, la zone des sites de confiance prend également en charge l'ouverture de session utilisateur pour le catalogue d'applications, ce qui requiert l'authentification Windows.  

Si vous conservez la valeur **Non** pour cette option, les clients Configuration Manager risquent de ne pas pouvoir installer des applications à partir du catalogue d’applications. Une autre méthode consiste à configurer ces paramètres Internet Explorer dans une autre zone pour l’URL du catalogue d’applications utilisée par les clients.  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>Autoriser les applications Silverlight à s'exécuter en mode de confiance élevé

> [!Important]  
> À compter de Configuration Manager version 1802, le client n’installe pas automatiquement Silverlight.
>
> À compter de la version 1806, **l’expérience utilisateur Silverlight** pour le point du site Web du catalogue des applications n’est plus prise en charge. Les utilisateurs doivent utiliser le nouveau Centre logiciel. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).  

Ce paramètre doit être **Oui** pour que les utilisateurs utilisent le catalogue d’applications.  

Si vous modifiez ce paramètre, il prend effet au prochain chargement du navigateur par les utilisateurs ou lorsqu'ils actualisent la fenêtre du navigateur actuellement ouverte.  

Pour plus d’informations sur ce paramètre, consultez [Certificats pour Microsoft Silverlight 5 et mode de confiance élevée obligatoires pour le catalogue des applications](/sccm/apps/plan-design/security-and-privacy-for-application-management#BKMK_CertificatesSilverlight5).  

### <a name="organization-name-displayed-in-software-center"></a>Nom d'organisation affiché dans le Centre logiciel

Tapez le nom que les utilisateurs voient dans le Centre logiciel. Ces informations personnalisées aident les utilisateurs à identifier cette application comme une source approuvée. Pour plus d’informations sur la priorité de ce paramètre, consultez [Personnalisation du Centre logiciel](/sccm/apps/plan-design/plan-for-and-configure-application-management#branding-software-center).  

### <a name="use-new-software-center"></a>Utiliser le nouveau Centre logiciel

À compter de Configuration Manager 1802, la valeur par défaut est **Oui**.

Si vous sélectionnez **Oui** pour cette option, tous les ordinateurs clients utilisent le Centre logiciel. Le Centre logiciel répertorie les applications accessibles à l’utilisateur qui étaient auparavant uniquement disponibles dans le catalogue d’applications. Le catalogue d’applications nécessite Silverlight, qui n’est pas un prérequis pour le Centre logiciel.

À compter de la version 1806, les rôles de point du site Web et de point de service Web du catalogue des applications ne sont plus *requis*, mais ils sont toujours *pris en charge*. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).

> [!Note]  
> L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Pour plus d’informations, consultez [Fonctionnalités supprimées et déconseillées](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

### <a name="enable-communication-with-health-attestation-service"></a>Activer la communication avec le service d’attestation d’intégrité

Définissez cette option sur **Oui** pour que les appareils Windows 10 utilisent l’[attestation d’intégrité](/sccm/core/servers/manage/health-attestation). Quand vous activez ce paramètre, le paramètre suivant est également disponible pour la configuration.

### <a name="use-on-premises-health-attestation-service"></a>Utiliser le service d'attestation d'intégrité local

Définissez cette option sur **Oui** pour que les appareils utilisent un service local. Définissez ce paramètre sur **non** pour que les appareils utilisent le service cloud de Microsoft.  

### <a name="install-permissions"></a>Autorisations d'installation

> [!IMPORTANT]  
> Ce paramètre s'applique au catalogue des applications et au Centre logiciel. Ce paramètre n’a aucun effet quand les utilisateurs utilisent le portail d’entreprise.  

Configurez la manière dont les utilisateurs peuvent lancer l'installation des logiciels, des mises à jour logicielles et des séquences de tâches :  

- **Tous les utilisateurs** : les utilisateurs disposant de toutes les autorisations, sauf Invité.  

- **Administrateurs uniquement** : l’utilisateur doit être membre du groupe Administrateurs local.  

- **Administrateurs et utilisateurs principaux uniquement** : les utilisateurs doivent être membres du groupe Administrateurs local ou des utilisateurs principaux de l’ordinateur.  

- **Aucun utilisateur** : aucun utilisateur connecté à un ordinateur client ne peut lancer l’installation des logiciels, mises à jour logicielles et séquences de tâches. Les déploiements requis pour l’ordinateur sont toujours installés à la date d’échéance. Les utilisateurs ne peuvent pas lancer l’installation du logiciel à partir du catalogue d’applications ou du Centre logiciel.  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>Interrompre l'entrée du code confidentiel BitLocker au redémarrage

Si les ordinateurs exigent une entrée de code PIN BitLocker, cette option contourne la nécessité d’entrer un code PIN quand l’ordinateur redémarre après l’installation d’un logiciel.  

- **Toujours** : Configuration Manager suspend temporairement BitLocker après l’installation d’un logiciel nécessitant un redémarrage de l’ordinateur et qu’un redémarrage a été effectué. Ce paramètre s’applique uniquement à un redémarrage de l’ordinateur lancé par Configuration Manager. Il ne suspend pas l’obligation d’entrer le code PIN BitLocker quand l’utilisateur redémarre l’ordinateur. L’obligation d’entrer un code PIN BitLocker reprend après le démarrage de Windows.

- **Jamais** : Configuration Manager ne suspend pas BitLocker après avoir installé un logiciel qui nécessite un redémarrage. Dans ce cas, l’installation du logiciel ne peut être finalisée que lorsque l’utilisateur entre le code confidentiel pour terminer le processus de démarrage standard et charger Windows.

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>D’autres logiciels gèrent le déploiement d’applications et de mises à jour logicielles

Activez cette option uniquement si l'une des conditions suivantes s'applique :  

- Vous utilisez une solution de fabricant qui nécessite l'activation de ce paramètre.  

- Vous utilisez le kit de développement logiciel (SDK) Configuration Manager pour gérer les notifications d’agent client et l’installation d’applications et de mises à jour logicielles.  

> [!WARNING]  
> Si vous choisissez cette option quand aucune de ces conditions ne s’applique, le client n’installe pas les mises à jour logicielles et les applications exigées. Ce paramètre n’empêche pas les utilisateurs d’installer des applications à partir du catalogue d’applications, ou n’empêche pas l’installation de packages, de programmes et de séquences de tâches.  

### <a name="powershell-execution-policy"></a>Stratégie d'exécution de PowerShell

Configurez la façon dont les clients Configuration Manager peuvent exécuter des scripts Windows PowerShell. Vous pouvez utiliser ces scripts pour la détection dans les éléments de configuration de paramètres de conformité. Vous pouvez également envoyer les scripts dans un déploiement sous la forme d’un script standard.  

- **Ignorer** : le client Configuration Manager ignore la configuration Windows PowerShell sur l’ordinateur client afin que les scripts non signés puissent s’exécuter.  

- **Restreint** : le client Configuration Manager utilise la configuration PowerShell actuelle sur l’ordinateur client. Cette configuration détermine si les scripts non signés peuvent s’exécuter.  

- **Tous signés** : le client Configuration Manager exécute les scripts uniquement s’ils sont signés par un éditeur approuvé. Cette restriction s'applique indépendamment de la configuration PowerShell actuelle sur l'ordinateur client.  

Cette option nécessite au minimum la version 2.0 de Windows PowerShell. La valeur par défaut est **Toutes signées**.  

> [!TIP]  
> Si les scripts non signés ne parviennent pas à s’exécuter en raison de ce paramètre client, Configuration Manager signale cette erreur ainsi :  
>
> - L’espace de travail **Surveillance** dans la console affiche l’ID d’erreur d’état de déploiement **0x87D00327**. Il affiche également la description **Le script n’est pas signé**.  
> - Les rapports affichent le type d’erreur **Erreur de découverte**. Les rapports affichent ensuite le code d’erreur **0x87D00327** et la description **Le script n’est pas signé**, ou le code d’erreur  **0x87D00320** et la description **L’environnement d’exécution de scripts n’a pas encore été installé**. Exemple de rapport : **Détails des erreurs des éléments de configuration dans la ligne de base de configuration d’un composant**.  
> - Le fichier **DcmWmiProvider.log** affiche le message : **Le script n’est pas signé (Erreur : 87D00327; Source : CCM)** .  

### <a name="show-notifications-for-new-deployments"></a>Afficher les notifications de nouveaux déploiements

Choisissez **Oui** pour afficher une notification pour les déploiements disponibles moins d’une semaine. Ce message s’affiche à chaque démarrage de l’agent du client.

### <a name="disable-deadline-randomization"></a>Désactiver la randomisation des échéances

Quand la date limite est atteinte, ce paramètre détermine si le client utilise un délai d’activation pouvant aller jusqu’à deux heures pour installer les mises à jour logicielles requises. Par défaut, le délai d'activation est désactivé.  

Pour les scénarios d’infrastructure VDI (Virtual Desktop Infrastructure), ce délai aide à distribuer le traitement par le processeur et le transfert de données pour un ordinateur hôte doté de plusieurs machines virtuelles. Même si vous n’utilisez pas d’infrastructure VDI, si de nombreux clients installent les mêmes mises à jour en même temps, cela peut augmenter l’utilisation du processeur sur le serveur de site. Ce comportement peut également ralentir les points de distribution et réduire considérablement la bande passante réseau disponible.  

Si les clients doivent installer des mises à jour logicielles requises à l’échéance du déploiement sans délai, configurez ce paramètre sur **Oui**.

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)

Si vous souhaitez accorder aux utilisateurs plus de temps pour installer les déploiements de mises à jour logicielles ou d’applications obligatoires au-delà de l’échéance, définissez cette option sur **Oui**. Cette période de grâce est destinée au scénario dans lequel un ordinateur est hors tension pendant une durée prolongée et l’utilisateur doit installer de nombreux déploiements d’applications ou de mises à jour. Par exemple, ce paramètre est utile si un utilisateur rentre de congés et qu’il doit patienter longtemps pendant que le client installe les déploiements d’applications en retard.

Définissez une période de grâce comprise entre une et 120 heures. Utilisez ce paramètre conjointement avec la propriété de déploiement **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur**. Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).


## <a name="computer-restart"></a>Redémarrage de l’ordinateur

Les paramètres suivants doivent être inférieurs à la durée de la fenêtre de maintenance la plus courte appliquée à l’ordinateur :

- **Afficher une notification temporaire à l’utilisateur indiquant l’intervalle avant la fermeture de la session de l’utilisateur ou le redémarrage de l’ordinateur (minutes)**
- **Afficher une boîte de dialogue que l’utilisateur ne peut pas fermer, indiquant l’intervalle de compte à rebours avant la fermeture de la session de l’utilisateur ou le redémarrage de l’ordinateur (minutes)**

Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).

**Quand un déploiement nécessite un redémarrage, montrer une fenêtre de dialogue à l’utilisateur au lieu d’une notification toast**<!--3555947-->: À compter de la version 1902, la configuration de ce paramètre sur **Oui** rend l’expérience utilisateur plus intrusive. Ce paramètre s’applique à tous les déploiements d’applications, à toutes les séquences de tâches et à toutes les mises à jour logicielles. Pour plus d’informations, consultez [Planifier le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_impact).



## <a name="delivery-optimization"></a>Optimisation de la distribution

<!-- 1324696 -->
Les groupes de limites Configuration Manager permettent de définir et de réguler la distribution de contenu sur le réseau de l’entreprise et dans les agences. [L’Optimisation de la distribution de Windows](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) est une technologie cloud pair à pair de partage de contenu entre appareils Windows 10. À compter de la version 1802, configurez-la de façon à ce qu’elle utilise vos groupes de limites pour partager du contenu entre homologues.

> [!Note]
> L’Optimisation de la distribution n’est disponible que sur les clients Windows 10

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>Utiliser les groupes de limites Configuration Manager pour l’ID de groupe d’Optimisation de la distribution

Choisissez **Oui** pour appliquer l’identificateur de groupe de limites en tant qu’identificateur de groupe d’Optimisation de la distribution sur le client. Lorsque le client communique avec le service de cloud d’Optimisation de la distribution, il utilise cet identificateur pour localiser les pairs possédant le contenu souhaité.



## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> En plus des informations suivantes, vous pouvez trouver des détails sur l’utilisation des paramètres du client Endpoint Protection dans [Exemple de scénario : utilisation d’Endpoint Protection pour protéger des ordinateurs contre les programmes malveillants](/sccm/protect/deploy-use/scenarios-endpoint-protection).

### <a name="manage-endpoint-protection-client-on-client-computers"></a>Gérer le client Endpoint Protection sur les ordinateurs clients

Choisissez **Oui** si vous souhaitez gérer les clients Endpoint Protection et Windows Defender existants sur des ordinateurs de la hiérarchie.  

Choisissez cette option si vous avez déjà installé le client Endpoint Protection et que vous souhaitez le gérer avec Configuration Manager. Cette installation distincte inclut un processus sous forme de script utilisant un programme et un package ou une application Configuration Manager. À compter de Configuration Manager 1802, l’agent Endpoint Protection n’a pas besoin d’être installé sur les appareils Windows 10. L’option **Gérer le client Endpoint Protection sur les ordinateurs clients** doit néanmoins être activée sur ces ordinateurs. <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>Installer le client Endpoint Protection sur les ordinateurs clients

Choisissez **Oui** pour installer et activer le client Endpoint Protection sur les ordinateurs clients qui ne l’exécutent pas encore. À compter de Configuration Manager 1802, l’agent Endpoint Protection n’a pas besoin d’être installé sur les clients Windows 10.  

> [!NOTE]  
> Si le client Endpoint Protection est déjà installé, le fait de choisir la valeur **Non** ne le désinstalle pas. Pour désinstaller le client Endpoint Protection, affectez au paramètre client **Gérer le client Endpoint Protection sur les ordinateurs clients** la valeur **Non**. Ensuite, déployez un package et un programme pour désinstaller le client Endpoint Protection.  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>Autoriser l’installation du client Endpoint Protection et redémarrer en dehors des fenêtres de maintenance. Celles-ci doivent être d’une durée minimale de 30 minutes pour l’installation du client

Définissez cette option sur **Oui** pour remplacer les comportements d’installation par défaut avec des fenêtres de maintenance. Ce paramètre satisfait aux besoins de l’entreprise en ce qui concerne la priorité de la maintenance du système pour des raisons de sécurité.

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>Pour les appareils Windows Embedded avec des filtres d'écriture, valider l'installation du client Endpoint Protection (nécessite un redémarrage)

Choisissez **Oui** pour désactiver le filtre d’écriture sur l’appareil Windows Embedded et le redémarrer. Cette action valide l’installation sur l’appareil.  

Si vous choisissez **Non**, le client est installé sur une superposition temporaire qui est effacée lors du redémarrage de l’appareil. Dans ce cas, le client Endpoint Protection n’est entièrement installé que lorsqu’une autre installation valide les changements apportés à l’appareil. Il s’agit de la configuration par défaut.  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>Supprimer tout redémarrage d'ordinateur requis après l'installation du client Endpoint Protection

Choisissez **Oui** pour ignorer le redémarrage de l’ordinateur après l’installation du client Endpoint Protection.  

> [!IMPORTANT]  
> Si le client Endpoint Protection nécessite un redémarrage de l’ordinateur et que ce paramètre est **Non**, l’ordinateur redémarre quelle que soit la fenêtre de maintenance configurée.  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>Durée pendant laquelle les utilisateurs sont autorisés à différer un redémarrage nécessaire pour terminer l’installation de Endpoint Protection (heures)

Si un redémarrage est nécessaire après l’installation du client Endpoint Protection, ce paramètre spécifie le nombre d’heures duquel les utilisateurs sont autorisés à différer le redémarrage. Ce paramètre exige que le paramètre **Supprimer tout redémarrage d’ordinateur requis après l’installation du client Endpoint Protection** soit **Non**.  

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>Désactiver les autres sources (telles que Microsoft Windows Update, Microsoft Windows Server Update Services ou les partages UNC) pour la mise à jour initiale des définitions sur les ordinateurs clients

Choisissez **Oui** si vous souhaitez que Configuration Manager installe uniquement la mise à jour de définition initiale sur les ordinateurs clients. Ce paramètre peut s'avérer pratique pour éviter les connexions réseau inutiles et réduire la bande passante réseau pendant l'installation initiale de la mise à jour de définition.  



## <a name="enrollment"></a>Inscription

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>Intervalle d'interrogation pour clients hérités de périphériques mobiles

Sélectionnez **Déf. un interv.** pour spécifier la durée, en minutes ou heures, d’interrogation de la stratégie par les appareils mobiles hérités. Ces appareils incluent des plateformes telles que Windows CE, Mac OS X et Unix ou Linux.

### <a name="polling-interval-for-modern-devices-minutes"></a>Fréquence d'interrogation des appareils récents (minutes)

Entrez l’intervalle d’interrogation (en minutes) de la stratégie par les appareils récents. Ce paramètre concerne les appareils Windows 10 gérés par le biais de la gestion des appareils mobiles locale.

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac

Pour activer l’inscription basée sur l’utilisateur des appareils hérités, définissez cette option sur **Oui**, puis configurez le paramètre suivant :

- **Profil d’inscription** : Sélectionnez **Définir un profil** pour créer ou sélectionner un profil d’inscription. Pour plus d’informations, consultez [Configurer les paramètres client pour l’inscription](/sccm/core/clients/deploy/deploy-clients-to-macs#configure-client-settings-for-enrollment).

### <a name="allow-users-to-enroll-modern-devices"></a>Autoriser les utilisateurs à inscrire des appareils récents

Pour activer l’inscription basée sur l’utilisateur des appareils récents, définissez cette option sur **Oui**, puis configurez le paramètre suivant :

- **Profil d’inscription des appareils récents** : Sélectionnez **Définir un profil** pour créer ou sélectionner un profil d’inscription. Pour plus d’informations, consultez [Créer un profil d’inscription qui permet aux utilisateurs d’inscrire des appareils récents](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm#bkmk_createProf).



## <a name="hardware-inventory"></a>Inventaire matériel  

### <a name="enable-hardware-inventory-on-clients"></a>Activer l'inventaire matériel sur les clients

Par défaut, ce paramètre est défini sur **Oui**. Pour plus d’informations, consultez [Présentation de l’inventaire matériel](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).

### <a name="hardware-inventory-schedule"></a>Calendrier de l'inventaire matériel

Sélectionnez **Planifier** pour régler la fréquence à laquelle les clients exécutent le cycle d’inventaire matériel. Par défaut, ce cycle se produit tous les sept jours.

### <a name="maximum-random-delay-minutes"></a>Délai aléatoire maximal (minutes)

Spécifiez le nombre maximal de minutes pour la définition d’un délai aléatoire du cycle d’inventaire matériel par le client Configuration Manager, par rapport à la planification définie. Cette fonctionnalité de randomisation parmi tous les clients aide à équilibrer la charge d’inventaire sur le serveur de site. Vous pouvez spécifier une valeur comprise entre 0 et 480 minutes. Par défaut, cette valeur est définie sur 240 minutes (4 heures).

### <a name="maximum-custom-mif-file-size-kb"></a>Taille maximale du fichier MIF personnalisé (Ko)

Spécifiez la taille maximale, en kilo-octets (Ko), autorisée pour chaque fichier Management Information Format (MIF) personnalisé recueilli par le client lors d’un cycle d’inventaire matériel. L’agent d’inventaire matériel Configuration Manager ne traite pas les fichiers MIF personnalisés qui dépassent cette taille. Vous pouvez spécifier une taille comprise entre 1 et 5 120 Ko. Par défaut, cette valeur est définie à 250 Ko. Ce paramètre n’affecte pas la taille du fichier de données d’inventaire matériel standard.  

> [!NOTE]  
> Ce paramètre est disponible uniquement dans les paramètres client par défaut.  

### <a name="hardware-inventory-classes"></a>Classes d'inventaire matériel

Sélectionnez **Déf. classes** pour étendre les informations matérielles que vous recueillez auprès des clients sans modifier manuellement le fichier sms_def.mof. Pour plus d’informations, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).  

### <a name="collect-mif-files"></a>Collecter des fichiers MIF

Utilisez ce paramètre pour spécifier si vous souhaitez collecter des fichiers MIF à partir de clients Configuration Manager pendant l’inventaire matériel.  

Pour qu’un fichier MIF soit collecté par un inventaire matériel, il doit se trouver à l’emplacement approprié sur l’ordinateur client. Par défaut, les fichiers se trouvent aux chemins suivants :  

- Les **fichiers IDMIF** doivent être dans le dossier Windows\System32\CCM\Inventory\Idmif.

- Les **fichiers NOIDMIF** doivent être dans le dossier Windows\System32\CCM\Inventory\Noidmif.

> [!NOTE]  
> Ce paramètre est disponible uniquement dans les paramètres client par défaut.



## <a name="metered-internet-connections"></a>Connexions Internet facturées à l’usage  

Gérez la façon dont les ordinateurs Windows 8 et versions ultérieures utilisent des connexions Internet facturées à l’usage pour communiquer avec Configuration Manager. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

> [!NOTE]  
> Le paramètre client configuré n’est pas appliqué dans les cas suivants :  
>
> - Si l’ordinateur se trouve sur une connexion de données itinérante, le client Configuration Manager n’exécute aucune tâche nécessitant le transfert de données vers des sites Configuration Manager.  
> - Si les propriétés de la connexion réseau Windows sont configurées pour une connexion non facturée à l’usage, le client Configuration Manager se comporte comme si la connexion n’était pas facturée à l’usage, et transfère donc les données vers le site.  

### <a name="client-communication-on-metered-internet-connections"></a>Communication des clients sur des connexions Internet facturées à l’usage

Choisissez l’une des options suivantes pour ce paramètre :  

- **Autoriser** : toutes les communications client sont autorisées via la connexion Internet facturée à l’usage, sauf si l’appareil client utilise une connexion de données itinérante.  

- **Limiter** : seules les communications client suivantes sont autorisées via la connexion Internet facturée à l’usage :  

    - Récupération de stratégie client  

    - Messages d'état du client à envoyer au site  

    - Demandes d'installation de logiciels à l'aide du catalogue des applications  

    - Déploiements requis (lorsque la date limite d'installation est atteinte)  

    > [!IMPORTANT]  
    > Le client autorise toujours les installations de logiciels à partir du Centre logiciel ou du catalogue des applications, quels que soient les paramètres de la connexion Internet facturée à l’usage.  

    Si le client atteint la limite de transfert de données pour la connexion Internet facturée à l’usage, le client n’essaie plus de communiquer avec les sites Configuration Manager.  

- **Bloquer** : le client Configuration Manager n’essaie pas de communiquer avec les sites Configuration Manager quand il se trouve sur une connexion Internet limitée. Il s’agit de l’option par défaut.  



## <a name="power-management"></a>Gestion de l'alimentation  

### <a name="allow-power-management-of-devices"></a>Autoriser la gestion de l'alimentation des périphériques

Définissez cette option sur **Oui** pour activer la gestion de l’alimentation sur les clients. Pour plus d’informations, consultez [Présentation de la gestion de l’alimentation](/sccm/core/clients/manage/power/introduction-to-power-management).

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>Autoriser les utilisateurs à exclure leur appareil de la gestion de l'alimentation

Choisissez **Oui** pour permettre aux utilisateurs du Centre logiciel d’exclure leur ordinateur des paramètres de gestion de l’alimentation configurés.  

### <a name="allow-network-wake-up"></a>Autoriser la sortie de veille du réseau

Ajouté dans la version 1810. Quand elle est définie sur **Activer**, configure les paramètres d’alimentation sur la carte réseau pour autoriser la carte réseau à sortir de veille l’appareil. Quand elle est définie sur **Désactiver**, les paramètres d’alimentation sur la carte réseau sont configurés pour ne pas autoriser la carte réseau à sortir de veille l’appareil.

### <a name="enable-wake-up-proxy"></a>Autoriser le proxy de mise en éveil

Spécifiez **Oui** pour compléter le paramètre Wake On LAN du site quand il est configuré pour les paquets de monodiffusion.  

Pour plus d’informations sur le proxy de mise en éveil, consultez [Planifier le mode de sortie de veille des clients](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

> [!WARNING]  
> N’activez pas le proxy de mise en éveil dans un réseau de production sans d’abord comprendre comment il fonctionne et l’évaluer dans un environnement de test.  

Ensuite, configurez les paramètres supplémentaires suivants en fonction des besoins :

- **Numéro de port du proxy de mise en éveil (UDP)** : Numéro du port utilisé par les clients pour envoyer des paquets de réveil aux ordinateurs en état de veille. Conservez le port par défaut 25536 ou remplacez-le par le numéro de votre choix.  

- **Numéro de port Wake On LAN (UDP)** : Conservez la valeur par défaut (9), sauf si vous avez modifié le numéro du port Wake On LAN (UDP) sous l’onglet **Ports** des **Propriétés** du site.  

    > [!IMPORTANT]  
    > Ce numéro doit correspondre au numéro figurant dans les **Propriétés**du site. Si vous modifiez ce numéro dans un seul emplacement, sachez qu’il n’est pas actualisé automatiquement dans l’autre emplacement.  

- **Exception du pare-feu Windows Defender pour le proxy de mise en éveil** : Le client Configuration Manager configure automatiquement le numéro de port du proxy de mise en éveil sur les appareils qui exécutent le Pare-feu Windows Defender. Sélectionnez **Configurer** pour spécifier les profils de pare-feu souhaités.  

    Si les clients exécutent un autre pare-feu, configurez-le manuellement pour autoriser le **Numéro de port du proxy de mise en éveil (UDP)** .  

- **Préfixes IPv6 si nécessaires pour DirectAccess ou d’autres périphériques réseau intervenants. Spécifiez plusieurs entrées en utilisant une virgule** : Entrez les préfixes IPv6 nécessaires pour que le proxy de mise en éveil fonctionne sur votre réseau.



## <a name="remote-tools"></a>outils de contrôle à distance.  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>Activer le contrôle à distance sur des clients et Profils d'exception de pare-feu

Sélectionnez **Configurer** pour activer la fonctionnalité de contrôle à distance de Configuration Manager. Vous pouvez éventuellement configurer les paramètres du pare-feu pour autoriser le contrôle à distance sur des ordinateurs clients.  

Le contrôle à distance est désactivé par défaut.  

> [!IMPORTANT]  
> Si vous ne configurez pas de paramètres de pare-feu, le contrôle à distance risque de ne pas fonctionner correctement.  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>Les utilisateurs peuvent modifier les paramètres de stratégie ou de notification dans le Centre logiciel

Indiquez si les utilisateurs peuvent modifier les options de contrôle à distance à partir du Centre logiciel.  

### <a name="allow-remote-control-of-an-unattended-computer"></a>Autoriser le contrôle à distance d'un ordinateur autonome

Indiquez si un administrateur peut utiliser le contrôle à distance pour accéder à un ordinateur client qui est déconnecté ou verrouillé. Seul un ordinateur connecté et déverrouillé peut être contrôlé à distance quand ce paramètre est désactivé.  

### <a name="prompt-user-for-remote-control-permission"></a>Inviter l'utilisateur à autoriser le contrôle à distance

Choisissez si l’ordinateur client affiche un message demandant l’autorisation de l’utilisateur avant d’autoriser une session de contrôle à distance.  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>Demander à l'utilisateur l'autorisation de transférer le contenu du Presse-papiers partagé

Avant de transférer le contenu du Presse-papiers partagé dans une session de contrôle à distance, donnez à vos utilisateurs la possibilité d’accepter ou de refuser des transferts de fichiers. Les utilisateurs n’ont besoin d’accorder l’autorisation qu’une seule fois par session. L’observateur ne peut pas s’accorder à lui-même l’autorisation de transférer le fichier.

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>Accorder l'autorisation de contrôle à distance au groupe Administrateurs local

Indiquez si les administrateurs locaux sur le serveur qui lance la connexion de contrôle à distance peuvent établir des sessions de contrôle à distance vers des ordinateurs client.  

### <a name="access-level-allowed"></a>Niveau d'accès autorisé

Spécifiez le niveau d’accès de contrôle à distance à accorder. Choisissez parmi les paramètres suivants :  

- **Aucun accès**
- **Afficher uniquement**
- **Contrôle intégral**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>Observateurs autorisés des options de contrôle à distance et d'assistance à distance

Sélectionnez **Définir des observateurs** pour spécifier les noms des utilisateurs Windows qui peuvent établir des sessions de contrôle à distance vers des ordinateurs clients.  

### <a name="show-session-notification-icon-on-taskbar"></a>Afficher l'icône de notification de session sur la barre des tâches

Configurez ce paramètre sur **Oui** pour afficher une icône dans la barre des tâches de Windows du client quand une session de contrôle à distance est en cours.  

### <a name="show-session-connection-bar"></a>Afficher la barre de connexion de session

Définissez cette option sur **Oui** pour afficher une barre de connexion de session très visible sur les clients, pour indiquer qu’une session de contrôle à distance est en cours.  

### <a name="play-a-sound-on-client"></a>Émettre un signal sonore sur le client

Définissez cette option afin d’utiliser le son pour indiquer qu’une session de contrôle à distance est active sur un ordinateur client. Sélectionnez l'une des options suivantes :

- **Aucun signal sonore**
- **Début et fin de session** (par défaut)
- **Fréquemment au cours d’une session**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>Gérer les paramètres de l'Assistance à distance non sollicités

Configurez ce paramètre sur **Oui** pour autoriser Configuration Manager à gérer les sessions d’assistance à distance non sollicitées.  

Dans une session d’Assistance à distance non sollicitée, l’utilisateur de l’ordinateur client n’a pas demandé d’assistance pour lancer la session.  

### <a name="manage-solicited-remote-assistance-settings"></a>Gérer les paramètres de l'Assistance à distance sollicités

Définissez cette option sur **Oui** pour autoriser Configuration Manager à gérer les sessions d’Assistance à distance sollicitées.  

Dans une session d’assistance à distance sollicitée, l’utilisateur de l’ordinateur client envoie une demande d’assistance à distance à l’administrateur.  

### <a name="level-of-access-for-remote-assistance"></a>Niveau d'accès de l'Assistance à distance

Choisissez le niveau d’accès à attribuer aux sessions d’assistance à distance lancées à partir de la console Configuration Manager. Sélectionnez l'une des options suivantes :

- **Aucun** (par défaut)
- **Affichage à distance**
- **Contrôle intégral**

> [!NOTE]  
> L'utilisateur de l'ordinateur client doit toujours autoriser l'ouverture d'une session d'assistance à distance.  

### <a name="manage-remote-desktop-settings"></a>Gérer les paramètres du Bureau à distance

Définissez cette option sur **Oui** pour autoriser Configuration Manager à gérer les sessions Bureau à distance des ordinateurs.  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>Autoriser la connexion des observateurs autorisés à l'aide d'une connexion Bureau à distance

Définissez cette option sur **Oui** pour ajouter les utilisateurs spécifiés dans la liste des observateurs autorisés au groupe d’utilisateurs locaux du Bureau à distance sur les clients.  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>Exiger l'authentification au niveau du réseau sur les ordinateurs exécutant le système d'exploitation Windows Vista et versions ultérieures

Définissez cette option sur **Oui** pour utiliser l’authentification au niveau du réseau afin d’établir des connexions Bureau à distance aux ordinateurs clients. L’authentification au niveau du réseau nécessite moins de ressources d’ordinateur distant, car l’authentification des utilisateurs se termine avant l’établissement de la connexion Bureau à distance. L’authentification au niveau du réseau est une configuration plus sécurisée. Elle contribue à protéger l’ordinateur des utilisateurs ou logiciels malveillants, et réduit le risque d’attaque par déni de service.  



## <a name="software-center"></a>Centre logiciel

### <a name="select-these-new-settings-to-specify-company-information"></a>Sélectionnez ces nouveaux paramètres pour spécifier des informations sur l'entreprise

Définissez cette option sur **Oui**, puis spécifiez les paramètres suivants pour personnaliser le Centre logiciel et l’adapter à votre organisation :

- **Nom de la société** : Entrez le nom d’organisation visible par les utilisateurs dans le Centre logiciel.  

- **Modèle de couleurs pour le Centre logiciel** : Choisissez **Sélectionner une couleur** pour définir la couleur principale utilisée par le Centre logiciel.  

- **Sélectionner un logo pour le Centre logiciel** : Choisissez **Parcourir** pour sélectionner une image à afficher dans le Centre logiciel. Le logo doit être de type JPEG, PNG ou BMP et au format 400 x 100 pixels, avec une taille maximale de 750 Ko. Le nom de fichier du logo ne doit pas contenir d’espace.  

### <a name="bkmk_HideUnapproved"></a> Masquer les applications non approuvées dans le Centre logiciel

À compter de Configuration Manager version 1802, quand vous activez cette option, les applications disponibles pour l’utilisateur qui nécessitent une approbation sont masquées dans le Centre logiciel.<!--1355146-->

### <a name="bkmk_HideInstalled"></a> Masquer les applications installées dans le Centre logiciel

À compter de Configuration Manager version 1802, quand vous activez cette option, les applications qui sont déjà installées ne s’affichent plus sous l’onglet Applications. Cette option est définie par défaut quand vous installez ou mettez à niveau vers Configuration Manager 1802. Les applications installées sont toujours disponibles pour examen sous l’onglet de l’état d’installation. <!--1357592-->

### <a name="bkmk_HideAppCat"></a> Masquer le lien du catalogue d’applications dans le Centre logiciel

À compter de Configuration Manager version 1806, vous pouvez spécifier la visibilité du lien du site web du catalogue d’applications dans le Centre logiciel. Quand cette option est définie, les utilisateurs ne voient pas le lien du site web du catalogue d’applications dans le nœud d’état d’installation du Centre logiciel. <!--1358214-->


### <a name="software-center-tab-visibility"></a>Visibilité de l’onglet Centre logiciel

Affectez la valeur **Oui** aux paramètres supplémentaires de ce groupe pour afficher les onglets suivants dans le Centre logiciel :

- **Applications**
- **Mises à jour**
- **Systèmes d’exploitation**
- **État de l’installation**
- **Conformité de l’appareil**
- **Options**
- **Spécifier un onglet personnalisé pour le Centre logiciel** (à compter de la version 1806) <!--1358132-->
    - **Nom de l’onglet**
    - **URL du contenu**

    >[!Important]  
    > Certaines fonctionnalités de site web peuvent ne pas fonctionner quand vous l’utilisez comme onglet personnalisé dans le Centre logiciel. Veillez à tester les résultats avant de le déployer sur des clients. <!--519659-->
    >
    > Ne spécifiez que des adresses de site web intranet ou de confiance lorsque vous ajoutez un onglet personnalisé.<!--SCCMDocs issue 1575-->

Par exemple, si votre organisation n’utilise pas de stratégies de conformité et que vous souhaitez masquer l’onglet Conformité de l’appareil dans le Centre logiciel, définissez l’onglet **Activer l’onglet Conformité de l’appareil** sur **Non**.



## <a name="software-deployment"></a>Déploiement logiciel  

### <a name="schedule-re-evaluation-for-deployments"></a>Planifier la réévaluation des déploiements

Configurez une planification pour la réévaluation des règles de spécifications par Configuration Manager pour tous les déploiements. La valeur par défaut est tous les sept jours.  

> [!IMPORTANT]  
> Ce paramètre est plus invasif sur le client local que sur le serveur réseau ou de site. Une planification de réévaluation plus agressive affecte négativement les performances de votre réseau et des ordinateurs clients. Microsoft déconseille de définir une valeur inférieure à la valeur par défaut. Si vous changez cette valeur, supervisez attentivement les performances.  

Lancez cette action à partir du client en procédant comme suit : dans le panneau de configuration de **Configuration Manager**, dans l’onglet **Actions**, sélectionnez **Cycle d’évaluation du déploiement de l’application**.  



## <a name="software-inventory"></a>Inventaire logiciel  

### <a name="enable-software-inventory-on-clients"></a>Activer l’inventaire logiciel sur les clients

Cette option est définie sur **Oui** par défaut. Pour plus d’informations, consultez [Présentation de l’inventaire logiciel](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

### <a name="schedule-software-inventory-and-file-collection"></a>Planifier l'inventaire logiciel et le regroupement de fichiers

Sélectionnez **Planifier** pour régler la fréquence à laquelle les clients exécutent les cycles de regroupement de fichiers et d’inventaire logiciel. Par défaut, ce cycle se produit tous les sept jours.

### <a name="inventory-reporting-detail"></a>Détails sur le rapport d'inventaire

Spécifiez l’un des niveaux d’informations de fichiers suivants à inventorier :

- **Fichier uniquement**
- **Produit uniquement**
- **Détails complets** (par défaut)

### <a name="inventory-these-file-types"></a>Inventorier ces types de fichiers

Si vous souhaitez spécifier les types de fichiers à inventorier, sélectionnez **Définir des types**, puis configurez les options suivantes :  

> [!NOTE]  
> Si plusieurs paramètres clients personnalisés sont appliqués à un ordinateur, l’inventaire retourné par chaque paramètre est fusionné.  

- Sélectionnez **Nouveau** pour ajouter un nouveau type de fichier à l’inventaire. Ensuite, spécifiez les informations suivantes dans la boîte de dialogue **Propriétés du fichier inventorié** :  

    - **Nom** : définissez le nom du fichier à inventorier. Utilisez un astérisque (`*`) comme caractère générique pour représenter une chaîne de texte et un point d’interrogation (`?`) pour représenter n’importe quel caractère. Par exemple, si vous voulez inventorier tous les fichiers portant l’extension .doc, spécifiez le nom de fichier `*.doc`.  

    - **Emplacement** : sélectionnez **Définir** pour ouvrir la boîte de dialogue **Propriétés du chemin d’accès**. Configurez l’inventaire logiciel pour rechercher le fichier spécifié sur tous les disques durs des clients, pour effectuer une recherche à un emplacement spécifié (par exemple `C:\Folder`) ou pour rechercher une variable spécifiée (par exemple `%windir%`). Vous pouvez également exécuter une recherche dans tous les sous-dossiers du chemin indiqué.  

    - **Exclure les fichiers chiffrés et compressés** : quand vous choisissez cette option, tous les fichiers compressés ou chiffrés ne sont pas inventoriés.  

    - **Exclure des fichiers dans le dossier Windows** : quand vous choisissez cette option, tout fichier présent dans le dossier Windows et ses sous-répertoires n’est pas inventorié.  

    Sélectionnez **OK** pour fermer la boîte de dialogue **Propriétés du fichier inventorié**. Ajoutez tous les fichiers à inventorier, puis sélectionnez **OK** pour fermer la boîte de dialogue **Configurer le paramètre client**.  

### <a name="collect-files"></a>Collecter des fichiers

Si vous souhaitez collecter des fichiers stockés à partir d’ordinateurs clients, sélectionnez **Définir des fichiers**, puis configurez les paramètres suivants :  

> [!NOTE]  
> Si plusieurs paramètres clients personnalisés sont appliqués à un ordinateur, l’inventaire retourné par chaque paramètre est fusionné.  

- Dans la boîte de dialogue **Configurer le paramètre client**, sélectionnez **Nouveau** pour ajouter un fichier à collecter.  

- Dans la boîte de dialogue **Propriétés du fichier collecté** , fournissez les informations suivantes :  

    - **Nom** : définissez le nom du fichier à collecter. Utilisez un astérisque (`*`) comme caractère générique pour représenter une chaîne de texte et un point d’interrogation (`?`) pour représenter n’importe quel caractère.  

    - **Emplacement** : sélectionnez **Définir** pour ouvrir la boîte de dialogue **Propriétés du chemin d’accès**. Configurez l’inventaire logiciel pour rechercher le fichier à collecter sur tous les disques durs des clients, pour effectuer une recherche à un emplacement spécifié (par exemple `C:\Folder`) ou pour rechercher une variable spécifiée (par exemple `%windir%`). Vous pouvez également exécuter une recherche dans tous les sous-dossiers du chemin indiqué.  

    - **Exclure les fichiers chiffrés et compressés** : quand vous choisissez cette option, tout fichier compressé ou chiffré n’est pas collecté.  

    - **Arrêter le regroupement de fichiers lorsque la taille totale dépasse (Ko)** : spécifiez la taille des fichiers, en kilo-octets (Ko), au-delà de laquelle le client arrête le regroupement des fichiers spécifiés.  

    > [!NOTE]  
    > Le serveur de site collecte les cinq dernières versions changées des fichiers collectés et les stocke dans le répertoire `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol`. Si un fichier n’a pas changé depuis le dernier cycle d’inventaire logiciel, le fichier n’est pas recollecté.  
    >
    > L’inventaire logiciel ne collecte pas les fichiers de plus de 20 Mo.  
    >
    > La valeur **Taille maximale pour tous les fichiers regroupés (Ko)** dans la boîte de dialogue **Configurer le paramètre client** indique la taille maximale de tous les fichiers collectés. Quand cette taille est atteinte, la collecte de fichiers s’arrête. Tous les fichiers déjà regroupés sont conservés et envoyés au serveur de site.  

    > [!IMPORTANT]
    > Si vous configurez l’inventaire logiciel pour collecter un grand nombre de fichiers volumineux, vous risquez d’affecter négativement les performances du serveur de site et du réseau.  

    Pour plus d’informations sur l’affichage des fichiers collectés, consultez [Guide pratique pour utiliser l’Explorateur de ressources pour afficher l’inventaire logiciel](/sccm/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory).  

    Sélectionnez **OK** pour fermer la boîte de dialogue **Propriétés du fichier collecté**. Ajoutez tous les fichiers à collecter, puis sélectionnez **OK** pour fermer la boîte de dialogue **Configurer le paramètre client**.  

### <a name="set-names"></a>Définir des noms

L’agent d’inventaire logiciel récupère le nom du fabricant et du produit à partir des informations d’en-tête de fichier. Ces noms ne sont pas systématiquement normalisés dans les informations d’en-tête de fichier. Quand vous affichez l’inventaire logiciel dans l’Explorateur de ressources, des versions différentes du même nom de fabricant ou de produit peuvent apparaître. Pour normaliser ces noms complets, sélectionnez **Définir des noms**, puis configurez les paramètres suivants :  

- **Type de nom** : l’inventaire logiciel recueille des informations sur les produits et les fabricants. Choisissez si vous souhaitez configurer des noms complets pour un **Fabricant** ou un **Produit**.  

- **Nom complet** : spécifiez le nom complet que vous souhaitez utiliser à la place des noms dans la liste **Noms inventoriés**. Sélectionnez **Nouveau** pour spécifier un nouveau nom complet.  

- **Noms inventoriés** : sélectionnez **Nouveau** pour ajouter un nom inventorié. Ce nom est remplacé dans l’inventaire logiciel par le nom choisi dans la liste **Nom complet**. Vous pouvez ajouter plusieurs noms à remplacer.  



## <a name="software-metering"></a>Contrôle de logiciel

### <a name="enable-software-metering-on-clients"></a>Activer le contrôle de logiciel sur les clients

Par défaut, ce paramètre est défini sur **Oui**. Pour plus d’informations, consultez [Contrôle de logiciel](/sccm/apps/deploy-use/monitor-app-usage-with-software-metering#configure-software-metering).

### <a name="schedule-data-collection"></a>Planifier le regroupement de données

Sélectionnez **Planifier** pour régler la fréquence à laquelle les clients exécutent le cycle de contrôle de logiciel. Par défaut, ce cycle se produit tous les sept jours.



## <a name="software-updates"></a>Mises à jour logicielles  

### <a name="enable-software-updates-on-clients"></a>Activer les mises à jour logicielles sur les clients

Utilisez ce paramètre pour activer les mises à jour logicielles sur les clients Configuration Manager. Quand vous désactivez ce paramètre, Configuration Manager supprime les stratégies de déploiement existantes des clients. Lorsque vous réactivez ce paramètre, le client télécharge la stratégie de déploiement actuelle.  

> [!IMPORTANT]  
> Quand vous désactivez ce paramètre, les stratégies de conformité qui reposent sur les mises à jour logicielles ne fonctionnent plus.  

### <a name="software-update-scan-schedule"></a>Calendrier d'analyse des mises à jour logicielles

Sélectionnez **Planifier** pour spécifier la fréquence à laquelle le client lance une analyse de la conformité. Cette analyse détermine l’état des mises à jour logicielles sur le client (par exemple, requise ou installée). Pour plus d’informations sur l’évaluation de la conformité, consultez [Évaluation de la conformité des mises à jour logicielles](/sccm/sum/understand/software-updates-introduction#BKMK_SUMCompliance).  

Par défaut, cette analyse utilise un calendrier simple pour une exécution tous les sept jours. Vous pouvez créer une planification personnalisée. Vous pouvez spécifier une date et une heure exactes de début, utiliser le temps universel coordonné (UTC) ou l’heure locale, et configurer l’intervalle de récurrence pour un jour spécifique de la semaine.  

> [!NOTE]  
> Si vous spécifiez un intervalle inférieur à une journée, Configuration Manager rétablit automatiquement la valeur par défaut (une journée).  

> [!WARNING]  
> L’heure de début réelle sur les ordinateurs clients est l’heure de début plus une durée aléatoire de deux heures maximum. Cette fonctionnalité de randomisation empêche les ordinateurs clients de lancer l’analyse et de se connecter simultanément au point de mise à jour logicielle actif.  

### <a name="schedule-deployment-re-evaluation"></a>Planifier la réévaluation du déploiement

Sélectionnez **Planifier** pour configurer la fréquence à laquelle l’agent client des mises à jour logicielles réévalue les mises à jour logicielles pour en déterminer l’état de l’installation sur les ordinateurs clients Configuration Manager. Quand des mises à jour logicielles préalablement installées ne sont plus disponibles sur les clients, mais sont toujours requises, le client réinstalle les mises à jour logicielles.

Ajustez cette planification en fonction de la stratégie de l’entreprise relative à la conformité des mises à jour logicielles et du droit des utilisateurs à désinstaller des mises à jour logicielles. Chaque cycle de réévaluation du déploiement provoque une activité processeur sur l’ordinateur client et le réseau. Par défaut, ce paramètre utilise un calendrier simple pour lancer l’analyse de réévaluation du déploiement tous les sept jours.  

> [!NOTE]  
> Si vous spécifiez un intervalle inférieur à une journée, Configuration Manager rétablit automatiquement la valeur par défaut (une journée).  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>Dès que l'échéance d'un déploiement de mise à jour logicielle est atteinte, installer tous les autres déploiements de mise à jour logicielle avec une échéance pendant une période de temps spécifiée

Définissez cette option sur **Oui** pour installer toutes les mises à jour logicielles à partir des déploiements obligatoires dont les échéances ont lieu pendant une période spécifiée. Quand un déploiement de mises à jour logicielles requis atteint une échéance, le client lance l’installation des mises à jour logicielles du déploiement. Ce paramètre détermine s’il faut installer des mises à jour logicielles d’autres déploiements requis dont l’échéance tombe dans le délai spécifié.  

Utilisez-le pour accélérer l’installation des mises à jour logicielles requises. Ce paramètre est également susceptible d’augmenter la sécurité du client, les notifications à l’utilisateur et réduire les redémarrages du client. Par défaut, ce paramètre est défini sur **Non**.  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>Durée pendant laquelle tous les déploiements en attente avec une échéance dans cette période seront également installés

Utilisez ce paramètre pour spécifier le laps de temps pour le paramètre précédent. Vous pouvez entrer une valeur comprise entre 1 et 23 heures et entre 1 et 365 jours. Par défaut, ce paramètre est configuré pour sept jours.  

### <a name="enable-installation-of-express-installation-files-on-clients"></a>Activer l’installation de fichiers d’installation rapide sur les clients

Définissez cette option sur **Oui** pour permettre aux clients d’utiliser des fichiers d’installation rapide. Pour plus d’informations, consultez [Gérer les fichiers d’installation rapide pour les mises à jour de Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).


### <a name="port-used-to-download-content-for-express-installation-files"></a>Port utilisé pour télécharger du contenu pour les fichiers d’installation rapide

Ce paramètre configure le port local permettant à l’écouteur HTTP de télécharger le contenu express. Par défaut, il est définit sur 8005. Vous n’avez pas besoin d’ouvrir ce port dans le pare-feu du client.

### <a name="enable-management-of-the-office-365-client-agent"></a>Activer la gestion de l'agent Office 365 Client

Quand vous définissez cette option sur **Oui**, il permet de configurer les paramètres d’installation d’Office 365. Il permet également de télécharger des fichiers à partir de réseaux de distribution de contenu (CDN) Office et déployer les fichiers en tant qu’application dans Configuration Manager. Pour plus d’informations, consultez [Gérer Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

### <a name="bkmk_SUMMaint"></a> Activer l’installation des mises à jour de logiciels dans la fenêtre de maintenance « Tous les déploiements » quand la fenêtre de maintenance « Mise à jour de logiciel » est disponible

Si cette option est paramétrée sur **Oui** et qu’au moins une fenêtre de maintenance « Mise à jour de logiciel » est définie sur le client, les mises à jour de logiciels s’installent pendant une fenêtre de maintenance « Tous les déploiements ». Par défaut, ce paramètre est défini sur **Non**. Ce paramètre client a été ajouté dans la version 1810 de Configuration Manager. <!--2839307-->

### <a name="bkmk_thread-priority"></a> Spécifier la priorité du thread pour les mises à jour des fonctionnalités

<!--3734525-->
À compter de la version 1902 de Configuration Manager, vous pourrez ajuster l’ordre de priorité utilisé par Windows 10 version 1709 ou clients ultérieurs pour l’installation d’une mise à jour de fonctionnalité via [maintenance de Windows 10](/sccm/osd/deploy-use/manage-windows-as-a-service). Ce paramètre n’a pas impact sur les séquences de tâches de mise à niveau sur place de Windows 10.

Ce paramètre client offre les options suivantes :

- **Non configuré** : Configuration Manager ne change pas le paramètre. Les administrateurs peuvent prédéfinir leur propre fichier setupconfig.ini. Cette valeur est la valeur par défaut.

- **Normale** : L’installation de Windows utilise plus de ressources système et effectue les mises à jour plus rapidement. Elle utilise plus de temps processeur : le temps total d’installation est donc plus court, mais le temps d’arrêt est plus long pour l’utilisateur.  

    - Configure le fichier setupconfig.ini sur l’appareil avec l’[option de la ligne de commande du programme d’installation de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) `/Priority Normal`.

- **Faible** : Vous pouvez continuer à travailler sur l’appareil pendant qu’il télécharge et se met à jour en arrière-plan. Le temps total d’installation est plus long, mais le temps d’arrêt est plus court pour l’utilisateur. En utilisant cette option, vous devrez peut-être augmenter le temps d’exécution maximale de la mise à jour afin d’éviter l’expiration du délai d’attente.  

    - Supprime l’[option de la ligne de commande du programme d’installation de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options) `/Priority` à partir du fichier setupconfig.ini.


### <a name="enable-third-party-software-updates"></a>Activer les mises à jour de logiciels tiers

Le fait d’affecter la valeur **Oui** à cette option définit la stratégie pour **Autoriser les mises à jour signées provenant d’un emplacement intranet du service de mise à jour Microsoft** et installe le certificat de signature dans le magasin d’éditeurs approuvés sur le client. Ce paramètre client a été ajouté dans Configuration Manager version 1802.

## <a name="state-messaging"></a>Messagerie d’état

### <a name="state-message-reporting-cycle-minutes"></a>Cycle de diffusion des messages d’état (en minutes)

Spécifie la fréquence à laquelle les clients signalent les messages d’état. La valeur par défaut est de 15 minutes.



## <a name="user-and-device-affinity"></a>Affinité entre utilisateur et appareil  

### <a name="user-device-affinity-usage-threshold-minutes"></a>Seuil d'utilisation de l'affinité entre utilisateur et appareil (minutes)

Spécifiez le nombre de minutes avant que Configuration Manager ne crée un mappage d’affinité entre utilisateur et appareil. Par défaut, cette valeur est 2 880 minutes (deux jours).

### <a name="user-device-affinity-usage-threshold-days"></a>Seuil d'utilisation de l'affinité entre utilisateur et appareil (jour)

Spécifiez le nombre de jours durant lesquels le client mesure le seuil de l’affinité d’appareil basée sur l’utilisation. Par défaut, cette valeur est de 30 jours.

> [!NOTE]  
> Par exemple, si vous réglez **Seuil d’utilisation de l’affinité entre utilisateur et périphérique (minutes)** sur **60** minutes et **Seuil d’utilisation de l’affinité entre utilisateur et périphérique (jours)** sur **5** jours, l’utilisateur doit utiliser l’appareil pendant 60 minutes sur une période de 5 jours pour créer une affinité automatique avec l’appareil.  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>Configurer automatiquement l'affinité entre utilisateur et appareil à partir des données d'utilisation

Choisissez **Oui** pour créer une affinité automatique entre appareil et utilisateur en fonction des informations d’utilisation recueillies par Configuration Manager.  

### <a name="allow-user-to-define-their-primary-devices"></a>Autoriser les utilisateurs à définir leurs appareils principaux

Quand ce paramètre est défini sur **Oui**, les utilisateurs peuvent identifier leurs propres appareils principaux dans le Centre logiciel.



## <a name="windows-analytics"></a>Windows Analytics

Pour plus d’informations sur ces paramètres, consultez [Configurer les clients pour envoyer des données à Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics).
