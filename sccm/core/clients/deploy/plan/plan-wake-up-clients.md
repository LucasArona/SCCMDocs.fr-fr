---
title: Sortie de veille des clients
titleSuffix: Configuration Manager
description: Planifier la sortie de veille des clients dans System Center Configuration Manager à l’aide de Wake On LAN (WOL).
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2f36ff6c28bd8a3fa23599652aff82ef0c721cad
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474138"
---
# <a name="plan-how-to-wake-up-clients-in-system-center-configuration-manager"></a>Planifier la sortie de veille des clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Configuration Manager prend en charge les paquets de mise en éveil traditionnels permettant de réveiller les ordinateurs en mode veille lorsque vous souhaitez installer le logiciel requis, par exemple des mises à jour logicielles et des applications.  

Vous pouvez compléter la méthode traditionnelle des paquets de mise en éveil par des paramètres de client de proxy de mise en éveil. Le proxy de mise en éveil utilise un protocole entre homologues et des ordinateurs sélectionnés pour vérifier si les autres ordinateurs du sous-réseau sont éveillés et les sortir de veille si nécessaire. Lorsque le site est configuré pour l'éveil par appel réseau (Wake On LAN) et les clients configurés pour le proxy de mise en éveil, le processus fonctionne comme suit :  

1.  Les ordinateurs dotés du client Configuration Manager qui ne sont pas en veille sur le sous-réseau vérifient si les autres ordinateurs du sous-réseau sont éveillés. Pour effectuer cette vérification, ils s'envoient une commande ping TCP/IP toutes les cinq secondes.  

2.  Si les autres ordinateurs ne répondent pas, ils sont considérés comme étant en veille. Les ordinateurs qui ne sont pas en veille deviennent *ordinateurs gestionnaires* du sous-réseau.  

     Étant donné qu’un ordinateur risque ne pas répondre pour une raison autre que la veille (par exemple, s’il est éteint, supprimé du réseau ou si le paramètre client de mise en éveil du proxy n’est plus appliqué), les ordinateurs reçoivent un paquet de mise en éveil tous les jours à 14h00, heure locale. Les ordinateurs qui ne répondent pas ne sont plus considérés comme étant en veille et ne sont pas mis en éveil par le proxy de mise en éveil.  

     Pour prendre en charge un proxy de mise en éveil, au moins trois ordinateurs doivent être sortis de veille pour chaque sous-réseau. Pour remplir cette condition, trois ordinateurs sont choisis sans déterminisme en tant que *gardiens* du sous-réseau. Cet état signifie qu'ils restent éveillés, malgré toute stratégie d'alimentation configurée pour la mise en veille ou la mise en veille prolongée à l'issue d'une période d'inactivité. Les gardiens respectent les commandes d'arrêt ou de redémarrage, par exemple, consécutivement à des tâches de maintenance. Dans ce cas, les gardiens restants mettent en éveil un autre ordinateur du sous-réseau afin que le sous-réseau continue à disposer de trois gardiens.  

3.  Les ordinateurs gestionnaires demandent au commutateur réseau de rediriger le trafic réseau des ordinateurs en veille vers eux-mêmes.  

     La redirection est accomplie par l'ordinateur gestionnaire qui émet une trame Ethernet qui utilise l'adresse MAC de l'ordinateur en veille comme adresse source. Ce comportement permet au commutateur réseau de se comporter comme si l'ordinateur en veille avait été déplacé vers le même port que celui sur lequel se trouve l'ordinateur gestionnaire. L'ordinateur gestionnaire envoie également des paquets ARP pour que les ordinateurs en veille conservent l'entrée actualisée dans le cache ARP. L'ordinateur gestionnaire répond également aux requêtes ARP au nom de l'ordinateur en veille en utilisant l'adresse MAC de cet ordinateur en veille.  

    > [!WARNING]  
    >  Pendant ce processus, le mappage IP vers MAC de l'ordinateur en veille reste le même. Le proxy de mise en éveil fonctionne en informant le commutateur réseau qu'une autre carte réseau utilise le port qui a été enregistré par une autre carte réseau. Toutefois, ce comportement est connu sous le nom de bagottement MAC et il est inhabituel dans le cadre d'un fonctionnement normal du réseau. Certains outils d'analyse réseau recherchent ce comportement et peuvent supposer que quelque chose ne va pas. Par conséquent, ces outils d'analyse peuvent générer des alertes ou arrêter des ports lorsque vous utilisez le proxy de mise en éveil.  
    >   
    >  N'utilisez pas de proxy de mise en éveil si vos outils et services d'analyse réseau n'autorisent pas les bagottements MAC.  

