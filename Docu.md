# API

## Description

Cette application porte sur la gestion de l'inventaire d'une grande chaîne de magasins. L'API fournit des fonctionnalités pour gérer les articles disponibles en magasin, consulter les niveaux de stock, effectuer des ventes, etc.

## Types de Rôles

- **Administrateur** : Accès complet à toutes les fonctionnalités de l'API, y compris la gestion des utilisateurs, des articles, etc.

- **Gestionnaire** : Peut effectuer des opérations de gestion sur les articles, telles que l'ajout, la modification et la suppression, mais n'a pas nécessairement accès à d'autres fonctionnalités d'administration.

- **Employé du Magasin** : Limité à des actions spécifiques telles que la vente d'articles par exemple.

## Endpoint :

### Liste des Articles

   Récupère la liste des articles disponibles en magasin.

   - **URL** : `index.php/inventory/articles`
   - **Méthode** : GET
   - **Authentification requise** : Non
   - **Permissions requises** : Aucune

   **Réponse en cas de succès** :
   ```json
   [
       {
           "id": 1,
           "name": "T-shirt",
           "category": "Vêtements",
           "stock": 100,
           "price": 10
       },
       {
           "id": 2,
           "name": "Laptop",
           "category": "Électronique",
           "stock": 50
           "price": 800
       }
   ]
```

### Détails d'un Article

Récupère les détails d'un article spécifique.

- **URL** : `index.php/inventory/articles/{article_id}`
- **Méthode** : GET
- **Authentification requise** : Non
- **Permissions requises** : Aucune

**Réponse en cas de succès** :
```json
{
    "id": 1,
    "name": "T-shirt",
    "category": "Vêtements",
    "stock": 100
    "price": 9.99
}
```

### Ajouter du Stock à un Article

Permet d'ajouter du stock à un article existant.

- **URL** : index.php/inventory/articles/{article_id}/add-stock
- **Méthode** : POST
- **Authentification requise** : Oui (Administrateur ou Gestionnaire)
- **Permissions requises** : Administrateur ou Gestionnaire
- **Données attendues dans le corps de la requête** :

```json
{
    "quantity": 50
}
```

Réponse en cas de succès :

```json
{
    "message": "Stock ajouté avec succès",
    "new_stock": 150
}
```

### Consulter le Stock d'un Magasin

Récupère le stock disponible dans un magasin spécifique.

- **URL** : index.php/inventory/store/{store_id}/stock
- **Méthode** : GET
- **Authentification requise** : Oui
- **Permissions requises** : Employé du Magasin ou Administrateur

Réponse en cas de succès :

```json
[
    {
        "article_id": 1,
        "name": "T-shirt",
        "stock": 100
    },
    {
        "article_id": 2,
        "name": "Laptop",
        "stock": 50
    }
]
```

### Rechercher des Articles par Nom ou Catégorie

Permet de rechercher des articles en fonction de leur nom ou de leur catégorie.

- **URL** : index.php/inventory/articles/search
- **Méthode** : GET
- **Authentification requise** : Non
- **Permissions requises** : Aucune
- **Paramètres de requête possibles** :
  - **name**: Nom de l'article (optionnel)  
  - **category**: Catégorie de l'article (optionnel)

Réponse en cas de succès:

```json
[
    {
        "id": 1,
        "name": "T-shirt",
        "category": "Vêtements",
        "stock": 100
    }
]
```

### Supprimer du Stock d'un Article

Permet de supprimer du stock d'un article existant.

- **URL** : index.php/inventory/articles/{article_id}/remove-stock
- **Méthode** : POST
- **Authentification requise** : Oui (Administrateur ou Gestionnaire)
- **Permissions requises** : Administrateur ou Gestionnaire
- **Données attendues dans le corps de la requête** :

```json
{
    "quantity": 20
}
```

Réponse en cas de succès :

```json
{
    "message": "Stock supprimé avec succès",
    "new_stock": 80
}
```

### Modifier les Informations d'un Article

Permet de modifier les informations d'un article existant.

- **URL** : index.php/inventory/articles/{article_id}
- **Méthode** : PUT
- **Authentification requise** : Oui (Administrateur ou Gestionnaire)
- **Permissions requises** : Administrateur ou Gestionnaire
- **Données attendues dans le corps de la requête** :

```json
{
    "name": "Nouveau nom de l'article",
    "category": "Nouvelle catégorie",
    "price": 29.99,
    "description": "Nouvelle description de l'article"
}
```

Réponse en cas de succès :

```json
{
    "message": "Informations de l'article mises à jour avec succès"
}
```

### Ajouter un Nouvel Article

Permet d'ajouter un nouvel article à l'inventaire.

- **URL** : index.php/inventory/articles
- **Méthode** : POST
- **Authentification requise** : Oui (Administrateur ou Gestionnaire)
- **Permissions requises** : Administrateur ou Gestionnaire
- **Données attendues dans le corps de la requête** :

```json
{
    "name": "Nouvel article",
    "category": "Nouvelle catégorie",
    "stock": 50,
    "price": 19.99,
    "description": "Description du nouvel article"
}
```

Réponse en cas de succès :

```json
{
    "message": "Article ajouté avec succès",
    "article_id": 3
}
```

### Supprimer un Article

Permet de supprimer un article de l'inventaire.

- **URL** : index.php/inventory/articles/{article_id}
- **Méthode** : DELETE
- **Authentification requise** : Oui (Administrateur)
- **Permissions requises** : Administrateur

Réponse en cas de succès :

```json
{
    "message": "Article supprimé avec succès"
}
```

### Historique des Ventes

Permet de consulter l'historique des ventes pour un article spécifique.

- **URL** : index.php/inventory/articles/{article_id}/sales-history
- **Méthode** : GET
- **Authentification requise** : Oui (Administrateur ou Gestionnaire)
- **Permissions requises** : Administrateur ou Gestionnaire

Réponse en cas de succès :

```json
[
    {
        "sale_id": 1,
        "quantity": 5,
        "total_price": 49.95,
        "date": "2024-02-11T15:30:00Z"
    },
    {
        "sale_id": 2,
        "quantity": 3,
        "total_price": 29.97,
        "date": "2024-02-12T10:45:00Z"
    }
]
```

## Architecture :

```
.
├── common
│   ├── exceptions
│   │   ├── controller_exceptions.php
│   │   └── repository_exceptions.php
│   ├── request.php
│   └── response.php
├── index.php
└── inventory
    ├── controller.php
    ├── repository.php
    ├── service.php
    └── models
        ├── article.php
        └── category.php

```
