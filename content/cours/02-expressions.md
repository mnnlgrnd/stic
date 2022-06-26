---
title: "02 - Expressions"
prev_class: "01-variables-litteraux"
next_class: "03-tableaux-matrices"
---


## Définition

En Java, une **expression** est une écriture possédant une ***valeur*** et un ***type*** et dans laquelle on peut retrouver :
- Des littéraux
- Des noms de variables
- Des opérateurs
- Des appels de [fonctions](cours/06-fonctions.md)

La ***valeur*** d'une expression est calculée en tenant compte des valeurs contenues dans les variables apparaissant dans l'expression et des valeurs retournées par les appels de fonction. Le ***type*** de l'expression est le type de cette valeur, du résultat.

Les opérateurs possibles dans une expression dépendent de son type. Comme dans des expressions mathématiques classiques, la priorité des opérateurs est respectée pour obtenir le résultat final, et on peut utiliser des parenthèses 

## Expressions booléennes

Les expressions booléennes sont des expressions dont le type est `boolean`, c'est-à-dire des expressions dans la valeur est `true` ou `false`. 

### Opérateurs 

Les opérateurs possibles dans les expressions booléennes sont donc les opérateurs logiques de base ainsi que les opérateurs de comparaison entre nombres.

Les opérateurs logiques sont, dans l'ordre des priorités :

- `!`, la négation 
- `&&`, le ET logique
- `||` , le OU logique

```java
println(true); // Affiche true
println(!true); // Affiche false
println(true || false); // Affiche true
println(true && false); // Affiche false

println(true || false && false); // Affiche true car on fait d'abord le &&
                                 // Ca équivaut donc à true || false -> true
println((true || false) && false); // Affiche false car on respecte les parenthèses
                                   // Ca équivaut donc à true && false -> false
``` 

Les opérateurs de comparaison ont tous le même ordre d'importance, et sont :

- `==` , l'égalité
- `!=` , la différence
- `>` , strictement plus grand
- `>=`, plus grand ou égal
- `<`, strictement plus petit
- `<=`, plus petit ou égal

```java
println(1 == 1); // Affiche true
println(1 != 1); // Affiche false
println(2 > 1); // Affiche true
println(1 >= 2); // Affiche false
println(1 < 2); // Affiche true
println(2 <= 1); // Affiche false
```

## Expressions mathématiques

Les expressions mathématiques sont des expressions dont le résultat est de type numérique (entier ou flottant). Les opérateurs sont donc les opérateurs classiques en mathématiques, dans l'ordre des priorités :

- `*` et `/` pour la multiplication et la division
- `+` et `-` pour l'addition et la soustraction

```java
println(1 + 1); // Affiche 2
println(3 * 3); // Affiche 9
println(2 + 2 * 2); // Affiche 6
```

### Entiers et flottants

Il faut bien faire attention aux types des valeurs que l'on utilise dans une expression car ce sont eux qui déterminent le type du résultat. 

Lorsqu'une expression ne contient que des valeurs entières, le résultat sera lui-même entier, et ce même si la vraie expression mathématique correspondante ne l'est pas. Ainsi, l'expression `1 / 2` ne contient que des entiers, et le résultat sera donc le résultat de la *division entière* de 1 par 2, qui vaut donc `0`. 

De façon plus générale, si une expression ne contient que des valeurs du même type, ce sera aussi le type de l'expression. Si par contre l'expression contient des valeurs de différents types, l'expression prendra le type ayant la plus grande précision (voir [01 - Variables et littéraux](cours/01-variables-litteraux.md)).

Ainsi, si une expression contient des valeurs de type `int` et des valeurs de type `float`, donc flottantes, l'expression sera de type `float`. Par exemple, le résultat de `1.0 / 2` est flottant, et il s'agit donc de la division normale dont le résultat `0.5`.

```java
int m = 1 / 2; // 0
float n = 1.0 / 2; // 0.5
```

### Modulo

On peut également utiliser l'opérateur `%` pour le "modulo", le reste de la division entière. 

```java
println(1 % 4); // Affiche 1
println(10 % 4); // Affiche 2
println(12 % 4); // Affiche 0
```

L'utilisation du modulo permet de transformer une suite continue en un cycle de valeurs allant de 0 à la valeur du modulo - 1 :


<p align="center">
<img src="/stic/images/modulo_dm.svg" class="svg-dark-mode w-75"/>
<img src="/stic/images/modulo_lm.svg" class="svg-light-mode w-75"/>
</p>

### Sucres syntaxiques
(A prononcer avec l'accent québecois car c'est la seule bonne raison de traduire un terme anglais)

Les sucres syntaxiques, ou *syntactic sugars*, sont des facilités, des raccourcis de code qu'un langage met à disposition des utilisateurs.

Pour les opérations mathématiques, Java propose des raccourcis pour les calculs de la forme *x = x \<opérateur\> \<expression\>*. C'est-à-dire quand on assigne à une variable le résultat d'une opération simple entre cette variable et une autre expression. On peut éviter de répéter la variable *x* en utilisant le sucre syntaxique correspondant *x \<opérateur\>= \<expression\>*. Ceci est valable pour les 4 opérateurs mathématiques standards `+`, `-`, `*` et `/`.

```java
int i = 0;

i = i + 5; // Forme normale
i += 5; // Sucre syntaxique 

i = i * (45 / 3); // Forme normale
i *= 45 / 3; // Sucre syntaxique
```

De plus, lorsque le calcul est de type *x = x + 1* ou *x = x - 1*, on peut davantage simplifier la ligne de code en utilisant les opérateurs d'incrémentation `++` et de décrémentation `--`.

```java
int i = 0;

i = i + 1; // Forme normale
i++; // Incrémentation

i = i - 1; // Forme normale
i--; // Décrémentation
```

Les opérateurs `++` et `--` peuvent s'utiliser avant ou après la variable à incrémenter/décrémentér. Dans les deux cas, la valeur de la variable sera mise à jour avec le résultat de l'addition/soustraction avec 1.

La différence réside dans le fait qu'il s'agit d'une expression ; on peut donc utiliser l'incrémentation/décrémentation comme expression pour une assignation : `int y = x++`. Dans ce cas, l'ordre dans lequel Java va effecter le calcul et l'évaluation de la valeur à assigner à la deuxième variable dépend du placement de l'opérateur `++` ou `--` :

- Si l'opérateur se situe *après* la variable `x` , alors Java va d'abord évaluer la valeur actuelle de cette variable. Cette valeur sera assignée à la variable `y`, puis le calcul incrémental/décrémental sera effectué et la valeur de `x` changée

```java
int x = 0;
int y = x++;
println(x); // Affiche 1
println(y); // Affiche 0
```

- Si l'opération se situe *avant* la variable `x`, c'est l'inverse. C'est d'abord l'incrémentation/décrémentation qui est faite, puis cette nouvelle valeur de `x` sera assignée à `y`.

```java
int x = 0;
int y = ++x;
println(x); // Affiche 1
println(y); // Affiche 1
```