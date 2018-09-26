---
title: Préparer la mise en cache d’homologue Windows PE pour réduire le trafic WAN
titleSuffix: Configuration Manager
description: Le cache d’homologue Windows PE vise à obtenir le contenu d’un homologue local et à réduire le trafic WAN en l’absence de point de distribution local.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 69d8db3cceff45319ed4f2fc0b2962c3bb50b0f2
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756170"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-system-center-configuration-manager"></a>Préparer le cache d’homologue Windows PE pour réduire le trafic WAN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous déployez un nouveau système d’exploitation dans System Center Configuration Manager, les ordinateurs qui exécutent la séquence de tâches peuvent utiliser le cache d’homologue Windows PE pour obtenir du contenu à partir d’un homologue local (source de cache d’homologue) au lieu de le télécharger à partir d’un point de distribution. Cela permet de réduire le trafic du réseau étendu dans les scénarios de succursale où il n'existe aucun point de distribution local.  

 La mise en cache d’homologue Windows PE est similaire à [Windows BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmk_branchcache), mais elle fonctionne dans l’environnement de préinstallation Windows (Windows PE). Les termes suivants sont employés pour décrire les clients qui utilisent la mise en cache d’homologue Windows PE :  

-   Un **client de mise en cache d'homologue** est un ordinateur configuré pour utiliser la mise en cache d'homologue Windows PE.  

-   Une **source de mise en cache d'homologue** est un client  configuré pour la mise en cache d'homologue et qui met du contenu à disposition d'autres clients de cache d'homologue qui demandent ce contenu.  

Pour savoir comment gérer le cache d’homologue, consultez les sections suivantes.

##  <a name="BKMK_PeerCacheObjects"></a> Objets stockés dans une source de mise en cache d’homologue  
 Une séquence de tâches configurée pour utiliser la mise en cache d’homologue Windows PE peut obtenir les objets de contenu suivants en cas d’exécution dans Windows PE :  

-   Image du système d'exploitation  

-   Package de pilotes  

-   Packages et des programmes (lorsque le client continue d’exécuter la séquence de tâches dans le système d’exploitation complet, le client obtient ce contenu à partir d’une source de mise en cache d’homologue si la séquence de tâches a été initialement configurée pour la mise en cache d’homologue lors de l’exécution dans Windows PE).  

-   des images de démarrage supplémentaires.  

 Les objets de contenu suivants ne sont jamais transférés à l’aide de la mise en cache d’homologue. Au lieu de cela, ils sont transférés à partir d’un point de distribution, ou par Windows BranchCache si vous avez configuré Windows BranchCache dans votre environnement :  

-   Applications  

-   Mises à jour logicielles  

##  <a name="BKMK_PeerCacheWork"></a> Comment fonctionne la mise en cache d’homologue Windows PE ?  
 Imaginez un scénario avec une filiale qui ne dispose pas de point de distribution, mais qui a plusieurs clients activés pour utiliser la mise en cache d’homologue Windows PE. Vous déployez la séquence de tâches configurée pour utiliser la mise en cache d’homologue sur plusieurs clients qui sont configurés comme faisant partie de la source de mise en cache d’homologue. Le premier client à exécuter la séquence de tâches diffuse une demande pour trouver un homologue qui possède le contenu. N’en trouvant aucun, il obtient le contenu à partir d’un point de distribution sur le réseau étendu. Le client installe la nouvelle image et stocke ensuite le contenu dans son cache de client Configuration Manager pour pouvoir fonctionner en tant que source de cache d’homologue pour d’autres clients. Lorsque le client suivant exécute la séquence de tâches, il diffuse une requête sur le sous-réseau pour une source de mise en cache d'homologue et le premier client répond et rend son contenu mis en cache accessible.  

##  <a name="BKMK_PeerCacheDetermine"></a> Déterminer les clients qui feront partie de la source de mise en cache d’homologue Windows PE  
 Pour faciliter la sélection des ordinateurs qui doivent faire partie de la source de mise en cache d’homologue Windows PE, vous devez prendre en compte plusieurs facteurs :  

-   La source de mise en cache d’homologue Windows PE doit être un ordinateur de bureau qui est toujours sous tension et accessible aux clients de mise en cache d’homologue.  

-   La mise en cache d’homologue Windows PE a une taille de cache client suffisante pour stocker les images.  

##  <a name="BKMK_PeerCacheRequirements"></a> Configuration requise pour qu’un client puisse utiliser une source de mise en cache d’homologue Windows PE  
 Pour qu’un client puisse utiliser une source de mise en cache d’homologue Windows PE, il doit remplir les conditions suivantes :  

-   Le client Configuration Manager doit pouvoir communiquer via les ports suivants sur votre réseau :  

    -   Port pour la diffusion réseau initiale, pour rechercher une source de mise en cache d’homologue. Par défaut, il s’agit du port 8004.  

    -   Port pour le téléchargement de contenu à partir d’une source de mise en cache d’homologue (HTTP et HTTPS). Par défaut, il s’agit du port 8003.  

        > [!TIP]  
        >  Les clients utilisent le protocole HTTPS pour télécharger le contenu quand il est disponible. Toutefois, le même numéro de port est utilisé pour HTTP ou HTTPS.  

-   [Configurez le cache client pour les clients Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache) sur les clients pour vous assurer qu’ils ont suffisamment d’espace pour stocker les images que vous déployez. La mise en cache d’homologue Windows PE n’affecte pas la configuration ou le comportement du cache du client.  

-   Les options de déploiement de séquence de tâches doivent être configurées pour télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches.  