4.  Lorsqu'un ordinateur gestionnaire voit une nouvelle demande de connexion TCP pour un ordinateur en veille et que la demande cible un port que l'ordinateur en veille écoutait avant sa mise en veille, l'ordinateur gestionnaire envoie un paquet de mise en éveil à l'ordinateur en veille, puis arrête la redirection du trafic pour cet ordinateur.  

5.  L'ordinateur en veille reçoit le paquet de mise en éveil et sort de veille. L'ordinateur expéditeur procède automatiquement à une nouvelle tentative de connexion et cette fois, l'ordinateur est mis en éveil et peut répondre.  

 Le proxy de mise en éveil est soumis aux conditions préalables et limitations suivantes :  

> [!IMPORTANT]  
>  Si vous disposez d'une équipe distincte responsable de l'infrastructure réseau et des services réseau, avertissez-la et intégrez-la lors de votre évaluation et votre période de test. Par exemple, sur un réseau qui utilise le contrôle d'accès réseau 802.1X, le proxy de mise en éveil ne fonctionne pas et peut perturber le service réseau. En outre, le proxy de mise en éveil peut amener certains outils d'analyse réseau à générer des alertes en cas de détection de trafic destiné à mettre en éveil d'autres ordinateurs.  

-   Tous les systèmes d’exploitation Windows répertoriés comme clients pris en charge dans [Systèmes d’exploitation pris en charge pour les clients et appareils](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sont pris en charge pour l'éveil par appel réseau (Wake On LAN).  

-   Les systèmes d'exploitation invités qui s'exécutent sur une machine virtuelle ne sont pas pris en charge.  

-   Les clients doivent être activés pour le proxy de mise en éveil via des paramètres client. Bien que le fonctionnement du proxy de mise en éveil ne dépende pas de l'inventaire matériel, les clients ne signalent pas l'installation du service du proxy de mise en éveil sauf s'ils sont activés pour l'inventaire matériel et qu'ils ont soumis au moins un inventaire matériel.  

-   Les cartes réseau (et éventuellement le BIOS) doivent être activées et configurées pour les paquets de mise en éveil. Si la carte réseau n’est pas configurée pour les paquets de mise en éveil ou que ce paramètre est désactivé, Configuration Manager le configure et l’active automatiquement pour un ordinateur à réception du paramètre client permettant d’activer le proxy de mise en éveil.  

-   Si un ordinateur possède plusieurs cartes réseau, vous ne pouvez pas configurer la carte à utiliser pour le proxy de mise en éveil ; ce choix s'effectue sans déterminisme. Cependant, la carte choisie est enregistrée dans le fichier SleepAgent_<DOMAINE\>@SYSTEM_0.log.  

-   Le réseau doit autoriser les requêtes d'écho ICMP (au moins au sein du sous-réseau). Vous ne pouvez pas configurer l'intervalle de cinq secondes qui est utilisé pour envoyer les commandes ping ICMP.  

-   La communication est décryptée et non authentifiée, et le protocole IPsec n'est pas pris en charge.  

-   Les configurations réseau suivantes ne sont pas prises en charge :  

    -   802.1X avec authentification de port  

    -   Réseaux sans fil  

    -   Commutateurs réseau permettant de lier des adresses MAC à des ports spécifiques  

    -   Réseaux IPv6 uniquement  

    -   Durées de bail DHCP inférieures à 24 heures  

Si vous voulez sortir de veille des ordinateurs pour l’installation planifiée d’un logiciel, vous devez configurer chaque site principal de sorte que ce dernier utilise des paquets de mise en éveil.  

 Pour utiliser le proxy de mise en éveil, vous devez déployer les paramètres client correspondants de gestion de l’alimentation en plus de configurer le site principal.  

Décidez d’utiliser ou non des paquets de diffusions dirigées vers le sous-réseau, ou des paquets monodiffusion, ainsi que le numéro de port UDP à utiliser. Par défaut, les paquets de mise en éveil traditionnels sont transmis via le port UDP 9, mais pour une plus grande sécurité, vous pouvez sélectionner un autre port pour le site si cet autre port est pris en charge par les routeurs et pare-feu qui interviennent.  

### <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Choisir entre une diffusion monodiffusion et une diffusion dirigée vers le sous-réseau pour Wake on LAN  
 Si vous avez choisi de réveiller des ordinateurs en envoyant des paquets de mise en éveil traditionnels, vous devez décider de transmettre les paquets monodiffusion ou les paquets de diffusion dirigée vers le sous-réseau. Si vous utilisez le proxy de mise en éveil, vous devez utiliser des paquets monodiffusion. Sinon, utilisez le tableau suivant pour déterminer la méthode de transmission à choisir.  

|Méthode de transmission|Avantages|Inconvénients|  
|-------------------------|---------------|------------------|  
|Monodiffusion|Il s'agit d'une solution plus sécurisée que les diffusions dirigées vers le sous-réseau car le paquet est envoyé directement à un seul ordinateur, et non à tous les ordinateurs d'un sous-réseau.<br /><br /> Ne nécessite pas de reconfiguration des routeurs (vous devrez peut-être configurer le cache ARP).<br /><br /> Elle consomme moins de bande passante réseau que les transmissions par diffusion dirigées vers le sous-réseau.<br /><br /> Prise en charge avec IPv4 et IPv6.|Les paquets de mise en éveil ne trouvent pas les ordinateurs de destination qui ont modifié leur adresse de sous-réseau depuis le dernier calendrier d'inventaire matériel.<br /><br /> La configuration des commutateurs sera peut-être nécessaire pour transmettre les paquets UDP.<br /><br /> Il est possible que certaines cartes réseau ne répondent pas aux paquets de mise en éveil dans tous les états de veille lorsque la monodiffusion est utilisée comme méthode de transmission.|  
|Diffusion dirigée vers le sous-réseau|Elle génère un taux de réussite supérieur à celui de la monodiffusion si vous possédez des ordinateurs qui modifient souvent leur adresse IP dans le même sous-réseau.<br /><br /> Aucune configuration de commutateur n'est requise.<br /><br /> Le taux de compatibilité avec les cartes d'ordinateurs pour tous les états de veille est élevé. En effet, les diffusions dirigées vers le sous-réseau correspondaient à la méthode de transmission d'origine pour l'envoi des paquets de mise en éveil.|Solution moins sûre que l'utilisation de la monodiffusion, car une personne malveillante pourrait envoyer des flux continus de demandes d'écho ICMP à partir d'une adresse source falsifiée à l'adresse de diffusion dirigée. En conséquence, tous les hôtes répondent à cette adresse source. Si les routeurs sont configurés pour autoriser les diffusions dirigées vers le sous-réseau, la configuration supplémentaire est recommandée pour des raisons de sécurité :<br /><br /> -   Configurez les routeurs pour autoriser uniquement les diffusions dirigées vers IP depuis le serveur de site Configuration Manager, à l’aide d’un numéro de port UDP spécifique.<br />-   Configurez Configuration Manager pour utiliser le numéro de port autre que celui par défaut spécifié.<br /><br /> Il peut être nécessaire de reconfigurer tous les routeurs intervenants pour permettre des diffusions dirigées vers le sous-réseau.<br /><br /> Elle consomme plus de bande passante réseau que les transmissions par monodiffusion.<br /><br /> Prise en charge avec IPv4 uniquement. IPv6 n'est pas pris en charge.|  

> [!WARNING]  
>  Il existe des risques de sécurité associés aux diffusions dirigées vers le sous-réseau : Une personne malveillante pourrait envoyer des flux continus de demandes d'écho ICMP (Internet Control Message Protocol) à partir d'une adresse source falsifiée vers l'adresse de diffusion dirigée, obligeant tous les hôtes à répondre à cette adresse source. Ce type d'attaque par déni de service est généralement appelé attaque de réflexion et est traité en rejetant les diffusions dirigées vers le sous-réseau.
