---
title: Configurer les paramètres Microsoft Edge
titleSuffix: Configuration Manager
description: Configurer les paramètres du navigateur web Microsoft Edge sur les clients Windows 10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/28/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 81bd0a59a24cab446668911f714548581c1347df
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343768"
---
# <a name="configure-microsoft-edge-settings-in-system-center-configuration-manager"></a>Configurer les paramètres Microsoft Edge dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!-- 1357310 -->
À compter de la version 1802, pour les clients qui utilisent le navigateur web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) sur des clients Windows 10, créez une stratégie de paramètres de conformité Configuration Manager pour configurer plusieurs paramètres Microsoft Edge. 

Cette stratégie s’applique uniquement aux clients sur Windows 10, versions 1703 ou ultérieures. <!--511552-->


## <a name="policy-settings"></a>Paramètres de stratégie
Actuellement, cette stratégie comprend les paramètres suivants :
- **Définir Microsoft Edge comme navigateur par défaut** : configure le paramètre d’application Windows 10 par défaut avec le navigateur web Microsoft Edge
- **Autoriser la barre d’adresse déroulante** : nécessite Windows 10, version 1703 ou ultérieure. Pour plus d’informations, consultez la section [Stratégie de navigateur AllowAddressBarDropdown](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).
- **Autoriser la synchronisation des favoris entre les navigateurs Microsoft** : nécessite la version 1703 ou une version ultérieure de Windows 10. Pour plus d’informations, consultez la section [Stratégie de navigateur SyncFavoritesBetweenIEAndMicrosoftEdge](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).
- **Autoriser l’effacement des données de navigation à la fermeture** : nécessite la version 1703 ou une version ultérieure de Windows 10. Pour plus d’informations, consultez la section [Stratégie de navigateur ClearBrowsingDataOnExit](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).
- **Autoriser les en-têtes Do Not Track** : pour plus d’informations, consultez la section [Stratégie de navigateur AllowDoNotTrack](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).
- **Autoriser le remplissage automatique** : pour plus d’informations, consultez la section [Stratégie de navigateur AllowAutofill](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).
- **Autoriser les cookies** : pour plus d’informations, consultez la section [Stratégie de navigateur AllowCookies](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).
- **Autoriser le bloqueur de fenêtres publicitaires** : pour plus d’informations, consultez la section [Stratégie de navigateur AllowPopups](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).
- **Autoriser les suggestions de recherche dans la barre d’adresses** : pour plus d’informations, consultez la section [Stratégie de navigateur AllowSearchSuggestionsinAddressBar](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).
- **Autoriser l’envoi du trafic intranet vers Internet Explorer** : pour plus d’informations, consultez la section [Stratégie de navigateur SendIntranetTraffictoInternetExplorer](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).
- **Autoriser le gestionnaire de mot de passe** : pour plus d’informations, consultez la page [Stratégie de navigateur AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).
- **Autoriser les Outils de développement** : pour plus d’informations, consultez la page [Stratégie de navigateur AllowDeveloperTools](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).
- **Autoriser les extensions** : pour plus d’informations, consultez la page [Stratégie de navigateur AllowExtensions](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).



## <a name="create-the-microsoft-edge-browser-profile"></a>Créer le profil de navigateur Microsoft Edge

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Actifs et conformité**. Développez **Paramètres de conformité** et sélectionnez le nouveau nœud **Profils de navigateur Microsoft Edge**. Cliquez sur l’option du ruban **Créer une stratégie de navigateur Microsoft Edge**.
2. Donnez un **Nom** à la stratégie et, éventuellement, une **Description** ; ensuite, cliquez sur **Suivant**.
3. Sur la page **Paramètres**, remplacez la valeur des paramètres à inclure dans cette stratégie par **Configuré**, puis cliquez sur **Suivant**.
4. Sur la page **Plateformes prises en charge**, sélectionnez les architectures et les versions de système d’exploitation auxquelles s’applique cette stratégie, puis cliquez sur **Suivant**. 
5. Effectuez toutes les étapes de l'Assistant.



## <a name="deploy-the-policy"></a>Déployer la stratégie

1. Sélectionnez votre stratégie et cliquez sur l’option de ruban **Déployer**.
2. Cliquez sur **Parcourir** et sélectionnez le regroupement d'utilisateurs ou d'appareils sur lequel la stratégie sera déployée. 
3. Sélectionnez d’autres options si nécessaire. 
    a. Générez des alertes lorsque la stratégie n’est pas conforme. 
    b. Définissez la planification selon laquelle le client évaluera la conformité à cette stratégie.
4. Cliquez sur **OK** pour créer le déploiement.



## <a name="next-steps"></a>Étapes suivantes

Comme toute stratégie de paramètres de conformité, le client corrige les paramètres selon le calendrier spécifié par vos soins. [Effectuez le monitoring et créez des rapports sur la conformité des appareils](/sccm/compliance/deploy-use/monitor-compliance-settings) dans la console de Configuration Manager.
