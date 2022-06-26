---
title: "04 - Alternatives"
prev_class: "03-tableaux-matrices"
next_class: "05-boucles"
---

## Définition

Une alternative, ou branchement conditionnel, est un *bloc de code* dont l'exécution est **optionnelle** et dépend d'une certaine **condition**, **une [expression](cours/02-expressions.md) booléenne** dans laquelle on retrouve en général des variables utilisées avant cette alternative.

## Branchement `if` simple {id="branchementsimple"}

On commence toujours une alternative par le mot clé `if` suivi de la condition entre parenthèses. Le code optionnel est le bloc de code compris entre les accolades `{}` venant après le `if`.

```java
int i = int(random(-10, 10));

if (i == 0) {
  // Bloc de code conditionnel
  // Exécuté uniquement si i est à égal à 0
  println("i est égal à 0");
}

println("Après le if");
```

## Branchement avec `else`

Le mot clé `else` permet d'exécuter un bloc de code optionnel, différent, lorsque la condition du `if` le précédant n'est pas remplie. Il faut encore une fois mettre ce bloc de code entre accolades `{}`.

```java
int i = int(random(-10, 10));

if (i == 0) {
  // Bloc de code conditionnel
  // Exécuté uniquement si i est à égal à 0
  println("i est égal à 0");
} else {
  // Bloc de code conditionnel
  // Exécuté uniquement si i n'est pas égal à 0
  println("i n'est pas égal à 0");
}

println("Après le if/else");
```

## Branchement multiple avec `else if`

Il est possible de faire un branchement multiple avec différentes conditions, chacune ayant son propre bloc de code optionnel. Ce branchement multiple commence toujours par un `if`, et chaque branche conditionnelle supplémentaire est introduite via le mot clé `else if` suivi de la condition entre parenthèses.

Dès que la condition d'un des branchements est respectée, le bloc de code correspondant sera exécuté, et **on finit le branchement** ; on en sort et continue l'exécution du code suivant le branchement.

Dans le cas d'un branchement multiple, le branchement `else`, si présent, ne sera donc exécuté que lorsqu'aucune condition de tous les `if`/`else if` n'est remplie.

```java
int i = int(random(-10, 10));

if (i == 0) {
  // Bloc de code conditionnel
  // Exécuté uniquement si i est à égal à 0
  println("i est égal à 0");
} else if (i > 0) {
  // Bloc de code conditionnel
  // Exécuté uniquement si i est strictement supérieur à 0
  println("i est plus grand que 0");
} else {
  // Bloc de code conditionnel
  // Exécuté uniquement si i n'est ni égal, ni supérieur à 0
  println("i n'est pas égal ni plus grand que 0");
}

println("Après le if/else");
```

> ⚠️ Enchaîner plusieurs branchements `if` n'est pas équivalent à un branche `if`/`else if`.  Dans le cas de `if` consécutifs, chaque branchement/condition sera évalué ; dans le cas d'un branchement multiple `if`/`else if`, l'évaluation des conditions s'arrête dès lors que la condition d'une des branches est respectée.

## Branchements imbriqués
On parle d'*imbrication* lorsqu'on utilise un branchement conditionnel à l'intérieur d'un autre branchement conditionnel.

```java
int i = int(random(-10, 10));

if (i == 0) {
  // Bloc de code conditionnel
  // Exécuté uniquement si i est à égal à 0
  println("i est égal à 0");
} else if (i > 0) {
  // Bloc de code conditionnel
  // Exécuté uniquement si i est strictement supérieur à 0
  println("i est plus grand que 0");
  if (i > 5) {
    println("i est plus grand que 5");
  }
} else {
  // Bloc de code conditionnel
  // Exécuté uniquement si i n'est ni égal, ni supérieur à 0
  println("i n'est pas égal ni plus grand que 0");
  if (i < -5) {
    println("i est plus petit que -5");
  }
}

println("Après le if/else");
```

## Remarques

### Blocs et indentation
Un bloc de code est délimité par des accolades `{}`. Pour une meilleure lisibilité du code, il est important de penser à *indenter* chaque bloc, c'est à dire à le décaler (vers la droite) du bloc de code qui l'englobe. L'indentation est complètement optionnelle mais essentielle pour un code propre et lisible. 

On peut ainsi facilement voir, dans le cas des branchements conditionnels, dans quelle branche se situe le bloc de code. Cela devient encore plus utile lorsqu'on a plusieurs `if` imbriqués.

```java
int i = int(random(-10, 10));

// Peu lisible
if (i > 0) {
println("i est plus grand que 0");
if (i > 5) {
println("i est plus grand que 5");
}
}

// Avec accolades
if (i > 0) {
  println("i plus grand que 0");
  if (i > 5) {
    println("i est plus grand que 5");
  }
}
```

### Notation alternative

Lorsqu'un bloc de code conditionnel ne contient qu'une seule ligne de code *exécutable*, on peut se passer des accolades `{}`. 

```java
int i = int(random(-10, 10));

// Avec accolades
if (i > 0) {
  if (i > 5) {
    println("i est plus grand que 5");
  }
}

// Sans accolades
if (i > 0)
  if (i > 5)
    println("i est plus grand que 5");
```

Comme on le voit ici, le `if` imbriqué et ce qu'il contient ne sont considérés que comme un seul bloc exécutable, et on peut donc se passer des accolades autour même s'il s'agit, visuellement, de plus qu'une seule ligne de code.

> ⚠️ Pour éviter des problèmes, je conseille d'éviter cette notation et de toujours utiliser les accolades pour délimiter les blocs.