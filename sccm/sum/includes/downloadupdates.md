1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, puis sélectionnez le nœud **Mises à jour logicielles**.  

2.  Choisissez la mise à jour logicielle à télécharger selon l'une des méthodes suivantes :  

    -   Sélectionnez un ou plusieurs groupes de mise à jour logicielles dans le nœud **Groupes de mises à jour logicielles**. Ensuite, cliquez sur **Télécharger** dans le ruban.  

    -   Sélectionnez une ou plusieurs mises à jour logicielles dans le nœud **Toutes les mises à jour logicielles**. Ensuite, cliquez sur **Télécharger** dans le ruban.  

        > [!NOTE]  
        >  Dans le nœud **Toutes les mises à jour logicielles**, Configuration Manager affiche uniquement les mises à jour logicielles classées selon les critères **Critique** et **Sécurité** qui ont été publiées au cours des 30 derniers jours.  

        > [!TIP]  
        >  Cliquez sur **Ajouter des critères** pour filtrer les mises à jour logicielles affichées dans le nœud **Toutes les mises à jour logicielles**. Enregistrez les critères de recherche que vous utilisez souvent, puis gérez les recherches enregistrées sous l’onglet **Recherche**.  


3.  Dans la page **Package de déploiement** de l’Assistant Téléchargement des mises à jour logicielles, configurez les paramètres suivants :  

    -  **Sélectionner un package de déploiement**: choisissez ce paramètre pour sélectionner un package de déploiement existant pour les mises à jour logicielles incluses dans le déploiement.  

        > [!NOTE]  
        >  Les mises à jour logicielles que le site a déjà téléchargées dans le package de déploiement sélectionné ne sont pas retéléchargées.  

    -  **Créer un package de déploiement**: sélectionnez ce paramètre pour créer un package de déploiement pour les mises à jour logicielles incluses dans le déploiement. Configurez les paramètres suivants :  

        -   **Nom**: spécifie le nom du package de déploiement. Le package doit porter un nom unique qui décrit brièvement son contenu. Il est limité à 50 caractères.  

        -   **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description facultative est limitée à 127 caractères.    

        -   **Source du package**: spécifie l’emplacement des fichiers sources des mises à jour logicielles. Tapez un chemin réseau pour l’emplacement source, par exemple `\\server\sharename\path`, ou cliquez sur **Parcourir** pour trouver l’emplacement réseau. Créez le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

             - Vous ne pouvez pas utiliser l’emplacement spécifié comme source d’un autre package de déploiement de logiciels.  

             - Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Dans ce cas, copiez d’abord le contenu à partir de la source du package d’origine vers le nouvel emplacement source du package.  

             -  Le compte d’ordinateur du fournisseur SMS et l’utilisateur qui exécute l’Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations d’**Écriture** sur l’emplacement de téléchargement. Limitez l’accès à l’emplacement de téléchargement. Cette restriction réduit le risque que des personnes malveillantes falsifient les fichiers sources des mises à jour logicielles.  

        - **Activer la réplication différentielle binaire** : activez ce paramètre pour réduire le trafic réseau entre les sites. La réplication différentielle binaire met à jour uniquement le contenu qui a changé dans le package, au lieu de mettre à jour tout le contenu du package. Pour plus d’informations, consultez [Réplication différentielle binaire](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

4.  Dans la page **Points de distribution**, spécifiez les points de distribution ou les groupes de points de distribution où héberger les fichiers de mise à jour logicielle. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs). Cette page est disponible uniquement lorsque vous créez un nouveau package de déploiement de mise à jour logicielle.  

5.  La page **Paramètres de distribution** est disponible uniquement quand vous créez un package de déploiement de mises à jour logicielles. Spécifiez les paramètres suivants :  

    -   **Priorité de distribution**: utilisez ce paramètre pour spécifier la priorité de distribution pour le package de déploiement. La priorité de distribution s'applique lorsque le package de déploiement est envoyé aux points de distribution sur les sites enfants. Les packages de déploiement sont envoyés par ordre de priorité : haute, moyenne ou faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. S’il n’y a pas de backlog, le package est traité immédiatement, quelle que soit sa priorité. Par défaut, le site envoie les packages avec la priorité **Moyenne**.  

    -   **Activer pour la distribution à la demande** : utilisez ce paramètre pour activer la distribution de contenu à la demande sur les points de distribution configurés pour cette fonctionnalité et dans le groupe de limites actuel du client. Quand vous activez ce paramètre, le point de gestion crée un déclencheur afin que le gestionnaire de distribution distribue le contenu à tous ces points de distribution quand un client demande le contenu du package et que le contenu n’est disponible. Pour plus d’informations, consultez [Distribution de contenu à la demande](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).  

    -   **Paramètres du point de distribution préparé**: utilisez ce paramètre pour spécifier la manière dont vous voulez distribuer du contenu à des points de distribution préparés. Choisissez l'une des options suivantes :  

        -   **Télécharger automatiquement du contenu lorsque des packages sont affectés à des points de distribution**: utilisez ce paramètre pour ignorer les paramètres de préparation et distribuer du contenu au point de distribution.   

        -   **Télécharger uniquement les modifications de contenu vers le point de distribution**: utilisez ce paramètre pour préparer le contenu initial sur le point de distribution, puis distribuer les modifications apportées au contenu au point de distribution.  

        -   **Copier manuellement le contenu de ce package vers le point de distribution**: utilisez ce paramètre pour toujours préparer le contenu sur le point de distribution. Il s’agit de l’option par défaut.  

        Pour plus d’informations sur la préparation du contenu sur les points de distribution, consultez [Utiliser du contenu préparé](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  


6.  Dans la page **Emplacement de téléchargement**, spécifiez l’emplacement où Configuration Manager doit télécharger les fichiers sources des mises à jour logicielles. Utilisez l’une des options suivantes :  

    -   **Télécharger les mises à jour logicielles depuis Internet** : sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir de l’emplacement sur Internet. Il s’agit de l’option par défaut.  

    -   **Télécharger les mises à jour logicielles depuis un emplacement sur mon réseau** : sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un répertoire local ou d’un dossier partagé. Ce paramètre est utile quand l’ordinateur exécutant l’Assistant ne dispose d’aucun accès à Internet. Tout ordinateur connecté à Internet peut télécharger préalablement les mises à jour logicielles, puis les stocker à un emplacement sur le réseau local qui est accessible à partir de l’ordinateur exécutant l’Assistant.  


7.  Dans la page **Sélection de la langue**, sélectionnez les langues pour lesquelles le site télécharge les mises à jour logicielles sélectionnées. Le site télécharge uniquement ces mises à jour si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont pas propres à une langue sont toujours téléchargées. Par défaut, l’Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qu’une mise à jour logicielle ne prend pas en charge, le téléchargement de cette mise à jour échoue.  

8. Dans la page **Résumé**, vérifiez les paramètres que vous avez sélectionnés dans l’Assistant, puis cliquez sur **Suivant** pour télécharger les mises à jour logicielles.  

9. Dans la page **Dernière étape**, vérifiez que les mises à jour logicielles ont été téléchargées avec succès, puis cliquez sur **Fermer**.  
