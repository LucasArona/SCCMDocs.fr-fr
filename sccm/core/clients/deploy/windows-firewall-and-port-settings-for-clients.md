---
title: Paramètres de pare-feu et de port du client Windows
titleSuffix: Configuration Manager
description: Sélectionnez les paramètres de port et de pare-feu Windows pour les clients dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 94af249b91735a535ea4056f8a5f19d120632770
ms.sourcegitcommit: 818f98187d377a90263d1b1c89d4c1fdbf8c908b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2019
ms.locfileid: "54398487"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-system-center-configuration-manager"></a>Paramètres de port et de pare-feu Windows pour les clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les ordinateurs clients qui exécutent le Pare-feu Windows exigent souvent que des exceptions soient configurées pour permettre la communication avec leur site. Les exceptions que vous devez configurer dépendent des fonctionnalités de gestion que vous utilisez avec le client Configuration Manager.  

 Utilisez les sections suivantes pour identifier ces fonctionnalités de gestion et pour obtenir plus d'informations sur la configuration du Pare-feu Windows pour ces exceptions.  

##  <a name="BKMK_ModifyingWindowsFirewall"></a> Modification des ports et programmes autorisés par le Pare-feu Windows  
 Utilisez la procédure suivante pour modifier les ports et les programmes sur le Pare-feu Windows pour le client Configuration Manager.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>Pour modifier les ports et programmes autorisés par le Pare-feu Windows  

1.  Sur l'ordinateur exécutant le Pare-feu Windows, ouvrez le Panneau de configuration.  

2.  Cliquez avec le bouton droit sur **Pare-feu Windows**, puis cliquez sur **Ouvrir**.  

3.  Configurez toutes les exceptions nécessaires et tous les programmes et ports personnalisés dont vous avez besoin.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Programmes et ports dont Configuration Manager a besoin  
 Les fonctionnalités de Configuration Manager suivantes nécessitent des exceptions sur le Pare-feu Windows :  

### <a name="queries"></a>Requêtes  
 Si vous exécutez la console Configuration Manager sur un ordinateur qui exécute le Pare-feu Windows, les requêtes échouent à leur première exécution et le système d’exploitation affiche une boîte de dialogue vous demandant si vous voulez débloquer statview.exe. Si vous débloquez statview.exe, les requêtes ultérieures s'exécuteront sans erreur. Vous pouvez également ajouter manuellement le fichier Statview.exe à la liste des programmes et services dans l'onglet **Exceptions** du Pare-feu Windows avant d'exécuter une requête.  

### <a name="client-push-installation"></a>Installation poussée du client  
 Pour procéder à une installation Push du client Configuration Manager, ajoutez les éléments suivants en tant qu’exceptions au Pare-feu Windows :  

-   Éléments sortants et entrants : **Partage de fichiers et d’imprimantes**  

-   Entrant : **Windows Management Instrumentation (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Installation du client à l'aide de la stratégie de groupe  
 Pour installer le client Configuration Manager à l’aide de la stratégie de groupe, ajoutez **Partage de fichiers et d’imprimantes** en tant qu’exception au Pare-feu Windows.  

### <a name="client-requests"></a>Requêtes client  
 Pour permettre aux ordinateurs clients de communiquer avec les systèmes de site Configuration Manager, ajoutez les éléments suivants en tant qu’exceptions au Pare-feu Windows :  

 Sortant : Port TCP **80** (pour les communications HTTP)  

 Sortant : Port TCP **443** (pour les communications HTTPS)  

> [!IMPORTANT]  
>  Ces numéros de port sont les valeurs par défaut. Elles peuvent être modifiées dans Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour configurer les ports de communication des clients dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md). Si ces ports ont été modifiés par rapport aux valeurs par défaut, vous devez également configurer des exceptions correspondantes pour le Pare-feu Windows.  

### <a name="client-notification"></a>Notification du client  
 Pour que le point de gestion signale aux ordinateurs clients les actions qu’ils doivent entreprendre quand un utilisateur administratif sélectionne une action de client dans la console Configuration Manager (téléchargement d’une stratégie d’ordinateur, démarrage d’une recherche de programmes malveillants, etc.), ajoutez l’exception suivante au Pare-feu Windows :  

 Sortant : Port TCP **10123**  

 Si la communication n’aboutit pas, Configuration Manager recommence automatiquement à utiliser le port de communication HTTP ou HTTPS existant entre le client et le point de gestion :  

 Sortant : Port TCP **80** (pour les communications HTTP)  

 Sortant : Port TCP **443** (pour les communications HTTPS)  

> [!IMPORTANT]  
>  Ces numéros de port sont les valeurs par défaut. Elles peuvent être modifiées dans Configuration Manager. Pour plus d’informations, consultez [Guide pratique pour configurer les ports de communication des clients dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md). Si ces ports ont été modifiés par rapport aux valeurs par défaut, vous devez également configurer des exceptions correspondantes pour le Pare-feu Windows.  

