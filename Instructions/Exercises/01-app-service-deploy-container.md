---
lab:
  title: "Déployer une application conteneurisée sur Azure\_App\_Service"
  description: "Découvrez comment déployer une application conteneurisée sur Azure\_App\_Service."
---

# Déployer une application conteneurisée sur Azure App Service

Dans cet exercice, vous déployez une application conteneurisée simple sur Azure App Service. 

Tâches effectuées dans cet exercice :

* Créer une ressource Azure App Service pour une application conteneurisée
* Affichage des résultats
* Nettoyer les ressources

Vous devriez terminer cet exercice en **15** minutes environ.

## Avant de commencer

Pour faire cet exercice, vous avez besoin de :

* Un abonnement Azure. Si vous n’en avez pas, vous pouvez [vous inscrire](https://azure.microsoft.com/).

## Créer une ressource d’application web

1. Dans votre navigateur, accédez au portail Azure [https://portal.azure.com](https://portal.azure.com) et connectez-vous en utilisant vos informations d’identification Azure.
1. Sélectionnez l’option **+ Créer une ressource** située dans le titre **Services Azure** en haut de la page d’accueil. 
1. Dans la barre de recherche **Rechercher dans la Place de marché**, entrez *Application web* et appuyez sur **Entrée** pour commencer la recherche.
1. Dans la vignette Application web, sélectionnez la liste déroulante **Créer**, puis sélectionnez **Application web**.

    ![Capture d’écran de la vignette Application web.](./media/01/create-web-app-tile.png)

La sélection de **Créer** ouvre un modèle avec quelques onglets pour renseigner des informations sur votre déploiement. Les étapes suivantes vous guident tout au long des modifications à apporter dans les onglets pertinents.

1. Renseignez l’onglet **Informations de base** en utilisant les informations contenues dans le tableau suivant :

    | Setting | Action |
    |--|--|
    | **Abonnement** | Conservez les valeurs par défaut. |
    | **Groupe de ressources** | Sélectionnez Créer nouveau, entrez `rg-WebApp`, puis sélectionnez OK. |
    | **Nom** | Entrez un nom de serveur, par exemple, `<your-initials>-containerwebapp`. Remplacez *\<your-initials>* par vos initiales ou une autre valeur. Le nom doit être unique, ce qui peut nécessiter quelques modifications. |
    | Curseur sous le paramètre **Nom** | Sélectionnez le curseur pour le désactiver. |
    | **Publier** | Sélectionnez l’option **Conteneur**. |
    | **Système d’exploitation** | Vérifiez que **Linux** est sélectionné. |
    | **Région** | Conservez la sélection par défaut ou choisissez une région proche de vous. |
    | **Plan Linux** | Conservez la sélection par défaut. |
    | **Plan tarifaire** | Sélectionnez la liste déroulante et choisissez le plan **F1 gratuit**. |

1. Sélectionnez ou accédez à l’onglet **Conteneur**, puis entrez les informations dans le tableau suivant :

    | Setting | Action |
    |--|--|
    | **Prise en charge de side-car** | Conservez la position désactivée par défaut. |
    | **Source d’image** | Sélectionnez **Autres registres de conteneurs**. |
    | **Type d’accès** | Conservez la sélection **Public** par défaut. |
    | **URL du serveur de Registre** | Saisissez `mcr.microsoft.com/k8se`. |
    | **Image et étiquette** | Saisissez `quickstart:latest`. |
    | **Commande de démarrage** | Laisser vide. |

1. Sélectionnez l’onglet **Vérifier + créer**.
1. Passez en revue vos sélections, puis sélectionnez le bouton **Créer**.

Le déploiement peut prendre quelques minutes. Une fois le déploiement terminé, sélectionnez le bouton **Accéder à la ressource**.

Maintenant que votre déploiement a terminé, il est temps d’afficher l’application web. Sélectionnez le lien vers votre application web située en regard du champ **Domaine par défaut** dans la section **Essentials**. Le lien ouvre le site dans un nouvel onglet.

>**Remarque :** l’exécution et l’affichage de l’application conteneurisée déployée dans le nouvel onglet peuvent prendre quelques minutes.

## Nettoyer les ressources

Maintenant que vous avez terminé l’exercice, vous devez supprimer les ressources cloud que vous avez créées pour éviter une utilisation inutile des ressources.

1. Accédez au groupe de ressources que vous avez créé et affichez le contenu des ressources utilisées dans cet exercice.
1. Dans la barre d’outils, sélectionnez **Supprimer le groupe de ressources**.
1. Entrez le nom du groupe de ressources et confirmez que vous souhaitez le supprimer.
