<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "f0ce2d470f3efad6f8c7df376f416a4b",
  "translation_date": "2025-07-12T07:32:44+00:00",
  "source_file": "00-course-setup/AzureSearch.md",
  "language_code": "fr"
}
-->
# Guide d'installation d'Azure AI Search

Ce guide vous aidera à configurer Azure AI Search via le portail Azure. Suivez les étapes ci-dessous pour créer et configurer votre service Azure AI Search.

## Prérequis

Avant de commencer, assurez-vous de disposer des éléments suivants :

- Un abonnement Azure. Si vous n'avez pas d'abonnement Azure, vous pouvez créer un compte gratuit sur [Azure Free Account](https://azure.microsoft.com/free/?wt.mc_id=studentamb_258691).

## Étape 1 : Créer un service Azure AI Search

1. Connectez-vous au [portail Azure](https://portal.azure.com/?wt.mc_id=studentamb_258691).
2. Dans le volet de navigation à gauche, cliquez sur **Créer une ressource**.
3. Dans la barre de recherche, tapez "Azure AI Search" et sélectionnez **Azure AI Search** dans la liste des résultats.
4. Cliquez sur le bouton **Créer**.
5. Dans l’onglet **Bases**, renseignez les informations suivantes :
   - **Abonnement** : Sélectionnez votre abonnement Azure.
   - **Groupe de ressources** : Créez un nouveau groupe de ressources ou sélectionnez-en un existant.
   - **Nom de la ressource** : Entrez un nom unique pour votre service de recherche.
   - **Région** : Choisissez la région la plus proche de vos utilisateurs.
   - **Niveau tarifaire** : Sélectionnez un niveau tarifaire adapté à vos besoins. Vous pouvez commencer avec le niveau Gratuit pour des tests.
6. Cliquez sur **Vérifier + créer**.
7. Vérifiez les paramètres puis cliquez sur **Créer** pour lancer la création du service de recherche.

## Étape 2 : Premiers pas avec Azure AI Search

1. Une fois le déploiement terminé, accédez à votre service de recherche dans le portail Azure.
2. Sur la page de présentation du service, cliquez sur le bouton **Démarrage rapide**.
3. Suivez les étapes du guide Démarrage rapide pour créer un index, importer des données et effectuer une requête de recherche.

### Créer un index

1. Dans le guide Démarrage rapide, cliquez sur **Créer un index**.
2. Définissez le schéma de l’index en précisant les champs et leurs attributs (par exemple, type de données, recherche possible, filtrable).
3. Cliquez sur **Créer** pour créer l’index.

### Importer des données

1. Dans le guide Démarrage rapide, cliquez sur **Importer des données**.
2. Choisissez une source de données (par exemple, Azure Blob Storage, Azure SQL Database) et fournissez les informations de connexion nécessaires.
3. Faites correspondre les champs de la source de données avec ceux de l’index.
4. Cliquez sur **Soumettre** pour importer les données dans l’index.

### Effectuer une requête de recherche

1. Dans le guide Démarrage rapide, cliquez sur **Explorateur de recherche**.
2. Saisissez une requête dans la barre de recherche pour tester la fonctionnalité.
3. Consultez les résultats et ajustez le schéma de l’index ou les données si nécessaire.

## Étape 3 : Utiliser les outils Azure AI Search

Azure AI Search s’intègre à divers outils pour enrichir vos capacités de recherche. Vous pouvez utiliser Azure CLI, le SDK Python et d’autres outils pour des configurations et opérations avancées.

### Utilisation d’Azure CLI

1. Installez Azure CLI en suivant les instructions sur [Install Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli?wt.mc_id=studentamb_258691).
2. Connectez-vous à Azure CLI avec la commande :
   ```bash
   az login
   ```
3. Créez un nouveau service de recherche avec Azure CLI :
   ```bash
   az search service create --resource-group <resource-group> --name <service-name> --sku Free
   ```
4. Créez un index avec Azure CLI :
   ```bash
   az search index create --service-name <service-name> --name <index-name> --fields "field1:type, field2:type"
   ```

### Utilisation du SDK Python

1. Installez la bibliothèque cliente Azure Cognitive Search pour Python :
   ```bash
   pip install azure-search-documents
   ```
2. Utilisez le code Python suivant pour créer un index et importer des documents :
   ```python
   from azure.core.credentials import AzureKeyCredential
   from azure.search.documents import SearchClient
   from azure.search.documents.indexes import SearchIndexClient
   from azure.search.documents.indexes.models import SearchIndex, SimpleField, edm

   service_endpoint = "https://<service-name>.search.windows.net"
   api_key = "<api-key>"

   index_client = SearchIndexClient(service_endpoint, AzureKeyCredential(api_key))

   fields = [
       SimpleField(name="id", type=edm.String, key=True),
       SimpleField(name="content", type=edm.String, searchable=True),
   ]

   index = SearchIndex(name="sample-index", fields=fields)

   index_client.create_index(index)

   search_client = SearchClient(service_endpoint, "sample-index", AzureKeyCredential(api_key))

   documents = [
       {"id": "1", "content": "Hello world"},
       {"id": "2", "content": "Azure Cognitive Search"}
   ]

   search_client.upload_documents(documents)
   ```

Pour plus d’informations détaillées, consultez la documentation suivante :

- [Créer un service Azure Cognitive Search](https://learn.microsoft.com/en-us/azure/search/search-create-service-portal?wt.mc_id=studentamb_258691)
- [Premiers pas avec Azure Cognitive Search](https://learn.microsoft.com/en-us/azure/search/search-get-started-portal?wt.mc_id=studentamb_258691)
- [Outils Azure AI Search](https://learn.microsoft.com/en-us/azure/ai-services/agents/how-to/tools/azure-ai-search?tabs=azurecli%2Cpython&pivots=code-examples?wt.mc_id=studentamb_258691)

## Conclusion

Vous avez configuré avec succès Azure AI Search via le portail Azure et les outils associés. Vous pouvez désormais explorer des fonctionnalités plus avancées pour améliorer vos solutions de recherche.

Pour toute aide supplémentaire, consultez la [documentation Azure Cognitive Search](https://learn.microsoft.com/en-us/azure/search/?wt.mc_id=studentamb_258691).

**Avertissement** :  
Ce document a été traduit à l’aide du service de traduction automatique [Co-op Translator](https://github.com/Azure/co-op-translator). Bien que nous nous efforcions d’assurer l’exactitude, veuillez noter que les traductions automatiques peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d’origine doit être considéré comme la source faisant foi. Pour les informations critiques, une traduction professionnelle réalisée par un humain est recommandée. Nous déclinons toute responsabilité en cas de malentendus ou de mauvaises interprétations résultant de l’utilisation de cette traduction.