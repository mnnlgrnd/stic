---
title: "03 - Matrices"
prev: "tableaux"
next: "fonctions"
---

## Définition

Un tableau étant un type
Une matrice est un **[tableau](cours/tableaux.md) de tableaux**, c'est-à-dire que chaque élément du tableau est une référence vers un autre tableau d'un même type de données. Conceptuellement, on peut facilement représenter une matrice comme une table à deux dimensions (comme dans Excel, par exemple). On parlera ainsi de lignes pour la première dimension et de colonnes pour la deuxième dimension.

## Déclaration

Pour déclarer une matrice, il faut simplement déclarer un tableau dont le type d'éléments est lui-même tableau : pour un tableau d'entiers `int[]`, un tableau de tableau d'entiers sera noté `int[][]`. 

Pour déclarer une matrice d'entiers, il suffit donc de déclarer un [tableau](cours/tableaux.md) dont le type est lui-même un tableau, c'est-à-dire en rajoutant `[]` après le type d'éléments du tableau.

```java
int[][] t1; // Tableau de tableaux d'entiers
float[][] t2; // Tableau de tableaux de float
boolean[][] t3; Tableau de tableaux de booléens
```

## Création