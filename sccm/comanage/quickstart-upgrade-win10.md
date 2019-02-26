---
title: Mettre à niveau Windows 10
titleSuffix: Configuration Manager
description: Mettre à niveau les appareils Windows 10 version 1709 ou ultérieure, qui est requis pour la cogestion
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0815a974f3b1f29f664a2948eed33de24c6ecff3
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754887"
---
# <a name="upgrade-windows-10-for-co-management"></a>Mise à niveau Windows 10 pour la cogestion

Lorsque vous travaillez à l’intégration de votre organisation à la cogestion, obtenir actuelle est un obstacle important pour certains clients. Cogestion nécessite [Windows 10 version 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) ou version ultérieure. Une fois que vous mettez à jour de Windows et configurez l’inscription automatique, vos clients sont automatiquement inscrits à la cogestion.

Dans la vidéo suivante, responsable de programme senior Rob York produit marketing Ainley Locky manager discuter et démonstration de la mise à niveau vers Windows 10 pour la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Pourquoi mettre à niveau ?

Parmi les autres améliorations de plate-forme, Windows 10 version 1709 et versions ultérieure prend en charge l’inscription automatique. Ce comportement permet à un périphérique inscrire automatiquement à Intune quand il joint à Azure Active Directory (Azure AD). 

Pour plus d’informations, consultez [activer Windows 10 l’inscription automatique](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Marche à suivre

Voici quelques conseils que nous avons appris à partir de l’aider des milliers de clients rapidement actuel :

- Utilisez des déploiements par phases pour déployer cette mise à niveau aux bonnes personnes à droite fois. Pour plus d’informations, voir [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Utilisez la mise en cache pour réduire le temps d’attente utilisateur. Pour plus d’informations, consultez la section [Configurer le contenu précache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Utilisez le modèle de séquence de tâches de mise à niveau sur place par défaut. Puis configurez vos étapes de pré et post-mise à niveau et les actions d’échec. Pour plus d’informations, consultez [recommandé des étapes de séquence de tâches pour le post-traitement](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Si votre environnement comporte un personnel hautement mobile, Configuration Manager prend en charge la mise à niveau sur place sur la passerelle de gestion cloud (CMG). Cette fonctionnalité vous permet de mettre à niveau vos clients Windows 10 lorsqu’ils sont basés sur internet. Pour plus d’informations sur la passerelle CMG, consultez [ ](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Offre un option d’adhésion dans cogestion pour les utilisateurs qui souhaitent être précoces. Cette approche accélère l’adoption initiale. En identifiant ces personnes à l’avance, vous pouvez effectuer bien sûr une bonne couverture dans les premiers jours d’un déploiement. Vous recevez également la validation et les commentaires des utilisateurs qui sont heureux de modification et intéressé par des versions plus fréquentes. Programmes d’adoption précoce susciter l’intérêt dans les nouvelles technologies et taille augmente au fil du temps.  


## <a name="case-studies"></a>Études de cas

Microsoft IT a déployé Windows 10 pour les utilisateurs distribués 96,000 chez Microsoft. Le déploiement inclus à la fois les utilisateurs distants et les utilisateurs sur le réseau d’entreprise. Le déploiement s’est terminé en neuf semaines. Pour plus d’informations sur leur expérience, consultez [déploiement de Windows 10 chez Microsoft en tant qu’une mise à niveau sur place](https://www.microsoft.com/download/details.aspx?id=50377).  

Un fabricant de logiciels d’envergure utilise avec succès un plus réceptifs. Après avoir testé initiale et groupes de pilotage, environ 2 000 employés recevoir la première mise à jour, les mises à niveau et les logiciels. Ce groupe inclut le personnel informatique et participer volontaires. Ce niveau d’engagement avec leurs utilisateurs leur donne un niveau supérieur de confiance lors du test et plus de crédibilité lors des déploiements en masse commencent.



## <a name="contact-fasttrack"></a>Contactez FastTrack

Si vous avez besoin d’aide avec votre mise à niveau Windows 10 à tout moment dans le processus, accédez à [Microsoft FastTrack](https://Microsoft.com/FastTrack/), connectez-vous, puis demander une assistance. 

Pour plus d’informations, consultez [obtenir de l’aide de FastTrack](/sccm/comanage/quickstart-fasttrack). 