### <a name="remote-control"></a>Contrôle à distance  
 Pour utiliser la fonctionnalité de contrôle à distance de Configuration Manager, autorisez le port suivant :  

-   Entrant : Port TCP **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Assistance à distance et Bureau à distance  
 Pour lancer l’assistance à distance à partir de la console Configuration Manager, ajoutez le programme personnalisé **Helpsvc.exe** et le port personnalisé entrant TCP **135** à la liste des programmes et services autorisés dans le Pare-feu Windows de l’ordinateur client. Vous devez également autoriser l' **Assistance à distance** et le **Bureau à distance**. Si vous lancez l'assistance à distance depuis l'ordinateur client, le Pare-feu Windows configure et autorise automatiquement l' **Assistance à distance** et le **Bureau à distance**.  

### <a name="wake-up-proxy"></a>Proxy de mise en éveil  
 Si vous activez le paramètre client du proxy de mise en éveil, un nouveau service appelé ConfigMgr Wake-up Proxy utilise un protocole pair à pair pour savoir si d'autres ordinateurs du sous-réseau sont en éveil et pour les mettre en éveil, le cas échéant. Cette communication utilise les ports suivants :  

 Sortant : Port UDP **25536**  

 Sortant : Port UDP **9**  

 Ces numéros correspondent aux ports par défaut qui peuvent être modifiés dans Configuration Manager en utilisant les paramètres client de **Gestion de l’alimentation** appelés **Numéro de port du proxy de mise en éveil (UDP)** et **Numéro de port Wake On LAN (UDP)**. Si vous spécifiez le paramètre client **Gestion de l’alimentation** : **Exception du Pare-feu Windows pour le proxy de mise en éveil**, ces ports sont configurés automatiquement dans le Pare-feu Windows des clients. Toutefois, si les clients exécutent un autre pare-feu, vous devez configurer manuellement les exceptions pour ces numéros de port.  

 En plus de ces ports, le proxy de mise en éveil utilise également des messages de demande d'écho ICMP (Internet Control Message Protocol) entre un ordinateur client et un autre ordinateur client. Cette communication permet de savoir si l'autre ordinateur client est en éveil sur le réseau. ICMP est parfois appelé commandes ping TCP/IP.  

 Pour plus d’informations sur le proxy de mise en éveil, consultez [Planifier la sortie de veille des clients dans System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Observateur d'événements de Windows, Analyseur de performances de Windows et Diagnostics Windows  
 Pour accéder à l’Observateur d’événements Windows, à l’Analyseur de performances Windows et à Diagnostics Windows à partir de la console Configuration Manager, activez **Partage de fichiers et d’imprimantes** en tant qu’exception sur le Pare-feu Windows.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Ports utilisés lors du déploiement du client de Configuration Manager  
 Les tableaux suivants référencent les ports utilisés lors du processus d'installation du client.  

> [!IMPORTANT]  
>  S'il existe un pare-feu entre les serveurs de système de site et l'ordinateur client, confirmez si le pare-feu autorise le trafic pour les ports requis pour la méthode d'installation du client que vous avez choisie. Par exemple, les pare-feu causent souvent l'échec d'une installation poussée du client car ils bloquent le protocole SMB et les appels de procédure distante (RPC). Dans ce cas, utilisez une méthode d'installation du client différente, telle que l'installation manuelle (en exécutant CCMSetup.exe) ou l'installation du client basée sur une stratégie de groupe. Ces méthodes alternatives d'installation du client ne nécessitent pas de protocole SMB ou RPC.  

 Pour plus d'informations sur la configuration du Pare-feu Windows sur l'ordinateur client, voir la section [Modification des ports et programmes autorisés par le Pare-feu Windows](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Ports utilisés pour toutes les méthodes d'installation  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Protocole HTTP (Hypertext Transfer) à partir de l'ordinateur client vers un point d'état de secours, lorsqu'un point d'état de secours est affecté au client.|--|80 (Voir remarque 1, **Port alternatif disponible**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Ports utilisés avec l'installation poussée du client  
 Outre les ports répertoriés dans le tableau ci-après, l'installation poussée du client utilise également les messages de demande echo Internet Control Message Protocol (ICMP) à partir du serveur du site vers l'ordinateur client pour vérifier si l'ordinateur client est disponible sur le réseau. ICMP est parfois appelé commandes ping TCP/IP. ICMP ne dispose pas d'un numéro de protocole UDP ou TCP, et par conséquent, il ne figure pas dans le tableau suivant. Toutefois, tous les périphériques réseau concernés, tels que les pare-feux, doivent autoriser le trafic ICMP pour l'installation poussée du client.  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Server Message Block (SMB) entre le serveur de site et l'ordinateur client.|--|445|  
|Mappeur de point de terminaison RPC entre le serveur de site et l'ordinateur client.|135|135|  
|Ports dynamiques RPC entre le serveur de site et l'ordinateur client.|--|DYNAMIC|  
|Protocole HTTP depuis l'ordinateur client vers un point de gestion lorsque la connexion est effectuée via HTTP.|--|80 (Voir remarque 1, **Port alternatif disponible**)|  
|Protocole HTTPS depuis l'ordinateur client vers un point de gestion lorsque la connexion est effectuée via HTTPS.|--|443 (Voir remarque 1, **Port alternatif disponible**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Ports utilisés avec l'installation basée sur le point de mise à jour logicielle  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Protocole HTTP (Hypertext Transfer Protocol) à partir de l'ordinateur client vers le point de mise à jour logicielle.|--|80 ou 8530 (Voir remarque 2, **Windows Server Update Services**)|  
|Protocole HTTPS (Secure Hypertext Transfer Protocol) à partir de l'ordinateur client vers le point de mise à jour logicielle.|--|443 ou 8531 (Voir remarque 2, **Windows Server Update Services**)|  
|SMB (Server Message Block) entre le serveur source et l’ordinateur client quand vous spécifiez la propriété de ligne de commande CCMSetup **/source:&lt;Chemin\>**.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Ports utilisés avec l'installation basée sur une stratégie de groupe  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|Protocole HTTP depuis l'ordinateur client vers un point de gestion lorsque la connexion est effectuée via HTTP.|--|80 (Voir remarque 1, **Port alternatif disponible**)|  
|Protocole HTTPS depuis l'ordinateur client vers un point de gestion lorsque la connexion est effectuée via HTTPS.|--|443 (Voir remarque 1, **Port alternatif disponible**)|  
|SMB (Server Message Block) entre le serveur source et l’ordinateur client quand vous spécifiez la propriété de ligne de commande CCMSetup **/source:&lt;Chemin\>**.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Ports utilisés avec l'installation manuelle et l'installation basée sur un script d'ouverture de session  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) entre l'ordinateur client et un partage réseau à partir duquel vous exécutez CCMSetup.exe.<br /><br /> Quand vous installez Configuration Manager, les fichiers sources d’installation du client sont copiés et partagés automatiquement à partir du dossier *&lt;Chemin_Installation\>* \Client sur les points de gestion. Toutefois, vous pouvez copier ces fichiers et créer un nouveau partage sur n'importe quel ordinateur du réseau. Vous pouvez également éliminer ce trafic réseau en exécutant CCMSetup.exe localement, par exemple, à l'aide d'un support amovible.|--|445|  
|Protocole HTTP de l’ordinateur client vers un point de gestion quand la connexion est effectuée via HTTP et que vous ne spécifiez pas la propriété de ligne de commande CCMSetup **/source:&lt;Chemin\>**.|--|80 (Voir remarque 1, **Port alternatif disponible**)|  
|Protocole HTTPS de l’ordinateur client vers un point de gestion quand la connexion est effectuée via HTTPS et que vous ne spécifiez pas la propriété de ligne de commande CCMSetup **/source:&lt;Chemin\>**.|--|443 (Voir remarque 1, **Port alternatif disponible**)|  
|SMB (Server Message Block) entre le serveur source et l’ordinateur client quand vous spécifiez la propriété de ligne de commande CCMSetup **/source:&lt;Chemin\>**.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Ports utilisés avec l'installation basée sur la distribution de logiciels  

|Description|UDP|TCP|  
|-----------------|---------|---------|  
|SMB (Server Message Block) entre le point de distribution et l'ordinateur client.|--|445|  
|Protocole HTTP depuis le client vers un point de distribution lorsque la connexion est effectuée via HTTP.|--|80 (Voir remarque 1, **Port alternatif disponible**)|  
|Protocole HTTPS depuis le client vers un point de distribution lorsque la connexion est effectuée via HTTPS.|--|443 (Voir remarque 1, **Port alternatif disponible**)|  

## <a name="notes"></a>Remarques  
 **Port alternatif disponible** Dans Configuration Manager, vous pouvez définir un port alternatif pour cette valeur. Si un port personnalisé a été défini, remplacez-le quand vous définissez les informations de filtre IP pour les stratégies IPsec ou pour la configuration de pare-feu.  

 **2 Windows Server Update Services** Vous pouvez installer Windows Server Update Services (WSUS) sur le site Web par défaut (port 80) ou sur un site Web personnalisé (port 8530).  

 Après l'installation, vous pouvez modifier le port. Vous n'avez pas à utiliser le même numéro de port dans l'ensemble de la hiérarchie du site.  

 Si le numéro de port HTTP est 80, le numéro de port HTTPS doit être 443.  

 S’il s’agit d’un autre numéro de port HTTP, le numéro de port HTTPS doit être supérieur de 1 (par exemple, 8530 et 8531).
