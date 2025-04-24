---
lab:
  title: "Créer des ressources Azure\_Cosmos\_DB avec for NoSQL à l’aide de .NET"
  description: "Découvrez comment créer des ressources de base de données et de conteneur dans Azure\_Cosmos\_DB avec le kit de développement logiciel (SDK) Microsoft .NET\_v3."
---

# Créer des ressources Azure Cosmos DB avec for NoSQL à l’aide de .NET

Dans cet exercice, vous créez une application console qui crée un conteneur, une base de données et un élément dans Azure Cosmos DB.

Tâches effectuées dans cet exercice :

* Création d’un compte Azure Cosmos DB
* Créer l’application console
* Exécuter l’application console et vérifier les résultats

Cet exercice devrait prendre environ **30** minutes.

## Avant de commencer

Avant de commencer, vérifiez que les exigences suivantes sont remplies :

* Un abonnement Azure. Si vous n’en avez pas, vous pouvez [vous inscrire](https://azure.microsoft.com/).

## Création d’un compte Azure Cosmos DB

Dans cette section de l’exercice, vous créez un groupe de ressources et un compte Azure Cosmos DB. Vous enregistrez également le point de terminaison et la clé d’accès pour le compte.

1. Dans votre navigateur, accédez au portail Azure [https://portal.azure.com](https://portal.azure.com) et connectez-vous en utilisant vos informations d’identification Azure.

1. Cliquez sur le bouton **[\>_]** à droite de la barre de recherche, en haut de la page, pour créer un Cloud Shell dans le portail Azure, puis sélectionnez un environnement ***Bash***. Cloud Shell fournit une interface de ligne de commande dans un volet situé en bas du portail Azure.

    > **Note** : si vous avez déjà créé un Cloud Shell qui utilise un environnement *PowerShel*, basculez-le vers ***Bash***.

1. Dans la barre d’outils Cloud Shell, dans le menu **Paramètres**, sélectionnez **Accéder à la version classique** (cela est nécessaire pour utiliser l’éditeur de code).

1. Créez un groupe de ressources pour les ressources nécessaires à cet exercice. Remplacez **\<myResourceGroup>** par un nom que vous souhaitez utiliser pour le groupe de ressources. Vous pouvez remplacer **useast** par une région proche de vous si nécessaire. 

    ```
    az group create --location useast --name <myResourceGroup>
    ```

1. Exécutez la commande suivante pour créer le compte Azure Cosmos DB. Remplacez **\<myCosmosDBacct>** par un nom *unique* pour identifier votre compte Azure Cosmos DB. Remplacez **\<myResourceGroup>** par le nom que vous avez choisi précédemment.

    >**Remarque :** le nom du compte peut uniquement contenir des lettres minuscules, des chiffres et le caractère de trait d’union (-). Sa longueur doit être comprise entre 3 et 31 caractères. *L’exécution de cette commande prend quelques minutes.*

    ```
    az cosmosdb create -n <myCosmosDBacct> -g <myResourceGroup>
    ```

1.  Exécutez la commande suivante pour récupérer le **documentEndpoint** pour le compte Azure Cosmos DB. Enregistrez le point de terminaison à partir des résultats de la commande, il est nécessaire plus loin dans l’exercice. Remplacez **\<myCosmosDBacct>** et **\<myResourceGroup>** par les noms que vous avez créés.

    ```bash
    az cosmosdb show -n <myCosmosDBacct> -g <myResourceGroup> --query "documentEndpoint" --output tsv
    ```

1. Récupérez la clé primaire du compte avec la commande suivante. Enregistrez la **primaryMasterKey** à partir des résultats de la commande pour l’utiliser dans le code. Remplacez **\<myCosmosDBacct>** et **\<myResourceGroup>** par les noms que vous avez créés.

     ```
    # Retrieve the primary key
    az cosmosdb keys list -n <myCosmosDBacct> -g <myResourceGroup>
    ```

## Création d'application console

Maintenant que les ressources nécessaires sont déployées sur Azure, l’étape suivante consiste à configurer l’application console en utilisant la même fenêtre de terminal dans Visual Studio Code.

1. Créez un dossier pour le projet et accédez à ce dossier.

    ```bash
    mkdir cosmosdb
    cd cosmosdb
    ```

1. Créez l’application console .NET.

    ```dotnetcli
    dotnet new console --framework net8.0
    ```

1. Exécutez les commandes suivantes pour ajouter le package **Microsoft.Azure.Cosmos** au projet, ainsi que le package **Newtonsoft.Json** connexe.

    ```dotnetcli
    dotnet add package Microsoft.Azure.Cosmos --version 3.*
    dotnet add package Newtonsoft.Json --version 13.*
    ```

Il est maintenant temps de remplacer le code du modèle dans le fichier **Program.cs** à l’aide de l’éditeur dans Cloud Shell.

### Ajouter le code de démarrage du projet

1. Pour commencer à modifier l’application, exécutez la commande suivante dans Cloud Shell :

    ```bash
    code Program.cs
    ```

1. Remplacez tout code existant par l’extrait de code suivant après les instructions **using**. Veillez à remplacer les valeurs des espaces réservés pour **\<documentEndpoint>** et **\<primaryKey>** en suivant les consignes dans les commentaires de code.

    Le code fournit la structure globale de l’application et certains éléments nécessaires. Passez en revue les commentaires dans le code ; vous ajoutez du code dans des zones spécifiées dans les instructions. 

    ```csharp
    using Microsoft.Azure.Cosmos;
    
    namespace CosmosExercise
    {
        // This class represents a product in the Cosmos DB container
        public class Product
        {
            public string? id { get; set; }
            public string? name { get; set; }
            public string? description { get; set; }
        }
    
        public class Program
        {
            // Cosmos DB account URL - replace with your actual Cosmos DB account URL
            static string cosmosDbAccountUrl = "<documentEndpoint>";
    
            // Cosmos DB account key - replace with your actual Cosmos DB account key
            static string accountKey = "<primaryKey>";
    
            // Name of the database to create or use
            static string databaseName = "myDatabase";
    
            // Name of the container to create or use
            static string containerName = "myContainer";
    
            public static async Task Main(string[] args)
            {
                // Create the Cosmos DB client using the account URL and key
    
    
                try
                {
                    // Create a database if it doesn't already exist
    
    
                    // Create a container with a specified partition key
    
    
                    // Define a typed item (Product) to add to the container
    
    
                    // Add the item to the container
                    // The partition key ensures the item is stored in the correct partition
    
    
                }
                catch (CosmosException ex)
                {
                    // Handle Cosmos DB-specific exceptions
                    // Log the status code and error message for debugging
                    Console.WriteLine($"Cosmos DB Error: {ex.StatusCode} - {ex.Message}");
                }
                catch (Exception ex)
                {
                    // Handle general exceptions
                    // Log the error message for debugging
                    Console.WriteLine($"Error: {ex.Message}");
                }
            }
        }
    }
    ```

### Ajouter du code pour créer le client et effectuer des opérations 

Dans cette section de l’exercice, vous ajoutez du code dans des zones spécifiées des projets pour créer le client, la base de données, le conteneur, et pour ajouter un exemple d’élément au conteneur.

1. Ajoutez le code suivant dans l’espace après le commentaire **// Créer le client Cosmos DB à l’aide de l’URL et de la clé du compte**. Ce code définit le client utilisé pour se connecter à votre compte Azure Cosmos DB.

    ```csharp
    CosmosClient client = new(
        accountEndpoint: cosmosDbAccountUrl,
        authKeyOrResourceToken: accountKey
    );
    ```

    >Remarque : il est recommandé d’utiliser **DefaultAzureCredential** de la bibliothèque *Azure Identity*. Des exigences de configuration supplémentaires dans Azure peuvent être nécessaires en fonction de la configuration de votre abonnement. 

1. Ajoutez le code suivant dans l’espace après le commentaire **// Créer une base de données si elle n’existe pas déjà**. 

    ```csharp
    Microsoft.Azure.Cosmos.Database database = await client.CreateDatabaseIfNotExistsAsync(databaseName);
    Console.WriteLine($"Created or retrieved database: {database.Id}");
    ```

1. Ajoutez le code suivant dans l’espace après le commentaire **// Créer un conteneur avec une clé de partition spécifiée**. 

    ```csharp
    Microsoft.Azure.Cosmos.Database database = await client.CreateDatabaseIfNotExistsAsync(databaseName);
    Console.WriteLine($"Created or retrieved database: {database.Id}");
    ```

1. Ajoutez le code suivant dans l’espace après le commentaire **// Définir un élément typé (Produit) à ajouter au conteneur**. Cela définit l’élément ajouté au conteneur.

    ```csharp
    Product newItem = new Product
    {
        id = Guid.NewGuid().ToString(), // Generate a unique ID for the product
        name = "Sample Item",
        description = "This is a sample item in my Azure Cosmos DB exercise."
    };
    ```

1. Ajoutez le code suivant dans l’espace après le commentaire **// Ajouter l’élément au conteneur**. 

    ```csharp
    ItemResponse<Product> createResponse = await container.CreateItemAsync(
        item: newItem,
        partitionKey: new PartitionKey(newItem.id)
    );
    ```

1. Maintenant que le code est terminé, enregistrez votre progression à l’aide de **Ctrl+S** pour enregistrer le fichier, puis **Ctrl+Q** pour quitter l’éditeur.

1. Exécutez la commande suivante dans Cloud Shell pour rechercher d’éventuelles erreurs dans le projet. Si des erreurs s’affichent, ouvrez le fichier *Program.cs* dans l’éditeur et recherchez des erreurs de code manquant ou de collage.

    ```bash
    dotnet build
    ```

Maintenant que le projet est terminé, il est temps d’exécuter l’application et de vérifier les résultats dans le portail Azure.

## Exécuter l’application et vérifier les résultats

1. Exécutez la commande `dotnet run` si vous êtes dans Cloud Shell. La sortie doit être similaire à l’exemple suivant.

    ```
    Created or retrieved database: myDatabase
    Created or retrieved container: myContainer
    Created item: c549c3fa-054d-40db-a42b-c05deabbc4a6
    Request charge: 6.29 RUs
    ```

1. Dans le portail Azure, accédez à la ressource Azure Cosmos DB que vous avez créée précédemment. Sélectionnez **Explorateur de données** dans le volet de navigation de gauche. Dans l’**Explorateur de données**, sélectionnez **myDatabase**, puis développez **myContainer**. Vous pouvez afficher l’élément que vous avez créé en sélectionnant **Éléments**.

    ![Capture d’écran montrant l’emplacement de Éléments dans l’Explorateur de données.](./media/09/cosmos-data-explorer.png)

## Nettoyer les ressources

Maintenant que vous avez terminé l’exercice, vous devez supprimer les ressources cloud que vous avez créées pour éviter une utilisation inutile des ressources.

1. Accédez au groupe de ressources que vous avez créé et affichez le contenu des ressources utilisées dans cet exercice.
1. Dans la barre d’outils, sélectionnez **Supprimer le groupe de ressources**.
1. Entrez le nom du groupe de ressources et confirmez que vous souhaitez le supprimer.
