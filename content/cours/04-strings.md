---
title: "04 - Strings"
prev_class: "03-matrices"
next_class: "05-alternatives"
---

## Définition
 Un **string** est un type de données particulier permettant de contenir une chaîne de caractères, du texte. Il ne s'agit pas d'un type primitif comme `int`, `float`, etc. mais d'une [classe](cours/09-classes/md) `String` existante dans le langage Java de base.

Comme toute variable, on déclare un string en indiquant son type, `String`, et le nom de la variable. En Java, une chaîne de caractères est délimitée par des guillemets. Ainsi, toute valeur entre `" "` sera évaluée par processing comme étant du type `String`.

```java
String s = "Hello, world!";
println(s); // Affiche Hello, world!
```

## Manipulation

### Concaténation

La **concaténation** est une opération qui permet de combiner deux chaînes de caractères via l'opérateur `+`. Les deux chaînes de caractères seront alors mises "bout à bout" pour n'en former qu'une.

```java
String s1 = "Hello ";
String s2 = "World";
String s3 = s1 + s2;
println(s); // Affiche Hello World
```

Comme toute opération simple, on peut l'utiliser plusieurs fois dans une même expression, ce qui permet de construire facilement des chaînes de caractères en combinant des variables de type `String` et des valeurs directement.

```java
String s1 = "Hello";
String s2 = "World";
println(s1 + " " + s2 + "!");
```

#### Concaténation avec un autre type

On peut concaténer une chaîne de caractères avec une valeur d'un autre type, cette valeur sera alors convertie automatiquement par processing en une chaîne de caractères correspondant à son contenu.

```java
String s = "Number ";
int i = 5;
println(s + i); // Affiche Number 5
```