##  <a name="BKMK_PeerCacheConfigure"></a> Configurer la mise en cache d’homologue Windows PE  
 Vous pouvez appliquer les méthodes suivantes pour approvisionner un client avec du contenu de mise en cache d’homologue, pour qu’il puisse agir comme source de mise en cache d’homologue :  

-   Un client de mise en cache d'homologue qui ne trouve pas de source de mise en cache d'homologue avec le contenu le télécharge à partir d'un point de distribution.  Si le client reçoit des paramètres client qui activent la mise en cache d'homologue et que la séquence de tâches est configurée pour conserver le contenu mis en cache, le client devient une source de mise en cache d'homologue.  

-   Un client de mise en cache d'homologue peut obtenir du contenu à partir d'un autre client de mise en cache d'homologue (une source de mise en cache d'homologue).  Le client étant configuré pour la mise en cache d'homologue, quand il exécute une séquence de tâches configurée pour conserver le contenu mis en cache, il devient une source de mise en cache d'homologue.  

-   Un client exécute une séquence de tâches qui comprend l’étape facultative [Télécharger le contenu du package](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent), qui sert à préparer le contenu pertinent inclus dans la séquence de tâches de mise en cache d’homologue Windows PE. Quand vous appliquez cette méthode :  

    -   Le client n'a pas besoin d'installer l'image qui est en cours de déploiement.  

    -   Outre l’option **Télécharger le contenu du package**, la séquence de tâches doit également utiliser l’option **Cache du client Configuration Manager**. Cette option vous permet de stocker le contenu dans le cache des clients pour que le client puisse agir comme source de mise en cache d'homologue pour d'autres clients de mise en cache d'homologue.  

 Les procédures suivantes vous aideront à configurer la mise en cache d'homologue Windows PE sur les clients et à configurer des séquences de tâches qui prennent en charge la mise en cache d'homologue.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>Pour configurer les ordinateurs sources de mise en cache d’homologue Windows PE  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client**, puis créez des **paramètres de périphérique client personnalisés** ou modifiez un objet de paramètres existant. Vous pouvez aussi configurer cela pour l'objet **Paramètres client par défaut** .  

    > [!TIP]  
    >  Utilisez un objet de paramètres personnalisés pour gérer les clients qui reçoivent cette configuration. Par exemple, vous souhaiterez peut-être éviter de configurer cela sur les ordinateurs portables des utilisateurs qui sont souvent en déplacement. Un système hautement mobile peut être une source médiocre pour fournir du contenu à d'autres clients de mise en cache d'homologue.  
    >   
    >  Souvenez-vous aussi que lorsque vous configurez ce paramètre dans le cadre des **Paramètres client par défaut**, la configuration s'applique à tous les clients de votre environnement.  

2.  Sous **Mise en cache d'homologue Windows PE**, affectez la valeur **Oui** à **Permettre au client Configuration Manager exécutant le système d'exploitation complet de partager du contenu**.  

    -   Par défaut, seul le protocole HTTP est activé. Si vous souhaitez permettre aux clients de télécharger du contenu via HTTPS, affectez la valeur **Oui** à **Activer HTTPS pour la communication d'homologues clients**.  

    -   Par défaut, le port pour les diffusions est défini sur 8004 et le port pour les téléchargements de contenu est défini sur 8003. Vous pouvez les changer tous les deux.  

3.  Enregistrez et déployer les paramètres client sur les clients que vous sélectionnez comme sources de mise en cache d’homologue.  

 Une fois qu'un appareil est configuré avec cet objet de paramètres, il est configuré pour agir comme source de mise en cache d'homologue. Vous devez déployer ces paramètres sur les clients de mise en cache d'homologue potentiels pour configurer les ports et protocoles nécessaires.  

###  <a name="BKMK_PeerCacheConfigureTS"></a> Configurer une séquence de tâches pour la mise en cache d’homologue Windows PE  
 Quand vous configurez la séquence de tâches, utilisez les variables suivantes comme Variables du regroupement sur le regroupement dans lequel la séquence de tâches est déployée :  

-   **SMSTSPeerDownload**  

     Valeur :  TRUE  

     Cela permet au client d'utiliser la mise en cache d'homologue Windows PE.  

-   **SMSTSPeerRequestPort**  

     Valeur : <Numéro de port\>  

     Lorsque vous n’utilisez pas le port par défaut configuré dans les Paramètres client (8004), vous devez configurer cette variable avec une valeur personnalisée du port réseau à utiliser pour la diffusion initiale.  

-   **SMSTSPreserveContent**  

     Valeur : TRUE  

     Le contenu est ainsi marqué dans la séquence de tâches de façon à être conservé dans le cache du client Configuration Manager après le déploiement. Cette variable se distingue de SMSTSPersisContent, qui conserve uniquement le contenu pendant la durée de la séquence de tâches et utilise le cache de la séquence de tâches, et non le cache du client Configuration Manager.  

 Pour plus d’informations, consultez [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables).  

###  <a name="BKMK_PeerCacheValidate"></a> Valider la réussite de l’utilisation de la mise en cache d’homologue Windows PE  
 Une fois que vous avez utilisé la mise en cache d’homologue Windows PE pour déployer et installer une séquence de tâches, vous pouvez vérifier que le processus a bien utilisé la mise en cache d’homologue en consultant le fichier **smsts.log** sur le client qui a exécuté la séquence de tâches.  

 Dans le journal, recherchez une entrée similaire à la suivante, où <*Nom_Serveur_Source*> identifie l’ordinateur à partir duquel le client a obtenu le contenu. Cet ordinateur doit être une source de mise en cache d'homologue, et non un serveur de point de distribution. Les autres informations varient en fonction de votre environnement local et des configurations.  

-   *<![LOG[Downloaded file from http:// <Nom_Serveur_Source\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim to C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
