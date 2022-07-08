---
title: "01 - Variables et littéraux"
next_class: "02-expressions"
---

## Variables

### Définition

Une variable est un **_conteneur_** défini par

-   Son **type** : le type de données qu'elle pourra contenir
-   Son **nom** : le nom à utiliser pour récupérer la valeur qu'elle contient

### Types

Les types de variables dits **primitifs** sont les types inhérents au langage (ici, Java), on retrouve notamment

| Type      | Valeurs                                                 |
|:--------- |:------------------------------------------------------- |
| `boolean` | `true` ou `false`                                       |
| `char`    | Caractère, toujours écrit entre `''`, par exemple `'a'` |
| `short`   | Petit nombre entier entre `-128` et `127`               |
| `int`     | Grand nombre entier entre `-2147483648` à `2147483647`  |
| `long`    | Très grand nombre entier                                |
| `float`   | Nombre décimal, par exemple `3.14`                      |
| `double`  | Nombre décimal plus précis                              |

### Déclaration

Déclarer une variable permet de créer une nouvelle variable qui sera désormais utilisable dans la suite du code. Pour déclarer une variable, il faut impérativement indiquer son type et son nom :

```java
int i;
```

Dans ce cas-ci, la variable `i` existe maintenant en processing, mais ne contient encore aucune valeur. On peut également déclarer une nouvelle variable **et** lui donner une valeur initiale :

```java
int i = 5;
```

#### Erreurs

-   Lorsque l'on veut utiliser une variable qui n'existe pas, qui n'a pas été déclarée, processing affichera une erreur du type `The variable "j" does not exist`
-  Lorsque l'on déclare une variable avec le même nom qu'une autre variable, processing renverra une erreur du type `Duplicate local variable i`

### Assignation

L'assignation consiste à définir la (nouvelle) valeur d'une variable déclarée :

```java
int i; // Déclaration
i = 5; // Assignation
```
  

L'assignation est donc une ligne de code du type :

\<nom\_variable\> **=** \<valeur\> ;
  
Le symbole **=** est **toujours** l'opérateur qui permet d'assigner une valeur à une variable. La comparaison de deux valeurs se fait avec le symbole **\=\=**.

On peut mettre à droite d'une assignation tout ce qui sera _évalué_ par processing au **même type** que la variable à laquelle on va assigner cette valeur.

#### Exemples

```java
// Déclarations

int i;
int j;

// Assignations

i = 5; // i va contenir 5
j = 5 * 2; // j va contenir 5 * 2 -> évalué à 10
i = j; // i va contenir j -> évalué à 10
i = j * 2; // i va contenir j * 2 -> évalué à 10 * 2 -> évalué à 20
```

#### Erreurs

- Lorsque l'on veut assigner à une variable une valeur d'un type incompatible, par exemple `int i = 3.14;`, on aura une erreur du type `Type mismatch, "float" does not match with "int"`

### Constantes

Si la valeur contenue dans une variable n'est pas amenée à évoluer pendant l'exécution du programme, mais qu'elle restera toujours la même, on peut imposer cette contrainte en déclarant explicitement une variable *constante*. Pour ce faire, il faut utiliser le mot clé `final` avant le type de la variable.

```java
final int CONSTANT = 1;
```

Pour facilement différencier les variables constantes, qui sont donc des variables auxquelles on ne pourra assigner qu'une seule fois une valeur, il est conseillé de mettre leur nom entièrement en majuscule.

Si, par inadvertance, on essaie malgré tout d'assigner une nouvelle valeur à une variable constante, on aura une erreur du type `Final local variable <name> may already have been assigned`.

## Littéraux

### Définition

A la différence d'une variable, un *littéral* qualifie une valeur constante utilisée directement dans du code. 

### Type

Tout comme une variable, un littéral a un type, mais celui est en général implicite et inféré directement par le langage. On retrouve différents littéraux :
- `true` et `false`, les littéraux de type booléen
- Les littéraux de nombres entiers comme `1`, `23094`, etc.
- Les littéraux de nombres à virgule, comme `3.14`, `-23.45`, etc. On peut forcer le type d'un littéral de nombre à être `float` ou `double`  en utilisant `f` ou `d` après le littéral :
	- `1f` est de type `float`
	- `3.14d` est de type `double`
- Les littéraux de type caractère (`char`) comme `'a'`, `'+'`, etc. ; n'importe quel caractère entre deux `'`
- Les littéraux de chaînes de caractères (strings), vues dans la leçon [09 - Strings](cours/10-strings.md)

### Assignation à une variable

Lorsque l'on utilise un littéral dans une assignation pour stocker sa valeur dans une variable, il faut donc que ce type *corresponde* à celui de la variable. 

> **Correspondance n'est ici pas équivalence**. 

Le littéral `10` est de type entier, mais peut tout à fait être stocké dans une variable de type `float` puisque float peut contenir des nombres de plus grande précision. Le contraire n'est pas vrai ; par exemple, le littéral `3.14` contient un nombre à virgule qui ne peut pas être stocké dans une variable entière (`int`,  `long`) car la précision du littéral est plus grande que celle du type de la variable. Il faut alors convertir explicitement le littéral en entier via la fonction de conversion `int`, par exemple `int(3.14)`, qui ne conservera que la partie entière du nombre.