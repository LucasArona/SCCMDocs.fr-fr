---
title: Forum aux questions sur le client Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenez des réponses aux questions fréquemment posées sur Windows Defender et Endpoint Protection.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3aaa9d2-a40e-42b1-ad75-5a115351729e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ba364ce222ae5e07cc1a0e9d25eb3ae525f2cbbf
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142389"
---
# <a name="endpoint-protection-client-frequently-asked-questions"></a>Forum aux questions sur le client Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*


Ce forum aux questions est destiné aux utilisateurs dont l’administrateur informatique a déployé Windows Defender ou Endpoint Protection sur leur ordinateur. Les informations fournies ci-après peuvent ne pas s’appliquer aux autres logiciels anti-programme malveillant. Microsoft System Center Endpoint Protection gère Windows Defender sur Windows 10. Il peut également déployer et gérer le client Endpoint Protection sur des ordinateurs exécutant une version antérieure à Windows 10. Windows Defender est décrit dans cet article, mais les informations qui le concernent s’appliquent également à Endpoint Protection.  

-   [Pourquoi ai-je besoin d’un logiciel antivirus et anti-espion ?](#why-do-i-need-antivirus-and-antispyware-software)  
-   [Comment savoir si mon ordinateur est infecté par un logiciel malveillant ?](#how-can-i-tell-if-my-computer-is-infected-with-malicious-software)
-   [Comment puis-je trouver la version de Windows Defender ?](#how-can-i-find-the-version-of-windows-defender)
-   [Que faire si Windows Defender ou Endpoint Protection détecte un logiciel malveillant sur mon ordinateur ?](#what-should-i-do-if-windows-defender-or-endpoint-protection-detects-software-on-my-computer)  
-   [Qu’est-ce qu’un virus ?](#what-is-a-virus)  
-   [Qu’est-ce qu’un logiciel espion ?](#what-is-spyware)  
-   [Quelle est la différence entre les virus, les logiciels espions et autres logiciels potentiellement dangereux ?](#hat-s-the-difference-between-viruses-spyware-and-other-potentially-harmful-software)  
-   [D’où viennent les virus, les logiciels espions et les autres logiciels potentiellement indésirables ?](#where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from)  
-   [Puis-je recevoir un logiciel malveillant sans le savoir ?](#can-i-get-malicious-software-without-knowing-it)  
-   [Pourquoi est-il important de lire les contrats de licence avant d’installer des logiciels ?](#why-is-it-important-to-review-license-agreements-before-installing-software)  
-   [Quelle est la différence entre Endpoint Protection et Windows Defender ?](#what-s-the-difference-between-endpoint-protection-and-windows-defender)  
-   [Pourquoi Windows Defender ne détecte-t-il pas les cookies ?](#why-doesn-t-windows-defender-detect-cookies)  
-   [Comment me protéger contre les programmes malveillants ?](#how-can-i-prevent-malware)  
-   [Que sont les définitions de virus et de logiciels espions ?](#what-are-virus-and-spyware-definitions)  
-   [Comment maintenir à jour les définitions de virus et de logiciels espions ?](#how-do-i-keep-virus-and-spyware-definitions-up-to-date)  
-   [Comment supprimer ou restaurer des éléments mis en quarantaine par Windows Defender ou Endpoint Protection ?](#how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection)  
-   [Qu’est-ce que la protection en temps réel ?](#what-is-real-time-protection)  
-   [Comment savoir si Windows Defender ou Endpoint Protection est en cours d’exécution sur mon ordinateur ?](#how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer)
-   [Comment configurer les alertes envoyées par Windows Defender ou Endpoint Protection ?](#how-to-set-up-windows-defender-or-endpoint-protection-alerts)  

##  <a name="why-do-i-need-antivirus-and-antispyware-software"></a>Pourquoi ai-je besoin d’un logiciel antivirus et anti-espion ?  

 Il est primordial que votre ordinateur soit doté d'un logiciel de protection contre les logiciels malveillants. Les logiciels malveillants, qui comprennent les virus, logiciels espions ou tout autre logiciel potentiellement indésirable, peuvent tenter de s'installer sur votre ordinateur à chaque fois que vous êtes connecté à Internet. Ils peuvent également infecter votre ordinateur lorsque vous installez un programme à l'aide d'un CD, DVD ou tout autre support amovible. Les programmes malveillants peuvent également être programmés pour s'exécuter à des moments inattendus, et pas seulement au moment de leur installation.  

 Windows Defender ou Endpoint Protection offre trois méthodes permettant d’empêcher les programmes malveillants d’infecter votre ordinateur :  

-   **Utilisation de la protection en temps réel** : la protection en temps réel permet à Windows Defender de surveiller en permanence votre ordinateur et de vous alerter quand des logiciels malveillants ‍‍tentent de s’installer ou de s’exécuter sur votre ordinateur. Windows Defender suspend alors l’exécution du logiciel et vous invite à suivre sa recommandation concernant le logiciel, ou à entreprendre une autre action.  

    |**Option de protection en temps réel** |**Fonction** |

    |-|-|  
    |Analyser tous les téléchargements|Cette option surveille les fichiers et programmes qui sont téléchargés, y compris les fichiers qui sont téléchargés automatiquement via Windows Internet Explorer et Microsoft Outlook® Express, comme les contrôles ActiveX® et les programmes d’installation de logiciel. Ces fichiers peuvent être téléchargés, installés ou exécutés par le navigateur lui-même. Des logiciels malveillants, notamment des virus, des logiciels espions et des autres logiciels potentiellement indésirables, peuvent être inclus dans ces fichiers et installés à votre insu.<br /><br /> Avec l’option de protection en temps réel, Windows Defender surveille votre ordinateur en permanence, et recherche les fichiers ou les programmes malveillants que vous pourriez avoir téléchargés. Avec cette fonctionnalité de surveillance, Windows Defender n’a pas besoin de ralentir votre navigation ou votre utilisation de la messagerie électronique en imposant une vérification des fichiers ou des programmes que vous voulez télécharger.|  
    |Surveiller l’activité des programmes et des fichiers sur votre ordinateur|Cette option surveille le démarrage de l’exécution des fichiers ou programmes sur votre ordinateur, et vous avertit des actions effectuées par ou sur ces fichiers et programmes. Ceci est important, car les logiciels malveillants peuvent exploiter les vulnérabilités des programmes que vous avez installés pour exécuter à votre insu des logiciels malveillants ou indésirables. Par exemple, un logiciel espion peut s’exécuter lui-même en arrière-plan quand vous démarrez un programme que vous utilisez fréquemment. Windows Defender surveille vos programmes et vous avertit s’il détecte une activité suspecte.|  
    |Activer la surveillance du comportement|Cette option surveille les ensembles de comportements de types suspects qui peuvent ne pas être détectés par les méthodes de détection antivirus traditionnelles.|  

    |Activer le système d’inspection du réseau|Cette option permet de protéger votre ordinateur contre les attaques « zero-day » de vulnérabilités connues, en réduisant le délai entre la découverte d’une vulnérabilité et l’application d’une mise à jour.|  

-   **Options d’analyse** : vous pouvez utiliser Windows Defender pour rechercher les menaces potentielles, notamment des virus, des logiciels espions et d’autres logiciels malveillants susceptibles de mettre votre ordinateur en danger. Il vous permet également de planifier des analyses régulières et de supprimer les logiciels malveillants qu'il détecte au cours d'une analyse.  

-   **Communauté Microsoft Active Protection Service** : cette communauté en ligne vous permet de savoir comment d’autres utilisateurs ont réagi face à des logiciels dont le niveau de dangerosité n’a pas encore été établi. Ces informations vous aident à choisir si vous devez autoriser ou non le logiciel sur votre ordinateur. De même, si vous participez, vos décisions sont ajoutées aux classements de la communauté afin d'aider d'autres personnes.  

##  <a name="how-can-i-tell-if-my-computer-is-infected-with-malicious-software"></a>Comment savoir si mon ordinateur est infecté par un logiciel malveillant ?  

 Une forme de logiciel malveillant, notamment des virus, des logiciels espions ou d’autres logiciels potentiellement indésirables, peut être présent sur votre ordinateur si :  

-   vous remarquez des barres d’outils, des liens ou des Favoris que vous n’avez pas explicitement ajoutés à votre navigateur web ;  

-   votre page d’accueil, le pointeur de votre souris ou le programme de recherche change de façon inattendue ;  

-   vous tapez l’adresse d’un site spécifique, comme un moteur de recherche, mais vous accédez à un autre site web sans avertissement ;  

-   des fichiers sont automatiquement supprimés de votre ordinateur ;  

-   votre ordinateur est utilisé pour attaquer d’autres ordinateurs ;  

-   vous voyez des fenêtres publicitaires, même si vous n’êtes pas sur Internet ;  

-   votre ordinateur fonctionne subitement plus lentement que d’habitude. Tous les problèmes de performances des ordinateurs ne sont pas provoqués par des logiciels malveillants, mais les logiciels malveillants, et notamment les logiciels espions, peuvent provoquer un changement notable.  

Des logiciels malveillants peuvent être présents sur votre ordinateur, même si vous ne voyez pas de symptômes. Ce type de logiciel peut collecter à votre insu des informations sur vous et votre ordinateur. Pour protéger votre confidentialité et votre ordinateur, vous devez exécuter en permanence Windows Defender ou Endpoint Protection.  

## <a name="how-can-i-find-the-version-of-windows-defender"></a>Comment puis-je trouver la version de Windows Defender ?
 Pour afficher la version de Windows Defender en cours d’exécution sur votre ordinateur, ouvrez Windows Defender (cliquez sur **Démarrer**, puis recherchez **Windows Defender**), cliquez sur **Paramètres** et faites défiler vers le bas les paramètres Windows Defender jusqu’à **Informations de version**.

##  <a name="what-should-i-do-if-windows-defender-or-endpoint-protection-detects-malicious-software-on-my-computer"></a>Que faire si Windows Defender ou Endpoint Protection détecte un logiciel malveillant sur mon ordinateur ?  

 Si Windows Defender détecte un logiciel malveillant ou un logiciel potentiellement indésirable sur votre ordinateur (en surveillant votre ordinateur via la protection en temps réel ou après une analyse), il vous informe de l’élément détecté en affichant un message de notification dans le coin inférieur droit de l’écran.  

 Le message de notification comprend un bouton **Nettoyer l'ordinateur** et un lien **Afficher les détails** qui vous permet d'afficher des informations complémentaires sur l'élément détecté. Cliquez sur le lien **Afficher les détails** pour ouvrir la fenêtre **Détails concernant les menaces potentielles** et obtenir des informations complémentaires sur l'élément détecté. Vous pouvez maintenant choisir quelle action appliquer à l'élément, ou cliquer sur **Nettoyer l'ordinateur**. Si vous avez besoin d’aide pour déterminer quelle action appliquer à l’élément détecté, utilisez le niveau d’alerte affecté à l’élément par Windows Defender pour vous guider (pour plus d’informations, consultez Comprendre les niveaux d’alerte).  

 Les niveaux d'alerte vous aident à choisir comment répondre aux virus, logiciels espions et autres logiciels potentiellement indésirables. Bien que Windows Defender vous conseille de supprimer tous les virus et logiciels malveillants, tous les logiciels qui sont signalés ne sont pas nécessairement malveillants ou indésirables. Les informations suivantes peuvent vous aider à prendre la bonne décision quand Windows Defender détecte un logiciel potentiellement indésirable sur votre ordinateur.  

 Selon le niveau d'alerte, vous pouvez appliquer une des trois actions suivantes à l'élément détecté :  

- **Supprimer** : cette action supprime de façon définitive le logiciel de votre ordinateur.  

- **Mettre en quarantaine** : cette action met le logiciel en quarantaine pour l’empêcher de s’exécuter. Quand Windows Defender met un logiciel en quarantaine, il le déplace à un autre emplacement de votre ordinateur, puis l’empêche de s’exécuter jusqu’à sa restauration ou sa suppression de l’ordinateur.  

- **Autoriser** : cette action ajoute le logiciel à la liste autorisée de Windows Defender et l’autorise à s’exécuter sur votre ordinateur. Windows Defender ne vous avertira plus des risques que le logiciel peut poser pour la confidentialité de vos données ou de votre ordinateur.  

  Si vous choisissez **Autoriser** pour un élément, par exemple un logiciel, Windows Defender ne vous avertira plus des risques que le logiciel peut poser pour la confidentialité de vos données ou de votre ordinateur. Par conséquent, ajoutez le logiciel à la liste des éléments autorisés uniquement si vous connaissez le logiciel et faites confiance à son éditeur.  

### <a name="how-to-remove-potentially-harmful-software"></a>Comment supprimer les logiciels potentiellement dangereux

Pour supprimer rapidement et facilement tous les éléments indésirables ou potentiellement dangereux détectés par Windows Defender, utilisez l’option **Nettoyer l’ordinateur** .  

1.  Quand vous voyez le message de notification que Windows Defender affiche dans la zone de notification après la détection de menaces potentielles, cliquez sur **Nettoyer l’ordinateur**.  

2.  Windows Defender supprime la ou les menaces potentielles, puis vous avertit quand le nettoyage de l’ordinateur est terminé.  

3.  Pour en savoir plus sur les menaces détectées, sélectionnez l'onglet **Historique** , puis choisissez **Tous les éléments détectés**.  

4.  Si vous ne voyez pas tous les éléments détectés, cliquez sur **Afficher les détails**. Si vous êtes invité à entrer un mot de passe d'administrateur ou à confirmer, tapez le mot de passe ou confirmez l'opération. Sur des systèmes exécutant Windows XP, vous devrez peut-être ouvrir une session en tant qu'administrateur sur cet ordinateur.  

> [!NOTE]  
>  Lors du nettoyage de l’ordinateur, quand c’est possible, Windows Defender supprime seulement la partie infectée d’un fichier, et non pas fichier entier.  

##  <a name="what-is-a-virus"></a>Qu’est-ce qu’un virus ?  
 Les virus informatiques sont des logiciels délibérément conçus pour interférer avec le fonctionnement de l’ordinateur, pour enregistrer, endommager ou supprimer des données, ou pour infecter d’autres ordinateurs via Internet. Les virus ralentissent souvent les ordinateurs et provoquent d’autres problèmes dans les processus.  

##  <a name="what-is-spyware"></a>Qu’est-ce qu’un logiciel espion ?  
 Un logiciel espion est un logiciel qui peut s’installer lui-même ou s’exécuter sur votre ordinateur sans votre accord ou sans vous fournir une indication ou un contrôle suffisant. Les logiciels espions peuvent ne pas montrer de symptômes une fois que votre ordinateur est infecté, mais de nombreux programmes malveillants ou indésirables peuvent affecter le fonctionnement de votre ordinateur. Par exemple, les logiciels espions peuvent surveiller votre comportement en ligne ou collecter des informations vous concernant (notamment les informations qui peuvent vous identifier ou d’autres informations sensibles), modifier des paramètres sur votre ordinateur ou le ralentir.  

##  <a name="whats-the-difference-between-viruses-spyware-and-other-potentially-harmful-software"></a>Quelle est la différence entre les virus, logiciels espions et d’autres logiciels potentiellement dangereux ?  
 Les virus et les logiciels espions sont installés à votre insu sur votre ordinateur, et ils sont potentiellement intrusifs et destructeurs. Ils ont également la possibilité de capturer des informations sur votre ordinateur, et d’endommager ou de supprimer ces informations. Ils peuvent nuire aux performances de votre ordinateur.  

 La principale différence entre les virus et logiciels espions est leur comportement sur votre ordinateur. Les virus, tels des organismes vivants, veulent infecter un ordinateur, se répliquer, puis se propager vers autant d’autres ordinateurs que possible. Un logiciel espion s’apparente plus à une « taupe », à savoir qu’il veut « pénétrer » dans votre ordinateur et y rester le plus longtemps possible pour pouvoir envoyer des informations importantes liées à votre ordinateur à une source externe.  

##  <a name="where-do-viruses-spyware-and-other-potentially-unwanted-software-come-from"></a>D’où viennent les virus, les logiciels espions et les autres logiciels potentiellement indésirables ?  
 Les logiciels indésirables, comme les virus, peuvent être installés par des sites web, ou par des programmes que vous téléchargez ou que vous installez en utilisant un CD, un DVD, un disque dur externe ou un périphérique. Les logiciels espions sont généralement installés via des logiciels gratuits, comme du partage de fichiers, des économiseurs d’écran ou des barres d’outils de recherche.  

##  <a name="can-i-get-malicious-software-without-knowing-it"></a>Puis-je recevoir un logiciel malveillant sans le savoir ?  
 Oui, certains logiciels malveillants peuvent être installés à partir d’un site web via un script ou un programme incorporé dans une page web. Certains logiciels malveillants ont besoin de votre aide pour s’installer. Ces logiciels utilisent des fenêtres publicitaires web ou des logiciels gratuits qui vous obligent à accepter un fichier téléchargeable. Cependant, si vous conservez Microsoft Windows® à jour et que vous ne réduisez pas le niveau de protection de vos paramètres de sécurité, vous pouvez réduire les risques d’infection.  

##  <a name="why-is-it-important-to-review-license-agreements-before-installing-software"></a>Pourquoi est-il important de lire les contrats de licence avant d’installer des logiciels ?  
 Quand vous visitez des sites web, n’acceptez pas automatiquement de télécharger ce que proposent les sites. Si vous téléchargez des logiciels gratuits, comme des programmes de partage de fichiers ou des économiseurs d’écran, lisez attentivement le contrat de licence. Recherchez les clauses stipulant que vous devez accepter les publicités et les fenêtres publicitaires de la société, ou spécifiant que le logiciel enverra certaines informations à l’éditeur du logiciel.  

##  <a name="whats-the-difference-between-endpoint-protection-and-windows-defender"></a>Quelle est la différence entre Endpoint Protection et Windows Defender ?  
 Endpoint Protection est un logiciel anti-programme malveillant, ce qui signifie qu’il est conçu pour détecter et aider à protéger votre ordinateur contre un large éventail de logiciels malveillants, notamment les virus, les logiciels espions et d’autres logiciels potentiellement indésirables. Windows Defender, qui est installé automatiquement avec le système d’exploitation Windows, est un logiciel qui détecte et arrête les logiciels espions.  

##  <a name="why-doesnt-windows-defender-detect-cookies"></a>Pourquoi Windows Defender ne détecte-t-il pas les cookies ?  
 Les cookies sont de petits fichiers texte que les sites web placent sur votre ordinateur pour enregistrer des informations sur vous et vos préférences. Les sites web utilisent des cookies pour vous offrir une navigation personnalisée et collecter des informations sur votre utilisation d’un site web. Windows Defender ne détecte pas les cookies, car il ne les considère pas comme une menace pour votre vie privée ou pour la sécurité de votre ordinateur. La plupart des navigateurs Internet vous permettent de bloquer les cookies.  

##  <a name="how-can-i-prevent-malware"></a>Comment me protéger contre les programmes malveillants ?  
 Aujourd’hui, deux des principales préoccupations des utilisateurs d’ordinateurs sont les virus et les logiciels espions. Dans les deux cas, si ceux-ci peuvent être un problème, vous pouvez vous défendre assez facilement contre eux avec un peu de prévention :  

-   Maintenez à jour les logiciels installés sur votre ordinateur et n’oubliez pas d’installer tous les correctifs logiciels. Mettez régulièrement à jour votre système d’exploitation.  

-   Vérifiez que votre logiciel antivirus et anti-logiciels espions, Windows Defender, utilise bien les dernières mises à jour contre les menaces potentielles (consultez Comment conserver à jour les définitions de virus et de logiciels espions ?). Vérifiez aussi que vous utilisez toujours la dernière version de Windows Defender.  

-   Téléchargez uniquement les mises à jour provenant de sources fiables. Pour les systèmes d’exploitation Windows, effectuez toujours les téléchargements depuis [Microsoft Update](http://go.microsoft.com/fwlink/?LinkID=96304) (http://go.microsoft.com/fwlink/?LinkID=96304). Pour les autres logiciels, utilisez toujours les sites web légitimes de l’entreprise ou de la personne qui les fournit.  

-   Si vous recevez un message électronique avec une pièce jointe et que vous n’êtes pas sûr de la source, vous devez la supprimer immédiatement. Ne téléchargez pas d’applications ou de fichiers provenant de sources inconnues, et soyez prudent quand vous échangez des fichiers avec d’autres utilisateurs.  

-   Installez et utilisez un pare-feu. Il est recommandé d’activer le Pare-feu Windows.  

##  <a name="what-are-virus-and-spyware-definitions"></a>Que sont les définitions de virus et de logiciels espions ?  
 Quand vous utilisez Windows Defender ou Endpoint Protection, il est important de disposer de définitions de virus et de logiciels espions à jour. Les définitions sont des fichiers qui agissent comme une encyclopédie constamment enrichie des menaces logicielles potentielles. Windows Defender ou Endpoint Protection utilise des définitions pour déterminer si un logiciel détecté est un virus, un logiciel espion ou un autre programme potentiellement indésirable. Il vous avertit ensuite des risques potentiels. Pour vous aider à tenir à jour vos définitions, Windows Defender ou Endpoint Protection utilise Microsoft Update pour installer automatiquement les nouvelles définitions dès qu’elles sont disponibles. Vous pouvez également configurer Windows Defender ou Endpoint Protection pour rechercher en ligne les définitions mises à jour avant d’effectuer une analyse.  

##  <a name="how-do-i-keep-virus-and-spyware-definitions-up-to-date"></a>Comment maintenir à jour les définitions de virus et de logiciels espions ?  
 Les définitions de virus et de logiciels espions sont des fichiers qui agissent comme une encyclopédie des logiciels malveillants connus, notamment les virus, les logiciels espions et d’autres logiciels potentiellement indésirables. Comme des logiciels malveillants ne cessent d’être développés, Windows Defender ou Endpoint Protection s’appuie sur des définitions à jour pour déterminer si le logiciel qui tente de s’installer, de s’exécuter ou de modifier des paramètres de votre ordinateur est un virus, un logiciel espion ou un autre logiciel potentiellement indésirable.  

### <a name="to-automatically-check-for-new-definitions-before-scheduled-scans-recommended"></a>Pour rechercher automatiquement les nouvelles définitions avant les analyses planifiées (recommandé)  

1.  Ouvrez le client Windows Defender ou Endpoint Protection en cliquant sur l’icône dans la zone de notification, ou en le lançant à partir du menu **Démarrer** .  

2.  Cliquez sur **Paramètres**, puis sur **Analyse planifiée**.  

3.  Vérifiez que la case **Rechercher les dernières définitions de virus et de logiciels espions avant d’exécuter une analyse planifiée** est cochée, puis cliquez sur **Enregistrer les modifications**. Si vous êtes invité à entrer un mot de passe d'administrateur ou à confirmer, tapez le mot de passe ou confirmez l'opération.  

### <a name="to-check-for-new-definitions-manually"></a>Pour rechercher les nouvelles définitions manuellement

 Windows Defender ou Endpoint Protection met automatiquement à jour les définitions de virus et de logiciels espions sur votre ordinateur. Si les définitions n’ont pas été mises à jour depuis plus de sept jours (par exemple, si vous n’avez pas allumé votre ordinateur pendant une semaine), Windows Defender ou Endpoint Protection vous avertit que les définitions sont obsolètes.  

1.  Ouvrez le client Windows Defender ou Endpoint Protection en cliquant sur l’icône dans la zone de notification, ou en le lançant à partir du menu **Démarrer** .  

2.  Pour rechercher manuellement les nouvelles définitions, cliquez sur l’onglet **Mettre à jour** , puis cliquez sur **Mettre à jour les définitions**.  

##  <a name="how-do-i-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Comment supprimer ou restaurer les éléments mis en quarantaine par Windows Defender ou Endpoint Protection ?  

 Quand Windows Defender or Endpoint Protection met le logiciel en quarantaine, il le déplace à un autre emplacement sur votre ordinateur, puis l’empêche de s’exécuter jusqu’à sa restauration ou sa suppression de l’ordinateur.  

 Pour toutes les étapes mentionnées dans cette procédure, si vous êtes invité à entrer un mot de passe d'administrateur ou à confirmer, tapez le mot de passe ou confirmez l'opération.  

###  <a name="to-remove-or-restore-items-quarantined-by-windows-defender-or-endpoint-protection"></a>Pour supprimer ou restaurer les éléments mis en quarantaine par Windows Defender ou Endpoint Protection


1.  Cliquez sur l’onglet **Historique** , sélectionnez **Éléments en quarantaine**, puis sélectionnez l’option **Éléments en quarantaine** .  

2.  Cliquez sur **Afficher les détails** pour afficher tous les éléments.  

3.  Passez chaque élément en revue, puis cliquez sur **Supprimer** ou **Restaurer** pour chacun d'entre eux. Pour supprimer tous les éléments mis en quarantaine de votre ordinateur, cliquez sur **Supprimer tout**.  

##  <a name="what-is-real-time-protection"></a>Qu’est-ce que la protection en temps réel ?  

 La protection en temps réel permet à Windows Defender d’analyser votre ordinateur en permanence et de vous avertir quand des menaces potentielles, notamment des virus et des logiciels espions, essayent de s’installer eux-mêmes ou de s’exécuter sur votre ordinateur. Comme cette fonctionnalité est un élément important de la façon dont Windows Defender contribue à protéger votre ordinateur, vérifiez que la protection en temps réel est toujours activée. Si la protection en temps réel est désactivée, Windows Defender vous avertit et change l’état de votre ordinateur en **Risqué**.  

 Chaque fois que la protection en temps réel détecte une menace ou une menace potentielle, Windows Defender affiche une notification. Vous pouvez maintenant choisir parmi les options suivantes :  

- Cliquez sur **Nettoyer l’ordinateur** pour supprimer l’élément détecté. Windows Defender va supprimer automatiquement l’élément de votre ordinateur.  

- Cliquez sur le lien **Afficher les détails** pour afficher la fenêtre Détails concernant les menaces potentielles, puis choisissez l’action à appliquer à l’élément détecté.  

  Vous pouvez choisir les logiciels et les paramètres à surveiller par Windows Defender, mais nous vous recommandons d’activer la protection en temps réel, ainsi que toutes ses options. Le tableau suivant explique les options disponibles.  

|||  
|-|-|  
|**Option de protection en temps réel**|**Fonction**|  
|Analyser tous les téléchargements|Cette option surveille les fichiers et programmes qui sont téléchargés, y compris les fichiers qui sont téléchargés automatiquement via Windows Internet Explorer et Microsoft Outlook® Express, comme les contrôles ActiveX® et les programmes d’installation de logiciel. Ces fichiers peuvent être téléchargés, installés ou exécutés par le navigateur lui-même. Des logiciels malveillants, notamment des virus, des logiciels espions et des autres logiciels potentiellement indésirables, peuvent être inclus dans ces fichiers et installés à votre insu.<br /><br /> Avec l’option de protection en temps réel, Windows Defender surveille votre ordinateur en permanence, et recherche les fichiers ou les programmes malveillants que vous pourriez avoir téléchargés. Cette fonctionnalité de surveillance signifie que Windows Defender n’a pas besoin de ralentir votre navigation ou votre utilisation de la messagerie électronique en imposant une vérification des fichiers ou des programmes que vous voulez télécharger.|  
|Surveiller l'activité des programmes et des fichiers sur votre ordinateur|Cette option surveille le démarrage de l’exécution des fichiers ou des programmes, puis vous avertit des actions qu’ils effectuent et des actions entreprises sur ces fichiers et programmes. Ceci est important, car les logiciels malveillants peuvent exploiter les vulnérabilités des programmes que vous avez installés pour exécuter à votre insu des logiciels malveillants ou indésirables. Par exemple, un logiciel espion peut s’exécuter lui-même en arrière-plan quand vous démarrez un programme que vous utilisez fréquemment. Windows Defender surveille vos programmes et vous avertit s’il détecte une activité suspecte.|  
|Activer l'analyse du comportement|Cette option surveille les ensembles de comportements de types suspects qui peuvent ne pas être détectés par les méthodes de détection antivirus traditionnelles.|  
|Activer le système NIS (Network Inspection System)|Cette option permet de protéger votre ordinateur contre les attaques « zero day » sur des vulnérabilités connues, en réduisant le délai entre la découverte d’une vulnérabilité et l’application d’une mise à jour.|  

### <a name="to-turn-off-real-time-protection"></a>Pour désactiver la protection en temps réel  

1.  Cliquez sur **Paramètres**, puis sur **Protection en temps réel.**  

2.  Désactivez les options de protection en temps réel que vous voulez désactiver, puis cliquez sur **Enregistrer les modifications**. Si vous êtes invité à entrer un mot de passe d'administrateur ou à confirmer, tapez le mot de passe ou confirmez l'opération.  

##  <a name="how-do-i-know-that-windows-defender-or-endpoint-protection-is-running-on-my-computer"></a>Comment savoir si Windows Defender ou Endpoint Protection est en cours d’exécution sur mon ordinateur ?  

 Après l’installation de Windows Defender sur votre ordinateur, vous pouvez fermer la fenêtre principale et laisser Windows Defender s’exécuter en mode silencieux en arrière-plan. Windows Defender va continuer à s’exécuter sur votre ordinateur, à le surveiller et à le protéger contre les menaces.  

 Vous savez que Windows Defender est en cours d’exécution chaque fois qu’il affiche des messages de notification dans la zone de notification. Ces notifications vous informent des menaces potentielles que Windows Defender a détectées.  

 Vous recevrez également d'autres types de notifications, par exemple si, pour une raison quelconque, la protection en temps réel a été désactivée, si vous n'avez pas mis à jour vos définitions de virus et de logiciels espions depuis un certain nombre de jours ou lorsque les mises à niveau du programme sont disponibles. Windows Defender affiche aussi brièvement une notification pour vous avertir qu’il analyse votre ordinateur.  

> [!TIP]
> 
> Si vous ne voyez pas l’icône de Windows Defender dans la zone de notification, cliquez sur la flèche dans cette zone pour afficher les icônes masquées, notamment l’icône de Windows Defender.  


 La couleur de l'icône dépend du statut actuel de l'ordinateur :  

-   Vert indique que le statut de votre ordinateur est « Protégé ».  

-   Jaune indique que le statut de votre ordinateur est « Potentiellement non protégé ».  

-   Rouge indique que le statut de votre ordinateur est « En danger ».  

##  <a name="how-to-set-up-windows-defender-or-endpoint-protection-alerts"></a>Comment configurer les alertes envoyées par Windows Defender ou Endpoint Protection ?  
 Quand Windows Defender est en cours d’exécution sur votre ordinateur, il vous avertit automatiquement s’il détecte des virus, des logiciels espions ou d’autres logiciels potentiellement indésirables. Vous pouvez également configurer Windows Defender pour vous avertir si vous exécutez un logiciel qui n’a pas encore été analysé. Vous pouvez également être alerté quand un logiciel modifie votre ordinateur.  

### <a name="to-set-up-alerts"></a>Pour configurer des alertes  

1.  Cliquez sur **Paramètres**, puis sur **Protection en temps réel.**  

2.  Vérifiez que la case **Activer la protection en temps réel (recommandé)** est cochée.  

3.  Cochez les cases situées à côté des options de protection en temps réel que vous voulez exécuter, puis cliquez sur **Enregistrer les modifications**. Si vous êtes invité à entrer un mot de passe d'administrateur ou à confirmer, tapez le mot de passe ou confirmez l'opération.  

### <a name="see-also"></a>Voir aussi  
 [Résolution des problèmes liés au client Windows Defender ou Endpoint Protection](troubleshoot-endpoint-client.md)   

 [Aide du client Endpoint Protection](endpoint-protection-client-help.md)
