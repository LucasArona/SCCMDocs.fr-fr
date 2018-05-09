---
title: Paramètres Windows Hello Entreprise
titleSuffix: Configuration Manager
description: Découvrez comment intégrer Windows Hello Entreprise dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7471b408fbc8ce55e443873e4662c2ed87410c3a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager-hybrid"></a>Paramètres Windows Hello Entreprise dans System Center Configuration Manager (hybride)

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager permet d’intégrer Windows Hello Entreprise (anciennement Microsoft Passport pour Windows), qui constitue une méthode alternative de connexion pour les appareils Windows 10. Hello Entreprise utilise Active Directory ou un compte Azure Active Directory pour remplacer un mot de passe, une carte à puce ou une carte à puce virtuelle.  

Hello Entreprise vous permet d’utiliser un **geste utilisateur** pour vous connecter, au lieu d’un mot de passe. Un geste utilisateur peut être un simple code confidentiel, une authentification biométrique ou un appareil externe tel qu’un lecteur d’empreintes digitales.  

 Configuration Manager s’intègre avec Windows Hello Entreprise de deux manières :  

-   Vous pouvez utiliser Configuration Manager pour contrôler les gestes que les utilisateurs peuvent et ne peuvent pas utiliser pour se connecter.  

-   Vous pouvez stocker des certificats d’authentification dans le fournisseur de stockage de clés Windows Hello Entreprise. Pour plus d’informations, consultez [Profils de certificat](create-pfx-certificate-profiles.md).  

