---
title: "03 - Tableaux et matrices"
prev_class: "02-expressions"
next_class: "04-strings"
---

## Définition

Un **tableau** est une collection ordonnée de variables du même type. On accède a une variable du tableau grâce au nom du tableau et à la position de la variable dans celui-ci.

Un tableau est un type de données au même titre que le sont `int`, `float`, etc. Il s'agit cependant d'un type dit *référentiel* et non primitif, car la variable de type tableau contient en réalité une référence vers un une suite de blocs en mémoire contenant les variables du tableau.

### Stockage en mémoire

Lorsqu'un programme processing s'exécute, il possède sa propre mémoire dans laquelle seront stockées toutes les variables et tout ce qu'il se déroule dans le programme (appels de fonction, etc.). Cette mémoire se compose de deux parties :

- La mémoire dite statique, le *stack*, qui contient notamment les variables (locales) de type primitif et des **références** vers des données stockées dans le *heap*
- La mémoire dite dynamique, le *heap*, qui contient notamment des tableaux et des [objets](cours/09-classes.md)

<img src="/stic/images/stack_heap_dm.svg" class="svg-dark-mode"/>
<img src="/stic/images/stack_heap_lm.svg" class="svg-light-mode"/>

> ⚠️ Le stockage en mémoire est en réalité plus complexe, l'important ici est de comprendre la différence entre une valeur et une référence. Pour plus de détails sur la gestion de la mémoire lors de l'exécution d'un programme Java, Google est votre ami.

## Déclaration

On déclare un tableau comme on déclare une [variable](cours/01-variables-litteraux.md), à ceci près qu'il faut rajouter l'opérateur `[]` pour indiquer qu'il s'agit d'un tableau. On peut ajouter cet opérateur soit après le **type** de données du tableau, soit après son nom. Il s'agit de déclarations équivalentes.

```java
int[] integers;
```

ou

```java
int integers[];
```

On déclare ici une variable appelée `integers` qui est un tableau de nombres entiers.

## Création

Il existe deux façons de créer un tableau :

1. On peut créer un tableau vide en indiquant sa taille, le nombre d'éléments qu'il contient.

```java
int[] integers = new int[6];
```

2. On peut créer un tableau en indiquant directement les valeurs qu'il contient entre `{}`. La taille du tableau sera donc le nombre d'éléments qu'on définit.

```java
int[] integers = new int[] { 1, 2, 4, 8, 16, 32 };
```

Dans les deux cas, l'utilisation du mot clé `new` est obligatoire. Ce mot clé indique qu'on crée une nouvelle **référence** et est responsable de l'allocation en mémoire.

## Manipulation

Une fois un tableau déclaré et créé, on peut accéder à sa taille et aux différents éléments qu'il contient.

### Taille du tableau

La taille d'un tableau **est déterminée à sa création et ne peut pas être changée**, on peut la récupérer grâce au champ spécial `length` du tableau, de la façon suivante :

```java
int[] integers = new int[] { 1, 2, 3 };
println(integers.length); // Affiche 3
```

### Élements du tableau

Pour accéder à un élément particulier du tableau, il faut utiliser l'opérateur de tableau et l'indice de l'élément après le nom du tableau, par exemple `integers[1]`.

> ⚠️ En informatique, on commence à compter à partir de 0. Le premier élément aura donc l'indice 0, le deuxième l'indice 1, ainsi de suite.

Lorsque l'on accède à un élément du tableau, on récupère une variable (celle stockée dans le heap), et on peut donc s'en servir comme tel ; c'est-à-dire lui assigner une valeur, ou l'évaluer dans des expressions.

```java
int[] integers = new int[] { 1, 2, 3 };

// Evalue la variable à l'indice 0 dans le tableau et affiche 1
println(integers[0]); 

// Assigne la valeur 0 à la variable à l'indice 1 dans le tableau
integers[1] = 0; 

// Evalue la variable à l'indice 1 dans le tableau et affiche 0
println(integers[0]);

// Evalue la variable à l'indice 2 dans le tableau et affiche 3
println(integers[2]); 
```

