---
title: Planification du déploiement de clients sur des ordinateurs Linux et UNIX
titleSuffix: Configuration Manager
description: Planifiez le déploiement de clients sur des ordinateurs Linux et UNIX dans System Center Configuration Manager.
ms.date: 08/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 44153689-70e8-42ad-9ae8-17ae35f6a2e3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7251ac6bf623236492f0843b8562a06e547c9cb1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32343682"
---
# <a name="planning-for-client-deployment-to-linux-and-unix-computers-in-system-center-configuration-manager"></a>Planification du déploiement de clients sur des ordinateurs Linux et UNIX dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez installer le client System Center Configuration Manager sur des ordinateurs exécutant Linux ou UNIX. Ce client est conçu pour les serveurs qui fonctionnent en tant qu'ordinateur de groupe de travail, et le client ne prend pas en charge l'interaction avec les utilisateurs connectés. Une fois que le logiciel client est installé et que le client a établi la communication avec le site Configuration Manager, vous gérez le client à l’aide de la console et des rapports Configuration Manager.  

> [!NOTE]  
>  Le client Configuration Manager pour les ordinateurs Linux et UNIX ne prend pas en charge les fonctionnalités de gestion suivantes :  
>   
>  -   Installation poussée du client  
> -   Déploiement du système d'exploitation  
> -   Déploiement d'application ; à la place, déployez des logiciels à l'aide de packages et programmes.  
> -   Inventaire logiciel  
> -   Mises à jour logicielles  
> -   Paramètres de conformité  
> -   Contrôle à distance  
> -   Gestion de l'alimentation  
> -   Vérification et correction de l'état du client  
> -   Gestion des clients basés sur Internet  

 Pour plus d’informations sur les distributions Linux et UNIX prises en charge et le matériel requis pour prendre en charge le client pour Linux et UNIX, consultez [Matériel recommandé pour System Center Configuration Manager](../../../../core/plan-design/configs/recommended-hardware.md).  

 Aidez-vous des informations de cet article pour planifier le déploiement du client Configuration Manager pour Linux et UNIX.  

##  <a name="BKMK_ClientDeployPrereqforLnU"></a> Conditions préalables pour le déploiement du client sur des serveurs Linux et UNIX  
 Utilisez les informations suivantes pour déterminer les conditions préalables pour que doivent avoir mis en place installer le client pour Linux et UNIX.  

###  <a name="BKMK_ClientDeployExternalforLnU"></a> Dépendances externes à Configuration Manager :  
 Les tableaux suivants décrivent les systèmes d'exploitation UNIX et Linux requis et les dépendances des packages.  

 **Red Hat Enterprise Linux Server 5.1 (Tikanga)**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliothèques standards C|2.5-12|  
|Openssl|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|0.9.8b-8.3.el5|  
|PAM|Modules d'authentification enfichables|0.99.6.2-3.14.el5|  

 **Red Hat Enterprise Linux Server 6**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliothèques standards C|2.12-1.7|  
|Openssl|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|1.0.0-4|  
|PAM|Modules d'authentification enfichables|1.1.1-4|  

 **Red Hat Enterprise Linux Server version 7**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliothèques standards C|2.17|  
|Openssl|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|1.0.1|  
|PAM|Modules d'authentification enfichables|1.1.1-4|  

 **Solaris 10 SPARC**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|Correctifs du système d'exploitation requis|Fuites de mémoire PAM|117463-05|  
