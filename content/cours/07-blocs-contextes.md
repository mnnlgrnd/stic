---
title: "07 - Blocs et contextes"
prev_class: "06-fonctions"
next_class: "08-recursivite"
---

## Blocs

Un *bloc de code* est une série de lignes de code délimitée par des accolades `{}`. Ces blocs sont, comme vu précédemment, liés à des [branchements conditionnels](cours/04-alternatives), des [boucles](cours/05-boucles) ou des [fonctions](cours/06-fonctions.md). Chaque bloc a son propre *contexte*.

## Contexte et portée
La *portée* d'une variable définit dans quel contexte celle-ci est visible par du code et donc utilisable. Chaque bloc a accès aux variables déclarées dans son propre contexte et à celles déclarées dans le contexte "parent" ou englobant.

```java
int i = 0;
int j = 1;

if (i == 0) {
  // Début du contexte du if, on a accès aux variables i et j
  int k = 2 * j; // La variable k est locale au contexte du if
  println(k);
}

// A partir d'ici, k n'existe plus

```

> ℹ Une indentation correcte du code permet de facilement voir les différents niveaux de contextes

### Global

Le contexte global est le contexte principal d'exécution du programme dans lequel on va retrouver des variables globales, des branchements, des boucles, des définitions de fonctions, etc.

### Branchements et boucles

Les contextes des branchements conditionnels et des boucles sont des "sous" contextes, des contextes englobés dans d'autres contextes. 

Pour les boucles, chaque *itération* de la boucle est un contexte différent. Le contexte d'une itération prend fin quand on arrive au bout de l'exécution de cette itération.

### Fonctions

Pour les fonctions, chaque *appel* de fonction est un contexte différent et **indépendant**, le contexte parent de l'appel de la fonction est le contexte global et non le bloc de code dans lequel se trouve l'appel à cette fonction. Les paramètres de la fonction sont également des variables locales à chaque appel de la fonction dont la valeur est celle qu'on a passée dans l'appel.

```java
int i = 1; // Variable globale

if (i > 0) {
  int j = 1; // Variable locale
  foo(j + i); // Appel de fonction
}

void foo(int k) {
  int j = k; // Variable locale, le j dans le if n'est pas visible ici
  println(i, j); // Affiche 1 2
}
```