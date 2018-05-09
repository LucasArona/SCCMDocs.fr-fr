---
title: Aide Endpoint Protection Client
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités et améliorations dans Endpoint Protection qui vous aident à protéger votre ordinateur contre les menaces.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 580218b701b01af388b56bbd2b7293f67cf5d77d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="endpoint-protection-client-help"></a>Aide Endpoint Protection Client

*S’applique à : System Center Configuration Manager (Current Branch)*


Cette version de Windows Defender ou d’Endpoint Protection inclut les fonctionnalités suivantes pour mieux protéger votre ordinateur contre les menaces :  

-   **Intégration du Pare-feu Windows** Le programme d’installation de Endpoint Protection vous permet d’activer ou de désactiver le Pare-feu Windows.  
-   **Système d'inspection réseau.** Cette fonctionnalité améliore la protection en temps réel en inspectant le trafic réseau pour mieux bloquer de façon proactive les attaques visant les failles de sécurité connues du réseau.  
-   **Moteur de protection.** La protection en temps réel détecte les logiciels malveillants et les empêche de s’installer ou de s’exécuter sur votre PC. Le moteur mis à jour offre des fonctions de nettoyage et de détection améliorées avec de meilleures performances.  

Windows Defender est fourni comme composant du système d’exploitation Windows 10.  Dans les versions antérieures de Windows, votre administrateur peut fournir Windows Defender ou Endpoint Protection à l’aide du logiciel de gestion.

Vous y trouverez également une liste de [questions fréquentes sur Windows Defender et Endpoint Protection](endpoint-protection-client-faq.md). Pour obtenir de l’aide sur la résolution des problèmes, consultez [Résolution des problèmes du client Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md). Pour obtenir une liste des nouvelles fonctionnalités, consultez [Nouveautés de Windows Defender](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender).

## <a name="windows-firewall-integration"></a>Intégration du Pare-feu Windows  
 Le Pare-feu Windows peut permettre d'empêcher les personnes ou logiciels malveillants d'accéder à votre ordinateur via Internet ou un réseau. Quand vous installez Endpoint Protection, l’Assistant Installation vérifie que le Pare-feu Windows est activé. Si vous avez volontairement désactivé le Pare-feu Windows, vous pouvez éviter de l'activer en désactivant une case à cocher. Vous pouvez modifier les paramètres du Pare-feu Windows à tout moment via les paramètres Système et sécurité dans le Panneau de configuration.  

## <a name="network-inspection-system"></a>Système d'inspection réseau  
 Les personnes malveillantes mènent de plus en plus d'attaques par le réseau contre des failles de sécurité exposées avant que les éditeurs de logiciels ne puissent développer et distribuer des mises à jour de sécurité. Les études des failles de sécurité montrent que le délai peut être d'un mois ou plus entre le moment où une attaque est signalée et celui où une mise à jour de sécurité appropriée est développée, testée et publiée. Ce manque de protection laisse de nombreux ordinateurs vulnérables aux attaques pendant une longue période. Le système d'inspection réseau fonctionne avec la protection en temps réel pour mieux vous protéger contre les attaques par le réseau en réduisant grandement le délai entre les divulgations des vulnérabilités et le déploiement des mises à jour, de quelques semaines à quelques heures.  

## <a name="award-winning-protection-engine"></a>Moteur de protection primé  
 Windows Defender ou Endpoint Protection comprend un moteur de protection reconnu, qui est mis à jour régulièrement. Le moteur est soutenu par une équipe de chercheurs de logiciels anti-programme malveillant du Centre de protection Microsoft contre les programmes malveillants, qui fournit des réponses aux menaces les plus récentes des programmes malveillants 24 heures sur 24.  

## <a name="windows-defender-settings"></a>Paramètres de Windows Defender
Les paramètres de Windows Defender activent des paramètres qui permettent de protéger votre PC contre les logiciels malveillants. Votre administrateur peut gérer certains paramètres de Windows Defender à votre place. Vous pouvez en gérer d’autres en utilisant les paramètres de Windows Defender. Nous vous recommandons d’activer les paramètres de Windows Defender afin de protéger votre PC et vos données.

Pour afficher les paramètres de Windows Defender, recherchez `Windows Defender` sur votre PC. Ouvrez **Windows Defender** et sélectionnez **Paramètres**. Les paramètres de Windows Defender incluent :
- **Protection en temps réel** : détecte les logiciels malveillants et les empêche de s’installer ou de s’exécuter sur votre PC.
- **Protection dans le cloud** : Windows Defender envoie des informations à Microsoft sur les menaces de sécurité potentielles.
- **Envoi automatique d’un échantillon** : autorisez Windows Defender à envoyer des échantillons de fichiers suspects à Microsoft pour améliorer la détection de programmes malveillants.
- **Exclusions** : vous pouvez exclure des fichiers, dossiers, extensions de fichiers ou processus spécifiques de l’analyse de Windows Defender.
- **Notifications améliorées** : active des notifications qui vous informent sur l’intégrité de votre PC. Même si le paramètre est **désactivé**, vous recevez les notifications critiques.
- **Windows Defender hors ligne** : vous pouvez exécuter Windows Defender hors ligne pour mieux détecter et supprimer les logiciels malveillants. Cette analyse va redémarrer votre PC et prendra environ 15 minutes.

### <a name="see-also"></a>Voir aussi  
 [Forum aux questions sur le client Endpoint Protection](endpoint-protection-client-faq.md)   
 [Résolution des problèmes du client Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md)
