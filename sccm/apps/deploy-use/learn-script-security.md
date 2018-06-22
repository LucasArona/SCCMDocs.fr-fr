---
title: En savoir plus sur la sécurité des scripts PowerShell
titleSuffix: Configuraton Manager
description: Ressources pour en savoir plus sur la sécurité des scripts PowerShell.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: a0bd093d-67a5-4f74-bf79-dd604889f5ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7799ac9737ac3a6a73d2d7241dd8b56325d4e340
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343709"
---
# <a name="learn-more-about-powershell-script-security"></a>En savoir plus sur la sécurité des scripts PowerShell

*S’applique à : System Center Configuration Manager (Current Branch)*

Il est de la responsabilité de l’administrateur de valider l’utilisation des paramètres PowerShell et PowerShell proposés dans son environnement. Les ressources fournies dans ce document visent à sensibiliser les administrateurs à la puissance de PowerShell, mais aussi aux risques potentiels associés. Elles donnent des indications sur la façon de limiter ces risques potentiels et d’utiliser les scripts en toute sécurité.

## <a name="powershell-script-security"></a>Sécurité des scripts PowerShell
Intégrée à l’exécution de scripts, une fonctionnalité permet d’examiner et d’approuver les scripts appelés à être exécutés dans l’environnement. Les administrateurs doivent savoir que derrière les scripts PowerShell peuvent se cacher un script obfusqué, c’est-à-dire un script malveillant et difficile à détecter visuellement pendant la phase d’approbation. En guise de bonne pratique, en plus de l’examen visuel des scripts PowerShell, il est recommandé d’utiliser certains outils d’inspection de façon à détecter les scripts suspects. Si ces outils ne peuvent pas toujours déterminer l’intention de l’auteur PowerShell, ils permettent d’attirer l’attention sur un script suspect. Il revient cependant à l’administrateur de juger du caractère malveillant ou intentionnel de la syntaxe du script.

## <a name="recommendations"></a>Recommandations
- Prenez-connaissance des bonnes pratiques de sécurité PowerShell en utilisant les différents liens présentés ci-dessous en référence.
- **Signez vos scripts** : pour sécuriser les scripts dans la durée, une autre méthode consiste à les examiner minutieusement et à les signer avant de les importer pour les utiliser.
- Évitez de stocker les secrets (tels que les mots de passe) dans les scripts PowerShell et apprenez à mieux les gérer.


## <a name="general-information-about-powershell-security-best-practices"></a>Informations générales sur les bonnes pratiques en matière de sécurité PowerShell

Ces différents liens ont été choisis comme point de départ pour permettre aux administrateurs de Configuration Manager d’assimiler les bonnes pratiques en matière de sécurité des scripts PowerShell.  

[Introduction to PowerShell Security Best Practices](https://blogs.msdn.microsoft.com/powershell/2013/12/16/powershell-security-best-practices/ )

[PowerShell Security Best Practices (diaporama PowerPoint)](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/74/metablogapi/1055.PowerShell-Security-Best-Practices_3CA24C32.pptx)

<iframe src="https://channel9.msdn.com/Events/Blue-Hat-Security-Briefings/BlueHat-Security-Briefings-Fall-2013-Sessions/PowerShell-Best-Practices/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

[Defending Against PowerShell Attacks, blog de l’équipe PowerShell](https://blogs.msdn.microsoft.com/powershell/2017/10/23/defending-against-powershell-attacks/)

[Defending Against PowerShell Attacks (Twitter), de Lee Holmes, promoteur de Microsoft PowerShell et de la sécurité](https://twitter.com/Lee_Holmes/status/922462821081694208)

[Protecting Against Malicious Code Injection](https://blogs.msdn.microsoft.com/powershell/2006/11/22/protecting-against-malicious-code-injection/)

[Informations sur la sécurité dans PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2015/08/06/powershell-gallery-new-security-scan/)

[PowerShell The Blue Team, évoque la journalisation de blocs de script en profondeur, la journalisation d’événements protégée, l’interface d’analyse anti-programme malveillant, les API de génération de code sécurisé](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)

[Pour Windows 10, il existe une API pour une interface d’analyse anti-programme malveillant](https://cloudblogs.microsoft.com/microsoftsecure/2015/06/09/windows-10-to-offer-application-developers-new-malware-defenses/?source=mmpc)

## <a name="powershell-parameters-security"></a>Sécurité des paramètres PowerShell
Passer les paramètres est un moyen de bénéficier d’une certaine souplesse avec les scripts et de remettre les décisions au moment de l’exécution. Cela vous expose aussi à d’autres risques. Les bonnes pratiques pour empêcher l’injection de paramètres ou de scripts malveillants sont les suivantes :

- Autorisez uniquement l’utilisation de paramètres prédéfinis.
- Utilisez la fonctionnalité d’expression régulière pour valider les paramètres autorisés.
    - Exemple : si seulement une certaine plage de valeurs est autorisée, utilisez une expression régulière pour rechercher uniquement les caractères ou les valeurs qui figurent dans la plage.
    - La validation des paramètres peut contribuer à dissuader les utilisateurs d’essayer d’utiliser certains caractères qui peuvent être des caractères d’échappement, comme les guillemets. Sachant qu’il existe plusieurs types de guillemets, il est souvent plus facile d’utiliser des expressions régulières pour valider les caractères que vous avez décidé d’autoriser que d’essayer de définir toutes les entrées non autorisées.
- Tirez parti du module PowerShell [« InjectionHunter »](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) dans PowerShell Gallery.
    - Sachant qu’il peut renvoyer des faux positifs, examinez l’intention des éléments signalés comme étant suspects pour déterminer s’il s’agit de problèmes réels. 
- Microsoft Visual Studio intègre un analyseur de script qui peut vous aider à vérifier la syntaxe PowerShell.
- Cette vidéo intitulée : « DEF CON 25 - Lee Holmes - Get $pwnd: Attacking Battle Hardened Windows Server » offre une vue d’ensemble des différents types de problèmes contre lesquels vous pouvez vous protéger (en particulier la passage de 12:20 à 17:50) :     <iframe width="560" height="315" src="https://www.youtube.com/embed/ahxMOAAani8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

## <a name="environment-recommendations"></a>Recommendations concernant l’environnement
Recommandations générales pour les administrateurs de PowerShell.
1. Déployez la dernière version de PowerShell, par exemple la version 5 ou ultérieure, intégrée à Windows 10. Vous pouvez aussi déployer [Windows Management Framework](https://www.microsoft.com/en-us/download/details.aspx?id=54616) dès Windows 7 et Windows Server 2008 R2. 
2. Activez et collectez les journaux PowerShell en incluant éventuellement la journalisation d’événements protégée. Incorporez ces journaux dans vos flux de travail de signature, de recherche et de réponse aux incidents.
3. Implémentez Just Enough Administration sur les systèmes de grande valeur pour éliminer ou limiter l’accès administratif sans contrainte à ces systèmes.
4. Déployez des stratégies Device Guard/Application Control pour permettre une pleine exploitation des capacités du langage PowerShell dans les tâches d’administration pré-approuvées, tout en limitant l’utilisation interactive et non approuvée à une partie limitée du langage PowerShell.
5. Déployez Windows 10 pour que votre fournisseur de logiciel antivirus puisse accéder à l’ensemble du contenu (y compris au contenu généré ou dé-obfusqué au moment de l’exécution) traité par les hôtes de script Windows, notamment PowerShell.