|SUNWlibC|Compilateurs Sun Workshop fournis en standard libC (sparc)|5.10, REV=2004.12.22|  
|SUNWlibms|Bibliothèques Math & Microtasking (Usr) (sparc)|5.10, REV=2004.11.23|  
|SUNWlibmsr|Bibliothèques Math & Microtasking (Root) (sparc)|5.10, REV=2004.11.23|  
|SUNWcslr|Bibliothèques Core Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|SUNWcsl|Bibliothèques Core Solaris (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  
|Openssl|SUNopenssl-libraries (Usr)<br /><br /> Sun fournit les bibliothèques OpenSSL pour Solaris 10 SPARC. Elles sont fournies avec le système d'exploitation.|11.10.0,REV=2005.01.21.15.53|  
|PAM|Modules d'authentification enfichables<br /><br /> SUNWcsr, Core Solaris, (Root) (sparc)|11.10.0, REV=2005.01.21.15.53|  

 **Solaris 10 x86**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|Correctifs du système d'exploitation requis|Fuites de mémoire PAM|117464-04|  
|SUNWlibC|LibC regroupés de compilateurs Sun atelier (i386)|5.10,REV=2004.12.20|  
|SUNWlibmsr|Bibliothèques Math & Microtasking (Root) (i386)|5.10, REV=2004.12.18|  
|SUNWcsl|Solaris, (et les bibliothèques partagées) de base (i386)|11.10.0,REV=2005.01.21.16.34|  
|SUNWcslr|Bibliothèques de Solaris principales (racine) (i386)|11.10.0, REV=2005.01.21.16.34|  
|Openssl|Bibliothèques SUNWopenssl ; Bibliothèques OpenSSL (Usr) (i386)|11.10.0, REV=2005.01.21.16.34|  
|PAM|Modules d'authentification enfichables<br /><br /> Installation principale, Solaris, (Root)(i386)|11.10.0,REV=2005.01.21.16.34|  

 **Solaris 11 SPARC**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliothèques Math & Microtasking (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Bibliothèques OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  

 **Solaris 11 x86**  

|Package requis|Description|Version minimale|  
|----------------|-----------|---------------|  
|SUNWlibC|Sun Workshop Compilers Bundled libC|5.11, REV=2011.04.11|  
|SUNWlibmsr|Bibliothèques Math & Microtasking (Root)|5.11, REV=2011.04.11|  
|SUNWcslr|Core Solaris Libraries (Root)|11.11, REV=2009.11.11|  
|SUNWcsl|Core Solaris, (Shared Libs)|11.11, REV=2009.11.11|  
|SUNWcsr|Core Solaris, (Root)|11.11, REV=2009.11.11|  
|SUNWopenssl-libraries|Bibliothèques OpenSSL (Usr)|11.11.0,REV=2010.05.25.01.00|  


 **SUSE Linux Enterprise Server 10 SP1 (i586)**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|glibc-2,4-31,30|Bibliothèque standard partagée C|2.4-31.30|  
|OpenSSL|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|0.9.8a-18.15|  
|PAM|Modules d'authentification enfichables|0.99.6.3-28.8|  

 **SUSE Linux Enterprise Server 11 (i586)**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|glibc-2.9-13.2|Bibliothèque standard partagée C|2.9-13.2|  
|PAM|Modules d'authentification enfichables|pam-1.0.2-20.1|  

 **Universal Linux (Debian package) Debian, Ubuntu Server**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|libc6|Bibliothèque standard partagée C|2.3.6|  
|Openssl|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|0.9.8 ou 1.0|  
|PAM|Modules d'authentification enfichables|0.79-3|  

 **Universal Linux (RPM package) CentOS, Oracle Linux**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|glibc|Bibliothèque standard partagée C|2.5-12|  
|Openssl|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|0.9.8 ou 1.0|  
|PAM|Modules d'authentification enfichables|0.99.6.2-3.14|  


 **IBM AIX 6.1**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|Version du système d'exploitation|Version du système d'exploitation|AIX 6.1, technologie de tout niveau et tout Service Pack|  
|xlC.rte|XL C/C++ Runtime|9.0.0.5|  
|OpenSSL/openssl.base|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|0.9.8.4|  

 **IBM AIX 7.1 (Power)**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|Version du système d'exploitation|Version du système d'exploitation|AIX 7.1, technologie de tout niveau et tout Service Pack|  
|xlC.rte|XL C/C++ Runtime||  
|OpenSSL/openssl.base|Bibliothèque OpenSSL, protocole de communication réseau sécurisé||  


 **HP-UX 11i v3 IA64**  

|Package requis|Description|Version minimale|  
|----------------------|-----------------|---------------------|  
|HPUX11i-OE|HP-UX Foundation Operating Environment|B.11.31.0709|  
|OS-Core.MinimumRuntime.CORE-SHLIBS|Bibliothèques spécifiques de développement IA|B.11.31|  
|SysMgmtMin|Outils minimum de déploiement logiciel|B.11.31.0709|  
|SysMgmtMin.openssl|Bibliothèque OpenSSL, protocole de communication réseau sécurisé|A.00.09.08d.002|  
|PAM|Modules d'authentification enfichables|Sous HP-UX, PAM fait partie des composants centraux du système d’exploitation. Il n’y a pas d’autre dépendance.|  

 **Dépendances de Configuration Manager :** le tableau suivant répertorie les rôles de système de site qui prennent en charge des clients Linux et UNIX. Pour plus d’informations sur ces rôles de système de site, consultez [Déterminer les rôles de système de site pour les clients System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md).  

|Système de site Configuration Manager|Plus d'informations|  
|---------------------------------------|----------------------|  
|Point de gestion|Bien qu’un point de gestion ne soit pas nécessaire pour installer un client Configuration Manager pour Linux et UNIX, vous devez disposer d’un point de gestion pour transférer les informations entre les ordinateurs clients et les serveurs Configuration Manager. Sans point de gestion, vous ne pouvez pas gérer les ordinateurs clients.|  
|Point de distribution|Le point de distribution n’est pas nécessaire pour installer un client Configuration Manager pour Linux et UNIX. Toutefois, le rôle de système de site est requis si vous déployez des logiciels sur des serveurs Linux et UNIX.<br /><br /> Dans la mesure où le client Configuration Manager pour Linux et UNIX ne prend pas en charge le protocole SMB, les points de distribution que vous utilisez avec le client doivent prendre en charge la communication HTTP ou HTTPS.|  
|Point d’état de secours|Le point d’état de secours n’est pas nécessaire pour installer un client Configuration Manager pour Linux et UNIX. Toutefois, le point d’état de secours permet aux ordinateurs du site Configuration Manager d’envoyer des messages d’état quand ils ne peuvent pas communiquer avec un point de gestion. Client peut également envoyer leur état d'installation pour le point d'état de secours.|  

 **Pare-feu exigences**: Assurez-vous que les pare-feu ne bloquent pas les communications sur les ports que vous spécifiez en tant que ports de demande client. Le client pour Linux et UNIX communique directement avec les points de gestion, les points de distribution et les points d’état de secours.  

 Pour plus d’informations sur les ports de demande et de communication client, consultez  [Configurer le client pour Linux et UNIX pour qu’il localise des points de gestion](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigClientMP).  

##  <a name="BKMK_PlanningforCommunicationsforLnU"></a> Planification des communications entre les approbations de forêts pour les serveurs Linux et UNIX  
 Les serveurs Linux et UNIX que vous gérez avec Configuration Manager fonctionnent comme des clients de groupe de travail et nécessitent des configurations similaires à celles des clients Windows situés dans un groupe de travail. Pour plus d’informations sur les communications à partir d’ordinateurs qui se trouvent dans des groupes de travail, consultez la section [Communications dans les forêts Active Directory](../../../../core/plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest) dans la rubrique [Communications entre points de terminaison dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

###  <a name="BKMK_ServiceLocationforLnU"></a> Emplacement du service par le client pour Linux et UNIX  
 La tâche de recherche d'un serveur de système de site qui fournit le service aux clients est appelée emplacement de service. Contrairement à un client fonctionnant sous Windows, le client pour Linux et UNIX n'utilise pas Active Directory pour l'emplacement de service. De plus, le client Configuration Manager pour Linux et UNIX ne prend pas en charge une propriété cliente qui spécifie le suffixe de domaine d’un point de gestion. Au lieu de cela, le client a eu connaissance des serveurs de système de site supplémentaires qui fournissent des services aux clients à partir d'un point de gestion connu que vous affectez lorsque vous installez le logiciel client.  

 Pour plus d’informations sur l’emplacement de service, consultez la section [Emplacement du service et façon dont les clients déterminent leur point de gestion attribué](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) dans la rubrique [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

##  <a name="BKMK_SecurityforLnU"></a> Planification de la sécurité et des certificats pour les serveurs Linux et UNIX  
 Pour des communications sécurisées et authentifiées avec les sites Configuration Manager, le client Configuration Manager pour Linux et UNIX utilise le même modèle de communication que le client Configuration Manager pour Windows.  

 Quand vous installez le client pour Linux et UNIX, vous pouvez lui affecter un certificat PKI qui lui permet d’utiliser le protocole HTTPS pour communiquer avec les sites Configuration Manager. Si vous n'affectez pas un certificat PKI, le client crée un certificat auto-signé et communique uniquement par HTTP.  

 Les clients qui sont fournis un certificat PKI lorsqu'ils installent utilisent HTTPS pour communiquer avec les points de gestion. Lorsqu'un client est impossible de trouver un point de gestion qui prend en charge le protocole HTTPS, il revient pour utiliser HTTP avec le certificat PKI fourni.  

 Lorsqu'un client Linux ou UNIX utilise un certificat PKI vous n'êtes pas obligé de les approuver. Quand un client utilise un certificat auto-signé, passez en revue les paramètres de hiérarchie pour l’approbation du client dans la console Configuration Manager. Si la méthode d'approbation du client n'est pas **Approuver automatiquement tous les ordinateurs (non recommandés)**, vous devez approuver manuellement le client.  

 Pour plus d’informations sur l’approbation manuelle du client, consultez la section [Gérer les clients à partir du nœud Appareils](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode) dans la rubrique [Comment gérer les clients dans System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

 Pour plus d’informations sur l’utilisation des certificats dans Configuration Manager, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

###  <a name="BKMK_AboutCertsforLnU"></a> À propos des certificats pour les serveurs Linux et UNIX  
 Le client Configuration Manager pour Linux et UNIX utilise un certificat auto-signé ou un certificat PKI X.509, comme les clients Windows. Aucune modification des exigences PKI pour les systèmes de site Configuration Manager n’est nécessaire quand vous gérez des clients Linux et UNIX.  

 Les certificats utilisés pour les clients Linux et UNIX qui communiquent avec les systèmes de site Configuration Manager doivent être au format PKCS#12 (Public Key Certificate Standard). De plus, vous devez connaître le mot de passe pour pouvoir l’indiquer au client quand vous spécifiez le certificat PKI.  

 Le client Configuration Manager pour Linux et UNIX ne prend en charge qu’un seul certificat PKI. Il ne prend pas en charge plusieurs certificats. Ainsi, les critères de sélection de certificat que vous configurez pour un site Configuration Manager ne s’appliquent pas.  

###  <a name="BKMK_ConfigCertsforLnU"></a> Configuration de certificats pour les serveurs Linux et UNIX  
 Pour configurer l’utilisation des communications HTTPS par un client Configuration Manager pour les serveurs Linux et UNIX, vous devez configurer le client pour qu’il utilise un certificat PKI au moment de son installation. Vous ne pouvez pas configurer un certificat avant l'installation du logiciel client.  

 Lorsque vous installez un client qui utilise un certificat PKI, vous utilisez le paramètre de ligne de commande **- /usepkicert** pour spécifier l'emplacement et le nom d'un fichier PKCS #12 qui contient le certificat PKI. En outre, vous devez utiliser le paramètre de ligne de commande **- certpw** pour spécifier le mot de passe du certificat.  

 Si vous ne spécifiez pas **- /usepkicert**, le client génère un certificat auto-signé et tente de communiquer avec les serveurs de système de site via le protocole HTTP uniquement.  

##  <a name="BKMK_NoSHA-256"></a> À propos des systèmes d’exploitation Linux et UNIX qui ne prennent pas en charge SHA-256  
 Les systèmes d’exploitation Linux et UNIX suivants, pris en charge en tant que clients pour Configuration Manager, ont été publiés avec des versions d’OpenSSL qui ne prennent pas en charge SHA-256 :  

-   Solaris Version 10 (SPARC/x86)  


 Pour gérer ces systèmes d’exploitation avec Configuration Manager, vous devez installer le client Configuration Manager pour Linux et UNIX avec un commutateur de ligne de commande qui indique au client d’ignorer la validation de SHA-256. Les clients Configuration Manager qui s’exécutent sur ces versions de système d’exploitation fonctionnent dans un mode moins sécurisé que les clients qui prennent en charge SHA-256. Ce mode de fonctionnement moins sécurisé a le comportement suivant :  

-   Les clients ne valident pas la signature de serveur de site associée qu'ils demandent à partir d'un point de gestion de stratégie.  

-   Les clients ne valident pas le hachage des packages qu'ils téléchargent à partir d'un point de distribution.  

> [!IMPORTANT]  
>  Le **ignoreSHA256validation** option permet d'exécuter le client pour les ordinateurs Linux et UNIX en mode moins sécurisé. Cela est voulu pour une utilisation sur des plates-formes plus anciennes qui n'inclut pas de prise en charge de l'algorithme SHA-256. Ceci est un remplacement de la sécurité et n'est pas recommandé par Microsoft, mais est pris en charge pour une utilisation dans un environnement de centre de données sécurisé et fiable.  

 Durant l’installation du client Configuration Manager pour Linux et UNIX, le script d’installation vérifie la version du système d’exploitation. Par défaut, si la version du système d’exploitation est identifiée comme ayant été publiée sans une version d’OpenSSL prenant en charge SHA-256, l’installation du client Configuration Manager se solde par un échec.  

 Pour installer le client Configuration Manager sur les systèmes d’exploitation Linux et UNIX qui n’ont pas été publiés avec une version d’OpenSSL prenant en SHA-256, vous devez utiliser le commutateur de ligne de commande **ignoreSHA256validation**. Quand vous utilisez cette option de ligne de commande sur un système d’exploitation Linux ou UNIX applicable, le client Configuration Manager ignore la validation de SHA-256. Une fois l’installation effectuée, le client n’utilise pas SHA-256 pour signer les données qu’il envoie aux systèmes de site via HTTP. Pour plus d’informations sur la configuration des clients Linux et UNIX pour utiliser des certificats, consultez [Planification de la sécurité et des certificats pour les serveurs Linux et UNIX](#BKMK_SecurityforLnU) dans cette rubrique. Pour plus d’informations sur l’utilisation de SHA-256, consultez la section [Configurer la signature et le chiffrement](../../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) dans la rubrique [Configurer la sécurité dans System Center Configuration Manager](../../../../core/plan-design/security/configure-security.md).  

> [!NOTE]  
>  L'option de ligne de commande **ignoreSHA256validation** est ignorée sur les ordinateurs qui exécutent une version de Linux et UNIX publié avec les versions d'OpenSSL qui prennent en charge SHA-256.  