### Parcourir le tableau

Pour parcourir un tableau, c'est-à-dire pour *itérer* sur chacun de ces éléments, il faudra utiliser une boucle dont les explications sont disponibles dans la leçon [06 - Boucles](cours/06-boucles.md).

### Erreurs

- Lorsque l'on essaie d'accéder à un élément dont l'indice est supérieur à la taille du tableau, c'est-à-dire à une position **hors** du tableau, l'exécution du code provoquera une erreur du type `ArrayIndexOutOfBoundsException` avec l'indice auquel on a voulu accéder.


## Matrices

### Tableau de tableaux

Un [tableau](cours/03-tableaux-matrices.md) étant un type de données, il est tout à fait possible de définir un tableau *de tableaux*, c'est-à-dire un tableau dont tous les éléments sont des références vers des tableaux d'un (même) type de données. On peut ainsi avoir un tableau de tableaux d'entiers (2 dimensions), un tableau de tableaux de tableaux de booléens (3 dimensions), etc. Tous les tableaux d'une même dimension auront la même taille, puisque la taille d'un tableau est statique et définie à sa création.

<img src="/stic/images/matrix_dm.svg" class="svg-dark-mode"/>
<img src="/stic/images/matrix_lm.svg" class="svg-light-mode"/>

Une matrice est un tableau de tableaux : un tableau à deux dimensions, comme dans Excel, par exemple. On parlera ainsi de **lignes** pour la première dimension et de **colonnes** pour la deuxième dimension.

### Déclaration et création

Pour déclarer une matrice, il faut simplement déclarer un tableau dont le type d'éléments est lui-même tableau, c'est-à-dire en rajoutant `[]` après le type d'éléments de ce tableau. Par exemple, un tableau de tableaux d'entiers sera noté `int[][]`. 

```java
int[][] t1; // Tableau de tableaux d'entiers
float[][] t2; // Tableau de tableaux de float
boolean[][] t3; // Tableau de tableaux de booléens
```

Comme pour un tableau "classique", à une seule dimension, une matrice peut être créée de deux façons :

1. On peut créer une matrice vide en indiquant la taille du tableau (le nombre de lignes), et la taille des tableaux se trouvant dans ce tableau principal (le nombre de colonnes) dans l'opérateur `[]`, un par dimension.

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
  { 7, 8, 9 }  // Troisième ligne
};
```

#### Taille de la matrice

Pour la taille de la matrice, on parlera plus simplement de son nombre de lignes et de colonnes qui sont, respectivement, la taille du tableau de la première dimension et la taille des tableaux de la deuxième dimension. On peut récupérer ces informations comme on le ferait pour un tableau quelconque.

```java
int[] m = new int[] { 
  { 1, 2, 3 }, 
  { 4, 5, 6 }, 
  { 7, 8, 9 } 
};

int nbLines = m.length;
int nbColumns = m[0].length; // m[0] = première ligne
```

#### Élements de la matrice

On accède aux **lignes** d'une matrice de la même façon qu'un tableau, avec l'opérateur `[]`, et aux éléments d'une ligne en réutilisant l'opérateur `[]` sur la ligne récupérée.

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

On parlera en général de coordonnées *i* et *j* des éléments dans la matrice :
- i est l'indice de la ligne, à utiliser dans les premiers `[]`
- j est l'indice de la colonne, à utiliser dans les deuxièmes `[]` (les crochets qui s'appliquent donc sur la ligne, le tableau, récupérée par les premiers crochets)

// TODO Schéma

#### Parcourir une matrice

Pour parcourir une matrice, c'est-à-dire pour *itérer* sur chacun de ces éléments, il faudra utiliser des boucles imbriquées dont les explications sont disponibles dans la leçon [06 - Boucles](cours/06-boucles.md).