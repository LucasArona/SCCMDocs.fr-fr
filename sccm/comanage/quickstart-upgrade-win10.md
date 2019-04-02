---
title: Mettre à niveau Windows 10
titleSuffix: Configuration Manager
description: Mettre à niveau les appareils vers Windows 10 version 1709 ou ultérieure, nécessaire pour la cogestion
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754887"
---
# <a name="upgrade-windows-10-for-co-management"></a>Mettre à niveau Windows 10 pour la cogestion

Lorsque vous préparez l’intégration de votre organisation à la cogestion, se mettre à jour peut être un obstacle non négligeable pour certains clients. La cogestion nécessite [Windows 10 version 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) ou ultérieure. Une fois que vous mettez à jour Windows et configurez l’inscription automatique, vos clients sont automatiquement inscrits à la cogestion.

Dans la vidéo suivante, le program manager senior, Rob York, et le directeur du marketing produit, Locky Ainley, parlent et font la démonstration de la mise à niveau de Windows 10 pour la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Pourquoi une mise à niveau ?

Entre autres améliorations de la plateforme, Windows 10 version 1709 et ultérieure prend en charge l’inscription automatique. Ce comportement permet d’inscrire automatiquement un appareil à Intune quand il est joint à Azure Active Directory (Azure AD). 

Pour plus d’informations, consultez [Activer l’inscription automatique Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Marche à suivre

Voici quelques astuces que nous avons relevées en aidant des milliers de clients à se mettre à jour rapidement :

- Utilisez des déploiements par phases pour déployer cette mise à niveau pour les bonnes personnes au bon moment. Pour plus d’informations, voir [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).  

- Utilisez la pré-mise en cache pour réduire les temps d’attente des utilisateurs. Pour plus d’informations, consultez la section [Configurer le contenu précache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

- Utilisez le modèle de séquence de tâches de mise à niveau sur place par défaut. Ensuite, configurez vos étapes de pré- et post-mise à niveau et les actions en cas d’échec. Pour plus d’informations, consultez [Étapes de séquence de tâches recommandées pour le post-traitement](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#recommended-task-sequence-steps-for-post-processing).  

- Si votre environnement compte du personnel très mobile, Configuration Manager prend en charge la mise à niveau sur place sur la passerelle de gestion cloud (CMG). Cette fonctionnalité vous permet de mettre à niveau vos clients Windows 10 s’ils sont basés sur Internet. Pour plus d’informations sur la passerelle CMG, consultez [](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).  

- Proposez une option d’adhésion à la cogestion pour les utilisateurs qui souhaitent être des utilisateurs précoces. Cette approche accélère le processus d’adoption initiale. En identifiant ces personnes à l’avance, vous pouvez assurer une bonne couverture les premiers jours du déploiement. Vous recevez aussi la validation et le feedback des utilisateurs qui sont contents du changement et intéressés par des versions plus fréquentes. Les programmes d’adoption précoce suscitent l’intérêt dans les nouvelles technologies et prennent de l’ampleur au fil du temps.  


## <a name="case-studies"></a>Études de cas

Microsoft IT a déployé Windows 10 pour 96 000 utilisateurs distribués chez Microsoft. Le déploiement comprenait à la fois les utilisateurs distants et les utilisateurs sur le réseau d’entreprise. Le déploiement a duré neuf semaines. Pour plus d’informations sur cette expérience, consultez [Déploiement de Windows 10 chez Microsoft avec une mise à niveau sur place](https://www.microsoft.com/download/details.aspx?id=50377).  

Un important éditeur de logiciels européen utilise un groupe d’utilisateurs précoces. Après les premiers tests et pilotages des groupes, environ 2 000 employés reçoivent la première mise à jour, les mises à niveau et les logiciels. Ce groupe comprend le personnel informatique et les volontaires qui ont choisi d’adhérer. Ce niveau d’engagement avec ses utilisateurs lui donne une plus grande confiance lors des tests et plus de crédibilité quand les déploiements en masse commencent.



## <a name="contact-fasttrack"></a>Contacter FastTrack

Si vous avez besoin d’assistance concernant votre mise à niveau Windows 10 à n’importe quelle étape de la procédure, accédez à [Microsoft FastTrack](https://Microsoft.com/FastTrack/), connectez-vous, puis demandez de l’aide. 

Pour plus d’informations, consultez [Obtenir de l’aide de FastTrack](/sccm/comanage/quickstart-fasttrack). 

