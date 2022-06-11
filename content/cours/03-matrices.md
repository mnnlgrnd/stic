---
title: "03 - Matrices"
url: "cours/03-matrices"
prev_class: "02-tableaux"
next_class: "04-strings"
---

## Définition

Un [tableau](cours/02-tableaux.md) étant un type de données, il est tout à fait possible de définir un tableau *de tableaux*, c'est-à-dire un tableau dont tous les éléments sont des références vers des tableaux d'un (même) type de données. On peut ainsi avoir un tableau de tableaux d'entiers (2 dimensions), un tableau de tableaux de tableaux de booléen (3 dimensions), etc. Tous les tableaux d'une même dimension auront la même taille, puisque la taille d'un tableau est statique et définie à sa création.

<img src="/stic/images/matrix_dm.svg" class="svg-dark-mode"/>
<img src="/stic/images/matrix_lm.svg" class="svg-light-mode"/>

Une matrice est un tableau de tableaux, et on peut donc le considérer comme un tableau à deux dimensions (comme dans Excel, par exemple). On parlera ainsi de **lignes** pour la première dimension et de colonnes **pour** la deuxième dimension.

## Déclaration

Pour déclarer une matrice, il faut simplement déclarer un tableau dont le type d'éléments est lui-même tableau, c'est-à-dire en rajoutant `[]` après le type d'éléments de ce tableau. Par exemple, pour un tableau d'entiers `int[]`, un tableau de tableau d'entiers sera noté `int[][]`. 

```java
int[][] t1; // Tableau de tableaux d'entiers
float[][] t2; // Tableau de tableaux de float
boolean[][] t3; // Tableau de tableaux de booléens
```

## Création

Comme pour un tableau "classique", à 1 dimension, une matrice peut être créée de deux façons :

1. On peut créer une matrice vide en indiquant la taille du tableau (le nombre de lignes), et la taille des tableaux se trouvant dans ce tableau principal (le nombre de colonnes) dans l'opérateur `[]` (un par dimension).

```java
// Tableau contenant 3 tableaux de 10 éléments chacun
int[][] integers = new int[3][10]; 
```

On peut donc ainsi créer des tableaux de dimension complètement arbitraire :

```java
int[][][][][] whyNot = new int[3][6][9][6][3];
```

2. On peut créer une matrice en indiquant directement les valeurs qu'elle contient entre `{}`. Les accolades délimitent **un** tableau, et pour définir le contenu de la deuxième dimension, le contenu de chaque ligne, il faut aussi utiliser `{}`. Les tailles des tableaux seront alors déterminées automatiquement.

```java
int[][] integers = new int[][] { 
  { 1, 2, 3 }, // Première ligne
  { 4, 5, 6 }, // Deuxième ligne
  { 7, 8, 9 } // Troisième ligne
};
```

## Manipulation

Une matrice étant un tableau, on la manipule de la même façon. La différence est que chaque variable de la première dimension est elle-même un tableau, et qu'on peut donc directement chaîner l'adressage `[]` pour accéder aux éléments de ce tableau.

### Taille de la matrice

Pour la taille de la matrice, on parlera plus simplement de son nombre de lignes et de colonnes qui sont, respectivement, la taille du tableau de la première dimension et la taille des tableaux de la deuxième dimension. On peut récupérer cette information comme on le ferait pour un tableau quelconque.

```java
int[] m = new int[] { 
  { 1, 2, 3 }, 
  { 4, 5, 6 }, 
  { 7, 8, 9 } 
};

int nbLines = m.length;
int nbColumns = m[0].length; // m[0] = première ligne
```

### Élements de la matrice

On accède aux **lignes** du matrice de la même façon qu'un tableau, avec l'opérateur `[]`, et aux éléments d'une ligne en réutilisant l'opérateur `[]` sur la ligne récupérée.

// TODO schéma

```java
int[] m = new int[] { 
  { 1, 2, 3 }, 
  { 4, 5, 6 }, 
  { 7, 8, 9 } 
};

int[] firstLine = m[0];
int[] secondLine = m[1];
int firstElementOfFirstLine = firstLine[0];
int lastElementOfThirdLine = m[2][2];

println(m[1][1]); // Affiche 5
m[1][1] = 10;
println(m[1][1]); // Affiche 10
```

### Parcourir une matrice

Pour parcourir une matrice, c'est-à-dire pour *itérer* sur chacun de ces éléments, il faudra utiliser des boucles imbriquées dont les explications sont disponibles dans la leçon [06 - Boucles](cours/06-boucles.md).