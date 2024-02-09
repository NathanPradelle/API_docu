# REST API

Par groupe de 3, vous allez concevoir une API répondant à certains critères.

Cette documentation incluera différents éléments tels que:

- Toutes les routes(endpoints) que comportera votre API (resources, methods, descriptions de l'action effectuée, exemple fictif d'output)
- L'architecture que vous avez prévue pour votre code

## L'application

Votre application portera sur l'inventaire d'une grande chaine de magasin.

Dans votre application, vous devrez gérer une serie d'articles, disponibles en magasin.

Pour chacun de ces articles, il y aura une donnée sur le stock, présent dans chaque magasin.

Les articles seront inscrits dans des catégories.

Une personne qui travaille dans un magasin ne pourra que consulter les stocks de son magasin, sauf s'il s'agit d'un compte administrateur.

Vous devrez faire des routes qui seront utilisées par les gestionnaires de l'inventaire, qui renfloueront les stocks, ainsi que par les commerciaux, par le biais de l'application de leurs caisses enregistreuses.

Les clients auront aussi accès à la consultation des stocks depuis un site web publique.

Nous comparerons à la fin de la séance les différentes propositions.


## Exemples de documentations: 

**Endpoint**:

### Ajouter un To-do

Ajouter un To-do à la base de données.

**URL** : `index.php/to-do`

**Method** : `POST`

**Auth required** : NO

**Permissions required** : None

**Data constraints**

Donner une description pour le To-do à créer.

```json
{
  "description": "Mop the floor"
}
```

#### Success Response

**Code** : `201 Created`

**Content examples**

For a Todo

```json
{
    "id": 1,
    "description": "Mop the floor",
    "done": false,
    "date":"2014-03-02"
}
```

#### Error Responses

**Condition**: if the description is empty

**Code**: `400 Bad Request`

**Content**: `{ "message": "Description should have more than 1 character" }`

#### Notes

* l'attribut `done` sera mis à "faux" par défaut.

**Architecture**:
```
.
├── common
│   ├── exceptions
│   │   ├── controller_exceptions.php
│   │   └── repository_exceptions.php
│   ├── request.php
│   └── response.php
├── index.php
└── todo
    ├── controller.php
    ├── repository.php
    ├── service.php
    └── todo.php
```