- Vous pouvez déployer des stratégies Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine qui exécutent le client Configuration Manager. Cette configuration est décrite dans la section [Configurer Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Lorsque vous utilisez Configuration Manager avec Intune (hybride), vous pouvez configurer ces paramètres sur les appareils Windows 10 et Windows 10 Mobile, mais pas sur les appareils joints à un domaine qui exécutent le client Configuration Manager.   

Pour en savoir plus sur la configuration des paramètres de Windows Hello Entreprise, voir [Paramètres Windows Hello Entreprise dans System Center Configuration Manager](../../protect/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurer les paramètres Windows Hello Entreprise (hybride)  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Services cloud** > **Abonnements Microsoft Intune**.  

3.  Dans la liste, sélectionnez votre abonnement Microsoft Intune, puis, sous l’onglet **Accueil** , dans le groupe **Abonnement** , cliquez sur **Configurer des plateformes** > **Windows (MDM)**.  

4.  Sous l’onglet **Windows Hello Entreprise** de la boîte de dialogue **Propriétés de l’abonnement Microsoft Intune** , choisissez parmi les valeurs suivantes celles que vous voulez appliquer à tous les appareils Windows 10 et Windows 10 Mobile inscrits :  

    -   **Désactiver Windows Hello Entreprise sur les appareils inscrits** ou **Activer Windows Hello Entreprise sur les appareils inscrits** : active ou désactive l’utilisation de Windows Hello Entreprise sur tous les appareils Windows 10 et Windows 10 Mobile inscrits.  

    -   **Utiliser un module de plateforme sécurisée (TPM)** : une puce de module de plateforme sécurisée (TPM) fournit une couche supplémentaire de sécurité des données. Choisissez l'une des valeurs suivantes :  

        -   **Requis** (par défaut) : seuls les appareils avec un module de plateforme sécurisée accessible peuvent configurer Windows Hello Entreprise.  

        -   **Préféré** : les appareils tentent d’abord d’utiliser un module de plateforme sécurisée. Si ce n’est pas possible, ils peuvent utiliser un chiffrement logiciel.  

    -   **Exiger une longueur minimale du code confidentiel** : spécifiez le nombre minimal de caractères nécessaire pour le code confidentiel Windows Hello Entreprise. Vous devez utiliser au moins 4 caractères (la valeur par défaut est 6 caractères).  

    -   **Exiger une longueur maximale du code confidentiel** : spécifiez le nombre maximal de caractères autorisé pour le code confidentiel Windows Hello Entreprise. Vous pouvez entrer jusqu’à 127 caractères.  

    -   **Exiger des minuscules dans le code confidentiel** : spécifie si des lettres minuscules doivent être utilisées dans le code confidentiel Windows Hello Entreprise. Choisissez parmi :  

        -   **Autorisé** : les utilisateurs peuvent utiliser des minuscules dans leur code confidentiel.  

        -   **Requis** : les utilisateurs doivent inclure au moins un caractère en minuscule dans leur code confidentiel.  

        -   **Non autorisé** (par défaut) : les utilisateurs ne doivent pas utiliser de caractères minuscules dans leur code confidentiel.  

    -   **Exiger des majuscules dans le code confidentiel** : spécifie si des lettres majuscules doivent être utilisées dans le code confidentiel Windows Hello Entreprise. Choisissez parmi :  

        -   **Autorisé** : les utilisateurs peuvent utiliser des majuscules dans leur code confidentiel.  

        -   **Requis** : les utilisateurs doivent inclure au moins un caractère en majuscule dans leur code confidentiel.  

        -   **Non autorisé** (par défaut) : les utilisateurs ne doivent pas utiliser de caractères majuscules dans leur code confidentiel.  

    -   **Exiger des caractères spéciaux** : spécifie l’utilisation de caractères spéciaux dans le code confidentiel. Choisissez parmi :  

        -   **Autorisé** : les utilisateurs peuvent utiliser des caractères spéciaux dans leur code confidentiel.  

        -   **Requis** : les utilisateurs doivent inclure au moins un caractère spécial dans leur code confidentiel.  

        -   **Non autorisé** (par défaut) : les utilisateurs ne doivent pas utiliser de caractères spéciaux dans leur code confidentiel (ce comportement vaut également si le paramètre n’est pas configuré).  

         Les caractères spéciaux sont les suivants : **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **Exiger un délai d’expiration du code confidentiel (en jours)**  : spécifie le nombre de jours avant de devoir modifier le code confidentiel de l’appareil. La valeur par défaut est 41 jours.  

    -   **Empêcher la réutilisation de codes confidentiels précédents** : utilisez ce paramètre pour limiter la réutilisation des codes confidentiels précédemment utilisés. Par défaut, les 5 derniers codes confidentiels utilisés ne peuvent pas être réutilisés.  

    -   **Activer les mouvements biométriques** : permet d’utiliser l’authentification biométrique, telle que la reconnaissance des visages ou les empreintes digitales, à la place d’un code confidentiel pour Windows Hello Entreprise. Les utilisateurs doivent toujours configurer un code confidentiel professionnel en cas d’échec de l’authentification biométrique.  

         Si vous choisissez **Activé**, Windows Hello Entreprise autorise l’authentification biométrique.  Si vous choisissez **Désactivé**, Windows Hello Entreprise empêche l’authentification biométrique (pour tous les types de compte).  

    -   **Utiliser la détection d’usurpation avancée, si disponible** : détermine si la détection d’usurpation avancée est utilisée sur les appareils qui la prennent en charge.  

         Si cette option est définie sur **Activé**, Windows nécessite que tous les utilisateurs utilisent la détection d’usurpation pour les fonctions de reconnaissance faciale, si disponible.  

    -   **Utiliser Remote Passport** : si cette option a la valeur **Activé**, les utilisateurs peuvent utiliser un appareil Remote Passport comme appareil mobile pour l’authentification d’ordinateur du bureau. L’ordinateur de bureau doit être joint à Azure Active Directory, et l’appareil mobile doit être configuré avec un code confidentiel Windows Hello Entreprise.  

5.  Lorsque vous avez terminé, cliquez sur **OK**.  

### <a name="see-also"></a>Voir aussi  
 [Protéger les données et l’infrastructure des sites avec System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Gérer la vérification d’identité à l’aide de Windows Hello Entreprise](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport).  
