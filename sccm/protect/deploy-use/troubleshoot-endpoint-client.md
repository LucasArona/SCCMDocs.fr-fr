---
title: Résolution des problèmes du client Windows Defender ou Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment résoudre les problèmes liés à Windows Defender et Endpoint Protection.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2a8f0e51e5808a691251e4d9acf38d70f2874508
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351579"
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Résolution des problèmes du client Windows Defender ou Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*


Si vous rencontrez des problèmes avec Windows Defender ou Endpoint Protection, contactez votre administrateur de sécurité pour obtenir du support. Vous pouvez également tenter de résoudre les problèmes suivants :  

-   [Mettre à jour Windows Defender ou Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
-   [Démarrage du service Windows Defender ou Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
-   [Problèmes de connexion Internet](#internet-connection-issues)  
-   [Impossible de remédier à une menace détectée](#detected-threat-cant-be-remediated)  
-   [Installer le client Endpoint Protection](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Mettre à jour Windows Defender ou Endpoint Protection  
 Windows Defender ou Endpoint Protection fonctionne automatiquement avec Microsoft Update pour garantir que vos définitions de virus et de logiciels espions sont à jour.  

 **Symptômes**  

 Cet article traite des problèmes courants liés aux mises à jour automatiques, notamment les situations suivantes :  

-   Vous voyez des messages d’erreur indiquant que les mises à jour ont échoué.  

-   Quand vous recherchez les mises à jour, vous recevez un message d’erreur indiquant que les mises à jour des définitions de virus et de logiciels espions ne peut pas être recherchées, téléchargées ou installées.  

-   Même si vous êtes connecté à Internet, les mises à jour échouent.  

-   Les mises à jour ne sont pas installées automatiquement comme planifié.  

 **Cause**  

 Les causes les plus courantes des problèmes de mise à jour sont des problèmes de connectivité Internet. Cependant, si vous savez que vous êtes connecté à Internet dans la mesure où vous pouvez accéder à d’autres sites web, le problème peut être dû à des conflits avec vos paramètres de Windows Internet Explorer.  

> [!IMPORTANT]  
>  Vous devez quitter Internet Explorer pour effectuer ces étapes. Par conséquent, imprimez-les, notez-les ou copiez-les dans un autre fichier, puis ajoutez cette rubrique à vos favoris pour y accéder ultérieurement.  

### <a name="step-1-reset-your-internet-explorer-settings"></a>Étape 1 : Réinitialiser vos paramètres Internet Explorer  

1.  Quittez tous les programmes ouverts, y compris Internet Explorer.  

    > [!NOTE]  
    >  La réinitialisation de ces paramètres dans Internet Explorer supprime vos fichiers temporaires, vos cookies, votre historique de navigation et vos mots de passe en ligne. Vos favoris ne sont cependant pas supprimés.  

2.  Cliquez sur **Démarrer** et recherchez **inetcpl.cpl**, puis appuyez sur **Entrée**.  

3.  Dans la boîte de dialogue **Options Internet** , cliquez sur l’onglet **Avancé** .  

4.  Sous **Réinitialiser les paramètres d’Internet Explorer**, cliquez sur **Réinitialiser**, puis cliquez à nouveau sur **Réinitialiser** .  

5.  Attendez qu’Internet Explorer ait terminé de réinitialiser les paramètres, puis cliquez sur **OK**.  

6.  Ouvrez Internet Explorer.  

7.  Ouvrez Microsoft Security Essentials, cliquez sur l’onglet **Mettre à jour** , puis cliquez sur **Mettre à jour**.  

8.  Si le problème persiste, passez à l’étape suivante.  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>Étape 2 : Définir Internet Explorer comme navigateur par défaut  

1.  Quittez tous les programmes ouverts, y compris Internet Explorer.  

2.  Cliquez sur **Démarrer** et recherchez **inetcpl.cpl**, puis appuyez sur **Entrée**.  

3.  Dans la boîte de dialogue **Options Internet** , cliquez sur l’onglet **Programmes** .  

4.  Sous **Navigateur Web par défaut**, cliquez sur **Par défaut**.  

5.  Cliquez sur **OK**.  

6.  Ouvrez Windows Defender ou Endpoint Protection. Cliquez sur l'onglet **Mise à jour** , puis sur **Mettre à jour**.  

7.  Si le problème persiste, passez à l’étape suivante.  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Étape 3 : Vérifier que la date et l’heure sont correctement définies sur votre ordinateur  

1.  Ouvrez Windows Defender ou Endpoint Protection.  

2.  Si le message d’erreur que vous avez reçu contient le code 0x80072f8f, le problème est probablement dû à une valeur de date ou d’heure incorrecte sur votre ordinateur.  

3.  Pour réinitialiser la date ou l’heure de votre ordinateur, suivez les étapes décrites dans [Résoudre les problèmes liés aux raccourcis Bureau rompus et aux tâches courantes de maintenance du système](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579).  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>Étape 4 : Renommer le dossier Distribution de logiciels sur votre ordinateur  

1. Arrêtez le service Mises à jour automatiques  

    1.  Cliquez sur **Démarrer** et recherchez **services.msc**, puis cliquez sur **OK**.  

    2.  Cliquez avec le bouton droit de la souris sur **Service Mises à jour automatiques**, puis cliquez sur **Arrêter**.  

    3.  Réduisez le composant logiciel enfichable Services.  

2.  Renommez le répertoire **SoftwareDistribution** comme suit :  

    1.  Cliquez sur **Démarrer** et recherchez  **cmd**, puis cliquez sur **OK**.  

    2.  Tapez **cd %windir%**, puis appuyez sur **Entrée**.  

    3.  Tapez **ren SoftwareDistribution SDTemp**, puis appuyez sur **Entrée**.  

    4.  Tapez **exit**, puis appuyez sur **Entrée**.  

3.  Démarrez le service Mises à jour automatiques comme suit :  

    1.  Agrandissez le composant logiciel enfichable Services.  

    2.  Cliquez avec le bouton droit de la souris sur **Service Mises à jour automatiques**, puis cliquez sur **Démarrer**.  

    3.  Fermez la fenêtre du composant logiciel enfichable Services.  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Étape 5 : Réinitialiser le moteur de mise à jour antivirus de Microsoft sur votre ordinateur  

1.  Cliquez sur **Démarrer** et recherchez  **cmd**, cliquez sur **OK**, cliquez sur **Invite de commande**, puis sélectionnez **Exécuter en tant qu’administrateur**.  

2.  Dans la fenêtre **Invite de commande** , tapez les commandes suivantes en appuyant sur **Entrée** après chacune d’elles.  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **Quitter**  

3.  Redémarrez votre ordinateur.  

4.  Ouvrez Windows Defender ou  
          Endpoint Protection, cliquez sur l’onglet **Mise à jour**, puis cliquez sur **Mettre à jour**.  

5.  Si le problème persiste, passez à l’étape suivante.  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>Étape 6 : Installer manuellement les mises à jour des définitions de virus et de logiciels espions  

-   Si vous exécutez un système d’exploitation Windows 32 bits, téléchargez les dernières mises à jour manuellement à l’adresse [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342).  

-   Si vous exécutez un système d’exploitation Windows 64 bits, téléchargez les dernières mises à jour manuellement à l’adresse [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341).  

-   Cliquez sur **Exécuter**. Les dernières mises à jour sont installés manuellement sur votre ordinateur.  


### <a name="step-7-contact-support"></a>Étape 7 : Contacter le support technique  

-   Si les étapes ne résolvent pas le problème, contactez le support technique. Pour plus d’informations, consultez le [Support technique](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174).  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>Démarrage du service Windows Defender ou Endpoint Protection  
 **Symptôme**  

 Vous recevez un message qui vous informe que **Windows Defender ou Endpoint Protection ne surveille pas votre ordinateur car le service du programme s’est arrêté. Nous vous conseillons de le redémarrer immédiatement.** 

 **Solution**  

### <a name="step-1-restart-your-computer"></a>Étape 1 : Redémarrer votre ordinateur  

-   Fermez toutes les applications et redémarrez l'ordinateur.  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>Étape 2: Vérifier que le service « Windows Defender » ou « Endpoint Protection » est défini sur « Automatique » et qu’il est démarré  

1.  Cliquez sur **Démarrer** et recherchez **services.msc**, puis appuyez sur **Entrée**.  

2.  Recherchez **Service anti-programme malveillant de Microsoft**. Cliquez avec le bouton droit de la souris et sélectionnez **Propriétés** ou double-cliquez pour ouvrir le service.  

3.  Vérifiez que**Type de démarrage**est défini sur**Automatique**.  

4.  Cliquez sur le bouton **Démarrer** pour lancer le service. Si le bouton **Démarrer** n'est pas disponible, cliquez sur le bouton **Arrêter** , puis sur le bouton **Démarrer** pour relancer le service.  

5.  N'oubliez pas de noter toutes les erreurs pouvant apparaître lors de cette procédure et d'envoyer votre problème en ligne en incluant les informations sur l'erreur.  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>Étape 3 : Supprime les programmes de sécurité Internet existants  

1.  Cliquez sur **Démarrer** et recherchez **appwiz.cpl**, puis appuyez sur **Entrée**.  

2.  Dans la liste des programmes installés, désinstallez tous les programmes de sécurité Internet tiers.*  

3.  Redémarrez votre ordinateur, puis réessayez d’installer Windows Defender ou  
          Endpoint Protection.  

> [!NOTE]  
>  Certaines applications de sécurité Internet ne se désinstallent pas complètement. Vous devrez peut-être télécharger et exécuter un utilitaire de nettoyage approprié afin de supprimer complètement l'application de sécurité précédente.  

> [!CAUTION]  
>  Lorsque vous supprimez les programmes de sécurité Internet, votre ordinateur n'est plus protégé. Si vous rencontrez des problèmes pour installer   
>       Endpoint Protection après avoir supprimé des programmes de sécurité Internet existants, contactez le support de Windows Defender ou  
>       Endpoint Protection en envoyant un dossier en ligne (pour plus d’informations, consultez [Guide pratique pour envoyer un dossier en ligne](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx)).  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>Étape 4 : Désinstaller/réinstaller Endpoint Protection  

1.  Cliquez sur **Démarrer** et recherchez **appwiz.cpl**, puis appuyez sur **Entrée**.  

2.  Dans la liste des programmes installés, cliquez sur **Endpoint Protection**, puis désinstallez-le.  

3.  Si vous y êtes invité, redémarrez l’ordinateur, puis essayez de réinstaller Endpoint Protection.  

##  <a name="internet-connection-issues"></a>Problèmes de connexion Internet  
 Pour que votre ordinateur reçoive bien les dernières mises à jour de Windows Update, vous devez être connecté à Internet.  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>Étape 1 : Vérifier que votre ordinateur est connecté à Internet  

1.  Cliquez sur **Démarrer**et recherchez **ncpa.cpl**, puis appuyez sur **Entrée**.  

2.  Cliquez avec le bouton droit sur le nom de la connexion, puis cliquez sur **État**.  

3.  Si votre ordinateur est connecté, dans Windows XP, l’état de la connexion peut être **Connectée**, **Activée**ou **Authentification réussie** . Dans Windows Vista et Windows 7, l’état de **IPv4** est **Internet**.  

4.  Si votre ordinateur n’est pas connecté, cliquez avec le bouton droit sur le nom de la connexion, puis cliquez sur **Connecter**, **Activer**, **Authentifier**ou **Réparer**.  

### <a name="step-3-restart-your-computer"></a>Étape 3 : Redémarrer votre ordinateur  

-   Fermez tous les programmes ouverts et redémarrez votre ordinateur.  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>Étape 4 : Si vous ne pouvez toujours pas vous connecter à Internet, vérifier vos connexions  

1.  Si vous utilisez une connexion d’accès à distance, vérifiez que le cordon téléphonique de la prise murale et de votre modem est correctement branché.  

2.  Si vous utilisez un modem câble, vérifiez que la connexion du câble au modem et la connexion du modem à votre ordinateur sont correctement branchées.  

3.  Si vous utilisez un modem câble ou un routeur DSL, vérifiez que les connexions au routeur et à l’ordinateur sont correctement branchées. Déconnectez et arrêtez le routeur et le modem. Attendez quelques minutes, branchez d’abord le modem, patientez une minute, puis branchez le routeur et redémarrez votre ordinateur.  

##  <a name="detected-threat-cant-be-remediated"></a>Impossible de remédier à une menace détectée  
 Quand Windows Defender ou Endpoint Protection détecte une menace potentielle dissimulée dans un fichier compressé avec une extension .zip ou dans un partage réseau, il tente d’y remédier en supprimant la menace ou en la plaçant en quarantaine.  

### <a name="remove-or-scan-the-file"></a>Supprimer ou analyser le fichier  

-   Si la menace détectée se trouve dans un fichier .zip, accédez à ce fichier, puis supprimez-le, ou analysez-le en cliquant avec le bouton droit sur le fichier et en sélectionnant **Analyser avec Windows Defender** ou **Analyser avec Endpoint Protection**. Si Windows Defender ou Endpoint Protection détecte d’autres menaces dans le fichier, il vous en avertit et vous permet de choisir une action appropriée.  

-   Si la menace détectée se trouve dans un partage réseau, accédez au partage réseau et analysez-la en cliquant avec le bouton droit sur le fichier et en sélectionnant **Analyser avec Windows Defender** ou **Analyser avec Endpoint Protection**. Si Windows Defender ou Endpoint Protection détecte d’autres menaces dans le partage réseau, il vous en avertit et vous permet de choisir une action appropriée.  

-   Si vous n'êtes pas certain de l'origine du fichier, la meilleure solution est de lancer une analyse complète sur votre ordinateur. Une analyse complète peut prendre un certain temps, mais elle permet à Windows Defender ou à Endpoint Protection de rechercher la source de l’infection et de la nettoyer.  

##  <a name="install-the-endpoint-protection-client"></a>Installer le client Endpoint Protection  

> [!NOTE]  
>  Windows Defender est installé avec le système d’exploitation sur les PC Windows 10.  

 **Symptômes**  

 L'installation a échoué pour une raison inconnue ou un message d'erreur s'affiche avec un code d'erreur de type 0x80070643, 0X8007064A, 0x8004FF2E, 0x8004FF01, 0x8004FF07, 0x80070002, 0x8007064C, 0x8004FF00, 0x80070001, 0x80070656, 0x8004FF40, 0xC0000156, 0x8004FF41 0x8004FF0B, 0x8004FF11, 0x80240022, 0x8004FF04, 0x80070660, 0x800106B5, 0x80070715, 0x80070005, 0x8004EE00, 0x8007003, 0x800B0100, 0x8007064E ou 0x8007007E.  

 Si votre ordinateur exécute Windows XP Service Pack 2 (SP2), un ou plusieurs des messages suivants peuvent s'afficher :  

-   L'exécution de l'Assistant Installation ne peut pas se terminer car un package cumulatif pour le gestionnaire de filtres est manquant.  

-   KB914882 Erreur d'installation : le programme d'installation ne peut pas mettre à jour les fichiers Windows XP car la langue installée sur le système et celle de la mise à jour ne correspondent pas.  

 **Cause**  

 Il est impossible d’installer Endpoint Protection sur un ordinateur exécutant d’autres programmes de sécurité. Parfois, même si vous supprimez ces autres programmes de sécurité, ils ne se désinstallent pas complètement. Vous devez exécuter une version authentique du système d’exploitation Windows pour installer Endpoint Protection.  

 **Solution**  

> [!IMPORTANT]  
>  Vous devrez redémarrer votre ordinateur au cours de la procédure de résolution de ce problème. Créez un signet pour cette page (ajoutez-la à vos Favoris) pour pouvoir retrouver cette rubrique plus facilement, ou imprimez-la pour vous y référer ultérieurement.  

### <a name="step-1-remove-any-existing-security-programs"></a>Étape 1 : Supprimer les programmes de sécurité existants  
**Endpoint Protection uniquement**

1.  Désinstallez complètement les programmes de sécurité Internet existants.  

2.  Redémarrez votre ordinateur.  

3.  Installez à nouveau Endpoint Protection. Si le problème n'est pas résolu, passez à l'étape suivante.  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>Étape 2 : Vérifier que le service Windows Installer est en cours d’exécution  

1.  Cliquez sur **Démarrer** et recherchez **services.msc**, puis appuyez sur **Entrée**.  

2.  Cliquez avec le bouton droit de la souris sur **Windows Installer**, puis cliquez sur **Démarrer**. Si le bouton **Démarrer** n'est pas disponible et que les options **Arrêter** et **Redémarrer** sont disponibles, vous pouvez en déduire que le service est déjà lancé.  

3.  Dans la page **Services** , dans le menu **Fichier** , cliquez sur **Quitter**.  

4.  Cliquez sur **Démarrer** et recherchez **invite de commandes**. Cliquez avec le bouton droit de la souris sur **Invite de commande**, puis cliquez sur **Exécuter en tant qu'administrateur**.  

5.  Tapez **MSIEXEC /REGSERVER**, puis appuyez sur **Entrée**.  

    > [!NOTE]  
    >  Aucun message ne s'affiche pour indiquer si la commande a réussi ou échoué.  

6.  Installez à nouveau Endpoint Protection. Si le problème n'est pas résolu, passez à l'étape suivante.  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>Étape 3 : Démarrer Windows en mode de démarrage sélectif  

1.  Cliquez sur **Démarrer** et recherchez **msconfig**, puis appuyez sur **Entrée**.  

2.  Sur l'onglet **Général** , cliquez sur **Démarrage Sélectif**, puis désactivez la case à cocher **Charger les éléments de démarrage** .  

3.  Sous l'onglet **Services** , cochez la case **Masquer tous les services Microsoft** , puis décochez toutes les cases correspondant aux services restants dans la liste.  

4.  Cliquez sur **OK**, puis sur **Redémarrer** pour relancer l'ordinateur.  

5.  Essayez d’installer à nouveau Endpoint Protection.  



### <a name="see-also"></a>Voir aussi  
 [Forum aux questions sur le client Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Aide du client Endpoint Protection](../../protect/deploy-use/endpoint-protection-client-help.md)
