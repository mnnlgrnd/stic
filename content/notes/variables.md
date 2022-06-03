---
title: "01 - Variables"
---

# Définition

Une variable est un **_conteneur_** défini par

-   Son **type** : le type de données qu'elle pourra contenir
-   Son **nom** : le nom à utiliser pour récupérer la valeur qu'elle contient

# Types

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

Note : On peut forcer un nombre décimal à être évalué comme un `float` ou un `double` en écrivant respectivement f ou d à la fin du nombre, par exemple `3.14f` ou `3.14d`

# Déclaration

Déclarer une variable permet de créer une nouvelle variable qui sera désormais utilisable dans la suite du code. Pour déclarer une variable, il faut impérativement indiquer son type et son nom :

```java
int i;
```

Dans ce cas-ci, la variable `i` existe maintenant en processing, mais ne contient encore aucune valeur. On peut également déclarer une nouvelle variable **et** lui donner une valeur initiale :

```java
int i = 5;
```

## Erreurs

-   Lorsque l'on veut utiliser une variable qui n'existe pas, qui n'a pas été déclarée, processing affichera une erreur du type `The variable "j" does not exist`
-  Lorsque l'on déclare une variable avec le même nom qu'une autre variable, processing renverra une erreur du type `Duplicate local variable i`

# Assignation

L'assignation consiste à définir la (nouvelle) valeur d'une variable déclarée :

```java
int i; // Déclaration
i = 5; // Assignation
```
  

L'assignation est donc une ligne de code du type :

\<nom\_variable\> **=** \<valeur\> ;
  
Le symbole **=** est **toujours** l'opérateur qui permet d'assigner une valeur à une variable. La comparaison de deux valeurs se fait avec le symbole **\=\=**.

On peut mettre à droite d'une assignation tout ce qui sera _évalué_ par Processing au **même type** que la variable à laquelle on va assigner cette valeur.

## Exemples

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

## Erreurs

- Lorsque l'on veut assigner à une variable une valeur d'un type incompatible, par exemple `int i = 3.14;`, processing affichera une erreur du type `Type mismatch, "float" does not match with "int"`

# Evaluation

L'**évaluation** est l'interprétation, par Processing, d'un morceau de code pour en déduire une **valeur.** Peuvent être évalués :

-   Une valeur (par exemple `1`, `'a'`, `true`, etc.)
-   Une variable
-   Un appel de fonction : le type de la valeur sera le type de retour de cette fonction
-   Un calcul impliquant des valeurs, variables ou appels de fonction : processing respectera alors l'ordre des opérateurs/parenthèses

Une valeur évaluée peut donc être utilisée :

-   Pour une assignation

```java
int i = 5;
i = 5 * 2;
i = i + 1;
```

-   Dans un appel de fonction

```java
println(i); // On affiche ce que contient la variable i
```

## Exercices

\1. Que sera-t-il affiché dans la console lorsqu'on exécute le code suivant ?

```java
int i = 1;
int j = 2;
println(i);
println(i + j);
i = i + j;
j = 2 * i;
j = 2 * j;
println(i);
println(j);
```

%%<details> 
<summary>Solution</summary>
<div class="highlight">
<div class="chroma">
<table class="lntable">
<tbody>
<tr>
<td class="lntd">
<pre tabindex="0" class="chroma"><code class="language-java" data-lang="java"><span class="line">1</span>
<span class="line">3</span>
<span class="line">3</span>
<span class="line">12</span></code></pre>
</td>
</tr>
</tbody>
</table>		
</div>
</div>
</details>%%
