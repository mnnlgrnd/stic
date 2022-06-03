[Index](_index.md) / 01 - Variables

# 01 - Variables

## Définition

Une variable est un **_conteneur_** défini par

-   Son **type** : le type de données qu'elle pourra contenir
-   Son **nom** : le nom à utiliser pour récupérer la valeur qu'elle contient

## Types

Les types de variables dits **primitifs** sont les types inhérents au langage (ici, Java), on retrouve notamment

| Type | Valeurs |
| --- | --- |
| `boolean` | `true` ou `false` |
| `char` | Caractère, toujours écrit entre `''`, par exemple `'a'`
| `short` | Petit nombre entier entre `-128` et `127`
| `int` | Grand nombre entier entre `-2147483648` à `2147483647` |
| `long` | Très grand nombre entier |
| `float` | Nombre décimal, par exemple `3.14` |
| `double` | Nombre décimal plus précis |

Note : On peut forcer un nombre décimal à être évalué comme un `float` ou un `double` en écrivant respectivement f ou d à la fin du nombre, par exemple `3.14f` ou `3.14d`


Processing propose un type spécifique pour gérer les couleurs : `color`