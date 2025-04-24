---
lab:
  title: "Échanger des emplacements de déploiement dans Azure\_App\_Service"
  description: "Découvrez comment échanger des emplacements de déploiement dans Azure\_App\_Service. Dans cet exercice, vous déployez une application simple sur App\_Service, apportez une petite modification à l’application et la déployez sur un emplacement de préproduction. Enfin, vous échangez les emplacements afin que l’application mise à jour soit en production."
---

# Échanger des emplacements de déploiement dans Azure App Service

Dans cet exercice, vous allez déployer un site HTML+CSS de base sur Azure App Service avec la commande **az webapp up** d’Azure CLI. Ensuite, vous mettez à jour le code et déployez la modification sur un emplacement de préproduction. Enfin, vous échangez les emplacements.

Tâches effectuées dans cet exercice :

* Télécharger et déployer l’exemple d’application dans Azure App Service.
* Créer un emplacement de déploiement intermédiaire.
* Apporter une modification à l’exemple d’application et la déployer sur l’emplacement de préproduction.
* Échanger les emplacements de préproduction et de production par défaut pour déplacer les modifications vers l’emplacement de production.

Cet exercice devrait prendre environ **20** minutes.

## Avant de commencer

Pour faire cet exercice, vous avez besoin de :

* Un abonnement Azure. Si vous n’en avez pas, vous pouvez vous inscrire à un [https://azure.microsoft.com/](https://azure.microsoft.com/).

## Télécharger et déployer l’exemple d’application

Dans cette section, vous téléchargez l’exemple d’application et définissez des variables pour faciliter l’entrée des commandes, puis créez une ressource Azure App Service et déployez un site HTML statique à l’aide de commandes Azure CLI.

1. Dans votre navigateur, accédez au portail Azure [https://portal.azure.com](https://portal.azure.com) et connectez-vous en utilisant vos informations d’identification Azure.

1. Cliquez sur le bouton **[\>_]** à droite de la barre de recherche, en haut de la page, pour créer un Cloud Shell dans le portail Azure, puis sélectionnez un environnement ***Bash***. Cloud Shell fournit une interface de ligne de commande dans un volet situé en bas du portail Azure.

    > **Note** : si vous avez déjà créé un Cloud Shell qui utilise un environnement *PowerShel*, basculez-le vers ***Bash***.

1. Dans la barre d’outils Cloud Shell, dans le menu **Paramètres**, sélectionnez **Accéder à la version classique** (cela est nécessaire pour utiliser l’éditeur de code).

1. Exécutez la commande **git** suivante pour cloner l’exemple de référentiel d’applications :

    ```bash
    git clone https://github.com/Azure-Samples/html-docs-hello-world.git
    ```

1. Définissez des variables destinées à contenir les noms du groupe de ressources et de l’application en exécutant les commandes suivantes. Notez la valeur de l’**appName** qui s’affiche après l’exécution des commandes, vous en aurez besoin plus loin dans cet exercice.

    ```bash
    resourceGroup=rg-mywebapp

    appName=mywebapp$RANDOM
    echo $appName
    ```

1. Accédez au répertoire qui contient l’exemple de code et exécutez la commande **az webapp up**. **Remarque :** l’exécution de cette commande peut prendre quelques minutes.

    ```bash
    cd html-docs-hello-world

    az webapp up -g $resourceGroup -n $appName --sku P0V3 --html
    ```

    Maintenant que votre déploiement a terminé, il est temps d’afficher l’application web.

1. Dans le portail Azure, accédez à l’application web que vous avez déployée. Vous pouvez entrer le nom que vous avez noté précédemment dans la barre de recherche **Rechercher des ressources, des services et des documents (G + /)** et sélectionner la ressource dans la liste.

1. Sélectionnez le lien vers votre application web située dans le champ **Domaine par défaut** dans la section **Essentials**. Le lien ouvre le site dans un nouvel onglet.

## Déployer du code mis à jour sur un emplacement de déploiement

Dans cette section, vous créez un emplacement de déploiement, modifiez le code HTML dans l’application et déployez le code mis à jour sur le nouvel emplacement de déploiement.

### Créer un emplacement de déploiement 

1. Revenez à l’onglet avec le portail Azure et Cloud Shell.

1. Entrez la commande suivante dans Cloud Shell pour créer un emplacement de déploiement nommé *intermédiaire*.

    ```bash
    az webapp deployment slot create -n $appName -g $resourceGroup --slot staging
    ```

1. Attendez la fin de la commande, puis sélectionnez **Déploiement > Emplacements de déploiement** dans le menu de gauche pour afficher les emplacements de déploiement de votre application web. Notez que *-intermédiaire* est ajouté au nom de votre application web dans le nom du nouvel emplacement.

### Mettre à jour le code et déployer sur l’emplacement de préproduction

1. Dans Cloud Shell, saisissez `code index.html` pour ouvrir l’éditeur. Dans l’étiquette de titre `<h1>`, remplacez *Azure App Service - Sample Static HTML Site* par *Azure App Service Updated* ou par la valeur de votre choix.

1. Utilisez la commande **ctrl-s** pour enregistrer et la commande **ctrl-q** pour quitter.

1. Dans Cloud Shell, exécutez la commande suivante pour créer un fichier zip du projet mis à jour. Un fichier zip ou un fichier de ressource d’application web (WAR) est nécessaire pour l’étape suivante.

    ```bash
    zip -r stagingcode.zip .
    ```

1. Exécutez la commande suivante dans Cloud Shell pour déployer vos mises à jour sur l’emplacement de préproduction.

    ```bash
    az webapp deploy -g $resourceGroup -n $appName --src-path ./stagingcode.zip --slot staging
    ```

1. Sélectionnez **Déploiement > Emplacements de déploiement** dans le menu de gauche de votre application web, puis sélectionnez l’emplacement de préproduction que vous avez créé précédemment.

1. Sélectionnez le lien dans le champ **Domaine par défaut** dans la section **Essentials**. Le lien ouvre le site web pour l’emplacement de préproduction dans un nouvel onglet.

## Échanger les emplacements de préproduction et de production

Vous pouvez effectuer un échange dans le portail Azure avec l’option **Échanger** de la barre d’outils. L’option **Échanger** s’affiche dans la barre d’outils si vous sélectionnez **Vue d’ensemble** ou **Déploiement > Emplacements de déploiement** dans le menu de gauche.

1. Dans le portail Azure, sélectionnez **Échanger** dans la barre d’outils pour ouvrir le panneau **Échanger**.

1. Passez en revue les paramètres dans le panneau Échanger. La **Source** doit afficher l’emplacement de **préproduction** et la **Cible** doit afficher l’emplacement de production par défaut.

    ![Capture d’écran du panneau Échanger.](./media/02/app-service-swap-panel.png)

1. Sélectionnez **Démarrer l’échange** et attendez que l’opération soit terminée. Vous pouvez suivre l’achèvement dans le panneau **Notifications** que vous pouvez ouvrir en sélectionnant l’icône en forme de cloche en haut du portail.

1. Pour vérifier l’échange, accédez à l’application web que vous avez déployée. Entrez le nom de l’application web que vous avez créé précédemment (par exemple, *mywebapp12360*) dans la barre de recherche **Rechercher des ressources, des services et des documents (G + /)**, puis sélectionnez la ressource dans la liste.

1. Sélectionnez le lien vers votre application web située dans le champ **Domaine par défaut** dans la section **Essentials**. Le lien ouvre le site (emplacement de production) dans un nouvel onglet.

1. Vérifiez vos modifications ; vous devrez peut-être actualiser la page pour qu’elles apparaissent.

## Nettoyer les ressources

Maintenant que vous avez terminé l’exercice, vous devez supprimer les ressources cloud que vous avez créées pour éviter une utilisation inutile des ressources.

1. Accédez au groupe de ressources que vous avez créé et affichez le contenu des ressources utilisées dans cet exercice.
1. Dans la barre d’outils, sélectionnez **Supprimer le groupe de ressources**.
1. Entrez le nom du groupe de ressources et confirmez que vous souhaitez le supprimer.
